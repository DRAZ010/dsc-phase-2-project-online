# The King County Real Estate Project
By: David Rasmusen
Date: 10/2020

## Introduction
The Seattle area is one of the most expensive real estate markets in the United States. 
The scope of this project is to determine what factors most impact price.  This information is valuable to anyone looking to assess an entry into the Seattle real estate market.  This could either be an investor or potential resident.  I would love to move out of Iowa and break in to the Seattle market.

## The Data Provided

Here is the data provided by the flatiron school relating to the real estate in King County:
 * Date the property sold
 * The price the property sold at
 * The number of bedrooms and bathrooms
 * Square footage information
 * If the property has a view of the waterfront
 * What the condition and grade the property is in
 * When the property was built and if/when it had been renovated
 * The latitude and longitude of each property


## Technologies utilized

- Python
- QGIS
- Plotly
- Seaborn
- Pandas
- Numpy
- Sci-kit Learn
- Statsmodel


## Questions addressed

### Where are the most expensive places to live?
Let's face it, most of us have budget constraints.  An old cliche comes to mind: the three most important factors when considering real estate are location, location and location!  As I was provided pricing and longitude and latitude data it was simply a function of overlaying price on top of the location data.  Here is graph:

![Imgur](https://i.imgur.com/3rmFEhI.png)

For context, here is a map of the King Country with zip codes included.

![Imgur](https://i.imgur.com/A0SciBt.png)

As you can see the most expensive real estate is clustered around Lake Washington.  Specifically, prices are highest in the following zip codes 98033, 98039, 98004 and 98040.  

Conclusion:  We can infer that these locations have more desirable attributes given their higher prices. 

### How strong is the relationship between price and the bedroom/bathroom ratio?

It would be nice if I didn't have to share a bathroom with someone. So naturally the question is, how much more must I spend for each additional bathroom per bedroom.  Here is how the relationship looks graphically:

![Imgur](https://i.imgur.com/X1E3We9.png)

As expected, as the bed/bath ratio climbs the price of the property tends to be lower.  To confirm this mathematically, I did a quick correlation calculation:  -0.23  
 
Conclusion:  There is a negative but not strong relationship between price and the number of bedrooms that share a bathroom.

### Which variables most impact price?

We have established that there is a discernible relationship between price and location and a fairly weak relationship between price and the number of bedrooms that share a bathroom. Let's directly look at which variables in the data have the strongest relationship to price.  Perhaps the most concise way to look at how all the variables are related is with a correlation matrix.  I narrowed the matrix down to variables with at least a correlation absolute value of 0.2. Here is a result:

![Imgur](https://i.imgur.com/t6FLbxO.png)

Conclusion:  It looks like grade has the highest impact on price with a correlation of 0.63.  There really isn't anything surprising about the directional correlation between each variable but the strength or absolute value of the correlation will help select predictive variables in a regression model.  It is also important to consider cross correlations to avoid multicollinearity.

As grade has the strongest relationship, I looked into the King County grading system for further information.  The grade scores are on a scale between 1 and 12 and here are the definitions:

1-3 Falls short of minimum building standards. Normally cabin or inferior structure.

4 Generally older, low quality construction. Does not meet code.

5 Low construction costs and workmanship. Small, simple design.

6 Lowest grade currently meeting building code. Low quality materials and simple designs.

7 Average grade of construction and design. Commonly seen in plats and older sub-divisions.

8 Just above average in construction and design. Usually better materials in both the exterior and interior finish work.

9 Better architectural design with extra interior and exterior design and quality.

10 Homes of this quality generally have high quality features. Finish work is better and more design quality is seen in the floor plans. Generally have a larger square footage.

11 Custom design and higher quality finish work with added amenities of solid woods, bathroom fixtures and more luxurious options.

12 Custom design and excellent builders. All materials are of the highest quality and all conveniences are present.

13 Generally custom designed and built. Mansion level. Large amount of highest quality cabinet work, wood trim, marble, entry ways etc.

## Linear Regression

The rubric of our second project at flatiron included linear regression. This is a precursor to machine learning later in the bootcamp and a good skill to hone in business.  The model enables one to predict price, in this case, if you know a few of the underlying variables.  Out of the data provided I had to narrow the independent variables down to reduce the impact of multicollinearity.

As mentioned the predicted or dependent variable is price.  The predictive or independent variables are as follows:
* Grade
* The Bedroom to Bathroom ratio
* A dummy variable that indicates whether or not the property is located in the expesive zip codes mentioned above: 98033, 98039, 98004 and 98040.

Here are the model results which inlclude the coefficients needed to establish the predictive regression model:

![Imgur](https://i.imgur.com/tGUgj8l.png)

Model Conclusions:
* All P values are low indicating that each variable is significant.  
* A coefficient of determination, or R-squared, at 87% indicates a highly predictive model.
* In other words 87% of the variation in dependent variables are explained by the independent variables.
* A Durbin-Watson of 2 means that there is no autocorrelation amongst the residuals.
* The high Jarque-Bera indicates that the residuals are not normally distributed which is an issue.
* Based on q-q plot, significant heteroskedasticity exists. The residuals vary with price. There is more noise in the model as price increases.

## Further Research
Here are some issues that I would like to further explore if given the time and data required:
* A look at pricing data through time at each propriety to assess price changes through time.  The current data provided is only a snaposhot in time. Time series data would better enable an investor to identify trends.
* Demographic data to look for areas most attractive to young professionals, the elderly and families.
* King County economic data to assess real estate price sensitivity through the business cycle.
* How each school disctrict impacts the relative value of real estate.
* Proposals to address affordable housing and gentrification issues.




