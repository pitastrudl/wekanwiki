### Running Wekan server at Android

Requirements:
- arm64 or x64 Android with at least 3 GB RAM. Tested with with OnePlus 3 that has 6 GB RAM.
- It is not necessary to root Android.

## 1) Install AnLinux and Termux from Play Store

At AnLinux choose:
- Ubuntu
- XFCE4
- Copy those commands to Termux to install Linux.

## 2) At Termux

When you get from Termux to Ubuntu bash, you can install Wekan similarly like Raspberry Pi arm64:
https://github.com/wekan/wekan/wiki/Raspberry-Pi

And edit start-wekan.sh so you can start Wekan for example:
```
ROOT_URL=http://localhost:2000
PORT=2000
```
And at Android webbrowser like Chrome and Firefox browse to http://localhost:2000