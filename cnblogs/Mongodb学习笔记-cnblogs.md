<p>&nbsp;</p>
<p><a href="#a1">一、CentOS安装mongodb</a></p>
<p><a href="#a2">二、mongodb的三个元素</a></p>
<p><a href="#a3">三、Bson Types</a></p>
<p><a href="#a4">四、Sql与Mogondb对比</a></p>
<p><a href="#a5">五、比较运算符</a></p>
<p><a href="#a6">六、逻辑运算符</a></p>
<p><a href="#a7">七、元素查询运算符</a></p>
<p><a href="#a8">八、评估查询运算符</a></p>
<p><a href="#a9">九、数组查询操作符</a></p>
<p><a href="#a10">十、更新操作结构</a></p>
<p><a href="#a11">十一、字段更新操作符</a></p>
<p><a href="#a12">十二、数组更新</a></p>
<p><a href="#a13">十三、位更新操作</a></p>
<p><a href="#q14">十四、CURD&nbsp;</a></p>
<p><a href="#a15">十五、索引</a></p>
<p><a href="#a16">十六、分布式文件系统GridFS</a></p>
<p><a href="#a17">十七、重量级聚合框架</a></p>
<p><a href="#a18">十八、轻量级聚合框架group</a></p>
<p><a href="#a19">十九、distinct</a></p>
<p><a href="#a20">二十、mapReduce</a></p>
<p><a href="#a21">二十一、master-slave</a></p>
<p><a href="#a22">二十二、ReplicaSet集群</a></p>
<p><a href="#a23">二十三、mongodb分片（未完成）</a></p>
<p><a href="#a24">二十四、驱动链接mongodb</a></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a1"></a>一、CentOS安装mongodb</span></strong></span></p>
<p>1，下载并安装mongodb</p>
<p>①下载地址：<a href="https://www.mongodb.com/download-center?jmp=nav#community" target="_blank">https://www.mongodb.com/download-center?jmp=nav#community</a></p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201801/741594-20180131210628609-1018346412.png" alt="" width="443" height="201" /></p>
<p>将下载的mongodb-linux-x86_64-3.6.2.tgz放置在centos的usr目录下</p>
<p>网盘下载：<a href="https://pan.baidu.com/s/1c4dcdig" target="_blank">https://pan.baidu.com/s/1c4dcdig</a></p>
<p>②解压：mongodb-linux-x86_64-3.6.2.tgz</p>
<p>进入mongodb-linux-x86_64-3.6.2文件夹创建一个db文件夹</p>
<p>③启动mongodb</p>
<p>命令：bin/mongod --dbpath=db</p>
<p>默认端口号：27017</p>
<p>2，下载并安装robomongo可视化工具</p>
<p>①下载地址：<a href="https://robomongo.org/" target="_blank">https://robomongo.org/</a></p>
<p>网盘下载：<a href="https://pan.baidu.com/s/1oAl5kT0" target="_blank">https://pan.baidu.com/s/1oAl5kT0</a></p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201802/741594-20180202153657000-804516367.png" alt="" width="568" height="228" /></p>
<p>&nbsp;</p>
<p>3，连接mongodb服务器</p>
<p><span style="font-size: 12px; color: #ff0000;">mongodb客户端一直连接不上centos的mongodb服务器</span><br /><span style="font-size: 12px; color: #ff0000;">启动mongodb服务须加上--bind_ip_all（例如：bin/mongod --dbpath=db --auth --bind_ip_all）</span></p>
<p><span style="font-size: 12px; color: #ff0000;">给mongodb服务器设置密码：</span><br /><span style="font-size: 12px; color: #ff0000;">①./mongo 连接mongodb服务器（./mongo --port 27017 -u "userAdmin" -p "123" --authenticationDatabase "admin"）</span><br /><span style="font-size: 12px; color: #ff0000;">②use admin 切换至admin数据库</span><br /><span style="font-size: 12px; color: #ff0000;">③db.createUser({user: "userAdmin",pwd: "123",roles: [ { role: "userAdminAnyDatabase", db: "admin" } ]}) 创建管理员用户，并指定其权限</span></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a2"></a>二、mongodb的三个元素</span></strong></span></p>
<p><span style="font-size: 12px;">mongodb &nbsp; 对应 &nbsp; sqlserver</span></p>
<p><span style="font-size: 12px;">database=》database</span></p>
<p><span style="font-size: 12px;">collection=》table</span></p>
<p><span style="font-size: 12px;">document=》row</span></p>
<p><span style="font-size: 12px;">1，基本操作</span></p>
<p><span style="font-size: 12px;">①创建database</span></p>
<p><span style="font-size: 12px;">②创建collection</span></p>
<p><span style="font-size: 12px;">③创建document</span></p>
<p>1，capped&nbsp;collection（固定集合）</p>
<p>①可视化设置固定集合</p>
<div>两种存储引擎：wiredtiger，mmap</div>
<p><img src="http://images2017.cnblogs.com/blog/741594/201802/741594-20180203162719031-643037444.png" alt="" width="395" height="335" /></p>
<p>②代码创建固定集合</p>
<p>1)简单创建固定集合</p>
<div class="cnblogs_code">
<pre>db.createCollection(<span style="color: #800000;">"</span><span style="color: #800000;">log</span><span style="color: #800000;">"</span>, { capped : <span style="color: #0000ff;">true</span>, size : <span style="color: #800080;">5242880</span>, max : <span style="color: #800080;">5000</span> } )</pre>
</div>
<p>2)复杂创建固定集合</p>
<div class="cnblogs_code">
<pre>db.createCollection(&lt;name&gt;<span style="color: #000000;">,
 { capped: </span>&lt;boolean&gt;<span style="color: #000000;">,
    autoIndexId: </span>&lt;boolean&gt;<span style="color: #000000;">,
    size: </span>&lt;number&gt;<span style="color: #000000;">,
    max: </span>&lt;number&gt;<span style="color: #000000;">,
    storageEngine: </span>&lt;document&gt;<span style="color: #000000;">,
    validator: </span>&lt;document&gt;<span style="color: #000000;">,
    validationLevel: </span>&lt;<span style="color: #0000ff;">string</span>&gt;<span style="color: #000000;">,
    validationAction: </span>&lt;<span style="color: #0000ff;">string</span>&gt;<span style="color: #000000;">,
    indexOptionDefaults: </span>&lt;document&gt;<span style="color: #000000;"> 
} )</span></pre>
</div>
<p>3)将集合转换为固定集合</p>
<div class="cnblogs_code">
<pre>db.runCommand({<span style="color: #800000;">"</span><span style="color: #800000;">convertToCapped</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">mycoll</span><span style="color: #800000;">"</span>, size: <span style="color: #800080;">100000</span>});</pre>
</div>
<p>4)查看collection的状态</p>
<div class="cnblogs_code">
<pre>db.log.stats()</pre>
</div>
<p>5)倒序查询</p>
<div class="cnblogs_code">
<pre>db.log.find().sort( { $natural: -<span style="color: #800080;">1</span> } )</pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a3"></a>三、Bson Types</span></strong></p>
<p>参考文档：<a href="https://docs.mongodb.com/manual/reference/bson-types/" target="_blank">https://docs.mongodb.com/manual/reference/bson-types/</a></p>
<table class="docutils" style="height: 468px; width: 748px;" border="1">
<thead valign="bottom">
<tr class="row-odd"><th class="head">Type</th><th class="head">Number</th><th class="head">Alias</th><th class="head">Notes</th></tr>
</thead>
<tbody valign="top">
<tr class="row-even">
<td>Double</td>
<td>1</td>
<td>&ldquo;double&rdquo;</td>
<td>&nbsp;</td>
</tr>
<tr class="row-odd">
<td>String</td>
<td>2</td>
<td>&ldquo;string&rdquo;</td>
<td>&nbsp;</td>
</tr>
<tr class="row-even">
<td>Object</td>
<td>3</td>
<td>&ldquo;object&rdquo;</td>
<td>&nbsp;</td>
</tr>
<tr class="row-odd">
<td>Array</td>
<td>4</td>
<td>&ldquo;array&rdquo;</td>
<td>&nbsp;</td>
</tr>
<tr class="row-even">
<td>Binary data</td>
<td>5</td>
<td>&ldquo;binData&rdquo;</td>
<td>&nbsp;</td>
</tr>
<tr class="row-odd">
<td>Undefined</td>
<td>6</td>
<td>&ldquo;undefined&rdquo;</td>
<td>Deprecated.</td>
</tr>
<tr class="row-even">
<td>ObjectId</td>
<td>7</td>
<td>&ldquo;objectId&rdquo;</td>
<td>&nbsp;</td>
</tr>
<tr class="row-odd">
<td>Boolean</td>
<td>8</td>
<td>&ldquo;bool&rdquo;</td>
<td>&nbsp;</td>
</tr>
<tr class="row-even">
<td>Date</td>
<td>9</td>
<td>&ldquo;date&rdquo;</td>
<td>&nbsp;</td>
</tr>
<tr class="row-odd">
<td>Null</td>
<td>10</td>
<td>&ldquo;null&rdquo;</td>
<td>&nbsp;</td>
</tr>
<tr class="row-even">
<td>Regular Expression</td>
<td>11</td>
<td>&ldquo;regex&rdquo;</td>
<td>&nbsp;</td>
</tr>
<tr class="row-odd">
<td>DBPointer</td>
<td>12</td>
<td>&ldquo;dbPointer&rdquo;</td>
<td>Deprecated.</td>
</tr>
<tr class="row-even">
<td>JavaScript</td>
<td>13</td>
<td>&ldquo;javascript&rdquo;</td>
<td>&nbsp;</td>
</tr>
<tr class="row-odd">
<td>Symbol</td>
<td>14</td>
<td>&ldquo;symbol&rdquo;</td>
<td>Deprecated.</td>
</tr>
<tr class="row-even">
<td>JavaScript (with scope)</td>
<td>15</td>
<td>&ldquo;javascriptWithScope&rdquo;</td>
<td>&nbsp;</td>
</tr>
<tr class="row-odd">
<td>32-bit integer</td>
<td>16</td>
<td>&ldquo;int&rdquo;</td>
<td>&nbsp;</td>
</tr>
<tr class="row-even">
<td>Timestamp</td>
<td>17</td>
<td>&ldquo;timestamp&rdquo;</td>
<td>&nbsp;</td>
</tr>
<tr class="row-odd">
<td>64-bit integer</td>
<td>18</td>
<td>&ldquo;long&rdquo;</td>
<td>&nbsp;</td>
</tr>
<tr class="row-even">
<td>Decimal128</td>
<td>19</td>
<td>&ldquo;decimal&rdquo;</td>
<td>New in version 3.4.</td>
</tr>
<tr class="row-odd">
<td>Min key</td>
<td>-1</td>
<td>&ldquo;minKey&rdquo;</td>
<td>&nbsp;</td>
</tr>
<tr class="row-even">
<td>Max key</td>
<td>127</td>
<td>&ldquo;maxKey&rdquo;</td>
<td>&nbsp;</td>
</tr>
</tbody>
</table>
<p>1，通过find操作，用undefined做作为比较条件</p>
<div class="cnblogs_code">
<pre>printjson(db.mycollection.find({<span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span>:{$type:<span style="color: #800080;">6</span><span style="color: #000000;">}}).toArray());
printjson(db.mycollection.find({</span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span>:{$type:<span style="color: #800000;">'</span><span style="color: #800000;">undefined</span><span style="color: #800000;">'</span>}}).toArray());</pre>
</div>
<p>2，Timestamps</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> a = <span style="color: #0000ff;">new</span><span style="color: #000000;"> Timestamp();
db.test.insertOne( { ts: a } );</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a4"></a>四、Sql与Mogondb对比</span></strong></span></p>
<p>1，创建和更改表</p>
<table style="width: 890px; height: 541px;" border="1">
<tbody>
<tr>
<td>SQL</td>
<td>Mongodb</td>
</tr>
<tr>
<td>
<pre><span class="k">CREATE <span class="k">TABLE <span class="n">people <span class="p">(
    <span class="n">id <span class="n">MEDIUMINT <span class="k">NOT <span class="k">NULL
        <span class="n">AUTO_INCREMENT<span class="p">,
    <span class="n">user_id <span class="nb">Varchar<span class="p">(<span class="mi">30<span class="p">),
    <span class="n">age <span class="nb">Number<span class="p">,
    <span class="n">status <span class="nb">char<span class="p">(<span class="mi">1<span class="p">),
    <span class="k">PRIMARY <span class="k">KEY <span class="p">(<span class="n">id<span class="p">)
<span class="p">)</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></pre>
</td>
<td>
<pre><span class="hll"><span class="nx">db<span class="p">.<span class="nx">people<span class="p">.<span class="nx">insertOne<span class="p">( <span class="p">{
<span class="hll">    <span class="nx">user_id<span class="o">: <span class="s2">"abc123"<span class="p">,
<span class="hll">    <span class="nx">age<span class="o">: <span class="mi">55<span class="p">,
<span class="hll">    <span class="nx">status<span class="o">: <span class="s2">"A"
<span class="hll"> <span class="p">} <span class="p">)</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span><br />或者<br /><span class="nx">db<span class="p">.<span class="nx">createCollection<span class="p">(<span class="s2">"people"<span class="p">)</span></span></span></span></span></span></pre>
</td>
</tr>
<tr>
<td>
<pre><span class="k">ALTER <span class="k">TABLE <span class="n">people
<span class="k">ADD <span class="n">join_date <span class="n">DATETIME</span></span></span></span></span></span></pre>
</td>
<td>&nbsp;
<pre><span class="hll"><span class="nx">db<span class="p">.<span class="nx">people<span class="p">.<span class="nx">updateMany<span class="p">(
<span class="hll">    <span class="p">{ <span class="p">},
<span class="hll">    <span class="p">{ <span class="nx">$set<span class="o">: <span class="p">{ <span class="nx">join_date<span class="o">: <span class="k">new <span class="nb">Date<span class="p">() <span class="p">} <span class="p">}
<span class="hll"><span class="p">)</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></pre>
</td>
</tr>
<tr>
<td>
<pre><span class="k">ALTER <span class="k">TABLE <span class="n">people
<span class="k">DROP <span class="k">COLUMN <span class="n">join_date</span></span></span></span></span></span></pre>
</td>
<td>&nbsp;
<pre><span class="hll"><span class="nx">db<span class="p">.<span class="nx">people<span class="p">.<span class="nx">updateMany<span class="p">(
<span class="hll">    <span class="p">{ <span class="p">},
<span class="hll">    <span class="p">{ <span class="nx">$unset<span class="o">: <span class="p">{ <span class="s2">"join_date"<span class="o">: <span class="s2">"" <span class="p">} <span class="p">}
<span class="hll"><span class="p">)</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></pre>
</td>
</tr>
<tr>
<td>
<pre><span class="k">CREATE <span class="k">INDEX <span class="n">idx_user_id_asc
<span class="k">ON <span class="n">people<span class="p">(<span class="n">user_id<span class="p">)</span></span></span></span></span></span></span></span></pre>
</td>
<td>&nbsp;<span class="nx">db<span class="p">.<span class="nx">people<span class="p">.<span class="nx">createIndex<span class="p">( <span class="p">{ <span class="nx">user_id<span class="o">: <span class="mi">1 <span class="p">} <span class="p">)</span></span></span></span></span></span></span></span></span></span></span></span></td>
</tr>
<tr>
<td>
<pre><span class="k">CREATE <span class="k">INDEX
       <span class="n">idx_user_id_asc_age_desc
<span class="k">ON <span class="n">people<span class="p">(<span class="n">user_id<span class="p">, <span class="n">age <span class="k">DESC<span class="p">)</span></span></span></span></span></span></span></span></span></span></span></pre>
</td>
<td>&nbsp;<span class="nx">db<span class="p">.<span class="nx">people<span class="p">.<span class="nx">createIndex<span class="p">( <span class="p">{ <span class="nx">user_id<span class="o">: <span class="mi">1<span class="p">, <span class="nx">age<span class="o">: <span class="o">-<span class="mi">1 <span class="p">} <span class="p">)</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></td>
</tr>
<tr>
<td>
<pre><span class="k">DROP <span class="k">TABLE <span class="n">people</span></span></span></pre>
</td>
<td>&nbsp;<span class="nx">db<span class="p">.<span class="nx">people<span class="p">.<span class="nx">drop<span class="p">()</span></span></span></span></span></span></td>
</tr>
</tbody>
</table>
<p>2，插入数据</p>
<table style="height: 146px; width: 886px;" border="1">
<tbody>
<tr>
<td>SQL</td>
<td>Mongodb</td>
</tr>
<tr>
<td>
<pre><span class="k">INSERT <span class="k">INTO <span class="n">people<span class="p">(<span class="n">user_id<span class="p">,
                  <span class="n">age<span class="p">,
                  <span class="n">status<span class="p">)
<span class="k">VALUES <span class="p">(<span class="ss">"bcd001"<span class="p">,
        <span class="mi">45<span class="p">,
        <span class="ss">"A"<span class="p">)</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></pre>
</td>
<td>
<pre><span class="hll"><span class="nx">db<span class="p">.<span class="nx">people<span class="p">.<span class="nx">insertOne<span class="p">(
   <span class="p">{ <span class="nx">user_id<span class="o">: <span class="s2">"bcd001"<span class="p">, <span class="nx">age<span class="o">: <span class="mi">45<span class="p">, <span class="nx">status<span class="o">: <span class="s2">"A" <span class="p">}
<span class="p">)</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></pre>
<pre><span class="hll"><span class="nx"><span class="p"><span class="nx"><span class="p"><span class="nx"><span class="p"><span class="p"><span class="hll"><span class="nx"><span class="o"><span class="s2"><span class="p"><span class="hll"><span class="nx"><span class="o"><span class="mi"><span class="p"><span class="hll"><span class="nx"><span class="o"><span class="s2"><span class="hll"><span class="p"><span class="p"><span class="nx"><span class="p"><span class="nx"><span class="p"><span class="s2"><span class="p">&nbsp;</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></pre>
</td>
</tr>
</tbody>
</table>
<p>3，查询数据</p>
<p>&nbsp;</p>
<table style="width: 886px;" border="1">
<tbody>
<tr>
<td>SQL</td>
<td>Mongodb</td>
</tr>
<tr>
<td>
<pre><span class="k">SELECT <span class="o">*
<span class="k">FROM <span class="n">people</span></span></span></span></pre>
</td>
<td>
<pre><span class="nx">db<span class="p">.<span class="nx">people<span class="p">.<span class="nx">find<span class="p">()</span></span></span></span></span></span></pre>
<p><span class="hll"><span class="nx"><span class="p"><span class="nx"><span class="p"><span class="nx"><span class="p"><span class="p"><span class="nx"><span class="o"><span class="s2"><span class="p"><span class="nx"><span class="o"><span class="mi"><span class="p"><span class="nx"><span class="o"><span class="s2"><span class="p"><span class="p">&nbsp;</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></p>
</td>
</tr>
<tr>
<td>
<pre><span class="k">SELECT <span class="n">id<span class="p">,
       <span class="n">user_id<span class="p">,
       <span class="n">status
<span class="k">FROM <span class="n">people</span></span></span></span></span></span></span></span></pre>
</td>
<td>&nbsp;
<pre><span class="hll"><span class="nx">db<span class="p">.<span class="nx">people<span class="p">.<span class="nx">find<span class="p">(
<span class="hll">    <span class="p">{ <span class="p">},
<span class="hll">    <span class="p">{ <span class="nx">user_id<span class="o">: <span class="mi">1<span class="p">, <span class="nx">status<span class="o">: <span class="mi">1 <span class="p">}
<span class="hll"><span class="p">)</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></pre>
</td>
</tr>
<tr>
<td>
<pre><span class="k">SELECT <span class="n">user_id<span class="p">, <span class="n">status
<span class="k">FROM <span class="n">people</span></span></span></span></span></span></pre>
</td>
<td>&nbsp;
<pre><span class="hll"><span class="nx">db<span class="p">.<span class="nx">people<span class="p">.<span class="nx">find<span class="p">(
<span class="hll">    <span class="p">{ <span class="p">},
<span class="hll">    <span class="p">{ <span class="nx">user_id<span class="o">: <span class="mi">1<span class="p">, <span class="nx">status<span class="o">: <span class="mi">1<span class="p">, <span class="nx">_id<span class="o">: <span class="mi">0 <span class="p">}
<span class="hll"><span class="p">)</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></pre>
</td>
</tr>
<tr>
<td>
<pre><span class="k">SELECT <span class="o">*
<span class="k">FROM <span class="n">people
<span class="k">WHERE <span class="n">status <span class="o">= <span class="ss">"A"</span></span></span></span></span></span></span></span></pre>
</td>
<td>&nbsp;
<pre><span class="hll"><span class="nx">db<span class="p">.<span class="nx">people<span class="p">.<span class="nx">find<span class="p">(
<span class="hll">    <span class="p">{ <span class="nx">status<span class="o">: <span class="s2">"A" <span class="p">}
<span class="hll"><span class="p">)</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></pre>
</td>
</tr>
<tr>
<td>
<pre><span class="k">SELECT <span class="n">user_id<span class="p">, <span class="n">status
<span class="k">FROM <span class="n">people
<span class="k">WHERE <span class="n">status <span class="o">= <span class="ss">"A"</span></span></span></span></span></span></span></span></span></span></pre>
</td>
<td>&nbsp;
<pre><span class="hll"><span class="nx">db<span class="p">.<span class="nx">people<span class="p">.<span class="nx">find<span class="p">(
<span class="hll">    <span class="p">{ <span class="nx">status<span class="o">: <span class="s2">"A" <span class="p">},
<span class="hll">    <span class="p">{ <span class="nx">user_id<span class="o">: <span class="mi">1<span class="p">, <span class="nx">status<span class="o">: <span class="mi">1<span class="p">, <span class="nx">_id<span class="o">: <span class="mi">0 <span class="p">}
<span class="p">)</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></pre>
</td>
</tr>
<tr>
<td>
<pre><span class="k">SELECT <span class="o">*
<span class="k">FROM <span class="n">people
<span class="k">WHERE <span class="n">status <span class="o">!= <span class="ss">"A"</span></span></span></span></span></span></span></span></pre>
</td>
<td>&nbsp;
<pre><span class="hll"><span class="nx">db<span class="p">.<span class="nx">people<span class="p">.<span class="nx">find<span class="p">(
<span class="hll">    <span class="p">{ <span class="nx">status<span class="o">: <span class="p">{ <span class="nx">$ne<span class="o">: <span class="s2">"A" <span class="p">} <span class="p">}
<span class="hll"><span class="p">)</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></pre>
</td>
</tr>
<tr>
<td>
<pre><span class="k">SELECT <span class="o">*
<span class="k">FROM <span class="n">people
<span class="k">WHERE <span class="n">status <span class="o">= <span class="ss">"A"
<span class="k">AND <span class="n">age <span class="o">= <span class="mi">50</span></span></span></span></span></span></span></span></span></span></span></span></pre>
</td>
<td>&nbsp;
<pre><span class="hll"><span class="nx">db<span class="p">.<span class="nx">people<span class="p">.<span class="nx">find<span class="p">(
<span class="hll">    <span class="p">{ <span class="nx">status<span class="o">: <span class="s2">"A"<span class="p">,
<span class="hll">      <span class="nx">age<span class="o">: <span class="mi">50 <span class="p">}
<span class="hll"><span class="p">)</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></pre>
</td>
</tr>
<tr>
<td>
<pre><span class="k">SELECT <span class="o">*
<span class="k">FROM <span class="n">people
<span class="k">WHERE <span class="n">status <span class="o">= <span class="ss">"A"
<span class="k">OR <span class="n">age <span class="o">= <span class="mi">50</span></span></span></span></span></span></span></span></span></span></span></span></pre>
</td>
<td>&nbsp;
<pre><span class="hll"><span class="nx">db<span class="p">.<span class="nx">people<span class="p">.<span class="nx">find<span class="p">(
<span class="hll">    <span class="p">{ <span class="nx">$or<span class="o">: <span class="p">[ <span class="p">{ <span class="nx">status<span class="o">: <span class="s2">"A" <span class="p">} <span class="p">,
<span class="hll">             <span class="p">{ <span class="nx">age<span class="o">: <span class="mi">50 <span class="p">} <span class="p">] <span class="p">}
<span class="hll"><span class="p">)</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></pre>
</td>
</tr>
<tr>
<td>
<pre><span class="k">SELECT <span class="o">*
<span class="k">FROM <span class="n">people
<span class="k">WHERE <span class="n">age <span class="o">&gt; <span class="mi">25</span></span></span></span></span></span></span></span></pre>
</td>
<td>&nbsp;
<pre><span class="hll"><span class="nx">db<span class="p">.<span class="nx">people<span class="p">.<span class="nx">find<span class="p">(
<span class="hll">    <span class="p">{ <span class="nx">age<span class="o">: <span class="p">{ <span class="nx">$gt<span class="o">: <span class="mi">25 <span class="p">} <span class="p">}
<span class="hll"><span class="p">)</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></pre>
</td>
</tr>
<tr>
<td>
<pre><span class="k">SELECT <span class="o">*
<span class="k">FROM <span class="n">people
<span class="k">WHERE <span class="n">age <span class="o">&lt; <span class="mi">25</span></span></span></span></span></span></span></span></pre>
</td>
<td>&nbsp;
<pre><span class="hll"><span class="nx">db<span class="p">.<span class="nx">people<span class="p">.<span class="nx">find<span class="p">(
<span class="hll">   <span class="p">{ <span class="nx">age<span class="o">: <span class="p">{ <span class="nx">$lt<span class="o">: <span class="mi">25 <span class="p">} <span class="p">}
<span class="hll"><span class="p">)</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></pre>
</td>
</tr>
<tr>
<td>
<pre><span class="k">SELECT <span class="o">*
<span class="k">FROM <span class="n">people
<span class="k">WHERE <span class="n">age <span class="o">&gt; <span class="mi">25
<span class="k">AND   <span class="n">age <span class="o">&lt;= <span class="mi">50</span></span></span></span></span></span></span></span></span></span></span></span></pre>
</td>
<td>&nbsp;
<pre><span class="hll"><span class="nx">db<span class="p">.<span class="nx">people<span class="p">.<span class="nx">find<span class="p">(
<span class="hll">   <span class="p">{ <span class="nx">age<span class="o">: <span class="p">{ <span class="nx">$gt<span class="o">: <span class="mi">25<span class="p">, <span class="nx">$lte<span class="o">: <span class="mi">50 <span class="p">} <span class="p">}
<span class="hll"><span class="p">)</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></pre>
</td>
</tr>
<tr>
<td>
<pre><span class="k">SELECT <span class="o">*
<span class="k">FROM <span class="n">people
<span class="k">WHERE <span class="n">user_id <span class="k">like <span class="ss">"%bc%"</span></span></span></span></span></span></span></span></pre>
</td>
<td>&nbsp;
<div class="first highlight-javascript">
<div class="highlight">
<pre><span class="hll"><span class="nx">db<span class="p">.<span class="nx">people<span class="p">.<span class="nx">find<span class="p">( <span class="p">{ <span class="nx">user_id<span class="o">: <span class="sr">/bc/ <span class="p">} <span class="p">)</span></span></span></span></span></span></span></span></span></span></span></span></span></pre>
</div>
</div>
<div class="last highlight-javascript">
<div class="highlight">
<pre><span class="hll"><span class="nx">db<span class="p">.<span class="nx">people<span class="p">.<span class="nx">find<span class="p">( <span class="p">{ <span class="nx">user_id<span class="o">: <span class="p">{ <span class="nx">$regex<span class="o">: <span class="sr">/bc/ <span class="p">} <span class="p">} <span class="p">)</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></pre>
</div>
</div>
</td>
</tr>
<tr>
<td>
<pre><span class="k">SELECT <span class="o">*
<span class="k">FROM <span class="n">people
<span class="k">WHERE <span class="n">user_id <span class="k">like <span class="ss">"bc%"</span></span></span></span></span></span></span></span></pre>
</td>
<td>
<div class="first highlight-javascript">
<div class="highlight">
<pre><span class="hll"><span class="nx">db<span class="p">.<span class="nx">people<span class="p">.<span class="nx">find<span class="p">( <span class="p">{ <span class="nx">user_id<span class="o">: <span class="sr">/^bc/ <span class="p">} <span class="p">)</span></span></span></span></span></span></span></span></span></span></span></span></span></pre>
</div>
</div>
<div class="last highlight-javascript">
<div class="highlight">
<pre><span class="hll"><span class="nx">db<span class="p">.<span class="nx">people<span class="p">.<span class="nx">find<span class="p">( <span class="p">{ <span class="nx">user_id<span class="o">: <span class="p">{ <span class="nx">$regex<span class="o">: <span class="sr">/^bc/ <span class="p">} <span class="p">} <span class="p">)</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></pre>
</div>
</div>
</td>
</tr>
<tr>
<td>
<pre><span class="k">SELECT <span class="o">*
<span class="k">FROM <span class="n">people
<span class="k">WHERE <span class="n">status <span class="o">= <span class="ss">"A"
<span class="k">ORDER <span class="k">BY <span class="n">user_id <span class="k">ASC</span></span></span></span></span></span></span></span></span></span></span></span></pre>
</td>
<td>&nbsp;<span class="nx">db<span class="p">.<span class="nx">people<span class="p">.<span class="nx">find<span class="p">( <span class="p">{ <span class="nx">status<span class="o">: <span class="s2">"A" <span class="p">} <span class="p">).<span class="nx">sort<span class="p">( <span class="p">{ <span class="nx">user_id<span class="o">: <span class="mi">1 <span class="p">} <span class="p">)</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></td>
</tr>
<tr>
<td>
<pre><span class="k">SELECT <span class="o">*
<span class="k">FROM <span class="n">people
<span class="k">WHERE <span class="n">status <span class="o">= <span class="ss">"A"
<span class="k">ORDER <span class="k">BY <span class="n">user_id <span class="k">DESC</span></span></span></span></span></span></span></span></span></span></span></span></pre>
</td>
<td>&nbsp;<span class="nx">db<span class="p">.<span class="nx">people<span class="p">.<span class="nx">find<span class="p">( <span class="p">{ <span class="nx">status<span class="o">: <span class="s2">"A" <span class="p">} <span class="p">).<span class="nx">sort<span class="p">( <span class="p">{ <span class="nx">user_id<span class="o">: <span class="o">-<span class="mi">1 <span class="p">} <span class="p">)</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></td>
</tr>
<tr>
<td>
<pre><span class="k">SELECT <span class="k">COUNT<span class="p">(<span class="o">*<span class="p">)
<span class="k">FROM <span class="n">people</span></span></span></span></span></span></span></pre>
</td>
<td>&nbsp;
<div class="first highlight-javascript">
<div class="highlight">
<pre><span class="hll"><span class="nx">db<span class="p">.<span class="nx">people<span class="p">.<span class="nx">count<span class="p">()</span></span></span></span></span></span></span></pre>
</div>
</div>
<div class="last highlight-javascript">
<div class="highlight">
<pre><span class="hll"><span class="nx">db<span class="p">.<span class="nx">people<span class="p">.<span class="nx">find<span class="p">().<span class="nx">count<span class="p">()</span></span></span></span></span></span></span></span></span></pre>
</div>
</div>
</td>
</tr>
<tr>
<td>
<pre><span class="k">SELECT <span class="k">COUNT<span class="p">(<span class="n">user_id<span class="p">)
<span class="k">FROM <span class="n">people</span></span></span></span></span></span></span></pre>
</td>
<td>&nbsp;
<div class="first highlight-javascript">
<div class="highlight">
<pre><span class="hll"><span class="nx">db<span class="p">.<span class="nx">people<span class="p">.<span class="nx">count<span class="p">( <span class="p">{ <span class="nx">user_id<span class="o">: <span class="p">{ <span class="nx">$exists<span class="o">: <span class="kc">true <span class="p">} <span class="p">} <span class="p">)</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></pre>
</div>
</div>
<div class="last highlight-javascript">
<div class="highlight">
<pre><span class="hll"><span class="nx">db<span class="p">.<span class="nx">people<span class="p">.<span class="nx">find<span class="p">( <span class="p">{ <span class="nx">user_id<span class="o">: <span class="p">{ <span class="nx">$exists<span class="o">: <span class="kc">true <span class="p">} <span class="p">} <span class="p">).<span class="nx">count<span class="p">()</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></pre>
</div>
</div>
</td>
</tr>
<tr>
<td>
<pre><span class="k">SELECT <span class="k">COUNT<span class="p">(<span class="o">*<span class="p">)
<span class="k">FROM <span class="n">people
<span class="k">WHERE <span class="n">age <span class="o">&gt; <span class="mi">30</span></span></span></span></span></span></span></span></span></span></span></pre>
</td>
<td>&nbsp;
<div class="first highlight-javascript">
<div class="highlight">
<pre><span class="hll"><span class="nx">db<span class="p">.<span class="nx">people<span class="p">.<span class="nx">count<span class="p">( <span class="p">{ <span class="nx">age<span class="o">: <span class="p">{ <span class="nx">$gt<span class="o">: <span class="mi">30 <span class="p">} <span class="p">} <span class="p">)</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></pre>
</div>
</div>
<div class="last highlight-javascript">
<div class="highlight">
<pre><span class="hll"><span class="nx">db<span class="p">.<span class="nx">people<span class="p">.<span class="nx">find<span class="p">( <span class="p">{ <span class="nx">age<span class="o">: <span class="p">{ <span class="nx">$gt<span class="o">: <span class="mi">30 <span class="p">} <span class="p">} <span class="p">).<span class="nx">count<span class="p">()</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></pre>
</div>
</div>
</td>
</tr>
<tr>
<td>
<pre><span class="k">SELECT <span class="k">DISTINCT<span class="p">(<span class="n">status<span class="p">)
<span class="k">FROM <span class="n">people</span></span></span></span></span></span></span></pre>
</td>
<td>&nbsp;
<div class="first highlight-javascript">
<div class="highlight">
<pre><span class="hll"><span class="nx">db<span class="p">.<span class="nx">people<span class="p">.<span class="nx">aggregate<span class="p">( <span class="p">[ <span class="p">{ <span class="nx">$group <span class="o">: <span class="p">{ <span class="nx">_id <span class="o">: <span class="s2">"$status" <span class="p">} <span class="p">} <span class="p">] <span class="p">)</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></pre>
</div>
</div>
<div class="last highlight-javascript">
<div class="highlight">
<pre><span class="hll"><span class="nx">db<span class="p">.<span class="nx">people<span class="p">.<span class="nx">distinct<span class="p">( <span class="s2">"status" <span class="p">)</span></span></span></span></span></span></span></span></span></pre>
</div>
</div>
</td>
</tr>
<tr>
<td>
<pre><span class="k">SELECT <span class="o">*
<span class="k">FROM <span class="n">people
<span class="k">LIMIT <span class="mi">1</span></span></span></span></span></span></pre>
</td>
<td>&nbsp;
<div class="first highlight-javascript">
<div class="highlight">
<pre><span class="hll"><span class="nx">db<span class="p">.<span class="nx">people<span class="p">.<span class="nx">findOne<span class="p">()</span></span></span></span></span></span></span></pre>
</div>
</div>
<div class="last highlight-javascript">
<div class="highlight">
<pre><span class="hll"><span class="nx">db<span class="p">.<span class="nx">people<span class="p">.<span class="nx">find<span class="p">().<span class="nx">limit<span class="p">(<span class="mi">1<span class="p">)</span></span></span></span></span></span></span></span></span></span></span></pre>
</div>
</div>
</td>
</tr>
<tr>
<td>
<pre><span class="k">SELECT <span class="o">*
<span class="k">FROM <span class="n">people
<span class="k">LIMIT <span class="mi">5
<span class="n">SKIP <span class="mi">10</span></span></span></span></span></span></span></span></pre>
</td>
<td>&nbsp;<span class="nx">db<span class="p">.<span class="nx">people<span class="p">.<span class="nx">find<span class="p">().<span class="nx">limit<span class="p">(<span class="mi">5<span class="p">).<span class="nx">skip<span class="p">(<span class="mi">10<span class="p">)</span></span></span></span></span></span></span></span></span></span></span></span></span></span></td>
</tr>
<tr>
<td>
<pre><span class="k">EXPLAIN <span class="k">SELECT <span class="o">*
<span class="k">FROM <span class="n">people
<span class="k">WHERE <span class="n">status <span class="o">= <span class="ss">"A"</span></span></span></span></span></span></span></span></span></pre>
</td>
<td>&nbsp;<span class="nx">db<span class="p">.<span class="nx">people<span class="p">.<span class="nx">find<span class="p">( <span class="p">{ <span class="nx">status<span class="o">: <span class="s2">"A" <span class="p">} <span class="p">).<span class="nx">explain<span class="p">()</span></span></span></span></span></span></span></span></span></span></span></span></span></span></td>
</tr>
</tbody>
</table>
<p>4，修改数据</p>
<table style="width: 886px;" border="1">
<tbody>
<tr>
<td>SQL</td>
<td>Mongodb</td>
</tr>
<tr>
<td>
<pre><span class="k">UPDATE <span class="n">people
<span class="k">SET <span class="n">status <span class="o">= <span class="ss">"C"
<span class="k">WHERE <span class="n">age <span class="o">&gt; <span class="mi">25</span></span></span></span></span></span></span></span></span></span></pre>
</td>
<td>
<pre><span class="hll"><span class="nx">db<span class="p">.<span class="nx">people<span class="p">.<span class="nx">updateMany<span class="p">(
<span class="hll">   <span class="p">{ <span class="nx">age<span class="o">: <span class="p">{ <span class="nx">$gt<span class="o">: <span class="mi">25 <span class="p">} <span class="p">},
<span class="hll">   <span class="p">{ <span class="nx">$set<span class="o">: <span class="p">{ <span class="nx">status<span class="o">: <span class="s2">"C" <span class="p">} <span class="p">}
<span class="hll"><span class="p">)</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></pre>
</td>
</tr>
<tr>
<td>
<pre><span class="k">UPDATE <span class="n">people
<span class="k">SET <span class="n">age <span class="o">= <span class="n">age <span class="o">+ <span class="mi">3
<span class="k">WHERE <span class="n">status <span class="o">= <span class="ss">"A"</span></span></span></span></span></span></span></span></span></span></span></span></pre>
</td>
<td>&nbsp;
<pre><span class="hll"><span class="nx">db<span class="p">.<span class="nx">people<span class="p">.<span class="nx">updateMany<span class="p">(
<span class="hll">   <span class="p">{ <span class="nx">status<span class="o">: <span class="s2">"A" <span class="p">} <span class="p">,
<span class="hll">   <span class="p">{ <span class="nx">$inc<span class="o">: <span class="p">{ <span class="nx">age<span class="o">: <span class="mi">3 <span class="p">} <span class="p">}
<span class="hll"><span class="p">)</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></pre>
</td>
</tr>
</tbody>
</table>
<p>5，删除数据</p>
<table style="height: 134px; width: 892px;" border="1">
<tbody>
<tr>
<td>SQL</td>
<td>Mongodb</td>
</tr>
<tr>
<td>
<pre><span class="k">DELETE <span class="k">FROM <span class="n">people
<span class="k">WHERE <span class="n">status <span class="o">= <span class="ss">"D"</span></span></span></span></span></span></span></pre>
</td>
<td>
<pre><span class="nx">db<span class="p">.<span class="nx">people<span class="p">.<span class="nx">deleteMany<span class="p">( <span class="p">{ <span class="nx">status<span class="o">: <span class="s2">"D" <span class="p">} <span class="p">)</span></span></span></span></span></span></span></span></span></span></span></span></pre>
</td>
</tr>
<tr>
<td>
<pre><span class="k">DELETE <span class="k">FROM <span class="n">people</span></span></span></pre>
</td>
<td>&nbsp;
<pre><span class="nx">db<span class="p">.<span class="nx">people<span class="p">.<span class="nx">deleteMany<span class="p">({})</span></span></span></span></span></span></pre>
</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a5"></a>五、比较运算符</span></strong></span></p>
<table style="height: 190px; width: 741px;" border="1">
<tbody>
<tr>
<td>比较运算符</td>
<td>备注</td>
<td>说明</td>
<td>用法</td>
</tr>
<tr>
<td>$eq</td>
<td>=</td>
<td>equal</td>
<td>
<pre><span class="p">{ <span class="o">&lt;<span class="nx">field<span class="o">&gt;: <span class="p">{ <span class="nx">$eq<span class="o">: <span class="o">&lt;<span class="nx">value<span class="o">&gt; <span class="p">} <span class="p">}<br />相当于<span class="pre">{&nbsp;<span class="pre">field:&nbsp;<span class="pre">&lt;value&gt;&nbsp;<span class="pre">}</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></pre>
</td>
</tr>
<tr>
<td>$gt</td>
<td>&gt;</td>
<td>greater than</td>
<td><span class="pre">{field:&nbsp;<span class="pre">{$gt:&nbsp;<span class="pre">value}&nbsp;<span class="pre">}</span></span></span></span></td>
</tr>
<tr>
<td>$gte</td>
<td>&gt;=</td>
<td>greater than&nbsp;equal</td>
<td><span class="pre">{field:&nbsp;<span class="pre">{$gte:&nbsp;<span class="pre">value}&nbsp;<span class="pre">}</span></span></span></span></td>
</tr>
<tr>
<td>$lt</td>
<td>&lt;</td>
<td>less than</td>
<td>
<pre>{field:&nbsp;<span class="pre">{$lt:&nbsp;<span class="pre">value}&nbsp;<span class="pre">}</span></span></span></pre>
</td>
</tr>
<tr>
<td>$lte</td>
<td>&lt;=</td>
<td>less than&nbsp;equal</td>
<td>{&nbsp;<span class="pre">field:&nbsp;<span class="pre">{&nbsp;<span class="pre">$lte:&nbsp;<span class="pre">value}&nbsp;<span class="pre">}</span></span></span></span></span></td>
</tr>
<tr>
<td>$ne</td>
<td>!=</td>
<td>not equal</td>
<td>&nbsp;<code class="docutils literal"><span class="pre">{field:&nbsp;<span class="pre">{$ne:&nbsp;<span class="pre">value}&nbsp;<span class="pre">}</span></span></span></span></code></td>
</tr>
<tr>
<td>$in</td>
<td>in</td>
<td>&nbsp;</td>
<td>
<pre><span class="p">{ <span class="nx">field<span class="o">: <span class="p">{ <span class="nx">$in<span class="o">: <span class="p">[<span class="o">&lt;<span class="nx">value1<span class="o">&gt;<span class="p">, <span class="o">&lt;<span class="nx">value2<span class="o">&gt;<span class="p">, <span class="p">... <span class="o">&lt;<span class="nx">valueN<span class="o">&gt; <span class="p">] <span class="p">} <span class="p">}</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></pre>
</td>
</tr>
<tr>
<td>$nin</td>
<td>!in</td>
<td>not in</td>
<td><span class="pre">{&nbsp;<span class="pre">field:&nbsp;<span class="pre">{&nbsp;<span class="pre">$nin:&nbsp;<span class="pre">[&nbsp;<span class="pre">&lt;value1&gt;,&nbsp;<span class="pre">&lt;value2&gt;&nbsp;<span class="pre">...&nbsp;<span class="pre">&lt;valueN&gt;&nbsp;<span class="pre">]}&nbsp;<span class="pre">}</span></span></span></span></span></span></span></span></span></span></span></td>
</tr>
</tbody>
</table>
<p>1，测试数据</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.inventory.insert([
{ _id: </span><span style="color: #800080;">1</span>, item: { name: <span style="color: #800000;">"</span><span style="color: #800000;">ab</span><span style="color: #800000;">"</span>, code: <span style="color: #800000;">"</span><span style="color: #800000;">123</span><span style="color: #800000;">"</span> }, qty: <span style="color: #800080;">15</span>, tags: [ <span style="color: #800000;">"</span><span style="color: #800000;">A</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">B</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">C</span><span style="color: #800000;">"</span><span style="color: #000000;"> ] },
{ _id: </span><span style="color: #800080;">2</span>, item: { name: <span style="color: #800000;">"</span><span style="color: #800000;">cd</span><span style="color: #800000;">"</span>, code: <span style="color: #800000;">"</span><span style="color: #800000;">123</span><span style="color: #800000;">"</span> }, qty: <span style="color: #800080;">20</span>, tags: [ <span style="color: #800000;">"</span><span style="color: #800000;">B</span><span style="color: #800000;">"</span><span style="color: #000000;"> ] },
{ _id: </span><span style="color: #800080;">3</span>, item: { name: <span style="color: #800000;">"</span><span style="color: #800000;">ij</span><span style="color: #800000;">"</span>, code: <span style="color: #800000;">"</span><span style="color: #800000;">456</span><span style="color: #800000;">"</span> }, qty: <span style="color: #800080;">25</span>, tags: [ <span style="color: #800000;">"</span><span style="color: #800000;">A</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">B</span><span style="color: #800000;">"</span><span style="color: #000000;"> ] },
{ _id: </span><span style="color: #800080;">4</span>, item: { name: <span style="color: #800000;">"</span><span style="color: #800000;">xy</span><span style="color: #800000;">"</span>, code: <span style="color: #800000;">"</span><span style="color: #800000;">456</span><span style="color: #800000;">"</span> }, qty: <span style="color: #800080;">30</span>, tags: [ <span style="color: #800000;">"</span><span style="color: #800000;">B</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">A</span><span style="color: #800000;">"</span><span style="color: #000000;"> ] },
{ _id: </span><span style="color: #800080;">5</span>, item: { name: <span style="color: #800000;">"</span><span style="color: #800000;">mn</span><span style="color: #800000;">"</span>, code: <span style="color: #800000;">"</span><span style="color: #800000;">000</span><span style="color: #800000;">"</span> }, qty: <span style="color: #800080;">20</span>, tags: [ [ <span style="color: #800000;">"</span><span style="color: #800000;">A</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">B</span><span style="color: #800000;">"</span> ], <span style="color: #800000;">"</span><span style="color: #800000;">C</span><span style="color: #800000;">"</span> ] }])</pre>
</div>
<p>2，案例</p>
<p>①查询qty&gt;=20的数据</p>
<div class="cnblogs_code">
<pre>db.inventory.find({<span style="color: #800000;">"</span><span style="color: #800000;">qty</span><span style="color: #800000;">"</span>:{$gte:<span style="color: #800080;">20</span>}})</pre>
</div>
<p>②查询item对象中的name为ab的数据</p>
<div class="cnblogs_code">
<pre>db.inventory.find({<span style="color: #800000;">"</span><span style="color: #800000;">item.name</span><span style="color: #800000;">"</span>:{$eq:<span style="color: #800000;">"</span><span style="color: #800000;">ab</span><span style="color: #800000;">"</span>}})</pre>
</div>
<div class="cnblogs_code">
<pre>db.inventory.find({<span style="color: #800000;">"</span><span style="color: #800000;">item.name</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">ab</span><span style="color: #800000;">"</span>})</pre>
</div>
<p>③查询tags集合中包含C的数据</p>
<div class="cnblogs_code">
<pre>db.inventory.find({tags:{$<span style="color: #0000ff;">in</span>:[<span style="color: #800000;">"</span><span style="color: #800000;">C</span><span style="color: #800000;">"</span>]}})</pre>
</div>
<p>④查询出tags集合为[ [ "A", "B" ], "C" ]的数据</p>
<div class="cnblogs_code">
<pre>db.inventory.find({tags:{$eq:[[<span style="color: #800000;">"</span><span style="color: #800000;">A</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">B</span><span style="color: #800000;">"</span>],<span style="color: #800000;">"</span><span style="color: #800000;">C</span><span style="color: #800000;">"</span>]}})</pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a6"></a>六、逻辑运算符</span></strong></p>
<p>1，$and</p>
<p>①使用方法：&nbsp;<span class="cnblogs_code">{ $and: [ { &lt;expression1&gt; }, { &lt;expression2&gt; } , ... , {&lt;expressionN&gt; } ] }</span>&nbsp;</p>
<p>②案例</p>
<div class="cnblogs_code">
<pre>db.inventory.find( { $and: [ { price: { $ne: <span style="color: #800080;">1.99</span> } }, { price: { $exists: <span style="color: #0000ff;">true</span> } } ] } )</pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.inventory.find( {
    $and : [
        { $or : [ { price : </span><span style="color: #800080;">0.99</span> }, { price : <span style="color: #800080;">1.99</span><span style="color: #000000;"> } ] },
        { $or : [ { sale : </span><span style="color: #0000ff;">true</span> }, { qty : { $lt : <span style="color: #800080;">20</span><span style="color: #000000;"> } } ] }
    ]
} )</span></pre>
</div>
<p>2，$not</p>
<p>①使用方法：&nbsp;&nbsp;<span class="cnblogs_code">{ field: { $not: { &lt;<span style="color: #0000ff;">operator</span>-expression&gt; } } }</span>&nbsp;</p>
<p>②案例</p>
<div class="cnblogs_code">
<pre>db.inventory.find( { price: { $not: { $gt: <span style="color: #800080;">1.99</span> } } } )</pre>
</div>
<div class="cnblogs_code">
<pre>db.inventory.find( { item: { $not: /^p.*/ } } )</pre>
</div>
<p>3，$nor（or的反向）</p>
<p>①使用方法：&nbsp;<span class="cnblogs_code">{ $nor: [ { &lt;expression1&gt; }, { &lt;expression2&gt; }, ... { &lt;expressionN&gt; } ] }</span>&nbsp;</p>
<p>②案例</p>
<div class="cnblogs_code">
<pre>db.inventory.find( { $nor: [ { price: <span style="color: #800080;">1.99</span> }, { sale: <span style="color: #0000ff;">true</span> } ]  } )</pre>
</div>
<div class="cnblogs_code">
<pre>db.inventory.find( { $nor: [ { price: <span style="color: #800080;">1.99</span> }, { qty: { $lt: <span style="color: #800080;">20</span> } }, { sale: <span style="color: #0000ff;">true</span> } ] } )</pre>
</div>
<p>4，$or</p>
<p>①使用方法：&nbsp;<span class="cnblogs_code">{ $or: [ { &lt;expression1&gt; }, { &lt;expression2&gt; }, ... , { &lt;expressionN&gt; } ] }</span>&nbsp;</p>
<p>②案例</p>
<div class="cnblogs_code">
<pre>db.inventory.find( { $or: [ { quantity: { $lt: <span style="color: #800080;">20</span> } }, { price: <span style="color: #800080;">10</span> } ] } )</pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a7"></a>七、元素查询运算符</span></strong></span></p>
<p>1，$exists（判断存不存在字段）</p>
<p>①使用方法：&nbsp;<span class="cnblogs_code">{ field: { $exists: &lt;boolean&gt; } }</span>&nbsp;</p>
<p>②案例</p>
<div class="cnblogs_code">
<pre>db.inventory.find( { qty: { $exists: <span style="color: #0000ff;">true</span>, $nin: [ <span style="color: #800080;">5</span>, <span style="color: #800080;">15</span> ] } } )</pre>
</div>
<p>2，$type</p>
<p>①使用方法：&nbsp;<span class="cnblogs_code">{ field: { $type: &lt;BSON type&gt; } }</span>&nbsp;</p>
<p>②案例</p>
<div class="cnblogs_code">
<pre>db.addressBook.find( { <span style="color: #800000;">"</span><span style="color: #800000;">zipCode</span><span style="color: #800000;">"</span> : { $type : <span style="color: #800000;">"</span><span style="color: #800000;">number</span><span style="color: #800000;">"</span> } } )</pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a8"></a>八、评估查询运算符</span></strong></span></p>
<p>1，$expr【允许在查询语言中使用聚合表达式。】</p>
<p>①使用方法：&nbsp;<span class="cnblogs_code">{ $expr: { &lt;expression&gt; } }</span>&nbsp;</p>
<p>②案例</p>
<p>1）查询花费大于预算</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('10f740f6-d4b4-42d7-b96a-7aaaf0cc6a36')"><img id="code_img_closed_10f740f6-d4b4-42d7-b96a-7aaaf0cc6a36" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_10f740f6-d4b4-42d7-b96a-7aaaf0cc6a36" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('10f740f6-d4b4-42d7-b96a-7aaaf0cc6a36',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_10f740f6-d4b4-42d7-b96a-7aaaf0cc6a36" class="cnblogs_code_hide">
<pre>{ <span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">1</span>, <span style="color: #800000;">"</span><span style="color: #800000;">category</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">food</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">budget</span><span style="color: #800000;">"</span>: <span style="color: #800080;">400</span>, <span style="color: #800000;">"</span><span style="color: #800000;">spent</span><span style="color: #800000;">"</span>: <span style="color: #800080;">450</span><span style="color: #000000;"> }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">2</span>, <span style="color: #800000;">"</span><span style="color: #800000;">category</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">drinks</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">budget</span><span style="color: #800000;">"</span>: <span style="color: #800080;">100</span>, <span style="color: #800000;">"</span><span style="color: #800000;">spent</span><span style="color: #800000;">"</span>: <span style="color: #800080;">150</span><span style="color: #000000;"> }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">3</span>, <span style="color: #800000;">"</span><span style="color: #800000;">category</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">clothes</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">budget</span><span style="color: #800000;">"</span>: <span style="color: #800080;">100</span>, <span style="color: #800000;">"</span><span style="color: #800000;">spent</span><span style="color: #800000;">"</span>: <span style="color: #800080;">50</span><span style="color: #000000;"> }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">4</span>, <span style="color: #800000;">"</span><span style="color: #800000;">category</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">misc</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">budget</span><span style="color: #800000;">"</span>: <span style="color: #800080;">500</span>, <span style="color: #800000;">"</span><span style="color: #800000;">spent</span><span style="color: #800000;">"</span>: <span style="color: #800080;">300</span><span style="color: #000000;"> }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">5</span>, <span style="color: #800000;">"</span><span style="color: #800000;">category</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">travel</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">budget</span><span style="color: #800000;">"</span>: <span style="color: #800080;">200</span>, <span style="color: #800000;">"</span><span style="color: #800000;">spent</span><span style="color: #800000;">"</span>: <span style="color: #800080;">650</span> }</pre>
</div>
<span class="cnblogs_code_collapse">数据</span></div>
<div class="cnblogs_code">
<pre>db.monthlyBudget.find({$expr:{$gt:[ <span style="color: #800000;">"</span><span style="color: #800000;">$spent</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">$budget</span><span style="color: #800000;">"</span> ]}})</pre>
</div>
<p>2）qty&gt;=100的情况(price/2)&lt;5；qty&lt;100的情况(price/4)&lt;5</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('3dd0666d-a05e-45b9-81f1-b4fb2c955bdc')"><img id="code_img_closed_3dd0666d-a05e-45b9-81f1-b4fb2c955bdc" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_3dd0666d-a05e-45b9-81f1-b4fb2c955bdc" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('3dd0666d-a05e-45b9-81f1-b4fb2c955bdc',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_3dd0666d-a05e-45b9-81f1-b4fb2c955bdc" class="cnblogs_code_hide">
<pre>{ <span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">1</span>, <span style="color: #800000;">"</span><span style="color: #800000;">item</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">binder</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">qty</span><span style="color: #800000;">"</span>: <span style="color: #800080;">100</span> , <span style="color: #800000;">"</span><span style="color: #800000;">price</span><span style="color: #800000;">"</span>: <span style="color: #800080;">12</span><span style="color: #000000;"> }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">2</span>, <span style="color: #800000;">"</span><span style="color: #800000;">item</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">notebook</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">qty</span><span style="color: #800000;">"</span>: <span style="color: #800080;">200</span> , <span style="color: #800000;">"</span><span style="color: #800000;">price</span><span style="color: #800000;">"</span>: <span style="color: #800080;">8</span><span style="color: #000000;"> }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">3</span>, <span style="color: #800000;">"</span><span style="color: #800000;">item</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">pencil</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">qty</span><span style="color: #800000;">"</span>: <span style="color: #800080;">50</span> , <span style="color: #800000;">"</span><span style="color: #800000;">price</span><span style="color: #800000;">"</span>: <span style="color: #800080;">6</span><span style="color: #000000;"> }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">4</span>, <span style="color: #800000;">"</span><span style="color: #800000;">item</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">eraser</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">qty</span><span style="color: #800000;">"</span>: <span style="color: #800080;">150</span> , <span style="color: #800000;">"</span><span style="color: #800000;">price</span><span style="color: #800000;">"</span>: <span style="color: #800080;">3</span> }</pre>
</div>
<span class="cnblogs_code_collapse">supplies数据</span></div>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.supplies.find( {
    $expr: {
       $lt:[ {
          $cond: {
             </span><span style="color: #0000ff;">if</span>: { $gte: [<span style="color: #800000;">"</span><span style="color: #800000;">$qty</span><span style="color: #800000;">"</span>, <span style="color: #800080;">100</span><span style="color: #000000;">] },
             then: { $divide: [</span><span style="color: #800000;">"</span><span style="color: #800000;">$price</span><span style="color: #800000;">"</span>, <span style="color: #800080;">2</span><span style="color: #000000;">] },
             </span><span style="color: #0000ff;">else</span>: { $divide: [<span style="color: #800000;">"</span><span style="color: #800000;">$price</span><span style="color: #800000;">"</span>, <span style="color: #800080;">4</span><span style="color: #000000;">] }
           }
       },
       </span><span style="color: #800080;">5</span><span style="color: #000000;"> ] }
} )</span></pre>
</div>
<p>2，$jsonSchema【根据给定的JSON模式验证文档】</p>
<p>①使用方法：&nbsp;<span class="cnblogs_code">{ $jsonSchema: &lt;schema&gt; }</span>&nbsp;</p>
<p>参照文档：<a href="https://docs.mongodb.com/manual/reference/operator/query/jsonSchema/#op._S_jsonSchema" target="_blank">https://docs.mongodb.com/manual/reference/operator/query/jsonSchema/#op._S_jsonSchema</a></p>
<p>3，$mod【取模运算】</p>
<p>①使用方法：&nbsp;<span class="cnblogs_code">{ field: { $mod: [ 除数, 余] } }</span>&nbsp;</p>
<p>②案例</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('d59ff8f1-937a-4d81-b529-dabe479f5c9a')"><img id="code_img_closed_d59ff8f1-937a-4d81-b529-dabe479f5c9a" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_d59ff8f1-937a-4d81-b529-dabe479f5c9a" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('d59ff8f1-937a-4d81-b529-dabe479f5c9a',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_d59ff8f1-937a-4d81-b529-dabe479f5c9a" class="cnblogs_code_hide">
<pre>{ <span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">1</span>, <span style="color: #800000;">"</span><span style="color: #800000;">item</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">abc123</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">qty</span><span style="color: #800000;">"</span> : <span style="color: #800080;">0</span><span style="color: #000000;"> }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">2</span>, <span style="color: #800000;">"</span><span style="color: #800000;">item</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">xyz123</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">qty</span><span style="color: #800000;">"</span> : <span style="color: #800080;">5</span><span style="color: #000000;"> }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">3</span>, <span style="color: #800000;">"</span><span style="color: #800000;">item</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">ijk123</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">qty</span><span style="color: #800000;">"</span> : <span style="color: #800080;">12</span> }</pre>
</div>
<span class="cnblogs_code_collapse">inventory数据</span></div>
<p>捞出qty除4余0的数据</p>
<div class="cnblogs_code">
<pre>db.inventory.find( { qty: { $mod: [ <span style="color: #800080;">4</span>, <span style="color: #800080;">0</span> ] } } )</pre>
</div>
<p>3，$regex【选择值与指定正则表达式匹配的文档】</p>
<p>①使用方法：&nbsp;<span class="cnblogs_code">{ &lt;field&gt;: /pattern/&lt;options&gt; }</span>&nbsp;</p>
<div class="cnblogs_code">
<pre>{ &lt;field&gt;: { $regex: /pattern/, $options: <span style="color: #800000;">'</span><span style="color: #800000;">&lt;options&gt;</span><span style="color: #800000;">'</span><span style="color: #000000;"> } }
{ </span>&lt;field&gt;: { $regex: <span style="color: #800000;">'</span><span style="color: #800000;">pattern</span><span style="color: #800000;">'</span>, $options: <span style="color: #800000;">'</span><span style="color: #800000;">&lt;options&gt;</span><span style="color: #800000;">'</span><span style="color: #000000;"> } }
{ </span>&lt;field&gt;: { $regex: /pattern/&lt;options&gt; } }</pre>
</div>
<table class="colwidths-given docutils" border="1">
<thead valign="bottom">
<tr class="row-odd"><th class="head">Option</th><th class="head">描述</th><th class="head">语法限制</th></tr>
</thead>
<tbody valign="top">
<tr class="row-even">
<td><code class="docutils literal">i</code></td>
<td>不区分大小写</td>
<td>&nbsp;</td>
</tr>
<tr class="row-odd">
<td><code class="docutils literal">m</code></td>
<td>
<p>对于包含锚的模式（即起始为^，结束为$），在每行的开始或结束处匹配具有多行值的字符串。 没有这个选项，这些锚点匹配字符串的开头或结尾。 有关示例，请参阅多行匹配以指定模式开始的行。<br />如果模式不包含锚，或者字符串值没有换行符（例如\ n），则m选项不起作用。</p>





























































</td>
<td>&nbsp;</td>





























































</tr>
<tr class="row-even">
<td><code class="docutils literal">x</code></td>
<td>
<p class="first">忽略$regex模式中的所有空格字符，除非转义或包含在字符类中</p>





























































</td>
<td>需要使用$ options语法的$ regex</td>





























































</tr>
<tr class="row-odd">
<td><code class="docutils literal">s</code></td>
<td>允许点字符匹配包括换行符的所有字符</td>
<td>需要使用$ options语法的$ regex</td>





























































</tr>





























































</tbody>





























































</table>
<p>②案例</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('cf49ba34-e5be-42f2-b8b2-db67f4dd71d4')"><img id="code_img_closed_cf49ba34-e5be-42f2-b8b2-db67f4dd71d4" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_cf49ba34-e5be-42f2-b8b2-db67f4dd71d4" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('cf49ba34-e5be-42f2-b8b2-db67f4dd71d4',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_cf49ba34-e5be-42f2-b8b2-db67f4dd71d4" class="cnblogs_code_hide">
<pre>{ <span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">100</span>, <span style="color: #800000;">"</span><span style="color: #800000;">sku</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">abc123</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">description</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">Single line description.</span><span style="color: #800000;">"</span><span style="color: #000000;"> }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">101</span>, <span style="color: #800000;">"</span><span style="color: #800000;">sku</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">abc789</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">description</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">First line\nSecond line</span><span style="color: #800000;">"</span><span style="color: #000000;"> }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">102</span>, <span style="color: #800000;">"</span><span style="color: #800000;">sku</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">xyz456</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">description</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">Many spaces before     line</span><span style="color: #800000;">"</span><span style="color: #000000;"> }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">103</span>, <span style="color: #800000;">"</span><span style="color: #800000;">sku</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">xyz789</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">description</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">Multiple\nline description</span><span style="color: #800000;">"</span> }</pre>
</div>
<span class="cnblogs_code_collapse">products数据</span></div>
<p>查询sku789结尾的数据（忽略大小写）</p>
<div class="cnblogs_code">
<pre>db.products.find( { sku: { $regex: /<span style="color: #800080;">789</span>$/ } } )</pre>
</div>
<div class="cnblogs_code">
<pre>db.products.find( { sku:/<span style="color: #800080;">789</span>$/i } )</pre>
</div>
<p>4，$text【全文搜索。不支持中文】</p>
<p>①使用方法：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">{
  $text:
    {
      $search: </span>&lt;<span style="color: #0000ff;">string</span>&gt;<span style="color: #000000;">,
      $language: </span>&lt;<span style="color: #0000ff;">string</span>&gt;<span style="color: #000000;">,
      $caseSensitive: </span>&lt;boolean&gt;<span style="color: #000000;">,
      $diacriticSensitive: </span>&lt;boolean&gt;<span style="color: #000000;">
    }
}</span></pre>
</div>
<p>参考文档：<a href="https://docs.mongodb.com/manual/reference/operator/query/text/#op._S_text" target="_blank">https://docs.mongodb.com/manual/reference/operator/query/text/#op._S_text</a></p>
<p>5，$where【匹配满足JavaScript表达式的文档】</p>
<p>①案例</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('e25d0567-c711-4623-a57c-aa3bdeb673b2')"><img id="code_img_closed_e25d0567-c711-4623-a57c-aa3bdeb673b2" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_e25d0567-c711-4623-a57c-aa3bdeb673b2" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('e25d0567-c711-4623-a57c-aa3bdeb673b2',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_e25d0567-c711-4623-a57c-aa3bdeb673b2" class="cnblogs_code_hide">
<pre><span style="color: #000000;">{
   _id: </span><span style="color: #800080;">12378</span><span style="color: #000000;">,
   name: </span><span style="color: #800000;">"</span><span style="color: #800000;">Steve</span><span style="color: #800000;">"</span><span style="color: #000000;">,
   username: </span><span style="color: #800000;">"</span><span style="color: #800000;">steveisawesome</span><span style="color: #800000;">"</span><span style="color: #000000;">,
   first_login: </span><span style="color: #800000;">"</span><span style="color: #800000;">2017-01-01</span><span style="color: #800000;">"</span><span style="color: #000000;">
}
{
   _id: </span><span style="color: #800080;">2</span><span style="color: #000000;">,
   name: </span><span style="color: #800000;">"</span><span style="color: #800000;">Anya</span><span style="color: #800000;">"</span><span style="color: #000000;">,
   username: </span><span style="color: #800000;">"</span><span style="color: #800000;">anya</span><span style="color: #800000;">"</span><span style="color: #000000;">,
   first_login: </span><span style="color: #800000;">"</span><span style="color: #800000;">2001-02-02</span><span style="color: #800000;">"</span><span style="color: #000000;">
}</span></pre>
</div>
<span class="cnblogs_code_collapse">users数据</span></div>
<div class="cnblogs_code">
<pre>db.foo.find( { $<span style="color: #0000ff;">where</span><span style="color: #000000;">: function() {
   </span><span style="color: #0000ff;">return</span> (hex_md5(<span style="color: #0000ff;">this</span>.name) == <span style="color: #800000;">"</span><span style="color: #800000;">9b53e667f30cd329dca1ec9e6a83e994</span><span style="color: #800000;">"</span><span style="color: #000000;">)
} } );</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a9"></a>九、数组查询操作符</span></strong></span></p>
<p>1，$all【匹配包含查询中指定的所有元素的数组】</p>
<p>①使用方法：&nbsp;<span class="cnblogs_code">{ &lt;field&gt;: { $all: [ &lt;value1&gt; , &lt;value2&gt; ... ] } }</span>&nbsp;</p>
<p>②案例</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('181b882a-a364-4de3-ae12-66d5732c88ed')"><img id="code_img_closed_181b882a-a364-4de3-ae12-66d5732c88ed" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_181b882a-a364-4de3-ae12-66d5732c88ed" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('181b882a-a364-4de3-ae12-66d5732c88ed',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_181b882a-a364-4de3-ae12-66d5732c88ed" class="cnblogs_code_hide">
<pre><span style="color: #000000;">{
   _id: ObjectId(</span><span style="color: #800000;">"</span><span style="color: #800000;">5234cc89687ea597eabee675</span><span style="color: #800000;">"</span><span style="color: #000000;">),
   code: </span><span style="color: #800000;">"</span><span style="color: #800000;">xyz</span><span style="color: #800000;">"</span><span style="color: #000000;">,
   tags: [ </span><span style="color: #800000;">"</span><span style="color: #800000;">school</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">book</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">bag</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">headphone</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">appliance</span><span style="color: #800000;">"</span><span style="color: #000000;"> ],
   qty: [
          { size: </span><span style="color: #800000;">"</span><span style="color: #800000;">S</span><span style="color: #800000;">"</span>, num: <span style="color: #800080;">10</span>, color: <span style="color: #800000;">"</span><span style="color: #800000;">blue</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
          { size: </span><span style="color: #800000;">"</span><span style="color: #800000;">M</span><span style="color: #800000;">"</span>, num: <span style="color: #800080;">45</span>, color: <span style="color: #800000;">"</span><span style="color: #800000;">blue</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
          { size: </span><span style="color: #800000;">"</span><span style="color: #800000;">L</span><span style="color: #800000;">"</span>, num: <span style="color: #800080;">100</span>, color: <span style="color: #800000;">"</span><span style="color: #800000;">green</span><span style="color: #800000;">"</span><span style="color: #000000;"> }
        ]
}

{
   _id: ObjectId(</span><span style="color: #800000;">"</span><span style="color: #800000;">5234cc8a687ea597eabee676</span><span style="color: #800000;">"</span><span style="color: #000000;">),
   code: </span><span style="color: #800000;">"</span><span style="color: #800000;">abc</span><span style="color: #800000;">"</span><span style="color: #000000;">,
   tags: [ </span><span style="color: #800000;">"</span><span style="color: #800000;">appliance</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">school</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">book</span><span style="color: #800000;">"</span><span style="color: #000000;"> ],
   qty: [
          { size: </span><span style="color: #800000;">"</span><span style="color: #800000;">6</span><span style="color: #800000;">"</span>, num: <span style="color: #800080;">100</span>, color: <span style="color: #800000;">"</span><span style="color: #800000;">green</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
          { size: </span><span style="color: #800000;">"</span><span style="color: #800000;">6</span><span style="color: #800000;">"</span>, num: <span style="color: #800080;">50</span>, color: <span style="color: #800000;">"</span><span style="color: #800000;">blue</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
          { size: </span><span style="color: #800000;">"</span><span style="color: #800000;">8</span><span style="color: #800000;">"</span>, num: <span style="color: #800080;">100</span>, color: <span style="color: #800000;">"</span><span style="color: #800000;">brown</span><span style="color: #800000;">"</span><span style="color: #000000;"> }
        ]
}

{
   _id: ObjectId(</span><span style="color: #800000;">"</span><span style="color: #800000;">5234ccb7687ea597eabee677</span><span style="color: #800000;">"</span><span style="color: #000000;">),
   code: </span><span style="color: #800000;">"</span><span style="color: #800000;">efg</span><span style="color: #800000;">"</span><span style="color: #000000;">,
   tags: [ </span><span style="color: #800000;">"</span><span style="color: #800000;">school</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">book</span><span style="color: #800000;">"</span><span style="color: #000000;"> ],
   qty: [
          { size: </span><span style="color: #800000;">"</span><span style="color: #800000;">S</span><span style="color: #800000;">"</span>, num: <span style="color: #800080;">10</span>, color: <span style="color: #800000;">"</span><span style="color: #800000;">blue</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
          { size: </span><span style="color: #800000;">"</span><span style="color: #800000;">M</span><span style="color: #800000;">"</span>, num: <span style="color: #800080;">100</span>, color: <span style="color: #800000;">"</span><span style="color: #800000;">blue</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
          { size: </span><span style="color: #800000;">"</span><span style="color: #800000;">L</span><span style="color: #800000;">"</span>, num: <span style="color: #800080;">100</span>, color: <span style="color: #800000;">"</span><span style="color: #800000;">green</span><span style="color: #800000;">"</span><span style="color: #000000;"> }
        ]
}

{
   _id: ObjectId(</span><span style="color: #800000;">"</span><span style="color: #800000;">52350353b2eff1353b349de9</span><span style="color: #800000;">"</span><span style="color: #000000;">),
   code: </span><span style="color: #800000;">"</span><span style="color: #800000;">ijk</span><span style="color: #800000;">"</span><span style="color: #000000;">,
   tags: [ </span><span style="color: #800000;">"</span><span style="color: #800000;">electronics</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">school</span><span style="color: #800000;">"</span><span style="color: #000000;"> ],
   qty: [
          { size: </span><span style="color: #800000;">"</span><span style="color: #800000;">M</span><span style="color: #800000;">"</span>, num: <span style="color: #800080;">100</span>, color: <span style="color: #800000;">"</span><span style="color: #800000;">green</span><span style="color: #800000;">"</span><span style="color: #000000;"> }
        ]
}</span></pre>
</div>
<span class="cnblogs_code_collapse">inventory数据</span></div>
<p>集合中包含<span class="s2">"appliance"<span class="p">, <span class="s2">"school"<span class="p">, <span class="s2">"book" 的文档</span></span></span></span></span></p>
<div class="cnblogs_code">
<pre>db.inventory.find( { tags: { $all: [ <span style="color: #800000;">"</span><span style="color: #800000;">appliance</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">school</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">book</span><span style="color: #800000;">"</span> ] } } )</pre>
</div>
<p>&nbsp;</p>
<p>2，$elemMatch【如果数组中的元素匹配所有指定的$ elemMatch条件，则选择文档】</p>
<p>①使用方法：&nbsp;<span class="cnblogs_code">{ &lt;field&gt;: { $elemMatch: { &lt;query1&gt;, &lt;query2&gt;, ... } } }</span>&nbsp;</p>
<p>②案例</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('f31ac40c-0689-4525-aa08-04ad3e62a6db')"><img id="code_img_closed_f31ac40c-0689-4525-aa08-04ad3e62a6db" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_f31ac40c-0689-4525-aa08-04ad3e62a6db" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('f31ac40c-0689-4525-aa08-04ad3e62a6db',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_f31ac40c-0689-4525-aa08-04ad3e62a6db" class="cnblogs_code_hide">
<pre>{ _id: <span style="color: #800080;">1</span>, results: [ { product: <span style="color: #800000;">"</span><span style="color: #800000;">abc</span><span style="color: #800000;">"</span>, score: <span style="color: #800080;">10</span> }, { product: <span style="color: #800000;">"</span><span style="color: #800000;">xyz</span><span style="color: #800000;">"</span>, score: <span style="color: #800080;">5</span><span style="color: #000000;"> } ] }
{ _id: </span><span style="color: #800080;">2</span>, results: [ { product: <span style="color: #800000;">"</span><span style="color: #800000;">abc</span><span style="color: #800000;">"</span>, score: <span style="color: #800080;">8</span> }, { product: <span style="color: #800000;">"</span><span style="color: #800000;">xyz</span><span style="color: #800000;">"</span>, score: <span style="color: #800080;">7</span><span style="color: #000000;"> } ] }
{ _id: </span><span style="color: #800080;">3</span>, results: [ { product: <span style="color: #800000;">"</span><span style="color: #800000;">abc</span><span style="color: #800000;">"</span>, score: <span style="color: #800080;">7</span> }, { product: <span style="color: #800000;">"</span><span style="color: #800000;">xyz</span><span style="color: #800000;">"</span>, score: <span style="color: #800080;">8</span> } ] }</pre>
</div>
<span class="cnblogs_code_collapse">survey数据</span></div>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.survey.find(
   { results: { $elemMatch: { product: </span><span style="color: #800000;">"</span><span style="color: #800000;">xyz</span><span style="color: #800000;">"</span>, score: { $gte: <span style="color: #800080;">8</span><span style="color: #000000;"> } } } }
)</span></pre>
</div>
<p>&nbsp;</p>
<p>3，$size【如果数组字段是指定的大小，则选择文档。】</p>
<div class="cnblogs_code">
<pre>db.collection.find( { field: { $size: <span style="color: #800080;">2</span> } } );</pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a10"></a>十、更新操作结构</span></strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.collection.update(
   </span>&lt;query&gt;<span style="color: #000000;">,
   </span>&lt;update&gt;<span style="color: #000000;">,
   {
     upsert: </span>&lt;boolean&gt;<span style="color: #000000;">,
     multi: </span>&lt;boolean&gt;<span style="color: #000000;">,
     writeConcern: </span>&lt;document&gt;<span style="color: #000000;">,
     collation: </span>&lt;document&gt;<span style="color: #000000;">,
     arrayFilters: [ </span>&lt;filterdocument1&gt;<span style="color: #000000;">, ... ]
   }
)</span></pre>
</div>
<table class="colwidths-given docutils" border="1">
<thead valign="bottom">
<tr class="row-odd"><th class="head">Parameter</th><th class="head">Type</th><th class="head">Description</th></tr>
</thead>
<tbody valign="top">
<tr class="row-even">
<td><code class="docutils literal">query</code></td>
<td>document</td>
<td>
<p class="first"><span style="font-size: 10px;">更新筛选条件</span></p>
</td>
</tr>
<tr class="row-odd">
<td><code class="docutils literal">update</code></td>
<td>document</td>
<td>修改</td>
</tr>
<tr class="row-even">
<td><code class="docutils literal">upsert</code></td>
<td>boolean</td>
<td>可选的。 如果设置为true，则在没有文档匹配查询条件时创建一个新文档。 默认值为false，当找不到匹配项时不插入新文档。</td>
</tr>
<tr class="row-odd">
<td><code class="docutils literal">multi</code></td>
<td>boolean</td>
<td>可选的。 如果设置为true，则更新符合查询条件的多个文档。 如果设置为false，则更新一个文档。 默认值是false。 有关其他信息，请参阅多参数。</td>
</tr>
<tr class="row-even">
<td><code class="docutils literal">writeConcern</code></td>
<td>document</td>
<td>
<p class="first">可选的。 表达写入关注的文档。 省略使用默认的写入问题</p>
</td>
</tr>
<tr class="row-odd">
<td><code class="docutils literal">collation</code></td>
<td>document</td>
<td>
<p>可选的。</p>
<p>指定用于操作的排序规则。</p>
<p>整理允许用户为字符串比较指定特定于语言的规则</p>
<p>排序选项具有以下语法：</p>
<div class="highlight-javascript">
<div class="highlight">
<pre><span class="nx">collation<span class="o">: <span class="p">{
   <span class="nx">locale<span class="o">: <span class="o">&lt;<span class="nx">string<span class="o">&gt;<span class="p">,
   <span class="nx">caseLevel<span class="o">: <span class="o">&lt;<span class="kr">boolean<span class="o">&gt;<span class="p">,
   <span class="nx">caseFirst<span class="o">: <span class="o">&lt;<span class="nx">string<span class="o">&gt;<span class="p">,
   <span class="nx">strength<span class="o">: <span class="o">&lt;<span class="kr">int<span class="o">&gt;<span class="p">,
   <span class="nx">numericOrdering<span class="o">: <span class="o">&lt;<span class="kr">boolean<span class="o">&gt;<span class="p">,
   <span class="nx">alternate<span class="o">: <span class="o">&lt;<span class="nx">string<span class="o">&gt;<span class="p">,
   <span class="nx">maxVariable<span class="o">: <span class="o">&lt;<span class="nx">string<span class="o">&gt;<span class="p">,
   <span class="nx">backwards<span class="o">: <span class="o">&lt;<span class="kr">boolean<span class="o">&gt;
<span class="p">}
</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></pre>
</div>
</div>
<p>指定排序规则时，语言环境字段是强制性的; 所有其他整理字段是可选的。 有关这些字段的说明，请参阅整理文档。</p>
<p>如果排序规则未指定，但该集合具有默认排序规则（请参阅db.createCollection（）），则该操作使用为该集合指定的排序规则。</p>
<p>如果没有为集合或操作指定排序规则，则MongoDB使用先前版本中使用的简单二进制比较进行字符串比较。</p>
<p>您无法为操作指定多个归类。 例如，不能为每个字段指定不同的排序规则，或者如果使用排序来执行查找，则不能使用一个排序规则查找，另一个排序规则。</p>
</td>
</tr>
<tr class="row-even">
<td><code class="docutils literal">arrayFilters</code></td>
<td>array</td>
<td>
<p>可选的。 一组过滤器文档，用于确定要修改阵列字段上的更新操作的数组元素。</p>
<p>在更新文档中，使用$ [&lt;identifier&gt;]过滤位置运算符来定义标识符，然后在阵列过滤器文档中引用该标识符。 如果标识符未包含在更新文档中，则不能拥有标识符的数组筛选器文档。</p>
<div class="admonition note">
<p>注意</p>
<p>&lt;identifier&gt;必须以小写字母开头，并且只包含字母数字字符。</p>
<p>您可以在更新文档中多次包含相同的标识符; 但是，对于更新文档中的每个不同标识符（$ [identifier]），必须正好指定一个相应的数组过滤器文档。 也就是说，不能为同一个标识符指定多个数组过滤器文档。 例如，如果更新语句包含标识符x（可能多次），则不能为arrayFilters指定以下值：</p>
</div>
<div class="highlight-javascript">
<div class="highlight">
<pre><span class="p">[ <span class="p">{ <span class="s2">"x.a"<span class="o">: <span class="p">{ <span class="nx">$gt<span class="o">: <span class="mi">85<span class="p">} <span class="p">}, <span class="p">{ <span class="s2">"x.b"<span class="o">: <span class="p">{ <span class="nx">$gt<span class="o">: <span class="mi">80 <span class="p">} <span class="p">} <span class="p">]
</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></pre>
</div>
</div>
<p>但是，您可以在单个数组过滤器文档中的相同标识符上指定复合条件，例如：</p>
<div class="highlight-javascript">
<div class="highlight">
<pre><span class="p">[ <span class="p">{ <span class="nx">$or<span class="o">: <span class="p">[ <span class="p">{ <span class="s2">"x.a"<span class="o">: <span class="p">{ <span class="nx">$gt<span class="o">: <span class="mi">85<span class="p">} <span class="p">}, <span class="p">{ <span class="s2">"x.b"<span class="o">: <span class="p">{ <span class="nx">$gt<span class="o">: <span class="mi">80 <span class="p">} <span class="p">} <span class="p">] <span class="p">} <span class="p">]
<span class="p">[ <span class="p">{ <span class="nx">$and<span class="o">: <span class="p">[ <span class="p">{ <span class="s2">"x.a"<span class="o">: <span class="p">{ <span class="nx">$gt<span class="o">: <span class="mi">85<span class="p">} <span class="p">}, <span class="p">{ <span class="s2">"x.b"<span class="o">: <span class="p">{ <span class="nx">$gt<span class="o">: <span class="mi">80 <span class="p">} <span class="p">} <span class="p">] <span class="p">} <span class="p">]</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></pre>
</div>
</div>
</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a11"></a>十一、字段更新操作符</span></strong></span></p>
<p>1，$currentDate【将字段的值设置为当前日期，可以是日期或时间戳】</p>
<p>①使用方法：&nbsp;<span class="cnblogs_code">{ $currentDate: { &lt;field1&gt;: &lt;typeSpecification1&gt;, ... } }</span>&nbsp;</p>
<p>②案例</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('21eddaf5-f0ba-4e2c-bc4e-410bd0501ec8')"><img id="code_img_closed_21eddaf5-f0ba-4e2c-bc4e-410bd0501ec8" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_21eddaf5-f0ba-4e2c-bc4e-410bd0501ec8" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('21eddaf5-f0ba-4e2c-bc4e-410bd0501ec8',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_21eddaf5-f0ba-4e2c-bc4e-410bd0501ec8" class="cnblogs_code_hide">
<pre>{ _id: <span style="color: #800080;">1</span>, status: <span style="color: #800000;">"</span><span style="color: #800000;">a</span><span style="color: #800000;">"</span>, lastModified: ISODate(<span style="color: #800000;">"</span><span style="color: #800000;">2013-10-02T01:11:18.965Z</span><span style="color: #800000;">"</span>) }</pre>
</div>
<span class="cnblogs_code_collapse">users数据</span></div>
<div class="cnblogs_code">
<pre>db.users.update({_id:<span style="color: #800080;">2</span>},{$currentDate:{lastModified:{ $type: <span style="color: #800000;">"</span><span style="color: #800000;">date</span><span style="color: #800000;">"</span> }}})</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>2，$inc【按指定的量增加字段的值】</p>
<p>①使用方法：&nbsp;<span class="cnblogs_code">{ $inc: { &lt;field1&gt;: &lt;amount1&gt;, &lt;field2&gt;: &lt;amount2&gt;, ... } }</span>&nbsp;</p>
<p>②案例</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('6bb59f0a-bece-492a-ba96-6a9e46e99281')"><img id="code_img_closed_6bb59f0a-bece-492a-ba96-6a9e46e99281" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_6bb59f0a-bece-492a-ba96-6a9e46e99281" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('6bb59f0a-bece-492a-ba96-6a9e46e99281',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_6bb59f0a-bece-492a-ba96-6a9e46e99281" class="cnblogs_code_hide">
<pre><span style="color: #000000;">{
  _id: </span><span style="color: #800080;">1</span><span style="color: #000000;">,
  sku: </span><span style="color: #800000;">"</span><span style="color: #800000;">abc123</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  quantity: </span><span style="color: #800080;">10</span><span style="color: #000000;">,
  metrics: {
    orders: </span><span style="color: #800080;">2</span><span style="color: #000000;">,
    ratings: </span><span style="color: #800080;">3.5</span><span style="color: #000000;">
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">products数据</span></div>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.products.update(
   { sku: </span><span style="color: #800000;">"</span><span style="color: #800000;">abc123</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
   { $inc: { quantity: </span>-<span style="color: #800080;">2</span>, <span style="color: #800000;">"</span><span style="color: #800000;">metrics.orders</span><span style="color: #800000;">"</span>: <span style="color: #800080;">1</span><span style="color: #000000;"> } }
)</span></pre>
</div>
<p>&nbsp;</p>
<p>3，$min【如果指定的值小于现有字段值，则只更新字段】</p>
<p>①使用方法：&nbsp;<span class="cnblogs_code">{ $min: { &lt;field1&gt;: &lt;value1&gt;, ... } }</span>&nbsp;</p>
<p>②案例</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('86e6bff6-7162-4d4f-adc4-c94c06beea7a')"><img id="code_img_closed_86e6bff6-7162-4d4f-adc4-c94c06beea7a" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_86e6bff6-7162-4d4f-adc4-c94c06beea7a" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('86e6bff6-7162-4d4f-adc4-c94c06beea7a',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_86e6bff6-7162-4d4f-adc4-c94c06beea7a" class="cnblogs_code_hide">
<pre>{ _id: <span style="color: #800080;">1</span>, highScore: <span style="color: #800080;">800</span>, lowScore: <span style="color: #800080;">200</span> }</pre>
</div>
<span class="cnblogs_code_collapse"> scores数据</span></div>
<p>比原有lowScore的值小则更新</p>
<div class="cnblogs_code">
<pre>db.scores.update( { _id: <span style="color: #800080;">1</span> }, { $min: { lowScore: <span style="color: #800080;">150</span> } } )</pre>
</div>
<p>&nbsp;</p>
<p>4，$max【如果指定的值大于现有字段值，则只更新字段】</p>
<p>①使用方法：&nbsp;<span class="cnblogs_code">{ $max: { &lt;field1&gt;: &lt;value1&gt;, ... } }</span>&nbsp;</p>
<p>②案例</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('178b6bb5-8589-47c6-b648-80bbdba2ec34')"><img id="code_img_closed_178b6bb5-8589-47c6-b648-80bbdba2ec34" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_178b6bb5-8589-47c6-b648-80bbdba2ec34" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('178b6bb5-8589-47c6-b648-80bbdba2ec34',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_178b6bb5-8589-47c6-b648-80bbdba2ec34" class="cnblogs_code_hide">
<pre>{ _id: <span style="color: #800080;">1</span>, highScore: <span style="color: #800080;">800</span>, lowScore: <span style="color: #800080;">200</span> }</pre>
</div>
<span class="cnblogs_code_collapse"> scores数据</span></div>
<p>比原有highScore的值大则更新</p>
<div class="cnblogs_code">
<pre>db.scores.update( { _id: <span style="color: #800080;">1</span> }, { $max: { highScore: <span style="color: #800080;">950</span> } } )</pre>
</div>
<p>&nbsp;</p>
<p>5，$mul【将字段的值乘以指定的数量】</p>
<p>①使用方法：&nbsp;<span class="cnblogs_code">{ $mul: { field: &lt;number&gt; } }</span>&nbsp;</p>
<p>②案例</p>
<div class="cnblogs_code">
<pre>{ _id: <span style="color: #800080;">1</span>, item: <span style="color: #800000;">"</span><span style="color: #800000;">ABC</span><span style="color: #800000;">"</span>, price: <span style="color: #800080;">10.99</span> }</pre>
</div>
<p>price值乘1.25</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.products.update(
   { _id: </span><span style="color: #800080;">1</span><span style="color: #000000;"> },
   { $mul: { price: </span><span style="color: #800080;">1.25</span><span style="color: #000000;"> } }
)</span></pre>
</div>
<p>&nbsp;</p>
<p>6，$rename【重命名一个字段】</p>
<p>①使用方法：&nbsp;<span class="cnblogs_code">{$rename: { &lt;field1&gt;: &lt;newName1&gt;, &lt;field2&gt;: &lt;newName2&gt;, ... } }</span>&nbsp;</p>
<p>②案例</p>
<div class="cnblogs_code">
<pre>db.students.updateMany( {}, { $rename: { <span style="color: #800000;">"</span><span style="color: #800000;">nmae</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span> } } )</pre>
</div>
<div class="cnblogs_code">
<pre>db.students.update( { _id: <span style="color: #800080;">1</span> }, { $rename: { <span style="color: #800000;">"</span><span style="color: #800000;">name.first</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">name.fname</span><span style="color: #800000;">"</span> } } )</pre>
</div>
<p>&nbsp;</p>
<p>7，$set【设置文档中字段的值】</p>
<p>①使用方法：&nbsp;<span class="cnblogs_code">{ $<span style="color: #0000ff;">set</span>: { &lt;field1&gt;: &lt;value1&gt;, ... } }</span>&nbsp;</p>
<p>②案例</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('cbff47d8-e83f-4608-92a8-db50076f6d0f')"><img id="code_img_closed_cbff47d8-e83f-4608-92a8-db50076f6d0f" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_cbff47d8-e83f-4608-92a8-db50076f6d0f" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('cbff47d8-e83f-4608-92a8-db50076f6d0f',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_cbff47d8-e83f-4608-92a8-db50076f6d0f" class="cnblogs_code_hide">
<pre><span style="color: #000000;">{
  _id: </span><span style="color: #800080;">100</span><span style="color: #000000;">,
  sku: </span><span style="color: #800000;">"</span><span style="color: #800000;">abc123</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  quantity: </span><span style="color: #800080;">250</span><span style="color: #000000;">,
  instock: </span><span style="color: #0000ff;">true</span><span style="color: #000000;">,
  reorder: </span><span style="color: #0000ff;">false</span><span style="color: #000000;">,
  details: { model: </span><span style="color: #800000;">"</span><span style="color: #800000;">14Q2</span><span style="color: #800000;">"</span>, make: <span style="color: #800000;">"</span><span style="color: #800000;">xyz</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
  tags: [ </span><span style="color: #800000;">"</span><span style="color: #800000;">apparel</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">clothing</span><span style="color: #800000;">"</span><span style="color: #000000;"> ],
  ratings: [ { by: </span><span style="color: #800000;">"</span><span style="color: #800000;">ijk</span><span style="color: #800000;">"</span>, rating: <span style="color: #800080;">4</span><span style="color: #000000;"> } ]
}</span></pre>
</div>
<span class="cnblogs_code_collapse">数据</span></div>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.products.update(
   { _id: </span><span style="color: #800080;">100</span><span style="color: #000000;"> },
   { $</span><span style="color: #0000ff;">set</span><span style="color: #000000;">:
      {
        quantity: </span><span style="color: #800080;">500</span><span style="color: #000000;">,
        details: { model: </span><span style="color: #800000;">"</span><span style="color: #800000;">14Q3</span><span style="color: #800000;">"</span>, make: <span style="color: #800000;">"</span><span style="color: #800000;">xyz</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
        tags: [ </span><span style="color: #800000;">"</span><span style="color: #800000;">coats</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">outerwear</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">clothing</span><span style="color: #800000;">"</span><span style="color: #000000;"> ]
      }
   }
)</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.products.update(
   { _id: </span><span style="color: #800080;">100</span><span style="color: #000000;"> },
   { $</span><span style="color: #0000ff;">set</span>: { <span style="color: #800000;">"</span><span style="color: #800000;">details.make</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">zzz</span><span style="color: #800000;">"</span><span style="color: #000000;"> } }
)</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.products.update(
   { _id: </span><span style="color: #800080;">100</span><span style="color: #000000;"> },
   { $</span><span style="color: #0000ff;">set</span><span style="color: #000000;">:
      {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">tags.1</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">rain gear</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">ratings.0.rating</span><span style="color: #800000;">"</span>: <span style="color: #800080;">2</span><span style="color: #000000;">
      }
   }
)</span></pre>
</div>
<p>&nbsp;</p>
<p>8，$setOnInsert【如果更新导致插入文档，则设置字段的值。 对修改现有文档的更新操作没有影响】</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.products.update(
  { _id: </span><span style="color: #800080;">1</span><span style="color: #000000;"> },
  {
     $</span><span style="color: #0000ff;">set</span>: { item: <span style="color: #800000;">"</span><span style="color: #800000;">apple</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
     $setOnInsert: { defaultQty: </span><span style="color: #800080;">200</span><span style="color: #000000;"> }
  },
  { upsert: </span><span style="color: #0000ff;">true</span><span style="color: #000000;"> }
)</span></pre>
</div>
<p>upsert: true表示没有数据则插入；false表示没有数据则什么也不做<br />$setOnInsert: { defaultQty: 200 }表示只有插入时才会将defaultQty设置为 200。更新操作不会设置此值</p>
<p>&nbsp;</p>
<p>9，$unset【从文档中删除指定的字段】</p>
<p>①使用方法：&nbsp;<span class="cnblogs_code">{ $unset: { &lt;field1&gt;: <span style="color: #800000;">""</span>, ... } }</span>&nbsp;</p>
<p>②案例</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.products.update(
  { _id: </span><span style="color: #800080;">2</span><span style="color: #000000;"> },
  {$unset:{item:</span><span style="color: #800000;">""</span><span style="color: #000000;">}}
)</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a12"></a>十二、数组更新</span></strong></p>
<p>1，$ 【充当占位符来更新匹配查询条件的第一个元素】</p>
<p>①使用方法：&nbsp;<span class="cnblogs_code">{ <span style="color: #800000;">"</span><span style="color: #800000;">&lt;array&gt;.$</span><span style="color: #800000;">"</span> : value }</span>&nbsp;</p>
<p>②案例</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('33bf0a82-5758-420c-8836-69801bdcaa4f')"><img id="code_img_closed_33bf0a82-5758-420c-8836-69801bdcaa4f" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_33bf0a82-5758-420c-8836-69801bdcaa4f" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('33bf0a82-5758-420c-8836-69801bdcaa4f',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_33bf0a82-5758-420c-8836-69801bdcaa4f" class="cnblogs_code_hide">
<pre><span style="color: #000000;">db.students.insert([
   { </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">1</span>, <span style="color: #800000;">"</span><span style="color: #800000;">grades</span><span style="color: #800000;">"</span> : [ <span style="color: #800080;">85</span>, <span style="color: #800080;">80</span>, <span style="color: #800080;">80</span><span style="color: #000000;"> ] },
   { </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">2</span>, <span style="color: #800000;">"</span><span style="color: #800000;">grades</span><span style="color: #800000;">"</span> : [ <span style="color: #800080;">88</span>, <span style="color: #800080;">90</span>, <span style="color: #800080;">92</span><span style="color: #000000;"> ] },
   { </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">3</span>, <span style="color: #800000;">"</span><span style="color: #800000;">grades</span><span style="color: #800000;">"</span> : [ <span style="color: #800080;">85</span>, <span style="color: #800080;">100</span>, <span style="color: #800080;">90</span><span style="color: #000000;"> ] }
])</span></pre>
</div>
<span class="cnblogs_code_collapse">students数据</span></div>
<p>id为1的项，将第一个grades为80的项改为82</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.students.update(
   { _id: </span><span style="color: #800080;">1</span>, grades: <span style="color: #800080;">80</span><span style="color: #000000;"> },
   { $</span><span style="color: #0000ff;">set</span>: { <span style="color: #800000;">"</span><span style="color: #800000;">grades.$</span><span style="color: #800000;">"</span> : <span style="color: #800080;">82</span><span style="color: #000000;"> } }
)</span></pre>
</div>
<p>&nbsp;</p>
<p>2，$[] 【充当占位符来更新数组中与查询条件匹配的所有元素】</p>
<p>①使用方法：&nbsp;<span class="cnblogs_code">{ &lt;update <span style="color: #0000ff;">operator</span>&gt;: { <span style="color: #800000;">"</span><span style="color: #800000;">&lt;array&gt;.$[]</span><span style="color: #800000;">"</span> : value } }</span>&nbsp;</p>
<p>②案例</p>
<p>&nbsp;id为1的项，将grades所有项改为80</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.students.update(
   { _id: </span><span style="color: #800080;">1</span>, grades: <span style="color: #800080;">82</span><span style="color: #000000;"> },
   { $</span><span style="color: #0000ff;">set</span>: { <span style="color: #800000;">"</span><span style="color: #800000;">grades.$[]</span><span style="color: #800000;">"</span> : <span style="color: #800080;">80</span><span style="color: #000000;"> } }
)</span></pre>
</div>
<p>&nbsp;</p>
<p>3，$[&lt;identifier&gt;] 【充当占位符以更新与匹配查询条件的文档的arrayFilters条件匹配的所有元素】</p>
<p>①使用方法：</p>
<div class="cnblogs_code">
<pre>{ &lt;update <span style="color: #0000ff;">operator</span>&gt;: { <span style="color: #800000;">"</span><span style="color: #800000;">&lt;array&gt;.$[&lt;identifier&gt;]</span><span style="color: #800000;">"</span><span style="color: #000000;"> : value } },
{ arrayFilters: [ { </span>&lt;identifier&gt;: &lt;condition&gt; } } ] }</pre>
</div>
<p>②案例</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('282bf2e8-a64b-4540-a2f3-a25512c179c7')"><img id="code_img_closed_282bf2e8-a64b-4540-a2f3-a25512c179c7" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_282bf2e8-a64b-4540-a2f3-a25512c179c7" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('282bf2e8-a64b-4540-a2f3-a25512c179c7',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_282bf2e8-a64b-4540-a2f3-a25512c179c7" class="cnblogs_code_hide">
<pre>{ <span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">1</span>, <span style="color: #800000;">"</span><span style="color: #800000;">grades</span><span style="color: #800000;">"</span> : [ <span style="color: #800080;">95</span>, <span style="color: #800080;">92</span>, <span style="color: #800080;">90</span><span style="color: #000000;"> ] }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">2</span>, <span style="color: #800000;">"</span><span style="color: #800000;">grades</span><span style="color: #800000;">"</span> : [ <span style="color: #800080;">98</span>, <span style="color: #800080;">100</span>, <span style="color: #800080;">102</span><span style="color: #000000;"> ] }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">3</span>, <span style="color: #800000;">"</span><span style="color: #800000;">grades</span><span style="color: #800000;">"</span> : [ <span style="color: #800080;">95</span>, <span style="color: #800080;">110</span>, <span style="color: #800080;">100</span> ] }</pre>
</div>
<span class="cnblogs_code_collapse">students数据</span></div>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.students.update(
   { },
   { $</span><span style="color: #0000ff;">set</span>: { <span style="color: #800000;">"</span><span style="color: #800000;">grades.$[element]</span><span style="color: #800000;">"</span> : <span style="color: #800080;">100</span><span style="color: #000000;"> } },
   { multi: </span><span style="color: #0000ff;">true</span><span style="color: #000000;">,
     arrayFilters: [ { </span><span style="color: #800000;">"</span><span style="color: #800000;">element</span><span style="color: #800000;">"</span>: { $gte: <span style="color: #800080;">100</span><span style="color: #000000;"> } } ]
   }
)</span></pre>
</div>
<p>&nbsp;</p>
<p>4，$addToSet 【只有在数组中不存在元素的情况下，才能将元素添加到数组中】</p>
<p>①使用方法：&nbsp;<span class="cnblogs_code">{ $addToSet: { &lt;field1&gt;: &lt;value1&gt;, ... } }</span>&nbsp;</p>
<p>②案例</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('7bf70a48-4c41-4dbd-9627-1569c678ab43')"><img id="code_img_closed_7bf70a48-4c41-4dbd-9627-1569c678ab43" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_7bf70a48-4c41-4dbd-9627-1569c678ab43" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('7bf70a48-4c41-4dbd-9627-1569c678ab43',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_7bf70a48-4c41-4dbd-9627-1569c678ab43" class="cnblogs_code_hide">
<pre>{ _id: <span style="color: #800080;">1</span>, letters: [<span style="color: #800000;">"</span><span style="color: #800000;">a</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">b</span><span style="color: #800000;">"</span>] }</pre>
</div>
<span class="cnblogs_code_collapse">test数据</span></div>
<div class="cnblogs_code">
<pre>db.test.update({_id:<span style="color: #800080;">1</span>},{$addToSet:{<span style="color: #800000;">"</span><span style="color: #800000;">letters</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">e</span><span style="color: #800000;">"</span>}})</pre>
</div>
<div class="cnblogs_code">
<pre>db.test.update({_id:<span style="color: #800080;">1</span>},{$addToSet:{<span style="color: #800000;">"</span><span style="color: #800000;">letters</span><span style="color: #800000;">"</span>: {$each: [ <span style="color: #800000;">"</span><span style="color: #800000;">camera</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">electronics</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">accessories</span><span style="color: #800000;">"</span> ]}}})</pre>
</div>
<p>&nbsp;</p>
<p>5，$pop 【删除数据中的最后一个或第一个】</p>
<p>①使用方法：&nbsp;<span class="cnblogs_code">{ $pop: { &lt;field&gt;: &lt;-<span style="color: #800080;">1</span> | <span style="color: #800080;">1</span>&gt;, ... } }</span>&nbsp;</p>
<p>-1：弹出第一个；1：弹出最后一个</p>
<p>②案例</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('0ad0a839-f67e-4b67-b6ac-a0313b930f91')"><img id="code_img_closed_0ad0a839-f67e-4b67-b6ac-a0313b930f91" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_0ad0a839-f67e-4b67-b6ac-a0313b930f91" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('0ad0a839-f67e-4b67-b6ac-a0313b930f91',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_0ad0a839-f67e-4b67-b6ac-a0313b930f91" class="cnblogs_code_hide">
<pre><span style="color: #000000;">{
    </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">1</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">letters</span><span style="color: #800000;">"</span><span style="color: #000000;"> : [ 
        </span><span style="color: #800000;">"</span><span style="color: #800000;">d</span><span style="color: #800000;">"</span><span style="color: #000000;">, 
        </span><span style="color: #800000;">"</span><span style="color: #800000;">camera</span><span style="color: #800000;">"</span><span style="color: #000000;">, 
        </span><span style="color: #800000;">"</span><span style="color: #800000;">electronics</span><span style="color: #800000;">"</span><span style="color: #000000;">, 
        </span><span style="color: #800000;">"</span><span style="color: #800000;">accessories</span><span style="color: #800000;">"</span><span style="color: #000000;">
    ]
}</span></pre>
</div>
<span class="cnblogs_code_collapse">数据</span></div>
<div class="cnblogs_code">
<pre>db.test.update({_id:<span style="color: #800080;">1</span>},{$pop:{<span style="color: #800000;">"</span><span style="color: #800000;">letters</span><span style="color: #800000;">"</span>:-<span style="color: #800080;">1</span>}})</pre>
</div>
<p>&nbsp;</p>
<p>6，$pull 【删除所有匹配指定查询的数组元素】</p>
<p>①使用方法：&nbsp;<span class="cnblogs_code">{ $pull: { &lt;field1&gt;: &lt;value|condition&gt;, &lt;field2&gt;: &lt;value|condition&gt;, ... } }</span>&nbsp;</p>
<p>②案例</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('c14c1d68-a654-47d3-87c5-fc41838d3ab8')"><img id="code_img_closed_c14c1d68-a654-47d3-87c5-fc41838d3ab8" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_c14c1d68-a654-47d3-87c5-fc41838d3ab8" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('c14c1d68-a654-47d3-87c5-fc41838d3ab8',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_c14c1d68-a654-47d3-87c5-fc41838d3ab8" class="cnblogs_code_hide">
<pre><span style="color: #000000;">{
   _id: </span><span style="color: #800080;">1</span><span style="color: #000000;">,
   fruits: [ </span><span style="color: #800000;">"</span><span style="color: #800000;">apples</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">pears</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">oranges</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">grapes</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">bananas</span><span style="color: #800000;">"</span><span style="color: #000000;"> ],
   vegetables: [ </span><span style="color: #800000;">"</span><span style="color: #800000;">carrots</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">celery</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">squash</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">carrots</span><span style="color: #800000;">"</span><span style="color: #000000;"> ]
}
{
   _id: </span><span style="color: #800080;">2</span><span style="color: #000000;">,
   fruits: [ </span><span style="color: #800000;">"</span><span style="color: #800000;">plums</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">kiwis</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">oranges</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">bananas</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">apples</span><span style="color: #800000;">"</span><span style="color: #000000;"> ],
   vegetables: [ </span><span style="color: #800000;">"</span><span style="color: #800000;">broccoli</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">zucchini</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">carrots</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">onions</span><span style="color: #800000;">"</span><span style="color: #000000;"> ]
}</span></pre>
</div>
<span class="cnblogs_code_collapse">stores数据</span></div>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.stores.update(
    { },
    { $pull: { fruits: { $</span><span style="color: #0000ff;">in</span>: [ <span style="color: #800000;">"</span><span style="color: #800000;">apples</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">oranges</span><span style="color: #800000;">"</span> ] }, vegetables: <span style="color: #800000;">"</span><span style="color: #800000;">carrots</span><span style="color: #800000;">"</span><span style="color: #000000;"> } },
    { multi: </span><span style="color: #0000ff;">true</span><span style="color: #000000;"> }
)</span></pre>
</div>
<div class="cnblogs_code" onclick="cnblogs_code_show('08329282-461e-42f7-b081-3d7ccf325bc4')"><img id="code_img_closed_08329282-461e-42f7-b081-3d7ccf325bc4" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_08329282-461e-42f7-b081-3d7ccf325bc4" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('08329282-461e-42f7-b081-3d7ccf325bc4',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_08329282-461e-42f7-b081-3d7ccf325bc4" class="cnblogs_code_hide">
<pre><span style="color: #000000;">{
   _id: </span><span style="color: #800080;">1</span><span style="color: #000000;">,
   results: [
      { item: </span><span style="color: #800000;">"</span><span style="color: #800000;">A</span><span style="color: #800000;">"</span>, score: <span style="color: #800080;">5</span><span style="color: #000000;"> },
      { item: </span><span style="color: #800000;">"</span><span style="color: #800000;">B</span><span style="color: #800000;">"</span>, score: <span style="color: #800080;">8</span>, comment: <span style="color: #800000;">"</span><span style="color: #800000;">Strongly agree</span><span style="color: #800000;">"</span><span style="color: #000000;"> }
   ]
}
{
   _id: </span><span style="color: #800080;">2</span><span style="color: #000000;">,
   results: [
      { item: </span><span style="color: #800000;">"</span><span style="color: #800000;">C</span><span style="color: #800000;">"</span>, score: <span style="color: #800080;">8</span>, comment: <span style="color: #800000;">"</span><span style="color: #800000;">Strongly agree</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
      { item: </span><span style="color: #800000;">"</span><span style="color: #800000;">B</span><span style="color: #800000;">"</span>, score: <span style="color: #800080;">4</span><span style="color: #000000;"> }
   ]
}</span></pre>
</div>
<span class="cnblogs_code_collapse">survey数据</span></div>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.survey.update(
  { },
  { $pull: { results: { score: </span><span style="color: #800080;">8</span> , item: <span style="color: #800000;">"</span><span style="color: #800000;">B</span><span style="color: #800000;">"</span><span style="color: #000000;"> } } },
  { multi: </span><span style="color: #0000ff;">true</span><span style="color: #000000;"> }
)</span></pre>
</div>
<p><br />7，$push 【将一个项添加到数组中】</p>
<p>①使用方法：&nbsp;<span class="cnblogs_code">{ $push: { &lt;field1&gt;: &lt;value1&gt;, ... } }</span>&nbsp;</p>
<table class="colwidths-given docutils" border="1">
<thead valign="bottom">
<tr class="row-odd"><th class="head">Modifier</th><th class="head">Description</th></tr>




















































</thead>
<tbody valign="top">
<tr class="row-even">
<td><a class="reference internal" title="$each" href="https://docs.mongodb.com/manual/reference/operator/update/each/#up._S_each"><code class="xref mongodb mongodb-update docutils literal">$each</code></a></td>
<td>
<p class="first">将多个值附加到数组字段</p>




















































</td>




















































</tr>
<tr class="row-odd">
<td><a class="reference internal" title="$slice" href="https://docs.mongodb.com/manual/reference/operator/update/slice/#up._S_slice"><code class="xref mongodb mongodb-update docutils literal">$slice</code></a></td>
<td>限制数组元素的数量。 需要使用$ each修饰符。</td>




















































</tr>
<tr class="row-even">
<td><a class="reference internal" title="$sort" href="https://docs.mongodb.com/manual/reference/operator/update/sort/#up._S_sort"><code class="xref mongodb mongodb-update docutils literal">$sort</code></a></td>
<td>
<p class="first">排序 1：升序 -1：降序</p>




















































</td>




















































</tr>
<tr class="row-odd">
<td><a class="reference internal" title="$position" href="https://docs.mongodb.com/manual/reference/operator/update/position/#up._S_position"><code class="xref mongodb mongodb-update docutils literal">$position</code></a></td>
<td>
<p class="first">指定数组中插入新元素的位置。 需要使用$ each修饰符。 如果没有$ position修饰符，$ push会将元素附加到数组的末尾。</p>




















































</td>




















































</tr>




















































</tbody>




















































</table>
<p>②案例</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.students.update(
   { _id: </span><span style="color: #800080;">1</span><span style="color: #000000;"> },
   {
     $push: {
       quizzes: {
         $each: [ { id: </span><span style="color: #800080;">3</span>, score: <span style="color: #800080;">8</span> }, { id: <span style="color: #800080;">4</span>, score: <span style="color: #800080;">7</span> }, { id: <span style="color: #800080;">5</span>, score: <span style="color: #800080;">6</span><span style="color: #000000;"> } ],
         $sort: { score: </span><span style="color: #800080;">1</span><span style="color: #000000;"> }
       }
     }
   }
)</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.students.update(
   { _id: </span><span style="color: #800080;">2</span><span style="color: #000000;"> },
   { $push: { tests: { $each: [ </span><span style="color: #800080;">40</span>, <span style="color: #800080;">60</span> ], $sort: <span style="color: #800080;">1</span><span style="color: #000000;"> } } }
)</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.students.update(
   { _id: </span><span style="color: #800080;">6</span><span style="color: #000000;"> },
   {
     $push: {
       quizzes: {
          $each: [ { wk: </span><span style="color: #800080;">5</span>, score: <span style="color: #800080;">8</span> }, { wk: <span style="color: #800080;">6</span>, score: <span style="color: #800080;">7</span> }, { wk: <span style="color: #800080;">7</span>, score: <span style="color: #800080;">6</span><span style="color: #000000;"> } ],
          $sort: { score: </span>-<span style="color: #800080;">1</span><span style="color: #000000;"> },
          $slice: </span><span style="color: #800080;">2</span> <span style="color: #008000;">//</span><span style="color: #008000;">限制长度，多了会截取</span>
<span style="color: #000000;">       }
     }
   },
   {
       upsert:</span><span style="color: #0000ff;">true</span><span style="color: #000000;">}
)</span></pre>
</div>
<p>&nbsp;</p>
<p>8，$pullAll 【从数组中删除所有匹配的值】</p>
<p>①使用方法：&nbsp;<span class="cnblogs_code">{ $pullAll: { &lt;field1&gt;: [ &lt;value1&gt;, &lt;value2&gt; ... ], ... } }</span>&nbsp;</p>
<p>②案例</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('b163d8ac-f853-425d-ac93-40dd61d6f152')"><img id="code_img_closed_b163d8ac-f853-425d-ac93-40dd61d6f152" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_b163d8ac-f853-425d-ac93-40dd61d6f152" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('b163d8ac-f853-425d-ac93-40dd61d6f152',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_b163d8ac-f853-425d-ac93-40dd61d6f152" class="cnblogs_code_hide">
<pre>{ _id: <span style="color: #800080;">1</span>, scores: [ <span style="color: #800080;">0</span>, <span style="color: #800080;">2</span>, <span style="color: #800080;">5</span>, <span style="color: #800080;">5</span>, <span style="color: #800080;">1</span>, <span style="color: #800080;">0</span> ] }</pre>
</div>
<span class="cnblogs_code_collapse">survey数据</span></div>
<div class="cnblogs_code">
<pre>db.survey.update( { _id: <span style="color: #800080;">1</span> }, { $pullAll: { scores: [ <span style="color: #800080;">0</span>, <span style="color: #800080;">5</span> ] } } )</pre>
</div>
<p>&nbsp;</p>
<p>9，$each【修改$push和$addToSet操作符以追加多个项目进行数组更新】</p>
<p>①使用方法：</p>
<div class="cnblogs_code">
<pre>{ $addToSet: { &lt;field&gt;: { $each: [ &lt;value1&gt;, &lt;value2&gt; ... ] } } }</pre>
</div>
<div class="cnblogs_code">
<pre>{ $push: { &lt;field&gt;: { $each: [ &lt;value1&gt;, &lt;value2&gt; ... ] } } }</pre>
</div>
<p>②案例</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.students.update(
   { name: </span><span style="color: #800000;">"</span><span style="color: #800000;">joe</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
   { $push: { scores: { $each: [ </span><span style="color: #800080;">90</span>, <span style="color: #800080;">92</span>, <span style="color: #800080;">85</span><span style="color: #000000;"> ] } } }
)</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.inventory.update(
   { _id: </span><span style="color: #800080;">2</span><span style="color: #000000;"> },
   { $addToSet: { tags: { $each: [ </span><span style="color: #800000;">"</span><span style="color: #800000;">camera</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">electronics</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">accessories</span><span style="color: #800000;">"</span><span style="color: #000000;"> ] } } }
 )</span></pre>
</div>
<p>&nbsp;</p>
<p>10，$position【修改$push操作符以指定数组中的位置以添加元素】</p>
<p>①使用方法：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">{
  $push: {
    </span>&lt;field&gt;<span style="color: #000000;">: {
       $each: [ </span>&lt;value1&gt;, &lt;value2&gt;<span style="color: #000000;">, ... ],
       $position: </span>&lt;num&gt;<span style="color: #000000;">
    }
  }
}</span></pre>
</div>
<p>②案例</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('9a35567b-cf89-4854-9f4b-694cc9f71127')"><img id="code_img_closed_9a35567b-cf89-4854-9f4b-694cc9f71127" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_9a35567b-cf89-4854-9f4b-694cc9f71127" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('9a35567b-cf89-4854-9f4b-694cc9f71127',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_9a35567b-cf89-4854-9f4b-694cc9f71127" class="cnblogs_code_hide">
<pre>{ <span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">1</span>, <span style="color: #800000;">"</span><span style="color: #800000;">scores</span><span style="color: #800000;">"</span> : [ <span style="color: #800080;">100</span> ] }</pre>
</div>
<span class="cnblogs_code_collapse">students数据</span></div>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.students.update(
   { _id: </span><span style="color: #800080;">1</span><span style="color: #000000;"> },
   {
     $push: {
        scores: {
           $each: [ </span><span style="color: #800080;">50</span>, <span style="color: #800080;">60</span>, <span style="color: #800080;">70</span><span style="color: #000000;"> ],
           $position: </span><span style="color: #800080;">0</span><span style="color: #000000;">
        }
     }
   }
)</span></pre>
</div>
<div class="cnblogs_code" onclick="cnblogs_code_show('1b49e9c7-e6ad-490a-be4c-5a243cc3268d')"><img id="code_img_closed_1b49e9c7-e6ad-490a-be4c-5a243cc3268d" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_1b49e9c7-e6ad-490a-be4c-5a243cc3268d" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('1b49e9c7-e6ad-490a-be4c-5a243cc3268d',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_1b49e9c7-e6ad-490a-be4c-5a243cc3268d" class="cnblogs_code_hide">
<pre>{ <span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">1</span>, <span style="color: #800000;">"</span><span style="color: #800000;">scores</span><span style="color: #800000;">"</span> : [  <span style="color: #800080;">50</span>,  <span style="color: #800080;">60</span>,  <span style="color: #800080;">70</span>,  <span style="color: #800080;">100</span> ] }</pre>
</div>
<span class="cnblogs_code_collapse">显示结果</span></div>
<p>&nbsp;</p>
<p>11，$slice【修改$push操作符以限制更新数组的大小】</p>
<p>①使用方法：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">{
  $push: {
     </span>&lt;field&gt;<span style="color: #000000;">: {
       $each: [ </span>&lt;value1&gt;, &lt;value2&gt;<span style="color: #000000;">, ... ],
       $slice: </span>&lt;num&gt;<span style="color: #000000;">
     }
  }
}</span></pre>
</div>
<table class="colwidths-given docutils" border="1">
<thead valign="bottom">
<tr class="row-odd"><th class="head">Value</th><th class="head">Description</th></tr>
</thead>
<tbody valign="top">
<tr class="row-even">
<td>0</td>
<td>将数组更新为一个空数组（[]）</td>
</tr>
<tr class="row-odd">
<td>负数</td>
<td>保留数据最后一位，数组超出大小从左边开始截取</td>
</tr>
<tr class="row-even">
<td>正数</td>
<td>
<p class="first">保留第一位，数组超出大小从右边开始截取</p>
</td>
</tr>
</tbody>
</table>
<p>②案例</p>
<p>1）将grades数组更新空数组</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.students.update(
   { _id: </span><span style="color: #800080;">1</span><span style="color: #000000;"> },
   {
     $push: {
       grades: {
          $each: [ </span><span style="color: #800080;">1</span>,<span style="color: #800080;">2</span>,<span style="color: #800080;">4</span><span style="color: #000000;"> ],
          $sort: { score: </span>-<span style="color: #800080;">1</span><span style="color: #000000;"> },
          $slice: </span><span style="color: #800080;">0</span><span style="color: #000000;">
       }
     }
   }
)</span></pre>
</div>
<p>2）插入1，2，4 只会保留4</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.students.update(
   { _id: </span><span style="color: #800080;">1</span><span style="color: #000000;"> },
   {
     $push: {
       grades: {
          $each: [ </span><span style="color: #800080;">1</span>,<span style="color: #800080;">2</span>,<span style="color: #800080;">4</span><span style="color: #000000;"> ],
          $sort: { score: </span>-<span style="color: #800080;">1</span><span style="color: #000000;"> },
          $slice: </span>-<span style="color: #800080;">1</span><span style="color: #000000;">
       }
     }
   }
)</span></pre>
</div>
<p>3）插入1，2，4 只会保留1</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.students.update(
   { _id: </span><span style="color: #800080;">1</span><span style="color: #000000;"> },
   {
     $push: {
       grades: {
          $each: [ </span><span style="color: #800080;">1</span>,<span style="color: #800080;">2</span>,<span style="color: #800080;">4</span><span style="color: #000000;"> ],
          $sort: { score: </span>-<span style="color: #800080;">1</span><span style="color: #000000;"> },
          $slice:</span><span style="color: #800080;">1</span><span style="color: #000000;">
       }
     }
   }
)</span></pre>
</div>
<p>&nbsp;</p>
<p>12，$sort【修改$ push操作符以重新排列存储在数组中的文档】</p>
<p>①使用方法：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">{
  $push: {
     </span>&lt;field&gt;<span style="color: #000000;">: {
       $each: [ </span>&lt;value1&gt;, &lt;value2&gt;<span style="color: #000000;">, ... ],
       $sort: </span>&lt;sort specification&gt;<span style="color: #000000;">
     }
  }
}</span></pre>
</div>
<p>1指定为升序，-1指定为降序。</p>
<p>②案例</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('a6fe250e-73b2-427e-8f75-857850ca2f03')"><img id="code_img_closed_a6fe250e-73b2-427e-8f75-857850ca2f03" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_a6fe250e-73b2-427e-8f75-857850ca2f03" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('a6fe250e-73b2-427e-8f75-857850ca2f03',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_a6fe250e-73b2-427e-8f75-857850ca2f03" class="cnblogs_code_hide">
<pre><span style="color: #000000;">{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span>: <span style="color: #800080;">1</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">quizzes</span><span style="color: #800000;">"</span><span style="color: #000000;">: [
    { </span><span style="color: #800000;">"</span><span style="color: #800000;">id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">1</span>, <span style="color: #800000;">"</span><span style="color: #800000;">score</span><span style="color: #800000;">"</span> : <span style="color: #800080;">6</span><span style="color: #000000;"> },
    { </span><span style="color: #800000;">"</span><span style="color: #800000;">id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">2</span>, <span style="color: #800000;">"</span><span style="color: #800000;">score</span><span style="color: #800000;">"</span> : <span style="color: #800080;">9</span><span style="color: #000000;"> }
  ]
}</span></pre>
</div>
<span class="cnblogs_code_collapse">students数据</span></div>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.students.update(
   { _id: </span><span style="color: #800080;">1</span><span style="color: #000000;"> },
   {
     $push: {
       quizzes: {
         $each: [ { id: </span><span style="color: #800080;">3</span>, score: <span style="color: #800080;">8</span> }, { id: <span style="color: #800080;">4</span>, score: <span style="color: #800080;">7</span> }, { id: <span style="color: #800080;">5</span>, score: <span style="color: #800080;">6</span><span style="color: #000000;"> } ],
         $sort: { score: </span><span style="color: #800080;">1</span><span style="color: #000000;"> }
       }
     }
   }
)</span></pre>
</div>
<div class="cnblogs_code" onclick="cnblogs_code_show('780ea3a1-284a-4d98-802b-33a856edeb93')"><img id="code_img_closed_780ea3a1-284a-4d98-802b-33a856edeb93" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_780ea3a1-284a-4d98-802b-33a856edeb93" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('780ea3a1-284a-4d98-802b-33a856edeb93',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_780ea3a1-284a-4d98-802b-33a856edeb93" class="cnblogs_code_hide">
<pre><span style="color: #000000;">{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">1</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">quizzes</span><span style="color: #800000;">"</span><span style="color: #000000;"> : [
     { </span><span style="color: #800000;">"</span><span style="color: #800000;">id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">1</span>, <span style="color: #800000;">"</span><span style="color: #800000;">score</span><span style="color: #800000;">"</span> : <span style="color: #800080;">6</span><span style="color: #000000;"> },
     { </span><span style="color: #800000;">"</span><span style="color: #800000;">id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">5</span>, <span style="color: #800000;">"</span><span style="color: #800000;">score</span><span style="color: #800000;">"</span> : <span style="color: #800080;">6</span><span style="color: #000000;"> },
     { </span><span style="color: #800000;">"</span><span style="color: #800000;">id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">4</span>, <span style="color: #800000;">"</span><span style="color: #800000;">score</span><span style="color: #800000;">"</span> : <span style="color: #800080;">7</span><span style="color: #000000;"> },
     { </span><span style="color: #800000;">"</span><span style="color: #800000;">id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">3</span>, <span style="color: #800000;">"</span><span style="color: #800000;">score</span><span style="color: #800000;">"</span> : <span style="color: #800080;">8</span><span style="color: #000000;"> },
     { </span><span style="color: #800000;">"</span><span style="color: #800000;">id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">2</span>, <span style="color: #800000;">"</span><span style="color: #800000;">score</span><span style="color: #800000;">"</span> : <span style="color: #800080;">9</span><span style="color: #000000;"> }
  ]
}</span></pre>
</div>
<span class="cnblogs_code_collapse">结果</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('8acdf5d3-e94e-4c38-bb90-52f3daf8b0d1')"><img id="code_img_closed_8acdf5d3-e94e-4c38-bb90-52f3daf8b0d1" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_8acdf5d3-e94e-4c38-bb90-52f3daf8b0d1" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('8acdf5d3-e94e-4c38-bb90-52f3daf8b0d1',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_8acdf5d3-e94e-4c38-bb90-52f3daf8b0d1" class="cnblogs_code_hide">
<pre>{ <span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">2</span>, <span style="color: #800000;">"</span><span style="color: #800000;">tests</span><span style="color: #800000;">"</span> : [  <span style="color: #800080;">89</span>,  <span style="color: #800080;">70</span>,  <span style="color: #800080;">89</span>,  <span style="color: #800080;">50</span> ] }</pre>
</div>
<span class="cnblogs_code_collapse">students数据</span></div>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.students.update(
   { _id: </span><span style="color: #800080;">2</span><span style="color: #000000;"> },
   { $push: { tests: { $each: [ </span><span style="color: #800080;">40</span>, <span style="color: #800080;">60</span> ], $sort: <span style="color: #800080;">1</span><span style="color: #000000;"> } } }
)</span></pre>
</div>
<div class="cnblogs_code" onclick="cnblogs_code_show('45ee3c65-8ab1-4406-bb49-2d78ecd2adf2')"><img id="code_img_closed_45ee3c65-8ab1-4406-bb49-2d78ecd2adf2" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_45ee3c65-8ab1-4406-bb49-2d78ecd2adf2" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('45ee3c65-8ab1-4406-bb49-2d78ecd2adf2',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_45ee3c65-8ab1-4406-bb49-2d78ecd2adf2" class="cnblogs_code_hide">
<pre>{ <span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">2</span>, <span style="color: #800000;">"</span><span style="color: #800000;">tests</span><span style="color: #800000;">"</span> : [  <span style="color: #800080;">40</span>,  <span style="color: #800080;">50</span>,  <span style="color: #800080;">60</span>,  <span style="color: #800080;">70</span>,  <span style="color: #800080;">89</span>,  <span style="color: #800080;">89</span> ] }</pre>
</div>
<span class="cnblogs_code_collapse">结果</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('b9aadf7c-e8b3-46fb-89f8-de34690b2103')"><img id="code_img_closed_b9aadf7c-e8b3-46fb-89f8-de34690b2103" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_b9aadf7c-e8b3-46fb-89f8-de34690b2103" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('b9aadf7c-e8b3-46fb-89f8-de34690b2103',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_b9aadf7c-e8b3-46fb-89f8-de34690b2103" class="cnblogs_code_hide">
<pre>{ <span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">3</span>, <span style="color: #800000;">"</span><span style="color: #800000;">tests</span><span style="color: #800000;">"</span> : [  <span style="color: #800080;">89</span>,  <span style="color: #800080;">70</span>,  <span style="color: #800080;">100</span>,  <span style="color: #800080;">20</span> ] }</pre>
</div>
<span class="cnblogs_code_collapse">students数据</span></div>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.students.update(
   { _id: </span><span style="color: #800080;">3</span><span style="color: #000000;"> },
   { $push: { tests: { $each: [ ], $sort: </span>-<span style="color: #800080;">1</span><span style="color: #000000;"> } } }
)</span></pre>
</div>
<div class="cnblogs_code" onclick="cnblogs_code_show('2c46b1fa-a123-460d-a76f-c58743ef85be')"><img id="code_img_closed_2c46b1fa-a123-460d-a76f-c58743ef85be" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_2c46b1fa-a123-460d-a76f-c58743ef85be" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('2c46b1fa-a123-460d-a76f-c58743ef85be',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_2c46b1fa-a123-460d-a76f-c58743ef85be" class="cnblogs_code_hide">
<pre>{ <span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">3</span>, <span style="color: #800000;">"</span><span style="color: #800000;">tests</span><span style="color: #800000;">"</span> : [ <span style="color: #800080;">100</span>,  <span style="color: #800080;">89</span>,  <span style="color: #800080;">70</span>,  <span style="color: #800080;">20</span> ] }</pre>
</div>
<span class="cnblogs_code_collapse">结果</span></div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a13"></a>十三、位更新操作</span></strong></span></p>
<p>1，$bit【执行整数值的按位AND，OR和XOR更新。】</p>
<p>①使用方法：&nbsp;<span class="cnblogs_code">{ $bit: { &lt;field&gt;: { &lt;and|or|xor&gt;: &lt;<span style="color: #0000ff;">int</span>&gt; } } }</span>&nbsp;</p>
<p>②案例</p>
<div class="cnblogs_code">
<pre>{ _id: <span style="color: #800080;">1</span>, expdata: NumberInt(<span style="color: #800080;">13</span><span style="color: #000000;">) }

db.switches.update(
   { _id: </span><span style="color: #800080;">1</span><span style="color: #000000;"> },
   { $bit: { expdata: { and: NumberInt(</span><span style="color: #800080;">10</span><span style="color: #000000;">) } } }
)

</span><span style="color: #800080;">1101</span>
<span style="color: #800080;">1010</span>
----
<span style="color: #800080;">1000<br /><br /></span></pre>
<pre><span class="p">{ <span class="s2">"_id" <span class="o">: <span class="mi">1<span class="p">, <span class="s2">"expdata" <span class="o">: <span class="mi">8 <span class="p">}</span></span></span></span></span></span></span></span></span></pre>
</div>
<div class="cnblogs_code">
<pre>{ _id: <span style="color: #800080;">2</span>, expdata: NumberLong(<span style="color: #800080;">3</span><span style="color: #000000;">) }

db.switches.update(
   { _id: </span><span style="color: #800080;">2</span><span style="color: #000000;"> },
   { $bit: { expdata: { or: NumberInt(</span><span style="color: #800080;">5</span><span style="color: #000000;">) } } }
)

</span><span style="color: #800080;">0011</span>
<span style="color: #800080;">0101</span>
----
<span style="color: #800080;">0111</span><span style="color: #000000;">

{ </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">2</span>, <span style="color: #800000;">"</span><span style="color: #800000;">expdata</span><span style="color: #800000;">"</span> : NumberLong(<span style="color: #800080;">7</span>) }</pre>
</div>
<div class="cnblogs_code">
<pre>{ _id: <span style="color: #800080;">3</span>, expdata: NumberLong(<span style="color: #800080;">1</span><span style="color: #000000;">) }

db.switches.update(
   { _id: </span><span style="color: #800080;">3</span><span style="color: #000000;"> },
   { $bit: { expdata: { xor: NumberInt(</span><span style="color: #800080;">5</span><span style="color: #000000;">) } } }
)

</span><span style="color: #800080;">0001</span>
<span style="color: #800080;">0101</span>
----
<span style="color: #800080;">0100</span><span style="color: #000000;">

{ </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">3</span>, <span style="color: #800000;">"</span><span style="color: #800000;">expdata</span><span style="color: #800000;">"</span> : NumberLong(<span style="color: #800080;">4</span>) }</pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="q14"></a>十四、CURD&nbsp;</span></strong></p>
<p>1，Insert</p>
<p>1）db.collection.insertOne()【将单个文档插入到一个集合中】</p>
<p>详细文档：<a href="https://docs.mongodb.com/manual/reference/method/db.collection.insertOne/#db.collection.insertOne" target="_blank">https://docs.mongodb.com/manual/reference/method/db.collection.insertOne/#db.collection.insertOne</a></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.collection.insertOne(
   </span>&lt;document&gt;<span style="color: #000000;">,
   {
      writeConcern: </span>&lt;document&gt;<span style="color: #000000;">
   }
)</span></pre>
</div>
<p>2）db.collection.insertMany()【将多个文档插入到一个集合中】</p>
<p>详细文档：<a href="https://docs.mongodb.com/manual/reference/method/db.collection.insertMany/#db.collection.insertMany" target="_blank">https://docs.mongodb.com/manual/reference/method/db.collection.insertMany/#db.collection.insertMany</a></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.collection.insertMany(
   [ </span>&lt;document <span style="color: #800080;">1</span>&gt; , &lt;document <span style="color: #800080;">2</span>&gt;<span style="color: #000000;">, ... ],
   {
      writeConcern: </span>&lt;document&gt;<span style="color: #000000;">,
      ordered: </span>&lt;boolean&gt;<span style="color: #000000;">
   }
)</span></pre>
</div>
<p>3）db.collection.insert()【将单个文档或多个文档插入到集合中】</p>
<p>详细文档：<a href="https://docs.mongodb.com/manual/reference/method/db.collection.insert/#db.collection.insert" target="_blank">https://docs.mongodb.com/manual/reference/method/db.collection.insert/#db.collection.insert</a></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.collection.insert(
   </span>&lt;document or array of documents&gt;<span style="color: #000000;">,
   {
     writeConcern: </span>&lt;document&gt;<span style="color: #000000;">,
     ordered: </span>&lt;boolean&gt;<span style="color: #000000;">
   }
)</span></pre>
</div>
<p>&nbsp;</p>
<p>2，Query</p>
<p>1）查询嵌入式/嵌套文档</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('f011a183-4089-4f41-9e83-d407871b5fe4')"><img id="code_img_closed_f011a183-4089-4f41-9e83-d407871b5fe4" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_f011a183-4089-4f41-9e83-d407871b5fe4" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('f011a183-4089-4f41-9e83-d407871b5fe4',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_f011a183-4089-4f41-9e83-d407871b5fe4" class="cnblogs_code_hide">
<pre><span style="color: #000000;">db.inventory.insertMany( [
   { item: </span><span style="color: #800000;">"</span><span style="color: #800000;">journal</span><span style="color: #800000;">"</span>, qty: <span style="color: #800080;">25</span>, size: { h: <span style="color: #800080;">14</span>, w: <span style="color: #800080;">21</span>, uom: <span style="color: #800000;">"</span><span style="color: #800000;">cm</span><span style="color: #800000;">"</span> }, status: <span style="color: #800000;">"</span><span style="color: #800000;">A</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
   { item: </span><span style="color: #800000;">"</span><span style="color: #800000;">notebook</span><span style="color: #800000;">"</span>, qty: <span style="color: #800080;">50</span>, size: { h: <span style="color: #800080;">8.5</span>, w: <span style="color: #800080;">11</span>, uom: <span style="color: #800000;">"</span><span style="color: #800000;">in</span><span style="color: #800000;">"</span> }, status: <span style="color: #800000;">"</span><span style="color: #800000;">A</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
   { item: </span><span style="color: #800000;">"</span><span style="color: #800000;">paper</span><span style="color: #800000;">"</span>, qty: <span style="color: #800080;">100</span>, size: { h: <span style="color: #800080;">8.5</span>, w: <span style="color: #800080;">11</span>, uom: <span style="color: #800000;">"</span><span style="color: #800000;">in</span><span style="color: #800000;">"</span> }, status: <span style="color: #800000;">"</span><span style="color: #800000;">D</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
   { item: </span><span style="color: #800000;">"</span><span style="color: #800000;">planner</span><span style="color: #800000;">"</span>, qty: <span style="color: #800080;">75</span>, size: { h: <span style="color: #800080;">22.85</span>, w: <span style="color: #800080;">30</span>, uom: <span style="color: #800000;">"</span><span style="color: #800000;">cm</span><span style="color: #800000;">"</span> }, status: <span style="color: #800000;">"</span><span style="color: #800000;">D</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
   { item: </span><span style="color: #800000;">"</span><span style="color: #800000;">postcard</span><span style="color: #800000;">"</span>, qty: <span style="color: #800080;">45</span>, size: { h: <span style="color: #800080;">10</span>, w: <span style="color: #800080;">15.25</span>, uom: <span style="color: #800000;">"</span><span style="color: #800000;">cm</span><span style="color: #800000;">"</span> }, status: <span style="color: #800000;">"</span><span style="color: #800000;">A</span><span style="color: #800000;">"</span><span style="color: #000000;"> }
]);</span></pre>
</div>
<span class="cnblogs_code_collapse">数据</span></div>
<div class="cnblogs_code">
<pre>db.inventory.find( { size: { h: <span style="color: #800080;">14</span>, w: <span style="color: #800080;">21</span>, uom: <span style="color: #800000;">"</span><span style="color: #800000;">cm</span><span style="color: #800000;">"</span><span style="color: #000000;"> } } )
db.inventory.find( { </span><span style="color: #800000;">"</span><span style="color: #800000;">size.uom</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">in</span><span style="color: #800000;">"</span><span style="color: #000000;"> } )
db.inventory.find( { </span><span style="color: #800000;">"</span><span style="color: #800000;">size.h</span><span style="color: #800000;">"</span>: { $lt: <span style="color: #800080;">15</span><span style="color: #000000;"> } } )
db.inventory.find( { </span><span style="color: #800000;">"</span><span style="color: #800000;">size.h</span><span style="color: #800000;">"</span>: { $lt: <span style="color: #800080;">15</span> }, <span style="color: #800000;">"</span><span style="color: #800000;">size.uom</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">in</span><span style="color: #800000;">"</span>, status: <span style="color: #800000;">"</span><span style="color: #800000;">D</span><span style="color: #800000;">"</span> } )</pre>
</div>
<p>2）查询数组</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('5b82fad6-89d9-421e-b5da-04d0b301761e')"><img id="code_img_closed_5b82fad6-89d9-421e-b5da-04d0b301761e" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_5b82fad6-89d9-421e-b5da-04d0b301761e" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('5b82fad6-89d9-421e-b5da-04d0b301761e',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_5b82fad6-89d9-421e-b5da-04d0b301761e" class="cnblogs_code_hide">
<pre><span style="color: #000000;">db.inventory.insertMany([
   { item: </span><span style="color: #800000;">"</span><span style="color: #800000;">journal</span><span style="color: #800000;">"</span>, qty: <span style="color: #800080;">25</span>, tags: [<span style="color: #800000;">"</span><span style="color: #800000;">blank</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">red</span><span style="color: #800000;">"</span>], dim_cm: [ <span style="color: #800080;">14</span>, <span style="color: #800080;">21</span><span style="color: #000000;"> ] },
   { item: </span><span style="color: #800000;">"</span><span style="color: #800000;">notebook</span><span style="color: #800000;">"</span>, qty: <span style="color: #800080;">50</span>, tags: [<span style="color: #800000;">"</span><span style="color: #800000;">red</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">blank</span><span style="color: #800000;">"</span>], dim_cm: [ <span style="color: #800080;">14</span>, <span style="color: #800080;">21</span><span style="color: #000000;"> ] },
   { item: </span><span style="color: #800000;">"</span><span style="color: #800000;">paper</span><span style="color: #800000;">"</span>, qty: <span style="color: #800080;">100</span>, tags: [<span style="color: #800000;">"</span><span style="color: #800000;">red</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">blank</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">plain</span><span style="color: #800000;">"</span>], dim_cm: [ <span style="color: #800080;">14</span>, <span style="color: #800080;">21</span><span style="color: #000000;"> ] },
   { item: </span><span style="color: #800000;">"</span><span style="color: #800000;">planner</span><span style="color: #800000;">"</span>, qty: <span style="color: #800080;">75</span>, tags: [<span style="color: #800000;">"</span><span style="color: #800000;">blank</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">red</span><span style="color: #800000;">"</span>], dim_cm: [ <span style="color: #800080;">22.85</span>, <span style="color: #800080;">30</span><span style="color: #000000;"> ] },
   { item: </span><span style="color: #800000;">"</span><span style="color: #800000;">postcard</span><span style="color: #800000;">"</span>, qty: <span style="color: #800080;">45</span>, tags: [<span style="color: #800000;">"</span><span style="color: #800000;">blue</span><span style="color: #800000;">"</span>], dim_cm: [ <span style="color: #800080;">10</span>, <span style="color: #800080;">15.25</span><span style="color: #000000;"> ] }
]);</span></pre>
</div>
<span class="cnblogs_code_collapse">数据</span></div>
<div class="cnblogs_code">
<pre>db.inventory.find( { tags: [<span style="color: #800000;">"</span><span style="color: #800000;">red</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">blank</span><span style="color: #800000;">"</span><span style="color: #000000;">] } )
db.inventory.find( { tags: { $all: [</span><span style="color: #800000;">"</span><span style="color: #800000;">red</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">blank</span><span style="color: #800000;">"</span><span style="color: #000000;">] } } )
db.inventory.find( { tags: </span><span style="color: #800000;">"</span><span style="color: #800000;">red</span><span style="color: #800000;">"</span><span style="color: #000000;"> } )
db.inventory.find( { dim_cm: { $gt: </span><span style="color: #800080;">25</span><span style="color: #000000;"> } } )
db.inventory.find( { dim_cm: { $gt: </span><span style="color: #800080;">15</span>, $lt: <span style="color: #800080;">20</span><span style="color: #000000;"> } } )
db.inventory.find( { dim_cm: { $elemMatch: { $gt: </span><span style="color: #800080;">22</span>, $lt: <span style="color: #800080;">30</span><span style="color: #000000;"> } } } )
db.inventory.find( { </span><span style="color: #800000;">"</span><span style="color: #800000;">dim_cm.1</span><span style="color: #800000;">"</span>: { $gt: <span style="color: #800080;">25</span><span style="color: #000000;"> } } )
db.inventory.find( { </span><span style="color: #800000;">"</span><span style="color: #800000;">tags</span><span style="color: #800000;">"</span>: { $size: <span style="color: #800080;">3</span> } } )</pre>
</div>
<p>3）查询嵌入式文档数组</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('8222d448-912b-4312-b85f-72531e3a58e3')"><img id="code_img_closed_8222d448-912b-4312-b85f-72531e3a58e3" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_8222d448-912b-4312-b85f-72531e3a58e3" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('8222d448-912b-4312-b85f-72531e3a58e3',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_8222d448-912b-4312-b85f-72531e3a58e3" class="cnblogs_code_hide">
<pre><span style="color: #000000;">db.inventory.insertMany( [
   { item: </span><span style="color: #800000;">"</span><span style="color: #800000;">journal</span><span style="color: #800000;">"</span>, instock: [ { warehouse: <span style="color: #800000;">"</span><span style="color: #800000;">A</span><span style="color: #800000;">"</span>, qty: <span style="color: #800080;">5</span> }, { warehouse: <span style="color: #800000;">"</span><span style="color: #800000;">C</span><span style="color: #800000;">"</span>, qty: <span style="color: #800080;">15</span><span style="color: #000000;"> } ] },
   { item: </span><span style="color: #800000;">"</span><span style="color: #800000;">notebook</span><span style="color: #800000;">"</span>, instock: [ { warehouse: <span style="color: #800000;">"</span><span style="color: #800000;">C</span><span style="color: #800000;">"</span>, qty: <span style="color: #800080;">5</span><span style="color: #000000;"> } ] },
   { item: </span><span style="color: #800000;">"</span><span style="color: #800000;">paper</span><span style="color: #800000;">"</span>, instock: [ { warehouse: <span style="color: #800000;">"</span><span style="color: #800000;">A</span><span style="color: #800000;">"</span>, qty: <span style="color: #800080;">60</span> }, { warehouse: <span style="color: #800000;">"</span><span style="color: #800000;">B</span><span style="color: #800000;">"</span>, qty: <span style="color: #800080;">15</span><span style="color: #000000;"> } ] },
   { item: </span><span style="color: #800000;">"</span><span style="color: #800000;">planner</span><span style="color: #800000;">"</span>, instock: [ { warehouse: <span style="color: #800000;">"</span><span style="color: #800000;">A</span><span style="color: #800000;">"</span>, qty: <span style="color: #800080;">40</span> }, { warehouse: <span style="color: #800000;">"</span><span style="color: #800000;">B</span><span style="color: #800000;">"</span>, qty: <span style="color: #800080;">5</span><span style="color: #000000;"> } ] },
   { item: </span><span style="color: #800000;">"</span><span style="color: #800000;">postcard</span><span style="color: #800000;">"</span>, instock: [ { warehouse: <span style="color: #800000;">"</span><span style="color: #800000;">B</span><span style="color: #800000;">"</span>, qty: <span style="color: #800080;">15</span> }, { warehouse: <span style="color: #800000;">"</span><span style="color: #800000;">C</span><span style="color: #800000;">"</span>, qty: <span style="color: #800080;">35</span><span style="color: #000000;"> } ] }
]);</span></pre>
</div>
<span class="cnblogs_code_collapse">数据</span></div>
<div class="cnblogs_code">
<pre>db.inventory.find( { <span style="color: #800000;">"</span><span style="color: #800000;">instock</span><span style="color: #800000;">"</span>: { warehouse: <span style="color: #800000;">"</span><span style="color: #800000;">A</span><span style="color: #800000;">"</span>, qty: <span style="color: #800080;">5</span><span style="color: #000000;"> } } )
db.inventory.find( { </span><span style="color: #800000;">'</span><span style="color: #800000;">instock.qty</span><span style="color: #800000;">'</span>: { $lte: <span style="color: #800080;">20</span><span style="color: #000000;"> } } )
db.inventory.find( { </span><span style="color: #800000;">'</span><span style="color: #800000;">instock.0.qty</span><span style="color: #800000;">'</span>: { $lte: <span style="color: #800080;">20</span><span style="color: #000000;"> } } )
db.inventory.find( { </span><span style="color: #800000;">"</span><span style="color: #800000;">instock</span><span style="color: #800000;">"</span>: { $elemMatch: { qty: <span style="color: #800080;">5</span>, warehouse: <span style="color: #800000;">"</span><span style="color: #800000;">A</span><span style="color: #800000;">"</span><span style="color: #000000;"> } } } ) 
db.inventory.find( { </span><span style="color: #800000;">"</span><span style="color: #800000;">instock</span><span style="color: #800000;">"</span>: { $elemMatch: { qty: { $gt: <span style="color: #800080;">10</span>, $lte: <span style="color: #800080;">20</span><span style="color: #000000;"> } } } } )
db.inventory.find( { </span><span style="color: #800000;">"</span><span style="color: #800000;">instock.qty</span><span style="color: #800000;">"</span>: { $gt: <span style="color: #800080;">10</span>,  $lte: <span style="color: #800080;">20</span><span style="color: #000000;"> } } )
db.inventory.find( { </span><span style="color: #800000;">"</span><span style="color: #800000;">instock.qty</span><span style="color: #800000;">"</span>: <span style="color: #800080;">5</span>, <span style="color: #800000;">"</span><span style="color: #800000;">instock.warehouse</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">A</span><span style="color: #800000;">"</span> } )</pre>
</div>
<p>4）返回指定的字段</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('8e129fa8-2f7e-49bc-a642-f9ad29a1c06c')"><img id="code_img_closed_8e129fa8-2f7e-49bc-a642-f9ad29a1c06c" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_8e129fa8-2f7e-49bc-a642-f9ad29a1c06c" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('8e129fa8-2f7e-49bc-a642-f9ad29a1c06c',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_8e129fa8-2f7e-49bc-a642-f9ad29a1c06c" class="cnblogs_code_hide">
<pre><span style="color: #000000;">db.inventory.insertMany( [
  { item: </span><span style="color: #800000;">"</span><span style="color: #800000;">journal</span><span style="color: #800000;">"</span>, status: <span style="color: #800000;">"</span><span style="color: #800000;">A</span><span style="color: #800000;">"</span>, size: { h: <span style="color: #800080;">14</span>, w: <span style="color: #800080;">21</span>, uom: <span style="color: #800000;">"</span><span style="color: #800000;">cm</span><span style="color: #800000;">"</span> }, instock: [ { warehouse: <span style="color: #800000;">"</span><span style="color: #800000;">A</span><span style="color: #800000;">"</span>, qty: <span style="color: #800080;">5</span><span style="color: #000000;"> } ] },
  { item: </span><span style="color: #800000;">"</span><span style="color: #800000;">notebook</span><span style="color: #800000;">"</span>, status: <span style="color: #800000;">"</span><span style="color: #800000;">A</span><span style="color: #800000;">"</span>,  size: { h: <span style="color: #800080;">8.5</span>, w: <span style="color: #800080;">11</span>, uom: <span style="color: #800000;">"</span><span style="color: #800000;">in</span><span style="color: #800000;">"</span> }, instock: [ { warehouse: <span style="color: #800000;">"</span><span style="color: #800000;">C</span><span style="color: #800000;">"</span>, qty: <span style="color: #800080;">5</span><span style="color: #000000;"> } ] },
  { item: </span><span style="color: #800000;">"</span><span style="color: #800000;">paper</span><span style="color: #800000;">"</span>, status: <span style="color: #800000;">"</span><span style="color: #800000;">D</span><span style="color: #800000;">"</span>, size: { h: <span style="color: #800080;">8.5</span>, w: <span style="color: #800080;">11</span>, uom: <span style="color: #800000;">"</span><span style="color: #800000;">in</span><span style="color: #800000;">"</span> }, instock: [ { warehouse: <span style="color: #800000;">"</span><span style="color: #800000;">A</span><span style="color: #800000;">"</span>, qty: <span style="color: #800080;">60</span><span style="color: #000000;"> } ] },
  { item: </span><span style="color: #800000;">"</span><span style="color: #800000;">planner</span><span style="color: #800000;">"</span>, status: <span style="color: #800000;">"</span><span style="color: #800000;">D</span><span style="color: #800000;">"</span>, size: { h: <span style="color: #800080;">22.85</span>, w: <span style="color: #800080;">30</span>, uom: <span style="color: #800000;">"</span><span style="color: #800000;">cm</span><span style="color: #800000;">"</span> }, instock: [ { warehouse: <span style="color: #800000;">"</span><span style="color: #800000;">A</span><span style="color: #800000;">"</span>, qty: <span style="color: #800080;">40</span><span style="color: #000000;"> } ] },
  { item: </span><span style="color: #800000;">"</span><span style="color: #800000;">postcard</span><span style="color: #800000;">"</span>, status: <span style="color: #800000;">"</span><span style="color: #800000;">A</span><span style="color: #800000;">"</span>, size: { h: <span style="color: #800080;">10</span>, w: <span style="color: #800080;">15.25</span>, uom: <span style="color: #800000;">"</span><span style="color: #800000;">cm</span><span style="color: #800000;">"</span> }, instock: [ { warehouse: <span style="color: #800000;">"</span><span style="color: #800000;">B</span><span style="color: #800000;">"</span>, qty: <span style="color: #800080;">15</span> }, { warehouse: <span style="color: #800000;">"</span><span style="color: #800000;">C</span><span style="color: #800000;">"</span>, qty: <span style="color: #800080;">35</span><span style="color: #000000;"> } ] }
]);</span></pre>
</div>
<span class="cnblogs_code_collapse">数据</span></div>
<div class="cnblogs_code">
<pre>db.inventory.find( { status: <span style="color: #800000;">"</span><span style="color: #800000;">A</span><span style="color: #800000;">"</span> }, { item: <span style="color: #800080;">1</span>, status: <span style="color: #800080;">1</span><span style="color: #000000;"> } )
SELECT _id, item, status </span><span style="color: #0000ff;">from</span> inventory WHERE status = <span style="color: #800000;">"</span><span style="color: #800000;">A</span><span style="color: #800000;">"</span></pre>
</div>
<div class="cnblogs_code">
<pre>db.inventory.find( { status: <span style="color: #800000;">"</span><span style="color: #800000;">A</span><span style="color: #800000;">"</span> }, { item: <span style="color: #800080;">1</span>, status: <span style="color: #800080;">1</span>, _id: <span style="color: #800080;">0</span><span style="color: #000000;"> } )
SELECT item, status </span><span style="color: #0000ff;">from</span> inventory WHERE status = <span style="color: #800000;">"</span><span style="color: #800000;">A</span><span style="color: #800000;">"</span></pre>
</div>
<p>5）查询空字段或缺少字段</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('4e6bf81e-cf77-4141-98b2-027f0298e942')"><img id="code_img_closed_4e6bf81e-cf77-4141-98b2-027f0298e942" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_4e6bf81e-cf77-4141-98b2-027f0298e942" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('4e6bf81e-cf77-4141-98b2-027f0298e942',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_4e6bf81e-cf77-4141-98b2-027f0298e942" class="cnblogs_code_hide">
<pre><span style="color: #000000;">db.inventory.insertMany([
   { _id: </span><span style="color: #800080;">1</span>, item: <span style="color: #0000ff;">null</span><span style="color: #000000;"> },
   { _id: </span><span style="color: #800080;">2</span><span style="color: #000000;"> }
])</span></pre>
</div>
<span class="cnblogs_code_collapse">数据</span></div>
<div class="cnblogs_code">
<pre>db.inventory.find( { item: <span style="color: #0000ff;">null</span><span style="color: #000000;"> } )
db.inventory.find( { item : { $type: </span><span style="color: #800080;">10</span><span style="color: #000000;"> } } )
db.inventory.find( { item : { $exists: </span><span style="color: #0000ff;">false</span> } } )</pre>
</div>
<p>6）迭代游标</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> myCursor = db.users.find( { type: <span style="color: #800080;">2</span><span style="color: #000000;"> } );

</span><span style="color: #0000ff;">while</span><span style="color: #000000;"> (myCursor.hasNext()) {
   print(tojson(myCursor.next()));
}</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> myCursor = db.users.find( { type: <span style="color: #800080;">2</span><span style="color: #000000;"> } );

</span><span style="color: #0000ff;">while</span><span style="color: #000000;"> (myCursor.hasNext()) {
   printjson(myCursor.next());
}</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> myCursor =  db.users.find( { type: <span style="color: #800080;">2</span><span style="color: #000000;"> } );

myCursor.forEach(printjson);</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> myCursor = db.inventory.find( { type: <span style="color: #800080;">2</span><span style="color: #000000;"> } );
</span><span style="color: #0000ff;">var</span> documentArray =<span style="color: #000000;"> myCursor.toArray();
</span><span style="color: #0000ff;">var</span> myDocument = documentArray[<span style="color: #800080;">3</span>];</pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> myCursor = db.users.find( { type: <span style="color: #800080;">2</span><span style="color: #000000;"> } );
</span><span style="color: #0000ff;">var</span> myDocument = myCursor[<span style="color: #800080;">1</span>];</pre>
</div>
<p>&nbsp;</p>
<p>3，Update</p>
<p>1）db.collection.updateOne() 【即使多个文档可能与指定的过滤器匹配，也会更新与指定过滤器匹配的单个文档】<br />详细文档：<a href="https://docs.mongodb.com/manual/reference/method/db.collection.updateOne/#db.collection.updateOne" target="_blank">https://docs.mongodb.com/manual/reference/method/db.collection.updateOne/#db.collection.updateOne</a></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.collection.updateOne(
   </span>&lt;filter&gt;<span style="color: #000000;">,
   </span>&lt;update&gt;<span style="color: #000000;">,
   {
     upsert: </span>&lt;boolean&gt;<span style="color: #000000;">,
     writeConcern: </span>&lt;document&gt;<span style="color: #000000;">,
     collation: </span>&lt;document&gt;<span style="color: #000000;">,
     arrayFilters: [ </span>&lt;filterdocument1&gt;<span style="color: #000000;">, ... ]
   }
)</span></pre>
</div>
<p>&nbsp;</p>
<p>2）db.collection.updateMany() 【更新所有匹配指定过滤器的文档】</p>
<p>详细文档：<a href="https://docs.mongodb.com/manual/reference/method/db.collection.updateMany/#db.collection.updateMany" target="_blank">https://docs.mongodb.com/manual/reference/method/db.collection.updateMany/#db.collection.updateMany</a></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.collection.updateMany(
   </span>&lt;filter&gt;<span style="color: #000000;">,
   </span>&lt;update&gt;<span style="color: #000000;">,
   {
     upsert: </span>&lt;boolean&gt;<span style="color: #000000;">,
     writeConcern: </span>&lt;document&gt;<span style="color: #000000;">,
     collation: </span>&lt;document&gt;<span style="color: #000000;">,
     arrayFilters: [ </span>&lt;filterdocument1&gt;<span style="color: #000000;">, ... ]
   }
)</span></pre>
</div>
<p>&nbsp;</p>
<p>3）db.collection.replaceOne() 【即使多个文档可能与指定的过滤器匹配，也只能替换与指定过滤器匹配的单个文档】</p>
<p>详细文档：<a href="https://docs.mongodb.com/manual/reference/method/db.collection.replaceOne/#db.collection.replaceOne" target="_blank">https://docs.mongodb.com/manual/reference/method/db.collection.replaceOne/#db.collection.replaceOne</a></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.collection.replaceOne(
   </span>&lt;filter&gt;<span style="color: #000000;">,
   </span>&lt;replacement&gt;<span style="color: #000000;">,
   {
     upsert: </span>&lt;boolean&gt;<span style="color: #000000;">,
     writeConcern: </span>&lt;document&gt;<span style="color: #000000;">,
     collation: </span>&lt;document&gt;<span style="color: #000000;">
   }
)</span></pre>
</div>
<p>&nbsp;</p>
<p>4）db.collection.update()</p>
<p>详细文档：<a href="https://docs.mongodb.com/manual/reference/method/db.collection.update/#db.collection.update" target="_blank">https://docs.mongodb.com/manual/reference/method/db.collection.update/#db.collection.update</a></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.collection.update(
   </span>&lt;query&gt;<span style="color: #000000;">,
   </span>&lt;update&gt;<span style="color: #000000;">,
   {
     upsert: </span>&lt;boolean&gt;<span style="color: #000000;">,
     multi: </span>&lt;boolean&gt;<span style="color: #000000;">,
     writeConcern: </span>&lt;document&gt;<span style="color: #000000;">,
     collation: </span>&lt;document&gt;<span style="color: #000000;">,
     arrayFilters: [ </span>&lt;filterdocument1&gt;<span style="color: #000000;">, ... ]
   }
)</span></pre>
</div>
<p>更新或替换与指定过滤器匹配的单个文档，或更新与指定过滤器匹配的所有文档。</p>
<p>默认情况下，db.collection.update()方法更新单个文档。 要更新多个文档，请使用multi选项。</p>
<p>&nbsp;</p>
<p>4，Delete</p>
<p><br />1）db.collection.deleteOne() 【即使多个文档可能匹配指定的过滤器，也最多删除与指定过滤器匹配的单个文档】</p>
<p>详细文档：<a href="https://docs.mongodb.com/manual/reference/method/db.collection.deleteOne/#db.collection.deleteOne" target="_blank">https://docs.mongodb.com/manual/reference/method/db.collection.deleteOne/#db.collection.deleteOne</a></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.collection.deleteOne(
   </span>&lt;filter&gt;<span style="color: #000000;">,
   {
      writeConcern: </span>&lt;document&gt;<span style="color: #000000;">,
      collation: </span>&lt;document&gt;<span style="color: #000000;">
   }
)</span></pre>
</div>
<p>&nbsp;</p>
<p>2）db.collection.deleteMany() 【删除所有匹配指定过滤器的文档】</p>
<p>详细文档：<a href="https://docs.mongodb.com/manual/reference/method/db.collection.deleteMany/#db.collection.deleteMany" target="_blank">https://docs.mongodb.com/manual/reference/method/db.collection.deleteMany/#db.collection.deleteMany</a></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.collection.deleteMany(
   </span>&lt;filter&gt;<span style="color: #000000;">,
   {
      writeConcern: </span>&lt;document&gt;<span style="color: #000000;">,
      collation: </span>&lt;document&gt;<span style="color: #000000;">
   }
)</span></pre>
</div>
<p>&nbsp;</p>
<p>3）db.collection.remove() 【删除单个文档或与指定过滤器匹配的所有文档】.</p>
<p>详细文档：<a href="https://docs.mongodb.com/manual/reference/method/db.collection.remove/#db.collection.remove" target="_blank">https://docs.mongodb.com/manual/reference/method/db.collection.remove/#db.collection.remove</a></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.collection.remove(
   </span>&lt;query&gt;<span style="color: #000000;">,
   </span>&lt;justOne&gt;<span style="color: #000000;">
)</span></pre>
</div>
<p>justOne（true：删除一个。false：删除多个）。默认为false</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a15"></a>十五、索引</span></strong></span></p>
<div class="cnblogs_code">
<pre>db.students.find({}).explain() <span style="color: #008000;">//</span><span style="color: #008000;">查询执行计划</span></pre>
</div>
<p>1，Single Field Indexes（单键索引）</p>
<p>详细文档：<a href="https://docs.mongodb.com/manual/core/index-single/#create-an-index-on-an-embedded-field" target="_blank">https://docs.mongodb.com/manual/core/index-single/#create-an-index-on-an-embedded-field</a></p>
<p>1）在单个字段上创建升序索引</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span>: ObjectId(<span style="color: #800000;">"</span><span style="color: #800000;">570c04a4ad233577f97dc459</span><span style="color: #800000;">"</span><span style="color: #000000;">),
  </span><span style="color: #800000;">"</span><span style="color: #800000;">score</span><span style="color: #800000;">"</span>: <span style="color: #800080;">1034</span><span style="color: #000000;">,
  </span><span style="color: #800000;">"</span><span style="color: #800000;">location</span><span style="color: #800000;">"</span>: { state: <span style="color: #800000;">"</span><span style="color: #800000;">NY</span><span style="color: #800000;">"</span>, city: <span style="color: #800000;">"</span><span style="color: #800000;">New York</span><span style="color: #800000;">"</span><span style="color: #000000;"> }
}
db.records.createIndex( { score: </span><span style="color: #800080;">1</span> } )</pre>
</div>
<p>2）在嵌入式字段上创建索引</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">{
</span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span>: ObjectId(<span style="color: #800000;">"</span><span style="color: #800000;">570c04a4ad233577f97dc459</span><span style="color: #800000;">"</span><span style="color: #000000;">),
</span><span style="color: #800000;">"</span><span style="color: #800000;">score</span><span style="color: #800000;">"</span>: <span style="color: #800080;">1034</span><span style="color: #000000;">,
</span><span style="color: #800000;">"</span><span style="color: #800000;">location</span><span style="color: #800000;">"</span>: { state: <span style="color: #800000;">"</span><span style="color: #800000;">NY</span><span style="color: #800000;">"</span>, city: <span style="color: #800000;">"</span><span style="color: #800000;">New York</span><span style="color: #800000;">"</span><span style="color: #000000;"> }
}
db.records.createIndex( { </span><span style="color: #800000;">"</span><span style="color: #800000;">location.state</span><span style="color: #800000;">"</span>: <span style="color: #800080;">1</span> } )</pre>
</div>
<p>3）在嵌入式文档上创建一个索引</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">{
</span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span>: ObjectId(<span style="color: #800000;">"</span><span style="color: #800000;">570c04a4ad233577f97dc459</span><span style="color: #800000;">"</span><span style="color: #000000;">),
</span><span style="color: #800000;">"</span><span style="color: #800000;">score</span><span style="color: #800000;">"</span>: <span style="color: #800080;">1034</span><span style="color: #000000;">,
</span><span style="color: #800000;">"</span><span style="color: #800000;">location</span><span style="color: #800000;">"</span>: { state: <span style="color: #800000;">"</span><span style="color: #800000;">NY</span><span style="color: #800000;">"</span>, city: <span style="color: #800000;">"</span><span style="color: #800000;">New York</span><span style="color: #800000;">"</span><span style="color: #000000;"> }
}
db.records.createIndex( { location: </span><span style="color: #800080;">1</span> } )</pre>
</div>
<p>2，Compound Indexes（复合索引）</p>
<p>详细文档：<a href="https://docs.mongodb.com/manual/core/index-compound/" target="_blank">https://docs.mongodb.com/manual/core/index-compound/</a></p>
<p>1）创建一个复合索引</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">{
</span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span><span style="color: #000000;">: ObjectId(...),
</span><span style="color: #800000;">"</span><span style="color: #800000;">item</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">Banana</span><span style="color: #800000;">"</span><span style="color: #000000;">,
</span><span style="color: #800000;">"</span><span style="color: #800000;">category</span><span style="color: #800000;">"</span>: [<span style="color: #800000;">"</span><span style="color: #800000;">food</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">produce</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">grocery</span><span style="color: #800000;">"</span><span style="color: #000000;">],
</span><span style="color: #800000;">"</span><span style="color: #800000;">location</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">4th Street Store</span><span style="color: #800000;">"</span><span style="color: #000000;">,
</span><span style="color: #800000;">"</span><span style="color: #800000;">stock</span><span style="color: #800000;">"</span>: <span style="color: #800080;">4</span><span style="color: #000000;">,
</span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">cases</span><span style="color: #800000;">"</span><span style="color: #000000;">
}
db.products.createIndex( { </span><span style="color: #800000;">"</span><span style="color: #800000;">item</span><span style="color: #800000;">"</span>: <span style="color: #800080;">1</span>, <span style="color: #800000;">"</span><span style="color: #800000;">stock</span><span style="color: #800000;">"</span>: <span style="color: #800080;">1</span> } )</pre>
</div>
<p>3，Multikey Indexes（多键索引）</p>
<p>详细文档：<a href="https://docs.mongodb.com/manual/core/index-multikey/" target="_blank">https://docs.mongodb.com/manual/core/index-multikey/</a></p>
<p>要索引一个包含数组值的字段，MongoDB会为数组中的每个元素创建一个索引键</p>
<div class="cnblogs_code">
<pre>{ _id: <span style="color: #800080;">5</span>, type: <span style="color: #800000;">"</span><span style="color: #800000;">food</span><span style="color: #800000;">"</span>, item: <span style="color: #800000;">"</span><span style="color: #800000;">aaa</span><span style="color: #800000;">"</span>, ratings: [ <span style="color: #800080;">5</span>, <span style="color: #800080;">8</span>, <span style="color: #800080;">9</span><span style="color: #000000;"> ] }
{ _id: </span><span style="color: #800080;">6</span>, type: <span style="color: #800000;">"</span><span style="color: #800000;">food</span><span style="color: #800000;">"</span>, item: <span style="color: #800000;">"</span><span style="color: #800000;">bbb</span><span style="color: #800000;">"</span>, ratings: [ <span style="color: #800080;">5</span>, <span style="color: #800080;">9</span><span style="color: #000000;"> ] }
{ _id: </span><span style="color: #800080;">7</span>, type: <span style="color: #800000;">"</span><span style="color: #800000;">food</span><span style="color: #800000;">"</span>, item: <span style="color: #800000;">"</span><span style="color: #800000;">ccc</span><span style="color: #800000;">"</span>, ratings: [ <span style="color: #800080;">9</span>, <span style="color: #800080;">5</span>, <span style="color: #800080;">8</span><span style="color: #000000;"> ] }
{ _id: </span><span style="color: #800080;">8</span>, type: <span style="color: #800000;">"</span><span style="color: #800000;">food</span><span style="color: #800000;">"</span>, item: <span style="color: #800000;">"</span><span style="color: #800000;">ddd</span><span style="color: #800000;">"</span>, ratings: [ <span style="color: #800080;">9</span>, <span style="color: #800080;">5</span><span style="color: #000000;"> ] }
{ _id: </span><span style="color: #800080;">9</span>, type: <span style="color: #800000;">"</span><span style="color: #800000;">food</span><span style="color: #800000;">"</span>, item: <span style="color: #800000;">"</span><span style="color: #800000;">eee</span><span style="color: #800000;">"</span>, ratings: [ <span style="color: #800080;">5</span>, <span style="color: #800080;">9</span>, <span style="color: #800080;">5</span><span style="color: #000000;"> ] }

db.inventory.createIndex( { ratings: </span><span style="color: #800080;">1</span> } )</pre>
</div>
<p>4，Hashed Indexes（hash索引）</p>
<p>详细文档：<a href="https://docs.mongodb.com/manual/core/index-hashed/" target="_blank">https://docs.mongodb.com/manual/core/index-hashed/</a></p>
<div class="cnblogs_code">
<pre>db.collection.createIndex( { _id: <span style="color: #800000;">"</span><span style="color: #800000;">hashed</span><span style="color: #800000;">"</span> } )</pre>
</div>
<p>5，Partial Indexes（局部索引）</p>
<p>使用更小的空间提高部分性能</p>
<p>1）例如，以下操作将创建仅索引defaultQty字段大于200的文档的复合索引。</p>
<div class="cnblogs_code">
<pre>db.products.createIndex({defaultQty:<span style="color: #800080;">1</span>},{ partialFilterExpression: { defaultQty: { $gt: <span style="color: #800080;">200</span> } } })</pre>
</div>
<p>6，Unique Indexes（唯一索引）</p>
<div class="cnblogs_code">
<pre>db.members.createIndex( { <span style="color: #800000;">"</span><span style="color: #800000;">user_id</span><span style="color: #800000;">"</span>: <span style="color: #800080;">1</span> }, { unique: <span style="color: #0000ff;">true</span> } )</pre>
</div>
<p>7，Sparse Indexes（稀疏索引）</p>
<p>详细文档：<a href="https://docs.mongodb.com/manual/core/index-sparse/" target="_blank">https://docs.mongodb.com/manual/core/index-sparse/</a></p>
<p>即使索引字段包含空值，稀疏索引也只包含具有索引字段的文档的条目。 索引跳过缺少索引字段的任何文档。 索引是&ldquo;稀疏的&rdquo;，因为它不包含集合的所有文档。 相比之下，非稀疏索引包含集合中的所有文档，为那些不包含索引字段的文档存储空值。</p>
<p>1)创建一个稀疏索引（使用a作为条件时会IXSCAN）</p>
<div class="cnblogs_code">
<pre>{ <span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : ObjectId(<span style="color: #800000;">"</span><span style="color: #800000;">523b6e32fb408eea0eec2647</span><span style="color: #800000;">"</span>), <span style="color: #800000;">"</span><span style="color: #800000;">a</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">a</span><span style="color: #800000;">"</span><span style="color: #000000;"> }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : ObjectId(<span style="color: #800000;">"</span><span style="color: #800000;">523b6e61fb408eea0eec2648</span><span style="color: #800000;">"</span>), <span style="color: #800000;">"</span><span style="color: #800000;">b</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">b</span><span style="color: #800000;">"</span><span style="color: #000000;"> }
{ </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : ObjectId(<span style="color: #800000;">"</span><span style="color: #800000;">523b6e6ffb408eea0eec2649</span><span style="color: #800000;">"</span>), <span style="color: #800000;">"</span><span style="color: #800000;">c</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">c</span><span style="color: #800000;">"</span><span style="color: #000000;">}

db.scores.createIndex( { a: </span><span style="color: #800080;">1</span> } , { sparse: <span style="color: #0000ff;">true</span> } )</pre>
</div>
<p>2）只查询包含稀疏索引的字段（a）</p>
<div class="cnblogs_code">
<pre>db.getCollection(<span style="color: #800000;">'</span><span style="color: #800000;">test</span><span style="color: #800000;">'</span>).find().hint({ a: <span style="color: #800080;">1</span><span style="color: #000000;"> })

结果：
</span><span style="color: #008000;">/*</span><span style="color: #008000;"> 1 </span><span style="color: #008000;">*/</span><span style="color: #000000;">
{
    </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : ObjectId(<span style="color: #800000;">"</span><span style="color: #800000;">523b6e32fb408eea0eec2647</span><span style="color: #800000;">"</span><span style="color: #000000;">),
    </span><span style="color: #800000;">"</span><span style="color: #800000;">a</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">a</span><span style="color: #800000;">"</span><span style="color: #000000;">
}</span></pre>
</div>
<p>&nbsp;</p>
<p>8，TTL Indexes（过期索引）</p>
<p>详细文档：<a href="https://docs.mongodb.com/manual/core/index-ttl/" target="_blank">https://docs.mongodb.com/manual/core/index-ttl/</a></p>
<div class="cnblogs_code">
<pre>db.eventlog.createIndex( { <span style="color: #800000;">"</span><span style="color: #800000;">lastModifiedDate</span><span style="color: #800000;">"</span>: <span style="color: #800080;">1</span> }, { expireAfterSeconds: <span style="color: #800080;">3600</span> } )</pre>
</div>
<pre><span class="nx">expireAfterSeconds：过期秒数<br /><span style="color: #ff0000;">注：mongodb每60s执行一次task。所以把过期时间设置的过短，也会60s执行一次</span></span></pre>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.dates.insert({
    lastdate:</span><span style="color: #0000ff;">new</span><span style="color: #000000;"> Date(),
    a:</span><span style="color: #800000;">"</span><span style="color: #800000;">a</span><span style="color: #800000;">"</span><span style="color: #000000;">
    })

db.dates.createIndex({</span><span style="color: #800000;">"</span><span style="color: #800000;">lastdate</span><span style="color: #800000;">"</span>:<span style="color: #800080;">1</span>},{expireAfterSeconds:<span style="color: #800080;">1</span>})</pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a16"></a>十六，分布式文件系统GridFS</span></strong></span></p>
<p>1，何时使用GridFS？</p>
<p>在MongoDB中，使用GridFS存储大于16 MB的文件。&nbsp;</p>
<p>2，GridFS集合</p>
<p>GridFS将文件存储在两个集合中：</p>
<ul class="simple">
<li><code class="docutils literal">chunks</code>&nbsp;（fs.chunks）存储二进制块</li>
<li><code class="docutils literal">files</code>&nbsp;（fs.files）存储文件的元数据</li>
</ul>
<div class="cnblogs_code" onclick="cnblogs_code_show('a7903330-271b-407b-aee5-9844c54a3911')"><img id="code_img_closed_a7903330-271b-407b-aee5-9844c54a3911" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_a7903330-271b-407b-aee5-9844c54a3911" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('a7903330-271b-407b-aee5-9844c54a3911',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_a7903330-271b-407b-aee5-9844c54a3911" class="cnblogs_code_hide">
<pre><span style="color: #000000;">{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : &lt;ObjectId&gt;,  <span style="color: #008000;">//</span><span style="color: #008000;">chunk的唯一ObjectId。</span>
  <span style="color: #800000;">"</span><span style="color: #800000;">files_id</span><span style="color: #800000;">"</span> : &lt;ObjectId&gt;, <span style="color: #008000;">//</span><span style="color: #008000;">文件集合中指定的&ldquo;父&rdquo;文档的_id。</span>
  <span style="color: #800000;">"</span><span style="color: #800000;">n</span><span style="color: #800000;">"</span> : &lt;num&gt;, <span style="color: #008000;">//</span><span style="color: #008000;">chunk的序列号。 GridFS将所有chunk从0开始编号。</span>
  <span style="color: #800000;">"</span><span style="color: #800000;">data</span><span style="color: #800000;">"</span> : &lt;binary&gt; <span style="color: #008000;">//</span><span style="color: #008000;">二进制</span>
}</pre>
</div>
<span class="cnblogs_code_collapse">fs.chunks数据结构</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('fc871616-0ac9-4a4c-a209-5c144d2392c9')"><img id="code_img_closed_fc871616-0ac9-4a4c-a209-5c144d2392c9" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_fc871616-0ac9-4a4c-a209-5c144d2392c9" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('fc871616-0ac9-4a4c-a209-5c144d2392c9',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_fc871616-0ac9-4a4c-a209-5c144d2392c9" class="cnblogs_code_hide">
<pre><span style="color: #000000;">{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : &lt;ObjectId&gt;, <span style="color: #008000;">//</span><span style="color: #008000;">此文档的唯一标识符</span>
  <span style="color: #800000;">"</span><span style="color: #800000;">length</span><span style="color: #800000;">"</span> : &lt;num&gt;, <span style="color: #008000;">//</span><span style="color: #008000;">文档的大小（以字节为单位）</span>
  <span style="color: #800000;">"</span><span style="color: #800000;">chunkSize</span><span style="color: #800000;">"</span> : &lt;num&gt;, <span style="color: #008000;">//</span><span style="color: #008000;">每个块的大小（以字节为单位）默认大小是255千字节（kB）</span>
  <span style="color: #800000;">"</span><span style="color: #800000;">uploadDate</span><span style="color: #800000;">"</span> : &lt;timestamp&gt;,<span style="color: #008000;">//</span><span style="color: #008000;">GridFS首次存储文档的日期</span>
  <span style="color: #800000;">"</span><span style="color: #800000;">md5</span><span style="color: #800000;">"</span> : &lt;hash&gt;,<span style="color: #008000;">//
</span>  <span style="color: #800000;">"</span><span style="color: #800000;">filename</span><span style="color: #800000;">"</span> : &lt;<span style="color: #0000ff;">string</span>&gt;,<span style="color: #008000;">//</span><span style="color: #008000;">可选的。 GridFS文件的可读名称。</span>
  <span style="color: #800000;">"</span><span style="color: #800000;">contentType</span><span style="color: #800000;">"</span> : &lt;<span style="color: #0000ff;">string</span>&gt;,<span style="color: #008000;">//</span><span style="color: #008000;">可选的。 GridFS文件的有效MIME类型。</span>
  <span style="color: #800000;">"</span><span style="color: #800000;">aliases</span><span style="color: #800000;">"</span> : &lt;<span style="color: #0000ff;">string</span> array&gt;,<span style="color: #008000;">//</span><span style="color: #008000;">可选的。 一组别名字符串。</span>
  <span style="color: #800000;">"</span><span style="color: #800000;">metadata</span><span style="color: #800000;">"</span> : &lt;any&gt;,<span style="color: #008000;">//</span><span style="color: #008000;">可选的。 元数据字段可以是任何数据类型，并且可以保存您想要存储的任何附加信息</span>
}</pre>
</div>
<span class="cnblogs_code_collapse">fs.files数据结构</span></div>
<p>3，这个&nbsp;fs.chunks的索引</p>
<p>GridFS使用files_id和n字段在块集合上使用唯一的复合索引。 这可以有效地检索块，如以下示例所示：</p>
<div class="cnblogs_code">
<pre>db.fs.chunks.find( { files_id: myFileID } ).sort( { n: <span style="color: #800080;">1</span> } )</pre>
</div>
<p>如果此索引不存在，则可以发出以下操作以使用mongo shell创建它：</p>
<div class="cnblogs_code">
<pre>db.fs.chunks.createIndex( { files_id: <span style="color: #800080;">1</span>, n: <span style="color: #800080;">1</span> }, { unique: <span style="color: #0000ff;">true</span> } );</pre>
</div>
<p>4，这个&nbsp;fs.files的索引</p>
<p>GridFS使用文件名和uploadDate字段在文件集合上使用索引。 这个索引允许高效地检索文件，如下例所示：</p>
<div class="cnblogs_code">
<pre>db.fs.files.find( { filename: myFileName } ).sort( { uploadDate: <span style="color: #800080;">1</span> } )</pre>
</div>
<p>如果此索引不存在，则可以发出以下操作以使用mongo shell创建它：</p>
<div class="cnblogs_code">
<pre>db.fs.files.createIndex( { filename: <span style="color: #800080;">1</span>, uploadDate: <span style="color: #800080;">1</span> } );</pre>
</div>
<p>6，使用mongofiles命令行工具上传文件</p>
<p>详细文档：<a href="https://docs.mongodb.com/manual/reference/program/mongofiles/#bin.mongofiles" target="_blank">https://docs.mongodb.com/manual/reference/program/mongofiles/#bin.mongofiles</a></p>
<p>所有mongofiles命令都具有以下形式：&nbsp;<span class="cnblogs_code">mongofiles &lt;options&gt; &lt;commands&gt; &lt;filename&gt;</span>&nbsp;</p>
<p>mongofiles命令的组件是:</p>
<ol class="arabic simple">
<li><a class="reference internal" href="https://docs.mongodb.com/manual/reference/program/mongofiles/#mongofiles-options">Options</a>.&nbsp;您可以使用一个或多个这些选项来控制mongofiles的行为</li>
<li><a class="reference internal" href="https://docs.mongodb.com/manual/reference/program/mongofiles/#mongofiles-commands">Commands</a>.&nbsp;使用这些命令之一来确定mongofiles的操作</li>
<li>一个文件名，它可以是：本地文件系统上的文件名称，也可以是GridFS对象.</li>
</ol>
<p>1)案例</p>
<p>① 上传文件</p>
<p>[root@localhost bin]# ./mongofiles -d test put ./sp.3gp</p>
<p>②查看test数据库</p>
<p>&nbsp;<img src="https://images2018.cnblogs.com/blog/741594/201803/741594-20180301232134568-1557348189.png" alt="" width="502" height="116" /></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a17"></a>十七、重量级聚合框架</span></strong></span></p>
<p>参考文档：<a href="https://docs.mongodb.com/manual/reference/method/db.collection.aggregate/#db.collection.aggregate" target="_blank">https://docs.mongodb.com/manual/reference/method/db.collection.aggregate/#db.collection.aggregate</a></p>
<p><span style="color: #ff0000; font-size: 12px;">注意：因为是管道执行，则需要注意执行顺序</span></p>
<p>1，使用方式：&nbsp;<span class="cnblogs_code">db.collection.aggregate(pipeline, options)&para;</span>&nbsp;</p>
<p>pipeline：管道</p>
<p>options：可选的。 aggregate()传递给聚合命令的其他选项。</p>
<p>管道：</p>
<table class="docutils" border="1"><colgroup><col width="29%" /><col width="71%" /></colgroup>
<thead valign="bottom">
<tr class="row-odd"><th class="head">Name</th><th class="head">Description</th></tr>
</thead>
<tbody valign="top">
<tr class="row-even">
<td><a class="reference internal" title="$addFields" href="https://docs.mongodb.com/manual/reference/operator/aggregation/addFields/#pipe._S_addFields"><code class="xref mongodb mongodb-pipeline docutils literal">$addFields</code></a></td>
<td>将新字段添加到文档。 输出包含输入文档和新添加字段中所有现有字段的文档。</td>
</tr>
<tr class="row-odd">
<td><a class="reference internal" title="$bucket" href="https://docs.mongodb.com/manual/reference/operator/aggregation/bucket/#pipe._S_bucket"><code class="xref mongodb mongodb-pipeline docutils literal">$bucket</code></a></td>
<td>根据指定的表达式和存储区边界将传入文档分组到称为存储桶的组中。</td>
</tr>
<tr class="row-even">
<td><a class="reference internal" title="$bucketAuto" href="https://docs.mongodb.com/manual/reference/operator/aggregation/bucketAuto/#pipe._S_bucketAuto"><code class="xref mongodb mongodb-pipeline docutils literal">$bucketAuto</code></a></td>
<td>根据指定的表达式将传入文档分类到特定数量的组（称为存储桶）。 桶边界自动确定，试图将文档均匀分布到指定数量的桶中。</td>
</tr>
<tr class="row-odd">
<td><a class="reference internal" title="$collStats" href="https://docs.mongodb.com/manual/reference/operator/aggregation/collStats/#pipe._S_collStats"><code class="xref mongodb mongodb-pipeline docutils literal">$collStats</code></a></td>
<td>返回有关集合或视图的统计信息。</td>
</tr>
<tr class="row-even">
<td><a class="reference internal" title="$count" href="https://docs.mongodb.com/manual/reference/operator/aggregation/count/#pipe._S_count"><code class="xref mongodb mongodb-pipeline docutils literal">$count</code></a></td>
<td>返回聚合管道此阶段的文档数量。</td>
</tr>
<tr class="row-odd">
<td><a class="reference internal" title="$currentOp" href="https://docs.mongodb.com/manual/reference/operator/aggregation/currentOp/#pipe._S_currentOp"><code class="xref mongodb mongodb-pipeline docutils literal">$currentOp</code></a></td>
<td>返回有关MongoDB部署的活动和/或休眠操作的信息。 要运行，请使用db.aggregate（）方法。</td>
</tr>
<tr class="row-even">
<td><a class="reference internal" title="$facet" href="https://docs.mongodb.com/manual/reference/operator/aggregation/facet/#pipe._S_facet"><code class="xref mongodb mongodb-pipeline docutils literal">$facet</code></a></td>
<td>在同一组输入文档中的单个阶段内处理多个聚合流水线。 支持创建多方面的聚合，能够在单个阶段中跨多个维度或方面表征数据。</td>
</tr>
<tr class="row-odd">
<td><a class="reference internal" title="$geoNear" href="https://docs.mongodb.com/manual/reference/operator/aggregation/geoNear/#pipe._S_geoNear"><code class="xref mongodb mongodb-pipeline docutils literal">$geoNear</code></a></td>
<td>根据地理空间点的接近度返回有序的文档流。 包含地理空间数据的$ match，$ sort和$ limit功能。 输出文件包含一个额外的距离字段，并可包含位置标识符字段。</td>
</tr>
<tr class="row-even">
<td><a class="reference internal" title="$graphLookup" href="https://docs.mongodb.com/manual/reference/operator/aggregation/graphLookup/#pipe._S_graphLookup"><code class="xref mongodb mongodb-pipeline docutils literal">$graphLookup</code></a></td>
<td>对集合执行递归搜索。 为每个输出文档添加一个新的数组字段，其中包含该文档的递归搜索的遍历结果。</td>
</tr>
<tr class="row-odd">
<td><a class="reference internal" title="$group" href="https://docs.mongodb.com/manual/reference/operator/aggregation/group/#pipe._S_group"><code class="xref mongodb mongodb-pipeline docutils literal">$group</code></a></td>
<td>分组计算</td>
</tr>
<tr class="row-even">
<td><a class="reference internal" title="$indexStats" href="https://docs.mongodb.com/manual/reference/operator/aggregation/indexStats/#pipe._S_indexStats"><code class="xref mongodb mongodb-pipeline docutils literal">$indexStats</code></a></td>
<td>查询过程中的索引情况</td>
</tr>
<tr class="row-odd">
<td><a class="reference internal" title="$limit" href="https://docs.mongodb.com/manual/reference/operator/aggregation/limit/#pipe._S_limit"><code class="xref mongodb mongodb-pipeline docutils literal">$limit</code></a></td>
<td>返回制指定数量的文档</td>
</tr>
<tr class="row-even">
<td><a class="reference internal" title="$listLocalSessions" href="https://docs.mongodb.com/manual/reference/operator/aggregation/listLocalSessions/#pipe._S_listLocalSessions"><code class="xref mongodb mongodb-pipeline docutils literal">$listLocalSessions</code></a></td>
<td>列出当前连接的mongos或mongodinstance上最近使用的所有活动会话。 这些会话可能尚未传播到system.sessions集合。</td>
</tr>
<tr class="row-odd">
<td><a class="reference internal" title="$listSessions" href="https://docs.mongodb.com/manual/reference/operator/aggregation/listSessions/#pipe._S_listSessions"><code class="xref mongodb mongodb-pipeline docutils literal">$listSessions</code></a></td>
<td>列出所有活动时间足以传播到system.sessions集合的所有会话。</td>
</tr>
<tr class="row-even">
<td><a class="reference internal" title="$lookup" href="https://docs.mongodb.com/manual/reference/operator/aggregation/lookup/#pipe._S_lookup"><code class="xref mongodb mongodb-pipeline docutils literal">$lookup</code></a></td>
<td>表连接</td>
</tr>
<tr class="row-odd">
<td><a class="reference internal" title="$match" href="https://docs.mongodb.com/manual/reference/operator/aggregation/match/#pipe._S_match"><code class="xref mongodb mongodb-pipeline docutils literal">$match</code></a></td>
<td>相当于我们的 where</td>
</tr>
<tr class="row-even">
<td><a class="reference internal" title="$out" href="https://docs.mongodb.com/manual/reference/operator/aggregation/out/#pipe._S_out"><code class="xref mongodb mongodb-pipeline docutils literal">$out</code></a></td>
<td>将最后的结果输出到指定的collection中去</td>
</tr>
<tr class="row-odd">
<td><a class="reference internal" title="$project" href="https://docs.mongodb.com/manual/reference/operator/aggregation/project/#pipe._S_project"><code class="xref mongodb mongodb-pipeline docutils literal">$project</code></a></td>
<td>相当于我们sql操作的 select</td>
</tr>
<tr class="row-even">
<td><a class="reference internal" title="$redact" href="https://docs.mongodb.com/manual/reference/operator/aggregation/redact/#pipe._S_redact"><code class="xref mongodb mongodb-pipeline docutils literal">$redact</code></a></td>
<td>根据存储在文档本身中的信息限制每个文档的内容，重新整形流中的每个文档。 包含$ project和$ match的功能。 可用于实施字段级别的编校。 对于每个输入文档，输出一个或零个文档。</td>
</tr>
<tr class="row-odd">
<td><a class="reference internal" title="$replaceRoot" href="https://docs.mongodb.com/manual/reference/operator/aggregation/replaceRoot/#pipe._S_replaceRoot"><code class="xref mongodb mongodb-pipeline docutils literal">$replaceRoot</code></a></td>
<td>用指定的嵌入式文档替换文档。 该操作将替换输入文档中的所有现有字段，包括_id字段。 指定嵌入在输入文档中的文档以将嵌入式文档提升到顶层。</td>
</tr>
<tr class="row-even">
<td><a class="reference internal" title="$sample" href="https://docs.mongodb.com/manual/reference/operator/aggregation/sample/#pipe._S_sample"><code class="xref mongodb mongodb-pipeline docutils literal">$sample</code></a></td>
<td>从其输入中随机选择指定数量的文档。</td>
</tr>
<tr class="row-odd">
<td><a class="reference internal" title="$skip" href="https://docs.mongodb.com/manual/reference/operator/aggregation/skip/#pipe._S_skip"><code class="xref mongodb mongodb-pipeline docutils literal">$skip</code></a></td>
<td>跳过前n个文档</td>
</tr>
<tr class="row-even">
<td><a class="reference internal" title="$sort" href="https://docs.mongodb.com/manual/reference/operator/aggregation/sort/#pipe._S_sort"><code class="xref mongodb mongodb-pipeline docutils literal">$sort</code></a></td>
<td>通过指定的排序键对文档流进行重新排序。 只有订单改变了; 文件保持不变。 对于每个输入文档，输出一个文档。</td>
</tr>
<tr class="row-odd">
<td><a class="reference internal" title="$sortByCount" href="https://docs.mongodb.com/manual/reference/operator/aggregation/sortByCount/#pipe._S_sortByCount"><code class="xref mongodb mongodb-pipeline docutils literal">$sortByCount</code></a></td>
<td>根据指定表达式的值对传入文档分组，然后计算每个不同组中文档的数量。</td>
</tr>
<tr class="row-even">
<td><a class="reference internal" title="$unwind" href="https://docs.mongodb.com/manual/reference/operator/aggregation/unwind/#pipe._S_unwind"><code class="xref mongodb mongodb-pipeline docutils literal">$unwind</code></a></td>
<td>将数据拆解成每一个document</td>
</tr>
</tbody>
</table>
<p>2，案例</p>
<p>①分组并计算amount的总和</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('baace333-3cdc-4f06-93a4-2c07eb07fafb')"><img id="code_img_closed_baace333-3cdc-4f06-93a4-2c07eb07fafb" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_baace333-3cdc-4f06-93a4-2c07eb07fafb" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('baace333-3cdc-4f06-93a4-2c07eb07fafb',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_baace333-3cdc-4f06-93a4-2c07eb07fafb" class="cnblogs_code_hide">
<pre>{ _id: <span style="color: #800080;">1</span>, cust_id: <span style="color: #800000;">"</span><span style="color: #800000;">abc1</span><span style="color: #800000;">"</span>, ord_date: ISODate(<span style="color: #800000;">"</span><span style="color: #800000;">2012-11-02T17:04:11.102Z</span><span style="color: #800000;">"</span>), status: <span style="color: #800000;">"</span><span style="color: #800000;">A</span><span style="color: #800000;">"</span>, amount: <span style="color: #800080;">50</span><span style="color: #000000;"> }
{ _id: </span><span style="color: #800080;">2</span>, cust_id: <span style="color: #800000;">"</span><span style="color: #800000;">xyz1</span><span style="color: #800000;">"</span>, ord_date: ISODate(<span style="color: #800000;">"</span><span style="color: #800000;">2013-10-01T17:04:11.102Z</span><span style="color: #800000;">"</span>), status: <span style="color: #800000;">"</span><span style="color: #800000;">A</span><span style="color: #800000;">"</span>, amount: <span style="color: #800080;">100</span><span style="color: #000000;"> }
{ _id: </span><span style="color: #800080;">3</span>, cust_id: <span style="color: #800000;">"</span><span style="color: #800000;">xyz1</span><span style="color: #800000;">"</span>, ord_date: ISODate(<span style="color: #800000;">"</span><span style="color: #800000;">2013-10-12T17:04:11.102Z</span><span style="color: #800000;">"</span>), status: <span style="color: #800000;">"</span><span style="color: #800000;">D</span><span style="color: #800000;">"</span>, amount: <span style="color: #800080;">25</span><span style="color: #000000;"> }
{ _id: </span><span style="color: #800080;">4</span>, cust_id: <span style="color: #800000;">"</span><span style="color: #800000;">xyz1</span><span style="color: #800000;">"</span>, ord_date: ISODate(<span style="color: #800000;">"</span><span style="color: #800000;">2013-10-11T17:04:11.102Z</span><span style="color: #800000;">"</span>), status: <span style="color: #800000;">"</span><span style="color: #800000;">D</span><span style="color: #800000;">"</span>, amount: <span style="color: #800080;">125</span><span style="color: #000000;"> }
{ _id: </span><span style="color: #800080;">5</span>, cust_id: <span style="color: #800000;">"</span><span style="color: #800000;">abc1</span><span style="color: #800000;">"</span>, ord_date: ISODate(<span style="color: #800000;">"</span><span style="color: #800000;">2013-11-12T17:04:11.102Z</span><span style="color: #800000;">"</span>), status: <span style="color: #800000;">"</span><span style="color: #800000;">A</span><span style="color: #800000;">"</span>, amount: <span style="color: #800080;">25</span> }</pre>
</div>
<span class="cnblogs_code_collapse">orders 数据</span></div>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.orders.aggregate([
    {$match:{status:</span><span style="color: #800000;">"</span><span style="color: #800000;">A</span><span style="color: #800000;">"</span><span style="color: #000000;">}},
    {$group:{_id:</span><span style="color: #800000;">"</span><span style="color: #800000;">$cust_id</span><span style="color: #800000;">"</span>,total:{$sum:<span style="color: #800000;">"</span><span style="color: #800000;">$amount</span><span style="color: #800000;">"</span><span style="color: #000000;">}}},
    {$sort:{total:</span>-<span style="color: #800080;">1</span><span style="color: #000000;">}}
    ])</span></pre>
</div>
<p>②返回①的执行计划</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.orders.aggregate([
    {$match:{status:</span><span style="color: #800000;">"</span><span style="color: #800000;">A</span><span style="color: #800000;">"</span><span style="color: #000000;">}},
    {$group:{_id:</span><span style="color: #800000;">"</span><span style="color: #800000;">$cust_id</span><span style="color: #800000;">"</span>,total:{$sum:<span style="color: #800000;">"</span><span style="color: #800000;">$amount</span><span style="color: #800000;">"</span><span style="color: #000000;">}}},
    {$sort:{total:</span>-<span style="color: #800080;">1</span><span style="color: #000000;">}}
    ],
    {
        explain:</span><span style="color: #0000ff;">true</span><span style="color: #000000;">
     }
     )</span></pre>
</div>
<p>③分页</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.orders.aggregate([
    {$match:{status:</span><span style="color: #800000;">"</span><span style="color: #800000;">A</span><span style="color: #800000;">"</span><span style="color: #000000;">}},
    {$group:{_id:</span><span style="color: #800000;">"</span><span style="color: #800000;">$cust_id</span><span style="color: #800000;">"</span>,total:{$sum:<span style="color: #800000;">"</span><span style="color: #800000;">$amount</span><span style="color: #800000;">"</span><span style="color: #000000;">}}},
    {$sort:{total:</span>-<span style="color: #800080;">1</span><span style="color: #000000;">}},
    {$skip:</span><span style="color: #800080;">1</span>},<span style="color: #008000;">//</span><span style="color: #008000;">跳过一条</span>
    {$limit:<span style="color: #800080;">2</span>}<span style="color: #008000;">//</span><span style="color: #008000;">返回两条数据</span>
    ])</pre>
</div>
<div class="cnblogs_code">
<pre>db.orders.find().skip(<span style="color: #800080;">0</span>).limit(<span style="color: #800080;">10</span>)//普通分页</pre>
</div>
<p>③表连接</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('04eb5c58-640a-4fd7-b385-445d2d8b6270')"><img id="code_img_closed_04eb5c58-640a-4fd7-b385-445d2d8b6270" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_04eb5c58-640a-4fd7-b385-445d2d8b6270" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('04eb5c58-640a-4fd7-b385-445d2d8b6270',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_04eb5c58-640a-4fd7-b385-445d2d8b6270" class="cnblogs_code_hide">
<pre><span style="color: #000000;">db.orders.insert([
   { </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">1</span>, <span style="color: #800000;">"</span><span style="color: #800000;">item</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">almonds</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">price</span><span style="color: #800000;">"</span> : <span style="color: #800080;">12</span>, <span style="color: #800000;">"</span><span style="color: #800000;">quantity</span><span style="color: #800000;">"</span> : <span style="color: #800080;">2</span><span style="color: #000000;"> },
   { </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">2</span>, <span style="color: #800000;">"</span><span style="color: #800000;">item</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">pecans</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">price</span><span style="color: #800000;">"</span> : <span style="color: #800080;">20</span>, <span style="color: #800000;">"</span><span style="color: #800000;">quantity</span><span style="color: #800000;">"</span> : <span style="color: #800080;">1</span><span style="color: #000000;"> },
   { </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">3</span><span style="color: #000000;">  }
])
db.inventory.insert([
   { </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">1</span>, <span style="color: #800000;">"</span><span style="color: #800000;">sku</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">almonds</span><span style="color: #800000;">"</span>, description: <span style="color: #800000;">"</span><span style="color: #800000;">product 1</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">instock</span><span style="color: #800000;">"</span> : <span style="color: #800080;">120</span><span style="color: #000000;"> },
   { </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">2</span>, <span style="color: #800000;">"</span><span style="color: #800000;">sku</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">bread</span><span style="color: #800000;">"</span>, description: <span style="color: #800000;">"</span><span style="color: #800000;">product 2</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">instock</span><span style="color: #800000;">"</span> : <span style="color: #800080;">80</span><span style="color: #000000;"> },
   { </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">3</span>, <span style="color: #800000;">"</span><span style="color: #800000;">sku</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">cashews</span><span style="color: #800000;">"</span>, description: <span style="color: #800000;">"</span><span style="color: #800000;">product 3</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">instock</span><span style="color: #800000;">"</span> : <span style="color: #800080;">60</span><span style="color: #000000;"> },
   { </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">4</span>, <span style="color: #800000;">"</span><span style="color: #800000;">sku</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">pecans</span><span style="color: #800000;">"</span>, description: <span style="color: #800000;">"</span><span style="color: #800000;">product 4</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">instock</span><span style="color: #800000;">"</span> : <span style="color: #800080;">70</span><span style="color: #000000;"> },
   { </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">5</span>, <span style="color: #800000;">"</span><span style="color: #800000;">sku</span><span style="color: #800000;">"</span>: <span style="color: #0000ff;">null</span>, description: <span style="color: #800000;">"</span><span style="color: #800000;">Incomplete</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
   { </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">6</span><span style="color: #000000;"> }
])</span></pre>
</div>
<span class="cnblogs_code_collapse">数据</span></div>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.orders.aggregate([
    {
        $lookup:{
            </span><span style="color: #0000ff;">from</span>:<span style="color: #800000;">"</span><span style="color: #800000;">inventory</span><span style="color: #800000;">"</span><span style="color: #000000;">,
            localField:</span><span style="color: #800000;">"</span><span style="color: #800000;">item</span><span style="color: #800000;">"</span><span style="color: #000000;">,
            foreignField:</span><span style="color: #800000;">"</span><span style="color: #800000;">sku</span><span style="color: #800000;">"</span><span style="color: #000000;">,
            </span><span style="color: #0000ff;">as</span>:<span style="color: #800000;">"</span><span style="color: #800000;">inventory_docs</span><span style="color: #800000;">"</span><span style="color: #000000;">
        }
    }
])</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a18"></a>十八、轻量级聚合框架group</span></strong></p>
<p>详细文档：<a href="https://docs.mongodb.com/manual/reference/command/group/" target="_blank">https://docs.mongodb.com/manual/reference/command/group/</a></p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201803/741594-20180305200508063-1420367183.png" alt="" width="507" height="358" /></p>
<p>使用方法：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">{
  group:
   {
     ns: </span>&lt;<span style="color: #0000ff;">namespace</span>&gt;<span style="color: #000000;">,
     key: </span>&lt;key&gt;<span style="color: #000000;">,
     $reduce: </span>&lt;reduce function&gt;<span style="color: #000000;">,
     $keyf: </span>&lt;key function&gt;<span style="color: #000000;">,
     cond: </span>&lt;query&gt;<span style="color: #000000;">,
     finalize: </span>&lt;finalize function&gt;<span style="color: #000000;">
   }
}</span></pre>
</div>
<p>ns：collections 你group的集合。。。</p>
<p>key: 我们group的键值。。</p>
<p>$keyf: 采用函数的定义我们的key， 我们可以后更高的灵活性来定义(去string的最后一个字母，或者中间，或者最后)</p>
<p>$reduce: 刚好就是我们聚合进行中的每个操作。。。</p>
<p>$initial: 聚合的初始文档。。。</p>
<p>cond: ($match) where条件</p>
<p>finalize: 在某一个groupkey结束后插入点。。。。</p>
<p>1，案例：</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('d5b3362f-28d7-441b-9fcb-926114a6128d')"><img id="code_img_closed_d5b3362f-28d7-441b-9fcb-926114a6128d" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_d5b3362f-28d7-441b-9fcb-926114a6128d" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('d5b3362f-28d7-441b-9fcb-926114a6128d',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_d5b3362f-28d7-441b-9fcb-926114a6128d" class="cnblogs_code_hide">
<pre><span style="color: #000000;">{
    </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">1</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">sku</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">abc</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">description</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">product 1</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">instock</span><span style="color: #800000;">"</span> : <span style="color: #800080;">120</span><span style="color: #000000;">
}
{
    </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">2</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">sku</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">def</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">description</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">product 2</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">instock</span><span style="color: #800000;">"</span> : <span style="color: #800080;">80</span><span style="color: #000000;">
}
{
    </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">3</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">sku</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">ijk</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">description</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">product 3</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">instock</span><span style="color: #800000;">"</span> : <span style="color: #800080;">60</span><span style="color: #000000;">
}
{
    </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">4</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">sku</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">jkl</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">description</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">product 4</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">instock</span><span style="color: #800000;">"</span> : <span style="color: #800080;">70</span><span style="color: #000000;">
}
{
    </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">5</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">sku</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">abcedfe</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">description</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">product 1</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">instock</span><span style="color: #800000;">"</span> : <span style="color: #800080;">120</span><span style="color: #000000;">
}

{
    </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span> : <span style="color: #800080;">6</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">sku</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">def而微软为</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">description</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">product 2</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">instock</span><span style="color: #800000;">"</span> : <span style="color: #800080;">70</span><span style="color: #000000;">
}</span></pre>
</div>
<span class="cnblogs_code_collapse">数据</span></div>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.runCommand(
   {
     group:
       {
         ns: </span><span style="color: #800000;">'</span><span style="color: #800000;">test</span><span style="color: #800000;">'</span><span style="color: #000000;">,
         key: { </span><span style="color: #800000;">"</span><span style="color: #800000;">description</span><span style="color: #800000;">"</span>:<span style="color: #800080;">1</span> },   <span style="color: #008000;">//</span><span style="color: #008000;">分组的key</span>
         cond: { <span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span>:{$gt:<span style="color: #800080;">1</span>} },    <span style="color: #008000;">//</span><span style="color: #008000;">筛选条件</span>
<span style="color: #000000;">         $reduce: function ( curr, result ) {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">curr:   当前当前得到的document
            </span><span style="color: #008000;">//</span><span style="color: #008000;">result: 第一次就是我们目前的initial，后续的话看你怎么对result进行操作</span>
                   result.count++<span style="color: #000000;">;
            </span><span style="color: #0000ff;">return</span> result.total+=<span style="color: #000000;">curr.instock;
         },
         initial: {</span><span style="color: #800000;">"</span><span style="color: #800000;">total</span><span style="color: #800000;">"</span>:<span style="color: #800080;">0</span>,<span style="color: #800000;">"</span><span style="color: #800000;">count</span><span style="color: #800000;">"</span>:<span style="color: #800080;">0</span> },  <span style="color: #008000;">//</span><span style="color: #008000;">初始化文档</span>
         finalize:function(result){     <span style="color: #008000;">//</span><span style="color: #008000;">结束执行</span>
            result.avg=result.total/<span style="color: #000000;">result.count;
         }
       }
   }
)


db.runCommand(
   {
     group:
       {
         ns: </span><span style="color: #800000;">'</span><span style="color: #800000;">test</span><span style="color: #800000;">'</span><span style="color: #000000;">,
        </span><span style="color: #008000;">//</span><span style="color: #008000;">key: { "description":1 },   </span><span style="color: #008000;">//</span><span style="color: #008000;">分组的key</span>
<span style="color: #000000;">         $keyf:function(doc){
             </span><span style="color: #0000ff;">return</span> {<span style="color: #800000;">"</span><span style="color: #800000;">description</span><span style="color: #800000;">"</span>:<span style="color: #800080;">1</span>}      <span style="color: #008000;">//</span><span style="color: #008000;">doc: 当前的文档</span>
<span style="color: #000000;">          },
         cond: { </span><span style="color: #800000;">"</span><span style="color: #800000;">_id</span><span style="color: #800000;">"</span>:{$gt:<span style="color: #800080;">1</span><span style="color: #000000;">} },
         $reduce: function ( curr, result ) {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">curr:   当前当前得到的document
            </span><span style="color: #008000;">//</span><span style="color: #008000;">result: 第一次就是我们目前的initial，后续的话看你怎么对result进行操作</span>
                   result.count++<span style="color: #000000;">;
            </span><span style="color: #0000ff;">return</span> result.total+=<span style="color: #000000;">curr.instock;
         },
         initial: {</span><span style="color: #800000;">"</span><span style="color: #800000;">total</span><span style="color: #800000;">"</span>:<span style="color: #800080;">0</span>,<span style="color: #800000;">"</span><span style="color: #800000;">count</span><span style="color: #800000;">"</span>:<span style="color: #800080;">0</span><span style="color: #000000;"> },
         finalize:function(result){
            result.avg</span>=result.total/<span style="color: #000000;">result.count;
         }
       }
   }
)</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a19"></a>十九、distinct</span></strong></p>
<p>参考文档：<a href="https://docs.mongodb.com/manual/reference/command/distinct/" target="_blank">https://docs.mongodb.com/manual/reference/command/distinct/</a></p>
<p>使用方法：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">{
  distinct: </span><span style="color: #800000;">"</span><span style="color: #800000;">&lt;collection&gt;</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  key: </span><span style="color: #800000;">"</span><span style="color: #800000;">&lt;field&gt;</span><span style="color: #800000;">"</span><span style="color: #000000;">,
  query: </span>&lt;query&gt;<span style="color: #000000;">,
  readConcern: </span>&lt;read concern document&gt;<span style="color: #000000;">,
  collation: </span>&lt;collation document&gt;<span style="color: #000000;">
}</span></pre>
</div>
<p>案例：&nbsp;<span class="cnblogs_code">db.runCommand ( { distinct: <span style="color: #800000;">"</span><span style="color: #800000;">test</span><span style="color: #800000;">"</span>, key: <span style="color: #800000;">"</span><span style="color: #800000;">description</span><span style="color: #800000;">"</span> } )</span>&nbsp;</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a20"></a>二十、mapReduce</span></strong></p>
<p>参考文档：<a href="https://docs.mongodb.com/manual/reference/method/db.collection.mapReduce/index.html" target="_blank">https://docs.mongodb.com/manual/reference/method/db.collection.mapReduce/index.html</a></p>
<p>使用方法：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">db.collection.mapReduce(
                         </span>&lt;map&gt;<span style="color: #000000;">,
                         </span>&lt;reduce&gt;<span style="color: #000000;">,
                         {
                           </span><span style="color: #0000ff;">out</span>: &lt;collection&gt;<span style="color: #000000;">,
                           query: </span>&lt;document&gt;<span style="color: #000000;">,
                           sort: </span>&lt;document&gt;<span style="color: #000000;">,
                           limit: </span>&lt;number&gt;<span style="color: #000000;">,
                           finalize: </span>&lt;function&gt;<span style="color: #000000;">,
                           scope: </span>&lt;document&gt;<span style="color: #000000;">,
                           jsMode: </span>&lt;boolean&gt;<span style="color: #000000;">,
                           verbose: </span>&lt;boolean&gt;<span style="color: #000000;">,
                           bypassDocumentValidation: </span>&lt;boolean&gt;<span style="color: #000000;">
                         }
                       )</span></pre>
</div>
<table class="colwidths-given docutils" border="1">
<thead valign="bottom">
<tr class="row-odd"><th class="head">Parameter</th><th class="head">Type</th><th class="head">Description</th></tr>
</thead>
<tbody valign="top">
<tr class="row-even">
<td><code class="docutils literal">map</code></td>
<td>function</td>
<td>
<p class="first">一个JavaScript函数，该函数将一个值与一个键关联或&ldquo;映射&rdquo;，并发出键和值对。</p>
</td>
</tr>
<tr class="row-odd">
<td><code class="docutils literal">reduce</code></td>
<td>function</td>
<td>
<p class="first">一个JavaScript函数，它&ldquo;减少&rdquo;到一个对象，所有的值都与一个特定的键相关联。</p>
</td>
</tr>
<tr class="row-even">
<td><code class="docutils literal">options</code></td>
<td>document</td>
<td>其他参数选项</td>
</tr>
<tr class="row-odd">
<td><code class="docutils literal">bypassDocumentValidation</code></td>
<td>boolean</td>
<td>
<p class="first">可选的。允许mapReduce在操作过程中绕过文档验证。这允许您插入不符合验证要求的文档。</p>
</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<table class="colwidths-given docutils" border="1">
<thead valign="bottom">
<tr class="row-odd"><th class="head">Field</th><th class="head">Type</th><th class="head">Description</th></tr>
</thead>
<tbody valign="top">
<tr class="row-even">
<td><code class="docutils literal">out</code></td>
<td>string or document</td>
<td>
<p class="first">指定map-reduce操作结果的位置。您可以输出到一个集合，输出到一个具有动作的集合，或者内联（inline）输出。在对集合的主要成员执行map-reduce操作时，可以输出到集合;对于次要成员，您可能只使用内联（inline）输出。</p>
</td>
</tr>
<tr class="row-odd">
<td><code class="docutils literal">query</code></td>
<td>document</td>
<td>条件</td>
</tr>
<tr class="row-even">
<td><code class="docutils literal">sort</code></td>
<td>document</td>
<td>排序</td>
</tr>
<tr class="row-odd">
<td><code class="docutils literal">limit</code></td>
<td>number</td>
<td>指定输入到map函数的最大文档数。</td>
</tr>
<tr class="row-even">
<td><code class="docutils literal">finalize</code></td>
<td>function</td>
<td>
<p class="first"><span style="font-size: 10px;">可选的。遵循reduce方法并修改输出</span></p>
</td>
</tr>
<tr class="row-odd">
<td><code class="docutils literal">scope</code></td>
<td>document</td>
<td>指定在映射中可访问的全局变量，减少和确定函数。</td>
</tr>
<tr class="row-even">
<td><code class="docutils literal">jsMode</code></td>
<td>boolean</td>
<td>
<p>指定是否将中间数据转换为BSON格式，以执行映射和reduce函数。<br />默认值为false。</p>
<p>If&nbsp;<code class="docutils literal">false</code>:</p>
<ul class="simple">
<li>在内部，MongoDB将映射函数发出的JavaScript对象转换为BSON对象。当调用reduce函数时，这些BSON对象被转换回JavaScript对象。</li>
<li>map-reduce操作将中间的BSON对象放在临时的磁盘存储中。这允许map-reduce操作执行任意大的数据集。</li>






















</ul>
<p>If&nbsp;<code class="docutils literal">true</code>:</p>
<ul class="last simple">
<li>在内部，map函数中发出的JavaScript对象仍然是JavaScript对象。不需要将对象转换为reduce函数，这会导致更快的执行。</li>
<li>您只能使用少于500,000个不同关键参数的jsMode来获得mapper的emit()函数。</li>






















</ul>






















</td>






















</tr>
<tr class="row-odd">
<td><code class="docutils literal">verbose</code></td>
<td>boolean</td>
<td>
<p>指定是否在结果信息中包含计时信息。将verbose设置为true，以包含计时信息。<br />默认值为false。</p>






















</td>






















</tr>
<tr class="row-even">
<td><code class="docutils literal">collation</code></td>
<td>document</td>
<td>
<p>可选的。<br />指定用于操作的排序规则。<br />Collation允许用户为字符串比较指定特定于语言的规则，比如字母大小写和重音符号的规则。<br />collation选项有以下语法:</p>
<div class="button-code-block">
<div class="copyable-code-block highlight-javascript">
<div class="highlight">
<pre><span class="nx">collation<span class="o">: <span class="p">{
   <span class="nx">locale<span class="o">: <span class="o">&lt;<span class="nx">string<span class="o">&gt;<span class="p">,
   <span class="nx">caseLevel<span class="o">: <span class="o">&lt;<span class="kr">boolean<span class="o">&gt;<span class="p">,
   <span class="nx">caseFirst<span class="o">: <span class="o">&lt;<span class="nx">string<span class="o">&gt;<span class="p">,
   <span class="nx">strength<span class="o">: <span class="o">&lt;<span class="kr">int<span class="o">&gt;<span class="p">,
   <span class="nx">numericOrdering<span class="o">: <span class="o">&lt;<span class="kr">boolean<span class="o">&gt;<span class="p">,
   <span class="nx">alternate<span class="o">: <span class="o">&lt;<span class="nx">string<span class="o">&gt;<span class="p">,
   <span class="nx">maxVariable<span class="o">: <span class="o">&lt;<span class="nx">string<span class="o">&gt;<span class="p">,
   <span class="nx">backwards<span class="o">: <span class="o">&lt;<span class="kr">boolean<span class="o">&gt;
<span class="p">}
</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></pre>
</div>
</div>
</div>
<p>在指定排序时，locale字段是强制的;所有其他排序字段都是可选的。有关字段的描述，请参见Collation文档。</p>
<p>如果排序未指定，但是集合有默认的排序规则(请参阅db.createCollection())，该操作将使用指定的排序集。<br />如果没有为集合或操作指定排序，MongoDB将使用以前版本中用于字符串比较的简单二进制比较。<br />不能为操作指定多个排序。例如，您不能指定每个字段的不同排序，或者如果使用排序来执行查找，您不能使用一个排序来查找，而另一个排序。<br />新的3.4版本中。</p>






















</td>






















</tr>






















</tbody>






















</table>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a21"></a>二十一、master-slave</span></strong></span></p>
<p>详细文档：<a href="https://docs.mongodb.com/manual/core/master-slave/" target="_blank">https://docs.mongodb.com/manual/core/master-slave/</a></p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201803/741594-20180317154925700-1082351645.png" alt="" /></p>
<p>1，基础搭建</p>
<p>①复制mongod程序到27000文件夹</p>
<p>②创建配置文件（1.config）</p>
<p>③创建db存储文件夹</p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201803/741594-20180317155136159-1474230565.png" alt="" width="251" height="87" /></p>
<p>2，配置master config</p>
<div class="cnblogs_code">
<pre>port=<span style="color: #800080;">27000</span><span style="color: #000000;">
bind_ip</span>=<span style="color: #800080;">192.168</span>.<span style="color: #800080;">1.150</span><span style="color: #000000;">
dbpath</span>=./<span style="color: #000000;">db
master</span>=<span style="color: #0000ff;">true</span></pre>
</div>
<p>启动mongodb：&nbsp;<span class="cnblogs_code">./mongod --config <span style="color: #800080;">1</span>.config</span>&nbsp;</p>
<p>3，配置slave config</p>
<div class="cnblogs_code">
<pre>port=<span style="color: #800080;">27001</span><span style="color: #000000;">
bind_ip</span>=<span style="color: #800080;">192.168</span>.<span style="color: #800080;">1.150</span><span style="color: #000000;">
dbpath</span>=./<span style="color: #000000;">db
slave</span>=<span style="color: #0000ff;">true</span><span style="color: #000000;">
source</span>=<span style="color: #800080;">192.168</span>.<span style="color: #800080;">1.150</span>:<span style="color: #800080;">27000</span></pre>
</div>
<p>启动mongodb：&nbsp;<span class="cnblogs_code">./mongod --config&nbsp;1.config&nbsp;</span></p>
<p>4，其他配置项</p>
<p>only:可选的。 指定数据库的名称。 指定时，MongoDB将只复制指定的数据库。&nbsp;</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a22"></a>二十二、ReplicaSet集群</span></strong></span></p>
<p>master挂掉其中一个secondary变为master</p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201803/741594-20180317190642362-1283190563.png" alt="" /></p>
<p>&nbsp;</p>
<p>arbiter：仲裁者没有数据集的副本，也不能成为主数据集。 副本组可能会有仲裁者在选举主要增加一票。 仲裁者总是恰好1选投票，从而让副本集有奇数表决权的成员</p>
<p>1，配置</p>
<div class="cnblogs_code">
<pre>port=<span style="color: #800080;">27000</span><span style="color: #000000;"> 
bind_ip</span>=<span style="color: #800080;">192.168</span>.<span style="color: #800080;">1.150</span><span style="color: #000000;">
dbpath</span>=./<span style="color: #000000;">db
replSet</span>=test</pre>
</div>
<p>27001、27002、27003配置文件差不多</p>
<p>2，启动服务</p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201803/741594-20180318161720427-527439423.png" alt="" width="416" height="146" /></p>
<div class="cnblogs_code">
<pre>./mongod --config <span style="color: #800080;">1</span>.config</pre>
</div>
<p>3，随便链接一台mongodb（例如链接192.168.1.150：27000）</p>
<p>添加集群</p>
<div class="cnblogs_code">
<pre>rs.initiate()<span style="color: #008000;">//</span><span style="color: #008000;">初始化ReplicaSet集群</span>
<span style="color: #000000;">
rs.config()</span><span style="color: #008000;">//</span><span style="color: #008000;">查看配置信息</span>
<span style="color: #000000;">
rs.status()</span><span style="color: #008000;">//</span><span style="color: #008000;">查看状态

</span><span style="color: #008000;">//</span><span style="color: #008000;">向集群中添加members</span>
rs.add(<span style="color: #800000;">"</span><span style="color: #800000;">192.168.1.150:27001</span><span style="color: #800000;">"</span><span style="color: #000000;">)
rs.add(</span><span style="color: #800000;">"</span><span style="color: #800000;">192.168.1.150:27002</span><span style="color: #800000;">"</span><span style="color: #000000;">)

</span><span style="color: #008000;">//</span><span style="color: #008000;">添加仲裁</span>
rs.addArb(<span style="color: #800000;">"</span><span style="color: #800000;">192.168.1.150:27003</span><span style="color: #800000;">"</span>)</pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a23"></a>二十三、mongodb分片（未完成）</span></strong></p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201803/741594-20180318164614334-1313475372.png" alt="" /></p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201803/741594-20180318164856641-1072125966.png" alt="" width="446" height="110" /></p>
<p>1，配置</p>
<p>27000（mongos）：</p>
<div class="cnblogs_code">
<pre>port=<span style="color: #800080;">27000</span><span style="color: #000000;">
bind_ip</span>=<span style="color: #800080;">192.168</span>.<span style="color: #800080;">1.150</span><span style="color: #000000;">
configdb</span>=<span style="color: #800080;">192.168</span>.<span style="color: #800080;">1.150</span>:<span style="color: #800080;">27001</span></pre>
</div>
<p>27001（config）：</p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201803/741594-20180318172213800-535606639.png" alt="" width="315" height="121" /></p>
<div class="cnblogs_code">
<pre>port=<span style="color: #800080;">27001</span><span style="color: #000000;">
bind_ip</span>=<span style="color: #800080;">192.168</span>.<span style="color: #800080;">1.150</span><span style="color: #000000;">
dbpath</span>=./<span style="color: #000000;">db
configsvr</span>=<span style="color: #0000ff;">true</span></pre>
</div>
<p>启动：&nbsp;<span class="cnblogs_code">./mongod --config <span style="color: #800080;">1</span>.config</span>&nbsp;</p>
<p>27002：</p>
<p>27003：</p>
<p>3，步骤</p>
<p>①开启config服务器</p>
<p>②开启mongos服务器</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a24"></a>二十四、驱动链接mongodb</span></strong></span></p>
<p>参考文档：<a href="http://mongodb.github.io/mongo-csharp-driver/2.2/getting_started/?jmp=docs&amp;_ga=2.64367849.778289673.1521255001-1734184491.1516893909" target="_blank">http://mongodb.github.io/mongo-csharp-driver/2.2/getting_started/?jmp=docs&amp;_ga=2.64367849.778289673.1521255001-1734184491.1516893909</a></p>
<p>nuget：MongoDB.Driver</p>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> or use a connection string</span>
            <span style="color: #0000ff;">var</span> client = <span style="color: #0000ff;">new</span> MongoClient(<span style="color: #800000;">"</span><span style="color: #800000;">mongodb://192.168.1.150:27017</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            </span><span style="color: #0000ff;">var</span> db = client.GetDatabase(<span style="color: #800000;">"</span><span style="color: #800000;">test</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            db.CreateCollection(</span><span style="color: #800000;">"</span><span style="color: #800000;">aa</span><span style="color: #800000;">"</span><span style="color: #000000;">);

        }
    }</span></pre>
</div>
<p>&nbsp;</p>