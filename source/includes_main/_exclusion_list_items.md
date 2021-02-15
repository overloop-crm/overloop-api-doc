# Exclusion List Items
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
value | no | **string** <br />The value of the exclusion list item
item_type | no | **string** <br />The type of the exclusion list item, can be one of the following: `email`, `domain`
created_at | no | **datetime** <br /> ISO 8601 format with timezone offset

## Create an Exclusion List Item



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
