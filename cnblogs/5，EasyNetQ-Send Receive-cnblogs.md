<p>而发布/订阅和请求/响应模式是位置透明的，因为您不需要指定消息的消费者所在的位置，发送/接收模式专门用于通过命名队列进行通信。 它也不会对可以通过队列发送的消息的类型做任何假设。 这意味着您可以通过同一个队列发送不同类型的消息。</p>
<p>&nbsp;</p>
<p>要发送消息，请使用IBus上的发送方法，指定要发送消息的队列的名称和消息本身：</p>
<div class="cnblogs_code">
<pre>bus.Send(<span style="color: #800000;">"</span><span style="color: #800000;">my.queue</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span> MyMessage{ Text = <span style="color: #800000;">"</span><span style="color: #800000;">Hello Widgets!</span><span style="color: #800000;">"</span> });</pre>
</div>
<p>要为特定消息类型设置消息接收器，请使用IBus上的Receive方法：</p>
<div class="cnblogs_code">
<pre>bus.Receive&lt;MyMessage&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">my.queue</span><span style="color: #800000;">"</span>, message =&gt; Console.WriteLine(<span style="color: #800000;">"</span><span style="color: #800000;">MyMessage: {0}</span><span style="color: #800000;">"</span>, message.Text));</pre>
</div>
<p>您可以通过使用采取Action &lt;IReceiveRegistration&gt;的接收重载来为同一队列上的不同消息类型设置多个接收器，例如：</p>
<div class="cnblogs_code">
<pre>bus.Receive(<span style="color: #800000;">"</span><span style="color: #800000;">my.queue</span><span style="color: #800000;">"</span>, x =&gt;<span style="color: #000000;"> x
    .Add</span>&lt;MyMessage&gt;(message =&gt; deliveredMyMessage =<span style="color: #000000;"> message)
    .Add</span>&lt;MyOtherMessage&gt;(message =&gt; deliveredMyOtherMessage = message));</pre>
</div>
<p>如果消息到达不具有匹配接收者的接收队列，则EasyNetQ将将消息写入到EasyNetQ错误队列，其中有一个异常，称为&ldquo;找不到消息类型&lt;message type&gt;&rdquo;的处理程序。</p>
<p>&nbsp;</p>