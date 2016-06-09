### Python的面向对象 (二)
#### 封装、继承和多态
在面向对象的编程设计中的三个特点：封装、继承、多态。在此我们就学习一下Python语言中面向对象编程的三个特点。

#### 封装
封装就是在由类创建对象时候，每个被创建的对象中都有这个类的所有的属性和方法，当方法需要执行时候，需要使用的变量保存在对象中，这样对象所使用的方法对对象来说就是隐藏的，看不见的。**简单来说**：就是私有化方法，把一些属性和方法私有化，外部无法调用，增强了代码的安全性。
那么如何将属性或者方法进行私有化呢？在要进行私有化的属性名前面添加两个下划线```"__"```，或者在要进行私有化的方法名字前面添加两个下划线```“__”```。
下面举例说明：

*未进行封装（私有化）处理*

```python
# 定义一个BOY类,
class BOY():
    '''
    利用初始化函数初始化类的共同特性，name，age
    此处的属性名字均未作处理，保持原样
    '''
    def __init__(self,name,age):
        # 此处的属性name,age都未作私有化处理
    	self.name = name
        self.age = age
        # 此处定义一个打印函数printer，同样未封装
    def printer(self):
        print self.age
    
# 对类进行了实例化，出入了相应的参数
Me = BOY("Lynn",25)
print Me.name
Me.printer()
```

因为上面函数中定义的属性和方法军未封装，那么在类的外面我们是可以调用类中的属性和方法的，即通过实例调用。
下面为上面程序运行的结果：

```python
>>> Lynn
>>> 25
```

*进行封装（私有化）处理后*

```python
# 定义一个BOY类,
class BOY():
	'''
	利用初始化函数初始化类的共同特性，name，age
    此处的属性名字均添加双下划线'__'，封装私有化处理
    '''
    def __init__(self,name,age):
        # 此处的属性name,age都进行私有化处理
    	self.__name = name
        self.__age = age
        # 此处定义的方法也进行封装
    def __printer(self):
        print self.age
    
# 对类进行了实例化，出入了相应的参数
Me = BOY("Lynn",25)
print Me.name
Me.printer()
```

按照Python私有化定义来看，对类的属性和方法进行私有化，类外部是无法正常对其调用的，那么程序运行的结果是：

```python
Traceback (most recent call last):
  File "E:/PycharmProjects/MD/test.py", line 14, in <module>
    print Me.name
AttributeError: BOY instance has no attribute 'name'
```
此时控制台提示属性错误(AttributeError)，*BOY instance has no attribute 'name'*即BOY实例中不含有*name*属性。说明我们在累的外面不能通过实例去访问类里面的私有化属性，这个属性已经被类私有化，通过这种方式提高了代码的安全性、私密性。

由于程序的执行的顺序性，并没有抛出调用*printer*的错误，如果将属性不做私有化处理（即去掉属性*name*，*age*前面的两条下滑线s），只对方法做私有化封装处理，那么程序的运行结果就是：
```python
Lynn
Traceback (most recent call last):
  File "E:/PycharmProjects/MD/test.py", line 15, in <module>
    Me.printer()
AttributeError: BOY instance has no attribute 'printer'

```
因为*name*，*age*属性为能够正常调用，所以能够正常显示名字，但是*printer*方法由于做了私有化封装不能正常调用，抛出异常。

将代码封装私有化之后代码的健壮性安全性提高了，那么问题又来了，如果我们需要得到*name*，*age*该怎么办？这个时候就需要在类的内部添加一个方法用于外部调用以得到*name*，*age*属性。同样，如果类在初始化的时候给了*name*赋值，当我们需要另外再给*name*赋新值的时候，这个时候我们也可以在类的内部增加一个修改*name*的方法，然后通过外部调用来修改值。

就像下面：

```python
#-*- coding:utf-8 -*-

class BOY():

    def __init__(self,age，name = "David"):
        self.__name = name 
        self.__age = age
        
    # 在类的内部定义一个专门用来获取name的方法
    def get_name(self):
        print self.__name
        return None
    # 在类的内部定义一个专门用来获取age的方法
    def get_age(self):
        print self.__age
        return None
    # 定义修改name值得方法
    def change_name(self,name):
        self.name = name

# 对方法进行实例化
Me = BOY(25)
''' 
 name,age私有化封装之后无法直接调用，在此调用打印
 name,age的方法 查看初始化name，age的值
'''
Me.get_name()
Me.get_age()
'''
 调用修改name的方法，将初始化的 name = "David"
 修改为 name = "Lynn",调用方法如下，将新值作为
 参数传入name
'''
Me.change_name("Lynn")
# 再次调用打印name方法，查看修改是否成功
Me.get_name()
```
上面程序的运行结果如下：
```python
>>> David
>>> 25
>>> Lynn
```
说明调用打印*name*和*age*的方法成功，并成功修改了*name*。