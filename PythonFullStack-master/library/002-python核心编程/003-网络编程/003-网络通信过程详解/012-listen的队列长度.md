## listen的队列长度
### 服务器端运行

    #coding=utf-8
    from socket import *
    from time import sleep

    # 创建socket
    tcpSerSocket = socket(AF_INET, SOCK_STREAM)

    # 绑定本地信息
    address = ('', 7788)
    tcpSerSocket.bind(address)

    connNum = int(raw_input("请输入要最大的链接数:"))

    # 使用socket创建的套接字默认的属性是主动的，使用listen将其变为被动的，这样就可以接收别人的链接了
    tcpSerSocket.listen(connNum)

    while True:

        # 如果有新的客户端来链接服务器，那么就产生一个新的套接字专门为这个客户端服务器
        newSocket, clientAddr = tcpSerSocket.accept()
        print clientAddr
        sleep(1)

### 客户端运行

    #coding=utf-8
    from socket import *

    connNum = raw_input("请输入要链接服务器的次数:")
    for i in range(int(connNum)):
        s = socket(AF_INET, SOCK_STREAM)
        s.connect(("192.168.1.102", 7788))
        print(i)
##### 总结
+ listen中的black表示已经建立链接和半链接的总数
+ 如果当前已建立链接数和半链接数以达到设定值，那么新客户端就不会connect成功，而是等待服务器
