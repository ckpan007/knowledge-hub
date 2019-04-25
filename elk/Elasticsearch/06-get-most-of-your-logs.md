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
Depending on the data typology (heavy documents, multiples indices, …), you may experience performance issues, with slow elasticsearch queries as one of the symptoms.
Queries with high execution time results in bad user experience, and with the state of the current digital age, we all want to avoid it. The 90’s are long gone.

### Configuration
Determine the threshold for considering an elasticsearch query slow based on your business and industry, and register it in the elasticsearch.yml config file. You can also set it at runtime.
<br>
Setting several thresholds can be useful to monitor elasticsearch performance more finely. At Logmatic.io, our slow query thresholds are the one suggested in the Elasticsearch Slow Log configuration page:
```
index.search.slowlog.threshold.query.warn: 10s
index.search.slowlog.threshold.query.info: 5s 
index.search.slowlog.threshold.query.debug: 2s
index.search.slowlog.threshold.query.trace: 500ms
```

This config is a good start, but the best configuration is always one adapted to your specific workload challenges.

As mentioned previously, these logs go in a dedicated file, ${cluster.name}_index_search_slowlog.log, and you should definitely watch it carefully to ensure optimal elasticsearch performance.

### Elasticsearch slow log format
Let’s see what a slow log looks like:
```
[2016-02-04 16:07:32,964][INFO][index.search.slowlog.query] [vagrant-host] [client1_index3][0] took[5.2s], took_millis[5203],
types[], stats[], search_type[COUNT], total_shards[3],
source[{“size”:0,”timeout”:60000,”query”:{“constant_score”:{“filter”:{“range”:{“fsmatic.date”:{“from”:1454599730468,”to”:1454604106092,”include_lower”:true,”include_upper”:false}}}}},”aggregations”:{“time”:{“fast_date_histogram”:{“field”:”fsmatic.date”,”interval”:”30000″,”pre_offset”:”3600000″,”post_offset”:”-3600000″}}}}], extra_source[],
```

Here are some interesting pieces of information:
* took[5.2s] Execution time. This is a metric, and a good log analytics tool should let you draw analytics based on it. See our blogpost here if you need some more insights on log-based metrics.

![Query Duration](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/elasticsearch/query-duration.png)


* [vagrant-host]: Hostname. Your problems could be caused by one or several specific hosts, so pay attention to this field. At Logmatic.io, we once detected disk failures on one node thanks to elasticsearch slow query logs, and our further investigation showed a latency issue yet undiscovered.
* [client1_index3]: index name. Obviously, you have to check whether one index causes slow queries. If you have a multi-tenant infrastructure or if your indices carry some temporal logic, you should be able to identify from the index name the time or the client and thus refine your analysis. At Logmatic.io, we extract the client ID from the index, and make sure nobody is experiencing too many slow queries.
* Source[..]: The query. By looking at it (range, aggregation, …), you could simply identify why your query is slow.

## Useful Use cases
* Index creation log, especially creation time. It is a good indication of your cluster health
* Index deletion logs
* Snapshot / restore tasks

# Reference Link
https://logmatic.io/blog/get-the-most-of-your-elasticsearch-logs/
