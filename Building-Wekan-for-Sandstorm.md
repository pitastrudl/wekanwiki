## 1) Download Wekan VirtualBox image

[https://wekan.xet7.org](https://wekan.xet7.org)

## 2) After starting VirtualBox VM, stop Wekan

```
cd ~/repos
./stop.wekan.sh
```

Check did wekan stop really:

```
ps aux | grep 'node main.js'
```

You may need to kill it:

```
sudo kill -9 PID-NUMBER-HERE
```

(This process should be improved).

## 3) Install Sandstorm dev version

[Info source](https://sandstorm.io/install):

Start install:

```
curl https://install.sandstorm.io | bash
```

Use options for development / dev install.

## 3) Download meteor-spk packaging tool

[Info source](https://github.com/sandstorm-io/meteor-spk)

```
cd ~/repos
curl https://dl.sandstorm.io/meteor-spk-0.3.2.tar.xz | tar Jxf -
echo "export PATH=$PATH:~/repos/meteor-spk-0.3.2" >> ~/.bashrc
source ~/.bashrc
```