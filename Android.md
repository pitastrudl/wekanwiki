### Running Wekan server at Android

Requirements:
- arm64 or x64 Android with at least 3 GB RAM. Tested with with arm64 OnePlus 3 that has 6 GB RAM.
- It is not necessary to root Android.

## 1) Install AnLinux and Termux from Play Store

At AnLinux choose:
- Ubuntu
- XFCE4
- Copy those commands to Termux to install Linux.

## 2) At Termux

When you get from Termux to Ubuntu bash, you can install Wekan similarly like arm64 or x64:
https://github.com/wekan/wekan/wiki/Raspberry-Pi

Edit start-wekan.sh so you can start Wekan for example:
```
ROOT_URL=http://localhost:2000
PORT=2000
```
At Android webbrowser like Chrome and Firefox browse to http://localhost:2000

## 3) WLAN

If you connect to WLAN, you can get your IP address with command:
```
ip address
```
Edit start-wekan.sh so you can start Wekan for example:
```
ROOT_URL=http://IP-ADDRESS:2000
PORT=2000
```
Then you can use any computer or mobile phone Javascript capable webbrowser at WLAN to use Wekan at http://IP-ADDRESS:2000 like http://192.168.0.100:2000