<p>&nbsp;<strong>一、ASP.NET Identity入门</strong></p>
<p><strong>二、功能和API</strong></p>
<p><strong><strong>三、可扩展性</strong></strong></p>
<p><strong><strong><strong>四、迁移</strong></strong></strong></p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">一、ASP.NET <strong>Identity</strong>入门</span></strong></span></p>
<p><strong><span style="font-size: 18px;">1，开始使用ASP.NET&nbsp;<strong>Identity</strong><br /></span></strong></p>
<p>①用个人帐户创建一个ASP.NET MVC应用程序。 您可以在ASP.NET MVC，Web窗体，Web API，SignalR等中使用ASP.NET Identity。在本文中，我们将从ASP.NET MVC应用程序开始。</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201711/741594-20171113221911656-1704764808.png" alt="" width="482" height="313" /></p>
<p>②创建的项目包含以下三个包</p>
<p>&nbsp;<span class="cnblogs_code">Microsoft.AspNet.Identity.EntityFramework</span>&nbsp;将ASP.NET Identity数据结构持久化到SQL Server中</p>
<p>&nbsp;<span class="cnblogs_code">Microsoft.AspNet.Identity.Core</span>&nbsp;这个包有ASP.NET身份的核心接口。这个包可以用来编写针对不同持久化存储的ASP.NET Identity实现，比如Azure表存储，NoSQL数据库等等。</p>
<p>&nbsp;<span class="cnblogs_code">Microsoft.AspNet.Identity.Owin</span>&nbsp;&nbsp;此包中包含用于在ASP.NET应用程序中使用ASP.NET Identity插入OWIN身份验证的功能。当您将登录功能添加到您的应用程序并调用OWIN Cookie身份验证中间件来生成cookie时，会使用此功能。</p>
<p>③创建一个用户。<br />启动应用程序，然后点击注册链接来创建一个用户。</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201711/741594-20171113224609327-384235494.png" alt="" width="362" height="222" /></p>
<p>当用户点击注册按钮时，Account控制器的Register操作通过调用ASP.NET Identity API来创建用户，如下所示：</p>
<p>④登录</p>
<p>如果用户成功创建，则通过SignInAsync方法登录</p>
<div class="cnblogs_code">
<pre>        <span style="color: #008000;">//</span>
        <span style="color: #008000;">//</span><span style="color: #008000;"> POST: /Account/Register</span>
<span style="color: #000000;">        [HttpPost]
        [AllowAnonymous]
        [ValidateAntiForgeryToken]
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task&lt;ActionResult&gt;<span style="color: #000000;"> Register(RegisterViewModel model)
        {
            </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (ModelState.IsValid)
            {
                </span><span style="color: #0000ff;">var</span> user = <span style="color: #0000ff;">new</span> ApplicationUser { UserName = model.Email, Email =<span style="color: #000000;"> model.Email };
                </span><span style="color: #0000ff;">var</span> result = <span style="color: #0000ff;">await</span><span style="color: #000000;"> UserManager.CreateAsync(user, model.Password);
                </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (result.Succeeded)
                {
                    </span><span style="color: #008000;">//</span><span style="color: #008000;">如果用户成功创建，则通过SignInAsync方法登录。</span>
                    <span style="color: #0000ff;">await</span> SignInManager.SignInAsync(user, isPersistent:<span style="color: #0000ff;">false</span>, rememberBrowser:<span style="color: #0000ff;">false</span><span style="color: #000000;">);
                    
                    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 有关如何启用帐户确认和密码重置的详细信息，请访问 </span><span style="color: #008000; text-decoration: underline;">https://go.microsoft.com/fwlink/?LinkID=320771</span>
                    <span style="color: #008000;">//</span><span style="color: #008000;"> 发送包含此链接的电子邮件
                    </span><span style="color: #008000;">//</span><span style="color: #008000;"> string code = await UserManager.GenerateEmailConfirmationTokenAsync(user.Id);
                    </span><span style="color: #008000;">//</span><span style="color: #008000;"> var callbackUrl = Url.Action("ConfirmEmail", "Account", new { userId = user.Id, code = code }, protocol: Request.Url.Scheme);
                    </span><span style="color: #008000;">//</span><span style="color: #008000;"> await UserManager.SendEmailAsync(user.Id, "确认你的帐户", "请通过单击 &lt;a href=\"" + callbackUrl + "\"&gt;這裏&lt;/a&gt;来确认你的帐户");</span>

                    <span style="color: #0000ff;">return</span> RedirectToAction(<span style="color: #800000;">"</span><span style="color: #800000;">Index</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">Home</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                }
                AddErrors(result);
            }

            </span><span style="color: #008000;">//</span><span style="color: #008000;"> 如果我们进行到这一步时某个地方出错，则重新显示表单</span>
            <span style="color: #0000ff;">return</span><span style="color: #000000;"> View(model);
        }</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">async</span> Task SignInAsync(ApplicationUser user, <span style="color: #0000ff;">bool</span><span style="color: #000000;"> isPersistent)
{
    AuthenticationManager.SignOut(DefaultAuthenticationTypes.ExternalCookie);

</span><span style="color: #008000;">//</span><span style="color: #008000;">由于ASP.NET身份和OWIN Cookie身份验证是基于声明的系统，因此该框架需要应用程序为用户生成ClaimsIdentity</span>
    <span style="color: #0000ff;">var</span> identity = <span style="color: #0000ff;">await</span><span style="color: #000000;"> UserManager.CreateIdentityAsync(
       user, DefaultAuthenticationTypes.ApplicationCookie);
</span><span style="color: #008000;">//</span><span style="color: #008000;">通过使用OWIN中的AuthenticationManager并调用SignIn并传入ClaimsIdentity来签署用户。</span>
<span style="color: #000000;">    AuthenticationManager.SignIn(
       </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> AuthenticationProperties() { 
          IsPersistent </span>=<span style="color: #000000;"> isPersistent 
       }, identity);
}</span></pre>
</div>
<p>⑤注销</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> POST: /Account/LogOff</span>
<span style="color: #000000;">[HttpPost]
[ValidateAntiForgeryToken]
</span><span style="color: #0000ff;">public</span><span style="color: #000000;"> ActionResult LogOff()
{
    AuthenticationManager.SignOut();
    </span><span style="color: #0000ff;">return</span> RedirectToAction(<span style="color: #800000;">"</span><span style="color: #800000;">Index</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">Home</span><span style="color: #800000;">"</span><span style="color: #000000;">);
}</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">二、功能和API</span></strong></span></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">三、可扩展性</span></strong></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">四、迁移</span></strong></span></p>
<p>&nbsp;</p>