# Workflows
## The workflow object
```
# EXAMPLE OBJECT
```

```json
{
  "data": {
    "id": "1",
    "type": "workflows",
    "attributes": {
      "name": "Public API Workflow Example",
      "enter_triggers": [
        "contact.created",
      ],
      "enter_trigger_attributes": {},
      "exit_triggers": [
        "contact.replied"x
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
      "type": "contacts",
      "created_at": "2020-01-31T12:00:00.000Z",
      "updated_at": "2020-01-31T12:00:00.000Z"
    },
    "relationships": {
      "steps": {
        "data": [
          {
            "id": "a-z0-9-abc1",
            "type": "workflows_steps"
          },
          {
            "id": "a-z0-9-abc2",
            "type": "workflows_steps"
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
id | no | **integer** <br />A unique identifier for the workflow
name | no | **string** <br />The workflow's name
type | **yes** | **string** <br />The type of records that can be enrolled into the workflow, either `contacts`, `organizations` or `deals`
enter_triggers | no | **array** <br />An array containing the events that will make contacts entering the workflow. Possible values depends on the type.
enter_trigger_attributes | no | **json** <br />A json object containing additional information about the enter triggers settings. Its content varies depending on the selected enter triggers.
exit_triggers | no | **array** <br />An array containing the events that will make contacts exit the workflow. Possible values depends on the type.
status | **yes** | **string** <br />The workflow's status that can take 3 different values: `on`, `off`
send_as_thread | no | **boolean** <br />The workflow's emails should be sent as threads.
sending_days | no | **array** <br />An array containing days during which emails can be sent ("monday", "tuesday", etc.)
start_sending_minutes | no | **integer** <br />The hour at which we can start sending emails, between 00:00 and 23:45 with 15 minutes intervals. Value is in minutes between `0` and `1425`.
end_sending_minutes | no | **integer** <br />The hour at which we can stop sending emails, between 00:00 and 23:45 with 15 minutes intervals. Value is in minutes between `0` and `1425`.
created_at | no | **datetime** <br />ISO 8601 format with timezone offset
updated_at | no | **datetime** <br />ISO 8601 format with timezone offset

### Relationships
Object | Description
--------- | -----------
steps | The [steps](#workflow-steps) of the workflow.
enter_segment | The reference of the workflow filters for the _enter_segment_ trigger event.
filters | The conditions of the _enter_segment_ trigger event.

## Retrieve a workflow
```shell
# DEFINITION
GET https://api.overloop.com/public/v1/workflows/{WORKFLOW_ID}

# EXAMPLE
curl -X GET "https://api.overloop.com/public/v1/workflows/1" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

### Parameters
Parameter | Description
--------- | -----------
id<br />**required** - *integer* | The ID of the workflow to retrieve

### Returns
Returns the [workflow object](#the-workflow-object).

## List workflows
```shell
# DEFINITION
GET https://api.overloop.com/public/v1/workflows

# EXAMPLE
curl -X GET "https://api.overloop.com/public/v1/workflows" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": "1",
      "type": "workflows",
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
      "type": "workflows",
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
    "self": "https://api.overloop.com/public/v1/workflows/?page%5Bnumber%5D=1&page%5Bsize%5D=100",
    "next": "https://api.overloop.com/public/v1/workflows/?page%5Bnumber%5D=2&page%5Bsize%5D=100",
    "last": "https://api.overloop.com/public/v1/workflows/?page%5Bnumber%5D=5&page%5Bsize%5D=100"
  }
}
```

Returns a list of workflows.

This list is [paginated](#pagination) by 100 records and can also be [sorted](#sorting) or [filtered](#filtering).
