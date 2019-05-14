## 单进程服务器-gevent版
### gevent版-TCP服务器

    import sys
    import time
    import gevent

    from gevent import socket,monkey
    monkey.patch_all()

    def handle_request(conn):
        while True:
            data = conn.recv(1024)
            if not data:
                conn.close()
                break
            print("recv:", data)
            conn.send(data)


    def server(port):
        s = socket.socket()
        s.bind(('', port))
        s.listen(5)
        while True:
            cli, addr = s.accept()
            gevent.spawn(handle_request, cli)

    if __name__ == '__main__':
        server(7788)
