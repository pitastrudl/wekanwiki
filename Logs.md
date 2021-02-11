Logs are at /var/log/syslog , like with:
```
sudo tail -f 1000 /var/log/syslog | less
```

Or:

## Snap
All:
```
sudo snap logs wekan
```
Partial:
```
sudo snap logs wekan.wekan

sudo snap logs wekan.mongodb

sudo snap logs wekan.caddy
```
## Docker

```
docker logs wekan-app

docker logs wekan-db
```
## Sandstorm

When Wekan grain is open, click at top terminal icon, so then opens new window that shows logs

## Additional logs

- https://github.com/wekan/wekan-logstash
- https://github.com/wekan/wekan-stats
- Boards count https://github.com/wekan/wekan/pull/3556
- At this wiki right menu, also look at Webhooks topic
- https://github.com/wekan/wekan/wiki/Features#Stats
- https://github.com/wekan/wekan/issues/1001
