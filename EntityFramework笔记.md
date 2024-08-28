<p>参照文档：<a href="http://www.cnblogs.com/farb/p/ABPAdvancedTheoryContent.html" target="_blank">&nbsp;http://www.cnblogs.com/farb/p/ABPAdvancedTheoryContent.html</a></p>
<p>案例：<a href="http://pan.baidu.com/s/1c1Qgg28" target="_blank">http://pan.baidu.com/s/1c1Qgg28</a></p>
<p>&nbsp;</p>
<p><a href="#1"><strong>一、领域建模和管理实体关系</strong></a></p>
<p><a href="#2"><strong><strong>二、&nbsp;使用LINQ to Entities操作实体</strong></strong></a></p>
<p><a href="#3"><strong>三、预加载</strong></a></p>
<p><a href="#4"><strong><strong>四、CURD</strong></strong></a></p>
<p><a href="#5"><strong>五、EF使用视图</strong></a></p>
<p><a href="#6"><strong><strong>六、EF使用存储过程</strong></strong></a></p>
<p><a href="#7"><strong>七、异步API</strong></a></p>
<p><a href="#8"><strong><strong>八、管理并发</strong></strong></a></p>
<p><a href="#9"><strong>九、事务</strong></a></p>
<p><a href="#10"><strong>十、数据库迁移</strong></a></p>
<p><a href="#11"><strong><strong>十一、应用迁移</strong></strong></a></p>
<p><a href="#12"><strong><strong><strong>十二、EF的其他功能</strong></strong></strong></a></p>
<p>&nbsp;</p>
<p><a name="1"></a></p>
<p style="background-color: #169fe6;"><strong><span style="color: #ffffff; font-size: 18pt;">一、领域建模和管理实体关系</span></strong></p>
<p><strong><span style="font-size: 14pt;">&nbsp;1，流利地配置领域类到数据库模式的映射</span></strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> FirstCodeFirstApp
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Context:DbContext
    {
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Context()
            : </span><span style="color: #0000ff;">base</span>(<span style="color: #800000;">"</span><span style="color: #800000;">name=FirstCodeFirstApp</span><span style="color: #800000;">"</span><span style="color: #000000;">)
        {
        }

        </span><span style="color: #0000ff;">public</span> DbSet&lt;Donator&gt; Donators { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
        </span><span style="color: #0000ff;">public</span> DbSet&lt;PayWay&gt; PayWays { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

        </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> OnModelCreating(DbModelBuilder modelBuilder)
        {
            modelBuilder.Entity</span>&lt;Donator&gt;().ToTable(<span style="color: #800000;">"</span><span style="color: #800000;">Donators</span><span style="color: #800000;">"</span>).HasKey(m =&gt; m.DonatorId);<span style="color: #008000;">//</span><span style="color: #008000;">映射到表Donators,DonatorId当作主键对待</span>
            modelBuilder.Entity&lt;Donator&gt;().Property(m =&gt; m.DonatorId).HasColumnName(<span style="color: #800000;">"</span><span style="color: #800000;">Id</span><span style="color: #800000;">"</span>);<span style="color: #008000;">//</span><span style="color: #008000;">映射到数据表中的主键名为Id而不是DonatorId</span>
            modelBuilder.Entity&lt;Donator&gt;().Property(m =&gt;<span style="color: #000000;"> m.Name)
                .IsRequired()</span><span style="color: #008000;">//</span><span style="color: #008000;">设置Name是必须的，即不为null,默认是可为null的</span>
                .IsUnicode()<span style="color: #008000;">//</span><span style="color: #008000;">设置Name列为Unicode字符，实际上默认就是unicode,所以该方法可不写</span>
                .HasMaxLength(<span style="color: #800080;">10</span>);<span style="color: #008000;">//</span><span style="color: #008000;">最大长度为10</span>

            <span style="color: #0000ff;">base</span><span style="color: #000000;">.OnModelCreating(modelBuilder);
        }
    }
}</span></pre>
</div>
<p><span style="font-size: 14px;">1.1，每个实体类单独创建一个配置类。然后再在<code>OnModelCreating</code>方法中调用这些配置伙伴类</span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> DonatorMap:EntityTypeConfiguration&lt;Donator&gt;<span style="color: #000000;">
{
    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> DonatorMap()
    {
        ToTable(</span><span style="color: #800000;">"</span><span style="color: #800000;">DonatorFromConfig</span><span style="color: #800000;">"</span>);<span style="color: #008000;">//</span><span style="color: #008000;">为了区分之前的结果</span>
        Property(m =&gt;<span style="color: #000000;"> m.Name)
            .IsRequired()</span><span style="color: #008000;">//</span><span style="color: #008000;">将Name设置为必须的</span>
            .HasColumnName(<span style="color: #800000;">"</span><span style="color: #800000;">DonatorName</span><span style="color: #800000;">"</span>);<span style="color: #008000;">//</span><span style="color: #008000;">为了区别之前的结果，将Name映射到数据表的DonatorName</span>
<span style="color: #000000;">    }
}</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> OnModelCreating(DbModelBuilder modelBuilder)
{
       modelBuilder.Configurations.Add(</span><span style="color: #0000ff;">new</span><span style="color: #000000;"> DonatorMap());
       </span><span style="color: #0000ff;">base</span><span style="color: #000000;">.OnModelCreating(modelBuilder);
}</span></pre>
</div>
<p><strong><span style="font-size: 18px;">&nbsp;2，一对多关系</span></strong></p>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> OnModelCreating(DbModelBuilder modelBuilder)
        {
            modelBuilder.Entity</span>&lt;Donator&gt;().HasMany(r =&gt; r.PayWays)<span style="color: #008000;">//</span><span style="color: #008000;">HasMany方法告诉EF在Donator和Payway类之间有一个一对多的关系</span>
                .WithRequired()<span style="color: #008000;">//</span><span style="color: #008000;">WithRequired方法表明链接在PayWays属性上的Donator是必须的,换言之，Payway对象不是独立的对象，必须要链接到一个Donator</span>
                .HasForeignKey(r =&gt; r.DonatorId);<span style="color: #008000;">//</span><span style="color: #008000;">HasForeignKey方法会识别哪一个属性会作为链接</span>
            <span style="color: #0000ff;">base</span><span style="color: #000000;">.OnModelCreating(modelBuilder);
        }</span></pre>
</div>
<p>2.1，指定约束的删除规则</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> DonatorTypeMap:EntityTypeConfiguration&lt;DonatorType&gt;<span style="color: #000000;">
{
    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> DonatorTypeMap()
    {
        HasMany(dt</span>=&gt;<span style="color: #000000;">dt.Donators)
            .WithOptional(d</span>=&gt;<span style="color: #000000;">d.DonatorType)
            .HasForeignKey(d</span>=&gt;<span style="color: #000000;">d.DonatorTypeId)
            .WillCascadeOnDelete(</span><span style="color: #0000ff;">false</span><span style="color: #000000;">);//指定约束的删除规则
    }
}</span></pre>
</div>
<p>2.2调用<code>WillCascadeOnDelete</code>的另一种选择是，从 model builder中移除全局的约定，在数据库上下文的<code>OnModelCreating</code>方法中关闭整个数据库模型的级联删除规则</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> OnModelCreating(DbModelBuilder modelBuilder)
{

    modelBuilder.Configurations.Add(</span><span style="color: #0000ff;">new</span><span style="color: #000000;"> DonatorMap());
    modelBuilder.Configurations.Add(</span><span style="color: #0000ff;">new</span><span style="color: #000000;"> DonatorTypeMap());
    modelBuilder.Conventions.Remove</span>&lt;OneToManyCascadeDeleteConvention&gt;<span style="color: #000000;">();
    modelBuilder.Conventions.Remove</span>&lt;ManyToManyCascadeDeleteConvention&gt;<span style="color: #000000;">();
    </span><span style="color: #0000ff;">base</span><span style="color: #000000;">.OnModelCreating(modelBuilder);
}</span></pre>
</div>
<p>&nbsp;2.3创建一对多关系的代码</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">#region</span> 6.1 一对多关系 例子2

<span style="color: #0000ff;">var</span> donatorType = <span style="color: #0000ff;">new</span><span style="color: #000000;"> DonatorType
{
    Name </span>= <span style="color: #800000;">"</span><span style="color: #800000;">博客园园友</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    Donators </span>= <span style="color: #0000ff;">new</span> List&lt;Donator&gt;<span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> Donator
        {
            Amount </span>=<span style="color: #800080;">6</span>,Name = <span style="color: #800000;">"</span><span style="color: #800000;">键盘里的鼠标</span><span style="color: #800000;">"</span>,DonateDate =DateTime.Parse(<span style="color: #800000;">"</span><span style="color: #800000;">2016-4-13</span><span style="color: #800000;">"</span><span style="color: #000000;">),
            PayWays </span>= <span style="color: #0000ff;">new</span> List&lt;PayWay&gt;{<span style="color: #0000ff;">new</span> PayWay{Name = <span style="color: #800000;">"</span><span style="color: #800000;">支付宝</span><span style="color: #800000;">"</span>},<span style="color: #0000ff;">new</span> PayWay{Name = <span style="color: #800000;">"</span><span style="color: #800000;">微信</span><span style="color: #800000;">"</span><span style="color: #000000;">}}
        }     
    }
};
</span><span style="color: #0000ff;">var</span> donatorType2 = <span style="color: #0000ff;">new</span><span style="color: #000000;"> DonatorType
{
    Name </span>= <span style="color: #800000;">"</span><span style="color: #800000;">非博客园园友</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    Donators </span>= <span style="color: #0000ff;">new</span> List&lt;Donator&gt;<span style="color: #000000;">
    {

         </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> Donator
        {
            Amount </span>=<span style="color: #800080;">10</span>,Name = <span style="color: #800000;">"</span><span style="color: #800000;">待赞助</span><span style="color: #800000;">"</span>,DonateDate =DateTime.Parse(<span style="color: #800000;">"</span><span style="color: #800000;">2016-4-27</span><span style="color: #800000;">"</span><span style="color: #000000;">),
            PayWays </span>= <span style="color: #0000ff;">new</span> List&lt;PayWay&gt;{<span style="color: #0000ff;">new</span> PayWay{Name = <span style="color: #800000;">"</span><span style="color: #800000;">支付宝</span><span style="color: #800000;">"</span>},<span style="color: #0000ff;">new</span> PayWay{Name = <span style="color: #800000;">"</span><span style="color: #800000;">微信</span><span style="color: #800000;">"</span><span style="color: #000000;">}}
        }
        
    }
};
context.DonatorTypes.Add(donatorType);
context.DonatorTypes.Add(donatorType2);
context.SaveChanges();</span></pre>
</div>
<p>&nbsp;<img src="http://images2017.cnblogs.com/blog/741594/201708/741594-20170823151207058-808999523.png" alt="" /></p>
<p><strong><span style="font-size: 14pt;">3，一对一关系</span></strong></p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201708/741594-20170831180828765-1768322651.png" alt="" /></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Person
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span> PersonId { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Name { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">bool</span> IsActive { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">virtual</span> Student Student { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}


</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Student
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span> PersonId { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">virtual</span> Person Person { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> CollegeName { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    </span><span style="color: #0000ff;">public</span> DateTime EnrollmentDate { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> StudentMap:EntityTypeConfiguration&lt;Student&gt;<span style="color: #000000;">
{
    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> StudentMap()
    {
        HasRequired(s</span>=&gt;<span style="color: #000000;">s.Person)
            .WithOptional(p</span>=&gt;<span style="color: #000000;">p.Student);//一或零对一
        HasKey(s </span>=&gt;<span style="color: #000000;"> s.PersonId);
        Property(s </span>=&gt;<span style="color: #000000;"> s.CollegeName)
            .HasMaxLength(</span><span style="color: #800080;">50</span><span style="color: #000000;">)
            .IsRequired();
    }
}</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> student = <span style="color: #0000ff;">new</span><span style="color: #000000;"> Student
{
    CollegeName </span>= <span style="color: #800000;">"</span><span style="color: #800000;">XX大学</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    EnrollmentDate </span>= DateTime.Parse(<span style="color: #800000;">"</span><span style="color: #800000;">2011-11-11</span><span style="color: #800000;">"</span><span style="color: #000000;">),
    Person </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> Person
    {
        Name </span>= <span style="color: #800000;">"</span><span style="color: #800000;">Farb</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    }
};

context.Students.Add(student);
context.SaveChanges();</span></pre>
</div>
<p><strong><span style="font-size: 14pt;">4,多对多</span></strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Company
{
     </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Company()
     {
        Persons </span>= <span style="color: #0000ff;">new</span> HashSet&lt;Person&gt;<span style="color: #000000;">();
     }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span> CompanyId { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> CompanyName { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">virtual</span> ICollection &lt;Person&gt; Persons { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Person
{
    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Person()
    {
        Companies</span>=<span style="color: #0000ff;">new</span> HashSet&lt;Company&gt;<span style="color: #000000;">();
    }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span> PersonId { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Name { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">bool</span> IsActive { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">virtual</span> Student Student { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">virtual</span> ICollection&lt;Company&gt; Companies { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> PersonMap:EntityTypeConfiguration&lt;Person&gt;<span style="color: #000000;">
{
    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> PersonMap()
    {
        HasMany(p </span>=&gt;<span style="color: #000000;"> p.Companies)
            .WithMany(c </span>=&gt;<span style="color: #000000;"> c.Persons)
            .Map(m </span>=&gt;<span style="color: #000000;">
            {
                m.MapLeftKey(</span><span style="color: #800000;">"</span><span style="color: #800000;">PersonId</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                m.MapRightKey(</span><span style="color: #800000;">"</span><span style="color: #800000;">CompanyId</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            });
    }
}</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">#region</span> 8 多对多关系

<span style="color: #0000ff;">var</span> person = <span style="color: #0000ff;">new</span><span style="color: #000000;"> Person
{
    Name </span>= <span style="color: #800000;">"</span><span style="color: #800000;">比尔盖茨</span><span style="color: #800000;">"</span><span style="color: #000000;">,
};
</span><span style="color: #0000ff;">var</span> person2 = <span style="color: #0000ff;">new</span><span style="color: #000000;"> Person
{
    Name </span>= <span style="color: #800000;">"</span><span style="color: #800000;">乔布斯</span><span style="color: #800000;">"</span><span style="color: #000000;">,
};
context.People.Add(person);
context.People.Add(person2);
</span><span style="color: #0000ff;">var</span> company = <span style="color: #0000ff;">new</span><span style="color: #000000;"> Company
{
    CompanyName </span>= <span style="color: #800000;">"</span><span style="color: #800000;">微软</span><span style="color: #800000;">"</span><span style="color: #000000;">
};
company.Persons.Add(person);
context.Companies.Add(company);
context.SaveChanges();

</span><span style="color: #0000ff;">#endregion</span></pre>
</div>
<p><img src="http://images2017.cnblogs.com/blog/741594/201708/741594-20170831181305765-19039498.png" alt="" /></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;如果我们连接表需要保存更多的数据怎么办？比如当每个人开始为公司干活时，我们想为他们添加雇佣日期。这样的话，实际上我们需要创建一个类来模型化该连接表，我们暂且称为PersonCompany吧。它仍然具有两个的主键属性，PersonId和CompanyId，它还有Person和Company的属性以及雇佣日期的属性。此外，Person和Company类分别都有PersonCompanies的集合属性而不是单独的Person和Company集合属性。</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p><strong><span style="font-size: 18px;">&nbsp;5，Table per Type(TPT)继承</span></strong></p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201708/741594-20170823160707043-841777042.png" alt="" /><img src="http://images2017.cnblogs.com/blog/741594/201708/741594-20170823160812808-12119182.png" alt="" /></p>
<p>&nbsp;派生类加上数据注解，表明他们是独立的表</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Person
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span> Id { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Name { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Email { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> PhoneNumber { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}

[Table(</span><span style="color: #800000;">"</span><span style="color: #800000;">Employees</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Employee : Person
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">decimal</span> Salary { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}

[Table(</span><span style="color: #800000;">"</span><span style="color: #800000;">Vendors</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
 </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Vendor : Person
 {
     </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">decimal</span> HourlyRate { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
 }</span></pre>
</div>
<div class="cnblogs_code">
<pre> <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Context:DbContext
 {
     </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">virtual</span> DbSet&lt;Person&gt; People { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }//上面的上下文中，我们只添加了实体Person的DbSet。因为其它的两个领域模型都是从这个模型派生的，所以我们也就相当于将其它两个类添加到了DbSet集合中了，这样EF会使用多 态性来使用实际的领域模型
 }</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">#region</span> 1.0  TPT继承

<span style="color: #0000ff;">var</span> employee = <span style="color: #0000ff;">new</span><span style="color: #000000;"> Employee
{
    Name </span>= <span style="color: #800000;">"</span><span style="color: #800000;">farb</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    Email </span>= <span style="color: #800000;">"</span><span style="color: #800000;">farbguo@qq.com</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    PhoneNumber </span>= <span style="color: #800000;">"</span><span style="color: #800000;">12345678</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    Salary </span>=<span style="color: #000000;"> 1234m
};

</span><span style="color: #0000ff;">var</span> vendor = <span style="color: #0000ff;">new</span><span style="color: #000000;"> Vendor
{
    Name </span>= <span style="color: #800000;">"</span><span style="color: #800000;">tkb至简</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    Email </span>= <span style="color: #800000;">"</span><span style="color: #800000;">farbguo@outlook.com</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    PhoneNumber </span>= <span style="color: #800000;">"</span><span style="color: #800000;">78956131</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    HourlyRate </span>=<span style="color: #000000;"> 4567m
};

context.People.Add(employee);
context.People.Add(vendor);
context.SaveChanges();
</span><span style="color: #0000ff;">#endregion</span></pre>
</div>
<p><strong><span style="font-size: 18px;">&nbsp;</span></strong></p>
<p><strong><span style="font-size: 18px;">6，Table per Class Hierarchy(TPH)继承</span></strong></p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201708/741594-20170823160916839-1552673044.png" alt="" /></p>
<p>&nbsp;</p>
<p>&nbsp;未使用数据注解指点派生类的表明</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Person
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span> Id { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Name { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Email { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> PhoneNumber { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}


 </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Employee : Person
 {
     </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">decimal</span> Salary { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
 }


</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Vendor : Person
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">decimal</span> HourlyRate { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Context:DbContext
{
    </span><span style="color: #0000ff;">public</span> Context():<span style="color: #0000ff;">base</span>(<span style="color: #800000;">"</span><span style="color: #800000;">ThreeInheritance</span><span style="color: #800000;">"</span><span style="color: #000000;">)
    {
        
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">virtual</span> DbSet&lt;Person&gt; Person { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">#region</span> 2.0 TPH 继承
  <span style="color: #0000ff;">var</span> employee = <span style="color: #0000ff;">new</span><span style="color: #000000;"> Employee
  {
      Name </span>= <span style="color: #800000;">"</span><span style="color: #800000;">farb</span><span style="color: #800000;">"</span><span style="color: #000000;">,
      Email </span>= <span style="color: #800000;">"</span><span style="color: #800000;">farbguo@qq.com</span><span style="color: #800000;">"</span><span style="color: #000000;">,
      PhoneNumber </span>= <span style="color: #800000;">"</span><span style="color: #800000;">12345678</span><span style="color: #800000;">"</span><span style="color: #000000;">,
      Salary </span>=<span style="color: #000000;"> 1234m
  };
 
  </span><span style="color: #0000ff;">var</span> vendor = <span style="color: #0000ff;">new</span><span style="color: #000000;"> Vendor
  {
      Name </span>= <span style="color: #800000;">"</span><span style="color: #800000;">tkb至简</span><span style="color: #800000;">"</span><span style="color: #000000;">,
      Email </span>= <span style="color: #800000;">"</span><span style="color: #800000;">farbguo@outlook.com</span><span style="color: #800000;">"</span><span style="color: #000000;">,
      PhoneNumber </span>= <span style="color: #800000;">"</span><span style="color: #800000;">78956131</span><span style="color: #800000;">"</span><span style="color: #000000;">,
      HourlyRate </span>=<span style="color: #000000;"> 4567m
  };
 
  context.Person.Add(employee);
  context.Person.Add(vendor);
  context.SaveChanges();
 </span><span style="color: #0000ff;">#endregion</span></pre>
</div>
<p><img src="http://images2017.cnblogs.com/blog/741594/201708/741594-20170823162543480-1495924357.png" alt="" /></p>
<p>&nbsp;</p>
<p><span style="font-size: 18px;"><strong>7，Table per Concrete Class(TPC)继承</strong></span></p>
<p>如果我们想使用TPC继承，那么要么使用基于GUID的Id，要么从应用程序中传入Id，或者使用能够维护对多张表自动生成的列的唯一性的某些数据库机制</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201708/741594-20170823162727808-1441050209.png" alt="" /></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Person
{
    [DatabaseGenerated(DatabaseGeneratedOption.Identity)]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span> Id { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Name { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Email { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> PhoneNumber { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Vendor : Person
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">decimal</span> HourlyRate { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Employee : Person
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">decimal</span> Salary { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">virtual</span> DbSet&lt;Person&gt; People { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

</span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> OnModelCreating(DbModelBuilder modelBuilder)
{
    modelBuilder.Entity</span>&lt;Employee&gt;().Map(m =&gt;<span style="color: #000000;">
    {
        m.MapInheritedProperties();//<code>MapInheritedProperties</code>方法将继承的属性映射到表中，然后我们根据不同的对象类型映射到不同的表中
        m.ToTable(</span><span style="color: #800000;">"</span><span style="color: #800000;">Employees</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    });

    modelBuilder.Entity</span>&lt;Vendor&gt;().Map(m =&gt;<span style="color: #000000;">
    {
        m.MapInheritedProperties();
        m.ToTable(</span><span style="color: #800000;">"</span><span style="color: #800000;">Vendors</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    });
    </span><span style="color: #0000ff;">base</span><span style="color: #000000;">.OnModelCreating(modelBuilder);
}</span></pre>
</div>
<p><a name="2"></a></p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">二、&nbsp;使用LINQ to Entities操作实体</span></strong></span></p>
<p>&nbsp;1，实现多表连接join</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> join1 = <span style="color: #0000ff;">from</span> province <span style="color: #0000ff;">in</span><span style="color: #000000;"> db.Provinces
            join donator </span><span style="color: #0000ff;">in</span><span style="color: #000000;"> db.Donators on province.Id equals donator.Province.Id
            into donatorList</span><span style="color: #008000;">//</span><span style="color: #008000;">注意，这里的donatorList是属于某个省份的所有打赏者，很多人会误解为这是两张表join之后的结果集</span>
            <span style="color: #0000ff;">select</span> <span style="color: #0000ff;">new</span><span style="color: #000000;">
            {
                ProvinceName </span>=<span style="color: #000000;"> province.ProvinceName,
                DonatorList </span>=<span style="color: #000000;"> donatorList
            };

</span><span style="color: #0000ff;">var</span> join2 = db.Provinces.GroupJoin(db.Donators,<span style="color: #008000;">//</span><span style="color: #008000;">Provinces集合要连接的Donators实体集合</span>
    province =&gt; province.Id,<span style="color: #008000;">//</span><span style="color: #008000;">左表要连接的键</span>
    donator =&gt; donator.Province.Id,<span style="color: #008000;">//</span><span style="color: #008000;">右表要连接的键</span>
    (province, donatorGroup) =&gt; <span style="color: #0000ff;">new</span><span style="color: #008000;">//</span><span style="color: #008000;">返回的结果集</span>
<span style="color: #000000;">    {
        ProvinceName </span>=<span style="color: #000000;"> province.ProvinceName,
        DonatorList </span>=<span style="color: #000000;"> donatorGroup
    }
    );</span></pre>
</div>
<p><a name="3"></a></p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">三、预加载</span></strong></p>
<p>&nbsp;预加载是这样一种过程，当我们要加载查询中的主要实体时，同时也加载与之相关的实体。要实现预加载，我们要使用<code>Include</code>方法。下面我们看一下如何在加载Donator数据的时候，同时也预先加载所有的Provinces数据：</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">预加载,以下两种方式都可以</span>
<span style="color: #0000ff;">var</span> donators2 = db.Donators.Include(d =&gt;<span style="color: #000000;"> d.Province).ToList();
</span><span style="color: #0000ff;">var</span> donators3 = db.Donators.Include(<span style="color: #800000;">"</span><span style="color: #800000;">Provinces</span><span style="color: #800000;">"</span>).ToList();</pre>
</div>
<p>这样，当我们从数据库中取到Donators集合时，也取到了Provinces集合。</p>
<p>&nbsp;</p>
<p><a name="4"></a></p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;"><strong>四、CURD</strong></span></p>
<table>
<thead>
<tr class="header"><th>状态</th><th>描述</th></tr>
</thead>
<tbody>
<tr class="odd">
<td>Added</td>
<td>添加了一个新的实体。该状态会导致一个插入操作。</td>
</tr>
<tr class="even">
<td>Deleted</td>
<td>将一个实体标记为删除。设置该状态时，该实体会从DbSet中移除。该状态会导致删除操作。</td>
</tr>
<tr class="odd">
<td>Detached</td>
<td>DbContext不再追踪该实体。</td>
</tr>
<tr class="even">
<td>Modified</td>
<td>自从DbContext开始追踪该实体，该实体的一个或多个属性已经更改了。该状态会导致更新操作。</td>
</tr>
<tr class="odd">
<td>Unchanged</td>
<td>自从DbContext开始追踪该实体以来，它的任何属性都没有改变。</td>
</tr>
</tbody>
</table>
<p>&nbsp;1，DbSet的<code>Attach</code>方法本质上是将实体的状态设置为<code>Unchanged</code></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> donator = <span style="color: #0000ff;">new</span><span style="color: #000000;"> Donator
{
    Id </span>= <span style="color: #800080;">4</span><span style="color: #000000;">,
    Name </span>= <span style="color: #800000;">"</span><span style="color: #800000;">雪茄</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    Amount </span>= <span style="color: #800080;">18.80m</span><span style="color: #000000;">,
    DonateDate </span>= DateTime.Parse(<span style="color: #800000;">"</span><span style="color: #800000;">2016/4/15 0:00:00</span><span style="color: #800000;">"</span><span style="color: #000000;">)
};
</span><span style="color: #0000ff;">using</span> (<span style="color: #0000ff;">var</span> db = <span style="color: #0000ff;">new</span><span style="color: #000000;"> DonatorsContext())
{
    db.Donators.Attach(donator);
    </span><span style="color: #008000;">//</span><span style="color: #008000;">db.Entry(donator).State=EntityState.Modified;</span><span style="color: #008000;">//</span><span style="color: #008000;">这句可以作为第二种方法替换上面一句代码</span>
    donator.Name = <span style="color: #800000;">"</span><span style="color: #800000;">秦皇岛-雪茄</span><span style="color: #800000;">"</span><span style="color: #000000;">;
    db.SaveChanges();
}</span></pre>
</div>
<p>2，可以使用<code>RemoveRange</code>方法删除多个实体&nbsp;</p>
<p>3，DbSet的<code>Local</code>属性强制执行一个只针对内存数据的查询</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> query= db.Provinces.Local.Where(p =&gt; p.ProvinceName.Contains(<span style="color: #800000;">"</span><span style="color: #800000;">东</span><span style="color: #800000;">"</span>)).ToList();</pre>
</div>
<p>4，<code>Find</code>方法在构建数据库查询之前，会先去本地的上下文中搜索</p>
<p>5，通过<code>ChangeTracker</code>对象，我们可以访问内存中所有实体的状态</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">using</span> (<span style="color: #0000ff;">var</span> db=<span style="color: #0000ff;">new</span><span style="color: #000000;"> DonatorsContext())
{
    </span><span style="color: #008000;">//</span><span style="color: #008000;">14.1 证明Find方法先去内存中寻找数据</span>
    <span style="color: #0000ff;">var</span> provinces =<span style="color: #000000;"> db.Provinces.ToList();
    </span><span style="color: #008000;">//</span><span style="color: #008000;">var query = db.Provinces.Find(3);</span><span style="color: #008000;">//</span><span style="color: #008000;">还剩Id=3和4的两条数据了

    </span><span style="color: #008000;">//</span><span style="color: #008000;">14.2 ChangeTracker的使用</span>
    <span style="color: #0000ff;">foreach</span> (<span style="color: #0000ff;">var</span> dbEntityEntry <span style="color: #0000ff;">in</span> db.ChangeTracker.Entries&lt;Province&gt;<span style="color: #000000;">())
    {
        Console.WriteLine(dbEntityEntry.State);
        Console.WriteLine(dbEntityEntry.Entity.ProvinceName);
    }
}
#endregio</span></pre>
</div>
<p>&nbsp;</p>
<p><a name="5"></a></p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">五、EF使用视图</span></strong></span></p>
<p>使用Database对象的另一个方法<code>SqlQuery</code>查询数据，该方法和<code>ExecuteSqlCommand</code>方法有相同的形参，但是最终返回一个结果集</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> sql = <span style="color: #800000;">@"</span><span style="color: #800000;">SELECT DonatorId ,DonatorName ,Amount ,DonateDate ,ProvinceName from dbo.DonatorViews where ProvinceName={0}</span><span style="color: #800000;">"</span><span style="color: #000000;">;
</span><span style="color: #0000ff;">var</span> donatorsViaCommand = db.Database.SqlQuery&lt;DonatorViewInfo&gt;(sql,<span style="color: #800000;">"</span><span style="color: #800000;">河北省</span><span style="color: #800000;">"</span><span style="color: #000000;">);
</span><span style="color: #0000ff;">foreach</span> (<span style="color: #0000ff;">var</span> donator <span style="color: #0000ff;">in</span><span style="color: #000000;"> donatorsViaCommand)
{
    Console.WriteLine(donator.ProvinceName </span>+ <span style="color: #800000;">"</span><span style="color: #800000;">\t</span><span style="color: #800000;">"</span> + donator.DonatorId + <span style="color: #800000;">"</span><span style="color: #800000;">\t</span><span style="color: #800000;">"</span> + donator.DonatorName + <span style="color: #800000;">"</span><span style="color: #800000;">\t</span><span style="color: #800000;">"</span> + donator.Amount + <span style="color: #800000;">"</span><span style="color: #800000;">\t</span><span style="color: #800000;">"</span> +<span style="color: #000000;"> donator.DonateDate);
}</span></pre>
</div>
<p><code>SqlQuery</code>方法的泛型参数不一定非得是一个类，也可以.Net的基本类型，如string或者int</p>
<p>&nbsp;</p>
<p><a name="6"></a></p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">六、EF使用存储过程</span></strong></span></p>
<p>1，使用SqlQuery方法</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">using</span> (<span style="color: #0000ff;">var</span> db=<span style="color: #0000ff;">new</span><span style="color: #000000;"> DonatorsContext())
{
    </span><span style="color: #0000ff;">var</span> sql = <span style="color: #800000;">"</span><span style="color: #800000;">SelectDonators {0}</span><span style="color: #800000;">"</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">var</span> donators = db.Database.SqlQuery&lt;DonatorFromStoreProcedure&gt;(sql,<span style="color: #800000;">"</span><span style="color: #800000;">山东省</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    </span><span style="color: #0000ff;">foreach</span> (<span style="color: #0000ff;">var</span> donator <span style="color: #0000ff;">in</span><span style="color: #000000;"> donators)
    {
        Console.WriteLine(donator.ProvinceName</span>+<span style="color: #800000;">"</span><span style="color: #800000;">\t</span><span style="color: #800000;">"</span>+donator.Name+<span style="color: #800000;">"</span><span style="color: #800000;">\t</span><span style="color: #800000;">"</span>+donator.Amount+<span style="color: #800000;">"</span><span style="color: #800000;">\t</span><span style="color: #800000;">"</span>+<span style="color: #000000;">donator.DonateDate);
    }
}</span></pre>
</div>
<p>假如要提供多个参数的话，多个格式化占位符必须用逗号分隔，还要给<code>SqlQuery</code>提供值的数组</p>
<p>2，使用ExecuteSqlCommand方法</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">using</span> (<span style="color: #0000ff;">var</span> db = <span style="color: #0000ff;">new</span><span style="color: #000000;"> DonatorsContext())
{
    </span><span style="color: #0000ff;">var</span> sql = <span style="color: #800000;">"</span><span style="color: #800000;">UpdateDonator {0},{1}</span><span style="color: #800000;">"</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">var</span> rowsAffected = db.Database.ExecuteSqlCommand(sql, <span style="color: #800000;">"</span><span style="color: #800000;">Update</span><span style="color: #800000;">"</span><span style="color: #000000;">, 10m);
}</span></pre>
</div>
<p>3，使用存储过程CUD</p>
<p>EF Code First全面支持这些查询。我们可以使用熟悉的<code>EntityTypeConfiguration</code>类来给存储过程配置该支持，只需要简单地调用<code>MapToStoredProcedures</code>方法就可以了</p>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> UserMap:EntityTypeConfiguration&lt;User&gt;<span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> UserMap()
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">只需要简单地调用MapToStoredProcedures方法就可以了
            </span><span style="color: #008000;">//</span><span style="color: #008000;">MapToStoredProcedures();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">自定义配置</span>
            MapToStoredProcedures(config =&gt;<span style="color: #000000;">
            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;">将删除打赏者的默认存储过程名称更改为&ldquo;DonatorDelete&rdquo;，
                </span><span style="color: #008000;">//</span><span style="color: #008000;">同时将该存储过程的参数名称更改为&ldquo;donatorId&rdquo;，并指定该值来自Id属性</span>
<span style="color: #000000;">                config.Delete(
                    procConfig </span>=&gt;<span style="color: #000000;">
                    {
                        procConfig.HasName(</span><span style="color: #800000;">"</span><span style="color: #800000;">UserDelete</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                        procConfig.Parameter(d </span>=&gt; d.Id, <span style="color: #800000;">"</span><span style="color: #800000;">userId</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                    });

                </span><span style="color: #008000;">//</span><span style="color: #008000;">将默认的插入存储过程名称更改为&ldquo;DonatorInsert&rdquo;</span>
<span style="color: #000000;">                config.Insert(
                    procConfig </span>=&gt;<span style="color: #000000;">
                    {
                        procConfig.HasName(</span><span style="color: #800000;">"</span><span style="color: #800000;">UserInsert</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                    });
                </span><span style="color: #008000;">//</span><span style="color: #008000;">将默认的更新存储过程名称更改为&ldquo;DonatorUpdate&rdquo;</span>
                config.Update(procConfig =&gt;<span style="color: #000000;">
                {
                    procConfig.HasName(</span><span style="color: #800000;">"</span><span style="color: #800000;">UserUpdate</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                });
            });
        }
    }</span></pre>
</div>
<p>&nbsp;</p>
<p><a name="7"></a></p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">七、异步API</span></strong></span></p>
<p>例如，如果使用了异步的方式在创建一个Web应用，当我们等待数据库完成处理一个请求（无论它是一个保存还是检索操作）时，通过将web工作线程释放回线程池，就可以更有效地利用服务器资源</p>
<p>&nbsp;1，异步地从数据库中获取对象的列表</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">3.1 异步查询对象列表</span>
<span style="color: #0000ff;">static</span> <span style="color: #0000ff;">async</span> Task&lt;IEnumerable&lt;Donator&gt;&gt;<span style="color: #000000;"> GetDonatorsAsync()
{
    </span><span style="color: #0000ff;">using</span> (<span style="color: #0000ff;">var</span> db = <span style="color: #0000ff;">new</span><span style="color: #000000;"> DonatorsContext())
    {
        </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">await</span><span style="color: #000000;"> db.Donators.ToListAsync();
    }
}  </span></pre>
</div>
<p>2，&nbsp;异步定位一条记录</p>
<p>我们可以异步定位一条记录，可以使用很多方法，比如<code>Single</code>或<code>First</code>，这两个方法都有异步版本。</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">3.3 异步定位一条记录</span>
<span style="color: #0000ff;">static</span> <span style="color: #0000ff;">async</span> Task&lt;Donator&gt; FindDonatorAsync(<span style="color: #0000ff;">int</span><span style="color: #000000;"> donatorId)
{
    </span><span style="color: #0000ff;">using</span> (<span style="color: #0000ff;">var</span> db = <span style="color: #0000ff;">new</span><span style="color: #000000;"> DonatorsContext())
    {
      </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">await</span><span style="color: #000000;"> db.Donators.FindAsync(donatorId);
    }
}</span></pre>
</div>
<p>3，异步聚合函数</p>
<p>对应于同步版本，异步聚合函数包括这么几个方法，<code>MaxAsync</code>,<code>MinAsync</code>,<code>CountAsync</code>,<code>SumAsync</code>,<code>AverageAsync</code>。</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">3.4 异步聚合函数</span>
<span style="color: #0000ff;">static</span> <span style="color: #0000ff;">async</span> Task&lt;<span style="color: #0000ff;">int</span>&gt;<span style="color: #000000;"> GetDonatorCountAsync()
{
    </span><span style="color: #0000ff;">using</span> (<span style="color: #0000ff;">var</span> db = <span style="color: #0000ff;">new</span><span style="color: #000000;"> DonatorsContext())
    {
        </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">await</span><span style="color: #000000;"> db.Donators.CountAsync();
    }
}</span></pre>
</div>
<p>4，异步遍历查询结果</p>
<p>如果要对查询结果进行异步遍历，可以使用<code>ForEachAsync</code></p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">3.5 异步遍历查询结果</span>
<span style="color: #0000ff;">static</span> <span style="color: #0000ff;">async</span><span style="color: #000000;"> Task LoopDonatorsAsync()
{
    </span><span style="color: #0000ff;">using</span> (<span style="color: #0000ff;">var</span> db = <span style="color: #0000ff;">new</span><span style="color: #000000;"> DonatorsContext())
    {
        </span><span style="color: #0000ff;">await</span> db.Donators.ForEachAsync(d =&gt;<span style="color: #000000;">
        {
            d.DonateDate</span>=<span style="color: #000000;">DateTime.Today;
        });
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p><a name="8"></a></p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">八、管理并发</span></strong></span></p>
<p>&nbsp;1，为并发实现RowVersion</p>
<p>RowVersion机制使用了一种数据库功能，每当更新行的时候，就会创建一个新的行值</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">[Timestamp]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">byte</span>[] RowVersion { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

</span><span style="color: #008000;">//</span><span style="color: #008000;">修改上下文</span>

<span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> OnModelCreating(DbModelBuilder modelBuilder)
{
    modelBuilder.Entity</span>&lt;Donator&gt;().Property(d =&gt;<span style="color: #000000;"> d.RowVersion).IsRowVersion();
    </span><span style="color: #0000ff;">base</span><span style="color: #000000;">.OnModelCreating(modelBuilder);
}</span></pre>
</div>
<p><img src="http://images2017.cnblogs.com/blog/741594/201708/741594-20170828144132874-1866620698.png" alt="" /></p>
<p>现在，EF就会为并发控制追踪RowVersion列值。接下来尝试更新不同的列：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">try</span><span style="color: #000000;">{
  </span><span style="color: #008000;">//</span><span style="color: #008000;">1.用户甲获取id=1的打赏者</span>
  <span style="color: #0000ff;">var</span> donator1 = GetDonator(<span style="color: #800080;">1</span><span style="color: #000000;">);
  </span><span style="color: #008000;">//</span><span style="color: #008000;">2.用户乙也获取id=1的打赏者</span>
  <span style="color: #0000ff;">var</span> donator2 = GetDonator(<span style="color: #800080;">1</span><span style="color: #000000;">);
  </span><span style="color: #008000;">//</span><span style="color: #008000;">3.用户甲只更新这个实体的Name字段</span>
  donator1.Name = <span style="color: #800000;">"</span><span style="color: #800000;">用户甲</span><span style="color: #800000;">"</span><span style="color: #000000;">;
  UpdateDonator(donator1);
  </span><span style="color: #008000;">//</span><span style="color: #008000;">4.用户乙只更新这个实体的Amount字段</span>
  donator2.Amount =<span style="color: #000000;"> 100m;
  UpdateDonator(donator2);   
}
</span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (DbUpdateConcurrencyException ex)
{
    Console.WriteLine(</span><span style="color: #800000;">"发生并发更新</span><span style="color: #800000;">！</span><span style="color: #800000;">"</span><span style="color: #000000;">);
}</span></pre>
</div>
<p>&nbsp;</p>
<p><a name="9"></a></p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">九、事务</span></strong></span></p>
<p><strong><span style="font-size: 18px;">&nbsp;1，EF的默认事务处理</span></strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">int</span> outputId = <span style="color: #800080;">2</span>,inputId=<span style="color: #800080;">1</span><span style="color: #000000;">;
</span><span style="color: #0000ff;">decimal</span> transferAmount =<span style="color: #000000;"> 1000m;
</span><span style="color: #0000ff;">using</span> (<span style="color: #0000ff;">var</span> db=<span style="color: #0000ff;">new</span><span style="color: #000000;"> Context())
{
    </span><span style="color: #008000;">//</span><span style="color: #008000;">1 检索事务中涉及的账户</span>
    <span style="color: #0000ff;">var</span> outputAccount =<span style="color: #000000;"> db.OutputAccounts.Find(outputId);
    </span><span style="color: #0000ff;">var</span> inputAccount =<span style="color: #000000;"> db.InputAccounts.Find(inputId);
    </span><span style="color: #008000;">//</span><span style="color: #008000;">2 从输出账户上扣除1000</span>
    outputAccount.Balance -=<span style="color: #000000;"> transferAmount;
    </span><span style="color: #008000;">//</span><span style="color: #008000;">3 从输入账户上增加1000</span>
    inputAccount.Balance +=<span style="color: #000000;"> transferAmount;

    </span><span style="color: #008000;">//</span><span style="color: #008000;">4 提交事务</span>
<span style="color: #000000;">    db.SaveChanges();
}</span></pre>
</div>
<p><strong><span style="font-size: 18px;">2，使用TransactionScope处理事务</span></strong></p>
<div class="cnblogs_code">
<pre> <span style="color: #0000ff;">int</span> outputId = <span style="color: #800080;">2</span>, inputId = <span style="color: #800080;">1</span><span style="color: #000000;">;
 </span><span style="color: #0000ff;">decimal</span> transferAmount =<span style="color: #000000;"> 1000m;
 </span><span style="color: #0000ff;">using</span> (<span style="color: #0000ff;">var</span> ts=<span style="color: #0000ff;">new</span><span style="color: #000000;"> TransactionScope(TransactionScopeOption.Required))
 {
     </span><span style="color: #0000ff;">var</span> db1=<span style="color: #0000ff;">new</span><span style="color: #000000;"> Context();
     </span><span style="color: #0000ff;">var</span> db2=<span style="color: #0000ff;">new</span><span style="color: #000000;"> Context();
     </span><span style="color: #008000;">//</span><span style="color: #008000;">1 检索事务中涉及的账户</span>
     <span style="color: #0000ff;">var</span> outputAccount =<span style="color: #000000;"> db1.OutputAccounts.Find(outputId);
     </span><span style="color: #0000ff;">var</span> inputAccount =<span style="color: #000000;"> db2.InputAccounts.Find(inputId);
     </span><span style="color: #008000;">//</span><span style="color: #008000;">2 从输出账户上扣除1000</span>
     outputAccount.Balance -=<span style="color: #000000;"> transferAmount;
     </span><span style="color: #008000;">//</span><span style="color: #008000;">3 从输入账户上增加1000</span>
     inputAccount.Balance +=<span style="color: #000000;"> transferAmount;

     db1.SaveChanges();
     db2.SaveChanges();

     ts.Complete();
 }</span></pre>
</div>
<p><strong><span style="font-size: 18px;">3，使用EF6管理事务</span></strong></p>
<div class="cnblogs_code">
<pre> <span style="color: #0000ff;">int</span> outputId = <span style="color: #800080;">2</span>, inputId = <span style="color: #800080;">1</span><span style="color: #000000;">;
 </span><span style="color: #0000ff;">decimal</span> transferAmount =<span style="color: #000000;"> 1000m;
 </span><span style="color: #0000ff;">using</span> (<span style="color: #0000ff;">var</span> db=<span style="color: #0000ff;">new</span><span style="color: #000000;"> Context())
 {
     </span><span style="color: #0000ff;">using</span> (<span style="color: #0000ff;">var</span> trans=<span style="color: #000000;">db.Database.BeginTransaction())
     {
         </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
         {
             </span><span style="color: #0000ff;">var</span> sql = <span style="color: #800000;">"</span><span style="color: #800000;">Update OutputAccounts set Balance=Balance-@amountToDebit where id=@outputId</span><span style="color: #800000;">"</span><span style="color: #000000;">;
             db.Database.ExecuteSqlCommand(sql, </span><span style="color: #0000ff;">new</span> SqlParameter(<span style="color: #800000;">"</span><span style="color: #800000;">@amountToDebit</span><span style="color: #800000;">"</span>, transferAmount), <span style="color: #0000ff;">new</span> SqlParameter(<span style="color: #800000;">"</span><span style="color: #800000;">@outputId</span><span style="color: #800000;">"</span><span style="color: #000000;">,outputId));

             </span><span style="color: #0000ff;">var</span> inputAccount =<span style="color: #000000;"> db.InputAccounts.Find(inputId);
             inputAccount.Balance </span>+=<span style="color: #000000;"> transferAmount;
             db.SaveChanges();

             trans.Commit();
         }
         </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (Exception ex)
         {
             trans.Rollback();
         }
     }
 }</span></pre>
</div>
<p><strong><span style="font-size: 18px;">4，使用已存在的事务</span></strong></p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">模拟老项目的类库</span>
<span style="color: #0000ff;">static</span> <span style="color: #0000ff;">bool</span> DebitOutputAccount(SqlConnection conn, SqlTransaction trans, <span style="color: #0000ff;">int</span> accountId, <span style="color: #0000ff;">decimal</span><span style="color: #000000;"> amountToDebit)
{
    </span><span style="color: #0000ff;">int</span> affectedRows = <span style="color: #800080;">0</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">var</span> command =<span style="color: #000000;"> conn.CreateCommand();
    command.Transaction </span>=<span style="color: #000000;"> trans;
    command.CommandType</span>=<span style="color: #000000;">CommandType.Text;
    command.CommandText </span>= <span style="color: #800000;">"</span><span style="color: #800000;">Update OutputAccounts set Balance=Balance-@amountToDebit where id=@accountId</span><span style="color: #800000;">"</span><span style="color: #000000;">;
    command.Parameters.AddRange(</span><span style="color: #0000ff;">new</span><span style="color: #000000;"> SqlParameter[]
    {
        </span><span style="color: #0000ff;">new</span> SqlParameter(<span style="color: #800000;">"</span><span style="color: #800000;">@amountToDebit</span><span style="color: #800000;">"</span><span style="color: #000000;">,amountToDebit), 
        </span><span style="color: #0000ff;">new</span> SqlParameter(<span style="color: #800000;">"</span><span style="color: #800000;">@accountId</span><span style="color: #800000;">"</span><span style="color: #000000;">,accountId) 
    });

    </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
    {
        affectedRows</span>=<span style="color: #000000;"> command.ExecuteNonQuery();
    }
    </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (Exception ex)
    {
        </span><span style="color: #0000ff;">throw</span><span style="color: #000000;"> ex;
    }
    </span><span style="color: #0000ff;">return</span> affectedRows == <span style="color: #800080;">1</span><span style="color: #000000;">;
}</span></pre>
</div>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">#region</span> 7.0 使用已存在的事务
    <span style="color: #0000ff;">int</span> outputId = <span style="color: #800080;">2</span>, inputId = <span style="color: #800080;">1</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">decimal</span> transferAmount =<span style="color: #000000;"> 1000m;
    </span><span style="color: #0000ff;">var</span> connectionString = ConfigurationManager.ConnectionStrings[<span style="color: #800000;">"</span><span style="color: #800000;">ConcurrencyAndTransactionManagementConn</span><span style="color: #800000;">"</span><span style="color: #000000;">].ConnectionString;
    </span><span style="color: #0000ff;">using</span> (<span style="color: #0000ff;">var</span> conn=<span style="color: #0000ff;">new</span><span style="color: #000000;"> SqlConnection(connectionString))
    {
        conn.Open();
        </span><span style="color: #0000ff;">using</span> (<span style="color: #0000ff;">var</span> trans=<span style="color: #000000;">conn.BeginTransaction())
        {
            </span><span style="color: #0000ff;">try</span><span style="color: #000000;">
            {
                </span><span style="color: #0000ff;">var</span> result =<span style="color: #000000;"> DebitOutputAccount(conn, trans, outputId, transferAmount);
                </span><span style="color: #0000ff;">if</span> (!<span style="color: #000000;">result)
                {
                    </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> Exception(<span style="color: #800000;">"</span><span style="color: #800000;">不能正常扣款！</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                }
                </span><span style="color: #0000ff;">using</span> (<span style="color: #0000ff;">var</span> db=<span style="color: #0000ff;">new</span> Context(conn,contextOwnsConnection:<span style="color: #0000ff;">false</span><span style="color: #000000;">))
                {
                    db.Database.UseTransaction(trans);
                    </span><span style="color: #0000ff;">var</span> inputAccount=<span style="color: #000000;">db.InputAccounts.Find(inputId);
                    inputAccount.Balance </span>+=<span style="color: #000000;"> transferAmount;
                    db.SaveChanges();
                }
                trans.Commit();
            }
            </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (Exception ex) 
            {
                trans.Rollback();
            }
        }
    }

    </span><span style="color: #0000ff;">#endregion</span></pre>
</div>
<p>db.Database.UseTransaction(trans)：这句话的意思是，EF执行的操作都在外部传入的事务中执行</p>
<p><code>contextOwnsConnection</code>的值为false：表示上下文和数据库连接没有关系，上下文释放了，数据库连接还没释放；反之为true的话，上下文释放了，数据库连接也就释放了</p>
<p><strong><span style="font-size: 18px;">5，选择合适的事务管理</span></strong></p>
<p>目前，我们已经知道了好几种使用EF处理事务的方法，下面一一对号入座：</p>
<ul>
<li>如果只有一个DbContext类，那么应该尽力使用EF的默认事务管理。我们总应该将所有的操作组成一个在相同的DbContext对象的作用域中执行的工作单元，<code>SaveChanges()</code>方法会处理提交事务。</li>
<li>如果使用了多个DbContext对象，那么管理事务的最佳方法可能就是把调用放到<code>TransactionScope</code>对象的作用域中了。</li>
<li>如果要执行原生SQL，并想把这些操作和事务关联起来，那么应该使用EF提供的<code>Database.BeginTransaction()</code>方法。然而这种方法只支持EF6，不支持之前的版本。</li>
<li>如果想为要求<code>SqlTransaction</code>的老项目使用EF，那么可以使用<code>Database.UseTransaction()</code>方法，在EF6中可用。</li>
</ul>
<p>&nbsp;</p>
<p><a name="10"></a></p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">十、数据库迁移</span></strong></span></p>
<p><span style="font-size: 18px;"><strong>1，我们要给Message属性添加一个限制，即最大长度为50（默认的长度是MAX），然后更新数据库，结果会报错</strong></span></p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201708/741594-20170828161004968-2047136041.png" alt="" /></p>
<p>产生这个错误的道理很简单，字符串长度从最大变成50，肯定会造成数据丢失的。如果你知道会造成数据丢失，还要这么做，可以在后面加参数<code>-Force</code>,这个参数会强制更新数据库。或者，我们可以开启数据丢失支持，正如EF暴露的这个设置<strong>Set AutomaticMigrationDataLossAllowed to 'true'</strong>（错误信息中提到的）。</p>
<p>&nbsp;</p>
<p><span style="font-size: 18px;"><strong>2，<code></code><code>Up</code>和<code>Down</code>方法</strong></span></p>
<p>Up方法将数据库结构向前移动，例如，我们这里创建了两张新的表；Down方法帮助我们撤销更改，以防我们发现了软件问题需要回滚到之前的数据库结构</p>
<p>&nbsp;</p>
<p><strong><span style="font-size: 18px;">3，__MigrationHistory表</span></strong></p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201708/741594-20170828161357812-1403943169.png" alt="" /></p>
<p><code>__MigrationHistory</code>这张表，顾名思义，是记录迁移历史的。可以看到，<em>MigrationId</em>对应于初次迁移的文件名，<em>Model</em>列包含了上下文的哈希值，<em>ContextKey</em>包含了上下文配置类的类名</p>
<p>&nbsp;</p>
<p><strong><span style="font-size: 18px;">4，defaultValueSql</span></strong></p>
<p>要指定硬编码默认值，我们可以使用<code>defaultValue</code>参</p>
<div class="cnblogs_code">
<pre> <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Up()
 {
     AddColumn(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.Donators</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">CreationTime</span><span style="color: #800000;">"</span>, c =&gt; c.DateTime(nullable: <span style="color: #0000ff;">false</span>,defaultValueSql:<span style="color: #800000;">"</span><span style="color: #800000;">GetDate()</span><span style="color: #800000;">"</span><span style="color: #000000;">));
 }</span></pre>
</div>
<p>上面的代码中，我们使用了SQL Server中的<strong>GetDate</strong>函数使用当前日期填充新加入的列</p>
<p>&nbsp;</p>
<p><strong><span style="font-size: 18px;">5，要创建迁移，我们不一定非要有未处理的更改。我们仍然使用之前的指令<code>Add-Migration</code>，这样就给项目添加了一个迁移，但是Up和Down方法都是空的。现在，我们需要添加创建索引的自定义的代码，如下所示</span></strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">partial</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Donator_Add_Index_Name : DbMigration
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Up()
    {
        CreateIndex(
            </span><span style="color: #800000;">"</span><span style="color: #800000;">Donators</span><span style="color: #800000;">"</span><span style="color: #000000;">,
            </span><span style="color: #0000ff;">new</span> []{<span style="color: #800000;">"</span><span style="color: #800000;">Name</span><span style="color: #800000;">"</span><span style="color: #000000;">},
            name:</span><span style="color: #800000;">"</span><span style="color: #800000;">Index_Donator_Name</span><span style="color: #800000;">"</span><span style="color: #000000;">
            );
    }
    
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Down()
    {
        DropIndex(</span><span style="color: #800000;">"</span><span style="color: #800000;">Donators</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">Index_Donator_Name</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p><strong><span style="font-size: 18px;">6，回滚</span></strong></p>
<p>现在，尝试通过指定创建索引迁移之前的目标迁移删除该索引，创建索引之前的迁移名称是<strong>Donator_Add_CreationTime</strong>，要退回上一个迁移，我们可以使用下面的指令：</p>
<p>Update-Database -TargetMigration Donator_Add_CreationTime&nbsp;</p>
<p>&nbsp;</p>
<p><a name="11"></a></p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">十一、应用迁移</span></strong></span></p>
<p>&nbsp;1，通过脚本应用迁移</p>
<p>在<strong>包管理器控制台</strong>窗口中，我们可以通过<code>Update-Database -Script</code>生成脚本，该命令一执行完成，生成的脚本就会在VS中打开</p>
<p><span style="color: #ff0000;">需要注意的是，我们要指定匹配目标环境的数据库的正确连接字符串，因为迁移API会使用上下文比较实时数据库。我们要么在<code>Update-Database</code>后面带上连接字符串，要么在配置文件中使用正确的连接字符串。</span></p>
<p>&nbsp;</p>
<p>2，给已存在的数据库添加迁移</p>
<p>有时，我们想为一个已存在的数据库添加EF迁移，为的是将处理模式变化从一种方式移动到迁移API。当然，因为数据库已存在于生产环境，所以我们需要让迁移知道迁移起始的已知状态。使用<code>Add-Migration -IgnoreChanges</code>指令处理这个是相当简单的，当执行该命令时，EF会创建一个空的迁移，它会假设上下文和实体定义的模型和数据库是兼容的。一旦通过运行这个迁移更新了数据库，数据库模式不会发生变化，但是会在<code>_MigrationHistory</code>表中添加一条新的数据来对应初次迁移。这个完成之后，我们就可以安全地切换到EF的迁移API来维护数据库模式变化了。</p>
<p>&nbsp;</p>
<p><a name="12"></a></p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">十二、EF的其他功能</span></strong></span></p>
<p>1，&nbsp;应用于很多实体类型或者表的全局更改（比如，下面是如何设置所有的string属性在数据库中存储为非Unicode列）</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> OnModelCreating(DbModelBuilder modelBuilder)
{
    modelBuilder.Properties</span>&lt;<span style="color: #0000ff;">string</span>&gt;().Configure(config=&gt;config.IsUnicode(<span style="color: #0000ff;">false</span><span style="color: #000000;">));
}</span></pre>
</div>
<p>我们也可以写相同的代码作为自定义约定，然后在model builder中加入到约定集合中。要这么做的话，首先创建一个继承自<code>Convention</code>的类，重写构造函数，然后使用之前相同的代码，调用<code>Convention</code>类的<code>Properties</code>方法。代码如下：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> CustomConventions:Convention
{
    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> CustomConventions()
    {
        Properties</span>&lt;<span style="color: #0000ff;">string</span>&gt;().Configure(config=&gt;config.IsUnicode(<span style="color: #0000ff;">false</span><span style="color: #000000;">));
    }
}

</span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> OnModelCreating(DbModelBuilder modelBuilder)
{
    </span><span style="color: #008000;">//</span><span style="color: #008000;">modelBuilder.Properties&lt;string&gt;().Configure(config=&gt;config.IsUnicode(false));</span>
    modelBuilder.Conventions.Add&lt;CustomConventions&gt;<span style="color: #000000;">();
}</span></pre>
</div>
<p>&nbsp;</p>
<p>2，地理空间数据</p>
<p>除了标量类型数据，如string或decimal，EF也通过.Net中的<code>DbGeometry</code>和<code>DbGeography</code>支持地理空间数据。这些类型有支持地理空间查询的内置支持和正确翻译，例如地图上两点之间的距离。这些特定的查询方法对于具有地理空间属性的实体的查询很有用，换言之，当使用空间类型时，我们仍编写.Net代码。</p>
<p>&nbsp;</p>
<p>----------------------------------------------------------------------------------------</p>
<p>Local只能跟踪CUR操作。Local只能针对某一个DbSet而言<br />ChangeTracker可以跟踪整个DBContext<br />Entry只能跟踪某个一实体</p>
<p>继承IDbCommonInterceptor进行拦截EF执行</p>
<p>Timestamp特性标记字段为时间戳（该字段类型必须是byte[]）<br />ConcurrencyCheck特性并发检测<br />NotMapped特性：使该字段不生成数据库字段</p>
<p>Codefirst四大初始化策略<br />Database.SetInitializer&lt;Entity&gt;(new DropCreateDatabaseIfModelChanges&lt;Entity&gt;())</p>
<p>1，CreateDatabaseIfNotExists:默认策略<br />①数据库不存在，创建数据库<br />②model修改，执行抛出异常</p>
<p><br />2，DropCreateDatabaseIfModelChanges:<br />model一旦修改，我们将会执行dropdatabase操作</p>
<p>3，DropCreateDatabaseAlways：<br />每一次执行就重新创建表</p>
<p>4，Customer DB Initializer：<br />自定义初始化</p>
<p><br />5，禁用数据库初始化策略<br />Database.SetInitializer&lt;Entity&gt;(null)</p>
<p>使用EFProf工具监视ef支持的sql<br />https://www.codeproject.com/Articles/101214/EFProf-Profiler-Tool-for-Entity-Framework</p>