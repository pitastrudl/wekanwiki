# Cloudron setup

Status:
- [Cloudron now uses upstream Wekan directly](https://github.com/wekan/wekan/issues/3035), so Cloudron users get all Wekan newest features and fixes

Cloudron is a complete solution for running apps on your server and keeping them up-to-date and secure.

1. First install Cloudron on your server with 3 simple commands - https://cloudron.io/get.html
2. Install Wekan from the Cloudron Store. Once installed, you will get automatic updates for Wekan as and when they get released.

[![Install](https://cloudron.io/img/button.svg)](https://cloudron.io/button.html?app=io.wekan.cloudronapp)

The source code for the package can be found [here](https://git.cloudron.io/cloudron/wekan-app/).

You can also test the wekan installation on the demo Cloudron instance - https://my.demo.cloudron.io (username: cloudron password: cloudron).

# Backup

If those [Backup](https://github.com/wekan/wekan/wiki/Backup) ways are not easily found at Cloudron, one way is to install [Redash](https://redash.io/) and then backup this way:

Redash works with this kind of queries:
```
{
	"collection": "accountSettings",
	"query": {
		"type": 1
	},
	"fields": {
		"_id": 1,
		"booleanValue": 1,
		"createdAt": 1,
		"modifiedAt": 1,		
	}
}
```
So:

1) Create this kind of query:
```
{
	"collection": "boards"
}
```

Later when you modify query, you can remove text like boards with double-click-with-mouse and delete-key-at-keyboard (or select characters with mouse and delete-key-at-keyboard), and then click collection/table >> button to insert name of next collection/table.

2) Click Save

3) Click Execute. This will cache query for use with REST API.

4) Click at right top [...] => Show API key

It looks like this:

https://redash.example.com/api/queries/1/results.json?api_key=...

5) Only when saving first collection/table, Save API key to text file script like this `dl.sh` 
```
#!/bin/bash

# Example: ./dl.sh boards

export APIKEY=https://redash.example.com/api/queries/1/results.json?api_key=...

curl -o $1.json $APIKEY
```

6) Run save script like:
```
./dl.sh boards
```
Note: 1) Save 2) Execute => webbrowser can give this kind of timeout,
but downloading with API script still works:

> wekan
> Error running query: failed communicating with server. Please check your Internet connection and try again.

7) Repeat steps 1-4 and 6 for every collection/table like boards,cards, etc

8) Remove from downloaded .json files extra query related data, so that it is similar like [any other Wekan database backup JSON files](https://github.com/wekan/wekan/wiki/Export-from-Wekan-Sandstorm-grain-.zip-file)

9) Insert data to some other Wekan install with nosqlbooster like mentioned at page [Backup](https://github.com/wekan/wekan/wiki/Backup)