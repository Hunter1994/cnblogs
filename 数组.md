<p><strong><span style="font-size: 18px;">1，所有数组都隐式派生自System.Array</span></strong></p>
<p><span style="font-size: 18px;"><strong>2，所有数组都隐式实现IEnumerable,ICollecation,IList</strong></span></p>
<p>①创建一个0基数组类型时，CLR自动是数组类型实现IEnumberable&lt;T&gt;,ICollection&lt;T&gt;,IList&lt;T&gt;。同时，还为数组类型的所有基类型实现这三个接口。以下层次结构图对此进行了澄清</p>
<p>Object</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Array(非泛型IEnumberable，ICollection,IList)</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Object[](IEnumberable，ICollection,IList of Object)</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Stream[](IEnumberable，ICollection,IList of Stream)</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; FileStream[](IEnumberable，ICollection,IList of FileStream)</p>
<p>&nbsp;</p>
<p>②如果数组包含值类型的元素，数组类型不会为元素的基类型实现接口（DateTime[] dtArray）</p>
<p><strong><span style="font-size: 18px;">3，创建下限非零的数组</span></strong></p>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {

            </span><span style="color: #008000;">//</span><span style="color: #008000;">下届非0的二维数组</span>
            <span style="color: #0000ff;">int</span>[] lowerBounds = {<span style="color: #800080;">2015</span>, <span style="color: #800080;">1</span>};<span style="color: #008000;">//</span><span style="color: #008000;">下界</span>
            <span style="color: #0000ff;">int</span>[] lengths = {<span style="color: #800080;">5</span>, <span style="color: #800080;">4</span>};<span style="color: #008000;">//</span><span style="color: #008000;">它包含要创建的 System.Array 的每个维度的大小</span>

            <span style="color: #0000ff;">var</span> d = (<span style="color: #0000ff;">decimal</span>[,]) Array.CreateInstance(<span style="color: #0000ff;">typeof</span> (<span style="color: #0000ff;">decimal</span><span style="color: #000000;">), lengths, lowerBounds);

            Console.WriteLine(d.GetLowerBound(</span><span style="color: #800080;">0</span>));<span style="color: #008000;">//</span><span style="color: #008000;">1维第一个元素的索引。输出2015</span>
            Console.WriteLine(d.GetUpperBound(<span style="color: #800080;">0</span>));<span style="color: #008000;">//</span><span style="color: #008000;">1维最后一个元素的索引。输出2019</span>
            Console.WriteLine(d.GetLowerBound(<span style="color: #800080;">1</span>));<span style="color: #008000;">//</span><span style="color: #008000;">2维第一个元素的索引。输出1</span>
            Console.WriteLine(d.GetUpperBound(<span style="color: #800080;">1</span>));<span style="color: #008000;">//</span><span style="color: #008000;">2维最后一个元素的索引。输出4</span>
<span style="color: #000000;">

            Console.ReadKey();

        }</span></pre>
</div>
<p><strong><span style="font-size: 18px;">4，CLR内部实际支持两种不同的数组</span></strong><br />①下限为0的一维数组。这些数组有时称为SZ（一维0基）数组或向量<br />②下限未知的一维或多维数组</p>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            Array a;
            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建一维0基数组，不包含任何元素</span>
            a = <span style="color: #0000ff;">new</span> <span style="color: #0000ff;">string</span>[<span style="color: #800080;">0</span><span style="color: #000000;">];
            Console.WriteLine(a.GetType());</span><span style="color: #008000;">//</span><span style="color: #008000;">System.String[]

            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建一维0基数组，不包含任何元素</span>
            a = Array.CreateInstance(<span style="color: #0000ff;">typeof</span> (String), <span style="color: #0000ff;">new</span> <span style="color: #0000ff;">int</span>[] {<span style="color: #800080;">0</span>}, <span style="color: #0000ff;">new</span> <span style="color: #0000ff;">int</span>[] {<span style="color: #800080;">0</span><span style="color: #000000;">});
            Console.WriteLine(a.GetType());</span><span style="color: #008000;">//</span><span style="color: #008000;">System.String[]

            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建一维1基数组，不包含任何元素</span>
            a = Array.CreateInstance(<span style="color: #0000ff;">typeof</span>(String), <span style="color: #0000ff;">new</span> <span style="color: #0000ff;">int</span>[] { <span style="color: #800080;">0</span> }, <span style="color: #0000ff;">new</span> <span style="color: #0000ff;">int</span>[] { <span style="color: #800080;">1</span><span style="color: #000000;"> });
            Console.WriteLine(a.GetType());</span><span style="color: #008000;">//</span><span style="color: #008000;">System.String[*]  *符号表明CLR知道该数组不是0基的

            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建二维0基数组，不包含任何元素</span>
            a = <span style="color: #0000ff;">new</span> <span style="color: #0000ff;">string</span>[<span style="color: #800080;">0</span>,<span style="color: #800080;">0</span><span style="color: #000000;">];
            Console.WriteLine(a.GetType());</span><span style="color: #008000;">//</span><span style="color: #008000;">System.String[,]

            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建二维0基数组，不包含任何元素</span>
            a = Array.CreateInstance(<span style="color: #0000ff;">typeof</span>(String), <span style="color: #0000ff;">new</span> <span style="color: #0000ff;">int</span>[] { <span style="color: #800080;">0</span>,<span style="color: #800080;">0</span> }, <span style="color: #0000ff;">new</span> <span style="color: #0000ff;">int</span>[] { <span style="color: #800080;">0</span>,<span style="color: #800080;">0</span><span style="color: #000000;"> });
            Console.WriteLine(a.GetType());</span><span style="color: #008000;">//</span><span style="color: #008000;">System.String[,]

            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建二维1基数组，不包含任何元素</span>
            a = Array.CreateInstance(<span style="color: #0000ff;">typeof</span>(String), <span style="color: #0000ff;">new</span> <span style="color: #0000ff;">int</span>[] { <span style="color: #800080;">0</span>,<span style="color: #800080;">0</span> }, <span style="color: #0000ff;">new</span> <span style="color: #0000ff;">int</span>[] { <span style="color: #800080;">1</span>,<span style="color: #800080;">1</span><span style="color: #000000;"> });
            Console.WriteLine(a.GetType());</span><span style="color: #008000;">//</span><span style="color: #008000;">System.String[,]</span>
<span style="color: #000000;">
            Console.ReadKey();
        }</span></pre>
</div>
<p>在运行时，CLR将所有的多维数组都视为非0基数组<br />访问一维0基数组的元素比访问非0基一维或多维数组的元素稍快</p>