# Campaigns
## The campaign object
```
# EXAMPLE OBJECT
```

```json
{
  "data": {
    "id": "1961",
    "type": "campaigns",
    "attributes": {
      "name": "Intro + 1 follow up",
      "status": "available",
      "steps_count": 2,
      "sending_days": [
        "1",
        "2",
        "3",
        "4",
        "5"
      ],
      "stop_when": [
        "prospect.replied"
      ],
      "created_at": "2015-08-15T16:48:46+02:00",
      "updated_at": "2016-11-25T12:40:46+01:00"
    },
    "relationships": {
      "steps": {
        "data": [
          {
            "id": "3920",
            "type": "steps_prospect_email_steps"
          },
          {
            "id": "3922",
            "type": "steps_prospect_email_steps"
          }
        ]
      }
    }
  }
}
```

### Object attributes
Attribute | Filterable? | Description
--------- | ----------- | -----------
id | no | **integer** <br />A unique identifier for the campaign
name | no | **string** <br />The campaign's name
status | **yes** | **string** <br />The campaign's status that can take 3 different values: `available`, `archived` and `draft`
steps_count | no | **integer** <br />The number of steps in the campaign
sending_days | no | **array** <br />An array containing the days of the week when the campaign will send. Monday is `1`
stop_when | no | **array** <br />An array containing the events that trigger the campaign to stops. Possible values are `message.click`, `prospect.replied` and `prospect.convert`
created_at | no | **datetime** | ISO 8601 format with timezone offset
updated_at | no | **datetime** | ISO 8601 format with timezone offset

### Relationships
Object | Description
--------- | -----------
steps | The [steps](#campaign-steps) of the campaign. Can be a email to the prospect `steps_prospect_email_steps` or a team notification email `steps_notification_email_steps`.

## Retrieve a campaign
```shell
# DEFINITION
GET https://api.prospect.io/public/v1/campaigns/{CAMPAIGN_ID}

# EXAMPLE
curl -X GET "https://api.prospect.io/public/v1/campaigns/1" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

### Parameters
Parameter | Description
--------- | -----------
id<br />**required** - *integer* | The ID of the campaign to retrieve

### Returns
Returns the [campaign object](#the-campaign-object).

## List campaigns
```shell
# DEFINITION
GET https://api.prospect.io/public/v1/campaigns

# EXAMPLE
curl -X GET "https://api.prospect.io/public/v1/campaigns" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8" \
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": "1",
      "type": "campaigns",
      "attributes": {
        ...
      },
      "relationships": {
        "steps": {
          "data": [
            ...
          ]
        }
      }
    },
    {
      "id": "2",
      "type": "campaigns",
      "attributes": {
        ...
      },
      "relationships": {
        "steps": {
          "data": [
            ...
          ]
        }
      }
    }
  ],
  "links": {
    "self": "https://api.prospect.io/public/v1/campaigns/?page%5Bnumber%5D=1&page%5Bsize%5D=100",
    "next": "https://api.prospect.io/public/v1/campaigns/?page%5Bnumber%5D=2&page%5Bsize%5D=100",
    "last": "https://api.prospect.io/public/v1/campaigns/?page%5Bnumber%5D=5&page%5Bsize%5D=100"
  }
}
```

Returns a list of campaigns.

This list is [paginated](#pagination) by 100 records and can also be [sorted](#sorting) or [filtered](#filtering).
