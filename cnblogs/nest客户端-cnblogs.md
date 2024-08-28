<p>一、客户端封装</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('ccc422ab-f84b-471d-b776-a08a3761333f')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_ccc422ab-f84b-471d-b776-a08a3761333f" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_ccc422ab-f84b-471d-b776-a08a3761333f" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_ccc422ab-f84b-471d-b776-a08a3761333f" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> Elasticsearch.Net;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Nest;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> esdemo
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ElasticsearchUtils
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> ElasticsearchUtils _elasticsearchUtils;
        </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
        <span style="color: #808080;">///</span><span style="color: #008000;"> Linq查询的官方Client
        </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
        <span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> IElasticClient _elasticLinqClient { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
        </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
        <span style="color: #808080;">///</span><span style="color: #008000;"> Js查询的官方Client
        </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
        <span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> IElasticLowLevelClient _elasticJsonClient { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

        </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> ElasticsearchUtils()
        {

        }
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">readonly</span> <span style="color: #0000ff;">object</span> eslock = <span style="color: #0000ff;">new</span> <span style="color: #0000ff;">object</span><span style="color: #000000;">();
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> ElasticsearchUtils GetInstance()
        {
            </span><span style="color: #0000ff;">if</span> (_elasticsearchUtils == <span style="color: #0000ff;">null</span><span style="color: #000000;">)
            {
                </span><span style="color: #0000ff;">lock</span><span style="color: #000000;"> (eslock)
                {
                    </span><span style="color: #0000ff;">if</span> (_elasticsearchUtils == <span style="color: #0000ff;">null</span><span style="color: #000000;">)
                    {
                        </span><span style="color: #0000ff;">var</span> urls = <span style="color: #800000;">"</span><span style="color: #800000;">http://192.168.0.150:9200</span><span style="color: #800000;">"</span><span style="color: #000000;">;
                        </span><span style="color: #0000ff;">var</span> username = <span style="color: #800000;">"</span><span style="color: #800000;">elastic</span><span style="color: #800000;">"</span><span style="color: #000000;">;
                        </span><span style="color: #0000ff;">var</span> passowrd = <span style="color: #800000;">"</span><span style="color: #800000;">123456</span><span style="color: #800000;">"</span><span style="color: #000000;">;
                        </span><span style="color: #0000ff;">var</span> uris = urls.Split(<span style="color: #800000;">"</span><span style="color: #800000;">,</span><span style="color: #800000;">"</span>).ToList().ConvertAll(x =&gt; <span style="color: #0000ff;">new</span> Uri(x));<span style="color: #008000;">//</span><span style="color: #008000;">配置节点地址，以，分开</span>
                        <span style="color: #0000ff;">var</span> connectionPool = <span style="color: #0000ff;">new</span> StaticConnectionPool(uris);<span style="color: #008000;">//</span><span style="color: #008000;">配置请求池</span>
                        <span style="color: #0000ff;">var</span> settings = <span style="color: #0000ff;">new</span><span style="color: #000000;"> ConnectionSettings(connectionPool)
                            .BasicAuthentication(username, passowrd)
                            .RequestTimeout(TimeSpan.FromSeconds(</span><span style="color: #800080;">30</span>));<span style="color: #008000;">//</span><span style="color: #008000;">请求配置参数</span>
                        _elasticLinqClient = <span style="color: #0000ff;">new</span><span style="color: #000000;"> ElasticClient(settings);
                        _elasticJsonClient </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> ElasticLowLevelClient(settings);
                        _elasticsearchUtils </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> ElasticsearchUtils();
                    }
                }
            }
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> _elasticsearchUtils;
        }

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> IElasticClient LinqClient()
        {
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> _elasticLinqClient;
        }


        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> IElasticLowLevelClient JsonClient()
        {
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> _elasticJsonClient;
        }


    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">ElasticsearchUtils</span></div>
<p>二、CURD</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('a5378fe5-55ea-4f1d-b20d-eb15886194a3')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_a5378fe5-55ea-4f1d-b20d-eb15886194a3" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_a5378fe5-55ea-4f1d-b20d-eb15886194a3" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_a5378fe5-55ea-4f1d-b20d-eb15886194a3" class="cnblogs_code_hide">
<pre> DataService dataService = <span style="color: #0000ff;">new</span><span style="color: #000000;"> DataService();
            </span><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> i = <span style="color: #800080;">0</span>; i &lt; <span style="color: #800080;">10000</span>; i++<span style="color: #000000;">)
            {
                </span><span style="color: #0000ff;">var</span> logs = dataService.GetSource(i * <span style="color: #800080;">10</span>, <span style="color: #800080;">10</span><span style="color: #000000;">);

                </span><span style="color: #0000ff;">var</span> logsv2 = <span style="color: #0000ff;">new</span> List&lt;request_audit_logs_v2&gt;<span style="color: #000000;">();
                </span><span style="color: #0000ff;">foreach</span> (<span style="color: #0000ff;">var</span> item <span style="color: #0000ff;">in</span><span style="color: #000000;"> logs)
                {
                    </span><span style="color: #008000;">//</span><span style="color: #008000;">var aa = JsonConvert.DeserializeObject&lt;dynamic&gt;(item.request_content);
                    </span><span style="color: #008000;">//</span><span style="color: #008000;">var aaa = aa.parm.Token;</span>
                    request_audit_logs_v2 log = <span style="color: #0000ff;">new</span><span style="color: #000000;"> request_audit_logs_v2();
                    log.api </span>=<span style="color: #000000;"> log.api;
                    log.key </span>=<span style="color: #000000;"> item.key;
                    log.post_type </span>=<span style="color: #000000;"> item.post_type;
                    log.url </span>=<span style="color: #000000;"> item.url;
                    log.request_content </span>=<span style="color: #000000;"> item.request_content;
                    log.hander </span>=<span style="color: #000000;"> item.hander;
                    log.status </span>=<span style="color: #000000;"> item.status;
                    log.response_content </span>=<span style="color: #000000;"> item.response_content;
                    log.request_time </span>= item.request_time.ToString(<span style="color: #800000;">"</span><span style="color: #800000;">yyyy-MM-dd HH:mm:ss</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                    log.response_time </span>= item.response_time.ToString(<span style="color: #800000;">"</span><span style="color: #800000;">yyyy-MM-dd HH:mm:ss</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                    log.exception </span>=<span style="color: #000000;"> item.exception;
                    log.run_time </span>=<span style="color: #000000;"> item.run_time;
                    log.thread_num </span>=<span style="color: #000000;"> item.thread_num;
                    log.create_time </span>= item.create_time.ToString(<span style="color: #800000;">"</span><span style="color: #800000;">yyyy-MM-dd HH:mm:ss</span><span style="color: #800000;">"</span><span style="color: #000000;">); 
                    log.modify_time </span>=item.modify_time.ToString(<span style="color: #800000;">"</span><span style="color: #800000;">yyyy-MM-dd HH:mm:ss</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                    log.user_name </span>=<span style="color: #000000;"> item.user_name;
                    logsv2.Add(log);
                    </span><span style="color: #008000;">//</span><span style="color: #008000;">var atters1 = ElasticsearchUtils.GetInstance().LinqClient().Bulk(p =&gt; p.Create&lt;object&gt;(c =&gt; c.Index("request_audit_logs").Document(log)));</span>
<span style="color: #000000;">
                }
                </span><span style="color: #0000ff;">var</span> bulkAllObserver = <span style="color: #0000ff;">new</span><span style="color: #000000;"> BulkAllObserver();
                </span><span style="color: #0000ff;">var</span> aa= ElasticsearchUtils.GetInstance().LinqClient().BulkAll(logsv2, f =&gt; f.Index(<span style="color: #800000;">"</span><span style="color: #800000;">request_audit_logs</span><span style="color: #800000;">"</span><span style="color: #000000;">));
                aa.Subscribe(bulkAllObserver);
            }
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">完成</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            Console.ReadKey();</span></pre>
</div>
<span class="cnblogs_code_collapse">Bulk与BulkAll</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('847b4aae-fcb1-4ed7-91f9-f78aa24921a6')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_847b4aae-fcb1-4ed7-91f9-f78aa24921a6" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_847b4aae-fcb1-4ed7-91f9-f78aa24921a6" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_847b4aae-fcb1-4ed7-91f9-f78aa24921a6" class="cnblogs_code_hide">
<pre> <span style="color: #0000ff;">var</span> aa = server.ElasticJsonClient.Update&lt;StringResponse&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">employees</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">DOBxx3MBH3d_nFQ4zJ-J</span><span style="color: #800000;">"</span><span style="color: #000000;">, PostData.Serializable(emp));
            </span><span style="color: #0000ff;">var</span> updateResponse = server.ElasticLinqClient.Update&lt;<span style="color: #0000ff;">object</span>&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">DOBxx3MBH3d_nFQ4zJ-J</span><span style="color: #800000;">"</span>, u =&gt;<span style="color: #000000;"> u
                                                                            .Index(</span><span style="color: #800000;">"</span><span style="color: #800000;">employees</span><span style="color: #800000;">"</span><span style="color: #000000;">)
                                                                            .Doc(</span><span style="color: #0000ff;">new</span><span style="color: #000000;">
                                                                            {
                                                                                name </span>= <span style="color: #800000;">"</span><span style="color: #800000;">new_name</span><span style="color: #800000;">"</span><span style="color: #000000;">
                                                                            })
                                                                            .DetectNoop(</span><span style="color: #0000ff;">false</span><span style="color: #000000;">)
                                                                        );</span></pre>
</div>
<span class="cnblogs_code_collapse">Update</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('e4e80b12-5f49-41e7-8e99-d3106ef5f93d')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_e4e80b12-5f49-41e7-8e99-d3106ef5f93d" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_e4e80b12-5f49-41e7-8e99-d3106ef5f93d" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_e4e80b12-5f49-41e7-8e99-d3106ef5f93d" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">var</span> searchResponse = client.Search&lt;Account&gt;(s =&gt;<span style="color: #000000;"> s
    .AllIndices()
    .Query(q </span>=&gt;<span style="color: #000000;"> q
        .Bool(b </span>=&gt;<span style="color: #000000;"> b
            .Must(m </span>=&gt; m.Term(p =&gt; p.User, <span style="color: #800000;">"</span><span style="color: #800000;">kimchy</span><span style="color: #800000;">"</span><span style="color: #000000;">))
            .Filter(f </span>=&gt; f.Term(p =&gt; p.Tags, <span style="color: #800000;">"</span><span style="color: #800000;">tech</span><span style="color: #800000;">"</span><span style="color: #000000;">))
            .MustNot(m </span>=&gt;<span style="color: #000000;"> m
                .Range(r </span>=&gt;<span style="color: #000000;"> r
                    .Field(p </span>=&gt;<span style="color: #000000;"> p.Age)
                    .GreaterThanOrEquals(</span><span style="color: #800080;">10</span><span style="color: #000000;">)
                    .LessThanOrEquals(</span><span style="color: #800080;">20</span><span style="color: #000000;">)
                )
            )
            .Should(
                sh </span>=&gt; sh.Term(p =&gt; p.Tags, <span style="color: #800000;">"</span><span style="color: #800000;">wow</span><span style="color: #800000;">"</span><span style="color: #000000;">),
                sh </span>=&gt; sh.Term(p =&gt; p.Tags, <span style="color: #800000;">"</span><span style="color: #800000;">elasticsearch</span><span style="color: #800000;">"</span><span style="color: #000000;">)
            )
            .MinimumShouldMatch(</span><span style="color: #800080;">1</span><span style="color: #000000;">)
            .Boost(</span><span style="color: #800080;">1.0</span><span style="color: #000000;">)
        )
    )
);</span></pre>
</div>
<span class="cnblogs_code_collapse">Query</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('51ddff1e-7a9d-4335-8a64-5e5ab5da6172')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_51ddff1e-7a9d-4335-8a64-5e5ab5da6172" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_51ddff1e-7a9d-4335-8a64-5e5ab5da6172" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_51ddff1e-7a9d-4335-8a64-5e5ab5da6172" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task&lt;Tuple&lt;<span style="color: #0000ff;">long</span>, List&lt;notify_announce_range_description&gt;&gt;&gt;<span style="color: #000000;"> GetListByPages(NotifyAnnounceRangeDescriptionGetListByPages data)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">var predicate = PredicateBuilder.New&lt;notify_announce_range_description&gt;();
            </span><span style="color: #008000;">//</span><span style="color: #008000;">predicate = predicate.And(t =&gt; t.system_tag == data.system_tag);</span>

            <span style="color: #0000ff;">var</span> conditions =<span style="color: #0000ff;">new</span> List&lt;Func&lt;QueryContainerDescriptor&lt;notify_announce_range_description&gt;, QueryContainer&gt;&gt;<span style="color: #000000;">();
            conditions.Add(f </span>=&gt; f.Term(p =&gt; p.is_deleted, <span style="color: #800080;">1</span><span style="color: #000000;">));
            </span><span style="color: #0000ff;">if</span> (data.system_tag &gt; <span style="color: #800080;">0</span><span style="color: #000000;">)
            {
                conditions.Add(f</span>=&gt;f.Term(p =&gt;<span style="color: #000000;"> p.system_tag, data.system_tag));
            }
            </span><span style="color: #0000ff;">if</span> (data.id != <span style="color: #0000ff;">null</span><span style="color: #000000;">)
            {
                conditions.Add(f </span>=&gt; f.Term(p =&gt;<span style="color: #000000;"> p.id, data.id));
            }

            </span><span style="color: #0000ff;">var</span> res = _elasticsearchUtils.LinqClient().Search&lt;notify_announce_range_description&gt;(a =&gt;<span style="color: #000000;"> {
                a.Index(</span><span style="color: #0000ff;">typeof</span><span style="color: #000000;">(notify_announce_range_description).Name);
                a.Query(q </span>=&gt;<span style="color: #000000;"> {
                    q.Bool(b </span>=&gt;<span style="color: #000000;"> {
                            b.Filter(conditions);
                        </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> b;
                    });
                    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> q;
                });
                a.PageBy(data);
                </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> a;
            });

            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> Tuple.Create(res.Total, res.Documents.ToList());
        }</span></pre>
</div>
<span class="cnblogs_code_collapse">query code</span></div>
<p>三、立即刷盘&amp;&amp;设置刷盘时间</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('70cc4cdc-b0e1-47f8-b108-ee3e4ae6c048')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_70cc4cdc-b0e1-47f8-b108-ee3e4ae6c048" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_70cc4cdc-b0e1-47f8-b108-ee3e4ae6c048" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_70cc4cdc-b0e1-47f8-b108-ee3e4ae6c048" class="cnblogs_code_hide">
<pre>        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task BaseUpdate&lt;T&gt;(T data, <span style="color: #0000ff;">string</span> storage_indexs = <span style="color: #0000ff;">null</span>) <span style="color: #0000ff;">where</span><span style="color: #000000;"> T : BaseEntity
        {
            _elasticsearchUtils.LinqClient().Bulk(b </span>=&gt;<span style="color: #000000;">
            {
                b.Update</span>&lt;T&gt;(c =&gt;<span style="color: #000000;">
                {
                    c.Index(GetIndex</span>&lt;T&gt;<span style="color: #000000;">(storage_indexs));
                    c.Id(data.id);
                    c.Doc(data);
                    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> c;
                });
                b.Refresh(Refresh.True);
                </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> b;
            });
        }</span></pre>
</div>
<span class="cnblogs_code_collapse">立即刷盘</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('6e791dc5-f910-4032-a19c-9d0b3a63e69d')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_6e791dc5-f910-4032-a19c-9d0b3a63e69d" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_6e791dc5-f910-4032-a19c-9d0b3a63e69d" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_6e791dc5-f910-4032-a19c-9d0b3a63e69d" class="cnblogs_code_hide">
<pre>PUT student/<span style="color: #000000;">_settings
{
    </span><span style="color: #800000;">"</span><span style="color: #800000;">index</span><span style="color: #800000;">"</span><span style="color: #000000;"> : {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">refresh_interval</span><span style="color: #800000;">"</span> : <span style="color: #800000;">"</span><span style="color: #800000;">1m</span><span style="color: #800000;">"</span><span style="color: #000000;">
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">设置刷盘时间</span></div>
<ul>
<li>ms: 毫秒</li>
<li>s: 秒</li>
<li>m: 分钟</li>
</ul>
<p>&nbsp;</p>