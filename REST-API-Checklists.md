## In Wekan code

### Checklist Items

wekan/models/checklistItems.js at bottom:

```
JsonRoutes.add('GET', '/api/boards/:boardId/cards/:cardId/checklists/:checklistId/items/:itemId', function (req, res) {
    Authentication.checkUserId( req.userId);
    const paramItemId = req.params.itemId;
    const checklistItem = ChecklistItems.findOne({ _id: paramItemId });
    if (checklistItem) {
      JsonRoutes.sendResult(res, {
        code: 200,
        data: checklistItem,
      });
    } else {
      JsonRoutes.sendResult(res, {
        code: 500,
      });
    }
  });

  JsonRoutes.add('PUT', '/api/boards/:boardId/cards/:cardId/checklists/:checklistId/items/:itemId', function (req, res) {
    Authentication.checkUserId( req.userId);

    const paramItemId = req.params.itemId;

    if (req.body.hasOwnProperty('isFinished')) {
      ChecklistItems.direct.update({_id: paramItemId}, {$set: {isFinished: req.body.isFinished}});
    }
    if (req.body.hasOwnProperty('title')) {
      ChecklistItems.direct.update({_id: paramItemId}, {$set: {title: req.body.title}});
    }

    JsonRoutes.sendResult(res, {
      code: 200,
      data: {
        _id: paramItemId,
      },
    });
  });

  JsonRoutes.add('DELETE', '/api/boards/:boardId/cards/:cardId/checklists/:checklistId/items/:itemId', function (req, res) {
    Authentication.checkUserId( req.userId);
    const paramItemId = req.params.itemId;
    ChecklistItems.direct.remove({ _id: paramItemId });
    JsonRoutes.sendResult(res, {
      code: 200,
      data: {
        _id: paramItemId,
      },
    });
```
