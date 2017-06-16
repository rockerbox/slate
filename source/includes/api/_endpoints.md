# Other Endpoints


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

Every action will have the following items in its response:

Key | Description
--- | -----------
action_id | this is an auto generated identifier for the action. this identifier will be use later to relate actions to funnels
url_pattern | this is an array of strings that are used to match against the url associated with an event
operator | by default, this should only be set to "or". The behavior associated with an "and" operator can be achieved by comma seperating strings
advertiser | this is the advertiser that the action is associated with


## Get all actions

> Request All

```shell
curl http://crusher.getrockerbox.com/crusher/funnel/action?format=json
```

> Response All

```json
{
    "status": "ok",
    "response":[
        {
            "advertiser": "my_advertiser",
            "action_name": "checkout",
            "url_pattern": [ "checkout" ],
            "action_id": 1
        },
        {
            "advertiser": "my_advertiser",
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


## Get a specific action

> Request One

```shell
curl http://crusher.getrockerbox.com/crusher/funnel/action?format=json&id=1
```

> Response One

```json
{
    "status": "ok",
    "response":[{
        "advertiser": "my_advertiser",
        "action_name": "checkout",
        "url_pattern": [ "checkout" ],
        "action_id": 1
    }]
}
```

To view a specific action, the request is modified to additional query string parameter specifying the id of the action you would like to view.

`GET http://crusher.getrockerbox.com/crusher/funnel/action?format=json&id=<ACTION_ID>`

In this case, rather than return a list we instead see that a single action is returned for our response

## Creating an action

> Create

```shell
cat <<EOF > action
{
    "action_name": "checkout",
    "url_pattern": [ "checkout" ],
}
EOF
curl -X POST -d @action http://crusher.getrockerbox.com/crusher/funnel/action
```

> Response

```json
{
    "status": "ok",
    "response":{
        "advertiser": "my_advertiser",
        "action_name": "checkout",
        "url_pattern": [ "checkout" ],
        "action_id": 1
    }
}
```

To create a new action, post a json object that has a name to identify the action, `action_name`, and a list of patterns you want to match in the `url_pattern`.

`POST http://crusher.getrockerbox.com/crusher/funnel/action?format=json`

The response from this endpoint will be a standard action json object described above in the anatomy of an action.


## Updating an action

> Update

```bash
cat <<EOF > action
{
    "action_id": 1,
    "action_name": "checkout",
    "url_pattern": [ "checkOUT" ],
}
EOF
curl -X PUT -d @action http://crusher.getrockerbox.com/crusher/funnel/action?id=1
```

> Response

```json
{
    "status": "ok",
    "response":{
        "advertiser": "my_advertiser",
        "action_name": "checkout",
        "url_pattern": [ "checkOUT" ],
        "action_id": 1
    }
}
```

To update an action, put a json object with the desired changes to an endpoint which has an `action_id` qs parameter corresponding to the object you want to update.

`PUT http://crusher.getrockerbox.com/crusher/funnel/action?format=json&id=<ACTION_ID>`

The response will be the standard json object.

## Deleting an action

> DELETE

```bash
curl -X DELETE http://crusher.getrockerbox.com/crusher/funnel/action?id=1
```

> Response

```json
{
    "status": "ok",
    "response":{
        "action_id": 1
    }
}
```

To delete an action, send a delete request to the endpoint with the `action_id` qs parameter corresponding to the object you want to delete.

`DELETE http://crusher.getrockerbox.com/crusher/funnel/action?format=json&id=<ACTION_ID>`

The response will be an object with only the action_id of the deleted object.
