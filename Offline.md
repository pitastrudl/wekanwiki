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