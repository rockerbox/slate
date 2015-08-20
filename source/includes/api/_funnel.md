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
{
}
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
curl -X PUT -d @action http://crusher.getrockerbox.com/crusher/funnel?funnel_id=1
```

> Response

```json
{
}
```

## Deleting a funnel

> DELETE

```bash
curl -X DELETE http://crusher.getrockerbox.com/crusher/funnel?funnel_id=1
```

> Response

```json
{
}
```

