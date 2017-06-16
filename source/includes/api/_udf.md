# UDF

> Example Response

```json
{
    "response": [{}],
    "search": [["/"]],
    "summary": {},
    "after": [{}],
    "before": [{}]
}
```


UDF or User Defined Functions are the core way for which we return data. A standard set of datasets containing information about the users` onsite and offsite behavior as well as user and domain level data arre passed into the user defined function. The function then analyses and aggregated the data to create the response.

The UDF requested is determined by the RESTful URL schema . See the examples below for samples of existing udfs and schema acess pattern.

All response are in JSON format.


Every UDF will have the following items in its response:

Key | Description
--- | -----------
response | this is an auto generated identifier for the action. this identifier will be use later to relate actions to funnels
search | this is an array of strings that are used to match against the url associated with an event
summary | (optional) by default, this should only be set to "or". The behavior associated with an "and" operator can be achieved by comma seperating strings
before | (optional) this is the advertiser that the action is associated with
after | (optional) this is the advertiser that the action is associated with


## Get UDF

> Request UDF

```shell
curl http://hindsight.getrockerbox.com/crusher/v1/visitor/<UDF>?url_pattern=/&filter_id=1
curl http://hindsight.getrockerbox.com/crusher/v1/visitor/domains?url_pattern=/&filter_id=1
```

> Response

```json
{
    "response":[
        {"count":2,"domain":"recipes.com","uniques":1,"time to site":5.7666666667,"Importance":24690.3333333333,"rank":24690.3333333333,"num_users":1000000.0,"parent_category_name":"Food & Drink","idf":24690.3333333333,"category_name":"Cooking & Recipes"},
        {...}
    ]
}
```

To view all the actions that you have created, you can simply send a get request to the action endpoint with the format query string parameter set to json.

## Datasets


