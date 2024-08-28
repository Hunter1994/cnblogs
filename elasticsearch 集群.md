<p style="font-size: 18pt; background-color: #169fe6;"><span style="color: #ffffff;"><strong>一、节点</strong></span></p>
<p><strong>1，Coordination Node</strong></p>
<p>①处理请求的节点，叫Coordination Node，路由请求到正确的节点，例如创建索引的请求，需要路由到master节点</p>
<p>②所有节点默认都是Coordination Node</p>
<p>③通过将其他类型设置false，使其成为Dedicated&nbsp;Coordination Node</p>
<p><strong>2，Data Node</strong></p>
<p>①可以保存数据的节点，叫做Data Node，节点启动后，默认就是数据节点。可以设置node.data:false禁止</p>
<p>②Data Node的职责：保存分片数据。在数据扩展上起到了至关重要的作用（由Master Node决定如何把分片分发到数据节点上）</p>
<p>③通过增加数据节点，可以解决数据水平扩展和解决数据单点问题</p>
<p><strong>3，Master Node</strong></p>
<p>Master Node职责：</p>
<p>①处理创建、删除索引等请求/决定分片被分配到哪个节点/负责索引的创建与删除</p>
<p>②维护并且更新Cluster State</p>
<p>Master Node最佳实践：</p>
<p>①Master 节点非常重要，在部署上需要考虑决绝单点的问题</p>
<p>②为一个集群设置多个Master节点/每个节点只承担Master的单一角色</p>
<p><strong>4，Master Eligible Nodes &amp; 选主流程</strong></p>
<p>①一个集群，支持配置多个Master Eligible节点。这些节点可以在必要时（如Master 节点出现故障，网络故障时）参与选主流程，成为Master节点</p>
<p>②每个节点启动后，默认就是一个Master Eligible节点，可以设置node.master:false 禁止</p>
<p>③单集群内第一个Master Eligible节点启动时，它会将自己选举成Master节点</p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: #169fe6;"><span style="color: #ffffff;"><strong>二、分片</strong></span></p>
<p><strong>1，主分片-提升系统存储容量</strong></p>
<p>分片是elasticsearch分布式存储的基石（主分片/副本分片）</p>
<p>通过主分片，将数据分布在所有节点上</p>
<p>　　主分片，可以将一份索引的数据，分散在多个Data Node上，实现存储的水平扩展</p>
<p>　　主分片数在索引创建的时候指定，后续默认不能修改，如需修改，需要重建索引</p>
<p><strong>2，副本分片-提高数据可用性</strong></p>
<p>数据可用性</p>
<p>　　通过引入副本分片提高数据的可用性。一旦主分片丢失，副本分片可以promote成主分片。副本分片数可以动态调整。每个节点上都有完备的数据。如果不设置副本分片，一旦出现节点硬件故障，就有可能造成数据丢失</p>
<p>提成系统的读取性能</p>
<p>　　副本分片由主分片同步。通过支持增加replica个数，一定程度可以提高读取的吞吐量</p>
<p><strong>3，分片数的设定-如何规划一个索引的主分片数和副本分片数</strong></p>
<p>① 主分片数过小：例如创建了1个主分片的索引。如果该索引增长的很快，集群无法通过增加节点实现对这个索引的数据扩展</p>
<p>②主分片数设置过大：导致单个分片容量很小，引发一个节点上有过多的分片，影响性能</p>
<p>③副本分片数设置过多，会降低集群整体的写入性能</p>
<p><strong>4，如何确定主分片数</strong></p>
<p>①从存储物理角度看</p>
<p>　　日志类应用，单个分片不要大于50GB</p>
<p>　　搜索类应用，单个分片不要超过20GB</p>
<p>②为什么要控制分片大小</p>
<p>　　提高update的性能</p>
<p>　　Merge时，减少所需的资源</p>
<p>　　丢失节点后，具备更快的恢复速度/便于分片在集群内Rebalancing</p>
<p><strong>5，如何确定副本分片数</strong></p>
<p>①副本是主分片的拷贝</p>
<p>　　提高系统的可用性：相应查询请求，防止数据丢失</p>
<p>　　需要占用和主分片一样的资源</p>
<p>②对性能的影响</p>
<p>　　副本会降低数据的索引速度：有几分副本就会有几倍的CPU资源消耗在索引上</p>
<p>　　会减缓对主分片的查询压力，但是会消耗同样的内存资源。如果机器资源充分，提高副本数，可以提高整体的查询QPS</p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: #169fe6;"><span style="color: #ffffff;"><strong>三、监控elasticsearch集群</strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;"># Node Stats：
GET _nodes</span>/<span style="color: #000000;">stats

#Cluster Stats:
GET _cluster</span>/<span style="color: #000000;">stats

#Index Stats:
GET kibana_sample_data_ecommerce</span>/<span style="color: #000000;">_stats

#Pending Cluster Tasks API:
GET _cluster</span>/<span style="color: #000000;">pending_tasks

# 查看所有的 tasks，也支持 cancel task
GET _tasks


GET _nodes</span>/<span style="color: #000000;">thread_pool
GET _nodes</span>/stats/<span style="color: #000000;">thread_pool
GET _cat</span>/thread_pool?<span style="color: #000000;">v
GET _nodes</span>/<span style="color: #000000;">hot_threads
GET _nodes</span>/stats/<span style="color: #000000;">thread_pool


# 设置 Index Slowlogs
# the first </span><span style="color: #800080;">1000</span> characters of the doc<span style="color: #800000;">'</span><span style="color: #800000;">s source will be logged</span>
PUT my_index/<span style="color: #000000;">_settings
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">index.indexing.slowlog</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
    </span><span style="color: #800000;">"</span><span style="color: #800000;">threshold.index</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
      </span><span style="color: #800000;">"</span><span style="color: #800000;">warn</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">10s</span><span style="color: #800000;">"</span><span style="color: #000000;">,
      </span><span style="color: #800000;">"</span><span style="color: #800000;">info</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">4s</span><span style="color: #800000;">"</span><span style="color: #000000;">,
      </span><span style="color: #800000;">"</span><span style="color: #800000;">debug</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">2s</span><span style="color: #800000;">"</span><span style="color: #000000;">,
      </span><span style="color: #800000;">"</span><span style="color: #800000;">trace</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">0s</span><span style="color: #800000;">"</span><span style="color: #000000;">
    },
    </span><span style="color: #800000;">"</span><span style="color: #800000;">level</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">trace</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">source</span><span style="color: #800000;">"</span>:<span style="color: #800080;">1000</span><span style="color: #000000;">  
  }
}

# 设置查询
DELETE my_index
</span><span style="color: #008000;">//</span><span style="color: #008000;">"0" logs all queries</span>
PUT my_index/<span style="color: #000000;">
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">settings</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">index.search.slowlog.threshold</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">query.warn</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">10s</span><span style="color: #800000;">"</span><span style="color: #000000;">,
      </span><span style="color: #800000;">"</span><span style="color: #800000;">query.info</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">3s</span><span style="color: #800000;">"</span><span style="color: #000000;">,
      </span><span style="color: #800000;">"</span><span style="color: #800000;">query.debug</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">2s</span><span style="color: #800000;">"</span><span style="color: #000000;">,
      </span><span style="color: #800000;">"</span><span style="color: #800000;">query.trace</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">0s</span><span style="color: #800000;">"</span><span style="color: #000000;">,
      </span><span style="color: #800000;">"</span><span style="color: #800000;">fetch.warn</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">1s</span><span style="color: #800000;">"</span><span style="color: #000000;">,
      </span><span style="color: #800000;">"</span><span style="color: #800000;">fetch.info</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">600ms</span><span style="color: #800000;">"</span><span style="color: #000000;">,
      </span><span style="color: #800000;">"</span><span style="color: #800000;">fetch.debug</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">400ms</span><span style="color: #800000;">"</span><span style="color: #000000;">,
      </span><span style="color: #800000;">"</span><span style="color: #800000;">fetch.trace</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">0s</span><span style="color: #800000;">"</span><span style="color: #000000;">
    }
  }
}

GET my_index</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #000000;">#案例1
DELETE mytest
PUT mytest
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">settings</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
    </span><span style="color: #800000;">"</span><span style="color: #800000;">number_of_shards</span><span style="color: #800000;">"</span>:<span style="color: #800080;">3</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">number_of_replicas</span><span style="color: #800000;">"</span>:<span style="color: #800080;">0</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">index.routing.allocation.require.box_type</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">hott</span><span style="color: #800000;">"</span><span style="color: #000000;">
  }
}





# 检查集群状态，查看是否有节点丢失，有多少分片无法分配
GET </span>/_cluster/health/<span style="color: #000000;">

# 查看索引级别,找到红色的索引
GET </span>/_cluster/health?level=<span style="color: #000000;">indices


#查看索引的分片
GET _cluster</span>/health?level=<span style="color: #000000;">shards

# Explain 变红的原因
GET </span>/_cluster/allocation/<span style="color: #000000;">explain

GET </span>/_cat/shards/<span style="color: #000000;">mytest
GET _cat</span>/<span style="color: #000000;">nodeattrs

DELETE mytest
GET </span>/_cluster/health/<span style="color: #000000;">

PUT mytest
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">settings</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
    </span><span style="color: #800000;">"</span><span style="color: #800000;">number_of_shards</span><span style="color: #800000;">"</span>:<span style="color: #800080;">3</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">number_of_replicas</span><span style="color: #800000;">"</span>:<span style="color: #800080;">0</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">index.routing.allocation.require.box_type</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">hot</span><span style="color: #800000;">"</span><span style="color: #000000;">
  }
}

GET </span>/_cluster/health/<span style="color: #000000;">

#案例2, Explain 看 hot 上的 explain
DELETE mytest
PUT mytest
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">settings</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
    </span><span style="color: #800000;">"</span><span style="color: #800000;">number_of_shards</span><span style="color: #800000;">"</span>:<span style="color: #800080;">2</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">number_of_replicas</span><span style="color: #800000;">"</span>:<span style="color: #800080;">1</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">index.routing.allocation.require.box_type</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">hot</span><span style="color: #800000;">"</span><span style="color: #000000;">
  }
}

GET _cluster</span>/<span style="color: #000000;">health
GET _cat</span>/shards/<span style="color: #000000;">mytest
GET </span>/_cluster/allocation/<span style="color: #000000;">explain

PUT mytest</span>/<span style="color: #000000;">_settings
{
    </span><span style="color: #800000;">"</span><span style="color: #800000;">number_of_replicas</span><span style="color: #800000;">"</span>: <span style="color: #800080;">0</span><span style="color: #000000;">
}</span></pre>
</div>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: #169fe6;"><span style="color: #ffffff;"><strong>四、提升集群写性能</strong></span></p>
<p><strong>1，关闭无关的功能</strong></p>
<p>①只需要聚合不需要搜索，index设置成false</p>
<p>②不需要算分，Norms设置成false</p>
<p>③不要对字符串使用默认的dynamic mapping。字段数量过多，会对性能产生比较大的印象</p>
<p>④index_options控制在创建倒排索引时，那些内容会被添加到倒排索引中。优化这些设置，一定程度上可以cpu</p>
<p>⑤关闭_source，减少io操作；（不能被reindex了，适合指标型数据）</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">PUT index
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">mappings</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">properties</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">foo</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">integer</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span>: <span style="color: #0000ff;">false</span><span style="color: #000000;">
      }
    }
  }
}

PUT index
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">mappings</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">properties</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">foo</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">norms</span><span style="color: #800000;">"</span>: <span style="color: #0000ff;">false</span><span style="color: #000000;">
      }
    }
  }
}</span></pre>
</div>
<p>2，一个索引设定的例子</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">DELETE myindex
PUT myindex
{
  </span><span style="color: #800000;">"</span><span style="color: #800000;">settings</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">refresh_interval</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">30s</span><span style="color: #800000;">"</span><span style="color: #000000;">,//30秒一次refresh
      </span><span style="color: #800000;">"</span><span style="color: #800000;">number_of_shards</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">2</span><span style="color: #800000;">"</span><span style="color: #000000;">
    },
    </span><span style="color: #800000;">"</span><span style="color: #800000;">routing</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">allocation</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">total_shards_per_node</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">3</span><span style="color: #800000;">"//控制分片，避免数据热点</span><span style="color: #000000;">
      }
    },
    </span><span style="color: #800000;">"</span><span style="color: #800000;">translog</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
      </span><span style="color: #800000;">"</span><span style="color: #800000;">sync_interval</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">30s</span><span style="color: #800000;">"</span><span style="color: #000000;">,//降低translog落盘
      </span><span style="color: #800000;">"</span><span style="color: #800000;">durability</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">async</span><span style="color: #800000;">"</span><span style="color: #000000;">
    },
    </span><span style="color: #800000;">"</span><span style="color: #800000;">number_of_replicas</span><span style="color: #800000;">"</span>: <span style="color: #800080;">0</span><span style="color: #000000;">
  },
  </span><span style="color: #800000;">"</span><span style="color: #800000;">mappings</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
    </span><span style="color: #800000;">"</span><span style="color: #800000;">dynamic</span><span style="color: #800000;">"</span>: <span style="color: #0000ff;">false</span><span style="color: #000000;">,//避免不必要的字段索引
    </span><span style="color: #800000;">"</span><span style="color: #800000;">properties</span><span style="color: #800000;">"</span><span style="color: #000000;">: {}
  }
}</span></pre>
</div>
<p>&nbsp;</p>