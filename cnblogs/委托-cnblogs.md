<div class="cnblogs_code">
<pre><span style="color: #0000ff;">internal</span> <span style="color: #0000ff;">delegate</span> <span style="color: #0000ff;">void</span> Feedback(<span style="color: #0000ff;">int</span> i);</pre>
</div>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">internal</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Feedback : System.MulticastDelegate
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;">构造器</span>
        <span style="color: #0000ff;">public</span> Feedback(<span style="color: #0000ff;">object</span><span style="color: #000000;"> @object, IntPtr method);
        </span><span style="color: #008000;">//</span><span style="color: #008000;">这个方法的原型和源代码指定的一样</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">virtual</span> <span style="color: #0000ff;">void</span> Invoke(<span style="color: #0000ff;">int</span><span style="color: #000000;"> i);

        </span><span style="color: #008000;">//</span><span style="color: #008000;">以下方法实现对回调方法的异步回调</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">virtual</span> IAsyncResult BeginInvoke(<span style="color: #0000ff;">int</span> i, AsyncCallback callback, <span style="color: #0000ff;">object</span><span style="color: #000000;"> @object);
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">virtual</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> EndInvoke(IAsyncResult result);

    }</span></pre>
</div>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;"><strong>1，委托基础</strong></span></p>
<p><span style="font-size: 14px;">①System.MulticastDelegate派生自System.Delegate，后者派生自System.Object。由于历史原因造成两个委托类（MulticastDelegate、Delegate）。即使创建的所有委托类型都将MulticastDelegate作为基类，个别情况下还是会使用到Delegate类型，例如Delegate类的两个静态方法（Combine、Remove）需要传递Delegate类型参数</span></p>
<p><span style="font-size: 14px;">②委托是类，所以凡是能够定义类的地方，都能定义委托</span></p>
<p><span style="font-size: 14px;">③MulticastDelegate</span></p>
<table style="height: 208px; width: 846px;" border="1" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td valign="top" width="102">
<p><strong>字段</strong></p>
</td>
<td valign="top" width="132">
<p><strong>类型</strong></p>
</td>
<td valign="top" width="334">
<p><strong>说明</strong></p>
</td>
</tr>
<tr>
<td valign="top" width="102">
<p><strong>_target</strong></p>
</td>
<td valign="top" width="132">
<p>System.object</p>
</td>
<td valign="top" width="334">
<p>委托对象包含一个静态方法：为null；</p>
<p>委托对象包含一个实例方法：这个字段引用的是回调方法要操作的对象</p>
</td>
</tr>
<tr>
<td valign="top" width="102">
<p><strong>_methedPtr</strong></p>
</td>
<td valign="top" width="132">
<p>System.IntPtr</p>
</td>
<td valign="top" width="334">
<p>一个内部的整数值，CLR用它标识要回调的方法</p>
</td>
</tr>
<tr>
<td valign="top" width="102">
<p><strong>_invocationList</strong></p>
</td>
<td valign="top" width="132">
<p>System.Object</p>
</td>
<td valign="top" width="334">
<p>该字段通常为null，构造委托链时它引用一个委托数组</p>
</td>
</tr>
</tbody>
</table>
<div class="cnblogs_code">
<pre>Feedback fbStatic = <span style="color: #0000ff;">new</span><span style="color: #000000;"> Feedback(Program.FeedbackToConsole);
Feedback fbInstance </span>= <span style="color: #0000ff;">new</span> Feedback(<span style="color: #0000ff;">new</span> Program.FeedbackToFile());</pre>
</div>
<p><img src="http://images2015.cnblogs.com/blog/741594/201706/741594-20170612215551071-1251988213.png" alt="" /></p>
<p>&nbsp;</p>
<p>由于Feedback委托要获取一个int参数并返回void，所以编译器生成的Invoke方法也要获取一个int并返回void</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;"><strong>2，用委托回调多个方法（委托链）</strong></span></p>
<p>①</p>
<div class="cnblogs_code">
<p> Feedback fbChain=null;<br />            fbChain = (Feedback) Delegate.Combine(fbChain, fb1);</p>















</div>
<p>fbChain为null，fb1不为null，Combine发现视图合并的是null和fb1，在内部会直接返回fb1</p>
<p><img src="http://images2015.cnblogs.com/blog/741594/201706/741594-20170614212810868-1868852037.jpg" alt="" /></p>
<p>&nbsp;②</p>
<div class="cnblogs_code">
<p> Feedback fbChain=null;<br />            fbChain = (Feedback) Delegate.Combine(fbChain, fb1);<br />            fbChain = (Feedback) Delegate.Combine(fbChain, fb2);</p>















</div>
<p>Combine发现fbChain和fb2都不为null，会构造一个新的委托对象（_target和_methedPtr不重要）。_invocationList会初始化一个委托对象数组，索引0处被初始化为fb1，索引2处被初始化为fb2</p>
<p><img src="http://images2015.cnblogs.com/blog/741594/201706/741594-20170614212835806-1089450401.jpg" alt="" /></p>
<p>&nbsp;③</p>
<div class="cnblogs_code">
<pre>            Feedback fbChain=<span style="color: #0000ff;">null</span><span style="color: #000000;">;
            fbChain </span>=<span style="color: #000000;"> (Feedback) Delegate.Combine(fbChain, fb1);
            fbChain </span>=<span style="color: #000000;"> (Feedback) Delegate.Combine(fbChain, fb2);
            fbChain </span>= (Feedback) Delegate.Combine(fbChain, fb3);</pre>
</div>
<p>Combine发现fbChain和fb3都不为null。会如②一样创建一个新的对象。之前新建的委托对象以其_invocationList字段引用的数据现在可以进行垃圾回收</p>
<p><img src="http://images2015.cnblogs.com/blog/741594/201706/741594-20170614214807150-272025614.jpg" alt="" /></p>
<p>④在fbChain引用的委托上调用Invoke时，该委托发现私有字段_invocationList不为null，所以会执行一个循环来遍历数组中的所有元素，并依次调用每个委托包装的方法</p>
<div class="cnblogs_code">
<pre>        <span style="color: #008000;">//</span><span style="color: #008000;">伪代码Invoke的实现</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> Invoke(<span style="color: #0000ff;">int</span><span style="color: #000000;"> value)
        {
            Delegate[] delegateSet</span>= _invocationList <span style="color: #0000ff;">as</span><span style="color: #000000;"> Delegate[];
            </span><span style="color: #0000ff;">if</span> (delegateSet != <span style="color: #0000ff;">null</span><span style="color: #000000;">)
            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;">这个委托数组指定了应该调用的委托</span>
                <span style="color: #0000ff;">foreach</span> (Feedback d <span style="color: #0000ff;">in</span><span style="color: #000000;"> delegateSet)
                {
                    d(value);
                }
            }
            </span><span style="color: #0000ff;">else</span><span style="color: #000000;">
            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;">该委托标识了要回调的单个方法
                </span><span style="color: #008000;">//</span><span style="color: #008000;">在指定的目标对象上调用这个回调方法</span>
<span style="color: #000000;">                _methedPtr.Invoke(_target, value);
            }
        }</span></pre>
</div>
<p>如果委托有返回值（internal delegate int Feedback(int i)），则只返回最后一个委托的结果（前面的返回值会被丢弃）</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;"><strong>3，删除委托&nbsp;</strong></span></p>
<div class="cnblogs_code">
<pre>fbChain = (Feedback) Delegate.Remove(fbChain, fb3);</pre>
</div>
<p>①链中只有一个委托，Remove之后会返回null<br />②链中只有两个委托，Remove之后会返回剩余的那个数据项<br />③链中有两个以上，Remove之后会新建一个委托对象（初始化_invocationList数组将引用原始数组中的所有数据项，被删除的除外）</p>
<p>④每次Remove方法调用只能从链中删除一个委托</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;"><strong>4，取得对委托链调用的更多控制</strong></span></p>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MulticastDelegate
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建一个委托数组，其中每个元素都引用链中的一个委托</span>
            <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">sealed</span> <span style="color: #0000ff;">override</span><span style="color: #000000;"> Delegate[] GetInvocationList();
        }</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;"><strong>5，c#为委托提供的简化语法</strong></span></p>
<p>语法糖：越是高级的语言，提供的简化语法越多，以方便写程序</p>
<p>①不需要构造委托对象</p>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> SomeAysncTask(<span style="color: #0000ff;">object</span><span style="color: #000000;"> o){}
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> aa()
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">QueueUserWorkItem方法的第一参数要求的是一个委托对象，
            </span><span style="color: #008000;">//</span><span style="color: #008000;">可以直接传入签名相同的方法</span>
            ThreadPool.QueueUserWorkItem(SomeAysncTask, <span style="color: #800080;">1</span><span style="color: #000000;">);
        }</span></pre>
</div>
<p>②不需要定义回调方法（lambda表达式）</p>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">class</span><span style="color: #000000;"> Class1
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> aa()
        {
            ThreadPool.QueueUserWorkItem(r </span>=&gt; Console.WriteLine(r), <span style="color: #800080;">1</span><span style="color: #000000;">);
        }
    }</span></pre>
</div>
<p>编译器看到lambda表达式后，会在当前类（Class1）中自定义一个新的私有方法（匿名函数）。由编译器生成，可以使用ILDasm.exe查看方法名称。每次编译都可能为方法生成一个不同的名称。（<span style="color: #ff0000;">注意：C#编译器向方法引用了System.Runtime.CompilerServices.CompilerGeneratedAttribute特性，指出该方法由编译器生成，而非程序员写</span>的）</p>
<p>匿名方法是否是static取决于方法内部有没有访问任何实例成员，如果方法内部没有访问任何实例成员，则匿名方式标记为static</p>
<p>③局部变量不需要手动包装到类中即可回调方法</p>
<p>回调代码引用存在于定义方法中的局部参数(numToDo)或变量(squares)</p>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">internal</span> <span style="color: #0000ff;">sealed</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> AClass
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> UsingLocalVariablesInTheCallbackCode(<span style="color: #0000ff;">int</span><span style="color: #000000;"> numToDo)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">一些局部变量</span>
            <span style="color: #0000ff;">int</span>[] squares = <span style="color: #0000ff;">new</span> <span style="color: #0000ff;">int</span><span style="color: #000000;">[numToDo];
            AutoResetEvent done </span>= <span style="color: #0000ff;">new</span> AutoResetEvent(<span style="color: #0000ff;">false</span><span style="color: #000000;">);
            </span><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> i = <span style="color: #800080;">0</span>; i &lt; squares.Length; i++<span style="color: #000000;">)
            {
                ThreadPool.QueueUserWorkItem(obj </span>=&gt;<span style="color: #000000;">
                {
                    </span><span style="color: #0000ff;">int</span> num = (<span style="color: #0000ff;">int</span><span style="color: #000000;">) obj;
                    squares[num] </span>= num*num;<span style="color: #008000;">//</span><span style="color: #008000;">该任务通常更耗时
                    </span><span style="color: #008000;">//</span><span style="color: #008000;">如果是最后一个任务，就让主线程继续运行</span>
                    <span style="color: #0000ff;">if</span> (Interlocked.Decrement(<span style="color: #0000ff;">ref</span> numToDo) == <span style="color: #800080;">0</span><span style="color: #000000;">)
                        done.Set();
                }, i);
            }
            </span><span style="color: #008000;">//</span><span style="color: #008000;">等待其他所有线程结束运行</span>
<span style="color: #000000;">            done.WaitOne();
            </span><span style="color: #008000;">//</span><span style="color: #008000;">显示结果</span>
            <span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> i = <span style="color: #800080;">0</span>; i &lt; squares.Length; i++<span style="color: #000000;">)
            {
                Console.WriteLine(squares[i]);
            }
        }
    }</span></pre>
</div>
<p>c#编译器重写了以上的代码</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">internal</span> <span style="color: #0000ff;">sealed</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> AClass
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> UsingLocalVariablesInTheCallbackCode(<span style="color: #0000ff;">int</span><span style="color: #000000;"> numToDo)
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;">一些局部变量</span>
        WaitCallback callback1 = <span style="color: #0000ff;">null</span><span style="color: #000000;">;
        </span>&lt;&gt;c_DisplayClass2 class1=<span style="color: #0000ff;">new</span> &lt;&gt;<span style="color: #000000;">c_DisplayClass2();
        class1.numToDo </span>=<span style="color: #000000;"> numToDo;
        class1.squares </span>= <span style="color: #0000ff;">new</span> <span style="color: #0000ff;">int</span><span style="color: #000000;">[numToDo];
        class1.done </span>= <span style="color: #0000ff;">new</span> AutoResetEvent(<span style="color: #0000ff;">false</span><span style="color: #000000;">);
        </span><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> i = <span style="color: #800080;">0</span>; i &lt; class1.squares.Length; i++<span style="color: #000000;">)
        {
            </span><span style="color: #0000ff;">if</span>(callback1 == <span style="color: #0000ff;">null</span><span style="color: #000000;">)
                </span><span style="color: #008000;">//</span><span style="color: #008000;">新建的委托对象绑定到辅助对象及其匿名实例方法</span>
                callback1=<span style="color: #0000ff;">new</span> WaitCallback(class1.&lt; UsingLocalVariablesInTheCallbackCode &gt;<span style="color: #000000;"> b_0);
            ThreadPool.QueueUserWorkItem(callback1, i);
        }
        </span><span style="color: #008000;">//</span><span style="color: #008000;">等待其他所有线程结束运行</span>
<span style="color: #000000;">        class1.done.WaitOne();
        </span><span style="color: #008000;">//</span><span style="color: #008000;">显示结果</span>
        <span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> i = <span style="color: #800080;">0</span>; i &lt; class1.squares.Length; i++<span style="color: #000000;">)
        {
            Console.WriteLine(class1.squares[i]);
        }

    }
}
</span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">sealed</span> <span style="color: #0000ff;">class</span> &lt;&gt;c_DisplayClass2:<span style="color: #0000ff;">object</span><span style="color: #000000;">
{
    </span><span style="color: #008000;">//</span><span style="color: #008000;">回调代码要使用的每个变量都有一个对应的公共字段</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span><span style="color: #000000;">[] squares;
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span><span style="color: #000000;"> numToDo;
    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> AutoResetEvent done;
    </span><span style="color: #008000;">//</span><span style="color: #008000;">公共无参构造器</span>
    <span style="color: #0000ff;">public</span> &lt;&gt;<span style="color: #000000;">c_DisplayClass2{}
    </span><span style="color: #008000;">//</span><span style="color: #008000;">包含回调代码的公共实例方法</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> &lt;UsingLocalVariablesInTheCallbackCode&gt;b_0(<span style="color: #0000ff;">object</span><span style="color: #000000;"> obj)
    {
        </span><span style="color: #0000ff;">int</span> num = (<span style="color: #0000ff;">int</span><span style="color: #000000;">) obj;
        squares[num] </span>= num*<span style="color: #000000;">num;
        </span><span style="color: #0000ff;">if</span> (Interlocked.Decrement(<span style="color: #0000ff;">ref</span> numToDo) == <span style="color: #800080;">0</span><span style="color: #000000;">) done.Set();
    }
}</span></pre>
</div>
<p>&nbsp;</p>