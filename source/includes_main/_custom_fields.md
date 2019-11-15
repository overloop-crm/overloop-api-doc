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
value_type | no | **string** <br />The custom field's value type, can be one of the following: `numeric`, `text`, `text_long`, `phone`, `url`, `boolean`, `list_single`, `list_multiple`, `datetime`, `date`

### Value format

Depending on the type of custom field value, it can accept different kinds of value: 

 - `numeric`: any number (integer or float number) 
 - `text`, `text_long`: any string
 - `phone`: any string
 - `url`: any string
 - `boolean`: a boolean (true or false) 
 - `list_single`: a string representing any value from the list of choice for this field (case sensitive) 
 - `list_mulitple`: an array of string representing values from the list of choice for this field (case sensitive) 
 - `datetime`: a string representing time in the ISO 8601 format (ex: 2019-11-14T09:45:30Z) 
 - `date`: a string representing a date in the YYYY-MM-DD format (ex: 2018-01-04 for the 1st April of 2018) 

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
