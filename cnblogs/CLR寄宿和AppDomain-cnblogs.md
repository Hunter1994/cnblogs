<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">一、CLR寄宿</span></strong></span></p>
<p>.net framework在windows平台的顶部允许。者意味着.net framework必须用windows能理解的技术来构建。所有托管模块和程序集文件必须使用windows PE文件格式，而且要么是windows exe文件，要么是DLL文件</p>
<p><strong><span style="font-size: 14pt;">1，MSCorEE.dll（垫片）</span></strong><br />①CLRCreateInstance函数在MSCorEE.dll文件中实现。&ldquo;垫片&rdquo;的工作是决定创建哪个版本的CLR（1.0、2.0、3.0的CLR代码在MSCorWks.dll文件中；版本4则在Clr.dll文件中）</p>
<p>②CLRCreateInstance函数可返回一个ICLRMetaHost接口。宿主应用程序可调用这个接口的GetRuntime函数，指定宿主要创建的CLR版本。然后，垫片将所需版本的CLR加载到宿主的进程中</p>
<p><br /><strong><span style="font-size: 14pt;">2，ICLRRuntimeHost可以做以下事情</span></strong><br />①设置宿主管理器。该诉CLR宿主想参与与涉及以下操作的决策：内存分配、线程调度/同步以及程序集加载等。宿主还可声明它想获得有关垃圾回收启动和停止以及特定操作超时的通知<br />②获取CLR管理器。告诉CLR阻止使用某些类/成员。另外，宿主能分辨哪些代码可以调试，哪些不可以，以及当特定事件（例如AppDomain卸载、CLR停止或者堆栈移除异常）发生时宿主应调用哪个方法<br />③初始化并启动CLR<br />④加载程序集并执行其中的代码<br />⑤停止CLR，阻止任何更多的托管代码在Windows进程中运行</p>
<p>&nbsp;<img src="http://images2015.cnblogs.com/blog/741594/201707/741594-20170713215458228-2105719035.png" alt="" /></p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">二、AppDomain</span></strong></p>
<p>CLR COM服务器初始化时会创建一个AppDomain。AppDomain是一组程序集的逻辑容器。CLR初始化时创建的第一个AppDomain称为&ldquo;默认AppDomain&rdquo;，这个默认的AppDomain只有在Windows进程终止时才会被销毁</p>
<p><span style="font-size: 18px;"><strong>1，AppDomain的具体功能</strong></span><br />①一个AppDomain的代码不能直接访问另一个AppDomain的代码创建的对象。<br />一个AppDomain中的代码创建了一个对象后，该对象便被该AppDomain&ldquo;拥有&rdquo;。换言之，它的生存期不能超过创建它的代码所有的AppDomain。一个AppDomain中的代码要访问另一个AppDomain的对象，只能使用&ldquo;按引用封送&rdquo;或者&ldquo;按值封送&rdquo;的予以。这就强制建立了清晰的分割和边界，因为一个AppDomain中的代码不能直接引用另一个AppDomain中的代码创建的对象。这种隔离使AppDomain能很容易地从进程中卸载，不会影响其他AppDomain正在运行的代码<br />②AppDomain可以卸载<br />CLR不支持从AppDomain中卸载特定的程序集，但可以告诉CLR卸载一个AppDomain，从而卸载该AppDomain当前包含的所有程序集<br />③AppDomain可以单独保护<br />AppDomain创建后会应用一个权限集，它决定了想这个AppDomain中运行的程序集授予最大权限，正是由于存在这样的权限，所以当宿主加载一些代码后，可以保证这些代码不会破坏（或读取）宿主本身使用的一些重要数据结构<br />④AppDomain可以单独配置<br />AppDomain创建后会关联一组配置设置。这些设置主要影响CLR在AppDomain中加载程序集的方式，设计搜索路径、版本绑定重定向、卷影复制以及加载器优化</p>
<p><span style="font-size: 18px;"><strong>2，Windows进程</strong></span></p>
<p><img src="http://images2015.cnblogs.com/blog/741594/201707/741594-20170713214704431-1124047183.png" alt="" /></p>
<p>中立的AppDomain：</p>
<p>MSCorLib.dll包含了System.Object，System.Int32以及其他所有与.NET Framework密不可分的类型</p>
<p>该Loader堆中的所有类型对象，以及为这些类型定义的JIT编译生成的所有本机代码，都会由进程中的所有AppDomain共享</p>
<p>该中立的AppDomain不能被卸载，除非终止windows进程</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">&nbsp;三、跨越AppDomain边界访问对象</span></strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Reflection;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Runtime.Remoting;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Runtime.Serialization;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ConsoleApplication7
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            Marshalling();
        }


        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Marshalling()
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">获取AppDomain引用（&ldquo;调用线程&rdquo;当前正在该AppDomain中执行）</span>
            AppDomain adCallingThreadDomain =<span style="color: #000000;"> Thread.GetDomain();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">每个AppDomain都分配了友好字符串名称（以便调试）
            </span><span style="color: #008000;">//</span><span style="color: #008000;">获取这个AppDomain的友好名称并显示它</span>
            String CallingDomainName =<span style="color: #000000;"> adCallingThreadDomain.FriendlyName;
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">默认AppDomain友好的名称={0}</span><span style="color: #800000;">"</span><span style="color: #000000;">,adCallingThreadDomain);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">获取并显示我们的AppDomain中包含了&ldquo;Main&rdquo;方法的程序集</span>
            String exeAssembly =<span style="color: #000000;"> Assembly.GetEntryAssembly().FullName;
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">包含&ldquo;Main&rdquo;方法的程序集={0}</span><span style="color: #800000;">"</span><span style="color: #000000;">, exeAssembly);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">定义局部变量来引用一个AppDomain</span>
            AppDomain ad2 = <span style="color: #0000ff;">null</span><span style="color: #000000;">;

            </span><span style="color: #008000;">//</span><span style="color: #008000;">************************************************************************************************************
            </span><span style="color: #008000;">//</span><span style="color: #008000;">************************************************************ DEMO 1：使用&ldquo;按引用封送&rdquo;进行跨AppDomain通信 ***
            </span><span style="color: #008000;">//</span><span style="color: #008000;">************************************************************************************************************</span>
            Console.WriteLine(<span style="color: #800000;">"</span><span style="color: #800000;">{0} Demo1 按引用封送</span><span style="color: #800000;">"</span><span style="color: #000000;">, Environment.NewLine);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">新建一个AppDomain（从当前AppDomain继承安全性和配置）</span>
            ad2 = AppDomain.CreateDomain(<span style="color: #800000;">"</span><span style="color: #800000;">AD #2</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">null</span>, <span style="color: #0000ff;">null</span><span style="color: #000000;">);
            MarshalByRefType mbrt </span>= <span style="color: #0000ff;">null</span><span style="color: #000000;">;


            </span><span style="color: #008000;">//</span><span style="color: #008000;">将我们的程序集加载到新AppDomain,构造一个对象，把它封送回我们的AppDomain（实际得到对一个代理的引用）</span>
            mbrt = (MarshalByRefType)ad2.CreateInstanceAndUnwrap(exeAssembly, <span style="color: #800000;">"</span><span style="color: #800000;">ConsoleApplication7.MarshalByRefType</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">Type={0}</span><span style="color: #800000;">"</span>, mbrt.GetType());<span style="color: #008000;">//</span><span style="color: #008000;">CLR在类型上撒谎了

            </span><span style="color: #008000;">//</span><span style="color: #008000;">证明得到的是对一个代理对象的引用</span>
            Console.WriteLine(<span style="color: #800000;">"</span><span style="color: #800000;">Is proxy={0}</span><span style="color: #800000;">"</span><span style="color: #000000;">, RemotingServices.IsTransparentProxy(mbrt));

            </span><span style="color: #008000;">//</span><span style="color: #008000;">看起来像是在MarshalByRefType上调用了一个方法，实则不然。
            </span><span style="color: #008000;">//</span><span style="color: #008000;">我们是在代理类型上调用了一个方法，代理是线程切换到拥有对象的那个
            </span><span style="color: #008000;">//</span><span style="color: #008000;">AppDomain,并在真实的对象上调用这个方法</span>
<span style="color: #000000;">            mbrt.SomeMethod();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">卸载新的AppDomain</span>
<span style="color: #000000;">            AppDomain.Unload(ad2);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">此时，mbrt引用了一个有效的代理对象；代理对象引用一个无效的AppDomain</span>
            <span style="color: #0000ff;">try</span><span style="color: #000000;">
            {
                mbrt.SomeMethod();
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">调用成功</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }
            </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (AppDomainUnloadedException)
            {
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">调用失败，AppDomain被卸载了</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }

            </span><span style="color: #008000;">//</span><span style="color: #008000;">************************************************************************************************************
            </span><span style="color: #008000;">//</span><span style="color: #008000;">************************************************************ DEMO 2：使用&ldquo;按值封送&rdquo;进行跨AppDomain通信 ***
            </span><span style="color: #008000;">//</span><span style="color: #008000;">************************************************************************************************************</span>
            Console.WriteLine(<span style="color: #800000;">"</span><span style="color: #800000;">{0} Demo2 按值封送</span><span style="color: #800000;">"</span><span style="color: #000000;">, Environment.NewLine);
            ad2 </span>= AppDomain.CreateDomain(<span style="color: #800000;">"</span><span style="color: #800000;">AD #2</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">null</span>, <span style="color: #0000ff;">null</span><span style="color: #000000;">);
            mbrt </span>= (MarshalByRefType)ad2.CreateInstanceAndUnwrap(exeAssembly, <span style="color: #800000;">"</span><span style="color: #800000;">ConsoleApplication7.MarshalByRefType</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">对象的方法返回所返回对象的副本
            </span><span style="color: #008000;">//</span><span style="color: #008000;">对象按值（而非按引用）封送</span>
            MarshalByValType mbvt=<span style="color: #000000;"> mbrt.MethodWithReturn();
            </span><span style="color: #008000;">//</span><span style="color: #008000;">证明得到的是对一个代理对象的引用</span>
            Console.WriteLine(<span style="color: #800000;">"</span><span style="color: #800000;">Is proxy={0}</span><span style="color: #800000;">"</span><span style="color: #000000;">, RemotingServices.IsTransparentProxy(mbvt));
            </span><span style="color: #008000;">//</span><span style="color: #008000;">看起来在MarshalByValType上调用一个方法，实际也是如此</span>
            Console.WriteLine(<span style="color: #800000;">"</span><span style="color: #800000;">Return object created </span><span style="color: #800000;">"</span> +<span style="color: #000000;"> mbvt.ToString());
            </span><span style="color: #008000;">//</span><span style="color: #008000;">卸载新的AppDomain</span>
<span style="color: #000000;">            AppDomain.Unload(ad2);
            </span><span style="color: #008000;">//</span><span style="color: #008000;">此时，mbrt引用了一个有效的x代理对象；代理对象引用一个无效的AppDomain</span>
            <span style="color: #0000ff;">try</span><span style="color: #000000;">
            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;">卸载AppDomain之后调用mbvt方法不会抛出异常</span>
                Console.WriteLine(<span style="color: #800000;">"</span><span style="color: #800000;">Return object created </span><span style="color: #800000;">"</span> +<span style="color: #000000;"> mbvt.ToString());
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">调用成功</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }
            </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (AppDomainUnloadedException)
            {
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">调用失败，AppDomain被卸载了</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }
            </span><span style="color: #008000;">//</span><span style="color: #008000;">************************************************************************************************************
            </span><span style="color: #008000;">//</span><span style="color: #008000;">************************************************************ DEMO 3：使用不可封送的类型进行跨AppDomain通信 ***
            </span><span style="color: #008000;">//</span><span style="color: #008000;">************************************************************************************************************</span>
            ad2 = AppDomain.CreateDomain(<span style="color: #800000;">"</span><span style="color: #800000;">AD #2</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">null</span>, <span style="color: #0000ff;">null</span><span style="color: #000000;">);
            mbrt </span>= (MarshalByRefType)ad2.CreateInstanceAndUnwrap(exeAssembly, <span style="color: #800000;">"</span><span style="color: #800000;">ConsoleApplication7.MarshalByRefType</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
            {
                NonMarshalableType nmt </span>= mbrt.MethodArgAndReturn(CallingDomainName);<span style="color: #008000;">//</span><span style="color: #008000;">抛出异常:未标记为可序列化</span>
<span style="color: #000000;">            }
            </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (SerializationException)
            {
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">抛出异常:未标记为可序列化</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }

            Console.ReadKey();
        }


    }


    </span><span style="color: #008000;">//</span><span style="color: #008000;">该类型的实例可跨越AppDomain的边界&ldquo;按引用封送&rdquo;</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">sealed</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MarshalByRefType : MarshalByRefObject
    {

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> MarshalByRefType()
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">{0} ctor running in {1}</span><span style="color: #800000;">"</span><span style="color: #000000;">, GetType(), Thread.GetDomain().FriendlyName);
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> SomeMethod()
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">Executing in </span><span style="color: #800000;">"</span> +<span style="color: #000000;"> Thread.GetDomain().FriendlyName);
        }

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> MarshalByValType MethodWithReturn()
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">Execute in </span><span style="color: #800000;">"</span> +<span style="color: #000000;"> Thread.GetDomain().FriendlyName);
            MarshalByValType t </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> MarshalByValType();
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> t;
        }

        </span><span style="color: #0000ff;">public</span> NonMarshalableType MethodArgAndReturn(<span style="color: #0000ff;">string</span><span style="color: #000000;"> callingDomainName)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">注意：callingDomainName是可序列化的</span>
            Console.WriteLine(<span style="color: #800000;">"</span><span style="color: #800000;">Calling from '{0}' to '{1}'.</span><span style="color: #800000;">"</span><span style="color: #000000;">, callingDomainName, Thread.GetDomain().FriendlyName);
            NonMarshalableType t</span>=<span style="color: #0000ff;">new</span><span style="color: #000000;"> NonMarshalableType();
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> t;
        }
    }


    </span><span style="color: #008000;">//</span><span style="color: #008000;">该类的实例可跨越AppDomain的边界&ldquo;按值封送&rdquo;</span>
<span style="color: #000000;">    [Serializable]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">sealed</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MarshalByValType : Object
    {
        </span><span style="color: #0000ff;">private</span> DateTime m_creationTime = DateTime.Now;<span style="color: #008000;">//</span><span style="color: #008000;">注意：DateTime是可序列化的</span>

        <span style="color: #0000ff;">public</span><span style="color: #000000;"> MarshalByValType()
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">{0} ctor running in {1}, Created no {2:D}</span><span style="color: #800000;">"</span><span style="color: #000000;">, GetType(), Thread.GetDomain().FriendlyName,
                m_creationTime);
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">string</span><span style="color: #000000;"> ToString()
        {
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> m_creationTime.ToLongDateString();
        }
    }
    </span><span style="color: #008000;">//</span><span style="color: #008000;">该类的实例不能跨AppDomain边界进行封送
    </span><span style="color: #008000;">//</span><span style="color: #008000;">[Serializable]</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">sealed</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> NonMarshalableType : Object
    {
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> NonMarshalableType()
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">Execute in </span><span style="color: #800000;">"</span> +<span style="color: #000000;"> Thread.GetDomain().FriendlyName);
        }
    }

}</span></pre>
</div>
<p>一个线程能执行一个AppDomain中的代码，再执行另一个AppDomain的代码。Thread.GetDomain()方法向CLR询问它正在执行哪个AppDomain。AppDomain的FriendlyName属性获取AppDomain的友好名称（默认AppDomain使用可执行文件的名称作为友好名称）</p>
<p><span style="font-size: 14pt;"><strong>演示1：使用&ldquo;按引用封送（Marshal-by-Refernce）&rdquo;AppDomain通信</strong></span></p>
<p><strong>1，AppDomain.CreateDomain三个参数：</strong></p>
<p><strong>friendlyName：</strong>代表新AppDomain的友好名称的一个String，</p>
<p><strong>securityInfo：</strong>一个System.Security.Polict.Evidence，是CLR用于计算AppDomain权限集的证据。本例为null，造成新的AppDomain从创建它的AppDomain继承权限集。通常，如果希望围绕AppDomain中的代码创建安全边界，可构造一个System.Security.PermssionSet对象，在其中添加希望的权限对象（实现了IPermission接口的类型实例），将得到的PermssionSet对象引用传给接受一个PermssionSet的CreateDomain方法</p>
<p><strong>info：</strong>一个System.AppDomainSetup，代表CLR为新AppDomain使用的配置设置。同样，本例为该参数传递为null，是新的AppDomain从创建它的AppDomain继承配置设置。如果希望对新AppDomain进行特殊配置，可构造一个AppDomainSetup对象，将它的各种属性（例如置文件的名称）设为你希望的值，然后将得到的AppDomainSetup对象引用传给CreateDomain方法</p>
<p><strong>2，AppDomain的CreateInstanceAndUnwrap内部实现</strong></p>
<p>①CreateInstanceAndUnwrap方法导致调用线程从当前AppDomain切换到新的AppDomain</p>
<p>②线程将指定的程序集加载到新AppDomain中，并扫描程序集的类型定义元数据表，查找指定类型</p>
<p>③找到类型后，线程调用该类型的无参构造器（CreateInstanceAndUnwrap方法一些重载方法允许在调用类型的构造器时传递实参）</p>
<p>④现在线程又切换回默认的AppDomain，时CreateInstanceAndUnwrap能返回对新类型对象的引用</p>
<p><strong>3，&ldquo;按引用封送&rdquo;的具体含义</strong></p>
<p>当CreateInstanceAndUnwrapA线它封送的一个对象的类型派生自MarshalByRefObject时，CLR就会跨AppDomain边界按引用封送</p>
<p>①源AppDomain想向目标AppDomain发送或返回对象引用时，CLR会在目标AppDomain的Loader堆中定义一个代理类型，代理类型是用原始类型的元数据定义的，所以它看起来和原始类型完全一样，有完全一样的实例成员（属性、事件和方法）。实例字段不会成为（代理）类型的一部分。代理类型确定定义了几个（自己的）实例字段，但这些字段和原始类型的不一致。相反，这些字段只是指出哪个AppDomain&ldquo;拥有&rdquo;真实的对象，以及如何在拥有（对象的）AppDomain中找到真实的对象</p>
<p>②在目标AppDomain中定义好这个代理类型之后，CreateInstanceAndUnwrapA方法就会创建代理类型的实例，初始化它的字段来标识源AppDomain和真实对象，然后将这个代理对象的引用返回给目标AppDomain（调用该对象的GetType方法，他会向你撒谎）</p>
<p>③应用程序使用代理调用SomeMethod方法。由于mbrt变量用代理对象，所以会调用由代理实现的SomeMethod。代理的实现利用代理对象中的信息字段，将调用线程从默认AppDomain切换至新AppDomain。现在，该线程的任何行动都在新AppDomain的安全策略和配置设置下运行。线程接着使用代理对象的GCHandle字段查找新AppDomain中的真实对象，并用真实对象调用真实的SomeMethod方法</p>
<p>④AppDomain类的公共静态方法Unload方法会强制CLR卸载指定的AppDomain（包括加载到其中的所有程序集），并强制执行一次垃圾回收，已释放有卸载的AppDomain中的代码创建的所有对象，这时，默认AppDomain的mbrt变量仍然引用一个有效的代理对象，但代理对象已经不再引用一个有效的AppDomain</p>
<p>⑤使用&ldquo;按引用封送&rdquo;的语义进行跨AppDomain边界的对象访问，会产生一些性能上的开销。所以一般应该尽量少用这个功能</p>
<p><strong>4，MarshalByRefObject派生</strong></p>
<p>从MarshalByRefObject派生的类型可定义实例字段。但这些实例字段不会成为代理类型的一部分，也不会包含在代理对象中</p>
<p>对派生自的MarshalByRefObject类型的实例字段进行读写时，JIT编译器会自动生成代码，分别调用system.object的FieldGetter或FieldSetter来使用代理对象。这些方法利用反射机制获取或设置字段值，性能很差</p>
<p>派生自MarshalByRefObject的类型真的应该避免定义任何静态成员</p>
<p>&nbsp;</p>
<p><span style="font-size: 14pt;"><strong>演示2：使用&ldquo;按值封送（Marshal-by-Value）&rdquo;AppDomain通信</strong></span></p>
<p>&nbsp;CLR在目标AppDomain中精确的赋值了源对象。然后MethodWithReturn方法返回对这个副本的引用。源AppDomain中的对象和目标AppDomain中的对象有了独立的生存期，它们的状态也可以独立地更改</p>
<p>&nbsp;</p>
<p><strong><span style="font-size: 14pt;">演示3：使用不可封送的类型跨AppDomain通信</span></strong></p>
<p>&nbsp;由于NonMarshalableType不是从System. MarshalByRefObject中派生的，也没有用[Serializable]定制特性进行标记，所以不允许MethodArgAndReturn按引用或按值封送对象--对象完全不能跨越AppDomain边界进行封送</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">四、卸载AppDomain</span></strong></span></p>
<p>①CLR挂起进程中执行过托管代码的所有线程</p>
<p>②CLR检查所有线程栈，查看哪些线程正在执行要卸载的AppDomain中的代码，或者哪些线性会在某个时候返回至要卸载的AppDomain。任何栈上有要卸载的AppDomain，CLR都会强制对应的线程抛出一个ThreadAbortException(同时恢复线程的执行)。这将导致线程展开，并执行遇到的所有finally块以清理资源。如果没有代码捕捉ThreadAbortException，它最终会成为未处理的异常，CLR会&ldquo;吞噬&rdquo;这个异常，线程会终止，但进程可继续执行</p>
<p>③当第2步发现的所有线程都离开AppDomain后，CLR遍历堆，为引用了&ldquo;由于卸载的AppDomain创建的对象&rdquo;的每个代理对象都设置一个标志（flag）、这些代理对象现在知道他们引用的真实对象已经不存在了。现在，任何代码在无效的代理对象上调用方法都会抛出AppDomainUnloadedException异常</p>
<p>④CLR强制垃圾回收，回收由已卸载的AppDomain创建的任何对象的内存。这些对象的Finalze方法被调用，是对象由机会正确清理他们占用的资源</p>
<p>⑤CLR恢复剩余所有线程的执行。调用AppDomain.Unload方法的线程将继续运行；对于AppDomain.Unload的调用是同步进行的</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">五、监视AppDomain</span></strong></span></p>
<p>1，AppDomain的几条MonitoringEnabled属性设置为true显式打开监控。打开监控后，代码可查询AppDomain类提供的以下4个属性</p>
<p>①MonitoringSurvivedProcessMemorySize:这个Int64静态属性返回由当前CLR实例控制的所有AppDomain使用的字节数。这个数字值保证在上一次垃圾回收时时准确的</p>
<p>②MonitoringTotalAllocatedMemorySize:这个Int64实例属性返回特定AppDomain已分配的字节数。这个数字只保证在上一次垃圾回收时是准确的</p>
<p>③MonitoringSuvivedMemorySize:这个Int64实例属性返回特定AppDomain当前正在使用的字节数。这个数字只保证在上一次垃圾回收时是准确的</p>
<p>④MonitoringTotalProcessorTime:这个TimeSpan实例返回特定AppDomain的CPU占用率</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('352b8599-19db-4220-a024-6836897d426e')"><img id="code_img_closed_352b8599-19db-4220-a024-6836897d426e" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_352b8599-19db-4220-a024-6836897d426e" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('352b8599-19db-4220-a024-6836897d426e',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_352b8599-19db-4220-a024-6836897d426e" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ConsoleApplication8
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            AppDomainResourceMonitoring();
            Console.WriteLine(Environment.TickCount);
            Console.ReadLine();
        }
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> AppDomainResourceMonitoring()
        {
            </span><span style="color: #0000ff;">using</span> (<span style="color: #0000ff;">new</span> AppDomainMonitorDalte(<span style="color: #0000ff;">null</span><span style="color: #000000;">))
            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;">分配在回收时能存活的约10MB</span>
                <span style="color: #0000ff;">var</span> list = <span style="color: #0000ff;">new</span> List&lt;<span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">();
                </span><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> x = <span style="color: #800080;">0</span>; x &lt; <span style="color: #800080;">1000</span>; x++<span style="color: #000000;">)
                {
                    list.Add(</span><span style="color: #0000ff;">new</span> <span style="color: #0000ff;">byte</span>[<span style="color: #800080;">1000</span><span style="color: #000000;">]);
                }
                </span><span style="color: #008000;">//</span><span style="color: #008000;">分配在回收时存活不了的约20MB</span>
                <span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> x = <span style="color: #800080;">0</span>; x &lt; <span style="color: #800080;">2000</span>; x++<span style="color: #000000;">)
                {
                    </span><span style="color: #0000ff;">new</span> <span style="color: #0000ff;">byte</span>[<span style="color: #800080;">10000</span><span style="color: #000000;">].GetType();
                }

                </span><span style="color: #008000;">//</span><span style="color: #008000;">保持CPU工作约5秒</span>
                <span style="color: #0000ff;">var</span> stop = Environment.TickCount + <span style="color: #800080;">5000</span><span style="color: #000000;">;
                </span><span style="color: #0000ff;">while</span> (Environment.TickCount &lt;<span style="color: #000000;"> stop) ;

            }

        }
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> AppDomainMonitorDalte : IDisposable
    {
        </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> AppDomain m_appdomain;
        </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> TimeSpan m_thisADCpu;
        </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> Int64 m_thisAdMemoryInUse;
        </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> Int64 m_thisADMemoryAllocated;

        </span><span style="color: #0000ff;">static</span><span style="color: #000000;"> AppDomainMonitorDalte()
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">确定已打开AppDomain监视</span>
            AppDomain.MonitoringIsEnabled = <span style="color: #0000ff;">true</span><span style="color: #000000;">;
        }

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> AppDomainMonitorDalte(AppDomain ad)
        {
            m_appdomain </span>= ad ??<span style="color: #000000;"> AppDomain.CurrentDomain;
            m_thisADCpu </span>=<span style="color: #000000;"> m_appdomain.MonitoringTotalProcessorTime;
            m_thisAdMemoryInUse </span>=<span style="color: #000000;"> m_appdomain.MonitoringSurvivedMemorySize;
            m_thisADMemoryAllocated </span>=<span style="color: #000000;"> m_appdomain.MonitoringTotalAllocatedMemorySize;
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Dispose()
        {
            GC.Collect();
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">AppDomain友好名称={0}，CPU={1}ms</span><span style="color: #800000;">"</span><span style="color: #000000;">, m_appdomain.FriendlyName,
                (m_appdomain.MonitoringTotalProcessorTime </span>-<span style="color: #000000;"> m_thisADCpu).TotalMilliseconds);
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">Allocated {0:N0} bytes of which {1:N0} survied GCs</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                m_appdomain.MonitoringTotalAllocatedMemorySize </span>-<span style="color: #000000;"> m_thisADMemoryAllocated,
                m_appdomain.MonitoringSurvivedMemorySize </span>-<span style="color: #000000;"> m_thisAdMemoryInUse);
        }



    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">六、AppDomain FirstCance异常通知</span></strong></span></p>
<p>为AppDomain的实例事件FirstChanceException添加一个委托就可以了<br /><span style="font-size: 14pt;"><strong>1，CLR如何处理异常：</strong></span><br />①异常首次抛出时，CLR调用向抛出异常的AppDomain登记的所有FirstChanceException回调方法。<br />②然后。CLR查找栈上同一个AppDomain中的任何catch块，有一个catch块能处理异常，则异常处理完成，将继续执行<br />③如果AppDomain中没有一个catch块能处理异常，则CLR沿着栈向上来到调用AppDomain，再次抛出同一异常对象（序列化和反序列化之后）<br />④这个感觉抛出一个新的异常，CLR调用当前AppDomain登记的所有FirstChanceException回调方法<br />⑤这个过程会一直执行，知道抵达线程栈顶部。如果异常还未处理，则进程终止<br />	</p>