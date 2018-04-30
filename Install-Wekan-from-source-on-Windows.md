# Alternative: Docker, without build from source

Use Docker Compose:
https://github.com/wekan/wekan-mongodb

Or adding also MongoDB mirroring to PostgreSQL:
https://github.com/wekan/wekan-postgresql

# Source install required dependencies

Requirements:
- Install [MeteorJS](https://www.meteor.com/) 
- Install [NodeJS](https://nodejs.org/en/download/releases/) (Optional but recommended)
- Install Python 2.7 (Installation through Chocolatey(`choco install python2 -y`) is recomended)
- If you are on windows 7, Install .NET 4.5.1+
- **MUST MAKE SURE TO** Install [Visual C++ 2015 Build Tools](http://landinghub.visualstudio.com/visual-cpp-build-tools) or run this command from an elevated PowerShell or CMD.exe (run as Administrator) to install, `npm install --global --production windows-build-tools`
- Install Git
- Restart Windows (Optional but recommended)

From this point, it's advised to use **Git bash** to run commands to make sure everything works as is, but if you had trouble accessing meteor or npm commands via Git bash, windows CMD will most likely work without any problem.

Inside the Git Bash, run these commands:

```
npm config -g set msvs_version 2015

meteor npm config -g set msvs_version 2015
```

# Running Wekan
- Clone the repo (`https://github.com/wekan/wekan`)
- Browse the wekan directory and run `meteor`, 
- If you see any error regarding **xss**, do `meteor npm i --save xss` to install xss.
- Set the Environment variables, or create a .env file with the following data.
- open your browser, make changes and see it reflecting real-time.

## Example of setting environment variables

You need to have start-wekan.bat textfile with that content of those environment variables.
In Windows, .bat files use DOS style of setting varibles.

Similar file for Linux bash is here:
https://github.com/wekan/wekan-maintainer/blob/master/virtualbox/start-wekan.sh

ROOT_URL examples are here:
https://github.com/wekan/wekan/releases

```
SET MONGO_URL=mongodb://127.0.0.1:27017/wekan
SET ROOT_URL=http://127.0.0.1/
SET MAIL_URL=smtp://user:pass@mailserver.example.com:25/
SET MAIL_FROM=admin@example.com
SET PORT=8081
```

## Example contents of  `.env` file
```
MONGO_URL=mongodb://127.0.0.1:27017/wekan
ROOT_URL=http://127.0.0.1/
MAIL_URL=smtp://user:pass@mailserver.example.com:25/
MAIL_FROM=admin@example.com
PORT=8081
```

That URL format is: mongodb://ip-address-of-server:port/database-name

You can access MongoDB database with GUI like Robo 3T https://robomongo.org .
There is no username and password set by default.

## Overview,
Here is how it looks like,
```
git clone https://github.com/wekan/wekan
cd wekan
<SET ENV OR CREATE .env FILE>
meteor npm install --save xss
meteor
```

![](https://i.imgur.com/aNVBhj5.png)

# FAQ
### I am getting `node-gyp` related issues.
Make sure to install all required programs stated here, https://github.com/wekan/wekan/wiki/Install-Wekan-from-source-on-Windows#setup-required-dependencies

### I am getting `Error: Cannot find module 'fibers'` related problem.
Make sure to run the command `meteor` instead of `node`.

# VBA

For accessing Wekan with Excel VBA, you can use Wekan REST API:
https://github.com/wekan/wekan/wiki/REST-API

For example, with using curl, you first login with admin credentials,
by sending username and password to url.
Change your server url etc details to below:

```
curl http://localhost:3000/users/login \
-d "username=USER&password=PASSWORD"
```
=>
```
{
 "id": "ABCDEFG123456",
 "token": "AUTH-TOKEN",
 "tokenExpires": "2018-07-15T14:23:18.313Z"
}
```
Then you update card content by sending to card URL the new content:

```
curl -H "Authorization: Bearer AUTH-TOKEN" \
   -H "Content-type:application/json" \
   -X PUT \
http://localhost:3000/api/boards/ABCDEFG123456/lists/ABCDEFG123456/cards/ABCDEFG123456 \
-d '{ "title": "Card new title", "listId": "ABCDEFG123456", "description": "Card new description" }'
```

When using VBA, you can optionally:
* Use direct VBA commands to send and receive from URLs
* Download curl for Windows, and in VBA call curl.exe with those parameters, and get the result.

You can also google search how you can use JSON format files in VBA,
converting them to other formats etc. I presume there is something similar that
exists in PHP, that JSON file can be converted to PHP array, and array items accessed
individually, and array converted back to JSON.

Current Wekan REST API does not yet cover access to all data that is in MongoDB.
If you need that, REST API page also has link to Restheart, that adds REST API
to MongoDB, so youc an use all of MongoDB data directly with REST API.
https://github.com/wekan/wekan/wiki/REST-API

Wekan boards also have export JSON, where also attachments are included in JSON as
base64 encoded files. To convert them back to files, you first get whole one board exported
after authentication like this:

```
curl https://Bearer:APIKEY@ip-address/api/boards/BOARD-ID/export?authToken=#APIKEY > wekanboard.json
```

Then you read that JSON file with VBA, and get that part where in JSON is the base64 text
of the file. Then you use VBA base64 function to convert it to binary, and write content to file.

# CSV/TSC Import/Export

There is [CSV/TSV pull request](https://github.com/wekan/wekan/pull/413), but it has been made
a long time ago, it would need some work to add all the new tables, columns etc from
MongoDB database, so that it would export everything correctly.

Options are:
a) Some developer could do that work and contribute that code to Wekan as
new pull request to Wekan devel branch.

b) Use [Commercial Support](https://wekan.team) and pay for the time to get it implemented.