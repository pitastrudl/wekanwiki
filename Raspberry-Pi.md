## Wekan for RasPi3 arm64 and other CPU architectures

- Ubuntu 18.04 Server arm64 for RasPi3
- Has MongoDB 3.6.x running

Note: Raspbian is not recommended, because it is 32bit and has 32bit MongoDB that has file size limit of 2 GB, if it grows bigger then it gets corrupted. That's why here is arm64 version of Ubuntu 18.04.

### Download

.7z size 876 MB, unarchived RasPi3 .img size of 4.5 GB:

https://releases.wekan.team/raspi3/wekan-2.94-raspi3-ubuntu18.04server.img.7z

Or alternatively Wekan Meteor 1.8.1 bundle for arm64:

https://releases.wekan.team/raspi3/wekan-2.94-arm64-bundle.tar.gz

### How to use .img

1) Write image to SD card
```
sudo apt-get install p7zip-full
7z x wekan-2.94-raspi3-ubuntu18.04server.img.7z
sudo dd if=wekan-2.94-raspi3-ubuntu18.04server.img of=/dev/mmcblk0 conv=sync status=progress bs=100M
```

At first boot disk image expands to full SD card size.

2) Login for Wekan files
- Username wekan
- Password wekan (for Wekan files)

(Or for ubuntu user: username ubuntu password ubuntuubuntu)

3) After login as wekan user, check IP address with command:
```
ip address
```
4) Change that IP addess to start-wekan.sh:
```
cd repos
nano start-wekan.sh
```
There change ROOT_URL to have your IP address. Save and Exit: Ctrl-o Enter Ctrl-x Enter

5) Start Wekan:
```
./start-wekan.sh
```
6) On other computer, with webbrowser go to http://192.168.0.12 (or other of your IP address you changed to start-wekan.sh)

### How to use bundle

#### a) On any Ubuntu 18.04 arm64 server
```
wget https://releases.wekan.team/raspi3/wekan-2.94-arm64-bundle.tar.gz
tar -xzf wekan-2.94-arm64-bundle.tar.gz
sudo apt-get install build-essential curl make nodejs npm mongodb-clients mongodb-server
sudo npm -g install npm
sudo npm -g install n
sudo n 8.16.0
sudo systemctl start mongodb
sudo systemctl enable mongodb
wget https://releases.wekan.team/raspi3/start-wekan.sh
nano start-wekan.sh
```
There edit [ROOT_URL to have your IP address or domain, and PORT for your localhost port](https://github.com/wekan/wekan/wiki/Settings). 

You can also allow node to run on port 80, when you check where node is:
```
which node
```
and then allow it:
```
sudo setcap cap_net_bind_service=+ep /usr/local/bin/node
```
[Adding users](https://github.com/wekan/wekan/wiki/Adding-users)

#### b) Other CPU architectures

Do as above, but then also install node packages for your architecture:
```
cd bundle/programs/server
npm install
npm install node-gyp node-pre-gyp fibers
cd ../../..
```
Then start Wekan
```
./start-wekan.sh
```

#### c) Even more something?

Well, you could get some other newest Meteor x64 bundle, like RocketChat, and this way make it run on your CPU architecture, that has required Node+NPM+MongoDB.

### How this was done

1) Bundle at https://releases.wekan.team/raspi3/ was created this way originally on Xubuntu 19.10 x64:
```
git clone https://github.com/wekan/wekan
cd wekan
git checkout meteor-1.8
./rebuild-wekan.sh
# 1 and Enter to install deps
./rebuild-wekan.sh
# 2 and Enter to build Wekan
cd .build
```
Then create tar.gz that included bundle directory, with name wekan-VERSION.tar.gz

Ready-made bundles of Meteor 1.6 Wekan x64 at https://releases.wekan.team

Ready-made bundle of Meteor 1.8 Wekan for arm64 at https://releases.wekan.team , works at RasPi3, and any other arm64 server that has Ubuntu 18.04 arm64.

2) Ubuntu Server for RasPi3 from https://www.raspberrypi.org/downloads/

Write to SD card.

Boot:
- Username ubuntu
- Password ubuntu
- It asks to change password at first boot.

3) Create new user:
```
sudo adduser wekan
```
Add name wekan, password wekan, and then other empty with Enter, and accept with Y.

4) Add passwordless sudo:
```
export EDITOR=nano
sudo visudo
```
There below root add:
```
wekan  ALL=(ALL:ALL) NOPASSWD:ALL
```
Save and Exit: Ctrl-o Enter Ctrl-x Enter

5) Logout, and login

- Username wekan
- Password wekan

6) Download bundle etc

See above about downloading bundle, start-wekan.sh, dependencies etc.

7) Shutdown RasPi3
``` 
sudo shutdown -h now
```

8) At computer, insert SD card and unmount partitions:
```
sudo umount /dev/mmcblk0p1 /dev/mmcblk0p2
```
9) Read SD card to image
```
sudo dd if=/dev/mmcblk0 of=wekan-2.94-raspi3-ubuntu18.04server.img conv=sync status=progress
```
10) Resize image to smaller from 32 GB to 4.5 GB:

Resize script is [originally from here](https://evilshit.wordpress.com/2014/02/07/how-to-trim-disk-images-to-partition-size/).
```
wget https://releases.wekan.team/raspi3/resize.sh
chmod +x resize.sh
sudo ./resize.sh wekan-2.94-raspi3-ubuntu18.04server.img
```
11) Make .7z archive to pack about 4.5 GB to about 800 MB:
```
7z a wekan-2.94-raspi3-ubuntu18.04server.img.7z wekan-2.94-raspi3-ubuntu18.04server.img
```
