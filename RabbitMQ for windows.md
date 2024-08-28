<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">一、搭建环境</span></p>
<p>Rabbit MQ 是建立在强大的Erlang OTP平台上，因此安装RabbitMQ之前要先安装Erlang。</p>
<p>erlang：<a href="http://www.erlang.org/download.html" target="_blank">http://www.erlang.org/download.html</a></p>
<p>rabbitmq：<a href="http://www.rabbitmq.com/download.html" target="_blank">http://www.rabbitmq.com/download.html</a></p>
<p>我目前使用的：<a href="http://pan.baidu.com/s/1eS8Dhse" target="_blank">http://pan.baidu.com/s/1eS8Dhse</a></p>
<p>默认安装的Rabbit MQ 监听端口是：5672</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">二、配置</span></p>
<p>1. 安装完以后erlang需要手动设置ERLANG_HOME 的系统变量。</p>
<p>输入：set&nbsp;ERLANG_HOME=C:\Program Files\erl9.0</p>
<p>2，打开cmd定位到rabbitmq的安装路径：C:\Program Files\RabbitMQ Server\rabbitmq_server-3.6.10\sbin</p>
<p>上述命令回车后接着输入rabbitmqctl status，回车后出现下面一坨的即说明安装没有问题：</p>
<p><img src="http://img.blog.csdn.net/20160321150710124?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center" alt="" /></p>
<p><span style="color: #ff0000;">出现问题： Error:unable to connect to node rabbit@Hunter:nodedown</span><br /><span style="color: #ff0000;">也不知道怎么回事，重新安装了下rabbitmq-server-3.6.10</span></p>
<p>3，rabbitmq-plugins enable rabbitmq_management（安装 RabbitMQWeb的管理插件。此时，已经可以通过&nbsp;http://127.0.0.1:15672/ 地址来访问web管理界面了，默认的账户和密码均是 guest。但实际使用时可能需要重新一个新的管理账户）　　&nbsp;</p>
<p>4，rabbitmqctl.bat add_user zhangdi 123456（创建管理用户，这一步还不能登录）</p>
<p>5，rabbitmqctl.bat set_user_tags zhangdi&nbsp;administrator（设置管理员，可以登录了）</p>
<p>6，rabbitmqctl.bat set_permissions -p / &nbsp;zhangdi&nbsp;".*" ".*" ".*"（授予管理员权限）</p>
<p>7，其他命令</p>
<p>　　a. 查询用户： rabbitmqctl.bat list_users</p>
<p>　　b. 查询vhosts： rabbitmqctl.bat list_vhosts</p>
<p>　　c. 启动RabbitMQ服务: net stop RabbitMQ &amp;&amp; net start RabbitMQ</p>
<p>8，centos配置</p>
<p><a href="https://ken.io/note/centos7-rabbitmq-install-setup#H3-7" target="_blank">https://ken.io/note/centos7-rabbitmq-install-setup#H3-7</a></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('fb36efc4-b237-40a1-be0f-209c49987347')"><img id="code_img_closed_fb36efc4-b237-40a1-be0f-209c49987347" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_fb36efc4-b237-40a1-be0f-209c49987347" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('fb36efc4-b237-40a1-be0f-209c49987347',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_fb36efc4-b237-40a1-be0f-209c49987347" class="cnblogs_code_hide">
<pre><span style="color: #000000;">#添加用户
sudo rabbitmqctl add_user admin pwd

#设置用户角色
sudo rabbitmqctl set_user_tags admin administrator

#tag（administrator，monitoring，policymaker，management）

#设置用户权限(接受来自所有Host的所有操作)
sudo rabbitmqctl  set_permissions </span>-p <span style="color: #800000;">"</span><span style="color: #800000;">/</span><span style="color: #800000;">"</span> admin <span style="color: #800000;">'</span><span style="color: #800000;">.*</span><span style="color: #800000;">'</span> <span style="color: #800000;">'</span><span style="color: #800000;">.*</span><span style="color: #800000;">'</span> <span style="color: #800000;">'</span><span style="color: #800000;">.*</span><span style="color: #800000;">'</span><span style="color: #000000;">  

#查看用户权限
sudo rabbitmqctl list_user_permissions admin</span></pre>
</div>
<span class="cnblogs_code_collapse">centos配置用户</span></div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>新版配置：</p>
<p>下载地址：<a href="https://pan.baidu.com/s/18-rLh0e3mSY0xX4YfDqi3g" target="_blank">https://pan.baidu.com/s/18-rLh0e3mSY0xX4YfDqi3g</a></p>
<p>参考地址：<a href="https://blog.csdn.net/hzw19920329/article/details/53156015" target="_blank">https://blog.csdn.net/hzw19920329/article/details/53156015</a></p>
<p>1，下载安装erlang<br />①添加系统变量：ERLANG_HOME=C:\Program Files\erl9.3（安装路径）<br />②添加系统变量path：C:\Program Files\erl9.3\bin<br />③测试安装是否成功：打开cmd 输入erl，如果出现erlang的版本信息就表示erlang语言环境安装成功</p>
<p>2，下载安装RabbitMQ<br />注意：安装目录不能存在空格，最好安装到c盘（我安装rabbitmq到D盘出错）<br />①cmd进入C:\RabbitMQServer\rabbitmq_server-3.7.4\sbin目录 输入：rabbitmq-plugins enable rabbitmq_management安装管理界面</p>
<p>②安装完成进入http://localhost:15672，默认管理员和密码都是guest</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">三、C#使用RabbitMQ（使用EasyNetQ）</span></p>
<p>&nbsp;<img src="http://images2015.cnblogs.com/blog/741594/201707/741594-20170702214214055-648861262.jpg" alt="" /></p>
<p><span style="font-size: 14px;"><strong>1，MQ.Common</strong></span></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('c24183b9-edd1-42b4-a4a4-c8a648609de5')"><img id="code_img_closed_c24183b9-edd1-42b4-a4a4-c8a648609de5" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_c24183b9-edd1-42b4-a4a4-c8a648609de5" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('c24183b9-edd1-42b4-a4a4-c8a648609de5',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_c24183b9-edd1-42b4-a4a4-c8a648609de5" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> EasyNetQ;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> MQ.Common
{
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
    <span style="color: #808080;">///</span><span style="color: #008000;"> 消息服务器连接器
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> BusBuilder
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> IBus CreateMessageBus()
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> 消息服务器连接字符串
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> var connectionString = ConfigurationManager.ConnectionStrings["RabbitMQ"];
            </span><span style="color: #008000;">//</span><span style="color: #008000;">string connString = "host=192.168.98.107:5672;virtualHost=OrderQueue;username=zhangdi;password=123456";</span>
            <span style="color: #0000ff;">string</span> connString = <span style="color: #800000;">"</span><span style="color: #800000;">host=127.0.0.1:5672;virtualHost=text;username=zhangdi;password=123456</span><span style="color: #800000;">"</span><span style="color: #000000;">;
            </span><span style="color: #0000ff;">if</span>(<span style="color: #0000ff;">string</span><span style="color: #000000;">.IsNullOrEmpty(connString))
                </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> Exception(<span style="color: #800000;">"</span><span style="color: #800000;">messageserver connection string is missing or empty</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> RabbitHutch.CreateBus(connString);
        }

    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">BusBuilder</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('3e1aff3b-949a-41c3-857d-b7c0ce77c6d8')"><img id="code_img_closed_3e1aff3b-949a-41c3-857d-b7c0ce77c6d8" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_3e1aff3b-949a-41c3-857d-b7c0ce77c6d8" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('3e1aff3b-949a-41c3-857d-b7c0ce77c6d8',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_3e1aff3b-949a-41c3-857d-b7c0ce77c6d8" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> MQ.Common
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IProcessMessage
    {
        </span><span style="color: #0000ff;">void</span><span style="color: #000000;"> ProcessMsg(Message msg);
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">IProcessMessage</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('11d06f08-c19b-479d-a926-ef47d208c092')"><img id="code_img_closed_11d06f08-c19b-479d-a926-ef47d208c092" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_11d06f08-c19b-479d-a926-ef47d208c092" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('11d06f08-c19b-479d-a926-ef47d208c092',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_11d06f08-c19b-479d-a926-ef47d208c092" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> EasyNetQ;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> MQ.Common
{
    </span><span style="color: #0000ff;">public</span>  <span style="color: #0000ff;">class</span><span style="color: #000000;"> Message
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> MessageID { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> MessageTitle { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> MessageBody { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> MessageRouter { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Message</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('7e49298c-a2c3-4c66-b83e-0c36c0f101cf')"><img id="code_img_closed_7e49298c-a2c3-4c66-b83e-0c36c0f101cf" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_7e49298c-a2c3-4c66-b83e-0c36c0f101cf" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('7e49298c-a2c3-4c66-b83e-0c36c0f101cf',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_7e49298c-a2c3-4c66-b83e-0c36c0f101cf" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> EasyNetQ;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> MQ.Common
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MQHelper
    {
        </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
        <span style="color: #808080;">///</span><span style="color: #008000;"> 发送消息
        </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
        <span style="color: #808080;">///</span> <span style="color: #808080;">&lt;param name="msg"&gt;&lt;/param&gt;</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Publish(Message msg)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> 创建消息bus</span>
            IBus bus =<span style="color: #000000;"> BusBuilder.CreateMessageBus();
            </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
            {
                bus.Publish(msg, x </span>=&gt;<span style="color: #000000;"> x.WithTopic(msg.MessageRouter));
            }
            </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (EasyNetQException ex)
            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;">处理连接消息服务器异常</span>
<span style="color: #000000;">            }
            bus.Dispose();</span><span style="color: #008000;">//</span><span style="color: #008000;">与数据库connection类似，使用后记得销毁bus对象</span>
<span style="color: #000000;">        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Subscibe(Message msg, IProcessMessage ipro)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> 创建消息bus</span>
            IBus bus =<span style="color: #000000;"> BusBuilder.CreateMessageBus();
            </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
            {
                bus.Subscribe</span>&lt;Message&gt;(msg.MessageRouter, message =&gt;<span style="color: #000000;"> ipro.ProcessMsg(message),
                    x </span>=&gt;<span style="color: #000000;"> x.WithTopic(msg.MessageRouter));
            }
            </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (EasyNetQException ex)
            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;">处理连接消息服务器异常 </span>
<span style="color: #000000;">            }
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">MQHelper</span></div>
<p><strong>2，MQ.Consumer</strong></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('0c9b0dc6-3782-40ac-b176-66afe984b6dd')"><img id="code_img_closed_0c9b0dc6-3782-40ac-b176-66afe984b6dd" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_0c9b0dc6-3782-40ac-b176-66afe984b6dd" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('0c9b0dc6-3782-40ac-b176-66afe984b6dd',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_0c9b0dc6-3782-40ac-b176-66afe984b6dd" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> MQ.Common;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> MQ.Consumer
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> OrderProcessMessage : IProcessMessage
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> ProcessMsg(Message msg)
        {
            Console.WriteLine(msg.MessageBody);
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">OrderProcessMessage</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('5680cdfb-bdc7-40bc-8588-d8de1917579d')"><img id="code_img_closed_5680cdfb-bdc7-40bc-8588-d8de1917579d" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_5680cdfb-bdc7-40bc-8588-d8de1917579d" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('5680cdfb-bdc7-40bc-8588-d8de1917579d',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_5680cdfb-bdc7-40bc-8588-d8de1917579d" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> MQ.Common;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> MQ.Consumer
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            OrderProcessMessage order </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> OrderProcessMessage();
            Message msg </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> Message();
            msg.MessageID </span>= <span style="color: #800000;">"</span><span style="color: #800000;">1</span><span style="color: #800000;">"</span><span style="color: #000000;">;
            msg.MessageRouter </span>= <span style="color: #800000;">"</span><span style="color: #800000;">pcm.notice.zhangsan</span><span style="color: #800000;">"</span><span style="color: #000000;">;
            MQHelper.Subscibe(msg, order);

            Console.ReadLine();
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Program</span></div>
<p><strong>3，MQ.Producer</strong></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('d932ae94-7dfc-48e0-91d5-6960f2c6dcea')"><img id="code_img_closed_d932ae94-7dfc-48e0-91d5-6960f2c6dcea" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_d932ae94-7dfc-48e0-91d5-6960f2c6dcea" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('d932ae94-7dfc-48e0-91d5-6960f2c6dcea',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_d932ae94-7dfc-48e0-91d5-6960f2c6dcea" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> MQ.Common;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> MQ.Producer
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            Message msg </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> Message();
            msg.MessageID </span>= <span style="color: #800000;">"</span><span style="color: #800000;">1</span><span style="color: #800000;">"</span><span style="color: #000000;">;
            msg.MessageBody </span>=<span style="color: #000000;"> DateTime.Now.ToString();
            msg.MessageTitle </span>= <span style="color: #800000;">"</span><span style="color: #800000;">1</span><span style="color: #800000;">"</span><span style="color: #000000;">;
            msg.MessageRouter </span>= <span style="color: #800000;">"</span><span style="color: #800000;">pcm.notice.zhangsan</span><span style="color: #800000;">"</span><span style="color: #000000;">;
            MQHelper.Publish(msg);

            Console.ReadLine();
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Program</span></div>
<p>当启动Consumer（消费者）时，会自动在RabbitMQ服务器上创建相关的exchange和queue。<br /><span style="font-size: 12px; color: #ff0000;">注意：这个程序应该先启动Consumer（消费者）</span></p>
<p>案例下载：&nbsp;<a href="http://pan.baidu.com/s/1c1LY9gc" target="_blank">http://pan.baidu.com/s/1c1LY9gc</a></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>参考文档：</p>
<p><a href="http://blog.csdn.net/seven_coder/article/details/50946562" target="_blank">http://blog.csdn.net/seven_coder/article/details/50946562</a></p>
<p><a href="http://www.cnblogs.com/zhangweizhong/p/5687457.html" target="_blank">http://www.cnblogs.com/zhangweizhong/p/5687457.html</a></p>
<p>&nbsp;</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201707/741594-20170728135009571-369864018.png" alt="" /></p>