# Prerequisites
* Java 8 supported, currently java 9 not supported, you'd better use jdk nor jre
* JAVA_HOME path environment variable set

# Installation in Ubuntu - APT

## Download and install the Public Signing Key

```sh
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
```
![Public Key](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/logstash/public-key.jpg)



## Install the apt-transport-https package on Debian
```sh
sudo apt-get install apt-transport-https
```

## Save the repository definition to /etc/apt/sources.list.d/elastic-6.x.list
```sh
echo "deb https://artifacts.elastic.co/packages/6.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-6.x.list

```

## apt-get update and install
```sh
sudo apt-get update && sudo apt-get install logstash
```

![APT Installation](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/logstash/apt-installation.jpg)



# Intallation in RHEL - YUM
Refer to [Here](https://www.elastic.co/guide/en/logstash/6.2/installing-logstash.html#_yum).


# Docker running Logstash
Refer to [Here](https://www.elastic.co/guide/en/logstash/6.2/docker.html).