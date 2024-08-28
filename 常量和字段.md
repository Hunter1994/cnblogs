<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">1.类型的各种成员</span></p>
<table style="height: 677px; width: 803px;" border="1" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td valign="top" width="121">
<p>成员</p>
</td>
<td valign="top" width="448">
<p>说明</p>
</td>
</tr>
<tr>
<td valign="top" width="121">
<p>常量</p>
</td>
<td valign="top" width="448">
<p>指出数据值恒定不变的符号。一般设计为静态的</p>
</td>
</tr>
<tr>
<td valign="top" width="121">
<p>字段</p>
</td>
<td valign="top" width="448">
<p>①表示数据值。</p>
<p>⑤静态字段：类型状态的一部分</p>
<p>③实例字段：对象状态的一部分</p>
<p>④建议将字段设计为私有，防止类型或对象的状态被类型外部的代码破坏</p>
</td>
</tr>
<tr>
<td valign="top" width="121">
<p>实例构造器</p>
</td>
<td valign="top" width="448">
<p>将实例字段初始化</p>
</td>
</tr>
<tr>
<td valign="top" width="121">
<p>类型构造器</p>
</td>
<td valign="top" width="448">
<p>将静态字段初始化</p>
</td>
</tr>
<tr>
<td valign="top" width="121">
<p>方法</p>
</td>
<td valign="top" width="448">
<p>①方法是更改或查询类型或对象状态的函数</p>
<p>②作用于类型称为静态方法</p>
<p>③作用于对象称为实例方法</p>
</td>
</tr>
<tr>
<td valign="top" width="121">
<p>操作符重载</p>
</td>
<td valign="top" width="448">
<p>操作符重载实际是方法，定义了当操作符作用于对象时，应该如何操作该对象</p>
</td>
</tr>
<tr>
<td valign="top" width="121">
<p>转换操作符</p>
</td>
<td valign="top" width="448">
<p>定义如何隐式或显示将对象重一种类型转型为另一种类型</p>
</td>
</tr>
<tr>
<td valign="top" width="121">
<p>属性</p>
</td>
<td valign="top" width="448">
<p>①用简单的字段风格的语法设置或查询类型或对象的状态</p>
<p>②作用于类型称为静态属性</p>
<p>③作用于对象称为实例属性</p>
</td>
</tr>
<tr>
<td valign="top" width="121">
<p>事件</p>
</td>
<td valign="top" width="448">
<p>①静态事件允许类型向一个或多个静态或实例方法发送通知</p>
<p>②实例事件允许想一个或多个静态或实例方法发送通知</p>
</td>
</tr>
<tr>
<td valign="top" width="121">
<p>类型</p>
</td>
<td valign="top" width="448">
<p>类型可以定义其他嵌套类型。通常用这个方法将大的、复杂的类型分解成更小的构建单元以简化实现</p>
</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">2.类型的可见性</span></p>
<p>public：不仅对定义程序集中的所有代码可见，还对其他程序集中的代码可见<br />internal：仅对定义程序集中的代码可见<br />友元程序集：可见性为internal的类型可以指定其他程序集访问</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">3.成员的可访问性</span></p>
<table style="height: 469px; width: 905px;" border="1" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td valign="top" width="156">
<p>CLR术语</p>

</td>
<td valign="top" width="125">
<p>C#术语</p>

</td>
<td valign="top" width="287">
<p>描述</p>

</td>

</tr>
<tr>
<td valign="top" width="156">
<p>Pivate</p>

</td>
<td valign="top" width="125">
<p>private</p>

</td>
<td valign="top" width="287">
<p>当前类</p>
<p>嵌套类</p>

</td>

</tr>
<tr>
<td valign="top" width="156">
<p>Family</p>

</td>
<td valign="top" width="125">
<p>protected</p>

</td>
<td valign="top" width="287">
<p>当前类</p>
<p>嵌套类</p>
<p>任何派生类</p>

</td>

</tr>
<tr>
<td valign="top" width="156">
<p>Family and Assembly</p>

</td>
<td valign="top" width="125">
<p>不支持</p>

</td>
<td valign="top" width="287">
<p>当前类</p>
<p>嵌套类</p>
<p>派生类（同一程序集）</p>

</td>

</tr>
<tr>
<td valign="top" width="156">
<p>Assembly</p>

</td>
<td valign="top" width="125">
<p>internal</p>

</td>
<td valign="top" width="287">
<p>当前程序集</p>

</td>

</tr>
<tr>
<td valign="top" width="156">
<p>Family or Assembly</p>

</td>
<td valign="top" width="125">
<p>protected internal</p>

</td>
<td valign="top" width="287">
<p>嵌套类</p>
<p>任何派生类</p>
<p>当前程序集</p>

</td>

</tr>
<tr>
<td valign="top" width="156">
<p>Public</p>

</td>
<td valign="top" width="125">
<p>public</p>

</td>
<td valign="top" width="287">
<p>任何程序集的任何方法访问</p>

</td>

</tr>

</tbody>

</table>
<p><br /><br /></p>
<p><br />            </p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">4.静态类</span></p>
<p>static只能应用于类，不能应用于结构（值类型）<br />c#编译器对静态类型进行了如下限制<br />①静态类必须直接从基类Object派生，从其他任何基类派生都没有意义。继承只适用于对象，而你不能创建静态类的实例<br />②静态类不能实现接口，这个因为只有使用类的实例时，才可调用类的接口方法<br />③静态类只能定义静态成员（字段、方法、属性和事件），任何实例成员都会导致编译器报错<br />④静态类不能作为字段、方法参数或局部变量使用，因为他们都代表应用了实例的变量。而这是不允许的。编译器检查到会报错</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">5.c#关键字及其对组件版本控制的影响</span></p>
<table style="height: 371px; width: 788px;" border="1" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td valign="top" width="142">
<p>C#关键字</p>


</td>
<td valign="top" width="142">
<p>类型</p>


</td>
<td valign="top" width="142">
<p>方法、属性、事件</p>


</td>
<td valign="top" width="142">
<p>常量、字段</p>


</td>


</tr>
<tr>
<td valign="top" width="142">
<p>abstract</p>


</td>
<td valign="top" width="142">
<p>表示不能构造该类型的实例</p>


</td>
<td valign="top" width="142">
<p>表示为了构造派生类型的实例，派生类型必须重写并实现这个成员</p>


</td>
<td valign="top" width="142">
<p>不允许</p>


</td>


</tr>
<tr>
<td valign="top" width="142">
<p>virtual</p>


</td>
<td valign="top" width="142">
<p>不允许</p>


</td>
<td valign="top" width="142">
<p>表示这个成员可由派生类重写</p>


</td>
<td valign="top" width="142">
<p>不允许</p>


</td>


</tr>
<tr>
<td valign="top" width="142">
<p>override</p>


</td>
<td valign="top" width="142">
<p>不允许</p>


</td>
<td valign="top" width="142">
<p>表示派生类型正在重写基类型的成员</p>


</td>
<td valign="top" width="142">
<p>不允许</p>


</td>


</tr>
<tr>
<td valign="top" width="142">
<p>sealed</p>


</td>
<td valign="top" width="142">
<p>表示该类型不能用作基类型</p>


</td>
<td valign="top" width="142">
<p>表示这个成员不能被派生类型重写，只能将该关键字应用于重写虚方法的方法</p>


</td>
<td valign="top" width="142">
<p>不允许</p>


</td>


</tr>
<tr>
<td valign="top" width="142">
<p>new</p>


</td>
<td colspan="3" valign="top" width="426">
<p>应用于嵌套类型、方法、属性、事件、常量或字段时，表示该成员与基类中相似的成员无任何关系</p>


</td>


</tr>


</tbody>


</table>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">6，CLR提供两个方法调用指令</span></p>
<p><strong><span style="font-size: 18px;">call</span></strong><br />①该IL指令可调用静态方法、实例方法、虚方法<br />②call调用静态方法，必须指定方法定义类型<br />③call调用实例方法或者虚方法，必须指定引用了对象的变量<br />④call指令假定该变量不为null<br />⑤换言之，变量本身的类型指明了方法的定义类型。如果变量的类型没有定义该方法，就检查基类型来查找匹配方法<br />⑥call指令经常用于以非虚方式调用虚方法</p>
<p><strong><span style="font-size: 18px;">callvirt</span></strong><br />①该IL指令可调用实例方法和虚方法，不能调用静态方法<br />②用callvirt指令调用实例方法或虚方法，必须指定引用了对象的变量<br />③用callvirt指令调用非虚实例方法，变量的类型指明了方法的定义类型<br />④用callvirt指令调用虚实例方法，CLR调查发出调用的对象的实际类型，然后以多态的方式调用方法。为了确定类型，发出调用的变量觉不能null。换言之，编译这个调用时，JIT编译器会生成代码来验证变量的值是不是null。如果是，callvirt指令造成CLR抛出NullReferenceException异常。正式由于要进行这种额外的检查，所以callvirt指令的执行速度比call指令稍慢。<br />⑤即使callvirt指令调用的是非虚实例方法，也要执行这种null检查</p>
<p>&nbsp;</p>