<p><a href="#a1"><strong>一、配置管理</strong></a></p>
<p><strong><strong><a href="#a2">二、管道</a></strong></strong></p>
<p><a href="#a3"><strong><strong>三、认证与授权</strong></strong></a></p>
<p><a href="#a4"><strong>四、MVCDemo</strong></a></p>
<p><a href="#a5"><strong>五、IdentityServer4</strong></a></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff; font-size: 18pt;"><strong><a name="a1"></a>一、配置管理</strong></span></p>
<p>1，读取内存配置</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('38fa0e4d-1b7b-489a-9f2f-6136ec1fa739')"><img id="code_img_closed_38fa0e4d-1b7b-489a-9f2f-6136ec1fa739" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_38fa0e4d-1b7b-489a-9f2f-6136ec1fa739" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('38fa0e4d-1b7b-489a-9f2f-6136ec1fa739',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_38fa0e4d-1b7b-489a-9f2f-6136ec1fa739" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Configuration;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ConsoleApp1
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {

            Dictionary</span>&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">string</span>&gt; dic = <span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">string</span>&gt;<span style="color: #000000;">() {
                { </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">},
                { </span><span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">10</span><span style="color: #800000;">"</span><span style="color: #000000;">}
            };

            </span><span style="color: #0000ff;">var</span> builder = <span style="color: #0000ff;">new</span><span style="color: #000000;"> ConfigurationBuilder()
                .AddInMemoryCollection(dic)</span><span style="color: #008000;">//</span><span style="color: #008000;">当age没有值的时候使用dic里面的值</span>
<span style="color: #000000;">                .AddCommandLine(args);

            </span><span style="color: #0000ff;">var</span> configuration =<span style="color: #000000;"> builder.Build();

            Console.WriteLine($</span><span style="color: #800000;">"</span><span style="color: #800000;">name:{configuration[</span><span style="color: #800000;">"</span>name<span style="color: #800000;">"</span><span style="color: #800000;">]}</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            Console.WriteLine($</span><span style="color: #800000;">"</span><span style="color: #800000;">age:{configuration[</span><span style="color: #800000;">"</span>age<span style="color: #800000;">"</span><span style="color: #800000;">]}</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            Console.ReadKey();
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">demo</span></div>
<p><img src="https://images2018.cnblogs.com/blog/741594/201805/741594-20180503193355116-2075826337.png" alt="" width="846" height="59" /></p>
<p>2，读取json文件</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('e58db543-7ca4-4ead-9382-efbe65a5ca5d')"><img id="code_img_closed_e58db543-7ca4-4ead-9382-efbe65a5ca5d" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_e58db543-7ca4-4ead-9382-efbe65a5ca5d" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('e58db543-7ca4-4ead-9382-efbe65a5ca5d',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_e58db543-7ca4-4ead-9382-efbe65a5ca5d" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Configuration;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ConsoleApp1
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #0000ff;">var</span> builder = <span style="color: #0000ff;">new</span><span style="color: #000000;"> ConfigurationBuilder()
                .AddJsonFile(</span><span style="color: #800000;">"</span><span style="color: #800000;">class.json</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            </span><span style="color: #0000ff;">var</span> configuration =<span style="color: #000000;"> builder.Build();

            Console.WriteLine($</span><span style="color: #800000;">"</span><span style="color: #800000;">no:{configuration[</span><span style="color: #800000;">"</span>no<span style="color: #800000;">"</span><span style="color: #800000;">]}</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            Console.WriteLine($</span><span style="color: #800000;">"</span><span style="color: #800000;">name:{configuration[</span><span style="color: #800000;">"</span>name<span style="color: #800000;">"</span><span style="color: #800000;">]}</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">student:</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            Console.WriteLine($</span><span style="color: #800000;">"</span><span style="color: #800000;">no:{configuration[</span><span style="color: #800000;">"</span>student:<span style="color: #800080;">0</span>:no<span style="color: #800000;">"</span><span style="color: #800000;">]},name:{configuration[</span><span style="color: #800000;">"</span>student:<span style="color: #800080;">0</span>:name<span style="color: #800000;">"</span><span style="color: #800000;">]}</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            Console.WriteLine($</span><span style="color: #800000;">"</span><span style="color: #800000;">no:{configuration[</span><span style="color: #800000;">"</span>student:<span style="color: #800080;">1</span>:no<span style="color: #800000;">"</span><span style="color: #800000;">]},name:{configuration[</span><span style="color: #800000;">"</span>student:<span style="color: #800080;">1</span>:name<span style="color: #800000;">"</span><span style="color: #800000;">]}</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            Console.ReadKey();
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">demo</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('ddc3ae55-fccd-4c92-b85b-03a017ba348d')"><img id="code_img_closed_ddc3ae55-fccd-4c92-b85b-03a017ba348d" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_ddc3ae55-fccd-4c92-b85b-03a017ba348d" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('ddc3ae55-fccd-4c92-b85b-03a017ba348d',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_ddc3ae55-fccd-4c92-b85b-03a017ba348d" class="cnblogs_code_hide">
<pre><span style="color: #000000;">{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">no</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">1</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">asp.net core</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">student</span><span style="color: #800000;">"</span><span style="color: #000000;">: [
    {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">no</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">1</span><span style="color: #800000;">"</span><span style="color: #000000;">,
      </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">张三</span><span style="color: #800000;">"</span><span style="color: #000000;">
    },
    {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">no</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">2</span><span style="color: #800000;">"</span><span style="color: #000000;">,
      </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">张三</span><span style="color: #800000;">"</span><span style="color: #000000;">
    }
  ]
}</span></pre>
</div>
<span class="cnblogs_code_collapse">class.json</span></div>
<p>3，读取appsettings.json</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('993e93b3-29b3-492d-8ef3-b4a1f22385e8')"><img id="code_img_closed_993e93b3-29b3-492d-8ef3-b4a1f22385e8" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_993e93b3-29b3-492d-8ef3-b4a1f22385e8" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('993e93b3-29b3-492d-8ef3-b4a1f22385e8',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_993e93b3-29b3-492d-8ef3-b4a1f22385e8" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Mvc;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Configuration;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> WebApplication1.Controllers
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> HomeController : Controller
    {
        </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> IConfiguration _configuration;
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> HomeController(IConfiguration configuration)
        {
            _configuration </span>=<span style="color: #000000;"> configuration;
        }

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> IActionResult Index()
        {
            Class c </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> Class();
            _configuration.Bind(c);

            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> View();
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">构造注入iconfiguration</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('320ab53a-9426-4103-b7d4-eec4618bdcef')"><img id="code_img_closed_320ab53a-9426-4103-b7d4-eec4618bdcef" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_320ab53a-9426-4103-b7d4-eec4618bdcef" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('320ab53a-9426-4103-b7d4-eec4618bdcef',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_320ab53a-9426-4103-b7d4-eec4618bdcef" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> WebApplication1
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Class
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> no { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> name { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
        </span><span style="color: #0000ff;">public</span> IEnumerable&lt;student&gt; student { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> student {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> no { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> name { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Class类</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('97270f2c-8833-46bb-8c9c-ab5331812adb')"><img id="code_img_closed_97270f2c-8833-46bb-8c9c-ab5331812adb" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_97270f2c-8833-46bb-8c9c-ab5331812adb" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('97270f2c-8833-46bb-8c9c-ab5331812adb',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_97270f2c-8833-46bb-8c9c-ab5331812adb" class="cnblogs_code_hide">
<pre><span style="color: #000000;">{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">no</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">1</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">asp.net core</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">student</span><span style="color: #800000;">"</span><span style="color: #000000;">: [
    {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">no</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">1</span><span style="color: #800000;">"</span><span style="color: #000000;">,
      </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">张三</span><span style="color: #800000;">"</span><span style="color: #000000;">
    },
    {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">no</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">2</span><span style="color: #800000;">"</span><span style="color: #000000;">,
      </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">张三</span><span style="color: #800000;">"</span><span style="color: #000000;">
    }
  ]
}</span></pre>
</div>
<span class="cnblogs_code_collapse">appsettings.json</span></div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a2"></a>二、管道</span></strong></span></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('83807306-9f6d-4ef3-ba2c-c68f50ffc7bb')"><img id="code_img_closed_83807306-9f6d-4ef3-ba2c-c68f50ffc7bb" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_83807306-9f6d-4ef3-ba2c-c68f50ffc7bb" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('83807306-9f6d-4ef3-ba2c-c68f50ffc7bb',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_83807306-9f6d-4ef3-ba2c-c68f50ffc7bb" class="cnblogs_code_hide">
<pre><span style="color: #008080;"> 1</span> <span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #008080;"> 2</span> <span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #008080;"> 3</span> <span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #008080;"> 4</span> <span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #008080;"> 5</span> <span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Builder;
</span><span style="color: #008080;"> 6</span> <span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Hosting;
</span><span style="color: #008080;"> 7</span> <span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Configuration;
</span><span style="color: #008080;"> 8</span> <span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.DependencyInjection;
</span><span style="color: #008080;"> 9</span> <span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Http;
</span><span style="color: #008080;">10</span> 
<span style="color: #008080;">11</span> <span style="color: #0000ff;">namespace</span><span style="color: #000000;"> test2
</span><span style="color: #008080;">12</span> <span style="color: #000000;">{
</span><span style="color: #008080;">13</span>     <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Startup
</span><span style="color: #008080;">14</span> <span style="color: #000000;">    {
</span><span style="color: #008080;">15</span>         <span style="color: #0000ff;">public</span><span style="color: #000000;"> Startup(IConfiguration configuration)
</span><span style="color: #008080;">16</span> <span style="color: #000000;">        {
</span><span style="color: #008080;">17</span>             Configuration =<span style="color: #000000;"> configuration;
</span><span style="color: #008080;">18</span> <span style="color: #000000;">        }
</span><span style="color: #008080;">19</span> 
<span style="color: #008080;">20</span>         <span style="color: #0000ff;">public</span> IConfiguration Configuration { <span style="color: #0000ff;">get</span><span style="color: #000000;">; }
</span><span style="color: #008080;">21</span> 
<span style="color: #008080;">22</span>         <span style="color: #008000;">//</span><span style="color: #008000;"> This method gets called by the runtime. Use this method to add services to the container.</span>
<span style="color: #008080;">23</span>         <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> ConfigureServices(IServiceCollection services)
</span><span style="color: #008080;">24</span> <span style="color: #000000;">        {
</span><span style="color: #008080;">25</span> <span style="color: #000000;">            services.AddMvc();
</span><span style="color: #008080;">26</span> <span style="color: #000000;">        }
</span><span style="color: #008080;">27</span> 
<span style="color: #008080;">28</span>         <span style="color: #008000;">//</span><span style="color: #008000;"> This method gets called by the runtime. Use this method to configure the HTTP request pipeline.</span>
<span style="color: #008080;">29</span>         <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configure(IApplicationBuilder app, IHostingEnvironment env)
</span><span style="color: #008080;">30</span> <span style="color: #000000;">        {
</span><span style="color: #008080;">31</span>             <span style="color: #0000ff;">if</span><span style="color: #000000;"> (env.IsDevelopment())
</span><span style="color: #008080;">32</span> <span style="color: #000000;">            {
</span><span style="color: #008080;">33</span> <span style="color: #000000;">                app.UseDeveloperExceptionPage();
</span><span style="color: #008080;">34</span> <span style="color: #000000;">            }
</span><span style="color: #008080;">35</span>             <span style="color: #0000ff;">else</span>
<span style="color: #008080;">36</span> <span style="color: #000000;">            {
</span><span style="color: #008080;">37</span>                 app.UseExceptionHandler(<span style="color: #800000;">"</span><span style="color: #800000;">/Home/Error</span><span style="color: #800000;">"</span><span style="color: #000000;">);
</span><span style="color: #008080;">38</span> <span style="color: #000000;">            }
</span><span style="color: #008080;">39</span> 
<span style="color: #008080;">40</span>             <span style="color: #008000;">//</span><span style="color: #008000;">管道被截断 url：</span><span style="color: #008000; text-decoration: underline;">http://ip</span><span style="color: #008000;">:port/test</span>
<span style="color: #008080;">41</span>             app.Map(<span style="color: #800000;">"</span><span style="color: #800000;">/test</span><span style="color: #800000;">"</span>,testApp=&gt;<span style="color: #000000;">{
</span><span style="color: #008080;">42</span>                 testApp.Run(<span style="color: #0000ff;">async</span>(context)=&gt;<span style="color: #000000;">{
</span><span style="color: #008080;">43</span>                     <span style="color: #0000ff;">await</span> context.Response.WriteAsync(<span style="color: #800000;">"</span><span style="color: #800000;">test</span><span style="color: #800000;">"</span><span style="color: #000000;">);
</span><span style="color: #008080;">44</span> <span style="color: #000000;">                });
</span><span style="color: #008080;">45</span> <span style="color: #000000;">            });
</span><span style="color: #008080;">46</span> 
<span style="color: #008080;">47</span>             <span style="color: #008000;">//</span><span style="color: #008000;">管道插入</span>
<span style="color: #008080;">48</span>             app.Use(<span style="color: #0000ff;">async</span> (context,next)=&gt;<span style="color: #000000;">{
</span><span style="color: #008080;">49</span>                 <span style="color: #0000ff;">await</span> context.Response.WriteAsync(<span style="color: #800000;">"</span><span style="color: #800000;">1</span><span style="color: #800000;">"</span><span style="color: #000000;">);
</span><span style="color: #008080;">50</span>                 <span style="color: #0000ff;">await</span><span style="color: #000000;"> next.Invoke();
</span><span style="color: #008080;">51</span> <span style="color: #000000;">            });
</span><span style="color: #008080;">52</span> 
<span style="color: #008080;">53</span>             <span style="color: #008000;">//</span><span style="color: #008000;">管道插入</span>
<span style="color: #008080;">54</span>             app.Use(next=&gt;<span style="color: #000000;">{
</span><span style="color: #008080;">55</span>                 <span style="color: #0000ff;">return</span> (context)=&gt;<span style="color: #000000;">{
</span><span style="color: #008080;">56</span>                     <span style="color: #0000ff;">return</span> context.Response.WriteAsync(<span style="color: #800000;">"</span><span style="color: #800000;">2</span><span style="color: #800000;">"</span><span style="color: #000000;">);
</span><span style="color: #008080;">57</span> <span style="color: #000000;">                };
</span><span style="color: #008080;">58</span> <span style="color: #000000;">            });
</span><span style="color: #008080;">59</span> 
<span style="color: #008080;">60</span>            
<span style="color: #008080;">61</span> <span style="color: #000000;">            app.UseStaticFiles();
</span><span style="color: #008080;">62</span> 
<span style="color: #008080;">63</span>             app.UseMvc(routes =&gt;
<span style="color: #008080;">64</span> <span style="color: #000000;">            {
</span><span style="color: #008080;">65</span> <span style="color: #000000;">                routes.MapRoute(
</span><span style="color: #008080;">66</span>                     name: <span style="color: #800000;">"</span><span style="color: #800000;">default</span><span style="color: #800000;">"</span><span style="color: #000000;">,
</span><span style="color: #008080;">67</span>                     template: <span style="color: #800000;">"</span><span style="color: #800000;">{controller=Home}/{action=Index}/{id?}</span><span style="color: #800000;">"</span><span style="color: #000000;">);
</span><span style="color: #008080;">68</span> <span style="color: #000000;">            });
</span><span style="color: #008080;">69</span> <span style="color: #000000;">        }
</span><span style="color: #008080;">70</span> <span style="color: #000000;">    }
</span><span style="color: #008080;">71</span> }</pre>
</div>
<span class="cnblogs_code_collapse">Startup</span></div>
<p>1，模拟RequestDelegete</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('3ae74907-5f7b-45a0-9aaa-e6c848d8109a')"><img id="code_img_closed_3ae74907-5f7b-45a0-9aaa-e6c848d8109a" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_3ae74907-5f7b-45a0-9aaa-e6c848d8109a" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('3ae74907-5f7b-45a0-9aaa-e6c848d8109a',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_3ae74907-5f7b-45a0-9aaa-e6c848d8109a" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> test3
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> List&lt;Func&lt;RequestDelegete,RequestDelegete&gt;&gt; _list=<span style="color: #0000ff;">new</span> List&lt;Func&lt;RequestDelegete, RequestDelegete&gt;&gt;<span style="color: #000000;">();
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            Use(next</span>=&gt;<span style="color: #000000;">{
                </span><span style="color: #0000ff;">return</span> (context)=&gt;<span style="color: #000000;">{
                    Console.WriteLine(</span><span style="color: #800080;">1</span><span style="color: #000000;">);
                    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> Task.CompletedTask;
                    </span><span style="color: #008000;">//</span><span style="color: #008000;">return next.Invoke(context);</span>
<span style="color: #000000;">                };
            });

            Use(next</span>=&gt;<span style="color: #000000;">{
                </span><span style="color: #0000ff;">return</span> (context)=&gt;<span style="color: #000000;">{
                    Console.WriteLine(</span><span style="color: #800080;">2</span><span style="color: #000000;">);
                    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> next.Invoke(context);
                };
            });

            RequestDelegete end</span>=(context)=&gt;<span style="color: #000000;">{
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">end</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> Task.CompletedTask;};
            
            _list.Reverse();
            </span><span style="color: #0000ff;">foreach</span>(<span style="color: #0000ff;">var</span> item <span style="color: #0000ff;">in</span><span style="color: #000000;"> _list)
            {
                end</span>=<span style="color: #000000;">item.Invoke(end);
            }
            end.Invoke(</span><span style="color: #0000ff;">new</span><span style="color: #000000;"> Context());

            Console.ReadKey();
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Use(Func&lt;RequestDelegete,RequestDelegete&gt;<span style="color: #000000;"> func)
        {
            _list.Add(func);
        }

    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Program</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('4051f19b-f63f-4c98-a12d-22872f388e8b')"><img id="code_img_closed_4051f19b-f63f-4c98-a12d-22872f388e8b" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_4051f19b-f63f-4c98-a12d-22872f388e8b" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('4051f19b-f63f-4c98-a12d-22872f388e8b',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_4051f19b-f63f-4c98-a12d-22872f388e8b" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> test3
{
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">delegate</span><span style="color: #000000;"> Task RequestDelegete(Context context);
}</span></pre>
</div>
<span class="cnblogs_code_collapse">RequestDelegete</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('ab4fd4ab-290b-4d98-a5e5-308d873579b9')"><img id="code_img_closed_ab4fd4ab-290b-4d98-a5e5-308d873579b9" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_ab4fd4ab-290b-4d98-a5e5-308d873579b9" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('ab4fd4ab-290b-4d98-a5e5-308d873579b9',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_ab4fd4ab-290b-4d98-a5e5-308d873579b9" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> test3
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Context
    {
        
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Context</span></div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a3"></a>三、认证与授权</span></strong></p>
<p>1，Cookie-based认证</p>
<p>①注册Cookie认证</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('ab4e3e5c-4632-4df2-9cad-2d3863eccfce')"><img id="code_img_closed_ab4e3e5c-4632-4df2-9cad-2d3863eccfce" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_ab4e3e5c-4632-4df2-9cad-2d3863eccfce" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('ab4e3e5c-4632-4df2-9cad-2d3863eccfce',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_ab4e3e5c-4632-4df2-9cad-2d3863eccfce" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Builder;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Hosting;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Configuration;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.DependencyInjection;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Authentication;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Authentication.Cookies;


</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> cookieBased
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
            </span><span style="color: #008000;">//</span><span style="color: #008000;">注册</span>
<span style="color: #000000;">            services.AddAuthentication(CookieAuthenticationDefaults.AuthenticationScheme)
                    .AddCookie(option</span>=&gt;<span style="color: #000000;">{
                        option.LoginPath</span>=<span style="color: #800000;">"</span><span style="color: #800000;">/Login/Index</span><span style="color: #800000;">"</span><span style="color: #000000;">;
                    });

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

            app.UseStaticFiles();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">添加认证中间件</span>
<span style="color: #000000;">            app.UseAuthentication();

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
<p>②实现登录与注销</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('d359801b-5bd9-431b-a09d-ace2d56dde06')"><img id="code_img_closed_d359801b-5bd9-431b-a09d-ace2d56dde06" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_d359801b-5bd9-431b-a09d-ace2d56dde06" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('d359801b-5bd9-431b-a09d-ace2d56dde06',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_d359801b-5bd9-431b-a09d-ace2d56dde06" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Diagnostics;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Mvc;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> cookieBased.Models;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Authentication;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Authentication.Cookies;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Security.Claims;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> cookieBased.Controllers
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> LoginController:Controller
    {
        [HttpGet]
        </span><span style="color: #0000ff;">public</span> IActionResult Index(<span style="color: #0000ff;">string</span><span style="color: #000000;"> returnUrl)
        {
            ViewData[</span><span style="color: #800000;">"</span><span style="color: #800000;">returnUrl</span><span style="color: #800000;">"</span>]=<span style="color: #000000;">returnUrl;
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> View();
        }

        [HttpPost]
        </span><span style="color: #0000ff;">public</span> IActionResult LoginIn(<span style="color: #0000ff;">string</span><span style="color: #000000;"> returnUrl)
        {
            ClaimsIdentity identity</span>=<span style="color: #0000ff;">new</span> ClaimsIdentity (<span style="color: #0000ff;">new</span> List&lt;Claim&gt;<span style="color: #000000;">(){
                </span><span style="color: #0000ff;">new</span> Claim(ClaimTypes.Name,<span style="color: #800000;">"</span><span style="color: #800000;">hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">),
                </span><span style="color: #0000ff;">new</span> Claim(ClaimTypes.Role,<span style="color: #800000;">"</span><span style="color: #800000;">admin</span><span style="color: #800000;">"</span><span style="color: #000000;">)
            },CookieAuthenticationDefaults.AuthenticationScheme);
            HttpContext.SignInAsync(CookieAuthenticationDefaults.AuthenticationScheme,</span><span style="color: #0000ff;">new</span><span style="color: #000000;"> ClaimsPrincipal(identity));

            </span><span style="color: #0000ff;">var</span> user=<span style="color: #000000;"> HttpContext.User.Identity.Name;
            </span><span style="color: #0000ff;">var</span> b=<span style="color: #000000;"> HttpContext.User.Identity.IsAuthenticated;

            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> Redirect(returnUrl);
        }

        [HttpPost]
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> IActionResult LoginOut()
        {
            HttpContext.SignOutAsync(CookieAuthenticationDefaults.AuthenticationScheme);
            </span><span style="color: #0000ff;">return</span> Redirect(<span style="color: #800000;">"</span><span style="color: #800000;">/</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }

    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">LoginController</span></div>
<p>案例下载：<a href="https://pan.baidu.com/s/15etE9CNfzDLCHW6ZHc-euw" target="_blank">https://pan.baidu.com/s/15etE9CNfzDLCHW6ZHc-euw</a></p>
<p>&nbsp;</p>
<p>2，JWT认证</p>
<p>jwt验证网站： <a href="https://jwt.io/" target="_blank">https://jwt.io/</a></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('e1cc7276-b40e-482c-a0e4-97ffbcf3ca81')"><img id="code_img_closed_e1cc7276-b40e-482c-a0e4-97ffbcf3ca81" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_e1cc7276-b40e-482c-a0e4-97ffbcf3ca81" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('e1cc7276-b40e-482c-a0e4-97ffbcf3ca81',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_e1cc7276-b40e-482c-a0e4-97ffbcf3ca81" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> JwtAuthenticate.Models
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> JwtSettings
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;">token是谁颁发的</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Issure{<span style="color: #0000ff;">get</span>;<span style="color: #0000ff;">set</span><span style="color: #000000;">;}
        </span><span style="color: #008000;">//</span><span style="color: #008000;">可以给那些客户端使用</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Audience{<span style="color: #0000ff;">get</span>;<span style="color: #0000ff;">set</span><span style="color: #000000;">;}
        </span><span style="color: #008000;">//</span><span style="color: #008000;">需要加密的Secretkey</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Secretkey{<span style="color: #0000ff;">get</span>;<span style="color: #0000ff;">set</span><span style="color: #000000;">;}
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">JwtAuthenticate.Models.JwtSettings</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('8d70b5ad-f2a0-4833-a499-540bd803dd0f')"><img id="code_img_closed_8d70b5ad-f2a0-4833-a499-540bd803dd0f" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_8d70b5ad-f2a0-4833-a499-540bd803dd0f" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('8d70b5ad-f2a0-4833-a499-540bd803dd0f',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_8d70b5ad-f2a0-4833-a499-540bd803dd0f" class="cnblogs_code_hide">
<pre><span style="color: #000000;">{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">Logging</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">IncludeScopes</span><span style="color: #800000;">"</span>: <span style="color: #0000ff;">false</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">Debug</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">LogLevel</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">Default</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">Warning</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    },
    </span><span style="color: #800000;">"</span><span style="color: #800000;">Console</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">LogLevel</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">Default</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">Warning</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    }
  },
  </span><span style="color: #800000;">"</span><span style="color: #800000;">JwtSettings</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
    </span><span style="color: #800000;">"</span><span style="color: #800000;">Audience</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:5000</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">Issure</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:5000</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">SecretKey</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">11111111111111111</span><span style="color: #800000;">"</span><span style="color: #000000;">
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">appsettings.json</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('8ff20c1f-99cb-4c64-a3d0-040477c55ed9')"><img id="code_img_closed_8ff20c1f-99cb-4c64-a3d0-040477c55ed9" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_8ff20c1f-99cb-4c64-a3d0-040477c55ed9" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('8ff20c1f-99cb-4c64-a3d0-040477c55ed9',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_8ff20c1f-99cb-4c64-a3d0-040477c55ed9" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Builder;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Hosting;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Configuration;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.DependencyInjection;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Logging;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Options;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> JwtAuthenticate.Models;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Authentication.JwtBearer;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.IdentityModel.Tokens;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> JwtAuthenticate
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
            </span><span style="color: #008000;">//</span><span style="color: #008000;">将配置文件jwtSettings注册进来
            </span><span style="color: #008000;">//</span><span style="color: #008000;">public AuthorizeController(IOptions&lt;JwtSettings&gt; jwtSettings)会使用到</span>
            services.Configure&lt;JwtSettings&gt;(Configuration.GetSection(<span style="color: #800000;">"</span><span style="color: #800000;">jwtSettings</span><span style="color: #800000;">"</span><span style="color: #000000;">));

            </span><span style="color: #0000ff;">var</span> jwtSettings=<span style="color: #0000ff;">new</span><span style="color: #000000;"> JwtSettings();
            Configuration.Bind(</span><span style="color: #800000;">"</span><span style="color: #800000;">JwtSettings</span><span style="color: #800000;">"</span><span style="color: #000000;">,jwtSettings);
            
            services.AddAuthentication(options</span>=&gt;{<span style="color: #008000;">//</span><span style="color: #008000;">配置Authentication</span>
                options.DefaultAuthenticateScheme=<span style="color: #000000;">JwtBearerDefaults.AuthenticationScheme;
                options.DefaultChallengeScheme</span>=<span style="color: #000000;">JwtBearerDefaults.AuthenticationScheme;
            })
            .AddJwtBearer(options</span>=&gt;{<span style="color: #008000;">//</span><span style="color: #008000;">配置JwtBearer</span>
                options.TokenValidationParameters=<span style="color: #0000ff;">new</span><span style="color: #000000;"> TokenValidationParameters{
                    ValidIssuer</span>=<span style="color: #000000;">jwtSettings.Issure,
                    ValidAudience</span>=<span style="color: #000000;">jwtSettings.Audience,
                    IssuerSigningKey</span>=<span style="color: #0000ff;">new</span><span style="color: #000000;"> SymmetricSecurityKey(Encoding.UTF8.GetBytes(jwtSettings.Secretkey))
                };
            });

            services.AddMvc();
        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> This method gets called by the runtime. Use this method to configure the HTTP request pipeline.</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configure(IApplicationBuilder app, IHostingEnvironment env)
        {
            </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (env.IsDevelopment())
            {
                app.UseDeveloperExceptionPage();
            }

            app.UseAuthentication();
            app.UseMvc();
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Startup</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('d62ba77a-3d71-44c1-932a-1613692ae333')"><img id="code_img_closed_d62ba77a-3d71-44c1-932a-1613692ae333" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_d62ba77a-3d71-44c1-932a-1613692ae333" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('d62ba77a-3d71-44c1-932a-1613692ae333',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_d62ba77a-3d71-44c1-932a-1613692ae333" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Mvc;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Authorization;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> JwtAuthenticate.Models;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Security.Claims;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.IdentityModel.Tokens;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Options;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.IdentityModel.Tokens.Jwt;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> JwtAuthenticate.Controllers
{

    [Route(</span><span style="color: #800000;">"</span><span style="color: #800000;">api/[controller]</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> AuthorizeController:Controller
    {
        </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> JwtSettings _jwtSettings;
        </span><span style="color: #0000ff;">public</span> AuthorizeController(IOptions&lt;JwtSettings&gt;<span style="color: #000000;"> jwtSettings)
        {
            _jwtSettings</span>=<span style="color: #000000;">jwtSettings.Value;
        }

        [HttpGet]
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span><span style="color: #000000;"> A()
        {
            </span><span style="color: #0000ff;">return</span> <span style="color: #800000;">"</span><span style="color: #800000;">a</span><span style="color: #800000;">"</span><span style="color: #000000;">;
        }

        [HttpPost]
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> IActionResult Token([FromBody]LoginViewModel model)
        {
            </span><span style="color: #0000ff;">if</span>(!ModelState.IsValid)<span style="color: #0000ff;">return</span><span style="color: #000000;"> BadRequest();
            </span><span style="color: #0000ff;">if</span>(!(model.UserName==<span style="color: #800000;">"</span><span style="color: #800000;">hunter</span><span style="color: #800000;">"</span>&amp;&amp;model.Password==<span style="color: #800000;">"</span><span style="color: #800000;">123456</span><span style="color: #800000;">"</span>))<span style="color: #0000ff;">return</span><span style="color: #000000;"> BadRequest();
            
            </span><span style="color: #0000ff;">var</span> claims=<span style="color: #0000ff;">new</span><span style="color: #000000;"> Claim[]{
                </span><span style="color: #0000ff;">new</span> Claim(ClaimTypes.Name,<span style="color: #800000;">"</span><span style="color: #800000;">hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">),
                </span><span style="color: #0000ff;">new</span> Claim(ClaimTypes.Role,<span style="color: #800000;">"</span><span style="color: #800000;">admin</span><span style="color: #800000;">"</span><span style="color: #000000;">)
            };

            </span><span style="color: #0000ff;">var</span> key=<span style="color: #0000ff;">new</span><span style="color: #000000;"> SymmetricSecurityKey(Encoding.UTF8.GetBytes(_jwtSettings.Secretkey));
            </span><span style="color: #0000ff;">var</span> creds=<span style="color: #0000ff;">new</span><span style="color: #000000;"> SigningCredentials(key,SecurityAlgorithms.HmacSha256);
            </span><span style="color: #0000ff;">var</span> token=<span style="color: #0000ff;">new</span><span style="color: #000000;"> JwtSecurityToken(
                _jwtSettings.Issure
                ,_jwtSettings.Audience
                ,claims,DateTime.Now,DateTime.Now.AddMinutes(</span><span style="color: #800080;">30</span><span style="color: #000000;">)
                ,creds);
            </span><span style="color: #0000ff;">return</span> Ok(<span style="color: #0000ff;">new</span> {token=<span style="color: #0000ff;">new</span><span style="color: #000000;"> JwtSecurityTokenHandler().WriteToken(token)});
        }
        
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">AuthorizeController</span></div>
<p><img src="https://images2018.cnblogs.com/blog/741594/201805/741594-20180505165311175-514976331.png" alt="" width="983" height="384" /></p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201805/741594-20180505165413269-1453364783.png" alt="" width="912" height="258" /></p>
<p>&nbsp;</p>
<p>3，基于Claim的Jwt认证</p>
<p>①加上authorize标签</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('e77ecc45-0ad7-44d1-a97f-48e0e802ed6c')"><img id="code_img_closed_e77ecc45-0ad7-44d1-a97f-48e0e802ed6c" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_e77ecc45-0ad7-44d1-a97f-48e0e802ed6c" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('e77ecc45-0ad7-44d1-a97f-48e0e802ed6c',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_e77ecc45-0ad7-44d1-a97f-48e0e802ed6c" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Mvc;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Authorization;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> JwtAuthenticate.Controllers
{

    [Route(</span><span style="color: #800000;">"</span><span style="color: #800000;">api/[controller]</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ValuesController : Controller
    {
    
        [Authorize(Policy</span>=<span style="color: #800000;">"</span><span style="color: #800000;">values.Get</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
        
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> GET api/values</span>
<span style="color: #000000;">        [HttpGet] 
        </span><span style="color: #0000ff;">public</span> IEnumerable&lt;<span style="color: #0000ff;">string</span>&gt;<span style="color: #000000;"> Get()
        {
            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> <span style="color: #0000ff;">string</span>[] { <span style="color: #800000;">"</span><span style="color: #800000;">value1</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">value2</span><span style="color: #800000;">"</span><span style="color: #000000;"> };
        }

         [Authorize(Policy</span>=<span style="color: #800000;">"</span><span style="color: #800000;">values.Get</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> GET api/values/5</span>
        [HttpGet(<span style="color: #800000;">"</span><span style="color: #800000;">{id}</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Get(<span style="color: #0000ff;">int</span><span style="color: #000000;"> id)
        {
            </span><span style="color: #0000ff;">return</span> <span style="color: #800000;">"</span><span style="color: #800000;">value</span><span style="color: #800000;">"</span><span style="color: #000000;">;
        }

        [Authorize(Policy</span>=<span style="color: #800000;">"</span><span style="color: #800000;">values.Post</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> POST api/values</span>
<span style="color: #000000;">        [HttpPost]
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> Post([FromBody]<span style="color: #0000ff;">string</span><span style="color: #000000;"> value)
        {
        }

        [Authorize(Policy</span>=<span style="color: #800000;">"</span><span style="color: #800000;">values.Put</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> PUT api/values/5</span>
        [HttpPut(<span style="color: #800000;">"</span><span style="color: #800000;">{id}</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> Put(<span style="color: #0000ff;">int</span> id, [FromBody]<span style="color: #0000ff;">string</span><span style="color: #000000;"> value)
        {
        }

        [Authorize(Policy</span>=<span style="color: #800000;">"</span><span style="color: #800000;">values.Delete</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> DELETE api/values/5</span>
        [HttpDelete(<span style="color: #800000;">"</span><span style="color: #800000;">{id}</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> Delete(<span style="color: #0000ff;">int</span><span style="color: #000000;"> id)
        {
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">ValuesController</span></div>
<p>②设置Policy</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('da93d25b-7705-453c-915c-6413c5cf5f52')"><img id="code_img_closed_da93d25b-7705-453c-915c-6413c5cf5f52" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_da93d25b-7705-453c-915c-6413c5cf5f52" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('da93d25b-7705-453c-915c-6413c5cf5f52',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_da93d25b-7705-453c-915c-6413c5cf5f52" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Builder;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Hosting;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Configuration;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.DependencyInjection;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Logging;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Options;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> JwtAuthenticate.Models;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Authentication.JwtBearer;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.IdentityModel.Tokens;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> JwtAuthenticate
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
            </span><span style="color: #008000;">//</span><span style="color: #008000;">将配置文件jwtSettings注册进来
            </span><span style="color: #008000;">//</span><span style="color: #008000;">public AuthorizeController(IOptions&lt;JwtSettings&gt; jwtSettings)会使用到</span>
            services.Configure&lt;JwtSettings&gt;(Configuration.GetSection(<span style="color: #800000;">"</span><span style="color: #800000;">jwtSettings</span><span style="color: #800000;">"</span><span style="color: #000000;">));

            </span><span style="color: #0000ff;">var</span> jwtSettings=<span style="color: #0000ff;">new</span><span style="color: #000000;"> JwtSettings();
            Configuration.Bind(</span><span style="color: #800000;">"</span><span style="color: #800000;">JwtSettings</span><span style="color: #800000;">"</span><span style="color: #000000;">,jwtSettings);
            
            services.AddAuthentication(options</span>=&gt;{<span style="color: #008000;">//</span><span style="color: #008000;">配置Authentication</span>
                options.DefaultAuthenticateScheme=<span style="color: #000000;">JwtBearerDefaults.AuthenticationScheme;
                options.DefaultChallengeScheme</span>=<span style="color: #000000;">JwtBearerDefaults.AuthenticationScheme;
            })
            .AddJwtBearer(options</span>=&gt;{<span style="color: #008000;">//</span><span style="color: #008000;">配置JwtBearer</span>
                options.TokenValidationParameters=<span style="color: #0000ff;">new</span><span style="color: #000000;"> TokenValidationParameters{
                    ValidIssuer</span>=<span style="color: #000000;">jwtSettings.Issure,
                    ValidAudience</span>=<span style="color: #000000;">jwtSettings.Audience,
                    IssuerSigningKey</span>=<span style="color: #0000ff;">new</span><span style="color: #000000;"> SymmetricSecurityKey(Encoding.UTF8.GetBytes(jwtSettings.Secretkey))
                };
            });

            </span><span style="color: #008000;">//</span><span style="color: #008000;">设置policy</span>
            services.AddAuthorization(option=&gt;<span style="color: #000000;">{
                option.AddPolicy(</span><span style="color: #800000;">"</span><span style="color: #800000;">values.Get</span><span style="color: #800000;">"</span>,policy=&gt;{policy.RequireClaim(<span style="color: #800000;">"</span><span style="color: #800000;">values.Get</span><span style="color: #800000;">"</span><span style="color: #000000;">);});
                option.AddPolicy(</span><span style="color: #800000;">"</span><span style="color: #800000;">values.Post</span><span style="color: #800000;">"</span>,policy=&gt;{policy.RequireClaim(<span style="color: #800000;">"</span><span style="color: #800000;">values.Post</span><span style="color: #800000;">"</span><span style="color: #000000;">);});
                option.AddPolicy(</span><span style="color: #800000;">"</span><span style="color: #800000;">values.Delete</span><span style="color: #800000;">"</span>,policy=&gt;{policy.RequireClaim(<span style="color: #800000;">"</span><span style="color: #800000;">values.Delete</span><span style="color: #800000;">"</span><span style="color: #000000;">);});
                option.AddPolicy(</span><span style="color: #800000;">"</span><span style="color: #800000;">values.Put</span><span style="color: #800000;">"</span>,policy=&gt;{policy.RequireClaim(<span style="color: #800000;">"</span><span style="color: #800000;">values.Put</span><span style="color: #800000;">"</span><span style="color: #000000;">);});
            });

            services.AddMvc();
        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> This method gets called by the runtime. Use this method to configure the HTTP request pipeline.</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configure(IApplicationBuilder app, IHostingEnvironment env)
        {
            </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (env.IsDevelopment())
            {
                app.UseDeveloperExceptionPage();
            }

            app.UseAuthentication();
            app.UseMvc();
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Startup</span></div>
<p>③授权</p>
<p>只能访问values.Get和values.Put了</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('a103dc04-73d2-4f5a-927f-077cb752e727')"><img id="code_img_closed_a103dc04-73d2-4f5a-927f-077cb752e727" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_a103dc04-73d2-4f5a-927f-077cb752e727" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('a103dc04-73d2-4f5a-927f-077cb752e727',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_a103dc04-73d2-4f5a-927f-077cb752e727" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Mvc;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Authorization;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> JwtAuthenticate.Models;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Security.Claims;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.IdentityModel.Tokens;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Options;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.IdentityModel.Tokens.Jwt;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> JwtAuthenticate.Controllers
{

    [Route(</span><span style="color: #800000;">"</span><span style="color: #800000;">api/[controller]</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> AuthorizeController:Controller
    {
        </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> JwtSettings _jwtSettings;
        </span><span style="color: #0000ff;">public</span> AuthorizeController(IOptions&lt;JwtSettings&gt;<span style="color: #000000;"> jwtSettings)
        {
            _jwtSettings</span>=<span style="color: #000000;">jwtSettings.Value;
        }

        [HttpGet]
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span><span style="color: #000000;"> A()
        {
            </span><span style="color: #0000ff;">return</span> <span style="color: #800000;">"</span><span style="color: #800000;">a</span><span style="color: #800000;">"</span><span style="color: #000000;">;
        }

        [HttpPost]
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> IActionResult Token([FromBody]LoginViewModel model)
        {
            </span><span style="color: #0000ff;">if</span>(!ModelState.IsValid)<span style="color: #0000ff;">return</span><span style="color: #000000;"> BadRequest();
            </span><span style="color: #0000ff;">if</span>(!(model.UserName==<span style="color: #800000;">"</span><span style="color: #800000;">hunter</span><span style="color: #800000;">"</span>&amp;&amp;model.Password==<span style="color: #800000;">"</span><span style="color: #800000;">123456</span><span style="color: #800000;">"</span>))<span style="color: #0000ff;">return</span><span style="color: #000000;"> BadRequest();
            
            </span><span style="color: #0000ff;">var</span> claims=<span style="color: #0000ff;">new</span><span style="color: #000000;"> Claim[]{
                </span><span style="color: #0000ff;">new</span> Claim(ClaimTypes.Name,<span style="color: #800000;">"</span><span style="color: #800000;">hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">),
                </span><span style="color: #0000ff;">new</span> Claim(<span style="color: #800000;">"</span><span style="color: #800000;">values.Get</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">true</span><span style="color: #800000;">"</span><span style="color: #000000;">),
                </span><span style="color: #0000ff;">new</span> Claim(<span style="color: #800000;">"</span><span style="color: #800000;">values.Put</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">true</span><span style="color: #800000;">"</span><span style="color: #000000;">)
            };

            </span><span style="color: #0000ff;">var</span> key=<span style="color: #0000ff;">new</span><span style="color: #000000;"> SymmetricSecurityKey(Encoding.UTF8.GetBytes(_jwtSettings.Secretkey));
            </span><span style="color: #0000ff;">var</span> creds=<span style="color: #0000ff;">new</span><span style="color: #000000;"> SigningCredentials(key,SecurityAlgorithms.HmacSha256);
            </span><span style="color: #0000ff;">var</span> token=<span style="color: #0000ff;">new</span><span style="color: #000000;"> JwtSecurityToken(
                _jwtSettings.Issure
                ,_jwtSettings.Audience
                ,claims,DateTime.Now,DateTime.Now.AddMinutes(</span><span style="color: #800080;">30</span><span style="color: #000000;">)
                ,creds);
            </span><span style="color: #0000ff;">return</span> Ok(<span style="color: #0000ff;">new</span> {token=<span style="color: #0000ff;">new</span><span style="color: #000000;"> JwtSecurityTokenHandler().WriteToken(token)});
        }
        
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">AuthorizeController</span></div>
<p>案例下载：<a href="https://pan.baidu.com/s/1NKJNVMIHeVdPFcua_eH1sQ" target="_blank">https://pan.baidu.com/s/1NKJNVMIHeVdPFcua_eH1sQ&nbsp;</a></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a4"></a>四、MVCDemo</span></strong></p>
<p>使用&nbsp;<span class="cnblogs_code">dotnet <span style="color: #0000ff;">new</span> mvc -au individual -uld</span>&nbsp;创建mvc模板</p>
<p>1，项目启动创建种子数据</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('51598f74-218f-45ee-b218-59fba0aeb7ca')"><img id="code_img_closed_51598f74-218f-45ee-b218-59fba0aeb7ca" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_51598f74-218f-45ee-b218-59fba0aeb7ca" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('51598f74-218f-45ee-b218-59fba0aeb7ca',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_51598f74-218f-45ee-b218-59fba0aeb7ca" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.DependencyInjection;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.EntityFrameworkCore;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Identity;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> mvcDemo2.Data;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> mvcDemo2.Data
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> DbContextSeed
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Seed(DemoDbContext context,IServiceProvider service)
        {
            </span><span style="color: #0000ff;">if</span>(!<span style="color: #000000;">context.Users.Any())
            {
                </span><span style="color: #0000ff;">var</span> usermanager=service.GetRequiredService&lt;UserManager&lt;DemoUser&gt;&gt;<span style="color: #000000;">();
                </span><span style="color: #0000ff;">var</span> result= usermanager.CreateAsync(<span style="color: #0000ff;">new</span><span style="color: #000000;"> DemoUser (){
                    UserName</span>=<span style="color: #800000;">"</span><span style="color: #800000;">admin</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    NormalizedUserName</span>=<span style="color: #800000;">"</span><span style="color: #800000;">admin</span><span style="color: #800000;">"</span><span style="color: #000000;">
                },</span><span style="color: #800000;">"</span><span style="color: #800000;">123456</span><span style="color: #800000;">"</span><span style="color: #000000;">).Result;
                </span><span style="color: #0000ff;">if</span>(!result.Succeeded)<span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> Exception(<span style="color: #800000;">"</span><span style="color: #800000;">创建管理员失败</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">DbContextSeed</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('ff89912c-edd7-4681-86f7-2dcf472e9e0e')"><img id="code_img_closed_ff89912c-edd7-4681-86f7-2dcf472e9e0e" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_ff89912c-edd7-4681-86f7-2dcf472e9e0e" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('ff89912c-edd7-4681-86f7-2dcf472e9e0e',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_ff89912c-edd7-4681-86f7-2dcf472e9e0e" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Hosting;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.EntityFrameworkCore;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.DependencyInjection;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Logging;
</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> mvcDemo2.Data
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> WebHostMigrationExtensions
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span>  IWebHost MigrationDbContext&lt;TContext&gt;(<span style="color: #0000ff;">this</span> IWebHost webhost,Action&lt;TContext,IServiceProvider&gt;<span style="color: #000000;"> sedder)
        </span><span style="color: #0000ff;">where</span><span style="color: #000000;"> TContext:DbContext
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">使用依赖注入，并且在此using中有效</span>
            <span style="color: #0000ff;">using</span>(<span style="color: #0000ff;">var</span> scope=<span style="color: #000000;">webhost.Services.CreateScope()) 
            {
                </span><span style="color: #0000ff;">var</span> service=<span style="color: #000000;"> scope.ServiceProvider;
                </span><span style="color: #0000ff;">var</span> logger= service.GetRequiredService&lt;ILogger&lt;TContext&gt;&gt;<span style="color: #000000;">();
                </span><span style="color: #0000ff;">var</span> context=service.GetRequiredService&lt;TContext&gt;<span style="color: #000000;">();
                </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
                {
                    </span><span style="color: #008000;">//</span><span style="color: #008000;">当数据库不存在会创建数据库</span>
<span style="color: #000000;">                    context.Database.Migrate();
                    sedder(context,service);
                }
                </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (System.Exception ex)
                {
                    logger.LogError(ex.Message);
                }
            }
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> webhost;
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">WebHostMigrationExtensions</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('ddff40c4-9463-468d-a47d-cd35600e93b4')"><img id="code_img_closed_ddff40c4-9463-468d-a47d-cd35600e93b4" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_ddff40c4-9463-468d-a47d-cd35600e93b4" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('ddff40c4-9463-468d-a47d-cd35600e93b4',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_ddff40c4-9463-468d-a47d-cd35600e93b4" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.IO;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Hosting;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Configuration;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Logging;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> mvcDemo2.Data;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> mvcDemo2
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            BuildWebHost(args)
            .MigrationDbContext</span>&lt;DemoDbContext&gt;((context,service)=&gt;<span style="color: #000000;">{
                </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> DbContextSeed().Seed(context,service);
            })
            .Run();
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> IWebHost BuildWebHost(<span style="color: #0000ff;">string</span>[] args) =&gt;<span style="color: #000000;">
            WebHost.CreateDefaultBuilder(args)
                .UseStartup</span>&lt;Startup&gt;<span style="color: #000000;">()
                .Build();
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Program</span></div>
<p>案例下载：<a href="https://pan.baidu.com/s/1y1B3Vnudkke71eIuPQ937A" target="_blank">https://pan.baidu.com/s/1y1B3Vnudkke71eIuPQ937A</a></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a5"></a>五、IdentityServer4</span></strong></p>
<p>1，OAuth2.0密码登录模式（内存操作）</p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201805/741594-20180519202119756-313238837.png" alt="" width="616" height="359" /></p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201805/741594-20180519202142005-1231075795.png" alt="" width="795" height="384" /></p>
<p>&nbsp;①IdentityServerCenter</p>
<p>nuget：&nbsp;<span class="cnblogs_code">IdentityServer4</span>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('4e7aae44-501e-4844-80f6-607caed71bc6')"><img id="code_img_closed_4e7aae44-501e-4844-80f6-607caed71bc6" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_4e7aae44-501e-4844-80f6-607caed71bc6" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('4e7aae44-501e-4844-80f6-607caed71bc6',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_4e7aae44-501e-4844-80f6-607caed71bc6" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> IdentityServer4.Models;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> IdentityServer4.Test;
</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> IdentityServerCenter
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Config
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;">所有可以访问的对象</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> IEnumerable&lt;ApiResource&gt;<span style="color: #000000;"> GetApiResource(){
            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span>  List&lt;ApiResource&gt;<span style="color: #000000;">(){
                </span><span style="color: #0000ff;">new</span> ApiResource(<span style="color: #800000;">"</span><span style="color: #800000;">api</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">api resource</span><span style="color: #800000;">"</span><span style="color: #000000;">)
            };
        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;">客户端配置 </span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> IEnumerable&lt;Client&gt;<span style="color: #000000;"> GetClient(){
            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> List&lt;Client&gt;<span style="color: #000000;">(){
                </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> Client(){
                    ClientId</span>=<span style="color: #800000;">"</span><span style="color: #800000;">123</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    AllowedGrantTypes</span>={GrantType.ResourceOwnerPassword},<span style="color: #008000;">//</span><span style="color: #008000;">访问模式</span>
                    RequireConsent=<span style="color: #0000ff;">false</span><span style="color: #000000;">,
                    ClientSecrets</span>=<span style="color: #000000;">{
                        </span><span style="color: #0000ff;">new</span> Secret(<span style="color: #800000;">"</span><span style="color: #800000;">secret</span><span style="color: #800000;">"</span><span style="color: #000000;">.Sha256())
                    },
                    AllowedScopes</span>={<span style="color: #800000;">"</span><span style="color: #800000;">api</span><span style="color: #800000;">"</span>},<span style="color: #008000;">//</span><span style="color: #008000;">可以访问的resource
                    </span><span style="color: #008000;">//</span><span style="color: #008000;">AllowOfflineAccess=true,</span><span style="color: #008000;">//</span><span style="color: #008000;">使用refresh_token</span>
                    AccessTokenLifetime=<span style="color: #800080;">10</span><span style="color: #000000;">
                }


            };
        }
         </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> List&lt;TestUser&gt;<span style="color: #000000;"> GetUsers(){
            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> List&lt;TestUser&gt;<span style="color: #000000;">(){
                </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> TestUser(){
                    SubjectId</span>=<span style="color: #800000;">"</span><span style="color: #800000;">1</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    Username</span>=<span style="color: #800000;">"</span><span style="color: #800000;">hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    Password</span>=<span style="color: #800000;">"</span><span style="color: #800000;">123456</span><span style="color: #800000;">"</span><span style="color: #000000;">
                }
            };
        }
       

    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Config</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('92e764d6-e7ff-4ee5-95cd-094c18911570')"><img id="code_img_closed_92e764d6-e7ff-4ee5-95cd-094c18911570" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_92e764d6-e7ff-4ee5-95cd-094c18911570" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('92e764d6-e7ff-4ee5-95cd-094c18911570',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_92e764d6-e7ff-4ee5-95cd-094c18911570" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Builder;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Hosting;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Configuration;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.DependencyInjection;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Logging;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Options;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> IdentityServer4;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> IdentityServerCenter
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
            services.AddIdentityServer()
            .AddDeveloperSigningCredential()</span><span style="color: #008000;">//</span><span style="color: #008000;">设置临时签名凭证</span>
            .AddInMemoryApiResources(Config.GetApiResource())<span style="color: #008000;">//</span><span style="color: #008000;">添加api资源</span>
            .AddInMemoryClients(Config.GetClient())<span style="color: #008000;">//</span><span style="color: #008000;">添加客户端</span>
            .AddTestUsers(Config.GetUsers());<span style="color: #008000;">//</span><span style="color: #008000;">添加测试用户</span>
<span style="color: #000000;">
            services.AddMvc();
        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> This method gets called by the runtime. Use this method to configure the HTTP request pipeline.</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configure(IApplicationBuilder app, IHostingEnvironment env)
        {
            </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (env.IsDevelopment())
            {
                app.UseDeveloperExceptionPage();
            }

            app.UseIdentityServer();
            app.UseMvc();
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Startup</span></div>
<p>②ApiResource</p>
<p>nuget：&nbsp;<span class="cnblogs_code">IdentityServer4.AccessTokenValidation</span>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('c490b849-be04-401e-9fb2-e47109639159')"><img id="code_img_closed_c490b849-be04-401e-9fb2-e47109639159" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_c490b849-be04-401e-9fb2-e47109639159" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('c490b849-be04-401e-9fb2-e47109639159',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_c490b849-be04-401e-9fb2-e47109639159" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Builder;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Hosting;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Configuration;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.DependencyInjection;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Logging;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Options;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> IdentityServer4.AccessTokenValidation;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ApiResource
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
            services.AddAuthentication(</span><span style="color: #800000;">"</span><span style="color: #800000;">Bearer</span><span style="color: #800000;">"</span>)<span style="color: #008000;">//</span><span style="color: #008000;">采用Bearer验证类型</span>
                    .AddIdentityServerAuthentication(Options=&gt;<span style="color: #000000;">{
                        Options.ApiName</span>=<span style="color: #800000;">"</span><span style="color: #800000;">api</span><span style="color: #800000;">"</span><span style="color: #000000;">;
                        Options.Authority</span>=<span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:5000</span><span style="color: #800000;">"</span><span style="color: #000000;">;
                        Options.RequireHttpsMetadata</span>=<span style="color: #0000ff;">false</span>;<span style="color: #008000;">//</span><span style="color: #008000;">是否需要https</span>
<span style="color: #000000;">                    });

            services.AddMvc();
        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> This method gets called by the runtime. Use this method to configure the HTTP request pipeline.</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configure(IApplicationBuilder app, IHostingEnvironment env)
        {
            </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (env.IsDevelopment())
            {
                app.UseDeveloperExceptionPage();
            }
            </span><span style="color: #008000;">//</span><span style="color: #008000;">加上认证中间件</span>
<span style="color: #000000;">            app.UseAuthentication();
            app.UseMvc();
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Startup</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('1a75c43b-b5d0-4ecb-9ae6-417bf92d19b8')"><img id="code_img_closed_1a75c43b-b5d0-4ecb-9ae6-417bf92d19b8" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_1a75c43b-b5d0-4ecb-9ae6-417bf92d19b8" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('1a75c43b-b5d0-4ecb-9ae6-417bf92d19b8',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_1a75c43b-b5d0-4ecb-9ae6-417bf92d19b8" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.IO;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Hosting;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Configuration;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Logging;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ApiResource
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
                .UseUrls(</span><span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:5001</span><span style="color: #800000;">"</span><span style="color: #000000;">)
                .Build();
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Program</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('baf09b12-96e3-4399-94cc-2144927b9539')"><img id="code_img_closed_baf09b12-96e3-4399-94cc-2144927b9539" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_baf09b12-96e3-4399-94cc-2144927b9539" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('baf09b12-96e3-4399-94cc-2144927b9539',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_baf09b12-96e3-4399-94cc-2144927b9539" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Mvc;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Authorization;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ApiResource.Controllers
{
    [Route(</span><span style="color: #800000;">"</span><span style="color: #800000;">api/[controller]</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
    [Authorize]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ValuesController : Controller
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> GET api/values</span>
<span style="color: #000000;">        [HttpGet]
        </span><span style="color: #0000ff;">public</span> IEnumerable&lt;<span style="color: #0000ff;">string</span>&gt;<span style="color: #000000;"> Get()
        {
            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> <span style="color: #0000ff;">string</span>[] { <span style="color: #800000;">"</span><span style="color: #800000;">value1</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">value2</span><span style="color: #800000;">"</span><span style="color: #000000;"> };
        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> GET api/values/5</span>
        [HttpGet(<span style="color: #800000;">"</span><span style="color: #800000;">{id}</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Get(<span style="color: #0000ff;">int</span><span style="color: #000000;"> id)
        {
            </span><span style="color: #0000ff;">return</span> <span style="color: #800000;">"</span><span style="color: #800000;">value</span><span style="color: #800000;">"</span><span style="color: #000000;">;
        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> POST api/values</span>
<span style="color: #000000;">        [HttpPost]
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> Post([FromBody]<span style="color: #0000ff;">string</span><span style="color: #000000;"> value)
        {
        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> PUT api/values/5</span>
        [HttpPut(<span style="color: #800000;">"</span><span style="color: #800000;">{id}</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> Put(<span style="color: #0000ff;">int</span> id, [FromBody]<span style="color: #0000ff;">string</span><span style="color: #000000;"> value)
        {
        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> DELETE api/values/5</span>
        [HttpDelete(<span style="color: #800000;">"</span><span style="color: #800000;">{id}</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> Delete(<span style="color: #0000ff;">int</span><span style="color: #000000;"> id)
        {
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Controllers</span></div>
<p><img src="https://images2018.cnblogs.com/blog/741594/201805/741594-20180522172503707-362817385.png" alt="" width="741" height="222" /></p>
<p>③ThreeClient</p>
<p>nuget：&nbsp;<span class="cnblogs_code">IdentityModel</span>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('cf501f9c-6239-43a6-8505-a321ad622e9a')"><img id="code_img_closed_cf501f9c-6239-43a6-8505-a321ad622e9a" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_cf501f9c-6239-43a6-8505-a321ad622e9a" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('cf501f9c-6239-43a6-8505-a321ad622e9a',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_cf501f9c-6239-43a6-8505-a321ad622e9a" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> IdentityModel.Client;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Net.Http;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ThreeClient
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">访问授权服务器</span>
            <span style="color: #0000ff;">var</span> diso= DiscoveryClient.GetAsync(<span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:5000</span><span style="color: #800000;">"</span><span style="color: #000000;">).Result;
            </span><span style="color: #0000ff;">if</span><span style="color: #000000;">(diso.IsError)
            {
                Console.WriteLine(diso.Error);
            }
            </span><span style="color: #0000ff;">var</span> tokenClient=<span style="color: #0000ff;">new</span> TokenClient(diso.TokenEndpoint,<span style="color: #800000;">"</span><span style="color: #800000;">123</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">secret</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            </span><span style="color: #0000ff;">var</span> res= tokenClient.RequestResourceOwnerPasswordAsync(<span style="color: #800000;">"</span><span style="color: #800000;">hunter</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">123456</span><span style="color: #800000;">"</span><span style="color: #000000;">).Result;
            </span><span style="color: #0000ff;">if</span><span style="color: #000000;">(res.IsError)
            {
                Console.WriteLine(res.Error);
            }
            </span><span style="color: #0000ff;">else</span><span style="color: #000000;">
            {
                Console.WriteLine(res.Json);
            }

            </span><span style="color: #008000;">//</span><span style="color: #008000;">访问资源服务器</span>
            <span style="color: #0000ff;">var</span> client=<span style="color: #0000ff;">new</span><span style="color: #000000;"> HttpClient();
            client.SetBearerToken(res.AccessToken);
            </span><span style="color: #0000ff;">var</span> result= client.GetAsync(<span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:5001/api/values</span><span style="color: #800000;">"</span><span style="color: #000000;">).Result;
            </span><span style="color: #0000ff;">if</span><span style="color: #000000;">(result.IsSuccessStatusCode)
            {
                Console.WriteLine(result.Content.ReadAsStringAsync().Result);
            }
            </span><span style="color: #0000ff;">else</span><span style="color: #000000;">
            {
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">失败</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }

        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Program</span></div>
<p>案例下载：<a href="https://pan.baidu.com/s/1zoX3P5yuktW_HaaOGRGFOQ" target="_blank">https://pan.baidu.com/s/1zoX3P5yuktW_HaaOGRGFOQ</a></p>
<p>&nbsp;</p>
<p>2，刷新token</p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201805/741594-20180522172653664-809736377.png" alt="" width="711" height="279" />,&nbsp;</p>
<p>&nbsp;</p>
<p>3，OAuth2.0密码模式（数据库操作）</p>
<p>&nbsp;</p>
<p>4，OIDC（内存模式）</p>
<p>①介绍</p>
<p>OpenID Connect是OpenID的升级版，简称OIDC。OIDC使用OAuth2的授权服务器来为第三方客户端提供用户的身份认证，并把对应的身份认证信息传递给客户端&nbsp;。</p>
<p>OAuth2.0主要用于授权。OIDC主要用来认证</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>5，OIDC（数据库模式）</p>
<p>&nbsp;</p>