

### Create conda environement
```
# $ conda create --name <env> --file algotrading-env.txt
```
### Create .env file with following variables

```
tweepyKey=
NEWS_API_KEY=
```

### Get twitter data by running get_twitter_data.ipynb
### Get news data by running get_news_data.ipynb
### process data using data_processing.ipynb
### run all the models to get results


---
## Presentation

`Background`
```
Markets reacts to tweets from multiple key personalities.Such as Elon Musk, Mark Cuban

As we can see Musks tweet cause price jump in Bitcoin & the tweet nearly got 2k replies
Also same with Mark Cuban, his tweet was also responsible for the Dogecoin pump.
So the team came up with an idea & decided to create a trading strategy based on twitter sentiment.
Hypothesis,
if there is a positive sentiment, price will go up, if there is negative sentiment price will go down.

Data collection
- Pull nearly 100 tweets for each minute for BTC
- Also we pulled News data from NewsApi
- Asset data from yahoo finance.
```

`Data exploration process, APIS`
```
For our data sources we used twitter for our sentiment input data, yahoo finance for the crypto prices data and news api for new articles sentiment data.
The twitter data we saved to a csv to not exceed our api request limits.
NewsAPi, we had a function that got the themed articles, tokenised, ran sentiment analyser, and put it into a appropriate dataframe.
Cleaning the tweets (twitter data)
For the twitter data cleaning we removed punctuation, emojis and foreign characters. We then tokenised the remaining words. The sentiment was formulated using NLTK VADER sentiment analyser. For all the tweets we grouped by each minute so we could then concatenate it with the BTC minute trading data.  We removed NA compound scores to reduce noise.
An issue we didn’t consider was removing retweets but we found a solution to that easily.
But For the news api data, we discovered that the articles were grouped into ‘days’ when we needed minute based data. So we couldn’t use that in our models.
BACKTEST function.
notes on how to use the backtest function are in the file, defines the appropriate input data for the function. You also set the initial investment and the stock/asset trade (buy/sell) amount
After that is a plotting function that plots the backtesting results. (feeds off the backtest functions output)
```

`SVM`
```
We started by setting a buy and sell signal. We denominated 1 as a buy and -1 as a sell. If we had the time, we would have created a hold signal. This hold signal would’ve had elements of a certain threshold of returns and other elements such as compound score.
We set the features as positive, negative, compound, and close. Our training data had 56% accuracy and our back test data had 52% accuracy. In the future we could have analysed the data to a greater extent. Not having a hold signal hurt the model quite a bit as there was constant buying and selling every minute per tweet. Having a hold signal would allow our positions to build to appropriate levels.
```