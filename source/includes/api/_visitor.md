# Visitor Endpoints

> Example action

```json
{
    "response": 
	{
		"data":100,
		"otherdata":200,
		"moredata":[]
	},
    "search": "[[myurlpattern]]",
    "summary": {},
    "logic": "and"
}
```

Visitor endpoints provide data related to visitors to client pages with pixel on page. Endpoints will contain a response key which will contain the relevant data from specified endpoint. The available endpoints, the data returned and an example of the call and response are provided below

All activities related to actions require the user to be logged in.


Key | Description
--- | -----------
response | This key will contain the data for the response of the given endpoint
summary | A summary of the response object, includes sum for numeric or count for non numeric data keys in response object
logic | by default, this should only be set to "or". The behavior associated with an "and" operator can be achieved by comma seperating strings
search | array containing the url pattern associated with the response


## Domains (offsite)

> Request domains for All Pages segment

```shell
curl http://crusher.getrockerbox.com/crusher/visitor/v2/domains?url_pattern=/&format=json
```

> Response All

```json
{
    "status": "ok",
    "response":[
        {
	    "count":695,
	    "domain":"ebay.com",
	    "num_users":34204.0,
	    "parent_category_name":"Shopping",
	    "idf":4.65,
	    "category_name":"Auctions"
        },
        {
	    "count":576,
	    "domain":"cnn.com",
	    "num_users":585.0,
	    "parent_category_name":"News",
	    "idf":8.72,
	    "category_name":"Broadcast & Network News"
        }
    ]
}
```


`GET http://crusher.getrockerbox.com/crusher/visitor/v2/domains?url_pattern=/&format=json`

The response will consist of a list of action objects, which are defined above in the **Anatomy of an action**.


## Full URL (off site)

> Request One

```shell
curl http://crusher.getrockerbox.com/crusher/v2/visitor/domains_full?url_pattern=/format=json
```

> Response One

```json
{
    "status": "ok",
    "response":[{
    	"count":37,
	"domain":"hgtv.com",
	"url":"http:\/\/www.hgtv.com\/design\/hgtv-smart-home\/sweepstakes",
	"num_users":2974.0,
	"parent_category_name":"Home & Garden",
	"idf":7.13,
	"category_name":"Home Furnishings"
    }]
}
```


Domains Full

## Onsite user ids

> User ids for those users who have been onsite

```shell
curl GET  curl http://crusher.getrockerbox.com/crusher/v2/visitor/onsite?url_pattern=/format=json
```

> Response

```json
{
    "status": "ok",
    "response":[
	{
	    "uid":"1034077027452067558",
	    "visits":8,
	    "sessions":1
	},
	{
	    "uid":"1050263989851933110",
	    "visits":6,
	    "sessions":1
	}
    ]
}
```


The response from this endpoint will be a standard action json object described above in the anatomy of an action.


## Crusher Modules

> GET

```bash
curl GET http://crusher.getrockerbox.com/crusher/visitor/v2/before_and_after?url_pattern=/&format=json
```

> Response

```json
{
    "status": "ok",
    "response":{
        "before_categories":
	    [{
		"values":
			[{
			    "count":0.0,
			    "num":10.0,
			    "time_bucket":5
			}]
    	}]
   }
}

```

`GET http://crusher.getrockerbox.com/crusher/visitor/v2/onsite?url_pattern=/format=json`

The response will be the standard json object.

## User Defined Functions

> GET

```bash
curl GET http://crusher.getrockerbox.com/crusher/visitor/v2/<FUNCTION NAME>?url_pattern=/&format=json
```

> Response

```json
{
    "status": "ok",
    "response":{
        "data":[]
    }
}
```

The response will vary depending on the output of the user defined function
