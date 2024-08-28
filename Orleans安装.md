<p>一、Nuget包<br />Orleans NuGet软件包从v1.5.0开始<br />在大多数情况下，您需要使用4个关键的NuGet包：</p>
<p>1，Microsoft Orleans Build-time Code Generation</p>
<div class="cnblogs_code">
<pre>PM&gt; Install-Package Microsoft.Orleans.OrleansCodeGenerator.Build</pre>
</div>
<p>为Grain接口和实现项目提供支持。将其添加到grainaaa接口和实现项目中，以启用Grain引用和序列化程序代码生成。Microsoft.Orleans.Templates.Interfaces和Microsoft.Orleans.Templates.Grain 包是过时的，只提供向后兼容性和迁移。</p>
<p>2，Microsoft Orleans Core Library</p>
<div class="cnblogs_code">
<pre>PM&gt; Install-Package Microsoft.Orleans.Core</pre>
</div>
<p>包含Orleans.dll，它定义了Orleans公共类型和Orleans客户端的大部分。 引用它来构建使用Orleans类型的库和客户端应用程序，但不需要任何包含的提供程序。</p>
<p>3，Microsoft Orleans Server Libraries</p>
<div class="cnblogs_code">
<pre>PM&gt; Install-Package Microsoft.Orleans.Server</pre>
</div>
<p>包括运行silo所需的一切。</p>
<p>4，Microsoft Orleans Client Libraries</p>
<div class="cnblogs_code">
<pre>PM&gt; Install-Package Microsoft.Orleans.Client</pre>
</div>
<p>包括你需要的一切Orleans客户端（前端）。</p>
<p>&nbsp;</p>
<p>二、其他软件包<br />下面的包提供了额外的功能。</p>
<p>1，Microsoft Orleans Providers</p>
<div class="cnblogs_code">
<pre>PM&gt; Install-Package Microsoft.Orleans.OrleansProviders</pre>
</div>
<p>包含一组内置的持久性和流提供程序，主要用于测试，以及用于构建持久性和流提供程序的一些抽象和实用程序类型。 包含在Microsoft.Orleans.Client和Microsoft.Orleans.Server中。</p>
<p>2，Microsoft Orleans Event-Sourcing</p>
<div class="cnblogs_code">
<pre>PM&gt; Install-Package Microsoft.Orleans.EventSourcing</pre>
</div>
<p>包含用于创建具有事件源状态的grain类的一组基类型。</p>
<p>&nbsp;</p>
<p>三、提供商和扩展</p>
<p>1，Microsoft Orleans Azure Utilities</p>
<div class="cnblogs_code">
<pre>PM&gt; Install-Package Microsoft.Orleans.OrleansAzureUtils</pre>
</div>
<p>包含基于Azure表的集群成员资格提供程序，简化Azure工作站/ Web角色中silos&nbsp;和客户端的实例化的包装类，Azure表和Azure Blobs的持久性提供程序以及Azure队列的流提供程序。</p>
<p><br />2，Microsoft Orleans Sql Utilities</p>
<div class="cnblogs_code">
<pre>PM&gt; Install-Package Microsoft.Orleans.OrleansSqlUtils</pre>
</div>
<p>包含用于SQL Server，MySQL，PostgreSQL和其他SQL数据库的基于SQL的群集成员资格和持久性提供程序。</p>
<p><br />3，Microsoft Orleans ServiceBus Utilities</p>
<div class="cnblogs_code">
<pre>PM&gt; Install-Package Microsoft.Orleans.OrleansServiceBus</pre>
</div>
<p>包含Azure事件中心的流提供程序。</p>
<p><br />4，Microsoft Orleans Consul Utilities</p>
<div class="cnblogs_code">
<pre>PM&gt; Install-Package Microsoft.Orleans.OrleansConsulUtils</pre>
</div>
<p>包括使用Consul存储集群成员数据的插件</p>
<p><br />5，Microsoft Orleans ZooKeeper Utilities</p>
<div class="cnblogs_code">
<pre>PM&gt; Install-Package Microsoft.Orleans.OrleansZooKeeperUtils</pre>
</div>
<p>包含使用ZooKeeper存储集群成员数据的插件。</p>
<p><br />6，Microsoft Orleans AWS Utilities</p>
<div class="cnblogs_code">
<pre>PM&gt; Install-Package Microsoft.Orleans.OrleansAWSUtils</pre>
</div>
<p>包括基于DynamoDB的集群成员资格提供程序，DynamoDB持久性提供程序和基于SQS的流提供程序。</p>
<p><br />7，Microsoft Orleans Telemetry Consumer - Performance Counters</p>
<div class="cnblogs_code">
<pre>PM&gt; Install-Package Microsoft.Orleans.OrleansTelemetryConsumers.Counters</pre>
</div>
<p>Windows性能计数器实现Orleans Telemetry&nbsp;API。</p>
<p><br />9，Microsoft Orleans Telemetry Consumer - Azure Application Insights</p>
<div class="cnblogs_code">
<pre>PM&gt; Install-Package Microsoft.Orleans.OrleansTelemetryConsumers.AI</pre>
</div>
<p>包括Azure Application Insights的Telemetry&nbsp;消费者。</p>
<p><br />10，Microsoft Orleans Telemetry Consumer - NewRelic</p>
<div class="cnblogs_code">
<pre>PM&gt; Install-Package Microsoft.Orleans.OrleansTelemetryConsumers.NewRelic</pre>
</div>
<p>包括NewRelic的Telemetry&nbsp;消费者。</p>
<p><br />11，Microsoft Orleans Bond Serializer</p>
<div class="cnblogs_code">
<pre>PM&gt; Install-Package Microsoft.Orleans.Serialization.Bond</pre>
</div>
<p>包括对Bond序列化器的支持</p>
<p><br />12，Microsoft Orleans Google Utilities</p>
<div class="cnblogs_code">
<pre>PM&gt; Install-Package Microsoft.Orleans.OrleansGoogleUtils</pre>
</div>
<p>Includes Google Protocol Buffers serializer</p>
<p>&nbsp;</p>
<p>四、托管和测试</p>
<p>1，Microsoft Orleans Runtime</p>
<div class="cnblogs_code">
<pre>PM&gt; Install-Package Microsoft.Orleans.OrleansRuntime</pre>
</div>
<p>Microsoft Orleans的核心运行时库，在一个silo内托管和执行grains&nbsp;。</p>
<p><br />2，Microsoft Orleans Silo Host</p>
<div class="cnblogs_code">
<pre>PM&gt; Install-Package Microsoft.Orleans.OrleansHost</pre>
</div>
<p>包括默认的silo主机 - OrleansHost.exe。 可用于本地部署或作为Azure工作者角色中的进程外silo主机。 包含在Microsoft.Orleans.Server中。 我们计划弃用这个软件包，转而建立自己的定制silo主机进程，以简化依赖管理和程序化配置。</p>
<p><br />3，Microsoft Orleans Service Fabric Support</p>
<div class="cnblogs_code">
<pre>PM&gt; Install-Package Microsoft.Orleans.ServiceFabric</pre>
</div>
<p>支持在服务结构上托管Microsoft Orleans。</p>
<p><br />4，Microsoft Orleans Testing Host Library</p>
<div class="cnblogs_code">
<pre>PM&gt; Install-Package Microsoft.Orleans.TestingHost</pre>
</div>
<p>包括在测试项目中托管silos的库。</p>
<p><br />5，Microsoft Orleans Code Generation</p>
<div class="cnblogs_Highlighter">
<pre class="brush:csharp;gutter:true;">PM&gt; Install-Package Microsoft.Orleans.OrleansCodeGenerator
</pre>
</div>
<p>包括运行时代码生成器。 包含在Microsoft.Orleans.Server和Microsoft.Orleans.Client中　</p>
<p>&nbsp;</p>
<p>五、工具</p>
<p>1，Microsoft Orleans Performance Counter Tool</p>
<div class="cnblogs_code">
<pre>PM&gt; Install-Package Microsoft.Orleans.CounterControl</pre>
</div>
<p>包括OrleansCounterControl.exe，它为Orleans统计信息和已部署的grain类注册Windows性能计数器类别。 需要提升。 可以在Azure中作为角色启动任务的一部分执行。 包含在Microsoft.Orleans.Server中。</p>
<p><br />2，Microsoft Orleans Management Tool</p>
<div class="cnblogs_code">
<pre>PM&gt; Install-Package Microsoft.Orleans.OrleansManager</pre>
</div>
<p>包括Orleans管理工具 - OrleansManager.exe。 为了简化依赖管理和程序化配置，我们计划弃用这个软件包，转而建立自定义管理工具的客户。</p>
<p>&nbsp;</p>