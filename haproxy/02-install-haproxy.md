# 安装HA
HA可以安装在很多Linux based的系统中。大多数情况下，我们只要使用HA的安装包安装，那么安装完成之后就可以启动运行HA了。但是如果为了拿到最新版本的HA，我们需要自己手动编辑HA的源码。在本章节中，我们将在Unbuntu中安装HA。

# 实际安装 - Ubuntu
```sh
# 安装software-properties-common package
apt install software-properties-common -y

# 引用HAProxy repository, ppa:vbernat/haproxy-1.6
add-apt-repository ppa:vbernat/haproxy-1.6

# Update Ubuntu package list
apt update

# Install haproxy package
apt install haproxy -y

# Check haproxy version
haproxy -v

# Verify haproxy service is running
service haproxy status


```

# HAProxy files
| File Name | Description |
|:---|:---|
| /usr/sbin | HA的软件运行程序 |
| /usr/share/lintian/overrides | Lintian是一个Debian package checker. |
| /usr/share/doc/haproxy | HA文档 |
| /run/haproxy | 包含一个UNIX socket，HA在启动的时候会绑定这个套接字 |
| /var/lib/haproxy | HA运行时的data所存放的目录 |
| /etc/logrotate.d/haproxy | 配置HA使用logrotate |
| /etc/default/haproxy | HA默认配置目录，比如在这里您可以更改配置让HA启动的时候到自定义目录去查找配置文件 |
| /etc/haproxy | HA的配置文件所在目录，以及当发生HTTP错误页面所在目录 |
| /etc/init.d | HA服务的初始化程序 |
