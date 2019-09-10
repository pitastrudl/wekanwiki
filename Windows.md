## a) Bundle with Windows Node+MongoDB - highest performance, lowest RAM usage

1. Install newest Node.js v8.x.x for Windows
https://nodejs.org/dist/v8.16.1/

2. Install MongoDB 4.x for Windows
https://www.mongodb.com/download-center/community

3. Download and newest Wekan bundle wekan-3.xx.zip from https://releases.wekan.team

4. Unzip wekan-3.xx.zip, it has directory name `bundle`

5. Like at [bundle wiki page](https://github.com/wekan/wekan/wiki/Platforms#not-exposed-to-internet-bundle-for-raspi-3-arm64-windows-and-any-nodemongo-cpu-architectures-no-automatic-updates-no-sandboxing), similarly do for bundle:
```
cd bundle/programs/server
npm install
npm install node-gyp node-pre-gyp fibers
cd ..\..\..
```
6. Download [start-wekan.bat](https://raw.githubusercontent.com/wekan/wekan/master/start-wekan.bat) to your bundle directory. Edit it for your [ROOT_URL](https://github.com/wekan/wekan/wiki/Settings) etc settings.

7. Start Wekan:
```
cd bundle
start-wekan.bat
```

## b) [Docker](https://github.com/wekan/wekan/wiki/Docker)

## c) Windows Subsystem for Linux on Windows 10
- [Install Windows Subsystem for Linux](https://wiki.debian.org/InstallingDebianOn/Microsoft/Windows/SubsystemForLinux)
- Install Debian from Windows Store
- Use [VirtualBox scripts](https://github.com/wekan/wekan-maintainer/tree/master/virtualbox) of rebuild-wekan.sh etc to install and build Wekan
- Run Wekan locally with meteor at http://localhost:3000 : `cd wekan && meteor`
- Or: try to modify start-wekan.sh etc to run wekan at http://ip-address or http://example.com
- You could try to proxy from IIS SSL website to Wekan localhost port, for example when ROOT_URL=https://example.com and PORT=3001 , and you make IIS config that supports websockets proxy to Wekan http port 3001.

## d) Probaby does not work: [Install from source directly on Windows](https://github.com/wekan/wekan/wiki/Install-Wekan-from-source-on-Windows) to get Wekan running natively on Windows. [git clone on Windows has been fixed](https://github.com/wekan/wekan/issues/977). Related: [running standalone](https://github.com/wekan/wekan/issues/883) and [nexe](https://github.com/wekan/wekan/issues/710).

## Related

[Linux stuff in Windows 10 part 1](https://cepa.io/2018/02/10/linuxizing-your-windows-pc-part1/) and [part 2](https://cepa.io/2018/02/20/linuxizing-your-windows-pc-part2/).
