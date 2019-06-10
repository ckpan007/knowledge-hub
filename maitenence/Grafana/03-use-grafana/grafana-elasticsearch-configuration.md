# 配置Grafana使用ES的一些原则要点
关键词：Grafana与Elasticsearch集成， grafana with elasticsearch<br>
首先，此文章解决的是：单纯配置elasticsearch中单index与Grafana集成的场景。在集成过程中有多个地方需要注意，否则图表可能无法体现真实的index的情况。


## Grafana

* 创建data source的时候，请一定要记住输入interval的值：
![Grafana Elasticsearch 01](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/grafana/grafana-elasticsearch-01.jpg)
之前很多次配置不成功，就是因为这个值没有设置，保留为空，即使用其默认的值。

```
Interval:
A lower limit for the auto group by time interval. Recommended to be set to write frequency, for example 1m if your data is written every minute.
```
这个值可以看作是设置Grafana多久去同步一次es中的数据。设置较小的数据会导致grafana频繁的去同步ES中的数据。当我设置其为10s的数据的时候，我更改的数据就立刻被同步显示到了Grafana上。

* 创建Panel的时候，要确保连接的是正确的data source
```
一般情况下，当你只有一个数据源的时候，，那么这个数据源就是默认的数据源，也可以在创建数据源的时候，标注其成为默认的数据源。
```
* 创建Panel的时候，有以下几个地方需要注意：
![Grafana Elasticsearch 02](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/grafana/grafana-elasticsearch-02.jpg)

```
由上到下:
1. 当你在ES中添加了数据，你发现该数据没有被立即显示出来，请确保你选择了正确的时间区间
2. Query为Lucene Query，不要被这种Lucene Query迷惑，很直白的说，这个地方的query其实是Elasticsearch中的query dsl，具体可以参照链接：
https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl.html
3. Metric决定上面显示的图表的纵轴，该Metric同样参照上面第二点是ES自身的query聚集，其实就是订制化你的纵轴将要显示什么样的结果
4. Group by决定上面显示的图表的横轴，按照什么来对数据进行分组等。
```

## Elasticsearch
配置Grafana使用ES的数据源，在ES这边有很多地方需要注意，总结如下：
* 创建index的时候，可添加一个date类型的字段作为时间戳标识符。该时间戳标识符的作用在于提供一个分类依据。比如在上面Grafana Panel的时候，就可以将该field作为一个data histogram来进行分组。
* 上面的第一点是说创建Index的时候添加一个date类型的字段，而对于ES 6.0版本来说，在创建document的时候，那么就需要有一个上面date类型的字段有对应的值，即可塞到index的数据在该字段上是有值的。这样Grafana才能根据该字段显示出图表。








