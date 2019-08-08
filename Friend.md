[Wekan integration to Friend TODO list, In Progress](https://github.com/FriendUPCloud/friendup/issues/114)

Friend Cloud OS: Secure encrypted skinnable fast Open Source desktop in webbrowser/mobile/desktop app. Wekan as one app at Friend.

## Contributor Agreement

Sign [Contributor Agreement](https://friendup.cloud/contributors/) and come to build secure encrypted Open Source Friend Cloud OS that has Wekan app.

Also looking for partners, please come to developer chat at Discord, link below.

## Chat

[Friend developer chat at Discord](https://discord.gg/HQ93NFG) - [direct link](https://discordapp.com/channels/459616484369498123/459616484369498131). At Chat above also looking for new contributors to sign [Contributor Agreement](https://friendup.cloud/contributors/) and partners (making press release with m0ns00n).

Not in use currently: IRC at Freenode #friendup

## Website

[Friend Website](https://friendup.cloud)

## Video

https://www.youtube.com/watch?v=SB4dNC7u2MU

## Roadmap

It's possible to use Wekan with Friend and [there will be more Wekan integration to Friend](https://github.com/wekan/wekan/milestone/60) so [now 2019-06-30 that Wekan also works at RasPi3](https://github.com/wekan/wekan/wiki/Raspberry-Pi) like Friend already works, it makes possible local RasPi3-only network.

Then on local network you can use RasPi3 Cromium or Friend mobile/tablet Android/iOS app to connect to local network Friend desktop, also possible without connection to Internet.

If using RasPi4 with 4 GB RAM instead, it's possible to run Wekan+Friend+Desktop etc on same RasPi4, servers+client webbrowser.

## Screenshot

Wekan Friend development version at Friend Desktop. Not released to Friend Store yet.

![Wekan Friend development version screenshot](https://wekan.github.io/wekan-friend-dev.png)

[More Screenshots of Wekan and Friend](https://blog.wekan.team/2018/05/upcoming-wekan-v1-00-and-platforms/index.html)

## Source code

[Friend Server source code at GitHub](https://github.com/FriendUPCloud/friendup). Mobile apps are not at GitHub yet.

[Friend Apps source code at GitHub](https://github.com/FriendUPCloud/friend-applications)

[Wekan FriendUPApp source code at GitHub](https://github.com/wekan/FriendUPApp)

Friend repos:

- https://github.com/FriendSoftwareLabs/
- https://github.com/FriendUPCloud/

[Docker: In progress](https://github.com/wekan/docker-friendup)

## Demo

Sign Up to Friend:

- https://go.friendup.cloud/

Old:

- [New development v1.2rc1 Friend demo](https://my.friendup.cloud)

- [Old Friend demo](https://friendsky.cloud)

## Bounties

[Friend bounties](https://friendup.tech/page/bounties.html)

## News about upcoming Wekan at Friend

[Friend Software Labs Releases FriendUP v1.2 Release Candidate](https://medium.com/friendupcloud/friend-software-labs-releases-friendup-v1-2-release-candidate-637d7bf800d4)

[Medium 2018-01-26: With Friend Wekan!](https://medium.com/friendupcloud/with-friend-wekan-707af8d04d9f), you can [discuss at Hacker News](https://news.ycombinator.com/item?id=16240639)

## News about Friend

[Video of Friend Desktop walkthrough](https://www.youtube.com/watch?v=PX-74ooqino)

[Friend Network and Friend Store questions answered](https://medium.com/friendupcloud/friend-network-and-friend-store-questions-answered-56fefff5506a)

[How Friend Store unifies Blockchain projects](https://medium.com/friendupcloud/how-friend-store-unifies-blockchain-projects-d3a889874bec)

[Video of Friend Talk at Blockchangers Event - Oslo 2018](https://www.youtube.com/watch?v=7AsSlFenRwQ)

[Video of Friend talk at DeveloperWeek 2018](https://medium.com/friendupcloud/video-of-our-talk-at-developerweek-2018-e9b10246a92f)

[Video review about Friend ICO](https://www.youtube.com/watch?v=LP7r_jrVfXQ), video has note that some corrections to that video details are at Friend website.

[FriendUp Launches TGE, Meeting Norwegian Values of Ethical Business and Transparency](https://www.coinspeaker.com/2018/02/23/friendup-launches-tge-meeting-norwegian-values-ethical-business-transparency/)

[Friend announces partnership with Hove Medical Systems AS](https://friendup.cloud/friend-hove-medical-partnership/)

[Friend interview at FLOSS450](https://twit.tv/shows/floss-weekly/episodes/450)

***

## Install from Source

### 1. Setup new Ubuntu 16.04 64bit server or VM

Install script currently works only on Ubuntu 16.04 (and similar Xubuntu 16.04 64bit etc).

### 2. Install git and create repos directory

```
sudo apt-get update
sudo apt-get install git
mkdir ~/repos
cd repos
```
### 3. Clone Friend server repo
```
git clone https://github.com/FriendUPCloud/friendup
```
### 4. Clone Friend Apps repos
```
git clone https://github.com/FriendUPCloud/friend-applications
```
### 5. Clone Friend Chat repo
```
git clone https://github.com/FriendSoftwareLabs/friendchat
```
### 6. Clone Wekan App repo
```
git clone https://github.com/wekan/FriendUPApp
```
### 7. Optional: Clone Webmail repo
```
git clone https://github.com/RainLoop/rainloop-webmail
```
### 8. Install Friend to `~/repos/friendup/build` directory
This will install:
- MySQL database, credentials are in install.sh script, can be changed
- Untrusted SSL certificate for Friend with OpenSSL command
```
cd friendup
./install.sh
```
### 9. Add Wekan app
```
cd ~/repos/friendup/build/resources/webclient/apps
ln -s ~/repos/FriendUPApp/Wekan Wekan
```
### 10. Add other apps
```
cd ~/repos/friendup/build/resources/webclient/apps
ln -s ~/repos/FriendUPCloud/friend-applications/Astray Astray
ln -s ~/repos/FriendUPCloud/friend-applications/CNESSatellites CNESSatellites
ln -s ~/repos/FriendUPCloud/friend-applications/CubeSlam CubeSlam
ln -s ~/repos/FriendUPCloud/friend-applications/Doom Doom
ln -s ~/repos/FriendUPCloud/friend-applications/FriendBrowser FriendBrowser
ln -s ~/repos/FriendUPCloud/friend-applications/GameOfBombs GameOfBombs
ln -s ~/repos/FriendUPCloud/friend-applications/GeoGuessr GeoGuessr
ln -s ~/repos/FriendUPCloud/friend-applications/Instagram Instagram
ln -s ~/repos/FriendUPCloud/friend-applications/InternetArchive InternetArchive
ln -s ~/repos/FriendUPCloud/friend-applications/MissileGame MissileGame
ln -s ~/repos/FriendUPCloud/friend-applications/Photopea Photopea
ln -s ~/repos/FriendUPCloud/friend-applications/PolarrPhotoEditor PolarrPhotoEditor
ln -s ~/repos/FriendUPCloud/friend-applications/Swooop Swooop
ln -s ~/repos/FriendUPCloud/friend-applications/TED TED
```
### 11. Optional: Add custom modules
```
cd ~/repos/friendup/build/modules
ln -s ~/repos/mysupermodule mysupermodule
```
### 12. Install [Wekan Snap](https://github.com/wekan/wekan-snap/wiki/Install)
```
sudo apt-get -y install snapd
sudo snap install wekan
```
### 13. [ROOT_URL settings](https://github.com/wekan/wekan/wiki/Settings)
```
sudo snap set wekan root-url='http://localhost:5000'
sudo snap set wekan port='5000'
```
### 14a) Trusted URL
Configure [trusted url](https://github.com/wekan/wekan-snap/wiki/Supported-settings-keys) to allow Friend to iframe Wekan.
```
sudo snap set wekan trusted-url='https://friendup.example.com'
```
### 14b) Disable browser policy and allow any website to iframe Wekan
Not recommended.
```
sudo snap set wekan browser-policy-enabled='false'
```
### 15) Start Wekan
```
sudo snap start wekan
sudo snap enable wekan
```
### 16) Start Friend
a) To background:
```
cd ~/repos/friendup/build
./nohup_FriendCore.sh
```
b) to foreground, useful when developing:
```
./Phonix_FriendCore.sh
```
or some of the following
```
./Phonix_FriendCoreGDB.sh
./ValgrindGriendCore.sh
```
### 17) Use with webbrowser

Chrome or Chromium works best 32bit/64bit OS and also with Raspberry Pi on ARM.

https://localhost:6502/webclient/index.html

Username: fadmin

Password: securefassword

### 18) Use with mobile app

Play Store: FriendUP by Friend Software Labs

iOS App Store for iPhone/iPad: If not at App Store, ask 

Using Friend Android app to connect to your Friend server URL.

There is also Friend iOS app, but I think it's not yet officially released. If someone is interested, invite to iOS Testflight can be had from [Friend chat](https://github.com/wekan/wekan/wiki/Friend).


# Adding app icons to Friend desktop menus

@CraigL: I found that when I added my web apps to the Dock (by dragging the .jsx file onto it) The app list (on the left side) in the Dock editor showed the full path of the application even after adding a "Display Name" field entry. What I did was to use the Display Name entry for the App list (if available). What I ended up with was:
Orig:
     App List => /Home/apps/Youtube/YouTube.jsx
New:
     App List => YouTube

[My change is here](https://github.com/344Clinton/friendup/commit/6943cc3c05d74adc147950fb2a272d025b50e680). The fix was simple enough. Tracking it down took me a long time :grinning:
