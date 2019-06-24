# 实践的主要内容
当你看过第一篇General Introduction你就知道，HA所起到的作用就是将本来要发送到web server（比如Nginx）的请求代理并管理起来。那么可以这样认为，我们的实践起点可以从代理请求做起。
那么我们的实践首先的一点就是安装web server比如Nginx。

# 安装Nginx
```sh
apt update
apt install nginx -y
```

```

curl -X GET "http://localhost"
默认访问80端口


root@ubuntu:/etc/haproxy# curl -X GET "http://localhost"
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
root@ubuntu:/etc/haproxy#

```


## Nginx目录结构

| File Name | Description |
|:---|:---|
| /etc/nginx | Nginx文件的总目录 |
| /etc/nginx/nginx.conf | Nginx的配置文件 |
| /usr/share/nginx/html | Nginx的html文件 |

# 配置HA代理Nginx

## 配置frontend

```
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

frontend nginxproxy
        bind 127.0.0.1:81
        default_backend nginxwebserver

```

可以看到，上面添加了名称为nginxproxy的frontend配置项。
```
配置nginxproxy的HA的frontend配置项来做请求的代理，监听本地81端口。
```

## 配置frontend方式2

```
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

frontend nginxproxy
        bind *:81
        default_backend nginxwebserver
```
上面表示，HA所在的机器配置代表的任何IP，都将被代理。上面的“bind *:81”与“bind:81”是等效的。

## 配置frontend方式3

```
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

frontend nginxproxy
        bind 127.0.0.1:81
        bind 10.0.0.5:81
        default_backend nginxwebserver
```
上面表示，HA将新建一个新的reverse proxy代理监听针对于localhost和10.0.0.5在端口81上的请求


## HA检查配置更改的可用性

```sh

root@ubuntu:/etc/haproxy# haproxy -f /etc/haproxy/haproxy.cfg -c
[ALERT] 174/000737 (78772) : Proxy 'nginxproxy': unable to find required default_backend: 'nginxwebserver'.
[ALERT] 174/000737 (78772) : Fatal errors found in configuration.
root@ubuntu:/etc/haproxy#

```
出现上面原因是因为我们忘记配置了default_backend nginxwebserver。

## 配置default_backend nginxwebserver
我们在上面配置了前端代理服务器，监听指向到某个IP端口的请求，现在我们要配置代理这些请求之后，这些请求将被转到哪里去，就是default_backend。

```

frontend nginxproxy
        bind 127.0.0.1:81
        default_backend nginxwebserver

backend nginxwebserver
        server nginx1 127.0.0.1:80

```
可以看到我们配置了名为nginxwebserver的backend配置项。同时在其中指定frontend nginxproxy代理的请求将要被指向到后端的哪个server：nginx1 : localhost到端口80上。

```

root@ubuntu:/etc/haproxy# haproxy -f /etc/haproxy/haproxy.cfg -c
Configuration file is valid
root@ubuntu:/etc/haproxy#

```

至此，我们就完成了一个最简单的HAproxy的配置。**注意**：这里精华的地方在于，为每一个server配置了一个label标签，这点被Kubernetes借用了。

## 重启HA服务

```sh
service haproxy restart
```

## 测试代理效果
```sh
curl -X GET "http://localhost:81/"
```
代理如果成功，那么访问haproxy的配置代理服务器监听在81端口，请求将被转到backend的真正的nginx的80端口。结果如下：
```
root@ubuntu:/etc/haproxy# curl -X GET "http://localhost:81"
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
root@ubuntu:/etc/haproxy#

```

## 使用listen配置代理服务

从上面可以观察到，其实是通过配置了两端，一段frontend负责代理监听某端口的需求，一段负责将frontend引用的后端真实负责处理请求的明晰化。那么HA同样支持listen方式来糅合两种合并为一种：
```
listen myproxy
       bind *:81
       server nginx1 127.0.0.1:80
```
所起到的效果和上面两端配置效果一样。记住哈，任何一次修改了HA的配置，一定要重启HA服务。



# LB开始
从上述我们发现，我们配置了监听前端请求，然后代理请求转发到后端的某个具体的backend server负责处理具体的请求。
那么问题来了，怎样做负载均衡LB呢？所谓LB就是将请求分流，从后端多个server中抽取合适的server来负责处理用户请求，真实其中要负责的东西有很多，比如怎样记忆并保持前端请求与后端server之间的连接，让响应从后端回归到正确到前端请求上。接下来我们将来讨论并且实践这些。

```
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

frontend nginxproxy
        bind 127.0.0.1:81
        bind 10.0.0.5:81
        default_backend backendservers
backend backendservers
        balance roundrobin
        server nginx1 127.0.0.1:80
        server nginx2 192.168.50.30:80
        server nginx2 192.168.50.31:80
        server nginx2 192.168.50.32:80
```

上述新建了后端集群backendservers,官方说是a pool of backend servers。其实就是集群。集群配置使用了roundrobin算法，即轮询算法，同时配置使用了多组server来做LB。通过轮询算法在多组server中协调网络请求。通过上述的配置，我们就可以灵活多变的配置多组不同的集群，以及不同的frontend，来配置来自于不同地段的请求，将这些请求导向转发到不同的集群中。

注意：**通过将安装配置HA的虚机IP对外暴露给用户，用户访问HA的IP的某个端口，就可以起到代理的效果。而用户对于HA是无感知的。应用放置在HA后面，请求访问到应用会首先到HA，然后HA再根据配置将请求代理转发做LB**。







