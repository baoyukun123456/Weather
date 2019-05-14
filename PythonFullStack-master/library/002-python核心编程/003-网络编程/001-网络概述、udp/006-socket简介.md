## socket简介
### 1.本地的进程间通信（IPC）有很多种方式，例如
+ 队列
+ 同步（互斥锁、条件变量等）

以上通信方式都是在一台机器上不同进程之间的通信方式，那么问题来了

网络中进程之间如何通信？

### 2. 网络中进程之间如何通信
首要解决的问题是如何唯一标识一个进程，否则通信无从谈起！

在本地可以通过进程PID来唯一标识一个进程，但是在网络中这是行不通的。

其实TCP/IP协议族已经帮我们解决了这个问题，网络层的“ip地址”可以唯一标识网络中的主机，而传输层的“协议+端口”可以唯一标识主机中的应用程序（进程）。

这样利用ip地址，协议，端口就可以标识网络的进程了，网络中的进程通信就可以利用这个标志与其它进程进行交互

### 3. 什么是socket
socket(简称 套接字) 是进程间通信的一种方式，它与其他进程间通信的一个主要不同是：

它能实现不同主机间的进程间通信，我们网络上各种各样的服务大多都是基于 Socket 来完成通信的

例如我们每天浏览网页、QQ 聊天、收发 email 等等

### 4. 创建socket
在 Python 中 使用socket 模块的函数 socket 就可以完成：

socket.socket(AddressFamily, Type)
##### 说明：
函数 socket.socket 创建一个 socket，返回该 socket 的描述符，该函数带有两个参数：

+ Address Family：可以选择 AF_INET（用于 Internet 进程间通信） 或者 AF_UNIX（用于同一台机器进程间通信）,实际工作中常用AF_INET
+ Type：套接字类型，可以是 SOCK_STREAM（流式套接字，主要用于 TCP 协议）或者 SOCK_DGRAM（数据报套接字，主要用于 UDP 协议）

创建一个tcp socket（tcp套接字）

    import socket

    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

    print 'Socket Created'
创建一个udp socket（udp套接字）

    import socket

    s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

    print 'Socket Created'
