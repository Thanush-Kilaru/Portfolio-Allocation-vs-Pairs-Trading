# Portfolio-Allocation-vs-Pairs-Trading

## Introduction
The project's objective is to contrast the Pair Trading Strategy(using mean reversion) with the Portfolio Allocation Strategy. The Indian Equities Market is included in the project's purview.
Our goal was to use the Sharpe, Sortino, and Calmar ratio to conduct a comparative comparison.

According to the aforementioned presumptions, it was discovered that the pharmaceutical and financial services sectors benefit more from allocation.

The technology, auto, and private banks basket sectors appear to be more suited for pairs trading.

The Sortino and Calmar ratio measures, which account for the downside risk and drawdown connected with a specific strategy, are recommended to be used in addition to the Sharpe ratio statistic.

## More About the Ratios
For both strategies, I employed a triplet, or 3 stocks, as opposed to a pair. I would base my comparison of the effectiveness of the above strategies on the following ratios:
* Sharpe
* Sortino
* Calmar

### Sharpe Ratio
It is the ratio for comparing reward (return on investment) to risk (standard deviation). This allows us to adjust the returns on an investment by the amount of risk that was taken in order to achieve it.

<img src="./static/Screenshot 2022-11-04 at 15.39.18.png"/>

* 𝑅 - annual expected return of the asset in question.
* 𝑅𝑓 - annual risk-free rate. Think of this as a deposit in the bank earning x% per annum.
* 𝜎 - annualized standard deviation of returns

### Sortino Ratio
The Sortino ratio is very similar to the Sharpe ratio, the only difference being that where the Sharpe ratio uses all the observations for calculating the standard deviation,  the Sortino ratio only considers the negative variance.

The rationale for this is that we aren't too worried about positive deviations, however, the negative deviations are of great concern, since they represent a loss of our money. This is given by the following formula:

<img src="./static/Screenshot 2022-11-04 at 16.04.44.png"/>

* R - annual expected return of the asset in question.
* 𝑅𝑓 - annual risk-free rate.
* 𝜎 - annualized downside standard deviation of returns

### Calamar Ratio
This is similar to the other ratios, with the key difference being that the Calmar ratio uses max drawdown in the denominator as opposed to standard deviation.

<img src="./static/Screenshot 2022-11-04 at 16.04.53.png"/>

* R -  annual expected return of the asset in question.
* 𝑅𝑓 - annual risk-free rate.

For simplicity of calculations, I have considered Rf to be 0, for all ratios.

## Portfolio Allocation Strategy Methodology
At first, I computed the Sharpe ratio. The procedure was as follows:

* I imported the relevant stock data from Yahoo Finance.
* Then I calculated the Return of the Adjusted Close prices using the pct_change() method.
* After that, I calculated the mean of returns and the covariance matrix. The covariance matrix tells us about the relationship between the movement of 2 stocks.
* In order to run a simulation, I first had to create a matrix. Since I planned to run 10000 simulations, I initialized the rows to be of the number 10000. In the said matrix, I wanted to display the Mean returns, Standard deviation, Sharpe ratio, and the 3 stocks. Hence the matrix would be of the order 10000 x 6.
* The 3 ‘stocks’ columns would display their respective weightage in the portfolio. The idea was to randomize the weightage of the stocks in the portfolio (The weights are assigned inside a 'for loop').
* Initially, all the values in the matrix are displayed as zero because no values are fed to it.
* The main computation takes place inside the 'for loop'.
* Portfolio return is calculated as follows:<br/>
  𝑃𝑜𝑟𝑡𝑓𝑜𝑙𝑖𝑜 𝑟𝑒𝑡𝑢𝑟𝑛=𝑀𝑒𝑎𝑛 𝑟𝑒𝑡𝑢𝑟𝑛𝑠∗𝑤𝑒𝑖𝑔ℎ𝑡𝑠∗252

Where 252 is the number of trading days in a year

Portfolio Standard deviation is calculated as follows:
𝑃𝑜𝑟𝑡𝑓𝑜𝑙𝑖𝑜 𝑆𝑡𝑎𝑛𝑑𝑎𝑟𝑑 𝑑𝑒𝑣𝑖𝑎𝑡𝑖𝑜𝑛= √(𝑤𝑒𝑖𝑔ℎ𝑡𝑠)∙((√𝐶𝑜𝑣𝑎𝑟𝑖𝑎𝑛𝑐𝑒 𝑀𝑎𝑡𝑟𝑖𝑥)∙(√𝑤𝑒𝑖𝑔ℎ𝑡𝑠))

The Portfolio Standard deviation is the square root of the dot product of weights and dot product of Covariance matrix and weights.

Then we calculate the Sharpe ratio by dividing the portfolio return by the Portfolio Standard deviation.<br/>
𝑆ℎ𝑎𝑟𝑝𝑒 𝑟𝑎𝑡𝑖𝑜= 𝑃𝑜𝑟𝑡𝑓𝑜𝑙𝑖𝑜 𝑟𝑒𝑡𝑢𝑟𝑛/𝑃𝑜𝑟𝑡𝑓𝑜𝑙𝑖𝑜 𝑆𝑡𝑎𝑛𝑑𝑎𝑟𝑑 𝑑𝑒𝑣𝑖𝑎𝑡𝑖𝑜𝑛

* We then populate the ‘zero’ matrix with the required values.
* Our aim is to find the following portfolios: One with the maximum Sharpe ratio and the other with the least Standard deviation.
* For that we use the ‘iloc’ functionality of pandas, to locate the following rows.
* The ‘iloc’ functionality is used in conjunction with ‘idxmax’ and ‘idxmin’ functionalities to compute the portfolios with the maximum Sharpe ratio and the least Standard deviation respectively.
* At the end, we plot our results using the matplotlib library.

## Procedure for computing the Sortino ratio

The procedure is similar to calculating the Sharpe ratio. The difference lies in the for loop i.e the calculations inside it
* First I calculated the daily portfolio return 
* Then I calculated the mean of the portfolio return (using the mean() method ) and multiplied it by 252, in order to annualize the return. 
* In order to calculate the downside Standard deviation, I only considered those Portfolio returns which were negative (using the np.where method as a filter). The Standard deviation was calculated using the std() method.
* After that I calculate the Sortino ratio:<br/>
 𝑆𝑜𝑟𝑡𝑖𝑛𝑜 𝑅𝑎𝑡𝑖𝑜= 𝐴𝑛𝑛𝑢𝑎𝑙𝑖𝑠𝑒𝑑 𝑃𝑜𝑟𝑡𝑓𝑜𝑙𝑖𝑜 𝑟𝑒𝑡𝑢𝑟𝑛/𝐷𝑜𝑤𝑛𝑠𝑖𝑑𝑒 𝑆𝑡𝑎𝑛𝑑𝑎𝑟𝑑 𝑑𝑒𝑣𝑖𝑎𝑡𝑖𝑜𝑛

After using the ‘iloc’ functionality as I had done whilst calculating the Sharpe ratio, I plotted the results using the matplotlib library.

## Procedure for calculating the Calmar ratio

The procedure is similar to calculating the Sharpe ratio. The difference lies in the for loop i.e the calculations inside it
* First I calculated the daily portfolio return
* After that, I created a function called maximum drawdown. This function is used to calculate the drawdown as follows:<br/>
𝐷𝑟𝑎𝑤𝑑𝑜𝑤𝑛= 1−(𝑃𝑜𝑟𝑡𝑓𝑜𝑙𝑖𝑜 𝑟𝑒𝑡𝑢𝑟𝑛.𝑅𝑢𝑛𝑛𝑖𝑛𝑔 𝑀𝑎𝑥) <br/>
* Portfolio return can be thought of as equity and running max as Peak drawdown equity. Running Max is always greater than or equal to Portfolio return.
* After that, I computed the maximum drawdown using the max() function
* Once this was done, I proceeded to calculate the Calmar Ratio as follows: <br/>
𝐶𝑎𝑙𝑚𝑎𝑟 𝑟𝑎𝑡𝑖𝑜= 𝑃𝑜𝑟𝑡𝑓𝑜𝑙𝑖𝑜 𝑟𝑒𝑡𝑢𝑟𝑛/𝑀𝑎𝑥𝑖𝑚𝑢𝑚 𝐷𝑟𝑎𝑤𝑑𝑜𝑤𝑛 <br/>

After using the ‘iloc’ functionality as I had done whilst calculating the Sharpe ratio, I plotted the results using the matplotlib library.

## Procedure for the Pair trading strategy
At first, I imported the data from Yahoo finance.

* Unlike the Portfolio Allocation strategy, I am only interested in the price series. Hence I only imported the Adjusted Close series and did not calculate the return. <br/>

After that, I plotted the series using the plot() method.

* Now we get into the nitty-gritty of the pair trading strategy. I started by calculating the hedge ratio.
* The Hedge ratio tells us about the number of shares we have to buy/sell for the strategy to remain mean reverting.
* For e.g.  I buy a share of  X, and the hedge ratio for Y is 1.29 and for Z is -2.29. This means that when I buy a share of X, I need to sell 1.29 shares of Y and buy 2.29 shares of Z for the strategy to remain mean reverting.
* Then I calculated the spread of the strategy. The spread is the difference between the long position and the short position.

Then I plotted the spread.

* For a pair trading strategy, the spread must be stationary. To check this, we perform a statistical test called the ADF test.
* To satisfy the ADF test, the P-value at ADF index 0 i.eADF[0] must be less than the P- values at ADF index 4 i.e ADF[4].<br/>

After that, I created a function called ‘stat_arb’ and the values fed to it were the Adjusted Close price, the lookback period and the Standard deviation.

* The ‘stat_arb’ was created so that I could generate signals for the pair trading strategy. The signals are generated using Bollinger bands. The Bollinger band consists of 3 lines: the moving average, lower band and upper band.
* Inside the function, I calculated the Moving Average and the Moving Standard Deviation. Lookback was used as a value for the rolling window.

Then I computed the Upper band and the Lower band:

* Upper Band = Moving Average + Standard Deviation * Moving Standard Deviation

* Lower Band = Moving Average - Standard Deviation * Moving Standard Deviation

Then I created the entry and exit positions for the long and short positions.

* A long entry is when the spread is lesser than the lower band.
* A long exit is when the spread is greater than or equal to the moving average.
* A short entry is when the spread is greater than the upper band.
* A short exit is when the spread is lesser than or equal to the moving average.
* An exit is denoted by 0. Along entry is denoted by 1 and a short entry is denoted by -1.
* A net position is the summation of long and short positions.

Then I calculated the spread difference so that I could calculate the pnl. The spread difference is Today’s spread – The previous day’s spread. The pnl is the spread difference multiplied by the net positions. The net position is shifted by 1 i.e the previous day, in order to avoid the look-ahead bias.

After that, I calculated the cumulative pnl. The strategy returns are needed to calculate the Sharpe, Sortino and Calmar ratio. To calculate the strategy returns I first need to calculate the percentage change of spread.

𝑃𝑒𝑟𝑐𝑒𝑛𝑡𝑎𝑔𝑒 𝑐ℎ𝑎𝑛𝑔𝑒 𝑜𝑓 𝑠𝑝𝑟𝑒𝑎𝑑=(𝑇𝑜𝑑𝑎𝑦′𝑠𝑝𝑟𝑒𝑎𝑑−𝑃𝑟𝑒𝑣𝑖𝑜𝑢𝑠 𝑑𝑎𝑦′𝑠 𝑠𝑝𝑟𝑒𝑎𝑑)/( 𝑝𝑎𝑟𝑎𝑚𝑒𝑡𝑒𝑟 0∗𝐴𝑑𝑗𝑢𝑠𝑡𝑒𝑑 𝐶𝑙𝑜𝑠𝑒 𝑜𝑓 𝑆𝑡𝑜𝑐𝑘 𝐵∗𝑆ℎ𝑖𝑓𝑡(1)+(𝑝𝑎𝑟𝑎𝑚𝑒𝑡𝑒𝑟 0∗𝐴𝑑𝑗𝑢𝑠𝑡𝑒𝑑 𝐶𝑙𝑜𝑠𝑒 𝑜𝑓 𝑆𝑡𝑜𝑐𝑘 𝐶∗𝑆ℎ𝑖𝑓𝑡(1)+𝑆𝑡𝑜𝑐𝑘 𝐴

𝑆𝑡𝑟𝑎𝑡𝑒𝑔𝑦 𝑟𝑒𝑡𝑢𝑟𝑛𝑠=𝑛𝑒𝑡 𝑝𝑜𝑠𝑖𝑡𝑖𝑜𝑛.𝑠ℎ𝑖𝑓𝑡(1)∗𝑝𝑒𝑟𝑐𝑒𝑛𝑡𝑎𝑔𝑒 𝑐ℎ𝑎𝑛𝑔𝑒 𝑜𝑓 𝑠𝑝𝑟𝑒𝑎𝑑

The net position is shifted by a day to avoid look-ahead bias.

Then I calculated the cumulative product of strategy returns (cumulative returns) and plotted it on a graph. In another cell, I plotted the cumulative returns with the

Then I proceeded with calculating the drawdown (required to calculate the Calmar ratio).

1− (𝐶𝑢𝑚𝑢𝑙𝑎𝑡𝑖𝑣𝑒 𝑟𝑒𝑡𝑢𝑟𝑛𝑠/𝑅𝑢𝑛𝑛𝑖𝑛𝑔 𝑀𝑎𝑥)

Cumulative returns can be thought of as the equity and Running max as Peak equity. Running max is always greater than or equal to Cumulative returns.

Then I plot the drawdown.

After that, I proceeded with calculating the Sharpe, Sortino and Calmar ratio.

𝑆ℎ𝑎𝑟𝑝𝑒 𝑟𝑎𝑡𝑖𝑜= 𝑀𝑒𝑎𝑛 𝑜𝑓 𝑆𝑡𝑟𝑎𝑡𝑒𝑔𝑦 𝑟𝑒𝑡𝑢𝑟𝑛𝑠/(𝑆𝑡𝑎𝑛𝑑𝑎𝑟𝑑 𝑑𝑒𝑣𝑖𝑎𝑡𝑖𝑜𝑛 𝑜𝑓 𝑆𝑡𝑟𝑎𝑡𝑒𝑔𝑦 𝑟𝑒𝑡𝑢𝑟𝑛𝑠∗ √252)

𝑆𝑜𝑟𝑡𝑖𝑛𝑜 𝑟𝑎𝑡𝑖𝑜= 𝑀𝑒𝑎𝑛 𝑜𝑓 𝑆𝑡𝑟𝑎𝑡𝑒𝑔𝑦 𝑟𝑒𝑡𝑢𝑟𝑛𝑠/(𝑆𝑡𝑎𝑛𝑑𝑎𝑟𝑑 𝑑𝑒𝑣𝑖𝑎𝑡𝑖𝑜𝑛 𝑜𝑓 𝑛𝑒𝑔𝑎𝑡𝑖𝑣𝑒 𝑆𝑡𝑟𝑎𝑡𝑒𝑔𝑦 𝑟𝑒𝑡𝑢𝑟𝑛𝑠∗ √252)

* To calculate the Calmar ratio, I needed the Average annual return and the Maximum drawdown. 
* To calculate the Average annual return, I require the last value of cumulative returns and the years.
* To calculate the years I need to count the number of years and divided it by  252i.e the number of trading days.

𝐴𝑣𝑒𝑟𝑎𝑔𝑒 𝑎𝑛𝑛𝑢𝑎𝑙 𝑟𝑒𝑡𝑢𝑟𝑛=(𝐹𝑖𝑛𝑎𝑙 𝑣𝑎𝑙𝑢𝑒 𝑜𝑓 𝐶𝑢𝑚𝑢𝑙𝑎𝑡𝑖𝑣𝑒 𝑟𝑒𝑡𝑢𝑟𝑛)1/𝑦𝑒𝑎𝑟𝑠−1

𝐶𝑎𝑙𝑚𝑎𝑟 𝑟𝑎𝑡𝑖𝑜= 𝐴𝑣𝑒𝑟𝑎𝑔𝑒 𝑎𝑛𝑛𝑢𝑎𝑙 𝑟𝑒𝑡𝑢𝑟𝑛/𝑀𝑎𝑥𝑖𝑚𝑢𝑚 𝑑𝑟𝑎𝑤𝑑𝑜𝑤𝑛

## Results
<img src="./static/Screenshot 2022-11-04 at 15.58.01.png"/>
<img src="./static/Screenshot 2022-11-04 at 15.58.14.png"/>
<img src="./static/Screenshot 2022-11-04 at 15.58.25.png"/>

## Conclusion and future implications
The big assumption made:
We can only invest in specific stocks from the selected sectors.

Further, we assumed that the margin required to put on a pair trade is:

* This is from the percentage change of the spread equation.
* In reality, the broker can charge much more margin for overnight positions in the futures.
* Our aim was to perform a comparative analysis under the assumptions and limitations.

Under the above assumptions, it was found that:

* Allocation works better for the following sectors: Pharmaceuticals and Financial Services basket
* Pair Trading seems to be a better alternative for the following sectors: Technology, Automobile, and Private Banks basket

The Portfolio allocation strategy generates alpha from correct security selection and the weightage assigned to the stocks. The pair trading strategy generates its alpha from the pair selection and the mean reversion process (Learn Mean Reversion Strategy in detail in the Quantra course).

In the Pair trading Strategy, I have gone ahead with implementing the strategy in spite of it not fulfilling the ADF test criteria.

* What is the advantage of using either strategy?
The advantage of a Pair Trading Strategy is that it is market neutral.

* What are the limitations?
Short selling for overnight positions is not allowed in the Indian cash Equities Market. Shorting is allowed in the Futures segment. In such a situation, portfolio allocation strategy takes the cake as much less margin is required.

Shorting is difficult with the Pair Trading Strategy as there is much more margin required. In a bear market, the Portfolio allocation strategy has a higher chance of performing worse.

