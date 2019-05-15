# What it is for
This exercise is for the real world, during this exercise you will try to insert more than 1000 items of data via JSON format.

# Preparation

## Data
You will use [Json Generator](https://www.json-generator.com/) to create more than 1000 items of single data.
<br>
You will store the data into a local file named _account.json_.

## Data operation
For ES if you want to use _Batch Processing_ you might need to do some changement for the generated json data, follow ES's standard:

```sh
curl -X POST "localhost:9200/customer/_bulk?pretty" -H 'Content-Type: application/json' -d'
{"index":{"_id":"1"}}
{"name": "John Doe" }
{"index":{"_id":"2"}}
{"name": "Jane Doe" }
'

```

From above you need to follow the style to change your generated json data.
For [Batch Processing](https://www.elastic.co/guide/en/elasticsearch/reference/current/getting-started-batch-processing.html)

## Insert data into ES
After you set up the set of your data, now it is the time to insert the data into ES.

```sh
curl -H "Content-Type: application/json" -XPOST "localhost:9200/bank/_bulk?pretty&refresh" --data-binary "@accounts.json"
curl "localhost:9200/_cat/indices?v"
```


