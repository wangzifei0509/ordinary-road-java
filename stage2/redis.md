## redis 分布式缓存中间件 [redis文档](http://www.redisdoc.com)
### redis特点
- NoSql数据库
- 分布式缓存中间件
- key-value形式存储
- 提供海量数据存储和访问
- 数据存储在内存中，读取更快
- 非关系型、分布式、开源、水平扩展
### 为什么选择redis而不选择Memcache
优点：丰富的数据结构、持久化、主从同步、故障转移、内存数据库
缺点：单线程、单核
redis相较于memcache，支持更丰富的数据结构，支持持久化，这两点决定了选择redis而不选择Memcache。
### redis 5种数据类型
- string
- hash 用来保存对象类，有序，加入顺序，不过只能以属性设置和查看
- list 用来保存数组类，有序，加入顺序，可以以index设置和查看
- set 与list相比，list允许成员重复，set不允许成员重复
- zset=sorted set 可以用来做排名排行榜
### redis 常用命令
### redis 使用场景
低频更改的数据可以缓存，提高查询效率，如果数据变更，更新缓存的方式：
- 数据库数据更新了之后，删除缓存，同时将新数据放入缓存
- 对时效性要求不高的，定时重置缓存
- 根据缓存内容的失效时间来更新
### redis 发布订阅功能
redis能实现类似mq的功能，但是不建议使用，专人干专事
### redis的持久化模式
- rdb
- aop
### redis的集群模式
主从模式，读写分离，一主二从
### redis的哨兵模式
为了保证redis的可用性，如果master节点挂了，那么需要哨兵监控master的状态，并选举出一个新的master。哨兵进程可以有多个。
### redis架构 
- 单点单实例
- 一主二从，读写分离，哨兵的集群模式
- 三主三从，这种架构在实际生产中最常用，因为一主二从模式依然可能有数据丢失的问题，比如在主从复制的过程中，master节点挂了，那么就会有几秒的数据丢失。











由于一主二从结构只有一个master节点来处理写操作，实质上还是单实例，应对高并发仍有可能超载，所以3主3从的集群结构应运而生。
三主三从架构详解：
总共分配了n槽点，平均分配给3个master节点，根据key值得hash结果决定放在哪个槽点中，使用一致性hash。
hash(key)%n结果为槽点的index，index从0到n-1。
redis的key建议使用 业务id:子业务id来表示
### redis缓存穿透
非法用户对不存在的结果进行访问，那么由于结果集为空，没有被缓存在redis中，这些非法请求会一直访问数据库，对数据库造成压力，从而可能造成数据库宕机。解决方法如下：
- 对空结果集进行缓存，也就是对所有可能的结果都进行缓存，不管是什么样的查询，都只能查询一次数据库，之后的查询都应该走缓存，由于非法请求高频持久时间少，那么可以将非法请求的结果缓存时间设置的比较小，比如5min。
- 布隆过滤器
百分之1的误判率，以及不能删除
### redis雪崩
如果恰巧很多key过期，同时又有很多请求访问，那么大量的请求就会访问数据库，造成数据库宕机。
- 设置key永不过期，手动去删除key
- 过期时间分散分布，比如有效期都是1h，那么这一批key的有效期可以设置50-70min之间随机。
- 多层缓存
- 采购商业redis
### redis-java-client的批量查询
- 使用mget等批量处理的接口。
- 使用pipeline方式，foreach处理，相比于第一种方式的优势是在foreach中可以使用任意的redis的操作，而速度不慢的原因是这一批操作只打开一个长链接。



