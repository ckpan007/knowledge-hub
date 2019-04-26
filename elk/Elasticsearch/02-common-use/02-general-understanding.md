# Introduction
ElasticSearch is an open source, **RESTful search engine** built on top of Apache Lucene and released under the Apache license. It is Java-based, and can search and index document files in diverse formats.

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

## Document in ES
The data store in ES is called as _Document_. Documents in Elasticsearch are represented in JSON format. Also, documents are added to indices, and documents have a type. We are adding now to the index named accounts a document of type person having the id 1; since the index does not exist yet, Elasticsearch will automatically create it.

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



# Reference Link
https://www.elastic.co/blog/a-practical-introduction-to-elasticsearch
