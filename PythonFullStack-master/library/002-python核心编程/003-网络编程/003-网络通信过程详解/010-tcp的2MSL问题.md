## tcp的2MSL问题
### tcp的2MSL问题
![alt文本](Images/2MSL.JPG "Title")

#### 说明
2MSL即两倍的MSL，TCP的TIME_WAIT状态也称为2MSL等待状态，

当TCP的一端发起主动关闭，在发出最后一个ACK包后，

即第3次握 手完成后发送了第四次握手的ACK包后就进入了TIME_WAIT状态，

必须在此状态上停留两倍的MSL时间，

等待2MSL时间主要目的是怕最后一个 ACK包对方没收到，

那么对方在超时后将重发第三次握手的FIN包，

主动关闭端接到重发的FIN包后可以再发一个ACK应答包。

在TIME_WAIT状态 时两端的端口不能使用，要等到2MSL时间结束才可继续使用。

当连接处于2MSL等待阶段时任何迟到的报文段都将被丢弃。

不过在实际应用中可以通过设置 SO_REUSEADDR选项达到不必等待2MSL时间结束再使用此端口。
