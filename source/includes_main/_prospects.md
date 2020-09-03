# Prospects
## The prospect object
```
# EXAMPLE OBJECT
```

```json
{
  "data": {
    "id": "1",
    "type": "prospects",
    "attributes": {
      "email": "vincenzo@prospect.io",
      "first_name": "Vincenzo",
      "last_name": "Ruggiero",
      "organisation_name": "Prospect.io",
      "description": null,
      "domain": "https://prospect.io",
      "jobtitle": "CEO",
      "linkedin_profile": "https://www.linkedin.com/in/vincenzor",
      "phone": "+32-481-754-301",
      "title": "Mr.",
      "country": "Belgium",
      "state": "Walloon Brabant",
      "city": "Wavre",
      "industry": "IT",
      "c_custom_field_a": "Hot lead",
      "created_from": "extension",
      "last_emailed_at": null,
      "converted": false,
      "converted_at": null,
      "qualified": true,
      "archived": true,
      "archived_reason": "excluded",
      "replied": false,
      "replied_at": null,
      "bounced": false,
      "campaign_status": null,
      "url": "https://prospect.io/prospects/1",
      "list_name": "Sales Managers in UK",
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
      "responsible": {
        "data": {
          "id": "2",
          "type": "users"
        }
      },
      "list": {
        "data": {
          "id": "1",
          "type": "lists"
        }
      },
      "campaign": {
        "data": null
      },
      "current_campaign_subscription": {
        "data": null
      }
    }
  }
}
```

### Object attributes
Attribute | Filterable? | Description
--------- | ---------- | -----------
id | **yes** | **integer** <br />A unique identifier for the prospect
email | **yes** | **string** <br />The prospect's email address
first_name | **yes** | **string** <br />The prospect's first name
last_name | **yes** | **string** <br />The prospect's last name
organisation_name | no | **string** <br />The prospect's company name
description | no | **string** <br />A text description of the prospect
domain | **yes** | **string** <br />The prospect's website
jobtitle | **yes** | **string** <br />The prospect's job title
linkedin_profile | no |**string** <br />A link to the prospect's LinkedIn profile
phone | **yes** | **string** <br />The prospect's phone number
title | **yes** | **string** <br />The prospect's title of civility
country | **yes** | **string** <br />The prospect's country
state | **yes** | **string** <br />The prospect's state or region
city | **yes** | **string** <br />The prospect's city
industry | **yes** | **string** <br />The prospect's industry
created_from | no | **string** <br />The source of the prospect. Can be `web`, `extension`, `api` or `import`
last_emailed_at | no | **datetime** <br />The date and time of the last email sent to this prospect in ISO 8601 format with timezone offset
converted | **yes** | **boolean** <br />Whether or not the prospect is marked as converted
converted_at | no | **datetime** <br />The date and time when the prospect has been marked as converted
qualified | **yes** | **boolean** <br />Whether or not the prospect is marked as qualified
archived | **yes** | **boolean** <br />Whether or not the prospect is archived
archived_reason | **yes** | **string** <br />If the prospect is archived, this attribute contains the reason. Can be `exluded`, `opt-out` or nothing if the archive was manual.
opened | **yes** | **boolean** <br />Wheteer or not the prospect opened any of your emails
clicked | **yes** | **boolean** <br />Wheter or not the prospect clicked a link in any of your emails
replied | **yes** | **boolean** <br />Whether or not the prospect replied to any of your emails
replied_at | no | **datetime** <br />The date and time when the prospect first replied
bounced | **yes** | **boolean** <br />Whether or not the prospect email bounced
campaign_status | no | **string** <br />If the prospect is currently in a campaign, this attribute contains the status of the campaign. Can be `running`, `paused` or `scheduled`
url | no | **string** <br />The full URL to the prospect on Prospect.io
list_name | no | **string** <br />The name of the list if the prospect is in a list
created_at | no | **datetime** | ISO 8601 format with timezone offset
updated_at | no | **datetime** | ISO 8601 format with timezone offset

### Custom Fields

Custom fields can be used as normal attributes by using their `identifier` as attribute key, see the `c_custom_field_a` example in the above payload.

You can retrieve the list of your custom fields by using the [custom fields index endpoint](#list-custom-fields). 

They accept a value depending on [their format](#the-custom-field-object)

### Relationships
Object | Description
--------- | -----------
creator | The [user](#users) who created the prospect
responsible | The [user](#users) responsible of the prospect
list | Describe a [list object](#lists) if the prospect is in a list
campaign | Describe a [campaign object](#campaign) if the prospect is currently in a campaign. The campaign status is described in the `campaign_status` attribute
current_campaign_subscription | Describe a [campaign subscription](#campaign-subscriptions) if the prospect is currently in a campaign.


## Create a prospect
```shell
# DEFINITION
POST https://api.prospect.io/public/v1/prospects

# EXAMPLE
curl -X POST "https://api.prospect.io/public/v1/prospects" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8" \
-d '{
  "data": {
    "type": "prospects",
    "attributes": {
      "email": "vincenzo@prospect.io",
      "first_name": "Vincenzo",
      "last_name": "Ruggiero",
      "c_custom_field_a": "Hot lead"
    }
  }
}'
```

This will create a new prospect. If you don't set the `responsible_id` parameter then the user who performed the action will be assigned as the responsible user.

### Parameters
Parameter | Default | Description
--------- | ------- | ------------
email<br />**required** - *string* | / | The prospect's email
first_name<br />*string* | *NULL* | The prospect's first name
last_name<br />*string* | *NULL* | The prospect's last name
organisation_name<br />*string* | *NULL* | The prospect's company name
description<br />*string* | *NULL* | A text description of the prospect
domain<br />*string* | *NULL* | The prospect's website
jobtitle<br />*string* | *NULL* | The prospect's job title
linkedin_profile<br />*string* | *NULL* | A link to the prospect's LinkedIn profile
phone<br />*string* | *NULL* | The prospect's phone number
title<br />*string* | *NULL* | The prospect's title of civility
country<br />*string* | *NULL* | The prospect's country
state<br />*string* | *NULL* | The prospect's state or region
city<br />*string* | *NULL* | The prospect's city
industry<br />*string* | *NULL* | The prospect's industry
list_id<br />*integer* | *NULL* | ID of the list where to save the prospect
responsible_id<br />*integer* | ID of the user who created the prospect | The ID of the user responsible for this prospect

### Returns
Returns the [prospect object](#the-prospect-object).

## Retrieve a prospect
```shell
# DEFINITION
GET https://api.prospect.io/public/v1/prospects/{PROSPECT_ID}

# EXAMPLE
curl -X GET "https://api.prospect.io/public/v1/prospects/1" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

### Parameters
Parameter | Description
--------- | -----------
id<br />**required** - *integer* | The ID of the prospect to retrieve

### Returns
Returns the [prospect object](#the-prospect-object).

## Update a prospect
```shell
# DEFINITION
PATCH https://api.prospect.io/public/v1/prospects/{PROSPECT_ID}

# EXAMPLE
curl -X PATCH "https://api.prospect.io/public/v1/prospects/1" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8" \
-d '{
  "data": {
    "type": "prospects",
    "attributes": {
      "email": "vincenzo@prospect.io",
      "first_name": "Vincent",
      "c_custom_field_a": "Hot lead"
    }
  }
}'
```

Updates the specified prospect by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

### Parameters
Parameter | Description
--------- | -----------
id<br />**required** - *integer* | The ID of the prospect to update
email<br />**required** - *string* | The prospect's email
first_name<br />*string* | The prospect's first name
last_name<br />*string* | The prospect's last name
organisation_name<br />*string* | The prospect's company name
description<br />*string* | A text description of the prospect
domain<br />*string* | The prospect's website
jobtitle<br />*string* | The prospect's job title
linkedin_profile<br />*string* | A link to the prospect's LinkedIn profile
phone<br />*string* | The prospect's phone number
title<br />*string* | The prospect's title of civility
country<br />*string* | The prospect's country
state<br />*string* | *NULL* | The prospect's state or region
city<br />*string* | *NULL* | The prospect's city
industry<br />*string* | The prospect's industry
list_id<br />*integer* | ID of the list where to save the prospect
responsible_id<br />*integer* | The ID of the user responsible for this prospect

### Returns
Returns the [prospect object](#the-prospect-object).

## Delete a prospect
```shell
# DEFINITION
DELETE https://api.prospect.io/public/v1/prospects/{PROSPECT_ID}

# EXAMPLE
curl -X DELETE "https://api.prospect.io/public/v1/prospects/1" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8" \
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "1",
    "type": "prospects"
  }
}
```

Permanently deletes a prospect. It cannot be undone.

<aside class="warning">
Warning — Deleting a prospect will also delete all history with this prospect (messages, replies, etc.)
</aside>

### Parameters
Parameter | Required? | Type | Description
--------- | --------- | -----| -----------
id | **yes** | integer | The ID of the prospect to delete

### Returns
Returns an object containing the prospect ID.

## List prospects

```shell
# DEFINITION
GET https://api.prospect.io/public/v1/prospects

# EXAMPLE
curl -X GET "https://api.prospect.io/public/v1/prospects" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8" \
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": "1",
      "type": "prospects",
      "attributes": {
        ...
      },
      "relationships": {
        "responsible": {
          "data": {
            ...
          }
        },
        "list": {
          "data": {
            ...
          }
        },
        "campaign": {
          "data": {
            ...
          }
        },
        "current_campaign_subscription": {
          "data": {
            ...
          }
        }
      }
    },
    {
      "id": "2",
      "type": "prospects",
      "attributes": {
        ...
      },
      "relationships": {
        "responsible": {
          "data": {
            ...
          }
        },
        "list": {
          "data": {
            ...
          }
        },
        "campaign": {
          "data": {
            ...
          }
        },
        "current_campaign_subscription": {
          "data": {
            ...
          }
        }
      }
    }
  ],
  "links": {
    "self": "https://api.prospect.io/public/v1/prospects/?page%5Bnumber%5D=1&page%5Bsize%5D=100",
    "next": "https://api.prospect.io/public/v1/prospects/?page%5Bnumber%5D=2&page%5Bsize%5D=100",
    "last": "https://api.prospect.io/public/v1/prospects/?page%5Bnumber%5D=5&page%5Bsize%5D=100"
  }
}
```

Returns a list of prospects.

This list is [paginated](#pagination) by 100 records. It can also be [sorted](#sorting) or [filtered](#filtering).

## Mark as (not) qualified
```shell
# DEFINITION: Mark as qualified
POST https://api.prospect.io/public/v1/prospects/{PROSPECT_ID}/qualification

# EXAMPLE
curl -X POST "https://api.prospect.io/public/v1/prospects/1/qualification" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8" \

# DEFINITION: Mark as not qualified
DELETE https://api.prospect.io/public/v1/prospects/{PROSPECT_ID}/qualification

# EXAMPLE
curl -X DELETE "https://api.prospect.io/public/v1/prospects/1/qualification" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8" \
```

Mark a prospect as qualified or not qualified.

### Parameters
Parameter | Required? | Type | Description
--------- | --------- | -----| -----------
id | **yes** | integer | The ID of the prospect to mark as (not) qualified

### Returns
Returns the [prospect object](#the-prospect-object).

## Mark as (not) converted
```shell
# DEFINITION: Mark as converted
POST https://api.prospect.io/public/v1/prospects/{PROSPECT_ID}/conversion

# EXAMPLE
curl -X POST "https://api.prospect.io/public/v1/prospects/1/conversion" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8" \

# DEFINITION: Mark as not converted
DELETE https://api.prospect.io/public/v1/prospects/{PROSPECT_ID}/conversion

# EXAMPLE
curl -X DELETE "https://api.prospect.io/public/v1/prospects/1/conversion" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8" \
```

Mark a prospect as converted or not converted.

### Parameters
Parameter | Required? | Type | Description
--------- | --------- | -----| -----------
id | **yes** | integer | The ID of the prospect to mark as (not) converted

### Returns
Returns the [prospect object](#the-prospect-object).

## Mark as (not) archived
```shell
# DEFINITION: Mark as archived
POST https://api.prospect.io/public/v1/prospects/{PROSPECT_ID}/archive

# EXAMPLE
curl -X POST "https://api.prospect.io/public/v1/prospects/1/archive" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8" \

# DEFINITION: Mark as not archived
DELETE https://api.prospect.io/public/v1/prospects/{PROSPECT_ID}/archive

# EXAMPLE
curl -X DELETE "https://api.prospect.io/public/v1/prospects/1/archive" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8" \
```

Mark a prospect as archived or not archived.

### Parameters
Parameter | Required? | Type | Description
--------- | --------- | -----| -----------
id | **yes** | integer | The ID of the prospect to mark as (not) archived
remove_tasks | ***yes*** (when archiving) | boolean | Whether the prospect's tasks are to be deleted

### Returns
Returns the [prospect object](#the-prospect-object).
