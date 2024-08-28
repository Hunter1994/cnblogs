<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">一、基础层搭建</span></strong></span></p>
<p>1，创建一个空解决方案&nbsp;</p>
<p>2，层结构</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201709/741594-20170915104832047-1406655887.png" alt="" /></p>
<p>Demo.Core[v:4.6.1]：类库</p>
<p>Demo.EntityFramework[v:4.6.1]：类库（引用Demo.Core）</p>
<p>Demo.Application[v:4.6.1]：类库（引用Demo.Core）</p>
<p>Demo.WebApi[v:4.6.1]：类库（引用Demo.Application）</p>
<p>Demo.Web[v:4.6.1]：WebMvc5.X（引用Demo.Core、Demo.EntityFramework、Demo.Application、Demo.WebApi）</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">二、Demo.Core</span></strong></span></p>
<p>&nbsp;1，NuGet安装Abp2.1.3</p>
<p>&nbsp;2，添加Module类</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> Demo.Core
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> DemoCoreModule:AbpModule
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Initialize()
        {
            IocManager.RegisterAssemblyByConvention(Assembly.GetExecutingAssembly());
        }
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;"><strong>三、Demo.EntityFramework</strong></span></p>
<p>&nbsp;1，NuGet安装Abp.EntityFramework2.1.3</p>
<p>&nbsp;2，添加Module类</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> Demo.EntityFramework
{
    [DependsOn(</span><span style="color: #0000ff;">typeof</span>(AbpEntityFrameworkModule),<span style="color: #0000ff;">typeof</span><span style="color: #000000;">(DemoCoreModule))]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> DemoDataModule:AbpModule
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Initialize()
        {
            IocManager.RegisterAssemblyByConvention(Assembly.GetExecutingAssembly());
        }
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">&nbsp;四、Demo.Application</span></strong></span></p>
<p>&nbsp;1，NuGet安装Abp.AutoMapper2.1.3</p>
<p>&nbsp;2，添加Module类</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> Demo.Application
{
    [DependsOn(</span><span style="color: #0000ff;">typeof</span>(AbpAutoMapperModule), <span style="color: #0000ff;">typeof</span><span style="color: #000000;">(DemoCoreModule))]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> DemoApplicationModule:AbpModule
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Initialize()
        {
            IocManager.RegisterAssemblyByConvention(Assembly.GetExecutingAssembly());
        }
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">五、Demo.WebApi</span></strong></span></p>
<p>&nbsp;1，NuGet安装Abp.Web.Api2.1.3</p>
<p>&nbsp;2，添加Module类</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> Demo.WebApi
{
    [DependsOn(</span><span style="color: #0000ff;">typeof</span>(AbpWebApiModule),<span style="color: #0000ff;">typeof</span><span style="color: #000000;">(DemoApplicationModule))]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> DemoWebApiModule:AbpModule
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Initialize()
        {
            IocManager.RegisterAssemblyByConvention(Assembly.GetExecutingAssembly());

            Configuration.Modules.AbpWebApi().DynamicApiControllerBuilder.ForAll</span>&lt;IApplicationService&gt;(<span style="color: #0000ff;">typeof</span>(DemoApplicationModule).Assembly,<span style="color: #800000;">"</span><span style="color: #800000;">app</span><span style="color: #800000;">"</span><span style="color: #000000;">).Build();
        }
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">六、Demo.Web</span></strong></span></p>
<p>&nbsp;1，NuGet安装</p>
<p>Abp.Web.Mvc2.1.3</p>
<p>Abp.Web.Api2.1.3</p>
<p>&nbsp;2，添加Module类</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> Demo.Web.App_Start
{

    [DependsOn(</span><span style="color: #0000ff;">typeof</span>(AbpWebMvcModule), <span style="color: #0000ff;">typeof</span>(DemoWebApiModule), <span style="color: #0000ff;">typeof</span><span style="color: #000000;">(DemoDataModule))]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> DemoWebModule:AbpModule
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Initialize()
        {
            IocManager.RegisterAssemblyByConvention(Assembly.GetExecutingAssembly());
            AreaRegistration.RegisterAllAreas();
            FilterConfig.RegisterGlobalFilters(GlobalFilters.Filters);
            RouteConfig.RegisterRoutes(RouteTable.Routes);
            BundleConfig.RegisterBundles(BundleTable.Bundles);
        }
    }
}</span></pre>
</div>
<p>3，修改Global.asax类</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> Demo.Web
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> MvcApplication : AbpWebApplication&lt;DemoWebModule&gt;<span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span> Application_Start(<span style="color: #0000ff;">object</span><span style="color: #000000;"> sender, EventArgs e)
        {
            </span><span style="color: #0000ff;">base</span><span style="color: #000000;">.Application_Start(sender, e);
        }
    }
}</span></pre>
</div>
<p>4，修改RouteConfig.cs</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> Demo.Web
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> RouteConfig
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> RegisterRoutes(RouteCollection routes)
        {
            routes.IgnoreRoute(</span><span style="color: #800000;">"</span><span style="color: #800000;">{resource}.axd/{*pathInfo}</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            
            routes.MapHttpRoute(
                name: </span><span style="color: #800000;">"</span><span style="color: #800000;">DefaultApi</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                routeTemplate: </span><span style="color: #800000;">"</span><span style="color: #800000;">api/{controller}/{id}</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                defaults: </span><span style="color: #0000ff;">new</span> { id =<span style="color: #000000;"> UrlParameter.Optional }
            );

            routes.MapRoute(
                name: </span><span style="color: #800000;">"</span><span style="color: #800000;">Default</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                url: </span><span style="color: #800000;">"</span><span style="color: #800000;">{controller}/{action}/{id}</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                defaults: </span><span style="color: #0000ff;">new</span> { controller = <span style="color: #800000;">"</span><span style="color: #800000;">Home</span><span style="color: #800000;">"</span>, action = <span style="color: #800000;">"</span><span style="color: #800000;">Index</span><span style="color: #800000;">"</span>, id =<span style="color: #000000;"> UrlParameter.Optional }
            );
        }
    }
}</span></pre>
</div>
<p>&nbsp;5，修改web.config连接字符串</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">add </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="Default"</span><span style="color: #ff0000;"> connectionString</span><span style="color: #0000ff;">="Server=localhost; Database=demo; Trusted_Connection=True;"</span><span style="color: #ff0000;"> providerName</span><span style="color: #0000ff;">="System.Data.SqlClient"</span> <span style="color: #0000ff;">/&gt;</span></pre>
</div>
<p>&nbsp;</p>
<p>demo下载：<a href="http://pan.baidu.com/s/1boSQwSv" target="_blank">http://pan.baidu.com/s/1boSQwSv</a></p>
<p>&nbsp;</p>