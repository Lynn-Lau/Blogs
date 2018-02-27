### Papers Summary

​        本学期从四月份开始学习论文文献，中间有其他工作安排，所以学习断断续续，文献涉及的方面有_Data Virtualization_(数据虚拟化), *Incentive Mechanism* (激励机制), *Human Mobility* (人类移动性) 等方面。下面对本学期学习过的论文文献进行总结回顾。

#### 1. Data Virtualization

​        关于数据虚拟化方面学习时间较短，只有一个星期左右，所以学习研究仍然停留在较浅的水平。学习的文章数量较少，只有两篇，分别是：*Data Virtualization*， _A New ETL Approach Based on Data Virtualization_。

##### 1.1 Data Virtualization

​        第一篇是综述性文章，文章从总体上介绍了数据虚拟化技术，并对其涉及到的相关技术进行了介绍，
本篇文献篇幅较长。

* 首先，对数据虚拟化技术进行介绍，通俗的来说就是将存放在不同的地方的不同格式的数据通过映射
  的方式将所有数据映射到同一个虚拟数据库中，好像所有的数据以同一种方式存放在同一个数据库中
  一样。通过数据虚拟化技术，将所有的数据整合之后可以集中管控与查询，方便提供商业服务。

* 然后，介绍数据虚拟化计数的必要性。随着数据体量的增大，数据分布地点与格式也多种多样，公司
  分布于不同地点，产生数据类型多种多样，如结构化数据（员工信息、财会信息等），非结构化数据
  （设备运行日志、大量文件等）。如何将这些信息进行集中管理并发掘有价值的商业信息为用户提供
  服务越来越重要，数据虚拟化技术解决了数据管理的难题。

* 然后，介绍数据虚拟化实现的方法。在数据虚拟层服务器上为虚拟数据视图定义共同规则；给需要虚
  拟化的数据源做相同的定义；根据前面定义好的虚拟数据视图按照相应的规则将数据源的数据映射到
  虚拟数据层的服务器上完成数据虚拟化。经过上面三部数据虚拟化完成，完成后所有的数据仿佛都存
  在了同一个数据库之中。

* 最后，介绍了几种常见的数据虚拟化模式。

  * *Data Warehousing* (*DW*), 数据仓

  * *Master Data Management* (*MDM*), 主数据管理

  * *Cloud Computing*, 云计算

  * *Data Management and Data Integration*, 数据管理与数据整合

    除了对上面的概念以及技术进行了介绍之外同时也介绍了一些相关案例，比如使用云计算的数据虚拟化模式的公司有哪些，如何实现的等。

##### 1.2 A New ETL Approach Based on Data Virtualization

​        第二篇文章并不是综述介绍性文章，本文主要提出了在数据虚拟化的过程中一个步骤的新的实现方
法。数据虚拟化的过程中一共有三个步骤，分别是*E-T-L*，*Extract-Transform-Load*，即“抽取-转化-加载”，
但是本文中提出的技术将原来的三个步骤变成了*T-E-L*。

​        传统的数据虚拟化步骤中存在这一定的问题：

* 存在临时数据存储区域，ETL执行效率低；
* 数据进行查询请求的时候存在数据准备阶段，所以时延较大；
* 存在这数据冗余，导致存储空间的浪费；
* 等。

​        通过将数据虚拟化的过程步骤交换一下可以免除上面问题。具体如何解决在此不做介绍。关于数据虚拟化的知识以及文献目前只有这些，因为学习时间较短，在此不做介绍。

#### 2. Task Assignments and Routing Protocols of Crowd-sensing 

​        由于阅读文献的时间的断断续续，选择文献的方向不稳定，所以选择了群智感知中的任务分发和路由协议的方向文献暂时学习。同样学习的时间很短，两片相关文献。

##### 2.1 Dynamic Data Driven Crowd Sensing Task Assignment

​        群智感知中动态数据驱动的任务分发，在移动群智感知中，由于参与者的位置以及运动路径的不确定性给群智感知的任务分发带来一定的困难。本文提出了一种通过使用最优化的动态自适应的数据驱动方案来给移动群智感知参与者分发任务。本文中的方案是通过公开的历史移动轨迹建立移动模型，并使用在其初始人物分配由噪声以及不确定测量值来确定位置值。

​        群智感之中进行任务分发的时候，会尽量将感知任务分发给距离感知目标比较近的参与者，但是因为
各种原因会出现误差，为了降低误差，提高用户位置的精确性，提出了实时动态的任务分发机制。

![](https://lynnlaulsl.files.wordpress.com/2016/06/task-assignment.png)

如上图所示，整个任务分发的过程可以分成几个步骤：

1. 根据感知任务，参与者向应用上报自己的已经收集到的数据以及他们目前的确定（不确定的）位置信
   息；
2. 将收集到的动态数据整合进行仿真模拟或者补充应用模型；
3. 报告的位置是动态的集成到一个执行移动模型中并准确的各宗参与的移动位置；
4. 执行仿真更新数据收集的目标和要求以及参与者的位置，然后通过任务分配模块使新的任务分配和引
   导将来的数据采集。

​        通过使用上面的方法不断精确自己的位置，进而使任务能够更加准确的分配到合适的参与者，然后获
得更好的数据。

##### 2.2 Integrated Routing Protocol for Opportunistic Networks

​        本文中主要介绍机会网络中的路由协议，根据以往两种路由协议的优点和缺点提出整合之后的路由协
议。

​        机会网络中常见的信息传输协议大约分为两类。

​        第一类，基于传播的传输协议。这种传输协议的优点是无论周边节点的数量是多少都会发送信息副
本，最终使信息传送到目的节点。此传输协议的缺点是大量的发送消息的副本会造成信息的拥塞，等缺
点。

​        第二类，基于上下文信息的路由协议。这种传输协议是通过知道节点之间的拓扑关系、位置关系以及
送达概率等信息来将信息进行交付，进而到达目的节点。优点是，在信息节点较多的时候传输信息可以降
低网络占用率，拥塞率。缺点是，当信息节点的数量较少的时候，信息可能不能正常的传送到目的节点。

​        基于上面两周机会网络中协议的优点和缺点，本文提出了将上面两类协议进行整合然后传输的整个协
议。无论节点数量的多少都能正常的将消息传送到目的节点。当上下文信息不可用的时候，即信息节点附
近的节点数量较少，且拓扑信息、位置信息与能够将信息成功交付给目的节点的概率信息不可知的时候，
使用基于传播的方式将其信息传播，即向附近所有节点传输其携带的信息以提高交付率；当信息节点附近
的上下文信息可用的时候，便是用基于上下文信息的传输方式传输信息，在降低网络拥塞的情况下将信息
成功的交付给目的节点。

​        文中有介绍整合协议的过程是如何进行的，以及仿真效果如何，在此不做重点介绍。

#### 3. Wi-Fi & AP (Access Point)

​        在四月末和五月份在准备学习Panabit时候学习了几篇有关于WLAN的文献，分别是_An Approximation Algorithm for AP Association under User Migration Cost Constraint_，_Monitoring Enterprise Wi-Fi Networks Using Smartphone Channel Scans_，在此一同总结一下。

##### 3.1 An Approximation Algorithm for AP Association under User Migration Cost Constraint

​        本文主要介绍用户迁移代价受限下的*AP*关联的近似算法。其主要内容是，在*WLANs*中用户的终端在与_AP_的关联并不是一成不变的，由于用户的移动会使部分用户移动出_AP_的覆盖范围，或者会有新的用户与_AP_发生关联，这样就会使_AP_之间的吞吐量也是处于变换不平衡的，也会造成网络的拥塞，如果在多个_AP_覆盖的区域，用户可以从网络拥塞大的*AP*迁移到网络拥塞小负载小的_AP_上那么可以大大减轻这种不平衡，提高用户的体验。

​        在多个用户关联的_AP_中，如果产生了网络拥塞，那么哪些用户可以迁移到负载小的_AP_，迁移到哪些_AP_中，这些问题就是本文着重研究的问题，但是目前关于该问的研究仍然是一个_NP_难得问题，所以本文介绍一种近似算法。

​                        ![](https://lynnlaulsl.files.wordpress.com/2016/06/acsaps.png)

​        如上图所示在APA上关联着四个用户，而在*APD* 上却没有关联任何用户，如果让A上的某个用户迁移到*D*上，需要花费一些代价，比如用户需要与D重新进行关联、握手认证等其他过程，那么如何在代价一定的情况下完成用户的迁移，保证用户服务质量，本文提出了*An approximation algorithm for AP re-association under migration cost constrain* (*Cost-constrained Association Control Algorithm, CACA*)，然后在*NS3*进行仿真实验并证明。

​        在本文之前也有许多学者在研究相关工作，有一些方法是周期性的由中心控制器决定目前的用户需要
于某个*AP*进行关联，这种最优化的关联方式是通过离线的优化算法根据迁移用户计算出来的；还有一些方法是在用户迁移的过程中并没有考虑其代价，这样不能保证用户的体验。本文的工作吸取上面方法的优点，避免了其缺点在代价一定的限制提出了近似的关联算法。

​        具体计算仿真过程不表。

##### 3.2 A Walk on the Client Side: Monitoring Enterprise Wifi Networks Using Smartphone Channel Scans

​        本文主要介绍在WLAN中智能手机的信道扫描数据如何被用于提高信道管理，预测*AP*故障与过载。在每个案例中通过用户侧测量产生的有价值的数据都是运营者在*AP*侧测量无法获取的，这些数据与我们实验的结果一同说明了智能手机信道扫描机的价值。

​        在本文中主要获取的数据，扫描时间戳、*SSID*和*BSSID*、*RSSI*和信道号，从*AP*侧可以获取的信息是移动终端的*MAC*地址、_AP_的_BSSID_和_SSID_、_Wi-Fi_会话的起止时间和统计会话期间转发的数据量。通过上面的数据建立AP之间信号的冲突图，然后根据冲突图合理分配AP的位置和信道。

![](https://lynnlaulsl.files.wordpress.com/2016/06/conflict-graph.png)

​        我们可以根据上面信道之间的相互冲突信道号重新分配*AP*的信道，达到频率复用。除了上面解决信道之间的相互冲突，我们可以可以通过*AP*之间数据的相互转发配合，进而计算出这些AP中哪些负载较大，哪些*AP*转发的数据量较小，然后吐过合理分配位置和信道是各个*AP*之间达到尽量的负载均衡。

#### 4. Incentive Mechanism of Crowdsensing

​        六月份学习了几篇有关与群智感知的文章，涉及到的是群智感知中的激励机制(*Incentive Mechanism*)，主要是群智感知总体上进行了解。

​        激励机制不仅应用于群智感知也应用于机会网络，延迟容忍网络和P2P网络等网络中。在群智感知网络中其主要目的是在服务器平台的管理下激励具有相应感知能力人参加感知项目，积极参与感知任务，提高质量可靠的数据。

##### 4.1 Literature Review of Incentive Mechanism

​        本文主要是对群智感知中的激励机制做了文献综述，介绍群智感知中激励机制的研究进展，常用的激励方式，在不同的研究中使用的激励方式有哪些等。

​        首先，激励机制的主要方式：

* *Monetary Reward Incentive* ，报酬支付激励。这种激励方式主要是服务器平台通过给参与用户一定的报酬来激励用户参与其中提供高质量的数据。在报酬支付中，服务器平台和参与者之间常常是通过博弈、拍卖的方式进行任务的获取或者报酬支付。常见的拍卖方式：
  * *Reverse Auction* ，逆向拍卖。这种拍卖方式是多个参与者将自己的数据以减价的形式进行拍
    卖，服务器平台选择价钱低、质量优的数据买入。
  * *Combinatorial Auction* ，组合拍卖。这种拍卖方式通常是服务器平台一次性发布多个任务，每
    个参与者可以选择多个任务进行一起感知。
  * *Multi-Attributive Auction* ， 多属性拍卖。
  * *All-pay Auction* ，全付拍卖。
  * *Others* 。

​        在报酬支付的激励下，通过博弈论以及拍卖的方式能够很好的激励用户参与其中，除此之外理论基础比较好，但是服务器平台需要付出一定的金钱报酬。

* *Entertainment & Gamification Incentive*，娱乐游戏激励。这种激励方式是指参与者进行游戏，由游戏带来的排名或者积分，然后激励用户参与其中。这种激励方式具有趣味性，能够给用户带来满足感，但是这种激励方式具有一定的局限性，并不是所有的任务都可以做成游戏的方式激励用户参与。
* *Social Relation Incentive* ，社交关系激励。这种激励方式是利用参与者形成的社交关系网来激励用户参与感知任务，通过社交关系激励来维护自己的社交关系网，提高自己的地位、荣誉等。
* *Virtual Credit Incentive* ，虚拟机分激励。这种激励方式与直接给参与者报酬的激励方式有所不同，通过给予参与用户一定的积分同样能够激励用户参与其中。
* ​