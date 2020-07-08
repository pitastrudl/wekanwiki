### Install for example from:
- [Snap](https://github.com/wekan/wekan/wiki/Snap)
- [Docker](https://github.com/wekan/wekan/wiki/Docker)

*Make sure you are running at least **v2.21***

### Snap install info, tested 2020-07-07

```
sudo snap set wekan debug='true'
sudo snap set wekan caddy-enabled='true'
sudo snap set wekan mail-from='Example Boards <joe@example.com>'
sudo snap set wekan mail-url='smtps://username:password@in-v3.mailjet.com:465/'
sudo snap set wekan oauth2-enabled='true'
sudo snap set wekan oauth2-request-permissions='openid'
sudo snap set wekan oauth2-client-id='AZURE-NEW-APP-CLIENT-ID'
sudo snap set wekan oauth2-secret='AZURE-NEW-APP-SECRET'
sudo snap set wekan oauth2-auth-endpoint='/oauth2/v2.0/authorize'
sudo snap set wekan oauth2-server-url='https://login.microsoftonline.com/TENANT-NAME-FOR-YOUR-ORGANIZATION'
sudo snap set wekan oauth2-token-endpoint='/oauth2/v2.0/token'
sudo snap set wekan oauth2-userinfo-endpoint='https://graph.microsoft.com/oidc/userinfo'
sudo snap set wekan oauth2-email-map='email'
sudo snap set wekan oauth2-username-map='email'
sudo snap set wekan oauth2-fullname-map='name'
sudo snap set wekan oauth2-id-map='email'
sudo snap set wekan port='3001'
sudo snap set wekan richer-card-comment-editor='false'
sudo snap set wekan root-url='https://boards.example.com'
sudo snap set wekan with-api='true'
```
At Admin Panel / Settings / Email:
- SMTP Host: `in-v3.mailjet.com`
- SMTP Port: `465`
- Username: `MAILJET-USERNAME`
- Password: `MAILJET-PASSWORD`
- TLS Support: `[_]` (not checked)

### There are two major steps for configuring Wekan to authenticate to Azure AD via OpenID Connect (OIDC)

1. Register the application with Azure. Make sure you capture the application ID as well as generate a secret key.
2. Configure the environment variables.  This differs slightly by installation type, but make sure you have the following:
* OAUTH2_ENABLED = true
* OAUTH2_CLIENT_ID = xxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx (application GUID captured during app registration)
* OAUTH2_SECRET = xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx (secret key generated during app registration)
* OAUTH2_SERVER_URL = https://login.microsoftonline.com/<tenant GUID specific to your organization>
* OAUTH2_AUTH_ENDPOINT = /oauth2/v2.0/authorize
* OAUTH2_USERINFO_ENDPOINT = https://graph.microsoft.com/oidc/userinfo
* OAUTH2_TOKEN_ENDPOINT = /oauth2/v2.0/token
* OAUTH2_ID_MAP = email (the claim name you want to map to the unique ID field)
* OAUTH2_USERNAME_MAP = email (the claim name you want to map to the username field)
* OAUTH2_FULLNAME_MAP = name (the claim name you want to map to the full name field)
* OAUTH2_EMAIL_MAP = email (the claim name you want to map to the email field)

I also recommend setting DEBUG = true until you have a working configuration.  It helps.

You may also find it useful to look at the following configuration information:
https://login.microsoftonline.com/**the-tenant-name-for-your-organization**/v2.0/.well-known/openid-configuration

Some Azure links also at wiki page about moving from Sandstorm to Docker/Snap , and using Docker Swarm:
- https://github.com/wekan/wekan/wiki/Export-from-Wekan-Sandstorm-grain-.zip-file#azure-links