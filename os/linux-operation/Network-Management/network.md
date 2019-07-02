# 网络管理

## 查看主机名
```sh
hostname
```

## 临时设置主机名
```sh
hostname <your host name>
```
操作系统重启之后，临时设置主机名失效。

## 永久设置主机名

```sh
vi /etc/sysconfig/network

更改其中的第二行：HOSTNAME=XXXXX
```
更改不会立即生效，需要重启使得其生效。在真实生产环境中，要更改主机名：
* 先临时更改主机名
* 更改配置文件中的主机名

上述两种配套方式使得主机名更改为我们期望的主机名

## 查看网络
```sh
ifconfig

ifconfig <具体网卡名称>

eth0是ethernet和第一块网卡的组合名，意思就是系统识别到的我们的第一块网卡

lo - 本地回环地址



```

| Resource Name | Value |
| :--- | :--- |
| inet addr | IPV4地址 |
| Bcast | 广播地址 |
| MASK | 子网掩码 |


## 查看网络 ip a

```sh
ip a
```
效果等同于上面。


## 临时修改IP地址

```sh
ifconfig <网卡名称> <ip地址>/<子网掩码>
```
仅仅临时立即生效，但是不是永久的。

## 永久修改IP地址

### setup

```sh
setup
使用上下键进入到Network configuration选项/ Device configuration

a. 取消勾选DHCP，表示不再默认由DHCP动态分配
b. static ip, netmask, 默认网关设置为192.168.100.1即可

tab切换到ok，然后保存退出即可
```

```sh
service network restart # 重启网络服务
```
所以要首先通过setup，然后重启网络服务即可永久修改虚机IP。

### 关闭激活网卡
```sh
# 默认情况下新机器的网卡是不启动的
ifdown <网卡名称> # 临时停止某网卡


ifup <网卡名称> # 临时启用某网卡
```

### 修改网卡配置文件

```sh
vi /etc/sysconfig/network-scripts/ifcfg-eth0

#上面就表示打开第一块网卡的配置文件。

onboot=no #开机的时候该网卡是启动还是不启动
bootproto=dhcp #表示动态分配IP还是静态设置IP

# 更改配置文件内容如下：
ONBOOT=yes
BOOTPROTO=none
IPADDR=192.168.100.2
NETMASK=255.255.255.0
GATEWAY=192.168.100.1
```

```sh
service network restart
```
可以发现更改生效。















