<p>1，安装EF Core</p>
<p>在.csproj中添加一下配置，用于使用dotnet ef 命令</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('9f3a6ec1-e1c8-4846-b81a-e8276660ea41')"><img id="code_img_closed_9f3a6ec1-e1c8-4846-b81a-e8276660ea41" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_9f3a6ec1-e1c8-4846-b81a-e8276660ea41" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('9f3a6ec1-e1c8-4846-b81a-e8276660ea41',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_9f3a6ec1-e1c8-4846-b81a-e8276660ea41" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ItemGroup</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">DotNetCliToolReference </span><span style="color: #ff0000;">Include</span><span style="color: #0000ff;">="Microsoft.EntityFrameworkCore.Tools.DotNet"</span><span style="color: #ff0000;"> Version</span><span style="color: #0000ff;">="2.0.0"</span> <span style="color: #0000ff;">/&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">ItemGroup</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<span class="cnblogs_code_collapse">DotNetCliToolReference </span></div>
<p>2， 配置文件</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('552154bd-da2d-45a6-abeb-5028e9a1b275')"><img id="code_img_closed_552154bd-da2d-45a6-abeb-5028e9a1b275" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_552154bd-da2d-45a6-abeb-5028e9a1b275" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('552154bd-da2d-45a6-abeb-5028e9a1b275',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_552154bd-da2d-45a6-abeb-5028e9a1b275" class="cnblogs_code_hide">
<pre>  <span style="color: #800000;">"</span><span style="color: #800000;">ConnectionStrings</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">DefaultConnection</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">Server=(localdb)\\mssqllocaldb;Database=aspnet-mvcDemo2;Trusted_Connection=True;MultipleActiveResultSets=true</span><span style="color: #800000;">"</span><span style="color: #000000;">
  }</span></pre>
</div>
<span class="cnblogs_code_collapse">a使用本地数据库</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('09a229e3-08a2-41af-b2ca-79d75bd18196')"><img id="code_img_closed_09a229e3-08a2-41af-b2ca-79d75bd18196" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_09a229e3-08a2-41af-b2ca-79d75bd18196" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('09a229e3-08a2-41af-b2ca-79d75bd18196',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_09a229e3-08a2-41af-b2ca-79d75bd18196" class="cnblogs_code_hide">
<pre>  <span style="color: #800000;">"</span><span style="color: #800000;">ConnectionStrings</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">MysqlConnection</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">server=127.0.0.1;port=3306;database=demo1;userid=root;password=123456;</span><span style="color: #800000;">"</span><span style="color: #000000;">
  }</span></pre>
</div>
<span class="cnblogs_code_collapse">mysql简单连接</span></div>
<p>&nbsp;</p>
<p>3，注册服务</p>
<div class="cnblogs_code">
<pre>            services.AddDbContext&lt;MyDbContext&gt;(options=&gt;<span style="color: #000000;">{
                options.UseMySql(Configuration.GetConnectionString(</span><span style="color: #800000;">"</span><span style="color: #800000;">MysqlConnection</span><span style="color: #800000;">"</span><span style="color: #000000;">));
            });</span></pre>
</div>
<p>注意asp.net core2.1连接ef使用MySql.Data.EntityFrameworkCore连接有问题。需要使用Pomelo.EntityFrameworkCore.MySql&nbsp;2.1.0</p>
<p>&nbsp;</p>