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
## Install Docker Compose - Ubuntu
Please refer to [Docker Compose Installation](https://github.com/HuangMarco/docker-gg/blob/dev/docker-compose/docker-compose.md).




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

## Prerequisites

* docker-ce

## Declaration

Please refer to [Here](https://stackoverflow.com/questions/42294304/minikube-install-in-ubuntu-vm-vt-x-amd-v-enabling-to-vm-inside-another-vm) for much more information.
From above we realize that: 
* Virtual Box does not support VT-X/AMD-v in nested virtualisation. See this open ticket/feature request on virtualbox.org.

### Possible solutions:

* Use a different hypervisor that does support VT-X/AMD-v in nested virtualisation (like Xen, KVM or VMware).
* Install Minikube on the host OS and not in a VM.

So that we cannot run _minikube start_ within a vm which is also running in vmware workstation (不能在一个虚机上再次安装virtualbox，然后运行minikube start).
<br>
You can **directly** run _minikube start_ **in your host**, **or** you can run **minikube start --vm-driver=none** to run minikube not using virtualbox.
Also you can run **minikube config set vm-driver none** to set the minikube to run in none vm driver mode (this will try running minikube without nested virtualization (docker should be installed).



## Installation for Ubuntu OS in China - 1

### Official for outside network

```sh
# Ensure you open the Hyper-V

# Because of unauthenticated mirror, so you need to install kubectl without -y

sudo apt-get install kubectl
sudo apt-get install kubelet kubeadm kubernetes-cni
```

### Install kubectl via USTC within China

```sh
# You need to use USTC to download the .deb package files, keep in mind that the version for kubectl, kubelet, kubeadm should be the same version
# And also for the .deb file should be .amd64 but not .arf64

curl -LO https://mirrors.ustc.edu.cn/kubernetes/apt/pool/kubelet_1.14.0-00_amd64_a0b145a6601fb6c03c8f401d65c5c94cc75bf17bc7a19a00fdff44a17b6e230f.deb
curl -LO https://mirrors.ustc.edu.cn/kubernetes/apt/pool/kubectl_1.14.0-00_amd64_f6aa3b36f039aa9ce3614c08978ecbdff0900c7fc966bde6647c5d5b969dfabc.deb
curl -LO https://mirrors.ustc.edu.cn/kubernetes/apt/pool/kubeadm_1.14.0-00_amd64_37d071fc4060e54bd626faae826e8ab2750a7cb6bf90d189cea52453677df80a.deb

dpkg -i kubectl_1.14.0-00_amd64_f6aa3b36f039aa9ce3614c08978ecbdff0900c7fc966bde6647c5d5b969dfabc.deb

dpkg -i kubeadm_1.14.0-00_amd64_37d071fc4060e54bd626faae826e8ab2750a7cb6bf90d189cea52453677df80a.deb

# You meet error here and now you need to resolve the dependency

apt-get install -f

dpkg -i kubelet_1.14.0-00_amd64_a0b145a6601fb6c03c8f401d65c5c94cc75bf17bc7a19a00fdff44a17b6e230f.deb

```

### Install minikube using Aliyun within China

```sh

# After you complete the installation of the three components, then start to install minikube
# Refer to https://yangmingxiong.com/ for the minikube installation. By the way minikube version does not need to be the same with this three components

curl -Lo minikube http://kubernetes.oss-cn-hangzhou.aliyuncs.com/minikube/releases/v1.0.0/minikube-linux-amd64 && chmod +x minikube && sudo mv minikube /usr/local/bin/

# Start the minikube

minikube start --vm-driver=none --registry-mirror=https://registry.docker-cn.com --kubernetes-version v1.14.0


# Test the node
kubectl get nodes -o wide

# Open the dashboard

minikube dashboard


# The console will display information about dashboard api:
# http://127.0.0.1:38643/api/v1/namespaces/kube-system/services/http:kubernetes-dashboard:/proxy/#!/overview?namespace=default
# Open the browser and access that url you will see the overview page of kubernetes


```

## Installation for Ubuntu OS in China - 2

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

# change echo if you changed the sources.list.d
echo "deb http://mirrors.ustc.edu.cn/kubernetes/apt kubernetes-xenial main" | sudo tee -a /etc/apt/sources.list.d/kubernetes.list

sudo apt-get update
sudo apt-get install -y kubectl
```


### Trouble shooting
If you meet error by running above commands, you can try below:
```sh

```
  

# VirualBox Installation


```sh
apt-get update
apt-get upgrade

wget -q https://www.virtualbox.org/download/oracle_vbox_2016.asc -O- | sudo apt-key add -

wget -q https://www.virtualbox.org/download/oracle_vbox.asc -O- | sudo apt-key add -

add-apt-repository "deb http://download.virtualbox.org/virtualbox/debian xenial contrib"

apt-get update

apt-get install virtualbox

```

## Virtualbox installation for RHEL
```sh
# Please refer to https://www.itzgeek.com/how-tos/linux/centos-how-tos/install-virtualbox-4-3-on-centos-7-rhel-7.html for more detail

# Update the system to the latest version.

yum update
# Reboot the system.

reboot
# Once the system is up, install header and development tools.

yum install -y kernel-devel kernel-headers gcc make perl
# Also, install the wget package to download items using the terminal.

yum -y install wget
# Download the Oracle public key.

wget https://www.virtualbox.org/download/oracle_vbox.asc

# Import Oracle public key.

rpm --import oracle_vbox.asc

# Download the VirtualBox repository file for CentOS 7 / RHEL 7 and move it into /etc/yum.repos.d/ directory.

 wget http://download.virtualbox.org/virtualbox/rpm/el/virtualbox.repo -O /etc/yum.repos.d/virtualbox.repo

# OR


# Create the /etc/yum.repos.d/virtualbox.repo file with the following repository information.

```
[virtualbox]
name=Oracle Linux / RHEL / CentOS-$releasever / $basearch - VirtualBox
baseurl=http://download.virtualbox.org/virtualbox/rpm/el/$releasever/$basearch
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://www.virtualbox.org/download/oracle_vbox.asc
```

Install VirtualBox using the yum command.
```

```sh
yum install -y VirtualBox-6.0
```

VirtualBox v5.2:


```sh
yum install -y VirtualBox-5.2
```

Run the below command to check the status of VirtualBox Linux kernel module service.

```sh
systemctl status vboxdrv
```

  









	
	
