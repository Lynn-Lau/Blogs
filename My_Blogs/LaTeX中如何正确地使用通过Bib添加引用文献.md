### LaTeX中如何正确地使用通过BibTeX添加引用文献

使用LaTeX写文章的时候不可避免回添加引用文献，LaTeX中包含了很多中引用文献的方式，其中一种使用通过bib数据库的方式添加引用文献，使用这种方式引用文献也是最容易出现错误的一种。

使用BibTeX引用文献常常出现的错误有以下几种：

* bib文件内数据格式未按照正确的格式添加文献，出现错误；
* 编译tex源文件与bib文件时候的编译顺序出现错误，致使正文中无法正确显示文献引用；



针对第一个问题，我们首先确定bib文件中的文献数据是如何组织的，利用TeXworks打开空白文档，然后将下面所有数据复制粘贴到文档中，然后保存到tex文件同级目录线面，名为 "test.bib"。

```latex
%% test.bib
@article{ganti2011mobile,
  title={Mobile crowdsensing: current state and future challenges},
  author={Ganti, Raghu K and Ye, Fan and Lei, Hui},
  journal={IEEE Communications Magazine},
  volume={49},
  number={11},
  year={2011},
  publisher={IEEE}
}
```

首先，bib文件中第一行“@”后面介绍这篇文献的类型“article(文章)"，此外会有“book”之类的类型，后面花括号里面介绍“ganti2011mobile”，这是在tex文件中引用此文献时引用标签，后面几行分别介绍了这篇文献的标题、作者、期刊名称、卷号和年份等信息，每一篇文献都是以这样结构化的数据组织起来形成整篇文章的文献引用数据库。



知道了如何去组织bib文献数据库，那么如何在正文中引用数据库中的文件呢？下面先看一段代码

```latex
\documentclass[a4paper,10pt]{article}
\usepackage[utf8]{inputenc}

\title{Bibliography management: BibTeX}
\author{Lynn}

\begin{document}
\maketitle

This document is an example of BibTeX using in bibliography management. Three items are cited: \textit{The \LaTeX\ Companion} book \cite{ganti2011mobile}, the Einstein journal paper \cite{xiao2013lowering}, and the Donald Knuth's website \cite{sherchan2012using}. The \LaTeX\ related items are \cite{latexcompanion,knuthwebsite}. 
\medskip

\bibliographystyle{unsrt} %Used BibTeX style is unsrt
\bibliography{sample} %the bib file name is sammple

\end{document}
```

在这一段代码中，我们引用test.bib中的文献(`\cite{ganti2011mobile}`等)，然后经过正确的编译就可以在正文中显示正确的文献引用方式了。在这里先将这一段正文代码进行保存，保存在和bib文件同级目录下，命名bib.tex即可。



上面介绍到使用这种方法进行编译的时候由于编译顺序和编译文件的错误，经常是无法得到正确的结果。下面介绍正确的编译顺序：

1. 使用LaTeX编译bib.tex文件，编译结束之后，tex同级目录下面会生成很多文件其中包含一个*bib.aux*文件，这个文件为辅助文件，与此同时在生成的pdf文件中文献引用处出现问号；
2. 使用TeXworks打开bib.aux文件，使用BibTeX编译该文件，此时目录下面会生成更多文件其中会包含.bbl文件；
3. 使用TeXworks编辑器中LaTeX继续编译bib.tex文件，此时发现生成的PDF文件中参考文献列表生成，但是正文引用处仍然是问号；
4. 再次使用LaTeX编译bib.tex文件，PDF正文中参考文献显示正常。

**正常的文献引用如下图所示。**

![](https://lynnlaulsl.files.wordpress.com/2017/03/time688aae59bbe20170716141522.png)

