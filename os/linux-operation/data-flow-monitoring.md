# Tools

## 监控总体带宽使用

### nload
可以读取"proc/net/dev"文件，以获得流量统计信息.
```sh
# fedora或centos 
$ yum install nload -y 
# ubuntu/debian 
$ sudo apt-get install nload 
```

![Nload](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/linux-dataflow-monitoring/nload.jpg)

### bmon
```sh
# ubuntu或debian 
$ sudo apt-get install bmon 
# fedora或centos（来自repoforge） 
$ sudo yum install bmon 
```
![bmon](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/linux-dataflow-monitoring/bmon.jpg)


### bwm-ng
可以报告摘要信息，显示进出系统上所有可用网络接口的不同数据的传输速度.
```sh
# ubuntu或debian 
$ sudo apt-get install bwm-ng 
# fedora或centos（来自epel） 
$ sudo apt-get install bwm-ng 

bwm-ng
```
![bwm-ng](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/linux-dataflow-monitoring/bwm-ng.jpg)

##  cbm：Color Bandwidth Meter
```sh
apt-get install cbm
```
![cbm](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/linux-dataflow-monitoring/cbm.jpg)


### speedometer
图形显示通过某个接口传输的入站流量和出站流量。

```sh
# ubuntu或debian用户 
$ sudo apt-get install speedometer 

ifcofnig
# -r监控入 -t监控出
speedometer -r <网卡名称> -t <网卡名称>
```
![speedometer](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/linux-dataflow-monitoring/speedometer.png)



## 监控总体带宽使用（批量式输出）

### vnstat

vnstat更像是一款制作历史报告的工具，显示每天或过去一个月使用了多少带宽。它并不是严格意义上的实时监控网络的工具。运行后台服务/守护进程，始终不停地记录所传输数据的大小。之外，它可以用来制作显示网络使用历史情况的报告。
```sh
# ubuntu或debian 
$ sudo apt-get install vnstat 
# fedora或 centos（来自epel） 
$ sudo yum install vnstat

# 运行没有任何选项的vnstat，只会显示自守护进程运行以来所传输的数据总量。
service vnstat status 

# 使用-l实时监控带宽使用情况
vnstat -l -i ens33

```

### ifstat
ifstat能够以批处理式模式显示网络带宽。输出采用的一种格式便于用户使用其他程序或实用工具来记入日志和分析.
```sh
# ubuntu, debian 
$ sudo apt-get install ifstat 
# fedora, centos（Repoforge） 
$ sudo yum install ifstat 


 ifstat -t -i eth0 0.5 
```

### dstat

用python语言编写, 可以监控系统的不同统计信息，并使用批处理模式来报告，或者将相关数据记入到CSV或类似的文件.
```sh
dstat -nt 
```

## 每个套接字连接的带宽使用

### iftop
```sh
# Centos（基本软件库） 
$ yum install iptraf 
# fedora或centos（带epel） 
$ yum install iptraf-ng -y 
# ubuntu或debian 
$ sudo apt-get install iptraf iptraf-ng 

iftop -n

```
![iftop](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/linux-dataflow-monitoring/iftop.jpg)


### iptraf
```sh
# Centos（基本软件库） 
$ yum install iptraf 
# fedora或centos（带epel） 
$ yum install iptraf-ng -y 
# ubuntu或debian 
$ sudo apt-get install iptraf iptraf-ng 
```
![iptraf](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/linux-dataflow-monitoring/iptraf.jpg)

### tcptrack
tcptrack类似iftop，使用pcap库来捕获数据包，并计算各种统计信息，比如每个连接所使用的带宽。它还支持标准的pcap过滤器，这些过滤器可用来监控特定的连接。
```sh
# ubuntu, debian 
$ sudo apt-get install tcptrack 
# fedora, centos（来自repoforge软件库） 
$ sudo yum install tcptrack 
```

![tcptrack](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/linux-dataflow-monitoring/tcptrack.jpg)

### pktstat
可以实时显示所有活动连接，并显示哪些数据通过这些活动连接传输的速度。它还可以显示连接类型，比如TCP连接或UDP连接；如果涉及HTTP连接，还会显示关于HTTP请求的详细信息。
```sh
$ sudo pktstat -i eth0 -nt 
$ sudo apt-get install pktstat 
```
![pktstat](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/linux-dataflow-monitoring/pktstat.jpg)




## 每个进程的带宽使用
### nethogs
```sh
# ubuntu或debian（默认软件库） 
$ sudo apt-get install nethogs 
# fedora或centos（来自epel） 
$ sudo yum install nethogs -y
```
![nethogs](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/linux-dataflow-monitoring/nethogs.jpg)

