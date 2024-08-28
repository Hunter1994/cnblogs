<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">一、实例类型</span></p>
<p>Employee e=new Employee("ConstructorParaml")<br />1，计算类型及其所有基类型（一直到System.Object）中定义的所有实例字段需要的字节数。堆上每个对象都需要一些额外成员，包括&ldquo;类型对象指针&rdquo;和&ldquo;同步块索引&rdquo;。CLR利用这些成员管理对象。额外成员的字节数要计入对象大小<br />2，从托管堆中分配类型要求的字节数，从而分配对象的内存，分配的所有字节都设为零<br />3，初始化对象的&ldquo;类型对象指针&rdquo;和&ldquo;同步块索引&rdquo;成员<br />4，调用类型的实例构造器，传递在new调用中指定的实参。大多数编译器都在构造器中自动生成代码来调用基类构造器。每个类型的构造器都负责初始化类型定义的实例字段。最终调用System.Object的构造器，该构造器什么都不做，简单的返回<br />5，new执行了所有的操作之后，返回新建对象的一个引用，保存到e变量中</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">二、类型安全</span></p>
<p>1，CLR总是知道对象的类型是什么。调用GetType方法可知道对象的确切类型<br />2，类型转换安全</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">三、使用C#的Is和As操作符来转型</span></p>
<p>1，is检查对象是否兼容于指定的类型，返回boolean<br />Object o=New Object();<br />bool b=(o is Employee);</p>
<p>2，as判断对象是否兼容于指定的类型，如果兼容，则返回该类型，否则返回null<br />Object o=New Object();<br />Employee e=o is Employee;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">四、运行时得到相互关系</span></p>
<p>序幕代码：在方法开始工作前对其进行初始化<br />尾声代码：在方法做完工作后对其进行清理</p>