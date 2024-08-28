<p>默认的AMQP发布不是事务性的，并且不能保证您的消息实际上会到达代理。 AMQP指定了一个事务性发布，但是对于RabbitMQ来说，它非常慢，我们还没有通过EasyNetQ API支持。 对于高性能保证交付，建议您使用&ldquo;发布确认&rdquo;。 简而言之，这是AMQP的扩展，<span style="color: #ff0000;">当代理成功收到您的消息时，它会提供回调</span>。</p>
<p>'成功收到'是什么意思？ 这取决于 ...</p>
<ul>
<li>transient(瞬时)消息在队列入场时被确认。</li>
<li>持久性消息一旦被保存到磁盘或者在每个队列上被使用，就会被确认。</li>
<li>直接发布不可修改的瞬态消息。</li>
</ul>
<p>通过在连接字符串上设置publisherConfirms = true来启用发布确认：</p>
<div class="cnblogs_code">
<pre>bus = RabbitHutch.CreateBus(<span style="color: #800000;">"</span><span style="color: #800000;">host=localhost;publisherConfirms=true;timeout=10</span><span style="color: #800000;">"</span>);</pre>
</div>
<p>同步bus.Publish（..）方法将在返回之前等待确认。 在超时期限之前未确认（也在连接字符串中配置）将导致引发异常。 发布确认同步发布方法会显着减慢。 如果性能问题，您应该考虑使用PublishAsync方法：</p>
<div class="cnblogs_code">
<pre>bus.PublishAsync(<span style="color: #0000ff;">new</span><span style="color: #000000;"> MyMessage
    {
        Text </span>= <span style="color: #800000;">"</span><span style="color: #800000;">Hello World</span><span style="color: #800000;">"</span><span style="color: #000000;">
    }).ContinueWith(task </span>=&gt;<span style="color: #000000;">
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> 这只会检查完成的任务IsCompleted是否成立，即使对于我们使用if（task.IsCompleted &amp;&amp;！task.IsFaulted）来检查成功的故障状态任务</span>
            <span style="color: #0000ff;">if</span><span style="color: #000000;"> (task.IsCompleted) 
            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;">Console.Out.WriteLine("{0} Completed", count);</span>
<span style="color: #000000;">            }
            </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (task.IsFaulted)
            {
                Console.Out.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">\n\n</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                Console.Out.WriteLine(task.Exception);
                Console.Out.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">\n\n</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }
        });</span></pre>
</div>
<p>这将在收到确认之前返回。 如果未收到确认或NACK确认，任务将在故障状态下完成。</p>
<p>&nbsp;</p>