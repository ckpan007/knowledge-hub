# Installation - Unbuntu Deb
```sh
curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.0.1-amd64.deb
sudo dpkg -i filebeat-7.0.1-amd64.deb

```

![Installation](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/filebeat/installation.jpg)


# Installation Output
* The filebeat will be installed at **/usr/share/filebeat**
* The configuration files stored at **/etc/filebeat/filebeat.yml**

# Configuration
```
filebeat.inputs:
- type: log
  enabled: true
  paths:
    - /var/log/*.log
    #- c:\programdata\elasticsearch\logs\*
```

Above is the sample of the filebeat section of the filebeat.yml file.

# Start a behavior of configuring filebeat

## Define the path (or paths) to your log files.
```
filebeat.inputs:
- type: log
  enabled: true
  paths:
    - /var/log/*.log

```
The input in this example harvests all files in the path /var/log/*.log, which means that Filebeat will harvest all files in the directory /var/log/ that end with .log. All patterns supported by [Go Glob](https://golang.org/pkg/path/filepath/#Glob) are also supported here.

```
/var/log/*/*.log

```
This fetches all .log files from the subfolders of /var/log. It does not fetch log files from the /var/log folder itself.
<br>
**Notice**: Currently it is not possible to recursively fetch all files in all subdirectories of a directory.

## Configure the output
You need to define the output of the logs. For all the availbale choice you can use as the output:
See [Output](https://www.elastic.co/guide/en/beats/filebeat/current/configuring-output.html).

* [Output for Elasticsearch](https://www.elastic.co/guide/en/beats/filebeat/current/elasticsearch-output.html)
* [Output for Logstash](https://www.elastic.co/guide/en/beats/filebeat/current/logstash-output.html)
* [Output for kafka](https://www.elastic.co/guide/en/beats/filebeat/current/kafka-output.html)
* [Output for Redis](https://www.elastic.co/guide/en/beats/filebeat/current/redis-output.html)
* [Output for Fuke](https://www.elastic.co/guide/en/beats/filebeat/current/file-output.html)




For much more detail related with [Configuration of Filebeat](https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-configuration.html#filebeat-configuration).

And also [Configuring filebeat](https://www.elastic.co/guide/en/beats/filebeat/current/configuring-howto-filebeat.html) for the summary of configuring filebeat.




# Reference Link
https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-getting-started.html


