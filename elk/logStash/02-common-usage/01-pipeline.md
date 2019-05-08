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
* beats: processes events sent by Beats.

For more information about the available inputs, see [Input Plugins](https://www.elastic.co/guide/en/logstash/current/input-plugins.html).


