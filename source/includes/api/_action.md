# Model APIs

The model APIs allow us to model information that we receive from an on page pixel. These APIs are the building blocks for our UI and allow the user to store saved and recurring data queries.

### Generic anatomy of a Response

```json
{
    "response": [],
    "summary": {},
    "errors": []
}
```

Each json response with have a similar format. Below we outline the high level stucture a user can expect from a JSON response.

Key | Description
--- | ----------
response | (required) This is where the data relevant to the response lives. This will typically be an array of objects
summary  | (optional) This is where any summary information about the request and response lives
errors   | (optional) This is where any errors associated with the request live. This will typically be an array of objects

## Action

> Example action

```json
{
    "action_id": 1,
    "action_name": "checkout",
    "acvertiser": "my_advertiser",
    "url_pattern": ["checkout"]
}
```


Actions are our fundamental block for understand both on-site and off-site user behavior. 
Actions allow the user to specify a series of patterns that correspond to central idea or theme of on-site behavior. 
Below we take you through how to view, create, update and delete an action.

All activities related to actions require the user to be logged in.

### Anatomy of an action


Every action will have the following items in its response:

Key | Description
--- | -----------
action_id | this is an auto generated identifier for the action. this identifier will be use later to relate actions to funnels
url_pattern | this is an array of strings that are used to match against the url associated with an event
operator | by default, this should only be set to "or". The behavior associated with an "and" operator can be achieved by comma seperating strings
advertiser | this is the advertiser that the action is associated with

### TODOs: 

- DONE rename pixel_source_name to advertiser
- DONE potentially get rid of operator from this response. it probably isnt necessary anymore given our lookup using lucene
- DONE remove the date ranges from the action response
- DONE lets change the default response type to json so that it doesnt need to be on the url and a format=json



### Get all actions

> Request (all actions)

```shell
curl http://crusher.getrockerbox.com/crusher/funnel/action?format=json
```

> Response (all actions)

```json
{
    "response":[
        {
            "advertiser": "baublebar",
            "action_name": "checkout",
            "url_pattern": [ "checkout" ],
            "action_id": 1
        },
        {
            "advertiser": "baublebar",
            "action_name": "necklaces utm",
            "url_pattern": [ "utm" ],
            "action_id": 15
        }
    ]
}
```

To view all the actions that you have created, you can simply send a get request to the action endpoint with the format query string parameter set to json.

`GET http://crusher.getrockerbox.com/crusher/funnel/action?format=json`

The response will consist of a list of action objects, which are defined above in the **Anatomy of an action**.

### TODOs: 

- DONE this should be within our standard response format
- DONE want to transition all the APIs so that we have them within a wrapping object


### Get a specific action

> Request (specific action)

```shell
curl http://crusher.getrockerbox.com/crusher/funnel/action?format=json&id=1
```

> Response (specific actions)

```json
{
    "response":[{
        "advertiser": "baublebar",
        "action_name": "checkout",
        "url_pattern": [ "checkout" ],
        "action_id": 1
    }]
}
```

To view a specific action, the request is modified to additional query string parameter specifying the id of the action you would like to view.

`GET http://crusher.getrockerbox.com/crusher/funnel/action?format=json&id=<ACTION_ID>`

In this case, rather than return a list we instead see that a single action is returned for our response

### Creating an action

```shell

```

To create a new action, post a json object that has a name to identify the action, `action_name`, and a list of patterns you want to match in the `url_pattern`.

`POST http://crusher.getrockerbox.com/crusher/funnel/action?format=json`

The response from this endpoint will be a standard action json object described above in the anatomy of an action.


### Updating an action

`PUT http://crusher.getrockerbox.com/crusher/funnel/action?format=json&id=<ACTION_ID>`

### Deleting an action

`DELETE http://crusher.getrockerbox.com/crusher/funnel/action?format=json&id=<ACTION_ID>`

