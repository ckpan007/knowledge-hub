# Installation
The installation of Elasticsearch can be distributed into two parts:
* Use Elasticesearch hosted service on Elastic Cloud in AWS and GCP
* Install Elasticsearch via binary

## Install Elasticesearch via binary
Download URL as http://www.elastic.co/downloads along with all the releases have been made in the past.

## Installation on Ubuntu - Official
```sh
curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.0.0-linux-x86_64.tar.gz
tar -xvf elasticsearch-7.0.0-linux-x86_64.tar.gz
cd elasticsearch-7.0.0/bin
./elasticsearch

```

## Installation on Ubuntu - wget
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

### Pulling the image
```sh
docker pull docker.elastic.co/elasticsearch/elasticsearch:7.0.0
docker run -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:7.0.0

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









# Reference Links

https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-elasticsearch-on-ubuntu-16-04

https://dzone.com/articles/install-elasticsearch-on-ubuntu-18041

https://my.oschina.net/yimingkeji/blog/2978993

https://www.cnblogs.com/showtime813/p/5710829.html

https://www.elastic.co/guide/en/elasticsearch/reference/current/deb.html



