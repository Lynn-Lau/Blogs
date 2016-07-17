### Python中的函数与多态

开始在学习Python的面向对象编程的时候，总也没有找到“多态”，最近在看《Python学习手册》的时候在函数这一章介绍了多态概念。在此就借着介绍函数中的部分知识学习理解一下到底什么是Python中的“多态”。
先介绍几个函数相关的语句和表达式

| 语句     | 例子                |
| ------ | ----------------- |
| def    | def fun(a,b,...): |
| return | return a+b+c      |
| global | global X          |
| lambda |                   |
在此仅举几个例子，并介绍其功能，其他性质在此不作过多介绍。

#### 函数简介

* *def*语句与*return*
```python
def <name>(arg1,arg2,...argN):
    ...
    return <values>
```
*def*语句定义的函数主题往往都包含了一条*return*语句。按道理上说*Python*中的*return*语句可以在函数主题的任何一部分出现，但是往往出现在了函数主体的末尾。它表示函数调用的结束，并将结果返回到函数调用处。*rerurn*语句是可选的，如果没有在函数主体中出现，那么函数将会在控制流执行完函数主体时结束。从技术角度来讲，一个没有返回值得函数自动会反悔了**none**对象，但是这个只往往被忽略。

#### Python中的多态

在学习Python的面向对象编程的时候并没有提到多态，今天在此介绍一下多态，介绍多态的同时举一个小例子，算是锻炼一下自己的代码水平了:(

```python
>>>def times(x,y):
...    trturn (x*y)
...
```

上面定义了一个*times*函数如果调用此函数，如下：

```python
>>>times(2,4)
8
```

上面调用*times*函数的时候传入的两个参数为2、4，都是整形的数字，如果传入的实参不是整形的数字呢？

```python
>>>times(1.5,4)
6
>>>times('Hello',4)
'HelloHelloHelloHello'
```

上面两次对*times*函数的调用传入的实参分别是浮点型数据、整形和字符串、整形，我们可以看出*times*函数对数字做了乘法，重复了四次字符串序列。当*times*函数传入的实参数据类型不同时候“*”的操作也不同。

_注意，上面的times函数两个参数有一个为字符串时候，另外一个参数必须为整形，如果两都是字符串或者一个字符串一个浮点类型，则会报错。_

```python
>>> times("hello",2.5)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<stdin>", line 2, in times
TypeError: can't multiply sequence by non-int of type 'float'   
```

通过上面调用函数我们可以看到*times*函数中表达式```x*y```的意义完全取决于*x*和*y*的对象类型，同样的函数，在一个实例下执行的是乘法，在另一个实例下执行的是赋值。在Python中将对某一对象在某种语法的合理性交由对象自身来判断，这种依赖类型的行为便可以称为**多态**。 

介绍完多态之后，我们再通过第二个例子来认识多态。本例主要功能寻找两个序列的交集，在两个字符串中寻找相同的元素并进行输出。

首先，定义寻找交集的函数，然后调用函数。

```python
def intersect(seq1,seq2):
    res = []
    for x in seq1:
        if x in seq2:
            res.append(x)
    return res
```

调用上面函数，

```python
>>>s1 = "SPAM"
>>>s2 = "SPCM"
>>>intersect(s1,s2)
['S','P','M']
```

Python中的函数和上面的函数一样是多态的，同样*intersect*也是多态的，支持多种类型。

```python
>>>x = intersect([1,2,4],(1,4))
>>>x
[1,4]
```

这次我们给函数传递了不同类型的对象，一个列表一个元组，两个不同类型的数据，同样输出了预期的结果，所以传递的两个参数支持迭代功能即可完成上述功能，再一次体现出了Python的多态。

Python中的多态功能，增加了代码的灵活性。
June 26, 2016 3:18 PM