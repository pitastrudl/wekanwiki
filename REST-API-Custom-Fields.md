## In Wekan code

wekan/models/customFields.js , at bottom

```
//CUSTOM FIELD REST API
if (Meteor.isServer) {
  JsonRoutes.add('GET', '/api/boards/:boardId/custom-fields', function (req, res) {
    Authentication.checkUserId( req.userId);
    const paramBoardId = req.params.boardId;
    JsonRoutes.sendResult(res, {
      code: 200,
      data: CustomFields.find({ boardId: paramBoardId }),
    });
  });

  JsonRoutes.add('GET', '/api/boards/:boardId/custom-fields/:customFieldId', function (req, res) {
    Authentication.checkUserId( req.userId);
    const paramBoardId = req.params.boardId;
    const paramCustomFieldId = req.params.customFieldId;
    JsonRoutes.sendResult(res, {
      code: 200,
      data: CustomFields.findOne({ _id: paramCustomFieldId, boardId: paramBoardId }),
    });
  });

  JsonRoutes.add('POST', '/api/boards/:boardId/custom-fields', function (req, res) {
    Authentication.checkUserId( req.userId);
    const paramBoardId = req.params.boardId;
    const id = CustomFields.direct.insert({
      name: req.body.name,
      type: req.body.type,
      settings: req.body.settings,
      showOnCard: req.body.showOnCard,
      boardId: paramBoardId,
    });

    const customField = CustomFields.findOne({_id: id, boardId: paramBoardId });
    customFieldCreation(req.body.authorId, customField);

    JsonRoutes.sendResult(res, {
      code: 200,
      data: {
        _id: id,
      },
    });
  });

  JsonRoutes.add('DELETE', '/api/boards/:boardId/custom-fields/:customFieldId', function (req, res) {
    Authentication.checkUserId( req.userId);
    const paramBoardId = req.params.boardId;
    const id = req.params.customFieldId;
    CustomFields.remove({ _id: id, boardId: paramBoardId });
    JsonRoutes.sendResult(res, {
      code: 200,
      data: {
        _id: id,
      },
    });
  });
}
```