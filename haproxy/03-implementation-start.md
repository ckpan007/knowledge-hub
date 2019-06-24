# 实践的主要内容
当你看过第一篇General Introduction你就知道，HA所起到的作用就是将本来要发送到web server（比如Nginx）的请求代理并管理起来。那么可以这样认为，我们的实践起点可以从代理请求做起。
那么我们的实践首先的一点就是安装web server比如Nginx。

# 安装Nginx
```sh
apt update
apt install nginx -y

```

## Nginx目录结构

| File Name | Description |
|:---|:---|
| /etc/nginx | Nginx文件的总目录 |
| /etc/nginx/nginx.conf | Nginx的配置文件 |
| /usr/share/nginx/html | Nginx的html文件 |

# 配置HA代理Nginx





