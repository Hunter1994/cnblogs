<p><span style="font-size: 16px;"><strong>一、在讲堆栈之前，我们先看看值类型和引用类型：</strong></span></p>
<p>&nbsp;</p>
<p><span style="font-size: 16px;"><img src="http://images.cnitblog.com/blog2015/741594/201504/161025226201207.jpg" alt="" /></span></p>
<p>&nbsp;</p>
<p><strong>1，我们看看值类型与引用类型的存储方式：</strong></p>
<p>引用类型：引用类型存储在堆中。类型实例化的时候，会在堆中开辟一部分空间存储类的实例。类对象的引用还是存储在栈中。</p>
<p>值类型：值类型总是分配在它声明的地方，做为局部变量时，存储在栈上；类对象的字段时，则跟随此类存储在堆中。</p>
<p>什么是堆什么是栈我们后面解释。</p>
<p>&nbsp;</p>
<p><img src="http://images.cnitblog.com/blog2015/741594/201504/171120038703080.png" alt="" /></p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 图1-1</p>
<p>&nbsp;</p>
<p><strong>2，我们再看看引用类型与值类型的区别：</strong></p>
<p>①引用类型和值类型都继承自Systerm.Object类。不同之处，几乎所有的引用类型都是直接从Systerm.Object继承，而值类型则是继承Systerm.Object的子类Systerm.ValueType类。</p>
<p>②我们在给引用类型的变量赋值的时候，其实只是赋值了对象的引用；而给值类型变量赋值的时候是创建了一个副本（副本不明白？说通俗点，就是克隆了一个变量）。</p>
<p>文字不够形象？我们上代码看看</p>
<p><img src="http://images.cnitblog.com/blog2015/741594/201504/171142215578041.png" alt="" /></p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 图1-2</p>
<p>&nbsp;</p>
<p><strong>&nbsp;3，我们再看看引用类型和值类型的内存分配情况（我们对着代码与图看）</strong></p>
<p><img src="http://images.cnitblog.com/blog2015/741594/201504/301435158026063.png" alt="" /></p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 图1-3</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p><img src="http://images.cnitblog.com/blog2015/741594/201504/301442244905529.png" alt="" /></p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 图1-4</p>
<p>&nbsp;</p>
<p>&nbsp;看了图1-3和图1-4之后，你们可能问我了：你是怎么知道变量在栈中的地址的。嘿嘿，等下教你用c#玩指针</p>
<p>从上面两张图我们可以看出：</p>
<p>①栈的结构是后进先出，也就是说：变量j的生命周期在变量s之前结束，变量s的生命周期在变量i之前结束，</p>
<p>②栈地址从高往底分配</p>
<p>③类型的引用也存储在栈中</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p><span style="font-size: 16px;"><strong>二、对于堆和栈的详细介绍，我们往下看。</strong></span></p>
<p>&nbsp;</p>
<p><strong>1,有人老是搞不明白堆和栈的叫法。我来解释下：</strong></p>
<p>堆：在c里面叫堆，在c#里面其实叫托管堆。为什么叫托管堆，我们往下看。</p>
<p>栈：就是堆栈，因为和堆一起叫着别扭，就简称栈了。</p>
<p>&nbsp;</p>
<p><strong>2,托管堆：</strong></p>
<p>托管堆不同于堆，它是由CLR（公共语言运行库(Common Language Runtime)）管理，当堆中满了之后，会自动清理堆中的垃圾。所以，做为.net开发，我们不需要关心内存释放的问题。</p>
<p>&nbsp;</p>
<p><strong>3,有人老是搞不清楚内存堆栈与数据结构堆栈，我们来看看什么是内存堆栈，什么是数据结构堆栈</strong></p>
<p>①数据结构堆栈：是一种后进先出的数据结构，它是一个概念，图4-1中可以看出，栈是一种后进先出的数据结构。</p>
<p>②内存堆栈：存在内存中的两个存储区（堆区，栈区）。</p>
<p>　　　　　　栈区：存放函数的参数、局部变量、返回数据等值，由编译器自动释放</p>
<p>　　　　　　堆区：存放着引用类型的对象，由CLR释放</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p><span style="font-size: 16px;"><strong>&nbsp;三、最后我们用c#玩一玩指针</strong></span></p>
<p><strong>1，首先右键项目--&gt;属性--&gt;生成--&gt;勾选允许不安全代码</strong></p>
<p><img src="http://images0.cnblogs.com/blog2015/741594/201505/251719340995418.png" alt="" /></p>
<p>&nbsp;</p>
<p><strong>2，在写不安全代码的时候需要加上<span style="color: #3366ff;">unsafe</span></strong></p>
<div class="cnblogs_Highlighter">
<pre class="brush:csharp;gutter:true;">    //标记类
    unsafe public class Student
    {
        //标记字段
        unsafe int* pAge;
        //标记方法
        unsafe void getType(int* a)
        {
            //标记代码段
            unsafe
            {
                int* pAbc;      //声明指针语法
            }
        }
    }
</pre>
</div>
<p>　　</p>
<p><strong>3，指针的语法</strong></p>
<div class="cnblogs_Highlighter">
<pre class="brush:csharp;gutter:true;">            unsafe
            {
                int* pWidth, pHeight;
                double* pResult;
                byte*[] pByte;
                //&amp;：表示&ldquo;取地址&rdquo;,并把一个值数据类型转换为指针，例如，int转换为*int。这个运算称为【寻址运算符】
                //*：表示&ldquo;获取地址内容&rdquo;，把一个指针转换为一个值数据类型（例如：*float转换为float）。这个运算符被
                    //称为&ldquo;间接寻址运算符&rdquo;（有时称&ldquo;取消引用运算符&rdquo;）
                int a = 10;//声明一个值类型，给它赋值10
                int* pA, pB;//声明2个指针
                pA = &amp;a;//取出值类型a的地址，赋值给指针pA
                pB = pA;//把指针pA的地址赋值给pB
                *pB = 20;//获取pB指向的地址内容，并赋值20
                Console.WriteLine(a);//输出20
            }
</pre>
</div>
<p>　　</p>
<p><strong>4，将指针强制转化为整数类型(只能转化为uing、long、ulong类型)</strong></p>
<div class="cnblogs_Highlighter">
<pre class="brush:csharp;gutter:true;">int a = 10;
int* pA, pB;
pA = &amp;a;
uint address = (uint)pA;//将指针地址强制转换为整数类型
pB = (int*)address;//将整数类型强制转换为指针
*pB = 20;//指针指向a
Console.WriteLine(a);//输出20
</pre>
</div>
<p>　　</p>
<p><strong>5，指针类型的强制装换</strong></p>
<div class="cnblogs_Highlighter">
<pre class="brush:csharp;gutter:true;">int b = 10;
int* pIa;
double* pDa;
pIa = &amp;b;
pDa = (double*)pIa;//将int*强制转换成double*
</pre>
</div>
<p>　　</p>
<p><strong>6，void指针（不指向任何数据类型的指针）</strong></p>
<div class="cnblogs_Highlighter">
<pre class="brush:csharp;gutter:true;">int c = 10;
int* pAA;
pAA = &amp;c;
void* pVa = (void*)pAA;//转换viod指针
</pre>
</div>
<p>　　</p>
<p><strong>7，指针算数的运算（不允许对void指针进行运算）</strong></p>
<div class="cnblogs_Highlighter">
<pre class="brush:csharp;gutter:true;">int d = 10;
int* pId;//如果地址为100000
pId = &amp;d;
pId++;//结果：100004（int类型的大小为4个字节）
</pre>
</div>
<p>　　</p>
<p><strong>8，结构指针：指针成员访问运算符</strong></p>
<p>①指针不能只想任何引用类型<br />②结构里面不能包含引用类型</p>
<div class="cnblogs_Highlighter">
<pre class="brush:csharp;gutter:true;">MyStruct* pStruct;
MyStruct ms = new MyStruct();
pStruct = &amp;ms;
//--取地址内容赋值为10
(*pStruct).X = 10;
pStruct-&gt;X = 10;
//--取地址赋值给pIs
int* pIs1 = &amp;(ms.X);
int* pIs2 = &amp;(pStruct-&gt;X); 
//结构
struct MyStruct
{
        public int X = 1;
        public int Y = 2;
}
</pre>
</div>
<p>　　</p>
<p><strong>9，类成员指针</strong></p>
<div class="cnblogs_Highlighter">
<pre class="brush:csharp;gutter:true;">Person p = new Person();
fixed (int* pIp1 = &amp;(p.X), pIp2 = &amp;(p.Y))
{
}//pIp1和pIp2的生命周期
//类
class Person
{
     public int X;
     public int Y;
}
</pre>
</div>
<p>　　</p>
<p>&nbsp;</p>
<p><strong>10，有趣的实验</strong></p>
<div class="cnblogs_Highlighter">
<pre class="brush:csharp;gutter:true;">unsafe
{
//有趣的问题：为什么b的值改变了
//回答：因为i的地址指向了b
int a = 10;
int b = 20;
int* i;
i = &amp;a;//将a的地址赋值给指针i
i -= 1;//将i的地址-1（相当于向下移动4个字节（int类型的大小为4个字节））
*i = 30;//取出i指针指向的内容赋值为30
Console.WriteLine(b);//输出30
}
</pre>
</div>
<p>　　</p>
<p>&nbsp;</p>