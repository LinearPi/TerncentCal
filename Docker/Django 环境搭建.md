#### django 项目部署

# Django 环境搭建

## 安装 Django

> 任务时间：5min ~ 10min

先安装 PIP，再通过 PIP 安装 Django

### 安装 PIP

```
cd /data;
mkdir tmp;
cd tmp;
wget https://bootstrap.pypa.io/get-pip.py;
python ./get-pip.py;

```

### 使用 PIP，安装 Django

```
pip install Django==1.11.7

```

## 安装 Mysql

> 任务时间：10min ~ 15min

### 安装并启动 mariadb

因为 CentOS 7 之后的版本都不在提供 Mysql 安装源，这里我们使用 mariadb 代替 mysql，依次执行下列命令

```
yum install mariadb mariadb-server -y

```

```
yum install MySQL-python -y

```

```
systemctl start mariadb

```

### 对 mariadb 进行初始化设置

- 执行下面命令，根据提示操作
- 设置新密码为 test
- 默认密码为空，直接回车即可

```
mysql_secure_installation

```

### 使用设置的密码登陆 mariadb

- 登陆 db，这里假设密码被设置为 test

```
mysql -uroot -ptest

```

### 创建一个数据库

```
create database mysite;

```

成功后，输入 exit 命令退出 db

```
exit

```

## 创建 Django 项目

> 任务时间：10min ~ 15min

### 创建 mysite 项目

- 在 /data/ 目录下，创建一个名为 mysite 的 Django 项目

```
cd /data/
django-admin startproject mysite

```

### 修改配置文件，与 Mysql 数据库相关联

- 备注：SECRET_KEY 配置项无需修改
- *编辑 /data/mysite/mysite/settings.py*

##### 示例代码：/data/mysite/mysite/settings.py

```

ALLOWED_HOSTS = ["*"]

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'mysite',
        'PASSWORD':'test',
        'USER': 'root',
        'HOST':'127.0.0.1',
        'PORT':'3306',
    }
}



```

### 创建 Django 数据库

```
cd /data/mysite
python manage.py migrate

```

### 启动 Django

```
python manage.py runserver

```

- 如果没有报错，就说明 Django 已经安装成功了，并且跟 Mysql 的连接正常

### 退出 Django

```
按 ctrl+c 退出 Django 服务

```

## 安装 Nginx

> 任务时间：5min ~ 10min

### 通过 yum 安装 Nginx

```
yum install nginx -y

```

### 启动 Nginx 服务

```
systemctl start nginx

```

- 访问下面的链接，可以看到 nginx 的欢迎界面
  http://<您的 CVM IP 地址>/

## 安装 uwsgi

> 任务时间：5min ~ 10min

### 使用 yum 命令安装 uwsgi

```
yum install uwsgi uwsgi-plugin-python -y

```

## 让 Nginx，uwsgi，Django 协同工作

> 任务时间：5min ~ 15min

### 修改 Nginx 配置文件

- *编辑 /etc/nginx/nginx.conf*

##### 示例代码：/etc/nginx/nginx.conf

```
# For more information on configuration, see:
#   * Official English Documentation: http://nginx.org/en/docs/
#   * Official Russian Documentation: http://nginx.org/ru/docs/

user nginx;
worker_processes auto;
error_log /var/log/nginx/error.log;
pid /run/nginx.pid;

# Load dynamic modules. See /usr/share/nginx/README.dynamic.
include /usr/share/nginx/modules/*.conf;

events {
    worker_connections 1024;
}

http {
    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile            on;
    tcp_nopush          on;
    tcp_nodelay         on;
    keepalive_timeout   65;
    types_hash_max_size 2048;

    include             /etc/nginx/mime.types;
    default_type        application/octet-stream;

    # Load modular configuration files from the /etc/nginx/conf.d directory.
    # See http://nginx.org/en/docs/ngx_core_module.html#include
    # for more information.
    include /etc/nginx/conf.d/*.conf;

    server {
        listen       80 default_server;
        listen       [::]:80 default_server;
        server_name  _;
        root         /usr/share/nginx/html;

        # Load configuration files for the default server block.
        include /etc/nginx/default.d/*.conf;

        location / {
            include uwsgi_params;
            uwsgi_pass 127.0.0.1:8000;
        }

        error_page 404 /404.html;
            location = /40x.html {
        }

        error_page 500 502 503 504 /50x.html;
            location = /50x.html {
        }
    }

# Settings for a TLS enabled server.
#
#    server {
#        listen       443 ssl http2 default_server;
#        listen       [::]:443 ssl http2 default_server;
#        server_name  _;
#        root         /usr/share/nginx/html;
#
#        ssl_certificate "/etc/pki/nginx/server.crt";
#        ssl_certificate_key "/etc/pki/nginx/private/server.key";
#        ssl_session_cache shared:SSL:1m;
#        ssl_session_timeout  10m;
#        ssl_ciphers HIGH:!aNULL:!MD5;
#        ssl_prefer_server_ciphers on;
#
#        # Load configuration files for the default server block.
#        include /etc/nginx/default.d/*.conf;
#
#        location / {
#        }
#
#        error_page 404 /404.html;
#            location = /40x.html {
#        }
#
#        error_page 500 502 503 504 /50x.html;
#            location = /50x.html {
#        }
#    }

}

```

### 重启 Nginx

```
/usr/sbin/nginx -s reload

```

### 创建 uwsgi 配置文件

请在 `/data/mysite` 目录下*创建 uwsgi.ini*，参考下面的内容。

##### 示例代码：/data/mysite/uwsgi.ini

```
[uwsgi]
socket = 127.0.0.1:8000
chdir = /data/mysite
wsgi-file = mysite/wsgi.py
processes = 4
threads = 2
stats = 127.0.0.1:9191
uid = nobody
gid = nobody
master = true
harakiri = 30
daemonize = /data/mysite/uwsgi.log
plugins = python

```

### 启动 uwsgi

```
uwsgi uwsgi.ini
```

### 测试

访问链接 http://<您的 CVM IP 地址>/ 
如果可以看到 Django 的界面，恭喜你，环境搭建成功