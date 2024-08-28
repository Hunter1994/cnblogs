<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt;"><strong><span style="color: #ffffff;">一、使用IIS在Windows上进行托管</span></strong></span></p>
<p><strong>1，部署asp.net core</strong></p>
<p>①检查安装最新的SDK和运行时</p>
<p><a href="https://www.microsoft.com/net/download/windows#/runtime" target="_blank">https://www.microsoft.com/net/download/windows#/runtime</a></p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201806/741594-20180605153507373-1762291729.png" alt="" width="343" height="333" /></p>
<p>IIS需要跑asp.net core必须要安装Runtime</p>
<p>②执行&nbsp;<span class="cnblogs_code">dotnet publish</span>&nbsp;命令发布程序</p>
<p>③IIS添加网站</p>
<p>④设置程序池</p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201806/741594-20180605153734743-1330923730.png" alt="" width="213" height="215" /></p>
<p><strong>2， Asp.net Core 模块的配置</strong></p>
<p>①web.config的配置</p>
<p>以下&nbsp;<em>web.config</em>&nbsp;文件发布用于<a href="https://docs.microsoft.com/zh-cn/dotnet/articles/core/deploying/#framework-dependent-deployments-fdd" data-linktype="absolute-path">依赖框架的部署</a>，并配置 ASP.NET Core 模块以处理站点请求：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;?</span><span style="color: #ff00ff;">xml version="1.0" encoding="utf-8"</span><span style="color: #0000ff;">?&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">configuration</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">system.webServer</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">handlers</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">add </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="aspNetCore"</span><span style="color: #ff0000;"> path</span><span style="color: #0000ff;">="*"</span><span style="color: #ff0000;"> verb</span><span style="color: #0000ff;">="*"</span><span style="color: #ff0000;"> modules</span><span style="color: #0000ff;">="AspNetCoreModule"</span><span style="color: #ff0000;"> resourceType</span><span style="color: #0000ff;">="Unspecified"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">handlers</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">aspNetCore </span><span style="color: #ff0000;">processPath</span><span style="color: #0000ff;">="dotnet"</span><span style="color: #ff0000;"> 
                arguments</span><span style="color: #0000ff;">=".\MyApp.dll"</span><span style="color: #ff0000;"> 
                stdoutLogEnabled</span><span style="color: #0000ff;">="false"</span><span style="color: #ff0000;"> 
                stdoutLogFile</span><span style="color: #0000ff;">=".\logs\stdout"</span> <span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">system.webServer</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">configuration</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>以下 web.config 发布用于<a href="https://docs.microsoft.com/zh-cn/dotnet/articles/core/deploying/#self-contained-deployments-scd" data-linktype="absolute-path">独立部署</a>：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;?</span><span style="color: #ff00ff;">xml version="1.0" encoding="utf-8"</span><span style="color: #0000ff;">?&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">configuration</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">system.webServer</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">handlers</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">add </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="aspNetCore"</span><span style="color: #ff0000;"> path</span><span style="color: #0000ff;">="*"</span><span style="color: #ff0000;"> verb</span><span style="color: #0000ff;">="*"</span><span style="color: #ff0000;"> modules</span><span style="color: #0000ff;">="AspNetCoreModule"</span><span style="color: #ff0000;"> resourceType</span><span style="color: #0000ff;">="Unspecified"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">handlers</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">aspNetCore </span><span style="color: #ff0000;">processPath</span><span style="color: #0000ff;">=".\MyApp.exe"</span><span style="color: #ff0000;"> 
                stdoutLogEnabled</span><span style="color: #0000ff;">="false"</span><span style="color: #ff0000;"> 
                stdoutLogFile</span><span style="color: #0000ff;">=".\logs\stdout"</span> <span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">system.webServer</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">configuration</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>①<span data-ttu-id="863f8-114">aspNetCore 元素的属性</span></p>
<table border="1">
<thead>
<tr><th><span data-ttu-id="863f8-150">特性</span></th><th><span data-ttu-id="863f8-151">描述</span></th><th><span data-ttu-id="863f8-152">默认</span></th></tr>
</thead>
<tbody>
<tr>
<td><code>arguments</code></td>
<td>
<p><span data-ttu-id="863f8-153">可选的字符串属性。</span></p>
<p><span data-ttu-id="863f8-154">processPath 中指定的可执行文件的参数。</span></p>
</td>
<td>&nbsp;</td>
</tr>
<tr>
<td><code>disableStartUpErrorPage</code></td>
<td><span data-ttu-id="863f8-155"><span data-ttu-id="863f8-155">&ldquo;true&rdquo;或&ldquo;false&rdquo;。</span></span>
<p><span data-ttu-id="863f8-156">如果为 true，将禁止显示&ldquo;502.5 - 进程失败&rdquo;页面，而会优先显示 web.config 中配置的 502 状态代码页面。</span></p>
</td>
<td><code>false</code></td>
</tr>
<tr>
<td><code>forwardWindowsAuthToken</code></td>
<td><span data-ttu-id="863f8-157"><span data-ttu-id="863f8-157">&ldquo;true&rdquo;或&ldquo;false&rdquo;。</span></span>
<p>&nbsp;<span data-ttu-id="863f8-158">如果为 true，会将令牌作为每个请求的标头&ldquo;MS-ASPNETCORE-WINAUTHTOKEN&rdquo;，转发到在 %ASPNETCORE_PORT% 上侦听的子进程。&nbsp;<span data-ttu-id="863f8-159">该进程负责在每个请求的此令牌上调用 CloseHandle。</span></span></p>
</td>
<td><code>true</code></td>
</tr>
<tr>
<td><code>processPath</code></td>
<td>
<p><span data-ttu-id="863f8-160">必需的字符串属性。</span></p>
<p><span data-ttu-id="863f8-161">为 HTTP 请求启动进程侦听的可执行文件的路径。&nbsp;<span data-ttu-id="863f8-162">支持相对路径。&nbsp;<span data-ttu-id="863f8-163">如果路径以&nbsp;<code>.</code>&nbsp;开头，则该路径被视为与站点根目录相对。</span></span></span></p>
</td>
<td>&nbsp;</td>
</tr>
<tr>
<td><code>rapidFailsPerMinute</code></td>
<td>
<p><span data-ttu-id="863f8-164">可选的整数属性。</span></p>
<p><span data-ttu-id="863f8-165">指定允许 processPath 中指定的进程每分钟崩溃的次数。&nbsp;<span data-ttu-id="863f8-166">如果超出了此限制，模块将在剩余分钟数内停止启动该进程。</span></span></p>
</td>
<td><code>10</code></td>
</tr>
<tr>
<td><code>requestTimeout</code></td>
<td>
<p><span data-ttu-id="863f8-167">可选的 timespan 属性。</span></p>
<p><span data-ttu-id="863f8-168">指定 ASP.NET Core 模块等待来自 %ASPNETCORE_PORT% 上侦听的进程的响应的持续时间。</span></p>
<p><span data-ttu-id="863f8-169">在 ASP.NET Core 2.1 或更高版本附带的 ASP.NET Core 模块版本中，使用小时数、分钟数和秒数指定&nbsp;<code>requestTimeout</code>。</span></p>
</td>
<td><code>00:02:00</code></td>
</tr>
<tr>
<td><code>shutdownTimeLimit</code></td>
<td>
<p><span data-ttu-id="863f8-170">可选的整数属性。</span></p>
<p><span data-ttu-id="863f8-171">检测到 app_offline.htm 文件时，模块等待可执行文件正常关闭的持续时间（以秒为单位）。</span></p>
</td>
<td><code>10</code></td>
</tr>
<tr>
<td><code>startupTimeLimit</code></td>
<td>
<p><span data-ttu-id="863f8-172">可选的整数属性。</span></p>
<p><span data-ttu-id="863f8-173">模块等待可执行文件启动端口上侦听的进程的持续时间（以秒为单位）。&nbsp;<span data-ttu-id="863f8-174">如果超出了此时间限制，模块将终止该进程。&nbsp;<span data-ttu-id="863f8-175">模块在收到新请求时尝试重新启动该进程，并在收到后续传入请求时继续尝试重新启动该进程，除非应用在上一回滚分钟内无法启动 rapidFailsPerMinute 次。</span></span></span></p>
</td>
<td><code>120</code></td>
</tr>
<tr>
<td><code>stdoutLogEnabled</code></td>
<td>
<p><span data-ttu-id="863f8-176">可选布尔属性。</span></p>
<p><span data-ttu-id="863f8-177">如果为 true，processPath 中指定的 进程的 stdout 和 stderr 将重定向到 stdoutLogFile 中指定的文件。</span></p>
</td>
<td><code>false</code></td>
</tr>
<tr>
<td><code>stdoutLogFile</code></td>
<td>
<p><span data-ttu-id="863f8-178">可选的字符串属性。</span></p>
<p><span data-ttu-id="863f8-179">指定在其中记录 processPath 中指定进程的 stdout 和 stderr 的相对路径或绝对路径。&nbsp;<span data-ttu-id="863f8-180">相对路径与站点根目录相对。&nbsp;<span data-ttu-id="863f8-181">以&nbsp;<code>.</code>&nbsp;开头的任何路径均与站点根目录相对，所有其他路径被视为绝对路径。&nbsp;<span data-ttu-id="863f8-182">路径中提供的任何文件夹都必须存在，以便模块创建日志文件。&nbsp;<span data-ttu-id="863f8-183">使用下划线分隔符，将时间戳、进程 ID 和文件扩展名 (.log) 添加到 stdoutLogFile 路径的最后一段。&nbsp;<span data-ttu-id="863f8-184">如果&nbsp;<code>.\logs\stdout</code>&nbsp;作为值提供，则在示例 stdout 日志使用进程 ID 1934 于 2018 年 2 月 5 日 19:41:32 保存时，将在 logs 文件夹中保存为 stdout_20180205194132_1934.log。</span></span></span></span></span></span></p>
</td>
<td><code>aspnetcore-stdout</code></td>
</tr>
</tbody>
</table>
<p>&nbsp;②设置环境变量</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">aspNetCore </span><span style="color: #ff0000;">processPath</span><span style="color: #0000ff;">="dotnet"</span><span style="color: #ff0000;">
      arguments</span><span style="color: #0000ff;">=".\MyApp.dll"</span><span style="color: #ff0000;">
      stdoutLogEnabled</span><span style="color: #0000ff;">="false"</span><span style="color: #ff0000;">
      stdoutLogFile</span><span style="color: #0000ff;">="\\?\%home%\LogFiles\stdout"</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">environmentVariables</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">environmentVariable </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="ASPNETCORE_ENVIRONMENT"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">="Development"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">environmentVariable </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="CONFIG_DIR"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">="f:\application_config"</span> <span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">environmentVariables</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">aspNetCore</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>ASPNETCORE_ENVIRONMENT：设置环境</p>
<p>CONFIG_DIR：用户定义的环境变量的一个示例，其中开发人员已写入可在启动时读取值的代码以便形成用于加载应用配置文件的路径</p>
<p><span style="font-size: 12px; color: #ff0000;">在不可访问不受信任的网络（如 Internet）的暂存服务器和测试服务器上，仅将&nbsp;<code>ASPNETCORE_ENVIRONMENT</code>&nbsp;环境变量设置为&nbsp;<code>Development</code>。</span></p>
<p>&nbsp;</p>
<p><strong>3，<span data-ttu-id="863f8-194">app_offline.htm文件</span></strong></p>
<p><span data-ttu-id="863f8-194">将此文件放到程序根目录（不是wwwroot下的目录），<span data-ttu-id="863f8-197">存在 app_offline.htm 文件时，ASP.NET Core 模块会通过发送回 app_offline.htm 文件的内容来响应请求。&nbsp;<span data-ttu-id="863f8-198">删除 app_offline.htm 文件后，下一个请求将启动应用</span></span></span></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">二、CentOS7部署asp.net core</span></strong></p>
<p><strong>1，安装Nginx</strong></p>
<p>①添加Nginx存储库</p>
<p>要添加CentOS 7 EPEL仓库，请打开终端并使用以下命令：&nbsp;<span class="cnblogs_code">sudo yum install epel-release</span>&nbsp;</p>
<p>如果出现以下错误：</p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201806/741594-20180605200604856-322093230.png" alt="" /></p>
<p>解决方法，输入一下两个命令：</p>
<p>&nbsp;<span class="cnblogs_code">yum clean all</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">yum makecache </span>&nbsp;</p>
<p>②安装Nginx</p>
<p>现在Nginx存储库已经安装在您的服务器上，使用以下<code>yum</code>命令安装Nginx&nbsp;：&nbsp;<span class="cnblogs_code">sudo yum install nginx</span>&nbsp;</p>
<p>在对提示回答yes后，Nginx将在服务器上完成安装</p>
<p>③启动Nginx</p>
<p>Nginx不会自行启动。要运行Nginx，请输入：&nbsp;<span class="cnblogs_code">sudo systemctl start nginx</span>&nbsp;</p>
<p>如果您正在运行防火墙，请运行以下命令以允许HTTP和HTTPS通信：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">sudo firewall-cmd --permanent --zone=public --add-service=http 
sudo firewall-cmd --permanent --zone=public --add-service=https
sudo firewall-cmd --reload</span></pre>
</div>
<p>④如果想在系统启动时启用Nginx。请输入以下命令：</p>
<p>&nbsp;<span class="cnblogs_code">sudo systemctl enable nginx</span>&nbsp;</p>
<p>其他命令：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">systemctl disable nginx   #禁止开机启动
systemctl status nginx     #查看运行状态
systemctl restart nginx    #重启服务</span></pre>
</div>
<p>&nbsp;<span class="cnblogs_code">nginx -s reload</span>&nbsp;重启nginx</p>
<p>&nbsp;</p>
<p><strong>2，安装asp.net core运行时&nbsp;</strong></p>
<p><a href="https://www.microsoft.com/net/download/linux-package-manager/centos/runtime-current" target="_blank">https://www.microsoft.com/net/download/linux-package-manager/centos/runtime-current</a></p>
<p>&nbsp;</p>
<p><strong>3，配置nginx设置反向代理</strong></p>
<p>①修改配置文件&nbsp;<span class="cnblogs_code">/etc/nginx/nginx.conf</span>&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">server {
    listen </span>8054<span style="color: #000000;">;
    location </span>/<span style="color: #000000;"> {
        proxy_pass http:</span>//localhost:5000<span style="color: #000000;">;
        proxy_http_version </span>1.1<span style="color: #000000;">;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection keep</span>-<span style="color: #000000;">alive;
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}</span></pre>
</div>
<p>修改完成之后执行&nbsp;<span class="cnblogs_code">nginx -s reload</span>&nbsp;重启nginx</p>
<p>②由于SELinux保护机制所导致，我们需要将Nginx添加至SELinux的白名单，需要执行命令</p>
<div class="cnblogs_code">
<pre>yum install policycoreutils-<span style="color: #000000;">python

sudo cat </span>/var/log/audit/audit.log | grep nginx | grep denied | audit2allow -<span style="color: #000000;">M mynginx

sudo semodule </span>-i mynginx.pp</pre>
</div>
<p>③启动</p>
<p>第一步&nbsp;<span class="cnblogs_code">dotnet &lt;项目程序集dll&gt;</span>&nbsp;</p>
<p>第二步访问http://ip:8054就可以访问到网站了</p>
<p>&nbsp;</p>
<p><strong>4，Supervisor配置守护进程</strong></p>
<p>使用Supervisor首先我们的asp.net core项目进程，实时监控进程状态，异常退出时能自动重启</p>
<p>①安装Supervisor</p>
<p>&nbsp;<span class="cnblogs_code">yum install python-setuptools</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">easy_install supervisor</span>&nbsp;请更换<code>root</code>用户，执行如下命令安装Supervisor：</p>
<p>②配置Supervisor</p>
<p>运行<code>supervisord</code>服务的时候，需要指定Supervisor配置文件，如果没有显示指定，默认会从以下目录中加载：</p>
<div class="cnblogs_code">
<pre>$CWD/supervisord.conf  <span style="color: #008000;">#</span><span style="color: #008000;">$CWD表示运行supervisord程序的目录</span>
$CWD/etc/<span style="color: #000000;">supervisord.conf
</span>/etc/<span style="color: #000000;">supervisord.conf
</span>/etc/supervisor/supervisord.conf (since Supervisor 3.3<span style="color: #000000;">.0)
..</span>/etc/<span style="color: #000000;">supervisord.conf (Relative to the executable)
..</span>/supervisord.conf (Relative to the executable)</pre>
</div>
<p>所以先要创建一个supervisor目录&nbsp;<span class="cnblogs_code">mkdir /etc/supervisor</span>&nbsp;</p>
<p>③加载目录有了，然后通过<code>echo_supervisord_conf</code>程序（用来生成初始配置文件）来初始化一个配置文件：&nbsp;<span class="cnblogs_code">echo_supervisord_conf &gt; /etc/supervisor/supervisord.conf</span>&nbsp;</p>
<p>④打开<code>supervisord.conf</code>文件，需要修改底部的配置，改为：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">[include]
files </span>= conf.d/*.conf</pre>
</div>
<p>把注释去除、设置<code>/etc/supervisor/conf.d</code>为Supervisor进程配置文件加载目录</p>
<p>⑥创建进程配置加载目录：&nbsp;<span class="cnblogs_code">mkdir /etc/supervisor/conf.d</span>&nbsp;</p>
<p>⑦在&nbsp;<span class="cnblogs_code">/etc/supervisor/conf.d</span>&nbsp;目录下创建一个&nbsp;<span class="cnblogs_code">netcore.conf</span>&nbsp;文件</p>
<p>⑧配置<span class="cnblogs_code">netcore.conf&nbsp;文件</span></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">[program:SignalRDemo]                        ;自定义进程名称
command</span>=<span style="color: #000000;">dotnet SignalRDemo.dll               ;程序启动命令
directory</span>=/usr/share/nginx/<span style="color: #000000;">publish              ;命令执行的目录
autostart</span>=<span style="color: #000000;">true                                  ;在Supervisord启动时，程序是否启动
autorestart</span>=<span style="color: #000000;">true                                ;程序退出后自动重启
startretries</span>=5<span style="color: #000000;">                                  ;启动失败自动重试次数，默认是3
startsecs</span>=1<span style="color: #000000;">                                     ;自动重启间隔
user</span>=<span style="color: #000000;">root                                       ;设置启动进程的用户，默认是root
priority</span>=999<span style="color: #000000;">                                    ;进程启动优先级，默认999，值小的优先启动
stderr_logfile</span>=/var/log/<span style="color: #000000;">SignalRDemo.log  ;标准错误日志
stdout_logfile</span>=/var/log/<span style="color: #000000;">SignalRDemo.log  ;标准输出日志
environment</span>=ASPNETCORE_ENVIRONMENT=<span style="color: #000000;">Production   ;进程环境变量
stopsignal</span>=INT                                  ;请求停止时用来杀死程序的信号</pre>
</div>
<p>⑨启动Supervisor服务，命令如下：&nbsp;<span class="cnblogs_code">supervisord -c /etc/supervisor/supervisord.conf</span>&nbsp;</p>
<p>这时，在会发现我们部署的网站程序不在shell中通过<code>dotnet xxx.dll</code>启动，同样可以访问。</p>
<p>⑩设置Supervisor开机启动</p>
<p>第一步：在&nbsp;<span class="cnblogs_code">/usr/lib/systemd/system/</span>&nbsp;目录下创建&nbsp;<span class="cnblogs_code">supervisor.service</span>&nbsp;文件</p>
<p><span class="cnblogs_code">supervisor.service&nbsp;</span>文件内容如下：</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">#</span><span style="color: #008000;"> supervisord service for systemd (CentOS 7.0+)</span><span style="color: #008000;">
#</span><span style="color: #008000;"> by ET-CS (https://github.com/ET-CS)</span>
<span style="color: #000000;">[Unit]
Description</span>=<span style="color: #000000;">Supervisor daemon

[Service]
Type</span>=<span style="color: #000000;">forking
ExecStart</span>=/usr/bin/supervisord -c /etc/supervisor/<span style="color: #000000;">supervisord.conf
ExecStop</span>=/usr/bin/<span style="color: #000000;">supervisorctl $OPTIONS shutdown
ExecReload</span>=/usr/bin/<span style="color: #000000;">supervisorctl $OPTIONS reload
KillMode</span>=<span style="color: #000000;">process
Restart</span>=on-<span style="color: #000000;">failure
RestartSec</span>=<span style="color: #000000;">42s

[Install]
WantedBy</span>=multi-user.target</pre>
</div>
<p>第二步：设置开机启动：&nbsp;<span class="cnblogs_code">systemctl enable supervisor</span>&nbsp;</p>
<p>第三部：验证是否成功：&nbsp;<span class="cnblogs_code">systemctl <span style="color: #0000ff;">is</span>-enabled supervisor</span>&nbsp;</p>
<p>如果输出<code>enabled</code>则表示设置成功，也可重启服务器验证。</p>
<p>&nbsp;</p>
<p><strong>5，Supervisorctl管理进程</strong></p>
<p>进入<code>supervisorctl</code>交互终端：&nbsp;<span class="cnblogs_code">supervisorctl</span>&nbsp;</p>
<p>输入<code>help</code>查询帮助：</p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201806/741594-20180607112447536-2142772158.png" alt="" /></p>
<p>&nbsp;</p>
<p>问题：<a href="http://www.cashqian.net/blog/001472975510127673ea63db9234c4e8293cf43cefcafde000" target="_blank">1，"unix:///tmp/supervisor.sock no such file" 错误处理</a></p>
<p>&nbsp;</p>
<p>&nbsp;<strong>6，Supervisorctl错误</strong></p>
<div class="postTitle"><a id="cb_post_title_url" href="https://www.cnblogs.com/WangShengguang/p/5332232.html">supervisor Error: Another program is already listening</a></div>
<div class="postText">
<div id="cnblogs_post_body" class="blogpost-body">
<p>Error: Another program is already listening on a port that one of our HTTP servers is configured to use.&nbsp; Shut this program down first before starting supervisord.</p>
<p>StackOverflow<a title="http://serverfault.com/questions/114477/supervisor-http-server-port-issue" href="http://serverfault.com/questions/114477/supervisor-http-server-port-issue">&nbsp; http://serverfault.com/questions/114477/supervisor-http-server-port-issue</a></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<pre><code>sudo unlink /tmp/supervisor.sock

sudo unlink /var/run/supervisor.sock
</code></pre>
<p>This .sock file is defined in /etc/supervisord.conf's [unix_http_server]'s file config value (default is /tmp/supervisor.sock or /var/run/supervisor.sock).</p>
<p>Hope this helps someone in the future.</p>
</div>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p><strong>6，nginx代理signalR站点</strong></p>
<p>编辑/etc/nginx/nginx.conf文件</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">  map $http_upgrade $connection_upgrade{
        </span><span style="color: #0000ff;">default</span><span style="color: #000000;"> upgrade;
        &lsquo;&rsquo; close;
    } 
 server {
    listen </span><span style="color: #800080;">8054</span><span style="color: #000000;">;
    location </span>/<span style="color: #000000;"> {
        proxy_pass http:</span><span style="color: #008000;">//</span><span style="color: #008000;">localhost:5000;</span>
        proxy_http_version <span style="color: #800080;">1.1</span><span style="color: #000000;">;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection $connection_upgrade;
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }</span></pre>
</div>
<p>&nbsp;</p>