# Funnel Search

This endpoint is very similar to the multi pattern group search, in that it allows us to access the same type of information. 
The only difference is that the Funnel Search API takes a funnel_id as a paramater, and performs the search based on that funnel's settings.

This API supports the following query result types: (count, uids, domains)

## HTTP Request

`GET http://crusher.getrockerbox.com/crusher/funnel/search/<QUERY_TYPE>?id=<FUNNEL_ID>`

