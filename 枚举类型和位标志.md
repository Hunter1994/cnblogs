<p style="background-color: #169fe6;"><span style="color: #ffffff; font-size: 18pt;">一、枚举类型</span></p>
<p>1，编译枚举时，C#编译器把每个符号转换成类型的一个常量字段。例如将Color枚举类型看成以下代码</p>
<div class="cnblogs_code">
<pre>    <span style="color: #008000;">//</span><span style="color: #008000;">编译枚举时，c#编译器把每个符号转化成类型的一个常量字段</span>
    <span style="color: #0000ff;">internal</span> <span style="color: #0000ff;">struct</span><span style="color: #000000;"> Color : System.Enum
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;">以下一些公共常量，它们定义了Color的符号和值</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">const</span> Color White = (Color) <span style="color: #800080;">0</span><span style="color: #000000;">;
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">const</span> Color Red = (Color) <span style="color: #800080;">1</span><span style="color: #000000;">;
        </span><span style="color: #008000;">//</span><span style="color: #008000;">以下是一个公共实例字段，包含Color变量的值
        </span><span style="color: #008000;">//</span><span style="color: #008000;">不能写代码来直接引用该字段</span>
        <span style="color: #0000ff;">public</span><span style="color: #000000;"> Int32 value_;
    }</span></pre>
</div>
<p>简单的说，枚举是一个结构，其中定义了一组常量字段和一个实例字段。常量字段会嵌入程序集的元数据中，并可以通过反射来访问</p>
<p>2，以下代码显示了如何声明一个基础类型为byte的枚举类型：</p>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">internal</span> <span style="color: #0000ff;">enum</span> Color : <span style="color: #0000ff;">byte</span><span style="color: #000000;">
    {
        Red
    }</span></pre>
</div>
<p>3，枚举的使用</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Drawing;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ConsoleApplication4
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">返回用于容纳一个枚举类型的基础类型
            </span><span style="color: #008000;">//</span><span style="color: #008000;">System.Int32</span>
            Console.WriteLine(Enum.GetUnderlyingType(<span style="color: #0000ff;">typeof</span><span style="color: #000000;"> (ConsoleColor)));

            </span><span style="color: #008000;">//</span><span style="color: #008000;">输出枚举</span>
            Console.WriteLine(ConsoleColor.Blue);<span style="color: #008000;">//</span><span style="color: #008000;">Blue(常规格式)</span>
            Console.WriteLine(ConsoleColor.Blue.ToString());<span style="color: #008000;">//</span><span style="color: #008000;">Blue(常规格式)</span>
            Console.WriteLine(ConsoleColor.Blue.ToString(<span style="color: #800000;">"</span><span style="color: #800000;">G</span><span style="color: #800000;">"</span>));<span style="color: #008000;">//</span><span style="color: #008000;">Blue(常规格式)</span>
            Console.WriteLine(ConsoleColor.Blue.ToString(<span style="color: #800000;">"</span><span style="color: #800000;">D</span><span style="color: #800000;">"</span>));<span style="color: #008000;">//</span><span style="color: #008000;">9(十进制格式)</span>
            Console.WriteLine(ConsoleColor.Blue.ToString(<span style="color: #800000;">"</span><span style="color: #800000;">X</span><span style="color: #800000;">"</span>));<span style="color: #008000;">//</span><span style="color: #008000;">00000009(十六进制格式)


            </span><span style="color: #008000;">//</span><span style="color: #008000;">获取枚举数组</span>
            <span style="color: #0000ff;">var</span> s = (ConsoleColor[]) Enum.GetValues(<span style="color: #0000ff;">typeof</span><span style="color: #000000;"> (ConsoleColor));
            </span><span style="color: #0000ff;">foreach</span> (<span style="color: #0000ff;">var</span> consoleColor <span style="color: #0000ff;">in</span><span style="color: #000000;"> s)
            {
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">{0,5:D}\t{0:G}</span><span style="color: #800000;">"</span><span style="color: #000000;">,consoleColor);
            }

            </span><span style="color: #008000;">//</span><span style="color: #008000;">输出Blue</span>
            Console.WriteLine(Enum.GetName(<span style="color: #0000ff;">typeof</span> (ConsoleColor), <span style="color: #800080;">9</span><span style="color: #000000;">)) ;

            </span><span style="color: #008000;">//</span><span style="color: #008000;">根据名称获取枚举值，没找到则抛异常</span>
            <span style="color: #0000ff;">var</span> color = (ConsoleColor) Enum.Parse(<span style="color: #0000ff;">typeof</span> (ConsoleColor), <span style="color: #800000;">"</span><span style="color: #800000;">Blue</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">true</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">根据枚举值获取枚举</span>
<span style="color: #000000;">            ConsoleColor c;
            Enum.TryParse</span>&lt;ConsoleColor&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">9</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">true</span>, <span style="color: #0000ff;">out</span><span style="color: #000000;"> c);
            Console.WriteLine(c.ToString()); </span><span style="color: #008000;">//</span><span style="color: #008000;">输出Blue</span>
            Enum.TryParse&lt;ConsoleColor&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">1231</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">true</span>, <span style="color: #0000ff;">out</span><span style="color: #000000;"> c);
            Console.WriteLine(c.ToString());</span><span style="color: #008000;">//</span><span style="color: #008000;">输出1231

            </span><span style="color: #008000;">//</span><span style="color: #008000;">IsDefined方法判断数据对于某枚举是否合法</span>
            Console.WriteLine(Enum.IsDefined(<span style="color: #0000ff;">typeof</span>(ConsoleColor),<span style="color: #800080;">1</span>));<span style="color: #008000;">//</span><span style="color: #008000;">True 存在该值的枚举</span>
            Console.WriteLine(Enum.IsDefined(<span style="color: #0000ff;">typeof</span>(ConsoleColor), <span style="color: #800000;">"</span><span style="color: #800000;">Blue</span><span style="color: #800000;">"</span>));<span style="color: #008000;">//</span><span style="color: #008000;">True 存在该名称的枚举</span>
            Console.WriteLine(Enum.IsDefined(<span style="color: #0000ff;">typeof</span>(ConsoleColor), <span style="color: #800000;">"</span><span style="color: #800000;">blue</span><span style="color: #800000;">"</span>));<span style="color: #008000;">//</span><span style="color: #008000;">Flase 不存在该名称的枚举（区分大小写）</span>
            Console.WriteLine(Enum.IsDefined(<span style="color: #0000ff;">typeof</span>(ConsoleColor), <span style="color: #800080;">1231</span>));<span style="color: #008000;">//</span><span style="color: #008000;">Flase 不存在该值的枚举</span>
            Console.WriteLine(Enum.IsDefined(<span style="color: #0000ff;">typeof</span>(ConsoleColor), (ConsoleColor)<span style="color: #800080;">1231</span>));<span style="color: #008000;">//</span><span style="color: #008000;">Flase 不存在该值的枚举</span>
<span style="color: #000000;">
            Console.ReadKey();
        }
    }
}</span></pre>
</div>
<p>&nbsp;IsDefined使用需谨慎，首先它总是执行区分大小写的查找；其次它相当慢，因为它在内部使用了反射</p>
<p>4，枚举的默认值</p>
<p>如果没有为枚举显示设置值得话，会有默认值</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">二、位标志</span></p>
<p>定义用于标识位标识的枚举类型时，当然应该显示为每个符号分配一个数值。强烈建议向枚举类型应用[Flags]特性</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">    [Flags]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">enum</span><span style="color: #000000;"> Status
    {
        Start</span>=<span style="color: #800080;">1</span><span style="color: #000000;">,
        Order</span>=<span style="color: #800080;">2</span><span style="color: #000000;">,
        End</span>=<span style="color: #800080;">4</span><span style="color: #000000;">,
        All</span>= Start|<span style="color: #000000;"> Order
    }</span></pre>
</div>
<p>1，[Flags]特性</p>
<div class="cnblogs_code">
<pre>//Status s = (Status)5;<br />Status s = Status.Start |<span style="color: #000000;"> Status.End;//5
Console.WriteLine(s.ToString());</span><span style="color: #008000;">//</span><span style="color: #008000;">Start,End<br />Console.WriteLine(s.ToString("F"));//如果不加上flags特性可以使用&ldquo;F&rdquo;格式获得正确的字符串<br /></span></pre>
</div>
<p>调用ToString时，他会视图将数值转换为对应的符号。现在的数值是5，没有对应的符号。如果不加上[Flags]特性的话，就会显示5。加上该特性，就会把它视为一组为标志，由于5是由1(Start)和4(End)组成，所以ToString会生成字符串Start,End</p>
<p>2，位标志的使用</p>
<div class="cnblogs_code">
<pre>            <span style="color: #008000;">//</span><span style="color: #008000;">由于Start被定义为1，所以"s"被初始化为1</span>
            Status s =(Status)Enum.Parse(<span style="color: #0000ff;">typeof</span> (Status), <span style="color: #800000;">"</span><span style="color: #800000;">Start</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">true</span><span style="color: #000000;">);
            Console.WriteLine(s.ToString());</span><span style="color: #008000;">//</span><span style="color: #008000;">Start

            </span><span style="color: #008000;">//</span><span style="color: #008000;">由于Start和End已定义，所以"s1"初始化为5</span>
<span style="color: #000000;">            Status s1;
            Enum.TryParse</span>&lt;Status&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">Start,End</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">true</span>, <span style="color: #0000ff;">out</span><span style="color: #000000;"> s1);
            Console.WriteLine(s1.ToString());</span><span style="color: #008000;">//</span><span style="color: #008000;">Start,End

            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建一个Status枚举实例，其值为7</span>
            Status s2 = (Status)Enum.Parse(<span style="color: #0000ff;">typeof</span>(Status),<span style="color: #800000;">"</span><span style="color: #800000;">7</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">true</span><span style="color: #000000;">);
            Console.WriteLine(s2.ToString());</span><span style="color: #008000;">//</span><span style="color: #008000;">All,End</span></pre>
</div>
<p>&nbsp;</p>