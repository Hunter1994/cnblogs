<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">一、托管堆基础</span></p>
<p><strong><span style="font-size: 18px;">1，访问一个资源（文件、内存缓冲区、屏幕空间、网络连接、数据库资源等）所需的步骤</span></strong></p>
<p>①调用IL指令newobj，为代表资源的类型分配内存（一般使用c# new操作符来完成）</p>
<p>②初始化内存，设置资源的初始状态并使资源可用。类型的实例构造器负责设置初始状态</p>
<p>③访问类型的成员来使用资源（有必要可以重复）</p>
<p>④摧毁资源的状态以进行清理</p>
<p>⑤释放内存。垃圾回收器独自负责这一步</p>
<p>&nbsp;</p>
<p><strong><span style="font-size: 18px;">2，从托管堆分配资源</span></strong></p>
<p>初始化进程时，CLR划出一个地址空间区域作为托管堆，一个区域被非垃圾对象填满后，CLR会分配更多的区域（32位进程最多能分配1.5GB，64为进程最多能分配8TB）。CLR还要维护一个指针（NextObjPtr），该指针指向下一个对象在堆中的分配位值。刚开始的时候，NextObjPtr设为地址空间区域的基地址。</p>
<p>&nbsp;</p>
<p><strong><span style="font-size: 18px;">3，C#的new操作符导致CLR执行以下步骤</span></strong></p>
<p>①计算类型的字段（以及从基类型继承的字段）所需的字节数。</p>
<p>②加上对象的开销所需的字节数。每个对象都有两个开销字段：类型对象指针和同步快索引（32位：两个字段各需32位，所以每个对象要增加8字节。64位：每个字段各需64位，所以每个对象要增加16字节）（int=4字节；long=8字节）</p>
<p>③CLR检查区域中是否有分配对象所需的字节数。如果托管堆有足够的可用空间，就在NextObjPtr指针指向的地址处放入对象，为对象分配的字节会被清零。接着调用类型的构造器（为this参数传递NextObjPtr），new操作符返回对象的引用。就在返回这个引用之前，NextObjPtr指针的值会加上对象占用的字节数来得到一个新值，即下一个对象放入托管堆是的地址</p>
<p>&nbsp;</p>
<p><strong><span style="font-size: 18px;">4，垃圾回收算法</span></strong></p>
<p>CLR使用一种引用跟踪算法。引用跟踪算法只关心引用类型的变量，因为只有这种变量才能引用堆上的对象，我们将所有引用类型的变量都称为<strong>根</strong>。</p>
<p>①CLR开始GC时，首先暂停进程中的所有线程（这样可以防止线程在CLR检查期间访问对象并更改其状态）</p>
<p>②CLR进入GC标记阶段（这个阶段，CLR遍历堆中所有对象，将同步块索引字段中的一位设为0。这表明所有的对象都应该删除）</p>
<p>③CLR检查所有活动根（根为null，则CLR忽略这个根），查看他们引用了那些对象。如果引用了堆上的对象，CLR都会标记那个对象（将对象的同步块索引中的位设置为1）</p>
<p>④检查完毕后，堆中的对象要么标记。要么未标记。已标记的对象不能被垃圾回收，因为至少有一个根在引用它，我们说这些对象时<strong>可达</strong>的</p>
<p>⑤进入GC的压缩阶段，在这个阶段，CLR对堆中已标记的对象进行&ldquo;乾坤大挪移&rdquo;，压缩所有幸存下来的对象，使它们占用连续的内存对象</p>
<p>⑥压缩之后，根现在的引用还是原来的位置，而非移动之后的位置。所以作为压缩阶段的一部分，CLR还要从每个根减去所引用的对象在内存中的偏移的字节数。这样就能保证根还是引用和之前一样的对象；只是对象在内存中换了位置</p>
<p>&nbsp;<img src="http://images2015.cnblogs.com/blog/741594/201707/741594-20170701163526102-595038334.png" alt="" /></p>
<p>&nbsp;</p>
<p><strong><span style="font-size: 18px;">5，垃圾回收和调试</span></strong></p>
<p>&nbsp;</p>
<p>①使用Release编译后，允许可执行文件，会发现TimerCallback方法只被调用了一次。因为Timer在初始化之后再也没有用过变量t。（调试模式下Timer对象不会被回收）</p>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建没2000毫秒就调用一次TimerCallback方法的timer对象</span>
            Timer t = <span style="color: #0000ff;">new</span> Timer(TimerCallback, <span style="color: #0000ff;">null</span>, <span style="color: #800080;">0</span>, <span style="color: #800080;">2000</span><span style="color: #000000;">);
            Console.ReadLine();
        }
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> TimerCallback(<span style="color: #0000ff;">object</span><span style="color: #000000;"> o)
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">a</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">出于演示目的，强制执行一次垃圾回收</span>
<span style="color: #000000;">            GC.Collect();
        }</span></pre>
</div>
<p>②显示要求释放计时器，它才能活到被释放的那一刻</p>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建没2000毫秒就调用一次TimerCallback方法的timer对象</span>
            Timer t = <span style="color: #0000ff;">new</span> Timer(TimerCallback, <span style="color: #0000ff;">null</span>, <span style="color: #800080;">0</span>, <span style="color: #800080;">2000</span><span style="color: #000000;">);
            Console.ReadLine();
            </span><span style="color: #008000;">//</span><span style="color: #008000;">在ReadLine之后引用t（在Dispose方法返回之前，t会在GC中存活）</span>
<span style="color: #000000;">            t.Dispose();
        }
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> TimerCallback(<span style="color: #0000ff;">object</span><span style="color: #000000;"> o)
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">a</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">出于演示目的，强制执行一次垃圾回收</span>
<span style="color: #000000;">            GC.Collect();
        }</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">二、代：提升性能</span></p>
<p>对象越新，生存期越短<br />对象越老，生存期越长<br />回收堆的一部分，速度快于回收整个堆<br /><span style="font-size: 18px;"><strong>1，原理</strong></span><br /><strong><span style="color: #ff0000;">①CLR初始化堆时为0代和1代选择预算容量（以kb为单位）。后期CLR会自动调节预算容量</span></strong><br /><strong><span style="color: #ff0000;">②如果分配一个新的对象造成第0代超过预算，就必须启动一次垃圾回收</span></strong><br /><strong><span style="color: #ff0000;">③经过垃圾回收之后，第0代的幸存者被提升到1代（第一代的大小增加）；第0代又空了出来</span></strong><br /><strong><span style="color: #ff0000;">④由于第0代已满，所以必须垃圾回收。但这一次垃圾回收器发现第1代用完了预算容量。所以这次垃圾回收器决定检查第1代和第0代的所有对象。两代被垃圾回收以后，第1代的幸存者提升到2代，第0代的幸存者提升到1代</span></strong></p>
<p><strong><span style="font-size: 18px;">2，垃圾回收触发的条件</span></strong><br />①最常见触发条件：CLR在检查第0代超过预算时触发一次GC<br />②代码显示调用Sytem.GC的静态Collect方法<br />③Windows报告底内存情况<br />④CLR正在卸载AppDomain<br />⑤CLR正在关闭（CLR在进程正常终止时）</p>
<p><strong><span style="font-size: 18px;">3，大对象</span></strong><br />目前认为85000字节或更大的对象时大对象。（之前讨论的都是小对象）。大对象一般是大字符串（比如XML或JSON）或者用于I/O操作的字节数组（比如从文件或网络将字节读入缓冲区一遍处理）<br />①大对象不是在小对象的地址空间分配，而是在进程地址空间的其他地方分配<br />②目前版本的GC不压缩大对象，因为在内存中移动它们的代价过高<br />③大对象总是第2代，绝不可能是第0代或者第1代</p>
<p><strong><span style="font-size: 18px;">4，垃圾回收模式</span></strong></p>
<p>CLR启动时会选择一个GC模式，进程终止前该模式不会变。</p>
<p>①两个主要模式：</p>
<p>1&gt;工作站</p>
<p>该模式针对客户端应用程序优化GC。GC造成的延时很低，应用程序线程挂起时间很短，避免是用户感到焦虑。</p>
<p>2&gt;服务器</p>
<p>该模式针对服务器应用程序优化GC。被优化的主要是吞吐量和资源利用。</p>
<p>②应用程序模式以&ldquo;工作站&rdquo;GC模式运行</p>
<p>③显示告诉CLR使用服务器回收站</p>
<div class="cnblogs_code">
<pre>  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">runtime</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">gcServer </span><span style="color: #ff0000;">enabled</span><span style="color: #0000ff;">="true"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">gcServer</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">runtime</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<div class="cnblogs_code">
<pre>            <span style="color: #008000;">//</span><span style="color: #008000;">询问CLR它是否在&ldquo;服务器&rdquo;GC模式中运行</span>
<span style="color: #000000;">            Console.WriteLine(GCSettings.IsServerGC);
            Console.ReadLine();</span></pre>
</div>
<p>&nbsp;④两个子模式（并发（默认）或非并发）</p>
<p>在并发模式中，垃圾回收器有一个额外的后台线性，它能在应用程序运行时并发标记对象</p>
<div class="cnblogs_code">
<pre>  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">runtime</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #008000;">&lt;!--</span><span style="color: #008000;">告诉CLR不要使用并发回收器</span><span style="color: #008000;">--&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">gcConcurrent </span><span style="color: #ff0000;">enabled</span><span style="color: #0000ff;">="false"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">gcConcurrent</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">runtime</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;⑤GCSettings的LatencyMode属性对垃圾回收进行某种程度的控制</p>
<table class="MsoTableGrid" style="border: none; height: 266px; width: 735px;" border="1" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td style="width: 118.8pt; border-color: windowtext; border-width: 1pt; padding: 0cm 5.4pt;" valign="top" width="158">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">符号名称</span></p>
</td>
<td style="width: 307.3pt; border-top-color: windowtext; border-right-color: windowtext; border-bottom-color: windowtext; border-top-width: 1pt; border-right-width: 1pt; border-bottom-width: 1pt; border-left-style: none; padding: 0cm 5.4pt;" valign="top" width="410">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">说明</span></p>
</td>
</tr>
<tr>
<td style="width: 118.8pt; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-right-width: 1pt; border-bottom-width: 1pt; border-left-width: 1pt; border-top-style: none; padding: 0cm 5.4pt;" valign="top" width="158">
<p class="MsoNormal"><span lang="EN-US">Batch(</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">&ldquo;服务器&rdquo;</span><span lang="EN-US">GC</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">模式的默认值</span><span lang="EN-US">)</span></p>
</td>
<td style="width: 307.3pt; border-top-style: none; border-left-style: none; border-bottom-color: windowtext; border-bottom-width: 1pt; border-right-color: windowtext; border-right-width: 1pt; padding: 0cm 5.4pt;" valign="top" width="410">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">关闭并发</span><span lang="EN-US">GC</span></p>
</td>
</tr>
<tr>
<td style="width: 118.8pt; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-right-width: 1pt; border-bottom-width: 1pt; border-left-width: 1pt; border-top-style: none; padding: 0cm 5.4pt;" valign="top" width="158">
<p class="MsoNormal"><span lang="EN-US">Interactive(</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">&ldquo;工作站&rdquo;</span><span lang="EN-US">GC</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">模式的默认值</span><span lang="EN-US">)</span></p>
</td>
<td style="width: 307.3pt; border-top-style: none; border-left-style: none; border-bottom-color: windowtext; border-bottom-width: 1pt; border-right-color: windowtext; border-right-width: 1pt; padding: 0cm 5.4pt;" valign="top" width="410">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">打开并发</span><span lang="EN-US">GC</span></p>
</td>
</tr>
<tr>
<td style="width: 118.8pt; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-right-width: 1pt; border-bottom-width: 1pt; border-left-width: 1pt; border-top-style: none; padding: 0cm 5.4pt;" valign="top" width="158">
<p class="MsoNormal">LowLatency</p>
</td>
<td style="width: 307.3pt; border-top-style: none; border-left-style: none; border-bottom-color: windowtext; border-bottom-width: 1pt; border-right-color: windowtext; border-right-width: 1pt; padding: 0cm 5.4pt;" valign="top" width="410">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">在短期的、时间敏感的操作中（如果动画绘制）使用这个延迟模式。这些操作不适合对第二代进行回收</span></p>
</td>
</tr>
<tr>
<td style="width: 118.8pt; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-right-width: 1pt; border-bottom-width: 1pt; border-left-width: 1pt; border-top-style: none; padding: 0cm 5.4pt;" valign="top" width="158">
<p class="MsoNormal"><span lang="EN-US">Sustained LowLatency</span></p>
</td>
<td style="width: 307.3pt; border-top-style: none; border-left-style: none; border-bottom-color: windowtext; border-bottom-width: 1pt; border-right-color: windowtext; border-right-width: 1pt; padding: 0cm 5.4pt;" valign="top" width="410">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">使用这个延迟模式，应用程序的大多数操作都不会发生长的</span><span lang="EN-US">GC</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">暂停。只要有足够的内存，它将禁止所有会造成阻塞的第二代回收操作。事实上，这种应用程序（例如需要迅速响应的股票软件）的用户应该考虑安装更多的</span><span lang="EN-US">RAM</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">来防止发生生长的</span><span lang="EN-US">GC</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">暂停</span></p>
</td>
</tr>
</tbody>
</table>
<p>⑥正确的使用LowLatency</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('e2a52125-84ab-48e9-92a1-a7b45a1fea06')"><img id="code_img_closed_e2a52125-84ab-48e9-92a1-a7b45a1fea06" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_e2a52125-84ab-48e9-92a1-a7b45a1fea06" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('e2a52125-84ab-48e9-92a1-a7b45a1fea06',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_e2a52125-84ab-48e9-92a1-a7b45a1fea06" class="cnblogs_code_hide">
<pre>        <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {

            GCLatencyMode oldModel </span>=<span style="color: #000000;"> GCSettings.LatencyMode;
            Console.WriteLine(oldModel);
            
            </span><span style="color: #008000;">//</span><span style="color: #008000;">约束执行区域（CER）</span>
<span style="color: #000000;">            System.Runtime.CompilerServices.RuntimeHelpers.PrepareConstrainedRegions();
            </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
            {
                GCSettings.LatencyMode </span>=<span style="color: #000000;"> GCLatencyMode.LowLatency;
                </span><span style="color: #008000;">//</span><span style="color: #008000;">在这里运行你的代码...</span>
<span style="color: #000000;">            }
            </span><span style="color: #0000ff;">finally</span><span style="color: #000000;">
            {
                GCSettings.LatencyMode </span>=<span style="color: #000000;"> oldModel;
            }
            Console.ReadLine();

        }</span></pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<p><strong><span style="font-size: 18px;">&nbsp;5，强制垃圾回收</span></strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Collect(<span style="color: #0000ff;">int</span> generation, System.GCCollectionMode mode, <span style="color: #0000ff;">bool</span> blocking, <span style="color: #0000ff;">bool</span> compacting)</pre>
</div>
<table style="height: 213px; width: 763px;" border="1" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td valign="top" width="284">
<p>符号名称</p>
</td>
<td valign="top" width="284">
<p>说明</p>
</td>
</tr>
<tr>
<td valign="top" width="284">
<p>Default</p>
</td>
<td valign="top" width="284">
<p>等同于不传递任何符号名称。目前还等同于Forced,但未来的版本可能对此进行修改</p>
</td>
</tr>
<tr>
<td valign="top" width="284">
<p>Forced</p>
</td>
<td valign="top" width="284">
<p>强制回收指定的代（以及低于它的所有代）</p>
</td>
</tr>
<tr>
<td valign="top" width="284">
<p>Optimized</p>
</td>
<td valign="top" width="284">
<p>只有在能释放大量内存或者能减少碎片化的前提下，才执行回收。如果垃圾回收没有什么效率，当前调用就没有任何效果</p>
</td>
</tr>
</tbody>
</table>
<p>如果写一个CUI（控制台用户界面）或GUI（图形用户界面）应用程序，你可能希望建议垃圾回收的时间；为此，请将GCCollectionMode设置为Optimized并调用Collect。Default和Forced模式一般用于调试、测试和查找内存泄露</p>
<p>如果刚才发生了某个非重复性的事件，并导致大量旧对象死亡，就可考虑手动调用一次collect方法。由于是非重复性事件，垃圾回收器基于历史的预测可能不准确。所以，这是调用collect方法时合适的</p>
<div class="cnblogs_code">
<pre>            <span style="color: #008000;">//</span><span style="color: #008000;">查看某一代发生了多少次垃圾回收</span>
            Console.WriteLine(GC.CollectionCount(<span style="color: #800080;">0</span><span style="color: #000000;">));
            </span><span style="color: #008000;">//</span><span style="color: #008000;">查看托管堆中的对象当前使用了多少内存</span>
            Console.WriteLine(GC.GetTotalMemory(<span style="color: #0000ff;">true</span>));</pre>
</div>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">三、使用需要特殊清理的类型</span></strong></p>
<p>包含本机资源的类型被GC时，GC会回收对象在托管堆中使用的内存。但这样会造成本机资源的泄漏，所以CLR提供了称为终结的机制，允许对象在被判定为垃圾之后，但在对象内存被回收之前执行一些代码。任何包装了本机资源（文件、网络连接、套接字、互斥体）的类型都支持终结。CLR判定一个对象不可达时，对象将终结自己，释放它包装的本机资源。之后，GC会从托管堆回收对象</p>
<p><strong><span style="font-size: 18px;">1，Finalize</span></strong></p>
<p>它是为释放本机资源而设计的</p>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">internal</span> <span style="color: #0000ff;">sealed</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SomeType
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;">这是一个Finalize方法</span>
        ~<span style="color: #000000;">SomeType()
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">这里的代码会进入Finalize方法</span>
<span style="color: #000000;">        }
    }</span></pre>
</div>
<p><strong><span style="font-size: 18px;">&nbsp;2，SafeHandle</span></strong></p>
<p>创建封装了本机资源的托管类型是，应该先从using System.Runtime.InteropServices.SafeHandle这个特殊基类派生一个类</p>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SafeHandle : CriticalFinalizerObject, IDisposable
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;">这是本机资源句柄</span>
        <span style="color: #0000ff;">protected</span><span style="color: #000000;"> IntPtr handle;

        </span><span style="color: #0000ff;">protected</span><span style="color: #000000;"> SafeHandle(IntPtr invalidHandleValue, Boolean ownsHandle)
        {
            handle </span>=<span style="color: #000000;"> invalidHandleValue;
            </span><span style="color: #008000;">//</span><span style="color: #008000;">如果ownsHandle为true，那么这个从SafeHandle派生的对象被回收时，本机资源会被关闭</span>
<span style="color: #000000;">        }

        </span><span style="color: #0000ff;">protected</span><span style="color: #000000;"> SafeHandle(IntPtr invalidHandleValue)
        {
            handle </span>=<span style="color: #000000;"> invalidHandleValue;
        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;">显式释放资源</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> Dispose(){Dispose(<span style="color: #0000ff;">true</span><span style="color: #000000;">);}

        </span><span style="color: #008000;">//</span><span style="color: #008000;">默认的Dispose实现（如下所示）正是我们希望的。强烈建议不要重写这个方法</span>
        <span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">virtual</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Dispose(Boolean disposing)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">这个默认实现会忽略disposing参数
            </span><span style="color: #008000;">//</span><span style="color: #008000;">如果资源已经释放，那么返回
            </span><span style="color: #008000;">//</span><span style="color: #008000;">如果ownsHandle为true，那么返回
            </span><span style="color: #008000;">//</span><span style="color: #008000;">设置一个标志来指明该资源已经释放
            </span><span style="color: #008000;">//</span><span style="color: #008000;">调用虚方法ReleaseHandle
            </span><span style="color: #008000;">//</span><span style="color: #008000;">调用GC.SuppressFinalize(this)方法来阻止调用Finalize方法
            </span><span style="color: #008000;">//</span><span style="color: #008000;">如果ReleaseHandled返回true，那么返回
            </span><span style="color: #008000;">//</span><span style="color: #008000;">如果走到这一步，就激活ReleaseHandleFailed托管调试助手（MDA）</span>
<span style="color: #000000;">
        }
        </span><span style="color: #008000;">//</span><span style="color: #008000;">派生类型要从写这个方法以实现释放资源的代码</span>
        <span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">abstract</span><span style="color: #000000;"> Boolean ReleaseHandle();

        </span><span style="color: #008000;">//</span><span style="color: #008000;">默认的Dispose实现（如下所示）正是我们希望的。强烈建议不要重写这个方法</span>
        ~SafeHandle(){Dispose(<span style="color: #0000ff;">false</span><span style="color: #000000;">);}

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> SetHandleAsInvalid()
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">设置标志来指出这个资源已经释放
            </span><span style="color: #008000;">//</span><span style="color: #008000;">调用GC.SuppressFinalize(this)方法来阻止调用Finalize方法</span>
<span style="color: #000000;">        }

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Boolean IsClosed {
            </span><span style="color: #0000ff;">get</span> { <span style="color: #008000;">//</span><span style="color: #008000;">返回指出资源是否释放的一个标志}</span>
<span style="color: #000000;">        }
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span><span style="color: #000000;"> Boolean IsInvalid
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">派生类要重写这个属性
            </span><span style="color: #008000;">//</span><span style="color: #008000;">如果句柄的值不代表资源（通常意味着句柄为0或-1），实现应返回true</span>
            <span style="color: #0000ff;">get</span><span style="color: #000000;">;
        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;">以下三个方法设计安全性和引用计数</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> DangerousAddRef(<span style="color: #0000ff;">ref</span><span style="color: #000000;"> Boolean success){}
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> IntPtr DangerousGetHandle(){}
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> DangerousRelease(){}

    }</span></pre>
</div>
<p>CLR赋予这个类以下三个很酷的功能</p>
<p>①首次构造CriticalFinalizerObject派生类型对象时，CLR立即对继承层次结构中的所有Finalize方法进行JIT编译。构造对象时接编译这些方法，可确保放当对象被确定为垃圾之后，本机资源肯定会得以释放。不对Finalize方法进行提前编译，那么也许能分配并使用本机资源，但无法保证释放。内存紧张时，CLR可能找不到足够的内存来编译Finalize方法，这会阻止Finalize方法的执行，造成本机资源泄漏。另外，如果Finalize方法中的代码引用了另一个程序集中的类型，但CLR定位该程序集失败，那么资源将得不到释放。</p>
<p>②CLR是在调用了非CriticalFinalizerObject派生类型的Finalize方法之后，才调用CriticalFinalizerObject派生类的Finalize方法。这样，托管资源类就可以在它们的Finalize方法中成功地访问CriticalFinalizerObject派生类型的对象。例如，FileStram类型的Finalize方法可以放心地将数据从内存缓冲区flush到磁盘，它知道此时磁盘文件还没有关闭</p>
<p>③如果AppDomain被一个宿主应用程序（例如Microsoft SQL Server或者Microsoft ASP.NET）强行中断，CLR将调用CriticalFinalizerObject派生类型的Finalize方法。宿主应用程序不再信任它内部允许的托管代码，也利用这个功能确保本机资源得以释放。</p>
<p><strong><span style="font-size: 18px;">3,SafeHandle派生类</span></strong></p>
<p>SafeHandle派生类非常有用，因为它们保证本机资源在垃圾回收得以释放</p>
<p><img src="http://images2015.cnblogs.com/blog/741594/201707/741594-20170708152210972-1490480462.png" alt="" /></p>
<p>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('1fabd283-9053-4382-bae3-84ff32219cce')"><img id="code_img_closed_1fabd283-9053-4382-bae3-84ff32219cce" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_1fabd283-9053-4382-bae3-84ff32219cce" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('1fabd283-9053-4382-bae3-84ff32219cce',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_1fabd283-9053-4382-bae3-84ff32219cce" class="cnblogs_code_hide">
<pre>    <span style="color: #0000ff;">internal</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SomeType
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;">这个原型不健壮</span>
        [DllImport(<span style="color: #800000;">"</span><span style="color: #800000;">Kernal32</span><span style="color: #800000;">"</span>,CharSet = CharSet.Unicode,EntryPoint = <span style="color: #800000;">"</span><span style="color: #800000;">CreateEvent</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">extern</span><span style="color: #000000;"> IntPtr CreateEventBad(IntPtr pSecurityAttribute, Boolean manualReset, Boolean initialState,
            </span><span style="color: #0000ff;">string</span><span style="color: #000000;"> name);

        </span><span style="color: #008000;">//</span><span style="color: #008000;">这个原型是健壮的</span>
        [DllImport(<span style="color: #800000;">"</span><span style="color: #800000;">Kernal32</span><span style="color: #800000;">"</span>, CharSet = CharSet.Unicode, EntryPoint = <span style="color: #800000;">"</span><span style="color: #800000;">CreateEvent</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span>  <span style="color: #0000ff;">extern</span><span style="color: #000000;"> SafeWaitHandle CreateEventGood(IntPtr pSecurityAttribute, Boolean manualReset, Boolean initialState,
            </span><span style="color: #0000ff;">string</span><span style="color: #000000;"> name);

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> SomeMethod()
        {
            IntPtr handle </span>= CreateEventBad(IntPtr.Zero, <span style="color: #0000ff;">false</span>, <span style="color: #0000ff;">false</span>, <span style="color: #0000ff;">null</span><span style="color: #000000;">);
            SafeWaitHandle swh </span>= CreateEventGood(IntPtr.Zero, <span style="color: #0000ff;">false</span>, <span style="color: #0000ff;">false</span>, <span style="color: #0000ff;">null</span><span style="color: #000000;">);
        }
    }</span></pre>
</div>
<span class="cnblogs_code_collapse">SomeType</span></div>
<p>&nbsp;</p>
<p><strong><span style="font-size: 18px;">4，使用包装了本机资源的类型</span></strong></p>
<p><strong>1&gt;以FileStream为例，可以用它打开一个文件，从文件中读取字节，向文件中写入字节，然后关闭文件</strong><br />①FileStream对象在构造时会调用Win32 CreateFile函数<br />②函数返回句柄保存到SafeFileHandle对象中<br />③然后通过FileStream对象的一个私有字段来维护对象的引用</p>
<p><strong>2&gt;FileStream的Dispose方法</strong></p>
<p>①FileStream实现了IDisposable接口。FileStream的Dispose方法会调用SafeFileHandle字段上的Dispose方法。<br />②<span style="color: #ff6600;">FileStream调用Dispose方法会清理本机资源</span>。（并非一定要调用Dispose才能保证本机资源得以清理。本机资源的清理最终总会发生，调用Dispose只是控制这个清理动作的发生时间）<br />③<span style="color: #ff6600;">FileStream调用Dispose方法不会导致FileStram对象从托管堆中删除</span>。只有在垃圾回收之后，托管堆中的内存才会得以回收</p>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建要写入临时文件的字节</span>
            <span style="color: #0000ff;">byte</span>[] bytesToWrite = <span style="color: #0000ff;">new</span> <span style="color: #0000ff;">byte</span>[] {<span style="color: #800080;">1</span>, <span style="color: #800080;">2</span>, <span style="color: #800080;">3</span>, <span style="color: #800080;">4</span>, <span style="color: #800080;">5</span><span style="color: #000000;">};

            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建临时文件</span>
            FileStream fs = <span style="color: #0000ff;">new</span> FileStream(<span style="color: #800000;">"</span><span style="color: #800000;">Temp.dat</span><span style="color: #800000;">"</span><span style="color: #000000;">, FileMode.Create);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">将字节写入临时文件</span>
            fs.Write(bytesToWrite, <span style="color: #800080;">0</span><span style="color: #000000;">, bytesToWrite.Length);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">删除临时文件</span>
            File.Delete(<span style="color: #800000;">"</span><span style="color: #800000;">Temp.dat</span><span style="color: #800000;">"</span>);<span style="color: #008000;">//</span><span style="color: #008000;">抛出IOException异常</span>
<span style="color: #000000;">
            Console.ReadLine();
        }</span></pre>
</div>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建要写入临时文件的字节</span>
            <span style="color: #0000ff;">byte</span>[] bytesToWrite = <span style="color: #0000ff;">new</span> <span style="color: #0000ff;">byte</span>[] {<span style="color: #800080;">1</span>, <span style="color: #800080;">2</span>, <span style="color: #800080;">3</span>, <span style="color: #800080;">4</span>, <span style="color: #800080;">5</span><span style="color: #000000;">};

            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建临时文件</span>
            FileStream fs = <span style="color: #0000ff;">new</span> FileStream(<span style="color: #800000;">"</span><span style="color: #800000;">Temp.dat</span><span style="color: #800000;">"</span><span style="color: #000000;">, FileMode.Create);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">将字节写入临时文件</span>
            fs.Write(bytesToWrite, <span style="color: #800080;">0</span><span style="color: #000000;">, bytesToWrite.Length);
            
            </span><span style="color: #008000;">//</span><span style="color: #008000;">结束写入后显式关闭文件</span>
<span style="color: #000000;">            fs.Dispose();

            fs.Write(bytesToWrite, </span><span style="color: #800080;">0</span>, bytesToWrite.Length);<span style="color: #008000;">//</span><span style="color: #008000;">抛出ObjectDisposedException

            </span><span style="color: #008000;">//</span><span style="color: #008000;">删除临时文件</span>
            File.Delete(<span style="color: #800000;">"</span><span style="color: #800000;">Temp.dat</span><span style="color: #800000;">"</span>);<span style="color: #008000;">//</span><span style="color: #008000;">抛出IOException异常</span>
<span style="color: #000000;">
            Console.ReadLine();
        }</span></pre>
</div>
<p><strong><span style="font-size: 18px;">&nbsp;5，一个有趣的依赖性问题</span></strong></p>
<div class="cnblogs_code">
<pre>            <span style="color: #008000;">//</span><span style="color: #008000;">创建临时文件</span>
            FileStream fs = <span style="color: #0000ff;">new</span> FileStream(<span style="color: #800000;">"</span><span style="color: #800000;">Temp.txt</span><span style="color: #800000;">"</span><span style="color: #000000;">, FileMode.Create);
            StreamWriter sw </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> StreamWriter(fs);
            sw.Write(</span><span style="color: #800000;">"</span><span style="color: #800000;">abc</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            </span><span style="color: #008000;">//</span><span style="color: #008000;">不要忘记这个Dispose的调用，不执行sw.Dispose()数据写不进文件</span>
<span style="color: #000000;">            sw.Dispose();
            </span><span style="color: #008000;">//</span><span style="color: #008000;">注意：调用StreamWriter.Dispose会关闭FileStream；
            </span><span style="color: #008000;">//</span><span style="color: #008000;">FileStream对象无需显示关闭</span></pre>
</div>
<p>不需要再FileStream对象上显式调用Dispose，因为StreanWrite会帮你调用。但如果非要显式调用Dispose，FileStream会发现对象已经清理过了，所以方法什么都不做直接返回</p>
<p><strong><span style="font-size: 18px;">&nbsp;6，终结器的内部工作原理</span></strong></p>
<p>①应用程序创建新对象时，New操作符会从推中分配内存。如果对象的类型定义了Funalize方法，那么在该类型的实例构造器被调用之前，会将指向该对象的指针放到一个<strong>终结列表</strong>中</p>
<p><img src="http://images2015.cnblogs.com/blog/741594/201707/741594-20170710213454087-921354911.png" alt="" /></p>
<p>②垃圾回收时，对象B,D,E,F判定为垃圾。垃圾回收器扫描终结列表以查找这些对象的引用。找到一个引用之后，该引用从终结列表中移除，并附加到freachable队列中</p>
<p><img src="http://images2015.cnblogs.com/blog/741594/201707/741594-20170710213507525-964544348.png" alt="" /></p>
<p>③一个特殊的高优先级CLR线程专门调用Finalize方法。一旦freachable队列中有记录项出现，线程就会唤醒，将每一项都从freachable队列中移除，同时调用每个对象的Finalize方法。</p>
<p><img src="http://images2015.cnblogs.com/blog/741594/201707/741594-20170710213523197-1355046611.png" alt="" /></p>
<p>④下一次对老一代垃圾回收时，会发现已终结的对象成为真正的垃圾，因为没有应用程序的根指向它们，freachable队列也不再指向它们，所以，这些对象的内存会直接回收</p>
<p><img src="http://images2015.cnblogs.com/blog/741594/201707/741594-20170710213533462-54507658.png" alt="" /></p>
<p><span style="font-size: 12px; color: #ff0000;">（注意：CLR会忽略System.Object定义的Finalize方法）</span></p>
<p><span style="font-size: 12px; color: #ff0000;">（注意：可终结对象需要执行两次垃圾回收才能释放它们的内存。在实际应用中，由于对象可能被提升至另一代，所以可能要求不止进行两次垃圾回收）</span></p>
<p><strong><span style="font-size: 18px; color: #000000;">7，手动监视和控制对象的生存期</span></strong></p>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">struct</span><span style="color: #000000;"> GCHandle
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;">静态方法，用于在表中创建一个记录项</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> GCHandle Alloc(<span style="color: #0000ff;">object</span><span style="color: #000000;"> value);
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> GCHandle Alloc(<span style="color: #0000ff;">object</span><span style="color: #000000;"> value,GCHandleType type);

        </span><span style="color: #008000;">//</span><span style="color: #008000;">静态方法，用于将一个GCHandle转成一个IntPtr</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">explicit</span> <span style="color: #0000ff;">operator</span><span style="color: #000000;"> IntPtr(GCHandle value);
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> IntPtr ToIntPtr(GCHandle value);

        </span><span style="color: #008000;">//</span><span style="color: #008000;">静态方法，用于将一个IntPtr转成一个GCHandle</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">explicit</span> <span style="color: #0000ff;">operator</span><span style="color: #000000;"> GCHandle(IntPtr value);
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> GCHandle FromIntPtr(IntPtr value);

        </span><span style="color: #008000;">//</span><span style="color: #008000;">实例方法，用于释放表中的记录项（索引设置为0）</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Free();

        </span><span style="color: #008000;">//</span><span style="color: #008000;">实例属性，用于get/set记录项的对象引用</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">object</span> Target { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

        </span><span style="color: #008000;">//</span><span style="color: #008000;">实例属性，如果索引不为0，就放回true</span>
        <span style="color: #0000ff;">public</span> Boolean IsAllocated { <span style="color: #0000ff;">get</span><span style="color: #000000;">; }

        </span><span style="color: #008000;">//</span><span style="color: #008000;">对于已固定（pinned）的记录项，这个方法返回对象的地址</span>
        <span style="color: #0000ff;">public</span><span style="color: #000000;"> IntPtr AddrOfPinnedObject();
    }</span></pre>
</div>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">enum</span><span style="color: #000000;"> GCHandleType
    {
        Weak </span>= <span style="color: #800080;">0</span>, <span style="color: #008000;">//</span><span style="color: #008000;">监事对象的存在</span>
        WeakTrackResurrection = <span style="color: #800080;">1</span>, <span style="color: #008000;">//</span><span style="color: #008000;">监事对象的存在</span>
        Normal = <span style="color: #800080;">2</span>, <span style="color: #008000;">//</span><span style="color: #008000;">控制对象的生存期</span>
        Pinned = <span style="color: #800080;">3</span> <span style="color: #008000;">//</span><span style="color: #008000;">控制对象的生存期</span>
    }</pre>
</div>
<p>Weak：</p>
<p>该标志允许监视对象的生存期。可检测垃圾回收器再什么时候判定该对象在应用程序代码中不可达。注意，此时对象的Finalize方法可能执行，也可能没有执行，对象可能还在内存中。</p>
<p>WeakTrackResurrection：</p>
<p>该标志允许监视对象的生存期。可检测垃圾回收器在什么时候判定该对象在应用程序的代码不可达。注意，此时对象的Finalize方法（如果有的话）已经执行，对象的内存已经回收</p>
<p>Normal：</p>
<p>该标志允许控制对象的生存期。告诉垃圾回收器：即使应用程序中没有根引用对象，该对象也必须留在内存中。垃圾回收发生时，该对象的内存可以压缩（移动）。Alloc方法默认的标志</p>
<p>Pinned：&nbsp;</p>
<p>该标志允许控制对象的生存期。告诉垃圾回收器：即使应用程序中没有根引用对象，该对象也必须留在内存中。垃圾回收发生时，该对象的内存不压缩（移动）。需要将内存地址交给本机代码时，这个功能很好用。本机代码知道GC不会移动对象，所以能放心地向托管堆的这个内存写入。</p>
<p>1&gt;垃圾回收器如何使用GC句柄表。当垃圾回收发生时，垃圾回收器的行为如下<br />①垃圾回收器标记所有可达的对象。然后。垃圾回收器扫描GC句柄表；所有Normal或Pinned对象都被看成是根，同时标记这些对象（包括对象通过他们的字段引用的对象）<br />②垃圾回收器扫描GC句柄表，查找所有Weak记录项。如果一个Weak记录项引用了未标记的对象，该引用标识的就是不可达对象（垃圾），记录项的引用值更改为null<br />③垃圾回收器扫描终结列表。在列表中，对未标记对象的引用标识的是不可达对象，这个引用从终结列表移至freachable队列，这是对象会被标记，因为对象又变成可达了<br />④垃圾回收器扫描GC句柄表，查找所有WeakTrackResurrection记录项。如果一个WeakTrackResurrection记录项引用了未标记的对象（它现在是有freachable队列中的记录项引用的），该引用标识的就是不可达对象（垃圾），该记录项的引用值更改为null<br />⑤垃圾回收器对内存进行压缩，填补不可达对象留下的内存&ldquo;空调&rdquo;，这其实就是一个内存碎片整理的过程。Pinned对象不会压缩（移动），垃圾回收器会移动它周围的其他对象</p>
<p>&nbsp;</p>