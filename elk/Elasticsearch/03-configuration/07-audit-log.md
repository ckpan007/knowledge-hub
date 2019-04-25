# Before you read
Currently if you are reading configuration about version 7.0.0, I advised you move to version 6.2 for more detail. There you will find much more clear detail about the configruation. Similar with _xpack.security.audit.enabled_ this type of configuration are all configured within _elasticsearch.yml_.
<br>
https://www.elastic.co/guide/en/x-pack/current/auditing.html#auditing


# General Auditing Settings
```
xpack.security.audit.enabled

Set to true to enable auditing on the node. The default value is false. This puts the auditing events in a dedicated file named <clustername>_audit.json on each node. For more information, see [Configuring logging levels](https://www.elastic.co/guide/en/elasticsearch/reference/current/logging.html#configuring-logging-levels).
```

# Audited Security Event Settings
You can enable auditing to keep track of security-related events such as authentication failures and refused connections. Logging these events enables you to monitor your cluster for suspicious activity and provides evidence in the event of an attack.

```
Audit logs are disabled by default. To enable this functionality, you must set xpack.security.audit.enabled to true in elasticsearch.yml.
```

## X-Pack security provides two ways to persist audit logs
* The logfile output, which persists events to a dedicated _<clustername>_access.log_ file on the host’s file system
* The index output, which persists events to an Elasticsearch index. The audit index can reside on the same cluster, or a separate cluster

By default, only the logfile output is used when enabling auditing. To facilitate browsing and analyzing the events, you can also enable indexing by setting xpack.security.audit.outputs in elasticsearch.yml:
```
xpack.security.audit.outputs: [ index, logfile ]
```

# Audit Event Types
There are many event types that can be audited. Official documentation already listed them as below.
Please refer to https://www.elastic.co/guide/en/x-pack/current/auditing.html#audit-event-types for much more detail.

# Audit Event Attributes
Please also refer to official document for the attributes involved in Audit Event.
https://www.elastic.co/guide/en/x-pack/current/auditing.html#audit-event-attributes

# Logfile Audit Output
For Audit Log, there mush have some output for operator to get through and check.
<br>
The _logfile_ is the default output for auditing, that means all the audit logs will flow to the logfile as the style of the output.

## File name of the audit log
The output log file name style is always as _<clustername>_access.log_ in the log directory (default is /var/log/elasticsearch/)

## Log entry format
For each log item in the logfile output, the item looks as below:
```
[<timestamp>] [<local_node_info>] [<layer>] [<entry_type>] <attribute_list>
```

### timestamp
When the event occurred. You can configure the timestamp format in log4j2.properties.
### local_node_info
Information about the local node that generated the log entry. You can control what node information is included by configuring the [local node info settings](https://www.elastic.co/guide/en/elasticsearch/reference/6.2/auditing-settings.html#node-audit-settings).

### layer
The layer from which this event originated: rest, transport or ip_filter.
### entry_type
The type of event that occurred: anonymous_access_denied, authentication_failed, access_denied, access_granted, connection_granted, connection_denied.
### attribute_list
A comma-separated list of key-value pairs that contain data pertaining to the event. Formatted as attr1=[val1], attr2=[val2]. See Audit Entry Attributes for the attributes that can be included for each type of event.

## Configure Logfile Output
The events and some other information about what gets logged can be controlled using settings in the elasticsearch.yml file. See [Audited Event Settings](https://www.elastic.co/guide/en/elasticsearch/reference/6.2/auditing-settings.html#event-audit-settings) and  [local node info settings](https://www.elastic.co/guide/en/elasticsearch/reference/6.2/auditing-settings.html#node-audit-settings).

You can also configure how the logfile is written in the log4j2.properties file located in ES_PATH_CONF/x-pack. By default, audit information is appended to the <clustername>_access.log file located in the standard Elasticsearch logs directory (typically located at $ES_HOME/logs). The file rolls over on a daily basis.

# Ignore Policies for Audit Log
You might not want to record all the logs or you want to filter some logs that you dont want to audit, then you can refer to [Audit Log Ignore Policies](https://www.elastic.co/guide/en/x-pack/current/auditing.html#audit-log-ignore-policy).

```
xpack.security.audit.logfile.events.ignore_filters:
  example1:
    users: ["kibana", "admin_user"]
    indices: ["app-logs*"]
```

# Audit Index
Please refer to [Audit Index](https://www.elastic.co/guide/en/x-pack/current/auditing.html#audit-index).

# Reference Link
https://www.elastic.co/guide/en/elasticsearch/reference/current/auditing-settings.html#node-audit-settings

