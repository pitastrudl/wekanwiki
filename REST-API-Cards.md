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