# What is pipeline
![Basic Pipeline](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/logstash/basic_logstash_pipeline.png)

From above you will know that: <br>
A Logstash pipeline has below elements:
* input - **required, must have**, consume data from a source
* filter - **optional**, modify the data as you specify
* output - **required, must have**, write the data to a destination

# How Logstash works
Each Logstash event processes pipeline has three stages:
```
INPUTS ======> FILTERS ======> OUTPUTS
```
* Inputs generate events
* Filters modify events created by Inputs
* Outputs support codecs enable you to encode or decode the data as it enters or exits the pipeline without having to use a separate filter

Inputs, Filters, Outputs they are all called _plugins_ in Logstash.


## Input

You use inputs to get data into Logstash. Some of the more commonly-used inputs are:
* file: reads from a file on the filesystem, much like the UNIX command tail -0F
* syslog: listens on the well-known port 514 for syslog messages and parses according to the RFC3164 format
* redis: reads from a redis server, using both redis channels and redis lists. Redis is often used as a "broker" in a centralized Logstash installation, which queues Logstash events from remote Logstash "shippers".
* beats: processes events sent by [Beats](https://www.elastic.co/downloads/beats).

For more information about the available inputs, see [Input Plugins](https://www.elastic.co/guide/en/logstash/current/input-plugins.html).

## Filters
Filters are intermediary processing devices in the Logstash pipeline. You can combine filters with conditionals to perform an action on an event if it meets certain criteria. Some useful filters include:

* grok: parse and structure arbitrary text. Grok is currently the best way in Logstash to parse unstructured log data into something structured and queryable. With 120 patterns built-in to Logstash, it’s more than likely you’ll find one that meets your needs!
* mutate: perform general transformations on event fields. You can rename, remove, replace, and modify fields in your events.
* drop: drop an event completely, for example, debug events.
* clone: make a copy of an event, possibly adding or removing fields.
* geoip: add information about geographical location of IP addresses (also displays amazing charts in Kibana!)

All of the available operations are for events.
For more information about the available filters, see [Filter Plugins](https://www.elastic.co/guide/en/logstash/current/filter-plugins.html).

## Outputs
Outputs are the final phase of the Logstash pipeline. An event can pass through multiple outputs, but once all output processing is complete, the event has finished its execution. Some commonly used outputs include:

* elasticsearch: send event data to Elasticsearch. If you’re planning to save your data in an efficient, convenient, and easily queryable format… Elasticsearch is the way to go. Period. Yes, we’re biased :)
* file: write event data to a file on disk.
* graphite: send event data to graphite, a popular open source tool for storing and graphing metrics. http://graphite.readthedocs.io/en/latest/
* statsd: send event data to statsd, a service that "listens for statistics, like counters and timers, sent over UDP and sends aggregates to one or more pluggable backend services". If you’re already using statsd, this could be useful for you!

For more information about the available outputs, see [[Output Plugins](https://www.elastic.co/guide/en/logstash/current/output-plugins.html).

## Codecs
Codecs are basically stream filters that can operate as part of an input or output. Codecs enable you to easily separate the transport of your messages from the serialization process. Popular codecs include json, msgpack, and plain (text).

* json: encode or decode data in the JSON format.
* multiline: merge multiple-line text events such as java exception and stacktrace messages into a single event.

For more information about the available codecs, see [Codec Plugins](https://www.elastic.co/guide/en/logstash/current/codec-plugins.html).

# Reference Link
https://www.elastic.co/guide/en/logstash/current/pipeline.html