## self
### 1. 理解self
看如下示例:

    # 定义一个类
    class Animal:

        # 方法
        def __init__(self, name):
            self.name = name

        def printName(self):
            print('名字为:%s'%self.name)

    # 定义一个函数
    def myPrint(animal):
        animal.printName()


    dog1 = Animal('西西')
    myPrint(dog1)

    dog2 = Animal('北北')
    myPrint(dog2)
运行结果:

![alt文本](Images/Snip20161023_87.png "Title")

##### 总结
+ 所谓的self，可以理解为自己
+ 可以把self当做C++中类里面的this指针一样理解，就是对象自身的意思
+ 某个对象调用其方法时，python解释器会把这个对象作为第一个参数传递给self，所以开发者只需要传递后面的参数即可
