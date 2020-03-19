## a) Bundle with Windows Node+MongoDB

This has **highest performance and lowest RAM usage**, because there is no virtualization like Docker, Windows Subsystem for Linux, etc. Wekan is run with Windows native version of Node.js and MongoDB, directly at Windows filesystem.

1. If you have important data in Wekan, do [backup](https://github.com/wekan/wekan/wiki/Backup).

2. Install newest Node.js v12.x.x for Windows
https://nodejs.org/dist/v12.16.1/

3. Install MongoDB 4.x for Windows
https://www.mongodb.com/download-center/community

4. Download and newest Wekan bundle wekan-3.xx.zip from https://releases.wekan.team

5. Unzip wekan-3.xx.zip, it has directory name `bundle`

6. (This in not required) Like at [bundle wiki page](https://github.com/wekan/wekan/wiki/Platforms#not-exposed-to-internet-bundle-for-raspi-3-arm64-windows-and-any-nodemongo-cpu-architectures-no-automatic-updates-no-sandboxing), similarly do for bundle:
```
cd bundle/programs/server
npm install
npm install node-gyp node-pre-gyp fibers
cd ..\..\..
```
7. Download [start-wekan.bat](https://raw.githubusercontent.com/wekan/wekan/master/start-wekan.bat) to your bundle directory. Edit it for your [ROOT_URL](https://github.com/wekan/wekan/wiki/Settings) etc settings.

8. Start Wekan:
```
cd bundle
start-wekan.bat
```

9. [Add users](https://github.com/wekan/wekan/wiki/Adding-users).


***

## b) [Docker](https://github.com/wekan/wekan/wiki/Docker)

If you don't need to build Wekan, use prebuilt container with docker-compose.yml from https://github.com/wekan/wekan like this:
```
docker-compose up -d
```

If you like to build from source, clone Wekan repo:
```
git clone https://github.com/wekan/wekan
```
Then edit docker-compose.yml with [these lines uncommented](https://github.com/wekan/wekan/blob/master/docker-compose.yml#L132-L142) this way:
```
   #-------------------------------------------------------------------------------------
    # ==== BUILD wekan-app DOCKER CONTAINER FROM SOURCE, if you uncomment these ====
    # ==== and use commands: docker-compose up -d --build
    build:
      context: .
      dockerfile: Dockerfile
      args:
        - NODE_VERSION=${NODE_VERSION}
        - METEOR_RELEASE=${METEOR_RELEASE}
        - NPM_VERSION=${NPM_VERSION}
        - ARCHITECTURE=${ARCHITECTURE}
        - SRC_PATH=${SRC_PATH}
        - METEOR_EDGE=${METEOR_EDGE}
        - USE_EDGE=${USE_EDGE}
    #-------------------------------------------------------------------------------------
```
Then you can build Wekan with 
```
docker-compose up -d --build
```

## c) Windows Subsystem for Linux on Windows 10
- [Install Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/wsl2-install) in PowerShell as Administrator `Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux` and reboot
- Install Ubuntu 18.04 from Windows Store

If you don't need to build from source, download newest wekan-VERSION.zip from https://releases.wekan.team and unzip it. Then:
```
sudo apt update
sudo apt install npm mongodb-server mongodb-clients
sudo npm -g install n
sudo n 12.16.1
sudo npm -g install npm
```
Then edit `start-wekan.sh` to start at correct port, ROOT_URL setting, and MONGO_URL to port 27017, cd to correct bundle directory where `node main.js` can be run, and then:
```
./start-wekan.sh
```
More info at https://github.com/wekan/wekan/wiki/Raspberry-Pi
- You could try to proxy from IIS SSL website to Wekan localhost port, for example when ROOT_URL=https://example.com and PORT=3001 , and you make IIS config that supports websockets proxy to Wekan http port 3001.

If you need to build from source, do as above, and build Wekan with `wekan/rebuild-wekan.sh`.
After building, if you like to start meteor faster by excluding some parts, have rebuilds after file change, and test on local network devices, try with your computer IP address:
```
WITH_API=true RICHER_CARD_COMMENT_EDITOR=false ROOT_URL=http://192.168.0.200:4000 meteor --exclude-archs web.browser.legacy,web.cordova --port 4000
```
## d) VirtualBox with Ubuntu 19.10 64bit

Install Ubuntu to VirtualBox and then Wekan, for example Wekan Snap.

Currently Snap works only when installed to Ubuntu 19.10 64bit running on VirtualBox VM.

https://github.com/wekan/wekan-snap/wiki/Install

[Related VM info how to expose port with bridged networking](https://github.com/wekan/wekan/wiki/Virtual-Appliance)

[UCS has prebuilt VirtualBox VM](https://github.com/wekan/wekan/wiki/Platforms#production-univention-platform-many-apps-and-wekan)

***

# BELOW: DOES NOT WORK

## e) Probaby does not work

[Install from source directly on Windows](https://github.com/wekan/wekan/wiki/Install-Wekan-from-source-on-Windows) to get Wekan running natively on Windows. [git clone on Windows has been fixed](https://github.com/wekan/wekan/issues/977). Related: [running standalone](https://github.com/wekan/wekan/issues/883) and [nexe](https://github.com/wekan/wekan/issues/710).

## f) Install Meteor on Windows - does not build correctly, gives errors

https://github.com/zodern/windows-meteor-installer/

```
REM Install Chocolatey from
REM https://chocolatey.org/install
REM in PowerShell as Administrator

Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))

REM Install with cmd.exe or PowerShell as Administrator
REM - nodejs-lts, that is 12.x
REM - ndm, that is npm package manager for Windows

choco install -y nodejs-lts ndm git

REM Close and open cmd.exe or PowerShell as normal user.
REM Update npm:

npm -g install npm

REM Install meteor using https://github.com/zodern/windows-meteor-installer/

npm i -g @zodern/windows-meteor-installer

REM Close and open cmd.exe or PowerShell as normal user.

git clone https://github.com/wekan/wekan
cd wekan

REM a) For development, available at local network, at your computer IP address. Does rebuild when code changes.

SET WITH_API=true
SET RICHER_CARD_EDITOR=false
SET ROOT_URL=http://192.168.0.200:4000
meteorz --port 4000

REM b) For development, available only at http://localhost:4000 . Does rebuild when code changes.

SET WITH_API=true
SET RICHER_CARD_EDITOR=false
meteorz --port 4000

REM c) For production, after Wekan is built to "wekan/.build/bundle",
REM    edit "start-wekan.bat" to "cd" to correct bundle directory to run "node main.js"
```
## g) Snap

Sometime Snap could start working on WSL2, if all required options are enabled in Linux kernel included to Windows.

## Related

[Linux stuff in Windows 10 part 1](https://cepa.io/2018/02/10/linuxizing-your-windows-pc-part1/) and [part 2](https://cepa.io/2018/02/20/linuxizing-your-windows-pc-part2/).
