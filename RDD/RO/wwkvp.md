#Working with Key-Value Pairs
尽管大多数的工作在RDDs上的Spark操作可以包含任意类型的对象，但有少数几个特殊操作的仅能使用key-value 对。最常用的一个就是分布式的"shuffle"，比如根据一个key来分组或聚集元素。

在Scala里面，这些操作会自动可在包含[2元组](http://www.scala-lang.org/api/2.10.4/index.html#scala.Tuple2)对象的RDDs里可用（语言里内建的元组，可用简单的写(a, b)来创建）只要你在你的程序里引入了 `org.apache.spark.SparkContext._`来使用Spark的隐式转化。在[PairRDDFunctions](https://spark.apache.org/docs/latest/api/scala/index.html#org.apache.spark.rdd.PairRDDFunctions)可得到key-value对的操作，如果你引入了（隐式）转化，它会自动封装RDD的元组。


比如，下面的代码使用了`reduceByKey`操作在key-value对上来统计一个文件里每行文本出现的次数：

	val lines = sc.textFile("data.txt")
	val pairs = lines.map(s => (s, 1))
	val counts = pairs.reduceByKey((a, b) => a + b)
	

我们也可以用`counts.sortByKey（）`，例如，向对按字母顺序排序，最后`counts.collect（）`，使它们作为对象的数组返回到驱动程序。


**注意 ：** 在我们在key-value对操作里使用自定义的对象，你必须确保一个自定义的 `equals()`方法和匹配的自定义`hashCode()`方法协同。参见 [Object.hashCode() 文档](http://docs.oracle.com/javase/7/docs/api/java/lang/Object.html#hashCode())可得到更全面的说明。