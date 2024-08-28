<p><a href="#a1"><strong>一、Redis安装</strong></a></p>
<p><a href="#a2"><strong>二、Redis命令</strong></a></p>
<p><a href="#a3"><strong><strong>三、StackExchange.Redis</strong></strong></a></p>
<p><a href="#a4"><strong><strong>四、四大结构体</strong></strong></a></p>
<p><a href="#a5"><strong><strong>五、Redis数据结构之String</strong></strong></a></p>
<p><strong><strong><a href="#a6">六、Redis数据结构之List</a></strong></strong></p>
<p><a href="#a7"><strong>七、Redis数据结构之Hash表</strong></a></p>
<p><a href="#a8"><strong>八、Redis数据结构之Set</strong></a></p>
<p><a href="#a9"><strong>九、Redis数据结构之sorted_set</strong></a></p>
<p><strong><strong><a href="#a10">十、Redis数据结构之hyperloglog</a></strong></strong></p>
<p><a href="#a11"><strong>十一、Transactions</strong></a></p>
<p><a href="#a12"><strong>十二、发布/订阅</strong></a></p>
<p><a href="#a13"><strong>十三、redis驱动批量执行命令</strong></a></p>
<p><a href="#a14"><strong><strong>十四、Redis使用Lua</strong></strong></a></p>
<p><a href="#a15"><strong><strong>十五、Redis两种持久化方式</strong></strong></a></p>
<p><a href="#a16"><strong><strong>十六、搭建Redis主-备（mster-slave）</strong></strong></a></p>
<p><a href="#a17"><strong>十七、搭建Redis主-备（mster-slave）+哨兵（sentinel）</strong></a></p>
<p><a href="#a18"><strong>十八、 web监控【redislive】</strong></a></p>
<p><a href="#a19"><strong>十九、&nbsp;搭建cluster（集群）</strong>&nbsp;</a></p>
<p>redis中文文档：<a href="http://www.redis.cn/" target="_blank">http://www.redis.cn/</a></p>
<p>redis可视化工具：<a href="https://raw.githubusercontent.com/caoxinyu/RedisClient/windows/release/redisclient-win32.x86.2.0.exe" target="_blank">https://raw.githubusercontent.com/caoxinyu/RedisClient/windows/release/redisclient-win32.x86.2.0.exe</a></p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;"><strong><a name="a1"></a>一、Redis安装</strong></span></p>
<p>1，Windows安装</p>
<p>①下载redis并安装msi文件</p>
<p>https://github.com/MicrosoftArchive/redis</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201801/741594-20180120181550928-1074320446.png" alt="" width="374" height="89" /></p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201801/741594-20180120182045459-1517801499.png" alt="" width="381" height="129" /></p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201801/741594-20180120183622193-125495878.png" alt="" width="409" height="271" /></p>
<p>&nbsp;</p>
<p>②设置环境变量</p>
<p>&nbsp;<img src="http://images2017.cnblogs.com/blog/741594/201801/741594-20180120182251599-1784279513.png" alt="" width="258" height="271" /></p>
<p>③运行server</p>
<p>redis-server D:\Redis\redis.windows-service.conf</p>
<p>④运行client</p>
<p>redis-cli</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201801/741594-20180120183505256-1633422520.png" alt="" width="409" height="138" /></p>
<p>&nbsp;</p>
<p>2，Linux安装</p>
<p>①进入usr-》local目录下</p>
<p>②$ wget http://download.redis.io/releases/redis-4.0.6.tar.gz&nbsp;　　下载redis</p>
<p>③$ tar xzf redis-4.0.6.tar.gz　　解压</p>
<p>④$ cd redis-4.0.6　　进入目录</p>
<p>⑤$ make　　编译</p>
<p>⑥编译好之后进入src文件下，发现编译好了几个可执行文件。将这几个文件考到sbin下面</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201801/741594-20180121154235240-456835426.png" alt="" width="382" height="135" /></p>
<p>⑦配置环境变量</p>
<p>/etc/profile 打开文件，设置</p>
<p>export PATH=$PATH:/usr/local/redis-4.0.6/sbin</p>
<p>⑧重启centOS&nbsp;</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a2"></a>二、Redis命令</span></strong></p>
<p>set username jack 设置缓存</p>
<p>get username 读取缓存</p>
<p>keys * 查看所有的key</p>
<p>flushall 清空所有数据（没有一点安全保证）</p>
<p>bgsave 立马持久化缓存信息</p>
<p>bind 127.0.0.1　　如果没有注销掉bind，则Redis监听所有链接</p>
<p>protected-mode yes【yes只能回路地址127.0.0.1 本地访问】</p>
<p><span style="font-size: 12px; color: #0000ff;">生产环境一般配置</span><br /><span style="font-size: 12px; color: #0000ff;">#bind</span><br /><span style="font-size: 12px; color: #0000ff;">protected-mode no</span></p>
<p>port 6379 配置redis端口</p>
<p>dir ./ 配置rdb和logfile的存放位置（例如：dir /usr/redis/sbin/db）</p>
<p>databases 16设置数据库的数量</p>
<p>logfile "server_log.txt"  指定日志文件名称</p>
<p>loglevel notice 日志记录级别</p>
<p>rename-command 改变命令的名称</p>
<p>redis-cli -h 192.168.1.102 -p 6379 远程链接redis</p>
<p>redis-cli -h 192.168.1.102 -p 6379 -a 123456 --stat 监控redis状态</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">设置密码：

在配置文件中设置requirepass（例如 requirepass </span><span style="color: #800080;">123456</span><span style="color: #000000;">）
连接redis服务器时需要带上密码（例如：redis</span>-cli -h <span style="color: #800080;">192.168</span>.<span style="color: #800080;">1.102</span> -p <span style="color: #800080;">6379</span> -a <span style="color: #800080;">123456</span>）</pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #ff0000;">redis远程链接失败总结
①看看redis-server指向的配置文件是否指定对了
②conf配置
#bind
protected-mode no
③关闭centOS的防火墙
systemctl stop firewalld.service #停止firewall
systemctl disable firewalld.service #禁止firewall开机启动</span></pre>
</div>
<p>1，设置key的过期时间<br />persist【O(1)】：PERSIST key【移除给定key的生存时间】<br />expire【O(1)】：EXPIRE key seconds【设置key的过期时间，单位秒】<br />pexpire【O(1)】：PEXPIRE key milliseconds【设置key的过期时间，单位毫秒】<br />expireat【O(1)】：EXPIREAT key timestamp【设置key的过期时间，单位时间戳】</p>
<p>2，Redis配置</p>
<p>①maxmemory设置最大内存空间（默认注释）</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201801/741594-20180127163031240-1011852957.png" alt="" /></p>
<p>&nbsp;</p>
<p>②maxmemory-policy最大内存空间策略（默认注释）</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201801/741594-20180127163040725-1615193251.png" alt="" /></p>
<p><span style="font-size: 12px; color: #ff0000;">策略：</span></p>
<p><span style="font-size: 12px; color: #ff0000;"># volatile-lru -&gt;&nbsp;删除使用LRU算法设置过期的key</span><br /><span style="font-size: 12px; color: #ff0000;"># allkeys-lru -&gt;根据LRU算法删除任何key</span><br /><span style="font-size: 12px; color: #ff0000;"># volatile-random -&gt;&nbsp;删除过期集合的key</span><br /><span style="font-size: 12px; color: #ff0000;"># allkeys-random -&gt;删除一个随机key，任何key</span><br /><span style="font-size: 12px; color: #ff0000;"># volatile-ttl -&gt;删除最接近过期时间的key</span><br /><span style="font-size: 12px; color: #ff0000;"># noeviction -&gt; 如果内存写满，则抛异常</span></p>
<p><span style="font-size: 12px; color: #ff0000;">lru ：最久未使用的&nbsp;</span></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a3"></a>三、StackExchange.Redis</span></strong></p>
<p>wireshark 网络封包分析软件</p>
<p>nuget StackExchange.Redis</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('eeb093a2-b202-4927-b3fc-8ec24ff348d4')"><img id="code_img_closed_eeb093a2-b202-4927-b3fc-8ec24ff348d4" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_eeb093a2-b202-4927-b3fc-8ec24ff348d4" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('eeb093a2-b202-4927-b3fc-8ec24ff348d4',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_eeb093a2-b202-4927-b3fc-8ec24ff348d4" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> RedisCache
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> ConnectionMultiplexer connection;
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> IDatabase database;

        </span><span style="color: #0000ff;">static</span><span style="color: #000000;"> RedisCache()
        {
            </span><span style="color: #0000ff;">var</span> options=<span style="color: #0000ff;">new</span><span style="color: #000000;"> ConfigurationOptions()
            {
                Password </span>= <span style="color: #800000;">"</span><span style="color: #800000;">123456</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                EndPoints </span>= { { <span style="color: #800000;">"</span><span style="color: #800000;">192.168.1.101</span><span style="color: #800000;">"</span>, <span style="color: #800080;">6379</span><span style="color: #000000;"> } }
            };
            connection </span>=<span style="color: #000000;"> ConnectionMultiplexer.Connect(options);
            database </span>=<span style="color: #000000;"> connection.GetDatabase();
        }
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Set(<span style="color: #0000ff;">string</span> key,<span style="color: #0000ff;">string</span><span style="color: #000000;"> str)
        {
            database.StringSet(key, str);
        }
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">string</span> Get(<span style="color: #0000ff;">string</span><span style="color: #000000;"> key)
        {
           </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> database.StringGet(key);
        }
    }</span></pre>
</div>
<span class="cnblogs_code_collapse">RedisCache</span></div>
<p>https://stackexchange.github.io/StackExchange.Redis/Configuration</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a4"></a>四、四大结构体</span></strong></p>
<p>1，RedisServer struct</p>
<p>2，RedisDb&nbsp;struct 标识一个db，config配置默认为16个RedisDb&nbsp;</p>
<p>3，RedisObject struct&nbsp;也就是对象化的数据结构表示</p>
<p>4，SDS struct char[] 一个包装类（存放字符串）</p>
<p>&nbsp;<img src="http://images2017.cnblogs.com/blog/741594/201801/741594-20180122221751412-1701431824.png" alt="" width="648" height="458" /></p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a5"></a>五、Redis数据结构之String</span></strong></p>
<p>1，get/set 命令（时间复杂度O(1)）</p>
<p>SET key value [EX seconds] [PX milliseconds] [NX|XX]</p>
<ul>
<li><code class="highlighter-rouge">EX</code>&nbsp;<em>seconds</em>&nbsp;&ndash; 设置键key的过期时间，单位时秒</li>
<li><code class="highlighter-rouge">PX</code>&nbsp;<em>milliseconds</em>&nbsp;&ndash; 设置键key的过期时间，单位时毫秒</li>
<li><code class="highlighter-rouge">NX</code>&nbsp;&ndash; 只有键key不存在的时候才会设置key的值</li>
<li><code class="highlighter-rouge">XX</code>&nbsp;&ndash; 只有键key存在的时候才会设置key的值</li>
</ul>
<div class="cnblogs_code">
<pre><span style="color: #000000;">案例：使用分布式锁
</span><span style="color: #0000ff;">set</span><span style="color: #000000;"> a a NX
业务操作
del a</span></pre>
</div>
<p>2，incr/decr/incrby/decrby</p>
<p>incr 自增加1（i++）</p>
<p>decr自增减1（i--）</p>
<p>incrby自增加n(i=i+n)</p>
<p>decrby自增减n（i=i-n）</p>
<p>如果存放string中的value是int，则内存使用int存储值</p>
<p>3，ttl key 查询key还有多长时间过期（-2 表示过期）</p>
<p>4，PSETEX/SETEX&nbsp;</p>
<p>PSETEX key milliseconds value<br />SETEX key seconds value<br />PSETEX和SETEX一样，唯一的区别是到期时间以毫秒为单位,而不是秒。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a6"></a>六、Redis数据结构之List</span></strong></p>
<p>双向链表</p>
<p>可以用作队列（lpush/rpop、rpush/lpop）或者栈(lpush/lpop、rpush/rpop)</p>
<p>一般用作队列</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201801/741594-20180123220051928-1320587093.png" alt="" width="642" height="423" /></p>
<p>&nbsp;</p>
<p>lpush：LPUSH key value [value ...]【将所有指定的值插入到存于 key 的列表的头部。如果 key 不存在，那么在进行 push 操作前会创建一个空列表】</p>
<p>lpop：LPOP key【移除并且返回 key 对应的 list 的第一个元素】</p>
<p>rpush：RPUSH key value [value ...]【向存于 key 的列表的尾部插入所有指定的值。如果 key 不存在，那么会创建一个空的列表然后再进行 push 操作】</p>
<p>rpop：RPOP key【移除并返回存于 key 的 list 的最后一个元素】</p>
<p>llen：LLEN key【返回存储在 key 里的list的长度。 如果 key 不存在，那么就被看作是空list，并且返回长度为 0】</p>
<p>blpop：BLPOP key [key ...] timeout【弹出最前面的值，如果列表中没有值，会阻塞】<br />brpop：BRPOP key [key ...] timeout【弹出最后面的值，如果列表中没有值，会阻塞】<br /><span style="font-size: 12px; color: #ff0000;">注：timeout：等待时间，单位秒。0：标识永久等待</span><br />lrange：LRANGE key start stop【返回存储在 key 的列表里指定范围内的元素】<br /><span style="font-size: 12px; color: #ff0000;">注：start stop位数组的下标</span></p>
<p>linsert：LINSERT key BEFORE|AFTER pivot value【把 value 插入存于 key 的列表中在基准值 pivot 的前面或后面】<br /><span style="font-size: 12px; color: #ff0000;">注：BEFORE为之前/AFTER为之后</span><br /><span style="font-size: 12px; color: #ff0000;">pivot：list中的值</span></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a7"></a>七、Redis数据结构之Hash表</span></strong></p>
<p>hget：HGET key field【返回 key 指定的哈希集中该字段所关联的值】<br />hset：HSET key field value<br /><span style="font-size: 12px; color: #ff0000;">设置 key 指定的哈希集中指定字段的值。</span><br /><span style="font-size: 12px; color: #ff0000;">如果 key 指定的哈希集不存在，会创建一个新的哈希集并与 key 关联。</span><br /><span style="font-size: 12px; color: #ff0000;">如果字段在哈希集中存在，它将被重写。</span><br /><span style="font-size: 12px; color: #ff0000;">field：字典中的key</span><br /><span style="font-size: 12px; color: #ff0000;">value：字典中的value</span></p>
<p>hdel：HDEL key field [field ...]【从 key 指定的哈希集中移除指定的域】<br />hexists：HEXISTS key field【返回hash里面field是否存在】<br />hgetall：HGETALL key【返回 key 指定的哈希集中所有的字段和值】<br />hkeys：HKEYS key【返回 key 指定的哈希集中所有字段的名字】<br />hlen：HLEN key【返回 key 指定的哈希集包含的字段的数量】<br />hmget：HMGET key field [field ...]【返回 key 指定的哈希集中指定字段的值】<br />hmset：HMSET key field value [field value ...]【设置 key 指定的哈希集中指定字段的值】<br />hvals：HVALS key【返回 key 指定的哈希集中所有字段的值】</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a8"></a>八、Redis数据结构之Set</span></strong></p>
<p>无value的字典</p>
<p>sadd【O(N)】：SADD key member [member ...]【添加一个或多个指定的member元素到集合的 key中】<br />scard【O(1)】：SCARD key【返回集合存储的key的基数 (集合元素的数量)】<br />sismember【O(1)】：SISMEMBER key member【检查成员member是否存在集合中】<br />smembers【O(N)】：SMEMBERS key【返回key集合所有的元素】<br />spop【O(1)】：SPOP key [count]【随机从集合弹出count（默认1）个值】<br />srem【O(N)】：SREM key member [member ...]【在key集合中移除指定的元素】</p>
<p>差集、交集、并集<br />sdiff【O(N)】：SDIFF key [key ...]【差集】<br />sdiffstore【O(N)】：SDIFFSTORE destination key [key ...]【将差集保存到destination中】<br />sinter【O(N*M)】：SINTER key [key ...]【交集】<br />sinterstore【O(N*M)】：SINTERSTORE destination key [key ...]【将交集保存到destination中】<br />sunion【O(N)】：SUNION key [key ...]【并集】<br />sunionstore【O(N)】：SUNIONSTORE destination key [key ...]【将并集保存到destination中】</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a9"></a>九、Redis数据结构之sorted_set</span></strong></p>
<p>一般用做优先级队列</p>
<p>zadd【O(log(N))】：ZADD key [NX|XX] [CH] [INCR] score member [score member ...]【将所有指定成员添加到键为key有序集合（sorted set）里面】<br /><span style="font-size: 12px; color: #ff0000;">XX: 仅仅更新存在的成员，不添加新成员。</span><br /><span style="font-size: 12px; color: #ff0000;">NX: 不更新存在的成员。只添加新成员。</span><br /><span style="font-size: 12px; color: #ff0000;">CH: 修改返回值为发生变化的成员总数，原始是返回新添加成员的总数 (CH 是 changed 的意思)。更改的元素是新添加的成员，已经存在的成员更新分数。 所以在命令中指定的成员有相同的分数将不被计算在内。注：在通常情况下，ZADD返回值只计算新添加成员的数量。</span><br /><span style="font-size: 12px; color: #ff0000;">INCR: 当ZADD指定这个选项时，成员的操作就等同ZINCRBY命令，对成员的分数进行递增操作。</span><br />zcard【O(1)】：ZCARD key【返回key的有序集元素个数】<br />zrange【O(log(N)+M)】：ZRANGE key start stop [WITHSCORES]【从小到大排序。显示字典信息（WITHSCORES 显示出key）】【例如：zrange sdic 0 -1 withscores】<br />zrevrange【O(log(N)+M)】：ZREVRANGE key start stop [WITHSCORES]【从大到小排序。显示字典信息（WITHSCORES 显示出key）】【例如：zrevrange sdic 0 -1 withscores】<br />zremrangebyrank【O(log(N)+M)】：ZREMRANGEBYRANK key start stop【移除有序集key中】<br /><span style="font-size: 12px; color: #ff0000;">0：最小</span><br /><span style="font-size: 12px; color: #ff0000;">-1：最大</span><br /><span style="font-size: 12px; color: #ff0000;">-2：第二大。。以此类推</span></p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201801/741594-20180125220148944-721265337.png" alt="" /></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a10"></a>十、Redis数据结构之hyperloglog</span></strong></p>
<p>等于distinct+count<br />计算不是100%准确<br />使用场景：计算某一天独立ip访问数量<br />pfadd 20180125 192.168.1.1 192.168.1.1 192.168.1.2【O(1)】<br />pfcount 20180125【O(1)】</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a11"></a>十一、Transactions</span></strong></p>
<p>multi：开启一个事务<br />exec：提交事务<br />discard：回滚事务</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201801/741594-20180126211342365-527880042.png" alt="" /></p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201801/741594-20180126211359803-784420630.png" alt="" /></p>
<p>watch【乐观锁】：WATCH key [key ...]</p>
<p>例如客户端1watch username并开启了一个事务。当在另一个客户端2修改了username值的时候。客户端1事务exec会执行失败（回滚）</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201801/741594-20180126212012444-1232957836.png" alt="" /></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a12"></a>十二、发布/订阅</span></strong></p>
<p>subscribe：SUBSCRIBE channel [channel ...]【订阅频道】<br />publish：PUBLISH channel message【发布消息】</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201801/741594-20180126215734647-1822427912.png" alt="" /></p>
<p>&nbsp;psubscribe：PSUBSCRIBE pattern [pattern ...]【订阅给定的模式的频道】</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201801/741594-20180126220028100-312432252.png" alt="" /></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a13"></a>十三、redis驱动批量执行命令</span></strong></p>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #0000ff;">var</span> con= ConnectionMultiplexer.Connect(<span style="color: #800000;">"</span><span style="color: #800000;">192.168.1.102:6379</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            </span><span style="color: #0000ff;">var</span> db =<span style="color: #000000;"> con.GetDatabase();

            </span><span style="color: #0000ff;">var</span> batch=<span style="color: #000000;"> db.CreateBatch();

            batch.SetAddAsync(</span><span style="color: #800000;">"</span><span style="color: #800000;">username</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            batch.ListInsertBeforeAsync(</span><span style="color: #800000;">"</span><span style="color: #800000;">list</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">1</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">2</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            batch.HashSetAsync(</span><span style="color: #800000;">"</span><span style="color: #800000;">dic</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">username</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">jack</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            batch.Execute();
            Console.ReadKey();
        }</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a14"></a>十四、Redis使用Lua</span></strong></p>
<p>Lua工具下载地址：<a href="http://static.runoob.com/download/LuaForWindows_v5.1.4-46.exe" target="_blank">LuaForWindows_v5.1.4-46.exe</a></p>
<p>1，命令<br />EVAL script numkeys key [key ...] arg [arg ...]<br />script：指定lua脚本的路径。或者直接写lua脚本<br />numkeys：制定参数的个数<br />key：在脚本中使用到的key（KEYS 全局key集合。单项：KEYS[1]）<br />arg：在脚本中使用到的arg（ARGV 全局arg集合。单项：ARGV[1]）<br /><span style="font-size: 12px; color: #ff0000;">注：KEYS[0]或者ARGV[0]是错误的写法</span></p>
<p>2，Lua脚本调用Redis<br />redis.call('set','foo','bar')<br />redis.pcall('hset','dic','key','value')<br />redis.call() 与 redis.pcall()很类似, 他们唯一的区别是当redis命令执行结果返回错误时， <br />redis.call()将返回给调用者一个错误，而redis.pcall()会将捕获的错误以Lua表的形式返回</p>
<p>3，案例<br />①直接嵌入lua脚本</p>
<div class="cnblogs_code">
<pre>&gt; eval <span style="color: #800000;">"</span><span style="color: #800000;">return {KEYS[1],KEYS[2],ARGV[1],ARGV[2]}</span><span style="color: #800000;">"</span> <span style="color: #800080;">2</span><span style="color: #000000;"> key1 key2 first second
</span><span style="color: #800080;">1</span>) <span style="color: #800000;">"</span><span style="color: #800000;">key1</span><span style="color: #800000;">"</span>
<span style="color: #800080;">2</span>) <span style="color: #800000;">"</span><span style="color: #800000;">key2</span><span style="color: #800000;">"</span>
<span style="color: #800080;">3</span>) <span style="color: #800000;">"</span><span style="color: #800000;">first</span><span style="color: #800000;">"</span>
<span style="color: #800080;">4</span>) <span style="color: #800000;">"</span><span style="color: #800000;">second</span><span style="color: #800000;">"</span></pre>
</div>
<p>②调用独立的lua脚本</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('d64bba0b-cca5-4a17-83b9-37e95a310056')"><img id="code_img_closed_d64bba0b-cca5-4a17-83b9-37e95a310056" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_d64bba0b-cca5-4a17-83b9-37e95a310056" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('d64bba0b-cca5-4a17-83b9-37e95a310056',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_d64bba0b-cca5-4a17-83b9-37e95a310056" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">return</span> {KEYS[<span style="color: #800080;">1</span>],KEYS[<span style="color: #800080;">2</span>],ARGV[<span style="color: #800080;">1</span>],ARGV[<span style="color: #800080;">2</span>]}</pre>
</div>
<span class="cnblogs_code_collapse">lua文件</span></div>
<div class="cnblogs_code">
<pre>redis-cli <span style="color: #008000;">--</span><span style="color: #008000;">eval C:\Users\Hunter2\Desktop\Lua\text.lua a b , a b</span>
<span style="color: #800080;">1</span>) <span style="color: #800000;">"</span><span style="color: #800000;">key1</span><span style="color: #800000;">"</span>
<span style="color: #800080;">2</span>) <span style="color: #800000;">"</span><span style="color: #800000;">key2</span><span style="color: #800000;">"</span>
<span style="color: #800080;">3</span>) <span style="color: #800000;">"</span><span style="color: #800000;">first</span><span style="color: #800000;">"</span>
<span style="color: #800080;">4</span>) <span style="color: #800000;">"</span><span style="color: #800000;">second</span><span style="color: #800000;">"</span></pre>
</div>
<p>③更高级的调用</p>
<p>需求：输入的参数在集合中存在，则打印出来</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201801/741594-20180127210430240-1211464296.png" alt="" /></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('4b39cd7a-8f70-40da-8ab7-41897d9b3e15')"><img id="code_img_closed_4b39cd7a-8f70-40da-8ab7-41897d9b3e15" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_4b39cd7a-8f70-40da-8ab7-41897d9b3e15" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('4b39cd7a-8f70-40da-8ab7-41897d9b3e15',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_4b39cd7a-8f70-40da-8ab7-41897d9b3e15" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">local</span> key=KEYS[<span style="color: #800080;">1</span><span style="color: #000000;">]
</span><span style="color: #0000ff;">local</span> args=<span style="color: #000000;">ARGV

</span><span style="color: #0000ff;">local</span> result=<span style="color: #000000;">{}
</span><span style="color: #0000ff;">local</span> list=redis.call(<span style="color: #800000;">"</span><span style="color: #800000;">smembers</span><span style="color: #800000;">"</span><span style="color: #000000;">,key)
</span><span style="color: #0000ff;">for</span> m,n <span style="color: #0000ff;">in</span> <span style="color: #ff00ff;">ipairs</span>(args) <span style="color: #0000ff;">do</span>
    <span style="color: #0000ff;">local</span> exists= redis.call(<span style="color: #800000;">"</span><span style="color: #800000;">sismember</span><span style="color: #800000;">"</span><span style="color: #000000;">,key,n)
    </span><span style="color: #0000ff;">if</span>(exists==<span style="color: #800080;">1</span>)<span style="color: #0000ff;">then</span>
    <span style="color: #ff00ff;">table.insert</span><span style="color: #000000;">(result,n)
    </span><span style="color: #0000ff;">end</span>
<span style="color: #0000ff;">end</span>
<span style="color: #0000ff;">return</span> result</pre>
</div>
<span class="cnblogs_code_collapse">Lua文件</span></div>
<div class="cnblogs_code">
<pre>C:\WINDOWS\system32&gt;redis-cli <span style="color: #008000;">--</span><span style="color: #008000;">eval C:\Users\Hunter2\Desktop\Lua\text.lua list , 1 2 3 10</span>
<span style="color: #800080;">1</span>) <span style="color: #800000;">"</span><span style="color: #800000;">1</span><span style="color: #800000;">"</span>
<span style="color: #800080;">2</span>) <span style="color: #800000;">"</span><span style="color: #800000;">2</span><span style="color: #800000;">"</span>
<span style="color: #800080;">3</span>) <span style="color: #800000;">"</span><span style="color: #800000;">3</span><span style="color: #800000;">"</span></pre>
</div>
<p><span style="font-size: 12px; color: #ff0000;">注：逗号分割key和agrv&nbsp;</span></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a15"></a>十五、Redis两种持久化方式</span></strong></p>
<p>1，rds（默认）<br />快照模式，定时保存。如果重启有可能会丢失部分数据</p>
<p>配置信息：</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201801/741594-20180127215343709-210745059.png" alt="" /></p>
<p>强制持久化命令：save（客户端阻塞）或者bgsave（会开启一个进程执行）</p>
<p>2，aof</p>
<p>来一条命令则保存一次，aof文件保存的是文本协议</p>
<p>开启方式&nbsp;</p>
<p>①注销save</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201801/741594-20180127215640834-2080389915.png" alt="" /></p>
<p>②appendonly设置为yes</p>
<p>&nbsp;<img src="http://images2017.cnblogs.com/blog/741594/201801/741594-20180127215728584-1747654685.png" alt="" /></p>
<p>三种写入模式：</p>
<p>#appendfsync always：来一条保存一条，强制保存到硬盘【安全性高，性能差】<br />appendfsync everysec：1秒强制保存到硬盘一次【折中方案】<br />#appendfsync no：来一条保存一条，只保存到系统的缓冲期，至于保存到硬盘是有系统决定【安全性差，性能高】</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a16"></a>十六、搭建Redis主-备（mster-slave）</span></strong></p>
<p>1，配置mster-slave<br />配置文件# slaveof &lt;masterip&gt; &lt;masterport&gt;配置主机地址<br />例如:slaveof 192.168.1.102 6379<br />如果主redis有密码需要配置# masterauth &lt;master-password&gt;<br />info 查看redis信息</p>
<p><span style="font-size: 12px; color: #ff0000;">注：一旦redis服务器被设置为slave，则该redis不能写入了。只能从master中写入</span></p>
<p>2，c#中使用</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('ce54840e-b445-45a6-99a2-e9da9778cc18')"><img id="code_img_closed_ce54840e-b445-45a6-99a2-e9da9778cc18" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_ce54840e-b445-45a6-99a2-e9da9778cc18" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('ce54840e-b445-45a6-99a2-e9da9778cc18',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_ce54840e-b445-45a6-99a2-e9da9778cc18" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> StackExchange.Redis;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ConsoleApp1
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #0000ff;">var</span> con= ConnectionMultiplexer.Connect(<span style="color: #800000;">"</span><span style="color: #800000;">192.168.1.102:6379,192.168.1.103:6379</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            </span><span style="color: #0000ff;">var</span> db =<span style="color: #000000;"> con.GetDatabase();

            db.StringAppendAsync(</span><span style="color: #800000;">"</span><span style="color: #800000;">password</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">123456</span><span style="color: #800000;">"</span>);<span style="color: #008000;">//</span><span style="color: #008000;">会使用主redis</span>
            <span style="color: #0000ff;">var</span> p = db.StringGetAsync(<span style="color: #800000;">"</span><span style="color: #800000;">password</span><span style="color: #800000;">"</span>).Result;<span style="color: #008000;">//</span><span style="color: #008000;">会使用备redis</span>
<span style="color: #000000;">
            Console.WriteLine(p);
            Console.ReadKey();
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">c#端调用</span></div>
<p><span style="font-size: 12px; color: #ff0000;">注：如果主redis挂了，则写入会失败。可以查询</span></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a17"></a>十七、搭建Redis主-备（mster-slave）+哨兵（sentinel）</span></strong></p>
<p>sentinel监视redis主备，当主redis挂了，sentinel自动让一个slave变为master。<br />当原来master恢复之后，原来master恢复已经成为slave了</p>
<p>1，架构sentinel</p>
<p>例如在一台centos上建立三个哨兵</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201801/741594-20180128204956225-471824403.png" alt="" width="451" height="133" /></p>
<p>这三个哨兵会监视一个master，当有2个哨兵主观认为master挂了，则sentinel自动让一个slave变为master</p>
<p>主redis：192.168.1.102:6379</p>
<p>备redis：192.168.1.103:6379</p>
<p>主redis未挂时，备redis的状态：</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201801/741594-20180128215446834-2137149938.png" alt="" /></p>
<p>主redis挂了，备redis的状态：</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201801/741594-20180128215510178-939599751.png" alt="" /></p>
<p>sentinel案例下载：<a href="https://pan.baidu.com/s/1ggvCu47" target="_blank">https://pan.baidu.com/s/1ggvCu47</a></p>
<p>1，配置具体的sentinel</p>
<p>①拷贝redis-sentinel程序和sentinel.conf配置文件到s1、s2、s3文件中</p>
<p>②配置sentinel.conf</p>
<p>port 26379 &nbsp;#设置sentinel的端口</p>
<p>protected-mode no #将protected-mode设置为no</p>
<p>sentinel monitor &lt;master-name&gt; &lt;ip&gt; &lt;redis-port&gt; &lt;quorum&gt; #设置监控的master</p>
<p><span style="font-size: 12px; color: #ff0000;">master-name：设置主redis 的名称，随便写</span></p>
<p><span style="font-size: 12px; color: #ff0000;">ip：主redis 的ip地址</span></p>
<p><span style="font-size: 12px; color: #ff0000;">redis-port：主redis的端口号</span></p>
<p><span style="font-size: 12px; color: #ff0000;">quorum：当主观认为master挂掉的哨兵达到2个时，则客观认为master挂了。需要切换master了</span></p>
<p><span style="font-size: 12px; color: #ff0000;">例：sentinel monitor mymaster 192.168.1.102 6379 2</span></p>
<p>sentinel auth-pass &lt;master-name&gt; &lt;password&gt; #如果master设置了密码，则需要配置master的密码</p>
<p><span style="font-size: 12px; color: #ff0000;">例：sentinel auth-pass&nbsp;mymaster 123456</span></p>
<p>sentinel down-after-milliseconds mymaster 30000 #master30秒没响应，则主观认为master挂了</p>
<p>③启动sentinel</p>
<p>进入放置sentinel的文件夹</p>
<p>执行命令./redis-sentinel ./sentinel.conf 启动sentinel</p>
<p><span style="font-size: 12px; color: #ff0000;">注意：在同一系统下运行多个sentinel，sentinel的端口号不要重复</span></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a18"></a>十八、 web监控【redislive】</span></strong></p>
<p>python写的一个web监控</p>
<p>1，安装redislive</p>
<p>①首先需要安装pip（python的安装工具包pip-9.0.1.tar.gz）【相当于nuget】<br />下载地址：<a href="https://pypi.python.org/pypi/pip" target="_blank">https://pypi.python.org/pypi/pip</a></p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201801/741594-20180129220756703-1084435550.png" alt="" width="494" height="152" /></p>
<p>网速慢可以下载：<a href="https://pan.baidu.com/s/1qZezffm" target="_blank">https://pan.baidu.com/s/1qZezffm</a></p>
<p>拷贝到centos的usr文件下，解压，进入解压文件中<br />python setup.py install 安装</p>
<p>②安装tornado【相当于iis】<br />pip install tornado --upgrade</p>
<p>③安装redis.py 【python redis驱动，相当于.net StackExchange】<br />pip install redis</p>
<p>④安装python-dateutil 【类库，相当于dll】<br />pip install python-dateutil --upgrade 强制更新到最新</p>
<p>⑤获取redislive的源代码<br />https://github.com/nkrode/RedisLive<br />解压放到centos的usr文件下。进入文件夹<br />将redis-live.conf.example改为redis-live.conf</p>
<div class="cnblogs_code">
<pre>redis-<span style="color: #000000;">live.conf配置文件解析：
RedisServers：监控的RedisServers的服务器地址和端口
DataStoreType：存储类型（redis或者Sqlite存储，默认redis）
RedisStatsServer：配置存储redis的服务器地址和端口</span></pre>
</div>
<div class="cnblogs_code" onclick="cnblogs_code_show('445e2dc1-279a-4f47-8cf6-6682bc2b096f')"><img id="code_img_closed_445e2dc1-279a-4f47-8cf6-6682bc2b096f" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_445e2dc1-279a-4f47-8cf6-6682bc2b096f" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('445e2dc1-279a-4f47-8cf6-6682bc2b096f',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_445e2dc1-279a-4f47-8cf6-6682bc2b096f" class="cnblogs_code_hide">
<pre><span style="color: #000000;">{
    </span><span style="color: #800000;">"</span><span style="color: #800000;">RedisServers</span><span style="color: #800000;">"</span><span style="color: #000000;">:
    [ 
        {
              </span><span style="color: #800000;">"</span><span style="color: #800000;">server</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">192.168.1.103</span><span style="color: #800000;">"</span><span style="color: #000000;">,
              </span><span style="color: #800000;">"</span><span style="color: #800000;">port</span><span style="color: #800000;">"</span> : <span style="color: #800080;">6379</span><span style="color: #000000;">
        }        
    ],

    </span><span style="color: #800000;">"</span><span style="color: #800000;">DataStoreType</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">redis</span><span style="color: #800000;">"</span><span style="color: #000000;">,

    </span><span style="color: #800000;">"</span><span style="color: #800000;">RedisStatsServer</span><span style="color: #800000;">"</span><span style="color: #000000;">:
    {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">server</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">192.168.1.103</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">port</span><span style="color: #800000;">"</span> : <span style="color: #800080;">6379</span><span style="color: #000000;">
    },
    
    </span><span style="color: #800000;">"</span><span style="color: #800000;">SqliteStatsStore</span><span style="color: #800000;">"</span><span style="color: #000000;"> :
    {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">path</span><span style="color: #800000;">"</span>:  <span style="color: #800000;">"</span><span style="color: #800000;">to your sql lite file</span><span style="color: #800000;">"</span><span style="color: #000000;">
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">配置案例</span></div>
<p>⑥开启监控脚本：./redis-monitor.py --duration=120【duration=120 默认采集二分钟】</p>
<p>⑦开启web站点：./redis-live.py</p>
<p>⑧访问<br />http://localhost:8888/index.html<br />http://192.168.1.103:8888/index.html</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;"><strong><a name="a19"></a>十九、&nbsp;搭建cluster（集群）</strong></span></p>
<p>参考文档：<a href="http://www.redis.cn/topics/cluster-tutorial.html" target="_blank">http://www.redis.cn/topics/cluster-tutorial.html</a></p>
<p>可能出现各种依赖问题请参考：<br /><a href="https://www.cnblogs.com/carryping/p/7447823.html" target="_blank">https://www.cnblogs.com/carryping/p/7447823.html</a><br /><a href="http://blog.csdn.net/Hello_World_QWP/article/details/78260684" target="_blank">http://blog.csdn.net/Hello_World_QWP/article/details/78260684</a><br /><a href="http://blog.csdn.net/hello_world_qwp/article/details/78261618" target="_blank">http://blog.csdn.net/hello_world_qwp/article/details/78261618</a></p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201801/741594-20180130210732281-310554798.png" alt="" /></p>
<p>1，开启cluster（集群）模式<br />配置文件：<br />cluster-enabled yes	开启集群<br />cluster-config-file nodes-6379.conf	集群节点文件</p>
<p>2，redis src下找到redis-trib.rb<br />①安装ruby环境：yum install ruby</p>
<p>②ruby的redis驱动：gem install redis<br />③rubygems安装：yum install -y rubygems</p>
<p>④通过第三方工具进行安装<br />./redis-trib.rb create --replicas 1 192.168.1.103:6379 192.168.1.103:6380 192.168.1.103:6381 192.168.1.103:6382</p>
<p>cluster nodes 查看集群<br />redis-cli -c 使用这种redis-cli的开启方式</p>
<p>3，c#驱动访问方式：</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('26a30a7d-8507-4a65-9cb1-29e12652a7f5')"><img id="code_img_closed_26a30a7d-8507-4a65-9cb1-29e12652a7f5" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_26a30a7d-8507-4a65-9cb1-29e12652a7f5" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('26a30a7d-8507-4a65-9cb1-29e12652a7f5',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_26a30a7d-8507-4a65-9cb1-29e12652a7f5" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> StackExchange.Redis;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ConsoleApp1
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #0000ff;">var</span> con= ConnectionMultiplexer.Connect(<span style="color: #800000;">"</span><span style="color: #800000;">192.168.1.103:6379,192.168.1.103:6380,192.168.1.103:6381,192.168.1.103:6382</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            </span><span style="color: #0000ff;">var</span> db =<span style="color: #000000;"> con.GetDatabase();

            db.StringSet(</span><span style="color: #800000;">"</span><span style="color: #800000;">cc</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">123456</span><span style="color: #800000;">"</span>);<span style="color: #008000;">//</span><span style="color: #008000;">会使用主redis</span>
            <span style="color: #0000ff;">var</span> p = db.StringGetAsync(<span style="color: #800000;">"</span><span style="color: #800000;">cc</span><span style="color: #800000;">"</span>).Result;<span style="color: #008000;">//</span><span style="color: #008000;">会使用备redis</span>
<span style="color: #000000;">
            Console.WriteLine(p);
            Console.ReadKey();
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<p><span style="font-size: 12px; color: #ff0000;">升级完ruby需要重启</span></p>
<p><span style="font-size: 12px; color: #ff0000;">注意：</span></p>
<p><span style="font-size: 12px; color: #ff0000;">&gt;&gt;&gt;创建群集</span><br /><span style="font-size: 12px; color: #ff0000;">***错误：集群创建的配置无效。</span><br /><span style="font-size: 12px; color: #ff0000;">*** Redis群集至少需要3个主节点。</span><br /><span style="font-size: 12px; color: #ff0000;">***对于每个节点3个节点和1个副本，这是不可能的。</span><br /><span style="font-size: 12px; color: #ff0000;">***至少需要6个节点。</span></p>
<p>&nbsp;</p>