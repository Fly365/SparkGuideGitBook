#Passing Functions to Spark
Spark的API很大程度上依赖在驱动程序上传递函数去集群上执行。有两种推荐的方式：

- [匿名函数语法](http://docs.scala-lang.org/tutorials/tour/anonymous-function-syntax.html),这在短代码片可用到
- 一个单例对象的静态方法。比如，你可以定义对象`MyFuctions`,并传递MyFunctions.func1，就像下面这样:

```
object MyFunctions {
  def func1(s: String): String = { ... }
}

myRdd.map(MyFunctions.func1)

```

注意到，这个也可以传递一个类实例（与单例相对）的方法的引用，这个要求传递这个对象同时包含类和方法。如：

```
class MyClass {
  def func1(s: String): String = { ... }
  def doStuff(rdd: RDD[String]): RDD[String] = { rdd.map(func1) }
}
```
因此，如果我们新建一个`new MyClass`并调用`doStuff`，里面的map引用了在`MyClass`实例的func1方法。所以整个对象需要被发送给集群。这和写`rdd.map(x => this.func1(x))`是相似的。

同样的道理，访问外部对象的字段会引用整个对象：

```
class MyClass {
  val field = "Hello"
  def doStuff(rdd: RDD[String]): RDD[String] = { rdd.map(x => field + x) }
}
```

这等价于写 `rdd.map(x => this.field + x)`，将引用`this`的全部。为了避免这种情况，最简单的方法是复制一个`field`到局部变量，而不是直接外部访问。

```
def doStuff(rdd: RDD[String]): RDD[String] = {
  val field_ = this.field
  rdd.map(x => field_ + x)
}
```



	
