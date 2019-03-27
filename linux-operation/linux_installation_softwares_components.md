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


  


  









	
	
