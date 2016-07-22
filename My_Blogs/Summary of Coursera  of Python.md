### Make  a Summary of Coursera of Python 

在[*Coursera*](https://www.coursera.org/)上学习的有关于Python的基础课告一段落了，已经正式结课，并且成绩也还不错。学到了不少的知识，有些知识点平时自己学习的时候会忽略，有的干脆自己学不懂，所以经过老师的讲解和课下作业，基本能够将重点知识掌握。密歇根大学的*Dr.Chuck*讲解的也很好，也很幽默，所以比较推荐学习这门课。今天想把平时自己学习过程中忽略掉的知识进行整理、总结，然后复习一下，争取能够更好的进行下一步学习。

#### 1. Conditional Execution 

Python中同样有大量的条件语句，其中自己没有学过的就是`try/except`语句。在__《Python学习手册》__中对于该语句讲解比较充分，也比较复杂，在这里只介绍简单的`try/except`语句的用法。

首先，`try/except`语句常常用来捕获程序执行的异常，或者不确定某个语句能不能正确的执行，需要使用该语句来进行实验。具体来说，`try`执行相关代码，`except`去捕捉`try`代码块中语句执行时发生的异常或错误。

* 如果`try`代码块的语句执行时候出现了异常，那么Python就会跳出`try`语句，执行`except`语句下面引发异常的语句。当`except`语句执行完之后，那么Python会执行这一`try/except`语句下面对应的代码。
* 如果`try`语句下的代码块出现了异常，但是在`except`中没有符合的句子，那么该异常就会想上传递到该`try/except`之外，然后就会出现`Traceback`，并且程序中止执行。
* 如果`try`语句下的语句执行时候没有出现错误或异常，那么Python会执行`try/except`语句（一般是`else`）语句，即不执行（跳过）`except`语句。

```python
astr = "hello"
try:
    istr = int(astr)
except:
    istr = 1
print istr
```

上面程序执行的结果`1`，因为上面`try`语句下语句无法执行，所以接着执行`except`语句的下面的语句将`istr`赋值为`1`，然后进行打印。

```python
astr = "23"
try:
    istr = int(astr)
except:
    istr = 1
print istr
```

上面程序执行的结果为``23`，`try`语句可以正确的执行，无异常，那么Python便会跳过`except`语句，所以`istr`赋值为`23`，然后打印。

#### 2. Function

##### 2.1 *arguments* & *parameters*

介绍一下函数中的两个参数，在课程中使用函数的参数称谓的时候为*__arguments__*,*__parameters__*，这两个单词都是参数的意思，但是表示的意思却不相同，所以在这里简单介绍一下。

* *__parameters__*，这个参数是我们在定义函数时候赋予函数的变量，我们称谓”**形参**“，并不是我们传给函数的实际值。*__A parameter is variable which we use in the function definition__*.

  ```python
  def addNumber(x, y):
      z = x + y
      return z
  ```

  上面定义的函数中`x, y`称谓形参，*__parameters__* 。

* *__arguments__*， 这个参数是我们引用函数时候传给函数的实际值，我们称为”**实参**“。*__An argument is a value we pass into the function  as its input when we call the function__*.

  ```python
  # addNumber(x,y) is a defined function
  addNumber(2,3)
  ```

  上面引用`addNumber()`函数的时候，`2，3`就是实参，*__arguments__* 。

##### 2.2 *return*

对函数的返回值（*__return__*），简单说明一下，在这之前不是很注意函数的返回值问题，但是在准备写课下作业的时候才发现不知道如何正确的处理返回值问题，所有又返回视频部分将返回值介绍部分重新看了一下。

其实，返回值就是调用函数时候函数运算的结果，*__A "fruitful" function is one that produces a result (return a value)__*。有的函数没有返回值，有的函数没有返回值，按道理所有的函数都应该有返回值，而那些没有返回值的函数是`return None`。

```python
>>>def greet(lang):
...    if lang == 'en':
...        return 'Hello'
...    elif lang == 'es':
...        return 'Halo'
...    elif lang == 'fr':
...        return 'Bonjour'
...
>>> print greet('en'), 'Jim'
Hello Jim
>>> print greet('es'), 'Green'
Halo Green
```

通过上面的例子可以看到函数的返回值就是该函数的执行结果。

#### 3. Strings

字符串部分掌握相对比较扎实，所以公开课上涉及到的知识都已经掌握，这里比较重要的只是有字符串的索引，分片，替换以及字符串进行迭代，去除字符串中不同位置的空格字符等知识。

在这里相对生疏没有使用过的就是字符串的替换了，字符串中字符的替换使用的关键字`replace`，包含两个过程，搜索、替换。*__The replace() function is like a "search and replace" operation in a word processor.__*

```python
>>>greet = "hello world"
>>>Greet = greet.replace('world','there')
>>>print Greet
hello there
>>>GReet = greet.replace('l','n')
>>>print GReet
henno wornd
```

通过上面的例子我们可以看出`replace()`函数在进行字符串替换的时候只要是被替换的字符串中包含符合替换条件的字符，那么所有符合条件的字符都会被替换成目标字符。

字符串中其他的函数，以及方法不继续介绍，在课后作业assignments中涉及到的方法，在相应[作业](https://github.com/Lynn-Lau/Python-Practice/blob/master/coursera%20code/coursera0.py)代码中可以找到。

#### 4. Files

Python中文件的读取也是Data Structures中重要的一部分，同样在这儿介绍关于文件的操作中自己学习过程中忽略的部分。

首先介绍一下文件的打开，我们在打开文件的时候调用的是`open()`函数对文件进行打开。`open()`是一个带有返回值的函数，返回值为`file handle`，我们常常称为**“句柄”**，其实改返回值是Python要执行的函数与硬盘上文件之间相关联的一个组件，可以称为*__Connector__*，通过这个*__Connector__*将硬盘中的文件与Python中的文件读取函数连接起来，并且不断向读取函数返回值，理解之后有助于对文件的打开更加有帮助。然后，关于文件的打开方式，比如只读、读写等不做介绍。

![file handle](https://lynnlaulsl.files.wordpress.com/2016/06/file-handle.png)

除了上面的一个文件的读取时候的概念，关于文件的读取，比如通过循环的方式逐行读取文件，在文件文中寻找某些特定的行等，同样不做介绍，关于部分代码使用在[课后作业](https://github.com/Lynn-Lau/Python-Practice/blob/master/coursera%20code/coursera1.py)的代码中可以看到。

#### 5. Collections

Python中元组(*tuples*)、列表(*lists*)、字典(*dictionaries*)统称为*__collection__*，这几个常用的collection相似性比较大，所以在此一起介绍了。

##### 5.1 List

在列表中需要注意几个小地方，易错点。

* “+”号的使用

  在列表中两个列表之间有“+”表示的并不是列表中的元素相加，而是列个列表合成一个列表。

  ```python
  >>>a = [1,2,3]
  >>>b = [4,5,6]
  >>>c = a + b
  >>>print c
  [1,2,3,4,5,6]
  ```

* 列表重元素的排序

  列表中的元素需要进行排序时，使用的`sort()`函数，但是在这里需要注意的是`sort`之后原来的列表已经排好序了，不用使用`list.sort()`。

  ```python
  >>>List = ['Joseph','Bell','Green']
  >>>List.sort()
  >>>print List
  ['Bell','Green','Joseph']
  ```

  前面使用的过程中出现了一个错误，`print List.sort()`，以为这句应该这样使用，但是出现了`Traceback`，说明使用出现了异常。

##### 5.2 Dictionary

字典中需要注意的事项在博客[字典](https://github.com/Lynn-Lau/Blogs/blob/master/My_Blogs/Coursera%20Code%20Python%202nd.md)中可以看到，在此不作介绍。

##### 5.3 Tuples

元组的介绍，见[作业](https://github.com/Lynn-Lau/Python-Practice/blob/master/coursera%20code/coursera4.py)。



