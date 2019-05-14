## 多线程-threading
python的thread模块是比较底层的模块，python的threading模块是对thread做了一些包装的，可以更加方便的被使用

---
### 1. 使用threading模块
##### 单线程执行
#coding=utf-8
    import time

    def saySorry():
        print("亲爱的，我错了，我能吃饭了吗？")
        time.sleep(1)

    if __name__ == "__main__":
        for i in range(5):
            saySorry()
运行结果：

![alt文本](Images/02-就业班-01-6.gif "Title")

##### 多线程执行
    #coding=utf-8
    import threading
    import time

    def saySorry():
        print("亲爱的，我错了，我能吃饭了吗？")
        time.sleep(1)

    if __name__ == "__main__":
        for i in range(5):
            t = threading.Thread(target=saySorry)
            t.start() #启动线程，即让线程开始执行
运行结果：

![alt文本](Images/02-就业班-01-5.gif "Title")

##### 说明
+ 可以明显看出使用了多线程并发的操作，花费时间要短很多
+ 创建好的线程，需要调用start()方法来启动

### 2. 主线程会等待所有的子线程结束后才结束
#coding=utf-8
    import threading
    from time import sleep,ctime

    def sing():
        for i in range(3):
            print("正在唱歌...%d"%i)
            sleep(1)

    def dance():
        for i in range(3):
            print("正在跳舞...%d"%i)
            sleep(1)

    if __name__ == '__main__':
        print('---开始---:%s'%ctime())

        t1 = threading.Thread(target=sing)
        t2 = threading.Thread(target=dance)

        t1.start()
        t2.start()

        #sleep(5) # 屏蔽此行代码，试试看，程序是否会立马结束？
        print('---结束---:%s'%ctime())

![alt文本](Images/18.gif "Title")

### 3. 查看线程数量
    #coding=utf-8
    import threading
    from time import sleep,ctime

    def sing():
        for i in range(3):
            print("正在唱歌...%d"%i)
            sleep(1)

    def dance():
        for i in range(3):
            print("正在跳舞...%d"%i)
            sleep(1)

    if __name__ == '__main__':
        print('---开始---:%s'%ctime())

        t1 = threading.Thread(target=sing)
        t2 = threading.Thread(target=dance)

        t1.start()
        t2.start()

        while True:
            length = len(threading.enumerate())
            print('当前运行的线程数为：%d'%length)
            if length<=1:
                break

            sleep(0.5)

![alt文本](Images/17.gif "Title")
