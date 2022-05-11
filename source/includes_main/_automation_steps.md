# Automation Steps
## The automation step object
```
# EXAMPLE OBJECT
```

```json
{
  "data": [
    {
      "id": "a-z0-9-abc1",
      "type": "automations_steps",
      "attributes": {
        "step_type": "task",
        "position": 0,
        "previous_step_id" : null,
        "created_at": "2020-01-31T12:00:00.000Z",
        "updated_at": "2020-01-31T12:00:00.000Z",
        "config": {
          "title": "Public API Automation Step Example",
          "due_time": "09:00:00",
          "due_offset": 1,
          "description": "This is an example description",
          "task_category": null,
          "contact_segment": null,
          "wait_for_completion": true
        }
      },
      "relationships": {
        "automation": {
          "data": {
            "id": "1",
            "type": "automations"
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
id | **integer** <br />A unique identifier for the automation step
step_type | **string** <br />The type of step. Possible values depend on the automation type.
position | **integer** <br />When the previous_step is not a `condition`, the position will always be 0. Otherwise, `0` is the left/yes branch of a condition, while `1` is the right/no branch
previous_step_id | **string** <br />The unique identifier of the previous step. A `null` value will always be assigned to the first step of the automation
created_at | **datetime** <br />ISO 8601 format with timezone offset
updated_at | **datetime** <br />ISO 8601 format with timezone offset
config | **object** <br />All specific attributes related to the _step_type_

### Relationships
Object | Description
--------- | -----------
automation | The parent [automation](#automations)

## Retrieve a automation step
```shell
# DEFINITION
GET https://api.overloop.com/public/v1/automations/{AUTOMATION_ID}/steps/{STEP_ID}

# EXAMPLE
curl -X GET "https://api.overloop.com/public/v1/automations/1/steps/1" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

### Parameters
Parameter | Description
--------- | -----------
automation_id<br />**required** - *integer* | The ID of the automation
id<br />**required** - *integer* | The ID of the automation step to retrieve

### Returns
Returns the [automation step object](#the-automation-step-object).

## List automation steps
```shell
# DEFINITION
GET https://api.overloop.com/public/v1/automations/{AUTOMATION_ID}/steps

# EXAMPLE
curl -X GET "https://api.overloop.com/public/v1/automations/1/steps" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": "a-z0-9-abc1",
      "type": "automations_steps",
      "attributes": {
        ...
      },
      "relationships": {
        "automation": {
          "data": {
            "id": "1",
            "type": "automations"
          }
        }
      }
    },
    {
      "id": "a-z0-9-abc2",
      "type": "automations_steps",
      "attributes": {
        ...
      },
      "relationships": {
        "automation": {
          "data": {
            "id": "1",
            "type": "automations"
          }
        }
      }
    },
    {
      "id": "a-z0-9-abc3",
      "type": "automations_steps",
      "attributes": {
        ...
      },
      "relationships": {
        "automation": {
          "data": {
            "id": "1",
            "type": "automations"
          }
        }
      }
    }
  ],
  "links": {
    "self": "https://api.overloop.com/public/v1/automations/1/steps?page%5Bnumber%5D=1&page%5Bsize%5D=100",
    "next": "https://api.overloop.com/public/v1/automations/1/steps?page%5Bnumber%5D=2&page%5Bsize%5D=100",
    "last": "https://api.overloop.com/public/v1/automations/1/steps?page%5Bnumber%5D=5&page%5Bsize%5D=100"
  }
}
```

Returns a list of automation steps.

This list is [paginated](#pagination) by 100 records and can also be [sorted](#sorting).
