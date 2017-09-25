Suppose you deploy rocketchat behind a reverse proxy on https with a Let's Encrypt certificate. If you want to send wekan notifications to rocketchat, you may have a certificate problem: Let's Encrypt's CA is not recognized.

* Download the Let’s Encrypt Authority X3 (IdenTrust cross-signed) from [here](https://letsencrypt.org/certificates/)
```sh
cd /etc/ssl/certs
wget https://letsencrypt.org/certs/lets-encrypt-x3-cross-signed.pem.txt -O lets-encrypt-x3-cross-signed.pem
```

* Now start the application with 
```sh
NODE_EXTRA_CA_CERTS=/etc/ssl/certs/lets-encrypt-x3-cross-signed.pem node main.js
```