### Python常用的几个函数
![台灯](https://lynnlaulsl.files.wordpress.com/2016/06/pexels-photo-112811.jpeg)
在Python中经常会见到几个函数，但是并不知道函数的作用是什么，或者会用到几个函数的作用，但是不知道如何写，如何调用，下面介绍几个自己常用常不会的函数。

#### 字符串解析常用的几个函数

*  *s.rstrip()*函数，在爬虫程序中经常见到，尤其是抓取内容之后对内容进行处理的时候，它的作用就是清除每行末尾的空白。

```python
>>>line = "The knights who say Ni\n"
>>>line.rstrip()
'The knights who say Ni'
```
 
*  *s.split()*函数 ，同样，在爬虫程序中经常见到，其作用就是分割字符串。

```python
>>>line = "aaa bbb ccc"
>>>Line = line.split()
>>>Line
['aaa','bbb','ccc']
>>>string = "aaa,bbb,ccc"
>>>String = string.split(',')
>>>String
['aaa','bbb','ccc']
>>>str = "aaaAbbbAccc"
>>>Str = str.split('A')
>>>Str
['aaa','bbb','ccc']
```
通过上面的例子我们可以看出*s.split()*函数的作用以及使用方法了，若*s.split()*函数的括号中不写东西，那么默认按照s中的空格将字符串分割；若*s.split()*的括号中填写了符号或者字母，则以符号或者字母为标识对字符串进行分割。
June 22, 2016 10:20 PM