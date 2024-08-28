<p><span style="font-size: 14px;"><a href="#a1"><span style="color: #000000; background-color: #ffffff;">1.引导Abp系统</span></a></span></p>
<p><a href="#a2"><span style="color: #000000; background-color: #ffffff; font-size: 14px;">2.AbpSwaggerDemo</span></a></p>
<p><a href="#a3"><span style="font-size: 14px;">3.加密类</span></a></p>
<p><a href="#a4"><span style="font-size: 14px;">4.忽略webapi中的某个方法</span></a></p>
<p><a href="#a5"><span style="font-size: 14px;">5.Http动词</span></a></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p><span style="color: #000000; background-color: #ffffff;"><strong><span style="font-size: 18px;"><a name="a1"></a>1.引导Abp系统</span></strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Dependency;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Castle.Facilities.Logging;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> AbpEfConsoleApp
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">引导ABP系统</span>
            <span style="color: #0000ff;">using</span> (<span style="color: #0000ff;">var</span> bootstrapper = AbpBootstrapper.Create&lt;MyConsoleAppModule&gt;<span style="color: #000000;">())
            {
                bootstrapper.IocManager
                    .IocContainer
                    .AddFacility</span>&lt;LoggingFacility&gt;(f =&gt; f.UseLog4Net().WithConfig(<span style="color: #800000;">"</span><span style="color: #800000;">log4net.config</span><span style="color: #800000;">"</span><span style="color: #000000;">));

                bootstrapper.Initialize();

                </span><span style="color: #008000;">//</span><span style="color: #008000;">从DI获取测试对象并运行它</span>
                <span style="color: #0000ff;">using</span> (<span style="color: #0000ff;">var</span> tester = bootstrapper.IocManager.ResolveAsDisposable&lt;Tester&gt;<span style="color: #000000;">())
                {
                    tester.Object.Run();
                } </span><span style="color: #008000;">//</span><span style="color: #008000;">部署测试和所有它的依赖</span>
<span style="color: #000000;">
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">Press enter to exit...</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                Console.ReadLine();
            }
        }
    }
}</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Reflection;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.EntityFramework;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Modules;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> AbpEfConsoleApp
{
    </span><span style="color: #008000;">//</span><span style="color: #008000;">定义模块取决于AbpEntityFrameworkModule</span>
    [DependsOn(<span style="color: #0000ff;">typeof</span><span style="color: #000000;">(AbpEntityFrameworkModule))]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyConsoleAppModule : AbpModule
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Initialize()
        {
            IocManager.RegisterAssemblyByConvention(Assembly.GetExecutingAssembly());
        }
    }
}</span></pre>
</div>
<p><strong><span style="font-size: 18px;"><a name="a2"></a>2.AbpSwaggerDemo</span></strong></p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201710/741594-20171023155455691-2095379643.png" alt="" /></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Reflection;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Application.Services;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Modules;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.WebApi;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.WebApi.Controllers.Dynamic.Builders;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> OtherApp.Application;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> AbpSwagger.Application.WebApi.WebApi
{
    [DependsOn(
        </span><span style="color: #0000ff;">typeof</span><span style="color: #000000;">(AbpWebApiModule),
        </span><span style="color: #0000ff;">typeof</span><span style="color: #000000;">(AbpSwaggerAppModule),
        </span><span style="color: #0000ff;">typeof</span><span style="color: #000000;">(OtherAppModule))]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SwaggerWebApiModule : AbpModule
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Initialize()
        {
            IocManager.RegisterAssemblyByConvention(Assembly.GetExecutingAssembly());

            DynamicApiControllerBuilder
                .ForAll</span>&lt;IApplicationService&gt;(<span style="color: #0000ff;">typeof</span>(AbpSwaggerAppModule).Assembly, <span style="color: #800000;">"</span><span style="color: #800000;">app</span><span style="color: #800000;">"</span><span style="color: #000000;">)
                .WithConventionalVerbs()
                .Build();

            DynamicApiControllerBuilder
                .ForAll</span>&lt;IApplicationService&gt;(<span style="color: #0000ff;">typeof</span>(OtherAppModule).Assembly, <span style="color: #800000;">"</span><span style="color: #800000;">app</span><span style="color: #800000;">"</span><span style="color: #000000;">)
                .Build();
        }
    }
}</span></pre>
</div>
<p><strong><span style="font-size: 18px;"><a name="a3"></a>3.加密类</span></strong></p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">AES对称加密</span>
SimpleStringCipher.Instance.Encrypt(input.ConnectionString)</pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">实现密码哈希方法</span>
<span style="color: #0000ff;">new</span> PasswordHasher().HashPassword(input.Password)</pre>
</div>
<p>&nbsp;</p>
<p><strong><span style="font-size: 18px;"><a name="a4"></a>4.忽略webapi中的某个方法</span></strong></p>
<div class="cnblogs_code">
<div class="cnblogs_code_toolbar"><span class="cnblogs_code_copy"><a title="复制代码"><img src="http://common.cnblogs.com/images/copycode.gif" alt="复制代码" /></a></span></div>
<pre>DynamicApiControllerBuilder
    .ForAll&lt;IApplicationService&gt;(typeof(ChargeStationApplicationModule).Assembly, "ChargeStationAPI")
    .Build();//告诉生成器为所有实现了IApplicationService接口的服务方法创建api控制器
DynamicApiControllerBuilder
    .For&lt;ICityAppService&gt;("ChargeStationAPI/City")
    .ForMethod("CreateCity").DontCreateAction()
    .Build();//忽略"ChargeStationAPI/City"的"CreateCity"方法</pre>
<div class="cnblogs_code_toolbar"><span class="cnblogs_code_copy"><a title="复制代码"><img src="http://common.cnblogs.com/images/copycode.gif" alt="复制代码" /></a></span></div>
</div>
<p>&nbsp;</p>
<p><strong><span style="font-size: 18px;"><a name="a5"></a>5.Http动词</span></strong></p>
<p>①使用WithVerb</p>
<div class="cnblogs_code">
<pre>DynamicApiControllerBuilder.For&lt;ICityAppService&gt;("ChargeStationAPI/City")
    .ForMethod("getCities").WithVerb(HttpVerb.Get)
    .Build();</pre>
</div>
<p>②使用特性（需要添加<strong><a href="https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Core">Microsoft.AspNet.WebApi.Core</a>&nbsp;</strong>Nuget包的引用）</p>
<div class="cnblogs_code">
<div class="cnblogs_code_toolbar"><span class="cnblogs_code_copy"><a title="复制代码"><img src="http://common.cnblogs.com/images/copycode.gif" alt="复制代码" /></a></span></div>
<pre>public interface ICityAppService:IApplicationService
{
    [HttpGet]
    GetCitiesOutput GetCities(GetCityInput input);
    [HttpPost]
    void UpdateCity(CityInput input);
}</pre>
<div class="cnblogs_code_toolbar"><span class="cnblogs_code_copy"><a title="复制代码"><img src="http://common.cnblogs.com/images/copycode.gif" alt="复制代码" /></a></span></div>
</div>
<p>③使用restful风格</p>
<div class="cnblogs_code">
<pre>DynamicApiControllerBuilder
    .ForAll&lt;IApplicationService&gt;(typeof(ChargeStationApplicationModule).Assembly, "ChargeStationAPI")
    .WithConventionalVerbs()//根据方法名使用惯例HTTP动词，默认对于所有的action使用Post
    .Build();</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>九十九、api用法</p>
<div class="cnblogs_code">
<pre>                <span style="color: #008000;">//</span><span style="color: #008000;">_userManager.SetRoles方法的作用：变更角色（前提：用户表以已经创建）</span>
                CheckErrors(<span style="color: #0000ff;">await</span> _userManager.SetRoles(user, input.RoleNames));</pre>
</div>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre>            <span style="color: #008000;">//</span><span style="color: #008000;">admin用户不能被删除（删除用户的同时会删除UserRole）</span>
            <span style="color: #0000ff;">await</span> _userManager.DeleteAsync(user);</pre>
</div>
<p>&nbsp;</p>
<p>用户名只能包含字母或数字</p>
<p>&nbsp;</p>