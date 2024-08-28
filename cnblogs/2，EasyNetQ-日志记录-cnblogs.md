<p>EasyNetQ提供了一个IEasyNetQLogger接口：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IEasyNetQLogger
{
   </span><span style="color: #0000ff;">void</span> DebugWrite(<span style="color: #0000ff;">string</span> format, <span style="color: #0000ff;">params</span> <span style="color: #0000ff;">object</span><span style="color: #000000;">[] args);
   </span><span style="color: #0000ff;">void</span> InfoWrite(<span style="color: #0000ff;">string</span> format, <span style="color: #0000ff;">params</span> <span style="color: #0000ff;">object</span><span style="color: #000000;">[] args);
   </span><span style="color: #0000ff;">void</span> ErrorWrite(<span style="color: #0000ff;">string</span> format, <span style="color: #0000ff;">params</span> <span style="color: #0000ff;">object</span><span style="color: #000000;">[] args);
   </span><span style="color: #0000ff;">void</span><span style="color: #000000;"> ErrorWrite(Exception exception);
}</span></pre>
</div>
<p>实现IEasyNetQLogger接口</p>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyLogger : IEasyNetQLogger
        {
            </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> DebugWrite(<span style="color: #0000ff;">string</span> format, <span style="color: #0000ff;">params</span> <span style="color: #0000ff;">object</span><span style="color: #000000;">[] args)
            {
            }

            </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> ErrorWrite(Exception exception)
            {
            }

            </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> ErrorWrite(<span style="color: #0000ff;">string</span> format, <span style="color: #0000ff;">params</span> <span style="color: #0000ff;">object</span><span style="color: #000000;">[] args)
            {
            }

            </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> InfoWrite(<span style="color: #0000ff;">string</span> format, <span style="color: #0000ff;">params</span> <span style="color: #0000ff;">object</span><span style="color: #000000;">[] args)
            {
                Console.WriteLine(format, args);
            }
        }</span></pre>
</div>
<p>使用日志记录</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> bus = RabbitHutch.CreateBus(<span style="color: #800000;">"</span><span style="color: #800000;">host=localhost</span><span style="color: #800000;">"</span>, x =&gt; x.Register&lt;IEasyNetQLogger&gt;(_ =&gt; <span style="color: #0000ff;">new</span> MyLogger()))</pre>
</div>
<p>&nbsp;</p>