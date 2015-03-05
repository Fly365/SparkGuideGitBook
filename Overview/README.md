#Overview
**推广: 更快更好的翻墙神器 [红杏]( http://honx.in/i/VPZdDZnKEyd7byzB)**

---
在一个高的层面上看，每一个Saprk应用都包含了驱动程序，来运行`main`方法和在集群上执行各种`parallel operations`。Spark提供的主要抽象是 `resilient distributed dataset (RDD)`(分布式弹性数据集)，这是在各个能够并行操作的集群节点间划分的数据集合。RDDs可以使用Hadoop文件系统里面文件构造（或其他Hadoop支持的文件系统），或在驱动程序里已经存在的Scala集合，并转化它。用户可能也需要去要求Spark去在内存里持久化RDD，来使得在并行操作之间更有效的复用。最后，RDDs 能够自动从失败到节点恢复。


Spark的第二个抽象是能在并行操作使用的`shared variables`(共享变量)。默认情况下，当Spark在不同节点并行地执行的一个方法是任务集合时，它能移动方法里面使用的变量的副本到各个任务。有时候，一个变量需要在不同任务间共享，有时候需要在任务和启动程序之间共享。Spark提供了两种类型的共享变量：`broadcast variables`（广播变量）,即用于在所有节点内存缓存一个值；`accumulators`(累加器)，即只能执行“加”的变量，比如计数器或求和等。

本教程最易配合Spark的交互式脚本来学习，不管是对于scala语言的`bin/spark-shell`或对于python的`bin/pyspark`。