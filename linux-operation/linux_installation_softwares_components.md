# For RedHat Enterprise


## Install Docker CE

### Install using the repository
```sh
# https://docs.docker.com/install/linux/docker-ce/centos/
# Step1: Install using the repository
yum install -y yum-utils \
device-mapper-persistent-data \
lvm2
```


```sh
#Step2: Set up the stable repository
yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
```

```sh
# enable the test channe
sudo yum-config-manager --enable docker-ce-test

# If you want to disable the nightly or test repository:
sudo yum-config-manager --disable docker-ce-nightly
```


### Install Docker CE
```sh
 yum install docker-ce docker-ce-cli containerd.io
```
#### Install sepecific docker ce
```sh
yum list docker-ce --showduplicates | sort -r

sudo yum install docker-ce-<VERSION_STRING> docker-ce-cli-<VERSION_STRING> containerd.io

```


### Start docker
```sh
systemctl start docker
docker run hello-world
```



## Linux Monitoring Tools

### Sysstat
```sh
yum search sysstat
yum install sysstat
```




## Java
### Installation on RHEL
#### Install OpenJDK 8 JRE
```sh
yum install java-1.8.0-openjdk
```
#### Install OpenJDK 8 JDK
```sh
yum install java-1.8.0-openjdk-devel
```
After installation, java and javac can be directlry used in your environment.
For more detail, see [here](https://www.digitalocean.com/community/tutorials/how-to-install-java-on-centos-and-fedora).
### Configure java environment variables
```sh
# https://access.redhat.com/documentation/en-US/JBoss_Communications_Platform/5.0/html/Platform_Installation_Guide/sect-Configuring_Java.html
export JAVA_HOME=/usr/lib/jvm/jre-1.8.0-openjdk-1.8.0.191.b12-1.el7_6.x86_64
export PATH=$JAVA_HOME/bin:$PATH
```









	
	
