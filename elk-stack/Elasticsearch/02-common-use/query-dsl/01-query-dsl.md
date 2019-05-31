# Query String

```sh
curl -X GET "localhost:9200/_search" -H 'Content-Type: application/json' -d'
{
    "query": {
        "query_string" : {
            "default_field" : "address",
            "query" : "address1 OR address2"
        }
    }
}
'
```

* 查询address字段值为address1或者address2
* 不管你有多少index，只要你有docment包含符合的数据即返回结果

查询结果如下：

![Query DSL](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/elasticsearch/querydsl/query-dsl-result.jpg)

Detail you can go to [Elasticsearch 7.1 Query DSL](https://www.elastic.co/guide/en/elasticsearch/reference/7.1/query-dsl-query-string-query.html#query-string-syntax).

## 多字段查询
```sh
curl -X GET "localhost:9200/_search" -H 'Content-Type: application/json' -d'
{
    "query": {
        "query_string" : {
            "fields" : ["address","name"],
            "query" : "(address:address1) OR (address:address2) OR (name:name1) OR (name:1)"
        }
    }
}
'
```

查询结果如下：

```
{
    "took": 128,
    "timed_out": false,
    "_shards": {
        "total": 3,
        "successful": 2,
        "skipped": 0,
        "failed": 1,
        "failures": [
            {
                "shard": 0,
                "index": "test",
                "node": "OcB8mJHSSAyRUDBLG4CNAw",
                "reason": {
                    "type": "query_shard_exception",
                    "reason": "failed to create query: {\n  \"query_string\" : {\n    \"query\" : \"(address:address1) OR (address:address2) OR (name:name1) OR (name:1)\",\n    \"fields\" : [\n      \"address^1.0\",\n      \"name^1.0\"\n    ],\n    \"type\" : \"best_fields\",\n    \"default_operator\" : \"or\",\n    \"max_determinized_states\" : 10000,\n    \"enable_position_increments\" : true,\n    \"fuzziness\" : \"AUTO\",\n    \"fuzzy_prefix_length\" : 0,\n    \"fuzzy_max_expansions\" : 50,\n    \"phrase_slop\" : 0,\n    \"escape\" : false,\n    \"auto_generate_synonyms_phrase_query\" : true,\n    \"fuzzy_transpositions\" : true,\n    \"boost\" : 1.0\n  }\n}",
                    "index_uuid": "B2Zq824SR56nlfzzp7UIVg",
                    "index": "test",
                    "caused_by": {
                        "type": "number_format_exception",
                        "reason": "For input string: \"name1\""
                    }
                }
            }
        ]
    },
    "hits": {
        "total": {
            "value": 2,
            "relation": "eq"
        },
        "max_score": 1.4508328,
        "hits": [
            {
                "_index": "accounts",
                "_type": "_doc",
                "_id": "1",
                "_score": 1.4508328,
                "_source": {
                    "name": "name1",
                    "user-id": 1,
                    "age": 20,
                    "@timestamp": "2019-05-27",
                    "address": "address1",
                    "job-position": "police"
                }
            },
            {
                "_index": "accounts",
                "_type": "_doc",
                "_id": "2",
                "_score": 0.47000363,
                "_source": {
                    "name": "name2",
                    "user-id": 2,
                    "age": 20,
                    "@timestamp": "2019-05-27",
                    "address": "address1",
                    "job-position": "police"
                }
            }
        ]
    }
}
```

