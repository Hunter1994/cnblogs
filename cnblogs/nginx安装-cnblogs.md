<p style="font-size: 18pt; background-color: #169fe6;"><span style="color: #ffffff;"><strong>一、centos平台编译环境安装</strong></span></p>
<p>1，安装make：</p>
<div class="cnblogs_code">
<pre>yum -y install gcc automake autoconf libtool make</pre>
</div>
<p>2，安装g++：</p>
<div class="cnblogs_code">
<pre>yum install gcc gcc-c++</pre>
</div>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: #169fe6;"><strong><span style="color: #ffffff;">二、安装依赖库（cd /usr/local/src）</span></strong></p>
<p>1，安装PCRE库(ftp://ftp.csx.cam.ac.uk/pub/software/programming/pcre/)</p>
<div class="cnblogs_code">
<pre>cd /usr/local/<span style="color: #000000;">src
wget ftp:</span><span style="color: #008000;">//</span><span style="color: #008000;">ftp.csx.cam.ac.uk/pub/software/programming/pcre/pcre-8.39.tar.gz </span>
tar -zxvf pcre-<span style="color: #800080;">8.37</span><span style="color: #000000;">.tar.gz
cd pcre</span>-<span style="color: #800080;">8.34</span><span style="color: #000000;">
.</span>/<span style="color: #000000;">configure
make
make install</span></pre>
</div>
<p>&nbsp;</p>
<p>2，安装zlib库(http://zlib.net/)</p>
<div class="cnblogs_code">
<pre>cd /usr/local/<span style="color: #000000;">src
wget http:</span><span style="color: #008000;">//</span><span style="color: #008000;">zlib.net/zlib-1.2.11.tar.gz</span>
tar -zxvf zlib-<span style="color: #800080;">1.2</span>.<span style="color: #800080;">11</span><span style="color: #000000;">.tar.gz
cd zlib</span>-<span style="color: #800080;">1.2</span>.<span style="color: #800080;">11</span><span style="color: #000000;">
.</span>/<span style="color: #000000;">configure
make
make install</span></pre>
</div>
<p>&nbsp;</p>
<p>3，安装openssl（某些vps默认没装ssl)</p>
<div class="cnblogs_code">
<pre>cd /usr/local/<span style="color: #000000;">src
wget https:</span><span style="color: #008000;">//</span><span style="color: #008000;">www.openssl.org/source/openssl-1.0.1t.tar.gz</span>
tar -zxvf openssl-<span style="color: #800080;">1.0</span><span style="color: #000000;">.1t.tar.gz
cd openssl</span>-<span style="color: #800080;">1.0</span><span style="color: #000000;">.1t
.</span>/<span style="color: #000000;">Configure
make
make install</span></pre>
</div>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: #169fe6;"><strong><span style="color: #ffffff;">三、安装nginx</span></strong></p>
<div class="cnblogs_code">
<pre>cd /usr/local/<span style="color: #000000;">src
wget http:</span><span style="color: #008000;">//</span><span style="color: #008000;">nginx.org/download/nginx-1.1.10.tar.gz</span>
tar -zxvf nginx-<span style="color: #800080;">1.1</span>.<span style="color: #800080;">10</span><span style="color: #000000;">.tar.gz
cd nginx</span>-<span style="color: #800080;">1.1</span>.<span style="color: #800080;">10</span><span style="color: #000000;">
.</span>/<span style="color: #000000;">configure
make
make install</span></pre>
</div>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: #169fe6;"><strong><span style="color: #ffffff;">四、nginx重启、关闭、启动</span></strong></p>
<p>1，启动：</p>
<div class="cnblogs_code">
<pre>/usr/local/nginx/sbin/nginx -c /usr/local/nginx/conf/nginx.conf</pre>
</div>
<p>&nbsp;</p>
<p>2，停止（三种）<br />①快速停止：&nbsp;<span class="cnblogs_code">kill -INT <span style="color: #800080;">2132</span></span>&nbsp;<br />②从容停止：&nbsp;<span class="cnblogs_code">kill -QUIT <span style="color: #800080;">2072</span></span>&nbsp;<br />③强制停止：&nbsp;<span class="cnblogs_code">pkill -<span style="color: #800080;">9</span> nginx</span>&nbsp;</p>
<p>3，重启<br />①验证nginx配置文件是否正确：&nbsp;<span class="cnblogs_code">./nginx -t</span>&nbsp;<br />②重启：目录sbin下 &nbsp;<span class="cnblogs_code">./nginx -s reload </span>&nbsp;或者&nbsp;&nbsp;<span class="cnblogs_code">kill -HUP 进程号</span>&nbsp;</p>
<p>&nbsp;</p>