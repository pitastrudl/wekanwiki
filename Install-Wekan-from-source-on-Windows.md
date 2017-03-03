Requirements:
- Install [MeteorJS](https://www.meteor.com/) 
- Install [NodeJS](https://nodejs.org/en/download/releases/) (Optional but recommended)
- Install Python 2.7 (Installation through Chocolatey(`choco install python2 -y`) is recomended)
- If you are on windows 7, Install .NET 4.5.1+
- Install [Visual C++ 2015 Build Tools](http://landinghub.visualstudio.com/visual-cpp-build-tools)
- Install Git
- Restart Windows (Optional but recommended)

Regarding Node Version, Tested versions for this note were, It's reported that version 0.10 works too. 
![](https://i.imgur.com/w83BFBI.png)

From this point, use Git bash to run commands to make sure everything works as is, but if you had trouble accessing meteor or npm commands via Git bash, windows CMD will most likely work without any problem.
- Inside the Git Bash, run these commands:

```
npm config -g set msvs_version 2015
meteor npm config -g set msvs_version 2015
```

Running Wekan:
- Clone the repo (`https://github.com/wekan/wekan`)
- Browse the wekan directory and run `meteor`, if you see any error regarding **xss**, do `meteor npm i --save xss` to install xss.
- open your browser, make changes and see it reflecting real-time.

Here is how it looks like,

```
git clone https://github.com/wekan/wekan
cd wekan
meteor npm install --save xss
meteor
```

![](https://i.imgur.com/aNVBhj5.png)