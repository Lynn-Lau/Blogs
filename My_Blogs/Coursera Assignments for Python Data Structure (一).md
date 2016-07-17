### Coursera Assignments for Python Data Structure 

​        最近在[Coursera](https://www.coursera.org/)学习Python的数据结构的一些简单知识，Coursera是不以不错的线上学习平台，不仅可以线上学习国外很多名校的课程，顺便可以练习一下英语水平，也算是一举两得了。除了能够学习线上只是之外，老师还会留了下作业，以便巩固课堂知识，但是作业都比较简单；还有线上测验，测试你本章知识的掌握程度，课程短小精悍，内容丰富，还是很值得大家学习一下的。

​        本周老师留的一道作业题是，在一个文件中寻找一些包含特定内容的行，然后对行中的内容进行提取，然后进行进一步处理。主要涉及到的知识点很多，包括**文件的读取**，**字符串的解析**，**循环的使用**，**格式化输出**等。具体先看题设与内容：

```python
'''
A Simple Program for Coursera Python Data Structure $ Chapter Seven  Files

Open a file whose name is "mbox-short.txt"
Look for lines just like "X-DSPAM-Confidence : 0.8475"
Count the lines of them and Calculate the AVERAGE Value of float numbers 

Author:Lynn-Lau
Date: 2016/07/13
'''
path = 'D:\mbox-short.txt'
file = open(path,'r')
NumberList = []
for line in file:
	Line = line.strip()
	if Line.startswith('X-DSPAM-Confidence:'):
		Number = float(Line[20:])
		NumberList.append(Number)

Index = 0
Value = 0
while Index < len(NumberList):
	Value = Value + NumberList[Index]
	Index = Index + 1

AverageValue = Value/len(NumberList)
print "Average spam confidence: %.12f" % AverageValue
```

在这而非常值得一提的就是格式化输出，在*float*类型数据输出的时候，如果`%f`那么默认的输出小数点后面的位数为**6**，超过了就进行四舍五入然后输出。如果想要输出一定位数的小数那么就要在格式化输出时候进行规定：

```python
>>>import math
#默认输出位数，不做修改
>>>print 'PI = %f' % math.pi
PI = 3.141593
#修改输出位数，保留三位小数
>>>print 'PI = %.3f' % math.pi
PI = 3.142

```

最常见的方式就是上面两种方式格式化输出，其他方式也有少见，另做补充。

除了格式化输出之外，还有就是`startswith()`函数，这个函数第一遇见并使用，一般用与字符串中，匹配字符串。注意是`startswith()`而不是`startwith()`。