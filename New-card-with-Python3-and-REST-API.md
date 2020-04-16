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
python3 newcard.py
```
Debian/Ubuntu
```
sudo apt-get -y install python3 python3-pip python3-pycurl
sudo pip3 install pip --upgrade
sudo pip3 install certifi json
chmod +x newcard.py
./newcard.py
```

# newcard.py

Change these:
- https://example.com => Your Wekan URL
- username: joe
- password: topsecret
- BOARD-ID-HERE
- LIST-ID-HERE
- USER-ID-HERE

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

buffer = BytesIO()
c = pycurl.Curl()
c.setopt(c.URL, 'https://example.com/users/login')
c.setopt(c.WRITEDATA, buffer)
c.setopt(c.CAINFO, certifi.where())
post_data = {"username": "joe", "password": "topsecret"}
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

# Lists of board
c = pycurl.Curl()
c.setopt(c.URL, 'https://example.com/api/boards/BOARD-ID-HERE/lists')
c.setopt(c.WRITEDATA, buffer)
c.setopt(c.CAINFO, certifi.where())
c.setopt(c.HTTPHEADER, ['Accept: application/json', 'Authorization: Bearer {}'.format(apikey)])
##post_data = {"authorId": "joe", "password": "topsecret"}
# Form data must be provided already urlencoded.
#postfields = urlencode(post_data)
# Sets request method to POST,
# Content-Type header to application/x-www-form-urlencoded
# and data to send in request body.
#c.setopt(c.POSTFIELDS, postfields)
c.perform()
c.close()
body = buffer.getvalue()
data = body.decode('iso-8859-1')
print("=== LISTS ===\n")
print(data)
print("\n")
data = ""

# Swimlanes of board
c = pycurl.Curl()
c.setopt(c.URL, 'https://example.com/api/boards/BOARD-ID-HERE/swimlanes')
c.setopt(c.WRITEDATA, buffer)
c.setopt(c.CAINFO, certifi.where())
c.setopt(c.HTTPHEADER, ['Accept: application/json', 'Authorization: Bearer {}'.format(apikey)])
##post_data = {"authorId": "joe", "password": "topsecret"}
# Form data must be provided already urlencoded.
#postfields = urlencode(post_data)
# Sets request method to POST,
# Content-Type header to application/x-www-form-urlencoded
# and data to send in request body.
#c.setopt(c.POSTFIELDS, postfields)
c.perform()
c.close()
body = buffer.getvalue()
data = body.decode('iso-8859-1')
print("=== SWIMLANES ===\n")
print(data)
print("\n")
data = ""

# Board info
c = pycurl.Curl()
c.setopt(c.URL, 'https://example.com/api/boards/BOARD-ID-HERE')
c.setopt(c.WRITEDATA, buffer)
c.setopt(c.CAINFO, certifi.where())
c.setopt(c.HTTPHEADER, ['Accept: application/json', 'Authorization: Bearer {}'.format(apikey)])
##post_data = {"authorId": "joe", "password": "topsecret"}
# Form data must be provided already urlencoded.
#postfields = urlencode(post_data)
# Sets request method to POST,
# Content-Type header to application/x-www-form-urlencoded
# and data to send in request body.
#c.setopt(c.POSTFIELDS, postfields)
c.perform()
c.close()
body = buffer.getvalue()
data = body.decode('iso-8859-1')
print("=== BOARD ===\n")
print(data)
print("\n")
data = ""

# Write to card
c = pycurl.Curl()
c.setopt(c.URL, 'https://example.com/api/boards/BOARD-ID-HERE/lists/LIST-ID-HERE/cards')
c.setopt(c.WRITEDATA, buffer)
c.setopt(c.CAINFO, certifi.where())
c.setopt(c.HTTPHEADER, ['Accept: application/json', 'Authorization: Bearer {}'.format(apikey)])
post_data = {"authorId": "USER-ID-HERE", "title": "Test API", "description": "Testing Description", "swimlaneId": "SWIMLANE-ID-HERE"}
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
print(data)


"""
authorId: string
members: string
assignees: string
title: string
description: string
swimlaneId: string
"""
```