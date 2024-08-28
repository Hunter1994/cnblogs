<p>EasyNetQ是一个由小型组件组成的库。 当你写：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> bus = RabbitHutch.CreateBus(<span style="color: #800000;">"</span><span style="color: #800000;">host=localhost</span><span style="color: #800000;">"</span>);</pre>
</div>
<p>...静态方法CreateBus使用一个微小的内部IoC容器来组装这些组件。 CreateBus方法的重载允许您访问组件注册，以便您可以提供您自己的任何EasyNetQ依赖关系的版本。 签名看起来像这样：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> IBus CreateBus(<span style="color: #0000ff;">string</span> connectionString, Action&lt;IServiceRegister&gt; registerServices)</pre>
</div>
<p>IServiceRegister接口提供了一种方法：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IServiceRegister
{
    IServiceRegister Register</span>&lt;TService&gt;(Func&lt;IServiceProvider, TService&gt; serviceCreator) <span style="color: #0000ff;">where</span> TService : <span style="color: #0000ff;">class</span><span style="color: #000000;">;
}</span></pre>
</div>
<p>因此，要基于IEasyNetQLogger注册您自己的记录器，您需要编写以下代码：</p>
<div class="cnblogs_code">
<pre>IEasyNetQLogger logger = <span style="color: #0000ff;">new</span> MyLogger(); <span style="color: #008000;">//</span><span style="color: #008000;"> note the use of IEasyNetQLogger not var.</span>
<span style="color: #0000ff;">var</span> bus =<span style="color: #000000;"> RabbitHutch.CreateBus(connectionString, 
    serviceRegister </span>=&gt; serviceRegister.Register(serviceProvider =&gt; logger));</pre>
</div>
<p>Register方法的参数Func &lt;IServiceProvider，TService&gt;是一个函数，它在CreateBus将这些组件拉到一起以生成一个IBus实例时运行。 IServiceProvider看起来像这样：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IServiceProvider
{
    TService Resolve</span>&lt;TService&gt;() <span style="color: #0000ff;">where</span> TService : <span style="color: #0000ff;">class</span><span style="color: #000000;">;
}</span></pre>
</div>
<p>这使您可以访问EasyNetQ提供的其他服务。 例如，如果您想用您自己的ISerializer实现来替换默认的序列化程序，并且想要通过引用记录器来构建它，则可以这样做：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> bus = RabbitHutch.CreateBus(connectionString, serviceRegister =&gt;<span style="color: #000000;"> 
    serviceRegister.Register</span>&lt;ISerializer&gt;<span style="color: #000000;">(
    serviceProvider </span>=&gt; <span style="color: #0000ff;">new</span> MySerializer(serviceProvider.Resolve&lt;IEasyNetQLogger&gt;())));</pre>
</div>
<p>请注意，我们必须在Register方法上使用明确的类型参数，以便内部IoC容器知道我们正在替换哪个服务。</p>
<p>要查看组成IBus实例的组件的完整列表，以及它们的组装方式，请查看ComponentRegistration类。</p>
<p>您可以通过IAdvancedBus的Container属性访问容器。 这使您可以访问内部组件：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> serializer = bus.Advanced.Container.Resolve&lt;ISerializer&gt;();</pre>
</div>
<p>要用您自己选择的IoC容器替换内部容器，请参阅使用替代DI容器</p>
<p>&nbsp;</p>