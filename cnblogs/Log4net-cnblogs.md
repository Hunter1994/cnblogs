<p>参考文档：<a href="http://www.cnblogs.com/LiZhiW/p/4317198.html" target="_blank">http://www.cnblogs.com/LiZhiW/p/4317198.html</a></p>
<p style="background-color: #169fe6;"><span style="color: #ffffff; font-size: 18pt;"><strong>一、关联配置文件</strong></span></p>
<p><strong>1，三种配置方式的方式</strong></p>
<p>①&nbsp;&nbsp;&nbsp; 默认web.config/app.config</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">监视默认的配置文件，App.exe.config </span>
<span style="color: #000000;">
[assembly: log4net.Config.XmlConfigurator(Watch </span>= <span style="color: #0000ff;">true</span>)]</pre>
</div>
<p>②&nbsp;&nbsp;&nbsp; 独立配置文件(&lt;项目名称&gt;.exe. log4net)(例如ConsoleApplication1.exe.log4net)</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">配置文件：App.exe.log4net</span>
<span style="color: #000000;">
[assembly:log4net.Config.XmlConfigurator(ConfigFileExtension</span>= <span style="color: #800000;">"</span><span style="color: #800000;">log4net</span><span style="color: #800000;">"</span>)]</pre>
</div>
<p>③&nbsp;&nbsp;&nbsp; 独立配置文件log4net.config</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">配置文件：log4net.config</span>
<span style="color: #000000;">
[assembly:log4net.Config.XmlConfigurator(ConfigFile</span>= <span style="color: #800000;">"</span><span style="color: #800000;">log4net.config</span><span style="color: #800000;">"</span>)]</pre>
</div>
<p>也可以在Global.asax的Application_Start里或者是Program.cs中的Main方法中添加，注意这里一定是绝对路径，如下所示：<br />
&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;log4net.Config.XmlConfigurator.Configure(new&nbsp;FileInfo(@"F:/log4net.config"));</p>
<p>&nbsp;</p>
<p><strong>2，</strong><strong>log4net.Config.XmlConifguratorAttribute</strong></p>
<p>ConfigFile：配置文件的名字，文件路径相对于应用程序目录</p>
<p>ConfigFileExtension：配置文件的扩展名，文件路径相对于应用程序的目录，不能和ConfigFile属性一起使用</p>
<p>Watch：如果将Watch属性设置为true，就会监视配置文件，当配置文件发生变化的时候，就会重新加载</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">二、案例</span></strong></span></p>
<p><strong><span style="font-size: 18px;">1，输出到文本</span></strong></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('0b1d5975-50b6-40a6-8638-65b700818b52')"><img id="code_img_closed_0b1d5975-50b6-40a6-8638-65b700818b52" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_0b1d5975-50b6-40a6-8638-65b700818b52" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('0b1d5975-50b6-40a6-8638-65b700818b52',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_0b1d5975-50b6-40a6-8638-65b700818b52" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">&lt;?</span><span style="color: #ff00ff;">xml version="1.0" encoding="utf-8" </span><span style="color: #0000ff;">?&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">configuration</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">configSections</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">section </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="log4net"</span><span style="color: #ff0000;"> type</span><span style="color: #0000ff;">="log4net.Config.Log4NetConfigurationSectionHandler, log4net"</span><span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">configSections</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">log4net</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">appender </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="AdoNetAppender_file"</span><span style="color: #ff0000;"> type</span><span style="color: #0000ff;">="log4net.Appender.RollingFileAppender"</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #008000;">&lt;!--</span><span style="color: #008000;">日志文件路径,按文件大小方式输出时在这里指定文件名，并且前面的日志按天在文件名后自动添加当天日期形成文件</span><span style="color: #008000;">--&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">param </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">= "File"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">= "D:\App_Log\Debug\"</span><span style="color: #0000ff;">/&gt;</span>
      <span style="color: #008000;">&lt;!--</span><span style="color: #008000;">是否是向文件中追加日志</span><span style="color: #008000;">--&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">param </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">= "AppendToFile"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">= "true"</span><span style="color: #0000ff;">/&gt;</span>
      <span style="color: #008000;">&lt;!--</span><span style="color: #008000;">记录日志写入文件时，不锁定文本文件</span><span style="color: #008000;">--&gt;</span>
      <span style="color: #008000;">&lt;!--</span><span style="color: #008000;">&lt;lockingModel type="log4net.Appender.FileAppender+MinimalLock" /&gt;</span><span style="color: #008000;">--&gt;</span>
      <span style="color: #008000;">&lt;!--</span><span style="color: #008000;">Unicode编码</span><span style="color: #008000;">--&gt;</span>
      <span style="color: #008000;">&lt;!--</span><span style="color: #008000;">&lt;Encoding value="UTF-8" /&gt;</span><span style="color: #008000;">--&gt;</span>
      <span style="color: #008000;">&lt;!--</span><span style="color: #008000;">最多产生的日志文件数，value="－1"为不限文件数</span><span style="color: #008000;">--&gt;</span>
      <span style="color: #008000;">&lt;!--</span><span style="color: #008000;">&lt;param name="MaxSizeRollBackups" value="100" /&gt;</span><span style="color: #008000;">--&gt;</span>
      <span style="color: #008000;">&lt;!--</span><span style="color: #008000;">log保留天数</span><span style="color: #008000;">--&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">param </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">= "MaxSizeRollBackups"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">= "30"</span><span style="color: #0000ff;">/&gt;</span>
      <span style="color: #008000;">&lt;!--</span><span style="color: #008000;">日志文件名是否是固定不变的（是否只写到一个文件中）</span><span style="color: #008000;">--&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">param </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">= "StaticLogFileName"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">= "false"</span><span style="color: #0000ff;">/&gt;</span>
      <span style="color: #008000;">&lt;!--</span><span style="color: #008000;">按照何种方式产生多个日志文件(日期[Date],文件大小[Size],混合[Composite])</span><span style="color: #008000;">--&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">param </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="RollingStyle"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">="Date"</span> <span style="color: #0000ff;">/&gt;</span>
      <span style="color: #008000;">&lt;!--</span><span style="color: #008000;">按日期产生文件夹，文件名［在日期方式与混合方式下使用］日志文件名格式为:2008-08-31.log </span><span style="color: #008000;">--&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">param </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">= "DatePattern"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">= "yyyy-MM-dd&amp;quot;.log&amp;quot;"</span><span style="color: #0000ff;">/&gt;</span>
      <span style="color: #008000;">&lt;!--</span><span style="color: #008000;">&lt;param name= "DatePattern" value= "yyyy-MM/yyyy-MM-dd&amp;quot;.log&amp;quot;"/&gt;</span><span style="color: #008000;">--&gt;</span>
      <span style="color: #008000;">&lt;!--</span><span style="color: #008000;">每个文件的大小。只在[混合方式与文件大小方式]下使用，超出大小的在文件名后自动增加1重新命名</span><span style="color: #008000;">--&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">param </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="maximumFileSize"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">="500KB"</span> <span style="color: #0000ff;">/&gt;</span>
      <span style="color: #008000;">&lt;!--</span><span style="color: #008000;">记录的格式。</span><span style="color: #008000;">--&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">layout </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="log4net.Layout.PatternLayout"</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #008000;">&lt;!--</span><span style="color: #008000;">
        %d, %date     ：表示当然的时间
　　    %p, %level    ：表示日志的级别
　　    %c, %logger   ：表示日志产生的主题或名称，通常是所在的类名，便于定位问题
　　    %m, %message  ：表示日志的具体内容
　　    %n, %newline  ：换行
        %exception    ：表示异常信息
        </span><span style="color: #008000;">--&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">param </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="ConversionPattern"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">="%d [%t] %-5p %c - %m %logger %exception %n"</span> <span style="color: #0000ff;">/&gt;</span>
      <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">layout</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">appender</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">logger </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="Test"</span><span style="color: #ff0000;"> additivity</span><span style="color: #0000ff;">="true"</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">level </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="ALL"</span><span style="color: #0000ff;">/&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">appender-ref </span><span style="color: #ff0000;">ref</span><span style="color: #0000ff;">="AdoNetAppender_file"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">logger</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">log4net</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">configuration</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<span class="cnblogs_code_collapse">log4net.config</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('6f2d4443-a6a0-4266-8df3-8bde1eb74839')"><img id="code_img_closed_6f2d4443-a6a0-4266-8df3-8bde1eb74839" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_6f2d4443-a6a0-4266-8df3-8bde1eb74839" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('6f2d4443-a6a0-4266-8df3-8bde1eb74839',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_6f2d4443-a6a0-4266-8df3-8bde1eb74839" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> log4net;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> LogDemo
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            ILog log </span>= log4net.LogManager.GetLogger(<span style="color: #800000;">"</span><span style="color: #800000;">Test</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            log.Error(</span><span style="color: #800000;">"</span><span style="color: #800000;">错误</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span> Exception(<span style="color: #800000;">"</span><span style="color: #800000;">发生了一个异常</span><span style="color: #800000;">"</span>));<span style="color: #008000;">//</span><span style="color: #008000;">错误</span>
            log.Fatal(<span style="color: #800000;">"</span><span style="color: #800000;">严重错误</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span> Exception(<span style="color: #800000;">"</span><span style="color: #800000;">发生了一个致命错误</span><span style="color: #800000;">"</span>));<span style="color: #008000;">//</span><span style="color: #008000;">严重错误</span>
            log.Info(<span style="color: #800000;">"</span><span style="color: #800000;">信息</span><span style="color: #800000;">"</span>); <span style="color: #008000;">//</span><span style="color: #008000;">记录一般信息</span>
            log.Debug(<span style="color: #800000;">"</span><span style="color: #800000;">调试信息</span><span style="color: #800000;">"</span>);<span style="color: #008000;">//</span><span style="color: #008000;">记录调试信息</span>
            log.Warn(<span style="color: #800000;">"</span><span style="color: #800000;">警告</span><span style="color: #800000;">"</span>);<span style="color: #008000;">//</span><span style="color: #008000;">记录警告信息</span>
<span style="color: #000000;">
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">日志记录完毕。</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            Console.Read();
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Program.cs</span></div>
<p>案例下载：<a href="http://pan.baidu.com/s/1nuU4f93" target="_blank">http://pan.baidu.com/s/1nuU4f93</a></p>
<p>&lt;param name= "File" value= "log\"/&gt;文件配置格式&nbsp;</p>
<p>&nbsp;</p>
<p><strong><span style="font-size: 18px;">2，输出到数据库</span></strong></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('e143c97a-a3b1-4e4f-a766-755ede0b1e5a')"><img id="code_img_closed_e143c97a-a3b1-4e4f-a766-755ede0b1e5a" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_e143c97a-a3b1-4e4f-a766-755ede0b1e5a" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('e143c97a-a3b1-4e4f-a766-755ede0b1e5a',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_e143c97a-a3b1-4e4f-a766-755ede0b1e5a" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">&lt;?</span><span style="color: #ff00ff;">xml version="1.0" encoding="utf-8" </span><span style="color: #0000ff;">?&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">configuration</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">configSections</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">section </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="log4net"</span><span style="color: #ff0000;"> type</span><span style="color: #0000ff;">="log4net.Config.Log4NetConfigurationSectionHandler, log4net"</span><span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">configSections</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">log4net</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">appender </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="AdoNetAppender_mysql"</span><span style="color: #ff0000;"> type</span><span style="color: #0000ff;">="log4net.Appender.AdoNetAppender"</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">bufferSize </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="0"</span> <span style="color: #0000ff;">/&gt;</span><span style="color: #008000;">&lt;!--</span><span style="color: #008000;">0:只要有一条就立刻写到数据库。4:第5条时写入数据库</span><span style="color: #008000;">--&gt;</span>
      <span style="color: #008000;">&lt;!--</span><span style="color: #008000;">日志数据库连接串mysql</span><span style="color: #008000;">--&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">connectionType </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="MySql.Data.MySqlClient.MySqlConnection, MySql.Data"</span> <span style="color: #0000ff;">/&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">connectionString </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="server=localhost;user id=root;pwd=123456;port=3306;pooling=True;database=xinleda"</span><span style="color: #ff0000;"> providerName</span><span style="color: #0000ff;">="MySql.Data.MySqlClient;"</span> <span style="color: #0000ff;">/&gt;</span>
      <span style="color: #008000;">&lt;!--</span><span style="color: #008000;">日志数据库脚本(注意：mysql不需要[]符号)</span><span style="color: #008000;">--&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">commandText </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="INSERT INTO LogDetails(LogDate,Thread,Level,Logger,Message) VALUES (@logDate, @thread, @logLevel, @logger,@message)"</span> <span style="color: #0000ff;">/&gt;</span>
      <span style="color: #008000;">&lt;!--</span><span style="color: #008000;">参数</span><span style="color: #008000;">--&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">parameter</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">parameterName </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="@logDate"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">dbType </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="Datetime"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">layout </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="log4net.Layout.RawTimeStampLayout"</span> <span style="color: #0000ff;">/&gt;</span>
      <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">parameter</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">parameter</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">parameterName </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="@thread"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">layout </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="log4net.Layout.PatternLayout"</span><span style="color: #0000ff;">&gt;</span>
          <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">conversionPattern </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="%thread"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">layout</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">parameter</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">parameter</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">parameterName </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="@logLevel"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">dbType </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="String"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">layout </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="log4net.Layout.PatternLayout"</span><span style="color: #0000ff;">&gt;</span>
          <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">conversionPattern </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="%level"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">layout</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">parameter</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">parameter</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">parameterName </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="@logger"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">dbType </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="String"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">size </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="240"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">layout </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="log4net.Layout.PatternLayout"</span><span style="color: #0000ff;">&gt;</span>
          <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">conversionPattern </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="%logger"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">layout</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">parameter</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">parameter</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">parameterName </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="@message"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">dbType </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="String"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">size </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="240"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">layout </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="log4net.Layout.PatternLayout"</span><span style="color: #0000ff;">&gt;</span>
          <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">conversionPattern </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="%message"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">layout</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">parameter</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">appender</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">logger </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="Test"</span><span style="color: #ff0000;"> additivity</span><span style="color: #0000ff;">="true"</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">level </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="ALL"</span><span style="color: #0000ff;">/&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">appender-ref </span><span style="color: #ff0000;">ref</span><span style="color: #0000ff;">="AdoNetAppender_mysql"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">logger</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">log4net</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">configuration</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<span class="cnblogs_code_collapse">log4net.config</span></div>
<p>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('96e9594d-af3c-494e-9eff-f4b2114cf704')"><img id="code_img_closed_96e9594d-af3c-494e-9eff-f4b2114cf704" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_96e9594d-af3c-494e-9eff-f4b2114cf704" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('96e9594d-af3c-494e-9eff-f4b2114cf704',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_96e9594d-af3c-494e-9eff-f4b2114cf704" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> log4net;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> log4net.Config;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.IO;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> LogDemo
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            ILog log </span>= log4net.LogManager.GetLogger(<span style="color: #800000;">"</span><span style="color: #800000;">Test</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            log.Error(</span><span style="color: #800000;">"</span><span style="color: #800000;">错误</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span> Exception(<span style="color: #800000;">"</span><span style="color: #800000;">发生了一个异常</span><span style="color: #800000;">"</span>));<span style="color: #008000;">//</span><span style="color: #008000;">错误</span>
            log.Fatal(<span style="color: #800000;">"</span><span style="color: #800000;">严重错误</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span> Exception(<span style="color: #800000;">"</span><span style="color: #800000;">发生了一个致命错误</span><span style="color: #800000;">"</span>));<span style="color: #008000;">//</span><span style="color: #008000;">严重错误</span>
            log.Info(<span style="color: #800000;">"</span><span style="color: #800000;">信息</span><span style="color: #800000;">"</span>); <span style="color: #008000;">//</span><span style="color: #008000;">记录一般信息</span>
            log.Debug(<span style="color: #800000;">"</span><span style="color: #800000;">调试信息</span><span style="color: #800000;">"</span>);<span style="color: #008000;">//</span><span style="color: #008000;">记录调试信息</span>
            log.Warn(<span style="color: #800000;">"</span><span style="color: #800000;">警告</span><span style="color: #800000;">"</span>);<span style="color: #008000;">//</span><span style="color: #008000;">记录警告信息</span>
            Console.WriteLine(<span style="color: #800000;">"</span><span style="color: #800000;">日志记录完毕。</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            Console.Read();
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Program.cs</span></div>
<p>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('dd5615e6-5a7f-434a-b696-7e8c8d845a47')"><img id="code_img_closed_dd5615e6-5a7f-434a-b696-7e8c8d845a47" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_dd5615e6-5a7f-434a-b696-7e8c8d845a47" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('dd5615e6-5a7f-434a-b696-7e8c8d845a47',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_dd5615e6-5a7f-434a-b696-7e8c8d845a47" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Reflection;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Runtime.CompilerServices;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Runtime.InteropServices;

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 有关程序集的一般信息由以下
</span><span style="color: #008000;">//</span><span style="color: #008000;"> 控制。更改这些特性值可修改
</span><span style="color: #008000;">//</span><span style="color: #008000;"> 与程序集关联的信息。</span>
[assembly: AssemblyTitle(<span style="color: #800000;">"</span><span style="color: #800000;">LogDemo</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
[assembly: AssemblyDescription(</span><span style="color: #800000;">""</span><span style="color: #000000;">)]
[assembly: AssemblyConfiguration(</span><span style="color: #800000;">""</span><span style="color: #000000;">)]
[assembly: AssemblyCompany(</span><span style="color: #800000;">""</span><span style="color: #000000;">)]
[assembly: AssemblyProduct(</span><span style="color: #800000;">"</span><span style="color: #800000;">LogDemo</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
[assembly: AssemblyCopyright(</span><span style="color: #800000;">"</span><span style="color: #800000;">Copyright &copy;  2017</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
[assembly: AssemblyTrademark(</span><span style="color: #800000;">""</span><span style="color: #000000;">)]
[assembly: AssemblyCulture(</span><span style="color: #800000;">""</span><span style="color: #000000;">)]

</span><span style="color: #008000;">//</span><span style="color: #008000;">将 ComVisible 设置为 false 将使此程序集中的类型
</span><span style="color: #008000;">//</span><span style="color: #008000;">对 COM 组件不可见。  如果需要从 COM 访问此程序集中的类型，
</span><span style="color: #008000;">//</span><span style="color: #008000;">请将此类型的 ComVisible 特性设置为 true。</span>
[assembly: ComVisible(<span style="color: #0000ff;">false</span><span style="color: #000000;">)]

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 如果此项目向 COM 公开，则下列 GUID 用于类型库的 ID</span>
[assembly: Guid(<span style="color: #800000;">"</span><span style="color: #800000;">3cef5427-d026-46c8-a73a-083215681098</span><span style="color: #800000;">"</span><span style="color: #000000;">)]

[assembly: log4net.Config.XmlConfigurator(ConfigFile </span>= <span style="color: #800000;">"</span><span style="color: #800000;">log4net.config</span><span style="color: #800000;">"</span><span style="color: #000000;">)]

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 程序集的版本信息由下列四个值组成:
</span><span style="color: #008000;">//</span>
<span style="color: #008000;">//</span><span style="color: #008000;">      主版本
</span><span style="color: #008000;">//</span><span style="color: #008000;">      次版本
</span><span style="color: #008000;">//</span><span style="color: #008000;">      生成号
</span><span style="color: #008000;">//</span><span style="color: #008000;">      修订号
</span><span style="color: #008000;">//</span>
<span style="color: #008000;">//</span><span style="color: #008000;">可以指定所有这些值，也可以使用&ldquo;生成号&rdquo;和&ldquo;修订号&rdquo;的默认值，
</span><span style="color: #008000;">//</span><span style="color: #008000;"> 方法是按如下所示使用&ldquo;*&rdquo;: :
</span><span style="color: #008000;">//</span><span style="color: #008000;"> [assembly: AssemblyVersion("1.0.*")]</span>
[assembly: AssemblyVersion(<span style="color: #800000;">"</span><span style="color: #800000;">1.0.0.0</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
[assembly: AssemblyFileVersion(</span><span style="color: #800000;">"</span><span style="color: #800000;">1.0.0.0</span><span style="color: #800000;">"</span>)]</pre>
</div>
<span class="cnblogs_code_collapse">AssemblyInfo.cs</span></div>
<p><span style="color: #ff0000;">注意:如果是链接到mysql需要引用组件MySql.Data</span></p>
<p>案例下载：<a href="http://pan.baidu.com/s/1c1QIF0s" target="_blank">http://pan.baidu.com/s/1c1QIF0s</a></p>
<p>&nbsp;</p>
<p><strong><span style="font-size: 18px;">3，自定义字段输出到数据库</span></strong></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('851f572e-019e-489c-8506-43de5c506eda')"><img id="code_img_closed_851f572e-019e-489c-8506-43de5c506eda" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_851f572e-019e-489c-8506-43de5c506eda" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('851f572e-019e-489c-8506-43de5c506eda',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_851f572e-019e-489c-8506-43de5c506eda" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">&lt;?</span><span style="color: #ff00ff;">xml version="1.0" encoding="utf-8" </span><span style="color: #0000ff;">?&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">configuration</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">configSections</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">section </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="log4net"</span><span style="color: #ff0000;"> type</span><span style="color: #0000ff;">="log4net.Config.Log4NetConfigurationSectionHandler, log4net"</span><span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">configSections</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">log4net</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">appender </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="AdoNetAppender_mysql"</span><span style="color: #ff0000;"> type</span><span style="color: #0000ff;">="log4net.Appender.AdoNetAppender"</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">bufferSize </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="0"</span> <span style="color: #0000ff;">/&gt;</span><span style="color: #008000;">&lt;!--</span><span style="color: #008000;">0:只要有一条就立刻写到数据库。4:第5条时写入数据库</span><span style="color: #008000;">--&gt;</span>
      <span style="color: #008000;">&lt;!--</span><span style="color: #008000;">日志数据库连接串mysql</span><span style="color: #008000;">--&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">connectionType </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="MySql.Data.MySqlClient.MySqlConnection, MySql.Data"</span> <span style="color: #0000ff;">/&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">connectionString </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="server=localhost;user id=root;pwd=123456;port=3306;pooling=True;database=xinleda"</span><span style="color: #ff0000;"> providerName</span><span style="color: #0000ff;">="MySql.Data.MySqlClient;"</span> <span style="color: #0000ff;">/&gt;</span>
      <span style="color: #008000;">&lt;!--</span><span style="color: #008000;">日志数据库脚本(注意：mysql不需要[]符号)</span><span style="color: #008000;">--&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">commandText </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="INSERT INTO LogDetails(LogDate,Thread,Level,Logger,Message,Content,Age) VALUES (@logDate, @thread, @logLevel, @logger,@message,@Content,@Age)"</span> <span style="color: #0000ff;">/&gt;</span>
      <span style="color: #008000;">&lt;!--</span><span style="color: #008000;">参数</span><span style="color: #008000;">--&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">parameter</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">parameterName </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="@logDate"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">dbType </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="Datetime"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">layout </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="log4net.Layout.RawTimeStampLayout"</span> <span style="color: #0000ff;">/&gt;</span>
      <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">parameter</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">parameter</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">parameterName </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="@thread"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">layout </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="log4net.Layout.PatternLayout"</span><span style="color: #0000ff;">&gt;</span>
          <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">conversionPattern </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="%thread"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">layout</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">parameter</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">parameter</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">parameterName </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="@logLevel"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">dbType </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="String"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">layout </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="log4net.Layout.PatternLayout"</span><span style="color: #0000ff;">&gt;</span>
          <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">conversionPattern </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="%level"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">layout</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">parameter</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">parameter</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">parameterName </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="@logger"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">dbType </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="String"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">size </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="240"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">layout </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="log4net.Layout.PatternLayout"</span><span style="color: #0000ff;">&gt;</span>
          <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">conversionPattern </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="%logger"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">layout</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">parameter</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">parameter</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">parameterName </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="@message"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">dbType </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="String"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">size </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="240"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">layout </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="log4net.Layout.PatternLayout"</span><span style="color: #0000ff;">&gt;</span>
          <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">conversionPattern </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="%message"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">layout</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">parameter</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">parameter</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">parameterName </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="@Content"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">dbType </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="String"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">size </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="240"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">layout </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="LogDemo.MessageLayout"</span><span style="color: #0000ff;">&gt;</span>
          <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">conversionPattern </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="%Content"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">layout</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">parameter</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">parameter</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">parameterName </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="@Age"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">layout </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="LogDemo.MessageLayout"</span><span style="color: #0000ff;">&gt;</span>
          <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">conversionPattern </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="%Age"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">layout</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">parameter</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">appender</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">logger </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="Test"</span><span style="color: #ff0000;"> additivity</span><span style="color: #0000ff;">="true"</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">level </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="ALL"</span><span style="color: #0000ff;">/&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">appender-ref </span><span style="color: #ff0000;">ref</span><span style="color: #0000ff;">="AdoNetAppender_mysql"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">logger</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">log4net</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">configuration</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<span class="cnblogs_code_collapse">log4net.config</span></div>
<p>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('36b659b1-a7fc-4143-9bb3-3ce8851f136f')"><img id="code_img_closed_36b659b1-a7fc-4143-9bb3-3ce8851f136f" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_36b659b1-a7fc-4143-9bb3-3ce8851f136f" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('36b659b1-a7fc-4143-9bb3-3ce8851f136f',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_36b659b1-a7fc-4143-9bb3-3ce8851f136f" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> log4net.Layout.Pattern;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> log4net.Core;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.IO;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> log4net.Layout;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> LogDemo
{
    </span><span style="color: #008000;">//</span><span style="color: #008000;">自定义字段</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> LogMassage
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Content { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span> Age { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
        </span><span style="color: #0000ff;">public</span> DateTime Dt { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">sealed</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ContentPatternConverter : PatternLayoutConverter
    {
        </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Convert(TextWriter writer, LoggingEvent loggingEvent)
        {
            </span><span style="color: #0000ff;">var</span> log =loggingEvent.MessageObject <span style="color: #0000ff;">as</span><span style="color: #000000;"> LogMassage;
            </span><span style="color: #0000ff;">if</span> (log != <span style="color: #0000ff;">null</span><span style="color: #000000;">)
            {
                writer.Write(log.Content);
            }
        }
    }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">sealed</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> AgePatternConverter : PatternLayoutConverter
    {
        </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Convert(TextWriter writer, LoggingEvent loggingEvent)
        {
            </span><span style="color: #0000ff;">var</span> log = loggingEvent.MessageObject <span style="color: #0000ff;">as</span><span style="color: #000000;"> LogMassage;
            </span><span style="color: #0000ff;">if</span> (log != <span style="color: #0000ff;">null</span><span style="color: #000000;">)
            {
                writer.Write(log.Age);
            }
        }
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MessageLayout : PatternLayout
    {
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> MessageLayout()
        {
            </span><span style="color: #0000ff;">this</span>.AddConverter(<span style="color: #800000;">"</span><span style="color: #800000;">Content</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">typeof</span><span style="color: #000000;">(ContentPatternConverter));
            </span><span style="color: #0000ff;">this</span>.AddConverter(<span style="color: #800000;">"</span><span style="color: #800000;">Age</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">typeof</span><span style="color: #000000;">(AgePatternConverter));
        }
    }

}</span></pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<p>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('8ce93bcc-c803-49bb-a4c7-5b563c9b207f')"><img id="code_img_closed_8ce93bcc-c803-49bb-a4c7-5b563c9b207f" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_8ce93bcc-c803-49bb-a4c7-5b563c9b207f" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('8ce93bcc-c803-49bb-a4c7-5b563c9b207f',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_8ce93bcc-c803-49bb-a4c7-5b563c9b207f" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> log4net;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> log4net.Config;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.IO;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> LogDemo
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            ILog log </span>= log4net.LogManager.GetLogger(<span style="color: #800000;">"</span><span style="color: #800000;">Test</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            log.Error(</span><span style="color: #800000;">"</span><span style="color: #800000;">错误</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span> Exception(<span style="color: #800000;">"</span><span style="color: #800000;">发生了一个异常</span><span style="color: #800000;">"</span>));<span style="color: #008000;">//</span><span style="color: #008000;">错误</span>
            log.Fatal(<span style="color: #800000;">"</span><span style="color: #800000;">严重错误</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span> Exception(<span style="color: #800000;">"</span><span style="color: #800000;">发生了一个致命错误</span><span style="color: #800000;">"</span>));<span style="color: #008000;">//</span><span style="color: #008000;">严重错误</span>
            log.Info(<span style="color: #800000;">"</span><span style="color: #800000;">信息</span><span style="color: #800000;">"</span>); <span style="color: #008000;">//</span><span style="color: #008000;">记录一般信息</span>
            log.Debug(<span style="color: #800000;">"</span><span style="color: #800000;">调试信息</span><span style="color: #800000;">"</span>);<span style="color: #008000;">//</span><span style="color: #008000;">记录调试信息</span>
            log.Warn(<span style="color: #800000;">"</span><span style="color: #800000;">警告</span><span style="color: #800000;">"</span>);<span style="color: #008000;">//</span><span style="color: #008000;">记录警告信息

            </span><span style="color: #008000;">//</span><span style="color: #008000;">记录自定义字段</span>
            <span style="color: #0000ff;">var</span> m = <span style="color: #0000ff;">new</span><span style="color: #000000;"> LogMassage();
            m.Content </span>= <span style="color: #800000;">"</span><span style="color: #800000;">asdasd</span><span style="color: #800000;">"</span><span style="color: #000000;">;
            m.Age </span>= <span style="color: #800080;">123</span><span style="color: #000000;">;
            m.Dt </span>=<span style="color: #000000;"> DateTime.Now;
            log.Info(m);

            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">日志记录完毕。</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            Console.Read();
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Program.cs</span></div>
<p>案例下载：<a href="http://pan.baidu.com/s/1hrNSB8C" target="_blank">http://pan.baidu.com/s/1hrNSB8C</a></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="color: #ffffff; font-size: 18pt;">三、配置详情</span></strong></p>
<p><strong><span style="font-size: 18px;">&nbsp;1，logger节点配置详解</span></strong></p>
<div class="cnblogs_code">
<pre>    <span style="color: #008000;">&lt;!--</span><span style="color: #008000;">name:必须的，logger的名称，在代码中得到ILog对象时用到</span><span style="color: #008000;">--&gt;</span>
    <span style="color: #008000;">&lt;!--</span><span style="color: #008000;">additivity:可选，取值是true或false，默认值是true。设置为false时将阻止父logger中的appender</span><span style="color: #008000;">--&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">logger </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="Test"</span><span style="color: #ff0000;"> additivity</span><span style="color: #0000ff;">="true"</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">level </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="ALL"</span><span style="color: #0000ff;">/&gt;</span><span style="color: #008000;">&lt;!--</span><span style="color: #008000;">日志级别等级。高到底分别为：OFF &gt; FATAL &gt; ERROR &gt; WARN &gt; INFO &gt; DEBUG  &gt; ALL</span><span style="color: #008000;">--&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">appender-ref </span><span style="color: #ff0000;">ref</span><span style="color: #0000ff;">="AdoNetAppender_mysql"</span> <span style="color: #0000ff;">/&gt;</span><span style="color: #008000;">&lt;!--</span><span style="color: #008000;">0个或多个，要引用的appender的名字</span><span style="color: #008000;">--&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">logger</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p><strong><span style="font-size: 18px;">&nbsp;2，filter节点配置详解</span></strong></p>
<p><span style="color: #ff0000;">filter只能作为&lt;appender&gt;的子元素</span>，type属性表示Filter的类型</p>
<p>DenyAllFilter&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 阻止所有的日志事件被记录</p>
<p>LevelMatchFilter&nbsp;&nbsp;&nbsp; 只有指定等级的日志事件才被记录</p>
<p>LevelRangeFilter&nbsp;&nbsp;&nbsp; 日志等级在指定范围内的事件才被记录</p>
<p>①记录日志等级为&ldquo;FATAL&rdquo;和&ldquo;ERROR&rdquo;的日志信息</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">filter </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="log4net.Filter.LevelMatchFilter"</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">levelToMatch </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="FATAL"</span><span style="color: #0000ff;">/&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">filter</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">filter </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="log4net.Filter.LevelMatchFilter"</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">levelToMatch </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="ERROR"</span><span style="color: #0000ff;">/&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">filter</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">filter </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="log4net.Filter.DenyAllFilter"</span><span style="color: #0000ff;">/&gt;</span></pre>
</div>
<p>②记录日志等级范围从&ldquo;ERROR&rdquo;到&ldquo;INFO&rdquo;的日志信息：</p>
<div class="cnblogs_code">
<pre>      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">filter </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="log4net.Filter.LevelRangeFilter"</span><span style="color: #0000ff;">&gt;</span>
         <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">levelMax </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="ERROR"</span><span style="color: #0000ff;">/&gt;</span>
         <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">levelMin </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="INFO"</span><span style="color: #0000ff;">/&gt;</span>
      <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">filter</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p><strong><span style="font-size: 18px;">&nbsp;3，Layout节点配置详解</span></strong></p>
<p><span style="color: #ff0000;">layout节点只能作为&lt;appender&gt;的子元素</span>。type属性表示Layout的类型</p>
<p>①layout节点的type属性取值</p>
<div>
<table style="width: 884px; height: 275px;" border="1" cellspacing="0" cellpadding="0">
<tbody>
<tr style="height: 15px;">
<td valign="top" width="277">
<p>ExceptionLayout</p>
</td>
<td valign="top" width="277">
<p>只呈现日志事件中异常的文本信息</p>
</td>
</tr>
<tr style="height: 25px;">
<td valign="top" width="277">
<p>PatternLayout</p>
</td>
<td valign="top" width="277">
<p>可以通过类型字符串来配置的布局</p>
</td>
</tr>
<tr style="height: 25px;">
<td valign="top" width="277">
<p>RawPropertyLayout</p>
</td>
<td valign="top" width="277">
<p>从日志事件中提取属性值</p>
</td>
</tr>
<tr style="height: 25px;">
<td valign="top" width="277">
<p>RawTimeStampLayout</p>
</td>
<td valign="top" width="277">
<p>从日志事件中提取日期</p>
</td>
</tr>
<tr style="height: 25px;">
<td valign="top" width="277">
<p>RawUtcTimeStampLayout</p>
</td>
<td valign="top" width="277">
<p>从日志事件中提取UTC日期</p>
</td>
</tr>
<tr style="height: 25px;">
<td valign="top" width="277">
<p>SimpleLayout</p>
</td>
<td valign="top" width="277">
<p>很简单的布局</p>
</td>
</tr>
<tr style="height: 25px;">
<td valign="top" width="277">
<p>XmlLayout</p>
</td>
<td valign="top" width="277">
<p>把日志事件格式化为XML元素的布局</p>
</td>
</tr>
</tbody>
</table>
</div>
<div>②PatterLayout的格式化字符串</div>
<div>
<table style="width: 885px; height: 908px;" border="1" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td valign="top" width="277">
<p>%m、%message</p>
</td>
<td valign="top" width="277">
<p>输出的日志消息</p>
</td>
</tr>
<tr>
<td valign="top" width="277">
<p>%d、%datetime</p>
</td>
<td valign="top" width="277">
<p>输出当前语句运行的时刻，格式%date{yyyy-MM-dd &nbsp; HH:mm:ss,fff}</p>
</td>
</tr>
<tr>
<td valign="top" width="277">
<p>%r、%timestamp</p>
</td>
<td valign="top" width="277">
<p>输出程序从运行到执行到当前语句时消耗的毫秒数</p>
</td>
</tr>
<tr>
<td valign="top" width="277">
<p>%p、%level</p>
</td>
<td valign="top" width="277">
<p>日志的当前优先级别</p>
</td>
</tr>
<tr>
<td valign="top" width="277">
<p>%c、%logger</p>
</td>
<td valign="top" width="277">
<p>当前日志对象的名称</p>
</td>
</tr>
<tr>
<td valign="top" width="277">
<p>%L、%line</p>
</td>
<td valign="top" width="277">
<p>输出语句所在的行号</p>
</td>
</tr>
<tr>
<td valign="top" width="277">
<p>%F、%file</p>
</td>
<td valign="top" width="277">
<p>输出语句所在的文件名，警告：只在调试的时候有效，调用本地信息会影响性能</p>
</td>
</tr>
<tr>
<td valign="top" width="277">
<p>%a、%appdomain</p>
</td>
<td valign="top" width="277">
<p>引发日志事件的应用程序域的名称。</p>
</td>
</tr>
<tr>
<td valign="top" width="277">
<p>%C、%class、%type</p>
</td>
<td valign="top" width="277">
<p>引发日志请求的类的全名，警告：会影响性能</p>
</td>
</tr>
<tr>
<td valign="top" width="277">
<p>%exception</p>
</td>
<td valign="top" width="277">
<p>异常信息</p>
</td>
</tr>
<tr>
<td valign="top" width="277">
<p>%u、%identity</p>
</td>
<td valign="top" width="277">
<p>当前活动用户的名字，我测试的时候%identity返回都是空的。警告：会影响性能</p>
</td>
</tr>
<tr>
<td valign="top" width="277">
<p>%l、%location</p>
</td>
<td valign="top" width="277">
<p>引发日志事件的名空间、类名、方法、行号。警告：会影响性能，依赖pdb文件</p>
</td>
</tr>
<tr>
<td valign="top" width="277">
<p>%M、%method</p>
</td>
<td valign="top" width="277">
<p>发生日志请求的方法名，警告：会影响性能</p>
</td>
</tr>
<tr>
<td valign="top" width="277">
<p>%n、%newline</p>
</td>
<td valign="top" width="277">
<p>换行符</p>
</td>
</tr>
<tr>
<td valign="top" width="277">
<p>%x、%ndc</p>
</td>
<td valign="top" width="277">
<p>NDC(nested diagnostic context)</p>
</td>
</tr>
<tr>
<td valign="top" width="277">
<p>%X、%mdc、%P、%properties</p>
</td>
<td valign="top" width="277">
<p>等介于 %property</p>
</td>
</tr>
<tr>
<td valign="top" width="277">
<p>%property</p>
</td>
<td valign="top" width="277">
<p>输出{log4net:Identity=, log4net:UserName=, &nbsp; log4net:HostName=}</p>
</td>
</tr>
<tr>
<td valign="top" width="277">
<p>%t、%thread</p>
</td>
<td valign="top" width="277">
<p>引发日志事件的线程，如果没有线程名就使用线程号。</p>
</td>
</tr>
<tr>
<td valign="top" width="277">
<p>%w、%username</p>
</td>
<td valign="top" width="277">
<p>当前用户的WindowsIdentity,类似：HostName/Username。警告：会影响性能</p>
</td>
</tr>
<tr>
<td valign="top" width="277">
<p>%utcdate</p>
</td>
<td valign="top" width="277">
<p>发生日志事件的UTC时间。例如：%utcdate{HH:mm:ss,fff}</p>
</td>
</tr>
<tr>
<td valign="top" width="277">
<p>%%</p>
</td>
<td valign="top" width="277">
<p>输出一个百分号</p>
</td>
</tr>
</tbody>
</table>
</div>
<div>&nbsp;</div>
<div>③案例</div>
<div>&nbsp;
<div class="cnblogs_code">
<pre>      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">parameter</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">parameterName </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="@logDate"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">dbType </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="Datetime"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">layout </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="log4net.Layout.RawTimeStampLayout"</span> <span style="color: #0000ff;">/&gt;</span>
      <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">parameter</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<div class="cnblogs_code">
<pre>      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">parameter</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">parameterName </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="@thread"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">layout </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="log4net.Layout.PatternLayout"</span><span style="color: #0000ff;">&gt;</span>
          <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">conversionPattern </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="%thread"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">layout</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">parameter</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;</p>
</div>
<div>&nbsp;</div>
<div>&nbsp;</div>