<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">一、显示接口方法实现（EIMI）</span></p>
<p>将定义方法的那个接口的名称作为方法的前缀</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('7f8504c4-3cb3-4af6-b35c-8bd6db538f8a')"><img id="code_img_closed_7f8504c4-3cb3-4af6-b35c-8bd6db538f8a" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_7f8504c4-3cb3-4af6-b35c-8bd6db538f8a" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('7f8504c4-3cb3-4af6-b35c-8bd6db538f8a',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_7f8504c4-3cb3-4af6-b35c-8bd6db538f8a" class="cnblogs_code_hide">
<pre>    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SimpleType : IDisposable
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Dispose()
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">SimpleType Dispose</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }
        </span><span style="color: #008000;">//</span><span style="color: #008000;">定义EIMI不允许指定可访问性。会自动设置为private。EIMI方法不能标记为virtual</span>
        <span style="color: #0000ff;">void</span><span style="color: #000000;"> IDisposable.Dispose()
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">IDisposable Dispose</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }
    }

    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {

        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            SimpleType s </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> SimpleType();
            s.Dispose();
            IDisposable idis </span>=<span style="color: #000000;"> s;
            idis.Dispose();
            Console.ReadKey();
        }
    }</span></pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">二、使用泛型接口的好处</span></p>
<p>1，泛型接口提供了出色的编译时留下安全性</p>
<p>2，处理值类型时装箱次数会少很多</p>
<p>3，类可以实现同一个接口若干次，只要每次使用不同的类型参数</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('d348d712-64a2-4f7a-93e3-85cf5577e077')"><img id="code_img_closed_d348d712-64a2-4f7a-93e3-85cf5577e077" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_d348d712-64a2-4f7a-93e3-85cf5577e077" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('d348d712-64a2-4f7a-93e3-85cf5577e077',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_d348d712-64a2-4f7a-93e3-85cf5577e077" class="cnblogs_code_hide">
<pre>    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> Number : IComparable&lt;Int32&gt;, IComparable&lt;<span style="color: #0000ff;">string</span>&gt;<span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span> CompareTo(<span style="color: #0000ff;">string</span><span style="color: #000000;"> other)
        {
            </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> NotImplementedException();
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span> CompareTo(<span style="color: #0000ff;">int</span><span style="color: #000000;"> other)
        {
            </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> NotImplementedException();
        }
    }</span></pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">三、EIMI最主要的问题</span></p>
<p>1，没有文档解释类型具体如何实现一个EIMI方法，也没有&ldquo;智能感知&rdquo;支持<br />2，值类型的实例在转换成接口时装箱<br />3，EIMI不能由派生类型调用</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">四、设计：基类还是接口</span></p>
<p>1，IS-A（指&ldquo;属于&rdquo;，例如，汽车属于交通工具）对比CAN-DO（指&ldquo;能做某事&rdquo;，例如，一个类型能将自己的实例装换为另一个类型）关系<br />类型只能继承一个实现。如果派生类和基类型建立不起IS-A关系，就不用基类而用接口。接口意味着CAN-DO关系。如果多种对象类型都&ldquo;能&rdquo;做某事，就为它们创建接口。例如，一个类型能将自己的实例转换为另一个类型（IConvertible），一个类型能序列化自己的实例（ISerializable）。注意，值类型必须从System.ValueType派生，所以不能从一个任意的基类派生。这时必须使用CAN-DO关系并定义接口<br />2，易用性<br />对于开发人员，定义从基类派生的新类型通常比实现接口的所有方法容易的多。基类型可提供大量功能，所以派生类型可能只需要稍作改动。而提供接口的话，新类型必须实现所有成员<br />3，一致性实现<br />无论接口协定订立得有多好，都无法保证所有人百分之百正确实现它。事实上，COM颇受该问题之累，导致有的COM对象只能正常用于Microsoft Office Word或者Microsoft Internet Explorer。而如果为基类型提供良好的默认实现，那么一开始得到的就是能正常工作并经过良好测试的类型。以后根据需要修改就可以了<br />4，版本控制<br />向基类添加一个方法，派生类型将继承新方法。一开始使用的就是一个能正常工作的类型，用户的源代码甚至不需要重新编译。而向接口添加新成员，会强迫接口的继承者更改其源代码并重新编译</p>