# Setup required dependencies

Requirements:
- Install [MeteorJS](https://www.meteor.com/) 
- Install [NodeJS](https://nodejs.org/en/download/releases/) (Optional but recommended)
- Install Python 2.7 (Installation through Chocolatey(`choco install python2 -y`) is recomended)
- If you are on windows 7, Install .NET 4.5.1+
- **MUST MAKE SURE TO** Install [Visual C++ 2015 Build Tools](http://landinghub.visualstudio.com/visual-cpp-build-tools), select custom and check all boxes to install all required dependencies. If there are no custom option, you have got the wrong version. It's much better than installing whole visual studio.
- Install Git
- Restart Windows (Optional but recommended)

Regarding Node Version, The wekan source requires at least**v0.10**, Tested versions for this note were as below even though it's optional, meteor should take care of all nodejs based dependency related issues.

![](https://i.imgur.com/w83BFBI.png)

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