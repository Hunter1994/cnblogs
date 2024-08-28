<p style="font-size: 18pt; background-color: #169fe6;"><span style="color: #ffffff;"><strong>一、索引与文档</strong></span></p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202004/741594-20200406164931922-2135897361.png" alt="" width="593" height="316" /></p>
<p>&nbsp;</p>
<p>&nbsp;<img src="https://img2020.cnblogs.com/blog/741594/202004/741594-20200406165030077-2070153348.png" alt="" width="590" height="287" /></p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">查看索引相关信息</span>
<span style="color: #000000;">GET movies

</span><span style="color: #008000;">//</span><span style="color: #008000;">查看索引文档总数</span>
GET movies/_count</pre>
</div>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: #169fe6;"><span style="color: #ffffff;"><strong>二、集群与分片</strong></span></p>
<p>1，查看集群的健康状况&nbsp;<span class="cnblogs_code">GET _cluster/health</span>&nbsp;</p>
<p>green - 主分片副本都正常分配</p>
<p>yellow - 主分片全部正常分配，有副本分片未能正常分配</p>
<p>red - 有主分片未能分配（例如，当服务器的磁盘容量超过85%时。去创建了一个新的索引）</p>
<p>2，查询节点：&nbsp;<span class="cnblogs_code">GET _cat/nodes</span>&nbsp;</p>
<p>3，查询分片：&nbsp;<span class="cnblogs_code">GET _cat/shards</span>&nbsp;</p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: #169fe6;"><strong><span style="color: #ffffff;">三、CRUD与批量操作</span></strong></p>
<p>1，crud</p>
<p>index： 针对整个文档，既可以新增又可以更新；<br />create：只是新增操作，已有报错，可以用PUT指定ID，或POST不指定ID；<br />update：指的是部分更新，官方只是说用POST，请求body里用script或 doc里包含文档要更新的部分；<br />delete和read：就是delete和get请求了，比较简单。</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">创建文档，自动生成 _id</span>
POST user/<span style="color: #000000;">_doc
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">user</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">post_date</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">2020-04-06T20:35:20</span><span style="color: #800000;">"</span><span style="color: #000000;">
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">创建文档，指定id，如果已存在报错，不存在修改</span>
PUT user/_doc/<span style="color: #800080;">2</span>?op_type=<span style="color: #000000;">create
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">user</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">post_date</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">2020-04-06T20:35:20</span><span style="color: #800000;">"</span><span style="color: #000000;">
}
PUT user</span>/_create/<span style="color: #800080;">3</span><span style="color: #000000;">
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">user</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">post_date</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">2020-04-06T20:35:20</span><span style="color: #800000;">"</span><span style="color: #000000;">
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">查询_id=1的文档</span>
GET user/_doc/<span style="color: #800080;">3</span>

<span style="color: #008000;">//</span><span style="color: #008000;">删除指定的文档</span>
DELETE user/_doc/<span style="color: #800080;">3<br /><br />//删除</span></pre>
<p>POST employees/_delete_by_query<br />{<br />   "track_total_hits": true,<br />  "query": {<br />    "bool": {<br />      "filter": [<br />        {"terms": {<br />          "name.keyword": [<br />            "李四"<br />          ]<br />        }}<br />      ]<br />    }<br />  }<br />}</p>
<pre><span style="color: #800080;">&nbsp;<br />//批量修改<br /></span></pre>
<p>POST project_demo/_update_by_query<br />{<br />  "script":{<br />    "source":"ctx._source['is_deleted']=2"<br />  },<br />  "query": {<br />    "bool": {<br />      "filter": {<br />        "term": {<br />          "system_tag": "2"<br />        }<br />      }<br />    }<br />  }<br />}</p>
<pre><span style="color: #800080;"><br /><br /><br /></span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">在原文档上增加字段</span>
POST user/_update/<span style="color: #800080;">3</span><span style="color: #000000;">
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">doc</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
      </span><span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">20</span><span style="color: #800000;">"</span><span style="color: #000000;">,
      </span><span style="color: #800000;">"</span><span style="color: #800000;">post_date</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">2020-04-06T20:35:21</span><span style="color: #800000;">"</span><span style="color: #000000;">
  }
}<br /><br /></span></pre>
<p>POST employees/_update/DOBxx3MBH3d_nFQ4zJ-J<br />{<br />  "doc":{<br />      "name":"张飞"<br />  }<br />}</p>
<pre><span style="color: #000000;">&nbsp;</span></pre>
</div>
<p>&nbsp;</p>
<p>2，批量操作</p>
<p>①一次api调用，对不同的索引进行操作</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">新增文档、修改文档值、删除文档</span>
<span style="color: #000000;">POST _bulk
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span>:{<span style="color: #800000;">"</span><span style="color: #800000;">_index</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">test</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">1</span><span style="color: #800000;">"</span><span style="color: #000000;">}}
{</span><span style="color: #800000;">"</span><span style="color: #800000;">field1</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">value1</span><span style="color: #800000;">"</span><span style="color: #000000;">}
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">update</span><span style="color: #800000;">"</span>:{<span style="color: #800000;">"</span><span style="color: #800000;">_index</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">test</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">1</span><span style="color: #800000;">"</span><span style="color: #000000;">}}
{</span><span style="color: #800000;">"</span><span style="color: #800000;">doc</span><span style="color: #800000;">"</span>:{ <span style="color: #800000;">"</span><span style="color: #800000;">field1</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">value2</span><span style="color: #800000;">"</span><span style="color: #000000;">}}
{</span><span style="color: #800000;">"</span><span style="color: #800000;">delete</span><span style="color: #800000;">"</span>:{<span style="color: #800000;">"</span><span style="color: #800000;">_index</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">test</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">1</span><span style="color: #800000;">"</span>}}<br /><br /></pre>
<p>post _bulk<br />{"create":{"_index":"employees"}}<br />{"name":"李四","age":20,"mobile":"1300000000"}</p>
<p><br />POST employees/_bulk<br />{"index":{}}<br />{"name":"王五","age":20,"mobile":"1300000000"}</p>



</div>
<p>&nbsp;②批量读取</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">GET _mget
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">docs</span><span style="color: #800000;">"</span><span style="color: #000000;">:[
      {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">_index</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">user</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">3</span><span style="color: #800000;">"</span><span style="color: #000000;">
      },
      {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">_index</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">movies</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">3</span><span style="color: #800000;">"</span><span style="color: #000000;">
      }
    ]
}</span></pre>
</div>
<p>③批量查询</p>
<div class="cnblogs_code">
<pre>GET movies/<span style="color: #000000;">_msearch
{}
{</span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span>:{<span style="color: #800000;">"</span><span style="color: #800000;">match_all</span><span style="color: #800000;">"</span>:{}},<span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>:<span style="color: #800080;">1</span><span style="color: #000000;">}}
{</span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">user</span><span style="color: #800000;">"</span><span style="color: #000000;">}
{</span><span style="color: #800000;">"</span><span style="color: #800000;">query</span><span style="color: #800000;">"</span>:{<span style="color: #800000;">"</span><span style="color: #800000;">match_all</span><span style="color: #800000;">"</span>:{}},<span style="color: #800000;">"</span><span style="color: #800000;">size</span><span style="color: #800000;">"</span>:<span style="color: #800080;">1</span>}}</pre>
</div>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: #169fe6;"><strong><span style="color: #ffffff;">四、常见错误返回</span></strong></p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202004/741594-20200406212513733-2140743905.png" alt="" width="523" height="241" /></p>
<p>&nbsp;</p>