<p>EasyNetQ自v0.7.1.30附带一个简单的AutoSubscriber。 您可以使用它轻松扫描实现接口IConsume &lt;T&gt;或IConsumeAsync &lt;T&gt;的类的特定程序集，然后让自动订户将这些使用者订阅到您的总线。 IConsume &lt;T&gt;的实现将使用总线Subscribe方法，而IConsumeAsync &lt;T&gt;的实现将使用总线SubscribeAsync方法，请参阅Subscribe以了解详细信息。 你当然可以让你的消费者处理多个消息。 我们来看看一些样品。</p>
<p>注意：从版本0.13.0开始，所有AutoSubscriber类都位于EasyNetQ.AutoSubscribe命名空间中，因此请添加以下using语句：&nbsp;<span class="cnblogs_code"><span style="color: #0000ff;">using</span> EasyNetQ.AutoSubscribe;</span>&nbsp;</p>
<p>让我们定义一个简单的消费者，处理三条消息：MessageA, MessageB and MessageC.</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> MyConsumer : IConsume&lt;MessageA&gt;, IConsume&lt;MessageB&gt;, IConsumeAsync&lt;MessageC&gt;<span style="color: #000000;">
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Consume(MessageA message) {...}

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Consume(MessageB message) {...}

    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Task Consume(MessageC message) {...}
}</span></pre>
</div>
<p>首先创建AutoSubscriber的新实例，将IBus实例和subscriptionId前缀传递给构造函数。 subscriptionId前缀的前缀是所有自动生成的subscriptionIds，但不是自定义subscriptionIds（请参见下文）。</p>
<p>为了注册这个以及同一个Assembly中的所有其他使用者，我们只需要将包含您的使用者的程序集传递给：AutoSubscriber.Subscribe（assembly）。 注意！ 这是你应该只做一次，最好在应用程序启动时。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> subscriber = <span style="color: #0000ff;">new</span> AutoSubscriber(bus, <span style="color: #800000;">"</span><span style="color: #800000;">my_applications_subscriptionId_prefix</span><span style="color: #800000;">"</span><span style="color: #000000;">);
subscriber.Subscribe(Assembly.GetExecutingAssembly());</span></pre>
</div>
<p>1，通过主题订阅（s）</p>
<p>默认情况下，AutoSubscriber将绑定无主题。 在下面的示例中，MessageA注册了两个主题。</p>
<p>注意！ 如果你运行没有ForTopic属性的代码，它将有一个&ldquo;＃&rdquo;的路由键，它将接收任何消息类型的订阅。 假设安装了默认端口和管理插件，只需访问http：// localhost：15672 /＃/队列并根据需要解除绑定即可。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> MyConsumer : IConsume&lt;MessageA&gt;, IConsume&lt;MessageB&gt;, IConsumeAsync&lt;MessageC&gt;<span style="color: #000000;">
{
    [ForTopic(</span><span style="color: #800000;">"</span><span style="color: #800000;">Topic.Foo</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
    [ForTopic(</span><span style="color: #800000;">"</span><span style="color: #800000;">Topic.Bar</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Consume(MessageA message) {...}

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Consume(MessageB message) {...}

    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Task Consume(MessageC message) {...}
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">To publish by topic</span>
<span style="color: #0000ff;">var</span> bus = RabbitHutch.CreateBus(<span style="color: #800000;">"</span><span style="color: #800000;">host=localhost</span><span style="color: #800000;">"</span><span style="color: #000000;">);

</span><span style="color: #0000ff;">var</span> msg1 = <span style="color: #0000ff;">new</span> MessageA(msg1, <span style="color: #800000;">"</span><span style="color: #800000;">Topic.Foo</span><span style="color: #800000;">"</span>);   <span style="color: #008000;">//</span><span style="color: #008000;">picked up</span>
<span style="color: #0000ff;">var</span> msg2 = <span style="color: #0000ff;">new</span> MessageA(msg2, <span style="color: #800000;">"</span><span style="color: #800000;">Topic.Bar</span><span style="color: #800000;">"</span>);   <span style="color: #008000;">//</span><span style="color: #008000;">picked up</span>
<span style="color: #0000ff;">var</span> msg3 = <span style="color: #0000ff;">new</span> MessageA(msg3);                <span style="color: #008000;">//</span><span style="color: #008000;">not picked up</span></pre>
</div>
<p>2，指定一个特定的SubscriptionId</p>
<p>默认情况下，AutoSubscriber将为每个消息/消费者组合生成唯一的SubscriptionId。 这意味着您将启动同一个使用者的多个实例，并且它们将以循环方式（工作模式）从相同的队列中读取。</p>
<p>如果您希望修订订阅ID，则可以使用AutoSubscriberConsumerAttribute修饰Consume方法。 为什么你会修正它，你可以在这里阅读。</p>
<p>比方说，上面的消费者应该有一个固定的SubscriptionId用于MessageB的消费者方法。 刚刚装饰它并为SubscriptionId定义一个值。</p>
<div class="cnblogs_code">
<pre>[AutoSubscriberConsumer(SubscriptionId = <span style="color: #800000;">"</span><span style="color: #800000;">MyExplicitId</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> Consume(MessageB message) { }</pre>
</div>
<p>3，控制SubscriptionId生成</p>
<p>您当然也可以控制实际的SubscriptionId生成。 只需替换AutoSubscriber.GenerateSubscriptionId：Func &lt;ConsumerInfo，string&gt;。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> subscriber = <span style="color: #0000ff;">new</span><span style="color: #000000;"> AutoSubscriber(bus)
{
    CreateConsumer </span>= t =&gt;<span style="color: #000000;"> objectResolver.Resolve(t),
    GenerateSubscriptionId </span>= c =&gt; AppDomain.CurrentDomain.FriendlyName +<span style="color: #000000;"> c.ConcreteType.Name
};
subscriber.Subscribe(Assembly.GetExecutingAssembly());</span></pre>
</div>
<p>注意！ 只是一个示例实现。 确保您已阅读并理解SubscriptionId值的重要性。</p>
<p>4，控制消费者配置设置</p>
<p>使用自动订阅服务器订阅队列时，可以设置ISubscriptionConfiguration值，例如AutoDelete，Priority等。</p>
<p>通过在创建AutoSubscriber时设置操作。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> subscriber = <span style="color: #0000ff;">new</span><span style="color: #000000;"> AutoSubscriber(bus)
{    
    ConfigureSubscriptionConfiguration </span>= c =&gt;<span style="color: #000000;"> c.WithAutoDelete()
                                               .WithPriority(</span><span style="color: #800080;">10</span><span style="color: #000000;">)
};
subscriber.Subscribe(Assembly.GetExecutingAssembly());</span></pre>
</div>
<p>或者，您可以将一个属性应用于使用方法，该方法优先于ConfigureSubscriptionConfiguration操作设置的任何配置值。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> MyConsumer : IConsume&lt;MessageA&gt;<span style="color: #000000;">
{
    [SubscriptionConfiguration(CancelOnHaFailover </span>= <span style="color: #0000ff;">true</span>, PrefetchCount = <span style="color: #800080;">10</span><span style="color: #000000;">)]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Consume(MessageA message) {...}
}</span></pre>
</div>
<p>5，在AutoSubscriber中使用IoC容器</p>
<p>AutoSubscriber有一个属性MessageDispatcher，它允许您插入自己的消息分派代码。 这使您可以从IoC容器中解析消费者或执行其他自定义调度时间任务。</p>
<p>我们编写一个定制的IAutoSubscriberMessageDispatcher来解析Windsor IoC容器中的消费者</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> WindsorMessageDispatcher : IAutoSubscriberMessageDispatcher
{
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> IWindsorContainer container;

    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> WindsorMessageDispatcher(IWindsorContainer container)
    {
        </span><span style="color: #0000ff;">this</span>.container =<span style="color: #000000;"> container;
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> Dispatch&lt;TMessage, TConsumer&gt;(TMessage message) <span style="color: #0000ff;">where</span> TMessage : <span style="color: #0000ff;">class</span> <span style="color: #0000ff;">where</span> TConsumer : IConsume&lt;TMessage&gt;<span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">var</span> consumer = container.Resolve&lt;TConsumer&gt;<span style="color: #000000;">();
        </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
        {
            consumer.Consume(message);
        }
        </span><span style="color: #0000ff;">finally</span><span style="color: #000000;">
        {
            container.Release(consumer);
        }
    }

    </span><span style="color: #0000ff;">public</span> Task DispatchAsync&lt;TMessage, TConsumer&gt;(TMessage message) <span style="color: #0000ff;">where</span> TMessage: <span style="color: #0000ff;">class</span> <span style="color: #0000ff;">where</span> TConsumer: IConsumeAsync&lt;TMessage&gt;<span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">var</span> consumer = _container.Resolve&lt;TConsumer&gt;<span style="color: #000000;">();           
        </span><span style="color: #0000ff;">return</span> consumer.Consume(message).ContinueWith(t=&gt;<span style="color: #000000;">_container.Release(consumer));            
    }
}</span></pre>
</div>
<p>现在我们需要在我们的IoC容器中注册我们的客户：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> container = <span style="color: #0000ff;">new</span><span style="color: #000000;"> WindsorContainer();
container.Register(
    Component.For</span>&lt;MyConsumer&gt;().ImplementedBy&lt;MyConsumer&gt;<span style="color: #000000;">()
    );</span></pre>
</div>
<p>接下来使用我们的自定义IMessageDispatcher设置AutoSubscriber：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> bus = RabbitHutch.CreateBus(<span style="color: #800000;">"</span><span style="color: #800000;">host=localhost</span><span style="color: #800000;">"</span><span style="color: #000000;">);

</span><span style="color: #0000ff;">var</span> autoSubscriber = <span style="color: #0000ff;">new</span> AutoSubscriber(bus, <span style="color: #800000;">"</span><span style="color: #800000;">My_subscription_id_prefix</span><span style="color: #800000;">"</span><span style="color: #000000;">)
{
    MessageDispatcher </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> WindsorMessageDispatcher(container)
};
autoSubscriber.Subscribe(GetType().Assembly);
autoSubscriber.SubscribeAsync(GetType().Assembly);</span></pre>
</div>
<p>现在，每次收到消息时，我们的消费者的新实例都将从我们的容器中解析出来。</p>
<p>&nbsp;</p>