<p><a href="#a1">一、设置和概述</a></p>
<p><a href="#a2">二、使用客户端凭证保护API</a></p>
<p><a href="#a3">三、使用密码保护API</a></p>
<p><a href="#a4">四、使用OpenID Connect添加用户验证</a></p>
<p><a href="#a5">五、添加对外部认证的支持</a></p>
<p><a href="#a6">六、切换到Hybrid Flow并添加API访问权限</a></p>
<p><a href="#a7">七、Using ASP.NET Core Identity</a></p>
<p><a href="#a8">八、添加一个JavaScript客户端</a></p>
<p><a href="#a9">九、使用EntityFramework core进行配置和操作数据</a></p>
<p><a href="#a10">十、社区快速入门&amp;样品</a></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">一、设置和概述<a name="a1"></a></span></strong></p>
<p>1，使用&nbsp;<span class="cnblogs_code">dotnet <span style="color: #0000ff;">new</span> mvc</span>&nbsp;创建一个mvc项目</p>
<p>2，nuget&nbsp;<span class="cnblogs_code">IdentityServer4</span>&nbsp;</p>
<p>3，修改Startup</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Startup
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> ConfigureServices(IServiceCollection services)
    {
        services.AddIdentityServer()</span><span style="color: #008000;">//</span><span style="color: #008000;">在DI中注册IdentityServer服务，它还为运行时状态注册一个内存存储</span>
            .AddDeveloperSigningCredential();<span style="color: #008000;">//</span><span style="color: #008000;">设置临时签名凭证</span>
<span style="color: #000000;">    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configure(IApplicationBuilder app, IHostingEnvironment env)
    {
        </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (env.IsDevelopment())
        {
            app.UseDeveloperExceptionPage();
        }

        app.UseIdentityServer();
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff; font-size: 18pt;"><strong>二、使用客户端凭证保护API<a name="a2"></a></strong></span></p>
<p>在这个场景中，我们将定义一个API和一个希望访问它的客户端。客户端将在IdentityServer中请求访问令牌，并使用它获得对API的访问。&nbsp;</p>
<p><strong><span style="font-size: 14pt;">定义API</span></strong></p>
<p>创建一个Config,cs文件，在该文件中定义您希望保护的系统中的资源，例如api。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> IEnumerable&lt;ApiResource&gt;<span style="color: #000000;"> GetApiResources()
{
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> List&lt;ApiResource&gt;<span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">new</span> ApiResource(<span style="color: #800000;">"</span><span style="color: #800000;">api1</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">My API</span><span style="color: #800000;">"</span><span style="color: #000000;">)
    };
}</span></pre>
</div>
<p><strong><span style="font-size: 14pt;">定义Client</span></strong></p>
<p>定义访问这个api的client</p>
<p>对于此场景，客户端将没有交互式用户，并将使用所谓的client secret与IdentityServer进行身份验证。将以下代码添加到配置中。cs文件:</p>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> IEnumerable&lt;Client&gt;<span style="color: #000000;"> GetClient()
        {
            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> List&lt;Client&gt;<span style="color: #000000;">()
            {
                </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> Client(){
                    ClientId</span>=<span style="color: #800000;">"</span><span style="color: #800000;">client</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    </span><span style="color: #008000;">//</span><span style="color: #008000;">没有交互式用户，使用clientid/secret进行身份验证</span>
                    AllowedGrantTypes=<span style="color: #000000;">GrantTypes.ClientCredentials,
                    </span><span style="color: #008000;">//</span><span style="color: #008000;">secret认证</span>
                    ClientSecrets={<span style="color: #0000ff;">new</span> Secret(<span style="color: #800000;">"</span><span style="color: #800000;">secret</span><span style="color: #800000;">"</span><span style="color: #000000;">.Sha256())},
                    </span><span style="color: #008000;">//</span><span style="color: #008000;">客户端有权访问的范围</span>
                    AllowedScopes={<span style="color: #800000;">"</span><span style="color: #800000;">api</span><span style="color: #800000;">"</span><span style="color: #000000;">}
                }
            };
        }</span></pre>
</div>
<p><strong><span style="font-size: 14pt;">配置IdentityServer</span></strong></p>
<p>在ConfigureServices添加AddInMemoryApiResources与AddInMemoryClients方法</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> ConfigureServices(IServiceCollection services)
{
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> configure identity server with in-memory stores, keys, clients and resources</span>
<span style="color: #000000;">    services.AddIdentityServer()
        .AddDeveloperSigningCredential()
        .AddInMemoryApiResources(Config.GetApiResources())
        .AddInMemoryClients(Config.GetClients());
}</span></pre>
</div>
<p>打开&nbsp;<span class="cnblogs_code">http:<span style="color: #008000;">//</span><span style="color: #008000;">localhost:5000/.well-known/openid-configuration</span></span>&nbsp;你应该看看所谓的发现文件。您的客户端和api将使用它来下载必要的配置数据。</p>
<p><strong><span style="font-size: 14pt;">添加一个API项目</span></strong></p>
<p>添加一个api项目，将url设置为&nbsp;<span class="cnblogs_code">http:<span style="color: #008000;">//</span><span style="color: #008000;">localhost:5001</span></span>&nbsp;</p>
<p>1，添加controller</p>
<div class="cnblogs_code">
<pre>[Route(<span style="color: #800000;">"</span><span style="color: #800000;">identity</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
[Authorize]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> IdentityController : ControllerBase
{
    [HttpGet]
    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> IActionResult Get()
    {
        </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> JsonResult(<span style="color: #0000ff;">from</span> c <span style="color: #0000ff;">in</span> User.Claims <span style="color: #0000ff;">select</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> { c.Type, c.Value });
    }
}</span></pre>
</div>
<p>2，配置</p>
<p>最后一步是将身份验证服务添加到DI，将身份验证中间件添加到管道。这些将会：</p>
<ul>
<li>验证传入的令牌以确保它来自受信任的颁发者</li>
<li>验证该令牌是否适用于此api（又名scope）</li>
</ul>
<p>nuget&nbsp;<span class="cnblogs_code">IdentityServer4.AccessTokenValidation&nbsp;</span></p>
<p>更新Startup如下</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Startup
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> ConfigureServices(IServiceCollection services)
    {
        services.AddMvcCore()
            .AddAuthorization()
            .AddJsonFormatters();
        </span><span style="color: #008000;">//</span><span style="color: #008000;">AddAuthentication将认证服务添加到DI，并将&ldquo;Bearer&rdquo;配置为默认方案。</span>
        services.AddAuthentication(<span style="color: #800000;">"</span><span style="color: #800000;">Bearer</span><span style="color: #800000;">"</span><span style="color: #000000;">)
            </span><span style="color: #008000;">//</span><span style="color: #008000;">将IdentityServer访问令牌验证处理程序添加到DI中以供验证服务使用</span>
            .AddIdentityServerAuthentication(options =&gt;<span style="color: #000000;">
            {
                options.Authority </span>= <span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:5000</span><span style="color: #800000;">"</span><span style="color: #000000;">;
                options.RequireHttpsMetadata </span>= <span style="color: #0000ff;">false</span><span style="color: #000000;">;

                options.ApiName </span>= <span style="color: #800000;">"</span><span style="color: #800000;">api1</span><span style="color: #800000;">"</span><span style="color: #000000;">;
            });
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configure(IApplicationBuilder app)
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;">UseAuthentication将认证中间件添加到管道，因此每次调用主机时都会自动执行认证。</span>
<span style="color: #000000;">        app.UseAuthentication();

        app.UseMvc();
    }
}</span></pre>
</div>
<p>如果使用浏览器导航到控制器(http://localhost:5001/identity)，则应该得到401状态码作为回报。这意味着您的API需要凭据。<br />就是这样，API现在由IdentityServer保护。</p>
<p><strong><span style="font-size: 14pt;">创建client</span></strong></p>
<p>添加一个console项目</p>
<p>IdentityServer中的令牌端点实现OAuth 2.0协议，您可以使用原始HTTP访问它。但是，我们有一个名为IdentityModel的客户端库，它将协议交互封装在一个易于使用的API中。</p>
<p>nuget&nbsp;<span class="cnblogs_code">IdentityModel</span>&nbsp;</p>
<p>IdentityModel包含一个用于发现端点的客户端库。 这样您只需要知道IdentityServer的基地址 - 可以从元数据中读取实际的端点地址：</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> 从元数据发现端点</span>
<span style="color: #0000ff;">var</span> disco = <span style="color: #0000ff;">await</span> DiscoveryClient.GetAsync(<span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:5000</span><span style="color: #800000;">"</span><span style="color: #000000;">);
</span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (disco.IsError)
{
    Console.WriteLine(disco.Error);
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;">;
}</span></pre>
</div>
<p>接下来，您可以使用TokenClient类来请求令牌。 要创建实例，您需要传入令牌端点地址，client ID和secret。</p>
<p>接下来，您可以使用requestcredenticlientalsasync方法为您的API请求一个令牌:</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> request token</span>
<span style="color: #0000ff;">var</span> tokenClient = <span style="color: #0000ff;">new</span> TokenClient(disco.TokenEndpoint, <span style="color: #800000;">"</span><span style="color: #800000;">client</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">secret</span><span style="color: #800000;">"</span><span style="color: #000000;">);
</span><span style="color: #0000ff;">var</span> tokenResponse = <span style="color: #0000ff;">await</span> tokenClient.RequestClientCredentialsAsync(<span style="color: #800000;">"</span><span style="color: #800000;">api1</span><span style="color: #800000;">"</span><span style="color: #000000;">);

</span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (tokenResponse.IsError)
{
    Console.WriteLine(tokenResponse.Error);
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;">;
}

Console.WriteLine(tokenResponse.Json);//将access token赋值到https://jwt.io/可以查看详细信息</span></pre>
</div>
<p>最后一步是调用API。<br />要将访问令牌发送到API，通常使用HTTP授权头。这是使用SetBearerToken扩展方法完成的:</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> call api</span>
<span style="color: #0000ff;">var</span> client = <span style="color: #0000ff;">new</span><span style="color: #000000;"> HttpClient();
client.SetBearerToken(tokenResponse.AccessToken);

</span><span style="color: #0000ff;">var</span> response = <span style="color: #0000ff;">await</span> client.GetAsync(<span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:5001/identity</span><span style="color: #800000;">"</span><span style="color: #000000;">);
</span><span style="color: #0000ff;">if</span> (!<span style="color: #000000;">response.IsSuccessStatusCode)
{
    Console.WriteLine(response.StatusCode);
}
</span><span style="color: #0000ff;">else</span><span style="color: #000000;">
{
    </span><span style="color: #0000ff;">var</span> content = <span style="color: #0000ff;">await</span><span style="color: #000000;"> response.Content.ReadAsStringAsync();
    Console.WriteLine(JArray.Parse(content));
}</span></pre>
</div>
<p>&nbsp;案例下载：<a href="https://pan.baidu.com/s/1xYxymmnn6giMUphnnCGaaQ" target="_blank">https://pan.baidu.com/s/1xYxymmnn6giMUphnnCGaaQ</a></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">三、使用密码保护API<a name="a3"></a></span></strong></span></p>
<p>客户端输入用户名和密码获取访问令牌，通过访问令牌访问资源，该规范建议仅将&ldquo;资源所有者密码授予&rdquo;用于&ldquo;可信&rdquo;应用程序</p>
<p><strong><span style="font-size: 14pt;">添加用户</span></strong></p>
<p>TestUser类表示测试用户。 让我们通过将以下代码添加到我们的配置类来创建几个用户：</p>
<p>首先将以下using语句添加到Config.cs文件中：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> IdentityServer4.Test;

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> List&lt;TestUser&gt;<span style="color: #000000;"> GetUsers()
{
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> List&lt;TestUser&gt;<span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> TestUser
        {
            SubjectId </span>= <span style="color: #800000;">"</span><span style="color: #800000;">1</span><span style="color: #800000;">"</span><span style="color: #000000;">,
            Username </span>= <span style="color: #800000;">"</span><span style="color: #800000;">alice</span><span style="color: #800000;">"</span><span style="color: #000000;">,
            Password </span>= <span style="color: #800000;">"</span><span style="color: #800000;">password</span><span style="color: #800000;">"</span><span style="color: #000000;">
        },
        </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> TestUser
        {
            SubjectId </span>= <span style="color: #800000;">"</span><span style="color: #800000;">2</span><span style="color: #800000;">"</span><span style="color: #000000;">,
            Username </span>= <span style="color: #800000;">"</span><span style="color: #800000;">bob</span><span style="color: #800000;">"</span><span style="color: #000000;">,
            Password </span>= <span style="color: #800000;">"</span><span style="color: #800000;">password</span><span style="color: #800000;">"</span><span style="color: #000000;">
        }
    };
}</span></pre>
</div>
<p>然后向IdentityServer注册测试用户：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> ConfigureServices(IServiceCollection services)
{
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> configure identity server with in-memory stores, keys, clients and scopes</span>
<span style="color: #000000;">    services.AddIdentityServer()
        .AddDeveloperSigningCredential()
        .AddInMemoryApiResources(Config.GetApiResources())
        .AddInMemoryClients(Config.GetClients())
        .AddTestUsers(Config.GetUsers());
}</span></pre>
</div>
<p>AddTestUsers扩展方法在底层做了几件事情</p>
<ul>
<li>增加了对资源所有者密码授权的支持</li>
<li>增加了对登录UI通常使用的用户相关服务的支持</li>
<li>基于测试用户添加了对配置文件服务的支持</li>
</ul>
<p><strong><span style="font-size: 14pt;">配置一个支持密码授权的客户端</span></strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> IEnumerable&lt;Client&gt;<span style="color: #000000;"> GetClients()
{
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> List&lt;Client&gt;<span style="color: #000000;">
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> other clients omitted...

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> resource owner password grant client</span>
        <span style="color: #0000ff;">new</span><span style="color: #000000;"> Client
        {
            ClientId </span>= <span style="color: #800000;">"</span><span style="color: #800000;">ro.client</span><span style="color: #800000;">"</span><span style="color: #000000;">,
            AllowedGrantTypes </span>=<span style="color: #000000;"> GrantTypes.ResourceOwnerPassword,

            ClientSecrets </span>=<span style="color: #000000;">
            {
                </span><span style="color: #0000ff;">new</span> Secret(<span style="color: #800000;">"</span><span style="color: #800000;">secret</span><span style="color: #800000;">"</span><span style="color: #000000;">.Sha256())
            },
            AllowedScopes </span>= { <span style="color: #800000;">"</span><span style="color: #800000;">api1</span><span style="color: #800000;">"</span><span style="color: #000000;"> }
        }
    };
}</span></pre>
</div>
<p><strong><span style="font-size: 14pt;">使用密码授予请求令牌</span></strong></p>
<p>客户端看起来非常类似于我们为客户端凭据授权所做的操作。 主要区别在于客户端会以某种方式收集用户的密码，并在令牌请求期间将其发送给令牌服务。</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> request token</span>
<span style="color: #0000ff;">var</span> tokenClient = <span style="color: #0000ff;">new</span> TokenClient(disco.TokenEndpoint, <span style="color: #800000;">"</span><span style="color: #800000;">ro.client</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">secret</span><span style="color: #800000;">"</span><span style="color: #000000;">);
</span><span style="color: #0000ff;">var</span> tokenResponse = <span style="color: #0000ff;">await</span> tokenClient.RequestResourceOwnerPasswordAsync(<span style="color: #800000;">"</span><span style="color: #800000;">alice</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">password</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">api1</span><span style="color: #800000;">"</span><span style="color: #000000;">);

</span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (tokenResponse.IsError)
{
    Console.WriteLine(tokenResponse.Error);
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;">;
}

Console.WriteLine(tokenResponse.Json);
Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">\n\n</span><span style="color: #800000;">"</span>);</pre>
</div>
<p>案例下载：<a href="https://pan.baidu.com/s/1q-UYw_34hX00MqxiZp524g" target="_blank">https://pan.baidu.com/s/1q-UYw_34hX00MqxiZp524g</a></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">四、使用OpenID Connect添加用户验证<a name="a4"></a></span></strong></span></p>
<p><strong><span style="font-size: 14pt;">添加UI</span></strong></p>
<p>OpenID Connect所需的所有协议支持都已内置到IdentityServer中。 您需要为登录，注销，同意和错误提供必要的UI部分。</p>
<p>虽然每个IdentityServer实现的外观和感觉以及确切的工作流程可能总是不同，但我们提供了一个基于MVC的示例UI，您可以将其用作起点。</p>
<p>这个用户界面可以在Quickstart UI仓库中找到。 您可以克隆或下载此repo，并将控制器，视图，模型和CSS放入您的IdentityServer Web应用程序。</p>
<p>创建一个MVC应用，然后将&nbsp;Quickstart UI复制到项目中，nuget&nbsp;&nbsp;<span class="cnblogs_code">IdentityServer4</span>&nbsp;。并配置Startup：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> ConfigureServices(IServiceCollection services)
{
    services.AddMvc();

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> configure identity server with in-memory stores, keys, clients and scopes</span>
<span style="color: #000000;">    services.AddIdentityServer()
        .AddDeveloperSigningCredential()
        .AddInMemoryApiResources(Config.GetApiResources())
        .AddInMemoryClients(Config.GetClients())
        .AddTestUsers(Config.GetUsers());
}</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
    }

    app.UseIdentityServer();

    app.UseStaticFiles();
    app.UseMvcWithDefaultRoute();
}</span></pre>
</div>
<p><strong><span style="font-size: 14pt;">创建一个MVC客户端&nbsp;</span></strong></p>
<p>要将OpenID Connect身份验证支持添加到MVC应用程序，请将以下内容添加到启动时的ConfigureServices中：&nbsp;</p>
<div class="cnblogs_code">
<pre>            <span style="color: #008000;">//</span><span style="color: #008000;">AddAuthentication将认证服务添加到DI</span>
            services.AddAuthentication(options=&gt;<span style="color: #000000;">{
                options.DefaultScheme</span>=<span style="color: #800000;">"</span><span style="color: #800000;">Cookies</span><span style="color: #800000;">"</span>;<span style="color: #008000;">//</span><span style="color: #008000;">设置Cookies为主要认证手段</span>
                options.DefaultChallengeScheme=<span style="color: #800000;">"</span><span style="color: #800000;">oidc</span><span style="color: #800000;">"</span>;<span style="color: #008000;">//</span><span style="color: #008000;">当需要登录时使用OpenID Connect方案</span>
<span style="color: #000000;">            })
            .AddCookie(</span><span style="color: #800000;">"</span><span style="color: #800000;">Cookies</span><span style="color: #800000;">"</span>)<span style="color: #008000;">//</span><span style="color: #008000;">使用AddCookie添加可以处理cookie的处理程序。</span>
            .AddOpenIdConnect(<span style="color: #800000;">"</span><span style="color: #800000;">oidc</span><span style="color: #800000;">"</span>,options=&gt;<span style="color: #000000;">{
                options.SignInScheme</span>=<span style="color: #800000;">"</span><span style="color: #800000;">Cookies</span><span style="color: #800000;">"</span><span style="color: #000000;">;
                options.Authority</span>=<span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:5000</span><span style="color: #800000;">"</span><span style="color: #000000;">;
                options.RequireHttpsMetadata</span>=<span style="color: #0000ff;">false</span><span style="color: #000000;">;
                options.ClientId</span>=<span style="color: #800000;">"</span><span style="color: #800000;">client</span><span style="color: #800000;">"</span><span style="color: #000000;">;
                options.SaveTokens</span>=<span style="color: #0000ff;">true</span><span style="color: #000000;">;
            });</span></pre>
</div>
<p>AddOpenIdConnect用于配置执行OpenID连接协议的处理程序。授权表明我们信任身份服务器。然后我们通过ClientId识别这个客户端。一旦OpenID连接协议完成，SignInScheme将使用cookie处理程序发出cookie。</p>
<p>savetoken用于将标识符从IdentityServer中持久化到cookie中(稍后需要它们)。</p>
<p>此外，我们关闭了JWT声明类型映射，以允许众所周知的声明（例如'sub'和'idp'）通过非混淆的声明：&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">JwtSecurityTokenHandler.DefaultInboundClaimTypeMap.Clear();</span>&nbsp;&nbsp;</p>
<p>&nbsp;然后为了确保验证服务在每个请求上执行，请添加UseAuthentication以在启动时进行配置：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
    }
    </span><span style="color: #0000ff;">else</span><span style="color: #000000;">
    {
        app.UseExceptionHandler(</span><span style="color: #800000;">"</span><span style="color: #800000;">/Home/Error</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    }

    app.UseAuthentication();//认证中间件应该在管道中的MVC之前添加。

    app.UseStaticFiles();
    app.UseMvcWithDefaultRoute();
}</span></pre>
</div>
<p><strong><span style="font-size: 14pt;">添加对OpenID Connect Identity Scopes的支持</span></strong></p>
<p>与OAuth 2.0类似，OpenID Connect也使用了作用域概念。同样，作用域表示您希望保护和客户端希望访问的内容。与OAuth相反，OIDC中的作用域并不表示api，而是用户id、名称或电子邮件地址等标识数据。</p>
<p>在Config.cs中创建一个IdentityResource对象集合，添加对标准openid(subject id)和profile(名字，姓氏等)作用域的支持</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> IEnumerable&lt;IdentityResource&gt;<span style="color: #000000;"> GetIdentityResources()
{
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> List&lt;IdentityResource&gt;<span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> IdentityResources.OpenId(),
        </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> IdentityResources.Profile(),
    };
}</span></pre>
</div>
<p>修改Startup</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> ConfigureServices(IServiceCollection services)
{
    services.AddMvc();

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> configure identity server with in-memory stores, keys, clients and scopes</span>
<span style="color: #000000;">    services.AddIdentityServer()
        .AddDeveloperSigningCredential()
        .AddInMemoryIdentityResources(Config.GetIdentityResources())
        .AddInMemoryApiResources(Config.GetApiResources())
        .AddInMemoryClients(Config.GetClients())
        .AddTestUsers(Config.GetUsers());
}</span></pre>
</div>
<p><strong><span style="font-size: 14pt;">为OpenID Connect隐式流添加客户端</span></strong></p>
<p>最后一步是将MVC客户端的新配置条目添加到IdentityServer。</p>
<p>基于OpenID Connect的客户端与我们迄今添加的OAuth 2.0客户端非常相似。 但由于OIDC中的流程始终是交互式的，因此我们需要将一些重定向URL添加到我们的配置中。</p>
<p>将以下内容添加到客户端配置中：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> IEnumerable&lt;Client&gt;<span style="color: #000000;"> GetClients()
{
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> List&lt;Client&gt;<span style="color: #000000;">
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 其他客户被忽略...

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> OpenID Connect隐式流程客户端（MVC）</span>
        <span style="color: #0000ff;">new</span><span style="color: #000000;"> Client
        {
            ClientId </span>= <span style="color: #800000;">"</span><span style="color: #800000;">mvc</span><span style="color: #800000;">"</span><span style="color: #000000;">,
            ClientName </span>= <span style="color: #800000;">"</span><span style="color: #800000;">MVC Client</span><span style="color: #800000;">"</span><span style="color: #000000;">,
            AllowedGrantTypes </span>=<span style="color: #000000;"> GrantTypes.Implicit,

            </span><span style="color: #008000;">//</span><span style="color: #008000;"> 登录后重定向到哪里</span>
            RedirectUris = { <span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:5001/signin-oidc</span><span style="color: #800000;">"</span><span style="color: #000000;"> },

            </span><span style="color: #008000;">//</span><span style="color: #008000;"> 注销后重定向到哪里</span>
            PostLogoutRedirectUris = { <span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:5001/signout-callback-oidc</span><span style="color: #800000;">"</span><span style="color: #000000;"> },

            AllowedScopes </span>= <span style="color: #0000ff;">new</span> List&lt;<span style="color: #0000ff;">string</span>&gt;<span style="color: #000000;">
            {
                IdentityServerConstants.StandardScopes.OpenId,
                IdentityServerConstants.StandardScopes.Profile
            }
        }
    };
}</span></pre>
</div>
<p><strong><span style="font-size: 14pt;">&nbsp;测试客户端</span></strong></p>
<p>现在，最终所有的东西都应该适用于新的MVC客户端。</p>
<p>通过导航到受保护的控制器操作来触发身份验证握手。 您应该看到重定向到IdentityServer的登录页面。</p>
<p>&nbsp;案例下载：<a href="https://pan.baidu.com/s/1XHL4eRzp3oqIK3ubMF-NLQ" target="_blank">https://pan.baidu.com/s/1XHL4eRzp3oqIK3ubMF-NLQ</a></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">五、添加对外部认证的支持<a name="a5"></a></span></strong></p>
<p>接下来我们将添加对外部认证的支持。 这非常简单，因为您真正需要的只是一个兼容ASP.NET Core的身份验证处理程序。&nbsp;</p>
<p>ASP.NET Core本身也支持Google，Facebook，Twitter，Microsoft帐户和OpenID Connect。 另外你可以在这里找到许多其他认证提供者的实现。</p>
<p><strong><span style="font-size: 14pt;">添加Google支持</span></strong></p>
<p>要能够使用谷歌进行身份验证，首先需要向它们注册。这是在开发人员控制台完成的。创建一个新项目，启用谷歌+ API，并通过将/signin-google路径添加到基本地址(例如http://localhost:5000/signin- Google)来配置本地标识服务器的回调地址。</p>
<p>如果您正在端口5000上运行&mdash;&mdash;您可以使用下面代码片段中的客户端id/secret，因为这是我们预先注册的。</p>
<p>首先添加Google身份验证处理程序到DI。 这是通过将此片段添加到启动时的ConfigureServices中完成的：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> ConfigureServices(IServiceCollection services)
{
    services.AddMvc();

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> configure identity server with in-memory stores, keys, clients and scopes</span>
<span style="color: #000000;">    services.AddIdentityServer()
        .AddDeveloperSigningCredential()
        .AddInMemoryIdentityResources(Config.GetIdentityResources())
        .AddInMemoryApiResources(Config.GetApiResources())
        .AddInMemoryClients(Config.GetClients())
        .AddTestUsers(Config.GetUsers());

    services.AddAuthentication()
        .AddGoogle(</span><span style="color: #800000;">"</span><span style="color: #800000;">Google</span><span style="color: #800000;">"</span>, options =&gt;<span style="color: #000000;">
        {
            options.SignInScheme </span>=<span style="color: #000000;"> IdentityServerConstants.ExternalCookieAuthenticationScheme;

            options.ClientId </span>= <span style="color: #800000;">"</span><span style="color: #800000;">434483408261-55tc8n0cs4ff1fe21ea8df2o443v2iuc.apps.googleusercontent.com</span><span style="color: #800000;">"</span><span style="color: #000000;">;
            options.ClientSecret </span>= <span style="color: #800000;">"</span><span style="color: #800000;">3gcoTrEDPPJ0ukn_aYYT6PWo</span><span style="color: #800000;">"</span><span style="color: #000000;">;
        });
}</span></pre>
</div>
<p>默认情况下，IdentityServer专门为外部认证的结果配置cookie处理程序（使用基于常量IdentityServerConstants.ExternalCookieAuthenticationScheme的方案）。 Google处理程序的配置然后使用该cookie处理程序。 为了更好地理解这是如何完成的，请参阅Quickstart文件夹下的AccountController类。</p>
<p><strong><span style="font-size: 14pt;">进一步实验</span></strong></p>
<p>您可以添加一个额外的外部提供者。 我们有一个云托管的IdentityServer4演示版本，您可以使用OpenID Connect进行集成。</p>
<p>将OpenId Connect处理程序添加到DI中：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">services.AddAuthentication()
    .AddGoogle(</span><span style="color: #800000;">"</span><span style="color: #800000;">Google</span><span style="color: #800000;">"</span>, options =&gt;<span style="color: #000000;">
    {
        options.SignInScheme </span>=<span style="color: #000000;"> IdentityServerConstants.ExternalCookieAuthenticationScheme;

        options.ClientId </span>= <span style="color: #800000;">"</span><span style="color: #800000;">434483408261-55tc8n0cs4ff1fe21ea8df2o443v2iuc.apps.googleusercontent.com</span><span style="color: #800000;">"</span><span style="color: #000000;">;
        options.ClientSecret </span>= <span style="color: #800000;">"</span><span style="color: #800000;">3gcoTrEDPPJ0ukn_aYYT6PWo</span><span style="color: #800000;">"</span><span style="color: #000000;">;
    })
    .AddOpenIdConnect(</span><span style="color: #800000;">"</span><span style="color: #800000;">oidc</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">OpenID Connect</span><span style="color: #800000;">"</span>, options =&gt;<span style="color: #000000;">
    {
        options.SignInScheme </span>=<span style="color: #000000;"> IdentityServerConstants.ExternalCookieAuthenticationScheme;
        options.SignOutScheme </span>=<span style="color: #000000;"> IdentityServerConstants.SignoutScheme;

        options.Authority </span>= <span style="color: #800000;">"</span><span style="color: #800000;">https://demo.identityserver.io/</span><span style="color: #800000;">"</span><span style="color: #000000;">;
        options.ClientId </span>= <span style="color: #800000;">"</span><span style="color: #800000;">implicit</span><span style="color: #800000;">"</span><span style="color: #000000;">;

        options.TokenValidationParameters </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> TokenValidationParameters
        {
            NameClaimType </span>= <span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span><span style="color: #000000;">,
            RoleClaimType </span>= <span style="color: #800000;">"</span><span style="color: #800000;">role</span><span style="color: #800000;">"</span><span style="color: #000000;">
        };
    });</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">六、切换到Hybrid Flow并添加API访问权限<a name="a6"></a></span></strong></p>
<p>在前面的快速启动中，我们研究了API访问和用户身份验证。现在我们要把这两个部分结合起来。&nbsp;</p>
<p>OpenID Connect &amp; OAuth 2.0组合的美妙之处在于，您可以通过一个协议和一个与令牌服务的交换来实现。</p>
<p>在前面的quickstart中，我们使用了OpenID连接隐式流。在隐式流中，所有令牌都通过浏览器传输，这对于身份令牌来说是完全没问题的。现在我们还想请求一个访问令牌。</p>
<p>访问令牌比身份令牌更加敏感，如果不需要，我们不希望将它们暴露于&ldquo;外部&rdquo;世界。 OpenID Connect包含一个名为&ldquo;混合流&rdquo;的流程，它可以让我们两全其美，身份令牌通过浏览器通道传输，因此客户可以在做更多工作之前验证它。 如果验证成功，客户端会打开令牌服务的后端通道来检索访问令牌。</p>
<p><strong><span style="font-size: 14pt;">修改client配置</span></strong></p>
<p>没有多少必要的修改。首先，我们希望允许客户端使用混合流，此外，我们还希望客户端允许执行服务器到服务器的API调用，这些调用不在用户的上下文中(这与我们的客户端凭证quickstart非常相似)。使用AllowedGrantTypes属性表示。</p>
<p>接下来，我们需要添加一个客户端secret。这将用于检索后通道上的访问令牌。</p>
<p>最后，我们还为客户端提供了对offline_access范围的访问权限&mdash;&mdash;这允许为长期存在的API访问请求刷新令牌:</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">new</span><span style="color: #000000;"> Client
{
    ClientId </span>= <span style="color: #800000;">"</span><span style="color: #800000;">mvc</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    ClientName </span>= <span style="color: #800000;">"</span><span style="color: #800000;">MVC Client</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    AllowedGrantTypes </span>=<span style="color: #000000;"> GrantTypes.HybridAndClientCredentials,

    ClientSecrets </span>=<span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">new</span> Secret(<span style="color: #800000;">"</span><span style="color: #800000;">secret</span><span style="color: #800000;">"</span><span style="color: #000000;">.Sha256())
    },

    RedirectUris           </span>= { <span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:5002/signin-oidc</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
    PostLogoutRedirectUris </span>= { <span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:5002/signout-callback-oidc</span><span style="color: #800000;">"</span><span style="color: #000000;"> },

    AllowedScopes </span>=<span style="color: #000000;">
    {
        IdentityServerConstants.StandardScopes.OpenId,
        IdentityServerConstants.StandardScopes.Profile,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">api1</span><span style="color: #800000;">"</span><span style="color: #000000;">
    },
    AllowOfflineAccess </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">
};</span></pre>
</div>
<p><strong><span style="font-size: 14pt;">修改MVC客户端</span></strong></p>
<p>MVC客户端的修改也是最小的&mdash;&mdash;ASP.NET核心的OpenID连接处理器对混合流有内置的支持，所以我们只需要更改一些配置值。</p>
<p>我们配置&nbsp;<span class="cnblogs_code">ClientSecret</span>&nbsp;以匹配IdentityServer上的secret。添加&nbsp;<span class="cnblogs_code">offline_access</span>&nbsp;和&nbsp;<span class="cnblogs_code">api1</span>&nbsp;作用域，并将&nbsp;<span class="cnblogs_code">ResponseType</span>&nbsp;设置为&nbsp;<span class="cnblogs_code">code id_token</span>&nbsp;(这基本上意味着&ldquo;使用混合流&rdquo;)</p>
<div class="cnblogs_code">
<pre>.AddOpenIdConnect(<span style="color: #800000;">"</span><span style="color: #800000;">oidc</span><span style="color: #800000;">"</span>, options =&gt;<span style="color: #000000;">
{
    options.SignInScheme </span>= <span style="color: #800000;">"</span><span style="color: #800000;">Cookies</span><span style="color: #800000;">"</span><span style="color: #000000;">;

    options.Authority </span>= <span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:5000</span><span style="color: #800000;">"</span><span style="color: #000000;">;
    options.RequireHttpsMetadata </span>= <span style="color: #0000ff;">false</span><span style="color: #000000;">;

    options.ClientId </span>= <span style="color: #800000;">"</span><span style="color: #800000;">mvc</span><span style="color: #800000;">"</span><span style="color: #000000;">;
    options.ClientSecret </span>= <span style="color: #800000;">"</span><span style="color: #800000;">secret</span><span style="color: #800000;">"</span><span style="color: #000000;">;
    options.ResponseType </span>= <span style="color: #800000;">"</span><span style="color: #800000;">code id_token</span><span style="color: #800000;">"</span><span style="color: #000000;">;

    options.SaveTokens </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">;
    options.GetClaimsFromUserInfoEndpoint </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">;

    options.Scope.Add(</span><span style="color: #800000;">"</span><span style="color: #800000;">api1</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    options.Scope.Add(</span><span style="color: #800000;">"</span><span style="color: #800000;">offline_access</span><span style="color: #800000;">"</span><span style="color: #000000;">);
});</span></pre>
</div>
<p>当您运行MVC客户端时，除了同意屏幕现在要求您提供额外的API和&nbsp;offline access scope外，没有太大区别。</p>
<p><strong><span style="font-size: 14pt;">使用访问令牌</span></strong></p>
<p>OpenID连接中间件为您自动保存令牌(标识、访问和刷新)。这就是savetoken设置的作用。</p>
<p>技术上，令牌存储在cookie的属性部分。 访问它们的最简单方法是使用Microsoft.AspNetCore.Authentication命名空间中的扩展方法。</p>
<p>例如在您的声明视图上：</p>
<div class="cnblogs_code">
<pre>&lt;dt&gt;access token&lt;/dt&gt;
&lt;dd&gt;@await ViewContext.HttpContext.GetTokenAsync(<span style="color: #800000;">"</span><span style="color: #800000;">access_token</span><span style="color: #800000;">"</span>)&lt;/dd&gt;

&lt;dt&gt;refresh token&lt;/dt&gt;
&lt;dd&gt;@await ViewContext.HttpContext.GetTokenAsync(<span style="color: #800000;">"</span><span style="color: #800000;">refresh_token</span><span style="color: #800000;">"</span>)&lt;/dd&gt;</pre>
</div>
<p>要使用访问令牌访问API，您只需检索令牌并将其设置在您的HttpClient上：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task&lt;IActionResult&gt;<span style="color: #000000;"> CallApiUsingUserAccessToken()
{
    </span><span style="color: #0000ff;">var</span> accessToken = <span style="color: #0000ff;">await</span> HttpContext.GetTokenAsync(<span style="color: #800000;">"</span><span style="color: #800000;">access_token</span><span style="color: #800000;">"</span><span style="color: #000000;">);

    </span><span style="color: #0000ff;">var</span> client = <span style="color: #0000ff;">new</span><span style="color: #000000;"> HttpClient();
    client.SetBearerToken(accessToken);
    </span><span style="color: #0000ff;">var</span> content = <span style="color: #0000ff;">await</span> client.GetStringAsync(<span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:5001/identity</span><span style="color: #800000;">"</span><span style="color: #000000;">);

    ViewBag.Json </span>=<span style="color: #000000;"> JArray.Parse(content).ToString();
    </span><span style="color: #0000ff;">return</span> View(<span style="color: #800000;">"</span><span style="color: #800000;">json</span><span style="color: #800000;">"</span><span style="color: #000000;">);
}</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">七、Using ASP.NET Core Identity<a name="a7"></a></span></strong></p>
<p>IdentityServer旨在提供灵活性，其中的一部分允许您为用户及其数据使用任何数据库（包括密码）。 如果你从一个新的用户数据库开始，那么ASP.NET Identity是你可以选择的一个选项。 本快速入门介绍了如何将Identity Identity与Identity Identity一起使用。&nbsp;</p>
<p>这个快速入门假设你已经完成了所有的快速入门。 快速入门使用ASP.NET Identity的方法是从Visual Studio中的ASP.NET Identity模板创建一个新项目。 这个新项目将取代之前在快速入门中从头开始构建的IdentityServer项目。 此解决方案中的所有其他项目（针对客户端和API）将保持不变。</p>
<p><strong><span style="font-size: 14pt;">新建ASP.NET Identity项目&nbsp;</span></strong></p>
<p>第一步是为您的解决方案添加一个ASP.NET Identity的新项目。 鉴于ASP.NET身份需要大量代码，因此使用Visual Studio中的模板是有意义的。 您最终将删除IdentityServer的旧项目（假设您正在关注其他快速入门），但您需要迁移几个项目（或按照之前的快速入门中所述从头开始重写）。</p>
<p>nuget&nbsp;&nbsp;<span class="cnblogs_code">dotnet <span style="color: #0000ff;">new</span> mvc --auth Individual</span>&nbsp;</p>
<p><strong><span style="font-size: 14pt;">修改hosting</span></strong></p>
<p>不要忘记修改主机（如此处所述）以在端口5000上运行。这非常重要，因此现有客户端和API项目将继续运行。</p>
<p><strong><span style="font-size: 14pt;">添加IdentityServer包&nbsp;</span></strong></p>
<p>添加IdentityServer4.AspNetIdentity NuGet包。 这取决于IdentityServer4包，因此会自动添加为传递依赖项。</p>
<p><strong><span style="font-size: 14pt;">Scopes和Clients配置</span></strong></p>
<p>尽管这是IdentityServer的一个新项目，但我们仍需要与之前的快速入门相同的范围和客户端配置。 将用于之前快速入门的配置类（在Config.cs中）复制到此新项目中。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">new</span><span style="color: #000000;"> Client
{
    ClientId </span>= <span style="color: #800000;">"</span><span style="color: #800000;">mvc</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    ClientName </span>= <span style="color: #800000;">"</span><span style="color: #800000;">MVC Client</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    AllowedGrantTypes </span>=<span style="color: #000000;"> GrantTypes.HybridAndClientCredentials,

    RequireConsent </span>= <span style="color: #0000ff;">false</span><span style="color: #000000;">,

    ClientSecrets </span>=<span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">new</span> Secret(<span style="color: #800000;">"</span><span style="color: #800000;">secret</span><span style="color: #800000;">"</span><span style="color: #000000;">.Sha256())
    },

    RedirectUris           </span>= { <span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:5002/signin-oidc</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
    PostLogoutRedirectUris </span>= { <span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:5002/signout-callback-oidc</span><span style="color: #800000;">"</span><span style="color: #000000;"> },

    AllowedScopes </span>=<span style="color: #000000;">
    {
        IdentityServerConstants.StandardScopes.OpenId,
        IdentityServerConstants.StandardScopes.Profile,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">api1</span><span style="color: #800000;">"</span><span style="color: #000000;">
    },
    AllowOfflineAccess </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">
}</span></pre>
</div>
<p><strong><span style="font-size: 14pt;">配置IdentityServer</span></strong></p>
<p>与前面一样，需要在Configure reservices中和Startup.cs中配置IdentityServer。</p>
<p>ConfigureServices</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> ConfigureServices(IServiceCollection services)
{
    services.AddDbContext</span>&lt;ApplicationDbContext&gt;(options =&gt;<span style="color: #000000;">
        options.UseSqlServer(Configuration.GetConnectionString(</span><span style="color: #800000;">"</span><span style="color: #800000;">DefaultConnection</span><span style="color: #800000;">"</span><span style="color: #000000;">)));

    services.AddIdentity</span>&lt;ApplicationUser, IdentityRole&gt;<span style="color: #000000;">()
        .AddEntityFrameworkStores</span>&lt;ApplicationDbContext&gt;<span style="color: #000000;">()
        .AddDefaultTokenProviders();

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> Add application services.</span>
    services.AddTransient&lt;IEmailSender, EmailSender&gt;<span style="color: #000000;">();

    services.AddMvc();

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> configure identity server with in-memory stores, keys, clients and scopes</span>
<span style="color: #000000;">    services.AddIdentityServer()
        .AddDeveloperSigningCredential()
        .AddInMemoryPersistedGrants()
        .AddInMemoryIdentityResources(Config.GetIdentityResources())
        .AddInMemoryApiResources(Config.GetApiResources())
        .AddInMemoryClients(Config.GetClients())
        .AddAspNetIdentity</span>&lt;ApplicationUser&gt;<span style="color: #000000;">();
}</span></pre>
</div>
<p>Configure</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
        app.UseBrowserLink();
        app.UseDatabaseErrorPage();
    }
    </span><span style="color: #0000ff;">else</span><span style="color: #000000;">
    {
        app.UseExceptionHandler(</span><span style="color: #800000;">"</span><span style="color: #800000;">/Home/Error</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    }

    app.UseStaticFiles();

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> app.UseAuthentication(); </span><span style="color: #008000;">//</span><span style="color: #008000;"> not needed, since UseIdentityServer adds the authentication middleware</span>
<span style="color: #000000;">    app.UseIdentityServer();

    app.UseMvc(routes </span>=&gt;<span style="color: #000000;">
    {
        routes.MapRoute(
            name: </span><span style="color: #800000;">"</span><span style="color: #800000;">default</span><span style="color: #800000;">"</span><span style="color: #000000;">,
            template: </span><span style="color: #800000;">"</span><span style="color: #800000;">{controller=Home}/{action=Index}/{id?}</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    });
}</span></pre>
</div>
<p><strong><span style="font-size: 14pt;">创建用户数据库</span></strong></p>
<p>鉴于这是一个新的ASP.NET Identity项目，您将需要创建数据库。 您可以通过从项目目录运行命令提示符并运行&nbsp;<span class="cnblogs_code">dotnet ef database update -c ApplicationDbContext</span>&nbsp;来执行此操作</p>
<p>案例下载：<a href="https://pan.baidu.com/s/1ZxVHNYApxyZMGcDg-XlTkg" target="_blank">https://pan.baidu.com/s/1ZxVHNYApxyZMGcDg-XlTkg&nbsp;</a></p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">八、添加一个JavaScript客户端<a name="a8"></a></span></strong></p>
<p>这个快速入门将展示如何构建JavaScript客户端应用程序。 用户将登录到IdentityServer，使用IdentityServer发出的访问令牌调用Web API，并注销IdentityServer。</p>
<p><strong><span style="font-size: 14pt;">添加一个JavaScript的客户端项目</span></strong></p>
<p>添加一个空项目&nbsp;</p>
<p><strong><span style="font-size: 14pt;">添加静态文件中间件</span></strong></p>
<p>鉴于此项目主要用于运行客户端，我们需要ASP.NET Core来提供构成我们应用程序的静态HTML和JavaScript文件。 静态文件中间件旨在执行此操作。</p>
<p>在Configure方法中的Startup.cs中注册静态文件中间件：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configure(IApplicationBuilder app)
{
    app.UseDefaultFiles();
    app.UseStaticFiles();
}</span></pre>
</div>
<p>这个中间件现在将从应用程序的〜/ wwwroot文件夹中提供静态文件。 这是我们将放置HTML和JavaScript文件的地方。</p>
<p><strong><span style="font-size: 14pt;">引用oidc-client</span></strong></p>
<p>在MVC项目中，我们使用一个库来处理OpenID Connect协议。 在这个项目中，我们需要一个类似的库，除了一个在JavaScript中工作并且被设计为在浏览器中运行的库。 oidc-client库就是这样一个库。 它可以通过NPM，Bower，以及从github直接下载。</p>
<p><strong>NPM</strong></p>
<p>如果您想使用NPM下载oidc-client，请按照以下步骤操作：</p>
<p>将一个新的NPM包文件添加到您的项目中，并将其命名为package.json。</p>
<p>在package.json中添加一个依赖到oidc-client：</p>
<div class="cnblogs_code">
<pre><span style="color: #800000;">"</span><span style="color: #800000;">dependencies</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
  </span><span style="color: #800000;">"</span><span style="color: #800000;">oidc-client</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">1.4.1</span><span style="color: #800000;">"</span><span style="color: #000000;">
}</span></pre>
</div>
<p>一旦保存了该文件，Visual Studio应该自动将这些软件包恢复到名为node_modules的文件夹中。</p>
<p>在〜/node_modules/oidc-client/dist文件夹中找到名为oidc-client.js的文件，并将其复制到应用程序的〜/wwwroot文件夹中。 有更复杂的方法将您的NPM软件包复制到〜/wwwroot中，但这些技术不在本快速入门的范围之内。</p>
<p><strong><span style="font-size: 14pt;">添加您的HTML和JavaScript文件</span></strong></p>
<p>在〜/wwwroot中，添加一个名为index.html和callback.html的HTML文件，并添加一个名为app.js的JavaScript文件。</p>
<p><strong>index.html</strong></p>
<p>这将是我们应用程序的主页面。 它将包含用于登录，注销并调用Web API的按钮的HTML。 它还将包含&lt;script&gt;标签以包含我们的两个JavaScript文件。 它还将包含用于向用户显示消息的&lt;pre&gt;。</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('0e2e9786-1d0f-4485-a97d-c406f424de78')"><img id="code_img_closed_0e2e9786-1d0f-4485-a97d-c406f424de78" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_0e2e9786-1d0f-4485-a97d-c406f424de78" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('0e2e9786-1d0f-4485-a97d-c406f424de78',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_0e2e9786-1d0f-4485-a97d-c406f424de78" class="cnblogs_code_hide">
<pre>&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
    &lt;meta charset=<span style="color: #800000;">"</span><span style="color: #800000;">utf-8</span><span style="color: #800000;">"</span> /&gt;
    &lt;title&gt;&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
    &lt;button id=<span style="color: #800000;">"</span><span style="color: #800000;">login</span><span style="color: #800000;">"</span>&gt;Login&lt;/button&gt;
    &lt;button id=<span style="color: #800000;">"</span><span style="color: #800000;">api</span><span style="color: #800000;">"</span>&gt;Call API&lt;/button&gt;
    &lt;button id=<span style="color: #800000;">"</span><span style="color: #800000;">logout</span><span style="color: #800000;">"</span>&gt;Logout&lt;/button&gt;

    &lt;pre id=<span style="color: #800000;">"</span><span style="color: #800000;">results</span><span style="color: #800000;">"</span>&gt;&lt;/pre&gt;

    &lt;script src=<span style="color: #800000;">"</span><span style="color: #800000;">oidc-client.js</span><span style="color: #800000;">"</span>&gt;&lt;/script&gt;
    &lt;script src=<span style="color: #800000;">"</span><span style="color: #800000;">app.js</span><span style="color: #800000;">"</span>&gt;&lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;</pre>
</div>
<span class="cnblogs_code_collapse">index.html</span></div>
<p><strong>app.js</strong></p>
<p>这将包含我们的应用程序的主要代码。 首先要添加一个辅助函数来将消息记录到&lt;pre&gt;：&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('170c7271-b075-45d4-9c6b-479c08b113c1')"><img id="code_img_closed_170c7271-b075-45d4-9c6b-479c08b113c1" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_170c7271-b075-45d4-9c6b-479c08b113c1" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('170c7271-b075-45d4-9c6b-479c08b113c1',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_170c7271-b075-45d4-9c6b-479c08b113c1" class="cnblogs_code_hide">
<pre><span style="color: #000000;">function log() {
    document.getElementById(</span><span style="color: #800000;">'</span><span style="color: #800000;">results</span><span style="color: #800000;">'</span>).innerText = <span style="color: #800000;">''</span><span style="color: #000000;">;

    Array.prototype.forEach.call(arguments, function (msg) {
        </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (msg instanceof Error) {
            msg </span>= <span style="color: #800000;">"</span><span style="color: #800000;">Error: </span><span style="color: #800000;">"</span> +<span style="color: #000000;"> msg.message;
        }
        </span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span> (<span style="color: #0000ff;">typeof</span> msg !== <span style="color: #800000;">'</span><span style="color: #800000;">string</span><span style="color: #800000;">'</span><span style="color: #000000;">) {
            msg </span>= JSON.stringify(msg, <span style="color: #0000ff;">null</span>, <span style="color: #800080;">2</span><span style="color: #000000;">);
        }
        document.getElementById(</span><span style="color: #800000;">'</span><span style="color: #800000;">results</span><span style="color: #800000;">'</span>).innerHTML += msg + <span style="color: #800000;">'</span><span style="color: #800000;">\r\n</span><span style="color: #800000;">'</span><span style="color: #000000;">;
    });
}</span></pre>
</div>
<span class="cnblogs_code_collapse">app.js</span></div>
<p>接下来，添加代码将&ldquo;click&rdquo;事件处理程序注册到三个按钮：</p>
<div class="cnblogs_code">
<pre>document.getElementById(<span style="color: #800000;">"</span><span style="color: #800000;">login</span><span style="color: #800000;">"</span>).addEventListener(<span style="color: #800000;">"</span><span style="color: #800000;">click</span><span style="color: #800000;">"</span>, login, <span style="color: #0000ff;">false</span><span style="color: #000000;">);
document.getElementById(</span><span style="color: #800000;">"</span><span style="color: #800000;">api</span><span style="color: #800000;">"</span>).addEventListener(<span style="color: #800000;">"</span><span style="color: #800000;">click</span><span style="color: #800000;">"</span>, api, <span style="color: #0000ff;">false</span><span style="color: #000000;">);
document.getElementById(</span><span style="color: #800000;">"</span><span style="color: #800000;">logout</span><span style="color: #800000;">"</span>).addEventListener(<span style="color: #800000;">"</span><span style="color: #800000;">click</span><span style="color: #800000;">"</span>, logout, <span style="color: #0000ff;">false</span>);</pre>
</div>
<p>接下来，我们可以使用oidc-client库中的UserManager类来管理OpenID Connect协议。 它需要类似的配置，这在MVC客户端中是必需的（虽然值不同）。 添加此代码以配置和实例化UserManager：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> config =<span style="color: #000000;"> {
    authority: </span><span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:5000</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    client_id: </span><span style="color: #800000;">"</span><span style="color: #800000;">js</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    redirect_uri: </span><span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:5003/callback.html</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    response_type: </span><span style="color: #800000;">"</span><span style="color: #800000;">id_token token</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    scope:</span><span style="color: #800000;">"</span><span style="color: #800000;">openid profile api1</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    post_logout_redirect_uri : </span><span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:5003/index.html</span><span style="color: #800000;">"</span><span style="color: #000000;">,
};
</span><span style="color: #0000ff;">var</span> mgr = <span style="color: #0000ff;">new</span> Oidc.UserManager(config);</pre>
</div>
<p>接下来，UserManager提供一个getUser API来知道用户是否登录到JavaScript应用程序。 它使用JavaScript Promise异步返回结果。 返回的用户对象具有包含用户声明的配置文件属性。 添加此代码以检测用户是否已登录JavaScript应用程序：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">mgr.getUser().then(function (user) {
    </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (user) {
        log(</span><span style="color: #800000;">"</span><span style="color: #800000;">User logged in</span><span style="color: #800000;">"</span><span style="color: #000000;">, user.profile);
    }
    </span><span style="color: #0000ff;">else</span><span style="color: #000000;"> {
        log(</span><span style="color: #800000;">"</span><span style="color: #800000;">User not logged in</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    }
});</span></pre>
</div>
<p>接下来，我们要实现登录，api和注销功能。 UserManager提供signinRedirect来登录用户，并提供signoutRedirect登录用户。 我们在上面的代码中获得的用户对象也具有access_token属性，可用于通过Web API进行身份验证。 access_token将通过Bearer方案的Authorization头传递给Web API。 添加此代码以在我们的应用程序中实现这三个功能：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">function</span><span style="color: #000000;"> login() {
    mgr.signinRedirect();
}

</span><span style="color: #0000ff;">function</span><span style="color: #000000;"> api() {
    mgr.getUser().then(</span><span style="color: #0000ff;">function</span><span style="color: #000000;"> (user) {
        </span><span style="color: #0000ff;">var</span> url = "http://localhost:5001/identity"<span style="color: #000000;">;

        </span><span style="color: #0000ff;">var</span> xhr = <span style="color: #0000ff;">new</span><span style="color: #000000;"> XMLHttpRequest();
        xhr.open(</span>"GET"<span style="color: #000000;">, url);
        xhr.onload </span>= <span style="color: #0000ff;">function</span><span style="color: #000000;"> () {
            log(xhr.status, JSON.parse(xhr.responseText));
        }
        xhr.setRequestHeader(</span>"Authorization", "Bearer " +<span style="color: #000000;"> user.access_token);
        xhr.send();
    });
}

</span><span style="color: #0000ff;">function</span><span style="color: #000000;"> logout() {
    mgr.signoutRedirect();
}</span></pre>
</div>
<p><strong>callback.html</strong></p>
<p>一旦用户登录到IdentityServer，该HTML文件就是指定的redirect_uri页面。 它将完成与IdentityServer的OpenID Connect协议登录握手。 这个代码全部由我们之前使用的UserManager类提供。 登录完成后，我们可以将用户重定向回主index.html页面。 添加此代码以完成登录过程：</p>
<div class="cnblogs_code">
<pre>&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
    &lt;meta charset=<span style="color: #800000;">"</span><span style="color: #800000;">utf-8</span><span style="color: #800000;">"</span> /&gt;
    &lt;title&gt;&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
    &lt;script src=<span style="color: #800000;">"</span><span style="color: #800000;">oidc-client.js</span><span style="color: #800000;">"</span>&gt;&lt;/script&gt;
    &lt;script&gt;
        <span style="color: #0000ff;">new</span><span style="color: #000000;"> Oidc.UserManager().signinRedirectCallback().then(function () {
            window.location </span>= <span style="color: #800000;">"</span><span style="color: #800000;">index.html</span><span style="color: #800000;">"</span><span style="color: #000000;">;
        }).</span><span style="color: #0000ff;">catch</span><span style="color: #000000;">(function (e) {
            console.error(e);
        });
    </span>&lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;</pre>
</div>
<p><strong><span style="font-size: 14pt;">为JavaScript客户端添加客户端注册到IdentityServer</span></strong></p>
<p>现在客户端应用程序已准备就绪，我们需要在IdentityServer中为这个新的JavaScript客户端定义配置条目。 在IdentityServer项目中找到客户端配置（在Config.cs中）。 为我们的新JavaScript应用程序添加一个新客户端到列表中。 它应该具有下面列出的配置：</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> JavaScript Client</span>
<span style="color: #0000ff;">new</span><span style="color: #000000;"> Client
{
    ClientId </span>= <span style="color: #800000;">"</span><span style="color: #800000;">js</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    ClientName </span>= <span style="color: #800000;">"</span><span style="color: #800000;">JavaScript Client</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    AllowedGrantTypes </span>=<span style="color: #000000;"> GrantTypes.Implicit,
    AllowAccessTokensViaBrowser </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">,

    RedirectUris </span>=           { <span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:5003/callback.html</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
    PostLogoutRedirectUris </span>= { <span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:5003/index.html</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
    AllowedCorsOrigins </span>=     { <span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:5003</span><span style="color: #800000;">"</span><span style="color: #000000;"> },

    AllowedScopes </span>=<span style="color: #000000;">
    {
        IdentityServerConstants.StandardScopes.OpenId,
        IdentityServerConstants.StandardScopes.Profile,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">api1</span><span style="color: #800000;">"</span><span style="color: #000000;">
    }
}</span></pre>
</div>
<p><strong><span style="font-size: 14pt;">允许使用CORS对Web API进行Ajax调用</span></strong></p>
<p>需要配置的最后一点是在Web API项目中配置CORS。 这将允许Ajax调用从http://localhost:5003到http://localhost:5001。</p>
<p><strong>Configure CORS</strong></p>
<p>将CORS服务添加到Startup.cs中ConfigureServices中的依赖注入系统：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> ConfigureServices(IServiceCollection services)
{
    services.AddMvcCore()
        .AddAuthorization()
        .AddJsonFormatters();

    services.AddAuthentication(</span><span style="color: #800000;">"</span><span style="color: #800000;">Bearer</span><span style="color: #800000;">"</span><span style="color: #000000;">)
        .AddIdentityServerAuthentication(options </span>=&gt;<span style="color: #000000;">
        {
            options.Authority </span>= <span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:5000</span><span style="color: #800000;">"</span><span style="color: #000000;">;
            options.RequireHttpsMetadata </span>= <span style="color: #0000ff;">false</span><span style="color: #000000;">;

            options.ApiName </span>= <span style="color: #800000;">"</span><span style="color: #800000;">api1</span><span style="color: #800000;">"</span><span style="color: #000000;">;
        });

    services.AddCors(options </span>=&gt;<span style="color: #000000;">
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> this defines a CORS policy called "default"</span>
        options.AddPolicy(<span style="color: #800000;">"</span><span style="color: #800000;">default</span><span style="color: #800000;">"</span>, policy =&gt;<span style="color: #000000;">
        {
            policy.WithOrigins(</span><span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:5003</span><span style="color: #800000;">"</span><span style="color: #000000;">)
                .AllowAnyHeader()
                .AllowAnyMethod();
        });
    });
}</span></pre>
</div>
<p>在配置中将CORS中间件添加到管道中：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configure(IApplicationBuilder app)
{
    app.UseCors(</span><span style="color: #800000;">"</span><span style="color: #800000;">default</span><span style="color: #800000;">"</span><span style="color: #000000;">);

    app.UseAuthentication();

    app.UseMvc();
}</span></pre>
</div>
<p>&nbsp;案例下载：<a href="https://pan.baidu.com/s/1wFDdwjmjWIhvMIPIoZQwBw" target="_blank">https://pan.baidu.com/s/1wFDdwjmjWIhvMIPIoZQwBw</a></p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">九、使用EntityFramework核心进行配置和操作数据<a name="a9"></a></span></strong></p>
<p>IdentityServer专为扩展性而设计，其中一个可扩展点是用于IdentityServer所需数据的存储机制。 本快速入门说明如何配置IdentityServer以使用EntityFramework（EF）作为此数据的存储机制（而不是使用我们迄今为止使用的内存中实现）。</p>
<p><strong><span style="font-size: 14pt;">IdentityServer4.EntityFramework</span></strong></p>
<p>我们正在向数据库移动两种类型的数据。 首先是配置数据（resources和client）。 第二个是IdentityServer在使用时生成的操作数据（tokens，codes和consents）。 这些商店使用接口建模，我们在&nbsp;<span class="cnblogs_code">IdentityServer4.EntityFramework</span>&nbsp; Nuget包中提供这些接口的EF实现。</p>
<p>通过添加对&nbsp;<span class="cnblogs_code">IdentityServer4.EntityFramework</span>&nbsp; Nuget包的IdentityServer项目的引用开始。</p>
<p><strong><span style="font-size: 14pt;">使用SqlServer</span></strong></p>
<p>鉴于EF的灵活性，您可以使用任何EF支持的数据库。 对于这个快速入门，我们将使用Visual Studio附带的SqlServer的LocalDb版本。</p>
<p>数据库模式更改和使用EF迁移</p>
<p>IdentityServer4.EntityFramework软件包包含从IdentityServer模型映射的实体类。 随着IdentityServer的模型更改，IdentityServer4.EntityFramework中的实体类也会更改。 在使用IdentityServer4.EntityFramework并随着时间的推移升级时，随着实体类的更改，您将负责自己的数据库模式以及对该模式所必需的更改。 管理这些变化的一种方法是使用EF迁移，这个快速入门将显示如何完成。 如果迁移不是您的偏好，那么您可以以任何您认为合适的方式管理架构更改。</p>
<p><strong><span style="font-size: 14pt;">用于迁移的EF工具</span></strong></p>
<p>除了使用EF迁移跟踪模式更改外，我们还将使用它来创建数据库中的初始模式。 这需要使用EF Core工具（更多细节在这里）。 我们现在将添加这些内容，不幸的是，这必须通过手工编辑您的.csproj文件来完成。 通过右键单击项目并选择&ldquo;编辑projectname.csproj&rdquo;来编辑.csproj：&nbsp;</p>
<div class="cnblogs_code">
<pre>&lt;ItemGroup&gt;
  &lt;DotNetCliToolReference Include=<span style="color: #800000;">"</span><span style="color: #800000;">Microsoft.EntityFrameworkCore.Tools.DotNet</span><span style="color: #800000;">"</span> Version=<span style="color: #800000;">"</span><span style="color: #800000;">2.0.0</span><span style="color: #800000;">"</span> /&gt;
&lt;/ItemGroup&gt;</pre>
</div>
<p><strong><span style="font-size: 14pt;">配置 stores</span></strong></p>
<p>下一步是将当前调用替换为Startup.cs中ConfigureServices方法中的AddInMemoryClients，AddInMemoryIdentityResources和AddInMemoryApiResources。 我们将用下面的代码替换它们：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">const</span> <span style="color: #0000ff;">string</span> connectionString = <span style="color: #800000;">@"</span><span style="color: #800000;">Data Source=(LocalDb)\MSSQLLocalDB;database=IdentityServer4.Quickstart.EntityFramework-2.0.0;trusted_connection=yes;</span><span style="color: #800000;">"</span><span style="color: #000000;">;
</span><span style="color: #0000ff;">var</span> migrationsAssembly = <span style="color: #0000ff;">typeof</span><span style="color: #000000;">(Startup).GetTypeInfo().Assembly.GetName().Name;

</span><span style="color: #008000;">//</span><span style="color: #008000;"> configure identity server with in-memory stores, keys, clients and scopes</span>
<span style="color: #000000;">services.AddIdentityServer()
    .AddDeveloperSigningCredential()
    .AddTestUsers(Config.GetUsers())
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> this adds the config data from DB (clients, resources)</span>
    .AddConfigurationStore(options =&gt;<span style="color: #000000;">
    {
        options.ConfigureDbContext </span>= builder =&gt;<span style="color: #000000;">
            builder.UseSqlServer(connectionString,
                sql </span>=&gt;<span style="color: #000000;"> sql.MigrationsAssembly(migrationsAssembly));
    })
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> this adds the operational data from DB (codes, tokens, consents)</span>
    .AddOperationalStore(options =&gt;<span style="color: #000000;">
    {
        options.ConfigureDbContext </span>= builder =&gt;<span style="color: #000000;">
            builder.UseSqlServer(connectionString,
                sql </span>=&gt;<span style="color: #000000;"> sql.MigrationsAssembly(migrationsAssembly));

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> this enables automatic token cleanup. this is optional.</span>
        options.EnableTokenCleanup = <span style="color: #0000ff;">true</span><span style="color: #000000;">;
        options.TokenCleanupInterval </span>= <span style="color: #800080;">30</span><span style="color: #000000;">;
    });</span></pre>
</div>
<p>您可能需要将这些命名空间添加到文件中：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.EntityFrameworkCore;
</span><span style="color: #0000ff;">using</span> System.Reflection;</pre>
</div>
<p>上面的代码是对连接字符串进行硬编码的，如果你愿意，你可以随意更改。 此外，对AddConfigurationStore和AddOperationalStore的调用正在注册EF支持的存储实现。</p>
<p><strong><span style="font-size: 14pt;">添加迁移</span></strong></p>
<p>要创建迁移，请在IdentityServer项目目录中打开命令提示符。 在命令提示符下运行这两个命令：</p>
<div class="cnblogs_code">
<pre>dotnet ef migrations add InitialIdentityServerPersistedGrantDbMigration -c PersistedGrantDbContext -o Data/Migrations/IdentityServer/<span style="color: #000000;">PersistedGrantDb
dotnet ef migrations add InitialIdentityServerConfigurationDbMigration </span>-c ConfigurationDbContext -o Data/Migrations/IdentityServer/ConfigurationDb</pre>
</div>
<p>您现在应该在项目中看到一个〜/Data/Migrations/IdentityServer文件夹。 这包含新创建的迁移的代码。</p>
<p><strong><span style="font-size: 14pt;">初始化数据库</span></strong></p>
<p>现在我们已经进行了迁移，我们可以编写代码来从迁移中创建数据库。 我们还将使用我们在之前的快速入门中定义的内存配置数据对数据库进行种子处理。</p>
<p>在Startup.cs中添加此方法以帮助初始化数据库：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> InitializeDatabase(IApplicationBuilder app)
{
    </span><span style="color: #0000ff;">using</span> (<span style="color: #0000ff;">var</span> serviceScope = app.ApplicationServices.GetService&lt;IServiceScopeFactory&gt;<span style="color: #000000;">().CreateScope())
    {
        serviceScope.ServiceProvider.GetRequiredService</span>&lt;PersistedGrantDbContext&gt;<span style="color: #000000;">().Database.Migrate();

        </span><span style="color: #0000ff;">var</span> context = serviceScope.ServiceProvider.GetRequiredService&lt;ConfigurationDbContext&gt;<span style="color: #000000;">();
        context.Database.Migrate();
        </span><span style="color: #0000ff;">if</span> (!<span style="color: #000000;">context.Clients.Any())
        {
            </span><span style="color: #0000ff;">foreach</span> (<span style="color: #0000ff;">var</span> client <span style="color: #0000ff;">in</span><span style="color: #000000;"> Config.GetClients())
            {
                context.Clients.Add(client.ToEntity());
            }
            context.SaveChanges();
        }

        </span><span style="color: #0000ff;">if</span> (!<span style="color: #000000;">context.IdentityResources.Any())
        {
            </span><span style="color: #0000ff;">foreach</span> (<span style="color: #0000ff;">var</span> resource <span style="color: #0000ff;">in</span><span style="color: #000000;"> Config.GetIdentityResources())
            {
                context.IdentityResources.Add(resource.ToEntity());
            }
            context.SaveChanges();
        }

        </span><span style="color: #0000ff;">if</span> (!<span style="color: #000000;">context.ApiResources.Any())
        {
            </span><span style="color: #0000ff;">foreach</span> (<span style="color: #0000ff;">var</span> resource <span style="color: #0000ff;">in</span><span style="color: #000000;"> Config.GetApiResources())
            {
                context.ApiResources.Add(resource.ToEntity());
            }
            context.SaveChanges();
        }
    }
}</span></pre>
</div>
<p>然后我们可以从Configure方法调用它::</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configure(IApplicationBuilder app, IHostingEnvironment env, ILoggerFactory loggerFactory)
{
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> this will do the initial DB population</span>
<span style="color: #000000;">    InitializeDatabase(app);

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> the rest of the code that was already here
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> ...</span>
}</pre>
</div>
<p>上面的InitializeDatabase帮助程序API可以方便地为数据库创建种子，但这种方法并不适合每次运行应用程序时执行。 一旦你的数据库被填充，考虑删除对API的调用。</p>
<p><strong><span style="font-size: 14pt;">运行客户端应用程序</span></strong></p>
<p>您现在应该能够运行任何现有的客户端应用程序并登录，获取令牌并调用API - 全部基于数据库配置。</p>
<p>&nbsp;</p>
<p>&nbsp;案例下载：<a href="https://pan.baidu.com/s/1zVRXIEB9VMbbbCBf3kokTA" target="_blank">https://pan.baidu.com/s/1zVRXIEB9VMbbbCBf3kokTA</a></p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">十、社区快速入门&amp;样品<a name="a10"></a></span></strong></p>
<p><strong><span style="font-size: 14pt;">各种ASP.NET core安全示例</span></strong></p>
<p><a class="reference external" href="https://github.com/leastprivilege/AspNetCoreSecuritySamples">https://github.com/leastprivilege/AspNetCoreSecuritySamples</a></p>
<p><strong><span style="font-size: 14pt;">IdentityServer4 EF 和 ASP.NET Identity</span></strong></p>
<p><a class="reference external" href="https://github.com/IdentityServer/IdentityServer4.Samples/tree/release/Quickstarts/Combined_AspNetIdentity_and_EntityFrameworkStorage">这个</a>样本结合了EF和ASP.NET身份快速入门（＃6和＃8）。</p>
<p><strong><span style="font-size: 14pt;">共同托管IdentityServer4和一个Web API</span></strong></p>
<p>此示例显示如何在保护API的IdentityServer所在的主机上托管API。</p>
<p><a class="reference external" href="https://github.com/brockallen/IdentityServerAndApi">https://github.com/brockallen/IdentityServerAndApi</a></p>
<p><strong><span style="font-size: 14pt;">用于MongoDB的IdentityServer4案例</span></strong></p>
<ul>
<li>IdentityServer4-mongo：与快速入门＃8 EntityFramework配置类似，但使用MongoDB作为配置数据。&nbsp;</li>
<li>IdentityServer4-mongo-AspIdentity：更详细的示例基于使用ASP.NET身份进行身份管理，该身份管理使用MongoDB作为配置数据</li>
</ul>
<p><a class="reference external" href="https://github.com/souzartn/IdentityServer4.Samples.Mongo">https://github.com/souzartn/IdentityServer4.Samples.Mongo</a></p>
<p><strong><span style="font-size: 14pt;">从Facebook，Google和Twitter交换外部令牌</span></strong></p>
<p>演示如何使用扩展授权将外部身份验证令牌交换到身份服务器访问令牌</p>
<p><a class="reference external" href="https://github.com/waqaskhan540/IdentityServerExternalAuth">https://github.com/waqaskhan540/IdentityServerExternalAuth</a></p>
<p><strong><span style="font-size: 14pt;">IdentityServer4快速入门UI的ASP.NET Core MVC RazorPages模板</span></strong></p>
<p><a class="reference external" href="https://github.com/IdentityServer4Contrib/IdentityServer4.Contrib.Templates.RazorPages">Razor Pages based QuickStart sample</a>&nbsp;by&nbsp;<a class="reference external" href="https://github.com/martinfletcher">Martin Fletcher</a>.</p>
<p><strong><span style="font-size: 14pt;">.NET core和ASP.NET core&ldquo;平台&rdquo;方案</span></strong></p>
<p>显示受信任的&ldquo;内部&rdquo;应用程序与&ldquo;外部&rdquo;应用程序与.NET Core 2.0和ASP.NET Core 2.0应用程序的交互</p>
<p><a class="reference external" href="https://github.com/BenjaminAbt/Samples.AspNetCore-IdentityServer4">https://github.com/BenjaminAbt/Samples.AspNetCore-IdentityServer4</a></p>
<p><strong><span style="font-size: 14pt;">使用JWKS使用来自IdentityServer4的令牌保护Node API</span></strong></p>
<ul>
<li>演示如何使用IdentityServer4的JWKS端点和RS256算法来保护Node（Express）API。</li>
<li>使用更高质量的生产准备模块为IdentityServer4.Samples中的NodeJsApi样本提供备选方案。</li>
</ul>
<p><a class="reference external" href="https://github.com/lyphtec/idsvr4-node-jwks">https://github.com/lyphtec/idsvr4-node-jwks</a></p>