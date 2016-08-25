THIS PAGE IN IN PROGRESS, NOT FINISHED YET.

Tested on Windows 10.

Source install is based on this page:
https://github.com/wekan/wekan/wiki/Install-and-Update#install-manually-from-source

1) Install [newest Node.js 0.10.x for Windows](https://nodejs.org/dist/latest-v0.10.x/).

2) Install [Chocolatey](https://chocolatey.org/install).

3) Install Git, Python2.7, and Microsoft Build Tools of Visual Studio 2015
for building Node.js extensions from source:

```
# Use cmd.exe as Administrator
choco install -y git python2 visualstudio2015community microsoft-build-tools
npm config set python C:\tools\python2\python.exe
npm config set msvs_version 2015
```

4) Install [Meteor Windows installer](https://www.meteor.com)

5) Clone Wekan git repo:

```
# Use cmd.exe as your normal user (not Administrator).
cd C:\Users\YOUR-USERNAME\Documents
git clone https://github.com/wekan/wekan.git
cd wekan
npm install -g node-gyp
npm install
# Change to older meteor version
meteor update --release 1.3.5.1
meteor build .build --directory
cd .build\bundle\programs\server
npm install
```

TODO:

* Try to get [node-gyp](https://github.com/nodejs/node-gyp) working, currently Visual Studio 2015 Community install in progress on my laptop
* Try to [get fibers compiled](https://forums.meteor.com/t/one-deployment-method-for-a-meteor-application-on-windows/13928/21) and maybe even create installer for Wekan
* Add mongo with ```npm install mongod``` or install separate mongo, version 3.2.9
* Add instructions how to run Wekan Node.js as service using for example [NSSM](https://nssm.cc)
* Add instructions of workaround, how to change Firefox language to English by removing other languages from settings, so it's possible to login to Wekan, this bypasses missing migrations of language to new version