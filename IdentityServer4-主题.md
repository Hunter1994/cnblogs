<p><a href="#a1">&nbsp;一、Startup</a></p>
<p><a href="#a2">二、定义Resources</a></p>
<p><a href="#a3">三、定义Clients</a></p>
<p><a href="#a4">四、登录</a></p>
<p><a href="#a5">五、使用外部身份提供商登录</a></p>
<p><a href="#a6">六、Windows身份验证</a></p>
<p><a href="#a7">七、登出</a></p>
<p><a href="#a8">八、注销外部身份提供商</a></p>
<p><a href="#a9">九、联合注销</a></p>
<p><a href="#a10">十、联合网关</a></p>
<p><a href="#a11">十一、Consent</a></p>
<p><a href="#a12">十二、保护APIs</a></p>
<p><a href="#a13">十三、部署</a></p>
<p><a href="#a14">十四、日志</a></p>
<p><a href="#a15">十五、事件</a></p>
<p><a href="#a16">十六、Cryptography, Keys and HTTPS</a></p>
<p><a href="#a17">十七、Grant Types</a></p>
<p><a href="#a18">十八、Secrets</a></p>
<p><a href="#a19">十九、Extension Grants</a></p>
<p><a href="#a20">二十、Resource Owner Password Validation</a></p>
<p><a href="#a21">二十一、Refresh Tokens</a></p>
<p><a href="#a22">二十二、Reference Tokens</a></p>
<p><a href="#a23">二十三、CORS</a></p>
<p><a href="#a24">二十四、Discovery</a></p>
<p><a href="#a25">二十五、Adding more API Endpoints</a></p>
<p><a href="#a26">二十六、Adding new Protocols</a></p>
<p><a href="#a27">二十七、Tools</a></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">一、Startup<a name="a1"></a></span></strong></span></p>
<p>&nbsp;IdentityServer是中间件和服务的组合。 所有的配置都在你的startup类上完成。</p>
<p><strong><span style="font-size: 14pt;">配置服务</span></strong></p>
<p>通过调用以下方式将IdentityServer服务添加到DI系统：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> ConfigureServices(IServiceCollection services)
{
    </span><span style="color: #0000ff;">var</span> builder =<span style="color: #000000;"> services.AddIdentityServer();
}</span></pre>
</div>
<p>或者，您可以将选项传入此调用。</p>
<p>这将返回一个构建器对象，该构造器对象又有许多方便的方法来连接其他服务。</p>
<p><strong><span style="font-size: 14pt;">key材料</span></strong></p>
<ul class="simple">
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">AddSigningCredential</span></code></dt><dd>添加一个签名密钥服务，该服务将指定的密钥材料提供给各种令牌创建/验证服务。 您可以传入X509Certificate2，SigningCredential或对证书存储区中证书的引用。</dd></dl></li>
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">AddDeveloperSigningCredential</span></code></dt><dd>在启动时创建临时密钥材料。 当您没有要使用的证书时，这仅适用于开发场景。 生成的密钥将保存到文件系统，以便在服务器重新启动之间保持稳定（可通过传递false来禁用）。 这解决了客户端/ api元数据缓存在开发期间不同步的问题。</dd></dl></li>
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">AddValidationKey</span></code></dt><dd>添加验证令牌的密钥。 它们将被内部令牌验证器使用，并将显示在发现文档中。 您可以传入X509Certificate2，SigningCredential或对证书存储区中证书的引用。 这对于key的转换场景很有用。</dd></dl></li>
</ul>
<p><strong><span style="font-size: 14pt;">In-Memory configuration stores</span></strong></p>
<p>各种&ldquo;in-memory&rdquo;从内存中配置IdentityServer。这些&ldquo;in-memory&rdquo;集合可以在宿主应用程序中进行硬编码，也可以从配置文件或数据库动态加载。 但是，通过设计，这些集合仅在托管应用程序启动时创建。</p>
<p>使用这些配置API可用于原型设计，开发和或测试时不需要在运行时动态查询配置数据的数据库。 如果配置很少发生变化，这种配置方式也适用于生产方案，或者如果必须更改值，则需要重新启动应用程序并不方便。&nbsp;</p>
<ul class="simple">
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">AddInMemoryClients</span></code></dt><dd>根据client配置对象的内存中集合注册IClientStore和ICorsPolicyService实现。</dd></dl></li>
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">AddInMemoryIdentityResources</span></code></dt><dd>基于IdentityResource配置对象的内存中集合注册IResourceStore实现。</dd></dl></li>
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">AddInMemoryApiResources</span></code></dt><dd>根据ApiResource配置对象的内存集合注册IResourceStore实现。</dd></dl></li>
</ul>
<p><strong><span style="font-size: 14pt;">Test stores</span></strong></p>
<p>TestUser类在IdentityServer中为用户及其凭据和声明建模。TestUser的使用与使用&ldquo;in-memory&rdquo;存储类似，因为它适用于原型开发和/或测试。 生产中不推荐使用TestUser。</p>
<ul>
<li><code class="docutils literal notranslate"><span class="pre">AddTestUsers</span></code></li>
</ul>
<p>　　　　　基于TestUser对象的集合注册TestUserStore。 TestUserStore由默认的快速入门用户界面使用。 还注册IProfileService和IResourceOwnerPasswordValidator的实现。</p>
<p><strong><span style="font-size: 14pt;">其他服务</span></strong></p>
<ul class="simple">
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">AddExtensionGrantValidator</span></code></dt><dd>添加用于扩展授权的IExtensionGrantValidator实现。</dd></dl></li>
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">AddSecretParser</span></code></dt><dd>添加ISecretParser实现以解析客户端或API资源凭证。</dd></dl></li>
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">AddSecretValidator</span></code></dt><dd>添加ISecretValidator实现，以针对凭证存储验证客户端或API资源凭证。</dd></dl></li>
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">AddResourceOwnerValidator</span></code></dt><dd>添加IResourceOwnerPasswordValidator实现，用于验证资源所有者密码凭据授权类型的用户凭证。</dd></dl></li>
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">AddProfileService</span></code></dt><dd>添加IProfileService实现以连接到您的自定义用户配置文件存储。 DefaultProfileService类提供了默认实现，它依赖于身份验证cookie作为唯一的凭证发放声明来源。</dd></dl></li>
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">AddAuthorizeInteractionResponseGenerator</span></code></dt><dd>添加IAuthorizeInteractionResponseGenerator实现以在授权端点自定义逻辑，以便必须向用户显示错误，登录，同意或任何其他自定义页面的UI。 AuthorizeInteractionResponseGenerator类提供了一个默认的实现，因此如果需要增加现有的行为，可以考虑从这个现有的类派生。</dd></dl></li>
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">AddCustomAuthorizeRequestValidator</span></code></dt><dd>添加ICustomAuthorizeRequestValidator实现以在授权端点定制请求参数验证。</dd></dl></li>
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">AddCustomTokenRequestValidator</span></code></dt><dd>添加ICustomTokenRequestValidator实现来定制令牌端点处的请求参数验证。</dd></dl></li>
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">AddRedirectUriValidator</span></code></dt><dd>添加IRedirectUriValidator实现来自定义重定向URI验证。</dd></dl></li>
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">AddAppAuthRedirectUriValidator</span></code></dt><dd>添加一个&ldquo;AppAuth&rdquo;（适用于本地应用的OAuth 2.0）兼容的重定向URI验证器（进行严格验证，但也允许http://127.0.0.1使用随机端口）。</dd></dl></li>
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">AddJwtBearerClientAuthentication</span></code></dt><dd>添加对使用JWT bearer断言的客户端身份验证的支持。</dd></dl></li>
</ul>
<p><strong><span style="font-size: 14pt;">Caching</span></strong></p>
<p>客户端和资源配置数据经常被IdentityServer使用。 如果从数据库或其他外部存储装载此数据，则经常重新加载相同数据可能会很昂贵。</p>
<ul class="simple">
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">AddInMemoryCaching</span></code></dt><dd>要使用下面描述的任何缓存，必须在DI中注册ICache &lt;T&gt;的实现。 此API注册了基于ASP.NET Core的MemoryCache的ICache &lt;T&gt;的默认内存实现。</dd></dl></li>
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">AddClientStoreCache</span></code></dt><dd>注册IClientStore装饰器实现，该实现将维护客户端配置对象的内存缓存。 可以在IdentityServerOptions上的Cachingconfiguration选项上配置缓存持续时间。</dd></dl></li>
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">AddResourceStoreCache</span></code></dt><dd>注册一个IResourceStore装饰器实现，它将维护IdentityResource和ApiResource配置对象的内存缓存。 缓存持续时间可以在IdentityServerOptions上的缓存配置选项上配置。</dd></dl></li>
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">AddCorsPolicyCache</span></code></dt><dd>注册一个ICorsPolicyService装饰器实现，它将维护CORS策略服务评估结果的内存缓存。 缓存持续时间可以在IdentityServerOptions上的缓存配置选项上配置。</dd></dl></li>
</ul>
<p>进一步定制缓存是可能的：</p>
<p>默认缓存依赖于ICache &lt;T&gt;实现。 如果您希望为特定配置对象定制缓存行为，则可以在依赖注入系统中替换此实现。</p>
<p>Cache &lt;T&gt;本身的默认实现依赖于.NET提供的IMemoryCache接口（和MemoryCache实现）。 如果您希望自定义内存中缓存行为，则可以替换依赖注入系统中的IMemoryCache实现。</p>
<p><strong><span style="font-size: 14pt;">配置管道</span></strong></p>
<p>您需要通过调用以下方式将IdentityServer添加到管道中：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configure(IApplicationBuilder app)
{
    app.UseIdentityServer();
}</span></pre>
</div>
<p>UseIdentityServer包含对UseAuthentication的调用，所以没有必要同时拥有两者。</p>
<p>没有额外的中间件配置。</p>
<p>请注意，管道的顺序中很重要。 例如，您需要在实现登录屏幕的UI框架之前添加IdentitySever。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">二、定义Resources<a name="a2"></a></span></strong></p>
<p>您通常在系统中定义的第一件事是您要保护的资源。 这可能是用户的身份信息，例如个人资料数据或电子邮件地址，或访问API。&nbsp;</p>
<p><strong><span style="font-size: 14pt;">定义identity resources</span></strong></p>
<p>identity resources是数据，如用户ID，姓名或用户的电子邮件地址。 身份资源具有唯一的名称，您可以为其分配任意声明类型。 这些声明将包含在用户的身份标识中。 客户端将使用scope参数来请求访问身份资源。</p>
<p>OpenID Connect规范指定了几个标准身份资源。 最低要求是，您提供了为用户发布唯一ID的支持 - 也称为subject id。 这是通过暴露名为openid的标准身份资源完成的：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> IEnumerable&lt;IdentityResource&gt;<span style="color: #000000;"> GetIdentityResources()
{
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> List&lt;IdentityResource&gt;<span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> IdentityResources.OpenId()
    };
}</span></pre>
</div>
<p>IdentityResources类支持规范中定义的所有范围（openid，电子邮件，配置文件，电话和地址）。 如果您想全部支持它们，可以将它们添加到支持的身份资源列表中：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> IEnumerable&lt;IdentityResource&gt;<span style="color: #000000;"> GetIdentityResources()
{
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> List&lt;IdentityResource&gt;<span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> IdentityResources.OpenId(),
        </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> IdentityResources.Email(),
        </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> IdentityResources.Profile(),
        </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> IdentityResources.Phone(),
        </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> IdentityResources.Address()
    };
}</span></pre>
</div>
<p><strong><span style="font-size: 14pt;">自定义identity resources</span></strong></p>
<p>您还可以自定义标识资源。 创建一个新的IdentityResource类，给它一个名称和一个可选的显示名称和描述，并在请求此资源时定义哪些用户声明应该包含在身份令牌中：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> IEnumerable&lt;IdentityResource&gt;<span style="color: #000000;"> GetIdentityResources()
{
    </span><span style="color: #0000ff;">var</span> customProfile = <span style="color: #0000ff;">new</span><span style="color: #000000;"> IdentityResource(
        name: </span><span style="color: #800000;">"</span><span style="color: #800000;">custom.profile</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        displayName: </span><span style="color: #800000;">"</span><span style="color: #800000;">Custom profile</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        claimTypes: </span><span style="color: #0000ff;">new</span>[] { <span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">email</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">status</span><span style="color: #800000;">"</span><span style="color: #000000;"> });

    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> List&lt;IdentityResource&gt;<span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> IdentityResources.OpenId(),
        </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> IdentityResources.Profile(),
        customProfile
    };
}</span></pre>
</div>
<p><strong><span style="font-size: 14pt;">定义API resources</span></strong></p>
<p>为了允许客户端请求API的访问令牌，您需要定义API资源，例如：</p>
<p>要获取API的访问令牌，还需要将它们注册为scope。 这次scope类型是Resource类型的：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> IEnumerable&lt;ApiResource&gt;<span style="color: #000000;"> GetApis()
{
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;">[]
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 简单的API与单一scope（在这种情况下，scope名称与api名称相同）</span>
        <span style="color: #0000ff;">new</span> ApiResource(<span style="color: #800000;">"</span><span style="color: #800000;">api1</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">Some API 1</span><span style="color: #800000;">"</span><span style="color: #000000;">),

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 如果需要更多的控制，扩展版本</span>
        <span style="color: #0000ff;">new</span><span style="color: #000000;"> ApiResource
        {
            Name </span>= <span style="color: #800000;">"</span><span style="color: #800000;">api2</span><span style="color: #800000;">"</span><span style="color: #000000;">,

            </span><span style="color: #008000;">//</span><span style="color: #008000;"> secret for using introspection endpoint</span>
            ApiSecrets =<span style="color: #000000;">
            {
                </span><span style="color: #0000ff;">new</span> Secret(<span style="color: #800000;">"</span><span style="color: #800000;">secret</span><span style="color: #800000;">"</span><span style="color: #000000;">.Sha256())
            },

            </span><span style="color: #008000;">//</span><span style="color: #008000;"> 在访问令牌中包含以下使用声明（除了subject ID）</span>
            UserClaims =<span style="color: #000000;"> { JwtClaimTypes.Name, JwtClaimTypes.Email },

            </span><span style="color: #008000;">//</span><span style="color: #008000;">此API定义了两个scope</span>
            Scopes =<span style="color: #000000;">
            {
                </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> Scope()
                {
                    Name </span>= <span style="color: #800000;">"</span><span style="color: #800000;">api2.full_access</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    DisplayName </span>= <span style="color: #800000;">"</span><span style="color: #800000;">Full access to API 2</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                },
                </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> Scope
                {
                    Name </span>= <span style="color: #800000;">"</span><span style="color: #800000;">api2.read_only</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    DisplayName </span>= <span style="color: #800000;">"</span><span style="color: #800000;">Read only access to API 2</span><span style="color: #800000;">"</span><span style="color: #000000;">
                }
            }
        }
    };
}</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">三、定义Clients<a name="a3"></a></span></strong></p>
<p>客户端代表可以从您的身份服务器请求令牌的应用程序。</p>
<p>细节有所不同，但您通常为客户端定义以下常用设置：</p>
<ul>
<li>一个唯一的client ID</li>
<li>secret&nbsp;如果需要的话</li>
<li>允许的与令牌服务的交互（称为授权类型）</li>
<li>身份和/或访问令牌发送到的网络位置（称为重定向URI）</li>
<li>客户端允许访问的范围列表（又名资源）</li>
</ul>
<p><strong><span style="font-size: 14pt;">定义服务器到服务器通信的客户端</span></strong></p>
<p>在这种情况下，不存在交互用户&mdash;服务(又称客户端)希望与API(又称范围)进行通信:</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Clients
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> IEnumerable&lt;Client&gt;<span style="color: #000000;"> Get()
    {
        </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> List&lt;Client&gt;<span style="color: #000000;">
        {
            </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> Client
            {
                ClientId </span>= <span style="color: #800000;">"</span><span style="color: #800000;">service.client</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                ClientSecrets </span>= { <span style="color: #0000ff;">new</span> Secret(<span style="color: #800000;">"</span><span style="color: #800000;">secret</span><span style="color: #800000;">"</span><span style="color: #000000;">.Sha256()) },

                AllowedGrantTypes </span>=<span style="color: #000000;"> GrantTypes.ClientCredentials,
                AllowedScopes </span>= { <span style="color: #800000;">"</span><span style="color: #800000;">api1</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">api2.read_only</span><span style="color: #800000;">"</span><span style="color: #000000;"> }
            }
        };
    }
}</span></pre>
</div>
<p><strong><span style="font-size: 14pt;">定义基于浏览器的JavaScript客户端（例如SPA）以进行用户身份验证和委派访问以及API</span></strong></p>
<p>该客户端使用所谓的隐式流来从JavaScript请求身份和访问令牌：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> jsClient = <span style="color: #0000ff;">new</span><span style="color: #000000;"> Client
{
    ClientId </span>= <span style="color: #800000;">"</span><span style="color: #800000;">js</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    ClientName </span>= <span style="color: #800000;">"</span><span style="color: #800000;">JavaScript Client</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    ClientUri </span>= <span style="color: #800000;">"</span><span style="color: #800000;">http://identityserver.io</span><span style="color: #800000;">"</span><span style="color: #000000;">,

    AllowedGrantTypes </span>=<span style="color: #000000;"> GrantTypes.Implicit,
    AllowAccessTokensViaBrowser </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">,

    RedirectUris </span>=           { <span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:7017/index.html</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
    PostLogoutRedirectUris </span>= { <span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:7017/index.html</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
    AllowedCorsOrigins </span>=     { <span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:7017</span><span style="color: #800000;">"</span><span style="color: #000000;"> },

    AllowedScopes </span>=<span style="color: #000000;">
    {
        IdentityServerConstants.StandardScopes.OpenId,
        IdentityServerConstants.StandardScopes.Profile,
        IdentityServerConstants.StandardScopes.Email,

        </span><span style="color: #800000;">"</span><span style="color: #800000;">api1</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">api2.read_only</span><span style="color: #800000;">"</span><span style="color: #000000;">
    }
};</span></pre>
</div>
<p>定义服务器端Web应用程序（例如MVC）以使用身份验证和委派API访问</p>
<p>交互式服务器端（或本地桌面/移动）应用程序使用混合流。 此流提供了最佳的安全性，因为访问令牌仅通过后通道调用传输(并允许您访问refresh令牌):：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> mvcClient = <span style="color: #0000ff;">new</span><span style="color: #000000;"> Client
{
    ClientId </span>= <span style="color: #800000;">"</span><span style="color: #800000;">mvc</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    ClientName </span>= <span style="color: #800000;">"</span><span style="color: #800000;">MVC Client</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    ClientUri </span>= <span style="color: #800000;">"</span><span style="color: #800000;">http://identityserver.io</span><span style="color: #800000;">"</span><span style="color: #000000;">,

    AllowedGrantTypes </span>=<span style="color: #000000;"> GrantTypes.Hybrid,
    AllowOfflineAccess </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">,
    ClientSecrets </span>= { <span style="color: #0000ff;">new</span> Secret(<span style="color: #800000;">"</span><span style="color: #800000;">secret</span><span style="color: #800000;">"</span><span style="color: #000000;">.Sha256()) },

    RedirectUris </span>=           { <span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:21402/signin-oidc</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
    PostLogoutRedirectUris </span>= { <span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:21402/</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
    FrontChannelLogoutUri </span>=  <span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:21402/signout-oidc</span><span style="color: #800000;">"</span><span style="color: #000000;">,

    AllowedScopes </span>=<span style="color: #000000;">
    {
        IdentityServerConstants.StandardScopes.OpenId,
        IdentityServerConstants.StandardScopes.Profile,
        IdentityServerConstants.StandardScopes.Email,

        </span><span style="color: #800000;">"</span><span style="color: #800000;">api1</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">api2.read_only</span><span style="color: #800000;">"</span><span style="color: #000000;">
    },
};</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">四、登录<a name="a4"></a></span></strong></span></p>
<p>&nbsp;为了让IdentityServer代表用户发出令牌，该用户必须登录到IdentityServer。</p>
<p><strong><span style="font-size: 14pt;">Cookie身份验证</span></strong></p>
<p>使用来自ASP.NET Core的cookie身份验证处理程序管理的cookie跟踪身份验证。</p>
<p>IdentityServer注册两个cookie处理程序（一个用于身份验证会话，另一个用于临时的外部cookie）。 这些是默认使用的，如果要手动引用它们，可以从IdentityServerConstants类（DefaultCookieAuthenticationScheme和ExternalCookieAuthenticationScheme）获取它们的名称。</p>
<p>我们只公开这些cookie的基本设置（到期和滑动），如果您需要更多控制，您可以注册自己的cookie处理程序。 当使用ASP.NET Core中的AddAuthentication时，IdentityServer使用与AuthenticationOptions上配置的任何cookie处理程序匹配的DefaultAuthenticateScheme。</p>
<p><strong><span style="font-size: 14pt;">重写cookie处理程序配置</span></strong></p>
<p>如果您希望使用自己的cookie身份验证处理程序，则必须自己配置它。 在DI（使用AddIdentityServer）注册IdentityServer后，必须在ConfigureServices中完成此操作。 例如：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">services.AddIdentityServer()
    .AddInMemoryClients(Clients.Get())
    .AddInMemoryIdentityResources(Resources.GetIdentityResources())
    .AddInMemoryApiResources(Resources.GetApiResources())
    .AddDeveloperSigningCredential()
    .AddTestUsers(TestUsers.Users);

services.AddAuthentication(</span><span style="color: #800000;">"</span><span style="color: #800000;">MyCookie</span><span style="color: #800000;">"</span><span style="color: #000000;">)
    .AddCookie(</span><span style="color: #800000;">"</span><span style="color: #800000;">MyCookie</span><span style="color: #800000;">"</span>, options =&gt;<span style="color: #000000;">
    {
        options.ExpireTimeSpan </span>=<span style="color: #000000;"> ...;
    });</span></pre>
</div>
<p><span style="font-size: 12px; color: #ff0000;">IdentityServer内部使用自定义方案（通过常量IdentityServerConstants.DefaultCookieAuthenticationScheme）调用AddAuthentication和AddCookie，因此要覆盖它们，必须在AddIdentityServer之后进行相同的调用。</span></p>
<p><strong><span style="font-size: 14pt;">登录用户界面和身份管理系统</span></strong></p>
<p>IdentityServer不为用户认证提供任何用户界面或用户数据库。 这些是您希望自己提供或开发的东西。</p>
<p>如果您需要基本UI的起点（登录，注销，同意和管理授权），您可以使用我们的<a class="reference external" href="https://github.com/IdentityServer/IdentityServer4.Quickstart.UI">quickstart UI</a>.</p>
<p>快速启动用户界面根据内存数据库对用户进行身份验证。 您可以通过访问真实用户存储来替换这些位。 我们有使用<a class="reference internal" href="https://identityserver4.readthedocs.io/en/release/quickstarts/6_aspnet_identity.html#refaspnetidentityquickstart"><span class="std std-ref">ASP.NET Identity</span></a>的示例。</p>
<p><strong><span style="font-size: 14pt;">登录工作流程</span></strong></p>
<p>当IdentityServer在授权端点收到请求并且用户未通过身份验证时，用户将被重定向到配置的登录页面。 您必须通过选项上的UserInteraction设置（默认为/ account/login）来通知IdentityServer您的登录页面的路径。 将传递returnUrl参数，通知您的登录页面，一旦登录完成，应该重定向用户。</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('76141d67-4b5b-4968-98b9-7cd64510073c')"><img id="code_img_closed_76141d67-4b5b-4968-98b9-7cd64510073c" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_76141d67-4b5b-4968-98b9-7cd64510073c" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('76141d67-4b5b-4968-98b9-7cd64510073c',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_76141d67-4b5b-4968-98b9-7cd64510073c" class="cnblogs_code_hide">
<pre>            services.AddIdentityServer(options=&gt;<span style="color: #000000;">{
                options.UserInteraction.LoginUrl</span>=<span style="color: #800000;">"</span><span style="color: #800000;">/Identity/Account/Login</span><span style="color: #800000;">"</span><span style="color: #000000;">;
            })
                    .AddDeveloperSigningCredential()
                    .AddInMemoryPersistedGrants()
                    .AddInMemoryApiResources(Config.GetApiResource())
                    .AddInMemoryIdentityResources(Config.GetIdentityResource())
                    .AddInMemoryClients(Config.GetClient())
                    .AddAspNetIdentity</span>&lt;IdentityUser&gt;();</pre>
</div>
<span class="cnblogs_code_collapse">重定向登录页面</span></div>
<p><img src="https://images2018.cnblogs.com/blog/741594/201806/741594-20180630171903380-1636471394.png" alt="" /></p>
<p><strong><span style="font-size: 14pt;">登录上下文</span></strong></p>
<p>在您的登录页面上，您可能需要有关请求上下文的信息，以便自定义登录体验（如客户端，提示参数，IdP提示或其他内容）。 这可以通过交互服务上的GetAuthorizationContextAsync API获取。</p>
<p><strong><span style="font-size: 14pt;">发布cookie和声明&nbsp;</span></strong></p>
<p>在ASP.NET Core的HttpContext上有与身份验证相关的扩展方法来发布身份验证cookie并签署用户身份。所使用的身份验证方案必须与您正在使用的cookie处理程序匹配（请参阅上文）。</p>
<p>当您在用户中签名时，您必须发出至少一个子claim和一个名称claim。IdentityServer还在HttpContext上提供一些SignInAsync扩展方法，使其更加方便。</p>
<p>您还可以选择发出idp声明（用于身份提供者名称），amr声明（用于所使用的身份验证方法）和/或auth_time声明（用于用户验证的纪元时间）。 如果您不提供这些，IdentityServer将提供默认值。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">五、使用外部身份提供商登录<a name="a5"></a></span></strong></p>
<p>ASP.NET Core具有处理外部认证的灵活方式。 这涉及几个步骤。</p>
<p><strong><span style="font-size: 14pt;">为外部提供者添加认证处理程序</span></strong></p>
<p>与外部提供者通信所需的协议实现封装在身份验证处理程序中。 一些提供商使用专有协议（例如Facebook等社交提供商），有些提供商使用标准协议，例如 OpenID Connect，WS-Federation或SAML2p。</p>
<p><strong><span style="font-size: 14pt;">Cookie的作用</span></strong></p>
<p>外部认证处理程序上的一个选项称为SignInScheme，例如：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">services.AddAuthentication()
    .AddGoogle(</span><span style="color: #800000;">"</span><span style="color: #800000;">Google</span><span style="color: #800000;">"</span>, options =&gt;<span style="color: #000000;">
    {
        options.SignInScheme </span>= <span style="color: #800000;">"</span><span style="color: #800000;">scheme of cookie handler to use</span><span style="color: #800000;">"</span><span style="color: #000000;">;

        options.ClientId </span>= <span style="color: #800000;">"</span><span style="color: #800000;">...</span><span style="color: #800000;">"</span><span style="color: #000000;">;
        options.ClientSecret </span>= <span style="color: #800000;">"</span><span style="color: #800000;">...</span><span style="color: #800000;">"</span><span style="color: #000000;">;
    })</span></pre>
</div>
<p>登录方案指定将临时存储外部认证结果的cookie处理程序的名称，例如 这得到了由外部供应商发来的声明。 这是必要的，因为在完成外部认证过程之前，通常会有几个重定向。</p>
<p>鉴于这是一种常见做法，IdentityServer专门为此外部提供程序工作流程注册一个Cookie处理程序。 该方案通过IdentityServerConstants.ExternalCookieAuthenticationScheme常量表示。 如果您要使用我们的外部cookie处理程序，那么对于上面的SignInScheme，您将分配的值为IdentityServerConstants.ExternalCookieAuthenticationScheme常量：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">services.AddAuthentication()
    .AddGoogle(</span><span style="color: #800000;">"</span><span style="color: #800000;">Google</span><span style="color: #800000;">"</span>, options =&gt;<span style="color: #000000;">
    {
        options.SignInScheme </span>=<span style="color: #000000;"> IdentityServerConstants.ExternalCookieAuthenticationScheme;

        options.ClientId </span>= <span style="color: #800000;">"</span><span style="color: #800000;">...</span><span style="color: #800000;">"</span><span style="color: #000000;">;
        options.ClientSecret </span>= <span style="color: #800000;">"</span><span style="color: #800000;">...</span><span style="color: #800000;">"</span><span style="color: #000000;">;
    })</span></pre>
</div>
<p>您也可以注册自己的自定义cookie处理程序，如下所示：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">services.AddAuthentication()
    .AddCookie(</span><span style="color: #800000;">"</span><span style="color: #800000;">YourCustomScheme</span><span style="color: #800000;">"</span><span style="color: #000000;">)
    .AddGoogle(</span><span style="color: #800000;">"</span><span style="color: #800000;">Google</span><span style="color: #800000;">"</span>, options =&gt;<span style="color: #000000;">
    {
        options.SignInScheme </span>= <span style="color: #800000;">"</span><span style="color: #800000;">YourCustomScheme</span><span style="color: #800000;">"</span><span style="color: #000000;">;

        options.ClientId </span>= <span style="color: #800000;">"</span><span style="color: #800000;">...</span><span style="color: #800000;">"</span><span style="color: #000000;">;
        options.ClientSecret </span>= <span style="color: #800000;">"</span><span style="color: #800000;">...</span><span style="color: #800000;">"</span><span style="color: #000000;">;
    })</span></pre>
</div>
<p><strong><span style="font-size: 14pt;">触发认证处理程序</span></strong></p>
<p>您可以通过HttpContext上的ChallengeAsync扩展方法（或使用MVC ChallengeResult）调用外部认证处理程序。</p>
<p>您通常希望将一些选项传递给challenge操作，例如回调页面的路径和簿记提供程序的名称，例如:</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> callbackUrl = Url.Action(<span style="color: #800000;">"</span><span style="color: #800000;">ExternalLoginCallback</span><span style="color: #800000;">"</span><span style="color: #000000;">);

</span><span style="color: #0000ff;">var</span> props = <span style="color: #0000ff;">new</span><span style="color: #000000;"> AuthenticationProperties
{
    RedirectUri </span>=<span style="color: #000000;"> callbackUrl,
    Items </span>=<span style="color: #000000;">
    {
        { </span><span style="color: #800000;">"</span><span style="color: #800000;">scheme</span><span style="color: #800000;">"</span><span style="color: #000000;">, provider },
        { </span><span style="color: #800000;">"</span><span style="color: #800000;">returnUrl</span><span style="color: #800000;">"</span><span style="color: #000000;">, returnUrl }
    }
};

</span><span style="color: #0000ff;">return</span> Challenge(provider, props);</pre>
</div>
<p><strong><span style="font-size: 14pt;">处理回调并在用户中签名</span></strong></p>
<p>在回调页面上，您的典型任务是：</p>
<ul>
<li>检查由外部提供商返回的身份。</li>
<li>决定如何处理该用户。 如果这是新用户或返回用户，这可能会有所不同。</li>
<li>新用户在允许之前可能需要额外的步骤和UI。</li>
<li>可能会创建一个链接到外部提供程序的新内部用户帐户。</li>
<li>存储您想要保留的外部声明。</li>
<li>删除临时cookie</li>
<li>登录用户</li>
</ul>
<p>检查外部身份：</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> 从临时cookie中读取外部身份</span>
<span style="color: #0000ff;">var</span> result = <span style="color: #0000ff;">await</span><span style="color: #000000;"> HttpContext.AuthenticateAsync(IdentityServerConstants.ExternalCookieAuthenticationScheme);
</span><span style="color: #0000ff;">if</span> (result?.Succeeded != <span style="color: #0000ff;">true</span><span style="color: #000000;">)
{
    </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> Exception(<span style="color: #800000;">"</span><span style="color: #800000;">External authentication error</span><span style="color: #800000;">"</span><span style="color: #000000;">);
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">检索外部用户的声明</span>
<span style="color: #0000ff;">var</span> externalUser =<span style="color: #000000;"> result.Principal;
</span><span style="color: #0000ff;">if</span> (externalUser == <span style="color: #0000ff;">null</span><span style="color: #000000;">)
{
    </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> Exception(<span style="color: #800000;">"</span><span style="color: #800000;">External authentication error</span><span style="color: #800000;">"</span><span style="color: #000000;">);
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 检索外部用户的声明</span>
<span style="color: #0000ff;">var</span> claims =<span style="color: #000000;"> externalUser.Claims.ToList();

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 尝试确定外部用户的唯一ID - 最常见的声明类型是子声明和NameIdentifier
</span><span style="color: #008000;">//</span><span style="color: #008000;"> 根据外部提供商，可能会使用其他一些声明类型</span>
<span style="color: #0000ff;">var</span> userIdClaim = claims.FirstOrDefault(x =&gt; x.Type ==<span style="color: #000000;"> JwtClaimTypes.Subject);
</span><span style="color: #0000ff;">if</span> (userIdClaim == <span style="color: #0000ff;">null</span><span style="color: #000000;">)
{
    userIdClaim </span>= claims.FirstOrDefault(x =&gt; x.Type ==<span style="color: #000000;"> ClaimTypes.NameIdentifier);
}
</span><span style="color: #0000ff;">if</span> (userIdClaim == <span style="color: #0000ff;">null</span><span style="color: #000000;">)
{
    </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> Exception(<span style="color: #800000;">"</span><span style="color: #800000;">Unknown userid</span><span style="color: #800000;">"</span><span style="color: #000000;">);
}

</span><span style="color: #0000ff;">var</span> externalUserId =<span style="color: #000000;"> userIdClaim.Value;
</span><span style="color: #0000ff;">var</span> externalProvider =<span style="color: #000000;"> userIdClaim.Issuer;

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 使用externalProvider和externalUserId查找您的用户，或者配置新用户</span></pre>
</div>
<p><strong><span style="font-size: 14pt;">清理和登录：</span></strong></p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">为用户发布身份验证Cookie</span>
<span style="color: #0000ff;">await</span><span style="color: #000000;"> HttpContext.SignInAsync(user.SubjectId, user.Username, provider, props, additionalClaims.ToArray());

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 删除外部认证期间使用的临时cookie</span>
<span style="color: #0000ff;">await</span><span style="color: #000000;"> HttpContext.SignOutAsync(IdentityServerConstants.ExternalCookieAuthenticationScheme);

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 验证返回URL并重定向回授权端点或本地页面</span>
<span style="color: #0000ff;">if</span> (_interaction.IsValidReturnUrl(returnUrl) ||<span style="color: #000000;"> Url.IsLocalUrl(returnUrl))
{
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> Redirect(returnUrl);
}

</span><span style="color: #0000ff;">return</span> Redirect(<span style="color: #800000;">"</span><span style="color: #800000;">~/</span><span style="color: #800000;">"</span>);</pre>
</div>
<p><strong><span style="font-size: 14pt;">状态，URL长度和ISecureDataFormat</span></strong></p>
<p>&nbsp;当重定向到外部提供商登录时，客户端应用程序中的频繁状态必须进行往返。 这意味着状态在离开客户端之前被捕获并保存直到用户返回到客户端应用程序。 包括OpenID Connect在内的许多协议都允许将某种状态作为参数传递，作为请求的一部分，身份提供者将在响应中返回该状态。 ASP.NET Core提供的OpenID Connect身份验证处理程序利用了协议的这一功能，这就是它如何实现上面提到的returnUrl功能。</p>
<p>在请求参数中存储状态的问题是请求URL可能会变得太大（超过2000个字符的公共限制）。 OpenID Connect身份验证处理程序的确提供了一个可扩展点，以便将状态存储在服务器中，而不是存储在请求URL中。 你可以通过实现ISecureDataFormat &lt;AuthenticationProperties&gt;并在OpenIdConnectOptions上配置它来实现这一点。</p>
<p>幸运的是，IdentityServer为您提供了一个实现，并由在DI容器中注册的IDistributedCache实现（例如标准MemoryDistributedCache）支持。 要使用IdentityServer提供的安全数据格式实现，只需在配置DI时在IServiceCollection上调用AddOidcStateDataFormatterCache扩展方法即可。 如果没有参数传递，则所有配置的OpenID Connect处理程序将使用IdentityServer提供的安全数据格式实现：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> ConfigureServices(IServiceCollection services)
{
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 配置OpenIdConnect处理程序以将状态参数保存到服务器端的IDistributedCache中。</span>
<span style="color: #000000;">    services.AddOidcStateDataFormatterCache();

    services.AddAuthentication()
        .AddOpenIdConnect(</span><span style="color: #800000;">"</span><span style="color: #800000;">demoidsrv</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">IdentityServer</span><span style="color: #800000;">"</span>, options =&gt;<span style="color: #000000;">
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> ...</span>
<span style="color: #000000;">        })
        .AddOpenIdConnect(</span><span style="color: #800000;">"</span><span style="color: #800000;">aad</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">Azure AD</span><span style="color: #800000;">"</span>, options =&gt;<span style="color: #000000;">
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> ...</span>
<span style="color: #000000;">        })
        .AddOpenIdConnect(</span><span style="color: #800000;">"</span><span style="color: #800000;">adfs</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">ADFS</span><span style="color: #800000;">"</span>, options =&gt;<span style="color: #000000;">
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> ...</span>
<span style="color: #000000;">        });
}</span></pre>
</div>
<p>如果只配置特定方案，则将这些方案作为参数传递：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> ConfigureServices(IServiceCollection services)
{
    </span><span style="color: #008000;">//</span><span style="color: #008000;">配置OpenIdConnect处理程序以将状态参数保存到服务器端的IDistributedCache中。</span>
    services.AddOidcStateDataFormatterCache(<span style="color: #800000;">"</span><span style="color: #800000;">aad</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">demoidsrv</span><span style="color: #800000;">"</span><span style="color: #000000;">);

    services.AddAuthentication()
        .AddOpenIdConnect(</span><span style="color: #800000;">"</span><span style="color: #800000;">demoidsrv</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">IdentityServer</span><span style="color: #800000;">"</span>, options =&gt;<span style="color: #000000;">
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> ...</span>
<span style="color: #000000;">        })
        .AddOpenIdConnect(</span><span style="color: #800000;">"</span><span style="color: #800000;">aad</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">Azure AD</span><span style="color: #800000;">"</span>, options =&gt;<span style="color: #000000;">
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> ...</span>
<span style="color: #000000;">        })
        .AddOpenIdConnect(</span><span style="color: #800000;">"</span><span style="color: #800000;">adfs</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">ADFS</span><span style="color: #800000;">"</span>, options =&gt;<span style="color: #000000;">
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> ...</span>
<span style="color: #000000;">        });
}</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">六、Windows身份验证<a name="a6"></a></span></strong></p>
<p>在支持的平台上，您可以使用IdentityServer使用Windows身份验证（例如，针对Active Directory）对用户进行身份验证。 当前使用以下命令托管IdentityServer时，Windows身份验证可用：&nbsp;</p>
<ul>
<li>使用IIS和IIS集成包在Windows上使用Kestrel</li>
<li>Windows上的HTTP.sys服务器</li>
</ul>
<p>在这两种情况下，使用方案&ldquo;Windows&rdquo;在HttpContext上使用ChallengeAsync API来触发Windows身份验证。 我们的快速入门UI中的帐户控制器实现了必要的逻辑。<br /><strong><span style="font-size: 14pt;">Using Kestrel</span></strong></p>
<p>使用Kestrel时，必须运行&ldquo;behind&rdquo;IIS并使用IIS integration：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> host = <span style="color: #0000ff;">new</span><span style="color: #000000;"> WebHostBuilder()
    .UseKestrel()
    .UseUrls(</span><span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:5000</span><span style="color: #800000;">"</span><span style="color: #000000;">)
    .UseContentRoot(Directory.GetCurrentDirectory())
    .UseIISIntegration()
    .UseStartup</span>&lt;Startup&gt;<span style="color: #000000;">()
    .Build();</span></pre>
</div>
<p>在使用WebHost.CreateDefaultBuilder方法设置WebHostBuilder时，Kestrel会自动配置。</p>
<p>此外，IIS（或IIS Express）中的虚拟目录必须启用Windows和匿名身份验证。</p>
<p>IIS集成层将Windows身份验证处理程序配置为DI，可以通过身份验证服务调用。 通常在IdentityServer中，建议禁用此自动行为。 这在ConfigureServices中完成：</p>
<div class="cnblogs_code">
<pre>services.Configure&lt;IISOptions&gt;(iis =&gt;<span style="color: #000000;">
{
    iis.AuthenticationDisplayName </span>= <span style="color: #800000;">"</span><span style="color: #800000;">Windows</span><span style="color: #800000;">"</span><span style="color: #000000;">;
    iis.AutomaticAuthentication </span>= <span style="color: #0000ff;">false</span><span style="color: #000000;">;
});</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">七、登出<a name="a7"></a></span></strong></p>
<p>注销IdentityServer就像删除身份验证cookie一样简单，但是为了完成联合注销，我们必须考虑将用户从客户端应用程序（甚至可能是上游身份提供商）中注销。&nbsp;</p>
<p><strong><span style="font-size: 14pt;">删除身份验证Cookie</span></strong></p>
<p>要删除身份验证cookie，只需在HttpContext上使用SignOutAsync扩展方法即可。 您将需要传递使用的方案（由IdentityServerConstants.DefaultCookieAuthenticationScheme提供，除非您已更改它）：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">await</span> HttpContext.SignOutAsync(IdentityServerConstants.DefaultCookieAuthenticationScheme);</pre>
</div>
<p>或者您可以使用IdentityServer提供的便捷扩展方法：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">await</span> HttpContext.SignOutAsync();</pre>
</div>
<p><strong><span style="font-size: 14pt;">通知客户该用户已注销</span></strong></p>
<p>作为注销过程的一部分，您需要确保向客户端应用程序通知用户已注销。 IdentityServer支持服务器端客户端（例如MVC）的前端通道规范，服务器端客户端的后端通道规范（例如MVC）以及基于浏览器的JavaScript客户端的会话管理规范（例如SPA，React，Angular 等）。</p>
<p><strong>前端服务器端客户端</strong></p>
<p>要通过前端通道规范从服务器端客户端应用程序注销用户，IdentityServer中的&ldquo;注销&rdquo;页面必须呈现&lt;iframe&gt;以通知客户端用户已注销。 希望被通知的客户端必须设置FrontChannelLogoutUri配置值。 IdentityServer跟踪用户登录的客户端，并在IIdentityServerInteractionService（详细信息）上提供名为GetLogoutContextAsync的API。 该API返回一个带有SignOutIFrameUrl属性的LogoutRequest对象，您注销的页面必须呈现为&lt;iframe&gt;。</p>
<p><strong>后端服务器端客户端</strong></p>
<p>要通过后端通道规范从服务器端客户端应用程序注销用户，IdentityServer中的SignOutIFrameUrl端点将自动触发服务器到服务器的调用，将签名注销请求传递给客户端。 这意味着即使没有前端通道客户端，IdentityServer中的&ldquo;注销&rdquo;页面也必须如上所述向SignOutIFrameUrl呈现&lt;iframe&gt;。 希望收到通知的客户端必须设置BackChannelLogoutUri配置值。</p>
<p><strong>基于浏览器的JavaScript客户端</strong></p>
<p>鉴于会话管理规范的设计方式，IdentityServer中没有什么特别的，您需要做的是通知这些客户端用户已注销。 但是，客户端必须对check_session_iframe执行监视，并且这由oidc-client JavaScript库实现。</p>
<p><strong><span style="font-size: 14pt;">由客户端应用程序发起的注销</span></strong></p>
<p>如果注销是由客户端应用程序启动的，则客户端首先将用户重定向到最终会话端点。 在会话结束端点进行处理可能需要通过重定向到注销页面来维护一些临时状态（例如，客户端的注销注销重定向uri）。 该状态可能对注销页面有用，并且状态的标识符通过logoutId参数传递到注销页面。</p>
<p>交互服务上的GetLogoutContextAsync API可用于加载状态。ShowSignoutPrompt指示注销请求是否已通过身份验证，&nbsp;因此不会提示用户注销。</p>
<p>默认情况下，此状态作为通过logoutId值传递的受保护数据结构进行管理。 如果您希望在终端会话终端和注销页面之间使用其他持久性，则可以实现IMessageStore &lt;LogoutMessage&gt;并在DI中注册实现。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">八、注销外部身份提供商<a name="a8"></a></span></strong></p>
<p>当用户注销IdentityServer，并且他们使用外部身份提供程序登录时，可能会将其重定向到也注销外部提供程序。 并非所有外部提供商都支持注销，因为它取决于它们支持的协议和功能。</p>
<p>要检测用户必须重定向到外部身份提供者进行注销，通常通过在IdentityServer中使用发布到cookie中的idp声明来完成。 此声明中设置的值是相应身份验证中间件的AuthenticationScheme。 在注销时，咨询此声明以了解是否需要外部注销。&nbsp;</p>
<p>归因于正常注销工作流程已经需要的清理和状态管理，将用户重定向至外部身份提供者是有问题的。 然后在IdentityServer上完成正常注销和清除过程的唯一方法是，然后向外部身份提供者请求在注销后将用户重定向回IdentityServer。 并非所有外部提供商都支持注销后重定向，因为它取决于它们支持的协议和功能。</p>
<p>然后，注销时的工作流程将撤消IdentityServer的身份验证cookie，然后重定向到请求退出后重定向的外部提供程序。 注销后重定向应保持此处所述的必要注销状态（即logoutId参数值）。 要在外部提供者注销后重定向到IdentityServer，在使用ASP.NET Core的SignOutAsync API时，应在AuthenticationProperties上使用RedirectUri，例如：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">[HttpPost]
[ValidateAntiForgeryToken]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task&lt;IActionResult&gt;<span style="color: #000000;"> Logout(LogoutInputModel model)
{
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 构建模型，以便注销页面知道要显示的内容</span>
    <span style="color: #0000ff;">var</span> vm = <span style="color: #0000ff;">await</span><span style="color: #000000;"> _account.BuildLoggedOutViewModelAsync(model.LogoutId);

    </span><span style="color: #0000ff;">var</span> user =<span style="color: #000000;"> HttpContext.User;
    </span><span style="color: #0000ff;">if</span> (user?.Identity.IsAuthenticated == <span style="color: #0000ff;">true</span><span style="color: #000000;">)
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 删除本地认证cookie</span>
        <span style="color: #0000ff;">await</span><span style="color: #000000;"> HttpContext.SignOutAsync();

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 唤起注销事件</span>
        <span style="color: #0000ff;">await</span> _events.RaiseAsync(<span style="color: #0000ff;">new</span><span style="color: #000000;"> UserLogoutSuccessEvent(user.GetSubjectId(), user.GetName()));
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">检查我们是否需要在上游身份提供商处触发注销</span>
    <span style="color: #0000ff;">if</span><span style="color: #000000;"> (vm.TriggerExternalSignout)
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 建立一个返回URL，以便上游提供商将重定向回来
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 在用户注销后给我们。 这可以让我们接下来
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 完成我们的单一注销处理。</span>
        <span style="color: #0000ff;">string</span> url = Url.Action(<span style="color: #800000;">"</span><span style="color: #800000;">Logout</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span> { logoutId =<span style="color: #000000;"> vm.LogoutId });

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 这会触发重定向到外部提供程序以进行注销</span>
        <span style="color: #0000ff;">return</span> SignOut(<span style="color: #0000ff;">new</span> AuthenticationProperties { RedirectUri =<span style="color: #000000;"> url }, vm.ExternalAuthenticationScheme);
    }

    </span><span style="color: #0000ff;">return</span> View(<span style="color: #800000;">"</span><span style="color: #800000;">LoggedOut</span><span style="color: #800000;">"</span><span style="color: #000000;">, vm);
}</span></pre>
</div>
<p>一旦用户注销外部提供者然后重定向，IdentityServer的正常注销处理应该执行，其中涉及处理logoutId并进行所有必要的清理。</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">九、联合注销<a name="a9"></a></span></strong></p>
<p>&nbsp;联合注销是指用户使用外部身份提供程序登录身份服务器的情况，然后，用户通过身份服务器未知的工作流注销该外部标识提供者。当用户注销时,通知身份服务器将非常有用，这样它就可以将用户从标识服务器和所有使用标识服务器的应用程序中注销。</p>
<p>并非所有外部身份提供者都支持联合注销，但是那些这样做的人将提供一种机制来通知客户端用户已经注销了。此通知通常以来自外部身份提供者的&ldquo;注销&rdquo;页面的&lt;iframe&gt;请求的形式出现。然后，IdentityServer必须通知其所有客户端（如此处所述），通常还要从外部身份提供者的&lt;iframe&gt;中以&lt;iframe&gt;的形式发送请求。</p>
<p>使联合注销成为特殊情况（与正常注销相比）的原因是联合注销请求不是IdentityServer中的正常注销端点。 事实上，每个外部IdentityProvider将在您的IdentityServer主机中具有不同的端点。 这是因为每个外部身份提供者可能使用不同的协议，并且每个中间件都在不同的端点上侦听。&nbsp;</p>
<p>所有这些因素的净效应是，没有像我们在正常注销工作流程中那样呈现&ldquo;注销&rdquo;页面，这意味着我们错过了IdentityServer客户端的注销通知。 我们必须为每个这些联合注销端点添加代码，以呈现必要的通知以实现联合注销。</p>
<p>幸运的是，IdentityServer已经包含此代码。 当请求进入IdentityServer并调用外部认证提供程序的处理程序时，IdentityServer会检测这些联合注销请求是否为联合注销请求，如果是，它将自动呈现与此处所述的相同的&lt;iframe&gt;用于注销。 简而言之，自动支持联合注销。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">十、联合网关<a name="a10"></a></span></strong></p>
<p>通用架构是所谓的联合网关。 在这种方法中，IdentityServer充当一个或多个外部身份提供者的网关。</p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201807/741594-20180702143926810-627526717.png" alt="" /></p>
<p>该架构具有以下优点</p>
<ul class="simple">
<li>你的应用程序只需要知道一个令牌服务（网关），并且不需要关于连接到外部提供者的所有细节。 这也意味着您可以添加或更改这些外部提供程序，而无需更新您的应用程序。</li>
<li>
<p>您控制网关（而不是某些外部服务提供商） - 这意味着您可以对其进行任何更改，并保护您的应用程序免受外部提供程序可能对其自己的服务所做的更改。</p>
</li>
<li>大多数外部提供商仅支持一组固定的声明和声明类型 - 在中间具有网关允许对提供商的响应进行后处理以转换/添加/修改特定于域的身份信息。</li>
<li>某些提供商不支持访问令牌（例如社交提供商） - 因为网关知道您的API，它可以根据外部身份发出访问令牌。</li>
<li>有些提供商会根据您连接到的应用程序的数量收费。 网关充当外部提供程序的单个应用程序。 在内部，您可以根据需要连接任意数量的应用程序。</li>
<li>一些提供商使用专有协议或对标准协议进行专有修改 - 对于网关，您只需要处理一个地方。</li>
<li>强制每个身份验证（内部或外部）通过一个地方为身份映射提供极大的灵活性，为您的所有应用程序提供稳定的身份并处理新的需求</li>
</ul>
<p>换句话说 - 拥有您的联合网关可以让您对您的身份基础架构进行很多控制。 由于您的用户身份是您最重要的资产之一，我们建议您控制网关。</p>
<p>我们的快速入门UI使用了以下一些功能。 还请查看外部认证快速入门和有关外部提供商的文档。</p>
<ul class="simple">
<li>您可以通过向IdentityServer应用程序添加身份验证处理程序来添加对外部身份提供程序的支持。</li>
<li>您可以通过调用IAuthenticationSchemeProvider以编程方式查询这些外部提供程序。 这允许根据注册的外部提供商动态呈现您的登录页面。</li>
<li>我们的客户端配置模型允许以每个客户端为基础限制可用的提供者（使用IdentityProviderRestrictions属性）。</li>
<li>您也可以使用客户端上的EnableLocalLogin属性来告诉您的UI是否应呈现用户名/密码输入。</li>
<li>我们的快速入门用户界面通过单个回调来引导所有外部认证调用（请参阅AccountController类中的ExternalLoginCallback）。 这允许单点进行后处理。</li>
</ul>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">十一、Consent<a name="a11"></a></span></strong></p>
<p>在授权请求期间，如果IdentityServer需要用户同意，则浏览器将被重定向到同意页面。&nbsp;</p>
<p>同意用于允许最终用户授予客户端对资源（身份或API）的访问权限。 这通常只对第三方客户端是必需的，并且可以在客户端设置上对每个客户端启用/禁用。</p>
<p><strong><span style="font-size: 14pt;">Consent页面</span></strong></p>
<p>为了让用户同意，托管应用程序必须提供同意页面。 快速入门UI具有同意页面的基本实现。</p>
<p>同意页面通常呈现当前用户的显示名称，请求访问的客户端的显示名称，客户端的徽标，有关客户端的更多信息的链接以及客户端请求访问的资源列表。 允许用户表明他们的同意应该被&ldquo;记住&rdquo;，以便将来不会再为相同的客户再次提示他们也是常见的。</p>
<p>一旦用户提供了同意，同意页面必须通知IdentityServer同意，然后浏览器必须重定向回授权端点。</p>
<p><strong><span style="font-size: 14pt;">授权上下文</span></strong></p>
<p>IdentityServer将传递一个returnUrl参数（<a href="https://identityserver4.readthedocs.io/en/release/reference/options.html#refoptions" target="_blank">可在用户交互选项上配置</a>）到包含授权请求参数的同意页面。 这些参数提供了同意页面的上下文，并且可以在交互服务的帮助下阅读。 GetAuthorizationContextAsync API将返回AuthorizationRequest的一个实例。</p>
<p>可以使用IClientStore和IResourceStore接口获取有关客户端或资源的其他详细信息。</p>
<p><strong><span style="font-size: 14pt;">向IdentityServer通知同意结果</span></strong></p>
<p>交互服务上的GrantConsentAsync API允许同意页面通知IdentityServer同意的结果（也可能是拒绝客户端访问）。</p>
<p>IdentityServer将暂时持久同意的结果。 这个持久性默认使用cookie，因为它只需保存足够长的时间以将结果传递回授权端点。 此临时持久性与用于&ldquo;记住我的同意&rdquo;功能的持久性不同（并且它是持久存储用户的&ldquo;记住我的同意&rdquo;的授权端点）。 如果您希望在许可页面和授权重定向之间使用其他持久性，则可以实现IMessageStore &lt;ConsentResponse&gt;并在DI中注册实现。</p>
<p><strong><span style="font-size: 14pt;">将用户返回到授权端点</span></strong></p>
<p>一旦同意页面通知了IdentityServer的结果，用户可以被重定向回returnUrl。 您的同意页面应通过验证returnUrl是否有效来防止打开重定向。 这可以通过在交互服务上调用IsValidReturnUrl来完成。 此外，如果GetAuthorizationContextAsync返回非null结果，那么您还可以信任returnUrl有效。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">十二、保护APIs<a name="a12"></a></span></strong></p>
<p>IdentityServer默认以JWT（JSON Web令牌）格式发出访问令牌。&nbsp;</p>
<p>今天的每个相关平台都支持验证JWT令牌，这里可以找到一个很好的JWT库列表：</p>
<ul class="simple">
<li><a class="reference external" href="https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.JwtBearer/">JWT bearer authentication handler</a>&nbsp;for ASP.NET Core</li>
<li><a class="reference external" href="https://www.nuget.org/packages/Microsoft.Owin.Security.Jwt">JWT bearer authentication middleware</a>&nbsp;for Katana</li>
<li><a class="reference external" href="https://identityserver.github.io/Documentation/docsv2/consuming/overview.html">IdentityServer authentication middleware</a>&nbsp;for Katana</li>
<li><a class="reference external" href="https://www.npmjs.com/package/jsonwebtoken">jsonwebtoken</a>&nbsp;for nodejs</li>
</ul>
<p>保护基于ASP.NET Core的API只是在DI中配置JWT承载身份验证处理程序，并将身份验证中间件添加到管道：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Startup
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> ConfigureServices(IServiceCollection services)
    {
        services.AddMvc();

        services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
            .AddJwtBearer(options </span>=&gt;<span style="color: #000000;">
            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;"> base-address of your identityserver</span>
                options.Authority = <span style="color: #800000;">"</span><span style="color: #800000;">https://demo.identityserver.io</span><span style="color: #800000;">"</span><span style="color: #000000;">;

                </span><span style="color: #008000;">//</span><span style="color: #008000;"> name of the API resource</span>
                options.Audience = <span style="color: #800000;">"</span><span style="color: #800000;">api1</span><span style="color: #800000;">"</span><span style="color: #000000;">;
            });
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configure(IApplicationBuilder app, ILoggerFactory loggerFactory)
    {
        app.UseAuthentication();
        app.UseMvc();
    }
}</span></pre>
</div>
<p><strong><span style="font-size: 14pt;">IdentityServer身份验证处理程序</span></strong></p>
<p>我们的身份验证处理程序与上述处理程序具有相同的用途（实际上它在内部使用Microsoft JWT库），但添加了一些附加功能：</p>
<ul class="simple">
<li>支持JWTs和引用令牌</li>
<li>用于引用标记的可扩展缓存</li>
<li>统一配置模型</li>
<li>scope验证</li>
</ul>
<p>对于最简单的情况，我们的处理程序配置与上面的代码片段非常相似：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Startup
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> ConfigureServices(IServiceCollection services)
    {
        services.AddMvc();

        services.AddAuthentication(IdentityServerAuthenticationDefaults.AuthenticationScheme)
            .AddIdentityServerAuthentication(options </span>=&gt;<span style="color: #000000;">
            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;"> base-address of your identityserver</span>
                options.Authority = <span style="color: #800000;">"</span><span style="color: #800000;">https://demo.identityserver.io</span><span style="color: #800000;">"</span><span style="color: #000000;">;

                </span><span style="color: #008000;">//</span><span style="color: #008000;"> name of the API resource</span>
                options.ApiName = <span style="color: #800000;">"</span><span style="color: #800000;">api1</span><span style="color: #800000;">"</span><span style="color: #000000;">;
            });
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configure(IApplicationBuilder app, ILoggerFactory loggerFactory)
    {
        app.UseAuthentication();
        app.UseMvc();
    }
}</span></pre>
</div>
<p><strong><span style="font-size: 14pt;">支持参考标记</span></strong></p>
<p>如果传入令牌不是JWT，我们的中间件将调用在发现文档中找到的自省端点以验证该令牌。 由于自检端点需要身份验证，因此您需要提供已配置的API secret，例如：</p>
<div class="cnblogs_code">
<pre>.AddIdentityServerAuthentication(options =&gt;<span style="color: #000000;">
{
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> base-address of your identityserver</span>
    options.Authority = <span style="color: #800000;">"</span><span style="color: #800000;">https://demo.identityserver.io</span><span style="color: #800000;">"</span><span style="color: #000000;">;

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> name of the API resource</span>
    options.ApiName = <span style="color: #800000;">"</span><span style="color: #800000;">api1</span><span style="color: #800000;">"</span><span style="color: #000000;">;
    options.ApiSecret </span>= <span style="color: #800000;">"</span><span style="color: #800000;">secret</span><span style="color: #800000;">"</span><span style="color: #000000;">;
})</span></pre>
</div>
<p>通常，您不希望为每个传入请求执行自检端点的往返。 中间件有一个内置缓存，您可以像这样启用：</p>
<div class="cnblogs_code">
<pre>.AddIdentityServerAuthentication(options =&gt;<span style="color: #000000;">
{
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> base-address of your identityserver</span>
    options.Authority = <span style="color: #800000;">"</span><span style="color: #800000;">https://demo.identityserver.io</span><span style="color: #800000;">"</span><span style="color: #000000;">;

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> name of the API resource</span>
    options.ApiName = <span style="color: #800000;">"</span><span style="color: #800000;">api1</span><span style="color: #800000;">"</span><span style="color: #000000;">;
    options.ApiSecret </span>= <span style="color: #800000;">"</span><span style="color: #800000;">secret</span><span style="color: #800000;">"</span><span style="color: #000000;">;

    options.EnableCaching </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">;
    options.CacheDuration </span>= TimeSpan.FromMinutes(<span style="color: #800080;">10</span>); <span style="color: #008000;">//</span><span style="color: #008000;"> that's the default</span>
})</pre>
</div>
<p>处理程序将使用DI容器中注册的任何IDistributedCache实现（例如，标准MemoryDistributedCache）。</p>
<p><strong><span style="font-size: 14pt;">验证scopes</span></strong></p>
<p>ApiName属性检查令牌是否具有匹配的受众（或短审计）声明。</p>
<p>在IdentityServer中，您还可以将API细分为多个范围。 如果您需要这种粒度，则可以使用ASP.NET Core授权策略系统来检查范围。</p>
<p>制定全局政策：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">services
    .AddMvcCore(options </span>=&gt;<span style="color: #000000;">
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> require scope1 or scope2</span>
        <span style="color: #0000ff;">var</span> policy = ScopePolicy.Create(<span style="color: #800000;">"</span><span style="color: #800000;">scope1</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">scope2</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        options.Filters.Add(</span><span style="color: #0000ff;">new</span><span style="color: #000000;"> AuthorizeFilter(policy));
    })
    .AddJsonFormatters()
    .AddAuthorization();</span></pre>
</div>
<p>撰写范围政策：</p>
<div class="cnblogs_code">
<pre>services.AddAuthorization(options =&gt;<span style="color: #000000;">
{
    options.AddPolicy(</span><span style="color: #800000;">"</span><span style="color: #800000;">myPolicy</span><span style="color: #800000;">"</span>, builder =&gt;<span style="color: #000000;">
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> require scope1</span>
        builder.RequireScope(<span style="color: #800000;">"</span><span style="color: #800000;">scope1</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> and require scope2 or scope3</span>
        builder.RequireScope(<span style="color: #800000;">"</span><span style="color: #800000;">scope2</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">scope3</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    });
});</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">十三、部署<a name="a13"></a></span></strong></p>
<p>您的身份服务器只是一个标准的ASP.NET核心应用程序，包括IdentityServer中间件。 首先阅读有关发布和部署的官方Microsoft文档。&nbsp;</p>
<p><strong><span style="font-size: 14pt;">您的典型架构</span></strong></p>
<p>通常，您将设计IdentityServer部署以实现高可用性：</p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201807/741594-20180702161411158-506915927.png" alt="" /></p>
<p>IdentityServer本身是无状态的，不需要服务器关联 - 但是有些数据需要在实例之间共享。</p>
<p><strong><span style="font-size: 14pt;">配置数据&nbsp;</span></strong></p>
<p>这通常包括：</p>
<ul class="simple">
<li>resources</li>
<li>clients</li>
<li>startup配置</li>
</ul>
<p>存储数据的方式取决于您的环境。 在配置数据很少更改的情况下，我们建议使用内存存储和代码或配置文件。</p>
<p>在高度动态的环境（例如Saas）中，我们建议使用数据库或配置服务动态加载配置。</p>
<p>IdentityServer支持代码配置和配置文件（请参阅此处）。 对于数据库，我们为基于Entity Framework Core的数据库提供支持。</p>
<p>您还可以通过实现IResourceStore和IClientStore来构建自己的配置存储。</p>
<p><strong><span style="font-size: 14pt;">Key material</span></strong></p>
<p>参考：<a href="https://identityserver4.readthedocs.io/en/release/topics/crypto.html#refcrypto" target="_blank">https://identityserver4.readthedocs.io/en/release/topics/crypto.html#refcrypto</a></p>
<p><strong><span style="font-size: 14pt;">运营数据</span></strong></p>
<p>对于某些操作，IdentityServer需要持久性存储来保持状态，这包括：</p>
<ul class="simple">
<li>发布授权码</li>
<li>发出引用和刷新令牌</li>
<li>存储同意</li>
</ul>
<p>您可以使用传统数据库来存储运营数据，也可以使用具有持久性功能（如Redis）的缓存。 上面提到的EF核心实施也支持运营数据。</p>
<p>您也可以通过实施IPersistedGrantStore来实现对自定义存储机制的支持 - 默认情况下IdentityServer会注入内存中的版本。</p>
<p><strong><span style="font-size: 14pt;">ASP.NET core数据保护</span></strong></p>
<p>ASP.NET Core本身需要共享key material来保护cookie，状态字符串等敏感数据。请参阅此处的官方文档。</p>
<p>您可以重复使用上述持久性存储之一，也可以使用像共享文件这样的简单文件。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">十四、日志<a name="a14"></a></span></strong></p>
<p>IdentityServer使用ASP.NET Core提供的标准日志记录工具。 <a href="https://docs.microsoft.com/en-us/aspnet/core/fundamentals/logging" target="_blank">Microsoft文档</a>有一个很好的介绍和内置日志记录提供程序的说明。&nbsp;</p>
<p>我们大致遵循Microsoft使用日志级别的准则：</p>
<ul class="simple">
<li><code class="docutils literal notranslate"><span class="pre">Trace</span></code>&nbsp;仅供开发人员解决问题的信息。 这些消息可能包含敏感的应用程序数据（如令牌），不应在生产环境中启用。</li>
<li><code class="docutils literal notranslate"><span class="pre">Debug</span></code>&nbsp;遵循内部流程并理解为什么做出某些决定。 在开发和调试过程中有短期的用处。</li>
<li><code class="docutils literal notranslate"><span class="pre">Information</span></code>&nbsp;用于跟踪应用程序的一般流程。 这些日志通常具有一些长期价值。</li>
<li><code class="docutils literal notranslate"><span class="pre">Warning针对应用程序流程中的异常或意外事件。 这些可能包括错误或其他不会导致应用程序停止的情况，但可能需要进行调查。</span></code></li>
<li><code class="docutils literal notranslate"><span class="pre">Error</span></code>&nbsp;对于无法处理的错误和异常。 示例：协议请求的验证失败。</li>
<li><code class="docutils literal notranslate"><span class="pre">Critical对于需要立即关注的故障。 示例：缺少商店实施，无效的key material......</span></code></li>
</ul>
<p><strong><span style="font-size: 14pt;">Serilog的设置</span></strong></p>
<p><a href="https://serilog.net/" target="_blank">https://serilog.net/</a></p>
<p><strong><span style="font-size: 14pt;">ASP.NET Core 2.0+</span></strong></p>
<p>对于以下配置，您需要Serilog.AspNetCore和Serilog.Sinks.Console包：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
    {
        Console.Title </span>= <span style="color: #800000;">"</span><span style="color: #800000;">IdentityServer4</span><span style="color: #800000;">"</span><span style="color: #000000;">;

        Log.Logger </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> LoggerConfiguration()
            .MinimumLevel.Debug()
            .MinimumLevel.Override(</span><span style="color: #800000;">"</span><span style="color: #800000;">Microsoft</span><span style="color: #800000;">"</span><span style="color: #000000;">, LogEventLevel.Warning)
            .MinimumLevel.Override(</span><span style="color: #800000;">"</span><span style="color: #800000;">System</span><span style="color: #800000;">"</span><span style="color: #000000;">, LogEventLevel.Warning)
            .MinimumLevel.Override(</span><span style="color: #800000;">"</span><span style="color: #800000;">Microsoft.AspNetCore.Authentication</span><span style="color: #800000;">"</span><span style="color: #000000;">, LogEventLevel.Information)
            .Enrich.FromLogContext()
            .WriteTo.Console(outputTemplate: </span><span style="color: #800000;">"</span><span style="color: #800000;">[{Timestamp:HH:mm:ss} {Level}] {SourceContext}{NewLine}{Message:lj}{NewLine}{Exception}{NewLine}</span><span style="color: #800000;">"</span><span style="color: #000000;">, theme: AnsiConsoleTheme.Literate)
            .CreateLogger();

        BuildWebHost(args).Run();
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> IWebHost BuildWebHost(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
    {
        </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> WebHost.CreateDefaultBuilder(args)
                .UseStartup</span>&lt;Startup&gt;<span style="color: #000000;">()
                .UseSerilog()
                .Build();
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">十五、事件<a name="a15"></a></span></strong></p>
<p>日志记录是更低级别的&ldquo;printf&rdquo;样式 - 事件代表有关IdentityServer中某些操作的更高级别信息。 事件是结构化数据，包括事件ID，成功/失败信息，类别和详细信息。 这使查询和分析它们变得很容易，并提取可用于进一步处理的有用信息。</p>
<p>Events work great with event stores like&nbsp;<a class="reference external" href="https://www.elastic.co/webinars/introduction-elk-stack">ELK</a>,&nbsp;<a class="reference external" href="https://getseq.net/">Seq</a>&nbsp;or&nbsp;<a class="reference external" href="https://www.splunk.com/">Splunk</a>.</p>
<p><strong><span style="font-size: 14pt;">发出事件</span></strong></p>
<p>默认情况下不会启用事件 - 但可以在ConfigureServices方法中全局配置，例如：</p>
<div class="cnblogs_code">
<pre>services.AddIdentityServer(options =&gt;<span style="color: #000000;">
{
    options.Events.RaiseSuccessEvents </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">;
    options.Events.RaiseFailureEvents </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">;
    options.Events.RaiseErrorEvents </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">;
});</span></pre>
</div>
<p>要发出一个事件，请使用DI容器中的IEventService并调用RaiseAsync方法，例如：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task&lt;IActionResult&gt;<span style="color: #000000;"> Login(LoginInputModel model)
{
    </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (_users.ValidateCredentials(model.Username, model.Password))
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> issue authentication cookie with subject ID and username</span>
        <span style="color: #0000ff;">var</span> user =<span style="color: #000000;"> _users.FindByUsername(model.Username);
        </span><span style="color: #0000ff;">await</span> _events.RaiseAsync(<span style="color: #0000ff;">new</span><span style="color: #000000;"> UserLoginSuccessEvent(user.Username, user.SubjectId, user.Username));
    }
    </span><span style="color: #0000ff;">else</span><span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">await</span> _events.RaiseAsync(<span style="color: #0000ff;">new</span> UserLoginFailureEvent(model.Username, <span style="color: #800000;">"</span><span style="color: #800000;">invalid credentials</span><span style="color: #800000;">"</span><span style="color: #000000;">));
    }
}</span></pre>
</div>
<p><strong><span style="font-size: 14pt;">自定义sinks</span></strong></p>
<p>我们的默认事件接收器将简单地将事件类序列化为JSON并将其转发给ASP.NET Core日志记录系统。 如果要连接到自定义事件存储，请实现IEventSink接口并将其注册到DI。</p>
<p>以下示例使用Seq发出事件：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SeqEventSink : IEventSink
{
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> Logger _log;

    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> SeqEventSink()
    {
        _log </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> LoggerConfiguration()
            .WriteTo.Seq(</span><span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:5341</span><span style="color: #800000;">"</span><span style="color: #000000;">)
            .CreateLogger();
    }

    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Task PersistAsync(Event evt)
    {
        </span><span style="color: #0000ff;">if</span> (evt.EventType == EventTypes.Success ||<span style="color: #000000;">
            evt.EventType </span>==<span style="color: #000000;"> EventTypes.Information)
        {
            _log.Information(</span><span style="color: #800000;">"</span><span style="color: #800000;">{Name} ({Id}), Details: {@details}</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                evt.Name,
                evt.Id,
                evt);
        }
        </span><span style="color: #0000ff;">else</span><span style="color: #000000;">
        {
            _log.Error(</span><span style="color: #800000;">"</span><span style="color: #800000;">{Name} ({Id}), Details: {@details}</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                evt.Name,
                evt.Id,
                evt);
        }

        </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> Task.CompletedTask;
    }
}</span></pre>
</div>
<p>将Serilog.Sinks.Seq包添加到主机以使上述代码生效。</p>
<p><strong><span style="font-size: 14pt;">内置事件</span></strong></p>
<p>IdentityServer中定义了以下事件：</p>
<p><code class="docutils literal notranslate"><span class="pre">ApiAuthenticationFailureEvent</span></code>&nbsp;&amp;&nbsp;<code class="docutils literal notranslate"><span class="pre">ApiAuthenticationSuccessEvent</span></code></p>
<p>获取用于在自检端点进行成功/失败的API身份验证。</p>
<p><code class="docutils literal notranslate"><span class="pre">ClientAuthenticationSuccessEvent</span></code>&nbsp;&amp;&nbsp;<code class="docutils literal notranslate"><span class="pre">ClientAuthenticationFailureEvent</span></code></p>
<p>获取令牌端点上的成功/失败客户端身份验证。</p>
<p><code class="docutils literal notranslate"><span class="pre">TokenIssuedSuccessEvent</span></code>&nbsp;&amp;&nbsp;<code class="docutils literal notranslate"><span class="pre">TokenIssuedFailureEvent</span></code></p>
<p>获取用于请求标识符、访问标记、刷新标记和授权代码的成功/失败尝试。</p>
<p><code class="docutils literal notranslate"><span class="pre">TokenIntrospectionSuccessEvent</span></code>&nbsp;&amp;&nbsp;<code class="docutils literal notranslate"><span class="pre">TokenIntrospectionFailureEvent</span></code></p>
<p>获取成功的令牌内省请求。</p>
<p><code class="docutils literal notranslate"><span class="pre">TokenRevokedSuccessEvent</span></code></p>
<p>获取成功的令牌撤销请求。</p>
<p><code class="docutils literal notranslate"><span class="pre">UserLoginSuccessEvent</span></code>&nbsp;&amp;&nbsp;<code class="docutils literal notranslate"><span class="pre">UserLoginFailureEvent</span></code></p>
<p>由quickstart UI引发，用于成功/失败的用户登录。</p>
<p><code class="docutils literal notranslate"><span class="pre">UserLogoutSuccessEvent</span></code></p>
<p>获取成功的注销请求。</p>
<p><code class="docutils literal notranslate"><span class="pre">ConsentGrantedEvent</span></code>&nbsp;&amp;&nbsp;<code class="docutils literal notranslate"><span class="pre">ConsentDeniedEvent</span></code></p>
<p>在同意UI中引发。</p>
<p><code class="docutils literal notranslate"><span class="pre">UnhandledExceptionEvent</span></code></p>
<p>获取未处理的异常。</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">十六、Cryptography, Keys and HTTPS<a name="a16"></a></span></strong></p>
<p>IdentityServer依赖于几个加密机制来完成其工作。&nbsp;</p>
<p><strong><span style="font-size: 14pt;">令牌签名和验证</span></strong></p>
<p>IdentityServer需要非对称密钥对来签署和验证JWT。 该密钥对可以是证书/私钥组合或原始RSA密钥。 无论如何，它必须支持带有SHA256的RSA。</p>
<p>加载签名密钥和相应的验证部分由ISigningCredentialStore和IValidationKeysStore的实现完成。 如果您想自定义加载密钥，您可以实现这些接口并使用DI注册它们。</p>
<p>DI构建器扩展有几种方便的方法来设置签名和验证密钥 - <a href="https://identityserver4.readthedocs.io/en/release/topics/startup.html#refstartupkeymaterial" target="_blank">请参阅此处</a>。</p>
<p><strong><span style="font-size: 14pt;">Signing key rollover</span></strong></p>
<p>虽然一次只能使用一个签名键，但是可以为发现文档发布多个验证键。这对于键翻转很有用。</p>
<p>rollover通常如下所示：</p>
<ol class="arabic simple">
<li>您请求/创建新的key material</li>
<li>除了当前的验证密钥之外，还要发布新的验证密钥。 您可以使用AddValidationKeys构建器扩展方法。</li>
<li>所有客户机和api现在都有机会在下次更新发现文档的本地副本时了解新的密钥</li>
<li>在一定时间（例如24小时）之后，所有客户端和API现在应该接受旧密钥材料和新密钥材料</li>
<li>只要你愿意，就可以保留旧的密钥材料，也许你有需要验证的长寿命令牌</li>
<li>当旧密钥材料不再使用时，将其退役</li>
<li>所有客户端和API将在下次更新发现文档的本地副本时&ldquo;忘记&rdquo;旧密钥</li>
</ol>
<p>这要求客户端和API使用发现文档，并且还具有定期刷新其配置的功能。</p>
<p><strong><span style="font-size: 14pt;">数据保护</span></strong></p>
<p>ASP.NET Core中的Cookie身份验证（或MVC中的防伪）使用ASP.NET Core数据保护功能。 根据您的部署方案，这可能需要额外的配置。 有关更多信息，<a href="https://docs.microsoft.com/en-us/aspnet/core/security/data-protection/configuration/overview?view=aspnetcore-2.1&amp;tabs=aspnetcore2x" target="_blank">请参阅Microsoft文档</a>。</p>
<p><strong><span style="font-size: 14pt;">HTTPS</span></strong></p>
<p>我们不强制使用HTTPS，但对于生产来说，它与IdentityServer的每次交互都是强制性的。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">十七、Grant Types<a name="a17"></a></span></strong></p>
<p>授予类型是一种指定客户端如何与IdentityServer交互的方式。 OpenID Connect和OAuth 2规范定义了以下授权类型：&nbsp;</p>
<ul class="simple">
<li>Implicit</li>
<li>Authorization code</li>
<li>Hybrid</li>
<li>Client credentials</li>
<li>Resource owner password</li>
<li>Refresh tokens</li>
<li>Extension grants</li>
</ul>
<p>您可以通过客户端配置上的AllowedGrantTypes属性指定客户端可以使用的授权类型。</p>
<p>客户端可以配置为使用多种授权类型（例如，用于以用户为中心的操作的混合以及用于服务器到服务器通信的客户端凭证）。 GrantTypes类可用于从典型的授予类型组合中进行选择：</p>
<div class="cnblogs_code">
<pre>Client.AllowedGrantTypes = GrantTypes.HybridAndClientCredentials;</pre>
</div>
<p>您也可以手动指定授权类型列表：</p>
<div class="cnblogs_code">
<pre>Client.AllowedGrantTypes =<span style="color: #000000;">
{
    GrantType.Hybrid,
    GrantType.ClientCredentials,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">my_custom_grant_type</span><span style="color: #800000;">"</span><span style="color: #000000;">
};</span></pre>
</div>
<p>如果您想通过浏览器通道传输访问令牌，则还需要明确地在客户端配置上允许使用该令牌：</p>
<div class="cnblogs_code">
<pre>Client.AllowAccessTokensViaBrowser = <span style="color: #0000ff;">true</span>;</pre>
</div>
<p>其余部分，简要介绍授权类型，以及何时使用它们。 还建议您另外阅读相应的规格以更好地理解差异。</p>
<p><strong><span style="font-size: 14pt;">Client credentials</span></strong></p>
<p>这是最简单的授权类型，用于服务器到服务器通信 - 始终代表客户端而不是用户请求令牌。</p>
<p>使用此授权类型，您可以向令牌端点发送令牌请求，并获取代表客户端的访问令牌。 客户端通常必须使用其客户端ID和密钥对令牌端点进行身份验证。</p>
<p><br /><strong><span style="font-size: 14pt;">Resource owner password</span></strong></p>
<p>资源所有者密码授予类型允许通过将用户名和密码发送给令牌端点来代表用户请求令牌。 这就是所谓的&ldquo;非交互式&rdquo;认证，通常不推荐。</p>
<p>通常对于信任应用使用此授权模式，但一般建议是使用implicit或hybrid&nbsp;流程来替代用户身份验证。</p>
<p>查看资源所有者密码快速入门以获取如何使用它的示例。 您还需要提供用于实现IResourceOwnerPasswordValidator接口的用户名/密码验证代码。 你可以在这里找到<a href="https://identityserver4.readthedocs.io/en/release/topics/resource_owner.html#refresourceownerpasswordvalidator" target="_blank">更多</a>关于这个接口的信息。</p>
<p><br /><strong><span style="font-size: 14pt;">Implicit</span></strong></p>
<p>&nbsp;隐式授权类型针对基于浏览器的应用程序进行了优化。 用于仅用户身份验证（服务器端和JavaScript应用程序）或身份验证和访问令牌请求（JavaScript应用程序）。</p>
<p>在隐式流程中，所有令牌都通过浏览器传输，因此不允许刷新令牌等高级功能。</p>
<p><a href="https://identityserver4.readthedocs.io/en/release/quickstarts/3_interactive_login.html#refimplicitquickstart" target="_blank">本快速入门</a>显示了服务端Web应用程序的身份验证，并显示了JavaScript。</p>
<p><br /><strong><span style="font-size: 14pt;">Authorization code</span></strong></p>
<p>授权代码流最初由OAuth 2指定，并提供了一种在反向通道上检索令牌而不是浏览器前端通道的方法。 它也支持客户端认证。</p>
<p>虽然这种授权类型本身是受支持的，但通常建议您将其与身份令牌结合使用，将其转换为所谓的混合流。 混合流程为您提供重要的额外功能，如签名的协议响应</p>
<p><br /><strong><span style="font-size: 14pt;">Hybrid</span></strong></p>
<p>混合流是隐式和授权代码流的组合 - 它使用多个授予类型的组合，最典型的是code id_token。</p>
<p>在混合流中，身份令牌通过浏览器通道传输，并包含签名的协议响应以及授权代码等其他部件的签名。这可以缓解适用于浏览器端的大量攻击。成功验证响应后，使用back-channel来检索访问和刷新令牌。</p>
<p>对于想要检索访问令牌（也可能是刷新令牌）的本地应用程序，这是推荐的流程，用于服务器端Web应用程序和本地桌面/移动应用程序。</p>
<p><a href="https://identityserver4.readthedocs.io/en/release/quickstarts/5_hybrid_and_api_access.html#refhybridquickstart" target="_blank">查看此快速入门以获取有关在MVC中使用混合流的更多信息</a>。</p>
<p><br /><strong><span style="font-size: 14pt;">Refresh tokens</span></strong></p>
<p>刷新令牌允许获得API的长期访问权限。</p>
<p>刷新令牌允许请求新的访问令牌，而无需用户交互。 每次客户端刷新令牌时，都需要对IdentityServer进行（认证）后向通道调用。 这允许检查刷新标记是否仍然有效，或者在此期间已被撤销。</p>
<p>在混合、授权代码和资源所有者密码流中支持刷新令牌。要请求刷新令牌，客户端需要在令牌请求中包含offline_access范围(并且必须被授权请求该范围)。</p>
<p><br /><strong><span style="font-size: 14pt;">Extension grants</span></strong></p>
<p>扩展授予允许使用新的授予类型扩展令牌端点。有关更多细节，<a href="https://identityserver4.readthedocs.io/en/release/topics/extension_grants.html#refextensiongrants" target="_blank">请参见本文</a>。</p>
<p><br /><strong><span style="font-size: 14pt;">Incompatible grant types</span></strong></p>
<p>禁止一些授权类型组合：</p>
<ul class="simple">
<li>混合隐式和授权代码或混合将允许从更安全的基于代码的流降级攻击到隐式攻击。</li>
<li>允许授权码和混合模式两者同样令人担忧</li>












</ul>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">十八、Secrets<a name="a18"></a></span></strong></p>
<p>secret解析和验证是身份服务器中的可扩展点，开箱即用它支持共享secret以及通过基本身份验证头或POST主体传输共享secret。</p>
<p><strong><span style="font-size: 14pt;">创建一个共享的secret</span></strong></p>
<p>以下代码设置了散列共享密钥：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> secret = <span style="color: #0000ff;">new</span> Secret(<span style="color: #800000;">"</span><span style="color: #800000;">secret</span><span style="color: #800000;">"</span>.Sha256());</pre>
</div>
<p>这个密钥现在可以分配给客户端或ApiResource。 请注意，两者不仅支持单个秘密，而且还支持多个密钥。 这对密钥翻转和旋转很有用：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> client = <span style="color: #0000ff;">new</span><span style="color: #000000;"> Client
{
    ClientId </span>= <span style="color: #800000;">"</span><span style="color: #800000;">client</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    ClientSecrets </span>= <span style="color: #0000ff;">new</span> List&lt;Secret&gt;<span style="color: #000000;"> { secret },

    AllowedGrantTypes </span>=<span style="color: #000000;"> GrantTypes.ClientCredentials,
    AllowedScopes </span>= <span style="color: #0000ff;">new</span> List&lt;<span style="color: #0000ff;">string</span>&gt;<span style="color: #000000;">
    {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">api1</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">api2</span><span style="color: #800000;">"</span><span style="color: #000000;">
    }
};</span></pre>
</div>
<p>实际上，您也可以为密钥分配说明和到期日期。 描述将用于日志记录，以及执行密钥生命周期的截止日期：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> secret = <span style="color: #0000ff;">new</span><span style="color: #000000;"> Secret(
    </span><span style="color: #800000;">"</span><span style="color: #800000;">secret</span><span style="color: #800000;">"</span><span style="color: #000000;">.Sha256(),
    </span><span style="color: #800000;">"</span><span style="color: #800000;">2016 secret</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #0000ff;">new</span> DateTime(<span style="color: #800080;">2016</span>, <span style="color: #800080;">12</span>, <span style="color: #800080;">31</span>));</pre>
</div>
<p><strong><span style="font-size: 14pt;">使用共享密钥进行身份验证</span></strong></p>
<p>您可以将客户端ID /secret组合作为POST正文的一部分发送：</p>
<div class="cnblogs_code">
<pre>POST /connect/<span style="color: #000000;">token

client_id</span>=client1&amp;<span style="color: #000000;">
client_secret</span>=secret&amp;<span style="color: #000000;">
...</span></pre>
</div>
<p>..或作为basic身份验证头：</p>
<div class="cnblogs_code">
<pre>POST /connect/<span style="color: #000000;">token

Authorization: Basic xxxxx

...</span></pre>
</div>
<p>您可以使用以下C＃代码手动创建basic身份验证头：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> credentials = <span style="color: #0000ff;">string</span>.Format(<span style="color: #800000;">"</span><span style="color: #800000;">{0}:{1}</span><span style="color: #800000;">"</span><span style="color: #000000;">, clientId, clientSecret);
</span><span style="color: #0000ff;">var</span> headerValue =<span style="color: #000000;"> Convert.ToBase64String(Encoding.UTF8.GetBytes(credentials));

</span><span style="color: #0000ff;">var</span> client = <span style="color: #0000ff;">new</span><span style="color: #000000;"> HttpClient();
client.DefaultRequestHeaders.Authorization </span>= <span style="color: #0000ff;">new</span> AuthenticationHeaderValue(<span style="color: #800000;">"</span><span style="color: #800000;">Basic</span><span style="color: #800000;">"</span>, headerValue);</pre>
</div>
<p>IdentityModel库具有名为TokenClient和IntrospectionClient的辅助类，它们封装了身份验证和协议消息。</p>
<p><strong><span style="font-size: 14pt;">除了共享secret</span></strong></p>
<p>还有其他技术来验证客户端，例如 基于公钥/私钥加密。 IdentityServer包括对私钥JWT客户机密钥的支持（请参阅RFC 7523）。</p>
<p>secret可扩展性通常包含三件事：</p>
<ul class="simple">
<li>一个secret的定义</li>
<li>一个知道如何从传入请求中提取secret的secret解析器</li>
<li>一个secret验证器，知道如何根据定义验证解析的secret</li>
</ul>
<p>secret解析器和验证器是ISecretParser和ISecretValidator接口的实现。 要使它们可用于IdentityServer，您需要将它们注册到DI容器，例如：</p>
<div class="cnblogs_code">
<pre>builder.AddSecretParser&lt;ClientAssertionSecretParser&gt;<span style="color: #000000;">()
builder.AddSecretValidator</span>&lt;PrivateKeyJwtSecretValidator&gt;()</pre>
</div>
<p>我们的默认私钥JWTsecret验证器期望完整的(leaf)证书作为secret定义上的base64。然后，该证书将用于验证自签名JWT上的签名，例如：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> client = <span style="color: #0000ff;">new</span><span style="color: #000000;"> Client
{
    ClientId </span>= <span style="color: #800000;">"</span><span style="color: #800000;">client.jwt</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    ClientSecrets </span>=<span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> Secret
        {
            Type </span>=<span style="color: #000000;"> IdentityServerConstants.SecretTypes.X509CertificateBase64,
            Value </span>= <span style="color: #800000;">"</span><span style="color: #800000;">MIIDATCCAe2gAwIBAgIQoHUYAquk9rBJcq8W+F0FAzAJBgUrDgMCHQUAMBIxEDAOBgNVBAMTB0RldlJvb3QwHhcNMTAwMTIwMjMwMDAwWhcNMjAwMTIwMjMwMDAwWjARMQ8wDQYDVQQDEwZDbGllbnQwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQDSaY4x1eXqjHF1iXQcF3pbFrIbmNw19w/IdOQxbavmuPbhY7jX0IORu/GQiHjmhqWt8F4G7KGLhXLC1j7rXdDmxXRyVJBZBTEaSYukuX7zGeUXscdpgODLQVay/0hUGz54aDZPAhtBHaYbog+yH10sCXgV1Mxtzx3dGelA6pPwiAmXwFxjJ1HGsS/hdbt+vgXhdlzud3ZSfyI/TJAnFeKxsmbJUyqMfoBl1zFKG4MOvgHhBjekp+r8gYNGknMYu9JDFr1ue0wylaw9UwG8ZXAkYmYbn2wN/CpJl3gJgX42/9g87uLvtVAmz5L+rZQTlS1ibv54ScR2lcRpGQiQav/LAgMBAAGjXDBaMBMGA1UdJQQMMAoGCCsGAQUFBwMCMEMGA1UdAQQ8MDqAENIWANpX5DZ3bX3WvoDfy0GhFDASMRAwDgYDVQQDEwdEZXZSb290ghAsWTt7E82DjU1E1p427Qj2MAkGBSsOAwIdBQADggEBADLje0qbqGVPaZHINLn+WSM2czZk0b5NG80btp7arjgDYoWBIe2TSOkkApTRhLPfmZTsaiI3Ro/64q+Dk3z3Kt7w+grHqu5nYhsn7xQFAQUf3y2KcJnRdIEk0jrLM4vgIzYdXsoC6YO+9QnlkNqcN36Y8IpSVSTda6gRKvGXiAhu42e2Qey/WNMFOL+YzMXGt/nDHL/qRKsuXBOarIb++43DV3YnxGTx22llhOnPpuZ9/gnNY7KLjODaiEciKhaKqt/b57mTEz4jTF4kIg6BP03MUfDXeVlM1Qf1jB43G2QQ19n5lUiqTpmQkcfLfyci2uBZ8BkOhXr3Vk9HIk/xBXQ=</span><span style="color: #800000;">"</span><span style="color: #000000;">
        }
    },

    AllowedGrantTypes </span>=<span style="color: #000000;"> GrantTypes.ClientCredentials,
    AllowedScopes </span>= { <span style="color: #800000;">"</span><span style="color: #800000;">api1</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">api2</span><span style="color: #800000;">"</span><span style="color: #000000;"> }
};</span></pre>
</div>
<p>您可以实现自己的secret验证器（或扩展我们的secret验证器）来实现例如 相反，链信任验证。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">十九、Extension Grants<a name="a19"></a></span></strong></p>
<p>OAuth 2.0定义了令牌端点的标准授权类型，例如password，authorization_code和refresh_token。 扩展授权是一种添加对非标准令牌颁发方案（如令牌转换，委派或自定义凭据）的支持的方法。</p>
<p>您可以通过实现IExtensionGrantValidator接口来添加对其他授权类型的支持：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IExtensionGrantValidator
{
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
    <span style="color: #808080;">///</span><span style="color: #008000;"> Handles the custom grant request.
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
    <span style="color: #808080;">///</span> <span style="color: #808080;">&lt;param name="request"&gt;</span><span style="color: #008000;">The validation context.</span><span style="color: #808080;">&lt;/param&gt;</span>
<span style="color: #000000;">    Task ValidateAsync(ExtensionGrantValidationContext context);

    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
    <span style="color: #808080;">///</span><span style="color: #008000;"> Returns the grant type this validator can deal with
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
    <span style="color: #808080;">///</span> <span style="color: #808080;">&lt;value&gt;</span>
    <span style="color: #808080;">///</span><span style="color: #008000;"> The type of the grant.
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/value&gt;</span>
    <span style="color: #0000ff;">string</span> GrantType { <span style="color: #0000ff;">get</span><span style="color: #000000;">; }
}</span></pre>
</div>
<p>他的ExtensionGrantValidationContext对象使您可以访问：</p>
<ul class="simple">
<li>传入令牌请求 - 众所周知的验证值，以及任何自定义值（通过Raw集合）</li>
<li>结果 - 错误或成功</li>
<li>自定义响应参数</li>
</ul>
<p>要注册扩展授权，请将其添加到DI：</p>
<div class="cnblogs_code">
<pre>builder.AddExtensionGrantValidator&lt;MyExtensionsGrantValidator&gt;();</pre>
</div>
<p><strong><span style="font-size: 14pt;">示例：使用扩展授权进行简单委派</span></strong></p>
<p>想象一下以下场景 - 前端客户端使用通过交互流（例如混合流）获取的令牌来调用中间层API。 此中间层API（API 1）现在希望代表交互式用户调用后端API（API 2）：</p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201807/741594-20180703192715769-409338229.png" alt="" width="596" height="281" /></p>
<p>换句话说，中间层API（API 1）需要包含用户身份的访问令牌，但需要具有后端API（API 2）的scope。</p>
<p><strong>实施扩展授权</strong>&nbsp;</p>
<p>前端会将令牌发送到API 1，现在需要在IdentityServer上使用API 2的新令牌交换此令牌。</p>
<p>在线上，对交换的令牌服务的调用可能如下所示：</p>
<div class="cnblogs_code">
<pre>POST /connect/<span style="color: #000000;">token

grant_type</span>=delegation&amp;<span style="color: #000000;">
scope</span>=api2&amp;<span style="color: #000000;">
token</span>=...&amp;<span style="color: #000000;">
client_id</span>=<span style="color: #000000;">api1.client
client_secret</span>=secret</pre>
</div>
<p>扩展授权验证程序的工作是通过验证传入令牌并返回表示新令牌的结果来处理该请求：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> DelegationGrantValidator : IExtensionGrantValidator
{
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> ITokenValidator _validator;

    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> DelegationGrantValidator(ITokenValidator validator)
    {
        _validator </span>=<span style="color: #000000;"> validator;
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> GrantType =&gt; <span style="color: #800000;">"</span><span style="color: #800000;">delegation</span><span style="color: #800000;">"</span><span style="color: #000000;">;

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span><span style="color: #000000;"> Task ValidateAsync(ExtensionGrantValidationContext context)
    {
        </span><span style="color: #0000ff;">var</span> userToken = context.Request.Raw.Get(<span style="color: #800000;">"</span><span style="color: #800000;">token</span><span style="color: #800000;">"</span><span style="color: #000000;">);

        </span><span style="color: #0000ff;">if</span> (<span style="color: #0000ff;">string</span><span style="color: #000000;">.IsNullOrEmpty(userToken))
        {
            context.Result </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> GrantValidationResult(TokenRequestErrors.InvalidGrant);
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;">;
        }

        </span><span style="color: #0000ff;">var</span> result = <span style="color: #0000ff;">await</span><span style="color: #000000;"> _validator.ValidateAccessTokenAsync(userToken);
        </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (result.IsError)
        {
            context.Result </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> GrantValidationResult(TokenRequestErrors.InvalidGrant);
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;">;
        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> get user's identity</span>
        <span style="color: #0000ff;">var</span> sub = result.Claims.FirstOrDefault(c =&gt; c.Type == <span style="color: #800000;">"</span><span style="color: #800000;">sub</span><span style="color: #800000;">"</span><span style="color: #000000;">).Value;

        context.Result </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> GrantValidationResult(sub, GrantType);
        </span><span style="color: #0000ff;">return</span><span style="color: #000000;">;
    }
}</span></pre>
</div>
<p>不要忘记在DI上注册验证器。</p>
<p><strong>注册委托客户端</strong></p>
<p>您需要在IdentityServer中进行客户端注册，以允许客户端使用此新的扩展授权，例如：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> client = <span style="color: #0000ff;">new</span><span style="color: #000000;"> client
{
    ClientId </span>= <span style="color: #800000;">"</span><span style="color: #800000;">api1.client</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    ClientSecrets </span>= <span style="color: #0000ff;">new</span> List&lt;Secret&gt;<span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">new</span> Secret(<span style="color: #800000;">"</span><span style="color: #800000;">secret</span><span style="color: #800000;">"</span><span style="color: #000000;">.Sha256())
    },

    AllowedGrantTypes </span>= { <span style="color: #800000;">"</span><span style="color: #800000;">delegation</span><span style="color: #800000;">"</span><span style="color: #000000;"> },

    AllowedScopes </span>= <span style="color: #0000ff;">new</span> List&lt;<span style="color: #0000ff;">string</span>&gt;<span style="color: #000000;">
    {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">api2</span><span style="color: #800000;">"</span><span style="color: #000000;">
    }
}</span></pre>
</div>
<p><strong>调用令牌端点</strong></p>
<p>在API 1中，您现在可以自己构建HTTP有效内容，或使用IdentityModel帮助程序库：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task&lt;TokenResponse&gt; DelegateAsync(<span style="color: #0000ff;">string</span><span style="color: #000000;"> userToken)
{
    </span><span style="color: #0000ff;">var</span> payload = <span style="color: #0000ff;">new</span><span style="color: #000000;">
    {
        token </span>=<span style="color: #000000;"> userToken
    };

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> create token client</span>
    <span style="color: #0000ff;">var</span> client = <span style="color: #0000ff;">new</span> TokenClient(disco.TokenEndpoint, <span style="color: #800000;">"</span><span style="color: #800000;">api1.client</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">secret</span><span style="color: #800000;">"</span><span style="color: #000000;">);

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> send custom grant to token endpoint, return response</span>
    <span style="color: #0000ff;">return</span> <span style="color: #0000ff;">await</span> client.RequestCustomGrantAsync(<span style="color: #800000;">"</span><span style="color: #800000;">delegation</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">api2</span><span style="color: #800000;">"</span><span style="color: #000000;">, payload);
}</span></pre>
</div>
<p>TokenResponse.AccessToken现在将包含委托访问令牌。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">二十、Resource Owner Password Validation<a name="a20"></a></span></strong></p>
<p>如果要使用OAuth 2.0资源所有者密码凭据授权（也称为密码），则需要实现并注册IResourceOwnerPasswordValidator接口：&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IResourceOwnerPasswordValidator
{
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
    <span style="color: #808080;">///</span><span style="color: #008000;"> Validates the resource owner password credential
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
    <span style="color: #808080;">///</span> <span style="color: #808080;">&lt;param name="context"&gt;</span><span style="color: #008000;">The context.</span><span style="color: #808080;">&lt;/param&gt;</span>
<span style="color: #000000;">    Task ValidateAsync(ResourceOwnerPasswordValidationContext context);
}</span></pre>
</div>
<p>在上下文中，您将找到已解析的协议参数，如UserName和Password，如果您想查看其他输入数据，还可以找到原始请求。</p>
<p>然后，您的工作是实施密码验证并相应地在上下文中设置结果。 请参阅<a href="https://identityserver4.readthedocs.io/en/release/reference/grant_validation_result.html#refgrantvalidationresult" target="_blank">GrantValidationResult</a>文档。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">二十一、Refresh Tokens<a name="a21"></a></span></strong></p>
<p>由于访问令牌的生命周期有限，因此刷新令牌允许在没有用户交互的情况下请求新的访问令牌。&nbsp;</p>
<p>以下流程支持刷新令牌：authorization code, hybrid 和resource owner password凭据流。 需要明确授权客户端通过将AllowOfflineAccess设置为true来请求刷新令牌。</p>
<p><strong><span style="font-size: 14pt;">其他客户端设置</span></strong></p>
<p><strong><code class="docutils literal notranslate"><span class="pre">AbsoluteRefreshTokenLifetime</span></code></strong></p>
<p>刷新令牌的最长生命周期，以秒为单位。 默认为2592000秒/ 30天。&nbsp;Zero与RefreshTokenExpiration = Sliding一起使用时永不过期的刷新令牌</p>
<p><strong><code class="docutils literal notranslate"><span class="pre">SlidingRefreshTokenLifetime</span></code></strong></p>
<p>刷新令牌的生命周期以秒为单位。 默认为1296000秒/ 15天</p>
<p><strong><code class="docutils literal notranslate"><span class="pre">RefreshTokenUsage</span></code></strong></p>
<p class="first"><code class="docutils literal notranslate"><span class="pre">ReUse</span></code>&nbsp;刷新令牌时刷新令牌句柄将保持不变</p>
<p class="last"><code class="docutils literal notranslate"><span class="pre">OneTime</span></code>&nbsp;刷新令牌时将更新刷新令牌句柄</p>
<p><strong><code class="docutils literal notranslate"><span class="pre">RefreshTokenExpiration</span></code></strong></p>
<p class="first"><code class="docutils literal notranslate"><span class="pre">Absolute刷新令牌将在固定时间点到期（由AbsoluteRefreshTokenLifetime指定）</span></code></p>
<p class="last"><code class="docutils literal notranslate"><span class="pre">Sliding</span></code>&nbsp;刷新令牌时，将刷新刷新令牌的生命周期（按SlidingRefreshTokenLifetime中指定的数量）。 生命周期不会超过AbsoluteRefreshTokenLifetime。</p>
<p><strong><code class="docutils literal notranslate"><span class="pre">UpdateAccessTokenClaimsOnRefresh</span></code></strong></p>
<p>获取或设置一个值，该值指示是否应在刷新令牌请求上更新访问令牌（及其声明）。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">二十二、Reference Tokens<a name="a22"></a></span></strong></p>
<p>访问令牌可以有两种形式 - 自包含或引用。&nbsp;</p>
<p>JWT令牌将是一个自包含的访问令牌 - 它是一个带有声明和过期的受保护数据结构。 一旦API了解了密钥材料，它就可以验证自包含的令牌，而无需与发行者进行通信。 这使得JWT难以撤销。 它们将一直有效，直到它们过期。</p>
<p>使用引用令牌时 - IdentityServer会将令牌的内容存储在数据存储中，并且只会将此令牌的唯一标识符发回给客户端。 接收此引用的API必须打开与IdentityServer的反向通道通信以验证令牌。</p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201807/741594-20180703200824124-132322519.png" alt="" /></p>
<p>您可以使用以下设置切换客户端的令牌类型：</p>
<div class="cnblogs_code">
<pre>client.AccessTokenType = AccessTokenType.Reference;</pre>
</div>
<p>IdentityServer提供了OAuth 2.0 introspection&nbsp;规范的实现，该规范允许API取消引用令牌。 您可以使用我们的专用introspection&nbsp;中间件或使用身份服务器身份验证中间件，它可以验证JWT和引用令牌。</p>
<p>introspection&nbsp;端点需要身份验证 - 因为introspection&nbsp;端点的客户端是API，您可以在ApiResource上配置密码：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> api = <span style="color: #0000ff;">new</span> ApiResource(<span style="color: #800000;">"</span><span style="color: #800000;">api1</span><span style="color: #800000;">"</span><span style="color: #000000;">)
{
    ApiSecrets </span>= { <span style="color: #0000ff;">new</span> Secret(<span style="color: #800000;">"</span><span style="color: #800000;">secret</span><span style="color: #800000;">"</span><span style="color: #000000;">.Sha256()) }
}</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">二十三、CORS<a name="a23"></a></span></strong></p>
<p>IdentityServer中的许多端点将通过基于JavaScript的客户端的Ajax调用进行访问。 鉴于IdentityServer最有可能托管在与这些客户端不同的源上，这意味着需要配置跨源资源共享（CORS）。&nbsp;</p>
<p><strong><span style="font-size: 14pt;">基于客户端的CORS配置</span></strong></p>
<p>配置CORS的一种方法是在客户端配置上使用AllowedCorsOrigins集合。 只需将客户端的原点添加到集合中，IdentityServer中的默认配置将查询这些值以允许来自源的跨源调用。</p>
<p>配置CORS时，请务必使用origin（不是URL）。 例如：https://foo:123/是一个URL，而https://foo:123是一个origin。</p>
<p>如果您使用我们提供的&ldquo;in-memory&rdquo;或基于EF的客户端配置，则将使用此默认CORS实现。 如果您定义自己的IClientStore，那么您将需要实现自己的自定义CORS策略服务（参见下文）。</p>
<p><strong><span style="font-size: 14pt;">自定义Cors策略服务</span></strong></p>
<p>IdentityServer允许托管应用程序实现ICorsPolicyService以完全控制CORS策略。</p>
<p>要实现的唯一方法是：Task&lt;bool&gt; IsOriginAllowedAsync(string origin)。 如果允许origin则返回true，否则返回false。</p>
<p>实现后，只需在DI中注册实现，然后IdentityServer将使用您的自定义实现。</p>
<p><strong>DefaultCorsPolicyService</strong></p>
<p>如果您只是希望对一组允许的origin进行硬编码，那么可以使用一个名为DefaultCorsPolicyService的预构建的ICorsPolicyService实现。 这将在DI中配置为单例，并使用其AllowedOrigins集合进行硬编码，或将AllowAll标志设置为true以允许所有来源。 例如，在ConfigureServices中：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> cors = <span style="color: #0000ff;">new</span> DefaultCorsPolicyService(_loggerFactory.CreateLogger&lt;DefaultCorsPolicyService&gt;<span style="color: #000000;">())
{
    AllowedOrigins </span>= { <span style="color: #800000;">"</span><span style="color: #800000;">https://foo</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">https://bar</span><span style="color: #800000;">"</span><span style="color: #000000;"> }
};
services.AddSingleton</span>&lt;ICorsPolicyService&gt;(cors);</pre>
</div>
<p>请谨慎使用AllowAll。</p>
<p><strong><span style="font-size: 14pt;">将IdentityServer的CORS策略与ASP.NET Core的CORS策略混合使用</span></strong></p>
<p>dentityServer使用ASP.NET Core的CORS中间件来提供其CORS实现。 托管IdentityServer的应用程序可能还需要CORS用于自己的自定义端点。 通常，两者应该在同一个应用程序中一起工作。</p>
<p>您的代码应使用ASP.NET Core中记录的CORS功能，而不考虑IdentityServer。 这意味着您应该定义策略并正常注册中间件。 如果您的应用程序在ConfigureServices中定义策略，那么这些策略应该继续在您使用它们的相同位置（在您配置CORS中间件的位置或在控制器代码中使用MVC EnableCors属性的位置）。 相反，如果您使用CORS中间件（通过策略构建器回调）定义内联策略，那么它也应该继续正常工作。</p>
<p>如果您决定创建自定义ICorsPolicyProvider，那么在您使用ASP.NET Core CORS服务和IdentityServer之间可能存在冲突的一种情况。 鉴于ASP.NET Core的CORS服务和中间件的设计，IdentityServer实现了自己的自定义ICorsPolicyProvider并将其注册到DI系统中。 幸运的是，IdentityServer实现旨在使用装饰器模式来包装已在DI中注册的任何现有ICorsPolicyProvider。 这意味着你也可以实现ICorsPolicyProvider，但它只需要在DI中的IdentityServer之前注册（例如在ConfigureServices中）。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">二十四、Discovery<a name="a24"></a></span></strong></p>
<p>可以在https://baseaddress/.well-known/openid-configuration找到发现文档。 它包含有关IdentityServer的端点，密钥材料和功能的信息。&nbsp;</p>
<p>默认情况下，所有信息都包含在发现文档中，但通过使用配置选项，您可以隐藏各个部分，例如：</p>
<div class="cnblogs_code">
<pre>services.AddIdentityServer(options =&gt;<span style="color: #000000;">
{
    options.Discovery.ShowIdentityScopes </span>= <span style="color: #0000ff;">false</span><span style="color: #000000;">;
    options.Discovery.ShowApiScopes </span>= <span style="color: #0000ff;">false</span><span style="color: #000000;">;
    options.Discovery.ShowClaims </span>= <span style="color: #0000ff;">false</span><span style="color: #000000;">;
    options.Discovery.ShowExtensionGrantTypes </span>= <span style="color: #0000ff;">false</span><span style="color: #000000;">;
});</span></pre>
</div>
<p><strong><span style="font-size: 14pt;">扩展发现</span></strong></p>
<p>您可以向发现文档添加自定义条目，例如：</p>
<div class="cnblogs_code">
<pre>services.AddIdentityServer(options =&gt;<span style="color: #000000;">
{
    options.Discovery.CustomEntries.Add(</span><span style="color: #800000;">"</span><span style="color: #800000;">my_setting</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">foo</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    options.Discovery.CustomEntries.Add(</span><span style="color: #800000;">"</span><span style="color: #800000;">my_complex_setting</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #0000ff;">new</span><span style="color: #000000;">
        {
            foo </span>= <span style="color: #800000;">"</span><span style="color: #800000;">foo</span><span style="color: #800000;">"</span><span style="color: #000000;">,
            bar </span>= <span style="color: #800000;">"</span><span style="color: #800000;">bar</span><span style="color: #800000;">"</span><span style="color: #000000;">
        });
});</span></pre>
</div>
<p>当您添加以〜开头的自定义值时，它将扩展为IdentityServer基址以下的绝对路径，例如：</p>
<div class="cnblogs_code">
<pre>options.Discovery.CustomEntries.Add(<span style="color: #800000;">"</span><span style="color: #800000;">my_custom_endpoint</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">~/custom</span><span style="color: #800000;">"</span>);</pre>
</div>
<p>如果要完全控制发现（和jwks）文档的呈现，可以实现IDiscoveryResponseGenerator接口（或从我们的默认实现派生）。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">二十五、Adding more API Endpoints<a name="a25"></a></span></strong></p>
<p>您可以向托管IdentityServer4的应用程序添加更多API端点。</p>
<p>您通常希望通过它们所托管的IdentityServer实例来保护这些API。这不是问题。 只需将令牌验证处理程序添加到主机（<a href="https://identityserver4.readthedocs.io/en/release/topics/apis.html#refprotectingapis" target="_blank">请参阅此处</a>）：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> ConfigureServices(IServiceCollection services)
{
    services.AddMvc();

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> details omitted</span>
<span style="color: #000000;">    services.AddIdentityServer();

    services.AddAuthentication()
        .AddIdentityServerAuthentication(</span><span style="color: #800000;">"</span><span style="color: #800000;">token</span><span style="color: #800000;">"</span>, isAuth =&gt;<span style="color: #000000;">
        {
            isAuth.Authority </span>= <span style="color: #800000;">"</span><span style="color: #800000;">base_address_of_identityserver</span><span style="color: #800000;">"</span><span style="color: #000000;">;
            isAuth.ApiName </span>= <span style="color: #800000;">"</span><span style="color: #800000;">name_of_api</span><span style="color: #800000;">"</span><span style="color: #000000;">;
        });
}</span></pre>
</div>
<p>在您的API上，您需要添加[Authorize]属性并显式引用您要使用的身份验证方案（在此示例中这是令牌，但您可以选择您喜欢的任何名称）：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> TestController : ControllerBase
{
    [Route(</span><span style="color: #800000;">"</span><span style="color: #800000;">test</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
    [Authorize(AuthenticationSchemes </span>= <span style="color: #800000;">"</span><span style="color: #800000;">token</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> IActionResult Get()
    {
        </span><span style="color: #0000ff;">var</span> claims = User.Claims.Select(c =&gt; <span style="color: #0000ff;">new</span><span style="color: #000000;"> { c.Type, c.Value }).ToArray();
        </span><span style="color: #0000ff;">return</span> Ok(<span style="color: #0000ff;">new</span> { message = <span style="color: #800000;">"</span><span style="color: #800000;">Hello API</span><span style="color: #800000;">"</span><span style="color: #000000;">, claims });
    }
}</span></pre>
</div>
<p>如果要从浏览器调用该API，则还需要配置CORS。</p>
<p><strong><span style="font-size: 14pt;">发现</span></strong></p>
<p>如果需要，您还可以将端点添加到发现文档中，例如：</p>
<div class="cnblogs_code">
<pre>services.AddIdentityServer(options =&gt;<span style="color: #000000;">
{
    options.Discovery.CustomEntries.Add(</span><span style="color: #800000;">"</span><span style="color: #800000;">custom_endpoint</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">~/api/custom</span><span style="color: #800000;">"</span><span style="color: #000000;">);
})</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">二十六、Adding new Protocols<a name="a26"></a></span></strong></p>
<p>除了对OpenID Connect和OAuth 2.0的内置支持之外，IdentityServer4还允许添加对其他协议的支持。&nbsp;</p>
<p>您可以将这些附加协议端点添加为中间件或使用例如 MVC控制器。 在这两种情况下，您都可以访问ASP.NET Core DI系统，该系统允许重用我们的内部服务，例如访问客户端定义或密钥材料。</p>
<p><a href="https://github.com/IdentityServer/IdentityServer4.WsFederation" target="_blank">可以在此处找到添加WS-Federation支持的示例</a>。</p>
<p><strong><span style="font-size: 14pt;">典型认证工作流程</span></strong></p>
<p>身份验证请求通常如下所示：</p>
<ul class="simple">
<li>身份验证请求到达协议端点</li>
<li>协议端点执行输入验证</li>
<li><dl class="first docutils"><dt>重定向到登录页面，返回URL设置回协议端点（如果用户是匿名的）</dt><dd>
<ul class="first last">
<li>通过IIdentityServerInteractionService访问当前请求详细信息</li>
<li>用户身份验证（本地或通过外部身份验证中间件）</li>
<li>登录用户</li>
<li>重定向回协议端点</li>
</ul>
</dd></dl></li>
<li>创建协议响应（令牌创建和重定向回客户端）</li>
</ul>
<p><strong><span style="font-size: 14pt;">Useful IdentityServer服务</span></strong></p>
<p>要实现上述工作流程，需要与IdentityServer建立一些交互点。</p>
<p><strong>访问配置并重定向到登录页面</strong></p>
<p>您可以通过将IdentityServerOptions类注入代码来访问IdentityServer配置。 这个，例如 具有登录页面的已配置路径：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> returnUrl = Url.Action(<span style="color: #800000;">"</span><span style="color: #800000;">Index</span><span style="color: #800000;">"</span><span style="color: #000000;">);
returnUrl </span>=<span style="color: #000000;"> returnUrl.AddQueryString(Request.QueryString.Value);

</span><span style="color: #0000ff;">var</span> loginUrl =<span style="color: #000000;"> _options.UserInteraction.LoginUrl;
</span><span style="color: #0000ff;">var</span> url =<span style="color: #000000;"> loginUrl.AddQueryString(_options.UserInteraction.LoginReturnUrlParameter, returnUrl);

</span><span style="color: #0000ff;">return</span> Redirect(url);</pre>
</div>
<p><strong>登录页面与当前协议请求之间的交互</strong></p>
<p>IIdentityServerInteractionService支持将协议返回URL转换为已解析和验证的上下文对象：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> context = <span style="color: #0000ff;">await</span> _interaction.GetAuthorizationContextAsync(returnUrl);</pre>
</div>
<p>默认情况下，交互服务仅了解OpenID Connect协议消息。 要扩展支持，您可以编写自己的IReturnUrlParser：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IReturnUrlParser
{
    </span><span style="color: #0000ff;">bool</span> IsValidReturnUrl(<span style="color: #0000ff;">string</span><span style="color: #000000;"> returnUrl);
    Task</span>&lt;AuthorizationRequest&gt; ParseAsync(<span style="color: #0000ff;">string</span><span style="color: #000000;"> returnUrl);
}</span></pre>
</div>
<p>..然后在DI中注册解析器：</p>
<div class="cnblogs_code">
<pre>builder.Services.AddTransient&lt;IReturnUrlParser, WsFederationReturnUrlParser&gt;();</pre>
</div>
<p>这允许登录页面获取客户端配置和其他协议参数等信息。</p>
<p><strong>访问用于创建协议响应的配置和密钥材料</strong></p>
<p>通过将IKeyMaterialService注入代码，您可以访问配置的签名凭据和验证密钥：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> credential = <span style="color: #0000ff;">await</span><span style="color: #000000;"> _keys.GetSigningCredentialsAsync();
</span><span style="color: #0000ff;">var</span> key = credential.Key <span style="color: #0000ff;">as</span><span style="color: #000000;"> Microsoft.IdentityModel.Tokens.X509SecurityKey;

</span><span style="color: #0000ff;">var</span> descriptor = <span style="color: #0000ff;">new</span><span style="color: #000000;"> SecurityTokenDescriptor
{
    AppliesToAddress </span>=<span style="color: #000000;"> result.Client.ClientId,
    Lifetime </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> Lifetime(DateTime.UtcNow, DateTime.UtcNow.AddSeconds(result.Client.IdentityTokenLifetime)),
    ReplyToAddress </span>=<span style="color: #000000;"> result.Client.RedirectUris.First(),
    SigningCredentials </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> X509SigningCredentials(key.Certificate, result.RelyingParty.SignatureAlgorithm, result.RelyingParty.DigestAlgorithm),
    Subject </span>=<span style="color: #000000;"> outgoingSubject,
    TokenIssuerName </span>=<span style="color: #000000;"> _contextAccessor.HttpContext.GetIdentityServerIssuerUri(),
    TokenType </span>=<span style="color: #000000;"> result.RelyingParty.TokenType
};</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">二十七、Tools<a name="a27"></a></span></strong></p>
<p>IdentityServerTools类是在为IdentityServer编写可扩展性代码时可能需要的有用内部工具的集合。 要使用它，请将其注入您的代码，例如 控制器：&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span><span style="color: #000000;"> MyController(IdentityServerTools tools)
{
    _tools </span>=<span style="color: #000000;"> tools;
}</span></pre>
</div>
<p>IssueJwtAsync方法允许使用IdentityServer令牌创建引擎创建JWT令牌。 IssueClientJwtAsync是用于为服务器到服务器通信创建令牌的简单版本（例如，当您必须从代码中调用受IdentityServer保护的API时）：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task&lt;IActionResult&gt;<span style="color: #000000;"> MyAction()
{
    </span><span style="color: #0000ff;">var</span> token = <span style="color: #0000ff;">await</span><span style="color: #000000;"> _tools.IssueClientJwtAsync(
        clientId: </span><span style="color: #800000;">"</span><span style="color: #800000;">client_id</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        lifetime: </span><span style="color: #800080;">3600</span><span style="color: #000000;">,
        audiences: </span><span style="color: #0000ff;">new</span>[] { <span style="color: #800000;">"</span><span style="color: #800000;">backend.api</span><span style="color: #800000;">"</span><span style="color: #000000;"> });

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> more code</span>
}</pre>
</div>
<p>&nbsp;</p>