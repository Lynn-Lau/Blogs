### 哥德巴赫猜想验证及质数相关-Tencent Interview

#### 1.Introduction

最近在帮助师兄准备工作笔试，顺手打个助攻练练手，昨天是腾讯公司的在线笔试，选择题涉及内容范围较广，不做介绍。编程题一共四个题，在此介绍其中一个，并完成。

题干介绍：

> **给定一个正整数，编写程序计算有多少对质数的和等于输入的这个正整数，并输出结构。输入的值小于1000，例如，输入为10，程序应该输出的结果为2。（共有两对质数的和为10，分别是（5，5），（3，7））。**

这个笔试题涉及到的知识无非就是迭代和质数的判断，但是平时在学习过程中没有好好总结过有关质数的相关问题和算法，所以在此利用这个机会想把与质数相关的常见算法和题型进行总结一下。

#### 2. Analysis

首先，什么是质数？

> **质数**（**Prime number**），又称**素数**，指在大于1的[自然数](https://zh.wikipedia.org/wiki/%E8%87%AA%E7%84%B6%E6%95%B0)中除了1和该数自身外，无法被其他自然数[整除](https://zh.wikipedia.org/wiki/%E6%95%B4%E9%99%A4)的数（也可定义为只有[1](https://zh.wikipedia.org/wiki/1)与该数本身两个[因数](https://zh.wikipedia.org/wiki/%E5%9B%A0%E6%95%B8)的数）。   ----From [Wikipedia](https://zh.wikipedia.org/wiki/%E7%B4%A0%E6%95%B0)

既然我们知道什么是质数了，那么我们在编程的过程中如何去判断它是不是质数呢？

在一般领域，对于正整数n，如果用2到![](https://lynnlaulsl.files.wordpress.com/2016/09/b03533fa828ba61e582843574234970a314e5980.png)之间的左右正整数去除，均无法整除，那么n为质数。

下面通过Python代码进行实现：

```python
import math

def is_prime(num):
    if num <= 1:
        return False
    for i in range(2, int(math.sqrt(num))+1):
        if num%i == 0:
            return False
    return True
```

通过上面的代码我们就可以判断一个数字是不是质数。如果要输出某个区间的所有质数，只需要在上面代码添加一个数据区间进行循环，即可。例如，输出1000以内的所有质数：

```python
import math

def is_prime(num):
    if num <= 1:
        return False
    for i in range(2, int(math.sqrt(num))+1):
        if num%i == 0:
            return False
    return True

if __name__ == "__main__":
    primelist = list()
    for num in range(2, 1000):
        if is_prime(num):
            primelist.append(num)
    print primelist
    
>>>[2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 67, 71, 73, 79, 83, 89, 97, 101, 103, 107, 109, 113, 127, 131, 137, 139, 149, 151, 157, 163, 167, 173, 179, ... , 971, 977, 983, 991, 997]
```

上面的代码完成的就是输出1000以内所有的质数。

回到上面的题目中，本题的题干就是著名的哥德巴赫猜想（Goldbach's Conjecture），即任意一个大于2的正整数都可以写成两个质数的和，上面这种说法还有另外一种版本，即任何一个大于2的偶数都可以写成两个质数的和。要通过编程来验证这一猜想，可以通过下面思路解决。

假如我们要验证10由两个质数相加得到，并求出这样的质数对的数量。首先，这样的质数对中的质数都是小于10 的质数，所以我们可以先把10以内的所有质数`prime`枚举出来，放到列表中`primelist`。然后对列表中的质数进行迭代`primelist[m]`,`primelist[n]`，如果`primelist[m]+primelist[n]=10`那么计数一次，直到将质数列表中的质数迭代结束为止。最后返回计数值即可。100以内的质数的总数才100多个所以使用`for`循环的复杂度很低，可以忽略，添加代码实现，只添加后面部分代码。

```python
import math

def is_prime(num):
    if num <= 1:
        return False
    for i in range(2, int(math.sqrt(num))+1):
        if num%i == 0:
            return False
    return True

primelist = list()
for j in range(2, 1000):
    if is_prime(j):
        primelist.append(j)

def sum(data):
    count = 0
    for m in range(0, len(primelist)):
        for n in range(m, len(primelist)):
            if primelist[m] + primelist[n] == data:
                count = count + 1
                print "%d = %d + %d" %(data, primelist[m], primelist[n])
    return count

result = sum(int(raw_input()))
print result 
```

