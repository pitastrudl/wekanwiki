# Webhook data

When a webhook is activated it sends the related information within the POST request body.

## Card creation

```
{
  text: '{{wekan-username}} added "{{card-title}}" to "{{list-name}}"\nhttp://{{wekan-host}}/b/{{board-id}}/{{board-name}}/{{card-id}}',
  cardId: '{{card-id}}',
  listId: '{{list-id}}',
  boardId: '{{board-id}}',
  user: '{{wekan-username}}',
  card: '{{card-title}}',
  description: 'act-createCard'
}
```

## Card archival

```
{
  text: '{{wekan-username}} archived "{{card-title}}"\nhttp://{{wekan-host}}/b/{{board-id}}/{{board-name}}/{{card-id}}',
  cardId: '{{card-id}}',
  listId: '{{list-id}}',
  boardId: '{{board-id}}',
  user: '{{wekan-username}}',
  card: '{{card-title}}',
  description: 'act-archivedCard'
}
```

## Comment creation

```
{
  text: '{{wekan-username}} commented on "{{card-title}}": "{{comment-body}}"\nhttp://{{wekan-host}}/b/{{board-id}}/{{board-name}}/{{card-id}}',
  cardId: '{{card-id}}',
  boardId: '{{board-id}}',
  comment: '{{comment-body}}',
  user: '{{wekan-username}}',
  card: '{{card-title}}',
  description: 'act-addComment'
}
```

## Card move

```
{
  text: '{{wekan-username}} moved "{{card-title}}" from "{{old-list-name}}" to "{{new-list-name}}"\nhttp://{{wekan-host}}/b/{{board-id}}/{{board-name}}/{{card-id}}',
  cardId: '{{card-id}}',
  listId: '{{new-list-id}}',
  oldListId: '{{old-list-id}}',
  boardId: '{{board-id}}',
  user: '{{wekan-username}}',
  card: '{{card-title}}',
  description: 'act-moveCard'
}
```