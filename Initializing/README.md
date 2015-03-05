#Initializing Spark
**推广: 更快更好的翻墙神器 [红杏]( http://honx.in/i/VPZdDZnKEyd7byzB)**

---
一个Spark程序要做的第一件事就是新建一个[SparkContext](https://spark.apache.org/docs/latest/api/scala/index.html#org.apache.spark.SparkContext)对象，它将告诉Spark如何访问一个集群。为了一个`SparkContext`对象，你需要先构建一个[SparkConf](https://spark.apache.org/docs/latest/api/scala/index.html#org.apache.spark.SparkConf),它包含了你的应用的信息。

一个JVM上只可能有一个SparkContext是激活的。你在创建一个新的SparkContext之前必须`stop()`一个活跃的SparkContext。

	val conf = new SparkConf().setAppName(appName).setMaster(master)
	new SparkContext(conf)
	
这个`appName`参数是用来在集群可视化UI上显示的应用名称。`master`是一个[Spark,Mesos or YARN cluster URL](https://spark.apache.org/docs/latest/submitting-applications.html#master-urls),或者是一个特殊的"local"字符串来运行在本地模式。实践里，当在集群下运行，你是不想去在程序里硬编码`master`,而是[使用spark-submit启动程序](https://spark.apache.org/docs/latest/submitting-applications.html),并获取(master)。然而，对于本地测试或单元测试，你可以传递"local"来运行Spark。