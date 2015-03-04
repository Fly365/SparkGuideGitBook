#Transformations
下面的表格展示了Spark常用的transformations。查阅RDD API的文档([Scala](https://spark.apache.org/docs/latest/api/scala/index.html#org.apache.spark.rdd.RDD),[Java](https://spark.apache.org/docs/latest/api/java/index.html?org/apache/spark/api/java/JavaRDD.html),[Python](https://spark.apache.org/docs/latest/api/python/pyspark.rdd.RDD-class.html))和pair RDD 方法文档([Scala](https://spark.apache.org/docs/latest/api/scala/index.html#org.apache.spark.rdd.PairRDDFunctions),[Java](https://spark.apache.org/docs/latest/api/java/index.html?org/apache/spark/api/java/JavaPairRDD.html))可以得到更多细节。

(这里太多了，隔日再翻译)

Transformation     |   含义
-------------      |   --------------
map(func)          |   返回一个新的分布式数据集，是通过函数`func`处理每个源元素组成的
filter(func)       |   返回一个新的数据集，通过选择源元素使得 `func`返回 true的组成
flatMap(func)      |   类似Map，但每个输入项可以被映射到0到更多的输出产品（所以`func`应返回序列而不是单一的项）。
mapPartitions(func)|   类似Map,但分别返回的是每个RDD分区（块），所以`func`当运行在T类型的RDD上时，必须是类型`Iterator<T> => Iterator<U>`
