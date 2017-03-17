### TCP/IP模型以及常用协议

关于网络的分层有两种常用的分层方法。一种是OSI七层模型包括：物理层、数据链路层、网络层、传输层、表示层、会话层、应用层，这种分层方法中分层详细，但是有些层中使用的协议不常用、较少或者没有典型的协议，在此不做讨论。一种分层方法是TCP/IP四层模型，自下而上可以分成网络接口层、网络层、运输层、应用层，这种分层方法每一层都有较多的典型协议，可以进行总结学习。

在此我们着重讨论TCP/IP四层模型。

#### TCP/IP四层模型

首先，将OSI七层模型与TCP/IP对比，如下图所示。图中TCP/IP模型的应用层对应的是OSI模型中的应用层、表示层和会话层，网络接口层对应的是数据链路层和物理层。右边提供了在TCP/IP模型中各个层的协议套件，这些都是常用协议，除此之外还有部分常考的协议在此没有列出，下面对这些协议进行分类讲解。

<img src="https://lynnlaulsl.files.wordpress.com/2017/03/ic213263.gif" width="400px" />

网络中的两台主机通过TCP/IP四层模型进行通信的过程如下：

<img src="https://lynnlaulsl.files.wordpress.com/2017/03/ip_stack_connections-svg.png" width="400px" />

#### 各层常用的协议

1. 网络接口层
   * Ethernet协议，即CSMA/CD，载波监听多点接入碰撞检测协议；
   * Token Ring，令牌环协议；
   * PPP，Point to Point Protocol，点对点协议；
   * L2TP，Layer 2 Tunneling Protocol；
   * Frame Relay，X.25；
   * ATM，异步传输模式；
2. 网络层
   * IP，IPv4、IPv6；
   * IPsec，Internet Protocol Security；
   * IGMP，Internet Group Management Protocol；网际组管理协议
   * ICMP，Internet Control Message Protocol；网际控制报文协议
   * ARP，RARP；
   * OSPF，Open Shortest Path First，开放最短路径优先；
   * RIP，
   * BGP，
   * IGRP
3. 传输层
   * TCP，Transmission Control Protocol，传输控制协议
   * UDP，User Datagram Protocol，用户数据报协议
4. 应用层
   * DNS，Domain Name Sysytem，下层使用的是UDP协议进行数据传输。
   * DHCP，Dynamic Host Configuration Protocol
   * FTP，File Transfer Protocol  两个端口20、21端口，20是数据端口，21是控制端口，下层使用的是TCP的可靠传输服务。
   * HTTP，Hyper Text Transfer Protocol 默认的端口号是80，下册使用的是TCP可靠传输服务。
   * HTTPS，Hyper Text Transfer Protocol Secure
   * IMAP，Internet Message Access Protocol
   * SIP，Session Initial Protocol 会话初始协议
   * Telnet，远程终端协议，通过TCP进行连接。
   * RADIUS，
   * POP，Post Office Protocol
   * SNMP，Simple Network Management Protocol 简单网络控制协议
   * SMTP，Short Mail Transfer Protocol 简单邮件传输协议 端口是25
   * TFTP，Trivial File Transfer Protocol 简单文件传输协议
   * SSH，Secure Shell
   * SSL，Secure Socket Layer