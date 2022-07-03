# Unsung Real Estate Agency Project
_by Nick P. Kimani_


## Business problem
Unsung real estate agency is an agency in King County that deals with clients who want to buy/sell homes.

They want to create an algorithm and use it to make a model for pricing of houses:
- The primary purpose of the model is to predict buying/selling prices of houses.
- The secondary purpose is for inferring features/atrributes that significantly affect the pricing of a house. 

By completing this, the business is at a better position to advise clients who want to buy/sell homes with factual information about homes, their costs or selling prices and exactly why their prices are as they are.


## Data 
I dealt with the original data(that was sourced externally) in the `Data cleaning notebook`, `Housing data` in the `data` folder has a couple of missing values which I filled with 0 after some considerations, and inappropriate records such as '?' in `sqft_basement` which I also replaced with 0. This is based on the assumption that such records mean that a house doesn't have that feature. After these minor tweaks I exported a new dataframe called `Cleaned data` which is what I use when making the model.

The new `cleaned data` has records for the year 2014 May - 2015 May. The data has no missing records or inappropriate datatypes. There are 21597 records of homes in King County, with their attributes, renovation year if any, and their selling price. 

After completing the model, I exported a csv file called `model features and coefficients` of the fetures and respecive coefficients(which are in dollars) for the agency to use when estimating the value of a house.

This information is significant for me to use when modelling and solving the business problem.

A description of some of the columns we are going to use:

- The target is __`price`__ which is the pricing/value of a house.
- `id` is a unique identifier of a house.
- `date` is the date a house was sold.
- `sqft_lot` is the area of the whole plot of land.
- `sqft_living` is the area which the house/home takes in the plot.
- `floors` are the levels in a house.
- `waterfront` is whether a house has a view of a waterfront or not.
- `bedrooms`and `bathrooms` are the number of the respective rooms in a house.
- `condition` is the overall condition of a house.
- `grade` is the grading of a house.
- `yr_built` and `yr_renovated` represent the year a house was built and the year a house was renovated respectively

categorical features in our data are:

- bedrooms
- bathrooms
- floors
- waterfront
- view
- condition
- grade
- renovated


## Methods

### Exploratory data analysis
While exploring the data an oulier was found in `bedrooms` and I dropped that record. 

I then replaced `yr_built` with `home_age` to represent the age of a house at the time it was sold. Also I replaced `yr_renovated` with `renovated` that shows whether a house has had any renovations done(1s) or not(0s).

I also found out that `sqft_living` is the summation of `sqft_basement` and `sqft_above` and decided to drop the latter 2 columns.

I continued to drop some other columns that seemed not to add any value to our business problem, these include: id, zipcode, lat, long, sqft_basement15 and sqft_above15.

I found the most correlated feature to price is `sqft_living`.
![Correlation_of_features](https://user-images.githubusercontent.com/104377216/177055982-e36d1981-bf68-4200-b5c4-60808b0fc41d.jpg)

### Pre-processing
After the above process I started preprocessing the data. I did one-hot encoding on all the categorical features except `renovated` and `waterfront` because these two have binary categories.

Then I did min_max scaling on home_age and log transformation on sqft_living and sqft_lot.


## Results

### Pre-procesing
The price distribution was: ![Price distribution](https://user-images.githubusercontent.com/104377216/177053873-f2ba0491-5226-4c6a-bdd0-852bb96f2e4b.jpg)

home_age, sqft_living and sqft_lot final distribution before transformation was: 

![Home_Age histogram](https://user-images.githubusercontent.com/104377216/177055876-1bf910b1-f4cd-48d8-97cb-1fa8cceff8d2.jpg)
![Sqft_Living histogram](https://user-images.githubusercontent.com/104377216/177055905-08f0a265-b02b-4530-8914-b787ae9b2eaa.jpg)
![Sqft_Lot histogram](https://user-images.githubusercontent.com/104377216/177055923-15ab9e5d-05fa-47e6-a4ea-6242f799eb47.jpg)

After transfomation:

scaled_home_age:

![scaled_home_age](https://user-images.githubusercontent.com/104377216/177055805-6e053cbb-017d-4472-9ff9-804390807e41.jpg)

transformed_sqft_living:

![transformed_sqft_living](https://user-images.githubusercontent.com/104377216/177055830-3b09c764-9c44-4dd0-a18f-89a3e793757c.jpg)

transformed_sqft_lot:

![transformed_sqft_lot](https://user-images.githubusercontent.com/104377216/177055844-097426ff-718d-46f6-b0ea-49084ca36102.jpg)

### Modelling
The final model is a multiple polynomial model that has transformed_sqft_living_sq as the only polynomial feature.

The train model results are:

![Screenshot from 2022-07-04 00-25-13](https://user-images.githubusercontent.com/104377216/177057864-dbf846d9-668e-4dec-8c2e-273a6067d86e.png)
![Screenshot from 2022-07-04 00-25-02](https://user-images.githubusercontent.com/104377216/177057868-1a61056c-9ddb-4522-a0ff-b46e16a464ac.png)

The train score value is = 0.657

The test score value is = 0.6430696957773693

#### Does it follow the linear regression assumptions?

Normality check:
![Normality assumption](https://user-images.githubusercontent.com/104377216/177058022-6d6ee7c0-4367-4841-8b80-743ec88a497d.jpg)

Homoscedasticity check:
![Homoscedasticity assumption](https://user-images.githubusercontent.com/104377216/177058047-6dadc120-f5fb-42f6-b6f0-0052e779e4b4.jpg)

Linearity check:
![Linearity assumption](https://user-images.githubusercontent.com/104377216/177058065-b46d5b12-2211-4251-817b-c43ea699db87.jpg)

Although there are some outliers here and there, we can say that the model meets all assumptions of linear regression.


## Conclusion and recommendation

### Conclusion
According to our model a house has a base price of 15,880,000 dollars. The base price can be off by +(plus) or -(minus) 217,461.106 dollars. 

After checking the attributes for a house, appropriate changes are made to the price. For example a house having a poor grade reduces the price by ~302,900 dollars while a house having an excellent grade increases the price by ~861,900 dollars. For more information on this check `model features and coefficients.csv` in the data folder.

### Recommendations
More investigation into the relation of certain features to price should be done to have a better and more accurate understanding of how said features affect the price of a house. 

A more complete dataset where we don't have to fill in values would be much better because with such data a more accurate model could be made.
