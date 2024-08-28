<div class="cnblogs_code">
<pre><span style="color: #000000;">[Serializable,StructLayout(LayoutKind.Sequential)]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">struct</span> Nullable&lt;T&gt; <span style="color: #0000ff;">where</span> T : <span style="color: #0000ff;">struct</span><span style="color: #000000;">
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;">这两个字段标识状态</span>
        <span style="color: #0000ff;">private</span> Boolean hasValue = <span style="color: #0000ff;">false</span>;<span style="color: #008000;">//</span><span style="color: #008000;">假定null</span>
        <span style="color: #0000ff;">internal</span> T value = <span style="color: #0000ff;">default</span>(T);<span style="color: #008000;">//</span><span style="color: #008000;">假定所有位都为零</span>

        <span style="color: #0000ff;">public</span><span style="color: #000000;"> Nullable(T value)
        {
            </span><span style="color: #0000ff;">this</span>.value =<span style="color: #000000;"> value;
            hasValue </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">;
        }

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> T GetValueOrDefault()
        {
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> value;
        }

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> T GetValueOrDefault(T defaultValue)
        {
            </span><span style="color: #0000ff;">if</span> (!hasValue) <span style="color: #0000ff;">return</span><span style="color: #000000;"> defaultValue;
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> value;
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">bool</span> Equals(<span style="color: #0000ff;">object</span><span style="color: #000000;"> obj)
        {
            </span><span style="color: #0000ff;">if</span> (!hasValue) <span style="color: #0000ff;">return</span> obj == <span style="color: #0000ff;">null</span><span style="color: #000000;">;
            </span><span style="color: #0000ff;">if</span> (obj == <span style="color: #0000ff;">null</span>) <span style="color: #0000ff;">return</span> <span style="color: #0000ff;">false</span><span style="color: #000000;">;
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> value.Equals(obj);
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">int</span><span style="color: #000000;"> GetHashCode()
        {
            </span><span style="color: #0000ff;">if</span> (!hasValue) <span style="color: #0000ff;">return</span> <span style="color: #800080;">0</span><span style="color: #000000;">;
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> value.GetHashCode();
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">string</span><span style="color: #000000;"> ToString()
        {
            </span><span style="color: #0000ff;">if</span> (!hasValue) <span style="color: #0000ff;">return</span> <span style="color: #800000;">""</span><span style="color: #000000;">;
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> value.ToString();
        }
        </span><span style="color: #008000;">//</span><span style="color: #008000;">隐式转换</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">implicit</span> <span style="color: #0000ff;">operator</span> Nullable&lt;T&gt;<span style="color: #000000;">(T value)
        {
            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> Nullable&lt;T&gt;<span style="color: #000000;">(value);
        }
        </span><span style="color: #008000;">//</span><span style="color: #008000;">显式装换</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">explicit</span> <span style="color: #0000ff;">operator</span> T(Nullable&lt;T&gt;<span style="color: #000000;"> value)
        {
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> value.value;
        }
    }</span></pre>
</div>
<p>&nbsp;</p>