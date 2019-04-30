# Introduction
ElasticSearch is an open source, **RESTful search engine** built on top of Apache Lucene and released under the Apache license. It is Java-based, and can search and index document files in diverse formats.
<br>
Very important feature: **RESTFUL API for you to do operations**.<br>

ElasticSearch has been compared to Apache Solr and offers several notable features:

* Provides a scalable search solution.
* Performs near-real-time searches.
* Provides support for multi-tenancy.
* An index can be easily recovered in a case of a server crash.
* Uses Javascript Object Notation (JSON) and Java application program interfaces (APIs).
* Automatically indexes JSON documents.
* Each index can have its own settings.
* Searches can be done with Lucene-based querystrings.

# Indices and Types
Every time you store data in Elasticsearch it gets saved inside an index which has a type. compared to MongoDB an index is similar to a database, and a type similar to a collection. Compared to SQL an index would be like a database, and a type like a table.
<br>
_Index_ is the result of the data store, and each index has a type with it. You can think index as database, and type as table.
```
localhost:9200/{index}/{type}/
```

# Document in ES
The data store in ES is called as _Document_. Documents in Elasticsearch are represented in JSON format. Also, documents are added to indices, and documents have a type. We are adding now to the index named accounts a document of type person having the id 1; since the index does not exist yet, Elasticsearch will automatically create it.

# Add Documenet
```
POST localhost:9200/accounts/person/1 
{
    "name" : "John",
    "lastname" : "Doe",
    "job_description" : "Systems administrator and Linux specialit"
}
```

The response will return information about the document creation:

```
{
    "_index": "accounts",
    "_type": "person",
    "_id": "1",
    "_version": 1,
    "result": "created",
    "_shards": {
        "total": 2,
        "successful": 1,
        "failed": 0
    },
    "created": true
}
```
# Get Document

Now that the document exists, we can retrieve it:
```
GET localhost:9200/accounts/person/1 
```
The result will contain metadata and also the full document (shown in the _source field) :
```
{
    "_index": "accounts",
    "_type": "person",
    "_id": "1",
    "_version": 1,
    "found": true,
    "_source": {
        "name": "John",
        "lastname": "Doe",
        "job_description": "Systems administrator and Linux specialit"
    }
}
```

# Update Document
```
POST localhost:9200/accounts/person/1/_update
{
      "doc":{
          "job_description" : "Systems administrator and Linux specialist"
       }
}
```

# Search
Search format looks like: **/_search?q=something**

```
GET localhost:9200/_search?q=john
```
The response:
```
{
    "took": 58,
    "timed_out": false,
    "_shards": {
        "total": 5,
        "successful": 5,
        "failed": 0
    },
    "hits": {
        "total": 2,
        "max_score": 0.2876821,
        "hits": [
            {
                "_index": "accounts",
                "_type": "person",
                "_id": "2",
                "_score": 0.2876821,
                "_source": {
                    "name": "John",
                    "lastname": "Smith",
                    "job_description": "Systems administrator"
                }
            },
            {
                "_index": "accounts",
                "_type": "person",
                "_id": "1",
                "_score": 0.28582606,
                "_source": {
                    "name": "John",
                    "lastname": "Doe",
                    "job_description": "Systems administrator and Linux specialist"
                }
            }
        ]
    }
}
```
For search functions you need to afford some search criterias in order to let ES do the search for you. The result is depends on the search criteria.
* _search?q=[value or contidition here for the search]
* _search?q=[some attribute name of your documen, e.g job_description in example] **:** [attribute value you want for the search]

# Delete Documenet
You added the document and now you want to delete document, you need to input the _path_ you defined that you added the document.
```
DELETE localhost:9200/accounts/person/1
```
The response will looks like below:
```
{
    "found": true,
    "_index": "accounts",
    "_type": "person",
    "_id": "1",
    "_version": 3,
    "result": "deleted",
    "_shards": {
        "total": 2,
        "successful": 1,
        "failed": 0
    }
}
```

# Delete full index
```
DELETE localhost:9200/accounts

```

# Index API
https://www.elastic.co/guide/en/elasticsearch/reference/5.5/docs-index_.html

## Create Index
```sh
curl -X PUT localhost:9200/customer?pretty
curl -X GET "localhost:9200/_cat/indices?v"

The first command creates the index named "customer" using the PUT verb. We simply append pretty to the end of the call to tell it to pretty-print the JSON response (if any).

```
https://www.elastic.co/guide/en/elasticsearch/reference/6.1/_create_an_index.html

# Get API
https://www.elastic.co/guide/en/elasticsearch/reference/5.5/docs-get.html
# Delete API
https://www.elastic.co/guide/en/elasticsearch/reference/5.5/docs-delete.html
# Update API
https://www.elastic.co/guide/en/elasticsearch/reference/5.5/docs-update.html
# URI Search
https://www.elastic.co/guide/en/elasticsearch/reference/5.5/search-uri-request.html


## Query Strings API
Please refer to https://www.elastic.co/guide/en/elasticsearch/reference/5.5/query-dsl-query-string-query.html#query-string-syntax



# Full Coding

## Touch a new file named data.json

```
# Input the value into this file:

{
    "name" : "John",
    "lastname" : "Doe",
    "job_description" : "Systems administrator and Linux specialit"
}

```
## Create a new Index named accounts
```sh
https://www.elastic.co/guide/en/elasticsearch/reference/current/getting-started-create-index.html

curl -X PUT localhost:9200/customer?pretty
curl -X GET "localhost:9200/_cat/indices?v"

```

## POST Request to the ES
```sh
curl -d '{"name":"John", "lastname":"Doe", "job_description":"Systems administrator and Linux specialit"}' -H "Content-Type: application/json" -X POST localhost:9200/accounts/person/1

```

![Index Document Create](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/elasticsearch/index-document-operation.jpg)


# Reference Link
https://www.elastic.co/blog/a-practical-introduction-to-elasticsearch

CURL POST:
https://gist.github.com/HuangMarco/3e42b19f1a9feed4cd748ac4016b8eb6


