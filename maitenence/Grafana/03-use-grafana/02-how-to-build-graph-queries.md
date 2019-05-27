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
https://cloud.ibm.com/docs/services/cloud-monitoring/grafana?topic=cloud-monitoring-define_query

<br>
youtube:
https://www.youtube.com/watch?v=mgcJPREl3CU
<br>
https://www.youtube.com/watch?v=d6KicssNzxM

<br>
https://www.youtube.com/watch?v=hEztaMtobXw - 就看这个




<br>
git lab:https://docs.gitlab.com/ee/administration/monitoring/performance/grafana_configuration.html
