<p>如果急着解决跨域问题则需要配置该配置到应用程序的Web.config文件中。如果想了解一下WebApi跨域问题则继续往下看</p>
<div class="cnblogs_code">
<pre>  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">system.webServer</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">httpProtocol</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">customHeaders</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">add </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="Access-Control-Allow-Origin"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">="*"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">add </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="Access-Control-Allow-Headers"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">="*"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">add </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="Access-Control-Allow-Methods"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">="GET, POST, PUT, DELETE"</span> <span style="color: #0000ff;">/&gt;</span>
      <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">customHeaders</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">httpProtocol</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">
  ...
  </span><span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">system.webServer</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">1，为什么会存在跨域问题？</span></strong></span></p>
<p>浏览器会对JavaScript的执行进行相应的限制，导致跨域问题</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">2，同源策略</span></strong></span></p>
<p>&ldquo;源&rdquo;是指站点或者域。必须要求相应的URI在如下三个方面均是相同的：</p>
<p>①主机名称（域/子域名或者IP地址）</p>
<p>②端口号</p>
<p>③网络协议(http或者https)</p>
<p>例如：https://192.168.1.1:8080（源）</p>
<p>在同源的情况下不会出现跨域问题</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">3，什么是CORS（跨域资源共享）规范？</span></strong></span></p>
<p>CORS是各个浏览器厂家共同遵守的标准</p>
<p><strong>①对消费者授权</strong></p>
<p>如果浏览器对CORS支持，由它发起的请求会携带一个&ldquo;Origin&rdquo;的报头表明请求页面所在的站点（例如：Origin:https://192.168.1.1:8080）</p>
<p><span style="color: #ff0000;">对消费者授权通过&ldquo;Access-Control-Allow-Origin&rdquo;响应报头来设置（设置&ldquo;*&rdquo;对所有消费者授权）</span></p>
<p><strong>②对响应报头的授权</strong></p>
<p>&nbsp;设置一组直接暴露给客户端JavaScript程序的响应报头，但是对简单响应报头设置是无效的</p>
<p>CORS简单响应报头包括：Cache-Control、Content-Language、Content-Type、Expries、Last-Modified、Pragma</p>
<p><span style="color: #ff0000;">"Access-Control-Expose-Headers"对响应报头的授权（设置&ldquo;*&rdquo;对所有响应报头授权）</span></p>
<p><strong>③预检请求</strong></p>
<p>所谓预检机制就是在浏览器发送真正的跨域资源请求前，先发送一个预检请求（可以使用&ldquo;Access-Control-Max-Age&rdquo;设置缓存时间）</p>
<p>CORS规范将跨域资源请求划分为两种类，即&ldquo;简单请求&rdquo;和&ldquo;非简单请求&rdquo;</p>
<p>1&gt;简单Http方法：GET、HEAD、POST</p>
<p>2&gt;简单请求报头：Accept、Accept-Language、Content-Language、Content-Type(application/x-www-form-urlencoded、multipart/form-data、text/plain)</p>
<p>3&gt;自定义请求报头：浏览器自动生成的报头、由JavaScript自行添加的报头</p>
<p>&ldquo;简单请求&rdquo;包括：①请求采用简单HTTP方法②请求不具有自定请求报头或者是简单请求报头</p>
<p><span style="color: #ff0000;">&ldquo;Access-Control-Allow-Methods&rdquo;：跨域资源请求允许采用的HTTP方法列表</span></p>
<p><span style="color: #ff0000;">&ldquo;Access-Control-Allow-Headers&rdquo;：跨域资源请求允许携带的自定义报头列表</span></p>
<p><span style="color: #ff0000;">&ldquo;Access-Control-Max-Age&rdquo;：将响应结果进行缓存（单位秒），这样可以让浏览器避免频繁的发送预检请求</span></p>
<p><strong>④是否支持用户凭证</strong></p>
<p>如果客户端JavaScript程序利用一个withCredentials属性为true的XMLHttpRequest发送了一个跨域请求，但是浏览器得到的响应中不具有一个值为&ldquo;ture&rdquo;的响应报头&ldquo;Access-Control-Allow-Credentials&rdquo;，它对获取资源的操作将会被浏览器拒绝</p>
<p>&nbsp;</p>