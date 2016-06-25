1) You can run Wekan on Docker locally like this on http://localhost:8080/
(or other port it you change 8080 in script):
```bash
docker run -d --name wekan-db mongo
docker run -d --link "wekan-db:db" -e "MONGO_URL=mongodb://db" \
   -e "ROOT_URL=http://localhost" -p 8080:80 mquandalle/wekan
```

2) List docker containers, your ID:s will be different:
```bash
docker ps
```
Result:
```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES
1234wekanid        mquandalle/wekan    "/bin/sh -c 'bash $ME"   About an hour ago   Up 46 minutes       0.0.0.0:8080->80/tcp   kickass_kirch
4321mongoid        mongo               "/entrypoint.sh mongo"   About an hour ago   Up 46 minutes       27017/tcp              wekan-db
```

3) Stop wekan container, so it does not make changes when running:
```bash
docker stop 1234wekanid
```

4) Enter inside mongo container:
```bash
docker exec -it 4321mongoid bash
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

6) Make directory for backups:
```bash
mkdir /data/backups
```

7) Backup database to files inside container, only Wekan database with name "admin" is included, not local:
```bash
mongodump --out /data/backup
```
8) Exit from inside of container:
```bash
exit
```

9) Copy backup directory from inside of container to directory /home/username/backup:
```bash
cd /home/username
docker cp 4321mongoid:/data/backup /home/username
```

10) Restore to another mongo database, for example in different port:
```bash
cd /home/username
mongorestore --port 11235 backup
```

11) After that start Wekan container again:
```bash
docker start 1234wekanid
```

12) If you would like to browse mongo database that is outside of docker in GUI, you could try some admin interface:

https://docs.mongodb.com/ecosystem/tools/administration-interfaces/
