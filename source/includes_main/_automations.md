# Automations
## The automation object
```
# EXAMPLE OBJECT
```

```json
{
  "data": {
    "id": "1",
    "type": "automations",
    "attributes": {
      "name": "Public API Automation Example",
      "enter_triggers": [
        "prospect.create",
      ],
      "exit_triggers": [
        "prospect.replied",
        "prospect.qualified",
        "prospect.convert"
      ],
      "status": "on",
      "send_as_thread": true,
      "sending_days": [
        "monday",
        "tuesday",
        "wednesday",
        "thursday",
        "friday"
      ],
      "start_sending_minutes": 480,
      "end_sending_minutes": 1020,
      "timezone": "Etc/UTC",
      "created_at": "2020-01-31T12:00:00.000Z",
      "updated_at": "2020-01-31T12:00:00.000Z"
    },
    "relationships": {
      "steps": {
        "data": [
          {
            "id": "a-z0-9-abc1",
            "type": "automations_steps"
          },
          {
            "id": "a-z0-9-abc2",
            "type": "automations_steps"
          }
        ]
      },
      "segment": {
        "data": {
          "id": "a-z0-9-abc3",
          "type": "segments"
        }
      }
    }
  },
  "included": [
    {
      "id": "a-z0-9-abc3",
      "type": "segments",
      "attributes": {
        "name": null,
        "combination_operator": "and"
      },
      "relationships": {
        "filters": {
          "data": [
            {
              "id": "a-z0-9-abc4",
              "type": "filters"
            }
          ]
        }
      }
    },
    {
      "id": "a-z0-9-abc4",
      "type": "filters",
      "attributes": {
        "attribute_name": "email",
        "operator": "doesnotcontain",
        "option_value": "info"
      },
      "relationships": {
        "segment" : {
          "data": {
            "id": "a-z0-9-abc3",
            "type": "segments"
          }
        }
      }
    }
  ]
}
```

### Object attributes
Attribute | Filterable? | Description
--------- | ----------- | -----------
id | no | **integer** <br />A unique identifier for the automation
name | no | **string** <br />The automation's name
enter_triggers | no | **array** <br />An array containing the events that will make prospects entering the automation. Possible values are `message.sent`, `message.open`, `message.click`, `prospect.create`, `prospect.updated`, `prospect.replied`, `prospect.qualified` and `prospect.convert`
exit_triggers | no | **array** <br />An array containing the events that will make prospects exiting the automation. Possible values are `message.click`, `prospect.replied`, `prospect.qualified`, `prospect.convert`, `message.hard_bounced` and `pseudo_event.unmatch` representing the event when the conditions of the _enter_segment_ event is no longer applicable.
status | **yes** | **string** <br />The automation's status that can take 2 different values: `on` and `off`
send_as_thread | no | **boolean** <br />The automation's emails should be sent as threads.
sending_days | no | **array** <br />An array containing days during which emails can be sent ("monday", "tuesday", etc.)
start_sending_minutes | no | **integer** <br />The hour at which we can start sending emails, between 00:00 and 23:45 with 15 minutes intervals. Value is in minutes between `0` and `1425`.
end_sending_minutes | no | **integer** <br />The hour at which we can stop sending emails, between 00:00 and 23:45 with 15 minutes intervals. Value is in minutes between `0` and `1425`.
created_at | no | **datetime** <br />ISO 8601 format with timezone offset
updated_at | no | **datetime** <br />ISO 8601 format with timezone offset

### Relationships
Object | Description
--------- | -----------
steps | The [steps](#automation-steps) of the automation.
enter_segment | The reference of the automation filters for the _enter_segment_ trigger event.
filters | The conditions of the _enter_segment_ trigger event.

## Retrieve an automation
```shell
# DEFINITION
GET https://api.prospect.io/public/v1/automations/{AUTOMATION_ID}

# EXAMPLE
curl -X GET "https://api.prospect.io/public/v1/automations/1" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

### Parameters
Parameter | Description
--------- | -----------
id<br />**required** - *integer* | The ID of the automation to retrieve

### Returns
Returns the [automation object](#the-automation-object).

## List automations
```shell
# DEFINITION
GET https://api.prospect.io/public/v1/automations

# EXAMPLE
curl -X GET "https://api.prospect.io/public/v1/automations" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": "1",
      "type": "automations",
      "attributes": {
        ...
      },
      "relationships": {
        "steps": {
          "data": [
            ...
          ]
        },
        "segment": {
          "data": {
            ...
          }
        }
      }
    },
    {
      "id": "2",
      "type": "automations",
      "attributes": {
        ...
      },
      "relationships": {
        "steps": {
          "data": [
            ...
          ]
        },
        "segment": {
          "data": {
            ...
          }
        }
      }
    }
  ],
  "links": {
    "self": "https://api.prospect.io/public/v1/automations/?page%5Bnumber%5D=1&page%5Bsize%5D=100",
    "next": "https://api.prospect.io/public/v1/automations/?page%5Bnumber%5D=2&page%5Bsize%5D=100",
    "last": "https://api.prospect.io/public/v1/automations/?page%5Bnumber%5D=5&page%5Bsize%5D=100"
  }
}
```

Returns a list of automations.

This list is [paginated](#pagination) by 100 records and can also be [sorted](#sorting) or [filtered](#filtering).
