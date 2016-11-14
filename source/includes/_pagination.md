# Pagination

```json
{
  "data": [
    {
      ...
    }
  ],
  "links": {
    "self": "https://prospect.io/api/public/v1/prospects?page%5Bnumber%5D=2&page%5Bsize%5D=1",
    "first": "https://prospect.io/api/public/v1/prospects?page%5Bnumber%5D=1&page%5Bsize%5D=1",
    "prev": "https://prospect.io/api/public/v1/prospects?page%5Bnumber%5D=1&page%5Bsize%5D=1",
    "next": "https://prospect.io/api/public/v1/prospects?page%5Bnumber%5D=3&page%5Bsize%5D=1",
    "last": "https://prospect.io/api/public/v1/prospects?page%5Bnumber%5D=2203&page%5Bsize%5D=1"
  }
}
```

Collection APIs paginate their results. The first request returns up to 100 records. If the request returns more than 100 records and `links` will be include in the result. This object may contains the following keys:

* **self**: the current page of data
* **first**: the first page of data
* **last**: the last page of data
* **prev**: the previous page of data
* **next**: the next page of data
