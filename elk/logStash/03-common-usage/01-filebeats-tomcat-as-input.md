# What is it
This is the exerciese to create a sample Logstash scenario. You will use [Filebeat](https://github.com/elastic/beats/tree/master/filebeat) to take Apache web logs as input, parses those logs to create specific, named fields from the logs, and writes the parsed data to an Elasticsearch cluster. You will define the configuration in a config file.


# Prerequisites
* Elasticsearch installed in your virtual machine
* You download the used sample data from [here](https://download.elastic.co/demos/logstash/gettingstarted/logstash-tutorial.log.gz) and unpack it

# Introduction about Filebeat
The Filebeat client is a lightweight, resource-friendly tool that collects logs from files on the server and forwards these logs to your Logstash instance for processing. Filebeat is designed for reliability and low latency. Filebeat has a light resource footprint on the host machine, and the Beats input plugin minimizes the resource demands on the Logstash instance. Your Filebeat running on the same machine with the Elasticsearch.




# Reference Link
https://www.elastic.co/guide/en/logstash/6.2/advanced-pipeline.html#configuring-filebeat
