# Social-Media-Sentiment-Analysis

Here's a basic Social Media Sentiment Analysis for Brands project using Python. This project typically involves collecting tweets, cleaning the data, analyzing sentiment using libraries like TextBlob or VADER, and visualizing the results.

Below is a simple example using tweepy (for Twitter data), TextBlob (for sentiment analysis), and matplotlib (for visualization).

Here is a detailed note on Social Media Sentiment Analysis for Brands — useful for understanding the concept, methodology, and applications. You can use this for documentation or as part of your project report.

# 1️⃣Install Required Libraries

pip install tweepy textblob    matplotlib   wordcloud

# 2️⃣Python Code for Sentiment Analysis

import tweepy
from textblob import TextBlob
import matplotlib.pyplot as plt
from wordcloud import WordCloud

# ---------------------------
# Twitter API Authentication
# ---------------------------
api_key = 'YOUR_API_KEY'
api_secret = 'YOUR_API_SECRET'
access_token = 'YOUR_ACCESS_TOKEN'
access_token_secret = 'YOUR_ACCESS_TOKEN_SECRET'

auth = tweepy.OAuth1UserHandler(api_key, api_secret, access_token, access_token_secret)
api = tweepy.API(auth)

# ---------------------------
# Fetch Tweets
# ---------------------------
brand = 'Nike'   # Example brand
query = f"{brand} -filter:retweets"
tweets = api.search_tweets(q=query, lang='en', count=100)

# ---------------------------
# Analyze Sentiment
# ---------------------------
positive = 0
neutral = 0
negative = 0
tweet_texts = []

for tweet in tweets:
    text = tweet.text
    tweet_texts.append(text)
    analysis = TextBlob(text)
    polarity = analysis.sentiment.polarity
    if polarity > 0:
        positive += 1
    elif polarity == 0:
        neutral += 1
    else:
        negative += 1

# ---------------------------
# Visualization
# ---------------------------
labels = ['Positive', 'Neutral', 'Negative']
sizes = [positive, neutral, negative]
colors = ['green', 'gray', 'red']

plt.figure(figsize=(6, 6))
plt.pie(sizes, labels=labels, colors=colors, autopct='%1.1f%%', startangle=140)
plt.title(f"Sentiment Analysis for {brand} (based on 100 Tweets)")
plt.axis('equal')
plt.show()

# ---------------------------
# WordCloud of Tweets
# ---------------------------
all_words = ' '.join(tweet_texts)
wordcloud = WordCloud(width=800, height=400, background_color='white').generate(all_words)

plt.figure(figsize=(10, 5))
plt.imshow(wordcloud, interpolation='bilinear')
plt.axis('off')
plt.title(f"WordCloud for {brand}")
plt.show()
