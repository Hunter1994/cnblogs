<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">一、AJAX</span></strong></p>
<p>1，ABP采用的方式</p>
<p>ASP.NET Boilerplate通过用abp.ajax函数包装AJAX调用来自动执行其中的一些步骤。 一个例子ajax调用：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> newPerson =<span style="color: #000000;"> {
    name: </span>'Dougles Adams'<span style="color: #000000;">,
    age: </span>42<span style="color: #000000;">
};

abp.ajax({
    url: </span>'/People/SavePerson'<span style="color: #000000;">,
    data: JSON.stringify(newPerson)
}).done(</span><span style="color: #0000ff;">function</span><span style="color: #000000;">(data) {
    abp.notify.success(</span>'created new person with id = ' +<span style="color: #000000;"> data.personId);
});</span></pre>
</div>
<p>abp.ajax以一个对象作为接收<strong>选项</strong>。你可以传递任何在jQuery的$.ajax方法中有效的任何参数。这里有一些&nbsp;<strong>默认</strong>的值：dataType是&lsquo;json&rsquo;，type是&lsquo;POST&rsquo;，contentType是&lsquo;application/json&rsquo;（因此，在发送到服务器之前，我们可以调用JSON.stringify将javascript对象转成JSON字符串）。你可以通过将选项传给abp.ajax重写默认值。</p>
<p>abp.ajax返回了<strong><a href="http://api.jquery.com/deferred.promise/">promise</a></strong>。因此，你可以写done,fail,then等处理函数。上面的例子中，我们向&nbsp;<strong>PeopleController的SavePerson</strong>的action发送了简单的Ajax请求。在&nbsp;<strong>done</strong>处理函数中，我们获得了新添加的person的数据库Id，而且展示了一个成功的通知。让我们看一下该Ajax请求的&nbsp;<strong>MVC控制器</strong></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">public class PeopleController : AbpController
{
    [HttpPost]
    public JsonResult SavePerson(SavePersonModel person)
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;">TODO:将新的person保存到数据库，并返回该person的Id</span>
        <span style="color: #0000ff;">return</span> Json(<span style="color: #0000ff;">new</span> {PersonId = 42<span style="color: #000000;">});
    }
}</span></pre>
</div>
<p><strong>SavePersonModel</strong>包含了Name和Age属性。SavePerson标记有&nbsp;<strong>HttpPost</strong>特性，因为abp.ajax默认的方法是POST。这里通过返回一个匿名的对象简化了方法的实现。</p>
<p>2，AJAX返回消息<br />即使我们直接返回PersonId = 2的对象，ASP.NET Boilerplate也由MvcAjaxResponse对象包装。 实际的AJAX响应是这样的：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">{
  </span>"success": <span style="color: #0000ff;">true</span><span style="color: #000000;">,
  </span>"result"<span style="color: #000000;">: {
    </span>"personId": 42<span style="color: #000000;">
  },
  </span>"error": <span style="color: #0000ff;">null</span><span style="color: #000000;">,
  </span>"targetUrl": <span style="color: #0000ff;">null</span><span style="color: #000000;">,
  </span>"unAuthorizedRequest": <span style="color: #0000ff;">false</span><span style="color: #000000;">
}</span></pre>
</div>
<p>这里，所有的属性都是camelCase的（因为在javascript中这是惯例），即使在服务端代码中是PascalCased的。下面解释一下所有的字段：</p>
<ul>
<li><strong>success</strong>:一个布尔值，表示操作的成功状态。如果是true，abp.ajax会解析该promise，并调用&nbsp;<strong>done</strong>处理函数。如果是false（如果在方法调用中发生了异常），它会调用&nbsp;<strong>fail</strong>处理函数并使用abp.message.error函数展示一个&nbsp;<strong>error</strong>消息。</li>
<li><strong>result</strong>：控制器的action返回的实际值。如果success是true，而且服务器发送了一个返回值，它才有效。</li>
<li><strong>error</strong>：如果success是false，那么该字段是一个包含了&nbsp;<strong>message</strong>和&nbsp;<strong>detail</strong>字段的对象。</li>
<li><strong>targetUrl</strong>:这为服务器提供了一种重定向客户端到其他Url的可能性。</li>
<li><strong>unAuthorizedRequest</strong>:这为服务器提供了通知客户端该操作没有授权或者用户没有认证的可能性。如果该值是true，那么abp.ajax会&nbsp;<strong>重新加载</strong>当前的页面。</li>
</ul>
<p>通过从<strong>AbpController</strong>类中派生就可以将返回值转换成一个封装的Ajax响应。&nbsp;<strong>abp.ajax</strong>会识别并计算该响应。因此，它们成对工作。如果没有发生错误的话，那么abp.ajax的done处理函数会获得控制器返回的实际值（一个具有personId属性的对象）。</p>
<p>当从<strong>AbpApiController</strong>类派生时，也会存在相同的机制。</p>
<p>3，处理错误</p>
<p>正如上面描述的，ABP会处理服务器中的所有异常，并返回一个具有错误信息的对象，如下所示：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">{
  </span>"targetUrl": <span style="color: #0000ff;">null</span><span style="color: #000000;">,
  </span>"result": <span style="color: #0000ff;">null</span><span style="color: #000000;">,
  </span>"success": <span style="color: #0000ff;">false</span><span style="color: #000000;">,
  </span>"error"<span style="color: #000000;">: {
    </span>"message": "An internal error occured during your request!"<span style="color: #000000;">,
    </span>"details": "..."<span style="color: #000000;">
  },
  </span>"unAuthorizedRequest": <span style="color: #0000ff;">false</span><span style="color: #000000;">
}</span></pre>
</div>
<p>可以看到，success是false，result是null。abp.ajax处理该对象，而且使用abp.message.error函数展示一个错误信息给用户。如果你的服务端代码抛出了一个<strong>UserFriendlyException</strong>类型的异常，它会直接给用户显示异常信息。否则，它会隐藏实际的错误（将错误写到日志中），并展示一个标准的&ldquo;服务器内部错误...&rdquo;信息给用户。所有的这些都是ABP自动处理的。</p>
<p>4，动态Web API层</p>
<p>虽然ABP提供了一种使得调用Ajax很简单的机制，但是在真实世界的应用中，为每个Ajax调用编写javascript函数是很经典的，比如：</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">创建一个抽象了Ajax调用的function</span>
<span style="color: #0000ff;">var</span> savePerson = <span style="color: #0000ff;">function</span><span style="color: #000000;">(person) {
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> abp.ajax({
        url: </span>'/People/SavePerson'<span style="color: #000000;">,
        data: JSON.stringify(person)
    });
};

</span><span style="color: #008000;">//</span><span style="color: #008000;">创建一个新的 person</span>
<span style="color: #0000ff;">var</span> newPerson =<span style="color: #000000;"> {
    name: </span>'Dougles Adams'<span style="color: #000000;">,
    age: </span>42<span style="color: #000000;">
};

</span><span style="color: #008000;">//</span><span style="color: #008000;">保存该person</span>
savePerson(newPerson).done(<span style="color: #0000ff;">function</span><span style="color: #000000;">(data) {
    abp.notify.success(</span>'created new person with id = ' +<span style="color: #000000;"> data.personId);
});</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">二、Notification</span></strong></span></p>
<p>展示自动关闭的通知。</p>
<p>我们喜欢一些事情发生时展示一些精致的自动消失的通知，比如当保存一条记录或者问题发生时。ABP为这个定义了标准的APIs。</p>
<div class="cnblogs_code">
<pre>abp.notify.success('a message text', 'optional title'<span style="color: #000000;">);
abp.notify.info(</span>'a message text', 'optional title'<span style="color: #000000;">);
abp.notify.warn(</span>'a message text', 'optional title'<span style="color: #000000;">);
abp.notify.error(</span>'a message text', 'optional title');</pre>
</div>
<p>通知API默认是使用<strong><a href="http://codeseven.github.io/toastr/demo.html">toastr</a></strong>库实现的。要使toastr生效，你应该引用toastr的css和javascript文件，然后再在页面中包含abp.toastr.js作为适配器。一个toastr成功通知如下所示：</p>
<p>&nbsp;<img src="http://images2017.cnblogs.com/blog/741594/201710/741594-20171018212313302-1192870405.png" alt="" /></p>
<p>你也可以用你最喜欢的通知库中实现通知。只需要在自定义javascript文件中重写所有的函数，然后把它添加到页面中而不是abp.toastr.js（你可以检查该文件看它是否实现，这个相当简单）中。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">三、Message</span></strong></span></p>
<p>给用户展示消息对话框。</p>
<p>消息API用于给用户展示消息或者获得用户的确认。</p>
<p>消息API默认是使用<strong><a href="http://tristanedwards.me/sweetalert">sweetalert</a></strong>实现的。要让sweetalert生效，你应该包含它的css和javascript文件，然后再页面中添加&nbsp;<strong>abp.sweet-alert.js</strong>的引用作为适配器。</p>
<div class="cnblogs_code">
<pre>abp.message.info('some info message', 'some optional title'<span style="color: #000000;">);
abp.message.success(</span>'some success message', 'some optional title'<span style="color: #000000;">);
abp.message.warn(</span>'some warning message', 'some optional title'<span style="color: #000000;">);
abp.message.error(</span>'some error message', 'some optional title');</pre>
</div>
<p>一个成功的消息如下所示：</p>
<p>&nbsp;<img src="http://images2017.cnblogs.com/blog/741594/201710/741594-20171018212450771-1867598287.png" alt="" /></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">abp.message.confirm(
    </span>'User admin will be deleted.'<span style="color: #000000;">,
    </span>'Are you sure?'<span style="color: #000000;">,
    </span><span style="color: #0000ff;">function</span><span style="color: #000000;"> (isConfirmed) {
        </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (isConfirmed) {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">...删除用户</span>
<span style="color: #000000;">        }
    }
);</span></pre>
</div>
<p>这里的第二个参数（title）是可选的，因此，回调函数也可以是第二个参数。</p>
<p>一个确认消息的例子如下所示：</p>
<p>&nbsp;<img src="http://images2017.cnblogs.com/blog/741594/201710/741594-20171018212510584-891983574.png" alt="" /></p>
<p>ABP内部使用了Message API。比如，如果Ajax调用失败了，那么它会调用abp.message.error。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">四、UI block和Busy API</span></strong></p>
<p>使用一个区域（一个div，form，整个页面等）阻塞用户的输入。此外，还使得一个区域处于繁忙状态（具有一个繁忙的指示器，如&lsquo;loading...&rsquo;）。</p>
<p>1，UI Block API</p>
<p>该API使用一个透明的涂层（transparent overlay）来阻塞整个页面或者该页面上的一个元素。这样，用户的点击就无效了。当保存一个表单或者加载一个区域（一个div或者整个页面）时这是很有用的，比如：</p>
<div class="cnblogs_code">
<pre>abp.ui.block(); <span style="color: #008000;">//</span><span style="color: #008000;">阻塞整个页面</span>
abp.ui.block($('#MyDivElement')); <span style="color: #008000;">//</span><span style="color: #008000;">可以使用jQuery 选择器..</span>
abp.ui.block('#MyDivElement'); <span style="color: #008000;">//</span><span style="color: #008000;">..或者直接使用选择器</span>
abp.ui.unblock(); <span style="color: #008000;">//</span><span style="color: #008000;">解除阻塞整个页面</span>
abp.ui.unblock('#MyDivElement'); <span style="color: #008000;">//</span><span style="color: #008000;">解除阻塞特定的元素</span></pre>
</div>
<p>UI Block API默认使用jQuery的blockUI插件实现的。要是它生效，你应该包含它的javascript文件，然后在页面中包含<strong>abp.blockUI.js</strong>作为适配器。</p>
<p>2，UI Busy API</p>
<p>该API用于使得某些页面或者元素处于繁忙状态。比如，你可能想阻塞一个表单，然后当提交表单至服务器时展示一个繁忙的指示器。例子：</p>
<div class="cnblogs_code">
<pre>abp.ui.setBusy('#MyLoginForm'<span style="color: #000000;">);
abp.ui.clearBusy(</span>'#MyLoginForm');</pre>
</div>
<p><img src="http://images2017.cnblogs.com/blog/741594/201710/741594-20171018212731490-1192721279.png" alt="" /></p>
<p>该参数应该是一个选择器（如&lsquo;#MyLoginForm&rsquo;）或者jQuery选择器（如$('#MyLoginForm')）。要使得整个页面处于繁忙状态，你可以传入null（或者'body'）作为选择器。</p>
<p>setBusy函数第二个参数接收一个promise（约定），当该约定完成时会自动清除繁忙的状态。例子：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">abp.ui.setBusy(
    $(</span>'#MyLoginForm'<span style="color: #000000;">), 
    abp.ajax({ ... })   
);</span></pre>
</div>
<p>因为abp.ajax返回promise，我们可以直接将它作为promise传入。要学习惯于promise更多的东西，查看jQuery的<strong><a href="http://api.jquery.com/category/deferred-object/">Deferred</a></strong>。</p>
<p>UI Busy API是使用<strong><a href="http://fgnass.github.io/spin.js/">spin.js</a></strong>实现的。要让它生效，应该包含它的javascript文件，然后在页面中包含<strong>abp.spin.js</strong>作为适配器。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">五、事件总线</span></strong></span></p>
<p>用于注册和触发客户端的全局事件。</p>
<p><strong>Pub/sub</strong>事件模型广泛用于客户端，ABP包含了一个简单的<strong>全局事件总线</strong>来&nbsp;<strong>注册</strong>并&nbsp;<strong>触发事件</strong>。</p>
<p>1，注册事件</p>
<p>可以使用<strong>abp.event.on</strong>来注册一个全局事件。一个注册的例子：</p>
<div class="cnblogs_code">
<pre>abp.event.on('itemAddedToBasket', <span style="color: #0000ff;">function</span><span style="color: #000000;"> (item) {
    console.log(item.name </span>+ ' is added to basket!'<span style="color: #000000;">);
});</span></pre>
</div>
<p>第一个参数是<strong>事件的唯一名称</strong>。第二个是回调函数，当特定事件被触发时，会被调用。</p>
<p>可以使用<strong>abp.event.off</strong>方法来从一个事件中取消注册。注意：要取消注册，要提供相同的函数。因此，对于上面的例子，你应该将回调函数设置为一个变量，然后在<strong>on和off</strong>方法中使用它。</p>
<p>2，触发事件</p>
<p><strong>abp.event.trigger</strong>用于触发一个全局事件。触发一个已经注册的事件的代码如下：</p>
<div class="cnblogs_code">
<pre>abp.event.trigger('itemAddedToBasket'<span style="color: #000000;">, {
    id: </span>42<span style="color: #000000;">,
    name: </span>'Acme Light MousePad'<span style="color: #000000;">
});</span></pre>
</div>
<p>第一个参数是<strong>该事件的唯一名称</strong>。第二个是（可选的）<strong>事件参数</strong>。你可以添加任何数量的参数，并且在回调方法中获得它们</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">六、日志</span></p>
<p>在客户端记录日志。</p>
<p>1，Javascript Logging API</p>
<p>当你想要在客户端记录一些简单的日志时，你可以使用console.log('...')API，这你已经知道了。但是这种写法不是所有的浏览器都支持的，而且可能会破坏你的脚本。因此，你应该首先检查console是否可用，此外，你可能想在别的地方记录日志，甚至你想以某种级别记录日志。ABP定义了安全的日志函数：</p>
<div class="cnblogs_code">
<pre>abp.log.debug('...'<span style="color: #000000;">);
abp.log.info(</span>'...'<span style="color: #000000;">);
abp.log.warn(</span>'...'<span style="color: #000000;">);
abp.log.error(</span>'...'<span style="color: #000000;">);
abp.log.fatal(</span>'...');</pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">七、其他工具技能</span></p>
<p>ABP提供了一些通用的工具功能。</p>
<p>1，abp.utils.createNamespace</p>
<p>用于立即创建更深的命名空间。假设我们有一个基命名空间&lsquo;abp&rsquo;，然后想要创建或者获得&lsquo;abp.utils.strings.formatting&rsquo;命名空间</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> formatting = abp.utils.createNamespace(abp, 'utils.strings.formatting'<span style="color: #000000;">;

</span><span style="color: #008000;">//</span><span style="color: #008000;">给该namespace添加一个function</span>
formatting.format = <span style="color: #0000ff;">function</span>() { ... };</pre>
</div>
<p>这样就简化了安全地创建深入的命名空间了。注意，第一个参数是必须存在的根命名空间。</p>
<p>2，abp.utils.formatString</p>
<p>这个和C#中的string.Format()很相似。用法示例：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> str = abp.utils.formatString('Hello {0}!', 'World'); <span style="color: #008000;">//</span><span style="color: #008000;">str = 'Hello World!'</span>
<span style="color: #0000ff;">var</span> str = abp.utils.formatString('{0} number is {1}.', 'Secret', 42); <span style="color: #008000;">//</span><span style="color: #008000;">str = 'Secret number is 42'</span></pre>
</div>
<p>&nbsp;</p>