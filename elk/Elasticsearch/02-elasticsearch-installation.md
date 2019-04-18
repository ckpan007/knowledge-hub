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
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.0.0-amd64.deb  
sudo dpkg -i elasticsearch-2.3.4.deb

# To make sure Elasticsearch starts and stops automatically with the server, add its init script to the default runlevels.
sudo systemctl enable elasticsearch.service
```


## Installation with docker
Elasticsearch is also available as Docker images. The images use centos:7 as the base image.

Firstly you need to find the correct elasticsearch docker image from [docker elasticsearch repo](https://www.docker.elastic.co/#).

### Pulling the image
```sh
docker pull docker.elastic.co/elasticsearch/elasticsearch:7.0.0

```
For much more detail you can go to [Install Elasticsearch with Docker](https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html#docker).

# Reference Links

https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-elasticsearch-on-ubuntu-16-04

https://dzone.com/articles/install-elasticsearch-on-ubuntu-18041


