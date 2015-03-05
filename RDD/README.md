#Resilient Distributed Datasets
**推广: 更快更好的翻墙神器 [红杏]( http://honx.in/i/VPZdDZnKEyd7byzB)**

---
Spark总是围绕着`resilient distributed dataset`(RDD)的概念，它是一个能并行操作的容错的元素集合。创建RDDs有两种方法：在你的驱动程序里`parallelizing`一个已经存在的集合；或者引用一个外部存储系统上的数据集，比如一个共享文件系统，HDFS，HBase，或者其他提供Hadoop输入格式的数据源。