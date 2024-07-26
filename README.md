# betting-against-beta

This brief note provides details about the implementation of Betting Against Beta strategy. I used SP500 historical dataset spanning from 2000-01-01 to the end of March 2024. The source of SP500 historical constituents is the following link:
https://github.com/fja05680/sp500/blob/master/S%26P%20500%20Historical%20Components%20%26%20Changes(04-08-2024).csv

The strategy in a nutshell
The idea behind the strategy is to short the stocks with the largest and long the stocks with the smallest betas. It is based on the idea that low-beta (low-risk) stocks tend to outperform high-beta (high-risk) stocks on a risk-adjusted basis.
Some data cleaning has been done, such as deleting several tickers with obvious data errors, e.g., stock trading at $21 at a particular date, and at $0.16 the next day. Once the dataset is ready, I calculate a stock beta using excess market returns and excess stock returns. As a risk-free rate I took 13-week Treasury bill with the ticker IRX from yfinance. 
Beta is computed on the last day of a month on a 1-year period data. Let’s say, I estimate beta on 2005-03-31; then I’ll use historical data from 2004-04-01 to 2005-03-31. Once betas are calculated, I sort stocks based on their betas, and select the 5 stocks with the highest and 5 with the lowest betas. 
The short and long trades are opened the next day, i.e., the first day of the next month. The holding period is 30 days. All positions are leveraged or deleveraged to the beta of 1. What this means is that if the beta of a stock is higher than 1, it’s deleveraged to 1; if it’s lower than, it’s leveraged to 1. For example, if a beta is 0.25, 4:1 leverage is applied which magnifies a return for that stock for that period by 4. The same logic applies to high-beta stocks. 
To avoid very large beta factors, stocks with the betas lower than 0.2 were dropped. Let’s say, beta for a stock during a particular period was 0.0015. We must apply 1/0.0015, or about 555 beta factor to leverage this stock to the beta of 1. In the future we can consider other weighting factors, such as the inverse of the stock’s volatility.

Results
The strategy delivered 20.95% annual rate with the max drawdown of 83.84%. Sharpe ratio is 0.162.
![image](https://github.com/user-attachments/assets/7057fc08-6ed0-4c90-84cb-85bc096c7e0b)

 
