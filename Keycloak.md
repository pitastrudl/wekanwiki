## OIDC Integration

[Outstanding Bug](https://github.com/wekan/wekan/issues/1874#issuecomment-460802250): Create the first user (admin) with the regular process.  Then the remaining users can use the Register with OIDC process.

Environment Variables that need to be set in your Wekan environment:

* OAUTH2_ENABLE = TRUE
* OAUTH2_CLIENT_ID = `<Keycloak create Client ID>`
* OAUTH2_SERVER_URL = `<Keycloak server name>/auth`
* OAUTH2_AUTH_ENDPOINT = `/realms/<keycloak realm>/protocol/openid-connect/auth`
* OAUTH2_USERINFO_ENDPOINT = `/realms/<keycloak realm>/protocol/openid-connect/userinfo`
* OAUTH2_TOKEN_ENDPOINT = `/realms/<keycloak realm>/protocol/openid-connect/token`
* OAUTH2_SECRET = `<keycloak client secret>`
> When creating a Client in keycloak, ensure the access type is confidential under the settings tab.  After clicking save, you will have a Credentials tab.  You can retrieve the secret from that location.

Under the Client area in Keycloak, click on the Mappers area and "create" the two following mappers:

1. displayName  
* Name: displayName
* Consent Required: Off
* Mapper Type: User Attribute
* User Attribute: displayName
* Token Claim Name: displayName
* Claim JSON Type: String
* Add to ID token: on
* Add to access token : on
* Add to userinfo : on
* Multivalued: off

2. id  
* Name: id
* Consent Required: Off
* Mapper Type: User Property
* User Attribute: username
* Token Claim Name: id
* Claim JSON Type: String
* Add to ID token: on
* Add to access token : on
* Add to userinfo : on

Then Edit the existing username mapper and update the following:  
* Token Claim Name: uid

