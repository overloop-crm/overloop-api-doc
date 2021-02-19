# Verify
The Emails Verify API lets you check in real time the deliverability (how likely it is to bounce or not from the mail server) of any email address without sending an email.

## The verify result object
```
# EXAMPLE OBJECT
```

```json
{
  "data": [],
  "meta": {
    "email": "vincenzo@prospect.io",
    "score": 84,
    "disposable": false,
    "role_address": false,
    "error_code": null
  }
}
```

### Verify result object attributes
Attribute | Description
--------- | -----------
email | **string** <br />The email address verified
score | **integer** <br />The validity score of this email. A value of 100 means we highly trust this email to be valid. A value of 0 indicates that we don't think the email is valid. 


## Verify an email
```shell
# DEFINITION
GET https://api.prospect.io/public/v1/emails/verify?email={{EMAIL_ADDRESS}}

# EXAMPLE
curl -X GET "https://api.prospect.io/public/v1/emails/verify?email=vincenzo@prospect.io" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

Every call will go against your quota and will cost you **1 credit**.

### Parameters
Parameter | Description
--------- | -----------
email<br />**required** - *string* | The email addresses to verify. For example, "vincenzo@prospect.io".

### Returns
Returns the [verify result object](#the-verify-result-object).
