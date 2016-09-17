### Windows 配置C语言环境

最近想学习一下C语言，可是有些问题实在是犯了难。老师一开始教大家学习C语言的时候使用的是Visual C++ 6.0这个IDE都是二十多年前的了，不但不支持新的C语言标准，而且没有关键字提示，最重要的是年代久远了兼容性太差，所以不得不放弃这个IDE了。很多人推荐Visual Studio 2015，抱歉，不是我说，这个IDE即便是安装时候只勾选C++一个选项安装之后也是臃肿的不得了，将近10G的空间，而且安装的时候巨费时间，所以这个IDE也放弃了。那怎么办，到底选哪个？

自己配置一个C语言的学习环境。

介绍一下，自己是在Windows 10（x64） 环境下，配置C语言的学习环境的，如果不完全在这个环境下，请灵活掌握，谢谢。

#### 1. 安装GCC

什么是GCC？（黑人问号脸）

说真的，其实我也解释不清楚什么是GCC，只要记住GCC是由GNU开发的编程语言编译器的套件，其中就包括可以编译C语言的编译器即可。那么Windows版本下载地址呢，[我是地址](http://tdm-gcc.tdragon.net/download)，根据自己操作系统的版本选择下载GCC的版本。

![](https://lynnlaulsl.files.wordpress.com/2016/09/version.png)

选择正确的版本下载，安装的过程就是一路默认即可，默认的安装配置是将GCC套件安装在了C盘的根目录下面，并且有版本指示GCC-64， 如下图所示：

​                   ![](https://lynnlaulsl.files.wordpress.com/2016/09/index.png)

安装结束之后，测试一下安装是否正确，我们通过Windows的CMD窗口，或者通过Powershell测试都可以，打开CMD命令行，输入下列命令，出现结果如下：

```shell
C:\Users\lynn>gcc
gcc: fatal error: no input files
compilation terminated.
```

说明GCC编译器安装成功，并且环境变量已经设置好。安装GCC到此结束。

#### 2. 编写代码测试

GCC编译器安装成功了，下一步应该编写C语言的代码进行测试一下了。因为我们安装的GCC只是编译器，不能进行代码编写，所以我们需要在别的地方编写代码，推荐专业的写代码的记事本比如[notepad++](https://notepad-plus-plus.org/)，[Visual Studio Code](https://code.visualstudio.com/)，[Sublime Text](http://www.sublimetext.com/)等。这些不仅仅有代码高亮、关键词提示，而且还有许多有意思的插件，提升写代码的质量。我在这里选择了VS Code，以此为例。

首先，打开VS Code，建立新的文件并保存，在保存的时候要将该文件的扩展名保存为**.C**的形式，这样才是C语言的代码，测试代码当然是hello world。

​                                         ![](https://lynnlaulsl.files.wordpress.com/2016/09/hello-world.png)

将代码保存到相应路径，然后在改路径下打开CMD命令行，我的路径是`D:\C-Project`，在改路径下打开的CMD命令行中并输入`gcc hello.c`，然后就会该路径下生成一个名为a.exe可执行文件，此时在CMD下输入`a.exe`，就会出现`hello world`。

​                                                                    ![](https://lynnlaulsl.files.wordpress.com/2016/09/world.png)

#### 3. We made it !    : )

到此，我们便成功的在Windows 上配置了C语言的学习环境。

------



