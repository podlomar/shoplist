---
layout: default
title: Data manipulation
permalink: /sending
nav_order: 1
---

# Manipulating the data on the server

All changes to the data on the server are done by a POST request. Each POST request has an `action` filed signaling the action to be performed.

## Create new shopping list [POST]

Create new shopping list with name `name`,

```
{{ site.apibase }}/lists/{name}
```

Body:

```json
{
  "action": "create"
}
```

The parametr `name` can only consist of lowercase letters and numbers. No special characters or accented letters are allowed.

## Add item to a list [POST]

Add one item to the shopping list with name `name`.

```
{{ site.apibase }}/lists/{name}
```

```json
{
  "action": "addItem",
  "product": "Apples",
  "amount": "10 pc",
  "done": true
}
```

Besides `action`, the JSON has these properties:

| Property | Type    | Required | Default value |
| -------- | ------- | -------- | ------------- |
| product  | string  | yes      | _none_        |
| amount   | string  | no       | `""`          |
| done     | boolean | no       | `false`       |

The endpoint returns the whole updated list.

## Toggle item done [POST]

Flip the boolean value of the field `done` of item with id `itemId` in the list with name `name`.

```
{{ site.apibase }}/lists/{name}/{itemId}
```

```json
{
  "action": "toggleDone"
}
```

The endpoint return the updated item.

## Delete item from a list [POST]

Delete the item with id `itemId` from the shopping list with name `name`.

```
{{ site.apibase }}/lists/{name}/{itemId}
```

```json
{
  "action": "deleteItem"
}
```

The endpoint returns the whole updated list.

## Delete the whole list [POST]

Delete the shopping list with name `name`.

```
{{ site.apibase }}/lists/{name}
```

```json
{
  "action": "delete"
}
```

Beware, that the default list with name _default_ cannot be deleted.
