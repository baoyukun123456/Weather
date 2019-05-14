## 协程-gevent版

greenlet已经实现了协程，但是这个还的人工切换，是不是觉得太麻烦了，不要捉急，python还有一个比greenlet更强大的并且能够自动切换任务的模块gevent

其原理是当一个greenlet遇到IO(指的是input output 输入输出，比如网络、文件操作等)操作时，比如访问网络，就自动切换到其他的greenlet，等到IO操作完成，再在适当的时候切换回来继续执行。

由于IO操作非常耗时，经常使程序处于等待状态，有了gevent为我们自动切换协程，就保证总有greenlet在运行，而不是等待IO

### 1. gevent的使用

    #coding=utf-8

    #请使用python 2 来执行此程序

    import gevent

    def f(n):
        for i in range(n):
            print gevent.getcurrent(), i

    g1 = gevent.spawn(f, 5)
    g2 = gevent.spawn(f, 5)
    g3 = gevent.spawn(f, 5)
    g1.join()
    g2.join()
    g3.join()  

运行结果

    <Greenlet at 0x10e49f550: f(5)> 0
    <Greenlet at 0x10e49f550: f(5)> 1
    <Greenlet at 0x10e49f550: f(5)> 2
    <Greenlet at 0x10e49f550: f(5)> 3
    <Greenlet at 0x10e49f550: f(5)> 4
    <Greenlet at 0x10e49f910: f(5)> 0
    <Greenlet at 0x10e49f910: f(5)> 1
    <Greenlet at 0x10e49f910: f(5)> 2
    <Greenlet at 0x10e49f910: f(5)> 3
    <Greenlet at 0x10e49f910: f(5)> 4
    <Greenlet at 0x10e49f4b0: f(5)> 0
    <Greenlet at 0x10e49f4b0: f(5)> 1
    <Greenlet at 0x10e49f4b0: f(5)> 2
    <Greenlet at 0x10e49f4b0: f(5)> 3
    <Greenlet at 0x10e49f4b0: f(5)> 4  

可以看到，3个greenlet是依次运行而不是交替运行

### 2. gevent切换执行


    import gevent

    def f(n):
        for i in range(n):
            print gevent.getcurrent(), i
            #用来模拟一个耗时操作，注意不是time模块中的sleep
            gevent.sleep(1)

    g1 = gevent.spawn(f, 5)
    g2 = gevent.spawn(f, 5)
    g3 = gevent.spawn(f, 5)
    g1.join()
    g2.join()
    g3.join()  

运行结果

    <Greenlet at 0x7fa70ffa1c30: f(5)> 0
    <Greenlet at 0x7fa70ffa1870: f(5)> 0
    <Greenlet at 0x7fa70ffa1eb0: f(5)> 0
    <Greenlet at 0x7fa70ffa1c30: f(5)> 1
    <Greenlet at 0x7fa70ffa1870: f(5)> 1
    <Greenlet at 0x7fa70ffa1eb0: f(5)> 1
    <Greenlet at 0x7fa70ffa1c30: f(5)> 2
    <Greenlet at 0x7fa70ffa1870: f(5)> 2
    <Greenlet at 0x7fa70ffa1eb0: f(5)> 2
    <Greenlet at 0x7fa70ffa1c30: f(5)> 3
    <Greenlet at 0x7fa70ffa1870: f(5)> 3
    <Greenlet at 0x7fa70ffa1eb0: f(5)> 3
    <Greenlet at 0x7fa70ffa1c30: f(5)> 4
    <Greenlet at 0x7fa70ffa1870: f(5)> 4
    <Greenlet at 0x7fa70ffa1eb0: f(5)> 4  

3个greenlet交替运行

### 3. gevent并发下载器

当然，实际代码里，我们不会用gevent.sleep()去切换协程，而是在执行到IO操作时，gevent自动切换，代码如下

    #coding=utf-8

    from gevent import monkey;
    import gevent
    import urllib2

    #有IO才做时需要这一句
    monkey.patch_all()

    def myDownLoad(url):
        print('GET: %s' % url)
        resp = urllib2.urlopen(url)
        data = resp.read()
        print('%d bytes received from %s.' % (len(data), url))

    gevent.joinall([
            gevent.spawn(myDownLoad, 'http://www.baidu.com/'),
            gevent.spawn(myDownLoad, 'http://www.itcast.cn/'),
            gevent.spawn(myDownLoad, 'http://www.itheima.com/'),
    ])
运行结果

    GET: http://www.baidu.com/
    GET: http://www.itcast.cn/
    GET: http://www.itheima.com/
    102247 bytes received from http://www.baidu.com/.
    166903 bytes received from http://www.itheima.com/.
    162294 bytes received from http://www.itcast.cn/.  

从上能够看到是先发送的获取baidu的相关信息，然后依次是itcast、itheima，但是收到数据的先后顺序不一定与发送顺序相同，这也就体现出了异步，即不确定什么时候会收到数据，顺序不一定
