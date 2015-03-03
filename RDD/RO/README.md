#RDD Operations
RDDs支持两种类型的操作：`transformations`,即从一个已经存在的数据集创建一个新的；`actions`,即在数据集上执行运算后返回一个值给驱动程序。比如，`map`是一个`transformation`,它通过一个方法传递每个集合元素并返回一个新的RDD来表示结果。另一方面，`reduce`是一个`action`,它使用某个方法聚集RDD上的所有元素并向驱动程序返回一个最终的结果(但是有一个并行的`reduceByKey`返回一个分布式数据集).

所有Spark的tranfomations都是lazy的，就是说它们不会立刻执行结果。它们会记住施加在某个基础数据集的所有tranfomation。这些tranformation仅当一个action要求向驱动程序返回结果时才会被计算。这个设计使得Spark执行得更有效率。比如说，我们可以意识到：一个通过map创建的数据集将被用在reduce，且仅返回reduce的结果给驱动程序，而不是更大的mapped数据集。

默认情况下，每个transformed RDD 在每次执行action时都会被计算。然而，你可能也要使用`persist`（或`cache`）方法在内存持久化一个RDD，这种情况下，Spark将在集群保存这些元素，以便下次你更快地查询。同时，也支持在磁盘持久化RDDs，或者在多个节点复制。