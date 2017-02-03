# Emails Search API
The Emails Search API lets you find email addresses associated with a company or a domain name.

## The search result object
```
# EXAMPLE OBJECT
```

```json
{
  "data": [
    {
      "id": "72947",
      "type": "emails",
      "attributes": {
        "value": "vincenzo@prospect.io",
        "type": "personal",
        "confidence": "98",
        "first_name": "Vincenzo",
        "last_name": "Ruggiero",
        "job_title": "Founder, CEO",
        "job_title": "Prospect.io",
        "phone": "555-12545474",
        "twitter": "VincenzoR",
        "linkedin_url": "https://www.linkedin.com/in/vincenzor",
        "angellist_url": "https://angel.co/vincenzo",
      },
      "relationships": {
        "domain": {
          "data": {
            "id": "1",
            "type": "domains"
          }
        }
      }
    }
  ],
  "included": [
    {
      "id": "1",
      "type": "domains",
      "attributes": {
        "name": "prospect.io",
        "pattern": "{first}",
        "company_name": "Prospect.io"
      }
    }
  ]
}
```

### Search result object attributes
Attribute | Description
--------- | -----------
id | **integer** <br />A unique identifier for the email
value | **string** <br />The email address
type | **string** <br />Can be `personal` for personal email addresses or `generic` for email addresses like `support@` or `contact@`
confidence | **integer** <br />Our estimation between 0 and 100 of the probability the email address returned is correct. It depends on several criteria such as the number and quality of sources
first_name | **string** <br />First name of the person
last_name | **string** <br />Last name of the person
job_title | **string** <br />Job title of the person
company | **string** <br />Company name of the person
phone | **string** <br />Phone number of the person
twitter | **string** <br />Twitter handle of the person
linkedin_url | **string** <br />Full LinkedIn profile URL of the person
angellist_url | **string** <br />Full AngelList profile URL of the person

### Relationships
Object | Description
--------- | -----------
domain | The domain (company) information

### Domain object attributes
Attribute | Description
--------- | -----------
id | **integer** <br />A unique identifier for the domain
name | **string** <br />The domain name
pattern | **string** <br />The pattern used in this companies for emails. Common values are: `{first}`, `{first}.{last}`, `{f}.{last}`, ...
company_name | **string** <br />Name of the company associated to the domain name

## Search for emails
```shell
# DEFINITION
GET https://prospect.io/api/public/v1/emails/search?domain={{DOMAIN}}&first_name={{FIRST_NAME}}&last_name={{LAST_NAME}}

# EXAMPLE
curl -X GET "https://prospect.io/api/public/v1/emails/search?domain=prospect.io&first_name=Vincenzo&last_name=Ruggiero" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

Only responses containing at least 1 email address go against your quota.

### Parameters
Parameter | Description
--------- | -----------
domain<br />**required** - *string* | Domain name from which you want to find the email addresses. For example, "prospect.io".
first_name<br />*string* | The person's first name
last_name<br />*string* | The person's last name
type<br />*string* | Only return emails of this type. Possible values are `personal` or `generic`.

### Returns
Returns the [email search object](#the-email-search-object).
