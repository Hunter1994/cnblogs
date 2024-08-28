<p>EasyNetQ在为队列生成名称时的默认行为是使用 &nbsp; 消息类型名称+subscription Id</p>
<p>例如，名称空间EasyNetQ.Tests.Integration中的PartyInvitation消息类型将使用队列名称EasyNetQ.Tests.Integration.PartyInvitation：EasyNetQ.Tests_schedulingTest1，假定订阅ID为schedulingTest1。</p>
<p>1，控制队列名称</p>
<p>要控制队列的名称，请使用Queue属性注释消息类：</p>
<div class="cnblogs_code">
<pre>[Queue(<span style="color: #800000;">"</span><span style="color: #800000;">TestMessagesQueue</span><span style="color: #800000;">"</span>, ExchangeName = <span style="color: #800000;">"</span><span style="color: #800000;">MyTestExchange</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> TestMessage
{
   </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Text { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> ...</span>
<span style="color: #000000;">
bus.Subscribe</span>&lt;TestMessage&gt;(<span style="color: #0000ff;">string</span>.Empty, msg =&gt; Console.WriteLine(msg.Text));</pre>
</div>
<p>在这里，我们告诉EasyNetQ将TestMessagesQueue用作队列名称，将MyTestExchange用作交换名称。 注意传递给Subscribe方法的subscriptionId是空的。 如果指定subscriptionId，则它将被追加到末尾并用作队列名称。</p>
<p>&nbsp;</p>
<p>2，有关命名队列的注意事项</p>
<p>将队列名称设置为空字符串将使用默认的命名行为。队列名称的最大长度为255个字符（这由RabbitMQ客户端库执行）。名称可以是字母，数字，连字符，下划线，句号或冒号的序列。队列名称以&ldquo;amq&rdquo;开头。保留给预先声明和标准化的队列。</p>
<p>&nbsp;</p>