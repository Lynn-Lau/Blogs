### Make  a Summary of Coursera  of Python 

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

首先，介绍一下函数中的两个参数，在课程中使用函数的参数称谓的时候为*__arguments__*,*__parameters__*，这两个单词都是参数的意思，但是表示的意思却不相同，所以在这里简单介绍一下。

* *__parameters__*，这个参数是我们在定义函数时候赋予函数的变量，我们称谓”**形参**“，并不是我们传给函数的实际值。*__A parameter is variable which we use in the function definition__*.

  ```python
  def add(x, y):
      z = x + y
      return z
  ```

  上面定义的函数中`x, y`称谓形参，*__parameters__* 。

* *__arguments__*， 这个参数是我们引用函数时候传给函数的实际值，我们称为”**实参**“。*__An argument is a value we pass into the function  as its input when we call the function__*.

  ```python
  # add(x,y) is a defined function
  add(2,3)
  ```

  上面引用`add()`函数的时候，`2，3`就是实参，*__arguments__* 。