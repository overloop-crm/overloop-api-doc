# Enrollments
## The enrollment object
To add a desired prospect/organization/deal to a specific workflow you have to create an **enrollment**. The enrollment is then used to describe the progression of the record into the workflow.

```
# EXAMPLE OBJECT
```
```json
{
  "data": {
    "id": "1",
    "type": "workflows_enrollments",
    "attributes": {
      "workflow_id": 1,
      "prospect_id":30332,
      "deal_id":null,
      "organization_id":null,
      "disenrolled_at": null,
      "start_at": "2020-08-20T08:00:00+02:00",
      "throttled": null,
      "created_at": "2020-08-13T10:12:23+02:00",
      "updated_at": "2020-08-13T10:12:23+02:00"
    },
    "relationships": {
      "current_step": {
        "data": {
          "id": "a-z0-9-abc1",
          "type": "workflows_steps"
        }
      },
      "automation": {
        "data": {
          "id": "374",
          "type": "automations"
        }
      },
      "record":{
        "data":{
          "id":"30332",
          "type":"prospects"
        }
      },
      "prospect": {
        "data": {
          "id": "30332",
          "type": "prospects"
        }
      },
      "organization": {
        "data": null
      },
      "deal": {
        "data": null
      }
    },
    "included": [
      {
        "id": "a-z0-9-abc1",
        "type": "workflows_steps",
        "attributes": {
          "step_type": "note",
          "position": 0,
          "previous_step_id": null,
          "created_at": "2020-01-31T12:00:00.000Z",
          "updated_at": "2020-01-31T12:00:00.000Z",
          "config": {
            "content": "Sample note text"
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
}
```

### Object attributes
Attribute | Description
--------- | -----------
id | **integer** <br />A unique identifier for the enrollment
record_id | **integer** <br />The unique identifier of the enrolled record
record_type | **string** <br />The type of the enrolled record (organizations, deals or prospects)
disenrolled_at | **datetime** <br />The date and time when the record has been leaved the workflow in ISO 8601 format with timezone
start_at | **datetime** <br />The date and time on which the enrollment must be started in ISO 8601 format with timezone offset. If not set or set in the past, the enrollment starts immediately.
throttled | **boolean** <br />If the enrollment start is being throttled.
created_at | **datetime** <br />ISO 8601 format with timezone offset
updated_at | **datetime** <br />ISO 8601 format with timezone offset

### Relationships
Object | Description
--------- | -----------
current_step | The current [step](#workflow-steps) of this enrollment.
workflow | The current [workflow](#workflows) of this enrollment.
prospect | The current [prospect](#prospects) of this enrollment (for prospect-based workflows).
organization | The current [organization](#organizations) of this enrollment (for organization-based workflows).
deal | The current [deal](#deals) of this enrollment (for deal-based workflows).

## Create an enrollment
```shell
# DEFINITION
POST https://api.prospect.io/public/v1/workflows/{{WORKFLOW_ID}}/enrollments

# EXAMPLE
curl -X POST "https://api.prospect.io/public/v1/workflows/1/enrollments" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8" \
-d '{
  "data": {
    "type": "enrollments",
    "attributes": {
      "prospect_id": 1,
      "step_id": "abc123",
      "reenroll": false,
      "start_at": "2020-08-20T08:00:00+02:00",
      "include": "current_step"
    }
  }
}'
```

This will create a new enrollment.

### Parameters
Parameter | Required? | Type | Description
--------- | --------- | ---- | ------------
prospect_id | **yes** | *integer* | The prospect's ID (required only for prospect-based workflows)
organization_id | **yes** | *integer* | The organization's ID (required only for organization-based workflows)
deal_id | **yes** | *integer* | The deal's ID (required only for deal-based workflows)
step_id | no | *string* | The step's ID of the workflow at which the prospect must be enrolled.
reenroll | no | *boolean* | Set to `false` if you want to prevent re enroll the prospect because he already has been enrolled. **If not set to** `false` **this parameter will always be** `true`
start_at | no | *string* | The date and time on which the enrollment must be started in the ISO 8601 format with timezone offset. If not set or set in the past, the enrollment will start immediately.

### Returns
Returns the [enrollment object](#the-enrollment-object).

## Stop an enrollment
```shell
# DEFINITION
DELETE https://api.prospect.io/public/v1/workflows/{{WORKFLOW_ID}}/enrollments/{{ENROLLMENT_ID}}

# EXAMPLE
curl -X DELETE "https://api.prospect.io/public/v1/workflows/1/enrollments/1" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

This will stop an enrollment.

### Parameters
Parameter | Required? | Type | Description
--------- | --------- | -----| -----------
id | **yes** | integer | The ID of the enrollment to stop

### Returns
Returns the [enrollment object](#the-enrollment-object).

## Retrieve an enrollment
```shell
# DEFINITION
GET https://api.prospect.io/public/v1/workflows/{{WORKFLOW_ID}}/enrollments/{{ENROLLMENT_ID}}

# EXAMPLE
curl -X GET "https://api.prospect.io/public/v1/workflows/1/enrollments/1" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

### Parameters
Parameter | Required? | Type | Description
--------- | --------- | -----| -----------
id | **yes** | *integer* | The ID of the enrollment to retrieve

### Returns
Returns the [enrollment object](#the-enrollment-object).


## List enrollments
```shell
# DEFINITION
GET https://api.prospect.io/public/v1/enrollments

# EXAMPLE
curl -X GET "https://api.prospect.io/public/v1/enrollments" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": "36",
      "type": "workflows_enrollments",
      "attributes": {
        "disenrolled_at": "2020-06-03T13:01:15.697Z",
        "start_at": null,
        "created_at": "2020-03-10T13:35:21Z",
        "updated_at": "2020-09-30T08:02:51Z"
      },
      "relationships": {
        "prospect": {
          "data": {
            "id": "29646",
            "type": "prospects"
          }
        },
        "workflow": {
          "data": {
            "id": "3",
            "type": "workflows"
          }
        },
        "current_step": {
          "data": null
        }
      }
    }
  ],
  "links": {
    "self": "https://localhost:3000/api/public/v1/enrollments?filter=prospect_id%3A29646&page%5Bnumber%5D=1&page%5Bsize%5D=100",
    "first": "https://localhost:3000/api/public/v1/enrollments?filter=prospect_id%3A29646&page%5Bnumber%5D=1&page%5Bsize%5D=100",
    "prev": null,
    "next": null,
    "last": "https://localhost:3000/api/public/v1/enrollments?filter=prospect_id%3A29646&page%5Bnumber%5D=1&page%5Bsize%5D=100"
  }
}
```

Returns a list of enrollments.

This list is [paginated](#pagination) by 100 records and can also be [sorted](#sorting) or [filtered](#filtering).
