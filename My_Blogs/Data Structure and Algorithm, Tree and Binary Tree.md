### Data Structure and Algorithm, Tree and Binary Tree

#### 1. Introduction

##### 1.1 Tree

前面我们已经介绍过了线性的数据结构，如链表、栈、队列等，下面我们介绍一种非线性的数据结构，树。在访问大量数据的时候，访问线性数据结构会花费大量的实践，不宜使用，相比之下使用树形结构进行查询则可以节省大量的时间，其大部分操作的时间复杂度的平均值都是**O(logN)**。树，在多个领域都有使用，在计算机中使用的更多，比如我们Unix操作系统下的文件目录系统，数据库系统中等，都有使用。

首先，我们先来看一下一种典型的树的例子。

![Tree](https://lynnlaulsl.files.wordpress.com/2016/10/biology.png)

上面的例子是一种典型的动物分类的树形结构，通过上面的例子我们可以看到树形结构有一些特点。

* 首先，树是分等级。最上面的一级是动物界(Animalia)，下一级，也就是动物界这一层的子类，分成门（phylum）包括脊椎动物（chordate）和无脊椎动物（arthropoda），依次往下类推。不管下面分类多少类，包含的都是动物。
* 第二个，树形中某个节点的子节点彼此之间都是相互独立的。比如，灵长类（primate）节点下面包括的两个节点人科（hominidae）和猩猩科（pongidae），人科和猩猩科同是灵长类动物的子类，但是二者是相互独立的。
* 第三个，每个节点都是独一无二的，Animalia →→ Chordate →→ Mammal →→ Carnivora →→ Felidae →→ Felis →→ Domestica.。

 最顶层的节点成为此树的根节点(Root)，根节点下面的节点成为子节点(Children)，同一个根节点下面的子节点之间互相为兄弟节点。子节点和父节点是一种相对的关系，在上面的例子中，哺乳动物(mammal)节点相对于脊椎动物(Chordate)节点来说是子节点，但是相对于灵长类(Primate)节点来说又是父节点。

树形结构另外一个应用，比如在操作系统中的文件系统中。在文件系统中，文件与文件夹，目录之间的关系便是一种树形关系。下面是Unix操作系统中一种文件系统。

![Unix_file_system](https://lynnlaulsl.files.wordpress.com/2016/10/directory.png)

从上面的图中我们可以看到，文件根目录下面包含多个子节点dev/,etc/,sbin/等等，我们可以选择一个目录的路径找到某个目录下面的文件。

##### 1.2 Binary Tree

二叉树(Binary Tree)，是一种特殊而且典型的树形结构，二叉树的特别之处在于每个父节点下面都最多能有两个子节点，常常用于存储数据，查询数据。

![binary_tree](https://lynnlaulsl.files.wordpress.com/2016/10/binary_tree.jpg)

上面的树形结构充分介绍了一个典型的二叉树的组成部分。根节点，父节点，子节点等关系不在介绍，同上。

介绍一下，二叉树的一些性质

* 在非空二叉树的第`i`层，之多存在着`2`的`i-1`次方个节点；
* 在任何非空的二叉树中，如果其叶子节点的个数为`n0`，度数为2的节点的个数为`n2`，那么`n0=n2+1`；
* 在高度为`h`的二叉树中，至多又`2`的`h+1`次方减`1`个节点；
* **完全二叉树**：对于一个高度`h`的二叉树，如果从第`0`层到第`h-1`层的节点都满了。如果下一层的节点不满，并且都排列在左边，空位在右边。那么这样的二叉树成为完全二叉树。

##### 1.3 Implement

在Python中，实现二叉树我们使用一种简单的技术，简单的看，二叉树是一三元组，包括其左子节点，右子节点和本节点的数据。Python中的list或者tuple都可以实现。

在二叉树的数据结构中，包括多种操作，如如插入节点，删除节点，查找节点，创建二叉树等，在此首先介绍创建一棵简单的二叉树，

* 空树采用None表示；
* 非空二叉树用包含三个元素的列表表示[*d, l, r*]，其中
  * d，表示的根节点；
  * l，表示的左子节点；
  * r，表示的右子节点；

通过上面的方法，就可以把二叉树映射到一种分层的list结构中。

![little_tree](https://lynnlaulsl.files.wordpress.com/2016/10/smalltree.png)

上面是一个简单的二叉树结构，映射到Python中list可以写成：

```python
mylist = ['a', # root 
          ['b', # left
            ['d', None, None], 
            ['e', None, None]], 
          ['c', # right
              ['f', None, None], 
              None] 
         ]
```

将上面整个创建二叉树的过程整理，可以得到完整的代码。

* 创建二叉树的方法：

  ```python
  # initialize a binary tree 
  def binarytree(root, left=None, right=None):
      return [root, None, None]
  ```

* 向二叉树中添加左子树：

  在向初始化的二叉树中添加左子节点的时候，因为初始化二叉树时候为空，所以不用过多考虑。假如原二叉树的左子节点已经存在元素，那么需要将此处的元素保持在左子节点的位置向下移动一层，这养空出的位置可以添加新的左子节点。因为二叉树的每个节点的都是三元组，所以使用的方法就是`pop.binarytree[1]`，然后进行操作。

  ```python
  #
  def insertleft(root, newleft):
      temp = root.pop(1)
      # len(temp)>1 indicates that there is left child
      # move the child node to the next level.
      if len(temp) > 1:
          root.insert(1, [newleft, temp, []])
      # there is no left child here.
      else:
          root.insert(1, [newleft, [], []])
  ```

* 向二叉树中添加右子树：

  向二叉树中添加右子树的方法和向二叉树中添加左子树的方法一样，只是将左子树变成右子树就可以

  ```python
  def insertright(root, newright):
      temp = root.pop(2)
      if len(temp) > 1:
          root.insert(2, [newright, [], temp])
      else:
          root.insert(2, [newright, [], []])
  ```

* 返回二叉树的子树和根值

  只需要将列表中的第一值返回就可以

  ```python
  def rtrnrtvlaue(root):
      return root[0]
  ```

  同样的操作可以返回二叉树的左子树和右子树。

  ```python
  def rtrnleft(root):
      return root[1]

  def rtrnrigh(root)t:
      return root[2]
  ```

二叉树中初步了解的各种方法，大约就这些，将这些代码组合在一起可以写一个简单的二叉树。

```python
class binarytree():
    
    def btree(root):
        return [root, None, None]
    
    def insertleft(root, newleft):
        temp = root.pop(2)
        if len(temp) > 1:
            root.inser(1, [newleft, temp, None])
        else:
            root.insert(1,[newleft, None, None])
            
    def insertright(root, newright):
        temp = root.pop(2)
        if len(temp) > 1:
            root.insert(2, [newright, None, temp])
        else:
            root.insert(2, [newright, None, None])
```

