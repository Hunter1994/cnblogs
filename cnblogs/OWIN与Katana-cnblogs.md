<p><strong><a href="#a1">一、OWIN</a></strong></p>
<p><strong><a href="#a2">二、Katana</a></strong></p>
<p><strong><a href="#a3">三、Middleware中间件</a></strong></p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a1"></a>一、OWIN</span></strong></span></p>
<p><strong>1，OWIN介绍</strong></p>
<p>OWIN是Open Web Server Interface for .Net的首字母缩写。OWIN在.Net Web Server与Web Application之间定义了一套标准接口。OWIN的目标用于解耦Web Server与Web Application。OWIN只是一个契约、规范，而非代码的实现（Katana实现了OWIN）</p>
<p><strong>2，OWIN规范</strong></p>
<p>1）OWIN定义了Host、Server、Middleware、Application四层</p>
<p>①Host：主要负责应用程序的配置和启动进程，包括初始化OWIN Pipeline（管道，包含了Middleware）、运行Server</p>
<p>②Server：绑定套接字并监听Http请求，然后将Request和Response的Body、Header封装成符合OWIN规范的字典并发送到OWIN Middleware Pipeline中处理</p>
<p>②Middleware：中间件、组件，位于Server与Application之间，用来处理发送到Pipeline中的请求</p>
<p>④Application：具体的应用程序代码</p>
<p>2）Application Delegate（应用程序委托），用于Server与Middleware的交互。他并不是严格意义上的接口，而是一个委托并且每个OWIN中间件组件必须提供。</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201711/741594-20171111232254263-1768697459.png" alt="" width="338" height="69" /></p>
<p>3）Environment Dictionary（环境字典），对http请求的封装</p>
<p>request data：</p>
<table class="table-view log-set-param" style="width: 800px;" border="1">
<tbody>
<tr>
<td valign="top">
<div class="para">Required</div>
</td>
<td>
<div class="para">Key Name</div>
</td>
<td>
<div class="para">Value Description</div>
</td>
</tr>
<tr>
<td valign="top">
<div class="para">Yes</div>
</td>
<td>
<div class="para">"owin.RequestBody"</div>
</td>
<td>
<div class="para">请求体。Stream类型</div>
</td>
</tr>
<tr>
<td valign="top">
<div class="para">Yes</div>
</td>
<td>
<div class="para">"owin.RequestHeaders"</div>
</td>
<td>
<div class="para">请求头。IDictionary&lt;string, string[]&gt;类型</div>
</td>
</tr>
<tr>
<td valign="top">
<div class="para">Yes</div>
</td>
<td>
<div class="para">"owin.RequestMethod"</div>
</td>
<td>
<div class="para">包含请求的HTTP请求方法（例如，&ldquo;GET&rdquo;，&ldquo;POST&rdquo;）的字符串。</div>
</td>
</tr>
<tr>
<td valign="top">
<div class="para">Yes</div>
</td>
<td>
<div class="para">"owin.RequestPath"</div>
</td>
<td>
<div class="para">包含请求路径的字符串。 该路径必须是相对于应用程序委托的&ldquo;根&rdquo;的</div>
</td>
</tr>
<tr>
<td valign="top">
<div class="para">Yes</div>
</td>
<td>
<div class="para">"owin.RequestPathBase"</div>
</td>
<td>
<div class="para">包含与应用程序委托的&ldquo;根&rdquo;对应的请求路径部分的字符串</div>
</td>
</tr>
<tr>
<td valign="top">
<div class="para">Yes</div>
</td>
<td>
<div class="para">"owin.RequestProtocol"</div>
</td>
<td>
<div class="para">包含协议名称和版本的字符串（例如&ldquo;HTTP / 1.0&rdquo;或&ldquo;HTTP / 1.1&rdquo;）。</div>
</td>
</tr>
<tr>
<td valign="top">
<div class="para">Yes</div>
</td>
<td>
<div class="para">"owin.RequestQueryString"</div>
</td>
<td>
<div class="para">包含HTTP请求URI的查询字符串组件的字符串，不含前导&ldquo;？&rdquo;（例如，&ldquo;foo = bar＆baz = quux&rdquo;）。 该值可能是一个空字符串。</div>
</td>
</tr>
<tr>
<td valign="top">
<div class="para">Yes</div>
</td>
<td>
<div class="para">"owin.RequestScheme"</div>
</td>
<td>
<div class="para">包含用于请求的URI方案（例如&ldquo;http&rdquo;，&ldquo;https&rdquo;）的字符串</div>
</td>
</tr>
</tbody>
</table>
<p>response data：</p>
<table class="table-view log-set-param" style="width: 800px;" border="1">
<tbody>
<tr>
<td valign="top">
<div class="para">Required</div>
</td>
<td>
<div class="para">Key Name</div>
</td>
<td>
<div class="para">Value Description</div>
</td>
</tr>
<tr>
<td valign="top">
<div class="para">Yes</div>
</td>
<td>
<div class="para">"owin.ResponseBody"</div>
</td>
<td>
<div class="para">响应体。Stream类型</div>
</td>
</tr>
<tr>
<td valign="top">
<div class="para">Yes</div>
</td>
<td>
<div class="para">"owin.ResponseHeaders"</div>
</td>
<td>
<div class="para">响应头。IDictionary&lt;string, string[]&gt;类型</div>
</td>
</tr>
<tr>
<td valign="top">
<div class="para">No</div>
</td>
<td>
<div class="para">"owin.ResponseStatusCode"</div>
</td>
<td>
<div class="para">包含RFC 2616第6.1.1节中定义的HTTP响应状态代码的可选项。 默认值是200。</div>
</td>
</tr>
<tr>
<td valign="top">
<div class="para">No</div>
</td>
<td>
<div class="para">"owin.ResponseReasonPhrase"</div>
</td>
<td>
<div class="para">包含原因短语的可选字符串关联给定的状态码。 如果没有提供，则服务器应该按照RFC 2616第6.1.1节的规定提供默认值</div>
</td>
</tr>
<tr>
<td valign="top">
<div class="para">No</div>
</td>
<td>
<div class="para">"owin.ResponseProtocol"</div>
</td>
<td>
<div class="para">包含协议名称和版本的可选字符串（例如&ldquo;HTTP / 1.0&rdquo;或&ldquo;HTTP / 1.1&rdquo;）。 如果没有提供，则&ldquo;owin.RequestProtocol&rdquo;键的值是默认值。</div>
</td>
</tr>
</tbody>
</table>
<p>other data：</p>
<table class="table-view log-set-param" style="height: 65px; width: 800px;" border="1">
<tbody>
<tr>
<td valign="top">
<div class="para">Required</div>
</td>
<td>
<div class="para">Key Name</div>
</td>
<td>
<div class="para">Value Description</div>
</td>
</tr>
<tr>
<td valign="top">
<div class="para">Yes</div>
</td>
<td>
<div class="para">"owin.CallCancelled"</div>
</td>
<td>
<div class="para">指示请求是否被取消/中止</div>
</td>
</tr>
<tr>
<td valign="top">
<div class="para">Yes</div>
</td>
<td>
<div class="para">"owin.Version"</div>
</td>
<td>
<div class="para">表示OWIN版本的字符串&ldquo;1.0&rdquo;</div>
</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a2"></a>二、Katana</span></strong></span></p>
<p><strong>1，Katana介绍</strong></p>
<p>①Katana实现了OWIN的Layers</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201711/741594-20171112133855434-62476723.png" alt="" width="554" height="216" /></p>
<p>②Pileline中的Middleware是链式执行的，有开发人员控制</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201711/741594-20171112134057778-22150047.png" alt="" width="517" height="245" /></p>
<p>③层</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201711/741594-20171112134333091-621507856.png" alt="" width="610" height="315" /></p>
<p>&nbsp;</p>
<p><strong>2，使用ASP.NET/IIS托管Katana-based应用程序</strong></p>
<p>nuget Microsoft.Owin.Host.SystemWeb</p>
<p>添加Startup启动类将Middleware中间件注册到Pileline中</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('ecf43aa1-9a1b-4e51-a3e4-d07020284242')"><img id="code_img_closed_ecf43aa1-9a1b-4e51-a3e4-d07020284242" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_ecf43aa1-9a1b-4e51-a3e4-d07020284242" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('ecf43aa1-9a1b-4e51-a3e4-d07020284242',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_ecf43aa1-9a1b-4e51-a3e4-d07020284242" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Owin;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Owin;

[assembly: OwinStartup(</span><span style="color: #0000ff;">typeof</span><span style="color: #000000;">(Katana.Systen.Web.Startup))]

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> Katana.Systen.Web
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Startup
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configuration(IAppBuilder app)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> 有关如何配置应用程序的详细信息，请访问 </span><span style="color: #008000; text-decoration: underline;">https://go.microsoft.com/fwlink/?LinkID=316888</span>
<span style="color: #000000;">
            app.Run(context </span>=&gt; { <span style="color: #0000ff;">return</span> context.Response.WriteAsync(<span style="color: #800000;">"</span><span style="color: #800000;">holle World</span><span style="color: #800000;">"</span><span style="color: #000000;">); });
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Startup</span></div>
<p><strong>3，自托管Katana-based应用程序</strong></p>
<p>nuget Microsoft.Owin.SelfHost</p>
<p>在Main方法中使用Startup配置项构建Pipeline并监听端口</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('eff42476-ade3-451c-900e-dc9acfb1923b')"><img id="code_img_closed_eff42476-ade3-451c-900e-dc9acfb1923b" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_eff42476-ade3-451c-900e-dc9acfb1923b" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('eff42476-ade3-451c-900e-dc9acfb1923b',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_eff42476-ade3-451c-900e-dc9acfb1923b" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Owin.Hosting;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> Katana.SelfHost
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #0000ff;">using</span> (WebApp.Start&lt;Startup&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:7000</span><span style="color: #800000;">"</span><span style="color: #000000;">))
            {
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">程序启动</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                Console.ReadLine();
            }

        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Program</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('a8949b2a-db54-4d1c-b260-2386291b2432')"><img id="code_img_closed_a8949b2a-db54-4d1c-b260-2386291b2432" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_a8949b2a-db54-4d1c-b260-2386291b2432" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('a8949b2a-db54-4d1c-b260-2386291b2432',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_a8949b2a-db54-4d1c-b260-2386291b2432" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Owin;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Owin;

[assembly: OwinStartup(</span><span style="color: #0000ff;">typeof</span><span style="color: #000000;">(Katana.SelfHost.Startup))]

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> Katana.SelfHost
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Startup
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configuration(IAppBuilder app)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> 有关如何配置应用程序的详细信息，请访问 </span><span style="color: #008000; text-decoration: underline;">https://go.microsoft.com/fwlink/?LinkID=316888</span>
<span style="color: #000000;">
            app.Run(context </span>=&gt; { <span style="color: #0000ff;">return</span> context.Response.WriteAsync(<span style="color: #800000;">"</span><span style="color: #800000;">holle World</span><span style="color: #800000;">"</span><span style="color: #000000;">); });
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Startup</span></div>
<p><strong>3.1，使用Katana Diagnostic Helpers</strong></p>
<p>将应用程序运行在自定义Host中，将失去IIS中所有的管理、诊断功能，但我们可以使用Katana提供的内置Helper比如Diagnostic helper来获取</p>
<p>nuget Micorost.Owin.Diagnostic</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('7f9d6eb4-d033-48ba-9765-92f83f39a105')"><img id="code_img_closed_7f9d6eb4-d033-48ba-9765-92f83f39a105" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_7f9d6eb4-d033-48ba-9765-92f83f39a105" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('7f9d6eb4-d033-48ba-9765-92f83f39a105',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_7f9d6eb4-d033-48ba-9765-92f83f39a105" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Owin.Hosting;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> Katana.SelfHost
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #0000ff;">using</span> (WebApp.Start&lt;DiagnosticStartup&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:7000</span><span style="color: #800000;">"</span><span style="color: #000000;">))
            {
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">程序启动</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                Console.ReadLine();
            }

        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Program</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('9b4e7f21-9a34-44c5-aec3-0f4c580c6542')"><img id="code_img_closed_9b4e7f21-9a34-44c5-aec3-0f4c580c6542" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_9b4e7f21-9a34-44c5-aec3-0f4c580c6542" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('9b4e7f21-9a34-44c5-aec3-0f4c580c6542',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_9b4e7f21-9a34-44c5-aec3-0f4c580c6542" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Owin;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Owin;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Diagnostics;

[assembly: OwinStartup(</span><span style="color: #0000ff;">typeof</span><span style="color: #000000;">(Katana.SelfHost.DiagnosticStartup))]

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> Katana.SelfHost
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> DiagnosticStartup
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configuration(IAppBuilder app)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> 有关如何配置应用程序的详细信息，请访问 </span><span style="color: #008000; text-decoration: underline;">https://go.microsoft.com/fwlink/?LinkID=316888</span>

            <span style="color: #008000;">//</span><span style="color: #008000;">将一个WelcomePage Middleware注册到pipeline中
            </span><span style="color: #008000;">//</span><span style="color: #008000;">（在此输出WelcomePage渲染页面，并且不会执行余下的pipeline middleware组件）</span>
            app.UseWelcomePage(<span style="color: #800000;">"</span><span style="color: #800000;">/</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            </span><span style="color: #008000;">//</span><span style="color: #008000;">将一个错误页注册到pipeline中</span>
<span style="color: #000000;">            app.UseErrorPage();
            app.Run(context </span>=&gt;<span style="color: #000000;">
            {
                </span><span style="color: #0000ff;">if</span> (context.Request.Path.ToString().Equals(<span style="color: #800000;">"</span><span style="color: #800000;">/error</span><span style="color: #800000;">"</span><span style="color: #000000;">))
                {
                    Trace.WriteLine(context.Request.Path);
                    </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> Exception(<span style="color: #800000;">"</span><span style="color: #800000;">抛出异常</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                }
                </span><span style="color: #0000ff;">return</span> context.Response.WriteAsync(<span style="color: #800000;">"</span><span style="color: #800000;">Hello World</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            });
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">DiagnosticStartup</span></div>
<p><strong>5，使用OwinHost.exe托管Katana-based应用程序</strong></p>
<p>nuget OwinHost</p>
<p>nuget Micosoft.Owin</p>
<p>配置web属性</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201711/741594-20171112144257716-1703756638.png" alt="" width="448" height="214" /></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('b3108792-0b98-44f8-9a69-63dcb06e4c8f')"><img id="code_img_closed_b3108792-0b98-44f8-9a69-63dcb06e4c8f" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_b3108792-0b98-44f8-9a69-63dcb06e4c8f" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('b3108792-0b98-44f8-9a69-63dcb06e4c8f',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_b3108792-0b98-44f8-9a69-63dcb06e4c8f" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Owin;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Owin;

[assembly: OwinStartup(</span><span style="color: #0000ff;">typeof</span><span style="color: #000000;">(Katana.OwinHost.WebApp.Startup))]

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> Katana.OwinHost.WebApp
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Startup
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configuration(IAppBuilder app)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> 有关如何配置应用程序的详细信息，请访问 </span><span style="color: #008000; text-decoration: underline;">https://go.microsoft.com/fwlink/?LinkID=316888</span>
<span style="color: #000000;">
            app.Run(context </span>=&gt; { <span style="color: #0000ff;">return</span> context.Response.WriteAsync(<span style="color: #800000;">"</span><span style="color: #800000;">holle World</span><span style="color: #800000;">"</span><span style="color: #000000;">); });
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Startup</span></div>
<p><strong>6，几种制定Startup启动项方式</strong></p>
<p>①默认名称约束：Host会去查找root namespace 下名为Startup的类作为启动项</p>
<p>②OwinStartup Attribute：当创建Owin Startup类时，自动会加上Attribute如：</p>
<p>&nbsp;<span class="cnblogs_code">[assembly: OwinStartup(<span style="color: #0000ff;">typeof</span>(Katana.OwinHost.WebApp.Startup))]</span>&nbsp;</p>
<p>③配置文件：如：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">add </span><span style="color: #ff0000;">key</span><span style="color: #0000ff;">="owin:appStartup"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">="Katana.OwinHost.WebApp.Startup"</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>④如果使用自定一host，那么可以通过&nbsp;<span class="cnblogs_code">WebApp.Start<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">DiagnosticStartup</span><span style="color: #0000ff;">&gt;</span>("http://localhost:7000")</span>&nbsp;来设置启动项</p>
<p>⑤如果使用OwinHost，那么可以通过命名行参数来实现</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a3"></a>三、创建自定义Middleware中间件</span></strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Owin;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Owin;

[assembly: OwinStartup(</span><span style="color: #0000ff;">typeof</span><span style="color: #000000;">(Katana.OwinHost.WebApp.Startup))]

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> Katana.OwinHost.WebApp
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Startup
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configuration(IAppBuilder app)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> 有关如何配置应用程序的详细信息，请访问 </span><span style="color: #008000; text-decoration: underline;">https://go.microsoft.com/fwlink/?LinkID=316888</span>
            app.Use(<span style="color: #0000ff;">async</span> (context, next) =&gt;<span style="color: #000000;"> {

                </span><span style="color: #0000ff;">await</span> context.Response.WriteAsync(<span style="color: #800000;">"</span><span style="color: #800000;">begin</span><span style="color: #800000;">"</span>+<span style="color: #000000;">Environment.NewLine);
                </span><span style="color: #0000ff;">await</span><span style="color: #000000;"> next();
                </span><span style="color: #0000ff;">await</span> context.Response.WriteAsync(<span style="color: #800000;">"</span><span style="color: #800000;">end</span><span style="color: #800000;">"</span> +<span style="color: #000000;"> Environment.NewLine);

            });

            app.Use</span>&lt;MyMiddleware&gt;<span style="color: #000000;">();

            app.Run(context </span>=&gt; { <span style="color: #0000ff;">return</span> context.Response.WriteAsync(<span style="color: #800000;">"</span><span style="color: #800000;">holle World</span><span style="color: #800000;">"</span> +<span style="color: #000000;"> Environment.NewLine); });
        }
    }
}</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Web;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Owin;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> Katana.OwinHost.WebApp
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyMiddleware : OwinMiddleware
    {
        </span><span style="color: #0000ff;">public</span> MyMiddleware(OwinMiddleware next) : <span style="color: #0000ff;">base</span><span style="color: #000000;">(next) { }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">async</span><span style="color: #000000;"> Task Invoke(IOwinContext context)
        {
            </span><span style="color: #0000ff;">await</span> context.Response.WriteAsync(<span style="color: #800000;">"</span><span style="color: #800000;">MyMiddleware-begin</span><span style="color: #800000;">"</span> +<span style="color: #000000;"> Environment.NewLine);
            </span><span style="color: #0000ff;">await</span> <span style="color: #0000ff;">this</span><span style="color: #000000;">.Next.Invoke(context);
            </span><span style="color: #0000ff;">await</span> context.Response.WriteAsync(<span style="color: #800000;">"</span><span style="color: #800000;">MyMiddleware-end</span><span style="color: #800000;">"</span> +<span style="color: #000000;"> Environment.NewLine);
        }

    }
}</span></pre>
</div>
<p>案例下载：<a href="http://pan.baidu.com/s/1qXAmu2w" target="_blank">http://pan.baidu.com/s/1qXAmu2w</a></p>