# Where to refer
You can refer to official [explore API](https://www.elastic.co/guide/en/elasticsearch/reference/current/getting-started-search-API.html) for much more detail.
<br>
You can use this page for some examples and if you want to get much more deeper you can go to the official page.

# Two ways to search
* By sending search parameters through the [REST request URI](https://www.elastic.co/guide/en/elasticsearch/reference/7.0/search-uri-request.html)
* By sending them through the [REST request body](https://www.elastic.co/guide/en/elasticsearch/reference/7.0/search-request-body.html)

## Which way is better?
For the first way, you can use it as the simple user cases. For example you just want to search something by inputting simple parameters you can use this way.
<br>
For the second way, you can use it as the complicated user cases. By using this way you will define your criterias in your request body, and those criteria you can define them by using readable JSON format.


# REST Request API

How to use the REST API just refer to [here](https://www.elastic.co/guide/en/elasticsearch/reference/7.0/search-uri-request.html).

```sh
curl -X GET "localhost:9200/bank/_search?q=*&sort=account_number:asc&pretty"

```
You will get the response body as:

```
{
  "took" : 63,
  "timed_out" : false,
  "_shards" : {
    "total" : 5,
    "successful" : 5,
    "skipped" : 0,
    "failed" : 0
  },
  "hits" : {
    "total" : {
        "value": 1000,
        "relation": "eq"
    },
    "max_score" : null,
    "hits" : [ {
      "_index" : "bank",
      "_type" : "_doc",
      "_id" : "0",
      "sort": [0],
      "_score" : null,
      "_source" : {"account_number":0,"balance":16623,"firstname":"Bradshaw","lastname":"Mckenzie","age":29,"gender":"F","address":"244 Columbus Place","employer":"Euron","email":"bradshawmckenzie@euron.com","city":"Hobucken","state":"CO"}
    }, {
      "_index" : "bank",
      "_type" : "_doc",
      "_id" : "1",
      "sort": [1],
      "_score" : null,
      "_source" : {"account_number":1,"balance":39225,"firstname":"Amber","lastname":"Duke","age":32,"gender":"M","address":"880 Holmes Lane","employer":"Pyrami","email":"amberduke@pyrami.com","city":"Brogan","state":"IL"}
    }, ...
    ]
  }
}
```
## Detail about the response
* took – time in milliseconds for Elasticsearch to execute the search
* timed_out – tells us if the search timed out or not
* _shards – tells us how many shards were searched, as well as a count of the successful/failed searched shards
* hits – search results
* hits.total – an object that contains information about the total number of documents matching our search criteria
* 
* hits.total.value - the value of the total hit count (must be interpreted in the context of hits.total.relation).
* hits.total.relation - whether hits.total.value is the exact hit count, in which case it is equal to "eq" or a lower bound of the total hit count (greater than * or equals), in which case it is equal to gte.
* hits.hits – actual array of search results (defaults to first 10 documents)
* hits.sort - sort key for results (missing if sorting by score)
* hits._score and max_score - ignore these fields for now


