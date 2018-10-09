## Retrieve cards by swimlane id

Please somebody add example by looking this:

[Issue](https://github.com/wekan/wekan/issues/1934) and [code](https://github.com/wekan/wekan/pull/1944/commits/be42b8d4cbdfa547ca019ab2dc9a590a115cc0e2). Also add to [Swimlanes page](https://github.com/wekan/wekan/wiki/REST-API-Swimlanes)

# Add Card to List-Board-Swimlane

| API URL / Code Link | Requires Admin Auth | HTTP Method |
| :--- | :--- | :--- |
| [/api/boards/:boardId/lists/:listId/cards](https://github.com/wekan/wekan/blob/c115046a7c86b30ab5deb8762d3ef7a5ea3f4f90/models/cards.js#L487) | `yes` | `POST` |

```shell
curl -H "Authorization: Bearer t7iYB86mXoLfP_XsMegxF41oKT7iiA9lDYiKVtXcctl" \
     -H "Content-type:application/json" \
     -X POST \
     http://localhost:3000/api/boards/YRgy7Ku6uLFv2pYwZ/lists/PgTuf6sFJsaxto5dC/cards \
     -d '{ "title": "Card title text", "description": "Card description text", "authorId": "The appropriate existing userId", "swimlaneId": "The destination swimlaneId" }'
```
## Result example
The new card's ID is returned in the format:
```json
{
    "_id": "W9m9YxQKT6zZrKzRW"
}
```

# Update a card
You can change (any of) the card's title, list, and description.

| API URL / Code Link | Requires Admin Auth | HTTP Method |
| :--- | :--- | :--- |
| [/api/boards/:boardId/lists/:fromListId/cards/:cardId](https://github.com/wekan/wekan/blob/c115046a7c86b30ab5deb8762d3ef7a5ea3f4f90/models/cards.js#L520) | `yes` | `PUT` |

```shell
curl -H "Authorization: Bearer t7iYB86mXoLfP_XsMegxF41oKT7iiA9lDYiKVtXcctl" \
     -H "Content-type:application/json" \
     -X PUT \
     http://localhost:3000/api/boards/YRgy7Ku6uLFv2pYwZ/lists/PgTuf6sFJsaxto5dC/cards/ssrNX9CvXvPxuC5DE \
     -d '{ "title": "New title text", "listId": "New destination listId", "description": "New description text" }'
```
## Result example
The card's ID is returned in the format:
```json
{
    "_id": "W9m9YxQKT6zZrKzRW"
}
```
# Delete a card

| API URL / Code Link | Requires Admin Auth | HTTP Method |
| :--- | :--- | :--- |
| [/api/boards/:boardId/lists/:listId/cards/:cardId](https://github.com/wekan/wekan/blob/c115046a7c86b30ab5deb8762d3ef7a5ea3f4f90/models/cards.js#L554) | `yes` | `DELETE` |

```shell
curl -H "Authorization: Bearer t7iYB86mXoLfP_XsMegxF41oKT7iiA9lDYiKVtXcctl" \
     -H "Content-type:application/json" \
     -X DELETE \
     http://localhost:3000/api/boards/YRgy7Ku6uLFv2pYwZ/lists/PgTuf6sFJsaxto5dC/cards/ssrNX9CvXvPxuC5DE \
     -d '{ "authorId": "the appropriate existing userId"}'
```
## Result example
The card's ID is returned in the format:
```json
{
    "_id": "W9m9YxQKT6zZrKzRW"
}
```

# In Wekan code

wekan/models/cards.js
```
  JsonRoutes.add('GET', '/api/boards/:boardId/lists/:listId/cards', function (req, res) {
    const paramBoardId = req.params.boardId;
    const paramListId = req.params.listId;
    Authentication.checkBoardAccess(req.userId, paramBoardId);
    JsonRoutes.sendResult(res, {
      code: 200,
      data: Cards.find({boardId: paramBoardId, listId: paramListId, archived: false}).map(function (doc) {
        return {
          _id: doc._id,
          title: doc.title,
          description: doc.description,
        };
      }),
    });
  });

  JsonRoutes.add('GET', '/api/boards/:boardId/lists/:listId/cards/:cardId', function (req, res) {
    const paramBoardId = req.params.boardId;
    const paramListId = req.params.listId;
    const paramCardId = req.params.cardId;
    Authentication.checkBoardAccess(req.userId, paramBoardId);
    JsonRoutes.sendResult(res, {
      code: 200,
      data: Cards.findOne({_id: paramCardId, listId: paramListId, boardId: paramBoardId, archived: false}),
    });
  });

  JsonRoutes.add('POST', '/api/boards/:boardId/lists/:listId/cards', function (req, res) {
    Authentication.checkUserId(req.userId);
    const paramBoardId = req.params.boardId;
    const paramListId = req.params.listId;
    const check = Users.findOne({_id: req.body.authorId});
    const members = req.body.members || [req.body.authorId];
    if (typeof  check !== 'undefined') {
      const id = Cards.direct.insert({
        title: req.body.title,
        boardId: paramBoardId,
        listId: paramListId,
        description: req.body.description,
        userId: req.body.authorId,
        swimlaneId: req.body.swimlaneId,
        sort: 0,
        members,
      });
      JsonRoutes.sendResult(res, {
        code: 200,
        data: {
          _id: id,
        },
      });

      const card = Cards.findOne({_id:id});
      cardCreation(req.body.authorId, card);

    } else {
      JsonRoutes.sendResult(res, {
        code: 401,
      });
    }
  });

  JsonRoutes.add('PUT', '/api/boards/:boardId/lists/:listId/cards/:cardId', function (req, res) {
    Authentication.checkUserId(req.userId);
    const paramBoardId = req.params.boardId;
    const paramCardId = req.params.cardId;
    const paramListId = req.params.listId;

    if (req.body.hasOwnProperty('title')) {
      const newTitle = req.body.title;
      Cards.direct.update({_id: paramCardId, listId: paramListId, boardId: paramBoardId, archived: false},
        {$set: {title: newTitle}});
    }
    if (req.body.hasOwnProperty('listId')) {
      const newParamListId = req.body.listId;
      Cards.direct.update({_id: paramCardId, listId: paramListId, boardId: paramBoardId, archived: false},
        {$set: {listId: newParamListId}});

      const card = Cards.findOne({_id: paramCardId} );
      cardMove(req.body.authorId, card, {fieldName: 'listId'}, paramListId);

    }
    if (req.body.hasOwnProperty('description')) {
      const newDescription = req.body.description;
      Cards.direct.update({_id: paramCardId, listId: paramListId, boardId: paramBoardId, archived: false},
        {$set: {description: newDescription}});
    }
    if (req.body.hasOwnProperty('labelIds')) {
      const newlabelIds = req.body.labelIds;
      Cards.direct.update({_id: paramCardId, listId: paramListId, boardId: paramBoardId, archived: false},
        {$set: {labelIds: newlabelIds}});
    }
    if (req.body.hasOwnProperty('requestedBy')) {
      const newrequestedBy = req.body.requestedBy;
      Cards.direct.update({_id: paramCardId, listId: paramListId, boardId: paramBoardId, archived: false},
        {$set: {requestedBy: newrequestedBy}});
    }
    if (req.body.hasOwnProperty('assignedBy')) {
      const newassignedBy = req.body.assignedBy;
      Cards.direct.update({_id: paramCardId, listId: paramListId, boardId: paramBoardId, archived: false},
        {$set: {assignedBy: newassignedBy}});
    }
    if (req.body.hasOwnProperty('receivedAt')) {
      const newreceivedAt = req.body.receivedAt;
      Cards.direct.update({_id: paramCardId, listId: paramListId, boardId: paramBoardId, archived: false},
        {$set: {receivedAt: newreceivedAt}});
    }
    if (req.body.hasOwnProperty('startAt')) {
      const newstartAt = req.body.startAt;
      Cards.direct.update({_id: paramCardId, listId: paramListId, boardId: paramBoardId, archived: false},
        {$set: {startAt: newstartAt}});
    }
    if (req.body.hasOwnProperty('dueAt')) {
      const newdueAt = req.body.dueAt;
      Cards.direct.update({_id: paramCardId, listId: paramListId, boardId: paramBoardId, archived: false},
        {$set: {dueAt: newdueAt}});
    }
    if (req.body.hasOwnProperty('endAt')) {
      const newendAt = req.body.endAt;
      Cards.direct.update({_id: paramCardId, listId: paramListId, boardId: paramBoardId, archived: false},
        {$set: {endAt: newendAt}});
    }
    if (req.body.hasOwnProperty('spentTime')) {
      const newspentTime = req.body.spentTime;
      Cards.direct.update({_id: paramCardId, listId: paramListId, boardId: paramBoardId, archived: false},
        {$set: {spentTime: newspentTime}});
    }
    if (req.body.hasOwnProperty('isOverTime')) {
      const newisOverTime = req.body.isOverTime;
      Cards.direct.update({_id: paramCardId, listId: paramListId, boardId: paramBoardId, archived: false},
        {$set: {isOverTime: newisOverTime}});
    }
    if (req.body.hasOwnProperty('customFields')) {
      const newcustomFields = req.body.customFields;
      Cards.direct.update({_id: paramCardId, listId: paramListId, boardId: paramBoardId, archived: false},
        {$set: {customFields: newcustomFields}});
    }
    JsonRoutes.sendResult(res, {
      code: 200,
      data: {
        _id: paramCardId,
      },
    });
  });


  JsonRoutes.add('DELETE', '/api/boards/:boardId/lists/:listId/cards/:cardId', function (req, res) {
    Authentication.checkUserId(req.userId);
    const paramBoardId = req.params.boardId;
    const paramListId = req.params.listId;
    const paramCardId = req.params.cardId;

    Cards.direct.remove({_id: paramCardId, listId: paramListId, boardId: paramBoardId});
    const card = Cards.find({_id: paramCardId} );
    cardRemover(req.body.authorId, card);
    JsonRoutes.sendResult(res, {
      code: 200,
      data: {
        _id: paramCardId,
      },
    });
```