<p>1， 什么是栈帧？</p>
<p>在调用方法的时候，内存从栈的顶部开始分配，保存和方法关联的一些数据项。这块内存叫方法的栈帧</p>
<p>2，栈帧包含的内存保存如下内容</p>
<p>①返回地址，也就是在方法退出的时候继续执行的位置</p>
<p>②这些参数分配的内存，就是这方法的值参数，或者还可能是参数数组（如果有的话）</p>
<p>③各种和方法调用相关的其他管理数据项</p>
<p>3，在方法调用时，整个栈帧都会压入栈</p>
<p>4，在方法退出时，整个栈帧都会从栈上弹出（栈展开）</p>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> MethedA(<span style="color: #0000ff;">int</span> p1, <span style="color: #0000ff;">int</span><span style="color: #000000;"> p2)
        {
            MethedB(p1, p2);
        }
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> MethedB(<span style="color: #0000ff;">int</span> p1, <span style="color: #0000ff;">int</span><span style="color: #000000;"> p2)
        {

        }

        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            MethedA(</span><span style="color: #800080;">1</span>, <span style="color: #800080;">2</span><span style="color: #000000;">);
        }
    }</span></pre>
</div>
<p>5，以下演示在调用方法时栈帧压入栈的过程和方法结束后栈展开的过程（一共创建了3个栈帧）</p>
<p><img src="http://images2015.cnblogs.com/blog/741594/201704/741594-20170406123601066-474868361.png" alt="" /></p>
<p>&nbsp;</p>