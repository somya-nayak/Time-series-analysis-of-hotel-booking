# Background
As a newly minted MSBA you start working for a large resort hotel managing 1,877 rooms. A tour operator that you frequently do business with has requested a block of 
60 rooms for Aug. 22. As this operator will pay a discounted rate for each room, your manager is uncertain if she should give this block of rooms to the tour operator, 
and she has asked you to provide model-based support for this decision.

Although the price is discounted and it may prevent you from selling some of these rooms at the regular price, if you reject this request, any empty rooms will not 
generate any revenue and you would have incurred an opportunity cost by not selling these rooms.

After judicious consideration of the economic tradeoffs in the Newsvendor model, you and your manager determine that the block should be assigned to the tour operator 
only if the probability of your organic demand (excluding the room block in question) is smaller than 67% (i.e., you are on track to achieve a 67% service level).

# Data
To address the booking question, you examine the following data set and proceed to develop a demand forecast model. The data set Booking Exercise.csv consists of daily observations of the following six variables:
- DATE: Calendar date corresponding to each observation.
- DOW: Index (1-7) to indicate the day of the week each DATE corresponds to. This is redundant and it is eliminated below.
- DEMAND: Number of rooms actually sold on each DATE.
- TUESDAY.BOOK: Number of rooms booked on the Tuesday of the previous week for each day of the forthcoming week. This variable is used as an input to inform the forecasts of DEMAND for each day of the forthcoming week.
- PICKUP.RATIO: This is a calculated variable obtained as PICKUP.RATIO = DEMAND/TUESDAY.BOOK historically as DEMAND is observed. Because of this is a calculated relationship you can use either PICKUP.RATIO or TUESDAY.BOOK but you cannot use both variables simultaneously in a model to predict DEMAND.
- DOW.INDEX: This is a pre-calculated indicator of day-of-the-week demand intensity. This is obtained by the Hotel using information beyond what it is contained in this data set.

# Problem
Recommend your manager regarding the tour operator block. Should your manager sell the block of 60 rooms at a discounted price?

# Approach
- Load the data. The data is available for three months, filter out the last week's data for forecasting.
- Fit the following models to predict the DEMAND:
  - ETS 
  - ARIMA
  - Linear regression
  - Non-seasonal regression model with ARIMA errors using TUESDAY.BOOK and DOW.INDEX as explanatory variables
  - Seasonal regression model with ARIMA errors using only TUESDAY.BOOK as an explanatory variable
 - Ljung-Box test was used to test the validity of the models
 - AICc and BIC values were used to determine the best model
 - As per AICc and BIC values, the seasonal regression model with ARIMA errors model came out to be the best model to forecast the demand
 - The forecast data for the last week was used to forecast the demand, based on which the final recommendation was given
 
 # Recommendation
 The cut-off for Aug 22 as per 67% service level is 0.67*1877 i.e., 1258 rooms. As per the forecast, in average the organic demand for rooms on Aug 22 (excluding the room block in question) is going to be 1643 which is already satisfying the minimum service level and can be sold at regular price. The condition is the block should be assigned to the tour operator only if the probability of organic demand is smaller than 67%. As the organic demand is greater than 67%, the manager should not sell the block of 60 rooms at a discounted price.
