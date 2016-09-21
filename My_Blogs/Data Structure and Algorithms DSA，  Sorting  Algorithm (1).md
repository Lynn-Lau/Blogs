### Data Structure and Algorithms DSA，  Sorting  Algorithm (1)

####  0.Introduction

排序(Sorting)，一直是数据结构中经久不衰的一个话题，除此之外每个公司的笔试测试题都包含排序算法，所以排序的重要性不言而喻。在此总结一下自己学习过程中关于排序的问题，并将重点代码写出来。

常见的排序算法有以下几种：

* 插入排序 (Insertion Sort)
* 冒泡算法 (Bubble Sort)
* 选择排序 (Selection Sort)
* 归并排序 (Merge Sort)
* 希尔排序 (Shell Sort)
* 快速排序 (Quick Sort)

下面会对以上所有的排序算法进行介绍，并完成关键部分的代码。关于排序算法还包括基本操作，性能和评价等等，在此先不做介绍。

#### 1. Insertion Sorting 

顾名思义，将原来序列中的元素按照一定的升序或者降序插入到新的序列中，直到所有的元素都符合顺序。

##### 1.1 How it works 

介绍一下插入排序的工作原理，在此我们选择一个数据序列作为实例进行演示。

* 取一列没有经过排序的随机数列：

  ![](https://lynnlaulsl.files.wordpress.com/2016/09/unsorted_array.jpg)

  上面数据列中的元素都是未经过排序的随机数字，一下默认的排序为升序，下面我们进行插入排序的操作。

* 首先，比较数列中的前两个元素，第一个14和第二个33，14<33 符合升序的要求，此时不需要对这两个元素的位置进行调节；

  ![](https://lynnlaulsl.files.wordpress.com/2016/09/insertion_sort_1.jpg)

* 然后，可以将14这一单独的元素作为整个序列的子序列，将新的元素插入这个子序列中；

  ![](https://lynnlaulsl.files.wordpress.com/2016/09/insertion_sort_2.jpg)

* 下一步，插入排序向后移动一个位置，比较33和27；

  ![](https://lynnlaulsl.files.wordpress.com/2016/09/insertion_sort_3.jpg)

* 通过比较发现，27和33 的位置并不是很正确；

  ![](https://lynnlaulsl.files.wordpress.com/2016/09/insertion_sort_4.jpg)

* 交换33和27的位置，并且将27和已经排好序的子序列中的元素进行比较，插入到其中，此时已排序的子序列为14，当27和33交换完位置后，和14比较后位置合适，便插入到14的后面；

  ![](https://lynnlaulsl.files.wordpress.com/2016/09/insertion_sort_5.jpg)

* 到此为止，14和27组成已经排好序的子序列了，下面比较33和10；

  ![](https://lynnlaulsl.files.wordpress.com/2016/09/insertion_sort_6.jpg)

* 33和10并没有在合适的位置；

  ![](https://lynnlaulsl.files.wordpress.com/2016/09/insertion_sort_7.jpg)

* 根据上面的相似，交换33和10 的位置；

  ![](https://lynnlaulsl.files.wordpress.com/2016/09/insertion_sort_8.jpg)

* 将10插入到子序列中，发现10和27的位置也不合适；

  ![](https://lynnlaulsl.files.wordpress.com/2016/09/insertion_sort_9.jpg)

* 交换他们的位置；

  ![](https://lynnlaulsl.files.wordpress.com/2016/09/insertion_sort_10.jpg)

* 比较14和10 的位置，发现同样不合适；

  ![](https://lynnlaulsl.files.wordpress.com/2016/09/insertion_sort_11.jpg)

* 调换他们的位置；

  ![](https://lynnlaulsl.files.wordpress.com/2016/09/insertion_sort_12.jpg)

  ​

至此，前面的三个元素已经完成排序，并组成了一个子序列，将这种方法一直持续到所有序列结束便可将所有的元素进行排序。将上面的详细的步骤进行总结，大体上可以分成以下六个步骤：

1.  选择第一个元素，并且认为第一个元素为已经排序的子序列；
2.  选择下一个元素；
3.  把该元素与已排序的子序列中左右元素进行比较；
4.  将比该元素大的元素均向后移动一个位置，留出一个空位置；
5.  把该元素插入到空位置；
6.  重复上述操作。 

##### 1.2 Implement

上面将插入排序的原理介绍清楚了，下面通过代码实现，选择Python和C语言，在编写代码实现的过程中有一些需要注意的地方。

Python，

```python
def insert_sort(lst):
    for index in range(1, len(lst)):
        # start from 1 not from 0
        temp = lst[index]
        m = index
        # initial the m and 0<m<=index
        while m > 0 and lst[m-1] > temp:
            lst[m] = lst[m-1]
            m = m-1
        lst[m] = temp
    
    return lst
```

C 语言，

```c
int InsertSort(Arr[])
{
    int index, m;
    int temp;
    for(index=1; index<N; index++)
    {
        temp = Arr[index];
        for(m=index; m>0 && Arr[m-1]>temp; m--)
            Arr[m] = Arr[m-1];
        Arr[m] = temp;
    }
    return Arr[];
}
```

##### 1.3 Analysis 

嵌套循环的每一次都花费N次迭代，因此插入排序的时间复杂度为:
$$
O(N^2)
$$
当输入的序列为反序列的时候可以精确的的得到该值。

#### 2. Selection Sorting

选择排序算法与插入算法相似，选择排序算法也是在序列中选元素插入子序列中，不同的是选择排序不是选择序列中的下一个元素，而是选择序列中的最小元素然后插入子序列中。

##### 2.1 How it works

在选择排序算法中，使用了一种“猜想(Guess)-验证(Check)”思想寻找第一个最小的元素。首先，猜想原始序列中的第一个元素是最小元素，然后对剩余的序列中进行线性搜索，如果没有元素比第一个元素更小，那么首元素便是最小的元素，否则，第一个最小的元素便是剩余序列中的最小元素。

举例介绍：

​       ![](https://lynnlaulsl.files.wordpress.com/2016/09/unsorted_array.jpg)

* 上面选取的随机数列进行介绍，同样默认的顺序为升序；

* 猜想第一个元素14是最小的元素，那么对除14外的序列进行线性检索验证，发现10是最小的元素且比14小；

  ![](https://lynnlaulsl.files.wordpress.com/2016/09/selection_sort_1.jpg)

* 将14和10这两个元素进行交换，交换后第一个元素便是最小的元素；

  ![](https://lynnlaulsl.files.wordpress.com/2016/09/selection_sort_2.jpg)

* 下面在剩余的序列中再次选一个最小的元素放在总序列的第二个位置，剩余序列的第一个位置；

  ![](https://lynnlaulsl.files.wordpress.com/2016/09/selection_sort_3.jpg)

* 通过线性检索，发现14是最小的元素，并且应该放在第二个位置；

  ![](https://lynnlaulsl.files.wordpress.com/2016/09/selection_sort_4.jpg)

* 交换14和33的位置；

  ![](https://lynnlaulsl.files.wordpress.com/2016/09/selection_sort_5.jpg)

* 经过两次迭代，我们发现两个最小的元素放在了最前面，同样我们将上述规律应用到剩余的序列中，我们可以得到下面的结果；

  ![](https://lynnlaulsl.files.wordpress.com/2016/09/selection_sort.jpg)

通过举例将选择排序算法大体介绍了一下，总结之后可以分成几个步骤：

1. 将序列中的第一个元素（索引为0）设定为最小的元素Min；
2. 在剩余的序列中选择最小的元素；
3. 将剩余列表中的最小元素与Min交换；
4. 寻找下一个最小元素；
5. 同理将上述方法应用到剩余的序列中；

##### 2.2 Implement 

下面将选择排序算法通过代码实现，选择Python和C语言。

Python

```python
# -*- coding:utf-8 -*-

# Sorting Algoritm: Selection Algoritm
# Author: Lynn Lau
# Date: 2016/09/21

def selection(mylist):
    
    for index in range(len(mylist)-1):
        Min = index
        for m in range(index, len(mylist)-1):
            if mylist[m] < mylist[Min]:
                Min = m
            
        if index != Min:
            temp = mylist[Min]
            mylist[Min] = mylist[index]
            mylist[index] = temp

mylist = [14, 33, 27, 10, 35, 19, 42, 44]
selection(mylist)    
print mylist
```

