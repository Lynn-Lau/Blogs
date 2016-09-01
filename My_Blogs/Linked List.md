### Linked List

#### 1. Introduction

*Linked List*, 链表。

首先，链表是数据结构(Data Structure)中比较基础的一种数据结构，是线性表的一种，抽象的一组包含多个元素的序列。链表中的多个元素是通过链接联系起来组成的一个表，每个链接连接着上一个元素和下一个元素，还包含一个元素，即存储的数据。

我们在此介绍简单单向链表，将链表进行可视化之后我们可以认为链表是具有以下结构的一个表，链表由一个个的节点(Node)前后连接起来组成的，每一个节点指向下一个节点，像链条一样。

​                              ![](https://lynnlaulsl.files.wordpress.com/2016/08/linked_list.jpg)

通过上面的链表图片我们可以得到链表以及节点的结构：

* 在单向链表中包含一个头节点(**Header**)，头节点是不存储数据的，头节点作为指示链表开始的地方，并指向下一个节点数据区域；
* 每个节点(Node)包含两部分，数据区域(Data Field)和链接区域(Link Field)，数据区域存储每个节点的数据；
* 链接区域负责将此节点与下一个节点相连（指向下一个节点），进而组成整个链表；
* 链表中最后一个节点的链接区域指向Null，表示这一链表的结束。

#### 2. Basic Operations

链表属于线性表(顺序表)的一种，其涉及到的常见操作有：

- Insertion (插入)：向链表中添加元素，包括向链表的开头，结尾和中间某处处添加元素；
- Deletion (删除)：删除列表中的元素，开头、结尾和中间某个固定的元素；
- Display (显示)：显示整个链表；
- Search (检索)：在链表中检索某个元素；
- Clear (清空)：清空整个链表；


上面为链表中常见的几种操作，如何通过代码实现这些操作，稍后介绍。

#### 3. Implement a Linked List

通过上面的介绍，我们对链表有了初步的了解和认识，那么链表如何通过代码实现呢？

下面我们介绍以下如何通过代码实现链表以及上述的各种操作。

##### 3.1 Initiate the Node

链表是由一个个的节点组成，所以构建一个链表首先要构造节点。通过开始部分介绍，每个节点包含两个部分（Data Field）和（Link Field），所以再初始化节点的时候每个节点至少包含这两部分信息。在初始化链表中的节点的时候链表是空的，所以初始值为0，下面代码为初始化过程：

* **初始化链表节点**

  ```python
  # This class is used to define the properties 
  # and function of the node.
  class Node:
      
      # Define the properties of node which has data field
      # and link field, the init node is a empty node(has no data). 
      def __init__(self, initdata, next_):
          self.data = initdata
          self.next_ = next_
          self.next_ = None
      
      def getdata(self):
          return self.data
      
      def getnext(self):
          return self.next_
      
      def setdata(self, newdata):
          self.data = newdata
      
      def setnext(self, newnext):
          self.next_ = newnext
  ```


在上面将节点进行初始化之后，利用上面的方法建立一个新的节点。利用上面的方法创建的节点如下图。

```python
>>>temp = Node(93)
>>>temp.getdata()
93
```

​                                                    ![](https://lynnlaulsl.files.wordpress.com/2016/09/node.png)

* 初始化建立链表

  * 建立链表类

    ```python
    class List:
        
        def __init__(self):
            self.head = None
    ```

    初始化 `mylist`，空链表。

    ```python
    mylist = List()
    ```

    ​                                                      ![](https://lynnlaulsl.files.wordpress.com/2016/09/initlinkedlist.png)

  * 检查链表是否为空

    检查链表是否为空链表，如果是空链表返回`None`，使用的表达式便是检查链表的`head`是否为`None`，

    `self.head == None`如果这个表达式的值为`True`，那说明这个链表中无节点。

    ```python
    def isempty(self):
        return self.empty == None
    ```

  * 向链表中添加元素

    通过上面建立链表之后，我们需要项链表中添加元素，但是在向链表中添加元素的时候，我们需要确定将元素添加在链表中的什么位置，链表的前端、链表的末尾或者是其他位置。在此先对添加位置不做考虑。在链表中的所有元素都可以通过第一个节点的`next`一个接一个搜索到，所以项链表中添加元素最简单的办法就是将元素添加在链表的起始位置，下面的方法中，我们便将新的元素添加到链表的起始位置。

    向链表中添加元素使用的是`add`方法，其实现代码如下：

    ```python
    def add(self, item):
        temp = Node(item)
        temp.setnext(self.head)
        self.head = temp
    ```

    在上面的代码中第二行，利用`Node`建立一个新的节点`temp`，然后将元素`item`放入节点的数据区域，节点建立完成。然后，我们将现有的链表结构链接到新的节点，其过程主要分成两步。第一步（第三行代码），将新节点的代码的`next`指向链表中原来链表中的第一个节点，所以链表中其余节点也完成了和新节点的链接。第二步（第四行代码），修改头节点指向新元素，完成。

    整个过程如下图所示：

    ​                                          ![](https://lynnlaulsl.files.wordpress.com/2016/09/addtohead.png)

    向链表中添加多个元素代码：

    ```python
    >>>mylist.add(31)
    >>>mylist.add(77)
    >>>mylist.add(17)
    >>>mylist.add(93)
    >>>mylist.add(26)
    >>>mylist.add(54)
    ```

  * 链表的大小、检索和移除

    下面要介绍的几种方法链表大小/长度的求取，检索链表的中的元素，移除链表中的某个元素都需要使用链表遍历(linked list traversal)的方法。在整个遍历过程中会访问每个节点，我们定一个外部变量帮助我们从链表的开始进行遍历。

    在求取链表的大小的过程中，一边需要遍历链表中的节点，还要对遍历过的节点进行计数。实现代码如下：

    ```python
    def size(self):
        current = self.head
        count = 0
        while current != None:
            count = count + 1
            current = current.getnext()
        return count
    ```

    ​                       ![](https://lynnlaulsl.files.wordpress.com/2016/09/traversal.png)

    对上面代码进行分析。我们引用的外部变量为`current`，在第二行代码中将其初始化为链表的头，计数的开始时候将`count`初始化为0。第4-6行代码实现的是遍历过程，只要是`current`变量没有遍历到达链表的末尾(`None`)，那么我们就将`current`沿着链表的`next`移动到下一个节点，每次当`current`向前移动一个节点的时候，`count`便加1。当遍历结束后，返回计数值，如上图所示。

    介绍链表中的检索方法，检索方法同样使用了链表的遍历，其代码如下：

    ```python
    def search(self, item):
        current = self.head
        found = False
        while current != None and not found:
            if current.getdata == item:
                found = True
            else:
                current = current.getnext()
        
        return found
    ```

    ​                                   ![](https://lynnlaulsl.files.wordpress.com/2016/09/search.png)

    对上面的代码进行分析，首先像前面遍历链表一样，在第二行引用1个外部变量初始化为头，然后定义一个布尔类型变量`found`用以记录检索过程是否已经找到了目的元素，在遍历开始的时候没有找到目的元素，继续向下遍历，并且此时`found`保持为`False`。第四行，为遍历条件，将上面的两种条件均考虑到，只要没有检索到目的元素，并且后面仍有未检索到的节点，我们继续向前检索下一个节点。第五行，如果检索到目的节点，`found`设为`True`。

    **举例**

    ```python
    >>>mylist.search(17)
    True
    ```

    ​
