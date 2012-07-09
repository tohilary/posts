#在Tornado中获取访客ip
- date: 2012-7-9

---
以前都是用`self.request.headers['X-Real-Ip']`来取访客ip，最近翻源码才发现官方已经给获取好了:
```python
        if connection and connection.xheaders:
            # Squid uses X-Forwarded-For, others use X-Real-Ip
            self.remote_ip = self.headers.get(
                "X-Real-Ip", self.headers.get("X-Forwarded-For", remote_ip))
```
[https://github.com/facebook/tornado/blob/master/tornado/httpserver.py#L358](https://github.com/facebook/tornado/blob/master/tornado/httpserver.py#L358)

用起来很简单：
把`http_server = tornado.httpserver.HTTPServer(application)`改成`http_server = tornado.httpserver.HTTPServer(application, xheaders=True)`
然后直接在RequestHandler里使用`self.request.remote_ip`就可以了