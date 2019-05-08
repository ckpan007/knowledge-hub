# What is it
This is the list of all the commands.

# Command

## Health Check

```sh
curl -X GET "localhost:9200/_cat/health?v"
```

## List all the nodes

```sh
curl -X GET "localhost:9200/_cat/nodes?v"
```

## List all the indices
```sh
curl -X GET "localhost:9200/_cat/indices?v"
```

The result looks like below:

```
mar@ubuntu:~$ curl -X GET "localhost:9200/_cat/indices?v"
health status index    uuid                   pri rep docs.count docs.deleted store.size pri.store.size
yellow open   accounts OKiBCaaFQ0yjJ1_JbrTkQw   1   1          1            0      4.9kb          4.9kb
yellow open   customer OLdrwRZmS8KB2mvxRgfTOw   1   1          1            0      3.5kb          3.5kb

```
You can get the index name.

## Search all the document

```sh
curl -X GET "localhost:9200/accounts/_search?q=*"
```
Above command searches all the documents. _accounts_ is the index name.
<br>
The response looks like below:

```
mar@ubuntu:~$ curl -X GET "localhost:9200/accounts/_search?q=*"
{"took":125,"timed_out":false,"_shards":{"total":1,"successful":1,"skipped":0,"failed":0},"hits":{"total":{"value":1,"relation":"eq"},"max_score":1.0,"hits":[{"_index":"accounts","_type":"person","_id":"1","_score":1.0,"_source":{"name":"John", "lastname":"Doe", "job_description":"Systems administrator and Linux specialit"}}]}}
```

## Search the document with the specific property
```sh
curl -X GET "localhost:9200/accounts/_search?q=name:John"
```
Above searches the specific document with property _name_ equals with _John_.


## Search the document with the request body

```sh
curl -X GET 'localhost:9200/accounts/_search' -H 'Content-Type: application/json' -d '
{
    "query" : {
        "match_all" : {}
    }
}'
```

```sh
curl -X GET 'localhost:9200/accounts/_search' -H 'Content-Type: application/json' -d '
{
    "query" : {
        "match" : {"name":"John"}
    }
}'
```

## Query DSL

### Match Query
Please refer to official website [match query](https://www.elastic.co/guide/en/elasticsearch/reference/7.0/query-dsl-match-query.html#query-dsl-match-query-boolean).


### Term Query
Please refer to official website [term query](https://www.elastic.co/guide/en/elasticsearch/reference/7.0/query-dsl-term-query.html).

### Range Query
Please refer to official website [range query](https://www.elastic.co/guide/en/elasticsearch/reference/7.0/query-dsl-range-query.html).


## Add Document
```sh

curl -d '{"name":"Joke", "lastname":"Kitty", "job_description":"Software engineer"}' -H "Content-Type: application/json" -X POST localhost:9200/accounts/person/2

```

## Get Document with specific ID
Below try to get the document with id value as 1

```sh
curl -X GET localhost:9200/accounts/person/2
```


