<p>本案例测试es版本等环境下载：链接: <a href="https://pan.baidu.com/s/1txx_TxE-bTYwqQEBKxtMKQ" target="_blank">https://pan.baidu.com/s/1txx_TxE-bTYwqQEBKxtMKQ</a> 提取码: xrrh</p>
<p>官网下载&nbsp;<a href="https://www.elastic.co/cn/downloads/elasticsearch%20" target="_blank">https://www.elastic.co/cn/downloads/elasticsearch&nbsp;</a></p>
<p style="font-size: 18pt; background-color: #169fe6;"><span style="color: #ffffff;"><strong>一、准备环境</strong></span></p>
<p>es需要有java环境，安装Java环境</p>
<p>1.先查看本地是否自带java环境：&nbsp;<span class="cnblogs_code">yum list installed |grep java</span>&nbsp;</p>
<p>2.卸载自带的java（输入su，输入root超级管理员的密码，切换到root用户模式）</p>
<p>&nbsp;<span class="cnblogs_code">yum -y remove java-*</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">yum -y remove tzdata-java*</span>&nbsp;</p>
<p>3，查看java包：&nbsp;<span class="cnblogs_code">yum -y list java*</span>&nbsp;</p>
<p>安装java：&nbsp;<span class="cnblogs_code">yum -y install java-<span style="color: #800080;">11</span>-openjdk*</span>&nbsp;</p>
<p>4，查找Java安装路径</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">which java

ls </span>-lrt /usr/bin/<span style="color: #000000;">java（也就是上一步查询出来的路径），然后回车

输入ls </span>-lrt /etc/alternatives/<span style="color: #000000;">java（也就是上一步查询出来的路径），然后回车

从路径中可以看到在jvm目录下，输入cd </span>/usr/lib/<span style="color: #000000;">jvm，跳转到jvm的目录

输入ls 列出当前目录下的文件和文件夹</span></pre>
</div>
<p>5，配置Java环境变量</p>
<div class="cnblogs_code">
<pre>输入vi /etc/profile去编辑环境变量</pre>
</div>
<p>添加如下：</p>
<div class="cnblogs_code">
<pre>export JAVA_HOME=/usr/lib/jvm/java-<span style="color: #800080;">1.8</span>.<span style="color: #800080;">0</span><span style="color: #000000;">
export JRE_HOME</span>=$JAVA_HOME/<span style="color: #000000;">jre  
export PATH</span>=$PATH:$JAVA_HOME/bin:$JRE_HOME/<span style="color: #000000;">bin
export CLASSPATH</span>=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib</pre>
</div>
<p>保存退出</p>
<p>输入source /etc/profile，使配置立即生效</p>
<p>7. 检查Java安装和配置情况 输入java -version，然后回车</p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: #169fe6;"><span style="color: #ffffff;"><strong>二、目录结构</strong></span></p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202004/741594-20200405171734298-1664180528.png" alt="" width="610" height="322" /></p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: #169fe6;"><span style="color: #ffffff;"><strong>三、启动</strong></span></p>
<p>elasticsearch不允许使用root启动，因此我们要解决这个问题需要新建一个用户来启动elasticsearch</p>
<p>&nbsp;启动：&nbsp;<span class="cnblogs_code">[hunter@localhost elasticsearch-<span style="color: #800080;">7.6</span>.<span style="color: #800080;">2</span>]$ bin/elasticsearch</span>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('512bc7bd-db65-472c-a621-4348a5dd8651')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_512bc7bd-db65-472c-a621-4348a5dd8651" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_512bc7bd-db65-472c-a621-4348a5dd8651" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_512bc7bd-db65-472c-a621-4348a5dd8651" class="cnblogs_code_hide">
<pre># ---------------------------------- Cluster -----------------------------------<span style="color: #000000;">

# Use a descriptive name </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> your cluster:
  
# 集群名称，用于定义哪些elasticsearch节点属同一个集群。
cluster.name: bigdata
  
# </span>------------------------------------ Node ------------------------------------<span style="color: #000000;">
# 节点名称，用于唯一标识节点，不可重名
node.name: server3
  
# </span><span style="color: #800080;">1</span><span style="color: #000000;">、以下列出了三种集群拓扑模式，如下:
# 如果想让节点不具备选举主节点的资格，只用来做数据存储节点。
node.master: </span><span style="color: #0000ff;">false</span><span style="color: #000000;">
node.data: </span><span style="color: #0000ff;">true</span><span style="color: #000000;">
  
# </span><span style="color: #800080;">2</span><span style="color: #000000;">、如果想让节点成为主节点，且不存储任何数据，只作为集群协调者。
node.master: </span><span style="color: #0000ff;">true</span><span style="color: #000000;">
node.data: </span><span style="color: #0000ff;">false</span><span style="color: #000000;">
  
# </span><span style="color: #800080;">3</span><span style="color: #000000;">、如果想让节点既不成为主节点,又不成为数据节点,那么可将他作为搜索器,从节点中获取数据,生成搜索结果等
node.master: </span><span style="color: #0000ff;">false</span><span style="color: #000000;">
node.data: </span><span style="color: #0000ff;">false</span><span style="color: #000000;">
  
# 这个配置限制了单机上可以开启的ES存储实例的个数,当我们需要单机多实例，则需要把这个配置赋值2，或者更高。
#node.max_local_storage_nodes: </span><span style="color: #800080;">1</span><span style="color: #000000;">
  
# </span>----------------------------------- Index ------------------------------------<span style="color: #000000;">
# 设置索引的分片数,默认为5  </span><span style="color: #800000;">"</span><span style="color: #800000;">number_of_shards</span><span style="color: #800000;">"</span><span style="color: #000000;"> 是索引创建后一次生成的,后续不可更改设置
index.number_of_shards: </span><span style="color: #800080;">5</span><span style="color: #000000;">
  
# 设置索引的副本数,默认为1
index.number_of_replicas: </span><span style="color: #800080;">1</span><span style="color: #000000;">
  
# 索引的刷新频率，默认1秒，太小会造成索引频繁刷新，新的数据写入就慢了。（此参数的设置需要在写入性能和实时搜索中取平衡）通常在ELK场景中需要将值调大一些比如60s，在有_template的情况下，需要设置在应用的_template中才生效。 
index.refresh_interval: 120s
  
# </span>----------------------------------- Paths ------------------------------------<span style="color: #000000;">
# 数据存储路径，可以设置多个路径用逗号分隔，有助于提高IO。 # path.data: </span>/home/path1,/home/<span style="color: #000000;">path2
path.data: </span>/home/elk/<span style="color: #000000;">server3_data
  
# 日志文件路径
path.logs: </span>/<span style="color: #0000ff;">var</span>/log/<span style="color: #000000;">elasticsearch
  
# 临时文件的路径
path.work: </span>/path/to/<span style="color: #000000;">work
  
# </span>----------------------------------- Memory -------------------------------------<span style="color: #000000;">
# 确保 ES_MIN_MEM 和 ES_MAX_MEM 环境变量设置为相同的值,以及机器有足够的内存分配给Elasticsearch
# 注意:内存也不是越大越好,一般64位机器,最大分配内存别才超过32G
  
# 当JVM开始写入交换空间时（swapping）ElasticSearch性能会低下,你应该保证它不会写入交换空间
# 设置这个属性为true来锁定内存,同时也要允许elasticsearch的进程可以锁住内存,linux下可以通过 `ulimit </span>-<span style="color: #000000;">l unlimited` 命令
  
bootstrap.mlockall: </span><span style="color: #0000ff;">true</span><span style="color: #000000;">
  
# 节点用于 fielddata 的最大内存，如果 fielddata 
# 达到该阈值，就会把旧数据交换出去。该参数可以设置百分比或者绝对值。默认设置是不限制，所以强烈建议设置该值，比如 </span><span style="color: #800080;">10</span>%<span style="color: #000000;">。
indices.fielddata.cache.size: 50mb
  
# indices.fielddata.cache.expire  这个参数绝对绝对不要设置！
  
indices.breaker.fielddata.limit 默认值是JVM堆内存的60</span>%<span style="color: #000000;">,注意为了让设置正常生效，一定要确保 indices.breaker.fielddata.limit 的值
大于 indices.fielddata.cache.size 的值。否则的话，fielddata 大小一到 limit 阈值就报错，就永远道不了 size 阈值，无法触发对旧数据的交换任务了。
  
#</span>------------------------------------ Network And HTTP -----------------------------<span style="color: #000000;">
# 设置绑定的ip地址,可以是ipv4或ipv6的,默认为0.</span><span style="color: #800080;">0.0</span>.<span style="color: #800080;">0</span><span style="color: #000000;">
network.bind_host: </span><span style="color: #800080;">192.168</span>.<span style="color: #800080;">0.1</span><span style="color: #000000;">
  
# 设置其它节点和该节点通信的ip地址,如果不设置它会自动设置,值必须是个真实的ip地址
network.publish_host: </span><span style="color: #800080;">192.168</span>.<span style="color: #800080;">0.1</span><span style="color: #000000;">
  
# 同时设置bind_host和publish_host上面两个参数
network.host: </span><span style="color: #800080;">192.168</span>.<span style="color: #800080;">0.1</span><span style="color: #000000;">
  
# 设置集群中节点间通信的tcp端口,默认是9300
transport.tcp.port: </span><span style="color: #800080;">9300</span><span style="color: #000000;">
  
# 设置是否压缩tcp传输时的数据，默认为false,不压缩
transport.tcp.compress: </span><span style="color: #0000ff;">true</span><span style="color: #000000;">
  
# 设置对外服务的http端口,默认为9200
http.port: </span><span style="color: #800080;">9200</span><span style="color: #000000;">
  
# 设置请求内容的最大容量,默认100mb
http.max_content_length: 100mb
  
# </span>------------------------------------ Translog -------------------------------------<span style="color: #000000;">
#当事务日志累积到多少条数据后flush一次。
index.translog.flush_threshold_ops: </span><span style="color: #800080;">50000</span><span style="color: #000000;">
  
# </span>--------------------------------- Discovery --------------------------------------<span style="color: #000000;">
# 这个参数决定了要选举一个Master至少需要多少个节点，默认值是1，推荐设置为 N</span>/<span style="color: #800080;">2</span> + <span style="color: #800080;">1</span><span style="color: #000000;">，N是集群中节点的数量，这样可以有效避免脑裂
discovery.zen.minimum_master_nodes: </span><span style="color: #800080;">1</span><span style="color: #000000;">
  
# 在java里面GC是很常见的，但在GC时间比较长的时候。在默认配置下，节点会频繁失联。节点的失联又会导致数据频繁重传，甚至会导致整个集群基本不可用。
  
# discovery参数是用来做集群之间节点通信的，默认超时时间是比较小的。我们把参数适当调大，避免集群GC时间较长导致节点的丢失、失联。
discovery.zen.ping.timeout: 200s
discovery.zen.fd.ping_timeout: 200s
discovery.zen.fd.ping.interval: 30s
discovery.zen.fd.ping.retries: </span><span style="color: #800080;">6</span><span style="color: #000000;">
  
# 设置集群中节点的探测列表，新加入集群的节点需要加入列表中才能被探测到。 
discovery.zen.ping.unicast.hosts: [</span><span style="color: #800000;">"</span><span style="color: #800000;">10.10.1.244:9300</span><span style="color: #800000;">"</span><span style="color: #000000;">,]
  
# 是否打开广播自动发现节点，默认为true
discovery.zen.ping.multicast.enabled: </span><span style="color: #0000ff;">false</span><span style="color: #000000;">
 
indices.store.throttle.type: merge
indices.store.throttle.max_bytes_per_sec: 100mb

es配置</span></pre>
</div>
<span class="cnblogs_code_collapse">es配置</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('cf3d7ea6-2363-4da4-a8e0-7c2959454419')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_cf3d7ea6-2363-4da4-a8e0-7c2959454419" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_cf3d7ea6-2363-4da4-a8e0-7c2959454419" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_cf3d7ea6-2363-4da4-a8e0-7c2959454419" class="cnblogs_code_hide">
<pre><span style="color: #000000;">修改elasticsearch.yml

http.cors.enabled: </span><span style="color: #0000ff;">true</span><span style="color: #000000;">
http.cors.allow</span>-origin: <span style="color: #800000;">"</span><span style="color: #800000;">*</span><span style="color: #800000;">"</span><span style="color: #000000;">
http.cors.allow</span>-<span style="color: #000000;">headers: Authorization
xpack.security.enabled: </span><span style="color: #0000ff;">true</span><span style="color: #000000;">
xpack.security.transport.ssl.enabled: </span><span style="color: #0000ff;">true</span><span style="color: #000000;">

启动es服务 .</span>/elasticsearch -<span style="color: #000000;">d

修改密码
$ .</span>/bin/elasticsearch-setup-<span style="color: #000000;">passwords interactive

You will be prompted to enter passwords </span><span style="color: #0000ff;">as</span><span style="color: #000000;"> the process progresses.
Please confirm that you would like to </span><span style="color: #0000ff;">continue</span> [y/<span style="color: #000000;">N] y 
Enter password </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> [elastic]: 
Reenter password </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> [elastic]: 
Enter password </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> [apm_system]: 
Reenter password </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> [apm_system]: 
Enter password </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> [kibana]: 
Reenter password </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> [kibana]: 
Enter password </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> [logstash_system]: 
Reenter password </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> [logstash_system]: 
Enter password </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> [beats_system]: 
Reenter password </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> [beats_system]: 
Enter password </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> [remote_monitoring_user]: 
Reenter password </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> [remote_monitoring_user]: 

修改密码： curl </span>-XPUT -u elastic:changeme <span style="color: #800000;">'</span><span style="color: #800000;">http://localhost:9200/_xpack/security/user/elastic/_password</span><span style="color: #800000;">'</span> -d <span style="color: #800000;">'</span><span style="color: #800000;">{ "password" : "your_passwd" }</span><span style="color: #800000;">'</span></pre>
</div>
<span class="cnblogs_code_collapse">配置密码</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('a607589c-dce8-4d11-90c1-fe4ed872a9fb')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_a607589c-dce8-4d11-90c1-fe4ed872a9fb" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_a607589c-dce8-4d11-90c1-fe4ed872a9fb" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_a607589c-dce8-4d11-90c1-fe4ed872a9fb" class="cnblogs_code_hide">
<pre># ======================== Elasticsearch Configuration =========================<span style="color: #000000;">
#
# NOTE: Elasticsearch comes with reasonable defaults </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> most settings.
#       Before you </span><span style="color: #0000ff;">set</span> <span style="color: #0000ff;">out</span><span style="color: #000000;"> to tweak and tune the configuration, make sure you
#       understand what are you trying to accomplish and the consequences.
#
# The primary way of configuring a node </span><span style="color: #0000ff;">is</span> via <span style="color: #0000ff;">this</span><span style="color: #000000;"> file. This template lists
# the most important settings you may want to configure </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> a production cluster.
#
# Please consult the documentation </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> further information on configuration options:
# https:</span><span style="color: #008000;">//</span><span style="color: #008000;">www.elastic.co/guide/en/elasticsearch/reference/index.html</span>
<span style="color: #000000;">#
# </span>---------------------------------- Cluster -----------------------------------<span style="color: #000000;">
#
# Use a descriptive name </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> your cluster:
#
cluster.name: demo
cluster.initial_master_nodes: [</span><span style="color: #800000;">"</span><span style="color: #800000;">node1</span><span style="color: #800000;">"</span><span style="color: #000000;">]
#
# </span>------------------------------------ Node ------------------------------------<span style="color: #000000;">
#
# Use a descriptive name </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> the node:
#
node.name: node1
#
# Add custom attributes to the node:
#
#node.attr.rack: r1
#
# </span>----------------------------------- Paths ------------------------------------<span style="color: #000000;">
#
# Path to directory </span><span style="color: #0000ff;">where</span><span style="color: #000000;"> to store the data (separate multiple locations by comma):
#
#path.data: </span>/path/to/<span style="color: #000000;">data
#
# Path to log files:
#
#path.logs: </span>/path/to/<span style="color: #000000;">logs
#
# </span>----------------------------------- Memory -----------------------------------<span style="color: #000000;">
#
# Lock the memory on startup:
#
#bootstrap.memory_lock: </span><span style="color: #0000ff;">true</span><span style="color: #000000;">
#
# Make sure that the heap size </span><span style="color: #0000ff;">is</span> <span style="color: #0000ff;">set</span><span style="color: #000000;"> to about half the memory available
# on the system and that the owner of the process </span><span style="color: #0000ff;">is</span> allowed to use <span style="color: #0000ff;">this</span><span style="color: #000000;">
# limit.
#
# Elasticsearch performs poorly when the system </span><span style="color: #0000ff;">is</span><span style="color: #000000;"> swapping the memory.
#
# </span>---------------------------------- Network -----------------------------------<span style="color: #000000;">
#
# Set the bind address to a specific IP (IPv4 or IPv6):
#
network.host: </span><span style="color: #800080;">192.168</span>.<span style="color: #800080;">0.150</span><span style="color: #000000;">
#
# Set a custom port </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> HTTP:
#
http.port: </span><span style="color: #800080;">9200</span><span style="color: #000000;">
#
# For more information, consult the network module documentation.
#
# </span>--------------------------------- Discovery ----------------------------------<span style="color: #000000;">
#
# Pass an initial list of hosts to perform discovery when </span><span style="color: #0000ff;">this</span> node <span style="color: #0000ff;">is</span><span style="color: #000000;"> started:
# The </span><span style="color: #0000ff;">default</span> list of hosts <span style="color: #0000ff;">is</span> [<span style="color: #800000;">"</span><span style="color: #800000;">127.0.0.1</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">[::1]</span><span style="color: #800000;">"</span><span style="color: #000000;">]
#
#discovery.seed_hosts: [</span><span style="color: #800000;">"</span><span style="color: #800000;">host1</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">host2</span><span style="color: #800000;">"</span><span style="color: #000000;">]
#
# Bootstrap the cluster </span><span style="color: #0000ff;">using</span> an initial <span style="color: #0000ff;">set</span> of master-<span style="color: #000000;">eligible nodes:
#
#cluster.initial_master_nodes: [</span><span style="color: #800000;">"</span><span style="color: #800000;">node-1</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">node-2</span><span style="color: #800000;">"</span><span style="color: #000000;">]
#
# For more information, consult the discovery and cluster formation module documentation.
#
# </span>---------------------------------- Gateway -----------------------------------<span style="color: #000000;">
#
# Block initial recovery after a full cluster restart until N nodes are started:
#
#gateway.recover_after_nodes: </span><span style="color: #800080;">3</span><span style="color: #000000;">
#
# For more information, consult the gateway module documentation.
#
# </span>---------------------------------- Various -----------------------------------<span style="color: #000000;">
#
# Require </span><span style="color: #0000ff;">explicit</span><span style="color: #000000;"> names when deleting indices:
#
#action.destructive_requires_name: </span><span style="color: #0000ff;">true</span><span style="color: #000000;">
#
#

http.cors.enabled: </span><span style="color: #0000ff;">true</span><span style="color: #000000;">
http.cors.allow</span>-origin: <span style="color: #800000;">"</span><span style="color: #800000;">*</span><span style="color: #800000;">"</span><span style="color: #000000;">
http.cors.allow</span>-<span style="color: #000000;">headers: Authorization
xpack.security.enabled: </span><span style="color: #0000ff;">true</span><span style="color: #000000;">
xpack.security.transport.ssl.enabled: </span><span style="color: #0000ff;">true</span></pre>
</div>
<span class="cnblogs_code_collapse">elasticsearch.yml</span></div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: #169fe6;"><span style="color: #ffffff;"><strong>四、安装插件</strong></span></p>
<p>&nbsp;<img src="https://img2020.cnblogs.com/blog/741594/202004/741594-20200405201800204-1037831468.png" alt="" width="506" height="220" /></p>
<p>&nbsp;查询安装的插件：&nbsp;<span class="cnblogs_code">[hunter@localhost elasticsearch-<span style="color: #800080;">7.6</span>.<span style="color: #800080;">2</span>]$ bin/elasticsearch-plugin list</span>&nbsp;</p>
<p>&nbsp;安装分词插件：&nbsp;<span class="cnblogs_code">bin/elasticsearch-plugin install analysis-icu</span>&nbsp;</p>
<p>&nbsp;url查询安装的插件：http://localhost:9200/_cat/plugins</p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: #169fe6;"><span style="color: #ffffff;"><strong>五、部署多个实例</strong></span></p>
<div class="cnblogs_code">
<pre>bin/elasticsearch -E node.name=node0 -E cluster.name=zhang -E path.data=node0_date -<span style="color: #000000;">d 
bin</span>/elasticsearch -E node.name=node1 -E cluster.name=zhang -E path.data=node1_date -<span style="color: #000000;">d 
bin</span>/elasticsearch -E node.name=node2 -E cluster.name=zhang -E path.data=node2_date -<span style="color: #000000;">d 
bin</span>/elasticsearch -E node.name=node3 -E cluster.name=zhang -E path.data=node3_date -d</pre>
</div>
<p>删除进程：</p>
<p><span class="cnblogs_code">ps -ef |grep elasticsearch</span>&nbsp;</p>
<p><span class="cnblogs_code">kill <span style="color: #800080;">1234</span></span>&nbsp;&nbsp;</p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: #169fe6;"><span style="color: #ffffff;"><strong>六、安装失败场景解决</strong></span></p>
<p>1，Exception in thread "main" java.nio.file.AccessDeniedException</p>
<p>原因：当前用户没有执行权限&nbsp;<br />解决方法： chown linux用户名 elasticsearch安装目录 -R&nbsp;&nbsp;&nbsp;<span class="cnblogs_code">chown hunter elasticsearch-<span style="color: #800080;">7.6</span>.<span style="color: #800080;">2</span> -R</span>&nbsp;</p>
<p>2，Exception in thread "main" org.elasticsearch.bootstrap.BootstrapException: java.nio.file.FileAlready</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202004/741594-20200405185619571-2029546639.png" alt="" /></p>
<p>&nbsp;解决方式，删除文件&nbsp;rm -rf elasticsearch.keystore.tmp</p>
<p>3，&nbsp;hunter 不在 sudoers 文件中。此事将被报告</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202004/741594-20200406005304606-479970612.png" alt="" width="347" height="164" /></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: #169fe6;"><strong><span style="color: #ffffff;">七、安装Kibana</span></strong></p>
<p>1，下载地址：<a href="https://www.elastic.co/cn/downloads/kibana" target="_blank">https://www.elastic.co/cn/downloads/kibana</a></p>
<p>2，启动：&nbsp;<span class="cnblogs_code">[hunter@localhost kibana-<span style="color: #800080;">7.6</span>.<span style="color: #800080;">2</span>-linux-x86_64]$ bin/kibana</span>&nbsp;</p>
<p>启动之前需要给hunter目录权限</p>
<p>修改host:</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202004/741594-20200406003218979-299703859.png" alt="" width="563" height="99" /></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>3，插件安装</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202004/741594-20200405233943677-1902065880.png" alt="" width="410" height="205" /></p>
<p>&nbsp;</p>
<p>4，导入测试数据&nbsp;</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202004/741594-20200405234119715-1936067242.png" alt="" width="651" height="351" /></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('8e0c71d0-3292-4d3f-be1b-4f916a4572cb')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_8e0c71d0-3292-4d3f-be1b-4f916a4572cb" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_8e0c71d0-3292-4d3f-be1b-4f916a4572cb" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_8e0c71d0-3292-4d3f-be1b-4f916a4572cb" class="cnblogs_code_hide">
<pre># Kibana <span style="color: #0000ff;">is</span><span style="color: #000000;"> served by a back end server. This setting specifies the port to use.
server.port: </span><span style="color: #800080;">5601</span><span style="color: #000000;">

# Specifies the address to which the Kibana server will bind. IP addresses and host names are both valid values.
# The </span><span style="color: #0000ff;">default</span> <span style="color: #0000ff;">is</span> <span style="color: #800000;">'</span><span style="color: #800000;">localhost</span><span style="color: #800000;">'</span><span style="color: #000000;">, which usually means remote machines will not be able to connect.
# To allow connections </span><span style="color: #0000ff;">from</span> remote users, <span style="color: #0000ff;">set</span> <span style="color: #0000ff;">this</span> parameter to a non-<span style="color: #000000;">loopback address.
server.host: </span><span style="color: #800000;">"</span><span style="color: #800000;">192.168.0.150</span><span style="color: #800000;">"</span><span style="color: #000000;">

# Enables you to specify a path to mount Kibana at </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> you are running behind a proxy.
# Use the `server.rewriteBasePath` setting to tell Kibana </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> it should remove the basePath
# </span><span style="color: #0000ff;">from</span><span style="color: #000000;"> requests it receives, and to prevent a deprecation warning at startup.
# This setting cannot end </span><span style="color: #0000ff;">in</span><span style="color: #000000;"> a slash.
#server.basePath: </span><span style="color: #800000;">""</span><span style="color: #000000;">

# Specifies whether Kibana should rewrite requests that are prefixed with
# `server.basePath` or require that they are rewritten by your reverse proxy.
# This setting was effectively always `</span><span style="color: #0000ff;">false</span>` before Kibana <span style="color: #800080;">6.3</span><span style="color: #000000;"> and will
# </span><span style="color: #0000ff;">default</span> to `<span style="color: #0000ff;">true</span>` starting <span style="color: #0000ff;">in</span> Kibana <span style="color: #800080;">7.0</span><span style="color: #000000;">.
#server.rewriteBasePath: </span><span style="color: #0000ff;">false</span><span style="color: #000000;">

# The maximum payload size </span><span style="color: #0000ff;">in</span> bytes <span style="color: #0000ff;">for</span><span style="color: #000000;"> incoming server requests.
#server.maxPayloadBytes: </span><span style="color: #800080;">1048576</span><span style="color: #000000;">

# The Kibana server</span><span style="color: #800000;">'</span><span style="color: #800000;">s name.  This is used for display purposes.</span>
#server.name: <span style="color: #800000;">"</span><span style="color: #800000;">your-hostname</span><span style="color: #800000;">"</span><span style="color: #000000;">

# The URLs of the Elasticsearch instances to use </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> all your queries.
elasticsearch.hosts: [</span><span style="color: #800000;">"</span><span style="color: #800000;">http://192.168.0.150:9200</span><span style="color: #800000;">"</span><span style="color: #000000;">]

# When </span><span style="color: #0000ff;">this</span> setting<span style="color: #800000;">'</span><span style="color: #800000;">s value is true Kibana uses the hostname specified in the server.host</span>
# setting. When the value of <span style="color: #0000ff;">this</span> setting <span style="color: #0000ff;">is</span> <span style="color: #0000ff;">false</span><span style="color: #000000;">, Kibana uses the hostname of the host
# that connects to </span><span style="color: #0000ff;">this</span><span style="color: #000000;"> Kibana instance.
#elasticsearch.preserveHost: </span><span style="color: #0000ff;">true</span><span style="color: #000000;">

# Kibana uses an index </span><span style="color: #0000ff;">in</span><span style="color: #000000;"> Elasticsearch to store saved searches, visualizations and
# dashboards. Kibana creates a </span><span style="color: #0000ff;">new</span> index <span style="color: #0000ff;">if</span> the index doesn<span style="color: #800000;">'</span><span style="color: #800000;">t already exist.</span>
#kibana.index: <span style="color: #800000;">"</span><span style="color: #800000;">.kibana</span><span style="color: #800000;">"</span><span style="color: #000000;">

# The </span><span style="color: #0000ff;">default</span><span style="color: #000000;"> application to load.
#kibana.defaultAppId: </span><span style="color: #800000;">"</span><span style="color: #800000;">home</span><span style="color: #800000;">"</span><span style="color: #000000;">

# If your Elasticsearch </span><span style="color: #0000ff;">is</span> <span style="color: #0000ff;">protected</span><span style="color: #000000;"> with basic authentication, these settings provide
# the username and password that the Kibana server uses to perform maintenance on the Kibana
# index at startup. Your Kibana users still need to authenticate with Elasticsearch, which
# </span><span style="color: #0000ff;">is</span><span style="color: #000000;"> proxied through the Kibana server.
elasticsearch.username: </span><span style="color: #800000;">"</span><span style="color: #800000;">kibana</span><span style="color: #800000;">"</span><span style="color: #000000;">
elasticsearch.password: </span><span style="color: #800000;">"</span><span style="color: #800000;">123456</span><span style="color: #800000;">"</span><span style="color: #000000;">

# Enables SSL and paths to the PEM</span>-<span style="color: #000000;">format SSL certificate and SSL key files, respectively.
# These settings enable SSL </span><span style="color: #0000ff;">for</span> outgoing requests <span style="color: #0000ff;">from</span><span style="color: #000000;"> the Kibana server to the browser.
#server.ssl.enabled: </span><span style="color: #0000ff;">false</span><span style="color: #000000;">
#server.ssl.certificate: </span>/path/to/your/<span style="color: #000000;">server.crt
#server.ssl.key: </span>/path/to/your/<span style="color: #000000;">server.key

# Optional settings that provide the paths to the PEM</span>-<span style="color: #000000;">format SSL certificate and key files.
# These files are used to verify the identity of Kibana to Elasticsearch and are required when
# xpack.security.http.ssl.client_authentication </span><span style="color: #0000ff;">in</span> Elasticsearch <span style="color: #0000ff;">is</span> <span style="color: #0000ff;">set</span><span style="color: #000000;"> to required.
#elasticsearch.ssl.certificate: </span>/path/to/your/<span style="color: #000000;">client.crt
#elasticsearch.ssl.key: </span>/path/to/your/<span style="color: #000000;">client.key

# Optional setting that enables you to specify a path to the PEM file </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> the certificate
# authority </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> your Elasticsearch instance.
#elasticsearch.ssl.certificateAuthorities: [ </span><span style="color: #800000;">"</span><span style="color: #800000;">/path/to/your/CA.pem</span><span style="color: #800000;">"</span><span style="color: #000000;"> ]

# To disregard the validity of SSL certificates, change </span><span style="color: #0000ff;">this</span> setting<span style="color: #800000;">'</span><span style="color: #800000;">s value to </span><span style="color: #800000;">'</span>none<span style="color: #800000;">'</span><span style="color: #800000;">.</span>
<span style="color: #000000;">#elasticsearch.ssl.verificationMode: full

# Time </span><span style="color: #0000ff;">in</span> milliseconds to wait <span style="color: #0000ff;">for</span><span style="color: #000000;"> Elasticsearch to respond to pings. Defaults to the value of
# the elasticsearch.requestTimeout setting.
#elasticsearch.pingTimeout: </span><span style="color: #800080;">1500</span><span style="color: #000000;">

# Time </span><span style="color: #0000ff;">in</span> milliseconds to wait <span style="color: #0000ff;">for</span> responses <span style="color: #0000ff;">from</span><span style="color: #000000;"> the back end or Elasticsearch. This value
# must be a positive integer.
#elasticsearch.requestTimeout: </span><span style="color: #800080;">30000</span><span style="color: #000000;">

# List of Kibana client</span>-side headers to send to Elasticsearch. To send *no* client-<span style="color: #000000;">side
# headers, </span><span style="color: #0000ff;">set</span> <span style="color: #0000ff;">this</span><span style="color: #000000;"> value to [] (an empty list).
#elasticsearch.requestHeadersWhitelist: [ authorization ]

# Header names and values that are sent to Elasticsearch. Any custom headers cannot be overwritten
# by client</span>-<span style="color: #000000;">side headers, regardless of the elasticsearch.requestHeadersWhitelist configuration.
#elasticsearch.customHeaders: {}

# Time </span><span style="color: #0000ff;">in</span> milliseconds <span style="color: #0000ff;">for</span> Elasticsearch to wait <span style="color: #0000ff;">for</span> responses <span style="color: #0000ff;">from</span> shards. Set to <span style="color: #800080;">0</span><span style="color: #000000;"> to disable.
#elasticsearch.shardTimeout: </span><span style="color: #800080;">30000</span><span style="color: #000000;">

# Time </span><span style="color: #0000ff;">in</span> milliseconds to wait <span style="color: #0000ff;">for</span><span style="color: #000000;"> Elasticsearch at Kibana startup before retrying.
#elasticsearch.startupTimeout: </span><span style="color: #800080;">5000</span><span style="color: #000000;">

# Logs queries sent to Elasticsearch. Requires logging.verbose </span><span style="color: #0000ff;">set</span> to <span style="color: #0000ff;">true</span><span style="color: #000000;">.
#elasticsearch.logQueries: </span><span style="color: #0000ff;">false</span><span style="color: #000000;">

# Specifies the path </span><span style="color: #0000ff;">where</span><span style="color: #000000;"> Kibana creates the process ID file.
#pid.file: </span>/<span style="color: #0000ff;">var</span>/run/<span style="color: #000000;">kibana.pid

# Enables you specify a file </span><span style="color: #0000ff;">where</span><span style="color: #000000;"> Kibana stores log output.
#logging.dest: stdout

# Set the value of </span><span style="color: #0000ff;">this</span> setting to <span style="color: #0000ff;">true</span><span style="color: #000000;"> to suppress all logging output.
#logging.silent: </span><span style="color: #0000ff;">false</span><span style="color: #000000;">

# Set the value of </span><span style="color: #0000ff;">this</span> setting to <span style="color: #0000ff;">true</span><span style="color: #000000;"> to suppress all logging output other than error messages.
#logging.quiet: </span><span style="color: #0000ff;">false</span><span style="color: #000000;">

# Set the value of </span><span style="color: #0000ff;">this</span> setting to <span style="color: #0000ff;">true</span><span style="color: #000000;"> to log all events, including system usage information
# and all requests.
#logging.verbose: </span><span style="color: #0000ff;">false</span><span style="color: #000000;">

# Set the interval </span><span style="color: #0000ff;">in</span><span style="color: #000000;"> milliseconds to sample system and process performance
# metrics. Minimum </span><span style="color: #0000ff;">is</span> 100ms. Defaults to <span style="color: #800080;">5000</span><span style="color: #000000;">.
#ops.interval: </span><span style="color: #800080;">5000</span><span style="color: #000000;">

# Specifies locale to be used </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> all localizable strings, dates and number formats.
# Supported languages are the following: English </span>- en , by <span style="color: #0000ff;">default</span> , Chinese - zh-<span style="color: #000000;">CN .
#i18n.locale: </span><span style="color: #800000;">"</span><span style="color: #800000;">en</span><span style="color: #800000;">"</span></pre>
</div>
<span class="cnblogs_code_collapse">kibana.yml</span></div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: #169fe6;"><strong><span style="color: #ffffff;">八、安装logstash</span></strong></p>
<p>1，下载地址：<a href="https://www.elastic.co/cn/downloads/logstash" target="_blank">https://www.elastic.co/cn/downloads/logstash</a></p>
<p>2，导入数据</p>
<p>①配置文件：<a href="https://github.com/geektime-geekbang/geektime-ELK/tree/master/part-1/2.4-Logstash%E5%AE%89%E8%A3%85%E4%B8%8E%E5%AF%BC%E5%85%A5%E6%95%B0%E6%8D%AE/movielens" target="_blank">https://github.com/geektime-geekbang/geektime-ELK/tree/master/part-1/2.4-Logstash%E5%AE%89%E8%A3%85%E4%B8%8E%E5%AF%BC%E5%85%A5%E6%95%B0%E6%8D%AE/movielens</a></p>
<p>②数据文件：<a href="https://github.com/geektime-geekbang/geektime-ELK/tree/master/part-1/2.4-Logstash%E5%AE%89%E8%A3%85%E4%B8%8E%E5%AF%BC%E5%85%A5%E6%95%B0%E6%8D%AE/movielens/ml-latest-small" target="_blank">https://github.com/geektime-geekbang/geektime-ELK/tree/master/part-1/2.4-Logstash%E5%AE%89%E8%A3%85%E4%B8%8E%E5%AF%BC%E5%85%A5%E6%95%B0%E6%8D%AE/movielens/ml-latest-small</a></p>
<p>3， 执行：&nbsp;<span class="cnblogs_code">[hunter@localhost bin]$ sudo ./logstash -f logstash.conf</span>&nbsp;</p>
<p><strong>4，Filter Plugin-Mutate</strong></p>
<p>Convert 类型转换</p>
<p>Gsub 字符串转换</p>
<p>Split/Join/Merge 字符串切割，数组合并字符串，数组合并数组</p>
<p>Rename 字段重命名</p>
<p>Update/Replace 字段内容更新替换</p>
<p>Remove_field 字段删除</p>
<p><strong>5，定期增量同步mysql表数据</strong></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">input {
  jdbc {
    jdbc_driver_class </span>=&gt; <span style="color: #800000;">"</span><span style="color: #800000;">com.mysql.jdbc.Driver</span><span style="color: #800000;">"</span><span style="color: #000000;">
    jdbc_connection_string </span>=&gt; <span style="color: #800000;">"</span><span style="color: #800000;">jdbc:mysql://localhost:3306/db_example</span><span style="color: #800000;">"</span><span style="color: #000000;">
    jdbc_user </span>=&gt;<span style="color: #000000;"> root
    jdbc_password </span>=&gt;<span style="color: #000000;"> ymruan123
    #启用追踪，如果为true，则需要指定tracking_column
    use_column_value </span>=&gt; <span style="color: #0000ff;">true</span><span style="color: #000000;">
    #指定追踪的字段，
    tracking_column </span>=&gt; <span style="color: #800000;">"</span><span style="color: #800000;">last_updated</span><span style="color: #800000;">"</span><span style="color: #000000;">
    #追踪字段的类型，目前只有数字(numeric)和时间类型(timestamp)，默认是数字类型
    tracking_column_type </span>=&gt; <span style="color: #800000;">"</span><span style="color: #800000;">numeric</span><span style="color: #800000;">"</span><span style="color: #000000;">
    #记录最后一次运行的结果
    record_last_run </span>=&gt; <span style="color: #0000ff;">true</span><span style="color: #000000;">
    #上面运行结果的保存位置
    last_run_metadata_path </span>=&gt; <span style="color: #800000;">"</span><span style="color: #800000;">jdbc-position.txt</span><span style="color: #800000;">"</span><span style="color: #000000;">
    statement </span>=&gt; <span style="color: #800000;">"</span><span style="color: #800000;">SELECT * FROM user where last_updated &gt;:sql_last_value;</span><span style="color: #800000;">"</span><span style="color: #000000;">
    schedule </span>=&gt; <span style="color: #800000;">"</span><span style="color: #800000;"> * * * * * *</span><span style="color: #800000;">"</span><span style="color: #000000;">
  }
}
output {
  elasticsearch {
    document_id </span>=&gt; <span style="color: #800000;">"</span><span style="color: #800000;">%{id}</span><span style="color: #800000;">"</span><span style="color: #000000;">
    document_type </span>=&gt; <span style="color: #800000;">"</span><span style="color: #800000;">_doc</span><span style="color: #800000;">"</span><span style="color: #000000;">
    index </span>=&gt; <span style="color: #800000;">"</span><span style="color: #800000;">users</span><span style="color: #800000;">"</span><span style="color: #000000;">
    hosts </span>=&gt; [<span style="color: #800000;">"</span><span style="color: #800000;">http://localhost:9200</span><span style="color: #800000;">"</span><span style="color: #000000;">]
  }
  stdout{
    codec </span>=&gt;<span style="color: #000000;"> rubydebug
  }
}</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: #169fe6;"><span style="color: #ffffff;"><strong>九、安装cerebro</strong></span></p>
<p>1，下载地址：<a href="https://github.com/lmenezes/cerebro/releases" target="_blank">https://github.com/lmenezes/cerebro/releases</a></p>
<p>2，配置es地址：&nbsp;<span class="cnblogs_code">[root@localhost ~]# vim /usr/cerebro-<span style="color: #800080;">0.8</span>.<span style="color: #800080;">5</span>/conf/application.conf</span>&nbsp;</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202004/741594-20200406173715083-498624750.png" alt="" /></p>
<p>&nbsp;</p>
<p>3，启动：&nbsp;<span class="cnblogs_code">[root@localhost ~]# vim /usr/cerebro-<span style="color: #800080;">0.8</span>.<span style="color: #800080;">5</span>/bin/cerebro</span>&nbsp;&nbsp;</p>
<p>&nbsp;</p>