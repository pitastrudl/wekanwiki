## Newest on edge

[Newest API additions are available only on edge](https://github.com/wekan/wekan-snap/wiki/Snap-Developer-Docs)

## Information about boards of user
```
curl -H "Authorization: Bearer a6DM_gOPRwBdynfXaGBaiiEwTiAuigR_Fj_81QmNpnf" \
      http://localhost:3000/api/users/XQMZgynx9M79qTtQc/boards
```

## Change role of user on board

[Change Role: admin/normal/nocomments/commentonly](https://github.com/wekan/wekan/wiki/REST-API-Role)

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
- "isAdmin":"true"
- "isActive":"true"
- "isNoComments":"false"
- "isCommentOnly":"false"
- "permission":"private"   <== Set to "public" if you want public Wekan board
- "color":"belize"        <== Board color: belize, nephritis, pomegranate, pumpkin, wisteria, midnight.

<img src="https://wekan.github.io/board-colors.png" width="40%" alt="Wekan logo" />

Example:
```
curl  -H "Authorization: Bearer t7iYB86mXoLfP_XsMegxF41oKT7iiA9lDYiKVtXcctl" \
      -H "Content-type:application/json" \
      -X POST \
      http://localhost:3000/api/boards \
      -d '{"title":"Board title here","owner":"ABCDE12345","permission":"private","color":"nephritis"}'
```

## In Wekan code

wekan/models/boards.js
```
  JsonRoutes.add('GET', '/api/users/:userId/boards', function (req, res) {
    try {
      Authentication.checkLoggedIn(req.userId);
      const paramUserId = req.params.userId;
      // A normal user should be able to see their own boards,
      // admins can access boards of any user
      Authentication.checkAdminOrCondition(req.userId, req.userId === paramUserId);

      const data = Boards.find({
        archived: false,
        'members.userId': paramUserId,
      }, {
        sort: ['title'],
      }).map(function(board) {
        return {
          _id: board._id,
          title: board.title,
        };
      });

      JsonRoutes.sendResult(res, {code: 200, data});
    }
    catch (error) {
      JsonRoutes.sendResult(res, {
        code: 200,
        data: error,
      });
    }
  });

  JsonRoutes.add('GET', '/api/boards', function (req, res) {
    try {
      Authentication.checkUserId(req.userId);
      JsonRoutes.sendResult(res, {
        code: 200,
        data: Boards.find({ permission: 'public' }).map(function (doc) {
          return {
            _id: doc._id,
            title: doc.title,
          };
        }),
      });
    }
    catch (error) {
      JsonRoutes.sendResult(res, {
        code: 200,
        data: error,
      });
    }
  });

  JsonRoutes.add('GET', '/api/boards/:id', function (req, res) {
    try {
      const id = req.params.id;
      Authentication.checkBoardAccess(req.userId, id);

      JsonRoutes.sendResult(res, {
        code: 200,
        data: Boards.findOne({ _id: id }),
      });
    }
    catch (error) {
      JsonRoutes.sendResult(res, {
        code: 200,
        data: error,
      });
    }
  });

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
      const swimlaneId = Swimlanes.insert({
        title: TAPi18n.__('default'),
        boardId: id,
      });
      JsonRoutes.sendResult(res, {
        code: 200,
        data: {
          _id: id,
          defaultSwimlaneId: swimlaneId,
        },
      });
    }
    catch (error) {
      JsonRoutes.sendResult(res, {
        code: 200,
        data: error,
      });
    }
  });

  JsonRoutes.add('DELETE', '/api/boards/:id', function (req, res) {
    try {
      Authentication.checkUserId(req.userId);
      const id = req.params.id;
      Boards.remove({ _id: id });
      JsonRoutes.sendResult(res, {
        code: 200,
        data:{
          _id: id,
        },
      });
    }
    catch (error) {
      JsonRoutes.sendResult(res, {
        code: 200,
        data: error,
      });
    }
  });

  JsonRoutes.add('PUT', '/api/boards/:id/labels', function (req, res) {
    Authentication.checkUserId(req.userId);
    const id = req.params.id;
    try {
      if (req.body.hasOwnProperty('label')) {
        const board = Boards.findOne({ _id: id });
        const color = req.body.label.color;
        const name = req.body.label.name;
        const labelId = Random.id(6);
        if (!board.getLabel(name, color)) {
          Boards.direct.update({ _id: id }, { $push: { labels: { _id: labelId,  name,  color } } });
          JsonRoutes.sendResult(res, {
            code: 200,
            data: labelId,
          });
        } else {
          JsonRoutes.sendResult(res, {
            code: 200,
          });
        }
      }
    }
    catch (error) {
      JsonRoutes.sendResult(res, {
        data: error,
      });
    }
  });
```