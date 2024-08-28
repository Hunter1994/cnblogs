<p><strong><span style="font-size: 16px;">一、为什么要使用依赖注入框架</span></strong></p>
<p>　　<span style="line-height: 1.5;">依赖注入框架也叫IoC容器。它的作用使类与类之间解耦</span></p>
<p><span style="line-height: 1.5;">　　我们看看为什么要用依赖注入框架，举个几个梨子：</span></p>
<p><span style="line-height: 1.5;">　　<strong><span style="font-size: 15px;">1，高度耦合的类</span></strong></span></p>
<p><span style="line-height: 1.5;">　　<img src="http://images0.cnblogs.com/blog2015/741594/201506/291458141815506.png" alt="" /></span></p>
<p><span style="line-height: 1.5;">&nbsp; &nbsp; &nbsp; 有一个Order类，Order类是用于订单操作的，DataAccess使用的sqlserver的方式查询订单。看看代码：</span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Order
    {
        </span><span style="color: #0000ff;">private</span> DataAccess dataAccess = <span style="color: #0000ff;">new</span><span style="color: #000000;"> DataAccess();
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span><span style="color: #000000;"> QueryOrder()
        {
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> dataAccess.QueryOrder();
        }
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> DataAccess
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span><span style="color: #000000;"> QueryOrder()
        {
            </span><span style="color: #0000ff;">return</span> <span style="color: #800000;">"</span><span style="color: #800000;">sqlserver查询Order</span><span style="color: #800000;">"</span><span style="color: #000000;">;
        }
    }</span></pre>
</div>
<p>&nbsp;</p>
<p>　　看到这两个类（Order，DataAccess），它们出现了高度耦合。如果产品汪突然狂犬病大发让我们换成MySql方式查询，我们不得不修改Order类的private DataAccess data = new DataAccess() 和DataAccess的QueryOrder方法。<span style="line-height: 1.5;">这里违反了</span><strong style="line-height: 1.5;">开放封闭原则（对扩展开放，对修改关闭）</strong><span style="line-height: 1.5;">，当然一个项目不只只有订单（Order）操作，还有购物车、产品等等操作，那改动起来将会是一场噩梦。</span></p>
<p>&nbsp;</p>
<p>　　<strong><span style="font-size: 15px;">2,使用依赖倒转原则来改进</span></strong></p>
<p>　　依赖倒转原则口诀:高层次模块不应该依赖于低层次模块，要依赖抽象，不要依赖具体。</p>
<p>　　口诀听着很绕口，其实理解起来并不难，看下面的类图，Order相当于是高层模块，SqlServerData和MySqlData相当于底层模块，高层模块依赖于接口，所以可以随时更换底层模块</p>
<p>　　<img src="http://images0.cnblogs.com/blog2015/741594/201506/291526385715539.png" alt="" /></p>
<p>　　我们现在把DataAccess抽象为接口，使SqlServerData和MySqlData实现IDataAccess</p>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Order
    {
        </span><span style="color: #0000ff;">private</span> IDataAccess dataAccess = <span style="color: #0000ff;">new</span><span style="color: #000000;"> MySqlData();
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span><span style="color: #000000;"> QueryOrder()
        {
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> dataAccess.QueryOrder();
        }
    }


    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IDataAccess
    {
        </span><span style="color: #0000ff;">string</span><span style="color: #000000;"> QueryOrder();
    }


    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SqlServerData : IDataAccess
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span><span style="color: #000000;"> QueryOrder()
        {
            </span><span style="color: #0000ff;">return</span> <span style="color: #800000;">"</span><span style="color: #800000;">sqlserver查询Order</span><span style="color: #800000;">"</span><span style="color: #000000;">;
        }
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MySqlData : IDataAccess
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span><span style="color: #000000;"> QueryOrder()
        {
            </span><span style="color: #0000ff;">return</span> <span style="color: #800000;">"</span><span style="color: #800000;">MySql查询Order</span><span style="color: #800000;">"</span><span style="color: #000000;">;
        }
    }</span></pre>
</div>
<p>　　现在我们高层模块依赖于接口，如果产品汪再叫我们换Oracle数据库，我们就可以再添加一个OracleData类，然后实现IDataAccess接口，然后在Order类中的private IDataAccess dataAccess = new MySqlData()改为private IDataAccess dataAccess = new OracleData()。虽然改动的地方减少了，但是我们还是修改了类。可是我们并不希望修改类，就可以更换数据访问，这就需要解耦，需要用到Ioc容器，我们的Ninject终于该出场了，出场费还不低哦！</p>
<p>&nbsp;</p>
<p><strong><span style="font-size: 16px;">二、实战Ninject</span></strong></p>
<p>　　</p>
<p><img src="http://images0.cnblogs.com/blog2015/741594/201507/031019541973375.png" alt="" /></p>
<p>&nbsp;</p>
<p><strong><span style="font-size: 15px;">1，使用注册机制</span></strong></p>
<p>　　首先安装一个Ninject的Dll，我们用NuGet安装。</p>
<p>　　①反键项目引用，选中管理NuGet程序包</p>
<p>　　<img src="http://images0.cnblogs.com/blog2015/741594/201507/011011460874458.png" alt="" width="205" height="142" /></p>
<p>　　②搜索Ninject，点击安装</p>
<p>　　<img src="http://images0.cnblogs.com/blog2015/741594/201507/011012280248713.png" alt="" width="650" height="365" /></p>
<p>　　③代码实现（只实现Order类操作，Product类操作与Order类一致）</p>
<p>　　<span style="color: #008000;"><strong>IDataAccess:</strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> RegisterNinject
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IDataAccess
    {
        </span><span style="color: #0000ff;">string</span><span style="color: #000000;"> QueryOrder();
    }
}</span></pre>
</div>
<p>　　<span style="color: #008000;"><strong>MySqlDataOrder:</strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> RegisterNinject
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MySqlDataOrder : IDataAccess
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span><span style="color: #000000;"> QueryOrder()
        {
            </span><span style="color: #0000ff;">return</span> <span style="color: #800000;">"</span><span style="color: #800000;">MySql查询Order</span><span style="color: #800000;">"</span><span style="color: #000000;">;
        }
    }
}</span></pre>
</div>
<p>　<span style="color: #008000;"><strong>　SqlServerDataOrder:</strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> RegisterNinject
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SqlServerDataOrder : IDataAccess
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span><span style="color: #000000;"> QueryOrder()
        {
            </span><span style="color: #0000ff;">return</span> <span style="color: #800000;">"</span><span style="color: #800000;">sqlserver查询Order</span><span style="color: #800000;">"</span><span style="color: #000000;">;
        }
    }
}</span></pre>
</div>
<p>　　<span style="color: #008000;"><strong>Register：</strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span> Ninject; <span style="color: #008000;">//</span><span style="color: #008000;">引入命名空间</span>
<span style="color: #0000ff;">namespace</span><span style="color: #000000;"> RegisterNinject
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Register
    {
        </span><span style="color: #0000ff;">private</span> StandardKernel _kernel = <span style="color: #0000ff;">new</span><span style="color: #000000;"> StandardKernel();
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 在这里注册</span>
        <span style="color: #0000ff;">public</span><span style="color: #000000;"> Register()
        {
            _kernel.Bind</span>&lt;IDataAccess&gt;().To&lt;MySqlDataOrder&gt;<span style="color: #000000;">();
            </span><span style="color: #008000;">//</span><span style="color: #008000;">_kernel.Bind&lt;IDataAccess&gt;().To&lt;SqlServerDataOrder&gt;();
            </span><span style="color: #008000;">//</span><span style="color: #008000;">_kernel.Bind&lt;IDataProduct&gt;().To&lt;SqlServerDataProduct&gt;();</span>
<span style="color: #000000;">        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;">获取</span>
        <span style="color: #0000ff;">public</span> TInterface Get&lt;TInterface&gt;<span style="color: #000000;">()
        {
            </span><span style="color: #0000ff;">return</span> _kernel.Get&lt;TInterface&gt;<span style="color: #000000;">();
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Dispose()
        {
            _kernel.Dispose();
        }
    }
}</span></pre>
</div>
<p><strong>　　<span style="color: #008000;">Order：</span></strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> RegisterNinject
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Order
    {
        </span><span style="color: #0000ff;">private</span> Register reg = <span style="color: #0000ff;">new</span><span style="color: #000000;"> Register();
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span><span style="color: #000000;"> QueryOrder()
        {
            </span><span style="color: #0000ff;">return</span> reg.Get&lt;IDataAccess&gt;<span style="color: #000000;">().QueryOrder();
        }

    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;　这样，妈妈再也不用担心我换数据库了。如果产品汪再让我们换回sqlserver数据库[神经病]（小插曲：换数据库是举的例子，Ioc容器的意义是让类与类之间解耦的，不是换数据库用的！），我们只需要在Register类中的构造函数中修改注册即可。</p>
<p>　　有人说，"你还是修改了类呀！"。Register类的定位不一样，他是一个公共类，专门提供注册机制的。如果不去要修改类，就能完成换数据库，那就要引入新的概念&mdash;&mdash;&mdash;热插拔技术。</p>
<p>　　</p>
<p><strong><span style="font-size: 15px;">2，使用Xml文件（热插拔）</span></strong></p>
<p>　　现在我们用xml文件的方式，动态的更换接口。我们需要建一个xml文件。把他放在项目中。</p>
<p>　　<span style="color: #008000;">Register.xml</span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;?</span><span style="color: #ff00ff;">xml version="1.0" encoding="utf-8" </span><span style="color: #0000ff;">?&gt;</span> 
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">module </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="register"</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">bind </span><span style="color: #ff0000;">service</span><span style="color: #0000ff;">="XmlNinject.IDataAccess,XmlNinject"</span><span style="color: #ff0000;"> to</span><span style="color: #0000ff;">="XmlNinject.SqlServerDataOrder,XmlNinject"</span><span style="color: #0000ff;">/&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">module</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;<span style="line-height: 1.5;">　注意：module元素，name属性，bind元素，service属性，to属性为规定的元素属性，不能写成别的。格式也要正确。</span></p>
<p><span style="line-height: 1.5;">　 然后更改下</span><span style="line-height: 1.5;"><strong><span style="color: #008000;">Register</span>：</strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span> Ninject; <span style="color: #008000;">//</span><span style="color: #008000;">引入命名空间</span>
<span style="color: #0000ff;">using</span> Ninject.Extensions.Xml;<span style="color: #008000;">//</span><span style="color: #008000;">引入命名空间</span>
<span style="color: #0000ff;">namespace</span><span style="color: #000000;"> XmlNinject
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Register
    {
        </span><span style="color: #0000ff;">private</span> StandardKernel _kernel = <span style="color: #0000ff;">new</span><span style="color: #000000;"> StandardKernel();

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 以后这里就不用更改这里了，只需要该xml文件就可以了</span>
        <span style="color: #0000ff;">public</span><span style="color: #000000;"> Register()
        {
            </span><span style="color: #0000ff;">var</span> settings = <span style="color: #0000ff;">new</span> NinjectSettings() { LoadExtensions = <span style="color: #0000ff;">false</span><span style="color: #000000;"> };
            _kernel </span>= <span style="color: #0000ff;">new</span> StandardKernel(settings, <span style="color: #0000ff;">new</span><span style="color: #000000;"> XmlExtensionModule());
            _kernel.Load(</span><span style="color: #800000;">"</span><span style="color: #800000;">Xml/Register.xml</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;">获取</span>
        <span style="color: #0000ff;">public</span> TInterface Get&lt;TInterface&gt;<span style="color: #000000;">()
        {
            </span><span style="color: #0000ff;">return</span> _kernel.Get&lt;TInterface&gt;<span style="color: #000000;">();
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Dispose()
        {
            _kernel.Dispose();
        }
    }
}</span></pre>
</div>
<p>&nbsp;　　以后要更换接口，直接更改xml文件就可以了。</p>
<p>　　 源码下载<a href="http://pan.baidu.com/s/1sjJXVrv" target="_blank">http://pan.baidu.com/s/1sjJXVrv</a>　　</p>
<p>&nbsp;</p>