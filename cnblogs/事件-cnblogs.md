<p>一、设计要公开事件的类型<br />1，第一步：定义类型来容纳所有需要发送给事件通知接受者的附加信息</p>
<p>2，第二步：定义事件成员</p>
<p>3，第三步：定义负责引发事件的方法来通知事件的登记对象<br />4，第四部：定义方法将输入转化为期望事件</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('40b907c8-8b14-4e44-b5c1-0aa2c92da6f9')"><img id="code_img_closed_40b907c8-8b14-4e44-b5c1-0aa2c92da6f9" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_40b907c8-8b14-4e44-b5c1-0aa2c92da6f9" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('40b907c8-8b14-4e44-b5c1-0aa2c92da6f9',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_40b907c8-8b14-4e44-b5c1-0aa2c92da6f9" class="cnblogs_code_hide">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">第一步：定义类型来容纳所有需要发送给事件通知接受者的附加信息</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> NewMailEventArgs:EventArgs
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span> <span style="color: #0000ff;">string</span><span style="color: #000000;"> m_from,m_to, m_subject;

        </span><span style="color: #0000ff;">public</span> NewMailEventArgs(<span style="color: #0000ff;">string</span> <span style="color: #0000ff;">from</span>, <span style="color: #0000ff;">string</span> to, <span style="color: #0000ff;">string</span><span style="color: #000000;"> subject)
        {
            m_from </span>= <span style="color: #0000ff;">from</span><span style="color: #000000;">;
            m_to </span>=<span style="color: #000000;"> to;
            m_subject </span>=<span style="color: #000000;"> subject;
        }
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span><span style="color: #000000;"> From {
            </span><span style="color: #0000ff;">get</span> { <span style="color: #0000ff;">return</span><span style="color: #000000;"> m_from;}
        }
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span><span style="color: #000000;"> To
        {
            </span><span style="color: #0000ff;">get</span> { <span style="color: #0000ff;">return</span><span style="color: #000000;"> m_to; }
        }
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span><span style="color: #000000;"> Subject
        {
            </span><span style="color: #0000ff;">get</span> { <span style="color: #0000ff;">return</span><span style="color: #000000;"> m_subject; }
        }
    }</span></pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('9e751185-bb86-4a7f-afe1-73f6a5a3e503')"><img id="code_img_closed_9e751185-bb86-4a7f-afe1-73f6a5a3e503" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_9e751185-bb86-4a7f-afe1-73f6a5a3e503" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('9e751185-bb86-4a7f-afe1-73f6a5a3e503',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_9e751185-bb86-4a7f-afe1-73f6a5a3e503" class="cnblogs_code_hide">
<pre>    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MailManager
    {

        </span><span style="color: #008000;">//</span><span style="color: #008000;">第二步：定义事件成员</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">event</span> EventHandler&lt;NewMailEventArgs&gt;<span style="color: #000000;"> NewMail;

        </span><span style="color: #008000;">//</span><span style="color: #008000;">第三步：定义负责引发事件的方法来通知事件的登记对象</span>
        <span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">virtual</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> OnNewMail(NewMailEventArgs e)
        {
            e.Raise(</span><span style="color: #0000ff;">this</span>, <span style="color: #0000ff;">ref</span><span style="color: #000000;"> NewMail);
        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;">第四部：定义方法将输入转化为期望事件</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> SimulateNewMail(<span style="color: #0000ff;">string</span> <span style="color: #0000ff;">from</span>, <span style="color: #0000ff;">string</span> to, <span style="color: #0000ff;">string</span><span style="color: #000000;"> subject)
        {
            NewMailEventArgs e </span>= <span style="color: #0000ff;">new</span> NewMailEventArgs(<span style="color: #0000ff;">from</span><span style="color: #000000;">, to, subject);
            OnNewMail(e);
        }

    }</span></pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('19f2f230-fa1d-4555-834e-53274835f277')"><img id="code_img_closed_19f2f230-fa1d-4555-834e-53274835f277" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_19f2f230-fa1d-4555-834e-53274835f277" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('19f2f230-fa1d-4555-834e-53274835f277',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_19f2f230-fa1d-4555-834e-53274835f277" class="cnblogs_code_hide">
<pre>    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> EventArgExtensions
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Raise&lt;TEventArg&gt;(<span style="color: #0000ff;">this</span> TEventArg tEventArg, <span style="color: #0000ff;">object</span><span style="color: #000000;"> sender,
            </span><span style="color: #0000ff;">ref</span> EventHandler&lt;TEventArg&gt; eventArgs) <span style="color: #0000ff;">where</span><span style="color: #000000;"> TEventArg : EventArgs
        {

            </span><span style="color: #008000;">//</span><span style="color: #008000;">Volatile.Read ：防止编译器优化掉代码，把temp优化掉了</span>
            EventHandler&lt;TEventArg&gt; temp = Volatile.Read(<span style="color: #0000ff;">ref</span><span style="color: #000000;"> eventArgs);
            </span><span style="color: #0000ff;">if</span> (temp != <span style="color: #0000ff;">null</span><span style="color: #000000;">)
                temp(sender, tEventArg);
        }
    }</span></pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<p>&nbsp;</p>