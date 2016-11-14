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
      "available": false,
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
      "created_at": "2015-10-27T19:57:00.000Z",
      "updated_at": "2016-08-03T13:36:13.000Z"
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
Attribute | Description
--------- | -----------
id | **integer** <br />A unique identifier for the campaign
name | **string** <br />The campaign's name
available | **boolean** <br />Whether or not the campaign is available
steps_count | **integer** <br />The number of steps in the campaign
sending_days | **array** <br />An array containing the days of the week when the campaign will send. Monday is `1`
stop_when | **array** <br />An array containing the events that trigger the campaign to stops. Possible values are `message.click`, `prospect.replied` and `prospect.convert`
created_at | **datetime**
updated_at | **datetime**

### Relationships
Object | Description
--------- | -----------
steps | The [steps](#campaign-steps) of the campaign. Can be a email to the prospect `steps_prospect_email_steps` or a team notification email `steps_notification_email_steps`.

## Retrieve a campaign
```shell
# DEFINITION
GET https://prospect.io/api/public/v1/campaigns/{CAMPAIGN_ID}

# EXAMPLE
curl -X GET "https://prospect.io/api/public/v1/campaigns/1" \
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
GET https://prospect.io/api/public/v1/campaigns

# EXAMPLE
curl -X GET "https://prospect.io/api/public/v1/campaigns" \
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
    "self": "https://prospect.io/api/public/v1/campaigns/?page%5Bnumber%5D=1&page%5Bsize%5D=100",
    "next": "https://prospect.io/api/public/v1/campaigns/?page%5Bnumber%5D=2&page%5Bsize%5D=100",
    "last": "https://prospect.io/api/public/v1/campaigns/?page%5Bnumber%5D=5&page%5Bsize%5D=100"
  }
}
```

Returns a list of campaigns.

This list is [paginate](#pagination) by 100 records and can also be [sorted](#sorting).
