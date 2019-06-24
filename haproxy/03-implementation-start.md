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





