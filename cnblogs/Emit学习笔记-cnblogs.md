<p>1，给字段设置值，并返回</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">给字段设置值，并返回</span>
            AssemblyName assemblyName = <span style="color: #0000ff;">new</span> AssemblyName(<span style="color: #800000;">"</span><span style="color: #800000;">test</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            </span><span style="color: #0000ff;">var</span> assemblyBuilder =<span style="color: #000000;"> AppDomain.CurrentDomain.DefineDynamicAssembly(assemblyName, AssemblyBuilderAccess.RunAndSave);
            </span><span style="color: #0000ff;">var</span> module = assemblyBuilder.DefineDynamicModule(<span style="color: #800000;">"</span><span style="color: #800000;">test_module</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            </span><span style="color: #0000ff;">var</span> typeBuilder = module.DefineType(<span style="color: #800000;">"</span><span style="color: #800000;">produce_123</span><span style="color: #800000;">"</span>, TypeAttributes.Class | TypeAttributes.Public |<span style="color: #000000;"> TypeAttributes.Sealed);
            </span><span style="color: #0000ff;">var</span> method = typeBuilder.DefineMethod(<span style="color: #800000;">"</span><span style="color: #800000;">aa</span><span style="color: #800000;">"</span>, MethodAttributes.Public, CallingConventions.Standard, <span style="color: #0000ff;">typeof</span>(<span style="color: #0000ff;">string</span>), <span style="color: #0000ff;">new</span> Type[] { <span style="color: #0000ff;">typeof</span>(<span style="color: #0000ff;">string</span><span style="color: #000000;">) });
            </span><span style="color: #0000ff;">var</span> fb = typeBuilder.DefineField(<span style="color: #800000;">"</span><span style="color: #800000;">bb</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">typeof</span>(<span style="color: #0000ff;">string</span><span style="color: #000000;">), FieldAttributes.Public);

            </span><span style="color: #0000ff;">var</span> li=<span style="color: #000000;"> method.GetILGenerator();
            li.Emit(OpCodes.Ldarg_0);</span><span style="color: #008000;">//</span><span style="color: #008000;">获取this</span>
            li.Emit(OpCodes.Ldarg_1);<span style="color: #008000;">//</span><span style="color: #008000;">获取aa方法的第一个参数</span>
            li.Emit(OpCodes.Stfld, fb);<span style="color: #008000;">//</span><span style="color: #008000;">设置bb字段的值</span>
            li.Emit(OpCodes.Ldarg_0);<span style="color: #008000;">//</span><span style="color: #008000;">获取this</span>
            li.Emit(OpCodes.Ldfld, fb);<span style="color: #008000;">//</span><span style="color: #008000;">将bb字段压入栈</span>
            li.Emit(OpCodes.Ret);<span style="color: #008000;">//</span><span style="color: #008000;">返回值</span>

            <span style="color: #0000ff;">var</span> type =<span style="color: #000000;"> typeBuilder.CreateType();
            </span><span style="color: #0000ff;">var</span> obj=<span style="color: #000000;">Activator.CreateInstance(type);

            </span><span style="color: #0000ff;">var</span> aa= type.GetMethod(<span style="color: #800000;">"</span><span style="color: #800000;">aa</span><span style="color: #800000;">"</span>).Invoke(obj, <span style="color: #0000ff;">new</span> <span style="color: #0000ff;">object</span>[] { <span style="color: #800000;">"</span><span style="color: #800000;">aa</span><span style="color: #800000;">"</span><span style="color: #000000;"> });
            Console.WriteLine(aa);
            Console.ReadKey();
        }</span></pre>
</div>
<p>&nbsp;</p>