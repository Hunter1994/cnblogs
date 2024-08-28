<p>一、介绍</p>
<p>Orleans是一个框架，提供了一个直接的方法来构建分布式高规模计算应用程序</p>
<p>默认可扩展 -》 Orleans处理构建分布式系统的复杂性，使您的应用程序能够扩展到数百台服务器。<br />低延迟		-》	Orleans允许你在内存中保持你需要的状态，所以你的应用程序可以快速响应传入的请求。<br />简化的并发性&nbsp;-》	Orleans允许你编写简单的单线程C＃代码，处理异步消息在对象（Grains）之间传递的并发性。</p>
<p>在Orleans，Grains是应用程序代码的基石。Grains是实现一致性接口的.net类的实例。接口的异步方法用于指示Grains可以执行哪些操作</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IMyGrain : IGrainWithStringKey
{
    Task</span>&lt;<span style="color: #0000ff;">string</span>&gt; SayHello(<span style="color: #0000ff;">string</span><span style="color: #000000;"> name);
}</span></pre>
</div>
<p>这个实现是在Orleans框架内执行的：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyGrain : IMyGrain
{
    </span><span style="color: #0000ff;">public</span> Task&lt;<span style="color: #0000ff;">string</span>&gt; SayHello(<span style="color: #0000ff;">string</span><span style="color: #000000;"> name)
    {
        </span><span style="color: #0000ff;">return</span> Task.FromResult($<span style="color: #800000;">"</span><span style="color: #800000;">Hello {name}</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    }
}</span></pre>
</div>
<p>然后你可以通过获取一个代理对象（一个Grains参考）来调用grain，然后调用这些方法：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> grain = GrainClient.GrainFactory.GetGrain&lt;IMyGrain&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">grain1</span><span style="color: #800000;">"</span><span style="color: #000000;">);
</span><span style="color: #0000ff;">await</span> grain.SayHello(<span style="color: #800000;">"</span><span style="color: #800000;">World</span><span style="color: #800000;">"</span>);</pre>
</div>
<p>&nbsp;</p>
<p>二、背景</p>
<p>云应用程序和服务本质上是并行和分布式的。 他们也是互动和动态的; 通常需要近实时的云实体之间的直接交互。 这样的应用程序今天很难建立。 开发过程需要专家级程序员，并且随着工作负载的增长，通常需要昂贵的设计和体系结构迭代。</p>
<p>当今大多数高规模的属性都是作为无状态n层服务的组合而构建的，其中大部分应用程序逻辑位于中间层。</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201712/741594-20171222143308365-1916738887.png" alt="" /></p>
<p>&nbsp;</p>
<p>虽然该模型允许通过向中间层添加更多服务器来扩展，但由于大多数来自前端Web服务器的中间层请求需要来自存储的一个或多个读取，所以受到存储层的性能和可伸缩性的限制， 更新更加复杂，并且由于中间层服务器之间缺乏协调而容易发生并发问题和冲突。 通常需要无状态层中的缓存来获得可接受的性能，增加复杂性并引入缓存一致性问题。 无状态n层模型的另一个问题是，它不支持中间层公开的各个应用实体之间良好的水平通信，这使得难以实现复杂的业务逻辑，多个实体执行单独的操作，作为处理 请求。</p>
<p>&nbsp;</p>
<p>二、Orleans 作为一个有状态的中间层</p>
<p>Orleans提供了一种构建有状态中间层的直观方式，其中各种业务逻辑实体显示为分布在一组服务器中的不同应用程序定义类型的独立全局可寻址.NET对象（grains）。</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201712/741594-20171222140637256-1840000609.png" alt="" width="782" height="397" /></p>
<p>grain类型是一个简单的.NET类，它实现了一个或多个应用程序定义的grain接口。单个grain是应用程序定义的grain类的实例，它们是由Orleans运行时自动创建的，在服务器上根据需要处理这些grain的请求。grain自然映射到大多数应用程序实体，例如用户，设备，会话，库存，订单等等，这使得构建面向对象的业务逻辑变得非常容易，而在一组服务器上透明地扩展。每个grain在由其应用逻辑选择的grain类型内具有稳定的逻辑身份（密钥），例如，用户电子邮件或设备ID或库存SKU代码。 Orleans保证每个单独grain的单线程执行，从而保护应用程序逻辑免受并发和竞争的危险。在微服务领域，Orleans被用作实现微服务的框架，微服务可以由开发人员选择的微服务部署/管理解决方案进行部署和管理。</p>
<p>&nbsp;</p>
<p>三、Grain生命周期</p>
<p>grain可以在存储或内存状态或两者的组合中具有持续状态。任何grain都可以通过任何其他grain或前端（客户）通过使用目标grain的逻辑身份来调用，而不需要创建或实例化目标grain。Orleans的编程模型使grain看起来好像在整个内存中。实际上，grain从整个生命周期开始，只是存储持久状态，到在内存中被实例化，到从内存中移除</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201712/741594-20171222142629256-884871966.png" alt="" /></p>
<p>grain需要工作时，Orleans在后台实例化（激活）grain，当它们闲置太久时，将它们从内存中移除（停用）以回收硬件资源。运行时的grain生命周期管理工作对应用程序代码是透明的，将其从分布式资源管理的复杂任务中解放出来。应用程序逻辑可以用所有可用的&ldquo;地址空间&rdquo;来编写，而无需使用硬件资源来将所有的grain同时存储在内存中，这在概念上类似于虚拟内存在操作系统中的工作方式。此外，grain的虚拟属性允许Orleans处理服务器故障，这主要是透明地处理应用程序逻辑，因为在故障被检测到的情况下，在故障服务器上执行的grain会自动在集群中的其他服务器上重新实例化。</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201712/741594-20171222144610178-1485376853.png" alt="" width="698" height="345" /></p>
<p>&nbsp;</p>
<p>&nbsp;四、虚拟Actors</p>
<p>Orleans的实施是基于20世纪70年代以来的Actor 模型。然而，与Erlang或Akka等传统Actor&nbsp;系统中的Actor&nbsp;不同，Orleans grain是虚拟Actor&nbsp;。最大的不同是，grain的物理实例被完全抽象出来，并由Orleans运行时自动管理。虚拟Actor 模型更适合于像云服务这样的大规模动态工作负载，并且是Orleans的主要创新。</p>
<p>&nbsp;</p>
<p>五、Orleans的起源</p>
<p>Orleans创建于微软研究院，设计用于云计算。自2011年以来,它已被广泛地应用在云计算和前提由几个微软产品组,尤其是通过游戏工作室,如343产业和光环背后的联盟作为云服务平台和战争机器4 4/5,以及许多其他公司。</p>
<p>Orleans在2015年1月是开源的，吸引了许多开发人员，他们形成了一个最活跃的开源社区。净生态系统。在开发人员社区和微软的Orleans团队之间的积极协作中，每天都会增加和改进特性。微软的研究继续与Orleans团队合作，以带来新的主要特征，如地理分布、索引和分布式事务，这正在推动艺术的发展。对许多人来说，Orleans已经成为构建分布式系统和云服务的首选框架。网络开发者。</p>
<p>&nbsp;</p>
<p>六、优点</p>
<p>Orleans的主要优点是:开发人员的生产力，即使是非专业的程序员;在默认情况下，透明的可伸缩性（轻松实现伸缩）。我们将在下面扩展这些优点。</p>
<p>1，开发人员生产力</p>
<p>Orleans编程模型通过提供以下关键抽象，保证和系统服务，提高了专家和非专业程序员的工作效率。</p>
<ul>
<li><strong>熟悉的面向对象编程(OOP)范式。</strong>&nbsp;Actors是. net类，它使用异步方法实现声明的. net actor接口。这样，参与者就可以作为远程对象出现，而这些对象的方法可以直接调用。这为程序员提供了熟悉的OOP范式，方法是将方法调用转换为消息，将它们路由到正确的端点，调用目标参与者的方法，以完全透明的方式处理故障和角落情况。</li>
<li><strong>单线程执行的Actors。</strong>运行时保证了一个参与者一次不会在多个线程上执行。与其他参与者的隔离相结合，程序员从不在actor级别上面对并发，因此永远不需要使用锁或其他同步机制来控制对共享数据的访问。仅这一特性就使得分布式应用程序的开发成为了非专家程序员的专利。</li>
<li><strong>透明激活。</strong>运行时激活一个Actor，只是在有消息要处理时才启动。这将清晰地分离了创建引用到Actor的概念，它是由应用程序代码可见和控制的，并且在内存中对Actor进行物理激活，这对应用程序是透明的。它决定何时禁用或激活一个Actor;应用程序可以不间断地访问逻辑创建的Actor的完整&ldquo;内存空间&rdquo;，不管它们是否在特定时间点的物理内存中。透明激活能够通过在硬件资源池中放置和迁移Actor来实现动态的、自适应的负载均衡。该特性是传统Actor模型的一个显著改进，在此模型中，Actor的生存期是应用程序管理的。</li>
<li><strong>位置透明性。</strong>程序员用来调用Actor的方法或传递给其他组件的Actor引用(代理对象)只包含了Actor的逻辑标识。将Actor的逻辑标识翻译到它的物理位置和相应的消息路由是由Orleans 运行时完成的。应用程序代码与Actors进行通信，而忽略它们的物理位置，由于故障或资源管理，可能会随着时间的推移而改变，或者因为在调用时，Actor会被禁用。</li>
<li><strong>与持久性存储的透明集成。</strong>Orleans允许将Actors的内存状态的声明映射到持久性存储。它同步更新，透明地保证调用者只有在持久状态成功更新后才会收到结果。扩展和/或自定义现有的持久存储提供程序集是直接的。</li>
<li><strong>错误自动传播。</strong>运行时通过异步和分布式的try / catch的语义自动将未处理的错误向上传递到调用链中。因此，错误不会在应用程序中丢失。这允许程序员在适当的地方放置错误处理逻辑，而不需要在每个层次上手工传播错误。&nbsp;</li>
</ul>
<p>2，默认的透明可伸缩性</p>
<p>Orleans编程模型旨在指导程序员通过几个数量级来扩展他们的应用程序或服务。这是通过结合已被证明的最佳实践和模式来完成的，并提供了较低级别系统功能的有效实现。下面是一些关键的因素，它们支持可伸缩性和性能。&nbsp;</p>
<ul>
<li><strong>应用状态的隐式grain分区。</strong>通过将Actors作为直接可寻址的实体，程序员将隐式地破坏其应用程序的整体状态。虽然Orleans编程模型没有规定Actor的大小，在大多数情况下是有意义有一个相对大量的actors&mdash;&mdash;百万甚至更多&mdash;&mdash;应用程序的每个代表一个自然实体,如用户帐户,一个购买订单,等。Actors是单独可寻址和他们的物理位置抽象的运行时,Orleans在平衡负载和以透明和通用的方式处理热点问题方面具有极大的灵活性，无需任何应用程序开发人员的考虑。</li>
<li><strong>自适应资源管理。</strong>与Actors作任何假设本地其他Actors他们相互作用,由于位置透明性,运行时可以管理和调整可用HW资源配置在一个非常动态的方式通过细grain决定位置/ Actors迁移反应的计算集群负载和交流模式没有失败传入的请求。通过创建特定actor的多个副本，运行时可以在必要时增加Actor的吞吐量，而无需对应用程序代码进行任何更改。</li>
<li><strong>多路复用通信。</strong>Orleans 的Actors 有逻辑端点，它们之间的消息传递是通过一组固定的全部物理连接(TCP套接字)进行复用的。这允许运行时在每个actor中承载一个非常大的(数百万)可寻址的实体。此外，actor的激活/注销不需要注册/取消物理端点的注册，例如TCP端口或HTTP URL，甚至关闭TCP连接。</li>
<li><strong>有效的调度。</strong>运行时调度大量单线程的Actors在一个自定义线程池中执行，每个线程池都有一个物理处理器内核。以非阻塞延续的方式编写的Actor代码(对Orleans 编程模型的需求)应用程序代码以非常高效的&ldquo;协作&rdquo;的多线程方式运行，并且没有争用。这使得系统能够达到很高的吞吐量，并在非常高的CPU利用率(高达90%以上)的情况下运行，并具有很大的稳定性。事实上，系统中Actors的数量增长和负载不会导致额外的线程或其他OS原语帮助单个节点和整个系统的可伸缩性。（在操作系统中叫原语,是执行过程中不可被打断的基本操作,你可以理解为一段代码,这段代码在执行过程中不能被打断）</li>
<li><strong>显式异步。</strong>Orleans编程模型使分布式应用程序的异步性质更加明确，并指导程序员编写非阻塞异步代码。与异步消息传递和高效调度相结合，这使得在没有显式使用多线程的情况下实现了大量的分布式并行性和总体吞吐量。</li>
</ul>
<p>&nbsp;</p>