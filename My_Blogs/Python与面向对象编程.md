### 浅谈Python中的面向对象编程(Object Oriented Programing,OOP)

在学习编程语言的时候总是能够听到面向对象的编程设计，包括我们在学习Python的初期，也能看到Python是一门解释性的语言，灵活，支持面向对象的程序设计。那么到底什么是面向对象的程序设计，如何理解更为彻底？
今天在这这里就介绍一下，到底什么是面向对象的程序设计。

首先，我们需要知道面向对象的程序设计符合我们人类认识客观事物的规律，这种设计思想也是从人们认识事物的过程中总结而来。我们认识自然中** 类（Class）** 和** 实例（Instance）**是自然而然的，所以面向对象的设计思想也是抽象出类Class和实例Instance。
先介绍一下Python的面向对象中几个常见的术语：** 类、类对象、实例对象、属性、函数和方法**

* **类：**类是对现实世界中一些事物的统称，比如，”狗 dog“就是一个统称，具体的有阿拉斯加犬、柯基、中华田园犬等，但是这些都是狗，所以“狗 dog”就是一个类。我们认识狗这类动物的认知过程就是先认识这一类，然后采取认识后面这些狗。那么在Python中如何体现这一过程呢，先定义一个类

```python
class Dog(object):
    pass
    # This is code block
```

* **类对象：**在上面当你定义类完成之后类对象就产生了,```Dog``` 就是对象(Object),对象支持的操作有两种：** 引用、实例化**。引用操作稍候再将，先介绍实例化操，通过对对象的实例化操作产生一个类的实例(Instance)，就是实例对象。在我们认识客观事物的过程中，比如我们定义了People类。
* **属性：**属性就是描述这一个类的东西。比如，我们向别人介绍一个人，身高、年龄、性别、姓名等，这些都是一个人的属性。

```python
class People():
    # name和height就是People类里面描述一个人的属性
    name = "David"
    height = "175"
    age = "25"    
# 此处变是对People()类进行了实例化people就是实例化对象，
# 然后就可以读取People的属性(因为David也是人类
# 所以他也有人类的属性，姓名，身高，年龄)
people = People()
print people.name,people.height,people.age
```

* ** 函数与方法 **，在此介绍函数与方法的区别可以有一个较为简单的区别方法，我们一般称在类内部定义的函数为方法，称在类外部定义的函数为函数。方法位于class的主体内，是由```def```语句创建的对象，与class绑定起来。

```python
class People():
    # 此处为描写类的属性
    name = "David"
    age = ”25“    
    # 定义一个方法
    def printName(self):
        print self.name
```
上面便是方法的定义使用方式，但是实际中我们在定义类的属性时候写法稍微规范些，如下：
```python
# 定义一个People类
class People():
    # 初始化，此处__init__是一个特殊的方法
    # 可以在创建实例的时候将一些重要的属性进行绑定
    def __init__(self,name,age,height):
        self.name = name
        self.age = age
        self.height = height
    # 定义方法
    def printName(self):
        print self.name
# 实例化    
people = People()
peole.name

```
在上面代码中描述人的基本信息如name,age,height，在Python术语中成为属性，如前面介绍。通常通过类方法函数中的self属性赋值创建。赋值实例属性的第一个值的通常方法是，在```__init__```构造函数方法中将它们赋值给 ```self```，构造函数方法包含； 每次创建一个实例的时候Python会自动运行的代码。

** Lynn **
