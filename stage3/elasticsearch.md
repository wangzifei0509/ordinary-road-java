## 分布式搜索几个组件对比，为啥适用ES
- solr
- ES
- Lunec


## elasticsearch
ES作为传统关系型数据库的补充，提供全文检索，相关度排名、海量数据近实时处理。
### ES特点
ES劣势
- 不支持事务
- 不支持关联查询  

ES优势
- 全文检索
- 数据分析
- 分布式
- 数据高可用 集群高可用
- 海量数据近实时处理
### elasticsearch与关系型数据库的类比
| 关系型数据库（比如Mysql）|	非关系型数据库（Elasticsearch）| 
|------|------|
|数据库Database	|索引Index|
|表Table|	类型Type|
|数据行Row|	文档Document|
|数据列Column|	字段Field|
|约束 Schema	|映射Mapping|
### ES字段类型
- keyword 默认会做分字的索引
- text 默认会做分词的索引 
- string，date，integer ...

### ES核心概念
1. 倒排索引
   使用空间换取时间的理念，在文档插入的时候就为必要的字段分字或者分词做好索引，由于是根据属性值确定记录的位置，所以是倒排索引
2. 分片 shard
   一个节点上不能保存海量的数据，一个index的数据保存在一个节点上也不安全，所以出现了分片，默认一个index是5个分片，5个副本。
3. 副本 replica
   为了保证节点宕机后，数据还在，副本分片和主分片不会放在一个节点上。
### ES应用场景
- 全文检索
- 根据id查询
- 有条件的查询


ES的配置中有一个clustername，如果该字段相同，那么ES就认为这几个节点是同一个集群。

