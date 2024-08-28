<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">一、介绍</span></strong></span></p>
<p>在本文中，我将介绍如何为基于ASP.NET Boilerplate的项目创建单元测试。 我将使用本文开发的相同的应用程序（使用AngularJs，ASP.NET MVC，Web API和EntityFramework来构建NLayered单页面Web应用程序）而不是创建要测试的新应用程序。 解决方案结构就是这样：</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201710/741594-20171021151010646-2134118422.png" alt="" /></p>
<p>我们将测试项目的应用服务。 它包括SimpleTaskSystem.Core，SimpleTaskSystem.Application和SimpleTaskSystem.EntityFramework项目。 您可以阅读本文，了解如何构建此应用程序。 在这里，我将专注于测试。</p>
<p>参照项目：<a href="http://pan.baidu.com/s/1gf9xEU3" target="_blank">http://pan.baidu.com/s/1gf9xEU3</a></p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">二、创建一个项目</span></strong></span></p>
<p>我创建了一个名为SimpleTaskSystem.Test的新类库项目，并添加了以下nuget包：</p>
<ul style="margin-top: 10px; margin-right: 0px; margin-bottom: 10px; padding-top: 0px; padding-right: 0px; padding-bottom: 0px; border: 0px; color: #111111; font-family: 'Segoe UI', Arial, sans-serif;">
<li style="margin-top: 0px; margin-right: 0px; margin-bottom: 0px; padding-top: 0px; padding-right: 0px; padding-bottom: 0px; border: 0px; line-height: normal;"><strong style="margin: 0px; padding: 0px; border: 0px;">Abp.TestBase</strong>:&nbsp;提供一些基类，使基于ABP的项目更容易测试。</li>
<li style="margin-top: 0px; margin-right: 0px; margin-bottom: 0px; padding-top: 0px; padding-right: 0px; padding-bottom: 0px; border: 0px; line-height: normal;"><strong style="margin: 0px; padding: 0px; border: 0px;">Abp.EntityFramework</strong>:&nbsp;我们使用EntityFramework 6.x作为ORM。</li>
<li style="margin-top: 0px; margin-right: 0px; margin-bottom: 0px; padding-top: 0px; padding-right: 0px; padding-bottom: 0px; border: 0px; line-height: normal;"><strong style="margin: 0px; padding: 0px; border: 0px;">Effort.EF6</strong>:&nbsp;可以为易于使用的EF创建一个假的，内存中的数据库。</li>
<li style="margin-top: 0px; margin-right: 0px; margin-bottom: 0px; padding-top: 0px; padding-right: 0px; padding-bottom: 0px; border: 0px; line-height: normal;"><strong style="margin: 0px; padding: 0px; border: 0px;">xunit</strong>:&nbsp;我们将使用的测试框架。 另外，添加了xunit.runner.visualstudio包以在Visual Studio中运行测试。 当我写这篇文章时，这个包是预先释放的。 所以，我在nuget包管理器对话框中选择了'Include Prerelease'。</li>
<li style="margin-top: 0px; margin-right: 0px; margin-bottom: 0px; padding-top: 0px; padding-right: 0px; padding-bottom: 0px; border: 0px; line-height: normal;"><strong style="margin: 0px; padding: 0px; border: 0px;">Shouldly</strong>:&nbsp;此库容易编写断言。</li>
<li style="margin-top: 0px; margin-right: 0px; margin-bottom: 0px; padding-top: 0px; padding-right: 0px; padding-bottom: 0px; border: 0px; line-height: normal;"><strong>xunit.runner.visualstudio</strong>: 不安装此库，发现不了测试方法</li>
</ul>
<p>当我们添加这些包时，它们的依赖关系也将被自动添加。 最后，我们应该添加对SimpleTaskSystem.Application，SimpleTaskSystem.Core和SimpleTaskSystem.EntityFramework程序集的引用，因为我们将测试这些项目。</p>
<p>二、准备一个基础测试类</p>
<p>1，为了更容易地创建测试类，我将创建一个准备假数据库连接的基类：</p>
<div class="cnblogs_code">
<pre><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
    <span style="color: #808080;">///</span><span style="color: #008000;"> 这是所有测试类的基础类。
    </span><span style="color: #808080;">///</span><span style="color: #008000;"> 它准备了ABP系统，模块和一个伪造的内存数据库。
    </span><span style="color: #808080;">///</span><span style="color: #008000;"> 具有初始数据的种子数据库（</span><span style="color: #808080;">&lt;see cref =&ldquo;SimpleTaskSystemInitialDataBuilder&rdquo;/&gt;</span><span style="color: #008000;">）。
    </span><span style="color: #808080;">///</span><span style="color: #008000;"> 提供使用DbContext轻松使用的方法。
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">class</span> SimpleTaskSystemTestBase : AbpIntegratedTestBase&lt;SimpleTaskSystemTestModule&gt;<span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">protected</span><span style="color: #000000;"> SimpleTaskSystemTestBase()
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">种子初始数据</span>
            UsingDbContext(context =&gt; <span style="color: #0000ff;">new</span><span style="color: #000000;"> SimpleTaskSystemInitialDataBuilder().Build(context));
        }

        </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> PreInitialize()
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">假DbConnection使用Effort！</span>
<span style="color: #000000;">            LocalIocManager.IocContainer.Register(
                Component.For</span>&lt;DbConnection&gt;<span style="color: #000000;">()
                    .UsingFactoryMethod(Effort.DbConnectionFactory.CreateTransient)
                    .LifestyleSingleton()
                );

            </span><span style="color: #0000ff;">base</span><span style="color: #000000;">.PreInitialize();
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> UsingDbContext(Action&lt;SimpleTaskSystemDbContext&gt;<span style="color: #000000;"> action)
        {
            </span><span style="color: #0000ff;">using</span> (<span style="color: #0000ff;">var</span> context = LocalIocManager.Resolve&lt;SimpleTaskSystemDbContext&gt;<span style="color: #000000;">())
            {
                context.DisableAllFilters();
                action(context);
                context.SaveChanges();
            }
        }

        </span><span style="color: #0000ff;">public</span> T UsingDbContext&lt;T&gt;(Func&lt;SimpleTaskSystemDbContext, T&gt;<span style="color: #000000;"> func)
        {
            T result;

            </span><span style="color: #0000ff;">using</span> (<span style="color: #0000ff;">var</span> context = LocalIocManager.Resolve&lt;SimpleTaskSystemDbContext&gt;<span style="color: #000000;">())
            {
                context.DisableAllFilters();
                result </span>=<span style="color: #000000;"> func(context);
                context.SaveChanges();
            }

            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> result;
        }
    }</span></pre>
</div>
<p>该基类继承了<strong>AbpIntegratedTestBase</strong>，它是一个初始化了ABP系统的基类，定义了&nbsp;<span class="cnblogs_code"><span style="color: #0000ff;">protected</span> IIocManager LocalIocManager { <span style="color: #0000ff;">get</span>; }</span>&nbsp;。每个测试都会使用这个专用的IIocManager。因此，测试之间是相互隔离的。</p>
<p>在SimpleTaskSystemTestBase的PreInitialize方法中，我们正在使用Effort注册DbConnection到依赖注入系统（PreInitialize方法用于运行一些代码，仅用于ABP初始化）。 我们将其注册为Singleton（用于LocalIocConainer）。 因此，即使我们在同一测试中创建了多个DbContext，测试中也将使用相同的数据库（和连接）。</p>
<p>SimpleTaskSystemTestBase的UsingDbContext方法使得当我们需要直接使用DbContect来处理数据库时，可以更容易地创建DbContextes。 在构造函数中，我们使用它。 另外，我们将在测试中看到如何使用它。</p>
<p><span style="color: #ff0000;">SimpleTaskSystemDbContext必须具有获取DbConnection的构造函数才能使用该内存数据库。 所以，我添加下面的构造函数接受一个DbConnection：</span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SimpleTaskSystemDbContext : AbpDbContext
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">virtual</span> IDbSet&lt;Task&gt; Tasks { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">virtual</span> IDbSet&lt;Person&gt; People { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> SimpleTaskSystemDbContext()
        : </span><span style="color: #0000ff;">base</span>(<span style="color: #800000;">"</span><span style="color: #800000;">Default</span><span style="color: #800000;">"</span><span style="color: #000000;">)
    {

    }

    </span><span style="color: #0000ff;">public</span> SimpleTaskSystemDbContext(<span style="color: #0000ff;">string</span><span style="color: #000000;"> nameOrConnectionString)
        : </span><span style="color: #0000ff;">base</span><span style="color: #000000;">(nameOrConnectionString)
    {
            
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">这个构造函数用于测试</span>
    <span style="color: #0000ff;">public</span><span style="color: #000000;"> SimpleTaskSystemDbContext(DbConnection connection)
        : </span><span style="color: #0000ff;">base</span>(connection, <span style="color: #0000ff;">true</span><span style="color: #000000;">)
    {

    }
}</span></pre>
</div>
<p>在SimpleTaskSystemTestBase的构造函数中，我们还在数据库中创建一个初始数据。 这很重要，因为一些测试需要数据库中存在的数据。 SimpleTaskSystemInitialDataBuilder类填充数据库，如下所示：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SimpleTaskSystemInitialDataBuilder
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Build(SimpleTaskSystemDbContext context)
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;">添加一些人     </span>
<span style="color: #000000;">        context.People.AddOrUpdate(
            p </span>=&gt;<span style="color: #000000;"> p.Name,
            </span><span style="color: #0000ff;">new</span> Person {Name = <span style="color: #800000;">"</span><span style="color: #800000;">Isaac Asimov</span><span style="color: #800000;">"</span><span style="color: #000000;">},
            </span><span style="color: #0000ff;">new</span> Person {Name = <span style="color: #800000;">"</span><span style="color: #800000;">Thomas More</span><span style="color: #800000;">"</span><span style="color: #000000;">},
            </span><span style="color: #0000ff;">new</span> Person {Name = <span style="color: #800000;">"</span><span style="color: #800000;">George Orwell</span><span style="color: #800000;">"</span><span style="color: #000000;">},
            </span><span style="color: #0000ff;">new</span> Person {Name = <span style="color: #800000;">"</span><span style="color: #800000;">Douglas Adams</span><span style="color: #800000;">"</span><span style="color: #000000;">}
            );
        context.SaveChanges();

        </span><span style="color: #008000;">//</span><span style="color: #008000;">添加一些任务</span>
<span style="color: #000000;">        context.Tasks.AddOrUpdate(
            t </span>=&gt;<span style="color: #000000;"> t.Description,
            </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> Task
            {
                Description </span>= <span style="color: #800000;">"</span><span style="color: #800000;">my initial task 1</span><span style="color: #800000;">"</span><span style="color: #000000;">
            },
            </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> Task
            {
                Description </span>= <span style="color: #800000;">"</span><span style="color: #800000;">my initial task 2</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                State </span>=<span style="color: #000000;"> TaskState.Completed
            },
            </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> Task
            {
                Description </span>= <span style="color: #800000;">"</span><span style="color: #800000;">my initial task 3</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                AssignedPerson </span>= context.People.Single(p =&gt; p.Name == <span style="color: #800000;">"</span><span style="color: #800000;">Douglas Adams</span><span style="color: #800000;">"</span><span style="color: #000000;">)
            },
            </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> Task
            {
                Description </span>= <span style="color: #800000;">"</span><span style="color: #800000;">my initial task 4</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                AssignedPerson </span>= context.People.Single(p =&gt; p.Name == <span style="color: #800000;">"</span><span style="color: #800000;">Isaac Asimov</span><span style="color: #800000;">"</span><span style="color: #000000;">),
                State </span>=<span style="color: #000000;"> TaskState.Completed
            });
        context.SaveChanges();
    }
}</span></pre>
</div>
<p>我们所有的测试类都将从SimpleTaskSystemTestBase继承。 因此，所有测试都将通过使用具有初始数据的假数据库初始化ABP来启动。 我们还可以为此基类添加常用的帮助方法，以便使测试更容易。</p>
<p>2，我们应该创建一个专门用于测试的模块。 这是SimpleTaskSystemTestModule在这里：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">[DependsOn(
        </span><span style="color: #0000ff;">typeof</span><span style="color: #000000;">(SimpleTaskSystemDataModule),
        </span><span style="color: #0000ff;">typeof</span><span style="color: #000000;">(SimpleTaskSystemApplicationModule)
    )]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SimpleTaskSystemTestModule : AbpModule
{
        
}</span></pre>
</div>
<p>此模块仅定义依赖模块，将进行测试。</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">三、创建第一个测试</span></strong></p>
<p>我们将创建第一个单元测试来测试TaskAppService类的CreateTask方法。</p>
<p>TaskAppService类和CreateTask方法定义如下：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> TaskAppService : ApplicationService, ITaskAppService
{
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> ITaskRepository _taskRepository;
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span> IRepository&lt;Person&gt;<span style="color: #000000;"> _personRepository;
        
    </span><span style="color: #0000ff;">public</span> TaskAppService(ITaskRepository taskRepository, IRepository&lt;Person&gt;<span style="color: #000000;"> personRepository)
    {
        _taskRepository </span>=<span style="color: #000000;"> taskRepository;
        _personRepository </span>=<span style="color: #000000;"> personRepository;
    }
        
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> CreateTask(CreateTaskInput input)
    {
        Logger.Info(</span><span style="color: #800000;">"</span><span style="color: #800000;">Creating a task for input: </span><span style="color: #800000;">"</span> +<span style="color: #000000;"> input);

        </span><span style="color: #0000ff;">var</span> task = <span style="color: #0000ff;">new</span> Task { Description =<span style="color: #000000;"> input.Description };

        </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (input.AssignedPersonId.HasValue)
        {
            task.AssignedPerson </span>=<span style="color: #000000;"> _personRepository.Load(input.AssignedPersonId.Value);
        }

        _taskRepository.Insert(task);
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">...other methods</span>
}</pre>
</div>
<p>我们先创建一个测试来测试CreateTask方法。</p>
<div class="cnblogs_code">
<pre> <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> TaskAppService_Tests : SimpleTaskSystemTestBase
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> ITaskAppService _taskAppService;

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> TaskAppService_Tests()
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建被测试的类（SUT（Software Under Test） - 被测系统）</span>
            _taskAppService = LocalIocManager.Resolve&lt;ITaskAppService&gt;<span style="color: #000000;">();
        }</span><span style="color: #000000;">
        [Fact]
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Should_Create_New_Tasks()
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">准备测试</span>
            <span style="color: #0000ff;">var</span> initialTaskCount = UsingDbContext(context =&gt;<span style="color: #000000;"> context.Tasks.Count());
            </span><span style="color: #0000ff;">var</span> thomasMore = GetPerson(<span style="color: #800000;">"</span><span style="color: #800000;">Thomas More</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">运行SUT</span>
<span style="color: #000000;">            _taskAppService.CreateTask(
                </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> CreateTaskInput
                {
                    Description </span>= <span style="color: #800000;">"</span><span style="color: #800000;">my test task 1</span><span style="color: #800000;">"</span><span style="color: #000000;">
                });
            _taskAppService.CreateTask(
                </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> CreateTaskInput
                {
                    Description </span>= <span style="color: #800000;">"</span><span style="color: #800000;">my test task 2</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    AssignedPersonId </span>=<span style="color: #000000;"> thomasMore.Id
                });

            </span><span style="color: #008000;">//</span><span style="color: #008000;">检查结果</span>
            UsingDbContext(context =&gt;<span style="color: #000000;">
            {
                context.Tasks.Count().ShouldBe(initialTaskCount </span>+ <span style="color: #800080;">2</span><span style="color: #000000;">);
                context.Tasks.FirstOrDefault(t </span>=&gt; t.AssignedPersonId == <span style="color: #0000ff;">null</span> &amp;&amp; t.Description == <span style="color: #800000;">"</span><span style="color: #800000;">my test task 1</span><span style="color: #800000;">"</span>).ShouldNotBe(<span style="color: #0000ff;">null</span><span style="color: #000000;">);
                </span><span style="color: #0000ff;">var</span> task2 = context.Tasks.FirstOrDefault(t =&gt; t.Description == <span style="color: #800000;">"</span><span style="color: #800000;">my test task 2</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                task2.ShouldNotBe(</span><span style="color: #0000ff;">null</span><span style="color: #000000;">);
                task2.AssignedPersonId.ShouldBe(thomasMore.Id);
            });
        }
</span><span style="color: #0000ff;">private</span> Person GetPerson(<span style="color: #0000ff;">string</span><span style="color: #000000;"> name)
        {
            </span><span style="color: #0000ff;">return</span> UsingDbContext(context =&gt; context.People.Single(p =&gt; p.Name ==<span style="color: #000000;"> name));
        }
    }</span></pre>
</div>
<p>如前所述，我们从SimpleTaskSystemTestBase继承。 在单元测试中，我们应该创建要测试的对象。 在构造函数中，我使用LocalIocManager（依赖注入管理器）来创建一个ITaskAppService（它创建了TaskAppService，因为它实现了ITaskAppService）。 以这种方式，我摆脱了创建依赖关系的模拟实现。</p>
<p>Should_Create_New_Tasks是测试方法。 它使用xUnit的Fact属性进行装饰。 因此，xUnit了解这是一种测试方法，它运行该方法。</p>
<p>&nbsp;</p>
<p>在测试方法中，我们通常遵循AAA模式，包括三个步骤：</p>
<ol style="margin-top: 10px; margin-right: 0px; margin-bottom: 10px; padding: 0px 0px 0px 40px; border: 0px; color: #111111; font-family: 'Segoe UI', Arial, sans-serif;">
<li style="margin-top: 0px; margin-right: 0px; margin-bottom: 0px; padding-top: 0px; padding-right: 0px; padding-bottom: 0px; border: 0px; line-height: normal;"><strong style="margin: 0px; padding: 0px; border: 0px;">Arrange(安排)</strong>: 准备测试</li>
<li style="margin-top: 0px; margin-right: 0px; margin-bottom: 0px; padding-top: 0px; padding-right: 0px; padding-bottom: 0px; border: 0px; line-height: normal;"><strong style="margin: 0px; padding: 0px; border: 0px;">Act(行为)</strong>: 运行SUT（被测软件 - 实际测试代码）</li>
<li style="margin-top: 0px; margin-right: 0px; margin-bottom: 0px; padding-top: 0px; padding-right: 0px; padding-bottom: 0px; border: 0px; line-height: normal;"><strong style="margin: 0px; padding: 0px; border: 0px;">Assert(断言)</strong>: 检查并验证结果</li>
</ol>
<p>在Should_Create_New_Tasks方法中，我们将创建两个任务，一个将被分配给Thomas More。 所以，我们的三个步骤是：</p>
<ol style="margin-top: 10px; margin-right: 0px; margin-bottom: 10px; padding: 0px 0px 0px 40px; border: 0px; color: #111111; font-family: 'Segoe UI', Arial, sans-serif;">
<li style="margin-top: 0px; margin-right: 0px; margin-bottom: 0px; padding-top: 0px; padding-right: 0px; padding-bottom: 0px; border: 0px; line-height: normal;"><strong style="margin: 0px; padding: 0px; border: 0px;">Arrange</strong>:&nbsp;我们从数据库获取该人（Thomas More），以获取数据库中的Id和当前任务数量（另外，我们在构造函数中创建了TaskAppService）。</li>
<li style="margin-top: 0px; margin-right: 0px; margin-bottom: 0px; padding-top: 0px; padding-right: 0px; padding-bottom: 0px; border: 0px; line-height: normal;"><strong style="margin: 0px; padding: 0px; border: 0px;">Act</strong>:&nbsp;我们正在使用TaskAppService.CreateTask方法创建两个任务。</li>
<li style="margin-top: 0px; margin-right: 0px; margin-bottom: 0px; padding-top: 0px; padding-right: 0px; padding-bottom: 0px; border: 0px; line-height: normal;"><strong style="margin: 0px; padding: 0px; border: 0px;">Assert</strong>:&nbsp;我们正在检查任务计数是否增加2.我们还尝试从数据库获取创建的任务，以查看它们是否正确插入数据库。</li>
</ol>
<p>在这里，UsingDbContext方法可以帮助我们直接使用DbContext。 如果此测试成功，我们了解如果我们提供有效的输入，CreateTask方法可以创建任务。 此外，存储库正在工作，因为它将Tasks插入数据库。</p>
<p>&nbsp;</p>
<p>要运行测试，我们通过选择TEST \ Windows \ Test Explorer打开Visual Studio测试资源管理器：</p>
<p>&nbsp;<img src="http://images2017.cnblogs.com/blog/741594/201710/741594-20171021154818896-243771766.png" alt="" /></p>
<p>然后我们点击测试资源管理器中的&ldquo;全部运行&rdquo;链接。 它在解决方案中找到并运行所有测试：</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201710/741594-20171021154913349-1779603056.png" alt="" /></p>
<p>如上所示，我们的第一个单元测试通过。恭喜！ 如果测试或测试代码不正确，测试将失败。 假设我们已经忘记将赋值赋给给某人（要测试它，注释掉TaskAppService.CreateTask方法中的相关行）。 当我们运行测试时，它将失败：</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201710/741594-20171021155008443-280182905.png" alt="" /></p>
<p>Shouldly库使得失败的消息更清晰。 它也使写入断言变得容易。 比较xUnit的Assert.Equal与Shouldly的ShouldBe扩展方法：</p>
<div class="cnblogs_code">
<pre>Assert.Equal(thomasMore.Id, task2.AssignedPersonId); <span style="color: #008000;">//</span><span style="color: #008000;">Using xunit's Assert</span>
task2.AssignedPersonId.ShouldBe(thomasMore.Id); <span style="color: #008000;">//</span><span style="color: #008000;">Using Shouldly</span></pre>
</div>
<p>我认为第二个更容易和自然地写和阅读。 应该有很多其他的扩展方法，使我们的生活更轻松。 看到它的文档。</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">四、测试异常</span></strong></p>
<p>我想为CreateTask方法创建第二个测试。 但是，这次输入无效：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">[Fact]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Should_Not_Create_Task_Without_Description()
{
    </span><span style="color: #008000;">//</span><span style="color: #008000;">说明未设置</span>
    Assert.Throws&lt;AbpValidationException&gt;(() =&gt; _taskAppService.CreateTask(<span style="color: #0000ff;">new</span><span style="color: #000000;"> CreateTaskInput()));
}</span></pre>
</div>
<p>我希望CreateTask方法抛出AbpValidationException，如果我没有设置描述创建任务。 因为在CreateTaskInput DTO类中将描述属性标记为必需（请参阅源代码）。 如果CreateTask引发异常，则此测试成功，否则失败。 注意; 验证输入和抛出异常是由ASP.NET Boilerplate基础架构完成的。</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">五、在测试中使用存储库</span></strong></p>
<p>我将测试从一个人到另一个人分配一个任务：</p>
<div class="cnblogs_code">
<pre>        <span style="color: #008000;">//</span><span style="color: #008000;">试图将Isaac Asimov的任务分配给Thomas More</span>
<span style="color: #000000;">        [Fact]
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Should_Change_Assigned_People()
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">我们可以使用存储库而不是DbContext</span>
            <span style="color: #0000ff;">var</span> taskRepository = LocalIocManager.Resolve&lt;ITaskRepository&gt;<span style="color: #000000;">();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">获取测试数据</span>
            <span style="color: #0000ff;">var</span> isaacAsimov = GetPerson(<span style="color: #800000;">"</span><span style="color: #800000;">Isaac Asimov</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            </span><span style="color: #0000ff;">var</span> thomasMore = GetPerson(<span style="color: #800000;">"</span><span style="color: #800000;">Thomas More</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            </span><span style="color: #0000ff;">var</span> targetTask = taskRepository.FirstOrDefault(t =&gt; t.AssignedPersonId ==<span style="color: #000000;"> isaacAsimov.Id);
            targetTask.ShouldNotBe(</span><span style="color: #0000ff;">null</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">运行 SUT</span>
<span style="color: #000000;">            _taskAppService.UpdateTask(
                </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> UpdateTaskInput
                {
                    TaskId </span>=<span style="color: #000000;"> targetTask.Id,
                    AssignedPersonId </span>=<span style="color: #000000;"> thomasMore.Id
                });

            </span><span style="color: #008000;">//</span><span style="color: #008000;">检查结果</span>
<span style="color: #000000;">            taskRepository.Get(targetTask.Id).AssignedPersonId.ShouldBe(thomasMore.Id);
        }</span></pre>
</div>
<p>在这个测试中，我使用ITaskRepository执行数据库操作，而不是直接使用DbContext。 您可以使用这些方法之一或混合。</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">六、测试异步方法</span></strong></p>
<p>我们也可以使用xUnit来测试异步方法。 请参阅写入以测试PersonAppService的GetAllPeople方法的方法。 GetAllPeople方法是异步的，所以测试方法也应该是异步的：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">[Fact]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span><span style="color: #000000;"> Task Should_Get_All_People()
{
    </span><span style="color: #0000ff;">var</span> output = <span style="color: #0000ff;">await</span><span style="color: #000000;"> _personAppService.GetAllPeople();
    output.People.Count.ShouldBe(</span><span style="color: #800080;">4</span><span style="color: #000000;">);
}</span></pre>
</div>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">七、概要</span></strong></p>
<p>在本文中，我想显示简单的测试项目开发ASP.NET Boilerplate应用程序框架。 ASP.NET Boilerplate为实现测试驱动开发提供了良好的基础设施，或者简单地为您的应用程序创建了一些单元/集成测试。</p>
<p>Effort库提供了一个与EntityFramework工作良好的假数据库。 只要您使用EntityFramework和LINQ执行数据库操作，它就可以工作。 如果你有一个存储过程并且要测试它，Effort不工作。 对于这种情况，我建议使用LocalDB。</p>
<p>&nbsp;</p>