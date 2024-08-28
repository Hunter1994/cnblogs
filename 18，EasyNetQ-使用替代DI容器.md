<p>EasyNetQ由独立组件组成。 它在内部使用称为DefaultServiceProvider的小型内部DI（IoC）容器。 如果您查看用于创建核心IBus接口实例的静态RabbitHutch类的代码，您将看到它仅创建一个新的DefaultServiceProvider，注册所有EasyNetQ组件，然后调用container.Resolve（）创建一个 IBus的新实例及其由容器提供的依赖关系树：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> IBus CreateBus(IConnectionConfiguration connectionConfiguration, Action&lt;IServiceRegister&gt;<span style="color: #000000;"> registerServices)
{
    Preconditions.CheckNotNull(connectionConfiguration, </span><span style="color: #800000;">"</span><span style="color: #800000;">connectionConfiguration</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    Preconditions.CheckNotNull(registerServices, </span><span style="color: #800000;">"</span><span style="color: #800000;">registerServices</span><span style="color: #800000;">"</span><span style="color: #000000;">);

    </span><span style="color: #0000ff;">var</span> container =<span style="color: #000000;"> createContainerInternal();
    </span><span style="color: #0000ff;">if</span> (container == <span style="color: #0000ff;">null</span><span style="color: #000000;">)
    {
        </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> EasyNetQException(<span style="color: #800000;">"</span><span style="color: #800000;">Could not create container. </span><span style="color: #800000;">"</span> + 
            <span style="color: #800000;">"</span><span style="color: #800000;">Have you called SetContainerFactory(...) with a function that returns null?</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    }

    registerServices(container);
    container.Register(_ </span>=&gt;<span style="color: #000000;"> connectionConfiguration);
    ComponentRegistration.RegisterServices(container);

    </span><span style="color: #0000ff;">return</span> container.Resolve&lt;IBus&gt;<span style="color: #000000;">();
}</span></pre>
</div>
<p>但是如果你想让EasyNetQ使用你选择的容器呢？ 从版本0.25开始，RabbitHutch类提供了一个静态方法SetContainerFactory，它允许您注册一个替代的容器工厂方法，该方法提供您所关心的EasyNetQ.IContainer的任何实现。</p>
<p>Jeff Doolittle在这里为Windsor和Structure Map创建了容器包装：<a href="https://github.com/jeffdoolittle/EasyNetQ.DI">https://github.com/jeffdoolittle/EasyNetQ.DI</a></p>
<p>在这个例子中，我们使用Castle Windsor IoC容器：</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">注册我们的替代容器工厂</span>
RabbitHutch.SetContainerFactory(() =&gt;<span style="color: #000000;">
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;">创建一个Windsor的实例</span>
        <span style="color: #0000ff;">var</span> windsorContainer = <span style="color: #0000ff;">new</span><span style="color: #000000;"> WindsorContainer();

        </span><span style="color: #008000;">//</span><span style="color: #008000;">将它包装在EasyNetQ.IContainer的实现中</span>
        <span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> WindsorContainerWrapper(windsorContainer);
    });

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 现在我们可以创建一个IBus实例，但它是从windsor解决的，而不是EasyNetQ的默认服务提供者。</span>
<span style="color: #0000ff;">var</span> bus = RabbitHutch.CreateBus(<span style="color: #800000;">"</span><span style="color: #800000;">host=localhost</span><span style="color: #800000;">"</span>);</pre>
</div>
<p>这里是WindsorContainerWrapper：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> WindsorContainerWrapper : IContainer, IDisposable
{
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> IWindsorContainer windsorContainer;

    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> WindsorContainerWrapper(IWindsorContainer windsorContainer)
    {
        </span><span style="color: #0000ff;">this</span>.windsorContainer =<span style="color: #000000;"> windsorContainer;
    }

    </span><span style="color: #0000ff;">public</span> TService Resolve&lt;TService&gt;() <span style="color: #0000ff;">where</span> TService : <span style="color: #0000ff;">class</span><span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">return</span> windsorContainer.Resolve&lt;TService&gt;<span style="color: #000000;">();
    }

    </span><span style="color: #0000ff;">public</span> IServiceRegister Register&lt;TService&gt;(System.Func&lt;IServiceProvider, TService&gt;<span style="color: #000000;"> serviceCreator) 
        </span><span style="color: #0000ff;">where</span> TService : <span style="color: #0000ff;">class</span><span style="color: #000000;">
    {
        windsorContainer.Register(
            Component.For</span>&lt;TService&gt;().UsingFactoryMethod(() =&gt; serviceCreator(<span style="color: #0000ff;">this</span><span style="color: #000000;">)).LifeStyle.Singleton
            );
        </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">this</span><span style="color: #000000;">;
    }

    </span><span style="color: #0000ff;">public</span> IServiceRegister Register&lt;TService, TImplementation&gt;<span style="color: #000000;">() 
        </span><span style="color: #0000ff;">where</span> TService : <span style="color: #0000ff;">class</span> 
        <span style="color: #0000ff;">where</span> TImplementation : <span style="color: #0000ff;">class</span><span style="color: #000000;">, TService
    {
        windsorContainer.Register(
            Component.For</span>&lt;TService&gt;().ImplementedBy&lt;TImplementation&gt;<span style="color: #000000;">().LifeStyle.Singleton
            );
        </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">this</span><span style="color: #000000;">;
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Dispose()
    {
        windsorContainer.Dispose();
    }
}</span></pre>
</div>
<p>请注意，所有EasyNetQ服务都应注册为singletons。</p>
<p>正确处理Windsor是非常重要的。 EasyNetQ不会在IContainer上提供Dispose方法，但您可以通过高级总线访问容器（是的，这也是新的），并以这种方式处置windsor：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">((WindsorContainerWrapper)bus.Advanced.Container).Dispose();
bus.Dispose();</span></pre>
</div>
<p>&nbsp;</p>