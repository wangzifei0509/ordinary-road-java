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







