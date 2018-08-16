## Standalone Wekan: Snap, (Docker, Source, VirtualBox)

1) [Install Wekan Snap](https://github.com/wekan/wekan-snap/wiki/Install)

2) Go to your Wekan URL like https://example.com/sign-up (your address + /sign-up)

3) Register your username, email address and password. First registered user will be admin, and next ones normal users. If you want other admins too, you can change their permission to admin at Admin Panel.

4) If you get some error about email settings, you can ignore it. Wekan works also without setting up email.

If you really want email sending, do for example:
```
sudo snap set wekan mail-url='smtps://user:pass@mailserver.example.com:457/'
sudo snap set wekan mail-from='Example Wekan Support <support@example.com>'
```
For more options see [Troubleshooting Email](https://github.com/wekan/wekan/wiki/Troubleshooting-Mail)

5) Login to Wekan at https://example.com/sign-in (your address + /sign-in)

6) Click on top right your username / Admin Panel. You can change permissions, name, email address and password in Admin Panel.

![Admin Panel](https://wekan.github.io/wekan-admin-panel.png)

7) For registering other users:

a) Let them self-register, or open webbrowser incongnito window, and register them at https://example.com/sign-up (your address + /sign-up)

b) If your email works, click Admin Panel / Settings / Registration / [X] Disable self-registration. Then invite new users to selected boards by email address.

## Forgot your Wekan password?

1) Download [Robo 3T](https://robomongo.org) on your Linux or Mac computer. Or, using ssh shell to server, [login to MongoDB database using mongo cli](https://github.com/wekan/wekan/wiki/Backup#mongodb-shell-on-wekan-snap)

2) Make SSH tunnel to your server, from your local port 9000 (or any other) to server MongoDB port 27019:
```
ssh -L 9000:localhost:27019 user@example.com
```
3) Open Robo 3T, create new connection: Name, address: localhost : 9000 

a) If you don't have self-registration disabled, register new account at /sign-up, and [make yourself admin in MongoDB database](https://github.com/wekan/wekan/blob/devel/CHANGELOG.md#v0111-rc2-2017-03-05-wekan-prerelease).

b) If someone else remembers their password, and his/her login works, copy their bcrypt hashed password to your password using Robo 3T.

c) Install Wekan elsewhere, create new user, copy bcrypt hashed password to your password.

d) Backup, New install, Create User, Copy Password, Restore:

1. [Backup Snap](https://github.com/wekan/wekan-snap/wiki/Backup-and-restore)
2. stop wekan `sudo snap stop wekan.wekan`
3a. Empty database by droppping wekan database in Mongo 3T
3b. Empty database in [mongo cli](mongo cli](https://github.com/wekan/wekan/wiki/Backup#mongodb-shell-on-wekan-snap):
```
mongo --port 27019
# look what databases there are
show dbs
# probably database is called wekan, so use it
use wekan
# delete database
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

