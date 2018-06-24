a) [Docker](https://github.com/wekan/wekan/wiki/Docker)

b) Windows Subsystem for Linux on Windows 10
- [Install Windows Subsystem for Linux](https://wiki.debian.org/InstallingDebianOn/Microsoft/Windows/SubsystemForLinux)
- Install Debian from Windows Store
- Use [VirtualBox scripts](https://github.com/wekan/wekan-maintainer/tree/master/virtualbox) of rebuild-wekan.sh etc to install and build Wekan
- Run Wekan locally with meteor at http://localhost:3000 : `cd wekan && meteor`
- Or: try to modify start-wekan.sh etc to run wekan at http://ip-address or http://example.com
- You could try to proxy from IIS SSL website to Wekan localhost port, for example when ROOT_URL=https://example.com and PORT=3001 , and you make IIS config that supports websockets proxy to Wekan http port 3001.

c) [Install from source directly on Windows](https://github.com/wekan/wekan/wiki/Install-Wekan-from-source-on-Windows) to get Wekan running natively on Windows. [git clone on Windows has been fixed](https://github.com/wekan/wekan/issues/977). Related: [running standalone](https://github.com/wekan/wekan/issues/883) and [nexe](https://github.com/wekan/wekan/issues/710).
