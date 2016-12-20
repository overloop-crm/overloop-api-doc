# Account
## The account object
```
# EXAMPLE OBJECT
```

```json
{
  "data": {
    "id": "1",
    "type": "companies",
    "attributes": {
      "name": "Prospect.io",
      "website": "https://prospect.io",
      "phone_number": "",
      "billing_name": "Prospect.io SPRL",
      "address": "rue des Pères Blancs 4\r\n1040 Brussels",
      "country": "BE",
      "vat": "BE0645917753",
      "plan_name": "5K Credits",
      "plan_code": "monthly_credits_5k",
      "credits_per_month": 5000,
      "this_month_used_credits": 1608,
      "email_queries_used_this_period_count": 135,
      "messages_sent_this_period_count": 1473,
      "created_at": "2015-08-15T16:48:46+02:00",
      "updated_at": "2016-11-25T12:40:46+01:00"
    }
  }
}
```

### Object attributes
Attribute | Description
--------- | -----------
id | **integer** <br />A unique identifier for the account
name | **string** <br />The account's name
website | **string** <br />The account's website
phone_number | **string** <br />The account's phone number
billing_name | **string** <br />The account's billing name (the name that will appear on invoices)
address | **string** <br />The account's address
country | **string** <br />The account's country code (ISO)
vat | **string** <br />The account's VAT number
plan_name | **string** <br />The account's plan
plan_code | **string** <br />The account's plan code
credits_per_month | **integer** <br />The number of credits available per month
this_month_used_credits | **integer** <br />The number of total credits used on the current billing period
email_queries_used_this_period_count | **integer** <br />The number of total credits used for email queries on the current billing period
messages_sent_this_period_count | **integer** <br />The number of total credits used for sending messages on the current billing period
created_at | **datetime** | ISO 8601 format with timezone offset
updated_at | **datetime** | ISO 8601 format with timezone offset

## Retrieve your account
```shell
# DEFINITION
GET https://prospect.io/api/public/v1/account

# EXAMPLE
curl -X GET "https://prospect.io/api/public/v1/account" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

### Parameters
*none*

### Returns
Returns the [account object](#the-account-object).
