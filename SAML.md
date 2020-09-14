[SAML Issue](https://github.com/wekan/wekan/issues/708)

Currently has code from https://github.com/steffow/meteor-accounts-saml/ copied to `wekan/packages/meteor-accounts-saml`

Does not yet have [fixes from RocketChat SAML](https://github.com/RocketChat/Rocket.Chat/tree/develop/app/meteor-accounts-saml)

Please add pull requests if it does not work.

Wekan clientside code is at `wekan/client/components/main/layouts.*`

Wekan serverside code is at:
- `wekan/server/authentication.js` at bottom
- `wekan/packages/meteor-accounts-saml/*`