# MySQL文件

## 非常规性整理
使用mysql的时候, 我们会去了解一些引擎和表的相关内容。下面就是对针对mysql的相关文件进行简单的介绍。

* ibdata1文件: innodb共享表空间文件，参数innodb_data_file_path提供配置
* ib_logfile0文件: 重做日志文件组1文件1
* ib_logfile1文件: 重做日志文件组1文件2
* ib_buffer_pool文件:
* ibtmp1文件:

二进制bin-log记录的是逻辑日志, 例如各种sql的执行呀. 重做日志记录的是物理日志, 记录的是对磁盘的修改。

## 错误日志

通过错误日志可以定位到一些问题, 性能优化, socket等.. 查看错误日志文件存放的目录

```
show variables like "log_error%";
```

## 慢查询日志


## 二进制日志



# 创建用户,并且修改默认的密码验证方式
CREATE USER 'dee'@'localhost' IDENTIFIED WITH mysql_native_password BY 'jack_dee!';
# 授权
GRANT ALL privileges ON *.* TO 'dee'@'localhost';

# 所以最好的管理策略就是创建一个用户,只给这个用户某一个db的管理权限

# 现在创建2个数据库,,创建一个用户,,只给单一权限

# mysql 开启补全提示 修改配置文件 添加 auto-rehash

# 当前有2个数据库，blog 和test1 我们创建一个用户 叫做onlytest 只准许访问test1数据库 并且只准他从本机登录

CREATE USER 'onlytest'@'localhost' IDENTIFIED WITH mysql_native_password BY 'onlytest';

# 给onlytest 授予test1数据库的权限    当然还可以限制只准许查,但是在一般的php项目里，不太需要这样搞了

GRANT ALL privileges ON test1.* TO 'onlytest'@'localhost';



# MySQL整体概览

一切的开始，先问自己一个问题：敲下 SELECT * FROM `TAB1` WHERE ID > 1000; 这样一条简单的sql,MySQL到底做了什么?

MySQL处理SQL分为下面几个步骤


# MySQL 的运维知识



# MySQL 的增删查改知识，建表删除表

CREATE TABLE `users_1` (
  `id` INT(10) UNSIGNED NOT NULL AUTO_INCREMENT,
  `name` VARCHAR(20) NOT NULL DEFAULT '',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=10000 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

# 汉字也是按照字符存的 varchar20 也能存下 那么如果是简单字符呢？
# 果然是按字符存
insert into `users`(`name`) VALUES('你好我吗');
insert into `users`(`name`) VALUES('is whathei what');
insert into `users`(`name`) VALUES('is me whataa jack');

关于or子句
and 子句和 or 子句一起使用时, and 子句的优先级是高于or 子句的

MySQL update 语句更新时一般只支持单条更新,如果要批量更新 可以使用case  when 子句


UNION 语句可以将2个或者多个表的相同字段查询出来合并成一个结果集.. 不过这个结果集默认删除了重复数据

CREATE TABLE `website` (
  `id` INT(10) UNSIGNED NOT NULL AUTO_INCREMENT,
  `name` VARCHAR(20) NOT NULL DEFAULT '',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=10000 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

insert into `website`(`name`) VALUES('an');
insert into `website`(`name`) VALUES('jk');
insert into `website`(`name`) VALUES('？!ad ');
insert into `website`(`name`) VALUES('奥yan');

CREATE TABLE `website1` (
  `id` INT(10) UNSIGNED NOT NULL AUTO_INCREMENT,
  `name` VARCHAR(20) NOT NULL DEFAULT '',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=10000 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

insert into `website1`(`name`) VALUES('mn');

联合查询，联合查询结果集成为一个新的结果集
select * from `website` UNION DISTINCT select * from `website1`;

排序查询
mysql ORDER BY 的排序规则是什么？ 按照首字母？ or 其他?

对于汉字,如果我们的表和database是utf8万国码编码的话，先使用convert函数转码成gbk比较

select distinct(name) from `website` order by CONVERT(name using gbk) asc;

对于 order by 我们一般会使用偏移量查询 limit offset 

分组查询 
select coalesce(name,'总数') as name,count(*) as times from website1 where id < 10005 group by name WITH ROLLUP;

mysql 5.7 在使用分组查询是要注意模式问题

# 客户端~ 设置group by 的模式为传统模式
[client]
init-command="set sql_mode='TRADITIONAL'"

having 子句



# MySQL 的基本数据类型
数值类型

微整型 TINYINT
小整型 SMALLINT
中整型 MEDIUMINT
整型 INT
大整型 BIGINT 
单精度浮点型 FLOAT
双精度浮点型 DOUBLE
制定的小数 DECIMAL

日期类型
DATE
DATETIME
TIMESTAMP 虽然是叫时间戳 但是存的却是  2019-08-19 15:31:28 这种数据

字符串类型
CHAR
VARCHAR 
TEXT
BLOB

# MySQL 的事务知识
# MySQL 的锁知识

MySQL使用锁是为了保证程序对数据并发处理时保持数据的一致性和完整性

这里所指的锁是面向事务的,不是线程锁;

那么INNODB具体有哪些锁呢?


表锁

行锁  - 标准的行级锁 共享锁 排他锁

间隙锁

意向锁 - 事务的更细粒度加锁

默认的隔离级别，不显示开启事务，也就是默认情况下，sql的执行会被加锁吗?


数据库事务当中，一致性非锁定读, 读取的是数据的快照, 透过undo 来实现 - 保证事务

读提交
可重复读(InnoDB默认的事务隔离级别)



# MySQL 的索引知识

# MySQL 数据的底层是怎样存储的?

他是一个索引组织表，所以不管是显示还是隐式(不声明主键)，innodb 都会有一个主键索引，然后有一棵B+树存储数据, 聚集索引的叶子节点即存储
了数据。

对主键形成的B+树来讲，因为叶子页的大小一般是计算机管理磁盘的页(4,8,16k)的整数倍，所以一个页可能会存在多行数据


# MySQL 的底层数据结构知识

mysql 索引是什么？ 索引其实是一种数据结构~ 通过这种数据结构,方便我们快速定位到结果而不是去扫描全表比较.
这里暂时只学习innodb 

二叉搜索树

就是一棵二叉树，但是其左值小于根值小于右值  其实就是二叉树的中序遍历限定树

那么平衡二叉树是什么呢？ 平衡二叉树是指在二叉搜索树当中删除和插入节点时尽量保持树形的一种策略，防止树变成线性表
一旦变成这种结构，肯定有范围查询用不上索引。

B树

B+树

B*树

红黑树

MySQL是索引组织表，表中的数据都是按照主键顺序存放.

主键索引也叫做聚集索引,主键索引的B+树叶子节点就存放了所有的数据，所以查询效率是非常的高。

辅助索引(非聚集索引)，叶子节点的索引行当中包含了一个“书签”, 这个书签存的是聚集索引的地址。

联合索引的左原则~  在数据结构里面 左侧的列是排序的，但是右侧的不是, 所以用不上索引~

但是如果是索引覆盖场景，联合索引的右字段也可以用的上索引~

索引使用原则

列独立 a = a + 1, 不要 a + 1 = b 假设a 上面有索引

左原则匹配

范围

in

group by 
 
order by

null 值

索引覆盖

小结果集驱动大结果集


针对区分度较高的字段设计索引~  对区分度不高的字段~  不建立索引可能扫描到的数据也少，然后sql 层再晒一下，建立索引意义不大。建立索引的目的是
为了快速检索到数据。


CREATE TABLE `admin` (
  `id` INT(10) UNSIGNED NOT NULL AUTO_INCREMENT,
  `name` VARCHAR(20) NOT NULL DEFAULT '',
  `age` TINYINT NOT NULL DEFAULT 1,
  `gender` CHAR(10) NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=10000 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

insert into `admin`(`name`,`age`,`gender`) VALUES('断浪','20','male');
insert into `admin`(`name`,`age`,`gender`) VALUES('乔峰','32','male');
insert into `admin`(`name`,`age`,`gender`) VALUES('阿朱','21','female');


alter table `admin` add index `name` (`name`);
alter table `admin` add index `name_time` (`name`, `create_time`);

explain select * from admin where create_time between '2019-01-01' and '2019-08-09';

alter table admin add column create_time date;
alter table admin drop index name_gender;

# MySQL 性能优化综合篇

# MySQL 分页查询优化篇


# MySQL 分表分库

分表分库，事务，连表查询怎么解决？ 单表的事务必定不可再用


# MySQL回表是什么

# MySQL EXPLAIN详细解释


# 数据库中间件 MyCAT



# MySQL在linux上的学习笔记


事务包括:

* 原子性 - redo log , 重做日志实现
* 一致性 - undo log , 
* 持久性 - redo log , 重做日志实现
* 隔离性 - 隔离性使用锁来实现的

redo 恢复提交事务修改的页操作， undo 恢复到一行记录的某一个版本。




















