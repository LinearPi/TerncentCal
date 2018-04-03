### uwsgi

```shell
[uwsgi]
socket = 127.0.0.1:8000
chdir = /data/mysite  #项目的位置
wsgi-file = mysite/wsgi.py  #项目的地方
processes = 4
threads = 2
stats = 127.0.0.1:9191  #这个不知道是什么
uid = nobody
gid = nobody
master = true
harakiri = 30
daemonize = /data/mysite/uwsgi.log  
plugins = python  # 这个有是什么鬼
```

