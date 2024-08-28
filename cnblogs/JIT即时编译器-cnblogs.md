<p style="background-color: #169fe6;"><span style="font-size: 18pt;"><strong><span style="color: #ffffff;">一、什么是JIT?</span></strong></span></p>
<p>即时编译器，负责将IL转换成本机CPU指令</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">二、JIT编译原理</span></strong></p>
<p>①在Main方法执行之前，CLR会检测出Main的代码引用的所有类型。会导致CLR分配一个内部结构。在这个结构中，Console类型定义的每个方法都有一个对应的记录项<br />②Main方法首次调用WriteLine时，JITComplier函数会被调用。JITComplier函数负责将方法的IL代码编译成CPU指令<br />③修改最初对JITComplier的引用，使其指向内存块（包含了刚才编译好的本机CPU指令）的地址<br />④当Main要第二次调用WriteLine时，会直接执行内存块的代码，完全跳过JITComplier函数</p>
<p>第一次调用Console.WriteLine</p>
<p><img src="http://images2015.cnblogs.com/blog/741594/201701/741594-20170119212556500-870067635.png" alt="" /></p>
<p>第二次调用Console.WriteLine</p>
<p><img src="http://images2015.cnblogs.com/blog/741594/201701/741594-20170119212704734-551015915.png" alt="" /></p>
<p>&nbsp;</p>
<p>方法仅在首次调用时才会有一些性能的损失。以后对该方法的所有调用都以本机代码的形式全速运行，无需重新验证IL并把它编译成本机代码</p>
<p>JIT编译器将本机CUP指令存储到动态内存中，这意味着一旦应用程序终止，编译好的代码会被丢弃</p>
<p>CLR的JIT编译器会对本机代码进行优化</p>