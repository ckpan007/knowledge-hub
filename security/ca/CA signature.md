# 证书由来
为什么需要证书？但凡是HTTPS场景，那么就需要有证书，通过证书对通信进行加密。既然有通信，就存在调用方和服务提供方。
## 调用方
调用方调用服务提供者，调用方与服务提供者通信，既然存在通信，那么就存在验证服务提供者是否是合法且经过权威机构认证的。在此过程中就存在着权威CA认证以及自签的情况。
<br>

## 服务提供者
作为服务提供一方，为了证明自己是合法且有效的，那么服务提供一方需首先创建自己的私钥。
* 如果是赛门铁克官方CA认证 - 那么需要调用openssl命令创建csr，然后将csr交给赛门铁克，赛门铁克返回crt
* 如果是自签使用CA情况 - 那么同样需要openssl创建csr，然后根据csr，再次调用openssl命令，创建产生crt

## 证书校验流程
```
a. 客户端client访问通过HTTPS访问某个服务
   如果是第一次访问，那么浏览器会提示发现未访问过的服务，是否信任该网站上证书，用户点击信任，那么浏览器安装Root CA
   如果是银行内部系统，那么专网不会对外网进行访问，调用者也只是分布在各个网点的使用者，那么此时Root CA就需要提前安装

   如果是内部服务间调用，那么内部HTTPS通信的时候，关于证书校验会怎样？

   最终结果是客户端获得Root CA，以此作为凭证为以后校验做准备

b. 服务提供方将自己的csr提供给Root CA, Root CA根据传过来的CSR根据Root CA的私钥加密产生CA signature，CA signature加上CSR  部分共同组成CRT证书。

b. 客户端向服务端发起调用，用户校验开始(以下只讨论单向校验即校验服务提供方的情况)
   服务提供方将自己的CRT发送给调用方
   <1> 调用方使用Root CA直接解压CRT中的CA Siganature，计算出一个Hash Value
   <2> 调用方再次使用约定好的算法计算CRT中的csr部分，计算出一个Hash Value
   <3> 调用方比对计算出的2个Hash Value，结果相同那么证明证书合法有效

```

# 根证书 - Root CA
## 根证书的要素
CA只需要2类文件
* rootCA.key
* rootCA.crt
### rootCA.key
CA的私钥，如果是赛门铁克类似这种证书颁发机构，那么该证书赛门铁克不会外传。如果是自签，那么通过openssl命令，就能创建该文件。
### rootCA.crt
CA的crt，通俗来说就是根证书。通过openssl命令使用rootCA.key生成rootCA.crt。

## 根证书的作用
作为CA，有两种情况:
* 由赛门铁克权威机构作为CA
* 由开发者自己作为CA

# 服务端证书 - Server CA
Server CA也需要提供3类文件：
* serverCA.key
* serverCA.req
* serverCA.crt
根证书的作用主要用来验证**服务提供者**对外提供服务的合法有效性：
<br>

## 根证书类型
### 赛门铁克类型
如果是赛门铁克类型的CA，那么创建之初也是通过某些命令，创建一个私钥，加上对外办法的赛门铁克的CRT，私钥不外传，作为权威机构，对外只提供CRT

### 自签证书类型
如果是自签证书，那么也同样都是有私钥和CRT的。只是创建方式是由开发者调用openSSL命令创建私钥和CRT。

# 服务端证书 - Server CA
在整个TLS握手阶段


# Reference Link
https://www.shellhacks.com/create-csr-openssl-without-prompt-non-interactive/
<br>
https://gist.github.com/fntlnz/cf14feb5a46b2eda428e000157447309



