# Exclusion list items
## The exclusion list item object
```
# EXAMPLE OBJECT
```

```json
{
  "data": {
    "id": "1",
    "type": "exclusion_list_item",
    "attributes": {
      "value": "vincenzo@prospect.io",
      "item_type": "email",
      "created_at": "2015-08-15T16:48:46+02:00"
    }
  }
}
```

### Object attributes
Attribute | Filterable? | Description
--------- | ----------- | -----------
id | no | **string** <br />The id of the exclusion list item
value | yes | **string** <br />The value of the exclusion list item
item_type | yes | **string** <br />The type of the exclusion list item, can be one of the following: `email`, `domain`
created_at | no | **datetime** <br /> ISO 8601 format with timezone offset

## Create an exclusion list item


This will create a new exclusion list item.

```shell
# DEFINITION
POST https://api.prospect.io/public/v1/exclusion_list_items

# EXAMPLE
curl -X POST "https://api.prospect.io/public/v1/exclusion_list_items" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8" \
-d '
  {
    "data": {
      "type": "exclusion_list_item",
      "attributes": {
        "value": "vincenzo@prospect.io",
        "item_type": "email"
      }
    }
  }
'
```

> The above command returns JSON structured like this:

```json
{
    "data": {
        "id": "1",
        "type": "exclusion_list_item",
        "attributes": {
            "value": "vincenzo@prospect.io",
            "item_type": "email",
            "created_at": "2015-08-15T16:48:46+02:00"
        }
    }
}
```

### Parameters

Attribute | Default | Description
--------- | ---------- | -----------
item_type | *NULL* | What would you like to exclude: "domain" or "email"
value | *NULL* | The domain or email value to exclude

## Delete an exclusion list item
```shell
# DEFINITION
DELETE https://api.prospect.io/public/v1/exclusion_list_items/{ITEM_ID}

# EXAMPLE
curl -X DELETE "https://api.prospect.io/public/v1/exclusion_list_items/1" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "1",
    "type": "exclusion_list_items"
  }
}
```

Permanently deletes an exclusion list item. It cannot be undone.


### Parameters
Parameter | Required? | Type | Description
--------- | --------- | -----| -----------
id | **yes** | integer | The ID of the item to delete

### Returns
Returns an object containing the exclusion list item ID.

## List exclusion list items

```shell
# DEFINITION
GET https://api.prospect.io/public/v1/exclusion_list_items

# EXAMPLE
curl -X GET "https://api.prospect.io/public/v1/exclusion_list_items" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": "1",
      "type": "exclusion_list_item",
      "attributes": {
        "value": "vincenzo@prospect.io",
        "item_type": "email",
        "created_at": "2015-08-15T16:48:46+02:00"
      }
    },
    {
      "id": "1",
      "type": "exclusion_list_item",
      "attributes": {
        "value": "gmail.com",
        "item_type": "domain",
        "created_at": "2015-08-15T16:48:46+02:00"
      }
    }
  ],
  "links": {
    "self": "https://api.prospect.io/public/v1/exclusion_list_items/?page%5Bnumber%5D=1&page%5Bsize%5D=100",
    "next": "https://api.prospect.io/public/v1/exclusion_list_items/?page%5Bnumber%5D=2&page%5Bsize%5D=100",
    "last": "https://api.prospect.io/public/v1/exclusion_list_items/?page%5Bnumber%5D=5&page%5Bsize%5D=100"
  }
}
```

Returns a list of exclusion list items.

This list is [paginated](#pagination) by 100 records. It can also be [sorted](#sorting) or [filtered](#filtering).
