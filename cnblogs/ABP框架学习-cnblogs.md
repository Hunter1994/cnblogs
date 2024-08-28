<p>&nbsp;</p>
<p><strong><span style="font-size: 18px;">一、总体与公共结构</span></strong><br /> 　　<a href="#a1"><strong>1，ABP配置</strong></a></p>
<p> 　　<strong><a href="#a2">2，多租户</a></strong></p>
<p> 　　<a href="#a3"><strong>3，ABP Session</strong></a></p>
<p> 　　<a href="#a4"><strong>4，缓存</strong>&nbsp;</a></p>
<p> 　　<a href="#a5"><strong>5，日志</strong></a></p>
<p> 　　<a href="#a6"><strong>6，设置管理</strong></a>&nbsp;</p>
<p> 　　<a href="#a7"><strong>7，Timing</strong>&nbsp;</a></p>
<p> 　　<a href="#a8"><strong>8，ABPMapper</strong></a></p>
<p> 　　<a href="#a9"><strong>9，发送电子邮件</strong></a>&nbsp;</p>
<p><span style="font-size: 18px;"><strong>二、领域层</strong></span></p>
<p> 　　<a href="#a10"><strong>10，实体</strong></a></p>
<p> 　　<a href="#a11"><strong>11，值对象</strong></a></p>
<p> 　　<a href="#a12"><strong>12，仓储</strong></a></p>
<p> 　　<a href="#a13"><strong>13，领域服务</strong></a>&nbsp;</p>
<p> 　　<a href="#a14"><strong>14，规格模式</strong></a></p>
<p> 　　<a href="#a15"><strong>15，工作单元</strong></a></p>
<p> 　　<a href="#a16"><strong>16，事件总线</strong>&nbsp;</a></p>
<p> 　　<a href="#a17"><strong>17，数据过滤器</strong></a></p>
<p><span style="font-size: 18px;"><strong>三、应用层</strong></span></p>
<p> 　　<a href="#a18"><strong>18，应用服务</strong>&nbsp;</a></p>
<p> 　　<a href="#a19"><strong>19，数据传输对象</strong></a></p>
<p> 　　<a href="#a20"><strong>20，验证数据传输对象</strong></a></p>
<p> 　　<a href="#a21"><strong>21，授权</strong><br /></a></p>
<p> 　　<a href="#a22"><strong>22，功能管理</strong></a></p>
<p> 　　<a href="#a23"><strong>23，审计日志</strong></a></p>
<p><span style="font-size: 18px;"><strong>四、分布式服务层</strong></span></p>
<p> 　　<a href="#a24"><strong>24，ASP.NET Web API Controllers</strong></a></p>
<p> 　　<a href="#a25"><strong>25，动态Webapi层</strong></a></p>
<p> 　　<a href="#a26"><strong>26，OData整合</strong></a></p>
<p> 　　<a href="#a27"><strong>27，Swagger UI 整合</strong>&nbsp;</a></p>
<p><strong><span style="font-size: 18px;">五、展示层</span></strong></p>
<p>　　<a href="#a28"><strong>28，ASP.NET MVC</strong></a></p>
<p> 　　<strong><a href="#a29">29，本地化</a></strong></p>
<p> 　　<a href="#a30"><strong>30，导航</strong></a></p>
<p> 　　<strong><a href="#a31">31，嵌入式资源文件</a></strong></p>
<p> 　　<a href="http://www.cnblogs.com/zd1994/p/7689164.html" target="_blank"><strong>32，</strong><strong>ABP-JavaScript AP</strong>I</a></p>
<p> 　　<a href="#a33"><strong>33，CSRF / XSRF保护</strong></a></p>
<p><span style="font-size: 18px;"><strong>六、后台服务</strong></span></p>
<p> 　　<a href="#a34"><strong>34，后台工作(Jobs)和工作者（Workers）</strong></a></p>
<p> 　　<a href="#a35"><strong>35，Hangfire集成</strong></a></p>
<p> 　　<a href="#a36"><strong>36，Quartz 集成</strong></a></p>
<p><strong><span style="font-size: 18px;">七、实时服务</span></strong>&nbsp;</p>
<p> 　　<strong><a href="#a37">37，通知系统</a></strong></p>
<p> 　　<a href="#a38"><strong>38，SignalR集成</strong></a></p>
<p><strong><span style="font-size: 18px;">&nbsp;八、ORM</span></strong></p>
<p> 　　<a href="#a39"><strong>39，EntityFramework集成</strong></a></p>
<p> 　　<a href="#a40"><strong>40，NHibernate集成</strong></a></p>
<p> 　　<a href="#a41"><strong>41，Dapper使用</strong></a></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a1"></a>一、ABP配置</span></strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">将所有异常发送到客户端</span>
Configuration.Modules.AbpWebCommon().SendAllExceptionsToClients = <span style="color: #0000ff;">true</span>;</pre>
</div>
<p>1，自定义配置</p>
<p>①创建配置类</p>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> CustomModule
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">bool</span> IsEnable { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    }</span></pre>
</div>
<p>&nbsp;</p>
<p>②定义Configuration扩展</p>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ModuleConfigrationExt
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> CustomModule GetCustomModule(<span style="color: #0000ff;">this</span><span style="color: #000000;"> IModuleConfigurations moduleConfigurations)
        {
            </span><span style="color: #0000ff;">return</span> moduleConfigurations.AbpConfiguration.Get&lt;CustomModule&gt;<span style="color: #000000;">();
        }
    }</span></pre>
</div>
<p>③使用自定义配置</p>
<div class="cnblogs_code">
<pre>            <span style="color: #008000;">//</span><span style="color: #008000;">注册CustomModule配置类</span>
            IocManager.Register&lt;CustomModule&gt;<span style="color: #000000;">();
            </span><span style="color: #008000;">//</span><span style="color: #008000;">设置CustomModule配置</span>
            Configuration.Modules.GetCustomModule().IsEnable = <span style="color: #0000ff;">true</span>;</pre>
</div>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a2"></a>二、多租户</span></strong></span></p>
<p>1，在core层开启多租户</p>
<div class="cnblogs_code">
<pre>Configuration.MultiTenancy.IsEnabled = <span style="color: #0000ff;">true</span>; </pre>
</div>
<p>2，主机与租户</p>
<p>主机：拥有自己的用户，角色，权限，设置的客户，并使用与其他租户完全隔离的应用程序。 多租户申请将有一个或多个租户。 如果这是CRM应用程序，不同的租户也有自己的帐户，联系人，产品和订单。 所以，当我们说一个'租户用户'时，我们的意思是租户拥有的用户。</p>
<p>租户：主机是单例（有一个主机）。 主持人负责创建和管理租户。 所以，&ldquo;主机用户&rdquo;是较高层次的，独立于所有租户，可以控制他们。</p>
<p>3，abp定义IAbpSession接口获取UserId和TenantId</p>
<p>如果UserId和TenantId都为空，则当前用户未登录到系统。 所以，我们不知道是主机用户还是租户用户。 在这种情况下，用户无法访问授权的内容。<br />如果UserId不为null并且TenantId为null，那么我们可以知道当前用户是主机用户。<br />如果UserId不为null，并且TenantId不为空，我们可以知道当前用户是租户用户。<br />如果UserId为null但TenantId不为空，那意味着我们可以知道当前的租户，但是当前的请求没有被授权（用户没有登录）</p>
<p>4，数据过滤器</p>
<p>如果实体实现的是IMustHaveTenant接口，且AbpSession.TenantId为null的时候（即主机用户），获取到的数据是所有租户的，除非你自己显式进行过滤。而在IMayHaveTenant情况下，AbpSession.TenantId为null获取到的是主机用户的数据。</p>
<p>①IMustHaveTenant 接口：该接口通过定义<strong>TenantId</strong>属性来区分不同租户的实体</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Product : Entity, IMustHaveTenant
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span> TenantId { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
        
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Name { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...其他属性</span>
}</pre>
</div>
<p>②IMayHaveTenant接口：我们可能需要在租户和租户之间共享一个<strong>实体类型</strong>。因此，一个实体可能会被一个租户或租主拥有</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Role : Entity, IMayHaveTenant
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span>? TenantId { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
        
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> RoleName { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...其他属性</span>
}</pre>
</div>
<p>IMayHaveTenant不像IMustHaveTenant一样常用。比如，一个Product类可以不实现IMayHaveTenant接口，因为Product和实际的应用功能相关，和管理租户不相干。因此，要小心使用IMayHaveTenant接口，因为它更难维护租户和租主共享的代码。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a3"></a>三、ABP Session</span></strong></span></p>
<p>1，AbpSession定义了一些关键属性：</p>
<p>UserId：当前用户的ID，如果没有当前用户，则为null。 如果通话代码被授权，则不能为空。<br />TenantId：当前租户的ID，如果没有当前租户（如果用户未登录或他是主机用户），则为null。<br />ImpersonatorUserId：当前会话由其他用户模拟时，模拟人员的身份。 如果这不是模拟登录，它为null。<br />ImpersonatorTenantId：假冒用户的租户的身份，如果当前会话由其他用户模拟。 如果这不是模拟登录，它为null。<br />MultiTenancySide：可能是主机或租户。</p>
<p>2，覆盖当前会话值</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyService
{
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> IAbpSession _session;

    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> MyService(IAbpSession session)
    {
        _session </span>=<span style="color: #000000;"> session;
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Test()
    {
        </span><span style="color: #0000ff;">using</span> (_session.Use(<span style="color: #800080;">42</span>, <span style="color: #0000ff;">null</span><span style="color: #000000;">))
        {
            </span><span style="color: #0000ff;">var</span> tenantId = _session.TenantId; <span style="color: #008000;">//</span><span style="color: #008000;">42</span>
            <span style="color: #0000ff;">var</span> userId = _session.UserId; <span style="color: #008000;">//</span><span style="color: #008000;">null</span>
<span style="color: #000000;">        }
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a4"></a>四、缓存</span></strong></span></p>
<p>1，我们可以注入它并使用它来获取缓存</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> TestAppService : ApplicationService
{
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> ICacheManager _cacheManager;

    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> TestAppService(ICacheManager cacheManager)
    {
        _cacheManager </span>=<span style="color: #000000;"> cacheManager;
    }

    </span><span style="color: #0000ff;">public</span> Item GetItem(<span style="color: #0000ff;">int</span><span style="color: #000000;"> id)
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;">Try to get from cache</span>
        <span style="color: #0000ff;">return</span><span style="color: #000000;"> _cacheManager
                .GetCache(</span><span style="color: #800000;">"</span><span style="color: #800000;">MyCache</span><span style="color: #800000;">"</span><span style="color: #000000;">)
                .Get(id.ToString(), () </span>=&gt; GetFromDatabase(id)) <span style="color: #0000ff;">as</span><span style="color: #000000;"> Item;
    }

    </span><span style="color: #0000ff;">public</span> Item GetFromDatabase(<span style="color: #0000ff;">int</span><span style="color: #000000;"> id)
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;">... retrieve item from database</span>
<span style="color: #000000;">    }
}</span></pre>
</div>
<p>2，配置缓存有效期</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">Configuration for all caches</span>
Configuration.Caching.ConfigureAll(cache =&gt;<span style="color: #000000;">
{
    cache.DefaultSlidingExpireTime </span>= TimeSpan.FromHours(<span style="color: #800080;">2</span><span style="color: #000000;">);
});

</span><span style="color: #008000;">//</span><span style="color: #008000;">Configuration for a specific cache</span>
Configuration.Caching.Configure(<span style="color: #800000;">"</span><span style="color: #800000;">MyCache</span><span style="color: #800000;">"</span>, cache =&gt;<span style="color: #000000;">
{
    cache.DefaultSlidingExpireTime </span>= TimeSpan.FromHours(<span style="color: #800080;">8</span><span style="color: #000000;">);
});</span></pre>
</div>
<p>默认缓存超时时间为60分钟。该代码应该放在您的模块的PreInitialize方法中。 有了这样一个代码，MyCache将有8个小时的过期时间，而所有其他缓存将有2个小时。</p>
<p>3，实体缓存（例如：根据人员id查询人员信息缓存）</p>
<p>①在dto中定义缓存类</p>
<div class="cnblogs_code">
<pre>[AutoMapFrom(<span style="color: #0000ff;">typeof</span><span style="color: #000000;">(Person))]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> PersonCacheItem
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Name { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}</span></pre>
</div>
<p>②在application层中定义实体缓存接口</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span> IPersonCache : IEntityCache&lt;PersonCacheItem&gt;<span style="color: #000000;">
{

}</span></pre>
</div>
<p>③实现缓存接口</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> PersonCache : EntityCache&lt;Person, PersonCacheItem&gt;<span style="color: #000000;">, IPersonCache, ITransientDependency
{
    </span><span style="color: #0000ff;">public</span> PersonCache(ICacheManager cacheManager, IRepository&lt;Person&gt;<span style="color: #000000;"> repository)
        : </span><span style="color: #0000ff;">base</span><span style="color: #000000;">(cacheManager, repository)
    {

    }
}</span></pre>
</div>
<p>④应用层使用</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyPersonService : ITransientDependency
{
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> IPersonCache _personCache;

    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> MyPersonService(IPersonCache personCache)
    {
        _personCache </span>=<span style="color: #000000;"> personCache;
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> GetPersonNameById(<span style="color: #0000ff;">int</span><span style="color: #000000;"> id)
    {
        </span><span style="color: #0000ff;">return</span> _personCache[id].Name; <span style="color: #008000;">//</span><span style="color: #008000;">替代: _personCache.Get(id).Name;</span>
<span style="color: #000000;">    }
}</span></pre>
</div>
<p>&nbsp;4，使用Redis缓存</p>
<p>①在Web项目中Nuget引用Abp.RedisCache</p>
<p>②设置Module</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Runtime.Caching.Redis;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> MyProject.AbpZeroTemplate.Web
{
    [DependsOn(
        </span><span style="color: #008000;">//</span><span style="color: #008000;">...other module dependencies</span>
        <span style="color: #0000ff;">typeof</span><span style="color: #000000;">(AbpRedisCacheModule))]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyProjectWebModule : AbpModule
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> PreInitialize()
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">...other configurations</span>
<span style="color: #000000;">            
            Configuration.Caching.UseRedis();
        }
        
        </span><span style="color: #008000;">//</span><span style="color: #008000;">...other code</span>
<span style="color: #000000;">    }
}</span></pre>
</div>
<p>③Abp.Redis Cache包使用&ldquo;localhost&rdquo;作为连接字符串作为默认值。 您可以将连接字符串添加到您的配置文件中以覆盖它。 例：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">add </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="Abp.Redis.Cache"</span><span style="color: #ff0000;"> connectionString</span><span style="color: #0000ff;">="localhost"</span><span style="color: #0000ff;">/&gt;</span></pre>
</div>
<p>④此外，您可以将appSettings的设置添加到Redis的数据库ID中。 例：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">add </span><span style="color: #ff0000;">key</span><span style="color: #0000ff;">="Abp.Redis.Cache.DatabaseId"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">="2"</span><span style="color: #0000ff;">/&gt;</span></pre>
</div>
<p>不同的数据库标识对于在同一服务器中创建不同的密钥空间（隔离缓存）很有用。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a5"></a>五、日志</span></strong></span></p>
<p>1，在Web层NuGet安装：Abp.Castle.Log4Net&nbsp;</p>
<p>2，在Web层的Global.asax注入logger</p>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> MvcApplication : AbpWebApplication&lt;SimpleWebModule&gt;<span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span> Session_Start(<span style="color: #0000ff;">object</span><span style="color: #000000;"> sender, EventArgs e)
        {
            IocManager.Instance.IocContainer.AddFacility</span>&lt;LoggingFacility&gt;<span style="color: #000000;">(
                f </span>=&gt; f.UseAbpLog4Net().WithConfig(<span style="color: #800000;">"</span><span style="color: #800000;">log4net.config</span><span style="color: #800000;">"</span><span style="color: #000000;">));
            </span><span style="color: #0000ff;">base</span><span style="color: #000000;">.Session_Start(sender, e);
        }
    }</span></pre>
</div>
<p>3，在Web层添加log4net配置文件（log4net.config）</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;?</span><span style="color: #ff00ff;">xml version="1.0" encoding="utf-8" </span><span style="color: #0000ff;">?&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">log4net</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">appender </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="RollingFileAppender"</span><span style="color: #ff0000;"> type</span><span style="color: #0000ff;">="log4net.Appender.RollingFileAppender"</span> <span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">file </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="App_Data/Logs/Logs.txt"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">appendToFile </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="true"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">rollingStyle </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="Size"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">maxSizeRollBackups </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="10"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">maximumFileSize </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="10000KB"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">staticLogFileName </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="true"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">layout </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="log4net.Layout.PatternLayout"</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">conversionPattern </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="%-5level %date [%-5.5thread] %-40.40logger - %message%newline"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">layout</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">appender</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">root</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">appender-ref </span><span style="color: #ff0000;">ref</span><span style="color: #0000ff;">="RollingFileAppender"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">level </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="DEBUG"</span> <span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">root</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">logger </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="NHibernate"</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">level </span><span style="color: #ff0000;">value</span><span style="color: #0000ff;">="WARN"</span> <span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">logger</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">log4net</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>4，在application层直接直接使用Logger</p>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task&lt;ListResultDto&lt;EmployeeListDto&gt;&gt;<span style="color: #000000;"> GetEmpAll()
        {
            Logger.Info(</span><span style="color: #800000;">"</span><span style="color: #800000;">查询员工信息</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            </span><span style="color: #0000ff;">var</span> emps = <span style="color: #0000ff;">await</span><span style="color: #000000;"> _employeeRepository.GetAllListAsync();
            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> ListResultDto&lt;EmployeeListDto&gt;(emps.MapTo&lt;List&lt;EmployeeListDto&gt;&gt;<span style="color: #000000;">());
        }</span></pre>
</div>
<p>5，客户端</p>
<div class="cnblogs_code">
<pre>abp.log.warn(<span style="color: #800000;">'</span><span style="color: #800000;">a sample log message...</span><span style="color: #800000;">'</span>);</pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a6"></a>六、设置管理</span></strong></span></p>
<p>一个设置一般是存储在数据库（或其他源）的<strong>name-value</strong>字符串对。我们可以将非字符串的值转换成字符串。</p>
<p>使用前必须定义一个设置。 ASP.NET Boilerplate设计为模块化。 所以，不同的模块可以有不同的设置</p>
<p>1，定义设置</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MySettingProvider : SettingProvider
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> IEnumerable&lt;SettingDefinition&gt;<span style="color: #000000;"> GetSettingDefinitions(SettingDefinitionProviderContext context)
    {
        </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;">[]
                {
                    </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> SettingDefinition(
                        </span><span style="color: #800000;">"</span><span style="color: #800000;">SmtpServerAddress</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                        </span><span style="color: #800000;">"</span><span style="color: #800000;">127.0.0.1</span><span style="color: #800000;">"</span><span style="color: #000000;">
                        ),

                    </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> SettingDefinition(
                        </span><span style="color: #800000;">"</span><span style="color: #800000;">PassiveUsersCanNotLogin</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                        </span><span style="color: #800000;">"</span><span style="color: #800000;">true</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                        scopes: SettingScopes.Application </span>|<span style="color: #000000;"> SettingScopes.Tenant
                        ),

                    </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> SettingDefinition(
                        </span><span style="color: #800000;">"</span><span style="color: #800000;">SiteColorPreference</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                        </span><span style="color: #800000;">"</span><span style="color: #800000;">red</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                        scopes: SettingScopes.User,
                        isVisibleToClients: </span><span style="color: #0000ff;">true</span><span style="color: #000000;">
                        )

                };
    }
}</span></pre>
</div>
<p>参数说明：</p>
<p>Name(必填)：名称</p>
<p>Default Name：默认值，该值可以为空或空字符串</p>
<p>Scopes：</p>
<p>　　　　Application：应用范围设置用于用户/租户独立设置。 例如，我们可以定义一个名为&ldquo;SmtpServerAddress&rdquo;的设置，以便在发送电子邮件时获取服务器的IP地址。 如果此设置具有单个值（不根据用户进行更改），那么我们可以将其定义为应用程序范围。</p>
<p>　　　　Tenant:如果应用程序是多租户，我们可以定义特定于租户的设置。</p>
<p>　　　　User:我们可以使用用户作用域设置来存储/获取每个用户特定设置的值。</p>
<p>Display Name：可用于在UI中稍后显示设置名称的本地化字符串。</p>
<p>Description：一个可本地化的字符串，可用于稍后在UI中显示设置描述。</p>
<p>Group：可用于分组设置。 这只是用于UI，不用于设置管理。</p>
<p>IsVisibleToClients：设置为true，使客户端可以使用设置。</p>
<p>&nbsp;</p>
<p>2，创建setting provider后，我们应该在本模块的PreIntialize方法中注册它：</p>
<div class="cnblogs_code">
<pre>Configuration.Settings.Providers.Add&lt;MySettingProvider&gt;();</pre>
</div>
<p>由于ISettingManager被广泛使用，一些特殊的基类（如ApplicationService，DomainService和AbpController）有一个名为SettingManager的属性。 如果我们从这些类派生，不需要明确地注入它们。</p>
<p>&nbsp;</p>
<p>3，获取设置</p>
<p>①服务器端：</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">获取布尔值（异步调用）</span>
<span style="color: #0000ff;">var</span> value1 = <span style="color: #0000ff;">await</span> SettingManager.GetSettingValueAsync&lt;<span style="color: #0000ff;">bool</span>&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">PassiveUsersCanNotLogin</span><span style="color: #800000;">"</span><span style="color: #000000;">);

</span><span style="color: #008000;">//</span><span style="color: #008000;">获取字符串值（同步调用）</span>
<span style="color: #0000ff;">var</span> value2 = SettingManager.GetSettingValue(<span style="color: #800000;">"</span><span style="color: #800000;">SmtpServerAddress</span><span style="color: #800000;">"</span>);</pre>
</div>
<p>②客户端：</p>
<p>当定义一个setting时，如果将<strong>IsVisibleToClients</strong>设置为true，那么可以使用javascript在客户端获得当前的值。<strong>abp.setting</strong>命名空间定义了一些用得到的函数和对象。例如：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> currentColor = abp.setting.<span style="color: #0000ff;">get</span>(<span style="color: #800000;">"</span><span style="color: #800000;">SiteColorPreference</span><span style="color: #800000;">"</span>);</pre>
</div>
<p>也有<strong>getInt</strong>和&nbsp;<strong>getBoolean</strong>&nbsp;方法。你可以使用<strong>abp.setting.values</strong>获得所有的值。注意：如果在服务端更改了一个setting，那么如果页面没有更新，setting没有重新加载或者通过代码手动更新的话，那么客户端就不知道该setting是否发生了变化。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a7"></a>七、Timing</span></strong></span></p>
<p>1，Clock类静态属性介绍</p>
<p>Now：根据当前提供商获取当前时间</p>
<p>Kind：获取当前提供者的DateTimeKind</p>
<p>SupportsMultipleTimezone：获取一个值，表示当前提供程序可以用于需要多个时区的应用程序</p>
<p>Normalize：对当前提供商的给定DateTime进行规范化/转换</p>
<div class="cnblogs_code">
<pre>DateTime now = Clock.Now;</pre>
</div>
<p>2，三种内置的clock&nbsp;</p>
<p>ClockProviders.Unspecified (UnspecifiedClockProvider)：默认的clock。就像DateTime.Now一样</p>
<p>ClockProviders.Utc (UtcClockProvider)：Normalize方法将给定的datetime转换为utc datetime，并将其设置为DateTimeKind.UTC。 它支持多个时区。</p>
<p>ClockProviders.Local (LocalClockProvider)：在本地计算机的时间工作。 Normalize方法将给定的datetime转换为本地datetime，并将其设置为DateTimeKind.Local</p>
<p>您可以设置Clock.Provider以使用不同的时钟提供程序：</p>
<div class="cnblogs_code">
<pre>Clock.Provider = ClockProviders.Utc;</pre>
</div>
<p>这通常在应用程序开始时完成（适用于Web应用程序中的Application_Start）。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a8"></a>八、ABPMapper</span></strong></span></p>
<p>1，使用AbpAutoMapper</p>
<p>①模块使用AbpAutoMapper需要引用依赖</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> SimpleDemo.Application
{
    [DependsOn(</span><span style="color: #0000ff;">typeof</span>(SimpleDemoCoreModule), <span style="color: #0000ff;">typeof</span><span style="color: #000000;">(AbpAutoMapperModule))]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SimpleDemoApplicationModule:AbpModule
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Initialize()
        {
            IocManager.RegisterAssemblyByConvention(Assembly.GetExecutingAssembly());
        }
    }
}</span></pre>
</div>
<p>②使用<strong>AutoMapFrom</strong>&nbsp;、<strong>AutoMapTo</strong>&nbsp;&nbsp;两个方向的映射</p>
<div class="cnblogs_code">
<pre>[AutoMapTo(<span style="color: #0000ff;">typeof</span><span style="color: #000000;">(User))]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> CreateUserInput
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Name { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Surname { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> EmailAddress { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Password { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}</span></pre>
</div>
<div class="cnblogs_code">
<pre>[AutoMapFrom(<span style="color: #0000ff;">typeof</span><span style="color: #000000;">(User))]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> CreateUserOutput
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Name { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Surname { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> EmailAddress { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Password { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}</span></pre>
</div>
<p>2，自定义映射</p>
<p>在某些情况下，简单的映射可能不合适。 例如，两个类的属性名可能有些不同，或者您可能希望在映射期间忽略某些属性</p>
<p>假设我们要忽略映射的密码，并且用户具有电子邮件地址的电子邮件属性。 我们可以定义映射，如下所示：</p>
<div class="cnblogs_code">
<pre>[DependsOn(<span style="color: #0000ff;">typeof</span><span style="color: #000000;">(AbpAutoMapperModule))]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyModule : AbpModule
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> PreInitialize()
    {
        Configuration.Modules.AbpAutoMapper().Configurators.Add(config </span>=&gt;<span style="color: #000000;">
        {
            config.CreateMap</span>&lt;CreateUserInput, User&gt;<span style="color: #000000;">()
                  .ForMember(u </span>=&gt; u.Password, options =&gt;<span style="color: #000000;"> options.Ignore())
                  .ForMember(u </span>=&gt; u.Email, options =&gt; options.MapFrom(input =&gt;<span style="color: #000000;"> input.EmailAddress));
        });
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a9"></a>九、发送电子邮件</span></strong></span></p>
<p>1，Abp.Net.Mail.EmailSettingNames类中定义为常量字符串。 他们的价值观和描述：</p>
<p>Abp.Net.Mail.DefaultFromAddress：在发送电子邮件时不指定发件人时，用作发件人电子邮件地址（如上面的示例所示）。<br />Abp.Net.Mail.DefaultFromDisplayName：在发送电子邮件时不指定发件人时，用作发件人显示名称（如上面的示例所示）。<br />Abp.Net.Mail.Smtp.Host：SMTP服务器的IP /域（默认值：127.0.0.1）。<br />Abp.Net.Mail.Smtp.Port：SMTP服务器的端口（默认值：25）。<br />Abp.Net.Mail.Smtp.UserName：用户名，如果SMTP服务器需要身份验证。<br />Abp.Net.Mail.Smtp.Password：密码，如果SMTP服务器需要身份验证。<br />Abp.Net.Mail.Smtp.Domain：域名用户名，如果SMTP服务器需要身份验证。<br />Abp.Net.Mail.Smtp.EnableSsl：一个值表示SMTP服务器使用SSL（&ldquo;true&rdquo;或&ldquo;false&rdquo;），默认值为&ldquo;false&rdquo;）。<br />Abp.Net.Mail.Smtp.UseDefaultCredentials：True，使用默认凭据而不是提供的用户名和密码（&ldquo;true&rdquo;或&ldquo;false&rdquo;）。默认值为&ldquo;true&rdquo;）。</p>
<p>2，使用qq邮箱发送邮件</p>
<p>①需要在qq邮箱中开启smtp服务</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201709/741594-20170918131017259-675639941.png" alt="" /></p>
<p>②配置设置</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> Demo.Core.Email
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> AppSettingProvider:SettingProvider
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> IEnumerable&lt;SettingDefinition&gt;<span style="color: #000000;"> GetSettingDefinitions(SettingDefinitionProviderContext context)
        {
            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;">[]
            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;">EnableSsl一定设置为true</span>
                <span style="color: #0000ff;">new</span> SettingDefinition( EmailSettingNames.Smtp.EnableSsl,<span style="color: #800000;">"</span><span style="color: #800000;">true</span><span style="color: #800000;">"</span>,L(<span style="color: #800000;">"</span><span style="color: #800000;">SmtpEnableSsl</span><span style="color: #800000;">"</span>),scopes:SettingScopes.Application|<span style="color: #000000;">SettingScopes.Tenant),
                </span><span style="color: #008000;">//</span><span style="color: #008000;">UseDefaultCredentials一定设置为false</span>
                <span style="color: #0000ff;">new</span> SettingDefinition( EmailSettingNames.Smtp.UseDefaultCredentials,<span style="color: #800000;">"</span><span style="color: #800000;">false</span><span style="color: #800000;">"</span>,L(<span style="color: #800000;">"</span><span style="color: #800000;">SmtpUseDefaultCredentials</span><span style="color: #800000;">"</span>),scopes:SettingScopes.Application|<span style="color: #000000;">SettingScopes.Tenant),
                </span><span style="color: #0000ff;">new</span> SettingDefinition( EmailSettingNames.Smtp.Host,<span style="color: #800000;">"</span><span style="color: #800000;">smtp.qq.com</span><span style="color: #800000;">"</span>,L(<span style="color: #800000;">"</span><span style="color: #800000;">SmtpHost</span><span style="color: #800000;">"</span>),scopes:SettingScopes.Application|<span style="color: #000000;">SettingScopes.Tenant),
                </span><span style="color: #0000ff;">new</span> SettingDefinition( EmailSettingNames.Smtp.Port,<span style="color: #800000;">"</span><span style="color: #800000;">25</span><span style="color: #800000;">"</span>,L(<span style="color: #800000;">"</span><span style="color: #800000;">SmtpPort</span><span style="color: #800000;">"</span>),scopes:SettingScopes.Application|<span style="color: #000000;">SettingScopes.Tenant),
                </span><span style="color: #0000ff;">new</span> SettingDefinition( EmailSettingNames.Smtp.UserName,<span style="color: #800000;">"</span><span style="color: #800000;">962410314@qq.com</span><span style="color: #800000;">"</span>,L(<span style="color: #800000;">"</span><span style="color: #800000;">SmtpUserName</span><span style="color: #800000;">"</span>),scopes:SettingScopes.Application|<span style="color: #000000;">SettingScopes.Tenant),
                </span><span style="color: #008000;">//</span><span style="color: #008000;">Password使用授权码</span>
                <span style="color: #0000ff;">new</span> SettingDefinition( EmailSettingNames.Smtp.Password,<span style="color: #800000;">"</span><span style="color: #800000;">aaa</span><span style="color: #800000;">"</span>,L(<span style="color: #800000;">"</span><span style="color: #800000;">SmtpPassword</span><span style="color: #800000;">"</span>),scopes:SettingScopes.Application|<span style="color: #000000;">SettingScopes.Tenant),
                </span><span style="color: #008000;">//</span><span style="color: #008000;">这个EmailSettingNames.Smtp.Domain设置后老是报错，索性直接注销了
                </span><span style="color: #008000;">//</span><span style="color: #008000;">new SettingDefinition( EmailSettingNames.Smtp.Domain,"962410314@qq.com",L("SmtpDomain"),scopes:SettingScopes.Application|SettingScopes.Tenant),</span>
                <span style="color: #0000ff;">new</span> SettingDefinition( EmailSettingNames.DefaultFromAddress,<span style="color: #800000;">"</span><span style="color: #800000;">962410314@qq.com</span><span style="color: #800000;">"</span>,L(<span style="color: #800000;">"</span><span style="color: #800000;">SmtpDefaultFromAddress</span><span style="color: #800000;">"</span>),scopes:SettingScopes.Application|<span style="color: #000000;">SettingScopes.Tenant),
                </span><span style="color: #0000ff;">new</span> SettingDefinition( EmailSettingNames.DefaultFromDisplayName,<span style="color: #800000;">"</span><span style="color: #800000;">默认</span><span style="color: #800000;">"</span>,L(<span style="color: #800000;">"</span><span style="color: #800000;">SmtpDefaultFromDisplayName</span><span style="color: #800000;">"</span>),scopes:SettingScopes.Application|<span style="color: #000000;">SettingScopes.Tenant),
            };
        }

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> LocalizableString L(<span style="color: #0000ff;">string</span><span style="color: #000000;"> name)
        {
            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> LocalizableString(name, AbpConsts.LocalizationSourceName);
        }
    }
}</span></pre>
</div>
<p>③在PreInitialize中注册</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> Demo.Core
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> DemoCoreModule:AbpModule
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> PreInitialize()
        {
            Configuration.Settings.Providers.Add</span>&lt;AppSettingProvider&gt;<span style="color: #000000;">();
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Initialize()
        {
            IocManager.RegisterAssemblyByConvention(Assembly.GetExecutingAssembly());
        }
    }
}</span></pre>
</div>
<p>④发送邮件</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> Demo.Core.Employee
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> EmployeeManager:IDomainService
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> IEmailSender _emailSender;
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> EmployeeManager(IEmailSender emailSender)
        {
            _emailSender </span>=<span style="color: #000000;"> emailSender;
        }
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> send()
        {
            _emailSender.Send(to: </span><span style="color: #800000;">"</span><span style="color: #800000;">qq962410314@163.com</span><span style="color: #800000;">"</span>, subject: <span style="color: #800000;">"</span><span style="color: #800000;">测试</span><span style="color: #800000;">"</span>, body: <span style="color: #800000;">"</span><span style="color: #800000;">测试</span><span style="color: #800000;">"</span>, isBodyHtml: <span style="color: #0000ff;">false</span><span style="color: #000000;">);
        }
    }
}</span></pre>
</div>
<p>案例下载：<a href="http://pan.baidu.com/s/1dF5wp9J" target="_blank">http://pan.baidu.com/s/1dF5wp9J</a></p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a10"></a>十、实体</span></strong></span></p>
<p>实体具有Id并存储在数据库中， 实体通常映射到关系数据库的表。</p>
<p>1，审计接口</p>
<p>①当Entity被插入到实现该接口的数据库中时，ASP.NET Boilerplate会自动将CreationTime设置为当前时间。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IHasCreationTime
{
    DateTime CreationTime { </span><span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}</span></pre>
</div>
<p>②ASP.NET Boilerplate在保存新实体时自动将CreatorUserId设置为当前用户的id</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> ICreationAudited : IHasCreationTime
{
    </span><span style="color: #0000ff;">long</span>? CreatorUserId { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}</span></pre>
</div>
<p>③编辑时间，编辑人员</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IHasModificationTime
{
    DateTime</span>? LastModificationTime { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IModificationAudited : IHasModificationTime
{
    </span><span style="color: #0000ff;">long</span>? LastModifierUserId { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}</span></pre>
</div>
<p>④如果要实现所有审计属性，可以直接实现IAudited接口：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IAudited : ICreationAudited, IModificationAudited
{

}</span></pre>
</div>
<p>⑤可以直接继承AuditedEntity审计类</p>
<p><span style="color: #ff0000; font-size: 13px;">注意：ASP.NET Boilerplate从ABP Session获取当前用户的Id。</span></p>
<p>⑥软删除</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> ISoftDelete
{
    </span><span style="color: #0000ff;">bool</span> IsDeleted { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IDeletionAudited : ISoftDelete
{
    </span><span style="color: #0000ff;">long</span>? DeleterUserId { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    DateTime</span>? DeletionTime { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}</span></pre>
</div>
<p>⑦所有审计接口</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IFullAudited : IAudited, IDeletionAudited
{

}</span></pre>
</div>
<p>⑧直接使用所有审计类<strong>FullAuditedEntity</strong>&nbsp;</p>
<p>2，继承IExtendableObject接口存储json字段</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Person : Entity, IExtendableObject
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Name { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> ExtensionData { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span> Person(<span style="color: #0000ff;">string</span><span style="color: #000000;"> name)
    {
        Name </span>=<span style="color: #000000;"> name;
    }
}</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> person = <span style="color: #0000ff;">new</span> Person(<span style="color: #800000;">"</span><span style="color: #800000;">John</span><span style="color: #800000;">"</span><span style="color: #000000;">);
//存入数据库中的值：</span>{"<span class="hljs-attribute">CustomData":<span class="hljs-value">{"<span class="hljs-attribute">Value1":<span class="hljs-value"><span class="hljs-number">42,"<span class="hljs-attribute">Value2":<span class="hljs-value"><span class="hljs-string">"forty-two"},"<span class="hljs-attribute">RandomValue":<span class="hljs-value">178}</span></span></span></span></span></span></span></span></span></span></pre>
<pre><span style="color: #000000;">person.SetData(</span><span style="color: #800000;">"</span><span style="color: #800000;">RandomValue</span><span style="color: #800000;">"</span>, RandomHelper.GetRandom(<span style="color: #800080;">1</span>, <span style="color: #800080;">1000</span><span style="color: #000000;">)); <br />person.SetData(</span><span style="color: #800000;">"</span><span style="color: #800000;">CustomData</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span> MyCustomObject { Value1 = <span style="color: #800080;">42</span>, Value2 = <span style="color: #800000;">"</span><span style="color: #800000;">forty-two</span><span style="color: #800000;">"</span> });</pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> randomValue = person.GetData&lt;<span style="color: #0000ff;">int</span>&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">RandomValue</span><span style="color: #800000;">"</span><span style="color: #000000;">);
</span><span style="color: #0000ff;">var</span> customData = person.GetData&lt;MyCustomObject&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">CustomData</span><span style="color: #800000;">"</span>);</pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a11"></a>十一、值对象</span></strong></span></p>
<p>与实体相反，实体拥有身份标识（id），而值对象没有。例如地址（这是一个经典的Value Object）类，如果两个地址有相同的国家/地区，城市，街道号等等，它们被认为是相同的地址。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> Address : ValueObject&lt;Address&gt;<span style="color: #000000;">
{
    </span><span style="color: #0000ff;">public</span> Guid CityId { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">private</span> <span style="color: #0000ff;">set</span>; } <span style="color: #008000;">//</span><span style="color: #008000;">A reference to a City entity.</span>

    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Street { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">private</span> <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span> Number { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">private</span> <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span> Address(Guid cityId, <span style="color: #0000ff;">string</span> street, <span style="color: #0000ff;">int</span><span style="color: #000000;"> number)
    {
        CityId </span>=<span style="color: #000000;"> cityId;
        Street </span>=<span style="color: #000000;"> street;
        Number </span>=<span style="color: #000000;"> number;
    }
}</span></pre>
</div>
<p>值对象基类覆盖了相等运算符（和其他相关的运算符和方法）来比较两个值对象</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> address1 = <span style="color: #0000ff;">new</span> Address(<span style="color: #0000ff;">new</span> Guid(<span style="color: #800000;">"</span><span style="color: #800000;">21C67A65-ED5A-4512-AA29-66308FAAB5AF</span><span style="color: #800000;">"</span>), <span style="color: #800000;">"</span><span style="color: #800000;">Baris Manco Street</span><span style="color: #800000;">"</span>, <span style="color: #800080;">42</span><span style="color: #000000;">);
</span><span style="color: #0000ff;">var</span> address2 = <span style="color: #0000ff;">new</span> Address(<span style="color: #0000ff;">new</span> Guid(<span style="color: #800000;">"</span><span style="color: #800000;">21C67A65-ED5A-4512-AA29-66308FAAB5AF</span><span style="color: #800000;">"</span>), <span style="color: #800000;">"</span><span style="color: #800000;">Baris Manco Street</span><span style="color: #800000;">"</span>, <span style="color: #800080;">42</span><span style="color: #000000;">);

Assert.Equal(address1, address2);
Assert.Equal(address1.GetHashCode(), address2.GetHashCode());
Assert.True(address1 </span>==<span style="color: #000000;"> address2);
Assert.False(address1 </span>!= address2);</pre>
</div>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a12"></a>十二、仓储</span></strong></span></p>
<p>是领域层与数据访问层的中介。每个实体（或聚合根）对应一个仓储</p>
<p>在领域层中定义仓储接口，在基础设施层实现</p>
<p>1，自定义仓储接口</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span> IPersonRepository : IRepository&lt;Person&gt;<span style="color: #000000;">
{
}</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span> IPersonRepository : IRepository&lt;Person, <span style="color: #0000ff;">long</span>&gt;<span style="color: #000000;">
{
}</span></pre>
</div>
<p>2，基类仓储接口方法</p>
<p>①获取单个实体</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">TEntity Get(TPrimaryKey id);
Task</span>&lt;TEntity&gt;<span style="color: #000000;"> GetAsync(TPrimaryKey id);
TEntity Single(Expression</span>&lt;Func&lt;TEntity, <span style="color: #0000ff;">bool</span>&gt;&gt;<span style="color: #000000;"> predicate);
Task</span>&lt;TEntity&gt; SingleAsync(Expression&lt;Func&lt;TEntity, <span style="color: #0000ff;">bool</span>&gt;&gt;<span style="color: #000000;"> predicate);
TEntity FirstOrDefault(TPrimaryKey id);
Task</span>&lt;TEntity&gt;<span style="color: #000000;"> FirstOrDefaultAsync(TPrimaryKey id);
TEntity FirstOrDefault(Expression</span>&lt;Func&lt;TEntity, <span style="color: #0000ff;">bool</span>&gt;&gt;<span style="color: #000000;"> predicate);
Task</span>&lt;TEntity&gt; FirstOrDefaultAsync(Expression&lt;Func&lt;TEntity, <span style="color: #0000ff;">bool</span>&gt;&gt;<span style="color: #000000;"> predicate);
TEntity Load(TPrimaryKey id);//不会从数据库中检索实体，而是延迟加载。&nbsp;（它在NHibernate中实现。 如果ORM提供程序未实现，Load方法与Get方法完全相同）</span></pre>
</div>
<p><strong>Get方法</strong>用于获取具有给定主键（Id）的实体。 如果数据库中没有给定Id的实体，它将抛出异常。 <strong>Single方法</strong>与Get类似，但需要一个表达式而不是Id。 所以，您可以编写一个lambda表达式来获取一个实体。 示例用法：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> person = _personRepository.Get(<span style="color: #800080;">42</span><span style="color: #000000;">);
</span><span style="color: #0000ff;">var</span> person = _personRepository.Single(p =&gt; p.Name == <span style="color: #800000;">"</span><span style="color: #800000;">John</span><span style="color: #800000;">"</span>);//请注意，如果没有给定条件的实体或有多个实体，Single方法将抛出异常。</pre>
</div>
<p>&nbsp;</p>
<p>②获取实体列表</p>
<div class="cnblogs_code">
<pre>List&lt;TEntity&gt;<span style="color: #000000;"> GetAllList();
Task</span>&lt;List&lt;TEntity&gt;&gt;<span style="color: #000000;"> GetAllListAsync();
List</span>&lt;TEntity&gt; GetAllList(Expression&lt;Func&lt;TEntity, <span style="color: #0000ff;">bool</span>&gt;&gt;<span style="color: #000000;"> predicate);
Task</span>&lt;List&lt;TEntity&gt;&gt; GetAllListAsync(Expression&lt;Func&lt;TEntity, <span style="color: #0000ff;">bool</span>&gt;&gt;<span style="color: #000000;"> predicate);
IQueryable</span>&lt;TEntity&gt; GetAll();</pre>
</div>
<p>GetAllList用于从数据库检索所有实体。 过载可用于过滤实体。 例子：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> allPeople =<span style="color: #000000;"> _personRepository.GetAllList();
</span><span style="color: #0000ff;">var</span> somePeople = _personRepository.GetAllList(person =&gt; person.IsActive &amp;&amp; person.Age &gt; <span style="color: #800080;">42</span>);</pre>
</div>
<p>GetAll返回IQueryable &lt;T&gt;。 所以，你可以添加Linq方法。 例子：</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">Example 1</span>
<span style="color: #0000ff;">var</span> query = <span style="color: #0000ff;">from</span> person <span style="color: #0000ff;">in</span><span style="color: #000000;"> _personRepository.GetAll()
            </span><span style="color: #0000ff;">where</span><span style="color: #000000;"> person.IsActive
            </span><span style="color: #0000ff;">orderby</span><span style="color: #000000;"> person.Name
            </span><span style="color: #0000ff;">select</span><span style="color: #000000;"> person;
</span><span style="color: #0000ff;">var</span> people =<span style="color: #000000;"> query.ToList();

</span><span style="color: #008000;">//</span><span style="color: #008000;">Example 2:</span>
List&lt;Person&gt; personList2 = _personRepository.GetAll().Where(p =&gt; p.Name.Contains(<span style="color: #800000;">"</span><span style="color: #800000;">H</span><span style="color: #800000;">"</span>)).OrderBy(p =&gt; p.Name).Skip(<span style="color: #800080;">40</span>).Take(<span style="color: #800080;">20</span>).ToList();</pre>
</div>
<p>③Insert</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">TEntity Insert(TEntity entity);
Task</span>&lt;TEntity&gt;<span style="color: #000000;"> InsertAsync(TEntity entity);
TPrimaryKey InsertAndGetId(TEntity entity);//方法返回新插入实体的ID
Task</span>&lt;TPrimaryKey&gt;<span style="color: #000000;"> InsertAndGetIdAsync(TEntity entity);
TEntity InsertOrUpdate(TEntity entity);//通过检查其Id值来插入或更新给定实体
Task</span>&lt;TEntity&gt;<span style="color: #000000;"> InsertOrUpdateAsync(TEntity entity);
TPrimaryKey InsertOrUpdateAndGetId(TEntity entity);//在插入或更新后返回实体的ID
Task</span>&lt;TPrimaryKey&gt; InsertOrUpdateAndGetIdAsync(TEntity entity);</pre>
</div>
<p>④Update</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">TEntity Update(TEntity entity);
Task</span>&lt;TEntity&gt; UpdateAsync(TEntity entity);</pre>
</div>
<p>大多数情况下，您不需要显式调用Update方法，因为在工作单元完成后，工作单元会自动保存所有更改</p>
<p>⑤Delete</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">void</span><span style="color: #000000;"> Delete(TEntity entity);
Task DeleteAsync(TEntity entity);
</span><span style="color: #0000ff;">void</span><span style="color: #000000;"> Delete(TPrimaryKey id);
Task DeleteAsync(TPrimaryKey id);
</span><span style="color: #0000ff;">void</span> Delete(Expression&lt;Func&lt;TEntity, <span style="color: #0000ff;">bool</span>&gt;&gt;<span style="color: #000000;"> predicate);
Task DeleteAsync(Expression</span>&lt;Func&lt;TEntity, <span style="color: #0000ff;">bool</span>&gt;&gt; predicate);</pre>
</div>
<p>⑥ASP.NET Boilerplate支持异步编程模型。 所以，存储库方法有Async版本。 这里，使用异步模型的示例应用程序服务方法：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> PersonAppService : AbpWpfDemoAppServiceBase, IPersonAppService
{
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span> IRepository&lt;Person&gt;<span style="color: #000000;"> _personRepository;

    </span><span style="color: #0000ff;">public</span> PersonAppService(IRepository&lt;Person&gt;<span style="color: #000000;"> personRepository)
    {
        _personRepository </span>=<span style="color: #000000;"> personRepository;
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task&lt;GetPeopleOutput&gt;<span style="color: #000000;"> GetAllPeople()
    {
        </span><span style="color: #0000ff;">var</span> people = <span style="color: #0000ff;">await</span><span style="color: #000000;"> _personRepository.GetAllListAsync();

        </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> GetPeopleOutput
        {
            People </span>= Mapper.Map&lt;List&lt;PersonDto&gt;&gt;<span style="color: #000000;">(people)
        };
    }
}</span></pre>
</div>
<p>自定义存储库方法不应包含业务逻辑或应用程序逻辑。 它应该只是执行与数据有关的或orm特定的任务。</p>
<p>　　</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a13"></a>十三、领域服务</span></strong></span></p>
<p>领域服务（或DDD中的服务）用于执行领域操作和业务规则。Eric Evans描述了一个好的服务应该具备下面三个特征：</p>
<ol>
<li>和领域概念相关的操作不是一个实体或者值对象的本质部分。</li>
<li>该接口是在领域模型的其他元素来定义的。</li>
<li>操作是无状态的。</li>
</ol>
<p>&nbsp;1，例子（假如我们有一个任务系统，并且将任务分配给一个人时，我们有业务规则）：</p>
<p>我们在这里有两个业务规则：</p>
<p>①任务应处于活动状态，以将其分配给新的人员。<br />②一个人最多可以有3个活动任务。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> ITaskManager : IDomainService
{
    </span><span style="color: #0000ff;">void</span><span style="color: #000000;"> AssignTaskToPerson(Task task, Person person);//将任务分配给人
}</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> TaskManager : DomainService, ITaskManager
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">const</span> <span style="color: #0000ff;">int</span> MaxActiveTaskCountForAPerson = <span style="color: #800080;">3</span><span style="color: #000000;">;

    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> ITaskRepository _taskRepository;

    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> TaskManager(ITaskRepository taskRepository)
    {
        _taskRepository </span>=<span style="color: #000000;"> taskRepository;
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> AssignTaskToPerson(Task task, Person person)
    {
        </span><span style="color: #0000ff;">if</span> (task.AssignedPersonId ==<span style="color: #000000;"> person.Id)
        {
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;">;
        }

        </span><span style="color: #0000ff;">if</span> (task.State !=<span style="color: #000000;"> TaskState.Active)
        {<br />　　　　　　　//认为这个一个应用程序错误
            </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> ApplicationException(<span style="color: #800000;">"</span><span style="color: #800000;">Can not assign a task to a person when task is not active!</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }

        </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (HasPersonMaximumAssignedTask(person))
        {<br />　　　　　　　//向用户展示错误
            </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> UserFriendlyException(L(<span style="color: #800000;">"</span><span style="color: #800000;">MaxPersonTaskLimitMessage</span><span style="color: #800000;">"</span><span style="color: #000000;">, person.Name));
        }

        task.AssignedPersonId </span>=<span style="color: #000000;"> person.Id;
    }

    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">bool</span><span style="color: #000000;"> HasPersonMaximumAssignedTask(Person person)
    {
        </span><span style="color: #0000ff;">var</span> assignedTaskCount = _taskRepository.Count(t =&gt; t.State == TaskState.Active &amp;&amp; t.AssignedPersonId ==<span style="color: #000000;"> person.Id);
        </span><span style="color: #0000ff;">return</span> assignedTaskCount &gt;=<span style="color: #000000;"> MaxActiveTaskCountForAPerson;
    }
}</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> TaskAppService : ApplicationService, ITaskAppService
{
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span> IRepository&lt;Task, <span style="color: #0000ff;">long</span>&gt;<span style="color: #000000;"> _taskRepository;
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span> IRepository&lt;Person&gt;<span style="color: #000000;"> _personRepository;
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> ITaskManager _taskManager;

    </span><span style="color: #0000ff;">public</span> TaskAppService(IRepository&lt;Task, <span style="color: #0000ff;">long</span>&gt; taskRepository, IRepository&lt;Person&gt;<span style="color: #000000;"> personRepository, ITaskManager taskManager)
    {
        _taskRepository </span>=<span style="color: #000000;"> taskRepository;
        _personRepository </span>=<span style="color: #000000;"> personRepository;
        _taskManager </span>=<span style="color: #000000;"> taskManager;
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> AssignTaskToPerson(AssignTaskToPersonInput input)
    {
        </span><span style="color: #0000ff;">var</span> task =<span style="color: #000000;"> _taskRepository.Get(input.TaskId);
        </span><span style="color: #0000ff;">var</span> person =<span style="color: #000000;"> _personRepository.Get(input.PersonId);

        _taskManager.AssignTaskToPerson(task, person);
    }
}</span></pre>
</div>
<p>2，强制使用领域服务</p>
<p>将任务实体设计成这样：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> Task : Entity&lt;<span style="color: #0000ff;">long</span>&gt;<span style="color: #000000;">
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">virtual</span> <span style="color: #0000ff;">int</span>? AssignedPersonId { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">...other members and codes of Task entity</span>

    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> AssignToPerson(Person person, ITaskPolicy taskPolicy)
    {
        taskPolicy.CheckIfCanAssignTaskToPerson(</span><span style="color: #0000ff;">this</span><span style="color: #000000;">, person);
        AssignedPersonId </span>=<span style="color: #000000;"> person.Id;
    }
}</span></pre>
</div>
<p>我们将AssignedPersonId的setter更改为protected。 所以，这个Task实体类不能被修改。 添加了一个AssignToPerson方法，该方法接受人员和任务策略。 CheckIfCanAssignTaskToPerson方法检查它是否是一个有效的赋值，如果没有，则抛出正确的异常（这里的实现不重要）。 那么应用服务方式就是这样的：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> AssignTaskToPerson(AssignTaskToPersonInput input)
{
    </span><span style="color: #0000ff;">var</span> task =<span style="color: #000000;"> _taskRepository.Get(input.TaskId);
    </span><span style="color: #0000ff;">var</span> person =<span style="color: #000000;"> _personRepository.Get(input.PersonId);

    task.AssignToPerson(person, _taskPolicy);
}</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a14"></a>十四、规格模式</span></strong></span></p>
<p>规格模式是一种特定的软件设计模式。通过使用布尔逻辑将业务规则链接在一起可以重组业务规则。在实际中，它主要用于为实体或其他业务对象定义可重用的过滤器</p>
<p>Abp定义了规范接口，和实现。使用时只需要继承Specification&lt;T&gt;</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span> ISpecification&lt;T&gt;<span style="color: #000000;">
{
    </span><span style="color: #0000ff;">bool</span><span style="color: #000000;"> IsSatisfiedBy(T obj);

    Expression</span>&lt;Func&lt;T, <span style="color: #0000ff;">bool</span>&gt;&gt;<span style="color: #000000;"> ToExpression();
}</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">拥有100,000美元余额的客户被认为是PREMIUM客户</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> PremiumCustomerSpecification : Specification&lt;Customer&gt;<span style="color: #000000;">
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> Expression&lt;Func&lt;Customer, <span style="color: #0000ff;">bool</span>&gt;&gt;<span style="color: #000000;"> ToExpression()
    {
        </span><span style="color: #0000ff;">return</span> (customer) =&gt; (customer.Balance &gt;= <span style="color: #800080;">100000</span><span style="color: #000000;">);
    }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">参数规范示例。</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> CustomerRegistrationYearSpecification : Specification&lt;Customer&gt;<span style="color: #000000;">
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span> Year { <span style="color: #0000ff;">get</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span> CustomerRegistrationYearSpecification(<span style="color: #0000ff;">int</span><span style="color: #000000;"> year)
    {
        Year </span>=<span style="color: #000000;"> year;
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> Expression&lt;Func&lt;Customer, <span style="color: #0000ff;">bool</span>&gt;&gt;<span style="color: #000000;"> ToExpression()
    {
        </span><span style="color: #0000ff;">return</span> (customer) =&gt; (customer.CreationYear ==<span style="color: #000000;"> Year);
    }
}</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> CustomerManager
{
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span> IRepository&lt;Customer&gt;<span style="color: #000000;"> _customerRepository;

    </span><span style="color: #0000ff;">public</span> CustomerManager(IRepository&lt;Customer&gt;<span style="color: #000000;"> customerRepository)
    {
        _customerRepository </span>=<span style="color: #000000;"> customerRepository;
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span> GetCustomerCount(ISpecification&lt;Customer&gt;<span style="color: #000000;"> spec)
    {
        </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> _customerRepository.Count(spec.ToExpression());
    }
}</span></pre>
</div>
<div class="cnblogs_code">
<pre>count = customerManager.GetCustomerCount(<span style="color: #0000ff;">new</span><span style="color: #000000;"> PremiumCustomerSpecification());
count </span>= customerManager.GetCustomerCount(<span style="color: #0000ff;">new</span> CustomerRegistrationYearSpecification(<span style="color: #800080;">2017</span>));</pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> count = customerManager.GetCustomerCount(<span style="color: #0000ff;">new</span> PremiumCustomerSpecification().And(<span style="color: #0000ff;">new</span> CustomerRegistrationYearSpecification(<span style="color: #800080;">2017</span>)));</pre>
</div>
<p>我们甚至可以从现有规范中创建一个新的规范类：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> NewPremiumCustomersSpecification : AndSpecification&lt;Customer&gt;<span style="color: #000000;">
{
    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> NewPremiumCustomersSpecification() 
        : </span><span style="color: #0000ff;">base</span>(<span style="color: #0000ff;">new</span> PremiumCustomerSpecification(), <span style="color: #0000ff;">new</span> CustomerRegistrationYearSpecification(<span style="color: #800080;">2017</span><span style="color: #000000;">))
    {
    }
}</span></pre>
</div>
<p>AndSpecification类是Specification类的一个子类，只有当两个规范都满足时才能满足。使用如下</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> count = customerManager.GetCustomerCount(<span style="color: #0000ff;">new</span> NewPremiumCustomersSpecification());</pre>
</div>
<p><strong>一般不需要使用规范类，可直接使用lambda表达式</strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> count = _customerRepository.Count(c =&gt; c.Balance &gt; <span style="color: #800080;">100000</span> &amp;&amp; c.CreationYear == <span style="color: #800080;">2017</span>);</pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a15"></a>十五、工作单元</span></strong></span></p>
<p>如果工作方法单元调用另一个工作单元方法，则使用相同的连接和事务。 第一个进入方法管理连接和事务，其他的使用它。</p>
<p>应用服务方法默认是工作单元。方法开始启动事务，方法结束提交事务。如果发生异常则回滚。这样应用服务方法中的所有数据库操作都将变为原子（工作单元）</p>
<p>1，显示使用工作单元</p>
<p>①在方法上引用[UnitOfWork]特性。如果是应用服务方法，则不需要应用此特性</p>
<p>②使用IUnitOfWorkManager</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyService
{
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> IUnitOfWorkManager _unitOfWorkManager;
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> IPersonRepository _personRepository;
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> IStatisticsRepository _statisticsRepository;

    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> MyService(IUnitOfWorkManager unitOfWorkManager, IPersonRepository personRepository, IStatisticsRepository statisticsRepository)
    {
        _unitOfWorkManager </span>=<span style="color: #000000;"> unitOfWorkManager;
        _personRepository </span>=<span style="color: #000000;"> personRepository;
        _statisticsRepository </span>=<span style="color: #000000;"> statisticsRepository;
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> CreatePerson(CreatePersonInput input)
    {
        </span><span style="color: #0000ff;">var</span> person = <span style="color: #0000ff;">new</span> Person { Name = input.Name, EmailAddress =<span style="color: #000000;"> input.EmailAddress };

        </span><span style="color: #0000ff;">using</span> (<span style="color: #0000ff;">var</span> unitOfWork =<span style="color: #000000;"> _unitOfWorkManager.Begin())
        {
            _personRepository.Insert(person);
            _statisticsRepository.IncrementPeopleCount();

            unitOfWork.Complete();
        }
    }
}</span></pre>
</div>
<p>2，禁用工作单元</p>
<div class="cnblogs_code">
<pre>[UnitOfWork(IsDisabled = <span style="color: #0000ff;">true</span><span style="color: #000000;">)]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">virtual</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> RemoveFriendship(RemoveFriendshipInput input)
{
    _friendshipRepository.Delete(input.Id);
}</span></pre>
</div>
<p>3，禁用事务功能</p>
<div class="cnblogs_code">
<pre>[UnitOfWork(isTransactional: <span style="color: #0000ff;">false</span><span style="color: #000000;">)]
</span><span style="color: #0000ff;">public</span><span style="color: #000000;"> GetTasksOutput GetTasks(GetTasksInput input)
{
    </span><span style="color: #0000ff;">var</span> tasks =<span style="color: #000000;"> _taskRepository.GetAllWithPeople(input.AssignedPersonId, input.State);
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> GetTasksOutput
            {
                Tasks </span>= Mapper.Map&lt;List&lt;TaskDto&gt;&gt;<span style="color: #000000;">(tasks)
            };
}</span></pre>
</div>
<p>4，自动保存更改<br />如果一个方法是工作单元，ASP.NET Boilerplate会自动在方法结束时保存所有更改。 假设我们需要更新一个人的名字的方法：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">[UnitOfWork]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> UpdateName(UpdateNameInput input)
{
    </span><span style="color: #0000ff;">var</span> person =<span style="color: #000000;"> _personRepository.Get(input.PersonId);
    person.Name </span>=<span style="color: #000000;"> input.NewName;
}</span></pre>
</div>
<p>5，更改工作单元配置</p>
<p>①通常在PreInitialize方法中完成</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SimpleTaskSystemCoreModule : AbpModule
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> PreInitialize()
    {
        Configuration.UnitOfWork.IsolationLevel </span>=<span style="color: #000000;"> IsolationLevel.ReadCommitted;
        Configuration.UnitOfWork.Timeout </span>= TimeSpan.FromMinutes(<span style="color: #800080;">30</span><span style="color: #000000;">);
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">...other module methods</span>
}</pre>
</div>
<p>6，如果访问工作单元</p>
<p>①如果您的类派生自某些特定的基类（ApplicationService，DomainService，AbpController，AbpApiController ...等），则可以直接使用CurrentUnitOfWork属性。<br />②您可以将IUnitOfWorkManager注入任何类并使用IUnitOfWorkManager.Current属性。</p>
<p>6，活动</p>
<p>工作单位已完成，失败和处理事件。 您可以注册这些事件并执行所需的操作。 例如，您可能希望在当前工作单元成功完成时运行一些代码。 例：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> CreateTask(CreateTaskInput input)
{
    </span><span style="color: #0000ff;">var</span> task = <span style="color: #0000ff;">new</span> Task { Description =<span style="color: #000000;"> input.Description };

    </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (input.AssignedPersonId.HasValue)
    {
        task.AssignedPersonId </span>=<span style="color: #000000;"> input.AssignedPersonId.Value;
        _unitOfWorkManager.Current.Completed </span>+= (sender, args) =&gt; { <span style="color: #008000;">/*</span><span style="color: #008000;"> TODO: Send email to assigned person </span><span style="color: #008000;">*/</span><span style="color: #000000;"> };
    }

    _taskRepository.Insert(task);
}</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a16"></a>十六、事件总线</span></strong></span></p>
<p>1，两种方式使用事件总线</p>
<p>①依赖注入IEventBus（属性注入比构造函数注入更适合于注入事件总线）</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> TaskAppService : ApplicationService
{
    </span><span style="color: #0000ff;">public</span> IEventBus EventBus { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> TaskAppService()
    {
        EventBus </span>=<span style="color: #000000;"> NullEventBus.Instance;//NullEventBus实现空对象模式。 当你调用它的方法时，它什么都不做
    }
}</span></pre>
</div>
<p>②获取默认实例（不建议直接使用EventBus.Default，因为它使得单元测试变得更加困难。）</p>
<p>如果不能注入，可以直接使用EventBus.Default</p>
<div class="cnblogs_code">
<pre>EventBus.Default.Trigger(...); <span style="color: #008000;">//</span><span style="color: #008000;">trigger an event</span></pre>
</div>
<p>2，定义事件（&nbsp;EventData类定义EventSource（哪个对象触发事件）和EventTime（触发时）属性）</p>
<p>在触发事件之前，应首先定义事件。 事件由派生自EventData的类表示。 假设我们要在任务完成时触发事件：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> TaskCompletedEventData : EventData
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span> TaskId { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}</span></pre>
</div>
<p>3，预定义事件</p>
<p>①AbpHandledExceptionData：任何异常时触发此事件</p>
<p>②实体变更<br />还有用于实体更改的通用事件数据类：EntityCreatingEventData &lt;TEntity&gt;，EntityCreatedEventData &lt;TEntity&gt;，EntityUpdatingEventData &lt;TEntity&gt;，EntityUpdatedEventData &lt;TEntity&gt;，EntityDeletingEventData &lt;TEntity&gt;和EntityDeletedEventData &lt;TEntity&gt;。 另外还有EntityChangingEventData &lt;TEntity&gt;和EntityChangedEventData &lt;TEntity&gt;。 可以插入，更新或删除更改。</p>
<p>"ing"：保存之前</p>
<p>"ed"：保存之后</p>
<p>4，触发事件</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> TaskAppService : ApplicationService
{
    </span><span style="color: #0000ff;">public</span> IEventBus EventBus { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> TaskAppService()
    {
        EventBus </span>=<span style="color: #000000;"> NullEventBus.Instance;
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> CompleteTask(CompleteTaskInput input)
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;">TODO: complete the task on database...</span>
        EventBus.Trigger(<span style="color: #0000ff;">new</span> TaskCompletedEventData {TaskId = <span style="color: #800080;">42</span><span style="color: #000000;">});
    }
}</span></pre>
</div>
<div class="cnblogs_code">
<pre>EventBus.Trigger&lt;TaskCompletedEventData&gt;(<span style="color: #0000ff;">new</span> TaskCompletedEventData { TaskId = <span style="color: #800080;">42</span> }); <span style="color: #008000;">//</span><span style="color: #008000;">明确地声明泛型参数</span>
EventBus.Trigger(<span style="color: #0000ff;">this</span>, <span style="color: #0000ff;">new</span> TaskCompletedEventData { TaskId = <span style="color: #800080;">42</span> }); <span style="color: #008000;">//</span><span style="color: #008000;">将&ldquo;事件源&rdquo;设置为&ldquo;this&rdquo;</span>
EventBus.Trigger(<span style="color: #0000ff;">typeof</span>(TaskCompletedEventData), <span style="color: #0000ff;">this</span>, <span style="color: #0000ff;">new</span> TaskCompletedEventData { TaskId = <span style="color: #800080;">42</span> }); <span style="color: #008000;">//</span><span style="color: #008000;">调用非泛型版本（第一个参数是事件类的类型）</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> ActivityWriter : IEventHandler&lt;TaskCompletedEventData&gt;<span style="color: #000000;">, ITransientDependency
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> HandleEvent(TaskCompletedEventData eventData)
    {
        WriteActivity(</span><span style="color: #800000;">"</span><span style="color: #800000;">A task is completed by id = </span><span style="color: #800000;">"</span> +<span style="color: #000000;"> eventData.TaskId);
    }
}</span></pre>
</div>
<p>5，处理多个事件</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ActivityWriter : 
    IEventHandler</span>&lt;TaskCompletedEventData&gt;<span style="color: #000000;">, 
    IEventHandler</span>&lt;TaskCreatedEventData&gt;<span style="color: #000000;">, 
    ITransientDependency
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> HandleEvent(TaskCompletedEventData eventData)
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;">TODO: handle the event...</span>
<span style="color: #000000;">    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> HandleEvent(TaskCreatedEventData eventData)
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;">TODO: handle the event...</span>
<span style="color: #000000;">    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a17"></a>十七、数据过滤器</span></strong></span></p>
<p>1，ISoftDelete软删除接口</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Person : Entity, ISoftDelete
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">virtual</span> <span style="color: #0000ff;">string</span> Name { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">virtual</span> <span style="color: #0000ff;">bool</span> IsDeleted { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}</span></pre>
</div>
<p>使用IRepository.Delete方法时将IsDeleted属性设置为true。_personRepository.GetAllList()不会查询出软删除的数据</p>
<p><span style="color: #ff0000;">注：如果您实现IDeletionAudited（扩展了ISoftDelete），则删除时间和删除用户标识也由ASP.NET Boilerplate自动设置。</span></p>
<p>2，&nbsp;IMustHaveTenant</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Product : Entity, IMustHaveTenant
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span> TenantId { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Name { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}</span></pre>
</div>
<p>IMustHaveTenant定义TenantId来区分不同的租户实体。 ASP.NET Boilerplate默认使用IAbpSession获取当前TenantId，并自动过滤当前租户的查询。</p>
<p>如果当前用户未登录到系统，或者当前用户是主机用户（主机用户是可管理租户和租户数据的上级用户），ASP.NET Boilerplate将自动禁用IMustHaveTenant过滤器。 因此，所有租户的所有数据都可以被检索到应用程序</p>
<p>3，IMayHaveTenant（没有IMustHaveTenant常用）</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Role : Entity, IMayHaveTenant
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span>? TenantId { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> RoleName { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}</span></pre>
</div>
<p>空值表示这是主机实体，非空值表示由租户拥有的该实体，其ID为TenantId</p>
<p>4，禁用过滤器</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> people1 = _personRepository.GetAllList();<span style="color: #008000;">//</span><span style="color: #008000;">访问未删除的</span>

<span style="color: #0000ff;">using</span><span style="color: #000000;"> (_unitOfWorkManager.Current.DisableFilter(AbpDataFilters.SoftDelete))
{
    </span><span style="color: #0000ff;">var</span> people2 = _personRepository.GetAllList(); <span style="color: #008000;">//</span><span style="color: #008000;">访问所有的        </span>
<span style="color: #000000;">}

</span><span style="color: #0000ff;">var</span> people3 = _personRepository.GetAllList();<span style="color: #008000;">//</span><span style="color: #008000;">访问未删除的</span></pre>
</div>
<p>5，全局禁用过滤器<br />如果需要，可以全局禁用预定义的过滤器。 例如，要全局禁用软删除过滤器，请将此代码添加到模块的PreInitialize方法中：</p>
<div class="cnblogs_code">
<pre>Configuration.UnitOfWork.OverrideFilter(AbpDataFilters.SoftDelete, <span style="color: #0000ff;">false</span>);</pre>
</div>
<p>&nbsp;6，自定义过滤器</p>
<p>①定义过滤字段</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IHasPerson
{
    </span><span style="color: #0000ff;">int</span> PersonId { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}</span></pre>
</div>
<p>②实体实现接口</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Phone : Entity, IHasPerson
{
    [ForeignKey(</span><span style="color: #800000;">"</span><span style="color: #800000;">PersonId</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">virtual</span> Person Person { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">virtual</span> <span style="color: #0000ff;">int</span> PersonId { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">virtual</span> <span style="color: #0000ff;">string</span> Number { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}</span></pre>
</div>
<p>③定义过滤器</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> OnModelCreating(DbModelBuilder modelBuilder)
{
    </span><span style="color: #0000ff;">base</span><span style="color: #000000;">.OnModelCreating(modelBuilder);

    modelBuilder.Filter(</span><span style="color: #800000;">"</span><span style="color: #800000;">PersonFilter</span><span style="color: #800000;">"</span>, (IHasPerson entity, <span style="color: #0000ff;">int</span> personId) =&gt; entity.PersonId == personId, <span style="color: #800080;">0</span><span style="color: #000000;">);
}</span></pre>
</div>
<p>&ldquo;PersonFilter&rdquo;是此处过滤器的唯一名称。 第二个参数定义了过滤器接口和personId过滤器参数（如果过滤器不是参数，则不需要），最后一个参数是personId的默认值。</p>
<p>最后，我们必须在本模块的PreInitialize方法中向ASP.NET Boilerplate的工作单元注册此过滤器：</p>
<div class="cnblogs_code">
<pre>Configuration.UnitOfWork.RegisterFilter(<span style="color: #800000;">"</span><span style="color: #800000;">PersonFilter</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">false</span>);</pre>
</div>
<p>第一个参数是我们之前定义的唯一的名称。 第二个参数表示默认情况下是启用还是禁用此过滤器</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">using</span> (CurrentUnitOfWork.EnableFilter(<span style="color: #800000;">"</span><span style="color: #800000;">PersonFilter</span><span style="color: #800000;">"</span><span style="color: #000000;">))
{
    </span><span style="color: #0000ff;">using</span>(CurrentUnitOfWork.SetFilterParameter(<span style="color: #800000;">"</span><span style="color: #800000;">PersonFilter</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">personId</span><span style="color: #800000;">"</span>, <span style="color: #800080;">42</span><span style="color: #000000;">))
    {
        </span><span style="color: #0000ff;">var</span> phones =<span style="color: #000000;"> _phoneRepository.GetAllList();
        </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">    }
}</span></pre>
</div>
<p>我们可以从某个来源获取personId，而不是静态编码。 以上示例是参数化过滤器。 滤波器可以有零个或多个参数。 如果没有参数，则不需要设置过滤器参数值。 此外，如果默认情况下启用，则不需要手动启用它（当然，我们可以禁用它）。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a18"></a>十八、应用服务</span></strong></span></p>
<p>1，CrudAppService和AsyncCrudAppService类</p>
<p>如果您需要创建一个应用程序服务，该服务将为特定实体创建&ldquo;创建&rdquo;，&ldquo;更新&rdquo;，&ldquo;删除&rdquo;，&ldquo;获取&rdquo;GetAll方法，则可以从CrudAppService继承（如果要创建异步方法，则可以继承AsyncCrudAppService）类来创建它。 CrudAppService基类是通用的，它将相关的实体和DTO类型作为通用参数，并且是可扩展的，允许您在需要自定义时重写功能。</p>
<p>①实体类</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Task : Entity, IHasCreationTime
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Title { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Description { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span> DateTime CreationTime { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span> TaskState State { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span> Person AssignedPerson { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    </span><span style="color: #0000ff;">public</span> Guid? AssignedPersonId { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Task()
    {
        CreationTime </span>=<span style="color: #000000;"> Clock.Now;
        State </span>=<span style="color: #000000;"> TaskState.Open;
    }
}</span></pre>
</div>
<p>②创建DTO</p>
<div class="cnblogs_code">
<pre>[AutoMap(<span style="color: #0000ff;">typeof</span><span style="color: #000000;">(Task))]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> TaskDto : EntityDto, IHasCreationTime
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Title { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Description { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span> DateTime CreationTime { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span> TaskState State { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span> Guid? AssignedPersonId { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> AssignedPersonName { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}</span></pre>
</div>
<p>③应用服务</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> TaskAppService : AsyncCrudAppService&lt;Task, TaskDto&gt;,<strong>ITaskAppService</strong></pre>
<pre><span style="color: #000000;"> { </span><span style="color: #0000ff;">public</span> TaskAppService(IRepository&lt;Task&gt;<span style="color: #000000;"> repository) : </span><span style="color: #0000ff;">base</span><span style="color: #000000;">(repository) { } }</span></pre>
</div>
<p>④应用服务接口</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span> ITaskAppService : IAsyncCrudAppService&lt;TaskDto&gt;<span style="color: #000000;">
{
        
}</span></pre>
</div>
<p>2，自定义CURD应用服务</p>
<p>1，查询</p>
<p>PagedAndSortedResultRequestDto，它提供可选的排序和分页参数。可以定义派生类过滤</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> GetAllTasksInput : PagedAndSortedResultRequestDto
{
    </span><span style="color: #0000ff;">public</span> TaskState? State { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}</span></pre>
</div>
<p>现在，我们应该更改TaskAppService以应用自定义过滤器</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> TaskAppService : AsyncCrudAppService&lt;Task, TaskDto, <span style="color: #0000ff;">int</span>, GetAllTasksInput&gt;<span style="color: #000000;">
{
    </span><span style="color: #0000ff;">public</span> TaskAppService(IRepository&lt;Task&gt;<span style="color: #000000;"> repository)
        : </span><span style="color: #0000ff;">base</span><span style="color: #000000;">(repository)
    {

    }

    </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span> IQueryable&lt;Task&gt;<span style="color: #000000;"> CreateFilteredQuery(GetAllTasksInput input)
    {
        </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">base</span><span style="color: #000000;">.CreateFilteredQuery(input)
            .WhereIf(input.State.HasValue, t </span>=&gt; t.State ==<span style="color: #000000;"> input.State.Value);
    }
}</span></pre>
</div>
<p>2，创建和更新</p>
<p>创建一个CreateTaskInput类&nbsp;</p>
<div class="cnblogs_code">
<pre>[AutoMapTo(<span style="color: #0000ff;">typeof</span><span style="color: #000000;">(Task))]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> CreateTaskInput
{
    [Required]
    [MaxLength(Task.MaxTitleLength)]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Title { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    [MaxLength(Task.MaxDescriptionLength)]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Description { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span> Guid? AssignedPersonId { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}</span></pre>
</div>
<p>并创建一个UpdateTaskInput类</p>
<div class="cnblogs_code">
<pre>[AutoMapTo(<span style="color: #0000ff;">typeof</span><span style="color: #000000;">(Task))]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> UpdateTaskInput : CreateTaskInput, IEntityDto
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span> Id { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span> TaskState State { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}</span></pre>
</div>
<p>现在，我们可以将这些DTO类作为AsyncCrudAppService类的通用参数，如下所示：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> TaskAppService : AsyncCrudAppService&lt;Task, TaskDto, <span style="color: #0000ff;">int</span>, GetAllTasksInput, CreateTaskInput, UpdateTaskInput&gt;<span style="color: #000000;">
{
    </span><span style="color: #0000ff;">public</span> TaskAppService(IRepository&lt;Task&gt;<span style="color: #000000;"> repository)
        : </span><span style="color: #0000ff;">base</span><span style="color: #000000;">(repository)
    {

    }

    </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span> IQueryable&lt;Task&gt;<span style="color: #000000;"> CreateFilteredQuery(GetAllTasksInput input)
    {
        </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">base</span><span style="color: #000000;">.CreateFilteredQuery(input)
            .WhereIf(input.State.HasValue, t </span>=&gt; t.State ==<span style="color: #000000;"> input.State.Value);
    }
}</span></pre>
</div>
<p>3，CURD权限</p>
<p>您可能需要授权您的CRUD方法。 您可以设置预定义的权限属性：GetPermissionName，GetAllPermissionName，CreatePermissionName，UpdatePermissionName和DeletePermissionName。 如果您设置它们，基本CRUD类将自动检查权限。 您可以在构造函数中设置它，如下所示：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> TaskAppService : AsyncCrudAppService&lt;Task, TaskDto&gt;<span style="color: #000000;">
{
    </span><span style="color: #0000ff;">public</span> TaskAppService(IRepository&lt;Task&gt;<span style="color: #000000;"> repository) 
        : </span><span style="color: #0000ff;">base</span><span style="color: #000000;">(repository)
    {
        CreatePermissionName </span>= <span style="color: #800000;">"</span><span style="color: #800000;">MyTaskCreationPermission</span><span style="color: #800000;">"</span><span style="color: #000000;">;
    }
}</span></pre>
</div>
<p>或者，您可以覆盖适当的权限检查方法来手动检查权限：CheckGetPermission（），CheckGetAllPermission（），CheckCreatePermission（），CheckUpdatePermission（），CheckDeletePermission（）。 默认情况下，它们都调用具有相关权限名称的CheckPermission（...）方法，该方法只需调用IPermissionChecker.Authorize（...）方法即可。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a19"></a>十九、数据传输对象</span></strong></span></p>
<p>1，帮助接口和类</p>
<p>ILimitedResultRequest定义MaxResultCount属性。 因此，您可以在输入的DTO中实现它，以便对限制结果集进行标准化。</p>
<p>IPagedResultRequest通过添加SkipCount扩展ILimitedResultRequest。 所以，我们可以在SearchPeopleInput中实现这个接口进行分页：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SearchPeopleInput : IPagedResultRequest
{
    [StringLength(</span><span style="color: #800080;">40</span>, MinimumLength = <span style="color: #800080;">1</span><span style="color: #000000;">)]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> SearchedName { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span> MaxResultCount { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span> SkipCount { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a20"></a>二十、验证数据传输对象</span></strong></span></p>
<p>1，使用数据注解（<strong>System.ComponentModel.DataAnnotations</strong>）</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> CreateTaskInput
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span>? AssignedPersonId { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    [Required]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Description { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}</span></pre>
</div>
<p>2，自定义验证</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> CreateTaskInput : ICustomValidate
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span>? AssignedPersonId { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">bool</span> SendEmailToAssignedPerson { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    [Required]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Description { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> AddValidationErrors(CustomValidatationContext context)
    {
        </span><span style="color: #0000ff;">if</span> (SendEmailToAssignedPerson &amp;&amp; (!AssignedPersonId.HasValue || AssignedPersonId.Value &lt;= <span style="color: #800080;">0</span><span style="color: #000000;">))
        {
            context.Results.Add(</span><span style="color: #0000ff;">new</span> ValidationResult(<span style="color: #800000;">"</span><span style="color: #800000;">AssignedPersonId must be set if SendEmailToAssignedPerson is true!</span><span style="color: #800000;">"</span><span style="color: #000000;">));
        }
    }
}</span></pre>
</div>
<p>3，Normalize方法在验证之后调用（并在调用方法之前）</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> GetTasksInput : IShouldNormalize
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Sorting { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Normalize()
    {
        </span><span style="color: #0000ff;">if</span> (<span style="color: #0000ff;">string</span><span style="color: #000000;">.IsNullOrWhiteSpace(Sorting))
        {
            Sorting </span>= <span style="color: #800000;">"</span><span style="color: #800000;">Name ASC</span><span style="color: #800000;">"</span><span style="color: #000000;">;
        }
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a21"></a>二十一、授权</span></strong></span></p>
<p>1，定义权限</p>
<p>①不同的模块可以有不同的权限。 一个模块应该创建一个派生自AuthorizationProvider的类来定义它的权限</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyAuthorizationProvider : AuthorizationProvider
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> SetPermissions(IPermissionDefinitionContext context)
    {
        </span><span style="color: #0000ff;">var</span> administration = context.CreatePermission(<span style="color: #800000;">"</span><span style="color: #800000;">Administration</span><span style="color: #800000;">"</span><span style="color: #000000;">);

        </span><span style="color: #0000ff;">var</span> userManagement = administration.CreateChildPermission(<span style="color: #800000;">"</span><span style="color: #800000;">Administration.UserManagement</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        userManagement.CreateChildPermission(</span><span style="color: #800000;">"</span><span style="color: #800000;">Administration.UserManagement.CreateUser</span><span style="color: #800000;">"</span><span style="color: #000000;">);

        </span><span style="color: #0000ff;">var</span> roleManagement = administration.CreateChildPermission(<span style="color: #800000;">"</span><span style="color: #800000;">Administration.RoleManagement</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    }
}
    </span></pre>
</div>
<p>IPermissionDefinitionContext属性定义：</p>
<p><span style="font-size: 12px;">Name：一个系统内的唯一名称，&nbsp;最好为权限名称</span></p>
<p><span style="font-size: 12px;">Display name：一个可本地化的字符串，可以在UI中稍后显示权限</span></p>
<p><span style="font-size: 12px;">Description：一个可本地化的字符串，可用于显示权限的定义，稍后在UI中</span></p>
<p><span style="font-size: 12px;">MultiTenancySides：对于多租户申请，租户或主机可以使用许可。 这是一个Flags枚举，因此可以在双方使用权限。</span></p>
<p><span style="font-size: 12px;">featureDependency：可用于声明对功能的依赖。 因此，仅当满足特征依赖性时，才允许该权限。 它等待一个对象实现IFeatureDependency。 默认实现是SimpleFeatureDependency类。 示例用法：new SimpleFeatureDependency（&ldquo;MyFeatureName&rdquo;）</span></p>
<p>②权限可以具有父权限和子级权限。 虽然这并不影响权限检查，但可能有助于在UI中分组权限。</p>
<p>③创建授权提供者后，我们应该在我们的模块的PreInitialize方法中注册它：</p>
<div class="cnblogs_code">
<pre>Configuration.Authorization.Providers.Add&lt;MyAuthorizationProvider&gt;();</pre>
</div>
<p>2，检查权限</p>
<p>①使用AbpAuthorize特性</p>
<div class="cnblogs_code">
<pre>[AbpAuthorize(<span style="color: #800000;">"</span><span style="color: #800000;">Administration.UserManagement.CreateUser</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> CreateUser(CreateUserInput input)
{
    </span><span style="color: #008000;">//</span><span style="color: #008000;">如果未授予&ldquo;Administration.UserManagement.CreateUser&rdquo;权限，用户将无法执行此方法。</span>
}</pre>
</div>
<p>AbpAuthorize属性还会检查当前用户是否已登录（使用IAbpSession.UserId）。 所以，如果我们为一个方法声明一个AbpAuthorize，它只检查登录：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">[AbpAuthorize]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> SomeMethod(SomeMethodInput input)
{
    </span><span style="color: #008000;">//</span><span style="color: #008000;">如果用户无法登录，则无法执行此方法。</span>
}</pre>
</div>
<p>②Abp授权属性说明</p>
<p><span style="font-size: 12px;">ASP.NET Boilerplate使用动态方法截取功能进行授权。 所以方法使用AbpAuthorize属性有一些限制。</span></p>
<p><span style="font-size: 12px;">不能用于私有方法。</span><br /><span style="font-size: 12px;">不能用于静态方法。</span><br /><span style="font-size: 12px;">不能用于非注入类的方法（我们必须使用依赖注入）。</span></p>
<p><span style="font-size: 12px;">此外</span></p>
<p><span style="font-size: 12px;">如果方法通过接口调用（如通过接口使用的应用程序服务），可以将其用于任何公共方法。</span><br /><span style="font-size: 12px;">如果直接从类引用（如ASP.NET MVC或Web API控制器）调用，则该方法应该是虚拟的。</span><br /><span style="font-size: 12px;">如果保护方法应该是虚拟的。</span></p>
<p>注意：有四种类型的授权属性：</p>
<p>在应用服务（应用层）中，我们使用Abp.Authorization.AbpAuthorize属性。<br />在MVC控制器（Web层）中，我们使用Abp.Web.Mvc.Authorization.AbpMvcAuthorize属性。<br />在ASP.NET Web API中，我们使用Abp.WebApi.Authorization.AbpApiAuthorize属性。<br />在ASP.NET Core中，我们使用Abp.AspNetCore.Mvc.Authorization.AbpMvcAuthorize属性。</p>
<p>③禁止授权</p>
<p>您可以通过将AbpAllowAnonymous属性添加到应用程序服务来禁用方法/类的授权。 对MVC，Web API和ASP.NET核心控制器使用AllowAnonymous，这些框架是这些框架的本机属性。</p>
<p>④使用IPermissionChecker&nbsp;</p>
<p>虽然AbpAuthorize属性在大多数情况下足够好，但是必须有一些情况需要检查方法体中的权限。 我们可以注入和使用IPermissionChecker，如下例所示：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> CreateUser(CreateOrUpdateUserInput input)
{
    </span><span style="color: #0000ff;">if</span> (!PermissionChecker.IsGranted(<span style="color: #800000;">"</span><span style="color: #800000;">Administration.UserManagement.CreateUser</span><span style="color: #800000;">"</span><span style="color: #000000;">))
    {
        </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> AbpAuthorizationException(<span style="color: #800000;">"</span><span style="color: #800000;">您无权创建用户！</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    }
    </span><span style="color: #008000;">//</span><span style="color: #008000;">如果用户未授予&ldquo;Administration.UserManagement.CreateUser&rdquo;权限，则无法达到此目的。</span>
}</pre>
</div>
<p>当然，您可以编写任何逻辑，因为IsGranted只返回true或false（也有Async版本）。 如果您只是检查权限并抛出如上所示的异常，则可以使用Authorize方法：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> CreateUser(CreateOrUpdateUserInput input)
{
    PermissionChecker.Authorize(</span><span style="color: #800000;">"</span><span style="color: #800000;">Administration.UserManagement.CreateUser</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    </span><span style="color: #008000;">//</span><span style="color: #008000;">如果用户未授予&ldquo;Administration.UserManagement.CreateUser&rdquo;权限，则无法达到此目的。</span>
}</pre>
</div>
<p>由于授权被广泛使用，ApplicationService和一些常见的基类注入并定义了PermissionChecker属性。 因此，可以在不注入应用程序服务类的情况下使用权限检查器。</p>
<p>⑤Razor 视图</p>
<p>基本视图类定义IsGranted方法来检查当前用户是否具有权限。 因此，我们可以有条件地呈现视图。 例：</p>
<div class="cnblogs_code">
<pre>@if (IsGranted(<span style="color: #800000;">"</span><span style="color: #800000;">Administration.UserManagement.CreateUser</span><span style="color: #800000;">"</span><span style="color: #000000;">))
{
    </span>&lt;button id=<span style="color: #800000;">"</span><span style="color: #800000;">CreateNewUserButton</span><span style="color: #800000;">"</span> <span style="color: #0000ff;">class</span>=<span style="color: #800000;">"</span><span style="color: #800000;">btn btn-primary</span><span style="color: #800000;">"</span>&gt;&lt;i <span style="color: #0000ff;">class</span>=<span style="color: #800000;">"</span><span style="color: #800000;">fa fa-plus</span><span style="color: #800000;">"</span>&gt;&lt;/i&gt; @L(<span style="color: #800000;">"</span><span style="color: #800000;">CreateNewUser</span><span style="color: #800000;">"</span>)&lt;/button&gt;<span style="color: #000000;">
}</span></pre>
</div>
<p>客户端（Javascript）<br />在客户端，我们可以使用在abp.auth命名空间中定义的API。 在大多数情况下，我们需要检查当前用户是否具有特定权限（具有权限名称）。 例：</p>
<div class="cnblogs_code">
<pre>abp.auth.isGranted(<span style="color: #800000;">'</span><span style="color: #800000;">Administration.UserManagement.CreateUser</span><span style="color: #800000;">'</span>);</pre>
</div>
<p>您还可以使用abp.auth.grantedPermissions获取所有授予的权限，或者使用abp.auth.allPermissions获取应用程序中的所有可用权限名称。 在运行时检查其他人的abp.auth命名空间。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a22"></a>二十二、功能管理</span></strong></span></p>
<p>大多数SaaS（多租户）应用程序都有具有不同功能的版本（包）。 因此，他们可以向租户（客户）提供不同的价格和功能选项。</p>
<p>1，定义功能<br />检查前应定义特征。 模块可以通过从FeatureProvider类派生来定义自己的特征。 在这里，一个非常简单的功能提供者定义了3个功能：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> AppFeatureProvider : FeatureProvider
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> SetFeatures(IFeatureDefinitionContext context)
    {<br />　　　　　//识别功能的唯一名称（作为字符串）.默认值
        </span><span style="color: #0000ff;">var</span> sampleBooleanFeature = context.Create(<span style="color: #800000;">"</span><span style="color: #800000;">SampleBooleanFeature</span><span style="color: #800000;">"</span>, defaultValue: <span style="color: #800000;">"</span><span style="color: #800000;">false</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        sampleBooleanFeature.CreateChildFeature(</span><span style="color: #800000;">"</span><span style="color: #800000;">SampleNumericFeature</span><span style="color: #800000;">"</span>, defaultValue: <span style="color: #800000;">"</span><span style="color: #800000;">10</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        context.Create(</span><span style="color: #800000;">"</span><span style="color: #800000;">SampleSelectionFeature</span><span style="color: #800000;">"</span>, defaultValue: <span style="color: #800000;">"</span><span style="color: #800000;">B</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    }
}</span></pre>
</div>
<p>创建功能提供者后，我们应该在模块的PreInitialize方法中注册，如下所示：</p>
<div class="cnblogs_code">
<pre>Configuration.Features.Providers.Add&lt;AppFeatureProvider&gt;();</pre>
</div>
<p>其他功能属性<br />虽然需要唯一的名称和默认值属性，但是有一些可选的属性用于详细控制。</p>
<p>Scope：FeatureScopes枚举中的值。 它可以是版本（如果此功能只能为版本级设置），租户（如果此功能只能为租户级别设置）或全部（如果此功能可以为版本和租户设置，租户设置覆盖其版本的 设置）。 默认值为全部。<br />DisplayName：一个可本地化的字符串，用于向用户显示该功能的名称。<br />Description：一个可本地化的字符串，用于向用户显示该功能的详细说明。<br />InputType：功能的UI输入类型。 这可以定义，然后可以在创建自动功能屏幕时使用。<br />Attributes：键值对的任意自定义词典可以与特征相关。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> AppFeatureProvider : FeatureProvider
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> SetFeatures(IFeatureDefinitionContext context)
    {
        </span><span style="color: #0000ff;">var</span> sampleBooleanFeature =<span style="color: #000000;"> context.Create(
            AppFeatures.SampleBooleanFeature,
            defaultValue: </span><span style="color: #800000;">"</span><span style="color: #800000;">false</span><span style="color: #800000;">"</span><span style="color: #000000;">,
            displayName: L(</span><span style="color: #800000;">"</span><span style="color: #800000;">Sample boolean feature</span><span style="color: #800000;">"</span><span style="color: #000000;">),
            inputType: </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> CheckboxInputType()
            );

        sampleBooleanFeature.CreateChildFeature(
            AppFeatures.SampleNumericFeature,
            defaultValue: </span><span style="color: #800000;">"</span><span style="color: #800000;">10</span><span style="color: #800000;">"</span><span style="color: #000000;">,
            displayName: L(</span><span style="color: #800000;">"</span><span style="color: #800000;">Sample numeric feature</span><span style="color: #800000;">"</span><span style="color: #000000;">),
            inputType: </span><span style="color: #0000ff;">new</span> SingleLineStringInputType(<span style="color: #0000ff;">new</span> NumericValueValidator(<span style="color: #800080;">1</span>, <span style="color: #800080;">1000000</span><span style="color: #000000;">))
            );

        context.Create(
            AppFeatures.SampleSelectionFeature,
            defaultValue: </span><span style="color: #800000;">"</span><span style="color: #800000;">B</span><span style="color: #800000;">"</span><span style="color: #000000;">,
            displayName: L(</span><span style="color: #800000;">"</span><span style="color: #800000;">Sample selection feature</span><span style="color: #800000;">"</span><span style="color: #000000;">),
            inputType: </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> ComboboxInputType(
                </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> StaticLocalizableComboboxItemSource(
                    </span><span style="color: #0000ff;">new</span> LocalizableComboboxItem(<span style="color: #800000;">"</span><span style="color: #800000;">A</span><span style="color: #800000;">"</span>, L(<span style="color: #800000;">"</span><span style="color: #800000;">Selection A</span><span style="color: #800000;">"</span><span style="color: #000000;">)),
                    </span><span style="color: #0000ff;">new</span> LocalizableComboboxItem(<span style="color: #800000;">"</span><span style="color: #800000;">B</span><span style="color: #800000;">"</span>, L(<span style="color: #800000;">"</span><span style="color: #800000;">Selection B</span><span style="color: #800000;">"</span><span style="color: #000000;">)),
                    </span><span style="color: #0000ff;">new</span> LocalizableComboboxItem(<span style="color: #800000;">"</span><span style="color: #800000;">C</span><span style="color: #800000;">"</span>, L(<span style="color: #800000;">"</span><span style="color: #800000;">Selection C</span><span style="color: #800000;">"</span><span style="color: #000000;">))
                    )
                )
            );
    }

    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> ILocalizableString L(<span style="color: #0000ff;">string</span><span style="color: #000000;"> name)
    {
        </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> LocalizableString(name, AbpZeroTemplateConsts.LocalizationSourceName);
    }
}</span></pre>
</div>
<p>功能层次结构<br />如示例功能提供者所示，功能可以具有子功能。 父功能通常定义为布尔特征。 子功能仅在启用父级时才可用。 ASP.NET Boilerplate不执行但建议这一点。 应用程序应该照顾它。</p>
<p>&nbsp;</p>
<p>2，检查功能</p>
<p>我们定义一个功能来检查应用程序中的值，以允许或阻止每个租户的某些应用程序功能。 有不同的检查方式。</p>
<p>①使用RequiresFeature属性</p>
<div class="cnblogs_code">
<pre>[RequiresFeature(<span style="color: #800000;">"</span><span style="color: #800000;">ExportToExcel</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task&lt;FileDto&gt;<span style="color: #000000;"> GetReportToExcel(...)
{
    ...
}</span></pre>
</div>
<p>只有对当前租户启用了&ldquo;ExportToExcel&rdquo;功能（当前租户从IAbpSession获取），才执行此方法。 如果未启用，则会自动抛出AbpAuthorizationException异常。</p>
<p>当然，RequiresFeature属性应该用于布尔类型的功能。 否则，你可能会得到异常。</p>
<p>②RequiresFeature属性注释</p>
<p><span style="font-size: 12px;">ASP.NET Boilerplate使用动态方法截取功能进行功能检查。 所以，方法使用RequiresFeature属性有一些限制。</span></p>
<p><span style="font-size: 12px;">不能用于私有方法。</span><br /><span style="font-size: 12px;">不能用于静态方法。</span><br /><span style="font-size: 12px;">不能用于非注入类的方法（我们必须使用依赖注入）。</span></p>
<p><span style="font-size: 12px;">此外</span></p>
<p><span style="font-size: 12px;">如果方法通过接口调用（如通过接口使用的应用程序服务），可以将其用于任何公共方法。</span><br /><span style="font-size: 12px;">如果直接从类引用（如ASP.NET MVC或Web API控制器）调用，则该方法应该是虚拟的。</span><br /><span style="font-size: 12px;">如果保护方法应该是虚拟的。</span></p>
<p>③使用IFeatureChecker<br />我们可以注入和使用IFeatureChecker手动检查功能（它自动注入并可直接用于应用程序服务，MVC和Web API控制器）。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task&lt;FileDto&gt;<span style="color: #000000;"> GetReportToExcel(...)
{
    </span><span style="color: #0000ff;">if</span> (<span style="color: #0000ff;">await</span> FeatureChecker.IsEnabledAsync(<span style="color: #800000;">"</span><span style="color: #800000;">ExportToExcel</span><span style="color: #800000;">"</span><span style="color: #000000;">))
    {
        </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> AbpAuthorizationException(<span style="color: #800000;">"</span><span style="color: #800000;">您没有此功能：ExportToExcel</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    }

    ...
}</span></pre>
</div>
<p>如果您只想检查一个功能并抛出异常，如示例所示，您只需使用CheckEnabled方法即可。</p>
<p>④获取功能的值</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> createdTaskCountInThisMonth =<span style="color: #000000;"> GetCreatedTaskCountInThisMonth();
</span><span style="color: #0000ff;">if</span> (createdTaskCountInThisMonth &gt;= FeatureChecker.GetValue(<span style="color: #800000;">"</span><span style="color: #800000;">MaxTaskCreationLimitPerMonth</span><span style="color: #800000;">"</span>).To&lt;<span style="color: #0000ff;">int</span>&gt;<span style="color: #000000;">())
{
    </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> AbpAuthorizationException(<span style="color: #800000;">"</span><span style="color: #800000;">你超过本月的任务创建限制</span><span style="color: #800000;">"</span><span style="color: #000000;">);
}</span></pre>
</div>
<p>FeatureChecker方法也覆盖了指定tenantId的工作功能，不仅适用于当前的tenantId。</p>
<p>⑤客户端<br />在客户端（javascript）中，我们可以使用abp.features命名空间来获取当前的功能值。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> isEnabled = abp.features.isEnabled(<span style="color: #800000;">'</span><span style="color: #800000;">SampleBooleanFeature</span><span style="color: #800000;">'</span><span style="color: #000000;">);
</span><span style="color: #0000ff;">var</span> value = abp.features.getValue(<span style="color: #800000;">'</span><span style="color: #800000;">SampleNumericFeature</span><span style="color: #800000;">'</span>);</pre>
</div>
<p>&nbsp;</p>
<p><span style="font-size: 18px;"><strong>3，深度研究</strong></span></p>
<p>一、AbpFeatures表分析<br />1，Name：<br />名称，必须先配置FeatureProvider，此名称一定在FeatureProvider配置中存在。唯一<br />2，Value：<br />①值。支持两种类型（bool类型和值类型）<br />②bool类型使用FeatureChecker.CheckEnabled("")获取，不存咋抛异常<br />③值类型使用FeatureChecker.GetValue("").To&lt;int&gt;()获取，不存咋抛异常<br />3，EditionId：<br />①版本关联，使用EditionFeatureSetting类型创建<br />②使用_abpEditionManager.SetFeatureValueAsync()设置基于版本的功能<br />4，TenantId：<br />①租户关联，使用TenantFeatureSetting类型创建<br />②使用TenantManager.SetFeatureValue()设置基于租户的功能<br />5，Discriminator：<br />①标识<br />②值为TenantFeatureSetting表示基于租户<br />③值为EditionFeatureSetting表示基于版本</p>
<p>二、案例分析</p>
<p>FeatureProvider配置</p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201711/741594-20171129141758315-1461902267.png" alt="" width="560" height="285" /></p>
<p>AbpFeatures表</p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201711/741594-20171129141205581-1852429658.png" alt="" width="635" height="88" /></p>
<p>权限配置</p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201711/741594-20171129141238550-129945882.png" alt="" width="825" height="285" /></p>
<p>1，租户1没有Product权限（当前Product权限为菜单权限），所以租户1在页面上不会显示出Product菜单权限</p>
<p>2，租户2&nbsp;<span class="cnblogs_code">FeatureChecker.GetValue(<span style="color: #800000;">"</span><span style="color: #800000;">Count</span><span style="color: #800000;">"</span>).To&lt;<span style="color: #0000ff;">int</span>&gt;()</span>&nbsp;值为20</p>
<p>3，租户3&nbsp;<span class="cnblogs_code">FeatureChecker.GetValue(<span style="color: #800000;">"</span><span style="color: #800000;">Count</span><span style="color: #800000;">"</span>).To&lt;<span style="color: #0000ff;">int</span>&gt;()</span>&nbsp;值为30</p>
<p>4，租户1&nbsp;<span class="cnblogs_code">FeatureChecker.GetValue(<span style="color: #800000;">"</span><span style="color: #800000;">Count</span><span style="color: #800000;">"</span>).To&lt;<span style="color: #0000ff;">int</span>&gt;()</span>&nbsp;值为10（默认配置的值）</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a23"></a>二十三、审计日志</span></strong></span></p>
<p>基本上保存的字段是：相关租户信息tenant id,、user id、服务名称（被调用方法的类）、方法名称、执行参数（序列化为json）、执行时间、执行持续时间（毫秒）、客户端ip地址、客户端计算机名称和异常（如果方法抛出异常）</p>
<p>1，配置</p>
<p>要配置审核，可以在模块的PreInitialize方法中使用Configuration.Auditing属性。 默认情况下启用审计。 您可以禁用它，如下所示。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyModule : AbpModule
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> PreInitialize()
    {
        Configuration.Auditing.IsEnabled </span>= <span style="color: #0000ff;">false</span><span style="color: #000000;">;
    }
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
}</pre>
</div>
<p>这里列出了审核配置属性：</p>
<ul>
<li><strong>IsEnabled</strong>:用于完全启用/禁用审计系统。 默认值：true。</li>
<li><strong>IsEnabledForAnonymousUsers</strong>:如果设置为true，则对于未登录系统的用户，还会保存审核日志。 默认值：false。</li>
<li><strong>Selectors</strong>:&nbsp;用于选择其他类来保存审核日志。</li>
</ul>
<p>选择器是选择其他类型以保存审核日志的谓词列表。 选择器具有唯一的名称和谓词。 此列表中唯一的默认选择器用于选择应用程序服务类。 定义如下：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">Configuration.Auditing.Selectors.Add(
    </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> NamedTypeSelector(
        </span><span style="color: #800000;">"</span><span style="color: #800000;">Abp.ApplicationServices</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        type </span>=&gt; <span style="color: #0000ff;">typeof</span><span style="color: #000000;"> (IApplicationService).IsAssignableFrom(type)
    )
);</span></pre>
</div>
<p>您可以在您的模块的PreInitialize方法中添加选择器。 另外，如果不想保存应用程序服务的审核日志，可以通过名称删除上面的选择器。 这就是为什么它有一个唯一的名称（使用简单的LINQ在选择器中找到选择器，如果需要的话）。</p>
<p>注意：除了标准审核配置外，MVC和ASP.NET Core模块还定义了启用/禁用审计日志记录的配置。</p>
<p>2，按属性启用/禁用</p>
<p>虽然您可以通过配置选择审核类，但可以对单个类使用&ldquo;已审核&rdquo;和&ldquo;禁用属性&rdquo;，也就是单一方法。 一个例子：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">[Audited]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyClass
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> MyMethod1(<span style="color: #0000ff;">int</span><span style="color: #000000;"> a)
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">    }

    [DisableAuditing]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> MyMethod2(<span style="color: #0000ff;">string</span><span style="color: #000000;"> b)
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> MyMethod3(<span style="color: #0000ff;">int</span> a, <span style="color: #0000ff;">int</span><span style="color: #000000;"> b)
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">    }
}</span></pre>
</div>
<p>除了MyMethod2，MyClass的所有方法都被审计，因为它被明确禁用。 经审计的属性可用于仅为所需方法保存审核的方法。</p>
<p>DisableAuditing也可以用于DTO的一个或一个属性。 因此，您可以隐藏审计日志中的敏感数据，例如密码。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a24"></a>二十四、ASP.NET Web API Controllers</span></strong></span></p>
<p>1，AbpApiController基类&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> UsersController : AbpApiController
{

}</span></pre>
</div>
<p>2，本地化</p>
<p>AbpApiController定义了L方法，使本地化更容易。 例：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> UsersController : AbpApiController
{
    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> UsersController()
    {
        LocalizationSourceName </span>= <span style="color: #800000;">"</span><span style="color: #800000;">MySourceName</span><span style="color: #800000;">"</span><span style="color: #000000;">;
    }

    </span><span style="color: #0000ff;">public</span> UserDto Get(<span style="color: #0000ff;">long</span><span style="color: #000000;"> id)
    {
        </span><span style="color: #0000ff;">var</span> helloWorldText = L(<span style="color: #800000;">"</span><span style="color: #800000;">HelloWorld</span><span style="color: #800000;">"</span><span style="color: #000000;">);

        </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">    }
}</span></pre>
</div>
<p>您应该设置LocalizationSourceName使L方法工作。 您可以将其设置在您自己的基本api控制器类中，以便不对每个api控制器重复。</p>
<p>3，其他<br />您还可以使用预先注入的AbpSession，EventBus，PermissionManager，PermissionChecker，SettingManager，FeatureManager，FeatureChecker，LocalizationManager，Logger，CurrentUnitOfWork基础属性等。</p>
<p>4，过滤器</p>
<p>①审计日志<br />AbpApiAuditFilter用于集成审计日志系统。 它默认将所有请求记录到所有操作（如果未禁用审核）。 您可以使用Audited和DisableAuditing属性控制审计日志记录，以执行操作和控制器。</p>
<p>②授权<br />您可以为您的api控制器或操作使用AbpApiAuthorize属性，以防止未经授权的用户使用您的控制器和操作。 例：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> UsersController : AbpApiController
{
    [AbpApiAuthorize(</span><span style="color: #800000;">"</span><span style="color: #800000;">MyPermissionName</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
    </span><span style="color: #0000ff;">public</span> UserDto Get(<span style="color: #0000ff;">long</span><span style="color: #000000;"> id)
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">    }
}</span></pre>
</div>
<p>您可以为操作或控制器定义AllowAnonymous属性以抑制身份验证/授权。 AbpApiController还将IsGranted方法定义为在代码中检查权限的快捷方式。</p>
<p>③防伪过滤器<br />AbpAntiForgeryApiFilter用于自动保护来自CSRF / XSRF攻击的POST，PUT和DELETE请求的ASP.NET Web API操作（包括动态Web api）</p>
<p>④工作单位<br />AbpApiUowFilter用于集成到工作单元系统。 在动作执行之前，它会自动开始一个新的工作单元，并在动作执行之后完成工作单元（如果没有异常被抛出）。</p>
<p>您可以使用UnitOfWork属性来控制操作的UOW的行为。 您还可以使用启动配置来更改所有操作的默认工作属性。</p>
<p>⑤结果缓存<br />ASP.NET Boilerplate为Web API请求的响应添加了Cache-Control头（无缓存，无存储）。 因此，它甚至阻止浏览器缓存GET请求。 可以通过配置禁用此行为。</p>
<p>⑥验证<br />AbpApiValidationFilter会自动检查ModelState.IsValid，如果该操作无效，可以防止执行该操作。 此外，实现验证文档中描述的输入DTO验证。</p>
<p>⑦模型绑定<br />AbpApiDateTimeBinder用于使用Clock.Normalize方法对DateTime（和Nullable &lt;DateTime&gt;）进行归一化。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a25"></a>二十五、动态Webapi层</span></strong></span></p>
<p>1，ForAll Method</p>
<p>DynamicApiControllerBuilper提供了一种在一个调用中为所有应用程序服务构建Web api控制器的方法</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">Configuration.Modules.AbpWebApi().DynamicApiControllerBuilder
    .ForAll</span>&lt;IApplicationService&gt;(Assembly.GetAssembly(<span style="color: #0000ff;">typeof</span>(SimpleTaskSystemApplicationModule)), <span style="color: #800000;">"</span><span style="color: #800000;">tasksystem</span><span style="color: #800000;">"</span><span style="color: #000000;">)
    .Build();</span></pre>
</div>
<p>&nbsp;对于此配置，服务将是&ldquo;/api/services/tasksystem/task&rdquo;和&ldquo;/api/services/tasksystem/person&rdquo;。 要计算服务名称：Service和AppService后缀和I前缀被删除（用于接口）</p>
<p>2，覆盖ForAll&nbsp;</p>
<p>我们可以在ForAll方法之后覆盖配置。 例：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">Configuration.Modules.AbpWebApi().DynamicApiControllerBuilder
    .ForAll</span>&lt;IApplicationService&gt;(Assembly.GetAssembly(<span style="color: #0000ff;">typeof</span>(SimpleTaskSystemApplicationModule)), <span style="color: #800000;">"</span><span style="color: #800000;">tasksystem</span><span style="color: #800000;">"</span><span style="color: #000000;">)
    .Build();

Configuration.Modules.AbpWebApi().DynamicApiControllerBuilder
    .For</span>&lt;ITaskAppService&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">tasksystem/task</span><span style="color: #800000;">"</span><span style="color: #000000;">)
    .ForMethod(</span><span style="color: #800000;">"</span><span style="color: #800000;">CreateTask</span><span style="color: #800000;">"</span>).DontCreateAction().Build();</pre>
</div>
<p>在此代码中，我们为程序集中的所有应用程序服务创建了动态Web API控制器。 然后覆盖单个应用程序服务（ITaskAppService）的配置来忽略CreateTask方法。</p>
<p>3，ForMethods</p>
<p>使用ForAll方法时，可以使用ForMethods方法来更好地调整每种方法。 例：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">Configuration.Modules.AbpWebApi().DynamicApiControllerBuilder
    .ForAll</span>&lt;IApplicationService&gt;(Assembly.GetExecutingAssembly(), <span style="color: #800000;">"</span><span style="color: #800000;">app</span><span style="color: #800000;">"</span><span style="color: #000000;">)
    .ForMethods(builder </span>=&gt;<span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">if</span> (builder.Method.IsDefined(<span style="color: #0000ff;">typeof</span><span style="color: #000000;">(MyIgnoreApiAttribute)))
        {
            builder.DontCreate </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">;
        }
    })
    .Build();</span></pre>
</div>
<p>在此示例中，我使用自定义属性（MyIgnoreApiAttribute）来检查所有方法，并且不为使用该属性标记的方法创建动态Web api控制器操作。</p>
<p>4，Http动词</p>
<p>默认情况下，所有方法都创建为POST</p>
<p>5，WithVerb Method</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">Configuration.Modules.AbpWebApi().DynamicApiControllerBuilder
    .For</span>&lt;ITaskAppService&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">tasksystem/task</span><span style="color: #800000;">"</span><span style="color: #000000;">)
    .ForMethod(</span><span style="color: #800000;">"</span><span style="color: #800000;">GetTasks</span><span style="color: #800000;">"</span><span style="color: #000000;">).WithVerb(HttpVerb.Get)
    .Build();</span></pre>
</div>
<p>6，Http特性</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> ITaskAppService : IApplicationService
{
    [HttpGet]
    GetTasksOutput GetTasks(GetTasksInput input);

    [HttpPut]
    </span><span style="color: #0000ff;">void</span><span style="color: #000000;"> UpdateTask(UpdateTaskInput input);

    [HttpPost]
    </span><span style="color: #0000ff;">void</span><span style="color: #000000;"> CreateTask(CreateTaskInput input);
}</span></pre>
</div>
<p>7，WithConventionalVerbs 命名公约</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">Configuration.Modules.AbpWebApi().DynamicApiControllerBuilder
    .ForAll</span>&lt;IApplicationService&gt;(Assembly.GetAssembly(<span style="color: #0000ff;">typeof</span>(SimpleTaskSystemApplicationModule)), <span style="color: #800000;">"</span><span style="color: #800000;">tasksystem</span><span style="color: #800000;">"</span><span style="color: #000000;">)
    .WithConventionalVerbs()
    .Build();</span></pre>
</div>
<ul>
<li><strong>Get</strong>:&nbsp;如果方法名以&ldquo;Get&rdquo;开头，则使用</li>
<li><strong>Put</strong>:如果方法名称以&ldquo;Put&rdquo;或&ldquo;Update&rdquo;开头，则使用</li>
<li><strong>Delete</strong>: 如果方法名称以&ldquo;Delete&rdquo;或&ldquo;Remove&rdquo;开头</li>
<li><strong>Post</strong>:&nbsp;如果方法名称以&ldquo;Post&rdquo;，&ldquo;Create&rdquo;或&ldquo;Insert&rdquo;开头，则使用</li>
<li><strong>Patch</strong>:&nbsp;如果方法名称以&ldquo;Patch&rdquo;开头，则使用</li>
<li>否则,Post被用作默认的HTTP动词</li>
</ul>
<p>8，远程服务属性<br />您还可以使用RemoteService属性进行任何接口或方法定义来启用/禁用（IsEnabled）动态API或API资源管理器设置（IsMetadataEnabled）。</p>
<p>9，动态Javascript代理</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">abp.services.tasksystem.task.getTasks({
    state: </span>1<span style="color: #000000;">
}).done(</span><span style="color: #0000ff;">function</span><span style="color: #000000;"> (result) {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">use result.tasks here...</span>
});</pre>
</div>
<p>Javascript代理是动态创建的。 在使用之前，您应该将动态脚本添加到页面中：</p>
<div class="cnblogs_code">
<pre>&lt;script src="/api/AbpServiceProxies/GetAll" type="text/javascript"&gt;&lt;/script&gt;</pre>
</div>
<p>10，AJAX参数<br />您可能希望将自定义ajax参数传递给代理方法。 你可以将它们作为第二个参数传递下面所示：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">abp.services.tasksystem.task.createTask({
    assignedPersonId: </span>3<span style="color: #000000;">,
    description: </span>'a new task description...'<span style="color: #000000;">
},{ </span><span style="color: #008000;">//</span><span style="color: #008000;">覆盖jQuery的ajax参数</span>
    async: <span style="color: #0000ff;">false</span><span style="color: #000000;">,
    timeout: </span>30000<span style="color: #000000;">
}).done(</span><span style="color: #0000ff;">function</span><span style="color: #000000;"> () {
    abp.notify.success(</span>'successfully created a task!'<span style="color: #000000;">);
});</span></pre>
</div>
<p>jQuery.ajax的所有参数在这里是有效的。</p>
<p>除了标准的jQuery.ajax参数之外，您可以向AJAX选项添加abpHandleError：false，以便在错误情况下禁用自动消息显示。</p>
<p>11，单一服务脚本<br />'/api/AbpServiceProxies/GetAll'在一个文件中生成所有服务代理。 您还可以使用'/api/AbpServiceProxies/Get?name=serviceName'生成单个服务代理，并将脚本包含在页面中，如下所示：</p>
<div class="cnblogs_code">
<pre>&lt;script src="/api/AbpServiceProxies/Get?name=tasksystem/task" type="text/javascript"&gt;&lt;/script&gt;</pre>
</div>
<p>12，Angular整合</p>
<div class="cnblogs_code">
<pre>(<span style="color: #0000ff;">function</span><span style="color: #000000;">() {
    angular.module(</span>'app').controller('TaskListController'<span style="color: #000000;">, [
        </span>'$scope', 'abp.services.tasksystem.task'<span style="color: #000000;">,
        </span><span style="color: #0000ff;">function</span><span style="color: #000000;">($scope, taskService) {
            </span><span style="color: #0000ff;">var</span> vm = <span style="color: #0000ff;">this</span><span style="color: #000000;">;
            vm.tasks </span>=<span style="color: #000000;"> [];
            taskService.getTasks({
                state: </span>0<span style="color: #000000;">
            }).success(</span><span style="color: #0000ff;">function</span><span style="color: #000000;">(result) {
                vm.tasks </span>=<span style="color: #000000;"> result.tasks;
            });
        }
    ]);
})();</span></pre>
</div>
<p>为了能够使用自动生成的服务，您应该在页面中包含所需的脚本：</p>
<div class="cnblogs_code">
<pre>&lt;script src="~/Abp/Framework/scripts/libs/angularjs/abp.ng.js"&gt;&lt;/script&gt;
&lt;script src="~/api/AbpServiceProxies/GetAll?type=angular"&gt;&lt;/script&gt;</pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a26"></a>二十六、OData整合</span></strong></span></p>
<p>OData被定义为&ldquo;odata.org中允许以简单和标准的方式创建和消费可查询和可互操作的RESTful API的开放式协议&rdquo;</p>
<p>1，安装包</p>
<div class="cnblogs_code">
<pre>Install-Package Abp.Web.Api.OData</pre>
</div>
<p>2，设置模块依赖</p>
<p>配置您的实体<br />OData需要声明可用作OData资源的实体。 我们应该在我们模块的PreInitialize方法中执行此操作，如下所示：</p>
<div class="cnblogs_code">
<pre>[DependsOn(<span style="color: #0000ff;">typeof</span><span style="color: #000000;">(AbpWebApiODataModule))]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyProjectWebApiModule : AbpModule
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> PreInitialize()
    {
        </span><span style="color: #0000ff;">var</span> builder =<span style="color: #000000;"> Configuration.Modules.AbpWebApiOData().ODataModelBuilder;

        </span><span style="color: #008000;">//</span><span style="color: #008000;">在这里配置您的实体</span>
        builder.EntitySet&lt;Person&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">Persons</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    }

    ...
}</span></pre>
</div>
<p>在这里，我们得到了ODataModelBuilder引用，并设置了Person实体。 您可以使用EntitySet添加类似的其他实体</p>
<p>3，创建控制器<br />Abp.Web.Api.OData nuget软件包包括AbpODataEntityController基类（扩展标准ODataController），以便更轻松地创建控制器。 为Person实体创建OData端点的示例：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> PersonsController : AbpODataEntityController&lt;Person&gt;<span style="color: #000000;">
{
    </span><span style="color: #0000ff;">public</span> PersonsController(IRepository&lt;Person&gt;<span style="color: #000000;"> repository)
        : </span><span style="color: #0000ff;">base</span><span style="color: #000000;">(repository)
    {
    }
}</span></pre>
</div>
<p>这很容易 AbpODataEntityController的所有方法都是虚拟的。 这意味着您可以覆盖Get，Post，Put，Patch，Delete和其他操作，并添加您自己的逻辑。</p>
<p>4，配置</p>
<p>Abp.Web.Api.OData自动调用HttpConfiguration.MapODataServiceRoute方法与常规配置。 如果需要，您可以设置Configuration.Modules.AbpWebApiOData（）。MapAction自己映射OData路由。</p>
<p>5，例子</p>
<p>在这里，一些例子请求到上面定义的控制器。 假设应用程序在http://localhost:61842上工作。 我们将展示一些基础知识。 由于OData是标准协议，您可以轻松地在网络上找到更多高级示例。</p>
<p>①获取所有列表</p>
<p>请求：GET http:<span class="hljs-comment">//localhost:61842/odata/Persons</span></p>
<p>响应：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">@odata.context</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:61842/odata/$metadata#Persons</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">value</span><span style="color: #800000;">"</span><span style="color: #000000;">:[
    {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">Name</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">Douglas Adams</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">IsDeleted</span><span style="color: #800000;">"</span>:<span style="color: #0000ff;">false</span>,<span style="color: #800000;">"</span><span style="color: #800000;">DeleterUserId</span><span style="color: #800000;">"</span>:<span style="color: #0000ff;">null</span>,<span style="color: #800000;">"</span><span style="color: #800000;">DeletionTime</span><span style="color: #800000;">"</span>:<span style="color: #0000ff;">null</span>,<span style="color: #800000;">"</span><span style="color: #800000;">LastModificationTime</span><span style="color: #800000;">"</span>:<span style="color: #0000ff;">null</span>,<span style="color: #800000;">"</span><span style="color: #800000;">LastModifierUserId</span><span style="color: #800000;">"</span>:<span style="color: #0000ff;">null</span>,<span style="color: #800000;">"</span><span style="color: #800000;">CreationTime</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">2015-11-07T20:12:39.363+03:00</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">CreatorUserId</span><span style="color: #800000;">"</span>:<span style="color: #0000ff;">null</span>,<span style="color: #800000;">"</span><span style="color: #800000;">Id</span><span style="color: #800000;">"</span>:<span style="color: #800080;">1</span><span style="color: #000000;">
    },{
      </span><span style="color: #800000;">"</span><span style="color: #800000;">Name</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">John Nash</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">IsDeleted</span><span style="color: #800000;">"</span>:<span style="color: #0000ff;">false</span>,<span style="color: #800000;">"</span><span style="color: #800000;">DeleterUserId</span><span style="color: #800000;">"</span>:<span style="color: #0000ff;">null</span>,<span style="color: #800000;">"</span><span style="color: #800000;">DeletionTime</span><span style="color: #800000;">"</span>:<span style="color: #0000ff;">null</span>,<span style="color: #800000;">"</span><span style="color: #800000;">LastModificationTime</span><span style="color: #800000;">"</span>:<span style="color: #0000ff;">null</span>,<span style="color: #800000;">"</span><span style="color: #800000;">LastModifierUserId</span><span style="color: #800000;">"</span>:<span style="color: #0000ff;">null</span>,<span style="color: #800000;">"</span><span style="color: #800000;">CreationTime</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">2015-11-07T20:12:39.363+03:00</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">CreatorUserId</span><span style="color: #800000;">"</span>:<span style="color: #0000ff;">null</span>,<span style="color: #800000;">"</span><span style="color: #800000;">Id</span><span style="color: #800000;">"</span>:<span style="color: #800080;">2</span><span style="color: #000000;">
    }
  ]
}</span></pre>
</div>
<p>②获取单个实体（where id=2）</p>
<p>请求：GET http:<span class="hljs-comment">//localhost:61842/odata/Persons(2)</span></p>
<p>&nbsp;响应：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">@odata.context</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:61842/odata/$metadata#Persons/$entity</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">Name</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">John Nash</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">IsDeleted</span><span style="color: #800000;">"</span>:<span style="color: #0000ff;">false</span>,<span style="color: #800000;">"</span><span style="color: #800000;">DeleterUserId</span><span style="color: #800000;">"</span>:<span style="color: #0000ff;">null</span>,<span style="color: #800000;">"</span><span style="color: #800000;">DeletionTime</span><span style="color: #800000;">"</span>:<span style="color: #0000ff;">null</span>,<span style="color: #800000;">"</span><span style="color: #800000;">LastModificationTime</span><span style="color: #800000;">"</span>:<span style="color: #0000ff;">null</span>,<span style="color: #800000;">"</span><span style="color: #800000;">LastModifierUserId</span><span style="color: #800000;">"</span>:<span style="color: #0000ff;">null</span>,<span style="color: #800000;">"</span><span style="color: #800000;">CreationTime</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">2015-11-07T20:12:39.363+03:00</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">CreatorUserId</span><span style="color: #800000;">"</span>:<span style="color: #0000ff;">null</span>,<span style="color: #800000;">"</span><span style="color: #800000;">Id</span><span style="color: #800000;">"</span>:<span style="color: #800080;">2</span><span style="color: #000000;">
}</span></pre>
</div>
<p>③获取具有导航属性的单个实体（获得Id = 1的人，包括他的电话号码）</p>
<p>请求：GET http:<span class="hljs-comment">//localhost:61842/odata/Persons(1)?$expand=Phones</span></p>
<p><span class="hljs-comment">响应：</span></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">@odata.context</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:61842/odata/$metadata#Persons/$entity</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">Name</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">Douglas Adams</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">IsDeleted</span><span style="color: #800000;">"</span>:<span style="color: #0000ff;">false</span>,<span style="color: #800000;">"</span><span style="color: #800000;">DeleterUserId</span><span style="color: #800000;">"</span>:<span style="color: #0000ff;">null</span>,<span style="color: #800000;">"</span><span style="color: #800000;">DeletionTime</span><span style="color: #800000;">"</span>:<span style="color: #0000ff;">null</span>,<span style="color: #800000;">"</span><span style="color: #800000;">LastModificationTime</span><span style="color: #800000;">"</span>:<span style="color: #0000ff;">null</span>,<span style="color: #800000;">"</span><span style="color: #800000;">LastModifierUserId</span><span style="color: #800000;">"</span>:<span style="color: #0000ff;">null</span>,<span style="color: #800000;">"</span><span style="color: #800000;">CreationTime</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">2015-11-07T20:12:39.363+03:00</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">CreatorUserId</span><span style="color: #800000;">"</span>:<span style="color: #0000ff;">null</span>,<span style="color: #800000;">"</span><span style="color: #800000;">Id</span><span style="color: #800000;">"</span>:<span style="color: #800080;">1</span>,<span style="color: #800000;">"</span><span style="color: #800000;">Phones</span><span style="color: #800000;">"</span><span style="color: #000000;">:[
    {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">PersonId</span><span style="color: #800000;">"</span>:<span style="color: #800080;">1</span>,<span style="color: #800000;">"</span><span style="color: #800000;">Type</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">Mobile</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">Number</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">4242424242</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">CreationTime</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">2015-11-07T20:12:39.363+03:00</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">CreatorUserId</span><span style="color: #800000;">"</span>:<span style="color: #0000ff;">null</span>,<span style="color: #800000;">"</span><span style="color: #800000;">Id</span><span style="color: #800000;">"</span>:<span style="color: #800080;">1</span><span style="color: #000000;">
    },{
      </span><span style="color: #800000;">"</span><span style="color: #800000;">PersonId</span><span style="color: #800000;">"</span>:<span style="color: #800080;">1</span>,<span style="color: #800000;">"</span><span style="color: #800000;">Type</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">Mobile</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">Number</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">2424242424</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">CreationTime</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">2015-11-07T20:12:39.363+03:00</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">CreatorUserId</span><span style="color: #800000;">"</span>:<span style="color: #0000ff;">null</span>,<span style="color: #800000;">"</span><span style="color: #800000;">Id</span><span style="color: #800000;">"</span>:<span style="color: #800080;">2</span><span style="color: #000000;">
    }
  ]
}</span></pre>
</div>
<p>④更高级的查询包括过滤，排序和获取前2个结果</p>
<p><span class="hljs-comment">请求：</span>GET http:<span class="hljs-comment">//localhost:61842/odata/Persons?$filter=Name eq 'Douglas Adams'&amp;$orderby=CreationTime&amp;$top=2</span></p>
<p><span class="hljs-comment">响应：</span></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">@odata.context</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:61842/odata/$metadata#Persons</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">value</span><span style="color: #800000;">"</span><span style="color: #000000;">:[
    {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">Name</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">Douglas Adams</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">IsDeleted</span><span style="color: #800000;">"</span>:<span style="color: #0000ff;">false</span>,<span style="color: #800000;">"</span><span style="color: #800000;">DeleterUserId</span><span style="color: #800000;">"</span>:<span style="color: #0000ff;">null</span>,<span style="color: #800000;">"</span><span style="color: #800000;">DeletionTime</span><span style="color: #800000;">"</span>:<span style="color: #0000ff;">null</span>,<span style="color: #800000;">"</span><span style="color: #800000;">LastModificationTime</span><span style="color: #800000;">"</span>:<span style="color: #0000ff;">null</span>,<span style="color: #800000;">"</span><span style="color: #800000;">LastModifierUserId</span><span style="color: #800000;">"</span>:<span style="color: #0000ff;">null</span>,<span style="color: #800000;">"</span><span style="color: #800000;">CreationTime</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">2015-11-07T20:12:39.363+03:00</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">CreatorUserId</span><span style="color: #800000;">"</span>:<span style="color: #0000ff;">null</span>,<span style="color: #800000;">"</span><span style="color: #800000;">Id</span><span style="color: #800000;">"</span>:<span style="color: #800080;">1</span><span style="color: #000000;">
    },{
      </span><span style="color: #800000;">"</span><span style="color: #800000;">Name</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">Douglas Adams</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">IsDeleted</span><span style="color: #800000;">"</span>:<span style="color: #0000ff;">false</span>,<span style="color: #800000;">"</span><span style="color: #800000;">DeleterUserId</span><span style="color: #800000;">"</span>:<span style="color: #0000ff;">null</span>,<span style="color: #800000;">"</span><span style="color: #800000;">DeletionTime</span><span style="color: #800000;">"</span>:<span style="color: #0000ff;">null</span>,<span style="color: #800000;">"</span><span style="color: #800000;">LastModificationTime</span><span style="color: #800000;">"</span>:<span style="color: #0000ff;">null</span>,<span style="color: #800000;">"</span><span style="color: #800000;">LastModifierUserId</span><span style="color: #800000;">"</span>:<span style="color: #0000ff;">null</span>,<span style="color: #800000;">"</span><span style="color: #800000;">CreationTime</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">2016-01-12T20:29:03+02:00</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">CreatorUserId</span><span style="color: #800000;">"</span>:<span style="color: #0000ff;">null</span>,<span style="color: #800000;">"</span><span style="color: #800000;">Id</span><span style="color: #800000;">"</span>:<span style="color: #800080;">3</span><span style="color: #000000;">
    }
  ]
}</span></pre>
</div>
<p>⑤创建新实体</p>
<p>请求（这里，&ldquo;Content-Type&rdquo;头是&ldquo;application / json&rdquo;）：</p>
<div class="cnblogs_code">
<pre>POST http:<span style="color: #008000;">//</span><span style="color: #008000;">localhost:61842/odata/Persons</span>
<span style="color: #000000;">
{
    Name: </span><span style="color: #800000;">"</span><span style="color: #800000;">Galileo Galilei</span><span style="color: #800000;">"</span><span style="color: #000000;">
}</span></pre>
</div>
<p>响应：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">@odata.context</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:61842/odata/$metadata#Persons/$entity</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">Name</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">Galileo Galilei</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">IsDeleted</span><span style="color: #800000;">"</span>: <span style="color: #0000ff;">false</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">DeleterUserId</span><span style="color: #800000;">"</span>: <span style="color: #0000ff;">null</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">DeletionTime</span><span style="color: #800000;">"</span>: <span style="color: #0000ff;">null</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">LastModificationTime</span><span style="color: #800000;">"</span>: <span style="color: #0000ff;">null</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">LastModifierUserId</span><span style="color: #800000;">"</span>: <span style="color: #0000ff;">null</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">CreationTime</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">2016-01-12T20:36:04.1628263+02:00</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">CreatorUserId</span><span style="color: #800000;">"</span>: <span style="color: #0000ff;">null</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">Id</span><span style="color: #800000;">"</span>: <span style="color: #800080;">4</span><span style="color: #000000;">
}</span></pre>
</div>
<p>⑥获取元数据（元数据用于调查服务）</p>
<p>请求：GET http:<span class="hljs-comment">//localhost:61842/odata/$metadata</span></p>
<p><span class="hljs-comment">响应：</span></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('24bb9113-b89e-4b2c-bd29-a4d00a3bd699')"><img id="code_img_closed_24bb9113-b89e-4b2c-bd29-a4d00a3bd699" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_24bb9113-b89e-4b2c-bd29-a4d00a3bd699" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('24bb9113-b89e-4b2c-bd29-a4d00a3bd699',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_24bb9113-b89e-4b2c-bd29-a4d00a3bd699" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">&lt;?</span><span style="color: #ff00ff;">xml version="1.0" encoding="utf-8"</span><span style="color: #0000ff;">?&gt;</span>

<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">edmx:Edmx </span><span style="color: #ff0000;">Version</span><span style="color: #0000ff;">="4.0"</span><span style="color: #ff0000;"> xmlns:edmx</span><span style="color: #0000ff;">="http://docs.oasis-open.org/odata/ns/edmx"</span><span style="color: #0000ff;">&gt;</span>

    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">edmx:DataServices</span><span style="color: #0000ff;">&gt;</span>

        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Schema </span><span style="color: #ff0000;">Namespace</span><span style="color: #0000ff;">="AbpODataDemo.People"</span><span style="color: #ff0000;"> xmlns</span><span style="color: #0000ff;">="http://docs.oasis-open.org/odata/ns/edm"</span><span style="color: #0000ff;">&gt;</span>

            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">EntityType </span><span style="color: #ff0000;">Name</span><span style="color: #0000ff;">="Person"</span><span style="color: #0000ff;">&gt;</span>

                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Key</span><span style="color: #0000ff;">&gt;</span>

                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">PropertyRef </span><span style="color: #ff0000;">Name</span><span style="color: #0000ff;">="Id"</span> <span style="color: #0000ff;">/&gt;</span>

                <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Key</span><span style="color: #0000ff;">&gt;</span>

                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Property </span><span style="color: #ff0000;">Name</span><span style="color: #0000ff;">="Name"</span><span style="color: #ff0000;"> Type</span><span style="color: #0000ff;">="Edm.String"</span><span style="color: #ff0000;"> Nullable</span><span style="color: #0000ff;">="false"</span> <span style="color: #0000ff;">/&gt;</span>

                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Property </span><span style="color: #ff0000;">Name</span><span style="color: #0000ff;">="IsDeleted"</span><span style="color: #ff0000;"> Type</span><span style="color: #0000ff;">="Edm.Boolean"</span><span style="color: #ff0000;"> Nullable</span><span style="color: #0000ff;">="false"</span> <span style="color: #0000ff;">/&gt;</span>

                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Property </span><span style="color: #ff0000;">Name</span><span style="color: #0000ff;">="DeleterUserId"</span><span style="color: #ff0000;"> Type</span><span style="color: #0000ff;">="Edm.Int64"</span> <span style="color: #0000ff;">/&gt;</span>

                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Property </span><span style="color: #ff0000;">Name</span><span style="color: #0000ff;">="DeletionTime"</span><span style="color: #ff0000;"> Type</span><span style="color: #0000ff;">="Edm.DateTimeOffset"</span> <span style="color: #0000ff;">/&gt;</span>

                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Property </span><span style="color: #ff0000;">Name</span><span style="color: #0000ff;">="LastModificationTime"</span><span style="color: #ff0000;"> Type</span><span style="color: #0000ff;">="Edm.DateTimeOffset"</span> <span style="color: #0000ff;">/&gt;</span>

                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Property </span><span style="color: #ff0000;">Name</span><span style="color: #0000ff;">="LastModifierUserId"</span><span style="color: #ff0000;"> Type</span><span style="color: #0000ff;">="Edm.Int64"</span> <span style="color: #0000ff;">/&gt;</span>

                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Property </span><span style="color: #ff0000;">Name</span><span style="color: #0000ff;">="CreationTime"</span><span style="color: #ff0000;"> Type</span><span style="color: #0000ff;">="Edm.DateTimeOffset"</span><span style="color: #ff0000;"> Nullable</span><span style="color: #0000ff;">="false"</span> <span style="color: #0000ff;">/&gt;</span>

                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Property </span><span style="color: #ff0000;">Name</span><span style="color: #0000ff;">="CreatorUserId"</span><span style="color: #ff0000;"> Type</span><span style="color: #0000ff;">="Edm.Int64"</span> <span style="color: #0000ff;">/&gt;</span>

                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Property </span><span style="color: #ff0000;">Name</span><span style="color: #0000ff;">="Id"</span><span style="color: #ff0000;"> Type</span><span style="color: #0000ff;">="Edm.Int32"</span><span style="color: #ff0000;"> Nullable</span><span style="color: #0000ff;">="false"</span> <span style="color: #0000ff;">/&gt;</span>

                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">NavigationProperty </span><span style="color: #ff0000;">Name</span><span style="color: #0000ff;">="Phones"</span><span style="color: #ff0000;"> Type</span><span style="color: #0000ff;">="Collection(AbpODataDemo.People.Phone)"</span> <span style="color: #0000ff;">/&gt;</span>

            <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">EntityType</span><span style="color: #0000ff;">&gt;</span>

            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">EntityType </span><span style="color: #ff0000;">Name</span><span style="color: #0000ff;">="Phone"</span><span style="color: #0000ff;">&gt;</span>

                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Key</span><span style="color: #0000ff;">&gt;</span>

                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">PropertyRef </span><span style="color: #ff0000;">Name</span><span style="color: #0000ff;">="Id"</span> <span style="color: #0000ff;">/&gt;</span>

                <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Key</span><span style="color: #0000ff;">&gt;</span>

                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Property </span><span style="color: #ff0000;">Name</span><span style="color: #0000ff;">="PersonId"</span><span style="color: #ff0000;"> Type</span><span style="color: #0000ff;">="Edm.Int32"</span> <span style="color: #0000ff;">/&gt;</span>

                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Property </span><span style="color: #ff0000;">Name</span><span style="color: #0000ff;">="Type"</span><span style="color: #ff0000;"> Type</span><span style="color: #0000ff;">="AbpODataDemo.People.PhoneType"</span><span style="color: #ff0000;"> Nullable</span><span style="color: #0000ff;">="false"</span> <span style="color: #0000ff;">/&gt;</span>

                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Property </span><span style="color: #ff0000;">Name</span><span style="color: #0000ff;">="Number"</span><span style="color: #ff0000;"> Type</span><span style="color: #0000ff;">="Edm.String"</span><span style="color: #ff0000;"> Nullable</span><span style="color: #0000ff;">="false"</span> <span style="color: #0000ff;">/&gt;</span>

                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Property </span><span style="color: #ff0000;">Name</span><span style="color: #0000ff;">="CreationTime"</span><span style="color: #ff0000;"> Type</span><span style="color: #0000ff;">="Edm.DateTimeOffset"</span><span style="color: #ff0000;"> Nullable</span><span style="color: #0000ff;">="false"</span> <span style="color: #0000ff;">/&gt;</span>

                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Property </span><span style="color: #ff0000;">Name</span><span style="color: #0000ff;">="CreatorUserId"</span><span style="color: #ff0000;"> Type</span><span style="color: #0000ff;">="Edm.Int64"</span> <span style="color: #0000ff;">/&gt;</span>

                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Property </span><span style="color: #ff0000;">Name</span><span style="color: #0000ff;">="Id"</span><span style="color: #ff0000;"> Type</span><span style="color: #0000ff;">="Edm.Int32"</span><span style="color: #ff0000;"> Nullable</span><span style="color: #0000ff;">="false"</span> <span style="color: #0000ff;">/&gt;</span>

                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">NavigationProperty </span><span style="color: #ff0000;">Name</span><span style="color: #0000ff;">="Person"</span><span style="color: #ff0000;"> Type</span><span style="color: #0000ff;">="AbpODataDemo.People.Person"</span><span style="color: #0000ff;">&gt;</span>

                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ReferentialConstraint </span><span style="color: #ff0000;">Property</span><span style="color: #0000ff;">="PersonId"</span><span style="color: #ff0000;"> ReferencedProperty</span><span style="color: #0000ff;">="Id"</span> <span style="color: #0000ff;">/&gt;</span>

                <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">NavigationProperty</span><span style="color: #0000ff;">&gt;</span>

            <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">EntityType</span><span style="color: #0000ff;">&gt;</span>

            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">EnumType </span><span style="color: #ff0000;">Name</span><span style="color: #0000ff;">="PhoneType"</span><span style="color: #0000ff;">&gt;</span>

                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Member </span><span style="color: #ff0000;">Name</span><span style="color: #0000ff;">="Unknown"</span><span style="color: #ff0000;"> Value</span><span style="color: #0000ff;">="0"</span> <span style="color: #0000ff;">/&gt;</span>

                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Member </span><span style="color: #ff0000;">Name</span><span style="color: #0000ff;">="Mobile"</span><span style="color: #ff0000;"> Value</span><span style="color: #0000ff;">="1"</span> <span style="color: #0000ff;">/&gt;</span>

                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Member </span><span style="color: #ff0000;">Name</span><span style="color: #0000ff;">="Home"</span><span style="color: #ff0000;"> Value</span><span style="color: #0000ff;">="2"</span> <span style="color: #0000ff;">/&gt;</span>

                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Member </span><span style="color: #ff0000;">Name</span><span style="color: #0000ff;">="Office"</span><span style="color: #ff0000;"> Value</span><span style="color: #0000ff;">="3"</span> <span style="color: #0000ff;">/&gt;</span>

            <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">EnumType</span><span style="color: #0000ff;">&gt;</span>

        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Schema</span><span style="color: #0000ff;">&gt;</span>

        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Schema </span><span style="color: #ff0000;">Namespace</span><span style="color: #0000ff;">="Default"</span><span style="color: #ff0000;"> xmlns</span><span style="color: #0000ff;">="http://docs.oasis-open.org/odata/ns/edm"</span><span style="color: #0000ff;">&gt;</span>

            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">EntityContainer </span><span style="color: #ff0000;">Name</span><span style="color: #0000ff;">="Container"</span><span style="color: #0000ff;">&gt;</span>

                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">EntitySet </span><span style="color: #ff0000;">Name</span><span style="color: #0000ff;">="Persons"</span><span style="color: #ff0000;"> EntityType</span><span style="color: #0000ff;">="AbpODataDemo.People.Person"</span> <span style="color: #0000ff;">/&gt;</span>

            <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">EntityContainer</span><span style="color: #0000ff;">&gt;</span>

        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Schema</span><span style="color: #0000ff;">&gt;</span>

    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">edmx:DataServices</span><span style="color: #0000ff;">&gt;</span>

<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">edmx:Edmx</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<span class="cnblogs_code_collapse">元数据</span></div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a27"></a>二十七、Swagger UI 整合</span></strong></span></p>
<p>....使用启用Swagger的API，您可以获得交互式文档，客户端SDK生成和可发现性。</p>
<p>1，ASP.NET Core</p>
<p>①安装Nuget软件包<br />将Swashbuckle.AspNetCore nuget软件包安装到您的Web项目中</p>
<p>②配置</p>
<p>将Swagger的配置代码添加到Startup.cs的ConfigureServices方法中</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span><span style="color: #000000;"> IServiceProvider ConfigureServices(IServiceCollection services)
{
    </span><span style="color: #008000;">//</span><span style="color: #008000;">your other code...</span>
<span style="color: #000000;">    
      services.AddSwaggerGen(options </span>=&gt;<span style="color: #000000;">
            {
                options.SwaggerDoc(</span><span style="color: #800000;">"</span><span style="color: #800000;">v1</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span> Info { Title = <span style="color: #800000;">"</span><span style="color: #800000;">AbpZeroTemplate API</span><span style="color: #800000;">"</span>, Version = <span style="color: #800000;">"</span><span style="color: #800000;">v1</span><span style="color: #800000;">"</span><span style="color: #000000;"> });
                options.DocInclusionPredicate((docName, description) </span>=&gt; <span style="color: #0000ff;">true</span><span style="color: #000000;">);
            });
    
    </span><span style="color: #008000;">//</span><span style="color: #008000;">your other code...</span>
}</pre>
</div>
<p>然后，将以下代码添加到Startup.cs的Configure方法中以使用Swagger</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configure(IApplicationBuilder app, IHostingEnvironment env, ILoggerFactory loggerFactory)
{
    </span><span style="color: #008000;">//</span><span style="color: #008000;">your other code...</span>
<span style="color: #000000;">
     app.UseSwagger();
            </span><span style="color: #008000;">//</span><span style="color: #008000;">Enable middleware to serve swagger - ui assets(HTML, JS, CSS etc.)</span>
            app.UseSwaggerUI(options =&gt;<span style="color: #000000;">
            {
                options.SwaggerEndpoint(</span><span style="color: #800000;">"</span><span style="color: #800000;">/swagger/v1/swagger.json</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">AbpZeroTemplate API V1</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }); </span><span style="color: #008000;">//</span><span style="color: #008000;">URL: /swagger 
            
    </span><span style="color: #008000;">//</span><span style="color: #008000;">your other code...</span>
}</pre>
</div>
<p>就这样。 您可以浏览&ldquo;/swagger&rdquo;下的swagger ui。</p>
<p>2，ASP.NET 5.x</p>
<p><span style="color: #ff0000; font-size: 12px;">注意，swagger只能在webapi层使用。我在web层使用失败</span></p>
<p>①安装Nuget软件包<br />将Swashbuckle.Core nuget软件包安装到WebApi项目（或Web项目）。</p>
<p>②配置</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SwaggerIntegrationDemoWebApiModule : AbpModule
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Initialize()
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;">your other code...</span>
<span style="color: #000000;">
        ConfigureSwaggerUi();
    }

    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> ConfigureSwaggerUi()
    {
        Configuration.Modules.AbpWebApi().HttpConfiguration
            .EnableSwagger(c </span>=&gt;<span style="color: #000000;">
            {
                c.SingleApiVersion(</span><span style="color: #800000;">"</span><span style="color: #800000;">v1</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">SwaggerIntegrationDemo.WebApi</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                c.ResolveConflictingActions(apiDescriptions </span>=&gt;<span style="color: #000000;"> apiDescriptions.First());
            })
            .EnableSwaggerUi(c </span>=&gt;<span style="color: #000000;">
            {
                c.InjectJavaScript(Assembly.GetAssembly(</span><span style="color: #0000ff;">typeof</span>(AbpProjectNameWebApiModule)), <span style="color: #800000;">"</span><span style="color: #800000;">AbpCompanyName.AbpProjectName.Api.Scripts.Swagger-Custom.js</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            });
    }
}</span></pre>
</div>
<p>注意，在配置swagger ui时，我们注入一个名为&ldquo;Swagger-Custom.js&rdquo;的javascript文件。 此脚本文件用于在swagger ui上测试api服务时向请求中添加CSRF令牌。 您还需要将此文件作为嵌入式资源添加到WebApi项目中，并在注入时使用InjectJavaScript方法中的逻辑名称。</p>
<p>Swagger-Custom.js的内容在这里：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> getCookieValue = <span style="color: #0000ff;">function</span><span style="color: #000000;">(key) {
    </span><span style="color: #0000ff;">var</span> equalities = document.cookie.split('; '<span style="color: #000000;">);
    </span><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">var</span> i = 0; i &lt; equalities.length; i++<span style="color: #000000;">) {
        </span><span style="color: #0000ff;">if</span> (!<span style="color: #000000;">equalities[i]) {
            </span><span style="color: #0000ff;">continue</span><span style="color: #000000;">;
        }

        </span><span style="color: #0000ff;">var</span> splitted = equalities[i].split('='<span style="color: #000000;">);
        </span><span style="color: #0000ff;">if</span> (splitted.length !== 2<span style="color: #000000;">) {
            </span><span style="color: #0000ff;">continue</span><span style="color: #000000;">;
        }

        </span><span style="color: #0000ff;">if</span> (decodeURIComponent(splitted[0]) ===<span style="color: #000000;"> key) {
            </span><span style="color: #0000ff;">return</span> decodeURIComponent(splitted[1] || ''<span style="color: #000000;">);
        }
    }

    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">null</span><span style="color: #000000;">;
};

</span><span style="color: #0000ff;">var</span> csrfCookie = getCookieValue("XSRF-TOKEN"<span style="color: #000000;">);
</span><span style="color: #0000ff;">var</span> csrfCookieAuth = <span style="color: #0000ff;">new</span> SwaggerClient.ApiKeyAuthorization("X-XSRF-TOKEN", csrfCookie, "header"<span style="color: #000000;">);
swaggerUi.api.clientAuthorizations.add(</span>"X-XSRF-TOKEN", csrfCookieAuth);</pre>
</div>
<p>3，测试</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201710/741594-20171017210224881-397072669.png" alt="" width="589" height="260" /></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a28"></a>二十八、ASP.NET MVC</span></strong></span></p>
<p>1，ASP.NET MVC Controllers</p>
<p>①，mvc控制器继承AbpController&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">public class HomeController : AbpController
{
    public HomeController()
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;">您应该设置LocalizationSourceName使L方法工作。 您可以将其设置在您自己的基本控制器类中，以便不对每个控制器重复。</span>
        LocalizationSourceName = "MySourceName"<span style="color: #000000;">;
    }
    public ActionResult Index()
    {
        </span><span style="color: #0000ff;">var</span> helloWorldText = L("HelloWorld"<span style="color: #000000;">);
        </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> View();
    }
}</span></pre>
</div>
<p>②，授权</p>
<p>您可以为控制器或操作使用AbpMvcAuthorize属性，以防止未经授权的用户使用您的控制器和操作。 例：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">public class HomeController : AbpController
{
    [AbpMvcAuthorize(</span>"MyPermissionName"<span style="color: #000000;">)]
    public ActionResult Index()
    {
        </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> View();
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p>2，ASP.NET MVC Views</p>
<p>①AbpWebViewPage基类<br />ASP.NET Boilerplate还提供了AbpWebViewPage，它定义了一些有用的属性和方法。 如果您使用启动模板创建了项目，则所有视图都将自动从该基类继承。</p>
<p>②AbpWebViewPage定义L方法进行本地化，IsGranted方法授权，IsFeatureEnabled和GetFeatureValue方法进行功能管理等。</p>
<p>&nbsp;</p>
<p>3，处理异常</p>
<p>①启用错误处理<br />要启用ASP.NET MVC控制器的错误处理，必须为ASP.NET MVC应用程序启用customErrors模式。</p>
<div class="cnblogs_code">
<pre>&lt;customErrors mode="On" /&gt;//如果您不想在本地计算机中处理错误，它也可以是&ldquo;RemoteOnly&rdquo;。 请注意，这仅适用于ASP.NET MVC控制器，不需要Web API控制器。</pre>
</div>
<p>②非AJAX请求</p>
<p>如果请求不是AJAX，则会显示错误页面。</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">public ActionResult Index()
{
    </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> Exception("A sample exception message..."<span style="color: #000000;">);
}</span></pre>
</div>
<p>当然，这个异常可以被另一个从这个动作调用的方法抛出。 ASP.NET Boilerplate处理这个异常，记录它并显示'Error.cshtml'视图。 您可以自定义此视图以显示错误。 示例错误视图（ASP.NET Boilerplate模板中的默认错误视图）：</p>
<p>&nbsp;<img src="http://images2017.cnblogs.com/blog/741594/201710/741594-20171017213101662-2138637068.png" alt="" width="375" height="96" /></p>
<p>UserFriendlyException<br />UserFriendlyException是一种特殊类型的异常，直接显示给用户。 见下面的示例：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">public ActionResult Index()
{
    </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> UserFriendlyException("Ooppps! There is a problem!", "You are trying to see a product that is deleted..."<span style="color: #000000;">);
}</span></pre>
</div>
<p><img src="http://images2017.cnblogs.com/blog/741594/201710/741594-20171017213221881-1288146600.png" alt="" width="401" height="105" /></p>
<p>错误模型<br />ASP.NET Boilerplate将ErrorViewModel对象作为模型传递给&ldquo;错误&rdquo;视图：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">public class ErrorViewModel
{
    public AbpErrorInfo ErrorInfo { get; set; }

    public Exception Exception { get; set; }
}</span></pre>
</div>
<p>ErrorInfo包含有关可以向用户显示的错误的详细信息。 异常对象是抛出的异常。 如果需要，您可以查看并显示其他信息。 例如，如果是AbpValidationException，我们可以显示验证错误：</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201710/741594-20171017213355084-1100723121.png" alt="" width="452" height="162" /></p>
<p>③AJAX请求</p>
<p>&nbsp;如果MVC操作的返回类型是JsonResult（或异步操作的Task JsonResult），则ASP.NET Boilerplate会向客户端返回异常的JSON对象。 示例返回对象的错误：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">{
  </span>"targetUrl": <span style="color: #0000ff;">null</span><span style="color: #000000;">,
  </span>"result": <span style="color: #0000ff;">null</span><span style="color: #000000;">,
  </span>"success": <span style="color: #0000ff;">false</span><span style="color: #000000;">,
  </span>"error"<span style="color: #000000;">: {
    </span>"message": "An internal error occured during your request!"<span style="color: #000000;">,
    </span>"details": "..."<span style="color: #000000;">
  },
  </span>"unAuthorizedRequest": <span style="color: #0000ff;">false</span><span style="color: #000000;">
}</span></pre>
</div>
<p>④异常事件<br />当ASP.NET Boilerplare处理任何异常时，它会触发可以注册的AbpHandledExceptionData事件（有关事件总线的更多信息，请参见eventbus文档）。 例：</p>
<div class="cnblogs_code">
<pre>public class MyExceptionHandler : IEventHandler&lt;AbpHandledExceptionData&gt;<span style="color: #000000;">, ITransientDependency
{
    public </span><span style="color: #0000ff;">void</span><span style="color: #000000;"> HandleEvent(AbpHandledExceptionData eventData)
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;">TODO: Check eventData.Exception!</span>
<span style="color: #000000;">    }
}</span></pre>
</div>
<p>如果将此示例类放入应用程序（通常在您的Web项目中），将为ASP.NET Boilerplate处理的所有异常调用HandleEvent方法。 因此，您可以详细调查Exception对象。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt;"><a name="a29"></a><span style="color: #ffffff;">二十九、本地化</span></span></strong></p>
<p>1，应用语言，首先申明支持哪些语，&nbsp;这在模块的PreInitialize方法中完成</p>
<div class="cnblogs_code">
<pre>Configuration.Localization.Languages.Add(<span style="color: #0000ff;">new</span> LanguageInfo(<span style="color: #800000;">"</span><span style="color: #800000;">en</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">English</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">famfamfam-flag-england</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">true</span><span style="color: #000000;">));
Configuration.Localization.Languages.Add(</span><span style="color: #0000ff;">new</span> LanguageInfo(<span style="color: #800000;">"</span><span style="color: #800000;">tr</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">T&uuml;rk&ccedil;e</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">famfamfam-flag-tr</span><span style="color: #800000;">"</span>));</pre>
</div>
<p>在服务器端，您可以注入并使用ILocalizationManager。 在客户端，您可以使用abp.localization javascript API来获取所有可用语言和当前语言的列表。 famfamfam-flag-england（和tr）只是一个CSS类，您可以根据需要进行更改。 然后你可以在UI上使用它来显示相关的标志。</p>
<p>2，本地化来源</p>
<p>本地化文本可以存储在不同的来源。 即使您可以在同一应用程序中使用多个源（如果您有多个模块，每个模块可以定义一个独立的本地化源，或者一个模块可以定义多个源）。 ILocalizationSource接口应由本地化源实现。 然后它被注册到ASP.NET Boilerplate的本地化配置。</p>
<p>每个本地化源必须具有唯一的源名称。 有如下定义的预定义的本地化源类型（xml文件、json文件、资源文件等）。</p>
<p>①XML文件</p>
<p>本地化文本可以存储在XML文件中。 XML文件的内容是这样的：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;?</span><span style="color: #ff00ff;">xml version="1.0" encoding="utf-8" </span><span style="color: #0000ff;">?&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">localizationDictionary </span><span style="color: #ff0000;">culture</span><span style="color: #0000ff;">="en"</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">texts</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">text </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="TaskSystem"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">="Task System"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">text </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="TaskList"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">="Task List"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">text </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="NewTask"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">="New Task"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">text </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="Xtasks"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">="{0} tasks"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">text </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="CompletedTasks"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">="Completed tasks"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">text </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="EmailWelcomeMessage"</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">Hi,
Welcome to Simple Task System! This is a sample
email content.</span><span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">text</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">texts</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">localizationDictionary</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>XML文件必须是unicode（utf-8）。 culture =&ldquo;en&rdquo;表示此XML文件包含英文文本。 对于文本节点; name属性用于标识文本。 您可以使用值属性或内部文本（如最后一个）来设置本地化文本的值。 我们为每种语言创建一个分离的XML文件，如下所示：</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201710/741594-20171018113751646-54250993.png" alt="" /></p>
<p>SimpleTaskSystem是这里的源名称，SimpleTaskSystem.xml定义了默认语言。 当请求文本时，ASP.NET Boilerplate从当前语言的XML文件获取文本（使用Thread.CurrentThread.CurrentUICulture查找当前语言）。 如果当前语言不存在，则会从默认语言的XML文件获取文本。</p>
<p><strong>注册XML本地化源，XML文件可以存储在文件系统中，也可以嵌入到程序集中。</strong></p>
<p><span style="font-size: 12px;">对于文件系统存储的XML，我们可以注册一个XML定位源，如下所示（这在模块的PreInitialize事件中完成）：</span></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">Configuration.Localization.Sources.Add(
    </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> DictionaryBasedLocalizationSource(
        </span><span style="color: #800000;">"</span><span style="color: #800000;">SimpleTaskSystem</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> XmlFileLocalizationDictionaryProvider(
            HttpContext.Current.Server.MapPath(</span><span style="color: #800000;">"</span><span style="color: #800000;">~/Localization/SimpleTaskSystem</span><span style="color: #800000;">"</span><span style="color: #000000;">)
            )
        )
    );</span></pre>
</div>
<p><span style="font-size: 12px;">对于嵌入式XML文件，我们应该将所有本地化XML文件标记为嵌入式资源（选择XML文件，打开属性窗口（F4）并将Build Action作为嵌入式资源更改）。 然后我们可以注册本地化源，如下所示：</span></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">Configuration.Localization.Sources.Add(
    </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> DictionaryBasedLocalizationSource(
        </span><span style="color: #800000;">"</span><span style="color: #800000;">SimpleTaskSystem</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> XmlEmbeddedFileLocalizationDictionaryProvider(
            Assembly.GetExecutingAssembly(),
            </span><span style="color: #800000;">"</span><span style="color: #800000;">MyCompany.MyProject.Localization.Sources</span><span style="color: #800000;">"</span><span style="color: #000000;">
            )
        )
    );</span></pre>
</div>
<p>XmlEmbeddedFileLocalizationDictionaryProvider获取一个包含XML文件的程序集（GetExecutingAssembly简称为当前程序集）和XML文件的命名空间（命名空间+ XML文件的文件夹层次结构）。</p>
<p><span style="font-size: 12px; color: #ff0000;">注意：当添加语言后缀到嵌入式XML文件时，不要使用像MySource.tr.xml这样的点符号，而是使用像MySource-tr.xml这样的破折号，因为点符号在找到资源时会导致命名空间的问题。</span></p>
<p>②json文件</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">culture</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">en</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">texts</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">TaskSystem</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">Task system</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">Xtasks</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">{0} tasks</span><span style="color: #800000;">"</span><span style="color: #000000;">
  }
}</span></pre>
</div>
<p>JSON文件应该是unicode（utf-8）。 文化：&ldquo;en&rdquo;声明此JSON文件包含英文文本。 我们为每种语言创建一个分隔的JSON文件，如下所示：</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201710/741594-20171018145048287-1054544445.png" alt="" /></p>
<p>MySourceName是源名，MySourceName.json定义了默认语言。 它类似于XML文件。</p>
<p><br /><strong>注册JSON本地化源，JSON文件可以存储在文件系统中，也可以嵌入到程序集中。</strong></p>
<p>文件系统存储的JSONs，我们可以注册一个JSON本地化源码，如下所示（这在模块的PreInitialize事件中完成）：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">Configuration.Localization.Sources.Add(
    </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> DictionaryBasedLocalizationSource(
        </span><span style="color: #800000;">"</span><span style="color: #800000;">MySourceName</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> JsonFileLocalizationDictionaryProvider(
            HttpContext.Current.Server.MapPath(</span><span style="color: #800000;">"</span><span style="color: #800000;">~/Localization/MySourceName</span><span style="color: #800000;">"</span><span style="color: #000000;">)
            )
        )
    );</span></pre>
</div>
<p>对于嵌入式JSON文件，我们应将所有本地化JSON文件标记为嵌入式资源（选择JSON文件，打开属性窗口（F4），并将Build Action作为嵌入式资源更改）。 然后我们可以注册本地化源，如下所示：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;"> Configuration.Localization.Sources.Add(
    </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> DictionaryBasedLocalizationSource(
        </span><span style="color: #800000;">"</span><span style="color: #800000;">MySourceName</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> JsonEmbeddedFileLocalizationDictionaryProvider(
            Assembly.GetExecutingAssembly(),
            </span><span style="color: #800000;">"</span><span style="color: #800000;">MyCompany.MyProject.Localization.Sources</span><span style="color: #800000;">"</span><span style="color: #000000;">
            )
        )
    );</span></pre>
</div>
<p>JsonEmbeddedFileLocalizationDictionaryProvider获取一个包含JSON文件的程序集（GetExecutingAssembly简称为当前程序集）和JSON文件的命名空间（命名空间是计算的程序集名称和JSON文件的文件夹层次结构）。</p>
<p><span style="font-size: 12px; color: #ff0000;">注意：在嵌入式JSON文件中添加语言后缀时，请勿使用像MySource.tr.json这样的点符号，而是使用像MySource-tr.json这样的破折号，因为点符号在找到资源时会导致命名空间问题。</span></p>
<p>③资源文件</p>
<p>本地化文本也可以存储在.NET的资源文件中。 我们可以为每种语言创建资源文件，如下所示（右键单击项目，选择添加新项目，然后查找资源文件）。</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201710/741594-20171018145603474-354462742.png" alt="" /></p>
<p>MyTexts.resx包含默认语言文本，MyTexts.tr.resx包含土耳其语的文本。 当我们打开MyTexts.resx时，我们可以看到所有的文本：</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201710/741594-20171018145826740-1910336477.png" alt="" width="314" height="113" /></p>
<p>在这种情况下，ASP.NET Boilerplate使用.NET的内置资源管理器进行本地化。 您应该为资源配置本地化源：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">Configuration.Localization.Sources.Add(
    </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> ResourceFileLocalizationSource(
        </span><span style="color: #800000;">"</span><span style="color: #800000;">MySource</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        MyTexts.ResourceManager
        ));</span></pre>
</div>
<p>源的唯一名称是MySource，而MyTexts.ResourceManager是用于获取本地化文本的资源管理器的引用。 这在模块的PreInitialize事件中完成（有关更多信息，请参阅模块系统）。</p>
<p>3，获取本地化文本</p>
<p>①在服务器端，我们可以注入ILocalizationManager并使用它的GetString方法。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> s1 = _localizationManager.GetString(<span style="color: #800000;">"</span><span style="color: #800000;">SimpleTaskSystem</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">NewTask</span><span style="color: #800000;">"</span>);</pre>
</div>
<p>GetString方法根据当前线程的UI文化从本地化源获取字符串。 如果没有找到，它将回退到默认语言。</p>
<p>②为了不重复源的名字，你可以先拿到源，然后得到从源字符串：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> source = _localizationManager.GetSource(<span style="color: #800000;">"</span><span style="color: #800000;">SimpleTaskSystem</span><span style="color: #800000;">"</span><span style="color: #000000;">);
</span><span style="color: #0000ff;">var</span> s1 = source.GetString(<span style="color: #800000;">"</span><span style="color: #800000;">NewTask</span><span style="color: #800000;">"</span>);</pre>
</div>
<p>③在mvc控制器</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> HomeController : SimpleTaskSystemControllerBase
{
    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> ActionResult Index()
    {
        </span><span style="color: #0000ff;">var</span> helloWorldText = L(<span style="color: #800000;">"</span><span style="color: #800000;">HelloWorld</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> View();
    }
}</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SimpleTaskSystemControllerBase : AbpController
{
    </span><span style="color: #0000ff;">protected</span><span style="color: #000000;"> SimpleTaskSystemControllerBase()
    {
        LocalizationSourceName </span>= <span style="color: #800000;">"</span><span style="color: #800000;">SimpleTaskSystem</span><span style="color: #800000;">"</span><span style="color: #000000;">;
    }
}</span></pre>
</div>
<p>L方法用于本地化字符串。 当然，您必须提供源名称。 它在SimpleTaskSystemControllerBase中完成。注意它是从AbpController派生的。 因此，您可以使用L方法轻松本地化文本。</p>
<p>④在MVC视图，同样的L方法也存在于视图中：</p>
<div class="cnblogs_code">
<pre>&lt;div&gt;
    &lt;form id=<span style="color: #800000;">"</span><span style="color: #800000;">NewTaskForm</span><span style="color: #800000;">"</span> role=<span style="color: #800000;">"</span><span style="color: #800000;">form</span><span style="color: #800000;">"</span>&gt;
        &lt;div <span style="color: #0000ff;">class</span>=<span style="color: #800000;">"</span><span style="color: #800000;">form-group</span><span style="color: #800000;">"</span>&gt;
            &lt;label <span style="color: #0000ff;">for</span>=<span style="color: #800000;">"</span><span style="color: #800000;">TaskDescription</span><span style="color: #800000;">"</span>&gt;@L(<span style="color: #800000;">"</span><span style="color: #800000;">TaskDescription</span><span style="color: #800000;">"</span>)&lt;/label&gt;
            &lt;textarea id=<span style="color: #800000;">"</span><span style="color: #800000;">TaskDescription</span><span style="color: #800000;">"</span> data-bind=<span style="color: #800000;">"</span><span style="color: #800000;">value: task.description</span><span style="color: #800000;">"</span> <span style="color: #0000ff;">class</span>=<span style="color: #800000;">"</span><span style="color: #800000;">form-control</span><span style="color: #800000;">"</span> rows=<span style="color: #800000;">"</span><span style="color: #800000;">3</span><span style="color: #800000;">"</span> placeholder=<span style="color: #800000;">"</span><span style="color: #800000;">@L(</span><span style="color: #800000;">"</span>EnterDescriptionHere<span style="color: #800000;">"</span><span style="color: #800000;">)</span><span style="color: #800000;">"</span> required&gt;&lt;/textarea&gt;
        &lt;/div&gt;
        &lt;div <span style="color: #0000ff;">class</span>=<span style="color: #800000;">"</span><span style="color: #800000;">form-group</span><span style="color: #800000;">"</span>&gt;
            &lt;label <span style="color: #0000ff;">for</span>=<span style="color: #800000;">"</span><span style="color: #800000;">TaskAssignedPerson</span><span style="color: #800000;">"</span>&gt;@L(<span style="color: #800000;">"</span><span style="color: #800000;">AssignTo</span><span style="color: #800000;">"</span>)&lt;/label&gt;
            &lt;<span style="color: #0000ff;">select</span> id=<span style="color: #800000;">"</span><span style="color: #800000;">TaskAssignedPerson</span><span style="color: #800000;">"</span> data-bind=<span style="color: #800000;">"</span><span style="color: #800000;">options: people, optionsText: 'name', optionsValue: 'id', value: task.assignedPersonId, optionsCaption: '@L(</span><span style="color: #800000;">"</span>SelectPerson<span style="color: #800000;">"</span><span style="color: #800000;">)'</span><span style="color: #800000;">"</span> <span style="color: #0000ff;">class</span>=<span style="color: #800000;">"</span><span style="color: #800000;">form-control</span><span style="color: #800000;">"</span>&gt;&lt;/<span style="color: #0000ff;">select</span>&gt;
        &lt;/div&gt;
        &lt;button data-bind=<span style="color: #800000;">"</span><span style="color: #800000;">click: saveTask</span><span style="color: #800000;">"</span> type=<span style="color: #800000;">"</span><span style="color: #800000;">submit</span><span style="color: #800000;">"</span> <span style="color: #0000ff;">class</span>=<span style="color: #800000;">"</span><span style="color: #800000;">btn btn-primary</span><span style="color: #800000;">"</span>&gt;@L(<span style="color: #800000;">"</span><span style="color: #800000;">CreateTheTask</span><span style="color: #800000;">"</span>)&lt;/button&gt;
    &lt;/form&gt;
&lt;/div&gt;</pre>
</div>
<p>为了使这项工作，您应该从设置源名称的基类派生您的视图：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">class</span> SimpleTaskSystemWebViewPageBase : SimpleTaskSystemWebViewPageBase&lt;<span style="color: #0000ff;">dynamic</span>&gt;<span style="color: #000000;">
{

}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">class</span> SimpleTaskSystemWebViewPageBase&lt;TModel&gt; : AbpWebViewPage&lt;TModel&gt;<span style="color: #000000;">
{
    </span><span style="color: #0000ff;">protected</span><span style="color: #000000;"> SimpleTaskSystemWebViewPageBase()
    {
        LocalizationSourceName </span>= <span style="color: #800000;">"</span><span style="color: #800000;">SimpleTaskSystem</span><span style="color: #800000;">"</span><span style="color: #000000;">;
    }
}</span></pre>
</div>
<p>并在web.config中设置此视图基类：</p>
<div class="cnblogs_code">
<pre>&lt;pages pageBaseType=<span style="color: #800000;">"</span><span style="color: #800000;">SimpleTaskSystem.Web.Views.SimpleTaskSystemWebViewPageBase</span><span style="color: #800000;">"</span>&gt;</pre>
</div>
<p>⑤在Javascript中</p>
<p>ASP.NET Boilerplate也可以使用同样的本地化文本也是JavaScript代码。 首先，您应该在页面中添加动态ABP脚本：</p>
<div class="cnblogs_code">
<pre>&lt;script src="/AbpScripts/GetScripts" type="text/javascript"&gt;&lt;/script&gt;</pre>
</div>
<p>ASP.NET Boilerplate自动生成需要的JavaScript代码，以便在客户端获取本地化的文本。 然后，您可以轻松地获取javascript中的本地化文本，如下所示：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> s1 = abp.localization.localize('NewTask', 'SimpleTaskSystem');</pre>
</div>
<p>NewTask是文本名，SimpleTaskSystem是源名。 不要重复源名称，您可以先获取源代码，然后获取文本：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> source = abp.localization.getSource('SimpleTaskSystem'<span style="color: #000000;">);
</span><span style="color: #0000ff;">var</span> s1 = source('NewTask');</pre>
</div>
<p>格式参数，本地化方法也可以获得附加的格式参数。 例：</p>
<div class="cnblogs_code">
<pre>abp.localization.localize('RoleDeleteWarningMessage', 'MySource', 'Admin'<span style="color: #000000;">);

</span><span style="color: #008000;">//</span><span style="color: #008000;">如果使用getSource得到源，则如上所示</span>
source('RoleDeleteWarningMessage', 'Admin');</pre>
</div>
<p>如果RoleDeleteWarningMessage ='Role {0}将被删除'，那么本地化的文本将被&ldquo;Role Admin将被删除&rdquo;。</p>
<p><br />默认本地化源，您可以设置默认的本地化源，并使用没有源名称的abp.localization.localize方法。</p>
<div class="cnblogs_code">
<pre>abp.localization.defaultSourceName = 'SimpleTaskSystem'<span style="color: #000000;">;
</span><span style="color: #0000ff;">var</span> s1 = abp.localization.localize('NewTask');</pre>
</div>
<p>defaultSourceName是全局的，一次只能运行一个源。</p>
<p>4，扩展本地化源</p>
<p>ASP.NET Boilerplate还定义了一些本地化源。 例如，Abp.Web nuget软件包将一个名为&ldquo;AbpWeb&rdquo;的本地化源定义为嵌入式XML文件：</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201710/741594-20171018172821677-247116186.png" alt="" /></p>
<p>默认（英文）XML文件如下（仅显示前两个文本）：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;?</span><span style="color: #ff00ff;">xml version="1.0" encoding="utf-8" </span><span style="color: #0000ff;">?&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">localizationDictionary </span><span style="color: #ff0000;">culture</span><span style="color: #0000ff;">="en"</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">texts</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">text </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="InternalServerError"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">="An internal error occurred during your request!"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">text </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="ValidationError"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">="Your request is not valid!"</span> <span style="color: #0000ff;">/&gt;</span><span style="color: #000000;">
    ...
  </span><span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">texts</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">localizationDictionary</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>为了扩展AbpWeb源，我们可以定义XML文件。 假设我们只想改变InternalServerError文本。 我们可以定义一个XML文件，如下所示：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;?</span><span style="color: #ff00ff;">xml version="1.0" encoding="utf-8" </span><span style="color: #0000ff;">?&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">localizationDictionary </span><span style="color: #ff0000;">culture</span><span style="color: #0000ff;">="en"</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">texts</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">text </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="InternalServerError"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">="Sorry :( It seems there is a problem. Let us to solve it and please try again later."</span> <span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">texts</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">localizationDictionary</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>然后我们可以在我们的模块的PreInitialize方法上注册它：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">Configuration.Localization.Sources.Extensions.Add(
    </span><span style="color: #0000ff;">new</span> LocalizationSourceExtensionInfo(<span style="color: #800000;">"</span><span style="color: #800000;">AbpWeb</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> XmlFileLocalizationDictionaryProvider(
            HttpContext.Current.Server.MapPath(</span><span style="color: #800000;">"</span><span style="color: #800000;">~/Localization/AbpWebExtensions</span><span style="color: #800000;">"</span><span style="color: #000000;">)
            )
        )
    );</span></pre>
</div>
<p>5，获取语言</p>
<p>ILanguageManager可用于获取所有可用语言和当前语言的列表。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a30"></a>三十、导航</span></strong></span></p>
<p>1，创建菜单</p>
<p>应用程序可能由不同的模块组成，每个模块都可以拥有自己的菜单项。 要定义菜单项，我们需要创建一个派生自NavigationProvider的类。</p>
<p>假设我们有一个主菜单，如下所示：</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201710/741594-20171018173810506-569647026.png" alt="" /></p>
<p>这里，管理菜单项有两个子菜单项。 示例导航提供程序类创建这样的菜单可以如下所示：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SimpleTaskSystemNavigationProvider : NavigationProvider
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> SetNavigation(INavigationProviderContext context)
    {
        context.Manager.MainMenu
            .AddItem(
                </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> MenuItemDefinition(
                    </span><span style="color: #800000;">"</span><span style="color: #800000;">Tasks</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    </span><span style="color: #0000ff;">new</span> LocalizableString(<span style="color: #800000;">"</span><span style="color: #800000;">Tasks</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">SimpleTaskSystem</span><span style="color: #800000;">"</span><span style="color: #000000;">),
                    url: </span><span style="color: #800000;">"</span><span style="color: #800000;">/Tasks</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    icon: </span><span style="color: #800000;">"</span><span style="color: #800000;">fa fa-tasks</span><span style="color: #800000;">"</span><span style="color: #000000;">
                    )
            ).AddItem(
                </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> MenuItemDefinition(
                    </span><span style="color: #800000;">"</span><span style="color: #800000;">Reports</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    </span><span style="color: #0000ff;">new</span> LocalizableString(<span style="color: #800000;">"</span><span style="color: #800000;">Reports</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">SimpleTaskSystem</span><span style="color: #800000;">"</span><span style="color: #000000;">),
                    url: </span><span style="color: #800000;">"</span><span style="color: #800000;">/Reports</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    icon: </span><span style="color: #800000;">"</span><span style="color: #800000;">fa fa-bar-chart</span><span style="color: #800000;">"</span><span style="color: #000000;">
                    )
            ).AddItem(
                </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> MenuItemDefinition(
                    </span><span style="color: #800000;">"</span><span style="color: #800000;">Administration</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    </span><span style="color: #0000ff;">new</span> LocalizableString(<span style="color: #800000;">"</span><span style="color: #800000;">Administration</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">SimpleTaskSystem</span><span style="color: #800000;">"</span><span style="color: #000000;">),
                    icon: </span><span style="color: #800000;">"</span><span style="color: #800000;">fa fa-cogs</span><span style="color: #800000;">"</span><span style="color: #000000;">
                    ).AddItem(
                        </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> MenuItemDefinition(
                            </span><span style="color: #800000;">"</span><span style="color: #800000;">UserManagement</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                            </span><span style="color: #0000ff;">new</span> LocalizableString(<span style="color: #800000;">"</span><span style="color: #800000;">UserManagement</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">SimpleTaskSystem</span><span style="color: #800000;">"</span><span style="color: #000000;">),
                            url: </span><span style="color: #800000;">"</span><span style="color: #800000;">/Administration/Users</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                            icon: </span><span style="color: #800000;">"</span><span style="color: #800000;">fa fa-users</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                            requiredPermissionName: </span><span style="color: #800000;">"</span><span style="color: #800000;">SimpleTaskSystem.Permissions.UserManagement</span><span style="color: #800000;">"</span><span style="color: #000000;">
                            )
                    ).AddItem(
                        </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> MenuItemDefinition(
                            </span><span style="color: #800000;">"</span><span style="color: #800000;">RoleManagement</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                            </span><span style="color: #0000ff;">new</span> LocalizableString(<span style="color: #800000;">"</span><span style="color: #800000;">RoleManagement</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">SimpleTaskSystem</span><span style="color: #800000;">"</span><span style="color: #000000;">),
                            url: </span><span style="color: #800000;">"</span><span style="color: #800000;">/Administration/Roles</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                            icon: </span><span style="color: #800000;">"</span><span style="color: #800000;">fa fa-star</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                            requiredPermissionName: </span><span style="color: #800000;">"</span><span style="color: #800000;">SimpleTaskSystem.Permissions.RoleManagement</span><span style="color: #800000;">"</span><span style="color: #000000;">
                            )
                    )
            );
    }
}</span></pre>
</div>
<p>MenuItemDefinition基本上可以有唯一的名称，可本地化的显示名称，url和图标。 也，</p>
<p>2，注册导航</p>
<p>创建导航提供程序后，我们应该在我们的模块的PreInitialize事件上注册到ASP.NET Boilerplate配置：&nbsp;</p>
<div class="cnblogs_code">
<pre>Configuration.Navigation.Providers.Add&lt;SimpleTaskSystemNavigationProvider&gt;(); </pre>
</div>
<p>3，显示菜单</p>
<p>IUserNavigationManager可以被注入并用于获取菜单项并显示给用户。 因此，我们可以在服务器端创建菜单。</p>
<p>ASP.NET Boilerplate自动生成一个JavaScript API来获取客户端的菜单和项目。 abp.nav命名空间下的方法和对象可以用于此目的。 例如，可以使用abp.nav.menus.MainMenu来获取应用程序的主菜单。 因此，我们可以在客户端创建菜单。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a31"></a>三十一、嵌入式资源文件</span></strong></span></p>
<p>在一个web应用中，有供客户端使用的javascript，css，xml等文件。它们一般是作为分离的文件被添加到web项目中并发布。有时，我们需要将这些文件打包到一个程序集（类库项目，一个dll文件）中，作为内嵌资源散布到程序集中。ABP提供了一个基础设施使得这个很容易实现。</p>
<p>1，创建嵌入式文件</p>
<p>我们首先应该创建一个资源文件并把它标记为<strong>内嵌的资源</strong>。任何程序集都可以包含内嵌的资源文件。假设我们有一个叫做&ldquo;Abp.Zero.Web.UI.Metronic.dll&rdquo;程序集，而且它包含了javascript，css，和图片文件：</p>
<p>①xproj / project.json格式<br />假设我们有一个名为EmbeddedPlugIn的项目，如下所示：</p>
<p>&nbsp;<img src="http://images2017.cnblogs.com/blog/741594/201710/741594-20171018181303709-667437597.png" alt="" /></p>
<p>我们想要使这些文件在一个web应用中可用，首先，我们应该将想要暴露的文件标记为<strong>内嵌的资源</strong>。在这里，我选择了&nbsp;<strong>metronic.js</strong>文件，右键打开属性面板（快捷键是F4）。</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201710/741594-20171018181334302-2065026478.png" alt="" /></p>
<p>选中你想在web应用中使用的所有文件，将<strong>生成操作（build action）</strong>的属性值选为<strong>内嵌的 资源</strong>。</p>
<p>2，暴露内嵌文件</p>
<p>ABP使得暴露这些内嵌资源很容易，只需要一行代码：</p>
<div class="cnblogs_code">
<pre>WebResourceHelper.ExposeEmbeddedResources(<span style="color: #800000;">"</span><span style="color: #800000;">AbpZero/Metronic</span><span style="color: #800000;">"</span>, Assembly.GetExecutingAssembly(), <span style="color: #800000;">"</span><span style="color: #800000;">Abp.Zero.Web.UI.Metronic</span><span style="color: #800000;">"</span>);</pre>
</div>
<p>这行代码一般放在模块的Initialize方法中，下面解释一下这些参数：</p>
<ul>
<li>第一个参数为这些文件定义了<strong>根文件夹</strong>，它匹配了根命名空间。</li>
<li>第二个参数定义了包含这些文件的<strong>程序集</strong>。本例中，我传入了包含这行代码的程序集。但你也可以传入任何包含内嵌资源的程序集。</li>
<li>最后一个参数定义了这些文件在程序集的根命名空间。它是&ldquo;默认的命名空间&rdquo;加上&ldquo;文件夹名&rdquo;。默认的命名空间一般和程序集的名字是相同的，但是在程序集的属性中进行更改。这里 ，默认的命名空间是Abp(已经更改了)，因此Metronic文件夹的命名空间是&ldquo;Abp.Zero.Web.UI.Metronic&rdquo;。</li>
</ul>
<p>3，使用内嵌文件</p>
<p>可以直接使用内嵌的资源：</p>
<div class="cnblogs_code">
<pre>&lt;script type=<span style="color: #800000;">"</span><span style="color: #800000;">text/javascript</span><span style="color: #800000;">"</span> src=<span style="color: #800000;">"</span><span style="color: #800000;">~/AbpZero/Metronic/assets/global/scripts/metronic.js</span><span style="color: #800000;">"</span>&gt;&lt;/script&gt;</pre>
</div>
<p>ABP知道这是一个内嵌的资源，因而可以从之前暴露的dll中获得文件。此外，还可以在razor视图中使用HtmlHelper的扩展方法<strong>IncludeScript</strong>:</p>
<div class="cnblogs_code">
<pre>@Html.IncludeScript(<span style="color: #800000;">"</span><span style="color: #800000;">~/AbpZero/Metronic/assets/global/scripts/metronic.js</span><span style="color: #800000;">"</span>)</pre>
</div>
<p>这会产生下面的代码：</p>
<div class="cnblogs_code">
<pre>&lt;script src=<span style="color: #800000;">"</span><span style="color: #800000;">/AbpZero/Metronic/assets/global/scripts/metronic.js?v=635438748506909100</span><span style="color: #800000;">"</span> type=<span style="color: #800000;">"</span><span style="color: #800000;">text/javascript</span><span style="color: #800000;">"</span>&gt;&lt;/script&gt;</pre>
</div>
<p>唯一的不同就是参数<strong>v=635438748506909100</strong>。这样做的好处是阻止了浏览器端脚本的<strong>失败缓存</strong>。该值只有当你的dll重新生成（实际上是文件的最后写入时间）的时候才会改变，而且如果该值改变了，浏览器就不会缓存这个文件了。因此，建议使用IncludeScript方式。这对于非嵌入的物理资源也是有效的。对应于css文件，也存在相应的<strong>IncludeStyle</strong>方法。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a33"></a>三十三、CSRF / XSRF保护</span></strong></span></p>
<p>&ldquo;跨站点请求伪造（CSRF）&rdquo;是一种当恶意网站，电子邮件，博客，即时消息或程序导致用户的Web浏览器对用户所在的受信任站点执行不必要的操作时发生的攻击类型 目前认证的&ldquo;（OWASP）。</p>
<p>1，ASP.NET MVC</p>
<p>①ABP做了下面这些事情来客服上面的困难：</p>
<ul>
<li>actions会被<strong>自动保护</strong>（通过AbpAntiForgeryMvcFilter）。自动保护可以应对大多数情况。当然，可以使用<strong>DisableAbpAntiForgeryTokenValidation</strong>特性为任何action和Controller关闭自动保护，也可以使用&nbsp;<strong>ValidateAbpAntiForgeryToken</strong>特性打开。</li>
<li>除了HTML的表单域，<strong>AbpAntiForgeryMvcFilter</strong>也会检查请求头中的token。因此，可以很容易对ajax请求使用反伪造token保护。</li>
<li>在js中可以使用<strong>abp.security.antiForgery.getToken()</strong>函数获得token。</li>
<li>为所有的ajax请求头部自动添加反伪造token。</li>
</ul>
<p>②在<strong>Layout</strong>视图中添加以下代码：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">@{
    SetAntiForgeryCookie();
}</span></pre>
</div>
<p>这样，所有使用了这个布局页的页面都会包含这句代码了，该方法定义在ABP视图基类中，它会创建和设置正确的token cookie，使得在js端可以工作。如果有多个Layout的话，需要为每个布局添加上面的代码。</p>
<p>对于ASP.NET MVC 应用，只需要做这么多，所有的ajax请求都会自动工作。但是对于HTML 表单仍然需要使用** @Html.AntiForgeryToken()** HTML帮助方法，因为表单不是通过Ajax提交的，但是不需要在相应的action上使用ValidateAbpAntiForgeryToken 特性了。</p>
<p>③配置</p>
<p>XSRF默认是打开的，也可以在模块的PreInitialize方法中关闭或配置，如下：</p>
<div class="cnblogs_code">
<pre>Configuration.Modules.AbpWeb().AntiForgery.IsEnabled = <span style="color: #0000ff;">false</span>;</pre>
</div>
<p>也可以使用Configuration.Modules.AbpWebCommon().AntiForgery对象配置token和cookie名称。</p>
<p>2，ASP.NET WEB API</p>
<p>ASP.NET Web API不包括反伪造机制，ABP为ASP.NET Web API Controllers提供了基础设施来添加CSRF保护，并且是完全自动化的。</p>
<p>①<strong>ASP.NET MVC客户端</strong></p>
<p>如果在MVC项目中使用了Web API,那么<strong>不需要额外的配置</strong>。只要Ajax请求是从一个配置的MVC应用中发出的，即使你的Web API层自宿主在其它进程中，也不需要配置。</p>
<p>②其他客户端</p>
<p>如果你的客户端是其它类型的应用（比如，一个独立的angularjs应用，它不能像之前描述的那样使用SetAntiForgeryCookie()方法），那么你应该提供一种设置反伪造token cookie的方法。一种可能的实现方式是像下面那样创建一个api控制器：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Net.Http;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Web.Security.AntiForgery;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.WebApi.Controllers;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> AngularForgeryDemo.Controllers
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> AntiForgeryController : AbpApiController
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> IAbpAntiForgeryManager _antiForgeryManager;

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> AntiForgeryController(IAbpAntiForgeryManager antiForgeryManager)
        {
            _antiForgeryManager </span>=<span style="color: #000000;"> antiForgeryManager;
        }

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> HttpResponseMessage GetTokenCookie()
        {
            </span><span style="color: #0000ff;">var</span> response = <span style="color: #0000ff;">new</span><span style="color: #000000;"> HttpResponseMessage();

            _antiForgeryManager.SetCookie(response.Headers);

            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> response;
        }
    }
}</span></pre>
</div>
<p>然后就可以从客户端调用这个action来设置cookie了。</p>
<p>3，客户端类</p>
<p>①jQuery</p>
<p>abp.jquery.js中定义了一个ajax拦截器，它可以将反伪造请求token添加到每个请求的请求头中，它会从<strong>abp.security.antiForgery.getToken()</strong>函数中获得token。</p>
<p>②Angularjs</p>
<p>Angularjs会将反伪造token自动添加到所有的ajax请求中，请<strong><a href="https://docs.angularjs.org/api/ng/service/$http">点击链接</a></strong>查看Angularjs的XSRF保护一节。ABP默认使用了相同的cookie和header名称。因此，Angularjs集成是现成可用的。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a34"></a>三十四、后台工作(Jobs)和工作者（Workers）</span></strong></span></p>
<p>1，后台工作</p>
<p>后台作业用于将某些任务排列在后台以排队和持久的方式执行。 您可能需要后台工作，原因有几个。 一些例子：</p>
<ul>
<li>执行<strong>长时间运行的任务</strong>。比如，一个用户按了&ldquo;report&rdquo;按钮来启动一个长时间运行的报告工作，点击了这个按钮你不可能让用户一直处于等待状态，所以你应该将这个工作（job）添加到&nbsp;<strong>队列（queue）</strong>中，然后，当这项工作完成时，通过邮件将报告结果发送给该用户。</li>
<li>创建<strong>重复尝试（re-trying）和持续的任务</strong>来保证代码将会&nbsp;<strong>成功执行</strong>。比如，你可以在后台工作中发送邮件以克服&nbsp;<strong>临时失败</strong>，并&nbsp;<strong>保证</strong>邮件最终能够发送出去。因此，当发送邮件的时候用户不需要等待。</li>
</ul>
<p>①创建后台工作</p>
<p>我们可以通过继承BackgroundJob &lt;TArgs&gt;类或直接实现IBackgroundJob &lt;TArgs&gt;接口来创建一个后台作业类。这是最简单的后台工作：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> TestJob : BackgroundJob&lt;<span style="color: #0000ff;">int</span>&gt;<span style="color: #000000;">, ITransientDependency
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span> Execute(<span style="color: #0000ff;">int</span><span style="color: #000000;"> number)
    {
        Logger.Debug(number.ToString());
    }
}</span></pre>
</div>
<p>后台作业定义了一个Execute方法获取一个输入参数。 参数类型定义为通用类参数，如示例所示。</p>
<p>后台作业必须注册到依赖注入。 实现ITransientDependency是最简单的方法。</p>
<p>我们来定义一个更现实的工作，在后台队列中发送电子邮件：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> SimpleSendEmailJob : BackgroundJob&lt;SimpleSendEmailJobArgs&gt;<span style="color: #000000;">, ITransientDependency
{
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span> IRepository&lt;User, <span style="color: #0000ff;">long</span>&gt;<span style="color: #000000;"> _userRepository;
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> IEmailSender _emailSender;

    </span><span style="color: #0000ff;">public</span> SimpleSendEmailJob(IRepository&lt;User, <span style="color: #0000ff;">long</span>&gt;<span style="color: #000000;"> userRepository, IEmailSender emailSender)
    {
        _userRepository </span>=<span style="color: #000000;"> userRepository;
        _emailSender </span>=<span style="color: #000000;"> emailSender;
    }
    
    [UnitOfWork]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Execute(SimpleSendEmailJobArgs args)
    {
        </span><span style="color: #0000ff;">var</span> senderUser =<span style="color: #000000;"> _userRepository.Get(args.SenderUserId);
        </span><span style="color: #0000ff;">var</span> targetUser =<span style="color: #000000;"> _userRepository.Get(args.TargetUserId);

        _emailSender.Send(senderUser.EmailAddress, targetUser.EmailAddress, args.Subject, args.Body);
    }
}</span></pre>
</div>
<p>我们注入了user仓储（为了获得用户信息）和email发送者（发送邮件的服务），然后简单地发送了该邮件。<strong>SimpleSendEmailJobArgs</strong>是该工作的参数，它定义如下：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">[Serializable]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SimpleSendEmailJobArgs
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">long</span> SenderUserId { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">long</span> TargetUserId { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Subject { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Body { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}</span></pre>
</div>
<p>工作参数应该是<strong>serializable(可序列化)</strong>，因为要将它&nbsp;<strong>序列化并存储</strong>到数据库中。虽然ABP默认的后台工作管理者使用了JSON序列化（它不需要[Serializable]特性），但是最好定义&nbsp;<strong>[Serializable]</strong>特性，因为我们将来可能会转换到其他使用二进制序列化的工作管理者。</p>
<p>记住，<strong>要保持你的参数简单</strong>，不要在参数中包含实体或者其他非可序列化的对象。正如上面的例子演示的那样，我们只存储了实体的&nbsp;<strong>Id</strong>，然后在该工作的内部从仓储中获得该实体。</p>
<p>②添加新工作到队列</p>
<p>定义后台作业后，我们可以注入并使用IBackgroundJobManager将作业添加到队列中。 参见上面定义的TestJob的示例：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">[AbpAuthorize]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyEmailAppService : ApplicationService, IMyEmailAppService
{
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> IBackgroundJobManager _backgroundJobManager;

    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> MyEmailAppService(IBackgroundJobManager backgroundJobManager)
    {
        _backgroundJobManager </span>=<span style="color: #000000;"> backgroundJobManager;
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span><span style="color: #000000;"> Task SendEmail(SendEmailInput input)
    {
            </span><span style="color: #0000ff;">await</span> _backgroundJobManager.EnqueueAsync&lt;SimpleSendEmailJob, SimpleSendEmailJobArgs&gt;<span style="color: #000000;">(
            </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> SimpleSendEmailJobArgs
            {
                Subject </span>=<span style="color: #000000;"> input.Subject,
                Body </span>=<span style="color: #000000;"> input.Body,
                SenderUserId </span>=<span style="color: #000000;"> AbpSession.GetUserId(),
                TargetUserId </span>=<span style="color: #000000;"> input.TargetUserId
            });
    }
}</span></pre>
</div>
<p>Enqueu (或 EnqueueAsync)方法还有其他的参数，比如&nbsp;<strong>priority和 delay（优先级和延迟）</strong>。</p>
<p>③IBackgroundJobManager默认实现</p>
<p>IBackgroundJobManager默认是由<strong>BackgroundJobManager</strong>实现的。它可以被其他的后台工作提供者替代（看后面的Hangfire集成）。关于默认的BackgroundJobManager一些信息如下：</p>
<ul>
<li>它是一个在单线程中以<strong>FIFO（First In First Out）</strong>工作的简单工作队列，使用&nbsp;<strong>IBackgroundJobStore</strong>来持久化工作。</li>
<li>它会<strong>重复尝试</strong>执行工作，直到工作成功执行（不会抛出任何异常）或者超时。默认的超时是一个工作2天。</li>
<li>当成功执行后，它会从存储（数据库）中<strong>删除</strong>该工作。如果超时了，就会将该工作设置为&nbsp;<strong>abandoned（废弃的）</strong>，并保留在数据库中。</li>
<li>在重复尝试一个工作之间会<strong>增加等待时间</strong>。第一次重试时等待1分钟，第二次等待2分钟，第三次等待4分钟等等。</li>
<li>在固定的时间间隔轮询工作的存储。查询工作时先按优先级排序，再按尝试次数排序。</li>
</ul>
<p><strong>后台工作存储</strong></p>
<p>默认的BackgroundJobManager需要一个数据存储来保存、获得工作。如果你没有实现<strong>IBackgroundJobStore</strong>，那么它会使用&nbsp;<strong>InMemoryBackgroundJobStore</strong>，它不会将工作持久化到数据库中。你可以简单地实现它来存储工作到数据库或者你可以使用module-zero，它已经实现了IBackgroundJobStore。</p>
<p>如果你正在使用第三方的工作管理者（像Hangfire），那么不需要实现IBackgroundJobStore。</p>
<p>④配置</p>
<p>您可以在模块的PreInitialize方法中使用Configuration.BackgroundJobs来配置后台作业系统。</p>
<p><strong>关闭工作执行功能</strong><br />你可能想关闭应用程序的后台工作执行：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyProjectWebModule : AbpModule
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> PreInitialize()
    {
        Configuration.BackgroundJobs.IsJobExecutionEnabled </span>= <span style="color: #0000ff;">false</span><span style="color: #000000;">;
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
}</pre>
</div>
<p>2，后台工作者</p>
<p>后台工作者不同于后台工作。它们是运行在应用后台的简单<strong>独立线程</strong>。一般来说，它们会定期地执行一些任务。比如：</p>
<ul>
<li>后台工作者可以定期运行来<strong>删除旧的日志</strong>。</li>
<li>后台工作者可以定期运行来<strong>确定不活跃的用户</strong>，并给他们发送邮件以使他们返回你的应用。</li>
</ul>
<p>①创建后台工作者</p>
<p>要创建后台工作者，我们应该实现<strong>IBackgroundWorker</strong>接口。除此之外，我们可以基于需求从&nbsp;<strong>BackgroundWorkerBase</strong>或者&nbsp;<strong>PeriodicBackgroundWorkerBase</strong>继承。</p>
<p>假设一个用户在过去30天内没有登录到该应用，那我们想要让Ta的状态为passive。看下面的代码：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MakeInactiveUsersPassiveWorker : PeriodicBackgroundWorkerBase, ISingletonDependency
{
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span> IRepository&lt;User, <span style="color: #0000ff;">long</span>&gt;<span style="color: #000000;"> _userRepository;

    </span><span style="color: #0000ff;">public</span> MakeInactiveUsersPassiveWorker(AbpTimer timer, IRepository&lt;User, <span style="color: #0000ff;">long</span>&gt;<span style="color: #000000;"> userRepository)
        : </span><span style="color: #0000ff;">base</span><span style="color: #000000;">(timer)
    {
        _userRepository </span>=<span style="color: #000000;"> userRepository;
        Timer.Period </span>= <span style="color: #800080;">5000</span>; <span style="color: #008000;">//</span><span style="color: #008000;">5 seconds (good for tests, but normally will be more)</span>
<span style="color: #000000;">    }

    [UnitOfWork]
    </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> DoWork()
    {
        </span><span style="color: #0000ff;">using</span><span style="color: #000000;"> (CurrentUnitOfWork.DisableFilter(AbpDataFilters.MayHaveTenant))
        {
            </span><span style="color: #0000ff;">var</span> oneMonthAgo = Clock.Now.Subtract(TimeSpan.FromDays(<span style="color: #800080;">30</span><span style="color: #000000;">));

            </span><span style="color: #0000ff;">var</span> inactiveUsers = _userRepository.GetAllList(u =&gt;<span style="color: #000000;">
                u.IsActive </span>&amp;&amp;<span style="color: #000000;">
                ((u.LastLoginTime </span>&lt; oneMonthAgo &amp;&amp; u.LastLoginTime != <span style="color: #0000ff;">null</span>) || (u.CreationTime &lt; oneMonthAgo &amp;&amp; u.LastLoginTime == <span style="color: #0000ff;">null</span><span style="color: #000000;">))
                );

            </span><span style="color: #0000ff;">foreach</span> (<span style="color: #0000ff;">var</span> inactiveUser <span style="color: #0000ff;">in</span><span style="color: #000000;"> inactiveUsers)
            {
                inactiveUser.IsActive </span>= <span style="color: #0000ff;">false</span><span style="color: #000000;">;
                Logger.Info(inactiveUser </span>+ <span style="color: #800000;">"</span><span style="color: #800000;"> made passive since he/she did not login in last 30 days.</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }

            CurrentUnitOfWork.SaveChanges();
        }
    }
}</span></pre>
</div>
<p>这是现实中的代码，并且在具有module-zero模块的ABP中直接有效。</p>
<ul>
<li>如果你从<strong>PeriodicBackgroundWorkerBase</strong>&nbsp;类继承（如这个例子），那么你应该实现&nbsp;<strong>DoWork</strong>方法来执行定期运行的代码。</li>
<li>如果从<strong>BackgroundWorkerBase</strong>继承或直接实现了&nbsp;<strong>IBackgroundWorker</strong>，那么你要重写或者实现Start, Stop 和 WaitToStop方法。Start和Stop方法应该是&nbsp;<strong>非阻塞的（non-blocking）</strong>，WaitToStop方法应该等待工作者完成当前重要的工作。</li>
</ul>
<p>②注册后台工作者</p>
<p>创建一个后台工作者后，我们应该把它添加到<strong>IBackgroundWorkerManager</strong>，通常放在模块的PostInitialize方法中：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyProjectWebModule : AbpModule
{
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>

    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> PostInitialize()
    {
        </span><span style="color: #0000ff;">var</span> workManager = IocManager.Resolve&lt;IBackgroundWorkerManager&gt;<span style="color: #000000;">();
        workManager.Add(IocManager.Resolve</span>&lt;MakeInactiveUsersPassiveWorker&gt;<span style="color: #000000;">());
    }
}</span></pre>
</div>
<p>虽然一般我们将工作者添加到PostInitialize方法中，但是没有强制要求。你可以在任何地方注入IBackgroundWorkerManager，在运行时添加工作者。<br />当应用要关闭时，IBackgroundWorkerManager会停止并释放所有注册的工作者。</p>
<p>③后台工作者生命周期</p>
<p>&nbsp;后台工作者一般实现为单例的，但是没有严格限制。如果你需要相同工作者类的多个实例，那么可以使它成为transient（每次使用时创建），然后给IBackgroundWorkerManager添加多个实例。在这种情况下，你的工作者很可能会参数化（比如，你有单个LogCleaner类，但是两个LogCleaner工作者实例会监视并清除不同的log文件夹）。</p>
<p>3，让你的应用程序一直运行</p>
<p>只有当你的应用运行时，后台工作和工作者才会工作。如果一个Asp.Net 应用长时间没有执行请求，那么它默认会关闭（shutdown）。如果你想让后台工作一直在web应用中执行（这是默认行为），那么你要确保web应用配置成了总是运行。否则，后台工作只有在应用使用时才会执行。</p>
<p>有很多技术来实现这个目的。最简单的方法是从外部应用定期向你的web应用发送请求。这样，你可以检查web应用是否开启并且处于运行状态。<strong><a href="http://docs.hangfire.io/en/latest/deployment-to-production/making-aspnet-app-always-running.html">Hangfire文档</a></strong>讲解了一些其他的方法。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a35"></a>三十五、Hangfire集成</span></strong></span></p>
<p>Hangfire是一个综合的后台工作管理者。你可以将Hangfire集成到ABP中，这样就可以不使用默认的后台工作管理者了。但你仍然可以为Hangfire使用<strong>相同的后台工作API</strong>。这样，你的代码就独立于Hangfire了，但是，如果你喜欢的话，也可以直接使用&nbsp;<strong>Hangfire的API</strong>。</p>
<p>1，ASP.NET MVC 5.x 集成</p>
<p>Abp.HangFire nuget包用于ASP.NET MVC 5.x项目：</p>
<div class="cnblogs_code">
<pre>Install-Package Abp.HangFire</pre>
</div>
<p>然后，您可以为Hangfire安装任何存储。 最常见的是SQL Server存储（请参阅Hangfire.SqlServer nuget软件包）。 安装这些nuget软件包后，您可以将项目配置为使用Hangfire，如下所示：</p>
<div class="cnblogs_code">
<pre>[DependsOn(<span style="color: #0000ff;">typeof</span><span style="color: #000000;"> (AbpHangfireModule))]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyProjectWebModule : AbpModule
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> PreInitialize()
    {
        Configuration.BackgroundJobs.UseHangfire(configuration </span>=&gt;<span style="color: #000000;">
        {
            configuration.GlobalConfiguration.UseSqlServerStorage(</span><span style="color: #800000;">"</span><span style="color: #800000;">Default</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        });
                
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
}</pre>
</div>
<p>我们添加了AbpHangfireModule作为依赖，并使用Configuration.BackgroundJobs.UseHangfire方法启用和配置Hangfire（&ldquo;Default&rdquo;是web.config中的连接字符串）。</p>
<p>Hangfire在数据库中需要模式创建权限，因为它在第一次运行时创建自己的模式和表。</p>
<p>仪表板授权<br />Hagfire可以显示仪表板页面，以实时查看所有后台作业的状态。 您可以按照其说明文档中的说明进行配置。 默认情况下，此仪表板页面适用于所有用户，未经授权。 您可以使用Abp.HangFire包中定义的AbpHangfireAuthorizationFilter类将其集成到ABP的授权系统中。 示例配置：</p>
<div class="cnblogs_code">
<pre>app.UseHangfireDashboard(<span style="color: #800000;">"</span><span style="color: #800000;">/hangfire</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span><span style="color: #000000;"> DashboardOptions
{
    Authorization </span>= <span style="color: #0000ff;">new</span>[] { <span style="color: #0000ff;">new</span><span style="color: #000000;"> AbpHangfireAuthorizationFilter() }
});</span></pre>
</div>
<p>这将检查当前用户是否已登录到应用程序。 如果你想要一个额外的权限，你可以传入它的构造函数：</p>
<div class="cnblogs_code">
<pre>app.UseHangfireDashboard(<span style="color: #800000;">"</span><span style="color: #800000;">/hangfire</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span><span style="color: #000000;"> DashboardOptions
{
    Authorization </span>= <span style="color: #0000ff;">new</span>[] { <span style="color: #0000ff;">new</span> AbpHangfireAuthorizationFilter(<span style="color: #800000;">"</span><span style="color: #800000;">MyHangFireDashboardPermissionName</span><span style="color: #800000;">"</span><span style="color: #000000;">) }
});</span></pre>
</div>
<p>注意：UseHangfireDashboard应该在您的启动类中的认证中间件之后调用（可能是最后一行）。 否则，授权总是失败。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a36"></a>三十六、Quartz 集成</span></strong></span></p>
<p>Quartz是一个全功能的开源作业调度系统，可以从最小的应用程序到大型企业系统使用。 Abp.Quartz包简单地将Quartz集成到ASP.NET Boilerplate。</p>
<p>ASP.NET Boilerplate具有内置的持久性后台作业队列和后台工作系统。 如果您对后台工作人员有高级调度要求，Quartz可以是一个很好的选择。 此外，Hangfire可以成为持久后台作业队列的好选择。</p>
<p>1，安装</p>
<p>将Abp.Quartz nuget软件包安装到您的项目中，并将一个DependsOn属性添加到您的AbpQuartzModule模块中：</p>
<div class="cnblogs_code">
<pre>[DependsOn(<span style="color: #0000ff;">typeof</span><span style="color: #000000;"> (AbpQuartzModule))]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> YourModule : AbpModule
{
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
}</pre>
</div>
<p>要创建新作业，您可以实现Quartz的IJob界面，也可以从具有一些帮助属性/方法的JobBase类（在Abp.Quartz包中定义）派生（用于记录和本地化）。 一个简单的工作类如下所示：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyLogJob : JobBase, ITransientDependency
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Execute(IJobExecutionContext context)
    {
        Logger.Info(</span><span style="color: #800000;">"</span><span style="color: #800000;">Executed MyLogJob :)</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    }
}</span></pre>
</div>
<p>我们只是执行Execute方法来写一个日志。 您可以看到更多的Quartz的文档。</p>
<p>2，调度工作</p>
<p>IQuartzScheduleJobManager用于调度作业。 您可以将其注入到您的类（或者您可以在您的模块的PostInitialize方法中解析并使用它）来计划作业。 调度作业的示例控制器：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> HomeController : AbpController
{
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> IQuartzScheduleJobManager _jobManager;

    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> HomeController(IQuartzScheduleJobManager jobManager)
    {
        _jobManager </span>=<span style="color: #000000;"> jobManager;
    }
        
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task&lt;ActionResult&gt;<span style="color: #000000;"> ScheduleJob()
    {
        </span><span style="color: #0000ff;">await</span> _jobManager.ScheduleAsync&lt;MyLogJob&gt;<span style="color: #000000;">(
            job </span>=&gt;<span style="color: #000000;">
            {
                job.WithIdentity(</span><span style="color: #800000;">"</span><span style="color: #800000;">MyLogJobIdentity</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">MyGroup</span><span style="color: #800000;">"</span><span style="color: #000000;">)
                    .WithDescription(</span><span style="color: #800000;">"</span><span style="color: #800000;">A job to simply write logs.</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            },
            trigger </span>=&gt;<span style="color: #000000;">
            {
                trigger.StartNow()
                    .WithSimpleSchedule(schedule </span>=&gt;<span style="color: #000000;">
                    {
                        schedule.RepeatForever()
                            .WithIntervalInSeconds(</span><span style="color: #800080;">5</span><span style="color: #000000;">)
                            .Build();
                    });
            });

        </span><span style="color: #0000ff;">return</span> Content(<span style="color: #800000;">"</span><span style="color: #800000;">OK, scheduled!</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    }
}  </span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a37"></a>三十七、通知系统</span></strong></span></p>
<p>1，介绍</p>
<p>通知（Notification）用于告知用户系统中的特定事件。ABP提供了基于<strong>实时</strong>通知基础设施的发布订阅模型（pub/sub）。</p>
<p>①发送模型</p>
<p>给用户发送通知有两种方式：</p>
<ul>
<li>首先用户订阅特定的通知类型，然后我们发布这种类型的通知，这种类型的通知会传递给所有<strong>已经订阅</strong>的用户。这就是发布订阅（pub/sub）模型。</li>
<li>直接给目标用户发送通知。</li>
</ul>
<p>②通知类型</p>
<p>通知类型也有两种：</p>
<ul>
<li><strong>一般通知</strong>：是任意类型的通知。&ldquo;如果一个用户给我发送了添加好友的请求就通知我&rdquo;是这种通知类型的一个例子。</li>
<li><strong>实体通知</strong>：和特定的实体相关联。&ldquo;如果一个用户在&nbsp;<strong>这张</strong>图片上评论那么通知我&rdquo;是基于实体的通知，因为它和特定的实体相关联。用户可能想获得某些图片的通知而不是所有的图片通知。</li>
</ul>
<p>③通知数据&nbsp;</p>
<p>一个通知一般都会包括一个<strong>通知数据</strong>。比如，&ldquo;如果一个用户给我发送了添加好友的请求就通知我&rdquo;，这个通知可能有两个数据属性：发送者用户名（那哪一个用户发送的这个添加好友的请求）和请求内容（该用户在这个请求中写的东西）。很明显，该通知数据类型紧耦合于通知类型。不同的通知类型有不同的数据类型。</p>
<ul>
<li>通知数据是<strong>可选的</strong>。某些通知可能不需要数据。一些预定义的通知数据类型可能对于大多数情况够用了。&nbsp;<strong>MessageNotificationData</strong>可以用于简单的信息，&nbsp;<strong>LocalizableMessageNotificationData</strong>可以用于本地化的，带参数的通知信息。</li>
</ul>
<p>④通知安全</p>
<p>通知的安全性有5个级别，它们定义在NotificationSeverity枚举类中，分别是 Info,Success,Warn,Error和Fatal。默认值是Info。</p>
<p>2，订阅通知</p>
<p>INotificationSubscriptionManager提供API来订阅通知。 例子：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyService : ITransientDependency
{
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> INotificationSubscriptionManager _notificationSubscriptionManager;

    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> MyService(INotificationSubscriptionManager notificationSubscriptionManager)
    {
        _notificationSubscriptionManager </span>=<span style="color: #000000;"> notificationSubscriptionManager;
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">订阅一般通知（发送好友请求）</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task Subscribe_SentFrendshipRequest(<span style="color: #0000ff;">int</span>? tenantId, <span style="color: #0000ff;">long</span><span style="color: #000000;"> userId)
    {
        </span><span style="color: #0000ff;">await</span> _notificationSubscriptionManager.SubscribeAsync(<span style="color: #0000ff;">new</span> UserIdentifier(tenantId, userId), <span style="color: #800000;">"</span><span style="color: #800000;">SentFrendshipRequest</span><span style="color: #800000;">"</span><span style="color: #000000;">);    
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">订阅实体通知（评论图片）</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task Subscribe_CommentPhoto(<span style="color: #0000ff;">int</span>? tenantId, <span style="color: #0000ff;">long</span><span style="color: #000000;"> userId, Guid photoId)
    {
        </span><span style="color: #0000ff;">await</span> _notificationSubscriptionManager.SubscribeAsync(<span style="color: #0000ff;">new</span> UserIdentifier(tenantId, userId), <span style="color: #800000;">"</span><span style="color: #800000;">CommentPhoto</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span> EntityIdentifier(<span style="color: #0000ff;">typeof</span><span style="color: #000000;">(Photo), photoId));   
    }
}</span></pre>
</div>
<p>首先，我们注入了<strong>INotificationSubscriptionManager</strong>。第一个方法订阅了一个一般通知。当某人发送了一个添加好友的请求时，用户想得到通知。第二个方法订阅了一个和特定实体（Photo）相关的通知。如果任何人对这个特定的图片进行了评论，那么用户就会收到通知。</p>
<p>每一个通知应该有<strong>唯一的名字</strong>（比如例子中的SentFrendshipRequest和 CommentPhoto）。</p>
<p><strong>INotificationSubscriptionManager</strong>还有很多方法来管理通知，比如<strong>UnsubscribeAsync, IsSubscribedAsync, GetSubscriptionsAsync</strong>等方法。</p>
<p>3，发布通知</p>
<p>INotification Publisher用于发布通知。 例子：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyService : ITransientDependency
{
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> INotificationPublisher _notiticationPublisher;

    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> MyService(INotificationPublisher notiticationPublisher)
    {
        _notiticationPublisher </span>=<span style="color: #000000;"> notiticationPublisher;
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">给特定的用户发送一个一般通知</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task Publish_SentFrendshipRequest(<span style="color: #0000ff;">string</span> senderUserName, <span style="color: #0000ff;">string</span> friendshipMessage, <span style="color: #0000ff;">long</span><span style="color: #000000;"> targetUserId)
    {
        </span><span style="color: #0000ff;">await</span> _notiticationPublisher.PublishAsync(<span style="color: #800000;">"</span><span style="color: #800000;">SentFrendshipRequest</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span> SentFrendshipRequestNotificationData(senderUserName, friendshipMessage), userIds: <span style="color: #0000ff;">new</span><span style="color: #000000;">[] { targetUserId });
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">给特定的用户发送一个实体通知</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task Publish_CommentPhoto(<span style="color: #0000ff;">string</span> commenterUserName, <span style="color: #0000ff;">string</span> comment, Guid photoId, <span style="color: #0000ff;">long</span><span style="color: #000000;"> photoOwnerUserId)
    {
        </span><span style="color: #0000ff;">await</span> _notiticationPublisher.PublishAsync(<span style="color: #800000;">"</span><span style="color: #800000;">CommentPhoto</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span> CommentPhotoNotificationData(commenterUserName, comment), <span style="color: #0000ff;">new</span> EntityIdentifier(<span style="color: #0000ff;">typeof</span>(Photo), photoId), userIds: <span style="color: #0000ff;">new</span><span style="color: #000000;">[] { photoOwnerUserId });
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">给具特定严重级别程度的所有订阅用户发送一个一般通知</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task Publish_LowDisk(<span style="color: #0000ff;">int</span><span style="color: #000000;"> remainingDiskInMb)
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;">例如 "LowDiskWarningMessage"的英文内容 -&gt; "Attention! Only {remainingDiskInMb} MBs left on the disk!"</span>
        <span style="color: #0000ff;">var</span> data = <span style="color: #0000ff;">new</span> LocalizableMessageNotificationData(<span style="color: #0000ff;">new</span> LocalizableString(<span style="color: #800000;">"</span><span style="color: #800000;">LowDiskWarningMessage</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">MyLocalizationSourceName</span><span style="color: #800000;">"</span><span style="color: #000000;">));
        data[</span><span style="color: #800000;">"</span><span style="color: #800000;">remainingDiskInMb</span><span style="color: #800000;">"</span>] =<span style="color: #000000;"> remainingDiskInMb;

        </span><span style="color: #0000ff;">await</span> _notiticationPublisher.PublishAsync(<span style="color: #800000;">"</span><span style="color: #800000;">System.LowDisk</span><span style="color: #800000;">"</span><span style="color: #000000;">, data, severity: NotificationSeverity.Warn);    
    }
}</span></pre>
</div>
<p>在第一个例子中，我们向单个用户发布了一个通知。 SentFrendshipRequestNotificationData应该从NotificationData派生如下：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">[Serializable]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SentFrendshipRequestNotificationData : NotificationData
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> SenderUserName { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> FriendshipMessage { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span> SentFrendshipRequestNotificationData(<span style="color: #0000ff;">string</span> senderUserName, <span style="color: #0000ff;">string</span><span style="color: #000000;"> friendshipMessage)
    {
        SenderUserName </span>=<span style="color: #000000;"> senderUserName;
        FriendshipMessage </span>=<span style="color: #000000;"> friendshipMessage;
    }
}</span></pre>
</div>
<p>在第二个例子中，我们向特定的用户发送了一个特定实体的通知。通知数据类CommentPhotoNotificationData一般不需要<strong>serializble</strong>(因为默认使用了JSON序列化)。但是建议把它标记为serializable，因为你可能需要在应用之间移动通知，也可能在未来使用二进制的序列。此外，正如之前声明的那样，通知数据是可选的，而且对于所有的通知可能不是必须的。</p>
<p>注意：如果我们对特定的用户发布了一个通知，那么他们不需要订阅那些通知。</p>
<p>在第三个例子中，我们没有定义一个专用的通知数据类。相反，我们直接使用了内置的具有基于字典数据的<strong>LocalizableMessageNotificationData</strong>，并且以&nbsp;<strong>Warn</strong>发布了通知。<strong>LocalizableMessageNotificationData</strong>可以存储基于字典的任意数据（这对于自定义的通知数据类也是成立的，因为它们也从&nbsp;<strong>NotificationData类继承</strong>）。在本地化时我们使用了&ldquo;&nbsp;<strong>remaingDiskInMb</strong>&rdquo;作为参数。本地化信息可以包含这些参数（比如例子中的"Attention! Only {remainingDiskInMb} MBs left on the disk!"）</p>
<p>4，用户通知管理者</p>
<p><strong>IUserNotificationManager</strong>用于管理用户的通知，它有&nbsp;<strong>get,update或delete</strong>用户通知的方法。你可以为你的应用程序准备一个通知列表页面。</p>
<p>5，实时通知</p>
<p>虽然可以使用IUserNotificationManager来查询通知，但我们通常希望将实时通知推送到客户端。</p>
<p>通知系统使用IRealTimeNotifier向用户发送实时通知。 这可以用任何类型的实时通信系统来实现。 它使用SignalR在一个分开的包中实现。 启动模板已经安装了SignalR。 有关详细信息，请参阅SignalR集成文档。</p>
<p>注意：通知系统在后台作业中异步调用IRealTimeNotifier。 因此，可能会以较小的延迟发送通知。</p>
<p>①客户端</p>
<p>当收到实时通知时，ASP.NET Boilerplate会触发客户端的全局事件。 您可以注册以获取通知：</p>
<div class="cnblogs_code">
<pre>abp.<span style="color: #0000ff;">event</span>.on(<span style="color: #800000;">'</span><span style="color: #800000;">abp.notifications.received</span><span style="color: #800000;">'</span><span style="color: #000000;">, function (userNotification) {
    console.log(userNotification);
});</span></pre>
</div>
<p>每个收到的实时通知触发abp.notifications.received事件。 您可以注册到此事件，如上所示，以获得通知。 有关事件的更多信息，请参阅JavaScript事件总线文档。 &ldquo;System.LowDisk&rdquo;示例传入通知JSON示例：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">{
    </span>"userId": 2<span style="color: #000000;">,
    </span>"state": 0<span style="color: #000000;">,
    </span>"notification"<span style="color: #000000;">: {
        </span>"notificationName": "System.LowDisk"<span style="color: #000000;">,
        </span>"data"<span style="color: #000000;">: {
            </span>"message"<span style="color: #000000;">: {
                </span>"sourceName": "MyLocalizationSourceName"<span style="color: #000000;">,
                </span>"name": "LowDiskWarningMessage"<span style="color: #000000;">
            },
            </span>"type": "Abp.Notifications.LocalizableMessageNotificationData"<span style="color: #000000;">,
            </span>"properties"<span style="color: #000000;">: {
                </span>"remainingDiskInMb": "42"<span style="color: #000000;">
            }
        },
        </span>"entityType": <span style="color: #0000ff;">null</span><span style="color: #000000;">,
        </span>"entityTypeName": <span style="color: #0000ff;">null</span><span style="color: #000000;">,
        </span>"entityId": <span style="color: #0000ff;">null</span><span style="color: #000000;">,
        </span>"severity": 0<span style="color: #000000;">,
        </span>"creationTime": "2016-02-09T17:03:32.13"<span style="color: #000000;">,
        </span>"id": "0263d581-3d8a-476b-8e16-4f6a6f10a632"<span style="color: #000000;">
    },
    </span>"id": "4a546baf-bf17-4924-b993-32e420a8d468"<span style="color: #000000;">
}</span></pre>
</div>
<p>在这个对象中</p>
<ul>
<li><strong>userId</strong>:当前的用户Id。一般来说不需要这个，因为你知道当前的用户。</li>
<li><strong>state</strong>：&nbsp;<strong>UserNotificationState</strong>枚举的值。0：未读，1：已读。</li>
<li><strong>notification</strong>:通知细节。
<ul>
<li><strong>notificationName</strong>:通知的唯一名称。（当发布该通知时使用相同的值）</li>
<li><strong>data</strong>:通知数据。在本例中，我们使用了<strong>LocalizableMessageNotificationData&nbsp;</strong>（正如之前的例子中发布的）。</li>
<li><strong>message</strong>:本地的信息通知。我们可以使用&nbsp;<strong>sourceName</strong>和&nbsp;<strong>name</strong>来本地化UI上的信息。</li>
<li><strong>type</strong>:通知数据类型。全类型名称，包括命名空间。当处理该通知数据时我们可以检查该类型。</li>
<li><strong>properties</strong>：基于字典的自定义属性。</li>
<li><strong>entityType, entityTypeName和entityId</strong>：和通知相关的实体的信息。</li>
<li><strong>severity</strong>：&nbsp;<strong>NotificationSeverity</strong>枚举的值。0: Info, 1: Success, 2: Warn, 3: Error, 4: Fatal。</li>
<li><strong>creationTime</strong>:该通知创建的时间。</li>
<li><strong>id</strong>:通知的Id。</li>
</ul>
</li>
<li><strong>id</strong>:用户的通知id。</li>
</ul>
<p>当然，你不会只记录通知。 您可以使用通知数据向用户显示通知信息。 例：</p>
<div class="cnblogs_code">
<pre>abp.event.on('abp.notifications.received', <span style="color: #0000ff;">function</span><span style="color: #000000;"> (userNotification) {
    </span><span style="color: #0000ff;">if</span> (userNotification.notification.data.type === 'Abp.Notifications.LocalizableMessageNotificationData'<span style="color: #000000;">) {
        </span><span style="color: #0000ff;">var</span> localizedText =<span style="color: #000000;"> abp.localization.localize(
            userNotification.notification.data.message.name,
            userNotification.notification.data.message.sourceName
        );

        $.each(userNotification.notification.data.properties, </span><span style="color: #0000ff;">function</span><span style="color: #000000;"> (key, value) {
            localizedText </span>= localizedText.replace('{' + key + '}'<span style="color: #000000;">, value);
        });

        alert(</span>'New localized notification: ' +<span style="color: #000000;"> localizedText);
    } </span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span> (userNotification.notification.data.type === 'Abp.Notifications.MessageNotificationData'<span style="color: #000000;">) {
        alert(</span>'New simple notification: ' +<span style="color: #000000;"> userNotification.notification.data.message);
    }
});</span></pre>
</div>
<p>它适用于内置的通知数据类型（LocalizableMessageNotificationData和MessageNotificationData）。 如果您有自定义通知数据类型，那么您应该注册这样的数据格式化程序：</p>
<div class="cnblogs_code">
<pre>abp.notifications.messageFormatters['MyProject.MyNotificationDataType'] = <span style="color: #0000ff;">function</span><span style="color: #000000;">(userNotification) {
    </span><span style="color: #0000ff;">return</span> ...; <span style="color: #008000;">//</span><span style="color: #008000;">格式和返回信息</span>
};</pre>
</div>
<p>6，通知存储</p>
<p>通知系统使用了<strong>INotificationStore</strong>来持久化通知。为了使通知系统合适地工作，应该实现这个接口。你可以自己实现或者使用module-zero（它已经实现了该接口）。7，</p>
<p>7，通知定义</p>
<p>在使用之前你不必定义一个通知。你无需定义任何类型的<strong>通知名</strong>就可以使用它们。但是，定义通知名可能会给你带来额外的好处。比如，你以后要研究应用程序中所有的通知，在这种情况下，我们可以给我们的模块定义一个<strong>通知提供器</strong>（notification provider ），如下所示：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">public class MyAppNotificationProvider : NotificationProvider
{
    public override </span><span style="color: #0000ff;">void</span><span style="color: #000000;"> SetNotifications(INotificationDefinitionContext context)
    {
        context.Manager.Add(
            </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> NotificationDefinition(
                </span>"App.NewUserRegistered"<span style="color: #000000;">,
                displayName: </span><span style="color: #0000ff;">new</span> LocalizableString("NewUserRegisteredNotificationDefinition", "MyLocalizationSourceName"<span style="color: #000000;">),
                permissionDependency: </span><span style="color: #0000ff;">new</span> SimplePermissionDependency("App.Pages.UserManagement"<span style="color: #000000;">)
                )
            );
    }
}</span></pre>
</div>
<p><strong>"App.NewUserRegistered"</strong>是该通知的唯一名称。我们定义了一个本地的&nbsp;<strong>displayName</strong>（然后当在UI上订阅了该通知时，我们可以显示该通知）。最后，我们声明了只有拥有了<strong>"App.Pages.UserManagement"</strong>权限的用户才可以使用该通知。</p>
<p>也有一些其他的参数，你可以在代码中研究。对于一个通知定义，只有通知名称是<strong>必须</strong>的。</p>
<p>当定义了这么一个通知提供器之后，我们应该在模块的PreInitialize事件中进行注册，如下所示：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> AbpZeroTemplateCoreModule : AbpModule
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> PreInitialize()
    {
        Configuration.Notifications.Providers.Add</span>&lt;MyAppNotificationProvider&gt;<span style="color: #000000;">();
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
}</pre>
</div>
<p>最后，要获得通知定义，在应用程序中注入并使用<strong>INotificationDefinitionManager</strong>。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a38"></a>三十八、SignalR集成</span></strong></span></p>
<p>Abp.Web.SignalR nuget软件包可以方便地在基于ASP.NET Boilerplate的应用程序中使用SignalR</p>
<p>1，安装</p>
<p>①服务器端</p>
<p>将Abp.Web.SignalR nuget包安装到您的项目（通常到您的Web层），并向您的模块添加依赖关系：</p>
<div class="cnblogs_code">
<pre>[DependsOn(<span style="color: #0000ff;">typeof</span><span style="color: #000000;">(AbpWebSignalRModule))]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> YourProjectWebModule : AbpModule
{
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
}</pre>
</div>
<p>然后按照惯例，在OWIN启动类中使用MapSignalR方法：</p>
<div class="cnblogs_code">
<pre>[assembly: OwinStartup(<span style="color: #0000ff;">typeof</span><span style="color: #000000;">(Startup))]
</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> MyProject.Web
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Startup
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configuration(IAppBuilder app)
        {
            app.MapSignalR();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">        }
    }
}</span></pre>
</div>
<p>注意：Abp.Web.SignalR只依赖于Microsoft.AspNet.SignalR.Core包。 因此，如果以前没有安装，您还需要将Microsoft.AspNet.SignalR包安装到您的Web项目中（有关更多信息，请参阅SignalR文档）。</p>
<p>②客户端</p>
<p>应该将abp.signalr.js脚本包含在页面中。 它位于Abp.Web.Resources包（它已经安装在启动模板中）</p>
<div class="cnblogs_code">
<pre>&lt;script src="~/signalr/hubs"&gt;&lt;/script&gt;
&lt;script src="~/Abp/Framework/scripts/libs/abp.signalr.js"&gt;&lt;/script&gt;</pre>
</div>
<p>就这样。 SignalR已正确配置并集成到您的项目中。</p>
<p>2，建立连接</p>
<p>当您的页面中包含abp.signalr.js时，ASP.NET Boilerplate会自动连接到服务器（从客户端）。 这通常很好。 但可能有些情况你不想要它。 您可以在包括abp.signalr.js之前添加这些行以禁用自动连接：</p>
<div class="cnblogs_code">
<pre>&lt;script&gt;<span style="color: #000000;">
    abp.signalr </span>= abp.signalr ||<span style="color: #000000;"> {};
    abp.signalr.autoConnect </span>= <span style="color: #0000ff;">false</span><span style="color: #000000;">;
</span>&lt;/script&gt;</pre>
</div>
<p>在这种情况下，您可以在需要连接到服务器时手动调用abp.signalr.connect（）函数。</p>
<p>如果abp.signalr.autoConnect为true，ASP.NET Boilerplate也会自动重新连接到客户端（从客户端）。</p>
<p>当客户端连接到服务器时，会触发&ldquo;abp.signalr.connected&rdquo;全局事件。 您可以注册到此事件，以便在连接成功建立时采取行动。 有关客户端事件的更多信息，请参阅JavaScript事件总线文档。</p>
<p>3，内置功能</p>
<p>您可以在应用程序中使用SignalR的所有功能。 另外，Abp.Web.SignalR包实现了一些内置的功能。</p>
<p>①通知（Notification）</p>
<p>Abp.Web.SignalR包实现IRealTimeNotifier向客户端发送实时通知（见通知系统）。 因此，用户可以获得实时推送通知。</p>
<p>②在线客户端</p>
<p>ASP.NET Boilerplate提供IOnlineClientManager来获取有关在线用户的信息（注入IOnlineClientManager并使用GetByUserIdOrNull，GetAllClients，IsOnline方法）。 IOnlineClientManager需要通信基础设施才能正常工作。 Abp.Web.SignalR包提供了基础架构。 因此，如果安装了SignalR，您可以在应用程序的任何层中注入和使用IOnlineClientManager。</p>
<p>③PascalCase与camelCase<br />Abp.Web.SignalR包覆盖SignalR的默认ContractResolver，以便在序列化时使用CamelCasePropertyNamesContractResolver。 因此，我们可以让类在服务器上具有PascalCase属性，并将它们作为camelCase在客户端上发送/接收对象（因为camelCase是javascript中的首选符号）。 如果您想在某些程序集中忽略此类，那么可以将这些程序集添加到AbpSignalRContractResolver.IgnoredAssemblies列表中。</p>
<p>4，您的SignalR代码</p>
<p>Abp.Web.SignalR包也简化了SignalR代码。 假设我们要添加一个Hub到我们的应用程序：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyChatHub : Hub, ITransientDependency
{
    </span><span style="color: #0000ff;">public</span> IAbpSession AbpSession { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span> ILogger Logger { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> MyChatHub()
    {
        AbpSession </span>=<span style="color: #000000;"> NullAbpSession.Instance;
        Logger </span>=<span style="color: #000000;"> NullLogger.Instance;
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> SendMessage(<span style="color: #0000ff;">string</span><span style="color: #000000;"> message)
    {
        Clients.All.getMessage(</span><span style="color: #0000ff;">string</span>.Format(<span style="color: #800000;">"</span><span style="color: #800000;">User {0}: {1}</span><span style="color: #800000;">"</span><span style="color: #000000;">, AbpSession.UserId, message));
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> <span style="color: #0000ff;">override</span><span style="color: #000000;"> Task OnConnected()
    {
        </span><span style="color: #0000ff;">await</span> <span style="color: #0000ff;">base</span><span style="color: #000000;">.OnConnected();
        Logger.Debug(</span><span style="color: #800000;">"</span><span style="color: #800000;">A client connected to MyChatHub: </span><span style="color: #800000;">"</span> +<span style="color: #000000;"> Context.ConnectionId);
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> <span style="color: #0000ff;">override</span> Task OnDisconnected(<span style="color: #0000ff;">bool</span><span style="color: #000000;"> stopCalled)
    {
        </span><span style="color: #0000ff;">await</span> <span style="color: #0000ff;">base</span><span style="color: #000000;">.OnDisconnected(stopCalled);
        Logger.Debug(</span><span style="color: #800000;">"</span><span style="color: #800000;">A client disconnected from MyChatHub: </span><span style="color: #800000;">"</span> +<span style="color: #000000;"> Context.ConnectionId);
    }
}</span></pre>
</div>
<p>我们实现了ITransientDependency接口，简单地将我们的集线器注册到依赖注入系统（您可以根据需要进行单例化）。 我们注入session和logger。</p>
<p>SendMessage是我们的集线器的一种方法，可以被客户端使用。 我们在这个方法中调用所有客户端的getMessage函数。 我们可以使用AbpSession来获取当前用户ID（如果用户登录）。 我们还覆盖了OnConnected和OnDisconnected，这只是为了演示，实际上并不需要。</p>
<p>这里，客户端的JavaScript代码使用我们的集线器发送/接收消息。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> chatHub =<span style="color: #000000;"> $.connection.myChatHub; 

chatHub.client.getMessage </span>= function (message) { <span style="color: #008000;">//</span><span style="color: #008000;">注册传入消息</span>
    console.log(<span style="color: #800000;">'</span><span style="color: #800000;">received message: </span><span style="color: #800000;">'</span> +<span style="color: #000000;"> message);
};

abp.</span><span style="color: #0000ff;">event</span>.on(<span style="color: #800000;">'</span><span style="color: #800000;">abp.signalr.connected</span><span style="color: #800000;">'</span>, function() { <span style="color: #008000;">//注册连接事件</span>
    chatHub.server.sendMessage(<span style="color: #800000;">"</span><span style="color: #800000;">Hi everybody, I'm connected to the chat!</span><span style="color: #800000;">"</span>); <span style="color: #008000;">//</span><span style="color: #008000;">向服务器发送消息</span>
});</pre>
</div>
<p>然后我们可以随时使用chatHub发送消息到服务器。 有关SignalR的详细信息，请参阅SignalR文档。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a39"></a>三十九、EntityFramework集成</span></strong></span></p>
<p>1，Nuget包</p>
<p>Abp.EntityFramework</p>
<p>2，DbContext</p>
<p>如您所知，要使用EntityFramework，您应该为应用程序定义一个DbContext类。 示例DbContext如下所示：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SimpleTaskSystemDbContext : AbpDbContext
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">virtual</span> IDbSet&lt;Person&gt; People { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">virtual</span> IDbSet&lt;Task&gt; Tasks { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> SimpleTaskSystemDbContext()
        : </span><span style="color: #0000ff;">base</span>(<span style="color: #800000;">"</span><span style="color: #800000;">Default</span><span style="color: #800000;">"</span><span style="color: #000000;">)
    {

    }
    
    </span><span style="color: #0000ff;">public</span> SimpleTaskSystemDbContext(<span style="color: #0000ff;">string</span><span style="color: #000000;"> nameOrConnectionString)
        : </span><span style="color: #0000ff;">base</span><span style="color: #000000;">(nameOrConnectionString)
    {

    }

    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> SimpleTaskSystemDbContext(DbConnection existingConnection)
        : </span><span style="color: #0000ff;">base</span>(existingConnection, <span style="color: #0000ff;">false</span><span style="color: #000000;">)
    {

    }

    </span><span style="color: #0000ff;">public</span> SimpleTaskSystemDbContext(DbConnection existingConnection, <span style="color: #0000ff;">bool</span><span style="color: #000000;"> contextOwnsConnection)
        : </span><span style="color: #0000ff;">base</span><span style="color: #000000;">(existingConnection, contextOwnsConnection)
    {

    }

    </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> OnModelCreating(DbModelBuilder modelBuilder)
    {
        </span><span style="color: #0000ff;">base</span><span style="color: #000000;">.OnModelCreating(modelBuilder);

        modelBuilder.Entity</span>&lt;Person&gt;().ToTable(<span style="color: #800000;">"</span><span style="color: #800000;">StsPeople</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        modelBuilder.Entity</span>&lt;Task&gt;().ToTable(<span style="color: #800000;">"</span><span style="color: #800000;">StsTasks</span><span style="color: #800000;">"</span>).HasOptional(t =&gt;<span style="color: #000000;"> t.AssignedPerson);
    }
}</span></pre>
</div>
<p>除了以下规则，它是一个常规的DbContext类：</p>
<p>①它来自AbpDbContext而不是DbContext。&nbsp;</p>
<p>②它应该有上面的示例的构造函数（构造函数参数名也应该相同）。 说明：</p>
<p>　　默认构造器将&ldquo;Default&rdquo;传递给基类作为连接字符串。&nbsp;因此，它希望在web.config / app.config文件中使用一个名为&ldquo;Default&rdquo;的连接字符串。 这个构造函数不被ABP使用，而是由EF命令行迁移工具命令（如update-database）使用。</p>
<p>　　构造函数获取nameOrConnectionString由ABP用于在运行时传递连接名称或字符串。</p>
<p>　　构造函数获取existingConnection可以用于单元测试，而不是ABP直接使用。</p>
<p>　　构造函数获取existingConnection，并且在使用DbContextEfTransactionStrategy时，ABP在单个数据库多个dbcontext场景中使用contextOwnsConnection来共享相同的connection和transaction()（参见下面的事务管理部分）。</p>
<p>3，仓储</p>
<p>仓储库用于从较高层抽象数据访问</p>
<p>①默认仓储库</p>
<p>Abp.EntityFramework为您在DbContext中定义的所有实体实现默认存储库。 您不必创建存储库类以使用预定义的存储库方法。 例：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> PersonAppService : IPersonAppService
{
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span> IRepository&lt;Person&gt;<span style="color: #000000;"> _personRepository;

    </span><span style="color: #0000ff;">public</span> PersonAppService(IRepository&lt;Person&gt;<span style="color: #000000;"> personRepository)
    {
        _personRepository </span>=<span style="color: #000000;"> personRepository;
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> CreatePerson(CreatePersonInput input)
    {        
        person </span>= <span style="color: #0000ff;">new</span> Person { Name = input.Name, EmailAddress =<span style="color: #000000;"> input.EmailAddress };

        _personRepository.Insert(person);
    }
}</span></pre>
</div>
<p>②应用程序特定基础仓储库类</p>
<p>ASP.NET Boilerplate提供了一个基类EfRepositoryBase来轻松实现存储库。 要实现IRepository接口，您只需从该类派生您的存储库。 但是最好创建自己的扩展EfRepositoryBase的基类。 因此，您可以将共享/常用方法添加到存储库中，或轻松覆盖现有方法。 一个示例基类全部用于SimpleTaskSystem应用程序的存储库：</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">我的应用程序中所有存储库的基类</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> SimpleTaskSystemRepositoryBase&lt;TEntity, TPrimaryKey&gt; : EfRepositoryBase&lt;SimpleTaskSystemDbContext, TEntity, TPrimaryKey&gt;
    <span style="color: #0000ff;">where</span> TEntity : <span style="color: #0000ff;">class</span>, IEntity&lt;TPrimaryKey&gt;<span style="color: #000000;">
{
    </span><span style="color: #0000ff;">public</span> SimpleTaskSystemRepositoryBase(IDbContextProvider&lt;SimpleTaskSystemDbContext&gt;<span style="color: #000000;"> dbContextProvider)
        : </span><span style="color: #0000ff;">base</span><span style="color: #000000;">(dbContextProvider)
    {
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">为所有存储库添加常用方法</span>
<span style="color: #000000;">}

</span><span style="color: #008000;">//</span><span style="color: #008000;">具有整数ID的实体的快捷方式</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> SimpleTaskSystemRepositoryBase&lt;TEntity&gt; : SimpleTaskSystemRepositoryBase&lt;TEntity, <span style="color: #0000ff;">int</span>&gt;
    <span style="color: #0000ff;">where</span> TEntity : <span style="color: #0000ff;">class</span>, IEntity&lt;<span style="color: #0000ff;">int</span>&gt;<span style="color: #000000;">
{
    </span><span style="color: #0000ff;">public</span> SimpleTaskSystemRepositoryBase(IDbContextProvider&lt;SimpleTaskSystemDbContext&gt;<span style="color: #000000;"> dbContextProvider)
        : </span><span style="color: #0000ff;">base</span><span style="color: #000000;">(dbContextProvider)
    {
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">不要在这里添加任何方法，添加到上面的类（因为这个类继承它）</span>
}</pre>
</div>
<p>请注意，我们继承自EfRepositoryBase &lt;SimpleTaskSystemDbContext，TEntity，TPrimaryKey&gt;。 这声明ASP.NET Boilerplate在我们的存储库中使用SimpleTaskSystemDbContext。</p>
<p>默认情况下，您使用EfRepositoryBase实现给定DbContext（此示例中为SimpleTaskSystemDbContext）的所有存储库。 您可以将AutoRepositoryTypes属性添加到DbContext中，将其替换为您自己的存储库库存储库类，如下所示：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">[AutoRepositoryTypes(
    </span><span style="color: #0000ff;">typeof</span>(IRepository&lt;&gt;<span style="color: #000000;">),
    </span><span style="color: #0000ff;">typeof</span>(IRepository&lt;,&gt;<span style="color: #000000;">),
    </span><span style="color: #0000ff;">typeof</span>(SimpleTaskSystemEfRepositoryBase&lt;&gt;<span style="color: #000000;">),
    </span><span style="color: #0000ff;">typeof</span>(SimpleTaskSystemEfRepositoryBase&lt;,&gt;<span style="color: #000000;">)
)]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SimpleTaskSystemDbContext : AbpDbContext
{
    ...
}</span></pre>
</div>
<p>③自定义存储库示例</p>
<p>要实现自定义存储库，只需从上面创建的应用程序特定的基础存储库类派生。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span> ITaskRepository : IRepository&lt;Task, <span style="color: #0000ff;">long</span>&gt;<span style="color: #000000;">
{
    List</span>&lt;Task&gt; GetAllWithPeople(<span style="color: #0000ff;">int</span>? assignedPersonId, TaskState?<span style="color: #000000;"> state);
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> TaskRepository : SimpleTaskSystemRepositoryBase&lt;Task, <span style="color: #0000ff;">long</span>&gt;<span style="color: #000000;">, ITaskRepository
{
    </span><span style="color: #0000ff;">public</span> TaskRepository(IDbContextProvider&lt;SimpleTaskSystemDbContext&gt;<span style="color: #000000;"> dbContextProvider)
        : </span><span style="color: #0000ff;">base</span><span style="color: #000000;">(dbContextProvider)
    {
    }

    </span><span style="color: #0000ff;">public</span> List&lt;Task&gt; GetAllWithPeople(<span style="color: #0000ff;">int</span>? assignedPersonId, TaskState?<span style="color: #000000;"> state)
    {
        </span><span style="color: #0000ff;">var</span> query =<span style="color: #000000;"> GetAll();

        </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (assignedPersonId.HasValue)
        {
            query </span>= query.Where(task =&gt; task.AssignedPerson.Id ==<span style="color: #000000;"> assignedPersonId.Value);
        }

        </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (state.HasValue)
        {
            query </span>= query.Where(task =&gt; task.State ==<span style="color: #000000;"> state);
        }

        </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> query
            .OrderByDescending(task </span>=&gt;<span style="color: #000000;"> task.CreationTime)
            .Include(task </span>=&gt;<span style="color: #000000;"> task.AssignedPerson)
            .ToList();
    }
}</span></pre>
</div>
<p>我们首先定义了ITaskRepository，然后实现它。 GetAll()返回IQueryable &lt;Task&gt;，然后我们可以使用给定的参数添加一些Where过滤器。 最后我们可以调用ToList()来获取任务列表。</p>
<p>您还可以使用存储库方法中的Context对象来访问DbContext并直接使用Entity Framework API。</p>
<p>④仓储库最佳实现</p>
<p>尽可能使用默认存储库</p>
<p>始终为您的应用程序创建自定义存储库的存储库基类，如上所述。</p>
<p>仓储接口在领域层定义，仓储实现在EntityFramework层</p>
<p>⑤事务管理</p>
<p>ASP.NET Boilerplate具有内置的工作系统单元来管理数据库连接和事务。 实体框架有不同的事务管理方法。 ASP.NET Boilerplate默认使用环境TransactionScope方法，但也具有DbContext事务API的内置实现。 如果要切换到DbContext事务API，可以在模块的PreInitialize方法中进行配置：</p>
<div class="cnblogs_code">
<pre>Configuration.ReplaceService&lt;IEfTransactionStrategy, DbContextEfTransactionStrategy&gt;(DependencyLifeStyle.Transient);</pre>
</div>
<p>记得添加&ldquo;using Abp.Configuration.Startup;&rdquo; 到你的代码文件可以使用ReplaceService泛型扩展方法。</p>
<p>此外，您的DbContext应具有本文档DbContext部分中所述的构造函数。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a40"></a>四十、NHibernate集成</span></strong></span></p>
<p>1，Nuget包</p>
<p>安装Abp.NHibernate</p>
<p>2，配置</p>
<p>要开始使用NHibernate，您应该在模块的PreInitialize中进行配置。</p>
<div class="cnblogs_code">
<pre>[DependsOn(<span style="color: #0000ff;">typeof</span><span style="color: #000000;">(AbpNHibernateModule))]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SimpleTaskSystemDataModule : AbpModule
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> PreInitialize()
    {
        </span><span style="color: #0000ff;">var</span> connStr = ConfigurationManager.ConnectionStrings[<span style="color: #800000;">"</span><span style="color: #800000;">Default</span><span style="color: #800000;">"</span><span style="color: #000000;">].ConnectionString;

        Configuration.Modules.AbpNHibernate().FluentConfiguration
            .Database(MsSqlConfiguration.MsSql2008.ConnectionString(connStr))
            .Mappings(m </span>=&gt;<span style="color: #000000;"> m.FluentMappings.AddFromAssembly(Assembly.GetExecutingAssembly()));
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Initialize()
    {
        IocManager.RegisterAssemblyByConvention(Assembly.GetExecutingAssembly());
    }
}</span></pre>
</div>
<p>3，映射实体</p>
<p>在上面的示例配置中，我们使用当前程序集中的所有映射类进行流畅映射。 示例映射类可以如下所示：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> TaskMap : EntityMap&lt;Task&gt;<span style="color: #000000;">
{
    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> TaskMap()
        : </span><span style="color: #0000ff;">base</span>(<span style="color: #800000;">"</span><span style="color: #800000;">TeTasks</span><span style="color: #800000;">"</span><span style="color: #000000;">)
    {
        References(x </span>=&gt; x.AssignedUser).Column(<span style="color: #800000;">"</span><span style="color: #800000;">AssignedUserId</span><span style="color: #800000;">"</span><span style="color: #000000;">).LazyLoad();

        Map(x </span>=&gt;<span style="color: #000000;"> x.Title).Not.Nullable();
        Map(x </span>=&gt;<span style="color: #000000;"> x.Description).Nullable();
        Map(x </span>=&gt; x.Priority).CustomType&lt;TaskPriority&gt;<span style="color: #000000;">().Not.Nullable();
        Map(x </span>=&gt; x.Privacy).CustomType&lt;TaskPrivacy&gt;<span style="color: #000000;">().Not.Nullable();
        Map(x </span>=&gt; x.State).CustomType&lt;TaskState&gt;<span style="color: #000000;">().Not.Nullable();
    }
}</span></pre>
</div>
<p>EntityMap是一个ASP.NET Boilerplate类，它扩展了ClassMap &lt;T&gt;，自动映射Id属性并在构造函数中获取表名。 所以，我从它导出，并使用FluentNHibernate映射其他属性。 当然，您可以直接从ClassMap中导出，您可以使用FluentNHibernate的完整API，您可以使用NHibernate的其他映射技术（如映射XML文件）。</p>
<p>4，仓储</p>
<p>①默认实现</p>
<p>Abp.NHibernate包实现了应用程序中实体的默认存储库。 您不必为实体创建存储库类，只需使用预定义的存储库方法。 例：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> PersonAppService : IPersonAppService
{
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span> IRepository&lt;Person&gt;<span style="color: #000000;"> _personRepository;

    </span><span style="color: #0000ff;">public</span> PersonAppService(IRepository&lt;Person&gt;<span style="color: #000000;"> personRepository)
    {
        _personRepository </span>=<span style="color: #000000;"> personRepository;
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> CreatePerson(CreatePersonInput input)
    {        
        person </span>= <span style="color: #0000ff;">new</span> Person { Name = input.Name, EmailAddress =<span style="color: #000000;"> input.EmailAddress };

        _personRepository.Insert(person);
    }
}</span></pre>
</div>
<p>②自定义仓储</p>
<p>如果要添加一些自定义方法，应首先将其添加到存储库接口（作为最佳实践），然后在存储库类中实现。 ASP.NET Boilerplate提供了一个基类NhRepositoryBase来轻松实现存储库。 要实现IRepository接口，您只需从该类派生您的存储库。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span> ITaskRepository : IRepository&lt;Task, <span style="color: #0000ff;">long</span>&gt;<span style="color: #000000;">
{
    List</span>&lt;Task&gt; GetAllWithPeople(<span style="color: #0000ff;">int</span>? assignedPersonId, TaskState?<span style="color: #000000;"> state);
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> TaskRepository : NhRepositoryBase&lt;Task, <span style="color: #0000ff;">long</span>&gt;<span style="color: #000000;">, ITaskRepository
{
    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> TaskRepository(ISessionProvider sessionProvider)
        : </span><span style="color: #0000ff;">base</span><span style="color: #000000;">(sessionProvider)
    {
    }

    </span><span style="color: #0000ff;">public</span> List&lt;Task&gt; GetAllWithPeople(<span style="color: #0000ff;">int</span>? assignedPersonId, TaskState?<span style="color: #000000;"> state)
    {
        </span><span style="color: #0000ff;">var</span> query =<span style="color: #000000;"> GetAll();

        </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (assignedPersonId.HasValue)
        {
            query </span>= query.Where(task =&gt; task.AssignedPerson.Id ==<span style="color: #000000;"> assignedPersonId.Value);
        }

        </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (state.HasValue)
        {
            query </span>= query.Where(task =&gt; task.State ==<span style="color: #000000;"> state);
        }

        </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> query
            .OrderByDescending(task </span>=&gt;<span style="color: #000000;"> task.CreationTime)
            .Fetch(task </span>=&gt;<span style="color: #000000;"> task.AssignedPerson)
            .ToList();
    }
}</span></pre>
</div>
<p>GetAll()返回IQueryable &lt;Task&gt;，然后我们可以使用给定的参数添加一些Where过滤器。 最后我们可以调用ToList()来获取任务列表。</p>
<p>您还可以使用存储库方法中的Session对象来使用NHibernate的完整API。</p>
<p>③应用程序特定的基本存储库类</p>
<p>虽然您可以从ASP.NET Boilerplate的NhRepositoryBase派生您的存储库，但更好的做法是创建自己的扩展NhRepositoryBase的基类。 因此，您可以轻松地将共享/常用方法添加到您的存储库。 例：</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">我的应用程序中所有存储库的基类</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">class</span> MyRepositoryBase&lt;TEntity, TPrimaryKey&gt; : NhRepositoryBase&lt;TEntity, TPrimaryKey&gt;
    <span style="color: #0000ff;">where</span> TEntity : <span style="color: #0000ff;">class</span>, IEntity&lt;TPrimaryKey&gt;<span style="color: #000000;">
{
    </span><span style="color: #0000ff;">protected</span><span style="color: #000000;"> MyRepositoryBase(ISessionProvider sessionProvider)
        : </span><span style="color: #0000ff;">base</span><span style="color: #000000;">(sessionProvider)
    {
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">为所有存储库添加常用方法</span>
<span style="color: #000000;">}

</span><span style="color: #008000;">//</span><span style="color: #008000;">具有整数ID的实体的快捷方式</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">class</span> MyRepositoryBase&lt;TEntity&gt; : MyRepositoryBase&lt;TEntity, <span style="color: #0000ff;">int</span>&gt;
    <span style="color: #0000ff;">where</span> TEntity : <span style="color: #0000ff;">class</span>, IEntity&lt;<span style="color: #0000ff;">int</span>&gt;<span style="color: #000000;">
{
    </span><span style="color: #0000ff;">protected</span><span style="color: #000000;"> MyRepositoryBase(ISessionProvider sessionProvider)
        : </span><span style="color: #0000ff;">base</span><span style="color: #000000;">(sessionProvider)
    {
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">不要在这里添加任何方法，添加上面的类（因为它继承它）</span>
<span style="color: #000000;">}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> TaskRepository : MyRepositoryBase&lt;Task&gt;<span style="color: #000000;">, ITaskRepository
{
    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> TaskRepository(ISessionProvider sessionProvider)
        : </span><span style="color: #0000ff;">base</span><span style="color: #000000;">(sessionProvider)
    {
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">任务存储库的具体方法</span>
}</pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a41"></a>四十一、Dapper使用</span></strong></span></p>
<p>1，安装</p>
<p>nuget Abp.Dapper</p>
<p>2，模块注册</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">[DependsOn(
     </span><span style="color: #0000ff;">typeof</span><span style="color: #000000;">(AbpEntityFrameworkCoreModule),
     </span><span style="color: #0000ff;">typeof</span><span style="color: #000000;">(AbpDapperModule)
)]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyModule : AbpModule
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Initialize()
    {
        IocManager.RegisterAssemblyByConvention(</span><span style="color: #0000ff;">typeof</span><span style="color: #000000;">(SampleApplicationModule).GetAssembly());
    }
}</span></pre>
</div>
<p>请注意，AbpDapperModule依赖关系应该晚于EF Core依赖项。</p>
<p>3，实体到表映射</p>
<p>您可以配置映射。 例如，Person类映射到以下示例中的Persons表：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> PersonMapper : ClassMapper&lt;Person&gt;<span style="color: #000000;">
{
    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> PersonMapper()
    {
        Table(</span><span style="color: #800000;">"</span><span style="color: #800000;">Persons</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        Map(x </span>=&gt;<span style="color: #000000;"> x.Roles).Ignore();
        AutoMap();
    }
}</span></pre>
</div>
<p>您应该设置包含映射器类的程序集。 例：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">[DependsOn(
     </span><span style="color: #0000ff;">typeof</span><span style="color: #000000;">(AbpEntityFrameworkModule),
     </span><span style="color: #0000ff;">typeof</span><span style="color: #000000;">(AbpDapperModule)
)]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyModule : AbpModule
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Initialize()
    {
        IocManager.RegisterAssemblyByConvention(</span><span style="color: #0000ff;">typeof</span><span style="color: #000000;">(SampleApplicationModule).GetAssembly());
        DapperExtensions.SetMappingAssemblies(</span><span style="color: #0000ff;">new</span> List&lt;Assembly&gt; { <span style="color: #0000ff;">typeof</span><span style="color: #000000;">(MyModule).GetAssembly() });
    }
}</span></pre>
</div>
<p>4，用法</p>
<p>注册AbpDapperModule后，您可以使用Generic IDapperRepository接口（而不是标准IRepository）来注入dapper存储库。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SomeApplicationService : ITransientDependency
{
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span> IDapperRepository&lt;Person&gt;<span style="color: #000000;"> _personDapperRepository;
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span> IRepository&lt;Person&gt;<span style="color: #000000;"> _personRepository;

    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> SomeApplicationService(
        IRepository</span>&lt;Person&gt;<span style="color: #000000;"> personRepository,
        IDapperRepository</span>&lt;Person&gt;<span style="color: #000000;"> personDapperRepository)
    {
        _personRepository </span>=<span style="color: #000000;"> personRepository;
        _personDapperRepository </span>=<span style="color: #000000;"> personDapperRepository;
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> DoSomeStuff()
    {
        </span><span style="color: #0000ff;">var</span> people = _personDapperRepository.Query(<span style="color: #800000;">"</span><span style="color: #800000;">select * from Persons</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    }
}</span></pre>
</div>
<p>&nbsp;</p>