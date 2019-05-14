## Python内置类型性能分析
---

### timeit模块
timeit模块可以用来测试一小段Python代码的执行速度。

##### class timeit.Timer(stmt='pass', setup='pass', timer=<timer function>)
Timer是测量小段代码执行速度的类。

stmt参数是要测试的代码语句（statment）；

setup参数是运行代码时需要的设置；

timer参数是一个定时器函数，与平台有关。

#####  timeit.Timer.timeit(number=1000000)
Timer类中测试语句执行速度的对象方法。number参数是测试代码时的测试次数，默认为1000000次。方法返回执行代码的平均耗时，一个float类型的秒数。

### list的操作测试
    def test1():
       l = []
       for i in range(1000):
          l = l + [i]
    def test2():
       l = []
       for i in range(1000):
          l.append(i)
    def test3():
       l = [i for i in range(1000)]
    def test4():
       l = list(range(1000))

    from timeit import Timer

    t1 = Timer("test1()", "from __main__ import test1")
    print("concat ",t1.timeit(number=1000), "seconds")
    t2 = Timer("test2()", "from __main__ import test2")
    print("append ",t2.timeit(number=1000), "seconds")
    t3 = Timer("test3()", "from __main__ import test3")
    print("comprehension ",t3.timeit(number=1000), "seconds")
    t4 = Timer("test4()", "from __main__ import test4")
    print("list range ",t4.timeit(number=1000), "seconds")

    # ('concat ', 1.7890608310699463, 'seconds')
    # ('append ', 0.13796091079711914, 'seconds')
    # ('comprehension ', 0.05671119689941406, 'seconds')
    # ('list range ', 0.014147043228149414, 'seconds')

### pop操作测试

    x = range(2000000)
    pop_zero = Timer("x.pop(0)","from __main__ import x")
    print("pop_zero ",pop_zero.timeit(number=1000), "seconds")
    x = range(2000000)
    pop_end = Timer("x.pop()","from __main__ import x")
    print("pop_end ",pop_end.timeit(number=1000), "seconds")

    # ('pop_zero ', 1.9101738929748535, 'seconds')
    # ('pop_end ', 0.00023603439331054688, 'seconds')

测试pop操作：从结果可以看出，pop最后一个元素的效率远远高于pop第一个元素

>可以自行尝试下list的append(value)和insert(0,value),即一个后面插入和一个前面插入？？？

### list内置操作的时间复杂度
![alt文本](img/list操作.png "list操作")

### dict内置操作的时间复杂度

![alt文本](img/dict操作.png "dict操作")
