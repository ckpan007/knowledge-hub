# About ES
ES features a distributed full-text search engine, provides high availability, and handles both the indexation and search of our clients’ logs in real-time. Plus it’s written in Java, which is at the core of our application.
<br>
But just as for any database, it really needs monitoring to ensure reliability and optimal performance. Elasticsearch provides a set of tools to get the state of your system at any given time (cat APIs, Cluster APIs, …). But if you want to monitor it in a more passive way and for optimal performance, you can rely on its logs.

# Basic elasticsearch logging configuration
By default, elasticsearch logs are located in ES_HOME/logs/${cluster.name}.log, at log level INFO. It’s a good compromise, as interesting logs can be caught with a log file of reasonable size.

In the same directory, you’ll find other files such as:
* ${cluster.name}_index_indexing_slowlog.log
* ${cluster.name}_index_search_slowlog.log

You can also tune your elasticsearch log settings: change level for one specific logger, add an output file, … To do so, you basically have two options:
* Modify the _log4j2.properties_: Modifications will require an rolling restart
* Use the ES's REST API about reloadable configuration settings, refer to [here](https://github.com/HuangMarco/knowledge-hub/blob/dev/elk/Elasticsearch/04-elasticsearch-config-jvm-secure.md#reload-the-secure-settings-to-make-the-changes-work---important)

For example, if you have the feeling that index creation is taking longer than usual, you can set the logger cluster.service to level DEBUG, and you’ll get the real creation time for each created index in your elasticsearch logs – like this:
```
processing [create-index [index6], cause [api]]: took 64ms done applying updated cluster_state (version: 194)).
```

# The top 3 elasticsearch logs to watch
## Check your elasticsearch error logs
it is important to extract log levels and monitor logs with a level higher or equal to ERROR. We strongly recommend you to setup an alert on these elasticsearch log levels with your favorite log analytics tool. Have a look at these, you could find some interesting stuff, for example, detect configuration issues.

## Keep an eye on slow elasticsearch GC logs
One frequent issue with Elasticsearch is the memory handling. You definitely don’t want to reach the OutOfMemory point. To prevent this from happening, here are a few best practices:
* Set the ES_HEAP_SIZE parameter properly, depending on the available resource of the host and your workload, without allocating more than 32GB. More details available here
* Monitor node heap usage (among other metrics like CPU, I/O…) with the [cat APIs](https://www.elastic.co/guide/en/elasticsearch/reference/current/cat-nodes.html) for ex., and get alerted when you reach a specific threshold on one node
* Make sure to set bootstrap.mlockall: true to [avoid swapping](https://www.elastic.co/guide/en/elasticsearch/guide/current/heap-sizing.html#_swapping_is_the_death_of_performance)
* Do not over-allocate your nodes (for example, use sharding to balance data across your cluster)

## Analyse elasticsearch Slow Queries


# Reference Link
https://logmatic.io/blog/get-the-most-of-your-elasticsearch-logs/
