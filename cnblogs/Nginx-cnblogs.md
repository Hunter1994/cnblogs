<p style="font-size: 18pt; background-color: rgba(22, 159, 230, 1);"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">一、安装Nginx</span></strong></span></p>
<p><strong>1，安装nginx</strong></p>
<p>nginx官网地址：http://nginx.org/en/download.html</p>
<p>&nbsp;<span class="cnblogs_code">yum install pcre pcre-devel -y</span>&nbsp;安装依赖包</p>
<p>&nbsp;<span class="cnblogs_code">yum install -y openssl openssl-devel</span>&nbsp;安装依赖包</p>
<p>&nbsp;<span class="cnblogs_code">wget http:<span style="color: #008000;">//</span><span style="color: #008000;">nginx.org/download/nginx-1.18.0.tar.gz</span></span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">tar zxvf nginx-<span style="color: #800080;">1.18</span>.<span style="color: #800080;">0</span>.tar.gz</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">cd nginx-<span style="color: #800080;">1.18</span>.<span style="color: #800080;">0</span>/</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">./configure --prefix=/usr/local/nginx</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">make</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">make install</span>&nbsp;</p>
<p><strong>2，nginx语法支持</strong></p>
<p>&nbsp;<span class="cnblogs_code">mkdir ~/.vim</span>&nbsp;创建目录</p>
<p>&nbsp;<span class="cnblogs_code">cp -r contrib/vim<span style="color: #008000;">/*</span><span style="color: #008000;"> ~/.vim</span></span>&nbsp;</p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: rgba(22, 159, 230, 1);"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">二、安装OpenResty</span></strong></span></p>
<p><strong>1，安装</strong></p>
<p>&nbsp;<span class="cnblogs_code"><span style="color: #0000ff;">wget</span> https:<span style="color: #008000;">//</span><span style="color: #008000;">openresty.org/download/openresty-1.19.3.1.tar.gz</span></span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code"><span style="color: #0000ff;">tar</span> zxvf openresty-<span style="color: #800080;">1.19</span>.<span style="color: #800080;">3.1</span>.<span style="color: #0000ff;">tar</span>.gz</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">cd openresty-<span style="color: #800080;">1.19</span>.<span style="color: #800080;">3.1</span>/</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">./configure --prefix=/usr/local/openresty</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">gmake</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">gmake <span style="color: #0000ff;">install</span></span>&nbsp;</p>
<p><strong>2，启动</strong></p>
<p>&nbsp;<span class="cnblogs_code">./nginx -c /usr/local/openresty/nginx/conf/nginx.conf</span>&nbsp;启动失败查看下端口是否被占用</p>
<p><strong>3，配置上游服务</strong></p>
<p>&nbsp;<span class="cnblogs_code">vim /usr/local/openresty/nginx/conf/nginx.conf</span>&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">...
 upstream local{
        server </span><span style="color: #800080;">127.0</span>.<span style="color: #800080;">0.1</span>:<span style="color: #800080;">8080</span><span style="color: #000000;">;
    }
    server {
        listen       </span><span style="color: #800080;">80</span><span style="color: #000000;">;
        server_name  localhost;

        #charset koi8</span>-<span style="color: #000000;">r;

        #access_log  logs</span>/<span style="color: #000000;">host.access.log  main;

        location </span>/<span style="color: #000000;"> {
            #root   html;
            #index  index.html index.htm;
            proxy_pass http:</span><span style="color: #008000;">//</span><span style="color: #008000;">local;</span>
<span style="color: #000000;">        }

...</span></pre>
</div>
<p><strong>&nbsp;4，配置返回真实的访问ip</strong></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">...

        location </span>/<span style="color: #000000;"> {
            proxy_set_header Host $host;
            proxy_set_header X</span>-Real-<span style="color: #000000;">IP $remote_addr;
            proxy_set_header X</span>-Forwarded-<span style="color: #000000;">For $proxy_add_x_forwarded_for;

...</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: rgba(22, 159, 230, 1);"><strong><span style="font-size: 18pt; color: #ffffff;">三、基本命令</span></strong></p>
<p><strong>1，基础命令</strong></p>
<p>&nbsp;<span class="cnblogs_code">[root@localhost sbin]#./nginx -c /usr/local/nginx/conf/nginx.conf</span>&nbsp;　　启动nginx</p>
<p>&nbsp;<span class="cnblogs_code">[root@localhost sbin]# ./nginx -t</span>&nbsp;　　测试配置文件是否有语法错误</p>
<p>&nbsp;<span class="cnblogs_code">[root@localhost sbin]# ./nginx -s reload</span>&nbsp;　　重载配置文件</p>
<p>&nbsp;<span class="cnblogs_code">[root@localhost sbin]# ./nginx -s stop</span>&nbsp;　　立刻停止服务</p>
<p>&nbsp;<span class="cnblogs_code">[root@localhost sbin]# ./nginx -s quit</span>&nbsp;　　优雅的停止服务</p>
<p>&nbsp;<span class="cnblogs_code">[root@localhost sbin]# ./nginx -s reopen</span>&nbsp;　　重新开始记录日志</p>
<p>&nbsp;</p>
<p><strong>2， 热部署</strong></p>
<p>热更新nginx程序，一般只需要替换掉sbin/nginx二进制文件，不需要更换其他文件</p>
<p>&nbsp;<span class="cnblogs_code">cp nginx nginx.old</span>&nbsp;备份nginx二进制文件</p>
<p>&nbsp;<span class="cnblogs_code">ps -ef | grep nginx</span>&nbsp;查看nginx进程号</p>
<p>&nbsp;<span class="cnblogs_code">kill -USR2 <span style="color: #800080;">10105</span></span>&nbsp;向nginx的老的master进程发送USR2信号，会新启动nginx进程，现在新老nginx进程并存，老的进程不再监听端口</p>
<p>&nbsp;<span class="cnblogs_code">kill -WINCH <span style="color: #800080;">10105</span></span>&nbsp;向nginx的老的master进程发送WINCH信号，请优雅的关闭掉所有的worker进程</p>
<p>&nbsp;<span class="cnblogs_code">kill -QUIT <span style="color: #800080;">10105</span></span>&nbsp;优雅的关闭老的master进程</p>
<p>&nbsp;<span class="cnblogs_code">kill -HUP <span style="color: #800080;">10105</span></span>&nbsp;版本回退操作，重启老的nginx的worker进程</p>
<p>&nbsp;</p>
<p><strong>3，日志切割</strong></p>
<p>如果日志文件过大，可以把日志文件清空（先把日志文件备份）</p>
<p>&nbsp;<span class="cnblogs_code">nginx -s reopen</span>&nbsp;或者&nbsp;<span class="cnblogs_code">kill -USR1 <span style="color: #800080;">10105</span></span>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: rgba(22, 159, 230, 1);"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">四、配置</span></strong></span></p>
<p><strong>1，gzip压缩</strong></p>
<p>①配置&nbsp;<span class="cnblogs_code">vim /usr/local/nginx/conf/nginx.conf</span>&nbsp;</p>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">gzip</span><span style="color: #000000;">  on; #on开启gzip off关闭
    gzip_min_length </span><span style="color: #800080;">1</span><span style="color: #000000;">;#小于多少字节的文件不进行压缩，测试可以配置小点看效果
    gzip_comp_level </span><span style="color: #800080;">2</span><span style="color: #000000;">;#压缩级别
    gzip_types text</span>/plain application/x-javascript text/css application/xml text/javascript application/x-httpd-php image/jpeg image/gif image/<span style="color: #000000;">png;#针对某些类型进行gzip压缩

    server {
        listen       </span><span style="color: #800080;">80</span><span style="color: #000000;">;
        server_name  localhost;</span></pre>
</div>
<p>②重载配置</p>
<p>&nbsp;<span class="cnblogs_code">./nginx -s reload</span>&nbsp;</p>
<p>&nbsp;</p>
<p><strong>2，限制访问速度</strong></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">    server {
        listen       </span><span style="color: #800080;">80</span><span style="color: #000000;">;
        server_name  localhost;
        #charset koi8</span>-<span style="color: #000000;">r;

        #access_log  logs</span>/<span style="color: #000000;">host.access.log  main;

        location </span>/<span style="color: #000000;"> {
            alias  html</span>/gentelella-master/production/<span style="color: #000000;">;
            index  index.html index.htm;
            set $limit_rate 1k;#限制访问速度，每秒传输1k 字节
        }</span></pre>
</div>
<p>&nbsp;</p>
<p><strong>3，配置请求日志</strong></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">ttp {
    include       mime.types;
    default_type  application</span>/octet-<span style="color: #000000;">stream;

    log_format  main  </span><span style="color: #800000;">'</span><span style="color: #800000;">$remote_addr - $remote_user [$time_local] "$request" </span><span style="color: #800000;">'</span>
                      <span style="color: #800000;">'</span><span style="color: #800000;">$status $body_bytes_sent "$http_referer" </span><span style="color: #800000;">'</span>
                      <span style="color: #800000;">'</span><span style="color: #800000;">"$http_user_agent" "$http_x_forwarded_for"</span><span style="color: #800000;">'</span><span style="color: #000000;">;

    #access_log  logs</span>/<span style="color: #000000;">access.log  main;

    sendfile        on;
...
...
server {
        listen       </span><span style="color: #800080;">80</span><span style="color: #000000;">;
        server_name  localhost;
        #charset koi8</span>-<span style="color: #000000;">r;

        access_log  logs</span>/host.access.log  main;</pre>
</div>
<p>&nbsp;</p>
<p><strong>3，缓存</strong></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">...
proxy_cache_path </span>/tmp/nginxcache levels=<span style="color: #800080;">1</span>:<span style="color: #800080;">2</span> keys_zone=my_cache:10m max_size=10g inactive=60m use_temp_path=<span style="color: #000000;">off;
    upstream local{
        server </span><span style="color: #800080;">127.0</span>.<span style="color: #800080;">0.1</span>:<span style="color: #800080;">8080</span><span style="color: #000000;">;
    }
    server {
        listen       </span><span style="color: #800080;">80</span><span style="color: #000000;">;
        server_name  localhost;

        #charset koi8</span>-<span style="color: #000000;">r;

        #access_log  logs</span>/<span style="color: #000000;">host.access.log  main;

        location </span>/<span style="color: #000000;"> {
            #root   html;
            #index  index.html index.htm;
            proxy_pass http:</span><span style="color: #008000;">//</span><span style="color: #008000;">local;</span>
<span style="color: #000000;">            proxy_cache my_cache;
            proxy_cache_key $host$uri$is_args$args;
            proxy_cache_valid </span><span style="color: #800080;">200</span> <span style="color: #800080;">304</span> <span style="color: #800080;">302</span><span style="color: #000000;"> 1d;
        }
...</span></pre>
</div>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: rgba(22, 159, 230, 1);"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">五、GoAccess可视化监控access日志</span></strong></span></p>
<p><strong>1，安装使用goaccess</strong></p>
<p>①安装ncurses</p>
<p>&nbsp;<span class="cnblogs_code">yum install ncurses-devel</span>&nbsp;</p>
<p>②安装geoip</p>
<p>&nbsp;<span class="cnblogs_code">yum install geoip-devel</span>&nbsp;</p>
<p>③安装goaccess</p>
<div class="cnblogs_code">
<pre>$ wget http:<span style="color: #008000;">//</span><span style="color: #008000;">tar.goaccess.io/goaccess-1.2.tar.gz</span>
$ tar -xzvf goaccess-<span style="color: #800080;">1.2</span><span style="color: #000000;">.tar.gz
$ cd goaccess</span>-<span style="color: #800080;">1.2</span>/<span style="color: #000000;">
$ .</span>/configure --enable-utf8 --enable-geoip=legacy --prefix=/usr/local/<span style="color: #000000;">goaccess
$ make
# make install</span></pre>
</div>
<p>④启动goaccess</p>
<p>&nbsp;<span class="cnblogs_code">./goaccess /usr/local/nginx/logs/host.access.log -o /usr/local/nginx/html/monitoring/report.html --real-time-html --time-format=<span style="color: #800000;">'</span><span style="color: #800000;">%H:%M:%S</span><span style="color: #800000;">'</span> --date-format=<span style="color: #800000;">'</span><span style="color: #800000;">%d/%b/%y</span><span style="color: #800000;">'</span> --log-format=COMBINED</span>&nbsp;</p>
<ul>
<li><span style="font-size: 12px;">/usr/local/nginx/logs/host.access.log 日志位置</span></li>
<li><span style="font-size: 12px;">-o /usr/local/nginx/html/monitoring/report.html 输出到report.html文件</span></li>
<li><span style="font-size: 12px;">--real-time-html 实时更新页面</span></li>
<li><span style="font-size: 12px;">--time-format='%H:%M:%S'&nbsp; 时间格式</span></li>
<li><span style="font-size: 12px;">--date-format='%d/%b/%y'&nbsp; 日期格式</span></li>
<li><span style="font-size: 12px;">--log-format=COMBINED&nbsp; 日志格式</span></li>
</ul>
<p>⑤修改nginx配置</p>
<p>&nbsp;<span class="cnblogs_code">vim /usr/local/nginx/conf/nginx.conf</span>&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">...
        location </span>/<span style="color: #000000;">report.html{
           alias </span>/usr/local/nginx/html/monitoring/<span style="color: #000000;">report.html;
        }
...</span></pre>
</div>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: rgba(22, 159, 230, 1);"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">六、SSL证书</span></strong></span></p>
<p><strong>1，证书类型</strong></p>
<p>&nbsp;①域名验证(domain validated,DV)证书</p>
<p>只会认证域名的归属是否正确。只要是你的域名指向的是申请证书的那台服务器。很多都是免费的</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202012/741594-20201229222723005-13572256.png" alt="" width="320" height="48" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;②组织验证（organization validated,OV）证书</p>
<p>在申请证书的时候会去验证填写的机构、企业名称是否正确。一般OV证书申请需要几天时间，价格高于DV证书</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202012/741594-20201229223041982-684411077.png" alt="" width="267" height="48" loading="lazy" /></p>
<p>&nbsp;③扩展演示（extended validation,EV）证书</p>
<p>EV证书更严格的验证，所以大部分浏览器对EV证书的显示非常友好，会在地址栏中显示机构名称</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202012/741594-20201229223217497-356730061.png" alt="" width="441" height="42" loading="lazy" /></p>
<p><strong>2，TLS安全密码套件</strong></p>
<p>&nbsp;<img src="https://img2020.cnblogs.com/blog/741594/202012/741594-20201230213044087-720819583.png" alt="" loading="lazy" /></p>
<p>&nbsp;</p>
<ul>
<li><span style="font-size: 12px;">&nbsp;第一部分： 密钥交换。椭圆曲线加密算法的表达。密钥交换是为了解决浏览器与服务器怎样各自独立的生成密钥，而最后生成的密钥是相同的，接下来会用这个密钥去加密数据。</span></li>
<li><span style="font-size: 12px;">&nbsp;第二部分：身份验证。密钥交换需要验证身份</span></li>
<li><span style="font-size: 12px;">&nbsp;第三部分：数据加密解密通讯的时候需要用到对称加密算法。AES（表达是那种算法），128（AES中有三种加密强度，使用128位加密强度），GCM（新的分组模式，可以提高多核CPU情况下加密或解密的性能）</span></li>
<li><span style="font-size: 12px;">&nbsp;第四部分：SHA256是一个摘要算法，把不定长度的字符串，生成一个固定长度的更短的一个摘要</span></li>
</ul>
<p><strong>&nbsp;3，生成免费证书</strong></p>
<p>&nbsp;<span class="cnblogs_code">yum install python2-certbot-nginx</span>&nbsp;安装certbot。yum搜索不到，则需要更新yum源。参考：<a href="https://blog.csdn.net/coderyqwh/article/details/111410616">https://blog.csdn.net/coderyqwh/article/details/111410616</a></p>
<p>&nbsp;<span class="cnblogs_code">ln -s /usr/local/openresty/nginx/sbin/nginx /usr/local/sbin/nginx</span>&nbsp;创建软链接。sbin里面没有nginx执行certbot会失败</p>
<p>&nbsp;<span class="cnblogs_code">certbot --nginx --nginx-server-root=/usr/local/openresty/nginx/conf/ -d www.zhang.com</span>&nbsp;--nginx-server-root指定nginx配置目录</p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: rgba(22, 159, 230, 1);"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">七、使用信号管理Nginx的父子进程</span></strong></span></p>
<p><strong>&nbsp;1，Master进程</strong></p>
<p>&nbsp;<span class="cnblogs_code">kill -TERM <span style="color: #800080;">2938</span> 或者kill -INT <span style="color: #800080;">2938</span> </span>&nbsp;立刻停止nginx进程</p>
<p>&nbsp;<span class="cnblogs_code">kill -QUIT <span style="color: #800080;">2938</span></span>&nbsp;优化的停止nginx进程</p>
<p>&nbsp;<span class="cnblogs_code">kill -HUP <span style="color: #800080;">2938</span></span>&nbsp;重载配置文件</p>
<p>&nbsp;<span class="cnblogs_code">kill -USR1 <span style="color: #800080;">2938</span></span>&nbsp;重新打开日志文件，做日志文件切割</p>
<p>&nbsp;<span class="cnblogs_code">kill -USR2 <span style="color: #800080;">2938</span></span>&nbsp;向nginx的老的master进程发送USR2信号，会新启动nginx进程，现在新老nginx进程并存，老的进程不再监听端口</p>
<p>&nbsp;<span class="cnblogs_code">kill -WINCH <span style="color: #800080;">2938</span></span>&nbsp;向nginx的老的master进程发送WINCH信号，请优雅的关闭掉所有的worker进程</p>
<p><strong>2，Worker进程（一般不会直接对worker进程进行管理）</strong></p>
<p>&nbsp;<span class="cnblogs_code"> kill -TERM 3<span style="color: #800080;">937</span>&nbsp;或者kill -INT 3<span style="color: #800080;">937</span></span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">kill -QUIT <span style="color: #800080;">3937</span></span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">kill -USR1 <span style="color: #800080;">3937</span></span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">kill -WINCH <span style="color: #800080;">3937</span></span>&nbsp;</p>
<p><strong>&nbsp;3，nginx命令行</strong></p>
<p>reload： HUP</p>
<p>reopen：USR1</p>
<p>stop：TERM</p>
<p>quit：QUIT</p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: rgba(22, 159, 230, 1);"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">八、模块&nbsp;</span></strong></span></p>
<p>&nbsp;nginx官网文档:<a href="http://nginx.org/en/docs/">http://nginx.org/en/docs/</a></p>
<p><strong>&nbsp;1，查询编译进来的模块</strong></p>
<p>&nbsp;<span class="cnblogs_code">vim /usr/local/src/nginx-<span style="color: #800080;">1.18</span>.<span style="color: #800080;">0</span>/objs/ngx_modules.c</span>&nbsp;</p>
<p>*ngx_modules[]数组里面是编辑进nginx的模块</p>
<p>①查询模块源代码（例如ngx_http_gzip_filter_module）</p>
<p>&nbsp;<span class="cnblogs_code">vim /usr/local/src/nginx-<span style="color: #800080;">1.18</span>.<span style="color: #800080;">0</span>/src/http/modules/ngx_http_gzip_filter_module.c</span>&nbsp;</p>
<p>&nbsp;<img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210103103510078-1143951786.png" alt="" width="603" height="263" loading="lazy" /></p>
<p>&nbsp;</p>