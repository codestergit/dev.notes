# nginx

##location
```
1. location = / {
    # 只有当用户请求是/时，才会匹配
}
2. ~ 匹配URI时时大小写敏感
3. ~* 大小写不敏感
4. ^~ 只需要前半部分匹配即可。
location ^~ /images/ {
    # 以images开头的都会匹配
}
5. @ nginx内容重定向
```

##upstream
```
upstream backend {
    server backend.example.com weight=5;
    server 127.0.0.1:8080 max_fails=3 fail_timeout=30s;
    server unix:tmp/backends3;
}
```

##开启gzip
```
gzip  on;
gzip_http_version 1.1;
gzip_disable "MSIE [1-6]\.";
gzip_vary on;
gzip_comp_level 2;
gzip_proxied any;
gzip_types text/plain application/javascript text/css text/javascript;
```

