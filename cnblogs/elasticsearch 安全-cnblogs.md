<p style="font-size: 18pt; background-color: #169fe6;"><span style="color: #ffffff;"><strong>一、集群身份认证与用户鉴权</strong></span></p>
<p>1，开启es安全模块</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">#启动单节点
bin</span>/elasticsearch -E node.name=node0 -E cluster.name=geektime -E path.data=node0_data -E http.port=<span style="color: #800080;">9200</span> -E xpack.security.enabled=<span style="color: #0000ff;">true</span><span style="color: #000000;">
或者
bin</span>/elasticsearch -E xpack.security.enabled=<span style="color: #0000ff;">true</span><span style="color: #000000;">


#使用Curl访问ES，或者浏览器访问 &ldquo;localhost:</span><span style="color: #800080;">9200</span>/_cat/nodes?<span style="color: #000000;">pretty&rdquo;。返回401错误
curl </span><span style="color: #800000;">'</span><span style="color: #800000;">localhost:9200/_cat/nodes?pretty</span><span style="color: #800000;">'</span><span style="color: #000000;">

#运行密码设定的命令，设置ES内置用户及其初始密码。
bin</span>/elasticsearch-setup-<span style="color: #000000;">passwords interactive

curl </span>-u elastic <span style="color: #800000;">'</span><span style="color: #800000;">localhost:9200/_cat/nodes?pretty</span><span style="color: #800000;">'</span></pre>
</div>
<p>2，设置kibana</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;"># 修改 kibana.yml
elasticsearch.username: </span><span style="color: #800000;">"</span><span style="color: #800000;">kibana</span><span style="color: #800000;">"</span><span style="color: #000000;">
elasticsearch.password: </span><span style="color: #800000;">"</span><span style="color: #800000;">changeme</span><span style="color: #800000;">"</span></pre>
</div>
<p>3，登录</p>
<div class="cnblogs_code">
<pre>#启动。使用用户名，elastic，密码a123456</pre>
</div>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: #169fe6;"><span style="color: #ffffff;"><strong>二、集群内安全通信</strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;"># 生成证书
# 为您的Elasticearch集群创建一个证书颁发机构。例如，使用elasticsearch</span>-<span style="color: #000000;">certutil ca命令：
bin</span>/elasticsearch-<span style="color: #000000;">certutil ca

#为群集中的每个节点生成证书和私钥。例如，使用elasticsearch</span>-<span style="color: #000000;">certutil cert 命令：
bin</span>/elasticsearch-certutil cert --ca elastic-stack-<span style="color: #000000;">ca.p12

#将证书拷贝到 config</span>/<span style="color: #000000;">certs目录下
elastic</span>-<span style="color: #000000;">certificates.p12


bin</span>/elasticsearch -E node.name=node0 -E cluster.name=geektime -E path.data=node0_data -E http.port=<span style="color: #800080;">9200</span> -E xpack.security.enabled=<span style="color: #0000ff;">true</span> -E xpack.security.transport.ssl.enabled=<span style="color: #0000ff;">true</span> -E xpack.security.transport.ssl.verification_mode=certificate -E xpack.security.transport.ssl.keystore.path=certs/elastic-certificates.p12 -E xpack.security.transport.ssl.truststore.path=certs/elastic-<span style="color: #000000;">certificates.p12

bin</span>/elasticsearch -E node.name=node1 -E cluster.name=geektime -E path.data=node1_data -E http.port=<span style="color: #800080;">9201</span> -E xpack.security.enabled=<span style="color: #0000ff;">true</span> -E xpack.security.transport.ssl.enabled=<span style="color: #0000ff;">true</span> -E xpack.security.transport.ssl.verification_mode=certificate -E xpack.security.transport.ssl.keystore.path=certs/elastic-certificates.p12 -E xpack.security.transport.ssl.truststore.path=certs/elastic-<span style="color: #000000;">certificates.p12


#不提供证书的节点，无法加入
bin</span>/elasticsearch -E node.name=node2 -E cluster.name=geektime -E path.data=node2_data -E http.port=<span style="color: #800080;">9202</span> -E xpack.security.enabled=<span style="color: #0000ff;">true</span> -E xpack.security.transport.ssl.enabled=<span style="color: #0000ff;">true</span> -E xpack.security.transport.ssl.verification_mode=certificate</pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #000000;">## elasticsearch.yml 配置

#xpack.security.transport.ssl.enabled: </span><span style="color: #0000ff;">true</span><span style="color: #000000;">
#xpack.security.transport.ssl.verification_mode: certificate

#xpack.security.transport.ssl.keystore.path: certs</span>/elastic-<span style="color: #000000;">certificates.p12
#xpack.security.transport.ssl.truststore.path: certs</span>/elastic-certificates.p12</pre>
</div>
<p style="font-size: 18pt; background-color: #169fe6;"><span style="color: #ffffff;"><strong>三、使用https与集群外部间的安全通信</strong></span></p>
<div class="cnblogs_code">
<pre>xpack.security.http.ssl.enabled: <span style="color: #0000ff;">true</span><span style="color: #000000;">
xpack.security.http.ssl.keystore.path: certs</span>/elastic-<span style="color: #000000;">certificates.p12
xpack.security.http.ssl.truststore.path: certs</span>/elastic-certificates.p12</pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #000000;"># ES 启用 https
bin</span>/elasticsearch -E node.name=node0 -E cluster.name=geektime -E path.data=node0_data -E http.port=<span style="color: #800080;">9200</span> -E xpack.security.enabled=<span style="color: #0000ff;">true</span> -E xpack.security.transport.ssl.enabled=<span style="color: #0000ff;">true</span> -E xpack.security.transport.ssl.verification_mode=certificate -E xpack.security.transport.ssl.keystore.path=certs/elastic-certificates.p12 -E xpack.security.http.ssl.enabled=<span style="color: #0000ff;">true</span> -E xpack.security.http.ssl.keystore.path=certs/elastic-certificates.p12 -E xpack.security.http.ssl.truststore.path=certs/elastic-certificates.p12</pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #000000;">#Kibana 连接 ES https



# 为kibana生成pem
openssl pkcs12 </span>-<span style="color: #0000ff;">in</span> elastic-certificates.p12 -cacerts -nokeys -<span style="color: #0000ff;">out</span> elastic-<span style="color: #000000;">ca.pem


elasticsearch.hosts: [</span><span style="color: #800000;">"</span><span style="color: #800000;">https://localhost:9200</span><span style="color: #800000;">"</span><span style="color: #000000;">]
elasticsearch.ssl.certificateAuthorities: [ </span><span style="color: #800000;">"</span><span style="color: #800000;">/Users/yiruan/geektime/kibana-7.1.0/config/certs/elastic-ca.pem</span><span style="color: #800000;">"</span><span style="color: #000000;"> ]
elasticsearch.ssl.verificationMode: certificate



# 为 Kibna 配置 HTTPS
# 生成后解压，包含了instance.crt 和 instance.key
bin</span>/elasticsearch-certutil ca --<span style="color: #000000;">pem

server.ssl.enabled: </span><span style="color: #0000ff;">true</span><span style="color: #000000;">
server.ssl.certificate: config</span>/certs/<span style="color: #000000;">instance.crt
server.ssl.key: config</span>/certs/instance.key</pre>
</div>
<p>&nbsp;</p>