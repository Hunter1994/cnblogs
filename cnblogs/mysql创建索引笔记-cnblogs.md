<p>1.添加PRIMARY KEY（主键索引。就是 唯一 且 不能为空。）：</p>
<p>ALTER TABLE `table_name` ADD PRIMARY KEY ( `column` )&nbsp;</p>
<p>2.添加UNIQUE(唯一索引)&nbsp;：</p>
<div>ALTER TABLE `table_name` ADD UNIQUE (&nbsp;`column`&nbsp;)&nbsp;</div>
<div>&nbsp;</div>
<div>3.添加INDEX(普通索引) ：</div>
<div>ALTER TABLE `table_name` ADD INDEX index_name ( `column` )</div>
<div>&nbsp;</div>
<div>4.添加FULLTEXT(全文索引，是全文索引，用于在一篇文章中，检索文本信息的。) ：</div>
<div>ALTER TABLE `table_name` ADD FULLTEXT ( `column`)&nbsp;</div>
<div>&nbsp;</div>
<div>5.添加多列索引：</div>
<div>ALTER TABLE `table_name` ADD INDEX index_name ( `column1`, `column2`, `column3` )</div>
<div>&nbsp;</div>
<div>6,临时表使用</div>
<div>
<p>create TEMPORARY table temp_1 like user<br />create TEMPORARY table temp_2 like project</p>
<p>insert into temp_1<br /> select * from (<br />select * from user where usertype=8<br />and uid not in (<br />select uid from po_user) order by create_time desc) a</p>
<p>insert into temp_2 select * from project where response_code in(<br />select username from temp_1<br />)</p>
<p>insert into po_user(uid,pid,project_name,is_deleted,last_modify_time,last_modify_user) </p>
<p>select uid,pid,project_name,1 as is_deleted,now() as last_modify_time,'手动修复数据' as last_modify_user from temp_1<br />join temp_2 on temp_1.username =temp_2.response_code</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>select * from po_user</p>
<p>&nbsp;</p>
&nbsp;</div>