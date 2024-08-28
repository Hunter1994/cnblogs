<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">1，为什么要定义GetHashCode方法</span></p>
<p>类型定义Equals之所以还要定义GetHashCode，是由于在Hashtable和Dictionary类型以及其他一些集合的实现中，要求对象必须具有相同哈希码才被视为相等。所以，重写Equals就必须重写GetHashCode方法，确保相等性算法和对象哈希码算法一致</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">2，选择算法来计算类型实例的哈希码时，请遵循以下规则</span></p>
<p>①这个算法要提供良好的随即分布，使哈希表获得最佳性能</p>
<p>②可在算法中调用基类的GetHashCode方法，并包含它的返回值。但一般不要调用Object或ValueType的GetHashCode方法，因为两者的实现都与高性能哈希算法&ldquo;不沾边&rdquo;<br />③算法至少使用一个实例字段<br />④理想情况下，算法使用的字段应该不可变；也就是说，字段应在对象构造时初始化，在对象生存期&ldquo;永不言变&rdquo;<br />⑤算法执行速度尽量快<br />⑥包含相同值得不同对象应返回相同的哈希码。例如，包含相同文本的两个String对象应该返回相同的哈希码</p>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ConsoleApplication3
{

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> A
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">int</span><span style="color: #000000;"> aaa;

        </span><span style="color: #0000ff;">public</span> A(<span style="color: #0000ff;">int</span><span style="color: #000000;"> aaaa)
        {
            aaa </span>=<span style="color: #000000;"> aaaa;
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> a { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">bool</span> Equals(<span style="color: #0000ff;">object</span><span style="color: #000000;"> obj)
        {
            </span><span style="color: #0000ff;">return</span> obj.GetType()==<span style="color: #000000;">GetType();
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">int</span><span style="color: #000000;"> GetHashCode()
        {
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> aaa;
        }
    }


    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #0000ff;">var</span> aa = <span style="color: #0000ff;">new</span> A(<span style="color: #800080;">1</span>) {a = <span style="color: #800000;">"</span><span style="color: #800000;">2</span><span style="color: #800000;">"</span><span style="color: #000000;">};
            </span><span style="color: #0000ff;">var</span> aa1 = <span style="color: #0000ff;">new</span> A(<span style="color: #800080;">1</span>) {a = <span style="color: #800000;">"</span><span style="color: #800000;">3</span><span style="color: #800000;">"</span><span style="color: #000000;">};

            Dictionary</span>&lt;A, <span style="color: #0000ff;">string</span>&gt; s = <span style="color: #0000ff;">new</span> Dictionary&lt;A, <span style="color: #0000ff;">string</span>&gt;<span style="color: #000000;">();
            s.Add(aa, </span><span style="color: #800000;">"</span><span style="color: #800000;">2</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            Console.WriteLine(aa.GetHashCode());
            Console.WriteLine(aa1.GetHashCode());

            </span><span style="color: #008000;">//</span><span style="color: #008000;">使用不同对象相同hash码能找到字典中的对象</span>
<span style="color: #000000;">            Console.WriteLine(s[aa1]);

            </span><span style="color: #0000ff;">foreach</span> (<span style="color: #0000ff;">var</span> VARIABLE <span style="color: #0000ff;">in</span><span style="color: #000000;"> s)
            {
                
                </span><span style="color: #008000;">//</span><span style="color: #008000;">Console.WriteLine(VARIABLE.Value);</span>
<span style="color: #000000;">            }

            Console.ReadKey();
        }
    }
}</span></pre>
</div>
<p>&nbsp;</p>