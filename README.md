# Insider-Trading-Analysis

(I've been working on a blog post for this repo, until then I'll use the readme file for explaining the analysis.)

Insider trading is the buying or selling of a security by someone who has access to material nonpublic information about the security. Insider trading can be illegal or legal depending on when the insider makes the trade. It is illegal when the material information is still nonpublic.

However, it is not illegal to own, or buy and sell shares of the company you work for, as long as the transactions are being disclosed publicly in a timely manner and as long as the information that is being used to trade is publicly available.
The Securities and Exchange Commission has rules to protect investments from the effects of insider trading. The SEC has prosecuted insider trading cases against Directors, officers and employees of involved corporations as well as tepees. 

When a corporate insider buys or sells his company's security this trading activity must be reported to the SEC, which then discloses this information to the public .Even though the trading is disclosed, Corporate Insiders can only trade their Corporation's Securities during certain windows of time when there is no material non-public information that might affect a buyer or seller's trading decision.
In this blog post I present the result of my Insider Trading Analysis , the code for which can be found in this repository.

I've scraped 30,000 rows of data from Insidertrading.org for the time period August 18 2016 to December 26 2017. This data contains features such as Transaction Date, Company Name, Company Stock Symbol, Insider Name, Transaction Volume, Price Per share etc.
Since the data didn't have the industry to which a company belongs to I matched up the Industry dataset from NASDAQ to the stock symbols in the above data.

Okay, let's first view the Insider activity over time for our dataset.

![](https://github.com/Ibtastic/Insider-Trading-Analysis/blob/master/plots/insider%20activity%20over%20time.png)

Most of the activity is concentrated between October 2016 to January 2017. Let's just zoom in to that time period.

![](https://github.com/Ibtastic/Insider-Trading-Analysis/blob/master/plots/zoomed%20in%20view.png)

The selling activity exceeds buying except for the data after December 25 and before Oct 16. Our data has :-

12427 rows for buying insider transactions 

17573 rows for selling insider transactions.

There is a peak in Insider activity between November 13 to November 15.

## Analyzing Distribution of number of Insiders per Company

Here, I have calculated the number of Insiders each company has and then grouped to find the number of companies that have a particular number of insiders.

![](https://github.com/Ibtastic/Insider-Trading-Analysis/blob/master/plots/distribution%20of%20number%20of%20insiders%20per%20company.png)

This plot is almost exponential having a heavy tail towards the left , indicating that **most companies have less number of insiders**. However, there are only a few companies (particularly involved in buying activity) that have a large number of insiders. This quite accurately reflects the real world scenario.

## Analyzing Distribution of number of transactions per Insider

In this section I'm doing quite the same thing as I did above but for numbers of transactions and insiders rather than number of insiders and companies.

![](https://github.com/Ibtastic/Insider-Trading-Analysis/blob/master/plots/Distribution%20of%20number%20of%20transactions%20per%20insider.png)

This is steeper and closer to the axis, let's have a zoomed-in view.

![](https://github.com/Ibtastic/Insider-Trading-Analysis/blob/master/plots/newplot.png)

Here too, we can find heavy tails, however the left tail is composed of heavy buying activity and right tail consists of heavy selling activity. Insiders involved in selling activities do a lot more transactions than those involved in buying activities. An insider can also be involved in both.

## Top companies involved in Insider Trading.
![](https://github.com/Ibtastic/Insider-Trading-Analysis/blob/master/plots/Top%20companies%20for%20insider%20activities.png)

Google's parent company Alphabet has around 550 insider cases. It is followed by DataWatch Corp. After that all the companies in the top 15 have roughly the same insider activity.

## Market Cap for Top Companies:

Let’s view the Market Cap of top companies listed on NASDAQ. Market capitalization is the aggregate market value of a company represented in dollar amount. It is calculated by multiplying a company's outstanding shares by the current market price of one share. 

Now, I'm going to visualize the companies that have the most insider activity during our observed time period.

![](https://github.com/Ibtastic/Insider-Trading-Analysis/blob/master/plots/marketcap.png)

Clearly the Market Cap of Alphabet and Facebook outshadows all the other companies. These are the only two Mega Cap Companies involved in Insider Trades. Salesforce Com Inc and HP are large caps. However most top companies involved are mid caps, small or micro cap. 

## Which Roles at Companies are most common for Insider Activity?

![](https://github.com/Ibtastic/Insider-Trading-Analysis/blob/master/plots/Insider%20activity%20for%20different%20roles.png)

Officers (CFOs, CEOs etc) followed by Directors are mostly involved in Insider trade . Officers, directors and employees of the comapny are called Corporate Insiders. Due to their roles and work tasks in the corporation ,these individuals possess information unavailabe to the public. They can exploit both bad and good news of the company before the news becomes public and can beat the average market.

## Which Industries are most common for Insider activities?

To analyze this I’ve removed the companies which were not listed on NASDAQ.

![](https://github.com/Ibtastic/Insider-Trading-Analysis/blob/master/plots/sectors.png)

Technology is the front-runner followed by Finance. This was expected as most of the top companies belonged to these sectors.

## Do Insiders trade in sync with the market?

In this plot I analyze Insider Selling activity(volume) over time against the SP500 volume over the same time.

![](https://github.com/Ibtastic/Insider-Trading-Analysis/blob/master/plots/Insider%20Selling%20activity%20vs%20SP500.png)

This plot clearly suggests that **Insiders are contrarians**. They tend to sell more when market buys and buy more when market sells.Insiders are found to be net buyers of relatively low P/E stocks and net sellers of relatively high P/E stocks.

## Short Term effects of Insider Trades on Stock prices

Following an Insider Transaction (Buy/Sell) , how does the stock price of the stock traded by insider changes? Since, Insiders work on privileged non-public information , we expect the stock prices to move in their favor. Let’s see what actually happens.
To analyze this I select a subset of top companies involved in Insider Trading. The subset includes Alphabet Inc, Facebook, First Bancorp, Synnex Corp, Central Pacific Financial Corp, Hewlett Packard Enterprise, Kulicke & Soffa Industries Inc and Saga Communications Inc.
Then I use Pandas Datareader to get stock prices of these stocks for the five days following the insider transaction from yahoo finance. Then I calculate the change in price over these days or returns of the stocks. I have used Adjusted Close rather than closing price because it’s the closing price of the day that has been slightly adapted to include any actions that occurred at any time before the next day’s open.

![](https://github.com/Ibtastic/Insider-Trading-Analysis/blob/master/plots/shortterm.png)

There are certainly a lot of outliers for Purchased Insider stocks the returns of which are in thousands. Let’s filter the returns down to 50 ,to view the boxplots clearly.

![](https://github.com/Ibtastic/Insider-Trading-Analysis/blob/master/plots/shortterm%20zoomed.png)

The returns on Purchased stocks increase following the transaction date and also get lesser negative.Clearly, the price of Insider Purchased stocks tend to rise during the days following the trade.

However, the returns on stocks sold by Insiders is negative. Using the private information, Insiders anticipate the decline in value of a certain stock and get rid of it before the price falls.

The expected short term trends followed by an Insider trading are clearly demonstrated by the plot.
An interesting theory called the “Copy Cat Theory” by Fried suggested that, “ abnormal price changes that occur after insiders’ trade are often not due to the release of specific news about their firms Instead, it is the stock prices move in reaction to the news of the trading itself: insiders’ excess returns occur not because of their access to non-public information , but because “market participants think insiders have inside information” and they copy-cat behaviors , which leads to the movement of the stock price favorable to the insider”.

## Are Insiders Farsighted? 

This is another debatable question in the Finance Industry . While Insiders are clearly able to fluctuate stock prices during the days immediately following the trade, are they able to anticipate long term returns on their trades? Do they beat the average stock market in the long run?
I answer these question for the data I used. 
To represent the broad market, I use the SP500 data from Yahoo Finance of the same dates as the Insider Transactions date. I then calculate returns after a month, six months and a year following the transaction.

![](https://github.com/Ibtastic/Insider-Trading-Analysis/blob/master/plots/longterm.png)

Again, there are outliers for Insider Purchased stocks where the returns are in thousands, and they seem to increase as time passes. Let’s zoom in the data, for a better view.

![](https://github.com/Ibtastic/Insider-Trading-Analysis/blob/master/plots/longterm%20zoomed.png)

Insiders do outperform the average market, in the long-run. The returns on the Purchased stocks increase as time passes. The blue boxplot is skewed towards the bottom, meaning that most of the purchased stocks experience less rapid increase in prices. 
Another eye-catching thing is the size of the boxplot, which makes me conclude that stocks traded by Insiders are more volatile than the broad market, especially Insider purchased stocks. It is riskier to invest in these kinds of stocks and the Insiders are certainly risk takers.

While the Insiders do well on purchased stocks, they certainly fail on long term returns of sold stocks, where the returns are in-turn positive. This can be attributed to the fact that there are numerous reasons other than inside information for Insiders to sell shares of their company.

In brief, Malkiel’s theory was helpful in explaining why insiders might sell their shares not considering private information as an input for the decision making process. Following the study of Malkiel regarding behavioral finance, people are seen far more distressed at taking losses than they are overjoyed at realizing gains. As a result, investors tend to take greater risks to avoid losses than they would to achieve equivalent gains; they tend to be more willing to discard their winners than selling their losers. Therefore, when insiders are observed to sell their stock, it might be mainly due to the fact that the stock has achieved their expected return and selling it will enable them to enjoy the success of being correct and not because they have seen any unfavorable trends.

## Triads of Trading Transactions:-
If you look closely you can find pairs or triads of transactions by Insiders where they first buy a stock on a very low price and sell it at a high price or vice versa probably all in the same day. 
I analyze such triads for Facebook.

![](https://github.com/Ibtastic/Insider-Trading-Analysis/blob/master/plots/fb%20triads.png)

I found three such incidents in Facebook’s insider triad incidents, two of which I’ve demonstrated above.	
The first incident occurred at 13th December 2016, in which FB first sold a stock at a price $ 121.078 and then bought it at a price $ 1.854. I denote the buying price as negative in the plots. Then again it purchased 8000 stocks at $ 119.21 each. This all happened in the same day, giving Facebook a net profit of $ 981,508.2
Such triads/pairs can easily be found by automation in the massive data of the trading activity of a company and can serve as a testament to Insider Activity or a basis of further investigation. 

