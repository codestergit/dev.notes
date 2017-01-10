# mongodb

## 特点
1. 无数据结构限制，没有表结构的概念 
2. 索引支持： 单建索引，多建索引，数组索引，全文索引(不支持中文)，地理位置索引
3. 方便的冗余与扩展：复制，分片


| MONGODB 特性 | 优势 |
| --- | --- |
| 事务支持  |  MongoDB 目前只支持单文档事务，需要复杂事务支持的场景暂时不适合 |
| 灵活的文档模型 | JSON 格式存储最接近真实对象模型，对开发者友好，方便快速开发迭代 |
| 高可用复制集 | 满足数据高可靠、服务高可用的需求，运维简单，故障自动切换 |
| 可扩展分片集群 | 海量数据存储，服务能力水平扩展 |
| 高性能 | mmapv1、wiredtiger、mongorocks（rocksdb）、in-memory 等多引擎支持满足各种场景需求 |
| 强大的索引支持 | 地理位置索引可用于构建 各种 O2O 应用、文本索引解决搜索的需求、TTL索引解决历史数据自动过期的需求 |
| Gridfs | 解决文件存储的需求 |
| aggregation & mapreduce | 解决数据分析场景需求，用户可以自己写查询语句或脚本，将请求都分发到 MongoDB 上完成 |


如果你还在为是否应该使用 MongoDB，不如来做几个选择题来辅助决策（

| 应用特征  |  YES / NO |
| --- | === |
| 应用不需要事务及复杂 join 支持 | 必须 Yes |
| 新应用，需求会变，数据模型无法确定，想快速迭代开发  | ？ |
| 应用需要2000-3000以上的读写QPS（更高也可以）  |  ？ |
| 应用需要TB甚至 PB 级别数据存储 | ? |
| 应用发展迅速，需要能快速水平扩展  |  ? |
| 应用要求存储的数据不丢失  |  ? |
| 应用需要99.999%高可用 | ? |
| 应用需要大量的地理位置查询、文本查询 | ？ |
如果上述有1个 Yes，可以考虑 MongoDB，2个及以上的 Yes，选择 MongoDB 绝不会后悔。

## 安装
1. 下载，编译`scons all -j cpu数`，或者下载对应的系统版本。

## 操作
```
db.collection.insert({x:1})
db.collection.find({x:1})
```

索引
_id索引、单建索引、多建索引、复合索引、过期索引、全文索引、地理位置索引。
```
db.collection.getIndexes()
db.collection.ensureIndex({x:1})
db.collection.ensureIndex({x:1},{unique:true/false})
db.collection.ensureIndex({x:-1})
db.collection.ensureIndex({x:1,y:1})
# 过期索引
db.collection.ensureIndex({time:1}, {expireAfterSeconds:30})
# 全文索引
db.collection.ensureIndex({key:"text"})
db.collection.ensureIndex({key_1:"text", key_1:"text"})
db.collection.ensureIndex({"$**":"text"})
# 查找
db.collection.ensureIndex({"$text":{$search:"aa"}})
db.collection.ensureIndex({"$text":{$search:"aa bb"}}) #或
db.collection.ensureIndex({"$text":{$search:"aa bb -cc"}}) #不包含cc
db.collection.ensureIndex({"$text":{$search:"\"aa\" \"bb\""}}) #与
# 全文索引相似度
$meta操作符：{score:{$meta:"textScore"}},与sort一起使用效果更佳
db.collection.find({$text:{$search:"aa bb"}},{score:{$meta:"textScore"}}).sort({score:{$meta:"textScore"}})

# 唯一性unique指定：
db.collection.ensureIndex({},{unique:true/false})
# 稀疏性 sparse
db.collection.ensureIndex({},{sparse:true/false})
```

# 地理位置索引
查找距离某个点一定距离内的点，查找某个区域  
2D索引：平面地理位置索引
创建方式： `db.collection.ensureIndex({"w":"2d"})`  
取值范围：经度：[-180,180] 纬度：[-90,90]
查询方式：  
1. $near查询：查询距离某个点最近的点。  
2. $geoWithin查询：查询某个形状内的点。  



