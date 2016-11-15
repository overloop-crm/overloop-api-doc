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
      "created_from": "extension",
      "last_emailed_at": null,
      "converted": false,
      "qualified": true,
      "archived": false,
      "replied": false,
      "campaign_status": null,
      "created_at": "2015-10-27T19:57:00.000Z",
      "updated_at": "2016-08-03T13:36:13.000Z"
    },
    "relationships": {
      "responsible": {
        "data": {
          "id": "1",
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
      }
    }
  }
}
```

### Object attributes
Attribute | Description
--------- | -----------
id | **integer** <br />A unique identifier for the prospect
email | **string** <br />The prospect's email address
first_name | **string** <br />The prospect's first name
last_name | **string** <br />The prospect's last name
organisation_name | **string** <br />The prospect's company name
description | **string** <br />A text description of the prospect
domain | **string** <br />The prospect's website
jobtitle | **string** <br />The prospect's job title
linkedin_profile | **string** <br />A link to the prospect's LinkedIn profile
created_from | **string** <br />The source of the prospect. Can be `web`, `extension`, `api` or `import`
last_emailed_at | **datetime** <br />The date and time of the last email sent to this prospect
converted | **boolean** <br />Whether or not the prospect is marked as converted
qualified | **boolean** <br />Whether or not the prospect is marked as qualified
archived | **boolean** <br />Whether or not the prospect is archived
replied | **boolean** <br />Whether or not the prospect replied to any of your emails
campaign_status | **string** <br />If the prospect is currently in a campaign, this attribute contains the status of the campaign. Can be `running`, `paused` or `scheduled`
created_at | **datetime**
updated_at | **datetime**

### Relationships
Object | Description
--------- | -----------
responsible | The [user](#users) responsible of the prospect
list | Describe a [list object](#lists) if the prospect is in a list
campaign | Describe a [campaign object](#lists) if the prospect is currently in a campaign. The campaign status is described in the `campaign_status` attribute

## Create a prospect
```shell
# DEFINITION
POST https://prospect.io/api/public/v1/prospects

# EXAMPLE
curl -X POST "https://prospect.io/api/public/v1/prospects" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8" \
-d '{
  "data": {
    "type": "prospects",
    "attributes": {
      "email": "vincenzo@prospect.io",
      "first_name": "Vincenzo",
      "last_name": "Ruggiero"
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
converted<br />*boolean* | false | Whether or not the prospect is marked as converted
qualified<br />*boolean* | false | Whether or not the prospect is marked as qualified
archived<br />*boolean* | false | Whether or not the prospect is marked as archived
list_id<br />*integer* | *NULL* | ID of the list where to save the prospect
responsible_id<br />*integer* | ID of the user who created the prospect | The ID of the user responsible for this prospect
campaign_id<br />*integer* | *NULL* | If you specify a campaign ID we'll add the prospect in the campaign. The attribute `campaign_status` will also be set to `running`.

### Returns
Returns the [prospect object](#the-prospect-object).

## Retrieve a prospect
```shell
# DEFINITION
GET https://prospect.io/api/public/v1/prospects/{PROSPECT_ID}

# EXAMPLE
curl -X GET "https://prospect.io/api/public/v1/prospects/1" \
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
PATCH https://prospect.io/api/public/v1/prospects/{PROSPECT_ID}

# EXAMPLE
curl -X PATCH "https://prospect.io/api/public/v1/prospects/1" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8" \
-d '{
  "data": {
    "type": "prospects",
    "attributes": {
      "first_name": "Vincent"
    }
  }
}'
```

Updates the specified prospect by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

### Parameters
Parameter | Description
--------- | -----------
id<br />**required** - *integer* | The ID of the prospect to update
email<br />*string* | The prospect's email
first_name<br />*string* | The prospect's first name
last_name<br />*string* | The prospect's last name
organisation_name<br />*string* | The prospect's company name
description<br />*string* | A text description of the prospect
domain<br />*string* | The prospect's website
jobtitle<br />*string* | The prospect's job title
linkedin_profile<br />*string* | A link to the prospect's LinkedIn profile
converted<br />*boolean* | Whether or not the prospect is marked as converted
qualified<br />*boolean* | Whether or not the prospect is marked as qualified
archived<br />*boolean* | Whether or not the prospect is marked as archived
list_id<br />*integer* | ID of the list where to save the prospect
responsible_id<br />*integer* | The ID of the user responsible for this prospect
campaign_id<br />*integer* | If you specify a campaign ID here we'll add the prospect in the campaign. The attribute `campaign_status` will also be set to `running`. <br /><br />If the prospect was already in a campaign you first need to do an update and set `campaign_id` to `NULL` before adding the prospect to a new campaign. Setting `campaign_id` to `NULL` will **stop** the campaign.

### Returns
Returns the [prospect object](#the-prospect-object).

## Delete a prospect
```shell
# DEFINITION
DELETE https://prospect.io/api/public/v1/prospects/{PROSPECT_ID}

# EXAMPLE
curl -X DELETE "https://prospect.io/api/public/v1/prospects/1" \
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
GET https://prospect.io/api/public/v1/prospects

# EXAMPLE
curl -X GET "https://prospect.io/api/public/v1/prospects" \
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
        }
      }
    }
  ],
  "links": {
    "self": "https://prospect.io/api/public/v1/prospects/?page%5Bnumber%5D=1&page%5Bsize%5D=100",
    "next": "https://prospect.io/api/public/v1/prospects/?page%5Bnumber%5D=2&page%5Bsize%5D=100",
    "last": "https://prospect.io/api/public/v1/prospects/?page%5Bnumber%5D=5&page%5Bsize%5D=100"
  }
}
```

Returns a list of prospects.

This list is [paginate](#pagination) by 100 records and can also be [sorted](#sorting).
