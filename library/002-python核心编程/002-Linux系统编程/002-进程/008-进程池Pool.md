## 进程池Pool
### 进程池Pool
当需要创建的子进程数量不多时，可以直接利用multiprocessing中的Process动态成生多个进程，但如果是上百甚至上千个目标，手动的去创建进程的工作量巨大，此时就可以用到multiprocessing模块提供的Pool方法。

初始化Pool时，可以指定一个最大进程数，当有新的请求提交到Pool中时，如果池还没有满，那么就会创建一个新的进程用来执行该请求；但如果池中的进程数已经达到指定的最大值，那么该请求就会等待，直到池中有进程结束，才会创建新的进程来执行，请看下面的实例：

    from multiprocessing import Pool
    import os,time,random

    def worker(msg):
        t_start = time.time()
        print("%s开始执行,进程号为%d"%(msg,os.getpid()))
        #random.random()随机生成0~1之间的浮点数
        time.sleep(random.random()*2)
        t_stop = time.time()
        print(msg,"执行完毕，耗时%0.2f"%(t_stop-t_start))

    po=Pool(3) #定义一个进程池，最大进程数3
    for i in range(0,10):
        #Pool.apply_async(要调用的目标,(传递给目标的参数元祖,))
        #每次循环将会用空闲出来的子进程去调用目标
        po.apply_async(worker,(i,))

    print("----start----")
    po.close() #关闭进程池，关闭后po不再接收新的请求
    po.join() #等待po中所有子进程执行完成，必须放在close语句之后
    print("-----end-----")

**运行结果:**

    ----start----
    0开始执行,进程号为21466
    1开始执行,进程号为21468
    2开始执行,进程号为21467
    0 执行完毕，耗时1.01
    3开始执行,进程号为21466
    2 执行完毕，耗时1.24
    4开始执行,进程号为21467
    3 执行完毕，耗时0.56
    5开始执行,进程号为21466
    1 执行完毕，耗时1.68
    6开始执行,进程号为21468
    4 执行完毕，耗时0.67
    7开始执行,进程号为21467
    5 执行完毕，耗时0.83
    8开始执行,进程号为21466
    6 执行完毕，耗时0.75
    9开始执行,进程号为21468
    7 执行完毕，耗时1.03
    8 执行完毕，耗时1.05
    9 执行完毕，耗时1.69
    -----end-----

##### multiprocessing.Pool常用函数解析：

+ apply_async(func[, args[, kwds]]) ：使用非阻塞方式调用func（并行执行，堵塞方式必须等待上一个进程退出才能执行下一个进程），args为传递给func的参数列表，kwds为传递给func的关键字参数列表；

+ apply(func[, args[, kwds]])：使用阻塞方式调用func

+ close()：关闭Pool，使其不再接受新的任务；

+ terminate()：不管任务是否完成，立即终止；

+ join()：主进程阻塞，等待子进程的退出， 必须在close或terminate之后使用；

### apply堵塞式

    from multiprocessing import Pool
    import os,time,random

    def worker(msg):
        t_start = time.time()
        print("%s开始执行,进程号为%d"%(msg,os.getpid()))
        #random.random()随机生成0~1之间的浮点数
        time.sleep(random.random()*2)
        t_stop = time.time()
        print(msg,"执行完毕，耗时%0.2f"%(t_stop-t_start))

    po=Pool(3) #定义一个进程池，最大进程数3
    for i in range(0,10):
        po.apply(worker,(i,))

    print("----start----")
    po.close() #关闭进程池，关闭后po不再接收新的请求
    po.join() #等待po中所有子进程执行完成，必须放在close语句之后
    print("-----end-----")

**运行结果:**

    0开始执行,进程号为21532
    0 执行完毕，耗时1.91
    1开始执行,进程号为21534
    1 执行完毕，耗时1.72
    2开始执行,进程号为21533
    2 执行完毕，耗时0.50
    3开始执行,进程号为21532
    3 执行完毕，耗时1.27
    4开始执行,进程号为21534
    4 执行完毕，耗时1.05
    5开始执行,进程号为21533
    5 执行完毕，耗时1.60
    6开始执行,进程号为21532
    6 执行完毕，耗时0.25
    7开始执行,进程号为21534
    7 执行完毕，耗时0.63
    8开始执行,进程号为21533
    8 执行完毕，耗时1.21
    9开始执行,进程号为21532
    9 执行完毕，耗时0.60
    ----start----
    -----end-----
