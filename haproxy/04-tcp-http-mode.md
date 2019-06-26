# 负载均衡从哪里来
负载均衡有两种方式：
* 通过Open Systems Interconnection (OSI)第四层传输层transport layer处理
* 通过第七层application layer进行处理


## 七层网络模型

| Layer | Description |
|:---|:---|
| 1-Physical | Streams of bits are transmitted as electronic signals over wires and other physical devices |
| 2-Data Link | Converts the electronic signals from the physical layers into packets that the network layer can understand and vice versa. Protocols used by routers, NICs and other network devices are defined here. |
| 3-Network | Defines how a network device will know where to route data to and also whether incoming data is addressed to the current device. |
| 4-Transport | Ensures that multiple applications on a computer can communicate over a network at the same time. To do so, data for each application is associated with a unique port on the computer. |
| 5-Session | Allows applications that are connected over a network to participate in a shared, ongoing conversation, much like a phone conversation between two people. |
| 6-Presentation | Responsible for transforming data between machines that may represent it differently, such as converting line endings between linux and windows. |
| 7-Application | Specifices how data is interpreted by various kinds of network applications. For example, HTTP is a protocol used by web browsers for sending and receiving webpages. |


## LB与OSI Layer
有些做负载均衡的只能处理第四层，仅仅根据源和目标IP地址和端口将数据路由到服务器。但是HA可以做到更高的一层第七层应用层。这样就能够看到每个请求的headers，cookies, message bodies等等。同样HA支持第四层，你可以配置HA使得其负载均衡到第四层的请求。比如当要负载某个MYSQL的主从时，就可以不使用HTTP，而是使用TCP。

# Mode tcp
```
frontend mysql
        mode tcp
        bind *:3306
        default_backend mysqlserver

backend mysqlserver
        mode tcp
        server db1 196.168.50.10:3306
        server db2 196.168.50.11:3307
```

mode默认指向到tcp如果没显示设置的话。即便服务是基于HTTP的，我们也依然可以配置使用TCP。当你设置Mode为tcp的时候，则表示你只希望HA帮你做到第四层tcp这一层。而不去应用HA到HTTP这一层。如果你要使用HTTP，那么就要使用mode http模式。

## http能做tcp不能做的事情

* 根据URL，Http headers或者body将请求路由到特定的server
* 修改URL和请求头部信息
* 读取和设置cookies
* 根据HTTP响应决定其health check的状态

注意：**default**模式代表既适用于tcp也适用于HTTP。

# 在代理过程中遇到的最大的问题
众所周知，代理其实就是在请求过来的时候加了一层，即本该由某个服务直接接受的请求，被另外一个代理服务器所接收，然后再次转发给具体的实际处理请求的服务。那么对于实际处理请求的服务来说，代理服务器就变成了客户端。这带来的问题就是：**请求源头的一些信息，比如IP，头部信息等等，可能会丢失**。怎样捕获client的请求源信息，比如IP地址，头部等等等等。

## 配置 - 捕获请求源IP地址
其实对于HA来说，还是配置的问题，HA针对此情况，添加配置可以捕获到源信息。其实这也很好理解，什么都是HA自己的，所以无论怎样做，都是有办法的。

```
frontend mysql
        mode http
        bind *:80
        option forwardfor
        default_backend mysqlserver
```

注意上面添加的option forwardfor将会影响到所有frontend配置项里面的所有的代理。

### X-Forwarded-For
HAProxy会添加一个头部信息到所有的HTTP请求，并且将其值设置为client端的IP地址。

```
frontend mysql
        mode http
        bind *:80
        option forwardfor if-none
        default_backend mysqlserver
```
if-none表示如果某个请求中已经包含X-Forwarded-For，即已经被其他的代理添加过头部信息了，那么通过if-none表示添加而不是覆盖的行为。但是要注意：X-Forwarded-For并不是标准的HTTP协议规范内容，在RFC 7239中一个被称为Forwarded的头部信息已经被添加到了HTTP规范中。

### Forwarded
如果你想通过Forwarded来获取client的IP地址等信息，那么需要配置如下：

```
frontend mysql
        mode http
        bind *:80
        option forwardfor if-none
        http-request set-header Forwarded for=%[src]
        default_backend mysqlserver
```

按照上述设置之后，你就可以通过Forwarded来设置代理记录所有的请求的IP地址信息。


