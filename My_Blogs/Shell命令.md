### Windows shell 常用命令

在Windows经常会用到的CMD窗口进行操作，在CMD使用的是命令行，shell语言，这个窗口在Linux中称为“bash”，在MacOS中称为“终端Terminal”，下面介绍在Windows常用的几个命令。

1. 切换目录命令
	在shell中操作时候如何从一个文件夹切换到另一个文件夹？
	* 切换目录
	```shell
	//切换到上一层目录
	cd..
	```
	如下图
	![切换到根目录](https://lynnlaulsl.files.wordpress.com/2016/06/qqe688aae59bbe20160623201257.png)
	连续使用上述命令便可以切换到根目录。
    
	* 切换到另外一个盘符的根目录：
	```shell
	//假如由C:\Users目录切换到D盘
	D:
	```
	![切换到D](https://lynnlaulsl.files.wordpress.com/2016/06/qqe688aae59bbe20160623204321.png)
    
	* 切换多级目录
	```shell
	cd Dir\dir\dir1
	D：
	cd Python\python study
	```
	![切换多级目录](https://lynnlaulsl.files.wordpress.com/2016/06/qqe688aae59bbe20160623205018.png)

2. tree生成目录树
	在任意文件夹下面使用*tree*命令都可以将该文件夹下面的所有文件（包括子文件夹下面的文件）的名字以树的形式显示出来。
    
    ```shell
    // 在shell界面显示该文件目录下的文件树目录
    tree
    // 将目录树生成tree.txt文件存放在文件夹查看文件目录
    tree /f>tree.txt
```
![树](https://lynnlaulsl.files.wordpress.com/2016/06/qqe688aae59bbe20160624212033.png)
*tree*命令后面还有其他的参数，在此不做过多介绍，只介绍最常见的用法。
June 25, 2016 11:52 AM