<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">一、介绍</span></strong></p>
<p>SignalR对websocket、SSE、长连接、forever frame进行封装。</p>
<p><strong>websocket（html5</strong>）：ws协议，这个协议基于tcp的。也就是说和http没有关系（兼容性不好）</p>
<p><strong>SSE</strong>：客户端订阅服务器的一个事件，然后方便通过这个事件推送到客户端。 &nbsp;server =&gt; client&nbsp;</p>
<p><strong>长链接</strong>：保持一次链接的时间，例如保持一个链接5s</p>
<p><strong>forever frame</strong>：在body中藏一个iframe，那么这个iframe和server是一个永久链接，如果server来数据，通过这个链接推送到client</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">二、PersistentConnection</span></strong></p>
<p>1，参数</p>
<p> 《1》 request： 获取一些链接中的附加信息，request.querystring<br />　　　　　　　　request.cookie</p>
<p>                     　　　　　　　　request是一个katana的包装类。</p>
<p>                     　　　　　　　　singlaR 的request 其实是asp.net 中的 Request的子集。</p>
<p>   《2》 connectionId 这个参数就是 客户端连接到服务器的唯一标识。。。也就说这个标识标识了客户端。本质上来说，和SessionID是一个性质。 【GUID】</p>
<p>2，demo</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('85319090-d5f1-43be-a5cf-c8af8a89237f')"><img id="code_img_closed_85319090-d5f1-43be-a5cf-c8af8a89237f" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_85319090-d5f1-43be-a5cf-c8af8a89237f" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('85319090-d5f1-43be-a5cf-c8af8a89237f',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_85319090-d5f1-43be-a5cf-c8af8a89237f" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Owin;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Owin;

[assembly: OwinStartup(</span><span style="color: #0000ff;">typeof</span><span style="color: #000000;">(WebApplication1.Startup1))]

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> WebApplication1
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Startup1
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configuration(IAppBuilder app)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> For more information on how to configure your application, visit </span><span style="color: #008000; text-decoration: underline;">https://go.microsoft.com/fwlink/?LinkID=316888</span>
<span style="color: #000000;">            
            app.MapSignalR</span>&lt;MyConnection1&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">/connection</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Startup1</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('827f02c7-6e3b-4e66-968d-de34f24a6e38')"><img id="code_img_closed_827f02c7-6e3b-4e66-968d-de34f24a6e38" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_827f02c7-6e3b-4e66-968d-de34f24a6e38" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('827f02c7-6e3b-4e66-968d-de34f24a6e38',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_827f02c7-6e3b-4e66-968d-de34f24a6e38" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Web;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNet.SignalR;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> WebApplication1
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyConnection1 : PersistentConnection
    {

        </span><span style="color: #008000;">//</span><span style="color: #008000;">js调用 start 触发</span>
        <span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span> Task OnConnected(IRequest request, <span style="color: #0000ff;">string</span><span style="color: #000000;"> connectionId)
        {
            </span><span style="color: #0000ff;">return</span> Connection.Send(connectionId, <span style="color: #800000;">"</span><span style="color: #800000;">Welcome!</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;">js 调用send触发</span>
        <span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span> Task OnReceived(IRequest request, <span style="color: #0000ff;">string</span> connectionId, <span style="color: #0000ff;">string</span><span style="color: #000000;"> data)
        {
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> Connection.Broadcast(data);
        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;">关闭连接（或者浏览器窗口）触发</span>
        <span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span> Task OnDisconnected(IRequest request, <span style="color: #0000ff;">string</span> connectionId, <span style="color: #0000ff;">bool</span><span style="color: #000000;"> stopCalled)
        {
            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">base</span><span style="color: #000000;">.OnDisconnected(request, connectionId, stopCalled);
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">MyConnection1</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('d7a0864d-56ca-4fa0-a40a-637cd4c69734')"><img id="code_img_closed_d7a0864d-56ca-4fa0-a40a-637cd4c69734" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_d7a0864d-56ca-4fa0-a40a-637cd4c69734" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('d7a0864d-56ca-4fa0-a40a-637cd4c69734',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_d7a0864d-56ca-4fa0-a40a-637cd4c69734" class="cnblogs_code_hide">
<pre>&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
    &lt;meta charset=<span style="color: #800000;">"</span><span style="color: #800000;">utf-8</span><span style="color: #800000;">"</span> /&gt;
    &lt;title&gt;&lt;/title&gt;
    &lt;script src=<span style="color: #800000;">"</span><span style="color: #800000;">Scripts/jquery-1.6.4.js</span><span style="color: #800000;">"</span>&gt;&lt;/script&gt;
    &lt;script src=<span style="color: #800000;">"</span><span style="color: #800000;">Scripts/jquery.signalR-2.2.3.js</span><span style="color: #800000;">"</span>&gt;&lt;/script&gt;
    &lt;script type=<span style="color: #800000;">"</span><span style="color: #800000;">text/javascript</span><span style="color: #800000;">"</span>&gt;
        <span style="color: #0000ff;">var</span> con = $.connection(<span style="color: #800000;">"</span><span style="color: #800000;">/connection</span><span style="color: #800000;">"</span><span style="color: #000000;">);

        </span><span style="color: #008000;">//</span><span style="color: #008000;">启动</span>
<span style="color: #000000;">        con.start(function (data) {
            con.send(</span><span style="color: #800000;">"</span><span style="color: #800000;">asdasd</span><span style="color: #800000;">"</span><span style="color: #000000;">)
        })

        con.received(function (data) {
            console.log(</span><span style="color: #800000;">"</span><span style="color: #800000;">receive:</span><span style="color: #800000;">"</span>+<span style="color: #000000;">data)
        })


    </span>&lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;

&lt;/body&gt;
&lt;/html&gt;</pre>
</div>
<span class="cnblogs_code_collapse">html</span></div>
<p>&nbsp;</p>
<p>二、group（建简易聊天室）</p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201804/741594-20180421192215526-655490584.png" alt="" width="1029" height="179" /></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('db180249-8d02-4b8c-b478-50f51a24c7f3')"><img id="code_img_closed_db180249-8d02-4b8c-b478-50f51a24c7f3" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_db180249-8d02-4b8c-b478-50f51a24c7f3" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('db180249-8d02-4b8c-b478-50f51a24c7f3',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_db180249-8d02-4b8c-b478-50f51a24c7f3" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Owin;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Owin;

[assembly: OwinStartup(</span><span style="color: #0000ff;">typeof</span><span style="color: #000000;">(WebApplication1.Startup1))]

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> WebApplication1
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Startup1
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configuration(IAppBuilder app)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> For more information on how to configure your application, visit </span><span style="color: #008000; text-decoration: underline;">https://go.microsoft.com/fwlink/?LinkID=316888</span>
<span style="color: #000000;">            
            app.MapSignalR</span>&lt;MyConnection1&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">/connection</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Startup1</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('b9aa9dca-d957-4496-874b-f81640b79608')"><img id="code_img_closed_b9aa9dca-d957-4496-874b-f81640b79608" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_b9aa9dca-d957-4496-874b-f81640b79608" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('b9aa9dca-d957-4496-874b-f81640b79608',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_b9aa9dca-d957-4496-874b-f81640b79608" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Web;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNet.SignalR;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> WebApplication1
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyConnection1 : PersistentConnection
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">const</span> <span style="color: #0000ff;">string</span> DEFAULT = <span style="color: #800000;">"</span><span style="color: #800000;">default</span><span style="color: #800000;">"</span><span style="color: #000000;">;
        </span><span style="color: #008000;">//</span><span style="color: #008000;">js调用 start 触发</span>
        <span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span> Task OnConnected(IRequest request, <span style="color: #0000ff;">string</span><span style="color: #000000;"> connectionId)
        {
            </span><span style="color: #0000ff;">this</span><span style="color: #000000;">.Groups.Add(connectionId, DEFAULT);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">excludeConnectionIds：排除通知的connectionId。在default组中，除了自己，其他人都能收到信息</span>
            <span style="color: #0000ff;">return</span> <span style="color: #0000ff;">this</span>.Groups.Send(DEFAULT, connectionId + <span style="color: #800000;">"</span><span style="color: #800000;">进入房间</span><span style="color: #800000;">"</span><span style="color: #000000;">, connectionId);
        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;">js 调用send触发</span>
        <span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span> Task OnReceived(IRequest request, <span style="color: #0000ff;">string</span> connectionId, <span style="color: #0000ff;">string</span><span style="color: #000000;"> data)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">excludeConnectionIds：排除通知的connectionId。在default组中，除了自己，其他人都能收到信息</span>
            <span style="color: #0000ff;">return</span> <span style="color: #0000ff;">this</span>.Groups.Send(DEFAULT, connectionId + <span style="color: #800000;">"</span><span style="color: #800000;">:</span><span style="color: #800000;">"</span> +<span style="color: #000000;"> data, connectionId);
        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;">关闭连接（或者浏览器窗口）触发</span>
        <span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span> Task OnDisconnected(IRequest request, <span style="color: #0000ff;">string</span> connectionId, <span style="color: #0000ff;">bool</span><span style="color: #000000;"> stopCalled)
        {
            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">base</span><span style="color: #000000;">.OnDisconnected(request, connectionId, stopCalled);
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">MyConnection1</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('c3c662b3-d4df-4bfb-a444-bdeadba09109')"><img id="code_img_closed_c3c662b3-d4df-4bfb-a444-bdeadba09109" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_c3c662b3-d4df-4bfb-a444-bdeadba09109" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('c3c662b3-d4df-4bfb-a444-bdeadba09109',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_c3c662b3-d4df-4bfb-a444-bdeadba09109" class="cnblogs_code_hide">
<pre>&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
    &lt;meta charset=<span style="color: #800000;">"</span><span style="color: #800000;">utf-8</span><span style="color: #800000;">"</span> /&gt;
    &lt;title&gt;&lt;/title&gt;
    &lt;script src=<span style="color: #800000;">"</span><span style="color: #800000;">Scripts/jquery-1.6.4.js</span><span style="color: #800000;">"</span>&gt;&lt;/script&gt;
    &lt;script src=<span style="color: #800000;">"</span><span style="color: #800000;">Scripts/jquery.signalR-2.2.3.js</span><span style="color: #800000;">"</span>&gt;&lt;/script&gt;
    &lt;script type=<span style="color: #800000;">"</span><span style="color: #800000;">text/javascript</span><span style="color: #800000;">"</span>&gt;<span style="color: #000000;">
        $(function () {


            </span><span style="color: #0000ff;">var</span> con = $.connection(<span style="color: #800000;">"</span><span style="color: #800000;">/connection</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            </span><span style="color: #008000;">//</span><span style="color: #008000;">启动</span>
<span style="color: #000000;">            con.start(function (data) {
            })

            con.received(function (data) {
                $(</span><span style="color: #800000;">"</span><span style="color: #800000;">#context</span><span style="color: #800000;">"</span>).append(<span style="color: #800000;">"</span><span style="color: #800000;">&lt;br/&gt;</span><span style="color: #800000;">"</span>+<span style="color: #000000;">data)
                console.log(data)
            })

            $(</span><span style="color: #800000;">"</span><span style="color: #800000;">#send</span><span style="color: #800000;">"</span><span style="color: #000000;">).click(function () {
                con.send($(</span><span style="color: #800000;">"</span><span style="color: #800000;">#txt</span><span style="color: #800000;">"</span><span style="color: #000000;">).val())
            })


        })

    </span>&lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
    &lt;input type=<span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span> id=<span style="color: #800000;">"</span><span style="color: #800000;">txt</span><span style="color: #800000;">"</span> /&gt;
    &lt;input type=<span style="color: #800000;">"</span><span style="color: #800000;">button</span><span style="color: #800000;">"</span> id=<span style="color: #800000;">"</span><span style="color: #800000;">send</span><span style="color: #800000;">"</span> value=<span style="color: #800000;">"</span><span style="color: #800000;">发送</span><span style="color: #800000;">"</span>/&gt;
    &lt;div id=<span style="color: #800000;">"</span><span style="color: #800000;">context</span><span style="color: #800000;">"</span>&gt;

    &lt;/div&gt;

&lt;/body&gt;
&lt;/html&gt;</pre>
</div>
<span class="cnblogs_code_collapse">html</span></div>
<p>案例下载：<a href="https://pan.baidu.com/s/1YJN-bwertKNQc2O5JHlQgg" target="_blank">https://pan.baidu.com/s/1YJN-bwertKNQc2O5JHlQgg</a></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">三、Hub</span></strong></p>
<p>1，js调用直接后端方法、后端直接调用js方法</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('064d4060-76b3-4e3c-8e2e-a83fd3ffeb65')"><img id="code_img_closed_064d4060-76b3-4e3c-8e2e-a83fd3ffeb65" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_064d4060-76b3-4e3c-8e2e-a83fd3ffeb65" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('064d4060-76b3-4e3c-8e2e-a83fd3ffeb65',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_064d4060-76b3-4e3c-8e2e-a83fd3ffeb65" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Owin;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Owin;

[assembly: OwinStartup(</span><span style="color: #0000ff;">typeof</span><span style="color: #000000;">(WebApplication1.Startup1))]

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> WebApplication1
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Startup1
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configuration(IAppBuilder app)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> For more information on how to configure your application, visit </span><span style="color: #008000; text-decoration: underline;">https://go.microsoft.com/fwlink/?LinkID=316888</span>
<span style="color: #000000;">            app.MapSignalR();
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Startup1</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('ff633036-d0ab-4641-8212-ac43cb8672ac')"><img id="code_img_closed_ff633036-d0ab-4641-8212-ac43cb8672ac" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_ff633036-d0ab-4641-8212-ac43cb8672ac" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('ff633036-d0ab-4641-8212-ac43cb8672ac',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_ff633036-d0ab-4641-8212-ac43cb8672ac" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Web;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNet.SignalR;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> WebApplication1
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyHub : Hub
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Hello()
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">直接调用前端js方法</span>
            Clients.All.aa(<span style="color: #800000;">"</span><span style="color: #800000;">abc</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Hub</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('bab25402-e658-4c71-bc01-250cdd0bd734')"><img id="code_img_closed_bab25402-e658-4c71-bc01-250cdd0bd734" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_bab25402-e658-4c71-bc01-250cdd0bd734" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('bab25402-e658-4c71-bc01-250cdd0bd734',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_bab25402-e658-4c71-bc01-250cdd0bd734" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">&lt;!</span><span style="color: #ff00ff;">DOCTYPE html</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">html</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">head</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">meta </span><span style="color: #ff0000;">charset</span><span style="color: #0000ff;">="utf-8"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">title</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">title</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="Scripts/jquery-1.6.4.js"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="Scripts/jquery.signalR-2.2.3.js"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>

    <span style="color: #008000;">&lt;!--</span><span style="color: #008000;">引用js</span><span style="color: #008000;">--&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="/signalr/js"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>

    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="text/javascript"</span><span style="color: #0000ff;">&gt;</span><span style="background-color: #f5f5f5; color: #000000;">
        $(</span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;"> () {

            </span><span style="background-color: #f5f5f5; color: #008000;">//</span><span style="background-color: #f5f5f5; color: #008000;">启动hub</span>
<span style="background-color: #f5f5f5; color: #000000;">            $.connection.hub.start()

            </span><span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> conne </span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;"> $.connection.myHub;

            </span><span style="background-color: #f5f5f5; color: #008000;">//</span><span style="background-color: #f5f5f5; color: #008000;">申明客户端js方法</span>
<span style="background-color: #f5f5f5; color: #000000;">            conne.client.aa </span><span style="background-color: #f5f5f5; color: #000000;">=</span> <span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;"> (msg) {
                $(</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">#context</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">).append(</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">&lt;br/&gt;</span><span style="background-color: #f5f5f5; color: #000000;">"</span> <span style="background-color: #f5f5f5; color: #000000;">+</span><span style="background-color: #f5f5f5; color: #000000;"> msg)
            }

            $(</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">#send</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">).click(</span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;"> () {
                </span><span style="background-color: #f5f5f5; color: #008000;">//</span><span style="background-color: #f5f5f5; color: #008000;">直接调用后端方法</span>
<span style="background-color: #f5f5f5; color: #000000;">                conne.server.hello();
            })


        })

    </span><span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">head</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">body</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="text"</span><span style="color: #ff0000;"> id</span><span style="color: #0000ff;">="txt"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="button"</span><span style="color: #ff0000;"> id</span><span style="color: #0000ff;">="send"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">="发送"</span><span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">id</span><span style="color: #0000ff;">="context"</span><span style="color: #0000ff;">&gt;</span>

    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>

<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">body</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">html</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<span class="cnblogs_code_collapse">html</span></div>
<p>2，HubName/HubMethodName</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">using</span> Microsoft.AspNet.SignalR.Hubs;</pre>
</div>
<div class="cnblogs_code" onclick="cnblogs_code_show('8e2eb8e4-10dc-4e02-8e79-7afac716be7c')"><img id="code_img_closed_8e2eb8e4-10dc-4e02-8e79-7afac716be7c" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_8e2eb8e4-10dc-4e02-8e79-7afac716be7c" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('8e2eb8e4-10dc-4e02-8e79-7afac716be7c',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_8e2eb8e4-10dc-4e02-8e79-7afac716be7c" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Web;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNet.SignalR;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNet.SignalR.Hubs;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> WebApplication1
{

    [HubName(</span><span style="color: #800000;">"</span><span style="color: #800000;">MyHub</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyHub : Hub
    {
        [HubMethodName(</span><span style="color: #800000;">"</span><span style="color: #800000;">Hello</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Hello()
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">直接调用前端js方法</span>
            Clients.All.aa(<span style="color: #800000;">"</span><span style="color: #800000;">abc</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">MyHub </span></div>
<p>3，ConnectionId</p>
<div class="cnblogs_code">
<pre> <span style="color: #0000ff;">this</span>.Context.ConnectionId;</pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">四、Hub中的clients 和 groups属性</span></strong></p>
<p>1，Clients</p>
<p>①T All { get; }</p>
<p> 相当于持久连接中的 Broadcast。<br /> </p>
<p>②T AllExcept(params string[] excludeConnectionIds);</p>
<p> 给排除本人所有人发送消息。（excludeConnectionIds排除的连接id）</p>
<p>③T Client(string connectionId);</p>
<p> 跟Send操作就是一样的了。    </p>
<p>④T Clients(IList&lt;string&gt; connectionIds);</p>
<p> 和Send操作的重载方法一样，可以给一批指定的人发送。</p>
<p>⑤T Group(string groupName, params string[] excludeConnectionIds);</p>
<p> 给房间中的指定人发送消息： Clients.Group("room1", "asdfasdfads");</p>
<p>⑥T Groups(IList&lt;string&gt; groupNames, params string[] excludeConnectionIds);</p>
<p> 给房间列表中的指定人发送消息；	【天然的聊天室功能】</p>
<p>⑦T User(string userId);</p>
<p>这个和Client是有区别的。 这个userId =＞　this.Context.Request.User.Identity.Name 【form验证】</p>
<p> cookie中间件来做到singlar的身份验证。</p>
<p>　　userId 是你自己定义的一个标识。</p>
<p>        T Users(IList&lt;string&gt; userIds);</p>
<p>2，Groups</p>
<p>①Task Add(string connectionId, string groupName);</p>
<p>向组内添加链接</p>
<p>②Task Remove(string connectionId, string groupName);</p>
<p>删除组内的连接</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">五、GlobalHost</span></strong></p>
<p>1，获取Hub的上下文</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> hub = GlobalHost.ConnectionManager.GetHubContext&lt;MyHub&gt;();</pre>
</div>
<p>2，对singlar的全局设置</p>
<p>GlobalHost.Configuration.MaxIncomingWebSocketMessageSize：<br />websocket模式下，消息的传输大小，如果大于默认的64k，那么就会出问题。</p>
<p>GlobalHost.Configuration.DisconnectTimeout：<br />websocket强制关闭的时间。  30 seconds</p>
<p>GlobalHost.Configuration.TransportConnectTimeout：<br /> 传输的超时时间。  5s</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">六、生成代理js</span></strong></p>
<p>下载安装nuget：&nbsp;<span class="cnblogs_code">Microsoft.AspNet.SignalR.Utils</span>&nbsp;</p>
<p>1，模板：signalr.exe ghp /path:《..\bin》 /o:《..\hub.js》<br />2，案例：<br />C:\Users\Hunter\Desktop\ConsoleApp3\packages\Microsoft.AspNet.SignalR.Utils.2.2.3\tools&gt;signalr.exe ghp /path:C:\Users\Hunter\Desktop\ConsoleApp3\WebApplication2\bin /o:C:\Users\Hunter\Desktop\ConsoleApp3\WebApplication2\Scripts\hub.js<br />3，编译命令：<br />$(SolutionDir)packages\Microsoft.AspNet.SignalR.Utils.2.2.3\tools\signalr.exe ghp /path:$(SolutionDir)$(ProjectName)\$(OutDir) /o:$(SolutionDir)$(ProjectName)\Scripts\hub.js</p>
<p>4，替换代理js</p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201804/741594-20180429161625606-1550388206.png" alt="" /></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">七、支持跨域</span></strong></p>
<p>①下载安装nuget：&nbsp;<span class="cnblogs_code">Microsoft.Owin.Cors</span>&nbsp;</p>
<p>②配置项</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('23e21a0a-6be6-4556-a275-d4482b22ef2a')"><img id="code_img_closed_23e21a0a-6be6-4556-a275-d4482b22ef2a" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_23e21a0a-6be6-4556-a275-d4482b22ef2a" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('23e21a0a-6be6-4556-a275-d4482b22ef2a',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_23e21a0a-6be6-4556-a275-d4482b22ef2a" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Owin;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Owin;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNet.SignalR;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Owin.Cors;

[assembly: OwinStartup(</span><span style="color: #0000ff;">typeof</span><span style="color: #000000;">(WebApplication2.Startup))]

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> WebApplication2
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Startup
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configuration(IAppBuilder app)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> For more information on how to configure your application, visit </span><span style="color: #008000; text-decoration: underline;">https://go.microsoft.com/fwlink/?LinkID=316888</span>
<span style="color: #000000;">           
            app.UseCors(CorsOptions.AllowAll);
            app.MapSignalR();
          
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Startup</span></div>
<p>③生成代理js</p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201805/741594-20180502094515980-1648076390.png" alt="" /></p>
<p>④修改代理js</p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201805/741594-20180502094543144-386905217.png" alt="" width="688" height="197" /></p>
<p>⑤html</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('eb36a48a-817b-49fc-86c9-4bbf0c93e000')"><img id="code_img_closed_eb36a48a-817b-49fc-86c9-4bbf0c93e000" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_eb36a48a-817b-49fc-86c9-4bbf0c93e000" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('eb36a48a-817b-49fc-86c9-4bbf0c93e000',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_eb36a48a-817b-49fc-86c9-4bbf0c93e000" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">&lt;!</span><span style="color: #ff00ff;">DOCTYPE html</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">html</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">head</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">meta </span><span style="color: #ff0000;">charset</span><span style="color: #0000ff;">="utf-8"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">title</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">title</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="Scripts/jquery-1.6.4.js"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="Scripts/jquery.signalR-2.2.3.js"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>

    <span style="color: #008000;">&lt;!--</span><span style="color: #008000;">引用js</span><span style="color: #008000;">--&gt;</span>
    <span style="color: #008000;">&lt;!--</span><span style="color: #008000;">&lt;script src="/signalr/js"&gt;&lt;/script&gt;</span><span style="color: #008000;">--&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="Scripts/hub.js"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="text/javascript"</span><span style="color: #0000ff;">&gt;</span><span style="background-color: #f5f5f5; color: #000000;">
        $(</span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;"> () {

            </span><span style="background-color: #f5f5f5; color: #008000;">//</span><span style="background-color: #f5f5f5; color: #008000;">启动hub</span>
<span style="background-color: #f5f5f5; color: #000000;">            $.connection.hub.start()

            </span><span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> conne </span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;"> $.connection.myHub;

            </span><span style="background-color: #f5f5f5; color: #008000;">//</span><span style="background-color: #f5f5f5; color: #008000;">申明客户端js方法</span>
<span style="background-color: #f5f5f5; color: #000000;">            conne.client.aa </span><span style="background-color: #f5f5f5; color: #000000;">=</span> <span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;"> (msg) {
                $(</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">#context</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">).append(</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">&lt;br/&gt;</span><span style="background-color: #f5f5f5; color: #000000;">"</span> <span style="background-color: #f5f5f5; color: #000000;">+</span><span style="background-color: #f5f5f5; color: #000000;"> msg)
            }

            $(</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">#send</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">).click(</span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;"> () {
                </span><span style="background-color: #f5f5f5; color: #008000;">//</span><span style="background-color: #f5f5f5; color: #008000;">直接调用后端方法</span>
<span style="background-color: #f5f5f5; color: #000000;">                conne.server.hello();
            })


        })

    </span><span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">head</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">body</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="text"</span><span style="color: #ff0000;"> id</span><span style="color: #0000ff;">="txt"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="button"</span><span style="color: #ff0000;"> id</span><span style="color: #0000ff;">="send"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">="发送"</span><span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">id</span><span style="color: #0000ff;">="context"</span><span style="color: #0000ff;">&gt;</span>

    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>

<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">body</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">html</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<span class="cnblogs_code_collapse">html</span></div>
<p>案例下载：<a href="https://pan.baidu.com/s/1GY_Io63qZeECbGbEH589fg" target="_blank">https://pan.baidu.com/s/1GY_Io63qZeECbGbEH589fg</a></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">八、集群部署</span></strong></p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201805/741594-20180502182857510-827290422.png" alt="" /></p>
<p>使用redis：</p>
<p>nuget：&nbsp;<span class="cnblogs_code">Microsoft.AspNet.SignalR.Redis</span>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('09219585-78d8-40d1-b4d1-53a6d3b4bc2c')"><img id="code_img_closed_09219585-78d8-40d1-b4d1-53a6d3b4bc2c" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_09219585-78d8-40d1-b4d1-53a6d3b4bc2c" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('09219585-78d8-40d1-b4d1-53a6d3b4bc2c',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_09219585-78d8-40d1-b4d1-53a6d3b4bc2c" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Owin;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Owin;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNet.SignalR;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Owin.Cors;

[assembly: OwinStartup(</span><span style="color: #0000ff;">typeof</span><span style="color: #000000;">(WebApplication2.Startup))]

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> WebApplication2
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Startup
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configuration(IAppBuilder app)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> For more information on how to configure your application, visit </span><span style="color: #008000; text-decoration: underline;">https://go.microsoft.com/fwlink/?LinkID=316888</span>
            <span style="color: #008000;">//</span><span style="color: #008000;">使用redis做底板</span>
            GlobalHost.DependencyResolver.UseRedis(<span style="color: #800000;">"</span><span style="color: #800000;">localhost</span><span style="color: #800000;">"</span>, <span style="color: #800080;">6379</span>,<span style="color: #0000ff;">string</span>.Empty, <span style="color: #800000;">"</span><span style="color: #800000;">mykey</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            app.UseCors(CorsOptions.AllowAll);
            app.MapSignalR();
          
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Startup</span></div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">九、将singlar.exe 装入到 性能监视器</span></strong></p>
<p>signlar.exe ipc 命令来安装性能监视器 [install performance counters]</p>
<p>signlar.exe upc 来卸载性能监视器 [uninstall performance counters]</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">十、HubPipeLine管道</span></strong></p>
<p>实现：IHubPipelineModule</p>
<p>①入流： BuildIncoming 监控</p>
<p>②出流： BuildOutgoing 监控</p>
<p>&nbsp;</p>