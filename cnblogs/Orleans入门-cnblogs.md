<p><a href="#a1"><strong>一、Grains</strong></a></p>
<p><strong><strong><a href="#a2">二、开发一个Grain</a></strong></strong></p>
<p><a href="#a3"><strong>三、开发一个客户端</strong></a></p>
<p><a href="#a4"><strong>四、运行应用程序</strong></a></p>
<p><a href="#a5"><strong>五、调式</strong></a></p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a1"></a>一、Grains</span></strong></span></p>
<p>Grains是Orleans编程模型的关键原语。 Grains是Orleans应用程序的构建块，它们是隔离，分配和持久性的原子单元。 Grains是表示应用程序实体的对象。 就像在经典的面向对象编程（Object Oriented Programming）中一样，grain封装实体的状态并在代码逻辑中对其行为进行编码。 Grains可以持有对方的引用，并通过调用通过接口公开的对方的方法进行交互。</p>
<p><span style="font-size: 12px; color: #ff0000;">注意：在操作系统中叫原语，是执行过程中不可被打断的基本操作，你可以理解为一段代码，这段代码在执行过程中不能被打断(在多道程序设计里进程间相互切换，还可能有中断发生，经常会被打断)。像原子一样具有不可分割的特性, 所以叫原语, 像原子一样的语句</span></p>
<p>Orleans的目标是大大简化构建可扩展的应用程序，并消除大部分的并发挑战</p>
<ul>
<li>除了通过消息传递之外，不在grains实例之间共享数据。</li>
<li>通过提供单线程执行保证每个单独的grain。</li>
</ul>
<p>典型的grain封装单个实体（例如特定用户或设备或会话）的状态和行为。</p>
<p>1，Grain身份</p>
<p>个体grain是grain类型（类）的一个唯一寻址实例。 每个grain在其类型中都有一个唯一的标识，也被称为grain键。 其类型中的Grain标识可以是一个长整型，一个GUID，一个字符串，或者一个长+字符串或GUID +字符串的组合。&nbsp;&nbsp;</p>
<p>2，访问Grain</p>
<p>grain类实现一个或多个grain接口，与这种类型的grain进行交互的形式代码契约。 为了调用grain，调用者需要知道grain类实现的grain接口，包括调用者想要调用的方法和目标grain的唯一标识（关键字）。 例如，以下是如何使用用户配置文件grain来更新用户的地址，如果电子邮件用作用户身份。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> user = grainFactory.GetGrain&lt;IUserProfile&gt;<span style="color: #000000;">(userEmail);
</span><span style="color: #0000ff;">await</span> user.UpdateAddress(newAddress);</pre>
</div>
<p>调用GetGrain是一个廉价的本地操作，构建一个具有嵌入标识和目标grain类型的grain参考。</p>
<p>注意，不需要创建或实例化目标grain。我们调用它来更新用户的地址，就好像用户的grain已经为我们实例化了一样。这是奥尔良编程模型最大的优点之一&mdash;&mdash;我们从不需要创建、实例化或删除grains。我们可以编写代码，就像所有可能的grains一样，例如数百万的用户配置文件，总是在内存中等待我们调用它们。在幕后，Orleans运行时执行所有繁重的管理资源，透明地将grains带到内存中。</p>
<p>3，幕后 - Grain生命周期</p>
<p>Grains居住在称为仓储的执行容器中。 仓储形成了一个集多个物理或虚拟机资源的集群。 当工作（请求）grain时，Orleans确保在群集中的一个仓储中有一个grain实例。 如果任何仓储上没有grain实例，则Orleans运行时创建一个。 这个过程被称为激活。 在grain使用Grain持久性的情况下，运行时会在激活时自动从后备存储中读取状态。</p>
<p>在仓储上激活后，grain会处理来自其他grain或群集外（通常来自前端Web服务器）的传入请求（方法调用）。 在处理请求的过程中，grain可能会调用其他grain或一些外部服务。 如果grain停止接收请求并保持空闲状态，在可配置的不活动时间段之后，Orleans从内存中删除grain（取消激活）以释放其他grains的资源。 如果当有新的请求时，奥尔良会再次激活它，可能在不同的仓储，所以调用者得到的印象是，gran一直留在内存中。 grain从存在的整个生命周期开始，只有存储器中的持久化状态（如果有的话）在内存中被实例化，才能从内存中移除。</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201712/741594-20171222180116803-2122662936.png" alt="" /></p>
<p>Orleans控制透明地激活和停用Grains的过程。 编码谷物时，开发者认为所有Grains总是被激活。</p>
<p>Grain生命周期中关键事件的顺序如下所示。</p>
<ul>
<li>另一个Grain或客户端调用Grain的方法（通过Grain参考）</li>
<li>grain被激活（如果它还没有在集群中的某个地方被激活），并创建一个grain类的实例，称为grain激活<br />
<ul>
<li>如果适用的话，grain的构造者是利用依赖注入来执行的</li>
<li>如果使用声明性持久性，则从存储中读取grain状态</li>
<li>如果重写，则调用OnActivateAsync</li>














</ul>














</li>
<li>grain处理传入的请求</li>
<li>grain保持闲置一段时间</li>
<li>仓储运行时间决定停用grain</li>
<li>仓储运行时调用OnDeactivateAsync，如果重写</li>
<li>仓储运行时间从内存中删除grain</li>














</ul>
<p>一个仓储的正常关闭后，所有的grain激活它停止。 任何等待在grain队列中处理的请求都会被转发到集群中的其他仓储，在那里根据需要创建停用的grain的新激活。 如果一个仓储关闭或死亡失败，集群中的其他仓储检测到失败，并开始创建失败的仓储上丢失的新的激活，因为这些grain的新的请求到达。 请注意，检测仓储故障需要一些时间（可配置），因此重新激活丢失谷物的过程不是即时的。</p>
<p>&nbsp;</p>
<p>4，Grain执行</p>
<p>grain激活在块中执行工作，并在每个块执行到下一段之前完成。大量的工作内容包括了对其他grains或外部客户的请求的方法调用，以及在完成前一段时间的关闭计划。与一大块工作相对应的基本执行单位称为turn。</p>
<p>虽然Orleans可能会执行很多次并行的不同激活，但每次激活都将一次执行一次。这意味着不需要使用锁或其他同步方法来防止数据竞争和其他多线程危害。&nbsp;</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a2"></a>二、开发一个Grain</span></strong></span></p>
<p>1，设置</p>
<p>在编写代码来实现Grain类之前，在Visual Studio中创建一个新的以.NET 4.6.1或更高版本为目标的类库项目，并向其中添加&nbsp;<span class="cnblogs_code">Microsoft.Orleans.OrleansCodeGenerator.Build</span>&nbsp; NuGet包。</p>
<div class="cnblogs_code">
<pre>PM&gt; Install-Package Microsoft.Orleans.OrleansCodeGenerator.Build</pre>
</div>
<p>2，Grain接口和类</p>
<p>Grain彼此交互，并通过调用声明为各自的Grain接口的一部分方法从外部被调用。 Grain类实现一个或多个先前声明的Grain接口。 Grains接口的所有方法必须返回一个Task（对于void方法）或Task &lt;T&gt;（对于返回类型T的值的方法）。</p>
<p>以下是Presence Service示例的摘录：</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">一个Grain界面的例子</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IPlayerGrain : IGrainWithGuidKey
{
  Task</span>&lt;IGameGrain&gt;<span style="color: #000000;"> GetCurrentGame();
  Task JoinGame(IGameGrain game);
  Task LeaveGame(IGameGrain game);
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">一个Grain类实现Grain接口的例子</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> PlayerGrain : Grain, IPlayerGrain
{
    </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> IGameGrain currentGame;

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 玩家目前所在的游戏。可能为空。</span>
    <span style="color: #0000ff;">public</span> Task&lt;IGameGrain&gt;<span style="color: #000000;"> GetCurrentGame()
    {
       </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> Task.FromResult(currentGame);
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">游戏谷歌调用此方法通知玩家已加入游戏。</span>
    <span style="color: #0000ff;">public</span><span style="color: #000000;"> Task JoinGame(IGameGrain game)
    {
       currentGame </span>=<span style="color: #000000;"> game;
       Console.WriteLine(
           </span><span style="color: #800000;">"</span><span style="color: #800000;">Player {0} joined game {1}</span><span style="color: #800000;">"</span><span style="color: #000000;">, 
           </span><span style="color: #0000ff;">this</span><span style="color: #000000;">.GetPrimaryKey(),
           game.GetPrimaryKey());

       </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> Task.CompletedTask;
    }

   </span><span style="color: #008000;">//</span><span style="color: #008000;">游戏谷歌称这种方法通知玩家已经离开游戏。</span>
   <span style="color: #0000ff;">public</span><span style="color: #000000;"> Task LeaveGame(IGameGrain game)
   {
       currentGame </span>= <span style="color: #0000ff;">null</span><span style="color: #000000;">;
       Console.WriteLine(
           </span><span style="color: #800000;">"</span><span style="color: #800000;">Player {0} left game {1}</span><span style="color: #800000;">"</span><span style="color: #000000;">,
           </span><span style="color: #0000ff;">this</span><span style="color: #000000;">.GetPrimaryKey(),
           game.GetPrimaryKey());

       </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> Task.CompletedTask;
   }
}</span></pre>
</div>
<p>3，从Grains方法返回值</p>
<p>返回类型T值的grain方法在grain接口中定义为返回Task &lt;T&gt;。 对于未使用async关键字标记的grain方法，当返回值可用时，通常通过以下语句返回：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> Task&lt;SomeType&gt;<span style="color: #000000;"> GrainMethod1()
{
    ...
    </span><span style="color: #0000ff;">return</span> Task.FromResult(&lt;variable or constant with result&gt;<span style="color: #000000;">);
}</span></pre>
</div>
<p>一个没有返回值的grain方法，实际上是一个void方法，在grain接口中被定义为返回Task。 返回的Task表示异步执行和方法的完成。 对于没有用async关键字标记的grain方法，当&ldquo;void&rdquo;方法完成它的执行时，它需要返回Task.CompletedTask的特殊值：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span><span style="color: #000000;"> Task GrainMethod2()
{
    ...
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> Task.CompletedTask;
}</span></pre>
</div>
<p>标记为async的grain方法直接返回值：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task&lt;SomeType&gt;<span style="color: #000000;"> GrainMethod3()
{
    ...
    </span><span style="color: #0000ff;">return</span> &lt;variable or constant with result&gt;<span style="color: #000000;">;
}</span></pre>
</div>
<p>标记为async的&ldquo;void&rdquo;grain方法不返回任何值，只是在执行结束时返回：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span><span style="color: #000000;"> Task GrainMethod4()
{
    ...
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;">;
}</span></pre>
</div>
<p>如果一个grain方法从另一个异步方法调用接收到返回值，并且不需要执行该调用的错误处理，那么它可以简单地将它从该异步调用接收的Task作为返回值返回：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> Task&lt;SomeType&gt;<span style="color: #000000;"> GrainMethod5()
{
    ...
    Task</span>&lt;SomeType&gt; task =<span style="color: #000000;"> CallToAnotherGrain();
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> task;
}</span></pre>
</div>
<p>类似地，&ldquo;void&rdquo;grain方法可以返回一个Task，而不是等待它，而是通过另一个调用返回给它。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span><span style="color: #000000;"> Task GrainMethod6()
{
    ...
    Task task </span>=<span style="color: #000000;"> CallToAsyncAPI();
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> task;
}</span></pre>
</div>
<p>4，Grain引用</p>
<p>Grain引用是一个代理对象，它实现与相应的grain类相同的grain接口。 它封装了目标grain的逻辑标识（类型和唯一键）。 Grain引用是用来调用目标Grain的。 每个Grain引用都是针对一个Grain（Grain类的单个实例），但是可以为同一个Grain创建多个独立的引用。</p>
<p>由于Grain引用代表目标Grain的逻辑身份，它独立于Grain的物理位置，并且即使在系统完全重新启动之后也保持有效。 开发人员可以像使用其他.NET对象一样使用Grain引用。 它可以传递给一个方法，用作方法的返回值等等，甚至保存到持久存储中。</p>
<p>通过将Grain身份传递给GrainFactory.GetGrain &lt;T&gt;（key）方法，可以获得Grain引用，其中T是Grain接口，而键是类型内Grain的唯一键。</p>
<p>以下是如何获取上面定义的IPlayerGrain接口的Grain引用的示例。</p>
<p>①从Grain里面使用的方式：</p>
<div class="cnblogs_code">
<pre>    <span style="color: #008000;">//</span><span style="color: #008000;">构建特定玩家的Grain引用</span>
    IPlayerGrain player = GrainFactory.GetGrain&lt;IPlayerGrain&gt;(playerId);</pre>
</div>
<p>②从Orleans客户端代理里面使用的方式</p>
<p>在1.5.0版本之前：&nbsp;<span class="cnblogs_code">IPlayerGrain player = GrainClient.GrainFactory.GetGrain&lt;IPlayerGrain&gt;(playerId);</span>&nbsp;</p>
<p>自1.5.0版本之后：&nbsp;<span class="cnblogs_code">IPlayerGrain player = client.GetGrain&lt;IPlayerGrain&gt;(playerId);</span>&nbsp;</p>
<p>5，Grain方法调用</p>
<p>Orleans编程模型基于Async和Await异步编程。</p>
<p>使用前面例子中的Grain引用，下面是一个如何执行Grain方法调用：</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">异步调用grain方法</span>
Task joinGameTask = player.JoinGame(<span style="color: #0000ff;">this</span><span style="color: #000000;">);
</span><span style="color: #008000;">//</span><span style="color: #008000;">await关键字有效地使方法的其余部分在稍后的时间点（在等待完成的任务完成时）异步执行，而不会阻塞线程。</span>
<span style="color: #0000ff;">await</span><span style="color: #000000;"> joinGameTask;
</span><span style="color: #008000;">//</span><span style="color: #008000;">joinGameTask完成后，下一行将执行。</span>
players.Add(playerId);</pre>
</div>
<p>可以加入两个或多个任务; 连接操作将创建一个新的&ldquo;任务&rdquo;，该任务在其所有组成任务完成时解决。 当Grain需要启动多个计算并等待所有的计算完成之前，这是一个有用的模式。 例如，生成由多个部分组成的网页的前端页面可能会进行多个后端调用，每个部分一个，并为每个结果接收一个任务。 Grain将等待所有这些任务的加入; 当加入任务被解决时，单独的任务已经完成，并且已经接收到格式化网页所需的所有数据。</p>
<p>例子：</p>
<div class="cnblogs_code">
<pre>List&lt;Task&gt; tasks = <span style="color: #0000ff;">new</span> List&lt;Task&gt;<span style="color: #000000;">();
Message notification </span>=<span style="color: #000000;"> CreateNewMessage(text);

</span><span style="color: #0000ff;">foreach</span> (ISubscriber subscriber <span style="color: #0000ff;">in</span><span style="color: #000000;"> subscribers)
{
   tasks.Add(subscriber.Notify(notification));
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> WhenAll加入一个任务集合，并返回一个联合任务，将解决所有单个通知任务时将解决。</span>
Task joinedTask =<span style="color: #000000;"> Task.WhenAll(tasks);
</span><span style="color: #0000ff;">await</span><span style="color: #000000;"> joinedTask;

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 方法的其余部分的执行将在joinedTask解析后继续异步执行。</span></pre>
</div>
<p>6，虚方法</p>
<p>一个Grain类可以选择重写OnActivateAsync和OnDeactivateAsync虚拟方法，这些方法被Orleans的运行时激活和取消激活时调用。这让Grain代码有机会进行额外的初始化和清理工作。OnActivateAsync引发的异常会使激活过程失败。虽然OnActivateAsync(如果被重写)总是被称为Grain激活过程的一部分，OnDeactivateAsync不能保证在所有情况下都被调用，例如，在服务器故障或其他异常事件时。因此，应用程序不应该依赖OnDeactivateAsync来执行关键操作，例如状态更改的持久性，只能用于最佳操作。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a3"></a>三、开发一个客户端</span></strong></span></p>
<p>1，什么是Grain客户端？</p>
<p>术语&ldquo;客户端&rdquo;或有时&ldquo;Grain客户端&rdquo;用于与Grains相互作用的应用代码，但其本身不是Grain逻辑的一部分。 客户端代码运行在托管Grains的称为仓储的Orleans服务器群集之外。 因此，客户作为连接器或通往集群和应用程序的所有Grains的通道。</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201712/741594-20171223144751115-1688359638.png" alt="" width="508" height="364" /></p>
<p>通常，前端Web服务器上使用客户端连接到作为中间层的Orleans群集，并执行业务逻辑。 在典型的设置中，前端Web服务器：</p>
<ul>
<li>接收Web请求</li>
<li>执行必要的身份验证和授权验证</li>
<li>决定哪些Grain(s)应该处理请求</li>
<li>使用Grain Client对Grain(s)进行一个或多个方法调用</li>
<li>处理Grain调用的成功完成或失败以及任何返回的值</li>
<li>发送Web请求的响应</li>
</ul>
<p>&nbsp;2，Grain Client的初始化</p>
<p>在Grain客户端可以用于调用Orleans集群托管的Grain之前，需要对Grain客户端进行配置，初始化和连接到集群。</p>
<p>通过ClientConfiguration对象提供配置，该对象包含用于以编程方式配置客户端的配置属性层次结构。 还有一种方法可以通过XML文件来配置客户端，但该选项将来会被弃用。 更多信息在&ldquo;客户端配置&rdquo;指南中。 在这里，我们将简单地使用一个帮助器方法来创建一个硬编码的配置对象，用于连接到作为本地主机运行的本地仓储</p>
<div class="cnblogs_code">
<pre>ClientConfiguration clientConfig = ClientConfiguration.LocalhostSilo(); </pre>
</div>
<p>一旦我们有了一个配置对象，我们可以通过ClientBuilder类建立一个客户端。</p>
<div class="cnblogs_code">
<pre>IClusterClient client = <span style="color: #0000ff;">new</span> ClientBuilder().UseConfiguration(clientConfig).Build();</pre>
</div>
<p>最后，我们需要在构建的客户端对象上调用Connect()方法，使其连接到Orleans集群。 这是一个返回任务的异步方法。 所以我们需要等待完成，等待或者.Wait()</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">await</span> client.Connect(); </pre>
</div>
<p>3，调用Grains</p>
<p>从客户端调用Grain与从Grain代码中进行这种调用确实没有区别。 在这两种情况下，使用相同的GetGrain &lt;T&gt;(key)方法（其中T是目标Grain接口）来获取Grain引用。 微小的差异在于通过我们调用GetGrain的工厂对象。 在客户端代码中，我们通过连接的客户端对象来实现。</p>
<div class="cnblogs_code">
<pre>IPlayerGrain player = client.GetGrain&lt;IPlayerGrain&gt;<span style="color: #000000;">(playerId);
Task t </span>=<span style="color: #000000;"> player.JoinGame(game)
</span><span style="color: #0000ff;">await</span> t;</pre>
</div>
<p>对grain方法的调用返回一个<span style="background-color: #ffff99; color: #ff6600;">Task</span>或<span style="background-color: #ffff99; color: #ff6600;">Task &lt;T&gt;</span>，按照grain接口规则的要求。 客户端可以使用await关键字异步等待返回的<span style="background-color: #ffff99; color: #ff6600;">Task</span>而不阻塞线程，或者在某些情况下用<span style="background-color: #ffff99; color: #ff6600;">Wait()</span>方法阻塞当前的执行线程。</p>
<p>从客户端代码和其他Grain中调用Grain的主要区别在于Grain的单线程执行模式。 Grain被Orleans运行时限制为单线程，而客户端可能是多线程的。 Orleans并没有在客户端提供任何这样的保证，所以客户可以使用任何适合其环境的同步结构（锁，事件，任务等）来管理自己的并发。</p>
<p>4，接收通知</p>
<p>有些情况下，一个简单的请求 - 响应模式是不够的，客户端需要接收异步通知。 例如，用户可能希望在她正在关注的人发布新消息时收到通知。</p>
<p>观察者就是这样一种机制，可以将客户端对象暴露为Gtains目标以被Grain调用。对观察者的调用不提供任何成功或失败的指示，因为它们被发送为单向的最佳工作消息。因此，在必要的地方，应用程序代码负责在观察者之上构建更高级别的可靠性机制。</p>
<p>另一种可用于向客户端传递异步消息的机制是Streams。 数据流暴露了单个消息传递成功或失败的迹象，从而使可靠的通信回到客户端。</p>
<p>5，例子：</p>
<p>这是上面给出的客户端应用程序的一个扩展版本，连接到Orleans，查找玩家帐户，订阅游戏会话的更新（玩家是观察者的一部分），并打印出通知，直到手动终止程序。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PlayerWatcher
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
        <span style="color: #808080;">///</span><span style="color: #008000;"> 模拟连接到特定玩家当前所参与的游戏的同伴应用程序，并订阅接收关于其进度的实时通知。.
        </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
        <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            RunWatcher().Wait();
            </span><span style="color: #008000;">//</span><span style="color: #008000;">阻塞主线程，以便进程不退出。更新到达线程池线程。</span>
<span style="color: #000000;">            Console.ReadLine();
        }

        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">async</span><span style="color: #000000;"> Task RunWatcher()
        {
            </span><span style="color: #0000ff;">try</span><span style="color: #000000;">

            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;"> 连接到本地仓储</span>
                <span style="color: #0000ff;">var</span> config =<span style="color: #000000;"> ClientConfiguration.LocalhostSilo();
                </span><span style="color: #0000ff;">var</span> client = <span style="color: #0000ff;">new</span><span style="color: #000000;"> ClientBuilder().UseConfiguration(config).Build();
                </span><span style="color: #0000ff;">await</span><span style="color: #000000;"> client.Connect();

                </span><span style="color: #008000;">//</span><span style="color: #008000;"> 硬编码的玩家ID</span>
                Guid playerId = <span style="color: #0000ff;">new</span> Guid(<span style="color: #800000;">"</span><span style="color: #800000;">{2349992C-860A-4EDA-9590-000000000006}</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                IPlayerGrain player </span>= client.GetGrain&lt;IPlayerGrain&gt;<span style="color: #000000;">(playerId);
                IGameGrain game </span>= <span style="color: #0000ff;">null</span><span style="color: #000000;">;

                </span><span style="color: #0000ff;">while</span> (game == <span style="color: #0000ff;">null</span><span style="color: #000000;">)
                {
                    Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">为玩家准备当前的游戏 {0}...</span><span style="color: #800000;">"</span><span style="color: #000000;">, playerId);

                    </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
                    {
                        game </span>= <span style="color: #0000ff;">await</span><span style="color: #000000;"> player.GetCurrentGame();
                        </span><span style="color: #0000ff;">if</span> (game == <span style="color: #0000ff;">null</span>) <span style="color: #008000;">//</span><span style="color: #008000;"> 等待玩家加入游戏</span>
<span style="color: #000000;">                        {
                            </span><span style="color: #0000ff;">await</span> Task.Delay(<span style="color: #800080;">5000</span><span style="color: #000000;">);
                        }
                    }
                    </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (Exception exc)
                    {
                        Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">Exception: </span><span style="color: #800000;">"</span><span style="color: #000000;">, exc.GetBaseException());
                    }
                }

                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">订阅更新游戏 {0}...</span><span style="color: #800000;">"</span><span style="color: #000000;">, game.GetPrimaryKey());

                </span><span style="color: #008000;">//</span><span style="color: #008000;"> 订阅的更新</span>
                <span style="color: #0000ff;">var</span> watcher = <span style="color: #0000ff;">new</span><span style="color: #000000;"> GameObserver();
                </span><span style="color: #0000ff;">await</span><span style="color: #000000;"> game.SubscribeForGameUpdates(
                    </span><span style="color: #0000ff;">await</span> client.CreateObjectReference&lt;IGameObserver&gt;<span style="color: #000000;">(watcher));

                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">成功订阅。按&lt;输入&gt;停止。</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }
            </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (Exception exc)
            {
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">意想不到的错误: {0}</span><span style="color: #800000;">"</span><span style="color: #000000;">, exc.GetBaseException());
            }
        }
    }

    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
    <span style="color: #808080;">///</span><span style="color: #008000;">实现Observer接口的Observer类。 需要将Grain引用传递给此类的实例以订阅更新。
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
    <span style="color: #0000ff;">class</span><span style="color: #000000;"> GameObserver : IGameObserver
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 接收更新</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> UpdateGameScore(<span style="color: #0000ff;">string</span><span style="color: #000000;"> score)
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">New game score: {0}</span><span style="color: #800000;">"</span><span style="color: #000000;">, score);
        }
    }
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a4"></a>四、运行应用程序</span></strong></span></p>
<p>1，Orleans应用</p>
<p>如上一个主题所述，一个典型的Orleans应用程序由Grains所在的一组服务器进程（仓储）和一组客户进程（通常是Web服务器）组成，这些客户进程接收外部请求，将其转换为Grain方法调用，以及 返回结果。 因此，运行Orleans应用程序需要做的第一件事就是启动一个仓储群。 出于测试目的，群集可以由单个仓储组成。 为了实现可靠的生产部署，我们显然希望集群中有多个仓储用于容错和扩展。</p>
<p>集群运行后，我们可以启动一个或多个连接到集群的客户端进程，并可以向Grains发送请求。 客户端连接到仓储网关上的特殊TCP端点。 默认情况下，群集中的每个仓储都启用了客户端网关。 因此，客户可以并行连接到所有仓储，以获得更好的性能和弹性。</p>
<p>2，配置和启动仓储</p>
<p>一个仓储通过一个ClusterConfiguration对象以编程方式进行配置。 它可以被实例化和直接填充，从一个文件加载设置，或者为不同的部署环境使用几个可用的帮助器方法创建。 对于本地测试，最简单的方法是使用ClusterConfiguration.LocalhostPrimarySilo()辅助方法。 然后将配置对象传递给SiloHost类的新实例，可以在此之后进行初始化和启动。</p>
<p>您可以创建一个空的控制台应用程序项目，以.NET Framework 4.6.1或更高版本为主机。 将Microsoft.Orleans.Server NuGet元数据包添加到项目。</p>
<div class="cnblogs_code">
<pre>PM&gt; Install-Package Microsoft.Orleans.Server</pre>
</div>
<p>下面是一个如何开始本地仓储的例子：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> siloConfig =<span style="color: #000000;"> ClusterConfiguration.LocalhostPrimarySilo(); 
</span><span style="color: #0000ff;">var</span> silo = <span style="color: #0000ff;">new</span> SiloHost(<span style="color: #800000;">"</span><span style="color: #800000;">Test Silo</span><span style="color: #800000;">"</span><span style="color: #000000;">, siloConfig); 
silo.InitializeOrleansSilo(); 
silo.StartOrleansSilo();

Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">按Enter键关闭。</span><span style="color: #800000;">"</span><span style="color: #000000;">); 
</span><span style="color: #008000;">//</span><span style="color: #008000;"> 在这里阻止</span>
<span style="color: #000000;">Console.ReadLine(); 

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 我们完成后关闭筒仓。</span>
silo.ShutdownOrleansSilo();</pre>
</div>
<p>3，配置和连接客户端</p>
<p>用于连接到仓储集群并向Grains发送请求的客户端通过ClientConfiguration对象和ClientBuilder以编程方式进行配置。 ClientConfiguration对象可以实例化并直接填充，从一个文件加载设置，或者为不同的部署环境使用多个可用的帮助器方法创建。 对于本地测试，最简单的方法是使用ClientConfiguration.LocalhostSilo()辅助方法。 然后将配置对象传递给ClientBuilder类的新实例。</p>
<p>ClientBuilder公开了更多配置其他客户端功能的方法。 之后调用ClientBuilder对象的Build方法来获得IClusterClient接口的实现。 最后，我们调用返回对象上的Connect()方法来连接到集群。</p>
<p>您可以创建一个空的控制台应用程序项目，以.NET Framework 4.6.1或更高版本为目标来运行客户端，或者重新使用您创建的控制台应用程序项目托管一个仓储。 将Microsoft.Orleans.Client NuGet元程序包添加到项目。</p>
<div class="cnblogs_code">
<pre>PM&gt; Install-Package Microsoft.Orleans.Client</pre>
</div>
<p>以下是一个客户端如何连接到本地仓储的例子：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> config =<span style="color: #000000;"> ClientConfiguration.LocalhostSilo();
</span><span style="color: #0000ff;">var</span> builder = <span style="color: #0000ff;">new</span><span style="color: #000000;"> ClientBuilder().UseConfiguration(config).
</span><span style="color: #0000ff;">var</span> client =<span style="color: #000000;"> builder.Build();
</span><span style="color: #0000ff;">await</span> client.Connect();</pre>
</div>
<p>4，生产配置</p>
<p>我们在这里使用的配置示例是用于测试与本地主机在同一台机器上运行的仓储和客户机。 在生产中，仓储和客户机通常运行在不同的服务器上，并配置有一个可靠的群集配置选项。 有关详细信息，请参阅<a href="https://dotnet.github.io/orleans/Documentation/Deployment-and-Operations/Configuration-Guide/index.html">Configuration Guide</a>和<a href="https://dotnet.github.io/orleans/Documentation/Runtime-Implementation-Details/Cluster-Management.html">Cluster Management</a>的说明。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a5"></a>五、调式</span></strong></p>
<p>1，调试</p>
<p>在开发过程中，基于Orleans的应用程序可以在开发过程中使用调试器来调试程序或客户进程。为了快速开发迭代，使用单独的进程来结合仓储和客户端是很方便的，例如，由Orleans Dev/Test Host项目模板创建的控制台应用程序项目，它是Microsoft Orleans工具扩展Visual Studio的一部分。当在Azure计算模拟器中运行时，可以将调试器附加到Worker / Web Role实例进程。</p>
<p>在生产环境中，在一个断点处停止仓储几乎不是一个好主意，因为冻结的仓储很快就会被集群成员协议投票死掉，并且将无法与集群中的其他仓储进行通信。 因此，在生产追踪是主要的&ldquo;调试&rdquo;机制。</p>
<p>2，来源链接</p>
<p>从2.0 - beta1版本开始，我们增加了对符号的源链接支持。这意味着，如果一个项目使用了新Orleans的NuGet软件包，在调试应用程序代码时，它们就可以进入Orleans源代码。在Steve Gordon的博客文章中，您可以看到配置它需要哪些步骤。</p>
<p>&nbsp;</p>