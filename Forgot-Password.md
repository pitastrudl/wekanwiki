## Forgot Password

1) Download [Robo 3T](https://robomongo.org) on your Linux or Mac computer. Or, using ssh shell to server, [login to MongoDB database using mongo cli](https://github.com/wekan/wekan/wiki/Backup#mongodb-shell-on-wekan-snap)

2) Make SSH tunnel to your server, from your local port 9000 (or any other) to server MongoDB port 27019:
```
ssh -L 9000:localhost:27019 user@example.com
```
3) Open Robo 3T, create new connection: Name, address: localhost : 9000 

a) If you don't have self-registration disabled, register new account at /sign-up, and make yourself admin in MongoDB database:

1) Use database that has wekan data, for example:
```
use wekan
```
2) Add Admin rights to some Wekan username:
```
db.users.update({username:'admin-username-here'},{$set:{isAdmin:true}})
```

b) If someone else remembers their password, and his/her login works, copy their bcrypt hashed password to your password using Robo 3T.

c) Install Wekan elsewhere, create new user, copy bcrypt hashed password to your password.

d) Backup, New install, Create User, Copy Password, Restore:

1. [Backup Snap](https://github.com/wekan/wekan-snap/wiki/Backup-and-restore)
2. stop wekan `sudo snap stop wekan.wekan`
3a. Empty database by droppping wekan database in Mongo 3T
3b. Empty database in [mongo cli](mongo cli](https://github.com/wekan/wekan/wiki/Backup#mongodb-shell-on-wekan-snap):
```
mongo --port 27019
```
Look what databases there are:
```
show dbs
```
Probably database is called wekan, so use it:
```
use wekan
```
Delete database:
```
db.dropDatabase()
```
4. Start wekan:
```
sudo snap stop wekan.wekan
```
5. Register at /sign-up
6. Copy bcrypt hashed password to text editor
7. [Restore your backup](https://github.com/wekan/wekan-snap/wiki/Backup-and-restore)
8. Change to database your new bcrypt password.

## Don't have Admin Rights to board

1. In Robo 3T, find where your ID that your username has:
```
db.getCollection('users').find({username: "YOUR-USERNAME-HERE"})
```
2. Find board where you are not admin, using user ID you found above:
```
db.getCollection('boards').find({members: {$elemMatch: { userId: "YOUR-USER-ID-HERE", isAdmin: false} } })
```
And set yourself as admin.