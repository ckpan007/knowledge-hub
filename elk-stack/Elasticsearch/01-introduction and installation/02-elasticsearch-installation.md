# Installation
The installation of Elasticsearch can be distributed into two parts:
* Use Elasticesearch hosted service on Elastic Cloud in AWS and GCP
* Install Elasticsearch via binary

## ES release references page
https://www.elastic.co/guide/en/elasticsearch/reference
<br>
For above you can get all the released ES. You should choose a specified version to install.<br>
http://www.elastic.co/downloads
For above it is a similar page.


## Installation on Ubuntu - tar
```sh
# See https://www.elastic.co/guide/en/elasticsearch/reference/6.0/_installation.html
# Uinstall the elasticsearch in case you have an old version
# Go to the directory /etc/apt/sources.list.d#
# Just remove all the other versions that you dont want.

# Get the version 6.0
cd xxx/Downloads
mkdir elasticsearch && cd elasticsearch
curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-6.0.1.tar.gz
tar -xvf elasticsearch-6.0.1.tar.gz
mv elasticsearch-6.0.1 elasticsearch

# Change the owner ship of the elasticsearch from root to elsearch
# See for more detail: https://github.com/HuangMarco/knowledge-hub/blob/dev/elk-stack/Elasticsearch/03-configuration/01-elasticsearch-config.md#create-elsearch-user-and-group-elsearch
sudo chown -R elsearch:elsearch  elasticsearch
cd elasticsearch
# Start the es
./bin/elasticsearch


```
## Installation on Ubuntu - apt install

### Uninstall the existing elasticsearch

```sh
# Go to the directory /etc/apt/sources.list.d#
# Just remove all the other versions that you dont want.

apt remove elasticsearch

# Then install the expected elasticsearch

```

```sh
# Import the ES PGP key
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -

apt-get install apt-transport-https
echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-7.x.list
apt-get update && sudo apt-get install elasticsearch


```


## Installation on Ubuntu - deb

You can go to [ES download page](https://www.elastic.co/downloads/past-releases) to seek for the specified release.
```sh

wget -o log https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.0.0-amd64.deb
sudo dpkg -i elasticsearch-2.3.4.deb

# To make sure Elasticsearch starts and stops automatically with the server, add its init script to the default runlevels.
sudo systemctl enable elasticsearch.service
systemctl start elasticsearch.service


# To tail the journal:

sudo journalctl -f

#To list journal entries for the elasticsearch service:

sudo journalctl --unit elasticsearch

# To list journal entries for the elasticsearch service starting from a given time:

sudo journalctl --unit elasticsearch --since  "2016-10-30 18:17:16"

```
Finally the **Elasticsearch** will be installed in /etc/elasticsearch/


## Installation on Ubuntu - Archive
```sh
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.0.0-linux-x86_64.tar.gz

```

## Installation with docker
Elasticsearch is also available as Docker images. The images use centos:7 as the base image.

Firstly you need to find the correct elasticsearch docker image from [docker elasticsearch repo](https://www.docker.elastic.co/#).

### Pulling the image and run

```sh
docker pull docker.elastic.co/elasticsearch/elasticsearch:7.0.0

docker run -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:7.0.0


curl http://127.0.0.1:9200/_cat/health

# Then just access http://localhost:9200/

```
For much more detail you can go to [Install Elasticsearch with Docker](https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html#docker).

### Production Mode

#### vm.max_map_count kernel setting

##### Linux
The vm.max_map_count kernel setting needs to be set to at least 262144 for production use. Depending on your platform.

```sh
# The vm.max_map_count setting should be set permanently in /etc/sysctl.conf:

$ grep vm.max_map_count /etc/sysctl.conf
vm.max_map_count=262144

```

##### macOS with Docker for Mac
```sh
# The vm.max_map_count setting must be set within the xhyve virtual machine:

$ screen ~/Library/Containers/com.docker.docker/Data/vms/0/tty
# Just press enter and configure the sysctl setting as you would for Linux:

sysctl -w vm.max_map_count=262144
```

##### Windows and macOS with Docker Toolbox
```
The vm.max_map_count setting must be set via docker-machine:

docker-machine ssh
sudo sysctl -w vm.max_map_count=262144
```


### Inspect the status of cluster
```sh
curl http://127.0.0.1:9200/_cat/health

```

## Mount the host's directory containing the elasticsearch.yml into the container
This is only applied to Linux. For more detail please check [Here in Stackflow](https://stackoverflow.com/questions/49751843/how-to-edit-elasticsearch-yml-in-a-docker-container).

```
services:
   elasticsearch:
      volumes:
        - path_to/custom_elasticsearch.yml:/usr/share/elasticsearch/config/elasticsearch.yml:ro
```

## Modify directly a relevant Dockerfile with the syntax
```
USER root
RUN echo "indices.query.bool.max_clause_count: 1000000" >> /usr/share/elasticsearch/config/elasticsearch.yml
```




## Installation using zip file
After you specifying the release number, now it is time to get the zip file.
```sh
wget -o log https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.0.0-windows-x86_64.zip

```

# Elasticsearch in Docker
https://docs.docker.com/samples/library/elasticsearch/


# Reference Links
Elasticsearch Repo: https://github.com/elastic/elasticsearch
<br>

https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-elasticsearch-on-ubuntu-16-04

https://dzone.com/articles/install-elasticsearch-on-ubuntu-18041

https://my.oschina.net/yimingkeji/blog/2978993

https://www.cnblogs.com/showtime813/p/5710829.html

https://www.elastic.co/guide/en/elasticsearch/reference/current/deb.html



