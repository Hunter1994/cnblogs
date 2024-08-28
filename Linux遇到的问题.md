<h2 style="background-color: #169fe6;"><span style="color: #ffffff;">一、基本命令</span></h2>
<p>&nbsp;<span class="cnblogs_code">yum list installed | grep docker&nbsp;</span>&nbsp;查看yum安装了哪些软件</p>
<p>&nbsp;<span class="cnblogs_code">netstat -lnp|grep 8000</span>&nbsp;查看端口</p>
<p>&nbsp;<span class="cnblogs_code">netstat -plutn | grep :<span style="color: #800080;">6069</span></span>&nbsp;查看端口</p>
<p>&nbsp;<span class="cnblogs_code">lsb_release -a</span>&nbsp;查看安装是哪个liunx系统</p>
<p>&nbsp;<span class="cnblogs_code">arch</span>&nbsp;查看系统是32位还是64位</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>//安装包<br />rpm -ivh rabbitmq-server-3.7.7-1.el7.noarch.rpm  <br />-i ：安装的意思<br />-v ：可视化<br />-h ：显示安装进度</p>
<p>//安装构建依赖<br />$ sudo yum install -y which wget perl openssl-devel make automake autoconf ncurses-devel gcc</p>
<p><br />//官网下载源码<br />$ curl -O http://erlang.org/download/otp_src_20.2.tar.gz</p>
<p>//解压包<br />$ tar zxvf otp_src_20.2.tar.gz</p>
<p>//批量卸载<br />yum remove erlang-*</p>
<p>//更新yum源<br />sudo yum clean all  <br />sudo yum makecache </p>
<p>//yum本地安装<br />yum localinstall rabbitmq-server-3.6.12-1.el6.noarch.rpm</p>
<p>&nbsp;</p>
<p>---------------------防火墙管理<br />//开启一个端口<br />firewall-cmd --zone=public --add-port=80/tcp --permanent    （--permanent永久生效，没有此参数重启后失效）<br />//重新载入<br />firewall-cmd --reload<br />//查看<br />firewall-cmd --zone= public --query-port=80/tcp<br />//删除<br />firewall-cmd --zone= public --remove-port=80/tcp --permanent</p>
<p><br />---------------------grep<br />cat /home/wwwroot/dutyliunx/App_Data/Logs/2018-09-05.log |grep -A 1 'fdata'<br />grep -C 5 foo file 显示file文件里匹配foo字串那行以及上下5行<br />grep -B 5 foo file 显示foo及前5行<br />grep -A 5 foo file 显示foo及后5行</p>
<p>&nbsp;</p>
<h2 style="background-color: #169fe6;"><span style="color: #ffffff;">二、网卡</span></h2>
<h2>1，虚拟机centos没有有线选项，而且不能上网，而且没有eth0网卡</h2>
<p>错误信息：<span style="color: #ff0000;">Job for network.service failed because the control process exited with error code. See "systemctl status network.service" and "journalctl -xe" for details</span></p>
<p>解决办法：</p>
<p>①新建eth0</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('1854de99-d195-4640-b0b8-f78a850e4615')"><img id="code_img_closed_1854de99-d195-4640-b0b8-f78a850e4615" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_1854de99-d195-4640-b0b8-f78a850e4615" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('1854de99-d195-4640-b0b8-f78a850e4615',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_1854de99-d195-4640-b0b8-f78a850e4615" class="cnblogs_code_hide">
<pre>TYPE=<span style="color: #000000;">Ethernet
PROXY_METHOD</span>=<span style="color: #000000;">none
BROWSER_ONLY</span>=<span style="color: #000000;">no
BOOTPROTO</span>=<span style="color: #000000;">dhcp
DEFROUTE</span>=<span style="color: #000000;">yes
PEERDNS</span>=<span style="color: #000000;">yes  
PEERROUTES</span>=<span style="color: #000000;">yes  
IPV4_FAILURE_FATAL</span>=<span style="color: #000000;">no
IPV6INIT</span>=<span style="color: #000000;">yes
IPV6_AUTOCONF</span>=<span style="color: #000000;">yes
IPV6_DEFROUTE</span>=<span style="color: #000000;">yes
IPV6_FAILURE_FATAL</span>=<span style="color: #000000;">no
IPV6_ADDR_GEN_MODE</span>=stable-<span style="color: #000000;">privacy
NAME</span>=<span style="color: #000000;">eth0
UUID</span>=fbb7785f-d35e-49ae-<span style="color: #800080;">9974</span>-<span style="color: #000000;">429ab14756f2
DEVICE</span>=<span style="color: #000000;">eth0
ONBOOT</span>=<span style="color: #000000;">yes
#GATEWAY</span>=<span style="color: #800080;">192.168</span>.<span style="color: #800080;">1.1</span><span style="color: #000000;">
#IPADDR</span>=<span style="color: #800080;">192.168</span>.<span style="color: #800080;">1.150</span><span style="color: #000000;">
#NETMASK</span>=<span style="color: #800080;">255.255</span>.<span style="color: #800080;">255.0</span><span style="color: #000000;">
#DNS1</span>=<span style="color: #800080;">218.30</span>.<span style="color: #800080;">118.6</span><span style="color: #000000;">
#DNS2</span>=<span style="color: #800080;">10.64</span>.<span style="color: #800080;">0.100</span></pre>
</div>
<span class="cnblogs_code_collapse">ifcfg-eth0</span></div>
<p>②和 NetworkManager 服务有冲突，这个好解决，直接关闭 NetworkManger 服务就好了， service NetworkManager stop，并且禁止开机启动 chkconfig NetworkManager off 。之后重启就好了</p>
<p>③设置虚拟机为桥接模式</p>
<p>参考文档：<a href="http://blog.csdn.net/weiyongle1996/article/details/75128239" target="_blank">http://blog.csdn.net/weiyongle1996/article/details/75128239</a></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('97a25bdf-bf92-4d76-ba74-55f58779c29b')"><img id="code_img_closed_97a25bdf-bf92-4d76-ba74-55f58779c29b" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_97a25bdf-bf92-4d76-ba74-55f58779c29b" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('97a25bdf-bf92-4d76-ba74-55f58779c29b',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_97a25bdf-bf92-4d76-ba74-55f58779c29b" class="cnblogs_code_hide">
<pre>DEVICE=<span style="color: #800000;">"</span><span style="color: #800000;">eth1</span><span style="color: #800000;">"</span><span style="color: #000000;">                             
    网卡名称
NM_CONTROLLED</span>=<span style="color: #800000;">"</span><span style="color: #800000;">yes</span><span style="color: #800000;">"</span><span style="color: #000000;">           
    network mamager的参数 ,是否可以由NNetwork Manager托管，建议设置成no
HWADDR</span>=<span style="color: #000000;">                                     
    MAC地址
TYPE</span>=<span style="color: #000000;">Ethernet                             
    类型
PREFIX</span>=<span style="color: #800080;">24</span><span style="color: #000000;">                                    
    子网掩码24位
DEFROUTE</span>=<span style="color: #000000;">yes                          
    就是default route，是否把这个eth设置为默认路由
ONBOOT</span>=<span style="color: #000000;">yes                               
    设置为yes，开机自动启用网络连接
IPADDR</span>=<span style="color: #000000;">                                        
    IP地址
BOOTPROTO</span>=<span style="color: #000000;">none                     
    设置为none禁止DHCP，设置为static启用静态IP地址，设置为dhcp开启DHCP服务
NETMASK</span>=<span style="color: #800080;">255.255</span>.<span style="color: #800080;">255.0</span><span style="color: #000000;">          
    子网掩码
DNS1</span>=<span style="color: #800080;">8.8</span>.<span style="color: #800080;">8.8</span><span style="color: #000000;">                                
    第一个dns服务器
BROADCAST                                 
    广播
UUID
    唯一标识
TYPE</span>=<span style="color: #000000;">Ethernet                              
    网络类型为：Ethernet
BRIDGE</span>=<span style="color: #000000;">                                   
    设置桥接网卡
GATEWAY</span>=<span style="color: #000000;">                                   
    设置网关
DNS2</span>=<span style="color: #800080;">8.8</span>.<span style="color: #800080;">4.4</span><span style="color: #000000;"> #                             
    第二个dns服务器
IPV6INIT</span>=<span style="color: #000000;">no                                    
    禁止IPV6
USERCTL</span>=<span style="color: #000000;">no                                
    是否允许非root用户控制该设备，设置为no，只能用root用户更改
NAME</span>=<span style="color: #800000;">"</span><span style="color: #800000;">System eth1</span><span style="color: #800000;">"</span><span style="color: #000000;">                   
    这个就是个网络连接的名字
MASTER</span>=<span style="color: #000000;">bond1                         
    指定主的名称 
SLAVE                                        
    指定了该接口是一个接合界面的组件。
NETWORK                                   
    网络地址
ARPCHECK</span>=<span style="color: #000000;">yes
    检测
PEERDNS                                  
    是否允许DHCP获得的DNS覆盖本地的DNS
PEERROUTES                           
    是否从DHCP服务器获取用于定义接口的默认网关的信息的路由表条目
IPV6INIT
    是否启用IPv6的接口。
IPV4_FAILURE_FATAL</span>=<span style="color: #000000;">yes       
    如果ipv4配置失败禁用设备
IPV6_FAILURE_FATAL</span>=<span style="color: #000000;">yes         
    如果ipv6配置失败禁用设备</span></pre>
</div>
<span class="cnblogs_code_collapse">网卡配置详情</span></div>
<p>&nbsp;</p>
<h2>2，centos7没有eth网卡解决办法</h2>
<p>&nbsp;参考：<a href="https://blog.csdn.net/u013252047/article/details/77947594" target="_blank">https://blog.csdn.net/u013252047/article/details/77947594</a></p>
<p>虚拟机设置：<img src="https://images2018.cnblogs.com/blog/741594/201807/741594-20180713120947767-838311275.png" alt="" /></p>
<p>&nbsp;</p>
<h2>3，centos7将ifcfg-ens33改为eth0</h2>
<p>①vi /etc/sysconfig/network-scripts/ifcfg-ens33</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('273f3375-529c-4352-9356-5d120a0a5d9c')"><img id="code_img_closed_273f3375-529c-4352-9356-5d120a0a5d9c" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_273f3375-529c-4352-9356-5d120a0a5d9c" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('273f3375-529c-4352-9356-5d120a0a5d9c',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_273f3375-529c-4352-9356-5d120a0a5d9c" class="cnblogs_code_hide">
<pre>TYPE=<span style="color: #000000;">Ethernet
PROXY_METHOD</span>=<span style="color: #000000;">none
BROWSER_ONLY</span>=<span style="color: #000000;">no
BOOTPROTO</span>=<span style="color: #0000ff;">static</span><span style="color: #000000;">
DEFROUTE</span>=<span style="color: #000000;">yes
GATEWAY</span>=<span style="color: #800080;">192.168</span>.<span style="color: #800080;">1.1</span><span style="color: #000000;">
IPADDR</span>=<span style="color: #800080;">192.168</span>.<span style="color: #800080;">1.150</span><span style="color: #000000;">
NETMASK</span>=<span style="color: #800080;">255.255</span>.<span style="color: #800080;">255.0</span><span style="color: #000000;">
IPV4_FAILURE_FATAL</span>=<span style="color: #000000;">yes
IPV6INIT</span>=<span style="color: #000000;">yes
IPV6_AUTOCONF</span>=<span style="color: #000000;">yes
IPV6_DEFROUTE</span>=<span style="color: #000000;">yes
IPV6_FAILURE_FATAL</span>=<span style="color: #000000;">no
IPV6_ADDR_GEN_MODE</span>=stable-<span style="color: #000000;">privacy
NAME</span>=<span style="color: #000000;">eth0
UUID</span>=1d2672e7-ef33-438c-bd64-<span style="color: #000000;">1fc8662bffc6
DEVICE</span>=<span style="color: #000000;">eth0
ONBOOT</span>=<span style="color: #000000;">yes
NM_CONTROLLED</span>=<span style="color: #000000;">no
HWADDR</span>=<span style="color: #800080;">00</span>:0c:<span style="color: #800080;">29</span>:<span style="color: #800080;">99</span>:0c:4c</pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<p>②ifcfg-ens33为ifcfg-eth0</p>
<p>mv ifcfg-ens33 ifcfg-eth0</p>
<p>③编辑/etc/default/grub并加入&ldquo;net.ifnames=0 biosdevname=0 &rdquo;到GRUB_CMDLINE_LINUX变量</p>
<p><img src="https://img2018.cnblogs.com/blog/741594/201903/741594-20190308153740619-1865011924.png" alt="" width="471" height="110" /></p>
<p>④运行命令&nbsp;<span class="cnblogs_code">grub2-mkconfig -o /boot/grub2/grub.cfg</span>&nbsp;来重新生成GRUB配置并更新内核参数</p>
<p>&nbsp;<img src="https://img2018.cnblogs.com/blog/741594/201903/741594-20190308153816543-133498640.png" alt="" width="453" height="83" /></p>
<p>⑤reboot</p>
<p><span style="color: #ff0000;">&nbsp;ps:检查其他ifcfg-*的ONBOOT配置，将其设为no。貌似只能存在一个ONBOOT=yes</span></p>
<p><span style="color: #ff0000;">注意配置DNS，不然域名解析不了</span></p>
<p>&nbsp;</p>
<p><span style="font-size: 18pt;"><strong>&nbsp;3，虚拟机始终连接不上，ping不通</strong></span></p>
<p><a href="https://www.cnblogs.com/zyp928/p/10729685.html">https://www.cnblogs.com/zyp928/p/10729685.html</a></p>
<p>&nbsp;<img src="https://img2020.cnblogs.com/blog/741594/202005/741594-20200510125542275-1157436636.png" alt="" /></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2 style="background-color: #169fe6;"><span style="color: #ffffff;">三、关闭防火墙</span></h2>
<p>systemctl stop firewalld.service #停止firewall<br />systemctl disable firewalld.service #禁止firewall开机启动</p>
<p>&nbsp;</p>
<h2 style="background-color: #169fe6;"><span style="color: #ffffff;">四、vim</span></h2>
<p>dd:删除游标所在的一整行(常用)<br />d+左方向键：删除光标左边的字符<br />i:开始编辑文本<br />esc:退出编辑文本模式<br />::进入命令模式<br />?字符：查找字符<br />u:撤销上一步的操作</p>
<p>:wq保存并退出</p>
<p>:q!退出不保存</p>
<p>&nbsp;</p>
<h2 style="background-color: #169fe6;"><span style="color: #ffffff;">五、安装/卸载ftp</span></h2>
<p>用户名<code>ftpuser；密码123456</code></p>
<h3>安装</h3>
<p>安装教程：</p>
<p><a href="https://www.cnblogs.com/zhi-leaf/p/5983550.html" target="_blank">https://www.cnblogs.com/zhi-leaf/p/5983550.html&nbsp;</a></p>
<p><a href="https://segmentfault.com/a/1190000008161400" target="_blank">https://segmentfault.com/a/1190000008161400</a></p>
<p><a href="https://www.jianshu.com/p/9abad055fff6" target="_blank">https://www.jianshu.com/p/9abad055fff6(亲测可以)</a></p>
<h3>配置ftp路径&nbsp;</h3>
<div class="cnblogs_code">
<pre>local_root=/<span style="color: #0000ff;">var</span>/www/<span style="color: #000000;">html
chroot_local_user</span>=<span style="color: #000000;">YES
anon_root</span>=/<span style="color: #0000ff;">var</span>/www/<span style="color: #000000;">html<br /></span></pre>
</div>
<p>注：local_root 针对系统用户；&nbsp;anon_root 针对匿名用户。</p>
<p>重新启动服务：service vsftpd restart</p>
<p>删除用户：userdel ftpuser</p>
<h3>卸载</h3>
<div class="cnblogs_code">
<pre>rpm -qa | grep vsftpd <span style="color: #008000;">//</span><span style="color: #008000;">查看ftp是否安装<br /></span></pre>
<pre class="hljs autoit"><code class="shell"><span class="hljs-meta">rpm -q vsftpd  //</span></code>查看ftp是否安装</pre>
</div>
<div class="cnblogs_code">
<pre>systemctl stop vsftpd <span style="color: #008000;">//</span><span style="color: #008000;">停止ftp服务 </span>
yum -y remove vsftpd.x86_64 <span style="color: #008000;">//</span><span style="color: #008000;">卸载ftp服务</span></pre>
</div>
<p>解决：ftp 上传 550 failed to change directory</p>
<p><a href="https://blog.csdn.net/coreyC/article/details/80866533" target="_blank">https://blog.csdn.net/coreyC/article/details/80866533</a></p>
<p>&nbsp;</p>
<h1 style="background-color: #169fe6;"><span style="font-size: 14pt; color: #ffffff;"><strong>六、Error: Cannot retrieve repository metadata (repomd.xml) for repository: base. Please verify its path and try again</strong></span></h1>
<p>解决方法：<a href="https://blog.csdn.net/ld362093642/article/details/78037865?locationNum=6&amp;fps=1" target="_blank">https://blog.csdn.net/ld362093642/article/details/78037865?locationNum=6&amp;fps=1</a></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6; font-size: 14pt; color: #ffffff;"><strong>七、您可以尝试添加 --skip-broken 选项来解决该问题</strong></p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202004/741594-20200405174251804-287713563.png" alt="" /></p>
<p>&nbsp;解决：yum clean all</p>
<p>&nbsp;</p>