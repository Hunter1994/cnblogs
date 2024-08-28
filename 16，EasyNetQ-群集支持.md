<p>EasyNetQ支持RabbitMQ群集，无需部署负载均衡器。</p>
<p>只需在连接字符串中列出群集的节点...</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> bus = RabbitHutch.CreateBus(<span style="color: #800000;">"</span><span style="color: #800000;">host=ubuntu:5672,ubuntu:5673</span><span style="color: #800000;">"</span>);</pre>
</div>
<p>在这个例子中，我们在一台机器上建立了一个集群'ubuntu'，端口5672上的节点1和端口5673上的节点2上。当CreateBus语句执行时，EasyNetQ将尝试连接到列出的第一台主机（ubuntu：5672）。 如果连接失败，它会尝试连接到列出的第二台主机（ubuntu：5673）。 如果两个节点都不可用，则它将位于重试循环中，每五秒钟尝试连接两台服务器。 它将所有这些活动记录到注册的IEasyNetQLogger。 如果第一个节点不可用，您可能会看到类似这样的内容：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">DEBUG: Trying to connect
ERROR: Failed to connect to Broker: </span><span style="color: #800000;">'</span><span style="color: #800000;">ubuntu</span><span style="color: #800000;">'</span>, Port: <span style="color: #800080;">5672</span> VHost: <span style="color: #800000;">'</span><span style="color: #800000;">/</span><span style="color: #800000;">'</span>. ExceptionMessage: <span style="color: #800000;">'</span><span style="color: #800000;">None of the specified endpoints were reachable</span><span style="color: #800000;">'</span><span style="color: #000000;">
DEBUG: OnConnected </span><span style="color: #0000ff;">event</span><span style="color: #000000;"> fired
INFO: Connected to RabbitMQ. Broker: </span><span style="color: #800000;">'</span><span style="color: #800000;">ubuntu</span><span style="color: #800000;">'</span>, Port: <span style="color: #800080;">5674</span>, VHost: <span style="color: #800000;">'</span><span style="color: #800000;">/</span><span style="color: #800000;">'</span></pre>
</div>
<p>如果EasyNetQ连接的节点发生故障，EasyNetQ将尝试连接到下一个列出的节点。 一旦连接，它将重新申报所有交易所和队列，并重新启动所有消费者。 以下是一个示例日志记录，显示一个节点出现故障，然后EasyNetQ连接到另一个节点并重新创建订户：</p>
<div class="cnblogs_code">
<pre>INFO: Disconnected <span style="color: #0000ff;">from</span><span style="color: #000000;"> RabbitMQ Broker
DEBUG: Trying to connect
DEBUG: OnConnected </span><span style="color: #0000ff;">event</span><span style="color: #000000;"> fired
DEBUG: Re</span>-<span style="color: #000000;">creating subscribers
INFO: Connected to RabbitMQ. Broker: </span><span style="color: #800000;">'</span><span style="color: #800000;">ubuntu</span><span style="color: #800000;">'</span>, Port: <span style="color: #800080;">5674</span>, VHost: <span style="color: #800000;">'</span><span style="color: #800000;">/</span><span style="color: #800000;">'</span></pre>
</div>
<p>1，随机主机选择</p>
<p>如果您有多个使用EasyNetQ连接到RabbitMQ群集的服务，它们将首先连接到其各自连接字符串中的第一个列出的节点。 如果您打算使用负载平衡功能，则应考虑切换到RandomClusterHostSelectionStrategy。 像这样配置它：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> bus = RabbitHutch.CreateBus(<span style="color: #800000;">"</span><span style="color: #800000;">host=myfirsthost,mysecondhost</span><span style="color: #800000;">"</span>, x =&gt; x.Register&lt;IClusterHostSelectionStrategy&lt;ConnectionFactoryInfo&gt;, RandomClusterHostSelectionStrategy&lt;ConnectionFactoryInfo&gt;&gt;());</pre>
</div>
<p>在这个片段中，我们已经替换了RandomClusterHostSelectionStrategy的默认IClusterHostSelectionStrategy，它将随机选择主机。 您可以在这里找到更多有关替换EasyNetQ组件的信息。</p>
<p>2，考虑使用专用的负载平衡器</p>
<p>EasyNetQ集群支持的替代方案是使用专用的前端代理。 有关详细信息，请参阅RabbitMQ集群指南的结尾：http：//www.rabbitmq.com/clustering.html</p>
<p>&nbsp;</p>