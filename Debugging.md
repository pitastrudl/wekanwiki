## Finding memory leaks

[How to Self Detect a Memory Leak in Node](https://www.nearform.com/blog/self-detect-memory-leak-node/)

## 100% CPU usage

1) Increase ulimit system wide to 100 000 in systemd config.

2) Wekan Javascript code has [Node 100% CPU fixes included](https://github.com/wekan/wekan/blob/devel/CHANGELOG.md#v084-2018-04-16-wekan-release). Also read [on-going 100% CPU usage issue progress](https://github.com/meteor/meteor/issues/9796).

3) Newest Wekan includes fixed Node.js binary. Use Fibers fixed [node source from Sandstorm](https://github.com/sandstorm-io/node/commits/sandstorm) or binary [copied from Sandstorm](https://github.com/wekan/wekan-mongodb/issues/2#issuecomment-381453161) or downloaded as node binary or tar.gz package from https://releases.wekan.team , related fixes are in Wekan GitHub repo [Dockerfile](https://github.com/wekan/wekan/blob/devel/Dockerfile), [snapcraft.yaml](https://github.com/wekan/wekan/blob/devel/snapcraft.yaml) and [wekan/server/authentication.js](https://github.com/wekan/wekan/blob/devel/server/authentication.js). 

## Scaling to thousands of users

[Production setup at AWS](https://github.com/wekan/wekan/wiki/AWS)
