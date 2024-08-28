<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">一、rabbitmqctl</span></strong></p>
<p>启动rabbitmq&nbsp;<span class="cnblogs_code">rabbitmqctl start_app</span>&nbsp;</p>
<p>关闭rabbitmq&nbsp;&nbsp;<span class="cnblogs_code">rabbitmqctl stop_app</span>&nbsp;</p>
<p>格式化rabbitmq&nbsp;&nbsp;&nbsp;<span class="cnblogs_code">rabbitmqctl reset</span>&nbsp;（格式化之前需要先关闭rabbitmq）</p>
<p>强制格式化rabbitmq&nbsp;&nbsp;&nbsp;<span class="cnblogs_code">rabbitmqctl force_reset</span>&nbsp;&nbsp;</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt;"><strong><span style="color: #ffffff;">二、ExChange</span></strong></span></p>
<p>1，Direct （直连）</p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201803/741594-20180329132744383-447062097.png" alt="" /></p>
<p>&nbsp;通过routingkey发送到指定的queue</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('e04f0686-cf4c-4f74-8c66-7271255fc65f')"><img id="code_img_closed_e04f0686-cf4c-4f74-8c66-7271255fc65f" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_e04f0686-cf4c-4f74-8c66-7271255fc65f" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('e04f0686-cf4c-4f74-8c66-7271255fc65f',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_e04f0686-cf4c-4f74-8c66-7271255fc65f" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> EasyNetQ;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> EasyNetQ.Topology;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> DirectConsumer
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #0000ff;">var</span> bus = RabbitHutch.CreateBus(<span style="color: #800000;">"</span><span style="color: #800000;">host=192.168.1.193:5672;username=hunter;password=hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">).Advanced;
            </span><span style="color: #0000ff;">var</span> ex= bus.ExchangeDeclare(<span style="color: #800000;">"</span><span style="color: #800000;">direct</span><span style="color: #800000;">"</span><span style="color: #000000;">, ExchangeType.Direct);
            </span><span style="color: #0000ff;">var</span> que= bus.QueueDeclare(<span style="color: #800000;">"</span><span style="color: #800000;">001</span><span style="color: #800000;">"</span>);<span style="color: #008000;">//</span><span style="color: #008000;">001为queue的名称</span>
            bus.Bind(ex, que, <span style="color: #800000;">"</span><span style="color: #800000;">000</span><span style="color: #800000;">"</span>);<span style="color: #008000;">//</span><span style="color: #008000;">000为routingkey</span>
<span style="color: #000000;">
            bus.Consume(que, (body, properties, info) </span>=&gt; Task.Factory.StartNew(() =&gt;<span style="color: #000000;">
            {
                </span><span style="color: #0000ff;">var</span> message =<span style="color: #000000;"> Encoding.UTF8.GetString(body);
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">Got message: '{0}'</span><span style="color: #800000;">"</span><span style="color: #000000;">, message);
            }));

            Console.ReadKey();
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">DirectConsumer</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('aeb091e9-a22e-4383-aef9-db43b66b4257')"><img id="code_img_closed_aeb091e9-a22e-4383-aef9-db43b66b4257" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_aeb091e9-a22e-4383-aef9-db43b66b4257" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('aeb091e9-a22e-4383-aef9-db43b66b4257',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_aeb091e9-a22e-4383-aef9-db43b66b4257" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> EasyNetQ;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> EasyNetQ.Topology;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> DirectProduce
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {

            </span><span style="color: #0000ff;">var</span> bus = RabbitHutch.CreateBus(<span style="color: #800000;">"</span><span style="color: #800000;">host=192.168.1.193:5672;username=hunter;password=hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">).Advanced;
            </span><span style="color: #0000ff;">var</span> ex = bus.ExchangeDeclare(<span style="color: #800000;">"</span><span style="color: #800000;">direct</span><span style="color: #800000;">"</span><span style="color: #000000;">, ExchangeType.Direct);a

            </span><span style="color: #0000ff;">var</span> message = <span style="color: #0000ff;">new</span> Message&lt;<span style="color: #0000ff;">string</span>&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">sad</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            </span><span style="color: #008000;">//</span><span style="color: #008000;">000:为routingkey</span>
            bus.Publish&lt;<span style="color: #0000ff;">string</span>&gt;(ex, <span style="color: #800000;">"</span><span style="color: #800000;">000</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">false</span><span style="color: #000000;">, message);

            bus.Dispose();

        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">DirectProduce</span></div>
<p>&nbsp;</p>
<p>2，Fanout（广播）</p>
<p>&nbsp;<img src="https://images2018.cnblogs.com/blog/741594/201803/741594-20180329132843484-628128589.png" alt="" /></p>
<p>&nbsp;</p>
<p>使用这种类型的Exchange，会忽略routing key的存在，直接将message广播到所有的Queue中。</p>
<h2>适用场景：</h2>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 第一：大型玩家在玩在线游戏的时候，可以用它来广播重大消息。这让我想到电影微微一笑很倾城中，有款游戏需要在世界上公布玩家重大消息，也许这个就是用的MQ实现的。这让我不禁佩服肖奈，人家在大学的时候就知道RabbitMQ的这种特性了。</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 第二：体育新闻实时更新到手机客户端。</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 第三：群聊功能，广播消息给当前群聊中的所有人。</p>
<p>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('ed3a0243-73f9-4dfa-b364-8e8dc1aef69b')"><img id="code_img_closed_ed3a0243-73f9-4dfa-b364-8e8dc1aef69b" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_ed3a0243-73f9-4dfa-b364-8e8dc1aef69b" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('ed3a0243-73f9-4dfa-b364-8e8dc1aef69b',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_ed3a0243-73f9-4dfa-b364-8e8dc1aef69b" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> EasyNetQ;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> EasyNetQ.Topology;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> FanoutConsumer
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            
            </span><span style="color: #0000ff;">var</span> bus = RabbitHutch.CreateBus(<span style="color: #800000;">"</span><span style="color: #800000;">host=192.168.1.193:5672;username=hunter;password=hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">).Advanced;
            </span><span style="color: #0000ff;">var</span> ex = bus.ExchangeDeclare(<span style="color: #800000;">"</span><span style="color: #800000;">fanout</span><span style="color: #800000;">"</span><span style="color: #000000;">, ExchangeType.Fanout);
            </span><span style="color: #0000ff;">var</span> que = bus.QueueDeclare(<span style="color: #800000;">"</span><span style="color: #800000;">directQueue</span><span style="color: #800000;">"</span>);<span style="color: #008000;">//</span><span style="color: #008000;">001为queue的名称</span>
            bus.Bind(ex, que, <span style="color: #0000ff;">string</span>.Empty);<span style="color: #008000;">//</span><span style="color: #008000;">Fanout不需要设置routingkey</span>
            bus.Consume(que, (body, properties, info) =&gt; Task.Factory.StartNew(() =&gt;<span style="color: #000000;">
            {
                </span><span style="color: #0000ff;">var</span> message =<span style="color: #000000;"> Encoding.UTF8.GetString(body);
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">Got message: '{0}'</span><span style="color: #800000;">"</span><span style="color: #000000;">, message);
            }));

            Console.ReadKey();

        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">FanoutConsumer</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('d85a349f-fd21-45f3-bd68-2349cb96c460')"><img id="code_img_closed_d85a349f-fd21-45f3-bd68-2349cb96c460" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_d85a349f-fd21-45f3-bd68-2349cb96c460" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('d85a349f-fd21-45f3-bd68-2349cb96c460',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_d85a349f-fd21-45f3-bd68-2349cb96c460" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> EasyNetQ;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> EasyNetQ.Topology;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> FanoutConsumer2
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #0000ff;">var</span> bus = RabbitHutch.CreateBus(<span style="color: #800000;">"</span><span style="color: #800000;">host=192.168.1.193:5672;username=hunter;password=hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">).Advanced;
            </span><span style="color: #0000ff;">var</span> ex = bus.ExchangeDeclare(<span style="color: #800000;">"</span><span style="color: #800000;">fanout</span><span style="color: #800000;">"</span><span style="color: #000000;">, ExchangeType.Fanout);
            </span><span style="color: #0000ff;">var</span> que = bus.QueueDeclare(<span style="color: #800000;">"</span><span style="color: #800000;">directQueue2</span><span style="color: #800000;">"</span>);<span style="color: #008000;">//</span><span style="color: #008000;">001为queue的名称</span>
            bus.Bind(ex, que, <span style="color: #0000ff;">string</span>.Empty);<span style="color: #008000;">//</span><span style="color: #008000;">Fanout不需要设置routingkey</span>
            bus.Consume(que, (body, properties, info) =&gt; Task.Factory.StartNew(() =&gt;<span style="color: #000000;">
            {
                </span><span style="color: #0000ff;">var</span> message =<span style="color: #000000;"> Encoding.UTF8.GetString(body);
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">Got message: '{0}'</span><span style="color: #800000;">"</span><span style="color: #000000;">, message);
            }));

            Console.ReadKey();
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">FanoutConsumer2</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('d0763edb-3671-48bc-9b1f-6721ae3298ce')"><img id="code_img_closed_d0763edb-3671-48bc-9b1f-6721ae3298ce" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_d0763edb-3671-48bc-9b1f-6721ae3298ce" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('d0763edb-3671-48bc-9b1f-6721ae3298ce',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_d0763edb-3671-48bc-9b1f-6721ae3298ce" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> EasyNetQ;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> EasyNetQ.Topology;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> FanoutProduce
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #0000ff;">var</span> bus = RabbitHutch.CreateBus(<span style="color: #800000;">"</span><span style="color: #800000;">host=192.168.1.193:5672;username=hunter;password=hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">).Advanced;
            </span><span style="color: #0000ff;">var</span> ex = bus.ExchangeDeclare(<span style="color: #800000;">"</span><span style="color: #800000;">fanout</span><span style="color: #800000;">"</span><span style="color: #000000;">, ExchangeType.Fanout);
            </span><span style="color: #0000ff;">var</span> message = <span style="color: #0000ff;">new</span> Message&lt;<span style="color: #0000ff;">string</span>&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">sad</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">Fanout不需要设置routingkey</span>
            bus.Publish&lt;<span style="color: #0000ff;">string</span>&gt;(ex, <span style="color: #0000ff;">string</span>.Empty, <span style="color: #0000ff;">false</span><span style="color: #000000;">, message);

            bus.Dispose();


        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">FanoutProduce</span></div>
<p>&nbsp;</p>
<p>3，Topic（主题）</p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201803/741594-20180329133138846-1534667199.png" alt="" /></p>
<p>Topic Exchange是根据routing key和Exchange的类型将message发送到一个或者多个Queue中</p>
<h2>使用场景：</h2>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;新闻的分类更新</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;同一任务多个工作者协调完成</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;同一问题需要特定人员知晓</p>
<p>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('21597565-de79-4c46-8222-64f4ab45da1d')"><img id="code_img_closed_21597565-de79-4c46-8222-64f4ab45da1d" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_21597565-de79-4c46-8222-64f4ab45da1d" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('21597565-de79-4c46-8222-64f4ab45da1d',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_21597565-de79-4c46-8222-64f4ab45da1d" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> EasyNetQ;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> TopicConsumer
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #0000ff;">var</span> bus = RabbitHutch.CreateBus(<span style="color: #800000;">"</span><span style="color: #800000;">host=192.168.1.193:5672;username=hunter;password=hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">正确的使用方法：
            </span><span style="color: #008000;">//</span><span style="color: #008000;">c=&gt; { c.WithTopic("*.cn"); }设置    Routing key。如果没有这句，则Routing key为#
            </span><span style="color: #008000;">//</span><span style="color: #008000;">*.com 只是queue的名称
            </span><span style="color: #008000;">//</span><span style="color: #008000;">bus.Subscribe&lt;string&gt;("*.com", r =&gt; Console.WriteLine(r),c=&gt; { c.WithTopic("*.cn"); });

            </span><span style="color: #008000;">//</span><span style="color: #008000;">subscriptionId是queue的名称
            </span><span style="color: #008000;">//</span><span style="color: #008000;">subscriptionId+exchangeType=唯一</span>
            bus.Subscribe&lt;<span style="color: #0000ff;">string</span>&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">*.com</span><span style="color: #800000;">"</span>, r =&gt;<span style="color: #000000;"> Console.WriteLine(r));
            bus.Subscribe</span>&lt;<span style="color: #0000ff;">string</span>&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">*.cn</span><span style="color: #800000;">"</span>, r =&gt;<span style="color: #000000;"> Console.WriteLine(r));

            Console.ReadKey();
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">TopicConsumer</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('e6431c55-b303-472d-9a0d-3db120199acc')"><img id="code_img_closed_e6431c55-b303-472d-9a0d-3db120199acc" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_e6431c55-b303-472d-9a0d-3db120199acc" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('e6431c55-b303-472d-9a0d-3db120199acc',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_e6431c55-b303-472d-9a0d-3db120199acc" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> EasyNetQ;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> TopicProduce
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #0000ff;">var</span> bus = RabbitHutch.CreateBus(<span style="color: #800000;">"</span><span style="color: #800000;">host=192.168.1.193:5672;username=hunter;password=hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            bus.Publish</span>&lt;<span style="color: #0000ff;">string</span>&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">你好</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">www.oyunkeji.com</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            </span><span style="color: #008000;">//</span><span style="color: #008000;">bus.Publish&lt;string&gt;("你好", c =&gt; c.WithTopic("www.oyunkeji.com"));</span>
<span style="color: #000000;">
            bus.Dispose();
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">TopicProduce</span></div>
<p>&nbsp;</p>
<p>4，Headers（头信息）</p>
<p>&nbsp;<img src="https://images2018.cnblogs.com/blog/741594/201803/741594-20180329133230358-1618512522.png" alt="" /></p>
<p>它是根据Message的一些头部信息来分发过滤Message，忽略routing key的属性，如果Header信息和message消息的头信息相匹配，那么这条消息就匹配上了</p>
<p>x-match的头部必须设置：</p>
<p>当x-match的值设置为all时，header信息必须全部满足才会匹配上</p>
<p>当x-match的值设置为any时，header信息满足其中任意一个就会匹配上</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('6b824dc4-681c-4628-a7b2-291b4c131b6a')"><img id="code_img_closed_6b824dc4-681c-4628-a7b2-291b4c131b6a" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_6b824dc4-681c-4628-a7b2-291b4c131b6a" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('6b824dc4-681c-4628-a7b2-291b4c131b6a',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_6b824dc4-681c-4628-a7b2-291b4c131b6a" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> EasyNetQ;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> EasyNetQ.Topology;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> HeadersConsumer
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #0000ff;">var</span> bus = RabbitHutch.CreateBus(<span style="color: #800000;">"</span><span style="color: #800000;">host=192.168.1.193:5672;username=hunter;password=hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">).Advanced;
            </span><span style="color: #0000ff;">var</span> ex = bus.ExchangeDeclare(<span style="color: #800000;">"</span><span style="color: #800000;">headers</span><span style="color: #800000;">"</span><span style="color: #000000;">, ExchangeType.Header);
            </span><span style="color: #0000ff;">var</span> que = bus.QueueDeclare(<span style="color: #800000;">"</span><span style="color: #800000;">headersQueue</span><span style="color: #800000;">"</span>);<span style="color: #008000;">//</span><span style="color: #008000;">001为queue的名称</span>
            bus.Bind(ex, que, <span style="color: #0000ff;">string</span>.Empty,<span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">() {
                { </span><span style="color: #800000;">"</span><span style="color: #800000;">x-match</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">all</span><span style="color: #800000;">"</span><span style="color: #000000;">},
                { </span><span style="color: #800000;">"</span><span style="color: #800000;">username</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">},
                { </span><span style="color: #800000;">"</span><span style="color: #800000;">password</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">}
            });</span><span style="color: #008000;">//</span><span style="color: #008000;">Header不需要设置routingkey</span>
            bus.Consume(que, (body, properties, info) =&gt; Task.Factory.StartNew(() =&gt;<span style="color: #000000;">
            {
                </span><span style="color: #0000ff;">var</span> message =<span style="color: #000000;"> Encoding.UTF8.GetString(body);
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">Got message: '{0}'</span><span style="color: #800000;">"</span><span style="color: #000000;">, message);
            }));

            Console.ReadKey();

        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">HeadersConsumer</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('c2967d29-cc0a-4365-bb65-e6c25bbb3140')"><img id="code_img_closed_c2967d29-cc0a-4365-bb65-e6c25bbb3140" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_c2967d29-cc0a-4365-bb65-e6c25bbb3140" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('c2967d29-cc0a-4365-bb65-e6c25bbb3140',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_c2967d29-cc0a-4365-bb65-e6c25bbb3140" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> EasyNetQ;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> EasyNetQ.Topology;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> HeadersProduce
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #0000ff;">var</span> bus = RabbitHutch.CreateBus(<span style="color: #800000;">"</span><span style="color: #800000;">host=192.168.1.193:5672;username=hunter;password=hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">).Advanced;
            </span><span style="color: #0000ff;">var</span> ex = bus.ExchangeDeclare(<span style="color: #800000;">"</span><span style="color: #800000;">headers</span><span style="color: #800000;">"</span><span style="color: #000000;">, ExchangeType.Header);

            </span><span style="color: #0000ff;">var</span> properties = <span style="color: #0000ff;">new</span><span style="color: #000000;"> MessageProperties();
            properties.Headers.Add(</span><span style="color: #800000;">"</span><span style="color: #800000;">username</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            properties.Headers.Add(</span><span style="color: #800000;">"</span><span style="color: #800000;">password</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">Fanout不需要设置routingkey</span>
            bus.Publish(ex, <span style="color: #0000ff;">string</span>.Empty, <span style="color: #0000ff;">false</span>, properties, Encoding.UTF8.GetBytes(<span style="color: #800000;">"</span><span style="color: #800000;">你好</span><span style="color: #800000;">"</span><span style="color: #000000;">));
            bus.Dispose();

        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">HeadersProduce</span></div>
<p>&nbsp;</p>
<p>案例下载：<a href="https://pan.baidu.com/s/1gVBO3qLl9Dw5tIhIpETvkw" target="_blank">https://pan.baidu.com/s/1gVBO3qLl9Dw5tIhIpETvkw</a></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">三、Arguments</span></strong></p>
<p>1，Message TTL（x-message-ttl）</p>
<p>发布到队列的消息在丢弃之前可以存活多长时间（毫秒）。</p>
<p>①针对队列中的所有消息</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('a7523049-cfc6-4519-b032-454f40aa5c5a')"><img id="code_img_closed_a7523049-cfc6-4519-b032-454f40aa5c5a" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_a7523049-cfc6-4519-b032-454f40aa5c5a" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('a7523049-cfc6-4519-b032-454f40aa5c5a',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_a7523049-cfc6-4519-b032-454f40aa5c5a" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> EasyNetQ;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> EasyNetQ.Topology;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ConsoleApp1
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #0000ff;">var</span> bus = RabbitHutch.CreateBus(<span style="color: #800000;">"</span><span style="color: #800000;">host=localhost:5672;username=hunter;password=hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">).Advanced;
            </span><span style="color: #0000ff;">var</span> ex = bus.ExchangeDeclare(<span style="color: #800000;">"</span><span style="color: #800000;">directText</span><span style="color: #800000;">"</span><span style="color: #000000;">, ExchangeType.Direct);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">001为queue的名称
            </span><span style="color: #008000;">//</span><span style="color: #008000;">001队列下的消息5秒钟没有被消费自动删除</span>
            <span style="color: #0000ff;">var</span> que = bus.QueueDeclare(<span style="color: #800000;">"</span><span style="color: #800000;">001</span><span style="color: #800000;">"</span>,perQueueMessageTtl:<span style="color: #800080;">5000</span><span style="color: #000000;">);
            bus.Bind(ex, que, </span><span style="color: #800000;">"</span><span style="color: #800000;">000</span><span style="color: #800000;">"</span>);<span style="color: #008000;">//</span><span style="color: #008000;">000为routingkey</span>
<span style="color: #000000;">
            bus.Consume(que, (body, properties, info) </span>=&gt; Task.Factory.StartNew(() =&gt;<span style="color: #000000;">
            {
                </span><span style="color: #0000ff;">var</span> message =<span style="color: #000000;"> Encoding.UTF8.GetString(body);
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">Got message: '{0}'</span><span style="color: #800000;">"</span><span style="color: #000000;">, message);
            }));


            Console.ReadKey();
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">consumer</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('63016384-3f7f-43f4-968e-affae4ac17b2')"><img id="code_img_closed_63016384-3f7f-43f4-968e-affae4ac17b2" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_63016384-3f7f-43f4-968e-affae4ac17b2" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('63016384-3f7f-43f4-968e-affae4ac17b2',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_63016384-3f7f-43f4-968e-affae4ac17b2" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> EasyNetQ;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> EasyNetQ.Topology;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq.Expressions;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ConsoleApp2
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #0000ff;">var</span> bus = RabbitHutch.CreateBus(<span style="color: #800000;">"</span><span style="color: #800000;">host=localhost:5672;username=hunter;password=hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">).Advanced;
            </span><span style="color: #0000ff;">var</span> ex = bus.ExchangeDeclare(<span style="color: #800000;">"</span><span style="color: #800000;">directText</span><span style="color: #800000;">"</span><span style="color: #000000;">, ExchangeType.Direct);
            </span><span style="color: #0000ff;">var</span> properties = <span style="color: #0000ff;">new</span><span style="color: #000000;"> MessageProperties();
            </span><span style="color: #0000ff;">var</span> message = <span style="color: #0000ff;">new</span> Message&lt;<span style="color: #0000ff;">string</span>&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">你好</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            </span><span style="color: #008000;">//</span><span style="color: #008000;">000:为routingkey</span>
            bus.Publish&lt;<span style="color: #0000ff;">string</span>&gt;(ex, <span style="color: #800000;">"</span><span style="color: #800000;">000</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">false</span><span style="color: #000000;">, message);

            bus.Dispose();

        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">produce</span></div>
<p>②指定某个消息</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('76a43063-ce25-411c-bc4b-4bd5b81f8e88')"><img id="code_img_closed_76a43063-ce25-411c-bc4b-4bd5b81f8e88" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_76a43063-ce25-411c-bc4b-4bd5b81f8e88" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('76a43063-ce25-411c-bc4b-4bd5b81f8e88',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_76a43063-ce25-411c-bc4b-4bd5b81f8e88" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> EasyNetQ;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> EasyNetQ.Topology;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ConsoleApp1
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #0000ff;">var</span> bus = RabbitHutch.CreateBus(<span style="color: #800000;">"</span><span style="color: #800000;">host=localhost:5672;username=hunter;password=hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">).Advanced;
            </span><span style="color: #0000ff;">var</span> ex = bus.ExchangeDeclare(<span style="color: #800000;">"</span><span style="color: #800000;">directText</span><span style="color: #800000;">"</span><span style="color: #000000;">, ExchangeType.Direct);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">001为queue的名称
            </span><span style="color: #008000;">//</span><span style="color: #008000;">001队列下的消息5秒钟没有被消费自动删除</span>
            <span style="color: #0000ff;">var</span> que = bus.QueueDeclare(<span style="color: #800000;">"</span><span style="color: #800000;">001</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            bus.Bind(ex, que, </span><span style="color: #800000;">"</span><span style="color: #800000;">000</span><span style="color: #800000;">"</span>);<span style="color: #008000;">//</span><span style="color: #008000;">000为routingkey</span>
<span style="color: #000000;">
            bus.Consume(que, (body, properties, info) </span>=&gt; Task.Factory.StartNew(() =&gt;<span style="color: #000000;">
            {
                </span><span style="color: #0000ff;">var</span> message =<span style="color: #000000;"> Encoding.UTF8.GetString(body);
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">Got message: '{0}'</span><span style="color: #800000;">"</span><span style="color: #000000;">, message);
            }));


            Console.ReadKey();
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">consumer</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('3278e102-11a8-4850-a24b-13a396e6e957')"><img id="code_img_closed_3278e102-11a8-4850-a24b-13a396e6e957" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_3278e102-11a8-4850-a24b-13a396e6e957" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('3278e102-11a8-4850-a24b-13a396e6e957',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_3278e102-11a8-4850-a24b-13a396e6e957" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> EasyNetQ;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> EasyNetQ.Topology;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq.Expressions;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ConsoleApp2
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #0000ff;">var</span> bus = RabbitHutch.CreateBus(<span style="color: #800000;">"</span><span style="color: #800000;">host=localhost:5672;username=hunter;password=hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">).Advanced;
            </span><span style="color: #0000ff;">var</span> ex = bus.ExchangeDeclare(<span style="color: #800000;">"</span><span style="color: #800000;">directText</span><span style="color: #800000;">"</span><span style="color: #000000;">, ExchangeType.Direct);
            </span><span style="color: #0000ff;">var</span> properties = <span style="color: #0000ff;">new</span><span style="color: #000000;"> MessageProperties();
            properties.Expiration </span>= <span style="color: #800000;">"</span><span style="color: #800000;">5000</span><span style="color: #800000;">"</span>;<span style="color: #008000;">//</span><span style="color: #008000;">单位：毫秒
            </span><span style="color: #008000;">//</span><span style="color: #008000;">000:为routingkey</span>
            bus.Publish(ex, <span style="color: #800000;">"</span><span style="color: #800000;">000</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">false</span>, properties, Encoding.UTF8.GetBytes(<span style="color: #800000;">"</span><span style="color: #800000;">你好</span><span style="color: #800000;">"</span><span style="color: #000000;">));

            bus.Dispose();

        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">produce</span></div>
<p>2，Auto expire（x-expires）</p>
<p>&nbsp;queue在指定的时间未被访问，就会被删除（毫秒）。</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>3，Max length（x-max-length）</p>
<p>限定队列的最大长度，</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>4，Max length bytes（x-max-length-bytes）</p>
<p>限定队列的最大占用空间大小</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>5，Overflow behaviour（x-overflow）</p>
<p>&nbsp;设置队列溢出行为。这决定了在到达队列的最大长度时消息会发生什么情况。有效值是&nbsp;drop-head（删除头）或者 reject-publish（拒绝发布） 。</p>
<p>&nbsp;</p>
<p>6，Dead letter exchange/Dead letter routing key（x-dead-letter-exchange/x-dead-letter-routing-key）</p>
<p>queue中的message过期时间。</p>
<p>basicreject...basicnack等等。。。</p>
<p>这三种情况一般会drop这些message。。。</p>
<p>Dead letter exchange：时候我们不希望message被drop掉，而是走到另一个队列中，又或者是保存起来</p>
<p>Dead letter routing key：指定的routing key</p>
<p>&nbsp;</p>
<p>8，Maximum priority</p>
<p>（x-max-priority）</p>
<p>定义消息的优先级</p>
<p>&nbsp;</p>
<p>9，Lazy mode（x-queue-mode）</p>
<p>将队列设置为延迟模式，在磁盘上保留尽可能多的消息以减少RAM使用量; 如果未设置，队列将保留内存中的缓存以尽可能快地传递消息。</p>
<p>&nbsp;</p>
<p>10，Master locator&nbsp;（x-queue-master-locator）</p>
<p>将队列设置为主位置模式，确定队列主节点在节点集群上声明时所处的规则。<br /><br /></p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">四、高可靠消息队列</span></strong></span></p>
<p>1，消费端的确认</p>
<p>①自动确认</p>
<p>message出队列的时候就自动确认</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('7df41bd0-c319-4989-aaa7-419176fb8e7d')"><img id="code_img_closed_7df41bd0-c319-4989-aaa7-419176fb8e7d" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_7df41bd0-c319-4989-aaa7-419176fb8e7d" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('7df41bd0-c319-4989-aaa7-419176fb8e7d',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_7df41bd0-c319-4989-aaa7-419176fb8e7d" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> RabbitMQ.Client;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> RabbitMQ.Client.Events;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> Consumer
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            ConnectionFactory factory </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> ConnectionFactory()
            {
                HostName </span>= <span style="color: #800000;">"</span><span style="color: #800000;">localhost</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                Port </span>= <span style="color: #800080;">5672</span><span style="color: #000000;">,
                UserName </span>= <span style="color: #800000;">"</span><span style="color: #800000;">hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                Password </span>= <span style="color: #800000;">"</span><span style="color: #800000;">hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">
            };

            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建connection</span>
            <span style="color: #0000ff;">var</span> connection =<span style="color: #000000;"> factory.CreateConnection();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建chanel</span>
            <span style="color: #0000ff;">var</span> channel =<span style="color: #000000;"> connection.CreateModel();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建exchange</span>
            channel.ExchangeDeclare(<span style="color: #800000;">"</span><span style="color: #800000;">exchange1</span><span style="color: #800000;">"</span>, ExchangeType.Direct, <span style="color: #0000ff;">true</span>, <span style="color: #0000ff;">false</span>, <span style="color: #0000ff;">null</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建queue</span>
            channel.QueueDeclare(<span style="color: #800000;">"</span><span style="color: #800000;">queue1</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">true</span>, <span style="color: #0000ff;">false</span>, <span style="color: #0000ff;">false</span>, <span style="color: #0000ff;">null</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">exchange绑定queue</span>
            channel.QueueBind(<span style="color: #800000;">"</span><span style="color: #800000;">queue1</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">exchange1</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">queue1</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">null</span><span style="color: #000000;">);


            EventingBasicConsumer consumer </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> EventingBasicConsumer(channel);
            consumer.Received </span>+= (send, e) =&gt;<span style="color: #000000;">
            {
                Console.WriteLine(Encoding.UTF8.GetString(e.Body));
            };

            </span><span style="color: #008000;">//</span><span style="color: #008000;">autoAck 设置为true：自动确认</span>
            channel.BasicConsume(<span style="color: #800000;">"</span><span style="color: #800000;">queue1</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">true</span><span style="color: #000000;">, consumer);

            Console.ReadKey();
        }

    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Consumer</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('5e2991af-cb58-4b07-af72-08b76dd43183')"><img id="code_img_closed_5e2991af-cb58-4b07-af72-08b76dd43183" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_5e2991af-cb58-4b07-af72-08b76dd43183" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('5e2991af-cb58-4b07-af72-08b76dd43183',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_5e2991af-cb58-4b07-af72-08b76dd43183" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> RabbitMQ.Client;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> Produce
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            ConnectionFactory factory </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> ConnectionFactory()
            {
                HostName </span>= <span style="color: #800000;">"</span><span style="color: #800000;">localhost</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                Port </span>= <span style="color: #800080;">5672</span><span style="color: #000000;">,
                UserName </span>= <span style="color: #800000;">"</span><span style="color: #800000;">hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                Password </span>= <span style="color: #800000;">"</span><span style="color: #800000;">hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">
            };

            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建connection</span>
            <span style="color: #0000ff;">var</span> connection =<span style="color: #000000;"> factory.CreateConnection();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建chanel</span>
            <span style="color: #0000ff;">var</span> channel =<span style="color: #000000;"> connection.CreateModel();

            </span><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> i = <span style="color: #800080;">0</span>; i &lt; <span style="color: #800080;">10</span>; i++<span style="color: #000000;">)
            {
                channel.BasicPublish(</span><span style="color: #800000;">"</span><span style="color: #800000;">exchange1</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">queue1</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">null</span><span style="color: #000000;">, Encoding.UTF8.GetBytes(i.ToString()));
            }

            channel.Dispose();

            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">发布完毕</span><span style="color: #800000;">"</span><span style="color: #000000;">);


            Console.ReadKey();

        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Produce</span></div>
<p>②手动确认</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('1b9fa393-0229-4abb-816b-aaed1962c489')"><img id="code_img_closed_1b9fa393-0229-4abb-816b-aaed1962c489" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_1b9fa393-0229-4abb-816b-aaed1962c489" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('1b9fa393-0229-4abb-816b-aaed1962c489',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_1b9fa393-0229-4abb-816b-aaed1962c489" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> RabbitMQ.Client;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> RabbitMQ.Client.Events;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> Consumer
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            ConnectionFactory factory </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> ConnectionFactory()
            {
                HostName </span>= <span style="color: #800000;">"</span><span style="color: #800000;">localhost</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                Port </span>= <span style="color: #800080;">5672</span><span style="color: #000000;">,
                UserName </span>= <span style="color: #800000;">"</span><span style="color: #800000;">hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                Password </span>= <span style="color: #800000;">"</span><span style="color: #800000;">hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">
            };

            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建connection</span>
            <span style="color: #0000ff;">var</span> connection =<span style="color: #000000;"> factory.CreateConnection();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建chanel</span>
            <span style="color: #0000ff;">var</span> channel =<span style="color: #000000;"> connection.CreateModel();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建exchange</span>
            channel.ExchangeDeclare(<span style="color: #800000;">"</span><span style="color: #800000;">exchange1</span><span style="color: #800000;">"</span>, ExchangeType.Direct, <span style="color: #0000ff;">true</span>, <span style="color: #0000ff;">false</span>, <span style="color: #0000ff;">null</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建queue</span>
            channel.QueueDeclare(<span style="color: #800000;">"</span><span style="color: #800000;">queue1</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">true</span>, <span style="color: #0000ff;">false</span>, <span style="color: #0000ff;">false</span>, <span style="color: #0000ff;">null</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">exchange绑定queue</span>
            channel.QueueBind(<span style="color: #800000;">"</span><span style="color: #800000;">queue1</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">exchange1</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">queue1</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">null</span><span style="color: #000000;">);

            </span><span style="color: #0000ff;">var</span> result = channel.BasicGet(<span style="color: #800000;">"</span><span style="color: #800000;">queue1</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">false</span><span style="color: #000000;">);

            Console.WriteLine(Encoding.UTF8.GetString(result.Body));

            </span><span style="color: #008000;">//</span><span style="color: #008000;">拒绝掉
            </span><span style="color: #008000;">//</span><span style="color: #008000;">requeue:true:重新放回队列 false:直接丢弃</span>
            channel.BasicReject(result.DeliveryTag, <span style="color: #0000ff;">false</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">BasicRecover方法则是进行补发操作，
            </span><span style="color: #008000;">//</span><span style="color: #008000;">其中的参数如果为true是把消息退回到queue但是有可能被其它的consumer接收到，设置为false是只补发给当前的consumer
            </span><span style="color: #008000;">//</span><span style="color: #008000;">channel.BasicRecover(true);</span>
<span style="color: #000000;">
            Console.ReadKey();
        }

    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Consumer</span></div>
<p>&nbsp;</p>
<p>2，发布端的确认</p>
<p>其中事务的性能消耗最大，confirm其次</p>
<p>①confirm机制</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('b7f9eda3-c277-439f-89a2-8949736e0031')"><img id="code_img_closed_b7f9eda3-c277-439f-89a2-8949736e0031" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_b7f9eda3-c277-439f-89a2-8949736e0031" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('b7f9eda3-c277-439f-89a2-8949736e0031',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_b7f9eda3-c277-439f-89a2-8949736e0031" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> RabbitMQ.Client;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> Produce
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            ConnectionFactory factory </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> ConnectionFactory()
            {
                HostName </span>= <span style="color: #800000;">"</span><span style="color: #800000;">localhost</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                Port </span>= <span style="color: #800080;">5672</span><span style="color: #000000;">,
                UserName </span>= <span style="color: #800000;">"</span><span style="color: #800000;">hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                Password </span>= <span style="color: #800000;">"</span><span style="color: #800000;">hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">
            };

            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建connection</span>
            <span style="color: #0000ff;">var</span> connection =<span style="color: #000000;"> factory.CreateConnection();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建chanel</span>
            <span style="color: #0000ff;">var</span> channel =<span style="color: #000000;"> connection.CreateModel();

            channel.ConfirmSelect();
            </span><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> i = <span style="color: #800080;">0</span>; i &lt; <span style="color: #800080;">10000</span>; i++<span style="color: #000000;">)
            {
                channel.BasicPublish(</span><span style="color: #800000;">"</span><span style="color: #800000;">exchange1</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">queue1</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">null</span><span style="color: #000000;">, Encoding.UTF8.GetBytes(i.ToString()));
            }
            </span><span style="color: #0000ff;">var</span> isallPublish =<span style="color: #000000;"> channel.WaitForConfirms();
            Console.WriteLine(isallPublish);

            channel.Dispose();
            connection.Dispose();

            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">发布完毕</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            Console.ReadKey();

        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Produce</span></div>
<p>② 事物机制</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('c267b370-b771-43c3-9651-271e123e2e44')"><img id="code_img_closed_c267b370-b771-43c3-9651-271e123e2e44" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_c267b370-b771-43c3-9651-271e123e2e44" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('c267b370-b771-43c3-9651-271e123e2e44',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_c267b370-b771-43c3-9651-271e123e2e44" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> RabbitMQ.Client;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> Produce
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            ConnectionFactory factory </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> ConnectionFactory()
            {
                HostName </span>= <span style="color: #800000;">"</span><span style="color: #800000;">localhost</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                Port </span>= <span style="color: #800080;">5672</span><span style="color: #000000;">,
                UserName </span>= <span style="color: #800000;">"</span><span style="color: #800000;">hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                Password </span>= <span style="color: #800000;">"</span><span style="color: #800000;">hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">
            };

            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建connection</span>
            <span style="color: #0000ff;">var</span> connection =<span style="color: #000000;"> factory.CreateConnection();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建chanel</span>
            <span style="color: #0000ff;">var</span> channel =<span style="color: #000000;"> connection.CreateModel();

            </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
            {
                channel.TxSelect();
                </span><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> i = <span style="color: #800080;">0</span>; i &lt; <span style="color: #800080;">10000</span>; i++<span style="color: #000000;">)
                {
                    channel.BasicPublish(</span><span style="color: #800000;">"</span><span style="color: #800000;">exchange1</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">queue1</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">null</span><span style="color: #000000;">, Encoding.UTF8.GetBytes(i.ToString()));
                }
                channel.TxCommit();
            }
            </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (Exception ex)
            {
                channel.TxRollback();
            }

            channel.Dispose();
            connection.Dispose();

            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">发布完毕</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            Console.ReadKey();

        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Produce</span></div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">五、Consumer消费问题</span></strong></p>
<p>Consumer消费时，不管你是否却不确认，消息都会一股脑全部打入到你的consumer中去，导致consumer端内存暴涨（EasynetQ的Subscribe不会出现这种情况）</p>
<p>解决方法：</p>
<p>&nbsp;①eventbasicconsumer+QOS</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('158e879c-829d-470f-875d-5f447f8d4cf1')"><img id="code_img_closed_158e879c-829d-470f-875d-5f447f8d4cf1" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_158e879c-829d-470f-875d-5f447f8d4cf1" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('158e879c-829d-470f-875d-5f447f8d4cf1',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_158e879c-829d-470f-875d-5f447f8d4cf1" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> RabbitMQ.Client;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> RabbitMQ.Client.Events;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> EasyNetQ;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> Consumer
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            ConnectionFactory factory </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> ConnectionFactory()
            {
                HostName </span>= <span style="color: #800000;">"</span><span style="color: #800000;">localhost</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                Port </span>= <span style="color: #800080;">5672</span><span style="color: #000000;">,
                UserName </span>= <span style="color: #800000;">"</span><span style="color: #800000;">hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                Password </span>= <span style="color: #800000;">"</span><span style="color: #800000;">hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">
            };

            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建connection</span>
            <span style="color: #0000ff;">var</span> connection =<span style="color: #000000;"> factory.CreateConnection();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建chanel</span>
            <span style="color: #0000ff;">var</span> channel =<span style="color: #000000;"> connection.CreateModel();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建exchange</span>
            channel.ExchangeDeclare(<span style="color: #800000;">"</span><span style="color: #800000;">exchange1</span><span style="color: #800000;">"</span>, ExchangeType.Direct, <span style="color: #0000ff;">true</span>, <span style="color: #0000ff;">false</span>, <span style="color: #0000ff;">null</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建queue</span>
            channel.QueueDeclare(<span style="color: #800000;">"</span><span style="color: #800000;">queue1</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">true</span>, <span style="color: #0000ff;">false</span>, <span style="color: #0000ff;">false</span>, <span style="color: #0000ff;">null</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">exchange绑定queue</span>
            channel.QueueBind(<span style="color: #800000;">"</span><span style="color: #800000;">queue1</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">exchange1</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">queue1</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">null</span><span style="color: #000000;">);


            </span><span style="color: #008000;">//</span><span style="color: #008000;">prefetchSize:预取大小   prefetchCount:预取数量</span>
            channel.BasicQos(<span style="color: #800080;">0</span>, <span style="color: #800080;">1</span>, <span style="color: #0000ff;">false</span><span style="color: #000000;">);

            EventingBasicConsumer consumer </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> EventingBasicConsumer(channel);
            consumer.Received </span>+= (send, e) =&gt;<span style="color: #000000;">
            {
                Console.WriteLine(Encoding.UTF8.GetString(e.Body));

                channel.BasicAck(e.DeliveryTag, </span><span style="color: #0000ff;">false</span>);<span style="color: #008000;">//</span><span style="color: #008000;">确认送达</span>
                Thread.Sleep(<span style="color: #800080;">1000000</span><span style="color: #000000;">);
            };

            </span><span style="color: #008000;">//</span><span style="color: #008000;">autoAck 设置为true：自动确认</span>
            channel.BasicConsume(<span style="color: #800000;">"</span><span style="color: #800000;">queue1</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">false</span><span style="color: #000000;">, consumer);


            Console.ReadKey();

            Console.ReadKey();
        }

    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Consumer</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('c263f1ca-1c8a-45c5-a7d0-d3ad393a71e7')"><img id="code_img_closed_c263f1ca-1c8a-45c5-a7d0-d3ad393a71e7" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_c263f1ca-1c8a-45c5-a7d0-d3ad393a71e7" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('c263f1ca-1c8a-45c5-a7d0-d3ad393a71e7',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_c263f1ca-1c8a-45c5-a7d0-d3ad393a71e7" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> RabbitMQ.Client;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> Produce
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            ConnectionFactory factory </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> ConnectionFactory()
            {
                HostName </span>= <span style="color: #800000;">"</span><span style="color: #800000;">localhost</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                Port </span>= <span style="color: #800080;">5672</span><span style="color: #000000;">,
                UserName </span>= <span style="color: #800000;">"</span><span style="color: #800000;">hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                Password </span>= <span style="color: #800000;">"</span><span style="color: #800000;">hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">
            };

            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建connection</span>
            <span style="color: #0000ff;">var</span> connection =<span style="color: #000000;"> factory.CreateConnection();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建chanel</span>
            <span style="color: #0000ff;">var</span> channel =<span style="color: #000000;"> connection.CreateModel();

            </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
            {
                channel.TxSelect();
                </span><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> i = <span style="color: #800080;">0</span>; i &lt; <span style="color: #800080;">10000</span>; i++<span style="color: #000000;">)
                {
                    channel.BasicPublish(</span><span style="color: #800000;">"</span><span style="color: #800000;">exchange1</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">queue1</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">null</span><span style="color: #000000;">, Encoding.UTF8.GetBytes(i.ToString()));
                }
                channel.TxCommit();
            }
            </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (Exception ex)
            {
                channel.TxRollback();
            }

            channel.Dispose();
            connection.Dispose();

            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">发布完毕</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            Console.ReadKey();

        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Produce</span></div>
<p>&nbsp;</p>