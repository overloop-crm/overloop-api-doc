# Relationships
```shell
# EXAMPLE
GET https://api.overloop.com/public/v1/contacts?include=organization
```

> Get contacts with their associated organizations

Resources returned by the API are returned in the JSON API format, which means that related entities are 
linked using a "relationship" section in the JSON payloads. 
This section only contains the links between the unique identifier of related records (in the example, Contact#29964 and Organization#1). 

In order to get access to associated information on an entity, you can use the parameter `?include=`, which will create 
a new section "included" containing the full payload of all the associated data. Notice that you can include multiple 
relationships by joining them using a comma: `GET https://api.overloop.com/public/v1/contacts?include=organization,creator`

```shell
# RETURNS
{
    "data": {
        "id": "29964",
        "type": "contacts",
        "attributes": {
            …
        },
        "relationships": {
            "creator": {
                "data": {
                    "id": "181",
                    "type": "users"
                }
            },
            "owner": {
                "data": {
                    "id": "181",
                    "type": "users"
                }
            },
            "organization": {
                "data": {
                    "id": "1",
                    "type": "organizations"
                }
            }
        }
    },
    "included": [
        {
            "id": "1",
            "type": "organizations",
            "attributes": {
                "name": "Overloop",
                "created_at": "2020-11-06T13:56:44Z",
                "updated_at": "2020-11-06T13:56:44Z",
                "updater_id": 181,
                "creator_id": 181,
                "website": null,
                "phone": null,
                "email": null,
                "country": null,
                "city": null,
                "state": null,
                "address": null,
                "description": null,
                "lists": []
            }
        }
    ]
}
```
