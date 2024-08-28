<p style="font-size: 18pt; background-color: #169fe6;"><strong><span style="color: #ffffff;">一、Elasticsearch内置分词器</span></strong></p>
<pre><code>#Simple Analyzer &ndash; 按照非字母切分（符号被过滤），小写处理
#Stop Analyzer &ndash; 小写处理，停用词过滤（the，a，is）
#Whitespace Analyzer &ndash; 按照空格切分，不转小写
#Keyword Analyzer &ndash; 不分词，直接将输入当作输出
#Patter Analyzer &ndash; 正则表达式，默认 \W+ (非字符分隔)
#Language &ndash; 提供了30多种常见语言的分词器</code></pre>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;1，Standard Analyzer</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202004/741594-20200406222329964-460682138.png" alt="" width="515" height="288" /></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>2， Simple&nbsp;Analyzer</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202004/741594-20200406222402465-1422322316.png" alt="" /></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;3，Whitespace&nbsp;Analyzer</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202004/741594-20200406222616386-1476222651.png" alt="" /></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;4，Stop Analyzer</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202004/741594-20200406222833590-1656773120.png" alt="" /></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;&nbsp;5，Keywork&nbsp;Analyzer</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202004/741594-20200406222941098-723503115.png" alt="" /></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;6，Pattern&nbsp;Analyzer</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202004/741594-20200406223213025-674972192.jpg" alt="" /></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('536fcc1d-0076-4567-a77b-03e76ef3ce10')"><img id="code_img_closed_536fcc1d-0076-4567-a77b-03e76ef3ce10" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_536fcc1d-0076-4567-a77b-03e76ef3ce10" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('536fcc1d-0076-4567-a77b-03e76ef3ce10',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_536fcc1d-0076-4567-a77b-03e76ef3ce10" class="cnblogs_code_hide">
<pre><span style="color: #000000;">#Simple Analyzer &ndash; 按照非字母切分（符号被过滤），小写处理
#Stop Analyzer &ndash; 小写处理，停用词过滤（the，a，</span><span style="color: #0000ff;">is</span><span style="color: #000000;">）
#Whitespace Analyzer &ndash; 按照空格切分，不转小写
#Keyword Analyzer &ndash; 不分词，直接将输入当作输出
#Patter Analyzer &ndash; 正则表达式，默认 \W</span>+<span style="color: #000000;"> (非字符分隔)
#Language &ndash; 提供了30多种常见语言的分词器
#</span><span style="color: #800080;">2</span> running Quick brown-foxes leap over lazy dogs <span style="color: #0000ff;">in</span><span style="color: #000000;"> the summer evening

#查看不同的analyzer的效果
#standard
GET _analyze
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">analyzer</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">standard</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">2 running Quick brown-foxes leap over lazy dogs in the summer evening.</span><span style="color: #800000;">"</span><span style="color: #000000;">
}

#simpe
GET _analyze
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">analyzer</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">simple</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">2 running Quick brown-foxes leap over lazy dogs in the summer evening.</span><span style="color: #800000;">"</span><span style="color: #000000;">
}


GET _analyze
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">analyzer</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">stop</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">2 running Quick brown-foxes leap over lazy dogs in the summer evening.</span><span style="color: #800000;">"</span><span style="color: #000000;">
}


#stop
GET _analyze
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">analyzer</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">whitespace</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">2 running Quick brown-foxes leap over lazy dogs in the summer evening.</span><span style="color: #800000;">"</span><span style="color: #000000;">
}

#keyword
GET _analyze
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">analyzer</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">keyword</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">2 running Quick brown-foxes leap over lazy dogs in the summer evening.</span><span style="color: #800000;">"</span><span style="color: #000000;">
}

GET _analyze
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">analyzer</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">pattern</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">2 running Quick brown-foxes leap over lazy dogs in the summer evening.</span><span style="color: #800000;">"</span><span style="color: #000000;">
}


#english
GET _analyze
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">analyzer</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">english</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">2 running Quick brown-foxes leap over lazy dogs in the summer evening.</span><span style="color: #800000;">"</span><span style="color: #000000;">
}


POST _analyze
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">analyzer</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">icu_analyzer</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">他说的确实在理&rdquo;</span><span style="color: #800000;">"</span><span style="color: #000000;">
}


POST _analyze
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">analyzer</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">standard</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">他说的确实在理&rdquo;</span><span style="color: #800000;">"</span><span style="color: #000000;">
}


POST _analyze
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">analyzer</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">icu_analyzer</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">这个苹果不大好吃</span><span style="color: #800000;">"</span><span style="color: #000000;">
}</span></pre>
</div>
<span class="cnblogs_code_collapse">demo</span></div>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: #169fe6;"><strong><span style="color: #ffffff;">二、中文分词 ICU&nbsp;Analyzer</span></strong></p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202004/741594-20200406223941469-1098431685.jpg" alt="" /></p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">直接指定analyze进行测试</span>
<span style="color: #000000;">GET _analyze
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">analyzer</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">icu_analyzer</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">你好中国</span><span style="color: #800000;">"</span><span style="color: #000000;">
}</span></pre>
</div>
<p>2，其他中文分词插件</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202004/741594-20200406224140407-894395935.jpg" alt="" /></p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: #169fe6;"><span style="color: #ffffff;"><strong>三、自定义Analyzer</strong></span></p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202004/741594-20200412003352689-1691205670.png" alt="" /></p>
<p>&nbsp;</p>
<p>&nbsp;<img src="https://img2020.cnblogs.com/blog/741594/202004/741594-20200412003429873-1978773320.png" alt="" /></p>
<p>&nbsp;</p>
<p>&nbsp;<img src="https://img2020.cnblogs.com/blog/741594/202004/741594-20200412003529705-532621280.png" alt="" /></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">自定义分词器</span>
PUT /<span style="color: #000000;">my_index
{
    </span><span style="color: #800000;">"</span><span style="color: #800000;">settings</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">analysis</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
            </span><span style="color: #800000;">"</span><span style="color: #800000;">char_filter</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
                </span><span style="color: #800000;">"</span><span style="color: #800000;">&amp;_to_and</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
                    </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">mapping</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    </span><span style="color: #800000;">"</span><span style="color: #800000;">mappings</span><span style="color: #800000;">"</span>: [ <span style="color: #800000;">"</span><span style="color: #800000;">&amp;=&gt; and </span><span style="color: #800000;">"</span><span style="color: #000000;">]
            }},
            </span><span style="color: #800000;">"</span><span style="color: #800000;">filter</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
                </span><span style="color: #800000;">"</span><span style="color: #800000;">my_stopwords</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
                    </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">stop</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    </span><span style="color: #800000;">"</span><span style="color: #800000;">stopwords</span><span style="color: #800000;">"</span>: [ <span style="color: #800000;">"</span><span style="color: #800000;">the</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">a</span><span style="color: #800000;">"</span><span style="color: #000000;"> ]
            }},
            </span><span style="color: #800000;">"</span><span style="color: #800000;">analyzer</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
                </span><span style="color: #800000;">"</span><span style="color: #800000;">my_analyzer</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
                    </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">custom</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    </span><span style="color: #800000;">"</span><span style="color: #800000;">char_filter</span><span style="color: #800000;">"</span>: [ <span style="color: #800000;">"</span><span style="color: #800000;">html_strip</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">&amp;_to_and</span><span style="color: #800000;">"</span><span style="color: #000000;"> ],
                    </span><span style="color: #800000;">"</span><span style="color: #800000;">tokenizer</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">standard</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    </span><span style="color: #800000;">"</span><span style="color: #800000;">filter</span><span style="color: #800000;">"</span>: [ <span style="color: #800000;">"</span><span style="color: #800000;">lowercase</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">my_stopwords</span><span style="color: #800000;">"</span><span style="color: #000000;"> ]
            }}
}}}

</span><span style="color: #008000;">//</span><span style="color: #008000;">设置mapping</span>
PUT /my_index/<span style="color: #000000;">_mapping
{
   </span><span style="color: #800000;">"</span><span style="color: #800000;">properties</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">username</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
             </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span><span style="color: #000000;">,
             </span><span style="color: #800000;">"</span><span style="color: #800000;">analyzer</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">my_analyzer</span><span style="color: #800000;">"</span><span style="color: #000000;">
         },
        </span><span style="color: #800000;">"</span><span style="color: #800000;">password</span><span style="color: #800000;">"</span><span style="color: #000000;"> : {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span><span style="color: #000000;">
        }
    
  }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">插入数据</span>
PUT /my_index/_doc/<span style="color: #800080;">1</span><span style="color: #000000;">
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">username</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">The quick &amp; brown fox </span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">password</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">The quick &amp; brown fox </span><span style="color: #800000;">"</span><span style="color: #000000;">
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">验证</span>
GET my_index/<span style="color: #000000;">_analyze
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">username</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">The quick &amp; brown fox</span><span style="color: #800000;">"</span><span style="color: #000000;">
}

GET my_index</span>/<span style="color: #000000;">_analyze
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">password</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">The quick &amp; brown fox</span><span style="color: #800000;">"</span><span style="color: #000000;">
}</span></pre>
</div>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: #169fe6;"><span style="color: #ffffff;"><strong>四、ik分词插件</strong></span></p>
<p>1，下载地址：<a href="https://github.com/medcl/elasticsearch-analysis-ik/releases" target="_blank">https://github.com/medcl/elasticsearch-analysis-ik/releases</a></p>
<p>需要下载与el版本一致的分词器版本</p>
<p>2，plugins文件夹下面创建一个analysis-ik目录</p>
<p>3，将下载的zip文件copy到analysis-ik目录下，执行unzip</p>
<p>4，运行es</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">ik_max_word
</span><span style="color: #008000;">//</span><span style="color: #008000;">ik_smart</span>
<span style="color: #000000;">POST _analyze
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">analyzer</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">ik_max_word</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span>: [<span style="color: #800000;">"</span><span style="color: #800000;">剑桥分析公司多位高管对卧底记者说，他们确保了唐纳德&middot;特朗普在总统大选中获胜</span><span style="color: #800000;">"</span><span style="color: #000000;">]
} </span></pre>
</div>
<p>hanlp分词插件</p>
<p>1，下载地址：<a href="https://github.com/KennFalcon/elasticsearch-analysis-hanlp" target="_blank">https://github.com/KennFalcon/elasticsearch-analysis-hanlp</a></p>
<p>&nbsp;</p>