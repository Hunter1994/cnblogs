<p>1，Expression.Invoke</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">运用委托或Lambda表达式</span>
            System.Linq.Expressions.Expression&lt;Func&lt;<span style="color: #0000ff;">int</span>, <span style="color: #0000ff;">int</span>, <span style="color: #0000ff;">bool</span>&gt;&gt; largeSumTest =(num1, num2) =&gt; (num1 + num2) &gt; <span style="color: #800080;">1000</span><span style="color: #000000;">;
            System.Linq.Expressions.InvocationExpression invocationExpression </span>=<span style="color: #000000;">
                System.Linq.Expressions.Expression.Invoke(
                    largeSumTest,
                    System.Linq.Expressions.Expression.Constant(</span><span style="color: #800080;">539</span><span style="color: #000000;">),
                    System.Linq.Expressions.Expression.Constant(</span><span style="color: #800080;">281</span><span style="color: #000000;">));
            Console.WriteLine(invocationExpression.ToString());</span><span style="color: #008000;">//</span><span style="color: #008000;">输出：Invoke((num1, num2) =&gt; ((num1 + num2) &gt; 1000), 539, 281)</span>
            Console.WriteLine(Expression.Lambda&lt;Func&lt;<span style="color: #0000ff;">bool</span>&gt;&gt;(invocationExpression).Compile()());<span style="color: #008000;">//</span><span style="color: #008000;">计算委托 返回false</span>
            Console.ReadKey();</pre>
</div>
<p>&nbsp;</p>
<p>案例：</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">执行1+2</span>
<span style="color: #0000ff;">var</span> a = Expression.Add(Expression.Constant(<span style="color: #800080;">1</span>), Expression.Constant(<span style="color: #800080;">2</span><span style="color: #000000;">));
</span><span style="color: #0000ff;">var</span> lambda = Expression.Lambda&lt;Func&lt;<span style="color: #0000ff;">int</span>&gt;&gt;<span style="color: #000000;">(a).Compile();
            Console.WriteLine(lambda());</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">执行Math.Sin()</span>
<span style="color: #0000ff;">var</span> p = Expression.Parameter(<span style="color: #0000ff;">typeof</span>(<span style="color: #0000ff;">double</span>), <span style="color: #800000;">"</span><span style="color: #800000;">a</span><span style="color: #800000;">"</span><span style="color: #000000;">);
</span><span style="color: #008000;">//</span><span style="color: #008000;">Sin(a)</span>
<span style="color: #0000ff;">var</span> exp = Expression.Call(<span style="color: #0000ff;">null</span>, <span style="color: #0000ff;">typeof</span>(Math).GetMethod(<span style="color: #800000;">"</span><span style="color: #800000;">Sin</span><span style="color: #800000;">"</span>, BindingFlags.Public |<span style="color: #000000;"> BindingFlags.Static), p);
</span><span style="color: #008000;">//</span><span style="color: #008000;">a=&gt;Sin(a)</span>
<span style="color: #0000ff;">var</span> l = Expression.Lambda&lt;Func&lt;<span style="color: #0000ff;">double</span>,<span style="color: #0000ff;">double</span>&gt;&gt;<span style="color: #000000;">(exp, p).Compile();
Console.WriteLine(l(</span><span style="color: #800080;">123</span>));</pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">执行i =&gt; i委托</span>
Expression&lt;Func&lt;<span style="color: #0000ff;">int</span>, <span style="color: #0000ff;">int</span>&gt;&gt; ex1 = i =&gt;<span style="color: #000000;"> i;
</span><span style="color: #0000ff;">var</span> paraemter = Expression.Parameter(<span style="color: #0000ff;">typeof</span>(<span style="color: #0000ff;">int</span>), <span style="color: #800000;">"</span><span style="color: #800000;">a</span><span style="color: #800000;">"</span><span style="color: #000000;">);
Console.WriteLine(Expression.Lambda</span>&lt;Func&lt;<span style="color: #0000ff;">int</span>, <span style="color: #0000ff;">int</span>&gt;&gt;(Expression.Invoke(ex1, paraemter), paraemter).Compile()(<span style="color: #800080;">1</span>));</pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">输出：((r.Name == "张三") AndAlso Invoke(r =&gt; (r.Sex == "男"), r))</span>
Expression&lt;Func&lt;Product, <span style="color: #0000ff;">bool</span>&gt;&gt; <span style="color: #0000ff;">where</span> = r =&gt; r.Name == <span style="color: #800000;">"</span><span style="color: #800000;">张三</span><span style="color: #800000;">"</span><span style="color: #000000;">;
Expression</span>&lt;Func&lt;Product, <span style="color: #0000ff;">bool</span>&gt;&gt; where2 = r =&gt; r.Sex == <span style="color: #800000;">"</span><span style="color: #800000;">男</span><span style="color: #800000;">"</span><span style="color: #000000;">;
</span><span style="color: #0000ff;">var</span> invoke = Expression.Invoke(where2, <span style="color: #0000ff;">where</span><span style="color: #000000;">.Parameters);
Console.WriteLine(invoke);
</span><span style="color: #0000ff;">var</span> and = Expression.AndAlso(<span style="color: #0000ff;">where</span><span style="color: #000000;">.Body, invoke);
Console.WriteLine(and);</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> LinqKit;
</span><span style="color: #008000;">//</span><span style="color: #008000;">ef查询</span>
DbContext db = <span style="color: #0000ff;">new</span> DbContext(ConfigurationManager.ConnectionStrings[<span style="color: #800000;">"</span><span style="color: #800000;">blogEntities</span><span style="color: #800000;">"</span><span style="color: #000000;">].ConnectionString);
Expression</span>&lt;Func&lt;products, <span style="color: #0000ff;">bool</span>&gt;&gt; <span style="color: #0000ff;">where</span> = r =&gt; <span style="color: #0000ff;">true</span><span style="color: #000000;">;
Expression</span>&lt;Func&lt;products, <span style="color: #0000ff;">bool</span>&gt;&gt; wherename = r =&gt; r.Name == <span style="color: #800000;">"</span><span style="color: #800000;">asd</span><span style="color: #800000;">"</span><span style="color: #000000;">;
</span><span style="color: #0000ff;">where</span> = Expression.Lambda&lt;Func&lt;products, <span style="color: #0000ff;">bool</span>&gt;&gt;(Expression.AndAlso(<span style="color: #0000ff;">where</span>.Body, Expression.Invoke(wherename,<span style="color: #0000ff;">where</span>.Parameters)), <span style="color: #0000ff;">where</span><span style="color: #000000;">.Parameters);
</span><span style="color: #0000ff;">var</span> ps = db.Set&lt;products&gt;().AsNoTracking().AsExpandable().Where(<span style="color: #0000ff;">where</span><span style="color: #000000;">).AsQueryable().ToList();
</span><span style="color: #0000ff;">foreach</span> (<span style="color: #0000ff;">var</span> item <span style="color: #0000ff;">in</span><span style="color: #000000;"> ps)
{
      Console.WriteLine($</span><span style="color: #800000;">"</span><span style="color: #800000;">id:{item.Id} qty:{item.Qty} name:{item.Name} aa:{item.AA}</span><span style="color: #800000;">"</span><span style="color: #000000;">);
}</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">执行Lambda r =&gt; r 输出：1</span>
Expression&lt;Func&lt;<span style="color: #0000ff;">int</span>, <span style="color: #0000ff;">int</span>&gt;&gt; exr = r =&gt;<span style="color: #000000;"> r;
</span><span style="color: #0000ff;">var</span> invoke = Expression.Invoke(exr, Expression.Constant(<span style="color: #800080;">1</span><span style="color: #000000;">));
</span><span style="color: #0000ff;">var</span> d =<span style="color: #000000;"> Expression.Lambda(invoke).Compile();
Console.WriteLine(d.DynamicInvoke());</span></pre>
</div>
<p>&nbsp;一、QueryFilter</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('6e52af19-e478-4de0-ad29-a069e9dcbb46')"><img id="code_img_closed_6e52af19-e478-4de0-ad29-a069e9dcbb46" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_6e52af19-e478-4de0-ad29-a069e9dcbb46" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('6e52af19-e478-4de0-ad29-a069e9dcbb46',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_6e52af19-e478-4de0-ad29-a069e9dcbb46" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq.Expressions;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Reflection;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> QueryFilterComplete
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> QueryFilter
    {

        </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
        <span style="color: #808080;">///</span><span style="color: #008000;"> 查询条件过滤
        </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
        <span style="color: #808080;">///</span> <span style="color: #808080;">&lt;typeparam name="T"&gt;&lt;/typeparam&gt;</span>
        <span style="color: #808080;">///</span> <span style="color: #808080;">&lt;param name="t"&gt;&lt;/param&gt;</span>
        <span style="color: #808080;">///</span> <span style="color: #808080;">&lt;param name="valNames"&gt;</span><span style="color: #008000;">需要过滤的字段</span><span style="color: #808080;">&lt;/param&gt;</span>
        <span style="color: #808080;">///</span> <span style="color: #808080;">&lt;param name="vagueNames"&gt;</span><span style="color: #008000;">需要模糊查询的字段</span><span style="color: #808080;">&lt;/param&gt;</span>
        <span style="color: #808080;">///</span> <span style="color: #808080;">&lt;param name="isIgnoreZero"&gt;</span><span style="color: #008000;">true：忽略0</span><span style="color: #808080;">&lt;/param&gt;</span>
        <span style="color: #808080;">///</span> <span style="color: #808080;">&lt;returns&gt;&lt;/returns&gt;</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> Expression&lt;Func&lt;T, Boolean&gt;&gt; Filter&lt;T,Twhere&gt;(Twhere t, IEnumerable&lt;<span style="color: #0000ff;">string</span>&gt; valNames, IEnumerable&lt;<span style="color: #0000ff;">string</span>&gt; vagueNames, <span style="color: #0000ff;">bool</span> isIgnoreZero = <span style="color: #0000ff;">true</span>) <span style="color: #0000ff;">where</span> T : <span style="color: #0000ff;">class</span> <span style="color: #0000ff;">where</span> Twhere:<span style="color: #0000ff;">class</span><span style="color: #000000;">
        {
            Expression</span>&lt;Func&lt;T, Boolean&gt;&gt; e = r =&gt; <span style="color: #0000ff;">true</span><span style="color: #000000;">;
            </span><span style="color: #0000ff;">foreach</span> (<span style="color: #0000ff;">var</span> item <span style="color: #0000ff;">in</span><span style="color: #000000;"> valNames)
            {
                </span><span style="color: #0000ff;">var</span> result =<span style="color: #000000;"> GetFilterType(item, vagueNames);
                </span><span style="color: #0000ff;">if</span> (result.Item1 == QFilterType.None) <span style="color: #0000ff;">continue</span><span style="color: #000000;">;
                PropertyInfo property </span>= <span style="color: #0000ff;">typeof</span><span style="color: #000000;">(Twhere).GetProperty(item);
                </span><span style="color: #0000ff;">var</span> value =<span style="color: #000000;"> property.GetValue(t);
                </span><span style="color: #0000ff;">if</span> (!Validate(property.PropertyType, value, isIgnoreZero)) <span style="color: #0000ff;">continue</span><span style="color: #000000;">;

                </span><span style="color: #0000ff;">var</span> rE = Expression.Parameter(<span style="color: #0000ff;">typeof</span>(T), <span style="color: #800000;">"</span><span style="color: #800000;">r</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                </span><span style="color: #0000ff;">var</span> propertyE =<span style="color: #000000;"> Expression.Property(rE, result.Item2);
                </span><span style="color: #0000ff;">var</span> valueE =<span style="color: #000000;"> Expression.Constant(value);
                </span><span style="color: #0000ff;">var</span> lambda = Expression.Lambda&lt;Func&lt;T, Boolean&gt;&gt;<span style="color: #000000;">(ComputeExpression(result.Item1, t, property, propertyE, valueE), rE);
                </span><span style="color: #0000ff;">var</span> invoke =<span style="color: #000000;"> Expression.Invoke(lambda, e.Parameters);
                e </span>= Expression.Lambda&lt;Func&lt;T, Boolean&gt;&gt;<span style="color: #000000;">(Expression.AndAlso(e.Body, invoke), e.Parameters);
            }
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> e;
        }
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">bool</span> Validate(Type t,<span style="color: #0000ff;">object</span> value, <span style="color: #0000ff;">bool</span><span style="color: #000000;"> isIgnoreZero)
        {
            </span><span style="color: #0000ff;">if</span> (value == <span style="color: #0000ff;">null</span>) <span style="color: #0000ff;">return</span> <span style="color: #0000ff;">false</span><span style="color: #000000;">;
            </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (t.IsValueType)
            {
                </span><span style="color: #0000ff;">if</span> (t == <span style="color: #0000ff;">typeof</span>(DateTime)) <span style="color: #0000ff;">return</span> <span style="color: #0000ff;">true</span><span style="color: #000000;">;
                </span><span style="color: #0000ff;">if</span> (t == <span style="color: #0000ff;">typeof</span>(<span style="color: #0000ff;">bool</span>)) <span style="color: #0000ff;">return</span> <span style="color: #0000ff;">true</span><span style="color: #000000;">;
                </span><span style="color: #0000ff;">if</span> (Convert.ToDouble(value) == <span style="color: #800080;">0</span> &amp;&amp; isIgnoreZero) <span style="color: #0000ff;">return</span> <span style="color: #0000ff;">false</span><span style="color: #000000;">;
            }
            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">true</span><span style="color: #000000;">;
        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;">获取过滤类型</span>
        <span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> Tuple&lt;QFilterType, <span style="color: #0000ff;">string</span>&gt; GetFilterType(<span style="color: #0000ff;">string</span> valName, IEnumerable&lt;<span style="color: #0000ff;">string</span>&gt;<span style="color: #000000;"> vagueNames)
        {
            QFilterType type </span>=<span style="color: #000000;"> QFilterType.None;
            </span><span style="color: #0000ff;">string</span> propertyName = <span style="color: #800000;">""</span><span style="color: #000000;">;
            </span><span style="color: #0000ff;">if</span> (<span style="color: #0000ff;">string</span><span style="color: #000000;">.IsNullOrEmpty(valName)) {
                </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> Tuple.Create(type, propertyName);
            }
            type </span>=<span style="color: #000000;"> QFilterType.Equal;
            propertyName </span>=<span style="color: #000000;"> valName;
            </span><span style="color: #0000ff;">if</span> (valName.EndsWith(<span style="color: #800000;">"</span><span style="color: #800000;">_ge</span><span style="color: #800000;">"</span><span style="color: #000000;">))
            {
                type </span>=<span style="color: #000000;"> QFilterType.ge;
                propertyName </span>= valName.TrimEnd(<span style="color: #800000;">'</span><span style="color: #800000;">_</span><span style="color: #800000;">'</span>, <span style="color: #800000;">'</span><span style="color: #800000;">g</span><span style="color: #800000;">'</span>, <span style="color: #800000;">'</span><span style="color: #800000;">e</span><span style="color: #800000;">'</span><span style="color: #000000;">);
            }
            </span><span style="color: #0000ff;">if</span> (valName.EndsWith(<span style="color: #800000;">"</span><span style="color: #800000;">_gt</span><span style="color: #800000;">"</span><span style="color: #000000;">))
            {
                type </span>=<span style="color: #000000;"> QFilterType.gt;
                propertyName </span>= valName.TrimEnd(<span style="color: #800000;">'</span><span style="color: #800000;">_</span><span style="color: #800000;">'</span>, <span style="color: #800000;">'</span><span style="color: #800000;">g</span><span style="color: #800000;">'</span>, <span style="color: #800000;">'</span><span style="color: #800000;">t</span><span style="color: #800000;">'</span><span style="color: #000000;">);
            }
            </span><span style="color: #0000ff;">if</span> (valName.EndsWith(<span style="color: #800000;">"</span><span style="color: #800000;">_le</span><span style="color: #800000;">"</span><span style="color: #000000;">))
            {
                type </span>=<span style="color: #000000;"> QFilterType.le;
                propertyName </span>= valName.TrimEnd(<span style="color: #800000;">'</span><span style="color: #800000;">_</span><span style="color: #800000;">'</span>, <span style="color: #800000;">'</span><span style="color: #800000;">l</span><span style="color: #800000;">'</span>, <span style="color: #800000;">'</span><span style="color: #800000;">e</span><span style="color: #800000;">'</span><span style="color: #000000;">);
            }
            </span><span style="color: #0000ff;">if</span> (valName.EndsWith(<span style="color: #800000;">"</span><span style="color: #800000;">_lt</span><span style="color: #800000;">"</span><span style="color: #000000;">))
            {
                type </span>=<span style="color: #000000;"> QFilterType.lt;
                propertyName </span>= valName.TrimEnd(<span style="color: #800000;">'</span><span style="color: #800000;">_</span><span style="color: #800000;">'</span>, <span style="color: #800000;">'</span><span style="color: #800000;">l</span><span style="color: #800000;">'</span>, <span style="color: #800000;">'</span><span style="color: #800000;">t</span><span style="color: #800000;">'</span><span style="color: #000000;">);
            }
            </span><span style="color: #0000ff;">if</span> (valName.EndsWith(<span style="color: #800000;">"</span><span style="color: #800000;">_ne</span><span style="color: #800000;">"</span><span style="color: #000000;">))
            {
                type </span>=<span style="color: #000000;"> QFilterType.ne;
                propertyName </span>= valName.TrimEnd(<span style="color: #800000;">'</span><span style="color: #800000;">_</span><span style="color: #800000;">'</span>, <span style="color: #800000;">'</span><span style="color: #800000;">n</span><span style="color: #800000;">'</span>, <span style="color: #800000;">'</span><span style="color: #800000;">e</span><span style="color: #800000;">'</span><span style="color: #000000;">);
            }
            </span><span style="color: #0000ff;">if</span> (valName.EndsWith(<span style="color: #800000;">"</span><span style="color: #800000;">_csv</span><span style="color: #800000;">"</span><span style="color: #000000;">))
            {
                type </span>=<span style="color: #000000;"> QFilterType.csv;
                propertyName </span>= valName.TrimEnd(<span style="color: #800000;">'</span><span style="color: #800000;">_</span><span style="color: #800000;">'</span>, <span style="color: #800000;">'</span><span style="color: #800000;">c</span><span style="color: #800000;">'</span>, <span style="color: #800000;">'</span><span style="color: #800000;">s</span><span style="color: #800000;">'</span>, <span style="color: #800000;">'</span><span style="color: #800000;">v</span><span style="color: #800000;">'</span><span style="color: #000000;">);
            }
            </span><span style="color: #0000ff;">if</span> (vagueNames!=<span style="color: #0000ff;">null</span>&amp;&amp;<span style="color: #000000;">vagueNames.Contains(valName))
            {
                type </span>=<span style="color: #000000;"> QFilterType.VaguesEqual;
                propertyName </span>=<span style="color: #000000;"> valName;
            }
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> Tuple.Create(type, propertyName);
        }
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> Expression ComputeExpression&lt;T&gt;<span style="color: #000000;">(QFilterType type,T t, PropertyInfo pInfo, Expression propertyE, Expression valueE)
        {
            </span><span style="color: #0000ff;">if</span> (type ==<span style="color: #000000;"> QFilterType.Equal)
            {
                </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> Expression.Equal(propertyE, valueE);
            }
            </span><span style="color: #0000ff;">if</span> (type ==<span style="color: #000000;"> QFilterType.VaguesEqual)
            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;">Console.WriteLine(Expression.Call(typeof(Program), "VaguesEqual", null, p, value));</span>
                <span style="color: #0000ff;">return</span> Expression.Call(<span style="color: #0000ff;">typeof</span>(QueryFilter), <span style="color: #800000;">"</span><span style="color: #800000;">VaguesEqual</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">null</span><span style="color: #000000;">, propertyE, valueE);
            }
            </span><span style="color: #0000ff;">if</span> (type ==<span style="color: #000000;"> QFilterType.ge)
            {
                </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> Expression.GreaterThanOrEqual(propertyE, valueE);
            }
            </span><span style="color: #0000ff;">if</span> (type ==<span style="color: #000000;"> QFilterType.gt)
            {
                </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> Expression.GreaterThan(propertyE, valueE);
            }
            </span><span style="color: #0000ff;">if</span> (type ==<span style="color: #000000;"> QFilterType.le)
            {
                </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> Expression.LessThanOrEqual(propertyE, valueE);
            }
            </span><span style="color: #0000ff;">if</span> (type ==<span style="color: #000000;"> QFilterType.lt)
            {
                </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> Expression.LessThan(propertyE, valueE);
            }
            </span><span style="color: #0000ff;">if</span> (type ==<span style="color: #000000;"> QFilterType.ne)
            {
                </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> Expression.NotEqual(propertyE, valueE);
            }
            </span><span style="color: #0000ff;">if</span> (type ==<span style="color: #000000;"> QFilterType.csv)
            {
                </span><span style="color: #0000ff;">if</span> (pInfo.PropertyType.GetGenericTypeDefinition()==<span style="color: #0000ff;">typeof</span>(IEnumerable&lt;&gt;) || pInfo.PropertyType.IsSubclassOf(<span style="color: #0000ff;">typeof</span>(IEnumerable&lt;&gt;<span style="color: #000000;">)))
                {
                    </span><span style="color: #0000ff;">return</span> Expression.Call(<span style="color: #0000ff;">typeof</span>(QueryFilter), <span style="color: #800000;">"</span><span style="color: #800000;">VaguesEqual</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span> Type[] { pInfo.PropertyType.GenericTypeArguments[<span style="color: #800080;">0</span><span style="color: #000000;">] },Expression.Constant(pInfo.GetValue(t)), propertyE);
                }
            }
            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">null</span><span style="color: #000000;">;
        }

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">bool</span> VaguesEqual&lt;T&gt;(IEnumerable&lt;T&gt;<span style="color: #000000;"> t, T value)
        {
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> t.Contains(value);
        }
        </span><span style="color: #008000;">//</span><span style="color: #008000;">模糊匹配</span>
        <span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">bool</span> VaguesEqual(<span style="color: #0000ff;">string</span> t, <span style="color: #0000ff;">string</span><span style="color: #000000;"> value)
        {
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> t.Contains(value);
        }

    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<p>下载地址v1：<a href="http://pan.baidu.com/s/1jI1I2MU" target="_blank">http://pan.baidu.com/s/1jI1I2MU</a></p>
<p>&nbsp;</p>