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
        for m in range(index, len(mylist)):
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

C语言

```c
#include <stdio.h>

int main()
{
    int Arr[10];
    int i, m, n, temp;
    printf("Please input 10 numbers:\n");
    for (i = 0; i < 10 ; i++)
    {
        scanf("%d", &Arr[i]);
    }
    for ( m = 0; m < 9; m++)
        for (n = 0; n < 9-m; n++)
            if (Arr[n]>Arr[n+1])
            {
                temp = Arr[n];
                Arr[n] = Arr[n+1];
                Arr[n+1] = temp;
            }

    printf("The Sorted Numbers are:\n");
    for (i = 0; i < 10 ; i++)
    {
        printf("%d ", Arr[i]);
    }

    return 0;
}
```

##### 2.3 Analysis

在选择排序中同样使用了两个`for`循环，时间复杂度为：
$$
O(N^2)
$$
当初始序列为逆序列地时候正好可以得到该时间复杂度。

#### 3. Bubble Sorting

冒泡排序算法，冒泡排序算法是这些排序算法中最容易理解地算法，在学习C语言地初始阶段就介绍过冒泡排序算法，其大致思想，就是将序列中地逆序数进行交换，一直到序列中地元素按照一定规律排序为止。

##### 3.1 How it works

在此我们同样选择未排序地随机序列进行举例，并且默认地排序未升序地方式。

* 选择未排序地序列；

  ![](https://lynnlaulsl.files.wordpress.com/2016/09/bubble_sort_0.jpg)

* 冒泡排序一开始要比较前两个元素，将大的元素向后移，小的元素向前移，14<33两者都在合适的为止，那么不做任何变化；

  ![](https://lynnlaulsl.files.wordpress.com/2016/09/bubble_sort_1.jpg)

* 紧接着需要比较第二个和第三个元素，33和27；

  ![](https://lynnlaulsl.files.wordpress.com/2016/09/bubble_sort_2.jpg)

* 因为33>27，两者需要交换位置，大的在后，小的在前；

  ![](https://lynnlaulsl.files.wordpress.com/2016/09/bubble_sort_3.jpg)

* 交换完成之后，序列应如下；

  ![](https://lynnlaulsl.files.wordpress.com/2016/09/bubble_sort_4.jpg)

* 下一步，我们比较33和35两个元素；

  ![](https://lynnlaulsl.files.wordpress.com/2016/09/bubble_sort_5.jpg)

* 33<35两者的位置不用交换，再比较35和10；

  ![](https://lynnlaulsl.files.wordpress.com/2016/09/bubble_sort_6.jpg)

* 因为35>10，交换二者的位置，交换完位置后应如下图所示；

  ![](https://lynnlaulsl.files.wordpress.com/2016/09/bubble_sort_8.jpg)

* 此时完成了第一趟排序，将序列中的最大元素经过冒泡排序排到了最后面，下一趟排序则可忽略此最大元素，从左边剩余的序列再次进行排序，选出最大的元素放到剩余序列的最右边，并将此方法依次类推一直将整个序列循环完毕，可以得到升序的序列。

  ![](https://lynnlaulsl.files.wordpress.com/2016/09/bubble_sort_9.jpg)

  ![](https://lynnlaulsl.files.wordpress.com/2016/09/bubble_sort_10.jpg)

  ![](https://lynnlaulsl.files.wordpress.com/2016/09/bubble_sort_11.jpg)

  ​

至此，冒泡排序方法介绍到这里，下面通过编程语言实现。

##### 3.2 Implement

通过Python和C语言实现冒泡算法。

```python
#-*- coding:utf-8 -*-

# Data Structure and Algorithm: Bubble Sorting
# Author: Lynn Lau
# Date: 2016/09/23

def bubble_sort(lst):
    N = len(lst)
    for m in range(0, N):
        for n in range(1, N-m):
            if lst[n-1] > lst[n]:
                temp = lst[n-1]
                lst[n-1] = lst[n]
                lst[n] = temp

    return lst

lst = [14, 33, 27, 10, 35, 19, 42, 44]
result = bubble_sort(lst)
print result
```

C语言，

```c
#include <stdio.h>

int main()
{
    int Arr[10];
    int i, m, n, temp;
    printf("Please input 10 numbers:\n");
    for (i = 0; i < 10 ; i++)
    {
        scanf("%d", &Arr[i]);
    }
    for ( m = 0; m < 10; m++)
        for (n = 0; n < 9 - m; n++)
            if (Arr[n-1]>Arr[n])
            {
                temp = Arr[n-1];
                Arr[n-1] = Arr[n];
                Arr[n] = temp;
            }

    printf("The Sorted Numbers are:\n");
    for (i = 0; i < 10 ; i++)
    {
        printf("%d ", Arr[i]);
    }

    return 0;
}
```

##### 3.3 Analysis

冒泡法的时间复杂度不用过多介绍：
$$
O(N^2)
$$
最容易理解的方法，也是时间复杂度最高的算法。

#### 4. Quick Sort

快速排序(Quick Sort)是在实践中已知最快的排序算法，使用了递归的方式进行扫描，之所以运行快，是因为非常精炼和高度优化的内部循环，它的平均运行时间复杂度为：O(*N logN*)，最坏的运行时间和冒泡算法的运行时间相同。

##### 4.1 How it works

假设给定的未排序的数组是随机无序的数组，之所以假设是随机无序的数组，是为了让算法的运行时间更接近于平均运行时间，避免出现最坏的运行时间。

首先，我们要在给定的未排序的数组中选择一个数字作为**枢纽/枢轴元素(Pivot Value)**，枢纽元素的作用是帮助我们在排序过程中对数组中的元素分开并进行比较。我们要选的枢轴元素通常选择数组中的第一个元素，选择枢纽元素的方法有很多种，我们还是简单的选取第一个元素。

假设给定的未排序随机序列为54，26，93，17，77，31，44，55，20，九个元素。那么我们选择54作为我们的枢纽元素，54在给定的数组中按大小排列的话应该在中间附近，那么小于54的数字会分成左边一个数组，大于54会分成右边一个数组，那么这两个数组包含数字数量相近。

![](https://lynnlaulsl.files.wordpress.com/2016/09/firstsplit.png)



我们已经选定54作为枢纽元素，然后选择Leftmark和Rightmark分别从剩余的数组的左边和右边元素开始向中间的元素靠拢，在靠拢的同时，分别比较leftmark和rightmark指向的元素于枢轴元素的大小。当leftmark从左向右移动的过程中遇到大于枢纽元素的元素时候停止，当rightmark从右向左移动的过程中遇到小于枢纽元素的元素的时候停止，然后将两个元素互换，一直持续下去，直到leftmark指向元素的索引大于rightmark指向元素的索引小于leftmark指向的元素的索引为止，此时快速排序的第一趟排序还没有结束。

![](https://lynnlaulsl.files.wordpress.com/2016/09/partitiona.png)

然后将rightmark指向的元素和枢纽元素进行互换，至此，快速排序的第一趟排序到此结束，小于54枢纽元素的值都在54的左边，大于54枢纽元素的值都在54的右边。然后在对小于54的左边数组，大于54的右边数组进行同样的方法递归，那么就可以得到正确排序的数组。

![](https://lynnlaulsl.files.wordpress.com/2016/09/partitionb.png)

##### 4.2 Implement

上面介绍了快速排序算法的原理，下面介绍，快速排序算法的程序实现。本程序使用的是递归算法，首先要确定递归的框架，然后完成递归函数。

首先介绍通过Python语言实现的算法。定义一个非递归的函数，在本函数中定义子函数，子函数进行递归完成快速排序，如下所示：

```python
def quick_sort(lst):
    # declartion of recursion 
    qsort_rec(lst, 0, len(lst)-1)
```

对递归函数内容进行补充：

```python
def qsort_rec(lst, left, right):
    # there is one or no items in the lst
    if left >= right:
        return
    #choose the first item as pivot
    #so the first item in the list can be covered
    pivot = lst[0]
    
    #if left >= right the comparison will stop
    while left < right:
        # scan the items from right to left and 
        # find the item  who is no bigger than pivot.
        while left < right and lst[right] >= pivot:
            right -= 1
        # put the item found last step to the first position, 
        # so the left should point to the next item. 
        if left < right:
            lst[left] = lst[right]
            left += 1
        # scan the items from left to right and
        # find the item who is no smaller than pivot
        while left < right and lst[left] <= pivot:
            left += 1
        # put the item found last step to the last position,
        # so the left should point to the next item.
        if left < right:
            lst[right] = lst[left]
            right -= 1
    # change the pivot and final left position
    lst[left] = pivot
    # divide the lst  after first round quick sort and recursion
    qsort_rec(lst, left-1, right)
    qsort_rec(lst, left+1, right)
```

#### 5. Merge Sort

归并排序（Merge Sort），归并排序算法同样是一种典型的排序算法，归并排序的算法使用的思想是分治（Divide and Conquer），归并排序算法也是一种高效的排序算法。

##### 5.1 Introduction

归并排序使用的算法思想是Divide and Conquer，其内容主要是将整问题分成多个相同的小而且容易解决的问题，这个过程称为Divide，然后解决分别解决这个小问题，进行和并，进而解决整个大问题称为Merge。在归并排序中使用该算法，同样是将整个未排序的数组进行切分称为小的数组一直到每个数字成为一个数组，然后比较这个数字之间的大小，一次次的进行递归，合并成为一个升序或者降序的序列。

归并排序算法的时间复杂度为**O(NlogN)**，当未排序的数组是相反序列的时候最坏的实践复杂度可以达到**O(NlogN)**。

##### 5.2 How it works

在介绍归并排序的时候，我们将整个排序过程分成两个步骤。一，将整个数组进行分裂，直到成为单个数字为止；二，合并，比较数字并将他们进行合并成为一个已排序的数组。

假设我们有一未排序的数组，54，25，93，17，77，31，44，55，20，排序的后为升序。

1. 那么分割数组的过程如下所示：

![](https://lynnlaulsl.files.wordpress.com/2016/10/mergesorta.png)

一直将整个数组分成单个数字组成的数组为止，至此Divide过程结束。

2. 上面的divide的过程结束之后，进行比较单个数组的数字的大小，然后合并成为一个数组。首先，我们比较第一个、第二个数字54、26的大小，很明显26<54，所以将此两个组成数组应该是[26, 54]，同理一次向后选择两个数字进行比较，如果数字为奇数个那么可以剩余一个不参与比较，等下一轮比较合并的过程会参加比较，所以可以得到[26, 54]，[17, 93]，[31, 77]，[44]，[20, 55]。

   第二轮比较，将上一步比较的结果得到的多个数组进行比较，首先比较数组[26, 54]和[17, 93]，26和17相比，显然17最小，所以排序后新数组[17]，然后比较26和93，26更小，则将26放到17后面，得到[17, 26]，然后比较93和54，54更小，把54放到26后面，得到[17, 26, 54]，只剩下一个93，所以将93放到最后，得到[17, 26, 54, 93]， 同理比较后面的数组可以得到，[31, 44, 77]和[20, 55]。

   在进行第三轮的比较合并，首先比较[17,26,54,93]和[31,44,77]，从第一个元素开始比较，17<31，那么新列表[17]，比较31和26，得到[17, 26]，比较31和54，得到[17, 26, 31]，比较54和44，得到[17, 26, 31, 44]，比较54和77，得到[17,26,31 44,54]，比较77和93，得到[17, 26, 31, 44, 54, 77]，剩余93，得到[17, 26, 31, 44, 54, 77, 93]。最终得到的两个列表为[17, 26, 31, 44, 54, 77, 93]和[20, 55]。

   进行第四轮比较合并，从第一个元素开始比较，比较17和20，得到[17]，比较20和26，得到[17, 20]，比较26和55，得到[17, 20, 26]，比较55和31，得到[17, 20, 26, 31]，比较55和44，得到[17, 20, 26, 31, 44]，比较55和54，得到[17, 20 ,26, 31, 44, 54]，比较55和77，得到[17, 20, 26, 31, 44, 54, 55]，此时原来两个列表中的一个列表已经没有元素，那么下面只需要将剩余另外一个列表的元素添加到新的已排序的列表即可，可以得到[17, 20, 26, 31, 44, 54, 55, 77, 93]。到此为止归并排序的整个过程结束。

​                                                                                                                                       