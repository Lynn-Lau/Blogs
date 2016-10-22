### H3C WX3010E 无线控制器 (Wireless Access Point Controller，AC) 配置Web服务功能

最近在学习无线网络相关知识，老师买了一套设备，但是大家都不会使用，所以只能靠大家自己摸索学习。将WX3010E这款AC开箱接入电源进行下一步使用的时候，却犯了难。官方的说明书上介绍配置AC的相关功能需要使用超级终端，同样很陌生，同样摸索前进。

#### 1. 通过Console进行登录

通过Console口进行本地登录是登录设备的最基本的方式，也是配置通过其他方式登录设备的基础，只有先从Console登录完成基本的设置，然后才可以进行下一步的配置，所以这一步必不可少。使用Console进行登录时候需要用到串口转USB接口线，当Console接口线准备之后，在PC端配置超级终端进行登录。

在使用超级终端进行登录的过程中，下图中有一个地方需要注意一下。

如果使用的是直接将串口DB-9口直接与电脑的串口连接，那么在配置超级终端的时候我们选择使用**COM1**进行连接。

 ![ConfigTER](https://lynnlaulsl.files.wordpress.com/2016/10/configter.png)

如果我们使用了DB-9和串口转USB接线口的话，将USB线接入电脑的USB接口，此时配置超级终端的时候，选择上图中的**Connect using**，选择**COM3**。官方的教程在这个问题上没有解释清楚，也直接造成我自己配置过程拖慢了很长时间，因为我使用了USB串口转接线所以尝试了很多此，自己尝试了**COM3**，出现了正确的界面才可以。

#### 2. 配置Web服务器功能设置权限

在官方的教程中这样说明：设备出厂时Web 服务器功能默认已开启，并且设置了默认的Web登录信息，用户可以直接使用该默认信息登录设备。默认的登录信息包括：用户名：“admin”，密码：“admin”，设备的Vlan-interface1接口的IP 地址：“192.168.0.100/24”。这样说明却无法登录，所以重新配置一下。

通过超级终端登录，然后配置过程如下：

```shell
<H3C>sys  //进入命令行
[H3C]interface Vlan-interface 1
[H3C-Vlan-interface1]ip address 192.168.1.100 255.255.255.0 //添加新的ip地址和掩码
[H3C-Vlan-interface1]quit
```

上面设置的部分是为WX3010E添加新的ip地址和子网掩码，用于后面部分的Web页面进行登录。下面还要设置用户权限。

```shell
[H3C]local-user admin //设置用户名为"admin"
[H3C-luser-admin]password simple admin  //设置密码为"admin"
[H3C-luser-admin]service-type telnet 
[H3C-luser-admin]quit
```

上面设置的部分是为3010设置用户权限。下面进行用户视图设置

```shell
[H3C]user vty 0 4 //进入用户视图
[H3C-ui-vty0-4]auth s //对用户进行授权
[H3C-ui-vty0-4]quit
```

将上属性信息设置完成之后，还要将其保存写入到配置文件

```shell
[H3C]save
The current configuration will be writen to the device. Are you sure?[Y/N]:Y
Please input the file name(*.cfg)[cfa0:/startup.cfg]
# 下面，机器出厂初始化的cfg文件为startup.cfg，如果将上述配置保存在自己的文件中，自己输入名字。扩展名为cfg，
# 在此我重新配置文件保存在了con.cfg文件中，如果不另存到新的文件直接点击回车键即可。
(To leave the existing file name unchaged ,press the enter key):con.cfg
Validating file. Please wait....
Configuration is saved to device successfully.
```

到此为止，通过Console口配置Web登录结束，通过浏览器输入ip地址，192.168.1.100就可以愉快的进行AC配置了。