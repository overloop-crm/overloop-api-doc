# Workflow Steps
## The workflow step object
```
# EXAMPLE OBJECT
```

```json
{
  "data": [
    {
      "id": "a-z0-9-abc1",
      "type": "workflows_steps",
      "attributes": {
        "step_type": "task",
        "position": 0,
        "previous_step_id" : null,
        "created_at": "2020-01-31T12:00:00.000Z",
        "updated_at": "2020-01-31T12:00:00.000Z",
        "config": {
          "title": "Public API Workflow Step Example",
          "due_time": "09:00:00",
          "due_offset": 1,
          "description": "This is an example description",
          "task_category": null,
          "contact_segment": null,
          "wait_for_completion": true
        }
      },
      "relationships": {
        "workflow": {
          "data": {
            "id": "1",
            "type": "workflows"
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
id | **integer** <br />A unique identifier for the workflow step
step_type | **string** <br />The type of step. Possible values depend on the workflow type.
position | **integer** <br />When the previous_step is not a `condition`, the position will always be 0. Otherwise, `0` is the left/yes branch of a condition, while `1` is the right/no branch.
previous_step_id | **string** <br />The unique identifier of the previous step. A `null` value will always be assigned to the first step of the workflow.
created_at | **datetime** <br />ISO 8601 format with timezone offset
updated_at | **datetime** <br />ISO 8601 format with timezone offset
config | **object** <br />All specific attributes related to the _step_type_

### Relationships
Object | Description
--------- | -----------
workflow | The parent [workflow](#workflows)

## Retrieve a workflow step
```shell
# DEFINITION
GET https://api.overloop.com/public/v1/workflows/{WORKFLOW_ID}/steps/{STEP_ID}

# EXAMPLE
curl -X GET "https://api.overloop.com/public/v1/workflows/1/steps/1" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

### Parameters
Parameter | Description
--------- | -----------
workflow_id<br />**required** - *integer* | The ID of the workflow
id<br />**required** - *integer* | The ID of the workflow step to retrieve

### Returns
Returns the [workflow step object](#the-workflow-step-object).

## List workflows steps
```shell
# DEFINITION
GET https://api.overloop.com/public/v1/workflows/{WORKFLOW_ID}/steps

# EXAMPLE
curl -X GET "https://api.overloop.com/public/v1/workflows/1/steps" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": "a-z0-9-abc1",
      "type": "workflows_steps",
      "attributes": {
        ...
      },
      "relationships": {
        "workflow": {
          "data": {
            "id": "1",
            "type": "workflows"
          }
        }
      }
    },
    {
      "id": "a-z0-9-abc2",
      "type": "workflows_steps",
      "attributes": {
        ...
      },
      "relationships": {
        "workflow": {
          "data": {
            "id": "1",
            "type": "workflows"
          }
        }
      }
    },
    {
      "id": "a-z0-9-abc3",
      "type": "workflows_steps",
      "attributes": {
        ...
      },
      "relationships": {
        "workflow": {
          "data": {
            "id": "1",
            "type": "workflows"
          }
        }
      }
    }
  ],
  "links": {
    "self": "https://api.overloop.com/public/v1/workflows/1/steps?page%5Bnumber%5D=1&page%5Bsize%5D=100",
    "next": "https://api.overloop.com/public/v1/workflows/1/steps?page%5Bnumber%5D=2&page%5Bsize%5D=100",
    "last": "https://api.overloop.com/public/v1/workflows/1/steps?page%5Bnumber%5D=5&page%5Bsize%5D=100"
  }
}
```

Returns a list of workflows steps.

This list is [paginated](#pagination) by 100 records and can also be [sorted](#sorting).
