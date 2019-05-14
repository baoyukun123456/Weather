## udp应用：echo服务器
### 1. 运行现象
测试端

![alt文本](Images/Snip20160901_74.png "Title")

echo服务器端

![alt文本](Images/Snip20160901_73.png "Title")

### 2. 参考代码
    #coding=utf-8

    from socket import *

    #1. 创建套接字
    udpSocket = socket(AF_INET, SOCK_DGRAM)

    #2. 绑定本地的相关信息
    bindAddr = ('', 7788) # ip地址和端口号，ip一般不用写，表示本机的任何一个ip
    udpSocket.bind(bindAddr)

    num = 1
    while True:

        #3. 等待接收对方发送的数据
        recvData = udpSocket.recvfrom(1024) # 1024表示本次接收的最大字节数

        #4. 将接收到的数据再发送给对方
        udpSocket.sendto(recvData[0], recvData[1])

        #5. 统计信息
        print('已经将接收到的第%d个数据返回给对方,内容为:%s'%(num,recvData[0]))
        num+=1


    #5. 关闭套接字
    udpSocket.close()
