#Parallelized Collections
在你的驱动程序存在的集合（一个Scala Seq）上调用`SparkContext`'s `parallelize`方法，可以创建Parallelized集合。该集合的元素可被复制组成一个能被并行操作的分布式数据集。举个例子，下面是如何创建一个包含数字1到5的并行化集合：

	val data = Array(1, 2, 3, 4, 5)
	val distData = sc.parallelize(data) 
	
一旦被创建，这个分布式数据集（distData）就能被并行地操作。比如，我们可能调用`distData.reduce((a, b) => a + b)` 去累加一个数组的元素。我们将在后面讲解分布式数据集上的操作。

对于并行集合一个重要的参数是该数据集分割成多少部分。Spark将为集群的每个分区运行一个任务。一般地你需要在你的集群上的每个CPU使用2-4个分区。Spark通常试着去根据你的集群自动设置这个分区数。但是，你可以手动地设置，通过给`parallelize`传递第二个参数(e.g. `sc.parallelize(data, 10)`)。注意：代码的有些地方为了保障向后兼容，使用术语分片(slices)(分区的同义词 patitions)。

