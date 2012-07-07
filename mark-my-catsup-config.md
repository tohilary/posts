#记录一下Catsup的Nginx设置
- date: 2012-7-7

----

nginx.conf:
```

user  nginx;
worker_processes  1;

error_log  /var/log/nginx/error.log warn;
pid        /var/run/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    keepalive_timeout  65;

    gzip  on;
    gzip_disable "msie6";
    gzip_proxied any;
    gzip_types text/plain text/css text/xml application/x-javascript application/xml application/atom+xml text/javascript;  

    include /etc/nginx/sites-available/*.conf;
}

```

catsup.conf:
```
upstream catsup_whtsky{
    server localhost:8001;
    server localhost:8002;
    server localhost:8003;
    server localhost:8004;
}
server {
    server_name whouz.com;

    proxy_read_timeout 200;
    tcp_nopush on;
    gzip_min_length 1000;
    gzip_proxied any;
    proxy_next_upstream error;

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
```