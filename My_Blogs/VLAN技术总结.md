### VLAN技术总结

在实验项目中由于对于VLAN技术的生疏致使项目很长时间停滞不前，不仅老师着急，自己也是无从下手。另外由于设备使用中缺少得当的文档，更是雪上加霜，束手无策。后来在另外老师的指导讲解之下，才把VLAN技术入门，设备的调试也顺手，项目开始有些起色，在此对VLAN技术做个总结。

#### 一、VLAN技术的起始

在网络设计的初期是没有VLAN的，是基于局域网(LAN)的，但是随着局域网中用户的激增，传统的局域网技术出现了各种各样的问题。例如在下图中传统的局域网中，

<img src="https://lynnlaulsl.files.wordpress.com/2017/03/vlan-summary-1.png" width="600px" />

1. 某时刻有多个节点同时发送消息，那么节点之间会发生冲突；
2. 从任意节点发出的消息都会被发送到其他节点，形成广播；
3. 局域网中所有主机共享一条数据传输通道，无法控制网络中的信息安全；

这种网络构成了一个冲突域，网络中计算机数量越多，冲突越严重，网络效率越低。同时，该网络也是一个广播域，当网络中发送信息的计算机数量越多时，广播流量将会耗费大量带宽。因此，传统局域网不仅面临冲突域太大和广播域太大两大难题，而且无法保障传输信息的安全。

为了扩展传统LAN，以接入更多计算机，同时避免冲突的恶化，出现了网桥和二层交换机，它们能有效隔离冲突域。网桥和交换机采用交换方式将来自入端口的信息转发到出端口上，克服了共享网络中的冲突问题。但是，采用交换机进行组网时，广播域和信息安全问题依旧存在。

为限制广播域的范围，减少广播流量，需要在没有二层互访需求的主机之间进行隔离。路由器是基于三层IP地址信息来选择路由和转发数据的，其连接两个网段时可以有效抑制广播报文的转发，但成本较高。因此，人们设想在物理局域网上构建多个逻辑局域网，即VLAN。

#### 二、VLAN技术简介

VLAN技术可以将一个物理局域网在逻辑上划分成多个广播域，也就是多个VLAN。VLAN技术部署在数据链路层，用于隔离二层流量。同一个VLAN内的主机共享同一个广播域，它们之间可以直接进行二层通信。而VLAN间的主机属于不同的广播域，不能直接实现二层互通。这样，广播报文就被限制在各个相应的VLAN内，同时也提高了网络安全性。 本例中，原本属于同一广播域的主机被划分到了两个VLAN中，即，VLAN1和VLAN2。VLAN内部的主机可以直接在二层互相通信，VLAN1和VLAN2之间的主机无法直接实现二层通信。

<img src="https://lynnlaulsl.files.wordpress.com/2017/03/vlan-summary-2.png" width="600px" />

在网络中实现VLAN技术就是在传输的数据帧上加上或者消除VLAN标记，然后通过识别数据帧上的标记来完成设备之间的胡同。VLAN标记是在现有的数据帧的头部直接添加，VLAN标记的长度为4个字节，这样在局域网中传输的数据可以分成两类，一类是没有添加VLAN标记的标准以太网数据帧(untagged frame)，另外一种就是添加了VLAN标记的以太网数据帧(tagged frame)。

#### 三、VLAN链路类型

VLAN链路分为两种类型：Access链路和Trunk链路。 接入链路（Access Link）：连接用户主机和交换机的链路称为接入链路。如本例所示，图中主机和交换机之间的链路都是接入链路。 干道链路（Trunk Link）：连接交换机和交换机的链路称为干道链路。如本例所示，图中交换机之间的链路都是干道链路。干道链路上通过的帧一般为带Tag的VLAN帧。

<img src="https://lynnlaulsl.files.wordpress.com/2017/03/vlan-summary-31.png" width="600px"/>

此外还有一中混合类型，混合类型的链路既可以传输Access链路类型的信息，又可以传输Trunk链路的信息。

<img src="https://lynnlaulsl.files.wordpress.com/2017/03/vlan-summary-4.png" width="600px"/>

此外，在VLAN技术的配置过程中PVID非常重要，PVID即Port VLAN ID，代表端口的缺省VLAN是一种端口属性。交换机从对端设备收到的帧有可能是Untagged的数据帧，但所有以太网帧在交换机中都是以Tagged的形式来被处理和转发的，因此交换机必须给端口收到的Untagged数据帧添加上Tag。为了实现此目的，必须为交换机配置端口的缺省VLAN。当该端口收到Untagged数据帧时，交换机将给它加上该缺省VLAN的VLAN Tag。如上图所示。

##### 端口类型Access

 <img src="https://lynnlaulsl.files.wordpress.com/2017/03/vlan-summary-5.png" width="600px" />

Access端口是交换机上用来连接用户主机的端口，它只能连接接入链路，并且只能允许唯一的VLAN ID通过本端口。 Access端口收发数据帧的规则如下：

1. 如果该端口收到对端设备发送的帧是untagged（不带VLAN标签），交换机将强制加上该端口的PVID。如果该端口收到对端设备发送的帧是tagged（带VLAN标签），交换机会检查该标签内的VLAN ID。当VLAN ID与该端口的PVID相同时，接收该报文。当VLAN ID与该端口的PVID不同时，丢弃该报文。
2. Access端口发送数据帧时，总是先剥离帧的Tag，然后再发送。Access端口发往对端设备的以太网帧永远是不带标签的帧。

在本示例中，交换机的G0/0/1，G0/0/2，G0/0/3端口分别连接三台主机，都配置为Access端口。主机A把数据帧（未加标签）发送到交换机的G0/0/1端口，再由交换机发往其他目的地。收到数据帧之后，交换机根据端口的PVID给数据帧打上VLAN标签10，然后决定从G0/0/3端口转发数据帧。G0/0/3端口的PVID也是10，与VLAN标签中的VLAN ID相同，交换机移除标签，把数据帧发送到主机C。连接主机B的端口的PVID是2，与VLAN10不属于同一个VLAN，因此此端口不会接收到VLAN10的数据帧。

##### 端口类型Trunk

<img src="https://lynnlaulsl.files.wordpress.com/2017/03/vlan-summary-6.png" width="600px" />

Trunk端口是交换机上用来和其他交换机连接的端口，它只能连接干道链路。Trunk端口允许多个VLAN的帧（带Tag标记）通过。 Trunk端口收发数据帧的规则如下：

1. 当接收到对端设备发送的不带Tag的数据帧时，会添加该端口的PVID，如果PVID在允许通过的VLAN ID列表中，则接收该报文，否则丢弃该报文。当接收到对端设备发送的带Tag的数据帧时，检查VLAN ID是否在允许通过的VLAN ID列表中。如果VLAN ID在接口允许通过的VLAN ID列表中，则接收该报文。否则丢弃该报文。
2. 端口发送数据帧时，当VLAN ID与端口的PVID相同，且是该端口允许通过的VLAN ID时，去掉Tag，发送该报文。当VLAN ID与端口的PVID不同，且是该端口允许通过的VLAN ID时，保持原有Tag，发送该报文。

在本示例中，SWA和SWB连接主机的端口为Access端口，PVID如图所示。SWA和SWB互连的端口为Trunk端口，PVID都为1，此Trunk链路允许所有VLAN的流量通过。当SWA转发VLAN1的数据帧时会剥离VLAN标签，然后发送到Trunk链路上。而在转发VLAN20的数据帧时，不剥离VLAN标签直接转发到Trunk链路上。

##### 端口类型Hybrid

<img src="https://lynnlaulsl.files.wordpress.com/2017/03/vlan-summary-7.png" width="600px" />

Access端口发往其他设备的报文，都是Untagged数据帧，而Trunk端口仅在一种特定情况下才能发出untagged数据帧，其它情况发出的都是Tagged数据帧。
Hybrid端口是交换机上既可以连接用户主机，又可以连接其他交换机的端口。Hybrid端口既可以连接接入链路又可以连接干道链路。Hybrid端口允许多个VLAN的帧通过，并可以在出端口方向将某些VLAN帧的Tag剥掉。华为设备默认的端口类型是Hybrid。
在本示例中，要求主机A和主机B都能访问服务器，但是它们之间不能互相访问。此时交换机连接主机和服务器的端口，以及交换机互连的端口都配置为Hybrid类型。交换机连接主机A的端口的PVID是2，连接主机B的端口的PVID是3，连接服务器的端口的PVID是100。

<img src="https://lynnlaulsl.files.wordpress.com/2017/03/vlan-summary-8.png" width="600px" />

Hybrid端口收发数据帧的规则如下：

1. 当接收到对端设备发送的不带Tag的数据帧时，会添加该端口的PVID，如果PVID在允许通过的VLAN ID列表中，则接收该报文，否则丢弃该报文。当接收到对端设备发送的带Tag的数据帧时，检查VLAN ID是否在允许通过的VLAN ID列表中。如果VLAN ID在接口允许通过的VLAN ID列表中，则接收该报文，否则丢弃该报文。
2. Hybrid端口发送数据帧时，将检查该接口是否允许该VLAN数据帧通过。如果允许通过，则可以通过命令配置发送时是否携带Tag。

配置port hybrid tagged vlan vlan-id命令后，接口发送该vlan-id的数据帧时，不剥离帧中的VLAN Tag，直接发送。该命令一般配置在连接交换机的端口上。

 配置port hybrid untagged vlan vlan-id命令后，接口在发送vlan-id的数据帧时，会将帧中的VLAN Tag剥离掉再发送出去。该命令一般配置在连接主机的端口上。

 本例介绍了主机A和主机B发送数据给服务器的情况。在SWA和SWB互连的端口上配置了port hybrid tagged vlan 2 3 100命令后，SWA和SWB之间的链路上传输的都是带Tag标签的数据帧。在SWB连接服务器的端口上配置了port hybrid untagged vlan 2 3，主机A和主机B发送的数据会被剥离VLAN标签后转发到服务器。