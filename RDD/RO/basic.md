#Basic
为了说明RDD的基本操作，考虑下面的简单程序：

```
val lines = sc.textFile("data.txt")
val lineLength = lines.map(s => s.length)
val totalLength = lineLengths.reduce((a, b) => a + b)
```

第一行从外部文件定义了一个基本RDD。这个数据集没有载入内存或者以其他方式采取行动：`lines`仅仅是一个指向这个文件的指针。第二行定义了`linesLength`,作为`map` transformation的结果。同样的，`linesLength`由于“延迟性”并没有立刻被计算。最后，我们执行reduce，这是一个action。这个时候，Spark将计算分解成多个任务在不同机器上运行，并且每个机器都运行它所在部分的map和本地reduce操作，仅返回一个值到驱动程序。

如果我们希望在随后再使用 `lineLengths`，我们可以在`reduce`之前添加:

	linesLengths.persist()
	
这样会导致`lineLengths`在第一次计算后保存到内存。

