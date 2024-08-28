<p style="font-size: 18pt; background-color: #169fe6;"><span style="color: #ffffff;"><strong>一、安装docker</strong></span></p>
<p>1，卸载旧版本</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">$ sudo yum remove docker \
                  docker</span>-<span style="color: #000000;">client \
                  docker</span>-client-<span style="color: #000000;">latest \
                  docker</span>-<span style="color: #000000;">common \
                  docker</span>-<span style="color: #000000;">latest \
                  docker</span>-latest-<span style="color: #000000;">logrotate \
                  docker</span>-<span style="color: #000000;">logrotate \
                  docker</span>-engine</pre>
</div>
<p>2，获取安装脚本，并安装&nbsp;<span class="cnblogs_code">wget -qO- https:<span style="color: #008000;">//</span><span style="color: #008000;">get.docker.com/ | sh</span></span>&nbsp;</p>
<p>3，将docker配置为开启启动</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">systemctl enable docker
systemctl </span><span style="color: #0000ff;">is</span>-enabled docker</pre>
</div>
<p>4，启动docker&nbsp;&nbsp;<span class="cnblogs_code">systemctl start docker</span>&nbsp;</p>
<p>5，查询docker版本&nbsp;<span class="cnblogs_code">docker --version</span>&nbsp;</p>
<p>6，查询docker信息&nbsp;<span class="cnblogs_code">docker system info</span>&nbsp;</p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: #169fe6;"><span style="color: #ffffff;"><strong>二、镜像</strong></span></p>
<p>下载镜像：&nbsp;<span class="cnblogs_code">docker image pull &lt;repository&gt;:&lt;tag&gt;</span>&nbsp;</p>
<p>返回废墟镜像：&nbsp;<span class="cnblogs_code">docker image ls --filter dangling=<span style="color: #0000ff;">true</span></span>&nbsp;</p>
<p>移除全部的废墟镜像：&nbsp;<span class="cnblogs_code">docker image prune</span>&nbsp;</p>
<p>过滤查询：&nbsp;<span class="cnblogs_code">docker image ls --filter=reference=<span style="color: #800000;">"</span><span style="color: #800000;">*:latest</span><span style="color: #800000;">"</span></span>&nbsp;</p>
<p>在docker hub上搜索镜像：&nbsp;&nbsp;<span class="cnblogs_code">docker search mysql --filter=<span style="color: #800000;">"</span><span style="color: #800000;">is-official=true</span><span style="color: #800000;">"</span> --limit <span style="color: #800080;">100</span></span>&nbsp;</p>
<p><em><span style="font-size: 12px;">--filter="is-official=true" ：只查询官方的</span></em></p>
<p><em><span style="font-size: 12px;">--limit&nbsp;100 ：返回条数</span></em></p>
<p>查看镜像分层：&nbsp;<span class="cnblogs_code">docker image inspect ubuntu:latest</span>&nbsp;&nbsp;</p>
<p>删除镜像：&nbsp;<span class="cnblogs_code">docker image rm alpine:latest</span>&nbsp;</p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: #169fe6;"><span style="color: #ffffff;"><strong>三、容器</strong></span></p>
<p>启动ubuntu liunx并运行Bash Shell作为其应用：&nbsp;<span class="cnblogs_code">docker container run -it ubuntu /bin/bash</span>&nbsp;</p>
<p><span style="font-size: 12px;"><em>-it 参数可以将当前终端连接到容器的Shell终端之上</em></span></p>
<p><span style="font-size: 12px;"><em>Ctrl+PQ 退出容器（没有终止容器）</em></span></p>
<p>链接到运行容器的终端中：&nbsp;<span class="cnblogs_code">docker container exec -it &lt;name or id&gt; bash</span>&nbsp;</p>
<p>启动容器：&nbsp;<span class="cnblogs_code">docker container run -d --name webservice -p <span style="color: #800080;">80</span>:<span style="color: #800080;">8080</span> nigelpoulton/pluralsight-docker-ci</span>&nbsp;</p>
<p><em><span style="font-size: 12px;">-d 后台运行</span></em></p>
<p><em><span style="font-size: 12px;">-p&nbsp;80:8080 docker上80端口映射到容器内8080端口</span></em></p>
<p>查看容器：&nbsp;<span class="cnblogs_code">docker container ls</span>&nbsp;</p>
<p><em><span style="font-size: 12px;">-a 查询所有的容器</span></em></p>
<p>停止容器：&nbsp;<span class="cnblogs_code">docker container stop 6b4857fe6314</span>&nbsp;</p>
<p>删除容器：&nbsp;<span class="cnblogs_code">docker container rm 6b4857fe6314</span>&nbsp;</p>
<p>启动容器：&nbsp;<span class="cnblogs_code">docker container start percy</span>&nbsp;</p>
<p>重启策略：&nbsp;<span class="cnblogs_code">docker container run -d --name always --restrart always alpine</span>&nbsp;</p>
<p><em><span style="font-size: 12px;">always：除非明确docker container stop停止该容器，否则该策略会一直尝试重启处于停止状态的容器</span></em></p>
<p><em><span style="font-size: 12px;">unless-stopped：和always的区别是不会再docker daemon重启的时候被启动</span></em></p>
<p><em><span style="font-size: 12px;">on-failure：会在退出容器并且返回值不是0的时候重启容器</span></em></p>
<p>清理所有的容器：&nbsp;<span class="cnblogs_code">docker container rm $(docker container ls -aq) -f</span>&nbsp;&nbsp;</p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: #169fe6;"><span style="color: #ffffff;"><strong>四、netcore应用容器化</strong></span></p>
<p><strong>1，Dockerfile</strong></p>
<p><a href="https://docs.microsoft.com/en-us/aspnet/core/host-and-deploy/docker/building-net-docker-images?view=aspnetcore-2.0" target="_blank">aspnetcore Dockerfile指导链接</a></p>
<p><span class="pl-k">demo下载：链接: <a href="https://pan.baidu.com/s/1tej3V3S6_oqOKhFB5BSMmw" target="_blank">https://pan.baidu.com/s/1tej3V3S6_oqOKhFB5BSMmw</a> 提取码: ia8a&nbsp;</span></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('4ea1e893-6901-4647-8a2b-4a4ce1a82d0a')"><img id="code_img_closed_4ea1e893-6901-4647-8a2b-4a4ce1a82d0a" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_4ea1e893-6901-4647-8a2b-4a4ce1a82d0a" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('4ea1e893-6901-4647-8a2b-4a4ce1a82d0a',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_4ea1e893-6901-4647-8a2b-4a4ce1a82d0a" class="cnblogs_code_hide">
<pre>FROM mcr.microsoft.com/dotnet/core/sdk:<span style="color: #800080;">2.2</span><span style="color: #000000;"> AS build
WORKDIR </span>/<span style="color: #000000;">app

COPY </span>*<span style="color: #000000;">.csproj .
RUN dotnet restore

COPY . .
RUN dotnet publish </span>-c Release -o <span style="color: #0000ff;">out</span><span style="color: #000000;">


FROM mcr.microsoft.com</span>/dotnet/core/aspnet:<span style="color: #800080;">2.2</span><span style="color: #000000;"> AS runtime
WORKDIR </span>/<span style="color: #000000;">app
COPY </span>--<span style="color: #0000ff;">from</span>=build /app/<span style="color: #0000ff;">out</span> ./<span style="color: #000000;">
EXPOSE </span><span style="color: #800080;">5000</span><span style="color: #000000;">
ENTRYPOINT [</span><span style="color: #800000;">"</span><span style="color: #800000;">dotnet</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">netcoremvc_demo.dll</span><span style="color: #800000;">"</span>]</pre>
</div>
<span class="cnblogs_code_collapse">Dockerfile</span></div>
<p>&nbsp;</p>
<p><span class="pl-k">FROM：指定要构建的镜像的基础镜像</span></p>
<p><span class="pl-k">RUN：在镜像中执行命命令，会创建新的镜像层</span></p>
<p><span class="pl-k">COPY：将文件作为新的层添加到镜像中，通常使用COPY将应用代码赋值到镜像中</span></p>
<p><span class="pl-k">EXPOSE：声明容器运行的服务端口&nbsp;<span class="cnblogs_code">EXPOSE <span style="color: #800080;">80</span> <span style="color: #800080;">443</span></span>&nbsp;</span></p>
<p><span class="pl-k">ENTERPOINT：指定镜像以容器方式启动后默认运行的程序</span></p>
<p>ENV：设置环境变量&nbsp;<span class="cnblogs_code">ENV MYSQL_ROOT_PASSWORD <span style="color: #800080;">123456</span></span>&nbsp;</p>
<p>ADD：和COPY一样，支持自动下载和自动解压&nbsp;<span class="cnblogs_code">ADD https:<span style="color: #008000;">//</span><span style="color: #008000;">xxx.com/html.tar.gz /var/www/html</span></span>&nbsp;</p>
<p>WORKDIR：定位到指定目录（为RUN、CMD、ENTRYPOINT以及COPY和AND设置工作目录）</p>
<p>&nbsp;</p>
<p><strong>2，构建docker 镜像</strong></p>
<p>打包镜像：&nbsp;<span class="cnblogs_code">docker image build -t demo:latest .</span>&nbsp;</p>
<p>查询构建过程(size&gt;0的会新建镜像层)：&nbsp;<span class="cnblogs_code">docker image history demo:latest</span>&nbsp;</p>
<p>&nbsp;</p>
<p><strong>3，将镜像推送到docker hub</strong></p>
<p>登录docker&nbsp;<span class="cnblogs_code">docker login</span>&nbsp;</p>
<p>为镜像重新打一个标签（因为需要推送的到我们自己的docker hub下）：&nbsp;<span class="cnblogs_code">docker image tag alpine:latest <span style="color: #800080;">962410314</span>/alpine:latest</span>&nbsp;</p>
<p>推送：&nbsp;<span class="cnblogs_code">docker image push <span style="color: #800080;">962410314</span>/alpine</span>&nbsp;</p>
<p>&nbsp;</p>