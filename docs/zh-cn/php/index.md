## 语言基础

### 面向对象

我给一些内容点你们自己去了解吧
抽象类和接口类的语法是怎样的？
抽象类和接口类分别能直接实例化吗？
抽象类的方法可以存在方法体吗？
抽象方法和普通方法的区别是什么？
抽象方法可以是静态方法吗？
抽象类可以存在成员属性吗？所有等级都可以吗？
接口类的方法可以存在方法体吗？
接口类可以存在成员属性吗？所有等级都可以吗？
普通类可以同时继承多个抽象类吗？如果可以如何实现？（这里还可以延伸去 Trait）
普通类可以同时实现多个接口类吗？如果可以如何实现？
抽象类可以实现接口类吗？如果可以，那抽象类需要实现接口类定义的方法体吗？
普通类可以既继承抽象类又实现接口类吗？

### 垃圾回收

php 采用引用计数的垃圾回收机制, 那么怎么理解这个引用计数呢?

### php安装扩展

此处以安装swoole扩展为例, 更多信息请查看swoole官方文档[swoole](https://wiki.swoole.com/wiki/page/1.html)。下载swoole源码, pecl下载4.4.5稳定版本[PECL链接](http://pecl.php.net/package/swoole)。

获得源码之后解压并进入目录:

```shell
cd /yourpath/swoole-4.4.5.tgz

tar -zxvf swoole-4.4.5.tgz

cd swoole-4.4.5

```

查找phpize位置, 我的在: /usr/local/opt/php@7.2/bin 目录下面, 绝对路径: /usr/local/opt/php@7.2/bin/phpize

```shell
whereis phpize
```

在目录swoole-4.5.5下, 运行如下命令

```shell
/usr/local/opt/php@7.2/bin/phpize

./configure --with-php-config=/usr/local/opt/php@7.2/bin/php-config

make && make install

```

找到php.ini文件, 在extension定义的地方加上

```php.ini
extension=swoole.so
```

使用php -m 或者 phpinfo()函数检测是否成功加载swoole

>安装时一定要确保php版本达到swoole的版本依赖要求!!



## 设计模式

### 单例模式

