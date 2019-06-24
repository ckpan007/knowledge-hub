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
