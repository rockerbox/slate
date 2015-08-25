# Multi Pattern Group search

This endpoint allows us search for statistics about the sequential intersection of multiple pattern groups. This API builds off of the pattern group concept introduced in the [Pattern Group URL Search] API.

Similar to the the Pattern Group URL search, this API shares the idea of the pattern group, but limits the logic of a pattern group to look only at the union of a pattern. 

Similar to the other search APIs. this API allows the user to specify:

- the logic used between pattern groups (union, funnel)
- the result type: (count, uids, domains)

To represent the logic between pattern groups, the ">" operator is used to demarcate distinct pattern groups. This operators was chosen because it helps to represent the sequential nature of the computed intersection (the default behavior of the API).


## HTTP Request

`GET http://crusher.getrockerbox.com/crusher/multi_pattern_search/<QUERY_TYPE>`

## Query Parameters

Parameter | Default | Description
--------- | ------- | ----------
search    | None         | this is a **required** field. the search string is made up of > seperated pattern groups. See the pattern group API to
logic     | funnel       | this specifies whether were looking at the union or intersection of the pattern groups.
format    | json         | this specifies the response type. currently only json is supported
timeout   | 60           | this is the amount of time in seconds we will attempt to process the query before timing out. Its default and max value is 60 seconds

## More about multiple pattern group evaluation

The search parameter is made up of multiple pattern groups seperated by **>** characters. 

`
?search=[pattern_group1]>[pattern_group_2]>[pattern_group_3]
`

When this API evaluates each pattern group, it uses the default **UNION** logic to evaluate the pattern group meaning that all users who visited a URL that matched either pattern in a group are included. Also note that within a pattern the default **AND** logic is also used.

## Logic Operator

The **>** operator then takes the result of each pattern group and evaluates either:

- a sequential intersection (a funnel)
- a union (a union)

## Logic Types: 

**1. Funnel (Sequential intersection)**

The default behavior is to perform a sequential intersection (funnel) of users. More specifically, this is best described as:

Step | Users
---- | -----
1    | User in Group 1 
2    | User in Group 1 AND Group 2 
3    | User in Group 1 AND Group 2 AND Group 3

implying that each sequential group will be smaller than the previous. 

**2. Union**

The union logic type is included to make it convienent to get back information about the entire state space that the intersection is operating over. 

More specifically, we can describe this as follows:

Step | Users
---- | -----
1    | User in Group 1 
2    | User in Group 1 OR Group 2 
3    | User in Group 1 OR Group 2 OR Group 3

implying that each sequential group will be larger than the previous. 

### Response Types

**1. count**

- this is the count of users in each bucket

**2. uids**

- this is the raw user ids for users in each bucket

**3. domains**

- this is the domain associated with the users in each bucket

**4. all**

- this is all of the information


## Example

The following is an example of two URL pattern strings used as a search parameter:

`/crusher/multi_pattern_search?search=signup>nature|wild>checkout`

Our evaluation for each step would then look like the following:

Step | Users
---- | -----
1    | Visited signup page
2    | Visited signup page AND visited a (nature OR wild) urls
3    | Visited signup page AND visited a (nature OR wild) urls AND checked out
