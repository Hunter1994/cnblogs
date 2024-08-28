<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">一，泛型的优势</span></p>
<p>1，源代码保护<br />使用泛型算法的开发人员不需要访问算法的源代码。然而，使用c++模板的泛型技术时，算法的源代码必须提供给准备使用算法的用户<br />2，类型安全<br />将泛型算法应用于一个具体的类型时，编译器和CLR能理解开发人员的意图，并保证只有与指定数据类型兼容的对象才能用于算法。试图使用不兼容的类型的对象会造成编译时错误，或在运行时抛出异常。<br />3，更清晰的代码<br />由于编译器强制类型安全性，所以减少了源代码中必须进行的强制类型转换次数，使代码更容易编写和维护。<br />4，更佳的性能<br />将泛型算法应用于一个具体的类型，避免了值类型存在装箱拆箱的操作</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff; font-size: 18pt;">二、开放类型和封闭类型</span></p>
<p>1，具有泛型类参数的类型称为开放类型，CLR禁止构造开放类型的任何实例。<br />2，代码引用泛型类型时可指定一组泛型类型实参。为所有类型参数都传递了实际的数据类型，类型就称封闭类型。CLR允许构造封闭类型的实例</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('d5267b14-5820-42d3-8c04-d7a14b0bd469')"><img id="code_img_closed_d5267b14-5820-42d3-8c04-d7a14b0bd469" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_d5267b14-5820-42d3-8c04-d7a14b0bd469" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('d5267b14-5820-42d3-8c04-d7a14b0bd469',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_d5267b14-5820-42d3-8c04-d7a14b0bd469" class="cnblogs_code_hide">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">实例开放类型（失败）</span>
Type t = <span style="color: #0000ff;">typeof</span> (Dictionary&lt;,&gt;<span style="color: #000000;">);
Activator.CreateInstance(t);

</span><span style="color: #008000;">//</span><span style="color: #008000;">实例封闭类型（成功）</span>
Type t2 = <span style="color: #0000ff;">typeof</span>(Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">string</span>&gt;<span style="color: #000000;">);
Activator.CreateInstance(t);


</span><span style="color: #008000;">//</span><span style="color: #008000;">Dictionary：类型名
</span><span style="color: #008000;">//</span><span style="color: #008000;">2：类型有2个元数
</span><span style="color: #008000;">//</span><span style="color: #008000;">TKey,TValue：要求为TKey,TValue2个类型参数指定具体的类型
</span><span style="color: #008000;">//</span><span style="color: #008000;">System.Collections.Generic.Dictionary'2[TKey,TValue]</span></pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">三、逆变和协变</span></p>
<p>1，不变量：意味着泛型类型参数不能改变<br />2，逆变量：意味着泛型类型参数可以从一个类更改为它的某个派生类。使用in关键字标记。逆变量泛型类型参数只能出现在输入位置，比如作为方法的参数<br />3，协变量：意味着泛型类型参数可以从一个类型改变为它的某个基类。使用out关键字标记。协变量泛型类型参数只能出现在输出位置，比如作为方法的返回类型</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">四、约束</span></p>
<p>1，主要约束<br />主要约束可以是代表非密封类的一个引用类型，两个特殊的主要类型：class和struct</p>
<p>2，次要类型<br />次要约束代表接口类型。这种约束想编译器承诺类型实参实现了接口</p>
<p>3，构造器约束<br />class a&lt;T&gt; where T:new(){}</p>
<p>4，将泛型类型变量设为默认值<br />class a&lt;T&gt; where T:new(){ T temp=default(T)}<br />如果T是引用类型，就将temp设为null；是值类型则设为0</p>