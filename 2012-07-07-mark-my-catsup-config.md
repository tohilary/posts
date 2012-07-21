#记录一下Catsup的Nginx设置
- date: 2012-7-7
- tags: catsup, nginx

----

catsup.conf:
```
upstream catsup_whtsky{
    server localhost:2331;
}
server {
    server_name whouz.com;

    proxy_read_timeout 200;
    tcp_nopush on;
    gzip_min_length 1000;
    gzip_proxied any;
    proxy_next_upstream error;

    if ($host != 'whouz.com' ) { 
        rewrite  ^/(.*)$  http://whouz.com/$1  permanent; 
    }

    listen 80;

    location / {
        proxy_pass_header Server;
        proxy_set_header Host $http_host;
        proxy_redirect off;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Scheme $scheme;

        # proxy to your upstream
        proxy_pass http://catsup_whtsky;
    }
}

server {
    server_name assets.whouz.com;
    gzip_min_length 1;
    gzip_proxied any;

    listen 80;

    add_header Vary Accept-Encoding;
    access_log   off;

    root /web/catsup/themes/sealscript/static;
    expires 30d;
}
```