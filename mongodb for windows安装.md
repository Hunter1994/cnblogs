<p>1，下载mongodb for windwos</p>
<p>下载地址：<a href="https://www.mongodb.com/download-center#community" target="_blank">https://www.mongodb.com/download-center#community</a></p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201712/741594-20171220140758459-1328251982.png" alt="" width="796" height="434" /></p>
<p>2，创建db和log的文件夹</p>
<p>D:\data\db</p>
<p>D:\data\log</p>
<p>&nbsp;</p>
<p>3，配置mongodb.cfg</p>
<div class="cnblogs_code">
<pre>dbpath=<span style="color: #000000;">d:\data\db
logpath</span>=<span style="color: #000000;">D:\data\log\mongodb.log
logappend </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">
port</span>=<span style="color: #800080;">27017</span><span style="color: #000000;"> 
bind_ip </span>= <span style="color: #800080;">127.0</span>.<span style="color: #800080;">0.1</span> </pre>
</div>
<p>把文件放在</p>
<p>&nbsp;</p>
<p>3，安装MongoDb服务（待确定）</p>
<p>"D:\install\mongodb\bin\mongod.exe" --config "D:\install\mongodb\mongodb.cfg" --serviceName "Mongodb" --serviceDisplayName "MongoDB" --install</p>
<p><br />mongod.exe --bind_ip 127.0.0.1 --logpath "D:\data\log\mongodb.log"--logappend --dbpath "D:\data\db" --serviceName "Mongodb" --serviceDisplayName "MongoDB" --install</p>
<p>&nbsp;</p>