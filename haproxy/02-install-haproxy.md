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

注意：一般涉及到ha的一些行为上的变更等，主要更改配置文件发生在上面的/etc/haproxy/haproxy.cfg文件。


## haproxy.cfg详解

### global部分

| Item | Description |
|:---|:---|
| global | HA定义其自身运行进程的相关的属性，在global中可以分为多个具体的配置项 |
| log | 配置当有新的请求过来的时候，配置其syslog以及任何错误记录的路径 |
| chroot | 出于安全角度考虑，通过chroot来运行HA进程 |
| stats | 包含一个UNIX socket，HA在启动的时候会绑定这个套接字，这样用户可以通过命令行来与HA进行交互，比如enable或者disable我们设置好的代理等 |
| user和group | HA进程作为哪个user哪个group来运行， 可以通过"ps -eo user,group,args | grep haproxy"查看 |
| daemon | 配置HA使用后台方式运行 |
| /etc/default/haproxy | HA默认配置目录，比如在这里您可以更改配置让HA启动的时候到自定义目录去查找配置文件 |
| /etc/haproxy | HA的配置文件所在目录，以及当发生HTTP错误页面所在目录 |
| /etc/init.d | HA服务的初始化程序 |

```sh
root@ubuntu:/etc/haproxy# ps -eo user,group,args | grep haproxy
root     root     /usr/sbin/haproxy-systemd-wrapper -f /etc/haproxy/haproxy.cfg -p /run/haproxy.pid
haproxy  haproxy  /usr/sbin/haproxy -f /etc/haproxy/haproxy.cfg -p /run/haproxy.pid -Ds
haproxy  haproxy  /usr/sbin/haproxy -f /etc/haproxy/haproxy.cfg -p /run/haproxy.pid -Ds
root     root     grep --color=auto haproxy
root@ubuntu:/etc/haproxy#

```
### defaults部分

这部分的定义将应用于所有代理的配置项

| Item | Description |
|:---|:---|
| log global | 告诉每个代理使用HA在global中定义的log选项内容 |
| mode http | 告诉每个代理处理第七层http，而不是第四层tcp，将使得HA拥有监察HTTP消息的能力 |
| option  httplog | 打开开关来详细记录http message |
| option  dontlognull | 当某个request没有发送任何数据的时候不记录任何日志 |
| timeout connect 5000 | 请求成功连接到后端服务的最大毫秒数，超过就掐断 |
| timeout client | 等待客户端比如Nginx server响应的最大毫秒数，超过就掐断 |
| timeout server | 等待后端server给予响应的最大毫秒数，超过就掐断 |
| errorfile | 发生错误的时候返回的错误页面 |



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


