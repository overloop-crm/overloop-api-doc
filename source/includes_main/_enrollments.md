# Enrollments
## The enrollment object
To add a desired prospect to a specific automation you have to create an **enrollment**. The enrollment is then used to describe the progression of the prospect into the automation flow.

```
# EXAMPLE OBJECT
```
```json
{
  "data": {
    "id": "1",
    "type": "automations_enrollments",
    "attributes": {
      "automation_id": 1,
      "prospect_id": 1,
      "disenrolled_at": null,
      "created_at": "2020-01-31T12:00:00.000Z",
      "updated_at": "2020-01-31T12:00:00.000Z"
    },
    "relationships": {
      "current_step": {
        "data": {
          "id": "a-z0-9-abc1",
          "type": "automations_steps"
        }
      }
    },
    "included": [
      {
        "id": "a-z0-9-abc1",
        "type": "automations_steps",
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
}
```

### Object attributes
Attribute | Description
--------- | -----------
id | **integer** <br />A unique identifier for the enrollment
automation_id | **integer** <br />The automation's ID this enrollment is associated to
prospect_id | **integer** <br />The prospect's ID this enrollment is associated to
disenrolled_at | **datetime** <br />The date and time when the prospect has been leaved the automation in ISO 8601 format with timezone
created_at | **datetime** <br />ISO 8601 format with timezone offset
updated_at | **datetime** <br />ISO 8601 format with timezone offset

### Relationships
Object | Description
--------- | -----------
current_step | The current [step](#automation-steps) of this enrollment.

## Create an enrollment
```shell
# DEFINITION
POST https://api.prospect.io/public/v1/automations/{{AUTOMATION_ID}}/enrollments

# EXAMPLE
curl -X POST "https://api.prospect.io/public/v1/automations/1/enrollments" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8" \
-d '{
  "data": {
    "type": "enrollments",
    "attributes": {
      "prospect_id": 1,
      "step_id": "abc123",
      "reenroll": false,
      "include": "current_step"
    }
  }
}'
```

This will create a new enrollment.

### Parameters
Parameter | Required? | Type | Description
--------- | --------- | ---- | ------------
prospect_id | **yes** | *integer* | The prospect's ID
step_id | no | *string* | The step's ID of the automation at which the prospect must be enrolled.
reenroll | no | *boolean* | Set to `false` if you want to prevent re enroll the prospect because he already has been enrolled. **If not set to** `false` **this parameter will always be** `true`
include | no | *string* | Set to `current_step` if you want to have the related step included with the returned result.

### Returns
Returns the [enrollment object](#the-enrollment-object).

## Retrieve an enrollment
```shell
# DEFINITION
GET https://api.prospect.io/public/v1/automations/{{AUTOMATION_ID}}/enrollments/{{ENROLLMENT_ID}}

# EXAMPLE
curl -X GET "https://api.prospect.io/public/v1/automations/1/enrollments/1" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

### Parameters
Parameter | Required? | Type | Description
--------- | --------- | -----| -----------
id | **yes** | *integer* | The ID of the enrollment to retrieve

### Returns
Returns the [enrollment object](#the-enrollment-object).
