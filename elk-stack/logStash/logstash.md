# What is Logstash
Logstash is one component of the whole Elastic Stack. 是全家桶的一部分。

* Logstash is an _open source_ data collection engine with real-time pipelining capabilities
* Logstash can dynamically unify data from disparate sources and normalize the data into destinations of your choice
* Cleanse and democratize all your data for diverse advanced downstream analytics and visualization use cases
* Collect more, so you can know more. Logstash welcomes data of all shapes and sizes
* Pluggable pipeline architecture - That means you can choose many data sources to do the data input

# Log data for Logstash
* Web logs from [Apache](http://www.elastic.co/guide/en/logstash/6.2/advanced-pipeline.html), application logs like log4j for Java
* other log formats like [syslog](http://www.elastic.co/guide/en/logstash/6.2/plugins-inputs-syslog.html), networking and firewall logs, and more
* complementary secure log forwarding capabilities with [Filebeat](https://www.elastic.co/products/beats/filebeat)

# Metrics for Logstash
Collect metrics from [Ganglia](http://www.elastic.co/guide/en/logstash/6.2/plugins-inputs-ganglia.html), [collectd](http://www.elastic.co/guide/en/logstash/6.2/plugins-codecs-collectd.html), [NetFlow](http://www.elastic.co/guide/en/logstash/6.2/plugins-codecs-netflow.html), [JMX](http://www.elastic.co/guide/en/logstash/6.2/plugins-inputs-jmx.html), and many other infrastructure and application platforms over TCP and UDP

# Http Request for Logstash
* Logstash can receive single or multiline events over http(s), Applications can send an HTTP POST request with a body to the endpoint started by this input and Logstash will convert it into an event for subsequent processing. Users can pass plain text, JSON, or any formatted data and use a corresponding codec with this input. For Content-Type application/json the json codec is used, but for all other data formats, plain codec is used.
<br>
https://www.elastic.co/guide/en/logstash/6.2/plugins-inputs-http.html

# Stash for Logstash
**Stash** is a really important concept in the design of the Logstash. You can think _Stash_ as the resource of the log data, Logstash afford many choices for you for the stash.
## Analysis

* Elasticsearch
* Data stores such as MongoDB and [Riak](http://www.elastic.co/guide/en/logstash/6.2/plugins-outputs-riak.html)

## Archiving
* [HDFS](http://www.elastic.co/guide/en/logstash/6.2/plugins-outputs-webhdfs.html)
* [S3](http://www.elastic.co/guide/en/logstash/6.2/plugins-outputs-s3.html)

# Monitoring
* [Nagios](http://www.elastic.co/guide/en/logstash/6.2/plugins-outputs-nagios.html)
* [Ganglia](http://www.elastic.co/guide/en/logstash/6.2/plugins-outputs-ganglia.html)
* [Zabbix](http://www.elastic.co/guide/en/logstash/6.2/plugins-outputs-zabbix.html)
* [Graphite](http://www.elastic.co/guide/en/logstash/6.2/plugins-outputs-graphite.html)
* [Datadog](http://www.elastic.co/guide/en/logstash/6.2/plugins-outputs-datadog.html)
* [CloudWatch](http://www.elastic.co/guide/en/logstash/6.2/plugins-outputs-cloudwatch.html)

# Alerting
* Watcher with Elasticsearch
* Email
* Pagerduty
* IRC
* SNS


# Reference Link
https://www.elastic.co/guide/en/logstash/6.2/introduction.html

