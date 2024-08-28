<p>1，添加引用</p>
<pre>&lt;GenerateDocumentationFile&gt;true&lt;/GenerateDocumentationFile&gt;
    &lt;NoWarn&gt;$(NoWarn);1591&lt;/NoWarn&gt; 生成注释文件</pre>
<div class="cnblogs_code">
<pre>&lt;Project Sdk=<span style="color: #800000;">"</span><span style="color: #800000;">Microsoft.NET.Sdk.Web</span><span style="color: #800000;">"</span>&gt;

  &lt;PropertyGroup&gt;
 &lt;GenerateDocumentationFile&gt;<span style="color: #0000ff;">true</span>&lt;/GenerateDocumentationFile&gt;
    &lt;NoWarn&gt;$(NoWarn);<span style="color: #800080;">1591</span>&lt;/NoWarn&gt;
  &lt;/PropertyGroup&gt;

  &lt;ItemGroup&gt;
    &lt;PackageReference Include=<span style="color: #800000;">"</span><span style="color: #800000;">Swashbuckle.AspNetCore</span><span style="color: #800000;">"</span> Version=<span style="color: #800000;">"</span><span style="color: #800000;">5.5.0</span><span style="color: #800000;">"</span> /&gt;
  &lt;/ItemGroup&gt;


&lt;/Project&gt;</pre>
</div>
<p>2，添加服务、中间件</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Builder;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Hosting;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.HttpsPolicy;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Mvc;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Configuration;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.DependencyInjection;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Hosting;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Logging;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.OpenApi.Models;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Reflection;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.IO;


</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> swaggerdemo
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

            services.AddControllers();
            </span><span style="color: #008000;">//</span><span style="color: #008000;">注册Swagger生成器，定义一个或多个Swagger文档</span>
            services.AddSwaggerGen(c =&gt;<span style="color: #000000;">
            {
                c.ResolveConflictingActions(api</span>=&gt;api.Last());<span style="color: #008000;">//</span><span style="color: #008000;">同样的接口名 传递了不同参数，使用第一个api名称</span>
                c.SwaggerDoc(<span style="color: #800000;">"</span><span style="color: #800000;">v1</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span><span style="color: #000000;"> OpenApiInfo()
                {</span><span style="color: #008000;">//</span><span style="color: #008000;">添加描述信息</span>
                    Version = <span style="color: #800000;">"</span><span style="color: #800000;">v1</span><span style="color: #800000;">"</span>,<span style="color: #008000;">//</span><span style="color: #008000;">描述文档的版本</span>
                    Title = <span style="color: #800000;">"</span><span style="color: #800000;">openapi</span><span style="color: #800000;">"</span>,<span style="color: #008000;">//</span><span style="color: #008000;">描述文档的标题</span>
                    Description = <span style="color: #800000;">"</span><span style="color: #800000;">这个一个对外的文档</span><span style="color: #800000;">"</span>,<span style="color: #008000;">//</span><span style="color: #008000;">描述信息</span>
                    TermsOfService = <span style="color: #0000ff;">new</span> Uri(<span style="color: #800000;">"</span><span style="color: #800000;">https://www.baidu.com</span><span style="color: #800000;">"</span>),<span style="color: #008000;">//</span><span style="color: #008000;">服务条款</span>
                    Contact = <span style="color: #0000ff;">new</span> OpenApiContact()<span style="color: #008000;">//</span><span style="color: #008000;">联系方式</span>
<span style="color: #000000;">                    {
                        Name </span>= <span style="color: #800000;">"</span><span style="color: #800000;">张迪</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                        Email </span>= <span style="color: #800000;">"</span><span style="color: #800000;">123@qq.com</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                        Url </span>= <span style="color: #0000ff;">new</span> Uri(<span style="color: #800000;">"</span><span style="color: #800000;">https://www.zhangdi.com</span><span style="color: #800000;">"</span><span style="color: #000000;">)
                    },
                    License </span>= <span style="color: #0000ff;">new</span> OpenApiLicense()<span style="color: #008000;">//</span><span style="color: #008000;">许可证</span>
<span style="color: #000000;">                    {
                        Name </span>= <span style="color: #800000;">"</span><span style="color: #800000;">Use under LICX</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                        Url </span>= <span style="color: #0000ff;">new</span> Uri(<span style="color: #800000;">"</span><span style="color: #800000;">https://example.com/license</span><span style="color: #800000;">"</span><span style="color: #000000;">)
                    }
                });
                </span><span style="color: #0000ff;">var</span> xmlFile = $<span style="color: #800000;">"</span><span style="color: #800000;">{Assembly.GetExecutingAssembly().GetName().Name}.xml</span><span style="color: #800000;">"</span><span style="color: #000000;">;
                </span><span style="color: #0000ff;">var</span> xmlPath =<span style="color: #000000;"> Path.Combine(AppContext.BaseDirectory, xmlFile);
                c.IncludeXmlComments(xmlPath);
            });




        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> This method gets called by the runtime. Use this method to configure the HTTP request pipeline.</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configure(IApplicationBuilder app, IWebHostEnvironment env)
        {
            </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (env.IsDevelopment())
            {
                app.UseDeveloperExceptionPage();
            }

            </span><span style="color: #008000;">//</span><span style="color: #008000;">允许中间件将生成的Swagger作为JSON端点提供</span>
<span style="color: #000000;">            app.UseSwagger();
            </span><span style="color: #008000;">//</span><span style="color: #008000;">启用中间件来服务Swagger -ui (HTML, JS, CSS等)，指定Swagger JSON端点。</span>
            app.UseSwaggerUI(options =&gt;<span style="color: #000000;">
            {
                options.SwaggerEndpoint(</span><span style="color: #800000;">"</span><span style="color: #800000;">/swagger/v1/swagger.json</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">版本1</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                options.RoutePrefix </span>= <span style="color: #0000ff;">string</span>.Empty;<span style="color: #008000;">//</span><span style="color: #008000;">要在应用程序的根目录（</span><span style="color: #008000; text-decoration: underline;">http://localhost</span><span style="color: #008000;">:&lt;port&gt;/）提供Swagger UI</span>
<span style="color: #000000;">            });

            app.UseHttpsRedirection();

            app.UseRouting();

            app.UseAuthorization();

            app.UseEndpoints(endpoints </span>=&gt;<span style="color: #000000;">
            {
                endpoints.MapControllers();
            });
        }
    }
}</span></pre>
</div>
<p>&nbsp;</p>