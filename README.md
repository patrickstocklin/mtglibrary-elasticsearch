# Useful Commands

### HC on Cluster

```curl -X GET "localhost:9200/_cat/health" ```

### Create Index

```curl -X PUT "localhost:9200/pat"```

### Destroy Index

```curl -X DELETE "localhost:9200/pat"```

### Insert Document into Index

```
curl -X PUT "localhost:9200/pat/_doc/" -H 'Content-Type: application/json' -d' {
  "object" : "card",
  "id" : "906b6e99-128f-4c11-8daf-16099d35b0d4",
  "name" : "Assassin's Trophy",
  "prices" : {
    "usd" : 12.57,
    "usd_foil" : 28.42
  },
  "image_uris" : {
    "small" : "https://img.scryfall.com/cards/small/front/9/0/906b6e99-128f-4c11-8daf-16099d35b0d4.jpg?1538879946"
  }
} '
```

### Sum prices of all cards across index

```
curl -X POST "localhost:9200/pat/_search?size=0&pretty" -H 'Content-Type: application/json' -d'
{
    "aggs" : {
        "prices" : { "sum" : { "field" : "prices.usd" } }
    }
}
'
{
  "took" : 67,
  "timed_out" : false,
  "_shards" : {
    "total" : 1,
    "successful" : 1,
    "skipped" : 0,
    "failed" : 0
  },
  "hits" : {
    "total" : {
      "value" : 53,
      "relation" : "eq"
    },
    "max_score" : null,
    "hits" : [ ]
  },
  "aggregations" : {
    "prices" : {
      "value" : 236.04000083357096
    }
  }
}
```