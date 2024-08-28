<p>EasyNetQ的使命是为基于RabbitMQ的消息传递提供最简单的API。 核心IBus接口有意避免公开AMQP概念，如交换，绑定和队列，而是实现基于消息类型的默认交换绑定队列拓扑。</p>
<p>对于某些场景，能够配置您自己的exchange绑定队列拓扑是很有用的;高级EasyNetQ API允许您这样做。高级API对AMQP有很好的理解。</p>
<p>高级API通过IAdvancedBus接口实现。 该接口的一个实例可以通过IBus的高级属性进行访问：&nbsp;<span class="cnblogs_code"><span style="color: #0000ff;">var</span> advancedBus = RabbitHutch.CreateBus(<span style="color: #800000;">"</span><span style="color: #800000;">host=localhost</span><span style="color: #800000;">"</span>).Advanced;</span>&nbsp;</p>
<p>1，声明交换机</p>
<p>要声明交换机，请使用IAdvancedBus的ExchangeDeclare方法：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">IExchange ExchangeDeclare(
    </span><span style="color: #0000ff;">string</span><span style="color: #000000;"> name, 
    </span><span style="color: #0000ff;">string</span><span style="color: #000000;"> type, 
    </span><span style="color: #0000ff;">bool</span> passive = <span style="color: #0000ff;">false</span><span style="color: #000000;">, 
    </span><span style="color: #0000ff;">bool</span> durable = <span style="color: #0000ff;">true</span><span style="color: #000000;">, 
    </span><span style="color: #0000ff;">bool</span> autoDelete = <span style="color: #0000ff;">false</span><span style="color: #000000;">, 
    </span><span style="color: #0000ff;">bool</span> @internal = <span style="color: #0000ff;">false</span><span style="color: #000000;">, 
    </span><span style="color: #0000ff;">string</span> alternateExchange = <span style="color: #0000ff;">null</span><span style="color: #000000;">, 
    </span><span style="color: #0000ff;">bool</span> delayed = <span style="color: #0000ff;">false</span>);</pre>
</div>
<p>name: 交换机名称<br />type:		有效的交换机类型（使用静态ExchangeType类的属性安全地声明交换）<br />passive:&nbsp;不要创建交换。 如果指定的交换不存在，则抛出异常。 （默认为false）<br />durable:&nbsp;生存服务器重新启动。 如果此参数为false，则在服务器重新启动时，交换将被删除。 （默认为true）<br />autoDelete:&nbsp;最后一个队列未被绑定时删除此交换。 （默认为false）<br />internal:&nbsp;这种交换不能由发布者直接使用，而只能由交换使用来交换绑定。 （默认为false）<br />alternateExchange:如果无法路由邮件，则将邮件路由到此交换机。<br />delayed:如果设置，则分配x延迟型交换以路由延迟的消息。</p>
<p>①简单案例</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> create a direct exchange</span>
<span style="color: #0000ff;">var</span> exchange = advancedBus.ExchangeDeclare(<span style="color: #800000;">"</span><span style="color: #800000;">my_exchange</span><span style="color: #800000;">"</span><span style="color: #000000;">, ExchangeType.Direct);

</span><span style="color: #008000;">//</span><span style="color: #008000;"> create a topic exchange</span>
<span style="color: #0000ff;">var</span> exchange = advancedBus.ExchangeDeclare(<span style="color: #800000;">"</span><span style="color: #800000;">my_exchange</span><span style="color: #800000;">"</span><span style="color: #000000;">, ExchangeType.Topic);

</span><span style="color: #008000;">//</span><span style="color: #008000;"> create a fanout exchange</span>
<span style="color: #0000ff;">var</span> exchange = advancedBus.ExchangeDeclare(<span style="color: #800000;">"</span><span style="color: #800000;">my_exchange</span><span style="color: #800000;">"</span>, ExchangeType.Fanout);</pre>
</div>
<p>要获得RabbitMQ默认交换，请执行以下操作：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> exchange = Exchange.GetDefault();</pre>
</div>
<p>2，声明队列</p>
<p>要声明队列，请使用IAdvancedBus的QueueDeclare方法：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">IQueue QueueDeclare(
    </span><span style="color: #0000ff;">string</span><span style="color: #000000;"> name, 
    </span><span style="color: #0000ff;">bool</span> passive = <span style="color: #0000ff;">false</span><span style="color: #000000;">, 
    </span><span style="color: #0000ff;">bool</span> durable = <span style="color: #0000ff;">true</span><span style="color: #000000;">, 
    </span><span style="color: #0000ff;">bool</span> exclusive = <span style="color: #0000ff;">false</span><span style="color: #000000;">, 
    </span><span style="color: #0000ff;">bool</span> autoDelete = <span style="color: #0000ff;">false</span><span style="color: #000000;">,
    </span><span style="color: #0000ff;">int</span>? perQueueMessageTtl  = <span style="color: #0000ff;">null</span><span style="color: #000000;">, 
    </span><span style="color: #0000ff;">int</span>? expires = <span style="color: #0000ff;">null</span><span style="color: #000000;">,
    </span><span style="color: #0000ff;">byte</span>? maxPriority = <span style="color: #0000ff;">null</span><span style="color: #000000;">,
    </span><span style="color: #0000ff;">string</span> deadLetterExchange = <span style="color: #0000ff;">null</span><span style="color: #000000;">, 
    </span><span style="color: #0000ff;">string</span> deadLetterRoutingKey = <span style="color: #0000ff;">null</span><span style="color: #000000;">,
    </span><span style="color: #0000ff;">int</span>? maxLength = <span style="color: #0000ff;">null</span><span style="color: #000000;">,
    </span><span style="color: #0000ff;">int</span>? maxLengthBytes = <span style="color: #0000ff;">null</span>);</pre>
</div>
<p>name: 队列的名称<br />passive:如果队列不存在，则不要创建该队列，而是引发异常（默认为false）<br />durable:&nbsp;可以在服务器重新启动后继续运行 如果这是错误的，则在服务器重新启动时，队列将被删除。 （默认为true）<br />exclusive:&nbsp;只能由当前连接访问，其他连接上来会抛异常。 （默认为false）<br />autoDelete:&nbsp;所有消费者断开连接后删除队列。 （默认为false）<br />perQueueMessageTtl:丢弃之前，消息在队列中应保留多长时间（以毫秒为单位）。 （默认未设置）<br />expires:&nbsp;自动删除之前，队列应该保持未使用状态的时间以毫秒为单位。 （默认未设置）<br />maxPriority:&nbsp;确定队列应支持的最大消息优先级。<br />deadLetterExchange:确定交换机的名称在被服务器自动删除之前可以保持未使用状态。<br />deadLetterRoutingKey:如果设置，将路由消息与指定的路由密钥，如果未设置，则消息将使用与最初发布的路由密钥相同的路由。<br />maxLength:&nbsp;队列中可能存在的最大可用消息数。 一旦达到限制，邮件就会从队列的前面被删除或死信，以便为新邮件腾出空间。<br />maxLengthBytes:队列的最大大小（以字节为单位）。 一旦达到限制，邮件就会从队列的前面被删除或死信，以便为新邮件腾出空间</p>
<p>请注意，如果定义了maxLength和/或maxLengthBytes属性，则RabbitMQ的行为可能并不如人们所期望的那样。 人们可能会期望代理拒绝进一步的消息; 但是RabbitMQ文档（https://www.rabbitmq.com/maxlength.html）表明，一旦达到限制，邮件将从队列的前端丢弃或死锁，以便为新邮件腾出空间。</p>
<p>①简单案例</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> declare a durable queue</span>
<span style="color: #0000ff;">var</span> queue = advancedBus.QueueDeclare(<span style="color: #800000;">"</span><span style="color: #800000;">my_queue</span><span style="color: #800000;">"</span><span style="color: #000000;">);

</span><span style="color: #008000;">//</span><span style="color: #008000;"> declare a queue with message TTL of 10 seconds:</span>
<span style="color: #0000ff;">var</span> queue = advancedBus.QueueDeclare(<span style="color: #800000;">"</span><span style="color: #800000;">my_queue</span><span style="color: #800000;">"</span>, perQueueTtl:<span style="color: #800080;">10000</span>);</pre>
</div>
<p>要声明一个'未命名的'独占队列，其中RabbitMQ提供队列名称，请使用不带参数的QueueDeclare重载：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> queue = advancedBus.QueueDeclare();</pre>
</div>
<p>请注意，EasyNetQ的自动消费者重新连接逻辑被关闭以用于独占队列。</p>
<p>3，绑定</p>
<p>你将一个队列绑定到像这样的交换机上：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> queue = advancedBus.QueueDeclare(<span style="color: #800000;">"</span><span style="color: #800000;">my.queue</span><span style="color: #800000;">"</span><span style="color: #000000;">);
</span><span style="color: #0000ff;">var</span> exchange = advancedBus.ExchangeDeclare(<span style="color: #800000;">"</span><span style="color: #800000;">my.exchange</span><span style="color: #800000;">"</span><span style="color: #000000;">, ExchangeType.Topic);
</span><span style="color: #0000ff;">var</span> binding = advancedBus.Bind(exchange, queue, <span style="color: #800000;">"</span><span style="color: #800000;">A.*</span><span style="color: #800000;">"</span>);</pre>
</div>
<p>要指定队列和交换机之间的多个绑定，只需执行多个绑定调用即可：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> queue = advancedBus.QueueDeclare(<span style="color: #800000;">"</span><span style="color: #800000;">my.queue</span><span style="color: #800000;">"</span><span style="color: #000000;">);
</span><span style="color: #0000ff;">var</span> exchange = advancedBus.ExchangeDeclare(<span style="color: #800000;">"</span><span style="color: #800000;">my.exchange</span><span style="color: #800000;">"</span><span style="color: #000000;">, ExchangeType.Topic);
advancedBus.Bind(exchange, queue, </span><span style="color: #800000;">"</span><span style="color: #800000;">A.B</span><span style="color: #800000;">"</span><span style="color: #000000;">);
advancedBus.Bind(exchange, queue, </span><span style="color: #800000;">"</span><span style="color: #800000;">A.C</span><span style="color: #800000;">"</span>);</pre>
</div>
<p>你也可以将交换机绑定在一个链上:</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> sourceExchange = advancedBus.ExchangeDeclare(<span style="color: #800000;">"</span><span style="color: #800000;">my.exchange.1</span><span style="color: #800000;">"</span><span style="color: #000000;">, ExchangeType.Topic);
</span><span style="color: #0000ff;">var</span> destinationExchange = advancedBus.ExchangeDeclare(<span style="color: #800000;">"</span><span style="color: #800000;">my.exchange.2</span><span style="color: #800000;">"</span><span style="color: #000000;">, ExchangeType.Topic);
</span><span style="color: #0000ff;">var</span> queue = advancedBus.QueueDeclare(<span style="color: #800000;">"</span><span style="color: #800000;">my.queue</span><span style="color: #800000;">"</span><span style="color: #000000;">);

advancedBus.Bind(sourceExchange, destinationExchange, </span><span style="color: #800000;">"</span><span style="color: #800000;">A.*</span><span style="color: #800000;">"</span><span style="color: #000000;">);
advancedBus.Bind(destinationExchange, queue, </span><span style="color: #800000;">"</span><span style="color: #800000;">A.C</span><span style="color: #800000;">"</span>);</pre>
</div>
<p>4，发布</p>
<p>先进的Publish方法允许您指定要发布消息的交换机。 它还允许访问消息的AMQP基本属性。</p>
<p>创建你的消息。 高级API要求您的消息包装在消息中：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> myMessage = <span style="color: #0000ff;">new</span> MyMessage {Text = <span style="color: #800000;">"</span><span style="color: #800000;">Hello from the publisher</span><span style="color: #800000;">"</span><span style="color: #000000;">};
</span><span style="color: #0000ff;">var</span> message = <span style="color: #0000ff;">new</span> Message&lt;MyMessage&gt;(myMessage);</pre>
</div>
<p>Message类可让您访问AMQP基本属性，例如：</p>
<div class="cnblogs_code">
<pre>message.Properties.AppId = <span style="color: #800000;">"</span><span style="color: #800000;">my_app_id</span><span style="color: #800000;">"</span><span style="color: #000000;">;
message.Properties.ReplyTo </span>= <span style="color: #800000;">"</span><span style="color: #800000;">my_reply_queue</span><span style="color: #800000;">"</span>;</pre>
</div>
<p>最后使用发布方法发布您的消息。 在这里，我们正在向默认交流发布：</p>
<div class="cnblogs_code">
<pre>bus.Publish(Exchange.GetDefault(), queueName, <span style="color: #0000ff;">false</span>, <span style="color: #0000ff;">false</span>, message);</pre>
</div>
<p>发布的重载允许您绕过EasyNetQ的消息序列化并创建自己的字节数组消息:</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> properties = <span style="color: #0000ff;">new</span><span style="color: #000000;"> MessageProperties();
</span><span style="color: #0000ff;">var</span> body = Encoding.UTF8.GetBytes(<span style="color: #800000;">"</span><span style="color: #800000;">Hello World!</span><span style="color: #800000;">"</span><span style="color: #000000;">);
bus.Publish(Exchange.GetDefault(), queueName, </span><span style="color: #0000ff;">false</span>, <span style="color: #0000ff;">false</span>, properties, body);</pre>
</div>
<p>5，订阅</p>
<p>使用IAdvancedBus的Consume方法来消费队列中的消息。</p>
<div class="cnblogs_code">
<pre>IDisposable Consume&lt;T&gt;(IQueue queue, Func&lt;IMessage&lt;T&gt;, MessageReceivedInfo, Task&gt; onMessage) <span style="color: #0000ff;">where</span> T : <span style="color: #0000ff;">class</span>;</pre>
</div>
<p>onMessage委托是您为消息传递提供的处理程序。 其参数如下：</p>
<p>如上面发布部分所述，IMessage使您可以访问消息及其MessageProperties。 MessageReceivedInfo为您提供有关消息消耗的上下文的额外信息：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MessageReceivedInfo
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> ConsumerTag { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">ulong</span> DeliverTag { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">bool</span> Redelivered { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Exchange { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> RoutingKey { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }         
}</span></pre>
</div>
<p>您返回一个允许您编写非阻塞异步处理程序的任务。</p>
<p>消耗方法返回一个IDisposable。 调用其Dispose方法来取消使用者。</p>
<p>如果您只需要同步处理程序，则可以使用同步重载：</p>
<div class="cnblogs_code">
<pre>IDisposable Consume&lt;T&gt;(IQueue queue, Action&lt;IMessage&lt;T&gt;, MessageReceivedInfo&gt; onMessage) <span style="color: #0000ff;">where</span> T : <span style="color: #0000ff;">class</span>;</pre>
</div>
<p>要绕过EasyNetQ的消息序列化器，请使用提供原始字节数组消息的消耗超载：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">void</span> Consume(IQueue queue, Func&lt;Byte[], MessageProperties, MessageReceivedInfo, Task&gt; onMessage);</pre>
</div>
<p>在这个例子中，我们使用队列'my_queue'中的原始消息字节：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> queue = advancedBus.QueueDeclare(<span style="color: #800000;">"</span><span style="color: #800000;">my_queue</span><span style="color: #800000;">"</span><span style="color: #000000;">);
advancedBus.Consume(queue, (body, properties, info) </span>=&gt; Task.Factory.StartNew(() =&gt;<span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">var</span> message =<span style="color: #000000;"> Encoding.UTF8.GetString(body);
        Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">Got message: '{0}'</span><span style="color: #800000;">"</span><span style="color: #000000;">, message);
    }));</span></pre>
</div>
<p>您可以选择使用Consume方法的这种重载向单个使用者注册多个处理程序：</p>
<div class="cnblogs_code">
<pre>IDisposable Consume(IQueue queue, Action&lt;IHandlerRegistration&gt; addHandlers);</pre>
</div>
<p>IHandlerRegistration接口如下所示：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IHandlerRegistration
{
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
    <span style="color: #808080;">///</span><span style="color: #008000;"> 添加异步处理程序
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
    <span style="color: #808080;">///</span> <span style="color: #808080;">&lt;typeparam name="T"&gt;</span><span style="color: #008000;">The message type</span><span style="color: #808080;">&lt;/typeparam&gt;</span>
    <span style="color: #808080;">///</span> <span style="color: #808080;">&lt;param name="handler"&gt;</span><span style="color: #008000;">The handler</span><span style="color: #808080;">&lt;/param&gt;</span>
    <span style="color: #808080;">///</span> <span style="color: #808080;">&lt;returns&gt;&lt;/returns&gt;</span>
    IHandlerRegistration Add&lt;T&gt;(Func&lt;IMessage&lt;T&gt;, MessageReceivedInfo, Task&gt;<span style="color: #000000;"> handler)
        </span><span style="color: #0000ff;">where</span> T : <span style="color: #0000ff;">class</span><span style="color: #000000;">;

    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
    <span style="color: #808080;">///</span><span style="color: #008000;"> 添加同步处理程序
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
    <span style="color: #808080;">///</span> <span style="color: #808080;">&lt;typeparam name="T"&gt;</span><span style="color: #008000;">消息类型</span><span style="color: #808080;">&lt;/typeparam&gt;</span>
    <span style="color: #808080;">///</span> <span style="color: #808080;">&lt;param name="handler"&gt;</span><span style="color: #008000;">The handler</span><span style="color: #808080;">&lt;/param&gt;</span>
    <span style="color: #808080;">///</span> <span style="color: #808080;">&lt;returns&gt;&lt;/returns&gt;</span>
    IHandlerRegistration Add&lt;T&gt;(Action&lt;IMessage&lt;T&gt;, MessageReceivedInfo&gt;<span style="color: #000000;"> handler)
        </span><span style="color: #0000ff;">where</span> T : <span style="color: #0000ff;">class</span><span style="color: #000000;">;

    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
    <span style="color: #808080;">///</span><span style="color: #008000;">如果处理程序集合在未找到匹配的处理程序时应抛出EasyNetQException，则设置为true;如果应返回noop处理程序，则设置为false .Default为true。
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
    <span style="color: #0000ff;">bool</span> ThrowOnNoMatchingHandler { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}</span></pre>
</div>
<p>在这个例子中，我们注册了两个不同的处理程序，一个处理MyMessage类型的消息，另一个处理MyOtherMessage类型的消息：</p>
<div class="cnblogs_code">
<pre>bus.Advanced.Consume(queue, x =&gt;<span style="color: #000000;"> x
        .Add</span>&lt;MyMessage&gt;((message, info) =&gt;<span style="color: #000000;"> 
            { 
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">Got MyMessage {0}</span><span style="color: #800000;">"</span><span style="color: #000000;">, message.Body.Text);
                countdownEvent.Signal();
            })
        .Add</span>&lt;MyOtherMessage&gt;((message, info) =&gt;<span style="color: #000000;">
            {
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">Got MyOtherMessage {0}</span><span style="color: #800000;">"</span><span style="color: #000000;">, message.Body.Text);
                countdownEvent.Signal();
            })
    );</span></pre>
</div>
<p>查看这篇博文了解更多信息：<a href="http://mikehadlow.blogspot.co.uk/2013/11/easynetq-multiple-handlers-per-consumer.html" rel="nofollow">http://mikehadlow.blogspot.co.uk/2013/11/easynetq-multiple-handlers-per-consumer.html</a></p>
<p>6，从队列中获取单个消息</p>
<p>要从队列中获取单条消息，请使用IAdvancedBus.Get方法：</p>
<div class="cnblogs_code">
<pre>IBasicGetResult&lt;T&gt; Get&lt;T&gt;(IQueue queue) <span style="color: #0000ff;">where</span> T : <span style="color: #0000ff;">class</span>;</pre>
</div>
<p>从AMQP文档：&ldquo;此方法使用同步对话提供对队列中消息的直接访问，该同步对话旨在用于同步功能比性能更重要的特定类型的应用程序。&rdquo; 不要使用Get来轮询消息。 在典型的应用场景中，您应该始终支持消费。</p>
<p>IBasicGetResult具有以下签名：</p>
<div class="cnblogs_code">
<pre><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
<span style="color: #808080;">///</span><span style="color: #008000;">AdvancedBus Get方法的结果
</span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
<span style="color: #808080;">///</span> <span style="color: #808080;">&lt;typeparam name="T"&gt;&lt;/typeparam&gt;</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span> IBasicGetResult&lt;T&gt; <span style="color: #0000ff;">where</span> T : <span style="color: #0000ff;">class</span><span style="color: #000000;">
{
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
    <span style="color: #808080;">///</span><span style="color: #008000;">如果消息可用，则为true，否则为false。
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
    <span style="color: #0000ff;">bool</span> MessageAvailable { <span style="color: #0000ff;">get</span><span style="color: #000000;">; }

    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
    <span style="color: #808080;">///</span><span style="color: #008000;"> 消息从队列中回收。 如果没有消息可用，此属性将引发MessageNotAvailableException。 在尝试访问它之前，您应该检查MessageAvailable属性。
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
    IMessage&lt;T&gt; Message { <span style="color: #0000ff;">get</span><span style="color: #000000;">; }
}</span></pre>
</div>
<p>在访问Message属性前总是检查MessageAvailable方法。</p>
<p>一个例子：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> queue = advancedBus.QueueDeclare(<span style="color: #800000;">"</span><span style="color: #800000;">get_test</span><span style="color: #800000;">"</span><span style="color: #000000;">);
advancedBus.Publish(Exchange.GetDefault(), </span><span style="color: #800000;">"</span><span style="color: #800000;">get_test</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">false</span>, <span style="color: #0000ff;">false</span><span style="color: #000000;">,
    </span><span style="color: #0000ff;">new</span> Message&lt;MyMessage&gt;(<span style="color: #0000ff;">new</span> MyMessage{ Text = <span style="color: #800000;">"</span><span style="color: #800000;">Oh! Hello!</span><span style="color: #800000;">"</span><span style="color: #000000;"> }));

</span><span style="color: #0000ff;">var</span> getResult = advancedBus.Get&lt;MyMessage&gt;<span style="color: #000000;">(queue);

</span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (getResult.MessageAvailable)
{
    Console.Out.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">Got message: {0}</span><span style="color: #800000;">"</span><span style="color: #000000;">, getResult.Message.Body.Text);
}
</span><span style="color: #0000ff;">else</span><span style="color: #000000;">
{
    Console.Out.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">Failed to get message!</span><span style="color: #800000;">"</span><span style="color: #000000;">);
}</span></pre>
</div>
<p>要访问原始二进制消息，请使用非通用Get方法：</p>
<div class="cnblogs_code">
<pre>IBasicGetResult Get(IQueue queue);</pre>
</div>
<p>非泛型IBasicGetResult具有以下定义：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IBasicGetResult
{
    </span><span style="color: #0000ff;">byte</span>[] Body { <span style="color: #0000ff;">get</span><span style="color: #000000;">; }
    MessageProperties Properties { </span><span style="color: #0000ff;">get</span><span style="color: #000000;">; }
    MessageReceivedInfo Info { </span><span style="color: #0000ff;">get</span><span style="color: #000000;">; }
}</span></pre>
</div>
<p>7，消息类型必须匹配</p>
<p>EasyNetQ高级API期望订户仅接收通用类型参数提供的类型的消息。 在上面的例子中，只有MyMessage类型的消息应该被接收。 但是，EasyNetQ不保护您不向用户发布错误类型的消息。 我可以很容易地设置一个交换绑定队列拓扑来发布NotMyMessage类型的消息，该消息将被上面的处理程序接收。 如果接收到错误类型的消息，EasyNetQ将抛出EasyNetQInvalidMessageTypeException异常：</p>
<div class="cnblogs_code">
<pre>EasyNetQ.EasyNetQInvalidMessageTypeException: Message type <span style="color: #0000ff;">is</span> incorrect. Expected <span style="color: #800000;">'</span><span style="color: #800000;">EasyNetQ_Tests_MyMessage:EasyNetQ_Tests</span><span style="color: #800000;">'</span>, but was <span style="color: #800000;">'</span><span style="color: #800000;">EasyNetQ_Tests_MyOtherMessage:EasyNetQ_Tests</span><span style="color: #800000;">'</span><span style="color: #000000;">
   at EasyNetQ.RabbitAdvancedBus.CheckMessageType[TMessage](MessageProperties properties) </span><span style="color: #0000ff;">in</span> D:\Source\EasyNetQ\Source\EasyNetQ\RabbitAdvancedBus.cs:line <span style="color: #800080;">217</span><span style="color: #000000;">
   at EasyNetQ.RabbitAdvancedBus.</span>&lt;&gt;c__DisplayClass1`<span style="color: #800080;">1</span>.&lt;Subscribe&gt;b__0(Byte[] body, MessageProperties properties, MessageReceivedInfo messageRecievedInfo) <span style="color: #0000ff;">in</span> D:\Source\EasyNetQ\Source\EasyNetQ\RabbitAdvancedBus.cs:line <span style="color: #800080;">131</span><span style="color: #000000;">
   at EasyNetQ.RabbitAdvancedBus.</span>&lt;&gt;c__DisplayClass6.&lt;Subscribe&gt;b__5(String consumerTag, UInt64 deliveryTag, Boolean redelivered, String exchange, String routingKey, IBasicProperties properties, Byte[] body) <span style="color: #0000ff;">in</span> D:\Source\EasyNetQ\Source\EasyNetQ\RabbitAdvancedBus.cs:line <span style="color: #800080;">176</span><span style="color: #000000;">
   at EasyNetQ.QueueingConsumerFactory.HandleMessageDelivery(BasicDeliverEventArgs basicDeliverEventArgs) </span><span style="color: #0000ff;">in</span> D:\Source\EasyNetQ\Source\EasyNetQ\QueueingConsumerFactory.cs:line <span style="color: #800080;">85</span></pre>
</div>
<p>8，事件</p>
<p>当通过RabbitHutch实例化一个IBus时，您可以指定一个AdvancedBusEventHandlers。 该类包含IAdvancedBus中存在的每个事件的事件处理程序属性，并提供了在总线实例化之前指定事件处理程序的方法。</p>
<p>不必使用它，因为一旦创建了总线，它仍然可以添加事件处理程序。 但是，如果您希望能够捕获RabbitAdvancedBus的第一个Connected事件，则必须将AdvancedBusEventHandlers与Connected EventHandler一起使用。 这是因为总线将在构造函数返回之前尝试连接一次，如果连接尝试成功，将会引发RabbitAdvancedBus.OnConnected。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> buss = RabbitHutch.CreateBus(<span style="color: #800000;">"</span><span style="color: #800000;">host=localhost</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span> AdvancedBusEventHandlers(connected: (s, e) =&gt;<span style="color: #000000;">
{
      </span><span style="color: #0000ff;">var</span> advancedBus =<span style="color: #000000;"> (IAdvancedBus)s;
      Console.WriteLine(advancedBus.IsConnected); </span><span style="color: #008000;">//</span><span style="color: #008000;"> This will print true.</span>
}));</pre>
</div>
<p>&nbsp;</p>