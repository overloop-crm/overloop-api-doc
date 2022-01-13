# Contacts
## The contact object
```
# EXAMPLE OBJECT
```

```json
{
  "data": {
    "id": "1",
    "type": "contacts",
    "attributes": {
      "email": "vincenzo@overloop.com",
      "first_name": "Vincenzo",
      "last_name": "Ruggiero",
      "description": null,
      "jobtitle": "CEO",
      "linkedin_profile": "https://www.linkedin.com/in/vincenzor",
      "phone": "+32-481-754-301",
      "title": "Mr.",
      "country": "Belgium",
      "state": "Walloon Brabant",
      "city": "Wavre",
      "industry": "IT",
      "lists": [
        "CEO",
        "BE"
      ],
      "c_custom_field_a": "Hot lead",
      "created_from": "extension",
      "last_emailed_at": null,
      "opened": false,
      "opened_at": null,
      "clicked": false,
      "clicked_at": null,
      "bounced": false,
      "replied": false,
      "replied_at": null,
      "excluded": false,
      "url": "https://overloop.com/contacts/1",
      "lists": ["Belgium", "Manager"],
      "created_at": "2015-08-15T16:48:46+02:00",
      "updated_at": "2016-11-25T12:40:46+01:00"
    },
    "relationships": {
      "creator": {
        "data": {
          "id": "1",
          "type": "users"
        }
      },
      "owner": {
        "data": {
          "id": "2",
          "type": "users"
        }
      },
      "organization": {
        "data": {
          "id": "2",
          "type": "organizations"
        }
      }
    }
  }
}
```

### Object attributes
Attribute | Filterable? | Description
--------- | ---------- | -----------
id | **yes** | **integer** <br />A unique identifier for the contact
email | **yes** | **string** <br />The contact's email address
first_name | **yes** | **string** <br />The contact's first name
last_name | **yes** | **string** <br />The contact's last name
description | no | **string** <br />A text description of the contact
jobtitle | **yes** | **string** <br />The contact's job title
linkedin_profile | no |**string** <br />A link to the contact's LinkedIn profile
phone | **yes** | **string** <br />The contact's phone number
title | **yes** | **string** <br />The contact's title of civility
country | **yes** | **string** <br />The contact's country
state | **yes** | **string** <br />The contact's state or region
city | **yes** | **string** <br />The contact's city
industry | **yes** | **string** <br />The contact's industry
created_from | no | **string** <br />The source of the contact. Can be `web`, `extension`, `api` or `import`
last_emailed_at | no | **datetime** <br />The date and time of the last email sent to this contact in ISO 8601 format with timezone offset
excluded | **yes** | **boolean** <br />Whether or not the contact is marked as excluded
opened | **yes** | **boolean** <br />Wheteer or not the contact opened any of your emails
clicked | **yes** | **boolean** <br />Wheter or not the contact clicked a link in any of your emails
replied | **yes** | **boolean** <br />Whether or not the contact replied to any of your emails
bounced | **yes** | **boolean** <br />Whether or not the contact email bounced
opened_at | no | **datetime** <br />The date and time when the contact last opened an email
clicked_at | no | **datetime** <br />The date and time when the contact last clicked a link in an email
replied_at | no | **datetime** <br />The date and time when the contact last replied to an email
url | no | **string** <br />The full URL to the contact on Overloop
lists | no | **array** <br /> Name of the lists of the contact
created_at | no | **datetime** <br />ISO 8601 format with timezone offset
updated_at | no | **datetime** <br />ISO 8601 format with timezone offset

### Custom Fields

Custom fields can be used as normal attributes by using their `identifier` as attribute key, see the `c_custom_field_a` example in the above payload.

You can retrieve the list of your custom fields by using the [custom fields index endpoint](#list-custom-fields).

They accept a value depending on [their format](#the-custom-field-object)

### Relationships
Object | Description
--------- | -----------
creator | The [user](#users) who created the contact
organization | The [organization](#organizations) of this contact
owner | The [user](#users) who owns the contact
enrollments | The [enrollments](#enrollments) of the contact in workflows


## Create a contact
```shell
# DEFINITION
POST https://api.overloop.com/public/v1/contacts

# EXAMPLE
curl -X POST "https://api.overloop.com/public/v1/contacts" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8" \
-d '{
  "data": {
    "type": "contacts",
    "attributes": {
      "email": "vincenzo@overloop.com",
      "first_name": "Vincenzo",
      "last_name": "Ruggiero",
      "lists": ["CEO", "BE"],
      "c_custom_field_a": "Hot lead"
    }
  }
}'
```

This will create a new contact. If you don't set the `owner_id` parameter then the user who performed the action will be assigned as the owner.

### Parameters
Parameter | Default | Description
--------- | ------- | ------------
email<br />*string* | *NULL* | The contact's email
first_name<br />*string* | *NULL* | The contact's first name
last_name<br />*string* | *NULL* | The contact's last name
description<br />*string* | *NULL* | A text description of the contact
jobtitle<br />*string* | *NULL* | The contact's job title
linkedin_profile<br />*string* | *NULL* | A link to the contact's LinkedIn profile
phone<br />*string* | *NULL* | The contact's phone number
title<br />*string* | *NULL* | The contact's title of civility
country<br />*string* | *NULL* | The contact's country
state<br />*string* | *NULL* | The contact's state or region
city<br />*string* | *NULL* | The contact's city
industry<br />*string* | *NULL* | The contact's industry
lists<br />*array* | *NULL* | Name of the lists where to save the contact<br/>(note: we will create the lists if they don't exist)
owner_id<br />*integer* | ID of the user who created the contact | The ID of the user owning this contact
organization_id<br />*integer* | ID of the organization this contact belongs to | See [create an organization](#create-an-organization)

This method accepts an optional URL parameter `return_existing`. When set to true (default is false),
that will return an existing organization if an organization with that name already exists (with 200 HTTP status code, 422 otherwise).

### Returns
Returns the [contact object](#the-contact-object).

## Retrieve a contact
```shell
# DEFINITION
GET https://api.overloop.com/public/v1/contacts/{CONTACT_ID}

# EXAMPLE
curl -X GET "https://api.overloop.com/public/v1/contacts/1" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

### Parameters
Parameter | Description
--------- | -----------
id<br />**required** - *integer* | The ID of the contact to retrieve

### Returns
Returns the [contact object](#the-contact-object).

## Update a contact
```shell
# DEFINITION
PATCH https://api.overloop.com/public/v1/contacts/{CONTACT_ID}

# EXAMPLE
curl -X PATCH "https://api.overloop.com/public/v1/contacts/1" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8" \
-d '{
  "data": {
    "type": "contacts",
    "attributes": {
      "email": "vincenzo@overloop.com",
      "first_name": "Vincent",
      "c_custom_field_a": "Hot lead"
    }
  }
}'
```

Updates the specified contact by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

### Parameters
Parameter | Description
--------- | -----------
id<br />**required** - *integer* | The ID of the contact to update
email<br />*string* | The contact's email
first_name<br />*string* | The contact's first name
last_name<br />*string* | The contact's last name
description<br />*string* | A text description of the contact
jobtitle<br />*string* | The contact's job title
linkedin_profile<br />*string* | A link to the contact's LinkedIn profile
phone<br />*string* | The contact's phone number
title<br />*string* | The contact's title of civility
country<br />*string* | The contact's country
state<br />*string* | *NULL* | The contact's state or region
city<br />*string* | *NULL* | The contact's city
industry<br />*string* | The contact's industry
lists<br />*array* | Name of the lists where to save the contact<br/>(note: we will create the lists if they don't exist)
owner_id<br />*integer* | The ID of the user owning this contact
organization_id<br />*integer* | ID of the organization this contact belongs to | See [create an organization](#create-an-organization)

### Returns
Returns the [contact object](#the-contact-object).

## Delete a contact
```shell
# DEFINITION
DELETE https://api.overloop.com/public/v1/contacts/{CONTACT_ID}

# EXAMPLE
curl -X DELETE "https://api.overloop.com/public/v1/contacts/1" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "1",
    "type": "contacts"
  }
}
```

Permanently deletes a contact. It cannot be undone.

<aside class="warning">
Warning — Deleting a contact will also delete all history with this contact (messages, replies, etc.)
</aside>

### Parameters
Parameter | Required? | Type | Description
--------- | --------- | -----| -----------
id | **yes** | integer | The ID of the contact to delete

### Returns
Returns an object containing the contact ID.

## List contacts

```shell
# DEFINITION
GET https://api.overloop.com/public/v1/contacts

# EXAMPLE
curl -X GET "https://api.overloop.com/public/v1/contacts" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": "1",
      "type": "contacts",
      "attributes": {
        ...
      },
      "relationships": {
        "owner": {
          "data": {
            ...
          }
        }
      }
    },
    {
      "id": "2",
      "type": "contacts",
      "attributes": {
        ...
      },
      "relationships": {
        "owner": {
          "data": {
            ...
          }
        }
      }
    }
  ],
  "links": {
    "self": "https://api.overloop.com/public/v1/contacts/?page%5Bnumber%5D=1&page%5Bsize%5D=100",
    "next": "https://api.overloop.com/public/v1/contacts/?page%5Bnumber%5D=2&page%5Bsize%5D=100",
    "last": "https://api.overloop.com/public/v1/contacts/?page%5Bnumber%5D=5&page%5Bsize%5D=100"
  }
}
```

Returns a list of contacts.

This list is [paginated](#pagination) by 100 records. It can also be [sorted](#sorting) or [filtered](#filtering).

### Returns
Returns the [contact object](#the-contact-object).
