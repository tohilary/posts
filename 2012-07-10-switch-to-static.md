#whouz.com切换到纯静态化
- date: 2012-7-10
- tags: catsup, nginx

---

目前的nginx配置：
```
server {
    server_name whouz.com;

    tcp_nopush on;
    gzip_min_length 500;
    gzip_proxied any;

    if ($host != 'whouz.com' ) {
        rewrite  ^/(.*)$  http://whouz.com/$1  permanent;
    }

    listen 80;

    root /web/catsup/deploy;
}

server {
    server_name assets.whouz.com;
    gzip_min_length 1;
    gzip_proxied any;

    listen 80;

    add_header Vary Accept-Encoding;
    access_log   off;

    root /web/catsup/deploy/static;
    expires 30d;
}

```