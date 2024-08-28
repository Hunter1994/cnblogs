<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">一、异常处理机制</span></p>
<p>1，应该在try中放置多少代码？<br />取决于状态管理。如果在一个try块中执行多个可能抛出同一个异常类型的操作，但不同的操作有不同的异常恢复措施，则应该将每个操作都放到他自己的try块中，这样才能正确地恢复状态<br />2，try、finally，catch执行顺序</p>
<div class="cnblogs_code">
<pre>            <span style="color: #0000ff;">try</span><span style="color: #000000;">
            {
                </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
                {
                    </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> Exception(<span style="color: #800000;">"</span><span style="color: #800000;">异常</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                }
                </span><span style="color: #0000ff;">finally</span><span style="color: #000000;">
                {
                    Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">finally</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                }
            }
            </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> 
            {
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">catch</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }
            </span><span style="color: #008000;">//</span><span style="color: #008000;">输出顺序：finally catch</span>
            Console.ReadLine();</pre>
</div>
<p>3，finally设计</p>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">private</span> <span style="color: #0000ff;">void</span> ReadData(<span style="color: #0000ff;">string</span><span style="color: #000000;"> pathname)
        {
            FileStream fs </span>= <span style="color: #0000ff;">null</span><span style="color: #000000;">;
            </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
            {
                fs </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> FileStream(pathname, FileMode.Open);
                </span><span style="color: #008000;">//</span><span style="color: #008000;">处理文件中的数据</span>
<span style="color: #000000;">            }
            </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (IOException)
            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;">在此添加从IOException恢复的代码</span>
<span style="color: #000000;">            }
            </span><span style="color: #0000ff;">finally</span><span style="color: #000000;">
            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;">确保文件被关闭</span>
                <span style="color: #0000ff;">if</span>(fs!=<span style="color: #0000ff;">null</span><span style="color: #000000;">)fs.Close();
            }
        }</span></pre>
</div>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">二、System.Exception类</span></p>
<table style="height: 663px; width: 794px;" border="1" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td valign="top" width="83">
<p>属性名称</p>
</td>
<td valign="top" width="66">
<p>访问</p>
</td>
<td valign="top" width="57">
<p>类型</p>
</td>
<td valign="top" width="362">
<p>说明</p>
</td>
</tr>
<tr>
<td valign="top" width="83">
<p>Message</p>
</td>
<td valign="top" width="66">
<p>只读</p>
</td>
<td valign="top" width="57">
<p>String</p>
</td>
<td valign="top" width="362">
<p>包含辅助性文字说明，指出抛出异常的原因。</p>
<p>如果抛出的异常未处理，该消息通常被写入日志。</p>
<p>由于最终用户一般不看这种消息，所以消息应提供尽可能多的技术细节，方便开发人员修正代码</p>
</td>
</tr>
<tr>
<td valign="top" width="83">
<p>Data</p>
</td>
<td valign="top" width="66">
<p>只读</p>
</td>
<td valign="top" width="57">
<p>IDictionary</p>
</td>
<td valign="top" width="362">
<p>引用一个&ldquo;键/值对&rdquo;集合。</p>
<p>代码在抛出异常前在该集合中添加记录项；捕捉异常的代码可在异常恢复过程中查询记录项并利用其中的信息</p>
</td>
</tr>
<tr>
<td valign="top" width="83">
<p>Source</p>
</td>
<td valign="top" width="66">
<p>读/写</p>
</td>
<td valign="top" width="57">
<p>String</p>
</td>
<td valign="top" width="362">
<p>包含生成异常的程序集名称</p>
</td>
</tr>
<tr>
<td valign="top" width="83">
<p>StackTrace</p>
</td>
<td valign="top" width="66">
<p>只读</p>
</td>
<td valign="top" width="57">
<p>String</p>
</td>
<td valign="top" width="362">
<p>包含抛出异常之前调用过的所有方法的名称和签名，该属性对调试很有用</p>
</td>
</tr>
<tr>
<td valign="top" width="83">
<p>TargetSite</p>
</td>
<td valign="top" width="66">
<p>只读</p>
</td>
<td valign="top" width="57">
<p>MethodBase</p>
</td>
<td valign="top" width="362">
<p>包含抛出异常的方法</p>
</td>
</tr>
<tr>
<td valign="top" width="83">
<p>HelpLink</p>
</td>
<td valign="top" width="66">
<p>只读</p>
</td>
<td valign="top" width="57">
<p>String</p>
</td>
<td valign="top" width="362">
<p>包含帮助用户理解异常的一个文档的URL（例如file://c:/myapp/help.html#MyExceptionHelp）。但要注意，健全的编程和安全实践阻止用户查看原始未处理的异常。因此，除非希望将信息传达给其他程序员，否则不要使用该属性</p>
</td>
</tr>
<tr>
<td valign="top" width="83">
<p>InnerException</p>
</td>
<td valign="top" width="66">
<p>只读</p>
</td>
<td valign="top" width="57">
<p>Exception</p>
</td>
<td valign="top" width="362">
<p>如果当前异常是在处理一个异常时抛出，该属性就指出上一个异常是什么。</p>
<p>这个属性通常为null。</p>
<p>Exception类型还提供了公共方法GetBaseException来遍历由内层构成的链表，并返回最初抛出的异常</p>
</td>
</tr>
<tr>
<td valign="top" width="83">
<p>HResult</p>
</td>
<td valign="top" width="66">
<p>读/写</p>
</td>
<td valign="top" width="57">
<p>Int32</p>
</td>
<td valign="top" width="362">
<p>托管代码喝本机代码边界时使用的一个32位值。</p>
<p>例如：当COM API返回代表失败的HRESULT值时，CLR抛出一个Exception派生对象，并通过该属性来维护HRESULT值</p>
</td>
</tr>
</tbody>
</table>
<div class="cnblogs_code">
<pre>        <span style="color: #008000;">//</span><span style="color: #008000;">禁止JIT编译器在调试喝发布生成时对该方法进行内联处理</span>
<span style="color: #000000;">        [MethodImpl(MethodImplOptions.NoInlining)]
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> aa()
        {
        }</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">三、设计规范和最佳实践</span></p>
<p>1，善用finally块</p>
<p>①无论线程抛出什么类型的异常，finally块中的代码都会执行</p>
<p>②应该先用finally块清理那些已成功启动的操作，再返回至调用者执行finally块之后的代码</p>
<p>③需经常利用finally块显式释放对象以避免资源泄露</p>
<p>&nbsp;</p>
<p>只要使用了lock、using、foreach语句、重写类的析构器时c#编译器也会自动生成try/finally块。使用这些构造时，编译器将你写的代码放到try块内部，并将清理代码放到finally块中</p>
<p>①使用lock语句时，锁在finally块中释放</p>
<p>②使用using语句时，在finally块中调用对象的Dispose方法</p>
<p>③使用foreach'语句时，在finally快中调用IEnumerator对象的Dispose方法</p>
<p>④定义析构方法时，在finally块中调用基类的Finalize方法</p>
<p>2，不要什么都捕捉</p>
<p>3，得体地从异常中恢复</p>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> CalculateSpreadsheetCell(<span style="color: #0000ff;">int</span> row, <span style="color: #0000ff;">int</span><span style="color: #000000;"> column)
        {
            </span><span style="color: #0000ff;">string</span><span style="color: #000000;"> result;
            </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
            {
                result </span>= <span style="color: #008000;">/*</span><span style="color: #008000;">计算电子表格单元格中的值</span><span style="color: #008000;">*/</span><span style="color: #000000;">
            }
            </span><span style="color: #0000ff;">catch</span> (DivideByZeroException) <span style="color: #008000;">//</span><span style="color: #008000;">捕捉被零整除错误</span>
<span style="color: #000000;">            {
                result </span>= <span style="color: #800000;">"</span><span style="color: #800000;">can't show value:divide by zero</span><span style="color: #800000;">"</span><span style="color: #000000;">;
            }
            </span><span style="color: #0000ff;">catch</span> (OverflowException)<span style="color: #008000;">//</span><span style="color: #008000;">捕捉溢出错误</span>
<span style="color: #000000;">            {
                result </span>= <span style="color: #800000;">"</span><span style="color: #800000;">can't show value:too big</span><span style="color: #800000;">"</span><span style="color: #000000;">;
            }
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> result;
        }</span></pre>
</div>
<p>4，发生不可恢复的异常时回滚部分完成的操作&mdash;&mdash;维持状态</p>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> SerializeObjectGraph(FileStream fs, IFormatter formatter, <span style="color: #0000ff;">object</span><span style="color: #000000;"> rootObj)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">保存文件的当前位置</span>
            Int64 beforeSerializetion = fs.Position;<span style="color: #008000;">//</span><span style="color: #008000;">获取或设置此流的当前位置</span>
            <span style="color: #0000ff;">try</span><span style="color: #000000;">
            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;">尝试将对象图序列化到文件中</span>
<span style="color: #000000;">                formatter.Serialize(fs, rootObj);
            }
            </span><span style="color: #0000ff;">catch</span> <span style="color: #008000;">//</span><span style="color: #008000;">捕捉所有异常</span>
<span style="color: #000000;">            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;">任何事情出错，就将文件恢复到一个有效的状态</span>
                fs.Position =<span style="color: #000000;"> beforeSerializetion;

                </span><span style="color: #008000;">//</span><span style="color: #008000;">截断文件</span>
<span style="color: #000000;">                fs.SetLength(fs.Position);

                </span><span style="color: #008000;">//</span><span style="color: #008000;">注意：上述代码没有放到finally快中，因为只有在序列化失败时才对流进行重置
                </span><span style="color: #008000;">//</span><span style="color: #008000;">重新抛出相同的异常，让调用者知道发生了什么</span>
                <span style="color: #0000ff;">throw</span><span style="color: #000000;">;
            }
        }</span></pre>
</div>
<p><span style="line-height: 1.5;">5，异常实现细节来维系协定</span></p>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">private</span> <span style="color: #0000ff;">string</span> m_pathname;<span style="color: #008000;">//</span><span style="color: #008000;">地址簿文件的路径名</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> GetPhoneNumber(<span style="color: #0000ff;">string</span><span style="color: #000000;"> name)
        {
            </span><span style="color: #0000ff;">string</span><span style="color: #000000;"> phone;
            FileStream fs </span>= <span style="color: #0000ff;">null</span><span style="color: #000000;">;
            </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
            {
                fs </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> FileStream(m_pathname, FileMode.Open);
                </span><span style="color: #008000;">//</span><span style="color: #008000;">这里的代码重fs读取内容，直至找到匹配的name</span>
                phone = <span style="color: #008000;">/*</span><span style="color: #008000;">已经找到的电话号码</span><span style="color: #008000;">*/</span><span style="color: #000000;">
            }
            </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (FileNotFoundException e)
            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;">抛出一个不同的异常，将name包含到其中，并将原来的异常设为内部异常</span>
                <span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> NameNotFoundException(name, e);
            }
            </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (IOException e)
            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;">抛出一个不同的异常，将name包含到其中，并将原来的异常设为内部异常</span>
                <span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> NameNotFoundException(name, e);
            }
            </span><span style="color: #0000ff;">finally</span><span style="color: #000000;">
            {
                </span><span style="color: #0000ff;">if</span>(fs!=<span style="color: #0000ff;">null</span><span style="color: #000000;">)fs.Close();
            }
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> phone;
        }</span></pre>
</div>
<p>&nbsp;通过反射调用方法时，CLR内部捕捉方法抛出的任何异常，并把它转换成一个<strong>TargetInvocationException</strong></p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">四、未处理的异常</span></p>
<p>1，异常抛出时，CLR在调用栈中向上查找与抛出的异常对象类型匹配的catch块。没有任何catch块匹配抛出的异常类型，就发生一个<strong>未处理的异常</strong>。CLR检测到继承中的任何线程有未处理的异常，都会禁止进程</p>
<p>2，类库开发人员不用去处理未处理的异常，应用程序开发人员需要处理，Micorosoft建议应用程序开发人员接受CLR默认策略（应用程序发生未处理的异常时，windows会想事件日志写入一条记录，通过windows日志-&gt;应用程序 查看）</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">五、约束执行区域（CER）</span></p>
<p>根据定义，CER是必须对错误有适应力的代码块</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Runtime.CompilerServices;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Runtime.ConstrainedExecution;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ConsoleApplication1
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">强迫finally块中的代码提前准备好</span>
            RuntimeHelpers.PrepareConstrainedRegions();<span style="color: #008000;">//</span><span style="color: #008000;">using System.Runtime.CompilerServices;</span>
            <span style="color: #0000ff;">try</span><span style="color: #000000;">
            {
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">In Try</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }
            </span><span style="color: #0000ff;">finally</span><span style="color: #000000;">
            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;">隐士调用Type1的静态构造器(调用S方法不会先输出.ctor exception)</span>
<span style="color: #000000;">                Type1.M();
            }
            Console.ReadLine();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">输出：.ctor exception
            </span><span style="color: #008000;">//</span><span style="color: #008000;">In Try</span>
<span style="color: #000000;">        }
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">sealed</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Type1
    {
        </span><span style="color: #0000ff;">static</span><span style="color: #000000;"> Type1()
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">如果这里抛出异常,M就得不到调用</span>
            Console.WriteLine(<span style="color: #800000;">"</span><span style="color: #800000;">.ctor exception</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }
        </span><span style="color: #008000;">//</span><span style="color: #008000;">using System.Runtime.ConstrainedExecution;</span>
<span style="color: #000000;">        [ReliabilityContract(Consistency.WillNotCorruptState, Cer.Success)]
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> M() { }
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> S() { }

    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p>1，PrepareConstrainedRegions是一个很特别的方法。<br />①JIT编译器如果发现在一个try块之前调用了这个方法，就会提前编译与try关联的catch和finally块中的代码。<br />②JIT编译器会加载任何程序集，创建任何类型对象，调用任何静态构造器，并对任何方法进行JIT编译<br />③如果其中任何操作造成异常，这个异常会在线程假如try块之前发生<br />④JIT编译器提前准备方法时，会遍历整个调用图，提前准备被调用的方法，前提是这些方法应用了ReliabilityContractAttribute（并且传递的是Consistency.WillNotCorruptState或者Consistency.MayCorruptInstance）<br />⑤如果你写的方法保证不损坏任何状态，就用Consistency.WillNotCorruptState，否则就用其他三个值之一来申明方法可能损坏哪一种状态<br />⑥如果方法保证不会失败，就用Cer.Success，否则用Cer.MayFail（Cer.None这个值表明方法不就行CER保证）</p>
<p>&nbsp;</p>