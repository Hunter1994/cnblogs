<p>一、asp.net core使用signalR入门</p>
<p>1，nuget&nbsp;<span class="cnblogs_code">Microsoft.AspNetCore.SignalR</span>&nbsp;</p>
<p>2，新建ChatHub文件</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('e861ccdc-c07e-41b1-b7e9-043505bca364')"><img id="code_img_closed_e861ccdc-c07e-41b1-b7e9-043505bca364" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_e861ccdc-c07e-41b1-b7e9-043505bca364" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('e861ccdc-c07e-41b1-b7e9-043505bca364',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_e861ccdc-c07e-41b1-b7e9-043505bca364" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.SignalR;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> SignalRDemo
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ChatHub:Hub
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task SendMessage(<span style="color: #0000ff;">string</span> user,<span style="color: #0000ff;">string</span><span style="color: #000000;"> message)
        {
            </span><span style="color: #0000ff;">await</span> Clients.All.SendAsync(<span style="color: #800000;">"</span><span style="color: #800000;">ReceiveMessage</span><span style="color: #800000;">"</span><span style="color: #000000;">,user,message);
        }
        
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">ChatHub</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('a7404229-d795-4f4b-92c7-e9fce24fa07f')"><img id="code_img_closed_a7404229-d795-4f4b-92c7-e9fce24fa07f" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_a7404229-d795-4f4b-92c7-e9fce24fa07f" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('a7404229-d795-4f4b-92c7-e9fce24fa07f',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_a7404229-d795-4f4b-92c7-e9fce24fa07f" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Builder;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Hosting;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Configuration;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.DependencyInjection;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.SignalR;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> SignalRDemo
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Startup
    {
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Startup(IConfiguration configuration)
        {
            Configuration </span>=<span style="color: #000000;"> configuration;
        }

        </span><span style="color: #0000ff;">public</span> IConfiguration Configuration { <span style="color: #0000ff;">get</span><span style="color: #000000;">; }

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> This method gets called by the runtime. Use this method to add services to the container.</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> ConfigureServices(IServiceCollection services)
        {
            services.AddMvc();

          
            services.AddSignalR();
        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> This method gets called by the runtime. Use this method to configure the HTTP request pipeline.</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configure(IApplicationBuilder app, IHostingEnvironment env)
        {
            </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (env.IsDevelopment())
            {
                app.UseDeveloperExceptionPage();
            }
            </span><span style="color: #0000ff;">else</span><span style="color: #000000;">
            {
                app.UseExceptionHandler(</span><span style="color: #800000;">"</span><span style="color: #800000;">/Home/Error</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }

            app.UseStaticFiles();


          
            app.UseSignalR(routes</span>=&gt;<span style="color: #000000;">{
                routes.MapHub</span>&lt;ChatHub&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">/chathub</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            });
        
            app.UseMvc(routes </span>=&gt;<span style="color: #000000;">
            {
                routes.MapRoute(
                    name: </span><span style="color: #800000;">"</span><span style="color: #800000;">default</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    template: </span><span style="color: #800000;">"</span><span style="color: #800000;">{controller=Home}/{action=Index}/{id?}</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            });
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">配置Startup</span></div>
<p>3，生成signalr.js文件</p>
<p>使用npm下载signalr&nbsp;<span class="cnblogs_code">D:\signalr&gt; npm install @aspnet/signalr</span>&nbsp;</p>
<p>将&nbsp;<span class="cnblogs_code">D:\signalr\node_modules\@aspnet\signalr\dist\browser\signalr.js</span>&nbsp;拷贝到项目中&nbsp;<span class="cnblogs_code">SignalRDemo\wwwroot\lib\signalr\signalr.js</span>&nbsp;</p>
<p>4，在视图页面使用</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('e59c87b8-3a82-4d4b-8980-11ae0bb907be')"><img id="code_img_closed_e59c87b8-3a82-4d4b-8980-11ae0bb907be" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_e59c87b8-3a82-4d4b-8980-11ae0bb907be" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('e59c87b8-3a82-4d4b-8980-11ae0bb907be',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_e59c87b8-3a82-4d4b-8980-11ae0bb907be" class="cnblogs_code_hide">
<pre><span style="color: #000000;">@{
    ViewData[</span><span style="color: #800000;">"</span><span style="color: #800000;">Title</span><span style="color: #800000;">"</span>] = <span style="color: #800000;">"</span><span style="color: #800000;">Home Page</span><span style="color: #800000;">"</span><span style="color: #000000;">;
}


</span>&lt;input type=<span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span> name=<span style="color: #800000;">""</span> id=<span style="color: #800000;">"</span><span style="color: #800000;">message</span><span style="color: #800000;">"</span> <span style="color: #0000ff;">class</span>=<span style="color: #800000;">"</span><span style="color: #800000;">form-control</span><span style="color: #800000;">"</span> value=<span style="color: #800000;">""</span> required=<span style="color: #800000;">"</span><span style="color: #800000;">required</span><span style="color: #800000;">"</span> pattern=<span style="color: #800000;">""</span> title=<span style="color: #800000;">""</span>&gt;

&lt;button type=<span style="color: #800000;">"</span><span style="color: #800000;">button</span><span style="color: #800000;">"</span> <span style="color: #0000ff;">class</span>=<span style="color: #800000;">"</span><span style="color: #800000;">btn btn-default</span><span style="color: #800000;">"</span> id=<span style="color: #800000;">"</span><span style="color: #800000;">send</span><span style="color: #800000;">"</span> &gt;发送&lt;/button&gt;


&lt;div id=<span style="color: #800000;">"</span><span style="color: #800000;">content</span><span style="color: #800000;">"</span>&gt;&lt;/div&gt;<span style="color: #000000;">

@section Scripts{

    </span>&lt;script src=<span style="color: #800000;">"</span><span style="color: #800000;">~/lib/signalr/signalr.js</span><span style="color: #800000;">"</span>&gt;&lt;/script&gt;
    &lt;script&gt;
        <span style="color: #0000ff;">const</span> connection=<span style="color: #0000ff;">new</span><span style="color: #000000;"> signalR.HubConnectionBuilder()
                            .withUrl(</span><span style="color: #800000;">"</span><span style="color: #800000;">/chatHub</span><span style="color: #800000;">"</span><span style="color: #000000;">)
                            .build();

        connection.on(</span><span style="color: #800000;">"</span><span style="color: #800000;">ReceiveMessage</span><span style="color: #800000;">"</span>,(use,message)=&gt;<span style="color: #000000;">{
            $(</span><span style="color: #800000;">"</span><span style="color: #800000;">#content</span><span style="color: #800000;">"</span>).append(message+<span style="color: #800000;">"</span><span style="color: #800000;">&lt;br/&gt;</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        });

        connection.start().</span><span style="color: #0000ff;">catch</span>(err=&gt;<span style="color: #000000;">{alert(err)});

        $(</span><span style="color: #800000;">"</span><span style="color: #800000;">#send</span><span style="color: #800000;">"</span><span style="color: #000000;">).click(function(){
            </span><span style="color: #0000ff;">var</span> msg= $(<span style="color: #800000;">"</span><span style="color: #800000;">#message</span><span style="color: #800000;">"</span><span style="color: #000000;">).val();
            connection.invoke(</span><span style="color: #800000;">"</span><span style="color: #800000;">SendMessage</span><span style="color: #800000;">"</span>,<span style="color: #800000;">""</span>,msg).<span style="color: #0000ff;">catch</span>(err=&gt;<span style="color: #000000;">{alert(err)})
        });

</span>&lt;/script&gt;<span style="color: #000000;">
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Index.cshtml</span></div>
<p>&nbsp;案例下载：<a href="https://pan.baidu.com/s/1FEgPEbPZOribtYnLv-XCNQ" target="_blank">https://pan.baidu.com/s/1FEgPEbPZOribtYnLv-XCNQ</a></p>
<p>&nbsp;</p>
<p>二、前后端分离模式</p>
<p>1，前端代码</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('30f2fad2-bde9-4087-af37-4deee7adb5cc')"><img id="code_img_closed_30f2fad2-bde9-4087-af37-4deee7adb5cc" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_30f2fad2-bde9-4087-af37-4deee7adb5cc" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('30f2fad2-bde9-4087-af37-4deee7adb5cc',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_30f2fad2-bde9-4087-af37-4deee7adb5cc" class="cnblogs_code_hide">
<pre>&lt;html&gt;
&lt;head&gt;
&lt;title&gt;&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;


&lt;input type=<span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span> name=<span style="color: #800000;">""</span> id=<span style="color: #800000;">"</span><span style="color: #800000;">message</span><span style="color: #800000;">"</span> <span style="color: #0000ff;">class</span>=<span style="color: #800000;">"</span><span style="color: #800000;">form-control</span><span style="color: #800000;">"</span> value=<span style="color: #800000;">""</span> required=<span style="color: #800000;">"</span><span style="color: #800000;">required</span><span style="color: #800000;">"</span> pattern=<span style="color: #800000;">""</span> title=<span style="color: #800000;">""</span>&gt;

&lt;button type=<span style="color: #800000;">"</span><span style="color: #800000;">button</span><span style="color: #800000;">"</span> <span style="color: #0000ff;">class</span>=<span style="color: #800000;">"</span><span style="color: #800000;">btn btn-default</span><span style="color: #800000;">"</span> id=<span style="color: #800000;">"</span><span style="color: #800000;">send</span><span style="color: #800000;">"</span> &gt;发送&lt;/button&gt;


&lt;div id=<span style="color: #800000;">"</span><span style="color: #800000;">content</span><span style="color: #800000;">"</span>&gt;&lt;/div&gt;


&lt;script src=<span style="color: #800000;">"</span><span style="color: #800000;">js/jquery.js</span><span style="color: #800000;">"</span> &gt;&lt;/script&gt;
&lt;script src=<span style="color: #800000;">"</span><span style="color: #800000;">js/signalr.js</span><span style="color: #800000;">"</span>&gt;&lt;/script&gt;
&lt;script&gt;
    <span style="color: #0000ff;">const</span> connection=<span style="color: #0000ff;">new</span><span style="color: #000000;"> signalR.HubConnectionBuilder()
                            .withUrl(</span><span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:5000/chatHub</span><span style="color: #800000;">"</span><span style="color: #000000;">)
                            .build();

        connection.on(</span><span style="color: #800000;">"</span><span style="color: #800000;">ReceiveMessage</span><span style="color: #800000;">"</span>,(use,message)=&gt;<span style="color: #000000;">{
            $(</span><span style="color: #800000;">"</span><span style="color: #800000;">#content</span><span style="color: #800000;">"</span>).append(message+<span style="color: #800000;">"</span><span style="color: #800000;">&lt;br/&gt;</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        });

        connection.start().</span><span style="color: #0000ff;">catch</span>(err=&gt;<span style="color: #000000;">{alert(err)});

        $(</span><span style="color: #800000;">"</span><span style="color: #800000;">#send</span><span style="color: #800000;">"</span><span style="color: #000000;">).click(function(){
            </span><span style="color: #0000ff;">var</span> msg= $(<span style="color: #800000;">"</span><span style="color: #800000;">#message</span><span style="color: #800000;">"</span><span style="color: #000000;">).val();
            connection.invoke(</span><span style="color: #800000;">"</span><span style="color: #800000;">SendMessage</span><span style="color: #800000;">"</span>,<span style="color: #800000;">""</span>,msg).<span style="color: #0000ff;">catch</span>(err=&gt;<span style="color: #000000;">{alert(err)})
        });
</span>&lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;</pre>
</div>
<span class="cnblogs_code_collapse">index.html</span></div>
<p>使用npm下载signalr</p>
<p>2，后端需要配置cors</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('ccdc3ec0-2685-4e02-8032-91a98943380e')"><img id="code_img_closed_ccdc3ec0-2685-4e02-8032-91a98943380e" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_ccdc3ec0-2685-4e02-8032-91a98943380e" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('ccdc3ec0-2685-4e02-8032-91a98943380e',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_ccdc3ec0-2685-4e02-8032-91a98943380e" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Builder;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Hosting;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Configuration;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.DependencyInjection;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.SignalR;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> SignalRDemo
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Startup
    {
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Startup(IConfiguration configuration)
        {
            Configuration </span>=<span style="color: #000000;"> configuration;
        }

        </span><span style="color: #0000ff;">public</span> IConfiguration Configuration { <span style="color: #0000ff;">get</span><span style="color: #000000;">; }

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> This method gets called by the runtime. Use this method to add services to the container.</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> ConfigureServices(IServiceCollection services)
        {
            services.AddMvc();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">注册Cors的策略</span>
            services.AddCors(options=&gt;options.AddPolicy(<span style="color: #800000;">"</span><span style="color: #800000;">CorsPolicy</span><span style="color: #800000;">"</span>,builder=&gt;<span style="color: #000000;">{
                builder.AllowAnyMethod()
                       .AllowAnyHeader()
                       .AllowAnyOrigin()
                       .AllowCredentials();
            }));

            services.AddSignalR();
        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> This method gets called by the runtime. Use this method to configure the HTTP request pipeline.</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configure(IApplicationBuilder app, IHostingEnvironment env)
        {
            </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (env.IsDevelopment())
            {
                app.UseDeveloperExceptionPage();
            }
            </span><span style="color: #0000ff;">else</span><span style="color: #000000;">
            {
                app.UseExceptionHandler(</span><span style="color: #800000;">"</span><span style="color: #800000;">/Home/Error</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }

            app.UseStaticFiles();


            </span><span style="color: #008000;">//</span><span style="color: #008000;">使用CorsPolicy策略的Cors</span>
            app.UseCors(<span style="color: #800000;">"</span><span style="color: #800000;">CorsPolicy</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            app.UseSignalR(routes</span>=&gt;<span style="color: #000000;">{
                routes.MapHub</span>&lt;ChatHub&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">/chathub</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            });
        
            app.UseMvc(routes </span>=&gt;<span style="color: #000000;">
            {
                routes.MapRoute(
                    name: </span><span style="color: #800000;">"</span><span style="color: #800000;">default</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    template: </span><span style="color: #800000;">"</span><span style="color: #800000;">{controller=Home}/{action=Index}/{id?}</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            });
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Startup</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('8b6c2c57-1534-4797-934c-ee5081a60f00')"><img id="code_img_closed_8b6c2c57-1534-4797-934c-ee5081a60f00" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_8b6c2c57-1534-4797-934c-ee5081a60f00" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('8b6c2c57-1534-4797-934c-ee5081a60f00',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_8b6c2c57-1534-4797-934c-ee5081a60f00" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.SignalR;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> SignalRDemo
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ChatHub:Hub
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task SendMessage(<span style="color: #0000ff;">string</span> user,<span style="color: #0000ff;">string</span><span style="color: #000000;"> message)
        {
            </span><span style="color: #0000ff;">await</span> Clients.All.SendAsync(<span style="color: #800000;">"</span><span style="color: #800000;">ReceiveMessage</span><span style="color: #800000;">"</span><span style="color: #000000;">,user,message);
        }
        
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">ChatHub</span></div>
<p>案例下载：<a href="https://pan.baidu.com/s/1qcYOKuO42HltFmwP3vZgSA">https://pan.baidu.com/s/1qcYOKuO42HltFmwP3vZgSA&nbsp;</a></p>
<p>&nbsp;</p>
<p>三、Hub</p>
<p>1，创建并使用Hub</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('9603fa42-2b81-4f98-b0f6-726d1f685c2e')"><img id="code_img_closed_9603fa42-2b81-4f98-b0f6-726d1f685c2e" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_9603fa42-2b81-4f98-b0f6-726d1f685c2e" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('9603fa42-2b81-4f98-b0f6-726d1f685c2e',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_9603fa42-2b81-4f98-b0f6-726d1f685c2e" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ChatHub : Hub
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task SendMessage(<span style="color: #0000ff;">string</span> user, <span style="color: #0000ff;">string</span><span style="color: #000000;"> message)
    {
        </span><span style="color: #0000ff;">await</span> Clients.All.SendAsync(<span style="color: #800000;">"</span><span style="color: #800000;">ReceiveMessage</span><span style="color: #800000;">"</span><span style="color: #000000;">, user,message);
    }

    </span><span style="color: #0000ff;">public</span> Task SendMessageToCaller(<span style="color: #0000ff;">string</span><span style="color: #000000;"> message)
    {
        </span><span style="color: #0000ff;">return</span> Clients.Caller.SendAsync(<span style="color: #800000;">"</span><span style="color: #800000;">ReceiveMessage</span><span style="color: #800000;">"</span><span style="color: #000000;">, message);
    }

    </span><span style="color: #0000ff;">public</span> Task SendMessageToGroups(<span style="color: #0000ff;">string</span><span style="color: #000000;"> message)
    {
        List</span>&lt;<span style="color: #0000ff;">string</span>&gt; groups = <span style="color: #0000ff;">new</span> List&lt;<span style="color: #0000ff;">string</span>&gt;() { <span style="color: #800000;">"</span><span style="color: #800000;">SignalR Users</span><span style="color: #800000;">"</span><span style="color: #000000;"> };
        </span><span style="color: #0000ff;">return</span> Clients.Groups(groups).SendAsync(<span style="color: #800000;">"</span><span style="color: #800000;">ReceiveMessage</span><span style="color: #800000;">"</span><span style="color: #000000;">, message);
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">async</span><span style="color: #000000;"> Task OnConnectedAsync()
    {
        </span><span style="color: #0000ff;">await</span> Groups.AddToGroupAsync(Context.ConnectionId, <span style="color: #800000;">"</span><span style="color: #800000;">SignalR Users</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        </span><span style="color: #0000ff;">await</span> <span style="color: #0000ff;">base</span><span style="color: #000000;">.OnConnectedAsync();
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">async</span><span style="color: #000000;"> Task OnDisconnectedAsync(Exception exception)
    {
        </span><span style="color: #0000ff;">await</span> Groups.RemoveFromGroupAsync(Context.ConnectionId, <span style="color: #800000;">"</span><span style="color: #800000;">SignalR Users</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        </span><span style="color: #0000ff;">await</span> <span style="color: #0000ff;">base</span><span style="color: #000000;">.OnDisconnectedAsync(exception);
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Hub</span></div>
<p>2，Clients对象</p>
<p>①每个实例<code>Hub</code>类有一个名为<code>Clients</code>包含服务器和客户端之间通信的以下成员：</p>
<table border="1">
<thead>
<tr><th><span data-ttu-id="5dad2-121">属性</span></th><th><span data-ttu-id="5dad2-122">描述</span></th></tr>
</thead>
<tbody>
<tr>
<td><code>All</code></td>
<td><span data-ttu-id="5dad2-123">在所有连接的客户端上调用方法</span></td>
</tr>
<tr>
<td><code>Caller</code></td>
<td><span data-ttu-id="5dad2-124">调用 hub 方法在客户端上调用方法</span></td>
</tr>
<tr>
<td><code>Others</code></td>
<td><span data-ttu-id="5dad2-125">除调用的方法的客户端的所有连接客户端上调用方法</span></td>
</tr>
</tbody>
</table>
<p>此外，<code>Hub.Clients</code>包含以下方法：</p>
<table border="1">
<thead>
<tr><th><span data-ttu-id="5dad2-127">方法</span></th><th><span data-ttu-id="5dad2-128">描述</span></th></tr>
</thead>
<tbody>
<tr>
<td><code>AllExcept</code></td>
<td><span data-ttu-id="5dad2-129">在指定的连接除外的所有连接的客户端上调用方法</span></td>
</tr>
<tr>
<td><code>Client</code></td>
<td><span data-ttu-id="5dad2-130">在特定连接的客户端上调用方法</span></td>
</tr>
<tr>
<td><code>Clients</code></td>
<td><span data-ttu-id="5dad2-131">在特定连接的客户端上调用方法</span></td>
</tr>
<tr>
<td><code>Group</code></td>
<td><span data-ttu-id="5dad2-132">将消息发送到指定的组中的所有连接</span></td>
</tr>
<tr>
<td><code>GroupExcept</code></td>
<td><span data-ttu-id="5dad2-133">将消息发送到指定的组，除非指定连接中的所有连接</span></td>
</tr>
<tr>
<td><code>Groups</code></td>
<td><span data-ttu-id="5dad2-134">将一条消息发送到多个组的连接</span></td>
</tr>
<tr>
<td><code>OthersInGroup</code></td>
<td><span data-ttu-id="5dad2-135">将一条消息发送到一组的连接，不包括客户端调用 hub 方法</span></td>
</tr>
<tr>
<td><code>User</code></td>
<td><span data-ttu-id="5dad2-136">将消息发送到与特定用户关联的所有连接</span></td>
</tr>
<tr>
<td><code>Users</code></td>
<td><span data-ttu-id="5dad2-137">将消息发送到与指定的用户相关联的所有连接</span></td>
</tr>
</tbody>
</table>
<p>3，将消息发送到客户端</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">将消息发送到调用此hub的客户端</span>
<span style="color: #0000ff;">public</span> Task SendMessageToCaller(<span style="color: #0000ff;">string</span><span style="color: #000000;"> message)
{
    </span><span style="color: #0000ff;">return</span> Clients.Caller.SendAsync(<span style="color: #800000;">"</span><span style="color: #800000;">ReceiveMessage</span><span style="color: #800000;">"</span><span style="color: #000000;">, message);
}
</span><span style="color: #008000;">//</span><span style="color: #008000;">将消息发送到指定发送的所有客户端</span>
<span style="color: #0000ff;">public</span> Task SendMessageToGroups(<span style="color: #0000ff;">string</span><span style="color: #000000;"> message)
{
    List</span>&lt;<span style="color: #0000ff;">string</span>&gt; groups = <span style="color: #0000ff;">new</span> List&lt;<span style="color: #0000ff;">string</span>&gt;() { <span style="color: #800000;">"</span><span style="color: #800000;">SignalR Users</span><span style="color: #800000;">"</span><span style="color: #000000;"> };
    </span><span style="color: #0000ff;">return</span> Clients.Groups(groups).SendAsync(<span style="color: #800000;">"</span><span style="color: #800000;">ReceiveMessage</span><span style="color: #800000;">"</span><span style="color: #000000;">, message);
}</span></pre>
</div>
<p>4，处理消息事件</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">连接触发</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">async</span><span style="color: #000000;"> Task OnConnectedAsync()
{
    </span><span style="color: #0000ff;">await</span> Groups.AddToGroupAsync(Context.ConnectionId, <span style="color: #800000;">"</span><span style="color: #800000;">SignalR Users</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    </span><span style="color: #0000ff;">await</span> <span style="color: #0000ff;">base</span><span style="color: #000000;">.OnConnectedAsync();
}
</span><span style="color: #008000;">//</span><span style="color: #008000;">断开连接触发</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">async</span><span style="color: #000000;"> Task OnDisconnectedAsync(Exception exception)
{
    </span><span style="color: #0000ff;">await</span> Groups.RemoveFromGroupAsync(Context.ConnectionId, <span style="color: #800000;">"</span><span style="color: #800000;">SignalR Users</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    </span><span style="color: #0000ff;">await</span> <span style="color: #0000ff;">base</span><span style="color: #000000;">.OnDisconnectedAsync(exception);
}</span></pre>
</div>
<p>5，客户端处理错误</p>
<div class="cnblogs_code">
<pre>connection.invoke(<span style="color: #800000;">"</span><span style="color: #800000;">SendMessage</span><span style="color: #800000;">"</span>, user, message).<span style="color: #0000ff;">catch</span>(err =&gt; console.error(err));</pre>
</div>
<p>&nbsp;</p>
<p>四、客户端调用hub</p>
<p>nuget&nbsp;<span class="cnblogs_code">Microsoft.AspNetCore.SignalR.Client</span>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('c716cced-c426-4665-8620-5205e74bc6c3')"><img id="code_img_closed_c716cced-c426-4665-8620-5205e74bc6c3" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_c716cced-c426-4665-8620-5205e74bc6c3" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('c716cced-c426-4665-8620-5205e74bc6c3',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_c716cced-c426-4665-8620-5205e74bc6c3" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.SignalR.Client;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> SignalRClient
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">准备就绪...</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            HubConnection connection</span>=<span style="color: #0000ff;">new</span><span style="color: #000000;"> HubConnectionBuilder()
                            .WithUrl(</span><span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:5000/chatHub</span><span style="color: #800000;">"</span><span style="color: #000000;">)
                            .Build();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">连接hub</span>
<span style="color: #000000;">            connection.StartAsync();
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">已连接</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            
            </span><span style="color: #008000;">//</span><span style="color: #008000;">定义一个客户端方法ReceiveMessage</span>
            connection.On&lt;<span style="color: #0000ff;">string</span>,<span style="color: #0000ff;">string</span>&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">ReceiveMessage</span><span style="color: #800000;">"</span>,(UriParser,message)=&gt;<span style="color: #000000;">{
                Console.WriteLine($</span><span style="color: #800000;">"</span><span style="color: #800000;">接收消息：{message}</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            });

            </span><span style="color: #0000ff;">while</span>(<span style="color: #0000ff;">true</span><span style="color: #000000;">)
            {
                Thread.Sleep(</span><span style="color: #800080;">1000</span><span style="color: #000000;">);
                </span><span style="color: #0000ff;">var</span> msg=<span style="color: #000000;">Console.ReadLine();
                </span><span style="color: #008000;">//</span><span style="color: #008000;">发送给hub的SendMessage方法</span>
                connection.InvokeAsync(<span style="color: #800000;">"</span><span style="color: #800000;">SendMessage</span><span style="color: #800000;">"</span>,<span style="color: #800000;">""</span><span style="color: #000000;">,msg);
            }

        }
    }

}</span></pre>
</div>
<span class="cnblogs_code_collapse">Main</span></div>
<p>案例下载：<a href="https://pan.baidu.com/s/1gqGNl_FPXxz0LYVozrqI5g" target="_blank">https://pan.baidu.com/s/1gqGNl_FPXxz0LYVozrqI5g</a></p>
<p>&nbsp;</p>