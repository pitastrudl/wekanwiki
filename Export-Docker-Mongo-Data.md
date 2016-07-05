1) You can run Wekan on Docker locally like this on http://localhost:8080/
(or other port it you change 8080 in script), 2 docker commands o:
```bash
docker run -d --restart=always --name wekan-db mongo

docker run -d --restart=always --name wekan --link "wekan-db:db" -e "MONGO_URL=mongodb://db" -e "ROOT_URL=http://localhost" -p 8080:80 mquandalle/wekan
```

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

3) Stop wekan container, so it does not make changes when running:
```bash
docker stop wekan
```

4) Enter inside mongo container:
```bash
docker exec -it wekan-db bash
```

5) OPTIONAL: If you want to browse data inside container, you can use CLI commands like listed at

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

6) Go to /data directory:
```bash
cd /data
```

7) Backup database to files inside container to directory /data/dump, only Wekan database with name "admin" is included, not local:
```bash
mongodump
```

8) Exit from inside of container:
```bash
exit
```

9) Copy backup directory /data/dump from inside of container to current directory:
```bash
docker cp wekan-db:/data/dump .
```

10) Restore to another mongo database, for example in different port:
```bash
mongorestore --port 11235
```

11) After that start Wekan container again:
```bash
docker start wekan
```

12) If you would like to browse mongo database that is outside of docker in GUI, you could try some admin interface:

https://docs.mongodb.com/ecosystem/tools/administration-interfaces/
