<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">一、实例构造器和类（引用类型）</span></p>
<p>1，极少数情况下可以在不调用实例构造器的前提下创建类型的实例<br />①Object的MemberwiseClone方法<br />②运行时序列化器反序列化对象时，通常也不需要调用构造器</p>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">internal</span> <span style="color: #0000ff;">sealed</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SomeType
    {
        </span><span style="color: #0000ff;">private</span> Int32 m_x = <span style="color: #800080;">5</span><span style="color: #000000;">;
        </span><span style="color: #0000ff;">private</span> String m_s = <span style="color: #800000;">"</span><span style="color: #800000;">Hi</span><span style="color: #800000;">"</span><span style="color: #000000;">;
        </span><span style="color: #0000ff;">private</span> Double m_d = <span style="color: #800080;">3.14</span><span style="color: #000000;">;
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">byte</span><span style="color: #000000;"> m_b;

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> SomeType()
        {
        }
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> SomeType(Int32 x)
        {
        }
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> SomeType(String s)
        {
            m_d </span>= <span style="color: #800080;">10</span><span style="color: #000000;">;
        }
    }</span></pre>
</div>
<p>由于有三个构造器，所以编译器生成三次初始化m_x，m_s，m_d的代码----每个构造器初始化一次。可以在一个构造器中初始化，让其他构造器都显示调用这个构造器。这样可以减少生成的代码</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">二、实例构造器和结构（值类型）</span></p>
<p>①值类型的实例构造器只有显式调用才会执行。<br />②结构不能包含显式的无参构造函数<br />③结构中不能有实例字段初始值设定项</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">internal</span> <span style="color: #0000ff;">struct</span> Point{<span style="color: #0000ff;">public</span> Int32 m_x, m_y=<span style="color: #800080;">5</span>;}</pre>
</div>
<p>④在有参构造函数中必须对所有字段赋值</p>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">internal</span> <span style="color: #0000ff;">struct</span><span style="color: #000000;"> Point
    {
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Int32 m_x, m_y;

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Point(Int32 x)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">看起来很奇怪，但编译没有问题，会将所有字段初始化为0/null</span>
            <span style="color: #0000ff;">this</span>=<span style="color: #0000ff;">new</span><span style="color: #000000;"> Point();
            m_x </span>=<span style="color: #000000;"> x;
        }
    }</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">三、类型构造器</span></p>
<p>①类型构造器最多只能定义一个。此外，类型构造器永远没有参数</p>
<p>②类型构造器总是私有的</p>
<p>③如果构造器从未执行，JIT编译器会在它生成的本机代码中添加对类型构造器的调用。如果类型构造器已经执行，JIT编译器就不添加对它的调用</p>
<p>④多个线程可能同时执行相同的方法</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">四、装换操作符方法</span></p>
<p>implicit：隐式转型。只有在转换不损失精度或数量级的前提下（比如int32转成Rational）</p>
<p>explicit：显示转型。装换会造成精度或数量级的损失（比如将Rational转成int32）</p>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> a
    {
        </span><span style="color: #0000ff;">public</span> a(<span style="color: #0000ff;">int</span><span style="color: #000000;"> i)
        {
            
        }
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> a <span style="color: #0000ff;">operator</span> +<span style="color: #000000;">(a a1)
        {
            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> a(<span style="color: #800080;">2</span><span style="color: #000000;">);
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">implicit</span> <span style="color: #0000ff;">operator</span> a(<span style="color: #0000ff;">int</span><span style="color: #000000;"> i)
        {
            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> a(i);
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">implicit</span> <span style="color: #0000ff;">operator</span> <span style="color: #0000ff;">int</span><span style="color: #000000;">(a i)
        {
            </span><span style="color: #0000ff;">return</span> <span style="color: #800080;">2</span><span style="color: #000000;">;
        }
    }</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">五、扩展方法的规则和原则</span></p>
<p>①C#只支持扩展方法，不支持扩展属性、扩展事件、扩展操作符等</p>
<p>②扩展方法必须在非泛型的静态类中声明</p>
<p>③扩展方法不可以是嵌套类</p>
<p>④为增强性能，并避免找到非你所愿的扩展方法，c#编译器要求&ldquo;导入&rdquo;扩展方法</p>
<p>⑤多个静态类可以定义相同的扩展方法，必须显式指定静态类的名称，明确告诉编译器要调用哪个方法</p>
<p>⑥不要将System.Object作为扩展方法的第一个参数</p>