### Data Structure and Algorithm, DSA  Stacks

#### 1. What's a Stack?

栈（Stack，堆栈）是一种可以存储数据元素、访问数据元素、删除数据元素等操作的一种容器。在栈中元素之间没有任何相互的关系，只有元素来到的时间的先后。

栈的最主要的特点就是，所有对栈的操作只能对最后一个进入栈的元素进行操作，这种规则成为后进先出(**Last In First Out，LIFO**)。在栈中进行操作的一段称为**栈顶**，另一端称为**栈底**。通过下图我们将四个元素组成的从上至下称为一个栈，我们可以看出，从左边观察第一个进栈的元素是‘4’，依次为‘dog’，‘True’，‘8.4’，但是当我们对栈进行操作时候，我们遵从的顺序从右边的顺序，首先操作的元素为‘8.4’，依次为‘dog’，‘True’，‘4’。符合后进先出的顺序，‘4’元素作为最早入栈的元素，最后进行操作，‘8.4’作为最晚入栈的元素，最早进行操作。

​                                              ![](https://lynnlaulsl.files.wordpress.com/2016/09/simplereversal.png)

#### 2. Basic Operations

栈同样是一种抽样的数据类型ADT，其基本的操作有：

|   Operation    |     Usage      |    Description     |
| :------------: | :------------: | :----------------: |
| Stack Creation |  s = Stack()   |        创建空栈        |
|      pop       | item = s.pop() | 删除栈的最后入栈元素并返回其值，弹出 |
|      top       | item= s.top()  |  返回栈的最后入栈元素的值，不删除  |
|      push      |  s.push(item)  |     将元素item压入栈     |
|    is_empty    |   s.is_empty   |      判断栈是否为空栈      |

对于栈的上述操作，所有的复杂度都是**O(1)**。下面对几种基本操作进行分析。

1. pop，返回栈的最后入栈的元素值，并删除

   * 检查栈是否为空栈
   * 如果栈是空栈，返回错误值并结束
   * 如果不是空栈，指向最后一个入栈的元素
   * 将最后一个入栈的元素删除
   * 返回删除元素的值，成功

   ​                               ![](https://lynnlaulsl.files.wordpress.com/2016/09/stack_pop_operation.jpg)

2. push，将元素压入栈

   * 检查栈是否已经满栈
   * 如果栈元素已经满了，返回错误并结束
   * 如果栈未满，指向空位置
   * 将元素压入栈，到指向的位置
   * 返回成功

   ​                                ![](https://lynnlaulsl.files.wordpress.com/2016/09/stack_push_operation.jpg)


在Python的数据结构和算法中，我们使用Python中内建(Buid-in)函数`list`来实现栈的各项操作，除了使用列表函数实现栈的功能还可以使用其他的顺序结构，比如链表等，在此我们以列表函数使用举例。

* 初始化栈

  ```python
  class stack:
      def __init__(self):
          self.items = []
  ```

  建立一个栈类`stack`，并初始化栈为空，即空列表`[]`。下面定义一些对栈的操作的方法。

* 检查栈是否为空栈

  ```python
  def isempty(self):
      return self.items == []
  ```

  定义一个检查栈是否为空栈的方法，如果该栈确实为空栈，那么`return self.items == []`应该为真值，即`True`，反之上面的返回值为假，即`False`。

* 入栈

  ```python
  def push(self, item):
      self.items.append(item)
  ```

  上面的代码执行的就是将`item`压入栈，在上面我们介绍栈的基本操作的时候元素入栈之间我们先要检查栈是否已经是满栈，即有没有空位，但是我们在上面代码中没有体现出来，其原因是我们实现的过程中使用的是Python的内建函数`list`，而该列表是没有固定长度的，可以向其中无限次添加元素，所以我们没有检查是否为空栈。

* 将元素弹出栈

  ```python
  def pop(self, item):
      # Check whether the stack is empty
      if self.isempty():
          raise RunTimeError("")
      # delete and return the item
      topindex = len(self.items)-1
      item = self.items(topindex)
      del self.items(topindex)
      return item
  ```

  在栈中弹出元素的时候，首先检查了栈是否为空栈，如果为空栈返回错误，否则，继续进行弹出操作。后面弹出操作的时候可以使用`list`特有的操作`list.pop()`，上面代码可以抽象成这个操作。

  ```python
  >>>mylist = [2,3,5]
  >>>mylist.pop()
  5
  ```

* 返回栈的最后元素

  ```python
  def top(self):
      # Check whether the stack is empty
      if self.isempty():
          raise RunTimeError("")
      
      topindex = len(self.items)-1
      item = self.items(topindex)
      return item
  ```



------



[TOC]