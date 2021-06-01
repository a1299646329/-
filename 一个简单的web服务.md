# **轮子**

在这个轮子满天飞的时代，试着学会造一个轮子似乎是个不错的注意。
用python写一个web服务，似乎有好多种轮子，web.py, flask, django, tornado 等等。
那么你知道这些轮子是怎么实现的吗？今天不跟你们讨论这个，我只想造一个轮子，
来自己实现一个web框架，或许它并不好用，但我觉得意义肯定是重大的

## socket
众所周知，http 是基于tcp协议的应用层协议。socket 是Tcp/IP协议的封装，socket不是协议，而是一套api
所以我们可以考虑用socket来实现我们的轮子计划。

```python
import socket

web = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
web.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)

ip_port = ('127.0.0.1', 9000)
web.bind(ip_port)
web.listen(5)

while True:
    conn, addr = web.accept()
    data = conn.recv(1024)
    conn.send(bytes("HTTP/1.1 201 OK\r\n\r\n", 'utf-8'))
    conn.send(bytes("<h1>welcome nginx</h1>", 'utf-8'))
    conn.close()
```
这样我们就实现了一个简单的web服务搭建， 运行代码，试着访问下http://127.0.0.1:9000/