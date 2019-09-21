## Nginx

> 操作系统环境: centos7; 2台机器 web1: 119.21.221.201 web2: 193.113.9.125

### 编译安装nginx服务

### 快速安装nginx服务

```shell
# 查看nginx
yum search nginx
# 安装nginx
yum install nginx
```

### nginx服务的启动和停止

上一部分安装好nginx之后, 我们需要启nginx服务, 我们采用systemctl的方式来管理服务:

```shell
# 检查服务
systemctl status nginx.service(service可省略)
# 启动服务
systemctl start nginx.service
```

### nginx服务平滑升级

### nginx服务日志文件

### nginx服务基础配置

### nginx服务高级配置

### nginx代理

代理是什么?

在Internet上指Proxy Server，是一个软件，运行于某台计算机上，使用代理服务器的计算机与Internet交换信息时都先将信息发给代理服务器，由其转发，并且将收到的应答回送给该计算机。

> 以上代理解释摘自百度百科

nginx支持正向代理和反向代理, 大多数情况下我们使用的都是反向代理。这里给个例子解释一下正向和反向代理。正向代理: 平时我们在公司的时候大家都在内网活动, 如果限制大家访问外网都要使用192.168.0.111这台服务器, 由代理服务器发送请求到外网,这时候就要设置正向代理.


### nginx负载均衡

### nginx转发

### nginx模块
