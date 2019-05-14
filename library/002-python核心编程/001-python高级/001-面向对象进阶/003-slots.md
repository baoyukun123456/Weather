## \__slots\__

现在我们终于明白了，动态语言与静态语言的不同

动态语言：可以在运行的过程中，修改代码

静态语言：编译时已经确定好代码，运行过程中不能修改

如果我们想要限制实例的属性怎么办？比如，只允许对Person实例添加name和age属性。

为了达到限制的目的，Python允许在定义class的时候，定义一个特殊的__slots__变量，来限制该class实例能添加的属性：

    >>> class Person(object):
        __slots__ = ("name", "age")

    >>> P = Person()
    >>> P.name = "老王"
    >>> P.age = 20
    >>> P.score = 100
    Traceback (most recent call last):
      File "<pyshell#3>", line 1, in <module>
    AttributeError: Person instance has no attribute 'score'
    >>>

注意:

* 使用\__slots\__要注意，\__slots\__定义的属性仅对当前类实例起作用，对继承的子类是不起作用的    


    In [67]: class Test(Person):
        ...:     pass
        ...:  
    In [68]: t = Test()

    In [69]: t.score = 100
