### Coursera Code Python 2nd

这次代码是Python Data Structure 的字典讲解部分，主要介绍字典的常用方法，通过课后作业进行集中展示其用法。Python中的字典（*__dict__* ）前面自己学习的时候接触比较少，所以这次需要多多介绍一下基本的知识。

字典（*__dict__*）是Python中非常强大的Collection，内部存放是的数据都是通过键值（*__Key-Value__*）对的形式存储，经过哈希化的映射表，可以存放一切。

#### 1. 字典的声明/定义方式

在Python中定义字典的方式是通过下面方式：

```python
>>>Dict = dict()
```

声明`Dict`变量是一个字典的形式，其实除了字典以上面的方式声明，列表*__list__*也可以通过按照字典的方式进行声明`List = list()`，平时使用习惯列表的声明方式都是`List = []`，这次开始都使用字典的声明方式进行声明。

#### 2. 字典中需要注意知识点

* 字典中的数据是通过键值对(Key,Value)的形式存放在字典中的；

* 字典中的键值对是无序存放的；

* 字典中添加键值对的方法：

  ```python
  >>>Dict = dict()
  >>>Dict[Today] = 'Sunday'
  >>>Dict[Tomorrow] = 'Monday'
  >>>print Dcit
  {'Todya':'Sunday','Tomorrow':'Sunday'}
  ```

  列表*__list__*中添加元素的方法是`List.append()`通过特定的保留字段进行添加，字典中则无保留字段，直接添加。

#### 3. 字典可以用来计数

字典计数的代码如下：

```python
>>>Dict[key1] = 1
>>>Dict[key2] = 1
>>>Dict[key1] = Dict[key1] + 1
>>>print Dict
{'key1':2,'key2':1}
```

字典计数的功能使用了字典的一个特点，就是可以方便地修改键值对的值，比如初始化的时候 `Dict[Hello] = 1`，通过赋值语句`Dict[Hello] = 3`，那么数字**3**就会覆盖数字**1**。那么当使用字典进行计数的时候我们就可以使用如下方法：

```python
#初始化字典，counts为空
>>>counts = dict()
#key值得取值范围
>>>keys = ['hello','Python','world']
>>>for key0 in keys:
    # 当key不在counts时，将目前key添加进去
       if key0 not in counts:
           counts[key0] = 1
    # 当key在counts时，key的值做加法
       else:
           counts[key0] = counts[key0] + 1
        
>>>print counts
```

通过上面的办法，我们就可以数出要计数的文字中，每个key值出现的次数，但是上面的`for`循环循环起来比较麻烦，所以官方给了另外的语句来代替循环的方法。

```python
>>>counts = dict()
>>>keys = ['hello','Python','world']
>>>for key0 in keys:
       counts[key0] = counts.get(key0,0) + 1
    
>>>print counts
```

在上面的`counts.get(key,0)`中*__0__*是初始值，可以设定为*__任意整数值（不确定）__*。整个句子相当于循环语句的里面两句话，使用起来相对简单很多。

#### 4. 字典的迭代

同样字典中的键值对也可以通过迭代的方式进行打印输出，字典的迭代有多种方式，包括只迭代key值，只迭代value值，还包括key-Value一起迭代。

##### 4.1 只进行key值迭代

当我们对字典里的Value值不感兴趣，只需要知道包括哪些key值得时候我们就可以只对key进行迭代输出，`key`是Python中的保留值，所以可以直接使用进行迭代：

```python
>>>counts = {'hello':2,'world':3}
>>>for key in counts:
>>>    print key
```

##### 4.2 对value/key-value值进行迭代

只需要在4.1程序中的最后一行修改为`print counts[key]`即可。将键值对一起迭代只需要将上面修改为`print key,counts[key]`，便可以进行两个都输出。

除了上面的办法，在字典中key-value键值对的存在还可以看作字典内部的*__items__*：

```python
>>>print counts.items()
>>>    {('hello',2),('world',3)}
```

此时字典中的键值对组成了一个*__item__*，多个*__item__*组成了字典中的*__items__*，此时如果对字典进行迭代的时候，如果还是想要输出`hello 2 `形式的键值对，可以按照4.2中典型的输出方法。由于键值对组成了一个*__item__*，我们还可以使用如下方法进行迭代：

```python
>>>counts = {'hello':2,'world':3}
>>>for item in counts.items():
>>>    print item
>>>
('hello':2)
('world':3)
```

上面方法对字典中的*__items__*，进行了迭代，然后进行输出，得到的结果是`('hello':2)`类型的数据，即一个一个的元组形式数据。

#### 5. 示例

下面的示例代码是Coursera公开课的课后作业代码，主要是练习Python中的字典的使用方法。

```python
'''
A Simple Program for Coursera. Python Data Structure Chapter $9 Dictionary

Read the file 'mbox-short.txt' figure out who sent the most great number
of e-mails, then print it out.

Author: Lynn Lau
Date: 2016/0717
Version: 1.0
'''
# The first step: read the file
path = 'D:mbox-short.txt'
file = open(path)
List = list()
AddressList = list()
# The second step: split the lines into words
# then put the proper words into list
for line in file:
	if line.startswith('From:'):
		Line = line.split()
		List.append(Line)
#print List
index = 0
while index < len(List):
	AddressList.append(List[index][1])
	index = index + 1
	#pass
#print AddressList

# The third step: count the words 
# then put the numbers into dictionary
counts = dict()
for address in AddressList:
	counts[address] = counts.get(address,0) + 1 
	#pass
#print counts

# The forth step: print the most words & frequency
bigCount = None
bigAddress = None
for address,count in counts.items():
	if bigCount is None or count > bigCount:
		bigCount = count
		bigAddress = address

print bigAddress, bigCount
```

