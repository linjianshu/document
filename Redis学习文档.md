### Redis学习文档

nosql讲解

阿里巴巴架构演进

nosql数据模型

nosql四大分类

cap

base

redis入门

redis安装

五大基本数据类型

string

list

set

hash

zset

三种特殊数据类型

geo

hyperloglog

bitmap

Redis配置详解

redis持久化

rdb

aof

redis事务操作

redis实现订阅发布

redis主从复制

redis哨兵模式

缓存穿透及解决方案

缓存击穿及解决方案

缓存雪崩及解决方案

基础api之jedis详解

springboot继承redis操作

redis的实践分析



nosql概述

大数据时代，一般的数据库无法进行分析处理了！

springboot+springcloud

1.单机mysql年代

app=>dal=>mysql

90年代静态网页html 服务器没有太大的压力

1.数据量如果太大，一台机器放不下了

2.数据的索引 300万条就一定要建立索引，那么一个机器的内存放不下

3.访问量，读写混合，一个服务器受不了



2.Memcached（缓存）mysql+垂直拆分（读写分离）

  网站80%都在读，如果每次去查询数据库的话就十分的麻烦！所以说我们希望减轻数据的压力，我们可以使用缓存来保证效率

![image-20200923185840123](E:\林健树\typora\image-20200923185840123.png)

发展过程：优化数据结构和索引===>文件缓存（IO）===>memchched(当时最热门的技术)===>

3.分库分表+水平拆分+mysql集群

![image-20200923190414174](E:\林健树\typora\image-20200923190414174.png)

本质：数据库（读写）

早些年mysiam：表锁（影响效率），高并发下出现严重的锁问题

早些年innodb：行锁，慢慢的就开始使用分库分表来解决写的压力！mysql在那个年代推出了表分区，这个并没有多少公司使用！

mysql的集群，很好的满足了那个年代的所有需求！

4.如今最近的年代

技术爆炸：

2000-2010：十年间，变化太快了（热榜、音乐）

mysql等关系型数据库就不够用了！数据量很多，变化很快！

mysql有的使用它来存储一些比较大的文件、播客、图片！数据库表很大，效率就很低了

如果有一种数据库来专门处理这种数据，mysql的压力就会变得十分小，（研究如何处理这些问题）大数据的io压力下，表几乎没法更改，

> 目前一个基本互联网项目！

 

![image-20200923191743309](E:\林健树\typora\image-20200923191743309.png)

> 为什么要用nosql

用户的个人信息，社交温昂罗，地理位置，用户自己产生的数据，用户日志等等爆发式增长！

这时候我们就需要使用nosql数据库的，nosql可以很好的处理以上情况

> 什么是nosql

nosql = not only sql(不仅仅是sql)

关系型数据库：表格，行，列（POI）

泛指非关系型数据库的， 随着web2.0互联网的诞生，传统的关系型数据库很难对付web2.0时代！尤其是超大规模的高并发的社区！暴露出来很多难以克服的问题，nosql在当今大数据环境下发展的十分迅速，redis是发展最快的，而且是我们当下必须掌握的一个技术！

很多的数据类型：个人信息，社交网络，地理位置，流媒体，这些数据类型的存储不需要一个固定的格式！不需要多余的操作就可以横向扩展的，Map<String , Object>使用键值对来控制！

Get Set

> nosql特点

1.方便扩展（数据之间没有关系，很好扩展）

解耦

2.大数据量高性能（Redis 一秒写80000次，读取110000次，nosql的缓存记录级，是一种细粒度的缓存，性能会比较高！）

3.数据类型是多样型！（不需要事先设计数据库！随取随用！如果数据量十分大的表，很多人就无法设计了！）

4.传统的rdbms 和nosql的区别

```java
传统的rdbms
-结构化组织
-sql
-数据和关系都存在单独的表中
-操作操作，数据定义语言
-严格的一致性
-基础的事务
-....
```



```java
nosql
-不仅仅是数据
-没有固定的查询语言
-键值对存储，列存储，文档存储，图形数据库（社交关系）
-最终一致性
-CAP定理 和 BASE（异地多活！） 初级架构师
-高性能，高可用，高可扩
-....
```



> 了解：3V+3高

大数据时代的3V：主要是描述问题的

1.海量volume

2.多样variety

3.实时velocity

大数据时代的3高：主要是对程序的要求

1.高并发

2.高可拓（随时水平拆分，机器不够了，可以扩展机器来解决）

3.高性能（保证用户体验和性能）



真正在公司中的实践一定是：nosql+RDBMS一起使用才是最强的，阿里巴巴的架构演进

技术没有高低之分，就看你如何使用



> 阿里巴巴的演进分析

这么多东西难道都是在一个数据库中的吗？

![image-20200923195311367](E:\林健树\typora\image-20200923195311367.png)

敏捷开发、极限编程

开源才牛

如果你未来想当一个架构是：没有什么是加一层解决不了的

![image-20200923200304616](E:\林健树\typora\image-20200923200304616.png)

```java
# 1.商品基本信息
名称、价格、商家信息；
关系型数据库就可以解决了！mysql /oracle(淘宝早年就去IOE!--王坚)
淘宝内部的mysql 不是大家用的mysql
#2.商品的描述、评论（文字比较多）
文档型数据库中，mongodb
#3.图片
分布式文件系统 FastDFS
 -淘宝自己的TFS
 —google自己的GFS
 -Hadoop HDFS
 -阿里云的 oss
 #4.商品的关键字（搜索）
 -搜索引擎 solr  elasticsearch
 -iseacher  多隆 
 所有牛逼的人都有一段苦逼的岁月
 #5.商品热门的波段信息
 -内存数据库
 -redis tair、memarche
 #6.商品的交易，外部的支付接口
 -三方应用
```

要知道，一个简单的网页背后的技术一定不是大家想的那么简单

大型互联网应用问题：

- 数据类型太多了
- 数据源繁多，经常重构
-  数据要改造，大面积改造

![image-20200923202347841](E:\林健树\typora\image-20200923202347841.png)

![image-20200923202441215](E:\林健树\typora\image-20200923202441215.png)

![image-20200923202455222](E:\林健树\typora\image-20200923202455222.png)

以上都是nosql入门概述



#### nosql的四大分类

KV键值对：

- 新浪：redis
- 美团：redis+tair
- 阿里、百度：redis+tair+meecache

文档型数据库（Bson格式和json一样）：

- MongoDB（一般必须掌握）
  - MongoDB是一个基于分布式文件存储的数据库，C++编写的
  - 主要用来处理大量的文档
  - MongoDB是一个介于关系型数据库和非关系型数据库中中间的产品，MongoDB是非关系型数据库中功能最丰富的，最像关系型数据库的！
- conthDB

列存储数据库

- HBase
- 分布式文件系统

图形关系数据库

![image-20200923203416066](E:\林健树\typora\image-20200923203416066.png)

- 他不是存图形，放的是关系，比如：朋友圈社交网络，广告推荐！
- neo4j，infogrid

> 四者对比

![image-20200923203555105](E:\林健树\typora\image-20200923203555105.png)



redis入门

概述

> redis是什么

remote dictionary server 远程字典服务

是一个开源的使用ANSI [C语言](https://baike.baidu.com/item/C语言)编写、支持网络、可基于内存亦可持久化的日志型、Key-Value[数据库](https://baike.baidu.com/item/数据库/103728)，并提供多种语言的API。

免费和开源！是当下最热门的nosql技术之一，也被人们称之为结构化数据库

> redis能干嘛

redis会周期性的把更新的数据写入磁盘或者把修改操作写入追加的记录文件，并且在此基础上实现了master-slave(主从)同步。

![image-20200924092136203](E:\林健树\typora\image-20200924092136203.png)

1.内存存储、持久化，内存中是断电即失，所以说持久化很重要（rdb、aof）

2.效率高，可以用户高速缓存

3.发布订阅系统

4.地图信息分析

5.计时器、计数器（浏览量！）

6....

> 特性

1.多样的数据类型

2.持久化

3.集群

4.事务

....

> 学习中需要用到的东西

1.公众号

2.redis.io

3.windows在github上下载（停更很久了）

redis推荐都是在linux服务器上搭建的，我们是基于linux学习



#### windows下安装

1.下载安装包

2.下载完毕得到压缩包

3.解压

![image-20200924095526656](E:\林健树\typora\image-20200924095526656.png)

4.开启redis，双击运行服务

![image-20200924095553184](E:\林健树\typora\image-20200924095553184.png)

默认端口号6379

5.使用redis客户端来连接redis

![image-20200924095651464](E:\林健树\typora\image-20200924095651464.png)

![image-20200924095841127](E:\林健树\typora\image-20200924095841127.png)

记住一句话，window下使用确实简单，但是redis推荐我们使用linux去开发使用

![image-20200924100331170](E:\林健树\typora\image-20200924100331170.png)



测试性能

redis-benchmark是一个压力测试工具

官方自带的性能测试工具！

![image-20200924101324907](E:\林健树\typora\image-20200924101324907.png)

100000并发，50台客户端并发，每次写入3个字节，只有一台服务器来处理这些请求，所有请求在2毫秒内处理完成



#### 基础知识

redis默认有16个数据库

默认使用第0个，可以切换数据库

```bash
127.0.0.1:6379> select 3	#切换数据库
OK
127.0.0.1:6379[3]> dbsize	#查看大小
(integer) 0
```

![image-20200924102052855](E:\林健树\typora\image-20200924102052855.png)

![image-20200924102123448](E:\林健树\typora\image-20200924102123448.png)

查看当前数据库中所有的key

![image-20200924102338783](E:\林健树\typora\image-20200924102338783.png)

删除当前数据库中`flush`

![image-20200924102622792](E:\林健树\typora\image-20200924102622792.png)

清空全部的数据库`flushall`

思考：为什么redis端口号是6379

> redis是单线程的

明白redis是很快的，官方表示，redis是基于内存操作的，cpu不是redis性能瓶颈，redis的瓶颈是根据机器的内存和网络带宽，既然可以使用单线程来实现，就是用单线程了，所以就使用了单线程了！

redis为什么单线程还这么快？

redis是c语言写的，官方提供的数据为100000+的QPS，这个不比同样是使用了key-value的memecache差

**redis为什么单线程还这么快**

1.高性能服务器一定是多线程的？？

2.多线程（CPU上下文切换）一定是单线程效率高？？

cpu/memory/硬盘速度要有所了解！

核心：redis是将所有的数据全部放在内存中的，所以说使用单线程去操作效率就是最高的，多线程（CPU上下文会切换：耗时的操作！！！！），对于内存系统来说，如果没有上下文切换效率就是最高的，多次读写都在一个cpu上的，所以在内存情况下，这个就是最佳的方案！

### 五大数据类型

 Redis 是一个开源（BSD许可）的，内存中的数据结构存储系统，它可以用作数据库、缓存和消息中间件. 它支持多种类型的数据结构，如 [字符串（strings）](http://www.redis.cn/topics/data-types-intro.html#strings)， [散列（hashes）](http://www.redis.cn/topics/data-types-intro.html#hashes)， [列表（lists）](http://www.redis.cn/topics/data-types-intro.html#lists)， [集合（sets）](http://www.redis.cn/topics/data-types-intro.html#sets)， [有序集合（sorted sets）](http://www.redis.cn/topics/data-types-intro.html#sorted-sets) 与范围查询， [bitmaps](http://www.redis.cn/topics/data-types-intro.html#bitmaps)， [hyperloglogs](http://www.redis.cn/topics/data-types-intro.html#hyperloglogs) 和 [地理空间（geospatial）](http://www.redis.cn/commands/geoadd.html) 索引半径查询. Redis 内置了 [复制（replication）](http://www.redis.cn/topics/replication.html)， [LUA脚本（Lua scripting）](http://www.redis.cn/commands/eval.html)， [LRU驱动事件（LRU eviction）](http://www.redis.cn/topics/lru-cache.html)， [事务（transactions）](http://www.redis.cn/topics/transactions.html) 和不同级别的 [磁盘持久化（persistence）](http://www.redis.cn/topics/persistence.html)， 并通过 [Redis哨兵（Sentinel）](http://www.redis.cn/topics/sentinel.html) 和自动 [分区（Cluster）](http://www.redis.cn/topics/cluster-tutorial.html)提供高可用性（high availability）.



> 讲解的所有命令，后面使用springboot、jedis，所有的方法都是这些命令
>
> 单点登陆

#### redis-key

```bash
keys * 查看所以的key
exists name 判断当前的key是否存在
move name 移除当前的key
expire name 10 设置key的过期时间 单位是秒哦
ttl 查看当前key的剩余时间
type name 查看当前key的类型
```

![image-20200924104300213](E:\林健树\typora\image-20200924104300213.png)

![image-20200924104451001](E:\林健树\typora\image-20200924104451001.png)

![image-20200924104806660](E:\林健树\typora\image-20200924104806660.png)



![image-20200924105127099](E:\林健树\typora\image-20200924105127099.png)

#### string（字符串）

90%的java程序员使用的都是redis的string类型

![image-20200924105632891](E:\林健树\typora\image-20200924105632891.png)

```
append 追加字符串 ， 如果key不存在 ， 就相当于set key value
exists 判断某个key是否存在
strlen 获取字符串的长度
```

![image-20200924110407868](E:\林健树\typora\image-20200924110407868.png)

```bush
incr key 自增命令，自增1
decr key 自减命令，自减1
incrby key increment 自增多少步长
decrby key decrement 自减多少步长
```

![image-20200924110748593](E:\林健树\typora\image-20200924110748593.png)

```bush
范围
getrange key start end
其实就是截取字符串
从0开始
如果是0到-1 就是截取全部的字符串

替换呢？
setrange key offset value 替换 key 从哪里开始算起，替换多少个字符

setex（set with expire)   #设置过期时间
setnx(set if not exist)  #不存在设置

```

![image-20200924111131931](E:\林健树\typora\image-20200924111131931.png)

```bush
setex key time value 设置过期时间
ttl key 查看多久过期
setnx key value 设置原本不存在的key的value值
返回值是0代表没有成功 1代表成功
```



![image-20200924111716363](E:\林健树\typora\image-20200924111716363.png)

```bush
mset 同时设置多个值 
mget 同时获取多个值
msetnx 是一个原子性的操作，要么一起成功，要么一起失败
```



![image-20200924112237809](E:\林健树\typora\image-20200924112237809.png)

```bush
#对象
set user1:1 {name:zhangsan,age:3}
#设置user:1对象 值为json字符串来保存一个对象
#这里的key是一个巧妙的设置：user：{id}：{filed}，如此设计在redis中是完全ok的
```

![image-20200924112908580](E:\林健树\typora\image-20200924112908580.png)

![image-20200924113631933](E:\林健树\typora\image-20200924113631933.png)

```bush
getset key value 
没有就设置
设置完了就可以再改
```

![image-20200924150037955](E:\林健树\typora\image-20200924150037955.png)

![image-20200924150059352](E:\林健树\typora\image-20200924150059352.png)

![image-20200924150112188](E:\林健树\typora\image-20200924150112188.png)



string类似的使用场景：value除了是我们的字符串还可以是我们的数字

> 

- 计数器
- 统计多单位数量 例如 uid:55646541:follow 0
- 粉丝数
- 对象缓存存储

#### list

在redis里，我们可以把list玩成一个栈、队列、阻塞队列！

所有的list命令都是以L开头的

```bush
lpush 将一个值或多个值，插入到列表头部（左）
rpush 将一个值或多个值，插入到列表尾部（右）
lrange key start end 获取值

```

![image-20200924151313766](E:\林健树\typora\image-20200924151313766.png)

```bush
lpop 移除list的第一个元素
rpop 移除list的最后一个元素

```

![image-20200924151853384](E:\林健树\typora\image-20200924151853384.png)

```bush
lindex key index 通过下标获取某一个值
```

![image-20200924152048330](E:\林健树\typora\image-20200924152048330.png)

```bush
llen list的长度
```

![image-20200924152237266](E:\林健树\typora\image-20200924152237266.png)

```bush
移除指定的值！
取消关注 uid
lrem key count value 移除特定个数的指定值
```

![image-20200924152956569](E:\林健树\typora\image-20200924152956569.png)

```bush
trim 修剪
ltrim 截断list集合并获取特定下标的集合
ltrim key start end 
```

![image-20200924153243035](E:\林健树\typora\image-20200924153243035.png)

```bush
rpoplpush
移除列表右边最后一个元素并且将其加入到一个新的列表中
rpoplpush source destination
```

![image-20200924153737788](E:\林健树\typora\image-20200924153737788.png)

```bush
lset key index value 将列表中指定下标的值替换为另外一个值，更新操作
如果不存在指定下标，就会报错
```

![image-20200924154630068](E:\林健树\typora\image-20200924154630068.png)

list中多用lrrange、lpush、lpop而非lset

```bush
linsert key before/after 特定的value 要插入的value
将某一个具体的value插入到列表中某个特定元素的前面或者后面
```

![image-20200924155744795](E:\林健树\typora\image-20200924155744795.png)

> 小结

- 他实际上是一个链表，before node after left right 都可以插入值
- 如果key不存在，创建新的链表
- 如果key存在，新增内容
- 如果移除了所有的值，空链表，也代表不存在
- 在两边插入或者改动值，效率最高！中间元素，相对来说效率会低一点！

消息排队！lpush rpop（消息队列） lpush lpop（栈） 

#### set（集合）

set中的值不能重复

```bush
set通常都是以s开头的
sadd  key member 向集合中添加元素
sismember key member 判断某元素是否在指定的集合中
smembers key  查看指定集合的所有元素
scard key 查看指定集合的长度
```

![image-20200924162841343](E:\林健树\typora\image-20200924162841343.png)

```bush
srem (s remove缩写) key value 删除指定集合里的指定元素
```

![image-20200924163026477](E:\林健树\typora\image-20200924163026477.png)

```bush
set无需不重复集合，可以实现抽随机
srandmember key 数量  随机抽取指定数量的元素从某指定集合中
```

![image-20200924163406035](E:\林健树\typora\image-20200924163406035.png)

```bush
删除指定的key， 随机删除指定的key0
spop key count 随机移除指定集合内指定数量的元素

```

![image-20200924163558641](E:\林健树\typora\image-20200924163558641.png)

```bush
将一个指定的集合中的指定元素移除至另一个指定集合中
smove source destination value 
```

![image-20200924163918565](E:\林健树\typora\image-20200924163918565.png)

微博、B站、共同关注（交集）

```bush
差集
sdiff(set different) sdiff key1 key2 与 sdiff key2 key1不同，参考系不一样
sunion key1 key2 
sinter key1 key2
```

![image-20200924164627415](E:\林健树\typora\image-20200924164627415.png)

微博，A用户将所有关注的人，放在一个set集合中，将他的粉丝也放在一个集合中，

共同关注：A用户和B用户的共同关注，二度好友，推荐好友，六度分割理论

#### hash（哈希）

想象成map集合，key-map集合， key -<key,value>集合，只是这个值是一个map集合，其实本质和string类型没有太大区别，还是一个简单的key-value

```bush
hset key field value 设置值
hget key field 		获取值
hmset key field1 value1 field2 value2 批量设置值
hget key field1 field2 批量设置值
hgetall key 获取所有的值
```

![image-20200924170715011](E:\林健树\typora\image-20200924170715011.png)

set myhash field kuansheng

所有的hash都是以H开头滴哈宝贝们



zset

### 三种特殊数据类型

geospatial

hyperloglog

bitmaps

