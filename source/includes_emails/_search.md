# Search
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
        "company": "Prospect",
        "first_name": "Vincenzo",
        "last_name": "Ruggiero"
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
confidence | **integer** <br />Our estimation between 0 and 100 of the probability the email address returned is correct. It depends on several criteria such as the number and quality of sources
first_name | **string** <br />First name of the person
last_name | **string** <br />Last name of the person
company | **string** <br />Company name of the person

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
GET https://api.prospect.io/public/v1/emails/search?domain={{DOMAIN}}&first_name={{FIRST_NAME}}&last_name={{LAST_NAME}}

# EXAMPLE
curl -X GET "https://api.prospect.io/public/v1/emails/search?domain=prospect.io&first_name=Vincenzo&last_name=Ruggiero" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

Every call returning at least 1 email address go against your quota and will cost you **1 credit**.

### Parameters
Parameter | Description
--------- | -----------
domain<br />**required** - *string* | Domain name from which you want to find the email addresses. For example, "prospect.io".
first_name<br />*string* | The person's first name
last_name<br />*string* | The person's last name

### Returns
Returns the [email search object](#the-email-search-object).
