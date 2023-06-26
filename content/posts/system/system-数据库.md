---
title: 数据库选型
date: 2018-07-07
tags: [数据库]
categories: [system]
---



作者：大宽宽

在整个行业发展过程中，一些需求催生了各种各样的的优化的机会。有人抓住机会去提出新的数据模型和查询接口。比如：

- 想内存数据库，上redis
- 想高性能访问KV模型，有rocksDB
- 想制作树状结构的数据，mongo你值得拥有
- 想做图分析，有图数据库
- 想要时序数据，有influxdb和Prometheus这种列存
- 想做Data Warehouse，有GP、有大规模的并行计算引擎
- 想做高性能海量数据存储，但是访问的方式相对简单，可以上Hadoop全家桶，Spark全家桶
- 想做海量数据的KV，有HBase，Cassandra
- ……

就连SQL自己也在演进，比如各大数据库增加了对json格式的支持，MySQL还搞了个X-API，弄得像mongo一样；Postgres中一列可以是复合的类型（类似于struct），也可以是数组类型。mysql和postgres还支持全文索引（按照王垠的讲法，是不是这时候得先用一套LSM tree库玩转sstable管理，然后再攒一个lucene做分词和倒排？）

根据实际需求，从上面这些备选中，总能找到几个东西组合在一起满足需要。如果还不够用，那就按照需求定制，就像polarDB，TiDB。但我相信，绝大部分的开发场景，弄个mysql，sqlite之类的就完事了，不需要特别仔细的优化。

遇到了SQL处理不了的，有价值的问题，去解决，去优化，去建模就好。光吐槽SQL这也不行，那也不行，没有任何卵用。