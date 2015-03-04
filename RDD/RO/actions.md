#Actions
下面的表格是Spark所支持的常见的action。查阅RDD API文档([Scala](https://spark.apache.org/docs/latest/api/scala/index.html#org.apache.spark.rdd.RDD),[Java](https://spark.apache.org/docs/latest/api/java/index.html?org/apache/spark/api/java/JavaRDD.html),[Python](https://spark.apache.org/docs/latest/api/python/pyspark.rdd.RDD-class.html))和pair RDD函数文档([Scala](https://spark.apache.org/docs/latest/api/scala/index.html#org.apache.spark.rdd.PairRDDFunctions),[Java](https://spark.apache.org/docs/latest/api/java/index.html?org/apache/spark/api/java/JavaPairRDD.html))可得到更多。

（ 内容很多，隔日再翻译）


Action      |     含义
---------   |    ---------
reduce(func)|    使用函数`func`(需要接受两个参数，返回一个值)聚集数据集上的元素。这个函数需要是可交换的和可关联的，以便在并行环境下正确执行。