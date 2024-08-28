<p>&nbsp;</p>
<p>参考文档：<a href="https://dotnet.github.io/orleans/Tutorials/index.html" target="_blank">https://dotnet.github.io/orleans/Tutorials/index.html</a></p>
<p>一、通过模板创建Orleans</p>
<p>①下载vs插件：<a href="https://marketplace.visualstudio.com/items?itemName=sbykov.MicrosoftOrleansToolsforVisualStudio">https://marketplace.visualstudio.com/items?itemName=sbykov.MicrosoftOrleansToolsforVisualStudio</a></p>
<p>②通过模板添加</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201801/741594-20180124142151444-482368539.png" alt="" width="568" height="227" /></p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201801/741594-20180124142226412-1443224356.png" alt="" width="212" height="300" /></p>
<p>③引用关系</p>
<p>Grains引用GrainInterfaces</p>
<p>Host引用&nbsp;Grains、GrainInterfaces</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('fc3426a3-7cf2-42ba-8b10-ba75d7804001')"><img id="code_img_closed_fc3426a3-7cf2-42ba-8b10-ba75d7804001" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_fc3426a3-7cf2-42ba-8b10-ba75d7804001" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('fc3426a3-7cf2-42ba-8b10-ba75d7804001',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_fc3426a3-7cf2-42ba-8b10-ba75d7804001" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Orleans;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> GrainInterfaces
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> ITestGrain:IGrainWithGuidKey
    {
        Task Run();
        Task</span>&lt;<span style="color: #0000ff;">string</span>&gt;<span style="color: #000000;"> Get();
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">GrainInterfaces-ITestGrain</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('9d95a775-9bce-4bc9-b6e4-9563ed38d1af')"><img id="code_img_closed_9d95a775-9bce-4bc9-b6e4-9563ed38d1af" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_9d95a775-9bce-4bc9-b6e4-9563ed38d1af" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('9d95a775-9bce-4bc9-b6e4-9563ed38d1af',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_9d95a775-9bce-4bc9-b6e4-9563ed38d1af" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Orleans;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> GrainInterfaces;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> Grains
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> TestGrain : Grain, ITestGrain
    {
        </span><span style="color: #0000ff;">public</span> Task&lt;<span style="color: #0000ff;">string</span>&gt;<span style="color: #000000;"> Get()
        {
            </span><span style="color: #0000ff;">return</span> Task.FromResult(<span style="color: #0000ff;">this</span>.GetType().FullName + <span style="color: #800000;">"</span><span style="color: #800000;">.Get()</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Task Run()
        {
            Console.WriteLine(</span><span style="color: #0000ff;">this</span>.GetType().FullName + <span style="color: #800000;">"</span><span style="color: #800000;">.Run()</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> Task.CompletedTask;
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Grains-TestGrain</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('eda4228c-4fd2-4544-9684-074d9aa26539')"><img id="code_img_closed_eda4228c-4fd2-4544-9684-074d9aa26539" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_eda4228c-4fd2-4544-9684-074d9aa26539" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('eda4228c-4fd2-4544-9684-074d9aa26539',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_eda4228c-4fd2-4544-9684-074d9aa26539" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;

</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Orleans;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Orleans.Runtime.Configuration;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Orleans.Runtime.Host;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> GrainInterfaces;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> Host
{
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
    <span style="color: #808080;">///</span><span style="color: #008000;"> Orleans test silo host
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> 首先，配置并启动一个本地silo</span>
            <span style="color: #0000ff;">var</span> siloConfig =<span style="color: #000000;"> ClusterConfiguration.LocalhostPrimarySilo();
            </span><span style="color: #0000ff;">var</span> silo = <span style="color: #0000ff;">new</span> SiloHost(<span style="color: #800000;">"</span><span style="color: #800000;">TestSilo</span><span style="color: #800000;">"</span><span style="color: #000000;">, siloConfig);
            silo.InitializeOrleansSilo();
            silo.StartOrleansSilo();

            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">Silo started.</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;"> 然后配置并连接一个客户端。</span>
            <span style="color: #0000ff;">var</span> clientConfig =<span style="color: #000000;"> ClientConfiguration.LocalhostSilo();
            </span><span style="color: #0000ff;">var</span> client = <span style="color: #0000ff;">new</span><span style="color: #000000;"> ClientBuilder().UseConfiguration(clientConfig).Build();
            client.Connect().Wait();

            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">Client connected.</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span>
            <span style="color: #008000;">//</span><span style="color: #008000;"> 这是你测试代码的地方
            </span><span style="color: #008000;">//
</span>            <span style="color: #0000ff;">var</span> testGrain = client.GetGrain&lt;ITestGrain&gt;<span style="color: #000000;">(Guid.Empty);
            </span><span style="color: #0000ff;">while</span> (<span style="color: #0000ff;">true</span><span style="color: #000000;">) {
                Console.ReadKey();
                testGrain.Run();
                Console.WriteLine(testGrain.Get().Result);

                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">\nPress Enter to terminate...</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                Console.ReadLine();
            }

            </span><span style="color: #008000;">//</span><span style="color: #008000;"> 关掉</span>
<span style="color: #000000;">            client.Close();
            silo.ShutdownOrleansSilo();
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Host-Program</span></div>
<p>下载地址：<a href="https://pan.baidu.com/s/1c3OO0zY" target="_blank">https://pan.baidu.com/s/1c3OO0zY</a></p>
<p>&nbsp;</p>