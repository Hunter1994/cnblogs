<p>&nbsp;</p>
<p><strong><span style="font-size: 18pt;">1，弱命名和强命名程序集的部署方式</span></strong></p>
<table border="1" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td valign="top" width="189">
<p>程序集种类</p>
</td>
<td valign="top" width="189">
<p>可以私有部署</p>
</td>
<td valign="top" width="189">
<p>可以全局部署</p>
</td>
</tr>
<tr>
<td valign="top" width="189">
<p>弱命名</p>
</td>
<td valign="top" width="189">
<p>是</p>
</td>
<td valign="top" width="189">
<p>否</p>
</td>
</tr>
<tr>
<td valign="top" width="189">
<p>强命名（需要使用发布者的公钥/私钥进行签名）</p>
</td>
<td valign="top" width="189">
<p>是</p>
</td>
<td valign="top" width="189">
<p>是</p>
</td>
</tr>
</tbody>
</table>
<p>注：利用辅助类System.Reflection.AssemblyName构造程序集名称，并获取程序集名称的各个组成部分</p>
<p>&nbsp;</p>
<p><strong><span style="font-size: 18pt;">2，两个（或更多）公司可能生成具有相同文件名的程序集会出现的问题</span></strong></p>
<p>两个（或更多）公司可能生成具有相同文件名的程序集。所以，假如两个程序集都复制到相同的公认目录，最后一个安装的就是&ldquo;老大&rdquo;。造成正在使用旧程序集的所有应用程序都无法正常工作（这正是Windows&ldquo;DLL hell&rdquo;的由来，因为共享DLL全部复制到System32目录）</p>
<p>&nbsp;</p>
<p><strong><span style="font-size: 18pt;">3，强命名程序集的特性</span></strong></p>
<p>强命名程序集具有4个重要的特性，它们共同对程序集进行唯一性标识</p>
<p>①文件名（不计扩展名）</p>
<p>②版本号</p>
<p>③语言文化（culture为neutral，说明没有任何内容与一种特定语言文化关联）</p>
<p>④公钥（由于公钥数字很大，所以经常使用从公钥派生的小哈希值，称为公钥标记）</p>
<p>&nbsp;</p>
<p><strong><span style="font-size: 18pt;">4，如何区分具有相同特性的两个公司的程序集</span></strong></p>
<p>使用标准的公钥/私钥加密技术</p>
<p>&nbsp;</p>
<p><strong><span style="font-size: 18pt;">5，创建强命名程序集</span></strong></p>
<p>使用VS工具属性-&gt;签名</p>
<p>&nbsp;</p>
<p><strong><span style="font-size: 18pt;">6，清单文件解析</span></strong></p>
<p>由于公钥是很大的数字，AssemblyRef表实际存储的是公钥标记</p>
<p>&nbsp;</p>
<p><strong><span style="font-size: 18pt;">7，全局程序集缓存（GAC）</span></strong></p>
<p>可以把强命名程序集部署在GAC中，一般GAC的目录在</p>
<p>%SystemRoot%\Microsoft.Net\Assembly</p>
<p>&nbsp;</p>