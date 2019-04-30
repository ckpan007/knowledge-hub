# Console output after set auto_reate_index to true

## Set auto_create_index to true
The default value of auto_create_index is true. For much more detail you can refer to [Here](https://www.elastic.co/guide/en/elasticsearch/reference/current/docs-index_.html).



## Create new document
Refer to [Modify the data](https://www.elastic.co/guide/en/elasticsearch/reference/current/getting-started-modify-data.html).

```sh
curl -X PUT "localhost:9200/customer/_doc/2?pretty" -H 'Content-Type: application/json' -d'
{
  "name": "Jane Doe"
}
'

```

The console will print below logs:

![Create Index](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/elasticsearch/create-index.jpg)



# Update, Delete, Batch Processing

* Update action: https://www.elastic.co/guide/en/elasticsearch/reference/current/getting-started-update-documents.html
* Delete action: https://www.elastic.co/guide/en/elasticsearch/reference/current/getting-started-delete-documents.html
* Batch Processing: https://www.elastic.co/guide/en/elasticsearch/reference/current/getting-started-batch-processing.html
