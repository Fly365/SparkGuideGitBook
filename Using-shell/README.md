#Using the Shell
**推广: 更快更好的翻墙神器 [红杏]( http://honx.in/i/VPZdDZnKEyd7byzB)**

---
在Spark脚本下，一个特殊的解释器下的 SparkContext已经为你创建好了，是一个叫做`sc`的变量。构建你自己的SparkContentex是不管用的。你可以使用`--master`参数来设置master, 你也可以传递通过逗号分割的`--jars`的参数来添加JARs到类加载路径。比如，在4核下运行`bin\spark-shell`:

	$ ./bin/spark-shell --master local[4]
	
或者，添加`code.jar`到类加载路径，

	$ ./bin/spark-shell --master local[4] --jars code.jar


运行`spark-shell --help`可以得到全部的可选参数。在解释器背后，`spark-shell`调用了更通用的[spark-submit 脚本](https://spark.apache.org/docs/latest/submitting-applications.html)。

