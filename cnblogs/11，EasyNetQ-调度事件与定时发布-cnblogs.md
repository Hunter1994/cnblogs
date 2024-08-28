<p>许多业务流程都要求将事件安排在未来的某个日期。 例如，在与客户进行初次销售联系之后，我们可能希望在将来某个时间安排后续电话。 EasyNetQ可以通过其未来发布功能帮助您实现此功能。 例如，我们在这里使用FuturePublish扩展方法来安排未来一个月的后续销售电话。 请注意，FuturePublish使用UTC时间。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> followUpCallMessage = <span style="color: #0000ff;">new</span><span style="color: #000000;"> FollowUpCallMessage( .. );

bus.FuturePublish(DateTime.UtcNow.AddMonths(</span><span style="color: #800080;">3</span>), followUpCallMessage);</pre>
</div>
<p>从现在开始三个月后，EasyNetQ将发布该消息，并且FollowUpCallMessage的任何订户都将收到原始消息的副本。</p>
<p>FuturePublish要求EasyNetQ.Scheduler服务正在运行。</p>
<p>1，它是如何工作的？</p>
<p>当您调用bus.FuturePublish（publishDate，message）时，EasyNetQ将您的消息包装在系统消息&ldquo;ScheduleMe&rdquo;中并将其发布到RabbitMQ。 调度程序服务订阅此消息。 当它收到一个ScheduleMe消息时，它将其存储在其本地数据库中。 调度程序服务在其数据库中查找调度日期到期的消息，当它发现任何到期的消息时，它将原始消息从ScheduleMe消息解开并发布到总线。</p>
<p>2，安装调度程序服务</p>
<ol>
<li>
<p>在SQL Server中，创建一个新的数据库EasyNetQ.Scheduler</p>
</li>
<li>
<p>获取EasyNetQ的源代码</p>
<p>git clone&nbsp;<a href="mailto:git@github.com">git@github.com</a>:mikehadlow/EasyNetQ.git</p>
</li>
<li>
<p>在Visual Studio中打开EasyNetQ.2012解决方案。 在文件夹DatabaseScripts - &gt; EasyNetQ.Scheduler中，您可以找到许多SQL脚本。 在EasyNetQ.Scheduler数据库中打开并运行它们。 您需要首先运行CreateWorkTables.sql，其他则是存储过程脚本，并且可以按任意顺序运行。</p>
</li>
<li>
<p>构建解决方案。</p>
</li>
<li>
<p>找到\ Source \ EasyNetQ.Scheduler \ bin \ Debug并将内容复制到您选择的部署文件夹。</p>
</li>
<li>
<p>在文本编辑器中打开EasyNetQ.Scheduler.exe.config，并将&ldquo;rabbit&rdquo;和&ldquo;scheduleDb&rdquo;连接字符串分别指向您的RabbitMQ代理和SQL Server实例。</p>
</li>
<li>
<p>打开控制台窗口并将路径更改为部署EasyNetQ.Scheduler的文件夹。</p>
</li>
<li>
<p>运行以下命令将EasyNetQ.Scheduler安装为Windows服务：</p>
<p>EasyNetQ.Scheduler.exe install</p>
<p>Configuration Result: [Success] Name EasyNetQ.Scheduler [Success] ServiceName EasyNetQ.Scheduler Topshelf v3.1.106.0, .NET Framework v4.0.30319.18051</p>
<p>Running a transacted installation.</p>
<p>Beginning the Install phase of the installation. Installing EasyNetQ.Scheduler service Installing service EasyNetQ.Scheduler... Service EasyNetQ.Scheduler has been successfully installed. Creating EventLog source EasyNetQ.Scheduler in log Application...</p>
<p>The Install phase completed successfully, and the Commit phase is beginning.</p>
<p>The Commit phase completed successfully.</p>
<p>The transacted install has completed.</p>
</li>
</ol>
<p>3，支持延迟消息插件</p>
<p>RabbitMQ延迟消息插件将新的交换类型添加到RabbitMQ，从而允许延迟消息传递。</p>
<p>EasyNetQ通过定义新的调度程序类型来提供对使用该交换的支持：DelayedExchangeScheduler。</p>
<p>这允许您像以前一样使用相同的Future Publish接口，但取消未来的消息除外。 由于延迟消息插件不支持消息取消，因此无论何时调用FuturePublish指定cancelKey，或者调用CancelFuturePublish时，调度程序都会抛出NotImplementedException异常。</p>
<p>以下示例显示了如何发布将在三个月后交付的消息：</p>
<div class="cnblogs_code">
<pre>bus = RabbitHutch.CreateBus(<span style="color: #800000;">"</span><span style="color: #800000;">host=localhost</span><span style="color: #800000;">"</span>, x =&gt; x.Register&lt;IScheduler, DelayedExchangeScheduler&gt;<span style="color: #000000;">());

</span><span style="color: #0000ff;">var</span> followUpCallMessage = <span style="color: #0000ff;">new</span><span style="color: #000000;"> FollowUpCallMessage( .. );

bus.FuturePublish(DateTime.UtcNow.AddMonths(</span><span style="color: #800080;">3</span>), followUpCallMessage);</pre>
</div>
<p>第一行指示EasyNetQ使用支持延迟消息交换的新调度程序。 接下来，该消息将创建并发布，交付时间设置为三个月。 请注意，FuturePublish使用UTC时间。</p>
<p>DelayedExchangeScheduler需要安装Delayed Message Plugin。</p>
<p>①插件安装</p>
<p>延迟消息插件可以在社区插件页面上找到。 为您的RabbitMQ安装下载相应的.ez文件，将其复制到RabbitMQ的插件文件夹中，然后通过运行以下命令启用它：</p>
<div class="cnblogs_code">
<pre>rabbitmq-plugins enable rabbitmq_delayed_message_exchange</pre>
</div>
<p>该插件需要RabbitMQ 3.4或更新版本。</p>
<p>②怎么运行的</p>
<p>当您调用bus.FuturePublish（...）时，EasyNetQ会自动创建新的x延迟消息交换以及正常交换并将它们绑定在一起。 该消息在延迟交换中发布，该交换将存储该消息，直到交付它为止。 此时，该消息被路由到正常交换并从那里到绑定队列。</p>
<p>当您调用Publish（...）方法时，消息将发布到正常交换，从而防止与使用新的x延迟消息交换相关的任何性能下降。</p>
<p>延迟交换持续使用Mnesia的消息。 这可以防止在服务器停机时丢失信息。 一旦服务器恢复，所有符合条件的消息都将按计划交付。</p>
<p>&nbsp;</p>