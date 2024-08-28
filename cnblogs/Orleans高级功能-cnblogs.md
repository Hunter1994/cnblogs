<p><a href="#a1">一、Reentrant Grains</a><br /><a href="#a2">二、请求上下文</a><br /><a href="#a3">三、激活垃圾收集</a><br /><a href="#a4">四、外部任务和Grains</a><br /><a href="#a5">五、序列化</a><br /><a href="#a6">六、代码生成</a><br /><a href="#a7">七、在Silo内的应用程序引导</a><br /><a href="#a8">八、拦截器</a><br /><a href="#a9">九、取消令牌</a><br /><a href="#a10">十、Powershell客户端</a><br /><a href="#a11">十一、Grains版本控制</a><br /><a href="#a12">十二、Event Sourcing</a><br /><a href="#a13">十三、多群集支持</a></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a1"></a>一、Reentrant Grains</span></strong></p>
<p>Grain类有以下两个方法</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">Task Foo()
{
    </span><span style="color: #0000ff;">await</span> task1;    <span style="color: #008000;">//</span><span style="color: #008000;"> line 1</span>
    <span style="color: #0000ff;">return</span> Do2();   <span style="color: #008000;">//</span><span style="color: #008000;"> line 2</span>
<span style="color: #000000;">}

Task Bar()
{
    </span><span style="color: #0000ff;">await</span> task2;   <span style="color: #008000;">//</span><span style="color: #008000;"> line 3</span>
    <span style="color: #0000ff;">return</span> Do2();  <span style="color: #008000;">//</span><span style="color: #008000;"> line 4</span>
}</pre>
</div>
<p>如果将这个grain标记为[Reentrant]，下面的执行顺序是可能会发生：第1行，第3行，第2行和第4行。</p>
<p>如果将这个grain没有标记为[Reentrant]，唯一可能的执行将是第1行，第2行，第3行，第4行或者第3行第4行第1行第2行（这个grain是单线程执行的）</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a2"></a>二、请求上下文</span></strong></p>
<p>1，RequestContext包含两个方法：</p>
<p>void Set(string key，object value)用于在请求上下文中存储一个值。该值可以是任何可序列化类型。 Object Get(string key)用于从当前请求上下文中检索一个值&nbsp;</p>
<p>2，例如，要将客户端中的跟踪标识设置为新的GUID，可以简单地调用：</p>
<div class="cnblogs_code">
<pre>RequestContext.Set(<span style="color: #800000;">"</span><span style="color: #800000;">TraceId</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span> Guid());</pre>
</div>
<p>在grain代码中(或在调度线程中运行在Orleans的其他代码)，可以使用原始客户机请求的跟踪ID，例如，在写入日志时:</p>
<div class="cnblogs_code">
<pre>Logger.Info(<span style="color: #800000;">"</span><span style="color: #800000;">Currently processing external request {0}</span><span style="color: #800000;">"</span>, RequestContext.Get(<span style="color: #800000;">"</span><span style="color: #800000;">TraceId</span><span style="color: #800000;">"</span>));</pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a3"></a>三、激活垃圾收集</span></strong></p>
<p>1,激活垃圾收集的显式控制&nbsp;</p>
<p>①延迟激活GC</p>
<p>grain激活可以通过调用this.DelayDeactivation()方法来延迟自己的激活GC：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">void</span> DelayDeactivation(TimeSpan timeSpan)</pre>
</div>
<p>②加快激活GC</p>
<p>通过调用this.DeactivateOnIdle()方法，grain激活还可以指示运行时在下次空闲时停用它。</p>
<div class="cnblogs_code">
<pre> <span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">void</span> DeactivateOnIdle()</pre>
</div>
<p>如果目前没有处理任何消息，则谷物激活被认为是空闲的。 如果在grain正在处理消息时调用DeactivateOnIdle，则当前消息的处理完成后将立即停用。 如果有任何排队等待谷物的请求，它们将被转发到下一个激活。</p>
<p>DeactivateOnIdle优先于配置或DelayDeactivation中指定的任何激活垃圾收集设置。 请注意，此设置仅适用于所谓的grain激活，并不适用于此类grain的其他激活。</p>
<p>2，配置</p>
<p>①编程配置</p>
<p>默认Collection Age Limit（所有grain类型）可以通过以下方式设置：</p>
<div class="cnblogs_code">
<pre>  <span style="color: #0000ff;">void</span> GlobalConfiguration.Application.SetDefaultCollectionAgeLimit(TimeSpan ageLimit)</pre>
</div>
<p>对于单独的grain类型，限制可以通过以下方式设置：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">void</span> GlobalConfiguration.Application.SetCollectionAgeLimit(Type type, TimeSpan ageLimit)</pre>
</div>
<p>该限制也可以为grain类型重置，所以默认限制将适用于它，通过：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">void</span> GlobalConfiguration.Application.ResetCollectionAgeLimitToDefault(Type type)</pre>
</div>
<p>②XML配置（不建议使用）</p>
<p>配置XML文件中的任何时间长度都可以使用指定时间单位的后缀：</p>
<table class="table table-bordered table-striped table-condensed" style="height: 132px; width: 598px;">
<thead>
<tr><th>后缀</th><th>单位</th></tr>
</thead>
<tbody>
<tr>
<td>none</td>
<td>millisecond(s)</td>
</tr>
<tr>
<td>ms</td>
<td>millisecond(s)</td>
</tr>
<tr>
<td>s</td>
<td>second(s)</td>
</tr>
<tr>
<td>m</td>
<td>minute(s)</td>
</tr>
<tr>
<td>hr</td>
<td>hour(s)</td>
</tr>
</tbody>
</table>
<p>指定默认收集年龄限制</p>
<p>通过将OrleansConfiguation / Globals / Application / Defaults / Deactivation元素添加到OrleansConfiguration.xml文件，可以自定义适用于所有grain类型的默认集合期限。 允许的最低年龄限制是1分钟。</p>
<p>以下示例指定已空闲10分钟或更长时间的所有激活应被视为取消激活的条件。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;?</span><span style="color: #ff00ff;">xml version="1.0" encoding="utf-8"</span><span style="color: #0000ff;">?&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">OrleansConfiguration </span><span style="color: #ff0000;">xmlns</span><span style="color: #0000ff;">="urn:orleans"</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Globals</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Application</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Defaults</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Deactivation </span><span style="color: #ff0000;">AgeLimit</span><span style="color: #0000ff;">="10m"</span><span style="color: #0000ff;">/&gt;</span>
      <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Defaults</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Application</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Globals</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">OrleansConfiguration</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>指定每个类型的年龄限制</p>
<p>单个grain类型可以使用OrleansConfiguation / Globals / Application / GrainType / Deactivation元素来指定独立于全局默认的集合年龄限制。 允许的最低年龄限制是1分钟。</p>
<p>在以下示例中，空闲10分钟的激活有资格进行收集，除MyGrainAssembly.DoNotDeactivateMeOften类实例化的激活之外，除非空闲整整24小时，否则不被视为可收集：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;?</span><span style="color: #ff00ff;">xml version="1.0" encoding="utf-8"</span><span style="color: #0000ff;">?&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">OrleansConfiguration </span><span style="color: #ff0000;">xmlns</span><span style="color: #0000ff;">="urn:orleans"</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Globals</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Application</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Defaults</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Deactivation </span><span style="color: #ff0000;">AgeLimit</span><span style="color: #0000ff;">="10m"</span><span style="color: #0000ff;">/&gt;</span>
      <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Defaults</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">GrainType </span><span style="color: #ff0000;">Type</span><span style="color: #0000ff;">="MyGrainAssembly.DoNotDeactivateMeOften"</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Deactivation </span><span style="color: #ff0000;">AgeLimit</span><span style="color: #0000ff;">="24hr"</span><span style="color: #0000ff;">/&gt;</span>
      <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">GrainType</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Application</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Globals</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">OrleansConfiguration</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a4"></a>四、外部任务和Grains</span></strong></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a5"></a>五、序列化</span></strong></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a6"></a>六、代码生成</span></strong></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a7"></a>七、在Silo内的应用程序引导</span></strong></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a8"></a>八、拦截器</span></strong></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a9"></a>九、取消令牌</span></strong></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a10"></a>十、Powershell客户端</span></strong></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a11"></a>十一、Grains版本控制</span></strong></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a12"></a>十二、Event Sourcing</span></strong></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a13"></a>十三、多群集支持</span></strong></p>
<p>&nbsp;</p>