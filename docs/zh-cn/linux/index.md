## 常用命令


### ps命令

使用ps命令,可以很方便的查看过去的时间进程的状态(不是实时).

常常会使用的排查命令: 查看php相关的进程信息, 展示状态, 进程id, 父进程id, 进程组id, 会话id, 控制终端

当然还有很多可选,比如查看是哪个cpu执行此进程, 消耗了多少内存等等

```bash
ps -e -ostat,pid,ppid,pgid,sid,cmd | grep php

# 结果
24247   650   649 24211 grep --color=auto php
    1 25019 25019 25019 php-fpm: master process (/etc/php-fpm.conf)
25019 25020 25019 25019 php-fpm: pool www
25019 25021 25019 25019 php-fpm: pool www
25019 25022 25019 25019 php-fpm: pool www
25019 25023 25019 25019 php-fpm: pool www
25019 25024 25019 25019 php-fpm: pool www

```

### netstat命令

使用netstat查看端口服务占用情况, 比如我们需要查询php-fpm占用了什么端口:

```bash
netstat -altnp

# 结果
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 127.0.0.1:9000          0.0.0.0:*               LISTEN      25019/php-fpm: mast 
tcp        0      0 127.0.0.1:6379          0.0.0.0:*               LISTEN      25283/redis-server  
tcp        0      0 0.0.0.0:80              0.0.0.0:*               LISTEN      24902/nginx: master 
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      22965/sshd          
tcp        0     36 172.16.25.152:22        183.233.211.22:59020    ESTABLISHED 24207/sshd: workerm 
tcp6       0      0 :::3306                 :::*                    LISTEN      24359/mysqld 
```

查看有多少连接建立, 并且查看状态, 看看time_wait是不是很多
