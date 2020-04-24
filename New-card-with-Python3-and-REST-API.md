Also see:
- [API Login to get Bearer token](https://github.com/wekan/wekan/wiki/REST-API#example-call---as-form-data)
- [API docs and examples for various programming languages](https://wekan.github.io/api/), there is Boards / Export for exporting board with API
- In the right menu, scroll down REST API Docs etc links =====>
- https://github.com/pycurl/pycurl/tree/master/examples/quickstart
- Wekan-Gogs integration with Node.js https://github.com/wekan/wekan-gogs

# Install

Windows
```
choco install python3
# REBOOT
pip3 install pip --upgrade
pip3 install pycurl certifi json
python3 wekan.py
```
Debian/Ubuntu
```
sudo apt-get -y install python3 python3-pip python3-pycurl python3-simplejson
sudo pip3 install pip --upgrade
sudo pip3 install certifi
chmod +x newcard.py
./wekan.py
```

# wekan.py

Change these:
- wekanurl: https://boards.example.com => Your Wekan URL
- username
- password

```
#! /usr/bin/env python3
# -*- coding: utf-8 -*-
# vi:ts=4:et

import pycurl
try:
    # python 3
    from urllib.parse import urlencode
except ImportError:
    # python 2
    from urllib import urlencode

import certifi
import json
from io import BytesIO
import sys

arguments = len(sys.argv) - 1

if arguments == 0:
    print("=== Wekan API Python CLI: Shows IDs for addcard ===")
    print("AUTHORID is USERID that writes card.")
    print("Syntax:")
    print("  python3 wekan.py users              # All users")
    print("  python3 wekan.py boards USERID      # Boards of USERID")
    print("  python3 wekan.py board BOARDID      # Info of BOARDID")
    print("  python3 wekan.py swimlanes BOARDID  # Swimlanes of BOARDID")
    print("  python3 wekan.py lists BOARDID      # Lists of BOARDID")
    print("  python3 wekan.py addcard AUTHORID BOARDID SWIMLANEID LISTID CARDTITLE CARDDESCRIPTION")
    exit

# ------- SETTINGS START -------------

username = 'wekan-admin'
password = 'wekan-admin-password'
#wekanurl = 'https://boards.example.com/'
wekanurl = 'http://localhost/'

# SYNTAX
# python3 wekan.py addcard AUTHORID BOARDID SWIMLANEID LISTID CARDTITLE CARDDESCRIPTION

# EXAMPLE 2:
# Write to Welcome board
# python3 wekan.py addcard abcd efgh ijkl mnop "Welcome test" "Description test"

# ------- SETTINGS END -------------

# ------- API URL GERENARTION START -----------

loginurl = 'users/login'
wekanloginurl = wekanurl + loginurl
apiboards = 'api/boards/'
apiusers = 'api/users/'
s = '/'
l = 'lists'
sw = 'swimlane'
sws = 'swimlanes'
cs = 'cards'
bs = 'boards'
users = wekanurl + apiusers

# ------- API URL GERENARTION END -----------

# ------- LOGIN TOKEN START -----------

buffer = BytesIO()
c = pycurl.Curl()
c.setopt(c.URL, wekanloginurl)
c.setopt(c.WRITEDATA, buffer)
c.setopt(c.CAINFO, certifi.where())
post_data = {"username": username, "password": password}
# Form data must be provided already urlencoded.
postfields = urlencode(post_data)
# Sets request method to POST,
# Content-Type header to application/x-www-form-urlencoded
# and data to send in request body.
c.setopt(c.POSTFIELDS, postfields)

c.perform()
c.close()

body = buffer.getvalue()
# Body is a byte string.
# We have to know the encoding in order to print it to a text file
# such as standard output.
data = body.decode('iso-8859-1')
#print(data)
d = json.loads(data)
#print(list(d.keys()))
#print(d['token'])
apikey = d['token']

# ------- LOGIN TOKEN END -----------

if arguments == 7:

    if sys.argv[1] == 'addcard':
        
        # ------- WRITE TO CARD START -----------
        authorid = sys.argv[2]
        boardid = sys.argv[3]
        swimlaneid = sys.argv[4]
        listid = sys.argv[5]
        cardtitle = sys.argv[6]
        carddescription = sys.argv[7]
        cardtolist = wekanurl + apiboards + boardid + s + l + s + listid + s + cs
        # Write to card
        c = pycurl.Curl()
        c.setopt(c.URL, cardtolist)
        c.setopt(c.WRITEDATA, buffer)
        c.setopt(c.CAINFO, certifi.where())
        c.setopt(c.HTTPHEADER, ['Accept: application/json', 'Authorization: Bearer {}'.format(apikey)])
        post_data = {"authorId": authorid, "title": cardtitle, "description": carddescription, "swimlaneId": swimlaneid}
        # Form data must be provided already urlencoded.
        postfields = urlencode(post_data)
        # Sets request method to POST,
        # Content-Type header to application/x-www-form-urlencoded
        # and data to send in request body.
        c.setopt(c.POSTFIELDS, postfields)
        c.perform()
        c.close()
        body = buffer.getvalue()
        data = body.decode('iso-8859-1')
        #print(data)

    # ------- WRITE TO CARD END -----------

if arguments == 2:

    # ------- BOARDS LIST START -----------
    userid = sys.argv[2]
    boards = wekanurl + apiusers + userid + s + bs
    if sys.argv[1] == 'boards':
        c = pycurl.Curl()
        c.setopt(c.URL, boards)
        c.setopt(c.WRITEDATA, buffer)
        c.setopt(c.CAINFO, certifi.where())
        c.setopt(c.HTTPHEADER, ['Accept: application/json', 'Authorization: Bearer {}'.format(apikey)])
        c.perform()
        c.close()
        body = buffer.getvalue()
        data = body.decode('iso-8859-1')
        print("=== BOARDS ===\n")
        data2 = data.replace('}',"}\n")
        print(data2)
        print("\n")
        data = ""
    # ------- BOARDS LIST END -----------

    if sys.argv[1] == 'board':

        # ------- BOARD INFO START -----------
        boardid = sys.argv[2]
        board = wekanurl + apiboards + boardid
        c = pycurl.Curl()
        c.setopt(c.URL, board)
        c.setopt(c.WRITEDATA, buffer)
        c.setopt(c.CAINFO, certifi.where())
        c.setopt(c.HTTPHEADER, ['Accept: application/json', 'Authorization: Bearer {}'.format(apikey)])
        c.perform()
        c.close()
        body = buffer.getvalue()
        data = body.decode('iso-8859-1')
        print("=== BOARD ===\n")
        data2 = data.replace('}',"}\n")
        print(data2)
        print("\n")
        data = ""

        # ------- BOARD INFO END -----------

    if sys.argv[1] == 'swimlanes':
        
        boardid = sys.argv[2]
        swimlanes = wekanurl + apiboards + boardid + s + sws
        # ------- SWIMLANES OF BOARD START -----------
        c = pycurl.Curl()
        c.setopt(c.URL, swimlanes)
        c.setopt(c.WRITEDATA, buffer)
        c.setopt(c.CAINFO, certifi.where())
        c.setopt(c.HTTPHEADER, ['Accept: application/json', 'Authorization: Bearer {}'.format(apikey)])
        c.perform()
        c.close()
        body = buffer.getvalue()
        data = body.decode('iso-8859-1')
        print("=== SWIMLANES ===\n")
        data2 = data.replace('}',"}\n")
        print(data2)
        print("\n")
        data = ""
        # ------- SWIMLANES OF BOARD END -----------

    if sys.argv[1] == 'lists':

        # ------- LISTS OF BOARD START -----------
        boardid = sys.argv[2]
        lists = wekanurl + apiboards + boardid + s + l
        c = pycurl.Curl()
        c.setopt(c.URL, lists)
        c.setopt(c.WRITEDATA, buffer)
        c.setopt(c.CAINFO, certifi.where())
        c.setopt(c.HTTPHEADER, ['Accept: application/json', 'Authorization: Bearer {}'.format(apikey)])
        c.perform()
        c.close()
        body = buffer.getvalue()
        data = body.decode('iso-8859-1')
        print("=== LISTS ===\n")
        data2 = data.replace('}',"}\n")
        print(data2)
        print("\n")
        data = ""
        # ------- LISTS OF BOARD END -----------

if arguments == 1:

    if sys.argv[1] == 'users':

        # ------- LIST OF USERS START -----------
        c = pycurl.Curl()
        c.setopt(c.URL, users)
        c.setopt(c.WRITEDATA, buffer)
        c.setopt(c.CAINFO, certifi.where())
        c.setopt(c.HTTPHEADER, ['Accept: application/json', 'Authorization: Bearer {}'.format(apikey)])
        c.perform()
        c.close()
        body = buffer.getvalue()
        data = body.decode('iso-8859-1')
        print("=== USERS ===\n")
        data2 = data.replace('}',"}\n")
        print(data2)
        print("\n")
        data = ""
        # ------- LIST OF USERS END -----------


"""
authorId: string
members: string
assignees: string
title: string
description: string
swimlaneId: string
"""
```