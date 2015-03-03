#External Datasets
Spark可以从任何被Hadoop支持的存储源创建分布式数据集，包括本地文件系统，HDFS，Cassandra，HBASE，[Amazon S3](http://wiki.apache.org/hadoop/AmazonS3)等等。Spark支持文本文件，[序列文件](http://hadoop.apache.org/common/docs/current/api/org/apache/hadoop/mapred/SequenceFileInputFormat.html),或任何其他Hadoop [inputFormat](http://hadoop.apache.org/docs/stable/api/org/apache/hadoop/mapred/InputFormat.html)。

文本文件的RDDs可以使用`SparkContext`的	`textFile`方法被创建。这个方法接受该文件的URL(包括本机上的路径，或是`hdfs://`,`s3n://`等URL)（作为参数），并读取各行作为集合。下面是调用的例子：

	scala> val distFile = sc.textFile("data.txt")
	distFile: RDD[String] = MappedRDD@1d4cee08
	
一旦被创建，`disFile`就可以通过集合操作变化。比如，我们可以使用`map`和`reduce`累计所有行的规模（长度）：`distFile.map(s => s.length).reduce((a, b) => a + b)`。

使用Spark读取文件时要注意：

- 如果使用了本地文件系统的路径，该文件必须在相同路径下能被其他工作节点访问。要么复制文件到工作节点，要么使用网络挂载的共享文件系统。
- 所有Spark的基于文件的输入方法，都支持运行在目录上，压缩文件，以及通配符。比如，你可以使用`textFile("/my/directory")`,`textFile("/my/directory/*.txt")`, 和`textFile("/my/directory/*.gz")`。
- `textFile`方法也可以接受一个可选的第二个参数来控制文件的分区数。默认情况下，Spark为文件的每个块创建一个分区(在HDFS里面，块大小默认是64MB)，但是你可以申请更大的分区数，但不能有更少多分区。


除了文本文件，Spark的Scala API也支持几种其他的数据格式：

- `SparkContext.wholeTextFiles`使你读取一个包含多个小文件的目录，并以(filename, content)键值对来返回每个文件。这个`textFile`不一样的是：它返回每个文件的每一行作为一个记录.
- 对于[序列文件](http://hadoop.apache.org/common/docs/current/api/org/apache/hadoop/mapred/SequenceFileInputFormat.html)，使用SparkContext的`sequenceFile[K,V]` 方法，其中K,V 是文件中的键和值的类型。这些应该是 Hadoop的[Writable](http://hadoop.apache.org/common/docs/current/api/org/apache/hadoop/io/Writable.html)的子类，像[IntWritable](http://hadoop.apache.org/common/docs/current/api/org/apache/hadoop/io/IntWritable.html)和[Text](http://hadoop.apache.org/common/docs/current/api/org/apache/hadoop/io/Text.html)。并且，Spark允许你指定少数常见Writables的原始类型。比如说，`sequenceFile[Int, String]`会自动读作IntWritables和Texts。
- 对于其他的Hadoop InputFormats，您可以使用`SparkContext.hadoopRDD`方法，这需要一个任意`JobConf`和输入格式类，key类和value类。设置这些同样的方式，你会为你的输入源Hadoop的工作。您还可以使用`SparkContext.newHadoopRDD`的基础上，“新”的MapReduce API（`org.apache.hadoop.mapreduce`）InputFormats。
- `RDD.saveAsObjectFile`和`SparkContext.objectFile`支持保存RDD以序列化的Java对象的简单的格式。虽然这是效率不高的专门格式，如Avro的，它提供了一个简单的方法来保存任何RDD。

