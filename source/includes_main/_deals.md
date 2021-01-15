# Deals
## The deal object
```
# EXAMPLE OBJECT
```

```json
{
  "data": {
    "id": "1",
    "type": "deals",
    "attributes": {
      "title": "3 licences for Apple INC",
      "value": "123456",
      "status": "won",
      "closed_at": "2015-08-15T16:48:46+02:00",
      "expected_close_date": "2015-09-15T16:48:46+02:00",
      "entered_stage_at": "2015-08-15T16:48:46+02:00",
      "c_custom_field_a": "Hot lead",
      "created_from": "web",
      "created_at": "2015-08-15T16:48:46+02:00",
      "updated_at": "2016-11-25T12:40:46+01:00"
    }
  },
  "relationships": {
    "creator": {
      "data": {
        "id": "1",
        "type": "users"
      }
    },
    "updater": {
      "data": {
        "id": "1",
        "type": "users"
      }
    },
    "owner": {
      "data": {
        "id": "2",
        "type": "users"
      }
    },
    "organization": {
      "data": {
        "id": "2",
        "type": "organizations"
      }
    },
    "prospect": {
      "data": {
        "id": "4",
        "type": "prospects"
      }
    },
    "stage": {
      "data": {
        "id": "9b13c0d1-a306-4f39-b851-dbddbbdde381",
        "type": "stages"
      }
    }
  }
}
```

### Object attributes
Attribute | Filterable? | Description
--------- | ---------- | -----------
id | **yes** | **integer** <br />A unique identifier for the deal
title | **yes** | **string** <br />The name of the deal
value | **yes** | **decimal** <br />The value of the deal
status | **yes** | **string** <br />The deal's status (won, lost or open) 
closed_at | no | **datetime** <br />ISO 8601 format of the moment when the deal was closed
expected_close_date | no | **datetime** <br />ISO 8601 format of the moment we expect the deal to close
entered_stage_at | no | **datetime** <br />ISO 8601 format of the last moment stage changed
created_at | no | **datetime** <br />ISO 8601 format of the moment the deal has been created
updated_at | no | **datetime** <br />ISO 8601 format of the moment the deal has been updated


### Custom Fields

Custom fields can be used as normal attributes by using their `identifier` as attribute key, see the `c_custom_field_a` example in the above payload.

You can retrieve the list of your custom fields by using the [custom fields index endpoint](#list-custom-fields).

They accept a value depending on [their format](#the-custom-field-object)

### Relationships
Object | Description
--------- | -----------
creator | The [user](#users) who created the deal
updater | The [user](#users) who updated the deal
owner | The [user](#users) responsible of the deal
prospect | The [prospect](#prospects) of this deal
organization | The [organization](#organizations) of this deal
stage | The [stage](#stages) of this deal


## Create a deal
```shell
# DEFINITION
POST https://api.deal.io/public/v1/deals

# EXAMPLE
curl -X POST "https://api.deal.io/public/v1/deals" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8" \
-d '{
  "data": {
    "type": "deals",
    "attributes": {
      "title": "16 licenses for ACME corp",
      "c_custom_field_a": "Hot lead"
    }
  }
}'
```

This will create a new deal. 

### Parameters

Attribute | Filterable? | Description
--------- | ---------- | -----------
id | *NULL* | A unique identifier for the deal
stage_id<br />**required** - *integer* | *NULL* | The stage of the deal
title | *NULL* | The name of the deal
value | *NULL* | The value of the deal
status | *NULL* | The deal's status (won, lost or open) 
closed_at | *NULL* | ISO 8601 format of the moment when the deal was closed
expected_close_date | *NULL* | ISO 8601 format of the moment we expect the deal to close
entered_stage_at | *NULL* | ISO 8601 format of the last moment stage changed
created_at | *NULL* | ISO 8601 format of the moment the deal has been created
updated_at | *NULL* | ISO 8601 format of the moment the deal has been updated



### Returns
Returns the [deal object](#the-deal-object).

## Retrieve a deal
```shell
# DEFINITION
GET https://api.deal.io/public/v1/deals/{DEAL_ID}

# EXAMPLE
curl -X GET "https://api.deal.io/public/v1/deals/1" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

### Parameters
Parameter | Description
--------- | -----------
id<br />**required** - *integer* | The ID of the deal to retrieve

### Returns
Returns the [deal object](#the-deal-object).

## Update a deal
```shell
# DEFINITION
PATCH https://api.deal.io/public/v1/deals/{DEAL_ID}

# EXAMPLE
curl -X PATCH "https://api.deal.io/public/v1/deals/1" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8" \
-d '{
  "data": {
    "type": "deals",
    "attributes": {
      "title": "4 licenses for ACME Corp", 
      "c_custom_field_a": "Hot lead"
    }
  }
}'
```

Updates the specified deal by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

### Parameters
Parameter | Description
--------- | -----------
id<br />**required** - *integer* | A unique identifier for the deal
title | The name of the deal
value | The value of the deal
status | The deal's status (won, lost or open) 
closed_at | ISO 8601 format of the moment when the deal was closed
expected_close_date | ISO 8601 format of the moment we expect the deal to close
entered_stage_at | ISO 8601 format of the last moment stage changed
created_at | ISO 8601 format of the moment the deal has been created
updated_at | ISO 8601 format of the moment the deal has been updated


### Returns
Returns the [deal object](#the-deal-object).

## Delete a deal
```shell
# DEFINITION
DELETE https://api.deal.io/public/v1/deals/{DEAL_ID}

# EXAMPLE
curl -X DELETE "https://api.deal.io/public/v1/deals/1" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "1",
    "type": "deals"
  }
}
```

Permanently deletes a deal. It cannot be undone.


### Parameters
Parameter | Required? | Type | Description
--------- | --------- | -----| -----------
id | **yes** | integer | The ID of the deal to delete

### Returns
Returns an object containing the deal ID.

## List deals

```shell
# DEFINITION
GET https://api.deal.io/public/v1/deals

# EXAMPLE
curl -X GET "https://api.deal.io/public/v1/deals" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": "1",
      "type": "deals",
      "attributes": {
        ...
      },
      "relationships": {
        "owner": {
          "data": {
            ...
          }
        }
      }
    },
    {
      "id": "2",
      "type": "deals",
      "attributes": {
        ...
      },
      "relationships": {
        "owner": {
          "data": {
            ...
          }
        }
      }
    }
  ],
  "links": {
    "self": "https://api.deal.io/public/v1/deals/?page%5Bnumber%5D=1&page%5Bsize%5D=100",
    "next": "https://api.deal.io/public/v1/deals/?page%5Bnumber%5D=2&page%5Bsize%5D=100",
    "last": "https://api.deal.io/public/v1/deals/?page%5Bnumber%5D=5&page%5Bsize%5D=100"
  }
}
```

Returns a list of deals.

This list is [paginated](#pagination) by 100 records. It can also be [sorted](#sorting) or [filtered](#filtering).


## Mark as won
```shell
# DEFINITION: Mark as won
POST https://api.prospect.io/public/v1/deals/{DEAL_ID}/mark_as_won

# EXAMPLE
curl -X POST "https://api.prospect.io/public/v1/deals/1/mark_as_won" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"

# DEFINITION: Mark as not won
DELETE https://api.prospect.io/public/v1/deals/{DEAL_ID}/mark_as_won

# EXAMPLE
curl -X DELETE "https://api.prospect.io/public/v1/deals/1/mark_as_won" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

Mark a deal as won or not.

### Parameters
Parameter | Required? | Type | Description
--------- | --------- | -----| -----------
id | **yes** | integer | The ID of the deal to mark as (not) won

### Returns
Returns the [deal object](#the-deal-object).


## Mark as lost
```shell
# DEFINITION: Mark as lost
POST https://api.prospect.io/public/v1/deals/{DEAL_ID}/mark_as_lost

# EXAMPLE
curl -X POST "https://api.prospect.io/public/v1/deals/1/mark_as_lost" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"

# DEFINITION: Mark as not lost
DELETE https://api.prospect.io/public/v1/deals/{DEAL_ID}/mark_as_lost

# EXAMPLE
curl -X DELETE "https://api.prospect.io/public/v1/deals/1/mark_as_lost" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

Mark a deal as lost or not.

### Parameters
Parameter | Required? | Type | Description
--------- | --------- | -----| -----------
id | **yes** | integer | The ID of the deal to mark as (not) lost

### Returns
Returns the [deal object](#the-deal-object).
