<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">一、装箱机制：</span></p>
<p>1，在托管堆中分配内存。分配的内存量是值类型各字段所需的内存量，还要加上托管堆中所有对象都有的两个额外成员（类型对象指针和同步块索引）所需的内存量<br />2，值类型字段复制到新分配的堆内存<br />3，返回对象地址。现在该地址是对象的引用；值类型成了引用类型</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">二、拆箱机制</span></p>
<p>1，获取已装箱值类型对象中的各个字段的地址（这个过程是装箱）<br />2，将字段包含的值从堆复制到基于栈的值类型字段实例中<br />3，如果包含&ldquo;对已装箱值类型实例的引用&rdquo;的变量为null，抛出NullReferenceException异常<br />4，如果引用对象不是所需值类型的已装箱实例，抛出InvalidCastException异常</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">三、未装箱值类型比引用类型更&ldquo;轻&rdquo;，这要归结于以下两个原因</span></p>
<p>1，不在托管堆上分配<br />2，堆上的每个对象都有两个额外成员（&ldquo;类型对象指针&rdquo;和&ldquo;同步快索引&rdquo;）。</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">四、对象相等性和同一性</span></p>
<p><strong><span style="font-size: 18px;">1，对于Object的Equals方法的默认实现，他实现的实际是同一性，而不是相等性</span></strong></p>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Object
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">virtual</span> <span style="color: #0000ff;">bool</span> Equals(<span style="color: #0000ff;">object</span><span style="color: #000000;"> obj)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">如果两个引用指向同一个对象，他们肯定包含相同的值</span>
            <span style="color: #0000ff;">if</span> (<span style="color: #0000ff;">this</span> ==<span style="color: #000000;"> obj)
                </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">true</span><span style="color: #000000;">;
            </span><span style="color: #008000;">//</span><span style="color: #008000;">假定对象不包含相同的值</span>
            <span style="color: #0000ff;">return</span> <span style="color: #0000ff;">false</span><span style="color: #000000;">;
        }
    }</span></pre>
</div>
<p><strong><span style="font-size: 18px;">2，正确的实现Equals</span></strong><br />①，如果obj实参为null，就返回false，因为调用非静态Equals方法时，this所标识的当前对象显然不为null<br />②如果this和obj实参引用同一个对象，就返回true。在比较包含大量字段的对象时，这一步有助于提升性能<br />③如果this和obj实参引用不同类型的对象，就返回false<br />④针对类型定义的每个实例字段，将this对象中的值与obj对象中的值进行比较。任何字段不相等，就返回false<br />⑤调用基类的Equals方法来比较它定义的任何字段。如果基类的Equals方法返回false，就返回false；否则返回true</p>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Object
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">virtual</span> <span style="color: #0000ff;">bool</span> Equals(<span style="color: #0000ff;">object</span><span style="color: #000000;"> obj)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">要比较的对象不能为null</span>
            <span style="color: #0000ff;">if</span> (obj == <span style="color: #0000ff;">null</span>) <span style="color: #0000ff;">return</span> <span style="color: #0000ff;">false</span><span style="color: #000000;">;

            </span><span style="color: #008000;">//</span><span style="color: #008000;">如果对象属于不同的类型，则肯定不相等</span>
            <span style="color: #0000ff;">if</span> (GetType() != obj.GetType()) <span style="color: #0000ff;">return</span> <span style="color: #0000ff;">false</span><span style="color: #000000;">;
            

            </span><span style="color: #008000;">//</span><span style="color: #008000;">如果对象属于相同的类型，那么在它们所有字段都匹配的前提下返回true
            </span><span style="color: #008000;">//</span><span style="color: #008000;">由于System.Object没有定义任何字段，所以不用比较</span>
            <span style="color: #0000ff;">return</span> <span style="color: #0000ff;">true</span><span style="color: #000000;">;
        }
    }</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">比较对象的同一性</span>
            <span style="color: #0000ff;">object</span>.ReferenceEquals(obj1, obj2);</pre>
</div>
<p><strong><span style="font-size: 18px;">3，ValueType的Equals内部是这样实现的</span></strong><br />①如果obj实参为null，就返回false<br />②如果this和obj实参引用不同类型的对象，就返回false<br />③针对类型定义的每个实例字段，都将this对象中的值与obj字段中的值进行比较（通过调用字段的Equals方法）。任何字段不相等，就返回false<br />④返回true，ValueType的Equals方法不调用Object的Equals方法</p>
<p>&nbsp;</p>