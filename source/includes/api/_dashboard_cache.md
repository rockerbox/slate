# Cached Endpoints

This api allows us to query the cache mysql table. Allows a much quicker response time for the population of the action/segment dashboard. Utilizes the crusher api to create cache version of this data in a mysql table and returns this data

### Generic anatomy of a Response#
> Request 10

```shell
curl http://crusher.getrockerbox.com/crusher/dashboard_cached?limit=10
```
>Response 1

```json
{
    "domains": [
		{
			"values": [
				{
					"domain":"domain",
					"count":1
				}
			],
			"key": "action"
		}
 	]
}
```

Key | Description
--- | ----------
domains| array containing data for the top domains for given advertiser 
key    | advertiser segment/action
action_type | segment or vendor
values | domain and count data for segment/action 


The limit argument is optional
If not used the response will contain the top 5 domains for the authenticated user
If limit is used the repsonse will contain the top X domains for the authenticated user where X is equal to the value of limited passed to the endpoint

