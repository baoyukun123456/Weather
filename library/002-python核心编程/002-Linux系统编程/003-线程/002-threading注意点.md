## threading注意点
### 1. 线程执行代码的封装
通过上一小节，能够看出，通过使用threading模块能完成多任务的程序开发，为了让每个线程的封装性更完美，所以使用threading模块时，往往会定义一个新的子类class，只要继承threading.Thread就可以了，然后重写run方法

示例如下：

    #coding=utf-8
    import threading
    import time

    class MyThread(threading.Thread):
        def run(self):
            for i in range(3):
                time.sleep(1)
                msg = "I'm "+self.name+' @ '+str(i) #name属性中保存的是当前线程的名字
                print(msg)


    if __name__ == '__main__':
        t = MyThread()
        t.start()

![alt文本](Images/19.gif "Title")

##### 说明
+ python的threading.Thread类有一个run方法，用于定义线程的功能函数，可以在自己的线程类中覆盖该方法。而创建自己的线程实例后，通过Thread类的start方法，可以启动该线程，交给python虚拟机进行调度，当该线程获得执行的机会时，就会调用run方法执行线程。

### 2. 线程的执行顺序
    #coding=utf-8
    import threading
    import time

    class MyThread(threading.Thread):
        def run(self):
            for i in range(3):
                time.sleep(1)
                msg = "I'm "+self.name+' @ '+str(i)
                print(msg)
    def test():
        for i in range(5):
            t = MyThread()
            t.start()
    if __name__ == '__main__':
        test()

执行结果：(运行的结果可能不一样，但是大体是一致的)

    I'm Thread-1 @ 0
    I'm Thread-2 @ 0
    I'm Thread-5 @ 0
    I'm Thread-3 @ 0
    I'm Thread-4 @ 0
    I'm Thread-3 @ 1
    I'm Thread-4 @ 1
    I'm Thread-5 @ 1
    I'm Thread-1 @ 1
    I'm Thread-2 @ 1
    I'm Thread-4 @ 2
    I'm Thread-5 @ 2
    I'm Thread-2 @ 2
    I'm Thread-1 @ 2
    I'm Thread-3 @ 2
##### 说明
从代码和执行结果我们可以看出，多线程程序的执行顺序是不确定的。当执行到sleep语句时，线程将被阻塞（Blocked），到sleep结束后，线程进入就绪（Runnable）状态，等待调度。而线程调度将自行选择一个线程执行。上面的代码中只能保证每个线程都运行完整个run函数，但是线程的启动顺序、run函数中每次循环的执行顺序都不能确定。

### 3. 总结
+ 每个线程一定会有一个名字，尽管上面的例子中没有指定线程对象的name，但是python会自动为线程指定一个名字。
+ 当线程的run()方法结束时该线程完成。
+ 无法控制线程调度程序，但可以通过别的方式来影响线程调度的方式。
+ 线程的几种状态

![alt文本](Images/Snip20160830_3.png "Title")
