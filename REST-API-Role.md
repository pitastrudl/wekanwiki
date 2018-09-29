# User Role on Board

## Admin
```
curl -H "Authorization: Bearer a6DM_gOPRwBdynfXaGBaiiEwTiAuigR_Fj_81QmNpnf" \
     -H "Content-type:application/json" \
     -X POST \
     http://localhost:3000/api/boards/BOARD-ID-HERE/members/USER-ID-HERE \
     -d '{"isAdmin": "true", "isNoComments":"false", "isCommentOnly": "false"}'
```
## Normal
```
curl -H "Authorization: Bearer a6DM_gOPRwBdynfXaGBaiiEwTiAuigR_Fj_81QmNpnf" \
     -H "Content-type:application/json" \
     -X POST \
     http://localhost:3000/api/boards/BOARD-ID-HERE/members/USER-ID-HERE \
     -d '{"isAdmin": "false", "isNoComments":"false", "isCommentOnly": "false"}'
```
## No Comments
```
curl -H "Authorization: Bearer a6DM_gOPRwBdynfXaGBaiiEwTiAuigR_Fj_81QmNpnf" \
     -H "Content-type:application/json" \
     -X POST \
     http://localhost:3000/api/boards/BOARD-ID-HERE/members/USER-ID-HERE \
     -d '{"isAdmin": "false", "isNoComments":"true", "isCommentOnly": "false"}'
```
## Comment Only
```
curl -H "Authorization: Bearer a6DM_gOPRwBdynfXaGBaiiEwTiAuigR_Fj_81QmNpnf" \
     -H "Content-type:application/json" \
     -X POST \
     http://localhost:3000/api/boards/BOARD-ID-HERE/members/USER-ID-HERE \
     -d '{"isAdmin": "false", "isNoComments":"false", "isCommentOnly": "true"}'
```
