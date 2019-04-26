# Running ES as special user for ES
You can refer to [Here](https://github.com/HuangMarco/knowledge-hub/blob/dev/elk/Elasticsearch/03-configuration/03-elasticsearch-config.md) for much more detail.

# Health check for all the culsters
Following before guide I will use user _elsearch_ to run ES. After you running ES you will execute below command for ES:
```sh
curl -X GET "localhost:9200/_cat/health?v"
```

![Get Health](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/elasticsearch/get-health.jpg)

From above you will get the health status for your cluster. **The default cluster name is elasticsearch**. There are three status options:
* Green - everything is good (cluster is fully functional)
* Yellow - all data is available but some replicas are not yet allocated (cluster is fully functional)
* Red - some data is not available for whatever reason (cluster is partially functional)

Notice: If the status is red, ES still afford search functions but you need to fix the issue ASAP.

# Health check for all the nodes

```sh
curl -X GET "localhost:9200/_cat/nodes?v"

```

