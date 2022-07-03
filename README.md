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

### Pre-processing
After the above process I started preprocessing the data. I did one-hot encoding on all the categorical features except `renovated` and `waterfront` because these two have binary categories.

Then I did min_max scaling on home_age and log transformation on sqft_living and sqft_lot.

## Results
The price distribution was: ![Price distribution](https://user-images.githubusercontent.com/104377216/177053873-f2ba0491-5226-4c6a-bdd0-852bb96f2e4b.jpg)

home_age, sqft_living and sqft_lot final distribution before transformation was: 
