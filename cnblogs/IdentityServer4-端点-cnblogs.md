<p><a href="#a1">一、发现端点</a></p>
<p><a href="#a2">二、授权端点</a></p>
<p><a href="#a3">三、令牌端点</a></p>
<p><a href="#a4">四、UserInfo端点</a></p>
<p><a href="#a5">五、Introspection端点</a></p>
<p><a href="#a6">六、撤销端点</a></p>
<p><a href="#a7">七、结束会话端点</a></p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">一、发现端点<a name="a1"></a></span></strong></span></p>
<p>发现端点可用于检索有关IdentityServer的元数据 - 它返回诸如颁发者名称，密钥材料，支持的范围等信息。&nbsp;</p>
<p>发现端点可通过/.well-known/openid-configuration相对于基地址获得，例如：</p>
<div class="cnblogs_code">
<pre>https:<span style="color: #008000;">//</span><span style="color: #008000;">demo.identityserver.io/.well-known/openid-configuration</span></pre>
</div>
<h2>IdentityModel</h2>
<p>您可以使用IdentityModel库以编程方式访问发现端点：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> discoveryClient = <span style="color: #0000ff;">new</span> DiscoveryClient(<span style="color: #800000;">"</span><span style="color: #800000;">https://demo.identityserver.io</span><span style="color: #800000;">"</span><span style="color: #000000;">);
</span><span style="color: #0000ff;">var</span> doc = <span style="color: #0000ff;">await</span><span style="color: #000000;"> discoveryClient.GetAsync();

</span><span style="color: #0000ff;">var</span> tokenEndpoint =<span style="color: #000000;"> doc.TokenEndpoint;
</span><span style="color: #0000ff;">var</span> keys = doc.KeySet.Keys;</pre>
</div>
<p>出于安全原因，DiscoveryClient具有可配置的验证策略，默认情况下会检查以下规则：</p>
<ul class="simple">
<li>HTTPS必须用于发现端点和所有协议端点</li>
<li>发布者名称应该与下载文档时指定的权限相匹配(这实际上是发现规范中必须的)</li>
<li>协议端点应该位于权限之下&mdash;&mdash;而不是在不同的服务器或URL上(这对于多租户操作来说可能特别有趣)</li>
<li>必须指定密钥集</li>
</ul>
<p>如果由于某种原因（例如开发环境）您需要放松设置，您可以使用以下代码：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> client = <span style="color: #0000ff;">new</span> DiscoveryClient(<span style="color: #800000;">"</span><span style="color: #800000;">http://dev.identityserver.internal</span><span style="color: #800000;">"</span><span style="color: #000000;">);
client.Policy.RequireHttps </span>= <span style="color: #0000ff;">false</span><span style="color: #000000;">;

</span><span style="color: #0000ff;">var</span> disco = <span style="color: #0000ff;">await</span> client.GetAsync();</pre>
</div>
<p>顺便说一句 - 你总是可以通过HTTP连接到localhost和127.0.0.1（但这也是可配置的）。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">二、授权端点<a name="a2"></a></span></strong></span></p>
<p>授权端点可用于通过浏览器请求令牌或授权码。 此过程通常涉及最终用户的身份验证和可选的同意。&nbsp;</p>
<p><span class="cnblogs_code">client_id</span>&nbsp;</p>
<p>客户的标识符（必填）。</p>
<p><code><span class="cnblogs_code">scope</span>&nbsp;</code></p>
<p>一个或多个注册范围（必填）</p>
<p><span class="cnblogs_code">redirect_uri</span>&nbsp;</p>
<p>必须与该客户端允许的重定向URI之一完全匹配（必需）</p>
<p><span class="cnblogs_code">response_type</span>&nbsp;</p>
<p>　　<span class="cnblogs_code">id_token </span>&nbsp;请求身份令牌（仅允许身份范围）</p>
<p>　　<span class="cnblogs_code">token </span>&nbsp;请求访问令牌（仅允许资源范围）</p>
<p>　　<span class="cnblogs_code">id_token token</span>&nbsp;&nbsp;请求身份令牌和访问令牌</p>
<p>　　<span class="cnblogs_code">code</span>&nbsp;请求授权码</p>
<p>　　<span class="cnblogs_code">code id_token</span>&nbsp;&nbsp;请求授权代码和身份令牌</p>
<p>　　<span class="cnblogs_code">code id_token token</span>&nbsp;&nbsp;请求授权代码，身份令牌和访问令牌　　</p>
<p><span class="cnblogs_code">response_mode</span>&nbsp;</p>
<p>　　<span class="cnblogs_code">form_post</span>&nbsp;&nbsp;将令牌响应作为表单发送而不是片段编码重定向（可选）</p>
<p><span class="cnblogs_code">state</span>&nbsp;</p>
<p>identityserver将回显令牌响应的状态值，这是客户端和提供者之间的往返状态，关联请求和响应以及CSRF /重放保护。 （推荐的）</p>
<p><span class="cnblogs_code">nonce</span>&nbsp;</p>
<p>identityserver将回显身份令牌中的nonce值，这是为了重放保护）</p>
<p>通过隐式授权对身份令牌是必需的。</p>
<p><code class="docutils literal notranslate"><span class="pre"><span class="cnblogs_code">prompt</span>&nbsp; &nbsp; &nbsp;</span></code></p>
<p><code class="docutils literal notranslate"><span class="pre">　　&nbsp;</span></code><span class="cnblogs_code">none</span>&nbsp;&nbsp;请求期间不会显示任何UI。 如果无法做到这一点（例如，因为用户必须登录或同意），则会返回错误</p>
<p class="first">　　 &nbsp;<span class="cnblogs_code">login</span>&nbsp;&nbsp;即使用户已登录并具有有效会话，也会显示登录UI</p>
<p><code class="docutils literal notranslate"><span class="pre"><span class="cnblogs_code">code_challenge</span>&nbsp;<br /></span></code></p>
<p>发送PKCE的代码质询</p>
<p><span class="cnblogs_code">code_challenge_method</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">plain</span>&nbsp;plain表示使用纯文本&nbsp;<code class="docutils literal notranslate"><span class="pre">S256</span></code>&nbsp;S256表示使用SHA256进行哈希处理</p>
<p><span class="cnblogs_code">login_hint</span>&nbsp;</p>
<p>可用于预先填写登录页面上的用户名字段</p>
<p><span class="cnblogs_code">ui_locales</span>&nbsp;</p>
<p>提供有关登录UI所需显示语言的提示</p>
<p><span class="cnblogs_code">max_age</span>&nbsp;</p>
<p>如果用户的登录会话超过最大时间（以秒为单位），将显示登录UI</p>
<p><span class="cnblogs_code">acr_values</span>&nbsp;</p>
<p class="first">允许传递额外的身份验证相关信息 - 身份服务器特殊情况下面的私有acr_values：</p>
<blockquote class="last">
<div>
<p>&nbsp;<span class="cnblogs_code">idp:name_of_idp</span>&nbsp;&nbsp;绕过login / home领域屏幕并将用户直接转发到选定的身份提供者（如果允许每个客户端配置）</p>
<p>&nbsp;<span class="cnblogs_code">tenant:name_of_tenant</span>&nbsp;&nbsp;可用于将租户名称传递给登录UI</p>





</div>





</blockquote>
<p>案例：</p>
<div class="cnblogs_code">
<pre>GET /connect/authorize?<span style="color: #000000;">
    client_id</span>=client1&amp;<span style="color: #000000;">
    scope</span>=openid email api1&amp;<span style="color: #000000;">
    response_type</span>=id_token token&amp;<span style="color: #000000;">
    redirect_uri</span>=https:<span style="color: #008000;">//</span><span style="color: #008000;">myapp/callback&amp;</span>
    state=abc&amp;<span style="color: #000000;">
    nonce</span>=xyz</pre>
</div>
<p>（删除了URL编码，并添加了换行符以提高可读性）</p>
<p>&nbsp;</p>
<h2>IdentityModel</h2>
<p>您可以使用IdentityModel库以编程方式为授权端点创建URL：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> request = <span style="color: #0000ff;">new</span><span style="color: #000000;"> RequestUrl(doc.AuthorizeEndpoint);
</span><span style="color: #0000ff;">var</span> url =<span style="color: #000000;"> request.CreateAuthorizeUrl(
    clientId:     </span><span style="color: #800000;">"</span><span style="color: #800000;">client</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    responseType: OidcConstants.ResponseTypes.CodeIdToken,
    responseMode: OidcConstants.ResponseModes.FormPost,
    redirectUri: </span><span style="color: #800000;">"</span><span style="color: #800000;">https://myapp.com/callback</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    state:       CryptoRandom.CreateUniqueId(),
    nonce:       CryptoRandom.CreateUniqueId());</span></pre>
</div>
<p>..并解析响应：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> response = <span style="color: #0000ff;">new</span><span style="color: #000000;"> AuthorizeResponse(callbackUrl);

</span><span style="color: #0000ff;">var</span> accessToken =<span style="color: #000000;"> response.AccessToken;
</span><span style="color: #0000ff;">var</span> idToken =<span style="color: #000000;"> response.IdentityToken;
</span><span style="color: #0000ff;">var</span> state = response.State;</pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">三、令牌端点<a name="a3"></a></span></strong></span></p>
<p>&nbsp;令牌端点可用于以编程方式请求令牌。 它支持password，authorization_code，client_credentials和refresh_token grant types。 此外，可以扩展令牌端点以支持扩展授权类型。</p>
<p><code class="docutils literal notranslate"><span class="pre">client_id</span></code></p>
<p>客户标识符（必填）</p>
<p><code class="docutils literal notranslate"><span class="pre">client_secret</span></code></p>
<p>客户端密钥要么在post主体中，要么作为基本的身份验证头。</p>
<p><code class="docutils literal notranslate"><span class="pre">grant_type</span></code></p>
<p><code class="docutils literal notranslate"><span class="pre">　　authorization_code</span></code>,&nbsp;<code class="docutils literal notranslate"><span class="pre">client_credentials</span></code>,&nbsp;<code class="docutils literal notranslate"><span class="pre">password</span></code>,&nbsp;<code class="docutils literal notranslate"><span class="pre">refresh_token</span></code>&nbsp;or 自定义</p>
<p><code class="docutils literal notranslate"><span class="pre">scope</span></code></p>
<p>一个或多个注册范围。如果没有指定，将发出所有显式允许作用域的令牌。</p>
<p><code class="docutils literal notranslate"><span class="pre">redirect_uri</span></code></p>
<p>authorization_code授权类型所必需的</p>
<p><code class="docutils literal notranslate"><span class="pre">code</span></code></p>
<p>授权码（authorization_code授权类型所需）</p>
<p><code class="docutils literal notranslate"><span class="pre">code_verifier</span></code></p>
<p>PKCE证明密钥</p>
<p><code class="docutils literal notranslate"><span class="pre">username</span></code></p>
<p>资源所有者用户名（密码授权类型所需）</p>
<p><code class="docutils literal notranslate"><span class="pre">password</span></code></p>
<p>资源所有者密码（密码授权类型所需）</p>
<p><code class="docutils literal notranslate"><span class="pre">acr_values</span></code></p>
<p class="first">允许传递密码授予类型的其他身份验证相关信息 - identityserver特殊情况下面的专有acr_values：</p>
<blockquote class="last">
<div>
<p><code class="docutils literal notranslate"><span class="pre">idp:name_of_idp</span></code>&nbsp;绕过login / home领域屏幕并将用户直接转发到选定的身份提供者（如果允许每个客户端配置）</p>
<p><code class="docutils literal notranslate"><span class="pre">tenant:name_of_tenant</span></code>&nbsp;可用于将租户名称传递给令牌端点</p>
</div>
</blockquote>
<p><code class="docutils literal notranslate"><span class="pre">refresh_token</span></code></p>
<p>刷新令牌（refresh_token授权类型所需）</p>
<p><strong>案例</strong></p>
<div class="cnblogs_code">
<pre>POST /connect/<span style="color: #000000;">token

    client_id</span>=client1&amp;<span style="color: #000000;">
    client_secret</span>=secret&amp;<span style="color: #000000;">
    grant_type</span>=authorization_code&amp;<span style="color: #000000;">
    code</span>=hdh922&amp;<span style="color: #000000;">
    redirect_uri</span>=https:<span style="color: #008000;">//</span><span style="color: #008000;">myapp.com/callback</span></pre>
</div>
<p>（为了便于阅读，删除了表格编码并添加了换行符）</p>
<h2>IdentityModel</h2>
<p>您可以使用IdentityModel库以编程方式访问令牌端点：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> client = <span style="color: #0000ff;">new</span><span style="color: #000000;"> TokenClient(
    doc.TokenEndpoint,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">client_id</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">secret</span><span style="color: #800000;">"</span><span style="color: #000000;">);

</span><span style="color: #0000ff;">var</span> response = <span style="color: #0000ff;">await</span> client.RequestAuthorizationCodeAsync(<span style="color: #800000;">"</span><span style="color: #800000;">hdh922</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">https://myapp.com/callback</span><span style="color: #800000;">"</span><span style="color: #000000;">);
</span><span style="color: #0000ff;">var</span> token = response.AccessToken;</pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">四、UserInfo端点<a name="a4"></a></span></strong></span></p>
<p>UserInfo端点可用于检索有关用户的身份信息（请参阅规范）。&nbsp;</p>
<p>调用者需要发送代表用户的有效访问令牌。 根据授予的范围，UserInfo端点将返回映射的声明（至少需要openid作用域）。</p>
<p><strong>案例</strong></p>
<div class="cnblogs_code">
<pre>GET /connect/<span style="color: #000000;">userinfo
Authorization: Bearer </span>&lt;access_token&gt;</pre>
</div>
<div class="cnblogs_code">
<pre>HTTP/<span style="color: #800080;">1.1</span> <span style="color: #800080;">200</span><span style="color: #000000;"> OK
Content</span>-Type: application/<span style="color: #000000;">json

{
    </span><span style="color: #800000;">"</span><span style="color: #800000;">sub</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">248289761001</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">Bob Smith</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">given_name</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">Bob</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">family_name</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">Smith</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">role</span><span style="color: #800000;">"</span><span style="color: #000000;">: [
        </span><span style="color: #800000;">"</span><span style="color: #800000;">user</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">admin</span><span style="color: #800000;">"</span><span style="color: #000000;">
    ]
}</span></pre>
</div>
<h2>IdentityModel</h2>
<p>您可以使用IdentityModel库以编程方式访问userinfo端点：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> userInfoClient = <span style="color: #0000ff;">new</span><span style="color: #000000;"> UserInfoClient(doc.UserInfoEndpoint, token);

</span><span style="color: #0000ff;">var</span> response = <span style="color: #0000ff;">await</span><span style="color: #000000;"> userInfoClient.GetAsync();
</span><span style="color: #0000ff;">var</span> claims = response.Claims;</pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">五、Introspection端点<a name="a5"></a></span></strong></span></p>
<p>内省端点是RFC 7662的实现。&nbsp;</p>
<p>它可用于验证引用令牌（如果消费者不支持适当的JWT或加密库，则可以使用JWT）。 内省端点需要使用范围密钥进行身份验证。</p>
<p><strong>案例</strong></p>
<div class="cnblogs_code">
<pre>POST /connect/<span style="color: #000000;">introspect
Authorization: Basic xxxyyy

token</span>=&lt;token&gt;</pre>
</div>
<p>成功的响应将返回状态代码200以及活动或非活动令牌：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">{
    </span><span style="color: #800000;">"</span><span style="color: #800000;">active</span><span style="color: #800000;">"</span>: <span style="color: #0000ff;">true</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">sub</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">123</span><span style="color: #800000;">"</span><span style="color: #000000;">
}</span></pre>
</div>
<p>未知或过期的令牌将被标记为无效：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">{
    </span><span style="color: #800000;">"</span><span style="color: #800000;">active</span><span style="color: #800000;">"</span>: <span style="color: #0000ff;">false</span><span style="color: #000000;">,
}</span></pre>
</div>
<p>无效请求将返回400，未授权请求401。</p>
<h2>IdentityModel</h2>
<p>您可以使用IdentityModel库以编程方式访问内省端点：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> introspectionClient = <span style="color: #0000ff;">new</span><span style="color: #000000;"> IntrospectionClient(
    doc.IntrospectionEndpoint,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">api_name</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">api_secret</span><span style="color: #800000;">"</span><span style="color: #000000;">);

</span><span style="color: #0000ff;">var</span> response = <span style="color: #0000ff;">await</span><span style="color: #000000;"> introspectionClient.SendAsync(
    </span><span style="color: #0000ff;">new</span> IntrospectionRequest { Token =<span style="color: #000000;"> token });

</span><span style="color: #0000ff;">var</span> isActive =<span style="color: #000000;"> response.IsActive;
</span><span style="color: #0000ff;">var</span> claims = response.Claims;</pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">六、撤销端点<a name="a6"></a></span></strong></span></p>
<p>此端点允许撤消访问令牌（仅限引用令牌）和刷新令牌。 它实现了令牌撤销规范（RFC 7009）。&nbsp;</p>
<p><code class="docutils literal notranslate"><span class="pre">token</span></code></p>
<p>要撤销的令牌（必填）</p>
<p><code class="docutils literal notranslate"><span class="pre">token_type_hint</span></code></p>
<p>access_token或refresh_token（可选）</p>
<p><strong>案例</strong></p>
<div class="cnblogs_code">
<pre>POST /connect/revocation HTTP/<span style="color: #800080;">1.1</span><span style="color: #000000;">
Host: server.example.com
Content</span>-Type: application/x-www-form-<span style="color: #000000;">urlencoded
Authorization: Basic czZCaGRSa3F0MzpnWDFmQmF0M2JW

token</span>=45ghiukldjahdnhzdauz&amp;token_type_hint=refresh_token</pre>
</div>
<h2>IdentityModel</h2>
<p>您可以使用IdentityModel库以编程方式撤消令牌：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> revocationClient = <span style="color: #0000ff;">new</span><span style="color: #000000;"> TokenRevocationClient(
    RevocationEndpoint,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">client</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">secret</span><span style="color: #800000;">"</span><span style="color: #000000;">);

</span><span style="color: #0000ff;">var</span> response = <span style="color: #0000ff;">await</span> revocationClient.RevokeAccessTokenAsync(token);</pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">七、结束会话端点<a name="a7"></a></span></strong></span></p>
<p>&nbsp;结束会话端点可用于触发单点注销（请参阅规范）。</p>
<p>要使用结束会话端点，客户端应用程序会将用户的浏览器重定向到结束会话URL。 用户在会话期间通过浏览器登录的所有应用程序都可以参与注销。</p>
<h2>Parameters</h2>
<p><strong>id_token_hint</strong></p>
<p>当用户被重定向到端点时，系统会提示他们是否真的想要注销。 发送从身份验证收到的原始id_token的客户端可以绕过此提示。 它作为名为id_token_hint的查询字符串参数传递。</p>
<p><strong>post_logout_redirect_uri</strong></p>
<p>如果传递了有效的id_token_hint，则客户端也可以发送post_logout_redirect_uriparameter。 这可用于允许用户在注销后重定向回客户端。 该值必须与客户端预先配置的PostLogoutRedirectUris（客户端文档）之一匹配。</p>
<p><strong>state</strong></p>
<p>如果传递了有效的post_logout_redirect_uri，则客户端也可以发送状态参数。 在用户重定向回客户端后，这将作为查询字符串参数返回给客户端。 这通常由客户端用于跨重定向的往返状态。</p>
<p><strong>案例</strong></p>
<div class="cnblogs_code">
<pre>GET /connect/endsession?id_token_hint=eyJhbGciOiJSUzI1NiIsImtpZCI6IjdlOGFkZmMzMjU1OTEyNzI0ZDY4NWZmYmIwOThjNDEyIiwidHlwIjoiSldUIn0.eyJuYmYiOjE0OTE3NjUzMjEsImV4cCI6MTQ5MTc2NTYyMSwiaXNzIjoiaHR0cDovL2xvY2FsaG9zdDo1MDAwIiwiYXVkIjoianNfb2lkYyIsIm5vbmNlIjoiYTQwNGFjN2NjYWEwNGFmNzkzNmJjYTkyNTJkYTRhODUiLCJpYXQiOjE0OTE3NjUzMjEsInNpZCI6IjI2YTYzNWVmOTQ2ZjRiZGU3ZWUzMzQ2ZjFmMWY1NTZjIiwic3ViIjoiODg0MjExMTMiLCJhdXRoX3RpbWUiOjE0OTE3NjUzMTksImlkcCI6ImxvY2FsIiwiYW1yIjpbInB3ZCJdfQ.STzOWoeVYMtZdRAeRT95cMYEmClixWkmGwVH2Yyiks9BETotbSZiSfgE5kRh72kghN78N3-RgCTUmM2edB3bZx4H5ut3wWsBnZtQ2JLfhTwJAjaLE9Ykt68ovNJySbm8hjZhHzPWKh55jzshivQvTX0GdtlbcDoEA1oNONxHkpDIcr3pRoGi6YveEAFsGOeSQwzT76aId-rAALhFPkyKnVc-uB8IHtGNSyRWLFhwVqAdS3fRNO7iIs5hYRxeFSU7a5ZuUqZ6RRi-bcDhI-djKO5uAwiyhfpbpYcaY_TxXWoCmq8N8uAw9zqFsQUwcXymfOAi2UF3eFZt02hBu-shKA&amp;post_logout_redirect_uri=http%3A%2F%2Flocalhost%3A7017%<span style="color: #000000;">2Findex.html
Next  Previous</span></pre>
</div>
<p>&nbsp;</p>