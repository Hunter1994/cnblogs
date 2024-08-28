<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">一、发布</span></strong></span></p>
<p>在发布/订阅模式中的角色是彼此陌生的。 一个发布者只是向世界说这个已经发生了，一位订阅者告诉世界&ldquo;我在乎这个&rdquo;。 在这个模型中，没有人关心特定的事件是很好的。 消息可能有一个订阅者，可能有200个，或者可能没有。&nbsp;发布者不应该关心。 EasyNetQ实现这种模式。 如果您开始发布，并且没有订阅者已经开始，那么您的消息就会消失。 这是设计（先订阅，后发布，如果现发布，则消息会丢失）。</p>
<p>代码：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> message = <span style="color: #0000ff;">new</span> MyMessage { Text = <span style="color: #800000;">"</span><span style="color: #800000;">Hello Rabbit</span><span style="color: #800000;">"</span><span style="color: #000000;"> };
bus.Publish(message);</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">二、订阅</span></strong></span></p>
<p>&nbsp;EasyNetQ用户订阅消息类型（消息类的.NET类型）。 一旦通过调用Subscribe方法设置了类型的订阅，就会在RabbitMQ代理上创建一个持久性队列，并且任何类型的消息将被放置在队列中。 RabbitMQ将在连接时将队列中的任何消息发送给用户。</p>
<p>&nbsp;</p>
<p>要订阅一个消息，我们需要给EasyNetQ一个消息到达时执行的操作。 我们通过订阅一个委托来做到这一点：</p>
<div class="cnblogs_code">
<pre>bus.Subscribe&lt;MyMessage&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">my_subscription_id</span><span style="color: #800000;">"</span>, msg =&gt; Console.WriteLine(msg.Text));</pre>
</div>
<p>现在每次发布MyMessage的一个实例，EasyNetQ将会调用我们的代理，并将消息的Text属性打印到控制台。</p>
<p>您传递给订阅的订阅ID很重要。 EasyNetQ将针对消息类型和订阅ID的每个独特组合在RabbitMQ代理上创建一个唯一的队列（<span style="color: #ff0000;">消息类型+订阅ID=唯一的队列</span>）。</p>
<p>&nbsp;</p>
<p>每个对Subscribe的调用都会创建一个新的队列消费者。 <span style="color: #ff0000;">如果您使用相同的消息类型和订阅ID来呼叫两次订阅，则将创建两个消费者从同一个队列中消费的消费者。 然后，RabbitMQ将轮流向每个消费者循环连续的消息。</span> 这对扩展和工作分享非常有用。 假设您已经创建了处理特定消息的服务，但是工作正在重载。 只需启动该服务的新实例（在同一台机器上或另一台机器上），而无需配置任何内容，就可以自动缩放。</p>
<p>&nbsp;</p>
<p><span style="color: #ff0000;">如果您使用不同的订阅ids但是相同的消息类型来呼叫两次订阅，那么您将创建两个队列，每个队列都有自己的消费者</span>。 给定类型的每个消息的副本将被路由到每个队列，因此每个消费者将获得所有消息（该类型的消息）。 如果您有几个不同的服务，那些都关心相同的信息类型，这是非常好的。</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p><span style="font-size: 14pt;"><strong>写订阅回调委托时的注意事项</strong></span></p>
<p>&nbsp;当从通过EasyNetQ订阅的队列接收到消息时，它们被放置在内存队列中。 一个线程坐在循环中，从队列中获取消息并调用其Action代理。 由于代理在一个线程上一次处理一次，所以您应该避免长时间运行的同步IO操作。 尽快从委托返回控制。</p>
<p>&nbsp;</p>
<p><span style="font-size: 14pt;"><strong>使用异步订阅</strong></span></p>
<p>异步订阅允许您的用户委托立即返回任务，然后异步执行长时间运行的IO操作。 一旦长时间运行的订阅完成，只需完成任务。 在下面的示例中，我们使用异步IO操作（DownloadStringTask）向Web服务发出请求。 当任务完成时，我们在控制台上写一行。</p>
<div class="cnblogs_code">
<pre>bus.SubscribeAsync&lt;MyMessage&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">subscribe_async_test</span><span style="color: #800000;">"</span>, message =&gt; 
    <span style="color: #0000ff;">new</span> WebClient().DownloadStringTask(<span style="color: #0000ff;">new</span> Uri(<span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:1338/?timeout=500</span><span style="color: #800000;">"</span><span style="color: #000000;">))
        .ContinueWith(task </span>=&gt;<span style="color: #000000;"> 
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">Received: '{0}', Downloaded: '{1}'</span><span style="color: #800000;">"</span><span style="color: #000000;">, 
                message.Text, 
                task.Result)));</span></pre>
</div>
<p>&nbsp;</p>
<p>另一个例子会导致异常被抛出，如果有故障，那么会导致消息被放置在默认的错误队列上：</p>
<div class="cnblogs_code">
<pre>_bus.SubscribeAsync&lt;MessageType&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">Queue_Identifier</span><span style="color: #800000;">"</span><span style="color: #000000;">,
            message </span>=&gt; Task.Factory.StartNew(() =&gt;<span style="color: #000000;">
            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;">在这里执行一些操作
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span><span style="color: #008000;">//</span><span style="color: #008000;">如果有异常，则会导致任务完成，但任务发生错误
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span><span style="color: #008000;">//</span><span style="color: #008000;">在下面的继续处理</span>
            }).ContinueWith(task =&gt;<span style="color: #000000;">
            {
                </span><span style="color: #0000ff;">if</span> (task.IsCompleted &amp;&amp; !<span style="color: #000000;">task.IsFaulted)
                {
                    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 一切都奏效了</span>
<span style="color: #000000;">                }
                </span><span style="color: #0000ff;">else</span><span style="color: #000000;">
                {                        
                    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 不要抓住这一点，它被进一步上升到层次结构，并导致发送到默认错误队列                  </span>
                    <span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> EasyNetQException(<span style="color: #800000;">"</span><span style="color: #800000;">Message processing exception - look in the default error queue (broker)</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                }
            }));</span></pre>
</div>
<p>&nbsp;</p>
<p><strong><span style="font-size: 14pt;">取消订阅</span></strong></p>
<p>所有的订阅方法返回一个ISubscriptionResult。 它包含描述底层IConsumer使用的IExchange和IQueue的属性，如果需要，可以使用高级API IAdvancedBus进一步操作这些属性。</p>
<p>&nbsp;</p>
<p>您可以随时通过在ISubscriptionResult实例或其ConsumerCancellation属性上调用Dispose来取消订户：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> subscriptionResult = bus.Subscribe&lt;MyMessage&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">sub_id</span><span style="color: #800000;">"</span><span style="color: #000000;">, MyHandler);

...

subscriptionResult.Dispose();
</span><span style="color: #008000;">//</span><span style="color: #008000;"> 这相当于 subscriptionResult.ConsumerCancellation.Dispose();</span></pre>
</div>
<p>这将阻止EasyNetQ从队列中消费，并关闭消费者的频道。</p>
<p>请注意，处理IBus或IAdvancedBus实例也将取消所有消费者并关闭与RabbitMQ的连接。</p>
<p><span style="color: #ff0000;">不要在消息处理程序中调用subscriptionResult.Dispose()。 </span>这将在EasyNetQ ACK消费者频道上的消息与subscriptionResult.Dispose()调用关闭该通道之间创建竞争条件。 由于EasyNetQ的内部架构，这些调用将在不同的线程上被调用，并且时序不是确定性的。</p>