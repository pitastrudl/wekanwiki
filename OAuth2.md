## Rocket.Chat can provide OAuth2 login to Wekan

## 1) Install Wekan

[Wekan Snap](https://github.com/wekan/wekan-snap/wiki/Install)
```
sudo snap install wekan
sudo snap set wekan root-url="https://wekan.example.com"
sudo snap set wekan port='3001'
sudo snap set core refresh.schedule=02:00-04:00
sudo snap set wekan mail-url='smtps://user:pass@mailserver.example.com:453'
sudo snap set wekan mail-from='Wekan Boards <support@example.com>'
sudo snap set with-api='true'
sudo snap set wekan oauth2-client-id='abcde12345'
sudo snap set wekan oauth2-secret='54321abcde'
sudo snap set oauth2-server-url='https://chat.example.com'
sudo snap set oauth2-auth-endpoint='/oauth/authorize'
sudo snap set oauth2-userinfo-endpoint='/oauth/userinfo'
sudo snap set oauth2-token-endpoint='/oauth/token'
```
Edit Caddyfile:
```
sudo nano /var/snap/wekan/common/Caddyfile
```
Add Caddy config:
```
wekan.example.com {
        proxy / localhost:3001 {
          websocket
          transparent
        }
}

chat.example.com {
        proxy / localhost:3000 {
          websocket
          transparent
        }
}
```