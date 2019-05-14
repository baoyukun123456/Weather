## \__init\__()方法
想一想:

在上一小节的demo中，我们已经给BMW这个对象添加了2个属性，wheelNum（车的轮胎数量）以及color（车的颜色），试想如果再次创建一个对象的话，肯定也需要进行添加属性，显然这样做很费事，那么有没有办法能够在创建对象的时候，就顺便把车这个对象的属性给设置呢？

答:

    __init__()方法

---

### <1>使用方式
    def 类名:
        #初始化函数，用来完成一些默认的设定
        def __init__():
            pass
### <2>__init__()方法的调用

    # 定义汽车类
    class Car:

        def __init__(self):
            self.wheelNum = 4
            self.color = '蓝色'

        def move(self):
            print('车在跑，目标:夏威夷')

    # 创建对象
    BMW = Car()

    print('车的颜色为:%s'%BMW.color)
    print('车轮胎数量为:%d'%BMW.wheelNum)

![alt文本](Images/Snip20160820_3.png "Title")

总结1

当创建Car对象后，在没有调用\__init\__()方法的前提下，BMW就默认拥有了2个属性wheelNum和color，原因是\__init\__()方法是在创建对象后，就立刻被默认调用了

### 想一想
既然在创建完对象后\__init\__()方法已经被默认的执行了，那么能否让对象在调用\__init\__()方法的时候传递一些参数呢？如果可以，那怎样传递呢？


    # 定义汽车类
    class Car:

        def __init__(self, newWheelNum, newColor):
            self.wheelNum = newWheelNum
            self.color = newColor

        def move(self):
            print('车在跑，目标:夏威夷')

    # 创建对象
    BMW = Car(4, 'green')

    print('车的颜色为:%s'%BMW.color)
    print('车轮子数量为:%d'%BMW.wheelNum)

![alt文本](Images/Snip20160820_4.png "Title")

总结2
+ \__init\__()方法，在创建一个对象时默认被调用，不需要手动调用
+ \__init\__(self)中，默认有1个参数名字为self，如果在创建对象时传递了2个实参，那么\__init\__(self)中出了self作为第一个形参外还需要2个形参，例如\__init\__(self,x,y)
+ \__init\__(self)中的self参数，不需要开发者传递，python解释器会自动把当前的对象引用传递进去
