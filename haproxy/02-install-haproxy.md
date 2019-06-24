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

# Restart HA service
service haproxy restart


```

也是可以选择通过docker方式来安装的，但是在本文中不会包含此项。


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


# /etc/haproxy

```
root@ubuntu:/etc/haproxy# cat haproxy.cfg
global
        log /dev/log    local0
        log /dev/log    local1 notice
        chroot /var/lib/haproxy
        stats socket /run/haproxy/admin.sock mode 660 level admin
        stats timeout 30s
        user haproxy
        group haproxy
        daemon

        # Default SSL material locations
        ca-base /etc/ssl/certs
        crt-base /etc/ssl/private

        # Default ciphers to use on SSL-enabled listening sockets.
        # For more information, see ciphers(1SSL). This list is from:
        #  https://hynek.me/articles/hardening-your-web-servers-ssl-ciphers/
        ssl-default-bind-ciphers ECDH+AESGCM:DH+AESGCM:ECDH+AES256:DH+AES256:ECDH+AES128:DH+AES:ECDH+3DES:DH+3DES:RSA+AESGCM:RSA+AES:RSA+3DES:!aNULL:!MD5:!DSS
        ssl-default-bind-options no-sslv3

defaults
        log     global
        mode    http
        option  httplog
        option  dontlognull
        timeout connect 5000
        timeout client  50000
        timeout server  50000
        errorfile 400 /etc/haproxy/errors/400.http
        errorfile 403 /etc/haproxy/errors/403.http
        errorfile 408 /etc/haproxy/errors/408.http
        errorfile 500 /etc/haproxy/errors/500.http
        errorfile 502 /etc/haproxy/errors/502.http
        errorfile 503 /etc/haproxy/errors/503.http
        errorfile 504 /etc/haproxy/errors/504.http
root@ubuntu:/etc/haproxy#

```

# /etc/default/haproxy

```
root@ubuntu:/etc/default# cat haproxy
# Defaults file for HAProxy
#
# This is sourced by both, the initscript and the systemd unit file, so do not
# treat it as a shell script fragment.

# Change the config file location if needed
#CONFIG="/etc/haproxy/haproxy.cfg"

# Add extra flags here, see haproxy(1) for a few options
#EXTRAOPTS="-de -m 16"
root@ubuntu:/etc/default#

```


