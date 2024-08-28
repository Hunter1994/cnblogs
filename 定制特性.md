<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">1，定制特性</span></p>
<p>①C#允许用一个前缀明确指定特性要应用的目标元素</p>
<div class="cnblogs_code">
<pre>[assembly: AssemblyVersion(<span style="color: #800000;">"</span><span style="color: #800000;">1.0.0.0</span><span style="color: #800000;">"</span>)]</pre>
</div>
<p>②AttributeUsage. Inherited(特性应用于基类时，是否同时应用于派生类和重写的方法)</p>
<div class="cnblogs_code">
<pre>    [AttributeUsage(AttributeTargets.Class|AttributeTargets.Method,Inherited = <span style="color: #0000ff;">true</span><span style="color: #000000;">)]
    </span><span style="color: #0000ff;">internal</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> TastyAttribute : Attribute
    {
    }

    [Tasty,Serializable]
    </span><span style="color: #0000ff;">internal</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> BaseType
    {
        [Tasty]
        </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">virtual</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> DoSomething(){}
    }
    </span><span style="color: #008000;">//</span><span style="color: #008000;">继承父类Tasty的特性</span>
    <span style="color: #0000ff;">internal</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> DerivedType : BaseType
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;">继承Tasty的特性</span>
        <span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> DoSomething(){}
    }</span></pre>
</div>
<div class="cnblogs_code">
<pre>    <span style="color: #008000;">//</span><span style="color: #008000;">如果特性类没有显示的引用AttributeUsage，则默认AttributeUsage如下</span>
    [AttributeUsage(AttributeTargets.All,AllowMultiple = <span style="color: #0000ff;">false</span>, Inherited = <span style="color: #0000ff;">true</span>)]</pre>
</div>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">&nbsp;2，检测定制特性</span></p>
<table style="height: 318px; width: 747px;" border="1" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td valign="top" width="140">
<p>方法名称</p>
</td>
<td valign="top" width="429">
<p>说明</p>
</td>
</tr>
<tr>
<td valign="top" width="140">
<p>IsDefined</p>
</td>
<td valign="top" width="429">
<p>至少有一个指定的Attribute派生类的实例与目标关联，就会返回true。</p>
<p>这个方法的效率很高，它不会构造（反序列化）特性类的任何实例</p>
</td>
</tr>
<tr>
<td valign="top" width="140">
<p>GetCustomerAttributes</p>
</td>
<td valign="top" width="429">
<p>返回应用于目标的指定特性对象的集合。</p>
<p>每个实例都使用编译时指定的参数、字段和属性来构造（反序列化）。</p>
<p>没有指定的集合则返回空集合。</p>
</td>
</tr>
<tr>
<td valign="top" width="140">
<p>GetCustomerAttribute</p>
</td>
<td valign="top" width="429">
<p>返回应用于目标的指定特性对象的实例。</p>
<p>实例使用编译时指定的参数、字段和属性来构造（但序列化）。</p>
<p>没有指定的特性实例，则返回null。</p>
<p>目标指定了多个实例，则抛出异常</p>
</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">3，检查定制特性时不创建从Attribute派生的对象</span></p>
<p>调用Attribute的GetCustomAttribute或者GetCustomerAttribute方法时，这些方法会在内部调用特性类的构造器，而且可能调用属性的set访问器方法。可能存在安全隐患</p>
<div class="cnblogs_code">
<pre>            <span style="color: #008000;">//</span><span style="color: #008000;">在查找特性的同时禁止执行特性类中的代码</span>
            CustomAttributeData.GetCustomAttributes()</pre>
</div>
<p>&nbsp;</p>