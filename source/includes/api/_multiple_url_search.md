# Group URL Search (DEPRECATED)

This endpoint allows us search for users who visited multiple URL patterns and get the union or intersection of the visits that have occured on these matched pages. 

Similar to the the single URL search, this API support:

- the query result types: (uids,count,timeseries)
- two type of logic: (union, intersection)

## HTTP Request

`GET http://crusher.getrockerbox.com/crusher/pattern_search/<QUERY_TYPE>`

## Query Parameters

Parameter | Default | Description
--------- | ------- | ----------
search    | None    | this is a **required** field. the search string is made up of comman seperated patterns and pipe seperated pattern groups. the comma seperated pattern requires all occurances of the pattern to be present in matched urls. the pipe seperation between pattern allows one to look at either the union or intersection of the users who have visited urls that matched the pattern string.
logic     | intersection | this specifies whether were looking at the union or intersection of the pattern strings. A union results in reporting based on all the patterns matched. An intersection is looking at the intersection of the two patterns
format    | json | this specifies the response type. currently only json is supported
timeout | 60 | this is the amount of time in seconds we will attempt to process the query before timing out. Its default and max value is 60 seconds

## More on the "search" and "logic" parameters

The search parameter is made up of multiple **URL pattern strings** seperated by pipe characters. 
A **URL pattern string** is a comma seperated string of values, e.g. "nature,nuture".
When this API evaluates a URL pattern string, the indivual patterns will be evaluated using an  **AND** operation, meaning that every url that matches this pattern must contain all terms in the string.

The following is an example of two URL pattern strings used as a search parameter:

`/crusher/pattern_search?search=nature,nuture|wild`

Each URL pattern string is used to find the users associated with each URL pattern string.

Pattern | Users 
------- | ----  
nature,nuture | User group 1 
wild | User group 2 

The logic parameter will then be used to either take the union or the intersection of the users that match. 

Logic | Matches 
----- | ------- 
Union | users who match any of the patterns
Intersection | users who many all of the patterns 

Finally, the eligible users will be selected out of the overall data set and an aggregated result will be returned. Specifically,

Logic | Description
----- | -----------
Union | This is an aggregation of all of the resulting patterns
Intersection | The resulting data set is an aggregation of all (URL, user) combinations from any pattern in search parameter but limited to the subset of the user groups



