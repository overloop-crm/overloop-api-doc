# Campaign Steps
## The campaign step object
```
# EXAMPLE OBJECT
```

```json
{
  "data": [
    {
      "id": "3920",
      "type": "steps_prospect_email_steps",
      "attributes": {
        "subject": "Introduction {{company_name}}",
        "content": "<div>Hi {{prospect_firstname | default: 'there'}},<br /><br /></div>\r\n<div>My name is {{user_name}} and I'm the founder of&nbsp;<a href=\"https://prospect.io\">{{company_name}}</a>. Our product is already used by hundred of organizations like {{prospect_company_name | default: 'yours'}} to improve their sales prospecting and cold emailing.<br /><br /></div>\r\n<div>Could you direct me to the right person to talk about this so we can explore if this would be something valuable for you?<a href=\"https://prospect.io\"><br /></a></div>\r\n<div>Thanks for your time,</div>",
        "offset": 0,
        "position": 1,
        "recipient": "",
        "schedule_time": null,
        "created_at": "2015-10-27T19:57:00.000Z",
        "updated_at": "2016-08-03T13:36:13.000Z"
      },
      "relationships": {
        "campaign": {
          "data": {
            "id": "1961",
            "type": "campaigns"
          }
        }
      }
    }
  ]
}
```


### Object attributes
Attribute | Description
--------- | -----------
id | **integer** <br />A unique identifier for the campaign step
type | **string** <br />The type of step. Can be a email to the prospect `steps_prospect_email_steps` or a team notification email `steps_notification_email_steps`
subject | **string** <br />The subject of the email
content | **string** <br />The HTML content of the email
offset | **integer** <br />The number of days the step will be sent after the previous step
position | **integer** <br />The order position in the list
recipient | **string** <br />The recipient email for step of type `steps_notification_email_steps`
schedule_time | **datetime** <br />Time of day for this step to send
created_at | **datetime**
updated_at | **datetime**

### Relationships
Object | Description
--------- | -----------
campaign | The parent [campaign](#campaign)

## Retrieve a campaign step
```shell
# DEFINITION
GET https://prospect.io/api/public/v1/campaigns/{CAMPAIGN_ID}/steps/{STEP_ID}

# EXAMPLE
curl -X GET "https://prospect.io/api/public/v1/campaigns/1/steps/1" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

### Parameters
Parameter | Description
--------- | -----------
campaign_id<br />**required** - *integer* | The ID of the campaign
id<br />**required** - *integer* | The ID of the campaign step to retrieve

### Returns
Returns the [campaign step object](#the-campaign-step-object).

## List campaigns steps
```shell
# DEFINITION
GET https://prospect.io/api/public/v1/campaigns/{CAMPAIGN_ID}/steps

# EXAMPLE
curl -X GET "https://prospect.io/api/public/v1/campaigns/1/steps" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8" \
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": "3920",
      "type": "steps_prospect_email_steps",
      "attributes": {
        ...
      },
      "relationships": {
        "campaign": {
          "data": {
            "id": "1961",
            "type": "campaigns"
          }
        }
      }
    },
    {
      "id": "3922",
      "type": "steps_prospect_email_steps",
      "attributes": {
        ...
      },
      "relationships": {
        "campaign": {
          "data": {
            "id": "1961",
            "type": "campaigns"
          }
        }
      }
    },
    {
      "id": "20837",
      "type": "steps_notification_email_steps",
      "attributes": {
        ...
      },
      "relationships": {
        "campaign": {
          "data": {
            "id": "1961",
            "type": "campaigns"
          }
        }
      }
    }
  ],
  "links": {
    "self": "https://prospect.io/api/public/v1/campaigns/1/steps?page%5Bnumber%5D=1&page%5Bsize%5D=100",
    "next": "https://prospect.io/api/public/v1/campaigns/1/steps?page%5Bnumber%5D=2&page%5Bsize%5D=100",
    "last": "https://prospect.io/api/public/v1/campaigns/1/steps?page%5Bnumber%5D=5&page%5Bsize%5D=100"
  }
}
```

Returns a list of campaigns steps.

This list is [paginate](#pagination) by 100 records and can also be [sorted](#sorting).
