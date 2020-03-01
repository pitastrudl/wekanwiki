[Blogpost](https://blog.wekan.team/2019/06/wekan-on-raspi3-and-arm64-server-now-works-and-whats-next-with-cncf/index.html) - [Blogpost repost at dev.to](https://dev.to/xet7/wekan-on-raspi3-and-arm64-server-now-works-and-what-s-next-with-cncf-pbk) - [Thanks at CNCF original issue](https://github.com/cncf/cluster/issues/45#issuecomment-507036930) - [Twitter tweet](https://twitter.com/WekanApp/status/1145168007901134848) - [HN](https://news.ycombinator.com/item?id=20318237)

## Bundle files

Bundle for x64 is at https://releases.wekan.team filename wekan-3.xx.zip

Bundle for arm64 is at https://releases.wekan.team/raspi3/ filename wekan-3.xx-arm64.zip

## Install Wekan to RasPi3, RasPi4 or any arm64 server

Look at webbrowser files at https://releases.wekan.team/raspi3/

Download and open README.md, there could be text similar to this:
```
README
Currently uses Node v12.16.1 and MongoDB v3.x or v4.x
Built on Ubuntu 19.10 64bit arm64 on RasPi4.
Should work on RasPi3 and RasPi4 on Ubuntu 19.10 64bit arm64.
Install info here:
https://github.com/wekan/wekan/wiki/Raspberry-Pi
```
You should always check what distro, node etc version it has, before downloading and installing.

As of 2020-02-13, newest Wekan:
- Ubuntu 19.10 Server arm64 for RasPi3 and RasPi4
- MongoDB 3.6.x
- Newest Wekan with newest Meteor

If you have RasPi3, 1 GB RAM can only run Wekan Node.js + MongoDB. There is not enough RAM to run also Ubuntu desktop at the same RasPi.

If you have RasPi3, you can install textmode webbrowser, and download files with it:
```
sudo apt-get install elinks
elinks https://releases.wekan.team/raspi3/
```

If you have RasPi4 with 4 GB RAM, you can also install Ubuntu Desktop with:
```
sudo apt-get install ubuntu-desktop
```

Note: Raspbian is not recommended, because it is 32bit and has [32bit MongoDB that has file size limit of 2 GB](https://www.mongodb.com/blog/post/32-bit-limitations), if it grows bigger then it gets corrupted. That's why here is 64bit arm64 version of Ubuntu.

### 1. Download Ubuntu 19.10 64bit Server for RasPi and write to SD Card

Download from: https://ubuntu.com/download/raspberry-pi

Alternatively, if that link does not work, go to https://ubuntu.com, Download, IoT RasPi arm, and there select 64bit Server for your RasPi.

It seems that [RasPi website](https://www.raspberrypi.org/documentation/installation/installing-images/) recommends [BalenaEtcher GUI](https://www.balena.io/etcher/) for writing image to SD Card.

For Linux dd users, after unarchiving in file manager, if sd card is /dev/sdb, it's for example:
```
sudo su
dd if=ubuntu.img of=/dev/sdb conv=sync bs=40M status=progress
sync
exit
```
And wait for SD card light stop blinking, so it has written everything.

### 2. Preparing for booting RasPi

With RasPi, you need:
- Ubuntu SD card inserted to your RasPi.
- Ethernet cable connected to your router/modem/hub, with connection to Internet.
- USB keyboard and mouse connected.
- Monitor connected to HDMI. Or alternatively, look at your router webpage http://192.168.0.1 (or similar) what is your RasPi IP address, and ssh ubuntu@192.168.0.x with password ubuntu.
- Power cable.

Boot RasPi.

Username: ubuntu

Password: ubuntu

This info is from https://wiki.ubuntu.com/ARM/RaspberryPi

It will ask you to change your password at first login.

### 3. Wait for updates to finish

After login, type:
```
top
```
When you see `apt` or `dpkg`, automatic updates are still running. Wait for updates to finish. Then press `q` to quit top.

### 4. Install remaining updates and reboot
```
sudo apt-get update
sudo apt-get -y dist-upgrade
sudo reboot
```
### 5. Login and install Wekan related files

Look at webbrowser files at https://releases.wekan.team/raspi3/

Or install elinks textmode browser and download with it:
```
sudo apt-get install elinks
elinks https://releases.wekan.team/raspi3
```
Download and open README.md, there could be text similar to this:
```
README
Currently uses Node v12.16.1 and MongoDB v3.x or v4.x
Built on Ubuntu 19.10 arm64 on RasPi4.
Should work on RasPi3 and RasPi4 on Ubuntu 19.10 64bit.
```
Install these:
```
sudo apt-get install npm mongodb-server mongodb-clients mongodb-tools zip unzip
sudo npm -g install npm
sudo npm -g install n
```
Then from README.md you downloaded, look at Node version, and install it, for example:
```
sudo n 12.16.1
```
Then look again files:
```
elinks https://releases.wekan.team/raspi3/
```
Download there from files like these:
```
wget https://releases.wekan.team/raspi3/wekan-3.xx-arm64.zip
```
Also download newest start-wekan.sh:
```
wget https://raw.githubusercontent.com/wekan/wekan/master/start-wekan.sh
```
With elinks, you can use arrow keys to navigate, and enter to download file to current directory.

Then unzip file:
```
unzip wekan*.zip
```

### 6. Running Wekan as service

If you would like to run node as non-root user, and still have node at port 80, you could add capability to it, by first looking where node binary is:
```
which node
```
And then adding capability to that path of node, for example:
```
sudo setcap cap_net_bind_service=+ep /usr/local/bin/node
```
This is modified version from https://www.certdepot.net/rhel7-install-wekan/

Edit this new service file:
```
sudo nano /etc/systemd/system/wekan.service
```
There add this text:
```
[Unit]
Description=The Wekan Service
After=syslog.target network.target

[Service]
EnvironmentFile=/etc/default/wekan
User=ubuntu
Group=ubuntu
WorkingDirectory=/home/ubuntu/bundle
ExecStart=/usr/local/bin/node main.js
Restart=on-failure
SuccessExitStatus=143

[Install]
WantedBy=multi-user.target
```
Look at what is your IP address at eth0, for example 192.168.0.x, with this command, and write it somewhere to your other computer or phone or paper:
```
ip address
```
IP address will be added as your ROOT_URL.

You could also login to your router for example at http://192.168.0.1 to set static IP pointing always to your specific RasPi IP address, so that address would not change.

Then edit this file:
```
sudo nano /etc/default/wekan
```
There add this text:
```
NODE_ENV=production
WITH_API=true
MONGO_URL=mongodb://127.0.0.1:27017/wekan
ROOT_URL=http://192.168.0.x
PORT=80
```
There are [many more other possible settings here that you can optionally add](https://raw.githubusercontent.com/wekan/wekan/master/start-wekan.sh)

After that start and enable Wekan:
```
sudo systemctl start wekan
sudo systemctl enable wekan
```

Wekan should work at your ROOT_URL in your webbrowser like http://192.168.0.x


## 7. Optional: Email

Note: Configuring email is not required to use Wekan.

If you really would like to install email sending server,
you could install [postfix](https://github.com/wekan/wekan-bash-install-autoupgrade/blob/master/install.sh#L63-L67), but that would probably make your mail to spam banning lists. You would add to above settings:
```
MAIL_URL='smtp://127.0.0.1:25/'
MAIL_FROM='Board Support <wekan@example.com>'
```
It is much more recommended to use [email sending service like AWS SES or some other service](https://github.com/wekan/wekan/wiki/Troubleshooting-Mail) that can ensure delivering email correctly, for Wekan email notifications etc.

## 8. Optional: Nginx and Let's Encrypt SSL

If your router has ports forwarded to your RasPi (in virtual server settings at http://192.168.0.1), then you could also [install nginx and Let's Encrypt SSL](https://github.com/wekan/wekan-bash-install-autoupgrade/blob/master/install.sh) in front of Wekan.

## 9. Updating Wekan
Stop Wekan and move old stuff away:
```
sudo systemctl stop wekan
mkdir old
mv wekan*.zip old/
mv bundle old/
```
Download new Wekan version:
```
elinks https://releases.wekan.team/raspi3/
```
There with keyboard arrow keys go move to top of newest `wekan-3.xx-arm64.zip` and press Enter to download.

Also check README.md about what Node version newest Wekan uses.

In elinks press `q` to exit elinks

Unzip and start Wekan:
```
unzip wekan*.zip
sudo systemctl start wekan
```
If it works, delete old files:
```
rm -rf old
```


***

# STOP HERE. OLD NOT NEEDED INFO BELOW.

***

### b) Running Wekan with startup script
Look at what is your IP address at eth0, for example 192.168.0.x, with this command, and write it somewhere to your other computer or phone or paper:
```
ip address
```
You could also login to your router for example at http://192.168.0.1 to set static IP pointing always to your specific RasPi IP address, so that address would not change.

Make start-wekan.sh executeable, and edit it:
```
chmod +x start-wekan.sh
nano start-wekan.sh
```
There change ROOT_URL like [described here](https://github.com/wekan/wekan/Settings),
for example your RasPi IP address and port, and MongoDB URL:
```
export ROOT_URL=http://192.168.0.x:2000
export PORT=2000
export MONGO_URL='mongodb://127.0.0.1:27017/wekan'
```
If you would like to run node as non-root user, and still have node at port 80, you could add capability to it, by first looking where node binary is:
```
which node
```
And then adding capability to that path of node, for example:
```
sudo setcap cap_net_bind_service=+ep /usr/local/bin/node
```
Then change to start-wekan.sh:
```
export ROOT_URL=http://192.168.0.x
export PORT=80
export MONGO_URL='mongodb://127.0.0.1:27017/wekan'
```
Also in start-wekan changing directory like this:
```
cd bundle
node main.js
```
You need to check that it changes to correct directory, so that it can start `node main.js`

And then start Wekan with:
```
./start-wekan.sh
``

***


## Wekan for RasPi3 arm64 and other CPU architectures

<img src="https://wekan.github.io/wekan-raspi3.png" width="100%" alt="Wekan on RasPi3" />

Newest Wekan:
- Ubuntu 19.10 Server arm64 for RasPi3 and RasPi4
- MongoDB 3.6.x
- Newest Wekan with newest Meteor

To test RasPi3, xet7 tested it with all his Wekan boards data:
```
mongorestore --drop
```
If there is errors in restoring, try:
```
mongorestore --drop --noIndexRestore
```
<img src="https://wekan.github.io/wekan-raspi3-with-all-data.jpg" width="100%" alt="Wekan on RasPi3" />

When using Firefox on network laptop (Core 2 Duo laptop, 8 GB RAM, SSD harddisk) to browse RasPi Wekan server, small boards load at about 3 seconds at first time. When loading, node CPU usage goes to about 100%. MongoDB CPU usage stays low, sometimes goes to 18%. This is because indexes has been added to Wekan MongoDB database. Loading my biggest Wekan board at first time takes 45 seconds, and next time takes about 2 seconds, because data is at browser cache. When Wekan browser tab is closed, node CPU usage drops 4-23%. There is no errors given by Wekan at RasPi3, RasPi3 arm64 behaves similar to x64 server that has 1 GB RAM. 

<img src="https://wekan.github.io/wekan-raspi3-cpu-usage.jpg" width="100%" alt="Wekan on RasPi3" />

I did also test Wekan arm64 on arm64 bare metal server, same Wekan bundle worked there.

# Old info below

.7z size 876 MB, unarchived RasPi3 .img size of 4.5 GB. At first boot disk image expands to full SD card size.

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

5) Restore your Wekan dump subdirectory
```
mongorestore --drop --noIndexRestore
```
6) Start Wekan:
```
./start-wekan.sh
```
And maybe [run as service](https://www.certdepot.net/rhel7-install-wekan/)

Or start at boot, by having [at bottom of /etc/rc.local](https://github.com/wekan/wekan/blob/master/releases/virtualbox/etc-rc.local.txt).

7) On other computer, with webbrowser go to http://192.168.0.12 (or other of your IP address you changed to start-wekan.sh)

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

#### Upgrade bundle

Stop Wekan. See what is newest bundle version at https://releases.wekan.team .

Then, for example:
```
cd ~/repos
rm -rf bundle
wget https://releases.wekan.team/wekan-3.01.zip
unzip wekan-3.01.zip
cd bundle/programs/server
npm install
npm install node-gyp node-pre-gyp fibers    (maybe not needed)
cd ../../..
```
Then Start Wekan.

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

1) Bundle at https://releases.wekan.team/raspi3/ was created this way originally on Xubuntu 19.10 x64. This is because officially Meteor only supports x32 and x64. One workaround would be to [add patch to allow other architecture, like this](https://github.com/wekan/meteor/commit/014fe0469bc75eb0371b90464befebc883a08a26). But better workaround is to just build bundle on x64 and then on other architectures download bundle and reinstall npm packages.
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
