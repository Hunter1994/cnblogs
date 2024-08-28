<p><a href="#a1">1，命令</a></p>
<p><a href="#a2">2，模板</a></p>
<p><a href="#a3">3，更换启动浏览器</a></p>
<p><a href="#a4">4，vscode使用nuget</a></p>
<p><a href="#a5">5，使用ef migration</a></p>
<p><a href="#a6">6，配置.net core的工作目录</a></p>
<p><a href="#a7">7，使用dotnet ef migrations命令</a></p>
<p><a href="#a8">8，指定migration生成的目录</a></p>
<p><a href="#a9">9，vscode使用Bower</a></p>
<p><a href="#a10">10，引用项目&nbsp;</a></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p><a name="a1"></a>1，命令</p>
<p>&nbsp;<span class="cnblogs_code">dotnet <span style="color: #0000ff;">new</span> --help</span>&nbsp;查询命令帮助</p>
<p>&nbsp;<span class="cnblogs_code">D:\github\test2&gt;dotnet run</span>&nbsp;启动web程序</p>
<p>&nbsp;<span class="cnblogs_code">dotnet build</span>&nbsp;编译代码</p>
<p>&nbsp;<span class="cnblogs_code">dotnet restore</span>&nbsp;还原包</p>
<p>&nbsp;<span class="cnblogs_code">dotnet publish</span>&nbsp;发布项目</p>
<p>&nbsp;</p>
<p><a name="a2"></a>2，模板</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('d5112601-62f7-49e4-b0c0-9842f38a4644')"><img id="code_img_closed_d5112601-62f7-49e4-b0c0-9842f38a4644" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_d5112601-62f7-49e4-b0c0-9842f38a4644" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('d5112601-62f7-49e4-b0c0-9842f38a4644',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_d5112601-62f7-49e4-b0c0-9842f38a4644" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Diagnostics;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Mvc;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> test3.Models;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> test3.Controllers
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> HomeController : Controller
    {
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> IActionResult Index()
        {
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> View();
        }

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> IActionResult About()
        {
            ViewData[</span><span style="color: #800000;">"</span><span style="color: #800000;">Message</span><span style="color: #800000;">"</span>] = <span style="color: #800000;">"</span><span style="color: #800000;">Your application description page.</span><span style="color: #800000;">"</span><span style="color: #000000;">;

            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> View();
        }

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> IActionResult Contact()
        {
            ViewData[</span><span style="color: #800000;">"</span><span style="color: #800000;">Message</span><span style="color: #800000;">"</span>] = <span style="color: #800000;">"</span><span style="color: #800000;">Your contact page.</span><span style="color: #800000;">"</span><span style="color: #000000;">;

            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> View();
        }

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> IActionResult Error()
        {
            </span><span style="color: #0000ff;">return</span> View(<span style="color: #0000ff;">new</span> ErrorViewModel { RequestId = Activity.Current?.Id ??<span style="color: #000000;"> HttpContext.TraceIdentifier });
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Controller模板</span></div>
<p>&nbsp;</p>
<p><a name="a3"></a>3，更换启动浏览器</p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201805/741594-20180505152211421-1402312013.png" alt="" width="532" height="278" /></p>
<p>windows下启动浏览器命令：&nbsp;<span class="cnblogs_code">C:\Windows\System32&gt;cmd.exe /C start http:<span style="color: #008000;">//</span><span style="color: #008000;">localhost:5000/api/values</span></span>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('b7f8ae9a-f62b-442c-bff4-887550232ff8')"><img id="code_img_closed_b7f8ae9a-f62b-442c-bff4-887550232ff8" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_b7f8ae9a-f62b-442c-bff4-887550232ff8" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('b7f8ae9a-f62b-442c-bff4-887550232ff8',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_b7f8ae9a-f62b-442c-bff4-887550232ff8" class="cnblogs_code_hide">
<pre><span style="color: #800000;">"</span><span style="color: #800000;">launchBrowser</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
                </span><span style="color: #800000;">"</span><span style="color: #800000;">enabled</span><span style="color: #800000;">"</span>: <span style="color: #0000ff;">true</span><span style="color: #000000;">,
                </span><span style="color: #800000;">"</span><span style="color: #800000;">args</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">${auto-detect-url}</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                </span><span style="color: #800000;">"</span><span style="color: #800000;">windows</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
                    </span><span style="color: #800000;">"</span><span style="color: #800000;">command</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">C:\\Users\\Hunter\\AppData\\Local\\Google\\Chrome\\Application\\chrome.exe</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    </span><span style="color: #800000;">"</span><span style="color: #800000;">args</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">${auto-detect-url}</span><span style="color: #800000;">"</span><span style="color: #000000;">
                },
                </span><span style="color: #800000;">"</span><span style="color: #800000;">osx</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
                    </span><span style="color: #800000;">"</span><span style="color: #800000;">command</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">open</span><span style="color: #800000;">"</span><span style="color: #000000;">
                },
                </span><span style="color: #800000;">"</span><span style="color: #800000;">linux</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
                    </span><span style="color: #800000;">"</span><span style="color: #800000;">command</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">xdg-open</span><span style="color: #800000;">"</span><span style="color: #000000;">
                }
            },</span></pre>
</div>
<span class="cnblogs_code_collapse">更新配置</span></div>
<p>&nbsp;</p>
<p><a name="a4"></a>4，vscode使用nuget</p>
<p>①安装nuget</p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201805/741594-20180505165550555-79704961.png" alt="" width="305" height="273" /></p>
<p>②&nbsp;<span class="cnblogs_code">ctrl</span>&nbsp;+&nbsp;<span class="cnblogs_code">shift</span>&nbsp;+P 选择nuget，然后输入包名称回车下载</p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201805/741594-20180505165616855-516793393.png" alt="" width="666" height="99" /></p>
<p>③包版本变更</p>
<p>打开.csproj文件，直接更改PackageReference下的Version</p>
<p>然后dotnet restore</p>
<p>&nbsp;</p>
<p><a name="a5"></a>5，使用ef migration</p>
<p>dotnet ef migrations add initialCreate　　Add-Migration【添加更新实体】</p>
<p>dotnet ef database update　　Update-Database【向数据库更新】</p>
<p>dotnet ef migrations remove　　Remove-Migration【删除最后一个migration文件，前提是该migration文件为update到数据库】</p>
<p>dotnet ef database update LastGoodMigration Update-Database LastGoodMigration【回滚到指定的migration文件。不会删除migration文件。如果不需要migration文件可以通过dotnet ef migrations remove删除掉】</p>
<p>dotnet ef migrations script　　Script-Migration【打印出数据库变更脚本】</p>
<p>&nbsp;</p>
<p><a name="a6"></a>6，配置.net core的工作目录</p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201805/741594-20180509174401766-1239834638.png" alt="" /></p>
<div>program：需要执行的dll</div>
<div>
<div>cwd：被调试程序的工作目录</div>
</div>
<p>&nbsp;</p>
<p><a name="a7"></a>7，使用dotnet ef migrations命令</p>
<p>需要在工程文件中加入</p>
<p>&nbsp;<span class="cnblogs_code">&lt;PackageReference Include=<span style="color: #800000;">"</span><span style="color: #800000;">Microsoft.EntityFrameworkCore.Tools</span><span style="color: #800000;">"</span> Version=<span style="color: #800000;">"</span><span style="color: #800000;">2.0.2</span><span style="color: #800000;">"</span>/&gt;</span>&nbsp;和&nbsp;<span class="cnblogs_code">&lt;DotNetCliToolReference Include=<span style="color: #800000;">"</span><span style="color: #800000;">Microsoft.EntityFrameworkCore.Tools.DotNet</span><span style="color: #800000;">"</span> Version=<span style="color: #800000;">"</span><span style="color: #800000;">2.0.2</span><span style="color: #800000;">"</span>/&gt;</span>&nbsp;</p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201805/741594-20180510111827443-1094200560.png" alt="" width="572" height="203" /></p>
<p>&nbsp;</p>
<p><a name="a8"></a>8，指定migration生成的目录</p>
<p>&nbsp;<span class="cnblogs_code">dotnet ef migrations add init -o Data/Migrations</span>&nbsp;</p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201805/741594-20180510111943762-1299255211.png" alt="" width="237" height="259" /></p>
<p>以后再添加不用使用&nbsp;<span class="cnblogs_code"> -o Data/Migrations</span>&nbsp;直接会添加在Data/Migrations文件夹下</p>
<p>&nbsp;</p>
<p><a name="a9"></a>9，vscode使用Bower</p>
<p>①vscode安装Bower扩展</p>
<p>&nbsp;<span class="cnblogs_code">Ctrl</span>&nbsp;+&nbsp;<span class="cnblogs_code">Shift</span>&nbsp;+&nbsp;<span class="cnblogs_code"> p</span>&nbsp;就可以使用Bower了</p>
<p>②在项目中添加.bowerrc文件指定包安装路径</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">{
    </span><span style="color: #800000;">"</span><span style="color: #800000;">directory</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">wwwroot/lib</span><span style="color: #800000;">"</span><span style="color: #000000;">
}</span></pre>
</div>
<p>③添加bower.json文件</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">MvcDemo2</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">private</span><span style="color: #800000;">"</span>: <span style="color: #0000ff;">true</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">dependencies</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">jquery</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">3.1.1</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">bootstrap</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">3.3.7</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">zTree</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">3.5.33</span><span style="color: #800000;">"</span><span style="color: #000000;">
  }
}</span></pre>
</div>
<p>&nbsp;</p>
<p>10，引用项目<a name="a10"></a></p>
<div class="cnblogs_code">
<div>&lt;ItemGroup&gt;</div>
<div>&lt;ProjectReference Include="..\IdentityServer4\IdentityServer4.csproj" /&gt;</div>
<div>&lt;/ItemGroup&gt;</div>
</div>
<p>&nbsp;</p>