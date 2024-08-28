<p>kubectl get pods -o wide 显示pod的ip所运行的节点</p>
<p>kubectl describe pod&nbsp; kubia-hczji</p>
<p>kubectl get po&nbsp;kubia-hczji -o yaml 查看yaml定义</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('8ba62fa4-aec1-4ab7-aa68-0645eaab63d2')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_8ba62fa4-aec1-4ab7-aa68-0645eaab63d2" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_8ba62fa4-aec1-4ab7-aa68-0645eaab63d2" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_8ba62fa4-aec1-4ab7-aa68-0645eaab63d2" class="cnblogs_code_hide">
<pre><span style="color: #000000;">apiVersion: v1
kind: pod
metadata:
 name:kubia</span>-manual    --<span style="color: #000000;">pod的名称
spec:
 containers:
  </span>- image: luksa:kubia    --<span style="color: #000000;">容器镜像
      name: kubia            </span>--<span style="color: #000000;">容器名称
     ports:
       </span>- containerPort: <span style="color: #800080;">8080</span>  --<span style="color: #000000;">应用监听的端口
          protocol: TCP</span></pre>
</div>
<span class="cnblogs_code_collapse">kubia-manual.yaml</span></div>
<p>&nbsp;</p>