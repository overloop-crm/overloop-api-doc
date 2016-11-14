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
      "created_at": "2015-08-15T14:48:46.000Z",
      "updated_at": "2016-11-11T10:54:51.000Z"
    }
  }
}
```

### Object attributes
Attribute | Description
--------- | -----------
id | **integer** <br />A unique identifier for the user
name | **string** <br />The user's name
email | **string** <br />The user's email address
role | **string** <br />The user's role. Can be `admin` or `user`
phone_number | **string** <br />The user's phone number
skype | **string** <br />The user's Skype username
signature | **string** <br />The user's HTML signature
disabled | **boolean** <br />Whether or not the user is disabled or not
from_name | **string** <br />The name we put in the email `from` field
timezone | **string** <br />The user's time zone
created_at | **datetime**
updated_at | **datetime**

## Retrieve a user
```shell
# DEFINITION
GET https://prospect.io/api/public/v1/users/{USER_ID}

# EXAMPLE
curl -X GET "https://prospect.io/api/public/v1/users/1" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

### Parameters
Parameter | Description
--------- | -----------
id<br />**required** - *integer* | The ID of the user to retrieve

### Returns
Returns the [user object](#the-user-object).

## List users
```shell
# DEFINITION
GET https://prospect.io/api/public/v1/users

# EXAMPLE
curl -X GET "https://prospect.io/api/public/v1/users" \
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
    "self": "https://prospect.io/api/public/v1/users?page%5Bnumber%5D=1&page%5Bsize%5D=100",
    "next": "https://prospect.io/api/public/v1/users?page%5Bnumber%5D=2&page%5Bsize%5D=100",
    "last": "https://prospect.io/api/public/v1/users?page%5Bnumber%5D=5&page%5Bsize%5D=100"
  }
}
```

Returns a list of campaigns steps.

This list is [paginate](#pagination) by 100 records and can also be [sorted](#sorting).
