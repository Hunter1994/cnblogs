<p>RabbitMQ具有非常酷的功能，基于主题的路由，允许订阅者基于多个标准过滤消息。 主题是与邮件一起发布的点分隔的单词列表。 例子是&ldquo;stock.usd.nyse&rdquo;或&ldquo;book.uk.london&rdquo;或&ldquo;a.b.c&rdquo;，这些单词可以是你喜欢的任何东西，但通常是消息的一些属性。 主题字符串的限制为255个字符。</p>
<p>&nbsp;</p>
<p>要使用主题发布，只需使用带有主题的重载的Publish方法：</p>
<div class="cnblogs_code">
<pre>bus.Publish(message, <span style="color: #800000;">"</span><span style="color: #800000;">X.A</span><span style="color: #800000;">"</span>);</pre>
</div>
<p>订阅者可以通过指定要匹配的主题来过滤邮件。 这些可以包括通配符：</p>
<p>*：匹配一个字。</p>
<p>＃：匹配到零个或多个单词。</p>
<p>所以发布的主题为&ldquo;X.A.2&rdquo;的消息将匹配&ldquo;＃&rdquo;，&ldquo;X.＃&rdquo;，&ldquo;* .A.*&rdquo;，而不是&ldquo;X.B. *&rdquo;或&ldquo;A&rdquo;。 要订阅一个主题，请使用重载的订阅方法与配置：</p>
<div class="cnblogs_code">
<pre>bus.Subscribe(<span style="color: #800000;">"</span><span style="color: #800000;">my_id</span><span style="color: #800000;">"</span>, handler, x =&gt; x.WithTopic(<span style="color: #800000;">"</span><span style="color: #800000;">X.*</span><span style="color: #800000;">"</span>));</pre>
</div>
<p>警告： 具有相同订阅者但不同主题字符串的两个单独订阅可能不会产生您期望的效果。 subscriberId有效地标识个体AMQP队列。 具有相同subscriptionId的两个订阅者将连接到相同的队列，并且两者都将添加自己的主题绑定。 所以，例如，如果你这样做：</p>
<div class="cnblogs_code">
<pre>bus.Subscribe(<span style="color: #800000;">"</span><span style="color: #800000;">my_id</span><span style="color: #800000;">"</span>, handlerOfXDotStar, x =&gt; x.WithTopic(<span style="color: #800000;">"</span><span style="color: #800000;">X.*</span><span style="color: #800000;">"</span><span style="color: #000000;">));
bus.Subscribe(</span><span style="color: #800000;">"</span><span style="color: #800000;">my_id</span><span style="color: #800000;">"</span>, handlerOfStarDotB, x =&gt; x.WithTopic(<span style="color: #800000;">"</span><span style="color: #800000;">*.B</span><span style="color: #800000;">"</span>));</pre>
</div>
<p>匹配&ldquo;x.*&rdquo;或&ldquo;* .B&rdquo;的所有消息将被传递到&ldquo;XXX_my_id&rdquo;队列。 然后，RabbitMQ将向两个消费者传递消息，其中handlerOfXDotStar和handlerOfStarDotB轮流获取每条消息。</p>
<p>&nbsp;现在，如果你想要匹配多个主题（&ldquo;X. *&rdquo;OR&ldquo;* .B&rdquo;），你可以使用另一个重载的订阅方法，它采用多个主题，如下所示：</p>
<div class="cnblogs_code">
<pre>bus.Subscribe(<span style="color: #800000;">"</span><span style="color: #800000;">my_id</span><span style="color: #800000;">"</span>, handler, x =&gt; x.WithTopic(<span style="color: #800000;">"</span><span style="color: #800000;">X.*</span><span style="color: #800000;">"</span>).WithTopic(<span style="color: #800000;">"</span><span style="color: #800000;">*.B</span><span style="color: #800000;">"</span>));</pre>
</div>
<p>有一些主题重载的SubscribeAsync方法的工作方式完全相同。</p>