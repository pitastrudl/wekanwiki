[Thanks to @mlazzje for this info below](https://github.com/wekan/wekan/issues/2527#issuecomment-654155289)

To create Google OAuth 2 credentials, you can follow this tutorial: https://developers.google.com/identity/sign-in/web/sign-in

Then replace `CLIENT_ID` and `CLIENT_SECRET` below.

In your wekan config, you have to set the following information in snap:
```
snap set wekan oauth2-enabled='true'
snap set wekan oauth2-client-id='CLIENT_ID'
snap set wekan oauth2-secret='CLIENT_SECRET'
snap set wekan oauth2-auth-endpoint='https://accounts.google.com/o/oauth2/v2/auth'
snap set wekan oauth2-token-endpoint='https://oauth2.googleapis.com/token'
snap set wekan oauth2-userinfo-endpoint='https://openidconnect.googleapis.com/v1/userinfo'
snap set wekan oauth2-id-map='sub'
snap set wekan oauth2-email-map='email'
snap set wekan oauth2-username-map='nickname'
snap set wekan oauth2-fullname-map='name'
snap set wekan oauth2-request-permissions='openid https://www.googleapis.com/auth/userinfo.profile https://www.googleapis.com/auth/userinfo.email'
```