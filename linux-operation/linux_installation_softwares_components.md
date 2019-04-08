# For RedHat Enterprise


## Install Docker CE - RHEL

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



## Install Docker CE - Ubuntu
```sh
# update package repository
apt package index
apt-get update

# install package to allow apt uses repository via https
apt-get install \
apt-transport-https \
ca-certificates \
curl \
software-properties-common

# add official docker GPG key
curl -fsSL https://download.docker.com/linux/ubuntu/gpg |sudo apt-key add -

# finger point
apt-key fingerprint 0EBFCD88

# install stable repository
add-apt-repository \
"deb [arch=amd64] https://download.docker.com/linux/ubuntu \
$(lsb_release -cs) \
 stable"

# start to install docker-CE
apt-get update
apt-get install docker-ce
```

### Accelarate docker
```sh
# Reference to link: https://www.jianshu.com/p/18441c7434a6

# Add new file under /etc/docker/daemon.json
vi /etc/docker/daemon.json
#Add below content:
{
  "registry-mirrors": ["https://docker.mirrors.ustc.edu.cn"]
}

# Restart the docker service:
sudo /etc/init.d/docker restart

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

### Maven Installation
* Download the maven package and put it into /Download<br>
  Query the version you expect: https://maven.apache.org/download.cgi
  ```sh
  wget http://artfiles.org/apache.org/maven/maven-3/3.6.0/binaries/apache-maven-3.6.0-bin.tar.gz
  # You should be certain which version of maven you want and use that version url instead of the url above
  ```
* tar the maven into the /opt<br>
  ```sh
  tar -xzvf apache-maven-3.6.0-bin.tar.gz
  ```
* Configure the M2_HOME<br>
  ```sh
  export M2_HOME=/usr/local/apache-maven/apache-maven-3.0.x
  # By inputting above command, you will configure M2_HOME, you need to use the location of your maven instead of above address: /usr/local/apache-maven/apache-mave-3.0.x
  echo $M2_HOME

  # Add the M2 environment variable
  export M2=$M2_HOME/bin

  # Add the M2 environment variable to path
  export PATH=$M2:$PATH

  vim .bashrc 
  # Add all the export into the .bashrc
    # export M2_HOME=/opt/apache-maven-3.6.0/
    # export M2=$M2_HOME/bin
    # export PATH=$M2:$PATH
  source .bashrc

  # Make sure that JAVA_HOME is set to the location of your JDK. For example
  # Make sure that $JAVA_HOME/bin is in your PATH environment variable

  # Execute below command will show maven version
  mvn -v
  ```
  For more detail, just refer to [here](https://access.redhat.com/documentation/en-us/red_hat_jboss_fuse/6.2.1/html/installation_on_jboss_eap/install_maven).


# Kubernetes

## Installation for Ubuntu
```sh
sudo apt-get update && sudo apt-get install -y apt-transport-https
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -

# If you meets error by running above CURL commands, you can try below:
# Reference to link: https://forums.docker.com/t/error-gpg-no-valid-openpgp-data-found/3857
wget https://yum.dockerproject.org/gpg
sudo apt-key add gpg

# If above still cannot resolve your issue, perhaps it is because of the ISP(Internet service provider)
# For China, becasue we cannot reach google, so that we shall need to use USTC(中国科学技术大学) mirror to install kubectl etc.
# use deb http://mirrors.ustc.edu.cn/kubernetes/apt kubernetes-xenial main instead of deb https://apt.kubernetes.io/ kubernetes-xenial main
vi /etc/apt/sources.list.d/kubernetes.list
# remove existing source of kubenetes and add deb http://mirrors.ustc.edu.cn/kubernetes/apt kubernetes-xenial main 
# more links reference to https://zhuanlan.zhihu.com/p/46341911 and https://blog.csdn.net/suresand/article/details/82321453


# continue with below command
echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee -a /etc/apt/sources.list.d/kubernetes.list
sudo apt-get update
sudo apt-get install -y kubectl

# Because of unauthenticated mirror, so you need to install kubectl without -y
sudo apt-get install kubectl
sudo apt-get install kubelet kubeadm kubernetes-cni
```
### Trouble shooting
If you meet error by running above commands, you can try below:
```sh

```
  


  









	
	
