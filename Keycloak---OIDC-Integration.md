Environment Variables that need to be set in your Wekan container:

OAUTH2_ENABLE = TRUE
OAUTH2_CLIENT_ID = <Keycloak create Client ID>
OAUTH2_SERVER_URL = <Keycloak server name>/auth
OAUTH2_AUTH_ENDPOINT = /realms/<keycloak realm>/protocol/openid-connect/auth
OAUTH2_USERINFO_ENDPOINT = /realms/<keycloak realm>/protocol/openid-connect/userinfo
OAUTH2_TOKEN_ENDPOINT = /realms/<keycloak realm>/protocol/openid-connect/token
OAUTH2_SECRET = <keycloak client secret>
** When creating a Client in keycloak, ensure the access type is confidential.  After clicking save, you will have a Credentials tab.  You can retrieve the secret from that location.

Under the Client area in Keycloak, click on the Mappers area and "create" the following:
 
