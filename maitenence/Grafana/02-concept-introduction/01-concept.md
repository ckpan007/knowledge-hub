# Deployment Models
A cloud deployment model represents a specific type of cloud environment, primarily distinguished by ownership, size, and access. There are four common cloud deployment models: Public Clouds; Community Clouds; Private Clouds; and Hybrid Clouds. Learn more in: [IT Strategy Follows Digitalization](https://www.igi-global.com/chapter/it-strategy-follows-digitalization/212133).


# Data Source
Below datasources are supported by Grafana:
* [Graphite](https://grafana.com/docs/features/datasources/graphite/)
* [InfluxDB](https://grafana.com/docs/features/datasources/influxdb/)
* [OpenTSDB](https://grafana.com/docs/features/datasources/opentsdb/)
* [Prometheus](https://grafana.com/docs/features/datasources/prometheus/)
* [Elsticsearch](https://grafana.com/docs/features/datasources/elasticsearch/)
* [CloudWatch](https://grafana.com/docs/features/datasources/cloudwatch/)

<br>

What is Data Source?
<br>
You can think Data Source as the **storage backends** for the time series data. Different type of data source has different Query Editor. The query language and capabilities of each Data Source are obviously very different. You can combine data from multiple Data Sources onto a single Dashboard, but each Panel is tied to a specific Data Source that belongs to a particular Organization.


# Organization
* In many cases, Grafana will be deployed with a single Organization
* A single Grafana service can provider service to multiple potentially untrusted Organizations
* Each Organization can have one or more Data Sources
* All Dashboards are owned by a particular Organization
* Grafana supports multiple organizations in order to support a wide variety of deployment models

# User
* A User is a named account in Grafana
* A user can belong to one or more Organizations
* A user can be assigned different levels of privileges through roles

For more detail related with [User Auth](https://grafana.com/docs/reference/http_api/#users).


# Panel
* The Panel is the basic visualization building block in Grafana
* Each Panel provides a Query Editor
* The Panel exposes many styling and formatting options to create perfect picture
* Panels can be dragged and dropped and rearranged on the Dashboard. They can also be resized.

# Query Editor
The Query Editor exposes capabilities of your Data Source and allows you to query the metrics that it contains.
* You can and you need to use Query Editor to build one or more queries (for one or more series) in your time series database. After that the panel will instantly update allowing you to effectively explore your data in real time and build a perfect query for that particular Panel.
* You need to firstly build your Query Editor for your panel.




## Panel Types
### [Graph](https://grafana.com/docs/reference/graph/)

It allows you to graph as many metrics and series as you want.

![Graph](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/grafana/graph_overview.png)

### [Singlestat](https://grafana.com/docs/reference/singlestat/)
It requires a reduction of a single query into a single number.

![Singlestat](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/grafana/singlestat-panel.png)



### [Dashlist](https://grafana.com/docs/reference/dashlist/)

Special panels that do not connect to any Data Source.

![Dashlist](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/grafana/dashboard-list-panels.png)

### [Table](https://grafana.com/docs/reference/table_panel/)

![Table](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/grafana/table-panel.png)


### [Text](https://grafana.com/docs/reference/text/)

Special panels that do not connect to any Data Source.

![Text](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/grafana/text-options.png)



# Reference Links

| Resource Name |
|:---|
| [Deployment Model](https://www.igi-global.com/dictionary/deployment-models/59553) |
| [Top 4 Deployment Models](https://www.sam-solutions.com/blog/four-best-cloud-deployment-models-you-need-to-know/) |

