# Start
At the very beginning, when you open the home page of the Grafana web page. You will see a flow chart picture displayed on the page.

![Home Page](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/grafana/home-page.jpg)

Above presents that you already completed the installation of the Grafana, now you will follow below steps in order to display something via Grafana:
* Add new Data Source
* Create new Dashboard to use the data source
* Invite other guys to invoke into Grafana
* Install apps & plugins

# Add new Data Source
Before you start to configure dashboard you need to tell Grafana where is the data comming from. If you dont afford Grafana Data Source even you still can add new dashboard that you still get no data visualization on the page.<br>

Here I will use _Elasticsearch_ as the expected data source. Before this you should already have Elasticsearch. For more detail check [Using Elasticsearch in Grafana](https://grafana.com/docs/features/datasources/elasticsearch/).

## Add new DataSource
You will follow below steps:
* Open the side menu by clicking the Grafana icon in the top header.
* In the side menu under the Dashboards link you should find a link named Data Sources.
* Click the + Add data source button in the top header.
* Select Elasticsearch from the Type dropdown.

![Add New Data Source](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/grafana/add-new-data-source.jpg)

You should choose **Elasticsearch**:

![Source Elasticsearch](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/grafana/source-elasticsearch.jpg)

| Name | Description |
|:---| :--- |
| Name | The data source name you define |
| Default | Default data source means that it will be pre-selected for new panels. |
| URL | Specify a complete HTTP URL (for example http://your_server:8080). Your access method is Server, this means the URL needs to be accessible from the grafana backend/server.  |
| Access | Access mode controls how requests to the data source will be handled. Server should be the preferred way if nothing else stated.**Server (default)** = URL needs to be accessible from the Grafana backend/server, **Browser** = URL needs to be accessible from the browser. |
| Whitelisted Cookies | Grafana Proxy deletes forwarded cookies by default. Specify cookies by name that should be forwarded to the data source.  |
| Auth | For detail just check on the page |
| Elasticsearch details | For detail just check on the page |

### Server access mode (Default)
Check official [Server access mode](https://grafana.com/docs/features/datasources/elasticsearch/#server-access-mode-default).

### Browser (Direct) access
Check official [Browser (Direct) access](https://grafana.com/docs/features/datasources/elasticsearch/#browser-direct-access).

### Configure new DataSource

From above we know that, if you want to configure Elasticsearch as the data source, you need to do some configuration: such as added new field named _timestamp_ in your Elasticsearch index.<br>

![Add New Data Source with field](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/grafana/add-new-data-source-2.jpg)

* Now you have your Elasticsearch server running at "http://localhost:9200/"
* You have index with name customer
* You have a field named as timestamp
* Pay attention to the version of the Elasticsearch
* After clicking **Save&Test** you get message that validation is okay, index ok.

Now you are ready for your elasticsearch data source. You can proceed with the next step.

### Timestamp field
In above you have a field named as **timestamp** in your index, and you set this field as frequency you configure Grafana to send request to Elasticsearch to check the data or do something else.
* Min time interval - A lower limit for the auto group by time interval, more detail see [Min time interval](https://grafana.com/docs/features/datasources/elasticsearch/#min-time-interval)

**Notice that**: The field **timestamp** is the necessary field.


# Create new Dashboard to use the data source

Let click the **Home** button to go back to the home page. And now it is the time to create new dashboard.

## Create new Dashboard

![New Dashboard](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/grafana/new-dashboard.jpg)

## Change General Information
![General](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/grafana/general.jpg)

## Queries
Query is the most important part if you want to configure Grafana. Within this board you configure Query to decide **the panel diagram chart**.
<br>
You can add queries to decide send request by which Elasticsearch index field. You can add some **grouby** attributes and so on.


![Queries](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/grafana/queries.jpg)

From above we realize that:
* Currently we are using Elasticsearch datasource. After you added new datasource, you can see Elasticsearch showes itself here
* Metric - I shall explain later
* Group By - You can add new **Group By** items by clicking left **+ -** button
* Terms - You can select other types of this _Group By_, I shall explain later
* Currently I used **age** field which is the field of my Elasticsearch index. You can change the field you want to do the group by


## Visualization

Click **Choose Visualization** to create _Graph, Table, Text and other types of panel.

![Choose Visualization](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/grafana/choose-visualization.jpg)

By default you will go to below page:

![Graph Visualization](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/grafana/graph-visualization.jpg)

You can also do some other changes there, such as _Axes, Draw Modes, Legend, Threshold and Time Region_.

<br>
You can add any account of panels as you wish within the dashboard.



In this panel you can edit some general information about Grafana such as _panel title, description_ and so on.

### Alert

![Alert](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/grafana/alert.jpg)



