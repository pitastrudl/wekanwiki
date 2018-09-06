## Information about boards of user
```
curl -H "Authorization: Bearer a6DM_gOPRwBdynfXaGBaiiEwTiAuigR_Fj_81QmNpnf" \
      http://localhost:3000/api/users/XQMZgynx9M79qTtQc/boards
```

## The admin takes the ownership of ALL boards of the user (archived and not archived) where the user is admin on.

| URL | Requires Admin Auth | HTTP Method |
| :--- | :--- | :--- |
| `/api/users/:id` | `yes` | `PUT` |

```shell
curl -H "Authorization: Bearer t7iYB86mXoLfP_XsMegxF41oKT7iiA9lDYiKVtXcctl" \
     -H "Content-type:application/json" \
     -X PUT \
     http://localhost:3000/api/users/ztKvBTzCqmyJ77on8 \
     -d '{ "action": "takeOwnership" }'
```

## Create board

Required:
- "title":"Board title here"
- "owner":"ABCDE12345"   <= User ID in Wekan. Not username or email.

Optional, and defaults:
- "isAdmin": "true"
- "isActive": "true"
- "isNoComments": "false"
- "isCommentOnly": "false"
- "permission": "private"   <== Set to "public" if you want public Wekan board
- "color": "belize"        <== Board color: belize, nephritis, pomegranate, pumpkin, wisteria, midnight.

<img src="https://wekan.github.io/board-colors.png" width="40%" alt="Wekan logo" />

Example:
```
curl  -H "Authorization: Bearer t7iYB86mXoLfP_XsMegxF41oKT7iiA9lDYiKVtXcctl" \
      -H "Content-type:application/json" \
      -X POST \
      http://localhost:3000/api/boards \
      -d '{"title":"Board title here","owner":"ABCDE12345","permission":"private","color":"nephritis"}'
```

## How REST API is implemented in Wekan code

wekan/models/boards.js
```
  JsonRoutes.add('POST', '/api/boards', function (req, res) {
    try {
      Authentication.checkUserId(req.userId);
      const id = Boards.insert({
        title: req.body.title,
        members: [
          {
            userId: req.body.owner,
            isAdmin: req.body.isAdmin || true,
            isActive: req.body.isActive || true,
            isNoComments: req.body.isNoComments || false,
            isCommentOnly: req.body.isCommentOnly || false,
          },
        ],
        permission: req.body.permission || 'private',
        color: req.body.color || 'belize',
      });
```