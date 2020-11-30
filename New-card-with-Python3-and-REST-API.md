Also see:
- [API Login to get Bearer token](https://github.com/wekan/wekan/wiki/REST-API#example-call---as-form-data)
- [API docs and examples for various programming languages](https://wekan.github.io/api/), there is Boards / Export for exporting board with API
- In the right menu, scroll down REST API Docs etc links =====>
- Wekan-Gogs integration with Node.js https://github.com/wekan/wekan-gogs

# Install

Windows
```
choco install python3
# REBOOT
pip3 install pip --upgrade
pip3 install json
python3 wekan.py
```
Debian/Ubuntu
```
sudo apt-get -y install python3 python3-pip python3-simplejson
sudo pip3 install pip --upgrade
chmod +x wekan.py
./wekan.py
```

# wekan.py creating new card with Python3 and REST API

Below code works now, fixed at 2020-10-29.

Change these:
- wekanurl: https://boards.example.com => Your Wekan URL
- username (could be username or username@example.com if OIDC/OAuth2 etc login)
- password

```
#! /usr/bin/env python3
# -*- coding: utf-8 -*-
# vi:ts=4:et

try:
    # python 3
    from urllib.parse import urlencode
except ImportError:
    # python 2
    from urllib import urlencode

import json
import requests
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
    print("  python3 wekan.py createlist BOARDID LISTTITLE # Create list")
    print("  python3 wekan.py addcard AUTHORID BOARDID SWIMLANEID LISTID CARDTITLE CARDDESCRIPTION")
    print("  python3 wekan.py listattachments BOARDID # List attachments")
    print("  python3 wekan.py attachmentjson BOARDID ATTACHMENTID # One attachment as JSON")
    print("  python3 wekan.py attachmentsjson BOARDID # All attachments as JSON")
    print("  python3 wekan.py attachmentdownload BOARDID ATTACHMENTID # One attachment as file")
    print("  python3 wekan.py attachmentsdownload BOARDID # All attachments as files")
    exit

# ------- SETTINGS START -------------

username = 'username' (or username@example.com if OIDC/OAuth2 etc login)

password = 'topsecret'

wekanurl = 'https://boards.example.com/'

# ------- SETTINGS END -------------

"""
EXAMPLE:

python3 wekan.py

=== Wekan API Python CLI: Shows IDs for addcard ===
AUTHORID is USERID that writes card.
Syntax:
  python3 wekan.py users              # All users
  python3 wekan.py boards USERID      # Boards of USERID
  python3 wekan.py board BOARDID      # Info of BOARDID
  python3 wekan.py swimlanes BOARDID  # Swimlanes of BOARDID
  python3 wekan.py lists BOARDID      # Lists of BOARDID
  python3 wekan.py createlist BOARDID LISTTITLE # Create list
  python3 wekan.py addcard AUTHORID BOARDID SWIMLANEID LISTID CARDTITLE CARDDESCRIPTION
  python3 wekan.py listattachments BOARDID # List attachments
  python3 wekan.py attachmentjson BOARDID ATTACHMENTID # One attachment as JSON
  python3 wekan.py attachmentsjson BOARDID # All attachments as JSON
  python3 wekan.py attachmentdownload BOARDID ATTACHMENTID # One attachment as file
  python3 wekan.py attachmentsdownload BOARDID # All attachments as files

python3 wekan.py boards ppg7R38ykWb28BWDp

=== BOARDS ===

[{"_id":"una","title":"Templates"}
,{"_id":"dYZ","title":"Global Status"}
]

python3 wekan.py swimlanes dYZ

=== SWIMLANES ===

[{"_id":"Jiv","title":"Default"}
]

python3 wekan.py lists dYZ

=== LISTS ===

[]

There is no lists, so create a list:

python3 wekan.py createlist dYZ 'Test'

=== CREATE LIST ===

{"_id":"7Kp"}

#  python3 wekan.py addcard AUTHORID BOARDID SWIMLANEID LISTID CARDTITLE CARDDESCRIPTION

python3 wekan.py addcard ppg dYZ Jiv 7Kp 'Test card' 'Test description'

"""

# ------- API URL GERENARTION START -----------

loginurl = 'users/login'
wekanloginurl = wekanurl + loginurl
apiboards = 'api/boards/'
apiattachments = 'api/attachments/'
apiusers = 'api/users'
e = 'export'
s = '/'
l = 'lists'
sw = 'swimlane'
sws = 'swimlanes'
cs = 'cards'
bs = 'boards'
atl = 'attachmentslist'
at = 'attachment'
ats = 'attachments'
users = wekanurl + apiusers

# ------- API URL GERENARTION END -----------

# ------- LOGIN TOKEN START -----------

data = {"username": username, "password": password}
body = requests.post(wekanloginurl, data=data)
d = body.json()
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
        headers = {'Accept': 'application/json', 'Authorization': 'Bearer {}'.format(apikey)}
        post_data = {'authorId': '{}'.format(authorid), 'title': '{}'.format(cardtitle), 'description': '{}'.format(carddescription), 'swimlaneId': '{}'.format(swimlaneid)}
        body = requests.post(cardtolist, data=post_data, headers=headers)
        print(body.text)
        # ------- WRITE TO CARD END -----------

if arguments == 3:

    if sys.argv[1] == 'createlist':

      # ------- CREATE LIST START -----------
      boardid = sys.argv[2]
      listtitle = sys.argv[3]
      list = wekanurl + apiboards + boardid + s + l
      headers = {'Accept': 'application/json', 'Authorization': 'Bearer {}'.format(apikey)}
      post_data = {'title': '{}'.format(listtitle)}
      body = requests.post(list, data=post_data, headers=headers)
      print("=== CREATE LIST ===\n")
      print(body.text)
      # ------- CREATE LIST END -----------

if arguments == 2:

    # ------- BOARDS LIST START -----------
    userid = sys.argv[2]
    boards = users + s + userid + s + bs
    if sys.argv[1] == 'boards':
        headers = {'Accept': 'application/json', 'Authorization': 'Bearer {}'.format(apikey)}
        #post_data = {'userId': '{}'.format(userid)}
        body = requests.get(boards, headers=headers)
        print("=== BOARDS ===\n")
        data2 = body.text.replace('}',"}\n")
        print(data2)
    # ------- BOARDS LIST END -----------
    if sys.argv[1] == 'board':

        # ------- BOARD INFO START -----------
        boardid = sys.argv[2]
        board = wekanurl + apiboards + boardid
        headers = {'Accept': 'application/json', 'Authorization': 'Bearer {}'.format(apikey)}
        body = requests.get(board, headers=headers)
        print("=== BOARD ===\n")
        data2 = body.text.replace('}',"}\n")
        print(data2)
        # ------- BOARD INFO END -----------

    if sys.argv[1] == 'swimlanes':
        boardid = sys.argv[2]
        swimlanes = wekanurl + apiboards + boardid + s + sws
        # ------- SWIMLANES OF BOARD START -----------
        headers = {'Accept': 'application/json', 'Authorization': 'Bearer {}'.format(apikey)}
        print("=== SWIMLANES ===\n")
        body = requests.get(swimlanes, headers=headers)
        data2 = body.text.replace('}',"}\n")
        print(data2)
        # ------- SWIMLANES OF BOARD END -----------

    if sys.argv[1] == 'lists':

        # ------- LISTS OF BOARD START -----------
        boardid = sys.argv[2]
        attachments = wekanurl + apiboards + boardid
        headers = {'Accept': 'application/json', 'Authorization': 'Bearer {}'.format(apikey)}
        print("=== LISTS ===\n")
        body = requests.get(lists, headers=headers)
        data2 = body.text.replace('}',"}\n")
        print(data2)
        # ------- LISTS OF BOARD END -----------

    if sys.argv[1] == 'listattachments':

        # ------- LISTS OF ATTACHMENTS START -----------
        boardid = sys.argv[2]
        listattachments = wekanurl + apiboards + boardid + s + ats
        print(listattachments)
        headers = {'Accept': 'application/json', 'Authorization': 'Bearer {}'.format(apikey)}
        print("=== LIST OF ATTACHMENTS ===\n")
        body = requests.get(listattachments, headers=headers)
        data2 = body.text.replace('}',"}\n")
        print(data2)
        # ------- LISTS OF ATTACHMENTS END -----------

if arguments == 1:

    if sys.argv[1] == 'users':

        # ------- LIST OF USERS START -----------
        headers = {'Accept': 'application/json', 'Authorization': 'Bearer {}'.format(apikey)}
        print(users)
        print("=== USERS ===\n")
        body = requests.get(users, headers=headers)
        data2 = body.text.replace('}',"}\n")
        print(data2)
        # ------- LIST OF USERS END -----------
```