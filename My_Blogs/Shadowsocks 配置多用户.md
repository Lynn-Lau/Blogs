### Shadowsocks 配置多用户

为了能够顺畅的科学上网，我们常常租用VPS，然后在VPS部署Shadowsocks服务端，在电脑或者移动终端使用Shadowsocks客户端便可以科学的使用网络。如果配置Shadowsocks服务一个人使用使用默认的配置即可，但是如果使用该VPS为多个用户提供科学上网服务，那么需要在Shadowsocks服务端配置多用户，每个用户使用各自相应的配置，如此方便用户的管理。下面介绍一下，如何在安装了Linux（Ubuntu/CentOS）操作系统的Shadowsocks 服务段配置多用户服务，**本教程是基于[Bandwagon](https://bwh1.net/index.php)服务下安装CentOS操作系统使用默认方式安装Shadowsocks的VPS**。

首先，通过SSH服务客户端远程登陆到VPS，Windows可以使用[PuTTy](http://www.putty.org/)软件登录。下载安装PuTTY，然后利用KiviVM Panel提供的SSH端口号和root密码登录，之后输入login as: root，回车，password:密码，回车即可。

<img src="https://lynnlaulsl.files.wordpress.com/2017/11/sshport.png" style="zoom:80%"/>

<img src="https://lynnlaulsl.files.wordpress.com/2017/11/putty.png" style="zoom:80%"/>

在远程登录到VPS之后，在命令行输入`vi /etc/shadowsocks.json`，然后回车即进入了Shadowsocks服务器端的配置文件编辑页，输入`i`，即可对该文件进行编辑配置，如果你是第一次对该文件进行配置，那么该文件应该为空，否则里面包括配置命令。好了，下面该配置多用户的Shadowsocks服务了，在命令行中一些输入以下代码，

```json
{
    "server":"your vps server ip",  #此处为代理VPS的IP地址
    "local_address":"127.0.0.1",
    "local_port":"1080",
    "port_password":{
    "8381":"password1",
    "8382":"password2",
    "8383":"password3",
    "8384":"password4"
    }, #此处为多用户分别对应的端口号和密码，注意逗号
    "timeout":300,
    "method":"aes-256-cfb",
    "fast_open":"false"
}
```

上面代码中配置了四个用户，可以根据实际情况自行增减，上面命令完成后，按`Esc`键，然后按`Shift`+`:`键，再然后输入`wq`，即完成了上述命令的保存，然后再按回车，退出了json文件配置环境，此时多用户配置仍然没有生效，此时在VPS上需要将Shadowsocks服务重新启动才能生效。重启Shadowsocks服务，在命令行输入，

```shell
ssserver -c /etc/shadowsocks.json -d restart
```

待Shadowsocks服务重新启动之后，测试多用户服务，如果有问题检查上述配置，直到可以使用为止。

