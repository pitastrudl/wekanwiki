## Install

On [Ubuntu Core KVM Download page](https://ubuntu.com/download/kvm) local VM:

```
ssh -p 8022 username@localhost

snap install wekan

snap set wekan root-url='http://localhost:8090'

snap set wekan port='80'
```
Then Wekan is visible at http://localhost:8090

[Adding users](https://github.com/wekan/wekan/wiki/Adding-users)

For more info, see [Snap Install page](https://github.com/wekan/wekan-snap/wiki/Install)