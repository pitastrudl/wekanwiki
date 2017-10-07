Code originally by ertanalytics (Eric Thompson / AZero). Script has been used for daily exports of a board.

***

![Wekan Sandstorm cards to CSV using Python screenshot](https://wekan.github.io/sandstorm-api-csv.png)

***

## Exporting Wekan board to JSON with Bash script

1) On Wekan grain, get Webkey like this:

```
https://api-URL.SUBDOMAIN.sandcats.io#APIKEY
```

2) Modity URL, SUBDOMAIN and APIKEY to this script that exports board to file directly:

```
curl https://Bearer:APIKEY@api-URL.SUBDOMAIN.sandcats.io/api/boards/sandstorm/export?authToken=#APIKEY > wekanboard.json
```

***

## Python script, has more dependencies

cards-to-csv.py

```
#Sandstorm Wekan API Access Testing
##Does not seem to pull the redirected content
import requests
from requests.auth import HTTPBasicAuth
from bs4 import BeautifulSoup
from time import sleep
import os
import sys
import urllib
#All imports needed site navigation
import datetime
from time import sleep
import time
from selenium import webdriver
#drive.get('http://www.google.com/');
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from selenium.common.exceptions import TimeoutException
from splinter import *
#driver = webdriver.Chrome()
##Data Handling
import pandas as pd
import json
from bson import json_util, ObjectId
from pandas.io.json import json_normalize
reload(sys)
sys.setdefaultencoding('utf-8')
#Need new API for KHS
#https://api-KEYCHANGED.example.com#MAYBEKEYHERE
apiURLnoAuth = 'https://username:password@api-KEY.example.com/'
apiURL = 'https://api-KEY.example.com/b/sandstorm/libreboard'
user = ''
password = ''

apiCredInURL = 'https://username:password@api-KEY.example.com/b/sandstorm/libreboard'
#East list has an ID - Each Card references this id with %22listId%22%3A%22

#All lists at top - Lists: "%22lists"
#After lists section begins  - Beginning of List - "title%22%3A%22" = title follows right after
#All cards after lists at the top - Cards: "%22cards%22"
#After cards section begins  - Beginning of Card - "title%22%3A%22" = title follows right after
#"%22" defines section of a card
#Created Date - "%22createdAt%22%3A%7B%22%24date%22%3A" follows right after
#Last Activity Date - "%22dateLastActivity%22%3A%7B%22%24date%22%3A" follows right after
##Date times use http://www.epochconverter.com/ - Find alternative in Python

sleep(1) #Time in seconds

# Choose the browser (default is Firefox)
browser2 = Browser('chrome')

# Fill in the url
browser2.visit(apiURLnoAuth)

sleep(1) #Time in seconds

soup = BeautifulSoup(browser2.html,'html.parser')
browser2.quit()

script = soup.find("script", attrs={'type' : 'text/inject-data'}).children.next()
sitedata = urllib.unquote(script)
        
sanitized = json.loads(sitedata)
normalized = json_normalize(sanitized)
df = pd.DataFrame(normalized)

#find a table
#df.iloc[0] 

dfboards = pd.DataFrame(df.iloc[0]['fast-render-data.collectionData.boards'])
dfcard_comments = pd.DataFrame(df.iloc[0]['fast-render-data.collectionData.card_comments'])
dfcards = pd.DataFrame(df.iloc[0]['fast-render-data.collectionData.cards'])
dffilerecord = pd.DataFrame(df.iloc[0]['fast-render-data.collectionData.cfs.attachments.filerecord'])
dflists = pd.DataFrame(df.iloc[0]['fast-render-data.collectionData.lists'])
dfpresences = pd.DataFrame(df.iloc[0]['fast-render-data.collectionData.presences'])
dfusers = pd.DataFrame(df.iloc[0]['fast-render-data.collectionData.users'])

#Puts dataframe in rows instead of columns
dfboards = pd.DataFrame(json_normalize(dfboards.iloc[0]))
dfcard_comments = pd.DataFrame(json_normalize(dfcard_comments.iloc[0]))
dfcards = pd.DataFrame(json_normalize(dfcards.iloc[0]))
dffilerecord = pd.DataFrame(json_normalize(dffilerecord.iloc[0]))
dflists = pd.DataFrame(json_normalize(dflists.iloc[0]))
dfpresences = pd.DataFrame(json_normalize(dfpresences.iloc[0]))
dfusers = pd.DataFrame(json_normalize(dfusers.iloc[0]))

#Sepecfic column within an above data frame
dfboardsLabels = pd.DataFrame(dfboards.iloc[0]['labels'])

#Find date columns
date_cols = [col for col in dfboards.columns if 'date' in col]
#Convert Epoch 13 digit date/time/second to normal timestamp
dflists['createdAt.$date'] = pd.to_datetime(dflists['createdAt.$date'],unit='ms')
dflists['updatedAt.$date'] = pd.to_datetime(dflists['updatedAt.$date'],unit='ms')

dfcards['createdAt.$date'] = pd.to_datetime(dfcards['createdAt.$date'],unit='ms')
dfcards['dateLastActivity.$date'] = pd.to_datetime(dfcards['dateLastActivity.$date'],unit='ms')
dfcards['title']=dfcards['title'].str.replace('\n','')

dfboards['createdAt.$date'] = pd.to_datetime(dfboards['createdAt.$date'],unit='ms')
dfboards['modifiedAt.$date'] = pd.to_datetime(dfboards['modifiedAt.$date'],unit='ms')

#dfFirstCard = pd.DataFrame(json_normalize(dfcards.iloc[2]))
dfcards.to_csv('//FOLDERDESTINATION/dfcards.csv',sep='|')
dflists.to_csv('//FOLDERDESTINATION/dflists.csv',sep='|')
dfboardsLabels.to_csv('//FOLDERDESTINATION/dfboardsLabels.csv',sep='|')
dfusers.to_csv('//FOLDERDESTINATION/dfusers.csv',sep='|')
```