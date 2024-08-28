<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">一、StringComparison</span></p>
<p>1，出于编程目的而比较字符串时，应该总数使用StringComparison.Ordinal或者StringComparison. OrdinalIgnoreCase。忽略语言文化是字符串比较最快的方式</p>
<p>2，要以语言文化正确的方式来比较字符串（通常为了向用户显示），就应该使用StringComparison. CurrentCulture或者StringComparison. CurrentCultureIgnoreCase</p>
<p>3，StringComparison. InvariantCulture和StringComparison. InvariantCultureIgnoreCase平时最好不要用</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">二、CultureInfo</span></p>
<p>在CLR中，每个线程都关联了两个特殊属性，每个属性都引用一个CultureInfo对象。两个属性的具体描述如下</p>
<p>1，CurrentUICulture属性：该属性获取向用户显示的资源。它在GUI或Web窗体应用程序中特别有用，因为他标志了在显示UI元素（比如标签和按钮）时应使用的语言。创建线程时，这个线程属性会被设置成一个默认的CultureInfo对象，该对象标识了正在运行时应用程序的Windows版本所用的语言。而这个语言使用Win32函数GetUserDefaultUILanguage来获取的。如果应用程序在Windows的MUI（多语言用户界面）版本上运行，可通过控制面板的&ldquo;区域和语言&rdquo;对话框来修改语言。在非MUI版本的Windows上，语言有安装的操作系统的本地化版本（或安装的语言包）决定，而且这个语言不可更改</p>
<p>2，CurrentCulture属性：不适合用CurrentUICulture属性场合就该用该属性，例如数字和日期格式化、字符串大小写转换以及字符串比较。格式化要同时用到CultureInfo对象的&ldquo;语言&rdquo;和&ldquo;国家&rdquo;部分。创建线程时，这个线程属性被设置为一个默认的CultureInfo对象，其之通过调用Win32函数GetUserDefaultLCUID来获取。可通过Windows控制面板的&ldquo;区域或语言&rdquo;对话框来修改这个值</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">三。字符串留用</span></p>
<p>程序集加载时，CLR默认留用程序集的元数据中描述的所有字面值字符串。4.5版本以上会进行留用</p>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            
            </span><span style="color: #0000ff;">var</span> s = <span style="color: #800000;">"</span><span style="color: #800000;">Hello</span><span style="color: #800000;">"</span><span style="color: #000000;">;
            </span><span style="color: #0000ff;">var</span> ss = <span style="color: #800000;">"</span><span style="color: #800000;">Hello</span><span style="color: #800000;">"</span><span style="color: #000000;">;
            </span><span style="color: #008000;">//</span><span style="color: #008000;">Console.WriteLine(string.IsInterned(ss)); </span><span style="color: #008000;">//</span><span style="color: #008000;">如果该字符已经留用，则返回对这个留用字符串对象的引用；没有留用，则返回null
            </span><span style="color: #008000;">//</span><span style="color: #008000;">Console.WriteLine(string.Intern(ss)); </span><span style="color: #008000;">//</span><span style="color: #008000;">如果该字符串已经留用，则返回对这个留用字符串对象的引用；没有留用，则留用
            </span><span style="color: #008000;">//</span><span style="color: #008000;">Console.ReadKey();</span>
<span style="color: #000000;">
            Console.WriteLine(Object.ReferenceEquals(s,ss));</span><span style="color: #008000;">//</span><span style="color: #008000;">Ture

            </span><span style="color: #008000;">//</span><span style="color: #008000;">显示留用</span>
            s = <span style="color: #0000ff;">string</span><span style="color: #000000;">.Intern(s);
            ss </span>= <span style="color: #0000ff;">string</span><span style="color: #000000;">.Intern(ss);
            Console.WriteLine(Object.ReferenceEquals(s, ss));</span><span style="color: #008000;">//</span><span style="color: #008000;">Ture</span>
<span style="color: #000000;">            Console.ReadKey();
        }</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">四、字符串池</span></p>
<p>编译源代码时，编译器必须处理每个字面值字符串，斌仔托管模块的元数据中嵌入。同一个字符串在源代码中多次出现，把它们都嵌入元数据会使生成的文件无畏地增大。为了解决这个问题，许多编译器（包括c#编译器）只在模块的元数据中只将字面值字符串写入一次</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">五、StringBuilder</span></p>
<p>StringBuilder代表可变字符串<br />StringBuilder只有以下两种情况才会分配新对象：<br />①动态构造字符串，其长度超过了设置的&ldquo;容量&rdquo;<br />②调用StringBuilder的ToString方法</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">六、IFormattable</span></p>
<p><img src="http://images2015.cnblogs.com/blog/741594/201705/741594-20170509213557894-1472187812.png" alt="" /></p>
<p>&nbsp;</p>
<p>format：这个特殊字符串告诉方法应该如何格式化对象<br />formatProvider：实现了system. IFormatProvider接口的一个类型的实例，该类型微ToString方法提供具体的语言文化信息<br />1，Datetime<br />d：短日期<br />D：长日期<br />g：常规<br />M：月/日<br />s：可排序<br />T：长时间<br />u：ISO 8601格式的协调世界时<br />U：长日期格式的协调世界时<br />Y：年/月<br />所有的枚举类型都支持用G表示常规，F表示标志，D表示十进制，X表示十六进制</p>
<p>2，数值类型<br />C：货币格式<br />D：十进制格式<br />E：科学计数法（指数）格式<br />F：定点格式<br />N：数字格式<br />P：百分比格式<br />R：往返行程格式</p>
<p>3，IFormatProvider<br /> </p>
<p>&nbsp;<img src="http://images2015.cnblogs.com/blog/741594/201705/741594-20170509213545504-1898117884.png" alt="" /></p>
<p>&nbsp;</p>