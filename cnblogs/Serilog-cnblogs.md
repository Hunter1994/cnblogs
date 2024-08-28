<p>1，引用包</p>
<div class="cnblogs_code">
<pre>    &lt;PackageReference Include=<span style="color: #800000;">"</span><span style="color: #800000;">Serilog.Extensions.Hosting</span><span style="color: #800000;">"</span> Version=<span style="color: #800000;">"</span><span style="color: #800000;">3.1.0</span><span style="color: #800000;">"</span> /&gt;
    &lt;PackageReference Include=<span style="color: #800000;">"</span><span style="color: #800000;">Serilog.Sinks.Async</span><span style="color: #800000;">"</span> Version=<span style="color: #800000;">"</span><span style="color: #800000;">1.4.0</span><span style="color: #800000;">"</span> /&gt;
    &lt;PackageReference Include=<span style="color: #800000;">"</span><span style="color: #800000;">Serilog.Sinks.Console</span><span style="color: #800000;">"</span> Version=<span style="color: #800000;">"</span><span style="color: #800000;">3.1.0</span><span style="color: #800000;">"</span> /&gt;
    &lt;PackageReference Include=<span style="color: #800000;">"</span><span style="color: #800000;">Serilog.Sinks.File</span><span style="color: #800000;">"</span> Version=<span style="color: #800000;">"</span><span style="color: #800000;">4.1.0</span><span style="color: #800000;">"</span> /&gt;</pre>
</div>
<p>2，初始化</p>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">async</span> Task Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            Log.Logger </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> LoggerConfiguration()
            .MinimumLevel.Information()
            .MinimumLevel.Override(</span><span style="color: #800000;">"</span><span style="color: #800000;">ProjectService</span><span style="color: #800000;">"</span>, LogEventLevel.Error)<span style="color: #008000;">//</span><span style="color: #008000;">当前log类型的输出等级为error</span>
            .Enrich.With(<span style="color: #0000ff;">new</span> ThreadIdEnrichar())<span style="color: #008000;">//</span><span style="color: #008000;">新增ThreadId字段</span>
<span style="color: #000000;">            .Enrich.FromLogContext()
            .WriteTo.Console(outputTemplate: </span><span style="color: #800000;">"</span><span style="color: #800000;">[{Timestamp:HH:mm:ss} {Level:u3} {ThreadId}] {Message}{NewLine}{Exception}</span><span style="color: #800000;">"</span>)<span style="color: #008000;">//</span><span style="color: #008000;">设置格式
            </span><span style="color: #008000;">//</span><span style="color: #008000;">.WriteTo.Async(c =&gt; c.File("Log\\logs.txt", rollingInterval: RollingInterval))</span>
            .WriteTo.File(<span style="color: #800000;">"</span><span style="color: #800000;">logs\\myapp.txt</span><span style="color: #800000;">"</span>, rollingInterval: RollingInterval.Day, outputTemplate: <span style="color: #800000;">"</span><span style="color: #800000;">[{Timestamp:HH:mm:ss} {Level:u3} {ThreadId}] {Message}{NewLine}{Exception}</span><span style="color: #800000;">"</span><span style="color: #000000;">)
            .CreateLogger();

            </span><span style="color: #0000ff;">string</span>[] s = <span style="color: #0000ff;">new</span> <span style="color: #0000ff;">string</span>[] { <span style="color: #800000;">"</span><span style="color: #800000;">1</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">2</span><span style="color: #800000;">"</span><span style="color: #000000;"> };
            Log.Information(</span><span style="color: #800000;">"</span><span style="color: #800000;">{@s}</span><span style="color: #800000;">"</span><span style="color: #000000;">, s);

            </span><span style="color: #0000ff;">await</span><span style="color: #000000;"> CreateHostBuilder(args).RunConsoleAsync();
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">Hello World!</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }</span></pre>
</div>
<div>ThreadIdEnrichar</div>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> Serilog.Core;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Serilog.Events;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading;

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ThreadIdEnrichar : ILogEventEnricher
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Enrich(LogEvent logEvent, ILogEventPropertyFactory propertyFactory)
    {
        logEvent.AddPropertyIfAbsent(propertyFactory.CreateProperty(</span><span style="color: #800000;">"</span><span style="color: #800000;">ThreadId</span><span style="color: #800000;">"</span><span style="color: #000000;">, Thread.CurrentThread.ManagedThreadId));
    }
}</span></pre>
</div>
<p>&nbsp;</p>