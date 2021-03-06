### 如何将Visio图形转化成为eps格式的图片

在写学术论文的时候，尤其是使用LaTeX撰写学术论文经常会在文章中插入各种各样的图形，比如仿真图、拓扑图、流程图等图形，在将图形插入到LaTeX生成PDF文档的时候为了获得清晰高质量的文章需要插入一些矢量格式的图形，最常见的图形格式就是eps(embed PostScript)。由于个人喜好和绘图限制，这些图形在绘制的时候也会使用到各种绘制软件，如Matlab、Visio等绘图工具，并不是所有的工具都支持生成eps格式的图形，Matlab则可以生成eps仿真图，Visio则不然，但是我们有时候又需要通过Visio绘制一些图形，那么如何解决该问题的呢？下面我们介绍一种借助第三方工具将Visio图形转化成为eps格式的方法，算是曲线救国了。

首先，介绍需要用到的工具包括Adobe Acrobat DC、Visio 2016，这里只介绍在Windows环境下的转化过程，Mac OS不介绍。

然后，介绍整个转换过程：

* 在Visio下画好将要转换格式的图形，如下图；

  ![](https://lynnlaulsl.files.wordpress.com/2017/01/qqe688aae59bbe20170117203941.png)

* 在Visio下，选择左上角的”文件——另存为Adobe PDF“，弹出的对话框一路确定即可，在存放的路径中可以看到该Visio转化成为PDF的文件

* 通过Adobe Acrobat DC打开该PDF文件，可以看到该图形在PDF文件中，但是图形的四周空白很多，这些空白我们是不需要的，所以我们在将图形转化成为eps的同时将空白去掉。

  ![](https://lynnlaulsl.files.wordpress.com/2017/01/qqe688aae59bbe20170117204407.png)

* 打开编辑模式，选择”裁剪页面“，然后画裁剪框，将将要裁剪的部分用裁剪框划出，然后选择Acrobat的页面的”工具——组织页面“

  ![](https://lynnlaulsl.files.wordpress.com/2017/01/qqe688aae59bbe20170117204738.png)

* 然后选择将要裁剪的页面，右击选择”裁剪页面“，然后在弹出的对话框中，作出如下选择后，确定即可

  ![]()

* 裁剪结束，然后将裁剪后的图形在Acrobat的页面下面选择”另存为“选择”eps“格式即可。