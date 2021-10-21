# Pipelines
## The pipeline object
```
# EXAMPLE OBJECT
```

```json
{
  "data": {
    "id": "1",
    "type": "pipelines",
    "attributes": {
      "name": "LinkedIn",
      "currency_code": "EUR",
      "created_at": "2015-08-15T16:48:46+02:00",
      "updated_at": "2016-11-25T12:40:46+01:00"
    }
  }
}
```

### Object attributes
Attribute | Filterable? | Description
--------- | ----------- | -----------
id | no | **integer** <br />A unique identifier for the pipeline
name | no | **string** <br />The pipeline's name
currency_code | no | **string** <br />ISO code of the currency to use in this pipeline
created_at | no | **datetime** <br />ISO 8601 format with timezone offset
updated_at | no | **datetime** <br />ISO 8601 format with timezone offset


## Create a pipeline
```shell
# DEFINITION
POST https://api.overloop.com/public/v1/pipelines

# EXAMPLE
curl -X POST "https://api.overloop.com/public/v1/pipelines" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8" \
-d '{
  "data": {
    "type": "pipelines",
    "attributes": {
      "name": "A pipeline name"
    }
  }
}'
```

This will create a new pipeline.

### Parameters
Parameter | Default | Description
--------- | ------- | ------------
name<br />**required** - *string* | / | The pipeline's name
currency_code<br />**required** - *string* | / | The pipeline's currency code

### Returns
Returns the [pipeline object](#the-pipeline-object).

## Retrieve a pipeline
```shell
# DEFINITION
GET https://api.overloop.com/public/v1/pipelines/{PIPELINE_ID}

# EXAMPLE
curl -X GET "https://api.overloop.com/public/v1/pipelines/1" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

### Parameters
Parameter | Description
--------- | -----------
id<br />**required** - *integer* | The ID of the pipeline to retrieve

### Returns
Returns the [pipeline object](#the-pipeline-object).

## Update a pipeline
```shell
# DEFINITION
PATCH https://api.overloop.com/public/v1/pipelines/{PIPELINE_ID}

# EXAMPLE
curl -X PATCH "https://api.overloop.com/public/v1/pipelines/1" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8" \
-d '{
  "data": {
    "type": "pipelines",
    "attributes": {
      "name": "Germany"
      "currency_code": "EUR"
    }
  }
}'
```

Updates the specified pipeline by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

### Parameters
Parameter | Description
--------- | -----------
id<br />**required** - *integer* | The ID of the pipeline to update
name<br />*string* | The pipeline's name
currency_code<br />*string* | The pipeline's currency code

### Returns
Returns the [pipeline object](#the-pipeline-object).

## Delete a pipeline
```shell
# DEFINITION
DELETE https://api.overloop.com/public/v1/pipelines/{PROSPECT_ID}

# EXAMPLE
curl -X DELETE "https://api.overloop.com/public/v1/pipelines/1" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "1",
    "type": "pipelines"
  }
}
```

Permanently deletes a pipeline. It cannot be undone.

<aside class="notice">
Warning — Deleting a pipeline will delete all the stages and all the deals inside it
</aside>

### Parameters
Parameter | Required? | Type | Description
--------- | --------- | -----| -----------
id | **yes** | integer | The ID of the pipeline to delete

### Returns
Returns an object containing the pipeline ID.

## List pipelines

```shell
# DEFINITION
GET https://api.overloop.com/public/v1/pipelines

# EXAMPLE
curl -X GET "https://api.overloop.com/public/v1/pipelines" \
-H "Authorization: your_api_key" \
-H "Content-Type: application/vnd.api+json; charset=utf-8"
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": "1",
      "type": "pipelines",
      "attributes": {
        ...
      }
    },
    {
      "id": "2",
      "type": "pipeline",
      "attributes": {
        ...
      }
    }
  ],
  "links": {
    "self": "https://api.overloop.com/public/v1/pipelines/?page%5Bnumber%5D=1&page%5Bsize%5D=100",
    "next": "https://api.overloop.com/public/v1/pipelines/?page%5Bnumber%5D=2&page%5Bsize%5D=100",
    "last": "https://api.overloop.com/public/v1/pipelines/?page%5Bnumber%5D=5&page%5Bsize%5D=100"
  }
}
```

Returns a list of pipelines.

This pipeline is [paginated](#pagination) by 100 records and can also be [sorted](#sorting) or [filtered](#filtering).
