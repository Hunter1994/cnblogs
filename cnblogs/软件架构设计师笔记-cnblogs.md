<p style="font-size: 18pt; background-color: rgba(22, 159, 230, 1);"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">一、计算机基础</span></strong></span></p>
<p style="background-color: yellow;"><strong>&nbsp;1，冯诺依曼计算机</strong></p>
<ul>
<li><span style="font-size: 12px;">计算机由五大部件组成（控制器、运算器、存储器、输入设备、输出设备）</span></li>
<li><span style="font-size: 12px;">指令和数据以同等地位存与存储器，可按地址寻访</span></li>
<li><span style="font-size: 12px;">指令和数据用二进制表示</span></li>
<li><span style="font-size: 12px;">指令由操作码(+-*/转移指令等等)和地址码组成</span></li>
<li><span style="font-size: 12px;">存储程序</span></li>
<li><span style="font-size: 12px;">以运算器为中心</span></li>
</ul>
<p>①五大部件</p>
<p>运算器：算数运算(+-*/)、逻辑运算(与、或、非逻辑判断)</p>
<p>存储器：存放程序和数据</p>
<p>控制器：指挥程序运行</p>
<p>输入设备：将信息转换成计算机能识别的二进制的形式</p>
<p>输出设备：将二进制装换成人类能识别的形式</p>
<p>②缺点</p>
<p>以运算器为中心，运算器属于CPU中的一部分，CPU要承担大量的工作。尽量让CPU处理一些比较重要的工作。</p>
<p>③基于冯诺依曼计算机的改进</p>
<p>1)将运算器与控制器放在一块形成CPU（中央处理器）</p>
<p>2)将与运算器为中心的计算方式逐渐的转变为以存储器为中心的计算方式</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210124151317851-17905654.png" alt="" width="202" height="132" loading="lazy" /></p>
<p>&nbsp;</p>
<p style="background-color: yellow;"><strong>2，现代计算机硬件图</strong></p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210124151810354-79542267.png" alt="" width="266" height="161" loading="lazy" /></p>
<p>&nbsp;</p>
<p style="background-color: yellow;"><strong>3，CPU</strong></p>
<p>①运算器</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210124155527951-357700564.png" alt="" width="289" height="172" loading="lazy" /></p>
<p>&nbsp;ALU（算罗运算）：算数运算+逻辑运算</p>
<p>&nbsp;ACC：累加器（必须的）</p>
<p>&nbsp;PSW：状态条件寄存器</p>
<table style="height: 134px; width: 480px;" border="0"><caption>指令分为指令的功能和指令的操作对象</caption>
<tbody>
<tr>
<td>例子</td>
<td>指令的功能</td>
<td>指令的操作对象</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>取数A</td>
<td>取数</td>
<td>A</td>
<td>[A]-&gt;ACC</td>
</tr>
<tr>
<td>存数B</td>
<td>存数</td>
<td>B</td>
<td>[ACC]-&gt;B</td>
</tr>
<tr>
<td>加C</td>
<td>加</td>
<td>C</td>
<td>[ACC]+[C]-&gt;ACC</td>
</tr>
</tbody>
</table>
<p>②控制器</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210124162212998-108685507.png" alt="" width="402" height="226" loading="lazy" /></p>
<p>&nbsp;PC：它是一个计数器，用来指向指令存在内存单元的什么位置</p>
<p>&nbsp;IR：指令寄存器，存储即将要执行的指令</p>
<p>&nbsp;ID：指令的译码器，翻译指令（操作码，地址码）</p>
<p>&nbsp;时序部件：控制计算机什么时候取一条指令、什么时候做翻译、什么时候取操作数、什么时候计算</p>
<p>&nbsp;MAR：地址寄存器（现在都集成到了CPU中）</p>
<p>&nbsp;MDR：数据寄存器，存放从内存单元取出来的指令或数据&nbsp;（现在都集成到了CPU中）</p>
<p>&nbsp;存储体：一块一块的芯片组成的</p>
<p>&nbsp;<img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210124162819739-1982261641.png" alt="" width="386" height="225" loading="lazy" /></p>
<p>运算器的组成部分包含如下：</p>
<ul>
<li><span style="font-size: 12px;">算数逻辑控制单元ALU：数据的算术运算和逻辑运算；</span></li>
<li><span style="font-size: 12px;">累加器寄存器AC：通用寄存器，为ALU提供一个工作区，用来暂存数据；</span></li>
<li><span style="font-size: 12px;">数据缓冲寄存器DR：写内存时，暂存指令或数据；</span></li>
<li><span style="font-size: 12px;">状态条件寄存器PSW：存状态标志与控制标志；</span></li>
</ul>
<p>控制器的组成部分包含如下：</p>
<ul>
<li><span style="font-size: 12px;">程序计数器PC：存储下一条要执行指令的地址；</span></li>
<li><span style="font-size: 12px;">指令寄存器IR：存储即将执行的指令；</span></li>
<li><span style="font-size: 12px;">指令译码器ID：对指令中的操作码字段进行分析解释；</span></li>
<li><span style="font-size: 12px;">地址寄存器AR：用来保存当前CPU所访问的内存单元的地址；</span></li>
<li><span style="font-size: 12px;">时序部件：提供时序控制信号；</span></li>
</ul>
<p>&nbsp;</p>
<p style="background-color: yellow;"><strong>4，校验码</strong></p>
<p>码距：是指两个码之间的不同位数，如1011和1101之间的码锯为&nbsp;2</p>
<ul>
<li><span style="font-size: 12px;">在一个码组内为了检测e个误码，要求最小码距应该满足：d&gt;=e+1；</span></li>
<li><span style="font-size: 12px;">在一个码组内为了纠正t个误码，要求最小码距应该满足：d&gt;=2t+1；</span></li>
<li><span style="font-size: 12px;">同时纠错检错：d&gt;=e+t+1；</span></li>
</ul>
<p>①奇偶校验码：只能发现奇数个位出错的情况</p>
<p>②海明码：奇偶校验、分组校验</p>
<p>数据位是n位，校验位是k位，则n和k必须满足以下关系：<img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210124231436730-48926752.png" alt="" width="128" height="29" loading="lazy" /></p>
<p>③CRC循环冗余校验码</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210125221547850-579274803.png" alt="" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;1）化解多项式<img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210125221714904-97032915.png" alt="" loading="lazy" /><img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210125221900025-1783867406.png" alt="" width="205" height="33" loading="lazy" /></p>
<p>&nbsp;2）信息吗加0（多项式的最高位是几就加几个0）做模二除运算（异或运算）。余数就是校验码：1100</p>
<p>&nbsp;<img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210125221923850-499378978.png" alt="" width="167" height="139" loading="lazy" /></p>
<p>&nbsp;</p>
<p style="background-color: yellow;"><strong>5，指令</strong></p>
<p>指令周期：取出（解释）并执行一条指令所需要的全部时间（取指周期、分析周期、执行周期）</p>
<p>①顺序方式。各条指令之前顺序串行执行，执行完一条指令后才取下一条执行。缺点是速度慢，机器各部件利用率低</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210125224925381-1888296863.png" alt="" width="372" height="61" loading="lazy" /></p>
<p>&nbsp;</p>
<p>②重叠方式。在解释第K条指令的操作完成之前就可以开始解释第K+1条指令。部分并行</p>
<p>&nbsp;<img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210125225039591-1073593633.png" alt="" width="375" height="57" loading="lazy" /></p>
<p>&nbsp;</p>
<p>③指令流水线技术。高性能计算机都采用这种技术</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210125225416694-1564349678.png" alt="" width="484" height="181" loading="lazy" /></p>
<p>&nbsp;</p>
<p>1)取指：2ns，分析：2ns，执行：1ns。100条指令执行完毕的时间</p>
<p>(t1+t2+...+tk)+(n-1)*△t=(2+2+1)+(100-1)*2=5+198=203ns</p>
<p>④流水线的吞吐率和最大吞吐率。吞吐率就是在单位时间执行的指令数</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210125231231679-2012852387.png" alt="" width="425" height="74" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;⑤流水线加速比</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210125231258375-1045561744.png" alt="" width="200" height="70" loading="lazy" /></p>
<p>&nbsp;</p>
<p style="background-color: yellow;"><strong>6，高速缓冲储存器</strong></p>
<p>解决cpu和主存之前的速度差异，避免cpu&ldquo;空等&rdquo;现象</p>
<p>①局部性原理（什么样的内容不会被替换出来，经常使用的内容不会被替换出去）</p>
<ul>
<li><span style="font-size: 12px;">时间局部性，例如for循环</span></li>
<li><span style="font-size: 12px;">空间局部性，例如相邻的地址空间</span></li>
</ul>
<p>②cache的映像方法</p>
<p>1）直接映像。优点：地址变换很简单；缺点：不灵活，快冲突率高</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210126224423565-1202829083.png" alt="" width="226" height="204" loading="lazy" /></p>
<p>2）全相联映像。优点：位置不受限制，灵活；缺点：复杂，速度比较慢</p>
<p>&nbsp;<img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210126224539572-600327553.png" alt="" width="326" height="214" loading="lazy" /></p>
<p>3）组相联映像。 结合直接映像和全相联映像</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210126224716638-655790157.png" alt="" width="289" height="249" loading="lazy" /></p>
<p>距离cpu较近位置可以采用直接映像或者组相联映像 ；距离cpu较远可以采用全相联映像</p>
<p>③求平均访问时间（命中率为98%，命中访问2ns，未命中访问5ns）</p>
<p>98%*2+2%+5=1.96+1=2.96</p>
<p>④写策略&nbsp;</p>
<ul>
<li><span style="font-size: 12px;">1）写回发（write-back）：当cpu对cache写命中时，只修改cache的内容不立即写入主存，当此行被替换出去的时候才写回主存。在读写方面都起到了高缓存作用</span></li>
<li><span style="font-size: 12px;">2）写直达法（write-through）：cache写命中时，cache与主存同时修改</span></li>
<li><span style="font-size: 12px;">3）标记法：cache写命中时，只写主存并把当前cache标记为0；从cache中读取数据时如果时标记不为0，直接从cache中读取，否则从主存中读取</span></li>
</ul>
<p>⑤替换算法</p>
<ul>
<li><span style="font-size: 12px;">1）随机替换</span></li>
<li><span style="font-size: 12px;">2）先进先出（FIFO）</span></li>
<li><span style="font-size: 12px;">3）近期最少使用算法（LRU）：需要额外的计算器，用于记录其被使用的情况</span></li>
<li><span style="font-size: 12px;">4）最不经常使用页置换算法（LFU）：该算法计数器位数多，实现困难</span></li>
</ul>
<p>&nbsp;</p>
<p style="background-color: yellow;"><strong>7，磁盘存储器</strong></p>
<p>存储容量=n(盘面)*t(磁道)*s(扇区/物理块)*b(扇区内字节数)</p>
<p>存取时间=寻道时间+等待时间+读写时间（存取时间=平均寻道时间+平均等待时间）&nbsp;</p>
<p>单缓冲区：一次只能存放一个数据</p>
<p style="background-color: yellow;"><strong>8，计算机结构的分类&amp;指令系统</strong></p>
<p>①Flynn根据不同的指令流-数据流组织方式，把计算机系统分成以下四类</p>
<ul>
<li><span style="font-size: 12px;">1）单指令流单数据流（SISD）：单处理器计算机，其指令部件每次只对一条指令进行译码，并只对一个操作部件分配数据</span></li>
<li><span style="font-size: 12px;">2）单指令流多数据流（SIMD）：由单一指令部件控制，按照同一指令流的要求为它们分配各自所需的不同数据</span></li>
<li><span style="font-size: 12px;">3）多指令流单数据流（MISD）：少见</span></li>
<li><span style="font-size: 12px;">4）多指令流多数据流（MIMD）：多核处理器，实现作业、任务、指令等各级全面并行的多核处理器</span></li>
</ul>
<p>②指令系统的分类</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210127214717267-1459360539.png" alt="" width="466" height="178" loading="lazy" /></p>
<p>&nbsp;</p>
<p style="background-color: yellow;"><strong>9，总线</strong></p>
<p>按照相对于CPU或其他芯片的位置分类：内部总线、外部总线</p>
<p>按照功能分类 ：地址总线、数据总线、控制总线</p>
<p>按照总线中数据线的多少分类：并行总线、串行总线</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210127215957686-1221538080.png" alt="" width="444" height="100" loading="lazy" /></p>
<p>&nbsp;</p>
<p style="background-color: yellow;"><strong>10，磁盘阵列</strong></p>
<p>&nbsp;磁盘阵列也叫廉价冗余磁盘阵列，目的是提高存取时间。由小磁盘形成一个阵列的方式</p>
<p>RAID0：（无冗余无校验的数据分块），存储性能最高。</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210127221854648-1584969738.png" alt="" width="111" height="175" loading="lazy" /></p>
<p>&nbsp;RAID1：（磁盘镜像阵列），空间利用率50%</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210127221948575-978481132.png" alt="" width="114" height="166" loading="lazy" /></p>
<p>RAID2：（采用纠错海明码的磁盘阵列），少用</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210127222034541-1422474548.png" alt="" width="265" height="128" loading="lazy" /></p>
<p>RAID3和RAID4：（采用奇偶校验码的磁盘阵列）。&nbsp;RAID3适用于大型文件且IO需求不频繁的应用；RAID4适用于大型文件的读取</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210127222226636-1279355012.png" alt="" width="436" height="147" loading="lazy" /></p>
<p>RAID5：（无独立校验码的奇偶校验码的磁盘阵列）：对于大批量和小批量数据的读写性能都很好，适用于IO需求频繁的应用。空间利用率N-1</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210127222412798-1677995549.png" alt="" width="240" height="158" loading="lazy" /></p>
<p>RAID6：（独立数据盘与两个独立的分布式校验方案）：相当于RAID5的扩展。&nbsp;空间利用率N-2</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210127222538653-2012505740.png" alt="" width="299" height="163" loading="lazy" /></p>
<p>&nbsp;RAID7：可以理解为独立存储计算机</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210127222623707-190323303.png" alt="" width="287" height="106" loading="lazy" /></p>
<p>&nbsp;RAID10：（最可靠与高性能），RAID1+0结合</p>
<p>&nbsp;<img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210127222712958-1309070461.png" alt="" width="307" height="225" loading="lazy" /></p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: rgba(22, 159, 230, 1);"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">二、操作系统基础&nbsp;</span></strong></span></p>
<p>操作系统主要的功能</p>
<ul>
<li><span style="font-size: 12px;">处理机处理（cpu）</span></li>
<li><span style="font-size: 12px;">存储器管理</span></li>
<li><span style="font-size: 12px;">设备管理</span></li>
<li><span style="font-size: 12px;">文件管理</span></li>
<li><span style="font-size: 12px;">用户接口&nbsp;</span></li>
</ul>
<p style="background-color: yellow;"><strong>1，进程</strong></p>
<p>&nbsp;<img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210128224114852-875628648.png" alt="" width="228" height="111" loading="lazy" /></p>
<p>&nbsp;</p>
<p>进程由程序、数据集合、进程控制块PCB组成。PCB是一种数据结构，是进程存在的唯一标识</p>
<p>线性方式：把所有的PCB组织在一张线性表中，每次查找是需要扫描全表</p>
<p>链接方式：把具有同一状态的PCB，用其中的链接字链接成一个队列，PCB存储在一个连续的区域</p>
<p>索引方式：同一状态的线程归入一个索引表，多个状态对应不同的索引表</p>
<p>&nbsp;<img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210128224602504-201250035.png" alt="" width="478" height="211" loading="lazy" /></p>
<p>①前驱图</p>
<p>前驱图是一个有向无循环图</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210128224706328-234341811.png" alt="" width="229" height="95" loading="lazy" /></p>
<p>&nbsp;</p>
<p style="background-color: yellow;"><strong>2，PV操作</strong></p>
<p>P操作</p>
<ul>
<li><span style="font-size: 12px;">1）将信号量S的值减1，即S=S-1；</span></li>
<li><span style="font-size: 12px;">2）如果S&gt;=0，则该进程继续执行，否则该进程置为等待状态</span></li>
</ul>
<p>V操作</p>
<ul>
<li><span style="font-size: 12px;">1）将信号量S的值加1，即S=S+1；</span></li>
<li><span style="font-size: 12px;">2）如果S&gt;0该进程继续执行；否则说明有等待队列中有等待进程，需要唤醒等待进程</span></li>
</ul>
<p>&nbsp;<img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210129213614905-1847737227.png" alt="" width="357" height="240" loading="lazy" /></p>
<p>&nbsp;</p>
<p style="background-color: yellow;"><strong>3，存储管理</strong></p>
<p>当内存太小不够用时，用辅存来支援内存</p>
<p>暂时不运行的模块换出到辅存上，必要时在换入内存</p>
<p>①地址重定位</p>
<p>地址重定位是指将程序中的地址虚拟地址（逻辑地址）变换成内存的真实地址（物理地址）的过程</p>
<ul>
<li><span style="font-size: 12px;">逻辑地址：相对地址。CPU所生产的地址。逻辑地址是内部和编程使用的、并不唯一</span></li>
<li><span style="font-size: 12px;">物理地址：绝对地址。加载到内存地址寄存器中的地址，内存单元的真正地址</span></li>
</ul>
<p>1）静态重定位：绝对地址=相对地址+程序存放的内存起始地址</p>
<ul>
<li><span style="font-size: 12px;">程序运行前就确定映射关系</span></li>
<li><span style="font-size: 12px;">程序装入后不能移动</span></li>
<li><span style="font-size: 12px;">程序占用连续的内存空间</span></li>
</ul>
<p><img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210129222848150-1272569838.png" alt="" width="249" height="141" loading="lazy" /></p>
<p>2）动态重定向：绝对地址=重定位寄存器的值（BR）+逻辑地址寄存器的值（VR）</p>
<ul>
<li><span style="font-size: 12px;">程序占用的内存空间可动态变化</span></li>
<li><span style="font-size: 12px;">程序不要求连续的内存空间</span></li>
<li><span style="font-size: 12px;">便于多个进程共享代码</span></li>
</ul>
<p><img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210129223005331-760889253.png" alt="" width="340" height="160" loading="lazy" /></p>
<p>②存储管理</p>
<p>1）分区存储管理：把主存的用户区划分成若干个区域，每个区域分配给一个用户作业使用，并限制它们只能在自己的区域运行。</p>
<p>2）分页存储管理：将一个进程的地址空间划分成若干大小相等的区域，成为页。相应的，将主存划分成与页相同大小的若干个物理块，称为页或叶框。</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210130200755888-370686450.png" alt="" width="334" height="202" loading="lazy" /></p>
<p>3）分段存储管理：为每个段分配一个连续的分区，而进程中的各个段可以离散地分配到主存的不同分区中。在系统中为每个进程建立一张段映射表（段表）。每个段在表中占有一个表项，在其中记录了改段在主存中的起始地址（基址）和段的长度。进程在执行时，通过查段表来找到每个段所对应的主存区</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210130200721493-2133522905.png" alt="" width="376" height="220" loading="lazy" /></p>
<p>4）段页式存储管理：先将整个主存划分为大小相等的存储块（页框），将用户程序按程序的逻辑关系分为若干段，再将每个段划分为若干页，以页框为单位离散分配。在段页式系统中，其地址结构由段号、段内页号和内页地址三部分组成</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210130200701674-1542516085.png" alt="" width="383" height="175" loading="lazy" /></p>
<p>5）虚拟内存管理：如果一个作业只部分装入主存便可开始启动运行，其余部分暂时留在磁盘上，在需要时再装入主存，这样可以有效的利用主存空间。从用户角度看，该系统所具有的主存容量将比实际主存容量大得多，人们把这样的存储器称为虚拟存储器（请求分页存储、请求分段存储、请求段页式存储）</p>
<p>&nbsp;</p>
<p style="background-color: yellow;"><strong>4，设备管理</strong></p>
<p>①工作方式</p>
<p>1）程序控制</p>
<ul>
<li><span style="font-size: 12px;">　　无条件传送：I/O端口总是准备好，cpu在需要时随时直接利用访问相应的I/O端口</span></li>
<li><span style="font-size: 12px;">&nbsp; &nbsp; &nbsp; &nbsp;程序查询：cpu必须不停地测试I/O设备的状态端口。cpu与I/O设备是串行工作的</span></li>
</ul>
<p><img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210131143303794-992755532.png" alt="" width="298" height="201" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;2）中断：某个进程要启动某个设备时，cpu就向相应的设备控制器发出一条I/O启动指令，然后cpu又返回原来的工作。cpu与I/O设备可以并行工作</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210131143502093-987569880.png" alt="" width="344" height="222" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;3）DMA（直接内存存取）：通过DMA控制器直接进行批量数据交换，出了在数据传输开始和结束时，整个过程无需cpu的干预</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210131143726369-121663728.png" alt="" width="328" height="199" loading="lazy" /></p>
<p>&nbsp;</p>
<p style="background-color: yellow;"><strong>5，文件存储管理</strong></p>
<p>主要关注查找文件的方式&nbsp;</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210131151521845-1482293219.png" alt="" width="467" height="316" loading="lazy" /></p>
<p>&nbsp;</p>
<p style="background-color: yellow;"><strong>6，文件存储设备管理</strong></p>
<p>位示图法。该方法是在外存上建议一张位示图。记录文件存储器的使用情况。每一位仅对应文件存储器上的一个物理块，取0和1分别表示空闲和占用</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210131153150478-1229792172.png" alt="" width="385" height="111" loading="lazy" /></p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: rgba(22, 159, 230, 1);"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">三、计算机网络基础</span></strong></span></p>
<p>&nbsp;<img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210131163922236-441842426.png" alt="" width="215" height="225" loading="lazy" /></p>
<p>&nbsp;<img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210131163932710-1529413869.png" alt="" width="740" height="523" loading="lazy" /></p>
<p style="background-color: yellow;"><strong>1，IP</strong></p>
<p>&nbsp;<img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210131200755845-839660926.png" alt="" width="447" height="217" loading="lazy" /></p>
<p style="background-color: yellow;"><strong>2，子网与子网掩码</strong></p>
<p>三级IP地址：网络号+子网号+主机号（子网号从主机号中借出来的）</p>
<ul>
<li><span style="font-size: 12px;">A类地址的子网掩码：255.0.0.0</span></li>
<li><span style="font-size: 12px;">B类地址的子网掩码：255.255.0.0</span></li>
<li><span style="font-size: 12px;">C类地址的子网掩码：255.255.255.0</span></li>
</ul>
<p>131.1.123.24/27(/27代表前27位都是网络号，主机号是5位)</p>
<p style="background-color: yellow;"><strong>3，IPV4/IPV6</strong></p>
<p>①ipv4数据报</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210131202840448-1686991609.png" alt="" width="435" height="204" loading="lazy" /></p>
<p>&nbsp;</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210131202852839-1731026760.png" alt="" width="549" height="354" loading="lazy" /></p>
<p>&nbsp;</p>
<p>②下一代ip地址，共128位，以16位为一段，共8段。</p>
<p><span style="font-size: 14px;">③ipv6对比ipv4的优势</span></p>
<ul>
<li><span style="font-size: 12px;">ipv6有更大的地址空间</span></li>
<li><span style="font-size: 12px;">ipv6使用更小的路由表</span></li>
<li><span style="font-size: 12px;">ipv6增加了组播支持与对流支持</span></li>
<li><span style="font-size: 12px;">ipv6加入了自动配置的支持</span></li>
<li><span style="font-size: 12px;">ipv6具有更高的安全性</span></li>
</ul>
<p>④ipv4/ipv6的过渡技术</p>
<ul>
<li><span style="font-size: 12px;">双协议栈技术：支持ipv4/ipv6两种协议共存</span></li>
<li><span style="font-size: 12px;">隧道技术：ipv4网络对ipv6业务的承载</span></li>
<li><span style="font-size: 12px;">NET-PT技术：两种协议的转换翻译和地址映射</span></li>
</ul>
<p>&nbsp;⑤ipv6数据报</p>
<p>&nbsp;<img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210131203530298-194183827.png" alt="" width="359" height="259" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;<img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210131203545230-1150651494.png" alt="" width="505" height="307" loading="lazy" /></p>
<p style="background-color: yellow;"><strong>4，TCP与UDP&nbsp;</strong></p>
<p>在TCP/IP协议簇中有两个传输协议，即传输控制协议（Transmission Control Protocol,TCP）和用户数据报协议（User Datagram Protocol,UDP）。TCP是面向连接的，而UDP是无连接的<br />①TCP<br />TCP建立在无连接的IP基础之上，因此使用了3种机制实现面向连接的服务</p>
<ul>
<li><span style="font-size: 12px;">1）使用序号对数据进行标记</span></li>
<li><span style="font-size: 12px;">2）TCP使用确认、校验和定时器系统提供可靠性。当接收者按照顺序识别出数据报未能到达或者发生错误是，接收者将通知发送者；当接受者在特定时间没有发送确认信息是，那么发送者就认为发送的数据包并没有达到接收方，这时发送者就会考虑重传数据</span></li>
<li><span style="font-size: 12px;">3）TCP使用窗口机制调整数据流量。并且窗口的大小并不是固定的，而是会随着网络的情况进行调整</span></li>






































</ul>
<p>②UDP<br />用户数据报协议是一种不可靠的、无连接的数据报服务。源主机在传送数据前不需要和目标主机建立连接</p>
<ul>
<li><span style="font-size: 12px;">1）UDP是无连接的，发送数据之前不需要建立连接，因此减少了开销和发送数据之前的时延</span></li>
<li><span style="font-size: 12px;">2）UDP使用尽最大努力交付，即不保证可靠交付，因此主机不需要维持复杂的连接状态表</span></li>
<li><span style="font-size: 12px;">3）UDP是面向报文的。UDP对应用层交下来的报文，既不合并，也不拆分，而是保留这些报文的边界。UDP一次交付一个完整的报文</span></li>
<li><span style="font-size: 12px;">4）UDP没有拥塞控制，因此网络出现的拥塞不会使源主机的发送速率降低。这对某些实时应用是很重要的。很适合多谋体通信的要求</span></li>
<li><span style="font-size: 12px;">5）UDP支持一对一、一对多、多对一和多对多的交互通信</span></li>
<li><span style="font-size: 12px;">6）UDP的首部开销小，只有8个字节，笔TCP的20个字节的首部要短</span></li>






































</ul>
<p style="background-color: yellow;"><strong>5，网络设计&amp;综合布线系统</strong></p>
<p>①网络设计</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210131230306557-524204400.png" alt="" width="433" height="231" loading="lazy" /></p>
<ul>
<li><span style="font-size: 12px;">1）接入层：通常将网络中直接面向用户连接或访问网络的部分称为接入层，将 位于接入层和核心层之间的部分称为分布层或汇聚层。目的是允许终端 用户连接到网络，主要解决相邻用户之间的互访需求，并且为这些访问 提供足够的带宽，接入层还应当适当负责一些用户管理功能（如地址认 证、用户认证、计费管理等），以及用户信息收集工作（如用户的IP地 址、MAC地址、访问日志等）。</span></li>
<li><span style="font-size: 12px;">2）汇聚层：汇聚层是核心层和接入层的分界面，完成网络访问策略控制、数 据包处理、过滤、寻址，以及其他数据处理的任务。汇聚层交换机是 多台接入层交换机的汇聚点，它必须能够处理来自接入层设备的所有 通信量，并提供到核心层的上行链路，因此，汇聚层交换机与接入层 交换机比较，需要更高的性能、更少的接口和更高的交换速率。汇聚层是核心层和接入层的分界面，完成网络访问策略控制、数 据包处理、过滤、寻址，以及其他数据处理的任务。汇聚层交换机是 多台接入层交换机的汇聚点，它必须能够处理来自接入层设备的所有 通信量，并提供到核心层的上行链路，因此，汇聚层交换机与接入层 交换机比较，需要更高的性能、更少的接口和更高的交换速率。</span></li>
<li><span style="font-size: 12px;">3）核心层：网络主干部分称为核心层，核心层的主要目的在于通过高速转发 通信，提供优化、可靠的骨干传输结构，因此，核心层交换机应拥有 更高的可靠性，性能和吞吐量。核心层为网络提供了骨干组件或高速 交换组件，在纯粹的分层设计中，核心层只完成数据交换的特殊任务。 需要根据网络需求的地理距离、信息流量和数据负载的轻重来选择核 心层技术，常用的技术包括ATM、100Base-Fx和千兆以太网等。在 主干网中，考虑到高可用性的需求，通常会使用双星（树）结构，即 采用两台同样的交换机，与汇聚层交换机分别连接，并使用链路聚合 技术实现双机互联。 核心层的设备采用双机冗余热备份是非常必要的，也可以使用负 载均衡功能来改善网络性能。</span></li>
<li><span style="font-size: 12px;">4）出口层：连接着运营商</span></li>




































</ul>
<p>②综合网络布线</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210131230541757-630176945.png" alt="" width="321" height="240" loading="lazy" /></p>
<ul>
<li><span style="font-size: 12px;">1.工作区子系统：它是工作区内终端设备连接到信息插座之间的设备 组成，包括信息插座、连接软线、适配器、计算机、网络集散器、电话、 报警探头、摄像机、监视器、音响等。</span></li>
<li><span style="font-size: 12px;">2.水平子系统：水平子系统是布置在同一楼层上，一端接在信息插座， 另一端接在配线间的跳线架上，它的功能是将干线子系统线路延伸到用户 工作区，将用户工作区引至管理子系统，并为用户提供一个符合国际标准， 满足语音及高速数据传输要求的信息点出口。</span></li>
<li><span style="font-size: 12px;">3.管理子系统：安装有线路管理器件及各种公用设备，实现整个系 统集中管理，它是干线子系统和水平子系统的桥梁，同时又可为同层组 网提供条件。其中包括双绞线跳线架、跳线(有快接式跳线和简易跳线 之分)。</span></li>
<li><span style="font-size: 12px;">4.垂直（干线）子系统：通常它是由主设备间至各层管理间，特别 是在位于中央点的公共系统设备处提供多个线路设施，采用大对数的电 缆馈线或光缆，两端分别端接在设备间和管理间的跳线架上，目的是实 现计算机设备、程控交换机(PBX)、控制中心与各管理子系统间的连接， 是建筑物干线电缆的路由</span></li>
<li><span style="font-size: 12px;">5.设备间子系统：该子系统是由设备间中的电缆、连接跳线架及相关支撑硬件、防雷电保护装置等构成。可以说是整个配线系统的中心单元，因此它的布放、造型及环境条件的考虑适当与否，直接影响到将来 信息系统的正常运行及维护和使用的灵活性。电话交换机、计算机主机 设备及入口设施也可与配线设备安装在一起。</span></li>
<li><span style="font-size: 12px;">6.建筑群子系统：它是将多个建筑物的数据通信信号连接成一体的 布线系统，它采用架空或地下电缆管道或直埋敷设的室外电缆和光缆互 连起来，是结构化布线系统的一部分，支持提供楼群之间通信所需的硬 件6，</span></li>




































</ul>
<p style="background-color: yellow;"><strong>6，域名和地址</strong></p>
<p>域名系统（DNS）:把主机域名解析为ip地址的系统。DNS使用UDP协议，较少情况下使用TCP协议，端口号均为53。<br />域名系统由三部分构成：DNS名字空间、域名服务器、DNS客户机<br />DNS协议：查询过程两种方法：</p>
<ul>
<li><span style="font-size: 12px;">递归查询：当用户发出查询请求时，本地服务器要进行递归查询。这种查询方式要求服务器彻底地进行名字解析，并返回最后的结果一一IP地址或错误信息</span></li>
<li><span style="font-size: 12px;">迭代查询：服务器与服务器之间的查询采用迭代的方式进行，发出查询请求的服务器得到的响应可能不是目标的IP地址，而是其他服务器的引用（名字和地址），那么本地服务器就要访问被引用的服务器，做进一步的查询。如此反复多次，每次都更接近目标的授权服务器，直至得到最后的结果一一目标的IP地址或错误信息。</span></li>

































</ul>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: rgba(22, 159, 230, 1);"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">四、数据库基础</span></strong></span></p>
<p style="background-color: yellow;"><strong>1，数据库系统的结构</strong></p>
<p>&nbsp;<img src="https://img2020.cnblogs.com/blog/741594/202102/741594-20210201194420947-1066555538.png" alt="" width="390" height="294" loading="lazy" /></p>
<p>概念模式：概念模式是数据库中的全体数据的逻辑结构和特征的描述，是所有用户的公共数据视图。一个数据库只有一个概念模式<br />外模式：外模式（子模式、用户模式）用以描述用户看到或使用的哪部分数据的逻辑结构，用户根据外模式用数据操作语句或应用程序去操作数据库中的数据<br />内模式：内模式定了的是存储记录的类型、存储域的表示以及存储记录的物理顺序，指引元、索引和存储路径等数据的存储组织。一个数据库只有一个内模式</p>
<p><br />逻辑独立性：当模式改变时（例如增加新的关系，新的属性，改变属性的数据类型等），由数据库管理员对各个外模式/模式的映像做相应的改变，可以使外模式保持不变。应用程序是依据数据的外模式编写的，从而应用程序不必修改，保证了数据与程序的逻辑独立性，简称数据的逻辑独立性。<br />物理独立性：当数据库的存储结构改变了，由数据库管理员对模式/内模式映像做相应的改变，可以使模式保持不变，从而应用程序也不必改变，保证了数据与程序的屋里独立性，简称数据的屋里独立性</p>
<p>&nbsp;</p>
<p style="background-color: yellow;"><strong>2，数据模型</strong></p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202102/741594-20210201222817782-1489473793.png" alt="" width="700" height="305" loading="lazy" /></p>
<p>&nbsp;</p>
<p>E-R图：</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202102/741594-20210201222844987-2130513885.png" alt="" width="288" height="174" loading="lazy" /></p>
<p>&nbsp;</p>
<p>关系模型：&nbsp;</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202102/741594-20210201222917830-46084873.png" alt="" width="447" height="218" loading="lazy" /></p>
<p>&nbsp;</p>
<p style="background-color: yellow;"><strong>3，关系型数据库</strong></p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202102/741594-20210201223516017-1666934487.png" alt="" width="469" height="262" loading="lazy" /></p>
<p style="background-color: yellow;"><strong>4，关系代数</strong></p>
<p>①集合运算符</p>
<p>&cup;（并）：R(A、B、C) &cup; S(A、B、D) = （A、B、C、D）</p>
<p>-（差）：R(A、B、C)&nbsp;- S(A、B、D) = （C）</p>
<p>&cap;（交）：R(A、B、C)&nbsp;&cup; S(A、B、D) = （A、B）</p>
<p>X（笛卡尔积）：</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202102/741594-20210201225922561-1625680980.png" alt="" width="361" height="187" loading="lazy" /></p>
<p>②专门运算符</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202102/741594-20210201225952880-955297148.png" alt="" width="411" height="213" loading="lazy" /></p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202102/741594-20210201230008769-108653859.png" alt="" width="424" height="134" loading="lazy" /></p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202102/741594-20210201230019775-1347723711.png" alt="" width="416" height="158" loading="lazy" /></p>
<p>外连接：</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202102/741594-20210201232831176-2116867677.png" alt="" width="409" height="319" loading="lazy" /></p>
<p>&nbsp;</p>
<p>③笛卡尔积转自然连接</p>
<p>R(A,B,C,D)和S(C，D，E)。&sigma;R.B&gt;S.E(R ⋈ S)<br />笛卡尔积：R.A,R.B,R.C,R.D,S.C,S.D,S.E<br />转：&pi;1,2,3,4,7(&sigma;2＞7&Lambda;3=5&Lambda;4=6(R&times;S))</p>
<p>&nbsp;</p>
<p style="background-color: yellow;"><strong>5，函数依赖</strong></p>
<p>①函数确定</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202102/741594-20210202230527914-1449978971.png" alt="" width="432" height="94" loading="lazy" /></p>
<p>&nbsp;</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202102/741594-20210202230605524-906681298.png" alt="" width="396" height="239" loading="lazy" /></p>
<p>&nbsp;</p>
<p>②Armstrong公理</p>
<p><span style="font-size: 12px;">Y&sube;X 可以理解为 X里面包含Y</span></p>
<ul>
<li><span style="font-size: 12px;">A1自反律：若Y&sube;X&sube;U，则X&rarr;Y</span></li>
<li><span style="font-size: 12px;">A2增广率：&nbsp;若X&rarr;Y，且Z&sube;U，则XZ&rarr;YZ</span></li>
<li><span style="font-size: 12px;">A3传递率：若X&rarr;Y，Y&rarr;Z，则X&rarr;Z</span></li>
<li><span style="font-size: 12px;">合并规则：若X&rarr;Y，X&rarr;Z，则X&rarr;YZ</span></li>
<li><span style="font-size: 12px;">伪传递规则：若X&rarr;Y，WY&rarr;Z，则XW&rarr;Z</span></li>
<li><span style="font-size: 12px;">分解规则：若X&rarr;Y，Z&sube;Y，则X&rarr;Z</span></li>




















</ul>
<p>③键</p>
<ul>
<li><span style="font-size: 12px;">超键：有多余的键</span></li>
<li><span style="font-size: 12px;">主键：不含多余的键</span></li>
<li><span style="font-size: 12px;">候选键：不含多余属性的超键</span></li>
<li><span style="font-size: 12px;">外键：其他属性集的主键</span></li>
<li><span style="font-size: 12px;">主属性与非主属性：包含在任意一个主键中，成为主属性，否则为非主属性</span></li>
<li><span style="font-size: 12px;">全码：全部属性都是主键</span></li>




















</ul>
<p style="background-color: yellow;"><strong>6，规范化</strong></p>
<p>第一范式（1NF）<br />若关系模式R的每一个字段是不可在分的数据项，则关系模式R属于第一范式。</p>
<p>第二范式（2NF）<br />若关系模式R&isin;1NF，且每一个非主属性完全依赖主键时，则关系式R是2NF（第二范式）</p>
<p>第三范式（3NF）<br />当2NF消除了主属性性对码的传递函数依赖，每一列数据都和主键直接相关，而不能间接相关，则称为3NF</p>
<p>&nbsp;</p>
<p style="background-color: yellow;"><strong>7，数据库设计</strong></p>
<p>①规划阶段：建立数据库的必要性、可行性</p>
<p>②需求分析：收集需求，理解需求。需求规格说明书、数据字典（数据项、数据流、数据存储、数据加工）</p>
<p>③概念设计：E-R模式设计</p>
<p>④逻辑设计：将E-R图转换为关系模型</p>
<p>⑤物理设计 ：设计存储结构</p>
<p>⑥反规范：</p>
<ul>
<li><span style="font-size: 12px;">增加冗余列</span></li>
<li><span style="font-size: 12px;">增加派生列（例如：增加订单总价字段）</span></li>
<li><span style="font-size: 12px;">重新组表（建宽表）</span></li>
<li><span style="font-size: 12px;">分割表（水平分割、垂直分割）</span></li>















</ul>
<p>&nbsp;</p>
<p style="background-color: yellow;"><strong>8，事务管理&amp;并发控制</strong></p>
<p>①数据库系统允许的基本工作单位是事务</p>
<ul>
<li><span style="font-size: 12px;">原子性（Atomicity）：操作。操作序列要么全做要么全不做</span></li>
<li><span style="font-size: 12px;">一致性（Consistency）：数据。数据库从一个一致性状态变成另一个一致性状态</span></li>
<li><span style="font-size: 12px;">隔离性（Isolation）：执行。不能被其他事务干扰</span></li>
<li><span style="font-size: 12px;">持久性（Durability）：变化。一旦提交，改变就是永久性的</span></li>













</ul>
<p>②并发控制</p>
<ul>
<li><span style="font-size: 12px;">排它锁（X）：其他事务不可读写</span></li>
<li><span style="font-size: 12px;">共享锁（S）：其他事务不可写，可读</span></li>












</ul>
<p>&nbsp;</p>
<p style="background-color: yellow;"><strong>9，分布式数据库&amp;故障恢复</strong></p>
<p>①分布式数据库</p>
<p>分布式数据库特点：</p>
<ul>
<li><span style="font-size: 12px;">数据分布性。数据分布在各个节点</span></li>
<li><span style="font-size: 12px;">统一性。统一管理</span></li>
<li><span style="font-size: 12px;">透明性。用户在使用分布式数据库时，与使用集中式数据库一样，无须 知道其所关心的数据存放在哪里，存储了几次。用户需要关心的仅仅是整个数 据库的逻辑结构</span></li>











</ul>
<p><br />与集中式数据库相比，分布式数据库具有下列优点：</p>
<ul>
<li><span style="font-size: 12px;">坚固性好。可靠性与可用性好</span></li>
<li><span style="font-size: 12px;">可扩充性好。可根据发展的需要增减结点</span></li>
<li><span style="font-size: 12px;">可改善性能。提高性能</span></li>
<li><span style="font-size: 12px;">自治性好。数据可以分散管理，统一协调，即系统中各结点的数据 操纵和相互作用是高度自治的，不存在主从控制，因此，分布式数据库较好地 满足了一个单位中各部门希望拥有自己的数据，管理自己的数据，同时又想共 享其他部门有关数据的要求</span></li>











</ul>
<p>问题：</p>
<ul>
<li><span style="font-size: 12px;">异构数据库的集成问题是一项 比较复杂的技术问题，目前还很难用一个通用的分布式数据库管理系统来解 决这一问题</span></li>
<li><span style="font-size: 12px;">如果数据库设计得不好，数据分布不合理，以致远距离 访问过多，尤其是分布连接操作过多，不但不能改善性能，反而会使性能降 低</span></li>











</ul>
<p>分布透明性包括：</p>
<ul>
<li><span style="font-size: 12px;">分片透明性是分布透明性的最高层次。所谓分片透明性是指用户或 应用程序只对全局关系进行操作而不必考虑数据的分片</span></li>
<li><span style="font-size: 12px;">位置透明性是分布透明性的下一层次。所谓位置透明性是指，用户 或应用程序应当了解分片情况，但不必了解片段的存储场地</span></li>
<li><span style="font-size: 12px;">局部数据模型（逻辑透明）透明性是指用户或应用程序应当了解分片 及各片断存储的场地，但不必了解局部场地上使用的是何种数据模型</span></li>











</ul>
<p>&nbsp;</p>
<p>②故障恢复</p>
<p>事务故障。使事务未运行至正常终止点就被撤销<br />系统故障。系统故障是指系统在运行过程中，由于某种原因，事务在执行过程中 以非正常方式终止，这时内存中的信息丢失，但存储在外存储设备上的数据不 会受影响<br />介质故障。系统在运行过程中，由于某种硬件故障<br />计算机病毒。</p>
<p>事务故障恢复：系统自动完成。反向扫描日志文件，对事务逆向操作，处理至事务开始标记<br />系统故障恢复：数据库重启完成。扫描日志文件，对未完成的事务进行回滚<br />介质故障与病毒破坏的恢复：备份恢复</p>
<p>&nbsp;</p>
<p>③备份</p>
<p>物理备份：</p>
<ul>
<li><span style="font-size: 12px;">冷备份：需要将数据库正常关闭</span></li>
<li><span style="font-size: 12px;">热备份：不需要将数据库正常关闭</span></li>









</ul>
<p>为了提高物理备份的效率，通常将完全、增量、差异三种备份方式相组合：</p>
<ul>
<li><span style="font-size: 12px;">完全备份是将数据库的内容全部备份</span></li>
<li><span style="font-size: 12px;">增量备份是只备份上次完全、增量或差异备份以来修改的数据</span></li>
<li><span style="font-size: 12px;">差异备份是备份自上次完全备份后发生变化的所有数据</span></li>









</ul>
<p>&nbsp;</p>
<p style="background-color: yellow;"><strong>10，数据仓库</strong></p>
<p>数据仓库是一个面向主题的、集成的、相对稳定的、反映历史变化的数据集合，用于支持管理决策</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202102/741594-20210208121257753-1095304391.png" alt="" width="578" height="197" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;<img src="https://img2020.cnblogs.com/blog/741594/202102/741594-20210208121314182-999821580.png" alt="" width="535" height="267" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;数据仓库的实现方法 从整体的角度来看，数据仓库的实现方法主要有自顶向下法、自底向上 法和联合方法。</p>
<p>&nbsp;</p>
<p style="background-color: yellow;"><strong>11，数据挖掘</strong></p>
<p>三种基础技术（海量数据搜集、强大的多处理器计算机和数据挖掘算法）<br />数据挖掘与传统的数据分析（如查询、报表、联机应用分析）的本质区 别是数据挖掘是在没有明确假设的前提下去挖掘信息、发现知识。<br />数据挖掘的流程：需求分析-建立数据挖掘库-分析数据-调整数据-模型化-评价和解释</p>
<p>&nbsp;</p>
<p style="background-color: yellow;"><strong>12，Nosql</strong></p>
<p>①关系型数据库的缺点</p>
<ul>
<li><span style="font-size: 12px;">不满足高并发读写需求</span></li>
<li><span style="font-size: 12px;">不满足海量数据的高效率读写</span></li>
<li><span style="font-size: 12px;">不满足高扩展性和可用性</span></li>

</ul>
<p><img src="https://img2020.cnblogs.com/blog/741594/202102/741594-20210208204632974-1450776932.png" alt="" width="407" height="172" loading="lazy" /></p>
<p>②ACID</p>
<p>ACID，是指数据库管理系统（DBMS）在写入或更新资料的过程中，为保证事务（transaction）是正确可靠的，所必须具备的四个特性<br />原子性（Atomicity）    一致性（Consistency）隔离性（Isolation）持续性（永久性）（Durability）</p>
<p>③NoSQL</p>
<p>NoSQL数据库的产生就是为了解决大规模数据集合多重数据种类带来的挑战，尤其是大数据应用难题</p>
<ul>
<li><span style="font-size: 12px;">灵活的可扩展性</span></li>
<li><span style="font-size: 12px;">灵活的数据模型</span></li>
<li><span style="font-size: 12px;">与云计算结合</span></li>

</ul>
<p>④CAP理论</p>
<ul>
<li><span style="font-size: 12px;">C（Consistency）一致性。一致性是指更新操作成功并返回客户端完成后，所有节点在同一时间的数据完全一致，与ACID的C完全不同。</span></li>
<li><span style="font-size: 12px;">A（Availability）可用性。可用性是指服务一直可用，而且是正常响应时间。</span></li>
<li><span style="font-size: 12px;">P（Partition tolerance）分区容错性。分区容错性是指分布式系统在遇到某节点或网络分区故障的时候，仍然能够对外提供满足一致性和可用性的服务。</span></li>

</ul>
<ul>
<li><span style="font-size: 12px;"> CA 优先保证一致性和可用性，放弃分区容错。缺点：不再是分布式系统</span></li>
<li><span style="font-size: 12px;"> CP 优先保证一致性和分区容错性，放弃可用性。缺点：牺牲用户体验</span></li>
<li><span style="font-size: 12px;"> AP 优先保证可用性和分区容错性，放弃一致性。缺点：全局数据的不一致性</span></li>

</ul>
<p>⑤Nosql数据库的主要类型</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202102/741594-20210208211301604-542799550.png" alt="" width="610" height="387" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;<img src="https://img2020.cnblogs.com/blog/741594/202102/741594-20210208211320222-2129523241.png" alt="" width="613" height="392" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;<img src="https://img2020.cnblogs.com/blog/741594/202102/741594-20210208211336113-437877850.png" alt="" width="614" height="374" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;<img src="https://img2020.cnblogs.com/blog/741594/202102/741594-20210208211350462-1337053732.png" alt="" width="611" height="343" loading="lazy" /></p>
<p>&nbsp;</p>