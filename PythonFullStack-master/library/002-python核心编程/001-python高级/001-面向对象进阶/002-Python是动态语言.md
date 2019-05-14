## python是动态语言

### 1. 动态语言的定义

动态编程语言 是 高级程序设计语言 的一个类别，在计算机科学领域已被广泛应用。它是一类 在运行时可以改变其结构的语言 ：例如新的函数、对象、甚至代码可以被引进，已有的函数可以被删除或是其他结构上的变化。动态语言目前非常具有活力。例如JavaScript便是一个动态语言，除此之外如 PHP 、 Ruby 、 Python 等也都属于动态语言，而 C 、 C++ 等语言则不属于动态语言。----来自 维基百科

### 2. 运行的过程中给对象绑定(添加)属性

    >>> class Person(object):
        def __init__(self, name = None, age = None):
            self.name = name
            self.age = age


    >>> P = Person("小明", "24")
    >>>  

在这里，我们定义了1个类Person，在这个类里，定义了两个初始属性name和age，但是人还有性别啊！如果这个类不是你写的是不是你会尝试访问性别这个属性呢？

    >>> P.sex = "male"
    >>> P.sex
    'male'
    >>>  

这时候就发现问题了，我们定义的类里面没有sex这个属性啊！怎么回事呢？ 这就是动态语言的魅力和坑！ 这里 实际上就是 动态给实例绑定属性！

### 3. 运行的过程中给类绑定(添加)属性

    >>> P1 = Person("小丽", "25")
    >>> P1.sex

    Traceback (most recent call last):
      File "<pyshell#21>", line 1, in <module>
        P1.sex
    AttributeError: Person instance has no attribute 'sex'
    >>>  

我们尝试打印P1.sex，发现报错，P1没有sex这个属性！---- 给P这个实例绑定属性对P1这个实例不起作用！ 那我们要给所有的Person的实例加上 sex属性怎么办呢？ 答案就是直接给Person绑定属性！

    >>>> Person.sex = None #给类Person添加一个属性
    >>> P1 = Person("小丽", "25")
    >>> print(P1.sex) #如果P1这个实例对象中没有sex属性的话，那么就会访问它的类属性
    None #可以看到没有出现异常
    >>>
### 4. 运行的过程中给类绑定(添加)方法

我们直接给Person绑定sex这个属性，重新实例化P1后，P1就有sex这个属性了！ 那么function呢？怎么绑定？

    >>> class Person(object):
        def __init__(self, name = None, age = None):
            self.name = name
            self.age = age
        def eat(self):
            print("eat food")


    >>> def run(self, speed):
        print("%s在移动, 速度是 %d km/h"%(self.name, speed))


    >>> P = Person("老王", 24)
    >>> P.eat()
    eat food
    >>>
    >>> P.run()
    Traceback (most recent call last):
      File "<pyshell#5>", line 1, in <module>
        P.run()
    AttributeError: Person instance has no attribute 'run'
    >>>
    >>>
    >>> import types
    >>> P.run = types.MethodType(run, P)
    >>> P.run(180)  

老王在移动,速度是 180 km/h
既然给类添加方法，是使用类名.方法名 = xxxx，那么给对象添加一个方法也是类似的对象.方法名 = xxxx

完整的代码如下：



    import types

    #定义了一个类
    class Person(object):
        num = 0
        def __init__(self, name = None, age = None):
            self.name = name
            self.age = age
        def eat(self):
            print("eat food")

    #定义一个实例方法
    def run(self, speed):
        print("%s在移动, 速度是 %d km/h"%(self.name, speed))

    #定义一个类方法
    @classmethod
    def testClass(cls):
        cls.num = 100

    #定义一个静态方法
    @staticmethod
    def testStatic():
        print("---static method----")

    #创建一个实例对象
    P = Person("老王", 24)
    #调用在class中的方法
    P.eat()

    #给这个对象添加实例方法
    P.run = types.MethodType(run, P)
    #调用实例方法
    P.run(180)

    #给Person类绑定类方法
    Person.testClass = testClass
    #调用类方法
    print(Person.num)
    Person.testClass()
    print(Person.num)

    #给Person类绑定静态方法
    Person.testStatic = testStatic
    #调用静态方法
    Person.testStatic()
### 5. 运行的过程中删除属性、方法

删除的方法:

1.del 对象.属性名  
2.delattr(对象, "属性名")  

通过以上例子可以得出一个结论：相对于动态语言，静态语言具有严谨性！所以，玩动态语言的时候，小心动态的坑！

那么怎么避免这种情况呢？ 请使用\__slots\__
