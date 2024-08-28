<p>元数据是由几个表构成的二进制数据块。有三种表，分别是定义表（definition table）、引用表（reference table）和清单表（manifest table）</p>
<p>1，常用的元数据定义表</p>
<table class="MsoTableGrid" style="border: none; height: 497px; width: 784px;" border="1" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td style="width: 97.55pt; border-color: windowtext; border-width: 1pt; padding: 0cm 5.4pt;" valign="top" width="130">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">元数据定义名称</span></p>
</td>
<td style="width: 328.55pt; border-top-color: windowtext; border-right-color: windowtext; border-bottom-color: windowtext; border-top-width: 1pt; border-right-width: 1pt; border-bottom-width: 1pt; border-left-style: none; padding: 0cm 5.4pt;" valign="top" width="438">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">说明</span></p>
</td>
</tr>
<tr>
<td style="width: 97.55pt; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-right-width: 1pt; border-bottom-width: 1pt; border-left-width: 1pt; border-top-style: none; padding: 0cm 5.4pt;" valign="top" width="130">
<p class="MsoNormal"><span lang="EN-US">ModuleDef</span></p>
</td>
<td style="width: 328.55pt; border-top-style: none; border-left-style: none; border-bottom-color: windowtext; border-bottom-width: 1pt; border-right-color: windowtext; border-right-width: 1pt; padding: 0cm 5.4pt;" valign="top" width="438">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">总是包含对模块进行标识的一个记录项；</span></p>
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">包含：模块文件名，扩展名（不含路径），模块版本</span><span lang="EN-US">ID</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">（编译器创建的</span><span lang="EN-US">GUID</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">）</span></p>
</td>
</tr>
<tr>
<td style="width: 97.55pt; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-right-width: 1pt; border-bottom-width: 1pt; border-left-width: 1pt; border-top-style: none; padding: 0cm 5.4pt;" valign="top" width="130">
<p class="MsoNormal"><span lang="EN-US">TypeDef</span></p>
</td>
<td style="width: 328.55pt; border-top-style: none; border-left-style: none; border-bottom-color: windowtext; border-bottom-width: 1pt; border-right-color: windowtext; border-right-width: 1pt; padding: 0cm 5.4pt;" valign="top" width="438">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">模块定义的每个类型在这个表中都有一个记录项；</span></p>
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">包含：类型的名称，基类型，标志（</span><span lang="EN-US">public</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">等），索引（索引指向</span><span lang="EN-US">MethodDef</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">表中该类型的方法，</span><span lang="EN-US">FieldDef</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">表中该类型的字段，</span><span lang="EN-US">PropertyDef</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">表中该类型的属性，</span><span lang="EN-US">EventDef</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">表中该类型的事件）</span></p>
</td>
</tr>
<tr>
<td style="width: 97.55pt; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-right-width: 1pt; border-bottom-width: 1pt; border-left-width: 1pt; border-top-style: none; padding: 0cm 5.4pt;" valign="top" width="130">
<p class="MsoNormal"><span lang="EN-US">MethodDef</span></p>
</td>
<td style="width: 328.55pt; border-top-style: none; border-left-style: none; border-bottom-color: windowtext; border-bottom-width: 1pt; border-right-color: windowtext; border-right-width: 1pt; padding: 0cm 5.4pt;" valign="top" width="438">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">模块定义的每个方法在这个保重都有一个记录项；</span></p>
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">包含：方法的名称，标志，签名，方法的</span><span lang="EN-US">IL</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">代码在模块中的偏移量。每个记录项还引用了</span><span lang="EN-US">ParamDef</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">表中的一个记录项，后者包括与方法参数有关的更多信息</span></p>
</td>
</tr>
<tr>
<td style="width: 97.55pt; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-right-width: 1pt; border-bottom-width: 1pt; border-left-width: 1pt; border-top-style: none; padding: 0cm 5.4pt;" valign="top" width="130">
<p class="MsoNormal"><span lang="EN-US">FieldDef</span></p>
</td>
<td style="width: 328.55pt; border-top-style: none; border-left-style: none; border-bottom-color: windowtext; border-bottom-width: 1pt; border-right-color: windowtext; border-right-width: 1pt; padding: 0cm 5.4pt;" valign="top" width="438">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">模块定义了每个字段在这个表中都有一个记录项；</span></p>
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">包含：标志，类型，名称</span></p>
</td>
</tr>
<tr>
<td style="width: 97.55pt; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-right-width: 1pt; border-bottom-width: 1pt; border-left-width: 1pt; border-top-style: none; padding: 0cm 5.4pt;" valign="top" width="130">
<p class="MsoNormal"><span lang="EN-US">ParamDef</span></p>
</td>
<td style="width: 328.55pt; border-top-style: none; border-left-style: none; border-bottom-color: windowtext; border-bottom-width: 1pt; border-right-color: windowtext; border-right-width: 1pt; padding: 0cm 5.4pt;" valign="top" width="438">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">模块定义的每个参数在这个表中都有一个记录项；</span></p>
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">包含：标志（</span><span lang="EN-US">in</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">，</span><span lang="EN-US">out</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">，</span><span lang="EN-US">retval</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">等），类型，名称</span></p>
</td>
</tr>
<tr>
<td style="width: 97.55pt; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-right-width: 1pt; border-bottom-width: 1pt; border-left-width: 1pt; border-top-style: none; padding: 0cm 5.4pt;" valign="top" width="130">
<p class="MsoNormal"><span lang="EN-US">PropertyDef</span></p>
</td>
<td style="width: 328.55pt; border-top-style: none; border-left-style: none; border-bottom-color: windowtext; border-bottom-width: 1pt; border-right-color: windowtext; border-right-width: 1pt; padding: 0cm 5.4pt;" valign="top" width="438">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">模块定义的每个属性在这个表中都有一个记录项；</span></p>
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">包含：标志，类型，名称</span></p>
</td>
</tr>
<tr>
<td style="width: 97.55pt; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-right-width: 1pt; border-bottom-width: 1pt; border-left-width: 1pt; border-top-style: none; padding: 0cm 5.4pt;" valign="top" width="130">
<p class="MsoNormal"><span lang="EN-US">EventDef</span></p>
</td>
<td style="width: 328.55pt; border-top-style: none; border-left-style: none; border-bottom-color: windowtext; border-bottom-width: 1pt; border-right-color: windowtext; border-right-width: 1pt; padding: 0cm 5.4pt;" valign="top" width="438">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">模块定义的每个事件在这个表中都有一个记录项；</span></p>
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">包括：标志，名称</span></p>
</td>
</tr>
</tbody>
</table>
<p>2，常用的引用元数据表</p>
<table class="MsoTableGrid" style="border: none; height: 298px; width: 784px;" border="1" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td style="width: 97.55pt; border-color: windowtext; border-width: 1pt; padding: 0cm 5.4pt;" valign="top" width="130">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">引用元数据的名称</span></p>
</td>
<td style="width: 328.55pt; border-top-color: windowtext; border-right-color: windowtext; border-bottom-color: windowtext; border-top-width: 1pt; border-right-width: 1pt; border-bottom-width: 1pt; border-left-style: none; padding: 0cm 5.4pt;" valign="top" width="438">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">说明</span></p>
</td>
</tr>
<tr>
<td style="width: 97.55pt; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-right-width: 1pt; border-bottom-width: 1pt; border-left-width: 1pt; border-top-style: none; padding: 0cm 5.4pt;" valign="top" width="130">
<p class="MsoNormal"><span lang="EN-US">AssemblyRef</span></p>
</td>
<td style="width: 328.55pt; border-top-style: none; border-left-style: none; border-bottom-color: windowtext; border-bottom-width: 1pt; border-right-color: windowtext; border-right-width: 1pt; padding: 0cm 5.4pt;" valign="top" width="438">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">模块引用的每个程序集在这个表中都有一个记录项；</span></p>
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">包含：程序集名（不包含路径和扩展名），版本号，语言文化，公钥</span><span lang="EN-US">token</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">，标志（</span><span lang="EN-US">flag</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">），哈希值</span></p>
</td>
</tr>
<tr>
<td style="width: 97.55pt; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-right-width: 1pt; border-bottom-width: 1pt; border-left-width: 1pt; border-top-style: none; padding: 0cm 5.4pt;" valign="top" width="130">
<p class="MsoNormal"><span lang="EN-US">ModuleRef</span></p>
</td>
<td style="width: 328.55pt; border-top-style: none; border-left-style: none; border-bottom-color: windowtext; border-bottom-width: 1pt; border-right-color: windowtext; border-right-width: 1pt; padding: 0cm 5.4pt;" valign="top" width="438">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">实现该模块所引用的类型的的每个</span><span lang="EN-US">PE</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">模块在这个表中都有一个记录项；</span></p>
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">包含：模块的文件名，扩展名（不含路径）</span></p>
</td>
</tr>
<tr>
<td style="width: 97.55pt; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-right-width: 1pt; border-bottom-width: 1pt; border-left-width: 1pt; border-top-style: none; padding: 0cm 5.4pt;" valign="top" width="130">
<p class="MsoNormal"><span lang="EN-US">TypeRef</span></p>
</td>
<td style="width: 328.55pt; border-top-style: none; border-left-style: none; border-bottom-color: windowtext; border-bottom-width: 1pt; border-right-color: windowtext; border-right-width: 1pt; padding: 0cm 5.4pt;" valign="top" width="438">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">模块引用的每个类型在这个表中都有一个记录项；</span></p>
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">包含：类型的名称，一个引用（指向类型的位置）</span></p>
</td>
</tr>
<tr>
<td style="width: 97.55pt; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-right-width: 1pt; border-bottom-width: 1pt; border-left-width: 1pt; border-top-style: none; padding: 0cm 5.4pt;" valign="top" width="130">
<p class="MsoNormal"><span lang="EN-US">MemberRef</span></p>
</td>
<td style="width: 328.55pt; border-top-style: none; border-left-style: none; border-bottom-color: windowtext; border-bottom-width: 1pt; border-right-color: windowtext; border-right-width: 1pt; padding: 0cm 5.4pt;" valign="top" width="438">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">模块引用的每个成员（字段和方法以及属性方法和事件方法）在这个表中都有一个记录项；</span></p>
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">包含：成员的名称，签名，并指向对成员进行定义的那个类型的</span><span lang="EN-US">TypeRef</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">记录项</span></p>
</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<p class="MsoNormal"><span lang="EN-US">&nbsp;</span></p>
<p>3，清单元数据表</p>
<table class="MsoTableGrid" style="border: none; height: 334px; width: 797px;" border="1" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td style="width: 97.55pt; border-color: windowtext; border-width: 1pt; padding: 0cm 5.4pt;" valign="top" width="130">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">清单元数据表名称</span></p>
</td>
<td style="width: 328.55pt; border-top-color: windowtext; border-right-color: windowtext; border-bottom-color: windowtext; border-top-width: 1pt; border-right-width: 1pt; border-bottom-width: 1pt; border-left-style: none; padding: 0cm 5.4pt;" valign="top" width="438">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">说明</span></p>
</td>
</tr>
<tr>
<td style="width: 97.55pt; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-right-width: 1pt; border-bottom-width: 1pt; border-left-width: 1pt; border-top-style: none; padding: 0cm 5.4pt;" valign="top" width="130">
<p class="MsoNormal"><span lang="EN-US">AssemblyDef</span></p>
</td>
<td style="width: 328.55pt; border-top-style: none; border-left-style: none; border-bottom-color: windowtext; border-bottom-width: 1pt; border-right-color: windowtext; border-right-width: 1pt; padding: 0cm 5.4pt;" valign="top" width="438">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">如果模块标识的是程序集，这个元数据表就包含单一记录项来列出程序集名称（不含路径和扩展名），版本（</span><span lang="EN-US">major</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">，</span><span lang="EN-US">minor</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">，</span><span lang="EN-US">build</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">和</span><span lang="EN-US">revision</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">），语言文化（</span><span lang="EN-US">culture</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">），一些标志（</span><span lang="EN-US">flag</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">），哈希算法以及发布者公钥（可为</span><span lang="EN-US">null</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">）</span></p>
</td>
</tr>
<tr>
<td style="width: 97.55pt; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-right-width: 1pt; border-bottom-width: 1pt; border-left-width: 1pt; border-top-style: none; padding: 0cm 5.4pt;" valign="top" width="130">
<p class="MsoNormal"><span lang="EN-US">FieldDef</span></p>
</td>
<td style="width: 328.55pt; border-top-style: none; border-left-style: none; border-bottom-color: windowtext; border-bottom-width: 1pt; border-right-color: windowtext; border-right-width: 1pt; padding: 0cm 5.4pt;" valign="top" width="438">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">作为程序集一部分的每个</span><span lang="EN-US">PE</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">文件和资源文件在这个表中都有一个记录项（清单本身所在的文件除外，该文件在</span><span lang="EN-US">AssemplyDef</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">表的单一记录项中列出）；</span></p>
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">包含：文件名，扩展名（不含路径），哈希值和一些标志（</span><span lang="EN-US">flags</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">）；</span></p>
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">如果程序集只包含它自己的文件，</span><span lang="EN-US">FileDef</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">表将无记录</span></p>
</td>
</tr>
<tr>
<td style="width: 97.55pt; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-right-width: 1pt; border-bottom-width: 1pt; border-left-width: 1pt; border-top-style: none; padding: 0cm 5.4pt;" valign="top" width="130">
<p class="MsoNormal"><span lang="EN-US">ManifestResourceDef</span></p>
</td>
<td style="width: 328.55pt; border-top-style: none; border-left-style: none; border-bottom-color: windowtext; border-bottom-width: 1pt; border-right-color: windowtext; border-right-width: 1pt; padding: 0cm 5.4pt;" valign="top" width="438">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">作为程序集一部分的每个资源在这个表中都有一个记录项；</span></p>
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">包含：资源名称，标志，</span><span lang="EN-US">FileDef</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">表的一个索引，偏移量（指出资源在</span><span lang="EN-US">PE</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">文件中的起始位置）</span></p>
</td>
</tr>
<tr>
<td style="width: 97.55pt; border-right-color: windowtext; border-bottom-color: windowtext; border-left-color: windowtext; border-right-width: 1pt; border-bottom-width: 1pt; border-left-width: 1pt; border-top-style: none; padding: 0cm 5.4pt;" valign="top" width="130">
<p class="MsoNormal"><span lang="EN-US">ExportedTypesDef</span></p>
</td>
<td style="width: 328.55pt; border-top-style: none; border-left-style: none; border-bottom-color: windowtext; border-bottom-width: 1pt; border-right-color: windowtext; border-right-width: 1pt; padding: 0cm 5.4pt;" valign="top" width="438">
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">从程序集的所有</span><span lang="EN-US">PE</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">模块中导出的每个</span><span lang="EN-US">public</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">类型在这个表中都有一个记录项；</span></p>
<p class="MsoNormal"><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">包含：类型名称，</span><span lang="EN-US">FileDef</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">表的一个索引，</span><span lang="EN-US">TypeDef</span><span style="font-family: 宋体; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-fareast-font-family: 宋体; mso-fareast-theme-font: minor-fareast; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin;">表的一个索引</span></p>
</td>
</tr>
</tbody>
</table>
<p>4，利用<a href="http://pan.baidu.com/s/1bQEtcU" target="_blank">ILDasm.exe</a>查看元数据</p>
<p>视图-》元信息-》显示</p>
<p>&nbsp;</p>