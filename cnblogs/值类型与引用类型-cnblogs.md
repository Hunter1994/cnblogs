<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">一、使用引用类型要认清一下四个事实</span></p>
<p>1，内存必须从托管堆分配</p>
<p>2，堆上分配的每个对象都有一个额外成员，这些对象必须初始化</p>
<p>3，对象中的其他字节（为字段而设）总是设为零</p>
<p>4，从托管堆分配对象时，可能强制执行一次垃圾回收</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">二、哪些是引用类型，哪些是值类型</span></p>
<p>1，任何称为&ldquo;类&rdquo;的类型都是引用类型（例如：System.Exception类，System.IO.FileStream类）</p>
<p>2，所有值类型都称为结构或枚举（例如：System.Int32结构，System.IO.FileAttributes枚举）。</p>
<p>所有值类型都必须从System.ValueType抽象类型派生</p>
<p>&nbsp;<img src="http://images2015.cnblogs.com/blog/741594/201702/741594-20170227210027860-1184259804.png" alt="" /></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">三、结构的两种实例分配方式</span></p>
<p>&nbsp;<img src="http://images2015.cnblogs.com/blog/741594/201702/741594-20170227210147157-1515477046.jpg" alt="" /></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">四，将类型声明成值类型必须满足一下条件</span></p>
<p>1，类型具有基元类型的行为。是十分简单的类型，没有成员会修改类型的任何实例字段</p>
<p>2，类型不需要从其他任何类型继承</p>
<p>3，类型也不派生出其他类型</p>
<p>4，类型的实例较小（小于16字节）</p>
<p>5，类型的实例较大（大于16字节），但不作为方法实参传递，也不从方法返回</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">五、值类型和引用类型的区别</span></p>
<p>1，值类型有两种表示形式（未装箱和已装箱）；引用类型总是处于已装箱形式</p>
<p>2，值类型从System.ValueType派生，System.ValueType重写了Equals和GetHashCode方法（由于这个默认实现存在性能问题）</p>
<p>3，值类型不能存在虚方法、抽象方法，所有方法都隐式密封（不可重写）</p>
<p>4，引用类型的变量包含堆中的对象的地址，在创建时默认初始化为null。值类型变量总是包含其基础类型的一个值，而值类型的所有成员都初始化为0</p>
<p>5，将值类型变量赋值给另一个值类型变量时，会执行逐字段的赋值。将引用类型的变量赋值给另一个引用类型的变量时只赋值内存地址</p>
<p>6，由于未装箱的值类型不在堆上分配，一旦法定义了该类型的一个实例的方法不再活动，为它们分配的存储就会释放，而不是等着进行垃圾回收</p>
<p>&nbsp;</p>