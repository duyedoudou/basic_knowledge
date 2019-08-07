

## TCP&http   socket编程

#### 图示：

![image-20190725175831594](/Users/mac/Library/Application Support/typora-user-images/image-20190725175831594.png)

#### 代码：

```python
# 客户端 client.py
import socket
 
s = socket.socket(socket.AF_INET,socket.SOCK_STREAM)
s.connect(('127.0.0.1',8888))
s.sendall(b'hello world')
data = s.recv(1024)
print(data.decode())
s.close()
```

```python
# 服务器端 server.py
import socket
import time

s = socket.socket()
s.bind(('',8888))
s.listen()

while True:
	client,addr = s.accept()
	print(client)
	timestr = time.ctime(time.time())
	client.send(timestr.encode())
	client.close()
```

#### 运行：

在两个终端运行，两个文件。python server.py   python client.py

```
# 服务器端
(base) MacdeMacBook-Pro-2:Movies mac$ python server.py 
<socket.socket fd=4, family=AddressFamily.AF_INET, type=SocketKind.SOCK_STREAM, proto=0, laddr=('127.0.0.1', 8888), raddr=('127.0.0.1', 57946)>

#客户端
(base) MacdeMacBook-Pro-2:Movies mac$ python client.py 
Thu Jul 25 17:56:32 2019
```




####  socket发送http请求： 


```python
# socket发送http请求  socket_send_http.py
import socket

s = socket.socket()
s.connect(('www.baidu.com',80))
http = b'GET / HTTP/1.1\r\nHost:www.baidu.com\r\n\r\n'
s.sendall(http)
buf = s.recv(1024)
print(buf)
s.close()
```

