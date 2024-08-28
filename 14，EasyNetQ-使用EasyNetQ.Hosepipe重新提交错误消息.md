<p>EasyNetQ队列管理实用程序。 用它从队列中抓取消息并重新发布。 还可以用它来检查错误队列消息并重试它们。</p>
<p>1，用法：</p>
<div class="cnblogs_code">
<pre>EasyNetQ.Hosepipe.exe &lt;command&gt; [&lt;option:value&gt; ..]</pre>
</div>
<p>2，命令：</p>
<pre><code>dump	将队列中的所有消息转储到给定的目录
		注意：这会为每条消息创建三个文件：

		消息体：
		&lt;queue_name&gt;.n.message.txt

		消息的基本属性：
		&lt;queue_name&gt;.n.properties.txt

		发布消息所需的信息，包括交换名称和路由密钥：
		&lt;queue_name&gt;.n.info.txt

insert	重新发布给定目录中的所有消息

err		将所有EasyNetQ错误消息转储到给定的目录

retry	重试给定目录中的任何EasyNetQ错误消息</code></pre>
<p>注意这会忽略* .properties.txt和* .info.txt文件<br />因为属性和信息包含在错误信息中<br />本身</p>
<pre><code>
?		输出这个使用信息</code></pre>
<p>&nbsp;</p>
<p>3，选项：</p>
<pre><code>s	RabbitMQ代理（服务器）连接到。 默认是'localhost'
v	虚拟主机。 默认是'/'
u	用于连接的用户名。 默认是'guest'
p	连接的密码。 默认是'guest'
q	从中获取消息的队列名称，或将它们发布到。
o	要输出消息的目录。 默认是当前目录。
n	要检索的最大邮件数量。 默认值是1000。</code></pre>
<p>4，案例：</p>
<ol>
<li>
<p>要将名为'my_queue'的队列中的所有消息作为文本文件输出到目录'C:\temp\messages'：</p>
<p><code>EasyNetQ.Hosepipe.exe dump s:localhost u:guest p:guest q:my_queue o:C:\temp\messages</code></p>
</li>
<li>
<p>插入（重新发布）目录'C:\temp\messages'中的所有消息：</p>
<p><code>EasyNetQ.Hosepipe.exe insert s:localhost u:guest p:guest o:C:\temp\messages</code></p>
</li>
<li>
<p>将所有在代理本地主机中排队的EasyNetQ消息转储到目录'C：\ temp \ messages'</p>
<p><code>EasyNetQ.Hosepipe.exe err s:localhost o:C:\temp\messages</code></p>
</li>
<li>
<p>重新发布目录'C:\temp\messages'中的所有错误消息：</p>
<p><code>EasyNetQ.Hosepipe.exe retry s:localhost u:guest p:guest o:C:\temp\messages</code></p>
</li>
</ol>
<p>注意</p>
<p>&ldquo;dump&rdquo;和&ldquo;err&rdquo;命令都不会从队列中移除消息，它们只是迭代队列并将消息复制到给定目录，而将原始消息留在队列中。 在重试首先清除错误队列的错误消息（使用RabbitMQ管理界面）时要小心，因为如果消息再次失败，它们也会导致新的错误消息被发布到错误队列中，并且可能重复的消息可能会 被创建。</p>
<p>&nbsp;</p>