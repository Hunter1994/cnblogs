<p><img src="https://images2018.cnblogs.com/blog/741594/201804/741594-20180412183307499-701650720.jpg" alt="" /></p>
<p>一、简单的Quartz程序</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('13ed0707-0164-43e2-a2fe-5b956cc6ef1c')"><img id="code_img_closed_13ed0707-0164-43e2-a2fe-5b956cc6ef1c" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_13ed0707-0164-43e2-a2fe-5b956cc6ef1c" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('13ed0707-0164-43e2-a2fe-5b956cc6ef1c',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_13ed0707-0164-43e2-a2fe-5b956cc6ef1c" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Impl;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Listener;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Impl.Matchers;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ConsoleApp3
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">scheduler [10 +1 都开启了，只不过都是等待状态]</span>
            <span style="color: #0000ff;">var</span> scheduler =<span style="color: #000000;"> StdSchedulerFactory.GetDefaultScheduler().Result;
            </span><span style="color: #008000;">//</span><span style="color: #008000;">[start 会让 调度线程 启动，从jobstore中获取快要执行的trigger，然后获取trigger关联的job进行执行。]</span>
<span style="color: #000000;">            scheduler.Start();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">job</span>
            <span style="color: #0000ff;">var</span> job = JobBuilder.Create&lt;JobTest&gt;<span style="color: #000000;">().Build();
            </span><span style="color: #008000;">//</span><span style="color: #008000;">trigger </span>
            <span style="color: #0000ff;">var</span> trigger = TriggerBuilder.Create().WithSimpleSchedule(x =&gt;<span style="color: #000000;"> x
                                                                        .WithIntervalInSeconds(</span><span style="color: #800080;">1</span>)<span style="color: #008000;">//</span><span style="color: #008000;">1s钟执行一次</span>
                                                                        .RepeatForever()<span style="color: #008000;">//</span><span style="color: #008000;">重复执行</span>
<span style="color: #000000;">                                                                        .Build()).Build();
            
            </span><span style="color: #008000;">//</span><span style="color: #008000;">添加监听</span>
            scheduler.ListenerManager.AddJobListener(<span style="color: #0000ff;">new</span> MyJobListener(), GroupMatcher&lt;JobKey&gt;<span style="color: #000000;">.AnyGroup());

            </span><span style="color: #008000;">//</span><span style="color: #008000;">开始调度</span>
<span style="color: #000000;">            scheduler.ScheduleJob(job, trigger);
            Console.ReadLine();
        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;">面向AOP</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyJobListener : IJobListener
        {
            </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Name =&gt; <span style="color: #800000;">"</span><span style="color: #800000;">test</span><span style="color: #800000;">"</span><span style="color: #000000;">;

            </span><span style="color: #008000;">//</span><span style="color: #008000;">job开始执行之前调用</span>
            <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task JobExecutionVetoed(IJobExecutionContext context, CancellationToken cancellationToken = <span style="color: #0000ff;">default</span><span style="color: #000000;">(CancellationToken))
            {
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">JobExecutionVetoed</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }

            </span><span style="color: #008000;">//</span><span style="color: #008000;">job每次执行之后调用</span>
            <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task JobToBeExecuted(IJobExecutionContext context, CancellationToken cancellationToken = <span style="color: #0000ff;">default</span><span style="color: #000000;">(CancellationToken))
            {
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">JobToBeExecuted</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }

            </span><span style="color: #008000;">//</span><span style="color: #008000;">job执行结束之后调用</span>
            <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task JobWasExecuted(IJobExecutionContext context, JobExecutionException jobException, CancellationToken cancellationToken = <span style="color: #0000ff;">default</span><span style="color: #000000;">(CancellationToken))
            {
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">JobWasExecuted</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }
        }
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> JobTest : IJob
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span><span style="color: #000000;"> Task Execute(IJobExecutionContext context)
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">asd</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">demo</span></div>
<p>&nbsp;</p>
<p>二、 quartz的五大构件</p>
<p>1. Scheduler [一个大容器]</p>
<p>2. job</p>
<p>3. trigger</p>
<p>4. SimpleThreadPool [最终的执行都是要委托给线程池]</p>
<p>　　10[WorkThread] + 1 [调度线程 QuartzSchedulerThread] =&gt; QuarzThread</p>
<p>　　SimpleThreadPool 默认是10个thread，是在thread上面进行的封装，不是线程池线程。。。</p>
<p>　　QuartzSchedulerThread =&gt; public override void Run()</p>
<p>5. JobStore =&gt;DbStore,RAMStore</p>
<p>　　timeTriggers 用于获取最近的trigger的。</p>
<p>&nbsp;</p>
<p>三、Job详解 【JobBuilder】</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> job = JobBuilder.Create&lt;HelloJob&gt;().Build();</pre>
</div>
<p>在JobBuilder中执行执行的Action有四种方法。。。 Create 和 OfType</p>
<p>1. Create&lt;T&gt;</p>
<p>写代码方便。。</p>
<p>2. Type类型</p>
<p>后期绑定。。。。</p>
<p>Action不是来自解决方案的。。。 可能你要执行的Action来自于其他的团队，对方所做的事情就是实现一下IJob接口就可以了。。。</p>
<p>我们拿到这个Dll，做反射，直接把job丢给scheduler。。。。</p>
<p>3，StoreDurably方法</p>
<p>设置job是否持久化</p>
<p>默认情况下： 一旦job没有相对应的trigger，那么这个job会被删除。。。</p>
<p>如果一对一的情况下，trigger删除，job也会被删除。。。</p>
<p>所有的Job，Trigger 都是在RAMJobStore里面。。。</p>
<p>4，UsingJobData / SetJobData 都是给一个Job添加附加信息。。。</p>
<p>JobDataMap 就是一个字典，用于添加多个信息。。</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('ec9cfaae-d8f3-47dd-a471-d9f0dc07f6be')"><img id="code_img_closed_ec9cfaae-d8f3-47dd-a471-d9f0dc07f6be" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_ec9cfaae-d8f3-47dd-a471-d9f0dc07f6be" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('ec9cfaae-d8f3-47dd-a471-d9f0dc07f6be',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_ec9cfaae-d8f3-47dd-a471-d9f0dc07f6be" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Impl;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Listener;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Impl.Matchers;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ConsoleApp3
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">scheduler [10 +1 都开启了，只不过都是等待状态]</span>
            <span style="color: #0000ff;">var</span> scheduler =<span style="color: #000000;"> StdSchedulerFactory.GetDefaultScheduler().Result;
            </span><span style="color: #008000;">//</span><span style="color: #008000;">[start 会让 调度线程 启动，从jobstore中获取快要执行的trigger，然后获取trigger关联的job进行执行。]</span>
<span style="color: #000000;">            scheduler.Start();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">job</span>
            <span style="color: #0000ff;">var</span> job = JobBuilder.Create&lt;JobTest&gt;<span style="color: #000000;">()
                                                .StoreDurably(</span><span style="color: #0000ff;">true</span><span style="color: #000000;">)
                                                .UsingJobData(</span><span style="color: #800000;">"</span><span style="color: #800000;">username</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">hunter</span><span style="color: #800000;">"</span>)<span style="color: #008000;">//</span><span style="color: #008000;">都是给一个Job添加附加信息</span>
<span style="color: #000000;">                                                .Build();
            </span><span style="color: #008000;">//</span><span style="color: #008000;">trigger </span>
            <span style="color: #0000ff;">var</span> trigger = TriggerBuilder.Create().WithSimpleSchedule(x =&gt;<span style="color: #000000;"> x
                                                                        .WithIntervalInSeconds(</span><span style="color: #800080;">1</span>)<span style="color: #008000;">//</span><span style="color: #008000;">1s钟执行一次</span>
                                                                        .RepeatForever()<span style="color: #008000;">//</span><span style="color: #008000;">重复执行</span>
<span style="color: #000000;">                                                                        .Build()).Build();
            
            </span><span style="color: #008000;">//</span><span style="color: #008000;">添加监听</span>
            scheduler.ListenerManager.AddJobListener(<span style="color: #0000ff;">new</span> MyJobListener(), GroupMatcher&lt;JobKey&gt;<span style="color: #000000;">.AnyGroup());

            </span><span style="color: #008000;">//</span><span style="color: #008000;">开始调度</span>
<span style="color: #000000;">            scheduler.ScheduleJob(job, trigger);
            Console.ReadLine();
        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;">面向AOP</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyJobListener : IJobListener
        {
            </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Name =&gt; <span style="color: #800000;">"</span><span style="color: #800000;">test</span><span style="color: #800000;">"</span><span style="color: #000000;">;

            </span><span style="color: #008000;">//</span><span style="color: #008000;">job开始执行之前调用</span>
            <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task JobExecutionVetoed(IJobExecutionContext context, CancellationToken cancellationToken = <span style="color: #0000ff;">default</span><span style="color: #000000;">(CancellationToken))
            {
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">JobExecutionVetoed</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }

            </span><span style="color: #008000;">//</span><span style="color: #008000;">job每次执行之后调用</span>
            <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task JobToBeExecuted(IJobExecutionContext context, CancellationToken cancellationToken = <span style="color: #0000ff;">default</span><span style="color: #000000;">(CancellationToken))
            {
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">JobToBeExecuted</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }

            </span><span style="color: #008000;">//</span><span style="color: #008000;">job执行结束之后调用</span>
            <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task JobWasExecuted(IJobExecutionContext context, JobExecutionException jobException, CancellationToken cancellationToken = <span style="color: #0000ff;">default</span><span style="color: #000000;">(CancellationToken))
            {
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">JobWasExecuted</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }
        }
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> JobTest : IJob
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span><span style="color: #000000;"> Task Execute(IJobExecutionContext context)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">获取附加信息</span>
            Console.WriteLine(context.MergedJobDataMap[<span style="color: #800000;">"</span><span style="color: #800000;">username</span><span style="color: #800000;">"</span><span style="color: #000000;">]);
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">demo</span></div>
<p>&nbsp;5，WithIdentity： &nbsp;如果没有制定，那么系统会给一个Guid的标识</p>
<div class="cnblogs_code">
<pre>            <span style="color: #0000ff;">if</span> (key == <span style="color: #0000ff;">null</span><span style="color: #000000;">)
            {
                key </span>= <span style="color: #0000ff;">new</span> JobKey(Guid.NewGuid().ToString(), <span style="color: #0000ff;">null</span><span style="color: #000000;">);
            }        </span></pre>
</div>
<p>四、TriggerBuilder</p>
<p>1. StartAt,EndAt，StartNow Trigger触发的起始时间和结束时间&nbsp;</p>
<p>DateTimeOffset有时区概念，DateTime没有时区的概念</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('35a2c4ce-7b70-40e5-81d1-27f87069d621')"><img id="code_img_closed_35a2c4ce-7b70-40e5-81d1-27f87069d621" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_35a2c4ce-7b70-40e5-81d1-27f87069d621" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('35a2c4ce-7b70-40e5-81d1-27f87069d621',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_35a2c4ce-7b70-40e5-81d1-27f87069d621" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Impl;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Listener;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Impl.Matchers;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ConsoleApp3
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">scheduler [10 +1 都开启了，只不过都是等待状态]</span>
            <span style="color: #0000ff;">var</span> scheduler =<span style="color: #000000;"> StdSchedulerFactory.GetDefaultScheduler().Result;
            </span><span style="color: #008000;">//</span><span style="color: #008000;">[start 会让 调度线程 启动，从jobstore中获取快要执行的trigger，然后获取trigger关联的job进行执行。]</span>
<span style="color: #000000;">            scheduler.Start();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">job</span>
            <span style="color: #0000ff;">var</span> job = JobBuilder.Create&lt;JobTest&gt;<span style="color: #000000;">()
                                                .StoreDurably(</span><span style="color: #0000ff;">true</span><span style="color: #000000;">)
                                                .UsingJobData(</span><span style="color: #800000;">"</span><span style="color: #800000;">username</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">hunter</span><span style="color: #800000;">"</span>)<span style="color: #008000;">//</span><span style="color: #008000;">都是给一个Job添加附加信息</span>
<span style="color: #000000;">                                                .Build();

            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">开始</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            </span><span style="color: #008000;">//</span><span style="color: #008000;">trigger </span>
            <span style="color: #0000ff;">var</span> trigger =<span style="color: #000000;"> TriggerBuilder.Create()
                                                .StartAt(DateTimeOffset.Now.AddSeconds(</span><span style="color: #800080;">1</span>))<span style="color: #008000;">//</span><span style="color: #008000;">开始执行时间</span>
                                                .EndAt(DateTimeOffset.Now.AddSeconds(<span style="color: #800080;">5</span>))<span style="color: #008000;">//</span><span style="color: #008000;">执行结束时间</span>
                                                .WithSimpleSchedule(x =&gt;<span style="color: #000000;"> x
                                                                        .WithIntervalInSeconds(</span><span style="color: #800080;">1</span>)<span style="color: #008000;">//</span><span style="color: #008000;">1s钟执行一次</span>
                                                                        .RepeatForever()<span style="color: #008000;">//</span><span style="color: #008000;">重复执行</span>
<span style="color: #000000;">                                                                        .Build()).Build();
            
            </span><span style="color: #008000;">//</span><span style="color: #008000;">添加监听</span>
            scheduler.ListenerManager.AddJobListener(<span style="color: #0000ff;">new</span> MyJobListener(), GroupMatcher&lt;JobKey&gt;<span style="color: #000000;">.AnyGroup());

            </span><span style="color: #008000;">//</span><span style="color: #008000;">开始调度</span>
<span style="color: #000000;">            scheduler.ScheduleJob(job, trigger);
            Console.ReadLine();
        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;">面向AOP</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyJobListener : IJobListener
        {
            </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Name =&gt; <span style="color: #800000;">"</span><span style="color: #800000;">test</span><span style="color: #800000;">"</span><span style="color: #000000;">;

            </span><span style="color: #008000;">//</span><span style="color: #008000;">job开始执行之前调用</span>
            <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task JobExecutionVetoed(IJobExecutionContext context, CancellationToken cancellationToken = <span style="color: #0000ff;">default</span><span style="color: #000000;">(CancellationToken))
            {
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">JobExecutionVetoed</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }

            </span><span style="color: #008000;">//</span><span style="color: #008000;">job每次执行之后调用</span>
            <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task JobToBeExecuted(IJobExecutionContext context, CancellationToken cancellationToken = <span style="color: #0000ff;">default</span><span style="color: #000000;">(CancellationToken))
            {
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">JobToBeExecuted</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }

            </span><span style="color: #008000;">//</span><span style="color: #008000;">job执行结束之后调用</span>
            <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task JobWasExecuted(IJobExecutionContext context, JobExecutionException jobException, CancellationToken cancellationToken = <span style="color: #0000ff;">default</span><span style="color: #000000;">(CancellationToken))
            {
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">JobWasExecuted</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }
        }
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> JobTest : IJob
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span><span style="color: #000000;"> Task Execute(IJobExecutionContext context)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">获取附加信息</span>
            Console.WriteLine(context.MergedJobDataMap[<span style="color: #800000;">"</span><span style="color: #800000;">username</span><span style="color: #800000;">"</span><span style="color: #000000;">]);
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">demo</span></div>
<p>&nbsp;</p>
<p>2，其他一些方法</p>
<p> .ForJob(job)//在定义Trigger的时候，就可以将对应关系做起来<br />                                                .UsingJobData("aa","abc")//给Job添加附加信息<br />                                                .WithPriority(1)//默认优先级【5】(优先级数字越大，优先级越高)</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('4d29422c-3052-4acd-813d-6727be98d107')"><img id="code_img_closed_4d29422c-3052-4acd-813d-6727be98d107" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_4d29422c-3052-4acd-813d-6727be98d107" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('4d29422c-3052-4acd-813d-6727be98d107',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_4d29422c-3052-4acd-813d-6727be98d107" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Impl;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Listener;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Impl.Matchers;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ConsoleApp3
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">scheduler [10 +1 都开启了，只不过都是等待状态]</span>
            <span style="color: #0000ff;">var</span> scheduler =<span style="color: #000000;"> StdSchedulerFactory.GetDefaultScheduler().Result;
            </span><span style="color: #008000;">//</span><span style="color: #008000;">[start 会让 调度线程 启动，从jobstore中获取快要执行的trigger，然后获取trigger关联的job进行执行。]</span>
<span style="color: #000000;">            scheduler.Start();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">job</span>
            <span style="color: #0000ff;">var</span> job = JobBuilder.Create&lt;JobTest&gt;<span style="color: #000000;">()
                                                .StoreDurably(</span><span style="color: #0000ff;">true</span><span style="color: #000000;">)
                                                .UsingJobData(</span><span style="color: #800000;">"</span><span style="color: #800000;">username</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">hunter</span><span style="color: #800000;">"</span>)<span style="color: #008000;">//</span><span style="color: #008000;">都是给一个Job添加附加信息</span>
<span style="color: #000000;">                                                .Build();

            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">开始</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            </span><span style="color: #008000;">//</span><span style="color: #008000;">trigger </span>
            <span style="color: #0000ff;">var</span> trigger =<span style="color: #000000;"> TriggerBuilder.Create()
                                                .StartAt(DateTimeOffset.Now.AddSeconds(</span><span style="color: #800080;">1</span>))<span style="color: #008000;">//</span><span style="color: #008000;">开始执行时间</span>
                                                .EndAt(DateTimeOffset.Now.AddSeconds(<span style="color: #800080;">5</span>))<span style="color: #008000;">//</span><span style="color: #008000;">执行结束时间</span>
                                                .ForJob(job)<span style="color: #008000;">//</span><span style="color: #008000;">在定义Trigger的时候，就可以将对应关系做起来</span>
                                                .UsingJobData(<span style="color: #800000;">"</span><span style="color: #800000;">aa</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">abc</span><span style="color: #800000;">"</span>)<span style="color: #008000;">//</span><span style="color: #008000;">给Job添加附加信息</span>
                                                .WithPriority(<span style="color: #800080;">1</span>)<span style="color: #008000;">//</span><span style="color: #008000;">默认优先级【5】(优先级数字越大，优先级越高)</span>
                                                .WithSimpleSchedule(x =&gt;<span style="color: #000000;"> x
                                                                        .WithIntervalInSeconds(</span><span style="color: #800080;">1</span>)<span style="color: #008000;">//</span><span style="color: #008000;">1s钟执行一次</span>
                                                                        .RepeatForever()<span style="color: #008000;">//</span><span style="color: #008000;">重复执行</span>
<span style="color: #000000;">                                                                        .Build()).Build();
            
            </span><span style="color: #008000;">//</span><span style="color: #008000;">添加监听</span>
            scheduler.ListenerManager.AddJobListener(<span style="color: #0000ff;">new</span> MyJobListener(), GroupMatcher&lt;JobKey&gt;<span style="color: #000000;">.AnyGroup());

            </span><span style="color: #008000;">//</span><span style="color: #008000;">开始调度</span>
<span style="color: #000000;">            scheduler.ScheduleJob(job, trigger);
            Console.ReadLine();
        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;">面向AOP</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyJobListener : IJobListener
        {
            </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Name =&gt; <span style="color: #800000;">"</span><span style="color: #800000;">test</span><span style="color: #800000;">"</span><span style="color: #000000;">;

            </span><span style="color: #008000;">//</span><span style="color: #008000;">job开始执行之前调用</span>
            <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task JobExecutionVetoed(IJobExecutionContext context, CancellationToken cancellationToken = <span style="color: #0000ff;">default</span><span style="color: #000000;">(CancellationToken))
            {
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">JobExecutionVetoed</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }

            </span><span style="color: #008000;">//</span><span style="color: #008000;">job每次执行之后调用</span>
            <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task JobToBeExecuted(IJobExecutionContext context, CancellationToken cancellationToken = <span style="color: #0000ff;">default</span><span style="color: #000000;">(CancellationToken))
            {
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">JobToBeExecuted</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }

            </span><span style="color: #008000;">//</span><span style="color: #008000;">job执行结束之后调用</span>
            <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task JobWasExecuted(IJobExecutionContext context, JobExecutionException jobException, CancellationToken cancellationToken = <span style="color: #0000ff;">default</span><span style="color: #000000;">(CancellationToken))
            {
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">JobWasExecuted</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }
        }
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> JobTest : IJob
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span><span style="color: #000000;"> Task Execute(IJobExecutionContext context)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">获取附加信息</span>
            Console.WriteLine(context.MergedJobDataMap[<span style="color: #800000;">"</span><span style="color: #800000;">aa</span><span style="color: #800000;">"</span><span style="color: #000000;">]);
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">demo</span></div>
<p>&nbsp;</p>
<p>五、四大trigger调度器</p>
<p>1，Simplescheduler<br />特点：只能在时分秒上做轮询</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">RepeatForever() 指定触发器将无限重复
WithInterval(TimeSpan timeSpan) 指定重复间隔（以毫秒为单位）
WithIntervalInHours(</span><span style="color: #0000ff;">int</span><span style="color: #000000;"> hours) 指定重复间隔（以小时为单位）
WithIntervalInMinutes(</span><span style="color: #0000ff;">int</span><span style="color: #000000;"> minutes) 指定重复间隔（以分钟为单位）
WithIntervalInSeconds(</span><span style="color: #0000ff;">int</span><span style="color: #000000;"> seconds) 以秒为单位指定重复间隔
WithRepeatCount(</span><span style="color: #0000ff;">int</span> repeatCount) 重复执行次数（repeatCount+<span style="color: #800080;">1</span>）</pre>
</div>
<div class="cnblogs_code" onclick="cnblogs_code_show('a4b9a661-3ad4-4971-b544-29ade7cd027f')"><img id="code_img_closed_a4b9a661-3ad4-4971-b544-29ade7cd027f" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_a4b9a661-3ad4-4971-b544-29ade7cd027f" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('a4b9a661-3ad4-4971-b544-29ade7cd027f',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_a4b9a661-3ad4-4971-b544-29ade7cd027f" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Impl;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Listener;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Impl.Matchers;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ConsoleApp3
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">scheduler [10 +1 都开启了，只不过都是等待状态]</span>
            <span style="color: #0000ff;">var</span> scheduler =<span style="color: #000000;"> StdSchedulerFactory.GetDefaultScheduler().Result;
            </span><span style="color: #008000;">//</span><span style="color: #008000;">[start 会让 调度线程 启动，从jobstore中获取快要执行的trigger，然后获取trigger关联的job进行执行。]</span>
<span style="color: #000000;">            scheduler.Start();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">job</span>
            <span style="color: #0000ff;">var</span> job = JobBuilder.Create&lt;JobTest&gt;<span style="color: #000000;">().Build();

            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">开始</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            </span><span style="color: #008000;">//</span><span style="color: #008000;">trigger </span>
            <span style="color: #0000ff;">var</span> trigger = TriggerBuilder.Create().WithSimpleSchedule(x =&gt;<span style="color: #000000;"> x
                                                                        .WithIntervalInSeconds(</span><span style="color: #800080;">1</span><span style="color: #000000;">)
                                                                        .RepeatForever()
                                                                        .Build()).Build();
            </span><span style="color: #008000;">//</span><span style="color: #008000;">开始调度</span>
<span style="color: #000000;">            scheduler.ScheduleJob(job, trigger);
            Console.ReadLine();
        }
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> JobTest : IJob
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">int</span> index = <span style="color: #800080;">0</span><span style="color: #000000;">;
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span><span style="color: #000000;"> Task Execute(IJobExecutionContext context)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">记录当前时间，记录&ldquo;scheduler&rdquo;调度时间 ，记录 下一次触发时间</span>
            Console.WriteLine(<span style="color: #800000;">"</span><span style="color: #800000;">index={0}, current={1},schedulertime={2},nexttime={3}</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                                                                        index</span>++<span style="color: #000000;">, DateTime.Now,
                                                                        context.ScheduledFireTimeUtc</span>?<span style="color: #000000;">.LocalDateTime,
                                                                        context.NextFireTimeUtc</span>?<span style="color: #000000;">.LocalDateTime);
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">demo</span></div>
<p>&nbsp;</p>
<p>2，&nbsp;CalendarIntervalSchedule</p>
<p>特点：和日历相关的轮询（1天执行一次，一周执行一次，一个月执行一次，一年执行一次）</p>
<div class="cnblogs_code">
<pre>WithInterval(<span style="color: #0000ff;">int</span><span style="color: #000000;"> interval, IntervalUnit unit) 指定重复间隔
WithIntervalInDays(</span><span style="color: #0000ff;">int</span><span style="color: #000000;"> intervalInDays) 指定重复间隔（按天）
WithIntervalInHours(</span><span style="color: #0000ff;">int</span><span style="color: #000000;"> intervalInHours) 指定重复间隔（按小时）
WithIntervalInMinutes(</span><span style="color: #0000ff;">int</span><span style="color: #000000;"> intervalInMinutes) 指定重复间隔（按分钟）
WithIntervalInMonths(</span><span style="color: #0000ff;">int</span><span style="color: #000000;"> intervalInMonths) 指定重复间隔（按月）
WithIntervalInSeconds(</span><span style="color: #0000ff;">int</span><span style="color: #000000;"> intervalInSeconds) 指定重复间隔（按秒）
WithIntervalInWeeks(</span><span style="color: #0000ff;">int</span><span style="color: #000000;"> intervalInWeeks) 指定重复间隔（按星期）
WithIntervalInYears(</span><span style="color: #0000ff;">int</span> intervalInYears) 指定重复间隔（按年）</pre>
</div>
<div class="cnblogs_code" onclick="cnblogs_code_show('413bee8c-34ab-43e3-88f7-9ebd66913812')"><img id="code_img_closed_413bee8c-34ab-43e3-88f7-9ebd66913812" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_413bee8c-34ab-43e3-88f7-9ebd66913812" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('413bee8c-34ab-43e3-88f7-9ebd66913812',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_413bee8c-34ab-43e3-88f7-9ebd66913812" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Impl;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Listener;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Impl.Matchers;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ConsoleApp3
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">scheduler [10 +1 都开启了，只不过都是等待状态]</span>
            <span style="color: #0000ff;">var</span> scheduler =<span style="color: #000000;"> StdSchedulerFactory.GetDefaultScheduler().Result;
            </span><span style="color: #008000;">//</span><span style="color: #008000;">[start 会让 调度线程 启动，从jobstore中获取快要执行的trigger，然后获取trigger关联的job进行执行。]</span>
<span style="color: #000000;">            scheduler.Start();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">job</span>
            <span style="color: #0000ff;">var</span> job = JobBuilder.Create&lt;JobTest&gt;<span style="color: #000000;">().Build();

            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">开始</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            </span><span style="color: #008000;">//</span><span style="color: #008000;">trigger </span>
            <span style="color: #0000ff;">var</span> trigger = TriggerBuilder.Create().WithCalendarIntervalSchedule(x =&gt;<span style="color: #000000;"> x
                                                                        .WithIntervalInWeeks(</span><span style="color: #800080;">2</span>)<span style="color: #008000;">//</span><span style="color: #008000;">每两周执行一次</span>
<span style="color: #000000;">                                                                        .Build()).Build();
            </span><span style="color: #008000;">//</span><span style="color: #008000;">开始调度</span>
<span style="color: #000000;">            scheduler.ScheduleJob(job, trigger);
            Console.ReadLine();
        }
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> JobTest : IJob
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">int</span> index = <span style="color: #800080;">0</span><span style="color: #000000;">;
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span><span style="color: #000000;"> Task Execute(IJobExecutionContext context)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">记录当前时间，记录&ldquo;scheduler&rdquo;调度时间 ，记录 下一次触发时间</span>
            Console.WriteLine(<span style="color: #800000;">"</span><span style="color: #800000;">index={0}, current={1},schedulertime={2},nexttime={3}</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                                                                        index</span>++<span style="color: #000000;">, DateTime.Now,
                                                                        context.ScheduledFireTimeUtc</span>?<span style="color: #000000;">.LocalDateTime,
                                                                        context.NextFireTimeUtc</span>?<span style="color: #000000;">.LocalDateTime);
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">每两周执行一次</span></div>
<p>&nbsp;</p>
<p>3，DailyTimeIntervalScheduleBuilder</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">OnMondayThroughFriday() 周一至周五执行
OnSaturdayAndSunday() 周六和周日执行<br />OnEveryDay() 一周所有日子
WithInterval(</span><span style="color: #0000ff;">int</span><span style="color: #000000;"> interval, IntervalUnit unit) 指定要生成的触发器的时间单位和时间间隔。
WithIntervalInHours(</span><span style="color: #0000ff;">int</span><span style="color: #000000;"> intervalInHours) 指定重复间隔（按天）
WithIntervalInMinutes(</span><span style="color: #0000ff;">int</span><span style="color: #000000;"> intervalInMinutes) 指定重复间隔（按分钟）
WithIntervalInSeconds(</span><span style="color: #0000ff;">int</span><span style="color: #000000;"> intervalInSeconds) 指定重复间隔（按秒）
StartingDailyAt(TimeOfDay.HourAndMinuteOfDay(</span><span style="color: #800080;">8</span>, <span style="color: #800080;">00</span><span style="color: #000000;">) 开始执行时间
EndingDailyAt(TimeOfDay.HourAndMinuteOfDay(</span><span style="color: #800080;">20</span>, <span style="color: #800080;">00</span>)  结束时间</pre>
</div>
<p>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('2039384d-7d13-4936-946b-b50543ce4d09')"><img id="code_img_closed_2039384d-7d13-4936-946b-b50543ce4d09" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_2039384d-7d13-4936-946b-b50543ce4d09" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('2039384d-7d13-4936-946b-b50543ce4d09',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_2039384d-7d13-4936-946b-b50543ce4d09" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Impl;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Listener;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Impl.Matchers;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ConsoleApp3
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">scheduler [10 +1 都开启了，只不过都是等待状态]</span>
            <span style="color: #0000ff;">var</span> scheduler =<span style="color: #000000;"> StdSchedulerFactory.GetDefaultScheduler().Result;
            </span><span style="color: #008000;">//</span><span style="color: #008000;">[start 会让 调度线程 启动，从jobstore中获取快要执行的trigger，然后获取trigger关联的job进行执行。]</span>
<span style="color: #000000;">            scheduler.Start();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">job</span>
            <span style="color: #0000ff;">var</span> job = JobBuilder.Create&lt;JobTest&gt;<span style="color: #000000;">().Build();

            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">开始</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">30分钟检测一次，8点-20点
            </span><span style="color: #008000;">//</span><span style="color: #008000;">trigger </span>
            <span style="color: #0000ff;">var</span> trigger = TriggerBuilder.Create().WithDailyTimeIntervalSchedule(x =&gt;<span style="color: #000000;"> x
                                                            .OnEveryDay()</span><span style="color: #008000;">//</span><span style="color: #008000;">没天执行</span>
                                                            .StartingDailyAt(TimeOfDay.HourAndMinuteOfDay(<span style="color: #800080;">8</span>,<span style="color: #800080;">0</span>))<span style="color: #008000;">//</span><span style="color: #008000;">开始执行时间</span>
                                                            .EndingDailyAt(TimeOfDay.HourAndMinuteOfDay(<span style="color: #800080;">20</span>,<span style="color: #800080;">0</span>))<span style="color: #008000;">//</span><span style="color: #008000;">结束执行时间</span>
                                                            .WithIntervalInMinutes(<span style="color: #800080;">30</span>)<span style="color: #008000;">//</span><span style="color: #008000;">不管什么时候执行的此程序，都是每30分钟整点执行一次（例如8:30,13:30）</span>
<span style="color: #000000;">                                                            .Build()).Build();



            </span><span style="color: #008000;">//</span><span style="color: #008000;">开始调度</span>
<span style="color: #000000;">            scheduler.ScheduleJob(job, trigger);
            Console.ReadLine();
        }
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> JobTest : IJob
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">int</span> index = <span style="color: #800080;">0</span><span style="color: #000000;">;
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span><span style="color: #000000;"> Task Execute(IJobExecutionContext context)
        {
            index</span>++<span style="color: #000000;">;

            </span><span style="color: #008000;">//</span><span style="color: #008000;">记录当前时间，记录&ldquo;scheduler&rdquo;调度时间 ，记录 下一次触发时间</span>
            Console.WriteLine(<span style="color: #800000;">"</span><span style="color: #800000;">index={0}, current={1},schedulertime={2},nexttime={3}</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                                                                        index, DateTime.Now,
                                                                        context.ScheduledFireTimeUtc</span>?<span style="color: #000000;">.LocalDateTime,
                                                                        context.NextFireTimeUtc</span>?<span style="color: #000000;">.LocalDateTime);
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">8点-20点，30分钟检测一次</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('e3ae6c87-7c43-4a64-bbdf-9e2559837003')"><img id="code_img_closed_e3ae6c87-7c43-4a64-bbdf-9e2559837003" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_e3ae6c87-7c43-4a64-bbdf-9e2559837003" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('e3ae6c87-7c43-4a64-bbdf-9e2559837003',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_e3ae6c87-7c43-4a64-bbdf-9e2559837003" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Impl;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Listener;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Impl.Matchers;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ConsoleApp3
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">scheduler [10 +1 都开启了，只不过都是等待状态]</span>
            <span style="color: #0000ff;">var</span> scheduler =<span style="color: #000000;"> StdSchedulerFactory.GetDefaultScheduler().Result;
            </span><span style="color: #008000;">//</span><span style="color: #008000;">[start 会让 调度线程 启动，从jobstore中获取快要执行的trigger，然后获取trigger关联的job进行执行。]</span>
<span style="color: #000000;">            scheduler.Start();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">job</span>
            <span style="color: #0000ff;">var</span> job = JobBuilder.Create&lt;JobTest&gt;<span style="color: #000000;">().Build();

            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">开始</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">每天凌晨2点跑一次
            </span><span style="color: #008000;">//</span><span style="color: #008000;">trigger </span>
            <span style="color: #0000ff;">var</span> trigger = TriggerBuilder.Create().WithDailyTimeIntervalSchedule(x =&gt;<span style="color: #000000;"> x
                                                            .OnEveryDay()</span><span style="color: #008000;">//</span><span style="color: #008000;">没天执行</span>
                                                            .StartingDailyAt(TimeOfDay.HourAndMinuteOfDay(<span style="color: #800080;">2</span>,<span style="color: #800080;">0</span>))<span style="color: #008000;">//</span><span style="color: #008000;">开始执行时间</span>
                                                            .EndingDailyAt(TimeOfDay.HourAndMinuteOfDay(<span style="color: #800080;">2</span>,<span style="color: #800080;">1</span>))<span style="color: #008000;">//</span><span style="color: #008000;">结束执行时间</span>
                                                            .WithIntervalInMinutes(<span style="color: #800080;">30</span>)<span style="color: #008000;">//</span><span style="color: #008000;">巧妙设计，是程序每天只执行一次</span>
<span style="color: #000000;">                                                            .Build()).Build();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">注意做一个问题：在测试的时候先调整好计算机时间，在run此程序
            </span><span style="color: #008000;">//</span><span style="color: #008000;">如果先run程序，在调整时间，会有问题

            </span><span style="color: #008000;">//</span><span style="color: #008000;">开始调度</span>
<span style="color: #000000;">            scheduler.ScheduleJob(job, trigger);
            Console.ReadLine();
        }
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> JobTest : IJob
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">int</span> index = <span style="color: #800080;">0</span><span style="color: #000000;">;
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span><span style="color: #000000;"> Task Execute(IJobExecutionContext context)
        {
            index</span>++<span style="color: #000000;">;

            </span><span style="color: #008000;">//</span><span style="color: #008000;">记录当前时间，记录&ldquo;scheduler&rdquo;调度时间 ，记录 下一次触发时间</span>
            Console.WriteLine(<span style="color: #800000;">"</span><span style="color: #800000;">index={0}, current={1},schedulertime={2},nexttime={3}</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                                                                        index, DateTime.Now,
                                                                        context.ScheduledFireTimeUtc</span>?<span style="color: #000000;">.LocalDateTime,
                                                                        context.NextFireTimeUtc</span>?<span style="color: #000000;">.LocalDateTime);
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">每天凌晨2点跑一次</span></div>
<p>&nbsp;</p>
<p>5，WithCronSchedule</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('35e861dd-bfeb-4923-8aba-19c172859abb')"><img id="code_img_closed_35e861dd-bfeb-4923-8aba-19c172859abb" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_35e861dd-bfeb-4923-8aba-19c172859abb" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('35e861dd-bfeb-4923-8aba-19c172859abb',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_35e861dd-bfeb-4923-8aba-19c172859abb" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Impl;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Listener;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Impl.Matchers;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ConsoleApp3
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">scheduler [10 +1 都开启了，只不过都是等待状态]</span>
            <span style="color: #0000ff;">var</span> scheduler =<span style="color: #000000;"> StdSchedulerFactory.GetDefaultScheduler().Result;
            </span><span style="color: #008000;">//</span><span style="color: #008000;">[start 会让 调度线程 启动，从jobstore中获取快要执行的trigger，然后获取trigger关联的job进行执行。]</span>
<span style="color: #000000;">            scheduler.Start();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">job</span>
            <span style="color: #0000ff;">var</span> job = JobBuilder.Create&lt;JobTest&gt;<span style="color: #000000;">().Build();

            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">开始</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">trigger </span>
            <span style="color: #0000ff;">var</span> trigger = TriggerBuilder.Create().WithCronSchedule(<span style="color: #800000;">"</span><span style="color: #800000;">* * * ? * MON</span><span style="color: #800000;">"</span><span style="color: #000000;">).Build();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">注意做一个问题：在测试的时候先调整好计算机时间，在run此程序
            </span><span style="color: #008000;">//</span><span style="color: #008000;">如果先run程序，在调整时间，会有问题

            </span><span style="color: #008000;">//</span><span style="color: #008000;">开始调度</span>
<span style="color: #000000;">            scheduler.ScheduleJob(job, trigger);
            Console.ReadLine();
        }
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> JobTest : IJob
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">int</span> index = <span style="color: #800080;">0</span><span style="color: #000000;">;
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span><span style="color: #000000;"> Task Execute(IJobExecutionContext context)
        {
            index</span>++<span style="color: #000000;">;

            </span><span style="color: #008000;">//</span><span style="color: #008000;">记录当前时间，记录&ldquo;scheduler&rdquo;调度时间 ，记录 下一次触发时间</span>
            Console.WriteLine(<span style="color: #800000;">"</span><span style="color: #800000;">index={0}, current={1},schedulertime={2},nexttime={3}</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                                                                        index, DateTime.Now,
                                                                        context.ScheduledFireTimeUtc</span>?<span style="color: #000000;">.LocalDateTime,
                                                                        context.NextFireTimeUtc</span>?<span style="color: #000000;">.LocalDateTime);
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">demo</span></div>
<h2><span style="font-size: 14px;">Cron表达式</span></h2>
<p>quartz中的cron表达式和Linux下的很类似，比如&nbsp;"/5 * * ? * * *" &nbsp;这样的7位表达式，最后一位年非必选。</p>
<p>表达式从左到右，依此是秒、分、时、月第几天、月、周几、年。下面表格是要遵守的规范：</p>
<table border="1" align="left">
<thead>
<tr><th><strong>字段名</strong></th><th>允许的值</th><th>允许的特殊字符</th></tr>
</thead>
<tbody>
<tr>
<td>Seconds</td>
<td>0-59</td>
<td>, - * /</td>
</tr>
<tr>
<td>Minutes</td>
<td>0-59</td>
<td>, - * /</td>
</tr>
<tr>
<td>Hours</td>
<td>0-23</td>
<td>, - * /</td>
</tr>
<tr>
<td>Day of month</td>
<td>1-31</td>
<td>, - * ? / L W</td>
</tr>
<tr>
<td>Month</td>
<td>1-12 or JAN-DEC</td>
<td>, - * /</td>
</tr>
<tr>
<td>Day of week</td>
<td>1-7 or SUN-SAT</td>
<td>, - * ? / L #</td>
</tr>
<tr>
<td>Year</td>
<td>空, 1970-2099</td>
<td>, - * /</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>星期一 MON <br />星期二 TUE <br />星期三 WED <br />星期四 THU <br />星期五 FRI <br />星期六 SAT <br />星期天 SUN</p>
<table style="height: 254px; width: 654px;" border="1" align="left">
<tbody>
<tr>
<td>特殊字符</td>
<td>解释</td>
















</tr>
<tr>
<td>,</td>
<td>或的意思。例：分钟位 5,10 &nbsp;即第5分钟或10分都触发。&nbsp;</td>
















</tr>
<tr>
<td>/</td>
<td>a/b。 a：代表起始时间，b频率时间。 例； 分钟位 &nbsp;3/5， &nbsp;从第三分钟开始，每5分钟执行一次。</td>
















</tr>
<tr>
<td>*</td>
<td>频率。 即每一次波动。 &nbsp; &nbsp;例；分钟位 * &nbsp;即表示每分钟&nbsp;</td>
















</tr>
<tr>
<td>-</td>
<td>区间。 &nbsp;例： 分钟位 &nbsp; 5-10 即5到10分期间。&nbsp;</td>
















</tr>
<tr>
<td>?</td>
<td>任意值&nbsp;。 &nbsp; 即每一次波动。只能用在DayofMonth和DayofWeek，二者冲突。指定一个另一个一个要用?</td>
















</tr>
<tr>
<td>L</td>
<td>表示最后。 只能用在DayofMonth和DayofWeek，4L即最后一个星期三</td>
















</tr>
<tr>
<td>W</td>
<td>工作日。 &nbsp;表示最后。 只能用在DayofWeek</td>
















</tr>
<tr>
<td>#</td>
<td>4#2。 只能用DayofMonth。 某月的第二个星期三 &nbsp;</td>
















</tr>
















</tbody>
















</table>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>实例：</p>
<p>每天8-20点间隔28分钟执行一次：0 0/28 8-20 * * ?" <br />间隔10秒跑一次：0/10 * 8-20 * * ?<br />每天8-20天，30分钟执行一次： 0 0/30 8-20 * * ? <br />周一到周五凌晨2点执行：      0 0 2 ? * MON-FRI  执行一次 </p>
<p>&rdquo;0 0 10,14,16 * * ?" &nbsp; &nbsp;每天10点，14点，16点 触发。</p>
<p>"0 0/5 14,18 * * ?" &nbsp; &nbsp;每天14点或18点中，每5分钟触发 。</p>
<p>"0 4/15 14-18 * * ?" &nbsp; &nbsp; &nbsp; 每天14点到18点期间, &nbsp;从第四分钟触发，每15分钟一次。</p>
<p>"0 15 10 ? * 6L"&nbsp; &nbsp; &nbsp; &nbsp;&nbsp;每月的最后一个星期五上午10:15触发。</p>
<p><a href="http://cron.qqe2.com/" target="_blank">&nbsp;http://cron.qqe2.com/</a></p>
<p>六、操作案例</p>
<p>1，trigger先绑定job，然后在执行</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('b40471e4-1c89-4fe2-849d-172b81894521')"><img id="code_img_closed_b40471e4-1c89-4fe2-849d-172b81894521" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_b40471e4-1c89-4fe2-849d-172b81894521" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('b40471e4-1c89-4fe2-849d-172b81894521',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_b40471e4-1c89-4fe2-849d-172b81894521" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Impl;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Listener;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Impl.Matchers;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ConsoleApp3
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">开始</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">scheduler [10 +1 都开启了，只不过都是等待状态]</span>
            <span style="color: #0000ff;">var</span> scheduler =<span style="color: #000000;"> StdSchedulerFactory.GetDefaultScheduler().Result;
            </span><span style="color: #008000;">//</span><span style="color: #008000;">[start 会让 调度线程 启动，从jobstore中获取快要执行的trigger，然后获取trigger关联的job进行执行。]</span>
<span style="color: #000000;">            scheduler.Start();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">job</span>
            <span style="color: #0000ff;">var</span> job = JobBuilder.Create&lt;JobTest&gt;<span style="color: #000000;">()
                .StoreDurably(</span><span style="color: #0000ff;">true</span><span style="color: #000000;">)
                .Build();
            scheduler.AddJob(job, </span><span style="color: #0000ff;">true</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">trigger </span>
            <span style="color: #0000ff;">var</span> trigger =<span style="color: #000000;"> TriggerBuilder.Create().ForJob(job)
                .WithCronSchedule(</span><span style="color: #800000;">"</span><span style="color: #800000;">* * * * * ?</span><span style="color: #800000;">"</span><span style="color: #000000;">).Build();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">使用这句话的前提是job必须是持久化的，否则只能使用下面那句话</span>
<span style="color: #000000;">            scheduler.ScheduleJob(trigger);
            </span><span style="color: #008000;">//</span><span style="color: #008000;">scheduler.ScheduleJob(job,trigger);</span>
<span style="color: #000000;">
            Console.ReadLine();
        }
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> JobTest : IJob
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">int</span> index = <span style="color: #800080;">0</span><span style="color: #000000;">;
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span><span style="color: #000000;"> Task Execute(IJobExecutionContext context)
        {
            index</span>++<span style="color: #000000;">;

            </span><span style="color: #008000;">//</span><span style="color: #008000;">记录当前时间，记录&ldquo;scheduler&rdquo;调度时间 ，记录 下一次触发时间</span>
            Console.WriteLine(<span style="color: #800000;">"</span><span style="color: #800000;">index={0}, current={1},schedulertime={2},nexttime={3}</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                                                                        index, DateTime.Now,
                                                                        context.ScheduledFireTimeUtc</span>?<span style="color: #000000;">.LocalDateTime,
                                                                        context.NextFireTimeUtc</span>?<span style="color: #000000;">.LocalDateTime);
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">demo</span></div>
<p>2，job操作</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('85ee73ec-0f57-4e54-8dcd-08ba71eff326')"><img id="code_img_closed_85ee73ec-0f57-4e54-8dcd-08ba71eff326" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_85ee73ec-0f57-4e54-8dcd-08ba71eff326" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('85ee73ec-0f57-4e54-8dcd-08ba71eff326',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_85ee73ec-0f57-4e54-8dcd-08ba71eff326" class="cnblogs_code_hide">
<pre>List&lt;JobDetailImpl&gt; jobList = <span style="color: #0000ff;">new</span> List&lt;JobDetailImpl&gt;<span style="color: #000000;">();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">第一步：获取所有的job信息</span>
            <span style="color: #0000ff;">var</span> jobKeySet = scheduler.GetJobKeys(GroupMatcher&lt;JobKey&gt;<span style="color: #000000;">.AnyGroup());

            </span><span style="color: #0000ff;">foreach</span> (<span style="color: #0000ff;">var</span> jobKey <span style="color: #0000ff;">in</span><span style="color: #000000;"> jobKeySet)
            {
                </span><span style="color: #0000ff;">var</span> jobDetail =<span style="color: #000000;"> (JobDetailImpl)scheduler.GetJobDetail(jobKey);

                jobList.Add(jobDetail);
            }

            </span><span style="color: #0000ff;">var</span> json = JsonConvert.SerializeObject(jobList.Select(i =&gt; <span style="color: #0000ff;">new</span><span style="color: #000000;">
            {
                i.Name,
                i.Group,
                i.Durable,
                i.JobDataMap,
                i.Description,
                TriggerList </span>= <span style="color: #0000ff;">string</span>.Join(<span style="color: #800000;">"</span><span style="color: #800000;">,</span><span style="color: #800000;">"</span>, scheduler.GetTriggersOfJob(<span style="color: #0000ff;">new</span><span style="color: #000000;"> JobKey(i.Name, i.Group))
                                    .Select(m </span>=&gt;<span style="color: #000000;"> m.Key.ToString()))
            }));</span></pre>
</div>
<span class="cnblogs_code_collapse">查询job</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('f083453a-24b7-49ee-bcb5-2fd892841ba1')"><img id="code_img_closed_f083453a-24b7-49ee-bcb5-2fd892841ba1" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_f083453a-24b7-49ee-bcb5-2fd892841ba1" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('f083453a-24b7-49ee-bcb5-2fd892841ba1',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_f083453a-24b7-49ee-bcb5-2fd892841ba1" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">var</span> exists = scheduler.CheckExists(<span style="color: #0000ff;">new</span><span style="color: #000000;"> JobKey(jobRequest.JobName,
                                                              jobRequest.JobGroupName));

                </span><span style="color: #0000ff;">if</span> (exists &amp;&amp; !<span style="color: #000000;">jobRequest.IsEdit)
                {
                    </span><span style="color: #0000ff;">return</span> Json(<span style="color: #800000;">"</span><span style="color: #800000;">已经存在同名的Job，请更换！</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                }

                </span><span style="color: #0000ff;">var</span> assemblyName = jobRequest.JobFullClass.Split(<span style="color: #800000;">'</span><span style="color: #800000;">.</span><span style="color: #800000;">'</span>)[<span style="color: #800080;">0</span><span style="color: #000000;">];
                </span><span style="color: #0000ff;">var</span> fullName =<span style="color: #000000;"> jobRequest.JobFullClass;
                </span><span style="color: #0000ff;">var</span> dllpath = Request.MapPath(<span style="color: #0000ff;">string</span>.Format(<span style="color: #800000;">"</span><span style="color: #800000;">~/bin/{0}.dll</span><span style="color: #800000;">"</span><span style="color: #000000;">, assemblyName));

                </span><span style="color: #008000;">//</span><span style="color: #008000;">需要执行的job名称</span>
                <span style="color: #0000ff;">var</span> jobClassName =<span style="color: #000000;"> Assembly.LoadFile(dllpath)
                                           .CreateInstance(jobRequest.JobFullClass);

                </span><span style="color: #008000;">//</span><span style="color: #008000;">第一种方式：</span>
                <span style="color: #0000ff;">var</span> job = JobBuilder.Create(jobClassName.GetType()).StoreDurably(<span style="color: #0000ff;">true</span><span style="color: #000000;">)
                                          .WithIdentity(jobRequest.JobName, jobRequest.JobGroupName)
                                          .WithDescription(jobRequest.Description)
                                          .Build();
                
                scheduler.AddJob(job, </span><span style="color: #0000ff;">true</span><span style="color: #000000;">);

                </span><span style="color: #008000;">//</span><span style="color: #008000;">第二种方式：获取job信息，再更新实体。。。</span>
                <span style="color: #0000ff;">var</span> jobdetail = scheduler.GetJobDetail(<span style="color: #0000ff;">new</span> JobKey(jobRequest.JobName, jobRequest.JobGroupName));</pre>
</div>
<span class="cnblogs_code_collapse">添加job</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('0beee030-747f-4f63-8610-6177710bd60c')"><img id="code_img_closed_0beee030-747f-4f63-8610-6177710bd60c" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_0beee030-747f-4f63-8610-6177710bd60c" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('0beee030-747f-4f63-8610-6177710bd60c',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_0beee030-747f-4f63-8610-6177710bd60c" class="cnblogs_code_hide">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">job暂停，所有关联的trigger也必须暂停</span>
                scheduler.PauseJob(<span style="color: #0000ff;">new</span> JobKey(jobName, groupName));</pre>
</div>
<span class="cnblogs_code_collapse">暂停job</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('119913f1-74f2-4712-a01a-b902784c9e92')"><img id="code_img_closed_119913f1-74f2-4712-a01a-b902784c9e92" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_119913f1-74f2-4712-a01a-b902784c9e92" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('119913f1-74f2-4712-a01a-b902784c9e92',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_119913f1-74f2-4712-a01a-b902784c9e92" class="cnblogs_code_hide">
<pre> scheduler.ResumeJob(<span style="color: #0000ff;">new</span> JobKey(jobName, groupName));</pre>
</div>
<span class="cnblogs_code_collapse">恢复job</span></div>
<p>&nbsp;2，trigger操作</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('e7f522a6-ca43-4a66-8af9-6ea1d85d980c')"><img id="code_img_closed_e7f522a6-ca43-4a66-8af9-6ea1d85d980c" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_e7f522a6-ca43-4a66-8af9-6ea1d85d980c" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('e7f522a6-ca43-4a66-8af9-6ea1d85d980c',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_e7f522a6-ca43-4a66-8af9-6ea1d85d980c" class="cnblogs_code_hide">
<pre> List&lt;CronTriggerImpl&gt; triggerList = <span style="color: #0000ff;">new</span> List&lt;CronTriggerImpl&gt;<span style="color: #000000;">();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">第一步：获取所有的trigger信息</span>
            <span style="color: #0000ff;">var</span> triggerKeys = scheduler.GetTriggerKeys(GroupMatcher&lt;TriggerKey&gt;<span style="color: #000000;">.AnyGroup());

            </span><span style="color: #0000ff;">foreach</span> (<span style="color: #0000ff;">var</span> triggerkey <span style="color: #0000ff;">in</span><span style="color: #000000;"> triggerKeys)
            {
                </span><span style="color: #0000ff;">var</span> triggerDetail =<span style="color: #000000;"> (CronTriggerImpl)scheduler.GetTrigger(triggerkey);

                triggerList.Add(triggerDetail);
            }

            </span><span style="color: #0000ff;">var</span> json = JsonConvert.SerializeObject(triggerList.Select(i =&gt; <span style="color: #0000ff;">new</span><span style="color: #000000;">
            {
                i.FullName,
                i.FullJobName,
                i.CronExpressionString,
                JobClassName </span>=<span style="color: #000000;"> scheduler.GetJobDetail(i.JobKey).JobType.FullName,
                StartFireTime </span>= i.StartTimeUtc.LocalDateTime.ToString(<span style="color: #800000;">"</span><span style="color: #800000;">yyyy-MM-dd HH:mm:ss</span><span style="color: #800000;">"</span><span style="color: #000000;">),
                PrevFireTime </span>= i.GetPreviousFireTimeUtc()?.LocalDateTime.ToString(<span style="color: #800000;">"</span><span style="color: #800000;">yyyy-MM-dd HH:mm:ss</span><span style="color: #800000;">"</span><span style="color: #000000;">),
                NextFireTime </span>= i.GetNextFireTimeUtc()?.LocalDateTime.ToString(<span style="color: #800000;">"</span><span style="color: #800000;">yyyy-MM-dd HH:mm:ss</span><span style="color: #800000;">"</span><span style="color: #000000;">),
                TriggerStatus </span>= scheduler.GetTriggerState(<span style="color: #0000ff;">new</span><span style="color: #000000;"> TriggerKey(i.Name, i.Group)).ToString(),
                i.Priority,
                i.Description,
                i.Name,
                i.Group
            }));</span></pre>
</div>
<span class="cnblogs_code_collapse">查询</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('83bc0e3a-fac9-467e-8244-7afd329c8d85')"><img id="code_img_closed_83bc0e3a-fac9-467e-8244-7afd329c8d85" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_83bc0e3a-fac9-467e-8244-7afd329c8d85" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('83bc0e3a-fac9-467e-8244-7afd329c8d85',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_83bc0e3a-fac9-467e-8244-7afd329c8d85" class="cnblogs_code_hide">
<pre> <span style="color: #0000ff;">var</span> exists = scheduler.CheckExists(<span style="color: #0000ff;">new</span><span style="color: #000000;"> TriggerKey(triggerRequest.TriggerName,
                                                                 triggerRequest.TriggerGroupName));

                </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (exists)
                {
                    </span><span style="color: #0000ff;">return</span> Json(<span style="color: #800000;">"</span><span style="color: #800000;">已经存在同名的trigger，请更换！</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                }

                </span><span style="color: #0000ff;">var</span> forJobName = triggerRequest.ForJobName.Split(<span style="color: #800000;">'</span><span style="color: #800000;">.</span><span style="color: #800000;">'</span><span style="color: #000000;">);
                </span><span style="color: #0000ff;">var</span> trigger = TriggerBuilder.Create().ForJob(forJobName[<span style="color: #800080;">1</span>], forJobName[<span style="color: #800080;">0</span><span style="color: #000000;">])
                                            .WithIdentity(triggerRequest.TriggerName, triggerRequest.TriggerGroupName)
                                            .WithCronSchedule(triggerRequest.CronExpress)
                                            .WithDescription(triggerRequest.Description)
                                            .Build();

                scheduler.ScheduleJob(trigger);</span></pre>
</div>
<span class="cnblogs_code_collapse">添加</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('884c8965-c622-4ce3-992d-e79fe7246f9b')"><img id="code_img_closed_884c8965-c622-4ce3-992d-e79fe7246f9b" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_884c8965-c622-4ce3-992d-e79fe7246f9b" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('884c8965-c622-4ce3-992d-e79fe7246f9b',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_884c8965-c622-4ce3-992d-e79fe7246f9b" class="cnblogs_code_hide">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">暂停 &ldquo;某一个trigger&rdquo;</span>
                scheduler.PauseTrigger(<span style="color: #0000ff;">new</span> TriggerKey(name, group));</pre>
</div>
<span class="cnblogs_code_collapse">暂停</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('865c35f8-1864-4ef3-9bb8-1bebee6d1313')"><img id="code_img_closed_865c35f8-1864-4ef3-9bb8-1bebee6d1313" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_865c35f8-1864-4ef3-9bb8-1bebee6d1313" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('865c35f8-1864-4ef3-9bb8-1bebee6d1313',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_865c35f8-1864-4ef3-9bb8-1bebee6d1313" class="cnblogs_code_hide">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">恢复 &ldquo;某一个trigger&rdquo;</span>
                scheduler.ResumeTrigger(<span style="color: #0000ff;">new</span> TriggerKey(name, group));</pre>
</div>
<span class="cnblogs_code_collapse">恢复</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('82bdba16-36bb-4f73-83cb-5024ab47e28f')"><img id="code_img_closed_82bdba16-36bb-4f73-83cb-5024ab47e28f" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_82bdba16-36bb-4f73-83cb-5024ab47e28f" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('82bdba16-36bb-4f73-83cb-5024ab47e28f',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_82bdba16-36bb-4f73-83cb-5024ab47e28f" class="cnblogs_code_hide">
<pre>scheduler.UnscheduleJob(<span style="color: #0000ff;">new</span> TriggerKey(name, group));</pre>
</div>
<span class="cnblogs_code_collapse">删除</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('c6b8b9d1-df6e-4efd-8bee-0580ead2b9e9')"><img id="code_img_closed_c6b8b9d1-df6e-4efd-8bee-0580ead2b9e9" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_c6b8b9d1-df6e-4efd-8bee-0580ead2b9e9" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('c6b8b9d1-df6e-4efd-8bee-0580ead2b9e9',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_c6b8b9d1-df6e-4efd-8bee-0580ead2b9e9" class="cnblogs_code_hide">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">编辑Trigger</span>
                <span style="color: #0000ff;">var</span> forJobName = triggerRequest.ForJobName.Split(<span style="color: #800000;">'</span><span style="color: #800000;">.</span><span style="color: #800000;">'</span><span style="color: #000000;">);

                </span><span style="color: #0000ff;">var</span> trigger = TriggerBuilder.Create().ForJob(forJobName[<span style="color: #800080;">1</span>], forJobName[<span style="color: #800080;">0</span><span style="color: #000000;">])
                                            .WithIdentity(triggerRequest.TriggerName, triggerRequest.TriggerGroupName)
                                            .WithCronSchedule(triggerRequest.CronExpress)
                                            .WithDescription(triggerRequest.Description)
                                            .Build();

                </span><span style="color: #008000;">//</span><span style="color: #008000;">编辑trigger操作</span>
                scheduler.RescheduleJob(<span style="color: #0000ff;">new</span> TriggerKey(triggerRequest.TriggerName, triggerRequest.TriggerGroupName), trigger);</pre>
</div>
<span class="cnblogs_code_collapse">编辑</span></div>
<p>3，scheduler操作</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('94d98a64-e53e-4095-b245-7d70442fba76')"><img id="code_img_closed_94d98a64-e53e-4095-b245-7d70442fba76" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_94d98a64-e53e-4095-b245-7d70442fba76" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('94d98a64-e53e-4095-b245-7d70442fba76',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_94d98a64-e53e-4095-b245-7d70442fba76" class="cnblogs_code_hide">
<pre> <span style="color: #0000ff;">var</span> meta = scheduler.GetMetaData();</pre>
</div>
<span class="cnblogs_code_collapse">获取元数据</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('570a634f-4ec0-4120-aeb0-d36fa88f28e5')"><img id="code_img_closed_570a634f-4ec0-4120-aeb0-d36fa88f28e5" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_570a634f-4ec0-4120-aeb0-d36fa88f28e5" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('570a634f-4ec0-4120-aeb0-d36fa88f28e5',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_570a634f-4ec0-4120-aeb0-d36fa88f28e5" class="cnblogs_code_hide">
<pre>  <span style="color: #0000ff;">if</span><span style="color: #000000;"> (scheduler.InStandbyMode)
                {
                    </span><span style="color: #008000;">//</span><span style="color: #008000;">只有暂停的状态，才能重新开启</span>
<span style="color: #000000;">                    scheduler.Start();
                }</span></pre>
</div>
<span class="cnblogs_code_collapse">恢复</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('844c8701-be6d-4fc6-ba0e-76f6a60bc62f')"><img id="code_img_closed_844c8701-be6d-4fc6-ba0e-76f6a60bc62f" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_844c8701-be6d-4fc6-ba0e-76f6a60bc62f" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('844c8701-be6d-4fc6-ba0e-76f6a60bc62f',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_844c8701-be6d-4fc6-ba0e-76f6a60bc62f" class="cnblogs_code_hide">
<pre> <span style="color: #0000ff;">if</span><span style="color: #000000;"> (scheduler.IsStarted)
                {
                    </span><span style="color: #008000;">//</span><span style="color: #008000;">暂停scheduler</span>
<span style="color: #000000;">                    scheduler.Standby();
                }</span></pre>
</div>
<span class="cnblogs_code_collapse">暂停</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('45d365f7-03a5-4199-99a9-87bd8c5c7bae')"><img id="code_img_closed_45d365f7-03a5-4199-99a9-87bd8c5c7bae" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_45d365f7-03a5-4199-99a9-87bd8c5c7bae" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('45d365f7-03a5-4199-99a9-87bd8c5c7bae',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_45d365f7-03a5-4199-99a9-87bd8c5c7bae" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">if</span> (scheduler.IsStarted ||<span style="color: #000000;"> scheduler.InStandbyMode)
                {
                    </span><span style="color: #008000;">//</span><span style="color: #008000;">暂停scheduler</span>
<span style="color: #000000;">                    scheduler.Shutdown();
                }</span></pre>
</div>
<span class="cnblogs_code_collapse">关闭</span></div>
<p>&nbsp;4，整个demo</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('423a967d-63d2-4b4b-b795-f52866de4f06')"><img id="code_img_closed_423a967d-63d2-4b4b-b795-f52866de4f06" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_423a967d-63d2-4b4b-b795-f52866de4f06" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('423a967d-63d2-4b4b-b795-f52866de4f06',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_423a967d-63d2-4b4b-b795-f52866de4f06" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> Newtonsoft.Json;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Impl;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Impl.Matchers;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Impl.Triggers;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Reflection;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Web;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Web.Mvc;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> WebApplication1.Entitys;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> WebApplication1.Controllers
{
    [RoutePrefix(</span><span style="color: #800000;">"</span><span style="color: #800000;">quartz</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> QuartzController : Controller
    {
        </span><span style="color: #0000ff;">static</span> IScheduler scheduler = <span style="color: #0000ff;">null</span><span style="color: #000000;">;

        </span><span style="color: #0000ff;">static</span><span style="color: #000000;"> QuartzController()
        {
            scheduler </span>=<span style="color: #000000;"> StdSchedulerFactory.GetDefaultScheduler();
            scheduler.Start();
        }

        [Route(</span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> ActionResult Index()
        {
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> View();
        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;">查询job</span>
        [Route(<span style="color: #800000;">"</span><span style="color: #800000;">joblist</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> JsonResult JobList()
        {
            List</span>&lt;JobDetailImpl&gt; jobList = <span style="color: #0000ff;">new</span> List&lt;JobDetailImpl&gt;<span style="color: #000000;">();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">第一步：获取所有的job信息</span>
            <span style="color: #0000ff;">var</span> jobKeySet = scheduler.GetJobKeys(GroupMatcher&lt;JobKey&gt;<span style="color: #000000;">.AnyGroup());

            </span><span style="color: #0000ff;">foreach</span> (<span style="color: #0000ff;">var</span> jobKey <span style="color: #0000ff;">in</span><span style="color: #000000;"> jobKeySet)
            {
                </span><span style="color: #0000ff;">var</span> jobDetail =<span style="color: #000000;"> (JobDetailImpl)scheduler.GetJobDetail(jobKey);

                jobList.Add(jobDetail);
            }

            </span><span style="color: #0000ff;">var</span> json = JsonConvert.SerializeObject(jobList.Select(i =&gt; <span style="color: #0000ff;">new</span><span style="color: #000000;">
            {
                i.Name,
                i.Group,
                i.Durable,
                i.JobDataMap,
                i.Description,
                TriggerList </span>= <span style="color: #0000ff;">string</span>.Join(<span style="color: #800000;">"</span><span style="color: #800000;">,</span><span style="color: #800000;">"</span>, scheduler.GetTriggersOfJob(<span style="color: #0000ff;">new</span><span style="color: #000000;"> JobKey(i.Name, i.Group))
                                    .Select(m </span>=&gt;<span style="color: #000000;"> m.Key.ToString()))
            }));

            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> Json(json);
        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;">添加job</span>
        [Route(<span style="color: #800000;">"</span><span style="color: #800000;">addjob</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> JsonResult AddJob(JobRequestEntity jobRequest)
        {
            </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
            {
                </span><span style="color: #0000ff;">var</span> exists = scheduler.CheckExists(<span style="color: #0000ff;">new</span><span style="color: #000000;"> JobKey(jobRequest.JobName,
                                                              jobRequest.JobGroupName));

                </span><span style="color: #0000ff;">if</span> (exists &amp;&amp; !<span style="color: #000000;">jobRequest.IsEdit)
                {
                    </span><span style="color: #0000ff;">return</span> Json(<span style="color: #800000;">"</span><span style="color: #800000;">已经存在同名的Job，请更换！</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                }

                </span><span style="color: #0000ff;">var</span> assemblyName = jobRequest.JobFullClass.Split(<span style="color: #800000;">'</span><span style="color: #800000;">.</span><span style="color: #800000;">'</span>)[<span style="color: #800080;">0</span><span style="color: #000000;">];
                </span><span style="color: #0000ff;">var</span> fullName =<span style="color: #000000;"> jobRequest.JobFullClass;
                </span><span style="color: #0000ff;">var</span> dllpath = Request.MapPath(<span style="color: #0000ff;">string</span>.Format(<span style="color: #800000;">"</span><span style="color: #800000;">~/bin/{0}.dll</span><span style="color: #800000;">"</span><span style="color: #000000;">, assemblyName));

                </span><span style="color: #008000;">//</span><span style="color: #008000;">需要执行的job名称</span>
                <span style="color: #0000ff;">var</span> jobClassName =<span style="color: #000000;"> Assembly.LoadFile(dllpath)
                                           .CreateInstance(jobRequest.JobFullClass);

                </span><span style="color: #008000;">//</span><span style="color: #008000;">第一种方式：</span>
                <span style="color: #0000ff;">var</span> job = JobBuilder.Create(jobClassName.GetType()).StoreDurably(<span style="color: #0000ff;">true</span><span style="color: #000000;">)
                                          .WithIdentity(jobRequest.JobName, jobRequest.JobGroupName)
                                          .WithDescription(jobRequest.Description)
                                          .Build();
                
                scheduler.AddJob(job, </span><span style="color: #0000ff;">true</span><span style="color: #000000;">);

                </span><span style="color: #008000;">//</span><span style="color: #008000;">第二种方式：获取job信息，再更新实体。。。</span>
                <span style="color: #0000ff;">var</span> jobdetail = scheduler.GetJobDetail(<span style="color: #0000ff;">new</span><span style="color: #000000;"> JobKey(jobRequest.JobName, jobRequest.JobGroupName));
                
                </span><span style="color: #0000ff;">return</span> Json(<span style="color: #800000;">"</span><span style="color: #800000;">1</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }
            </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (Exception ex)
            {
                </span><span style="color: #0000ff;">throw</span><span style="color: #000000;">;
            }
        }
        </span><span style="color: #008000;">//</span><span style="color: #008000;">暂停job（可恢复）</span>
        [Route(<span style="color: #800000;">"</span><span style="color: #800000;">pausejob</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
        </span><span style="color: #0000ff;">public</span> JsonResult PauseJob(<span style="color: #0000ff;">string</span> jobName, <span style="color: #0000ff;">string</span><span style="color: #000000;"> groupName)
        {
            </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;">job暂停，所有关联的trigger也必须暂停</span>
                scheduler.PauseJob(<span style="color: #0000ff;">new</span><span style="color: #000000;"> JobKey(jobName, groupName));

                </span><span style="color: #0000ff;">return</span> Json(<span style="color: #800080;">1</span><span style="color: #000000;">);
            }
            </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (Exception ex)
            {
                </span><span style="color: #0000ff;">throw</span><span style="color: #000000;">;
            }
        }
        </span><span style="color: #008000;">//</span><span style="color: #008000;">恢复job</span>
        [Route(<span style="color: #800000;">"</span><span style="color: #800000;">resumejob</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
        </span><span style="color: #0000ff;">public</span> JsonResult ResumeJob(<span style="color: #0000ff;">string</span> jobName, <span style="color: #0000ff;">string</span><span style="color: #000000;"> groupName)
        {
            </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
            {
                scheduler.ResumeJob(</span><span style="color: #0000ff;">new</span><span style="color: #000000;"> JobKey(jobName, groupName));

                </span><span style="color: #0000ff;">return</span> Json(<span style="color: #800080;">1</span><span style="color: #000000;">);
            }
            </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (Exception ex)
            {
                </span><span style="color: #0000ff;">throw</span><span style="color: #000000;">;
            }
        }
        </span><span style="color: #008000;">//</span><span style="color: #008000;">删除job</span>
        [Route(<span style="color: #800000;">"</span><span style="color: #800000;">removejob</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
        </span><span style="color: #0000ff;">public</span> JsonResult RemoveJob(<span style="color: #0000ff;">string</span> jobName, <span style="color: #0000ff;">string</span><span style="color: #000000;"> groupName)
        {
            </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
            {
                </span><span style="color: #0000ff;">var</span> isSuccess = scheduler.DeleteJob(<span style="color: #0000ff;">new</span><span style="color: #000000;"> JobKey(jobName, groupName));

                </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> Json(isSuccess);
            }
            </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (Exception ex)
            {
                </span><span style="color: #0000ff;">throw</span><span style="color: #000000;">;
            }
        }
        </span><span style="color: #008000;">//</span><span style="color: #008000;">trigger查询</span>
        [Route(<span style="color: #800000;">"</span><span style="color: #800000;">triggerlist</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> JsonResult TriggerList()
        {
            List</span>&lt;CronTriggerImpl&gt; triggerList = <span style="color: #0000ff;">new</span> List&lt;CronTriggerImpl&gt;<span style="color: #000000;">();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">第一步：获取所有的trigger信息</span>
            <span style="color: #0000ff;">var</span> triggerKeys = scheduler.GetTriggerKeys(GroupMatcher&lt;TriggerKey&gt;<span style="color: #000000;">.AnyGroup());

            </span><span style="color: #0000ff;">foreach</span> (<span style="color: #0000ff;">var</span> triggerkey <span style="color: #0000ff;">in</span><span style="color: #000000;"> triggerKeys)
            {
                </span><span style="color: #0000ff;">var</span> triggerDetail =<span style="color: #000000;"> (CronTriggerImpl)scheduler.GetTrigger(triggerkey);

                triggerList.Add(triggerDetail);
            }

            </span><span style="color: #0000ff;">var</span> json = JsonConvert.SerializeObject(triggerList.Select(i =&gt; <span style="color: #0000ff;">new</span><span style="color: #000000;">
            {
                i.FullName,
                i.FullJobName,
                i.CronExpressionString,
                JobClassName </span>=<span style="color: #000000;"> scheduler.GetJobDetail(i.JobKey).JobType.FullName,
                StartFireTime </span>= i.StartTimeUtc.LocalDateTime.ToString(<span style="color: #800000;">"</span><span style="color: #800000;">yyyy-MM-dd HH:mm:ss</span><span style="color: #800000;">"</span><span style="color: #000000;">),
                PrevFireTime </span>= i.GetPreviousFireTimeUtc()?.LocalDateTime.ToString(<span style="color: #800000;">"</span><span style="color: #800000;">yyyy-MM-dd HH:mm:ss</span><span style="color: #800000;">"</span><span style="color: #000000;">),
                NextFireTime </span>= i.GetNextFireTimeUtc()?.LocalDateTime.ToString(<span style="color: #800000;">"</span><span style="color: #800000;">yyyy-MM-dd HH:mm:ss</span><span style="color: #800000;">"</span><span style="color: #000000;">),
                TriggerStatus </span>= scheduler.GetTriggerState(<span style="color: #0000ff;">new</span><span style="color: #000000;"> TriggerKey(i.Name, i.Group)).ToString(),
                i.Priority,
                i.Description,
                i.Name,
                i.Group
            }));

            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> Json(json);
        }
        </span><span style="color: #008000;">//</span><span style="color: #008000;">添加trigger</span>
        [Route(<span style="color: #800000;">"</span><span style="color: #800000;">addtrigger</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> JsonResult AddTrigger(TriggerRequestEntity triggerRequest)
        {
            </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
            {
                </span><span style="color: #0000ff;">var</span> exists = scheduler.CheckExists(<span style="color: #0000ff;">new</span><span style="color: #000000;"> TriggerKey(triggerRequest.TriggerName,
                                                                 triggerRequest.TriggerGroupName));

                </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (exists)
                {
                    </span><span style="color: #0000ff;">return</span> Json(<span style="color: #800000;">"</span><span style="color: #800000;">已经存在同名的trigger，请更换！</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                }

                </span><span style="color: #0000ff;">var</span> forJobName = triggerRequest.ForJobName.Split(<span style="color: #800000;">'</span><span style="color: #800000;">.</span><span style="color: #800000;">'</span><span style="color: #000000;">);
                </span><span style="color: #0000ff;">var</span> trigger = TriggerBuilder.Create().ForJob(forJobName[<span style="color: #800080;">1</span>], forJobName[<span style="color: #800080;">0</span><span style="color: #000000;">])
                                            .WithIdentity(triggerRequest.TriggerName, triggerRequest.TriggerGroupName)
                                            .WithCronSchedule(triggerRequest.CronExpress)
                                            .WithDescription(triggerRequest.Description)
                                            .Build();

                scheduler.ScheduleJob(trigger);

                </span><span style="color: #0000ff;">return</span> Json(<span style="color: #800000;">"</span><span style="color: #800000;">1</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }
            </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (Exception ex)
            {
                </span><span style="color: #0000ff;">throw</span><span style="color: #000000;">;
            }
        }
        </span><span style="color: #008000;">//</span><span style="color: #008000;">暂停trigger（可恢复）</span>
        [Route(<span style="color: #800000;">"</span><span style="color: #800000;">pausetrigger</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
        </span><span style="color: #0000ff;">public</span> JsonResult PauseTrigger(<span style="color: #0000ff;">string</span> name, <span style="color: #0000ff;">string</span><span style="color: #000000;"> group)
        {
            </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;">暂停 &ldquo;某一个trigger&rdquo;</span>
                scheduler.PauseTrigger(<span style="color: #0000ff;">new</span><span style="color: #000000;"> TriggerKey(name, group));

                </span><span style="color: #0000ff;">return</span> Json(<span style="color: #800000;">"</span><span style="color: #800000;">1</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }
            </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (Exception ex)
            {
                </span><span style="color: #0000ff;">throw</span><span style="color: #000000;">;
            }
        }
        </span><span style="color: #008000;">//</span><span style="color: #008000;">恢复trigger</span>
        [Route(<span style="color: #800000;">"</span><span style="color: #800000;">resumetrigger</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
        </span><span style="color: #0000ff;">public</span> JsonResult ResumeTrigger(<span style="color: #0000ff;">string</span> name, <span style="color: #0000ff;">string</span><span style="color: #000000;"> group)
        {
            </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;">恢复 &ldquo;某一个trigger&rdquo;</span>
                scheduler.ResumeTrigger(<span style="color: #0000ff;">new</span><span style="color: #000000;"> TriggerKey(name, group));

                </span><span style="color: #0000ff;">return</span> Json(<span style="color: #800000;">"</span><span style="color: #800000;">1</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }
            </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (Exception ex)
            {
                </span><span style="color: #0000ff;">throw</span><span style="color: #000000;">;
            }
        }
        </span><span style="color: #008000;">//</span><span style="color: #008000;">删除trigger</span>
        [Route(<span style="color: #800000;">"</span><span style="color: #800000;">removetrigger</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
        </span><span style="color: #0000ff;">public</span> JsonResult RemoveTrigger(<span style="color: #0000ff;">string</span> name, <span style="color: #0000ff;">string</span><span style="color: #000000;"> group)
        {
            </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
            {
                scheduler.UnscheduleJob(</span><span style="color: #0000ff;">new</span><span style="color: #000000;"> TriggerKey(name, group));

                </span><span style="color: #0000ff;">return</span> Json(<span style="color: #800000;">"</span><span style="color: #800000;">1</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }
            </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (Exception ex)
            {
                </span><span style="color: #0000ff;">throw</span><span style="color: #000000;">;
            }
        }
        </span><span style="color: #008000;">//</span><span style="color: #008000;">编辑trigger</span>
        [Route(<span style="color: #800000;">"</span><span style="color: #800000;">edittrigger</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> JsonResult EditTrigger(TriggerRequestEntity triggerRequest)
        {
            </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;">编辑Trigger</span>
                <span style="color: #0000ff;">var</span> forJobName = triggerRequest.ForJobName.Split(<span style="color: #800000;">'</span><span style="color: #800000;">.</span><span style="color: #800000;">'</span><span style="color: #000000;">);

                </span><span style="color: #0000ff;">var</span> trigger = TriggerBuilder.Create().ForJob(forJobName[<span style="color: #800080;">1</span>], forJobName[<span style="color: #800080;">0</span><span style="color: #000000;">])
                                            .WithIdentity(triggerRequest.TriggerName, triggerRequest.TriggerGroupName)
                                            .WithCronSchedule(triggerRequest.CronExpress)
                                            .WithDescription(triggerRequest.Description)
                                            .Build();

                </span><span style="color: #008000;">//</span><span style="color: #008000;">编辑trigger操作</span>
                scheduler.RescheduleJob(<span style="color: #0000ff;">new</span><span style="color: #000000;"> TriggerKey(triggerRequest.TriggerName, triggerRequest.TriggerGroupName), trigger);

                </span><span style="color: #0000ff;">return</span> Json(<span style="color: #800000;">"</span><span style="color: #800000;">1</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }
            </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (Exception ex)
            {
                </span><span style="color: #0000ff;">throw</span><span style="color: #000000;">;
            }
        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;">获取scheduler元数据信息</span>
        [Route(<span style="color: #800000;">"</span><span style="color: #800000;">getmeta</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> JsonResult GetMeta()
        {
            </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
            {
                </span><span style="color: #0000ff;">var</span> meta =<span style="color: #000000;"> scheduler.GetMetaData();

                </span><span style="color: #0000ff;">var</span> json =<span style="color: #000000;"> JsonConvert.SerializeObject(meta);

                </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> Json(json);
            }
            </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (Exception ex)
            {
                </span><span style="color: #0000ff;">throw</span><span style="color: #000000;">;
            }
        }

        </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
        <span style="color: #808080;">///</span><span style="color: #008000;"> 恢复scheduler
        </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
        <span style="color: #808080;">///</span> <span style="color: #808080;">&lt;returns&gt;&lt;/returns&gt;</span>
        [Route(<span style="color: #800000;">"</span><span style="color: #800000;">resumescheduler</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> JsonResult ResumeScheduler()
        {
            </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
            {
                </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (scheduler.InStandbyMode)
                {
                    </span><span style="color: #008000;">//</span><span style="color: #008000;">只有暂停的状态，才能重新开启</span>
<span style="color: #000000;">                    scheduler.Start();
                }

                </span><span style="color: #0000ff;">return</span> Json(<span style="color: #800080;">1</span><span style="color: #000000;">);
            }
            </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (Exception ex)
            {
                </span><span style="color: #0000ff;">throw</span><span style="color: #000000;">;
            }
        }

        </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
        <span style="color: #808080;">///</span><span style="color: #008000;"> 暂停scheduler
        </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
        <span style="color: #808080;">///</span> <span style="color: #808080;">&lt;returns&gt;&lt;/returns&gt;</span>
        [Route(<span style="color: #800000;">"</span><span style="color: #800000;">pausescheduler</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> JsonResult PauseScheduler()
        {
            </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
            {
                </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (scheduler.IsStarted)
                {
                    </span><span style="color: #008000;">//</span><span style="color: #008000;">暂停scheduler</span>
<span style="color: #000000;">                    scheduler.Standby();
                }

                </span><span style="color: #0000ff;">return</span> Json(<span style="color: #800080;">1</span><span style="color: #000000;">);
            }
            </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (Exception ex)
            {
                </span><span style="color: #0000ff;">throw</span><span style="color: #000000;">;
            }
        }
        </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
        <span style="color: #808080;">///</span><span style="color: #008000;"> 关闭scheduler
        </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
        <span style="color: #808080;">///</span> <span style="color: #808080;">&lt;returns&gt;&lt;/returns&gt;</span>
        [Route(<span style="color: #800000;">"</span><span style="color: #800000;">shutdownscheduler</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> JsonResult ShutDownScheduler()
        {
            </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
            {
                </span><span style="color: #0000ff;">if</span> (scheduler.IsStarted ||<span style="color: #000000;"> scheduler.InStandbyMode)
                {
                    </span><span style="color: #008000;">//</span><span style="color: #008000;">暂停scheduler</span>
<span style="color: #000000;">                    scheduler.Shutdown();
                }

                </span><span style="color: #0000ff;">return</span> Json(<span style="color: #800080;">1</span><span style="color: #000000;">);
            }
            </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (Exception ex)
            {
                </span><span style="color: #0000ff;">throw</span><span style="color: #000000;">;
            }
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">demo</span></div>
<p>下载地址：<a href="https://pan.baidu.com/s/1uQMuQEvsky1poiBzg1H3JA" target="_blank">https://pan.baidu.com/s/1uQMuQEvsky1poiBzg1H3JA</a></p>
<p>&nbsp;</p>
<p>七、六大calendar排除</p>
<p>1，DailyCalendar<br />【适合在某一天的时间段上做&ldquo;减法操作&rdquo;】</p>
<p>&nbsp;可以动态的排除某天的某些时间段</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('0a54a6b0-7520-40aa-bdac-139284217b6e')"><img id="code_img_closed_0a54a6b0-7520-40aa-bdac-139284217b6e" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_0a54a6b0-7520-40aa-bdac-139284217b6e" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('0a54a6b0-7520-40aa-bdac-139284217b6e',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_0a54a6b0-7520-40aa-bdac-139284217b6e" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Impl;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Listener;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Impl.Matchers;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Impl.Calendar;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ConsoleApp3
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">开始</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">scheduler [10 +1 都开启了，只不过都是等待状态]</span>
            <span style="color: #0000ff;">var</span> scheduler =<span style="color: #000000;"> StdSchedulerFactory.GetDefaultScheduler().Result;
            </span><span style="color: #008000;">//</span><span style="color: #008000;">[start 会让 调度线程 启动，从jobstore中获取快要执行的trigger，然后获取trigger关联的job进行执行。]</span>
<span style="color: #000000;">            scheduler.Start();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">job</span>
            <span style="color: #0000ff;">var</span> job = JobBuilder.Create&lt;JobTest&gt;<span style="color: #000000;">()
                .StoreDurably(</span><span style="color: #0000ff;">true</span><span style="color: #000000;">)
                .Build();
            scheduler.AddJob(job, </span><span style="color: #0000ff;">true</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">trigger </span>
            <span style="color: #0000ff;">var</span> trigger =<span style="color: #000000;"> TriggerBuilder.Create().ForJob(job)
                .ModifiedByCalendar(</span><span style="color: #800000;">"</span><span style="color: #800000;">daily</span><span style="color: #800000;">"</span><span style="color: #000000;">)
                .WithCronSchedule(</span><span style="color: #800000;">"</span><span style="color: #800000;">* * * * * ?</span><span style="color: #800000;">"</span><span style="color: #000000;">).Build();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">每天20点到21点不要执行</span>
            <span style="color: #0000ff;">var</span> daily = <span style="color: #0000ff;">new</span> DailyCalendar(DateBuilder.DateOf(<span style="color: #800080;">20</span>, <span style="color: #800080;">0</span>, <span style="color: #800080;">0</span>).DateTime, DateBuilder.DateOf(<span style="color: #800080;">21</span>, <span style="color: #800080;">0</span>, <span style="color: #800080;">0</span><span style="color: #000000;">).DateTime);
            scheduler.AddCalendar(</span><span style="color: #800000;">"</span><span style="color: #800000;">daily</span><span style="color: #800000;">"</span>, daily, <span style="color: #0000ff;">true</span>, <span style="color: #0000ff;">true</span><span style="color: #000000;">);


            scheduler.ScheduleJob(trigger);

            Console.ReadLine();
        }
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> JobTest : IJob
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">int</span> index = <span style="color: #800080;">0</span><span style="color: #000000;">;
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span><span style="color: #000000;"> Task Execute(IJobExecutionContext context)
        {
            index</span>++<span style="color: #000000;">;

            </span><span style="color: #008000;">//</span><span style="color: #008000;">记录当前时间，记录&ldquo;scheduler&rdquo;调度时间 ，记录 下一次触发时间</span>
            Console.WriteLine(<span style="color: #800000;">"</span><span style="color: #800000;">index={0}, current={1},schedulertime={2},nexttime={3}</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                                                                        index, DateTime.Now,
                                                                        context.ScheduledFireTimeUtc</span>?<span style="color: #000000;">.LocalDateTime,
                                                                        context.NextFireTimeUtc</span>?<span style="color: #000000;">.LocalDateTime);
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">每天20点到21点不要执行</span></div>
<p>&nbsp;</p>
<p>2，WeeklyCalendar<br />【适合以星期几的维度上做&ldquo;减法操作&rdquo;】</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('c4b38204-f5c6-4867-8689-97e4ab71f3ff')"><img id="code_img_closed_c4b38204-f5c6-4867-8689-97e4ab71f3ff" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_c4b38204-f5c6-4867-8689-97e4ab71f3ff" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('c4b38204-f5c6-4867-8689-97e4ab71f3ff',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_c4b38204-f5c6-4867-8689-97e4ab71f3ff" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Impl;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Listener;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Impl.Matchers;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Impl.Calendar;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ConsoleApp3
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">开始</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">scheduler [10 +1 都开启了，只不过都是等待状态]</span>
            <span style="color: #0000ff;">var</span> scheduler =<span style="color: #000000;"> StdSchedulerFactory.GetDefaultScheduler().Result;
            </span><span style="color: #008000;">//</span><span style="color: #008000;">[start 会让 调度线程 启动，从jobstore中获取快要执行的trigger，然后获取trigger关联的job进行执行。]</span>
<span style="color: #000000;">            scheduler.Start();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">job</span>
            <span style="color: #0000ff;">var</span> job = JobBuilder.Create&lt;JobTest&gt;<span style="color: #000000;">()
                .StoreDurably(</span><span style="color: #0000ff;">true</span><span style="color: #000000;">)
                .Build();
            scheduler.AddJob(job, </span><span style="color: #0000ff;">true</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">trigger </span>
            <span style="color: #0000ff;">var</span> trigger =<span style="color: #000000;"> TriggerBuilder.Create().ForJob(job)
                .ModifiedByCalendar(</span><span style="color: #800000;">"</span><span style="color: #800000;">calendar</span><span style="color: #800000;">"</span><span style="color: #000000;">)
                .WithCronSchedule(</span><span style="color: #800000;">"</span><span style="color: #800000;">* * * * * ?</span><span style="color: #800000;">"</span><span style="color: #000000;">).Build();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">每周五不执行</span>
            WeeklyCalendar calendar = <span style="color: #0000ff;">new</span><span style="color: #000000;"> WeeklyCalendar();
            calendar.SetDayExcluded(DayOfWeek.Friday, </span><span style="color: #0000ff;">true</span><span style="color: #000000;">);
            scheduler.AddCalendar(</span><span style="color: #800000;">"</span><span style="color: #800000;">calendar</span><span style="color: #800000;">"</span>, calendar, <span style="color: #0000ff;">true</span>, <span style="color: #0000ff;">true</span><span style="color: #000000;">);

            scheduler.ScheduleJob(trigger);

            Console.ReadLine();
        }
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> JobTest : IJob
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">int</span> index = <span style="color: #800080;">0</span><span style="color: #000000;">;
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span><span style="color: #000000;"> Task Execute(IJobExecutionContext context)
        {
            index</span>++<span style="color: #000000;">;

            </span><span style="color: #008000;">//</span><span style="color: #008000;">记录当前时间，记录&ldquo;scheduler&rdquo;调度时间 ，记录 下一次触发时间</span>
            Console.WriteLine(<span style="color: #800000;">"</span><span style="color: #800000;">index={0}, current={1},schedulertime={2},nexttime={3}</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                                                                        index, DateTime.Now,
                                                                        context.ScheduledFireTimeUtc</span>?<span style="color: #000000;">.LocalDateTime,
                                                                        context.NextFireTimeUtc</span>?<span style="color: #000000;">.LocalDateTime);
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">每周五不执行</span></div>
<p>&nbsp;</p>
<p>3，HolidayCalendar<br />【适合当年的某一天不能执行】</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('0db018ca-d370-4ea3-bb45-6ba93d6b1227')"><img id="code_img_closed_0db018ca-d370-4ea3-bb45-6ba93d6b1227" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_0db018ca-d370-4ea3-bb45-6ba93d6b1227" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('0db018ca-d370-4ea3-bb45-6ba93d6b1227',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_0db018ca-d370-4ea3-bb45-6ba93d6b1227" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Impl;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Listener;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Impl.Matchers;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Impl.Calendar;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ConsoleApp3
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">开始</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">scheduler [10 +1 都开启了，只不过都是等待状态]</span>
            <span style="color: #0000ff;">var</span> scheduler =<span style="color: #000000;"> StdSchedulerFactory.GetDefaultScheduler().Result;
            </span><span style="color: #008000;">//</span><span style="color: #008000;">[start 会让 调度线程 启动，从jobstore中获取快要执行的trigger，然后获取trigger关联的job进行执行。]</span>
<span style="color: #000000;">            scheduler.Start();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">job</span>
            <span style="color: #0000ff;">var</span> job = JobBuilder.Create&lt;JobTest&gt;<span style="color: #000000;">()
                .StoreDurably(</span><span style="color: #0000ff;">true</span><span style="color: #000000;">)
                .Build();
            scheduler.AddJob(job, </span><span style="color: #0000ff;">true</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">trigger </span>
            <span style="color: #0000ff;">var</span> trigger =<span style="color: #000000;"> TriggerBuilder.Create().ForJob(job)
                .ModifiedByCalendar(</span><span style="color: #800000;">"</span><span style="color: #800000;">calendar</span><span style="color: #800000;">"</span><span style="color: #000000;">)
                .WithCronSchedule(</span><span style="color: #800000;">"</span><span style="color: #800000;">* * * * * ?</span><span style="color: #800000;">"</span><span style="color: #000000;">).Build();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">指定某一天不能执行
            </span><span style="color: #008000;">//</span><span style="color: #008000;">6月16号不要执行</span>
            <span style="color: #0000ff;">var</span> calendar = <span style="color: #0000ff;">new</span><span style="color: #000000;"> HolidayCalendar();
            calendar.AddExcludedDate(DateTime.Now);
            scheduler.AddCalendar(</span><span style="color: #800000;">"</span><span style="color: #800000;">calendar</span><span style="color: #800000;">"</span>, calendar, <span style="color: #0000ff;">true</span>, <span style="color: #0000ff;">true</span><span style="color: #000000;">);

            scheduler.ScheduleJob(trigger);

            Console.ReadLine();
        }
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> JobTest : IJob
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">int</span> index = <span style="color: #800080;">0</span><span style="color: #000000;">;
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span><span style="color: #000000;"> Task Execute(IJobExecutionContext context)
        {
            index</span>++<span style="color: #000000;">;

            </span><span style="color: #008000;">//</span><span style="color: #008000;">记录当前时间，记录&ldquo;scheduler&rdquo;调度时间 ，记录 下一次触发时间</span>
            Console.WriteLine(<span style="color: #800000;">"</span><span style="color: #800000;">index={0}, current={1},schedulertime={2},nexttime={3}</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                                                                        index, DateTime.Now,
                                                                        context.ScheduledFireTimeUtc</span>?<span style="color: #000000;">.LocalDateTime,
                                                                        context.NextFireTimeUtc</span>?<span style="color: #000000;">.LocalDateTime);
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">6月16号不要执行</span></div>
<p>&nbsp;</p>
<p>4，MonthlyCalendar<br />【适合某个月中的某一天不能执行】</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('7ec6938e-8ffd-4264-acfc-d914590b1a29')"><img id="code_img_closed_7ec6938e-8ffd-4264-acfc-d914590b1a29" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_7ec6938e-8ffd-4264-acfc-d914590b1a29" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('7ec6938e-8ffd-4264-acfc-d914590b1a29',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_7ec6938e-8ffd-4264-acfc-d914590b1a29" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Impl;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Listener;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Impl.Matchers;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Impl.Calendar;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ConsoleApp3
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">开始</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">scheduler [10 +1 都开启了，只不过都是等待状态]</span>
            <span style="color: #0000ff;">var</span> scheduler =<span style="color: #000000;"> StdSchedulerFactory.GetDefaultScheduler().Result;
            </span><span style="color: #008000;">//</span><span style="color: #008000;">[start 会让 调度线程 启动，从jobstore中获取快要执行的trigger，然后获取trigger关联的job进行执行。]</span>
<span style="color: #000000;">            scheduler.Start();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">job</span>
            <span style="color: #0000ff;">var</span> job = JobBuilder.Create&lt;JobTest&gt;<span style="color: #000000;">()
                .StoreDurably(</span><span style="color: #0000ff;">true</span><span style="color: #000000;">)
                .Build();
            scheduler.AddJob(job, </span><span style="color: #0000ff;">true</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">trigger </span>
            <span style="color: #0000ff;">var</span> trigger =<span style="color: #000000;"> TriggerBuilder.Create().ForJob(job)
                .ModifiedByCalendar(</span><span style="color: #800000;">"</span><span style="color: #800000;">calendar</span><span style="color: #800000;">"</span><span style="color: #000000;">)
                .WithCronSchedule(</span><span style="color: #800000;">"</span><span style="color: #800000;">* * * * * ?</span><span style="color: #800000;">"</span><span style="color: #000000;">).Build();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">每月20号不要执行</span>
            <span style="color: #0000ff;">var</span> calendar = <span style="color: #0000ff;">new</span><span style="color: #000000;"> MonthlyCalendar();
            calendar.SetDayExcluded(</span><span style="color: #800080;">20</span>, <span style="color: #0000ff;">true</span><span style="color: #000000;">);
            scheduler.AddCalendar(</span><span style="color: #800000;">"</span><span style="color: #800000;">calendar</span><span style="color: #800000;">"</span>, calendar, <span style="color: #0000ff;">true</span>, <span style="color: #0000ff;">true</span><span style="color: #000000;">);

            scheduler.ScheduleJob(trigger);

            Console.ReadLine();
        }
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> JobTest : IJob
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">int</span> index = <span style="color: #800080;">0</span><span style="color: #000000;">;
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span><span style="color: #000000;"> Task Execute(IJobExecutionContext context)
        {
            index</span>++<span style="color: #000000;">;

            </span><span style="color: #008000;">//</span><span style="color: #008000;">记录当前时间，记录&ldquo;scheduler&rdquo;调度时间 ，记录 下一次触发时间</span>
            Console.WriteLine(<span style="color: #800000;">"</span><span style="color: #800000;">index={0}, current={1},schedulertime={2},nexttime={3}</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                                                                        index, DateTime.Now,
                                                                        context.ScheduledFireTimeUtc</span>?<span style="color: #000000;">.LocalDateTime,
                                                                        context.NextFireTimeUtc</span>?<span style="color: #000000;">.LocalDateTime);
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">每月20号不要执行</span></div>
<p>&nbsp;</p>
<p>5，AnnualCalendar<br />【适合每年指定的某一天不能执行】</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('ce4555c5-8789-4c81-8414-9ea0f25cd337')"><img id="code_img_closed_ce4555c5-8789-4c81-8414-9ea0f25cd337" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_ce4555c5-8789-4c81-8414-9ea0f25cd337" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('ce4555c5-8789-4c81-8414-9ea0f25cd337',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_ce4555c5-8789-4c81-8414-9ea0f25cd337" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Impl;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Listener;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Impl.Matchers;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Impl.Calendar;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ConsoleApp3
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">开始</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">scheduler [10 +1 都开启了，只不过都是等待状态]</span>
            <span style="color: #0000ff;">var</span> scheduler =<span style="color: #000000;"> StdSchedulerFactory.GetDefaultScheduler().Result;
            </span><span style="color: #008000;">//</span><span style="color: #008000;">[start 会让 调度线程 启动，从jobstore中获取快要执行的trigger，然后获取trigger关联的job进行执行。]</span>
<span style="color: #000000;">            scheduler.Start();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">job</span>
            <span style="color: #0000ff;">var</span> job = JobBuilder.Create&lt;JobTest&gt;<span style="color: #000000;">()
                .StoreDurably(</span><span style="color: #0000ff;">true</span><span style="color: #000000;">)
                .Build();
            scheduler.AddJob(job, </span><span style="color: #0000ff;">true</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">trigger </span>
            <span style="color: #0000ff;">var</span> trigger =<span style="color: #000000;"> TriggerBuilder.Create().ForJob(job)
                .ModifiedByCalendar(</span><span style="color: #800000;">"</span><span style="color: #800000;">calendar</span><span style="color: #800000;">"</span><span style="color: #000000;">)
                .WithCronSchedule(</span><span style="color: #800000;">"</span><span style="color: #800000;">* * * * * ?</span><span style="color: #800000;">"</span><span style="color: #000000;">).Build();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">指定月份中的某一天不能执行</span>
            <span style="color: #0000ff;">var</span> calendar = <span style="color: #0000ff;">new</span><span style="color: #000000;"> AnnualCalendar();
            calendar.SetDayExcluded(DateTime.Now, </span><span style="color: #0000ff;">true</span><span style="color: #000000;">);
            scheduler.AddCalendar(</span><span style="color: #800000;">"</span><span style="color: #800000;">calendar</span><span style="color: #800000;">"</span>, calendar, <span style="color: #0000ff;">true</span>, <span style="color: #0000ff;">true</span><span style="color: #000000;">);

            scheduler.ScheduleJob(trigger);

            Console.ReadLine();
        }
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> JobTest : IJob
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">int</span> index = <span style="color: #800080;">0</span><span style="color: #000000;">;
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span><span style="color: #000000;"> Task Execute(IJobExecutionContext context)
        {
            index</span>++<span style="color: #000000;">;

            </span><span style="color: #008000;">//</span><span style="color: #008000;">记录当前时间，记录&ldquo;scheduler&rdquo;调度时间 ，记录 下一次触发时间</span>
            Console.WriteLine(<span style="color: #800000;">"</span><span style="color: #800000;">index={0}, current={1},schedulertime={2},nexttime={3}</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                                                                        index, DateTime.Now,
                                                                        context.ScheduledFireTimeUtc</span>?<span style="color: #000000;">.LocalDateTime,
                                                                        context.NextFireTimeUtc</span>?<span style="color: #000000;">.LocalDateTime);
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">指定月份中的某一天不能执行</span></div>
<p>&nbsp;</p>
<p>6，CronCalendar<br />【字符串表达式来排除某一天，某一个月份，某一年都可以】</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('cb5748ad-1a41-4e80-a942-7ffe1c59bb2f')"><img id="code_img_closed_cb5748ad-1a41-4e80-a942-7ffe1c59bb2f" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_cb5748ad-1a41-4e80-a942-7ffe1c59bb2f" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('cb5748ad-1a41-4e80-a942-7ffe1c59bb2f',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_cb5748ad-1a41-4e80-a942-7ffe1c59bb2f" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Impl;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Listener;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Impl.Matchers;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Quartz.Impl.Calendar;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ConsoleApp3
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">开始</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">scheduler [10 +1 都开启了，只不过都是等待状态]</span>
            <span style="color: #0000ff;">var</span> scheduler =<span style="color: #000000;"> StdSchedulerFactory.GetDefaultScheduler().Result;
            </span><span style="color: #008000;">//</span><span style="color: #008000;">[start 会让 调度线程 启动，从jobstore中获取快要执行的trigger，然后获取trigger关联的job进行执行。]</span>
<span style="color: #000000;">            scheduler.Start();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">job</span>
            <span style="color: #0000ff;">var</span> job = JobBuilder.Create&lt;JobTest&gt;<span style="color: #000000;">()
                .StoreDurably(</span><span style="color: #0000ff;">true</span><span style="color: #000000;">)
                .Build();
            scheduler.AddJob(job, </span><span style="color: #0000ff;">true</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">trigger </span>
            <span style="color: #0000ff;">var</span> trigger =<span style="color: #000000;"> TriggerBuilder.Create().ForJob(job)
                .ModifiedByCalendar(</span><span style="color: #800000;">"</span><span style="color: #800000;">calendar</span><span style="color: #800000;">"</span><span style="color: #000000;">)
                .WithCronSchedule(</span><span style="color: #800000;">"</span><span style="color: #800000;">* * * * * ?</span><span style="color: #800000;">"</span><span style="color: #000000;">).Build();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">4月21号不要执行</span>
            <span style="color: #0000ff;">var</span> calendar = <span style="color: #0000ff;">new</span> CronCalendar(<span style="color: #800000;">"</span><span style="color: #800000;">* * * 21 4 ?</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            scheduler.AddCalendar(</span><span style="color: #800000;">"</span><span style="color: #800000;">calendar</span><span style="color: #800000;">"</span>, calendar, <span style="color: #0000ff;">true</span>, <span style="color: #0000ff;">true</span><span style="color: #000000;">);

            scheduler.ScheduleJob(trigger);

            Console.ReadLine();
        }
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> JobTest : IJob
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">int</span> index = <span style="color: #800080;">0</span><span style="color: #000000;">;
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span><span style="color: #000000;"> Task Execute(IJobExecutionContext context)
        {
            index</span>++<span style="color: #000000;">;

            </span><span style="color: #008000;">//</span><span style="color: #008000;">记录当前时间，记录&ldquo;scheduler&rdquo;调度时间 ，记录 下一次触发时间</span>
            Console.WriteLine(<span style="color: #800000;">"</span><span style="color: #800000;">index={0}, current={1},schedulertime={2},nexttime={3}</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                                                                        index, DateTime.Now,
                                                                        context.ScheduledFireTimeUtc</span>?<span style="color: #000000;">.LocalDateTime,
                                                                        context.NextFireTimeUtc</span>?<span style="color: #000000;">.LocalDateTime);
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">4月21号不要执行</span></div>
<p>&nbsp;</p>