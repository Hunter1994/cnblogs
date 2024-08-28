<p><a href="#a1">一、基本Liunx命令</a><br /><a href="#a2">二、管道符、重定向与环境变量</a><br /><a href="#a3">三、Vim编辑器</a><br /><a href="#a4">四、Shell命令脚本</a><br /><a href="#a5">五、用户身份与文件权限</a><br /><a href="#a6">六、存储结构与磁盘划分</a><br /><a href="#a7">七、RAID与LVM磁盘阵列技术</a><br /><a href="#a8">八、iptables与firewalld防火墙</a><br /><a href="#a9">九、使用ssh服务管理远程主机</a><br /><a href="#a10">十、使用Apache服务部署静态网站</a><br /><a href="#a11">十一、使用vsftpd服务传输文件</a><br /><a href="#a12">十二、使用Samba或NFS实现文件共享</a><br /><a href="#a13">十三、使用Postfix与Dovecot部署邮件系统</a><br /><a href="#a14">十四、使用iSCSI服务器部署网络存储</a><br /><a href="#a15">十五、使用MariaDB数据库管理系统</a><br /><a href="#a16">十六、使用LNMP架构部署动态网站环境</a></p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: rgba(22, 159, 230, 1);"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a1"></a>一、基本Liunx命令</span></strong></span></p>
<p><strong>1,常用系统工作命令</strong><br />&nbsp;<span class="cnblogs_code">echo hunter</span>&nbsp;&nbsp;将hunter字符输出到终端<br />&nbsp;<span class="cnblogs_code">echo $SHELL</span>&nbsp;&nbsp;使用$变量提取变量SHELL的值</p>
<p>&nbsp;<span class="cnblogs_code">date <span style="color: #800000;">"</span><span style="color: #800000;">+%Y-%m-%d %H:%M:%S</span><span style="color: #800000;">"</span> </span>&nbsp;查看格式化的时间<br />&nbsp;<span class="cnblogs_code">date -s <span style="color: #800000;">"</span><span style="color: #800000;">20210101 7:7:7</span><span style="color: #800000;">"</span> </span>&nbsp;设置时间<br />&nbsp;<span class="cnblogs_code">date <span style="color: #800000;">"</span><span style="color: #800000;">+%j</span><span style="color: #800000;">"</span> </span>&nbsp;查看当天是当年中的第几天</p>
<p>&nbsp;<span class="cnblogs_code">reboot </span>&nbsp;重启系统</p>
<p>&nbsp;<span class="cnblogs_code">poweroff</span>&nbsp;&nbsp;关闭系统</p>
<p><span class="cnblogs_code">wget http:<span style="color: #008000;">//</span><span style="color: #008000;">www.baidu.com/123.pdf </span></span>&nbsp;下载资源</p>
<ul>
<li><span style="font-size: 12px;">-b 后台下载模式</span></li>
<li><span style="font-size: 12px;">-p 下载到指定目录里</span></li>
<li><span style="font-size: 12px;">-t 最大尝试次数</span></li>
<li><span style="font-size: 12px;">-c 断点续传</span></li>
<li><span style="font-size: 12px;">-p 下载页面内所有资源，包括图片、视频等</span></li>
<li><span style="font-size: 12px;">-r 递归下载</span></li>








































































































</ul>
<p><span class="cnblogs_code">ps </span>&nbsp;用于查看系统进程的状态</p>
<ul>
<li><span style="font-size: 12px;">-a 显示所有进场（包括其他用户的进程）</span></li>
<li><span style="font-size: 12px;">-u 用户以及其他详细详细</span></li>
<li><span style="font-size: 12px;">-x 显示没有控制终端的进程</span></li>








































































































</ul>
<p><span style="font-size: 12px;">进程状态：</span><br /><span style="font-size: 12px;">R(运行)：进程正在运行或在运行队列中等待</span><br /><span style="font-size: 12px;">S(中断)：进程处于休眠中，当某个条件形成后或者接受到信号时，则脱离该状态</span><br /><span style="font-size: 12px;">D(不可中断):进程不响应系统一步信号，即便用kill命令也不能将其中断</span><br /><span style="font-size: 12px;">Z(僵死)：进程已经终止，但进程描述符依然存在，指导父进程调用wait4()系统函数后将进程释放</span><br /><span style="font-size: 12px;">T(停止)：进程收到停止信号后停止运行</span><br /><span style="font-size: 12px;">USER：进程的所有者</span><br /><span style="font-size: 12px;">PID：进程ID号</span><br /><span style="font-size: 12px;">%CPU：运算器占用率</span><br /><span style="font-size: 12px;">%MEM：内存占用率</span><br /><span style="font-size: 12px;">VSZ：虚拟内存使用量（单位KB）</span><br /><span style="font-size: 12px;">RSS：占用的固定内存量（单位KB）</span><br /><span style="font-size: 12px;">TTY：所在终端</span><br /><span style="font-size: 12px;">STAT：进程状态</span><br /><span style="font-size: 12px;">START：被启动的时间</span><br /><span style="font-size: 12px;">TIME：实际使用CPU的时间</span><br /><span style="font-size: 12px;">COMMAND：命令名称与参数</span></p>
<p>&nbsp;<span class="cnblogs_code">top </span>&nbsp;动态监视进程活动与系统负载等信息<br /><span style="font-size: 12px;">第一行：系统时间、运行时间、登录终端数、系统负载（三个数值分别为1分钟、5分钟、15分钟内的平均值，数值越小意味着负载越低）</span><br /><span style="font-size: 12px;">第二行：进程总数、运行中的进程数、睡眠中的进程数、停止的进程数、僵死的进程数</span><br /><span style="font-size: 12px;">第三行：用户占用资源百分比、系统内核占用资源百分比、改变过优先级的进程资源百分比、空闲资源百分比（第四列如果是97.1 id意味着97.1%的CPU处于空闲）</span><br /><span style="font-size: 12px;">第四行：物理内存总量、内存使用量、内存空闲量、作为内核缓存的内存量</span><br /><span style="font-size: 12px;">第五行：虚拟内存总量、虚拟内存是用量、虚拟内存空闲量、已被提前加载的内存量</span></p>
<p>&nbsp;<span class="cnblogs_code">pidof sshd </span>&nbsp;查询指定某个服务进程PID值</p>
<p>&nbsp;<span class="cnblogs_code">kill <span style="color: #800080;">2156</span> </span>&nbsp;终止进程</p>
<p>&nbsp;<span class="cnblogs_code">killall httpd </span>&nbsp;终止指定名称的服务所对应的全部进程</p>
<p>&nbsp;<span class="cnblogs_code">whereis tar</span>&nbsp;输出tar命令的绝对路径</p>
<p><br /><strong>2，系统检测命令</strong><br />&nbsp;<span class="cnblogs_code">ifconfig </span>&nbsp;获取网卡配置与网络状态等信息<br /><span style="font-size: 12px;">inet参数后面的IP地址</span><br /><span style="font-size: 12px;">enher参数后面的网卡物理地址（MAC）</span><br /><span style="font-size: 12px;">RX、TX的接受数据包与发送数据包的个数及累计流量</span></p>
<p>&nbsp;<span class="cnblogs_code">uname </span>&nbsp;查看系统内核与系统版本信息</p>
<p>&nbsp;<span class="cnblogs_code">uptime</span>&nbsp;&nbsp;查看系统的负载信息<br />系统时间、系统运行时间、启用终端数、系统负载（三个数值分别为1分钟、5分钟、15分钟内的平均值，数值越小意味着负载越低）</p>
<p>&nbsp;<span class="cnblogs_code">free -h</span>&nbsp;&nbsp;用于显示内存的使用量情况<br /><span style="font-size: 12px;">total：内存总量</span><br /><span style="font-size: 12px;">used：已用量</span><br /><span style="font-size: 12px;">free：可用量</span><br /><span style="font-size: 12px;">shared：进程共享的内存量</span><br /><span style="font-size: 12px;">buffers：磁盘缓存的内存量</span><br /><span style="font-size: 12px;">cached：缓存的内存量</span></p>
<p>&nbsp;<span class="cnblogs_code">who </span>&nbsp;查看当前登入主机的用户终端信息</p>
<p>&nbsp;<span class="cnblogs_code">last</span>&nbsp;&nbsp;查看所有系统的登录记录</p>
<p><span class="cnblogs_code">history </span>&nbsp;显示历史执行过的命令</p>
<ul>
<li><span style="font-size: 12px;">-c 清理历史记录</span></li>
<li><span style="font-size: 12px;">!31 执行第31个命令</span></li>








































































































</ul>
<p>&nbsp;<span class="cnblogs_code">sosreport </span>&nbsp;收集系统配置及架构信息并输出诊断文档</p>
<p><br /><strong>3，工作目录切换命令</strong><br />&nbsp;<span class="cnblogs_code">pwd </span>&nbsp;显示用户当前所在的工作目录</p>
<p>&nbsp;<span class="cnblogs_code">cd </span>&nbsp;切换工作路径</p>
<p>&nbsp;<span class="cnblogs_code">ls -al </span>&nbsp;显示目录中的文件信息</p>
<p><br /><strong>4，文本文件编辑命令</strong><br /><span class="cnblogs_code">cat </span>&nbsp;用于查看纯文本文件（内容较少的）</p>
<ul>
<li>-n 展示行号</li>








































































































</ul>
<p>&nbsp;<span class="cnblogs_code">more </span>&nbsp;用于查看纯文本文件（内容较多的）</p>
<p>&nbsp;<span class="cnblogs_code">head -n <span style="color: #800080;">10</span></span>&nbsp;&nbsp;用于查看纯文本的前n行</p>
<p>&nbsp;<span class="cnblogs_code">tail -n <span style="color: #800080;">10</span></span>&nbsp;&nbsp;用于查看纯文本的后n行</p>
<p>&nbsp;<span class="cnblogs_code">cat a.txt | tr [a-z] [A-Z] </span>&nbsp;将文本中的小写替换成大写</p>
<p>&nbsp;<span class="cnblogs_code">wc <span style="color: #800080;">1</span>.txt</span>&nbsp;&nbsp;统计指定文本的行数、字数、字节数</p>
<p>&nbsp;<span class="cnblogs_code">stat</span>&nbsp;&nbsp;查询文件具体的存储信息和时间信息</p>
<p>&nbsp;<span class="cnblogs_code">cut -d: -f1 /etc/passwd </span>&nbsp;提取以冒号分隔为间隔符号的第一列内容</p>
<p>&nbsp;<span class="cnblogs_code">mkdir </span>&nbsp;创建空白的目录</p>
<p><span class="cnblogs_code">cp <span style="color: #800080;">1</span>.log <span style="color: #800080;">2</span>.log </span>&nbsp;用于复制文件或目录</p>
<ul>
<li><span style="font-size: 12px;">-p 保留原始文件属性</span></li>
<li><span style="font-size: 12px;">-d 若对象为&ldquo;链接文件&rdquo;，则保留该&ldquo;链接文件&rdquo;的属性</span></li>
<li><span style="font-size: 12px;">-r 递归持续复制（用于目录）</span></li>
<li><span style="font-size: 12px;">-i 若目标文件存在则询问是否覆盖</span></li>
<li><span style="font-size: 12px;">-a 相当于-pdr</span></li>








































































































</ul>
<p>&nbsp;<span class="cnblogs_code">mv </span>&nbsp;剪切文件或者重命名文件</p>
<p>&nbsp;<span class="cnblogs_code">rm -rf </span>&nbsp;删除文件或目录</p>
<p>&nbsp;<span class="cnblogs_code">dd <span style="color: #0000ff;">if</span>=/dev/zero of=560_file count=<span style="color: #800080;">1</span> bs=560M </span>&nbsp;按照指定的大小和个数数据块来负责文件或装换文件</p>
<p>&nbsp;<span class="cnblogs_code">file <span style="color: #800080;">1</span>.txt </span>&nbsp;查看文件的类型</p>
<p><strong>5，打包压缩与搜索命令</strong><br />&nbsp;<span class="cnblogs_code">tar -xzvf <span style="color: #800080;">11</span>.tar.gz</span>&nbsp;&nbsp;解压文件<br />&nbsp;<span class="cnblogs_code">tar -czvf <span style="color: #800080;">11</span>.tar.gz /etc</span>&nbsp;&nbsp;压缩文件</p>
<p><span class="cnblogs_code">grep /sbin/nologin /etc/passwd</span>&nbsp;&nbsp;查找出当前系统中不允许登录系统的所有用户</p>
<ul>
<li>-v 反向选择</li>








































































































</ul>
<p><span class="cnblogs_code">find /etc -name <span style="color: #800000;">"</span><span style="color: #800000;">host*</span><span style="color: #800000;">"</span> -print </span>&nbsp;获取该目录以host开头的文件列表<br /><span class="cnblogs_code">find / -perm -<span style="color: #800080;">4000</span> -print </span>&nbsp;整个系统搜索权限中包括SUID权限的所有文件，只需要使用-4000即可<br /><span class="cnblogs_code">find / -user hunter -exec cp -a {} /root/findresults/ \ </span>&nbsp;搜索出所有归属于hunter用户的文件并复制到/root/findresults/目录 （{}表示find命令搜索出来的每一个文件）</p>
<ul>
<li><span style="font-size: 12px;">-name 匹配名称</span></li>
<li><span style="font-size: 12px;">-perm 匹配权限</span></li>
<li><span style="font-size: 12px;">-user 匹配所有者</span></li>
<li><span style="font-size: 12px;">-group 匹配所有组</span></li>
<li><span style="font-size: 12px;">-mtime -n +n 匹配修改内容的时间(-n指n天以内，+n指n天以前)</span></li>
<li><span style="font-size: 12px;">-atime -n +n 匹配访问文件的时间(-n指n天以内，+n指n天以前)</span></li>
<li><span style="font-size: 12px;">-ctime -n +n 匹配修改文件权限的时间(-n指n天以内，+n指n天以前)</span></li>








































































































</ul>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: rgba(22, 159, 230, 1);"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a2"></a>二、管道符、重定向与环境变量</span></strong></span></p>
<p><strong>1，输出重定向</strong><br />&nbsp;<span class="cnblogs_code">man bash &gt; readme.txt</span>&nbsp;&nbsp;标准输出重定向将man bash 命令原本要输出到屏幕的小写写入到readme.txt<br />&nbsp;<span class="cnblogs_code">echo <span style="color: #800000;">"</span><span style="color: #800000;">hunter</span><span style="color: #800000;">"</span> &gt; readme.txt</span>&nbsp;&nbsp;将"hunter"字符覆盖写入readme.txt<br />&nbsp;<span class="cnblogs_code">echo <span style="color: #800000;">"</span><span style="color: #800000;">hunter</span><span style="color: #800000;">"</span> &gt;&gt; readme.txt</span>&nbsp;&nbsp;将"hunter"字符追加写入readme.txt<br />&nbsp;<span class="cnblogs_code">ls -l xx <span style="color: #800080;">2</span>&gt; readme.txt</span>&nbsp;&nbsp;将错误小写覆盖写入readme.txt<br />&nbsp;<span class="cnblogs_code">ls -l xx <span style="color: #800080;">2</span>&gt;&gt; readme.txt</span>&nbsp;&nbsp;将错误小写追加写入readme.txt</p>
<p>&amp;&gt; 可以将错误信息或者普通信息都重定向输出</p>
<p><strong>2，管道命令符</strong><br />&nbsp;<span class="cnblogs_code">grep <span style="color: #800000;">"</span><span style="color: #800000;">/sbin/nologin</span><span style="color: #800000;">"</span> /etc/passwd |wc -l </span>&nbsp;统计被限制登录的数量<br />&nbsp;<span class="cnblogs_code">ls -l /etc/ | more</span>&nbsp;&nbsp;翻页查询/etc/下面的文件<br />&nbsp;<span class="cnblogs_code">echo <span style="color: #800000;">"</span><span style="color: #800000;">123456</span><span style="color: #800000;">"</span>|passwd --stdin root</span>&nbsp;&nbsp;设置密码（stdin防止二次确认）<br />&nbsp;<span class="cnblogs_code">echo <span style="color: #800000;">"</span><span style="color: #800000;">hi</span><span style="color: #800000;">"</span> | mail -s <span style="color: #800000;">"</span><span style="color: #800000;">subject</span><span style="color: #800000;">"</span> hunter</span>&nbsp;&nbsp;把编辑好的内容与标题一起打包，发送邮件给hunter</p>
<p><strong>3，命令行的通配符</strong><br />&nbsp;<span class="cnblogs_code">ls -l /dev/sda?</span>&nbsp;&nbsp;？代表匹配单个字符<br />&nbsp;<span class="cnblogs_code">ls -l /dev/sda*</span>&nbsp;&nbsp;*代表匹配零个或者多个字符<br />&nbsp;<span class="cnblogs_code">ls -l /dev/sda[<span style="color: #800080;">1</span>-<span style="color: #800080;">9</span>]</span>&nbsp;匹配1~9之间单个数字字符</p>
<p><strong>4，转义字符</strong><br />反斜杠(\)：使反斜杠后面的一个变量变为单纯的字符串&nbsp;&nbsp;<span class="cnblogs_code">echo <span style="color: #800000;">"</span><span style="color: #800000;">$HOME</span><span style="color: #800000;">"</span></span>&nbsp;<br />单引号('')：转义其中所有的变量为单纯的字符串&nbsp;&nbsp;<span class="cnblogs_code">echo <span style="color: #800000;">"</span><span style="color: #800000;">\$$HOME</span><span style="color: #800000;">"</span></span>&nbsp;<br />双引号("")：保留其中的变量属性，不进行转义处理<br />反引号(``)：把其中的命令执行后返回结果&nbsp;&nbsp;<span class="cnblogs_code">echo <span style="color: #800000;">'</span><span style="color: #800000;">uname -a</span><span style="color: #800000;">'</span></span>&nbsp;</p>
<p><strong>5，环境变量</strong><br /><span style="font-size: 12px;">HOME：用户的主目录（即家目录）</span><br /><span style="font-size: 12px;">SHELL：用户在使用的shell解析器名称</span><br /><span style="font-size: 12px;">HISTSIZE：输出历史命令记录条数</span><br /><span style="font-size: 12px;">HISTFILESIZE：保存的历史命令记录条数</span><br /><span style="font-size: 12px;">MAIL：邮件保存路径</span><br /><span style="font-size: 12px;">LNAG：系统语言、语系名称</span><br /><span style="font-size: 12px;">RANDOM：生产一个随机数字</span><br /><span style="font-size: 12px;">PS1：Bash解析器的提示符</span><br /><span style="font-size: 12px;">PATH：定义解析器搜索用户执行命令的路径</span><br /><span style="font-size: 12px;">EDITOR：用户默认的文本编辑器</span></p>
<p>&nbsp;<span class="cnblogs_code">alias rm</span>&nbsp;&nbsp;查询实际命令<br />&nbsp;<span class="cnblogs_code">PATH=$PATH:/root/bin</span>&nbsp;&nbsp;设置环境变量（PATH会告诉Bash解析器执行的命令可能放在哪个位置）<br />&nbsp;<span class="cnblogs_code">env</span>&nbsp;&nbsp;查询系统中所有的环境变量<br />&nbsp;<span class="cnblogs_code">WORKDIR=/home/workdir</span>&nbsp;&nbsp;设置变量<br />&nbsp;<span class="cnblogs_code">export WORKDIR</span>&nbsp;&nbsp;提升变量为全局变量，其他用户也可以使用</p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: rgba(22, 159, 230, 1);"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a3"></a>三、Vim编辑器</span></strong></span></p>
<p><strong>1，vim文本编辑器</strong></p>
<p>①vim中常用的命令<br />dd	删除（剪切）光标所在整行<br />5dd	删除（剪切）从光标处开始的5行<br />yy	复制光标所在整行<br />5yy	复制从光标处开始的5行<br />n	显示搜索命令定位到下一个字符串<br />N	显示搜索命令定位到上一个字符串<br />u	撤销上一步操作<br />p	将之前删除（dd）或者复制（yy）过的数据粘贴到光标后面</p>
<p>②末行模式可用的命令<br />:w		保存<br />:q		退出<br />:q!		强制退出<br />:wq!	强制保存退出<br />:set nu	显示行号<br />:set nonu 不显示行号<br />:命令	执行该命令<br />:整数	跳转到该行<br />:s/one/two 将当前光标所在行的第一个one替换成two<br />:s/one/two/g 将当前光标所在行的所有one替换成two<br />:%s/one/two/g 将全文中所有one替换成two<br />?字符串	在文本中从下至上搜索该字符串<br />/字符串	在文本中从上至下搜索该字符串</p>
<p><strong>&nbsp;2，配置网卡</strong></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('b4044d3a-8940-4bbb-9819-b4a4a47047a3')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_b4044d3a-8940-4bbb-9819-b4a4a47047a3" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_b4044d3a-8940-4bbb-9819-b4a4a47047a3" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_b4044d3a-8940-4bbb-9819-b4a4a47047a3" class="cnblogs_code_hide">
<pre>TYPE=<span style="color: #000000;">Ethernet
BOOTPROTO</span>=<span style="color: #0000ff;">static</span><span style="color: #000000;">
IPADDR</span>=<span style="color: #800080;">192.168</span>.<span style="color: #800080;">0.140</span><span style="color: #000000;">
NETMASK</span>=<span style="color: #800080;">255.255</span>.<span style="color: #800080;">255.0</span><span style="color: #000000;">
GATEWAY</span>=<span style="color: #800080;">192.168</span>.<span style="color: #800080;">0.1</span><span style="color: #000000;">
NAME</span>=<span style="color: #000000;">ens32
DEVICE</span>=<span style="color: #000000;">ens32
ONBOOT</span>=<span style="color: #000000;">yes
DNS1</span>=<span style="color: #800080;">192.168</span>.<span style="color: #800080;">0.1</span></pre>
</div>
<span class="cnblogs_code_collapse">vim ifcfg-ens32</span></div>
<p>&nbsp;<span class="cnblogs_code">systemctl restart network</span>&nbsp;重启网卡</p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: rgba(22, 159, 230, 1);"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a4"></a>四、Shell命令脚本</span></strong></span></p>
<p><strong>1，接受用户参数</strong></p>
<div class="cnblogs_code">
<pre>#!/bin/<span style="color: #000000;">bash
echo </span><span style="color: #800000;">"</span><span style="color: #800000;">当前脚本名称$0</span><span style="color: #800000;">"</span><span style="color: #000000;">
echo </span><span style="color: #800000;">"</span><span style="color: #800000;">总共有$#个参数，分别是$*</span><span style="color: #800000;">"</span><span style="color: #000000;">
echo </span><span style="color: #800000;">"</span><span style="color: #800000;">第1个参数为$1,第5个参数为$5</span><span style="color: #800000;">"</span></pre>
</div>
<pre>#!/bin/<span>bash 用来告诉系统使用哪种shell解析器<br />$0　　当前shell脚本的名称<br />$#　　对应的是总共几个参数<br />$*　　所有的参数值<br />$?　　显示上一次命令的执行返回值<br />$1 $2 $3 分别对应着第N个位置的参数值<br /></span></pre>
<p><strong>2，判断用户的参数</strong></p>
<p>①文件测试语句</p>
<p><span style="font-size: 12px;">-d　　测试文件是否为目录类型</span></p>
<p><span style="font-size: 12px;">-e　　测试文件是否存在</span></p>
<p><span style="font-size: 12px;">-f　　判断是否为一般文件</span></p>
<p><span style="font-size: 12px;">-r　　测试当前用户是否有权限读取</span></p>
<p><span style="font-size: 12px;">-w　　测试当前用户是否有权限写入</span></p>
<p><span style="font-size: 12px;">-x　　测试当前用户是否有权限执行</span></p>
<p>判断/etc/fstab 是否为一个目录类型文件，然后同$?显示上一条命令执行后的返回值。如果返回0，则目录存在；如果返回值非零的值，则意味着目录不存在</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202010/741594-20201031101957468-399021858.png" alt="" loading="lazy" /></p>
<p>&nbsp;</p>
<p>判断/etc/fstab是否是一般文件</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202010/741594-20201031102312614-2089179848.png" alt="" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;判断文件是否存在，如果存在输出&ldquo;Exist&rdquo;</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202010/741594-20201031102440684-153693344.png" alt="" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;判断当前用户如果不是root则输出&ldquo;user&rdquo;，如果是root则输出&ldquo;root&rdquo;</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202010/741594-20201031102815019-1372055486.png" alt="" loading="lazy" /></p>
<p>&nbsp;</p>
<p>②可用的整数比较运算符</p>
<p><span style="font-size: 12px;">-eq　　是否等于</span></p>
<p><span style="font-size: 12px;">-ne　　是否不等于</span></p>
<p><span style="font-size: 12px;">-gt　　 是否大于</span></p>
<p><span style="font-size: 12px;">-lt　　&nbsp; 是否小于</span></p>
<p><span style="font-size: 12px;">-le　　是否等于或小于</span></p>
<p><span style="font-size: 12px;">-ge　　是否大于或等于</span></p>
<p>判断是否内存不足</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202010/741594-20201031103253607-711864298.png" alt="" loading="lazy" /></p>
<p>&nbsp;</p>
<p>③ 常见的字符串比较运算符</p>
<p>=　　比较字符串内容是否相等</p>
<p>!=　　比较字符串内容是否不同</p>
<p>-z　　判断字符串内容是否为空</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202010/741594-20201031103446334-1973592935.png" alt="" loading="lazy" /></p>
<p>&nbsp;</p>
<p><strong>3，流程控制语句&nbsp;</strong></p>
<p>①if条件测试语句</p>
<p>判断/media/cdrom 文件是否存在，不存在则创建一个</p>
<div class="cnblogs_code">
<pre>#!/bin/<span style="color: #000000;">bash
DIR</span>=<span style="color: #800000;">"</span><span style="color: #800000;">/media/cdrom</span><span style="color: #800000;">"</span>
<span style="color: #0000ff;">if</span> [ ! -<span style="color: #000000;">e $DIR ]
then
mkdir </span>-<span style="color: #000000;">p $DIR
fi</span></pre>
</div>
<p>验证ip地址是否可访问</p>
<div class="cnblogs_code">
<pre>#!/bin/<span style="color: #000000;">bash
# </span>-c 规定尝试次数 -i 每个数据包的发送间隔 -<span style="color: #000000;">W 定义等待超时时间
ping </span>-c <span style="color: #800080;">3</span> -i <span style="color: #800080;">0.2</span> -W <span style="color: #800080;">3</span> $<span style="color: #800080;">1</span> &amp;&gt; /dev/<span style="color: #0000ff;">null</span>
<span style="color: #0000ff;">if</span> [ $? -eq <span style="color: #800080;">0</span><span style="color: #000000;"> ]
then
echo </span><span style="color: #800000;">"</span><span style="color: #800000;">Host $1 is On-line</span><span style="color: #800000;">"</span>
<span style="color: #0000ff;">else</span><span style="color: #000000;">
echo </span><span style="color: #800000;">"</span><span style="color: #800000;">Host $1 is Off-line</span><span style="color: #800000;">"</span><span style="color: #000000;">
fi</span></pre>
</div>
<p>根据客户端输入的分数检测分数是否合格</p>
<div class="cnblogs_code">
<pre>#!/bin/<span style="color: #000000;">bash
read </span>-p <span style="color: #800000;">"</span><span style="color: #800000;">请输入分数</span><span style="color: #800000;">"</span><span style="color: #000000;"> GRADE
</span><span style="color: #0000ff;">if</span> [ $GRADE -ge <span style="color: #800080;">85</span> ] &amp;&amp; [ $GRADE -le <span style="color: #800080;">100</span><span style="color: #000000;"> ] ; then
echo </span><span style="color: #800000;">"</span><span style="color: #800000;">$GRADE 成绩优秀</span><span style="color: #800000;">"</span><span style="color: #000000;">
elif [ $GRADE </span>-ge <span style="color: #800080;">70</span> ] &amp;&amp; [ $GRADE -le <span style="color: #800080;">84</span><span style="color: #000000;"> ] ; then
echo </span><span style="color: #800000;">"</span><span style="color: #800000;">$GRADE 通过</span><span style="color: #800000;">"</span>
<span style="color: #0000ff;">else</span><span style="color: #000000;">
echo </span><span style="color: #800000;">"</span><span style="color: #800000;">$GRADE 不及格</span><span style="color: #800000;">"</span><span style="color: #000000;">
fi</span></pre>
</div>
<p>&nbsp;</p>
<p>②for条件循环语句</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">for</span> 变量名 <span style="color: #0000ff;">in</span><span style="color: #000000;"> 取值列表
</span><span style="color: #0000ff;">do</span><span style="color: #000000;">
...
done</span></pre>
</div>
<p>批量创建用户</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('38d2dae3-2946-490e-bfa8-be9ebdb4eea2')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_38d2dae3-2946-490e-bfa8-be9ebdb4eea2" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_38d2dae3-2946-490e-bfa8-be9ebdb4eea2" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_38d2dae3-2946-490e-bfa8-be9ebdb4eea2" class="cnblogs_code_hide">
<pre><span style="color: #000000;">user001
user002
user003
user004</span></pre>
</div>
<span class="cnblogs_code_collapse">vim users.txt</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('d13c8908-2bdb-4a53-8268-98c58c569647')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_d13c8908-2bdb-4a53-8268-98c58c569647" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_d13c8908-2bdb-4a53-8268-98c58c569647" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_d13c8908-2bdb-4a53-8268-98c58c569647" class="cnblogs_code_hide">
<pre>#!/bin/<span style="color: #000000;">bash
read </span>-p <span style="color: #800000;">"</span><span style="color: #800000;">请输入密码</span><span style="color: #800000;">"</span><span style="color: #000000;"> PASSWD
</span><span style="color: #0000ff;">for</span> UNAME <span style="color: #0000ff;">in</span><span style="color: #000000;"> `cat users.txt`
</span><span style="color: #0000ff;">do</span><span style="color: #000000;">
id $UNAME </span>&amp;&gt; /dev/<span style="color: #0000ff;">null</span>
<span style="color: #0000ff;">if</span> [ $? -eq <span style="color: #800080;">0</span><span style="color: #000000;"> ]
then
echo </span><span style="color: #800000;">"</span><span style="color: #800000;">$UNAME , 该用户已存在</span><span style="color: #800000;">"</span>
<span style="color: #0000ff;">else</span><span style="color: #000000;">
useradd $UNAME </span>&amp;&gt; /dev/<span style="color: #0000ff;">null</span><span style="color: #000000;">
echo </span><span style="color: #800000;">"</span><span style="color: #800000;">$PASSWD</span><span style="color: #800000;">"</span> | passwd --stdin $UNAME &amp;&gt; /dev/<span style="color: #0000ff;">null</span>
<span style="color: #0000ff;">if</span> [ $? -eq <span style="color: #800080;">0</span><span style="color: #000000;"> ]
then
echo </span><span style="color: #800000;">"</span><span style="color: #800000;">$UNAME , 创建成功</span><span style="color: #800000;">"</span>
<span style="color: #0000ff;">else</span><span style="color: #000000;">
echo </span><span style="color: #800000;">"</span><span style="color: #800000;">$UNAME , 创建失败</span><span style="color: #800000;">"</span><span style="color: #000000;">
fi
fi
done</span></pre>
</div>
<span class="cnblogs_code_collapse">vim addusers.sh</span></div>
<p>批量检测ip是否在线</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('f6a6a700-9509-4739-b993-aec7fb17dec6')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_f6a6a700-9509-4739-b993-aec7fb17dec6" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_f6a6a700-9509-4739-b993-aec7fb17dec6" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_f6a6a700-9509-4739-b993-aec7fb17dec6" class="cnblogs_code_hide">
<pre><span style="color: #800080;">192.168</span>.<span style="color: #800080;">0.1</span>
<span style="color: #800080;">192.168</span>.<span style="color: #800080;">0.103</span>
<span style="color: #800080;">192.168</span>.<span style="color: #800080;">0.102</span>
<span style="color: #800080;">192.168</span>.<span style="color: #800080;">0.105</span></pre>
</div>
<span class="cnblogs_code_collapse">vim ipadds.txt</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('adc245a3-59ec-48a3-b4c1-44c79999c1ab')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_adc245a3-59ec-48a3-b4c1-44c79999c1ab" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_adc245a3-59ec-48a3-b4c1-44c79999c1ab" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_adc245a3-59ec-48a3-b4c1-44c79999c1ab" class="cnblogs_code_hide">
<pre>#!/bin/<span style="color: #000000;">bash
HLIST</span>=$(cat ~/<span style="color: #000000;">ipadds.txt)
</span><span style="color: #0000ff;">for</span> IP <span style="color: #0000ff;">in</span><span style="color: #000000;"> $HLIST
</span><span style="color: #0000ff;">do</span><span style="color: #000000;">
ping </span>-c <span style="color: #800080;">3</span> -i <span style="color: #800080;">0.3</span> -W <span style="color: #800080;">3</span> $IP &amp;&gt; /dev/<span style="color: #0000ff;">null</span>
<span style="color: #0000ff;">if</span> [ $? -eq <span style="color: #800080;">0</span><span style="color: #000000;"> ]
then
echo </span><span style="color: #800000;">"</span><span style="color: #800000;">$IP , 访问成功</span><span style="color: #800000;">"</span>
<span style="color: #0000ff;">else</span><span style="color: #000000;">
echo </span><span style="color: #800000;">"</span><span style="color: #800000;">$IP , 访问失败</span><span style="color: #800000;">"</span><span style="color: #000000;">
fi
done</span></pre>
</div>
<span class="cnblogs_code_collapse">vim CheckHosts.sh</span></div>
<p>&nbsp;</p>
<p>③while条件循环语句</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">while</span><span style="color: #000000;"> 条件测试操作
</span><span style="color: #0000ff;">do</span><span style="color: #000000;">
...
done</span></pre>
</div>
<div class="cnblogs_code" onclick="cnblogs_code_show('ebfd6e3e-9a51-41ce-be05-bff532bcc4ff')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_ebfd6e3e-9a51-41ce-be05-bff532bcc4ff" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_ebfd6e3e-9a51-41ce-be05-bff532bcc4ff" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_ebfd6e3e-9a51-41ce-be05-bff532bcc4ff" class="cnblogs_code_hide">
<pre>#!/bin/<span style="color: #000000;">bash
PRICE</span>=$( expr $RANDOM % <span style="color: #800080;">1000</span><span style="color: #000000;"> )
TIMES</span>=<span style="color: #800080;">0</span><span style="color: #000000;">
echo </span><span style="color: #800000;">"</span><span style="color: #800000;">实际价格在0-999之间，猜猜看是多少？</span><span style="color: #800000;">"</span>
<span style="color: #0000ff;">while</span> <span style="color: #0000ff;">true</span>
<span style="color: #0000ff;">do</span><span style="color: #000000;">
read </span>-p <span style="color: #800000;">"</span><span style="color: #800000;">请输入您猜测的价格：</span><span style="color: #800000;">"</span><span style="color: #000000;"> INT
let TIMES</span>++
<span style="color: #0000ff;">if</span> [ $INT -<span style="color: #000000;">eq $PRICE ] ; then
echo </span><span style="color: #800000;">"</span><span style="color: #800000;">恭喜您，猜对了，实际价格为 $PRICE </span><span style="color: #800000;">"</span><span style="color: #000000;">
echo </span><span style="color: #800000;">"</span><span style="color: #800000;">您一共猜了 $TIMES 次</span><span style="color: #800000;">"</span><span style="color: #000000;">
exit </span><span style="color: #800080;">0</span><span style="color: #000000;">
elif [ $INT </span>-<span style="color: #000000;">gt $PRICE ] ; then
echo </span><span style="color: #800000;">"</span><span style="color: #800000;">太高了!</span><span style="color: #800000;">"</span>
<span style="color: #0000ff;">else</span><span style="color: #000000;">
echo </span><span style="color: #800000;">"</span><span style="color: #800000;">太低了!</span><span style="color: #800000;">"</span><span style="color: #000000;">
fi
done</span></pre>
</div>
<span class="cnblogs_code_collapse">价格猜测游戏 vim Guess.sh</span></div>
<p>&nbsp;</p>
<p>④case条件测试语句</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">case</span> 变量值 <span style="color: #0000ff;">in</span><span style="color: #000000;">
模式1)
    命令序列1
;;
模式2)
    命令序列2
;;
</span>*<span style="color: #000000;">)
    默认命令序列
esac</span></pre>
</div>
<div class="cnblogs_code" onclick="cnblogs_code_show('9c9015d8-55b5-486e-905c-d7e1b056599b')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_9c9015d8-55b5-486e-905c-d7e1b056599b" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_9c9015d8-55b5-486e-905c-d7e1b056599b" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_9c9015d8-55b5-486e-905c-d7e1b056599b" class="cnblogs_code_hide">
<pre>#!/bin/<span style="color: #000000;">bash
read </span>-p <span style="color: #800000;">"</span><span style="color: #800000;">请输入一个字符，并按Enter键确认：</span><span style="color: #800000;">"</span><span style="color: #000000;"> KEY
</span><span style="color: #0000ff;">case</span> <span style="color: #800000;">"</span><span style="color: #800000;">$KEY</span><span style="color: #800000;">"</span> <span style="color: #0000ff;">in</span><span style="color: #000000;">
[a</span>-z]|[A-<span style="color: #000000;">Z])
echo </span><span style="color: #800000;">"</span><span style="color: #800000;">您输入的是字母</span><span style="color: #800000;">"</span><span style="color: #000000;">
;;
[</span><span style="color: #800080;">0</span>-<span style="color: #800080;">9</span><span style="color: #000000;">])
echo </span><span style="color: #800000;">"</span><span style="color: #800000;">您输入的是数字</span><span style="color: #800000;">"</span><span style="color: #000000;">
;;
</span>*<span style="color: #000000;">)
echo &ldquo;您输入的是 空格、功能键或者其他控制字符&rdquo;
esac</span></pre>
</div>
<span class="cnblogs_code_collapse">输入一个字符提示识别是数字还是字母 vim CheckKeys.sh</span></div>
<p>&nbsp;</p>
<p>4，计划任务服务程序</p>
<p>①at 一次性计划任务</p>
<p>&nbsp;<span class="cnblogs_code">echo <span style="color: #800000;">"</span><span style="color: #800000;">systemctl restart httpd</span><span style="color: #800000;">"</span> | at <span style="color: #800080;">23</span>:<span style="color: #800080;">00</span></span>&nbsp;创建任务</p>
<p>&nbsp;<span class="cnblogs_code">at -l</span>&nbsp;查看任务</p>
<p>&nbsp;<span class="cnblogs_code">atrm <span style="color: #800080;">4</span></span>&nbsp;删除任务</p>
<p>②crontab 长期性计划任务</p>
<p>&nbsp;<span class="cnblogs_code">crontab -e</span>&nbsp;创建/编辑计划任务</p>
<p>&nbsp;<span class="cnblogs_code">crontab -l</span>&nbsp;显示计划任务</p>
<p>&nbsp;<span class="cnblogs_code">crontab -r</span>&nbsp;删除计划任务</p>
<p>&nbsp;<span class="cnblogs_code">*/<span style="color: #800080;">1</span> * * * * /usr/bin/tar -czvf /root/readme.txt.tar.gz /root</span>&nbsp;&nbsp;每隔一分钟打包/root</p>
<p>&nbsp;<span class="cnblogs_code"><span style="color: #800080;">25</span> <span style="color: #800080;">3</span> * * <span style="color: #800080;">1</span>,<span style="color: #800080;">3</span>,<span style="color: #800080;">5</span> /usr/bin/tar -czvf /root/readme.txt.tar.gz /root</span>&nbsp;每周一、三、五的凌晨3点25分打包/root</p>
<p>&nbsp;<span class="cnblogs_code"><span style="color: #800080;">0</span> <span style="color: #800080;">1</span> * * <span style="color: #800080;">1</span>-<span style="color: #800080;">5</span> /usr/bin/rm -rf /tmp<span style="color: #008000;">/*</span></span>&nbsp;每周一到周五的凌晨1点自动清空/tmp目录内的所有文件</p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: rgba(22, 159, 230, 1);"><span style="color: #ffffff;"><strong><a name="a5"></a>五、用户身份与文件权限</strong></span></p>
<p><strong>1，用户身份与能力</strong></p>
<p>①useradd 添加用户</p>
<ul>
<li><span style="font-size: 12px;">-d　　指定用户的家目录</span></li>
<li><span style="font-size: 12px;">-e　　账户的到期时间，格式为YYYY-MM-DD</span></li>
<li><span style="font-size: 12px;">-u　　指定该用户的默认UID</span></li>
<li><span style="font-size: 12px;">-g　　指定一个初始化的用户基本组（必须已存在）</span></li>
<li><span style="font-size: 12px;">-G　　指定一个或多个扩展用户组</span></li>
<li><span style="font-size: 12px;">-N　　不创建与用户同名的基本用户组</span></li>
<li><span style="font-size: 12px;">-s　　指定该用户的默认Shell解析器</span></li>
</ul>
<p>&nbsp;<span class="cnblogs_code">useradd user005</span>&nbsp;创建用户</p>
<p>&nbsp;<span class="cnblogs_code">usermod -s /sbin/nologin user001</span>&nbsp;创建用户（用户不可登陆）</p>
<p>&nbsp;<span class="cnblogs_code">id user001</span>&nbsp;查看用户信息</p>
<p>②groupadd 创建用户组</p>
<p>&nbsp;<span class="cnblogs_code">groupadd ronny</span>&nbsp;创建用户组，可以针对一类用户统一安排权限</p>
<p>③usermod 修改用户的属性</p>
<ul>
<li><span style="font-size: 12px;">-c　　填写用户账户的备注信息</span></li>
<li><span style="font-size: 12px;">-d -m　　参数一起用，可以重新指定用户的家目录并自动把旧的数据转移过去</span></li>
<li><span style="font-size: 12px;">-e　　账户的到期时间，格式为YYYY-MM-DD</span></li>
<li><span style="font-size: 12px;">-g　　变更所属用户组</span></li>
<li><span style="font-size: 12px;">-G　　变更扩展用户组</span></li>
<li><span style="font-size: 12px;">-L　　锁定用户禁止其登录系统</span></li>
<li><span style="font-size: 12px;">-U　　解锁用户，允许其登录系统</span></li>
<li><span style="font-size: 12px;">-s　　变更默认终端</span></li>
<li><span style="font-size: 12px;">-u　　修改用户的UID</span></li>
</ul>
<p>④passwd 修改用户密码&nbsp;</p>
<ul>
<li><span style="font-size: 12px;">-l　　锁定用户，禁止其登录</span></li>
<li><span style="font-size: 12px;">-u　　接触锁定，允许用户登录</span></li>
<li><span style="font-size: 12px;">--stdin　　允许通过标准输入修改密码。如：echo "123456" | pwsswd --stdin Username</span></li>
<li><span style="font-size: 12px;">-d　　该用户可以用空密码登录系统</span></li>
<li><span style="font-size: 12px;">-e　　强制用户在下次登录时修改密码</span></li>
<li><span style="font-size: 12px;">-S　　显示用户的密码是否被锁定，以及密码所采用的加密算法名称</span></li>
</ul>
<p>&nbsp;<span class="cnblogs_code">passwd</span>&nbsp;修改自己的密码</p>
<p>&nbsp;<span class="cnblogs_code">passwd username</span>&nbsp;修改别人的密码（需要有root管理员权限）</p>
<p>&nbsp;<span class="cnblogs_code">passwd -l user001</span>&nbsp;锁定账户</p>
<p>&nbsp;<span class="cnblogs_code">passwd -u user001</span>&nbsp;解锁账户</p>
<p>⑤userdel</p>
<ul>
<li><span style="font-size: 12px;">-f　　强制删除用户</span></li>
<li><span style="font-size: 12px;">-r　　同时删除用户及用户家目录</span></li>
</ul>
<p>&nbsp;<span class="cnblogs_code">userdel -rf user005</span>&nbsp;强制删除用户及家目录</p>
<p>&nbsp;</p>
<p><strong>2，文件权限与归属</strong></p>
<p>-：普通文件</p>
<p>d：目录文件</p>
<p>l：链接文件</p>
<p>b：块设备文件</p>
<p>c：字符设备文件</p>
<p>p：管道文件</p>
<p>针对目录：可读（能够读取目录内的文件列表）；可写（能够在目录内新增、删除、重命名文件）；可执行（能够进入该目录）</p>
<table style="height: 108px; width: 950px;" border="1"><caption>&nbsp;</caption>
<tbody>
<tr style="background-color: #787473;">
<td>权限分配</td>
<td colspan="3">文件所有者</td>
<td colspan="3">文件所属者</td>
<td colspan="3">其他用户</td>
</tr>
<tr>
<td>权限项</td>
<td>读</td>
<td>写</td>
<td>执行</td>
<td>读</td>
<td>写</td>
<td>执行</td>
<td>读</td>
<td>写</td>
<td>执行</td>
</tr>
<tr>
<td>字符表示</td>
<td>r</td>
<td>w</td>
<td>x</td>
<td>r</td>
<td>w</td>
<td>x</td>
<td>r</td>
<td>w</td>
<td>x</td>
</tr>
<tr>
<td>数字表示</td>
<td>4</td>
<td>2</td>
<td>1</td>
<td>4</td>
<td>2</td>
<td>1</td>
<td>4</td>
<td>2</td>
<td>1</td>
</tr>
</tbody>
</table>
<p>&nbsp;<span class="cnblogs_code">chmod <span style="color: #800080;">666</span> a</span>&nbsp;修改文件a的权限为rw-rw-rw-</p>
<p>&nbsp;<span class="cnblogs_code">chown hunter:root a</span>&nbsp;修改文件a的属主为hunter，属组为root</p>
<p><span style="font-size: 12px;">如果针对目录。加上-R来表示递归，针对目录内所有的文件进行整体操作</span></p>
<p>&nbsp;<span class="cnblogs_code">chmod -R o+t tmp/</span>&nbsp;将此文件设置为SBIT特殊权限位（tmp下面创建文件只能由创建者删除）</p>
<p>&nbsp;</p>
<p><strong>3，文件的隐藏属性</strong></p>
<p>①chattr 设置文件的隐藏权限（添加用 &ldquo;+参数&rdquo; ；移除用 &ldquo;-参数&rdquo;）</p>
<ul>
<li><span style="font-size: 12px;">i　　无法对文件进行修改；若对目录设置了该参数，则仅能修改其中的子文件内容而不能新增或删除文件</span></li>
<li><span style="font-size: 12px;">a　&nbsp; 仅允许补充（追加）内容，无法覆盖/删除内容</span></li>
<li><span style="font-size: 12px;">S&nbsp;　 文件内容在变更后立即同步到硬盘</span></li>
<li><span style="font-size: 12px;">s　　彻底从硬盘中删除，不可恢复（用0填充原文件所在的硬盘区域）</span></li>
<li><span style="font-size: 12px;">A　　不再修改这个文件或目录的最后访问时间</span></li>
<li><span style="font-size: 12px;">b　　不再修改无尽啊或目录的存取时间</span></li>
<li><span style="font-size: 12px;">D　　检查压缩文件中的错误</span></li>
<li><span style="font-size: 12px;">d　　使用dump命令备份时忽略本文件/目录</span></li>
<li><span style="font-size: 12px;">c　　默认将文件或目录进行压缩</span></li>
<li><span style="font-size: 12px;">u　　当删除该文件后依然保留其在硬盘中的数据，方便日后恢复</span></li>
<li><span style="font-size: 12px;">t　　让文件系统支持尾部合并</span></li>
<li><span style="font-size: 12px;">X　&nbsp; 可以直接访问压缩文件中内容</span></li>
</ul>
<p>&nbsp;<span class="cnblogs_code">chattr +a a</span>&nbsp;仅允许补充（追加）内容，无法覆盖/删除内容</p>
<p>&nbsp;<span class="cnblogs_code">lsattr a</span>&nbsp;查询隐藏属性</p>
<p>&nbsp;</p>
<p><strong>4，文件访问控制列表</strong></p>
<p>&nbsp;<span class="cnblogs_code">setfacl -Rm u:hunter:rwx /root</span>&nbsp; 递归设置/root下面的所有文件或目录对hunter用户可读、可写、可执行</p>
<p>&nbsp;<span class="cnblogs_code">getfacl /root/</span>&nbsp;查询文件设置的acl信息</p>
<p><span style="font-size: 12px;">ls 查看文件后面的不是.而是+这说明文件以及设置acl了</span></p>
<p>&nbsp;</p>
<p><strong>5，su命令与sudo服务</strong></p>
<p>&nbsp;<span class="cnblogs_code">su - root</span>&nbsp;加上减号说明完全切换到新的用户，即把环境变量信息也更新为新用户的相应信息</p>
<p>sudo：给普通用户提供额外的权限完成root管理员才能完成的事情</p>
<ul>
<li><span style="font-size: 12px;">-h　　列出帮助信息</span></li>
<li><span style="font-size: 12px;">-l　　列出放弃用户可执行的命令</span></li>
<li><span style="font-size: 12px;">-u用户名或者UID值　　以指定的用户身份执行命令</span></li>
<li><span style="font-size: 12px;">-k　　清空密码的有效时间，下次执行sudo时需要再次进行密码验证</span></li>
<li><span style="font-size: 12px;">-b　　在后台执行指定的命令</span></li>
<li><span style="font-size: 12px;">-p　　更改询问密码的提示语</span></li>
</ul>
<p>&nbsp;<span class="cnblogs_code">visudo</span>&nbsp;配置sudo命令配置文件</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202011/741594-20201101193858509-1626300769.png" alt="" loading="lazy" /></p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: rgba(22, 159, 230, 1);"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a6"></a>六、存储结构与磁盘划分</span></strong></span></p>
<table style="height: 523px; width: 1038px;" border="1"><caption>Liunx系统中常见的目录名称以及相应的内容&nbsp;</caption>
<tbody>
<tr style="background-color: #7e7877;">
<td>目录名称</td>
<td>应放置文件内容</td>
</tr>
<tr>
<td>/boot</td>
<td>开机所需文件--内核、开机菜单以及所需配置文件等</td>
</tr>
<tr>
<td>/dev</td>
<td>以文件形式存放任何设备与接口</td>
</tr>
<tr>
<td>/etc</td>
<td>配置文件</td>
</tr>
<tr>
<td>/home</td>
<td>用户家目录</td>
</tr>
<tr>
<td>/bin</td>
<td>存放单用户模式下还可以操作的命令</td>
</tr>
<tr>
<td>/lib</td>
<td>开机时用到的函数库，以及/bin与/sbin下面的命令要调用的函数</td>
</tr>
<tr>
<td>/sbin</td>
<td>开机过程中需要的命令</td>
</tr>
<tr>
<td>/media</td>
<td>用于挂载设备文件的目录</td>
</tr>
<tr>
<td>/opt</td>
<td>放置第三方的软件</td>
</tr>
<tr>
<td>/root</td>
<td>系统管理员的家目录</td>
</tr>
<tr>
<td>/srv</td>
<td>一些网络服务的数据文件目录</td>
</tr>
<tr>
<td>/tmp</td>
<td>任何人均可使用的&ldquo;共享&rdquo;临时目录</td>
</tr>
<tr>
<td>/proc</td>
<td>虚拟文件系统，例如系统内核、进程、外部设备及网络状态等</td>
</tr>
<tr>
<td>/usr/local</td>
<td>用户自行安装的软件</td>
</tr>
<tr>
<td>/usr/sbin</td>
<td>Liunx系统开机时不会使用到的软件/命令/脚本</td>
</tr>
<tr>
<td>/usr/share</td>
<td>帮助与说明文件，也可以放置共享文件</td>
</tr>
<tr>
<td>/var</td>
<td>主要存放经常变化的文件，如日志</td>
</tr>
<tr>
<td>/lost+found</td>
<td>当文件系统发生错误时，将一些丢失的文件片段存放在这里</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<p><strong>1，物理设备的命名规则</strong></p>
<table style="height: 170px; width: 914px;" border="0"><caption>常见的硬件设备及其文件名称</caption>
<tbody>
<tr style="background-color: #8b8888;">
<td>硬件设备</td>
<td>文件名称</td>
</tr>
<tr>
<td>IDE设备(设备很少见了)</td>
<td>/dev/hd[a-d]</td>
</tr>
<tr>
<td>SCSI/SATA/U盘</td>
<td>/dev/sd[a-p]</td>
</tr>
<tr>
<td>软驱</td>
<td>/dev/fd[0-1]</td>
</tr>
<tr>
<td>打印机</td>
<td>/dev/lp[0-15]</td>
</tr>
<tr>
<td>光驱</td>
<td>/dev/cdrom</td>
</tr>
<tr>
<td>鼠标</td>
<td>/dev/mouse</td>
</tr>
<tr>
<td>磁带机</td>
<td>/dev/st0或/dev/ht0</td>
</tr>
</tbody>
</table>
<p>一台电脑可以有多快硬盘，a~p来代表16快不同的硬盘（默认从a开始分配），硬盘的分区编号也有讲究</p>
<ul>
<li><span style="font-size: 12px;">主分区或扩展分区的编号从1开始，到4结束；</span></li>
<li><span style="font-size: 12px;">逻辑分区从编号5开始</span></li>
</ul>
<p><strong>2，挂载硬件设备</strong></p>
<p>①mount　　挂载文件系统</p>
<ul>
<li><span style="font-size: 12px;">-a　　挂载所有在/etc/fstab中定义的文件系统（自动检查/etc/fstab有没有疏漏被挂载的设备文件，如果有，则自动挂载）</span></li>
<li><span style="font-size: 12px;">-t　　指定文件系统的类型</span></li>
</ul>
<p>&nbsp;<span class="cnblogs_code">mount /dev/sdb1 /backup</span>&nbsp;挂载文件系统</p>
<p>&nbsp;<span class="cnblogs_code">umount /dev/sdb1</span>&nbsp;撤销已挂载的设备文件</p>
<p>&nbsp;<span class="cnblogs_code">vim /etc/fstab</span>&nbsp;永久挂载</p>
<ul>
<li><span style="font-size: 12px;">设备文件：一般为设备的路径+设备名称。也可以写唯一识别码（UUID）</span></li>
<li><span style="font-size: 12px;">挂载目录：指定要挂载到的目录，需要在挂载前创建好</span></li>
<li><span style="font-size: 12px;">格式类型：指定文件系统的格式，比如Ext3、Ext4、XFS、SWAP、iso9660（此为光盘设备）等</span></li>
<li><span style="font-size: 12px;">权限选项：若设置defaults，则默认权限为：rw，suid，dev，exec，auto，nouser，async</span></li>
<li><span style="font-size: 12px;">是否备份：若为1则开机后使用dnmp进行磁盘备份，为0则不备份</span></li>
<li><span style="font-size: 12px;">是否自检：若为1则开机进行磁盘自检，为0则不自检测</span></li>
</ul>
<p>&nbsp;<img src="https://img2020.cnblogs.com/blog/741594/202011/741594-20201102001337007-1116746216.png" alt="" width="625" height="69" loading="lazy" /></p>
<p>&nbsp;</p>
<p><span style="font-size: 12px;">&nbsp;配置完毕重新系统</span></p>
<p>②fdisk　　用于管理磁盘分区（交互式的命令）</p>
<ul>
<li><span style="font-size: 12px;">m　　查看全部可用参数</span></li>
<li><span style="font-size: 12px;">n　　添加新的分区</span></li>
<li><span style="font-size: 12px;">d　　删除某个分区</span></li>
<li><span style="font-size: 12px;">l　　列出所有可用的分区类型</span></li>
<li><span style="font-size: 12px;">t　　改变某个分区的类型</span></li>
<li><span style="font-size: 12px;">p　　查看分区信息</span></li>
<li><span style="font-size: 12px;">w　　保存并退出</span></li>
<li><span style="font-size: 12px;">q　　不保存直接退出</span></li>
</ul>
<p><img src="https://img2020.cnblogs.com/blog/741594/202011/741594-20201101235311064-1594543832.png" alt="" width="502" height="421" loading="lazy" /></p>
<p>&nbsp;<span class="cnblogs_code">file /dev/sdb1</span>&nbsp;查看文件的属性&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">partprobe</span>&nbsp;如果查询不到刚刚分区的文件，则使用此命令 手动将分区信息同步到内核（一般执行两次效果会好些）</p>
<p>&nbsp;<span class="cnblogs_code">mkfs.xfs /dev/sdb1</span>&nbsp;将分区格式化为xfs的文件系统</p>
<p>&nbsp;<span class="cnblogs_code">df -h</span>&nbsp;查看挂载状态和硬盘使用量信息</p>
<p>&nbsp;<span class="cnblogs_code">du -sh /backup/</span>&nbsp;查看文件占用的空间&nbsp;</p>
<p>&nbsp;</p>
<p>③SWAP 交换分区</p>
<p>SWAP（交换）分区是一种通过在硬盘中预先划分一定的空间，然后将内存中暂时不常用的数据临时存在到硬盘中，以便腾出物理内存空间让更活跃的持续服务来使用的技术，其设计目的为了解决真实物理内存不足的问题。（交换分区大小一般建议设置为真实物理内存的1.5 ~ 2倍）</p>
<p>&nbsp;<span class="cnblogs_code">fdisk /dev/sdb</span>&nbsp;创建分区</p>
<p>&nbsp;<span class="cnblogs_code">mkswap /dev/sdb2</span>&nbsp;使用SWAP专用的格式化命令对分区格式化</p>
<p>&nbsp;<span class="cnblogs_code">swapon /dev/sdb2</span>&nbsp;将swap分区设备正式挂载到系统中</p>
<p>永久挂载：<img src="https://img2020.cnblogs.com/blog/741594/202011/741594-20201102224343272-1749979087.png" alt="" loading="lazy" /></p>
<p>&nbsp;</p>
<p><strong>3，磁盘容量配额</strong></p>
<p>限制用户使用文件的容量</p>
<p>①先需要检测是否支持quota技术，不支持则需要&nbsp;<span class="cnblogs_code">vim /etc/fstab</span>&nbsp;,然后重启系统</p>
<p>&nbsp;<img src="https://img2020.cnblogs.com/blog/741594/202011/741594-20201102230216414-177463573.png" alt="" width="654" height="176" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;②正对tom用户，硬盘使用量的软限制和硬限制分别为3MB和6MB；创建文件数量的软限制和硬限制为3个和6个</p>
<ul>
<li><span style="font-size: 12px;">软限制：当达到软件限制时会提示用户，但扔允许用户在限定的额度内继续使用</span></li>
<li><span style="font-size: 12px;">硬限制：当达到硬限制时会提示用户，且强制终止用户的操作</span></li>
</ul>
<p>&nbsp;<span class="cnblogs_code">xfs_quota -x -c <span style="color: #800000;">'</span><span style="color: #800000;">limit bsoft=3m bhard=6m isoft=3 ihard=6 tom</span><span style="color: #800000;">'</span> /boot</span>&nbsp;</p>
<p>③查询用户使用的量&nbsp;<span class="cnblogs_code">xfs_quota -x -c report /boot/</span>&nbsp;</p>
<ul>
<li><span style="font-size: 12px;">-c 参数用于以参数的形式设置要执行的命令</span></li>
<li><span style="font-size: 12px;">-x 参数是专家模式，让运维人员对quota服务进行更多复杂的配置</span></li>
</ul>
<p>④&nbsp;<span class="cnblogs_code">edquota -u tom</span>&nbsp;编辑用户quota配额限制</p>
<ul>
<li><span style="font-size: 12px;">-u 参数表示正对哪个用户</span></li>
<li><span style="font-size: 12px;">-g 参数表示正对哪个用户组</span></li>
</ul>
<p><img src="https://img2020.cnblogs.com/blog/741594/202011/741594-20201102231125287-1688336499.png" alt="" width="432" height="42" loading="lazy" /></p>
<p>&nbsp;</p>
<p><strong>4，软件方式链接</strong></p>
<ul>
<li><span style="font-size: 12px;">硬链接：硬链接文件与原始文件其实是同一个文件，只是名字不同，我们每添加一个硬链接，该文件的inode连接数会增加1；而且只有当该文件的inode连接数为0的时候，才算彻底删除。</span></li>
<li><span style="font-size: 12px;">软连接（符号连接）：类似于快捷方式</span></li>
</ul>
<p>ln 命令</p>
<ul>
<li><span style="font-size: 12px;">-s 创建&ldquo;符号链接&rdquo;（如果不带-s参数，则默认创建硬链接）</span></li>
<li><span style="font-size: 12px;">-f 强制创建文件或目录的链接</span></li>
<li><span style="font-size: 12px;">-i 覆盖前先询问</span></li>
<li><span style="font-size: 12px;">-v 显示创建链接的过程</span></li>
</ul>
<p>&nbsp;<span class="cnblogs_code">ln -s readme.txt readit.txt</span>&nbsp;创建一个软连接</p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: rgba(22, 159, 230, 1);"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a7"></a>七、RAID与LVM磁盘阵列技术</span></strong></span></p>
<p>RAID0：数据分散存储，提高整体存取性能，至少2块硬盘，只要有一块损坏，则不可用</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202011/741594-20201103000311440-566333089.png" alt="" width="78" height="116" loading="lazy" /></p>
<p>RAID1：数据备份存储，提高数据数据读取性能，成本高，安全性与可用性好，一块损坏，自动切换到另一块</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202011/741594-20201103000323468-1148777874.png" alt="" width="90" height="79" loading="lazy" /></p>
<p>RAID10：RAID0+RAID1</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202011/741594-20201103000342002-1261299219.png" alt="" width="122" height="125" loading="lazy" /></p>
<p><strong>1，创建RAID10+备份盘（需要5块硬盘）</strong></p>
<p>①虚拟机创建5块硬盘</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202011/741594-20201103000640393-1066482102.png" alt="" width="118" height="80" loading="lazy" /></p>
<p>&nbsp;</p>
<p>②mdadm 创建和管理软件RAID磁盘阵列</p>
<ul>
<li><span style="font-size: 12px;">-a　　检测设备名称</span></li>
<li><span style="font-size: 12px;">-n　　指定设备数量</span></li>
<li><span style="font-size: 12px;">-l　　指定RAID级别</span></li>
<li><span style="font-size: 12px;">-C　　创建</span></li>
<li><span style="font-size: 12px;">-v　　显示过程</span></li>
<li><span style="font-size: 12px;">-f　　模拟设备损坏</span></li>
<li><span style="font-size: 12px;">-r　　移除设备</span></li>
<li><span style="font-size: 12px;">-Q　　查看摘要信息</span></li>
<li><span style="font-size: 12px;">-D　　查看详细详细</span></li>
<li><span style="font-size: 12px;">-S　　停止RAID磁盘阵列</span></li>
</ul>
<p>&nbsp;<span class="cnblogs_code">mdadm -Cv /dev/md0 -a yes -n <span style="color: #800080;">4</span> -l <span style="color: #800080;">10</span> -x <span style="color: #800080;">1</span> /dev/sdc /dev/sdd /dev/sde /dev/sdf /dev/sdg</span>&nbsp;创建一个/dev/md0的磁盘阵列</p>
<ul>
<li><span style="font-size: 12px;">-a yes ：代表自动创建设备文件</span></li>
<li><span style="font-size: 12px;">-n 4：代表使用4块硬盘来部署这个RAID磁盘阵列</span></li>
<li><span style="font-size: 12px;">-l 10：代表RAID10方案</span></li>
<li><span style="font-size: 12px;">-x 1：代表使用一块备份盘</span></li>
<li><span style="font-size: 12px;">后面的表述5块硬盘</span></li>
</ul>
<p><span class="cnblogs_code">mkfs.ext4 /dev/md0</span>&nbsp;格式化为ext4&nbsp;</p>
<p><span class="cnblogs_code">mount /dev/md0 /RAID/</span>&nbsp;挂载硬盘设备。&nbsp;<span class="cnblogs_code">df -h</span>&nbsp;查询可用空间</p>
<p><span class="cnblogs_code">echo <span style="color: #800000;">"</span><span style="color: #800000;">/dev/md0 /RAID ext4 defaults 0 0</span><span style="color: #800000;">"</span> &gt;&gt; /etc/fstab</span>&nbsp;永久挂载</p>
<p><span class="cnblogs_code">mdadm /dev/md0 -f /dev/sdd</span>&nbsp;移除硬盘</p>
<p>重启系统</p>
<p><span class="cnblogs_code">mdadm /dev/md0 -a /dev/sdd</span>&nbsp;添加硬盘</p>
<p>&nbsp;</p>
<p><strong>2，LVM（逻辑卷管理器）</strong></p>
<p>实现硬盘分区动态扩容缩容技术</p>
<table style="height: 200px; width: 853px;" border="0"><caption>常用的LVM部署命令</caption>
<tbody>
<tr style="background-color: #918783;">
<td>功能/命令</td>
<td>物理卷管理</td>
<td>卷组管理</td>
<td>逻辑卷管理</td>
</tr>
<tr>
<td>扫描</td>
<td>pvscan</td>
<td>vgscan</td>
<td>lvscan</td>
</tr>
<tr>
<td>建立</td>
<td>pvcreate</td>
<td>vgcreate</td>
<td>lvcreate</td>
</tr>
<tr>
<td>显示</td>
<td>pvdisplay</td>
<td>vgdisplay</td>
<td>lvdisplay</td>
</tr>
<tr>
<td>删除</td>
<td>pvremove</td>
<td>vgremove</td>
<td>lvremove</td>
</tr>
<tr>
<td>扩容</td>
<td>&nbsp;</td>
<td>vgextend</td>
<td>lvextend</td>
</tr>
<tr>
<td>缩小</td>
<td>&nbsp;</td>
<td>vgreduce</td>
<td>lvreduce</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202011/741594-20201103233228641-1848163506.png" alt="" width="416" height="226" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>个人理解：把多个物理卷（支持LVM技术的硬盘）抽象成一个卷组（vg），可以通过卷组分配出逻辑卷（lv）挂载使用</p>
<p>&nbsp;①部署逻辑卷</p>
<p>&nbsp;<span class="cnblogs_code">pvcreate /dev/sdh /dev/sdi</span>&nbsp;第一步，让两块硬盘支持lvm技术</p>
<p>&nbsp;<span class="cnblogs_code">vgcreate storage /dev/sdh /dev/sdi</span>&nbsp;第二步，将两块硬盘设备加入storege卷组</p>
<p>&nbsp;<span class="cnblogs_code">lvcreate -n vo -l <span style="color: #800080;">37</span> storage</span>&nbsp;第三步，切割出一个约150MB的逻辑卷</p>
<ul>
<li><span style="font-size: 12px;">-L 150M ：生成一个大小为150M的逻辑卷</span></li>
<li><span style="font-size: 12px;">-l 37：生成一个大小为37*4MB=148MB的逻辑卷（每个基本单元默认是4MB）</span></li>
<li><span style="font-size: 12px;">-n vo：逻辑卷的名字为vo</span></li>
</ul>
<p>&nbsp;<span class="cnblogs_code">mkfs.ext4 /dev/storage/vo</span>&nbsp;第四步，格式化</p>
<p>&nbsp;<span class="cnblogs_code">mount /dev/storage/vo /vo</span>&nbsp;第五步，挂载</p>
<p>&nbsp;<span class="cnblogs_code">echo <span style="color: #800000;">"</span><span style="color: #800000;">/dev/storage/vo /vo ext4 defaults 0 0</span><span style="color: #800000;">"</span> &gt;&gt; /etc/fstab</span>&nbsp;第六步，永久挂载</p>
<p>&nbsp;②扩容逻辑卷（注意顺序）</p>
<p>&nbsp;<span class="cnblogs_code">umount /vo</span>&nbsp;扩展前先卸载设备和挂载点的关联</p>
<p>&nbsp;<span class="cnblogs_code">lvextend -L 290M /dev/storage/vo</span>&nbsp;扩容至290M</p>
<p>&nbsp;<span class="cnblogs_code">e2fsck -f /dev/storage/vo</span>&nbsp;检测硬盘完整性，并重置硬盘容量</p>
<p>&nbsp;<span class="cnblogs_code">mount -a</span>&nbsp;重新挂载</p>
<p>&nbsp;③缩小逻辑卷（注意顺序）</p>
<p>&nbsp;<span class="cnblogs_code">umount /vo</span>&nbsp;缩小前先卸载设备和挂载点的关联</p>
<p>&nbsp;<span class="cnblogs_code">e2fsck -f /dev/storage/vo</span>&nbsp;检测硬盘完整性，并重置硬盘容量</p>
<p>&nbsp;<span class="cnblogs_code">resize2fs /dev/storage/vo 120M</span>&nbsp;把逻辑卷vo的容量减小到120M</p>
<p>&nbsp;<span class="cnblogs_code">mount -a</span>&nbsp;重新挂载</p>
<p>&nbsp;④逻辑卷快照</p>
<p>LVM的快照卷功能有两个特点</p>
<ul>
<li><span style="font-size: 12px;">快照卷的容量必须等同于逻辑卷的容量</span></li>
<li><span style="font-size: 12px;">快照卷仅使用一次，一旦执行还原操作后则会被立即自动删除</span></li>
</ul>
<p>&nbsp;<span class="cnblogs_code">lvcreate -L 120M -s -n SNAP /dev/storage/vo</span>&nbsp;创建一个逻辑卷快照SNAP</p>
<ul>
<li><span style="font-size: 12px;">-s ：参数生成一个快照</span></li>
</ul>
<p>&nbsp;<span class="cnblogs_code">umount /vo/</span>&nbsp;合并快照前先卸载设备和挂载点的关联</p>
<p>&nbsp;<span class="cnblogs_code">lvconvert --merge /dev/storage/SNAP</span>&nbsp;合并快照</p>
<p>&nbsp;<span class="cnblogs_code">mount -a</span>&nbsp;重新挂载</p>
<p>&nbsp;⑤删除逻辑卷</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202011/741594-20201104001105487-733887915.png" alt="" width="459" height="146" loading="lazy" /></p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: rgba(22, 159, 230, 1);"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a8"></a>八、iptables与firewalld防火墙</span></strong></span></p>
<p><strong>1，iptables</strong></p>
<p>防火墙策略的匹配规则从上到下，如果没有匹配到所有的规则，则只需默认的动作</p>
<p>①规则链分类</p>
<ul>
<li><span style="font-size: 12px;">在进行路由选择前处理数据包（PREROUTING）</span></li>
<li><span style="font-size: 12px;">处理流入的数据包（INPUT）。一般使用最多</span></li>
<li><span style="font-size: 12px;">处理流出的数据包（OUTPUT）</span></li>
<li><span style="font-size: 12px;">处理转发的数据包（FORWARD）</span></li>
<li><span style="font-size: 12px;">在进行路由选择后处理数据包（POSTROUTING）</span></li>
</ul>
<p>②处理动作</p>
<ul>
<li><span style="font-size: 12px;">ACCEPT（允许流量通过）</span></li>
<li><span style="font-size: 12px;">REJECT（拒绝流量通过）。在拒绝流量后回复一条&ldquo;您的信息已收到，但是被扔掉了&rdquo;信息，从而让流量发送方清晰地看到数据被拒绝的响应信息</span></li>
<li><span style="font-size: 12px;">LOG（记录日志信息）</span></li>
<li><span style="font-size: 12px;">DROP（拒绝流量通过）。直接将流量丢弃而且不响应</span></li>
</ul>
<p>③iptable参数</p>
<ul>
<li><span style="font-size: 12px;">-p　　设置默认策略</span></li>
<li><span style="font-size: 12px;">-F　　清空规则链</span></li>
<li><span style="font-size: 12px;">-L　　查看规则链</span></li>
<li><span style="font-size: 12px;">-A　　在规则链的末尾加入新规则</span></li>
<li><span style="font-size: 12px;">-I num　　在规则链的头部加入新规则</span></li>
<li><span style="font-size: 12px;">-D num　　删除某一条规则</span></li>
<li><span style="font-size: 12px;">-s　　匹配来源地址IP/MASK，加叹号&ldquo;!&rdquo; 表示除这个ip外</span></li>
<li><span style="font-size: 12px;">-d　　匹配目标地址</span></li>
<li><span style="font-size: 12px;">-i 网卡名称　　匹配从这块网卡流入的数据</span></li>
<li><span style="font-size: 12px;">-o 网卡名称　　匹配从这块网卡流出的数据</span></li>
<li><span style="font-size: 12px;">-p　　匹配协议，如TCP、UDP、ICMP</span></li>
<li><span style="font-size: 12px;">--dport num　　匹配目标端口号</span></li>
<li><span style="font-size: 12px;">--sport unm　　匹配来源端口号</span></li>
</ul>
<p>&nbsp;<span class="cnblogs_code">iptables -L</span>&nbsp;查看已有的防火墙规则链</p>
<p>&nbsp;<span class="cnblogs_code">iptables -F</span>&nbsp;清空已有的防火墙规则链</p>
<p>&nbsp;<span class="cnblogs_code">iptables -P INPUT DROP</span>&nbsp;把INPUT的规则链默认策略设置为拒绝</p>
<p>&nbsp;<span class="cnblogs_code">iptables -I INPUT -p icmp -j DROP</span>&nbsp;对方始终ping不通</p>
<p>&nbsp;<span class="cnblogs_code">iptables -D INPUT <span style="color: #800080;">1</span></span>&nbsp;删除INPUT的第一条命令</p>
<p>允许指定网段的主机访问本机22端口：</p>
<p>&nbsp;<span class="cnblogs_code">iptables -I INPUT -s <span style="color: #800080;">192.168</span>.<span style="color: #800080;">0.0</span>/<span style="color: #800080;">24</span> -p tcp --dport <span style="color: #800080;">22</span> -j ACCEPT</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">iptables -A INPUT -p tcp --dport <span style="color: #800080;">22</span> -j REJECT</span>&nbsp;</p>
<p>向INPUT规则链中添加拒绝所有人访问本机12345端口：</p>
<p>&nbsp;<span class="cnblogs_code">iptables -A INPUT -p tcp --dport <span style="color: #800080;">22</span> -j REJECT</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">iptables -I INPUT -p udp --dport <span style="color: #800080;">12345</span> -j REJECT</span>&nbsp;</p>
<p>向INPUT规则链中添加拒绝192.168.10.5主机访问本机80端口（web服务）的策略规则：</p>
<p>&nbsp;<span class="cnblogs_code">iptables -I INPUT -p tcp -s <span style="color: #800080;">192.168</span>.<span style="color: #800080;">10.5</span> --dport <span style="color: #800080;">80</span> -j REJECT</span>&nbsp;</p>
<p>向INPUT规则链添加拒绝所有主机访问本机1000~1024端口策略：</p>
<p>&nbsp;<span class="cnblogs_code">iptables -A INPUT -p tcp --dport <span style="color: #800080;">1000</span>:<span style="color: #800080;">1024</span> -j REJECT</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">iptables -A INPUT -p udp --dport <span style="color: #800080;">1000</span>:<span style="color: #800080;">1024</span> -j REJECT</span>&nbsp;</p>
<p>&nbsp;使配置永久生效（默认重启恢复默认配置）：</p>
<p>&nbsp;<span class="cnblogs_code">service iptables save</span>&nbsp;</p>
<p>&nbsp;</p>
<p><strong>2，firewalld</strong></p>
<p>&nbsp;</p>
<table style="height: 409px; width: 937px;" border="0"><caption>firewalld中常用的区域名称及策略规则</caption>
<tbody>
<tr style="background-color: #797371;">
<td>区域</td>
<td>默认策略规则</td>
</tr>
<tr>
<td>trusted</td>
<td>允许所有的数据包</td>
</tr>
<tr>
<td>home</td>
<td>拒绝流入的流量，除非与流出的流量相关；而如果流量与ssh、mdns、ipp-client、amda-client与dhcpv6-client服务相关，则允许流量</td>
</tr>
<tr>
<td>internal</td>
<td>等同于home区域</td>
</tr>
<tr>
<td>work</td>
<td>拒绝流入的流量，除非与流出的流量相关；而如果流量与ssh、ipp-client与dhcpv6-client服务相关，则允许流量</td>
</tr>
<tr>
<td>public</td>
<td>拒绝流入的流量，除非与流出的流量相关；而如果流量与ssh、dhcpv6-client服务相关，则允许流量</td>
</tr>
<tr>
<td>external</td>
<td>拒绝流入的流量，除非与流出的流量相关；而如果流量与ssh服务相关，则允许流量</td>
</tr>
<tr>
<td>dmz</td>
<td>拒绝流入的流量，除非与流出的流量相关；而如果流量与ssh服务相关，则允许流量</td>
</tr>
<tr>
<td>block</td>
<td>拒绝流入的流量，除非与流出的流量相关</td>
</tr>
<tr>
<td>drop</td>
<td>拒绝流入的流量，除非与流出的流量相关</td>
</tr>
</tbody>
</table>
<table style="height: 503px; width: 935px;" border="0"><caption>firewall-cmd命令中使用的参数以及作用</caption>
<tbody>
<tr style="background-color: #8c8887;">
<td>参数</td>
<td>作用</td>
</tr>
<tr>
<td>--get-default-zone</td>
<td>查询默认的区域名称</td>
</tr>
<tr>
<td>--set-default-zone=&lt;区域名称&gt;</td>
<td>设置默认的区域，使其永久生效</td>
</tr>
<tr>
<td>--get-zones</td>
<td>显示可用的区域</td>
</tr>
<tr>
<td>--get-services</td>
<td>显示预先定义的服务</td>
</tr>
<tr>
<td>--add-active-zones</td>
<td>显示当前正在使用的区域与网卡名</td>
</tr>
<tr>
<td>--add-source=</td>
<td>将源自此IP或子网的流量导向指定的区域</td>
</tr>
<tr>
<td>--remove-source=</td>
<td>不再将源自此IP或子网的流量导向指定的区域</td>
</tr>
<tr>
<td>--add-interface=&lt;网卡名称&gt;</td>
<td>将源自该网卡的所有流量都导向某个指定的区域</td>
</tr>
<tr>
<td>--change-interface=&lt;网卡名称&gt;</td>
<td>将某个网卡与区域进行关联</td>
</tr>
<tr>
<td>--list-all</td>
<td>显示当前区域的网卡配置参数、资源、端口以及服务等信息</td>
</tr>
<tr>
<td>--list-all-zones</td>
<td>显示所有区域的网卡配置参数、资源、端口以及服务等信息</td>
</tr>
<tr>
<td>--add-service=&lt;服务名&gt;</td>
<td>设置默认区域允许该服务的流量</td>
</tr>
<tr>
<td>--add-port=&lt;端口号/协议&gt;</td>
<td>设置默认区域允许该端口的流量</td>
</tr>
<tr>
<td>--remove-service=&lt;服务名&gt;</td>
<td>设置默认区域不再允许该服务的流量</td>
</tr>
<tr>
<td>--remove-port=&lt;端口号/协议&gt;</td>
<td>设置默认区域不再允许该端口的流量</td>
</tr>
<tr>
<td>--reload</td>
<td>让&ldquo;永久生效&rdquo;的配置规则立即生效，并覆盖当前的配置规则</td>
</tr>
<tr>
<td>--panic-on</td>
<td>开启应急状况模式</td>
</tr>
<tr>
<td>--panic-off</td>
<td>关闭应急状况模式</td>
</tr>
</tbody>
</table>
<p>firewalld配置的防火墙模式为运行时（Runtime）模式，又称为当前生效模式，而且随着系统的重启会失效。如果让配置一直存在，就需要使用永久模式（firawall-cmd 后面加上 --permanent参数）</p>
<p>①查看firewalld服务当前所使用的区域：</p>
<p>&nbsp;<span class="cnblogs_code">firewall-cmd --<span style="color: #0000ff;">get</span>-<span style="color: #0000ff;">default</span>-zone</span>&nbsp;</p>
<p>②查看ens32网卡在firewalld服务中的区域：</p>
<p>&nbsp;<span class="cnblogs_code">firewall-cmd --<span style="color: #0000ff;">get</span>-zone-of-<span style="color: #0000ff;">interface</span>=ens32</span>&nbsp;</p>
<p>③把firewalld服务中的ens32网卡默认区域修改为external，并查看</p>
<p>&nbsp;<span class="cnblogs_code">firewall-cmd --permanent --zone=external --change-<span style="color: #0000ff;">interface</span>=ens32</span>&nbsp;设置</p>
<p>&nbsp;<span class="cnblogs_code">firewall-cmd --<span style="color: #0000ff;">get</span>-zone-of-<span style="color: #0000ff;">interface</span>=ens32</span>&nbsp;查看</p>
<p>④把firewalld服务的当前默认区域设置为public</p>
<p>&nbsp;<span class="cnblogs_code">firewall-cmd --<span style="color: #0000ff;">set</span>-<span style="color: #0000ff;">default</span>-zone=<span style="color: #0000ff;">public</span></span>&nbsp;设置</p>
<p>&nbsp;<span class="cnblogs_code">firewall-cmd --<span style="color: #0000ff;">get</span>-<span style="color: #0000ff;">default</span>-zone</span>&nbsp;查看</p>
<p>⑤启动/关闭防火墙服务的应急状况模式，阻断一些网络连接（当远程控制服务器时慎用）</p>
<p>&nbsp;<span class="cnblogs_code">firewall-cmd --panic-on</span>&nbsp;连接都不可访问</p>
<p>&nbsp;<span class="cnblogs_code">firewall-cmd --panic-off </span>&nbsp;</p>
<p>⑥查询public区域是否允许请求SSH和HTTPS协议的流量</p>
<p>&nbsp;<span class="cnblogs_code">firewall-cmd --zone=<span style="color: #0000ff;">public</span> --query-service=ssh</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">firewall-cmd --zone=<span style="color: #0000ff;">public</span> --query-service=https</span>&nbsp;</p>
<p>⑦把firewalld服务中请求HTTPS协议的流量设置为永久允许，并立即生效</p>
<p>&nbsp;<span class="cnblogs_code">firewall-cmd --zone=<span style="color: #0000ff;">public</span> --add-service=https</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">firewall-cmd --permanent --zone=<span style="color: #0000ff;">public</span> --add-service=https</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">firewall-cmd --reload</span>&nbsp;</p>
<p>⑧把firewalld服务中请求的http协议的流量设置为永久拒绝，并立即生效</p>
<p>&nbsp;<span class="cnblogs_code">firewall-cmd --permanent --zone=<span style="color: #0000ff;">public</span> --remove-service=http</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">firewall-cmd --reload</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">firewall-cmd --zone=<span style="color: #0000ff;">public</span> --query-service=http</span>&nbsp;</p>
<p>⑨把在firewalld服务中访问8080和8081端口的流量策略设置为允许，但仅当前生效</p>
<p>&nbsp;<span class="cnblogs_code">firewall-cmd --zone=<span style="color: #0000ff;">public</span> --add-port=<span style="color: #800080;">8080</span>-<span style="color: #800080;">8081</span>/tcp</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">firewall-cmd --zone=<span style="color: #0000ff;">public</span> --list-ports</span>&nbsp;</p>
<p>⑩把原本访问本机888端口的流量转发到22端口，而且要求当前和长期有效</p>
<p>&nbsp;<span class="cnblogs_code">firewall-cmd --permanent --zone=<span style="color: #0000ff;">public</span> --add-forward-port=port=<span style="color: #800080;">888</span>:proto=tcp:toport=<span style="color: #800080;">22</span>:toaddr=<span style="color: #800080;">192.168</span>.<span style="color: #800080;">0.140</span></span>&nbsp;&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">ssh -p <span style="color: #800080;">888</span> <span style="color: #800080;">192.168</span>.<span style="color: #800080;">0.140</span></span>&nbsp;在客户端使用ssh命令尝试访问192.168.0.140主机的888端口</p>
<p>⑫拒绝192.168.0.0/24网段的所有用户访问本机的ssh服务</p>
<div class="cnblogs_code">
<pre>firewall-cmd --permanent --zone=<span style="color: #0000ff;">public</span> --add-rich-rule=<span style="color: #800000;">"</span><span style="color: #800000;">rule family=</span><span style="color: #800000;">"</span>ipv4<span style="color: #800000;">"</span><span style="color: #800000;"> source address=</span><span style="color: #800000;">"</span><span style="color: #800080;">192.168</span>.<span style="color: #800080;">0.0</span>/<span style="color: #800080;">24</span><span style="color: #800000;">"</span><span style="color: #800000;"> service name=</span><span style="color: #800000;">"</span>ssh<span style="color: #800000;">"</span><span style="color: #800000;"> reject</span><span style="color: #800000;">"</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: rgba(22, 159, 230, 1);"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a9"></a>九、使用ssh服务管理远程主机</span></strong></span></p>
<p><strong>1，配置网络服务</strong></p>
<p>①使用nmtui进行图形化配置。&nbsp;<span class="cnblogs_code">vim /etc/sysconfig/network-scripts/ifcfg-ens32</span>&nbsp;将NOBOOT=yes重启后激活网卡</p>
<p>②nmcli查看网络信息或网络状态</p>
<p>&nbsp;<span class="cnblogs_code">nmcli connection show</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">nmcli con show ens32</span>&nbsp;</p>
<p><strong>2，管理sshd服务</strong></p>
<p>①&nbsp;<span class="cnblogs_code">vim /etc/ssh/sshd_config</span>&nbsp;ssh配置信息</p>
<table style="height: 459px; width: 916px;" border="0"><caption>sshd服务配置文件中包含的参数以及作用</caption>
<tbody>
<tr style="background-color: #979290;">
<td>参数</td>
<td>作用</td>
</tr>
<tr>
<td>Port 22</td>
<td>默认的sshd服务端口</td>
</tr>
<tr>
<td>ListenAddress 0.0.0.0</td>
<td>设定sshd服务监听的IP地址</td>
</tr>
<tr>
<td>Protocol 2</td>
<td>SSH协议的版本号</td>
</tr>
<tr>
<td>HostKey /etc/ssh/ssh_host_key</td>
<td>SSH协议版本为1时，DES私钥存放的位置</td>
</tr>
<tr>
<td>HostKey /etc/ssh/ssh_host_ecdsa_key</td>
<td>SSH协议版本为2时，RSA私钥存放的位置</td>
</tr>
<tr>
<td>HostKey /etc/ssh/ssh_host_ed25519_key</td>
<td>SSH协议版本为2时，DSA私钥存放的位置</td>
</tr>
<tr>
<td>PermitRootLogin Yes</td>
<td>设定是否允许root管理员直接登录</td>
</tr>
<tr>
<td>StrictModes yes&nbsp;</td>
<td>当远程用户的私钥改变时直接拒绝连接&nbsp;</td>
</tr>
<tr>
<td>MaxSesstuins 6&nbsp;</td>
<td>最大密码尝试次数&nbsp;</td>
</tr>
<tr>
<td>MaxSessions 10&nbsp;</td>
<td>最大终端数&nbsp;</td>
</tr>
<tr>
<td>PasswordAuthentication yes&nbsp;</td>
<td>是否允许密码验证</td>
</tr>
<tr>
<td>PermitEmptyPasswords no&nbsp;</td>
<td>是否允许空密码登录（很不安全）&nbsp;</td>
</tr>
</tbody>
</table>
<p>②&nbsp;<span class="cnblogs_code">ssh <span style="color: #800080;">192.168</span>.<span style="color: #800080;">0.140</span></span>&nbsp;远程连接</p>
<p>③禁止root管理员远程登录</p>
<p>&nbsp;<span class="cnblogs_code">vim /etc/ssh/sshd_config </span>&nbsp;编辑</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202011/741594-20201109224119518-1712828530.png" alt="" width="176" height="74" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">systemctl restart sshd</span>&nbsp;重启服务</p>
<p>&nbsp;<span class="cnblogs_code">systemctl enable sshd</span>&nbsp;开机启动&nbsp;</p>
<p>④安全密钥验证</p>
<p>&nbsp;<span class="cnblogs_code">ssh-keygen</span>&nbsp;在客户端主机中生成密钥</p>
<p>&nbsp;<span class="cnblogs_code">ssh-copy-id <span style="color: #800080;">192.168</span>.<span style="color: #800080;">0.140</span></span>&nbsp;吧客户端主机生成的公钥文件传送至远程主机</p>
<p>只允许密钥验证：<img src="https://img2020.cnblogs.com/blog/741594/202011/741594-20201109225430748-415802957.png" alt="" loading="lazy" /></p>
<p><span class="cnblogs_code">systemctl restart sshd</span>&nbsp;重启服务</p>
<p>⑤远程传输命令</p>
<p>scp是一个基于SSH协议在网络之间进行安全传输的命令，会对数据进行加密传输</p>
<ul>
<li><span style="font-size: 12px;">-v　　显示详细的连接进度</span></li>
<li><span style="font-size: 12px;">-p　　指定远程主机的sshd端口号</span></li>
<li><span style="font-size: 12px;">-r　　用于传输文件夹</span></li>
<li><span style="font-size: 12px;">-6　　使用ipv6协议</span></li>
<li><span style="font-size: 12px;">如果要传送整个文件夹内所有的数据，还需要额外添加参数-r进行递归操作</span></li>
</ul>
<p>&nbsp;<span class="cnblogs_code">scp /root/readme.txt <span style="color: #800080;">192.168</span>.<span style="color: #800080;">0.140</span>:/root</span>&nbsp;将文件传输到远程主机</p>
<p>&nbsp;<span class="cnblogs_code">scp <span style="color: #800080;">192.168</span>.<span style="color: #800080;">0.140</span>:/root/readme.txt /root/</span>&nbsp;将远程主机的文件下载到本地主机</p>
<p><strong>&nbsp;3，不间断会话服务</strong></p>
<p>&nbsp;<span class="cnblogs_code">yum install screen</span>&nbsp;screen是一个能够实现多窗口控制的开源服务程序</p>
<p>①管理远程会话</p>
<p>&nbsp;<span class="cnblogs_code">screen -S backup</span>&nbsp;创建一个名词为backup的会话窗口</p>
<p>&nbsp;<span class="cnblogs_code">screen -ls</span>&nbsp;显示当前已有的会话</p>
<p>&nbsp;<span class="cnblogs_code">exit</span>&nbsp;退出会话</p>
<p>&nbsp;<span class="cnblogs_code">screen -x backup</span>&nbsp;共享backup会话的窗口</p>
<p>&nbsp;<span class="cnblogs_code">screen -r liunx</span>&nbsp;恢复指定的会话</p>
<p>&nbsp;<span class="cnblogs_code">screen -wipe liunxprobe</span>&nbsp;删除无法使用的会话</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: rgba(22, 159, 230, 1);"><span style="color: #ffffff;"><strong><a name="a10"></a>十、使用Apache服务部署静态网站</strong></span></p>
<p><strong>&nbsp;1，安装httpd（Apache服务软件包）</strong></p>
<p>&nbsp;&nbsp;<span class="cnblogs_code">yum install httpd</span>&nbsp;安装</p>
<p>&nbsp;&nbsp;<span class="cnblogs_code">systemctl start httpd</span>&nbsp;启动服务</p>
<p>&nbsp;&nbsp;<span class="cnblogs_code">systemctl enable httpd</span>&nbsp;开机启动</p>
<table style="height: 81px; width: 777px;" border="0"><caption>Liunx系统中的配置文件</caption>
<tbody>
<tr style="background-color: #7f8080;">
<td>配置文件的名称</td>
<td>存放位置</td>
</tr>
<tr>
<td>服务目录</td>
<td>/etc/httpd</td>
</tr>
<tr>
<td>主配置目录</td>
<td>/etc/httpd/conf/httpd.conf</td>
</tr>
<tr>
<td>网站数据目录</td>
<td>/var/www/html</td>
</tr>
<tr>
<td>访问日志</td>
<td>/var/log/httpd/access_log</td>
</tr>
<tr>
<td>错误日志</td>
<td>/var/log/httpd/error_log</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<table style="height: 523px; width: 779px;" border="0"><caption>配置httpd服务程序时最常用的参数以及用途描述</caption>
<tbody>
<tr style="background-color: #827e7d;">
<td>参数</td>
<td>用途</td>
</tr>
<tr>
<td>ServerRoot</td>
<td>服务目录</td>
</tr>
<tr>
<td>ServerAdmin</td>
<td>管理员邮箱</td>
</tr>
<tr>
<td>User</td>
<td>运行服务的用户</td>
</tr>
<tr>
<td>Group</td>
<td>运行服务的用户组</td>
</tr>
<tr>
<td>ServerName</td>
<td>运行服务器的域名</td>
</tr>
<tr>
<td>DocumentRoot</td>
<td>网站数据目录</td>
</tr>
<tr>
<td>Directory</td>
<td>网站数据目录的权限</td>
</tr>
<tr>
<td>Listen</td>
<td>监听的IP地址与端口号</td>
</tr>
<tr>
<td>DirectoryIndex</td>
<td>默认的索引页页面</td>
</tr>
<tr>
<td>ErrorLog</td>
<td>错误日志文件</td>
</tr>
<tr>
<td>CustomLog</td>
<td>访问日志文件</td>
</tr>
<tr>
<td>Timeout</td>
<td>网页超时时间，默认为300秒</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">echo <span style="color: #800000;">"</span><span style="color: #800000;">Hello</span><span style="color: #800000;">"</span> &gt;&gt; /<span style="color: #0000ff;">var</span>/www/html/index.html</span>&nbsp;改变主页</p>
<p><strong>2，将网站数据的目录修改为/home/wwwroot目录</strong></p>
<p>&nbsp;<span class="cnblogs_code">mkdir /home/wwwroot</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">echo <span style="color: #800000;">"</span><span style="color: #800000;">hello</span><span style="color: #800000;">"</span> &gt;&gt; /home/wwwroot/index.html</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">vim /etc/httpd/conf/httpd.conf</span>&nbsp;修改httpd配置文件</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202011/741594-20201110232133772-1094838377.png" alt="" width="270" height="125" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;&nbsp;<span class="cnblogs_code">systemctl restart httpd</span>&nbsp;重启服务</p>
<p>&nbsp;&nbsp;<span class="cnblogs_code">setenforce <span style="color: #800080;">0</span></span>&nbsp;受SELinux影响，改变目录访问会失败，可以关闭SELinux（0：关闭 1：开启）。配置命令后立即生效</p>
<p>①SELiunx服务有三种配置模式</p>
<ul>
<li><span style="font-size: 12px;">enforcing：强制启用安全策略模式，将拦截服务的不合法请求</span></li>
<li><span style="font-size: 12px;">permissive：遇到服务越权访问时，只发出警告而不拦截</span></li>
<li><span style="font-size: 12px;">disabled：对于越权的行为不警告也不拦截</span></li>
</ul>
<p>&nbsp;<span class="cnblogs_code">getenforce</span>&nbsp;获取SELiunx服务的允许模式</p>
<p>&nbsp;</p>
<p>②查看原始网站数据的保存目录与当前网站数据的保存目录是否拥有不同的SELiunx安全上下文</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202011/741594-20201110234908734-825219756.png" alt="" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;文件上设置的SELiunx安全上下文是由用户段、角色段以及类型等多个信息项共同组成的</p>
<ul>
<li><span style="font-size: 12px;">用户段system_u代表系统进程的身份</span></li>
<li><span style="font-size: 12px;">角色段object_r代表文件目录的角色</span></li>
<li><span style="font-size: 12px;">类型段httpd_sys_content_t代表网络服务的系统文件</span></li>
</ul>
<p>③semanage命令用于管理SELiunx的策略</p>
<ul>
<li><span style="font-size: 12px;">-l　　参数用户查询</span></li>
<li><span style="font-size: 12px;">-a　　参数用于添加</span></li>
<li><span style="font-size: 12px;">-m　　参数用于修改</span></li>
<li><span style="font-size: 12px;">-d　　参数用于删除</span></li>
</ul>
<p>让这个目录以及里面的所有文件能够被httpd服务程序所访问到：</p>
<p>&nbsp;<span class="cnblogs_code">semanage fcontext -a -t httpd_sys_content_t /home/wwwroot</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">semanage fcontext -a -t httpd_sys_content_t /home/wwwroot<span style="color: #008000;">/*</span></span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">restorecon -Rv /home/wwwroot/</span>&nbsp;设置好的SELiunx安全上下文立即生效。-Rv对指定的目录进行递归操作</p>
<p>到现在为止，/home/wwwroot下面的index.html可以正常访问了</p>
<p>&nbsp;</p>
<p><strong>3，个人用户主页功能</strong></p>
<p>可以给每个用户创建一个独立的网站。最终使用&nbsp;<span class="cnblogs_code">http:<span style="color: #008000;">//</span><span style="color: #008000;">127.0.0.1/~hunter/</span></span>&nbsp;访问</p>
<p>①修改配置文件&nbsp;<span class="cnblogs_code">vim /etc/httpd/conf.d/userdir.conf</span>&nbsp;</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202011/741594-20201111230511192-445362542.png" alt="" width="160" height="83" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>②创建用户站点目录，并把用户目录权限改为755</p>
<p>&nbsp;<span class="cnblogs_code">su - hunter</span>&nbsp;&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">mkdir public_html/</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">chmod -Rf <span style="color: #800080;">755</span> /home/hunter/</span>&nbsp;递归修改目录和子目录</p>
<p>③重启httpd服务</p>
<p>&nbsp;<span class="cnblogs_code">systemctl restart httpd</span>&nbsp;</p>
<p>④修改SELiunx规则</p>
<p>&nbsp;<span class="cnblogs_code">getsebool -a | grep http</span>&nbsp;查询并过滤出http协议相关的安全策略</p>
<p>&nbsp;<span class="cnblogs_code">setsebool -P httpd_enable_homedirs=on</span>&nbsp;大写P参数 使规则永久生效</p>
<p>⑤给用户网页添加密码验证</p>
<p>&nbsp;<span class="cnblogs_code">htpasswd -c /etc/httpd/passwd hunter</span>&nbsp;给用户设置密码</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('c9b4e79d-750c-40f7-9800-a31d9345d06e')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_c9b4e79d-750c-40f7-9800-a31d9345d06e" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_c9b4e79d-750c-40f7-9800-a31d9345d06e" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_c9b4e79d-750c-40f7-9800-a31d9345d06e" class="cnblogs_code_hide">
<pre>&lt;Directory <span style="color: #800000;">"</span><span style="color: #800000;">/home/*/public_html</span><span style="color: #800000;">"</span>&gt;<span style="color: #000000;">
        AllowOverride all
        authuserfile </span><span style="color: #800000;">"</span><span style="color: #800000;">/etc/httpd/passwd</span><span style="color: #800000;">"</span><span style="color: #000000;">
        authname </span><span style="color: #800000;">"</span><span style="color: #800000;">My pervately website</span><span style="color: #800000;">"</span><span style="color: #000000;">
        authtype basic
        require user hunter
</span>&lt;/Directory&gt;</pre>
</div>
<span class="cnblogs_code_collapse">配置设置</span></div>
<p>&nbsp;<span class="cnblogs_code"> systemctl restart httpd</span>&nbsp;重启httpd服务</p>
<p>&nbsp;</p>
<p><strong>4，基于IP地址访问站点</strong></p>
<p>①创建目录，放置index.html页面</p>
<div class="cnblogs_code">
<pre>mkdir -p /home/wwwroot/<span style="color: #800080;">001</span><span style="color: #000000;">
mkdir </span>-p /home/wwwroot/<span style="color: #800080;">002</span><span style="color: #000000;">
mkdir </span>-p /home/wwwroot/<span style="color: #800080;">003</span><span style="color: #000000;">

echo </span><span style="color: #800000;">"</span><span style="color: #800000;">001</span><span style="color: #800000;">"</span> &gt;&gt; <span style="color: #800080;">001</span>/<span style="color: #000000;">index.html
echo </span><span style="color: #800000;">"</span><span style="color: #800000;">002</span><span style="color: #800000;">"</span> &gt; <span style="color: #800080;">002</span>/<span style="color: #000000;">index.html
echo </span><span style="color: #800000;">"</span><span style="color: #800000;">003</span><span style="color: #800000;">"</span> &gt; <span style="color: #800080;">003</span>/index.html</pre>
</div>
<p>②在httpd服务配置文件大约113行处加上如下配置</p>
<div class="cnblogs_code">
<pre>&lt;VirtualHost <span style="color: #800080;">192.168</span>.<span style="color: #800080;">0.140</span>&gt;<span style="color: #000000;">
DocumentRoot </span>/home/wwwroot/<span style="color: #800080;">001</span><span style="color: #000000;">
ServerName www.hunter.com
</span>&lt;Directory /home/wwwroot/<span style="color: #800080;">001</span> &gt;<span style="color: #000000;">
AllowOverride None
Require all granted
</span>&lt;/Directory&gt;
&lt;/VirtualHost&gt;

&lt;VirtualHost <span style="color: #800080;">192.168</span>.<span style="color: #800080;">0.141</span>&gt;<span style="color: #000000;">
DocumentRoot </span>/home/wwwroot/<span style="color: #800080;">002</span><span style="color: #000000;">
ServerName bbs.hunter.com
</span>&lt;Directory /home/wwwroot/<span style="color: #800080;">002</span> &gt;<span style="color: #000000;">
AllowOverride None
Require all granted
</span>&lt;/Directory&gt;
&lt;/VirtualHost&gt;

&lt;VirtualHost <span style="color: #800080;">192.168</span>.<span style="color: #800080;">0.142</span>&gt;<span style="color: #000000;">
DocumentRoot </span>/home/wwwroot/<span style="color: #800080;">003</span><span style="color: #000000;">
ServerName tech.hunter.com
</span>&lt;Directory /home/wwwroot/<span style="color: #800080;">003</span> &gt;<span style="color: #000000;">
AllowOverride None
Require all granted
</span>&lt;/Directory&gt;
&lt;/VirtualHost&gt;</pre>
</div>
<p>&nbsp;<span class="cnblogs_code">systemctl restart httpd</span>&nbsp;重启httpd服务</p>
<p>③设置SELinux安全上下文</p>
<div class="cnblogs_code">
<pre>semanage fcontext -a -t httpd_sys_content_t /home/<span style="color: #000000;">wwwroot
semanage fcontext </span>-a -t httpd_sys_content_t /home/wwwroot/<span style="color: #800080;">001</span><span style="color: #000000;">
semanage fcontext </span>-a -t httpd_sys_content_t /home/wwwroot/<span style="color: #800080;">001</span><span style="color: #008000;">/*</span><span style="color: #008000;">
semanage fcontext -a -t httpd_sys_content_t /home/wwwroot/002
semanage fcontext -a -t httpd_sys_content_t /home/wwwroot/002/*
semanage fcontext -a -t httpd_sys_content_t /home/wwwroot/003
semanage fcontext -a -t httpd_sys_content_t /home/wwwroot/003/*</span></pre>
</div>
<p>&nbsp;<span class="cnblogs_code"> restorecon -Rv /home/wwwroot/</span>&nbsp;设置好的SELiunx安全上下文立即生效。-Rv对指定的目录进行递归操作</p>
<p>&nbsp;</p>
<p><strong>5，基于主机域名访问站点</strong></p>
<p>①参考4所有的配置</p>
<p>②&nbsp;<span class="cnblogs_code">vim /etc/hosts</span>&nbsp;手动定义ip地址与域名之间的对应关系。保存生效，就可以使用域名访问了</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202011/741594-20201112000141638-867095921.png" alt="" loading="lazy" /></p>
<p><strong>6，基于端口号</strong></p>
<p>①参考4所有的配置</p>
<p>②需要修改&nbsp;<span class="cnblogs_code">vim /etc/httpd/conf/httpd.conf</span>&nbsp;</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202011/741594-20201112001200663-2069155263.png" alt="" width="184" height="68" loading="lazy" /></p>
<p>&nbsp;<img src="https://img2020.cnblogs.com/blog/741594/202011/741594-20201112001222716-1895138379.png" alt="" width="288" height="391" loading="lazy" /></p>
<p>&nbsp;③重新httpd&nbsp;<span class="cnblogs_code">systemctl restart httpd</span>&nbsp;</p>
<p>&nbsp;④配置SELinux。使用semanage命令查询并过滤所有与Http协议相关且SELiunx服务允许的端口列表</p>
<p>&nbsp;<span class="cnblogs_code">semanage port -l | grep http</span>&nbsp;查询SELiunx服务允许的端口列表</p>
<p>&nbsp;<span class="cnblogs_code">semanage port -a -t http_port_t -p tcp <span style="color: #800080;">6111</span></span>&nbsp;设置，立即生效</p>
<p>&nbsp;<span class="cnblogs_code">semanage port -a -t http_port_t -p tcp <span style="color: #800080;">6222</span></span>&nbsp;设置，立即生效</p>
<p>&nbsp;<span class="cnblogs_code">semanage port -a -t http_port_t -p tcp <span style="color: #800080;">6333</span></span>&nbsp;设置，立即生效</p>
<p>⑤重新httpd&nbsp;<span class="cnblogs_code">systemctl restart httpd&nbsp;</span></p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: rgba(22, 159, 230, 1);"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a11"></a>十一、使用vsftpd服务传输文件</span></strong></span></p>
<p>FTP是一种在互联网中进行文件传输得当协议，基于客户端/服务器模式，默认使用20、21号端口。20（数据端口）用于进行数据传输，21（命令端口）用于接收客户端发出的相关的FTP命令与参数</p>
<p>FTP协议有下面两种工作模式：</p>
<ul>
<li><span style="font-size: 12px;">主动模式：FTP服务器主动向客户端发起连接请求。</span></li>
<li><span style="font-size: 12px;">被动模式：FTP服务器等待客户端发起连接请求（FTP的默认工作模式）</span></li>
</ul>
<p><strong>vsftpd：</strong>vsftpd（very secure ftp daemon，非常安全的FTP守护进程）是一款允许在Liunx操作系统上的FTP服务程序，不仅完全开源而且免费，此外，还具有很高的安全性、传输速度，以及支持虚拟用户验证等其他FTP服务程序不具备的特点</p>
<p><strong>ftp：</strong>ftp是liunx系统中以命令行界面方式来管理FTP传输服务的客户端工具</p>
<p>&nbsp;<span class="cnblogs_code">yum install vsftpd</span>&nbsp;安装vsftpd</p>
<p>&nbsp;<span class="cnblogs_code">yum install ftp</span>&nbsp;安装ftp</p>
<table style="height: 613px; width: 938px;" border="0"><caption>vsftpd服务程序常用的参数以及作用</caption>
<tbody>
<tr style="background-color: #958a89;">
<td>参数</td>
<td>作用</td>
</tr>
<tr>
<td>listen=[YES|NO]</td>
<td>是否以独立运行的方式监听服务</td>
</tr>
<tr>
<td>listen_address=IP地址</td>
<td>设置要监听的IP地址</td>
</tr>
<tr>
<td>listen_port=21</td>
<td>设置FTP服务的监听端口</td>
</tr>
<tr>
<td>download_enable=[YES|NO]</td>
<td>是否允许下载文件</td>
</tr>
<tr>
<td>
<p>userlist_enable=[YES|NO]</p>
<p>userlist_deny=[YES|NO]</p>
</td>
<td>设置用户列表为&ldquo;允许&rdquo;还是&ldquo;禁止&rdquo;操作</td>
</tr>
<tr>
<td>max_clients=0</td>
<td>最大客户连接数，0为不限制</td>
</tr>
<tr>
<td>max_per_ip=0</td>
<td>同一IP地址的最大连接数，0为不限制</td>
</tr>
<tr>
<td>anonymous_enable=[YES|NO]</td>
<td>是否允许匿名用户访问</td>
</tr>
<tr>
<td>anon_upload_enable=[YEA|NO]</td>
<td>是否允许匿名用户上传文件</td>
</tr>
<tr>
<td>anon_umask=022</td>
<td>匿名用户上传的umask值</td>
</tr>
<tr>
<td>anon_root=/var/ftp</td>
<td>匿名用户的FTP跟目录</td>
</tr>
<tr>
<td>anon_mkdir_write_enable=[YES|NO]</td>
<td>是否允许匿名用户创建目录</td>
</tr>
<tr>
<td>anon_other_write_enable=[YES|NO]</td>
<td>是否开放匿名用户的其他写入权限（包括重命名、删除等操作）</td>
</tr>
<tr>
<td>anon_max_rate=0</td>
<td>匿名用户的最大传输速率（字节/秒），0为不限制</td>
</tr>
<tr>
<td>local_enable=[YES|NO]</td>
<td>是否允许本地用户登录FTP</td>
</tr>
<tr>
<td>local_umask=022</td>
<td>本地用户上传文件的umask值</td>
</tr>
<tr>
<td>local_root=/var/ftp</td>
<td>本地用户的FTP根目录</td>
</tr>
<tr>
<td>chroot_local_user=[YES|NO]</td>
<td>是否将用户权限禁锢在FTP目录，以确保安全</td>
</tr>
<tr>
<td>local_max_rate=0</td>
<td>本地用户最大传输速率（字节/秒），0为不限制</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<p>vsftpd作为更加安全的文件传输服务程序，允许用户以三种认证模式登陆到FTP服务器上</p>
<ul>
<li><span style="font-size: 12px;">匿名开放模式：是一种不安全的认证模式，任何人都可以无需密码验证而直接登录到FTP服务器</span></li>
<li><span style="font-size: 12px;">本地用户模式：是同步Liunx系统本地的账户摩玛信息进行认证的模式，相较于匿名开发模式更安全，而且配置起来也很简单。但是如果被黑客破解了账户的信息，就可以畅通无阻的登录FTP服务器，从而完全控制整台服务器</span></li>
<li><span style="font-size: 12px;">虚拟用户模式：是这三种模式中最安全的一种认证模式，它需要为FTP服务单独建立用户数据库文件，虚拟出用来进行口令验证的账户信息，而这些账户信息在服务器系统中实际上是不存在的，仅供FTP服务程序进行认证使用。这样，即使黑客破解了账户信息也无法登录服务器，从而有效降低了破坏范围和影响</span></li>
</ul>
<p><span style="color: #ff0000;"><strong>1，iptables防火墙管理工具默认禁止了FTP传输协议的端口号，清理iptables防火墙的默认策略，并把当前的策略保存起来</strong></span></p>
<p>&nbsp;<span class="cnblogs_code">iptables -F</span>&nbsp;清理策略</p>
<p>&nbsp;<span class="cnblogs_code">service iptables save</span>&nbsp;永久保存，防止开机重置</p>
<p>&nbsp;</p>
<p><strong>1，匿名开放模式</strong></p>
<table style="height: 225px; width: 838px;" border="0"><caption>可以向匿名用户开放的权限参数以及作用</caption>
<tbody>
<tr style="background-color: #a29c99;">
<td>参数</td>
<td>作用</td>
</tr>
<tr>
<td>anonymous_enable=YES</td>
<td>&nbsp;允许匿名访问模式</td>
</tr>
<tr>
<td>anon_umask=022</td>
<td>&nbsp;匿名用户上传文件的umask值</td>
</tr>
<tr>
<td>anon_upload_enable=YES</td>
<td>&nbsp;允许匿名用户上传文件</td>
</tr>
<tr>
<td>anon_mkdir_write_enable=YES&nbsp;</td>
<td>&nbsp;允许匿名用户创建目录</td>
</tr>
<tr>
<td>anon_other_write_enable=YES</td>
<td>允许匿名用户修改目录名称或删除目录</td>
</tr>
</tbody>
</table>
<p>①配置vsftpd.conf配置文件</p>
<p>&nbsp;<span class="cnblogs_code">mv /etc/vsftpd/vsftpd.conf /etc/vsftpd/vsftpd.conf_bak</span>&nbsp;备份</p>
<p>&nbsp;<span class="cnblogs_code">rep -v <span style="color: #800000;">"</span><span style="color: #800000;">#</span><span style="color: #800000;">"</span> /etc/vsftpd/vsftpd.conf_bak &gt; /etc/vsftpd/vsftpd.conf</span>&nbsp;将未注释的配置写入vsftpd.conf文件中</p>
<p>&nbsp;<span class="cnblogs_code"> vim /etc/vsftpd/vsftpd.conf</span>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('b41bb743-e054-4f13-be6e-680256413403')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_b41bb743-e054-4f13-be6e-680256413403" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_b41bb743-e054-4f13-be6e-680256413403" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_b41bb743-e054-4f13-be6e-680256413403" class="cnblogs_code_hide">
<pre>anonymous_enable=<span style="color: #000000;">YES
anon_umask</span>=<span style="color: #800080;">022</span><span style="color: #000000;">
anon_upload_enable</span>=<span style="color: #000000;">YES
anon_mkdir_write_enable</span>=<span style="color: #000000;">YES
anon_other_write_enable</span>=<span style="color: #000000;">YES
local_enable</span>=<span style="color: #000000;">YES
write_enable</span>=<span style="color: #000000;">YES
local_umask</span>=<span style="color: #800080;">022</span><span style="color: #000000;">
dirmessage_enable</span>=<span style="color: #000000;">YES
xferlog_enable</span>=<span style="color: #000000;">YES
connect_from_port_20</span>=<span style="color: #000000;">YES
xferlog_std_format</span>=<span style="color: #000000;">YES
listen</span>=<span style="color: #000000;">NO
listen_ipv6</span>=<span style="color: #000000;">YES
pam_service_name</span>=<span style="color: #000000;">vsftpd
userlist_enable</span>=<span style="color: #000000;">YES
tcp_wrappers</span>=YES</pre>
</div>
<span class="cnblogs_code_collapse">vsftpd.conf</span></div>
<p>②重启vsftpd服务</p>
<p>&nbsp;<span class="cnblogs_code">systemctl restart vsftpd</span>&nbsp;</p>
<p>③开启启动</p>
<p>&nbsp;<span class="cnblogs_code">systemctl enable vsftpd</span>&nbsp;</p>
<p>④ftp客户端连接（连接不上注意iptables）</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202011/741594-20201115013106215-1681245461.png" alt="" width="300" height="139" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;⑤ftp创建目录失败解决方案</p>
<p>&nbsp;<span class="cnblogs_code">ls -ls /<span style="color: #0000ff;">var</span>/ftp/pub/</span>&nbsp;查看目录的全下，发现所有者的身份是root</p>
<p>&nbsp;<span class="cnblogs_code">chown -Rf ftp /<span style="color: #0000ff;">var</span>/ftp/pub/</span>&nbsp;将目录所有者和所有组的身份改成ftp</p>
<p>&nbsp;<span class="cnblogs_code">getsebool -a | grep ftp</span>&nbsp;查询与FTP相关的SELiunx域策略都有哪些</p>
<p>&nbsp;<span class="cnblogs_code">setsebool -P ftpd_full_access=on</span>&nbsp;修改此项策略。-P表示永久生效</p>
<p>&nbsp;</p>
<p><strong>2，本地用户模式</strong></p>
<table style="height: 194px; width: 786px;" border="0"><caption>本地用户模式使用的权限参数以及 作用</caption>
<tbody>
<tr style="background-color: #746d6c;">
<td>参数</td>
<td>作用</td>
</tr>
<tr>
<td>anonymous_enable=NO</td>
<td>禁止匿名访问模式</td>
</tr>
<tr>
<td>local_enable=YES</td>
<td>允许本地用户模式</td>
</tr>
<tr>
<td>write_enable=YES</td>
<td>设置可写权限</td>
</tr>
<tr>
<td>local_umask=022</td>
<td>本地用户模式创建文件的umask值</td>
</tr>
<tr>
<td>userlist_enable=YES</td>
<td>启用&ldquo;禁止用户名单&rdquo;，名单文件为ftpusers和user_list</td>
</tr>
<tr>
<td>userlist_deny=YES</td>
<td>开启用户作用名单文件功能</td>
</tr>
</tbody>
</table>
<p>①配置vsftpd.conf配置文件</p>
<p>&nbsp;<span class="cnblogs_code">systemctl restart vsftpd</span>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('e325f8fb-aa70-4673-8c89-c1c9583dccac')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_e325f8fb-aa70-4673-8c89-c1c9583dccac" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_e325f8fb-aa70-4673-8c89-c1c9583dccac" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_e325f8fb-aa70-4673-8c89-c1c9583dccac" class="cnblogs_code_hide">
<pre>anonymous_enable=<span style="color: #000000;">NO
local_enable</span>=<span style="color: #000000;">YES
write_enable</span>=<span style="color: #000000;">YES
local_umask</span>=<span style="color: #800080;">022</span><span style="color: #000000;">
dirmessage_enable</span>=<span style="color: #000000;">YES
xferlog_enable</span>=<span style="color: #000000;">YES
connect_from_port_20</span>=<span style="color: #000000;">YES
xferlog_std_format</span>=<span style="color: #000000;">YES
listen</span>=<span style="color: #000000;">NO
listen_ipv6</span>=<span style="color: #000000;">YES

pam_service_name</span>=<span style="color: #000000;">vsftpd
userlist_enable</span>=<span style="color: #000000;">YES
tcp_wrappers</span>=YES</pre>
</div>
<span class="cnblogs_code_collapse">vsftpd.conf</span></div>
<p>现在就可以用liunx系统账户进行登录了ftp了。但是root不能登录ftp</p>
<p>②root账户可以登录TTP服务器</p>
<p>&nbsp;<span class="cnblogs_code">cat /etc/vsftpd/user_list</span>&nbsp;查看禁用的登录账户</p>
<p>&nbsp;<span class="cnblogs_code">cat /etc/vsftpd/ftpusers</span>&nbsp;查看禁用的登录账户</p>
<p>&nbsp;<span class="cnblogs_code">vim /etc/httpd/conf/httpd.conf</span>&nbsp;将root删除掉</p>
<p>&nbsp;<span class="cnblogs_code">vim /etc/vsftpd/ftpusers</span>&nbsp;将root删除掉，删除之后，就可以立即登录了，不需要重启vsftpd服务</p>
<p>③使用普通账户hunter登录，创建目录不了问题</p>
<p>&nbsp;<span class="cnblogs_code">getsebool -a | grep ftp</span>&nbsp;查询与FTP相关的SELiunx域策略都有哪些</p>
<p>&nbsp;<span class="cnblogs_code">setsebool -P ftpd_full_access=on</span>&nbsp;修改此项策略。-P表示永久生效</p>
<p>&nbsp;</p>
<p><strong>3，虚拟用户模式</strong></p>
<p>①创建用于就那些FTP认证的用户数据库文件，其中奇数行为账户名，偶数行我密码，例如，分别创建zhangsan和lisi两个用户，密码均为redhat</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('b6cb1a38-659e-48ae-a5f6-808a89d5cb02')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_b6cb1a38-659e-48ae-a5f6-808a89d5cb02" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_b6cb1a38-659e-48ae-a5f6-808a89d5cb02" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_b6cb1a38-659e-48ae-a5f6-808a89d5cb02" class="cnblogs_code_hide">
<pre><span style="color: #000000;">zhangsan
redhat
lisi
redhat</span></pre>
</div>
<span class="cnblogs_code_collapse">vim /etc/vsftpd/vuser.list</span></div>
<p>&nbsp;<span class="cnblogs_code">db_load -T -t hash -f vuser.list vuser.db</span>&nbsp;db_load命令用哈希（hash）算法将原始的明文信息文件转换成数据库文件</p>
<p>&nbsp;<span class="cnblogs_code">chmod <span style="color: #800080;">600</span> vuser.db</span>&nbsp;降低数据库文件的权限（避免其他人看到数据库文件的内容）</p>
<p>&nbsp;<span class="cnblogs_code">rm -f vuser.list</span>&nbsp;删除原始文件</p>
<p>②创建vsftpd服务程序用于存储文件的根目录（虚拟用户登录后所访问的默认位置）以及虚拟用户映射的系统本地用户。</p>
<p>&nbsp;<span class="cnblogs_code">useradd -d /<span style="color: #0000ff;">var</span>/ftproot -s /sbin/nologin <span style="color: #0000ff;">virtual</span></span>&nbsp;创建virtual用户，此用户不能登录系统，家目录是/var/ftproot</p>
<p>&nbsp;<span class="cnblogs_code">ls -ld /<span style="color: #0000ff;">var</span>/ftproot/</span>&nbsp;查询目录的权限</p>
<p>&nbsp;<span class="cnblogs_code">chmod -Rf <span style="color: #800080;">755</span> /<span style="color: #0000ff;">var</span>/ftproot/</span>&nbsp;修改目录权限</p>
<p>③建立用于支持虚拟用户的PAM文件</p>
<p>新建一个用于虚拟用户认证的PAM文件vsftpd.vu，其中PAM文件内&ldquo;db=&rdquo;参数为使用db_local命令生成的账户密码数据库文件路径，但不用写数据库文件的后缀</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('aa31e87e-4eb3-4b51-b5e1-ea7176d1afed')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_aa31e87e-4eb3-4b51-b5e1-ea7176d1afed" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_aa31e87e-4eb3-4b51-b5e1-ea7176d1afed" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_aa31e87e-4eb3-4b51-b5e1-ea7176d1afed" class="cnblogs_code_hide">
<pre>auth required pam_userdb.so db=/etc/vsftpd/<span style="color: #000000;">vuser
account required pam_userdb.so db</span>=/etc/vsftpd/vuser</pre>
</div>
<span class="cnblogs_code_collapse">vim /etc/pam.d/vsftpd.vu</span></div>
<p>④配置vsftpd.conf</p>
<table style="height: 128px; width: 712px;" border="0"><caption>利用PAM文件进行认证时使用的参数以及作用</caption>
<tbody>
<tr style="background-color: #a19c9b;">
<td>参数</td>
<td>作用</td>
</tr>
<tr>
<td>anonymous_enable=NO</td>
<td>禁止匿名开放模式</td>
</tr>
<tr>
<td>local_enable=YES　　　　</td>
<td>允许本地用户模式</td>
</tr>
<tr>
<td>guest_enable=YES</td>
<td>开启虚拟用户模式</td>
</tr>
<tr>
<td>guest_username=virtual</td>
<td>指定虚拟用户账户</td>
</tr>
<tr>
<td>pam_service_name=vsftpd.vu</td>
<td>指定PAM文件</td>
</tr>
<tr>
<td>allow_writeable_chroot=YES</td>
<td>允许对禁锢的FTP根目录执行写入操作，而且不拒绝用户的登录请求</td>
</tr>
</tbody>
</table>
<div class="cnblogs_code" onclick="cnblogs_code_show('503d883f-1f99-4621-97f0-a265dccb9f2f')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_503d883f-1f99-4621-97f0-a265dccb9f2f" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_503d883f-1f99-4621-97f0-a265dccb9f2f" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_503d883f-1f99-4621-97f0-a265dccb9f2f" class="cnblogs_code_hide">
<pre>anonymous_enable=<span style="color: #000000;">NO
local_enable</span>=<span style="color: #000000;">YES
guest_enable</span>=<span style="color: #000000;">YES
guest_username</span>=<span style="color: #0000ff;">virtual</span><span style="color: #000000;">
allow_writeable_chroot</span>=<span style="color: #000000;">YES
write_enable</span>=<span style="color: #000000;">YES
local_umask</span>=<span style="color: #800080;">022</span><span style="color: #000000;">
dirmessage_enable</span>=<span style="color: #000000;">YES
xferlog_enable</span>=<span style="color: #000000;">YES
connect_from_port_20</span>=<span style="color: #000000;">YES
xferlog_std_format</span>=<span style="color: #000000;">YES
listen</span>=<span style="color: #000000;">NO
listen_ipv6</span>=<span style="color: #000000;">YES
pam_service_name</span>=<span style="color: #000000;">vsftpdi.vu
userlist_enable</span>=<span style="color: #000000;">YES
tcp_wrappers</span>=YES</pre>
</div>
<span class="cnblogs_code_collapse">vim /etc/vsftpd/vsftpd.conf</span></div>
<p>⑤为虚拟账户设置不同的权限</p>
<p>分别设置zhangsan和lisi的权限</p>
<p>zhangsan：允许上传、创建、修改、查看、删除文件</p>
<p>lisi：只允许查看文件</p>
<p>&nbsp;<span class="cnblogs_code">mkdir /etc/vsftpd/vusers_dir</span>&nbsp;创建一个目录，里面分别创建以zhangsan和lisi命令的文件</p>
<p>&nbsp;<span class="cnblogs_code">touch lisi</span>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('2ef4d3ef-630d-4b62-9fcd-aa95f9f7c157')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_2ef4d3ef-630d-4b62-9fcd-aa95f9f7c157" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_2ef4d3ef-630d-4b62-9fcd-aa95f9f7c157" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_2ef4d3ef-630d-4b62-9fcd-aa95f9f7c157" class="cnblogs_code_hide">
<pre>anon_upload_enable=<span style="color: #000000;">YES
anon_mkdir_write_enable</span>=<span style="color: #000000;">YES
anon_other_write_enable</span>=YES</pre>
</div>
<span class="cnblogs_code_collapse">vim zhangsan</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('756e48e4-7297-4e5d-87b7-fb71f53b3aca')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_756e48e4-7297-4e5d-87b7-fb71f53b3aca" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_756e48e4-7297-4e5d-87b7-fb71f53b3aca" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_756e48e4-7297-4e5d-87b7-fb71f53b3aca" class="cnblogs_code_hide">
<pre>anonymous_enable=<span style="color: #000000;">NO
local_enable</span>=<span style="color: #000000;">YES
guest_enable</span>=<span style="color: #000000;">YES
guest_username</span>=<span style="color: #0000ff;">virtual</span><span style="color: #000000;">
allow_writeable_chroot</span>=<span style="color: #000000;">YES
write_enable</span>=<span style="color: #000000;">YES
local_umask</span>=<span style="color: #800080;">022</span><span style="color: #000000;">
dirmessage_enable</span>=<span style="color: #000000;">YES
xferlog_enable</span>=<span style="color: #000000;">YES
connect_from_port_20</span>=<span style="color: #000000;">YES
xferlog_std_format</span>=<span style="color: #000000;">YES
listen</span>=<span style="color: #000000;">NO
listen_ipv6</span>=<span style="color: #000000;">YES
pam_service_name</span>=<span style="color: #000000;">vsftpdi.vu
userlist_enable</span>=<span style="color: #000000;">YES
tcp_wrappers</span>=<span style="color: #000000;">YES
user_config_dir</span>=/etc/vsftpd/vusers_dir</pre>
</div>
<span class="cnblogs_code_collapse">vim /etc/vsftpd/vsftpd.conf 添加user_config_dir配置</span></div>
<p>&nbsp;<span class="cnblogs_code">systemctl restart vsftpd</span>&nbsp;重启</p>
<p>&nbsp;<span class="cnblogs_code">systemctl enable vsftpd</span>&nbsp;开机启动</p>
<p>⑥设置SELiunx域允许策略</p>
<p>&nbsp;<span class="cnblogs_code">getsebool -a | grep ftp</span>&nbsp;查询与FTP相关的SELiunx域策略都有哪些</p>
<p>&nbsp;<span class="cnblogs_code">setsebool -P ftpd_full_access=on</span>&nbsp;修改此项策略。-P表示永久生效</p>
<p><strong><span style="color: #ff0000;">注意： 案例3的vsftpd.conf的pam_service_name=vsftpd.vu配置有问题，需要去掉i字母</span></strong></p>
<p><strong>4，上传下载文件</strong></p>
<p>&nbsp;<span class="cnblogs_code"><span style="color: #0000ff;">get</span> aa.txt /home/aa.txt</span>&nbsp;下载文件&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">put /home/<span style="color: #800080;">11</span>.txt <span style="color: #800080;">11</span>.txt</span>&nbsp;上传文件</p>
<p>&nbsp;</p>
<p><strong>5，简单文件传输协议</strong></p>
<p>简单文件传输协议（TFTP）是一种基于UDP协议在客户端和服务器之间进行简单的传输协议，占用端口号为69</p>
<p>&nbsp;<span class="cnblogs_code">yum install tftp-server tftp</span>&nbsp;安装tfpt</p>
<p>&nbsp;<span class="cnblogs_code">yum install xinetd</span>&nbsp;安装xinetd。TFTP服务是xinetd服务程序来管理的</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('e6f9452a-56d2-4941-986c-c2995cf5c887')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_e6f9452a-56d2-4941-986c-c2995cf5c887" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_e6f9452a-56d2-4941-986c-c2995cf5c887" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_e6f9452a-56d2-4941-986c-c2995cf5c887" class="cnblogs_code_hide">
<pre># <span style="color: #0000ff;">default</span><span style="color: #000000;">: off
# description: The tftp server serves files </span><span style="color: #0000ff;">using</span><span style="color: #000000;"> the trivial file transfer \
#       protocol.  The tftp protocol </span><span style="color: #0000ff;">is</span><span style="color: #000000;"> often used to boot diskless \
#       workstations, download configuration files to network</span>-<span style="color: #000000;">aware printers, \
#       and to start the installation process </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> some operating systems.
service tftp
{
        socket_type             </span>=<span style="color: #000000;"> dgram
        protocol                </span>=<span style="color: #000000;"> udp
        wait                    </span>=<span style="color: #000000;"> yes
        user                    </span>=<span style="color: #000000;"> root
        server                  </span>= /usr/sbin/<span style="color: #0000ff;">in</span><span style="color: #000000;">.tftpd
        server_args             </span>= -s /<span style="color: #0000ff;">var</span>/lib/<span style="color: #000000;">tftpboot
        disable                 </span>=<span style="color: #000000;"> no
        per_source              </span>= <span style="color: #800080;">11</span><span style="color: #000000;">
        cps                     </span>= <span style="color: #800080;">100</span> <span style="color: #800080;">2</span><span style="color: #000000;">
        flags                   </span>=<span style="color: #000000;"> IPv4
}</span></pre>
</div>
<span class="cnblogs_code_collapse">vim /etc/xinetd.d/tftp 把默认禁用（disable）参数修改为no</span></div>
<p>&nbsp;<span class="cnblogs_code">systemctl restart xinetd</span>&nbsp;重启服务</p>
<p>&nbsp;<span class="cnblogs_code">systemctl enable xinetd</span>&nbsp;加入开机启动</p>
<p>&nbsp;<span class="cnblogs_code">firewall-cmd --permanent --add-port=<span style="color: #800080;">69</span>/udp</span>&nbsp;设置防火墙允许UDP协议的69端口</p>
<p>&nbsp;<span class="cnblogs_code">firewall-cmd --reload</span>&nbsp;重启防火墙</p>
<p>①使用tftp目录访问文件</p>
<table style="height: 229px; width: 854px;" border="0"><caption>ftpd命令中可用的参数以及作用</caption>
<tbody>
<tr style="background-color: #696362;">
<td>参数</td>
<td>作用</td>
</tr>
<tr>
<td>&nbsp;?</td>
<td>帮助信息&nbsp;</td>
</tr>
<tr>
<td>&nbsp;put</td>
<td>&nbsp;上传文件</td>
</tr>
<tr>
<td>&nbsp;get</td>
<td>&nbsp;下载文件</td>
</tr>
<tr>
<td>&nbsp;verbose</td>
<td>&nbsp;显示详细的处理信息</td>
</tr>
<tr>
<td>&nbsp;status</td>
<td>&nbsp;显示当前的状态信息</td>
</tr>
<tr>
<td>&nbsp;binary</td>
<td>&nbsp;使用二进制进行传输</td>
</tr>
<tr>
<td>&nbsp;ascii</td>
<td>&nbsp;使用ASCII码进行传输</td>
</tr>
<tr>
<td>&nbsp;timeout</td>
<td>&nbsp;设置重传的超时时间</td>
</tr>
<tr>
<td>&nbsp;quit</td>
<td>&nbsp;退出</td>
</tr>
</tbody>
</table>
<p>&nbsp;<img src="https://img2020.cnblogs.com/blog/741594/202011/741594-20201115134156305-245103307.png" alt="" width="405" height="91" loading="lazy" /></p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: rgba(22, 159, 230, 1);"><span style="font-size: 18pt; color: #ffffff;"><strong><a name="a12"></a>十二、使用Samba或NFS实现文件共享</strong></span></p>
<p>&nbsp;<strong>1，Samba文件共享服务</strong></p>
<p>Samba服务程序现在已经成为在liunx系统与Windows系统之间共享文件的最佳选择</p>
<p>&nbsp;<span class="cnblogs_code">yum install samba</span>&nbsp;安装samba</p>
<table style="height: 706px; width: 961px;" border="0"><caption>Samba服务程序中的参数以及作用</caption>
<tbody>
<tr>
<td>&nbsp;</td>
<td>参数</td>
<td>作用</td>
</tr>
<tr>
<td rowspan="8">[global]</td>
<td>workgroup = MYGROUP</td>
<td>#工作组名称</td>
</tr>
<tr>
<td>server string = Samba Server Version %v</td>
<td>#服务器介绍信息，参数%v为显示SMB版本号</td>
</tr>
<tr>
<td>log file=/var/log/samba/log.%m</td>
<td>#定义日志文件存放位置与名称，参数%m为来访的主机名</td>
</tr>
<tr>
<td>max log size = 50</td>
<td>#定义日志文件的最大容量为50KB</td>
</tr>
<tr>
<td>security = user</td>
<td>
<p>#安全认证方式，总共有4种</p>
<p>#share：来访主机无需验证口令；比较方便，但安全性很差</p>
<p>#user：需要验证来访主机提供的口令后才可以访问；提升了安全性</p>
<p>#server：使用独立的远程主机验证来访问提供的口令（集中管理账户）</p>
<p>#domain：使用域控制器进行身份验证</p>
<p>&nbsp;</p>
</td>
</tr>
<tr>
<td>passdb backend = tdbsam</td>
<td>
<p>#定义用户后台的类型，共有3种</p>
<p>#smbpassword：使用smbpasswd命令为系统用户设置Samba服务程序密码</p>
<p>#tdbsam：创建数据库文件并使用pdbedit命令建立Samba服务程序的用户</p>
<p>#ldapsam：基于LDAP服务进行账户验证</p>
</td>
</tr>
<tr>
<td>load printers = yes</td>
<td>#设置在Samba服务启动时是否共享打印机设备</td>
</tr>
<tr>
<td>cups options= raw</td>
<td>#打印机的选项</td>
</tr>
<tr>
<td rowspan="3">
<p>[homes]</p>
<p>#共享参数</p>
</td>
<td>comment = Home Directories</td>
<td>#描述信息</td>
</tr>
<tr>
<td>browseable = no</td>
<td>#定义共享信息是否在&ldquo;网上邻居&rdquo;中可见</td>
</tr>
<tr>
<td>writable = yes</td>
<td>#定义是否可以执行写入操作，与&ldquo;read only&rdquo;相反</td>
</tr>
<tr>
<td>
<p>[printers]</p>
<p>#打印机共享参数</p>
</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
</tbody>
</table>
<p>&nbsp;<span class="cnblogs_code">mv /etc/samba/smb.conf /etc/samba/smb.conf_bak</span>&nbsp; 备份配置文件</p>
<div class="cnblogs_code">
<pre>cat /etc/samba/smb.conf_bak | grep -v <span style="color: #800000;">"</span><span style="color: #800000;">#</span><span style="color: #800000;">"</span> | grep -v <span style="color: #800000;">"</span><span style="color: #800000;">;</span><span style="color: #800000;">"</span> | grep -v <span style="color: #800000;">"</span><span style="color: #800000;">^$</span><span style="color: #800000;">"</span> &gt;/etc/samba/smb.conf</pre>
</div>
<p>将未注释的配置写入到smb.conf文件中。&nbsp;&nbsp;grep -v "^$"&nbsp; 可以去除空白行</p>
<p><strong>&nbsp;2，配置共享资源</strong></p>
<table style="height: 212px; width: 659px;" border="0"><caption>用于设置Samba服务程序的参数以及作用</caption>
<tbody>
<tr>
<td>参数</td>
<td>作用</td>
</tr>
<tr>
<td>[database]</td>
<td>共享名称为database</td>
</tr>
<tr>
<td>comment = Do not arbitrarily modify the database file</td>
<td>警告用户不要随便修改数据库</td>
</tr>
<tr>
<td>path = /home/database</td>
<td>共享目录为/home/database</td>
</tr>
<tr>
<td>public = no</td>
<td>关闭&ldquo;所有人可见&rdquo;</td>
</tr>
<tr>
<td>writable = yes</td>
<td>允许写入操作</td>
</tr>
</tbody>
</table>
<div class="cnblogs_code" onclick="cnblogs_code_show('3f8105bb-3a80-47f8-99db-5a798bfef010')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_3f8105bb-3a80-47f8-99db-5a798bfef010" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_3f8105bb-3a80-47f8-99db-5a798bfef010" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_3f8105bb-3a80-47f8-99db-5a798bfef010" class="cnblogs_code_hide">
<pre>[<span style="color: #0000ff;">global</span><span style="color: #000000;">]
        workgroup </span>=<span style="color: #000000;"> SAMBA
        security </span>=<span style="color: #000000;"> user
        passdb backend </span>=<span style="color: #000000;"> tdbsam
        printing </span>=<span style="color: #000000;"> cups
        printcap name </span>=<span style="color: #000000;"> cups
        load printers </span>=<span style="color: #000000;"> yes
        cups options </span>=<span style="color: #000000;"> raw
[homes]
        comment </span>=<span style="color: #000000;"> Home Directories
        valid users </span>= %S, %D%w%<span style="color: #000000;">S
        browseable </span>=<span style="color: #000000;"> No
        read only </span>=<span style="color: #000000;"> No
        inherit acls </span>=<span style="color: #000000;"> Yes
[printers]
        comment </span>=<span style="color: #000000;"> All Printers
        path </span>= /<span style="color: #0000ff;">var</span>/<span style="color: #000000;">tmp
        printable </span>=<span style="color: #000000;"> Yes
        create mask </span>= <span style="color: #800080;">0600</span><span style="color: #000000;">
        browseable </span>=<span style="color: #000000;"> No
[print$]
        comment </span>=<span style="color: #000000;"> Printer Drivers
        path </span>= /<span style="color: #0000ff;">var</span>/lib/samba/<span style="color: #000000;">drivers
        write list </span>=<span style="color: #000000;"> @printadmin root
        force group </span>=<span style="color: #000000;"> @printadmin
        create mask </span>= <span style="color: #800080;">0664</span><span style="color: #000000;">
        directory mask </span>= <span style="color: #800080;">0775</span><span style="color: #000000;">
[database]
        comment </span>=<span style="color: #000000;"> Do not arbitrarily modify the database file
        path </span>= /home/<span style="color: #000000;">database
        </span><span style="color: #0000ff;">public</span> =<span style="color: #000000;"> no
        writable </span>= yes</pre>
</div>
<span class="cnblogs_code_collapse">/etc/samba/smb.conf</span></div>
<p>①创建用于访问共享资源的账户信息。默认的使用的是用户口令认证模式（user）。Samba服务要求账户必须在当前系统已经存在</p>
<table style="height: 107px; width: 732px;" border="0"><caption>用户pdbedit命令的参数以及作用</caption>
<tbody>
<tr>
<td>参数</td>
<td>作用</td>
</tr>
<tr>
<td>-a 用户名</td>
<td>建立Samba账户</td>
</tr>
<tr>
<td>-x 用户名</td>
<td>删除Samba账户</td>
</tr>
<tr>
<td>-L</td>
<td>列出账户列表</td>
</tr>
<tr>
<td>-Lv</td>
<td>列出账户详细信息的列表</td>
</tr>
</tbody>
</table>
<p>&nbsp;<span class="cnblogs_code">id hunter</span>&nbsp;查看当前系统账户详细</p>
<p>&nbsp;<span class="cnblogs_code">pdbedit -a -u hunter</span>&nbsp;建立Samba账户</p>
<p>&nbsp;<span class="cnblogs_code">mkdir /home/database</span>&nbsp;创建共享目录</p>
<p>&nbsp;<span class="cnblogs_code">chown hunter /home/database/</span>&nbsp;设置共享目录的所有者和所属组</p>
<p>&nbsp;<span class="cnblogs_code">ls -Zd /home/database/</span>&nbsp;查看目录是否拥有不同的SELiunx安全上下文</p>
<p>&nbsp;<span class="cnblogs_code">semanage fcontext -a -t samba_share_t /home/database</span>&nbsp;设置SELiunx安全上下文</p>
<p>&nbsp;<span class="cnblogs_code">restorecon -Rv /home/database/</span>&nbsp;设置好的SELiunx安全上下文立即生效。-Rv对指定的目录进行递归操作</p>
<p>&nbsp;<span class="cnblogs_code">getsebool -a | grep samba</span>&nbsp;查询与Samba相关的SELiunx域策略都有哪些</p>
<p>&nbsp;<span class="cnblogs_code">setsebool -P samba_enable_home_dirs on</span>&nbsp;配置策略</p>
<p>&nbsp;<span class="cnblogs_code">systemctl restart smb</span>&nbsp;重启服务</p>
<p>&nbsp;<span class="cnblogs_code">systemctl enable smb</span>&nbsp;开启启动</p>
<p>&nbsp;<span class="cnblogs_code">iptables -F</span>&nbsp;清空iptables防火墙</p>
<p>②Windows访问文件共享服务</p>
<p>//192.168.0.140 输入用户名密码进入共享</p>
<p>③Liunx访问文件共享服务</p>
<p>&nbsp;&nbsp;<span class="cnblogs_code">yum install cifs-utils</span>&nbsp;在客户端安装支持文件共享服务的软件包（cifs-utils）</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('f3ae53a0-4895-43b4-ae14-b8f753ad574a')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_f3ae53a0-4895-43b4-ae14-b8f753ad574a" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_f3ae53a0-4895-43b4-ae14-b8f753ad574a" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_f3ae53a0-4895-43b4-ae14-b8f753ad574a" class="cnblogs_code_hide">
<pre>username=<span style="color: #000000;">hunter
password</span>=<span style="color: #800080;">123456</span><span style="color: #000000;">
domain</span>=MYGROUP</pre>
</div>
<span class="cnblogs_code_collapse">vim auth.smb 安装服务的用户名、密码、共享域的顺序写入到一个认证文件中</span></div>
<p>&nbsp;<span class="cnblogs_code">chmod <span style="color: #800080;">600</span> auth.smb</span>&nbsp;不让其他人随意看到，修改为仅root管理员才能够读写</p>
<p>&nbsp;<span class="cnblogs_code">mkdir /database</span>&nbsp;创建一个挂载目录</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('f2366be5-ade0-4348-9198-8de208e407b4')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_f2366be5-ade0-4348-9198-8de208e407b4" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_f2366be5-ade0-4348-9198-8de208e407b4" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_f2366be5-ade0-4348-9198-8de208e407b4" class="cnblogs_code_hide">
<pre><span style="color: #000000;">#
# </span>/etc/<span style="color: #000000;">fstab
# Created by anaconda on Wed Jul  </span><span style="color: #800080;">8</span> <span style="color: #800080;">05</span>:<span style="color: #800080;">42</span>:<span style="color: #800080;">34</span> <span style="color: #800080;">2020</span><span style="color: #000000;">
#
# Accessible filesystems, by reference, are maintained under </span><span style="color: #800000;">'</span><span style="color: #800000;">/dev/disk</span><span style="color: #800000;">'</span><span style="color: #000000;">
# See man pages fstab(</span><span style="color: #800080;">5</span>), findfs(<span style="color: #800080;">8</span>), mount(<span style="color: #800080;">8</span>) and/or blkid(<span style="color: #800080;">8</span>) <span style="color: #0000ff;">for</span><span style="color: #000000;"> more info
#
</span>/dev/mapper/centos-root /                       xfs     defaults        <span style="color: #800080;">0</span> <span style="color: #800080;">0</span><span style="color: #000000;">
UUID</span>=1c4160c0-<span style="color: #800080;">2579</span>-4b50-b4b8-dcf66caf05ec /boot                   xfs     defaults        <span style="color: #800080;">0</span> <span style="color: #800080;">0</span>
/dev/mapper/centos-home /home                   xfs     defaults        <span style="color: #800080;">0</span> <span style="color: #800080;">0</span>
/dev/mapper/centos-swap swap                    swap    defaults        <span style="color: #800080;">0</span> <span style="color: #800080;">0</span>
<span style="color: #008000;">//</span><span style="color: #008000;">192.168.0.140/database /database cifs credentials=/root/auth.smb 0 0</span></pre>
</div>
<span class="cnblogs_code_collapse">配置挂载信息 vim /etc/fstab</span></div>
<p>&nbsp;<span class="cnblogs_code">mount -a</span>&nbsp;挂载</p>
<p>&nbsp;</p>
<p><strong>3，NFS（网络文件系统）</strong></p>
<p>NFS服务可以将远程Liunx系统上的文件共享资源挂在到本地主机目录上</p>
<p>&nbsp;<span class="cnblogs_code">yum install nfs-utils</span>&nbsp;安装nfs</p>
<p>&nbsp;<span class="cnblogs_code">iptables -F</span>&nbsp;清理iptables规则</p>
<p>&nbsp;<span class="cnblogs_code">mkdir /nfsfile</span>&nbsp;创建一个目录作为后面的共享目录</p>
<p>&nbsp;<span class="cnblogs_code">chmod -Rf <span style="color: #800080;">777</span> /nfsfile/</span>&nbsp;给上最高权限</p>
<p>&nbsp;<span class="cnblogs_code">echo <span style="color: #800000;">"</span><span style="color: #800000;">111</span><span style="color: #800000;">"</span> &gt; /nfsfile/readme</span>&nbsp;往目录里面写入一个文件</p>
<p>&nbsp;<span class="cnblogs_code">vim /etc/exports</span>&nbsp;配置NFS服务程序的配置文件，默认此文件是空的。</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('7bf7fc9d-3b17-406f-9641-e500ab1c6da6')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_7bf7fc9d-3b17-406f-9641-e500ab1c6da6" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_7bf7fc9d-3b17-406f-9641-e500ab1c6da6" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_7bf7fc9d-3b17-406f-9641-e500ab1c6da6" class="cnblogs_code_hide">
<pre>/nfsfile <span style="color: #800080;">192.168</span>.<span style="color: #800080;">0</span>.*(rw,sync,root_squash)</pre>
</div>
<span class="cnblogs_code_collapse">/etc/exports</span></div>
<table style="height: 136px; width: 695px;" border="0"><caption>用于配置NFS服务程序配置文件的参数</caption>
<tbody>
<tr>
<td>参数</td>
<td>作用</td>
</tr>
<tr>
<td>ro</td>
<td>只读</td>
</tr>
<tr>
<td>rw</td>
<td>读写</td>
</tr>
<tr>
<td>root_squash</td>
<td>当NFS客户端以root管理员访问时，映射为NFS服务器的匿名用户</td>
</tr>
<tr>
<td>no_root_squash</td>
<td>当NFS客户端以root管理员访问时，映射为NFS服务器的root管理员</td>
</tr>
<tr>
<td>all_squash</td>
<td>无论NFS客户端使用什么账户访问，均映射为NFS服务器的匿名用户</td>
</tr>
<tr>
<td>sync</td>
<td>同时将数据写入到内存与硬盘中，保证不丢失数据</td>
</tr>
<tr>
<td>async</td>
<td>优先将数据保存在内存中，然后写入硬盘；这样效率更高，但可能会丢失数据</td>
</tr>
</tbody>
</table>
<p>&nbsp;<span class="cnblogs_code">systemctl restart rpcbind</span>&nbsp;先启用RPC</p>
<p>&nbsp;<span class="cnblogs_code">systemctl enable rpcbind</span>&nbsp;开启启动</p>
<p>&nbsp;<span class="cnblogs_code">systemctl restart nfs-server</span>&nbsp;启动nfs</p>
<p>&nbsp;<span class="cnblogs_code">systemctl enable nfs-server</span>&nbsp;开启启动</p>
<p>①客户端</p>
<p>&nbsp;<span class="cnblogs_code">showmount -e <span style="color: #800080;">192.168</span>.<span style="color: #800080;">0.140</span></span>&nbsp;查询远程NFS共享信息</p>
<p>&nbsp;<span class="cnblogs_code">mkdir /nfsfile</span>&nbsp;创建挂载目录</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('8bb97793-bf38-452f-9769-23a2cccc66b9')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_8bb97793-bf38-452f-9769-23a2cccc66b9" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_8bb97793-bf38-452f-9769-23a2cccc66b9" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_8bb97793-bf38-452f-9769-23a2cccc66b9" class="cnblogs_code_hide">
<pre><span style="color: #000000;">#
# </span>/etc/<span style="color: #000000;">fstab
# Created by anaconda on Wed Jul  </span><span style="color: #800080;">8</span> <span style="color: #800080;">05</span>:<span style="color: #800080;">42</span>:<span style="color: #800080;">34</span> <span style="color: #800080;">2020</span><span style="color: #000000;">
#
# Accessible filesystems, by reference, are maintained under </span><span style="color: #800000;">'</span><span style="color: #800000;">/dev/disk</span><span style="color: #800000;">'</span><span style="color: #000000;">
# See man pages fstab(</span><span style="color: #800080;">5</span>), findfs(<span style="color: #800080;">8</span>), mount(<span style="color: #800080;">8</span>) and/or blkid(<span style="color: #800080;">8</span>) <span style="color: #0000ff;">for</span><span style="color: #000000;"> more info
#
</span>/dev/mapper/centos-root /                       xfs     defaults        <span style="color: #800080;">0</span> <span style="color: #800080;">0</span><span style="color: #000000;">
UUID</span>=1c4160c0-<span style="color: #800080;">2579</span>-4b50-b4b8-dcf66caf05ec /boot                   xfs     defaults        <span style="color: #800080;">0</span> <span style="color: #800080;">0</span>
/dev/mapper/centos-home /home                   xfs     defaults        <span style="color: #800080;">0</span> <span style="color: #800080;">0</span>
/dev/mapper/centos-swap swap                    swap    defaults        <span style="color: #800080;">0</span> <span style="color: #800080;">0</span>
<span style="color: #008000;">//</span><span style="color: #008000;">192.168.0.140/database /database cifs credentials=/root/auth.smb 0 0</span>
<span style="color: #800080;">192.168</span>.<span style="color: #800080;">0.140</span>:/nfsfile /nfsfile nfs defaults <span style="color: #800080;">0</span> <span style="color: #800080;">0</span></pre>
</div>
<span class="cnblogs_code_collapse">vim /etc/fstab</span></div>
<p>&nbsp;<span class="cnblogs_code">mount -a</span>&nbsp;挂载</p>
<p>&nbsp;<span class="cnblogs_code">cd /nfsfile/</span>&nbsp;进入共享目录</p>
<p>&nbsp;</p>
<p><strong>4，autofs自动挂载服务</strong></p>
<p>&nbsp;<span class="cnblogs_code">yum install autofs</span>&nbsp;安装autofs</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('0c648a36-acf0-49f9-bdb3-71352713c55e')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_0c648a36-acf0-49f9-bdb3-71352713c55e" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_0c648a36-acf0-49f9-bdb3-71352713c55e" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_0c648a36-acf0-49f9-bdb3-71352713c55e" class="cnblogs_code_hide">
<pre><span style="color: #000000;">#
# Sample auto.master file
# This </span><span style="color: #0000ff;">is</span> a <span style="color: #800000;">'</span><span style="color: #800000;">master</span><span style="color: #800000;">'</span><span style="color: #000000;"> automounter map and it has the following format:
# mount</span>-point [map-<span style="color: #000000;">type[,format]:]map [options]
# For details of the format look at auto.master(</span><span style="color: #800080;">5</span><span style="color: #000000;">).
#
</span>/media  /etc/<span style="color: #000000;">iso.misc
</span>/misc   /etc/<span style="color: #000000;">auto.misc
#
# NOTE: mounts done </span><span style="color: #0000ff;">from</span><span style="color: #000000;"> a hosts map will be mounted with the
#       </span><span style="color: #800000;">"</span><span style="color: #800000;">nosuid</span><span style="color: #800000;">"</span> and <span style="color: #800000;">"</span><span style="color: #800000;">nodev</span><span style="color: #800000;">"</span> options unless the <span style="color: #800000;">"</span><span style="color: #800000;">suid</span><span style="color: #800000;">"</span> and <span style="color: #800000;">"</span><span style="color: #800000;">dev</span><span style="color: #800000;">"</span><span style="color: #000000;">
#       options are explicitly given.
#
</span>/net    -<span style="color: #000000;">hosts
#
# Include </span>/etc/auto.master.d<span style="color: #008000;">/*</span><span style="color: #008000;">.autofs
# The included files must conform to the format of this file.
#
+dir:/etc/auto.master.d
#
# Include central master map if it can be found using
# nsswitch sources.
#
# Note that if there are entries for /net or /misc (as
# above) in the included master map any keys that are the
# same will not be seen as the first read key seen takes
# precedence.
#
+auto.master</span></pre>
</div>
<span class="cnblogs_code_collapse">vim /etc/auto.master 配置autofs主配置文件，添加/media /etc/iso.misc</span></div>
<p>光盘设备一般挂载到/media/cdrom目录中，那么挂载目录写成/media即可，子目录cdrom在iso.misc文件中配置，目前没有这个文件，需要创建</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('5b94de93-3bda-4620-af13-c9fde695f35f')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_5b94de93-3bda-4620-af13-c9fde695f35f" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_5b94de93-3bda-4620-af13-c9fde695f35f" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_5b94de93-3bda-4620-af13-c9fde695f35f" class="cnblogs_code_hide">
<pre>iso -fstype=iso9660,ro,nosuid,nodev :/dev/cdrom</pre>
</div>
<span class="cnblogs_code_collapse">vim /etc/iso.misc</span></div>
<p>iso.misc 格式： 挂载目录[空格]挂载文件类型及权限[空格]:设备名称（iso -fstype=iso9660,ro,nosuid,nodev :/dev/cdrom）</p>
<p>例如，要把光盘设备挂载到/media/iso目录中，可将挂载目录写为iso，而-fstype为文件系统格式参数，iso9660为光盘设备格式，ro、nosuid及nodev为光盘设备具体的权限参数，/dev/cdrom则是定义要挂载的设备名称</p>
<p>&nbsp;<span class="cnblogs_code">systemctl start autofs</span>&nbsp;启动服务</p>
<p>&nbsp;<span class="cnblogs_code">systemctl enable autofs</span>&nbsp;开机加载</p>
<p>现在看/media目录下是没有目录的，可以用cd iso进入目录，并自动挂载</p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: rgba(22, 159, 230, 1);"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a13"></a>十三、使用Postfix与Dovecot部署邮件系统</span></strong></span></p>
<p>&nbsp;电子邮箱系统基于邮件协议来完成电子邮件的传输，常见的邮件协议有下面这些：</p>
<ul>
<li><span style="font-size: 12px;">简单邮件传输协议（Simple Mail Transfer Protocol，SMTP）：用于发送和中转发出的电子邮件，占用服务器的25/TCP端口</span></li>
<li><span style="font-size: 12px;">邮局协议版本3（Post Office Protocol 3）：用于将电子邮件存储到本地主机，占用服务器的110/TCP端口</span></li>
<li><span style="font-size: 12px;">Internet消息访问协议版本4（Internet Message Access Protocol 4）：用于在本地主机上访问邮件，占用服务器的143/TCP端口</span></li>
</ul>
<p>服务角色：</p>
<ul>
<li><span style="font-size: 12px;">MUA：为用户收发邮件的服务器名为邮件用户代理</span></li>
<li><span style="font-size: 12px;">MDA：邮件投递代理。保存用户邮件的&ldquo;信箱&rdquo;服务器。其工作职责是把来自邮件传输代理（MTA）的邮件保存到本地的收件箱中</span></li>
<li><span style="font-size: 12px;">MTA：邮件传输代理。它的工作职责是转发处理不同的电子邮件服务供应商之间的邮件，把来自MUA的邮件转发到合适的MTA服务器</span></li>
</ul>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: rgba(22, 159, 230, 1);"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a14"></a>十四、使用iSCSI服务器部署网络存储</span></strong></span></p>
<p>&nbsp;iSCSI（Internet Small Computer System Interface）：这是一种将SCSI接口与以太网技术相结合的新型存储技术，可以用来在网络中传输SCSI接口命令和数据</p>
<p><strong>&nbsp;1，配置iSCSI服务端</strong></p>
<p>①选择之前创建的/dev/md0（RAID10）作为远程设备</p>
<p>②安装iSCSI服务端并启动</p>
<p>&nbsp;<span class="cnblogs_code">yum -y install targetd targetcli</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">systemctl start targetd</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">systemctl enable targetd</span>&nbsp;</p>
<ul>
<li>&nbsp;<span style="font-size: 12px;">targetd：iSCSI服务端程序</span></li>
<li><span style="font-size: 12px;">&nbsp;targetcli：用于管理iSCSI服务端存储资源专用配置命令</span></li>
</ul>
<p>③配置iSCSI服务端共享资源</p>
<p>&nbsp;<span class="cnblogs_code">targetcli</span>&nbsp;在执行targetcli命令后就能看到交互式的配置界面了</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202011/741594-20201121141323222-624233263.png" alt="" width="501" height="88" loading="lazy" /></p>
<p>&nbsp;/backstores/block目录：iSCSI服务端配置共享设备的位置。我们需要把/dev/md0设备加入到共享设备的&ldquo;资源池&rdquo;中，并将该文件重新命名为disk0</p>
<p>&nbsp;&nbsp;<span class="cnblogs_code">cd backstores/block</span>&nbsp;进入block目录</p>
<p>&nbsp;&nbsp;<span class="cnblogs_code">create disk0 /dev/md0</span>&nbsp;把/dev/md0设备加入到共享设备的&ldquo;资源池&rdquo;中，并将该文件重新命名为disk0</p>
<p>④创建iSCSI target名称及配置共享资源。</p>
<p>这个是用于描述共享资源的唯一字符串</p>
<p>&nbsp;<span class="cnblogs_code">cd iscsi</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">create</span>&nbsp;创建</p>
<p>&nbsp;<span class="cnblogs_code">cd /iscsi/iqn.<span style="color: #800080;">2003</span>-<span style="color: #800080;">01</span>.org.linux-iscsi.liunxprobe.x8664:sn.e6ccae6a8603/tpg1/<span style="color: #000000;">luns </span>/iscsi/iqn.<span style="color: #800080;">20</span>...<span style="color: #800080;">603</span>/tpg1/luns&gt; create /backstores/block/disk0</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">create /backstores/block/disk0</span>&nbsp;</p>
<p>⑤设置访问控制列表（ACL）</p>
<p>acls参数目录用于存放能够访问iSCSI服务端共享存储资源的客户端名称</p>
<p>&nbsp;<span class="cnblogs_code">cd iqn.<span style="color: #800080;">2003</span>-<span style="color: #800080;">01</span>.org.linux-iscsi.liunxprobe.x8664:sn.e6ccae6a8603/tpg1/acls</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">create iqn.<span style="color: #800080;">2003</span>-<span style="color: #800080;">01</span>.org.linux-iscsi.liunxprobe.x8664:sn.e6ccae6a8603:client</span>&nbsp;</p>
<p>⑥设置iSCSI服务端的监听IP地址和端口号</p>
<p>&nbsp;<span class="cnblogs_code">cd /iscsi/iqn.<span style="color: #800080;">2003</span>-<span style="color: #800080;">01</span>.org.linux-iscsi.liunxprobe.x8664:sn.e6ccae6a8603/tpg1/portals/</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">delete <span style="color: #800080;">0.0</span>.<span style="color: #800080;">0.0</span> <span style="color: #800080;">3260</span></span>&nbsp;删除默认的配置</p>
<p>&nbsp;<span class="cnblogs_code">create <span style="color: #800080;">192.168</span>.<span style="color: #800080;">0.140</span></span>&nbsp;添加监听IP地址和端口号（192.168.0.140 3260）</p>
<p>&nbsp;⑦配合妥当后检查配置信息，重启iSCSI服务端程序并配置防火墙策略</p>
<p>在确认无误后输入exit命令退出配置。（如果Ctrl + C退出，则不会保存配置）</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202011/741594-20201121145256061-1007039704.png" alt="" width="800" height="335" loading="lazy" /></p>
<p>&nbsp;<span class="cnblogs_code">systemctl restart targetd</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">firewall-cmd --permanent --add-port=<span style="color: #800080;">3260</span>/tcp</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">firewall-cmd --reload</span>&nbsp;</p>
<p>&nbsp;</p>
<p><strong>2，配置Liunx客户端</strong></p>
<p>①安装iSCSI客户端服务程序initiator</p>
<p>&nbsp;<span class="cnblogs_code">yum -y install iscsi-initiator-utils</span>&nbsp;</p>
<p>②编辑配置文件，把服务器的访问控制列表名称填写进来，然后重新并加入开机启动</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('ca223582-71b4-4edd-852e-9762918d4bd4')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_ca223582-71b4-4edd-852e-9762918d4bd4" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_ca223582-71b4-4edd-852e-9762918d4bd4" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_ca223582-71b4-4edd-852e-9762918d4bd4" class="cnblogs_code_hide">
<pre>InitiatorName=iqn.<span style="color: #800080;">2003</span>-<span style="color: #800080;">01</span>.org.linux-iscsi.liunxprobe.x8664:sn.e6ccae6a8603:client</pre>
</div>
<span class="cnblogs_code_collapse">vim /etc/iscsi/initiatorname.iscsi</span></div>
<p>&nbsp;<span class="cnblogs_code">systemctl restart iscsid</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">systemctl enable iscsid</span>&nbsp;</p>
<p>③iSCSI客户端扫描iSCSI服务端有哪些共享资源</p>
<p>&nbsp;<span class="cnblogs_code">iscsiadm -m discovery -t st -p <span style="color: #800080;">192.168</span>.<span style="color: #800080;">0.140</span></span>&nbsp;</p>
<ul>
<li><span style="font-size: 12px;">-m discovery ：参数目录是扫描并发现可用的存储资源</span></li>
<li><span style="font-size: 12px;">-t st：参数为执行扫描操作的类型</span></li>
<li><span style="font-size: 12px;">-p 192.168.0.140：iSCSI服务端的地址</span></li>
</ul>
<p>④登录iSCSI服务端</p>
<p>&nbsp;<span class="cnblogs_code">iscsiadm -m node -T iqn.<span style="color: #800080;">2003</span>-<span style="color: #800080;">01</span>.org.linux-iscsi.liunxprobe.x8664:sn.e6ccae6a8603 -p <span style="color: #800080;">192.168</span>.<span style="color: #800080;">0.140</span> --login</span>&nbsp;</p>
<ul>
<li><span style="font-size: 12px;">-m node：参数为将客户端都在的主机作为一台节点服务器</span></li>
<li><span style="font-size: 12px;">-T iqn.2003-01.org.linux-iscsi.liunxprobe.x8664:sn.e6ccae6a8603：参数为要使用的存储资源</span></li>
<li><span style="font-size: 12px;">-p 192.168.0.140：iSCSI服务端的地址</span></li>
<li><span style="font-size: 12px;">--login：进行登录验证</span></li>
</ul>
<p>登录成功之后，会发现客户端主机上多了一个/dev/sdb的设备文件</p>
<p>⑤对/dev/sdb的设备文件继续格式化并挂载</p>
<p>&nbsp;<span class="cnblogs_code">mkfs.ext4 /dev/sdb</span>&nbsp;网络磁盘文件格式为ext4格式，所以需要用ext4类型格式化</p>
<p>&nbsp;<span class="cnblogs_code">mkdir /iscsi</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">mount /dev/sdb /iscsi/</span>&nbsp;</p>
<p>⑥对/dev/sdb的设备进行永久挂载</p>
<p>&nbsp;<span class="cnblogs_code">blkid | grep /dev/sdb</span>&nbsp;查看设备的UUID</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('46b44060-4a33-4420-b650-738d01172f49')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_46b44060-4a33-4420-b650-738d01172f49" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_46b44060-4a33-4420-b650-738d01172f49" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_46b44060-4a33-4420-b650-738d01172f49" class="cnblogs_code_hide">
<pre><span style="color: #000000;">#
# </span>/etc/<span style="color: #000000;">fstab
# Created by anaconda on Wed Jul  </span><span style="color: #800080;">8</span> <span style="color: #800080;">05</span>:<span style="color: #800080;">42</span>:<span style="color: #800080;">34</span> <span style="color: #800080;">2020</span><span style="color: #000000;">
#
# Accessible filesystems, by reference, are maintained under </span><span style="color: #800000;">'</span><span style="color: #800000;">/dev/disk</span><span style="color: #800000;">'</span><span style="color: #000000;">
# See man pages fstab(</span><span style="color: #800080;">5</span>), findfs(<span style="color: #800080;">8</span>), mount(<span style="color: #800080;">8</span>) and/or blkid(<span style="color: #800080;">8</span>) <span style="color: #0000ff;">for</span><span style="color: #000000;"> more info
#
</span>/dev/mapper/centos-root /                       xfs     defaults        <span style="color: #800080;">0</span> <span style="color: #800080;">0</span><span style="color: #000000;">
UUID</span>=1c4160c0-<span style="color: #800080;">2579</span>-4b50-b4b8-dcf66caf05ec /boot                   xfs     defaults        <span style="color: #800080;">0</span> <span style="color: #800080;">0</span>
/dev/mapper/centos-home /home                   xfs     defaults        <span style="color: #800080;">0</span> <span style="color: #800080;">0</span>
/dev/mapper/centos-swap swap                    swap    defaults        <span style="color: #800080;">0</span> <span style="color: #800080;">0</span>
<span style="color: #008000;">//</span><span style="color: #008000;">192.168.0.140/database /database cifs credentials=/root/auth.smb 0 0</span>
<span style="color: #800080;">192.168</span>.<span style="color: #800080;">0.140</span>:/nfsfile /nfsfile nfs defaults <span style="color: #800080;">0</span> <span style="color: #800080;">0</span><span style="color: #000000;">
#UUID</span>=1a24d4e6-<span style="color: #800080;">6797</span>-4ff8-88cb-687d1876f4c4 /iscsi ext4 defaults <span style="color: #800080;">0</span> <span style="color: #800080;">0</span></pre>
</div>
<span class="cnblogs_code_collapse">vim /etc/fstab</span></div>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: rgba(22, 159, 230, 1);"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a15"></a>十五、使用MariaDB数据库管理系统</span></strong></span></p>
<p><strong>&nbsp;1，安装MariaDB</strong></p>
<p>①安装</p>
<p>&nbsp;&nbsp;<span class="cnblogs_code">yum install mariadb mariadb-serve</span>&nbsp;</p>
<p>&nbsp;&nbsp;<span class="cnblogs_code">systemctl start mariadb</span>&nbsp;</p>
<p>&nbsp;&nbsp;<span class="cnblogs_code">systemctl enable mariadb</span>&nbsp;</p>
<p>②在确认MariaDB数据库软件程序安装完毕启动后请不要立即使用，需要先初始化</p>
<p>&nbsp;<span class="cnblogs_code">mysql_secure_installation</span>&nbsp;初始化命令</p>
<p>空格（当前数据库密码为空，直接空格）-y（设置root密码）-y（删除匿名账户）-y（禁止root管理员从远程登录）-y（删除test数据库并取消对它的访问）-y（刷新授权表，让初始化后的设定立即生效）</p>
<p>③设置防火墙，使其放行对数据库服务程序的访问请求，数据库服务程序默认会占用3306端口，在防火墙策略中服务名称统一叫做mysql</p>
<p>&nbsp;<span class="cnblogs_code">firewall-cmd --permanent --add-service=mysql</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">firewall-cmd --reload</span>&nbsp;</p>
<p>④登录mysql</p>
<p>&nbsp;<span class="cnblogs_code">mysql -u root -p</span>&nbsp;</p>
<p><strong>2，MariaDB基本命令</strong></p>
<p>&nbsp;<span class="cnblogs_code">MariaDB [(none)]&gt; <span style="color: #0000ff;">set</span> password = PASSWORD(<span style="color: #800000;">'</span><span style="color: #800000;">123456</span><span style="color: #800000;">'</span>);</span>&nbsp;修改密码</p>
<p>&nbsp;<span class="cnblogs_code">MariaDB [(none)]&gt; show databases;</span>&nbsp;查询数据库</p>
<p>&nbsp;</p>
<p><strong>3，管理账户以及授权</strong></p>
<p>&nbsp;<span class="cnblogs_code">MariaDB [(none)]&gt; CREATE USER hunter@localhost IDENTIFIEd BY <span style="color: #800000;">'</span><span style="color: #800000;">123456</span><span style="color: #800000;">'</span>;</span>&nbsp;创建账户hunter 密码123456</p>
<p>&nbsp;<span class="cnblogs_code">use mysql;</span>&nbsp;切换到mysql数据库</p>
<p>&nbsp;<span class="cnblogs_code"><span style="color: #0000ff;">select</span> * <span style="color: #0000ff;">from</span> user <span style="color: #0000ff;">where</span> user=<span style="color: #800000;">"</span><span style="color: #800000;">hunter</span><span style="color: #800000;">"</span>;</span>&nbsp;查询用户信息</p>
<table style="height: 81px; width: 728px;" border="0"><caption>GRANT命令常见格式以及解释</caption>
<tbody>
<tr>
<td>命令</td>
<td>作用</td>
</tr>
<tr>
<td>GRANT 权限 ON 数据库.表单名称 TO 账户名@主机名</td>
<td>对某个特定数据库中的特定表单给予授权</td>
</tr>
<tr>
<td>GRANT 权限 ON 数据库.* TO 账户名@主机名</td>
<td>对某个特定数据库中的所有表单给予授权</td>
</tr>
<tr>
<td>GRANT 权限 ON *.* TO 账户名@主机名</td>
<td>对所有数据库以及所有的表单给予授权</td>
</tr>
<tr>
<td>GRANT 权限1,权限2 ON 数据.* TO 账户名@主机名</td>
<td>对某个数据库的所有表单给予多个授权</td>
</tr>
<tr>
<td>GRANT ALL PRIVILEGES ON *.* TO 账户名@主机名</td>
<td>对所有数据库及所有表单给予全部授权（需谨慎操作）</td>
</tr>
</tbody>
</table>
<p>&nbsp;<span class="cnblogs_code">GRANT SELECT,UPDATE,DELETE,INSERT ON mysql.user TO hunter@localhost;</span>&nbsp;给hunter账户设置mysql数据库的user表的增删查改操作</p>
<p>&nbsp;<span class="cnblogs_code">REVOKE SELECT,UPDATE,DELETE,INSERT ON mysql.user FROM hunter@localhost;</span>&nbsp;移除hunter账户的权限</p>
<p>&nbsp;<span class="cnblogs_code">MariaDB [mysql]&gt; SHOW GRANTS FOR hunter@localhost;</span>&nbsp;查询hunter账户的权限</p>
<p>&nbsp;<span class="cnblogs_code">update user <span style="color: #0000ff;">set</span> host=<span style="color: #800000;">'</span><span style="color: #800000;">%</span><span style="color: #800000;">'</span> <span style="color: #0000ff;">where</span> user=<span style="color: #800000;">'</span><span style="color: #800000;">hunter</span><span style="color: #800000;">'</span>;</span>&nbsp;修改host允许其他服务器访问</p>
<p>&nbsp;<span class="cnblogs_code">GRANT SELECT,UPDATE,DELETE,INSERT ON *.* To <span style="color: #800000;">'</span><span style="color: #800000;">hunter</span><span style="color: #800000;">'</span>@<span style="color: #800000;">'</span><span style="color: #800000;">%</span><span style="color: #800000;">'</span>;</span>&nbsp;设置访问权限</p>
<p>&nbsp;</p>
<p><strong>4，创建数据库与表单</strong></p>
<p>&nbsp;<span class="cnblogs_code">create database project;</span>&nbsp;创建数据库</p>
<p>&nbsp;<span class="cnblogs_code">use project;</span>&nbsp;切换到project数据库</p>
<p>&nbsp;<span class="cnblogs_code">create table mybook(id bigint,name varchar(<span style="color: #800080;">20</span>));</span>&nbsp;创建表</p>
<p>&nbsp;<span class="cnblogs_code">show tables;</span>&nbsp;查询所有表</p>
<p>&nbsp;<span class="cnblogs_code">insert into mybook values(<span style="color: #800080;">1</span>,<span style="color: #800000;">"</span><span style="color: #800000;">1</span><span style="color: #800000;">"</span>);</span>&nbsp;插入数据</p>
<p>&nbsp;<span class="cnblogs_code">drop database project;</span>&nbsp;删除数据库</p>
<p><strong>5，数据库的备份及恢复</strong></p>
<p>&nbsp;<span class="cnblogs_code">mysqldump -u root -p project &gt; /root/projectDB.dump</span>&nbsp;创建备份</p>
<p>&nbsp;<span class="cnblogs_code">mysql -u root -p project &lt; /root/projectDB.dump</span>&nbsp;恢复数据库（需要先把project数据库创建出来&nbsp;<span class="cnblogs_code">create database project;</span>&nbsp;）</p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: rgba(22, 159, 230, 1);"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a16"></a>十六、使用LNMP架构部署动态网站环境</span></strong></span></p>
<p><strong>1，使用源码包安装步骤</strong></p>
<p>①下载及解压源码包文件</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">tar zxvf FileName.tar.gz
cd FileNameDirectory</span></pre>
</div>
<p>②编译源码包代码。（--prefix指定源码包安装路径）。如果没什么问题会在当前目录下生成一个Makefile安装文件</p>
<div class="cnblogs_code">
<pre>./configure --prefix=/usr/local/program</pre>
</div>
<p>③生成二进制安装程序。刚刚生成的Makefile文件中会保存有关系统环境、软件依赖关系和安装规则等内容，接下来便可以使用make命令来根据Makefile文件内容提供的合适规则编译生成出可供用户安装服务程序的二进制可执行文件</p>
<div class="cnblogs_code">
<pre>make</pre>
</div>
<p>④运行二进制的服务程序安装包。由于不需要再检查系统环境，也不需要再编译代码，因此允许二进制的服务程序安装包应该是速度最快的步骤。如果在源码包编译阶段使用了--prefix参数，那么此时服务程序就会被安装到那个目录，如果没有自行使用参数定义目录的话，一般会被默认安装到/usr/local/bin目录中</p>
<div class="cnblogs_code">
<pre>make install</pre>
</div>
<p>&nbsp;</p>
<p><strong>2，安装必要的软件包</strong></p>
<p>&nbsp;yum install -y apr* autoconf automake bison bzip2 bzip2* compat* cpp curl curl-devel fontconfig fontconfig-devel freetype freetype* freetype-devel gcc gcc-c++ gd gettext gettext-devel glibc kernel kernel-headers keyutils keyutils-libs-devel krb5-devel libcom_err-devel libpng libpng-devel libjpeg* libsepol-devel libselinux-devel libstdc++-devel libtool* libgomp libxml2 libxml2-devel libXpm* libtiff libtiff* make mpfr ncurses* ntp openssl openssl-devel patch pcre-devel perl php-common php-gd policycoreutils telnet t1lib t1lib* nasm nasm* wget zlib-devel</p>
<p>&nbsp;</p>
<p><strong>3，下载所需的16个软件源码包和1个用于检测效果的论坛网站系统软件</strong>&nbsp;</p>
<table style="height: 543px; width: 1053px;" border="0">
<tbody>
<tr>
<td>包</td>
<td>说明</td>
</tr>
<tr>
<td>wget https://www.linuxprobe.com/Software/cmake-2.8.11.2.tar.gz</td>
<td>CMake是Liunx系统中常用的编译工具</td>
</tr>
<tr>
<td>wget https://www.linuxprobe.com/Software/Discuz_X3.2_SC_GBK.zip</td>
<td>&nbsp;论坛源码包</td>
</tr>
<tr>
<td>wget https://www.linuxprobe.com/Software/freetype-2.5.3.tar.gz</td>
<td>&nbsp;用于提供字体支持引擎的服务程序</td>
</tr>
<tr>
<td>wget https://www.linuxprobe.com/Software/jpegsrc.v9a.tar.gz</td>
<td>&nbsp;用于提供jpeg图片格式支持函数库的服务程序</td>
</tr>
<tr>
<td>wget https://www.linuxprobe.com/Software/libgd-2.1.0.tar.gz</td>
<td>&nbsp;用于提供图形处理的服务程序</td>
</tr>
<tr>
<td>wget https://www.linuxprobe.com/Software/libmcrypt-2.5.8.tar.gz</td>
<td>&nbsp;用于加密算法的扩展库程序</td>
</tr>
<tr>
<td>wget https://www.linuxprobe.com/Software/libpng-1.6.12.tar.gz</td>
<td>&nbsp;用于提供png图片格式支持函数库的服务程序</td>
</tr>
<tr>
<td>wget https://www.linuxprobe.com/Software/libvpx-v1.3.0.tar.bz2</td>
<td>&nbsp;用于提供视频编码器的服务程序</td>
</tr>
<tr>
<td>wget https://www.linuxprobe.com/Software/mysql-5.6.19.tar.gz</td>
<td>&nbsp;mysql源码包</td>
</tr>
<tr>
<td>wget https://www.linuxprobe.com/Software/nginx-1.6.0.tar.gz</td>
<td>&nbsp;部署动态网站的轻量级服务程序</td>
</tr>
<tr>
<td>wget https://www.linuxprobe.com/Software/openssl-1.0.1h.tar.gz</td>
<td>&nbsp;用于提供网站证书服务的程序文件</td>
</tr>
<tr>
<td>wget https://www.linuxprobe.com/Software/php-5.5.14.tar.gz</td>
<td>&nbsp;php服务源码包</td>
</tr>
<tr>
<td>wget https://www.linuxprobe.com/Software/pcre-8.35.tar.gz</td>
<td>&nbsp;提供Perl语言兼容的正则表达式库的软件包</td>
</tr>
<tr>
<td>wget https://www.linuxprobe.com/Software/t1lib-5.1.2.tar.gz</td>
<td>&nbsp;用于提供图片生成函数库的服务程序</td>
</tr>
<tr>
<td>wget https://www.linuxprobe.com/Software/tiff-4.0.3.tar.gz</td>
<td>&nbsp;用于提供标签图像文件格式的服务程序</td>
</tr>
<tr>
<td>wget https://www.linuxprobe.com/Software/yasm-1.2.0.tar.gz</td>
<td>&nbsp;是一款常见的开源汇编器</td>
</tr>
<tr>
<td>wget https://www.linuxprobe.com/Software/zlib-1.2.8.tar.gz</td>
<td>&nbsp;用于提供压缩功能的函数文件</td>
</tr>
</tbody>
</table>
<p>①安装cmake</p>
<div class="cnblogs_code">
<pre>tar zxvf cmake-<span style="color: #800080;">2.8</span>.<span style="color: #800080;">11.2</span><span style="color: #000000;">.tar.gz
cd cmake</span>-<span style="color: #800080;">2.8</span>.<span style="color: #800080;">11.2</span>/<span style="color: #000000;">
.</span>/<span style="color: #000000;">configure
make
make install</span></pre>
</div>
<p>&nbsp;</p>
<p><strong>4，安装mysql</strong></p>
<p>&nbsp;①在系统里面创建一个mysql的用户</p>
<p>&nbsp;<span class="cnblogs_code">useradd mysql -s /sbin/nologin</span>&nbsp;</p>
<p>&nbsp;②创建一个用于保存mysql数据库程序文件的目录</p>
<p>&nbsp;<span class="cnblogs_code">mkdir -p /usr/local/mysql/<span style="color: #0000ff;">var</span></span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">chown -Rf mysql:mysql /usr/local/mysql</span>&nbsp;</p>
<p>③解压、编译、安装Mysql数据库服务程序</p>
<p>&nbsp;<span class="cnblogs_code">tar xzvf mysql-<span style="color: #800080;">5.6</span>.<span style="color: #800080;">19</span>.tar.gz</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">cd mysql-<span style="color: #800080;">5.6</span>.<span style="color: #800080;">19</span>/</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">cmake . -DCMAKE_INSTALL_PREFIX=/usr/local/mysql -DMYSQL_DATADIR=/usr/local/mysql/<span style="color: #0000ff;">var</span> -DSYSCONFDIR=/etc</span>&nbsp;</p>
<ul>
<li><span style="font-size: 12px;">在编译数据库时使用cmake命令</span></li>
<li><span style="font-size: 12px;">-DCMAKE_INSTALL_PREFIX=/usr/local/mysql&nbsp;参数用于定义数据库服务程序的保存目录</span></li>
<li><span style="font-size: 12px;">-DMYSQL_DATADIR=/usr/local/mysql/var 参数用于定义真实数据库文件的目录</span></li>
<li><span style="font-size: 12px;">-DSYSCONFDIR=/etc 定义mysql数据库配置文件的保存目录</span></li>
</ul>
<p>&nbsp;<span class="cnblogs_code">make</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">make install</span>&nbsp;</p>
<p>④生成新的配置文件</p>
<p>&nbsp;<span class="cnblogs_code">rm -rf /etc/my.cnf</span>&nbsp;删除默认配置文件</p>
<p>&nbsp;<span class="cnblogs_code">cd /usr/local/mysql</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">./scripts/mysql_install_db --user=mysql --basedir=/usr/local/mysql --datadir=/usr/local/mysql/<span style="color: #0000ff;">var</span></span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">ln -s&nbsp;/usr/local/mysql/my.cnf /etc/my.cnf</span>&nbsp;</p>
<p>⑤把程序目录中的开机程序文件复制到/etc/rc.d/init.d目录中，以便service命令来管理MySql数据库服务程序。需要把数据库脚本文件权限修改为755以便让用户有执行该脚本的权限</p>
<p>&nbsp;<span class="cnblogs_code">cp ./support-files/mysql.server /etc/rc.d/init.d/mysqld</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">chmod <span style="color: #800080;">755</span> /etc/rc.d/init.d/mysqld</span>&nbsp;</p>
<p>⑥修改mysqld数据库脚本文件basedir和datadir</p>
<div class="cnblogs_code">
<pre>[root@linuxprobe mysql]# vim /etc/rc.d/init.d/<span style="color: #000000;">mysqld 
&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;省略部分输出信息&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;
 </span><span style="color: #800080;">39</span><span style="color: #000000;"> #
 </span><span style="color: #800080;">40</span><span style="color: #000000;"> # If you want to affect other MySQL variables, you should make your changes
 </span><span style="color: #800080;">41</span> # <span style="color: #0000ff;">in</span> the /etc/my.cnf, ~/<span style="color: #000000;">.my.cnf or other MySQL configuration files.
 </span><span style="color: #800080;">42</span> 
 <span style="color: #800080;">43</span> # If you change <span style="color: #0000ff;">base</span> dir, you must also change datadir. These may <span style="color: #0000ff;">get</span>
 <span style="color: #800080;">44</span> # overwritten by settings <span style="color: #0000ff;">in</span><span style="color: #000000;"> the MySQL configuration files.
 </span><span style="color: #800080;">45</span> 
 <span style="color: #800080;">46</span> basedir=/usr/local/<span style="color: #000000;">mysql
 </span><span style="color: #800080;">47</span> datadir=/usr/local/mysql/<span style="color: #0000ff;">var</span>
 <span style="color: #800080;">48</span><span style="color: #000000;"> 
&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;省略部分输出信息&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;</span></pre>
</div>
<p>⑦启动服务并加入开机启动</p>
<p>&nbsp;<span class="cnblogs_code">service mysqld start</span>&nbsp;启动服务</p>
<p>&nbsp;<span class="cnblogs_code">chkconfig mysqld on</span>&nbsp;加入开机启动</p>
<p>⑧将mysql命令加入到BASH</p>
<p>&nbsp;<span class="cnblogs_code">vim /etc/profile</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">export PATH=$PATH:/usr/local/mysql/bin</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">source /etc/profile</span>&nbsp;立即生效</p>
<p>&nbsp;⑨MySQL数据库服务程序还会调用到一些程序文件和函数库文件。由于当前是通过源码包方式安装MySQL数据库，因此现在也必须以手动方式把这些文件链接过来。</p>
<p>&nbsp;<span class="cnblogs_code">mkdir /<span style="color: #0000ff;">var</span>/lib/mysql</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">ln -s /usr/local/mysql/lib/mysql /<span style="color: #0000ff;">var</span>/lib/mysql/</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">ln -s /tmp/mysql.sock /<span style="color: #0000ff;">var</span>/lib/mysql/mysql.sock</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">ln -s /usr/local/mysql/include/mysql /usr/include/mysql</span>&nbsp;</p>
<p>⑩mysql_secure_installation对MySQL数据库进行初始化</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">[root@linuxprobe mysql]# mysql_secure_installation 
NOTE: RUNNING ALL PARTS OF THIS SCRIPT IS RECOMMENDED FOR ALL MySQL
      SERVERS IN PRODUCTION USE</span>!  PLEASE READ EACH STEP CAREFULLY!<span style="color: #000000;">
In order to log into MySQL to secure it, we</span><span style="color: #800000;">'</span><span style="color: #800000;">ll need the current</span>
password <span style="color: #0000ff;">for</span> the root user.  If you<span style="color: #800000;">'</span><span style="color: #800000;">ve just installed MySQL, and</span>
you haven<span style="color: #800000;">'</span><span style="color: #800000;">t set the root password yet, the password will be blank,</span>
<span style="color: #000000;">so you should just press enter here.
Enter current password </span><span style="color: #0000ff;">for</span> root (enter <span style="color: #0000ff;">for</span><span style="color: #000000;"> none): 此处只需按下回车键
OK, successfully used password, moving on...
Setting the root password ensures that nobody can log into the MySQL
root user without the proper authorisation.
Set root password</span>? [Y/<span style="color: #000000;">n] y （要为root管理员设置数据库的密码）
New password: 输入要为root管理员设置的数据库密码
Re</span>-enter <span style="color: #0000ff;">new</span><span style="color: #000000;"> password: 再输入一次密码
Password updated successfully</span>!<span style="color: #000000;">
Reloading privilege tables..
 ... Success</span>!<span style="color: #000000;">
By </span><span style="color: #0000ff;">default</span><span style="color: #000000;">, a MySQL installation has an anonymous user, allowing anyone
to log into MySQL without having to have a user account created </span><span style="color: #0000ff;">for</span><span style="color: #000000;">
them.  This </span><span style="color: #0000ff;">is</span> intended only <span style="color: #0000ff;">for</span><span style="color: #000000;"> testing, and to make the installation
go a bit smoother.  You should remove them before moving into a
production environment.
Remove anonymous users</span>? [Y/<span style="color: #000000;">n] y （删除匿名账户）
 ... Success</span>!<span style="color: #000000;">
Normally, root should only be allowed to connect </span><span style="color: #0000ff;">from</span> <span style="color: #800000;">'</span><span style="color: #800000;">localhost</span><span style="color: #800000;">'</span><span style="color: #000000;">.  This
ensures that someone cannot guess at the root password </span><span style="color: #0000ff;">from</span><span style="color: #000000;"> the network.
Disallow root login remotely</span>? [Y/<span style="color: #000000;">n] y （禁止root管理员从远程登录）
 ... Success</span>!<span style="color: #000000;">
By </span><span style="color: #0000ff;">default</span>, MySQL comes with a database named <span style="color: #800000;">'</span><span style="color: #800000;">test</span><span style="color: #800000;">'</span><span style="color: #000000;"> that anyone can
access.  This </span><span style="color: #0000ff;">is</span> also intended only <span style="color: #0000ff;">for</span><span style="color: #000000;"> testing, and should be removed
before moving into a production environment.
Remove test database and access to it</span>? [Y/<span style="color: #000000;">n] y （删除test数据库并取消对其的访问权限）
 </span>-<span style="color: #000000;"> Dropping test database...
 ... Success</span>!
 -<span style="color: #000000;"> Removing privileges on test database...
 ... Success</span>!<span style="color: #000000;">
Reloading the privilege tables will ensure that all changes made so far
will take effect immediately.
Reload privilege tables now</span>? [Y/<span style="color: #000000;">n] y （刷新授权表，让初始化后的设定立即生效）
 ... Success</span>!<span style="color: #000000;">
All done</span>!  If you<span style="color: #800000;">'</span><span style="color: #800000;">ve completed all of the above steps, your MySQL</span>
<span style="color: #000000;">installation should now be secure.
Thanks </span><span style="color: #0000ff;">for</span> <span style="color: #0000ff;">using</span> MySQL!<span style="color: #000000;">
Cleaning up...</span></pre>
</div>
<p>&nbsp;</p>
<p><strong>5，安装Nginx服务</strong></p>
<p>①安装pcre</p>
<p>&nbsp;<span class="cnblogs_code">cd /usr/local/src/</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">tar zxvf pcre-<span style="color: #800080;">8.35</span>.tar.gz</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">cd pcre-<span style="color: #800080;">8.35</span>/</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">./configure --prefix=/usr/local/pcre</span>&nbsp;程序安装在/usr/local/pcre目录</p>
<p>&nbsp;<span class="cnblogs_code">make</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">make install</span>&nbsp;</p>
<p>②安装openssl</p>
<p>&nbsp;<span class="cnblogs_code">cd /usr/local/src/</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">tar zxvf openssl-<span style="color: #800080;">1.0</span>.1h.tar.gz</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">cd openssl-<span style="color: #800080;">1.0</span>.1h/</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">./config --prefix=/usr/local/openssl</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">make</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">make install</span>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('745fa7b6-42e7-4d38-bf17-90cef97ebfc1')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_745fa7b6-42e7-4d38-bf17-90cef97ebfc1" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_745fa7b6-42e7-4d38-bf17-90cef97ebfc1" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_745fa7b6-42e7-4d38-bf17-90cef97ebfc1" class="cnblogs_code_hide">
<pre><span style="color: #000000;">...
done
export PATH</span>=$PATH:/usr/local/mysql/bin;usr/local/openssl/<span style="color: #000000;">bin
unset i
unset </span>-f pathmunge</pre>
</div>
<span class="cnblogs_code_collapse">vim /etc/profile</span></div>
<p>&nbsp;<span class="cnblogs_code">source /etc/profile</span>&nbsp;</p>
<p>③安装zlib</p>
<p>&nbsp;<span class="cnblogs_code">cd /usr/local/src/</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">tar zxvf zlib-<span style="color: #800080;">1.2</span>.<span style="color: #800080;">8</span>.tar.gz</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">cd zlib-<span style="color: #800080;">1.2</span>.<span style="color: #800080;">8</span>/</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">./configure --prefix=/usr/local/zlib</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">make</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">make install</span>&nbsp;</p>
<p>④安装nginx</p>
<p>&nbsp;<span class="cnblogs_code">useradd www -s /sbin/nologin</span>&nbsp;创建一个用于执行nginx服务程序的账户</p>
<p>&nbsp;<span class="cnblogs_code">cd /usr/local/src/</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">tar zxvf nginx-<span style="color: #800080;">1.6</span>.<span style="color: #800080;">0</span>.tar.gz</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">cd nginx-<span style="color: #800080;">1.6</span>.<span style="color: #800080;">0</span>/</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">./configure --prefix=/usr/local/nginx --without-http_memcached_module --user=www --group=www --with-http_stub_status_module --with-http_ssl_module --with-http_gzip_static_module --with-openssl=/usr/local/src/openssl-<span style="color: #800080;">1.0</span>.1h --with-zlib=/usr/local/src/zlib-<span style="color: #800080;">1.2</span>.<span style="color: #800080;">8</span> --with-pcre=/usr/local/src/pcre-<span style="color: #800080;">8.35</span></span>&nbsp;</p>
<ul>
<li><span style="font-size: 12px;">--prefix=/usr/local/nginx 定义服务程序稍后安装的位置</span></li>
<li><span style="font-size: 12px;">--user=www --group=www 指定执行nginx服务程序的用户名和用户组</span></li>
<li><span style="font-size: 12px;">在使用参数调用openssl、zlid、pcre软件包时，请指定软件源码包的解压路径，而不是程序的安装路径</span></li>
</ul>
<p>&nbsp;<span class="cnblogs_code">make</span>&nbsp;</p>
<p>&nbsp;<span class="cnblogs_code">make install</span>&nbsp;</p>
<p>想要启动nginx服务程序以及将其加入到开启启动项中，需要脚本文件，需要自己编写：</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('51d0a66a-bb72-4621-a596-da813ead8805')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_51d0a66a-bb72-4621-a596-da813ead8805" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_51d0a66a-bb72-4621-a596-da813ead8805" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_51d0a66a-bb72-4621-a596-da813ead8805" class="cnblogs_code_hide">
<pre>#!/bin/<span style="color: #000000;">bash
# nginx </span>- <span style="color: #0000ff;">this</span><span style="color: #000000;"> script starts and stops the nginx daemon
# chkconfig: </span>- <span style="color: #800080;">85</span> <span style="color: #800080;">15</span><span style="color: #000000;">
# description: Nginx </span><span style="color: #0000ff;">is</span><span style="color: #000000;"> an HTTP(S) server, HTTP(S) reverse \
# proxy and IMAP</span>/<span style="color: #000000;">POP3 proxy server
# processname: nginx
# config: </span>/etc/nginx/<span style="color: #000000;">nginx.conf
# config: </span>/usr/local/nginx/conf/<span style="color: #000000;">nginx.conf
# pidfile: </span>/usr/local/nginx/logs/<span style="color: #000000;">nginx.pid
# Source function library.
. </span>/etc/rc.d/init.d/<span style="color: #000000;">functions
# Source networking configuration.
. </span>/etc/sysconfig/<span style="color: #000000;">network
# Check that networking </span><span style="color: #0000ff;">is</span><span style="color: #000000;"> up.
[ </span><span style="color: #800000;">"</span><span style="color: #800000;">$NETWORKING</span><span style="color: #800000;">"</span> = <span style="color: #800000;">"</span><span style="color: #800000;">no</span><span style="color: #800000;">"</span> ] &amp;&amp; exit <span style="color: #800080;">0</span><span style="color: #000000;">
nginx</span>=<span style="color: #800000;">"</span><span style="color: #800000;">/usr/local/nginx/sbin/nginx</span><span style="color: #800000;">"</span><span style="color: #000000;">
prog</span>=<span style="color: #000000;">$(basename $nginx)
NGINX_CONF_FILE</span>=<span style="color: #800000;">"</span><span style="color: #800000;">/usr/local/nginx/conf/nginx.conf</span><span style="color: #800000;">"</span><span style="color: #000000;">
[ </span>-f /etc/sysconfig/nginx ] &amp;&amp; . /etc/sysconfig/<span style="color: #000000;">nginx
lockfile</span>=/<span style="color: #0000ff;">var</span>/<span style="color: #0000ff;">lock</span>/subsys/<span style="color: #000000;">nginx
make_dirs() {
# make required directories
user</span>=`$nginx -V <span style="color: #800080;">2</span>&gt;&amp;<span style="color: #800080;">1</span> | grep <span style="color: #800000;">"</span><span style="color: #800000;">configure arguments:</span><span style="color: #800000;">"</span> | sed <span style="color: #800000;">'</span><span style="color: #800000;">s/[^*]*--user=\([^ ]*\).*/\1/g</span><span style="color: #800000;">'</span> -<span style="color: #000000;">`
        </span><span style="color: #0000ff;">if</span> [ -z <span style="color: #800000;">"</span><span style="color: #800000;">`grep $user /etc/passwd`</span><span style="color: #800000;">"</span><span style="color: #000000;"> ]; then
                useradd </span>-M -s /bin/<span style="color: #000000;">nologin $user
        fi
options</span>=`$nginx -V <span style="color: #800080;">2</span>&gt;&amp;<span style="color: #800080;">1</span> | grep <span style="color: #800000;">'</span><span style="color: #800000;">configure arguments:</span><span style="color: #800000;">'</span><span style="color: #000000;">`
</span><span style="color: #0000ff;">for</span> opt <span style="color: #0000ff;">in</span> $options; <span style="color: #0000ff;">do</span>
        <span style="color: #0000ff;">if</span> [ `echo $opt | grep <span style="color: #800000;">'</span><span style="color: #800000;">.*-temp-path</span><span style="color: #800000;">'</span><span style="color: #000000;">` ]; then
                value</span>=`echo $opt | cut -d <span style="color: #800000;">"</span><span style="color: #800000;">=</span><span style="color: #800000;">"</span> -f <span style="color: #800080;">2</span><span style="color: #000000;">`
                </span><span style="color: #0000ff;">if</span> [ ! -d <span style="color: #800000;">"</span><span style="color: #800000;">$value</span><span style="color: #800000;">"</span><span style="color: #000000;"> ]; then
                        # echo </span><span style="color: #800000;">"</span><span style="color: #800000;">creating</span><span style="color: #800000;">"</span><span style="color: #000000;"> $value
                        mkdir </span>-p $value &amp;&amp; chown -<span style="color: #000000;">R $user $value
                fi
        fi
done
}
start() {
[ </span>-x $nginx ] || exit <span style="color: #800080;">5</span><span style="color: #000000;">
[ </span>-f $NGINX_CONF_FILE ] || exit <span style="color: #800080;">6</span><span style="color: #000000;">
make_dirs
echo </span>-n $<span style="color: #800000;">"</span><span style="color: #800000;">Starting $prog: </span><span style="color: #800000;">"</span><span style="color: #000000;">
daemon $nginx </span>-<span style="color: #000000;">c $NGINX_CONF_FILE
retval</span>=$?<span style="color: #000000;">
echo
[ $retval </span>-eq <span style="color: #800080;">0</span> ] &amp;&amp;<span style="color: #000000;"> touch $lockfile
</span><span style="color: #0000ff;">return</span><span style="color: #000000;"> $retval
}
stop() {
echo </span>-n $<span style="color: #800000;">"</span><span style="color: #800000;">Stopping $prog: </span><span style="color: #800000;">"</span><span style="color: #000000;">
killproc $prog </span>-<span style="color: #000000;">QUIT
retval</span>=$?<span style="color: #000000;">
echo
[ $retval </span>-eq <span style="color: #800080;">0</span> ] &amp;&amp; rm -<span style="color: #000000;">f $lockfile
</span><span style="color: #0000ff;">return</span><span style="color: #000000;"> $retval
}
restart() {
#configtest </span>|| <span style="color: #0000ff;">return</span> $?<span style="color: #000000;">
stop
sleep </span><span style="color: #800080;">1</span><span style="color: #000000;">
start
}
reload() {
#configtest </span>|| <span style="color: #0000ff;">return</span> $?<span style="color: #000000;">
echo </span>-n $<span style="color: #800000;">"</span><span style="color: #800000;">Reloading $prog: </span><span style="color: #800000;">"</span><span style="color: #000000;">
killproc $nginx </span>-<span style="color: #000000;">HUP
RETVAL</span>=$?<span style="color: #000000;">
echo
}
force_reload() {
restart
}
configtest() {
$nginx </span>-t -<span style="color: #000000;">c $NGINX_CONF_FILE
}
rh_status() {
status $prog
}
rh_status_q() {
rh_status </span>&gt;/dev/<span style="color: #0000ff;">null</span> <span style="color: #800080;">2</span>&gt;&amp;<span style="color: #800080;">1</span><span style="color: #000000;">
}
</span><span style="color: #0000ff;">case</span> <span style="color: #800000;">"</span><span style="color: #800000;">$1</span><span style="color: #800000;">"</span> <span style="color: #0000ff;">in</span><span style="color: #000000;">
start)
        rh_status_q </span>&amp;&amp; exit <span style="color: #800080;">0</span><span style="color: #000000;">
        $</span><span style="color: #800080;">1</span><span style="color: #000000;">
        ;;
stop)
        rh_status_q </span>|| exit <span style="color: #800080;">0</span><span style="color: #000000;">
        $</span><span style="color: #800080;">1</span><span style="color: #000000;">
        ;;
restart</span>|<span style="color: #000000;">configtest)
$</span><span style="color: #800080;">1</span><span style="color: #000000;">
;;
reload)
        rh_status_q </span>|| exit <span style="color: #800080;">7</span><span style="color: #000000;">
        $</span><span style="color: #800080;">1</span><span style="color: #000000;">
        ;;
force</span>-<span style="color: #000000;">reload)
        force_reload
        ;;
status)
        rh_status
        ;;
condrestart</span>|<span style="color: #0000ff;">try</span>-<span style="color: #000000;">restart)
        rh_status_q </span>|| exit <span style="color: #800080;">0</span><span style="color: #000000;">
        ;;
</span>*<span style="color: #000000;">)
echo $</span><span style="color: #800000;">"</span><span style="color: #800000;">Usage: $0 {start|stop|status|restart|condrestart|try-restart|reload|force-reload|configtest}</span><span style="color: #800000;">"</span><span style="color: #000000;">
exit </span><span style="color: #800080;">2</span><span style="color: #000000;">
esac</span></pre>
</div>
<span class="cnblogs_code_collapse">vim /etc/rc.d/init.d/nginx</span></div>
<p>&nbsp;<span class="cnblogs_code">chmod <span style="color: #800080;">755</span> /etc/rc.d/init.d/nginx</span>&nbsp;设置755以便能执行这个脚本</p>
<p>&nbsp;<span class="cnblogs_code">/etc/rc.d/init.d/nginx restart</span>&nbsp;重启nginx服务程序</p>
<p>&nbsp;<span class="cnblogs_code">chkconfig nginx on</span>&nbsp;加入开机启动</p>
<p>&nbsp;<span class="cnblogs_code">iptables -F</span>&nbsp;</p>
<p>&nbsp;</p>
<p><strong>6，配置php服务</strong></p>
<p>①yasm源码包是一款常见的开源汇编器</p>
<div class="cnblogs_code">
<pre>[root@linuxprobe nginx-<span style="color: #800080;">1.6</span>.<span style="color: #800080;">0</span><span style="color: #000000;">]# cd ..
[root@linuxprobe src]# </span><span style="color: #0000ff;">tar</span> zxvf yasm-<span style="color: #800080;">1.2</span>.<span style="color: #800080;">0</span>.<span style="color: #0000ff;">tar</span><span style="color: #000000;">.gz
[root@linuxprobe src]# cd yasm</span>-<span style="color: #800080;">1.2</span>.<span style="color: #800080;">0</span><span style="color: #000000;">
[root@linuxprobe yasm</span>-<span style="color: #800080;">1.2</span>.<span style="color: #800080;">0</span>]# ./<span style="color: #000000;">configure
[root@linuxprobe yasm</span>-<span style="color: #800080;">1.2</span>.<span style="color: #800080;">0</span>]# <span style="color: #0000ff;">make</span><span style="color: #000000;">
[root@linuxprobe yasm</span>-<span style="color: #800080;">1.2</span>.<span style="color: #800080;">0</span>]# <span style="color: #0000ff;">make</span> <span style="color: #0000ff;">install</span></pre>
</div>
<p>②libmcrypt源码包是用于加密算法的扩展库程序</p>
<div class="cnblogs_code">
<pre>[root@linuxprobe yasm-<span style="color: #800080;">1.2</span>.<span style="color: #800080;">0</span><span style="color: #000000;">]# cd ..
[root@linuxprobe src]# </span><span style="color: #0000ff;">tar</span> zxvf libmcrypt-<span style="color: #800080;">2.5</span>.<span style="color: #800080;">8</span>.<span style="color: #0000ff;">tar</span><span style="color: #000000;">.gz
[root@linuxprobe src]# cd libmcrypt</span>-<span style="color: #800080;">2.5</span>.<span style="color: #800080;">8</span><span style="color: #000000;">
[root@linuxprobe libmcrypt</span>-<span style="color: #800080;">2.5</span>.<span style="color: #800080;">8</span>]# ./<span style="color: #000000;">configure
[root@linuxprobe libmcrypt</span>-<span style="color: #800080;">2.5</span>.<span style="color: #800080;">8</span>]# <span style="color: #0000ff;">make</span><span style="color: #000000;">
[root@linuxprobe libmcrypt</span>-<span style="color: #800080;">2.5</span>.<span style="color: #800080;">8</span>]# <span style="color: #0000ff;">make</span> <span style="color: #0000ff;">install</span></pre>
</div>
<p>③libvpx源码包是用于提供视频编码器的服务程序。libvpx源码包的后缀是.tar.bz2，即表示使用bzip2格式进行的压缩，因此正确的解压参数应该是xjvf</p>
<div class="cnblogs_code">
<pre>[root@linuxprobe libmcrypt-<span style="color: #800080;">2.5</span>.<span style="color: #800080;">8</span><span style="color: #000000;">]# cd ..
[root@linuxprobe src]# </span><span style="color: #0000ff;">tar</span> xjvf libvpx-v1.<span style="color: #800080;">3.0</span>.<span style="color: #0000ff;">tar</span><span style="color: #000000;">.bz2
[root@linuxprobe src]# cd libvpx</span>-v1.<span style="color: #800080;">3.0</span><span style="color: #000000;">
[root@linuxprobe libvpx</span>-v1.<span style="color: #800080;">3.0</span>]# ./configure --prefix=/usr/local/libvpx --enable-shared --enable-<span style="color: #000000;">vp9
[root@linuxprobe libvpx</span>-v1.<span style="color: #800080;">3.0</span>]# <span style="color: #0000ff;">make</span><span style="color: #000000;">
[root@linuxprobe libvpx</span>-v1.<span style="color: #800080;">3.0</span>]# <span style="color: #0000ff;">make</span> <span style="color: #0000ff;">install</span></pre>
</div>
<p>④tiff源码包是用于提供标签图像文件格式的服务程序</p>
<div class="cnblogs_code">
<pre>[root@linuxprobe libvpx-v1.<span style="color: #800080;">3.0</span><span style="color: #000000;">]# cd ..
[root@linuxprobe src]# </span><span style="color: #0000ff;">tar</span> zxvf tiff-<span style="color: #800080;">4.0</span>.<span style="color: #800080;">3</span>.<span style="color: #0000ff;">tar</span><span style="color: #000000;">.gz
[root@linuxprobe src]# cd tiff</span>-<span style="color: #800080;">4.0</span>.<span style="color: #800080;">3</span><span style="color: #000000;">
[root@linuxprobe tiff</span>-<span style="color: #800080;">4.0</span>.<span style="color: #800080;">3</span>]# ./configure --prefix=/usr/local/tiff --enable-<span style="color: #000000;">shared
[root@linuxprobe tiff</span>-<span style="color: #800080;">4.0</span>.<span style="color: #800080;">3</span>]# <span style="color: #0000ff;">make</span><span style="color: #000000;">
[root@linuxprobe tiff</span>-<span style="color: #800080;">4.0</span>.<span style="color: #800080;">3</span>]# <span style="color: #0000ff;">make</span> <span style="color: #0000ff;">install</span></pre>
</div>
<p>⑤libpng源码包是用于提供png图片格式支持函数库的服务程序</p>
<div class="cnblogs_code">
<pre>[root@linuxprobe tiff-<span style="color: #800080;">4.0</span>.<span style="color: #800080;">3</span><span style="color: #000000;">]# cd ..
[root@linuxprobe src]# </span><span style="color: #0000ff;">tar</span> zxvf libpng-<span style="color: #800080;">1.6</span>.<span style="color: #800080;">12</span>.<span style="color: #0000ff;">tar</span><span style="color: #000000;">.gz
[root@linuxprobe src]# cd libpng</span>-<span style="color: #800080;">1.6</span>.<span style="color: #800080;">12</span><span style="color: #000000;">
[root@linuxprobe libpng</span>-<span style="color: #800080;">1.6</span>.<span style="color: #800080;">12</span>]# ./configure --prefix=/usr/local/libpng --enable-<span style="color: #000000;">shared
[root@linuxprobe libpng</span>-<span style="color: #800080;">1.6</span>.<span style="color: #800080;">12</span>]# <span style="color: #0000ff;">make</span><span style="color: #000000;">
[root@linuxprobe libpng</span>-<span style="color: #800080;">1.6</span>.<span style="color: #800080;">12</span>]# <span style="color: #0000ff;">make</span> <span style="color: #0000ff;">install</span></pre>
</div>
<p>⑥freetype源码包是用于提供字体支持引擎的服务程序</p>
<div class="cnblogs_code">
<pre>[root@linuxprobe libpng-<span style="color: #800080;">1.6</span>.<span style="color: #800080;">12</span><span style="color: #000000;">]# cd ..
[root@linuxprobe src]# </span><span style="color: #0000ff;">tar</span> zxvf freetype-<span style="color: #800080;">2.5</span>.<span style="color: #800080;">3</span>.<span style="color: #0000ff;">tar</span><span style="color: #000000;">.gz
[root@linuxprobe src]# cd freetype</span>-<span style="color: #800080;">2.5</span>.<span style="color: #800080;">3</span><span style="color: #000000;">
[root@linuxprobe freetype</span>-<span style="color: #800080;">2.5</span>.<span style="color: #800080;">3</span>]# ./configure --prefix=/usr/local/freetype --enable-<span style="color: #000000;">shared
[root@linuxprobe freetype</span>-<span style="color: #800080;">2.5</span>.<span style="color: #800080;">3</span>]# <span style="color: #0000ff;">make</span><span style="color: #000000;">
[root@linuxprobe freetype</span>-<span style="color: #800080;">2.5</span>.<span style="color: #800080;">3</span>]# <span style="color: #0000ff;">make</span> <span style="color: #0000ff;">install</span></pre>
</div>
<p>⑦jpeg源码包是用于提供jpeg图片格式支持函数库的服务程序</p>
<div class="cnblogs_code">
<pre>[root@linuxprobe freetype-<span style="color: #800080;">2.5</span>.<span style="color: #800080;">3</span><span style="color: #000000;">]# cd ..
[root@linuxprobe src]# </span><span style="color: #0000ff;">tar</span> zxvf jpegsrc.v9a.<span style="color: #0000ff;">tar</span><span style="color: #000000;">.gz
[root@linuxprobe src]# cd jpeg</span>-<span style="color: #000000;">9a
[root@linuxprobe jpeg</span>-9a]# ./configure --prefix=/usr/local/jpeg --enable-<span style="color: #000000;">shared
[root@linuxprobe jpeg</span>-9a]# <span style="color: #0000ff;">make</span><span style="color: #000000;">
[root@linuxprobe jpeg</span>-9a]# <span style="color: #0000ff;">make</span> <span style="color: #0000ff;">install</span></pre>
</div>
<p>⑧libgd源码包是用于提供图形处理的服务程序，其解压、编译、安装过程中生成的输出信息均已省略。在编译libgd源码包时，请记得写入的是jpeg、libpng、freetype、tiff、libvpx等服务程序在系统中的安装路径，即在上面安装过程中使用--prefix参数指定的目录路径：</p>
<div class="cnblogs_code">
<pre>[root@linuxprobe jpeg-<span style="color: #000000;">9a]# cd ..
[root@linuxprobe src]# </span><span style="color: #0000ff;">tar</span> zxvf libgd-<span style="color: #800080;">2.1</span>.<span style="color: #800080;">0</span>.<span style="color: #0000ff;">tar</span><span style="color: #000000;">.gz
[root@linuxprobe src]# cd libgd</span>-<span style="color: #800080;">2.1</span>.<span style="color: #800080;">0</span><span style="color: #000000;">
[root@linuxprobe libgd</span>-<span style="color: #800080;">2.1</span>.<span style="color: #800080;">0</span>]# ./configure --prefix=/usr/local/libgd --enable-shared --with-jpeg=/usr/local/jpeg --with-png=/usr/local/libpng --with-freetype=/usr/local/freetype --with-fontconfig=/usr/local/freetype --with-xpm=/usr/ --with-tiff=/usr/local/tiff --with-vpx=/usr/local/<span style="color: #000000;">libvpx
[root@linuxprobe libgd</span>-<span style="color: #800080;">2.1</span>.<span style="color: #800080;">0</span>]# <span style="color: #0000ff;">make</span><span style="color: #000000;">
[root@linuxprobe libgd</span>-<span style="color: #800080;">2.1</span>.<span style="color: #800080;">0</span>]# <span style="color: #0000ff;">make</span> <span style="color: #0000ff;">install</span></pre>
</div>
<p>⑨t1lib源码包是用于提供图片生成函数库的服务程序，其解压、编译、安装过程中生成的输出信息均已省略。安装后把/usr/lib64目录中的函数文件链接到/usr/lib目录中，以便系统能够顺利调取到函数文件：</p>
<p>报未找到latex需要执行：&nbsp;<span class="cnblogs_code"><span style="color: #0000ff;">yum</span> <span style="color: #0000ff;">install</span> texlive-latex</span>&nbsp;&nbsp;<span class="cnblogs_code"><span style="color: #0000ff;">yum</span> <span style="color: #0000ff;">install</span> texlive-latex-extra</span>&nbsp;&nbsp;<span class="cnblogs_code"><span style="color: #0000ff;">yum</span> <span style="color: #0000ff;">install</span> texlive-latex-recommended</span>&nbsp;&nbsp;<span class="cnblogs_code"><span style="color: #0000ff;">yum</span> -y <span style="color: #0000ff;">install</span> texlive texlive-*.noarch</span>&nbsp;</p>
<div class="cnblogs_code">
<pre>[root@linuxprobe cd libgd-<span style="color: #800080;">2.1</span>.<span style="color: #800080;">0</span><span style="color: #000000;">]# cd ..
[root@linuxprobe src]# </span><span style="color: #0000ff;">tar</span> zxvf t1lib-<span style="color: #800080;">5.1</span>.<span style="color: #800080;">2</span>.<span style="color: #0000ff;">tar</span><span style="color: #000000;">.gz
[root@linuxprobe src]# cd t1lib</span>-<span style="color: #800080;">5.1</span>.<span style="color: #800080;">2</span><span style="color: #000000;">
[root@linuxprobe t1lib</span>-<span style="color: #800080;">5.1</span>.<span style="color: #800080;">2</span>]# ./configure --prefix=/usr/local/t1lib --enable-<span style="color: #000000;">shared
[root@linuxprobe t1lib</span>-<span style="color: #800080;">5.1</span>.<span style="color: #800080;">2</span>]# <span style="color: #0000ff;">make</span><span style="color: #000000;">
[root@linuxprobe t1lib</span>-<span style="color: #800080;">5.1</span>.<span style="color: #800080;">2</span>]# <span style="color: #0000ff;">make</span> <span style="color: #0000ff;">install</span><span style="color: #000000;">
[root@linuxprobe t1lib</span>-<span style="color: #800080;">5.1</span>.<span style="color: #800080;">2</span>]# <span style="color: #0000ff;">ln</span> -s /usr/lib64/libltdl.so /usr/lib/<span style="color: #000000;">libltdl.so 
[root@linuxprobe t1lib</span>-<span style="color: #800080;">5.1</span>.<span style="color: #800080;">2</span>]# <span style="color: #0000ff;">cp</span> -frp /usr/lib64/libXpm.so* /usr/lib/</pre>
</div>
<p>⑩此时终于把编译php服务源码包的相关软件包都已经安装部署妥当了。在开始编译php源码包之前，先定义一个名为LD_LIBRARY_PATH的全局环境变量，该环境变量的作用是帮助系统找到指定的动态链接库文件，这些文件是编译php服务源码包的必须元素之一。编译php服务源码包时，除了定义要安装到的目录以外，还需要依次定义配置php服务程序配置文件的保存目录、MySQL数据库服务程序所在目录、MySQL数据库服务程序配置文件所在目录，以及libpng、jpeg、freetype、libvpx、zlib、t1lib等服务程序的安装目录路径，并通过参数启动php服务程序的诸多默认功能：</p>
<div class="cnblogs_code">
<pre>[root@linuxprobe t1lib-<span style="color: #800080;">5.1</span>.<span style="color: #800080;">2</span><span style="color: #000000;">]# cd ..
[root@linuxprobe src]# </span><span style="color: #0000ff;">tar</span> -zvxf php-<span style="color: #800080;">5.5</span>.<span style="color: #800080;">14</span>.<span style="color: #0000ff;">tar</span><span style="color: #000000;">.gz
[root@linuxprobe src]# cd php</span>-<span style="color: #800080;">5.5</span>.<span style="color: #800080;">14</span><span style="color: #000000;">
[root@linuxprobe php</span>-<span style="color: #800080;">5.5</span>.<span style="color: #800080;">14</span>]# export LD_LIBRARY_PATH=/usr/local/libgd/<span style="color: #000000;">lib
[root@linuxprobe php</span>-<span style="color: #800080;">5.5</span>.<span style="color: #800080;">14</span>]# ./configure --prefix=/usr/local/php --with-config-<span style="color: #0000ff;">file</span>-path=/usr/local/php/etc --with-mysql=/usr/local/mysql --with-mysqli=/usr/local/mysql/bin/mysql_config --with-mysql-sock=/tmp/mysql.sock --with-pdo-mysql=/usr/local/mysql --with-gd --with-png-<span style="color: #0000ff;">dir</span>=/usr/local/libpng --with-jpeg-<span style="color: #0000ff;">dir</span>=/usr/local/jpeg --with-freetype-<span style="color: #0000ff;">dir</span>=/usr/local/freetype --with-xpm-<span style="color: #0000ff;">dir</span>=/usr/ --with-vpx-<span style="color: #0000ff;">dir</span>=/usr/local/libvpx/ --with-zlib-<span style="color: #0000ff;">dir</span>=/usr/local/zlib --with-t1lib=/usr/local/t1lib --with-iconv --enable-libxml --enable-xml --enable-bcmath --enable-shmop --enable-sysvsem --enable-inline-optimization --enable-opcache --enable-mbregex --enable-fpm --enable-mbstring --enable-<span style="color: #0000ff;">ftp</span> --enable-gd-native-ttf --with-openssl --enable-pcntl --enable-sockets --with-xmlrpc --enable-<span style="color: #0000ff;">zip</span> --enable-soap --without-pear --with-gettext --enable-session --with-mcrypt --with-curl --enable-<span style="color: #000000;">ctype 
[root@linuxprobe php</span>-<span style="color: #800080;">5.5</span>.<span style="color: #800080;">14</span>]# <span style="color: #0000ff;">make</span><span style="color: #000000;">
[root@linuxprobe php</span>-<span style="color: #800080;">5.5</span>.<span style="color: #800080;">14</span>]# <span style="color: #0000ff;">make</span> <span style="color: #0000ff;">install</span></pre>
</div>
<p>⑪在php源码包程序安装完成后，需要删除当前默认的配置文件，然后将php服务程序目录中相应的配置文件复制过来：</p>
<div class="cnblogs_code">
<pre>[root@linuxprobe php-<span style="color: #800080;">5.5</span>.<span style="color: #800080;">14</span>]# <span style="color: #0000ff;">rm</span> -rf /etc/<span style="color: #000000;">php.ini
[root@linuxprobe php</span>-<span style="color: #800080;">5.5</span>.<span style="color: #800080;">14</span>]# <span style="color: #0000ff;">ln</span> -s /usr/local/php/etc/php.ini /etc/<span style="color: #000000;">php.ini
[root@linuxprobe php</span>-<span style="color: #800080;">5.5</span>.<span style="color: #800080;">14</span>]# <span style="color: #0000ff;">cp</span> php.ini-production /usr/local/php/etc/<span style="color: #000000;">php.ini
[root@linuxprobe php</span>-<span style="color: #800080;">5.5</span>.<span style="color: #800080;">14</span>]# <span style="color: #0000ff;">cp</span> /usr/local/php/etc/php-fpm.conf.default /usr/local/php/etc/php-<span style="color: #000000;">fpm.conf
[root@linuxprobe php</span>-<span style="color: #800080;">5.5</span>.<span style="color: #800080;">14</span>]# <span style="color: #0000ff;">ln</span> -s /usr/local/php/etc/php-fpm.conf /etc/php-fpm.conf</pre>
</div>
<p>⑫php-fpm.conf是php服务程序重要的配置文件之一，我们需要启用该配置文件中第25行左右的pid文件保存目录，然后分别将第148和149行的user与group参数分别修改为www账户和用户组名称：</p>
<div class="cnblogs_code">
<pre>[root@linuxprobe php-<span style="color: #800080;">5.5</span>.<span style="color: #800080;">14</span>]# vim /usr/local/php/etc/php-<span style="color: #000000;">fpm.conf
</span><span style="color: #800080;">1</span><span style="color: #000000;"> ;;;;;;;;;;;;;;;;;;;;;
</span><span style="color: #800080;">2</span><span style="color: #000000;"> ; FPM Configuration ;
</span><span style="color: #800080;">3</span><span style="color: #000000;"> ;;;;;;;;;;;;;;;;;;;;;
</span><span style="color: #800080;">4</span> 
<span style="color: #800080;">5</span> ; All relative paths <span style="color: #0000ff;">in</span> this configuration <span style="color: #0000ff;">file</span> are relative to PHP<span style="color: #800000;">'</span><span style="color: #800000;">s instal l</span>
<span style="color: #800080;">6</span> ; prefix (/usr/local/<span style="color: #000000;">php). This prefix can be dynamically changed by using t he
</span><span style="color: #800080;">7</span> ; <span style="color: #800000;">'</span><span style="color: #800000;">-p</span><span style="color: #800000;">'</span><span style="color: #000000;"> argument from the command line.
</span><span style="color: #800080;">8</span> 
<span style="color: #800080;">9</span> ; Include one or <span style="color: #0000ff;">more</span> files. If glob(<span style="color: #800080;">3</span><span style="color: #000000;">) exists, it is used to include a bunc h of
</span><span style="color: #800080;">10</span> ; files from a glob(<span style="color: #800080;">3</span>) pattern. This directive can be used everywhere <span style="color: #0000ff;">in</span><span style="color: #000000;"> the
</span><span style="color: #800080;">11</span> ; <span style="color: #0000ff;">file</span><span style="color: #000000;">.
</span><span style="color: #800080;">12</span><span style="color: #000000;"> ; Relative path can also be used. They will be prefixed by:
</span><span style="color: #800080;">13</span> ; - the global prefix <span style="color: #0000ff;">if</span> it<span style="color: #800000;">'</span><span style="color: #800000;">s been set (-p argument)</span>
<span style="color: #800080;">14</span> ; - /usr/local/<span style="color: #000000;">php otherwise
</span><span style="color: #800080;">15</span> ;include=etc/fpm.d<span style="color: #008000;">/*</span><span style="color: #008000;">.conf
16 
17 ;;;;;;;;;;;;;;;;;;
18 ; Global Options ;
19 ;;;;;;;;;;;;;;;;;;
20 
21 [global]
22 ; Pid file
23 ; Note: the default prefix is /usr/local/php/var
24 ; Default Value: none
25 pid = run/php-fpm.pid
26 
&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;省略部分输出信息&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;
145 ; Unix user/group of processes
146 ; Note: The user is mandatory. If the group is not set, the default user's g roup
147 ; will be used.
148 user = www
149 group = www
150 
&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;省略部分输出信息&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;</span></pre>
</div>
<p>⑬配置妥当后便可把用于管理php服务的脚本文件复制到/etc/rc.d/init.d中了。为了能够执行脚本，请记得为脚本赋予755权限。最后把php-fpm服务程序加入到开机启动项中：</p>
<div class="cnblogs_code">
<pre>[root@linuxprobe php-<span style="color: #800080;">5.5</span>.<span style="color: #800080;">14</span>]# <span style="color: #0000ff;">cp</span> sapi/fpm/init.d.php-fpm /etc/rc.d/init.d/php-<span style="color: #000000;">fpm
[root@linuxprobe php</span>-<span style="color: #800080;">5.5</span>.<span style="color: #800080;">14</span>]# <span style="color: #0000ff;">chmod</span> <span style="color: #800080;">755</span> /etc/rc.d/init.d/php-<span style="color: #000000;">fpm
[root@linuxprobe php</span>-<span style="color: #800080;">5.5</span>.<span style="color: #800080;">14</span>]# chkconfig php-fpm on</pre>
</div>
<p>⑭由于php服务程序的配置参数直接会影响到Web服务服务的运行环境，因此，如果默认开启了一些不必要且高危的功能（如允许用户在网页中执行Linux命令），则会降低网站被入侵的难度，入侵人员甚至可以拿到整台Web服务器的管理权限。因此我们需要编辑php.ini配置文件，在305行的disable_functions参数后面追加上要禁止的功能。下面的禁用功能名单是依据网站运行的经验而定制的，不见得适合每个生产环境，建议大家在此基础上根据自身工作需求酌情删减：</p>
<div class="cnblogs_code">
<pre>[root@linuxprobe php-<span style="color: #800080;">5.5</span>.<span style="color: #800080;">14</span>]# vim /usr/local/php/etc/<span style="color: #000000;">php.ini
&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;省略部分输出信息&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;
</span><span style="color: #800080;">300</span> 
<span style="color: #800080;">301</span> ; This directive allows you to disable certain functions <span style="color: #0000ff;">for</span><span style="color: #000000;"> security reasons.
</span><span style="color: #800080;">302</span> ; It receives a comma-delimited list of <span style="color: #0000ff;">function</span><span style="color: #000000;"> names. This directive is
</span><span style="color: #800080;">303</span> ; *NOT*<span style="color: #000000;"> affected by whether Safe Mode is turned On or Off.
</span><span style="color: #800080;">304</span> ; http:<span style="color: #008000;">//</span><span style="color: #008000;">php.net/disable-functions</span>
<span style="color: #800080;">305</span> disable_functions = passthru,exec,system,<span style="color: #0000ff;">chroot</span>,scandir,<span style="color: #0000ff;">chgrp</span>,<span style="color: #0000ff;">chown</span>,shell_exec,proc_open,proc_get_status,ini_alter,ini_alter,ini_restor e,dl,openlog,syslog,<span style="color: #0000ff;">readlink</span><span style="color: #000000;">,symlink,popepassthru,stream_socket_server,escapeshellcmd,dll,popen,disk_free_space,checkdnsrr,checkdnsrr,g etservbyname,getservbyport,disk_total_space,posix_ctermid,posix_get_last_error,posix_getcwd,posix_getegid,posix_geteuid,posix_getgid,po six_getgrgid,posix_getgrnam,posix_getgroups,posix_getlogin,posix_getpgid,posix_getpgrp,posix_getpid,posix_getppid,posix_getpwnam,posix_ getpwuid,posix_getrlimit,posix_getsid,posix_getuid,posix_isatty,posix_kill,posix_mkfifo,posix_setegid,posix_seteuid,posix_setgid,posix_ setpgid,posix_setsid,posix_setuid,posix_strerror,posix_times,posix_ttyname,posix_uname
</span><span style="color: #800080;">306</span><span style="color: #000000;"> 
&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;省略部分输出信息&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;</span></pre>
</div>
<p>⑮这样就把php服务程序配置妥当了。最后，还需要编辑Nginx服务程序的主配置文件，把第2行的井号（#）删除，然后在后面写上负责运行Nginx服务程序的账户名称和用户组名称；在第45行的index参数后面写上网站的首页名称。最后是将第65～71行参数前的井号（#）删除来启用参数，主要是修改第69行的脚本名称路径参数，其中$document_root变量即为网站信息存储的根目录路径，若没有设置该变量，则Nginx服务程序无法找到网站信息，因此会提示&ldquo;404页面未找到&rdquo;的报错信息。在确认参数信息填写正确后便可重启Nginx服务与php-fpm服务。</p>
<div class="cnblogs_code">
<pre>[root@linuxprobe php-<span style="color: #800080;">5.5</span>.<span style="color: #800080;">14</span>]# vim /usr/local/nginx/conf/<span style="color: #000000;">nginx.conf
 </span><span style="color: #800080;">1</span> 
 <span style="color: #800080;">2</span><span style="color: #000000;"> user www www;
 </span><span style="color: #800080;">3</span> worker_processes <span style="color: #800080;">1</span><span style="color: #000000;">;
 </span><span style="color: #800080;">4</span> 
 <span style="color: #800080;">5</span> #error_log logs/<span style="color: #000000;">error.log;
 </span><span style="color: #800080;">6</span> #error_log logs/<span style="color: #000000;">error.log notice;
 </span><span style="color: #800080;">7</span> #error_log logs/error.log <span style="color: #0000ff;">info</span><span style="color: #000000;">;
 </span><span style="color: #800080;">8</span> 
 <span style="color: #800080;">9</span> #pid logs/<span style="color: #000000;">nginx.pid;
 </span><span style="color: #800080;">10</span> 
 <span style="color: #800080;">11</span><span style="color: #000000;"> 
&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;省略部分输出信息&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;
 </span><span style="color: #800080;">40</span> 
 <span style="color: #800080;">41</span> #access_log logs/<span style="color: #000000;">host.access.log main;
 </span><span style="color: #800080;">42</span> 
 <span style="color: #800080;">43</span> location /<span style="color: #000000;"> {
 </span><span style="color: #800080;">44</span><span style="color: #000000;"> root html;
 </span><span style="color: #800080;">45</span><span style="color: #000000;"> index index.html index.htm index.php;
 </span><span style="color: #800080;">46</span><span style="color: #000000;"> }
 </span><span style="color: #800080;">47</span><span style="color: #000000;"> 
&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;省略部分输出信息&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;
 </span><span style="color: #800080;">62</span> 
 <span style="color: #800080;">63</span> #pass the PHP scripts to FastCGI server listening on <span style="color: #800080;">127.0</span>.<span style="color: #800080;">0.1</span>:<span style="color: #800080;">9000</span>
 <span style="color: #800080;">64</span> 
 <span style="color: #800080;">65</span> location ~<span style="color: #000000;"> \.php$ {
 </span><span style="color: #800080;">66</span><span style="color: #000000;"> root html;
 </span><span style="color: #800080;">67</span> fastcgi_pass <span style="color: #800080;">127.0</span>.<span style="color: #800080;">0.1</span>:<span style="color: #800080;">9000</span><span style="color: #000000;">;
 </span><span style="color: #800080;">68</span><span style="color: #000000;"> fastcgi_index index.php;
 </span><span style="color: #800080;">69</span><span style="color: #000000;"> fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
 </span><span style="color: #800080;">70</span><span style="color: #000000;"> include fastcgi_params;
 </span><span style="color: #800080;">71</span><span style="color: #000000;"> }
 </span><span style="color: #800080;">72</span><span style="color: #000000;"> 
&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;省略部分输出信息&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;
[root@linuxprobe php</span>-<span style="color: #800080;">5.5</span>.<span style="color: #800080;">14</span><span style="color: #000000;">]# systemctl restart nginx
[root@linuxprobe php</span>-<span style="color: #800080;">5.5</span>.<span style="color: #800080;">14</span>]# systemctl restart php-fpm</pre>
</div>
<p><strong>7，搭建Discuz论坛</strong></p>
<p>为了检验LNMP动态网站环境是否配置妥当，可以使用在上面部署Discuz!系统，然后查看结果。如果能够在LNMP动态网站环境中成功安装使用Discuz!论坛系统，也就意味着这套架构是可用的。Discuz! X3.2是国内最常见的社区论坛系统，在经过十多年的研发后已经成为了全球成熟度最高、覆盖率最广的论坛网站系统之一。</p>
<p>Discuz! X3.2软件包的后缀是.zip格式，因此应当使用专用的unzip命令来进行解压。解压后会在当前目录中出现一个名为upload的文件目录，这里面保存的就是Discuz！论坛的系统程序。我们把Nginx服务程序网站根目录的内容清空后，就可以把这些这个目录中的文件都复制进去了。记得把Nginx服务程序的网站根目录的所有者和所属组修改为本地的www用户（已在20.2.2小节创建），并为其赋予755权限以便于能够读、写、执行该论坛系统内的文件。</p>
<div class="cnblogs_code">
<pre>[root@linuxprobe php-<span style="color: #800080;">5.5</span>.<span style="color: #800080;">14</span> ]# cd /usr/local/src/<span style="color: #000000;">
[root@linuxprobe src]# </span><span style="color: #0000ff;">unzip</span> Discuz_X3.2_SC_GBK.<span style="color: #0000ff;">zip</span><span style="color: #000000;">
[root@linuxprobe src]# </span><span style="color: #0000ff;">rm</span> -rf /usr/local/nginx/html/{index.html,50x.html}*<span style="color: #000000;">
[root@linuxprobe src]# </span><span style="color: #0000ff;">mv</span> upload<span style="color: #008000;">/*</span><span style="color: #008000;"> /usr/local/nginx/html/
[root@linuxprobe src]# chown -Rf www:www /usr/local/nginx/html
[root@linuxprobe src]# chmod -Rf 755 /usr/local/nginx/html</span></pre>
</div>
<p>①接受Discuz!安装向导的许可协议。在把Discuz!论坛系统程序（即刚才upload目录中的内容）复制Nginx服务网站根目录后便可刷新浏览器页面，这将自动跳转到Discuz! X3.2论坛系统的安装界面，此处需单击&ldquo;我同意&rdquo;按钮，进入下一步的安装过程中，如图20-4所示。</p>
<p>&nbsp;<img src="https://img2020.cnblogs.com/blog/741594/202012/741594-20201208204537466-449443284.png" alt="" width="717" height="316" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;②检查Discuz! X3.2论坛系统的安装环境及目录权限。我们部署的LNMP动态网站环境版本和软件都与Discuz!论坛的要求相符合，如果图20-5框中的目录状态为不可写，请自行检查目录的所有者和所属组是否为www用户，以及是否对目录设置了755权限，然后单击&ldquo;下一步&rdquo;按钮。</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202012/741594-20201208204605338-2034802024.png" alt="" width="682" height="676" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;③选择&ldquo;全新安装Discuz! X（含UCenter Server）&rdquo;。UCenter Server是站点的管理平台，能够在多个站点之间同步会员账户及密码信息，单击&ldquo;下一步&rdquo;按钮，如图20-6所示。</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202012/741594-20201208204630359-675603456.png" alt="" width="644" height="244" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;④填写服务器的数据库信息与论坛系统管理员信息。网站系统使用由服务器本地（localhost）提供的数据库服务，数据名称与数据表前缀可由用户自行填写，其中数据库的用户名和密码则为用于登录MySQL数据库的信息（以初始化MySQL服务程序时填写的信息为准）。论坛系统的管理员账户为今后登录、管理Discuz!论坛时使用的验证信息，其中账户可以设置得简单好记一些，但是要将密码设置得尽可能复杂一下。在信息填写正确后单击&ldquo;下一步&rdquo;按钮，如图20-7所示。</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202012/741594-20201208204655674-569995803.png" alt="" width="584" height="314" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>⑤等待Discuz! X3.2论坛系统安装完毕，如图20-8所示。这个安装过程是非常快速的，大概只需要30秒左右，然后就可看到论坛安装完成的欢迎界面了。由于虚拟机主机可能并没有连接到互联网，因此该界面中可能无法正常显示Discuz!论坛系统的广告信息。在接入了互联网的服务器上成功安装完Discuz! X3.2论坛系统之后，其界面如图20-9所示。随后单击&ldquo;您的论坛已完成安装，点此访问&rdquo;按钮，即可访问到论坛首页，如图20-10所示。</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202012/741594-20201208204717217-1018610719.png" alt="" width="647" height="353" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;<img src="https://img2020.cnblogs.com/blog/741594/202012/741594-20201208204740874-749868670.png" alt="" width="505" height="273" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;<img src="https://img2020.cnblogs.com/blog/741594/202012/741594-20201208204748760-16224330.png" alt="" width="483" height="256" loading="lazy" /></p>
<p>&nbsp;</p>