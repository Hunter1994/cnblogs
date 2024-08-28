<p>一、下载并安装Erlang</p>
<p>下载地址：<a href="http://www.erlang.org/downloads" target="_blank">http://www.erlang.org/downloads</a></p>
<p><a href="https://pan.baidu.com/s/1w0uEQIFnm7AJ4EjeIxmRqw" target="_blank">otp_src_20.3.tar.gz</a></p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201803/741594-20180323140642320-2022706220.png" alt="" width="516" height="206" /></p>
<p>①解压otp_src_20.3.tar.gz</p>
<p>②安装各种驱动&nbsp;<span class="cnblogs_code">yum -y install make gcc gcc-c++ kernel-devel m4 ncurses-devel openssl-devel unixODBC-devel</span>&nbsp;</p>
<p>③进入解压目录执行命令&nbsp;&nbsp;<span class="cnblogs_code">./configure --prefix=/opt/erlang --without-javac</span>&nbsp;</p>
<p>④执行编译命令&nbsp;<span class="cnblogs_code">make</span>&nbsp;</p>
<p>⑤执行命令&nbsp;<span class="cnblogs_code">make install</span>&nbsp;</p>
<p>⑥添加环境变量（/etc/profile文件编辑）</p>
<div class="cnblogs_code">
<pre>#<span style="color: #0000ff;">set</span><span style="color: #000000;"> erlang environment
export PATH</span>=$PATH:/opt/erlang/bin</pre>
</div>
<p>&nbsp;<span class="cnblogs_code">source /etc/profile</span>&nbsp;使得文件生效</p>
<p>重启</p>
<p>&nbsp;</p>
<p>二、下载并安装RabbitMQ</p>
<p><a href="https://pan.baidu.com/s/139Wvjxced_qA6wr_rtMluA" target="_blank">rabbitmq-server-generic-unix-3.7.4.tar</a></p>
<p>下载地址：<a href="http://www.rabbitmq.com/install-generic-unix.html" target="_blank">http://www.rabbitmq.com/install-generic-unix.html</a></p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201803/741594-20180323164243077-1374687689.png" alt="" width="879" height="301" /></p>
<p>&nbsp;</p>
<p>&nbsp;①添加环境变量（/etc/profile文件编辑）</p>
<div class="cnblogs_code">
<pre>    #<span style="color: #0000ff;">set</span><span style="color: #000000;"> rabbitmq environment
    export PATH</span>=$PATH:/usr/local/rabbitmq/sbin</pre>
</div>
<p>&nbsp;<span class="cnblogs_code">source /etc/profile&nbsp;使得文件生效</span></p>
<p>重启</p>
<p>②启动服务&nbsp;<span class="cnblogs_code">rabbitmq-server -detached <span style="color: #008000;">//</span><span style="color: #008000;">启动rabbitmq，-detached代表后台守护进程方式启动。</span></span>&nbsp;</p>
<p>③查看状态&nbsp;<span class="cnblogs_code">rabbitmqctl status</span>&nbsp;</p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201803/741594-20180323164438901-940284239.png" alt="" width="504" height="166" /></p>
<p>④启用插件&nbsp;<span class="cnblogs_code">rabbitmq-plugins enable rabbitmq_management</span>&nbsp;</p>
<p>⑤安装完成进入http://localhost:15672，默认管理员和密码都是guest&nbsp;</p>
<p>&nbsp;</p>