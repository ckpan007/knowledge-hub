# Introduction
Elasticsearch is a highly scalable open-source full-text search and analytics engine. It allows you to store, search, and analyze big volumes of data quickly and in near real time. It is generally used as the underlying engine/technology that powers applications that have complex search features and requirements.
<br>
Elasticsearch is an search engine based on Apache Lucene (TM), and Lucene is the widety accepted as the most advanced, best performing, and most versatile search engine. But Lucene is just a library you can use, you need to use Java as the programing language and integration the Lucene into your application.


# Basic Concepts

## NRT(Near Realtime)
Elasticsearch is a near-realtime search platform. What this means is there is a slight latency (normally one second) from the time you index a document until the time it becomes searchable.

## Cluster
A cluster is a collection of one or more nodes (servers) that together holds your entire data and provides federated indexing and search capabilities across all nodes. A cluster is identified by a unique name which by default is "elasticsearch". This name is important because a node can only be part of a cluster if the node is set up to join the cluster by its name.

### Notice about Cluster
* Default cluster name is given as _elasticsearch_
* Unique name for cluster
* Different cluster with different name
* Suggest cluster name as _logging-dev,logging-stage, logging-prod_

## Node
A node is a single server that is part of your cluster, stores your data, and participates in the cluster’s indexing and search capabilities. Just like a cluster, a node is identified by a name which by default is a random Universally Unique IDentifier (UUID) that is assigned to the node at startup. 

### Notice about Node
* A random UUID(Universally Unique IDentifier) as the default name is assigned to Node at the startup
* Node name can be changed and node name is important for administration purpose
* By default, each node is setup to join a cluster named _elasticsearch_ in case you dont assign it specifically
* A cluster can have as many node as you want
* If you start a single node first at the very beginning, then a cluster named as _elasticsearch_ will automatically created

## Document
A document is a basic unit of information that can be indexed. For example, you can have a document for a single customer, another document for a single product, and yet another for a single order. This document is expressed in **JSON** (JavaScript Object Notation) which is a ubiquitous internet data interchange format. Within an index, you can store as many documents as you want.

<br>
For example: you see below for a instance JSON for _account_.
```sh
'{"name":"John", "lastname":"Doe", "job_description":"Systems administrator and Linux specialit"}'
```

## Index
An index is a collection of documents that have somewhat similar characteristics. For example, you can have an index for customer data, another index for a product catalog, and yet another index for order data. An index is identified by a name (that must be all lowercase) and this name is used to refer to the index when performing indexing, search, update, and delete operations against the documents in it.

<br>
In a single cluster, you can define as many indexes as you want.


## Shards & Replicas
An index can potentially store a large amount of data that can exceed the hardware limits of a single node. For example, a single index of a billion documents taking up 1TB of disk space may not fit on the disk of a single node or may be too slow to serve search requests from a single node alone.
<br>
To solve this problem, Elasticsearch provides the ability to subdivide your index into multiple pieces called **shards**. When you create an index, you can simply define the number of shards that you want. Each shard is in itself a fully-functional and independent "index" that can be hosted on any node in the cluster.

### Shards
* It allows you to horizontally split/scale your content volume
* It allows you to distribute and parallelize operations across shards (potentially on multiple nodes) thus increasing performance/throughput

### Replicas
Elasticsearch allows you to make one or more copies of your index’s shards into what are called replica shards, or replicas for short.
* It provides high availability in case a shard/node fails. For this reason, it is important to note that a replica shard is never allocated on the same node as the original/primary shard that it was copied from.
* It allows you to scale out your search volume/throughput since searches can be executed on all replicas in parallel.

### Summary about Shards & Replicas
* Each index can be split into multiple shards
* An index can also be replicated zero (meaning no replicas) or more times
* Each index will have primary shards (the original shards that were replicated from) and replica shards (the copies of the primary shards)
* The number of shards and replicas can be defined per index at the time the index is created, and you can change the number anytime you like
* By default, each index in Elasticsearch is allocated one primary shard and one replica which means that if you have at least two nodes in your cluster, your index will have one primary shard and another replica shard (one complete replica) for a total of two shards per index




# Reference Links

Get Started: https://www.elastic.co/guide/en/elasticsearch/reference/current/getting-started.html

