# Custom Fields
## The custom field object
```
# EXAMPLE OBJECT
```

```json
{
  "data": {
    "id": "1",
    "type": "custom_fields",
    "attributes": {
      "identifier": "c_custom_field_a",
      "name": "Lead Value",
      "value_type": "text"
    }
  }
}
```

### Object attributes
Attribute | Filterable? | Description
--------- | ----------- | -----------
id | no | **string** <br />A UUID key for the custom field
identifier | no | **string** <br />The custom field's `identifier` **to be used as attribute key into prospect objects' payload**
name | no | **string** <br />The custom field's name/label
value_type | no | **string** <br />The custom field's value type, can be one of the following: `numeric`, `text`, `text_long`, `phone`, `url`, `boolean`, `list_single`, `list_multiple`, `datetime`


## List Custom Fields

```shell
# DEFINITION
GET https://api.prospect.io/public/v1/custom_fields

# EXAMPLE
curl -X GET "https://api.prospect.io/public/v1/custom_fields" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8" \
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": "1",
      "type": "custom_fields",
      "attributes": {
        ...
      }
    },
    {
      "id": "2",
      "type": "custom_fields",
      "attributes": {
        ...
      }
    }
  ]
}
```

Returns all custom fields.
