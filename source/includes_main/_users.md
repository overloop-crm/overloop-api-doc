# Users
## The user object
```
# EXAMPLE OBJECT
```

```json
{
  "data": {
    "id": "11",
    "type": "users",
    "attributes": {
      "name": "Vincenzo Ruggiero",
      "email": "vincenzo@prospect.io",
      "role": "admin",
      "phone_number": "",
      "skype": "ruggiero.vincenzo",
      "signature": "<p class=\"p1\"><span class=\"s1\">--&nbsp;<br /></span><span class=\"s1\"><strong>Vincenzo Ruggiero<br /></strong></span><span class=\"s1\">Founder<br /></span><span class=\"s2\"><a href=\"https://prospect.io/\"><strong>Prospect.io</strong><br /></a></span><span class=\"s2\"><a href=\"mailto:vincenzo@prospect.io\">vincenzo@prospect.io</a></span></p>",
      "disabled": false,
      "from_name": "Vincenzo Ruggiero",
      "timezone": "Brussels",
      "created_at": "2015-08-15T16:48:46+02:00",
      "updated_at": "2016-11-25T12:40:46+01:00"
    },
    "relationships": {
      "company": {
        "data": {
          "id": "5",
          "type": "companies"
        }
      }
    }
  }
}
```

### Object attributes
Attribute | Filterable? | Description
--------- | ----------- | -----------
id | no | **integer** <br />A unique identifier for the user
name | no | **string** <br />The user's name
email | no | **string** <br />The user's email address
role | no | **string** <br />The user's role. Can be `admin` or `user`
phone_number | no | **string** <br />The user's phone number
skype | no | **string** <br />The user's Skype username
signature | no | **string** <br />The user's HTML signature
disabled | **yes** | **boolean** <br />Whether or not the user is disabled or not
from_name | no | **string** <br />The name we put in the email `from` field
timezone | no | **string** <br />The user's time zone
created_at | no | **datetime** <br />ISO 8601 format with timezone offset
updated_at | no | **datetime** <br />ISO 8601 format with timezone offset

### Relationships
Object | Description
--------- | -----------
company | The user's company


## Retrieve a user
```shell
# DEFINITION
GET https://api.prospect.io/public/v1/users/{USER_ID}

# EXAMPLE
curl -X GET "https://api.prospect.io/public/v1/users/1" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

### Parameters
Parameter | Description
--------- | -----------
id<br />**required** - *integer* | The ID of the user to retrieve

### Returns
Returns the [user object](#the-user-object).

## Me
```shell
# DEFINITION
GET https://api.prospect.io/public/v1/me

# EXAMPLE
curl -X GET "https://api.prospect.io/public/v1/me" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

You can call this endpoint to retrive **your personnal information**.

### Parameters
*none*

### Returns
Returns your [user object](#the-user-object).

## List users
```shell
# DEFINITION
GET https://api.prospect.io/public/v1/users

# EXAMPLE
curl -X GET "https://api.prospect.io/public/v1/users" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8" \
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": "11",
      "type": "users",
      "attributes": {
        ...
      }
    },
    {
      "id": "38",
      "type": "users",
      "attributes": {
        ...
      }
    },
  ],
  "links": {
    "self": "https://api.prospect.io/public/v1/users?page%5Bnumber%5D=1&page%5Bsize%5D=100",
    "next": "https://api.prospect.io/public/v1/users?page%5Bnumber%5D=2&page%5Bsize%5D=100",
    "last": "https://api.prospect.io/public/v1/users?page%5Bnumber%5D=5&page%5Bsize%5D=100"
  }
}
```

Returns a list of users.

This list is [paginated](#pagination) by 100 records and can also be [sorted](#sorting) or [filtered](#filtering).
