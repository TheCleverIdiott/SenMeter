# 1. query twitter using tweepy
# 2. generate personality with personality insights
# 3. Visualise them using seaborn and Matplotlib
#______________________________________________________________________________________________________________

#importing libraries
import tweepy
from textblob import TextBlob
from wordcloud import WordCloud
import pandas as pd
import numpy as np
import re
import matplotlib.pyplot as plt
plt.style.use('fivethirtyeight')

#______________________________________________________________________________________________________________

#loading data

from google.colab import files
uploaded = files.upload(login.csv)  #login is in system

#______________________________________________________________________________________________________________

#getting data

log = pd.read_csv('login.csv')

#______________________________________________________________________________________________________________

#twitter API credentials

consumerKey = log['key'][0]
consumerSecret = log['key'][1]
accessToken = log['key'][2]
accessTokenSecret = log['key'][3]

#______________________________________________________________________________________________________________

#creating the authentication object
authenticate = tweepy.OAuth1UserHandler(consumerKey, consumerSecret)

#setting the access token and access tokem secret
authenticate.set_access_token(accessToken, accessTokenSecret)

#creating the API object while passing the auth info
api = tweepy.API(authenticate, wait_on_rate_limit = True)

#______________________________________________________________________________________________________________

#extract recent 100 tweets from twitter user {input()}
posts = api.user_timeline(screen_name = 'BillGates', count = 100, lang = 'en', tweet_mode = 'extended') #just an example...make it user specific

#printing the last 5 tweets
print('show the 5 recent tweets: \n')
i = 1
for tweets in posts[0:5]:
    print(str(i), ') ' + 'tweet.full_text' + '\n')
    i = i+1

#______________________________________________________________________________________________________________   

#creating a data frame witha a column called tweets
df = pd.DataFrame( [tweet.full_text for tweet in posts], columns = ["Tweets"])

#show first 5 rows of data
df.head()

#______________________________________________________________________________________________________________

#Cleaning the text

#creating a function to do so
def cleanText(text):
    text = re.sub(r'@[A-Za-z0-9]+', '', text)   #the r tells python that it is a raw string
#the line just above me  simply removes @ mentions
    text = re.sub(r'#', '', text) #removing the # symbol
    text = re.sub(r'RT[\s]+', '', text) #removing RT (retweets)
    text = re.sub(r'https?:\/\/\S+', '', text) #removes the hyperlinks
    
    return text

#cleaning
df['Tweets'] = df['Tweets'].apply(cleanText)

#show the cleaned text
df

#______________________________________________________________________________________________________________

#creating a function to get the subjectivity
def getSubjectivity(text):
    return TextBlob(text).sentiment.subjectivity

#creating a function to get the polarity
def getPolarity(text):
    return TextBlob(text).sentiment.polarity

#creating 2 new columns called subjectivity and polarity
df['subjectivity'] = df['Tweets'].apply(getSubjectivity)
df['polarity'] = df['Tweets'].apply(getPolarity)

#showing new df with new columns
df

#______________________________________________________________________________________________________________

#plot the word cloud

allWords = ' '.join( [twts for twts in df['Tweets']] )
wordCloud = WordCloud(width = 500, height = 300, random_state = 21, max_font_size = 110).generate(allWords)

plt.imshow(wordCloud, interpolation = 'bilinear')
plt.axis('off')
plt.show()

#______________________________________________________________________________________________________________

#creating a function to compute the negative,neutral and positive analysis

def getAnalysis(score):
    if(score<0):
        return 'Negtive'
    elif(score==0):
        return 'Neutral'
    else:
        return 'Positive'
    
#creating new column called analysis
df['Analysis'] = df['Polarity'].apply(getAnalysis)

#show the dataframe
df

#______________________________________________________________________________________________________________

'''
UPTO HERE IT SHOWS POSITIVE NEUTRAL AND NEGATIVE TWEETS AS AN EXCEL SHEET FORMAT
1st SEGMENT DONE (TILL HERE)
BELOW IS SECOND SEGMENT
'''

#______________________________________________________________________________________________________________

#print all of the positive tweets
