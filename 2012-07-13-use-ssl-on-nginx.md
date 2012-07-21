# 在Nginx上配置SSL
- date: 2012-7-13
- tags: nginx

----

```
server {
    server_name t.whouz.com;                                                                                  
    listen 443;
    ssl on;
    ssl_certificate /web/ptap/ssl.crt;
    ssl_certificate_key /web/ptap/ssl.key;
    root /web/catsup/deploy;
}
```