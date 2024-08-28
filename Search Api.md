<table style="height: 117px; width: 554px;" border="1">
<tbody>
<tr>
<td>语法</td>
<td>范围</td>
</tr>
<tr>
<td>/_search</td>
<td>集群上所有的索引</td>
</tr>
<tr>
<td>/index1/_search</td>
<td>index1</td>
</tr>
<tr>
<td>/index1,index2/_search</td>
<td>index1,index2</td>
</tr>
<tr>
<td>/index*/_search</td>
<td>以index开头的索引</td>
</tr>
</tbody>
</table>
<p><strong>Term ：</strong>Beautiful Mind 等效于&nbsp;Beautiful OR Mind。使用括号括起来：(Beautiful Mind)</p>
<p><strong>Phrase：</strong>"Beautiful Mind" 等效于&nbsp;Beautiful AND Mind 。Phrase查询还要求前后顺序保持一致。使用引号</p>
<p style="font-size: 18pt; background-color: #169fe6;"><strong><span style="color: #ffffff;">一、Url&nbsp;Search&nbsp;</span></strong></p>
<p>在url中使用查询参数</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">查询title字段包含2013的</span>
GET movies/_search?q=<span style="color: #800080;">2012</span>&amp;df=<span style="color: #000000;">title
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">profile</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">true</span><span style="color: #800000;">"</span><span style="color: #000000;">
}
</span><span style="color: #008000;">//</span><span style="color: #008000;">查询title字段包含2013的</span>
GET movies/_search?q=title:<span style="color: #800080;">2012</span>&amp;sort=year:desc&amp;<span style="color: #0000ff;">from</span>=<span style="color: #800080;">0</span>&amp;size=<span style="color: #800080;">10</span>&amp;timeout=<span style="color: #000000;">1m
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">profile</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">true</span><span style="color: #800000;">"</span><span style="color: #000000;">
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">查询所有字段包含2013的</span>
GET movies/_search?q=<span style="color: #800080;">2012</span><span style="color: #000000;">
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">profile</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">true</span><span style="color: #800000;">"</span><span style="color: #000000;">
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">PhraseQuery</span>
GET movies/_search?q=title:<span style="color: #800000;">"</span><span style="color: #800000;">Beautiful Mind</span><span style="color: #800000;">"</span><span style="color: #000000;">
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">profile</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">true</span><span style="color: #800000;">"</span><span style="color: #000000;">
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">TermQuery。两个Term在一起默认是 OR 的关系</span>
GET movies/_search?q=<span style="color: #000000;">title:(Beautiful Mind)
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">profile</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">true</span><span style="color: #800000;">"</span><span style="color: #000000;">
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">title 必须包括Beautiful 和 Mind</span>
GET movies/_search?q=<span style="color: #000000;">title:(Beautiful AND Mind)
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">profile</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">true</span><span style="color: #800000;">"</span><span style="color: #000000;">
}
</span><span style="color: #008000;">//</span><span style="color: #008000;">title 必须包括Beautiful 和 Mind</span>
GET movies/_search?q=title:(Beautiful %<span style="color: #000000;">2BMind)
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">profile</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">true</span><span style="color: #800000;">"</span><span style="color: #000000;">
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">title 必须包括Beautiful 不能包括Mind</span>
GET movies/_search?q=<span style="color: #000000;">title:(Beautiful NOT Mind)
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">profile</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">true</span><span style="color: #800000;">"</span><span style="color: #000000;">
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">查询1980以后的电影</span>
GET movies/_search?q=year:&gt;=<span style="color: #800080;">1980</span><span style="color: #000000;">
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">profile</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">true</span><span style="color: #800000;">"</span><span style="color: #000000;">
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">title包含b开头的</span>
GET movies/_search?q=title:b*<span style="color: #000000;">
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">profile</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">true</span><span style="color: #800000;">"</span><span style="color: #000000;">
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">模糊匹配&amp;近似匹配</span>
GET movies/_search?q=title:beautifl~<span style="color: #800080;">1</span><span style="color: #000000;">
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">profile</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">true</span><span style="color: #800000;">"</span><span style="color: #000000;">
}
GET movies</span>/_search?q=title:<span style="color: #800000;">"</span><span style="color: #800000;">lord rings</span><span style="color: #800000;">"</span>~<span style="color: #800080;">2</span><span style="color: #000000;">
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">profile</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">true</span><span style="color: #800000;">"</span><span style="color: #000000;">
}</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: #169fe6;"><strong><span style="color: #ffffff;">二、Request Body&nbsp;Search&nbsp;</span></strong></p>
<p>使用elasticsearch提供的，基于json格式的更加完备的DSL</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> 分页查询第一页，每页1条数据</span>
GET kibana_sample_data_ecommerce/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">from</span><span style="color: #800000;">"</span>: <span style="color: #800080;">0</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>: <span style="color: #800080;">1</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">match_all</span><span style="color: #800000;">"</span><span style="color: #000000;">: {}
  }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">根据order_date倒序</span>
GET kibana_sample_data_ecommerce/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">sort</span><span style="color: #800000;">"</span>:[{<span style="color: #800000;">"</span><span style="color: #800000;">order_date</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">desc</span><span style="color: #800000;">"</span><span style="color: #000000;">}], 
  </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">match_all</span><span style="color: #800000;">"</span><span style="color: #000000;">: {}
  }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">只返回order_date字段</span>
GET kibana_sample_data_ecommerce/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">_source</span><span style="color: #800000;">"</span>: [<span style="color: #800000;">"</span><span style="color: #800000;">order_date</span><span style="color: #800000;">"</span><span style="color: #000000;">], 
  </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span>: {<span style="color: #800000;">"</span><span style="color: #800000;">match_all</span><span style="color: #800000;">"</span><span style="color: #000000;">: {}}
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">脚本字段，新增一个new_field字段</span>
GET kibana_sample_data_ecommerce/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">script_fields</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">new_field</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">script</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">lang</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">painless</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">source</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">doc['order_date'].value+'_hello'</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    }
  }, 
  </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span>: {<span style="color: #800000;">"</span><span style="color: #800000;">match_all</span><span style="color: #800000;">"</span><span style="color: #000000;">: {}}
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">查询包含Last或者包含Christmas</span>
GET movies/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">match</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">title</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">Last Christmas</span><span style="color: #800000;">"</span><span style="color: #000000;">
    }
  }
  , </span><span style="color: #800000;">"</span><span style="color: #800000;">profile</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">true</span><span style="color: #800000;">"</span><span style="color: #000000;">
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">查询即包含Last又包含Christmas</span>
GET movies/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">match</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">title</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">Christmas Last</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">operator</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">and</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    }
  }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">slop 指定中间忽略匹配的数量。搜索出的结果：One I Love, The</span>
GET movies/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">match_phrase</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">title</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">one love</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">slop</span><span style="color: #800000;">"</span>: <span style="color: #800080;">1</span><span style="color: #000000;">
      }
    }
  }
  
}</span></pre>
</div>
<p><strong>1，Query String&amp;Simple&nbsp;&nbsp;Query String</strong></p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">title包含Homeward和Bound</span>
GET movies/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">query_string</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">default_field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">title</span><span style="color: #800000;">"</span><span style="color: #000000;">,
      </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">Homeward AND Bound</span><span style="color: #800000;">"</span><span style="color: #000000;">
    }
  }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">title包含Homeward和Bound 或者 包含Lost和in</span>
GET movies/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">query_string</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">default_field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">title</span><span style="color: #800000;">"</span><span style="color: #000000;">,
      </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">(Homeward AND Bound) or (Lost and in)</span><span style="color: #800000;">"</span><span style="color: #000000;">
    }
  }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">title包含Homeward和Bound </span>
GET movies/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">simple_query_string</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">Homeward Bound</span><span style="color: #800000;">"</span><span style="color: #000000;">,
      </span><span style="color: #800000;">"</span><span style="color: #800000;">fields</span><span style="color: #800000;">"</span>: [<span style="color: #800000;">"</span><span style="color: #800000;">title</span><span style="color: #800000;">"</span><span style="color: #000000;">],
      </span><span style="color: #800000;">"</span><span style="color: #800000;">default_operator</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">and</span><span style="color: #800000;">"</span><span style="color: #000000;">
    }
  }
}</span></pre>
</div>
<p>&nbsp;</p>
<p><strong>2，term查询</strong></p>
<p><span style="color: #505050; font-family: 'PingFang SC', 'Lantinghei SC', 'Microsoft Yahei', 'Hiragino Sans GB', 'Microsoft Sans Serif', 'WenQuanYi Micro Hei', Helvetica, sans-serif; background-color: #ffffff;">terms查询是用于结构化数据的查询。全文用match查询。而bool属于一种复合查询。可以结合terms查询和match查询</span></p>
<div class="cnblogs_code">
<pre>GET movies/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">term</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">title.keyword</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
            </span><span style="color: #800000;">"</span><span style="color: #800000;">value</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">Homeward Bound: The Incredible Journey</span><span style="color: #800000;">"</span><span style="color: #000000;">
          }
     }
  }
}</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">跳过算分，提高性能</span>
GET movies/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">constant_score</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">filter</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">term</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">title.keyword</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
            </span><span style="color: #800000;">"</span><span style="color: #800000;">value</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">Homeward Bound: The Incredible Journey</span><span style="color: #800000;">"</span><span style="color: #000000;">
          }
     }}
    }
  }
}</span></pre>
</div>
<div class="cnblogs_code">
<pre>GET request_audit_logs/<span style="color: #000000;">_search
{
   </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
     </span><span style="color: #800000;">"</span><span style="color: #800000;">bool</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
       </span><span style="color: #800000;">"</span><span style="color: #800000;">filter</span><span style="color: #800000;">"</span><span style="color: #000000;">: [
         {</span><span style="color: #800000;">"</span><span style="color: #800000;">term</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
           </span><span style="color: #800000;">"</span><span style="color: #800000;">url</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:18908/api/User/Login</span><span style="color: #800000;">"</span><span style="color: #000000;">
         }},
         {
           </span><span style="color: #800000;">"</span><span style="color: #800000;">match</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
             </span><span style="color: #800000;">"</span><span style="color: #800000;">request_content</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">15607172222</span><span style="color: #800000;">"</span><span style="color: #000000;">
           }
         },
         {
           </span><span style="color: #800000;">"</span><span style="color: #800000;">range</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
             </span><span style="color: #800000;">"</span><span style="color: #800000;">request_time</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
               </span><span style="color: #800000;">"</span><span style="color: #800000;">gte</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">2020-01-01 00:00:00</span><span style="color: #800000;">"</span><span style="color: #000000;">
             }
           }
         }
       ]
     }
   }
}</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p><strong>3，Query&amp;Filtering与多字符多字段查询</strong></p>
<p>gte：大等于<br />lte：小等于<br />gt：大于<br />lt：小于</p>
<table style="height: 182px; width: 624px;" border="1">
<tbody>
<tr>
<td>must</td>
<td>必须匹配。贡献算分</td>



























</tr>
<tr>
<td>should</td>
<td>选择性匹配。贡献算分</td>



























</tr>
<tr>
<td>must_not</td>
<td>
<p>Filter Context</p>
<p>查询字句，必须不能匹配</p>



























</td>



























</tr>
<tr>
<td>filter</td>
<td>
<p>Filter Context</p>
<p>必须匹配，但不贡献算分</p>



























</td>



























</tr>



























</tbody>



























</table>
<div class="cnblogs_code">
<pre>GET movies/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">bool</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">must</span><span style="color: #800000;">"</span>: {<span style="color: #800000;">"</span><span style="color: #800000;">term</span><span style="color: #800000;">"</span>: {<span style="color: #800000;">"</span><span style="color: #800000;">year</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">1960</span><span style="color: #800000;">"</span><span style="color: #000000;">}},
      </span><span style="color: #800000;">"</span><span style="color: #800000;">filter</span><span style="color: #800000;">"</span>: {<span style="color: #800000;">"</span><span style="color: #800000;">term</span><span style="color: #800000;">"</span>:{<span style="color: #800000;">"</span><span style="color: #800000;">title.keyword</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">Pollyanna</span><span style="color: #800000;">"</span><span style="color: #000000;">}},
      </span><span style="color: #800000;">"</span><span style="color: #800000;">must_not</span><span style="color: #800000;">"</span>:{<span style="color: #800000;">"</span><span style="color: #800000;">range</span><span style="color: #800000;">"</span>:{<span style="color: #800000;">"</span><span style="color: #800000;">year</span><span style="color: #800000;">"</span>:{<span style="color: #800000;">"</span><span style="color: #800000;">lte</span><span style="color: #800000;">"</span>:<span style="color: #800080;">1961</span><span style="color: #000000;">}}},
      </span><span style="color: #800000;">"</span><span style="color: #800000;">should</span><span style="color: #800000;">"</span><span style="color: #000000;">: [
        {</span><span style="color: #800000;">"</span><span style="color: #800000;">term</span><span style="color: #800000;">"</span>:{<span style="color: #800000;">"</span><span style="color: #800000;">genre.keyword</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">Children</span><span style="color: #800000;">"</span><span style="color: #000000;">}},
        {</span><span style="color: #800000;">"</span><span style="color: #800000;">term</span><span style="color: #800000;">"</span>:{<span style="color: #800000;">"</span><span style="color: #800000;">genre.keyword</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">Comedy</span><span style="color: #800000;">"</span><span style="color: #000000;">}}
      ]
    }
  }
}</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">title中包含The并且不包含Good</span>
GET movies/<span style="color: #000000;">_search
{
  
  </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">bool</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">must</span><span style="color: #800000;">"</span>: [{<span style="color: #800000;">"</span><span style="color: #800000;">match</span><span style="color: #800000;">"</span>: {<span style="color: #800000;">"</span><span style="color: #800000;">title</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">The</span><span style="color: #800000;">"</span><span style="color: #000000;">}}],
      </span><span style="color: #800000;">"</span><span style="color: #800000;">must_not</span><span style="color: #800000;">"</span>: [{<span style="color: #800000;">"</span><span style="color: #800000;">match</span><span style="color: #800000;">"</span>: {<span style="color: #800000;">"</span><span style="color: #800000;">title</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">Good</span><span style="color: #800000;">"</span><span style="color: #000000;">}}]
    }
  }
}</span></pre>
</div>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">将title中包含The的语句排在靠前，包含Grifters排在靠后</span>
GET movies/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">boosting</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">positive</span><span style="color: #800000;">"</span>: {<span style="color: #800000;">"</span><span style="color: #800000;">match</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">title</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">The</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }},
      </span><span style="color: #800000;">"</span><span style="color: #800000;">negative</span><span style="color: #800000;">"</span>: {<span style="color: #800000;">"</span><span style="color: #800000;">match</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">title</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">Grifters</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }},
      </span><span style="color: #800000;">"</span><span style="color: #800000;">negative_boost</span><span style="color: #800000;">"</span>: <span style="color: #800080;">0.5</span><span style="color: #000000;">
    }
    
  }
}</span></pre>
</div>
<p>&nbsp;</p>
<p><strong>4，单字符串多字段查询：Dis Max Query</strong></p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">1,获取最佳匹配语句的评分_score
</span><span style="color: #008000;">//</span><span style="color: #008000;">2,将其他匹配语句的评分与tie_breaker相乘
</span><span style="color: #008000;">//</span><span style="color: #008000;">3,对以上评分求和并规范
</span><span style="color: #008000;">//</span><span style="color: #008000;">tie_breaker是一个介于0-1之间的浮点数。0代表使用最佳匹配；1代表所有语句同等重要</span>
POST blogs/<span style="color: #000000;">_search
{
    </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">dis_max</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
            </span><span style="color: #800000;">"</span><span style="color: #800000;">queries</span><span style="color: #800000;">"</span><span style="color: #000000;">: [
                { </span><span style="color: #800000;">"</span><span style="color: #800000;">match</span><span style="color: #800000;">"</span>: { <span style="color: #800000;">"</span><span style="color: #800000;">title</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">Quick pets</span><span style="color: #800000;">"</span><span style="color: #000000;"> }},
                { </span><span style="color: #800000;">"</span><span style="color: #800000;">match</span><span style="color: #800000;">"</span>: { <span style="color: #800000;">"</span><span style="color: #800000;">body</span><span style="color: #800000;">"</span>:  <span style="color: #800000;">"</span><span style="color: #800000;">Quick pets</span><span style="color: #800000;">"</span><span style="color: #000000;"> }}
            ],
            </span><span style="color: #800000;">"</span><span style="color: #800000;">tie_breaker</span><span style="color: #800000;">"</span>: <span style="color: #800080;">0</span><span style="color: #000000;">
        }
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p><strong>5，单字符串多字段查询：Mult Match</strong></p>
<p>最佳字段（Best Fields）：当字段之间相互竞争，有相互关联。例如title和body这样的字段。评分来自最匹配字段</p>
<p>多数字段（Most Fields）：处理英文内容时：一种常见的手段是，在主字段（English Analyzer），抽取词干，加入同义词，以匹配更多的文档。相同的文本，加入子字段（Standard Analyzer），以提供更加精确的匹配。其他字段作为匹配文档提高相关度的信号。匹配字段越多则越好</p>
<p>混合字段（Corss Fields）：对于某些实体，例如人名、地址、图书信息。需要在多字字段中确定信息，单个字段只能作为整理的一部分。希望在任何这些列出的字段中找到尽可能多的词</p>
<div class="cnblogs_code">
<pre>POST blogs/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">multi_match</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">best_fields</span><span style="color: #800000;">"</span><span style="color: #000000;">,
      </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">Quick pets</span><span style="color: #800000;">"</span><span style="color: #000000;">,
      </span><span style="color: #800000;">"</span><span style="color: #800000;">fields</span><span style="color: #800000;">"</span>: [<span style="color: #800000;">"</span><span style="color: #800000;">title</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">body</span><span style="color: #800000;">"</span><span style="color: #000000;">],
      </span><span style="color: #800000;">"</span><span style="color: #800000;">tie_breaker</span><span style="color: #800000;">"</span>: <span style="color: #800080;">0.2</span><span style="color: #000000;">,
      </span><span style="color: #800000;">"</span><span style="color: #800000;">minimum_should_match</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">20%</span><span style="color: #800000;">"</span><span style="color: #000000;">
    }
  }
}</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">英文分词器可以提高算分值，标准分词器可以提高精度</span>
POST titles/<span style="color: #000000;">_bulk
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span>: { <span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span>: <span style="color: #800080;">1</span><span style="color: #000000;"> }}
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">title</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">My dog barks</span><span style="color: #800000;">"</span><span style="color: #000000;"> }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span>: { <span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span>: <span style="color: #800080;">2</span><span style="color: #000000;"> }}
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">title</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">I see a lot of barking dogs on the road </span><span style="color: #800000;">"</span><span style="color: #000000;"> }
PUT </span>/<span style="color: #000000;">titles
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">mappings</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">properties</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">title</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">analyzer</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">english</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">fields</span><span style="color: #800000;">"</span>: {<span style="color: #800000;">"</span><span style="color: #800000;">std</span><span style="color: #800000;">"</span>: {<span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">analyzer</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">standard</span><span style="color: #800000;">"</span><span style="color: #000000;">}}
      }
    }
  } 
}
GET </span>/titles/<span style="color: #000000;">_search
{
   </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">multi_match</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
            </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span>:  <span style="color: #800000;">"</span><span style="color: #800000;">barking dogs</span><span style="color: #800000;">"</span><span style="color: #000000;">,
            </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>:   <span style="color: #800000;">"</span><span style="color: #800000;">most_fields</span><span style="color: #800000;">"</span><span style="color: #000000;">,
            </span><span style="color: #800000;">"</span><span style="color: #800000;">fields</span><span style="color: #800000;">"</span>: [ <span style="color: #800000;">"</span><span style="color: #800000;">title</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">title.std</span><span style="color: #800000;">"</span><span style="color: #000000;"> ]
        }
    }
}</span></pre>
</div>
<div class="cnblogs_code">
<pre>GET /titles/<span style="color: #000000;">_search
{
   </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">multi_match</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
            </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span>:  <span style="color: #800000;">"</span><span style="color: #800000;">barking dogs</span><span style="color: #800000;">"</span><span style="color: #000000;">,
            </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>:   <span style="color: #800000;">"</span><span style="color: #800000;">cross_fields</span><span style="color: #800000;">"</span><span style="color: #000000;">,
            </span><span style="color: #800000;">"</span><span style="color: #800000;">operator</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">and</span><span style="color: #800000;">"</span><span style="color: #000000;">, 
            </span><span style="color: #800000;">"</span><span style="color: #800000;">fields</span><span style="color: #800000;">"</span>: [ <span style="color: #800000;">"</span><span style="color: #800000;">title</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">title.std</span><span style="color: #800000;">"</span><span style="color: #000000;"> ]
        }
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p><strong>&nbsp;6，Search Template与 Index Alias</strong></p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">删除搜索模版</span>
DELETE _scripts/<span style="color: #000000;">tmdb
</span><span style="color: #008000;">//</span><span style="color: #008000;">设置搜索模版</span>
POST _scripts/<span style="color: #000000;">tmdb
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">script</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
    </span><span style="color: #800000;">"</span><span style="color: #800000;">lang</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">mustache</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">source</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">_source</span><span style="color: #800000;">"</span>:[<span style="color: #800000;">"</span><span style="color: #800000;">title</span><span style="color: #800000;">"</span><span style="color: #000000;">],
    </span><span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>:<span style="color: #800080;">20</span><span style="color: #000000;">,
     </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
       </span><span style="color: #800000;">"</span><span style="color: #800000;">bool</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
         </span><span style="color: #800000;">"</span><span style="color: #800000;">must</span><span style="color: #800000;">"</span><span style="color: #000000;">: [
           {</span><span style="color: #800000;">"</span><span style="color: #800000;">term</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
              </span><span style="color: #800000;">"</span><span style="color: #800000;">title.keyword</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">{{q}}</span><span style="color: #800000;">"</span><span style="color: #000000;">
          }}
         ]
       }
     }
    }
  }
  
}
</span><span style="color: #008000;">//</span><span style="color: #008000;">使用搜索模版</span>
POST movies/_search/<span style="color: #000000;">template
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">id</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">tmdb</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">params</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">q</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">Lamerica</span><span style="color: #800000;">"</span><span style="color: #000000;">
  }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">删除别名</span>
<span style="color: #000000;">POST _aliases
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">actions</span><span style="color: #800000;">"</span><span style="color: #000000;">: [
    {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">remove</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">movies</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">alias</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">movies2</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    }
  ]
  
}
</span><span style="color: #008000;">//</span><span style="color: #008000;">设置别名</span>
<span style="color: #000000;">POST _aliases
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">actions</span><span style="color: #800000;">"</span><span style="color: #000000;">: [
    {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">add</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">movies</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">alias</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">movies2</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    }
  ]
}
</span><span style="color: #008000;">//</span><span style="color: #008000;">使用别名查询</span>
GET movies2/_search</pre>
</div>
<p>&nbsp;</p>
<p><strong>&nbsp;7，Function Score Query优化算分</strong></p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">fields算分度 * votes</span>
POST /blogs/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">function_score</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">multi_match</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span>:    <span style="color: #800000;">"</span><span style="color: #800000;">popularity</span><span style="color: #800000;">"</span><span style="color: #000000;">,
          </span><span style="color: #800000;">"</span><span style="color: #800000;">fields</span><span style="color: #800000;">"</span>: [ <span style="color: #800000;">"</span><span style="color: #800000;">title</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">content</span><span style="color: #800000;">"</span><span style="color: #000000;"> ]
        }
      },
      </span><span style="color: #800000;">"</span><span style="color: #800000;">field_value_factor</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">votes</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    }
  }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">log（fields算分度 * votes）</span>
POST /blogs/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">function_score</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">multi_match</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span>:    <span style="color: #800000;">"</span><span style="color: #800000;">popularity</span><span style="color: #800000;">"</span><span style="color: #000000;">,
          </span><span style="color: #800000;">"</span><span style="color: #800000;">fields</span><span style="color: #800000;">"</span>: [ <span style="color: #800000;">"</span><span style="color: #800000;">title</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">content</span><span style="color: #800000;">"</span><span style="color: #000000;"> ]
        }
      },
      </span><span style="color: #800000;">"</span><span style="color: #800000;">field_value_factor</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">votes</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">modifier</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">log1p</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    }
  }
}</span></pre>
</div>
<p>&nbsp;</p>
<p><strong>&nbsp;8，Term Suggester与Phrese&nbsp;Suggester</strong></p>
<p>missing 如索引中已经存在，就不建议提供</p>
<p>popular 推荐出现频率更加高的词</p>
<p>always 无论是否存在，都提供建议</p>
<div class="cnblogs_code">
<pre>POST /articles/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>: <span style="color: #800080;">1</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">match</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">body</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">lucen rock</span><span style="color: #800000;">"</span><span style="color: #000000;">
    }
  },
  </span><span style="color: #800000;">"</span><span style="color: #800000;">suggest</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">term</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">lucen rock</span><span style="color: #800000;">"</span><span style="color: #000000;">,
      </span><span style="color: #800000;">"</span><span style="color: #800000;">term</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">suggest_mode</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">missing</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">body</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    }
  }
}</span></pre>
</div>
<p>phrase多增加了几个参数</p>
<p>max_errors 最多可以拼错的terms数</p>
<p>confidence 限制返回的结果数</p>
<div class="cnblogs_code">
<pre>POST /articles/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">suggest</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">my-suggestion</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">lucne and elasticsear rock hello world </span><span style="color: #800000;">"</span><span style="color: #000000;">,
      </span><span style="color: #800000;">"</span><span style="color: #800000;">phrase</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">body</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">max_errors</span><span style="color: #800000;">"</span>:<span style="color: #800080;">2</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">confidence</span><span style="color: #800000;">"</span>:<span style="color: #800080;">0</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">direct_generator</span><span style="color: #800000;">"</span><span style="color: #000000;">:[{
          </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">body</span><span style="color: #800000;">"</span><span style="color: #000000;">,
          </span><span style="color: #800000;">"</span><span style="color: #800000;">suggest_mode</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">always</span><span style="color: #800000;">"</span><span style="color: #000000;">
        }],
        </span><span style="color: #800000;">"</span><span style="color: #800000;">highlight</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">pre_tag</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">&lt;em&gt;</span><span style="color: #800000;">"</span><span style="color: #000000;">,
          </span><span style="color: #800000;">"</span><span style="color: #800000;">post_tag</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">&lt;/em&gt;</span><span style="color: #800000;">"</span><span style="color: #000000;">
        }
      }
    }
  }
}</span></pre>
</div>
<p>&nbsp;</p>
<p><strong>9，自动补全与基于上下文的提示</strong></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('ba113c55-bc62-4bcf-8f78-4149849eec31')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" id="code_img_closed_ba113c55-bc62-4bcf-8f78-4149849eec31" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" id="code_img_opened_ba113c55-bc62-4bcf-8f78-4149849eec31" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_ba113c55-bc62-4bcf-8f78-4149849eec31" class="cnblogs_code_hide">
<pre><span style="color: #000000;">DELETE articles
</span><span style="color: #008000;">//</span><span style="color: #008000;">设置mapper</span>
<span style="color: #000000;">PUT articles
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">mappings</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">properties</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">title_completion</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">completion</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    }
  }
}

POST articles</span>/<span style="color: #000000;">_bulk
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span><span style="color: #000000;"> : { } }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">title_completion</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">lucene is very cool</span><span style="color: #800000;">"</span><span style="color: #000000;">}
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span><span style="color: #000000;"> : { } }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">title_completion</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">Elasticsearch builds on top of lucene</span><span style="color: #800000;">"</span><span style="color: #000000;">}
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span><span style="color: #000000;"> : { } }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">title_completion</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">Elasticsearch rocks</span><span style="color: #800000;">"</span><span style="color: #000000;">}
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span><span style="color: #000000;"> : { } }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">title_completion</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">elastic is the company behind ELK stack</span><span style="color: #800000;">"</span><span style="color: #000000;">}
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span><span style="color: #000000;"> : { } }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">title_completion</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">Elk stack rocks</span><span style="color: #800000;">"</span><span style="color: #000000;">}
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span><span style="color: #000000;"> : {} }


POST articles</span>/_search?<span style="color: #000000;">pretty
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>: <span style="color: #800080;">0</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">suggest</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">article-suggester</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">prefix</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">elk</span><span style="color: #800000;">"</span><span style="color: #000000;">,
      </span><span style="color: #800000;">"</span><span style="color: #800000;">completion</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">title_completion</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    }
  }
}

GET comments</span>/<span style="color: #000000;">_search
DELETE comments
PUT comments
</span><span style="color: #008000;">//</span><span style="color: #008000;">设置mapper，多了contexts</span>
PUT comments/<span style="color: #000000;">_mapping
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">properties</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">comment_autocomplete</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
      </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">completion</span><span style="color: #800000;">"</span><span style="color: #000000;">,
      </span><span style="color: #800000;">"</span><span style="color: #800000;">contexts</span><span style="color: #800000;">"</span><span style="color: #000000;">:[{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">category</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">comment_category</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }]
    }
  }
}

POST comments</span>/<span style="color: #000000;">_doc
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">comment</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">I love the star war movies</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">comment_autocomplete</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
    </span><span style="color: #800000;">"</span><span style="color: #800000;">input</span><span style="color: #800000;">"</span>:[<span style="color: #800000;">"</span><span style="color: #800000;">star wars</span><span style="color: #800000;">"</span><span style="color: #000000;">],
    </span><span style="color: #800000;">"</span><span style="color: #800000;">contexts</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
      </span><span style="color: #800000;">"</span><span style="color: #800000;">comment_category</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">movies</span><span style="color: #800000;">"</span><span style="color: #000000;">
    }
  }
}

POST comments</span>/<span style="color: #000000;">_doc
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">comment</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">Where can I find a Starbucks</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">comment_autocomplete</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
    </span><span style="color: #800000;">"</span><span style="color: #800000;">input</span><span style="color: #800000;">"</span>:[<span style="color: #800000;">"</span><span style="color: #800000;">starbucks</span><span style="color: #800000;">"</span><span style="color: #000000;">],
    </span><span style="color: #800000;">"</span><span style="color: #800000;">contexts</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
      </span><span style="color: #800000;">"</span><span style="color: #800000;">comment_category</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">coffee</span><span style="color: #800000;">"</span><span style="color: #000000;">
    }
  }
}


POST comments</span>/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">suggest</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">MY_SUGGESTION</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">prefix</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">sta</span><span style="color: #800000;">"</span><span style="color: #000000;">,
      </span><span style="color: #800000;">"</span><span style="color: #800000;">completion</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">comment_autocomplete</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">contexts</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
          </span><span style="color: #800000;">"</span><span style="color: #800000;">comment_category</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">coffee</span><span style="color: #800000;">"</span><span style="color: #000000;">
        }
      }
    }
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<p>&nbsp;</p>
<p><strong>10，Search After与Scroll Api解决分页大于10000条数据问题</strong></p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">search_after:order_id为740002后面下一条数据</span>
GET kibana_sample_data_ecommerce/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>: <span style="color: #800080;">1</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span>: {<span style="color: #800000;">"</span><span style="color: #800000;">match_all</span><span style="color: #800000;">"</span><span style="color: #000000;">: {}},
  </span><span style="color: #800000;">"</span><span style="color: #800000;">search_after</span><span style="color: #800000;">"</span>:[<span style="color: #800080;">740002</span><span style="color: #000000;">],
  </span><span style="color: #800000;">"</span><span style="color: #800000;">sort</span><span style="color: #800000;">"</span>: [{<span style="color: #800000;">"</span><span style="color: #800000;">order_id</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">desc</span><span style="color: #800000;">"</span><span style="color: #000000;">}]
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">先创建快照</span>
POST kibana_sample_data_ecommerce/_search?scroll=<span style="color: #000000;">5m
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>: <span style="color: #800080;">1</span><span style="color: #000000;">, 
  </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span>: {<span style="color: #800000;">"</span><span style="color: #800000;">match_all</span><span style="color: #800000;">"</span><span style="color: #000000;">: {}}
}
</span><span style="color: #008000;">//</span><span style="color: #008000;">根据上一个scroll_id查询下一页数据</span>
POST _search/<span style="color: #000000;">scroll
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">scroll</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">1m</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">scroll_id</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">DXF1ZXJ5QW5kRmV0Y2gBAAAAAAAAEuEWVHlEU0NNSFFSd2VQVElQX3Vza2Zfdw==</span><span style="color: #800000;">"</span><span style="color: #000000;">
}</span></pre>
</div>
<p>&nbsp;</p>
<p>11，使用乐观锁解决并发写入问题</p>
<p>①内部版本控制：&nbsp;if_seq_no+if_primary_term</p>
<p>②使用外部版本（使用其他数据库作为主要数据存储）：version+version_type=external</p>
<div class="cnblogs_code">
<pre>PUT products/_doc/<span style="color: #800080;">1</span>?if_seq_no=<span style="color: #800080;">1</span>&amp;if_primary_term=<span style="color: #800080;">1</span><span style="color: #000000;">
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">title</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">iphone</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">count</span><span style="color: #800000;">"</span>:<span style="color: #800080;">100</span><span style="color: #000000;">
}

PUT products</span>/_doc/<span style="color: #800080;">1</span>?version=<span style="color: #800080;">30000</span>&amp;version_type=<span style="color: #000000;">external
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">title</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">iphone</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">count</span><span style="color: #800000;">"</span>:<span style="color: #800080;">100</span><span style="color: #000000;">
}</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: #169fe6;"><span style="color: #ffffff;"><strong>三、Mapping</strong></span></p>
<p>1，设置Dynamic Mapping</p>
<table style="height: 112px; width: 675px;" border="1">
<tbody>
<tr>
<td>&nbsp;</td>
<td>"true"</td>
<td>"false"</td>
<td>"strict"</td>
</tr>
<tr>
<td>新增字段是否可保存</td>
<td>yes</td>
<td>yes</td>
<td>no</td>
</tr>
<tr>
<td>新增字段是否可被搜索</td>
<td>yes</td>
<td>no</td>
<td>no</td>
</tr>
<tr>
<td>Mapping会不会被更新</td>
<td>yes</td>
<td>no</td>
<td>no</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre>PUT user/<span style="color: #000000;">_mapping
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">dynamic</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">true</span><span style="color: #800000;">"</span><span style="color: #000000;">
}
PUT user</span>/<span style="color: #000000;">_mapping
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">dynamic</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">false</span><span style="color: #800000;">"</span><span style="color: #000000;">
}
PUT user</span>/<span style="color: #000000;">_mapping
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">dynamic</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">strict</span><span style="color: #800000;">"</span><span style="color: #000000;">
}<br /><br />//新增字段</span></pre>
<p>POST labourer_payroll_confirm_2022/_mapping<br />{<br />  "properties":{<br />    "seltime":{<br />          "type": "date"<br />        },<br />    "company_name":{<br />      "type": "text"<br />    },<br />     "project_name":{<br />      "type": "text"<br />    }<br />  }<br />}</p>
<pre><span style="color: #000000;"><br /><br /></span></pre>
</div>
<p>2，定义mapping</p>
<p>①index控制字段是否可以被搜索</p>
<p>②null_value设置一个默认值"NULL"，方便搜索null值字段</p>
<p>③text类型和keyword类型区别：text类型会使用默认分词器分词，当然你也可以为他指定特定的分词器。如果定义成keyword类型，那么默认就不会对其进行分词</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">查询user的mapping</span>
GET user/_mapping</pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #000000;">PUT employee
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">mappings</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">properties</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">firstName</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">copy_to</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">fullname</span><span style="color: #800000;">"</span><span style="color: #000000;">
      },
      </span><span style="color: #800000;">"</span><span style="color: #800000;">lastName</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">copy_to</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">fullname</span><span style="color: #800000;">"</span><span style="color: #000000;">
      },
      </span><span style="color: #800000;">"</span><span style="color: #800000;">mobile</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span>: <span style="color: #0000ff;">false</span><span style="color: #000000;">
      },
      </span><span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">integer</span><span style="color: #800000;">"</span><span style="color: #000000;">
      },
      </span><span style="color: #800000;">"</span><span style="color: #800000;">cardNo</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">keyword</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">null_value</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">NULL</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    }
  }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">添加值</span>
POST employee/<span style="color: #000000;">_doc
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">firstName</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">zhang</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">lastName</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">san</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">mobile</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">1300000000</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span>:<span style="color: #800080;">20</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">cardNo</span><span style="color: #800000;">"</span>:<span style="color: #0000ff;">null</span><span style="color: #000000;">
}
</span><span style="color: #008000;">//</span><span style="color: #008000;">查询cardNo是null的值</span>
GET employee/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">match</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">cardNo</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">NULL</span><span style="color: #800000;">"</span><span style="color: #000000;">
    }
  }
}
</span><span style="color: #008000;">//</span><span style="color: #008000;">搜索报错</span>
GET employee/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">match</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">mobile</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">1300000000</span><span style="color: #800000;">"</span><span style="color: #000000;">
    }
  }
}</span></pre>
</div>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: #169fe6;"><span style="color: #ffffff;"><strong>四、Index Templete与Dynamic&nbsp;Templete</strong></span></p>
<p>1，Index Templete</p>
<p>应用在所有的index上面。当一个索引被创建的时候</p>
<p>①应用elasticsearch默认的settings和mappings</p>
<p>②应用order数值低的index template中的设定</p>
<p>③应用order高的index&nbsp;template中的设定，之前的设定会被覆盖</p>
<p>④应用创建索引时，用户指定的settings和mappings，并覆盖之前模版中的设定</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">order数值：控制&ldquo;merging&rdquo;的过程。多个模版会merge在一起</span>
PUT _template/<span style="color: #000000;">template_default
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">index_patterns</span><span style="color: #800000;">"</span>: [<span style="color: #800000;">"</span><span style="color: #800000;">*</span><span style="color: #800000;">"</span><span style="color: #000000;">],
  </span><span style="color: #800000;">"</span><span style="color: #800000;">order</span><span style="color: #800000;">"</span>: <span style="color: #800080;">0</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">version</span><span style="color: #800000;">"</span>: <span style="color: #800080;">1</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">settings</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">number_of_shards</span><span style="color: #800000;">"</span>: <span style="color: #800080;">1</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">number_of_replicas</span><span style="color: #800000;">"</span>: <span style="color: #800080;">1</span><span style="color: #000000;">
  }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">创建test开头的索引时，主分片设置1，副本分片设置2，开启数值检测</span>
PUT _template/<span style="color: #000000;">template_test
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">index_patterns</span><span style="color: #800000;">"</span>: [<span style="color: #800000;">"</span><span style="color: #800000;">test*</span><span style="color: #800000;">"</span><span style="color: #000000;">],
  </span><span style="color: #800000;">"</span><span style="color: #800000;">order</span><span style="color: #800000;">"</span>: <span style="color: #800080;">1</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">settings</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">number_of_shards</span><span style="color: #800000;">"</span>: <span style="color: #800080;">1</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">number_of_replicas</span><span style="color: #800000;">"</span>: <span style="color: #800080;">2</span><span style="color: #000000;">
  },
  </span><span style="color: #800000;">"</span><span style="color: #800000;">mappings</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">date_detection</span><span style="color: #800000;">"</span>: <span style="color: #0000ff;">false</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">numeric_detection</span><span style="color: #800000;">"</span>: <span style="color: #0000ff;">true</span><span style="color: #000000;">
  }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">指定索引设置template</span>
<span style="color: #000000;">PUT testmy
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">settings</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">number_of_replicas</span><span style="color: #800000;">"</span>: <span style="color: #800080;">5</span><span style="color: #000000;">
  }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">查看template信息</span>
GET _template/<span style="color: #000000;">template_default
GET _template</span>/<span style="color: #000000;">template_test

</span><span style="color: #008000;">//</span><span style="color: #008000;">删除</span>
<span style="color: #000000;">DELETE testmy
DELETE _template</span>/<span style="color: #000000;">template_default
DELETE _template</span>/template_test</pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #000000;">PUT request_audit_logs_v2
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">mappings</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">properties</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">key</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">keyword</span><span style="color: #800000;">"</span><span style="color: #000000;">
      },
      </span><span style="color: #800000;">"</span><span style="color: #800000;">post_type</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">keyword</span><span style="color: #800000;">"</span><span style="color: #000000;">
      },
      </span><span style="color: #800000;">"</span><span style="color: #800000;">url</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">keyword</span><span style="color: #800000;">"</span><span style="color: #000000;">
      },
      </span><span style="color: #800000;">"</span><span style="color: #800000;">api</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">keyword</span><span style="color: #800000;">"</span><span style="color: #000000;">
      },
      </span><span style="color: #800000;">"</span><span style="color: #800000;">request_content</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">object</span><span style="color: #800000;">"</span><span style="color: #000000;">
      },
      </span><span style="color: #800000;">"</span><span style="color: #800000;">hander</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span>: <span style="color: #0000ff;">false</span><span style="color: #000000;">
      },
      </span><span style="color: #800000;">"</span><span style="color: #800000;">status</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">keyword</span><span style="color: #800000;">"</span><span style="color: #000000;">
      },
      </span><span style="color: #800000;">"</span><span style="color: #800000;">response_content</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">object</span><span style="color: #800000;">"</span><span style="color: #000000;">
      },
      </span><span style="color: #800000;">"</span><span style="color: #800000;">request_time</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">date</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">format</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">yyyy-MM-dd HH:mm:ss</span><span style="color: #800000;">"</span><span style="color: #000000;">
      },
      </span><span style="color: #800000;">"</span><span style="color: #800000;">response_time</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">date</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">format</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">yyyy-MM-dd HH:mm:ss</span><span style="color: #800000;">"</span><span style="color: #000000;">
      },
      </span><span style="color: #800000;">"</span><span style="color: #800000;">exception</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span><span style="color: #000000;">
      },
      </span><span style="color: #800000;">"</span><span style="color: #800000;">run_time</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">float</span><span style="color: #800000;">"</span><span style="color: #000000;">
      },
      </span><span style="color: #800000;">"</span><span style="color: #800000;">thread_num</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">integer</span><span style="color: #800000;">"</span><span style="color: #000000;">
      },
      </span><span style="color: #800000;">"</span><span style="color: #800000;">create_time</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">date</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">format</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">yyyy-MM-dd HH:mm:ss</span><span style="color: #800000;">"</span><span style="color: #000000;">
      },
      </span><span style="color: #800000;">"</span><span style="color: #800000;">modify_time</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">date</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">format</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">yyyy-MM-dd HH:mm:ss</span><span style="color: #800000;">"</span><span style="color: #000000;">
      },
      </span><span style="color: #800000;">"</span><span style="color: #800000;">user_name</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">keyword</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    },
    </span><span style="color: #800000;">"</span><span style="color: #800000;">dynamic</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">strict</span><span style="color: #800000;">"</span><span style="color: #000000;">

  }
}</span></pre>
</div>
<p>&nbsp;</p>
<p>2，Dynamic&nbsp;Templete</p>
<p>设置在具体的index上面</p>
<div class="cnblogs_code">
<pre>GET myindex/_search?q=<span style="color: #000000;">full_name:zhang
</span><span style="color: #008000;">//</span><span style="color: #008000;">将name.fitst和name.last映射到full_name字段上</span>
<span style="color: #000000;">PUT myindex
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">mappings</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
     </span><span style="color: #800000;">"</span><span style="color: #800000;">dynamic_templates</span><span style="color: #800000;">"</span><span style="color: #000000;">:[
        { 
          </span><span style="color: #800000;">"</span><span style="color: #800000;">full_name</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
            </span><span style="color: #800000;">"</span><span style="color: #800000;">path_match</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">name.*</span><span style="color: #800000;">"</span><span style="color: #000000;">,
            </span><span style="color: #800000;">"</span><span style="color: #800000;">path_unmatch</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">*.middle</span><span style="color: #800000;">"</span><span style="color: #000000;">,
            </span><span style="color: #800000;">"</span><span style="color: #800000;">mapping</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
              </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span><span style="color: #000000;">,
              </span><span style="color: #800000;">"</span><span style="color: #800000;">copy_to</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">full_name</span><span style="color: #800000;">"</span><span style="color: #000000;">
            }
          }
        }
       ]
  }
}

POST myindex</span>/<span style="color: #000000;">_doc
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
    </span><span style="color: #800000;">"</span><span style="color: #800000;">fitst</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">zhang</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">middle</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">123</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">last</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">san</span><span style="color: #800000;">"</span><span style="color: #000000;">
  }
}</span></pre>
</div>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: #169fe6;"><strong><span style="color: #ffffff;">五、Aggregation</span></strong></p>
<p>Bucket&nbsp;Aggregation：一些列满足特定条件的文档集合</p>
<p>Meric&nbsp;Aggregation：一些数学运算，可以对文档字段进行统计分析</p>
<p>Pipeline&nbsp;Aggregation：对其他聚合结果进行二次聚合</p>
<p>Matrix&nbsp;Aggregation：支持对多个字段的操做并提供一个结果矩阵</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">统计去往目的地的天气情况、价格情况</span>
GET kibana_sample_data_flights/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>: <span style="color: #800080;">0</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">flights_dest</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">terms</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">DestCountry</span><span style="color: #800000;">"</span><span style="color: #000000;">
      },
      </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">stats_price</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">stats</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
            </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">AvgTicketPrice</span><span style="color: #800000;">"</span><span style="color: #000000;">
          }
        },
        </span><span style="color: #800000;">"</span><span style="color: #800000;">wather</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
          </span><span style="color: #800000;">"</span><span style="color: #800000;">terms</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
            </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">DestWeather</span><span style="color: #800000;">"</span><span style="color: #000000;">
          }
        }
      }
    }
  }
}</span></pre>
</div>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre>PUT /employees/<span style="color: #000000;">
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">mappings</span><span style="color: #800000;">"</span><span style="color: #000000;"> : {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">properties</span><span style="color: #800000;">"</span><span style="color: #000000;"> : {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span><span style="color: #000000;"> : {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">integer</span><span style="color: #800000;">"</span><span style="color: #000000;">
        },
        </span><span style="color: #800000;">"</span><span style="color: #800000;">gender</span><span style="color: #800000;">"</span><span style="color: #000000;"> : {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">keyword</span><span style="color: #800000;">"</span><span style="color: #000000;">
        },
        </span><span style="color: #800000;">"</span><span style="color: #800000;">job</span><span style="color: #800000;">"</span><span style="color: #000000;"> : {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span><span style="color: #000000;">,
          </span><span style="color: #800000;">"</span><span style="color: #800000;">fields</span><span style="color: #800000;">"</span><span style="color: #000000;"> : {
            </span><span style="color: #800000;">"</span><span style="color: #800000;">keyword</span><span style="color: #800000;">"</span><span style="color: #000000;"> : {
              </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">keyword</span><span style="color: #800000;">"</span><span style="color: #000000;">,
              </span><span style="color: #800000;">"</span><span style="color: #800000;">ignore_above</span><span style="color: #800000;">"</span> : <span style="color: #800080;">50</span><span style="color: #000000;">
            }
          }
        },
        </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span><span style="color: #000000;"> : {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">keyword</span><span style="color: #800000;">"</span><span style="color: #000000;">
        },
        </span><span style="color: #800000;">"</span><span style="color: #800000;">salary</span><span style="color: #800000;">"</span><span style="color: #000000;"> : {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">integer</span><span style="color: #800000;">"</span><span style="color: #000000;">
        }
      }
    }
}

PUT </span>/employees/<span style="color: #000000;">_bulk
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span> : {  <span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">1</span><span style="color: #800000;">"</span><span style="color: #000000;"> } }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">Emma</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span>:<span style="color: #800080;">32</span>,<span style="color: #800000;">"</span><span style="color: #800000;">job</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">Product Manager</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">gender</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">female</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">salary</span><span style="color: #800000;">"</span>:<span style="color: #800080;">35000</span><span style="color: #000000;"> }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span> : {  <span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">2</span><span style="color: #800000;">"</span><span style="color: #000000;"> } }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">Underwood</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span>:<span style="color: #800080;">41</span>,<span style="color: #800000;">"</span><span style="color: #800000;">job</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">Dev Manager</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">gender</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">male</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">salary</span><span style="color: #800000;">"</span>: <span style="color: #800080;">50000</span><span style="color: #000000;">}
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span> : {  <span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">3</span><span style="color: #800000;">"</span><span style="color: #000000;"> } }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">Tran</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span>:<span style="color: #800080;">25</span>,<span style="color: #800000;">"</span><span style="color: #800000;">job</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">Web Designer</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">gender</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">male</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">salary</span><span style="color: #800000;">"</span>:<span style="color: #800080;">18000</span><span style="color: #000000;"> }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span> : {  <span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">4</span><span style="color: #800000;">"</span><span style="color: #000000;"> } }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">Rivera</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span>:<span style="color: #800080;">26</span>,<span style="color: #800000;">"</span><span style="color: #800000;">job</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">Web Designer</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">gender</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">female</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">salary</span><span style="color: #800000;">"</span>: <span style="color: #800080;">22000</span><span style="color: #000000;">}
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span> : {  <span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">5</span><span style="color: #800000;">"</span><span style="color: #000000;"> } }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">Rose</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span>:<span style="color: #800080;">25</span>,<span style="color: #800000;">"</span><span style="color: #800000;">job</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">QA</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">gender</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">female</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">salary</span><span style="color: #800000;">"</span>:<span style="color: #800080;">18000</span><span style="color: #000000;"> }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span> : {  <span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">6</span><span style="color: #800000;">"</span><span style="color: #000000;"> } }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">Lucy</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span>:<span style="color: #800080;">31</span>,<span style="color: #800000;">"</span><span style="color: #800000;">job</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">QA</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">gender</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">female</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">salary</span><span style="color: #800000;">"</span>: <span style="color: #800080;">25000</span><span style="color: #000000;">}
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span> : {  <span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">7</span><span style="color: #800000;">"</span><span style="color: #000000;"> } }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">Byrd</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span>:<span style="color: #800080;">27</span>,<span style="color: #800000;">"</span><span style="color: #800000;">job</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">QA</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">gender</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">male</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">salary</span><span style="color: #800000;">"</span>:<span style="color: #800080;">20000</span><span style="color: #000000;"> }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span> : {  <span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">8</span><span style="color: #800000;">"</span><span style="color: #000000;"> } }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">Foster</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span>:<span style="color: #800080;">27</span>,<span style="color: #800000;">"</span><span style="color: #800000;">job</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">Java Programmer</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">gender</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">male</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">salary</span><span style="color: #800000;">"</span>: <span style="color: #800080;">20000</span><span style="color: #000000;">}
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span> : {  <span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">9</span><span style="color: #800000;">"</span><span style="color: #000000;"> } }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">Gregory</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span>:<span style="color: #800080;">32</span>,<span style="color: #800000;">"</span><span style="color: #800000;">job</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">Java Programmer</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">gender</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">male</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">salary</span><span style="color: #800000;">"</span>:<span style="color: #800080;">22000</span><span style="color: #000000;"> }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span> : {  <span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">10</span><span style="color: #800000;">"</span><span style="color: #000000;"> } }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">Bryant</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span>:<span style="color: #800080;">20</span>,<span style="color: #800000;">"</span><span style="color: #800000;">job</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">Java Programmer</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">gender</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">male</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">salary</span><span style="color: #800000;">"</span>: <span style="color: #800080;">9000</span><span style="color: #000000;">}
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span> : {  <span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">11</span><span style="color: #800000;">"</span><span style="color: #000000;"> } }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">Jenny</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span>:<span style="color: #800080;">36</span>,<span style="color: #800000;">"</span><span style="color: #800000;">job</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">Java Programmer</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">gender</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">female</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">salary</span><span style="color: #800000;">"</span>:<span style="color: #800080;">38000</span><span style="color: #000000;"> }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span> : {  <span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">12</span><span style="color: #800000;">"</span><span style="color: #000000;"> } }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">Mcdonald</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span>:<span style="color: #800080;">31</span>,<span style="color: #800000;">"</span><span style="color: #800000;">job</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">Java Programmer</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">gender</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">male</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">salary</span><span style="color: #800000;">"</span>: <span style="color: #800080;">32000</span><span style="color: #000000;">}
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span> : {  <span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">13</span><span style="color: #800000;">"</span><span style="color: #000000;"> } }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">Jonthna</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span>:<span style="color: #800080;">30</span>,<span style="color: #800000;">"</span><span style="color: #800000;">job</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">Java Programmer</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">gender</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">female</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">salary</span><span style="color: #800000;">"</span>:<span style="color: #800080;">30000</span><span style="color: #000000;"> }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span> : {  <span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">14</span><span style="color: #800000;">"</span><span style="color: #000000;"> } }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">Marshall</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span>:<span style="color: #800080;">32</span>,<span style="color: #800000;">"</span><span style="color: #800000;">job</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">Javascript Programmer</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">gender</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">male</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">salary</span><span style="color: #800000;">"</span>: <span style="color: #800080;">25000</span><span style="color: #000000;">}
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span> : {  <span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">15</span><span style="color: #800000;">"</span><span style="color: #000000;"> } }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">King</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span>:<span style="color: #800080;">33</span>,<span style="color: #800000;">"</span><span style="color: #800000;">job</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">Java Programmer</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">gender</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">male</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">salary</span><span style="color: #800000;">"</span>:<span style="color: #800080;">28000</span><span style="color: #000000;"> }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span> : {  <span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">16</span><span style="color: #800000;">"</span><span style="color: #000000;"> } }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">Mccarthy</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span>:<span style="color: #800080;">21</span>,<span style="color: #800000;">"</span><span style="color: #800000;">job</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">Javascript Programmer</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">gender</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">male</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">salary</span><span style="color: #800000;">"</span>: <span style="color: #800080;">16000</span><span style="color: #000000;">}
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span> : {  <span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">17</span><span style="color: #800000;">"</span><span style="color: #000000;"> } }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">Goodwin</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span>:<span style="color: #800080;">25</span>,<span style="color: #800000;">"</span><span style="color: #800000;">job</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">Javascript Programmer</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">gender</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">male</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">salary</span><span style="color: #800000;">"</span>: <span style="color: #800080;">16000</span><span style="color: #000000;">}
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span> : {  <span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">18</span><span style="color: #800000;">"</span><span style="color: #000000;"> } }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">Catherine</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span>:<span style="color: #800080;">29</span>,<span style="color: #800000;">"</span><span style="color: #800000;">job</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">Javascript Programmer</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">gender</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">female</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">salary</span><span style="color: #800000;">"</span>: <span style="color: #800080;">20000</span><span style="color: #000000;">}
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span> : {  <span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">19</span><span style="color: #800000;">"</span><span style="color: #000000;"> } }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">Boone</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span>:<span style="color: #800080;">30</span>,<span style="color: #800000;">"</span><span style="color: #800000;">job</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">DBA</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">gender</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">male</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">salary</span><span style="color: #800000;">"</span>: <span style="color: #800080;">30000</span><span style="color: #000000;">}
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span> : {  <span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">20</span><span style="color: #800000;">"</span><span style="color: #000000;"> } }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">Kathy</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span>:<span style="color: #800080;">29</span>,<span style="color: #800000;">"</span><span style="color: #800000;">job</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">DBA</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">gender</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">female</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">salary</span><span style="color: #800000;">"</span>: <span style="color: #800080;">20000</span><span style="color: #000000;">}


# Metric 聚合，找到最低的工资
GET employees</span>/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>: <span style="color: #800080;">0</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">min_salary</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">min</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">salary</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    }
  }
}

# Metric 聚合，找到最高的工资
GET employees</span>/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>: <span style="color: #800080;">0</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">max_salary</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">max</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">salary</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    }
  }
}


# 多个 Metric 聚合，找到最低最高和平均工资
GET employees</span>/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>: <span style="color: #800080;">0</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">max_salary</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">max</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">salary</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    },
    </span><span style="color: #800000;">"</span><span style="color: #800000;">min_salary</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">min</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">salary</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    },
    </span><span style="color: #800000;">"</span><span style="color: #800000;">avg_salary</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">avg</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">salary</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    }
  }
}

# 一个聚合，输出多值
GET employees</span>/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>: <span style="color: #800080;">0</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">stats_salary</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">stats</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">salary</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    }
  }
}

# 对keword 进行聚合
GET employees</span>/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>: <span style="color: #800080;">0</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">jobs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">terms</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">job.keyword</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    }
  }
}

# 对 Text 字段进行 terms 聚合查询
#对 Text 字段打开 fielddata，支持terms aggregation
PUT employees</span>/<span style="color: #000000;">_mapping
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">properties</span><span style="color: #800000;">"</span><span style="color: #000000;"> : {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">job</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
       </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>:     <span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span><span style="color: #000000;">,
       </span><span style="color: #800000;">"</span><span style="color: #800000;">fielddata</span><span style="color: #800000;">"</span>: <span style="color: #0000ff;">true</span><span style="color: #000000;">
    }
  }
}
POST employees</span>/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>: <span style="color: #800080;">0</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">jobs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">terms</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">job</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    }
  }
}

# cardinality 相当于distinct count
POST employees</span>/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>: <span style="color: #800080;">0</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">cardinate</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">cardinality</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">job.keyword</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    }
  }
}


# 对 性别的 keyword 进行聚合
POST employees</span>/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>: <span style="color: #800080;">0</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">gender</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">terms</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">gender</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    }
  }
}

#指定 bucket 的 size
POST employees</span>/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>: <span style="color: #800080;">0</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">ages_5</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">terms</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>:<span style="color: #800080;">3</span><span style="color: #000000;">
      }
    }
  }
}

# 指定size，不同工种中，年纪最大的3个员工的具体信息
POST employees</span>/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>: <span style="color: #800080;">0</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">jobs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">terms</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">job.keyword</span><span style="color: #800000;">"</span><span style="color: #000000;">
      },
      </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">old_employee</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">top_hits</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
            </span><span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>: <span style="color: #800080;">3</span><span style="color: #000000;">,
            </span><span style="color: #800000;">"</span><span style="color: #800000;">sort</span><span style="color: #800000;">"</span><span style="color: #000000;">: [{
              </span><span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">desc</span><span style="color: #800000;">"</span><span style="color: #000000;">
            }]
          }
        }
      }
    }
  }
}

#自定义工资区间分桶
POST employees</span>/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>: <span style="color: #800080;">0</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">salary_range</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">range</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">salary</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">ranges</span><span style="color: #800000;">"</span><span style="color: #000000;">: [
          {
            </span><span style="color: #800000;">"</span><span style="color: #800000;">to</span><span style="color: #800000;">"</span>: <span style="color: #800080;">10000</span><span style="color: #000000;">
          },
          {
            </span><span style="color: #800000;">"</span><span style="color: #800000;">from</span><span style="color: #800000;">"</span>: <span style="color: #800080;">10000</span><span style="color: #000000;">, 
            </span><span style="color: #800000;">"</span><span style="color: #800000;">to</span><span style="color: #800000;">"</span>: <span style="color: #800080;">20000</span><span style="color: #000000;">
          }
          ,
          {
            </span><span style="color: #800000;">"</span><span style="color: #800000;">key</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">&gt;=20000</span><span style="color: #800000;">"</span><span style="color: #000000;">, 
            </span><span style="color: #800000;">"</span><span style="color: #800000;">from</span><span style="color: #800000;">"</span>: <span style="color: #800080;">20000</span><span style="color: #000000;">
          }
        ]
      }
    }
  }
}


#Salary Histogram,工资0到10万，以 5000一个区间进行分桶
POST employees</span>/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>: <span style="color: #800080;">0</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">salary_histrogram</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">histogram</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">salary</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">interval</span><span style="color: #800000;">"</span>: <span style="color: #800080;">5000</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">extended_bounds</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">min</span><span style="color: #800000;">"</span>: <span style="color: #800080;">0</span><span style="color: #000000;">,
          </span><span style="color: #800000;">"</span><span style="color: #800000;">max</span><span style="color: #800000;">"</span>: <span style="color: #800080;">100000</span><span style="color: #000000;">
        }
      }
    }
  }
}


# 嵌套聚合1，按照工作类型分桶，并统计工资信息
POST employees</span>/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>: <span style="color: #800080;">0</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">Job_salary_stats</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">terms</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">job.keyword</span><span style="color: #800000;">"</span><span style="color: #000000;">
      },
      </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">salary</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">stats</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
            </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">salary</span><span style="color: #800000;">"</span><span style="color: #000000;">
          }
        }
      }
    }
  }
}

# 多次嵌套。根据工作类型分桶，然后按照性别分桶，计算工资的统计信息
POST employees</span>/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>: <span style="color: #800080;">0</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">Job_gender_stats</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">terms</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">job.keyword</span><span style="color: #800000;">"</span><span style="color: #000000;">
      },
      </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">gender_stats</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">terms</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
            </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">gender</span><span style="color: #800000;">"</span><span style="color: #000000;">
          },
          </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
            </span><span style="color: #800000;">"</span><span style="color: #800000;">salary_stats</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
              </span><span style="color: #800000;">"</span><span style="color: #800000;">stats</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
                </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">salary</span><span style="color: #800000;">"</span><span style="color: #000000;">
              }
            }
          }
        }
      }
    }
  }
}</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #000000;"># 平均工资最低的工作类型
POST employees</span>/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>: <span style="color: #800080;">0</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">jobs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">terms</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">job.keyword</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">order</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">avg_salary</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">desc</span><span style="color: #800000;">"</span><span style="color: #000000;">
        }
      },
      </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">avg_salary</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">avg</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
            </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">salary</span><span style="color: #800000;">"</span><span style="color: #000000;">
          }
        }
      }
    },
    </span><span style="color: #800000;">"</span><span style="color: #800000;">min_salary_by_job</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
      </span><span style="color: #800000;">"</span><span style="color: #800000;">min_bucket</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">buckets_path</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">jobs&gt;avg_salary</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    }
  }
}


# 平均工资最高的工作类型
POST employees</span>/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>: <span style="color: #800080;">0</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">jobs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">terms</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">job.keyword</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">order</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">avg_salary</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">desc</span><span style="color: #800000;">"</span><span style="color: #000000;">
        }
      },
      </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">avg_salary</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">avg</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
            </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">salary</span><span style="color: #800000;">"</span><span style="color: #000000;">
          }
        }
      }
    },
    </span><span style="color: #800000;">"</span><span style="color: #800000;">max_salary_by_job</span><span style="color: #800000;">"</span><span style="color: #000000;">:
    {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">max_bucket</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">buckets_path</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">jobs&gt;avg_salary</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    }
  }
}

# 平均工资的平均工资
POST employees</span>/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>: <span style="color: #800080;">0</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">jobs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">terms</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">job.keyword</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">order</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">avg_salary</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">desc</span><span style="color: #800000;">"</span><span style="color: #000000;">
        }
      },
      </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">avg_salary</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">avg</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
            </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">salary</span><span style="color: #800000;">"</span><span style="color: #000000;">
          }
        }
      }
    },
    </span><span style="color: #800000;">"</span><span style="color: #800000;">avg_salary_by_job</span><span style="color: #800000;">"</span><span style="color: #000000;">:
    {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">avg_bucket</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">buckets_path</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">jobs&gt;avg_salary</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    }
  }
}

# 平均工资的统计分析
POST employees</span>/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>: <span style="color: #800080;">0</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">jobs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">terms</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">job.keyword</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>: <span style="color: #800080;">10</span><span style="color: #000000;">, 
        </span><span style="color: #800000;">"</span><span style="color: #800000;">order</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">avg_salary</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">desc</span><span style="color: #800000;">"</span><span style="color: #000000;">
        }
      },
      </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">avg_salary</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">avg</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
            </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">salary</span><span style="color: #800000;">"</span><span style="color: #000000;">
          }
        }
      }
    },
    </span><span style="color: #800000;">"</span><span style="color: #800000;">stats_salary_by_job</span><span style="color: #800000;">"</span><span style="color: #000000;">:
    {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">stats_bucket</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">buckets_path</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">jobs&gt;avg_salary</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    }
  }
}

# 平均工资的百分位数
POST employees</span>/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>: <span style="color: #800080;">0</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">jobs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">terms</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">job.keyword</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>: <span style="color: #800080;">10</span><span style="color: #000000;">
      },
      </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">avg_salary</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">avg</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
            </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">salary</span><span style="color: #800000;">"</span><span style="color: #000000;">
          }
        }
      }
    },
    </span><span style="color: #800000;">"</span><span style="color: #800000;">percentiles_salary_by_job</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
      </span><span style="color: #800000;">"</span><span style="color: #800000;">percentiles_bucket</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">buckets_path</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">jobs&gt;avg_salary</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    }
  }
}

#按照年龄对平均工资求导
POST employees</span>/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>: <span style="color: #800080;">0</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">histogram</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">min_doc_count</span><span style="color: #800000;">"</span>: <span style="color: #800080;">1</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">interval</span><span style="color: #800000;">"</span>: <span style="color: #800080;">1</span><span style="color: #000000;">
      },
      </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">avg_salary</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">avg</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
            </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">salary</span><span style="color: #800000;">"</span><span style="color: #000000;">
          }
        },
        </span><span style="color: #800000;">"</span><span style="color: #800000;">derivative_avg_salary</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
          </span><span style="color: #800000;">"</span><span style="color: #800000;">derivative</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
            </span><span style="color: #800000;">"</span><span style="color: #800000;">buckets_path</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">avg_salary</span><span style="color: #800000;">"</span><span style="color: #000000;">
          }
        }
      }
    }
  }
}</span></pre>
</div>
<p>&nbsp;</p>
<p><strong>作用范围</strong></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;"># Query 年龄大于20岁的员工，根据job分桶
POST employees</span>/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>: <span style="color: #800080;">0</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">range</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">gte</span><span style="color: #800000;">"</span>: <span style="color: #800080;">20</span><span style="color: #000000;">
      }
    }
  },
  </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">jobs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">terms</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">job.keyword</span><span style="color: #800000;">"</span><span style="color: #000000;">
        
      }
    }
  }
}


#field 年长的员工job分桶，和所有的员工job分桶
POST employees</span>/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>: <span style="color: #800080;">0</span><span style="color: #000000;">, 
  </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">older_person</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">filter</span><span style="color: #800000;">"</span>: {<span style="color: #800000;">"</span><span style="color: #800000;">range</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">gte</span><span style="color: #800000;">"</span>: <span style="color: #800080;">35</span><span style="color: #000000;">
        }
      }},
      </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">jobs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">terms</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
            </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">job.keyword</span><span style="color: #800000;">"</span><span style="color: #000000;">
          }
        }
      }
    },
    </span><span style="color: #800000;">"</span><span style="color: #800000;">all_jobs</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
      </span><span style="color: #800000;">"</span><span style="color: #800000;">terms</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">job.keyword</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    }
  }
}

#Post field. 一条语句，找出所有的job类型。还能找到聚合后符合条件的结果
#将分完桶的job为Javascript Programmer显示出来
POST employees</span>/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">jobs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">terms</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">job.keyword</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    }
  },
  </span><span style="color: #800000;">"</span><span style="color: #800000;">post_filter</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">match</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">job.keyword</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">Javascript Programmer</span><span style="color: #800000;">"</span><span style="color: #000000;">
    }
  }
}

#</span><span style="color: #0000ff;">global</span><span style="color: #000000;">
#global忽略query的条件限制
POST employees</span>/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>: <span style="color: #800080;">0</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">range</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">gte</span><span style="color: #800000;">"</span>: <span style="color: #800080;">40</span><span style="color: #000000;">
      }
    }
  },
  </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">jobs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">terms</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">job.keyword</span><span style="color: #800000;">"</span><span style="color: #000000;">
        
      }
    },
    
    </span><span style="color: #800000;">"</span><span style="color: #800000;">all</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
      </span><span style="color: #800000;">"</span><span style="color: #800000;">global</span><span style="color: #800000;">"</span><span style="color: #000000;">:{},
      </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">salary_avg</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
          </span><span style="color: #800000;">"</span><span style="color: #800000;">avg</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
            </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">salary</span><span style="color: #800000;">"</span><span style="color: #000000;">
          }
        }
      }
    }
  }
}</span></pre>
</div>
<p><strong>排序</strong></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">#排序 order 根据分桶之后的数量进行排序
POST employees</span>/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>: <span style="color: #800080;">0</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">range</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">gte</span><span style="color: #800000;">"</span>: <span style="color: #800080;">20</span><span style="color: #000000;">
      }
    }
  },
  </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">jobs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">terms</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">job.keyword</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">order</span><span style="color: #800000;">"</span><span style="color: #000000;">:[
          {</span><span style="color: #800000;">"</span><span style="color: #800000;">_count</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">asc</span><span style="color: #800000;">"</span><span style="color: #000000;">},
          {</span><span style="color: #800000;">"</span><span style="color: #800000;">_key</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">desc</span><span style="color: #800000;">"</span><span style="color: #000000;">}
          ]
        
      }
    }
  }
}


#排序 order 根据子聚合进行排序
POST employees</span>/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>: <span style="color: #800080;">0</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">jobs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">terms</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">job.keyword</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">order</span><span style="color: #800000;">"</span><span style="color: #000000;">:[  {
            </span><span style="color: #800000;">"</span><span style="color: #800000;">avg_salary</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">desc</span><span style="color: #800000;">"</span><span style="color: #000000;">
          }]
        
        
      },
    </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">avg_salary</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">avg</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">salary</span><span style="color: #800000;">"</span><span style="color: #000000;">
        }
      }
    }
    }
  }
}

#排序 order 根据子统计min进行排序
POST employees</span>/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>: <span style="color: #800080;">0</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">jobs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">terms</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">job.keyword</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">order</span><span style="color: #800000;">"</span><span style="color: #000000;">:[  {
            </span><span style="color: #800000;">"</span><span style="color: #800000;">stats_salary.min</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">desc</span><span style="color: #800000;">"</span><span style="color: #000000;">
          }]
        
        
      },
    </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">stats_salary</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">stats</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">salary</span><span style="color: #800000;">"</span><span style="color: #000000;">
        }
      }
    }
    }
  }
}<br /><br /></span></pre>
</div>
<p><strong>聚合分析精准度问题：</strong></p>
<p>doc_count_error_upper_bound：被遗漏的term分桶，包含的文档，有可能的最大值</p>
<p>sum_other_doc_count：除了返回结果bucket的terms以外，其他terms的文档总数（总数-返回的总数）</p>
<p>size和shard_size的区别？<br />size是最终返回多少个buckt的数量。<br />shard_size是每个bucket在一个shard上取回的bucket的总数。然后，每个shard上的结果，会在coordinate节点上在做一次汇总，返回总数。</p>
<p>①如何解决Terms不准的问题：</p>
<p>　　terms聚合分析不准的原因，数据分散在多个分片上，Coordinating Node无法获取数据全貌</p>
<p>　　解决方案1：当数据量不大时，设置Primary Shard为1；实现准确性</p>
<p>　　解决方案2：在分布式数据上，设置shard_size参数，提高精确度（原理：每次从shard上额外多获取数据，提升准确率）</p>
<p>&nbsp;</p>
<p>1，查询重复身份证号的第一个id：</p>
<div class="cnblogs_code">
<pre>GET xgj_ousu_payroll_sub_alias/<span style="color: #000000;">_search
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>: <span style="color: #800080;">0</span><span style="color: #000000;">, 
  </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">bool</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">filter</span><span style="color: #800000;">"</span><span style="color: #000000;">: [
        {</span><span style="color: #800000;">"</span><span style="color: #800000;">term</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">groupId</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">571709441825787907</span><span style="color: #800000;">"</span><span style="color: #000000;">
        }},
        {</span><span style="color: #800000;">"</span><span style="color: #800000;">term</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">payrollNo</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">583696291641577473</span><span style="color: #800000;">"</span><span style="color: #000000;">
        }}

      ]
    }
  },
  </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">ids</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">terms</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">idCardNo</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>:<span style="color: #800080;">100</span><span style="color: #000000;">
      },
      </span><span style="color: #800000;">"</span><span style="color: #800000;">aggs</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
         </span><span style="color: #800000;">"</span><span style="color: #800000;">first_doc</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">top_hits</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
            </span><span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>: <span style="color: #800080;">1</span><span style="color: #000000;">,
            </span><span style="color: #800000;">"</span><span style="color: #800000;">_source</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
              </span><span style="color: #800000;">"</span><span style="color: #800000;">includes</span><span style="color: #800000;">"</span>: [<span style="color: #800000;">"</span><span style="color: #800000;">id</span><span style="color: #800000;">"</span><span style="color: #000000;">]
            }
          }
         }
      }
    }
  }
}</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: #169fe6;"><strong><span style="color: #ffffff;">六、重建索引</span></strong></p>
<p>一般在以下几种情况下，需要重建索引</p>
<p>　　索引的mappings发生变更：字段类型更改，分词器及字典更新</p>
<p>　　索引的settings发生更改：索引的主分片数发生改变</p>
<p>　　集群内，集群间需要做数据迁移</p>
<p>Elasticsearch的内置提供API</p>
<p>　　Update By Query：在现有索引上重建</p>
<p>　　Reindex：在其他索引上重建索引</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;"># 修改 Mapping，增加子字段，使用英文分词器
PUT blogs</span>/<span style="color: #000000;">_mapping
{
      </span><span style="color: #800000;">"</span><span style="color: #800000;">properties</span><span style="color: #800000;">"</span><span style="color: #000000;"> : {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">content</span><span style="color: #800000;">"</span><span style="color: #000000;"> : {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span><span style="color: #000000;">,
          </span><span style="color: #800000;">"</span><span style="color: #800000;">fields</span><span style="color: #800000;">"</span><span style="color: #000000;"> : {
            </span><span style="color: #800000;">"</span><span style="color: #800000;">english</span><span style="color: #800000;">"</span><span style="color: #000000;"> : {
              </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span><span style="color: #000000;">,
              </span><span style="color: #800000;">"</span><span style="color: #800000;">analyzer</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">english</span><span style="color: #800000;">"</span><span style="color: #000000;">
            }
          }
        }
      }
    }

# Update所有文档
POST blogs</span>/<span style="color: #000000;">_update_by_query
{

}  <br /><br /># 替换字符串</span></pre>
<p>POST ousu_personnel_base_alias/_update_by_query<br />{<br />  "script":{<br />    "source":"def myStr=ctx._source['userPhoto'].replace('http://company.ousutec.cn:810/userpic/','http://supervisor2.oss-cn-hangzhou.aliyuncs.com/');ctx._source['userPhoto']=myStr;ctx._source['lastModifyTime']='2022-12-27T11:50:00';ctx._source['lastModifyUser']='头像修复';"<br />  },<br />  "query": {<br />    "bool": {<br />      "should": [<br />        {"wildcard":{<br />          "userPhoto":"http://company.ousutec.cn:810*"<br />        }}<br />      ]<br />    }<br />  }<br />}</p>
<pre></pre>
<p><br />POST ousu_personnel_job_alias/_update_by_query<br />{<br />  "script":{<br />    "source":"def myStr=ctx._source['userPhoto'].replace('http://company.ousutec.cn:810/userpic/','http://supervisor2.oss-cn-hangzhou.aliyuncs.com/');ctx._source['userPhoto']=myStr;ctx._source['lastModifyTime']='2022-12-27T11:55:00';ctx._source['lastModifyUser']='头像修复';"<br />  },<br />  "query": {<br />    "bool": {<br />      "should": [<br />        {"wildcard":{<br />          "userPhoto":"http://company.ousutec.cn:810*"<br />        }}<br />      ]<br />    }<br />  }<br />}</p>
<pre><span style="color: #000000;"><br /><br /><br />#删除字段</span></pre>
<p>POST ousu_personnel_base_alias/_update_by_query<br />{<br />  "script":{<br />    "source":"ctx._source.remove('birthday')"<br />  },<br />  "query": {<br />    "bool": {<br />      "filter": {<br />        "term": {<br />          "id": "1332023"<br />        }<br />      }<br />    }<br />  }<br />}</p>
<pre><span style="color: #000000;"><br /><br /></span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #000000;"># 创建新的索引并且设定新的Mapping
PUT blogs_fix</span>/<span style="color: #000000;">
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">mappings</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">properties</span><span style="color: #800000;">"</span><span style="color: #000000;"> : {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">content</span><span style="color: #800000;">"</span><span style="color: #000000;"> : {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span><span style="color: #000000;">,
          </span><span style="color: #800000;">"</span><span style="color: #800000;">fields</span><span style="color: #800000;">"</span><span style="color: #000000;"> : {
            </span><span style="color: #800000;">"</span><span style="color: #800000;">english</span><span style="color: #800000;">"</span><span style="color: #000000;"> : {
              </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span><span style="color: #000000;">,
              </span><span style="color: #800000;">"</span><span style="color: #800000;">analyzer</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">english</span><span style="color: #800000;">"</span><span style="color: #000000;">
            }
          }
        },
        </span><span style="color: #800000;">"</span><span style="color: #800000;">keyword</span><span style="color: #800000;">"</span><span style="color: #000000;"> : {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">keyword</span><span style="color: #800000;">"</span><span style="color: #000000;">
        }
      }    
  }
}

# Reindx API
POST  _reindex
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">source</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">blogs</span><span style="color: #800000;">"</span><span style="color: #000000;">
  },
  </span><span style="color: #800000;">"</span><span style="color: #800000;">dest</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">blogs_fix</span><span style="color: #800000;">"</span><span style="color: #000000;">
  }
}</span></pre>
</div>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: #169fe6;"><span style="color: #ffffff;"><strong>七、Ingest Pipeline&nbsp;</strong></span></p>
<p>1，测试</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;"># 测试split tags
POST _ingest</span>/pipeline/<span style="color: #000000;">_simulate
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">pipeline</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">description</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">to split blog tags</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">processors</span><span style="color: #800000;">"</span><span style="color: #000000;">: [
      {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">split</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">tags</span><span style="color: #800000;">"</span><span style="color: #000000;">,
          </span><span style="color: #800000;">"</span><span style="color: #800000;">separator</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">,</span><span style="color: #800000;">"</span><span style="color: #000000;">
        }
      }
    ]
  },
  </span><span style="color: #800000;">"</span><span style="color: #800000;">docs</span><span style="color: #800000;">"</span><span style="color: #000000;">: [
    {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">_index</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span><span style="color: #000000;">,
      </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">id</span><span style="color: #800000;">"</span><span style="color: #000000;">,
      </span><span style="color: #800000;">"</span><span style="color: #800000;">_source</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">title</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">Introducing big data......</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">tags</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">hadoop,elasticsearch,spark</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">content</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">You konw, for big data</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    },
    {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">_index</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span><span style="color: #000000;">,
      </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">idxx</span><span style="color: #800000;">"</span><span style="color: #000000;">,
      </span><span style="color: #800000;">"</span><span style="color: #800000;">_source</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">title</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">Introducing cloud computering</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">tags</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">openstack,k8s</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">content</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">You konw, for cloud</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    }
  ]
}</span></pre>
</div>
<p>2，创建pipeline</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;"># 为ES添加一个 Pipeline
PUT _ingest</span>/pipeline/<span style="color: #000000;">blog_pipeline
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">description</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">a blog pipeline</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">processors</span><span style="color: #800000;">"</span><span style="color: #000000;">: [
      {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">split</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
          </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">tags</span><span style="color: #800000;">"</span><span style="color: #000000;">,
          </span><span style="color: #800000;">"</span><span style="color: #800000;">separator</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">,</span><span style="color: #800000;">"</span><span style="color: #000000;">
        }
      },

      {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">set</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
          </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">views</span><span style="color: #800000;">"</span><span style="color: #000000;">,
          </span><span style="color: #800000;">"</span><span style="color: #800000;">value</span><span style="color: #800000;">"</span>: <span style="color: #800080;">0</span><span style="color: #000000;">
        }
      }
    ]
}

#查看Pipleline
GET _ingest</span>/pipeline/<span style="color: #000000;">blog_pipeline


#测试pipeline
POST _ingest</span>/pipeline/blog_pipeline/<span style="color: #000000;">_simulate
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">docs</span><span style="color: #800000;">"</span><span style="color: #000000;">: [
    {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">_source</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">title</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">Introducing cloud computering</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">tags</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">openstack,k8s</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">content</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">You konw, for cloud</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    }
  ]
}</span></pre>
</div>
<p>3，修复之前的数据</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">#增加update_by_query的条件
POST tech_blogs</span>/_update_by_query?pipeline=<span style="color: #000000;">blog_pipeline
{
    </span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">bool</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
            </span><span style="color: #800000;">"</span><span style="color: #800000;">must_not</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
                </span><span style="color: #800000;">"</span><span style="color: #800000;">exists</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
                    </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">views</span><span style="color: #800000;">"</span><span style="color: #000000;">
                }
            }
        }
    }
}</span></pre>
</div>
<p>4，使用pipeline更新添加文档</p>
<div class="cnblogs_code">
<pre>POST tech_blogs/_doc?pipeline=<span style="color: #000000;">blog_pipeline
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">title</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">Introducing big data......</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">tags</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">hadoop,elasticsearch,spark</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">content</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">You konw, for big data</span><span style="color: #800000;">"</span><span style="color: #000000;">
}
PUT tech_blogs</span>/_doc/<span style="color: #800080;">2</span>?pipeline=<span style="color: #000000;">blog_pipeline
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">title</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">Introducing cloud computering</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">tags</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">openstack,k8s</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">content</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">You konw, for cloud</span><span style="color: #800000;">"</span><span style="color: #000000;">
}</span></pre>
</div>
<div class="cnblogs_code" onclick="cnblogs_code_show('0d7d1cd9-4519-48e9-b6a2-64d1c81d85f9')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" id="code_img_closed_0d7d1cd9-4519-48e9-b6a2-64d1c81d85f9" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" id="code_img_opened_0d7d1cd9-4519-48e9-b6a2-64d1c81d85f9" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_0d7d1cd9-4519-48e9-b6a2-64d1c81d85f9" class="cnblogs_code_hide">
<pre>PUT _ingest/pipeline/<span style="color: #000000;">stackoverflow_pipeline
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">description</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">Pipeline for stackoverflow survey</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">processors</span><span style="color: #800000;">"</span><span style="color: #000000;">: [
    {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">split</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">DatabaseDesireNextYear</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">separator</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">;</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    },
    
    {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">split</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">DatabaseWorkedWith</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">separator</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">;</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    },
    
    {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">split</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">DevEnviron</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">separator</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">;</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    },
    
    {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">split</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">MiscTechDesireNextYear</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">separator</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">;</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    },
    
    {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">split</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">PlatformDesireNextYear</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">separator</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">;</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    },

   {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">split</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">WebFrameDesireNextYear</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">separator</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">;</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    }
    ,

   {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">split</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">field</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">Containers</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">separator</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">;</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    }

  ]
}</span></pre>
</div>
<span class="cnblogs_code_collapse">案例</span></div>
<p>&nbsp;</p>
GET xgj_ousu_payroll_sub_alias/_search{&nbsp; "size": 0,&nbsp;&nbsp; "query": {&nbsp; &nbsp; "bool": {&nbsp; &nbsp; &nbsp; "filter": [&nbsp; &nbsp; &nbsp; &nbsp; {"term": {&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; "groupId": "571709441825787907"&nbsp; &nbsp; &nbsp; &nbsp; }},&nbsp; &nbsp; &nbsp; &nbsp; {"term": {&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; "payrollNo": "583696291641577473"&nbsp; &nbsp; &nbsp; &nbsp; }}<br />&nbsp; &nbsp; &nbsp; ]&nbsp; &nbsp; }&nbsp; },&nbsp; "aggs": {&nbsp; &nbsp; "ids": {&nbsp; &nbsp; &nbsp; "terms": {&nbsp; &nbsp; &nbsp; &nbsp; "field": "idCardNo",&nbsp; &nbsp; &nbsp; &nbsp; "size":100&nbsp; &nbsp; &nbsp; },&nbsp; &nbsp; &nbsp; "aggs":{&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;"first_doc": {&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; "top_hits": {&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; "size": 1,&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; "_source": {&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; "includes": ["id"]&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; }&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; }&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;}&nbsp; &nbsp; &nbsp; }&nbsp; &nbsp; }&nbsp; }}