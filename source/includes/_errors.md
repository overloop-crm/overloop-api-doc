# Errors

```shell
# EXAMPLE OBJECT
## When trying to add a prospect with a duplicate email address
```

```json
{
  "errors": [
    {
      "source": {
        "pointer": "/data/attributes/email"
      },
      "detail": "has already been taken"
    }
  ]
}
```
```shell
## Error on authentication
```
```json
{
  "errors": [
    {
      "code": "unauthorized",
      "message": "Your API key is wrong. More information here https://apidoc.overloop.com/#authentication"
    }
  ]
}
```

Overloop uses conventional HTTP response codes to indicate success or failure of an API request. In general, codes in the 2xx range indicate success, codes in the 4xx range indicate an error that resulted from the provided information (e.g. a required parameter was missing, a prospect cannot be created, etc.), and codes in the 5xx range indicate an error with Overloop's servers.

Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request sucks
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- The resource requested is hidden for administrators only
404 | Not Found -- The specified resource could not be found
405 | Method Not Allowed -- You tried to access a resource with an invalid method
406 | Not Acceptable -- You requested a format that isn't json
410 | Gone -- The resource requested has been removed from our servers
410 | Gone -- The resource requested has been removed from our servers
500 | Unprocessable Entity -- You've provided invalid parameters with your request
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.
