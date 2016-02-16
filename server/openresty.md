# openresty

## install 
```
yum install readline-devel pcre-devel openssl-devel perl postgresql-devel
wget https://openresty.org/download/ngx_openresty-1.9.7.1.tar.gz
tar zxvf ngx_openresty-1.9.7.1.tar.gz
cd ngx_openresty-1.9.7.1
./configure --prefix=/opt/openresty \
            --with-luajit \
            --with-http_iconv_module \
            --with-http_postgres_module \
            --with-debug
gmake  
gmake install
```

###install errors
```
[root@vagrant-centos65 ngx_openresty-1.9.7.1]# yum install  postgresql-devel
Loaded plugins: fastestmirror
```            
resolve  
```
yum install
```

重启nginx加载配置文件
sudo  /opt/openresty/nginx/sbin/nginx  -c /opt/openresty/nginx/conf/nginx.conf -s reload

##install GraphicsMagick
yum install GraphicsMagick
