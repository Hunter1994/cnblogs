<p><strong>1，在abp官网下载的模板（asp.net+ef）写Application层的时候需要使用AutoMapper。结果ObjectMapper一直为null</strong></p>
<p>解决：需要在当前项目的Module依赖AbpAutoMapperModule</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201709/741594-20170905164325616-609509840.png" alt="" /></p>
<p>&nbsp;</p>
<p><strong>2，Linq&nbsp;Include扩展方法需要引用EntityFramework.dll</strong></p>
<p>&nbsp;</p>
<p><strong>3,ToListAsync扩展方法需要引用using&nbsp;Abp.Linq.Extensions;</strong></p>
<p>&nbsp;</p>
<p><strong>4,手动搭建abp2.x老是出现System.Collections.Immutable1.2.1.0找不到</strong></p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201709/741594-20170914141751032-1662633003.jpg" alt="" /></p>
<p>解决：</p>
<p>①编辑项目web.config改为（这个可以不管）</p>
<div class="cnblogs_code">
<pre>      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">dependentAssembly</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">assemblyIdentity </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="System.Collections.Immutable"</span><span style="color: #ff0000;"> publicKeyToken</span><span style="color: #0000ff;">="b03f5f7f11d50a3a"</span><span style="color: #ff0000;"> culture</span><span style="color: #0000ff;">="neutral"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">bindingRedirect </span><span style="color: #ff0000;">oldVersion</span><span style="color: #0000ff;">="0.0.0.0-1.2.1.0"</span><span style="color: #ff0000;"> newVersion</span><span style="color: #0000ff;">="1.2.1.0"</span> <span style="color: #0000ff;">/&gt;</span>
      <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">dependentAssembly</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>②编辑项目工程文件（例如Demo.Web.csproj文件）</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201709/741594-20170914143440610-2097135910.png" alt="" /></p>
<p>&nbsp;案例下载：<a href="http://pan.baidu.com/s/1kU7By31" target="_blank">http://pan.baidu.com/s/1kU7By31</a></p>
<p>&nbsp;</p>
<p><strong>5，创建租户（独立数据库）报MSDTC 不可用</strong></p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201710/741594-20171026222306992-992134892.png" alt="" width="333" height="241" /></p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201710/741594-20171026222341023-879523373.png" alt="" /></p>
<p>解决方案：</p>
<p>打开windows服务开启Distributed Transaction Coordinator服务</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201710/741594-20171026222456617-1739842337.png" alt="" /></p>
<p>&nbsp;</p>
<p><strong>6，单元测试时老是报个错：</strong></p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201710/741594-20171030221918355-1463449858.png" alt="" /></p>
<p>解决：</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201710/741594-20171030221958402-2110434623.png" alt="" /></p>
<p>单元测试Module需要依赖<strong>AbpTestBaseModule</strong></p>
<p>&nbsp;</p>
<p><strong>7，运行模板项目报错</strong></p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201711/741594-20171107163242919-1144581948.png" alt="" /></p>
<p>解决办法：删除项目下的bin目录，然后重新编译就好了</p>
<p>&nbsp;</p>
<p><strong>8， 把Abp.Zero.Common添加到项目报错</strong></p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201712/741594-20171204220218972-1741116725.png" alt="" /></p>
<p>解决方法：</p>
<p>在Abp.Zero.Common.csproj文件中删除</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201712/741594-20171204220225941-23273966.png" alt="" /></p>
<p>&nbsp;</p>
<p><strong>9，本地化失效</strong></p>
<p>解决方法：需要把xml设置为嵌入的资源</p>
<p>&nbsp;</p>
<p><strong>10，更改提示变成中文&nbsp;</strong></p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201808/741594-20180823190017695-701036412.png" alt="" width="567" height="224" /></p>
<p>扩展本地化文件</p>
<p>在Ousutec.Duty.Core中的DutyLocalizationConfigurer的Configure方法加上扩展配置</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('5116524d-f2cf-4303-b450-7439ded376f9')"><img id="code_img_closed_5116524d-f2cf-4303-b450-7439ded376f9" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_5116524d-f2cf-4303-b450-7439ded376f9" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('5116524d-f2cf-4303-b450-7439ded376f9',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_5116524d-f2cf-4303-b450-7439ded376f9" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Configuration.Startup;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Localization.Dictionaries;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Localization.Dictionaries.Xml;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Localization.Sources;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Reflection.Extensions;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> Ousutec.Duty.Localization
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> DutyLocalizationConfigurer
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configure(ILocalizationConfiguration localizationConfiguration)
        {
            localizationConfiguration.Sources.Add(
                </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> DictionaryBasedLocalizationSource(DutyConsts.LocalizationSourceName,
                    </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> XmlEmbeddedFileLocalizationDictionaryProvider(
                        </span><span style="color: #0000ff;">typeof</span><span style="color: #000000;">(DutyLocalizationConfigurer).GetAssembly(),
                        </span><span style="color: #800000;">"</span><span style="color: #800000;">Ousutec.Duty.Localization.SourceFiles</span><span style="color: #800000;">"</span><span style="color: #000000;">
                    )
                )
            );

            localizationConfiguration.Sources.Extensions.Add(
                </span><span style="color: #0000ff;">new</span> LocalizationSourceExtensionInfo(<span style="color: #800000;">"</span><span style="color: #800000;">AbpWeb</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> XmlEmbeddedFileLocalizationDictionaryProvider(
                        </span><span style="color: #0000ff;">typeof</span><span style="color: #000000;">(DutyLocalizationConfigurer).GetAssembly(),
                        </span><span style="color: #800000;">"</span><span style="color: #800000;">Ousutec.Duty.Localization.AbpWebExtensions</span><span style="color: #800000;">"</span><span style="color: #000000;">
                        )
                    )
                );
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">DutyLocalizationConfigurer</span></div>
<p>将Abp.Web.Common源码的AbpWeb-zh-Hans.xml复制到Ousutec.Duty.Core项目中。并嵌入资源</p>
<p>&nbsp;</p>
<p><strong>11，关于自动注册依赖</strong></p>
<p>约定名称必须一直，例如</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('eedb4461-1c45-4a77-9ccf-8e4b4e70d3a9')"><img id="code_img_closed_eedb4461-1c45-4a77-9ccf-8e4b4e70d3a9" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_eedb4461-1c45-4a77-9ccf-8e4b4e70d3a9" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('eedb4461-1c45-4a77-9ccf-8e4b4e70d3a9',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_eedb4461-1c45-4a77-9ccf-8e4b4e70d3a9" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Castle.Core.Logging;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Ousutec.Duty.Common;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Newtonsoft.Json;

</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Dependency;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Ousutec.Duty.DutyCmds;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.AutoMapper;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> Ousutec.Duty.RabbitMqListeners
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> DutyCmdListener : IDutyCmdListener, ITransientDependency
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> ILogger _logger;
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> IDutyCmdAppService _dutyCmdAppService;
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> DutyCmdListener(ILogger logger, IDutyCmdAppService dutyCmdAppService)
        {
            _logger </span>=<span style="color: #000000;"> logger;
            _dutyCmdAppService </span>=<span style="color: #000000;"> dutyCmdAppService;
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> ProcessMsg(DutyCmdMessage msg)
        {
            _logger.Info(JsonConvert.SerializeObject(msg));
            _dutyCmdAppService.Add(msg.DutyCmdDtos.MapTo</span>&lt;IEnumerable&lt;Addinput&gt;&gt;<span style="color: #000000;">());
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">DutyCmdListener</span></div>
<p>不一致会&nbsp;报找不到依赖异常</p>
<p>&nbsp;</p>
<p><strong>12，Swagger&nbsp;CustomSchemaIds错误</strong></p>
<p>Conflicting schemaIds: Identical schemaIds detected for types Ousutec.Duty.DutyRecords.AddInput and Ousutec.Duty.DutyDevSettings.AddInput. See config settings - "CustomSchemaIds" for a workaround</p>
<p>解决方法：&nbsp;<span class="cnblogs_code"> options.CustomSchemaIds(t =&gt; t.FullName);</span>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('5e2ec8d0-53f0-4f9e-bdaa-81c2f6f63ab7')"><img id="code_img_closed_5e2ec8d0-53f0-4f9e-bdaa-81c2f6f63ab7" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_5e2ec8d0-53f0-4f9e-bdaa-81c2f6f63ab7" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('5e2ec8d0-53f0-4f9e-bdaa-81c2f6f63ab7',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_5e2ec8d0-53f0-4f9e-bdaa-81c2f6f63ab7" class="cnblogs_code_hide">
<pre>            <span style="color: #008000;">//</span><span style="color: #008000;"> Swagger - Enable this line and the related lines in Configure method to enable swagger UI</span>
            services.AddSwaggerGen(options =&gt;<span style="color: #000000;">
            {
                options.SwaggerDoc(</span><span style="color: #800000;">"</span><span style="color: #800000;">v1</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span> Info { Title = <span style="color: #800000;">"</span><span style="color: #800000;">Duty API</span><span style="color: #800000;">"</span>, Version = <span style="color: #800000;">"</span><span style="color: #800000;">v1</span><span style="color: #800000;">"</span><span style="color: #000000;"> });
                options.DocInclusionPredicate((docName, description) </span>=&gt; <span style="color: #0000ff;">true</span><span style="color: #000000;">);

                options.CustomSchemaIds(t </span>=&gt;<span style="color: #000000;"> t.FullName);
                </span><span style="color: #008000;">//</span><span style="color: #008000;"> Define the BearerAuth scheme that's in use</span>
                options.AddSecurityDefinition(<span style="color: #800000;">"</span><span style="color: #800000;">bearerAuth</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span><span style="color: #000000;"> ApiKeyScheme()
                {
                    Description </span>= <span style="color: #800000;">"</span><span style="color: #800000;">JWT Authorization header using the Bearer scheme. Example: \"Authorization: Bearer {token}\"</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    Name </span>= <span style="color: #800000;">"</span><span style="color: #800000;">Authorization</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    In </span>= <span style="color: #800000;">"</span><span style="color: #800000;">header</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    Type </span>= <span style="color: #800000;">"</span><span style="color: #800000;">apiKey</span><span style="color: #800000;">"</span><span style="color: #000000;">
                });
                </span><span style="color: #008000;">//</span><span style="color: #008000;"> Assign scope requirements to operations based on AuthorizeAttribute</span>
                options.OperationFilter&lt;SecurityRequirementsOperationFilter&gt;<span style="color: #000000;">();
            });</span></pre>
</div>
<span class="cnblogs_code_collapse">Startup</span></div>
<p>&nbsp;</p>
<p><strong>13，接口返回参数命名，忽略abp框架设置的命名规则</strong></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('0be724fc-780e-4064-b1c4-871274904e36')"><img id="code_img_closed_0be724fc-780e-4064-b1c4-871274904e36" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_0be724fc-780e-4064-b1c4-871274904e36" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('0be724fc-780e-4064-b1c4-871274904e36',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_0be724fc-780e-4064-b1c4-871274904e36" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Reflection;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Mvc;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Builder;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Hosting;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Mvc.Cors.Internal;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.Configuration;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Extensions.DependencyInjection;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Castle.Facilities.Logging;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Swashbuckle.AspNetCore.Swagger;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.AspNetCore;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Castle.Logging.Log4Net;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Extensions;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Ousu.DataCollection.Attendance.Authentication.JwtBearer;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Ousu.DataCollection.Attendance.Configuration;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Ousu.DataCollection.Attendance.Identity;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Ousu.DataCollection.Attendance.Common;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.AspNetCore.SignalR.Hubs;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Ousu.DataCollection.Attendance.AttendanceCmds;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Dependency;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Castle.Windsor.MsDependencyInjection;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Aliyun.OSS;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Castle.Core.Logging;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Json;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Newtonsoft.Json.Serialization;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> Ousu.DataCollection.Attendance.Web.Host.Startup
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Startup
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">const</span> <span style="color: #0000ff;">string</span> _defaultCorsPolicyName = <span style="color: #800000;">"</span><span style="color: #800000;">localhost</span><span style="color: #800000;">"</span><span style="color: #000000;">;

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> IConfigurationRoot _appConfiguration;


        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Startup(IHostingEnvironment env)
        {
            _appConfiguration </span>=<span style="color: #000000;"> env.GetAppConfiguration();
        }

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> IServiceProvider ConfigureServices(IServiceCollection services)
        {

            </span><span style="color: #008000;">//</span><span style="color: #008000;"> MVC</span>
<span style="color: #000000;">            services.AddMvc(
                options </span>=&gt;<span style="color: #000000;">
                {
                    options.Filters.Add(</span><span style="color: #0000ff;">new</span><span style="color: #000000;"> CorsAuthorizationFilterFactory(_defaultCorsPolicyName));
                }
            );

            IdentityRegistrar.Register(services);
            AuthConfigurer.Configure(services, _appConfiguration);

            services.AddSignalR();

            </span><span style="color: #008000;">//</span><span style="color: #008000;"> Configure CORS for angular2 UI</span>
<span style="color: #000000;">            services.AddCors(
                options </span>=&gt;<span style="color: #000000;"> options.AddPolicy(
                    _defaultCorsPolicyName,
                    builder </span>=&gt;<span style="color: #000000;"> builder
                        .WithOrigins(
                            </span><span style="color: #008000;">//</span><span style="color: #008000;"> App:CorsOrigins in appsettings.json can contain more than one address separated by comma.</span>
                            _appConfiguration[<span style="color: #800000;">"</span><span style="color: #800000;">App:CorsOrigins</span><span style="color: #800000;">"</span><span style="color: #000000;">]
                                .Split(</span><span style="color: #800000;">"</span><span style="color: #800000;">,</span><span style="color: #800000;">"</span><span style="color: #000000;">, StringSplitOptions.RemoveEmptyEntries)
                                .Select(o </span>=&gt; o.RemovePostFix(<span style="color: #800000;">"</span><span style="color: #800000;">/</span><span style="color: #800000;">"</span><span style="color: #000000;">))
                                .ToArray()
                        )
                        .AllowAnyHeader()
                        .AllowAnyMethod()
                        .AllowCredentials()
                )
            );

            </span><span style="color: #008000;">//</span><span style="color: #008000;"> Swagger - Enable this line and the related lines in Configure method to enable swagger UI</span>
            services.AddSwaggerGen(options =&gt;<span style="color: #000000;">
            {
                options.SwaggerDoc(</span><span style="color: #800000;">"</span><span style="color: #800000;">v1</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span> Info { Title = <span style="color: #800000;">"</span><span style="color: #800000;">Attendance API</span><span style="color: #800000;">"</span>, Version = <span style="color: #800000;">"</span><span style="color: #800000;">v1</span><span style="color: #800000;">"</span><span style="color: #000000;"> });
                options.DocInclusionPredicate((docName, description) </span>=&gt; <span style="color: #0000ff;">true</span><span style="color: #000000;">);

                options.CustomSchemaIds(t </span>=&gt;<span style="color: #000000;"> t.FullName);
                </span><span style="color: #008000;">//</span><span style="color: #008000;"> Define the BearerAuth scheme that's in use</span>
                options.AddSecurityDefinition(<span style="color: #800000;">"</span><span style="color: #800000;">bearerAuth</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span><span style="color: #000000;"> ApiKeyScheme()
                {
                    Description </span>= <span style="color: #800000;">"</span><span style="color: #800000;">JWT Authorization header using the Bearer scheme. Example: \"Authorization: Bearer {token}\"</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    Name </span>= <span style="color: #800000;">"</span><span style="color: #800000;">Authorization</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    In </span>= <span style="color: #800000;">"</span><span style="color: #800000;">header</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    Type </span>= <span style="color: #800000;">"</span><span style="color: #800000;">apiKey</span><span style="color: #800000;">"</span><span style="color: #000000;">
                });
                </span><span style="color: #008000;">//</span><span style="color: #008000;"> Assign scope requirements to operations based on AuthorizeAttribute</span>
                options.OperationFilter&lt;SecurityRequirementsOperationFilter&gt;<span style="color: #000000;">();
            });

            </span><span style="color: #008000;">//</span><span style="color: #008000;">去除abp框架自带的命名规则</span>
            services.PostConfigure&lt;MvcJsonOptions&gt;(options =&gt;<span style="color: #000000;">
            {
                options.SerializerSettings.ContractResolver </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> AbpContractResolver();
            });

            </span><span style="color: #008000;">//</span><span style="color: #008000;"> Configure Abp and Dependency Injection </span>
            <span style="color: #0000ff;">return</span> services.AddAbp&lt;AttendanceWebHostModule&gt;<span style="color: #000000;">(
                </span><span style="color: #008000;">//</span><span style="color: #008000;"> Configure Log4Net logging</span>
                options =&gt;<span style="color: #000000;">
                {
                    options.IocManager.IocContainer.AddFacility</span>&lt;LoggingFacility&gt;(f =&gt; f.UseAbpLog4Net().WithConfig(<span style="color: #800000;">"</span><span style="color: #800000;">log4net.config</span><span style="color: #800000;">"</span><span style="color: #000000;">));
                }
            );
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configure(IApplicationBuilder app, IHostingEnvironment env, ILoggerFactory loggerFactory)
        {
            app.UseAbp(options </span>=&gt; { options.UseAbpRequestLocalization = <span style="color: #0000ff;">false</span>;}); <span style="color: #008000;">//</span><span style="color: #008000;"> Initializes ABP framework.</span>
<span style="color: #000000;">
            app.UseCors(_defaultCorsPolicyName); </span><span style="color: #008000;">//</span><span style="color: #008000;"> Enable CORS!</span>
<span style="color: #000000;">
            app.UseStaticFiles();

            app.UseAuthentication();

            app.UseAbpRequestLocalization();

            app.UseSignalR(routes </span>=&gt;<span style="color: #000000;">
            {
                routes.MapHub</span>&lt;AbpCommonHub&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">/signalr</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            });

            app.UseMvc(routes </span>=&gt;<span style="color: #000000;">
            {
                routes.MapRoute(
                    name: </span><span style="color: #800000;">"</span><span style="color: #800000;">defaultWithArea</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    template: </span><span style="color: #800000;">"</span><span style="color: #800000;">{area}/{controller=Home}/{action=Index}/{id?}</span><span style="color: #800000;">"</span><span style="color: #000000;">);

                routes.MapRoute(
                    name: </span><span style="color: #800000;">"</span><span style="color: #800000;">default</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    template: </span><span style="color: #800000;">"</span><span style="color: #800000;">{controller=Home}/{action=Index}/{id?}</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            });

            </span><span style="color: #008000;">//</span><span style="color: #008000;"> Enable middleware to serve generated Swagger as a JSON endpoint</span>
<span style="color: #000000;">            app.UseSwagger();
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> Enable middleware to serve swagger-ui assets (HTML, JS, CSS etc.)</span>
            app.UseSwaggerUI(options =&gt;<span style="color: #000000;">
            {
                options.SwaggerEndpoint(_appConfiguration[</span><span style="color: #800000;">"</span><span style="color: #800000;">App:ServerRootAddress</span><span style="color: #800000;">"</span>] + <span style="color: #800000;">"</span><span style="color: #800000;">/swagger/v1/swagger.json</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">Attendance API V1</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                options.IndexStream </span>= () =&gt;<span style="color: #000000;"> Assembly.GetExecutingAssembly()
                    .GetManifestResourceStream(</span><span style="color: #800000;">"</span><span style="color: #800000;">Ousu.DataCollection.Attendance.Web.Host.wwwroot.swagger.ui.index.html</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }); </span><span style="color: #008000;">//</span><span style="color: #008000;"> URL: /swagger</span>
<span style="color: #000000;">        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">去除abp框架自带的命名规则</span></div>
<p>&nbsp;</p>
<p><strong>14，不使用abp框架自带的返回格式</strong></p>
<p>在类或者方法上加上[DontWrapResult]特性</p>
<p>&nbsp;</p>