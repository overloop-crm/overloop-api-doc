# Enrollments
## The enrollment object
To add a desired prospect to a specific automation you have to create an **enrollment**. The enrollment is then used to describe the current status of the automation for the prospect.

```
# EXAMPLE OBJECT
```
```json
{
  "data": {
    "id": "1",
    "type": "automations-enrollments",
    "attributes": {
      "automation_id": 1,
      "prospect_id": 1,
      "current_stay_id": 1,
      "disenrolled_at": null,
      "created_at": "2020-01-01T12:00:00.000Z",
      "updated_at": "2020-01-01T12:00:00.000Z"
    }
  }
}
```

### Object attributes
Attribute | Description
--------- | -----------
id | **integer** <br />A unique identifier for the enrollment
automation_id | **integer** <br />The automation's ID this enrollment is associated to
prospect_id | **integer** <br />The prospect's ID this enrollment is associated to
current_stay_id | **integer** <br />Define the last stay
disenrolled_at | **datetime** <br />The date and time when the prospect has been leaved the automation in ISO 8601 format with timezone
created_at | **datetime** | ISO 8601 format with timezone offset
updated_at | **datetime** | ISO 8601 format with timezone offset


## Create an enrollment
```shell
# DEFINITION
POST https://api.prospect.io/public/v1/automations/{{AUTOMATION_ID}}/enrollments

# EXAMPLE
curl -X POST "https://api.prospect.io/public/v1/automations/1/subscriptions" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8" \
-d '{
  "data": {
    "type": "enrollments",
    "attributes": {
      "prospect_id": 1,
      "node_id": "123",
      "reenroll": false
    }
  }
}'
```

This will create a new enrollment.

### Parameters
Parameter | Required? | Type | Description
--------- | --------- | ---- | ------------
prospect_id | **yes** | *integer* | The prospect's ID
node_id | no | *string* | The step's ID of the automation at which the prospect must be enrolled.
reenroll | no | *boolean* | Set to `false` if you want to prevent re enroll the prospect because he already has been enrolled. **If not set to** `false` **this parameter will always be** `true`

### Returns
Returns the [enrollment object](#the-enrollment-object).
