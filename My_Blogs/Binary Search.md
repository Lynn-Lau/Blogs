### Binary Search

#### 1. Introduction 

Binary Search 又称“二分查找法”，与其相对应的便是“线性查找法(_Linear Search_)，线性查找法是在一个有序集合中通过集合中索引值的从大到小或者从小到大依次查找集合中的某个值，但是线性查找算法在集合中元素比较多的时候时间复杂度相比于二分查找法不是很理想，所以在这里介绍并学习”二分查找法“。

#### 2. Linear Search

* 线性查找算法介绍

  下面动图中我们可以看到，在集合中包含10个数字10、14、19、……42、44，要在这个集合中寻找数字33，那么只需要将集合中的每个数字按照索引值的从小到大依次和33作比较，如果在集合中找到等于33的值则返回其索引值，则程序停止（包含多个相同值暂且不考虑），否则一直进行下去知道与集合中所有元素进行比较完毕，没有找到该值则返回None。          

  ​                                     ![](https://lynnlaulsl.files.wordpress.com/2016/08/linear_search.gif)

* 关键程序代码

  ```python
  def linear_search(datalist, key):
      # key 相当于上面的数字‘33’，datalist为数据集合
      for index in range(len(datalist)):
          if datalist(index) == key:
              return index
  ```

线性查找算法比较简单在此不做过多介绍。

#### 3. Binary Search

* 二分查找算法介绍

  二分查找算法就是每次在有序集合中查找目的元素时候都会将查找的范围缩小一半，而线性查找算法每查找一次只是将查找范围缩小了一个值，所以当查找的集合较大的时候二分查找算法效率更高，时间更短，优势也比较明显。需要注意的是：**查找的有序集合必须是有序的，要么集合中的元素是以一种非递减的顺序，要么集合中的元素是一种非递增的顺序。**

  二分查找法的时间复杂度的是**O(log n)**，相比于线性查找算法的复杂度为**O(n)**要小一些，所以执行效率高。

* 查找步骤与过程

  * 开始的时候，要查找的元素的范围为整个有序集合；
  * 选择整个有序集合中的中间位置的元素与查找项进行比较，如果二者相等那么就可以返回中间位置元素的索引值，查找结束；
  * 如果查找项大于中间位置的元素（在数据集合是非递减的顺序下，说明查找项在有序集合的右半部分），那么就把查找范围缩小为中间位置右面的半个区间；如果查找项小于中间位置的元素（在数据集合是非递减的顺序下，说明查找项在有序集合的左半部分），那么就把查找范围缩小为中间位置左面的半个区间；
  * 重复上一步骤进行查找，找到元素返回索引值，查找结束；否则，没有找到，返回None。

  举个栗子

  我们要在10个数字组成的列表中找到“31”这个数字，那么我们通过二分查找法来试一下，理解其查找过程是怎样的。

  * 开始寻找的区间为整个集合

    ​                               ![](https://lynnlaulsl.files.wordpress.com/2016/08/binary_search_0.jpg) 

    10个数字， 索引值为0~9，确定列表中的中间位置的数据值，公式如下：

    ```python
    lowindex, highindex = 0, len(datalist)-1
    midpoint = int((lowindex + highindex)/2) 
    midvalue = datalist(midpoint)
    # midvalue 就是集合中间位置的数据值
    ```

    在本例中midpoint=4.5，在这里取值取floor值，取4，即第五个值27

    ​                               ![](https://lynnlaulsl.files.wordpress.com/2016/08/binary_search_1.jpg) 

    显然，31>27，说明查找项存在与整个有序数据集合的右半部份，所以左半部分不用考虑，直接将查找范围缩小了半。

    ​                                ![](https://lynnlaulsl.files.wordpress.com/2016/08/binary_search_2.jpg)

    右半部份查找的起始位置为索引值为“5”元素，结束为集合的末尾。

  * 按照查找过程，重复上述查找步骤进行查找。需要注意的是此时索引值的上界下界会发生变化（在这一步骤中，下界发生了变化，上界未发生变化），需要重新赋值，即

    ```python
    lowindex = midpoint + 1
    midpoint = int((lowindex + highindex)/2) # midpoint = int(5 + 9) = 7 
    ```

    确定右半部份中间位置的数据值，仍然通过开始的公式，`midpoint = 7`，`datalist(midpoint)=35`                      

    ​                                    ![](https://lynnlaulsl.files.wordpress.com/2016/08/binary_search_3.jpg)

    显然，35>31，二者不相等，需要继续查找。

  * 重复上面查找的过程，重复上面的步骤，确定再次查找的范围，即数据集的上界和下界（下界没有发生变化，上界发生了变化），靠右半部分可以忽略，通过上面的公式计算可得：

    ​                                    ![](https://lynnlaulsl.files.wordpress.com/2016/08/binary_search_4.jpg)

    ```python
    highindex = midpoint - 1
    midpoint = int((lowindex + highindex)/2) # midpoint = int(5 + 6)/2 = 5
    ```

    通过上面的计算的`midpoint = 5`，则`datalist(midpoint) = 31`在数据集中找到“31”与查找项相等。

    ​                                    ![](https://lynnlaulsl.files.wordpress.com/2016/08/binary_search_6.jpg)

    如上图所示，31在数据集中的索引值为5，到此二分查找结束，返回索引值。

* 算法分析

  在有序数据集中通过二分查找成功的查找过程中，查找比较的次数不超过floor(**log n**)+1。

  总结一下，采用有序表和二分查找法：

  * 主要的优点就是检索速度快，时间复杂度为O(**log n**)；
  * 二分查找算法只能用与关键码可以排序，数据项按照关键码排序的字典，而且只适用于顺序存储结构。

* 代码实现

  该算法通过代码进行实现的时候选择使用Python语言进行实现，Python浅显易懂。

  ```python
  # -*- coding: utf-8 -*-
  # Uses python2
  '''
  Author:Lynn Lau
  Data:2016/08/25
  '''
  def binary_search(datalist, key):
      
      lowindex, highindex = 0, len(datalist)-1
      while (lowindex <= highindex):
          midpoint = int((lowindex + highindex)/2)
          midvalue = datalist(midpoint)
          
          if midvalue < key:
              lowindex = midponit + 1
          elif midvalue > key:
              highindex = midvalue -1
          else:
              return midpoint
      return -1
      # rerurn -1 if the key not in the datalist

  if __name__ = '__main__':
      data1 = list(map(int, raw_input().split()))
      # data2 = list(map(int, raw_input().split()))
      n = data[0]
      datalist = data1[1:n+1]
      keys = [8, 1]
      for key in keys:
          print binary_serach(datalist, key)
  ```

  ​

