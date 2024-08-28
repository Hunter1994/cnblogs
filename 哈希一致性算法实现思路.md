<p>&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> HashDemo
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">list.key虚拟节点 list.value实际节点</span>
            Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">string</span>&gt; list = <span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">string</span>&gt;<span style="color: #000000;">();
            list.Add(</span><span style="color: #800000;">"</span><span style="color: #800000;">192.168.1.1</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">192.168.1.1</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            list.Add(</span><span style="color: #800000;">"</span><span style="color: #800000;">192.168.1.2</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">192.168.1.2</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            list.Add(</span><span style="color: #800000;">"</span><span style="color: #800000;">192.168.1.3</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">192.168.1.3</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            list.Add(</span><span style="color: #800000;">"</span><span style="color: #800000;">192.168.1.4</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">192.168.1.4</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            list.Add(</span><span style="color: #800000;">"</span><span style="color: #800000;">192.168.1.5</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">192.168.1.5</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            list.Add(</span><span style="color: #800000;">"</span><span style="color: #800000;">192.168.1.6</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">192.168.1.1</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            list.Add(</span><span style="color: #800000;">"</span><span style="color: #800000;">192.168.1.7</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">192.168.1.2</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            list.Add(</span><span style="color: #800000;">"</span><span style="color: #800000;">192.168.1.8</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">192.168.1.3</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            list.Add(</span><span style="color: #800000;">"</span><span style="color: #800000;">192.168.1.9</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">192.168.1.4</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            list.Add(</span><span style="color: #800000;">"</span><span style="color: #800000;">192.168.1.10</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">192.168.1.5</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">节点的hashcode和节点的实际地址</span>
            SortedDictionary&lt;<span style="color: #0000ff;">int</span>, <span style="color: #0000ff;">string</span>&gt; dic = <span style="color: #0000ff;">new</span> SortedDictionary&lt;<span style="color: #0000ff;">int</span>, <span style="color: #0000ff;">string</span>&gt;<span style="color: #000000;">();
            </span><span style="color: #0000ff;">foreach</span> (<span style="color: #0000ff;">var</span> item <span style="color: #0000ff;">in</span><span style="color: #000000;"> list)
            {
                dic.Add(item.Key.GetHashCode(), item.Value);
            }

            </span><span style="color: #008000;">//</span><span style="color: #008000;">请求的缓存</span>
            List&lt;<span style="color: #0000ff;">string</span>&gt; checheKey = <span style="color: #0000ff;">new</span> List&lt;<span style="color: #0000ff;">string</span>&gt;() { <span style="color: #800000;">"</span><span style="color: #800000;">enterprise456</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">project123</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">3</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">4</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">5</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">6</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">7</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">8</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">900000</span><span style="color: #800000;">"</span><span style="color: #000000;"> };
            </span><span style="color: #008000;">//</span><span style="color: #008000;">ip分配的节点值（测试看）</span>
            Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">string</span>&gt; result = <span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">string</span>&gt;<span style="color: #000000;">();
            </span><span style="color: #008000;">//</span><span style="color: #008000;">请求的缓存随机分配</span>
            <span style="color: #0000ff;">foreach</span> (<span style="color: #0000ff;">var</span> item2 <span style="color: #0000ff;">in</span><span style="color: #000000;"> checheKey)
            {
                </span><span style="color: #0000ff;">var</span> key1 =<span style="color: #000000;"> item2;
                </span><span style="color: #0000ff;">foreach</span> (<span style="color: #0000ff;">var</span> item <span style="color: #0000ff;">in</span><span style="color: #000000;"> dic)
                {
                    </span><span style="color: #0000ff;">if</span> (item.Key &gt;=<span style="color: #000000;"> key1.GetHashCode())
                    {
                        </span><span style="color: #0000ff;">string</span><span style="color: #000000;"> value;
                        </span><span style="color: #0000ff;">if</span> (result.TryGetValue(item.Value, <span style="color: #0000ff;">out</span><span style="color: #000000;"> value))
                        {
                            result[item.Value] </span>= result[item.Value] + <span style="color: #800000;">"</span><span style="color: #800000;">,</span><span style="color: #800000;">"</span> +<span style="color: #000000;"> key1;
                        }
                        </span><span style="color: #0000ff;">else</span><span style="color: #000000;">
                        {
                            result.Add(item.Value, key1);
                        }
                        </span><span style="color: #0000ff;">break</span><span style="color: #000000;">;
                    }
                }
            }
           
            </span><span style="color: #0000ff;">foreach</span> (<span style="color: #0000ff;">var</span> item <span style="color: #0000ff;">in</span><span style="color: #000000;"> result)
            {
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">key:{0} value:{1}</span><span style="color: #800000;">"</span><span style="color: #000000;">, item.Key, item.Value);
            }

            Console.ReadLine();
        }

    }
}</span></pre>
</div>
<p><a href="http://pan.baidu.com/s/1nvfpFsd" target="_blank">源码下载http://pan.baidu.com/s/1nvfpFsd</a></p>
<p>&nbsp;</p>