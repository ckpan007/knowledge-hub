# Automatic Index Creation
It is important to note that Elasticsearch does not require you to explicitly create an index first before you can index documents into it. In the previous example, Elasticsearch will automatically create the customer index if it didn’t already exist beforehand.
<br>
Above means that usually we can directly insert document into ES without create _index_ first.
<br>
The index operation automatically creates an index if it has not been created before (check out the create index API for manually creating an index), and also automatically creates a dynamic type mapping for the specific type if one has not yet been created (check out the put mapping API for manually creating a type mapping).
<br>
For more detail see official page: https://www.elastic.co/guide/en/elasticsearch/reference/5.5/docs-index_.html#index-creation

<br>
Automatic index creation can be disabled by setting **action.auto_create_index** to false in the config file of all nodes. Automatic mapping creation can be disabled by setting index.mapper.dynamic to false per-index as an index setting.
<br>
Automatic index creation can include a pattern based white/black list, for example, set **action.auto_create_index** to +aaa*,-bbb*,+ccc*,-* (+ meaning allowed, and - meaning disallowed).

