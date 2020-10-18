## Installing Wekan Snap to Chromebook

Installing to Asus Chromebook C223NA-GJ0007 11.6" laptop, that was cheapest available at local shop, did cost 199 euro.

It has:
- 4 GB RAM
- 32 GB eMMC disk
- Intel® Celeron® N3350 CPU
- Bluetooth
- webcam
- WLAN
- USB3
- 2 x USB-C, both work for charging (I have not tried data transfer yet)
- microSD
- package included USB-C charger and USB mouse
- keys for fullscreen, switch apps, brighness, volume, those do not need any modifier keys like other laptops
- playing youtube videos fullscreen works very well
- speakers sound can be set to very loud if needed
- big enough keys, good keyboard layout
- small and lightweight laptop
- has Play Store Android apps and Linux apps that can work fullscreen
- I did not try yet replacing Chrome OS with full Linux https://galliumos.org that has some drivers Chromebook needs, but according to their [hardware compatibility](https://wiki.galliumos.org/Hardware_Compatibility) this model has Known issues: internal audio, suspend/resume, when using galliumos.

### 1) Install Linux Beta

At Chromebook settings, install Linux Beta. It will have Debian 10, that will be changed to Ubuntu 20.04 64bit.

### 2) Install Ubuntu Container

[Source](http://intertwingly.net/blog/2020/07/21/Ubuntu-20-04-on-Chromebook)

Start by entering the Chrome shell (crosh) by pressing CTRL+ALT+T, then enter the default termina VM:
```
vmc start termina
```
Delete the default penguin container that had Debian 10:
```
lxc stop penguin --force
lxc rm penguin
```
Create a new Ubuntu container named penguin:
```
lxc launch ubuntu:20.04 penguin
```
Enter the new container (as root):
```
lxc exec penguin -- bash
```
### 3) Import public keys

While Ubuntu 20.04 will install, various apt commands will fail due to an inability to verify GPG keys. This problem is not unique to Crostini, it is seen in other environments, like Raspberry Pis.

The fix is to import two public keys:
```
apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 7638D0442B90D010
apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 04EE7237B7D453EC
```
### 4) Update groups
```
groups ubuntu >update-groups
sed -i 'y/ /,/; s/ubuntu,:,ubuntu,/sudo usermod -aG /; s/$/ \$USER/' update-groups
killall -u ubuntu
userdel -r ubuntu # ignore warning about mail spool
sed -i '/^ubuntu/d' /etc/sudoers.d/90-cloud-init-users
```
### 5) Install Crostini packages

Prepare for installing Google's Crostini specific packages. First bring Ubuntu up to date:
```
apt update
apt upgrade -y
```
Now add the Crostini package repository to apt. This repository provides the Linux integration with Chrome OS (ignore RLIMIT_CORE warning):
```
echo "deb https://storage.googleapis.com/cros-packages stretch main" > /etc/apt/sources.list.d/cros.list
if [ -f /dev/.cros_milestone ]; then sudo sed -i "s?packages?packages/$(cat /dev/.cros_milestone)?" /etc/apt/sources.list.d/cros.list; fi
apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 1397BC53640DB551
apt update
```
A work-around is needed for a cros-ui-config package installation conflict. First, install binutils to get the ar command:
```
apt install -y binutils
```
Then create the cros-ui-config work-around package:
```
apt download cros-ui-config # ignore any warning messages
ar x cros-ui-config_0.12_all.deb data.tar.gz
gunzip data.tar.gz
tar f data.tar --delete ./etc/gtk-3.0/settings.ini
gzip data.tar
ar r cros-ui-config_0.12_all.deb data.tar.gz
rm -rf data.tar.gz
```
Now install the Crostini packages and the "work-around" package, ignoring any warning messages. This will take awhile:
```
apt install -y cros-guest-tools ./cros-ui-config_0.12_all.deb
```
Delete the "work-around" package:
```
rm cros-ui-config_0.12_all.deb
```
Install the adwaita-icon-theme-full package. Without this package, GUI Linux apps may have a very small cursor:
```
apt install -y adwaita-icon-theme-full
```
Now, shut down the container:
```
shutdown -h now
```
Reboot Chrome OS and start the Terminal application from the launcher. If it fails to start the first time, try again and it should work.

Rebooting is by clicking desktop right bottom clock / Power icon. After Chromebook has shutdown, short press laptop power button to start Chromebook.

### 6) Edit the user and host names

By default, Crostini will have created you a user with a name that matches your Google id. If you want something different, you can follow the instructions to Change Default Username, reproduced here:

Exit the terminal, then launch the Chrome shell (crosh) once again by pressing CTRL+ALT+T, from there enter the default termina VM, and from there log in to the container as root:
```
vmc start termina
lxc exec penguin -- bash
```
### 7) Change your Ubuntu username to Wekan

Change below `markstoberg` to your Ubuntu username, that is usually your google username.
If you get errors on below commands, like `process number 189 running on that username`
then you can kill that process number, for example `kill -9 189` and try that command again.
```
killall --user markstosberg
groupmod --new-name weka markstosberg
usermod --move-home --home /home/wekan --login wekan markstosberg
usermod --append --groups users wekan
loginctl enable-linger wekan
```

### 8) Change Ubuntu container hostname

For example:
```
hostnamectl set-hostname wekanserver
```
The container name (which you generally don't see) will remain penguin, but the host name (which is what you see in places like bash prompts) will be changed.

Once you are complete, exit all three by pressing control-d, then entering
```
lxc stop penguin
``` 
Then press control-d two more times.

Reboot Chromebook by clicking desktop right bottom clock / Power icon. After Chromebook has shutdown, short press laptop power button to start Chromebook.

### 9) Optional, if you install some Snap GUI apps

These at 9) are from same [Source](http://intertwingly.net/blog/2020/07/21/Ubuntu-20-04-on-Chromebook)
but xet7 did not test them.

The fix is to copy the desktop and pixmap files to your .local environment:
```
mkdir -p ~/.local/share/pixmaps
cp /snap/code/current/snap/gui/com.visualstudio.code.png ~/.local/share/pixmaps
cp /snap/code/current/snap/gui/code.desktop ~/.local/share/applications
```
Finally, you will need to change three lines in the code.desktop file in your ~/.local directory.

First, you will need to change Exec=code to specify the full path, namely Exec=/snap/bin/code.

Next, in the two places where Icon= is defined, you will need to replace this with the path to the icon that you copied into your .local directory. In my case, the resulting lines look as follows:

Icon=/home/rubys/.local/share/pixmaps/com.visualstudio.code.png

Once these changes are made, you should be able to launch the application using the Launcher in the lower left hand corder of the screen, by clicking on the circle, entering code into the search box and then clicking on the Visual Studio Code icon. Once launched, the application will appear in the shelf at the bottom of the screen. Right clicking on this icon will give you the option to pin the application to the shelf.

It is still a beta, and the installation instructions (above) are still a bit daunting. More importantly, things that used to work can stop working at any time, like, for example, Ubuntu 18.04.

That being said, it is a full, no-compromise Ubuntu. I've developed and tested code using this setup. I even have installed my full development environment using Puppet.

The only glitch I do see is occasionally GUI applications don't receive keystrokes. This is generally fixed by switching focus to Chromebook application and then back again. Once the application is able to process keystrokes, it remains able to do so.

### 10) Install Wekan

At Ubuntu terminal:
```
sudo snap install wekan

sudo snap set wekan port='2000'
```
Look at your Chromebook wifi settings `(i)`, what is your laptop IP address, and use it with below http address:
```
sudo snap set wekan root-url='http://192.168.0.2:2000'
```
At Chromebook settings / Linux Beta / > / Port forwarding, forwart port `2000` with nickname like for example `wekan`. This does forward Chromebook port to inside Ubuntu 20.04 64bit LXC container where Wekan is running.

Then at your local network, you can use any computer or mobile webbrowser to login at your Chromebook address like http://192.168.0.2:2000/sign-in

At your Chromebook, you can use preinstalled Chrome to login to Wekan.

For iOS and Android, you can [create app icon this way](https://github.com/wekan/wekan/wiki/PWA).

## 11) Optional: Change Linux desktop apps language and install Firefox

Here changing to Finnish:
```
sudo dpkg-reconfigure-locales
```
There add this language, and set is as default:
```
fi_FI.UTF8
```
And install Ubuntu 20.04 version Firefox and translation:
```
sudo apt install firefox firefox-locale-fi
```
Shutdown Ubuntu container:
```
sudo shutdown -h now
```
Reboot Chromebook by clicking desktop right bottom clock / Power icon. After Chromebook has shutdown, short press laptop power button to start Chromebook.

## 12) Optional: Install HP DeskJet 2600 multifunction printer/scanner

This inkjet printer was cheapest available, and does print excellent quality similar to laser color printer.

You should set your wireless network printer to have Static IP address.

[Source](https://chromeunboxed.com/how-to-use-your-hp-printer-with-linux-on-chrome-os/)
```
sudo apt install hplip hplip-gui cups system-config-printer
sudo xhost +
sudo hp-setup
```
Check:
```
[X] Network/Ethernet/Wireless newtork (direct connection or JetDirect)
```
Click:
```
> Show Advanced Options:
```
Check:
```
[X] Manual Discovery
IP Address or network name: [ YOUR-PRINTER-STATIC-IP-HERE, for example 192.168.0.200 ]
JetDirect port: [1]
```
Next, Next, Add Printer.
```
sudo system-config-printer
```
Set printer as Default.

You are also able to Scan images from your multifunction printer with XSane, that was installed with HP printer drivers.

You can print from Ubuntu Linux apps, like for example Firefox, LibreOffice, Inkscape, etc what you can install with apt.
