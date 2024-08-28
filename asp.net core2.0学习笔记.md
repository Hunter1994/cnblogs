<p><a href="#a1">一、Core</a></p>
<p><a href="#a11">　　1，防止过度发布</a></p>
<p><a href="#a12">　　2，Main</a></p>
<p><a href="#a13">　　3，Startup</a></p>
<p><a href="#a14">　　4，添加过滤器</a></p>
<p><a href="#a15">　　5，依赖注入</a></p>
<p><a href="#a16">　　6，中间件</a></p>
<p><a href="#a17">　　7，静态文件</a></p>
<p><a href="#a18">　　8，路由</a></p>
<p><a href="#a19">　　9，环境</a></p>
<p><a href="#a110">　　10，配置和选项</a></p>
<p><a href="#a111">　　11，日志</a></p>
<p><a href="#a112">　　12，使用Sesstion</a></p>
<p><a href="#a113">　　13，使用po文件配置本地化</a></p>
<p><a href="#a114">　　14，在 ASP.NET 管道中运行 OWIN 中间件</a></p>
<p><a href="#a115">　　15，WebSockets</a></p>
<p><a href="#a116">　　16，使用内存缓存</a></p>
<p><a href="#a2">二、EF</a></p>
<p><a href="#a21">　　1，Include和ThenInclude</a></p>
<p><a href="#a22">　　2，通过依赖关系注入注册上下文</a></p>
<p><a href="#a23">　　3，种子数据</a></p>
<p><a href="#a24">　　4，级联删除</a></p>
<p><a href="#a25">　　5，组合PK</a></p>
<p><a href="#a26">　　6，使用原始sql</a></p>
<p><a href="#a4">三、Razor页面</a></p>
<p><a href="#a4">四、MVC</a></p>
<p><a href="#a41">　　1，模型绑定</a></p>
<p><a href="#a42">　　2，视图</a></p>
<p><a href="#a43">　　3，标记帮助程序</a></p>
<p><a href="#a44">　　4，内置标记帮助程序</a></p>
<p><a href="#a45">　　5，分部视图</a></p>
<p><a href="#a46">　　6，视图组件</a></p>
<p><a href="#a47">　　7，上传文件</a></p>
<p><a href="#a48">　　8，筛选器</a></p>
<p><a href="#a49">　　9，绑定与压缩</a></p>
<p><a href="#a5">五、Model</a></p>
<p><a href="#a6">六、配置</a></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a1"></a>一、Core</span></strong></span></p>
<p><strong>1，防止过度发布<a name="a11"></a></strong></p>
<p><span data-ttu-id="bdf25-168">①TryUpdateModelAsync</span></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('8f682438-b5fe-4d1a-bd9b-b2d952b8e91b')"><img id="code_img_closed_8f682438-b5fe-4d1a-bd9b-b2d952b8e91b" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_8f682438-b5fe-4d1a-bd9b-b2d952b8e91b" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('8f682438-b5fe-4d1a-bd9b-b2d952b8e91b',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_8f682438-b5fe-4d1a-bd9b-b2d952b8e91b" class="cnblogs_code_hide">
<pre>        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task&lt;IActionResult&gt;<span style="color: #000000;"> OnPostAsync()
        {
            </span><span style="color: #0000ff;">if</span> (!<span style="color: #000000;">ModelState.IsValid)
            {
                </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> Page();
            }
            </span><span style="color: #0000ff;">var</span> emptyStudent = <span style="color: #0000ff;">new</span><span style="color: #000000;"> Student();
            </span><span style="color: #0000ff;">if</span> (<span style="color: #0000ff;">await</span> TryUpdateModelAsync&lt;Student&gt;(emptyStudent, <span style="color: #800000;">"</span><span style="color: #800000;">student</span><span style="color: #800000;">"</span>, s =&gt; s.FirstMidName, s =&gt; s.LastName, s =&gt;<span style="color: #000000;"> s.EnrollmentDate))
            {
                _context.Students.Add(emptyStudent);
                </span><span style="color: #0000ff;">await</span><span style="color: #000000;"> _context.SaveChangesAsync();
                </span><span style="color: #0000ff;">return</span> RedirectToPage(<span style="color: #800000;">"</span><span style="color: #800000;">./Index</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            }
            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">null</span><span style="color: #000000;">;
        }</span></pre>
</div>
<span class="cnblogs_code_collapse">code</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('8958e33f-7aab-4014-8fee-0ececdf07626')"><img id="code_img_closed_8958e33f-7aab-4014-8fee-0ececdf07626" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_8958e33f-7aab-4014-8fee-0ececdf07626" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('8958e33f-7aab-4014-8fee-0ececdf07626',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_8958e33f-7aab-4014-8fee-0ececdf07626" class="cnblogs_code_hide">
<pre><span style="color: #000000;">        [BindProperty]
        </span><span style="color: #0000ff;">public</span> Student Student { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task&lt;IActionResult&gt; OnPostAsync(<span style="color: #0000ff;">int</span>?<span style="color: #000000;"> id)
        {
            </span><span style="color: #0000ff;">if</span> (!<span style="color: #000000;">ModelState.IsValid)
            {
                </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> Page();
            }

            </span><span style="color: #0000ff;">var</span> studentToUpdate =<span style="color: #0000ff;">await</span><span style="color: #000000;"> _context.Students.FindAsync(id);
            </span><span style="color: #0000ff;">if</span> (<span style="color: #0000ff;">await</span> TryUpdateModelAsync&lt;Student&gt;(studentToUpdate, <span style="color: #800000;">"</span><span style="color: #800000;">student</span><span style="color: #800000;">"</span>, s =&gt; s.LastName, s =&gt;<span style="color: #000000;"> s.EnrollmentDate))
            {
                </span><span style="color: #0000ff;">await</span><span style="color: #000000;"> _context.SaveChangesAsync();
                </span><span style="color: #0000ff;">return</span> RedirectToPage(<span style="color: #800000;">"</span><span style="color: #800000;">./Index</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> Page();
        }</span></pre>
</div>
<span class="cnblogs_code_collapse">code2</span></div>
<p>仅更新TryUpdateModelAsync列出的值</p>
<p><span data-ttu-id="bdf25-172">在上述示例中：</span></p>
<ul>
<li><span data-ttu-id="bdf25-173">第二个自变量 (<code>"student", // Prefix</code>) 是用于查找值的前缀。&nbsp;<span data-ttu-id="bdf25-174">该自变量不区分大小写。</span></span></li>
<li><span data-ttu-id="bdf25-175">已发布的表单值通过<a class="xref" href="https://docs.microsoft.com/zh-cn/aspnet/core/mvc/models/model-binding#how-model-binding-works" data-linktype="relative-path">模型绑定</a>转换为&nbsp;<code>Student</code>&nbsp;模型中的类型。</span></li>
</ul>
<p>&nbsp;②通过属性名称匹配</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('39cf1943-6b6b-4773-b8f0-50610aa7699c')"><img id="code_img_closed_39cf1943-6b6b-4773-b8f0-50610aa7699c" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_39cf1943-6b6b-4773-b8f0-50610aa7699c" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('39cf1943-6b6b-4773-b8f0-50610aa7699c',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_39cf1943-6b6b-4773-b8f0-50610aa7699c" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ContosoUniversity.Models
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> StudentVM
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span> ID { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> LastName { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> FirstMidName { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
        </span><span style="color: #0000ff;">public</span> DateTime EnrollmentDate { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">StudentVM</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('26d89b04-0c53-4b37-9426-19bd13deee7e')"><img id="code_img_closed_26d89b04-0c53-4b37-9426-19bd13deee7e" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_26d89b04-0c53-4b37-9426-19bd13deee7e" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('26d89b04-0c53-4b37-9426-19bd13deee7e',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_26d89b04-0c53-4b37-9426-19bd13deee7e" class="cnblogs_code_hide">
<pre><span style="color: #000000;">[BindProperty]
</span><span style="color: #0000ff;">public</span> StudentVM StudentVM { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task&lt;IActionResult&gt;<span style="color: #000000;"> OnPostAsync()
{
    </span><span style="color: #0000ff;">if</span> (!<span style="color: #000000;">ModelState.IsValid)
    {
        </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> Page();
    }

    </span><span style="color: #0000ff;">var</span> entry = _context.Add(<span style="color: #0000ff;">new</span><span style="color: #000000;"> Student());
    entry.CurrentValues.SetValues(StudentVM);
    </span><span style="color: #0000ff;">await</span><span style="color: #000000;"> _context.SaveChangesAsync();
    </span><span style="color: #0000ff;">return</span> RedirectToPage(<span style="color: #800000;">"</span><span style="color: #800000;">./Index</span><span style="color: #800000;">"</span><span style="color: #000000;">);
}</span></pre>
</div>
<span class="cnblogs_code_collapse">code</span></div>
<p>&nbsp;</p>
<p><strong>2，Main<a name="a12"></a></strong></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('7387226d-f250-4cd1-ae36-027b70919f6d')"><img id="code_img_closed_7387226d-f250-4cd1-ae36-027b70919f6d" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_7387226d-f250-4cd1-ae36-027b70919f6d" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('7387226d-f250-4cd1-ae36-027b70919f6d',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_7387226d-f250-4cd1-ae36-027b70919f6d" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Hosting;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> aspnetcoreapp
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            BuildWebHost(args).Run();
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> IWebHost BuildWebHost(<span style="color: #0000ff;">string</span>[] args) =&gt;<span style="color: #000000;">
            WebHost.CreateDefaultBuilder(args)
                .UseStartup</span>&lt;Startup&gt;<span style="color: #000000;">()
                .Build();
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Main</span></div>
<p><span style="color: #000000; text-transform: none; text-indent: 0px; letter-spacing: normal; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, sans-serif; font-size: 12.8px; font-style: normal; font-weight: normal; word-spacing: 0px; float: none; display: inline !important; white-space: normal; orphans: 2; widows: 2; background-color: #f9f9f9; font-variant-ligatures: normal; font-variant-caps: normal; -webkit-text-stroke-width: 0px;">UseHttpSys</span>:<span style="color: #000000; text-transform: none; text-indent: 0px; letter-spacing: normal; font-family: segoe-ui_normal, 'Segoe UI', Segoe, 'Segoe WP', 'Helvetica Neue', Helvetica, sans-serif; font-size: 16px; font-style: normal; font-weight: normal; word-spacing: 0px; float: none; display: inline !important; white-space: normal; orphans: 2; widows: 2; background-color: #ffffff; font-variant-ligatures: normal; font-variant-caps: normal; -webkit-text-stroke-width: 0px;">用于在 HTTP.sys 中托管应用</span></p>
<p><span style="color: #000000; text-transform: none; text-indent: 0px; letter-spacing: normal; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, sans-serif; font-size: 12.8px; font-style: normal; font-weight: normal; word-spacing: 0px; float: none; display: inline !important; white-space: normal; orphans: 2; widows: 2; background-color: #f9f9f9; font-variant-ligatures: normal; font-variant-caps: normal; -webkit-text-stroke-width: 0px;">UseContentRoot</span>:<span style="color: #000000; text-transform: none; text-indent: 0px; letter-spacing: normal; font-family: segoe-ui_normal, 'Segoe UI', Segoe, 'Segoe WP', 'Helvetica Neue', Helvetica, sans-serif; font-size: 16px; font-style: normal; font-weight: normal; word-spacing: 0px; float: none; display: inline !important; white-space: normal; orphans: 2; widows: 2; background-color: #ffffff; font-variant-ligatures: normal; font-variant-caps: normal; -webkit-text-stroke-width: 0px;">用于指定根内容目录</span></p>
<p><code style="padding: 3px 7px; border-radius: 2px; border: 1px solid #d3d6db; color: #000000; text-transform: none; line-height: 19px; text-indent: 0px; letter-spacing: normal; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, sans-serif; font-size: 0.8rem; font-style: normal; font-weight: normal; word-spacing: 0px; display: inline-block; white-space: normal; direction: ltr; orphans: 2; widows: 2; background-color: #f9f9f9; font-variant-ligatures: normal; font-variant-caps: normal; -webkit-text-stroke-width: 0px; -webkit-font-smoothing: auto;">Build</code><span style="color: #000000; text-transform: none; text-indent: 0px; letter-spacing: normal; font-family: segoe-ui_normal, 'Segoe UI', Segoe, 'Segoe WP', 'Helvetica Neue', Helvetica, sans-serif; font-size: 16px; font-style: normal; font-weight: normal; word-spacing: 0px; float: none; display: inline !important; white-space: normal; orphans: 2; widows: 2; background-color: #ffffff; font-variant-ligatures: normal; font-variant-caps: normal; -webkit-text-stroke-width: 0px;"><span class="Apple-converted-space">&nbsp;和<span class="Apple-converted-space">&nbsp;<code style="padding: 3px 7px; border-radius: 2px; border: 1px solid #d3d6db; color: #000000; text-transform: none; line-height: 19px; text-indent: 0px; letter-spacing: normal; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, sans-serif; font-size: 0.8rem; font-style: normal; font-weight: normal; word-spacing: 0px; display: inline-block; white-space: normal; direction: ltr; orphans: 2; widows: 2; background-color: #f9f9f9; font-variant-ligatures: normal; font-variant-caps: normal; -webkit-text-stroke-width: 0px; -webkit-font-smoothing: auto;">Run</code><span style="color: #000000; text-transform: none; text-indent: 0px; letter-spacing: normal; font-family: segoe-ui_normal, 'Segoe UI', Segoe, 'Segoe WP', 'Helvetica Neue', Helvetica, sans-serif; font-size: 16px; font-style: normal; font-weight: normal; word-spacing: 0px; float: none; display: inline !important; white-space: normal; orphans: 2; widows: 2; background-color: #ffffff; font-variant-ligatures: normal; font-variant-caps: normal; -webkit-text-stroke-width: 0px;"><span class="Apple-converted-space">&nbsp;方法生成<span class="Apple-converted-space">&nbsp;<code style="padding: 3px 7px; border-radius: 2px; border: 1px solid #d3d6db; color: #000000; text-transform: none; line-height: 19px; text-indent: 0px; letter-spacing: normal; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, sans-serif; font-size: 0.8rem; font-style: normal; font-weight: normal; word-spacing: 0px; display: inline-block; white-space: normal; direction: ltr; orphans: 2; widows: 2; background-color: #f9f9f9; font-variant-ligatures: normal; font-variant-caps: normal; -webkit-text-stroke-width: 0px; -webkit-font-smoothing: auto;">IWebHost</code><span style="color: #000000; text-transform: none; text-indent: 0px; letter-spacing: normal; font-family: segoe-ui_normal, 'Segoe UI', Segoe, 'Segoe WP', 'Helvetica Neue', Helvetica, sans-serif; font-size: 16px; font-style: normal; font-weight: normal; word-spacing: 0px; float: none; display: inline !important; white-space: normal; orphans: 2; widows: 2; background-color: #ffffff; font-variant-ligatures: normal; font-variant-caps: normal; -webkit-text-stroke-width: 0px;"><span class="Apple-converted-space">&nbsp;对象，该对象托管应用并开始侦听 HTTP 请求</span></span></span></span></span></span></span></span></p>
<p>&nbsp;<span style="color: #000000; text-transform: none; text-indent: 0px; letter-spacing: normal; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, sans-serif; font-size: 12.8px; font-style: normal; font-weight: normal; word-spacing: 0px; float: none; display: inline !important; white-space: normal; orphans: 2; widows: 2; background-color: #f9f9f9; font-variant-ligatures: normal; font-variant-caps: normal; -webkit-text-stroke-width: 0px;">UseStartup</span>:指定<code style="padding: 3px 7px; border-radius: 2px; border: 1px solid #d3d6db; color: #000000; text-transform: none; line-height: 19px; text-indent: 0px; letter-spacing: normal; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, sans-serif; font-size: 0.8rem; font-style: normal; font-weight: normal; word-spacing: 0px; display: inline-block; white-space: normal; direction: ltr; orphans: 2; widows: 2; background-color: #f9f9f9; font-variant-ligatures: normal; font-variant-caps: normal; -webkit-text-stroke-width: 0px; -webkit-font-smoothing: auto;">Startup</code><span style="color: #000000; text-transform: none; text-indent: 0px; letter-spacing: normal; font-family: segoe-ui_normal, 'Segoe UI', Segoe, 'Segoe WP', 'Helvetica Neue', Helvetica, sans-serif; font-size: 16px; font-style: normal; font-weight: normal; word-spacing: 0px; float: none; display: inline !important; white-space: normal; orphans: 2; widows: 2; background-color: #ffffff; font-variant-ligatures: normal; font-variant-caps: normal; -webkit-text-stroke-width: 0px;"><span class="Apple-converted-space">&nbsp;类</span></span></p>
<p>&nbsp;</p>
<p><strong>3，Startup<a name="a13"></a></strong></p>
<p><code style="padding: 3px 7px; border-radius: 2px; border: 1px solid #d3d6db; color: #000000; text-transform: none; line-height: 19px; text-indent: 0px; letter-spacing: normal; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, sans-serif; font-size: 0.8rem; font-style: normal; font-weight: normal; word-spacing: 0px; display: inline-block; white-space: normal; direction: ltr; orphans: 2; widows: 2; background-color: #f9f9f9; font-variant-ligatures: normal; font-variant-caps: normal; -webkit-text-stroke-width: 0px; -webkit-font-smoothing: auto;">ConfigureServices</code><span style="color: #000000; text-transform: none; text-indent: 0px; letter-spacing: normal; font-family: segoe-ui_normal, 'Segoe UI', Segoe, 'Segoe WP', 'Helvetica Neue', Helvetica, sans-serif; font-size: 16px; font-style: normal; font-weight: normal; word-spacing: 0px; float: none; display: inline !important; white-space: normal; orphans: 2; widows: 2; background-color: #ffffff; font-variant-ligatures: normal; font-variant-caps: normal; -webkit-text-stroke-width: 0px;"><span class="Apple-converted-space">&nbsp;定义应用所使用的服务<span style="color: #000000; text-transform: none; text-indent: 0px; letter-spacing: normal; font-family: segoe-ui_normal, 'Segoe UI', Segoe, 'Segoe WP', 'Helvetica Neue', Helvetica, sans-serif; font-size: 16px; font-style: normal; font-weight: normal; word-spacing: 0px; float: none; display: inline !important; white-space: normal; orphans: 2; widows: 2; background-color: #ffffff; font-variant-ligatures: normal; font-variant-caps: normal; -webkit-text-stroke-width: 0px;">（如 ASP.NET Core MVC、Entity Framework Core 和Identity）（可选择）</span></span></span></p>
<p><code style="padding: 3px 7px; border-radius: 2px; border: 1px solid #d3d6db; color: #000000; text-transform: none; line-height: 19px; text-indent: 0px; letter-spacing: normal; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, sans-serif; font-size: 0.8rem; font-style: normal; font-weight: normal; word-spacing: 0px; display: inline-block; white-space: normal; direction: ltr; orphans: 2; widows: 2; background-color: #f9f9f9; font-variant-ligatures: normal; font-variant-caps: normal; -webkit-text-stroke-width: 0px; -webkit-font-smoothing: auto;">Configure</code><span style="color: #000000; text-transform: none; text-indent: 0px; letter-spacing: normal; font-family: segoe-ui_normal, 'Segoe UI', Segoe, 'Segoe WP', 'Helvetica Neue', Helvetica, sans-serif; font-size: 16px; font-style: normal; font-weight: normal; word-spacing: 0px; float: none; display: inline !important; white-space: normal; orphans: 2; widows: 2; background-color: #ffffff; font-variant-ligatures: normal; font-variant-caps: normal; -webkit-text-stroke-width: 0px;"><span class="Apple-converted-space">&nbsp;定义请求管道的中间件（必须）</span></span></p>
<p>ConfigureServices在&nbsp;Configure之前执行</p>
<p><code style="padding: 3px 7px; border-radius: 2px; border: 1px solid #d3d6db; color: #000000; text-transform: none; line-height: 19px; text-indent: 0px; letter-spacing: normal; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, sans-serif; font-size: 0.8rem; font-style: normal; font-weight: normal; word-spacing: 0px; display: inline-block; white-space: normal; direction: ltr; orphans: 2; widows: 2; background-color: #f9f9f9; font-variant-ligatures: normal; font-variant-caps: normal; -webkit-text-stroke-width: 0px; -webkit-font-smoothing: auto;">UseMvc</code><span style="color: #000000; text-transform: none; text-indent: 0px; letter-spacing: normal; font-family: segoe-ui_normal, 'Segoe UI', Segoe, 'Segoe WP', 'Helvetica Neue', Helvetica, sans-serif; font-size: 16px; font-style: normal; font-weight: normal; word-spacing: 0px; float: none; display: inline !important; white-space: normal; orphans: 2; widows: 2; background-color: #ffffff; font-variant-ligatures: normal; font-variant-caps: normal; -webkit-text-stroke-width: 0px;"><span class="Apple-converted-space">&nbsp;扩展方法将<a class="xref" style="color: #0078d7; text-transform: none; text-indent: 0px; letter-spacing: normal; font-family: segoe-ui_normal, 'Segoe UI', Segoe, 'Segoe WP', 'Helvetica Neue', Helvetica, sans-serif; font-size: 16px; font-style: normal; font-weight: normal; text-decoration: underline; word-spacing: 0px; white-space: normal; cursor: pointer; -ms-word-wrap: break-word; orphans: 2; widows: 2; background-color: #ffffff; font-variant-ligatures: normal; font-variant-caps: normal; -webkit-text-stroke-width: 0px;" href="https://docs.microsoft.com/zh-cn/aspnet/core/fundamentals/routing" data-linktype="relative-path">路由中间件</a><span style="color: #000000; text-transform: none; text-indent: 0px; letter-spacing: normal; font-family: segoe-ui_normal, 'Segoe UI', Segoe, 'Segoe WP', 'Helvetica Neue', Helvetica, sans-serif; font-size: 16px; font-style: normal; font-weight: normal; word-spacing: 0px; float: none; display: inline !important; white-space: normal; orphans: 2; widows: 2; background-color: #ffffff; font-variant-ligatures: normal; font-variant-caps: normal; -webkit-text-stroke-width: 0px;">添加到请求管道，并将<span class="Apple-converted-space">&nbsp;<a class="xref" style="color: #0078d7; text-transform: none; text-indent: 0px; letter-spacing: normal; font-family: segoe-ui_normal, 'Segoe UI', Segoe, 'Segoe WP', 'Helvetica Neue', Helvetica, sans-serif; font-size: 16px; font-style: normal; font-weight: normal; text-decoration: underline; word-spacing: 0px; white-space: normal; cursor: pointer; -ms-word-wrap: break-word; orphans: 2; widows: 2; background-color: #ffffff; font-variant-ligatures: normal; font-variant-caps: normal; -webkit-text-stroke-width: 0px;" href="https://docs.microsoft.com/zh-cn/aspnet/core/mvc/overview" data-linktype="relative-path">MVC</a><span style="color: #000000; text-transform: none; text-indent: 0px; letter-spacing: normal; font-family: segoe-ui_normal, 'Segoe UI', Segoe, 'Segoe WP', 'Helvetica Neue', Helvetica, sans-serif; font-size: 16px; font-style: normal; font-weight: normal; word-spacing: 0px; float: none; display: inline !important; white-space: normal; orphans: 2; widows: 2; background-color: #ffffff; font-variant-ligatures: normal; font-variant-caps: normal; -webkit-text-stroke-width: 0px;"><span class="Apple-converted-space">&nbsp;配置为默认设置。</span></span></span></span></span></span>&nbsp;</p>
<p>&nbsp;</p>
<p><strong>4，添加过滤器<a name="a14"></a></strong></p>
<p>①定义Middleware</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('f92f48de-b087-4c05-a2bb-336e61b94f1b')"><img id="code_img_closed_f92f48de-b087-4c05-a2bb-336e61b94f1b" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_f92f48de-b087-4c05-a2bb-336e61b94f1b" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('f92f48de-b087-4c05-a2bb-336e61b94f1b',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_f92f48de-b087-4c05-a2bb-336e61b94f1b" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Net;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Http;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Options;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> WebApplication1.Models;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> WebApplication1
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> RequestSetOptionsMiddleware
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> RequestDelegate _next;
        </span><span style="color: #0000ff;">private</span> IOptions&lt;AppOptions&gt;<span style="color: #000000;"> _injectedOptions;

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> RequestSetOptionsMiddleware(
            RequestDelegate next, IOptions</span>&lt;AppOptions&gt;<span style="color: #000000;"> injectedOptions)
        {
            _next </span>=<span style="color: #000000;"> next;
            _injectedOptions </span>=<span style="color: #000000;"> injectedOptions;
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span><span style="color: #000000;"> Task Invoke(HttpContext httpContext)
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">RequestSetOptionsMiddleware.Invoke</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            </span><span style="color: #0000ff;">var</span> option = httpContext.Request.Query[<span style="color: #800000;">"</span><span style="color: #800000;">option</span><span style="color: #800000;">"</span><span style="color: #000000;">];

            </span><span style="color: #0000ff;">if</span> (!<span style="color: #0000ff;">string</span><span style="color: #000000;">.IsNullOrWhiteSpace(option))
            {
                _injectedOptions.Value.Option </span>=<span style="color: #000000;"> WebUtility.HtmlEncode(option);
            }

            </span><span style="color: #0000ff;">await</span><span style="color: #000000;"> _next(httpContext);
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">RequestSetOptionsMiddleware</span></div>
<p>②实现IStartupFilter</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('c6a5f1da-37d9-4b4a-9671-536dbeeb0bb1')"><img id="code_img_closed_c6a5f1da-37d9-4b4a-9671-536dbeeb0bb1" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_c6a5f1da-37d9-4b4a-9671-536dbeeb0bb1" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('c6a5f1da-37d9-4b4a-9671-536dbeeb0bb1',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_c6a5f1da-37d9-4b4a-9671-536dbeeb0bb1" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Hosting;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Builder;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> WebApplication1
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> RequestSetOptionsStartupFilter : IStartupFilter
    {
        </span><span style="color: #0000ff;">public</span> Action&lt;IApplicationBuilder&gt; Configure(Action&lt;IApplicationBuilder&gt;<span style="color: #000000;"> next)
        {
            </span><span style="color: #0000ff;">return</span> builder =&gt;<span style="color: #000000;">
            {
                builder.UseMiddleware</span>&lt;RequestSetOptionsMiddleware&gt;<span style="color: #000000;">();
                next(builder);
            };
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">RequestSetOptionsStartupFilter</span></div>
<p><span style="color: #000000; text-transform: none; text-indent: 0px; letter-spacing: normal; font-family: segoe-ui_normal, 'Segoe UI', Segoe, 'Segoe WP', 'Helvetica Neue', Helvetica, sans-serif; font-size: 16px; font-style: normal; font-weight: normal; word-spacing: 0px; float: none; display: inline !important; white-space: normal; orphans: 2; widows: 2; background-color: #ffffff; font-variant-ligatures: normal; font-variant-caps: normal; -webkit-text-stroke-width: 0px;">③在<span class="Apple-converted-space">&nbsp;<code style="padding: 3px 7px; border-radius: 2px; border: 1px solid #d3d6db; color: #000000; text-transform: none; line-height: 19px; text-indent: 0px; letter-spacing: normal; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, sans-serif; font-size: 0.8rem; font-style: normal; font-weight: normal; word-spacing: 0px; display: inline-block; white-space: normal; direction: ltr; orphans: 2; widows: 2; background-color: #f9f9f9; font-variant-ligatures: normal; font-variant-caps: normal; -webkit-text-stroke-width: 0px; -webkit-font-smoothing: auto;">ConfigureServices</code><span style="color: #000000; text-transform: none; text-indent: 0px; letter-spacing: normal; font-family: segoe-ui_normal, 'Segoe UI', Segoe, 'Segoe WP', 'Helvetica Neue', Helvetica, sans-serif; font-size: 16px; font-style: normal; font-weight: normal; word-spacing: 0px; float: none; display: inline !important; white-space: normal; orphans: 2; widows: 2; background-color: #ffffff; font-variant-ligatures: normal; font-variant-caps: normal; -webkit-text-stroke-width: 0px;"><span class="Apple-converted-space">&nbsp;的服务容器中注册<span class="Apple-converted-space">&nbsp;<code style="padding: 3px 7px; border-radius: 2px; border: 1px solid #d3d6db; color: #000000; text-transform: none; line-height: 19px; text-indent: 0px; letter-spacing: normal; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, sans-serif; font-size: 0.8rem; font-style: normal; font-weight: normal; word-spacing: 0px; display: inline-block; white-space: normal; direction: ltr; orphans: 2; widows: 2; background-color: #f9f9f9; font-variant-ligatures: normal; font-variant-caps: normal; -webkit-text-stroke-width: 0px; -webkit-font-smoothing: auto;">IStartupFilter</code></span></span></span></span></span></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('9d6c79a5-4ce7-4bee-90e9-019f523ac274')"><img id="code_img_closed_9d6c79a5-4ce7-4bee-90e9-019f523ac274" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_9d6c79a5-4ce7-4bee-90e9-019f523ac274" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('9d6c79a5-4ce7-4bee-90e9-019f523ac274',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_9d6c79a5-4ce7-4bee-90e9-019f523ac274" class="cnblogs_code_hide">
<pre>        <span style="color: #008000;">//</span><span style="color: #008000;"> This method gets called by the runtime. Use this method to add services to the container.</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> ConfigureServices(IServiceCollection services)
        {
            services.AddTransient</span>&lt;IStartupFilter, RequestSetOptionsStartupFilter&gt;<span style="color: #000000;">();
            services.AddMvc();
        }</span></pre>
</div>
<span class="cnblogs_code_collapse">Code</span></div>
<p>&nbsp;</p>
<p><strong>5，依赖注入<a name="a15"></a></strong></p>
<p>①注册案例</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('ff53763a-8f39-4312-beaf-8ef5e6bf556d')"><img id="code_img_closed_ff53763a-8f39-4312-beaf-8ef5e6bf556d" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_ff53763a-8f39-4312-beaf-8ef5e6bf556d" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('ff53763a-8f39-4312-beaf-8ef5e6bf556d',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_ff53763a-8f39-4312-beaf-8ef5e6bf556d" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> ConfigureServices(IServiceCollection services)
{
    services.AddDbContext</span>&lt;ApplicationDbContext&gt;(options =&gt;<span style="color: #000000;">
        options.UseInMemoryDatabase()
    );

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> Add framework services.</span>
<span style="color: #000000;">    services.AddMvc();

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> Register application services.</span>
    services.AddScoped&lt;ICharacterRepository, CharacterRepository&gt;<span style="color: #000000;">();
    services.AddTransient</span>&lt;IOperationTransient, Operation&gt;<span style="color: #000000;">();
    services.AddScoped</span>&lt;IOperationScoped, Operation&gt;<span style="color: #000000;">();
    services.AddSingleton</span>&lt;IOperationSingleton, Operation&gt;<span style="color: #000000;">();
    services.AddSingleton</span>&lt;IOperationSingletonInstance&gt;(<span style="color: #0000ff;">new</span><span style="color: #000000;"> Operation(Guid.Empty));
    services.AddTransient</span>&lt;OperationService, OperationService&gt;<span style="color: #000000;">();
}</span></pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<p>&nbsp;</p>
<p><strong>6，中间件<a name="a16"></a></strong></p>
<p>①中间件排序</p>
<div>Configure方法中定义的中间的顺序决定请求的顺序，响应的顺序则相反</div>
<p>②Use、Run 和 Map</p>
<p>Run：不会调用next方法。后面的管道将不会执行</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('25897bdf-e252-42f4-9cc2-898db097ae9b')"><img id="code_img_closed_25897bdf-e252-42f4-9cc2-898db097ae9b" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_25897bdf-e252-42f4-9cc2-898db097ae9b" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('25897bdf-e252-42f4-9cc2-898db097ae9b',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_25897bdf-e252-42f4-9cc2-898db097ae9b" class="cnblogs_code_hide">
<pre>        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configure(IApplicationBuilder app, IHostingEnvironment env)
        {
            
            app.Run(</span><span style="color: #0000ff;">async</span> (context)=&gt;<span style="color: #000000;">{
                 </span><span style="color: #0000ff;">await</span> context.Response.WriteAsync(<span style="color: #800000;">"</span><span style="color: #800000;">Map Test 1</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            });

            </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (env.IsDevelopment())
            {
                app.UseDeveloperExceptionPage();
            }
            </span><span style="color: #0000ff;">else</span><span style="color: #000000;">
            {
                app.UseExceptionHandler(</span><span style="color: #800000;">"</span><span style="color: #800000;">/Home/Error</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }

            </span><span style="color: #008000;">//</span><span style="color: #008000;">使用wwwroot</span>
<span style="color: #000000;">            app.UseStaticFiles();

            app.UseMvc(routes </span>=&gt;<span style="color: #000000;">
            {
                routes.MapRoute(
                    name: </span><span style="color: #800000;">"</span><span style="color: #800000;">default</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    template: </span><span style="color: #800000;">"</span><span style="color: #800000;">{controller=Home}/{action=Index}/{id?}</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            });

           
        }</span></pre>
</div>
<span class="cnblogs_code_collapse">Run</span></div>
<p>Use：如果中间件不调用next方法，会使管道短路。</p>
<p>Map：如果请求路径以给定路径开头，则执行分支。</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('bafa269a-cbb5-4052-bcf8-457e7abea910')"><img id="code_img_closed_bafa269a-cbb5-4052-bcf8-457e7abea910" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_bafa269a-cbb5-4052-bcf8-457e7abea910" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('bafa269a-cbb5-4052-bcf8-457e7abea910',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_bafa269a-cbb5-4052-bcf8-457e7abea910" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Startup
{
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> HandleMapTest1(IApplicationBuilder app)
    {
        app.Run(</span><span style="color: #0000ff;">async</span> context =&gt;<span style="color: #000000;">
        {
            </span><span style="color: #0000ff;">await</span> context.Response.WriteAsync(<span style="color: #800000;">"</span><span style="color: #800000;">Map Test 1</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        });
    }

    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> HandleMapTest2(IApplicationBuilder app)
    {
        app.Run(</span><span style="color: #0000ff;">async</span> context =&gt;<span style="color: #000000;">
        {
            </span><span style="color: #0000ff;">await</span> context.Response.WriteAsync(<span style="color: #800000;">"</span><span style="color: #800000;">Map Test 2</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        });
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configure(IApplicationBuilder app)
    {
        app.Map(</span><span style="color: #800000;">"</span><span style="color: #800000;">/map1</span><span style="color: #800000;">"</span><span style="color: #000000;">, HandleMapTest1);

        app.Map(</span><span style="color: #800000;">"</span><span style="color: #800000;">/map2</span><span style="color: #800000;">"</span><span style="color: #000000;">, HandleMapTest2);

        app.Run(</span><span style="color: #0000ff;">async</span> context =&gt;<span style="color: #000000;">
        {
            </span><span style="color: #0000ff;">await</span> context.Response.WriteAsync(<span style="color: #800000;">"</span><span style="color: #800000;">Hello from non-Map delegate. &lt;p&gt;</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        });
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Map</span></div>
<p><img src="https://images2018.cnblogs.com/blog/741594/201805/741594-20180524194830116-538039297.png" alt="" width="332" height="129" /></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('3db9aa33-990b-43fe-8f4d-82f80053117d')"><img id="code_img_closed_3db9aa33-990b-43fe-8f4d-82f80053117d" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_3db9aa33-990b-43fe-8f4d-82f80053117d" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('3db9aa33-990b-43fe-8f4d-82f80053117d',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_3db9aa33-990b-43fe-8f4d-82f80053117d" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Startup
{
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> HandleBranch(IApplicationBuilder app)
    {
        app.Run(</span><span style="color: #0000ff;">async</span> context =&gt;<span style="color: #000000;">
        {
            </span><span style="color: #0000ff;">var</span> branchVer = context.Request.Query[<span style="color: #800000;">"</span><span style="color: #800000;">branch</span><span style="color: #800000;">"</span><span style="color: #000000;">];
            </span><span style="color: #0000ff;">await</span> context.Response.WriteAsync($<span style="color: #800000;">"</span><span style="color: #800000;">Branch used = {branchVer}</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        });
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configure(IApplicationBuilder app)
    {
        app.MapWhen(context </span>=&gt; context.Request.Query.ContainsKey(<span style="color: #800000;">"</span><span style="color: #800000;">branch</span><span style="color: #800000;">"</span><span style="color: #000000;">),
                               HandleBranch);

        app.Run(</span><span style="color: #0000ff;">async</span> context =&gt;<span style="color: #000000;">
        {
            </span><span style="color: #0000ff;">await</span> context.Response.WriteAsync(<span style="color: #800000;">"</span><span style="color: #800000;">Hello from non-Map delegate. &lt;p&gt;</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        });
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">MapWhen 基于给定谓词的结果创建请求管道分支</span></div>
<p><img src="https://images2018.cnblogs.com/blog/741594/201805/741594-20180524195707064-741181327.png" alt="" width="322" height="57" /></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('47b371ed-892f-4c8a-8cff-b48e3e8197df')"><img id="code_img_closed_47b371ed-892f-4c8a-8cff-b48e3e8197df" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_47b371ed-892f-4c8a-8cff-b48e3e8197df" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('47b371ed-892f-4c8a-8cff-b48e3e8197df',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_47b371ed-892f-4c8a-8cff-b48e3e8197df" class="cnblogs_code_hide">
<pre>app.Map(<span style="color: #800000;">"</span><span style="color: #800000;">/level1</span><span style="color: #800000;">"</span>, level1App =&gt;<span style="color: #000000;"> {
       level1App.Map(</span><span style="color: #800000;">"</span><span style="color: #800000;">/level2a</span><span style="color: #800000;">"</span>, level2AApp =&gt;<span style="color: #000000;"> {
           </span><span style="color: #008000;">//</span><span style="color: #008000;"> "/level1/level2a"
           </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">       });
       level1App.Map(</span><span style="color: #800000;">"</span><span style="color: #800000;">/level2b</span><span style="color: #800000;">"</span>, level2BApp =&gt;<span style="color: #000000;"> {
           </span><span style="color: #008000;">//</span><span style="color: #008000;"> "/level1/level2b"
           </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">       });
   });</span></pre>
</div>
<span class="cnblogs_code_collapse">Map 支持嵌套</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('d525c8e1-a6d6-420c-a4c7-9f8ac92a4c01')"><img id="code_img_closed_d525c8e1-a6d6-420c-a4c7-9f8ac92a4c01" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_d525c8e1-a6d6-420c-a4c7-9f8ac92a4c01" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('d525c8e1-a6d6-420c-a4c7-9f8ac92a4c01',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_d525c8e1-a6d6-420c-a4c7-9f8ac92a4c01" class="cnblogs_code_hide">
<pre>app.Map(<span style="color: #800000;">"</span><span style="color: #800000;">/level1/level2</span><span style="color: #800000;">"</span>, HandleMultiSeg);</pre>
</div>
<span class="cnblogs_code_collapse">Map 还可同时匹配多个段</span></div>
<p>③自定义Middleware</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('b4051e41-abed-48be-bf3c-d0e1e4db93f4')"><img id="code_img_closed_b4051e41-abed-48be-bf3c-d0e1e4db93f4" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_b4051e41-abed-48be-bf3c-d0e1e4db93f4" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('b4051e41-abed-48be-bf3c-d0e1e4db93f4',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_b4051e41-abed-48be-bf3c-d0e1e4db93f4" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Builder;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Http;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Globalization;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> IocDemo
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> CustomMiddleware
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> RequestDelegate _next;

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> CustomMiddleware(RequestDelegate next)
        {
            _next</span>=<span style="color: #000000;">next;
        }
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Task InvokeAsync(HttpContext context)
        {
            </span><span style="color: #0000ff;">this</span><span style="color: #000000;">._next.Invoke(context); 
            context.Response.WriteAsync(</span><span style="color: #800000;">"</span><span style="color: #800000;">CustomMiddleware</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> Task.CompletedTask;
        }
    }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> CustomMiddlewareExtensions
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> IApplicationBuilder UseCustomer(<span style="color: #0000ff;">this</span><span style="color: #000000;"> IApplicationBuilder budiler)
        {
            </span><span style="color: #0000ff;">return</span> budiler.UseMiddleware&lt;CustomMiddleware&gt;<span style="color: #000000;">();
        }

    }

   
}</span></pre>
</div>
<span class="cnblogs_code_collapse">CustomMiddleware</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('58e3175c-2ebf-456b-bf63-e19a646b90c1')"><img id="code_img_closed_58e3175c-2ebf-456b-bf63-e19a646b90c1" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_58e3175c-2ebf-456b-bf63-e19a646b90c1" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('58e3175c-2ebf-456b-bf63-e19a646b90c1',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_58e3175c-2ebf-456b-bf63-e19a646b90c1" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Builder;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Hosting;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Http;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Configuration;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.DependencyInjection;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> IocDemo
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Startup
    {
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Startup(IConfiguration configuration)
        {
            Configuration </span>=<span style="color: #000000;"> configuration;
        }

        </span><span style="color: #0000ff;">public</span> IConfiguration Configuration { <span style="color: #0000ff;">get</span><span style="color: #000000;">; }

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> This method gets called by the runtime. Use this method to add services to the container.</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> ConfigureServices(IServiceCollection services)
        {
            services.AddMvc();
        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> This method gets called by the runtime. Use this method to configure the HTTP request pipeline.</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configure(IApplicationBuilder app, IHostingEnvironment env)
        {

            </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (env.IsDevelopment())
            {
                app.UseDeveloperExceptionPage();
            }
            </span><span style="color: #0000ff;">else</span><span style="color: #000000;">
            {
                app.UseExceptionHandler(</span><span style="color: #800000;">"</span><span style="color: #800000;">/Home/Error</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }

            </span><span style="color: #008000;">//</span><span style="color: #008000;">使用自定义middleware</span>
<span style="color: #000000;">            app.UseCustomer();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">使用wwwroot</span>
<span style="color: #000000;">            app.UseStaticFiles();

            app.UseMvc(routes </span>=&gt;<span style="color: #000000;">
            {
                routes.MapRoute(
                    name: </span><span style="color: #800000;">"</span><span style="color: #800000;">default</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    template: </span><span style="color: #800000;">"</span><span style="color: #800000;">{controller=Home}/{action=Index}/{id?}</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            });

           
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Startup</span></div>
<p>&nbsp;</p>
<p><strong>7，静态文件<a name="a17"></a></strong></p>
<p>①<span data-ttu-id="101b0-135">提供 Web 根目录外的文件</span></p>
<p><span data-ttu-id="101b0-135">请求 http://&lt;server_address&gt;/StaticFiles/images/banner1.svg 提供 banner1.svg 文件</span></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('de7a8fe9-9172-498e-b82b-5052b419cf61')"><img id="code_img_closed_de7a8fe9-9172-498e-b82b-5052b419cf61" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_de7a8fe9-9172-498e-b82b-5052b419cf61" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('de7a8fe9-9172-498e-b82b-5052b419cf61',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_de7a8fe9-9172-498e-b82b-5052b419cf61" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configure(IApplicationBuilder app)
{
    app.UseStaticFiles(); </span><span style="color: #008000;">//</span><span style="color: #008000;"> For the wwwroot folder</span>
<span style="color: #000000;">
    app.UseStaticFiles(</span><span style="color: #0000ff;">new</span><span style="color: #000000;"> StaticFileOptions
    {
        FileProvider </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> PhysicalFileProvider(
            Path.Combine(Directory.GetCurrentDirectory(), </span><span style="color: #800000;">"</span><span style="color: #800000;">MyStaticFiles</span><span style="color: #800000;">"</span><span style="color: #000000;">)),
        RequestPath </span>= <span style="color: #800000;">"</span><span style="color: #800000;">/StaticFiles</span><span style="color: #800000;">"</span><span style="color: #000000;">
    });
}</span></pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<p>②<span class="x-hidden-focus" data-ttu-id="101b0-148">设置 HTTP 响应标头</span></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('74b42f0c-3d32-4a40-b673-dbaa002ac1fd')"><img id="code_img_closed_74b42f0c-3d32-4a40-b673-dbaa002ac1fd" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_74b42f0c-3d32-4a40-b673-dbaa002ac1fd" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('74b42f0c-3d32-4a40-b673-dbaa002ac1fd',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_74b42f0c-3d32-4a40-b673-dbaa002ac1fd" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configure(IApplicationBuilder app)
{
    app.UseStaticFiles(</span><span style="color: #0000ff;">new</span><span style="color: #000000;"> StaticFileOptions
    {
        OnPrepareResponse </span>= ctx =&gt;<span style="color: #000000;">
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> Requires the following import:
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> using Microsoft.AspNetCore.Http;</span>
            ctx.Context.Response.Headers.Append(<span style="color: #800000;">"</span><span style="color: #800000;">Cache-Control</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">public,max-age=600</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }
    });
}</span></pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<p>③静态文件授权方法</p>
<p>新建个静态文件根文件夹</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('9418e1c8-1896-4362-a7ed-47f0a7f1fa4f')"><img id="code_img_closed_9418e1c8-1896-4362-a7ed-47f0a7f1fa4f" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_9418e1c8-1896-4362-a7ed-47f0a7f1fa4f" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('9418e1c8-1896-4362-a7ed-47f0a7f1fa4f',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_9418e1c8-1896-4362-a7ed-47f0a7f1fa4f" class="cnblogs_code_hide">
<pre><span style="color: #000000;">[Authorize]
</span><span style="color: #0000ff;">public</span><span style="color: #000000;"> IActionResult BannerImage()
{
    </span><span style="color: #0000ff;">var</span> file =<span style="color: #000000;"> Path.Combine(Directory.GetCurrentDirectory(), 
                            </span><span style="color: #800000;">"</span><span style="color: #800000;">MyStaticFiles</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">images</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">banner1.svg</span><span style="color: #800000;">"</span><span style="color: #000000;">);

    </span><span style="color: #0000ff;">return</span> PhysicalFile(file, <span style="color: #800000;">"</span><span style="color: #800000;">image/svg+xml</span><span style="color: #800000;">"</span><span style="color: #000000;">);
}</span></pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<p>④默认提供文档</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('0f1b21e9-a5ad-4572-be93-26240344195f')"><img id="code_img_closed_0f1b21e9-a5ad-4572-be93-26240344195f" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_0f1b21e9-a5ad-4572-be93-26240344195f" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('0f1b21e9-a5ad-4572-be93-26240344195f',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_0f1b21e9-a5ad-4572-be93-26240344195f" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configure(IApplicationBuilder app)
{
    app.UseDefaultFiles();
    app.UseStaticFiles();
}</span></pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<p><span data-ttu-id="101b0-175">要提供默认文件，必须在&nbsp;<code>UseStaticFiles</code>&nbsp;前调用&nbsp;<code>UseDefaultFiles</code>。&nbsp;<span data-ttu-id="101b0-176"><code>UseDefaultFiles</code>&nbsp;实际上用于重写 URL，不提供文件。&nbsp;<span data-ttu-id="101b0-177">通过&nbsp;<code>UseStaticFiles</code>&nbsp;启用静态文件中间件来提供文件。</span></span></span></p>
<p>&nbsp;<img src="https://images2018.cnblogs.com/blog/741594/201805/741594-20180525185347295-974198163.png" alt="" width="172" height="89" /></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('01e06eaa-178f-4dce-99be-fa4cdc3a8fff')"><img id="code_img_closed_01e06eaa-178f-4dce-99be-fa4cdc3a8fff" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_01e06eaa-178f-4dce-99be-fa4cdc3a8fff" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('01e06eaa-178f-4dce-99be-fa4cdc3a8fff',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_01e06eaa-178f-4dce-99be-fa4cdc3a8fff" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configure(IApplicationBuilder app)
{
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> Serve my app-specific default file, if present.</span>
    DefaultFilesOptions options = <span style="color: #0000ff;">new</span><span style="color: #000000;"> DefaultFilesOptions();
    options.DefaultFileNames.Clear();
    options.DefaultFileNames.Add(</span><span style="color: #800000;">"</span><span style="color: #800000;">mydefault.html</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    app.UseDefaultFiles(options);
    app.UseStaticFiles();
}</span></pre>
</div>
<span class="cnblogs_code_collapse">将默认文件名更改为 mydefault.html</span></div>
<p>&nbsp;</p>
<p><strong>8，路由<a name="a18"></a></strong></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('df0224e2-a800-4f63-9473-88ea328b6a5a')"><img id="code_img_closed_df0224e2-a800-4f63-9473-88ea328b6a5a" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_df0224e2-a800-4f63-9473-88ea328b6a5a" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('df0224e2-a800-4f63-9473-88ea328b6a5a',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_df0224e2-a800-4f63-9473-88ea328b6a5a" class="cnblogs_code_hide">
<pre><span style="color: #000000;">routes.MapRoute(
    name: </span><span style="color: #800000;">"</span><span style="color: #800000;">default</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    template: </span><span style="color: #800000;">"</span><span style="color: #800000;">{controller=Home}/{action=Index}/{id?}</span><span style="color: #800000;">"</span>);</pre>
</div>
<span class="cnblogs_code_collapse">典型路由</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('251fa7ad-e10a-4386-b387-435edb1b37cb')"><img id="code_img_closed_251fa7ad-e10a-4386-b387-435edb1b37cb" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_251fa7ad-e10a-4386-b387-435edb1b37cb" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('251fa7ad-e10a-4386-b387-435edb1b37cb',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_251fa7ad-e10a-4386-b387-435edb1b37cb" class="cnblogs_code_hide">
<pre><span style="color: #000000;">routes.MapRoute(
    name: </span><span style="color: #800000;">"</span><span style="color: #800000;">default</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    template: </span><span style="color: #800000;">"</span><span style="color: #800000;">{controller=Home}/{action=Index}/{id:int}</span><span style="color: #800000;">"</span>);</pre>
</div>
<span class="cnblogs_code_collapse">路由约束</span></div>
<p>①尾随句点&nbsp;<span class="cnblogs_code"> . </span>&nbsp;是可选：&nbsp;<span class="cnblogs_code">files/{filename}.{ext?}</span>&nbsp;</p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201805/741594-20180525194352081-548818071.png" alt="" /></p>
<p>②*全方位参数：&nbsp;<span class="cnblogs_code">blog/{*slug}</span>&nbsp;</p>
<p>&nbsp;将匹配以&nbsp;<code>/blog</code>&nbsp;开头且其后带有任何值（将分配给&nbsp;<code>slug</code>&nbsp;路由值）的 URI</p>
<p>&nbsp;</p>
<p><strong>9，环境<a name="a19"></a></strong></p>
<p>ASP.NET Core 在应用程序启动时读取环境变量&nbsp;<code>ASPNETCORE_ENVIRONMENT（<span style="font-size: 12px;">如果未设置&nbsp;<code>ASPNETCORE_ENVIRONMENT</code>，将默认为&nbsp;<code>Production</code></span>）</code></p>
<p><span style="font-size: 12px;">ASPNETCORE_ENVIRONMENT值：</span></p>
<ul>
<li><span style="font-size: 12px;">Development（开发）</span></li>
<li><span style="font-size: 12px;">Production（生产）</span></li>
<li><span style="font-size: 12px;">Staging（暂存）</span></li>
</ul>
<p>&nbsp;</p>
<p><strong>10，配置和选项<a name="a110"></a></strong></p>
<p>nuget&nbsp;<span class="cnblogs_code">Microsoft.Extensions.Configuration</span>&nbsp;</p>
<p>①读取json文件</p>
<p>nuget&nbsp;<span class="cnblogs_code">Microsoft.Extensions.Configuration.Json</span>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('958d50fe-ab2b-45f3-a01d-3ce059a73d82')"><img id="code_img_closed_958d50fe-ab2b-45f3-a01d-3ce059a73d82" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_958d50fe-ab2b-45f3-a01d-3ce059a73d82" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('958d50fe-ab2b-45f3-a01d-3ce059a73d82',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_958d50fe-ab2b-45f3-a01d-3ce059a73d82" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.IO;
</span><span style="color: #008000;">//</span><span style="color: #008000;"> Requires NuGet package
</span><span style="color: #008000;">//</span><span style="color: #008000;"> Microsoft.Extensions.Configuration.Json</span>
<span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Configuration;

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> IConfiguration Configuration { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span>[] args = <span style="color: #0000ff;">null</span><span style="color: #000000;">)
    {
        </span><span style="color: #0000ff;">var</span> builder = <span style="color: #0000ff;">new</span><span style="color: #000000;"> ConfigurationBuilder()
            .SetBasePath(Directory.GetCurrentDirectory())
            .AddJsonFile(</span><span style="color: #800000;">"</span><span style="color: #800000;">appsettings.json</span><span style="color: #800000;">"</span><span style="color: #000000;">);

        Configuration </span>=<span style="color: #000000;"> builder.Build();

        Console.WriteLine($</span><span style="color: #800000;">"</span><span style="color: #800000;">option1 = {Configuration[</span><span style="color: #800000;">"</span>Option1<span style="color: #800000;">"</span><span style="color: #800000;">]}</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        Console.WriteLine($</span><span style="color: #800000;">"</span><span style="color: #800000;">option2 = {Configuration[</span><span style="color: #800000;">"</span>option2<span style="color: #800000;">"</span><span style="color: #800000;">]}</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        Console.WriteLine(
            $</span><span style="color: #800000;">"</span><span style="color: #800000;">suboption1 = {Configuration[</span><span style="color: #800000;">"</span>subsection:suboption1<span style="color: #800000;">"</span><span style="color: #800000;">]}</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        Console.WriteLine();

        Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">Wizards:</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        Console.Write($</span><span style="color: #800000;">"</span><span style="color: #800000;">{Configuration[</span><span style="color: #800000;">"</span>wizards:<span style="color: #800080;">0</span>:Name<span style="color: #800000;">"</span><span style="color: #800000;">]}, </span><span style="color: #800000;">"</span><span style="color: #000000;">);
        Console.WriteLine($</span><span style="color: #800000;">"</span><span style="color: #800000;">age {Configuration[</span><span style="color: #800000;">"</span>wizards:<span style="color: #800080;">0</span>:Age<span style="color: #800000;">"</span><span style="color: #800000;">]}</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        Console.Write($</span><span style="color: #800000;">"</span><span style="color: #800000;">{Configuration[</span><span style="color: #800000;">"</span>wizards:<span style="color: #800080;">1</span>:Name<span style="color: #800000;">"</span><span style="color: #800000;">]}, </span><span style="color: #800000;">"</span><span style="color: #000000;">);
        Console.WriteLine($</span><span style="color: #800000;">"</span><span style="color: #800000;">age {Configuration[</span><span style="color: #800000;">"</span>wizards:<span style="color: #800080;">1</span>:Age<span style="color: #800000;">"</span><span style="color: #800000;">]}</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        Console.WriteLine();

        Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">Press a key...</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        Console.ReadKey();
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('0ec7fc3a-fc3e-42bb-9bab-2dcbcd9bae60')"><img id="code_img_closed_0ec7fc3a-fc3e-42bb-9bab-2dcbcd9bae60" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_0ec7fc3a-fc3e-42bb-9bab-2dcbcd9bae60" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('0ec7fc3a-fc3e-42bb-9bab-2dcbcd9bae60',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_0ec7fc3a-fc3e-42bb-9bab-2dcbcd9bae60" class="cnblogs_code_hide">
<pre><span style="color: #000000;">{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">option1</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">value1_from_json</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">option2</span><span style="color: #800000;">"</span>: <span style="color: #800080;">2</span><span style="color: #000000;">,

  </span><span style="color: #800000;">"</span><span style="color: #800000;">subsection</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">suboption1</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">subvalue1_from_json</span><span style="color: #800000;">"</span><span style="color: #000000;">
  },
  </span><span style="color: #800000;">"</span><span style="color: #800000;">wizards</span><span style="color: #800000;">"</span><span style="color: #000000;">: [
    {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">Name</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">Gandalf</span><span style="color: #800000;">"</span><span style="color: #000000;">,
      </span><span style="color: #800000;">"</span><span style="color: #800000;">Age</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">1000</span><span style="color: #800000;">"</span><span style="color: #000000;">
    },
    {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">Name</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">Harry</span><span style="color: #800000;">"</span><span style="color: #000000;">,
      </span><span style="color: #800000;">"</span><span style="color: #800000;">Age</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">17</span><span style="color: #800000;">"</span><span style="color: #000000;">
    }
  ]
}</span></pre>
</div>
<span class="cnblogs_code_collapse">json文件内容</span></div>
<p>&nbsp;节点由冒号&nbsp;<span class="cnblogs_code"> : </span>&nbsp;分隔：&nbsp;<span class="cnblogs_code">Configuration[<span style="color: #800000;">"</span><span style="color: #800000;">subsection:suboption1</span><span style="color: #800000;">"</span>]</span>&nbsp;</p>
<p>&nbsp;获取数组值：&nbsp;<span class="cnblogs_code">Configuration[<span style="color: #800000;">"</span><span style="color: #800000;">wizards:0:Name</span><span style="color: #800000;">"</span>]</span>&nbsp;</p>
<p>②读取xml文件</p>
<p>nuget&nbsp;<span class="cnblogs_code">Microsoft.Extensions.Configuration.Xml</span>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('72219785-a367-4098-a0fa-03a1fe70b71f')"><img id="code_img_closed_72219785-a367-4098-a0fa-03a1fe70b71f" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_72219785-a367-4098-a0fa-03a1fe70b71f" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('72219785-a367-4098-a0fa-03a1fe70b71f',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_72219785-a367-4098-a0fa-03a1fe70b71f" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Configuration;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.IO;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ConsoleDemo
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #0000ff;">var</span> builder= <span style="color: #0000ff;">new</span><span style="color: #000000;"> ConfigurationBuilder()
                        .SetBasePath(Directory.GetCurrentDirectory())
                        .AddXmlFile(</span><span style="color: #800000;">"</span><span style="color: #800000;">test.xml</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            </span><span style="color: #0000ff;">var</span> configuration=<span style="color: #000000;">builder.Build();
            Console.WriteLine(configuration[</span><span style="color: #800000;">"</span><span style="color: #800000;">wizard:Harry:age</span><span style="color: #800000;">"</span><span style="color: #000000;">]);
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('6dde652d-f79d-4bac-a863-a4572cd37d62')"><img id="code_img_closed_6dde652d-f79d-4bac-a863-a4572cd37d62" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_6dde652d-f79d-4bac-a863-a4572cd37d62" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('6dde652d-f79d-4bac-a863-a4572cd37d62',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_6dde652d-f79d-4bac-a863-a4572cd37d62" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">wizards</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">wizard </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="Gandalf"</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">age</span><span style="color: #0000ff;">&gt;</span>1000<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">age</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">wizard</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">wizard </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="Harry"</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">age</span><span style="color: #0000ff;">&gt;</span>17<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">age</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">wizard</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">wizards</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<span class="cnblogs_code_collapse">xml文件内容</span></div>
<p>③json绑定到对象里面</p>
<p>nuget&nbsp;<span class="cnblogs_code">Microsoft.Extensions.Configuration.Binder</span>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('0648024f-ba8e-4805-a90a-fd9eabd275fd')"><img id="code_img_closed_0648024f-ba8e-4805-a90a-fd9eabd275fd" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_0648024f-ba8e-4805-a90a-fd9eabd275fd" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('0648024f-ba8e-4805-a90a-fd9eabd275fd',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_0648024f-ba8e-4805-a90a-fd9eabd275fd" class="cnblogs_code_hide">
<pre><span style="color: #000000;">using System;
using Microsoft.Extensions.Configuration;
using System.IO;
using System.Collections.Generic;

namespace ConsoleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            var dic=new Dictionary</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">string</span><span style="color: #ff0000;">,string</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">();
            dic.Add("Person:Name","hunter");
            dic.Add("Person:Age","10");


            var builder=new ConfigurationBuilder()
                        .AddInMemoryCollection(dic);
            IConfiguration configuration=builder.Build();

            var person=new Person();
            configuration.GetSection("Person").Bind(person);
            Console.WriteLine(person.Name);
            Console.WriteLine(person.Age);

        }
    }

    public class Person{
        public string Name{get;set;}
        public int Age{get;set;}
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<p>&nbsp;④在razor视图获取mvc视图中使用configuration</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('a70452a0-4469-4f2a-adb3-2428bb9f0f01')"><img id="code_img_closed_a70452a0-4469-4f2a-adb3-2428bb9f0f01" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_a70452a0-4469-4f2a-adb3-2428bb9f0f01" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('a70452a0-4469-4f2a-adb3-2428bb9f0f01',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_a70452a0-4469-4f2a-adb3-2428bb9f0f01" class="cnblogs_code_hide">
<pre><span style="color: #000000;">@page
@model IndexModel

@using Microsoft.Extensions.Configuration
@inject IConfiguration Configuration

</span><span style="color: #0000ff;">&lt;!</span><span style="color: #ff00ff;">DOCTYPE html</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">html </span><span style="color: #ff0000;">lang</span><span style="color: #0000ff;">="en"</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">head</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">title</span><span style="color: #0000ff;">&gt;</span>Index Page<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">title</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">head</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">body</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">h1</span><span style="color: #0000ff;">&gt;</span>Access configuration in a Razor Pages page<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">h1</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span>Configuration[<span style="color: #ff0000;">&amp;quot;</span>key<span style="color: #ff0000;">&amp;quot;</span>]: @Configuration["key"]<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">body</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">html</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<span class="cnblogs_code_collapse">在 Razor 页面页中</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('3149bc83-7062-438b-b68e-bb990216bddf')"><img id="code_img_closed_3149bc83-7062-438b-b68e-bb990216bddf" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_3149bc83-7062-438b-b68e-bb990216bddf" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('3149bc83-7062-438b-b68e-bb990216bddf',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_3149bc83-7062-438b-b68e-bb990216bddf" class="cnblogs_code_hide">
<pre><span style="color: #000000;">@using Microsoft.Extensions.Configuration
@inject IConfiguration Configuration

</span><span style="color: #0000ff;">&lt;!</span><span style="color: #ff00ff;">DOCTYPE html</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">html </span><span style="color: #ff0000;">lang</span><span style="color: #0000ff;">="en"</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">head</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">title</span><span style="color: #0000ff;">&gt;</span>Index View<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">title</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">head</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">body</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">h1</span><span style="color: #0000ff;">&gt;</span>Access configuration in an MVC view<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">h1</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span>Configuration[<span style="color: #ff0000;">&amp;quot;</span>key<span style="color: #ff0000;">&amp;quot;</span>]: @Configuration["key"]<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">body</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">html</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<span class="cnblogs_code_collapse">在 MVC 视图中</span></div>
<p>&nbsp;④注入option配置</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('ee9360ea-fa0e-4459-9498-f243c56c0613')"><img id="code_img_closed_ee9360ea-fa0e-4459-9498-f243c56c0613" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_ee9360ea-fa0e-4459-9498-f243c56c0613" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('ee9360ea-fa0e-4459-9498-f243c56c0613',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_ee9360ea-fa0e-4459-9498-f243c56c0613" class="cnblogs_code_hide">
<pre><span style="color: #000000;">{
  "Logging": {
    "IncludeScopes": false,
    "LogLevel": {
      "Default": "Warning"
    }
  },
  "Option":{
    "option1":"value1_from_json",
    "option2":-1
  }
 
}</span></pre>
</div>
<span class="cnblogs_code_collapse">appsettings.json</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('5909c1b2-79c1-499d-a39a-92c2af786001')"><img id="code_img_closed_5909c1b2-79c1-499d-a39a-92c2af786001" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_5909c1b2-79c1-499d-a39a-92c2af786001" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('5909c1b2-79c1-499d-a39a-92c2af786001',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_5909c1b2-79c1-499d-a39a-92c2af786001" class="cnblogs_code_hide">
<pre><span style="color: #000000;">  public class MyOption{
        public string option1{get;set;}
        public int option2{get;set;}
    }</span></pre>
</div>
<span class="cnblogs_code_collapse">自定义MyOption类</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('5c84cba1-18dd-4c5a-a58f-55c6062ce599')"><img id="code_img_closed_5c84cba1-18dd-4c5a-a58f-55c6062ce599" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_5c84cba1-18dd-4c5a-a58f-55c6062ce599" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('5c84cba1-18dd-4c5a-a58f-55c6062ce599',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_5c84cba1-18dd-4c5a-a58f-55c6062ce599" class="cnblogs_code_hide">
<pre> services.Configure<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">MyOption</span><span style="color: #0000ff;">&gt;</span>(Configuration.GetSection("Option"));</pre>
</div>
<span class="cnblogs_code_collapse">在ConfigureServices注册</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('55a62c48-684b-4c3f-b79b-238a53d13017')"><img id="code_img_closed_55a62c48-684b-4c3f-b79b-238a53d13017" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_55a62c48-684b-4c3f-b79b-238a53d13017" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('55a62c48-684b-4c3f-b79b-238a53d13017',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_55a62c48-684b-4c3f-b79b-238a53d13017" class="cnblogs_code_hide">
<pre>        private  IOptions<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">MyOption</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;"> _option;
        public BlogController(IOptions</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">MyOption</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;"> option)
        {
            _option=option;
           _option.Value.option1+_option.Value.option2
        }</span></pre>
</div>
<span class="cnblogs_code_collapse">构造注入并使用</span></div>
<p>&nbsp;</p>
<p><strong>11，日志<a name="a111"></a></strong></p>
<p>①创建日志</p>
<p>nuget&nbsp;<span class="cnblogs_code">Microsoft.Extensions.Logging</span>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('8f7b65e0-64c4-4e76-825c-53f0fc8a5e6b')"><img id="code_img_closed_8f7b65e0-64c4-4e76-825c-53f0fc8a5e6b" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_8f7b65e0-64c4-4e76-825c-53f0fc8a5e6b" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('8f7b65e0-64c4-4e76-825c-53f0fc8a5e6b',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_8f7b65e0-64c4-4e76-825c-53f0fc8a5e6b" class="cnblogs_code_hide">
<pre><span style="color: #000000;">public class TodoController : Controller
{
    private readonly ITodoRepository _todoRepository;
    private readonly ILogger _logger;

    public TodoController(ITodoRepository todoRepository,
        ILogger</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">TodoController</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;"> logger)
    {
        _todoRepository = todoRepository;
        _logger = logger;
    }</span></pre>
</div>
<span class="cnblogs_code_collapse">要创建日志，请先从依赖关系注入容器获取 ILogger 对象</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('41c1e02c-7dac-4826-87fa-9c6362c7cef1')"><img id="code_img_closed_41c1e02c-7dac-4826-87fa-9c6362c7cef1" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_41c1e02c-7dac-4826-87fa-9c6362c7cef1" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('41c1e02c-7dac-4826-87fa-9c6362c7cef1',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_41c1e02c-7dac-4826-87fa-9c6362c7cef1" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> IActionResult GetById(<span style="color: #0000ff;">string</span><span style="color: #000000;"> id)
{
    _logger.LogInformation(LoggingEvents.GetItem, </span><span style="color: #800000;">"</span><span style="color: #800000;">Getting item {ID}</span><span style="color: #800000;">"</span><span style="color: #000000;">, id);
    </span><span style="color: #0000ff;">var</span> item =<span style="color: #000000;"> _todoRepository.Find(id);
    </span><span style="color: #0000ff;">if</span> (item == <span style="color: #0000ff;">null</span><span style="color: #000000;">)
    {
        _logger.LogWarning(LoggingEvents.GetItemNotFound, </span><span style="color: #800000;">"</span><span style="color: #800000;">GetById({ID}) NOT FOUND</span><span style="color: #800000;">"</span><span style="color: #000000;">, id);
        </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> NotFound();
    }
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> ObjectResult(item);
}</span></pre>
</div>
<span class="cnblogs_code_collapse">然后在该记录器对象上调用日志记录方法</span></div>
<p>②事件ID</p>
<p>LoggingEvents自己定义例如：</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('4d04a928-5588-4f89-80e4-897fe7d31a50')"><img id="code_img_closed_4d04a928-5588-4f89-80e4-897fe7d31a50" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_4d04a928-5588-4f89-80e4-897fe7d31a50" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('4d04a928-5588-4f89-80e4-897fe7d31a50',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_4d04a928-5588-4f89-80e4-897fe7d31a50" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> LoggingEvents
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">const</span> <span style="color: #0000ff;">int</span> GenerateItems = <span style="color: #800080;">1000</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">const</span> <span style="color: #0000ff;">int</span> ListItems = <span style="color: #800080;">1001</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">const</span> <span style="color: #0000ff;">int</span> GetItem = <span style="color: #800080;">1002</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">const</span> <span style="color: #0000ff;">int</span> InsertItem = <span style="color: #800080;">1003</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">const</span> <span style="color: #0000ff;">int</span> UpdateItem = <span style="color: #800080;">1004</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">const</span> <span style="color: #0000ff;">int</span> DeleteItem = <span style="color: #800080;">1005</span><span style="color: #000000;">;

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">const</span> <span style="color: #0000ff;">int</span> GetItemNotFound = <span style="color: #800080;">4000</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">const</span> <span style="color: #0000ff;">int</span> UpdateItemNotFound = <span style="color: #800080;">4001</span><span style="color: #000000;">;
}</span></pre>
</div>
<span class="cnblogs_code_collapse">LoggingEvents</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('5776a65d-18da-4ab1-b35b-b5e9e005c399')"><img id="code_img_closed_5776a65d-18da-4ab1-b35b-b5e9e005c399" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_5776a65d-18da-4ab1-b35b-b5e9e005c399" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('5776a65d-18da-4ab1-b35b-b5e9e005c399',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_5776a65d-18da-4ab1-b35b-b5e9e005c399" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> IActionResult GetById(<span style="color: #0000ff;">string</span><span style="color: #000000;"> id)
{
    _logger.LogInformation(LoggingEvents.GetItem, </span><span style="color: #800000;">"</span><span style="color: #800000;">Getting item {ID}</span><span style="color: #800000;">"</span><span style="color: #000000;">, id);
    </span><span style="color: #0000ff;">var</span> item =<span style="color: #000000;"> _todoRepository.Find(id);
    </span><span style="color: #0000ff;">if</span> (item == <span style="color: #0000ff;">null</span><span style="color: #000000;">)
    {
        _logger.LogWarning(LoggingEvents.GetItemNotFound, </span><span style="color: #800000;">"</span><span style="color: #800000;">GetById({ID}) NOT FOUND</span><span style="color: #800000;">"</span><span style="color: #000000;">, id);
        </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> NotFound();
    }
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> ObjectResult(item);
}</span></pre>
</div>
<span class="cnblogs_code_collapse">使用案例</span></div>
<p>&nbsp;</p>
<p><strong>12，使用Sesstion<a name="a112"></a></strong></p>
<p>&nbsp;<span class="cnblogs_code"><span style="color: #0000ff;">using</span> Microsoft.AspNetCore.Http</span>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('60a72279-9c81-4f61-ab11-535ca3e2b563')"><img id="code_img_closed_60a72279-9c81-4f61-ab11-535ca3e2b563" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_60a72279-9c81-4f61-ab11-535ca3e2b563" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('60a72279-9c81-4f61-ab11-535ca3e2b563',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_60a72279-9c81-4f61-ab11-535ca3e2b563" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Builder;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Hosting;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Configuration;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.DependencyInjection;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.FileProviders;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> MvcDemo
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Startup
    {
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Startup(IConfiguration configuration, IHostingEnvironment env)
        {
            Configuration </span>=<span style="color: #000000;"> configuration;
            HostingEnvironment</span>=<span style="color: #000000;">env;
        }

        </span><span style="color: #0000ff;">public</span> IConfiguration Configuration { <span style="color: #0000ff;">get</span><span style="color: #000000;">; }
        </span><span style="color: #0000ff;">public</span> IHostingEnvironment HostingEnvironment{<span style="color: #0000ff;">get</span><span style="color: #000000;">;}

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> This method gets called by the runtime. Use this method to add services to the container.</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> ConfigureServices(IServiceCollection services)
        {
            </span><span style="color: #0000ff;">var</span> physicalProvider=<span style="color: #000000;"> HostingEnvironment.ContentRootFileProvider;
            services.AddSingleton</span>&lt;IFileProvider&gt;<span style="color: #000000;">(physicalProvider);

            services.AddSession(option</span>=&gt;<span style="color: #000000;">{
                option.IdleTimeout</span>=TimeSpan.FromSeconds(<span style="color: #800080;">10</span><span style="color: #000000;">);
                option.Cookie.HttpOnly</span>=<span style="color: #0000ff;">true</span>;<span style="color: #008000;">//</span><span style="color: #008000;">指示客户端脚本是否可以访问cookie。</span>
<span style="color: #000000;">            });

            services.AddMvc();
        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> This method gets called by the runtime. Use this method to configure the HTTP request pipeline.</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configure(IApplicationBuilder app, IHostingEnvironment env)
        {
            </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (env.IsDevelopment())
            {
                app.UseDeveloperExceptionPage();
            }
            </span><span style="color: #0000ff;">else</span><span style="color: #000000;">
            {
                app.UseExceptionHandler(</span><span style="color: #800000;">"</span><span style="color: #800000;">/Home/Error</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }

            app.UseSession();</span><span style="color: #008000;">//</span><span style="color: #008000;">要在UseMvc之前调用</span>
<span style="color: #000000;">
            app.UseStaticFiles();

            app.UseMvc(routes </span>=&gt;<span style="color: #000000;">
            {
                routes.MapRoute(
                    name: </span><span style="color: #800000;">"</span><span style="color: #800000;">default</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    template: </span><span style="color: #800000;">"</span><span style="color: #800000;">{controller=Home}/{action=Index}/{id?}</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            });
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Startup</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('8beaac35-6c67-4f32-b5a3-44e013eb3825')"><img id="code_img_closed_8beaac35-6c67-4f32-b5a3-44e013eb3825" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_8beaac35-6c67-4f32-b5a3-44e013eb3825" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('8beaac35-6c67-4f32-b5a3-44e013eb3825',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_8beaac35-6c67-4f32-b5a3-44e013eb3825" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Diagnostics;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Mvc;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> MvcDemo.Models;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.FileProviders;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Http;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> MvcDemo.Controllers
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SesstionController : Controller
    {

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Index(<span style="color: #0000ff;">string</span><span style="color: #000000;"> str)
        {
            HttpContext.Session.SetString(</span><span style="color: #800000;">"</span><span style="color: #800000;">str</span><span style="color: #800000;">"</span><span style="color: #000000;">,str);
            
            </span><span style="color: #0000ff;">return</span> <span style="color: #800000;">"</span><span style="color: #800000;">sesstion已经设置</span><span style="color: #800000;">"</span><span style="color: #000000;">;
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span><span style="color: #000000;"> GetSession()
        {
           </span><span style="color: #0000ff;">var</span> val= HttpContext.Session.GetString(<span style="color: #800000;">"</span><span style="color: #800000;">str</span><span style="color: #800000;">"</span><span style="color: #000000;">);
           </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> val;
        }
        

    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">使用</span></div>
<p>&nbsp;</p>
<p><strong>13，使用po文件配置本地化<a name="a113"></a></strong></p>
<p>nuget&nbsp;<span class="cnblogs_code">OrchardCore.Localization.Core</span>&nbsp;</p>
<p>①配置Startup</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('80f8996e-af5b-4993-8718-d8d257dd9eaf')"><img id="code_img_closed_80f8996e-af5b-4993-8718-d8d257dd9eaf" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_80f8996e-af5b-4993-8718-d8d257dd9eaf" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('80f8996e-af5b-4993-8718-d8d257dd9eaf',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_80f8996e-af5b-4993-8718-d8d257dd9eaf" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Globalization;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Builder;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Hosting;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Localization;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Configuration;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.DependencyInjection;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.FileProviders;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> MvcDemo
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Startup
    {
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Startup(IConfiguration configuration, IHostingEnvironment env)
        {
            Configuration </span>=<span style="color: #000000;"> configuration;
            HostingEnvironment</span>=<span style="color: #000000;">env;
        }

        </span><span style="color: #0000ff;">public</span> IConfiguration Configuration { <span style="color: #0000ff;">get</span><span style="color: #000000;">; }
        </span><span style="color: #0000ff;">public</span> IHostingEnvironment HostingEnvironment{<span style="color: #0000ff;">get</span><span style="color: #000000;">;}

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> This method gets called by the runtime. Use this method to add services to the container.</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> ConfigureServices(IServiceCollection services)
        {
            </span><span style="color: #0000ff;">var</span> physicalProvider=<span style="color: #000000;"> HostingEnvironment.ContentRootFileProvider;
            services.AddSingleton</span>&lt;IFileProvider&gt;<span style="color: #000000;">(physicalProvider);

            services.AddSession(option</span>=&gt;<span style="color: #000000;">{
                option.IdleTimeout</span>=TimeSpan.FromSeconds(<span style="color: #800080;">10</span><span style="color: #000000;">);
                option.Cookie.HttpOnly</span>=<span style="color: #0000ff;">true</span>;<span style="color: #008000;">//</span><span style="color: #008000;">指示客户端脚本是否可以访问cookie。</span>
<span style="color: #000000;">            });

            services.AddLocalization(option</span>=&gt;<span style="color: #000000;">{

            });
            services.AddMvc()
                    .AddViewLocalization();
            services.AddPortableObjectLocalization(options</span>=&gt;<span style="color: #000000;">{
                options.ResourcesPath</span>=<span style="color: #800000;">"</span><span style="color: #800000;">Localization</span><span style="color: #800000;">"</span><span style="color: #000000;">;
            });
            services.Configure</span>&lt;RequestLocalizationOptions&gt;(options =&gt;<span style="color: #000000;">
            {
                </span><span style="color: #0000ff;">var</span> supportedCultures = <span style="color: #0000ff;">new</span> List&lt;CultureInfo&gt;<span style="color: #000000;">
                {
                    </span><span style="color: #0000ff;">new</span> CultureInfo(<span style="color: #800000;">"</span><span style="color: #800000;">en-US</span><span style="color: #800000;">"</span><span style="color: #000000;">),
                    </span><span style="color: #0000ff;">new</span> CultureInfo(<span style="color: #800000;">"</span><span style="color: #800000;">en</span><span style="color: #800000;">"</span><span style="color: #000000;">),
                    </span><span style="color: #0000ff;">new</span> CultureInfo(<span style="color: #800000;">"</span><span style="color: #800000;">fr-FR</span><span style="color: #800000;">"</span><span style="color: #000000;">),
                    </span><span style="color: #0000ff;">new</span> CultureInfo(<span style="color: #800000;">"</span><span style="color: #800000;">fr</span><span style="color: #800000;">"</span><span style="color: #000000;">),
                    </span><span style="color: #0000ff;">new</span> CultureInfo(<span style="color: #800000;">"</span><span style="color: #800000;">zh-CHS</span><span style="color: #800000;">"</span><span style="color: #000000;">)
                };

                options.DefaultRequestCulture </span>= <span style="color: #0000ff;">new</span> RequestCulture(<span style="color: #800000;">"</span><span style="color: #800000;">zh-CHS</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                options.SupportedCultures </span>=<span style="color: #000000;"> supportedCultures;
                options.SupportedUICultures </span>=<span style="color: #000000;"> supportedCultures;
            });

        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> This method gets called by the runtime. Use this method to configure the HTTP request pipeline.</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configure(IApplicationBuilder app, IHostingEnvironment env)
        {
            </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (env.IsDevelopment())
            {
                app.UseDeveloperExceptionPage();
            }
            </span><span style="color: #0000ff;">else</span><span style="color: #000000;">
            {
                app.UseExceptionHandler(</span><span style="color: #800000;">"</span><span style="color: #800000;">/Home/Error</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }

            app.UseSession();</span><span style="color: #008000;">//</span><span style="color: #008000;">要在UseMvc之前调用</span>
<span style="color: #000000;">
            app.UseStaticFiles();

            app.UseRequestLocalization();

            app.UseMvc(routes </span>=&gt;<span style="color: #000000;">
            {
                routes.MapRoute(
                    name: </span><span style="color: #800000;">"</span><span style="color: #800000;">default</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    template: </span><span style="color: #800000;">"</span><span style="color: #800000;">{controller=Home}/{action=Index}/{id?}</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            });
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">配置Startup</span></div>
<p>②使应用内容可本地化</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('fb04a1ab-20a6-4536-af4e-3498f89ce0e2')"><img id="code_img_closed_fb04a1ab-20a6-4536-af4e-3498f89ce0e2" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_fb04a1ab-20a6-4536-af4e-3498f89ce0e2" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('fb04a1ab-20a6-4536-af4e-3498f89ce0e2',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_fb04a1ab-20a6-4536-af4e-3498f89ce0e2" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Diagnostics;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Mvc;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> MvcDemo.Models;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Localization;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.DependencyInjection;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Builder;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Globalization;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Localization;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> MvcDemo.Controllers
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> LocalizationController : Controller
    {

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span> IStringLocalizer&lt;LocalizationController&gt;<span style="color: #000000;"> _localization;

        </span><span style="color: #0000ff;">public</span> LocalizationController(IStringLocalizer&lt;LocalizationController&gt;<span style="color: #000000;"> localization)
        {
            _localization</span>=<span style="color: #000000;">localization;
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span><span style="color: #000000;"> Index()
        {
            </span><span style="color: #0000ff;">return</span> _localization[<span style="color: #800000;">"</span><span style="color: #800000;">Localization</span><span style="color: #800000;">"</span><span style="color: #000000;">];
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span><span style="color: #000000;"> Get()
        {
            </span><span style="color: #0000ff;">return</span> _localization[<span style="color: #800000;">"</span><span style="color: #800000;">Test{0}</span><span style="color: #800000;">"</span>,<span style="color: #800080;">1</span><span style="color: #000000;">];
        }

    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">LocalizationController</span></div>
<p>③视图本地化</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('251b6be2-5ba3-4dca-a13d-3c8db9011815')"><img id="code_img_closed_251b6be2-5ba3-4dca-a13d-3c8db9011815" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_251b6be2-5ba3-4dca-a13d-3c8db9011815" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('251b6be2-5ba3-4dca-a13d-3c8db9011815',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_251b6be2-5ba3-4dca-a13d-3c8db9011815" class="cnblogs_code_hide">
<pre><span style="color: #000000;">@using Microsoft.AspNetCore.Mvc.Localization
@inject IViewLocalizer Localizer
@{
    ViewData[</span><span style="color: #800000;">"</span><span style="color: #800000;">Title</span><span style="color: #800000;">"</span>] = <span style="color: #800000;">"</span><span style="color: #800000;">Home Page</span><span style="color: #800000;">"</span><span style="color: #000000;">;
}
</span>&lt;p&gt;@Localizer[<span style="color: #800000;">"</span><span style="color: #800000;">Localization</span><span style="color: #800000;">"</span>]&lt;/p&gt;
&lt;p&gt;@Localizer[<span style="color: #800000;">"</span><span style="color: #800000;">Test{0}</span><span style="color: #800000;">"</span>,<span style="color: #800080;">1</span>]&lt;/p&gt;</pre>
</div>
<span class="cnblogs_code_collapse">视图</span></div>
<p>④DataAnnotations本地化</p>
<p>⑤po文件</p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201805/741594-20180528184621050-524205249.png" alt="" width="113" height="94" /></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('55840cff-7b4a-4825-9bea-fd3211395e83')"><img id="code_img_closed_55840cff-7b4a-4825-9bea-fd3211395e83" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_55840cff-7b4a-4825-9bea-fd3211395e83" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('55840cff-7b4a-4825-9bea-fd3211395e83',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_55840cff-7b4a-4825-9bea-fd3211395e83" class="cnblogs_code_hide">
<pre>msgid <span style="color: #800000;">"</span><span style="color: #800000;">Localization</span><span style="color: #800000;">"</span><span style="color: #000000;">
msgstr </span><span style="color: #800000;">"</span><span style="color: #800000;">Localization</span><span style="color: #800000;">"</span><span style="color: #000000;">

msgid </span><span style="color: #800000;">"</span><span style="color: #800000;">Home</span><span style="color: #800000;">"</span><span style="color: #000000;">
msgstr </span><span style="color: #800000;">"</span><span style="color: #800000;">Home</span><span style="color: #800000;">"</span><span style="color: #000000;">

msgid </span><span style="color: #800000;">"</span><span style="color: #800000;">Test{0}</span><span style="color: #800000;">"</span><span style="color: #000000;">
msgstr </span><span style="color: #800000;">"</span><span style="color: #800000;">Test{0}</span><span style="color: #800000;">"</span></pre>
</div>
<span class="cnblogs_code_collapse">en.po</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('101d8b25-e643-44f5-aad8-a6737c4aad50')"><img id="code_img_closed_101d8b25-e643-44f5-aad8-a6737c4aad50" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_101d8b25-e643-44f5-aad8-a6737c4aad50" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('101d8b25-e643-44f5-aad8-a6737c4aad50',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_101d8b25-e643-44f5-aad8-a6737c4aad50" class="cnblogs_code_hide">
<pre>msgid <span style="color: #800000;">"</span><span style="color: #800000;">Localization</span><span style="color: #800000;">"</span><span style="color: #000000;">
msgstr </span><span style="color: #800000;">"</span><span style="color: #800000;">本地化</span><span style="color: #800000;">"</span><span style="color: #000000;">

msgid </span><span style="color: #800000;">"</span><span style="color: #800000;">Home</span><span style="color: #800000;">"</span><span style="color: #000000;">
msgstr </span><span style="color: #800000;">"</span><span style="color: #800000;">主页</span><span style="color: #800000;">"</span><span style="color: #000000;">

msgid </span><span style="color: #800000;">"</span><span style="color: #800000;">Test{0}</span><span style="color: #800000;">"</span><span style="color: #000000;">
msgstr </span><span style="color: #800000;">"</span><span style="color: #800000;">测试{0}</span><span style="color: #800000;">"</span></pre>
</div>
<span class="cnblogs_code_collapse">zh-CHS.po</span></div>
<p>msgid：键</p>
<p>msgstr：值</p>
<p>&nbsp;</p>
<p><strong>14，<span data-ttu-id="8cb73-117">在 ASP.NET 管道中运行 OWIN 中间件<a name="a114"></a></span></strong></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('fbba9d63-4e6e-4e2d-bce9-5efc4fea072c')"><img id="code_img_closed_fbba9d63-4e6e-4e2d-bce9-5efc4fea072c" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_fbba9d63-4e6e-4e2d-bce9-5efc4fea072c" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('fbba9d63-4e6e-4e2d-bce9-5efc4fea072c',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_fbba9d63-4e6e-4e2d-bce9-5efc4fea072c" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Builder;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Hosting;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Configuration;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.DependencyInjection;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Owin;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.IO;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Globalization;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> AspNetCoreOwin
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Startup
    {
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Startup(IConfiguration configuration)
        {
            Configuration </span>=<span style="color: #000000;"> configuration;
        }

        </span><span style="color: #0000ff;">public</span> IConfiguration Configuration { <span style="color: #0000ff;">get</span><span style="color: #000000;">; }

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> This method gets called by the runtime. Use this method to add services to the container.</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> ConfigureServices(IServiceCollection services)
        {
            services.AddMvc();
        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> This method gets called by the runtime. Use this method to configure the HTTP request pipeline.</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configure(IApplicationBuilder app, IHostingEnvironment env)
        {
            </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (env.IsDevelopment())
            {
                app.UseDeveloperExceptionPage();
            }
            </span><span style="color: #0000ff;">else</span><span style="color: #000000;">
            {
                app.UseExceptionHandler(</span><span style="color: #800000;">"</span><span style="color: #800000;">/Home/Error</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }

            app.UseOwin(pipeline</span>=&gt;<span style="color: #000000;">{
                pipeline(next</span>=&gt;<span style="color: #000000;">OwinHello);
            });

            app.UseStaticFiles();

            app.UseMvc(routes </span>=&gt;<span style="color: #000000;">
            {
                routes.MapRoute(
                    name: </span><span style="color: #800000;">"</span><span style="color: #800000;">default</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    template: </span><span style="color: #800000;">"</span><span style="color: #800000;">{controller=Home}/{action=Index}/{id?}</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            });
        }

        </span><span style="color: #0000ff;">public</span> Task OwinHello(IDictionary&lt;<span style="color: #0000ff;">string</span>,<span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;"> environment)
        {
            </span><span style="color: #0000ff;">string</span> responseText=<span style="color: #800000;">"</span><span style="color: #800000;">hello owin</span><span style="color: #800000;">"</span><span style="color: #000000;">;
            </span><span style="color: #0000ff;">byte</span>[] responseBytes=<span style="color: #000000;">Encoding.UTF8.GetBytes(responseText);
            </span><span style="color: #0000ff;">var</span> responseStream=(Stream)environment[<span style="color: #800000;">"</span><span style="color: #800000;">owin.ResponseBody</span><span style="color: #800000;">"</span><span style="color: #000000;">];
            </span><span style="color: #0000ff;">var</span> responseHeaders=(IDictionary&lt;<span style="color: #0000ff;">string</span>,<span style="color: #0000ff;">string</span>[]&gt;)environment[<span style="color: #800000;">"</span><span style="color: #800000;">owin.ResponseHeaders</span><span style="color: #800000;">"</span><span style="color: #000000;">];
            responseHeaders[</span><span style="color: #800000;">"</span><span style="color: #800000;">Content-Length</span><span style="color: #800000;">"</span>]=<span style="color: #0000ff;">new</span> <span style="color: #0000ff;">string</span><span style="color: #000000;">[]{responseBytes.Length.ToString(CultureInfo.InvariantCulture)};
            responseHeaders[</span><span style="color: #800000;">"</span><span style="color: #800000;">Content-Type</span><span style="color: #800000;">"</span>]=<span style="color: #0000ff;">new</span> <span style="color: #0000ff;">string</span>[] {<span style="color: #800000;">"</span><span style="color: #800000;">text/plain</span><span style="color: #800000;">"</span><span style="color: #000000;">};
            </span><span style="color: #0000ff;">return</span> responseStream.WriteAsync(responseBytes,<span style="color: #800080;">0</span><span style="color: #000000;">,responseBytes.Length);
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Startup</span></div>
<p>案例下载：<a href="https://pan.baidu.com/s/1FLfBuqsMuKnv7wSF3BSW4w%20" target="_blank">https://pan.baidu.com/s/1FLfBuqsMuKnv7wSF3BSW4w&nbsp;</a></p>
<p>&nbsp;</p>
<p><strong>15，WebSockets<a name="a115"></a></strong></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('59e78eae-7a93-4ced-9b06-9c17832e38c9')"><img id="code_img_closed_59e78eae-7a93-4ced-9b06-9c17832e38c9" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_59e78eae-7a93-4ced-9b06-9c17832e38c9" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('59e78eae-7a93-4ced-9b06-9c17832e38c9',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_59e78eae-7a93-4ced-9b06-9c17832e38c9" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Builder;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Hosting;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Configuration;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.DependencyInjection;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.WebSockets;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Net.WebSockets;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Http;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Concurrent;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> WebSocketsDemo
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Startup
    {
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Startup(IConfiguration configuration)
        {
            Configuration </span>=<span style="color: #000000;"> configuration;
        }

        </span><span style="color: #0000ff;">public</span> IConfiguration Configuration { <span style="color: #0000ff;">get</span><span style="color: #000000;">; }

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> This method gets called by the runtime. Use this method to add services to the container.</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> ConfigureServices(IServiceCollection services)
        {
            services.AddMvc();
        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> This method gets called by the runtime. Use this method to configure the HTTP request pipeline.</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configure(IApplicationBuilder app, IHostingEnvironment env)
        {
            </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (env.IsDevelopment())
            {
                app.UseDeveloperExceptionPage();
            }
            </span><span style="color: #0000ff;">else</span><span style="color: #000000;">
            {
                app.UseExceptionHandler(</span><span style="color: #800000;">"</span><span style="color: #800000;">/Home/Error</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }

            app.UseDefaultFiles();
            app.UseStaticFiles();

            </span><span style="color: #0000ff;">var</span> webSocketOption=<span style="color: #0000ff;">new</span><span style="color: #000000;"> WebSocketOptions()
            {
                KeepAliveInterval</span>=TimeSpan.FromSeconds(<span style="color: #800080;">120</span>),<span style="color: #008000;">//</span><span style="color: #008000;">向客户端发送&ldquo;ping&rdquo;帧的频率，以确保代理保持连接处于打开状态</span>
                ReceiveBufferSize=<span style="color: #800080;">4</span>*<span style="color: #800080;">1024</span><span style="color: #008000;">//</span><span style="color: #008000;">用于接收数据的缓冲区的大小</span>
<span style="color: #000000;">            };
            app.UseWebSockets(webSocketOption);

            app.UseMvc(routes </span>=&gt;<span style="color: #000000;">
            {
                routes.MapRoute(
                    name: </span><span style="color: #800000;">"</span><span style="color: #800000;">default</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    template: </span><span style="color: #800000;">"</span><span style="color: #800000;">{controller=Home}/{action=Index}/{id?}</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            });

            app.Use(</span><span style="color: #0000ff;">async</span> (context,next)=&gt;<span style="color: #000000;">{
                </span><span style="color: #0000ff;">if</span>(context.Request.Path==<span style="color: #800000;">"</span><span style="color: #800000;">/ws</span><span style="color: #800000;">"</span><span style="color: #000000;">)
                {
                    </span><span style="color: #0000ff;">if</span>(context.WebSockets.IsWebSocketRequest)<span style="color: #008000;">//</span><span style="color: #008000;">判断是否是websocket请求</span>
<span style="color: #000000;">                    {
                        </span><span style="color: #008000;">//</span><span style="color: #008000;">将TCP连接升级到WebSocket连接，并提供websocket对象</span>
                        WebSocket webSocket=<span style="color: #0000ff;">await</span><span style="color: #000000;"> context.WebSockets.AcceptWebSocketAsync();
                        WebSockets.TryAdd(webSocket,</span><span style="color: #800000;">"</span><span style="color: #800000;">1</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                        </span><span style="color: #0000ff;">await</span><span style="color: #000000;"> Echo(context,webSocket);
                    }
                    </span><span style="color: #0000ff;">else</span><span style="color: #000000;">
                    {
                        context.Response.StatusCode</span>=<span style="color: #800080;">400</span><span style="color: #000000;">;
                    }
                }
                </span><span style="color: #0000ff;">else</span><span style="color: #000000;">
                {
                    </span><span style="color: #0000ff;">await</span><span style="color: #000000;"> next();
                }
            });
        }

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">async</span><span style="color: #000000;"> Task Echo(HttpContext context,WebSocket websocket)
        {
            </span><span style="color: #0000ff;">var</span> buffer=<span style="color: #0000ff;">new</span> <span style="color: #0000ff;">byte</span>[<span style="color: #800080;">4</span>*<span style="color: #800080;">1024</span><span style="color: #000000;">];
            WebSocketReceiveResult result</span>=<span style="color: #0000ff;">await</span> websocket.ReceiveAsync(<span style="color: #0000ff;">new</span> ArraySegment&lt;<span style="color: #0000ff;">byte</span>&gt;<span style="color: #000000;">(buffer),CancellationToken.None);
            </span><span style="color: #0000ff;">while</span>(!<span style="color: #000000;">result.CloseStatus.HasValue)
            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;">广播</span>
                <span style="color: #0000ff;">foreach</span>(<span style="color: #0000ff;">var</span> ws <span style="color: #0000ff;">in</span><span style="color: #000000;"> WebSockets)
                {
                    </span><span style="color: #0000ff;">if</span>(!<span style="color: #000000;">ws.Key.CloseStatus.HasValue)
                    {
                       </span><span style="color: #0000ff;">await</span> ws.Key.SendAsync(<span style="color: #0000ff;">new</span> ArraySegment&lt;<span style="color: #0000ff;">byte</span>&gt;(buffer,<span style="color: #800080;">0</span><span style="color: #000000;">,buffer.Length),result.MessageType,result.EndOfMessage,CancellationToken.None);
                    }
                    </span><span style="color: #0000ff;">else</span><span style="color: #000000;">
                    {
                        </span><span style="color: #0000ff;">string</span><span style="color: #000000;"> value;
                        WebSockets.TryRemove(ws.Key,</span><span style="color: #0000ff;">out</span><span style="color: #000000;"> value);
                    }
                    </span><span style="color: #008000;">//</span><span style="color: #008000;">await ws.SendAsync(new ArraySegment&lt;byte&gt;(buffer,0,buffer.Length),result.MessageType,result.EndOfMessage,CancellationToken.None);</span>
<span style="color: #000000;">                }
                
                result</span>=<span style="color: #0000ff;">await</span> websocket.ReceiveAsync(<span style="color: #0000ff;">new</span> ArraySegment&lt;<span style="color: #0000ff;">byte</span>&gt;<span style="color: #000000;">(buffer),CancellationToken.None);
            }
            </span><span style="color: #0000ff;">await</span><span style="color: #000000;"> websocket.CloseAsync(result.CloseStatus.Value,result.CloseStatusDescription,CancellationToken.None);
        }
        </span><span style="color: #008000;">//</span><span style="color: #008000;">可以开一个线程去检测WebSocket是否掉线，掉线则从字典中删除</span>
        <span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> ConcurrentDictionary&lt;WebSocket,<span style="color: #0000ff;">string</span>&gt; WebSockets=<span style="color: #0000ff;">new</span> ConcurrentDictionary&lt;WebSocket,<span style="color: #0000ff;">string</span>&gt;<span style="color: #000000;">();
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Startup</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('62d8e36b-3bf1-411d-ac9e-e7ed6a7ca0d8')"><img id="code_img_closed_62d8e36b-3bf1-411d-ac9e-e7ed6a7ca0d8" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_62d8e36b-3bf1-411d-ac9e-e7ed6a7ca0d8" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('62d8e36b-3bf1-411d-ac9e-e7ed6a7ca0d8',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_62d8e36b-3bf1-411d-ac9e-e7ed6a7ca0d8" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">&lt;!</span><span style="color: #ff00ff;">doctype html</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">html </span><span style="color: #ff0000;">lang</span><span style="color: #0000ff;">="en"</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">head</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">title</span><span style="color: #0000ff;">&gt;</span>Title<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">title</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> Required meta tags </span><span style="color: #008000;">--&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">meta </span><span style="color: #ff0000;">charset</span><span style="color: #0000ff;">="utf-8"</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">meta </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="viewport"</span><span style="color: #ff0000;"> content</span><span style="color: #0000ff;">="width=device-width, initial-scale=1, shrink-to-fit=no"</span><span style="color: #0000ff;">&gt;</span>

    <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> Bootstrap CSS </span><span style="color: #008000;">--&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">link </span><span style="color: #ff0000;">rel</span><span style="color: #0000ff;">="stylesheet"</span><span style="color: #ff0000;"> href</span><span style="color: #0000ff;">="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css"</span><span style="color: #ff0000;"> integrity</span><span style="color: #0000ff;">="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm"</span><span style="color: #ff0000;"> crossorigin</span><span style="color: #0000ff;">="anonymous"</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="lib/jquery/dist/jquery.min.js"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">head</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">body</span><span style="color: #0000ff;">&gt;</span>
    
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="text"</span><span style="color: #ff0000;"> id</span><span style="color: #0000ff;">="message"</span><span style="color: #0000ff;">/&gt;&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="button"</span><span style="color: #ff0000;"> id</span><span style="color: #0000ff;">="send"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">="发送"</span><span style="color: #0000ff;">/&gt;</span>

    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">id</span><span style="color: #0000ff;">="context"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>

    <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> Optional JavaScript </span><span style="color: #008000;">--&gt;</span>
    <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> jQuery first, then Popper.js, then Bootstrap JS </span><span style="color: #008000;">--&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="https://code.jquery.com/jquery-3.2.1.slim.min.js"</span><span style="color: #ff0000;"> integrity</span><span style="color: #0000ff;">="sha384-KJ3o2DKtIkvYIK3UENzmM7KCkRr/rE9/Qpg6aAZGJwFDMVNA/GpGFF93hXpG5KkN"</span><span style="color: #ff0000;"> crossorigin</span><span style="color: #0000ff;">="anonymous"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.12.9/umd/popper.min.js"</span><span style="color: #ff0000;"> integrity</span><span style="color: #0000ff;">="sha384-ApNbgh9B+Y1QKtv3Rn7W3mgPxhU9K/ScQsAP7hUibX39j7fakFPskvXusvfa0b4Q"</span><span style="color: #ff0000;"> crossorigin</span><span style="color: #0000ff;">="anonymous"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/js/bootstrap.min.js"</span><span style="color: #ff0000;"> integrity</span><span style="color: #0000ff;">="sha384-JZR6Spejh4U02d8jOt6vLEHfe/JQGiRRSQQxSfFWpi1MquVdAyjUar5+76PVCmYl"</span><span style="color: #ff0000;"> crossorigin</span><span style="color: #0000ff;">="anonymous"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">body</span><span style="color: #0000ff;">&gt;</span>

  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>

      <span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> ws;
      </span><span style="background-color: #f5f5f5; color: #0000ff;">if</span><span style="background-color: #f5f5f5; color: #000000;">(</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">WebSocket</span><span style="background-color: #f5f5f5; color: #000000;">"</span> <span style="background-color: #f5f5f5; color: #0000ff;">in</span><span style="background-color: #f5f5f5; color: #000000;"> window)
      {
         ws</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #0000ff;">new</span><span style="background-color: #f5f5f5; color: #000000;"> WebSocket(</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">ws://localhost:5000/ws</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">);
         ws.onopen</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;">(){
          alert(</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">开始</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">)
         }
         ws.onmessage</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;">(res){
           $(</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">#context</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">).append(res.data</span><span style="background-color: #f5f5f5; color: #000000;">+</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">&lt;br/&gt;</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">)
         }
         ws.onclose</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;">(){
           alert(</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">退出</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">)
         }
      }
      </span><span style="background-color: #f5f5f5; color: #0000ff;">else</span><span style="background-color: #f5f5f5; color: #000000;">
      {
          alert(</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">不支持websocket</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">);
      }

   $(</span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;">(){

          $(</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">#send</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">).click(</span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;">(){
            ws.send($(</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">#message</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">).val())
          })
   })

  </span><span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">html</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<span class="cnblogs_code_collapse">index.html</span></div>
<p>案例下载：<a href="https://pan.baidu.com/s/1C5CLrtD6Mr66oiM7sfEHaw" target="_blank">https://pan.baidu.com/s/1C5CLrtD6Mr66oiM7sfEHaw</a></p>
<p>&nbsp;</p>
<p><strong><a name="a116"></a>16，使用内存缓存</strong></p>
<p>nuget&nbsp;<span class="cnblogs_code">Microsoft.Extensions.Caching.Memory</span>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('2967ec2b-8331-4c4d-8aa3-7d310eeeec61')"><img id="code_img_closed_2967ec2b-8331-4c4d-8aa3-7d310eeeec61" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_2967ec2b-8331-4c4d-8aa3-7d310eeeec61" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('2967ec2b-8331-4c4d-8aa3-7d310eeeec61',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_2967ec2b-8331-4c4d-8aa3-7d310eeeec61" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Builder;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Hosting;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Http;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.HttpsPolicy;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Mvc;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Configuration;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.DependencyInjection;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Caching;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> CacheDemo
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Startup
    {
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Startup(IConfiguration configuration)
        {
            Configuration </span>=<span style="color: #000000;"> configuration;
        }

        </span><span style="color: #0000ff;">public</span> IConfiguration Configuration { <span style="color: #0000ff;">get</span><span style="color: #000000;">; }

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> This method gets called by the runtime. Use this method to add services to the container.</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> ConfigureServices(IServiceCollection services)
        {
            services.Configure</span>&lt;CookiePolicyOptions&gt;(options =&gt;<span style="color: #000000;">
            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;"> This lambda determines whether user consent for non-essential cookies is needed for a given request.</span>
                options.CheckConsentNeeded = context =&gt; <span style="color: #0000ff;">true</span><span style="color: #000000;">;
                options.MinimumSameSitePolicy </span>=<span style="color: #000000;"> SameSiteMode.None;
            });

            services.AddMemoryCache();
            services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_1);
        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> This method gets called by the runtime. Use this method to configure the HTTP request pipeline.</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configure(IApplicationBuilder app, IHostingEnvironment env)
        {
            </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (env.IsDevelopment())
            {
                app.UseDeveloperExceptionPage();
            }
            </span><span style="color: #0000ff;">else</span><span style="color: #000000;">
            {
                app.UseExceptionHandler(</span><span style="color: #800000;">"</span><span style="color: #800000;">/Home/Error</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                app.UseHsts();
            }

            app.UseHttpsRedirection();
            app.UseStaticFiles();
            app.UseCookiePolicy();

            app.UseMvc(routes </span>=&gt;<span style="color: #000000;">
            {
                routes.MapRoute(
                    name: </span><span style="color: #800000;">"</span><span style="color: #800000;">default</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    template: </span><span style="color: #800000;">"</span><span style="color: #800000;">{controller=Home}/{action=Index}/{id?}</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            });
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Startup</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('27041bad-e4d8-4859-a0fb-a2e4785cf0a6')"><img id="code_img_closed_27041bad-e4d8-4859-a0fb-a2e4785cf0a6" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_27041bad-e4d8-4859-a0fb-a2e4785cf0a6" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('27041bad-e4d8-4859-a0fb-a2e4785cf0a6',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_27041bad-e4d8-4859-a0fb-a2e4785cf0a6" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Diagnostics;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Mvc;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> CacheDemo.Models;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Caching.Memory;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> CacheDemo.Controllers
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> HomeController : Controller
    {

        </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> IMemoryCache _cache;

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> HomeController(IMemoryCache cache)
        {
            _cache</span>=<span style="color: #000000;">cache;
        }

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> IActionResult Index()
        {
            DateTime date;
            </span><span style="color: #0000ff;">if</span>(_cache.TryGetValue(<span style="color: #800000;">"</span><span style="color: #800000;">date</span><span style="color: #800000;">"</span>,<span style="color: #0000ff;">out</span><span style="color: #000000;"> date))
            {
                ViewData[</span><span style="color: #800000;">"</span><span style="color: #800000;">date</span><span style="color: #800000;">"</span>]=<span style="color: #000000;">date;
            }
            </span><span style="color: #0000ff;">else</span><span style="color: #000000;">
            {
                ViewData[</span><span style="color: #800000;">"</span><span style="color: #800000;">date</span><span style="color: #800000;">"</span>]=<span style="color: #800000;">"</span><span style="color: #800000;">未设置缓存</span><span style="color: #800000;">"</span><span style="color: #000000;">;
            }
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> View();
        }


        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> IActionResult Set()
        {
            _cache.Set</span>&lt;DateTime&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">date</span><span style="color: #800000;">"</span><span style="color: #000000;">,DateTime.Now);
            </span><span style="color: #0000ff;">return</span> RedirectToAction(<span style="color: #800000;">"</span><span style="color: #800000;">Index</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }

        
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">HomeController</span></div>
<p>案例下载：<a href="https://pan.baidu.com/s/1DEpF-_HLlEQFWswPyb-WkA" target="_blank">https://pan.baidu.com/s/1DEpF-_HLlEQFWswPyb-WkA</a></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a2"></a>二、EF</span></strong></span></p>
<p><strong>1，Include和ThenInclude<a name="a21"></a></strong></p>
<p>使上下文加载&nbsp;<code>Student.Enrollments</code>&nbsp;导航属性，并在每个注册中加载&nbsp;<code>Enrollment.Course</code>&nbsp;导航属性</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('ce99cf33-5f6d-4ed4-ba03-600a664d4679')"><img id="code_img_closed_ce99cf33-5f6d-4ed4-ba03-600a664d4679" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_ce99cf33-5f6d-4ed4-ba03-600a664d4679" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('ce99cf33-5f6d-4ed4-ba03-600a664d4679',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_ce99cf33-5f6d-4ed4-ba03-600a664d4679" class="cnblogs_code_hide">
<pre>    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Student
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span> ID { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> LastName { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> FirstMidName { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
        </span><span style="color: #0000ff;">public</span> DateTime EnrollmentDate { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

        </span><span style="color: #0000ff;">public</span> ICollection&lt;Enrollment&gt; Enrollments { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Enrollment
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span> EnrollmentID { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span> CourseID { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span> StudentID { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
        </span><span style="color: #0000ff;">public</span> Grade? Grade { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

        </span><span style="color: #0000ff;">public</span> Course Course { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
        </span><span style="color: #0000ff;">public</span> Student Student { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Course
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;">主键</span>
<span style="color: #000000;">        [DatabaseGenerated(DatabaseGeneratedOption.None)]
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span> CourseID { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Title { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span> Credits { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

        </span><span style="color: #0000ff;">public</span> ICollection&lt;Enrollment&gt; Enrollments { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    }</span></pre>
</div>
<span class="cnblogs_code_collapse">实体</span></div>
<p><strong>2，<span data-ttu-id="8be7c-222">通过依赖关系注入注册上下文<a name="a22"></a></span></strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> ConfigureServices(IServiceCollection services)
{
    services.AddDbContext</span>&lt;SchoolContext&gt;(options =&gt;<span style="color: #000000;">
      options.UseSqlServer(Configuration.GetConnectionString(</span><span style="color: #800000;">"</span><span style="color: #800000;">DefaultConnection</span><span style="color: #800000;">"</span><span style="color: #000000;">)));

    services.AddMvc();
}</span></pre>
</div>
<p>配置连接字符串</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('ec2ee468-19fc-4a46-9509-ac9a92cecb03')"><img id="code_img_closed_ec2ee468-19fc-4a46-9509-ac9a92cecb03" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_ec2ee468-19fc-4a46-9509-ac9a92cecb03" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('ec2ee468-19fc-4a46-9509-ac9a92cecb03',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_ec2ee468-19fc-4a46-9509-ac9a92cecb03" class="cnblogs_code_hide">
<pre><span style="color: #000000;">{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">ConnectionStrings</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">DefaultConnection</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">Server=(localdb)\\mssqllocaldb;Database=ContosoUniversity1;ConnectRetryCount=0;Trusted_Connection=True;MultipleActiveResultSets=true</span><span style="color: #800000;">"</span><span style="color: #000000;">
  },
  </span><span style="color: #800000;">"</span><span style="color: #800000;">Logging</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">IncludeScopes</span><span style="color: #800000;">"</span>: <span style="color: #0000ff;">false</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">LogLevel</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">Default</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">Warning</span><span style="color: #800000;">"</span><span style="color: #000000;">
    }
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">appsettings.json</span></div>
<p><span style="color: #ff6600;"><code>ConnectRetryCount=0</code>&nbsp;来防止&nbsp;<a href="https://docs.microsoft.com/dotnet/framework/data/adonet/ef/sqlclient-for-the-entity-framework" data-linktype="external"><span style="color: #ff6600;">SQLClient</span></a>&nbsp;挂起&nbsp;</span></p>
<p><strong>3，种子数据<a name="a23"></a></strong></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('afa533cf-5410-4d09-8ba7-95444244712c')"><img id="code_img_closed_afa533cf-5410-4d09-8ba7-95444244712c" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_afa533cf-5410-4d09-8ba7-95444244712c" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('afa533cf-5410-4d09-8ba7-95444244712c',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_afa533cf-5410-4d09-8ba7-95444244712c" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> ContosoUniversity.Models;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ContosoUniversity.Data
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> DbInitializer
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Initialize(SchoolContext context)
        {
            context.Database.EnsureCreated();

            </span><span style="color: #008000;">//</span><span style="color: #008000;"> Look for any students.</span>
            <span style="color: #0000ff;">if</span><span style="color: #000000;"> (context.Students.Any())
            {
                </span><span style="color: #0000ff;">return</span>;   <span style="color: #008000;">//</span><span style="color: #008000;"> DB has been seeded</span>
<span style="color: #000000;">            }

            </span><span style="color: #0000ff;">var</span> students = <span style="color: #0000ff;">new</span><span style="color: #000000;"> Student[]
            {
            </span><span style="color: #0000ff;">new</span> Student{FirstMidName=<span style="color: #800000;">"</span><span style="color: #800000;">Carson</span><span style="color: #800000;">"</span>,LastName=<span style="color: #800000;">"</span><span style="color: #800000;">Alexander</span><span style="color: #800000;">"</span>,EnrollmentDate=DateTime.Parse(<span style="color: #800000;">"</span><span style="color: #800000;">2005-09-01</span><span style="color: #800000;">"</span><span style="color: #000000;">)},
            </span><span style="color: #0000ff;">new</span> Student{FirstMidName=<span style="color: #800000;">"</span><span style="color: #800000;">Meredith</span><span style="color: #800000;">"</span>,LastName=<span style="color: #800000;">"</span><span style="color: #800000;">Alonso</span><span style="color: #800000;">"</span>,EnrollmentDate=DateTime.Parse(<span style="color: #800000;">"</span><span style="color: #800000;">2002-09-01</span><span style="color: #800000;">"</span><span style="color: #000000;">)},
            </span><span style="color: #0000ff;">new</span> Student{FirstMidName=<span style="color: #800000;">"</span><span style="color: #800000;">Arturo</span><span style="color: #800000;">"</span>,LastName=<span style="color: #800000;">"</span><span style="color: #800000;">Anand</span><span style="color: #800000;">"</span>,EnrollmentDate=DateTime.Parse(<span style="color: #800000;">"</span><span style="color: #800000;">2003-09-01</span><span style="color: #800000;">"</span><span style="color: #000000;">)},
            </span><span style="color: #0000ff;">new</span> Student{FirstMidName=<span style="color: #800000;">"</span><span style="color: #800000;">Gytis</span><span style="color: #800000;">"</span>,LastName=<span style="color: #800000;">"</span><span style="color: #800000;">Barzdukas</span><span style="color: #800000;">"</span>,EnrollmentDate=DateTime.Parse(<span style="color: #800000;">"</span><span style="color: #800000;">2002-09-01</span><span style="color: #800000;">"</span><span style="color: #000000;">)},
            </span><span style="color: #0000ff;">new</span> Student{FirstMidName=<span style="color: #800000;">"</span><span style="color: #800000;">Yan</span><span style="color: #800000;">"</span>,LastName=<span style="color: #800000;">"</span><span style="color: #800000;">Li</span><span style="color: #800000;">"</span>,EnrollmentDate=DateTime.Parse(<span style="color: #800000;">"</span><span style="color: #800000;">2002-09-01</span><span style="color: #800000;">"</span><span style="color: #000000;">)},
            </span><span style="color: #0000ff;">new</span> Student{FirstMidName=<span style="color: #800000;">"</span><span style="color: #800000;">Peggy</span><span style="color: #800000;">"</span>,LastName=<span style="color: #800000;">"</span><span style="color: #800000;">Justice</span><span style="color: #800000;">"</span>,EnrollmentDate=DateTime.Parse(<span style="color: #800000;">"</span><span style="color: #800000;">2001-09-01</span><span style="color: #800000;">"</span><span style="color: #000000;">)},
            </span><span style="color: #0000ff;">new</span> Student{FirstMidName=<span style="color: #800000;">"</span><span style="color: #800000;">Laura</span><span style="color: #800000;">"</span>,LastName=<span style="color: #800000;">"</span><span style="color: #800000;">Norman</span><span style="color: #800000;">"</span>,EnrollmentDate=DateTime.Parse(<span style="color: #800000;">"</span><span style="color: #800000;">2003-09-01</span><span style="color: #800000;">"</span><span style="color: #000000;">)},
            </span><span style="color: #0000ff;">new</span> Student{FirstMidName=<span style="color: #800000;">"</span><span style="color: #800000;">Nino</span><span style="color: #800000;">"</span>,LastName=<span style="color: #800000;">"</span><span style="color: #800000;">Olivetto</span><span style="color: #800000;">"</span>,EnrollmentDate=DateTime.Parse(<span style="color: #800000;">"</span><span style="color: #800000;">2005-09-01</span><span style="color: #800000;">"</span><span style="color: #000000;">)}
            };
            </span><span style="color: #0000ff;">foreach</span> (Student s <span style="color: #0000ff;">in</span><span style="color: #000000;"> students)
            {
                context.Students.Add(s);
            }
            context.SaveChanges();

            </span><span style="color: #0000ff;">var</span> courses = <span style="color: #0000ff;">new</span><span style="color: #000000;"> Course[]
            {
            </span><span style="color: #0000ff;">new</span> Course{CourseID=<span style="color: #800080;">1050</span>,Title=<span style="color: #800000;">"</span><span style="color: #800000;">Chemistry</span><span style="color: #800000;">"</span>,Credits=<span style="color: #800080;">3</span><span style="color: #000000;">},
            </span><span style="color: #0000ff;">new</span> Course{CourseID=<span style="color: #800080;">4022</span>,Title=<span style="color: #800000;">"</span><span style="color: #800000;">Microeconomics</span><span style="color: #800000;">"</span>,Credits=<span style="color: #800080;">3</span><span style="color: #000000;">},
            </span><span style="color: #0000ff;">new</span> Course{CourseID=<span style="color: #800080;">4041</span>,Title=<span style="color: #800000;">"</span><span style="color: #800000;">Macroeconomics</span><span style="color: #800000;">"</span>,Credits=<span style="color: #800080;">3</span><span style="color: #000000;">},
            </span><span style="color: #0000ff;">new</span> Course{CourseID=<span style="color: #800080;">1045</span>,Title=<span style="color: #800000;">"</span><span style="color: #800000;">Calculus</span><span style="color: #800000;">"</span>,Credits=<span style="color: #800080;">4</span><span style="color: #000000;">},
            </span><span style="color: #0000ff;">new</span> Course{CourseID=<span style="color: #800080;">3141</span>,Title=<span style="color: #800000;">"</span><span style="color: #800000;">Trigonometry</span><span style="color: #800000;">"</span>,Credits=<span style="color: #800080;">4</span><span style="color: #000000;">},
            </span><span style="color: #0000ff;">new</span> Course{CourseID=<span style="color: #800080;">2021</span>,Title=<span style="color: #800000;">"</span><span style="color: #800000;">Composition</span><span style="color: #800000;">"</span>,Credits=<span style="color: #800080;">3</span><span style="color: #000000;">},
            </span><span style="color: #0000ff;">new</span> Course{CourseID=<span style="color: #800080;">2042</span>,Title=<span style="color: #800000;">"</span><span style="color: #800000;">Literature</span><span style="color: #800000;">"</span>,Credits=<span style="color: #800080;">4</span><span style="color: #000000;">}
            };
            </span><span style="color: #0000ff;">foreach</span> (Course c <span style="color: #0000ff;">in</span><span style="color: #000000;"> courses)
            {
                context.Courses.Add(c);
            }
            context.SaveChanges();

            </span><span style="color: #0000ff;">var</span> enrollments = <span style="color: #0000ff;">new</span><span style="color: #000000;"> Enrollment[]
            {
            </span><span style="color: #0000ff;">new</span> Enrollment{StudentID=<span style="color: #800080;">1</span>,CourseID=<span style="color: #800080;">1050</span>,Grade=<span style="color: #000000;">Grade.A},
            </span><span style="color: #0000ff;">new</span> Enrollment{StudentID=<span style="color: #800080;">1</span>,CourseID=<span style="color: #800080;">4022</span>,Grade=<span style="color: #000000;">Grade.C},
            </span><span style="color: #0000ff;">new</span> Enrollment{StudentID=<span style="color: #800080;">1</span>,CourseID=<span style="color: #800080;">4041</span>,Grade=<span style="color: #000000;">Grade.B},
            </span><span style="color: #0000ff;">new</span> Enrollment{StudentID=<span style="color: #800080;">2</span>,CourseID=<span style="color: #800080;">1045</span>,Grade=<span style="color: #000000;">Grade.B},
            </span><span style="color: #0000ff;">new</span> Enrollment{StudentID=<span style="color: #800080;">2</span>,CourseID=<span style="color: #800080;">3141</span>,Grade=<span style="color: #000000;">Grade.F},
            </span><span style="color: #0000ff;">new</span> Enrollment{StudentID=<span style="color: #800080;">2</span>,CourseID=<span style="color: #800080;">2021</span>,Grade=<span style="color: #000000;">Grade.F},
            </span><span style="color: #0000ff;">new</span> Enrollment{StudentID=<span style="color: #800080;">3</span>,CourseID=<span style="color: #800080;">1050</span><span style="color: #000000;">},
            </span><span style="color: #0000ff;">new</span> Enrollment{StudentID=<span style="color: #800080;">4</span>,CourseID=<span style="color: #800080;">1050</span><span style="color: #000000;">},
            </span><span style="color: #0000ff;">new</span> Enrollment{StudentID=<span style="color: #800080;">4</span>,CourseID=<span style="color: #800080;">4022</span>,Grade=<span style="color: #000000;">Grade.F},
            </span><span style="color: #0000ff;">new</span> Enrollment{StudentID=<span style="color: #800080;">5</span>,CourseID=<span style="color: #800080;">4041</span>,Grade=<span style="color: #000000;">Grade.C},
            </span><span style="color: #0000ff;">new</span> Enrollment{StudentID=<span style="color: #800080;">6</span>,CourseID=<span style="color: #800080;">1045</span><span style="color: #000000;">},
            </span><span style="color: #0000ff;">new</span> Enrollment{StudentID=<span style="color: #800080;">7</span>,CourseID=<span style="color: #800080;">3141</span>,Grade=<span style="color: #000000;">Grade.A},
            };
            </span><span style="color: #0000ff;">foreach</span> (Enrollment e <span style="color: #0000ff;">in</span><span style="color: #000000;"> enrollments)
            {
                context.Enrollments.Add(e);
            }
            context.SaveChanges();
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">DbInitializer</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('79d1d318-9155-4461-992a-95ea8e31a9de')"><img id="code_img_closed_79d1d318-9155-4461-992a-95ea8e31a9de" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_79d1d318-9155-4461-992a-95ea8e31a9de" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('79d1d318-9155-4461-992a-95ea8e31a9de',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_79d1d318-9155-4461-992a-95ea8e31a9de" class="cnblogs_code_hide">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> Unused usings removed</span>
<span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Hosting;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Logging;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.DependencyInjection;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> ContosoUniversity.Data;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ContosoUniversity
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #0000ff;">var</span> host =<span style="color: #000000;"> BuildWebHost(args);

            </span><span style="color: #0000ff;">using</span> (<span style="color: #0000ff;">var</span> scope =<span style="color: #000000;"> host.Services.CreateScope())
            {
                </span><span style="color: #0000ff;">var</span> services =<span style="color: #000000;"> scope.ServiceProvider;
                </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
                {
                    </span><span style="color: #0000ff;">var</span> context = services.GetRequiredService&lt;SchoolContext&gt;<span style="color: #000000;">();
                    DbInitializer.Initialize(context);
                }
                </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (Exception ex)
                {
                    </span><span style="color: #0000ff;">var</span> logger = services.GetRequiredService&lt;ILogger&lt;Program&gt;&gt;<span style="color: #000000;">();
                    logger.LogError(ex, </span><span style="color: #800000;">"</span><span style="color: #800000;">An error occurred while seeding the database.</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                }
            }

            host.Run();
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> IWebHost BuildWebHost(<span style="color: #0000ff;">string</span>[] args) =&gt;<span style="color: #000000;">
            WebHost.CreateDefaultBuilder(args)
                .UseStartup</span>&lt;Startup&gt;<span style="color: #000000;">()
                .Build();
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Program.cs</span></div>
<p><span data-ttu-id="8be7c-253">第一次运行该应用时，会使用测试数据创建并填充数据库。&nbsp;<span data-ttu-id="8be7c-254">更新数据模型时：</span></span></p>
<ul>
<li><span data-ttu-id="8be7c-255">删除数据库。</span></li>
<li><span data-ttu-id="8be7c-256">更新 seed 方法。</span></li>
<li><span data-ttu-id="8be7c-257">运行该应用，并创建新的种子数据库。</span></li>
</ul>
<p><br /><strong>4，级联删除&nbsp;<a name="a24"></a></strong></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('c44ffb91-9f98-4057-bbb6-f14b438a32d1')"><img id="code_img_closed_c44ffb91-9f98-4057-bbb6-f14b438a32d1" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_c44ffb91-9f98-4057-bbb6-f14b438a32d1" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('c44ffb91-9f98-4057-bbb6-f14b438a32d1',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_c44ffb91-9f98-4057-bbb6-f14b438a32d1" class="cnblogs_code_hide">
<pre>modelBuilder.Entity&lt;Department&gt;<span style="color: #000000;">()
   .HasOne(d </span>=&gt;<span style="color: #000000;"> d.Administrator)
   .WithMany()
   .OnDelete(DeleteBehavior.Restrict)</span></pre>
</div>
<span class="cnblogs_code_collapse">Code</span></div>
<p>&nbsp;</p>
<p><strong>5，组合PK<a name="a25"></a></strong></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('bedaf6fd-9c51-46f4-a4ba-321135a9926b')"><img id="code_img_closed_bedaf6fd-9c51-46f4-a4ba-321135a9926b" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_bedaf6fd-9c51-46f4-a4ba-321135a9926b" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('bedaf6fd-9c51-46f4-a4ba-321135a9926b',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_bedaf6fd-9c51-46f4-a4ba-321135a9926b" class="cnblogs_code_hide">
<pre>    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> CourseAssignment
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span> InstructorID { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span> CourseID { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
        </span><span style="color: #0000ff;">public</span> Instructor Instructor { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
        </span><span style="color: #0000ff;">public</span> Course Course { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    }</span></pre>
</div>
<span class="cnblogs_code_collapse">Model</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('9ed5fa2b-dfeb-4a50-a244-611efc413488')"><img id="code_img_closed_9ed5fa2b-dfeb-4a50-a244-611efc413488" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_9ed5fa2b-dfeb-4a50-a244-611efc413488" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('9ed5fa2b-dfeb-4a50-a244-611efc413488',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_9ed5fa2b-dfeb-4a50-a244-611efc413488" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> OnModelCreating(ModelBuilder modelBuilder)
        {
modelBuilder.Entity</span>&lt;CourseAssignment&gt;<span style="color: #000000;">()
                .HasKey(c </span>=&gt; <span style="color: #0000ff;">new</span><span style="color: #000000;"> { c.CourseID, c.InstructorID });
 }</span></pre>
</div>
<span class="cnblogs_code_collapse">SchoolContext</span></div>
<p>&nbsp;</p>
<p><strong>&nbsp;6，使用原始sql<a name="a26"></a></strong></p>
<p>①<span data-ttu-id="4e9d1-123">调用返回实体的查询</span></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('fe90280d-726a-47ca-8262-71677faca77e')"><img id="code_img_closed_fe90280d-726a-47ca-8262-71677faca77e" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_fe90280d-726a-47ca-8262-71677faca77e" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('fe90280d-726a-47ca-8262-71677faca77e',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_fe90280d-726a-47ca-8262-71677faca77e" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task&lt;IActionResult&gt; Details(<span style="color: #0000ff;">int</span>?<span style="color: #000000;"> id)
{
    </span><span style="color: #0000ff;">if</span> (id == <span style="color: #0000ff;">null</span><span style="color: #000000;">)
    {
        </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> NotFound();
    }

    </span><span style="color: #0000ff;">string</span> query = <span style="color: #800000;">"</span><span style="color: #800000;">SELECT * FROM Department WHERE DepartmentID = {0}</span><span style="color: #800000;">"</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">var</span> department = <span style="color: #0000ff;">await</span><span style="color: #000000;"> _context.Departments
        .FromSql(query, id)
        .Include(d </span>=&gt;<span style="color: #000000;"> d.Administrator)
        .AsNoTracking()
        .SingleOrDefaultAsync();

    </span><span style="color: #0000ff;">if</span> (department == <span style="color: #0000ff;">null</span><span style="color: #000000;">)
    {
        </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> NotFound();
    }

    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> View(department);
}</span></pre>
</div>
<span class="cnblogs_code_collapse">FromSql</span></div>
<p>②<span data-ttu-id="4e9d1-129">调用返回其他类型的查询</span></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('f2990e29-a11e-4d5d-9c65-c3c6fea4d532')"><img id="code_img_closed_f2990e29-a11e-4d5d-9c65-c3c6fea4d532" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_f2990e29-a11e-4d5d-9c65-c3c6fea4d532" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('f2990e29-a11e-4d5d-9c65-c3c6fea4d532',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_f2990e29-a11e-4d5d-9c65-c3c6fea4d532" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task&lt;ActionResult&gt;<span style="color: #000000;"> About()
{
    List</span>&lt;EnrollmentDateGroup&gt; groups = <span style="color: #0000ff;">new</span> List&lt;EnrollmentDateGroup&gt;<span style="color: #000000;">();
    </span><span style="color: #0000ff;">var</span> conn =<span style="color: #000000;"> _context.Database.GetDbConnection();
    </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">await</span><span style="color: #000000;"> conn.OpenAsync();
        </span><span style="color: #0000ff;">using</span> (<span style="color: #0000ff;">var</span> command =<span style="color: #000000;"> conn.CreateCommand())
        {
            </span><span style="color: #0000ff;">string</span> query = <span style="color: #800000;">"</span><span style="color: #800000;">SELECT EnrollmentDate, COUNT(*) AS StudentCount </span><span style="color: #800000;">"</span>
                + <span style="color: #800000;">"</span><span style="color: #800000;">FROM Person </span><span style="color: #800000;">"</span>
                + <span style="color: #800000;">"</span><span style="color: #800000;">WHERE Discriminator = 'Student' </span><span style="color: #800000;">"</span>
                + <span style="color: #800000;">"</span><span style="color: #800000;">GROUP BY EnrollmentDate</span><span style="color: #800000;">"</span><span style="color: #000000;">;
            command.CommandText </span>=<span style="color: #000000;"> query;
            DbDataReader reader </span>= <span style="color: #0000ff;">await</span><span style="color: #000000;"> command.ExecuteReaderAsync();

            </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (reader.HasRows)
            {
                </span><span style="color: #0000ff;">while</span> (<span style="color: #0000ff;">await</span><span style="color: #000000;"> reader.ReadAsync())
                {
                    </span><span style="color: #0000ff;">var</span> row = <span style="color: #0000ff;">new</span> EnrollmentDateGroup { EnrollmentDate = reader.GetDateTime(<span style="color: #800080;">0</span>), StudentCount = reader.GetInt32(<span style="color: #800080;">1</span><span style="color: #000000;">) };
                    groups.Add(row);
                }
            }
            reader.Dispose();
        }
    }
    </span><span style="color: #0000ff;">finally</span><span style="color: #000000;">
    {
        conn.Close();
    }
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> View(groups);
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Code</span></div>
<p>③<span data-ttu-id="4e9d1-140">调用更新查询</span></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('4e80326b-0e29-4484-9185-64db7f978c45')"><img id="code_img_closed_4e80326b-0e29-4484-9185-64db7f978c45" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_4e80326b-0e29-4484-9185-64db7f978c45" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('4e80326b-0e29-4484-9185-64db7f978c45',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_4e80326b-0e29-4484-9185-64db7f978c45" class="cnblogs_code_hide">
<pre><span style="color: #000000;">[HttpPost]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task&lt;IActionResult&gt; UpdateCourseCredits(<span style="color: #0000ff;">int</span>?<span style="color: #000000;"> multiplier)
{
    </span><span style="color: #0000ff;">if</span> (multiplier != <span style="color: #0000ff;">null</span><span style="color: #000000;">)
    {
        ViewData[</span><span style="color: #800000;">"</span><span style="color: #800000;">RowsAffected</span><span style="color: #800000;">"</span>] = 
            <span style="color: #0000ff;">await</span><span style="color: #000000;"> _context.Database.ExecuteSqlCommandAsync(
                </span><span style="color: #800000;">"</span><span style="color: #800000;">UPDATE Course SET Credits = Credits * {0}</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                parameters: multiplier);
    }
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> View();
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Code</span></div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a3"></a>三、Razor页面</span></strong></p>
<p><strong>1，路由</strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">a </span><span style="color: #ff0000;">asp-action</span><span style="color: #0000ff;">="Edit"</span><span style="color: #ff0000;"> asp-route-studentID</span><span style="color: #0000ff;">="@item.ID"</span><span style="color: #0000ff;">&gt;</span>Edit<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">a</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">a </span><span style="color: #ff0000;">href</span><span style="color: #0000ff;">="/Students/Edit?studentID=6"</span><span style="color: #0000ff;">&gt;</span>Edit<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">a</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p><strong>2，命令搭建基架</strong></p>
<p>参考文档：<a href="https://docs.microsoft.com/zh-cn/aspnet/core/data/ef-rp/intro#add-scaffold-tooling" target="_blank">https://docs.microsoft.com/zh-cn/aspnet/core/data/ef-rp/intro#add-scaffold-tooling&nbsp;</a></p>
<p><strong>3，SelectList</strong></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('0db79e02-7202-40ce-9fea-cc2dcea4631c')"><img id="code_img_closed_0db79e02-7202-40ce-9fea-cc2dcea4631c" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_0db79e02-7202-40ce-9fea-cc2dcea4631c" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('0db79e02-7202-40ce-9fea-cc2dcea4631c',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_0db79e02-7202-40ce-9fea-cc2dcea4631c" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> ContosoUniversity.Data;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Mvc.RazorPages;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Mvc.Rendering;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.EntityFrameworkCore;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ContosoUniversity.Pages.Courses
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> DepartmentNamePageModel : PageModel
    {
        </span><span style="color: #0000ff;">public</span> SelectList DepartmentNameSL { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> PopulateDepartmentsDropDownList(SchoolContext _context,
            </span><span style="color: #0000ff;">object</span> selectedDepartment = <span style="color: #0000ff;">null</span><span style="color: #000000;">)
        {
            </span><span style="color: #0000ff;">var</span> departmentsQuery = <span style="color: #0000ff;">from</span> d <span style="color: #0000ff;">in</span><span style="color: #000000;"> _context.Departments
                                   </span><span style="color: #0000ff;">orderby</span> d.Name <span style="color: #008000;">//</span><span style="color: #008000;"> Sort by name.</span>
                                   <span style="color: #0000ff;">select</span><span style="color: #000000;"> d;

            DepartmentNameSL </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> SelectList(departmentsQuery.AsNoTracking(),
                        </span><span style="color: #800000;">"</span><span style="color: #800000;">DepartmentID</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">Name</span><span style="color: #800000;">"</span><span style="color: #000000;">, selectedDepartment);
        }
    }
}


  </span>&lt;div <span style="color: #0000ff;">class</span>=<span style="color: #800000;">"</span><span style="color: #800000;">form-group</span><span style="color: #800000;">"</span>&gt;
                &lt;label asp-<span style="color: #0000ff;">for</span>=<span style="color: #800000;">"</span><span style="color: #800000;">Course.Department</span><span style="color: #800000;">"</span> <span style="color: #0000ff;">class</span>=<span style="color: #800000;">"</span><span style="color: #800000;">control-label</span><span style="color: #800000;">"</span>&gt;&lt;/label&gt;
                &lt;<span style="color: #0000ff;">select</span> asp-<span style="color: #0000ff;">for</span>=<span style="color: #800000;">"</span><span style="color: #800000;">Course.DepartmentID</span><span style="color: #800000;">"</span> <span style="color: #0000ff;">class</span>=<span style="color: #800000;">"</span><span style="color: #800000;">form-control</span><span style="color: #800000;">"</span><span style="color: #000000;">
                        asp</span>-items=<span style="color: #800000;">"</span><span style="color: #800000;">@Model.DepartmentNameSL</span><span style="color: #800000;">"</span>&gt;
                    &lt;option value=<span style="color: #800000;">""</span>&gt;-- Select Department --&lt;/option&gt;
                &lt;/<span style="color: #0000ff;">select</span>&gt;
                &lt;span asp-validation-<span style="color: #0000ff;">for</span>=<span style="color: #800000;">"</span><span style="color: #800000;">Course.DepartmentID</span><span style="color: #800000;">"</span> <span style="color: #0000ff;">class</span>=<span style="color: #800000;">"</span><span style="color: #800000;">text-danger</span><span style="color: #800000;">"</span> /&gt;
            &lt;/div&gt;</pre>
</div>
<span class="cnblogs_code_collapse">Code</span></div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a4"></a>四、MVC</span></strong></p>
<p><strong>1，模型绑定&nbsp;<a name="a41"></a></strong></p>
<p>&nbsp;①常用的验证属性</p>
<ul>
<li>
<p><span data-ttu-id="3ae3f-123"><code>[CreditCard]</code>：验证属性是否具有信用卡格式。</span></p>
</li>
<li>
<p><span data-ttu-id="3ae3f-124"><code>[Compare]</code>：验证某个模型中的两个属性是否匹配。</span></p>
</li>
<li>
<p><span data-ttu-id="3ae3f-125"><code>[EmailAddress]</code>：验证属性是否具有电子邮件格式。</span></p>
</li>
<li>
<p><span data-ttu-id="3ae3f-126"><code>[Phone]</code>：验证属性是否具有电话格式。</span></p>
</li>
<li>
<p><span data-ttu-id="3ae3f-127"><code>[Range]</code>：验证属性值是否落在给定范围内。</span></p>
</li>
<li>
<p><span data-ttu-id="3ae3f-128"><code>[RegularExpression]</code>：验证数据是否与指定的正则表达式匹配。</span></p>
</li>
<li>
<p><span data-ttu-id="3ae3f-129"><code>[Required]</code>：将属性设置为必需属性。</span></p>
</li>
<li>
<p><span data-ttu-id="3ae3f-130"><code>[StringLength]</code>：验证字符串属性是否最多具有给定的最大长度。</span></p>
</li>
<li>
<p><span data-ttu-id="3ae3f-131"><code>[Url]</code>：验证属性是否具有 URL 格式。</span></p>
</li>
</ul>
<p>&nbsp;</p>
<p><strong>2，视图<a name="a42"></a></strong></p>
<p>①Razor语法</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('69499f0b-a3e4-43f5-8c0f-b666c04c0da4')"><img id="code_img_closed_69499f0b-a3e4-43f5-8c0f-b666c04c0da4" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_69499f0b-a3e4-43f5-8c0f-b666c04c0da4" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('69499f0b-a3e4-43f5-8c0f-b666c04c0da4',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_69499f0b-a3e4-43f5-8c0f-b666c04c0da4" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span>Last week this time: @(DateTime.Now - TimeSpan.FromDays(7))<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<span class="cnblogs_code_collapse">计算 @() 括号中的所有内容，并将其呈现到输出中</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('133471dc-f38c-4c74-9e30-446b9b578eb2')"><img id="code_img_closed_133471dc-f38c-4c74-9e30-446b9b578eb2" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_133471dc-f38c-4c74-9e30-446b9b578eb2" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('133471dc-f38c-4c74-9e30-446b9b578eb2',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_133471dc-f38c-4c74-9e30-446b9b578eb2" class="cnblogs_code_hide">
<pre><span style="color: #000000;">@{
    var joe = new Person("Joe", 33);
}

</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span>Age@(joe.Age)<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<span class="cnblogs_code_collapse">使用显式表达式将文本与表达式结果串联起来</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('7642785a-9c44-4525-b40d-e94125cec29c')"><img id="code_img_closed_7642785a-9c44-4525-b40d-e94125cec29c" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_7642785a-9c44-4525-b40d-e94125cec29c" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('7642785a-9c44-4525-b40d-e94125cec29c',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_7642785a-9c44-4525-b40d-e94125cec29c" class="cnblogs_code_hide">
<pre>@Html.Raw("<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">span</span><span style="color: #0000ff;">&gt;</span>Hello World<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">span</span><span style="color: #0000ff;">&gt;</span>")</pre>
</div>
<span class="cnblogs_code_collapse">输出不进行编码，但呈现为 HTML 标记</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('bf018ac0-202b-4f55-82a8-33cd7ffc6dd2')"><img id="code_img_closed_bf018ac0-202b-4f55-82a8-33cd7ffc6dd2" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_bf018ac0-202b-4f55-82a8-33cd7ffc6dd2" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('bf018ac0-202b-4f55-82a8-33cd7ffc6dd2',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_bf018ac0-202b-4f55-82a8-33cd7ffc6dd2" class="cnblogs_code_hide">
<pre>@for (var i = 0; i <span style="color: #0000ff;">&lt;</span><span style="color: #800000;"> people</span><span style="color: #ff0000;">.Length; i++)
{
    var person </span><span style="color: #0000ff;">= people[i];
    </span><span style="color: #ff0000;">&lt;text</span><span style="color: #0000ff;">&gt;</span>Name: @person.Name<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">text</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">
}</span></pre>
</div>
<span class="cnblogs_code_collapse">带分隔符的显式转换</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('8aadfeba-3351-4d91-b184-bfd33e36aecf')"><img id="code_img_closed_8aadfeba-3351-4d91-b184-bfd33e36aecf" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_8aadfeba-3351-4d91-b184-bfd33e36aecf" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('8aadfeba-3351-4d91-b184-bfd33e36aecf',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_8aadfeba-3351-4d91-b184-bfd33e36aecf" class="cnblogs_code_hide">
<pre>@for (var i = 0; i <span style="color: #0000ff;">&lt;</span><span style="color: #800000;"> people</span><span style="color: #ff0000;">.Length; i++)
{
    var person </span><span style="color: #0000ff;">= people[i];
    </span><span style="color: #ff0000;">@:Name: @person.Name
}</span></pre>
</div>
<span class="cnblogs_code_collapse">使用 @ 的显式行转换</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('4c083550-3b93-4099-b4b7-0033c0d3ab99')"><img id="code_img_closed_4c083550-3b93-4099-b4b7-0033c0d3ab99" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_4c083550-3b93-4099-b4b7-0033c0d3ab99" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('4c083550-3b93-4099-b4b7-0033c0d3ab99',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_4c083550-3b93-4099-b4b7-0033c0d3ab99" class="cnblogs_code_hide">
<pre><span style="color: #000000;">@if (value % 2 == 0)
{
    </span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span>The value was even.<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">
}
else if (value &gt;= 1337)
{
    </span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span>The value is large.<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">
}
else
{
    </span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span>The value is odd and small.<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">
}</span></pre>
</div>
<span class="cnblogs_code_collapse">@if、else if、else</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('d2dda91e-966d-47f0-bf25-1b025af24fa9')"><img id="code_img_closed_d2dda91e-966d-47f0-bf25-1b025af24fa9" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_d2dda91e-966d-47f0-bf25-1b025af24fa9" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('d2dda91e-966d-47f0-bf25-1b025af24fa9',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_d2dda91e-966d-47f0-bf25-1b025af24fa9" class="cnblogs_code_hide">
<pre><span style="color: #000000;">@switch (value)
{
    case 1:
        </span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span>The value is 1!<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">
        break;
    case 1337:
        </span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span>Your number is 1337!<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">
        break;
    default:
        </span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span>Your number wasn't 1 or 1337.<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">
        break;
}</span></pre>
</div>
<span class="cnblogs_code_collapse">@switch</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('eb112c9c-e77d-4525-b5a1-a4c7990f8160')"><img id="code_img_closed_eb112c9c-e77d-4525-b5a1-a4c7990f8160" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_eb112c9c-e77d-4525-b5a1-a4c7990f8160" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('eb112c9c-e77d-4525-b5a1-a4c7990f8160',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_eb112c9c-e77d-4525-b5a1-a4c7990f8160" class="cnblogs_code_hide">
<pre>@for (var i = 0; i <span style="color: #0000ff;">&lt;</span><span style="color: #800000;"> people</span><span style="color: #ff0000;">.Length; i++)
{
    var person </span><span style="color: #0000ff;">= people[i];
    </span><span style="color: #ff0000;">&lt;p</span><span style="color: #0000ff;">&gt;</span>Name: @person.Name<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span>Age: @person.Age<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">
}</span></pre>
</div>
<span class="cnblogs_code_collapse">@for</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('0c2d5540-d011-45e7-aabe-4314b997962d')"><img id="code_img_closed_0c2d5540-d011-45e7-aabe-4314b997962d" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_0c2d5540-d011-45e7-aabe-4314b997962d" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('0c2d5540-d011-45e7-aabe-4314b997962d',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_0c2d5540-d011-45e7-aabe-4314b997962d" class="cnblogs_code_hide">
<pre><span style="color: #000000;">@foreach (var person in people)
{
    </span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span>Name: @person.Name<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span>Age: @person.Age<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">
}</span></pre>
</div>
<span class="cnblogs_code_collapse">@foreach</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('aea94874-7bff-4565-a530-a7910c4a604a')"><img id="code_img_closed_aea94874-7bff-4565-a530-a7910c4a604a" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_aea94874-7bff-4565-a530-a7910c4a604a" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('aea94874-7bff-4565-a530-a7910c4a604a',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_aea94874-7bff-4565-a530-a7910c4a604a" class="cnblogs_code_hide">
<pre><span style="color: #000000;">@{ var i = 0; }
@while (i </span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;"> people</span><span style="color: #ff0000;">.Length)
{
    var person </span><span style="color: #0000ff;">= people[i];
    </span><span style="color: #ff0000;">&lt;p</span><span style="color: #0000ff;">&gt;</span>Name: @person.Name<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span>Age: @person.Age<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">

    i++;
}</span></pre>
</div>
<span class="cnblogs_code_collapse">@while</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('dd6bd1e7-2ac4-49ff-bfda-6a58474b79c5')"><img id="code_img_closed_dd6bd1e7-2ac4-49ff-bfda-6a58474b79c5" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_dd6bd1e7-2ac4-49ff-bfda-6a58474b79c5" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('dd6bd1e7-2ac4-49ff-bfda-6a58474b79c5',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_dd6bd1e7-2ac4-49ff-bfda-6a58474b79c5" class="cnblogs_code_hide">
<pre><span style="color: #000000;">@{ var i = 0; }
@do
{
    var person = people[i];
    </span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span>Name: @person.Name<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span>Age: @person.Age<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">

    i++;
} while (i </span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;"> people</span><span style="color: #ff0000;">.Length);</span></pre>
</div>
<span class="cnblogs_code_collapse">@do while</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('60cc90ce-a7e0-4b3e-addb-7dc624a06c72')"><img id="code_img_closed_60cc90ce-a7e0-4b3e-addb-7dc624a06c72" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_60cc90ce-a7e0-4b3e-addb-7dc624a06c72" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('60cc90ce-a7e0-4b3e-addb-7dc624a06c72',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_60cc90ce-a7e0-4b3e-addb-7dc624a06c72" class="cnblogs_code_hide">
<pre><span style="color: #000000;">@using (Html.BeginForm())
{
    </span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">
        email:
        </span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="email"</span><span style="color: #ff0000;"> id</span><span style="color: #0000ff;">="Email"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">=""</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">button</span><span style="color: #0000ff;">&gt;</span>Register<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">button</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">
}</span></pre>
</div>
<span class="cnblogs_code_collapse">复合语句 @using</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('28f8fd8e-f9ee-4e11-a311-7412e1c69767')"><img id="code_img_closed_28f8fd8e-f9ee-4e11-a311-7412e1c69767" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_28f8fd8e-f9ee-4e11-a311-7412e1c69767" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('28f8fd8e-f9ee-4e11-a311-7412e1c69767',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_28f8fd8e-f9ee-4e11-a311-7412e1c69767" class="cnblogs_code_hide">
<pre><span style="color: #000000;">@try
{
    throw new InvalidOperationException("You did something invalid.");
}
catch (Exception ex)
{
    </span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span>The exception message: @ex.Message<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">
}
finally
{
    </span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span>The finally statement.<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">p</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">
}</span></pre>
</div>
<span class="cnblogs_code_collapse">@try、catch、finally</span></div>
<p>②@inherits 指令对视图继承的类提供完全控制</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('9e19ead8-1ab3-42ed-85f8-c58166b20013')"><img id="code_img_closed_9e19ead8-1ab3-42ed-85f8-c58166b20013" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_9e19ead8-1ab3-42ed-85f8-c58166b20013" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('9e19ead8-1ab3-42ed-85f8-c58166b20013',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_9e19ead8-1ab3-42ed-85f8-c58166b20013" class="cnblogs_code_hide">
<pre><span style="color: #000000;">using Microsoft.AspNetCore.Mvc.Razor;

public abstract class CustomRazorPage</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">TModel</span><span style="color: #0000ff;">&gt;</span> : RazorPage<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">TModel</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">
{
    public string CustomText { get; } = "Gardyloo! - A Scottish warning yelled from a window before dumping a slop bucket on the street below.";
}</span></pre>
</div>
<span class="cnblogs_code_collapse">自定义 Razor 页面类型</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('ccb2c9cf-4f5c-4485-8728-f407cfeec26c')"><img id="code_img_closed_ccb2c9cf-4f5c-4485-8728-f407cfeec26c" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_ccb2c9cf-4f5c-4485-8728-f407cfeec26c" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('ccb2c9cf-4f5c-4485-8728-f407cfeec26c',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_ccb2c9cf-4f5c-4485-8728-f407cfeec26c" class="cnblogs_code_hide">
<pre>@inherits CustomRazorPage<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">TModel</span><span style="color: #0000ff;">&gt;</span>

<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>Custom text: @CustomText<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<span class="cnblogs_code_collapse">CustomText 显示在视图中</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('818b004d-9e7a-4191-bb73-64120c31db6b')"><img id="code_img_closed_818b004d-9e7a-4191-bb73-64120c31db6b" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_818b004d-9e7a-4191-bb73-64120c31db6b" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('818b004d-9e7a-4191-bb73-64120c31db6b',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_818b004d-9e7a-4191-bb73-64120c31db6b" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>Custom text: Gardyloo! - A Scottish warning yelled from a window before dumping a slop bucket on the street below.<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<span class="cnblogs_code_collapse">呈现</span></div>
<p>③<code>@functions</code>&nbsp;指令允许 Razor 页面将 C# 代码块添加到视图中</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('5830fc09-eba2-41de-813b-07813caea3a2')"><img id="code_img_closed_5830fc09-eba2-41de-813b-07813caea3a2" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_5830fc09-eba2-41de-813b-07813caea3a2" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('5830fc09-eba2-41de-813b-07813caea3a2',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_5830fc09-eba2-41de-813b-07813caea3a2" class="cnblogs_code_hide">
<pre><span style="color: #000000;">@functions {
    public string GetHello()
    {
        return "Hello";
    }
}

</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>From method: @GetHello()<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span> </pre>
</div>
<span class="cnblogs_code_collapse">视图</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('b4f4f294-e0f5-4a90-bf97-782a5aaae2bc')"><img id="code_img_closed_b4f4f294-e0f5-4a90-bf97-782a5aaae2bc" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_b4f4f294-e0f5-4a90-bf97-782a5aaae2bc" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('b4f4f294-e0f5-4a90-bf97-782a5aaae2bc',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_b4f4f294-e0f5-4a90-bf97-782a5aaae2bc" class="cnblogs_code_hide">
<pre><span style="color: #000000;">using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc.Razor;

public class _Views_Home_Test_cshtml : RazorPage</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">dynamic</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">
{
    // Functions placed between here 
    public string GetHello()
    {
        return "Hello";
    }
    // And here.
#pragma warning disable 1998
    public override async Task ExecuteAsync()
    {
        WriteLiteral("\r\n</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">From method: ");
        Write(GetHello());
        WriteLiteral("</span><span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">\r\n");
    }
#pragma warning restore 1998</span></pre>
</div>
<span class="cnblogs_code_collapse">生成的 Razor C# 类</span></div>
<p>④_ViewImports.cshtml<span data-ttu-id="bf002-146">导入共享指令</span></p>
<p>&nbsp;支持的指令：</p>
<ul>
<li>
<p><code>@addTagHelper</code></p>
</li>
<li>
<p><code>@removeTagHelper</code></p>
</li>
<li>
<p><code>@tagHelperPrefix</code></p>
</li>
<li>
<p><code>@using</code></p>
</li>
<li>
<p><code>@model</code></p>
</li>
<li>
<p><code>@inherits</code></p>
</li>
<li>
<p><code>@inject</code></p>
</li>
</ul>
<p>&nbsp;针对 ASP.NET Core MVC 应用的&nbsp;<code>_ViewImports.cshtml</code>&nbsp;文件通常放置在&nbsp;<code>Views</code>&nbsp;文件夹中</p>
<p>&nbsp;</p>
<p><strong>3，标记帮助程序<a name="a43"></a></strong></p>
<p>①@addTagHelper</p>
<div class="cnblogs_code">
<pre>@addTagHelper *<span style="color: #000000;">, Microsoft.AspNetCore.Mvc.TagHelpers
@addTagHelper MvcDemo2.TagHelpers.EmailTagHelper,MvcDemo2</span></pre>
</div>
<pre>@addTagHelper之后第一个参数：需要加载的标记帮助类（*表示所有）<br />第二个参数：标记帮助类所在的程序集</pre>
<p>②简单的将&nbsp;<span class="cnblogs_code"><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">email</span><span style="color: #0000ff;">&gt;</span>hunter<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">email</span><span style="color: #0000ff;">&gt;</span></span>&nbsp;变成&nbsp;<span class="cnblogs_code"><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">a</span><span style="color: #0000ff;">&gt;</span>hunter<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">a</span><span style="color: #0000ff;">&gt;</span></span>&nbsp;&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('a16ab08a-afbe-4512-9e37-d0f4d56b3154')"><img id="code_img_closed_a16ab08a-afbe-4512-9e37-d0f4d56b3154" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_a16ab08a-afbe-4512-9e37-d0f4d56b3154" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('a16ab08a-afbe-4512-9e37-d0f4d56b3154',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_a16ab08a-afbe-4512-9e37-d0f4d56b3154" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Razor.TagHelpers;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> MvcDemo2.TagHelpers
{
    </span><span style="color: #008000;">//</span><span style="color: #008000;">EmailTagHelper 的根名称是 email，因此 &lt;email&gt; 标记将作为目标名称</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> EmailTagHelper:TagHelper
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Process(TagHelperContext context, TagHelperOutput output)
        {
            output.TagName</span>=<span style="color: #800000;">"</span><span style="color: #800000;">a</span><span style="color: #800000;">"</span>;<span style="color: #008000;">//</span><span style="color: #008000;">用&lt;a&gt;标签替换&lt;email&gt;</span>
<span style="color: #000000;">        }

    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">①添加EmailTagHelper</span></div>
<p><img src="https://images2018.cnblogs.com/blog/741594/201805/741594-20180531195448508-925204350.png" alt="" width="147" height="84" /></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('6d9455d7-c3e5-486d-b64e-9a7dbc8febc3')"><img id="code_img_closed_6d9455d7-c3e5-486d-b64e-9a7dbc8febc3" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_6d9455d7-c3e5-486d-b64e-9a7dbc8febc3" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('6d9455d7-c3e5-486d-b64e-9a7dbc8febc3',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_6d9455d7-c3e5-486d-b64e-9a7dbc8febc3" class="cnblogs_code_hide">
<pre><span style="color: #000000;">@using MvcDemo2
@using MvcDemo2.Models
@addTagHelper </span>*<span style="color: #000000;">, Microsoft.AspNetCore.Mvc.TagHelpers
@addTagHelper MvcDemo2.TagHelpers.EmailTagHelper,MvcDemo2</span></pre>
</div>
<span class="cnblogs_code_collapse">②修改_ViewImports.cshtml</span></div>
<p>这时，在页面上的&nbsp;<span class="cnblogs_code">&lt;email&gt;hunter&lt;/email&gt;</span>&nbsp;会变成<span class="cnblogs_code">&lt;a&gt;hunter&lt;/a&gt;&nbsp;</span></p>
<p>③设置自结束标签&nbsp;<span class="cnblogs_code">&lt;email/&gt;</span>&nbsp;&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('7303ffeb-fba9-4eab-98be-63e39d8a1413')"><img id="code_img_closed_7303ffeb-fba9-4eab-98be-63e39d8a1413" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_7303ffeb-fba9-4eab-98be-63e39d8a1413" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('7303ffeb-fba9-4eab-98be-63e39d8a1413',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_7303ffeb-fba9-4eab-98be-63e39d8a1413" class="cnblogs_code_hide">
<pre>    [HtmlTargetElement(<span style="color: #800000;">"</span><span style="color: #800000;">email</span><span style="color: #800000;">"</span>,TagStructure=<span style="color: #000000;">TagStructure.WithoutEndTag)]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> EmailTagHelper:TagHelper</pre>
</div>
<span class="cnblogs_code_collapse">HtmlTargetElement</span></div>
<p>如果存在不是自结束标签，就会报错</p>
<p>④将&nbsp;<span class="cnblogs_code">&lt;email mail-to=<span style="color: #800000;">"</span><span style="color: #800000;">hunter</span><span style="color: #800000;">"</span>&gt;&lt;/email&gt;</span>&nbsp;变成&nbsp;<span class="cnblogs_code">&lt;a href=<span style="color: #800000;">"</span><span style="color: #800000;">hunter@qq.com</span><span style="color: #800000;">"</span>&gt;hunter@qq.com&lt;/a&gt;</span>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('953a8195-3bb2-4315-8fa1-3ee4bd98e2bb')"><img id="code_img_closed_953a8195-3bb2-4315-8fa1-3ee4bd98e2bb" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_953a8195-3bb2-4315-8fa1-3ee4bd98e2bb" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('953a8195-3bb2-4315-8fa1-3ee4bd98e2bb',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_953a8195-3bb2-4315-8fa1-3ee4bd98e2bb" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Razor.TagHelpers;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> MvcDemo2.TagHelpers
{
    </span><span style="color: #008000;">//</span><span style="color: #008000;">EmailTagHelper 的根名称是 email，因此 &lt;email&gt; 标记将作为目标名称</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> EmailTagHelper:TagHelper
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">const</span> <span style="color: #0000ff;">string</span> EmailDomain=<span style="color: #800000;">"</span><span style="color: #800000;">qq.com</span><span style="color: #800000;">"</span><span style="color: #000000;">;
        </span><span style="color: #008000;">//</span><span style="color: #008000;">可以通过&lt;email mail-to =&ldquo;...&rdquo;/&gt;传递
        </span><span style="color: #008000;">//</span><span style="color: #008000;">标记帮助程序采用 Pascal 大小写格式的类和属性名将转换为各自相应的小写短横线格式</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> MailTo{<span style="color: #0000ff;">get</span>;<span style="color: #0000ff;">set</span><span style="color: #000000;">;}
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Process(TagHelperContext context, TagHelperOutput output)
        {
            output.TagName</span>=<span style="color: #800000;">"</span><span style="color: #800000;">a</span><span style="color: #800000;">"</span>;<span style="color: #008000;">//</span><span style="color: #008000;">用&lt;a&gt;标签替换&lt;email&gt;</span>
            <span style="color: #0000ff;">var</span> address=MailTo+<span style="color: #800000;">"</span><span style="color: #800000;">@</span><span style="color: #800000;">"</span>+<span style="color: #000000;">EmailDomain;

            </span><span style="color: #008000;">//</span><span style="color: #008000;">给标签添加属性</span>
            output.Attributes.SetAttribute(<span style="color: #800000;">"</span><span style="color: #800000;">href</span><span style="color: #800000;">"</span><span style="color: #000000;">,address);
            </span><span style="color: #008000;">//</span><span style="color: #008000;">设置&lt;email&gt;&lt;/email&gt;里面的内容</span>
<span style="color: #000000;">            output.Content.SetContent(address);
        }

    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">EmailTagHelper</span></div>
<p>⑤将&nbsp;<span class="cnblogs_code">&lt;email&gt;hunter&lt;/email&gt;</span>&nbsp;变成<span class="cnblogs_code">&lt;a href="hunter@qq.com"&gt;hunter@qq.com&lt;/a&gt;&nbsp;</span></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('e4cacdda-b2b6-4781-ba40-3e732e3e7cef')"><img id="code_img_closed_e4cacdda-b2b6-4781-ba40-3e732e3e7cef" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_e4cacdda-b2b6-4781-ba40-3e732e3e7cef" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('e4cacdda-b2b6-4781-ba40-3e732e3e7cef',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_e4cacdda-b2b6-4781-ba40-3e732e3e7cef" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Razor.TagHelpers;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> MvcDemo2.TagHelpers
{
    </span><span style="color: #008000;">//</span><span style="color: #008000;">EmailTagHelper 的根名称是 email，因此 &lt;email&gt; 标记将作为目标名称</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> EmailTagHelper:TagHelper
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">const</span> <span style="color: #0000ff;">string</span> EmailDomain=<span style="color: #800000;">"</span><span style="color: #800000;">qq.com</span><span style="color: #800000;">"</span><span style="color: #000000;">;
        </span><span style="color: #008000;">//</span><span style="color: #008000;">可以通过&lt;email mail-to =&ldquo;...&rdquo;/&gt;传递</span>

        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">async</span><span style="color: #000000;"> Task ProcessAsync(TagHelperContext context, TagHelperOutput output)
        {
            output.TagName</span>=<span style="color: #800000;">"</span><span style="color: #800000;">a</span><span style="color: #800000;">"</span>;<span style="color: #008000;">//</span><span style="color: #008000;">用&lt;a&gt;标签替换&lt;email&gt;</span>

            <span style="color: #0000ff;">var</span> content=<span style="color: #0000ff;">await</span> output.GetChildContentAsync();<span style="color: #008000;">//</span><span style="color: #008000;">获取标签里的内容</span>
            <span style="color: #0000ff;">var</span> tagter=content.GetContent()+<span style="color: #800000;">"</span><span style="color: #800000;">@</span><span style="color: #800000;">"</span>+<span style="color: #000000;">EmailDomain;

            </span><span style="color: #008000;">//</span><span style="color: #008000;">给标签添加属性</span>
            output.Attributes.SetAttribute(<span style="color: #800000;">"</span><span style="color: #800000;">href</span><span style="color: #800000;">"</span><span style="color: #000000;">,tagter);
            </span><span style="color: #008000;">//</span><span style="color: #008000;">设置&lt;email&gt;&lt;/email&gt;里面的内容</span>
<span style="color: #000000;">            output.Content.SetContent(tagter);
        }

    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">EmailTagHelper</span></div>
<p>⑥将页面中的&nbsp;<span class="cnblogs_code">&lt;bold&gt;bbbb&lt;/bold&gt;</span>&nbsp;替换为&nbsp;<span class="cnblogs_code">&lt;strong&gt;bbbb&lt;/strong&gt;</span>&nbsp;&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('9354045f-b9c6-4a99-974f-89487a54cfb4')"><img id="code_img_closed_9354045f-b9c6-4a99-974f-89487a54cfb4" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_9354045f-b9c6-4a99-974f-89487a54cfb4" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('9354045f-b9c6-4a99-974f-89487a54cfb4',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_9354045f-b9c6-4a99-974f-89487a54cfb4" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Razor.TagHelpers;
</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> MvcDemo2.TagHelpers
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> BoldTagHelper:TagHelper
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Process(TagHelperContext context, TagHelperOutput output)
        {
            output.Attributes.RemoveAll(</span><span style="color: #800000;">"</span><span style="color: #800000;">bold</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            output.PreContent.SetHtmlContent(</span><span style="color: #800000;">"</span><span style="color: #800000;">&lt;strong&gt;</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            output.PostContent.SetHtmlContent(</span><span style="color: #800000;">"</span><span style="color: #800000;">&lt;/strong&gt;</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }
        
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">BoldTagHelper</span></div>
<p>③将model传入标记帮助程序</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('91f74a2f-1907-4c2f-9ae6-c8dda5d099fe')"><img id="code_img_closed_91f74a2f-1907-4c2f-9ae6-c8dda5d099fe" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_91f74a2f-1907-4c2f-9ae6-c8dda5d099fe" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('91f74a2f-1907-4c2f-9ae6-c8dda5d099fe',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_91f74a2f-1907-4c2f-9ae6-c8dda5d099fe" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> MvcDemo2.Models
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> WebsiteContext
    {
        </span><span style="color: #0000ff;">public</span> Version Version{<span style="color: #0000ff;">get</span>;<span style="color: #0000ff;">set</span><span style="color: #000000;">;}
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span> CopyrightYear{<span style="color: #0000ff;">get</span>;<span style="color: #0000ff;">set</span><span style="color: #000000;">;}
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">bool</span> Approved{<span style="color: #0000ff;">get</span>;<span style="color: #0000ff;">set</span><span style="color: #000000;">;}
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span> TagsToShow{<span style="color: #0000ff;">get</span>;<span style="color: #0000ff;">set</span><span style="color: #000000;">;}
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Model</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('e3eca4e5-f8b6-4c77-80cb-b8cfe53c30a9')"><img id="code_img_closed_e3eca4e5-f8b6-4c77-80cb-b8cfe53c30a9" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_e3eca4e5-f8b6-4c77-80cb-b8cfe53c30a9" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('e3eca4e5-f8b6-4c77-80cb-b8cfe53c30a9',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_e3eca4e5-f8b6-4c77-80cb-b8cfe53c30a9" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Razor.TagHelpers;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> MvcDemo2.Models;
</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> MvcDemo2.TagHelpers
{

    </span><span style="color: #008000;">//</span><span style="color: #008000;">使用&lt;website-information /&gt;</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> WebsiteInformationTagHelper:TagHelper
    {
        </span><span style="color: #0000ff;">public</span> WebsiteContext Info{<span style="color: #0000ff;">get</span>;<span style="color: #0000ff;">set</span><span style="color: #000000;">;}

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Process(TagHelperContext context, TagHelperOutput output)
        {
            output.TagName</span>=<span style="color: #800000;">"</span><span style="color: #800000;">section</span><span style="color: #800000;">"</span><span style="color: #000000;">;
            output.Content.SetHtmlContent(
                $</span><span style="color: #800000;">@"</span><span style="color: #800000;">&lt;ul&gt;&lt;li&gt;&lt;strong&gt;版本:&lt;/strong&gt; {Info.Version}&lt;/li&gt;
                &lt;li&gt;&lt;strong&gt;版权 年:&lt;/strong&gt; {Info.CopyrightYear}&lt;/li&gt;
                &lt;li&gt;&lt;strong&gt;是否批准:&lt;/strong&gt; {Info.Approved}&lt;/li&gt;
                &lt;li&gt;&lt;strong&gt;显示的标签:&lt;/strong&gt; {Info.TagsToShow}&lt;/li&gt;&lt;/ul&gt;</span><span style="color: #800000;">"</span><span style="color: #000000;">
            );
        }
        
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">WebsiteInformationTagHelper</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('fdda29d8-319c-403b-931b-1723ed6ca3bf')"><img id="code_img_closed_fdda29d8-319c-403b-931b-1723ed6ca3bf" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_fdda29d8-319c-403b-931b-1723ed6ca3bf" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('fdda29d8-319c-403b-931b-1723ed6ca3bf',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_fdda29d8-319c-403b-931b-1723ed6ca3bf" class="cnblogs_code_hide">
<pre>&lt;website-information info=<span style="color: #800000;">"</span><span style="color: #800000;">new WebsiteContext(){</span>
    Version=<span style="color: #0000ff;">new</span> Version(<span style="color: #800080;">1</span>,<span style="color: #800080;">3</span><span style="color: #000000;">),
    CopyrightYear</span>=<span style="color: #800080;">10</span><span style="color: #000000;">,
    Approved</span>=<span style="color: #0000ff;">true</span><span style="color: #000000;">,
    TagsToShow</span>=<span style="color: #800080;">131</span><span style="color: #000000;">
}</span><span style="color: #800000;">"</span><span style="color: #800000;">&gt;&lt;/website-information&gt;</span></pre>
</div>
<span class="cnblogs_code_collapse">Html</span></div>
<p>⑥.NET 类型和生成的 HTML 类型&nbsp;</p>
<table style="height: 154px; width: 576px;" border="1">
<thead>
<tr><th><span data-ttu-id="dd8b5-146">.NET 类型</span></th><th><span data-ttu-id="dd8b5-147">输入类型</span></th></tr>
</thead>
<tbody>
<tr>
<td><span data-ttu-id="dd8b5-148">Bool</span></td>
<td><span data-ttu-id="dd8b5-149">type=&rdquo;checkbox&rdquo;</span></td>
</tr>
<tr>
<td><span data-ttu-id="dd8b5-150">String</span></td>
<td><span data-ttu-id="dd8b5-151">type=&rdquo;text&rdquo;</span></td>
</tr>
<tr>
<td><span data-ttu-id="dd8b5-152">DateTime</span></td>
<td><span data-ttu-id="dd8b5-153">type=&rdquo;datetime&rdquo;</span></td>
</tr>
<tr>
<td><span data-ttu-id="dd8b5-154">Byte</span></td>
<td><span data-ttu-id="dd8b5-155">type=&rdquo;number&rdquo;</span></td>
</tr>
<tr>
<td><span data-ttu-id="dd8b5-156">Int</span></td>
<td><span data-ttu-id="dd8b5-157">type=&rdquo;number&rdquo;</span></td>
</tr>
<tr>
<td><span data-ttu-id="dd8b5-158">Single、Double</span></td>
<td><span data-ttu-id="dd8b5-159">type=&rdquo;number&rdquo;</span></td>
</tr>
</tbody>
</table>
<p>⑦数据注解和生成的 HTML 类型&nbsp;</p>
<p>&nbsp;</p>
<table style="height: 174px; width: 606px;" border="1">
<thead>
<tr><th><span data-ttu-id="dd8b5-161">特性</span></th><th><span data-ttu-id="dd8b5-162">输入类型</span></th></tr>
</thead>
<tbody>
<tr>
<td><span data-ttu-id="dd8b5-163">[EmailAddress]</span></td>
<td><span data-ttu-id="dd8b5-164">type=&rdquo;email&rdquo;</span></td>
</tr>
<tr>
<td><span data-ttu-id="dd8b5-165">[Url]</span></td>
<td><span data-ttu-id="dd8b5-166">type=&rdquo;url&rdquo;</span></td>
</tr>
<tr>
<td><span data-ttu-id="dd8b5-167">[HiddenInput]</span></td>
<td><span data-ttu-id="dd8b5-168">type=&rdquo;hidden&rdquo;</span></td>
</tr>
<tr>
<td><span data-ttu-id="dd8b5-169">[Phone]</span></td>
<td><span data-ttu-id="dd8b5-170">type=&rdquo;tel&rdquo;</span></td>
</tr>
<tr>
<td><span data-ttu-id="dd8b5-171">[DataType(DataType.Password)]</span></td>
<td><span data-ttu-id="dd8b5-172">type=&rdquo;password&rdquo;</span></td>
</tr>
<tr>
<td><span data-ttu-id="dd8b5-173">[DataType(DataType.Date)]</span></td>
<td><span data-ttu-id="dd8b5-174">type=&rdquo;date&rdquo;</span></td>
</tr>
<tr>
<td><span data-ttu-id="dd8b5-175">[DataType(DataType.Time)]</span></td>
<td><span data-ttu-id="dd8b5-176">type=&rdquo;time&rdquo;</span></td>
</tr>
</tbody>
</table>
<p>⑧验证标记帮助程序</p>
<p>&nbsp;<span class="cnblogs_code">&lt;span asp-validation-<span style="color: #0000ff;">for</span>=<span style="color: #800000;">"</span><span style="color: #800000;">Email</span><span style="color: #800000;">"</span>&gt;&lt;/span&gt;</span>&nbsp;</p>
<p>针对具有 asp-validation-summary 属性的 &lt;div&gt; 元素</p>
<table border="1">
<thead>
<tr><th><span data-ttu-id="dd8b5-267">asp-validation-summary</span></th><th><span data-ttu-id="dd8b5-268">显示的验证消息</span></th></tr>
</thead>
<tbody>
<tr>
<td><span data-ttu-id="dd8b5-269">ValidationSummary.All</span></td>
<td><span data-ttu-id="dd8b5-270">属性和模型级别</span></td>
</tr>
<tr>
<td><span data-ttu-id="dd8b5-271">ValidationSummary.ModelOnly</span></td>
<td><span data-ttu-id="dd8b5-272">模型</span></td>
</tr>
<tr>
<td><span data-ttu-id="dd8b5-273">ValidationSummary.None</span></td>
<td><span data-ttu-id="dd8b5-274">无</span></td>
</tr>
</tbody>
</table>
<p>实例：&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('557f7868-38d1-4495-b6e9-8ed678477ad6')"><img id="code_img_closed_557f7868-38d1-4495-b6e9-8ed678477ad6" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_557f7868-38d1-4495-b6e9-8ed678477ad6" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('557f7868-38d1-4495-b6e9-8ed678477ad6',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_557f7868-38d1-4495-b6e9-8ed678477ad6" class="cnblogs_code_hide">
<pre><span style="color: #000000;">@model RegisterViewModel
@{
    ViewData[</span><span style="color: #800000;">"</span><span style="color: #800000;">Title</span><span style="color: #800000;">"</span>] = <span style="color: #800000;">"</span><span style="color: #800000;">Home Page</span><span style="color: #800000;">"</span><span style="color: #000000;">;
}

</span>&lt;a bold&gt;aaa&lt;/a&gt;
&lt;bold&gt;bbbb&lt;/bold&gt;
&lt;!--Razor 知道 info 属性是一个类，而不是字符串，并且你想要编写 C# 代码。 编写任何非字符串标记帮助程序属性时，都不应使用 @@ 字符。--&gt;


&lt;website-information info=<span style="color: #800000;">"</span><span style="color: #800000;">new WebsiteContext(){</span>
    Version=<span style="color: #0000ff;">new</span> Version(<span style="color: #800080;">1</span>,<span style="color: #800080;">3</span><span style="color: #000000;">),
    CopyrightYear</span>=<span style="color: #800080;">10</span><span style="color: #000000;">,
    Approved</span>=<span style="color: #0000ff;">true</span><span style="color: #000000;">,
    TagsToShow</span>=<span style="color: #800080;">131</span><span style="color: #000000;">
}</span><span style="color: #800000;">"</span><span style="color: #800000;">&gt;&lt;/website-information&gt;</span>



&lt;form asp-action=<span style="color: #800000;">"</span><span style="color: #800000;">Register</span><span style="color: #800000;">"</span> method=<span style="color: #800000;">"</span><span style="color: #800000;">POST</span><span style="color: #800000;">"</span> role=<span style="color: #800000;">"</span><span style="color: #800000;">form</span><span style="color: #800000;">"</span>&gt;
    &lt;legend&gt;注册&lt;/legend&gt;

    &lt;div asp-validation-summary=<span style="color: #800000;">"</span><span style="color: #800000;">ModelOnly</span><span style="color: #800000;">"</span>&gt;&lt;/div&gt;

    &lt;div <span style="color: #0000ff;">class</span>=<span style="color: #800000;">"</span><span style="color: #800000;">form-group</span><span style="color: #800000;">"</span>&gt;
        &lt;input asp-<span style="color: #0000ff;">for</span>=<span style="color: #800000;">"</span><span style="color: #800000;">Email</span><span style="color: #800000;">"</span> <span style="color: #0000ff;">class</span>=<span style="color: #800000;">"</span><span style="color: #800000;">form-control</span><span style="color: #800000;">"</span> placeholder=<span style="color: #800000;">"</span><span style="color: #800000;">Input field</span><span style="color: #800000;">"</span>&gt;
        &lt;span asp-validation-<span style="color: #0000ff;">for</span>=<span style="color: #800000;">"</span><span style="color: #800000;">Email</span><span style="color: #800000;">"</span>&gt;&lt;/span&gt;
    &lt;/div&gt;

     &lt;div <span style="color: #0000ff;">class</span>=<span style="color: #800000;">"</span><span style="color: #800000;">form-group</span><span style="color: #800000;">"</span>&gt;
        &lt;input asp-<span style="color: #0000ff;">for</span>=<span style="color: #800000;">"</span><span style="color: #800000;">Password</span><span style="color: #800000;">"</span> <span style="color: #0000ff;">class</span>=<span style="color: #800000;">"</span><span style="color: #800000;">form-control</span><span style="color: #800000;">"</span> placeholder=<span style="color: #800000;">"</span><span style="color: #800000;">Input field</span><span style="color: #800000;">"</span>&gt;
        &lt;span asp-validation-<span style="color: #0000ff;">for</span>=<span style="color: #800000;">"</span><span style="color: #800000;">Password</span><span style="color: #800000;">"</span>&gt;&lt;/span&gt;
    &lt;/div&gt;

    &lt;button type=<span style="color: #800000;">"</span><span style="color: #800000;">submit</span><span style="color: #800000;">"</span> <span style="color: #0000ff;">class</span>=<span style="color: #800000;">"</span><span style="color: #800000;">btn btn-primary</span><span style="color: #800000;">"</span>&gt;Submit&lt;/button&gt;
&lt;/form&gt;</pre>
</div>
<span class="cnblogs_code_collapse">Index.cshtml</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('e361c30e-e085-4db5-b13a-20b85e7ee689')"><img id="code_img_closed_e361c30e-e085-4db5-b13a-20b85e7ee689" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_e361c30e-e085-4db5-b13a-20b85e7ee689" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('e361c30e-e085-4db5-b13a-20b85e7ee689',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_e361c30e-e085-4db5-b13a-20b85e7ee689" class="cnblogs_code_hide">
<pre><span style="color: #000000;">        [HttpPost]
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> IActionResult Register(RegisterViewModel model)
        {
            </span><span style="color: #0000ff;">return</span> View(<span style="color: #800000;">"</span><span style="color: #800000;">Index</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }</span></pre>
</div>
<span class="cnblogs_code_collapse">Controller</span></div>
<p>⑨选择标记帮助程序</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('b1326d96-0f0c-4406-9fa4-709731cc10cb')"><img id="code_img_closed_b1326d96-0f0c-4406-9fa4-709731cc10cb" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_b1326d96-0f0c-4406-9fa4-709731cc10cb" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('b1326d96-0f0c-4406-9fa4-709731cc10cb',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_b1326d96-0f0c-4406-9fa4-709731cc10cb" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Mvc.Rendering;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> MvcDemo2.Models
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> CountryViewModel
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Country{<span style="color: #0000ff;">get</span>;<span style="color: #0000ff;">set</span><span style="color: #000000;">;}
        </span><span style="color: #0000ff;">public</span> List&lt;SelectListItem&gt; Countries {<span style="color: #0000ff;">get</span>;}=<span style="color: #0000ff;">new</span> List&lt;SelectListItem&gt;<span style="color: #000000;">(){
            </span><span style="color: #0000ff;">new</span> SelectListItem(){Value=<span style="color: #800000;">"</span><span style="color: #800000;">MX</span><span style="color: #800000;">"</span>,Text=<span style="color: #800000;">"</span><span style="color: #800000;">墨西哥</span><span style="color: #800000;">"</span><span style="color: #000000;">},
            </span><span style="color: #0000ff;">new</span> SelectListItem(){Value=<span style="color: #800000;">"</span><span style="color: #800000;">CA</span><span style="color: #800000;">"</span>,Text=<span style="color: #800000;">"</span><span style="color: #800000;">加拿大</span><span style="color: #800000;">"</span><span style="color: #000000;">},
            </span><span style="color: #0000ff;">new</span> SelectListItem(){Value=<span style="color: #800000;">"</span><span style="color: #800000;">US</span><span style="color: #800000;">"</span>,Text=<span style="color: #800000;">"</span><span style="color: #800000;">美国</span><span style="color: #800000;">"</span><span style="color: #000000;">}
        };
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">CountryViewModel</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('2d6f56c3-1bc2-49b9-b1d4-993210dfb62e')"><img id="code_img_closed_2d6f56c3-1bc2-49b9-b1d4-993210dfb62e" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_2d6f56c3-1bc2-49b9-b1d4-993210dfb62e" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('2d6f56c3-1bc2-49b9-b1d4-993210dfb62e',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_2d6f56c3-1bc2-49b9-b1d4-993210dfb62e" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Diagnostics;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Mvc;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> MvcDemo2.Models;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> MvcDemo2.Controllers
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> HomeController : Controller
    {
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> IActionResult Index()
        {
            </span><span style="color: #0000ff;">var</span> country=<span style="color: #0000ff;">new</span><span style="color: #000000;"> CountryViewModel();
            country.Country</span>=<span style="color: #800000;">"</span><span style="color: #800000;">US</span><span style="color: #800000;">"</span><span style="color: #000000;">;
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> View(country);
        }

        [HttpPost]
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> IActionResult Index(CountryViewModel model)
        {
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> View(model);
        }
        
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">HomeController </span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('e8633354-8ff8-46ce-adae-bdcec15dfa4b')"><img id="code_img_closed_e8633354-8ff8-46ce-adae-bdcec15dfa4b" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_e8633354-8ff8-46ce-adae-bdcec15dfa4b" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('e8633354-8ff8-46ce-adae-bdcec15dfa4b',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_e8633354-8ff8-46ce-adae-bdcec15dfa4b" class="cnblogs_code_hide">
<pre><span style="color: #000000;">@model CountryViewModel


</span>&lt;form method=<span style="color: #800000;">"</span><span style="color: #800000;">POST</span><span style="color: #800000;">"</span> asp-action=<span style="color: #800000;">"</span><span style="color: #800000;">Index</span><span style="color: #800000;">"</span>&gt;

    &lt;<span style="color: #0000ff;">select</span> asp-<span style="color: #0000ff;">for</span>=<span style="color: #800000;">"</span><span style="color: #800000;">Country</span><span style="color: #800000;">"</span> asp-items=<span style="color: #800000;">"</span><span style="color: #800000;">Model.Countries</span><span style="color: #800000;">"</span>&gt;&lt;/<span style="color: #0000ff;">select</span>&gt;

    &lt;input type=<span style="color: #800000;">"</span><span style="color: #800000;">submit</span><span style="color: #800000;">"</span> value=<span style="color: #800000;">"</span><span style="color: #800000;">提交</span><span style="color: #800000;">"</span> /&gt;
&lt;/form&gt;</pre>
</div>
<span class="cnblogs_code_collapse">Index</span></div>
<p>⑩枚举绑定</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('fe51137a-8a85-46ec-bab8-b3f64c215592')"><img id="code_img_closed_fe51137a-8a85-46ec-bab8-b3f64c215592" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_fe51137a-8a85-46ec-bab8-b3f64c215592" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('fe51137a-8a85-46ec-bab8-b3f64c215592',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_fe51137a-8a85-46ec-bab8-b3f64c215592" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">enum</span><span style="color: #000000;"> CountryEnum
        {
            [Display(Name </span>= <span style="color: #800000;">"</span><span style="color: #800000;">墨西哥合众国</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
            Mexico,
            [Display(Name </span>= <span style="color: #800000;">"</span><span style="color: #800000;">美国</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
            USA,
            Canada,
            France,
            Germany,
            Spain
        }</span></pre>
</div>
<span class="cnblogs_code_collapse">定义枚举</span></div>
<p>&nbsp;<span class="cnblogs_code">&lt;<span style="color: #0000ff;">select</span> asp-<span style="color: #0000ff;">for</span>=<span style="color: #800000;">"</span><span style="color: #800000;">Country</span><span style="color: #800000;">"</span> asp-items=<span style="color: #800000;">"</span><span style="color: #800000;">Html.GetEnumSelectList&lt;CountryEnum&gt;()</span><span style="color: #800000;">"</span>&gt;&lt;/<span style="color: #0000ff;">select</span>&gt;</span>&nbsp;</p>
<p>⑩选项分组</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('6854e1d1-0ab8-44de-a565-56821c409eb8')"><img id="code_img_closed_6854e1d1-0ab8-44de-a565-56821c409eb8" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_6854e1d1-0ab8-44de-a565-56821c409eb8" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('6854e1d1-0ab8-44de-a565-56821c409eb8',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_6854e1d1-0ab8-44de-a565-56821c409eb8" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.ComponentModel.DataAnnotations;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Mvc.Rendering;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> MvcDemo2.Models
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> CountryViewModel
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Country{<span style="color: #0000ff;">get</span>;<span style="color: #0000ff;">set</span><span style="color: #000000;">;}

        </span><span style="color: #0000ff;">public</span> List&lt;SelectListItem&gt; Countries {<span style="color: #0000ff;">get</span>;}=<span style="color: #0000ff;">new</span> List&lt;SelectListItem&gt;<span style="color: #000000;">(){
            </span><span style="color: #0000ff;">new</span> SelectListItem(){Value=<span style="color: #800000;">"</span><span style="color: #800000;">MX</span><span style="color: #800000;">"</span>,Text=<span style="color: #800000;">"</span><span style="color: #800000;">墨西哥</span><span style="color: #800000;">"</span>,Group=<span style="color: #0000ff;">new</span> SelectListGroup(){Name=<span style="color: #800000;">"</span><span style="color: #800000;">分组一</span><span style="color: #800000;">"</span><span style="color: #000000;">}},
            </span><span style="color: #0000ff;">new</span> SelectListItem(){Value=<span style="color: #800000;">"</span><span style="color: #800000;">CA</span><span style="color: #800000;">"</span>,Text=<span style="color: #800000;">"</span><span style="color: #800000;">加拿大</span><span style="color: #800000;">"</span>,Group=<span style="color: #0000ff;">new</span> SelectListGroup(){Name=<span style="color: #800000;">"</span><span style="color: #800000;">分组二</span><span style="color: #800000;">"</span><span style="color: #000000;">}},
            </span><span style="color: #0000ff;">new</span> SelectListItem(){Value=<span style="color: #800000;">"</span><span style="color: #800000;">US</span><span style="color: #800000;">"</span>,Text=<span style="color: #800000;">"</span><span style="color: #800000;">美国</span><span style="color: #800000;">"</span>,Group=<span style="color: #0000ff;">new</span> SelectListGroup(){Name=<span style="color: #800000;">"</span><span style="color: #800000;">分组三</span><span style="color: #800000;">"</span><span style="color: #000000;">}}
        };

        
    }
      
}</span></pre>
</div>
<span class="cnblogs_code_collapse">CountryViewModel</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('e8ab7ae0-a52b-4910-b3df-9890d2772b19')"><img id="code_img_closed_e8ab7ae0-a52b-4910-b3df-9890d2772b19" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_e8ab7ae0-a52b-4910-b3df-9890d2772b19" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('e8ab7ae0-a52b-4910-b3df-9890d2772b19',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_e8ab7ae0-a52b-4910-b3df-9890d2772b19" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Diagnostics;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Mvc;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> MvcDemo2.Models;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> MvcDemo2.Controllers
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> HomeController : Controller
    {
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> IActionResult Index()
        {
            </span><span style="color: #0000ff;">var</span> country=<span style="color: #0000ff;">new</span><span style="color: #000000;"> CountryViewModel();
            country.Country</span>=<span style="color: #800000;">"</span><span style="color: #800000;">US</span><span style="color: #800000;">"</span><span style="color: #000000;">;
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> View(country);
        }

        [HttpPost]
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> IActionResult Index(CountryViewModel model)
        {
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> View(model);
        }
        
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">HomeController</span></div>
<p>&nbsp;<span class="cnblogs_code">&lt;<span style="color: #0000ff;">select</span> asp-<span style="color: #0000ff;">for</span>=<span style="color: #800000;">"</span><span style="color: #800000;">Country</span><span style="color: #800000;">"</span> asp-items=<span style="color: #800000;">"</span><span style="color: #800000;">Model.Countries</span><span style="color: #800000;">"</span>&gt;&lt;/<span style="color: #0000ff;">select</span>&gt;</span>&nbsp;</p>
<p>&nbsp;<img src="https://images2018.cnblogs.com/blog/741594/201806/741594-20180601204149147-1627808971.png" alt="" width="79" height="119" /></p>
<p>&nbsp;⑩多重选择</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('3ea9e775-f310-420a-8b83-ab7b117d5c2f')"><img id="code_img_closed_3ea9e775-f310-420a-8b83-ab7b117d5c2f" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_3ea9e775-f310-420a-8b83-ab7b117d5c2f" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('3ea9e775-f310-420a-8b83-ab7b117d5c2f',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_3ea9e775-f310-420a-8b83-ab7b117d5c2f" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.ComponentModel.DataAnnotations;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Mvc.Rendering;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> MvcDemo2.Models
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> CountryViewModel
    {
        </span><span style="color: #0000ff;">public</span> IEnumerable&lt;<span style="color: #0000ff;">string</span>&gt; Countrys{<span style="color: #0000ff;">get</span>;<span style="color: #0000ff;">set</span><span style="color: #000000;">;}

        </span><span style="color: #0000ff;">public</span> List&lt;SelectListItem&gt; Countries {<span style="color: #0000ff;">get</span>;}=<span style="color: #0000ff;">new</span> List&lt;SelectListItem&gt;<span style="color: #000000;">(){
            </span><span style="color: #0000ff;">new</span> SelectListItem(){Value=<span style="color: #800000;">"</span><span style="color: #800000;">MX</span><span style="color: #800000;">"</span>,Text=<span style="color: #800000;">"</span><span style="color: #800000;">墨西哥</span><span style="color: #800000;">"</span><span style="color: #000000;">},
            </span><span style="color: #0000ff;">new</span> SelectListItem(){Value=<span style="color: #800000;">"</span><span style="color: #800000;">CA</span><span style="color: #800000;">"</span>,Text=<span style="color: #800000;">"</span><span style="color: #800000;">加拿大</span><span style="color: #800000;">"</span><span style="color: #000000;">},
            </span><span style="color: #0000ff;">new</span> SelectListItem(){Value=<span style="color: #800000;">"</span><span style="color: #800000;">US</span><span style="color: #800000;">"</span>,Text=<span style="color: #800000;">"</span><span style="color: #800000;">美国</span><span style="color: #800000;">"</span><span style="color: #000000;">}
        };

        
    }
      
}</span></pre>
</div>
<span class="cnblogs_code_collapse">CountryViewModel</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('3a6e28a3-026b-4179-8bbf-bbf480f4b36b')"><img id="code_img_closed_3a6e28a3-026b-4179-8bbf-bbf480f4b36b" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_3a6e28a3-026b-4179-8bbf-bbf480f4b36b" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('3a6e28a3-026b-4179-8bbf-bbf480f4b36b',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_3a6e28a3-026b-4179-8bbf-bbf480f4b36b" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Diagnostics;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Mvc;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> MvcDemo2.Models;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> MvcDemo2.Controllers
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> HomeController : Controller
    {
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> IActionResult Index()
        {
            </span><span style="color: #0000ff;">var</span> country=<span style="color: #0000ff;">new</span><span style="color: #000000;"> CountryViewModel();
            country.Countrys</span>=<span style="color: #0000ff;">new</span> []{<span style="color: #800000;">"</span><span style="color: #800000;">US</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">MX</span><span style="color: #800000;">"</span><span style="color: #000000;">};
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> View(country);
        }

        [HttpPost]
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> IActionResult Index(CountryViewModel model)
        {
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> View(model);
        }
        
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">HomeController</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('5aa5da02-b472-4053-8b67-a032b307a162')"><img id="code_img_closed_5aa5da02-b472-4053-8b67-a032b307a162" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_5aa5da02-b472-4053-8b67-a032b307a162" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('5aa5da02-b472-4053-8b67-a032b307a162',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_5aa5da02-b472-4053-8b67-a032b307a162" class="cnblogs_code_hide">
<pre><span style="color: #000000;">@model CountryViewModel


</span>&lt;form method=<span style="color: #800000;">"</span><span style="color: #800000;">POST</span><span style="color: #800000;">"</span> asp-action=<span style="color: #800000;">"</span><span style="color: #800000;">Index</span><span style="color: #800000;">"</span>&gt;

    &lt;<span style="color: #0000ff;">select</span> asp-<span style="color: #0000ff;">for</span>=<span style="color: #800000;">"</span><span style="color: #800000;">Countrys</span><span style="color: #800000;">"</span> asp-items=<span style="color: #800000;">"</span><span style="color: #800000;">Model.Countries</span><span style="color: #800000;">"</span>&gt;&lt;/<span style="color: #0000ff;">select</span>&gt;

    &lt;input type=<span style="color: #800000;">"</span><span style="color: #800000;">submit</span><span style="color: #800000;">"</span> value=<span style="color: #800000;">"</span><span style="color: #800000;">提交</span><span style="color: #800000;">"</span> /&gt;
&lt;/form&gt;</pre>
</div>
<span class="cnblogs_code_collapse">index</span></div>
<p>⑩无选定内容</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('dce83e62-b0da-477c-a582-65921334824e')"><img id="code_img_closed_dce83e62-b0da-477c-a582-65921334824e" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_dce83e62-b0da-477c-a582-65921334824e" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('dce83e62-b0da-477c-a582-65921334824e',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_dce83e62-b0da-477c-a582-65921334824e" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.ComponentModel.DataAnnotations;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Mvc.Rendering;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> MvcDemo2.Models
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> CountryViewModel
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Country{<span style="color: #0000ff;">get</span>;<span style="color: #0000ff;">set</span><span style="color: #000000;">;}

        </span><span style="color: #0000ff;">public</span> List&lt;SelectListItem&gt; Countries {<span style="color: #0000ff;">get</span>;}=<span style="color: #0000ff;">new</span> List&lt;SelectListItem&gt;<span style="color: #000000;">(){
            </span><span style="color: #0000ff;">new</span> SelectListItem(){Value=<span style="color: #800000;">"</span><span style="color: #800000;">MX</span><span style="color: #800000;">"</span>,Text=<span style="color: #800000;">"</span><span style="color: #800000;">墨西哥</span><span style="color: #800000;">"</span><span style="color: #000000;">},
            </span><span style="color: #0000ff;">new</span> SelectListItem(){Value=<span style="color: #800000;">"</span><span style="color: #800000;">CA</span><span style="color: #800000;">"</span>,Text=<span style="color: #800000;">"</span><span style="color: #800000;">加拿大</span><span style="color: #800000;">"</span><span style="color: #000000;">},
            </span><span style="color: #0000ff;">new</span> SelectListItem(){Value=<span style="color: #800000;">"</span><span style="color: #800000;">US</span><span style="color: #800000;">"</span>,Text=<span style="color: #800000;">"</span><span style="color: #800000;">美国</span><span style="color: #800000;">"</span><span style="color: #000000;">}
        };

        
    }
      
}</span></pre>
</div>
<span class="cnblogs_code_collapse">CountryViewModel</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('abfb9bd3-005b-4b56-9775-6ea0eab6af53')"><img id="code_img_closed_abfb9bd3-005b-4b56-9775-6ea0eab6af53" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_abfb9bd3-005b-4b56-9775-6ea0eab6af53" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('abfb9bd3-005b-4b56-9775-6ea0eab6af53',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_abfb9bd3-005b-4b56-9775-6ea0eab6af53" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Diagnostics;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Mvc;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> MvcDemo2.Models;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> MvcDemo2.Controllers
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> HomeController : Controller
    {
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> IActionResult Index()
        {
            </span><span style="color: #0000ff;">var</span> country=<span style="color: #0000ff;">new</span><span style="color: #000000;"> CountryViewModel();
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> View(country);
        }

        [HttpPost]
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> IActionResult Index(CountryViewModel model)
        {
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> View(model);
        }
        
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">HomeController</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('2dcab08b-fba3-427d-92f9-b3aeca893aaa')"><img id="code_img_closed_2dcab08b-fba3-427d-92f9-b3aeca893aaa" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_2dcab08b-fba3-427d-92f9-b3aeca893aaa" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('2dcab08b-fba3-427d-92f9-b3aeca893aaa',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_2dcab08b-fba3-427d-92f9-b3aeca893aaa" class="cnblogs_code_hide">
<pre><span style="color: #000000;">@model CountryViewModel


</span>&lt;form method=<span style="color: #800000;">"</span><span style="color: #800000;">POST</span><span style="color: #800000;">"</span> asp-action=<span style="color: #800000;">"</span><span style="color: #800000;">Index</span><span style="color: #800000;">"</span>&gt;

    &lt;<span style="color: #0000ff;">select</span> asp-<span style="color: #0000ff;">for</span>=<span style="color: #800000;">"</span><span style="color: #800000;">Country</span><span style="color: #800000;">"</span> asp-items=<span style="color: #800000;">"</span><span style="color: #800000;">Model.Countries</span><span style="color: #800000;">"</span>&gt;
        &lt;option value=<span style="color: #800000;">""</span>&gt;--none--&lt;/option&gt;
    &lt;/<span style="color: #0000ff;">select</span>&gt;

    &lt;input type=<span style="color: #800000;">"</span><span style="color: #800000;">submit</span><span style="color: #800000;">"</span> value=<span style="color: #800000;">"</span><span style="color: #800000;">提交</span><span style="color: #800000;">"</span> /&gt;
&lt;/form&gt;</pre>
</div>
<span class="cnblogs_code_collapse">index</span></div>
<p>&nbsp;</p>
<p><strong>4，内置标记帮助程序<a name="a44"></a></strong></p>
<p>①<span data-ttu-id="8bda7-145">asp-all-route-data</span></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('8f364db2-f47e-490d-977f-2dd32e60d362')"><img id="code_img_closed_8f364db2-f47e-490d-977f-2dd32e60d362" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_8f364db2-f47e-490d-977f-2dd32e60d362" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('8f364db2-f47e-490d-977f-2dd32e60d362',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_8f364db2-f47e-490d-977f-2dd32e60d362" class="cnblogs_code_hide">
<pre><span style="color: #000000;">@{
</span><span style="color: #0000ff;">var</span> parms = <span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">string</span>&gt;<span style="color: #000000;">
            {
                { </span><span style="color: #800000;">"</span><span style="color: #800000;">speakerId</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">11</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                { </span><span style="color: #800000;">"</span><span style="color: #800000;">currentYear</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">true</span><span style="color: #800000;">"</span><span style="color: #000000;"> }
            };
}

</span>&lt;a asp-route=<span style="color: #800000;">"</span><span style="color: #800000;">speakerevalscurrent</span><span style="color: #800000;">"</span><span style="color: #000000;">
   asp</span>-all-route-data=<span style="color: #800000;">"</span><span style="color: #800000;">parms</span><span style="color: #800000;">"</span>&gt;Speaker Evaluations&lt;/a&gt;</pre>
</div>
<span class="cnblogs_code_collapse">试图</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('7179043e-f7dd-4eaf-a17d-8e1dd45e53ad')"><img id="code_img_closed_7179043e-f7dd-4eaf-a17d-8e1dd45e53ad" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_7179043e-f7dd-4eaf-a17d-8e1dd45e53ad" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('7179043e-f7dd-4eaf-a17d-8e1dd45e53ad',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_7179043e-f7dd-4eaf-a17d-8e1dd45e53ad" class="cnblogs_code_hide">
<pre>&lt;a href=<span style="color: #800000;">"</span><span style="color: #800000;">/Speaker/EvaluationsCurrent?speakerId=11&amp;currentYear=true</span><span style="color: #800000;">"</span>&gt;Speaker Evaluations&lt;/a&gt;</pre>
</div>
<span class="cnblogs_code_collapse">前面的代码生成以下 HTML：</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('eb04ef95-1f42-49a6-809e-e2bf1ebd614e')"><img id="code_img_closed_eb04ef95-1f42-49a6-809e-e2bf1ebd614e" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_eb04ef95-1f42-49a6-809e-e2bf1ebd614e" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('eb04ef95-1f42-49a6-809e-e2bf1ebd614e',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_eb04ef95-1f42-49a6-809e-e2bf1ebd614e" class="cnblogs_code_hide">
<pre>[Route(<span style="color: #800000;">"</span><span style="color: #800000;">/Speaker/EvaluationsCurrent</span><span style="color: #800000;">"</span><span style="color: #000000;">,
       Name </span>= <span style="color: #800000;">"</span><span style="color: #800000;">speakerevalscurrent</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
</span><span style="color: #0000ff;">public</span><span style="color: #000000;"> IActionResult Evaluations(
    </span><span style="color: #0000ff;">int</span><span style="color: #000000;"> speakerId,
    </span><span style="color: #0000ff;">bool</span> currentYear) =&gt; View();</pre>
</div>
<span class="cnblogs_code_collapse">Controller</span></div>
<p>②<span data-ttu-id="8bda7-154">asp-fragment</span></p>
<p>可定义要追加到 URL 的 URL 片段</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('4323e13c-d863-4ed5-a4d1-1cc57e5f84f5')"><img id="code_img_closed_4323e13c-d863-4ed5-a4d1-1cc57e5f84f5" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_4323e13c-d863-4ed5-a4d1-1cc57e5f84f5" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('4323e13c-d863-4ed5-a4d1-1cc57e5f84f5',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_4323e13c-d863-4ed5-a4d1-1cc57e5f84f5" class="cnblogs_code_hide">
<pre>&lt;a asp-controller=<span style="color: #800000;">"</span><span style="color: #800000;">Speaker</span><span style="color: #800000;">"</span><span style="color: #000000;">
   asp</span>-action=<span style="color: #800000;">"</span><span style="color: #800000;">Evaluations</span><span style="color: #800000;">"</span><span style="color: #000000;">
   asp</span>-fragment=<span style="color: #800000;">"</span><span style="color: #800000;">SpeakerEvaluations</span><span style="color: #800000;">"</span>&gt;Speaker Evaluations&lt;/a&gt;</pre>
</div>
<span class="cnblogs_code_collapse">试图</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('bc2c306a-d615-47b6-b3ca-cd06e14972ad')"><img id="code_img_closed_bc2c306a-d615-47b6-b3ca-cd06e14972ad" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_bc2c306a-d615-47b6-b3ca-cd06e14972ad" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('bc2c306a-d615-47b6-b3ca-cd06e14972ad',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_bc2c306a-d615-47b6-b3ca-cd06e14972ad" class="cnblogs_code_hide">
<pre>&lt;a href=<span style="color: #800000;">"</span><span style="color: #800000;">/Speaker/Evaluations#SpeakerEvaluations</span><span style="color: #800000;">"</span>&gt;Speaker Evaluations&lt;/a&gt;</pre>
</div>
<span class="cnblogs_code_collapse">生成的 HTML：</span></div>
<p>③<span data-ttu-id="8bda7-161">asp-area</span></p>
<p>设置相应路由的区域名称</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('c296661b-d857-40d9-8459-5b1de811a332')"><img id="code_img_closed_c296661b-d857-40d9-8459-5b1de811a332" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_c296661b-d857-40d9-8459-5b1de811a332" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('c296661b-d857-40d9-8459-5b1de811a332',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_c296661b-d857-40d9-8459-5b1de811a332" class="cnblogs_code_hide">
<pre>&lt;a asp-area=<span style="color: #800000;">"</span><span style="color: #800000;">Blogs</span><span style="color: #800000;">"</span><span style="color: #000000;">
   asp</span>-controller=<span style="color: #800000;">"</span><span style="color: #800000;">Home</span><span style="color: #800000;">"</span><span style="color: #000000;">
   asp</span>-action=<span style="color: #800000;">"</span><span style="color: #800000;">AboutBlog</span><span style="color: #800000;">"</span>&gt;About Blog&lt;/a&gt;</pre>
</div>
<span class="cnblogs_code_collapse">试图</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('98f69a6d-1e72-4e33-ada4-f9f09fbc79ba')"><img id="code_img_closed_98f69a6d-1e72-4e33-ada4-f9f09fbc79ba" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_98f69a6d-1e72-4e33-ada4-f9f09fbc79ba" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('98f69a6d-1e72-4e33-ada4-f9f09fbc79ba',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_98f69a6d-1e72-4e33-ada4-f9f09fbc79ba" class="cnblogs_code_hide">
<pre>&lt;a href=<span style="color: #800000;">"</span><span style="color: #800000;">/Blogs/Home/AboutBlog</span><span style="color: #800000;">"</span>&gt;About Blog&lt;/a&gt;</pre>
</div>
<span class="cnblogs_code_collapse">生成的 HTML：</span></div>
<p>④<span data-ttu-id="8bda7-181">asp-protocol</span></p>
<p>在URL 中指定协议（比如<span class="Apple-converted-space">&nbsp;<code>https</code>）</span></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('e8ba791a-7d25-4d24-9cd8-39bbd4849436')"><img id="code_img_closed_e8ba791a-7d25-4d24-9cd8-39bbd4849436" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_e8ba791a-7d25-4d24-9cd8-39bbd4849436" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('e8ba791a-7d25-4d24-9cd8-39bbd4849436',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_e8ba791a-7d25-4d24-9cd8-39bbd4849436" class="cnblogs_code_hide">
<pre>&lt;a asp-protocol=<span style="color: #800000;">"</span><span style="color: #800000;">https</span><span style="color: #800000;">"</span><span style="color: #000000;">
   asp</span>-controller=<span style="color: #800000;">"</span><span style="color: #800000;">Home</span><span style="color: #800000;">"</span><span style="color: #000000;">
   asp</span>-action=<span style="color: #800000;">"</span><span style="color: #800000;">About</span><span style="color: #800000;">"</span>&gt;About&lt;/a&gt;</pre>
</div>
<span class="cnblogs_code_collapse">试图</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('70dcbced-a270-4fa5-9b15-19b26dde6d17')"><img id="code_img_closed_70dcbced-a270-4fa5-9b15-19b26dde6d17" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_70dcbced-a270-4fa5-9b15-19b26dde6d17" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('70dcbced-a270-4fa5-9b15-19b26dde6d17',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_70dcbced-a270-4fa5-9b15-19b26dde6d17" class="cnblogs_code_hide">
<pre>&lt;a href=<span style="color: #800000;">"</span><span style="color: #800000;">https://localhost/Home/About</span><span style="color: #800000;">"</span>&gt;About&lt;/a&gt;</pre>
</div>
<span class="cnblogs_code_collapse">生成的 HTML：</span></div>
<p>⑤<span data-ttu-id="8bda7-186">asp-host</span></p>
<p>在 URL 中指定主机名</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('7ead0617-2496-471b-85a2-68671faf733f')"><img id="code_img_closed_7ead0617-2496-471b-85a2-68671faf733f" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_7ead0617-2496-471b-85a2-68671faf733f" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('7ead0617-2496-471b-85a2-68671faf733f',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_7ead0617-2496-471b-85a2-68671faf733f" class="cnblogs_code_hide">
<pre>&lt;a asp-protocol=<span style="color: #800000;">"</span><span style="color: #800000;">https</span><span style="color: #800000;">"</span><span style="color: #000000;">
   asp</span>-host=<span style="color: #800000;">"</span><span style="color: #800000;">microsoft.com</span><span style="color: #800000;">"</span><span style="color: #000000;">
   asp</span>-controller=<span style="color: #800000;">"</span><span style="color: #800000;">Home</span><span style="color: #800000;">"</span><span style="color: #000000;">
   asp</span>-action=<span style="color: #800000;">"</span><span style="color: #800000;">About</span><span style="color: #800000;">"</span>&gt;About&lt;/a&gt;</pre>
</div>
<span class="cnblogs_code_collapse">试图</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('d4f3661f-4b33-43d9-818e-1a37a37ed2b9')"><img id="code_img_closed_d4f3661f-4b33-43d9-818e-1a37a37ed2b9" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_d4f3661f-4b33-43d9-818e-1a37a37ed2b9" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('d4f3661f-4b33-43d9-818e-1a37a37ed2b9',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_d4f3661f-4b33-43d9-818e-1a37a37ed2b9" class="cnblogs_code_hide">
<pre>&lt;a href=<span style="color: #800000;">"</span><span style="color: #800000;">https://microsoft.com/Home/About</span><span style="color: #800000;">"</span>&gt;About&lt;/a&gt;</pre>
</div>
<span class="cnblogs_code_collapse">生成的 HTML：</span></div>
<p>&nbsp;⑥缓存标记帮助程序</p>
<p>&nbsp;<span class="cnblogs_code">&lt;cache enabled=<span style="color: #800000;">"</span><span style="color: #800000;">true</span><span style="color: #800000;">"</span>&gt;@DateTime.Now&lt;/cache&gt;</span>&nbsp;</p>
<p>&nbsp;属性<span data-ttu-id="8c512-130">expires-after：设置过期时间</span></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('ee874ba4-0f1d-481b-8dac-b07514d5d897')"><img id="code_img_closed_ee874ba4-0f1d-481b-8dac-b07514d5d897" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_ee874ba4-0f1d-481b-8dac-b07514d5d897" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('ee874ba4-0f1d-481b-8dac-b07514d5d897',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_ee874ba4-0f1d-481b-8dac-b07514d5d897" class="cnblogs_code_hide">
<pre>&lt;cache expires-after=<span style="color: #800000;">"</span><span style="color: #800000;">@TimeSpan.FromSeconds(120)</span><span style="color: #800000;">"</span>&gt;<span style="color: #000000;">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</span>&lt;/cache&gt;</pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<p>&nbsp;属性<span data-ttu-id="8c512-137">expires-sliding：设置多久未被访问过期设置</span></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('85c9c73f-04f5-4cf2-a338-0a3d7b2b84c2')"><img id="code_img_closed_85c9c73f-04f5-4cf2-a338-0a3d7b2b84c2" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_85c9c73f-04f5-4cf2-a338-0a3d7b2b84c2" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('85c9c73f-04f5-4cf2-a338-0a3d7b2b84c2',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_85c9c73f-04f5-4cf2-a338-0a3d7b2b84c2" class="cnblogs_code_hide">
<pre>&lt;cache expires-sliding=<span style="color: #800000;">"</span><span style="color: #800000;">@TimeSpan.FromSeconds(60)</span><span style="color: #800000;">"</span>&gt;<span style="color: #000000;">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</span>&lt;/cache&gt;</pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<p>&nbsp;⑦环境标记帮助程序</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('937da429-3c25-40ec-8839-9d478f312f99')"><img id="code_img_closed_937da429-3c25-40ec-8839-9d478f312f99" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_937da429-3c25-40ec-8839-9d478f312f99" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('937da429-3c25-40ec-8839-9d478f312f99',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_937da429-3c25-40ec-8839-9d478f312f99" class="cnblogs_code_hide">
<pre>&lt;environment include=<span style="color: #800000;">"</span><span style="color: #800000;">Development</span><span style="color: #800000;">"</span>&gt;Development&lt;/environment&gt;
&lt;environment include=<span style="color: #800000;">"</span><span style="color: #800000;">Staging</span><span style="color: #800000;">"</span>&gt;Staging&lt;/environment&gt;
&lt;environment include=<span style="color: #800000;">"</span><span style="color: #800000;">Production</span><span style="color: #800000;">"</span>&gt;Production&lt;/environment&gt;</pre>
</div>
<span class="cnblogs_code_collapse">不同的环境显示不同的标签</span></div>
<p>⑧图像标记帮助程序</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('677b1f97-a1ac-4336-92b7-fcf4d4b47180')"><img id="code_img_closed_677b1f97-a1ac-4336-92b7-fcf4d4b47180" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_677b1f97-a1ac-4336-92b7-fcf4d4b47180" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('677b1f97-a1ac-4336-92b7-fcf4d4b47180',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_677b1f97-a1ac-4336-92b7-fcf4d4b47180" class="cnblogs_code_hide">
<pre>&lt;img src=<span style="color: #800000;">"</span><span style="color: #800000;">~/images/1.jpg</span><span style="color: #800000;">"</span>  asp-append-version=<span style="color: #800000;">"</span><span style="color: #800000;">true</span><span style="color: #800000;">"</span>/&gt;</pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<p><span data-ttu-id="70f18-112">asp-append-version：追加版本号</span></p>
<p>&nbsp;</p>
<p><strong>5，分部视图<a name="a45"></a></strong></p>
<div class="cnblogs_code">
<pre>@await Html.PartialAsync(<span style="color: #800000;">"</span><span style="color: #800000;">ViewName</span><span style="color: #800000;">"</span><span style="color: #000000;">)
@await Html.PartialAsync(</span><span style="color: #800000;">"</span><span style="color: #800000;">ViewName.cshtml</span><span style="color: #800000;">"</span><span style="color: #000000;">)
@await Html.PartialAsync(</span><span style="color: #800000;">"</span><span style="color: #800000;">~/Views/Folder/ViewName.cshtml</span><span style="color: #800000;">"</span><span style="color: #000000;">)
@await Html.PartialAsync(</span><span style="color: #800000;">"</span><span style="color: #800000;">/Views/Folder/ViewName.cshtml</span><span style="color: #800000;">"</span><span style="color: #000000;">)
@await Html.PartialAsync(</span><span style="color: #800000;">"</span><span style="color: #800000;">../Account/LoginPartial.cshtml</span><span style="color: #800000;">"</span>)</pre>
</div>
<div class="cnblogs_code" onclick="cnblogs_code_show('e30b7efa-f1eb-44c4-b2d8-7477d847d63f')"><img id="code_img_closed_e30b7efa-f1eb-44c4-b2d8-7477d847d63f" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_e30b7efa-f1eb-44c4-b2d8-7477d847d63f" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('e30b7efa-f1eb-44c4-b2d8-7477d847d63f',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_e30b7efa-f1eb-44c4-b2d8-7477d847d63f" class="cnblogs_code_hide">
<pre>@model <span style="color: #0000ff;">string</span><span style="color: #000000;">
姓名：@Model</span></pre>
</div>
<span class="cnblogs_code_collapse">分布页面Person.cshtml</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('2fd991d3-777b-4fbd-b3d6-7ead63c0c59e')"><img id="code_img_closed_2fd991d3-777b-4fbd-b3d6-7ead63c0c59e" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_2fd991d3-777b-4fbd-b3d6-7ead63c0c59e" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('2fd991d3-777b-4fbd-b3d6-7ead63c0c59e',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_2fd991d3-777b-4fbd-b3d6-7ead63c0c59e" class="cnblogs_code_hide">
<pre>@await Html.PartialAsync(<span style="color: #800000;">"</span><span style="color: #800000;">Person</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">Hunter</span><span style="color: #800000;">"</span>)</pre>
</div>
<span class="cnblogs_code_collapse">调用</span></div>
<p>&nbsp;</p>
<p><strong>6，视图组件<a name="a46"></a></strong></p>
<p>①添加 ViewComponent 类</p>
<p>在根目录新建一个ViewComponents文件夹，建ViewComponent类放在此文件夹中</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('2dd36d0e-8c09-4eac-8b1c-9f5487b0d298')"><img id="code_img_closed_2dd36d0e-8c09-4eac-8b1c-9f5487b0d298" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_2dd36d0e-8c09-4eac-8b1c-9f5487b0d298" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('2dd36d0e-8c09-4eac-8b1c-9f5487b0d298',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_2dd36d0e-8c09-4eac-8b1c-9f5487b0d298" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> MvcDemo2.Models;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Mvc;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> MvcDemo2.ViewComponents
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ProductListViewComponent:ViewComponent
    { 
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task&lt;IViewComponentResult&gt; InvokeAsync(<span style="color: #0000ff;">bool</span> ischecked,<span style="color: #0000ff;">string</span><span style="color: #000000;"> name)
        {
            </span><span style="color: #0000ff;">var</span> list=<span style="color: #0000ff;">new</span> List&lt;Product&gt;<span style="color: #000000;">(){
                </span><span style="color: #0000ff;">new</span> Product(){IsChecked=<span style="color: #0000ff;">true</span>,Name=<span style="color: #800000;">"</span><span style="color: #800000;">iphone x</span><span style="color: #800000;">"</span>,Price=<span style="color: #800080;">10000</span><span style="color: #000000;">},
                </span><span style="color: #0000ff;">new</span> Product(){IsChecked=<span style="color: #0000ff;">false</span>,Name=<span style="color: #800000;">"</span><span style="color: #800000;">iphone 8p</span><span style="color: #800000;">"</span>,Price=<span style="color: #800080;">6600</span><span style="color: #000000;">},
            };
             </span><span style="color: #0000ff;">var</span> data= list.Where(m=&gt;m.IsChecked==ischecked&amp;&amp;<span style="color: #000000;">m.Name.Contains(name));
             </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> View(data);          
        }
        
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">ProductListViewComponent</span></div>
<p><img src="https://images2018.cnblogs.com/blog/741594/201806/741594-20180602125819114-455852503.png" alt="" width="188" height="60" /></p>
<p>②创建视图组件 Razor 视图</p>
<p>&nbsp;创建 Views/Shared/Components 文件夹。 此文件夹 必须 命名为 Components</p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201806/741594-20180602125911289-728419729.png" alt="" width="186" height="78" /></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('88e3621b-8416-4227-9051-42bd03f2eeab')"><img id="code_img_closed_88e3621b-8416-4227-9051-42bd03f2eeab" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_88e3621b-8416-4227-9051-42bd03f2eeab" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('88e3621b-8416-4227-9051-42bd03f2eeab',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_88e3621b-8416-4227-9051-42bd03f2eeab" class="cnblogs_code_hide">
<pre>@model IEnumerable&lt;Product&gt;<span style="color: #000000;">

@foreach(</span><span style="color: #0000ff;">var</span> item <span style="color: #0000ff;">in</span><span style="color: #000000;"> Model)
{
    </span>&lt;p&gt;@item.Name&lt;/p&gt;<span style="color: #000000;">
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Default.cshtml</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('517ae9c9-d337-4061-93e5-27862631dd85')"><img id="code_img_closed_517ae9c9-d337-4061-93e5-27862631dd85" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_517ae9c9-d337-4061-93e5-27862631dd85" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('517ae9c9-d337-4061-93e5-27862631dd85',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_517ae9c9-d337-4061-93e5-27862631dd85" class="cnblogs_code_hide">
<pre>@await Component.InvokeAsync(<span style="color: #800000;">"</span><span style="color: #800000;">ProductList</span><span style="color: #800000;">"</span>,<span style="color: #0000ff;">new</span> {ischecked=<span style="color: #0000ff;">true</span>,name=<span style="color: #800000;">"</span><span style="color: #800000;">iphone</span><span style="color: #800000;">"</span>})</pre>
</div>
<span class="cnblogs_code_collapse">视图页面调用</span></div>
<p>&nbsp;</p>
<p><strong>7，上传文件<a name="a47"></a></strong></p>
<p>①使用模型绑定上传小文件</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('53d75175-137b-4619-a430-fdc684f51f59')"><img id="code_img_closed_53d75175-137b-4619-a430-fdc684f51f59" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_53d75175-137b-4619-a430-fdc684f51f59" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('53d75175-137b-4619-a430-fdc684f51f59',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_53d75175-137b-4619-a430-fdc684f51f59" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Http;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> MvcDemo2.Models
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> FileUpViewModel
    {
        </span><span style="color: #0000ff;">public</span> IEnumerable&lt;IFormFile&gt; files {<span style="color: #0000ff;">get</span>;<span style="color: #0000ff;">set</span><span style="color: #000000;">;}
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> name{<span style="color: #0000ff;">get</span>;<span style="color: #0000ff;">set</span><span style="color: #000000;">;}
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">FileUpViewModel</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('ea479718-6641-4ca6-8105-e90e2bfc1160')"><img id="code_img_closed_ea479718-6641-4ca6-8105-e90e2bfc1160" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_ea479718-6641-4ca6-8105-e90e2bfc1160" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('ea479718-6641-4ca6-8105-e90e2bfc1160',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_ea479718-6641-4ca6-8105-e90e2bfc1160" class="cnblogs_code_hide">
<pre>        <span style="color: #0000ff;">public</span><span style="color: #000000;"> IActionResult FileUp(FileUpViewModel model)
        {
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> View();
        }
        </span></pre>
</div>
<span class="cnblogs_code_collapse">Controller</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('2bc3fed4-7a82-44f0-b226-b26ebe3a0012')"><img id="code_img_closed_2bc3fed4-7a82-44f0-b226-b26ebe3a0012" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_2bc3fed4-7a82-44f0-b226-b26ebe3a0012" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('2bc3fed4-7a82-44f0-b226-b26ebe3a0012',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_2bc3fed4-7a82-44f0-b226-b26ebe3a0012" class="cnblogs_code_hide">
<pre>&lt;form asp-action=<span style="color: #800000;">"</span><span style="color: #800000;">FileUp</span><span style="color: #800000;">"</span> enctype=<span style="color: #800000;">"</span><span style="color: #800000;">multipart/form-data</span><span style="color: #800000;">"</span> method=<span style="color: #800000;">"</span><span style="color: #800000;">POST</span><span style="color: #800000;">"</span> role=<span style="color: #800000;">"</span><span style="color: #800000;">form</span><span style="color: #800000;">"</span>&gt;
    &lt;legend&gt;提交&lt;/legend&gt;

        &lt;input type=<span style="color: #800000;">"</span><span style="color: #800000;">file</span><span style="color: #800000;">"</span> name=<span style="color: #800000;">"</span><span style="color: #800000;">files</span><span style="color: #800000;">"</span> <span style="color: #0000ff;">class</span>=<span style="color: #800000;">"</span><span style="color: #800000;">form-control</span><span style="color: #800000;">"</span> multiple/&gt;
        &lt;input type=<span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span> name=<span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span> <span style="color: #0000ff;">class</span>=<span style="color: #800000;">"</span><span style="color: #800000;">form-control</span><span style="color: #800000;">"</span>/&gt;
    
    
    &lt;button type=<span style="color: #800000;">"</span><span style="color: #800000;">submit</span><span style="color: #800000;">"</span> <span style="color: #0000ff;">class</span>=<span style="color: #800000;">"</span><span style="color: #800000;">btn btn-primary</span><span style="color: #800000;">"</span>&gt;Submit&lt;/button&gt;
&lt;/form&gt;</pre>
</div>
<span class="cnblogs_code_collapse">View</span></div>
<p>&nbsp;</p>
<p><strong>8，筛选器<a name="a48"></a></strong></p>
<p><span data-ttu-id="cd6b0-123">每种筛选器类型都在筛选器管道中的不同阶段执行。</span></p>
<ul>
<li>
<p><span data-ttu-id="cd6b0-124"><a href="https://docs.microsoft.com/zh-cn/aspnet/core/mvc/controllers/filters?view=aspnetcore-2.1#authorization-filters" data-linktype="self-bookmark">授权筛选器</a>最先运行，用于确定是否已针对当前请求为当前用户授权。<span class="Apple-converted-space">&nbsp;<span data-ttu-id="cd6b0-125">如果请求未获授权，它们可以让管道短路。</span></span></span></p>
</li>
<li>
<p><span data-ttu-id="cd6b0-126"><a href="https://docs.microsoft.com/zh-cn/aspnet/core/mvc/controllers/filters?view=aspnetcore-2.1#resource-filters" data-linktype="self-bookmark">资源筛选器</a>是授权后最先处理请求的筛选器。<span class="Apple-converted-space">&nbsp;<span data-ttu-id="cd6b0-127">它们可以在筛选器管道的其余阶段运行之前以及管道的其余阶段完成之后运行代码。<span class="Apple-converted-space">&nbsp;<span data-ttu-id="cd6b0-128">出于性能方面的考虑，可以使用它们来实现缓存或以其他方式让筛选器管道短路。<span data-ttu-id="cd6b0-129">它们在模型绑定之前运行，所以可以影响模型绑定。</span></span></span></span></span></span></p>
</li>
<li>
<p><span data-ttu-id="cd6b0-130"><a href="https://docs.microsoft.com/zh-cn/aspnet/core/mvc/controllers/filters?view=aspnetcore-2.1#action-filters" data-linktype="self-bookmark">操作筛选器</a>可以在调用单个操作方法之前和之后立即运行代码。<span class="Apple-converted-space">&nbsp;<span data-ttu-id="cd6b0-131">它们可用于处理传入某个操作的参数以及从该操作返回的结果。</span></span></span></p>
</li>
<li>
<p><span data-ttu-id="cd6b0-132"><a href="https://docs.microsoft.com/zh-cn/aspnet/core/mvc/controllers/filters?view=aspnetcore-2.1#exception-filters" data-linktype="self-bookmark">异常筛选器</a>用于在向响应正文写入任何内容之前，对未经处理的异常应用全局策略。</span></p>
</li>
<li>
<p><span data-ttu-id="cd6b0-133"><a href="https://docs.microsoft.com/zh-cn/aspnet/core/mvc/controllers/filters?view=aspnetcore-2.1#result-filters" data-linktype="self-bookmark">结果筛选器</a>可以在执行单个操作结果之前和之后立即运行代码。<span class="Apple-converted-space">&nbsp;<span data-ttu-id="cd6b0-134">仅当操作方法成功执行时，它们才会运行。<span data-ttu-id="cd6b0-135">对于必须围绕视图或格式化程序的执行的逻辑，它们很有用。</span></span></span></span></p>
</li>
</ul>
<p>下图展示了这些筛选器类型在筛选器管道中的交互方式：</p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201806/741594-20180602193454037-2121746650.png" alt="" width="364" height="288" /></p>
<p>①筛选器通过不同的接口定义支持同步和异步实现</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('46d70577-b00d-4079-8690-533db7858137')"><img id="code_img_closed_46d70577-b00d-4079-8690-533db7858137" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_46d70577-b00d-4079-8690-533db7858137" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('46d70577-b00d-4079-8690-533db7858137',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_46d70577-b00d-4079-8690-533db7858137" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> FiltersSample.Helper;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Mvc.Filters;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> FiltersSample.Filters
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SampleActionFilter : IActionFilter
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> OnActionExecuting(ActionExecutingContext context)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> do something before the action executes</span>
<span style="color: #000000;">        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> OnActionExecuted(ActionExecutedContext context)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> do something after the action executes</span>
<span style="color: #000000;">        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">同步实现</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('21fe04bf-59c7-4a1b-9d6d-1473540b2636')"><img id="code_img_closed_21fe04bf-59c7-4a1b-9d6d-1473540b2636" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_21fe04bf-59c7-4a1b-9d6d-1473540b2636" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('21fe04bf-59c7-4a1b-9d6d-1473540b2636',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_21fe04bf-59c7-4a1b-9d6d-1473540b2636" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Mvc.Filters;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> FiltersSample.Filters
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SampleAsyncActionFilter : IAsyncActionFilter
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span><span style="color: #000000;"> Task OnActionExecutionAsync(
            ActionExecutingContext context,
            ActionExecutionDelegate next)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> 在行动执行之前做一些事情</span>
            <span style="color: #0000ff;">var</span> resultContext = <span style="color: #0000ff;">await</span><span style="color: #000000;"> next();
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> 在执行操作后执行某些操作; resultContext.Result将被设置</span>
<span style="color: #000000;">        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">异步实现</span></div>
<p>②添加为全局筛选器</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('93c72c37-54e8-42b8-bcab-5311280ad0c8')"><img id="code_img_closed_93c72c37-54e8-42b8-bcab-5311280ad0c8" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_93c72c37-54e8-42b8-bcab-5311280ad0c8" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('93c72c37-54e8-42b8-bcab-5311280ad0c8',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_93c72c37-54e8-42b8-bcab-5311280ad0c8" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> ConfigureServices(IServiceCollection services)
{
    services.AddMvc(options </span>=&gt;<span style="color: #000000;">
    {
        options.Filters.Add(</span><span style="color: #0000ff;">new</span> AddHeaderAttribute(<span style="color: #800000;">"</span><span style="color: #800000;">GlobalAddHeader</span><span style="color: #800000;">"</span><span style="color: #000000;">, 
            </span><span style="color: #800000;">"</span><span style="color: #800000;">Result filter added to MvcOptions.Filters</span><span style="color: #800000;">"</span>)); <span style="color: #008000;">//</span><span style="color: #008000;"> an instance</span>
        options.Filters.Add(<span style="color: #0000ff;">typeof</span>(SampleActionFilter)); <span style="color: #008000;">//</span><span style="color: #008000;"> by type</span>
        options.Filters.Add(<span style="color: #0000ff;">new</span> SampleGlobalActionFilter()); <span style="color: #008000;">//</span><span style="color: #008000;"> an instance</span>
<span style="color: #000000;">    });

    services.AddScoped</span>&lt;AddHeaderFilterWithDi&gt;<span style="color: #000000;">();
}</span></pre>
</div>
<span class="cnblogs_code_collapse">ConfigureServices</span></div>
<p>③<span data-ttu-id="cd6b0-243">取消和设置短路</span></p>
<p>&nbsp;<span data-ttu-id="cd6b0-244">通过设置提供给筛选器方法的<span class="Apple-converted-space">&nbsp;<code>context</code><span class="Apple-converted-space">&nbsp;参数上的<span class="Apple-converted-space">&nbsp;<code>Result</code><span class="Apple-converted-space">&nbsp;属性，可以在筛选器管道的任意位置设置短路。<span class="Apple-converted-space">&nbsp;<span data-ttu-id="cd6b0-245">例如，以下资源筛选器将阻止执行管道的其余阶段</span></span></span></span></span></span></span></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('e6b2a5b9-939d-4233-a2b4-5e56e103e951')"><img id="code_img_closed_e6b2a5b9-939d-4233-a2b4-5e56e103e951" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_e6b2a5b9-939d-4233-a2b4-5e56e103e951" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('e6b2a5b9-939d-4233-a2b4-5e56e103e951',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_e6b2a5b9-939d-4233-a2b4-5e56e103e951" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Mvc;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Mvc.Filters;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> FiltersSample.Filters
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ShortCircuitingResourceFilterAttribute : Attribute,
            IResourceFilter
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> OnResourceExecuting(ResourceExecutingContext context)
        {
            context.Result </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> ContentResult()
            {
                Content </span>= <span style="color: #800000;">"</span><span style="color: #800000;">Resource unavailable - header should not be set</span><span style="color: #800000;">"</span><span style="color: #000000;">
            };
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> OnResourceExecuted(ResourceExecutedContext context)
        {
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">ShortCircuitingResourceFilterAttribute </span></div>
<p>&nbsp;</p>
<p><strong><a name="a49"></a>9，绑定与压缩</strong></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('fc4249ae-fb1b-4b06-9ed0-a57674de8d67')"><img id="code_img_closed_fc4249ae-fb1b-4b06-9ed0-a57674de8d67" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_fc4249ae-fb1b-4b06-9ed0-a57674de8d67" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('fc4249ae-fb1b-4b06-9ed0-a57674de8d67',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_fc4249ae-fb1b-4b06-9ed0-a57674de8d67" class="cnblogs_code_hide">
<pre><span style="color: #000000;">[
  {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">outputFileName</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">wwwroot/css/site.min.css</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">inputFiles</span><span style="color: #800000;">"</span><span style="color: #000000;">: [
      </span><span style="color: #800000;">"</span><span style="color: #800000;">wwwroot/css/site.css</span><span style="color: #800000;">"</span><span style="color: #000000;">
    ]
  },
  {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">outputFileName</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">wwwroot/js/site.min.js</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">inputFiles</span><span style="color: #800000;">"</span><span style="color: #000000;">: [
      </span><span style="color: #800000;">"</span><span style="color: #800000;">wwwroot/js/site.js</span><span style="color: #800000;">"</span><span style="color: #000000;">
    ],
    </span><span style="color: #800000;">"</span><span style="color: #800000;">minify</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">enabled</span><span style="color: #800000;">"</span>: <span style="color: #0000ff;">true</span><span style="color: #000000;">,
      </span><span style="color: #800000;">"</span><span style="color: #800000;">renameLocals</span><span style="color: #800000;">"</span>: <span style="color: #0000ff;">true</span><span style="color: #000000;">
    },
    </span><span style="color: #800000;">"</span><span style="color: #800000;">sourceMap</span><span style="color: #800000;">"</span>: <span style="color: #0000ff;">false</span><span style="color: #000000;">
  }
]</span></pre>
</div>
<span class="cnblogs_code_collapse">bundleconfig.json</span></div>
<div>outputFileName：要输出的捆绑文件名称。可以包含中的相对路径<em>bundleconfig.json</em>文件（必填）</div>
<div>
<div>inputFiles：<span data-ttu-id="51c52-165">要将捆绑在一起的文件的数组。&nbsp;<span data-ttu-id="51c52-166">这些是配置文件的相对路径（可选）</span></span></div>
<div>
<div>minify：输出类型缩减选项</div>
<div>
<div>sourceMap：指示是否生成捆绑的文件的源映射的标志</div>
</div>
</div>
</div>
<p>①需要引用：&nbsp;<span class="cnblogs_code">&lt;DotNetCliToolReference Include=<span style="color: #800000;">"</span><span style="color: #800000;">BundlerMinifier.Core</span><span style="color: #800000;">"</span> Version=<span style="color: #800000;">"</span><span style="color: #800000;">2.6.362</span><span style="color: #800000;">"</span> /&gt;</span>&nbsp;&nbsp;</p>
<p>②执行命令：&nbsp;&nbsp;<span class="cnblogs_code">dotnet bundle</span>&nbsp;会合并并压缩inputFiles里的文件到outputFileName</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a5"></a>五、Model</span></strong></span></p>
<p><strong>1，数据注解</strong></p>
<p>①DisplayFormat</p>
<div class="cnblogs_code">
<pre>[DisplayFormat(DataFormatString = <span style="color: #800000;">"</span><span style="color: #800000;">{0:yyyy-MM-dd}</span><span style="color: #800000;">"</span>, ApplyFormatInEditMode = <span style="color: #0000ff;">true</span>)]</pre>
</div>
<p>②<span data-ttu-id="b7998-165">Column&nbsp;</span></p>
<div class="cnblogs_code">
<pre> [Column(<span style="color: #800000;">"</span><span style="color: #800000;">FirstName</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
 </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> FirstMidName { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span>; }</pre>
</div>
<p>实体属性表字段映射</p>
<p>&nbsp;</p>
<p><strong>2，DatabaseGenerated标记主键</strong></p>
<div class="cnblogs_code"><img id="code_img_closed_56fcecec-665e-472f-8c2c-1f1ab761f227" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><span class="cnblogs_code_collapse">实体</span></div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a6"></a>六、配置</span></strong></p>
<p>&nbsp;</p>