# 数据库架构
- 关系数据
- 混合数据

- 图数据
Neo4j、ArangoDB、neo4j，arangodb，janus graph，nebula graph



## 数据
![alt text](./_res/image.png)
![IMG_256](./_res/image1.jpeg)

数据存储系统：最常见的就是分布式文件系统HDFS；如果需要使用NoSQL数据库功能，HBase是基于HDFS实现的一个分布式NoSQL数据库。

大数据ETL工具：负责把业务数据从前端搬运到后台的大数据平台，Sqoop是常见的结构化数据抽取工具；Flume和Logstach是用于抽取非结构化、半结构化数据工具。

基础层大数据引擎：所有大数据应用的底层核心引擎，主要是MapReduce和Spark。

分布式协调服务： Zookeeper，协调多个机器一起"友好"
高效工作的分布式调度工具。

分布式调度服务：任务顺序和时间（Azkaban、Oozie）

应用层大数据引擎：直接用MapReduce或Spark写程序比较困难，因此对基础层大数据引擎封装简化，提供一系列简易编程应用工具。

Pig/Hive/Spark SQL：面向SQL查询的编程工具。

Malhot：面向机器学习的分布式工具。

GraphX：面向图计算的分布式工具。

Elastic
Search：面向搜索应用的分布式工具，不依赖基础层大数据引擎，比较独立。

大数据实时处理：实时采集数据，实时分析， Spark
Streaming（大数据准实时计算）、Flink
（大数据实时计算）、CDC或者OGG（结构化数据的实时抽取）。

趋势：HDFS让位于由AWS
S3领导的对象存储。MapReduce已被Spark取代，随着时间的推移，它也减少了对Hadoop的依赖。Yarn正在被Kubernetes等技术所取代。而Hive
的查询引擎组件在性能和采用方面已经被Presto/Trino超越。

![](./_res/image2.png)

### 数据仓库hive和数据库MySQL

数据库是面向事务的设计，一般存储在线交易数据，数据仓库是面向主题设计的，存储的一般是历史数据；数据库设计是尽量避免冗余，一般采用符合范式的规则来设计，数据仓库在设计是有意引入冗余，采用反范式的方式来设计；数据库是为捕获数据而设计，数据仓库是为分析数据而设计，它的两个基本的元素是维表和事实表。

查询语言   |HQL   |SQL
-------|------|---
数据存储位置    |HDFS   |Local FS
数据格式     |用户自定      |系统决定
数据更新       |hive(0.14)后支持         |支持
索引        |无                  |有
执行   |MapReduce       |Executor
执行延迟   | 高         | 低
可扩展性  | 高         | 低
数据规模   |大        | 小
