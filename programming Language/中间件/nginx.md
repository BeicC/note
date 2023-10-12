* nginx的反向代理
<img src="./image/nginx反向代理.png">

正向还是反向，是阵对客户端（用户）来讲的

正向代理：帮助client进行发起请求，作用是隐藏客户端信息
反向代理：帮助server，作用是隐藏服务器信息

ngnix中的一些路径
* 配置文件：`/etc/nginx`
* index页面：`/usr/share/nginx/html`


situation：我需要让nginx把所有来自80端口的请求转到商品服务

action：
1、nginx的配置文件的路径是：`/etc/nginx`,将`config.d/default.conf`复制一份
```bash
cp default.conf gulimail.conf
```
2、
Q1: server_name为什么要写gulimail？写192.168.153.3不行吗
浏览器中用什么发起请求就写什么；因为浏览器中的地址会被放到request header中的host中。nginx根据host中的值进行相应的处理
```bash
server {
    listen       80;
    listen  [::]:80;
    -server_name  localhost;
    +server_name  gulimail.com
    #access_log  /var/log/nginx/host.access.log  main;

    location / {
        root   /usr/share/nginx/html;
        index  index.html index.htm;
    }

    #error_page  404              /404.html;

    # redirect server error pages to the static page /50x.html
    #
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }

    # proxy the PHP scripts to Apache listening on 127.0.0.1:80
    #
    #location ~ \.php$ {
    #    proxy_pass   http://127.0.0.1;
    #}

    # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
    #
    #location ~ \.php$ {
    #    root           html;
    #    fastcgi_pass   127.0.0.1:9000;
    #    fastcgi_index  index.php;
    #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
    #    include        fastcgi_params;
    #}

    # deny access to .htaccess files, if Apache's document root
    # concurs with nginx's one
    #
    #location ~ /\.ht {
    #    deny  all;
    #}
}
```
