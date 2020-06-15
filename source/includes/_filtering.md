# Filtering
```shell
# EXAMPLE
GET https://api.prospect.io/public/v1/prospects/?filter=first_name:john,last_name:doe
```

> Get prospects whose first name is 'john' and last name is 'doe'.

Resource collections retrieved through the API can be **filtered** using one or several object attributes, in the form of a comma separated list. The filterable attributes **accepted** by the API for **each object collection** are detailed in the section of the doc on the considered object.
