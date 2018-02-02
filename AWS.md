1) Add AWS Security Group with for example name wekan, and incoming ports 80 and 443 for all. Only add ssh access to your own IP address CIDR like 123.123.123.123/32 so it means one IP address. 

2) Start Ubuntu 17.10 64bit EC2 instance that has at least 2 GB RAM, 30 GB diskspace, probably you need more when you add more customers. Add your SSH public key to instance or let it create new.

3) Add new Elastic IP address pointing to your EC2 instance. That way IP address stays same, and you can also make snapshot of EC2 instance and start that as new EC2 instance with more RAM and change Elastic IP to point to new EC2 instance with minimal downtime, but prefer times when there is no active changes to Wekan.

4) Set your subdomain.yourdomain.com address DNS pointing to your Elastic IP address as A record in Route 53, Namecheap or elsewhere where your domain control panel is. It will take max 24h for DNS to propagate globally.

5) ssh to your server, for example:

```
ssh -i pubkey.pem ubuntu@server-ip-address 

(or: root@)
```

6) Update all packages:

```
sudo apt update
sudo apt -y dist-upgrade
reboot
```

7) Install Docker CE and docker-compose for ubuntu from www.docker.com , also add user ubuntu to group docker in post-install step.

8) Install nginx, for example:

```
sudo apt install nginx

(or: nginx-full)
```

Example nginx config at:
https://github.com/wekan/wekan/wiki/Nginx-Webserver-Config

Test nginx config with:

```
sudo nginx -t
```

And take config into use with:

```
sudo systemctl reload nginx
```

9) Install certbot from https://certbot.eff.org for Let's Encrypt SSL certs, redirect http to https

10) For different customers, you use different location /customer1 2 etc block and wekan running behind nginx proxy on different localhost port in same nginx virtualhost subdomain config file.

11) Get latest wekan release info from https://github.com/wekan/wekan/releases ,  read docker-compose.yml file from https://github.com/wekan/wekan-mongodb where all settings are explained, so you setup ROOT_URL=https://sub.yourdomain.com/customer1 and for example the 8080:80 for local server port 8080 to go inside docker port 80. 

For example Wekan v0.70, use in docker-compose.yml file:
image: quay.io/wekan/wekan:v0.70
Only use release version tags, because latest tag can be broken sometimes.

12) For email, in AWS SES add email address to domain, verify SPF and DKIM with Route53 wizard if you have domain at Route53 as I recommend. At SES create new SMTP credentials and add them to docker-compose.yml SMTP settings, see 

13) Start wekan and mongodb database containers with command:

```
docker-compose up -d
```

So it goes nginx SSL port 443 => proxy to localhost port 8080 or any other => wekan-app port 80 inside docker

14) For different customers have different docker-compose.yml script in directories named by customer names. You may need to rename docker containers from wekan-app to wekan-customer1 etc, and probably also docker internal network names.

15) Backup, restore, and moving data outside/inside docker https://github.com/wekan/wekan/wiki/Export-Docker-Mongo-Data