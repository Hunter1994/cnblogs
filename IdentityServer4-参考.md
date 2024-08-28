<p><a href="#a1">一、Identity Resource</a></p>
<p><a href="#a2">二、API Resource</a></p>
<p><a href="#a3">三、Client</a></p>
<p><a href="#a4">四、GrantValidationResult</a></p>
<p><a href="#a5">五、Profile Service</a></p>
<p><a href="#a6">六、IdentityServer Interaction Service</a></p>
<p><a href="#a7">七、IdentityServer Options</a></p>
<p><a href="#a8">八、Entity Framework Support</a></p>
<p><a href="#a9">九、ASP.NET Identity Support</a></p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">一、Identity Resource<a name="a1"></a></span></strong></span></p>
<p><code class="docutils literal notranslate"><span class="pre">Enabled</span></code></p>
<p>指示此资源是否已启用且可以请求。 默认为true。</p>
<p><code class="docutils literal notranslate"><span class="pre">Name</span></code></p>
<p>身份资源的唯一名称。 这是客户端将用于授权请求中的scope参数的值。</p>
<p><code class="docutils literal notranslate"><span class="pre">DisplayName</span></code></p>
<p>该值将用于例如 用在consent显示上。</p>
<p><code class="docutils literal notranslate"><span class="pre">Description</span></code></p>
<p>该值将用于例如&nbsp;用在consent显示上。</p>
<p><code class="docutils literal notranslate"><span class="pre">Required</span></code></p>
<p>是否在consent页面必须选择。 默认为false。</p>
<p><code class="docutils literal notranslate"><span class="pre">Emphasize</span></code></p>
<p>指定consent页面是否会强调此范围（如果consent页面要实现此类功能）。 将此设置用于敏感或重要范围。 默认为false。</p>
<p><code class="docutils literal notranslate"><span class="pre">ShowInDiscoveryDocument</span></code></p>
<p>指定此范围是否显示在发现文档中。 默认为true。</p>
<p><code class="docutils literal notranslate"><span class="pre">UserClaims</span></code></p>
<p>应包含在身份令牌中的关联用户声明类型的列表。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">二、API Resource<a name="a2"></a></span></strong></span></p>
<p><code class="docutils literal notranslate"><span class="pre">Enabled</span></code></p>
<p>指示此资源是否已启用且可以请求。 默认为true。</p>
<p><code class="docutils literal notranslate"><span class="pre">Name</span></code></p>
<p>API的唯一名称</p>
<p><code class="docutils literal notranslate"><span class="pre">DisplayName</span></code></p>
<p>该值将用于例如 用在consent显示上。</p>
<p><code class="docutils literal notranslate"><span class="pre">Description</span></code></p>
<p>该值将用于例如&nbsp;用在consent显示上。</p>
<p><code class="docutils literal notranslate"><span class="pre">ApiSecrets</span></code></p>
<p>API密钥用于自检端点。 API可以使用API名称和密钥进行自检验证。</p>
<p><code class="docutils literal notranslate"><span class="pre">UserClaims</span></code></p>
<p>应包含在访问令牌中的关联用户声明类型的列表。</p>
<p><code class="docutils literal notranslate"><span class="pre">Scopes</span></code></p>
<p>API必须至少有一个范围。 每个范围可以有不同的设置。</p>
<h2>Scopes</h2>
<p>在简单的情况下，API只有一个范围。 但是在某些情况下，您可能希望细分API的功能，并让不同的客户端访问不同的部分。</p>
<p><code class="docutils literal notranslate"><span class="pre">Name</span></code></p>
<p>scope的唯一名称。 这是客户端将用于授权/令牌请求中的scope参数的值。</p>
<p><code class="docutils literal notranslate"><span class="pre">DisplayName</span></code></p>
<p>显示名称，一般用在consent页面展示</p>
<p><code class="docutils literal notranslate"><span class="pre">Description</span></code></p>
<p>描述，一般用在consent页面展示</p>
<p><code class="docutils literal notranslate"><span class="pre">Required</span></code></p>
<p>是否必选，如果设置为true，则consent页面则不可取消此scope（&nbsp;默认为false）</p>
<p><code class="docutils literal notranslate"><span class="pre">Emphasize</span></code></p>
<p>指定consent页面是否会强调此范围（如果consent页面要实现此类功能）。 将此设置用于敏感或重要范围。 默认为false。</p>
<p><code class="docutils literal notranslate"><span class="pre">ShowInDiscoveryDocument</span></code></p>
<p>指定此范围是否显示在发现文档中。 默认为true。</p>
<p><code class="docutils literal notranslate"><span class="pre">UserClaims</span></code></p>
<p>应包含在访问令牌中的关联用户声明类型的列表。 此处指定的声明将添加到为API指定的声明列表中。</p>
<h2>便捷构造行为</h2>
<p>只是关于为ApiResource类提供的构造函数的注释。</p>
<p>要完全控制ApiResource中的数据，请使用不带参数的默认构造函数。 如果要为每个API配置多个范围，可以使用此方法。 例如：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">new</span><span style="color: #000000;"> ApiResource
{
    Name </span>= <span style="color: #800000;">"</span><span style="color: #800000;">api2</span><span style="color: #800000;">"</span><span style="color: #000000;">,

    Scopes </span>=<span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> Scope()
        {
            Name </span>= <span style="color: #800000;">"</span><span style="color: #800000;">api2.full_access</span><span style="color: #800000;">"</span><span style="color: #000000;">,
            DisplayName </span>= <span style="color: #800000;">"</span><span style="color: #800000;">Full access to API 2</span><span style="color: #800000;">"</span><span style="color: #000000;">
        },
        </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> Scope
        {
            Name </span>= <span style="color: #800000;">"</span><span style="color: #800000;">api2.read_only</span><span style="color: #800000;">"</span><span style="color: #000000;">,
            DisplayName </span>= <span style="color: #800000;">"</span><span style="color: #800000;">Read only access to API 2</span><span style="color: #800000;">"</span><span style="color: #000000;">
        }
    }
}</span></pre>
</div>
<p>对于每个API只需要一个范围的简单方案，则提供了几个接受名称的便捷构造函数。 例如：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">new</span> ApiResource(<span style="color: #800000;">"</span><span style="color: #800000;">api1</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">Some API 1</span><span style="color: #800000;">"</span>)</pre>
</div>
<p>使用便捷构造函数等同于：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">new</span><span style="color: #000000;"> ApiResource
{
    Name </span>= <span style="color: #800000;">"</span><span style="color: #800000;">api1</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    DisplayName </span>= <span style="color: #800000;">"</span><span style="color: #800000;">Some API 1</span><span style="color: #800000;">"</span><span style="color: #000000;">,

    Scopes </span>=<span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> Scope()
        {
            Name </span>= <span style="color: #800000;">"</span><span style="color: #800000;">api1</span><span style="color: #800000;">"</span><span style="color: #000000;">,
            DisplayName </span>= <span style="color: #800000;">"</span><span style="color: #800000;">Some API 1</span><span style="color: #800000;">"</span><span style="color: #000000;">
        }
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">三、Client<a name="a3"></a></span></strong></span></p>
<p>Client类为OpenID Connect或OAuth 2.0客户端建模 - 例如 本机应用程序，Web应用程序或基于JS的应用程序。&nbsp;</p>
<h2>基本</h2>
<p><code class="docutils literal notranslate"><span class="pre">Enabled</span></code></p>
<p>指定是否启用客户端。 默认为true。</p>
<p><code class="docutils literal notranslate"><span class="pre">ClientId</span></code></p>
<p>客户端的唯一ID</p>
<p><code class="docutils literal notranslate"><span class="pre">ClientSecrets</span></code></p>
<p>客户端密钥列表 - 访问令牌端点的凭据。</p>
<p><code class="docutils literal notranslate"><span class="pre">RequireClientSecret</span></code></p>
<p>指定此客户端是否需要密钥才能从令牌端点请求令牌（默认为true）</p>
<p><code class="docutils literal notranslate"><span class="pre">AllowedGrantTypes</span></code></p>
<p>指定允许客户端使用的授权类型。 使用GrantTypes类进行常见组合。</p>
<p><code class="docutils literal notranslate"><span class="pre">RequirePkce</span></code></p>
<p>指定使用基于授权代码的授权类型的客户端是否必须发送校验密钥</p>
<p><code class="docutils literal notranslate"><span class="pre">AllowPlainTextPkce</span></code></p>
<p>指定使用PKCE的客户端是否可以使用纯文本代码质询（不推荐 - 默认为false）</p>
<p><code class="docutils literal notranslate"><span class="pre">RedirectUris</span></code></p>
<p>指定允许的URI以返回令牌或授权码</p>
<p><code class="docutils literal notranslate"><span class="pre">AllowedScopes</span></code></p>
<p>默认情况下，客户端无权访问任何资源 - 通过添加相应的范围名称来指定允许的资源</p>
<p><code class="docutils literal notranslate"><span class="pre">AllowOfflineAccess</span></code></p>
<p>指定此客户端是否可以请求刷新令牌（请求offline_accessscope）</p>
<p><code class="docutils literal notranslate"><span class="pre">AllowAccessTokensViaBrowser</span></code></p>
<p>指定是否允许此客户端通过浏览器接收访问令牌。 这对于强化允许多种响应类型的流是有用的(例如，不允许混合流客户端使用code id_token添加令牌响应类型，从而将令牌泄露给浏览器。)</p>
<p><code class="docutils literal notranslate"><span class="pre">Properties</span></code></p>
<p>字典可根据需要保存任何自定义客户端特定值。</p>
<h2>认证/注销</h2>
<p><code class="docutils literal notranslate"><span class="pre">PostLogoutRedirectUris</span></code></p>
<p>指定在注销后重定向到的允许URI。</p>
<p><code class="docutils literal notranslate"><span class="pre">FrontChannelLogoutUri</span></code></p>
<p>指定客户端的注销URI，以用于基于HTTP的前端通道注销。</p>
<p><code class="docutils literal notranslate"><span class="pre">FrontChannelLogoutSessionRequired</span></code></p>
<p>指定是否应将用户的会话ID发送到FrontChannelLogoutUri。 默认为true。</p>
<p><code class="docutils literal notranslate"><span class="pre">BackChannelLogoutUri</span></code></p>
<p>指定客户端的注销URI，以用于基于HTTP的反向通道注销。</p>
<p><code class="docutils literal notranslate"><span class="pre">BackChannelLogoutSessionRequired</span></code></p>
<p>指定是否应在请求中将用户的会话ID发送到BackChannelLogoutUri。 默认为true。</p>
<p><code class="docutils literal notranslate"><span class="pre">EnableLocalLogin</span></code></p>
<p>指定此客户端是否可以仅使用本地帐户或外部IdP。 默认为true。</p>
<p><code class="docutils literal notranslate"><span class="pre">IdentityProviderRestrictions</span></code></p>
<p>指定可以与此客户端一起使用的外部IdP（如果列表为空，则允许所有IdP）。 默认为空。</p>
<h2>Token</h2>
<p><code class="docutils literal notranslate"><span class="pre">IdentityTokenLifetime</span></code></p>
<p>Identity令牌的生命周期（以秒为单位）（默认为300秒/ 5分钟）</p>
<p><code class="docutils literal notranslate"><span class="pre">AccessTokenLifetime</span></code></p>
<p>访问令牌的生命周期（以秒为单位）（默认为3600秒/ 1小时）</p>
<p><code class="docutils literal notranslate"><span class="pre">AuthorizationCodeLifetime</span></code></p>
<p>授权代码的生命周期（以秒为单位）（默认为300秒/ 5分钟）</p>
<p><code class="docutils literal notranslate"><span class="pre">AbsoluteRefreshTokenLifetime</span></code></p>
<p>刷新令牌的最长生命周期，以秒为单位。 默认为2592000秒/ 30天</p>
<p><code class="docutils literal notranslate"><span class="pre">SlidingRefreshTokenLifetime</span></code></p>
<p>刷新令牌的生命周期以秒为单位。 默认为1296000秒/ 15天</p>
<p><code class="docutils literal notranslate"><span class="pre">RefreshTokenUsage</span></code></p>
<p class="first"><code class="docutils literal notranslate"><span class="pre">　　ReUse</span></code>&nbsp;刷新令牌时刷新令牌句柄将保持不变</p>
<p class="last"><code class="docutils literal notranslate"><span class="pre">　　OneTime</span></code>&nbsp;刷新令牌时将更新刷新令牌句柄。 这是默认值。</p>
<p><code class="docutils literal notranslate"><span class="pre">RefreshTokenExpiration</span></code></p>
<p class="first"><code class="docutils literal notranslate"><span class="pre">　　Absolute</span></code>&nbsp;刷新令牌将在固定时间点到期（由AbsoluteRefreshTokenLifetime指定）</p>
<p class="last"><code class="docutils literal notranslate"><span class="pre">　　Sliding</span></code>&nbsp;刷新令牌时，将刷新刷新令牌的生命周期（按SlidingRefreshTokenLifetime中指定的数量）。 生命周期不会超过AbsoluteRefreshTokenLifetime。</p>
<p><code class="docutils literal notranslate"><span class="pre">UpdateAccessTokenClaimsOnRefresh</span></code></p>
<p>获取或设置一个值，该值指示是否应在刷新令牌请求上更新访问令牌（及其声明）。</p>
<p><code class="docutils literal notranslate"><span class="pre">AccessTokenType</span></code></p>
<p>指定访问令牌是引用令牌还是自包含JWT令牌（默认为Jwt）。</p>
<p><code class="docutils literal notranslate"><span class="pre">IncludeJwtId</span></code></p>
<p>指定JWT访问令牌是否应具有嵌入的唯一ID（通过jti声明）。</p>
<p><code class="docutils literal notranslate"><span class="pre">AllowedCorsOrigins</span></code></p>
<p>如果指定，将由默认CORS策略服务实现（In-Memory和EF）用于为JavaScript客户端构建CORS策略。</p>
<p><code class="docutils literal notranslate"><span class="pre">Claims</span></code></p>
<p>允许客户端的设置声明（将包含在访问令牌中）。</p>
<p><code class="docutils literal notranslate"><span class="pre">AlwaysSendClientClaims</span></code></p>
<p>如果设置，将为每个流发送客户端声明。 如果不是，仅用于客户端凭证流（默认为false）</p>
<p><code class="docutils literal notranslate"><span class="pre">AlwaysIncludeUserClaimsInIdToken</span></code></p>
<p>在请求id令牌和访问令牌时，如果用户声明始终将其添加到id令牌而不是请求客户端使用userinfo端点。 默认值为false。</p>
<p><code class="docutils literal notranslate"><span class="pre">ClientClaimsPrefix</span></code></p>
<p>如果设置，前缀客户端声明类型将被加上前缀。默认为client_。目的是确保它们不会意外地与用户声明发生冲突。</p>
<p><code class="docutils literal notranslate"><span class="pre">PairWiseSubjectSalt</span></code></p>
<p>对于此客户端的用户，在成对的subjectId生成中使用的salt值。</p>
<h2>Consent Screen</h2>
<p><code class="docutils literal notranslate"><span class="pre">RequireConsent</span></code></p>
<p>指定是否需要同意屏幕。 默认为true。</p>
<p><code class="docutils literal notranslate"><span class="pre">AllowRememberConsent</span></code></p>
<p>指定用户是否可以选择存储同意决策。 默认为true。</p>
<p><code class="docutils literal notranslate"><span class="pre">ConsentLifetime</span></code></p>
<p>用户同意的生命周期，以秒为单位。 默认为null（无到期）。</p>
<p><code class="docutils literal notranslate"><span class="pre">ClientName</span></code></p>
<p>客户端显示名称（用于记录和同意页面显示）</p>
<p><code class="docutils literal notranslate"><span class="pre">ClientUri</span></code></p>
<p>有关客户端的更多信息的URI（在同意屏幕上使用）</p>
<p><code class="docutils literal notranslate"><span class="pre">LogoUri</span></code></p>
<p>URI到客户端图标（在同意屏幕上使用）</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">四、GrantValidationResult<a name="a4"></a></span></strong></span></p>
<p>GrantValidationResult类为extensions grants和resource owner password grants的授权验证结果建模。&nbsp;</p>
<p>最常见的用法是使用身份（成功案例）新建它：</p>
<div class="cnblogs_code">
<pre>context.Result = <span style="color: #0000ff;">new</span><span style="color: #000000;"> GrantValidationResult(
    subject: </span><span style="color: #800000;">"</span><span style="color: #800000;">818727</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    authenticationMethod: </span><span style="color: #800000;">"</span><span style="color: #800000;">custom</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    claims: optionalClaims);</span></pre>
</div>
<p>...或使用错误和描述（失败案例）：</p>
<div class="cnblogs_code">
<pre>context.Result = <span style="color: #0000ff;">new</span><span style="color: #000000;"> GrantValidationResult(
    TokenRequestErrors.InvalidGrant,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">invalid custom credential</span><span style="color: #800000;">"</span>);</pre>
</div>
<p>在这两种情况下，您都可以传递将包含在令牌响应中的其他自定义值。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">五、Profile Service<a name="a5"></a></span></strong></span></p>
<p>IdentityServer通常在创建令牌或处理对userinfo或内省端点的请求时需要有关用户的身份信息。 默认情况下，IdentityServer仅在身份验证cookie中具有声明，以便为此身份数据进行绘制。&nbsp;</p>
<p>将用户所需的所有可能声明放入cookie中是不切实际的，因此IdentityServer定义了一个扩展点，允许根据用户需要动态加载声明。 此扩展点是IProfileService，开发人员通常可以实现此接口来访问包含用户身份数据的自定义数据库或API。</p>
<h2>IProfileService APIs</h2>
<p><code class="docutils literal notranslate"><span class="pre">GetProfileDataAsync</span></code></p>
<p>预期为用户加载声明的API。 它传递一个ProfileDataRequestContext的实例。</p>
<p><code class="docutils literal notranslate"><span class="pre">IsActiveAsync</span></code></p>
<p>预期用于指示当前是否允许用户获取令牌的API。 它传递一个IsActiveContext的实例。</p>
<h2>ProfileDataRequestContext</h2>
<p>模拟用户声明的请求，并且是返回这些声明的工具。 它包含以下属性：</p>
<p><code class="docutils literal notranslate"><span class="pre">Subject</span></code></p>
<p>ClaimsPrincipal为用户建模。</p>
<p><code class="docutils literal notranslate"><span class="pre">Client</span></code></p>
<p>被请求claims的客户。</p>
<p><code class="docutils literal notranslate"><span class="pre">RequestedClaimTypes</span></code></p>
<p>要求收集claim类型。</p>
<p><code class="docutils literal notranslate"><span class="pre">Caller</span></code></p>
<p>正在请求声明的上下文的标识符（例如，身份令牌，访问令牌或用户信息端点）。 常量IdentityServerConstants。</p>
<p><code class="docutils literal notranslate"><span class="pre">ProfileDataCallers</span></code></p>
<p>包含不同的常量值。</p>
<p><code class="docutils literal notranslate"><span class="pre">IssuedClaims</span></code></p>
<p>将返回的Claim的列表。 预计这将由自定义IProfileService实现填充。</p>
<p><code class="docutils literal notranslate"><span class="pre">AddRequestedClaims</span></code></p>
<p>ProfileDataRequestContext上的扩展方法用于填充IssuedClaims，但首先根据RequestedClaimTypes过滤声明。</p>
<h2>请求的范围和声明映射</h2>
<p>客户端请求的范围控制用户声明在令牌中返回给客户端的内容。 GetProfileDataAsync方法负责根据ProfileDataRequestContext上的RequestedClaimTypes集合动态获取这些声明。</p>
<p>RequestedClaimTypes集合基于在对作用域建模的资源上定义的用户声明进行填充。 如果请求的作用域是标识资源，则将根据IdentityResource中定义的用户声明类型填充RequestedClaimTypes中的声明。 如果请求的范围是API资源，则将根据ApiResource和/或Scope中定义的用户声明类型填充RequestedClaimTypes中的声明。</p>
<h2>IsActiveContext</h2>
<p>对请求进行建模以确定用户当前是否允许获取令牌。它包含这些属性:</p>
<p><code class="docutils literal notranslate"><span class="pre">Subject</span></code></p>
<p>ClaimsPrincipal为用户建模。</p>
<p><code class="docutils literal notranslate"><span class="pre">Client</span></code></p>
<p>要求提出claims的客户。</p>
<p><code class="docutils literal notranslate"><span class="pre">Caller</span></code></p>
<p>正在请求声明的上下文的标识符（例如，身份令牌，访问令牌或用户信息端点）。 常量IdentityServerConstants.ProfileDataCallers包含不同的常量值。</p>
<p><code class="docutils literal notranslate"><span class="pre">IsActive</span></code></p>
<p>指示是否允许用户获取令牌的标志。 预计这将由自定义IProfileService实现分配。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">六、IdentityServer Interaction Service<a name="a6"></a></span></strong></span></p>
<p>IIdentityServerInteractionService接口旨在提供用户界面用于与IdentityServer通信的服务，主要与用户交互有关。 它可以从依赖注入系统获得，通常作为构造函数参数注入到IdentityServer的用户界面的MVC控制器中。&nbsp;</p>
<h2>IIdentityServerInteractionService APIs</h2>
<p><code class="docutils literal notranslate"><span class="pre">GetAuthorizationContextAsync</span></code></p>
<p>基于传递给登录页面或同意页面的returnUrl返回AuthorizationRequest。</p>
<p><code class="docutils literal notranslate"><span class="pre">IsValidReturnUrl</span></code></p>
<p>指示在登录或同意后returnUrl是否为重定向的有效URL。</p>
<p><code class="docutils literal notranslate"><span class="pre">GetErrorContextAsync</span></code></p>
<p>根据传递给错误页面的errorId返回ErrorMessage。</p>
<p><code class="docutils literal notranslate"><span class="pre">GetLogoutContextAsync</span></code></p>
<p>根据传递给注销页面的logoutId返回LogoutRequest。</p>
<p><code class="docutils literal notranslate"><span class="pre">CreateLogoutContextAsync</span></code></p>
<p>如果当前没有logoutId，则用于创建logoutId。 这将创建一个cookie，捕获注销所需的所有当前状态，logoutId标识该cookie。 这通常在没有当前logoutId时使用，并且注销页面必须捕获当前用户在重定向到外部身份提供程序以进行注销之前注销所需的状态。 新创建的logoutId需要在注销时往返外部身份提供者，然后在注销回调页面上使用，就像在普通注销页面上一样。</p>
<p><code class="docutils literal notranslate"><span class="pre">GrantConsentAsync</span></code></p>
<p>接受ConsentResponse以通知IdentityServer用户同意特定的AuthorizationRequest。</p>
<p><code class="docutils literal notranslate"><span class="pre">GetAllUserConsentsAsync</span></code></p>
<p>返回用户的Consent集合。</p>
<p><code class="docutils literal notranslate"><span class="pre">RevokeUserConsentAsync</span></code></p>
<p>撤消用户对用户的所有同意和授权。</p>
<p><code class="docutils literal notranslate"><span class="pre">RevokeTokensForCurrentSessionAsync</span></code></p>
<p>撤消用户在当前会话期间签署的客户的所有同意和授权。</p>
<h2>AuthorizationRequest</h2>
<p><code class="docutils literal notranslate"><span class="pre">ClientId</span></code></p>
<p>发起请求的客户端标识符。</p>
<p><code class="docutils literal notranslate"><span class="pre">RedirectUri</span></code></p>
<p>成功授权后将用户重定向到的URI。</p>
<p><code class="docutils literal notranslate"><span class="pre">DisplayMode</span></code></p>
<p>显示模式从授权请求传递。</p>
<p><code class="docutils literal notranslate"><span class="pre">UiLocales</span></code></p>
<p>从授权请求传递的UI语言环境。</p>
<p><code class="docutils literal notranslate"><span class="pre">IdP</span></code></p>
<p>请求的外部标识提供程序。这是用来绕过国内领域发现(HRD)。这是通过授权请求上的acr_values参数的&ldquo;idp:&rdquo;前缀提供的。</p>
<p><code class="docutils literal notranslate"><span class="pre">Tenant</span></code></p>
<p>租客要求。 这是通过&ldquo;tenant：&rdquo;前缀提供给授权请求的acr_values参数。</p>
<p><code class="docutils literal notranslate"><span class="pre">LoginHint</span></code></p>
<p>用户将用于登录的预期用户名。 这是通过授权请求上的login_hint参数从客户端请求的。</p>
<p><code class="docutils literal notranslate"><span class="pre">PromptMode</span></code></p>
<p>从授权请求请求的提示模式。</p>
<p><code class="docutils literal notranslate"><span class="pre">AcrValues</span></code></p>
<p>从授权请求传递的acr值。</p>
<p><code class="docutils literal notranslate"><span class="pre">ScopesRequested</span></code></p>
<p>授权请求请求的范围。参数传递给授权请求的整个参数集合。</p>
<h2>ErrorMessage</h2>
<p><code class="docutils literal notranslate"><span class="pre">DisplayMode</span></code></p>
<p>从授权请求中传递的显示模式。</p>
<p><code class="docutils literal notranslate"><span class="pre">UiLocales</span></code></p>
<p>从授权请求中传递的UI区域。</p>
<p><code class="docutils literal notranslate"><span class="pre">Error</span></code></p>
<p>错误代码。</p>
<p><code class="docutils literal notranslate"><span class="pre">RequestId</span></code></p>
<p>每个请求标识符。这可以用于向最终用户显示，也可以用于诊断。</p>
<h2>LogoutRequest</h2>
<p><code class="docutils literal notranslate"><span class="pre">ClientId</span></code></p>
<p>发起请求的客户端标识符。</p>
<p><code class="docutils literal notranslate"><span class="pre">PostLogoutRedirectUri</span></code></p>
<p>用户在注销后将其重定向到的URL。</p>
<p><code class="docutils literal notranslate"><span class="pre">SessionId</span></code></p>
<p>用户当前的会话ID。</p>
<p><code class="docutils literal notranslate"><span class="pre">SignOutIFrameUrl</span></code></p>
<p>要在注销页面上的&lt;iframe&gt;中呈现以启用单点注销的URL。</p>
<p><code class="docutils literal notranslate"><span class="pre">Parameters</span></code></p>
<p>整个参数集合传递给结束会话端点。</p>
<p><code class="docutils literal notranslate"><span class="pre">ShowSignoutPrompt</span></code></p>
<p>指示是否应根据传递到结束会话端点的参数提示用户注销。</p>
<h2>ConsentResponse</h2>
<p><code class="docutils literal notranslate"><span class="pre">ScopesConsented</span></code></p>
<p>用户同意的范围集合。</p>
<p><code class="docutils literal notranslate"><span class="pre">RememberConsent</span></code></p>
<p>指示是否持久保留用户同意的标志。</p>
<h2>Consent</h2>
<p><code class="docutils literal notranslate"><span class="pre">SubjectId</span></code></p>
<p>授予同意的subjectID。</p>
<p><code class="docutils literal notranslate"><span class="pre">ClientId</span></code></p>
<p>客户端标识符。</p>
<p><code class="docutils literal notranslate"><span class="pre">Scopes</span></code></p>
<p>范围。</p>
<p><code class="docutils literal notranslate"><span class="pre">CreationTime</span></code></p>
<p>获得同意日期和时间</p>
<p><code class="docutils literal notranslate"><span class="pre">Expiration</span></code></p>
<p>同意过期的日期和时间。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">七、IdentityServer Options<a name="a7"></a></span></strong></span></p>
<ul class="simple">
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">IssuerUri</span></code></dt><dd>设置将在发现文档和已颁发的JWT令牌中显示的颁发者名称。 建议不要设置此属性，该属性从客户端使用的主机名中推断颁发者名称。</dd></dl></li>
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">PublicOrigin</span></code></dt><dd>此服务器实例的来源，例如https://myorigin.com。 如果未设置，则从请求推断出原始名称。</dd></dl></li>
</ul>
<h2>Endpoints</h2>
<p>允许启用/禁用各个端点，例如 令牌，授权，用户信息等</p>
<p>默认情况下，所有端点都已启用，但您可以通过禁用不需要的端点来锁定服务器。</p>
<h2>Discovery</h2>
<p>允许启用/禁用发现文档的各个部分，例如 端点，范围，声明，授权类型等</p>
<p>CustomEntries字典允许向发现文档添加自定义元素。</p>
<h2>Authentication</h2>
<ul class="simple">
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">CookieLifetime</span></code></dt><dd>身份验证cookie生存期（仅在使用IdentityServer提供的cookie处理程序时有效）。</dd></dl></li>
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">CookieSlidingExpiration</span></code></dt><dd>指定cookie是否应该滑动（仅在使用IdentityServer提供的cookie处理程序时有效）。</dd></dl></li>
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">RequireAuthenticatedUserForSignOutMessage</span></code></dt><dd>指示是否必须对用户进行身份验证以接受结束会话端点的参数。 默认为false。</dd></dl></li>
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">CheckSessionCookieName</span></code></dt><dd>用于检查会话端点的cookie的名称。</dd></dl></li>
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">RequireCspFrameSrcForSignout</span></code></dt><dd>如果设置，将要求frame-src CSP标头在结束会话回调端点上发出，该端点向客户端呈现iframe以进行前端通道注销通知。 默认为true。</dd></dl></li>
</ul>
<h2>Events</h2>
<p>允许配置是否应将哪些事件提交到已注册的事件接收器。 有关活动的更多信息，请参见此处。</p>
<h2>InputLengthRestrictions</h2>
<p>允许设置各种协议参数的长度限制，如客户端ID，范围，重定向URI等。</p>
<h2>UserInteraction</h2>
<ul class="simple">
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">LoginUrl</span></code>,&nbsp;<code class="docutils literal notranslate"><span class="pre">LogoutUrl</span></code>,&nbsp;<code class="docutils literal notranslate"><span class="pre">ConsentUrl</span></code>,&nbsp;<code class="docutils literal notranslate"><span class="pre">ErrorUrl</span></code></dt><dd>设置登录，注销，同意和错误页面的URL。</dd></dl></li>
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">LoginReturnUrlParameter</span></code></dt><dd>设置传递给登录页面的返回URL参数的名称。 默认为returnUrl。</dd></dl></li>
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">LogoutIdParameter</span></code></dt><dd>设置传递给注销页面的注销消息id参数的名称。 默认为logoutId。</dd></dl></li>
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">ConsentReturnUrlParameter</span></code></dt><dd>设置传递给同意页面的返回URL参数的名称。 默认为returnUrl。</dd></dl></li>
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">ErrorIdParameter</span></code></dt><dd>设置传递给错误页面的错误消息id参数的名称。 默认为errorId。</dd></dl></li>
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">CustomRedirectReturnUrlParameter</span></code></dt><dd>设置从授权端点传递给自定义重定向的返回URL参数的名称。 默认为returnUrl。</dd></dl></li>
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">CookieMessageThreshold</span></code></dt><dd>IdentityServer和某些UI页面之间的某些交互需要cookie来传递状态和上下文（上面的任何具有可配置&ldquo;message id&rdquo;参数的页面）。 由于浏览器对cookie的数量及其大小有限制，因此该设置用于防止创建过多的cookie。 该值设置将创建的任何类型的消息cookie的最大数量。 一旦达到限制，将清除最早的消息cookie。 这有效地表示用户在使用IdentityServer时可以打开多少个选项卡。</dd></dl></li>
</ul>
<h2>Caching</h2>
<p>这些设置仅在启动时在服务配置中启用了相应的缓存时才适用。</p>
<ul class="simple">
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">ClientStoreExpiration</span></code></dt><dd>从客户端存储加载的客户端配置的缓存持续时间。</dd></dl></li>
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">ResourceStoreExpiration</span></code></dt><dd>缓存从资源存储加载的标识和API资源配置的持续时间。</dd></dl></li>
</ul>
<h2>CORS</h2>
<p>IdentityServer支持某些端点的CORS。 底层CORS实现由ASP.NET Core提供，因此它在依赖注入系统中自动注册。</p>
<ul class="simple">
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">CorsPolicyName</span></code></dt><dd>将针对进入IdentityServer的CORS请求评估的CORS策略的名称（默认为&ldquo;IdentityServer4&rdquo;）。 处理此问题的策略提供程序是根据在依赖项注入系统中注册的ICorsPolicyService实现的。 如果您希望自定义允许连接的CORS源集，那么建议您提供ICorsPolicyService的自定义实现。</dd></dl></li>
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">CorsPaths</span></code></dt><dd>IdentityServer中支持CORS的端点。 默认为发现，用户信息，令牌和吊销端点。</dd></dl></li>
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">PreflightCacheDuration</span></code></dt><dd>Nullable &lt;TimeSpan&gt;指示在预检Access-Control-Max-Ageresponse标头中使用的值。 默认为null，表示未在响应上设置缓存标头。</dd></dl></li>
</ul>
<h2>CSP（内容安全政策）</h2>
<p>在适当的情况下，IdentityServer会为某些响应发出CSP标头。</p>
<ul class="simple">
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">Level</span></code></dt><dd>要使用的CSP级别。 默认情况下使用CSP级别2，但如果必须支持旧版浏览器，则将其更改为CspLevel.One以容纳它们。</dd></dl></li>
<li><dl class="first docutils"><dt><code class="docutils literal notranslate"><span class="pre">AddDeprecatedHeader</span></code></dt><dd>指示是否还应发出旧的X-Content-Security-Policy CSP标头（除了基于标准的标头值之外）。 默认为true。</dd></dl></li>
</ul>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">八、Entity Framework Support<a name="a8"></a></span></strong></span></p>
<p>为IdentityServer中的配置和操作数据扩展点提供了基于EntityFramework的实现。 EntityFramework的使用允许任何EF支持的数据库与此库一起使用。&nbsp;</p>
<p>这个库的<a href="https://github.com/IdentityServer/IdentityServer4.EntityFramework/" target="_blank">repo</a>位于这里，NuGet包在<a href="https://www.nuget.org/packages/IdentityServer4.EntityFramework" target="_blank">这里</a>。</p>
<p>此库提供的功能分为两个主要区域：配置存储和操作存储支持。 根据托管应用程序的需要，这两个不同的区域可以独立使用或一起使用。</p>
<h2>Configuration Store支持客户端，资源和CORS设置</h2>
<p>如果希望从EF支持的数据库加载客户端，标识资源，API资源或CORS数据（而不是使用内存配置），则可以使用配置存储。 此支持提供IClientStore，IResourceStore和ICorsPolicyService可扩展性点的实现。 这些实现使用名为ConfigurationDbContext的DbContext派生类来对数据库中的表进行建模。</p>
<p>要使用配置存储支持，请在调用AddIdentityServer后使用AddConfigurationStore扩展方法：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span><span style="color: #000000;"> IServiceProvider ConfigureServices(IServiceCollection services)
{
    </span><span style="color: #0000ff;">const</span> <span style="color: #0000ff;">string</span> connectionString = <span style="color: #800000;">@"</span><span style="color: #800000;">Data Source=(LocalDb)\MSSQLLocalDB;database=IdentityServer4.EntityFramework-2.0.0;trusted_connection=yes;</span><span style="color: #800000;">"</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">var</span> migrationsAssembly = <span style="color: #0000ff;">typeof</span><span style="color: #000000;">(Startup).GetTypeInfo().Assembly.GetName().Name;

    services.AddIdentityServer()
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> this adds the config data from DB (clients, resources, CORS)</span>
        .AddConfigurationStore(options =&gt;<span style="color: #000000;">
        {
            options.ConfigureDbContext </span>= builder =&gt;<span style="color: #000000;">
                builder.UseSqlServer(connectionString,
                    sql </span>=&gt;<span style="color: #000000;"> sql.MigrationsAssembly(migrationsAssembly));
        });
}</span></pre>
</div>
<p>要配置配置存储，请使用传递给配置回调的ConfigurationStoreOptions选项对象。</p>
<h2>ConfigurationStoreOptions</h2>
<p>此选项类包含用于控制配置存储和ConfigurationDbContext的属性。</p>
<p><code class="docutils literal notranslate"><span class="pre">ConfigureDbContext</span></code></p>
<p>Action &lt;DbContextOptionsBuilder&gt;类型的委托用作回调以配置基础ConfigurationDbContext。 如果EF直接与AddDbContext一起使用，则委托可以以相同的方式配置ConfigurationDbContext，这允许使用任何EF支持的数据库。</p>
<p><code class="docutils literal notranslate"><span class="pre">DefaultSchema</span></code></p>
<p>允许为ConfigurationDbContext中的所有表设置默认数据库模式名称。</p>
<h2>Operational Store对授权授权，同意和令牌的支持（刷新和引用）</h2>
<p>如果希望从EF支持的数据库（而不是默认的内存数据库）加载授权授予，同意和令牌（刷新和引用），则可以使用操作存储。 此支持提供IPersistedGrantStore扩展点的实现。 该实现使用名为PersistedGrantDbContext的DbContext派生类来对数据库中的表进行建模。</p>
<p>要使用操作存储支持，请在调用AddIdentityServer后使用AddOperationalStore扩展方法：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span><span style="color: #000000;"> IServiceProvider ConfigureServices(IServiceCollection services)
{
    </span><span style="color: #0000ff;">const</span> <span style="color: #0000ff;">string</span> connectionString = <span style="color: #800000;">@"</span><span style="color: #800000;">Data Source=(LocalDb)\MSSQLLocalDB;database=IdentityServer4.EntityFramework-2.0.0;trusted_connection=yes;</span><span style="color: #800000;">"</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">var</span> migrationsAssembly = <span style="color: #0000ff;">typeof</span><span style="color: #000000;">(Startup).GetTypeInfo().Assembly.GetName().Name;

    services.AddIdentityServer()
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> this adds the operational data from DB (codes, tokens, consents)</span>
        .AddOperationalStore(options =&gt;<span style="color: #000000;">
        {
            options.ConfigureDbContext </span>= builder =&gt;<span style="color: #000000;">
                builder.UseSqlServer(connectionString,
                    sql </span>=&gt;<span style="color: #000000;"> sql.MigrationsAssembly(migrationsAssembly));

            </span><span style="color: #008000;">//</span><span style="color: #008000;"> this enables automatic token cleanup. this is optional.</span>
            options.EnableTokenCleanup = <span style="color: #0000ff;">true</span><span style="color: #000000;">;
            options.TokenCleanupInterval </span>= <span style="color: #800080;">30</span>; <span style="color: #008000;">//</span><span style="color: #008000;"> interval in seconds</span>
<span style="color: #000000;">        });
}</span></pre>
</div>
<p>要配置操作存储，请使用传递给配置回调的OperationalStoreOptions选项对象。</p>
<h2>OperationalStoreOptions</h2>
<p>此选项类包含用于控制操作存储和PersistedGrantDbContext的属性。</p>
<p><code class="docutils literal notranslate"><span class="pre">ConfigureDbContext</span></code></p>
<p>Action &lt;DbContextOptionsBuilder&gt;类型的委托用作回调以配置基础PersistedGrantDbContext。 如果EF直接与AddDbContext一起使用，则委托可以以相同的方式配置PersistedGrantDbContext，这允许使用任何EF支持的数据库。</p>
<p><code class="docutils literal notranslate"><span class="pre">DefaultSchema</span></code></p>
<p>允许为PersistedGrantDbContext中的所有表设置默认数据库模式名称。</p>
<p><code class="docutils literal notranslate"><span class="pre">EnableTokenCleanup</span></code></p>
<p>指示是否将从数据库中自动清除过时条目。 默认值为false。</p>
<p><code class="docutils literal notranslate"><span class="pre">TokenCleanupInterval</span></code></p>
<p>令牌清理间隔（以秒为单位）。 默认值为3600（1小时）。</p>
<h2>跨不同版本的IdentityServer数据库创建和模式更改</h2>
<p>跨不同版本的IdentityServer（以及EF支持）很可能会更改数据库架构以适应新的和不断变化的功能。</p>
<p>我们不为创建数据库或将数据从一个版本迁移到另一个版本提供任何支持。 您需要以组织认为合适的任何方式管理数据库创建，架构更改和数据迁移。</p>
<p>使用EF迁移是一种可行的方法。 如果您确实希望使用迁移，请参阅EF快速入门以获取有关如何入门的示例，或参阅有关EF迁移的Microsoft文档。</p>
<p><a href="https://github.com/IdentityServer/IdentityServer4.EntityFramework/tree/dev/src/Host/Migrations/IdentityServer" target="_blank">我们还为当前版本的数据库模式发布了示例SQL脚本</a>。</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">九、ASP.NET Identity Support<a name="a9"></a></span></strong></span></p>
<p>提供了基于ASP.NET身份的实现，用于管理IdentityServer用户的身份数据库。 此实现实现IdentityServer中的扩展点，以便为用户加载身份数据以将声明发送到令牌。&nbsp;</p>
<p><a href="https://github.com/IdentityServer/IdentityServer4.AspNetIdentity/" target="_blank">https://github.com/IdentityServer/IdentityServer4.AspNetIdentity/</a></p>
<p>要使用此库，请正常配置ASP.NET标识。 然后在调用AddIdentityServer之后使用AddAspNetIdentity扩展方法：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> ConfigureServices(IServiceCollection services)
{
    services.AddIdentity</span>&lt;ApplicationUser, IdentityRole&gt;<span style="color: #000000;">()
        .AddEntityFrameworkStores</span>&lt;ApplicationDbContext&gt;<span style="color: #000000;">()
        .AddDefaultTokenProviders();

    services.AddIdentityServer()
        .AddAspNetIdentity</span>&lt;ApplicationUser&gt;<span style="color: #000000;">();
}</span></pre>
</div>
<p>AddAspNetIdentity需要将用户建模为ASP.NET标识的类（以及传递给AddIdentity的同一个用于配置ASP.NET标识的类）作为通用参数。 这会将IdentityServer配置为使用IUserClaimsPrincipalFactory，IResourceOwnerPasswordValidator和IProfileService的ASP.NET Identity实现。 它还配置了一些用于IdentityServer的ASP.NET Identity选项（例如要使用的声明类型和身份验证cookie设置）。</p>
<p>&nbsp;</p>