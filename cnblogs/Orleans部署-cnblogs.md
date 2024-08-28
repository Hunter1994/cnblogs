<p><a href="#a1"><strong>一、配置指南</strong></a></p>
<p><a href="#a11">1，客户端配置</a></p>
<p><a href="#a12">2，服务端配置</a></p>
<p><a href="#a13">3，典型配置</a></p>
<p><a href="#a14">4，配置.NET垃圾收集</a></p>
<p><a href="#a15">5，SQL系统存储</a></p>
<p><a href="#a2"><strong>二、监控</strong></a></p>
<p><a href="#a21">1，运行时监视</a></p>
<p><a href="#a22">2，silo错误代码监测</a></p>
<p><a href="#a23">3，客户端错误代码监测</a></p>
<p><strong><a href="#a24">三、解决部署问题</a></strong></p>
<p><strong><a href="#a25">四、异构silos</a></strong></p>
<p><strong><a href="#a26">五、开始使用Azure Web Apps</a></strong></p>
<p><strong><a href="#a27">六、Docker部署</a></strong></p>
<p><strong><a href="#a28">七、服务结构托管</a></strong></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><a name="a1"></a><strong><span style="color: #ffffff; font-size: 18pt;">一、配置指南</span></strong></p>
<p>本配置指南介绍了关键配置参数以及如何在大多数典型使用场景中使用这些参数。</p>
<p>Orleans Configuration xsd file&nbsp;is located&nbsp;<a href="https://github.com/dotnet/orleans/blob/master/src/Orleans.Core/Configuration/OrleansConfiguration.xsd">here</a>.</p>
<p>Orleans可以用于各种适合不同使用场景的配置，例如用于开发和测试的本地单节点部署，服务器群集，多实例Azure工作者角色等等。所有不同的目标场景都是通过指定特定 Orleans配置XML文件中的值。 本指南提供了使Orleans在其中一个目标方案中运行所需的关键配置参数的说明。 还有其他的配置参数，主要是为了更好地调整奥尔良的性能。 它们记录在XSD模式中，即使在生产中运行系统也不需要。</p>
<p>Orleans良是一个建立和运行高规模服务的框架。 Orleans应用程序的典型部署跨越了一组服务器。 在每台服务器上运行的Orleans运行时（称为silos）实例需要配置为相互连接。 除此之外，总是有一个连接到Orleans部署的客户端组件，通常是一个Web前端，需要配置它以连接到silos。 本指南的&ldquo;服务器配置&rdquo;和&ldquo;客户端配置&rdquo;部分分别介绍了这些方面。 &ldquo;典型配置&rdquo;部分提供了一些常见配置的摘要。</p>
<p><a name="a11"></a>1，客户端配置</p>
<p>有两种方法:手动配置一个或多个网关端点，或者将客户端指向由silos的集群成员使用的Azure表。在后一种情况下，客户端会自动发现在部署中启用的客户机网关的silos，并在连接或离开集群时调整其与网关的连接。该选项是可靠的，并推荐用于生产部署。</p>
<p>①固定网关配置</p>
<p>ClientConfiguration.xml中使用一个或多个网关节点指定一组固定的网关：&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ClientConfiguration </span><span style="color: #ff0000;">xmlns</span><span style="color: #0000ff;">="urn:orleans"</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Gateway </span><span style="color: #ff0000;">Address</span><span style="color: #0000ff;">="gateway1"</span><span style="color: #ff0000;"> Port</span><span style="color: #0000ff;">="30000"</span><span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Gateway </span><span style="color: #ff0000;">Address</span><span style="color: #0000ff;">="gateway2"</span><span style="color: #ff0000;"> Port</span><span style="color: #0000ff;">="30000"</span><span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Gateway </span><span style="color: #ff0000;">Address</span><span style="color: #0000ff;">="gateway3"</span><span style="color: #ff0000;"> Port</span><span style="color: #0000ff;">="30000"</span><span style="color: #0000ff;">/&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">ClientConfiguration</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>一个网关通常就足够了。 多个网关连接有助于提高系统的吞吐量和可靠性。</p>
<p>②基于群集成员的网关配置</p>
<p>要将客户端配置为从silo集群成员资格表中自动查找网关，您需要指定Azure表或SQL Server连接字符串以及目标部署标识</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ClientConfiguration </span><span style="color: #ff0000;">xmlns</span><span style="color: #0000ff;">="urn:orleans"</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">SystemStore </span><span style="color: #ff0000;">SystemStoreType</span><span style="color: #0000ff;">="AzureTable"</span><span style="color: #ff0000;">
               DeploymentId</span><span style="color: #0000ff;">="target deployment ID"</span><span style="color: #ff0000;">
               DataConnectionString</span><span style="color: #0000ff;">="Azure storage connection string"</span><span style="color: #0000ff;">/&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">ClientConfiguration</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>或者</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ClientConfiguration </span><span style="color: #ff0000;">xmlns</span><span style="color: #0000ff;">="urn:orleans"</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">SystemStore </span><span style="color: #ff0000;">SystemStoreType</span><span style="color: #0000ff;">="SqlServer"</span><span style="color: #ff0000;">
               DeploymentId</span><span style="color: #0000ff;">="target deployment ID"</span><span style="color: #ff0000;">
               DataConnectionString</span><span style="color: #0000ff;">="SQL connection string"</span><span style="color: #0000ff;">/&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">ClientConfiguration</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>或者</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ClientConfiguration </span><span style="color: #ff0000;">xmlns</span><span style="color: #0000ff;">="urn:orleans"</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">SystemStore </span><span style="color: #ff0000;">SystemStoreType</span><span style="color: #0000ff;">="ZooKeeper"</span><span style="color: #ff0000;">
               DeploymentId</span><span style="color: #0000ff;">="target deployment ID"</span><span style="color: #ff0000;">
               DataConnectionString</span><span style="color: #0000ff;">="ZooKeeper connection string"</span><span style="color: #0000ff;">/&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">ClientConfiguration</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>③本地silo</p>
<p>对于使用本地silo的本地开发/测试配置，应将客户端网关配置为&ldquo;localhost&rdquo;。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ClientConfiguration </span><span style="color: #ff0000;">xmlns</span><span style="color: #0000ff;">="urn:orleans"</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Gateway </span><span style="color: #ff0000;">Address</span><span style="color: #0000ff;">="localhost"</span><span style="color: #ff0000;"> Port</span><span style="color: #0000ff;">="30000"</span><span style="color: #0000ff;">/&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">ClientConfiguration</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>④Web Azure中的Web角色客户端</p>
<p>当客户端是与silo 工作角色相同的Azure部署中运行的Web角色时，当调用OrleansAzureClient.Initialize()时，将从OrleansSiloInstances表中读取所有网关地址信息。 用于查找正确OrleansSiloInstances表的Azure存储连接字符串在部署和角色的服务配置中定义的&ldquo;DataConnectionString&rdquo;设置中指定。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ServiceConfiguration  </span><span style="color: #ff0000;">...</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Role </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="WebRole"</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;"> ...
    </span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ConfigurationSettings</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Setting </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="DataConnectionString"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">="DefaultEndpointsProtocol=https;AccountName=MYACCOUNTNAME;AccountKey=MYACCOUNTKEY"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">ConfigurationSettings</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Role</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">
  ...
</span><span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">ServiceConfiguration</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>silo 工作者角色和Web客户端角色都需要使用相同的Azure存储帐户才能成功发现彼此。</p>
<p>当使用OrleansAzureClient.Initialize()和OrleansSiloInstances表进行网关地址发现时，客户端配置文件中不需要额外的网关地址信息。 通常，ClientConfiguration.xml文件将只包含一些最低限度的调试/跟踪配置设置，尽管这不是必需的。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ClientConfiguration </span><span style="color: #ff0000;">xmlns</span><span style="color: #0000ff;">="urn:orleans"</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Tracing </span><span style="color: #ff0000;">DefaultTraceLevel</span><span style="color: #0000ff;">="Info"</span> <span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">TraceLevelOverride </span><span style="color: #ff0000;">LogPrefix</span><span style="color: #0000ff;">="Application"</span><span style="color: #ff0000;"> TraceLevel</span><span style="color: #0000ff;">="Info"</span> <span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Tracing</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">ClientConfiguration</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>基于代码的客户端配置。 这是仅供参考的示例，不应该按原样使用 - 您可能需要针对特定环境微调客户端参数。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> dataConnection = <span style="color: #800000;">"</span><span style="color: #800000;">DefaultEndpointsProtocol=https;AccountName=MYACCOUNTNAME;AccountKey=MYACCOUNTKEY</span><span style="color: #800000;">"</span><span style="color: #000000;">;

</span><span style="color: #0000ff;">var</span> config = <span style="color: #0000ff;">new</span><span style="color: #000000;"> ClientConfiguration
{
    </span><span style="color: #008000;">//一些顶级功能</span>
    GatewayProvider =<span style="color: #000000;"> ClientConfiguration.GatewayProviderType.AzureTable,
    ResponseTimeout </span>= TimeSpan.FromSeconds(<span style="color: #800080;">30</span><span style="color: #000000;">),
    DeploymentId </span>=<span style="color: #000000;"> RoleEnvironment.DeploymentId,
    DataConnectionString </span>=<span style="color: #000000;"> dataConnection,
    PropagateActivityId </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">,

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 跟踪</span>
    DefaultTraceLevel =<span style="color: #000000;"> Severity.Info,
    TraceToConsole </span>= <span style="color: #0000ff;">false</span><span style="color: #000000;">,
    TraceFilePattern </span>= <span style="color: #800000;">@"</span><span style="color: #800000;">Client_{0}-{1}.log</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #008000;">//</span><span style="color: #008000;">TraceFilePattern = "false", </span><span style="color: #008000;">//</span><span style="color: #008000;"> 将其设置为false或none，禁用文件跟踪，有效地设置config.Defaults.TraceFileName = null;</span>
<span style="color: #000000;">
    TraceLevelOverrides </span>=<span style="color: #000000;">
    {
        Tuple.Create(</span><span style="color: #800000;">"</span><span style="color: #800000;">ComponentName</span><span style="color: #800000;">"</span><span style="color: #000000;">, Severity.Warning),
    }
};

config.RegisterStreamProvider</span>&lt;AzureQueueStreamProvider&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">AzureQueueStreams</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">string</span>&gt;<span style="color: #000000;">
    {
        { </span><span style="color: #800000;">"</span><span style="color: #800000;">PubSubType</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">ExplicitGrainBasedAndImplicit</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
        { </span><span style="color: #800000;">"</span><span style="color: #800000;">DeploymentId</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">orleans-streams</span><span style="color: #800000;">"</span> }, <span style="color: #008000;">//</span><span style="color: #008000;"> 这将是您的队列的前缀名称 - 所以要小心并使用对队列名称有效的字符串</span>
        { <span style="color: #800000;">"</span><span style="color: #800000;">NumQueues</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">4</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
        { </span><span style="color: #800000;">"</span><span style="color: #800000;">GetQueueMessagesTimerPeriod</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">100ms</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
        { </span><span style="color: #800000;">"</span><span style="color: #800000;">DataConnectionString</span><span style="color: #800000;">"</span><span style="color: #000000;">, dataConnection }
    });

config.RegisterStreamProvider</span>&lt;SimpleMessageStreamProvider&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">SimpleMessagingStreams</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">string</span>&gt;<span style="color: #000000;">
    {
        { </span><span style="color: #800000;">"</span><span style="color: #800000;">PubSubType</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">ExplicitGrainBasedAndImplicit</span><span style="color: #800000;">"</span><span style="color: #000000;"> }
    });

IClusterClient client </span>= <span style="color: #0000ff;">null</span><span style="color: #000000;">;
</span><span style="color: #0000ff;">while</span> (<span style="color: #0000ff;">true</span><span style="color: #000000;">)
{
    </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 构建一个客户端，然后将其连接到群集。</span>
        client = <span style="color: #0000ff;">new</span><span style="color: #000000;"> ClientBuilder()
            .UseConfiguration(config)
            .ConfigureServices(
                services </span>=&gt;<span style="color: #000000;">
                {
                    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 服务可以在这里提供给客户。 这些服务通过依赖注入来提供。 ConfigureServices可以多次调用一个ClientBuilder实例。</span>
<span style="color: #000000;">                })
            .Build();

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 将客户端连接到群集。 一旦连接成功，客户端将维护连接，根据需要自动重新连接。</span>
        <span style="color: #0000ff;">await</span> client.Connect().ConfigureAwait(<span style="color: #0000ff;">false</span><span style="color: #000000;">);
        </span><span style="color: #0000ff;">break</span><span style="color: #000000;">;
    }
    </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (Exception exception)
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 如果连接尝试失败，则必须处理客户机实例。</span>
        client?<span style="color: #000000;">.Dispose();

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> TODO:记录异常。
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> TODO: Add a counter to break up an infinite cycle (circuit breaker pattern).</span>
        <span style="color: #0000ff;">await</span> Task.Delay(TimeSpan.FromSeconds(<span style="color: #800080;">5</span><span style="color: #000000;">));
    }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 使用客户端。
</span><span style="color: #008000;">//</span><span style="color: #008000;"> 请注意，客户端可以在线程之间共享，并且通常是长期的。</span>
<span style="color: #0000ff;">var</span> user client.GetGrain&lt;IUserGrain&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">leeroy77jenkins@battle.net</span><span style="color: #800000;">"</span><span style="color: #000000;">);
Console.WriteLine(</span><span style="color: #0000ff;">await</span> user.GetProfile());</pre>
</div>
<p><a name="a12"></a>2，服务端配置</p>
<p>silo&nbsp;配置有两个关键方面：</p>
<ul>
<li>连通性：silo的其他silo和客户的端点</li>
<li>集群成员和可靠性：在部署中如何发现对方并检测节点故障。</li>
</ul>
<p>取决于你想在这些参数中运行Orleans的环境可能重要，也可能不重要。 例如，对于单个silo开发环境，通常不需要可靠性，并且所有端点都可以是本地主机</p>
<p>以下部分详细介绍了上述四个关键方面的配置设置。 然后在场景部分中，可以找到最典型的部署场景的建议组合设置。</p>
<p>①连接</p>
<p>连接设置定义了两个TCP / IP端点：一个用于silo 间通信，另一个用于客户端连接，也称为客户端网关或简单的网关。</p>
<p><strong>跨筒仓端点</strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Networking </span><span style="color: #ff0000;">Address</span><span style="color: #0000ff;">=" "</span><span style="color: #ff0000;"> Port</span><span style="color: #0000ff;">="11111"</span> <span style="color: #0000ff;">/&gt;</span></pre>
</div>
<p>地址：使用的IP地址或主机名。 如果留空，silo&nbsp;将选择第一个可用的IPv4地址。 Orleans支持IPv6以及IPv4。&nbsp;</p>
<p>端口：要使用的TCP端口。 如果留空，silo将会随机选择一个端口。 如果机器上只有一个silo正在运行，建议指定一个端口以保持一致性，并便于配置防火墙。 要在同一台计算机上运行多个silo，可以为每个silo提供不同的配置文件，也可以将端口属性留空以便随机分配端口。</p>
<p>对于分配了多个IP地址的计算机，如果您需要从特定子网或IPv6地址中选择一个地址，则可以通过分别添加子网和PreferredFamily属性来执行此操作（请参阅XSD模式以获取准确的语法 这些属性）。</p>
<p>对于本地开发环境，您可以简单地使用localhost作为主机名：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Networking </span><span style="color: #ff0000;">Address</span><span style="color: #0000ff;">="localhost"</span><span style="color: #ff0000;"> Port</span><span style="color: #0000ff;">="11111"</span> <span style="color: #0000ff;">/&gt;</span></pre>
</div>
<p>②客户端网关端点</p>
<p>除了XML元素名称之外，客户端网关端点的设置与silo间端点相同：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ProxyingGateway </span><span style="color: #ff0000;">Address</span><span style="color: #0000ff;">="localhost"</span><span style="color: #ff0000;"> Port</span><span style="color: #0000ff;">="30000"</span> <span style="color: #0000ff;">/&gt;</span></pre>
</div>
<p>您必须指定与用于inter-silo端点的端口号不同的端口号。</p>
<p>可以将客户端配置为连接到跨站点端点而不是网关，但是这需要在客户端上打开监听套接字（因此需要在客户端计算机防火墙上启用传入连接），并且通常不建议 对于一组非常有限的场景。</p>
<p>③集群成员和可靠性</p>
<p>通常，在Orleans上构建的服务部署在专用硬件或Azure节点集群上。 对于开发和基本测试，Orleans可以部署在单个节点配置中。 在部署到一个节点集群时，Orleans在内部实现了一套协议，以发现和维护集群中Orleans silos的成员资格，包括检测节点故障和自动重新配置。</p>
<p>为了可靠地管理集群成员资格，Orleans使用Azure Table，SQL Server或Apache ZooKeeper进行节点同步。 可靠的成员资格设置要求在silo配置文件中配置&ldquo;SystemStore&rdquo;元素设置：&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">SystemStore </span><span style="color: #ff0000;">SystemStoreType</span><span style="color: #0000ff;">="AzureTable"</span><span style="color: #ff0000;">
             DeploymentId</span><span style="color: #0000ff;">="..."</span><span style="color: #ff0000;">
             DataConnectionString</span><span style="color: #0000ff;">="..."</span><span style="color: #0000ff;">/&gt;</span></pre>
</div>
<p>或者</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">SystemStore </span><span style="color: #ff0000;">SystemStoreType</span><span style="color: #0000ff;">="SqlServer"</span><span style="color: #ff0000;">
             DeploymentId</span><span style="color: #0000ff;">="..."</span><span style="color: #ff0000;">
             DataConnectionString</span><span style="color: #0000ff;">="..."</span><span style="color: #0000ff;">/&gt;</span></pre>
</div>
<p>或者</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">SystemStore </span><span style="color: #ff0000;">SystemStoreType</span><span style="color: #0000ff;">="ZooKeeper"</span><span style="color: #ff0000;">
             DeploymentId</span><span style="color: #0000ff;">="..."</span><span style="color: #ff0000;">
             DataConnectionString</span><span style="color: #0000ff;">="..."</span><span style="color: #0000ff;">/&gt;</span></pre>
</div>
<p>DeploymentId是定义特定部署的唯一字符串。 将基于Orleans的服务部署到Azure时，使用辅助角色的Azure部署标识是最有意义的。</p>
<p>对于开发，或者如果不可能使用Azure表，可以将silos配置为使用成员grain。这样的配置是不可靠的，因为它将无法在主仓的失败中存活下来，而主仓则承载着会员的grain。&ldquo;MembershipTableGrain&rdquo;是LivenessType的默认值。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Liveness </span><span style="color: #ff0000;">LivenessType </span><span style="color: #0000ff;">="MembershipTableGrain"</span> <span style="color: #0000ff;">/&gt;</span></pre>
</div>
<p>④主silo</p>
<p>在可靠的部署中，使用Azure Table，SQL Server或ZooKeeper配置成员资格，所有创建的silo都是相同的，没有主要或次要silo的概念。 这是推荐用于生产的配置，能够在任何单个节点或节点组合的故障中幸免于难。 例如，Azure会定期推出操作系统修补程序，并最终导致所有角色实例重新启动。</p>
<p>当使用MembershipTableGrain进行开发或非可靠部署时，必须将其中一个silo指定为主要，并且必须在加入群集之前等待主要进行初始化的其他辅助silo之前启动和初始化。 在主节点出现故障的情况下，整个部署停止正常工作，必须重新启动。</p>
<p>主要是在配置文件中用全局部分中的以下设置指定的。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">SeedNode </span><span style="color: #ff0000;">Address</span><span style="color: #0000ff;">="&lt;host name or IP address of the primary node&gt;"</span><span style="color: #ff0000;"> Port</span><span style="color: #0000ff;">="11111"</span> <span style="color: #0000ff;">/&gt;</span></pre>
</div>
<p>下面是一个如何配置和启动托管在工作角色内的Orleans silo的例子。 这是仅供参考的示例，不应该按原样使用 - 您可能需要针对特定环境微调客户端参数。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> dataConnection = <span style="color: #800000;">"</span><span style="color: #800000;">DefaultEndpointsProtocol=https;AccountName=MYACCOUNTNAME;AccountKey=MYACCOUNTKEY</span><span style="color: #800000;">"</span><span style="color: #000000;">;

</span><span style="color: #0000ff;">var</span> config = <span style="color: #0000ff;">new</span><span style="color: #000000;"> ClusterConfiguration
{
    Globals </span>=<span style="color: #000000;">
    {
        DeploymentId </span>=<span style="color: #000000;"> RoleEnvironment.DeploymentId,
        ResponseTimeout </span>= TimeSpan.FromSeconds(<span style="color: #800080;">30</span><span style="color: #000000;">),
        DataConnectionString </span>=<span style="color: #000000;"> dataConnection,

        LivenessType </span>=<span style="color: #000000;"> GlobalConfiguration.LivenessProviderType.AzureTable,
        ReminderServiceType </span>=<span style="color: #000000;"> GlobalConfiguration.ReminderServiceProviderType.AzureTable,
    },
    Defaults </span>=<span style="color: #000000;">
    {
        PropagateActivityId </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">,

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 跟踪</span>
        DefaultTraceLevel =<span style="color: #000000;"> Severity.Info,
        TraceToConsole </span>= <span style="color: #0000ff;">false</span><span style="color: #000000;">,
        TraceFilePattern </span>= <span style="color: #800000;">@"</span><span style="color: #800000;">Silo_{0}-{1}.log</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #008000;">//TraceFilePattern =&ldquo;false&rdquo;，//将其设置为false或none来禁用文件跟踪，有效地设置了config.Defaults。TraceFileName =零;</span>
        TraceLevelOverrides =<span style="color: #000000;">
        {
            Tuple.Create(</span><span style="color: #800000;">"</span><span style="color: #800000;">ComponentName</span><span style="color: #800000;">"</span><span style="color: #000000;">, Severity.Warning),
        }
    }
};

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 注册引导provider类</span>
config.Globals.RegisterBootstrapProvider&lt;AutoStartBootstrapProvider&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">MyAutoStartBootstrapProvider</span><span style="color: #800000;">"</span><span style="color: #000000;">);

</span><span style="color: #008000;">//</span><span style="color: #008000;"> Add Storage Providers</span>
config.Globals.RegisterStorageProvider&lt;MemoryStorage&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">MemoryStore</span><span style="color: #800000;">"</span><span style="color: #000000;">);

config.Globals.RegisterStorageProvider</span>&lt;AzureTableStorage&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">PubSubStore</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">string</span>&gt;<span style="color: #000000;">
    {
        { </span><span style="color: #800000;">"</span><span style="color: #800000;">DeleteStateOnClear</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">true</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
        </span><span style="color: #008000;">//</span><span style="color: #008000;">{ "UseJsonFormat", "true" },</span>
        { <span style="color: #800000;">"</span><span style="color: #800000;">DataConnectionString</span><span style="color: #800000;">"</span><span style="color: #000000;">, dataConnection }
    });

config.Globals.RegisterStorageProvider</span>&lt;AzureTableStorage&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">AzureTable</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">string</span>&gt;<span style="color: #000000;">
    {
        { </span><span style="color: #800000;">"</span><span style="color: #800000;">DeleteStateOnClear</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">true</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
        { </span><span style="color: #800000;">"</span><span style="color: #800000;">DataConnectionString</span><span style="color: #800000;">"</span><span style="color: #000000;">, dataConnection }
    });

config.Globals.RegisterStorageProvider</span>&lt;AzureTableStorage&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">DataStorage</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">string</span>&gt;<span style="color: #000000;">
    {
        { </span><span style="color: #800000;">"</span><span style="color: #800000;">DeleteStateOnClear</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">true</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
        { </span><span style="color: #800000;">"</span><span style="color: #800000;">DataConnectionString</span><span style="color: #800000;">"</span><span style="color: #000000;">, dataConnection }
    });

config.Globals.RegisterStorageProvider</span>&lt;BlobStorageProvider&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">BlobStorage</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">string</span>&gt;<span style="color: #000000;">
    {
        { </span><span style="color: #800000;">"</span><span style="color: #800000;">DeleteStateOnClear</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">true</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
        { </span><span style="color: #800000;">"</span><span style="color: #800000;">ContainerName</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">grainstate</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
        { </span><span style="color: #800000;">"</span><span style="color: #800000;">DataConnectionString</span><span style="color: #800000;">"</span><span style="color: #000000;">, dataConnection }
    });

</span><span style="color: #008000;">//</span><span style="color: #008000;"> Add Stream Providers</span>
config.Globals.RegisterStreamProvider&lt;AzureQueueStreamProvider&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">AzureQueueStreams</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">string</span>&gt;<span style="color: #000000;">
    {
        { </span><span style="color: #800000;">"</span><span style="color: #800000;">PubSubType</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">ExplicitGrainBasedAndImplicit</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
        { </span><span style="color: #800000;">"</span><span style="color: #800000;">DeploymentId</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">orleans-streams</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
        { </span><span style="color: #800000;">"</span><span style="color: #800000;">NumQueues</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">4</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
        { </span><span style="color: #800000;">"</span><span style="color: #800000;">GetQueueMessagesTimerPeriod</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">100ms</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
        { </span><span style="color: #800000;">"</span><span style="color: #800000;">DataConnectionString</span><span style="color: #800000;">"</span><span style="color: #000000;">, dataConnection }
    });

</span><span style="color: #0000ff;">try</span><span style="color: #000000;">
{
    _orleansAzureSilo </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> AzureSilo();
    </span><span style="color: #0000ff;">var</span> ok =<span style="color: #000000;"> _orleansAzureSilo.Start(config, config.Globals.DeploymentId, config.Globals.DataConnectionString);

    _orleansAzureSilo.Run(); </span><span style="color: #008000;">//调用将阻塞直到silo关闭。</span>
<span style="color: #000000;">}
</span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (Exception exc)
{
    </span><span style="color: #008000;">//</span><span style="color: #008000;">Log "Error when starting Silo"</span>
}</pre>
</div>
<p><a name="a13"></a>3，典型配置</p>
<p>以下是可用于开发和生产部署的典型配置示例。</p>
<p>①本地开发</p>
<p>对于本地开发，在程序员的机器上只有一个本地运行的silo，配置已经包含在Microsoft Orleans Visual Studio的Orleans Dev / Test Host项目模板中。 可以通过运行使用Orleans Dev / Test Host模板创建的项目来启动的本地silo在DevTestServerConfiguration.xml中配置如下。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">OrleansConfiguration </span><span style="color: #ff0000;">xmlns</span><span style="color: #0000ff;">="urn:orleans"</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Globals</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">SeedNode </span><span style="color: #ff0000;">Address</span><span style="color: #0000ff;">="localhost"</span><span style="color: #ff0000;"> Port</span><span style="color: #0000ff;">="11111"</span> <span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Globals</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Defaults</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Networking </span><span style="color: #ff0000;">Address</span><span style="color: #0000ff;">="localhost"</span><span style="color: #ff0000;"> Port</span><span style="color: #0000ff;">="11111"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ProxyingGateway </span><span style="color: #ff0000;">Address</span><span style="color: #0000ff;">="localhost"</span><span style="color: #ff0000;"> Port</span><span style="color: #0000ff;">="30000"</span> <span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Defaults</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">OrleansConfiguration</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>通过代码的silo配置如下。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> config = ClusterConfiguration.LocalhostPrimarySilo(<span style="color: #800080;">11111</span>, <span style="color: #800080;">30000</span>);</pre>
</div>
<p>要连接到本地silo，客户端需要配置为本地主机，并且只能从同一台机器连接。 可以通过运行Orleans Dev / Test Host模板创建的项目启动的Orleans客户端在DevTestClientConfiguration.xml中配置如下</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ClientConfiguration </span><span style="color: #ff0000;">xmlns</span><span style="color: #0000ff;">="urn:orleans"</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Gateway </span><span style="color: #ff0000;">Address</span><span style="color: #0000ff;">="localhost"</span><span style="color: #ff0000;"> Port</span><span style="color: #0000ff;">="30000"</span><span style="color: #0000ff;">/&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">ClientConfiguration</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>通过代码进行客户端配置如下。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> config = ClientConfiguration.LocalhostSilo(<span style="color: #800080;">30000</span>);</pre>
</div>
<p>②使用Azure进行可靠的生产部署</p>
<p>对于使用Azure进行可靠的生产部署，您需要使用Azure Table选项来获得集群成员资格。 此配置是部署到本地服务器或Azure虚拟机实例的典型配置。</p>
<p>DataConnection字符串的格式是&ldquo;DefaultEndpointsProtocol = https; AccountName =; AccountKey =&rdquo;</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">OrleansConfiguration </span><span style="color: #ff0000;">xmlns</span><span style="color: #0000ff;">="urn:orleans"</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Globals</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">SystemStore </span><span style="color: #ff0000;">SystemStoreType</span><span style="color: #0000ff;">="AzureTable"</span><span style="color: #ff0000;">
         DeploymentId</span><span style="color: #0000ff;">="&lt;your deployment ID&gt;"</span><span style="color: #ff0000;">
         DataConnectionString</span><span style="color: #0000ff;">="&lt;&lt;see comment above&gt;&gt;"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Liveness </span><span style="color: #ff0000;">LivenessType </span><span style="color: #0000ff;">="AzureTable"</span> <span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Globals</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Defaults</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Networking </span><span style="color: #ff0000;">Address</span><span style="color: #0000ff;">=""</span><span style="color: #ff0000;"> Port</span><span style="color: #0000ff;">="11111"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ProxyingGateway </span><span style="color: #ff0000;">Address</span><span style="color: #0000ff;">=""</span><span style="color: #ff0000;"> Port</span><span style="color: #0000ff;">="30000"</span> <span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Defaults</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">OrleansConfiguration</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>客户端需要配置为使用Azure表来发现网关，Orleans 服务器的地址不是静态地被客户知道的。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ClientConfiguration </span><span style="color: #ff0000;">xmlns</span><span style="color: #0000ff;">="urn:orleans"</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">SystemStore </span><span style="color: #ff0000;">SystemStoreType</span><span style="color: #0000ff;">="AzureTable"</span><span style="color: #ff0000;"> DeploymentId</span><span style="color: #0000ff;">="target deployment ID"</span><span style="color: #ff0000;"> DataConnectionString</span><span style="color: #0000ff;">="&lt;&lt;see comment above&gt;&gt;"</span> <span style="color: #0000ff;">/&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">ClientConfiguration</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>③使用ZooKeeper进行可靠的生产部署</p>
<p>为了使用ZooKeeper进行可靠的生产部署，您需要使用ZooKeeper选项来获得集群成员资格。 此配置是部署到内部部署服务器的典型配置。</p>
<p>在&ldquo;ZooKeeper程序员指南&rdquo;中记录了DataConnection字符串的格式。 建议至少5台ZooKeeper服务器。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;?</span><span style="color: #ff00ff;">xml version="1.0" encoding="utf-8"</span><span style="color: #0000ff;">?&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">OrleansConfiguration </span><span style="color: #ff0000;">xmlns</span><span style="color: #0000ff;">="urn:orleans"</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Globals</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">SystemStore </span><span style="color: #ff0000;">SystemStoreType</span><span style="color: #0000ff;">="ZooKeeper"</span><span style="color: #ff0000;">
                   DeploymentId</span><span style="color: #0000ff;">="&lt;your deployment ID&gt;"</span><span style="color: #ff0000;">
                   DataConnectionString</span><span style="color: #0000ff;">="&lt;&lt;see comment above&gt;&gt;"</span><span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Globals</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Defaults</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Networking </span><span style="color: #ff0000;">Address</span><span style="color: #0000ff;">="localhost"</span><span style="color: #ff0000;"> Port</span><span style="color: #0000ff;">="11111"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ProxyingGateway </span><span style="color: #ff0000;">Address</span><span style="color: #0000ff;">="localhost"</span><span style="color: #ff0000;"> Port</span><span style="color: #0000ff;">="30000"</span> <span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Defaults</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">OrleansConfiguration</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>客户端需要配置为使用ZooKeeper来发现网关，Orleans 服务器的地址不是静态地被客户知道的。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;?</span><span style="color: #ff00ff;">xml version="1.0" encoding="utf-8" </span><span style="color: #0000ff;">?&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ClientConfiguration </span><span style="color: #ff0000;">xmlns</span><span style="color: #0000ff;">="urn:orleans"</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">SystemStore </span><span style="color: #ff0000;">SystemStoreType</span><span style="color: #0000ff;">="ZooKeeper"</span><span style="color: #ff0000;"> DeploymentId</span><span style="color: #0000ff;">="target deployment ID"</span><span style="color: #ff0000;"> DataConnectionString</span><span style="color: #0000ff;">="&lt;&lt;see comment above&gt;&gt;"</span><span style="color: #0000ff;">/&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">ClientConfiguration</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>④使用SQL Server进行可靠的生产部署</p>
<p>为了使用SQL Server进行可靠的生产部署，需要提供SQL Server连接字符串。</p>
<p>通过代码进行筒仓配置如下，包括日志配置。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> connectionString = <span style="color: #800000;">@"</span><span style="color: #800000;">Data Source=MSSQLDBServer;Initial Catalog=Orleans;Integrated Security=True;
    Max Pool Size=200;Asynchronous Processing=True;MultipleActiveResultSets=True</span><span style="color: #800000;">"</span><span style="color: #000000;">;

</span><span style="color: #0000ff;">var</span> config = <span style="color: #0000ff;">new</span><span style="color: #000000;"> ClusterConfiguration{    
    Globals </span>=<span style="color: #000000;">    
    {
        DataConnectionString </span>=<span style="color: #000000;"> connectionString,
        DeploymentId </span>= <span style="color: #800000;">"</span><span style="color: #800000;">&lt;your deployment ID&gt;</span><span style="color: #800000;">"</span><span style="color: #000000;">,

        LivenessType </span>=<span style="color: #000000;"> GlobalConfiguration.LivenessProviderType.SqlServer,
        LivenessEnabled </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">,
        ReminderServiceType </span>=<span style="color: #000000;"> GlobalConfiguration.ReminderServiceProviderType.SqlServer
    },
    Defaults </span>=<span style="color: #000000;">
    {        
        Port </span>= <span style="color: #800080;">11111</span><span style="color: #000000;">,
        ProxyGatewayEndpoint </span>= <span style="color: #0000ff;">new</span> IPEndPoint(address, <span style="color: #800080;">30000</span><span style="color: #000000;">),
        PropagateActivityId </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">
    }};

</span><span style="color: #0000ff;">var</span> siloHost = <span style="color: #0000ff;">new</span> SiloHost(System.Net.Dns.GetHostName(), config);</pre>
</div>
<p>客户端需要配置为使用SQL服务器来发现网关，就像Azure和Zookeeper一样，Orleans服务器的地址对于客户端来说并不是静态的。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> connectionString = <span style="color: #800000;">@"</span><span style="color: #800000;">Data Source=MSSQLDBServer;Initial Catalog=Orleans;Integrated Security=True;
    Max Pool Size=200;Asynchronous Processing=True;MultipleActiveResultSets=True</span><span style="color: #800000;">"</span><span style="color: #000000;">;

</span><span style="color: #0000ff;">var</span> config = <span style="color: #0000ff;">new</span><span style="color: #000000;"> ClientConfiguration{
    GatewayProvider </span>=<span style="color: #000000;"> ClientConfiguration.GatewayProviderType.SqlServer,
    AdoInvariant </span>= <span style="color: #800000;">"</span><span style="color: #800000;">System.Data.SqlClient</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    DataConnectionString </span>=<span style="color: #000000;"> connectionString,

    DeploymentId </span>= <span style="color: #800000;">"</span><span style="color: #800000;">&lt;your deployment ID&gt;</span><span style="color: #800000;">"</span><span style="color: #000000;">,    
    PropagateActivityId </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">
};

</span><span style="color: #0000ff;">var</span> client = <span style="color: #0000ff;">new</span><span style="color: #000000;"> ClientBuilder().UseConfiguration(config).Build();
</span><span style="color: #0000ff;">await</span> client.Connect();</pre>
</div>
<p>⑤不可靠的专用服务器集群部署</p>
<p>要在可靠性不是问题的情况下在专用服务器集群上进行测试，可以使用MembershipTableGrain并避免依赖于Azure表。 您只需要将其中一个节点指定为主节点。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">OrleansConfiguration </span><span style="color: #ff0000;">xmlns</span><span style="color: #0000ff;">="urn:orleans"</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Globals</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">SeedNode </span><span style="color: #ff0000;">Address</span><span style="color: #0000ff;">="&lt;primary node&gt;"</span><span style="color: #ff0000;"> Port</span><span style="color: #0000ff;">="11111"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Liveness </span><span style="color: #ff0000;">LivenessType </span><span style="color: #0000ff;">="MembershipTableGrain"</span> <span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Globals</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Defaults</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Networking </span><span style="color: #ff0000;">Address</span><span style="color: #0000ff;">=" "</span><span style="color: #ff0000;"> Port</span><span style="color: #0000ff;">="11111"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ProxyingGateway </span><span style="color: #ff0000;">Address</span><span style="color: #0000ff;">=" "</span><span style="color: #ff0000;"> Port</span><span style="color: #0000ff;">="30000"</span> <span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Defaults</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">OrleansConfiguration</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>对于客户：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ClientConfiguration </span><span style="color: #ff0000;">xmlns</span><span style="color: #0000ff;">="urn:orleans"</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Gateway </span><span style="color: #ff0000;">Address</span><span style="color: #0000ff;">="node-1"</span><span style="color: #ff0000;"> Port</span><span style="color: #0000ff;">="30000"</span><span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Gateway </span><span style="color: #ff0000;">Address</span><span style="color: #0000ff;">="node-2"</span><span style="color: #ff0000;"> Port</span><span style="color: #0000ff;">="30000"</span><span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Gateway </span><span style="color: #ff0000;">Address</span><span style="color: #0000ff;">="node-3"</span><span style="color: #ff0000;"> Port</span><span style="color: #0000ff;">="30000"</span><span style="color: #0000ff;">/&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">ClientConfiguration</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>⑥Azure工作者角色部署</p>
<p>当Orleans部署到Azure Worker角色而不是VM实例时，大部分的服务器端配置实际上是在OrleansConfiguration之外的其他文件中完成的，如下所示：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">OrleansConfiguration </span><span style="color: #ff0000;">xmlns</span><span style="color: #0000ff;">="urn:orleans"</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Globals</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Liveness </span><span style="color: #ff0000;">LivenessType</span><span style="color: #0000ff;">="AzureTable"</span> <span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Globals</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Defaults</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Tracing </span><span style="color: #ff0000;">DefaultTraceLevel</span><span style="color: #0000ff;">="Info"</span><span style="color: #ff0000;"> TraceToConsole</span><span style="color: #0000ff;">="true"</span><span style="color: #ff0000;"> TraceToFile</span><span style="color: #0000ff;">="{0}-{1}.log"</span> <span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Defaults</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">OrleansConfiguration</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>一些信息保存在服务配置文件中，其中worker角色部分如下所示：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Role </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="OrleansAzureSilos"</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Instances </span><span style="color: #ff0000;">count</span><span style="color: #0000ff;">="2"</span> <span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ConfigurationSettings</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Setting </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="DataConnectionString"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">="&lt;&lt;see earlier comment&gt;&gt;"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Setting </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">="&lt;&lt;see earlier comment&gt;&gt;"</span> <span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">ConfigurationSettings</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Role</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>数据连接字符串和诊断连接字符串不必相同。</p>
<p>一些配置信息保存在服务定义文件中。 工作者角色也必须在那里配置：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">WorkerRole </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="OrleansAzureSilos"</span><span style="color: #ff0000;"> vmsize</span><span style="color: #0000ff;">="Large"</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Imports</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Import </span><span style="color: #ff0000;">moduleName</span><span style="color: #0000ff;">="Diagnostics"</span> <span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Imports</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ConfigurationSettings</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Setting </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="DataConnectionString"</span> <span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">ConfigurationSettings</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">LocalResources</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">LocalStorage </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="LocalStoreDirectory"</span><span style="color: #ff0000;"> cleanOnRoleRecycle</span><span style="color: #0000ff;">="false"</span> <span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">LocalResources</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Endpoints</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">InternalEndpoint </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="OrleansSiloEndpoint"</span><span style="color: #ff0000;"> protocol</span><span style="color: #0000ff;">="tcp"</span><span style="color: #ff0000;"> port</span><span style="color: #0000ff;">="11111"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">InternalEndpoint </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="OrleansProxyEndpoint"</span><span style="color: #ff0000;"> protocol</span><span style="color: #0000ff;">="tcp"</span><span style="color: #ff0000;"> port</span><span style="color: #0000ff;">="30000"</span> <span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Endpoints</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">WorkerRole</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>这就是托管Orleans运行时的工作者角色。 但是，在部署到Azure时，通常会有某种类型的前端，无论是网站还是Web服务，因为公开发布Orleans 并不是一个好主意。 因此，客户端配置是位于Orleans前面的Web或Worker角色（或Web站点）的配置。</p>
<p>重要说明：截至2017年11月，Azure云服务存在限制，如果Cloud Service中只有1个角色，则会阻止InternalEndpoint的防火墙配置。 如果您要通过虚拟网络连接到您的云服务，则必须将您的云服务扩展为两个实例，以便创建防火墙规则</p>
<p>假设前端是一个web角色，应该使用一个简单的ClientConfiguration文件：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ClientConfiguration </span><span style="color: #ff0000;">xmlns</span><span style="color: #0000ff;">="urn:orleans"</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Tracing </span><span style="color: #ff0000;">DefaultTraceLevel</span><span style="color: #0000ff;">="Info"</span><span style="color: #ff0000;">
           TraceToConsole</span><span style="color: #0000ff;">="true"</span><span style="color: #ff0000;">
           TraceToFile</span><span style="color: #0000ff;">="{0}-{1}.log"</span><span style="color: #ff0000;">
           WriteTraces</span><span style="color: #0000ff;">="false"</span><span style="color: #0000ff;">/&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">ClientConfiguration</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>Web角色在服务配置文件中需要与worker角色相同的连接字符串信息：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Role </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="WebRole"</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Instances </span><span style="color: #ff0000;">count</span><span style="color: #0000ff;">="2"</span> <span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ConfigurationSettings</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Setting </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="DataConnectionString"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">="&lt;&lt;see earlier comment&gt;&gt;"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Setting </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">="&lt;&lt;see earlier comment&gt;&gt;"</span> <span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">ConfigurationSettings</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Role</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>并在服务定义文件中：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">WebRole </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="WebRole"</span><span style="color: #ff0000;"> vmsize</span><span style="color: #0000ff;">="Large"</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Imports</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Import </span><span style="color: #ff0000;">moduleName</span><span style="color: #0000ff;">="Diagnostics"</span> <span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Imports</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ConfigurationSettings</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Setting </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="DataConnectionString"</span> <span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">ConfigurationSettings</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> 还有其他的网络角色数据与Orleans没有任何关系 </span><span style="color: #008000;">--&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">WebRole</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p><a name="a14"></a>4，配置.NET垃圾收集</p>
<p>为了获得良好的性能，为silo进程配置.NET垃圾回收是非常重要的。 我们找到的设置的最佳组合是设置gcServer = true和gcConcurrent = true。 当筒仓作为独立进程运行时，通过应用程序配置文件很容易设置。 您可以使用Microsoft.Orleans.OrleansHost NuGet包中包含的OrleansHost.exe.config作为示例。</p>
<p>①.NET Framework</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">configuration</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">runtime</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">gcServer </span><span style="color: #ff0000;">enabled</span><span style="color: #0000ff;">="true"</span><span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">gcConcurrent </span><span style="color: #ff0000;">enabled</span><span style="color: #0000ff;">="true"</span><span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">runtime</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">configuration</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>②.NET Core</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">// .csproj
</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">PropertyGroup</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ServerGarbageCollection</span><span style="color: #0000ff;">&gt;</span>true<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">ServerGarbageCollection</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ConcurrentGarbageCollection</span><span style="color: #0000ff;">&gt;</span>true<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">ConcurrentGarbageCollection</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">PropertyGroup</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>但是，如果silo作为Azure工作者角色的一部分运行，则默认情况下配置为使用工作站GC，这并不容易。 此博客文章展示了如何为Azure工作者角色设置相同的配置 -&nbsp;</p>
<p><a href="https://blogs.msdn.microsoft.com/cclayton/2014/06/05/server-garbage-collection-mode-in-microsoft-azure/">https://blogs.msdn.microsoft.com/cclayton/2014/06/05/server-garbage-collection-mode-in-microsoft-azure/</a></p>
<p>重要的提示服务器垃圾回收仅在多处理器计算机上可用。 因此，即使您通过应用程序配置文件（app.config或web.config）或通过引用的博客帖子上的脚本来配置垃圾收集，如果silo正在单核的（虚拟）机器上运行， 不会得到gcServer = true的好处。改善这个文件在这篇文章中.NET Framework</p>
<p><a name="a15"></a>5，SQL系统存储</p>
<p>任何可靠的生产式Orleans部署都需要使用持久性存储来保持系统状态，特别是Orleans集群状态以及用于提醒功能的数据。 除了对Azure存储的开箱即用支持外，Orleans还提供了将此信息存储在SQL Server中的选项。</p>
<p>为了使用SQL Server作为系统存储，需要调整服务器端和客户端配置。</p>
<p>服务器配置应该如下所示：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">OrleansConfiguration </span><span style="color: #ff0000;">xmlns</span><span style="color: #0000ff;">="urn:orleans"</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Globals</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">SystemStore </span><span style="color: #ff0000;">SystemStoreType </span><span style="color: #0000ff;">="SqlServer"</span><span style="color: #ff0000;">
                 DeploymentId</span><span style="color: #0000ff;">="OrleansTest"</span><span style="color: #ff0000;">
                 DataConnectionString</span><span style="color: #0000ff;">="Data Source=(localdb)\MSSQLLocalDB;Initial Catalog=Orleans;Integrated Security=True;Pooling=False;Max Pool Size=200;Asynchronous Processing=True;MultipleActiveResultSets=True"</span><span style="color: #ff0000;"> AdoInvariant</span><span style="color: #0000ff;">="System.Data.SqlClient"</span> <span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Globals</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">OrleansConfiguration</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>客户端配置应如下所示：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ClientConfiguration </span><span style="color: #ff0000;">xmlns</span><span style="color: #0000ff;">="urn:orleans"</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">SystemStore </span><span style="color: #ff0000;">SystemStoreType </span><span style="color: #0000ff;">="SqlServer"</span><span style="color: #ff0000;">
                 DeploymentId</span><span style="color: #0000ff;">="OrleansTest"</span><span style="color: #ff0000;">
                 DataConnectionString</span><span style="color: #0000ff;">="Data Source=(localdb)\MSSQLLocalDB;Initial Catalog=Orleans;Integrated Security=True;Pooling=False;Max Pool Size=200;Asynchronous Processing=True;MultipleActiveResultSets=True"</span><span style="color: #ff0000;"> AdoInvariant</span><span style="color: #0000ff;">="System.Data.SqlClient"</span> <span style="color: #0000ff;">/&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">ClientConfiguration</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>DataConnectionString设置为任何有效的SQL Server连接字符串。 为了使用SQL Server作为系统数据存储，现在在Binaries \ OrleansServer文件夹中创建了一个脚本文件CreateOrleansTables _ *.sql（其中asterisk表示数据库供应商），该文件建立必要的数据库对象。 确保将要托管奥尔良仓库的所有服务器都可以访问数据库并拥有访问权限！ 在我们的测试过程中，我们已经绊倒了几次这个看起来微不足道的问题。 请注意，在Orleans 2.0.0中，这些SQL脚本已经被分成了每个功能部件以匹配更细粒度提供者模型：集群，持久性，提醒和统计。</p>
<p>①SQL度量和统计表</p>
<p>系统表目前只能存储在Azure表或SQL服务器中。 但是，对于度量标准和统计表，我们提供一个通用的支持来将其托管在任何持久性存储中。 这是通过StatisticsProvider的概念提供的。 任何应用程序都可以编写任意提供程序来将统计信息和指标数据存储在他们选择的持久存储中。 Orleans提供了一个这样的提供者的实现：SQL Table Statistics Provider。</p>
<p>为了将SQL服务器用于统计和指标表，需要调整服务器端和客户端配置。</p>
<p>服务器配置应该如下所示：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">OrleansConfiguration </span><span style="color: #ff0000;">xmlns</span><span style="color: #0000ff;">="urn:orleans"</span><span style="color: #0000ff;">&gt;</span>
     <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Globals</span><span style="color: #0000ff;">&gt;</span>
         <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">StatisticsProviders</span><span style="color: #0000ff;">&gt;</span>
             <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Provider </span><span style="color: #ff0000;">Type</span><span style="color: #0000ff;">="Orleans.Providers.SqlServer.SqlStatisticsPublisher"</span><span style="color: #ff0000;"> Name</span><span style="color: #0000ff;">="MySQLStatsProvider"</span><span style="color: #ff0000;"> ConnectionString</span><span style="color: #0000ff;">="Data Source=(localdb)\MSSQLLocalDB;Initial Catalog=Orleans;Integrated Security=True;Pooling=False;Max Pool Size=200;Asynchronous Processing=True;MultipleActiveResultSets=True"</span> <span style="color: #0000ff;">/&gt;</span>
         <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">StatisticsProviders</span><span style="color: #0000ff;">&gt;</span>
     <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Globals</span><span style="color: #0000ff;">&gt;</span>
     <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Defaults</span><span style="color: #0000ff;">&gt;</span>
         <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Statistics </span><span style="color: #ff0000;">ProviderType</span><span style="color: #0000ff;">="MySQLStatsProvider"</span><span style="color: #ff0000;"> WriteLogStatisticsToTable</span><span style="color: #0000ff;">="true"</span><span style="color: #0000ff;">/&gt;</span>
     <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Defaults</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">OrleansConfiguration</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>客户端配置应如下所示：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ClientConfiguration </span><span style="color: #ff0000;">xmlns</span><span style="color: #0000ff;">="urn:orleans"</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">StatisticsProviders</span><span style="color: #0000ff;">&gt;</span>
         <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Provider </span><span style="color: #ff0000;">Type</span><span style="color: #0000ff;">="Orleans.Providers.SqlServer.SqlStatisticsPublisher"</span><span style="color: #ff0000;"> Name</span><span style="color: #0000ff;">="SQL"</span><span style="color: #ff0000;"> ConnectionString</span><span style="color: #0000ff;">="Data Source=(localdb)\MSSQLLocalDB;Initial Catalog=Orleans;Integrated Security=True;Pooling=False;Max Pool Size=200;Asynchronous Processing=True;MultipleActiveResultSets=True"</span> <span style="color: #0000ff;">/&gt;</span>
      <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">StatisticsProviders</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Statistics </span><span style="color: #ff0000;">ProviderType</span><span style="color: #0000ff;">="MySQLStatsProvider"</span><span style="color: #ff0000;"> WriteLogStatisticsToTable</span><span style="color: #0000ff;">="true"</span><span style="color: #0000ff;">/&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">ClientConfiguration</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><a name="a2"></a><span style="font-size: 18pt;"><strong><span style="color: #ffffff;">二、监控</span></strong></span></p>
<p><a name="a21"></a>1，运行时监视</p>
<p>[[这是需要审查]]</p>
<p>通过利用Orleans自动向Azure存储写入的数据，外部操作员可以监控Orleans部署的五种方式。</p>
<p>下面提到的表格在这里有更详细的描述。</p>
<p><strong>OrleansSilosTable for cluster membership&nbsp;-</strong>此表列出了部署中的所有silos（分区键DeploymentID，行密钥silosID）。 操作员可以使用此表来检查群集运行状况，查看当前设置的活动silos，或了解某个silos发生故障的原因和时间。 Orleans的集群成员协议在内部使用此表，并用重要的成员事件（silos上下）更新它。</p>
<p><strong>OrleansSiloMetrics表-</strong>&nbsp;grain性能统计 - Orleans在这个表（分区键DeplomentID，行密钥仓库id）中写入了一个小数（约10）的grain性能统计。 该表格每隔X秒（每个silo可配置）自动更新一次。 这些度量指标包括：siloCPU，内存使用情况，该silo中grain激活的数量，发送/接收队列中的消息数量等。这些数据可以用来比较筒仓，检查是否没有明显的异常值（例如， silo运行在更高的CPU上），或者只是简单地检查一下通过grains报告的指标是否在预期的范围内。 此外，如果系统过载，则可以使用此数据决定是否添加新的silos，或者如果系统大部分空闲，则可以减少silos数量。</p>
<p><strong>OrleansSiloStatistics表</strong> - 这个表格包含了更多的性能统计数字（数百个计数器），这些统计数据提供了更详细，更深入的内部silos状态视图。 目前不推荐此表格供外部操作员使用。 主要是Orleans开发商帮助他们解决复杂的生产问题。 Orleans团队正在构建工具来自动分析这些数据，并基于此向运营商提供紧凑的建议。 这些工具也可以由任何人独立建造。</p>
<p><strong>Watching error codes in MDS&nbsp;-</strong>Orleans自动写入不同的错误消息到记录器。 该记录器可以配置为输出其数据到不同的目的地。 例如，Halo团队将生产中的所有日志重定向到MDS。 他们已经在MDS中编写了自定义警报，以监视特定的错误代码并计算它们的发生次数，并在这些阈值达到某个阈值时向其发出警报。 在这里指定要观察的重要错误代码列表：</p>
<ul>
<li>
<p><a href="https://dotnet.github.io/orleans/Documentation/Deployment-and-Operations/Monitoring/Silo-Error-Code-Monitoring.html">Silo Error Code Monitoring</a></p>
</li>
<li>
<p><a href="https://dotnet.github.io/orleans/Documentation/Deployment-and-Operations/Monitoring/Client-Error-Code-Monitoring.html">Client Error Code Monitoring</a></p>
</li>
</ul>
<p><strong>Windows performance counters&nbsp;-</strong>Orleans运行时不断更新其中的一些。 CounterControl.exe帮助注册计数器，并需要以提升的权限运行。 显然，性能计数器可以使用任何标准的监视工具进行监视。</p>
<p><a name="a22"></a>2，silo错误代码监测</p>
<table class="table table-bordered table-striped table-condensed" border="1">
<thead>
<tr><th>Group</th><th>Log Type</th><th>Log Code Values</th><th>Threshold</th><th>Description</th></tr>
</thead>
<tbody>
<tr>
<td>Azure Problems</td>
<td>Warning or Error</td>
<td>100800 - 100899</td>
<td>Any Error or Warning</td>
<td>读取或写入Azure表存储的瞬间问题将被记录为警告。 瞬时读取错误将自动重试。 最终的错误日志消息意味着连接到Azure表存储存在真正的问题。</td>
</tr>
<tr>
<td>Membership Connectivity Problems</td>
<td>Warning or Error</td>
<td>100600 - 100699</td>
<td>Any Error or Warning</td>
<td>警告日志是网络连接问题和/或silo重新启动/迁移的早期指示。 Ping超时和silo投票将显示为警告消息。 筒仓厌恶它被投票死了将显示为错误消息。</td>
</tr>
<tr>
<td>Grain call timeouts</td>
<td>Warning</td>
<td>100157</td>
<td>Multiple Warnings logged in short space of time</td>
<td>grain调用超时问题通常是由临时网络连接问题或silo重启/重启问题引起的。 系统应该在短时间后恢复（取决于Liveness配置设置），超时应该清除。 理想情况下，只监视这些警告的大量日志代码600157应该是足够的。</td>
</tr>
<tr>
<td>Silo Restart / Migration</td>
<td>Warning</td>
<td>100601 or 100602</td>
<td>Any Warning</td>
<td>silo检测到它在同一台机器上重新启动（100602）或迁移到其他机器（100601）</td>
</tr>
<tr>
<td>Network Socket Problems</td>
<td>Warning or Error</td>
<td>101000 to 101999, 100307,100015, 100016</td>
<td>Any Error or Warning</td>
<td>套接字断开被记录为警告消息。 打开套接字或发送消息时出现的问题记录为错误。</td>
</tr>
<tr>
<td>Bulk log message compaction</td>
<td>Any</td>
<td>500000 or higher</td>
<td>Message summary based on bulk message threshold settings</td>
<td>如果在指定的时间间隔内出现了多个相同日志代码的日志（缺省值在1分钟内大于5），则会删除包含该日志代码的其他日志消息，并将其输出为日志代码等于原始日志的&ldquo;批量&rdquo;条目 代码+ 500000.例如，多个100157条目将在日志中显示为每分钟5 x 100157 + 1 x 600157条目。</td>
</tr>
<tr>
<td>Grain problems</td>
<td>Warning or Error</td>
<td>101534</td>
<td>Any Error or Warning</td>
<td>检测对非折返grain的&ldquo;stuck&rdquo;请求。 每次请求花费超过5倍的请求超时时间执行时，都会报告错误代码。</td>
</tr>
</tbody>
</table>
<p><a name="a23"></a>3，客户端错误代码监测</p>
<table class="table table-bordered table-striped table-condensed" border="1">
<thead>
<tr><th>Group</th><th>Log Type</th><th>Log Code Values</th><th>Threshold</th><th>Description</th></tr>
</thead>
<tbody>
<tr>
<td>Azure Problems</td>
<td>Warning or Error</td>
<td>100800 - 100899</td>
<td>Any Error or Warning</td>
<td>读取或写入Azure表存储的瞬间问题将被记录为警告。 瞬时读取错误将自动重试。 最终的错误日志消息意味着连接到Azure表存储存在真正的问题。</td>
</tr>
<tr>
<td>Gateway connectivity problems</td>
<td>Warning or Error</td>
<td>100901 - 100904, 100912, 100913, 100921, 100923, 100158, 100161, 100178, , 101313</td>
<td>Any Error or Warning</td>
<td>连接到网关的问题。 Azure表中没有活动的网关。 连接到活动网关丢失。</td>
</tr>
<tr>
<td>Grain call timeouts</td>
<td>Warning</td>
<td>100157</td>
<td>Multiple Warnings logged in short space of time</td>
<td>grain调用超时问题通常是由临时网络连接问题或silos重启/重启问题引起的。 系统应该在短时间后恢复（取决于Liveness配置设置），超时应该清除。 理想情况下，只监视这些警告的大量日志代码600157应该是足够的。</td>
</tr>
<tr>
<td>Network Socket Problems</td>
<td>Warning or Error</td>
<td>101000 to 101999, 100307, 100015, 100016</td>
<td>Any Error or Warning</td>
<td>套接字断开被记录为警告消息。 打开套接字或发送消息时出现的问题记录为错误。</td>
</tr>
<tr>
<td>Bulk log message compaction</td>
<td>Any</td>
<td>500000 or higher</td>
<td>Message summary based on bulk message threshold settings</td>
<td>如果在指定的时间间隔内出现了多个相同日志代码的日志（缺省值在1分钟内大于5），则会删除包含该日志代码的其他日志消息，并将其输出为日志代码等于原始日志的&ldquo;批量&rdquo;条目 代码+ 500000.例如，多个100157条目将在日志中显示为每分钟5 x 100157 + 1 x 600157条目。</td>
</tr>
</tbody>
</table>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">三、<a name="a24"></a>解决部署问题</span></strong></p>
<p>&nbsp;本页提供了一些常规指导，可用于解决部署到Azure云服务时出现的任何问题。 这些是需要注意的常见问题。 请务必检查日志以获取更多信息。</p>
<p>1，获得一个SiloUnavailableException</p>
<p>首先检查一下，确保在尝试初始化客户端之前确实启动了筒仓。 有时silo需要很长时间才能启动，所以尝试多次初始化客户端可能会有所帮助。 如果它仍然抛出一个异常，那么silos可能会有另一个问题。检查silo配置，确保silo正确启动。</p>
<p>2，常见连接字符串问题</p>
<ul>
<li>部署到Azure时使用本地连接字符串 - 网站将无法连接</li>
<li>对silos和前端（web和worker角色）使用不同的连接字符串 - 网站将无法初始化客户端，因为它无法连接到silos</li>
</ul>
<p>可以在Azure门户中检查连接字符串配置。 如果连接字符串设置不正确，日志可能无法正确显示。</p>
<p>3，修改配置文件不当</p>
<p>确保在ServiceDefinition.csdef文件中配置了正确的端点，否则部署将不起作用。 它会给出错误，说明它不能获取端点信息。</p>
<p>4，缺少日志</p>
<p>确保连接字符串设置正确。</p>
<p>Web角色中的Web.config文件或worker角色中的app.config文件可能被错误地修改。 这些文件中的不正确版本可能会导致部署问题。 处理更新时要小心。</p>
<p>6，版本问题</p>
<p>确保解决方案中的每个项目都使用相同版本的Orleans。 不这样做可以导致员工角色回收。 检查日志以获取更多信息。 Visual Studio在部署历史记录中提供了一些silo启动错误消息。</p>
<p>7，角色不断回收</p>
<ul>
<li>检查所有合适的Orleans程序集是否在解决方案中，并将Copy Local设置为True。</li>
<li>检查日志以查看初始化时是否有未处理的异常。</li>
<li>确保连接字符串是正确的。</li>
<li>查看Azure云服务疑难解答页面以获取更多信息。</li>
</ul>
<p>8，如何检查日志</p>
<ul>
<li>使用Visual Studio中的云资源管理器导航到存储帐户中适当的存储表或blob。 WADLogsTable是查看日志的好起点。</li>
<li>您可能只会记录错误。 如果您还需要信息日志，则需要修改配置以设置日志严重性级别。</li>
</ul>
<p>编程配置：</p>
<ul>
<li>创建ClusterConfiguration对象时，请设置config.Defaults.DefaultTraceLevel = Severity.Info。</li>
<li>创建ClientConfiguration对象时，请设置config.DefaultTraceLevel = Severity.Info。</li>
</ul>
<p>声明式配置：</p>
<ul>
<li>将&lt;Tracing DefaultTraceLevel =&ldquo;Info&rdquo;/&gt;添加到OrleansConfiguration.xml和/或ClientConfiguration.xml文件中。</li>
</ul>
<p>在Web和辅助角色的diagnostics.wadcfgx文件中，请确保将Logs元素中的scheduledTransferLogLevelFilter属性设置为Information，因为这是一个额外的跟踪筛选层，它定义将哪些跟踪发送到Azure存储中的WADLogsTable。</p>
<p>在&ldquo;配置指南&rdquo;中可以找到关于此的更多信息。</p>
<p>8，与ASP.NET兼容</p>
<p>ASP.NET中包含的razor视图引擎使用与Orleans（Microsoft.CodeAnalysis和Microsoft.CodeAnalysis.CSharp）相同的代码生成程序集。 这可能会在运行时出现版本兼容性问题。</p>
<p>要解决此问题，请尝试将Microsoft.CodeDom.Providers.DotNetCompilerPlatform（这是ASP.NET用来包含上述程序集的NuGet程序包）升级到最新版本，并设置绑定重定向，如下所示：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">dependentAssembly</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">assemblyIdentity </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="Microsoft.CodeAnalysis.CSharp"</span><span style="color: #ff0000;"> publicKeyToken</span><span style="color: #0000ff;">="31bf3856ad364e35"</span><span style="color: #ff0000;"> culture</span><span style="color: #0000ff;">="neutral"</span> <span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">bindingRedirect </span><span style="color: #ff0000;">oldVersion</span><span style="color: #0000ff;">="0.0.0.0-2.0.0.0"</span><span style="color: #ff0000;"> newVersion</span><span style="color: #0000ff;">="1.3.1.0"</span> <span style="color: #0000ff;">/&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">dependentAssembly</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">dependentAssembly</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">assemblyIdentity </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="Microsoft.CodeAnalysis"</span><span style="color: #ff0000;"> publicKeyToken</span><span style="color: #0000ff;">="31bf3856ad364e35"</span><span style="color: #ff0000;"> culture</span><span style="color: #0000ff;">="neutral"</span> <span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">bindingRedirect </span><span style="color: #ff0000;">oldVersion</span><span style="color: #0000ff;">="0.0.0.0-2.0.0.0"</span><span style="color: #ff0000;"> newVersion</span><span style="color: #0000ff;">="1.3.1.0"</span> <span style="color: #0000ff;">/&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">dependentAssembly</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">四、<a name="a25"></a>异构silos</span></strong></p>
<p>&nbsp;概观在给定的集群上，筒仓可以支持一组不同的grain类型：</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201801/741594-20180128144115350-364282730.png" alt="" /></p>
<p>在这个例子中，集群支持类型A，B，C，D，E：</p>
<ul>
<li>grain种类A和B可以放置在silo1和2上。</li>
<li>grain类型C可以被放置在silo1,2或3。</li>
<li>grain类型D只能放在silo3上</li>
<li>grain类型E只能放在silo4上。</li>
</ul>
<p>所有的silo都应该引用所有的grain类型的接口，但是grain类只应该被容纳它们的silo所引用。</p>
<p>客户端不知道哪个silo支持给定的grain类型。</p>
<p>给定的Grain Type实现必须在支持它的每个silo中相同。 以下情况无效：</p>
<p>在silo1和2：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> C: Grain, IMyGrainInterface
{
   </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Task SomeMethod() { &hellip; }
}</span></pre>
</div>
<p>在silo3：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> C: Grain, IMyGrainInterface, IMyOtherGrainInterface
{
   </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Task SomeMethod() { &hellip; }
   </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Task SomeOtherMethod() { &hellip; }
}</span></pre>
</div>
<p>1，配置</p>
<p>不需要配置，您可以在群集中的每个silo上部署不同的二进制文件。 但是，如有必要，可以更改silos检查ClusterConfig.Globals.TypeMapRefreshInterval中支持的类型更改的时间间隔。出于测试目的，您可以在NodeConfiguration中使用ExcludedGrainTypes属性。 在基于代码的配置中，您可以在ClusterConfig.Defaults.ExcludedGrainTypes中找到它，它是要排除的类型的列表名称。</p>
<p>2，限制</p>
<ul>
<li>如果支持的&ldquo;grain类型&rdquo;集合发生更改，则不会通知连接的客户端。 在前面的例子中：<br />
<ul>
<li>如果Silo 4离开集群，客户端仍然会尝试调用E类型的grain。在运行时OrleansException会失败。</li>
<li>如果在Silo 4加入之前，客户端连接到群集，客户端将无法调用E类型的谷物。它将失败一个ArgumentException</li>








</ul>








</li>
<li>不支持无状态grain：群集中的所有silo必须支持同一组无状态grain。</li>








</ul>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">五、<a name="a26"></a>开始使用Azure Web Apps</span></strong></p>
<p>如果您想从Azure Web App连接到Azure Silo，而不是在同一云服务中托管的Web Role，则可以。&nbsp;</p>
<p>为了安全工作，您需要将Azure Web App和托管Silo的Worker角色分配给Azure虚拟网络。</p>
<p>首先，我们将设置Azure Web App，您可以按照本指南创建虚拟网络并将其分配给Azure Web App。</p>
<p>现在我们可以通过修改ServiceConfiguration文件来将云服务分配给虚拟网络。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">NetworkConfiguration</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">VirtualNetworkSite </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="virtual-network-name"</span> <span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">AddressAssignments</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">InstanceAddress </span><span style="color: #ff0000;">roleName</span><span style="color: #0000ff;">="role-name"</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Subnets</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Subnet </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="subnet-name"</span> <span style="color: #0000ff;">/&gt;</span>
      <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Subnets</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">InstanceAddress</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">AddressAssignments</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">NetworkConfiguration</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>还要确保silo端点已配置。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Endpoints</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">InternalEndpoint </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="OrleansSiloEndpoint"</span><span style="color: #ff0000;"> protocol</span><span style="color: #0000ff;">="tcp"</span><span style="color: #ff0000;"> port</span><span style="color: #0000ff;">="11111"</span> <span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">InternalEndpoint </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="OrleansProxyEndpoint"</span><span style="color: #ff0000;"> protocol</span><span style="color: #0000ff;">="tcp"</span><span style="color: #ff0000;"> port</span><span style="color: #0000ff;">="30000"</span> <span style="color: #0000ff;">/&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Endpoints</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>最后，您需要为silos和Web应用程序客户端指定相同的部署ID。</p>
<p>您现在可以使用GrainClient从Web App连接到silo。</p>
<p>1，潜在的问题</p>
<p>如果Web应用程序无法连接到筒仓：</p>
<ul>
<li>确保您的Azure云服务中至少有两个角色或两个角色，或者不能生成InternalEndpoint防火墙规则。</li>
<li>检查Web应用程序和silo是否使用相同的DeploymentId。</li>
<li>确保网络安全组已设置为允许内部虚拟网络连接。 如果你没有一个你可以使用下面的PowerShell轻松地创建和分配一个：</li>
</ul>
<div class="cnblogs_code">
<pre><span style="color: #000000;">New-AzureNetworkSecurityGroup -Name "Default" -Location "North Europe"
Get-AzureNetworkSecurityGroup -Name "Default" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName "virtual-network-name" -SubnetName "subnet-name"</span></pre>
</div>
<p style="background-color: #169fe6;"><span style="font-size: 18pt;"><strong><span style="color: #ffffff;">六、<a name="a27"></a>Docker部署</span></strong></span></p>
<p>1，部署Orleans解决方案到Docker</p>
<p>考虑到Docker协调器和集群堆栈的设计方式，将Orleans部署到Docker可能会非常棘手。 最复杂的是从Docker Swarm和Kubernets Networking模型中理解覆盖网络的概念。</p>
<p>Docker容器和网络模型被设计为运行大多数无状态和不可变的容器。 因此，启动一个运行node.js或nginx应用程序的集群是相当容易的。 但是，如果您尝试使用更复杂的东西，比如真正的集群或分布式应用程序（例如基于Orleans的应用程序），您最终会遇到麻烦。 这是可能的，但不像基于网络的应用程序那样简单。</p>
<p>Docker集群包括将多个主机放在一起，作为使用Container Orchestrator管理的单个资源池。 Docker Inc.提供Swarm作为Container Orchestration的选项，而Google则提供Kubernetes（又名K8s）。 还有其他的Orchestrator，如DC / OS，Mesos等，但是在这个文档中我们将会讨论Swarm和K8s，因为它们被更广泛地使用。</p>
<p>在Orleans的任何地方运行的相同的grain接口和实现已经被支持，也将在Docker容器上运行，所以为了能够在Docker容器中运行你的应用程序，不需要特别的考虑。</p>
<p>Orleans-Docker示例提供了如何运行两个控制台应用程序的工作示例。 一个作为Orleans客户，另一个作为silo，细节描述如下。</p>
<p>这里讨论的概念可以用在Orleans的.Net Core和.Net 4.6.1版本中，但为了说明Docker和.Net Core的跨平台性质，我们将着重考虑你正在使用的例子。 净核心。 本文可能会提供特定于平台（Windows / Linux / OSX）的详细信息。</p>
<p>2，先决条件</p>
<p>本文假定您已经安装了以下先决条件：</p>
<ul>
<li><a href="https://www.docker.com/community-edition#/download">Docker</a>&nbsp;-&nbsp;Docker4X有一个易于使用的主要支持平台的安装程序。 它包含Docker引擎和Docker Swarm。</li>
<li><a href="https://kubernetes.io/docs/tutorials/stateless-application/hello-minikube/">Kubernetes (K8s)</a>&nbsp;-&nbsp;Google提供的Container Orchestration。 它包含安装Minikube（K8s的本地部署）和kubectl及其所有依赖项的指导。</li>
<li><a href="https://dot.net/">.Net Core</a>&nbsp;-&nbsp;.Net的跨平台</li>
<li><a href="https://code.visualstudio.com/">Visual Studio Code (VSCode)</a>&nbsp;- 你可以使用任何你想要的IDE。 VSCode是跨平台的，所以我们正在使用它来确保它在所有平台上都能正常工作。 一旦你安装VSCode，安装&nbsp;<a href="https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp">C# extension</a>.</li>
</ul>
<p>注意：如果您不打算使用它，则不需要安装Kubernetes。 Docker4X安装程序已经包含了Swarm，因此不需要额外安装即可使用它。</p>
<p>Windows用户注意事项：在Windows上，Docker安装程序将在安装过程中启用Hyper-V。 由于本文及其示例使用.Net Core，所使用的容器映像基于Windows Server NanoServer。 如果你不打算使用.Net coew，并将目标.NET 4.6.1完整的框架，使用的图像应该是Windows Server Core和Orleans的1.4 +版本（只支持.net完整框架）。</p>
<p>3，创建Orleans解决方案</p>
<p>以下说明显示了如何使用新的dotnet工具创建常规的Orleans解决方案。</p>
<p>注意：请根据您的平台适当调整命令。 而且，目录结构只是一个建议。 请随意调整它。</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">mkdir Orleans-Docker
cd Orleans-Docker
dotnet new sln
mkdir -p src/OrleansSilo
mkdir -p src/OrleansClient
mkdir -p src/OrleansGrains
mkdir -p src/OrleansGrainInterfaces
dotnet new console -o src/OrleansSilo --framework netcoreapp1.</span>1<span style="color: #000000;">
dotnet new console -o src/OrleansClient --framework netcoreapp1.</span>1<span style="color: #000000;">
dotnet new classlib -o src/OrleansGrains --framework netstandard1.</span>5<span style="color: #000000;">
dotnet new classlib -o src/OrleansGrainInterfaces --framework netstandard1.</span>5<span style="color: #000000;">
dotnet sln add src/OrleansSilo/OrleansSilo.csproj
dotnet sln add src/OrleansClient/OrleansClient.csproj
dotnet sln add src/OrleansGrains/OrleansGrains.csproj
dotnet sln add src/OrleansGrainInterfaces/OrleansGrainInterfaces.csproj
dotnet add src/OrleansClient/OrleansClient.csproj reference src/OrleansGrainInterfaces/OrleansGrainInterfaces.csproj
dotnet add src/OrleansSilo/OrleansSilo.csproj reference src/OrleansGrainInterfaces/OrleansGrainInterfaces.csproj
dotnet add src/OrleansGrains/OrleansGrains.csproj reference src/OrleansGrainInterfaces/OrleansGrainInterfaces.csproj
dotnet add src/OrleansSilo/OrleansSilo.csproj reference src/OrleansGrains/OrleansGrains.csproj</span></pre>
</div>
<p>到目前为止，我们所做的仅仅是样板代码来创建解决方案结构，项目，并在项目之间添加引用。 没有什么比普通的Orleans项目不同。</p>
<p>在写这篇文章的时候，Orleans 2.0（这是唯一支持.Net Core和跨平台的版本）在技术预览版中，所以它的核心部分被托管在一个MyGet源中，而不是发布到Nuget.org的官方源。 为了安装预览版本，我们将使用dotnet cli强制MyGet的源代码和版本：</p>
<div class="cnblogs_code">
<pre>dotnet add src/OrleansClient/OrleansClient.csproj package Microsoft.Orleans.Core -s https://dotnet.myget.org/F/orleans-prerelease/api/v3/index.json -v 2.0.0-preview2-201705020000
dotnet add src/OrleansGrainInterfaces/OrleansGrainInterfaces.csproj package Microsoft.Orleans.Core -s https://dotnet.myget.org/F/orleans-prerelease/api/v3/index.json -v 2.0.0-preview2-201705020000
dotnet add src/OrleansGrains/OrleansGrains.csproj package Microsoft.Orleans.Core -s https://dotnet.myget.org/F/orleans-prerelease/api/v3/index.json -v 2.0.0-preview2-201705020000
dotnet add src/OrleansSilo/OrleansSilo.csproj package Microsoft.Orleans.Core -s https://dotnet.myget.org/F/orleans-prerelease/api/v3/index.json -v 2.0.0-preview2-201705020000
dotnet add src/OrleansSilo/OrleansSilo.csproj package Microsoft.Orleans.OrleansRuntime -s https://dotnet.myget.org/F/orleans-prerelease/api/v3/index.json -v 2.0.0-preview2-201705020000
dotnet restore</pre>
</div>
<p>好的，现在你拥有了运行一个简单的Orleans应用程序的所有基本的依赖关系。 请注意，迄今为止，您的常规Orleans应用程序没有任何变化。 现在，让我们添加一些代码，以便我们可以做一些事情。</p>
<p>4，实施你的Orleans应用程序</p>
<p>假设您正在使用VSCode，从解决方案目录中运行代码。这将打开VSCode中的目录并加载解决方案。</p>
<p>这是我们以前创建的解决方案结构。</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201801/741594-20180128151937100-405507371.png" alt="" /></p>
<p>我们还将Program.cs，OrleansHostWrapper，IGreetingGrain和GreetingGrain文件分别添加到接口和grain项目，这里是这些文件的代码：</p>
<p><code>IGreetingGrain.cs</code>:</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('62f87650-87cf-4ecb-ad75-3b83cb3b3390')"><img id="code_img_closed_62f87650-87cf-4ecb-ad75-3b83cb3b3390" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_62f87650-87cf-4ecb-ad75-3b83cb3b3390" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('62f87650-87cf-4ecb-ad75-3b83cb3b3390',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_62f87650-87cf-4ecb-ad75-3b83cb3b3390" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Orleans;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> OrleansGrainInterfaces
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IGreetingGrain : IGrainWithGuidKey
    {
        Task</span>&lt;<span style="color: #0000ff;">string</span>&gt; SayHello(<span style="color: #0000ff;">string</span><span style="color: #000000;"> name);
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">IGreetingGrain.cs</span></div>
<p><code>GreetingGrain.cs</code>:</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('52f60099-d6c2-40a1-b83f-685bc6b127a7')"><img id="code_img_closed_52f60099-d6c2-40a1-b83f-685bc6b127a7" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_52f60099-d6c2-40a1-b83f-685bc6b127a7" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('52f60099-d6c2-40a1-b83f-685bc6b127a7',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_52f60099-d6c2-40a1-b83f-685bc6b127a7" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> OrleansGrainInterfaces;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> OrleansGrains
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> GreetingGrain : Grain, IGreetingGrain
    {
        </span><span style="color: #0000ff;">public</span> Task&lt;<span style="color: #0000ff;">string</span>&gt; SayHello(<span style="color: #0000ff;">string</span><span style="color: #000000;"> name)
        {
            </span><span style="color: #0000ff;">return</span> Task.FromResult($<span style="color: #800000;">"</span><span style="color: #800000;">Hello from Orleans, {name}</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">GreetingGrain.cs</span></div>
<p><code>OrleansHostWrapper.cs</code>:</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('f612a32b-7d1b-42e3-aead-2b05da2c860c')"><img id="code_img_closed_f612a32b-7d1b-42e3-aead-2b05da2c860c" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_f612a32b-7d1b-42e3-aead-2b05da2c860c" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('f612a32b-7d1b-42e3-aead-2b05da2c860c',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_f612a32b-7d1b-42e3-aead-2b05da2c860c" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Net;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Orleans.Runtime;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Orleans.Runtime.Configuration;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Orleans.Runtime.Host;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> OrleansSilo
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> OrleansHostWrapper
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> SiloHost siloHost;

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> OrleansHostWrapper(ClusterConfiguration config)
        {
            siloHost </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> SiloHost(Dns.GetHostName(), config);
            siloHost.LoadOrleansConfig();
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span><span style="color: #000000;"> Run()
        {
            </span><span style="color: #0000ff;">if</span> (siloHost == <span style="color: #0000ff;">null</span><span style="color: #000000;">)
            {
                </span><span style="color: #0000ff;">return</span> <span style="color: #800080;">1</span><span style="color: #000000;">;
            }

            </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
            {
                siloHost.InitializeOrleansSilo();

                </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (siloHost.StartOrleansSilo())
                {
                    Console.WriteLine($</span><span style="color: #800000;">"</span><span style="color: #800000;">Successfully started Orleans silo '{siloHost.Name}' as a {siloHost.Type} node.</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                    </span><span style="color: #0000ff;">return</span> <span style="color: #800080;">0</span><span style="color: #000000;">;
                }
                </span><span style="color: #0000ff;">else</span><span style="color: #000000;">
                {
                    </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> OrleansException($<span style="color: #800000;">"</span><span style="color: #800000;">Failed to start Orleans silo '{siloHost.Name}' as a {siloHost.Type} node.</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                }
            }
            </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (Exception exc)
            {
                siloHost.ReportStartupError(exc);
                Console.Error.WriteLine(exc);
                </span><span style="color: #0000ff;">return</span> <span style="color: #800080;">1</span><span style="color: #000000;">;
            }
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span><span style="color: #000000;"> Stop()
        {
            </span><span style="color: #0000ff;">if</span> (siloHost != <span style="color: #0000ff;">null</span><span style="color: #000000;">)
            {
                </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
                {
                    siloHost.StopOrleansSilo();
                    siloHost.Dispose();
                    Console.WriteLine($</span><span style="color: #800000;">"</span><span style="color: #800000;">Orleans silo '{siloHost.Name}' shutdown.</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                }
                </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (Exception exc)
                {
                    siloHost.ReportStartupError(exc);
                    Console.Error.WriteLine(exc);
                    </span><span style="color: #0000ff;">return</span> <span style="color: #800080;">1</span><span style="color: #000000;">;
                }
            }
            </span><span style="color: #0000ff;">return</span> <span style="color: #800080;">0</span><span style="color: #000000;">;
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">OrleansHostWrapper.cs</span></div>
<p><code>Program.cs</code>&nbsp;(Silo):</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('a9602c0a-24d1-48e8-81ef-e4cce71b10d2')"><img id="code_img_closed_a9602c0a-24d1-48e8-81ef-e4cce71b10d2" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_a9602c0a-24d1-48e8-81ef-e4cce71b10d2" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('a9602c0a-24d1-48e8-81ef-e4cce71b10d2',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_a9602c0a-24d1-48e8-81ef-e4cce71b10d2" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Net;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Orleans.Runtime.Configuration;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> OrleansSilo
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> OrleansHostWrapper hostWrapper;

        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">int</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #0000ff;">int</span> exitCode =<span style="color: #000000;"> InitializeOrleans();

            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">Press Enter to terminate...</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            Console.ReadLine();

            exitCode </span>+=<span style="color: #000000;"> ShutdownSilo();

            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> exitCode;
        }

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">int</span><span style="color: #000000;"> InitializeOrleans()
        {
            </span><span style="color: #0000ff;">var</span> config = <span style="color: #0000ff;">new</span><span style="color: #000000;"> ClusterConfiguration();
            config.Globals.DataConnectionString </span>= <span style="color: #800000;">"</span><span style="color: #800000;">[AZURE STORAGE CONNECTION STRING HERE]</span><span style="color: #800000;">"</span><span style="color: #000000;">;
            config.Globals.DeploymentId </span>= <span style="color: #800000;">"</span><span style="color: #800000;">Orleans-Docker</span><span style="color: #800000;">"</span><span style="color: #000000;">;
            config.Globals.LivenessType </span>=<span style="color: #000000;"> GlobalConfiguration.LivenessProviderType.AzureTable;
            config.Globals.ReminderServiceType </span>=<span style="color: #000000;"> GlobalConfiguration.ReminderServiceProviderType.AzureTable;
            config.Defaults.PropagateActivityId </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">;
            config.Defaults.ProxyGatewayEndpoint </span>= <span style="color: #0000ff;">new</span> IPEndPoint(IPAddress.Any, <span style="color: #800080;">10400</span><span style="color: #000000;">);
            config.Defaults.Port </span>= <span style="color: #800080;">10300</span><span style="color: #000000;">;
            </span><span style="color: #0000ff;">var</span> ips =<span style="color: #000000;"> Dns.GetHostAddressesAsync(Dns.GetHostName()).Result;
            config.Defaults.HostNameOrIPAddress </span>= ips.FirstOrDefault()?<span style="color: #000000;">.ToString();
            hostWrapper </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> OrleansHostWrapper(config);
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> hostWrapper.Run();
        }

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">int</span><span style="color: #000000;"> ShutdownSilo()
        {
            </span><span style="color: #0000ff;">if</span> (hostWrapper != <span style="color: #0000ff;">null</span><span style="color: #000000;">)
            {
                </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> hostWrapper.Stop();
            }
            </span><span style="color: #0000ff;">return</span> <span style="color: #800080;">0</span><span style="color: #000000;">;
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Program.cs (Silo)</span></div>
<p><code>Program.cs</code>(client):</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('e47ac866-957b-46ae-8c76-0c7ed479ac96')"><img id="code_img_closed_e47ac866-957b-46ae-8c76-0c7ed479ac96" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_e47ac866-957b-46ae-8c76-0c7ed479ac96" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('e47ac866-957b-46ae-8c76-0c7ed479ac96',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_e47ac866-957b-46ae-8c76-0c7ed479ac96" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Net;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Orleans;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Orleans.Runtime.Configuration;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> OrleansGrainInterfaces;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> OrleansClient
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> IClusterClient client;
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">bool</span><span style="color: #000000;"> running;

        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            Task.Run(() </span>=&gt;<span style="color: #000000;"> InitializeOrleans());

            Console.ReadLine();

            running </span>= <span style="color: #0000ff;">false</span><span style="color: #000000;">;
        }

        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">async</span><span style="color: #000000;"> Task InitializeOrleans()
        {
            </span><span style="color: #0000ff;">var</span> config = <span style="color: #0000ff;">new</span><span style="color: #000000;"> ClientConfiguration();
            config.DeploymentId </span>= <span style="color: #800000;">"</span><span style="color: #800000;">Orleans-Docker</span><span style="color: #800000;">"</span><span style="color: #000000;">;
            config.PropagateActivityId </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">;
            </span><span style="color: #0000ff;">var</span> hostEntry = <span style="color: #0000ff;">await</span> Dns.GetHostEntryAsync(<span style="color: #800000;">"</span><span style="color: #800000;">orleans-silo</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            </span><span style="color: #0000ff;">var</span> ip = hostEntry.AddressList[<span style="color: #800080;">0</span><span style="color: #000000;">];
            config.Gateways.Add(</span><span style="color: #0000ff;">new</span> IPEndPoint(ip, <span style="color: #800080;">10400</span><span style="color: #000000;">));

            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">Initializing...</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            client </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> ClientBuilder().UseConfiguration(config).Build();
            </span><span style="color: #0000ff;">await</span><span style="color: #000000;"> client.Connect();
            running </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">;
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">Initialized!</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            </span><span style="color: #0000ff;">var</span> grain = client.GetGrain&lt;IGreetingGrain&gt;<span style="color: #000000;">(Guid.Empty);

            </span><span style="color: #0000ff;">while</span><span style="color: #000000;">(running)
            {
                </span><span style="color: #0000ff;">var</span> response = <span style="color: #0000ff;">await</span> grain.SayHello(<span style="color: #800000;">"</span><span style="color: #800000;">Gutemberg</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                Console.WriteLine($</span><span style="color: #800000;">"</span><span style="color: #800000;">[{DateTime.UtcNow}] - {response}</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                </span><span style="color: #0000ff;">await</span> Task.Delay(<span style="color: #800080;">1000</span><span style="color: #000000;">);
            }
            client.Dispose();
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Program.cs(client)</span></div>
<p>我们不在这里详细介绍grain的实施情况，因为它超出了本文的范围。 请检查与其相关的其他文件。 这些文件本质上是一个最小的Orleans应用程序，我们将从它开始继续本文的其余部分。</p>
<p>5，网关配置</p>
<p>您可能已经注意到我们在客户端配置中没有使用成员资格提供者。 之所以这样（我经历了与Docker人讨论的日子之后才想到）是因为我们的客户端 - &gt;membership&nbsp;- &gt;网关 - &gt;silo的工作方式与Docker覆盖网络的设计方式不兼容。</p>
<p>我们发现解决这个限制的方法是手动将网关添加到客户端配置中，如下所示：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> hostEntry = <span style="color: #0000ff;">await</span> Dns.GetHostEntryAsync(<span style="color: #800000;">"</span><span style="color: #800000;">orleans-silo</span><span style="color: #800000;">"</span><span style="color: #000000;">);
</span><span style="color: #0000ff;">var</span> ip = hostEntry.AddressList[<span style="color: #800080;">0</span><span style="color: #000000;">];
config.Gateways.Add(</span><span style="color: #0000ff;">new</span> IPEndPoint(ip, <span style="color: #800080;">10400</span>));</pre>
</div>
<p>这里的字符串orleans-silo基本上是docker-compose中使用的服务名称，稍后我们将深入研究更多细节（继续阅读！）。 它将解析到同一服务中的其中一个容器的ips（如Load Balancer）。 在docker-compose项目中，服务是一个给定容器的多个（完全相同）的实例。 例如，我们将为我们的OrleansSilo项目提供服务。 在该服务中，我们将能够水平地上下扩展服务，并将这些容器中的每一个添加到Orleans集群中，并自动遵守Orleans成员协议。 稍后更多。</p>
<p>注意：在本文中，我们使用OrleansAzureUtils成员资格提供者，但是您可以使用Orleans已经支持的任何其他资源。</p>
<p>6，Dockerfile</p>
<p>为了创建你的容器，Docker使用图像。 有关如何创建自己的更多详细信息，可以查看Docker文档。 在这篇文章中，我们将使用官方的微软图像。 基于目标和开发平台，您需要选择合适的图像。 在本文中，我们使用microsoft / dotnet：1.1.2-sdk这是一个基于linux的镜像。 例如，您可以使用microsoft / dotnet：1.1.2-sdk-nanoserver。 选一个适合你的需求。</p>
<p>Windows用户注意：如前所述，为了实现跨平台，本文使用.Net Core和Orleans Technical preview 2.0。 如果您想在Windows上使用Docker，并且完全发布Orleans 1.4+，则需要使用基于NanoServer和Linux的图像的基于Windows Server Core的映像，仅支持.Net Core。</p>
<p><code>Dockerfile.debug</code>:</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;">FROM</span> microsoft/dotnet:1.1.2<span style="color: #000000;">-sdk
</span><span style="color: #008080;">ENV</span><span style="color: #000000;"> NUGET_XMLDOC_MODE skip
</span><span style="color: #008080;">WORKDIR</span><span style="color: #000000;"> /vsdbg
</span><span style="color: #008080;">RUN</span><span style="color: #000000;"> apt-get update \
    &amp;&amp; apt-get install -y --no-install-recommends \
        unzip \
    &amp;&amp; rm -rf /var/lib/apt/lists</span>/*<span style="color: #000000;"> \
    &amp;&amp; curl -sSL </span><span style="color: #000000; text-decoration: underline;">https://aka.ms/getvsdbgsh</span><span style="color: #000000;"> | bash /dev/stdin -v latest -l /vsdbg 
WORKDIR /app
ENTRYPOINT ["tail", "-f", "/dev/null"]</span></pre>
</div>
<p>这dockerfile本质上下载并安装VSdbg调试器，并启动一个空的容器，并保持它永远活着，所以我们不需要拆除/调试时。</p>
<p>现在，为了生产，图像比较小，因为它只包含.Net Core运行时，而不是整个SDK，而且dockerfile有点简单：</p>
<p><code>Dockerfile</code>:</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;">FROM</span> microsoft/dotnet:1.1.2<span style="color: #000000;">-runtime
</span><span style="color: #008080;">WORKDIR</span><span style="color: #000000;"> /app
</span><span style="color: #008080;">ENTRYPOINT</span> ["dotnet", "OrleansSilo.dll"<span style="color: #000000;">]
</span><span style="color: #008080;">COPY</span> . /app</pre>
</div>
<p>7，docker-compose</p>
<p>docker-compose.yml文件实质上是在服务级别上打包了一组服务及其依赖关系。 每个服务都包含给定容器的一个或多个实例，该实例基于您在Dockerfile上选择的映像</p>
<p>对于Orleans部署，一个常见的用例是有一个包含两个服务的docker-compose.yml。 一个为Orleans silo，另一个为Orleans客户端。 客户将依赖于silo，这意味着，只有在silo服务启动后才会开始。 另一种情况是添加一个存储/数据库服务/容器，比如SQL Server，它应该在客户端和服务器之前先启动，所以两个服务都应该依赖它。</p>
<p>注意：在进一步阅读之前（最终会发疯），请注意在docker-compose文件中缩进很重要。 所以如果你有任何问题，请注意。</p>
<p>以下是我们将如何描述这篇文章的服务：</p>
<p><code>docker-compose.override.yml</code>&nbsp;(Debug):</p>
<div class="cnblogs_code">
<pre>version: '3.1'<span style="color: #000000;">

services:
  orleans-client:
    image: orleans-client:debug
    build:
      context: ./src/OrleansClient/bin/PublishOutput/
      dockerfile: Dockerfile.Debug
    volumes: 
      - ./src/OrleansClient/bin/PublishOutput/:/app
      - ~/.nuget/packages:/root/.nuget/packages:ro
    depends_on: 
      - orleans-silo
  orleans-silo:
    image: orleans-silo:debug
    build:
      context: ./src/OrleansSilo/bin/PublishOutput/
      dockerfile: Dockerfile.Debug
    volumes: 
      - ./src/OrleansSilo/bin/PublishOutput/:/app
      - ~/.nuget/packages:/root/.nuget/packages:ro</span></pre>
</div>
<p><code>docker-compose.yml</code>&nbsp;(production):</p>
<div class="cnblogs_code">
<pre>version: '3.1'<span style="color: #000000;">

services:
  orleans-client:
    image: orleans-client
    depends_on: 
      - orleans-silo
  orleans-silo:
    image: orleans-silo</span></pre>
</div>
<p>请注意，在生产中，我们不映射本地目录，也没有build：操作。 原因是在生产中，图像应该已经被构建并推送到你自己的Docker Registry。</p>
<p>8，把一切放在一起</p>
<p>现在我们有运行你的Orleans应用程序所需的所有移动部件，我们将把它放在一起，以便我们可以在Docker中运行Orleans解决方案（最后！）。</p>
<p>注：应从解决方案目录执行以下命令。</p>
<p>首先，请确保我们从我们的解决方案中恢复所有NuGet软件包。 你只需要做一次。 如果您更改了项目的任何软件包依赖项，只需要再次执行该操作。</p>
<p># dotnet restore</p>
<p>现在，让我们像往常一样使用dotnet CLI构建解决方案，并将其发布到输出目录：</p>
<p># dotnet publish -o ./bin/PublishOutput</p>
<p><span style="font-size: 12px; color: #ff0000;">注意：我们在这里使用发布而不是构建，以避免我们在Orleans中动态加载的程序集的问题。 我们仍然在寻找更好的解决方案。</span></p>
<p>随着应用程序的构建和发布，您需要构建Dockerfile图像。 这个步骤只需要在每个项目中执行一次，并且只有在您更改Dockerfil，docker-compose或出于任何原因清理本地映像注册表时才需要执行此步骤。</p>
<p># docker-compose build</p>
<p>在Dockerfile和docker-compose.yml中使用的所有图像都从注册表中获取并缓存在开发机器上。 你的图像已经建好了，而且你都准备好运行了。</p>
<p>现在让我们运行它！</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;"># docker-compose up -d
Creating network </span>"orleansdocker_default"<span style="color: #000000;"> with the default driver
Creating orleansdocker_orleans-silo_1 ... 
Creating orleansdocker_orleans-silo_1 ... done
Creating orleansdocker_orleans-client_1 ... 
Creating orleansdocker_orleans-client_1 ... done
#</span></pre>
</div>
<p>现在，如果您运行docker-compose ps，则会看到2个容器正在为orleansdocker项目运行：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;"># docker-compose ps
             Name                     Command        State   Ports 
------------------------------------------------------------------
orleansdocker_orleans-client_1   tail -f /dev/</span><span style="color: #008080;">null</span><span style="color: #000000;">   Up            
orleansdocker_orleans-silo_1     tail -f /dev/</span><span style="color: #008080;">null</span>   Up </pre>
</div>
<p><span style="font-size: 12px; color: #ff0000;">Windows用户注意事项：如果您在Windows上，并且您的容器使用Windows映像作为基础，那么命令列将向您显示Powershell相对命令到* NIX系统上的尾部，以便容器保持相同的方式。</span></p>
<p>现在你已经有了你的容器，每次你想要启动你的Orleans应用程序时都不需要停下来。 所有你需要的是集成你的IDE调试应用程序在以前映射在您的docker-compose.yml容器。</p>
<p>9，缩减</p>
<p>一旦你的撰写项目正在运行，你可以使用docker-compose scale命令轻松地扩展或缩减应用程序：</p>
<div class="cnblogs_code">
<pre># docker-compose scale orleans-silo=15<span style="color: #000000;">
Starting orleansdocker_orleans-silo_1 ... done
Creating orleansdocker_orleans-silo_2 ... 
Creating orleansdocker_orleans-silo_3 ... 
Creating orleansdocker_orleans-silo_4 ... 
Creating orleansdocker_orleans-silo_5 ... 
Creating orleansdocker_orleans-silo_6 ... 
Creating orleansdocker_orleans-silo_7 ... 
Creating orleansdocker_orleans-silo_8 ... 
Creating orleansdocker_orleans-silo_9 ... 
Creating orleansdocker_orleans-silo_10 ... 
Creating orleansdocker_orleans-silo_11 ... 
Creating orleansdocker_orleans-silo_12 ... 
Creating orleansdocker_orleans-silo_13 ... 
Creating orleansdocker_orleans-silo_14 ... 
Creating orleansdocker_orleans-silo_15 ... 
Creating orleansdocker_orleans-silo_6
Creating orleansdocker_orleans-silo_5
Creating orleansdocker_orleans-silo_3
Creating orleansdocker_orleans-silo_2
Creating orleansdocker_orleans-silo_4
Creating orleansdocker_orleans-silo_9
Creating orleansdocker_orleans-silo_7
Creating orleansdocker_orleans-silo_8
Creating orleansdocker_orleans-silo_10
Creating orleansdocker_orleans-silo_11
Creating orleansdocker_orleans-silo_15
Creating orleansdocker_orleans-silo_12
Creating orleansdocker_orleans-silo_14
Creating orleansdocker_orleans-silo_13</span></pre>
</div>
<p>几秒钟后，您将看到服务缩放到您请求的特定数量的实例。</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;"># docker-compose ps
             Name                     Command        State   Ports 
------------------------------------------------------------------
orleansdocker_orleans-client_1   tail -f /dev/</span><span style="color: #008080;">null</span><span style="color: #000000;">   Up            
orleansdocker_orleans-silo_1     tail -f /dev/</span><span style="color: #008080;">null</span><span style="color: #000000;">   Up            
orleansdocker_orleans-silo_10    tail -f /dev/</span><span style="color: #008080;">null</span><span style="color: #000000;">   Up            
orleansdocker_orleans-silo_11    tail -f /dev/</span><span style="color: #008080;">null</span><span style="color: #000000;">   Up            
orleansdocker_orleans-silo_12    tail -f /dev/</span><span style="color: #008080;">null</span><span style="color: #000000;">   Up            
orleansdocker_orleans-silo_13    tail -f /dev/</span><span style="color: #008080;">null</span><span style="color: #000000;">   Up            
orleansdocker_orleans-silo_14    tail -f /dev/</span><span style="color: #008080;">null</span><span style="color: #000000;">   Up            
orleansdocker_orleans-silo_15    tail -f /dev/</span><span style="color: #008080;">null</span><span style="color: #000000;">   Up            
orleansdocker_orleans-silo_2     tail -f /dev/</span><span style="color: #008080;">null</span><span style="color: #000000;">   Up            
orleansdocker_orleans-silo_3     tail -f /dev/</span><span style="color: #008080;">null</span><span style="color: #000000;">   Up            
orleansdocker_orleans-silo_4     tail -f /dev/</span><span style="color: #008080;">null</span><span style="color: #000000;">   Up            
orleansdocker_orleans-silo_5     tail -f /dev/</span><span style="color: #008080;">null</span><span style="color: #000000;">   Up            
orleansdocker_orleans-silo_6     tail -f /dev/</span><span style="color: #008080;">null</span><span style="color: #000000;">   Up            
orleansdocker_orleans-silo_7     tail -f /dev/</span><span style="color: #008080;">null</span><span style="color: #000000;">   Up            
orleansdocker_orleans-silo_8     tail -f /dev/</span><span style="color: #008080;">null</span><span style="color: #000000;">   Up            
orleansdocker_orleans-silo_9     tail -f /dev/</span><span style="color: #008080;">null</span>   Up </pre>
</div>
<p><span style="font-size: 12px; color: #ff0000;">注意：这些例子中的命令列仅显示了tail命令，因为我们正在使用调试器容器。 如果我们在生产，它会显示dotnet OrleansSilo.dll为例。</span></p>
<p>10，Docker集 群</p>
<p>Docker集群堆栈被称为Swarm，你可以在这里阅读它的文档来找到更多<a href="https://docs.docker.com/engine/swarm/">documentation here</a>.</p>
<p>要在Swarm集群中运行这篇文章，您没有任何额外的工作。 在Swarm节点中运行docker-compose -d时，它将根据配置的规则调度容器。 其他基于Swarm的服务（例如Docker Datacenter，Azure ACS（Swarm模式），AWS ECS Container Service等）也是如此。 您只需在部署dockerized Orleans应用程序之前部署您的Swarm集群。</p>
<p><span style="font-size: 12px; color: #ff0000;">注意：如果您使用的Swarm模式已经支持堆栈，部署和组合v3的Docker引擎，则部署解决方案的更好方法是使用docker stack deploy -c docker-compose.yml &lt;name&gt;。 请记住，它需要在您的Docker引擎上支持v3撰写文件，大多数托管服务（如Azure和AWS）仍然使用v2和更旧的引擎。</span></p>
<p>11，Google Kubernetes（K8s）</p>
<p>12，[奖金主题]调试容器内的Orleans</p>
<p>那么，现在你知道如何在一个容器中从头开始运行Orleans，将会很好地利用Docker中最重要的原则之一。 容器是不可变的。 他们在开发中应该具有（几乎）相同的图像，依赖性和运行时。 这确保了良好的陈述&ldquo;在我的机器上工作！&rdquo; 永远不会再发生。 为了做到这一点，你需要有一种方法来在容器内部进行开发，并且包含一个调试器连接到容器内的应用程序。</p>
<p>有多种方法可以使用多个工具来实现这一点。 经过几次评估之后，我写这篇文章的时候，我选择了一个看起来更简单，并且在应用程序中不那么干扰的程序。</p>
<p>正如本文前面提到的，我们使用VSCode来开发示例，所以下面是如何让调试器附加到容器内的Orleans应用程序。</p>
<p>首先，在您的解决方案中更改.vscode目录中的两个文件：</p>
<p><code>tasks.json</code>:</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">{
    </span>"version": "0.1.0"<span style="color: #000000;">,
    </span>"command": "dotnet"<span style="color: #000000;">,
    </span>"isShellCommand": <span style="color: #0000ff;">true</span><span style="color: #000000;">,
    </span>"args"<span style="color: #000000;">: [],
    </span>"tasks"<span style="color: #000000;">: [
        {
            </span>"taskName": "publish"<span style="color: #000000;">,
            </span>"args"<span style="color: #000000;">: [
                </span>"${workspaceRoot}/Orleans-Docker.sln", "-c", "Debug", "-o", "./bin/PublishOutput"<span style="color: #000000;">
            ],
            </span>"isBuildCommand": <span style="color: #0000ff;">true</span><span style="color: #000000;">,
            </span>"problemMatcher": "$msCompile"<span style="color: #000000;">
        }
    ]
}</span></pre>
</div>
<p>这个文件基本上告诉VSCode，无论何时你构建项目，它都会像我们以前手动执行的那样，执行publish命令。</p>
<p><code>launch.json</code>:</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">{
   </span>"version": "0.2.0"<span style="color: #000000;">,
   </span>"configurations"<span style="color: #000000;">: [
        {
            </span>"name": "Silo"<span style="color: #000000;">,
            </span>"type": "coreclr"<span style="color: #000000;">,
            </span>"request": "launch"<span style="color: #000000;">,
            </span>"cwd": "/app"<span style="color: #000000;">,
            </span>"program": "/app/OrleansSilo.dll"<span style="color: #000000;">,
            </span>"sourceFileMap"<span style="color: #000000;">: {
                </span>"/app": "${workspaceRoot}/src/OrleansSilo"<span style="color: #000000;">
            },
            </span>"pipeTransport"<span style="color: #000000;">: {
                </span>"debuggerPath": "/vsdbg/vsdbg"<span style="color: #000000;">,
                </span>"pipeProgram": "/bin/bash"<span style="color: #000000;">,
                </span>"pipeCwd": "${workspaceRoot}"<span style="color: #000000;">,
                </span>"pipeArgs"<span style="color: #000000;">: [
                    </span>"-c"<span style="color: #000000;">,
                    </span>"docker exec -i orleansdocker_orleans-silo_1 /vsdbg/vsdbg --interpreter=vscode"<span style="color: #000000;">
                ]
            }
        },
        {
            </span>"name": "Client"<span style="color: #000000;">,
            </span>"type": "coreclr"<span style="color: #000000;">,
            </span>"request": "launch"<span style="color: #000000;">,
            </span>"cwd": "/app"<span style="color: #000000;">,
            </span>"program": "/app/OrleansClient.dll"<span style="color: #000000;">,
            </span>"sourceFileMap"<span style="color: #000000;">: {
                </span>"/app": "${workspaceRoot}/src/OrleansClient"<span style="color: #000000;">
            },
            </span>"pipeTransport"<span style="color: #000000;">: {
                </span>"debuggerPath": "/vsdbg/vsdbg"<span style="color: #000000;">,
                </span>"pipeProgram": "/bin/bash"<span style="color: #000000;">,
                </span>"pipeCwd": "${workspaceRoot}"<span style="color: #000000;">,
                </span>"pipeArgs"<span style="color: #000000;">: [
                    </span>"-c"<span style="color: #000000;">,
                    </span>"docker exec -i orleansdocker_orleans-client_1 /vsdbg/vsdbg --interpreter=vscode"<span style="color: #000000;">
                ]
            }
        }
    ]
}</span></pre>
</div>
<p>现在，您可以从VSCode（将发布）构建解决方案，并启动silo和客户端。 它会发送一个docker exec命令给正在运行的docker-compose服务实例/容器，以启动调试器到应用程序，就是这样。 你有调试器附加到容器，并使用它，就好像它是一个本地运行的Orleans应用程序。 现在的区别在于它在容器内，一旦你完成了，你可以发布容器到你的注册表，并把它拖到你的Docker主机上。</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt;"><strong><span style="color: #ffffff;">七、<a name="a28"></a>服务结构托管</span></strong></span></p>
<p>Orleans可以在服务结构上托管。 目前有两个与Service Fabric的集成点：</p>
<ul>
<li>Hosting:&nbsp;silos可以托管在服务结构可靠服务内的服务结构中。 由于Orleans公司使用细粒度，动态的分布来管理grain的分配，因此silo应该作为未分区的无国籍服务托管。 其他主机选项（分区，有状态）目前未经测试和不受支持。</li>
<li>Clustering&nbsp;(beta):&nbsp;silos和客户端可以利用Service Fabric的服务发现机制来形成群集。 此选项需要服务结构托管，但服务结构托管不需要服务结构集群。</li>
</ul>
<p>展示托管和集群的样本存在于&nbsp;<a href="https://github.com/dotnet/orleans/tree/master/Samples/ServiceFabric">Samples/ServiceFabric</a>.</p>
<p>1，主机</p>
<p>主机支持可在Microsoft.Orleans.Hosting.ServiceFabric包中找到。 它允许Orleans silo作为服务结构ICommunicationListener运行。 Silo生命周期遵循典型的通信监听器生命周期：它通过ICommunicationListener.OpenAsync方法初始化，并通过ICommunicationListener.CloseAsync方法正常终止，或通过ICommunicationListener.Abort方法突然终止。</p>
<p>OrleansCommunicationListener提供了ICommunicationListener实现。 推荐的方法是使用Orleans.Hosting.ServiceFabric命名空间中的OrleansServiceListener.CreateStateless（Action &lt;StatelessServiceContext，ISiloHostBuilder&gt; configure）创建通信侦听器。 这可确保侦听器具有Clustering所需的端点名称（如下所述）。</p>
<p>每次打开通信侦听器时，调用传递给CreateStateless的配置委托来配置新的silo。</p>
<p>主机可以与服务结构集群提供者结合使用，但是也可以使用其他集群提供者。</p>
<p>2，示例：配置服务结构托管。</p>
<p>以下示例演示托管Orleans孤岛的Service Fabric StatelessService类。 完整的示例可以在Orleans存储库的Samples / ServiceFabric目录中找到。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">internal</span> <span style="color: #0000ff;">sealed</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> StatelessCalculatorService : StatelessService
{
    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> StatelessCalculatorService(StatelessServiceContext context)
        : </span><span style="color: #0000ff;">base</span><span style="color: #000000;">(context)
    {
    }

    </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span> IEnumerable&lt;ServiceInstanceListener&gt;<span style="color: #000000;"> CreateServiceInstanceListeners()
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 监听器可以在服务实例的生命周期中多次打开和关闭。 每当侦听器打开时，新的Orleans silo都将被创建和初始化，并且当侦听器关闭时将被关闭。</span>
        <span style="color: #0000ff;">var</span> listener =<span style="color: #000000;"> OrleansServiceListener.CreateStateless(
            (serviceContext, builder) </span>=&gt;<span style="color: #000000;">
            {
                </span><span style="color: #008000;">//可选：使用服务结构作为集群成员资格。</span>
<span style="color: #000000;">                builder.UseServiceFabricClustering(serviceContext);

                </span><span style="color: #008000;">//备选方法：使用Azure存储作为群集成员资格。</span>
                builder.UseAzureTableMembership(options =&gt;<span style="color: #000000;">
                {
                    </span><span style="color: #008000;">/*</span><span style="color: #008000;"> 配置连接字符串</span><span style="color: #008000;">*/</span><span style="color: #000000;">
                });

                </span><span style="color: #008000;">//</span><span style="color: #008000;"> 可选：配置日志记录。</span>
                builder.ConfigureLogging(logging =&gt;<span style="color: #000000;"> logging.AddDebug());

                </span><span style="color: #0000ff;">var</span> config = <span style="color: #0000ff;">new</span><span style="color: #000000;"> ClusterConfiguration();
                config.Globals.RegisterBootstrapProvider</span>&lt;BootstrapProvider&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">poke_grains</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                config.Globals.ReminderServiceType </span>=<span style="color: #000000;">
                    GlobalConfiguration.ReminderServiceProviderType.ReminderTableGrain;

                </span><span style="color: #008000;">//</span><span style="color: #008000;"> Service Fabric管理端口分配，因此使用这些端口更新配置。</span>
<span style="color: #000000;">                config.Defaults.ConfigureServiceFabricSiloEndpoints(serviceContext);

                </span><span style="color: #008000;">//</span><span style="color: #008000;"> 告诉Orleans 使用这个配置。</span>
<span style="color: #000000;">                builder.UseConfiguration(config);

                </span><span style="color: #008000;">//</span><span style="color: #008000;"> 添加你的应用程序集。</span>
                builder.ConfigureApplicationParts(parts =&gt;<span style="color: #000000;">
                {
                    parts.AddApplicationPart(</span><span style="color: #0000ff;">typeof</span><span style="color: #000000;">(CalculatorGrain).Assembly).WithReferences();

                    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 可选：在当前基本路径中添加所有可装载的程序集（请参阅AppDomain.BaseDirectory）。</span>
<span style="color: #000000;">                    parts.AddFromApplicationBaseDirectory();
                });
            });

        </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;">[] { listener };
    }

    </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">async</span><span style="color: #000000;"> Task RunAsync(CancellationToken cancellationToken)
    {
        </span><span style="color: #0000ff;">while</span> (<span style="color: #0000ff;">true</span><span style="color: #000000;">)
        {
            cancellationToken.ThrowIfCancellationRequested();
            </span><span style="color: #0000ff;">await</span> Task.Delay(TimeSpan.FromSeconds(<span style="color: #800080;">10</span><span style="color: #000000;">), cancellationToken);
        }
    }
}</span></pre>
</div>
<p>3，集群（测试版）</p>
<p>注意：目前推荐在生产中使用存储支持的集群提供程序，例如SQL，ZooKeeper，Consul或Azure表。</p>
<p>在Microsoft.Orleans.Clustering.ServiceFabric包中支持使用Service Fabric的服务发现（命名服务）机制来获得群集成员资格。 该实现要求还使用Service Fabric Hosting支持，并且从StatelessService.CreateServiceInstanceListeners（）返回的值中将Silo端点命名为&ldquo;Orleans&rdquo;。 确保这种最简单的方法是使用OrleansServiceListener.CreateStateless（...）方法，如前一节所述。</p>
<p>通过silo上的ISiloHostBuilder.UseServiceFabricClustering（ServiceContext）扩展方法和客户端上的IClientBuilder.UseServiceFabricClustering（Uri）扩展方法来启用Service Fabric Clustering。</p>
<p>目前的建议是使用存储支持的集群提供程序来执行生产服务，如SQL，ZooKeeper，Consul或Azure Storage。 这些提供程序（特别是SQL和Azure存储）已经在生产使用中进行了充分的测试。</p>