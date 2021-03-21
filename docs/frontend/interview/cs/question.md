# 面试问题

[[toc]]

:::tip 打开全部详情块

```js
document.querySelectorAll(".details").forEach((e) => (e.open = true));
```

:::

## 操作系统

### 进程和线程的区别

:::details
**进程**是并发执行的程序在执行过程中分配和管理资源的基本单位，是系统分配和调度资源的最小单位；

**线程**是进程中的一个控制单元，负责进程中程序的执行，是 CPU 调度的最小单位；一个进程有多个线程，多个线程可以共享进程的资源；
:::

## 计算机网络

### 网络七层

#### 网络七层结构及其作用？

:::details
物理层、数据链路层、网络层、传输层、会话层、表示层、应用层。

- 应用层，为应用程序提供服务，各种应用程序协议，如 HTTP、FTP、SMTP、POP3；
- 表示层，信息的语法语义以及它们的关联，如加密解密、转换翻译、压缩解压缩；
- 会话层，不同机器上的用户之间建立、管理和维护会话；
- 传输层，建立、管理和维护端到端的连接，接收上一层的数据，在必要的时候把数据进行分割，并将这些数据交给网络层，且保证这些数据端有效到达对端；
- 网络层，控制子网的运行，如逻辑编址、分组传输、路由选择；
- 数据链路层，提供介质访问和链路管理，物理寻址，同时将原始比特流转变为逻辑传输线路；
- 物理层，机械、电子、定时接口通信信道上的原始比特流传输；

TCP/IP 四层为应用层、传输层、网络层、数据链路层；
:::

#### 分层的优点？

:::details
建立七层模型的主要目的是为解决不同网络互连时所遇到的兼容性问题。它最大的优点是将服务、接口和协议这三个概念明确的区分开来（服务说明某一层为上一层提供了什么功能，接口说明了上一层如何使用下层的服务，协议说明如何实现本层服务），这样各层之间具有很强的独立性，即层次间无关性（处在高层次的系统仅是利用较低层次的系统提供接口功能，不需了解低层实现该功能所采用的算法和协议；较低层次也仅是使用从高层系统传送来的参数）。网络七层的划分也是为了使网络的不同功能模块分担不同的指责，从而带来如下好处：

- 减轻问题的复杂度，一旦网络发生故障，可迅速定位故障所在层次，便于查找和纠错；
- 在各层分别定义标准接口，使具备相同对等层的不同网络设备能实现互操作，各层之间则相对独立，一种高层协议可放在多种低层协议上运行；
- 能有效刺激网络技术革新，每次更新都可在小范围内进行，不需对修改整个网络；
- 便于讨论和学习协议的规范细节

:::

#### 网络不同层有哪些设备？

:::details
一个设备工作在哪一层，关键看它的作用或主要利用了哪一层的数据头部信息。

- 物理层：网卡、网线、集线器、中继器、调制调节器；
- 数据链路层：网桥、交换机；
- 网络层：路由器；
- 传输层及以上：网关；

:::

### HTTP 协议

#### HTTP 状态码

:::details

- 1\*\*，信息，服务器收到请求，需要请求者继续执行操作
  - 100，继续，客户端继续其请求
  - 101，切换请求协议，从 HTTP 切换到 WebSocket
- 2\*\*，成功，操作被成功接受并处理
  - 200，请求成功
- 3\*\*，重定向，需要进一步的操作以完成请求
  - 300，多种选择
  - 301，永久重定向，资源（网页等）被永久转移到其它 URL
  - 302，临时重定向
  - 304，所请求资源未修改，协商缓存命中
- 4\*\*，客户端错误，请求包含语法错误或无法完成请求
  - 400，客户端请求语法错误
  - 401，请求要求用户身份认证
  - 403，服务端禁止访问
  - 404，请求的资源不存在
- 5\*\*，服务器错误，服务器在处理请求的过程中发生错误
  - 500，服务器内部错误
  - 503，服务器繁忙

:::

#### HTTP 请求方法及用途

:::details

- GET，从指定资源中请求数据；
- HEAD，与 GET 相同，但服务器响应 HEAD 请求不会回传资源的内容部分；用于获取资源的元信息；
- POST，向指定资源提交数据；
- PUT，向指定资源提交新数据，请求服务器修改；
- DELETE，请求删除指定资源的数据；
- CONNECT，建立连接隧道，用于代理服务器；
- OPTIONS，请求指定资源所支持的 HTTP 请求方法，可以测试服务器功能是否正常；常用于跨域；
- TRACE，请求服务器回显其收到的请求信息；用于 HTTP 请求的测试或诊断。
- PATCH，与 PUT 类似，但 PATCH 用于部分更新，且资源不存在时会创建一个新的资源；

:::

#### HTTP 缓存

:::details
HTTP 缓存分为强缓存和协商缓存：

- 首先通过 Cache-Control 验证强缓存是否可用，如果强缓存可用，那么直接读取缓存
- 如果不可以，那么进入协商缓存阶段，发起 HTTP 请求，服务器通过请求头中是否带上 If-Modified-Since 和 If-None-Match 这些条件请求字段检查资源是否更新：
  - 若资源更新，那么返回资源和 200 状态码
  - 如果资源未更新，那么告诉浏览器直接使用缓存获取资源

:::

### HTTPS 协议

### DNS 协议

DNS 协议提供的是主机名到 IP 地址的转换服务，即常说的域名系统。它还是一个分层的 DNS 服务器组成的分布式数据库，是定义了主机如何查询这个分布式数据库的方式的应用层协议。DNS 协议运行在 UDP 协议 之上，使用 53 端口号。

![DNS 层次结构](https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/b54eeb16-0b0e-484c-be62-306f57c40d77.jpg)

#### DNS 查询过程

:::details
首先将 DNS 请求发送到本地 DNS 服务器，由本地 DNS 服务器来代为请求。

- 从"根域名服务器"查到"顶级域名服务器"的 NS 记录和 A 记录（ IP 地址）。
- 从"顶级域名服务器"查到"次级域名服务器"的 NS 记录和 A 记录（ IP 地址）。
- 从"次级域名服务器"查出"主机名"的 IP 地址。

例如查询 www.google.com 的 IP 地址：

- 首先向本地 DNS 服务器发送请求，本地 DNS 服务器判断是否存在缓存；如果不存在，则向根域名服务器发送一个请求，根域名服务器返回负责 .com 的顶级域名服务器的 IP 地址列表；
- 然后本地 DNS 服务器在向其中一个负责 `.com` 的顶级域名服务器发送一个请求，顶级域名服务器返回负责 `.google` 的权威域名服务器的 IP 地址列表；
- 最后本地 DNS 服务器再向其中一个权威域名服务器发送一个请求，最后权威域名服务器返回一个对应的主机名的 IP 地址列表。

:::

### TCP 和 UDP

#### TCP 和 UDP 的区别

:::details
**用户数据报协议 UDP**（User Datagram Protocol）是一种无连接的，不可靠的传输层协议。

- 面向报文
- 没有建立连接的过程，是无连接的；
- 尽最大可能交付，不保证数据的可靠交付；
- UDP 套接字只使用目的地址和目的端口来标识，所以支持一对一、一对多、多对一和多对多的交互通信；
- 没有拥塞控制和流量控制机制，报文段的发送速率没有限制；
- 适用于对实时性要求高的应用场景。

**传输控制协议 TCP**（Transmission Control Protocol）是面向连接的，
提供可靠的数据传输服务的传输层协议。

- 面向字节流（把应用层传下来的报文看成字节流，把字节流组织成大小不等的数据块）
- 面向连接，需要通过三次握手建立连接，在端系统中维护双方连接的状态信息；
- 通过序号、确认号、定时重传、检验和等机制，来提供可靠的数据传输服务；
- 端对端的服务，即单个发送方和单个接收方之间的连接；
- 提供拥塞控制和流量控制机制，控制发送数据的速率，减少数据包的丢失，保证可靠交付；
- 全双工服务，即连接双方能够向对方发送和接收数据；

:::

#### TCP 三次握手

![TCP三次握手](https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/e92d0ebc-7d46-413b-aec1-34a39602f787.png)

:::details

- 第一次握手
  - 客户端向服务端发送一个 SYN 连接请求报文段，报文段的首部中 SYN 标志位置为 1；
  - 序号字段是一个任选的随机数 $x$，代表客户端数据的初始序号。
- 第二次握手
  - 服务端接收到客户端发送到 SYN 连接请求报文段后，服务器首先会为该连接分配 TCP 缓存和变量；
  - 然后向客户端发送 SYN ACK 报文段，报文段的首部中 SYN 和 ACK 标志位都被置为 1，代表这是一个对 SYN 连接请求的确认；
  - 序号字段是服务端产生的一个任选的随机数 $y$，代表的是服务端数句的初始序号；确认号字段为客户端发送的序号加一（$x+1$）。
- 第三次握手
  - 客户端接收到服务端的肯定应答后，会为该连接分配 TCP 缓存和变量；
  - 同时向服务端放送一个对服务端报文段的确认，序号字段为 $x+1$；确认号字段为服务端发送的序号加一（$y+1$）;
  - 第三次握手可以在报文段中携带数据。

TCP 三次握手的建立连接的过程就是相互确认初始序号的过程，告诉对方，什么序号的报文段能够被正确接收。
:::

##### 三次握手的原因

:::details
第三次握手是为了防止失效的连接请求到达服务器，让服务器错误打开连接。

客户端发送的连接请求如果在网络中滞留，那么就会隔很长一段时间才能收到服务器端发回的连接确认。客户端等待一个超时重传时间之后，就会重新请求连接。但是这个滞留的连接请求最后还是会到达服务器，如果不进行三次握手，那么服务器就会打开两个连接。如果有第三次握手，客户端会忽略服务器之后发送的对滞留连接请求的连接确认，不进行第三次握手，因此就不会再次打开连接。
:::

#### TCP 四次挥手

![TCP四次挥手](https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/f87afe72-c2df-4c12-ac03-9b8d581a8af8.jpg)

:::details
因为 TCP 连接是全双工的，通信双方都可以向对方发送和接收消息，所以断开连接需要双方都确认。

- 第一次挥手
  - 客户端认为没有数据再发送给服务端，就向服务端发送一个 $\text{FIN}$ 报文段，申请断开连接；
  - 客户端进入 $\text{FIN-WAIT-1}$ 状态。
- 第二次挥手
  - 服务端接收到客户单释放连接的请求后，向客户端发送一个确认报文段，表示已经接收到客户端释放连接的请求，以后不再接收客户端发送的数据；由于连接是全双工的，此时服务器还可以向客户端发送数据；
  - 服务端进入 $\text{CLOSR-WAIT}$ 状态；
  - 客户端进入 $\text{FIN-WAIT-2}$ 状态。
- 第三次挥手
  - 服务端发送完所有数据后，向客户端发送 $\text{FIN}$ 报文，申请断开连接；
  - 服务端进入 $\text{LAST-ACK}$ 状态。
- 第四次挥手
  - 客户端接收到 $\text{FIN}$ 请求后，向服务端发送一个确认应答；
  - 客户端进入 $\text{TIME-WAIT}$ 状态，等待 2 $\text{MSL}$ （最大报文存活时间）后释放连接，客户端进入 $\text{CLOSED}$
  - 服务端收到客户端的确认报文段，服务端释放连接，服务端进入 $\text{CLOSED}$ 状态。

:::

##### 四次挥手的原因

:::details
TCP 连接是全双工的，需要双方分别释放到对方的连接，单独一方释放连接后不再向对方发送数据，连接处于半释放状态；客户端发送 $\text{FIN}$ 连接释放报文后，服务端收到后进入 $\text{CLOSE-WAIT}$ 状态，这个状态是为了让服务端发送还未传输完毕的数据，传输完毕后服务端发送 $\text{FIN}$ 连接释放报文。
:::

##### TIME_WAIT （第四次挥手的作用）

:::details

- 确保最后一个报文能够到达。如果服务端没有到客户端发来的确认报文，就会重新发送连接释放请求，客户端等待是为了处理这种情况，避免服务端连接不能正常关闭；
- 等待一段时间让本连接持续时间内所有报文都从网络中消失，使得下一个新的连接不会出现旧的连接请求报文。

:::

#### 一个 TCP 连接能够发送几个 HTTP 请求？

:::details

- HTTP 1.0 版本协议，一般情况下，不支持长连接，因此在每次请求发送完毕之后，TCP 连接即会断开，因此一个 TCP 发送一个 HTTP 请求，但是有一种情况可以将一条 TCP 连接保持在活跃状态，那就是通过 `Connection` 和 `Keep-Alive` 首部，在请求头带上 `Connection: Keep-Alive`，并且可以通过 `Keep-Alive` 通用首部中指定的，用逗号分隔的选项调节 `keep-alive` 的行为，如果客户端和服务端都支持，那么其实也可以发送多条，不过此方式也有限制，可以关注《HTTP 权威指南》4.5.5 节对于 `Keep-Alive` 连接的限制和规则。
- HTTP 1.1 版本协议，支持了长连接，因此只要 TCP 连接不断开，便可以一直发送 HTTP 请求，持续不断，没有上限；
- HTTP 2.0 版本协议，支持多用复用，一个 TCP 连接是可以并发多个 HTTP 请求的，同样也是支持长连接，因此只要不断开 TCP 的连接，HTTP 请求数也是可以没有上限地持续发送。

:::