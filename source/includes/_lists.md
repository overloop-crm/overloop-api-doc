# Lists
## The list object
```
# EXAMPLE OBJECT
```

```json
{
  "data": {
    "id": "1",
    "type": "lists",
    "attributes": {
      "name": "LinkedIn",
      "available": true,
      "created_at": "2015-08-15T16:48:46+02:00",
      "updated_at": "2016-11-25T12:40:46+01:00"
    }
  }
}
```

### Object attributes
Attribute | Description
--------- | -----------
id | **integer** <br />A unique identifier for the list
name | **string** <br />The list's name
available | **boolean** <br />Whether or not the list is available
created_at | **datetime** | ISO 8601 format with timezone offset
updated_at | **datetime** | ISO 8601 format with timezone offset


## Create a list
```shell
# DEFINITION
POST https://prospect.io/api/public/v1/lists

# EXAMPLE
curl -X POST "https://prospect.io/api/public/v1/lists" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8" \
-d '{
  "data": {
    "type": "lists",
    "attributes": {
      "name": "A list name",
      "available": true
    }
  }
}'
```

This will create a new list.

### Parameters
Parameter | Default | Description
--------- | ------- | ------------
name<br />**required** - *string* | / | The list's name
available<br />*boolean* | *true* | Whether or not the list is available

### Returns
Returns the [list object](#the-list-object).

## Retrieve a list
```shell
# DEFINITION
GET https://prospect.io/api/public/v1/lists/{LIST_ID}

# EXAMPLE
curl -X GET "https://prospect.io/api/public/v1/lists/1" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

### Parameters
Parameter | Description
--------- | -----------
id<br />**required** - *integer* | The ID of the list to retrieve

### Returns
Returns the [list object](#the-list-object).

## Update a list
```shell
# DEFINITION
PATCH https://prospect.io/api/public/v1/lists/{LIST_ID}

# EXAMPLE
curl -X PATCH "https://prospect.io/api/public/v1/lists/1" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8" \
-d '{
  "data": {
    "type": "lists",
    "attributes": {
      "name": "LinkedIn bis"
    }
  }
}'
```

Updates the specified list by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

### Parameters
Parameter | Description
--------- | -----------
id<br />**required** - *integer* | The ID of the list to update
name<br />*string* | / | The list's name
available<br />*boolean* | *true* | Whether or not the list is available

### Returns
Returns the [list object](#the-list-object).

## Delete a list
```shell
# DEFINITION
DELETE https://prospect.io/api/public/v1/lists/{PROSPECT_ID}

# EXAMPLE
curl -X DELETE "https://prospect.io/api/public/v1/lists/1" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8" \
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "1",
    "type": "lists"
  }
}
```

Permanently deletes a list. It cannot be undone.

<aside class="notice">
Warning — Deleting a list will keep the prospects of that list the `list_id` field to `NULL`
</aside>

### Parameters
Parameter | Required? | Type | Description
--------- | --------- | -----| -----------
id | **yes** | integer | The ID of the list to delete

### Returns
Returns an object containing the list ID.

## List lists

```shell
# DEFINITION
GET https://prospect.io/api/public/v1/lists

# EXAMPLE
curl -X GET "https://prospect.io/api/public/v1/lists" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8" \
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": "1",
      "type": "lists",
      "attributes": {
        ...
      }
    },
    {
      "id": "2",
      "type": "list",
      "attributes": {
        ...
      }
    }
  ],
  "links": {
    "self": "https://prospect.io/api/public/v1/lists/?page%5Bnumber%5D=1&page%5Bsize%5D=100",
    "next": "https://prospect.io/api/public/v1/lists/?page%5Bnumber%5D=2&page%5Bsize%5D=100",
    "last": "https://prospect.io/api/public/v1/lists/?page%5Bnumber%5D=5&page%5Bsize%5D=100"
  }
}
```

Returns a list of lists.

This list is [paginate](#pagination) by 100 records and can also be [sorted](#sorting).
