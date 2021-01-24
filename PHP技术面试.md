# PHP技术面试

会**基于面试者的简历**，问如下的一些问题：

## OOP

* 面向对象的3个特性：封装、继承、多态
* 什么是多态？
	* PHP下如何实现多态？
* 什么是接口？
* 什么是抽象类？
* 接口和抽象类的区别 ？

## 框架

> * 阅读源码是提升编程能力的最佳手段。不读阅读源码的开发者，是不合格的。
> * 在系统架构方面的设计能力
> * 是否了解设计模式

* 阅读过哪些开源框架的源码？
* 如果说阅读过，会问如何设计一个简单的**MVC框架**？
* 或者，假设由面试者来设计框架（比如laravel）的数据库处理，如何设计？

## 错误、异常和日志相关
> 面试者在编码过程中，是否思考：当代码没有按照既定逻辑运行时，该怎么处理？

* 了解错误（`Error`）和异常（`Exception`）吗？
* PHP设计中，为什么会有错误和异常这2种？
* 编码过程中是怎么处理这2种情况的？
* finally用来做什么？
* 如何收集**业务日志**？

## 语言特性
> 对PHP语言的了解，强烈建议每一位开发者都要通读[PHP手册](https://www.php.net/manual/zh/index.php)

* 魔术方法，比如析构（`__destruct`），会在什么时候调用；`__toString`能做什么？
* 语法糖，比如“`?:`”和“`??`”的区别
* cli V.S. fpm
* 方法的缺省值
* 运行超时，内存耗尽
* ArrayAccess，Traversable等接口的含义
* Traits的用法
* 是否支持多进程和多线程？
* 一些常用扩展：gd，pdo，加密等
* PHP7/8的一些新特性
* Swoole相关（异步，协程等等）

## 应用场景

* 什么是RESTful
* 如何设计一套合理、好用的RESTful API
* OAuth，JWT
* 如何保证接口的幂等性
* 超大流量下的秒杀场景，如何限流
* 如何设计前端页面的中商品列表的缓存
* 如何防止缓存击穿和雪崩
* 大数据量（1亿行+）下的搜索，有哪些实现方式
* 某个活动，总独立用户100万，高峰预计有1万QPS，大约要发出1亿张优惠券，如何设计
* 日增100万的用户表，手机号是唯一索引，且会通过手机号搜索用户，如何设计
* 扩展：日增100万的用户表，手机号和用户名均是唯一索引，且会通过手机号或者用户名搜索用户，如何设计
* 100个不同的数字分若干组组，每组数字相加不超过1000，越接近越好，如何设计？

## 数据库
> 参考：https://blog.csdn.net/ThinkWon/article/details/104778621

* 数据库范式有哪些：第一范式（1NF）、第二范式（2NF）、第三范式（3NF）、巴斯-科德范式（BCNF）、第四范式(4NF）、第五范式（5NF，又称完美范式）、DK范式和第六范式。
* 索引的知识点，比如**myisam**和**innodb**的索引的异同、前缀索引、索引数据结构
* 自增主键和uuid作为主键的区别？
* Innodb的聚簇索引设计
	1. 如果定义了主键，会使用主键作为聚簇索引
	2. 如果没有定义主键，会使用一个唯一且不为空的索引列作为聚簇索引
	3. 如果既没有主键也找不到合适的非空索引，InnoDB会自动生成一个不可见的名为ROW_ID的列名为GEN_CLUST_INDEX的聚簇索引，该列是一个6字节的自增数值，随着插入而自增
* 某张表有主键ID索引，也有某个字段（field）索引，当执行：select * from tbl_name where field = 'xxx'，时，是如何获的数据的？
* 事务的特性：ACID
* 事务的成功、失败对自增ID的影响
* 事务隔离机制，锁等问题：由低到高依次为Read uncommitted、Read committed、Repeatable read、Serializable，这四个级别可以逐个解决脏读、不可重复读、幻读这几类问题。
* 什么是脏读？幻读？不可重复读？
* 什么是死锁？怎么解决？
* 乐观锁和悲观锁分别是什么？
* in 和 exists 区别？
* varchar与char的区别？
* `mysqli`和`pdo_mysql`的相关问题
* 如何避免SQL注入
* 主从相关，比如读写不一致时如何处理
* 分库分表
* 大表数据查询，怎么优化？
* 超大分页怎么处理？

## Redis

* 几种数据结构，各自的容量分别多大，应用场景
* 实现一个简单的**分布式锁**，或者简单的**抢红包**
* 如果有电商经验，用Redis设计一个简单的**购物车**
* 如何避免大Key的情况出现
* 数据过期策略
	* `volatile-lru` -> Evict using approximated LRU among the keys with an expire set.
	* `allkeys-lru` -> Evict any key using approximated LRU.
	* `volatile-lfu` -> Evict using approximated LFU among the keys with an expire set.
	* `allkeys-lfu` -> Evict any key using approximated LFU.
	* `volatile-random` -> Remove a random key among the ones with an expire set.
	* `allkeys-random` -> Remove a random key, any key.
	* `volatile-ttl` -> Remove the key with the nearest expire time (minor TTL)
	* **`noeviction`** -> Don't evict anything, just return an error on write operations.
	* 
	* **LRU** means **Least Recently Used**
	* **LFU** means **Least Frequently Used**
* 数据持久化方式，奔溃后的数据恢复方式
* 假设有1亿个key，其中有10万个key是以前缀`neo:`开头的，如何将它们全部找出来？
* 常用的一些Redis命令

## 消息队列（RabbitMQ）

* 为什么使用消息队列：解耦、异步、削峰
* 消息队列是怎么工作的
* 交换机（Exchange）几种类型
* 几种工作模式
	* Work queues
	* Publish/Subscribe
	* Routing
	* Topics
	* Header
	* RPC
* 消息持久化
* 如何避免重复消费
* 如何防止消息丢失

## 分布式

* CAP，BASE相关概念
* 什么是一致性Hash
* 如何确保数据一致性
	* 2PC，3PC
	* Paxos，Raft
* 拜占庭将军问题
* Snowflake算法

## 安全方面

* XSS，CSRF等概念
* 如何避免重复提交数据
* 用户身份验证
* http V.S. https
* 一些安全算法

## 性能优化

* 大表查询
* 性能瓶颈的定位分析
* 常用的排序算法

## 质量控制

* 单元测试，冒烟测试
* 编码规范，[参考这里](https://github.com/zgia/manual/blob/master/PHP%E7%BC%96%E7%A0%81%E8%A7%84%E8%8C%83.md)
* 代码评审

## PSR

* 自动加载
* 事件、消息机制
* 容器

## 前端
* 访问一个链接（如：http://www.163.com/ ）时，浏览器做了哪些事情

## 其他
* 自己编译安装过PHP、MySQL、Redis等吗
* Composer
* Git

EOF.
