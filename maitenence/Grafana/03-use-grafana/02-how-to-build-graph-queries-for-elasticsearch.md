# Before you start
It takes long time that I tried to find the metrics information used in Grafana. At last I found that the metrics knowledge I can just read from Elasticsearch itself but not Grafana. So if you want to use Elasticsearch as the data source you should got through knowledge about [Elasticsearch Metrics](https://www.elastic.co/guide/en/elasticsearch/reference/master/search-aggregations.html). After that you will know how to build a grafana query using elasticsearch metrics. And in Grafana the query was called as [Lucene Query](https://lucene.apache.org/core/2_9_4/queryparsersyntax.html#Fields).

You should know below:
* ES query string - https://www.elastic.co/guide/en/elasticsearch/reference/5.0/query-dsl-query-string-query.html#query-string-syntax
* Lucene Query - https://lucene.apache.org/core/2_9_4/queryparsersyntax.html#Fields

# The initial dashboard
![Queries 1](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/grafana/queries-1.jpg)

When you create a new dashboard, above will showes itself.
<br>
* Just return the list of the documents there in your data source index.
* No other fields are applied to do the query
* The result is grouped by time, the time field is configured during your data source configuration
* The interval is set to auto means: grafana set the bucket size by your time range. You can change the interval as you wish

# Filter using ES index field
## Change the Metric type
First thing is to change the metric type as you wish. Here I used _Average_.

![Queries 2](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/grafana/queries-2.jpg)

## Select the field you want
Now you should select the field you want to do the filtering. Here I used _age_ because this field is existed in my index.


# Reference Links
* https://cloud.ibm.com/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-define_query
* youtube - https://www.youtube.com/watch?v=mgcJPREl3CU
* https://www.youtube.com/watch?v=d6KicssNzxM
* https://www.youtube.com/watch?v=hEztaMtobXw - 就看这个
* git lab:https://docs.gitlab.com/ee/administration/monitoring/performance/grafana_configuration.html
* Grafana Blogs: https://grafana.com/blog/2016/03/09/how-to-effectively-use-the-elasticsearch-data-source-in-grafana-and-solutions-to-common-pitfalls/
* Aggregation - https://www.cnblogs.com/ghj1976/p/5311183.html
* Elastcisearch 权威指南 - https://es.xiaoleilu.com/010_Intro/35_Tutorial_Aggregations.html
* Grafana使用 - http://docs.flycloud.me/docs/ELKStack/elasticsearch/other/grafana.html
* Logstash - http://ww25.kibana.logstash.es/content/?r=&gc=pid-bodis-gtest46%2Cpid-bodis-gcontrol108&query=Logs&afdToken=3B1g_1jUOpvYh0btwvTMViS8rtlk1mkUe8MMrX-pMz_0-_jspLt8M_qBpsFs-PIiY3IJ2lrEXjKl5dgCtvVBkju1_ph6V6m4TIwhJ1OB
* ELS Stack - http://ww25.kibana.logstash.es/content/

