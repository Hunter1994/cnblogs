<p>工具下载地址：链接: https://pan.baidu.com/s/1mLxHzpE91IFA0AaUELGCpw 提取码: 2vn3&nbsp;</p>
<p>一、Windbg的使用</p>
<p>运行Windbg--&gt;file-&gt;Attach to a Process 选择一个进程</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201801/741594-20180110235940238-1881062654.png" alt="" width="735" height="479" /></p>
<p>.loadby sos clr 首先需要加载sos和clr</p>
<p>!threads 显示线程信息</p>
<p>!teb 显示TEB信息&nbsp;</p>
<p>!dumpdomain 显示程序域</p>
<p>!clrstack 查看当前的调用堆栈（首先需要点击线程的osid）</p>
<p>点击线程的State可以查看线程的状态&nbsp;</p>
<p>!help 帮助命令&nbsp;</p>
<p>!FinalizeQueue 查看终结器</p>
<p>!threadpool 查询线程池</p>
<p>!dumpheap -stat 查看clr的托管堆中的各个类型的占用情况</p>
<p>&nbsp;</p>
<p>二、线程的开销</p>
<p>1，空间上的开销</p>
<p>①线程内核数据结构，其中有osid，线程上下文（包含CPU寄存器集合的内存块）</p>
<p>②TEB（线程环境块）</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201801/741594-20180110235414629-1743512583.png" alt="" width="241" height="149" /></p>
<p>③用户模式堆栈（默认分配1M空间）。会放参数、局部变量..</p>
<p>④内核模式堆栈（系统底层级别的堆栈空间）</p>
<p>2，时间上的开销</p>
<p>①进程启动时会加载很多的dll（托管和非托管）。当线程开启或销毁时，会标记所有非托管dll</p>
<p>②时间片切换。当开启的线程多余系统线程数时，会发生时间片切换（时间片切换休眠时间为30ms）</p>
<p>&nbsp;</p>
<p>三、线程的生命周期</p>
<p>Start：线程开启</p>
<p>Suspend：线程暂停</p>
<p>Resume：恢复暂停的线程</p>
<p>Intterupt：中断线程（会抛出异常）</p>
<p>Abort：销毁线程（会抛出异常）</p>
<p>Join：等待线程执行完毕</p>
<p>&nbsp;</p>
<p>四、工作线程和IO线程</p>
<p>工作线程：给一般的异步任务执行。其中不涉及到网络、文件这些IO 【开发者调用】</p>
<p>IO线程：一般用在文件、网络IO上【CLR调用】</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201801/741594-20180111152921176-1873378772.png" alt="" width="483" height="293" /></p>
<p>&nbsp;</p>
<p>五、Task</p>
<p>Task=Thread（控制能力）+ThreadPool （在此基础上封装）</p>
<p>Thread：容易造成时间+空间的浪费。控制能力可以</p>
<p>ThreadPool ：性能好，控制能力弱（控制权在CLR）。比如控制Thread超时、阻塞、取消等</p>
<p>1，Task的三种启动方式</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201801/741594-20180111170850426-315164828.png" alt="" /></p>
<p>Task底层都是由不同的TaskScheduler支撑（TaskScheduler相当于Task的CPU处理器）</p>
<p>默认TaskScheduler是ThreadPoolTaskScheduler</p>
<p>&nbsp;</p>
<p>六、任务调度器</p>
<p>任务都需要经过TaskScheduler</p>
<p>1，ThreadPoolTaskScheduler（task默认调用此TaskScheduler）<strong><br /></strong></p>
<p>&nbsp;这个方式底层如果标记为LongRunning则使用Thread。否则调用ThreadPool</p>
<p>2，SynchronizationContextTaskScheduler（同步上下文TaskScheduler）</p>
<p>案例：</p>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">private</span> <span style="color: #0000ff;">void</span> button1_Click(<span style="color: #0000ff;">object</span><span style="color: #000000;"> sender, EventArgs e)
        {
            </span><span style="color: #0000ff;">new</span> TaskFactory().StartNew(() =&gt;<span style="color: #000000;">
            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;">耗时的操作</span>
                Thread.Sleep(<span style="color: #800080;">3000</span><span style="color: #000000;">);
            }).ContinueWith(t </span>=&gt;<span style="color: #000000;">
            {
                label1.Text </span>= <span style="color: #800000;">"</span><span style="color: #800000;">执行完成</span><span style="color: #800000;">"</span><span style="color: #000000;">;
            }, TaskScheduler.FromCurrentSynchronizationContext());
        }</span></pre>
</div>
<p><img src="http://images2017.cnblogs.com/blog/741594/201801/741594-20180114163111238-1445362073.png" alt="" /></p>
<p>&nbsp;</p>
<p>七、多线程模型</p>
<p>1，同步编程模型（SPM）</p>
<p>2，异步编程模型（APM）</p>
<p>xxxbegin</p>
<p>xxxend</p>
<p>委托给线程池执行的。FileStream（BeginRead，EndRead）配对方法、Action委托，都可以异步执行</p>
<p>3，基于事件的编程模型（EAP）</p>
<p>xxxAsync这样的事件模型。WebClient</p>
<p>4，基于Task的编程模型（TAP）</p>
<p>微软大力推广。APM和EAP都能包装成Task使用</p>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">主线程。线程id：{0}</span><span style="color: #800000;">"</span><span style="color: #000000;">, Thread.CurrentThread.ManagedThreadId);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">异步编程模型（APM）包装成Task</span>
            <span style="color: #0000ff;">var</span> action = <span style="color: #0000ff;">new</span> Action(() =&gt; { Console.WriteLine(<span style="color: #800000;">"</span><span style="color: #800000;">执行Action。线程id：{0}</span><span style="color: #800000;">"</span><span style="color: #000000;">, Thread.CurrentThread.ManagedThreadId); });
            </span><span style="color: #0000ff;">var</span> task = Task.Factory.FromAsync(action.BeginInvoke, action.EndInvoke, <span style="color: #0000ff;">string</span><span style="color: #000000;">.Empty);



            </span><span style="color: #008000;">//</span><span style="color: #008000;">基于事件的编程模型（EAP）包装成Task</span>
            TaskCompletionSource&lt;<span style="color: #0000ff;">int</span>&gt; source = <span style="color: #0000ff;">new</span> TaskCompletionSource&lt;<span style="color: #0000ff;">int</span>&gt;<span style="color: #000000;">();
            WebClient web </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> WebClient();
            web.DownloadDataCompleted </span>+= (obj, e) =&gt;<span style="color: #000000;"> {
                </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
                {
                    source.TrySetResult(e.Result.Length);
                }
                </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (Exception ex)
                {
                    source.TrySetException(ex);
                }
            };
            web.DownloadDataAsync(</span><span style="color: #0000ff;">new</span> Uri(<span style="color: #800000;">"</span><span style="color: #800000;">https://www.oyunkeji.com</span><span style="color: #800000;">"</span><span style="color: #000000;">));
            Console.WriteLine(source.Task.Result);


            Console.ReadKey();
        }</span></pre>
</div>
<p>&nbsp;</p>
<p>八、锁机制</p>
<p>1，用户模式锁</p>
<p>就是通过一些cpu指令或者一个死循环达到thread等待和休眠</p>
<p>①易变结构 volatile</p>
<p>阻止cpu缓存，实时从内存中读取变量的值</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">volatile</span> <span style="color: #0000ff;">bool</span> isStop= <span style="color: #0000ff;">false</span>;</pre>
</div>
<p>②互锁结构 Interlocked</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201801/741594-20180114222611363-1489609895.png" alt="" /></p>
<p>③旋转锁&nbsp;SpinLock</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('d4686c3c-736f-4171-a377-3a0b870085cf')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" id="code_img_closed_d4686c3c-736f-4171-a377-3a0b870085cf" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" id="code_img_opened_d4686c3c-736f-4171-a377-3a0b870085cf" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_d4686c3c-736f-4171-a377-3a0b870085cf" class="cnblogs_code_hide">
<pre>        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> SpinLock spinLock = <span style="color: #0000ff;">new</span><span style="color: #000000;"> SpinLock();
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">int</span> nums = <span style="color: #800080;">0</span><span style="color: #000000;">;
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Run()
        {
            </span><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> i = <span style="color: #800080;">0</span>; i &lt; <span style="color: #800080;">10</span>; i++<span style="color: #000000;">)
            {
                </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
                {
                    </span><span style="color: #0000ff;">bool</span> b = <span style="color: #0000ff;">false</span><span style="color: #000000;">;
                    spinLock.Enter(</span><span style="color: #0000ff;">ref</span><span style="color: #000000;"> b);
                    Console.WriteLine(nums</span>++<span style="color: #000000;">);
                }
                </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (Exception ex)
                {
                    spinLock.Exit();
                }
               
            }
        }

        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {

            </span><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> i = <span style="color: #800080;">0</span>; i &lt; <span style="color: #800080;">5</span>; i++<span style="color: #000000;">)
            {
                Task.Run(() </span>=&gt;<span style="color: #000000;">
                {
                    Run();
                });
            }
            Console.ReadKey();
        }</span></pre>
</div>
<span class="cnblogs_code_collapse">SpinLock</span></div>
<p>&nbsp;</p>
<p>2，内核模式锁</p>
<p>调用win32底层代码，来实现thread的各种操作</p>
<p>万不得已的情况下，不要使用内核模式锁，代价太大</p>
<p>①自动事件锁</p>
<p>场景：使用火车票进闸机，一人一人进</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('443b604b-2476-4883-ac16-e3af31d1e847')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" id="code_img_closed_443b604b-2476-4883-ac16-e3af31d1e847" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" id="code_img_opened_443b604b-2476-4883-ac16-e3af31d1e847" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_443b604b-2476-4883-ac16-e3af31d1e847" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ConsoleApp1
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> AutoResetEvent areLock = <span style="color: #0000ff;">new</span> AutoResetEvent(<span style="color: #0000ff;">true</span><span style="color: #000000;">);
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">int</span> nums = <span style="color: #800080;">0</span><span style="color: #000000;">;
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Run()
        {
            </span><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> i = <span style="color: #800080;">0</span>; i &lt; <span style="color: #800080;">10</span>; i++<span style="color: #000000;">)
            {
                areLock.WaitOne();
                Console.WriteLine(nums</span>++<span style="color: #000000;">);
                areLock.Set();
            }
        }
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {

            </span><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> i = <span style="color: #800080;">0</span>; i &lt; <span style="color: #800080;">5</span>; i++<span style="color: #000000;">)
            {
                Task.Run(() </span>=&gt;<span style="color: #000000;">
                {
                    Run();
                });
            }
            Console.ReadKey();
        }
    }</span></pre>
</div>
<span class="cnblogs_code_collapse">AutoResetEvent</span></div>
<p>②手动事件锁</p>
<p>场景：栅栏阻挡行人、车辆等。适合批量</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('033e13a0-6682-4312-879b-3a62b3bbbed2')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" id="code_img_closed_033e13a0-6682-4312-879b-3a62b3bbbed2" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" id="code_img_opened_033e13a0-6682-4312-879b-3a62b3bbbed2" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_033e13a0-6682-4312-879b-3a62b3bbbed2" class="cnblogs_code_hide">
<pre>    <span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> ManualResetEvent mrLock = <span style="color: #0000ff;">new</span> ManualResetEvent(<span style="color: #0000ff;">false</span><span style="color: #000000;">);
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">int</span> nums = <span style="color: #800080;">0</span><span style="color: #000000;">;
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Run()
        {
            </span><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> i = <span style="color: #800080;">0</span>; i &lt; <span style="color: #800080;">10</span>; i++<span style="color: #000000;">)
            {
                mrLock.WaitOne();</span><span style="color: #008000;">//</span><span style="color: #008000;">等待5秒后才会执行。拦一批值</span>
                Console.WriteLine(nums++<span style="color: #000000;">);
            }
        }
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {

            </span><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> i = <span style="color: #800080;">0</span>; i &lt; <span style="color: #800080;">5</span>; i++<span style="color: #000000;">)
            {
                Task.Run(() </span>=&gt;<span style="color: #000000;">
                {
                    Run();
                });
            }
            Thread.Sleep(</span><span style="color: #800080;">5000</span><span style="color: #000000;">);
            mrLock.Set();

            Console.ReadKey();
        }
    }</span></pre>
</div>
<span class="cnblogs_code_collapse">ManualResetEvent</span></div>
<p>③信号量</p>
<p>场景：传入允许线程的数量</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('e94b57e6-c9ea-43d1-bd42-1e230bb8093c')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" id="code_img_closed_e94b57e6-c9ea-43d1-bd42-1e230bb8093c" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" id="code_img_opened_e94b57e6-c9ea-43d1-bd42-1e230bb8093c" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_e94b57e6-c9ea-43d1-bd42-1e230bb8093c" class="cnblogs_code_hide">
<pre>    <span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> Semaphore sLock = <span style="color: #0000ff;">new</span> Semaphore(<span style="color: #800080;">1</span>, <span style="color: #800080;">1</span><span style="color: #000000;">);
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">int</span> nums = <span style="color: #800080;">0</span><span style="color: #000000;">;
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Run()
        {
            </span><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> i = <span style="color: #800080;">0</span>; i &lt; <span style="color: #800080;">10</span>; i++<span style="color: #000000;">)
            {
                sLock.WaitOne();
                Console.WriteLine(nums</span>++<span style="color: #000000;">);
                sLock.Release();
            }
        }
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {

            </span><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> i = <span style="color: #800080;">0</span>; i &lt; <span style="color: #800080;">5</span>; i++<span style="color: #000000;">)
            {
                Task.Run(() </span>=&gt;<span style="color: #000000;">
                {
                    Run();
                });
            }
            Thread.Sleep(</span><span style="color: #800080;">5000</span><span style="color: #000000;">);

            Console.ReadKey();
        }
    }</span></pre>
</div>
<span class="cnblogs_code_collapse">Semaphore</span></div>
<p>④互斥锁&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('d64aa65e-f46a-41fa-8b74-6cbed047f9af')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" id="code_img_closed_d64aa65e-f46a-41fa-8b74-6cbed047f9af" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" id="code_img_opened_d64aa65e-f46a-41fa-8b74-6cbed047f9af" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_d64aa65e-f46a-41fa-8b74-6cbed047f9af" class="cnblogs_code_hide">
<pre>    <span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> Mutex mLock = <span style="color: #0000ff;">new</span><span style="color: #000000;"> Mutex();
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">int</span> nums = <span style="color: #800080;">0</span><span style="color: #000000;">;
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Run()
        {
            </span><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> i = <span style="color: #800080;">0</span>; i &lt; <span style="color: #800080;">10</span>; i++<span style="color: #000000;">)
            {
                mLock.WaitOne();
                Console.WriteLine(nums</span>++<span style="color: #000000;">);
                mLock.ReleaseMutex();
            }
        }
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {

            </span><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> i = <span style="color: #800080;">0</span>; i &lt; <span style="color: #800080;">5</span>; i++<span style="color: #000000;">)
            {
                Task.Run(() </span>=&gt;<span style="color: #000000;">
                {
                    Run();
                });
            }
            Thread.Sleep(</span><span style="color: #800080;">5000</span><span style="color: #000000;">);

            Console.ReadKey();
        }
    }</span></pre>
</div>
<span class="cnblogs_code_collapse">Mutex</span></div>
<p>这四种锁都有一个WaitOne方法，因为他们都继承WaitHandle，这四种锁本是同根生，底层都是通过SafeWaitHandle来对win32api的一个引用</p>
<p>⑤读写锁</p>
<p>如果写入线程时间太久，比如10s。这个时候读的线程会被卡死。从而超时</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('3fe734c0-6f5d-4a1f-828a-35511e1e47c5')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" id="code_img_closed_3fe734c0-6f5d-4a1f-828a-35511e1e47c5" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" id="code_img_opened_3fe734c0-6f5d-4a1f-828a-35511e1e47c5" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_3fe734c0-6f5d-4a1f-828a-35511e1e47c5" class="cnblogs_code_hide">
<pre>    <span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> ReaderWriterLock rwLock = <span style="color: #0000ff;">new</span><span style="color: #000000;"> ReaderWriterLock();
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {

            </span><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> i = <span style="color: #800080;">0</span>; i &lt; <span style="color: #800080;">5</span>; i++<span style="color: #000000;">)
            {
                Task.Factory.StartNew(() </span>=&gt;<span style="color: #000000;">
                {
                    Read();
                });
            }

            Task.Factory.StartNew(() </span>=&gt;<span style="color: #000000;">
            {
                Write();
            });

            Console.ReadKey();
        }

        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Read()
        {
            </span><span style="color: #0000ff;">while</span> (<span style="color: #0000ff;">true</span><span style="color: #000000;">)
            {
                rwLock.AcquireReaderLock(</span><span style="color: #0000ff;">int</span><span style="color: #000000;">.MaxValue);
                Thread.Sleep(</span><span style="color: #800080;">100</span><span style="color: #000000;">);
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">read {0}</span><span style="color: #800000;">"</span><span style="color: #000000;">, Thread.CurrentThread.ManagedThreadId);
                rwLock.ReleaseReaderLock();
            }
        }
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Write()
        {
            </span><span style="color: #0000ff;">while</span> (<span style="color: #0000ff;">true</span><span style="color: #000000;">)
            {
                Thread.Sleep(</span><span style="color: #800080;">3000</span><span style="color: #000000;">);
                rwLock.AcquireWriterLock(</span><span style="color: #0000ff;">int</span><span style="color: #000000;">.MaxValue);
                Thread.Sleep(</span><span style="color: #800080;">3000</span><span style="color: #000000;">);
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">write {0}</span><span style="color: #800000;">"</span><span style="color: #000000;">, Thread.CurrentThread.ManagedThreadId);
                rwLock.ReleaseWriterLock();
            }
        }
    }</span></pre>
</div>
<span class="cnblogs_code_collapse">ReaderWriterLock</span></div>
<p>⑥监视锁</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('6878540b-dc78-4658-8673-315ca06a68ff')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" id="code_img_closed_6878540b-dc78-4658-8673-315ca06a68ff" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" id="code_img_opened_6878540b-dc78-4658-8673-315ca06a68ff" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_6878540b-dc78-4658-8673-315ca06a68ff" class="cnblogs_code_hide">
<pre>    <span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">object</span> objLock = <span style="color: #0000ff;">new</span> <span style="color: #0000ff;">object</span><span style="color: #000000;">();
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> i = <span style="color: #800080;">0</span>; i &lt; <span style="color: #800080;">5</span>; i++<span style="color: #000000;">)
            {
                Task.Run(() </span>=&gt;<span style="color: #000000;">
                {
                    Run();
                });
            }
            Console.ReadKey();
        }

        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">int</span> nums = <span style="color: #800080;">0</span><span style="color: #000000;">;
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Run() {

            </span><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> i = <span style="color: #800080;">0</span>; i &lt; <span style="color: #800080;">100</span>; i++<span style="color: #000000;">)
            {
                </span><span style="color: #0000ff;">var</span> b = <span style="color: #0000ff;">false</span><span style="color: #000000;">;
                </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
                {
                    Monitor.Enter(objLock, </span><span style="color: #0000ff;">ref</span><span style="color: #000000;"> b);
                    Console.WriteLine(nums</span>++<span style="color: #000000;">);
                }
                </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (Exception ex)
                {
                    Console.WriteLine(ex.Message);
                }
                </span><span style="color: #0000ff;">finally</span><span style="color: #000000;">
                {
                    </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (b) Monitor.Exit(objLock);
                }
            }
        }
       
    }</span></pre>
</div>
<span class="cnblogs_code_collapse">lock</span></div>
<p>&nbsp;</p>
<p>3，混合锁</p>
<p>用户模式+内核模式（场景是最多的）</p>
<p>在用户模式下内旋，如果超过一定的阔值，会切换到内核锁。在内旋的情况下，我们会看到大量的Sleep(0)、Sleep(1)、Yield等</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201801/741594-20180115224641193-1035129780.png" alt="" /></p>
<p>①ManualResetEventSlim</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('5a508854-4fde-4c89-951f-f04b86ab4fd7')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" id="code_img_closed_5a508854-4fde-4c89-951f-f04b86ab4fd7" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" id="code_img_opened_5a508854-4fde-4c89-951f-f04b86ab4fd7" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_5a508854-4fde-4c89-951f-f04b86ab4fd7" class="cnblogs_code_hide">
<pre>    <span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> ManualResetEventSlim mrsLock = <span style="color: #0000ff;">new</span><span style="color: #000000;"> ManualResetEventSlim();
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> i = <span style="color: #800080;">0</span>; i &lt; <span style="color: #800080;">5</span>; i++<span style="color: #000000;">)
            {
                Task.Run(() </span>=&gt;<span style="color: #000000;">
                {
                    Run();
                });
            }

            Thread.Sleep(</span><span style="color: #800080;">1000</span><span style="color: #000000;">);
            mrsLock.Set();
            Console.ReadKey();
        }

        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">int</span> nums = <span style="color: #800080;">0</span><span style="color: #000000;">;
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Run()
        {
            </span><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> i = <span style="color: #800080;">0</span>; i &lt; <span style="color: #800080;">1000</span>; i++<span style="color: #000000;">)
            {
                mrsLock.Wait();</span><span style="color: #008000;">//</span><span style="color: #008000;">等待1秒后才会执行。拦一批值</span>
                Console.WriteLine(nums++<span style="color: #000000;">);
            }
        }
       
    }</span></pre>
</div>
<span class="cnblogs_code_collapse">ManualResetEventSlim </span></div>
<p>②SemaphoreSlim</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('b8271936-5f6b-45b7-9c2c-7f95f50ef523')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" id="code_img_closed_b8271936-5f6b-45b7-9c2c-7f95f50ef523" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" id="code_img_opened_b8271936-5f6b-45b7-9c2c-7f95f50ef523" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_b8271936-5f6b-45b7-9c2c-7f95f50ef523" class="cnblogs_code_hide">
<pre>    <span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> SemaphoreSlim mrsLock = <span style="color: #0000ff;">new</span> SemaphoreSlim(<span style="color: #800080;">1</span>,<span style="color: #800080;">10</span><span style="color: #000000;">);
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> i = <span style="color: #800080;">0</span>; i &lt; <span style="color: #800080;">5</span>; i++<span style="color: #000000;">)
            {
                Task.Run(() </span>=&gt;<span style="color: #000000;">
                {
                    Run();
                });
            }

            Console.ReadKey();
        }

        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">int</span> nums = <span style="color: #800080;">0</span><span style="color: #000000;">;
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Run()
        {
            </span><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> i = <span style="color: #800080;">0</span>; i &lt; <span style="color: #800080;">1000</span>; i++<span style="color: #000000;">)
            {
                mrsLock.Wait();
                Console.WriteLine(nums</span>++<span style="color: #000000;">);
                mrsLock.Release();
            }
        }
       
    }</span></pre>
</div>
<span class="cnblogs_code_collapse">SemaphoreSlim</span></div>
<p>③ReaderWriterLockSlim</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('d1e966a9-e093-42ca-9c50-ceec5ba0be5e')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" id="code_img_closed_d1e966a9-e093-42ca-9c50-ceec5ba0be5e" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" id="code_img_opened_d1e966a9-e093-42ca-9c50-ceec5ba0be5e" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_d1e966a9-e093-42ca-9c50-ceec5ba0be5e" class="cnblogs_code_hide">
<pre>    <span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> ReaderWriterLockSlim rwLock = <span style="color: #0000ff;">new</span><span style="color: #000000;"> ReaderWriterLockSlim();
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {

            </span><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> i = <span style="color: #800080;">0</span>; i &lt; <span style="color: #800080;">5</span>; i++<span style="color: #000000;">)
            {
                Task.Factory.StartNew(() </span>=&gt;<span style="color: #000000;">
                {
                    Read();
                });
            }

            Task.Factory.StartNew(() </span>=&gt;<span style="color: #000000;">
            {
                Write();
            });

            Console.ReadKey();
        }

        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Read()
        {
            </span><span style="color: #0000ff;">while</span> (<span style="color: #0000ff;">true</span><span style="color: #000000;">)
            {
                rwLock.EnterReadLock();
                Thread.Sleep(</span><span style="color: #800080;">100</span><span style="color: #000000;">);
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">read {0}</span><span style="color: #800000;">"</span><span style="color: #000000;">, Thread.CurrentThread.ManagedThreadId);
                rwLock.ExitReadLock();
            }
        }
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Write()
        {
            </span><span style="color: #0000ff;">while</span> (<span style="color: #0000ff;">true</span><span style="color: #000000;">)
            {
                Thread.Sleep(</span><span style="color: #800080;">3000</span><span style="color: #000000;">);
                rwLock.EnterWriteLock();
                Thread.Sleep(</span><span style="color: #800080;">3000</span><span style="color: #000000;">);
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">write {0}</span><span style="color: #800000;">"</span><span style="color: #000000;">, Thread.CurrentThread.ManagedThreadId);
                rwLock.ExitWriteLock();
            }
        }
    }</span></pre>
</div>
<span class="cnblogs_code_collapse">ReaderWriterLockSlim</span></div>
<p>&nbsp;</p>