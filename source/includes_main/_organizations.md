# Organizations
## The organization object
```
# EXAMPLE OBJECT
```

```json
{
  "data": {
    "id": "1",
    "type": "organizations",
    "attributes": {
      "name": "Prospect.io",
      "description": null,
      "website": "https://prospect.io",
      "email": "contact@prospect.io",
      "phone": "+32-481-754-301",
      "country": "Belgium",
      "state": "Walloon Brabant",
      "city": "Wavre",
      "address": "Wavre",
      "c_custom_field_a": "Hot lead",
      "created_from": "extension",
      "archived": true,
      "lists": ["Belgium", "IT"],
      "created_at": "2015-08-15T16:48:46+02:00",
      "updated_at": "2016-11-25T12:40:46+01:00"
    }
  }
}
```

### Object attributes
Attribute | Filterable? | Description
--------- | ---------- | -----------
id | **yes** | **integer** <br />A unique identifier for the organization
name | **yes** | **string** <br />The name of the organization
website | **yes** | **string** <br />The organization's website
description | **yes** | **string** <br />The organization's description
email | **yes** | **string** <br />The organization's contact email 
phone | **yes** | **string** <br />The organization's contact phone number
country | **yes** | **string** <br />The organization's country
city | **yes** | **string** <br />The organization's city
state | **yes** | **string** <br />The organization's state
address | **yes** |**string** <br />The organization's full address
archived | **yes** | **boolean** <br />Whether or not the organization is archived
lists | no | **string[]** <br /> Name of the lists of the organization
created_at | no | **datetime** <br />ISO 8601 format with timezone offset
updated_at | no | **datetime** <br />ISO 8601 format with timezone offset

### Custom Fields

Custom fields can be used as normal attributes by using their `identifier` as attribute key, see the `c_custom_field_a` example in the above payload.

You can retrieve the list of your custom fields by using the [custom fields index endpoint](#list-custom-fields).

They accept a value depending on [their format](#the-custom-field-object)

### Relationships
Object | Description
--------- | -----------
creator | The [user](#users) who created the organization
updater | The [user](#users) who updated the organization


## Create an organization
```shell
# DEFINITION
POST https://api.organization.io/public/v1/organizations

# EXAMPLE
curl -X POST "https://api.organization.io/public/v1/organizations" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8" \
-d '{
  "data": {
    "type": "organizations",
    "attributes": {
      "name": "Prospect.io",
      "c_custom_field_a": "Hot lead"
    }
  }
}'
```

This will create a new organization. If you don't set the `responsible_id` parameter then the user who performed the action will be assigned as the responsible user.

### Parameters
Parameter | Default | Description
--------- | ------- | ------------
id | *NULL* | A unique identifier for the organization
name | *NULL* | The name of the organization
website | *NULL* | The organization's website
description | *NULL* | The organization's description
email | *NULL* | The organization's contact email 
phone | *NULL* | The organization's contact phone number
country | *NULL* | The organization's country
city | *NULL* | The organization's city
state | *NULL* | The organization's state
address | *NULL* |The organization's full address
archived | *NULL* | Whether or not the organization is archived
lists | *NULL* | Name of the lists of the organization
created_at | *NULL* | ISO 8601 format with timezone offset
updated_at | *NULL* | ISO 8601 format with timezone offset


### Returns
Returns the [organization object](#the-organization-object).

## Retrieve an organization
```shell
# DEFINITION
GET https://api.organization.io/public/v1/organizations/{ORGANIZATION_ID}

# EXAMPLE
curl -X GET "https://api.organization.io/public/v1/organizations/1" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

### Parameters
Parameter | Description
--------- | -----------
id<br />**required** - *integer* | The ID of the organization to retrieve

### Returns
Returns the [organization object](#the-organization-object).

## Update an organization
```shell
# DEFINITION
PATCH https://api.organization.io/public/v1/organizations/{ORGANIZATION_ID}

# EXAMPLE
curl -X PATCH "https://api.organization.io/public/v1/organizations/1" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8" \
-d '{
  "data": {
    "type": "organizations",
    "attributes": {
      "name": "Prospect.io", 
      "c_custom_field_a": "Hot lead"
    }
  }
}'
```

Updates the specified organization by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

### Parameters
Parameter | Description
--------- | -----------
id | A unique identifier for the organization
name | The name of the organization
website | The organization's website
description | The organization's description
email | The organization's contact email 
phone | The organization's contact phone number
country | The organization's country
city | The organization's city
state | The organization's state
address | The organization's full address
archived | Whether or not the organization is archived
lists | Name of the lists of the organization
created_at | ISO 8601 format with timezone offset
updated_at | ISO 8601 format with timezone offset

### Returns
Returns the [organization object](#the-organization-object).

## Delete an organization
```shell
# DEFINITION
DELETE https://api.organization.io/public/v1/organizations/{ORGANIZATION_ID}

# EXAMPLE
curl -X DELETE "https://api.organization.io/public/v1/organizations/1" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "1",
    "type": "organizations"
  }
}
```

Permanently deletes an organization. It cannot be undone.

<aside class="warning">
Warning — Deleting an organization will also delete all history with this organization (messages, replies, etc.)
</aside>

### Parameters
Parameter | Required? | Type | Description
--------- | --------- | -----| -----------
id | **yes** | integer | The ID of the organization to delete

### Returns
Returns an object containing the organization ID.

## List organizations

```shell
# DEFINITION
GET https://api.organization.io/public/v1/organizations

# EXAMPLE
curl -X GET "https://api.organization.io/public/v1/organizations" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": "1",
      "type": "organizations",
      "attributes": {
        ...
      },
      "relationships": {
        "responsible": {
          "data": {
            ...
          }
        }
      }
    },
    {
      "id": "2",
      "type": "organizations",
      "attributes": {
        ...
      },
      "relationships": {
        "responsible": {
          "data": {
            ...
          }
        }
      }
    }
  ],
  "links": {
    "self": "https://api.organization.io/public/v1/organizations/?page%5Bnumber%5D=1&page%5Bsize%5D=100",
    "next": "https://api.organization.io/public/v1/organizations/?page%5Bnumber%5D=2&page%5Bsize%5D=100",
    "last": "https://api.organization.io/public/v1/organizations/?page%5Bnumber%5D=5&page%5Bsize%5D=100"
  }
}
```

Returns a list of organizations.

This list is [paginated](#pagination) by 100 records. It can also be [sorted](#sorting) or [filtered](#filtering).
