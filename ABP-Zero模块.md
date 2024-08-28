<p><a href="#a1"><strong>一、介绍</strong></a></p>
<p><a href="#a2"><strong><strong>二、启动模版</strong></strong></a></p>
<p><strong><strong>三、功能</strong></strong></p>
<p>　　<a href="#a3"><strong><strong>1，租户管理</strong></strong></a></p>
<p>　　<a href="#a4"><strong>2，版本管理</strong></a></p>
<p>　　<a href="#a5"><strong>3，用户管理</strong></a></p>
<p>　　<a href="#a6"><strong><strong>4，角色管理</strong></strong></a></p>
<p>　　<a href="#a7"><strong><strong><strong><strong>5，组织单位管理</strong></strong></strong></strong></a></p>
<p>　　<a href="#a8"><strong><strong><strong>6，权限管理</strong></strong></strong></a></p>
<p>　　<a href="#a9"><strong><strong><strong><strong>7，语言管理</strong></strong></strong></strong></a></p>
<p>　　<a href="#a10"><strong>8，Identity Server集成</strong></a></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a1"></a>一、介绍</span></strong></span></p>
<p>1，Zero模块实现ASP.NET&nbsp;Boilerplate框架的所有基本概念。如：</p>
<p><span style="font-size: 12px;">租户管理（多租户）、</span><span style="font-size: 12px;">角色管理、</span><span style="font-size: 12px;">用户管理、</span><span style="font-size: 12px;">session、</span><span style="font-size: 12px;">授权（权限管理）、</span><span style="font-size: 12px;">设置管理、</span><span style="font-size: 12px;">语言管理、</span><span style="font-size: 12px;">审计管理</span></p>
<p>2，Microsoft ASP.NET Identity模块有2个版本：</p>
<ul>
<li>Abp.Zero.*&nbsp;软件包基于Microsoft ASP.NET身份和EF6.x.</li>
<li>Abp.ZeroCore.*&nbsp;软件包基于Microsoft ASP.NET Core身份和Entity Framework Core。 这些软件包也支持.net内核。</li>
</ul>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a2"></a>二、启动模版</span></strong></span></p>
<p><span style="font-size: 12px; color: #ff0000;">注意：确保您已经为您的Visual Studio安装了Typescript 2.0+，因为Abp.Web.Resources nuget包附带d.ts，它需要Typescript 2.0+。</span></p>
<p>1，基于令牌的认证</p>
<p>启动模板使用基于cookie的浏览器身份验证。 但是，如果要从移动应用程序中使用Web API或应用程序服务（通过动态Web api公开），则可能需要基于令牌的身份验证机制。 启动模板包括承载令牌认证基础设施。 .WebApi项目中的AccountController包含用于获取令牌的Authenticate操作。 然后我们可以使用令牌进行下一个请求。</p>
<p>①认证</p>
<p>只需发送POST请求到<strong>http://localhost:6334/api/Account/Authenticate</strong>和&nbsp;<strong>Context-Type="application/json"</strong>头，如下所示：</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201710/741594-20171022211923162-1774348559.png" alt="" /></p>
<p>我们发送了一个JSON请求体，其中包含userNameOrEmailAddress和密码。 另外，应该为租户用户发送TenancyName。 如上所述，返回JSON的result属性包含令牌。 我们可以保存并用于下一个请求。</p>
<p>②使用API</p>
<p>在认证和获取令牌之后，我们可以使用它来调用任何授权的操作。 所有应用程序服务都可以远程使用。 例如，我们可以使用租户服务来获取租户列表：&nbsp;</p>
<p>&nbsp;<img src="http://images2017.cnblogs.com/blog/741594/201710/741594-20171022212137006-318553653.png" alt="" /></p>
<p>只需向<strong>http://localhost:6334/api/services/app/tenant/GetTenants</strong>发送POST请求到&nbsp;<strong>Content-Type="application/json"</strong>和<strong>Authorization="Bearer&nbsp;<em>your-</em></strong><em><strong>auth-token</strong>&nbsp;</em><strong>"</strong>。 请求正文只是空的{}。 当然，请求和响应机构对于不同的API将是不同的。</p>
<p>UI上几乎所有可用的操作也可用作Web API（由于UI使用相同的Web API），并且可以轻松地使用。</p>
<p>2，Migrator&nbsp;控制台应用程序</p>
<p>启动模板包含一个工具Migrator.exe，可轻松迁移数据库。 您可以运行此应用程序来创建/迁移主机和租户数据库。</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201710/741594-20171022212425662-304584238.png" alt="" /></p>
<p>此应用程序从它自己的.config文件获取主机连接字符串。 在开头的web.config中将是一样的。 确保配置文件中的连接字符串是您想要的数据库。 获取主机连接后，首先创建主机数据库或应用迁移（如果它已经存在）。 然后，它获取租户数据库的连接字符串，并为这些数据库运行迁移。 如果没有一个专用数据库，或者它的数据库已经迁移到另一个租户（用于多个租户之间的共享数据库），它会跳过租户。</p>
<p>您可以在开发或产品环境中使用此工具来迁移部署时的数据库，而不是EntityFramework自己的Migrate.exe（这需要一些配置，并且可以在一次运行中为单个数据库工作）。</p>
<p>3，单元测试<br />启动模板包括测试基础架构设置和.Test项目下的一些测试。 您可以检查它们并轻松编写类似的测试。 实际上，它们是集成测试而不是单元测试，因为它们使用所有ASP.NET Boilerplate基础架构（包括验证，授权，工作单元...）测试代码。</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a3"></a>三、租户管理</span></strong></p>
<p>1，启用多租户<br />ASP.NET Boilerplate和Zero模块可以运行多租户或单租户模式。 默认情况下禁用多租户。 我们可以在我们的模块的PreInitialize方法中启用它，如下所示：</p>
<div class="cnblogs_code">
<pre>[DependsOn(<span style="color: #0000ff;">typeof</span><span style="color: #000000;">(AbpZeroCoreModule))]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyCoreModule : AbpModule
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> PreInitialize()
    {
        Configuration.MultiTenancy.IsEnabled </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">;    
    }

    ...
}</span></pre>
</div>
<p>当我们创建一个基于ASP.NET Boilerplate和Zero模块的项目模板时，我们有一个Tenant实体和TenantManager领域服务。</p>
<p>2，租户实体</p>
<p>租户实体代表申请的租户。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> Tenant : AbpTenant&lt;Tenant, User&gt;<span style="color: #000000;">
{

}</span></pre>
</div>
<p>它源于通用的AbpTenant类。 租户实体存储在数据库中的AbpTenants表中。 您可以将自定义属性添加到Tenant类。</p>
<p>AbpTenant类定义了一些基本属性，大多数重要的是：</p>
<ul>
<li><strong>TenancyName</strong>:租户名称，唯一。不能正常改变 它可以用来为&ldquo;mytenant.mydomain.com&rdquo;这样的租户分配子域名。 Tenant.TenancyNameRegex常量定义命名规则。</li>
<li><strong>Name</strong>: 任意可读的名称</li>
<li><strong>IsActive</strong>:true:这个租户可以使用该应用程序;false:该租户的用户不能登录到系统</li>
</ul>
<p>AbpTenant类继承自FullAuditedEntity。 这意味着它具有创建，修改和删除审计属性。 它也是软删除。 所以，当我们删除租户时，它不会从数据库中删除，只是被标记为已删除。</p>
<p>最后，AbpTenant的Id被定义为int。</p>
<p>3，租户管理</p>
<p>租户管理是为租户执行领域逻辑的服务</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> TenantManager : AbpTenantManager&lt;Tenant, Role, User&gt;<span style="color: #000000;">
{
    </span><span style="color: #0000ff;">public</span> TenantManager(IRepository&lt;Tenant&gt;<span style="color: #000000;"> tenantRepository)
        : </span><span style="color: #0000ff;">base</span><span style="color: #000000;">(tenantRepository)
    {

    }
}</span></pre>
</div>
<p>TenantManager也用于管理租户功能。 你可以在这里添加你自己的方法。 此外，您可以根据自己的需要覆盖任何AbpTenantManager基类的方法。</p>
<p>4，默认租户<br />ASP.NET Boilerplate和Zero模块假设有一个预定义的租户，<strong>TenancyName</strong>为&ldquo;Default&rdquo;，Id为1.在单租户应用程序中，与租户一样使用。 在多租户应用程序中，您可以将其删除或将其设为被动。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a4"></a>四、版本管理</span></strong></span></p>
<p>大多数SaaS（多租户）应用程序都有具有不同功能的版本（包）。 因此，他们可以向租户（客户）提供不同的价格和功能选项。</p>
<p>1，版本实体（Edition Entity）</p>
<p>版本是一个简单的实体代表应用程序的一个版本（或包）。 它只有Name和DisplayName属性。</p>
<p>2，版本管理</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> EditionManager : AbpEditionManager
{
}</span></pre>
</div>
<p>它来自AbpEditionManager类。 您可以注入并使用EditionManager来创建，删除和更新版本。 此外，EditionManager用于管理版本的功能。 它内部缓存版本功能以获得更好的性能。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a5"></a>五、用户管理</span></strong></span></p>
<p>1，用户实体</p>
<p>用户实体表示应用程序的用户。 它应该从AbpUser类派生，如下所示：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> User : AbpUser&lt;Tenant, User&gt;<span style="color: #000000;">
{
    </span><span style="color: #008000;">//</span><span style="color: #008000;">在这里添加您自己的用户属性</span>
}</pre>
</div>
<p>此类在您安装模块零时创建。 用户存储在数据库中的AbpUsers表中。 您可以将自定义属性添加到User类（并为更改创建数据库迁移）。</p>
<p>AbpUser类定义了一些基本属性。 一些属性是：</p>
<ul>
<li><strong>UserName</strong>:&nbsp;用户的登录名对于租户应该是唯一的。</li>
<li><strong>EmailAddress</strong>:&nbsp;用户的电子邮件地址。 对于租户来说应该是独一无二的。</li>
<li><strong>Password</strong>:&nbsp;用户的密码。</li>
<li><strong>IsActive</strong>:true:用户可以登录到系统</li>
<li><strong>Name（用户姓名）</strong>&nbsp;和&nbsp;<strong>Surname（姓氏）</strong></li>
</ul>
<p>还有一些属性，如角色（Roles）、权限（Permissions）、租户（Tenant）、设置（Settings）、IsEmailConfirmed（邮箱是否确认）、</p>
<p>AbpUser类继承自FullAuditedEntity。 这意味着它具有创建，修改和删除审计属性。 它也是软删除。 所以，当我们删除一个用户时，它不会从数据库中删除，只是被标记为已删除。</p>
<p>AbpUser类实现了IMayHaveTenant过滤器，以便在多租户应用程序中正常工作。</p>
<p>最后，用户的ID被定义为long。</p>
<p>2，用户管理</p>
<p>UserManager是为用户执行领域逻辑的服务：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> UserManager : AbpUserManager&lt;Tenant, Role, User&gt;<span style="color: #000000;">
{
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
}</pre>
</div>
<p>您可以注入并使用UserManager来创建，删除，更新用户，授予权限，为用户更改角色等等。 你可以在这里添加你自己的方法。 此外，您可以根据自己的需要覆盖任何AbpUserManager基类的方法。</p>
<p>①多租户</p>
<p>UserManager旨在一次为单个租户工作。 它适用于当前租户的默认值。 让我们看看UserManager的一些用法：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyTestAppService : ApplicationService
{
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> UserManager _userManager;

    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> MyTestAppService(UserManager userManager)
    {
        _userManager </span>=<span style="color: #000000;"> userManager;
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> TestMethod_1()
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;">通过电子邮件寻找当前租户的用户</span>
        <span style="color: #0000ff;">var</span> user = _userManager.FindByEmail(<span style="color: #800000;">"</span><span style="color: #800000;">sampleuser@aspnetboilerplate.com</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> TestMethod_2()
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;">切换到租户42</span>
        CurrentUnitOfWork.SetFilterParameter(AbpDataFilters.MayHaveTenant, AbpDataFilters.Parameters.TenantId, <span style="color: #800080;">42</span><span style="color: #000000;">);

        </span><span style="color: #008000;">//</span><span style="color: #008000;">通过电子邮件找到租户42的一个用户</span>
        <span style="color: #0000ff;">var</span> user = _userManager.FindByEmail(<span style="color: #800000;">"</span><span style="color: #800000;">sampleuser@aspnetboilerplate.com</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> TestMethod_3()
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;">禁用MayHaveTenant过滤器，所以我们可以覆盖所有用户</span>
        <span style="color: #0000ff;">using</span><span style="color: #000000;"> (CurrentUnitOfWork.DisableFilter(AbpDataFilters.MayHaveTenant))
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">现在，我们可以在所有租户中搜索用户名</span>
            <span style="color: #0000ff;">var</span> users = _userManager.Users.Where(u =&gt; u.UserName == <span style="color: #800000;">"</span><span style="color: #800000;">sampleuser</span><span style="color: #800000;">"</span><span style="color: #000000;">).ToList();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">或者我们可以添加TenantId过滤器，如果我们要搜索一个特定的租户</span>
            <span style="color: #0000ff;">var</span> user = _userManager.Users.FirstOrDefault(u =&gt; u.TenantId == <span style="color: #800080;">42</span> &amp;&amp; u.UserName == <span style="color: #800000;">"</span><span style="color: #800000;">sampleuser</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }
    }
}</span></pre>
</div>
<p>②用户登录</p>
<p>Zero模块定义了LoginManager，它具有用于登录应用程序的LoginAsync方法。 它检查所有用于登录的逻辑，并返回登录结果。 LoginAsync方法还会自动将所有登录尝试保存到数据库（即使是尝试失败）。 您可以使用UserLoginAttempt实体进行查询。</p>
<p>③关于IdentityResults</p>
<p>UserManager的一些方法返回IdentityResult，而不是在某些情况下抛出异常。 这是ASP.NET Identity Framework的本质。 Zero模块也随之而来。 所以，我们应该检查这个返回的结果对象来知道操作是否成功。</p>
<p>Zero模块定义了CheckErrors扩展方法，如果需要，可自动检查错误并抛出异常（本地化的UserFriendlyException）。 使用示例</p>
<div class="cnblogs_code">
<pre>(<span style="color: #0000ff;">await</span> UserManager.CreateAsync(user)).CheckErrors();</pre>
</div>
<p>要获得本地化的例外，我们应该提供一个ILocalizationManager实例：</p>
<div class="cnblogs_code">
<pre>(<span style="color: #0000ff;">await</span> UserManager.CreateAsync(user)).CheckErrors(LocalizationManager);</pre>
</div>
<p>3，外部认证</p>
<p>Zero模块登录方式从数据库中的AbpUsers表中认证用户。 一些应用程序可能需要从一些外部来源（如活动目录，从另一个数据库的表甚至远程服务）来验证用户。</p>
<p>对于这种情况，UserManager定义了一个名为&ldquo;外部认证来源&rdquo;的扩展点。 我们可以创建一个派生自IExternalAuthenticationSource的类并注册到配置。 有一个DefaultExternalAuthenticationSource类来简化IExternalAuthenticationSource的实现。 我们来看一个例子：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> MyExternalAuthSource : DefaultExternalAuthenticationSource&lt;Tenant, User&gt;<span style="color: #000000;">
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">string</span><span style="color: #000000;"> Name
    {
        </span><span style="color: #0000ff;">get</span> { <span style="color: #0000ff;">return</span> <span style="color: #800000;">"</span><span style="color: #800000;">MyCustomSource</span><span style="color: #800000;">"</span><span style="color: #000000;">; }
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> Task&lt;<span style="color: #0000ff;">bool</span>&gt; TryAuthenticateAsync(<span style="color: #0000ff;">string</span> userNameOrEmailAddress, <span style="color: #0000ff;">string</span><span style="color: #000000;"> plainPassword, Tenant tenant)
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;">TODO：验证用户并返回true或false</span>
<span style="color: #000000;">    }
}</span></pre>
</div>
<p>在TryAuthenticateAsync方法中，我们可以从某些来源检查用户名和密码，如果给定用户由此源进行身份验证，则返回true。 此外，我们可以覆盖CreateUser和UpdateUser方法来控制用户创建和更新此源。</p>
<p>当用户通过外部源进行身份验证时，Zero模块检查该用户是否存在于数据库（AbpUsers表）中。 如果没有，它调用CreateUser来创建用户，否则调用UpdateUser来允许身份验证源来更新现有的用户信息。</p>
<p>我们可以在应用程序中定义多个外部认证源。 AbpUser实体具有AuthenticationSource属性，该属性显示哪个源验证了该用户。</p>
<p>要注册我们的认证来源，我们可以在我们的模块的PreInitialize中使用这样的代码：</p>
<div class="cnblogs_code">
<pre>Configuration.Modules.Zero().UserManagement.ExternalAuthenticationSources.Add&lt;MyExternalAuthSource&gt;();</pre>
</div>
<p>①LDAP/Active Directory</p>
<p>LdapAuthenticationSource是外部身份验证的一种实现，使用户可以使用其LDAP（活动目录）用户名和密码登录。</p>
<p>如果我们要使用LDAP认证，我们首先将Abp.Zero.Ldap nuget包添加到我们的项目（通常为Core（domain）项目）。 那么我们应该为我们的应用程序扩展LdapAuthenticationSource，如下所示：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> MyLdapAuthenticationSource : LdapAuthenticationSource&lt;Tenant, User&gt;<span style="color: #000000;">
{
    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> MyLdapAuthenticationSource(ILdapSettings settings, IAbpZeroLdapModuleConfig ldapModuleConfig)
        : </span><span style="color: #0000ff;">base</span><span style="color: #000000;">(settings, ldapModuleConfig)
    {
    }
}</span></pre>
</div>
<p>最后，我们应该将模块依赖关系设置为AbpZeroLdapModule，并使用上面创建的auth源启用LDAP：</p>
<div class="cnblogs_code">
<pre>[DependsOn(<span style="color: #0000ff;">typeof</span><span style="color: #000000;">(AbpZeroLdapModule))]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyApplicationCoreModule : AbpModule
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> PreInitialize()
    {
        Configuration.Modules.ZeroLdap().Enable(</span><span style="color: #0000ff;">typeof</span><span style="color: #000000;"> (MyLdapAuthenticationSource));    
    }

    ...
}</span></pre>
</div>
<p>在这些步骤之后，将为您的应用程序启用LDAP模块。 但默认情况下，LDAP认证未启用。 我们可以使用设置启用它。</p>
<p>1)设置</p>
<p>LdapSettingNames类定义了设置名称的常量。 您可以在更改设置（或获取设置）时使用这些常量名称。 LDAP设置是每个租户（对于多租户应用程序）。 因此，不同的租户具有不同的设置（请参阅在github上设置定义）。</p>
<p>您可以在MyLdapAuthenticationSource构造函数中看到，LdapAuthenticationSource期望ILdapSettings作为构造函数参数。 此界面用于获取LDAP设置，如域，用户名和密码以连接到Active Directory。 默认实现（LdapSettings类）从设置管理器获取这些设置。</p>
<p>如果您使用设置管理器，那么没有问题。 您可以使用设置管理器API更改LDAP设置。 如果需要，您可以将初始/种子数据添加到数据库，默认情况下启用LDAP验证。</p>
<p>注意：如果您不定义域，用户名和密码，LDAP认证适用于当前域，如果应用程序在具有适当权限的域中运行。</p>
<p>2)自定义设置</p>
<p>如果要定义另一个设置源，可以实现自定义ILdapSettings类，如下所示：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyLdapSettings : ILdapSettings
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task&lt;<span style="color: #0000ff;">bool</span>&gt; GetIsEnabled(<span style="color: #0000ff;">int</span>?<span style="color: #000000;"> tenantId)
    {
        </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">true</span><span style="color: #000000;">;
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task&lt;ContextType&gt; GetContextType(<span style="color: #0000ff;">int</span>?<span style="color: #000000;"> tenantId)
    {
        </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> ContextType.Domain;
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task&lt;<span style="color: #0000ff;">string</span>&gt; GetContainer(<span style="color: #0000ff;">int</span>?<span style="color: #000000;"> tenantId)
    {
        </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">null</span><span style="color: #000000;">;
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task&lt;<span style="color: #0000ff;">string</span>&gt; GetDomain(<span style="color: #0000ff;">int</span>?<span style="color: #000000;"> tenantId)
    {
        </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">null</span><span style="color: #000000;">;
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task&lt;<span style="color: #0000ff;">string</span>&gt; GetUserName(<span style="color: #0000ff;">int</span>?<span style="color: #000000;"> tenantId)
    {
        </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">null</span><span style="color: #000000;">;
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task&lt;<span style="color: #0000ff;">string</span>&gt; GetPassword(<span style="color: #0000ff;">int</span>?<span style="color: #000000;"> tenantId)
    {
        </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">null</span><span style="color: #000000;">;
    }
}</span></pre>
</div>
<p>并在您的模块的PreInitialize中注册到IOC：</p>
<div class="cnblogs_code">
<pre>[DependsOn(<span style="color: #0000ff;">typeof</span><span style="color: #000000;">(AbpZeroLdapModule))]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyApplicationCoreModule : AbpModule
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> PreInitialize()
    {
        IocManager.Register</span>&lt;ILdapSettings, MyLdapSettings&gt;(); <span style="color: #008000;">//</span><span style="color: #008000;">更改默认设置源</span>
        Configuration.Modules.ZeroLdap().Enable(<span style="color: #0000ff;">typeof</span><span style="color: #000000;"> (MyLdapAuthenticationSource));
    }

    ...
}</span></pre>
</div>
<p>然后，您可以从任何其他来源获取LDAP设置。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a6"></a>六、角色管理</span></strong></span></p>
<p>1，角色实体(Role Entity)</p>
<p>角色实体代表应用程序的角色。 它应该从AbpRole类派生，如下所示：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> Role : AbpRole&lt;Tenant, User&gt;<span style="color: #000000;">
{
    </span><span style="color: #008000;">//</span><span style="color: #008000;">在这里添加你自己的角色属性</span>
}</pre>
</div>
<p>此类在您安装Zero模块时创建。 角色存储在数据库中的AbpRoles表中。 您可以将自定义属性添加到Role类（并为更改创建数据库迁移）。</p>
<p>AbpRole定义了一些属性：</p>
<ul>
<li><strong>Name</strong>:&nbsp;租户角色的独特名称。</li>
<li><strong>DisplayName</strong>:&nbsp;显示名称的角色。</li>
<li><strong>IsDefault</strong>:这个角色是否默认分配给新用户？</li>
<li><strong>IsStatic</strong>:&nbsp;这个角色是静态的（预构建，不能被删除）。</li>
</ul>
<p>角色用于分组权限。 当用户有角色时，他/她将具有该角色的所有权限。 用户可以有多个角色。 该用户的权限将是所有分配角色的所有权限的合并。</p>
<p>2，动态vs静态角色</p>
<p>在模块零中，角色可以是动态的或静态的：</p>
<ul>
<li><strong>Static role</strong>:&nbsp;静态角色有一个已知的名称（如&ldquo;admin&rdquo;），不能更改此名称（我们可以更改显示名称）。 它存在于系统启动，无法删除。 因此，我们可以根据静态角色名称编写代码。</li>
<li><strong>Dynamic (non static) role</strong>:&nbsp;我们可以在部署后创建动态角色。 然后我们可以授予该角色的权限，我们可以将角色分配给某些用户，我们可以将其删除。 在开发时期，我们无法知道动态角色的名称。</li>
</ul>
<p>使用IsStatic属性为角色设置它。 此外，我们应该在我们的模块的PreInitialize上注册静态角色。 假设我们对租户有一个&ldquo;Admin&rdquo;静态角色：</p>
<div class="cnblogs_code">
<pre>Configuration.Modules.Zero().RoleManagement.StaticRoles.Add(<span style="color: #0000ff;">new</span> StaticRoleDefinition(<span style="color: #800000;">"</span><span style="color: #800000;">Admin</span><span style="color: #800000;">"</span>, MultiTenancySides.Tenant));</pre>
</div>
<p>因此，Zero模块将意识到静态角色。</p>
<p>3，默认角色</p>
<p>一个或多个角色可以设置为默认。 默认角色默认分配给新添加/注册的用户。 这不是开发时间属性，可以在部署后设置或更改。 使用IsDefault属性进行设置。</p>
<p>4，角色管理</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> RoleManager : AbpRoleManager&lt;Tenant, Role, User&gt;<span style="color: #000000;">
{
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
}</pre>
</div>
<p>您可以注入并使用RoleManager来创建，删除，更新角色，授予角色权限等等。 你可以在这里添加你自己的方法。 此外，您可以根据自己的需要覆盖任何AbpRoleManager基类的方法。</p>
<p>像UserManager一样，RoleManager的一些方法也返回IdentityResult，而不是在某些情况下抛出异常。 有关详细信息，请参阅用户管理文档</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a7"></a>七、组织单位管理</span></strong></p>
<p>组织单位（OU）可用于对用户和实体进行分层分组。</p>
<p>1，OrganizationUnit实体</p>
<p>OU由OrganizationUnit实体表示。 这个实体的基本属性是：</p>
<ul>
<li><strong>TenantId</strong>: 租户的这个OU的ID。 主机OU可以为空.</li>
<li><strong>ParentId</strong>: 父OU的ID。 如果这是根OU，则可以为null.</li>
<li><strong>Code</strong>:租户独有的层次化字符串代码.</li>
<li><strong>DisplayName</strong>: 显示OU的名称.</li>
</ul>
<p>OrganizationUnit entitiy的主键(id)为long类型，它源自FullAuditedEntity，它提供审计信息并实现ISoftDelete界面（因此，OU不会从数据库中删除，它们只被标记为已删除）</p>
<p>2，组织树<br />由于OU可以拥有父级，所以租户的所有OU都是树形结构。 这棵树有一些规则：</p>
<ul>
<li>可以有多个根（它们具有null ParentId）。</li>
<li>最大深度树被定义为一个常量作为OrganizationUnit.MaxDepth，它是16.</li>
<li>存在用于第一级子计数的OU的（因为固定OU代码单位长度在下面解释）的限制.</li>







</ul>
<p>2，OU Code</p>
<p>OU代码由OrganizationUnit Manager自动生成和维护。 这是一个字符串，如：</p>
<p>"<strong>00001.00042.00005</strong>"</p>
<p>该代码可用于轻松查询OU的所有子项（递归）的数据库。 这段代码有一些规则：</p>
<ul>
<li>这对租户来说是独一无二的.</li>
<li>同一个OU的所有子代都有父OU的代码开头的代码.</li>
<li>它是基于树中OU的级别的固定长度，如示例所示.</li>
<li>当OU代码是唯一的，如果您移动OU，它可以是可更改的。 因此，我们应该通过Id引用OU，而不是Code.</li>







</ul>
<p>3，OrganizationUnit 管理</p>
<p>可以注入OrganizationUnitManager类并用于管理OU。 常见用例有：</p>
<ul>
<li>创建，更新或删除OU</li>
<li>在OU树中移动OU.</li>
<li>获取关于OU树和项目的信息.</li>







</ul>
<p>4，多租户</p>
<p>OrganizationUnitManager旨在一次为单个租户工作。 它适用于当前租户的默认值。</p>
<p>5，常用案例</p>
<p>在这里，我们将看到OU的常见用例。 您可以在<a href="https://github.com/aspnetboilerplate/aspnetboilerplate-samples/tree/master/OrganizationUnitsDemo" target="_blank">这里</a>找到样品的源代码。</p>
<p>6，为组织单位创建实体,<br />OU的最明显的使用是将实体分配给OU。 我们来看一个示例实体：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Product : Entity, IMustHaveTenant, IMustHaveOrganizationUnit
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">virtual</span> <span style="color: #0000ff;">int</span> TenantId { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">virtual</span> <span style="color: #0000ff;">long</span> OrganizationUnitId { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">virtual</span> <span style="color: #0000ff;">string</span> Name { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">virtual</span> <span style="color: #0000ff;">float</span> Price { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}</span></pre>
</div>
<p>我们简单地创建了OrganizationUnitId属性来将此实体分配给OU。 IMustHaveOrganizationUnit定义了OrganizationUnitId属性。 我们不必执行它，但建议提供标准化。 还有一个具有可空的OrganizationUnitId属性的IMayHaveOrganizationId。</p>
<p>现在，我们可以将产品与OU相关联并查询特定OU的产品。</p>
<p>注意; 产品实体有一个TenantId（它是IMustHaveTenant的属性），用于区分多租户应用中不同租户的产品（见多租户文档）。 如果您的应用程序不是多租户，则不需要此接口和属性。</p>
<p>7，获取组织单位中的实体</p>
<p>获取OU的产品很简单。 我们来看看这个示例域服务：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ProductManager : IDomainService
{
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span> IRepository&lt;Product&gt;<span style="color: #000000;"> _productRepository;

    </span><span style="color: #0000ff;">public</span> ProductManager(IRepository&lt;Product&gt;<span style="color: #000000;"> productRepository)
    {
        _productRepository </span>=<span style="color: #000000;"> productRepository;
    }

    </span><span style="color: #0000ff;">public</span> List&lt;Product&gt; GetProductsInOu(<span style="color: #0000ff;">long</span><span style="color: #000000;"> organizationUnitId)
    {
        </span><span style="color: #0000ff;">return</span> _productRepository.GetAllList(p =&gt; p.OrganizationUnitId ==<span style="color: #000000;"> organizationUnitId);
    }
                
}</span></pre>
</div>
<p>我们可以简单地写一个反对Product.OrganizationUnitId的谓词，如上所示。</p>
<p>8，在组织单位中获得实体，包括其子单位单位<br />我们可能想要获得包含子组织单位的组织单位的产品。 在这种情况下，OU代码可以帮助我们：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ProductManager : IDomainService
{
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span> IRepository&lt;Product&gt;<span style="color: #000000;"> _productRepository;
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span> IRepository&lt;OrganizationUnit, <span style="color: #0000ff;">long</span>&gt;<span style="color: #000000;"> _organizationUnitRepository;

    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> ProductManager(
        IRepository</span>&lt;Product&gt;<span style="color: #000000;"> productRepository, 
        IRepository</span>&lt;OrganizationUnit, <span style="color: #0000ff;">long</span>&gt;<span style="color: #000000;"> organizationUnitRepository)
    {
        _productRepository </span>=<span style="color: #000000;"> productRepository;
        _organizationUnitRepository </span>=<span style="color: #000000;"> organizationUnitRepository;
    }

    [UnitOfWork]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">virtual</span> List&lt;Product&gt; GetProductsInOuIncludingChildren(<span style="color: #0000ff;">long</span><span style="color: #000000;"> organizationUnitId)
    {
        </span><span style="color: #0000ff;">var</span> code =<span style="color: #000000;"> _organizationUnitRepository.Get(organizationUnitId).Code;

        </span><span style="color: #0000ff;">var</span> query =
            <span style="color: #0000ff;">from</span> product <span style="color: #0000ff;">in</span><span style="color: #000000;"> _productRepository.GetAll()
            join organizationUnit </span><span style="color: #0000ff;">in</span><span style="color: #000000;"> _organizationUnitRepository.GetAll() on product.OrganizationUnitId equals organizationUnit.Id
            </span><span style="color: #0000ff;">where</span><span style="color: #000000;"> organizationUnit.Code.StartsWith(code)
            </span><span style="color: #0000ff;">select</span><span style="color: #000000;"> product;

        </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> query.ToList();
    }
}</span></pre>
</div>
<p>首先，我们得到了给定OU的代码。 然后我们创建了一个带有连接和StartsWith（代码）条件的LINQ（StartsWith在SQL中创建一个LIKE查询）。 因此，我们可以分级地获得OU的产品。</p>
<p>9，过滤用户的实体<br />我们可能希望获得特定用户的OU中的所有产品。 示例代码：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ProductManager : IDomainService
{
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span> IRepository&lt;Product&gt;<span style="color: #000000;"> _productRepository;
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> UserManager _userManager;

    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> ProductManager(
        IRepository</span>&lt;Product&gt;<span style="color: #000000;"> productRepository, 
        UserManager userManager)
    {
        _productRepository </span>=<span style="color: #000000;"> productRepository;
        _organizationUnitRepository </span>=<span style="color: #000000;"> organizationUnitRepository;
        _userManager </span>=<span style="color: #000000;"> userManager;
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task&lt;List&lt;Product&gt;&gt; GetProductsForUserAsync(<span style="color: #0000ff;">long</span><span style="color: #000000;"> userId)
    {
        </span><span style="color: #0000ff;">var</span> user = <span style="color: #0000ff;">await</span><span style="color: #000000;"> _userManager.GetUserByIdAsync(userId);
        </span><span style="color: #0000ff;">var</span> organizationUnits = <span style="color: #0000ff;">await</span><span style="color: #000000;"> _userManager.GetOrganizationUnitsAsync(user);
        </span><span style="color: #0000ff;">var</span> organizationUnitIds = organizationUnits.Select(ou =&gt;<span style="color: #000000;"> ou.Id);

        </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">await</span> _productRepository.GetAllListAsync(p =&gt;<span style="color: #000000;"> organizationUnitIds.Contains(p.OrganizationUnitId));
    }
}</span></pre>
</div>
<p>我们简单地发现了用户的OU的Ids。 然后在获得产品时使用包含条件。 当然，我们可以使用join创建一个LINQ查询来获取相同的列表。</p>
<p>我们可能想要在用户的OU中获得产品，包括其子OU：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ProductManager : IDomainService
{
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span> IRepository&lt;Product&gt;<span style="color: #000000;"> _productRepository;
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span> IRepository&lt;OrganizationUnit, <span style="color: #0000ff;">long</span>&gt;<span style="color: #000000;"> _organizationUnitRepository;
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> UserManager _userManager;

    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> ProductManager(
        IRepository</span>&lt;Product&gt;<span style="color: #000000;"> productRepository, 
        IRepository</span>&lt;OrganizationUnit, <span style="color: #0000ff;">long</span>&gt;<span style="color: #000000;"> organizationUnitRepository, 
        UserManager userManager)
    {
        _productRepository </span>=<span style="color: #000000;"> productRepository;
        _organizationUnitRepository </span>=<span style="color: #000000;"> organizationUnitRepository;
        _userManager </span>=<span style="color: #000000;"> userManager;
    }

    [UnitOfWork]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">virtual</span> <span style="color: #0000ff;">async</span> Task&lt;List&lt;Product&gt;&gt; GetProductsForUserIncludingChildOusAsync(<span style="color: #0000ff;">long</span><span style="color: #000000;"> userId)
    {
        </span><span style="color: #0000ff;">var</span> user = <span style="color: #0000ff;">await</span><span style="color: #000000;"> _userManager.GetUserByIdAsync(userId);
        </span><span style="color: #0000ff;">var</span> organizationUnits = <span style="color: #0000ff;">await</span><span style="color: #000000;"> _userManager.GetOrganizationUnitsAsync(user);
        </span><span style="color: #0000ff;">var</span> organizationUnitCodes = organizationUnits.Select(ou =&gt;<span style="color: #000000;"> ou.Code);

        </span><span style="color: #0000ff;">var</span> query =
            <span style="color: #0000ff;">from</span> product <span style="color: #0000ff;">in</span><span style="color: #000000;"> _productRepository.GetAll()
            join organizationUnit </span><span style="color: #0000ff;">in</span><span style="color: #000000;"> _organizationUnitRepository.GetAll() on product.OrganizationUnitId equals organizationUnit.Id
            </span><span style="color: #0000ff;">where</span> organizationUnitCodes.Any(code =&gt;<span style="color: #000000;"> organizationUnit.Code.StartsWith(code))
            </span><span style="color: #0000ff;">select</span><span style="color: #000000;"> product;

        </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> query.ToList();
    }
}</span></pre>
</div>
<p>我们将Any与StartsWith条件组合在LINQ连接语句中。</p>
<p>当然可能需要更复杂的要求，但是所有这些都可以用LINQ或SQL来完成。</p>
<p>10，设置</p>
<p>您可以注入并使用IOrganizationUnitSettings接口来获取组织单位设置值。 目前，只有一个可以根据您的应用需求进行更改的设置：</p>
<p>MaxUserMembershipCount：用户最大允许的会员数。<br />默认值为int.MaxValue，允许用户在同一时间成为无限制OU的成员。<br />设置名称是在AbpZeroSettingNames.OrganizationUnits.MaxUserMembershipCount中定义的常量。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a8"></a>八、权限管理</span></strong></p>
<p>1，角色权限</p>
<p>如果我们授予权限角色，则所有用户都有权限授权（除非明确禁止特定用户使用）。</p>
<p>我们使用RoleManager更改角色的权限。 例如，SetGrantedPermissionsAsync可用于在一个方法调用中更改角色的所有权限：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> RoleAppService : IRoleAppService
{
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> RoleManager _roleManager;
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> IPermissionManager _permissionManager;

    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> RoleAppService(RoleManager roleManager, IPermissionManager permissionManager)
    {
        _roleManager </span>=<span style="color: #000000;"> roleManager;
        _permissionManager </span>=<span style="color: #000000;"> permissionManager;
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span><span style="color: #000000;"> Task UpdateRolePermissions(UpdateRolePermissionsInput input)
    {
        </span><span style="color: #0000ff;">var</span> role = <span style="color: #0000ff;">await</span><span style="color: #000000;"> _roleManager.GetRoleByIdAsync(input.RoleId);
        </span><span style="color: #0000ff;">var</span> grantedPermissions =<span style="color: #000000;"> _permissionManager
            .GetAllPermissions()
            .Where(p </span>=&gt;<span style="color: #000000;"> input.GrantedPermissionNames.Contains(p.Name))
            .ToList();

        </span><span style="color: #0000ff;">await</span><span style="color: #000000;"> _roleManager.SetGrantedPermissionsAsync(role, grantedPermissions);
    }
}</span></pre>
</div>
<p>在这个例子中，我们得到一个RoleId和已授予的权限名称列表（input.GrantedPermissionNames是List &lt;string&gt;）作为输入。 我们使用IPermissionManager按名称查找所有权限对象。 然后我们调用SetGrantedPermissionsAsync方法来更新角色的权限。</p>
<p>还有其他方法，如GrantPermissionAsync和ProhibitPermissionAsync一个一个地控制权限。</p>
<p>2，用户权限</p>
<p>虽然基于角色的权限管理对于大多数应用程序来说足够，但我们可能需要控制每个用户的权限。 当我们为用户定义权限设置时，它覆盖权限设置来自用户的角色。</p>
<p>举个例子; 假设我们有一个应用程序服务来禁止用户的权限：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> UserAppService : IUserAppService
{
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> UserManager _userManager;
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> IPermissionManager _permissionManager;

    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> UserAppService(UserManager userManager, IPermissionManager permissionManager)
    {
        _userManager </span>=<span style="color: #000000;"> userManager;
        _permissionManager </span>=<span style="color: #000000;"> permissionManager;
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span><span style="color: #000000;"> Task ProhibitPermission(ProhibitPermissionInput input)
    {
        </span><span style="color: #0000ff;">var</span> user = <span style="color: #0000ff;">await</span><span style="color: #000000;"> _userManager.GetUserByIdAsync(input.UserId);
        </span><span style="color: #0000ff;">var</span> permission =<span style="color: #000000;"> _permissionManager.GetPermission(input.PermissionName);

        </span><span style="color: #0000ff;">await</span><span style="color: #000000;"> _userManager.ProhibitPermissionAsync(user, permission);
    }
}</span></pre>
</div>
<p>UserManager有许多方法来控制用户的权限。 在这个例子中，我们得到一个UserId和PermissionName，并使用UserManager的ProhibitPermissionAsync方法来禁止用户的权限。</p>
<p>当我们禁止用户的许可时，即使他/她的角色被授予许可，他/她也不能获得此许可。 我们可以说同样的原则给予。 当我们授予专门为用户授予的权限时，该用户被授予权限，即使用户的角色也不被授予权限。 我们可以为用户使用ResetAllPermissionsAsync来删除用户的所有用户特定权限设置。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a9"></a>九、语言管理</span></strong></span></p>
<p>虽然在大多数情况下都有好处，但我们可能希望在数据库上动态定义语言和文本。 Zero模块允许我们动态管理每个租户的应用程序语言和文本。</p>
<p>1，介绍</p>
<p>①EnableDbLocalization</p>
<p>启用</p>
<div class="cnblogs_code">
<pre>Configuration.Modules.Zero().LanguageManagement.EnableDbLocalization();</pre>
</div>
<p>这应该在顶级模块的PreInitialize方法（它是Web应用程序的Web模块）中导入Abp.Zero.Configuration命名空间（使用Abp.Zero.Configuration）来查看Zero（）扩展方法）。</p>
<p>②种子数据库语言</p>
<p>由于ABP将从数据库中获得语言列表，所以我们应该将默认语言插入数据库。 如果您使用EntityFramework，<a href="https://github.com/aspnetboilerplate/module-zero-template/blob/master/src/AbpCompanyName.AbpProjectName.EntityFramework/Migrations/SeedData/DefaultLanguagesCreator.cs" target="_blank">您可以像下面那样使用种子代码</a>：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Localization;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> AbpCompanyName.AbpProjectName.EntityFramework;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> AbpCompanyName.AbpProjectName.Migrations.SeedData
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> DefaultLanguagesCreator
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> List&lt;ApplicationLanguage&gt; InitialLanguages { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">private</span> <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> AbpProjectNameDbContext _context;

        </span><span style="color: #0000ff;">static</span><span style="color: #000000;"> DefaultLanguagesCreator()
        {
            InitialLanguages </span>= <span style="color: #0000ff;">new</span> List&lt;ApplicationLanguage&gt;<span style="color: #000000;">
            {
                </span><span style="color: #0000ff;">new</span> ApplicationLanguage(<span style="color: #0000ff;">null</span>, <span style="color: #800000;">"</span><span style="color: #800000;">en</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">English</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">famfamfam-flag-gb</span><span style="color: #800000;">"</span><span style="color: #000000;">),
                </span><span style="color: #0000ff;">new</span> ApplicationLanguage(<span style="color: #0000ff;">null</span>, <span style="color: #800000;">"</span><span style="color: #800000;">tr</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">T&uuml;rk&ccedil;e</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">famfamfam-flag-tr</span><span style="color: #800000;">"</span><span style="color: #000000;">),
                </span><span style="color: #0000ff;">new</span> ApplicationLanguage(<span style="color: #0000ff;">null</span>, <span style="color: #800000;">"</span><span style="color: #800000;">zh-CN</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">简体中文</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">famfamfam-flag-cn</span><span style="color: #800000;">"</span><span style="color: #000000;">),
                </span><span style="color: #0000ff;">new</span> ApplicationLanguage(<span style="color: #0000ff;">null</span>, <span style="color: #800000;">"</span><span style="color: #800000;">pt-BR</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">Portugu&ecirc;s-BR</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">famfamfam-flag-br</span><span style="color: #800000;">"</span><span style="color: #000000;">),
                </span><span style="color: #0000ff;">new</span> ApplicationLanguage(<span style="color: #0000ff;">null</span>, <span style="color: #800000;">"</span><span style="color: #800000;">es</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">Espa&ntilde;ol</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">famfamfam-flag-es</span><span style="color: #800000;">"</span><span style="color: #000000;">),
                </span><span style="color: #0000ff;">new</span> ApplicationLanguage(<span style="color: #0000ff;">null</span>, <span style="color: #800000;">"</span><span style="color: #800000;">fr</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">Fran&ccedil;ais</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">famfamfam-flag-fr</span><span style="color: #800000;">"</span><span style="color: #000000;">),
                </span><span style="color: #0000ff;">new</span> ApplicationLanguage(<span style="color: #0000ff;">null</span>, <span style="color: #800000;">"</span><span style="color: #800000;">it</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">Italiano</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">famfamfam-flag-it</span><span style="color: #800000;">"</span><span style="color: #000000;">),
                </span><span style="color: #0000ff;">new</span> ApplicationLanguage(<span style="color: #0000ff;">null</span>, <span style="color: #800000;">"</span><span style="color: #800000;">ja</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">日本語</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">famfamfam-flag-jp</span><span style="color: #800000;">"</span><span style="color: #000000;">),
                </span><span style="color: #0000ff;">new</span> ApplicationLanguage(<span style="color: #0000ff;">null</span>, <span style="color: #800000;">"</span><span style="color: #800000;">nl-NL</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">Nederlands</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">famfamfam-flag-nl</span><span style="color: #800000;">"</span><span style="color: #000000;">),
                </span><span style="color: #0000ff;">new</span> ApplicationLanguage(<span style="color: #0000ff;">null</span>, <span style="color: #800000;">"</span><span style="color: #800000;">lt</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">Lietuvos</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">famfamfam-flag-lt</span><span style="color: #800000;">"</span><span style="color: #000000;">)
            };
        }

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> DefaultLanguagesCreator(AbpProjectNameDbContext context)
        {
            _context </span>=<span style="color: #000000;"> context;
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Create()
        {
            CreateLanguages();
        }

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> CreateLanguages()
        {
            </span><span style="color: #0000ff;">foreach</span> (<span style="color: #0000ff;">var</span> language <span style="color: #0000ff;">in</span><span style="color: #000000;"> InitialLanguages)
            {
                AddLanguageIfNotExists(language);
            }
        }

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> AddLanguageIfNotExists(ApplicationLanguage language)
        {
            </span><span style="color: #0000ff;">if</span> (_context.Languages.Any(l =&gt; l.TenantId == language.TenantId &amp;&amp; l.Name ==<span style="color: #000000;"> language.Name))
            {
                </span><span style="color: #0000ff;">return</span><span style="color: #000000;">;
            }

            _context.Languages.Add(language);

            _context.SaveChanges();
        }
    }
}</span></pre>
</div>
<p>③删除静态语言配置</p>
<p>如果您具有如下所示的静态语言配置，您可以从配置代码中删除这些行，因为它将从数据库中获取语言。</p>
<div class="cnblogs_code">
<pre>Configuration.Localization.Languages.Add(<span style="color: #0000ff;">new</span> LanguageInfo(<span style="color: #800000;">"</span><span style="color: #800000;">en</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">English</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">famfamfam-flag-england</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">true</span>));</pre>
</div>
<p>④注意现有的XML本地化源</p>
<p>不要删除您的XML本地化文件和源配置代码。 因为这些文件被用作回退源，并且所有的本地化密钥都是从这个源获得的。</p>
<p>因此，当您需要一个新的本地化文本时，按照正常情况将其定义为XML文件。 您应至少在默认语言的XML文件中定义它。 因此，您不需要将本地化文本的默认值添加到数据库迁移代码。</p>
<p>2，管理语言</p>
<p>IApplicationLanguageManager接口被注入并用于管理语言。 它具有GetLanguagesAsync，AddAsync，RemoveAsync，UpdateAsync等方法来管理主机和租户的语言。</p>
<p>①语言列表逻辑</p>
<p>语言列表按租户和主机存储，计算方法如下：</p>
<ul>
<li>有一个为主机定义的语言列表。 该列表被视为所有租户的默认列表.</li>
<li>每个租户有一个单独的语言列表。 此列表继承主机列表添加特定于特定语言的语言。 租户不能删除或更新主机定义（默认）语言（但可以覆盖本地化文本，我们将在后面看到）.</li>
</ul>
<p>②ApplicationLanguage实体<br />ApplicationLanguage实体表示租户或主机的语言。</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">[Serializable]
[Table(</span><span style="color: #800000;">"</span><span style="color: #800000;">AbpLanguages</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ApplicationLanguage : FullAuditedEntity, IMayHaveTenant
{
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
}</pre>
</div>
<p>它的基本属性是：</p>
<ul>
<li><strong>TenantId</strong>&nbsp;(可空):&nbsp;包含有关租户的Id，如果这种语言是特定于租户的。 如果这是主机语言，则为null。</li>
<li><strong>Name</strong>:&nbsp;语言名称 这必须是列表中的文化代码。</li>
<li><strong>DisplayName</strong>: 显示语言的名称。 这可以是任意名称，一般是CultureInfo.DisplayName.</li>
<li><strong>Icon</strong>: .语言的任意图标/标志。 这可以用于在UI上显示语言的标志</li>
</ul>
<p>此外，ApplicationLanguage继承了您所看到的FullAuditedEntity。 这意味着它是一个软删除实体，并自动审核（有关更多信息，请参阅实体文档）。</p>
<p>ApplicationLanguage实体存储在数据库中的AbpLanguages表中。</p>
<p>3，管理本地化文本</p>
<p>IApplicationLanguageTextManager接口被注入并用于管理本地化文本。 它需要获取/设置租户或主机的本地化文本的方法。</p>
<p>①本地化文本<br />让我们看看当你想本地化一个文本时会发生什么？</p>
<ul>
<li>尝试获得当前文化（获得使用CurrentThread.CurrentUICulture）.
<ul>
<li>它检查给定文本是否定义（覆盖）当前租户（获取使用IAbpSession.TenantId）在数据库中的当前文化。 如果定义，则返回值.</li>
<li>然后，它检查数据库中当前文化中的主机是否定义（覆盖）给定文本。 如果定义，则返回值.</li>
<li>然后，它检查在当前文化中的底层XML文件中是否定义了给定的文本。 如果定义，则返回值.</li>





</ul>





</li>
<li>尝试寻找回归文化。 这样计算：如果现在的文化是&ldquo;en-GB&rdquo;，那么后备文化就是&ldquo;en&rdquo;.
<ul>
<li>它检查数据库中的后备文化中当前租户是否定义（覆盖）给定文本。 如果定义，则返回值.</li>
<li>然后，它检查在数据库中的后备文化中主机是否定义（覆盖）给定文本。 如果定义，则返回值.</li>
<li>然后，它会检查在后备文化中的底层XML文件中是否定义了给定的文本。 如果定义，则返回值.</li>





</ul>





</li>
<li>尝试找到默认文化.
<ul>
<li>它检查数据库中默认文化中当前租户是否定义（覆盖）给定文本。 如果定义，则返回值.</li>
<li>然后它检查在数据库中默认文化中主机是否定义（覆盖）给定文本。 如果定义，则返回值.</li>
<li>然后，它会检查在默认文化中的底层XML文件中是否定义了给定的文本。 如果定义，则返回值.</li>





</ul>





</li>
<li>获取相同的文本或抛出异常<br />
<ul>
<li>如果根本没有找到给定的文本（键），ABP会抛出异常或通过用[和]包装返回相同的文本（键）.</li>





</ul>





</li>





</ul>
<p>因此，获取本地化的文本有点复杂。 但它起作用很快，因为它使用缓存。</p>
<p>②ApplicationLanguageText实体<br />ApplicationLanguageText用于存储数据库中的本地化值。</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">[Serializable]
[Table(</span><span style="color: #800000;">"</span><span style="color: #800000;">AbpLanguageTexts</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> ApplicationLanguageText : AuditedEntity&lt;<span style="color: #0000ff;">long</span>&gt;<span style="color: #000000;">, IMayHaveTenant
{
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
}</pre>
</div>
<p>它的基本属性是：</p>
<ul>
<li><strong>TenantId</strong>&nbsp;(可空):如果本地化文本是特定于租户的，则包含相关租户的身份证号码。 如果这是主机本地化的文本，它为null .</li>
<li><strong>LanguageName</strong>: 语言名称 这必须是列表中的文化代码。 这与ApplicationLanguage.Name匹配，但不强制外键使其独立于语言条目。 IApplicationLanguageTextManager正确处理它.</li>
<li><strong>Source</strong>: 本地化源名称.</li>
<li><strong>Key</strong>: 本地化文本的键/名称.</li>
<li><strong>Value</strong>: 本地化值.</li>
</ul>
<p>ApplicationLanguageText实体存储在数据库的AbpLanguageTexts表中。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a10"></a>十、Identity Server集成</span></strong></span></p>
<p>Identity Server是一个开源OpenID Connect和OAuth 2.0框架。 它可以用于使您的应用程序在服务器上进行身份验证/单一登录。 它还可以为第三方客户端发出访问令牌。 本文档介绍如何将IdentityServer集成到项目中。</p>
<p>1，安装</p>
<ul>
<li><a href="https://www.nuget.org/packages/Abp.ZeroCore.IdentityServer4" target="_blank"><strong>Abp.ZeroCore.IdentityServer4</strong></a>&nbsp;是主要的集成包.</li>
<li><a href="https://www.nuget.org/packages/Abp.ZeroCore.IdentityServer4.EntityFrameworkCore" target="_blank"><strong>Abp.ZeroCore.IdentityServer4.EntityFrameworkCore</strong></a>&nbsp;.</li>
</ul>
<p>由于EF核心包已经取决于第一个，您只能将Abp.ZeroCore.IdentityServer4.EntityFrameworkCore包安装到您的项目中。 安装到项目中包含您的DbContext（.EntityFrameworkCore项目为默认模板）：</p>
<div class="cnblogs_code">
<pre>Install-Package Abp.ZeroCore.IdentityServer4.EntityFrameworkCore</pre>
</div>
<p>然后你可以添加依赖关系到你的模块（一般来说，你的EntityFrameworkCore项目）：</p>
<div class="cnblogs_code">
<pre>[DependsOn(<span style="color: #0000ff;">typeof</span><span style="color: #000000;">(AbpZeroCoreIdentityServerEntityFrameworkCoreModule))]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyModule : AbpModule
{
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
}</pre>
</div>
<p>2，配置</p>
<p>使用Abp.ZeroCore配置和使用IdentityServer4类似于独立使用IdentityServer4。 您应该阅读它自己的文档来了解和使用它。 在本文档中，我们仅显示了与Abp.ZeroCore集成所需的其他配置。</p>
<p>①Startup Class</p>
<p>在ASP.NET Core Startup类中，我们应该将IdentityServer添加到服务集合和ASP.NET Core中间件管道中。 突出了与标准IdentityServer4使用的差异：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Startup
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> ConfigureServices(IServiceCollection services)
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">        
        services.AddAbpIdentity</span>&lt;Tenant, User, Role&gt;<span style="color: #000000;">()
            ...
            .AddAbpIdentityServer();
        
        </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">        
        services.AddIdentityServer()
            .AddDeveloperSigningCredential()
            .AddInMemoryIdentityResources(IdentityServerConfig.GetIdentityResources())
            .AddInMemoryApiResources(IdentityServerConfig.GetApiResources())
            .AddInMemoryClients(IdentityServerConfig.GetClients())
            .AddAbpPersistedGrants</span>&lt;YourDbContext&gt;<span style="color: #000000;">()
            .AddAbpIdentityServer</span>&lt;User&gt;<span style="color: #000000;">();

        </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configure(IApplicationBuilder app)
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">        app.UseIdentityServer();
        </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">    }
}</span></pre>
</div>
<p>1）在AddAbpIdentity ... chain之后添加了.AddAbpIdentityServer（）。 在ABP中，启动模板AddAbpIdentity位于IdentityRegistrar.Register（services）方法中。 所以，你可以像IdentityRegistrar.Register（services）.AddAbpIdentityServer（）链接。</p>
<p>2）在启动项目中，在IdentityRegistrar.Register（services）之后添加了services.AddIdentityServer（）并添加了app.UseIdentityServer（）只是app.UseAuthentication（）。</p>
<p>3，IdentityServerConfig类<br />我们使用IdentityServerConfig类来获取身份资源，api资源和客户端。 您可以在自己的文档中找到有关此类的更多信息。 对于最简单的情况，它可以是一个静态类，如下所示</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> IdentityServerConfig
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> IEnumerable&lt;ApiResource&gt;<span style="color: #000000;"> GetApiResources()
    {
        </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> List&lt;ApiResource&gt;<span style="color: #000000;">
        {
            </span><span style="color: #0000ff;">new</span> ApiResource(<span style="color: #800000;">"</span><span style="color: #800000;">default-api</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">Default (all) API</span><span style="color: #800000;">"</span><span style="color: #000000;">)
        };
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> IEnumerable&lt;IdentityResource&gt;<span style="color: #000000;"> GetIdentityResources()
    {
        </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> List&lt;IdentityResource&gt;<span style="color: #000000;">
        {
            </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> IdentityResources.OpenId(),
            </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> IdentityResources.Profile(),
            </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> IdentityResources.Email(),
            </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> IdentityResources.Phone()
        };
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> IEnumerable&lt;Client&gt;<span style="color: #000000;"> GetClients()
    {
        </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> List&lt;Client&gt;<span style="color: #000000;">
        {
            </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> Client
            {
                ClientId </span>= <span style="color: #800000;">"</span><span style="color: #800000;">client</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                AllowedGrantTypes </span>=<span style="color: #000000;"> GrantTypes.ClientCredentials.Union(GrantTypes.ResourceOwnerPassword),
                AllowedScopes </span>= {<span style="color: #800000;">"</span><span style="color: #800000;">default-api</span><span style="color: #800000;">"</span><span style="color: #000000;">},
                ClientSecrets </span>=<span style="color: #000000;">
                {
                    </span><span style="color: #0000ff;">new</span> Secret(<span style="color: #800000;">"</span><span style="color: #800000;">secret</span><span style="color: #800000;">"</span><span style="color: #000000;">.Sha256())
                }
            }
        };
    }
}</span></pre>
</div>
<p>4，DbContext Changes</p>
<p>&nbsp;AddAbpPersistentGrants()方法用于保存持久数据存储的同意响应。 为了使用它，YourDbContext必须实现IAbpPersistedGrantDbContext接口，如下所示：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> YourDbContext : AbpZeroDbContext&lt;Tenant, Role, User, YourDbContext&gt;<span style="color: #000000;">, IAbpPersistedGrantDbContext
{
    </span><span style="color: #0000ff;">public</span> DbSet&lt;PersistedGrantEntity&gt; PersistedGrants { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span> YourDbContext(DbContextOptions&lt;YourDbContext&gt;<span style="color: #000000;"> options)
        : </span><span style="color: #0000ff;">base</span><span style="color: #000000;">(options)
    {
    }

    </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> OnModelCreating(ModelBuilder modelBuilder)
    {
        </span><span style="color: #0000ff;">base</span><span style="color: #000000;">.OnModelCreating(modelBuilder);

        modelBuilder.ConfigurePersistedGrantEntity();
    }
}</span></pre>
</div>
<p>IAbpPersistedGrantDbContext定义了PersistedGrants DbSet。 我们还应该调用上面显示的modelBuilder.ConfigurePersistedGrantEntity()扩展方法，以便为PersistedGrantEntity配置EntityFramework。</p>
<p>请注意，YourDbContext中的此更改会导致新的数据库迁移。 因此，请记住使用&ldquo;添加迁移&rdquo;和&ldquo;更新数据库&rdquo;命令来更新数据库。</p>
<p>即使您不调用AddAbpPersistedGrants &lt;YourDbContext&gt;()扩展方法，IdentityServer4仍将继续工作，但在这种情况下，用户同意响应将被存储在内存数据存储中（重新启动应用程序时会被清除）。</p>
<p>5，JWT认证中间件<br />如果我们要针对相同的应用程序授权客户端，我们可以使用IdentityServer身份验证中间件。</p>
<p>首先，将IdentityServer4.AccessTokenValidation包从nuget安装到您的项目中：</p>
<div class="cnblogs_code">
<pre>Install-Package IdentityServer4.AccessTokenValidation</pre>
</div>
<p>然后我们可以将中间件添加到Startup类中，如下所示</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">app.UseIdentityServerAuthentication(
    </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> IdentityServerAuthenticationOptions
    {
        Authority </span>= <span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:62114/</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        RequireHttpsMetadata </span>= <span style="color: #0000ff;">false</span><span style="color: #000000;">,
        AutomaticAuthenticate </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">,
        AutomaticChallenge </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">
    });</span></pre>
</div>
<p>我刚刚在启动项目中的app.UseIdentityServer()之后添加了这个。</p>
<p>6，测试</p>
<p>现在，我们的身份服务器已准备好从客户端获取请求。 我们可以创建一个控制台应用程序来发出请求并获得响应。</p>
<ul>
<li>在解决方案中创建一个新的控制台应用.</li>
<li>将IdentityModel nuget软件包添加到控制台应用程序。 此包用于为OAuth端点创建客户端.</li>
</ul>
<p>虽然IdentityModel nuget软件包足以创建客户端并使用您的API，但我想以更安全的方式显示使用API：我们将将传入的数据转换为应用程序服务返回的DTO。</p>
<ul>
<li>从控制台应用程序添加对应用程序层的引用。 这将允许我们使用客户端应用层返回的相同的DTO类.</li>
<li>添加Abp.Web.Common nuget包。 这将允许我们使用ASP.NET Boilerplate类中定义的AjaxResponse类。 否则，我们将处理原始的JSON字符串来处理服务器响应.</li>
</ul>
<p>那么我们可以改变Program.cs，如下所示：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Net;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Net.Http;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Application.Services.Dto;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Json;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> IdentityModel.Client;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.MultiTenancy;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Web.Models;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> IdentityServerIntegrationDemo.Users.Dto;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Newtonsoft.Json;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> IdentityServerIntegrationDemo.ConsoleApiClient
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            RunDemoAsync().Wait();
            Console.ReadLine();
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">async</span><span style="color: #000000;"> Task RunDemoAsync()
        {
            </span><span style="color: #0000ff;">var</span> accessToken = <span style="color: #0000ff;">await</span><span style="color: #000000;"> GetAccessTokenViaOwnerPasswordAsync();
            </span><span style="color: #0000ff;">await</span><span style="color: #000000;"> GetUsersListAsync(accessToken);
        }

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">async</span> Task&lt;<span style="color: #0000ff;">string</span>&gt;<span style="color: #000000;"> GetAccessTokenViaOwnerPasswordAsync()
        {
            </span><span style="color: #0000ff;">var</span> disco = <span style="color: #0000ff;">await</span> DiscoveryClient.GetAsync(<span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:62114</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            </span><span style="color: #0000ff;">var</span> httpHandler = <span style="color: #0000ff;">new</span><span style="color: #000000;"> HttpClientHandler();
            httpHandler.CookieContainer.Add(</span><span style="color: #0000ff;">new</span> Uri(<span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:62114/</span><span style="color: #800000;">"</span>), <span style="color: #0000ff;">new</span> Cookie(MultiTenancyConsts.TenantIdResolveKey, <span style="color: #800000;">"</span><span style="color: #800000;">1</span><span style="color: #800000;">"</span>)); <span style="color: #008000;">//</span><span style="color: #008000;">Set TenantId</span>
            <span style="color: #0000ff;">var</span> tokenClient = <span style="color: #0000ff;">new</span> TokenClient(disco.TokenEndpoint, <span style="color: #800000;">"</span><span style="color: #800000;">client</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">secret</span><span style="color: #800000;">"</span><span style="color: #000000;">, httpHandler);
            </span><span style="color: #0000ff;">var</span> tokenResponse = <span style="color: #0000ff;">await</span> tokenClient.RequestResourceOwnerPasswordAsync(<span style="color: #800000;">"</span><span style="color: #800000;">admin</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">123qwe</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (tokenResponse.IsError)
            {
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">Error: </span><span style="color: #800000;">"</span><span style="color: #000000;">);
                Console.WriteLine(tokenResponse.Error);
            }

            Console.WriteLine(tokenResponse.Json);

            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> tokenResponse.AccessToken;
        }

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">async</span> Task GetUsersListAsync(<span style="color: #0000ff;">string</span><span style="color: #000000;"> accessToken)
        {
            </span><span style="color: #0000ff;">var</span> client = <span style="color: #0000ff;">new</span><span style="color: #000000;"> HttpClient();
            client.SetBearerToken(accessToken);

            </span><span style="color: #0000ff;">var</span> response = <span style="color: #0000ff;">await</span> client.GetAsync(<span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:62114/api/services/app/user/getUsers</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            </span><span style="color: #0000ff;">if</span> (!<span style="color: #000000;">response.IsSuccessStatusCode)
            {
                Console.WriteLine(response.StatusCode);
                </span><span style="color: #0000ff;">return</span><span style="color: #000000;">;
            }

            </span><span style="color: #0000ff;">var</span> content = <span style="color: #0000ff;">await</span><span style="color: #000000;"> response.Content.ReadAsStringAsync();
            </span><span style="color: #0000ff;">var</span> ajaxResponse = JsonConvert.DeserializeObject&lt;AjaxResponse&lt;PagedResultDto&lt;UserListDto&gt;&gt;&gt;<span style="color: #000000;">(content);
            </span><span style="color: #0000ff;">if</span> (!<span style="color: #000000;">ajaxResponse.Success)
            {
                </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> Exception(ajaxResponse.Error?.Message ?? <span style="color: #800000;">"</span><span style="color: #800000;">Remote service throws exception!</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }

            Console.WriteLine();
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">Total user count: </span><span style="color: #800000;">"</span> +<span style="color: #000000;"> ajaxResponse.Result.TotalCount);
            Console.WriteLine();
            </span><span style="color: #0000ff;">foreach</span> (<span style="color: #0000ff;">var</span> user <span style="color: #0000ff;">in</span><span style="color: #000000;"> ajaxResponse.Result.Items)
            {
                Console.WriteLine($</span><span style="color: #800000;">"</span><span style="color: #800000;">### UserId: {user.Id}, UserName: {user.UserName}</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                Console.WriteLine(user.ToJsonString(indented: </span><span style="color: #0000ff;">true</span><span style="color: #000000;">));
            }
        }
    }
}</span></pre>
</div>
<p>运行此应用程序之前，请确保您的Web项目已启动并运行，因为此控制台应用程序将向Web应用程序发出请求。 另外，请确保请求端口（62114）与您的Web应用程序相同。</p>
<p>您可以在此处看到本教程的源代码：<a href="https://github.com/aspnetboilerplate/aspnetboilerplate-samples/tree/master/IdentityServerDemo" target="_blank">https://github.com/aspnetboilerplate/aspnetboilerplate-samples/tree/master/IdentityServerDemo</a>。&nbsp;</p>
<p>&nbsp;</p>