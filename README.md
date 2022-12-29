
# Detection feelings of tweets

### Sentiment analysis with BERT IA 

#### project make with [Google Colab](https://colab.research.google.com/)


1. [Version Google Colab](https://github.com/Kyytox/feelings-twitter-ia/blob/master/code/Sentiments_Tweets_IA_BERT.ipynb)

### Install Packages 
```python
pip install transformers>=4.0
pip install sentencepiece
pip install git+https://github.com/tweepy/tweepy.git --upgrade
pip install spacy
pip install circlify
```

### Import pack and Initialize Model 
```python 
import tensorflow as tf
assert tf.__version__ >= "2.0"

import matplotlib.pyplot as plt
import nltk
import spacy
import spacy.cli

import numpy as np
import pandas as pd
import tweepy
import json
import time
import calendar
import circlify
import re 

from wordcloud import WordCloud
from nltk.corpus import stopwords
from transformers import AutoModelForSequenceClassification
from transformers import TFAutoModelForSequenceClassification
from transformers import AutoTokenizer, AutoConfig
from scipy.special import softmax

# DL frequent words FR 
spacy.cli.download("fr_core_news_sm")
nltk.download('stopwords')
nlp = spacy.load("fr_core_news_sm")
stopWords = set(stopwords.words('french'))

# initialize model 
task='sentiment'
MODEL = "cardiffnlp/twitter-xlm-roberta-base-sentiment"
tokenizer = AutoTokenizer.from_pretrained(MODEL)
config = AutoConfig.from_pretrained(MODEL)
model = AutoModelForSequenceClassification.from_pretrained(MODEL)
model.save_pretrained(MODEL)
```

### Collect tweets of one user without RT and Replies and apply Model IA 
```python
# API TWiiter 

# function for remove spécific caract in tweet  
def nlp_pipeline(text):
    # remove specific caract usefull for help IA
    text = text.lower()
    text = text.replace('\n', ' ').replace('\r', '')
    text = ' '.join(text.split())
    text = re.sub(r"(\s\-\s|-$)", "", text)
    text = re.sub(r"\?", "", text)
    text = re.sub(r"https://", "", text)

    return text

# Initialization Tweepy for use Twitter APi v2
client = tweepy.Client(bearer_token='')

# create dataFrame with columns 
df = pd.DataFrame(columns=['Sentiment', 'Score', 'Id_Tweet', 'Negative', 'Neutral', 'Positive', 'Text_Tweet', 'Date_Tweet', 'Nb_interaction', 'retweet_count', 'reply_count', 'like_count', 'quote_count'])

# Id User
id_User = #######

# Lest tweet id of the user 
sauv_id = #########

# Retrive maximum tweets of users (max 3200 with RT and replies )
tweets = tweepy.Paginator(client.get_users_tweets, id_User, until_id = sauv_id, max_results=100,
                        tweet_fields=['created_at', 'public_metrics', 'in_reply_to_user_id', 'referenced_tweets'], expansions=['author_id'], limit=100)


# route retrieved tweets
for x in tweets:
  for i in x.data:
    #  Remove Replies and Retweets 
    if i.in_reply_to_user_id == None and i.referenced_tweets == None:
      if i.id == sauv_id: 
        break
      
      # remove spécifics caract in text
      text = nlp_pipeline(i.text)

      # detect Text sentiment 
      encoded_input = tokenizer(text, return_tensors='pt')
      output = model(**encoded_input)
      scores = output[0][0].detach().numpy()

      # Format outup : [Negative - Neutral - Positive]
      scores = softmax(scores)

      # Collect the max score and the sentment
      ranking = np.argsort(scores)
      ranking = ranking[::-1]

      l = config.id2label[ranking[0]]
      s = scores[ranking[0]]
      st_score = np.round(float(s), 3)

      # Retrieve Metrics , interactions 
      nb_inter = 0
      retweet_count = i.public_metrics['retweet_count']
      reply_count = i.public_metrics['reply_count']
      like_count = i.public_metrics['like_count']
      quote_count = i.public_metrics['quote_count']
      nb_inter = retweet_count + reply_count + like_count + quote_count

      # insert in DataFrame
      df = df.append({'Sentiment': l,'Score': st_score, 'Id_Tweet': i.id, 'Negative': scores[0], 'Neutral': scores[1], 'Positive': scores[2],
                      'Text_Tweet': text, 'Date_Tweet': i.created_at, 'Nb_interaction': nb_inter, 'retweet_count':retweet_count, 'reply_count':reply_count, 'like_count':like_count, 'quote_count':quote_count}, ignore_index=True)

      sauv_id = i.id

# insert in CSV
df.to_csv('out.csv', index=False, header=True)
```
 
