<p>要启用对版本化消息的支持，您需要确保配置所需的组件。 最简单的方法是：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> bus = RabbitHutch.CreateBus( <span style="color: #800000;">"</span><span style="color: #800000;">host=localhost</span><span style="color: #800000;">"</span>, services =&gt; services.EnableMessageVersioning() )</pre>
</div>
<p>一旦启用了对版本化消息的支持，您必须明确选择任何您希望被视为版本化的消息。</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> 此消息未经过版本控制，在发布时将按照与其他任何方式相同的方式进行处理</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyMessage
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Text { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 这条消息是版本化的，并且会发现它是MyMessageV2和MyMessage订阅者的方式</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> MyMessageV2 : MyMessage, ISupersede&lt;MyMessage&gt;<span style="color: #000000;">
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span> Number { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}</span></pre>
</div>
<p>1，它是如何工作的</p>
<p>当您发布消息时，EasyNetQ通常会为消息类型创建一个交换并将消息发布到该交换。 订户创建绑定到交易所的队列，因此接收发布给它的任何消息。</p>
<p>在启用消息版本控制的情况下，EasyNetQ将为版本层次结构中的每个消息类型创建一个交换，并将这些交换绑定在一起。 当您发布MyMessageV2消息时，它将被发送到MyMessageV2交换机，它将自动将其转发到MyMessage交换机。</p>
<p>消息序列化时，EasyNetQ将消息类型名称存储在消息属性的Type属性中。 此元数据与您的消息一起发送给任何可以使用它反序列化消息的订阅者。</p>
<p>在启用消息版本控制的情况下，EasyNetQ还会将所有被取代的消息类型存储在消息属性的标题中。 订阅者将使用它来找到消息可以被反序列化的第一种可用类型，意思是即使端点没有最新版本的消息，只要它有一个版本，它也可以被反序列化和处理。</p>
<p>&nbsp;</p>
<p>2，消息版本指导</p>
<ol>
<li>如果更改无法通过扩展原始消息类型来实现，那么它不是消息的新版本，而是新的消息类型。</li>
<li>如果您不确定，则倾向于创建新的消息类型，而不是现有消息的版本。</li>
<li>Versioned消息不应该与请求/响应一起使用，因为消息类型是请求/响应协定的一部分，并且即使V2扩展了V1，Request &lt;V1，Response&gt;与Request &lt;V2，Response&gt;也不相同（即公共类V2 ：V1 {}）</li>
<li>Versioned消息不应该用于发送/接收，因为这是针对性的发送，因此发送者和接收者之间存在声明的依赖关系。</li>
</ol>
<p>&nbsp;</p>