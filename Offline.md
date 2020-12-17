## Windows version offline

1. Download wekan-VERSION.zip from https://releases.wekan.team

2. Download node.exe for [Windows 64bit](https://nodejs.org/dist/v12.20.0/win-x64/)

3. Download Windows MongoDB .msi installer from https://www.mongodb.com/try/download/community

4. Download [start-wekan.bat](https://raw.githubusercontent.com/wekan/wekan/master/start-wekan.bat)

5. Copy files from steps 1-4 to offline Windows computer

6. Install MongoDB.msi . In installer, uncheck downloading MongoDB compass.

7. Unzip wekan-VERSION.zip and copy it's bundle directory files `node.exe` and `start-wekan.bat`

8. Edit `start-wekan.bat` with Notepad. There add windows computer IP address etc, like this, then Wekan will be at http://192.168.100/sign-in
```
SET ROOT_URL=http://192.168.0.100

SET PORT=80
```
Or other port:
```
SET ROOT_URL=http://192.168.0.100:2000

SET PORT=2000
```
Then Wekan will be at http://192.168.0.100:2000/sign-in

9. Double click `start-wekan.bat` to run it. (It may need right click, Run as Administrator).

## How to install Wekan to VirtualBox and copy to offline computer

1. Install [VirtualBox](https://www.virtualbox.org/)

2. Install [Ubuntu 20.10 64bit or newer](https://ubuntu.com) to VirtualBox

3. Install Wekan [Snap](https://github.com/wekan/wekan-snap/wiki/Install) version to Ubuntu with these commands:
```
sudo snap install wekan
```

4. Shutdown Ubuntu

5. At VirtualBox menu, export appliance to `wekan.ova` file

6. Copy `virtualbox-install.exe` and `wekan.ova` to offline computer

7. At offline computer, install virtualbox and import wekan.ova

8. Set virtualbox network to bridged:
https://github.com/wekan/wekan/wiki/virtual-appliance#how-to-use

9. Start VirtualBox and Ubuntu

10. In Ubuntu, type command:
```
ip address
```
=> it will show Ubuntu IP address

11. In Ubuntu Terminal, type with your IP address,
at below instead of 192.168.0.100:
```
sudo snap set wekan root-url='http://192.168.0.100'

sudo snap set wekan port='80'
```

12. Then at local network Wekan is at:
http://192.168.0.100