# Stages
## The stage object
```
# EXAMPLE OBJECT
```

```json
{
  "data": {
    "id": "1",
    "type": "stages",
    "attributes": {
      "name": "Qualified",
      "position": 3,
      "created_at": "2015-08-15T16:48:46+02:00",
      "updated_at": "2016-11-25T12:40:46+01:00"
    }
  },
  "relationships": {
    "pipeline": {
      "data": {
        "id": "1",
        "type": "pipelines"
      }
    }
  }
}
```

### Object attributes
Attribute | Filterable? | Description
--------- | ----------- | -----------
id | no | **integer** <br />A unique identifier for the stage
name | no | **string** <br />The stage's name
probability | no | **number** <br />The stage's probability (use 10 for 10%)
position | no | **number** <br />The stage's position in pipeline (starts at 0)
rotting days | no | **number** <br />The number of days before considering a deal as "rotting"
created_at | no | **datetime** <br />ISO 8601 format with timezone offset
updated_at | no | **datetime** <br />ISO 8601 format with timezone offset


## Create a stage
```shell
# DEFINITION
POST https://api.overloop.com/public/v1/stages

# EXAMPLE
curl -X POST "https://api.overloop.com/public/v1/stages" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8" \
-d '{
  "data": {
    "type": "stages",
    "attributes": {
      "name": "A stage name",
      "probability": 33,
      "pipeline_id": 2
    }
  }
}'
```

This will create a new stage.

### Parameters
Parameter | Default | Description
--------- | ------- | ------------
name<br />**required** - *string* | / | The stage's name
probability<br />**required** - *string* | / | The stage's probability
pipeline_id<br />**required** - *string* | / | The stage's pipeline
rotting | / | The number of days before considering a deal as "rotting"
position | / | The position of the stage in the pipeline

### Returns
Returns the [stage object](#the-stage-object).

## Retrieve a stage
```shell
# DEFINITION
GET https://api.overloop.com/public/v1/stages/{STAGE_ID}

# EXAMPLE
curl -X GET "https://api.overloop.com/public/v1/stages/1" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

### Parameters
Parameter | Description
--------- | -----------
id<br />**required** - *integer* | The ID of the stage to retrieve

### Returns
Returns the [stage object](#the-stage-object).

## Update a stage
```shell
# DEFINITION
PATCH https://api.overloop.com/public/v1/stages/{STAGE_ID}

# EXAMPLE
curl -X PATCH "https://api.overloop.com/public/v1/stages/1" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8" \
-d '{
  "data": {
    "type": "stages",
    "attributes": {
      "name": "Qualified bis"
    }
  }
}'
```

Updates the specified stage by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

### Parameters
Parameter | Description
--------- | -----------
id<br />**required** - *integer* | The ID of the stage to update
probability | / | The stage's probability
rotting | / | The number of days before considering a deal as "rotting"
position | / | The position of the stage in the pipeline

### Returns
Returns the [stage object](#the-stage-object).

## Delete a stage
```shell
# DEFINITION
DELETE https://api.overloop.com/public/v1/stages/{PROSPECT_ID}

# EXAMPLE
curl -X DELETE "https://api.overloop.com/public/v1/stages/1" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "1",
    "type": "stages"
  }
}
```

Permanently deletes a stage. It cannot be undone.

<aside class="notice">
Warning — Deleting a stage will delete all the deals inside that stage
</aside>

### Parameters
Parameter | Required? | Type | Description
--------- | --------- | -----| -----------
id | **yes** | integer | The ID of the stage to delete

### Returns
Returns an object containing the stage ID.

## List stages

```shell
# DEFINITION
GET https://api.overloop.com/public/v1/stages

# EXAMPLE
curl -X GET "https://api.overloop.com/public/v1/stages" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": "1",
      "type": "stages",
      "attributes": {
        ...
      }
    },
    {
      "id": "2",
      "type": "stage",
      "attributes": {
        ...
      }
    }
  ],
  "links": {
    "self": "https://api.overloop.com/public/v1/stages/?page%5Bnumber%5D=1&page%5Bsize%5D=100",
    "next": "https://api.overloop.com/public/v1/stages/?page%5Bnumber%5D=2&page%5Bsize%5D=100",
    "last": "https://api.overloop.com/public/v1/stages/?page%5Bnumber%5D=5&page%5Bsize%5D=100"
  }
}
```

Returns a list of stages.

This stage is [paginated](#pagination) by 100 records and can also be [sorted](#sorting) or [filtered](#filtering).
