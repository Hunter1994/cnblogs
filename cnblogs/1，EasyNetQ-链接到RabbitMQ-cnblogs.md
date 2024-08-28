<p style="background-color: #169fe6;"><strong><span style="color: #ffffff; font-size: 18pt;">一、链接到RabbitMQ</span></strong></p>
<p><strong><span style="font-size: 18px;">1，创建连接</span></strong></p>
<p><span style="font-size: 12px; color: #ff0000;">注意不能有空格</span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> bus = RabbitHutch.CreateBus(&ldquo;host=myServer;virtualHost=myVirtualHost;username=mike;password=topsecret&rdquo;);</pre>
</div>
<p><strong>1）host（必填）：</strong></p>
<p>例如：host=localhost或者host=192.168.2.56或者host=myhost.mydomain.com</p>
<p>使用标准格式主机:端口(host=myhost.com:5673)</p>
<p>如果省略端口号，默认端口使用AMQP(5672)</p>
<p>连接到RabbitMQ集群，每个集群节点指定以逗号分隔(host=myhost1.com,myhost2.com,myhost3.com)</p>
<p><strong>2）virtualHost（默认&lsquo;/&rsquo;）：</strong></p>
<p>例如：virtualHost=myVirtualHost</p>
<p><strong>3）username（默认guest）：</strong></p>
<p>例如：username=mike</p>
<p><strong>4）&nbsp;password（默认guest）：</strong></p>
<p>例如：password=mysecret</p>
<p><strong>5）requestedheartbeat（默认值是10秒）：</strong></p>
<p>例如：requestedHeartbeat=10。设置为0，没有心跳。</p>
<p><strong>6）&nbsp;prefetchcount（默认值是50）：</strong></p>
<p>例如：prefetchcount=1。这是由EasyNetQ发送ack之前由RabbitMQ发送的消息数。 设置为0用于无限预取（不推荐）。 设置为1，在消费者农场之间进行公平的工作平衡。</p>
<p><strong>&nbsp;7）publisherConfirms（默认为false）：</strong></p>
<p>例如：publisherConfirms=true，这打开了<a href="https://github.com/EasyNetQ/EasyNetQ/wiki/Publisher-Confirms">Publisher Confirms</a>.。</p>
<p><strong>8） persistentMessages（默认为true）：&nbsp;</strong></p>
<p>例如：persistentMessages=false。这决定了在发布消息时如何设置basic.properties中的delivery_mode。 false = 1，true = 2。 当设置为true时，消息将由RabbitMQ持久存储到磁盘，并在服务器重新启动后生存。 当设置为false时，可以预期性能提升。</p>
<p><strong>9） product（默认值是实例化总线的可执行文件的名称）：</strong></p>
<p>例如：product=My really important service。在EasyNetQ 0.27.3中引入。 此处输入的值将显示在RabbitMQ的管理界面中。</p>
<p><strong>10） platform（&nbsp;默认值是运行客户端进程实例化总线的机器的主机名）：</strong></p>
<p>例如platform = my.fully.qualified.domain.name。在EasyNetQ 0.27.3中引入。 此处输入的值将显示在RabbitMQ的管理界面中。</p>
<p><strong>11）timeout（默认为10秒）：</strong></p>
<p>例如timeout = 60。 在EasyNetQ 0.17中推出。 解析为System.UInt16。 范围从0到65535.格式为秒。 对于无限超时，请使用0。超出值时抛出System.TimeoutException。</p>
<p><strong><span style="font-size: 18px;">2，关闭连接</span></strong></p>
<div class="cnblogs_code">
<pre>bus.Dispose();</pre>
</div>
<p>这将关闭EasyNetQ使用的连接，渠道，消费者和所有其他资源。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">二、连接SSL</span></strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> connection = <span style="color: #0000ff;">new</span><span style="color: #000000;"> ConnectionConfiguration();

connection.Port </span>= <span style="color: #800080;">443</span><span style="color: #000000;">;
connection.UserName </span>= <span style="color: #800000;">"</span><span style="color: #800000;">user</span><span style="color: #800000;">"</span><span style="color: #000000;">;
connection.Password </span>= <span style="color: #800000;">"</span><span style="color: #800000;">pass</span><span style="color: #800000;">"</span><span style="color: #000000;">;
connection.Product </span>= <span style="color: #800000;">"</span><span style="color: #800000;">SSLTest</span><span style="color: #800000;">"</span><span style="color: #000000;">;

</span><span style="color: #0000ff;">var</span> host1 = <span style="color: #0000ff;">new</span><span style="color: #000000;"> HostConfiguration();
host1.Host </span>= <span style="color: #800000;">"</span><span style="color: #800000;">rmq1.contoso.com</span><span style="color: #800000;">"</span><span style="color: #000000;">;
host1.Port </span>= <span style="color: #800080;">443</span><span style="color: #000000;">;
host1.Ssl.Enabled </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">;
host1.Ssl.ServerName </span>= <span style="color: #800000;">"</span><span style="color: #800000;">rmq1.contoso.com</span><span style="color: #800000;">"</span><span style="color: #000000;">;
host1.Ssl.CertPath </span>= <span style="color: #800000;">"</span><span style="color: #800000;">c:\\tmp\\myclient.p12</span><span style="color: #800000;">"</span><span style="color: #000000;">;
host1.Ssl.CertPassphrase </span>= <span style="color: #800000;">"</span><span style="color: #800000;">secret</span><span style="color: #800000;">"</span><span style="color: #000000;">;

</span><span style="color: #0000ff;">var</span> host2 = <span style="color: #0000ff;">new</span><span style="color: #000000;"> HostConfiguration();
host2.Host </span>= <span style="color: #800000;">"</span><span style="color: #800000;">rmq2.contoso.com</span><span style="color: #800000;">"</span><span style="color: #000000;">;
host2.Port </span>= <span style="color: #800080;">443</span><span style="color: #000000;">;
host2.Ssl.Enabled </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">;
host2.Ssl.ServerName </span>= <span style="color: #800000;">"</span><span style="color: #800000;">rmq2.contoso.com</span><span style="color: #800000;">"</span><span style="color: #000000;">;
host2.Ssl.CertPath </span>= <span style="color: #800000;">"</span><span style="color: #800000;">c:\\tmp\\myclient.p12</span><span style="color: #800000;">"</span><span style="color: #000000;">;
host2.Ssl.CertPassphrase </span>= <span style="color: #800000;">"</span><span style="color: #800000;">secret</span><span style="color: #800000;">"</span><span style="color: #000000;">;

connection.Hosts </span>= <span style="color: #0000ff;">new</span> List&lt;HostConfiguration&gt;<span style="color: #000000;"> { host1, host2 };

connection.Validate();        </span><span style="color: #008000;">//非常重要</span>

<span style="color: #0000ff;">var</span> Bus = RabbitHutch.CreateBus(connection, services =&gt; services.Register&lt;IEasyNetQLogger&gt;(logger =&gt; <span style="color: #0000ff;">new</span> DoNothingLogger()));</pre>
</div>
<p>&nbsp;</p>