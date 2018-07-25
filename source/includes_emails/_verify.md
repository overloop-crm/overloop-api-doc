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
    "status": "valid",
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
status | **string** <br />The status of the email. Can be `valid`, `invalid`, `unknown` or `accept_all`.
disposable | **boolean** <br />Is the email a temporary or "disposable" email address
role_address | **boolean** <br />Is the email a "role" email address (like postmaster@, sales@, admin@, info@, webmaster@, etc. )
error_code | **string** <br />An error code if the email is invalid. Can be `email_address_invalid`, `email_domain_invalid` or `email_account_invalid`.

### Statuses

- **valid**: The email represents a real account / inbox available at the given domain
- **invalid**: Not a real email
- **unknown**: For some reason we cannot verify valid or invalid. Most of the time a domain did not respond quickly enough.
- **accept_all**: These are domains that respond to every verification request in the affirmative, and therefore cannot be fully verified.

### Error Codes

- **email_address_invalid**: The email address is not formatted correctly
- **email_domain_invalid**: The domain does not exist or is not capable of receiving email
- **email_account_invalid**: The email account does not exist on the domain



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
