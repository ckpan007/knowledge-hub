# Start
Before you start the configuration, you shall know that: **For different release of ES, the configuration is different**. The version _6.7_ is exactly not the same with _7.0_.


# Configuration for ES Deb installation
This is only for installation using deb package file.
https://www.elastic.co/guide/en/elasticsearch/reference/current/deb.html#deb-configuring

<br>
Elasticsearch defaults to using _/etc/elasticsearch_ for runtime configuration. The ownership of this directory and all files in this directory are set to _root:elasticsearch_ on package installation and the directory has the setgid flag set so that any files and subdirectories created under _/etc/elasticsearch_ are created with this ownership as well (e.g., if a keystore is created using the keystore tool). It is expected that this be maintained so that the Elasticsearch process can read the files under this directory via the group permissions.
<br>
Elasticsearch loads its configuration from the _/etc/elasticsearch/elasticsearch.yml_ file by default. The format of this config file is explained in [Configuring Elasticsearch](https://www.elastic.co/guide/en/elasticsearch/reference/current/settings.html).

The Debian package also has a system configuration file (_/etc/default/elasticsearch_), which allows you to set the following parameters:

<br>
In case you install ES by using deb package file. Then you can do the configuration by this way.


## Cofigure some configurations related with ES
Please refer to this [link](https://opensourceconnections.com/blog/2016/04/21/run-elasticsearch-in-your-shell/) for much more detail.

### Home sweet ES_HOME

First things first. The most important thing when setting up Elasticsearch is to set your ES_HOME. **ES_HOME** is an environment variable pointing **where Elasticsearch is installed**. If no other settings are specified, Elasticsearch operates **solely out of this directory**. 
<br>
For Debain package installation, the default installation directory of ES is as below:
![Default ES Installation directory]()

<br>
Open up a shell and set this all important variable:

```sh
export ES_HOME=/usr/share/elasticsearch
```

# Directory layout of ES Deb installation
https://www.elastic.co/guide/en/elasticsearch/reference/current/deb.html#deb-layout


# Configuration with Docker ES
https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html
<br>
You will be able to do the configuration in case you just use Docker Compose, and you can make your configuration in _docker-compose.yml_.
