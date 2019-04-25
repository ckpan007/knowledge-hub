# Log4j
ES is developed by java programming language, naturally it uses log4j as the logging component. Log4j can be configured using the log4j2.properties file, and _ES exposes three properties to let user change_. **${sys:es.logs.base_path}, ${sys:es.logs.cluster_name}, and ${sys:es.logs.node_name}** that can be referenced in the configuration file to determine the location of the log files.

* ${sys:es.logs.base_path} - resolves to the log directory
* ${sys:es.logs.cluster_name} - resolves to the cluster name (used as the prefix of log filenames in the default configuration)
* ${sys:es.logs.node_name} - resolves to the node name (if the node name is explicitly set)

**For example**: if your log directory _(path.logs)_ is _/var/log/elastcisearch_ and your cluster is named _production_ then ${sys:es.logs.base_path} will resolve to _/var/log/elasticsearch_ and ${sys:es.logs.base_path}${sys:file.separator}${sys:es.logs.cluster_name}.log will resolve to _/var/log/elasticsearch/production.log_.

# Detail Explanation about the logging
Please refer to official [Logging Configuration](https://www.elastic.co/guide/en/elasticsearch/reference/current/logging.html).

# You can got through earlier version of ES logging
When you are confused with many configuration options there for release 7.0.0, you can go back to get through an earlier version such as 5.x.x. ES gives much more clear detail about options of configuring logging. <br>
https://www.elastic.co/guide/en/elasticsearch/reference/5.5/settings.html


# Log rolling
Why you need log rooling? This is important that your application or system are creating logs all the time. With the time pass by, the log size is growing always. So that you need to do some limit for your logs, see below url for similar situation: https://github.com/elastic/logstash/issues/8233
<br>
Consider of above situation, ES affords you the functions of rolling over the logs of course for the retain logs.

# /var/log/elasticsearch/ and /etc/elasticsearch/log4j2.properties
For current release 7.0.0, the log location is stored in /etc/elasticsearch/elasticsearch.yml with configuration _path.log:/var/log/elasticsearch_
<br>
And also you can find the _log4j.properties_ file in location _/etc/elasticsearch/log4j2.properties_.

![Var Log](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/elasticsearch/var-log.jpg)

# How to configure log level
There are four ways to configuring logging levels, each having situations in which they are appropriate to use.
* Via the command-line - _-E <name of logging hierarchy>=<level>_ (e.g., -E logger.org.elasticsearch.transport=trace). This is most appropriate when you are temporarily debugging a problem on a single node (for example, a problem with startup, or during development).
* Via elasticsearch.yml - _<name of logging hierarchy>: <level> (e.g., logger.org.elasticsearch.transport: trace)_. This is most appropriate when you are temporarily debugging a problem but are not starting Elasticsearch via the command-line (e.g., via a service) or you want a logging level adjusted on a more permanent basis.
* Via cluster settings - 
```
PUT /_cluster/settings
{
  "transient": {
    "<name of logging hierarchy>": "<level>"
  }
}


PUT /_cluster/settings
{
  "transient": {
    "logger.org.elasticsearch.transport": "trace"
  }
}
```

* Via the log4j2.properties - This is most appropriate when you need fine-grained control over the logger (for example, you want to send the logger to another file, or manage the logger differently; this is a rare use-case).
```
logger.<unique_identifier>.name = <name of logging hierarchy>
logger.<unique_identifier>.level = <level>

logger.transport.name = org.elasticsearch.transport
logger.transport.level = trace
```

# Reference Link
https://www.elastic.co/guide/en/elasticsearch/reference/current/logging.html#configuring-logging-levels


