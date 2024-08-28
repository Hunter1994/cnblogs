<p style="background-color: #169fe6;"><span style="font-size: 18pt;"><strong><span style="color: #ffffff;">一、什么是&ldquo;公共语言规范&rdquo;（CLS）</span></strong></span></p>
<p>&nbsp;定义了一个最小公共集，任何编译器只有支持这个功能集，生成的类型才能兼容其他符合CLS、面向CLR的语言生成的组件</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt;"><strong><span style="color: #ffffff;">二、CLS规则</span></strong></span></p>
<p>类型的每个成员要么是字段（数据），要么是方法（行为），为简化编程，语言往往提供了额外的抽象</p>
<div class="cnblogs_code">
<pre> <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Test
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;">构造器</span>
        <span style="color: #0000ff;">public</span><span style="color: #000000;"> Test()
        {
        }
        </span><span style="color: #008000;">//</span><span style="color: #008000;">终结器</span>
        ~<span style="color: #000000;">Test()
        {
        }
        </span><span style="color: #008000;">//</span><span style="color: #008000;">操作符重载</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> Boolean <span style="color: #0000ff;">operator</span> ==<span style="color: #000000;">(Test t1, Test t2)
        {
            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">true</span><span style="color: #000000;">;
        }
        
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> Boolean <span style="color: #0000ff;">operator</span> !=<span style="color: #000000;">(Test t1, Test t2)
        {
            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">false</span><span style="color: #000000;">;
        }
        
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> Test <span style="color: #0000ff;">operator</span> +<span style="color: #000000;">(Test t1, Test t2)
        {
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> t1;
        }
        </span><span style="color: #008000;">//</span><span style="color: #008000;">属性</span>

        <span style="color: #0000ff;">public</span><span style="color: #000000;"> String AProperty {
            </span><span style="color: #0000ff;">get</span> { <span style="color: #0000ff;">return</span> <span style="color: #0000ff;">null</span><span style="color: #000000;">; }
            </span><span style="color: #0000ff;">set</span><span style="color: #000000;"> { }
        }
        </span><span style="color: #008000;">//</span><span style="color: #008000;">索引器</span>
        <span style="color: #0000ff;">public</span> String <span style="color: #0000ff;">this</span>[<span style="color: #0000ff;">int</span><span style="color: #000000;"> index]
        {
            </span><span style="color: #0000ff;">get</span> { <span style="color: #0000ff;">return</span> <span style="color: #0000ff;">null</span><span style="color: #000000;">; }
            </span><span style="color: #0000ff;">set</span><span style="color: #000000;"> { }
        }
        </span><span style="color: #008000;">//</span><span style="color: #008000;">事件</span>
        <span style="color: #0000ff;">event</span><span style="color: #000000;"> EventHandler AnEvent;
    }</span></pre>
</div>
<p><img src="http://images2015.cnblogs.com/blog/741594/201701/741594-20170122203834535-2026260509.jpg" alt="" /></p>
<p>该类型还有另一些节点未列出，包括.class、.custom、AnEvent、AProperty以及Item--他们标识了类型的其他元数据。这些节点不映射到字段或方法，只是提供了类型的一些额外的信息，供CLR、编程语言或工具访问。例如工具可以检测到该类型提供了一个名为AnEvent的事件，该事件借由两个方法（add_AEvent和remove_AEvent）公开</p>
<p>&nbsp;</p>