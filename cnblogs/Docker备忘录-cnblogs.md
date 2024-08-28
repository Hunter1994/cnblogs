<p>&nbsp;</p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201807/741594-20180712202734598-873021340.png" alt="" /></p>
<p>centOS安装教程：<a href="https://docs.docker-cn.com/engine/installation/linux/docker-ce/centos/" target="_blank">https://docs.docker-cn.com/engine/installation/linux/docker-ce/centos/</a></p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">一、常用命令</span></strong></span></p>
<div class="cnblogs_code">
<pre>docker build -t friendlyname .<span style="color: #008000;">#</span><span style="color: #008000;"> 使用此目录的 Dockerfile 创建镜像</span>
docker run -p 4000:80 friendlyname <span style="color: #008000;">#</span><span style="color: #008000;"> 运行端口 4000 到 90 的&ldquo;友好名称&rdquo;映射</span>
docker run -d -p 4000:80 friendlyname <span style="color: #008000;">#</span><span style="color: #008000;"> 内容相同，但在分离模式下</span>
docker ps <span style="color: #008000;">#</span><span style="color: #008000;"> 查看所有正在运行的容器的列表</span>
docker stop &lt;hash&gt; <span style="color: #008000;">#</span><span style="color: #008000;"> 平稳地停止指定的容器</span>
docker ps -a <span style="color: #008000;">#</span><span style="color: #008000;"> 查看所有容器的列表，甚至包含未运行的容器</span>
docker kill &lt;hash&gt; <span style="color: #008000;">#</span><span style="color: #008000;"> 强制关闭指定的容器</span>
docker rm &lt;hash&gt; <span style="color: #008000;">#</span><span style="color: #008000;"> 从此机器中删除指定的容器</span>
docker rm $(docker ps -a -q) <span style="color: #008000;">#</span><span style="color: #008000;"> 从此机器中删除所有容器</span>
docker images -a <span style="color: #008000;">#</span><span style="color: #008000;"> 显示此机器上的所有镜像</span>
docker rmi &lt;imagename&gt; <span style="color: #008000;">#</span><span style="color: #008000;"> 从此机器中删除指定的镜像</span>
docker rmi $(docker images -q) <span style="color: #008000;">#</span><span style="color: #008000;"> 从此机器中删除所有镜像</span>
docker login <span style="color: #008000;">#</span><span style="color: #008000;"> 使用您的 Docker 凭证登录此 CLI 会话</span>
docker tag &lt;image&gt; username/repository:tag <span style="color: #008000;">#</span><span style="color: #008000;"> 标记 &lt;image&gt; 以上传到镜像库</span>
docker push username/repository:tag <span style="color: #008000;">#</span><span style="color: #008000;"> 将已标记的镜像上传到镜像库</span>
docker run username/repository:tag <span style="color: #008000;">#</span><span style="color: #008000;"> 运行镜像库中的镜像</span></pre>
</div>
<p>&nbsp;$ sudo systemctl start docker //启动docker</p>
<p>&nbsp;$&nbsp;docker run -d -p 27017:27017 --name some-mongo mongo &nbsp; //启动容器</p>
<p>&nbsp;$shell&gt; docker exec -it mysql1 bash //进入mysql1容器</p>
<p>&nbsp;$bash-4.2# mysql -uroot -p &nbsp; //在mysql1容器执行。进入mysql</p>
<p>&nbsp;$docker restart mysql01 &nbsp;//重启容器</p>
<p>&nbsp;service docker start &nbsp;//启动容器</p>
<p>docker build --rm //build时删除中间镜像</p>
<p>1，设置docker镜像地址</p>
<p>&nbsp;<span class="cnblogs_code">vim /etc/docker/daemon.json</span></p>
<p>{&nbsp;<br />"registry-mirrors": ["https://docker.mirrors.ustc.edu.cn"]&nbsp;<br />}</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">二、mysql容器</span></strong></span></p>
<p>1，使用mysql的一些问题</p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201807/741594-20180714145256215-2108468321.png" alt="" /></p>
<p>创建的mysql的root用户只能通过本地登录。这种问题可以直接把root的host改为0.0.0.0允许任何ip登录。root是超级用户，这样做不安全，一般建议另创建一个用户：</p>
<div class="cnblogs_code">
<pre>mysql&gt; CREATE USER <span style="color: #800000;">'</span><span style="color: #800000;">test</span><span style="color: #800000;">'</span>@<span style="color: #800000;">'</span><span style="color: #800000;">localhost</span><span style="color: #800000;">'</span> IDENTIFIED BY <span style="color: #800000;">'</span><span style="color: #800000;">pwd123456</span><span style="color: #800000;">'</span><span style="color: #000000;">;
mysql</span>&gt; GRANT ALL PRIVILEGES ON *.* TO <span style="color: #800000;">'</span><span style="color: #800000;">test</span><span style="color: #800000;">'</span>@<span style="color: #800000;">'</span><span style="color: #800000;">localhost</span><span style="color: #800000;">'</span><span style="color: #000000;"> WITH GRANT OPTION;
mysql</span>&gt; CREATE USER <span style="color: #800000;">'</span><span style="color: #800000;">test</span><span style="color: #800000;">'</span>@<span style="color: #800000;">'</span><span style="color: #800000;">%</span><span style="color: #800000;">'</span> IDENTIFIED BY <span style="color: #800000;">'</span><span style="color: #800000;">pwd123456</span><span style="color: #800000;">'</span><span style="color: #000000;">;
mysql</span>&gt; GRANT ALL PRIVILEGES ON *.* TO <span style="color: #800000;">'</span><span style="color: #800000;">test</span><span style="color: #800000;">'</span>@<span style="color: #800000;">'</span><span style="color: #800000;">%</span><span style="color: #800000;">'</span> WITH GRANT OPTION;</pre>
</div>
<div class="cnblogs_code" onclick="cnblogs_code_show('e5efdfc2-f8e5-43f7-b75a-202fef7aaa0d')"><img id="code_img_closed_e5efdfc2-f8e5-43f7-b75a-202fef7aaa0d" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_e5efdfc2-f8e5-43f7-b75a-202fef7aaa0d" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('e5efdfc2-f8e5-43f7-b75a-202fef7aaa0d',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_e5efdfc2-f8e5-43f7-b75a-202fef7aaa0d" class="cnblogs_code_hide">
<pre>ALTER USER <span style="color: #800000;">'</span><span style="color: #800000;">test</span><span style="color: #800000;">'</span>@<span style="color: #800000;">'</span><span style="color: #800000;">%</span><span style="color: #800000;">'</span> IDENTIFIED WITH mysql_native_password BY <span style="color: #800000;">'</span><span style="color: #800000;">pwd123456</span><span style="color: #800000;">'</span><span style="color: #000000;">;
ALTER USER </span><span style="color: #800000;">'</span><span style="color: #800000;">test</span><span style="color: #800000;">'</span>@<span style="color: #800000;">'</span><span style="color: #800000;">localhost</span><span style="color: #800000;">'</span> IDENTIFIED WITH mysql_native_password BY <span style="color: #800000;">'</span><span style="color: #800000;">pwd123456</span><span style="color: #800000;">'</span><span style="color: #000000;">;
SELECT plugin FROM mysql.user WHERE User </span>= <span style="color: #800000;">'</span><span style="color: #800000;">test</span><span style="color: #800000;">'</span>;</pre>
</div>
<span class="cnblogs_code_collapse">client does not support authentication protocol by server;consider upgrading MYSQL client解决方法</span></div>
<p>2，允许mysql容器时设置用户名和密码和字符集</p>
<div class="cnblogs_code">
<pre>docker run -d -p <span style="color: #800080;">3307</span>:<span style="color: #800080;">3306</span> -e MYSQL_USER=<span style="color: #800000;">"</span><span style="color: #800000;">hunter</span><span style="color: #800000;">"</span> -e MYSQL_PASSWORD=<span style="color: #800000;">"</span><span style="color: #800000;">pwd123456</span><span style="color: #800000;">"</span> -e MYSQL_ROOT_PASSWORD=<span style="color: #800000;">"</span><span style="color: #800000;">pwd213456</span><span style="color: #800000;">"</span> --name mysql2 mysql/mysql-server --character-<span style="color: #0000ff;">set</span>-server=utf8 --collation-server=utf8_general_ci</pre>
</div>
<p>show variables like "%char%"; &nbsp; //查看字符集</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">三、资料卷挂载</span></strong></span></p>
<p>1，使用Volume进行mysql资料卷挂载</p>
<p>①在主机上新建&nbsp;<span class="cnblogs_code">/docker/mysql/config/my.cnf</span>&nbsp;文件和&nbsp;<span class="cnblogs_code">/docker/mysql/data</span>&nbsp;目录</p>
<p>在my.conf文件中指定用户（必须指定，不然会报错）</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">[mysqld]
user</span>=mysql</pre>
</div>
<div class="cnblogs_code" onclick="cnblogs_code_show('172b6b30-4eb4-4b68-94d9-f87fc167110a')"><img id="code_img_closed_172b6b30-4eb4-4b68-94d9-f87fc167110a" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_172b6b30-4eb4-4b68-94d9-f87fc167110a" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('172b6b30-4eb4-4b68-94d9-f87fc167110a',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_172b6b30-4eb4-4b68-94d9-f87fc167110a" class="cnblogs_code_hide">
<pre><span style="color: #000000;">  [mysqld] 
  character</span>-<span style="color: #0000ff;">set</span>-server=<span style="color: #000000;">utf8
  [client]
  </span><span style="color: #0000ff;">default</span>-character-<span style="color: #0000ff;">set</span>=<span style="color: #000000;">utf8
  [mysql]
  </span><span style="color: #0000ff;">default</span>-character-<span style="color: #0000ff;">set</span>=utf8</pre>
</div>
<span class="cnblogs_code_collapse">设置编码格式</span></div>
<p>&nbsp;</p>
<p>②启动mysql</p>
<p>&nbsp;<span class="cnblogs_code">[root@localhost config]# docker run -d -p <span style="color: #800080;">3308</span>:<span style="color: #800080;">3306</span> --name mysql3 -v=/docker/mysql/config/my.cnf:/etc/my.cnf -v=/docker/mysql/data:/<span style="color: #0000ff;">var</span>/lib/mysql mysql/mysql-server</span>&nbsp;</p>
<p>将容器中的&nbsp;<span class="cnblogs_code">/etc/my.cnf</span>&nbsp;映射到主机的&nbsp;<span class="cnblogs_code">/docker/mysql/config/my.cnf:/etc/my.cnf</span>&nbsp;文件。</p>
<p>将容器的&nbsp;<span class="cnblogs_code">/<span style="color: #0000ff;">var</span>/lib/mysql</span>&nbsp;目录映射到主机的&nbsp;<span class="cnblogs_code">/docker/mysql/data</span>&nbsp;目录</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">四、镜像打包</span></strong></span></p>
<div class="cnblogs_code">
<pre>FROM microsoft/dotnet:sdk AS build-<span style="color: #000000;">env
WORKDIR </span>/<span style="color: #000000;">app

# Copy csproj and restore </span><span style="color: #0000ff;">as</span><span style="color: #000000;"> distinct layers
COPY </span>*.csproj ./<span style="color: #000000;">
RUN dotnet restore

# Copy everything </span><span style="color: #0000ff;">else</span><span style="color: #000000;"> and build
COPY . .</span>/<span style="color: #000000;">
RUN dotnet publish </span>-c Release -o <span style="color: #0000ff;">out</span><span style="color: #000000;">

# Build runtime image
FROM microsoft</span>/dotnet:aspnetcore-<span style="color: #000000;">runtime
WORKDIR </span>/<span style="color: #000000;">app
COPY </span>--<span style="color: #0000ff;">from</span>=build-env /app/<span style="color: #0000ff;">out</span><span style="color: #000000;"> .
ENTRYPOINT [</span><span style="color: #800000;">"</span><span style="color: #800000;">dotnet</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">demo.dll</span><span style="color: #800000;">"</span>]</pre>
</div>
<p>案例下载：<a href="https://pan.baidu.com/s/1DLod4xexm7-_UjJ6A8N-Ug" target="_blank">https://pan.baidu.com/s/1DLod4xexm7-_UjJ6A8N-Ug</a></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">五、容器互联</span></strong></span></p>
<p>docker inspect mysql1 //查看容器网络</p>
<p>docker inspect network test1_default //查看网络</p>
<p>docker network create -d bridge my-net &nbsp;//&nbsp;新建my-net网络</p>
<p>docker network ls　　//查看网路</p>
<p>docker network connect my-net mysql1　　//将运行的容器加入到my-net网络</p>
<p>docker run -d -p 7001:80 --net my-net --name aspcore1 aspcore:1.1　　//启动容器时加入网络</p>
<p>yum <span class="hljs-keyword">install -y iputils</span>　　//yum安装ping&nbsp;</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">六、Docker-Compose</span></strong></span></p>
<p>1，基本命令</p>
<p>&nbsp; &nbsp;①安装</p>
<pre><code class="lang-bash">$ sudo curl -L https://github.com/docker/compose/releases/download/1.17.1/docker-compose-`uname <span class="hljs-_">-s`-`uname -m` &gt; /usr/<span class="hljs-built_in">local/bin/docker-compose
$ sudo chmod +x /usr/<span class="hljs-built_in">local/bin/docker-compose</span></span></span></code></pre>
<p>&nbsp; docker-compose up //该命令十分强大，它将尝试自动完成包括构建镜像，（重新）创建服务，启动服务，并关联服务相关容器的一系列操作</p>
<p>&nbsp; docker-compose up -d //后台启动</p>
<p>&nbsp;&nbsp;docker-compose down //此命令将会停止&nbsp;<code>up</code>&nbsp;命令所启动的容器，并移除网络</p>
<p>2，启动asp.net core+mysql</p>
<div class="cnblogs_code">
<pre>version: <span style="color: #000000; font-weight: bold;">"</span><span style="color: #000000; font-weight: bold;">3</span><span style="color: #000000; font-weight: bold;">"</span><span style="color: #000000;">
services</span>:<span style="color: #000000;">
  
  db</span>:<span style="color: #000000;">
    image</span>: mysql/mysql-<span style="color: #000000;">server
    container_name</span>:<span style="color: #000000;"> db
    </span><span style="color: #008000;">#</span><span style="color: #008000;">执行mysql命令指定编码格式</span>
    command: mysqld --character-set-server=utf8 --collation-server=<span style="color: #000000;">utf8_general_ci
    ports</span>: 
      - <span style="color: #000000; font-weight: bold;">"</span><span style="color: #000000; font-weight: bold;">3306:3306</span><span style="color: #000000; font-weight: bold;">"</span>
    <span style="color: #008000;">#</span><span style="color: #008000;">指定容器退出后的重启策略为始终重启。该命令对保持服务始终运行十分有效，在生产环境中推荐配置为 always 或者 unless-stopped。</span>
    restart:<span style="color: #000000;"> always
    environment</span>:<span style="color: #000000;"> 
      MYSQL_USER</span>:<span style="color: #000000;"> hunter
      MYSQL_PASSWORD</span>:<span style="color: #000000;"> pwd123456
      MYSQL_ROOT_PASSWORD</span>:<span style="color: #000000;"> pwd123456
    volumes</span>:
      <span style="color: #008000;">#</span><span style="color: #008000;"> 主机/docker/mysql/init目录映射到mysql容器/docker-entrypoint-initdb.d目录
      # 启动时会允许此目录下的sql脚本</span>
      - /docker/mysql2/init:/docker-entrypoint-initdb.<span style="color: #000000;">d
      </span>- /docker/mysql2/config/<span style="color: #0000ff;">my</span>.cnf:/etc/<span style="color: #0000ff;">my</span>.<span style="color: #000000;">cnf
      </span>- /docker/mysql2/data:/var/lib/<span style="color: #000000;">mysql
      
  web1</span>:<span style="color: #000000;">
    depends_on</span>:
      -<span style="color: #000000;"> db
    build</span>: .<span style="color: #000000;">
    container_name</span>:<span style="color: #000000;"> aspcore1
    ports</span>: 
      - <span style="color: #000000; font-weight: bold;">"</span><span style="color: #000000; font-weight: bold;">8002:80</span><span style="color: #000000; font-weight: bold;">"</span></pre>
</div>
<p>打包asp.net core镜像</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('a03d08bf-5fdf-4949-a6d8-c3a701077750')"><img id="code_img_closed_a03d08bf-5fdf-4949-a6d8-c3a701077750" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_a03d08bf-5fdf-4949-a6d8-c3a701077750" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('a03d08bf-5fdf-4949-a6d8-c3a701077750',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_a03d08bf-5fdf-4949-a6d8-c3a701077750" class="cnblogs_code_hide">
<pre>FROM microsoft/dotnet:sdk AS build-<span style="color: #000000;">env
WORKDIR </span>/<span style="color: #000000;">app

</span><span style="color: #008000;">#</span><span style="color: #008000;"> Copy csproj and restore as distinct layers</span>
COPY *.csproj ./<span style="color: #000000;">
RUN dotnet restore

</span><span style="color: #008000;">#</span><span style="color: #008000;"> Copy everything else and build</span>
COPY . ./<span style="color: #000000;">
RUN dotnet publish </span>-c Release -<span style="color: #000000;">o out

</span><span style="color: #008000;">#</span><span style="color: #008000;"> Build runtime image</span>
FROM microsoft/dotnet:aspnetcore-<span style="color: #000000;">runtime
WORKDIR </span>/<span style="color: #000000;">app
COPY </span>--from=build-env /app/out .<span style="color: #000000;">
ENTRYPOINT [</span><span style="color: #000000; font-weight: bold;">"</span><span style="color: #000000; font-weight: bold;">dotnet</span><span style="color: #000000; font-weight: bold;">"</span>, <span style="color: #000000; font-weight: bold;">"</span><span style="color: #000000; font-weight: bold;">demo.dll</span><span style="color: #000000; font-weight: bold;">"</span>]</pre>
</div>
<span class="cnblogs_code_collapse">Dockerfile</span></div>
<p>mysql初始化执行的脚本，设置权限</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('3b350f98-91db-4d49-9507-bdfa49841e63')"><img id="code_img_closed_3b350f98-91db-4d49-9507-bdfa49841e63" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_3b350f98-91db-4d49-9507-bdfa49841e63" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('3b350f98-91db-4d49-9507-bdfa49841e63',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_3b350f98-91db-4d49-9507-bdfa49841e63" class="cnblogs_code_hide">
<pre>GRANT ALL PRIVILEGES ON *.* TO <span style="color: #000000; font-weight: bold;">'</span><span style="color: #000000; font-weight: bold;">hunter</span><span style="color: #000000; font-weight: bold;">'</span>@<span style="color: #000000; font-weight: bold;">'</span><span style="color: #000000; font-weight: bold;">%</span><span style="color: #000000; font-weight: bold;">'</span><span style="color: #000000;"> WITH GRANT OPTION;
ALTER USER </span><span style="color: #000000; font-weight: bold;">'</span><span style="color: #000000; font-weight: bold;">hunter</span><span style="color: #000000; font-weight: bold;">'</span>@<span style="color: #000000; font-weight: bold;">'</span><span style="color: #000000; font-weight: bold;">%</span><span style="color: #000000; font-weight: bold;">'</span> IDENTIFIED WITH mysql_native_password BY <span style="color: #000000; font-weight: bold;">'</span><span style="color: #000000; font-weight: bold;">pwd123456</span><span style="color: #000000; font-weight: bold;">'</span>;</pre>
</div>
<span class="cnblogs_code_collapse">init.sql</span></div>
<p>使用重试方式，保证在db初始完成之后执行种子命令</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('4499329d-17c2-4d09-9d8f-b30e6772c6a8')"><img id="code_img_closed_4499329d-17c2-4d09-9d8f-b30e6772c6a8" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_4499329d-17c2-4d09-9d8f-b30e6772c6a8" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('4499329d-17c2-4d09-9d8f-b30e6772c6a8',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_4499329d-17c2-4d09-9d8f-b30e6772c6a8" class="cnblogs_code_hide">
<pre>using <span style="color: #0000ff;">System</span><span style="color: #000000;">;
using Microsoft</span>.Extensions.<span style="color: #000000;">DependencyInjection;
using </span><span style="color: #0000ff;">System</span>.<span style="color: #000000;">Linq;
using Microsoft</span>.<span style="color: #000000;">EntityFrameworkCore;
using Microsoft</span>.Extensions.<span style="color: #000000;">Logging;
using </span><span style="color: #0000ff;">System</span>.<span style="color: #000000;">Threading;

namespace demo</span>.<span style="color: #000000;">Data
{
    public class MyDbContextSeed
    {
        
        private ILogger</span>&lt;MyDbContextSeed&gt;<span style="color: #000000;"> _logger;
        public MyDbContextSeed(ILogger</span>&lt;MyDbContextSeed&gt;<span style="color: #000000;"> logger)
        {
            _logger</span>=<span style="color: #000000;">logger;
        }

        public void Seed(IServiceProvider service</span>,<span style="color: #0000ff;">int</span><span style="color: #000000;"> retry)
        {
            _logger</span>.LogDebug(<span style="color: #000000; font-weight: bold;">"</span><span style="color: #000000; font-weight: bold;">InSeed</span><span style="color: #000000; font-weight: bold;">"</span><span style="color: #000000;">);
            try{
                using(var services</span>=service.<span style="color: #000000;">CreateScope()) 
                {
                    var provider</span>= services.<span style="color: #000000;">ServiceProvider;
                    var logFactory</span>= services.ServiceProvider.GetService&lt;ILoggerFactory&gt;<span style="color: #000000;">();
                    var context</span>= provider.GetRequiredService&lt;MyDbContext&gt;<span style="color: #000000;">();
                    _logger</span>.LogDebug(<span style="color: #000000; font-weight: bold;">"</span><span style="color: #000000; font-weight: bold;">Migrate_Start</span><span style="color: #000000; font-weight: bold;">"</span><span style="color: #000000;">);
                    context</span>.Database.<span style="color: #000000;">Migrate();
                    _logger</span>.LogDebug(<span style="color: #000000; font-weight: bold;">"</span><span style="color: #000000; font-weight: bold;">Migrate_End</span><span style="color: #000000; font-weight: bold;">"</span><span style="color: #000000;">);
                    </span><span style="color: #0000ff;">if</span>(!context.Users.<span style="color: #000000;">Any())
                    {
                        _logger</span>.LogDebug(<span style="color: #000000; font-weight: bold;">"</span><span style="color: #000000; font-weight: bold;">UserAdd_Start</span><span style="color: #000000; font-weight: bold;">"</span><span style="color: #000000;">);
                        context</span>.Users.Add(new User(){Password=<span style="color: #000000; font-weight: bold;">"</span><span style="color: #000000; font-weight: bold;">123456</span><span style="color: #000000; font-weight: bold;">"</span>,UserName=<span style="color: #000000; font-weight: bold;">"</span><span style="color: #000000; font-weight: bold;">hunter</span><span style="color: #000000; font-weight: bold;">"</span><span style="color: #000000;">});
                        context</span>.<span style="color: #000000;">SaveChanges();
                        _logger</span>.LogDebug(<span style="color: #000000; font-weight: bold;">"</span><span style="color: #000000; font-weight: bold;">UserAdd_End</span><span style="color: #000000; font-weight: bold;">"</span><span style="color: #000000;">);
                    }
                } 
            }
            catch(Exception ex){
                _logger</span>.LogError(<span style="color: #000000; font-weight: bold;">"</span><span style="color: #000000; font-weight: bold;">失败重试:</span><span style="color: #000000; font-weight: bold;">"</span>+<span style="color: #000000;">retry);
                Thread</span>.<span style="color: #0000ff;">Sleep</span>(<span style="color: #800000;">2000</span><span style="color: #000000;">);
                Seed(service</span>,++<span style="color: #000000;">retry);
            }
               
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">MyDbContextSeed.cs</span></div>
<p>连接字符串server使用的容器名称</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('8a9b3101-0787-447c-be6d-6fb385b311ee')"><img id="code_img_closed_8a9b3101-0787-447c-be6d-6fb385b311ee" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_8a9b3101-0787-447c-be6d-6fb385b311ee" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('8a9b3101-0787-447c-be6d-6fb385b311ee',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_8a9b3101-0787-447c-be6d-6fb385b311ee" class="cnblogs_code_hide">
<pre><span style="color: #000000;">{
  </span><span style="color: #000000; font-weight: bold;">"</span><span style="color: #000000; font-weight: bold;">Logging</span><span style="color: #000000; font-weight: bold;">"</span>:<span style="color: #000000;"> {
    </span><span style="color: #000000; font-weight: bold;">"</span><span style="color: #000000; font-weight: bold;">LogLevel</span><span style="color: #000000; font-weight: bold;">"</span>:<span style="color: #000000;"> {
      </span><span style="color: #000000; font-weight: bold;">"</span><span style="color: #000000; font-weight: bold;">Default</span><span style="color: #000000; font-weight: bold;">"</span>: <span style="color: #000000; font-weight: bold;">"</span><span style="color: #000000; font-weight: bold;">Warning</span><span style="color: #000000; font-weight: bold;">"</span><span style="color: #000000;">
    }
  }</span>,
  <span style="color: #000000; font-weight: bold;">"</span><span style="color: #000000; font-weight: bold;">AllowedHosts</span><span style="color: #000000; font-weight: bold;">"</span>: <span style="color: #000000; font-weight: bold;">"</span><span style="color: #000000; font-weight: bold;">*</span><span style="color: #000000; font-weight: bold;">"</span>,
  <span style="color: #000000; font-weight: bold;">"</span><span style="color: #000000; font-weight: bold;">ConnectionStrings</span><span style="color: #000000; font-weight: bold;">"</span>:<span style="color: #000000;"> {
    </span><span style="color: #000000; font-weight: bold;">"</span><span style="color: #000000; font-weight: bold;">MysqlConnection</span><span style="color: #000000; font-weight: bold;">"</span>: <span style="color: #000000; font-weight: bold;">"</span><span style="color: #000000; font-weight: bold;">server=db;port=3306;database=demo1;userid=hunter;password=pwd123456;</span><span style="color: #000000; font-weight: bold;">"</span><span style="color: #000000;">
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">appsettings.json</span></div>
<p>案例下载：<a href="https://pan.baidu.com/s/1lAy6pM9uipQnbvGG6A2TYQ" target="_blank">https://pan.baidu.com/s/1lAy6pM9uipQnbvGG6A2TYQ</a></p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">七、Gitlab</span></strong></span></p>
<p>参考教程：<a href="https://docs.gitlab.com/omnibus/docker/#after-starting-a-container" target="_blank">https://docs.gitlab.com/omnibus/docker/#after-starting-a-container</a></p>
<p>本例使用&nbsp;<span class="cnblogs_code">GitLab CE</span>&nbsp;&nbsp;镜像，如果使用&nbsp;<span class="cnblogs_code">GitLab EE</span>&nbsp;将镜像名称替换为&nbsp;<span class="cnblogs_code">gitlab/gitlab-ee:latest</span>&nbsp;</p>
<p>gitlab可以使用以下三种方式运行</p>
<ul>
<li>使用docker引擎运行</li>
<li>将gitlab安装到集群中</li>
<li>使用docker-compose安装</li>
</ul>
<h2>运行镜像</h2>
<div class="cnblogs_code">
<pre>sudo docker run --<span style="color: #000000;">detach \
    </span>--<span style="color: #000000;">hostname gitlab.example.com \
    </span>--publish 443:443 --publish 80:80 --publish 22:22<span style="color: #000000;"> \
    </span>--<span style="color: #000000;">name gitlab \
    </span>--<span style="color: #000000;">restart always \
    </span>--volume /srv/gitlab/config:/etc/<span style="color: #000000;">gitlab \
    </span>--volume /srv/gitlab/logs:/var/log/<span style="color: #000000;">gitlab \
    </span>--volume /srv/gitlab/data:/var/opt/<span style="color: #000000;">gitlab \
    gitlab</span>/gitlab-ce:latest</pre>
</div>
<p>这将下载并启动GitLab CE容器并发布访问SSH，HTTP和HTTPS所需的端口。</p>
<p>所有GitLab数据都将存储为/srv/gitlab/的子目录。</p>
<p>restart always：系统重启后，容器将自动重启。</p>
<p>您现在可以按照启动容器后的说明登录Web界面。</p>
<h2>数据存储在哪里？</h2>
<p>GitLab容器使用主机安装的卷来存储持久数据：</p>
<table border="1" frame="vsides" align="left">
<thead>
<tr><th>Local location</th><th>Container location</th><th>Usage</th></tr>
</thead>
<tbody>
<tr>
<td><code>/srv/gitlab/data</code></td>
<td><code>/var/opt/gitlab</code></td>
<td>用于存储应用数据</td>
</tr>
<tr>
<td><code>/srv/gitlab/logs</code></td>
<td><code>/var/log/gitlab</code></td>
<td>用于存储日志</td>
</tr>
<tr>
<td><code>/srv/gitlab/config</code></td>
<td><code>/etc/gitlab</code></td>
<td>用于存储GitLab配置文件</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>配置GitLab</h2>
<p>此容器使用官方的Omnibus GitLab软件包，因此所有配置都在唯一的配置文件&nbsp;<span class="cnblogs_code">/etc/gitlab/gitlab.rb</span>&nbsp;中完成。</p>
<p>打开/etc/gitlab/gitlab.rb后，确保将&nbsp;<span class="cnblogs_code">external_url</span>&nbsp;设置为指向有效的URL。</p>
<p>要从GitLab接收电子邮件，您必须配置SMTP设置，因为GitLab Docker映像没有安装SMTP服务器。</p>
<p>完成所需的所有更改后，需要重新启动容器才能重新配置GitLab：&nbsp;<span class="cnblogs_code">sudo docker restart gitlab</span>&nbsp;</p>
<h2>预配置Docker容器</h2>
<p>您可以通过将环境变量GITLAB_OMNIBUS_CONFIG添加到docker run命令来预配置GitLab Docker映像。注意：GITLAB_OMNIBUS_CONFIG中包含的设置不会写入gitlab.rb配置文件</p>
<p>这是一个设置外部URL并在启动容器时启用LFS的示例：</p>
<div class="cnblogs_code">
<pre>sudo docker run --<span style="color: #000000;">detach \
    </span>--<span style="color: #000000;">hostname gitlab.example.com \
    </span>--env GITLAB_OMNIBUS_CONFIG=<span style="color: #800000;">"</span><span style="color: #800000;">external_url 'http://my.domain.com/'; gitlab_rails['lfs_enabled'] = true;</span><span style="color: #800000;">"</span><span style="color: #000000;"> \
    </span>--publish <span style="color: #800080;">443</span>:<span style="color: #800080;">443</span> --publish <span style="color: #800080;">80</span>:<span style="color: #800080;">80</span> --publish <span style="color: #800080;">22</span>:<span style="color: #800080;">22</span><span style="color: #000000;"> \
    </span>--<span style="color: #000000;">name gitlab \
    </span>--<span style="color: #000000;">restart always \
    </span>--volume /srv/gitlab/config:/etc/<span style="color: #000000;">gitlab \
    </span>--volume /srv/gitlab/logs:/<span style="color: #0000ff;">var</span>/log/<span style="color: #000000;">gitlab \
    </span>--volume /srv/gitlab/data:/<span style="color: #0000ff;">var</span>/opt/<span style="color: #000000;">gitlab \
    gitlab</span>/gitlab-ce:latest</pre>
</div>
<p>请注意，每次执行docker run命令时，都需要提供GITLAB_OMNIBUS_CONFIG选项。 后续运行之间不保留GITLAB_OMNIBUS_CONFIG的内容。</p>
<p><span style="font-size: 12px; color: #ff0000;">由于22端口被占用我使用的是23。网站端口改为8099</span></p>
<h2>启动容器后</h2>
<p>初始化过程可能需要很长时间。 您可以使用命令&nbsp;<span class="cnblogs_code">sudo docker logs -f gitlab</span>&nbsp;跟踪此过程<br />您第一次访问GitLab时，系统会要求您设置管理员密码。 更改后，您可以使用用户名root和您设置的密码登录</p>
<h2>将GitLab升级到更新版本</h2>
<p>要将GitLab升级到新版本，您必须：</p>
<p>1、停止正在运行的容器：&nbsp;<span class="cnblogs_code">sudo docker stop gitlab</span>&nbsp;</p>
<p>2、删除现有容器：&nbsp;<span class="cnblogs_code">sudo docker rm gitlab</span>&nbsp;</p>
<p>3、拉新镜像：&nbsp;<span class="cnblogs_code">sudo docker pull gitlab/gitlab-ce:latest</span>&nbsp;</p>
<p>4、使用先前指定的选项再次创建容器：</p>
<div class="cnblogs_code">
<pre>sudo docker run --<span style="color: #000000;">detach \
</span>--<span style="color: #000000;">hostname gitlab.example.com \
</span>--publish <span style="color: #800080;">443</span>:<span style="color: #800080;">443</span> --publish <span style="color: #800080;">80</span>:<span style="color: #800080;">80</span> --publish <span style="color: #800080;">22</span>:<span style="color: #800080;">22</span><span style="color: #000000;"> \
</span>--<span style="color: #000000;">name gitlab \
</span>--<span style="color: #000000;">restart always \
</span>--volume /srv/gitlab/config:/etc/<span style="color: #000000;">gitlab \
</span>--volume /srv/gitlab/logs:/<span style="color: #0000ff;">var</span>/log/<span style="color: #000000;">gitlab \
</span>--volume /srv/gitlab/data:/<span style="color: #0000ff;">var</span>/opt/<span style="color: #000000;">gitlab \
gitlab</span>/gitlab-ce:latest</pre>
</div>
<p>在第一次运行时，GitLab将重新配置和更新自己。</p>
<h2>在公共IP地址上运行GitLab CE</h2>
<p>您可以通过修改--publish标志使Docker使用您的IP地址并将所有流量转发到GitLab CE容器。<br />在IP 1.1.1.1上公开GitLab CE：</p>
<div class="cnblogs_code">
<pre>sudo docker run --<span style="color: #000000;">detach \
    </span>--<span style="color: #000000;">hostname gitlab.example.com \
    </span>--publish <span style="color: #800080;">1.1</span>.<span style="color: #800080;">1.1</span>:<span style="color: #800080;">443</span>:<span style="color: #800080;">443</span><span style="color: #000000;"> \
    </span>--publish <span style="color: #800080;">1.1</span>.<span style="color: #800080;">1.1</span>:<span style="color: #800080;">80</span>:<span style="color: #800080;">80</span><span style="color: #000000;"> \
    </span>--publish <span style="color: #800080;">1.1</span>.<span style="color: #800080;">1.1</span>:<span style="color: #800080;">22</span>:<span style="color: #800080;">22</span><span style="color: #000000;"> \
    </span>--<span style="color: #000000;">name gitlab \
    </span>--<span style="color: #000000;">restart always \
    </span>--volume /srv/gitlab/config:/etc/<span style="color: #000000;">gitlab \
    </span>--volume /srv/gitlab/logs:/<span style="color: #0000ff;">var</span>/log/<span style="color: #000000;">gitlab \
    </span>--volume /srv/gitlab/data:/<span style="color: #0000ff;">var</span>/opt/<span style="color: #000000;">gitlab \
    gitlab</span>/gitlab-ce:latest</pre>
</div>
<p>然后，您可以访问http://1.1.1.1/和https://1.1.1.1/访问您的GitLab实例</p>
<h2>在不同的端口上公开GitLab</h2>
<p>GitLab默认会占用容器内的以下端口：</p>
<ul>
<li><code>80</code>&nbsp;(HTTP)</li>
<li><code>443</code>&nbsp;(if you configure HTTPS)</li>
<li><code>8080</code>&nbsp;(Unicorn使用的)</li>
<li><code>22</code>&nbsp;(SSH守护程序使用的)</li>
</ul>
<p>如果要为容器使用与80（HTTP）或443（HTTPS）不同的端口，则需要在docker run命令中添加单独的--publish指令。</p>
<p>例如，要在端口8929上公开Web界面，在端口2289上公开SSH服务，请使用以下docker run命令：</p>
<div class="cnblogs_code">
<pre>sudo docker run --<span style="color: #000000;">detach \
    </span>--<span style="color: #000000;">hostname gitlab.example.com \
    </span>--publish <span style="color: #800080;">8929</span>:<span style="color: #800080;">80</span> --publish <span style="color: #800080;">2289</span>:<span style="color: #800080;">22</span><span style="color: #000000;"> \
    </span>--<span style="color: #000000;">name gitlab \
    </span>--<span style="color: #000000;">restart always \
    </span>--volume /srv/gitlab/config:/etc/<span style="color: #000000;">gitlab \
    </span>--volume /srv/gitlab/logs:/<span style="color: #0000ff;">var</span>/log/<span style="color: #000000;">gitlab \
    </span>--volume /srv/gitlab/data:/<span style="color: #0000ff;">var</span>/opt/<span style="color: #000000;">gitlab \
    gitlab</span>/gitlab-ce:latest</pre>
</div>
<p>然后，您需要适当地配置gitlab.rb：</p>
<p>1，配置&nbsp;&nbsp;<span class="cnblogs_code">external_url</span>&nbsp;:</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;"># For HTTP
external_url </span><span style="color: #800000;">"</span><span style="color: #800000;">http://gitlab.example.com:8929</span><span style="color: #800000;">"</span><span style="color: #000000;">

or

# For HTTPS (notice the https)
external_url </span><span style="color: #800000;">"</span><span style="color: #800000;">https://gitlab.example.com:8929</span><span style="color: #800000;">"</span></pre>
</div>
<p>2，配置&nbsp;<span class="cnblogs_code">gitlab_shell_ssh_port</span>&nbsp;:</p>
<div class="cnblogs_code">
<pre>gitlab_rails[<span style="color: #800000;">'</span><span style="color: #800000;">gitlab_shell_ssh_port</span><span style="color: #800000;">'</span>] = <span style="color: #800080;">2289</span></pre>
</div>
<p>按照上面的示例，您将能够通过&lt;hostIP&gt;：8929下的Web浏览器访问GitLab，并使用端口2289下的SSH进行推送。</p>
<p>可以在docker-compose部分中找到使用不同端口的docker-compose.yml示例</p>
<h2>诊断潜在问题</h2>
<p>读取容器日志：&nbsp;<span class="cnblogs_code">sudo docker logs gitlab</span>&nbsp;</p>
<p>输入运行容器：&nbsp;<span class="cnblogs_code">sudo docker exec -it gitlab /bin/bash</span>&nbsp;</p>
<p>在容器内，您可以像管理Omnibus安装一样管理GitLab容器</p>
<h2>使用docker-compose安装GitLab</h2>
<p>使用Docker撰写，您可以轻松配置，安装和升级基于Docker的GitLab安装。</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">web:
  image: </span><span style="color: #800000;">'</span><span style="color: #800000;">gitlab/gitlab-ce:latest</span><span style="color: #800000;">'</span><span style="color: #000000;">
  restart: always
  hostname: </span><span style="color: #800000;">'</span><span style="color: #800000;">gitlab.example.com</span><span style="color: #800000;">'</span><span style="color: #000000;">
  environment:
    GITLAB_OMNIBUS_CONFIG: </span>|<span style="color: #000000;">
      external_url </span><span style="color: #800000;">'</span><span style="color: #800000;">https://gitlab.example.com</span><span style="color: #800000;">'</span><span style="color: #000000;">
      # Add any other gitlab.rb configuration here, each on its own line
  ports:
    </span>- <span style="color: #800000;">'</span><span style="color: #800000;">80:80</span><span style="color: #800000;">'</span>
    - <span style="color: #800000;">'</span><span style="color: #800000;">443:443</span><span style="color: #800000;">'</span>
    - <span style="color: #800000;">'</span><span style="color: #800000;">22:22</span><span style="color: #800000;">'</span><span style="color: #000000;">
  volumes:
    </span>- <span style="color: #800000;">'</span><span style="color: #800000;">/srv/gitlab/config:/etc/gitlab</span><span style="color: #800000;">'</span>
    - <span style="color: #800000;">'</span><span style="color: #800000;">/srv/gitlab/logs:/var/log/gitlab</span><span style="color: #800000;">'</span>
    - <span style="color: #800000;">'</span><span style="color: #800000;">/srv/gitlab/data:/var/opt/gitlab</span><span style="color: #800000;">'</span></pre>
</div>
<p>确保您与docker-compose.yml在同一目录中并运行docker-compose up -d以启动GitLab</p>
<p>下面是另一个docker-compose.yml示例，其中GitLab在自定义HTTP和SSH端口上运行。 注意GITLAB_OMNIBUS_CONFIG变量如何与ports部分匹配：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">web:
  image: </span><span style="color: #800000;">'</span><span style="color: #800000;">gitlab/gitlab-ce:latest</span><span style="color: #800000;">'</span><span style="color: #000000;">
  restart: always
  hostname: </span><span style="color: #800000;">'</span><span style="color: #800000;">gitlab.example.com</span><span style="color: #800000;">'</span><span style="color: #000000;">
  environment:
    GITLAB_OMNIBUS_CONFIG: </span>|<span style="color: #000000;">
      external_url </span><span style="color: #800000;">'</span><span style="color: #800000;">http://gitlab.example.com:9090</span><span style="color: #800000;">'</span><span style="color: #000000;">
      gitlab_rails[</span><span style="color: #800000;">'</span><span style="color: #800000;">gitlab_shell_ssh_port</span><span style="color: #800000;">'</span>] = <span style="color: #800080;">2224</span><span style="color: #000000;">
  ports:
    </span>- <span style="color: #800000;">'</span><span style="color: #800000;">9090:9090</span><span style="color: #800000;">'</span>
    - <span style="color: #800000;">'</span><span style="color: #800000;">2224:22</span><span style="color: #800000;">'</span><span style="color: #000000;">
  volumes:
    </span>- <span style="color: #800000;">'</span><span style="color: #800000;">/srv/gitlab/config:/etc/gitlab</span><span style="color: #800000;">'</span>
    - <span style="color: #800000;">'</span><span style="color: #800000;">/srv/gitlab/logs:/var/log/gitlab</span><span style="color: #800000;">'</span>
    - <span style="color: #800000;">'</span><span style="color: #800000;">/srv/gitlab/data:/var/opt/gitlab</span><span style="color: #800000;">'</span></pre>
</div>
<p>这与使用--publish 9090：9090 --publish 2224：22相同</p>
<h2>使用Docker compose更新GitLab</h2>
<p>如果你使用docker-compose安装了GitLab，你所要做的就是运行docker-compose pull和docker-compose up -d来下载新版本并升级你的GitLab实例</p>
<h2>将GitLab安装到群集中</h2>
<p>GitLab Docker镜像也可以部署到各种容器调度平台。</p>
<ul>
<li>Kubernetes using the&nbsp;<a href="https://docs.gitlab.com/ce/install/kubernetes/">GitLab Helm Charts</a>.</li>
<li>Mesosphere DC/OS using the&nbsp;<a href="https://github.com/dcos/examples/tree/master/gitlab/1.8">DC/OS Package</a>.</li>
<li>Docker Cloud using the&nbsp;<a href="https://docs.gitlab.com/omnibus/docker/#install-gitlab-using-docker-compose">docker-compose config</a>.</li>
</ul>
<h2>故障排除</h2>
<p>1，500内部错误</p>
<p>更新Docker镜像时，您可能会遇到一个问题，其中所有路径都显示臭名昭着的500页。 如果发生这种情况，请尝试运行sudo docker restart gitlab重启容器并纠正问题</p>
<p>2，许可问题</p>
<p>从旧的GitLab Docker映像更新时，您可能会遇到权限问题。 这是因为先前镜像中的用户未正确保留。 有修复所有文件权限的脚本。<br />要修复容器，只需执行update-permissions并在之后重新启动容器：</p>
<div class="cnblogs_code">
<pre>sudo docker exec gitlab update-<span style="color: #000000;">permissions
sudo docker restart gitlab</span></pre>
</div>
<p>3，Windows/Mac: Error executing action run on resource ruby_block[directory resource: /data/GitLab]</p>
<p>在Windows或Mac上使用Docker Toolbox和VirtualBox并使用Docker卷时会发生此错误。/c/Users卷作为VirtualBox共享文件夹安装，不支持所有POSIX文件系统功能。 如果没有重新挂载，则无法更改目录所有权和权限，并且GitLab失败。</p>
<p>我们的建议是切换到您的平台使用本机Docker安装，而不是使用Docker Toolbox。</p>
<p>如果您无法使用本机Docker安装（Windows 10 Home Edition或Windows &lt;10），那么另一种解决方案是为Docker Toolbox的boot2docker设置NFS挂载而不是VirtualBox共享</p>
<p>4，Linux ACL问题</p>
<p>如果您在docker主机上使用文件ACL，则docker1组需要对卷进行完全访问才能使GitLab正常工作。</p>
<div class="cnblogs_code">
<pre>$ getfacl /srv/<span style="color: #000000;">gitlab
# file: </span>/srv/<span style="color: #000000;">gitlab
# owner: XXXX
# group: XXXX
user::rwx
group::rwx
group:docker:rwx
mask::rwx
</span><span style="color: #0000ff;">default</span><span style="color: #000000;">:user::rwx
</span><span style="color: #0000ff;">default</span><span style="color: #000000;">:group::rwx
</span><span style="color: #0000ff;">default</span><span style="color: #000000;">:group:docker:rwx
</span><span style="color: #0000ff;">default</span><span style="color: #000000;">:mask::rwx
</span><span style="color: #0000ff;">default</span>:other::r-x</pre>
</div>
<p>如果这些不正确，请将它们设置为：</p>
<div class="cnblogs_code">
<pre>$ sudo setfacl -mR <span style="color: #0000ff;">default</span>:group:docker:rwx /srv/gitlab</pre>
</div>
<p>&nbsp;</p>