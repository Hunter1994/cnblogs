<p><a href="https://www.cnblogs.com/zd1994/p/9193207.html">一、介绍</a></p>
<p><a href="https://www.cnblogs.com/zd1994/p/9193475.html">二、快速入门</a></p>
<p><a href="https://www.cnblogs.com/zd1994/p/9240357.html">三、主题</a></p>
<p><a href="https://www.cnblogs.com/zd1994/p/9265003.html">四、端点</a></p>
<p><a href="https://www.cnblogs.com/zd1994/p/9265185.html">五、参考</a></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201806/741594-20180617162752264-1112406193.png" alt="" /></p>
<p>IdentityServer4是ASP.NET Core 2的OpenID Connect和OAuth 2.0框架。</p>
<p>它可以在您的应用程序中启用以下功能：</p>
<p><strong><span style="font-size: 14pt;">身份验证服务</span></strong></p>
<p>所有应用程序的集中式登录逻辑和工作流程(web，本地，移动，服务)IdentityServer是经过官方认证的OpenID连接实现。</p>
<p><span style="font-size: 14pt;"><strong>单点登录/退出</strong></span><br />在多个应用程序类型上进行单点登录(并退出)。</p>
<p><span style="font-size: 14pt;"><strong>api访问控制</strong></span><br />为各种类型的客户端(如服务器对服务器、web应用程序、SPAs和本地/移动应用程序)发布api访问令牌。</p>
<p><strong><span style="font-size: 14pt;">联合网关</span></strong><br />支持Azure Active Directory、谷歌、Facebook等外部标识提供程序。这使您的应用程序不必了解如何连接这些外部提供程序的细节。</p>
<p><strong><span style="font-size: 14pt;">关注定制</span></strong></p>
<p>最重要的部分 - IdentityServer的许多方面可以定制以适合您的需求。 由于IdentityServer是一个框架，而不是一个封装的产品或一个SaaS，您可以编写代码来调整系统，使其适合您的场景。</p>
<p><strong><span style="font-size: 14pt;">成熟的开源</span></strong><br />IdentityServer使用允许在其之上构建商业产品的Apache 2许可证。它也是.net基金会提供治理和法律支持的一部分。</p>
<p><strong><span style="font-size: 14pt;">学习过程中遇到的问题</span></strong></p>
<p>1，在consent页面点击确认不能跳转到客户端</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('268879b7-19f9-46fa-b8d0-24e1ad82f277')"><img id="code_img_closed_268879b7-19f9-46fa-b8d0-24e1ad82f277" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_268879b7-19f9-46fa-b8d0-24e1ad82f277" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('268879b7-19f9-46fa-b8d0-24e1ad82f277',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_268879b7-19f9-46fa-b8d0-24e1ad82f277" class="cnblogs_code_hide">
<pre><span style="color: #800080;">1</span>，启动应用-&gt;<span style="color: #000000;">正常登陆
</span><span style="color: #800080;">2</span>，关闭浏览器/重启应用-&gt;<span style="color: #000000;">正常登陆
</span><span style="color: #800080;">3</span>，清除浏览器缓存/关闭浏览器/重启应用-&gt;consent进不去了</pre>
</div>
<span class="cnblogs_code_collapse">测试用例</span></div>
<p>解决方法：</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('7c514ff9-5b09-4cc1-a8ff-0acf7dd42aab')"><img id="code_img_closed_7c514ff9-5b09-4cc1-a8ff-0acf7dd42aab" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_7c514ff9-5b09-4cc1-a8ff-0acf7dd42aab" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('7c514ff9-5b09-4cc1-a8ff-0acf7dd42aab',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_7c514ff9-5b09-4cc1-a8ff-0acf7dd42aab" class="cnblogs_code_hide">
<pre>        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> ConfigureServices(IServiceCollection services)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> services.Configure&lt;CookiePolicyOptions&gt;(options =&gt;
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> {
            </span><span style="color: #008000;">//</span>     <span style="color: #008000;">//</span><span style="color: #008000;"> This lambda determines whether user consent for non-essential cookies is needed for a given request.
            </span><span style="color: #008000;">//</span><span style="color: #008000;">     options.CheckConsentNeeded = context =&gt; true;
            </span><span style="color: #008000;">//</span><span style="color: #008000;">     options.MinimumSameSitePolicy = SameSiteMode.None;
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> });</span></pre>
</div>
<span class="cnblogs_code_collapse">注释ConfigureServices方法中的</span></div>
<p>&nbsp;</p>