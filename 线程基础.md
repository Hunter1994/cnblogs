<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">一、线程开销</span></strong></span></p>
<p>线程有空间（内存耗用）和时间（运行时的执行性能）上的开销<br />①线程内核对象<br />OS为系统中创建的每个线程都分配并初始化这种数据结构之一（对线程进行描述的属性、线程上下文）。上下文是包含CPU寄存器集合的内存块。对于x86，x64和ARM CPU架构，线程上下文分别使用约700,1240,和350字节的内存<br />②线程环境块（TEB）<br />TEB是用户模式（应用程序代码能快速访问的地址空间）中分配和初始化的内存块。TEB耗用1个内存页（x86,x64和ARM CPU中时4kb）。TEB包含线程的异常处理链首（head）。线程进入每个try块都在链首插入一个节点；线程退出try块时从链中删除该节点。此外，TEB还包含线程的"线程本地存储"数据，以及由GDI和OpenGL图形使用的一些数据结构<br />③用户模式栈<br />用户模式栈存储传给方法的局部变量和实参。还包含一个地址；指出当前方法返回时，线程应该从什么地方接着执行。Windows默认为每个线程的用户模式栈分配1MB内存。更具体的说Windows只是保留1MB地址空间，在线程实际需要时才会提交（调拨）物理内存<br />④内核模式栈<br />应用程序代码操作系统中的内核模式函数传递实参时，还会使用到内核模式栈。出于对安全的考虑，针对从用户模式的代码传给内核的任何实参，Windows都会把它们从线程的用户模式栈复制到线程的内核模式栈。OS内核代码开始处理复制的值。除此之外，内核会调用它自己内部的方法，并利用内核模式栈传递它自己的实参、存储函数和局部变量以及存储返回地址。在32位Windwos上运行，内核模式栈大小是12kb；64位是24kb<br />⑤DLL线程连接（attach）和线程分离（detach）通知<br />Windows的一个策略是，任何时候在进程中创建线程，都会调用进程中加载的所有非托管DLL的DllMain方法，并向该方法传递DLL_THRAND_ATTACH标志。类似的，任何时候线程终止，都会调用进程中的所有非托管DLL的DllMain方法，并向方法传递DLL_THRAND_DETACH标志。有的DLL需要获取这些通知，才能为进程创建/销毁的每个线程执行特殊的初始化或（资源）清理操作。VS在它的进程地址空间加载了大约470个dll！这意味着每次在VS中创建或者销毁一个线程，都必须先调用470个dll函数</p>
<p><span style="color: #ff0000;">Windows任何时刻只将一个线程分配给一个CUP。那个线程能运行一个&ldquo;时间片&rdquo;（有时也称为&ldquo;量&rdquo;或者&ldquo;量程&rdquo;）的长度。时间片到期，Windows就上下文切换到另一个线程</span></p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">二、使用专用线程</span></strong></p>
<p>应尽量使用线程池来执行异步的计算限制操作。如果满足一下任何条件则可以使用专用线程<br />①线程需要以非普通线程优先级运行。所有线程池都以普通优先级运行<br />②需要线程表现为一个前台线程，防止应用程序在线程结束前终止。线程池始终是后台线程<br />③计算限制的任务需要长时间运行<br />④要启动线程，并可能调用Thread的Abort方法来提前终止它</p>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建专用线程</span>
            Thread th = <span style="color: #0000ff;">new</span><span style="color: #000000;"> Thread(ComputeBoundOp);
            th.Start(</span><span style="color: #800080;">5</span><span style="color: #000000;">);

            th.Join();</span><span style="color: #008000;">//</span><span style="color: #008000;">等待线程终止</span>
<span style="color: #000000;">            Console.ReadLine();

        }


        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> ComputeBoundOp(Object state)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">这个方法由一个专用线程执行</span>
<span style="color: #000000;">            Console.WriteLine(state);
            Thread.Sleep(</span><span style="color: #800080;">1000</span>);<span style="color: #008000;">//</span><span style="color: #008000;">模拟做其他任务（1秒）
            </span><span style="color: #008000;">//</span><span style="color: #008000;">这个方法返回后，专用线程将终止</span>
        }</pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">三、线程调度和优先级</span></strong></span></p>
<p>只要存在可调度的优先级31的线程，系统就永远不会讲优先级0~30的任何线程分配给CPU。这种情况称为饥饿<br />较高优先级总是抢占较低优先级的线程</p>
<table class="MsoTableGrid" style="border-width: initial; border-style: none; border-color: initial; height: 397px; width: 834px;" border="1" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td style="width: 54.5pt; border-width: 1pt; border-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="73">
<p class="MsoNormal"><span lang="EN-US">&nbsp;</span></p>






  </td>
<td style="width: 54.5pt; border-top-width: 1pt; border-right-width: 1pt; border-bottom-width: 1pt; border-top-color: windowtext; border-right-color: windowtext; border-bottom-color: windowtext; border-left: none; padding: 0cm 5.4pt;" valign="top" width="73">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">进程优先级类</span></p>






  </td>
<td style="width: 52.85pt; border-top-width: 1pt; border-right-width: 1pt; border-bottom-width: 1pt; border-top-color: windowtext; border-right-color: windowtext; border-bottom-color: windowtext; border-left: none; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">Idle</span></p>






  </td>
<td style="width: 52.85pt; border-top-width: 1pt; border-right-width: 1pt; border-bottom-width: 1pt; border-top-color: windowtext; border-right-color: windowtext; border-bottom-color: windowtext; border-left: none; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">Below Normal</span></p>






  </td>
<td style="width: 52.85pt; border-top-width: 1pt; border-right-width: 1pt; border-bottom-width: 1pt; border-top-color: windowtext; border-right-color: windowtext; border-bottom-color: windowtext; border-left: none; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">Normal</span></p>






  </td>
<td style="width: 52.85pt; border-top-width: 1pt; border-right-width: 1pt; border-bottom-width: 1pt; border-top-color: windowtext; border-right-color: windowtext; border-bottom-color: windowtext; border-left: none; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">Above Normal</span></p>






  </td>
<td style="width: 52.85pt; border-top-width: 1pt; border-right-width: 1pt; border-bottom-width: 1pt; border-top-color: windowtext; border-right-color: windowtext; border-bottom-color: windowtext; border-left: none; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">High</span></p>






  </td>
<td style="width: 52.85pt; border-top-width: 1pt; border-right-width: 1pt; border-bottom-width: 1pt; border-top-color: windowtext; border-right-color: windowtext; border-bottom-color: windowtext; border-left: none; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">Realtime</span></p>






  </td>






 </tr>
<tr>
<td style="width: 54.5pt; border-right-width: 1pt; border-bottom-width: 1pt; border-left-width: 1pt; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-top: none; padding: 0cm 5.4pt;" valign="top" width="73">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">相对线程优先级</span></p>






  </td>
<td style="width: 54.5pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="73">
<p class="MsoNormal"><span lang="EN-US">&nbsp;</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">&nbsp;</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">&nbsp;</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">&nbsp;</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">&nbsp;</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">&nbsp;</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">&nbsp;</span></p>






  </td>






 </tr>
<tr>
<td style="width: 54.5pt; border-right-width: 1pt; border-bottom-width: 1pt; border-left-width: 1pt; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-top: none; padding: 0cm 5.4pt;" valign="top" width="73">
<p class="MsoNormal"><span lang="EN-US">Time-Critical</span></p>






  </td>
<td style="width: 54.5pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="73">
<p class="MsoNormal"><span lang="EN-US">&nbsp;</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">15</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">15</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">15</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">15</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">15</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">31</span></p>






  </td>






 </tr>
<tr>
<td style="width: 54.5pt; border-right-width: 1pt; border-bottom-width: 1pt; border-left-width: 1pt; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-top: none; padding: 0cm 5.4pt;" valign="top" width="73">
<p class="MsoNormal"><span lang="EN-US">Highest</span></p>






  </td>
<td style="width: 54.5pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="73">
<p class="MsoNormal"><span lang="EN-US">&nbsp;</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">6</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">8</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">10</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">12</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">15</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">26</span></p>






  </td>






 </tr>
<tr>
<td style="width: 54.5pt; border-right-width: 1pt; border-bottom-width: 1pt; border-left-width: 1pt; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-top: none; padding: 0cm 5.4pt;" valign="top" width="73">
<p class="MsoNormal"><span lang="EN-US">Above Normal</span></p>






  </td>
<td style="width: 54.5pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="73">
<p class="MsoNormal"><span lang="EN-US">&nbsp;</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">5</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">7</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">9</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">11</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">14</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">25</span></p>






  </td>






 </tr>
<tr>
<td style="width: 54.5pt; border-right-width: 1pt; border-bottom-width: 1pt; border-left-width: 1pt; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-top: none; padding: 0cm 5.4pt;" valign="top" width="73">
<p class="MsoNormal"><span lang="EN-US">Normal</span></p>






  </td>
<td style="width: 54.5pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="73">
<p class="MsoNormal"><span lang="EN-US">&nbsp;</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">4</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">6</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">8</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">10</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">13</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">24</span></p>






  </td>






 </tr>
<tr>
<td style="width: 54.5pt; border-right-width: 1pt; border-bottom-width: 1pt; border-left-width: 1pt; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-top: none; padding: 0cm 5.4pt;" valign="top" width="73">
<p class="MsoNormal"><span lang="EN-US">Below Normal</span></p>






  </td>
<td style="width: 54.5pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="73">
<p class="MsoNormal"><span lang="EN-US">&nbsp;</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">3</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">5</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">7</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">9</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">12</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">23</span></p>






  </td>






 </tr>
<tr>
<td style="width: 54.5pt; border-right-width: 1pt; border-bottom-width: 1pt; border-left-width: 1pt; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-top: none; padding: 0cm 5.4pt;" valign="top" width="73">
<p class="MsoNormal"><span lang="EN-US">Lowest</span></p>






  </td>
<td style="width: 54.5pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="73">
<p class="MsoNormal"><span lang="EN-US">&nbsp;</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">2</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">4</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">6</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">8</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">11</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">22</span></p>






  </td>






 </tr>
<tr>
<td style="width: 54.5pt; border-right-width: 1pt; border-bottom-width: 1pt; border-left-width: 1pt; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-top: none; padding: 0cm 5.4pt;" valign="top" width="73">
<p class="MsoNormal"><span lang="EN-US">Idle</span></p>






  </td>
<td style="width: 54.5pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="73">
<p class="MsoNormal"><span lang="EN-US">&nbsp;</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">1</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">1</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">1</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">1</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">1</span></p>






  </td>
<td style="width: 52.85pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="70">
<p class="MsoNormal"><span lang="EN-US">16</span></p>






  </td>






 </tr>






</tbody>





</table>
<p>大多数进程时Normal线程时Normal。所以大多数线程的优先级是8</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">更改线程的相对线程优先级</span>
th.Priority=ThreadPriority.Normal;</pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">四、前台线程和后台线程</span></strong></span></p>
<p>1，一个进程的所有前台线程停止运行时，CLR强制终止仍在运行的任何后台线程<br />2，前台线程执行确实想完成的任务；后台线程执行非关键性的任务<br />3，演示前台线程和后台线程的差异</p>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            Thread th </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> Thread(ComputeBoundOp);
            th.Start(</span><span style="color: #800080;">5</span><span style="color: #000000;">);
            th.IsBackground </span>= <span style="color: #0000ff;">true</span>;<span style="color: #008000;">//</span><span style="color: #008000;">使用后台线程

            </span><span style="color: #008000;">//</span><span style="color: #008000;">如果th是前台线程，则应用程序大约3秒后才终止
            </span><span style="color: #008000;">//</span><span style="color: #008000;">如果th是后台线程，则应用程序立即终止</span>
            Console.WriteLine(<span style="color: #800000;">"</span><span style="color: #800000;">bbb</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> ComputeBoundOp(Object state)
        {
            Thread.Sleep(</span><span style="color: #800080;">3000</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">以下这行代码只有在有一个前台线程执行时才会显示</span>
            Console.WriteLine(<span style="color: #800000;">"</span><span style="color: #800000;">aaa</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }</span></pre>
</div>
<p>&nbsp;4，应用程序的主线程以及通过构造一个Thead对象来显示创建的任何线程都默认为前台线程。相反，线程池线程默认为后台线程，另外，由进入托管执行环境的本机代码创建的任何线程都被标记为后台线程</p>
<p>&nbsp;</p>