# Funnel


> Excample funnel

```json
{
}
```

## Get all funnels

> Request All

```shell
curl http://crusher.getrockerbox.com/crusher/funnel?format=json
```

> Response All

```json
[
  {
    "owner": "owner",
    "advertiser": "baublebar",
    "funnel_name": "",
    "actions": [
      {
        "url_pattern": [
          "utm"
        ],
        "action_name": "necklaces utm",
        "order": 1,
        "action_id": 15
      },
      {
        "url_pattern": [
          "http://www.baublebar.com/bracelets.html"
        ],
        "action_name": "bracelets",
        "order": 2,
        "action_id": 20
      },
      {
        "url_pattern": [
          "checkout"
        ],
        "action_name": "checkout",
        "order": 3,
        "action_id": 1
      }
    ],
    "funnel_id": 96
  },
  {
    "owner": "owner",
    "advertiser": "baublebar",
    "funnel_name": "alans",
    "actions": [
      {
        "url_pattern": [
          "rockerbox"
        ],
        "action_name": "rockerbox bracelets",
        "order": 1,
        "action_id": 149
      },
      {
        "url_pattern": [
          "checkout"
        ],
        "action_name": "checkout",
        "order": 2,
        "action_id": 1
      }
    ],
    "funnel_id": 117
  }
]
```

## Get a specific funnel

> Request One

```shell
curl http://crusher.getrockerbox.com/crusher/funnel?format=json&id=1
```

> Response One

```json
[
  {
    "owner": "owner",
    "advertiser": "baublebar",
    "funnel_name": "",
    "actions": [
      {
        "url_pattern": [
          "utm"
        ],
        "action_name": "necklaces utm",
        "order": 1,
        "action_id": 15
      },
      {
        "url_pattern": [
          "http://www.baublebar.com/bracelets.html"
        ],
        "action_name": "bracelets",
        "order": 2,
        "action_id": 20
      },
      {
        "url_pattern": [
          "checkout"
        ],
        "action_name": "checkout",
        "order": 3,
        "action_id": 1
      }
    ],
    "funnel_id": 96
  }
]
```

## Creating a funnel

> Create

```shell
cat <<EOF > funnel
{
    "advertiser": "baublebar",
    "funnel_name": "my_new_funnel",
    "owner": "my_username",
    "actions": [
      {
        "action_id": 20,
        "order": 1
      },
      {
        "action_id": 1,
        "order": 2,
      }
    ]
}
EOF
curl -X POST -d @funnel http://crusher.getrockerbox.com/crusher/funnel
```

> Response

```json
{
    "status": "ok",
    "response": {
        "advertiser": "baublebar",
        "segment_id": 3268470,
        "funnel_name": "my_new_funnel",
        "actions": [
            {
                "order": 1,
                "action_id": 20
            },
            {
                "order": 2,
                "action_id": 1
            }
        ],
        "owner": "my_username",
        "funnel_id": 153
    }
}
```

## Updating a funnel

> Update

```bash
cat <<EOF > action
{
    "owner": "owner",
    "advertiser": "baublebar",
    "funnel_name": "SOMETHING",
    "actions": [
        {
            "url_pattern": [
                "utm"
            ],
            "action_name": "necklaces utm",
            "order": 2,
            "action_id": 15
        },
        {
            "url_pattern": [
                "http://www.baublebar.com/bracelets.html"
            ],
            "action_name": "bracelets",
            "order": 3,
            "action_id": 20
        },
        {
            "url_pattern": [
                "checkout"
            ],
            "action_name": "checkout",
            "order": 1,
            "action_id": 1
        }
    ],
    "funnel_id": 96
}
EOF
curl -X PUT -d @action http://crusher.getrockerbox.com/crusher/funnel?id=1
```

> Response

```json
{
    "status": "ok",
    "response": {
        "advertiser": "baublebar",
        "funnel_name": "SOMETHING",
        "actions": [
            {
                "action_id": 15,
                "url_pattern": [
                    "utm"
                ],
		                "order": 2,
                "action_name": "necklaces utm"
            },
            {
                "action_id": 20,
                "url_pattern": [
                    "http://www.baublebar.com/bracelets.html"
                ],
                "order": 3,
                "action_name": "bracelets"
            },
            {
                "action_id": 1,
                "url_pattern": [
                    "checkout"
                ],
                "order": 1,
                "action_name": "checkout"
            }
        ],
        "owner": "owner",
        "funnel_id": 96
    }
}
```

## Deleting a funnel

> DELETE

```bash
curl -X DELETE http://crusher.getrockerbox.com/crusher/funnel?id=153
```

> Response

```json
{
    "status": "ok", 
    "response": "Funnel id 153 deleted successfully."
}
```

