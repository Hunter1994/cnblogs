<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">一、程序集加载</span></strong></span></p>
<p><strong>1，根据程序集名称查找程序集</strong></p>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Assembly
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> Assembly Load(AssemblyName assemblyRef);
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> Assembly Load(<span style="color: #0000ff;">string</span><span style="color: #000000;"> assemblyString);
        </span><span style="color: #008000;">//</span><span style="color: #008000;">未列出不常用的Load重载</span>
    }</pre>
</div>
<div class="cnblogs_code">
<pre>Assembly.Load(<span style="color: #800000;">"</span><span style="color: #800000;">ConsoleApplication2</span><span style="color: #800000;">"</span>);,</pre>
</div>
<p><strong>2，根据程序集文件路径名（包含扩展名）查找程序集</strong></p>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Assembly
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> Assembly LoadFrom(<span style="color: #0000ff;">string</span><span style="color: #000000;"> path);
        </span><span style="color: #008000;">//</span><span style="color: #008000;">未列出不常用的LoadFrom重载</span>
    }</pre>
</div>
<div class="cnblogs_code">
<pre>Assembly.LoadFrom(<span style="color: #800000;">"</span><span style="color: #800000;">ConsoleApplication2.exe</span><span style="color: #800000;">"</span>);</pre>
</div>
<p><strong>3，加载程序集时，确保程序集中的任何代码不会执行</strong></p>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Assembly
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> Assembly ReflectionOnlyLoadFrom(<span style="color: #0000ff;">string</span><span style="color: #000000;"> assemblyFile);
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> Assembly ReflectionOnlyLoad(<span style="color: #0000ff;">string</span><span style="color: #000000;"> assemblyFile);
        </span><span style="color: #008000;">//</span><span style="color: #008000;">未列出不常用的ReflectionOnlyLoad重载</span>
    }</pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">二、反射的性能</span></strong></span></p>
<p><span style="font-size: 14pt;"><strong>1，反射的两个缺点</strong></span><br />①反射造成编译时无法保证类型安全性。由于反射严重依赖字符串，所以会丧失编译时的类型安全性。例如，执行Type.GetType("int")；要求通过反射在程序集中查找名为&ldquo;int&rdquo;类型，代理会通过编译，但是在运行时会返回null，因为CLR只知&ldquo;System.Int32&rdquo;不知道&ldquo;int&rdquo;<br />②反射速度慢。使用反射是，类型及其成员的名称在编译时未知。你需要用字符串名称标识每个类型及其成员，然后再运行时发现他们。也就是说，使用System.Reflection命名空间中的类型扫描程序集的元数据时，反射机制会不停地执行字符串搜索。通常，字符串搜索执行的是不区分大小写的比较，这会进一步影响速度<br />③用反射调用方法时，首先必须将实参打包成数组。在内部，反射必须将这些实参解包到线程栈上。此外，在调用方法前，CLR必须检查实参具有正确的数据类型。最后，CLR必须确保调用者有正确的安全权限来访问被调用的成员</p>
<p><br /><strong><span style="font-size: 14pt;">2，利用一下两种技术之一开发应用程序来动态发现和构造类型实例</span></strong><br />①让类型从编译时一直的基类型派生。在运行时构造派生类型的实例，将对它的引用方到基类的变量中（利用转型），再调用基类定义的虚方法<br />②让类型实现编译时已知的接口。在运行时构造类型的实例，将对它的引用放到接口类型的变量中利用转型（），在调用接口定义的方法</p>
<p><br /><strong><span style="font-size: 14pt;">3，发现程序集中定义的类型</span></strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ConsoleApplication2
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">显示将程序集加载到这个AppDomain中</span>
            Assembly a = Assembly.Load(<span style="color: #800000;">"</span><span style="color: #800000;">ConsoleApplication2</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            </span><span style="color: #0000ff;">foreach</span> (<span style="color: #0000ff;">var</span> exportedType <span style="color: #0000ff;">in</span><span style="color: #000000;"> a.ExportedTypes)
            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;">显示访问修饰符为public的类型</span>
<span style="color: #000000;">                Console.WriteLine(exportedType.FullName);
            }
            Console.ReadKey();
        }
    }
}</span></pre>
</div>
<p><strong><span style="font-size: 14pt;">4，类型对象的准确含义</span></strong></p>
<p>①System.Type类型提供了静态GetType方法的几个重载版本。所有版本都接受一个String参数。字符串必须指定类型的全名（包括它的命名空间）。找到，则返回对恰当的Type对象的引用。没有找到，则就检查MSCorLib.dll定义类型，如果还是没找到，则为null或抛出System.TyprLoadException。可向GetType传递限定程序集的类型字符创，比如&ldquo;System.Int32,mscorlib,Version=4.0.0.0,Culture=neutral,PublicKeyToken=677a5c61934e098&rdquo;，GetType方法会在指定程序集中查找类型（如果有必要会加载程序集）</p>
<p>②System.Type类型提供静态ReflectionOnlyGetType方法。该方法与上一条提到的GetType方法在行为上相似，只是类型会以&ldquo;仅反射&rdquo;的方式加载，不能执行</p>
<p>③System.TypeInfo类型提供了实例成员DeclaredNestedTypes和GetDeclaredNestedType</p>
<p>④System.Reflection.Assemble类型提供了实例成员GetType，DefinedTypes和ExportedTypes</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> t = Type.GetType(<span style="color: #800000;">"</span><span style="color: #800000;">ConsoleApplication2.Program</span><span style="color: #800000;">"</span><span style="color: #000000;">);
Console.WriteLine(t </span>== <span style="color: #0000ff;">null</span> ? <span style="color: #800000;">"</span><span style="color: #800000;">未找到</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">找到</span><span style="color: #800000;">"</span>);</pre>
</div>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> SomeMethod(<span style="color: #0000ff;">object</span><span style="color: #000000;"> o)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">GetType在运行时返回对象的类型（晚期绑定）
            </span><span style="color: #008000;">//</span><span style="color: #008000;">typeof返回指定的类型（早起绑定）</span>
            <span style="color: #0000ff;">if</span> (o.GetType() == <span style="color: #0000ff;">typeof</span><span style="color: #000000;"> (FileInfo))
            {
            }
        }</span></pre>
</div>
<p>上述代码的第一个if语句检查变量o是否引用了FileInfo类型的对象；它不检查o是否引用从FileInfo类型派生的对象（<span style="color: #ff0000;">使用is/as操作符会检查派生对象</span>）</p>
<p>使用Type对象的GetTypeInfo方法获取对类型的更多控制</p>
<p><strong><span style="font-size: 14pt;">5，构造类型的实例</span></strong><br />①System.Activator的CreateInstance方法<br />②System.Activator的CreateInstanceFrom方法<br />他与CreateInstance的行为相似，只是必须通过字符串来指出类型及其程序集。程序集用Assembly的LoadFrom（而非Load）方法加载到调用AppDomain中。由于都不接受Type参数，所以返回的都是一个ObjectHandle对象引用，必须调用Unwrap方法进行具体化<br />③System. AppDomain的方法<br />AppDomain类型提供了4个用于构造类型实例的实例方法（每个都有几个重载版本），包括CreateInstance，CreateInstanceAndUnwrap，CreateInstanceForm和CreateInstanceFromAndUnwrap。这些方法的行为和Activator类的方法相似，区别在于它们都是实例方法，允许指定哪个AppDomain中构造对象。另外，带Unwrap后缀的方法还能简化操作，必须执行额外的方法调用<br />④System.Reflection.ConstructorInfo的Invoke实例方法<br />使用一个Type对象引用，可以绑定到一个特定的构造器，并获取对构造器的ConstructorInfo对象的引用。然后，可利用ConstructorInfo对象引用来调用它的Incoke方法。类型总是在调用AppDomain中创建，返回的是对新对象的引用<br />⑤创建数组<br />创建数组需要调用Array的静态CreateInstance方法<br />⑥创建委托<br />创建委托需要调用MethodInfo的静态CreateDelegate方法<br />⑦构造泛型类型</p>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">获取对泛型类型的类型对象引用</span>
            <span style="color: #0000ff;">var</span> openType = <span style="color: #0000ff;">typeof</span> (Dictionary&lt;,&gt;<span style="color: #000000;">);
            </span><span style="color: #008000;">//</span><span style="color: #008000;">使用TKey=String、TValue=Int32封闭泛型类型</span>
            <span style="color: #0000ff;">var</span> closedType = openType.MakeGenericType(<span style="color: #0000ff;">typeof</span> (<span style="color: #0000ff;">string</span>), <span style="color: #0000ff;">typeof</span><span style="color: #000000;"> (Int32));
            </span><span style="color: #008000;">//</span><span style="color: #008000;">构造封闭类型的实例</span>
            <span style="color: #0000ff;">var</span> o =<span style="color: #000000;"> Activator.CreateInstance(closedType);
            Console.WriteLine(o.GetType());

            Console.ReadKey();
        }</span></pre>
</div>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">&nbsp;三、设置支持加载项的引用程序</span></strong></span></p>
<p>1，HostSDK.dll接口设计</p>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IAddIn
    {
        </span><span style="color: #0000ff;">string</span> DoSomething(<span style="color: #0000ff;">int</span><span style="color: #000000;"> x);
    }</span></pre>
</div>
<p>2，加载项AddInTypes.dll设计</p>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> AddIn_A : IAddIn
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> DoSomething(<span style="color: #0000ff;">int</span><span style="color: #000000;"> x)
        {
            </span><span style="color: #0000ff;">return</span> <span style="color: #800000;">"</span><span style="color: #800000;">AddIn_A:</span><span style="color: #800000;">"</span> +<span style="color: #000000;"> x;
        }
    }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> AddIn_B : IAddIn
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> DoSomething(<span style="color: #0000ff;">int</span><span style="color: #000000;"> x)
        {
            </span><span style="color: #0000ff;">return</span> <span style="color: #800000;">"</span><span style="color: #800000;">AddIn_B:</span><span style="color: #800000;">"</span> +<span style="color: #000000;"> x;
        }
    }</span></pre>
</div>
<p>3，可扩展应用程序设计</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.IO;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Reflection;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> HostSDK;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> Host
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">查找宿主EXE文件所在的目录(例如：F:/../../bin/Debug)</span>
            <span style="color: #0000ff;">string</span> AddInDir =<span style="color: #000000;"> Path.GetDirectoryName(Assembly.GetEntryAssembly().Location);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">假定加载项程序集和宿主EXE文件在一个目录(例如：F:/../../bin/Debug/HostSDK.dll)</span>
            <span style="color: #0000ff;">var</span> AddInAssemblies = Directory.EnumerateFiles(AddInDir, <span style="color: #800000;">"</span><span style="color: #800000;">*.dll</span><span style="color: #800000;">"</span><span style="color: #000000;">);
           
            </span><span style="color: #0000ff;">var</span> AddInTypes = <span style="color: #0000ff;">from</span> file <span style="color: #0000ff;">in</span><span style="color: #000000;"> AddInAssemblies
                             let assembly </span>=<span style="color: #000000;"> Assembly.LoadFrom(file)
                </span><span style="color: #0000ff;">from</span> t <span style="color: #0000ff;">in</span> assembly.ExportedTypes<span style="color: #008000;">//</span><span style="color: #008000;">公开到处的类型
                </span><span style="color: #008000;">//</span><span style="color: #008000;">如果类型实现了IAddIn接口，该接口就可由宿主使用</span>
                <span style="color: #0000ff;">where</span> t.IsClass &amp;&amp; <span style="color: #0000ff;">typeof</span><span style="color: #000000;"> (IAddIn).GetTypeInfo().IsAssignableFrom(t.GetTypeInfo())
                </span><span style="color: #0000ff;">select</span><span style="color: #000000;"> t;
            </span><span style="color: #0000ff;">foreach</span> (<span style="color: #0000ff;">var</span> addInType <span style="color: #0000ff;">in</span><span style="color: #000000;"> AddInTypes)
            {
                IAddIn ai </span>=<span style="color: #000000;"> (IAddIn) Activator.CreateInstance(addInType);
                Console.WriteLine(ai.DoSomething(</span><span style="color: #800080;">5</span><span style="color: #000000;">));
            }

            Console.ReadKey();
        }
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">四、使用反射发现类型的成员</span></strong></span></p>
<p><strong><span style="font-size: 14pt;">&nbsp;1，发现类型的成员</span></strong></p>
<p><img src="http://images2015.cnblogs.com/blog/741594/201707/741594-20170722151919793-631192461.jpg" alt="" width="548" height="411" /></p>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
          
            </span><span style="color: #008000;">//</span><span style="color: #008000;">遍历这个AppDomain中加载的所有程序集</span>
            Assembly[] assemblies =<span style="color: #000000;"> AppDomain.CurrentDomain.GetAssemblies();

            </span><span style="color: #0000ff;">foreach</span> (Assembly a <span style="color: #0000ff;">in</span><span style="color: #000000;"> assemblies)
            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;">查找程序集中的类型</span>
                <span style="color: #0000ff;">foreach</span> (Type t <span style="color: #0000ff;">in</span><span style="color: #000000;"> a.ExportedTypes)
                {
                    </span><span style="color: #008000;">//</span><span style="color: #008000;">发现类型的成员</span>
                    <span style="color: #0000ff;">foreach</span> (MemberInfo mi <span style="color: #0000ff;">in</span><span style="color: #000000;"> t.GetTypeInfo().DeclaredMembers)
                    {
                        </span><span style="color: #0000ff;">if</span> (mi <span style="color: #0000ff;">is</span> Type)<span style="color: #008000;">//</span><span style="color: #008000;">嵌套类型</span>
                        <span style="color: #0000ff;">if</span> (mi <span style="color: #0000ff;">is</span> FieldInfo)<span style="color: #008000;">//</span><span style="color: #008000;">字段</span>
                        <span style="color: #0000ff;">if</span> (mi <span style="color: #0000ff;">is</span> MethodInfo)<span style="color: #008000;">//</span><span style="color: #008000;">方法</span>
                        <span style="color: #0000ff;">if</span> (mi <span style="color: #0000ff;">is</span> ConstructorInfo)<span style="color: #008000;">//</span><span style="color: #008000;">构造函数</span>
                        <span style="color: #0000ff;">if</span> (mi <span style="color: #0000ff;">is</span> PropertyInfo)<span style="color: #008000;">//</span><span style="color: #008000;">属性</span>
                        <span style="color: #0000ff;">if</span> (mi <span style="color: #0000ff;">is</span> EventInfo)<span style="color: #008000;">//</span><span style="color: #008000;">事件</span>
<span style="color: #000000;">                    }
                }
            }
        }</span></pre>
</div>
<p>&nbsp;MemberInfo的所有派生类型都通用的属性和方法</p>
<table class="MsoTableGrid" style="border-width: initial; border-style: none; border-color: initial; height: 223px; width: 775px;" border="1" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td style="width: 142pt; border-width: 1pt; border-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="189">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">成员名称</span></p>
</td>
<td style="width: 142.05pt; border-top-width: 1pt; border-right-width: 1pt; border-bottom-width: 1pt; border-top-color: windowtext; border-right-color: windowtext; border-bottom-color: windowtext; border-left: none; padding: 0cm 5.4pt;" valign="top" width="189">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">成员类型</span></p>
</td>
<td style="width: 142.05pt; border-top-width: 1pt; border-right-width: 1pt; border-bottom-width: 1pt; border-top-color: windowtext; border-right-color: windowtext; border-bottom-color: windowtext; border-left: none; padding: 0cm 5.4pt;" valign="top" width="189">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">说明</span></p>
</td>
</tr>
<tr>
<td style="width: 142pt; border-right-width: 1pt; border-bottom-width: 1pt; border-left-width: 1pt; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-top: none; padding: 0cm 5.4pt;" valign="top" width="189">
<p class="MsoNormal"><span lang="EN-US">Name</span></p>
</td>
<td style="width: 142.05pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="189">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">一个</span><span lang="EN-US">String</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">属性</span></p>
</td>
<td style="width: 142.05pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="189">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">返回成员名称</span></p>
</td>
</tr>
<tr>
<td style="width: 142pt; border-right-width: 1pt; border-bottom-width: 1pt; border-left-width: 1pt; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-top: none; padding: 0cm 5.4pt;" valign="top" width="189">
<p class="MsoNormal"><span lang="EN-US">Declaring</span><span lang="EN-US">Type</span></p>
</td>
<td style="width: 142.05pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="189">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">一个</span><span lang="EN-US">Type</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">属性</span></p>
</td>
<td style="width: 142.05pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="189">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">返回声明成员的</span><span lang="EN-US">Type</span></p>
</td>
</tr>
<tr>
<td style="width: 142pt; border-right-width: 1pt; border-bottom-width: 1pt; border-left-width: 1pt; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-top: none; padding: 0cm 5.4pt;" valign="top" width="189">
<p class="MsoNormal"><span lang="EN-US">Module</span></p>
</td>
<td style="width: 142.05pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="189">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">一个</span><span lang="EN-US">Module</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">属性</span></p>
</td>
<td style="width: 142.05pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="189">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">返回声明成员的</span><span lang="EN-US">Module</span></p>
</td>
</tr>
<tr>
<td style="width: 142pt; border-right-width: 1pt; border-bottom-width: 1pt; border-left-width: 1pt; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-top: none; padding: 0cm 5.4pt;" valign="top" width="189">
<p class="MsoNormal"><span lang="EN-US">CustomAttributes</span></p>
</td>
<td style="width: 142.05pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="189">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">该属性返回一个</span><span lang="EN-US">IEnumerable&lt;CustomAttributeData&gt;</span></p>
</td>
<td style="width: 142.05pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="189">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">返回一个集合，其中每个元素都标识了应用于该成员的一个定制特性的实例。定制特性可应用于如何成员。虽然</span><span lang="EN-US">Assembly</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">不从</span><span lang="EN-US">MemberInfo</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">派生，但它提供了可用于程序集的相同属性</span></p>
</td>
</tr>
</tbody>
</table>
<p><img src="http://images2015.cnblogs.com/blog/741594/201707/741594-20170722153429246-544712836.jpg" alt="" width="482" height="361" /></p>
<p>&nbsp;</p>
<p><strong><span style="font-size: 14pt;">2，调用类型成员</span></strong></p>
<table class="MsoTableGrid" style="border-width: initial; border-style: none; border-color: initial; height: 291px; width: 788px;" border="1" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td style="width: 90.45pt; border-width: 1pt; border-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="121">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">成员类型</span></p>
</td>
<td style="width: 335.65pt; border-top-width: 1pt; border-right-width: 1pt; border-bottom-width: 1pt; border-top-color: windowtext; border-right-color: windowtext; border-bottom-color: windowtext; border-left: none; padding: 0cm 5.4pt;" valign="top" width="448">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">调用（</span><span lang="EN-US">Invoke</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">）成员而需要调用（</span><span lang="EN-US">call</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">）的方法</span></p>
</td>
</tr>
<tr>
<td style="width: 90.45pt; border-right-width: 1pt; border-bottom-width: 1pt; border-left-width: 1pt; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-top: none; padding: 0cm 5.4pt;" valign="top" width="121">
<p class="MsoNormal"><span lang="EN-US">FieldInfo</span></p>
</td>
<td style="width: 335.65pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="448">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">调用</span><span lang="EN-US">GetValue</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">获取字段的值</span></p>
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">调用</span><span lang="EN-US">SetValue</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">设置字段的值</span></p>
</td>
</tr>
<tr>
<td style="width: 90.45pt; border-right-width: 1pt; border-bottom-width: 1pt; border-left-width: 1pt; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-top: none; padding: 0cm 5.4pt;" valign="top" width="121">
<p class="MsoNormal"><span lang="EN-US">ConstructorInfo</span></p>
</td>
<td style="width: 335.65pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="448">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">调用</span><span lang="EN-US">Invoke</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">构造类型的实例并调用构造器</span></p>
</td>
</tr>
<tr>
<td style="width: 90.45pt; border-right-width: 1pt; border-bottom-width: 1pt; border-left-width: 1pt; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-top: none; padding: 0cm 5.4pt;" valign="top" width="121">
<p class="MsoNormal"><span lang="EN-US">MethodInfo</span></p>
</td>
<td style="width: 335.65pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="448">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">调用</span><span lang="EN-US">Invoke</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">来调用类型的方法</span></p>
</td>
</tr>
<tr>
<td style="width: 90.45pt; border-right-width: 1pt; border-bottom-width: 1pt; border-left-width: 1pt; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-top: none; padding: 0cm 5.4pt;" valign="top" width="121">
<p class="MsoNormal"><span lang="EN-US">PropertyInfo</span></p>
</td>
<td style="width: 335.65pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="448">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">调用</span><span lang="EN-US">GetValue</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">来调用的属性的</span><span lang="EN-US">get</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">访问器方法</span></p>
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">调用</span><span lang="EN-US">SetValue</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">来调用属性的</span><span lang="EN-US">set</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">访问器方法</span></p>
</td>
</tr>
<tr>
<td style="width: 90.45pt; border-right-width: 1pt; border-bottom-width: 1pt; border-left-width: 1pt; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-top: none; padding: 0cm 5.4pt;" valign="top" width="121">
<p class="MsoNormal"><span lang="EN-US">EventInfo</span></p>
</td>
<td style="width: 335.65pt; border-top: none; border-left: none; border-bottom-width: 1pt; border-bottom-color: windowtext; border-right-width: 1pt; border-right-color: windowtext; padding: 0cm 5.4pt;" valign="top" width="448">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">调用</span><span lang="EN-US">AddEventHandler</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">来调用事件的</span><span lang="EN-US">add</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">访问器方法</span></p>
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">调用</span><span lang="EN-US">RemoveEventHandler</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">来调用事件的</span><span lang="EN-US">remove</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">访问器方法</span></p>
</td>
</tr>
</tbody>
</table>
<p><span style="color: #ff0000;">BindToMemberThenInvokeTheMember</span>：方法演示了如何绑定到成员并调用它</p>
<p><span style="color: #ff0000;">BindToMemberCreateDelegateToMemberThenInvokeThenMember</span>：方法演示了如何绑定到一个对象或成员，然后创建一个委托来引用对象或成员。通过委托来调用的速度很快。如果需要在相容的对象上多次调用相同的成员，这个技术的性能比上一个好</p>
<p><span style="color: #ff0000;">UseDynamicToBindAndInvokeTheMember</span>：方法演示了如何利用C#的dynamic基元类型简化成员访问语法。此外，在相同类型的不同对象上调用相同成员时，这个技术还能提供不错的性能，因为针对每个类型，绑定都只会发生一次。而且可以缓存起来，以后多次调用的速度回非常快。用这个技术也可以调用不容类型的对象的成员</p>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">internal</span> <span style="color: #0000ff;">sealed</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SomeType
    {
        </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> Int32 m_someField;
        </span><span style="color: #0000ff;">public</span> SomeType(<span style="color: #0000ff;">ref</span> Int32 x){x *= <span style="color: #800080;">2</span><span style="color: #000000;">;}
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">string</span> ToString(){<span style="color: #0000ff;">return</span><span style="color: #000000;"> m_someField.ToString();}
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Int32 SomeProp
        {
            </span><span style="color: #0000ff;">get</span> { <span style="color: #0000ff;">return</span><span style="color: #000000;"> m_someField;;}
            </span><span style="color: #0000ff;">set</span><span style="color: #000000;">
            {
                </span><span style="color: #0000ff;">if</span>(value&lt;<span style="color: #800080;">1</span>)<span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> ArgumentOutOfRangeException(<span style="color: #800000;">"</span><span style="color: #800000;">value</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                m_someField </span>=<span style="color: #000000;"> value;
            }

        }
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">event</span><span style="color: #000000;"> EventHandler SomeEvent;
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> NoCompilerWarnings(){SomeEvent.ToString();}
    }</span></pre>
</div>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">internal</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ReflectionExtensions
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;">这个辅助扩展方法简化了创建委托的语法</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> TDelegate CreateDelegate&lt;TDelegate&gt;(<span style="color: #0000ff;">this</span> MethodInfo mi, <span style="color: #0000ff;">object</span> target = <span style="color: #0000ff;">null</span><span style="color: #000000;">)
        {
            </span><span style="color: #0000ff;">return</span> (TDelegate) (<span style="color: #0000ff;">object</span>) mi.CreateDelegate(<span style="color: #0000ff;">typeof</span><span style="color: #000000;"> (TDelegate), target);
        }
    }</span></pre>
</div>
<div class="cnblogs_code">
<pre> <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            Type t </span>= <span style="color: #0000ff;">typeof</span><span style="color: #000000;"> (SomeType);
            BindToMemberThenInvokeTheMember(t);
            BindToMemberCreateDelegateToMemberThenInvokeThenMember(t);
            UseDynamicToBindAndInvokeTheMember(t);
            Console.ReadKey();
        }

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> BindToMemberThenInvokeTheMember(Type t)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">构造实例</span>
            Type ctorArgument = Type.GetType(<span style="color: #800000;">"</span><span style="color: #800000;">System.Int32&amp;</span><span style="color: #800000;">"</span>);<span style="color: #008000;">//</span><span style="color: #008000;">或者typeof (Int32).MakeByRefType();</span>
            ConstructorInfo ctor= t.GetTypeInfo().DeclaredConstructors.First(c =&gt; c.GetParameters()[<span style="color: #800080;">0</span>].ParameterType ==<span style="color: #000000;"> ctorArgument);
            </span><span style="color: #0000ff;">object</span>[] args = <span style="color: #0000ff;">new</span> <span style="color: #0000ff;">object</span>[] {<span style="color: #800080;">12</span>};<span style="color: #008000;">//</span><span style="color: #008000;">构造器实参</span>
            <span style="color: #0000ff;">object</span> obj =<span style="color: #000000;"> ctor.Invoke(args);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">读写字段</span>
            FieldInfo fi = obj.GetType().GetTypeInfo().GetDeclaredField(<span style="color: #800000;">"</span><span style="color: #800000;">m_someField</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            fi.SetValue(obj, </span><span style="color: #800080;">33</span><span style="color: #000000;">);
            Console.WriteLine(fi.GetValue(obj));

            </span><span style="color: #008000;">//</span><span style="color: #008000;">调用方法</span>
            MethodInfo mi= obj.GetType().GetTypeInfo().GetDeclaredMethod(<span style="color: #800000;">"</span><span style="color: #800000;">ToString</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            </span><span style="color: #0000ff;">string</span> s = (<span style="color: #0000ff;">string</span>) mi.Invoke(obj,<span style="color: #0000ff;">null</span><span style="color: #000000;">);
            Console.WriteLine(s);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">读写属性</span>
            PropertyInfo pi= obj.GetType().GetTypeInfo().GetDeclaredProperty(<span style="color: #800000;">"</span><span style="color: #800000;">SomeProp</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
            {
                pi.SetValue(obj,</span><span style="color: #800080;">0</span>,<span style="color: #0000ff;">null</span><span style="color: #000000;">);
            }
            </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (TargetInvocationException e)
            {
                </span><span style="color: #0000ff;">if</span> (e.InnerException.GetType() != <span style="color: #0000ff;">typeof</span> (ArgumentOutOfRangeException)) <span style="color: #0000ff;">throw</span><span style="color: #000000;">;
            }
            pi.SetValue(obj,</span><span style="color: #800080;">2</span><span style="color: #000000;">);
            Console.WriteLine(pi.GetValue(obj));

            </span><span style="color: #008000;">//</span><span style="color: #008000;">为事件添加和删除方法</span>
            EventInfo ei = obj.GetType().GetTypeInfo().GetDeclaredEvent(<span style="color: #800000;">"</span><span style="color: #800000;">SomeEvent</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            EventHandler eh </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> EventHandler(EventCallback);
            ei.AddEventHandler(obj, eh);
            ei.RemoveEventHandler(obj, eh);

        }

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> BindToMemberCreateDelegateToMemberThenInvokeThenMember(Type t)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">构造实例（不能创建对构造器的委托）</span>
            <span style="color: #0000ff;">object</span>[] args = <span style="color: #0000ff;">new</span> <span style="color: #0000ff;">object</span>[] {<span style="color: #800080;">12</span><span style="color: #000000;">};
            </span><span style="color: #0000ff;">object</span> obj =<span style="color: #000000;"> Activator.CreateInstance(t, args);
            </span><span style="color: #008000;">//</span><span style="color: #008000;">注意不能创建对字段的委托

            </span><span style="color: #008000;">//</span><span style="color: #008000;">调用方法</span>
            MethodInfo mi= obj.GetType().GetTypeInfo().GetDeclaredMethod(<span style="color: #800000;">"</span><span style="color: #800000;">ToString</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            </span><span style="color: #0000ff;">var</span> toString = mi.CreateDelegate&lt;Func&lt;<span style="color: #0000ff;">string</span>&gt;&gt;<span style="color: #000000;">(obj);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">读写属性</span>
            PropertyInfo pi = obj.GetType().GetTypeInfo().GetDeclaredProperty(<span style="color: #800000;">"</span><span style="color: #800000;">SomeProp</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            </span><span style="color: #0000ff;">var</span> setSomeProp = pi.SetMethod.CreateDelegate&lt;Action&lt;Int32&gt;&gt;<span style="color: #000000;">(obj);
            setSomeProp(</span><span style="color: #800080;">2</span><span style="color: #000000;">);
            </span><span style="color: #0000ff;">var</span> getSomeProp = pi.GetMethod.CreateDelegate&lt;Func&lt;Int32&gt;&gt;<span style="color: #000000;">(obj);
            Console.WriteLine(getSomeProp());

            </span><span style="color: #008000;">//</span><span style="color: #008000;">向事件增删委托</span>
            EventInfo ei = obj.GetType().GetTypeInfo().GetDeclaredEvent(<span style="color: #800000;">"</span><span style="color: #800000;">SomeEvent</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            </span><span style="color: #0000ff;">var</span> addSomeEvent= ei.AddMethod.CreateDelegate&lt;Action&lt;EventHandler&gt;&gt;<span style="color: #000000;">(obj);
            addSomeEvent(EventCallback);
            </span><span style="color: #0000ff;">var</span> removeSomeEvent = ei.RemoveMethod.CreateDelegate&lt;Action&lt;EventHandler&gt;&gt;<span style="color: #000000;">(obj);
            removeSomeEvent(EventCallback);
        }

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> UseDynamicToBindAndInvokeTheMember(Type t)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">构造实例（不能创建对构造器的委托）</span>
            <span style="color: #0000ff;">object</span>[] args = <span style="color: #0000ff;">new</span> <span style="color: #0000ff;">object</span>[] {<span style="color: #800080;">12</span><span style="color: #000000;">};
            </span><span style="color: #0000ff;">dynamic</span> obj =<span style="color: #000000;"> Activator.CreateInstance(t, args);

            </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;">读写字段</span>
                obj.m_someField = <span style="color: #800080;">5</span><span style="color: #000000;">;
                Int32 v </span>=<span style="color: #000000;"> (Int32) obj.m_someField;
            }
            </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (RuntimeBinderException e)
            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;">之所以会执行到这里，是因为字段是私有的</span>
<span style="color: #000000;">            }

            </span><span style="color: #008000;">//</span><span style="color: #008000;">调用方法</span>
            String s =<span style="color: #000000;"> obj.ToString();
            Console.WriteLine(s);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">读写属性</span>
            obj.SomeProp = <span style="color: #800080;">2</span><span style="color: #000000;">;
            Console.WriteLine(obj.SomeProp);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">从事件增删委托</span>
            obj.SomeEvent += <span style="color: #0000ff;">new</span><span style="color: #000000;"> EventHandler(EventCallback);
            obj.SomeEvent </span>-= <span style="color: #0000ff;">new</span><span style="color: #000000;"> EventHandler(EventCallback);
        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;">添加到事件回调方法</span>
        <span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> EventCallback(<span style="color: #0000ff;">object</span><span style="color: #000000;"> sender, EventArgs e){}
    }</span></pre>
</div>
<p>&nbsp;</p>
<p>成员类型调用（Invoke）成员而需要调用（call）的方法FieldInfo调用GetValue获取字段的值调用SetValue设置字段的值ConstructorInfo调用Invoke构造类型的实例并调用构造器MethodInfo调用Invoke来调用类型的方法PropertyInfo调用GetValue来调用的属性的get访问器方法调用SetValue来调用属性的set访问器方法EventInfo调用AddEventHandler来调用事件的add访问器方法调用RemoveEventHandler来调用事件的remove访问器方法</p>
<p>&nbsp;</p>
<p><strong><span style="font-size: 14pt;">3，使用绑定句柄减少进程的内存消耗</span></strong></p>
<p>许多应用程序都绑定了一组类型（Type对象）或者类型成员（MemberInfo派生对象），并将这些类型对象保存在某种形式的集合中。Type和MemberInfo派生会对象需要大量内存。</p>
<p>FCL定义了RuntimeTypeHandle、RuntimeFieldHandle、RuntimeMethodHandle三个运行时句柄类型，这些类型都只包含一个IntPtr，这使类型的实例显得相当精简（相当省内存）</p>
<p>①将Type装换为RuntimeTypeHandle：调用Type的静态GetTypeHandle方法并传递那个Type对象引用</p>
<p>②将RuntimeTypeHandle转换为Type对象：调用Type的静态方法GetTypeFromHandle，并传递那个RuntimeTypeHandle</p>
<p>③将FieldInfo对象转换为一个RuntimeFieldHandle：查询FieldInfo的实例只读属性FieldHandle</p>
<p>④将RuntimeFieldHandle转换为FieldInfo对象：调用FieldInfo的静态方法GetFieldFromHandle</p>
<p>⑤将MethodInfo对象转换为一个RuntimeMethodHandle：查询MethodInfo的实例只读属性MethodHandle</p>
<p>⑥将RuntimeMethodHandle转换MethodInfo对象：调用MethodInfo的静态方法GetMethodFromHandle</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Reflection;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ConsoleApplication1
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">const</span> BindingFlags c_bf =<span style="color: #000000;">
            BindingFlags.FlattenHierarchy </span>|<span style="color: #000000;"> 
            BindingFlags.Instance </span>|<span style="color: #000000;"> 
            BindingFlags.Static </span>|<span style="color: #000000;"> 
            BindingFlags.Public </span>|<span style="color: #000000;">
            BindingFlags.NonPublic;

        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            
            Show(</span><span style="color: #800000;">"</span><span style="color: #800000;">显示在任何反射操作之前堆的大小</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">为 MSCorlib.dll中的所有方法构建MethodInfo对象缓存</span>
            List&lt;MethodBase&gt; methodInfos = <span style="color: #0000ff;">new</span> List&lt;MethodBase&gt;<span style="color: #000000;">();
            </span><span style="color: #0000ff;">foreach</span> (Type t <span style="color: #0000ff;">in</span> <span style="color: #0000ff;">typeof</span><span style="color: #000000;">(Object).Assembly.GetExportedTypes())
            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;">跳过任何泛型类型</span>
                <span style="color: #0000ff;">if</span>(t.IsGenericTypeDefinition)<span style="color: #0000ff;">continue</span><span style="color: #000000;">;

                MethodBase[] bm </span>=<span style="color: #000000;"> t.GetMethods(c_bf);
                methodInfos.AddRange(bm);
            }

            </span><span style="color: #008000;">//</span><span style="color: #008000;">显示当绑定所有方法之后，方法的个数和堆的大小</span>
            Console.WriteLine(<span style="color: #800000;">"</span><span style="color: #800000;">methodInfos集合数量={0:N0}</span><span style="color: #800000;">"</span><span style="color: #000000;">, methodInfos.Count);
            Show(</span><span style="color: #800000;">"</span><span style="color: #800000;">构建methodInfos之后</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">为所有MethodInfo对象构建RuntimeMethodHandle缓存</span>
            List&lt;RuntimeMethodHandle&gt; methodHandles = methodInfos.ConvertAll&lt;RuntimeMethodHandle&gt;(mb =&gt;<span style="color: #000000;"> mb.MethodHandle);
            Show(</span><span style="color: #800000;">"</span><span style="color: #800000;">构建methodHandles之后</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            GC.KeepAlive(methodInfos); </span><span style="color: #008000;">//</span><span style="color: #008000;">阻止缓存被过早的垃圾回收</span>
            methodInfos = <span style="color: #0000ff;">null</span>; <span style="color: #008000;">//</span><span style="color: #008000;">现在允许缓存垃圾回收</span>
            Show(<span style="color: #800000;">"</span><span style="color: #800000;">构建methodHandles之后，并且methodInfos = null</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            methodInfos </span>= methodHandles.ConvertAll&lt;MethodBase&gt;(rmh =&gt;<span style="color: #000000;"> MethodInfo.GetMethodFromHandle(rmh));
            Show(</span><span style="color: #800000;">"</span><span style="color: #800000;">重新构建methodInfos之后</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            GC.KeepAlive(methodHandles);</span><span style="color: #008000;">//</span><span style="color: #008000;">阻止缓存被过早的垃圾回收</span>
            GC.KeepAlive(methodInfos);<span style="color: #008000;">//</span><span style="color: #008000;">阻止缓存被过早的垃圾回收</span>
<span style="color: #000000;">
            methodHandles </span>= <span style="color: #0000ff;">null</span>;<span style="color: #008000;">//</span><span style="color: #008000;">现在允许缓存垃圾回收</span>
            methodInfos = <span style="color: #0000ff;">null</span>; <span style="color: #008000;">//</span><span style="color: #008000;">现在允许缓存垃圾回收</span>
<span style="color: #000000;">
            Show(</span><span style="color: #800000;">"</span><span style="color: #800000;">最后</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            Console.ReadKey();
        }

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Show(<span style="color: #0000ff;">string</span><span style="color: #000000;"> s)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">GC.GetTotalMemory(true)返回之前等待垃圾回收</span>
            Console.WriteLine(<span style="color: #800000;">"</span><span style="color: #800000;"> Heap size={0,12:N0} - {1}</span><span style="color: #800000;">"</span>,GC.GetTotalMemory(<span style="color: #0000ff;">true</span><span style="color: #000000;">),s);
        }
    }
}</span></pre>
</div>
<p><img src="http://images2015.cnblogs.com/blog/741594/201707/741594-20170723175301799-821970507.jpg" alt="" /></p>
<p>&nbsp;</p>