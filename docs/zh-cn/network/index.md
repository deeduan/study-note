## 网络编程

### 进程


#### 进程关系

进程一般是以进程组的形式存在, 这个进程组可能只有一个进程, 也可能是多个进程.每个进程组都有一个进程组长, 进程组的id就是进程组长的进程id。 一个或者多个进程可以形成一个会话, 创建会话leader也会导致该leader成为进程组的组长,不过有一点需要注意的是: 父进程不能设置为进程组长.否则会返回一个错误。


#### 进程间通信

* 管道pipe
* 消息队列
* 信号
* 共享内存 - php 也有这个扩展
* 信号量?? 这个暂时不太理解

#### 僵尸进程

僵尸进程是当子进程比父进程先结束，而父进程又没有回收子进程，释放子进程占用的资源，此时子进程将成为一个僵尸进程。
如果父进程先退出 ，子进程被init接管，子进程退出后init会回收其占用的相关资源.

PHP生成和观察僵尸进程的一段代码

```php
// 生产僵尸进程  子进程退出, 父进程不做任何处理
foreach (range(1, 10) as $i) {
    $pid = pcntl_fork();

    if ($pid === 0)
    {
        exit(0);
    }
}

sleep(200);
exit('父进程退出');
```
上面这段代码, 生成10个僵尸进程, 但是由于主(父)进程阻塞了200s

php处理僵尸进程有2种方法, 第一种是通过SIGCLD信号, 第二种是通过调用pcntl_wait pcntl_wapid获取子进程退出事件;
子进程退出, 操作系统会给父进程发送SIGCLD信号, 父进程处理这个信号, 再调用wait即可。SIGCLD 信号不可靠, 同一时刻多个同一信号, 
只会报告一次.

> SIGCLD SIGCHLD linux平台下是同样的值

### socket

### 信号

信号机制可以实现进程间通信,
unix信号处理函数被执行的过程中, 如果有其他信号投递, 那么这些信号将被阻塞. 同时, 如果在这个期间, 有很多同样的信号
被投递, 那么unix最后也只处理一次. 这表明unix信号默认是不排队的。


### I/O复用

I/O复用是I/O模型当中的一种, 其本质也是阻塞的。程序升级了, 不在阻塞与accept而是阻塞在select或者epoll等系统调用.I/O复用的第一个使用点就是非阻塞connect。

阻塞的套接字描述符称之为阻塞IO, 同理, 非阻塞的套接字描述符称之为非阻塞IO.php如何处理非阻塞IO的异常? 看下workerman是怎么处理的?


### 高效的事件模式

### 并发模式

#### 半同步半异步模式

2、主进程负责处理连接, 每个子进程有自己的事件循环
3、主进程监控子进程, 处理信号, 处理子进程僵死


### 编程模型

### TCP字节流大小等

### 用户信息

网络编程当中可能需要当前用户和有效用户

