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

* Name -
* Default -

| Name | Description |
|:---| :--- |
| Name | The data source name you define |
| Default | Default data source means that it will be pre-selected for new panels. |
| URL | Specify a complete HTTP URL (for example http://your_server:8080). Your access method is Server, this means the URL needs to be accessible from the grafana backend/server.  |
| Access | Access mode controls how requests to the data source will be handled. Server should be the preferred way if nothing else stated.  |
| Whitelisted Cookies | Grafana Proxy deletes forwarded cookies by default. Specify cookies by name that should be forwarded to the data source.  |
| Auth | For detail just check on the page |
| Elasticsearch details | For detail just check on the page |







# Create new Dashboard to use the data source

## Create new Dashboard

![New Dashboard](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/grafana/new-dashboard.jpg)

### Visualization
Click **Choose Visualization** to create _Graph, Table, Text and other types of panel.

![Choose Visualization](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/grafana/choose-visualization.jpg)

By default you will go to below page:

![Graph Visualization](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/grafana/graph-visualization.jpg)

You can also do some other changes there, such as _Axes, Draw Modes, Legend, Threshold and Time Region_.

<br>
You can add any account of panels as you wish within the dashboard.

### Queries

![Queries](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/grafana/quries.jpg)

### General

![General](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/grafana/general.jpg)

In this panel you can edit some general information about Grafana such as _panel title, description_ and so on.

### Alert

![Alert](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/grafana/alert.jpg)



