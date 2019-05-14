## netcat
### netcat
	1.瑞士军刀
	2.TCP/IP
		传输控制协议，网络协议
		Socket
		ServerSocket
		Socket
	3.服务端
		nc -l port		//指定监听的端口号
					在本机启动一个ServerSocket进程，&表示在后台运行
	4.客户端
		nc ip port		//指定服务器的ip和监听端口号
		nc localhost 8888  			启动客户端，连接到服务器端口8888
		fg %1		切换
	5.端口扫描
		nc ip -z port1-portn
		nc -v -w 2 master -z 2000-4000
		-v 	详细信息
		-w	连接超时
		-z	端口扫描

### 命令前后台执行切换
---------------------------------
	1.启动进程并将其放在后台
		nc ip port &
	2.启动进程后将其手动放在后台
		Ctrl + z
	3.查看进程
		jobs
	4.fg %n		//切换进程
	  bg %n		//激活进程，并在后台作业
	5.杀死进程
		kill %n
	6.在进程内杀死进程
		Ctrl + c
