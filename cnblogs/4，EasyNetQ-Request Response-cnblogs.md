<p>EasyNetQ还支持请求/响应消息传递模式。 这使得客户端/服务器应用程序变得容易，客户机/服务器应用程序在客户端向服务器发出请求，然后处理请求并返回响应。 与传统的RPC机制不同，EasyNetQ请求/响应操作不具有名称，而是简单地由请求/响应消息类型对定义。</p>
<p>此外，与传统的RPC机制（包括大多数Web服务工具包）不同，EasyNetQ的请求/响应模式基于消息传递，因此它是异步开箱即用的。</p>
<p>&nbsp;</p>
<p><strong><span style="font-size: 14pt;">提出请求，并处理响应</span></strong></p>
<p>要使用EasyNetQ发出请求，请在IBus上调用Request方法：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> myRequest = <span style="color: #0000ff;">new</span> MyRequest { Text =<span style="color: #000000;"> &ldquo;Hello Server&rdquo; };
</span><span style="color: #0000ff;">var</span> response = bus.Request&lt;MyRequest, MyResponse&gt;<span style="color: #000000;">(myRequest);
Console.WriteLine(response.Text);</span></pre>
</div>
<p>这里我们创建一个MyMessage类型的新请求，然后调用Request方法，该消息作为参数。 当响应返回时，响应消息的Text属性被输出到控制台。</p>
<p>&nbsp;</p>
<p><strong><span style="font-size: 14pt;">异步请求</span></strong></p>
<p>消息传递本质上是异步的。 您发送消息，然后允许您的程序继续其他任务。 在将来的某一时刻，您会收到回应。 使用上面显示的同步请求方法，您的线程将阻塞，直到返回响应。 使用RequestAsync方法返回任务通常是一个更好的选择：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> task = bus.RequestAsync&lt;TestRequestMessage, TestResponseMessage&gt;<span style="color: #000000;">(request)
task.ContinueWith(response </span>=&gt;<span style="color: #000000;"> {
    Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">Got response: '{0}'</span><span style="color: #800000;">"</span><span style="color: #000000;">, response.Result.Text);
});</span></pre>
</div>
<p>&nbsp;</p>
<p><strong><span style="font-size: 14pt;">响应请求</span></strong></p>
<p>要编写响应请求的服务器，只需使用如下所示的IBus.Respond方法：</p>
<div class="cnblogs_code">
<pre>bus.Respond&lt;MyRequest, MyResponse&gt;(request =&gt; <span style="color: #0000ff;">new</span> MyResponse { Text = &ldquo;Responding to &ldquo; + request.Text});</pre>
</div>
<p>响应采用一个参数，一个需要请求并返回响应的Func &lt;TRequest，TResponse&gt;。 适用于订阅回调的相同建议也适用于响应者。 不要阻止长时间运行的IO操作。 如果要执行长时间运行的IO，请改用RespondAsync。</p>
<p>&nbsp;</p>
<p><strong><span style="font-size: 14pt;">异步响应</span></strong></p>
<p>EasyNetQ还提供了一个RespondAsync方法，它使用Func &lt;TRequest，Task &lt;TResponse &gt;&gt;委托。 这允许您执行长时间运行的IO绑定操作，而不会阻止EasyNetQ订阅处理循环。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;">创建一组工作对象</span>
        <span style="color: #0000ff;">var</span> workers = <span style="color: #0000ff;">new</span> BlockingCollection&lt;MyWorker&gt;<span style="color: #000000;">();
        </span><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> i = <span style="color: #800080;">0</span>; i &lt; <span style="color: #800080;">10</span>; i++<span style="color: #000000;">)
        {
            workers.Add(</span><span style="color: #0000ff;">new</span><span style="color: #000000;"> MyWorker());
        }
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 创建bus</span>
        <span style="color: #0000ff;">var</span> bus = RabbitHutch.CreateBus(<span style="color: #800000;">"</span><span style="color: #800000;">host=localhost</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 回应请求</span>
        bus.RespondAsync&lt;RequestServerTime, ResponseServerTime&gt;(request =&gt;<span style="color: #000000;">
            Task.Factory.StartNew(() </span>=&gt;<span style="color: #000000;">
            {
                </span><span style="color: #0000ff;">var</span> worker =<span style="color: #000000;"> workers.Take();
                </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
                {
                    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> worker.Execute(request);
                }
                </span><span style="color: #0000ff;">finally</span><span style="color: #000000;">
                {
                    workers.Add(worker);
                }
            }));
        Console.ReadLine();
        bus.Dispose();
    }</span></pre>
</div>
<p>&nbsp;</p>
<p><strong><span style="font-size: 14pt;">示例应用程序</span></strong></p>
<p>EasyNetQ示例显示请求响应和Autosubcriber，使用Windsor IOC进行连接</p>
<p><a style="color: #0366d6; text-transform: none; text-indent: 0px; letter-spacing: normal; font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol'; font-size: 16px; font-style: normal; font-weight: normal; text-decoration: underline; word-spacing: 0px; white-space: normal; outline-width: 0px; box-sizing: border-box; orphans: 2; widows: 2; background-color: #ffffff; font-variant-ligatures: normal; font-variant-caps: normal; -webkit-text-stroke-width: 0px;" href="https://bitbucket.org/philipogorman/createrequestservice/src">https://bitbucket.org/philipogorman/createrequestservice/src</a></p>
<p>&nbsp;</p>