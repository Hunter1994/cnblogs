<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">一、总体介绍</span></strong></span></p>
<p>大多数现代应用或多或少是这样的:</p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201806/741594-20180617164433288-941502447.png" alt="" /></p>
<p>通常，每个层(前端、中间层和后端)都必须保护资源并实现身份验证和/或授权&mdash;&mdash;通常针对相同的用户存储。</p>
<p>将这些基本的安全功能外包给安全令牌服务，可以防止在这些应用程序和端点之间重复这些功能。&nbsp;</p>
<p>重组应用程序以支持安全令牌服务将导致以下架构和协议:</p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201806/741594-20180617164733420-1296187395.png" alt="" /></p>
<p>这种设计将安全问题分为两部分:</p>
<p><strong><span style="font-size: 14pt;">身份认证</span></strong></p>
<p>当应用程序需要知道当前用户的身份时，需要进行身份验证。通常，这些应用程序代表该用户管理数据，并需要确保该用户只能访问允许他访问的数据。最常见的例子是（经典）Web应用程序 - 但原生和基于JS的应用程序也需要身份验证。</p>
<p>最常见的身份验证协议是SAML2p、WS-Federation和OpenID Connect&mdash;&mdash;SAML2p是最受欢迎的和最广泛部署的。</p>
<p>OpenID Connect是这三种类型中最新的一种，但被认为是未来的，因为它最有可能应用于现代应用。它从一开始就为移动应用程序场景构建，设计为API友好。&nbsp;</p>
<p><strong><span style="font-size: 14pt;">API访问</span></strong></p>
<p>应用程序有两种与API进行通信的基本方式 - 使用应用程序标识或发放用户身份。 有时两种方法需要结合。</p>
<p>OAuth2是一种协议，允许应用程序从安全令牌服务请求访问令牌，并使用它们与api通信。这种授权降低了客户端应用程序和API的复杂性，因为可以集中验证和授权。&nbsp;</p>
<p>OpenID连接和OAuth 2.0 -更好地结合在一起</p>
<p>OpenID连接和OAuth 2.0非常相似&mdash;&mdash;事实上，OpenID连接是OAuth 2.0之上的扩展。身份认证和API访问这两个基本的安全问题被合并为一个协议 - 往往只需一次往返安全令牌服务。</p>
<p>我们认为，OpenID Connect和OAuth 2.0的结合是在可预见的未来保护现代应用程序的最佳方法。IdentityServer4是这两个协议的一个实现，它高度优化以解决当今移动、本地和web应用程序的典型安全问题。</p>
<p><strong><span style="font-size: 14pt;">IdentityServer4如何提供帮助</span></strong></p>
<p>IdentityServer是一种中间件，可将符合规范的OpenID Connect和OAuth 2.0端点添加到任意的ASP.NET Core应用程序中。</p>
<p>通常情况下，您构建（或重新使用）包含登录和注销页面的应用程序（也可能取决于您的需要），IdentityServer中间件会添加必要的协议头，以便客户端应用程序可以使用这些标准协议与它进行对话。</p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201806/741594-20180617165807639-1923842096.png" alt="" /></p>
<p>托管应用程序可以像您想的那样复杂，但我们通常建议通过仅包含与身份验证相关的用户界面来尽可能缩小攻击面。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">二、术语</span></strong></p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201806/741594-20180617170126255-1126004843.png" alt="" /></p>
<p><strong><span style="font-size: 14pt;">IdentityServer</span></strong></p>
<p>IdentityServer是一个OpenID连接提供程序&mdash;&mdash;它实现了OpenID连接和OAuth 2.0协议。</p>
<p>不同的文献对相同的角色使用不同的术语&mdash;&mdash;您可能还会发现安全令牌服务、身份提供程序、授权服务器、IP-STS等等。</p>
<p>但他们简而言之就是：一种向客户发放安全令牌的软件。</p>
<p>IdentityServer有许多任务和特性&mdash;&mdash;包括:&nbsp;</p>
<ul>
<li>保护你的资源</li>
<li>使用本地帐户存储或通过外部标识提供程序对用户进行身份验证</li>
<li>提供会话管理和单点登录</li>
<li>管理和认证的客户端</li>
<li>向客户端发出标识和访问令牌</li>
<li>验证令牌</li>
</ul>
<p><strong><span style="font-size: 14pt;">User&nbsp;</span></strong></p>
<p>用户是使用注册客户端访问资源的人。</p>
<p><strong><span style="font-size: 14pt;">Client</span></strong></p>
<p>客户端是一种软件，它从IdentityServer请求令牌&mdash;&mdash;用于验证用户(请求身份令牌)或访问资源(请求访问令牌)。客户端必须首先在IdentityServer上注册，然后才能请求令牌。</p>
<p>客户端的示例包括web应用程序、本地移动或桌面应用程序、SPAs、服务器进程等。</p>
<p><strong><span style="font-size: 14pt;">Resources</span></strong></p>
<p>资源是您希望使用IdentityServer(用户的标识数据或api)保护的内容。</p>
<p>每个资源都有一个唯一的名称&mdash;&mdash;客户端使用这个名称来指定他们想要访问的资源。</p>
<p>关于用户的身份数据标识信息(又名claims)，例如姓名或电子邮件地址。</p>
<p>api资源表示客户机希望调用的功能&mdash;&mdash;通常建模为Web api，但不一定。</p>
<p><strong><span style="font-size: 14pt;">Identity Token</span></strong></p>
<p>标识符表示身份验证过程的结果。它至少包含用户的标识符(称为sub - 又名 subject claim)和用户如何以及何时认证的信息。它可以包含其他标识数据。</p>
<p><strong><span style="font-size: 14pt;">Access Token</span></strong></p>
<p>访问令牌允许访问API资源。客户端请求访问令牌并将它们转发到API。访问令牌包含关于客户端和用户的信息(如果存在)。api使用这些信息授权访问它们的数据。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">三、包和创建</span></strong></p>
<p>IdentityServer&nbsp;由许多nuget包组成。</p>
<p><strong><span style="font-size: 14pt;">IdentityServer4</span></strong></p>
<p><a class="reference external" href="https://www.nuget.org/packages/IdentityServer4/">nuget</a>&nbsp;|&nbsp;<a class="reference external" href="https://github.com/identityserver/IdentityServer4">github</a></p>
<p>包含核心IdentityServer对象模型，服务和中间件。 只包含对内存配置和用户存储的支持 - 但是您可以通过配置为其他存储提供插件支持。 这就是其他repos和包的内容。</p>
<p><strong><span style="font-size: 14pt;">Quickstart UI</span></strong></p>
<p><a class="reference external" href="https://github.com/IdentityServer/IdentityServer4.Quickstart.UI">github</a></p>
<p>包含一个简单的starter UI，包括登录、注销和同意页面。</p>
<p><strong><span style="font-size: 14pt;">Access token validation handler</span></strong></p>
<p><a class="reference external" href="https://www.nuget.org/packages/IdentityServer4.AccessTokenValidation">nuget</a>&nbsp;|&nbsp;<a class="reference external" href="https://github.com/IdentityServer/IdentityServer4.AccessTokenValidation">github</a></p>
<p>ASP.NET核心身份验证处理程序，用于在api中验证令牌。处理程序允许在相同的API中同时支持JWT和引用令牌。</p>
<p><strong><span style="font-size: 14pt;">ASP.NET Core Identity</span></strong></p>
<p><a class="reference external" href="https://www.nuget.org/packages/IdentityServer4.AspNetIdentity">nuget</a>&nbsp;|&nbsp;<a class="reference external" href="https://github.com/IdentityServer/IdentityServer4.AspNetIdentity">github</a></p>
<p>用于IdentityServer的ASP.NET Core Identity集成包。 该软件包提供了一个简单的配置API来为您的IdentityServer用户使用ASP.NET身份管理库。</p>
<p><strong><span style="font-size: 14pt;">EntityFramework Core</span></strong></p>
<p><a class="reference external" href="https://www.nuget.org/packages/IdentityServer4.EntityFramework">nuget</a>&nbsp;|&nbsp;<a class="reference external" href="https://github.com/IdentityServer/IdentityServer4.EntityFramework">github</a></p>
<p>EntityFramework用于IdentityServer的核心存储实现。这个包为IdentityServer中的配置和操作存储提供了EntityFramework实现。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">四、演示服务和测试</span></strong></p>
<p><a href="https://demo.identityserver.io/" target="_blank">https://demo.identityserver.io/</a></p>
<p>您可以使用您最喜欢的客户端库尝试IdentityServer4。我们在demo.identityserver.io中有一个测试实例。在主页上，您可以找到关于如何配置您的客户端以及如何调用API的说明。</p>
<p><a href="https://github.com/IdentityServer/CrossVersionIntegrationTests/tree/master/src" target="_blank">https://github.com/IdentityServer/CrossVersionIntegrationTests/tree/master/src</a></p>
<p>此外，我们还有一个可以执行各种IdentityServer和Web API组合（IdentityServer 3和4，ASP.NET Core和Katana）的repo。 我们使用这个测试工具来确保所有的排列工作。 你可以通过克隆这个回购测试你自己。</p>