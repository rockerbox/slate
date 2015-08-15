## Pattern search

> Request (count for a single pattern): 

```shell
# TODO: !!
# current -- needs format and advertiser on end of URL "&format=json&advertiser=baublebar"
# proposed -- use authentication

curl "http://crusher.getrockerbox.com/crusher/search/count?search=necklaces" 

```

> Response (count for single pattern):

```
{
    "logic": "should",
    "search": [
        "necklaces"
    ],
    "summary": {
        "num_users": 1200
    }
}
```

> Request 
> - urls that match pattern

```shell

curl "http://crusher.getrockerbox.com/crusher/search/urls?search=rockerbox"
```

> Response 
> - urls that match pattern

```shell
{
    "logic": "must",
    "results": [
        {
            "count": 1,
            "url": "http://www.baublebar.com/whats-new/just-added.html?cvosrc=display.rockerbox.072015_JulyDigAdsRefresh_300x250_3_9718787&utm_source=rockerbox&utm_medium=display&utm_campaign=072015_JulyDigAdsRefresh_300x250_3_9718787"
        },
        {
            "count": 1,
            "url": "http://www.baublebar.com/whats-new/just-added.html?cvosrc=display.rockerbox.072015_JulyDigAdsRefresh_300x600_1_4279296&utm_source=rockerbox&utm_medium=display&utm_campaign=072015_JulyDigAdsRefresh_300x600_1_4279296"
        },
        {
            "count": 1,
            "url": "http://www.baublebar.com/whats-new/just-added.html?cvosrc=display.rockerbox.072015_JulyDigAdsRefresh_728x90_1_3810899&utm_source=rockerbox&utm_medium=display&utm_campaign=072015_JulyDigAdsRefresh_728x90_1_3810899"
        }
    ],
    "search": [
        "rockerbox"
    ],
    "summary": {
        "num_urls": 3,
        "num_users": 3
    },
    "timeout": 60
}
```

> Request 
> - uids for multiple patterns using **AND** logic

```shell

# TODO: !!
# current (defaults to or)
# propsoed (should default to AND)
curl "http://crusher.getrockerbox.com/crusher/search/uids?search=necklaces,pepperjam"
```

> Response 
> - uids for multiple patterns using **AND** logic

```shell
{
    "logic": "must",
    "results": [
        "1658345989907319038",
        "8544236950523550015",
        "3647988598677495450",
        "8377247509133269564",
        "8728953026525723133",
        "4371882728305824796",
        "4355801865744751912",
        "3071870354224070944",
        "8282590386514880072",
        "5213257658303005847",
        "682573251720908722"
    ],
    "search": [
        "necklaces",
        "pepperjam"
    ],
    "summary": {
        "num_users": 11
    }
}
```


> Request 
> - timeseries for multiple patterns using **AND** logic

```shell

# TODO: !!
# current (defaults to or)
# propsoed (should default to AND)
curl "http://crusher.getrockerbox.com/crusher/search/timeseries?search=necklaces,pepperjam"
```

> Response 
> - timeseries for multiple patterns using **AND** logic

```shell
{
    "logic": "must",
    "results": [
        {
            "date": "2015-07-29 00:00:00",
            "num_users": 4,
            "num_visits": 5
        },
        {
            "date": "2015-07-30 00:00:00",
            "num_users": 7,
            "num_visits": 7
        }
    ],
    "search": [
        "necklaces",
        "pepperjam"
    ],
    "summary": {
        "num_users": 11,
        "num_visits": 12
    }
}
```


> Request 
> - timeseries for multiple patterns using **OR** logic

```shell

curl "http://crusher.getrockerbox.com/crusher/search/timeseries?search=necklaces,pepperjam&logic=or"
```

> Response 
> - timeseries for multiple patterns using **OR** logic

```shell
{
    "logic": "should",
    "results": [
        {
            "date": "2015-07-29 00:00:00",
            "num_users": 708,
            "num_visits": 2327
        },
        {
            "date": "2015-07-30 00:00:00",
            "num_users": 993,
            "num_visits": 2858
        }
    ],
    "search": [
        "necklaces",
        "pepperjam"
    ],
    "summary": {
        "num_users": 1653,
        "num_visits": 5185
    }
}
```



This endpoint allows us to search for the occurance of a pattern or multiple patterns within a single URL.

The pattern search API supports:

- four query result types (urls, uids, count, timeseries).
- two types of logic when searching for a pattern within a URL ("or","and")

### HTTP Request

`GET http://crusher.getrockerbox.com/crusher/search/<QUERY_TYPE>`


### Query Parameters

Parameter | Default | Description
--------- | ------- | ----------
search | None | this is a *required* field. it is a string or comman seperated string of terms  we will look for in the URL. If multiple terms are used, the logic parameter will be used param will be used to perform the search
logic | and | this specifies the logic to use for a search term. specifically, if we are looking for nature,nuture in a url, or would require either nature or nuture, and would require both nature and nuture
format | json | this specifies the response type. currently only json is supported
timeout | 60 | this is the amount of time in seconds we will attempt to process the query before timing out. Its default and max value is 60 seconds

<aside class="default">Note that the search field is required for all queries</aside>



### JSON Response

The JSON response will be formatted with the following fields:

Field | Description
----- | -----------
search | these are the terms entered as commas seperated values to the search QS parameter
logic | this is the logic used interally to evaluate URLs against the pattern(s) specified
summary | this is a summary object describing the results. depending on the query type it will have different values but will always be present
results | the result object is based on the query type. It will be present for all results with the exception of the count, which will only have a summary object

### JSON Result Objects

This describes the different JSON Result object types that one can expect for the different query types

Query Type | Description
---------- | --------------
urls | this is a list of objects that contain the URL and the number of matches for that url. it will be sorted based on count
uids | this is a list of UID strings associated with the pattern
timeseries |  this is a timeseries which shows the counts at each respective date

<aside class="warning">Note that the **count** query type does not have a results object present</aside>
