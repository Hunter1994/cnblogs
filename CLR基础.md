<p style="background-color: #169fe6;"><strong><span style="color: #ffffff; font-size: 18pt;">一、各个语言的长处</span></strong></p>
<p>①非托管C/C++可对系统进行低级控制。可完全按照自己的想法管理内存，必要时方便地创建线程<br />②使用Microsoft Visual Basic 6.0可以快速生成UI应用程序，并可以方便的控制COM对象和数据库<br />③公共语言运行时（CLR）是一个可以由多种编程语言使用的&ldquo;运行时&rdquo;。CLR的核心功能（内存管理、程序集加载、安全性、异常处理、线程同步）可由面向CLR的所有语言使用</p>
<p style="background-color: #169fe6;"><strong><span style="color: #ffffff; font-size: 18pt;">二、什么是托管模块</span></strong></p>
<p>托管模块是标准的32位Microsoft Windows可移植执行体（PE32）文件，或者是标准的64位Windows可移植执行体（PE32+）文件，它们都需要CLR才能执行<br />【PE：可移植执行体】</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">三、托管模块的各个组成部分</span></strong></p>
<table style="height: 510px; width: 826px;" border="1" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td valign="top" width="177">
<p><strong>组成部分</strong></p>













</td>
<td valign="top" width="391">
<p><strong>说明</strong></p>













</td>













</tr>
<tr>
<td valign="top" width="177">
<p><strong>PE32</strong><strong>或PE32+</strong><strong>头</strong></p>













</td>
<td valign="top" width="391">
<p>①标准Windows PE文件头。这个头使用PE32或PE32+格式</p>
<p>②标识文件类型（GUI,CUI或者DLL），并包含文件的生成时间</p>
<p>对于只包含IL代码的模块，PE32(+)头的大多数信息会被忽视。如果包含（native）CPU代码的模块，这个头包含与本机CPU代码有关的信息</p>













</td>













</tr>
<tr>
<td valign="top" width="177">
<p><strong>CLR</strong><strong>头</strong></p>













</td>
<td valign="top" width="391">
<p>包含使这个模块成为托管的信息（可由CLR和一些实用程序进行解释）</p>
<p>①CLR版本（major（主）minor（次）版本号）</p>
<p>②一些标志（flag）</p>
<p>③托管模块入口方法（Main方法）的MethodDef元数据token</p>
<p>④元数据</p>
<p>⑤资源</p>
<p>⑥强名称</p>
<p>⑦一些标志及其他不太重要的数据项的位置/大小</p>













</td>













</tr>
<tr>
<td valign="top" width="177">
<p><strong>元数据</strong></p>













</td>
<td valign="top" width="391">
<p>每个托管模块都包含元数据表（两种表）</p>
<p>①描述源代码中定义的类型和成员</p>
<p>②描述代码引用的类型和成员</p>













</td>













</tr>
<tr>
<td valign="top" width="177">
<p><strong>IL</strong><strong>（中间语言）代码</strong></p>













</td>
<td valign="top" width="391">
<p>编译器编译源代码时生成的代码。在运行时，CLR将IL编译成本机CPU指令</p>













</td>













</tr>













</tbody>













</table>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">四、安全性</span></strong></span></p>
<p>托管语言总是利用Windows的数据执行保护（Data Execution Prevention DEP）和地址空间布局随机化（Address Space Layout Randomization ASLR）来增强整个系统的安全性</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">五、什么是IL代码</span></strong></p>
<p>IL代码有时称为托管代码，因为CLR管理它的执行</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">六、元数据</span></strong></p>
<p>1，什么是元数据<br />①元数据是一些老技术的超集。这些老技术包括COM的&ldquo;类型库&rdquo;（Type Library）和&ldquo;接口定义语言&rdquo;（Interface Definition Language,IDL）文件<br />②元数据和类型库和IDL不同，元数据总是与包含IL代码的文件关联（元数据总是嵌入和代码相同的EXE/DLL文件中，并嵌入最终生成的托管模块，所以元数据和它描述的IL代码永远不会失去同步）</p>
<p>2，元数据的用途<br />①元数据避免了在编译时对原生C/C++头和库文件的需求，编译器直接从托管模块中读取元数据<br />②Microsoft Visual stidio&ldquo;智能感知&rdquo;技术会解析元数据，告诉你一个类型提供了那些方法、属性、事件和字段。对于方法，还能告诉你需要的参数<br />③CLR的代码验证过程使用元数据确保代码只执行&ldquo;类型安全&rdquo;的操作<br />④元数据允许将对象的字段序列化到内存块，将其发送到另一台机器，然后反序列化，在远程机器上重建对象状态<br />⑤元数据允许垃圾回收器跟踪对象的生存期。垃圾回收期能判断任何对象的类型，并从元数据知道那个对象中的哪些字段引用了其他对象</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">七、C++编译器</span></strong></p>
<p>Microsoft C++编译器的灵活性是其他编译器无法比拟的，因为它允许开发人员在托管代码中使用原生的C/C++代码</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">八、什么是程序集</span></strong></p>
<p>①一个或多个模块/资源文件的逻辑分组<br />②重用、安全性、版本控制的最小单元<br />③相当于组件<br />④将托管模块合并成程序集</p>
<p><img src="http://images2015.cnblogs.com/blog/741594/201701/741594-20170119193853218-1603648396.jpg" alt="" /></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt;"><strong><span style="color: #ffffff;">九、MSCorEE.dll</span></strong></span></p>
<p><br />当运行应用程序时，windows检查exe文件头，决定创建32位或者64位进程之后，会在进程地址空间加载MSCorEE.dll的x86，x64或ARM版本，然后进程的主线程调用MSCorEE.dll中定义的一个方法。这个方法初始化CLR，加载EXE程序集，在调用其入口方法（Main）。随即，托管应用程序启动并运行</p>