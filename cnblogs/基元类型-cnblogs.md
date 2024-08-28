<p>什么是基元类型？<br />编译器直接支持的数据类型</p>
<table style="height: 837px; width: 765px;" border="1" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td valign="top" width="142">
<p><strong>C#</strong><strong>基元类型</strong></p>

</td>
<td valign="top" width="142">
<p><strong>FCL</strong><strong>类型</strong></p>

</td>
<td valign="top" width="142">
<p><strong>符合CLS</strong></p>

</td>
<td valign="top" width="142">
<p><strong>说明</strong></p>

</td>

</tr>
<tr>
<td valign="top" width="142">
<p><strong>Sbyte</strong></p>

</td>
<td valign="top" width="142">
<p>System.SByte</p>

</td>
<td valign="top" width="142">
<p>否</p>

</td>
<td valign="top" width="142">
<p>有符号8位值</p>

</td>

</tr>
<tr>
<td valign="top" width="142">
<p><strong>byte</strong></p>

</td>
<td valign="top" width="142">
<p>System.Byte</p>

</td>
<td valign="top" width="142">
<p>是</p>

</td>
<td valign="top" width="142">
<p>无符号8位值</p>

</td>

</tr>
<tr>
<td valign="top" width="142">
<p><strong>Short</strong></p>

</td>
<td valign="top" width="142">
<p>System.Int16</p>

</td>
<td valign="top" width="142">
<p>是</p>

</td>
<td valign="top" width="142">
<p>有符号16位值</p>

</td>

</tr>
<tr>
<td valign="top" width="142">
<p><strong>Ushort</strong></p>

</td>
<td valign="top" width="142">
<p>System.UInt16</p>

</td>
<td valign="top" width="142">
<p>否</p>

</td>
<td valign="top" width="142">
<p>无符号16位值</p>

</td>

</tr>
<tr>
<td valign="top" width="142">
<p><strong>Int</strong></p>

</td>
<td valign="top" width="142">
<p>System.Int32</p>

</td>
<td valign="top" width="142">
<p>是</p>

</td>
<td valign="top" width="142">
<p>有符号32位值</p>

</td>

</tr>
<tr>
<td valign="top" width="142">
<p><strong>uint</strong></p>

</td>
<td valign="top" width="142">
<p>System.UInt32</p>

</td>
<td valign="top" width="142">
<p>否</p>

</td>
<td valign="top" width="142">
<p>无符号32位值</p>

</td>

</tr>
<tr>
<td valign="top" width="142">
<p><strong>long</strong></p>

</td>
<td valign="top" width="142">
<p>System.Int64</p>

</td>
<td valign="top" width="142">
<p>是</p>

</td>
<td valign="top" width="142">
<p>有符号64位值</p>

</td>

</tr>
<tr>
<td valign="top" width="142">
<p><strong>ulong</strong></p>

</td>
<td valign="top" width="142">
<p>System.Uint64</p>

</td>
<td valign="top" width="142">
<p>否</p>

</td>
<td valign="top" width="142">
<p>无符号64位值</p>

</td>

</tr>
<tr>
<td valign="top" width="142">
<p><strong>char</strong></p>

</td>
<td valign="top" width="142">
<p>System.Char</p>

</td>
<td valign="top" width="142">
<p>是</p>

</td>
<td valign="top" width="142">
<p>16位Unicode字符（char不像在非托管c++zhong那样代表一个8位值）</p>

</td>

</tr>
<tr>
<td valign="top" width="142">
<p><strong>float</strong></p>

</td>
<td valign="top" width="142">
<p>System.Singe</p>

</td>
<td valign="top" width="142">
<p>是</p>

</td>
<td valign="top" width="142">
<p>IEEE32位浮点值</p>

</td>

</tr>
<tr>
<td valign="top" width="142">
<p><strong>double</strong></p>

</td>
<td valign="top" width="142">
<p>System.Double</p>

</td>
<td valign="top" width="142">
<p>是</p>

</td>
<td valign="top" width="142">
<p>IEEE64位浮点值</p>

</td>

</tr>
<tr>
<td valign="top" width="142">
<p><strong>decimal</strong></p>

</td>
<td valign="top" width="142">
<p>System.Decimal</p>

</td>
<td valign="top" width="142">
<p>是</p>

</td>
<td valign="top" width="142">
<p>128位高精度浮点值，常用于不容许舍入差的金融计算。128位中，1位是符号，96位是值本身（N），8位是比例因子（k）</p>

</td>

</tr>
<tr>
<td valign="top" width="142">
<p><strong>string</strong></p>

</td>
<td valign="top" width="142">
<p>System.String</p>

</td>
<td valign="top" width="142">
<p>是</p>

</td>
<td valign="top" width="142">
<p>字符数组</p>

</td>

</tr>
<tr>
<td valign="top" width="142">
<p><strong>object</strong></p>

</td>
<td valign="top" width="142">
<p>System.Object</p>

</td>
<td valign="top" width="142">
<p>是</p>

</td>
<td valign="top" width="142">
<p>所有类型的基类型</p>

</td>

</tr>
<tr>
<td valign="top" width="142">
<p><strong>dynamic</strong></p>

</td>
<td valign="top" width="142">
<p>System.Object</p>

</td>
<td valign="top" width="142">
<p>是</p>

</td>
<td valign="top" width="142">
<p>对于CLR，dynam和object完全一致。但C#编译器允许使用简单的语法当dynamic变量参与动态调度</p>

</td>

</tr>

</tbody>

</table>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>可以认为C#编译器自动假定所有源代码文件都添加了一下using指令</p>
<p>using sbyte=System.SByte;</p>
<p>using int=System.Int32</p>
<p>...</p>
<p>&nbsp;</p>