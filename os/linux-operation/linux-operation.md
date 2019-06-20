# What is it?
This is for linux operation usage.

# Linux Operation

## 系统相关


## ssh connection

### Install openssh-server
```sh
apt-get install openssh-server
# optional- install openssh-client

```

## Linux version

```sh
cat /etc/*-release

hostnamectl
# find out the linux kernel
uname -a
uname -mrs

#check is 32bit or 64bit
uname -i

cat /proc/version

lsb_release
lsb_release -a

id
```
## User management

### Query how many users

```sh
less /etc/passwd | grep <username>

getent passwd | grep <username>

```


## Switch directory using pushd&dirs
```sh
# pushd to go to directory not cd
pushd <directoryname>

# dirs to select all parameters
dirs -v # 显示索引
dirs -p #每行显示一条记录
dirs -c 清空目录桟

pushd #不加任何参数代表在索引1和索引2中间切换

pushd +/-n #一般要先dirs -v，然后再用pushd加索引切换
```

## Software Installation
### RHEL - Red Hat Enterprise

```sh
For more: https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/deployment_guide/sec-listing_packages
yum search some-package-name
yum install some-package-name
yum list installed # list installed software
yum list all # list all softwares
yum update -y # update yum package
yum install -y <package name>

yum remove <package name> # rmove package
```



## Monitoring
### Monitoring - Sysstat
```sh

# installation
apt-get install sysstat

# Monitoring sar data collection
pushd /var/log/sar
less sar1

# Monitor CPU every 1 second for 3 times
sar -u 1 3
# Monitor all inforamtions
sar -u ALL 1 3
# 显示当天所有核心细分的CPU使用情况
sar -P 1 3

# Monitor memory
sar -r 1 3

# Swap Space Used
sar -S

# Monitor I/O activities
# tps – Transactions per second (this includes both read and write)
# rtps – Read transactions per second
# wtps – Write transactions per second
# bread/s – Bytes read per second
# bwrtn/s – Bytes written per second
sar -b 1 3



# Monitor network statistics
# DEV – Displays network devices vital statistics for eth0, eth1, etc.,
# EDEV – Display network device failure statistics
# NFS – Displays NFS client activities
# NFSD – Displays NFS server activities
# SOCK – Displays sockets in use for IPv4
# IP – Displays IPv4 network traffic
# EIP – Displays IPv4 network errors
# ICMP – Displays ICMPv4 network traffic
# EICMP – Displays ICMPv4 network errors
# TCP – Displays TCPv4 network traffic
# ETCP – Displays TCPv4 network errors
# UDP – Displays UDPv4 network traffic
# SOCK6, IP6, EIP6, ICMP6, UDP6 are for IPv6
# ALL – This displays all of the above information. The output will be very long.

sar -n KEYWORD


```


### Monitoring - ps
```sh
# Shows all the processes
ps -ef #-e - display all the processes; -f display full format listing
# Show all details
ps -aux | grep ssh
# Show process created by specific user
ps -f -u root,userone,usertwo
# Shwo process with specific pid
ps -f -p <pidnumber>
# Show all processes forked by a specific pid
ps -f --ppid <pidnumber>
# Display the process Id and commands in a hierarchy
ps -e -o pid,args --forest | grep ssh
# List all threads for a particular process (ps -L)
ps -C java -L -o pid,tid,pcpu,state,nlwp,args #显示所有的Java运行程序的详细的线程Thread
```


### Monitoring - top
```sh
# Cancel operation by clicking ESC
#Show Processes Sorted by any Top Output Column – Press O
# To sort top output by any column, Press O (upper-case O) , which will display all the possible columns that you can sort by as shown below.
# Kill a Task Without Exiting From Top – Press k
# Renice a Unix Process Without Exiting From Top – Press r
# Display Selected User in Top Output Using top -u

top -u root

# Display Only Specific Process with Given PIDs Using top -p
top -p 1309, 1882

# Display All CPUs / Cores in the Top Output – Press 1 (one)

# Highlight Running Processes in the Linux Top Command Output – Press z or b

# Display Absolute Path of the Command and its Arguments – Press c

# Quit Top Command After a Specified Number of Iterations Using top -n
# Decrease Number of Processes Displayed in Top Output – Press n

```


# Files Transfer

## SCP
http://www.hypexr.org/linux_scp_help.php









# Software Operation

## docker
```sh
# docker iamge all
docker image ls -a
#docker container -a
docker contaienr ls -a

```



# Ubuntu

## Package Management
```sh

# 查询出software name
dpkg --list #这样太不人性化，要加grep
dpkg --list | grep <关键词>

apt list --installed | grep <关键词>

apt-get --purge <software name> && apt-get autoremove

# 如果没有移除，继续执行
aptitude remove <software name>

# Installation of a package
dpkg -i PACKAGE_NAME
# Resolve the dependency if the error related with dependency show itself
sudo apt-get install -f

# Remove a package
sudo dpkg -r PACKAGE_NAME

# Reconfigure an existing package
sudo dpkg-reconfigure PACKAGE_NAME

# For more detail see https://askubuntu.com/questions/40779/how-do-i-install-a-deb-file-via-the-command-line

```

## Change VM Max Map Count
```sh
cat /proc/sys/vm/max_map_count

sysctl -w vm.max_map_count=262144

```

## wget download with log
```sh
wget -o <log file name> <download url>

tail -f <log file name>

```

## View log in Real time - 实时查看文件
```sh
tail -f <your log file>
tailf <your log file>
# The tail -F will keep track if new log file being created and will start following the new file instead of the old file.
tail -F <your log file>

# You can also use less +F
$ sudo less +F  /var/log/apache2/access.log
```

### Using Mutltitail

To install mulitail utility in Debian and RedHat based systems issue the below command.
```sh
$ sudo apt install multitail   [On Debian & Ubuntu]
$ sudo yum install multitail   [On RedHat & CentOS]
$ sudo dnf install multitail   [On Fedora 22+ version]

# To display the output of two log file simultaneous, execute the command as shown in the below example.
multitail /var/log/apache2/access.log /var/log/apache2/error.log

```

### Using lnav Command
```sh
# Lnav utility can also watch and follow multiple files and display their content in real time.

$ sudo apt install lnav   [On Debian & Ubuntu]
$ sudo yum install lnav   [On RedHat & CentOS]
$ sudo dnf install lnav   [On Fedora 22+ version]


$ sudo lnav /var/log/apache2/access.log /var/log/apache2/error.log
```



# Check VT-x or AMD-v virtualization
```sh
egrep --color 'vmx|svm' /proc/cpuinfo

# https://unix.stackexchange.com/questions/89714/easy-way-to-determine-virtualization-technology
sudo lshw -class system

```


# USTC Mirrors
https://mirrors.ustc.edu.cn/
<br>
https://mirrors.ustc.edu.cn/kubernetes/apt/pool/

