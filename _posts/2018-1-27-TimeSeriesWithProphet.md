---
layout: post
title: Time Series Analysis with Facebook's Prophet
---

Not quite a year ago (I am writing this on January 27, 2018), Facebook released its **Prophet** forecasting tool for Python. **Prophet** is an interface built on **PyStan**, making it relatively to do time series analysis based on Bayesian methods. **Prophet** has a lot of features to help with time series analysis. For one, Having recently learned of the existence of **Prophet** I wanted to take it for a test run and see what kind of results I could get with it. I decided to use a what I thought would be a pretty unpredictable time series for my data: Bitcoin prices starting from January 1, 2012 through January 8, 2018.

The data was taken from Bitstamp exchange and can be found [here](https://www.kaggle.com/mczielinski/bitcoin-historical-data). Though the original dataset included prices by the minute, I restricted the data to once daily prices to limit computing time. In order to use **Prophet**, data must be organized into a dataframe with datetime data in a column labeled 'ds' and the regressors in a column labeled 'y'. In order to both linearize our data and stabilize the variance, we perform a logarithmic transformation on our prices. (There are a number of reasons *not* to apply a log transform here, but this will do the trick for the purposes of this post). We then declare a Prophet object and fit it as we would a Scikit-Learn object. You'll notice that I've held out the last 26 weeks of 2017 from our training set for validation. 

![table](https://github.com/t-ricco/t-ricco.github.io/tree/master/images/prophet1.png)

Given that we know the rapid rate of increase in bitcoin price that took place over that time period, I don't expect our model to come very close to predicting it, but I'm curious how far off the model is.

We then set up a new dataframe with the `make_future_dataframe` method. In this case we'll be projecting out 365 days. After predicting our data we can visualize the results with the `plot` method supplied by **Prophet**. 

![plot_log](https://github.com/t-ricco/t-ricco.github.io/tree/master/images/prophet2.png)

What we see is the transformed data points along with the projected values. The visible colored band about the trendline represents the 80% confidence interval. We'll have to do a little bit more work if we want to see the results to our original scale in USD. 

![plot_actual](https://github.com/t-ricco/t-ricco.github.io/tree/master/images/prophet3.png)

Looking at that graph we do indeed see that the actual price of Bitcoin does indeed range outside that 80% confidence interval. Interestingly, after a price correction in December, the actual values do fall back within the 80% confidence interval. This suggests that the model gives a pretty good picture of the range of potential outcomes.


One of the features of **Prophet** is the fact that it can account for yearly, weekly, and daily seasonality. (It also can account for holiday seasonality, but we'll leave that exploration for another day.) We can view how those seasonal components are used in our model with the `plot_components`  method.

![components](https://github.com/t-ricco/t-ricco.github.io/tree/master/images/prophet4.png)

For comparisons sake, I looked at what a **Prophet** model would project for the price of Bitcoin going forward if it was trained on all available data. When I did that I got the following result.

![plot_all_data](https://github.com/t-ricco/t-ricco.github.io/tree/master/images/prophet4.png)

We can see that this model doesn't even accurately reflect the current price of Bitcoin, even though it was trained using those data. Of course, part of the problem is the extreme increase in Bitcoin price that is out of line with recent history. The other problem is that since we fit our model on the log of the price, errors were inflated greatly when exponentiating back to USD scale. The take away here is that no matter how sophisticated or up to date the machine learning tool brought to bear on a problem, we as data scientists still need to analyze, interpret, and update our models.

