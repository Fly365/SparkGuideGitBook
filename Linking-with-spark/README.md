#Linking with Spark
**推广: 更快更好的翻墙神器 [红杏]( http://honx.in/i/VPZdDZnKEyd7byzB)**

---
Spark 1.2.1 使用的是 Scala2.10。 为了使用Scala写程序，你应该使用一个兼容的Scala版本（e.g.2.10.x）。

为了写一个Spark程序，你需要添加Maven依赖。Spark可在Maven的中心仓库得到：

	groupId = org.apache.spark
	artifactId = spark-core_2.10
	version = 1.2.1

另外，如果你需要访问HDFS集群，你需要添加针对你的HDFS版本的`hadoop-client`的依赖。一些常见的HDFS版本的标记在[third party distributions](https://spark.apache.org/docs/latest/hadoop-third-party-distributions.html)列出了。

	groupId = org.apache.hadoop
	artifactId = hadoop-client
	version = <your-hdfs-version>
	
最后，你需要引入一些（必要的）Spark类和隐式转化到你的应用。加入下面的代码：

	import org.apache.spark.SparkContext
	import org.apache.spark.SparkContext._
	import org.apache.spark.SparkConf
	