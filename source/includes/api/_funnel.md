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
{
}
```

## Creating a funnel

> Create

```shell
cat <<EOF > funnel
{
}
EOF
curl -X POST -d @funnel http://crusher.getrockerbox.com/crusher/funnel
```

> Response

```json
{
}
```

## Updating a funnel

> Update

```bash
cat <<EOF > action
{
}
EOF
curl -X PUT -d @action http://crusher.getrockerbox.com/crusher/funnel?id=1
```

> Response

```json
{
}
```

## Deleting a funnel

> DELETE

```bash
curl -X DELETE http://crusher.getrockerbox.com/crusher/funnel?id=1
```

> Response

```json
{
}
```

