1) You can run Wekan on Docker locally like this on http://localhost:8080/
(or other port it you change 8080 in script):
```bash
docker run -d --restart=always --name wekan-db mongo:3.4

docker run -d --restart=always --name wekan --link "wekan-db:db" -e "MONGO_URL=mongodb://db" -e "ROOT_URL=http://localhost" -p 8080:80 mquandalle/wekan:0.10.0
```

Mongo 3.4 used because of bug in 3.4.1:

https://github.com/wefork/wekan/issues/58

2) List docker containers, your ID:s will be different:
```bash
docker ps
```
Result:
```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES
1234wekanid        mquandalle/wekan    "/bin/sh -c 'bash $ME"   About an hour ago   Up 46 minutes       0.0.0.0:8080->80/tcp   wekan
4321mongoid        mongo               "/entrypoint.sh mongo"   About an hour ago   Up 46 minutes       27017/tcp              wekan-db
```

3) Enter inside mongo container:
```bash
docker exec -it wekan-db bash
```

4) OPTIONAL: If you want to browse data inside container, you can use CLI commands like listed at

https://docs.mongodb.com/manual/reference/mongo-shell/

like this:

```bash
> mongo             
MongoDB shell version: 3.2.7
connecting to: test
Server has startup warnings: 
2016-06-25T11:39:55.913+0000 I CONTROL  [initandlisten] 
2016-06-25T11:39:55.913+0000 I CONTROL  [initandlisten] ** WARNING: /sys/kernel/mm/transparent_hugepage/enabled is 'always'.
2016-06-25T11:39:55.913+0000 I CONTROL  [initandlisten] **        We suggest setting it to 'never'
2016-06-25T11:39:55.913+0000 I CONTROL  [initandlisten] 
2016-06-25T11:39:55.913+0000 I CONTROL  [initandlisten] ** WARNING: /sys/kernel/mm/transparent_hugepage/defrag is 'always'.
2016-06-25T11:39:55.913+0000 I CONTROL  [initandlisten] **        We suggest setting it to 'never'
2016-06-25T11:39:55.913+0000 I CONTROL  [initandlisten] 
> show dbs
admin  0.034GB
local  0.000GB
> use admin
switched to db admin
> show collections
activities
boards
card_comments
cards
cfs._tempstore.chunks
cfs.attachments.filerecord
cfs_gridfs._tempstore.chunks
cfs_gridfs._tempstore.files
cfs_gridfs.attachments.chunks
cfs_gridfs.attachments.files
esCounts
lists
meteor-migrations
meteor_accounts_loginServiceConfiguration
presences
users
> exit
```

5) Go to /data directory:
```bash
cd /data
```

6) Backup database to files inside container to directory /data/dump, only Wekan database with name "admin" is included, not local:
```bash
mongodump
```

7) Exit from inside of container:
```bash
exit
```

8) Copy backup directory /data/dump from inside of container to current directory:
```bash
docker cp wekan-db:/data/dump .
```

9a) Restore backup later:
```bash
docker cp dump wekan-db:/data/
docker exec -it wekan-db bash
cd /data
mongorestore
exit
```

9b) Or restore to another mongo database, in different port:
```bash
mongorestore --port 11235
```

10) If you would like to browse mongo database that is outside of docker in GUI, you could try some admin interface:

https://docs.mongodb.com/ecosystem/tools/administration-interfaces/

11) If you sometime after backups want to remove wekan containers to reinstall them, do:
```bash
docker stop wekan wekan-db
docker rm wekan wekan-db
```
Then you can reinstall from step 1.

12) If latest version of Wekan Docker image is broken, here's how to run older version:

https://github.com/wekan/wekan/issues/659