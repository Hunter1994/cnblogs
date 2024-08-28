<p><a href="#a1"><strong>一、线程池</strong></a></p>
<p><a href="#a2"><strong><strong>二、执行上下文</strong></strong></a></p>
<p><a href="#a3"><strong><strong><strong>三、协作式取消和超时</strong></strong></strong></a></p>
<p><a href="#a4"><strong><strong><strong><strong>四、任务</strong></strong></strong></strong></a></p>
<p><a href="#a5"><strong><strong><strong><strong><strong>五、并行语言集成查询（PLINQ</strong></strong></strong></strong></strong></a></p>
<p><a href="#a6"><strong><strong><strong><strong><strong><strong>六、执行定时计算限制操作</strong></strong></strong></strong></strong></strong></a></p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a1"></a>一、线程池</span></strong></span></p>
<p>1，CLR初始化时，线程池中是没有线程的。在内部，线程池维护了一个操作请求队列</p>
<p>2，每CLR一个线程池，这个线程池有CLR控制的所有AppDomain共享。如果一个进程加载了多个CLR，那么每个CLR都有它自己的线程池<br />3，要将一个异步的计算限制操作放到线程池的队列中，通常使用ThreadPool类定义的以下方法之一</p>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">bool</span><span style="color: #000000;"> QueueUserWorkItem(WaitCallback callBack);
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">bool</span> QueueUserWorkItem(WaitCallback callBack, <span style="color: #0000ff;">object</span> state);</pre>
</div>
<p>这些方法向线程池的队列中加一个&ldquo;工作项&rdquo;（callBack）以及可选的状态数据。然后，所有方法会立即返回。无state参数的那个版本向回调方法传递一个null</p>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            ThreadPool.QueueUserWorkItem(ComputeBoundOp, </span><span style="color: #800080;">5</span><span style="color: #000000;">);
        }

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> ComputeBoundOp(Object state)
        {
            Console.WriteLine(state);<br />　　　　　　　//这个方法返回后，线程回到池中，等待另一个任务
        }</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a2"></a>二、执行上下文</span></strong></span></p>
<p>1，每个线程都关联一个执行上下文数据结构。<br />2，执行上下文包括<br />①安全设施（压缩栈、Thread的Principal、Windwos身份）<br />②宿主设置（参见System.Threading.HostExecutionContextManager）<br />③逻辑调用上下文数据（System.Runtime.Remoting.Messaging.CallContext的LogicalGetData和LogicalSetData方法）<br />3，每当一个线程（初始线程）使用另一个线程（辅助线性）执行任务时，前者的执行上下文应该流向（复制到）辅助线性。这会对性能造成影响。<br />4，System.Threading.ExecutionContext类控制线程的执行上下文如果从一个线程&ldquo;流&rdquo;向另一个</p>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">sealed</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ExecutionContext : IDisposable, ISerializable
    {
        [SecurityCritical]
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> AsyncFlowControl SuppressFlow();<span style="color: #008000;">//</span><span style="color: #008000;">阻止流</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> RestoreFlow();<span style="color: #008000;">//</span><span style="color: #008000;">恢复流</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> Boolean IsFlowSuppressed();<span style="color: #008000;">//</span><span style="color: #008000;">是否阻止流</span>
    }</pre>
</div>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">将一些数据方法Main线程的逻辑调用上下文中</span>
            CallContext.LogicalSetData(<span style="color: #800000;">"</span><span style="color: #800000;">Name</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">Hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">执行上下文流向辅助线程，辅助线程可以访问逻辑调用上下文的数据</span>
            ThreadPool.QueueUserWorkItem(r =&gt; Console.WriteLine(CallContext.LogicalGetData(<span style="color: #800000;">"</span><span style="color: #800000;">Name</span><span style="color: #800000;">"</span><span style="color: #000000;">)));

            </span><span style="color: #008000;">//</span><span style="color: #008000;">现在，阻止Main线程的执行上下文</span>
<span style="color: #000000;">            ExecutionContext.SuppressFlow();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">辅助线程不能访问逻辑调用上下文的数据</span>
            ThreadPool.QueueUserWorkItem(r =&gt; Console.WriteLine(CallContext.LogicalGetData(<span style="color: #800000;">"</span><span style="color: #800000;">Name</span><span style="color: #800000;">"</span><span style="color: #000000;">)));

            </span><span style="color: #008000;">//</span><span style="color: #008000;">恢复Main线程的执行上下文的流动，以免将来使用更多的线程池线程</span>
<span style="color: #000000;">            ExecutionContext.RestoreFlow();

            ThreadPool.QueueUserWorkItem(r </span>=&gt; Console.WriteLine(CallContext.LogicalGetData(<span style="color: #800000;">"</span><span style="color: #800000;">Name</span><span style="color: #800000;">"</span><span style="color: #000000;">)));

            </span><span style="color: #008000;">//</span><span style="color: #008000;">输出：
            </span><span style="color: #008000;">//</span><span style="color: #008000;">Hunter
            </span><span style="color: #008000;">//</span>
            <span style="color: #008000;">//</span><span style="color: #008000;">Hunter</span>
<span style="color: #000000;">            Console.ReadLine();
        }</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a3"></a>三、协作式取消和超时</span></strong></span></p>
<p><strong>1，CancellationTokenSource</strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">        static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">取消操作首先创建此对象</span>
            CancellationTokenSource cts = <span style="color: #0000ff;">new</span><span style="color: #000000;"> CancellationTokenSource();

            ThreadPool.QueueUserWorkItem(r </span>=&gt;<span style="color: #000000;"> Count(cts.Token));

            Thread.Sleep(</span><span style="color: #800080;">2000</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">如果Count方法已返回，Cancel没有任何效果</span>
            cts.Cancel();<span style="color: #008000;">//</span><span style="color: #008000;">取消操作

            </span><span style="color: #008000;">//</span><span style="color: #008000;">输出：
            </span><span style="color: #008000;">//</span><span style="color: #008000;">0
            </span><span style="color: #008000;">//</span><span style="color: #008000;">1
            </span><span style="color: #008000;">//</span><span style="color: #008000;">2
            </span><span style="color: #008000;">//</span><span style="color: #008000;">取消了</span>
<span style="color: #000000;">            Console.ReadLine();
        }

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Count(CancellationToken token)
        {
            </span><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> i = <span style="color: #800080;">0</span>; i &lt; <span style="color: #800080;">10</span>; i++<span style="color: #000000;">)
            {
                Console.WriteLine(i);

                </span><span style="color: #0000ff;">if</span> (token.IsCancellationRequested)<span style="color: #008000;">//</span><span style="color: #008000;">是否取消了</span>
<span style="color: #000000;">                {
                    Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">取消了</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                    </span><span style="color: #0000ff;">break</span><span style="color: #000000;">;
                }
                Thread.Sleep(</span><span style="color: #800080;">1000</span><span style="color: #000000;">);
            }

        }</span></pre>
</div>
<p>要执行一个不允许被取消的操作，可向该操作传递通过调用CancellationToken.None属性而返回的CancellationToken，该属性返回的CancellationToken不和任何CancellationTokenSource对象关联（实例的私有字段为null）</p>
<p><strong>&nbsp;2，取消回调</strong></p>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">取消操作首先创建此对象</span>
            CancellationTokenSource cts = <span style="color: #0000ff;">new</span><span style="color: #000000;"> CancellationTokenSource();
            cts.Token.Register(() </span>=&gt; Console.WriteLine(<span style="color: #800000;">"</span><span style="color: #800000;">取消回调1</span><span style="color: #800000;">"</span><span style="color: #000000;">));
            cts.Token.Register(() </span>=&gt; Console.WriteLine(<span style="color: #800000;">"</span><span style="color: #800000;">取消回调2</span><span style="color: #800000;">"</span><span style="color: #000000;">));

            cts.Cancel();</span><span style="color: #008000;">//</span><span style="color: #008000;">取消操作

            </span><span style="color: #008000;">//</span><span style="color: #008000;">输出：
            </span><span style="color: #008000;">//</span><span style="color: #008000;">取消回调2
            </span><span style="color: #008000;">//</span><span style="color: #008000;">取消回调1</span>
<span style="color: #000000;">            Console.ReadLine();
        }</span></pre>
</div>
<p>①useSynchronizationContext参数：</p>
<p>false:调用Cancel的线程会顺序调用已登记的所有方法</p>
<p>true:回调方法会被send给已捕捉的useSynchronizationContext对象</p>
<p>②CancellationTokenSource的Cancel方法参数</p>
<p>true：抛出了未处理异常的第一个方法会阻止其他回调方法的执行，抛出的异常会从Cancel中抛出</p>
<p>false：所有的回调方法都会执行。所有未处理的异常会被添加到一个集合中，抛出的异常会从Cancel中抛出（AggregateException）</p>
<p><strong>3，向一个CancellationTokenSource登记两个回调</strong></p>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建一个CancellationTokenSource</span>
            <span style="color: #0000ff;">var</span> cts1 =<span style="color: #0000ff;">new</span><span style="color: #000000;"> CancellationTokenSource();
            cts1.Token.Register(() </span>=&gt; Console.WriteLine(<span style="color: #800000;">"</span><span style="color: #800000;">cts1 取消了</span><span style="color: #800000;">"</span><span style="color: #000000;">));

            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建另一个创建一个CancellationTokenSource</span>
            <span style="color: #0000ff;">var</span> cts2 = <span style="color: #0000ff;">new</span><span style="color: #000000;"> CancellationTokenSource();
            cts2.Token.Register(() </span>=&gt; Console.WriteLine(<span style="color: #800000;">"</span><span style="color: #800000;">cts2 取消了</span><span style="color: #800000;">"</span><span style="color: #000000;">));

            </span><span style="color: #008000;">//</span><span style="color: #008000;">创一个新的CancellationTokenSource，它在cts1或cts2取消时取消</span>
            <span style="color: #0000ff;">var</span> linkedCts =<span style="color: #000000;"> CancellationTokenSource.CreateLinkedTokenSource(cts1.Token, cts2.Token);
            linkedCts.Token.Register(() </span>=&gt; Console.WriteLine(<span style="color: #800000;">"</span><span style="color: #800000;">linkedCts 取消了</span><span style="color: #800000;">"</span><span style="color: #000000;">));

            cts2.Cancel();

            Console.WriteLine(cts1.IsCancellationRequested</span>+<span style="color: #800000;">"</span> <span style="color: #800000;">"</span>+cts2.IsCancellationRequested+<span style="color: #800000;">"</span> <span style="color: #800000;">"</span>+<span style="color: #000000;">linkedCts.IsCancellationRequested);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">输出：
            </span><span style="color: #008000;">//</span><span style="color: #008000;">linkedCts 取消了
            </span><span style="color: #008000;">//</span><span style="color: #008000;">cts2 取消了
            </span><span style="color: #008000;">//</span><span style="color: #008000;">Flase True True</span>
<span style="color: #000000;">            Console.ReadLine();
        }</span></pre>
</div>
<p><strong>4，超时取消</strong></p>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            
            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建另一个创建一个CancellationTokenSource</span>
            <span style="color: #0000ff;">var</span> cts2 = <span style="color: #0000ff;">new</span><span style="color: #000000;"> CancellationTokenSource();
            cts2.Token.Register(() </span>=&gt; { Console.WriteLine(<span style="color: #800000;">"</span><span style="color: #800000;">cts2 取消了</span><span style="color: #800000;">"</span><span style="color: #000000;">); });
            cts2.CancelAfter(</span><span style="color: #800080;">1000</span>);<span style="color: #008000;">//</span><span style="color: #008000;">如果1秒钟还没有执行到cts2.Cancel()取消，则自动取消</span>
<span style="color: #000000;">
            Thread.Sleep(</span><span style="color: #800080;">100000</span><span style="color: #000000;">);
            
            cts2.Cancel();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">1秒中之后程序回输出：cts2 取消了</span>
<span style="color: #000000;">            Console.ReadLine();
        }</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a4"></a>四、任务</span></strong></span></p>
<p>ThreadPool.QueueUserWorkItem()没有内建机制让你知道操作在什么时候完成，也没有机制在完成操作时获得返回值</p>
<div class="cnblogs_code">
<pre>            ThreadPool.QueueUserWorkItem(r =&gt; { }); <span style="color: #008000;">//</span><span style="color: #008000;">调用QueueUserWorkItem</span>
            <span style="color: #0000ff;">new</span> Task(r =&gt; { Console.WriteLine(r); }, <span style="color: #800080;">5</span>).Start(); <span style="color: #008000;">//</span><span style="color: #008000;">用Task来做相同的事情。输出5</span>
            Task.Run(() =&gt; { }); <span style="color: #008000;">//</span><span style="color: #008000;">另一个等价写法</span></pre>
</div>
<p>可选择向构造器传递一些TaskCreationOptions标志来控制Task的执行方式</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">        [Flags,Serializable]
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">enum</span><span style="color: #000000;"> TaskCreationOptions
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">默认</span>
            None = <span style="color: #800080;">0x0000</span><span style="color: #000000;">,
            </span><span style="color: #008000;">//</span><span style="color: #008000;">提议TaskScheduler你希望该任务尽快执行（给你的感觉就像queue的感觉）</span>
            PreRunning = <span style="color: #800080;">0x0001</span><span style="color: #000000;">,
            </span><span style="color: #008000;">//</span><span style="color: #008000;">提议TaskScheduler应尽可能地创建线程池线程(如果是长时间运行的任务，建议使用此选项，使用此选项会创建一个线程，还不是使用线程池)</span>
            LongRunning = <span style="color: #800080;">0x0002</span><span style="color: #000000;">,
            </span><span style="color: #008000;">//</span><span style="color: #008000;">该提议总是被采纳：将一个Task和它的父Task关联</span>
            AttachedToParent=<span style="color: #800080;">0x0004</span><span style="color: #000000;">,
            </span><span style="color: #008000;">//</span><span style="color: #008000;">该提议总是被采纳：如果一个任务视图和这个父任务链接，它就是一个普通任务，而不是子任务</span>
            DenyChildAttach = <span style="color: #800080;">0x0008</span><span style="color: #000000;">,
            </span><span style="color: #008000;">//</span><span style="color: #008000;">该提议总是被采纳：强迫子任务使用默认调度器而不是父任务的调度器</span>
            HideScheduler = <span style="color: #800080;">0x0010</span><span style="color: #000000;">,
        }</span></pre>
</div>
<p><strong>&nbsp;1，等待任务完成并获取结果</strong></p>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建一个任务，现在还没有开始运行</span>
            Task&lt;<span style="color: #0000ff;">int</span>&gt; t1 = <span style="color: #0000ff;">new</span> Task&lt;<span style="color: #0000ff;">int</span>&gt;(() =&gt; <span style="color: #800080;">1</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">可以后再启动任务</span>
<span style="color: #000000;">            t1.Start();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">可选择显示等待任务完成</span>
<span style="color: #000000;">            t1.Wait();

            Console.WriteLine(t1.Result);</span><span style="color: #008000;">//</span><span style="color: #008000;">输出：1</span>
<span style="color: #000000;">
            Console.ReadLine();
        }</span></pre>
</div>
<p>任务抛出异常会被吞噬并存储到一个集合中，而线程池线程可以返回到线程池中。调用Wait方法或者Result属性时，这些成员会抛出一个System.AggregateException对象</p>
<p>除了等待单个任务，还可以等待一个Task对象数组</p>
<div class="cnblogs_code">
<pre>            <span style="color: #008000;">//</span><span style="color: #008000;">会阻塞调用线程，直到数组中的任何Task对象完成
            </span><span style="color: #008000;">//</span><span style="color: #008000;">方法返回Int32数组索引值，指明完成的是哪个Task对象
            </span><span style="color: #008000;">//</span><span style="color: #008000;">方法返回后。线程被唤醒并继续运行
            </span><span style="color: #008000;">//</span><span style="color: #008000;">如果发生超时，方法返回-1
            </span><span style="color: #008000;">//</span><span style="color: #008000;">如果WaitAny通过一个CancellationToken取消，会抛出一个OperationCanceledException</span>
<span style="color: #000000;">            Task.WaitAny(task1, task2);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">会阻塞调用线程，直到数组中的所有Task对象完成
            </span><span style="color: #008000;">//</span><span style="color: #008000;">所有Task对象都完成，WaitAll返回true
            </span><span style="color: #008000;">//</span><span style="color: #008000;">如果发生超时，方法返回false
            </span><span style="color: #008000;">//</span><span style="color: #008000;">如果WaitAll通过一个CancellationToken取消，会抛出一个OperationCanceledException</span>
            Task.WaitAll(task1, task2);</pre>
</div>
<p><strong>2，取消任务</strong></p>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {

            CancellationTokenSource cts </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> CancellationTokenSource();

            Task</span>&lt;Int32&gt; t = Task.Run(() =&gt; Sum(cts.Token, <span style="color: #800080;">100</span><span style="color: #000000;">), cts.Token);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">在之后的某个时间，取消CancellationTokenSource以取消Task</span>
<span style="color: #000000;">            cts.Cancel();

            </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;">如果任务已取消，Result会抛出一个AggregateException异常</span>
<span style="color: #000000;">                Console.WriteLine(t.Result);
            }
            </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (AggregateException x)
            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;">将任何OperationCanceledException对象都视为已处理
                </span><span style="color: #008000;">//</span><span style="color: #008000;">其他任何异常都造成抛出一个新的AggregateException
                </span><span style="color: #008000;">//</span><span style="color: #008000;">其中只包含未处理的异常</span>
                x.Handle(e =&gt; e <span style="color: #0000ff;">is</span><span style="color: #000000;"> OperationCanceledException);
                </span><span style="color: #008000;">//</span><span style="color: #008000;">所有异常都处理好之后，执行下面这一行</span>
                Console.WriteLine(<span style="color: #800000;">"</span><span style="color: #800000;">计算已取消</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }

            Console.ReadLine();
        }


        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> Int32 Sum(CancellationToken token, Int32 n)
        {
            </span><span style="color: #0000ff;">int</span> num = <span style="color: #800080;">0</span><span style="color: #000000;">;
            </span><span style="color: #0000ff;">for</span> (; n &gt; <span style="color: #800080;">0</span>; n--<span style="color: #000000;">)
            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;">如果任务取消，则抛出OperationCanceledException异常
                </span><span style="color: #008000;">//</span><span style="color: #008000;">这样设计是因为Task会捕获异常</span>
<span style="color: #000000;">                token.ThrowIfCancellationRequested();

                </span><span style="color: #0000ff;">checked</span><span style="color: #000000;">
                {
                    num </span>+=<span style="color: #000000;"> n;
                }
            }
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> num;
        }</span></pre>
</div>
<p><strong>4，任务完成时自动启动新任务&nbsp;</strong></p>
<p>TaskContinuationOptions.OnlyOnCanceled//第一个任务被取消时才执行<br />            TaskContinuationOptions.OnlyOnFaulted//第一个任务被抛异常时才执行<br />            TaskContinuationOptions.OnlyOnRanToCompletion//第一个任务顺利完成时才执行</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">        [Flags, Serializable]
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">enum</span><span style="color: #000000;"> TaskContinuationOptions
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">默认</span>
            None = <span style="color: #800080;">0x0000</span><span style="color: #000000;">,
            </span><span style="color: #008000;">//</span><span style="color: #008000;">提议TaskScheduler你希望该任务尽快执行</span>
            PreferRunning = <span style="color: #800080;">0x0001</span><span style="color: #000000;">,
            </span><span style="color: #008000;">//</span><span style="color: #008000;">提议TaskScheduler应尽可能地创建线程池线程</span>
            LongRunning = <span style="color: #800080;">0x0002</span><span style="color: #000000;">,
            </span><span style="color: #008000;">//</span><span style="color: #008000;">AttachedToParent：将一个Task和它的父Task关联</span>
            AttachedToParent = <span style="color: #800080;">0x0004</span><span style="color: #000000;">,
            </span><span style="color: #008000;">//</span><span style="color: #008000;">该提议总是被采纳：如果一个任务视图和这个父任务链接，它就是一个普通任务，而不是子任务</span>
            DenyChildAttach = <span style="color: #800080;">0x0008</span><span style="color: #000000;">,
            </span><span style="color: #008000;">//</span><span style="color: #008000;">该提议总是被采纳：强迫子任务使用默认调度器而不是父任务的调度器</span>
            HideScheduler = <span style="color: #800080;">0x0010</span><span style="color: #000000;">,
            </span><span style="color: #008000;">//</span><span style="color: #008000;">除非前置任务（antecedent task）完成，否则精致延续任务完成（取消）</span>
            LazyCancellation = <span style="color: #800080;">0x0020</span><span style="color: #000000;">,

            </span><span style="color: #008000;">//</span><span style="color: #008000;">这个标志指出你希望由执行第一个任务的线程执行ContinueWith任务。
            </span><span style="color: #008000;">//</span><span style="color: #008000;">第一个任务完成后，调用ContinueWith的线程接着执行ContinueWith任务</span>
            ExecuteSynchronously = <span style="color: #800080;">0x80000</span><span style="color: #000000;">,

            </span><span style="color: #008000;">//</span><span style="color: #008000;">这些标志指出在什么情况下运行ContinueWith任务</span>
            NotOnRanToCompletion = <span style="color: #800080;">0x10000</span><span style="color: #000000;">,
            NotOnFaulted </span>= <span style="color: #800080;">0x20000</span><span style="color: #000000;">,
            NotOnCanceled </span>= <span style="color: #800080;">0x40000</span><span style="color: #000000;">,

            </span><span style="color: #008000;">//</span><span style="color: #008000;">这些标志是以上三个标志的遍历组合</span>
            OnlyOnCanceled = NotOnRanToCompletion | NotOnFaulted,<span style="color: #008000;">//</span><span style="color: #008000;">第一个任务被取消时才执行</span>
            OnlyOnFaulted = NotOnRanToCompletion | NotOnCanceled,<span style="color: #008000;">//</span><span style="color: #008000;">第一个任务被抛异常时才执行</span>
            OnlyOnRanToCompletion = NotOnFaulted | NotOnCanceled<span style="color: #008000;">//</span><span style="color: #008000;">第一个任务顺利完成时才执行</span>
        }</pre>
</div>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {

            </span><span style="color: #0000ff;">var</span> t1 = Task.Run(() =&gt;Console.WriteLine(<span style="color: #800000;">"</span><span style="color: #800000;">第一个任务</span><span style="color: #800000;">"</span><span style="color: #000000;">));
            t1.ContinueWith(task </span>=&gt; Console.WriteLine(<span style="color: #800000;">"</span><span style="color: #800000;">任务顺利完成时执行</span><span style="color: #800000;">"</span><span style="color: #000000;">), TaskContinuationOptions.OnlyOnRanToCompletion);
            t1.ContinueWith(task </span>=&gt; Console.WriteLine(<span style="color: #800000;">"</span><span style="color: #800000;">任务抛异常时执行</span><span style="color: #800000;">"</span><span style="color: #000000;">), TaskContinuationOptions.OnlyOnFaulted);
            t1.ContinueWith(task </span>=&gt; Console.WriteLine(<span style="color: #800000;">"</span><span style="color: #800000;">任务取消时执行</span><span style="color: #800000;">"</span><span style="color: #000000;">), TaskContinuationOptions.OnlyOnCanceled);
            </span><span style="color: #008000;">//</span><span style="color: #008000;">输出：
            </span><span style="color: #008000;">//</span><span style="color: #008000;">第一个任务
            </span><span style="color: #008000;">//</span><span style="color: #008000;">任务顺利完成时执行</span>
<span style="color: #000000;">
            Console.ReadLine();
        }</span></pre>
</div>
<p><strong>5，任务可以启动子任务</strong></p>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">提高性能，一个任务泵本需要3秒执行完，使用子任务只需要1秒多就可以执行完</span>
            Task&lt;Int32[]&gt; parent = <span style="color: #0000ff;">new</span> Task&lt;Int32[]&gt;(() =&gt;<span style="color: #000000;">
            {
                </span><span style="color: #0000ff;">var</span> results = <span style="color: #0000ff;">new</span> <span style="color: #0000ff;">int</span>[<span style="color: #800080;">3</span><span style="color: #000000;">];

                </span><span style="color: #008000;">//</span><span style="color: #008000;">创建并启动3个子任务</span>
                <span style="color: #0000ff;">new</span> Task(() =&gt;<span style="color: #000000;">
                {
                    Thread.Sleep(</span><span style="color: #800080;">1000</span><span style="color: #000000;">);
                    results[</span><span style="color: #800080;">0</span>] = <span style="color: #800080;">1</span><span style="color: #000000;">;
                }, TaskCreationOptions.AttachedToParent).Start();
                </span><span style="color: #0000ff;">new</span> Task(() =&gt;<span style="color: #000000;">
                {
                    Thread.Sleep(</span><span style="color: #800080;">1000</span><span style="color: #000000;">);
                    results[</span><span style="color: #800080;">1</span>] = <span style="color: #800080;">2</span><span style="color: #000000;">;
                }, TaskCreationOptions.AttachedToParent).Start();
                </span><span style="color: #0000ff;">new</span> Task(() =&gt;<span style="color: #000000;">
                {
                    Thread.Sleep(</span><span style="color: #800080;">1000</span><span style="color: #000000;">);
                    results[</span><span style="color: #800080;">2</span>] = <span style="color: #800080;">3</span><span style="color: #000000;">;
                }, TaskCreationOptions.AttachedToParent).Start();

                </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> results;
            });

            </span><span style="color: #008000;">//</span><span style="color: #008000;">父任务及其子任务运行完成后，用一个延续任务显示结果</span>
            parent.ContinueWith(parentTask =&gt;<span style="color: #000000;"> Array.ForEach(parentTask.Result, Console.WriteLine));

            </span><span style="color: #008000;">//</span><span style="color: #008000;">启动父任务，便于它启动它的子任务</span>
<span style="color: #000000;">            parent.Start();

            Console.ReadLine();
        }</span></pre>
</div>
<p>&nbsp;TaskCreationOptions.AttachedToParent标志将一个Task和创建它的Task关联，结果是除非所有子任务（以及子任务的子任务）结束运行，否则创建任务（父任务）不认为已经结束</p>
<p><strong>6，任务内部揭秘</strong></p>
<p>①每个Task对象都有一组字段。必须为这些字段分配内存<br />Int32 ID（只读唯一标识，首次查询此字段时分配）<br />代表Task执行状态的一个Int32<br />对父任务的引用<br />对Task创建时指定的TaskScheduler的引用<br />对回调方法的引用<br />对要传给回调方法的对象的引用（可通过Task的只读AsyncState属性查询）<br />对ExecutionContext的引用<br />对ManualResetEventSlim对象的引用</p>
<p>&nbsp;</p>
<p>②Task生存期状态</p>
<div class="cnblogs_code">
<pre>    <span style="color: #008000;">//</span><span style="color: #008000;">这些标志指出一个Task在其生命周期内的状态</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">enum</span><span style="color: #000000;"> TaskStatus
    {
        Created,</span><span style="color: #008000;">//</span><span style="color: #008000;">任务以显示创建；可以手动Start()这个任务</span>
        WaitingForActivation,<span style="color: #008000;">//</span><span style="color: #008000;">任务以隐式创建；会自动开始</span>
        WaitingToRun,<span style="color: #008000;">//</span><span style="color: #008000;">任务以调度，但尚未运行</span>
        Running,<span style="color: #008000;">//</span><span style="color: #008000;">任务正在运行</span>
        WaitingForChildrenToComplate,<span style="color: #008000;">//</span><span style="color: #008000;">任务正在等待它的子任务完成，子任务完成后它才完成

        </span><span style="color: #008000;">//</span><span style="color: #008000;">任务最重状态时以下三个之一</span>
        RanToComplation,<span style="color: #008000;">//</span><span style="color: #008000;">运行完成</span>
        Canceled,<span style="color: #008000;">//</span><span style="color: #008000;">取消</span>
        Faulted<span style="color: #008000;">//</span><span style="color: #008000;">出错</span>
    }</pre>
</div>
<p>首次构造Task对象时，状态为Created<br />当任务启动时，它的状态变成WaitingToRun<br />Task实际在一个线程上运行时，它的状态变成Runting<br />任务停止运行并等待它的任何子任务时，状态变成WaitingForChildrenToComlate<br />任务完成时变成以下状态之一：RanToComplate（运行完成）、Canceled（取消）、Faulted（出错）<br />调用ContinueWith、ContinueWhenAll、ContinueWhenAny或FromAsync等方法创建的Task对象出于WaitingForActivation状态<br />通过TaskComplationSource&lt;TResult&gt;对象创建的Task也出于WaitingForActivation状态</p>
<p>&nbsp;</p>
<p><strong>7，任务工厂</strong></p>
<p>为什么要使用任务工厂：有时需要创建一组共享相同配置的Task对象，为避免机械地将相同的参数传给每个Task的构造器</p>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            Task parent </span>= <span style="color: #0000ff;">new</span> Task(() =&gt;<span style="color: #000000;">
            {
                </span><span style="color: #0000ff;">var</span> cts = <span style="color: #0000ff;">new</span><span style="color: #000000;"> CancellationTokenSource();
                </span><span style="color: #0000ff;">var</span> tf=<span style="color: #0000ff;">new</span> TaskFactory&lt;Int32&gt;<span style="color: #000000;">(
                    cts.Token,</span><span style="color: #008000;">//</span><span style="color: #008000;">每个task都共享相同的CancellationTokenSource标记</span>
                    TaskCreationOptions.AttachedToParent, <span style="color: #008000;">//</span><span style="color: #008000;">任务都被视为父任务的子任务</span>
                    TaskContinuationOptions.ExecuteSynchronously, <span style="color: #008000;">//</span><span style="color: #008000;">TaskFactory创建的所有延续任务都以同步方式执行</span>
                    TaskScheduler.Default<span style="color: #008000;">//</span><span style="color: #008000;">使用默认的任务调度器</span>
<span style="color: #000000;">                    );

                </span><span style="color: #008000;">//</span><span style="color: #008000;">这个任务创建并启动3个子任务</span>
                <span style="color: #0000ff;">var</span> childTasks = <span style="color: #0000ff;">new</span><span style="color: #000000;">[]
                {
                    tf.StartNew(() </span>=&gt; <span style="color: #800080;">1</span><span style="color: #000000;">),
                    tf.StartNew(() </span>=&gt; <span style="color: #800080;">2</span><span style="color: #000000;">),
                    tf.StartNew(() </span>=&gt; { <span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> ArgumentNullException();})
                };


                </span><span style="color: #008000;">//</span><span style="color: #008000;">任何子任务抛出异常，则终止所有子任务</span>
                <span style="color: #0000ff;">foreach</span> (<span style="color: #0000ff;">var</span> childTask <span style="color: #0000ff;">in</span><span style="color: #000000;"> childTasks)
                {
                    childTask.ContinueWith(t </span>=&gt;<span style="color: #000000;"> cts.Cancel(), TaskContinuationOptions.OnlyOnFaulted);
                }

                </span><span style="color: #008000;">//</span><span style="color: #008000;">输出子任务值合计</span>
<span style="color: #000000;">                tf.ContinueWhenAll(childTasks,
                    </span><span style="color: #008000;">//</span><span style="color: #008000;">该子任务不受 取消 影响</span>
                    complatedTasks =&gt; complatedTasks.Where(r =&gt; !r.IsFaulted &amp;&amp; !r.IsCanceled).Sum(r =&gt;<span style="color: #000000;"> r.Result),CancellationToken.None)
                    .ContinueWith(r </span>=&gt;<span style="color: #000000;"> Console.WriteLine(r.Result), TaskContinuationOptions.ExecuteSynchronously);
            });


            </span><span style="color: #008000;">//</span><span style="color: #008000;">上个任务有异常时执行输出抛出异常的类型</span>
            parent.ContinueWith(p =&gt;<span style="color: #000000;">
            {
                StringBuilder sb </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> StringBuilder();
                </span><span style="color: #0000ff;">foreach</span> (<span style="color: #0000ff;">var</span> e <span style="color: #0000ff;">in</span><span style="color: #000000;"> p.Exception.Flatten().InnerExceptions)
                {
                    sb.Append(e.GetType().ToString() </span>+<span style="color: #000000;"> Environment.NewLine);
                }
                Console.WriteLine(sb.ToString());

            },TaskContinuationOptions.OnlyOnFaulted);


            parent.Start();
            Console.ReadLine();
        }</span></pre>
</div>
<p>&nbsp;</p>
<p><strong>8，任务调度器</strong></p>
<p>FCL提供了两个派生自TaskScheduler的类型：</p>
<p>①线程池任务调度器（默认使用）</p>
<p>②同步上下文任务调度器</p>
<p>同步上下文任务调度器提供了图形用户界面的应用程序，例如Windows窗体等。它将所有任务都调度给应用程序的GUI线程，是所有任务代码都能成功更新UI组件（按钮、菜单项等）</p>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">private</span> <span style="color: #0000ff;">void</span> Form1_Load(<span style="color: #0000ff;">object</span><span style="color: #000000;"> sender, EventArgs e)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">TaskScheduler.FromCurrentSynchronizationContext()使用同步上下文任务调度器</span>
            Task.Run(() =&gt; { label1.Text = <span style="color: #800000;">"</span><span style="color: #800000;">同步上下文任务调度器(失败)</span><span style="color: #800000;">"</span><span style="color: #000000;">; }, CancellationToken.None)
                .ContinueWith(task </span>=&gt; { label1.Text = <span style="color: #800000;">"</span><span style="color: #800000;">同步上下文任务调度器（成功）</span><span style="color: #800000;">"</span><span style="color: #000000;">; }, CancellationToken.None,
                    TaskContinuationOptions.OnlyOnFaulted, TaskScheduler.FromCurrentSynchronizationContext());
        }</span></pre>
</div>
<p>&nbsp;</p>
<p><strong>8，Parallel的静态For,ForEach,Invoke方法</strong></p>
<p>1&gt;使用Parallel的前提条件：</p>
<p>①工作项必须能并行执行</p>
<p>②避免修改共享数据的工作项</p>
<p>2&gt;Parallel的性能开销：</p>
<p>①委托对象必须分配，而针对每个工作项都要调用一次这些委托</p>
<p>②如果为处理非常快的工作项使用Parallel的方法，则会得不偿失</p>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {

            </span><span style="color: #008000;">//</span><span style="color: #008000;">最后输出Complate。线程要在所有工作完成后才继续运行。如果存在异常，则抛出AggregateException
            
            </span><span style="color: #008000;">//</span><span style="color: #008000;">使用For执行更快</span>
            Parallel.For(<span style="color: #800080;">0</span>, <span style="color: #800080;">100</span>, r =&gt;<span style="color: #000000;"> Console.WriteLine(r));

            Parallel.ForEach(</span><span style="color: #0000ff;">new</span>[] {<span style="color: #800080;">1</span>, <span style="color: #800080;">2</span>}, r =&gt;<span style="color: #000000;"> { Console.WriteLine(r); });

            Parallel.Invoke(()</span>=&gt;Method1(), () =&gt;<span style="color: #000000;"> Method2());

            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">Complate</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            Console.ReadLine();
        }</span></pre>
</div>
<p>3&gt;Parallel的静态For,ForEach,Invoke方法都提供了此参数</p>
<div class="cnblogs_code">
<pre>    
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ParallelOptions
    {
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> ParallelOptions();

        </span><span style="color: #008000;">//</span><span style="color: #008000;">允许取消操作（默认为CancellationToken.None）</span>
        <span style="color: #0000ff;">public</span> CancellationToken CancellationToken { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
        </span><span style="color: #008000;">//</span><span style="color: #008000;">允许指定要使用哪个TaskScheduler（默认为TaskScheduler.Default）</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span> MaxDegreeOfParallelism { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    }</span></pre>
</div>
<p>&nbsp;4&gt;Parallel的静态For,ForEach方法有一些重载版本允许传递3个委托</p>
<p>①任务局部初始化委托（localInit）：为参与工作的每个任务都调用一次改委托。这个委托是在任务被要求处理一个工作项之前调用的</p>
<p>②主体委托（body）：为参与工作的各个线程所处理的每一项都调用一次该委托</p>
<p>③任务局部终结委托（localFinally）：为参与工作的每一个任务都调用一次改委托。这个委托实在任务处理好派发给它的所有工作项之后调用的。即使主体委托代码引发一个未处理的异常，也会调用它</p>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {

            Console.WriteLine(DirectoryBytes(</span><span style="color: #800000;">@"</span><span style="color: #800000;">E:\web</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">*</span><span style="color: #800000;">"</span><span style="color: #000000;">, SearchOption.TopDirectoryOnly));
            
            Console.ReadLine();
        }

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">long</span> DirectoryBytes(<span style="color: #0000ff;">string</span> path, <span style="color: #0000ff;">string</span><span style="color: #000000;"> searchPattern, SearchOption searchOption)
        {
            </span><span style="color: #0000ff;">var</span> files =<span style="color: #000000;"> Directory.EnumerateFiles(path, searchPattern, searchOption);
            </span><span style="color: #0000ff;">long</span> masterTotal = <span style="color: #800080;">0</span><span style="color: #000000;">;
            ParallelLoopResult result </span>= Parallel.ForEach&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">long</span>&gt;<span style="color: #000000;">(files,
                () </span>=&gt;<span style="color: #000000;">
                {
                    </span><span style="color: #008000;">//</span><span style="color: #008000;">localInit:每个任务开始之前调用一次
                    </span><span style="color: #008000;">//</span><span style="color: #008000;">每个任务开始之前，总计值都初始化为0</span>
                    <span style="color: #0000ff;">return</span> <span style="color: #800080;">0</span><span style="color: #000000;">;
                },
                (file, loopState, index, taskLocalTotal) </span>=&gt;<span style="color: #008000;">//</span><span style="color: #008000;">taskLocalTotal接受localInit的返回值</span>
<span style="color: #000000;">                {
                    </span><span style="color: #008000;">//</span><span style="color: #008000;">body：每个工作项调用一次
                    </span><span style="color: #008000;">//</span><span style="color: #008000;">获得这个文件的大小，把它添加到这个任务的累加值上</span>
                    <span style="color: #0000ff;">long</span> fileLength = <span style="color: #800080;">0</span><span style="color: #000000;">;
                    FileStream fs </span>= <span style="color: #0000ff;">null</span><span style="color: #000000;">;
                    </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
                    {
                        fs </span>=<span style="color: #000000;"> File.OpenRead(file);
                        fileLength </span>=<span style="color: #000000;"> fs.Length;
                    }
                    </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (IOException)
                    {
                        </span><span style="color: #008000;">//</span><span style="color: #008000;">忽略拒绝访问的文件</span>
<span style="color: #000000;">                    }
                    </span><span style="color: #0000ff;">finally</span><span style="color: #000000;">
                    {
                        </span><span style="color: #0000ff;">if</span> (fs != <span style="color: #0000ff;">null</span><span style="color: #000000;">) fs.Dispose();
                    }

                    </span><span style="color: #0000ff;">return</span> taskLocalTotal +<span style="color: #000000;"> fileLength;
                },
                taskLocalTotal </span>=&gt;<span style="color: #008000;">//</span><span style="color: #008000;">taskLocalTotal接受body的返回值</span>
<span style="color: #000000;">                {
                    </span><span style="color: #008000;">//</span><span style="color: #008000;">localFinally：每个任务完成时调用一次
                    </span><span style="color: #008000;">//</span><span style="color: #008000;">将这个任务的总计值（taskLocalTotal）加到总的总计值（masterTotal）上</span>
                    Interlocked.Add(<span style="color: #0000ff;">ref</span><span style="color: #000000;"> masterTotal, taskLocalTotal);
                });
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> masterTotal;
        }
    }</span></pre>
</div>
<p>loopState：</p>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ParallelLoopState
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;">告诉循环停止处理任何跟多的工作</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Stop();
        </span><span style="color: #008000;">//</span><span style="color: #008000;">停止之后该属性为true</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">bool</span> IsStopped { <span style="color: #0000ff;">get</span><span style="color: #000000;">; }
        </span><span style="color: #008000;">//</span><span style="color: #008000;">告诉循环不再继续处理当前项之后的项</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Break();
        </span><span style="color: #008000;">//</span><span style="color: #008000;">该属性返回在处理过程中调用过Break方法的最低的项（从来没有调用过，则返回null）</span>
        <span style="color: #0000ff;">public</span> Int64? LowestBreakInteration { <span style="color: #0000ff;">get</span><span style="color: #000000;">; }
        </span><span style="color: #008000;">//</span><span style="color: #008000;">任何项造成未处理的异常，则为true</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">bool</span> IsException { <span style="color: #0000ff;">get</span><span style="color: #000000;">; }
        </span><span style="color: #008000;">//</span><span style="color: #008000;">调用过Stop、Break、取消过CancellationTokenSource,造成未处理异常。则为true</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">bool</span> ShouldExitCurrentInteration { <span style="color: #0000ff;">get</span><span style="color: #000000;">; }
    }</span></pre>
</div>
<p>ParallelLoopResult：</p>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">struct</span><span style="color: #000000;"> ParallelLoopResult
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;">如果操作提前终止，则返回false</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">bool</span> IsComplated { <span style="color: #0000ff;">get</span><span style="color: #000000;">; }
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">long</span>? LowestBreakInteration { <span style="color: #0000ff;">get</span><span style="color: #000000;">; }
    }</span></pre>
</div>
<p>IsComplated=true 循环运行完成，所有项得到了处理<br />IsComplated=false LowestBreakInteration=null 参与工作的某个线程调用了Stop方法<br />IsComplated=false LowestBreakInteration!=null参与工作的某个线程调用了Break方法</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a5"></a>五、并行语言集成查询（PLINQ）</span></strong></span></p>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        [Obsolete(</span><span style="color: #800000;">"</span><span style="color: #800000;">已经过时</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {

            </span><span style="color: #008000;">//</span><span style="color: #008000;">AsParallel将顺序查询转换成并行查询
            </span><span style="color: #008000;">//</span><span style="color: #008000;">AsSequential将并行操作转换为循序操作</span>
            <span style="color: #0000ff;">var</span> query =
                <span style="color: #0000ff;">from</span> type <span style="color: #0000ff;">in</span><span style="color: #000000;"> Assembly.GetExecutingAssembly().GetExportedTypes().AsParallel().AsSequential().AsParallel()
                </span><span style="color: #0000ff;">from</span> methed <span style="color: #0000ff;">in</span><span style="color: #000000;"> type.GetMethods()
                let obsoleteAttrType</span>=<span style="color: #0000ff;">typeof</span><span style="color: #000000;">(ObsoleteAttribute)
                </span><span style="color: #0000ff;">where</span><span style="color: #000000;"> Attribute.IsDefined(methed, obsoleteAttrType)
                </span><span style="color: #0000ff;">orderby</span><span style="color: #000000;"> type.FullName
                let obsoleteAttrObj</span>=<span style="color: #000000;">(ObsoleteAttribute)Attribute.GetCustomAttribute(methed,obsoleteAttrType)
                </span><span style="color: #0000ff;">select</span> $<span style="color: #800000;">"</span><span style="color: #800000;">Type={type.FullName};Methed={methed.Name};Message={obsoleteAttrObj.Message}</span><span style="color: #800000;">"</span><span style="color: #000000;">;

            </span><span style="color: #008000;">//</span><span style="color: #008000;">并行处理结果</span>
<span style="color: #000000;">            query.ForAll(Console.WriteLine);
            Console.ReadLine();
        }
    }</span></pre>
</div>
<p>PLINQ处理是乱序的，如果想保持顺序，则可调用ParallelEnumerable的AsOrdered方法，调用这个方法线程会组成处理数据项，然后，这些组被合并回去，同时保持顺序（会损害性能）</p>
<p>PLINQ主要是划分区块，然后对区块（不同的线程）进行聚合计算，从而达到分而治之</p>
<p>AsParallel()：将串行的代码转换为并行</p>
<p>AsOrdered()：还原集合的初始顺序</p>
<p><span style="font-size: 12px;">AsOrdered和OrderBy比较</span></p>
<p><span style="font-size: 12px;">例如集合[10,1,4,2]</span></p>
<p><span style="font-size: 12px;">AsOrdered=&gt;[10,1,4,2]</span></p>
<p><span style="font-size: 12px;">OrderBy=&gt;[1,2,4,10]</span></p>
<p>AsSequential()：将并行转换为串行</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a6"></a>六、执行定时计算限制操作</span></strong></span></p>
<p>1，构造Timer参数：</p>
<p>callback：回调方法</p>
<p>state：回调方法参数</p>
<p>dueTime：首次回调方法之前要等待多时毫秒（0为立即执行）</p>
<p>period：以后每次回调方法之前要等待多时毫秒（Timeout.Infinite线程池只调用回调方法一次）</p>
<p><span style="color: #ff0000;">使用Timer对象时，要确定一个变量在保持Timer对象的存活，否则对你的回调方法的调用就会停止</span></p>
<p>2，演示如何让一个线程池线程立即调用回调方法</p>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> Timer _timer;
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建但不启动计时器</span>
            _timer = <span style="color: #0000ff;">new</span> Timer(Status, <span style="color: #0000ff;">null</span><span style="color: #000000;">, Timeout.Infinite, Timeout.Infinite);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">立即启动一次计时器</span>
            _timer.Change(<span style="color: #800080;">0</span><span style="color: #000000;">, Timeout.Infinite);

            Console.ReadLine();//防止进程终止
        }

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Status(<span style="color: #0000ff;">object</span><span style="color: #000000;"> state)
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">进入Status方法</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">这个方法由一个线程池线程执行</span>
            Thread.Sleep(<span style="color: #800080;">1000</span>);<span style="color: #008000;">//</span><span style="color: #008000;">模拟其它工作（1秒）

            </span><span style="color: #008000;">//</span><span style="color: #008000;">返回前让Timer在2秒后再次触发一次</span>
            _timer.Change(<span style="color: #800080;">2000</span><span style="color: #000000;">, Timeout.Infinite);
            </span><span style="color: #008000;">//</span><span style="color: #008000;">这个方法返回后，线程池回归池中，等待下一个工作项</span>
<span style="color: #000000;">        }
    }</span></pre>
</div>
<p>利用Task的静态Delay方法和async和await关键字</p>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> Timer _timer;
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            Status();
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">C</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            Console.ReadLine();</span><span style="color: #008000;">//</span><span style="color: #008000;">防止进程终止

            </span><span style="color: #008000;">//</span><span style="color: #008000;">输出：
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> A C B A B A B...</span>
<span style="color: #000000;">        }

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">async</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Status()
        {
            </span><span style="color: #0000ff;">while</span> (<span style="color: #0000ff;">true</span><span style="color: #000000;">)
            {
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">A</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                </span><span style="color: #008000;">//</span><span style="color: #008000;">在循环末尾，在不阻塞线程的前提下延迟2秒</span>
                <span style="color: #0000ff;">await</span> Task.Delay(<span style="color: #800080;">2000</span>);<span style="color: #008000;">//</span><span style="color: #008000;">await 运行线程返回</span>
                Console.WriteLine(<span style="color: #800000;">"</span><span style="color: #800000;">B</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                </span><span style="color: #008000;">//</span><span style="color: #008000;">2秒之后，某个线程会在await之后介入并继续循环</span>
<span style="color: #000000;">            }
        }
    }</span></pre>
</div>
<p>&nbsp;</p>