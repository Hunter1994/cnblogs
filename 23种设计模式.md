<p><a href="#a"><span style="font-size: 12px;">一、创建型</span></a></p>
<p><a href="#a1"><span style="font-size: 12px;">1，AbstractFactory（抽象工厂，对象模式）</span></a></p>
<p><a href="#a2"><span style="font-size: 12px;">2，Builder（建造者，对象模式）</span></a></p>
<p><span style="font-size: 12px;"><a href="#a3">3，Factory Method（工厂方法，类创模式）</a>&nbsp;</span></p>
<p><a href="#a4"><span style="font-size: 12px;">4，Prototype（原型，对象模式）</span></a></p>
<p><a href="#a5"><span style="font-size: 12px;">5，Singleton（单例，对象模式）</span></a></p>
<p><span style="font-size: 12px;"><a href="#b">二、结构型</a></span></p>
<p><span style="font-size: 12px;"><a href="#b1">1，Adapter（适配器，类模式）</a>&nbsp;</span></p>
<p><a href="#b2"><span style="font-size: 12px;">2，Bridge（桥接，对象模式）</span></a></p>
<p><a href="#b3"><span style="font-size: 12px;">3，Composite（组合，对象模式）</span></a></p>
<p><a href="#b4"><span style="font-size: 12px;">4，Decorator（装饰，对象模式）</span></a></p>
<p><a href="#b5"><span style="font-size: 12px;">5，Facade（外观，对象模式）</span></a></p>
<p><a href="#b6"><span style="font-size: 12px;">6，Flyweight（享元，对象模式）</span></a></p>
<p><a href="#b7"><span style="font-size: 12px;">7，Proxy（代理，对象模式）</span></a></p>
<p><span style="font-size: 12px;"><a href="#c">三、行为型</a></span></p>
<p><span style="font-size: 12px;"><a href="#c1">1，Chain of Responsibility（职责链，对象模式）</a></span></p>
<p><span style="font-size: 12px;"><a href="#c2">2，Command（命令，对象模式）</a></span></p>
<p><span style="font-size: 12px;"><a href="#c3">3，Interpreter（解释器，类模式）</a></span></p>
<p><span style="font-size: 12px;"><a href="#c4">4，Iterator（迭代器，对象模式）</a></span></p>
<p><span style="font-size: 12px;"><a href="#c5">5，Mediator（中介者，对象模式）</a></span></p>
<p><span style="font-size: 12px;"><a href="#c6">6，Memento（备忘录，对象模式）</a></span></p>
<p><span style="font-size: 12px;"><a href="#c7">7，Observer（观察者，对象模式）</a></span></p>
<p><span style="font-size: 12px;"><a href="#c8">8，State（状态，对象模式）&nbsp;</a></span></p>
<p><span style="font-size: 12px;"><a href="#c9">9，Strategy（策略，对象模式）</a></span></p>
<p><span style="font-size: 12px;"><a href="#c10">10，Template Method（模板方法，类模式）</a></span></p>
<p><span style="font-size: 12px;"><a href="#c11">11，Visitor（访问者，对象模式）</a></span></p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: rgba(22, 159, 230, 1);"><span style="color: rgba(255, 255, 255, 1);">一、创建型<a name="a"></a></span></p>
<p><span style="font-size: 18px; color: #ff6600;"><strong>创建型类模式将对象的部分创建工作延迟到子类，而创建型对象模式则将它延迟到另一个对象中</strong></span></p>
<p><strong><span style="font-size: 18px;">1，AbstractFactory（抽象工厂，对象模式）<a name="a1"></a></span></strong></p>
<p><strong>&nbsp;</strong><span style="color: #ff6600;"><strong>意图：</strong>提供一个接口以创建一系列相关或相互依赖的对象，而无需指向它们具体的类</span></p>
<p><span style="color: #ff6600;">&nbsp;<strong>使用场景：</strong>抽象工厂模式适用于需要创建一组相关或相互依赖的对象，并且这些对象的创建方式可能会发生变化的场景</span></p>
<p><strong><span style="color: #ff6600;">&nbsp;结构：</span></strong></p>
<p><img src="https://img2023.cnblogs.com/blog/741594/202303/741594-20230323204843003-251411659.png" alt="" width="532" height="341" loading="lazy" /></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('84ca5206-128d-49b1-a1d4-af4dffeb6100')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_84ca5206-128d-49b1-a1d4-af4dffeb6100" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_84ca5206-128d-49b1-a1d4-af4dffeb6100" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_84ca5206-128d-49b1-a1d4-af4dffeb6100" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> _11_抽象工厂模式
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            AbstractFactory factory</span>=<span style="color: #0000ff;">new</span><span style="color: #000000;"> SQLServerFactory();
            IProductA proA</span>=<span style="color: #000000;"> factory.CreateProductA();
            proA.GetProductA();


            Console.ReadLine();
        }
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">抽象工厂：创建所有的产品接口</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> AbstractFactory
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span><span style="color: #000000;"> IProductA CreateProductA();
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span><span style="color: #000000;"> IProductB CreateProductB();
    }
    </span><span style="color: #008000;">//</span><span style="color: #008000;">具体工厂。Access数据库访问工厂</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> AccessFactory : AbstractFactory
    {

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span><span style="color: #000000;"> IProductA CreateProductA()
        {
            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> Access_ProductA1();
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span><span style="color: #000000;"> IProductB CreateProductB()
        {
            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> Access_ProductB1();
        }
    }
    </span><span style="color: #008000;">//</span><span style="color: #008000;">具体工厂。SQLServer数据库访问工厂</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SQLServerFactory : AbstractFactory
    {

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span><span style="color: #000000;"> IProductA CreateProductA()
        {
            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> SQLServer_ProductA();
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span><span style="color: #000000;"> IProductB CreateProductB()
        {
            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> SQLServer_ProductB();
        }
    }


    </span><span style="color: #008000;">//</span><span style="color: #008000;">ProductA接口</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IProductA
    {
        </span><span style="color: #0000ff;">void</span><span style="color: #000000;"> GetProductA();
    }
    </span><span style="color: #008000;">//</span><span style="color: #008000;">具体ProductA</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Access_ProductA1 : IProductA
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> GetProductA()
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">access数据库访问tProductA</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }
    }
    </span><span style="color: #008000;">//</span><span style="color: #008000;">具体ProductA</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SQLServer_ProductA : IProductA
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> GetProductA()
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">SQLServer数据库访问tProductA</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">ProductB接口</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IProductB
    {
        </span><span style="color: #0000ff;">void</span><span style="color: #000000;"> GetProductB();
    }
    </span><span style="color: #008000;">//</span><span style="color: #008000;">具体ProductB</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Access_ProductB1 : IProductB
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> GetProductB()
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">access数据库访问tProductB</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }
    }
    </span><span style="color: #008000;">//</span><span style="color: #008000;">具体ProductB</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SQLServer_ProductB : IProductB
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> GetProductB()
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">SQLServer数据库访问tProductB</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }
    }


}

抽象工厂模式代码</span></pre>
</div>
<span class="cnblogs_code_collapse">抽象工厂模式代码</span></div>
<p><strong><span style="color: #ff6600;">使用案例：</span></strong>跨平台开发：在跨平台开发中，需要根据不同的操作系统和硬件平台使用不同的API。使用抽象工厂模式，可以为每个平台创建一个工厂，这样可以轻松地编写跨平台的代码。</p>
<p>&nbsp;</p>
<p><strong><span style="font-size: 18px;">2，Builder（建造者，对象模式）<a name="a2"></a></span></strong></p>
<p><span style="color: #ff6600;">&nbsp;<strong>意图：</strong>将一个复杂对象的构建与它的表示分离，使得同样的构建过程可以创建不同的表示</span></p>
<p><span style="color: #ff6600;">&nbsp;<strong>使用场景：</strong>当需要创建复杂对象并且需要控制对象的构造过程时，使用 Builder 模式可以提供一种清晰、简洁的解决方案</span></p>
<p><span style="color: #ff6600;">&nbsp;<strong>结构：</strong></span></p>
<p>&nbsp;<img src="https://img2023.cnblogs.com/blog/741594/202303/741594-20230321230823656-1288711003.png" alt="" width="418" height="260" loading="lazy" /></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('109139c0-b387-4292-bdc2-52588eb23ee1')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_109139c0-b387-4292-bdc2-52588eb23ee1" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_109139c0-b387-4292-bdc2-52588eb23ee1" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_109139c0-b387-4292-bdc2-52588eb23ee1" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> _9_建造者模式
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            Builder bui </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> ConcreteBuilder();
            Director dir </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> Director();
            dir.Construct(bui);
            bui.GetResult().GetProduct();

            Console.ReadLine();
        }
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">具体产品</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Product
    {
        </span><span style="color: #0000ff;">private</span> List&lt;<span style="color: #0000ff;">string</span>&gt; strList = <span style="color: #0000ff;">new</span> List&lt;<span style="color: #0000ff;">string</span>&gt;<span style="color: #000000;">();
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> Add(<span style="color: #0000ff;">string</span><span style="color: #000000;"> p)
        {
            strList.Add(p);
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> GetProduct()
        {
            </span><span style="color: #0000ff;">foreach</span> (<span style="color: #0000ff;">var</span> list <span style="color: #0000ff;">in</span><span style="color: #000000;"> strList)
            {
                Console.WriteLine(list);
            }
        }
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">抽象建造者</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Builder
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> BuilderPartA();
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> BuilderPartB();
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span><span style="color: #000000;"> Product GetResult();
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">具体建造者</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ConcreteBuilder : Builder
    {
        </span><span style="color: #0000ff;">private</span> Product pro = <span style="color: #0000ff;">new</span><span style="color: #000000;"> Product();

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> BuilderPartA()
        {
            pro.Add(</span><span style="color: #800000;">"</span><span style="color: #800000;">部件1</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> BuilderPartB()
        {
            pro.Add(</span><span style="color: #800000;">"</span><span style="color: #800000;">部件2</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span><span style="color: #000000;"> Product GetResult()
        {
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> pro;
        }
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">指挥者</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Director
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Construct(Builder bui)
        {
            bui.BuilderPartA();
            bui.BuilderPartB();
        }
    }


}</span></pre>
</div>
<span class="cnblogs_code_collapse">建造者结构代码</span></div>
<p>&nbsp;<strong><span style="color: #ff6600;">使用案例：</span></strong>在asp.net core框架中的应用：</p>
<p><img src="https://img2023.cnblogs.com/blog/741594/202303/741594-20230321231749934-752669291.png" alt="" width="414" height="230" loading="lazy" /></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('094711b6-2af2-4dcc-89bf-5033526c6a6a')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_094711b6-2af2-4dcc-89bf-5033526c6a6a" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_094711b6-2af2-4dcc-89bf-5033526c6a6a" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_094711b6-2af2-4dcc-89bf-5033526c6a6a" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Hosting;

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
    {
        CreateWebHostBuilder(args).Build().Run();
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> IWebHostBuilder CreateWebHostBuilder(<span style="color: #0000ff;">string</span>[] args) =&gt;<span style="color: #000000;">
        WebHost.CreateDefaultBuilder(args)
            .UseStartup</span>&lt;Startup&gt;<span style="color: #000000;">();
}</span></pre>
</div>
<span class="cnblogs_code_collapse">示例代码</span></div>
<p>&nbsp;</p>
<p><strong><span style="font-size: 18px;">&nbsp;3，Factory Method（工厂方法，类模式）<a name="a3"></a></span></strong></p>
<p><span style="color: #ff6600;">&nbsp;<strong>意图：</strong>定义一个用户创建对象的接口，让子类决定实例化那个类。Factory Method使一个类的实例化延迟到其子类</span></p>
<p><span style="color: #ff6600;">&nbsp;<strong>使用场景：</strong>将一个类的实例化延迟到其子类</span></p>
<p><strong>&nbsp;<span style="color: #ff6600;">结构：</span></strong></p>
<p><img src="https://img2023.cnblogs.com/blog/741594/202303/741594-20230326141611170-661818173.png" alt="" width="420" height="275" loading="lazy" /></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('d2e36153-0bee-4de4-bdd8-540cfc3addd2')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_d2e36153-0bee-4de4-bdd8-540cfc3addd2" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_d2e36153-0bee-4de4-bdd8-540cfc3addd2" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_d2e36153-0bee-4de4-bdd8-540cfc3addd2" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IProduct
    {
        
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ConcreteProduce : IProduct
    { 
    
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> ICreator
    {
        IProduct FactoryMethod();
    }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ConcreteCreator : ICreator
    {
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> IProduct FactoryMethod()
        {
            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> ConcreteProduce();
        }
    }</span></pre>
</div>
<span class="cnblogs_code_collapse">结构代码</span></div>
<p><strong><span style="color: #ff6600;">使用案例：</span></strong></p>
<p><img src="https://img2023.cnblogs.com/blog/741594/202303/741594-20230326142345280-2120039622.png" alt="" width="298" height="194" loading="lazy" /></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('38230c4b-c007-43e4-afba-80f011df5e09')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_38230c4b-c007-43e4-afba-80f011df5e09" class="code_img_closed" /><span class="cnblogs_code_collapse">使用工厂方法模式创建服务实例的简单示例代码</span></div>
<p>&nbsp;</p>
<p><strong><span style="font-size: 18px;">4，Prototype（原型，对象模式）<a name="a4"></a></span></strong></p>
<p><span style="color: #ff6600;"><strong>意图：</strong>用原型实例指定创建对象的种类，并且通过拷贝这些原型创建新的对象</span></p>
<p><span style="color: #ff6600;"><strong>应用场景：</strong>利用原有对象进行拷贝来创建新的对象</span></p>
<p><strong><span style="color: #ff6600;">结构：</span></strong></p>
<p><img src="https://img2023.cnblogs.com/blog/741594/202303/741594-20230326150931487-761602816.png" alt="" width="261" height="215" loading="lazy" /></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('46e5dfdc-e56d-48f8-a07d-fd588121dd56')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_46e5dfdc-e56d-48f8-a07d-fd588121dd56" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_46e5dfdc-e56d-48f8-a07d-fd588121dd56" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_46e5dfdc-e56d-48f8-a07d-fd588121dd56" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> _6_原型模式
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            Resume r </span>= <span style="color: #0000ff;">new</span> Resume(<span style="color: #800000;">"</span><span style="color: #800000;">Hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            r.SetPersonalInfo(</span><span style="color: #800000;">"</span><span style="color: #800000;">男</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">22</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            r.SetWorkExperience(</span><span style="color: #800000;">"</span><span style="color: #800000;">2014-2015</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">xx公司</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            Resume r2 </span>=<span style="color: #000000;"> (Resume)r.Clone();
            r2.SetWorkExperience(</span><span style="color: #800000;">"</span><span style="color: #800000;">2014-2016</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">xx公司</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            r.Display();
            r2.Display();

            Console.ReadLine();

        }
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Resume : ICloneable
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">string</span><span style="color: #000000;"> name;
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">string</span><span style="color: #000000;"> sex;
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">string</span><span style="color: #000000;"> age;
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">string</span><span style="color: #000000;"> timeArea;
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span><span style="color: #000000;"> company;

        </span><span style="color: #0000ff;">public</span> Resume(<span style="color: #0000ff;">string</span><span style="color: #000000;"> name)
        {
            </span><span style="color: #0000ff;">this</span>.name =<span style="color: #000000;"> name;
        }
        </span><span style="color: #008000;">//</span><span style="color: #008000;">设置个人信息</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> SetPersonalInfo(<span style="color: #0000ff;">string</span> sex, <span style="color: #0000ff;">string</span><span style="color: #000000;"> age)
        {
            </span><span style="color: #0000ff;">this</span>.sex =<span style="color: #000000;"> sex;
            </span><span style="color: #0000ff;">this</span>.age =<span style="color: #000000;"> age;
        }
        </span><span style="color: #008000;">//</span><span style="color: #008000;">设置工作经历</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> SetWorkExperience(<span style="color: #0000ff;">string</span> timeArea, <span style="color: #0000ff;">string</span><span style="color: #000000;"> company)
        {
            </span><span style="color: #0000ff;">this</span>.timeArea =<span style="color: #000000;"> timeArea;
            </span><span style="color: #0000ff;">this</span>.company =<span style="color: #000000;"> company;
        }
        </span><span style="color: #008000;">//</span><span style="color: #008000;">显示</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Display()
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">{0} {1} {2}</span><span style="color: #800000;">"</span><span style="color: #000000;">, name, sex, age);
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">工作经历：{0} {1}</span><span style="color: #800000;">"</span><span style="color: #000000;">, timeArea, company);
        }
        </span><span style="color: #008000;">//</span><span style="color: #008000;">克隆</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">object</span><span style="color: #000000;"> Clone()
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建当前对象的浅表副本。方法是创建一个新对象，
            </span><span style="color: #008000;">//</span><span style="color: #008000;">然后将当前对象的非静态字段复制到该新对象。
            </span><span style="color: #008000;">//</span><span style="color: #008000;">如果字段是值类型的，则对该字段执行逐位复制。
            </span><span style="color: #008000;">//</span><span style="color: #008000;">如果字段是引用类型，则复制引用但不复制引用的对象，
            </span><span style="color: #008000;">//</span><span style="color: #008000;">因此，原始对象及其副本引用同一个对象</span>
            <span style="color: #0000ff;">return</span> (<span style="color: #0000ff;">object</span>) <span style="color: #0000ff;">this</span><span style="color: #000000;">.MemberwiseClone();
        }
    }

}

原型模式代码</span></pre>
</div>
<span class="cnblogs_code_collapse">结构代码</span></div>
<p><strong><span style="color: #ff6600;">使用案例：</span></strong></p>
<p><img src="https://img2023.cnblogs.com/blog/741594/202303/741594-20230326151506546-1521227911.png" alt="" width="171" height="200" loading="lazy" /></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('a24a044d-6bd6-4e80-a528-a03221765c79')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_a24a044d-6bd6-4e80-a528-a03221765c79" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_a24a044d-6bd6-4e80-a528-a03221765c79" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_a24a044d-6bd6-4e80-a528-a03221765c79" class="cnblogs_code_hide">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> 定义原型接口</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span> ICloneable&lt;T&gt;<span style="color: #000000;">
{
    T Clone();
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 实现原型类</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> Person : ICloneable&lt;Person&gt;<span style="color: #000000;">
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Name { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span> Age { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Person Clone()
    {
        </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> Person { Name = <span style="color: #0000ff;">this</span>.Name, Age = <span style="color: #0000ff;">this</span><span style="color: #000000;">.Age };
    }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 创建原型对象</span>
<span style="color: #0000ff;">var</span> person1 = <span style="color: #0000ff;">new</span> Person { Name = <span style="color: #800000;">"</span><span style="color: #800000;">Alice</span><span style="color: #800000;">"</span>, Age = <span style="color: #800080;">20</span><span style="color: #000000;"> };

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 复制原型对象</span>
<span style="color: #0000ff;">var</span> person2 =<span style="color: #000000;"> person1.Clone();
person2.Name </span>= <span style="color: #800000;">"</span><span style="color: #800000;">Bob</span><span style="color: #800000;">"</span><span style="color: #000000;">;
person2.Age </span>= <span style="color: #800080;">25</span><span style="color: #000000;">;

Console.WriteLine($</span><span style="color: #800000;">"</span><span style="color: #800000;">Person 1: {person1.Name}, {person1.Age}</span><span style="color: #800000;">"</span><span style="color: #000000;">);
Console.WriteLine($</span><span style="color: #800000;">"</span><span style="color: #800000;">Person 2: {person2.Name}, {person2.Age}</span><span style="color: #800000;">"</span>);</pre>
</div>
<span class="cnblogs_code_collapse">示例代码</span></div>
<p>&nbsp;</p>
<p><span style="font-size: 18px;"><strong>5，Singleton（单例，对象模式）<a name="a5"></a></strong></span></p>
<p><span style="color: #ff6600;"><strong>意图：</strong>保证一个类仅有一个实例，并提供一个访问它的全局访问点</span></p>
<p><span style="color: #ff6600;"><strong>应用场景：</strong>一个类仅有一个实例</span></p>
<p><span style="color: #ff6600;"><strong>结构：</strong></span></p>
<p><strong><img src="https://img2023.cnblogs.com/blog/741594/202303/741594-20230326151953829-2007228953.png" alt="" loading="lazy" /></strong></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('65d1a2ec-b41f-4e4a-8605-50d2287e611b')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_65d1a2ec-b41f-4e4a-8605-50d2287e611b" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_65d1a2ec-b41f-4e4a-8605-50d2287e611b" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_65d1a2ec-b41f-4e4a-8605-50d2287e611b" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> _16_单例模式
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            Singleton s </span>=<span style="color: #000000;"> Singleton.GetInstance();
            Singleton s1 </span>=<span style="color: #000000;"> Singleton.GetInstance();
            Console.WriteLine(s</span>==<span style="color: #000000;">s1);

            Console.ReadLine();
        }
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">单例模式</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Singleton
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> Singleton instance;

        </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> Singleton()
        {

        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> Singleton GetInstance()
        {
            </span><span style="color: #0000ff;">if</span> (instance == <span style="color: #0000ff;">null</span><span style="color: #000000;">)
            {
                instance </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> Singleton();
            }
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> instance;
        }

    }


    </span><span style="color: #008000;">//</span><span style="color: #008000;">双重锁定</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Singleton2
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> Singleton2 instance;
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">object</span> o=<span style="color: #0000ff;">new</span> <span style="color: #0000ff;">object</span><span style="color: #000000;">();
        </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> Singleton2()
        {

        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> Singleton2 GetInstance()
        {
            </span><span style="color: #0000ff;">if</span> (instance == <span style="color: #0000ff;">null</span><span style="color: #000000;">)
            {
                </span><span style="color: #0000ff;">lock</span><span style="color: #000000;"> (o)
                {
                    </span><span style="color: #0000ff;">if</span> (instance == <span style="color: #0000ff;">null</span><span style="color: #000000;">)
                    {
                        instance </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> Singleton2();
                    }
                }
            }
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> instance;
        }
    }

}

单例模式代码</span></pre>
</div>
<span class="cnblogs_code_collapse">结构代码</span></div>
<p><span style="color: #ff6600;"><strong>使用案例：</strong></span></p>
<p>&nbsp;单例模式相对于之前类级别锁的好处是，不用创建那么多 Logger 对象，一方面节省内存空间，另一方面节省系统文件句柄</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('10832e3f-246f-4750-9edb-5d3d129604fc')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_10832e3f-246f-4750-9edb-5d3d129604fc" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_10832e3f-246f-4750-9edb-5d3d129604fc" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_10832e3f-246f-4750-9edb-5d3d129604fc" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Logger {
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> FileWriter writer;
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> final Logger instance = <span style="color: #0000ff;">new</span><span style="color: #000000;"> Logger();

  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> Logger() {
    File file </span>= <span style="color: #0000ff;">new</span> File(<span style="color: #800000;">"</span><span style="color: #800000;">/Users/wangzheng/log.txt</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    writer </span>= <span style="color: #0000ff;">new</span> FileWriter(file, <span style="color: #0000ff;">true</span>); <span style="color: #008000;">//</span><span style="color: #008000;">true表示追加写入</span>
<span style="color: #000000;">  }
  
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> Logger getInstance() {
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> instance;
  }
  
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> log(String message) {
    writer.write(mesasge);
  }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> Logger类的应用示例：</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> UserController {
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> login(String username, String password) {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> ...省略业务逻辑代码...</span>
    Logger.getInstance().log(username + <span style="color: #800000;">"</span><span style="color: #800000;"> logined!</span><span style="color: #800000;">"</span><span style="color: #000000;">);
  }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> OrderController {  
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> create(OrderVo order) {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> ...省略业务逻辑代码...</span>
    Logger.getInstance().log(<span style="color: #800000;">"</span><span style="color: #800000;">Created a order: </span><span style="color: #800000;">"</span> +<span style="color: #000000;"> order.toString());
  }
}

单例模式相对于之前类级别锁的好处是，不用创建那么多 Logger 对象，一方面节省内存空间，另一方面节省系统文件句柄</span></pre>
</div>
<span class="cnblogs_code_collapse">案例代码</span></div>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: rgba(22, 159, 230, 1);"><span style="color: rgba(255, 255, 255, 1);">二、结构型<a name="b"></a></span></p>
<p><span style="font-size: 18px; color: #ff6600;"><strong>结构型模式涉及如何组装类和对象以获得更大的结构。</strong></span></p>
<p><span style="font-size: 18px; color: #ff6600;"><strong>结构型类模式采用继承机制来组合接口实现；结构型对象模式不是对接口的实现进行组合，而是描述了如何对一些对象进行组合，从而实现新功能的一些方法</strong></span></p>
<p><strong><span style="font-size: 18px;">1，Adapter（适配器，类模式）&nbsp;<a name="b1"></a></span></strong></p>
<p><span style="color: #ff6600;"><strong>意图：</strong>将一个类的接口转换成客户希望的另一个接口。Adapter模式使得原本由于接口不兼容而不能一起工作的哪些类可以一起工作</span></p>
<p><span style="color: #ff6600;"><strong>应用场景：</strong>解决接口之前不匹配的问题</span></p>
<p><span style="color: #ff6600;"><strong>结构：</strong></span></p>
<p><strong><img src="https://img2023.cnblogs.com/blog/741594/202303/741594-20230327213118740-1285696411.png" alt="" width="460" height="263" loading="lazy" /></strong></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('da0f5e57-faca-4f43-95fb-cfb75292f002')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_da0f5e57-faca-4f43-95fb-cfb75292f002" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_da0f5e57-faca-4f43-95fb-cfb75292f002" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_da0f5e57-faca-4f43-95fb-cfb75292f002" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> _13_适配器模式
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            Target t</span>=<span style="color: #0000ff;">new</span><span style="color: #000000;"> Adapter();
            t.Request();

            Console.ReadLine();
        }
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">客户所期待的接口</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Target
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">virtual</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Request()
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">普通请求</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">适配器</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Adapter : Target
    {
        </span><span style="color: #0000ff;">private</span> Adaptee ada=<span style="color: #0000ff;">new</span><span style="color: #000000;"> Adaptee() ;
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Request()
        {
            ada.SpecificRequest();
        }
    }
    </span><span style="color: #008000;">//</span><span style="color: #008000;">需要适配的对象</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Adaptee
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> SpecificRequest()
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">特殊请求</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }
    }
}

适配器模式代码</span></pre>
</div>
<span class="cnblogs_code_collapse">结构代码</span></div>
<p><strong><strong>使用案例：</strong></strong></p>
<p><strong><span style="font-size: 18px;">2，Bridge（桥接，对象模式）&nbsp;<a name="b2"></a></span></strong></p>
<p><span style="color: #ff6600;"><strong>意图：</strong>将抽象部分与它的实现部分分离，使得它们可以独立变化</span></p>
<p><span style="color: #ff6600;"><strong>应用场景：</strong>抽象与实现分离</span></p>
<p><span style="color: #ff6600;"><strong>结构：</strong></span></p>
<p><strong><img src="https://img2023.cnblogs.com/blog/741594/202303/741594-20230328212701317-1251464616.png" alt="" width="1052" height="376" loading="lazy" /></strong></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('13c19182-7128-44f3-abd3-143eaaa4b803')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_13c19182-7128-44f3-abd3-143eaaa4b803" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_13c19182-7128-44f3-abd3-143eaaa4b803" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_13c19182-7128-44f3-abd3-143eaaa4b803" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ConsoleApp1
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IMsgSender
    {
        </span><span style="color: #0000ff;">void</span> Send(<span style="color: #0000ff;">string</span><span style="color: #000000;"> message);
    }
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
    <span style="color: #808080;">///</span><span style="color: #008000;"> 发送到手机
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> TelephoneMsgSender : IMsgSender
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> Send(<span style="color: #0000ff;">string</span><span style="color: #000000;"> message)
        {
            Console.WriteLine(message);
        }
    }
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
    <span style="color: #808080;">///</span><span style="color: #008000;"> 发送到邮箱
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> EmailMsgSender: IMsgSender
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> Send(<span style="color: #0000ff;">string</span><span style="color: #000000;"> message)
        {
            Console.WriteLine(message);
        }
    }
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
    <span style="color: #808080;">///</span><span style="color: #008000;"> 发送到微信
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> WechatMsgSender: IMsgSender
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> Send(<span style="color: #0000ff;">string</span><span style="color: #000000;"> message)
        {
            Console.WriteLine(message);
        }
    }

    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
    <span style="color: #808080;">///</span><span style="color: #008000;"> 通知
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Notification 
    {
        </span><span style="color: #0000ff;">protected</span><span style="color: #000000;"> IMsgSender _msgSender;

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Notification(IMsgSender msgSender)
        {
            _msgSender </span>=<span style="color: #000000;"> msgSender;
        }
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">void</span> notify(<span style="color: #0000ff;">string</span><span style="color: #000000;"> message);
    }

    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
    <span style="color: #808080;">///</span><span style="color: #008000;"> 严重通知
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SevereNotification : Notification
    {
        </span><span style="color: #0000ff;">public</span> SevereNotification(IMsgSender msgSender) : <span style="color: #0000ff;">base</span><span style="color: #000000;">(msgSender)
        {
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span> notify(<span style="color: #0000ff;">string</span><span style="color: #000000;"> message)
        {
            _msgSender.Send(message);
        }
    }
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
    <span style="color: #808080;">///</span><span style="color: #008000;"> 紧急情况通知
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> UrgencyNotification : Notification
    {
        </span><span style="color: #0000ff;">public</span> UrgencyNotification(IMsgSender msgSender) : <span style="color: #0000ff;">base</span><span style="color: #000000;">(msgSender)
        {
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span> notify(<span style="color: #0000ff;">string</span><span style="color: #000000;"> message)
        {
            _msgSender.Send(message);
        }
    }
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
    <span style="color: #808080;">///</span><span style="color: #008000;"> 正常通知
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> NormalNotification : Notification
    {
        </span><span style="color: #0000ff;">public</span> NormalNotification(IMsgSender msgSender) : <span style="color: #0000ff;">base</span><span style="color: #000000;">(msgSender)
        {
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span> notify(<span style="color: #0000ff;">string</span><span style="color: #000000;"> message)
        {
            _msgSender.Send(message);
        }
    }
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
    <span style="color: #808080;">///</span><span style="color: #008000;"> 不重要的通知
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> TrivialNotification : Notification
    {
        </span><span style="color: #0000ff;">public</span> TrivialNotification(IMsgSender msgSender) : <span style="color: #0000ff;">base</span><span style="color: #000000;">(msgSender)
        {
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span> notify(<span style="color: #0000ff;">string</span><span style="color: #000000;"> message)
        {
            _msgSender.Send(message);
        }
    }
}


IMsgSender msgSender </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> TelephoneMsgSender();
Notification notification </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> SevereNotification(msgSender);
notification.notify(</span><span style="color: #800000;">"</span><span style="color: #800000;">通知</span><span style="color: #800000;">"</span><span style="color: #000000;">);
Console.ReadLine();</span></pre>
</div>
<span class="cnblogs_code_collapse">结构代码</span></div>
<p><strong><span style="font-size: 18px;">3，Composite（组合，对象模式）<a name="b3"></a></span></strong></p>
<p><span style="color: #ff6600;"><strong>意图：</strong>将对象组合成树形结构以表示&ldquo;部分-整体&rdquo;的层次结构。Composite使得用户对单个对象和组合对象的使用具有一致性</span></p>
<p><span style="color: #ff6600;"><strong>应用场景：</strong>树形结构</span></p>
<p><span style="color: #ff6600;"><strong>结构：</strong></span></p>
<p>&nbsp;<img src="https://img2023.cnblogs.com/blog/741594/202303/741594-20230328221520280-1779697590.png" alt="" width="426" height="272" loading="lazy" /></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('db4aff7b-a644-4fd8-ac6d-f89318deb159')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_db4aff7b-a644-4fd8-ac6d-f89318deb159" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_db4aff7b-a644-4fd8-ac6d-f89318deb159" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_db4aff7b-a644-4fd8-ac6d-f89318deb159" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> _15_组合模式
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            Component com </span>= <span style="color: #0000ff;">new</span> Composite(<span style="color: #800000;">"</span><span style="color: #800000;">中国</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            
            Component com1</span>=<span style="color: #0000ff;">new</span> Composite(<span style="color: #800000;">"</span><span style="color: #800000;">湖北</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            Component com11 </span>= <span style="color: #0000ff;">new</span> Leaf(<span style="color: #800000;">"</span><span style="color: #800000;">荆门</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            Component com12 </span>= <span style="color: #0000ff;">new</span> Leaf(<span style="color: #800000;">"</span><span style="color: #800000;">武汉</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            com1.Add(com11);
            com1.Add(com12);

            com.Add(com1);

            com.Display(</span><span style="color: #800080;">2</span><span style="color: #000000;">);


            Console.ReadLine();
        }
    }


    </span><span style="color: #008000;">//</span><span style="color: #008000;">组合中的对象声明接口</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Component
    {
        </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">string</span><span style="color: #000000;"> name;
        </span><span style="color: #0000ff;">public</span> Component(<span style="color: #0000ff;">string</span><span style="color: #000000;"> name)
        {
            </span><span style="color: #0000ff;">this</span>.name =<span style="color: #000000;"> name;
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Add(Component c);
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Remove(Component c);
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">void</span> Display(<span style="color: #0000ff;">int</span><span style="color: #000000;"> depth);
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">枝节点</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Composite : Component
    {
        </span><span style="color: #0000ff;">public</span> Composite(<span style="color: #0000ff;">string</span> name) : <span style="color: #0000ff;">base</span><span style="color: #000000;">(name)
        {
        }

        </span><span style="color: #0000ff;">private</span> List&lt;Component&gt; children = <span style="color: #0000ff;">new</span> List&lt;Component&gt;<span style="color: #000000;">(); 
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Add(Component c)
        {
            children.Add(c);
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Remove(Component c)
        {
            children.Remove(c);
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span> Display(<span style="color: #0000ff;">int</span><span style="color: #000000;"> depth)
        {
            Console.WriteLine(</span><span style="color: #0000ff;">new</span> <span style="color: #0000ff;">string</span>(<span style="color: #800000;">'</span><span style="color: #800000;">+</span><span style="color: #800000;">'</span>, depth) +<span style="color: #000000;"> name);
            </span><span style="color: #0000ff;">foreach</span> (<span style="color: #0000ff;">var</span> component <span style="color: #0000ff;">in</span><span style="color: #000000;"> children)
            {
                component.Display(depth </span>+ <span style="color: #800080;">2</span><span style="color: #000000;">);
            }
        }
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">叶节点</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Leaf : Component
    {
        </span><span style="color: #0000ff;">public</span> Leaf(<span style="color: #0000ff;">string</span> name) : <span style="color: #0000ff;">base</span><span style="color: #000000;">(name)
        {
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Add(Component c)
        {
            </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> NotImplementedException();
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Remove(Component c)
        {
            </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> NotImplementedException();
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span> Display(<span style="color: #0000ff;">int</span><span style="color: #000000;"> depth)
        {
            Console.WriteLine(</span><span style="color: #0000ff;">new</span> <span style="color: #0000ff;">string</span>(<span style="color: #800000;">'</span><span style="color: #800000;">+</span><span style="color: #800000;">'</span>, depth) +<span style="color: #000000;"> name);
        }
    }

}

组合模式代码</span></pre>
</div>
<span class="cnblogs_code_collapse">结构代码</span></div>
<p><strong><span style="font-size: 18px;">4，Decorator（装饰，对象模式）<a name="b4"></a></span></strong></p>
<p><span style="color: #ff6600;"><strong>意图：</strong>动态的给一个对象添加一些额外的职责。就添加功能来说，Decorator模式相比生成子类更为灵活</span></p>
<p><span style="color: #ff6600;"><strong>应用场景：</strong>给对象添加额外的职责</span></p>
<p><span style="color: #ff6600;"><strong>结构：</strong></span></p>
<p><strong><img src="https://img2023.cnblogs.com/blog/741594/202303/741594-20230328222952752-794157740.png" alt="" width="520" height="287" loading="lazy" /></strong></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('f646eacc-4091-4ae4-8912-71e08061bb2d')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_f646eacc-4091-4ae4-8912-71e08061bb2d" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_f646eacc-4091-4ae4-8912-71e08061bb2d" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_f646eacc-4091-4ae4-8912-71e08061bb2d" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> _3_装饰模式
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            ConcreteComponent con </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> ConcreteComponent();
            ConcreteDecoratorA conA </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> ConcreteDecoratorA();
            ConcreteDecoratorB conB </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> ConcreteDecoratorB();
            conA.SetComponent(con);
            conB.SetComponent(conA);
            conB.Operation();

            Console.ReadLine();

        }
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">抽象对象类</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Component
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Operation();
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">具体对象类</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ConcreteComponent : Component
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Operation()
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">具体对象类</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">装饰类</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Decorator : Component
    {
        </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> Component component;
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> SetComponent(Component component)
        {
            </span><span style="color: #0000ff;">this</span>.component =<span style="color: #000000;"> component;
        }
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Operation()
        {
            </span><span style="color: #0000ff;">if</span> (component != <span style="color: #0000ff;">null</span><span style="color: #000000;">)
                component.Operation();
        }
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ConcreteDecoratorA : Decorator
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Operation()
        {
            </span><span style="color: #0000ff;">base</span><span style="color: #000000;">.Operation();
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">具体的职责A</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ConcreteDecoratorB : Decorator
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Operation()
        {
            </span><span style="color: #0000ff;">base</span><span style="color: #000000;">.Operation();
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">具体的职责B</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }
    }

}

装饰模式代码</span></pre>
</div>
<span class="cnblogs_code_collapse">结构代码</span></div>
<p><strong><span style="font-size: 18px;">5，Facade（外观，对象模式）<a name="b5"></a></span></strong></p>
<p><span style="color: #ff6600;"><strong>意图：</strong>为子系统中的一组接口提供一个一致的界面，Facade模式定义了一个高层接口，这个接口使得这一子系统更加容易使用</span></p>
<p><span style="color: #ff6600;"><strong>应用场景：</strong>为多个子系统提供一个统一的接口，减少相互之间的依赖</span></p>
<p><span style="color: #ff6600;"><strong>结构：</strong></span></p>
<p>&nbsp;<img src="https://img2023.cnblogs.com/blog/741594/202303/741594-20230329204741196-1628389932.png" alt="" width="452" height="300" loading="lazy" /></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('57f37471-838f-42d3-9be1-ee629780333a')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_57f37471-838f-42d3-9be1-ee629780333a" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_57f37471-838f-42d3-9be1-ee629780333a" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_57f37471-838f-42d3-9be1-ee629780333a" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> _8_外观模式
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            Facade f </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> Facade();
            f.MethodA();
            f.MethodB();

            Console.ReadLine();
        }
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">外观类</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Facade
    {
        </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> SubSystemOne one;
        </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> SubSystemTwo two;
        </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> SubSystemThree three;
        </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> SubSystemFour four;

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Facade()
        {
            one </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> SubSystemOne();
            two </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> SubSystemTwo();
            three </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> SubSystemThree();
            four </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> SubSystemFour();
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> MethodA()
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">方法组一</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            one.MethodOne();
            two.MethodTwo();
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> MethodB()
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">方法组二</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            three.MethodThree();
            four.MethodFour();
        }

    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">子系统类</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SubSystemOne
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> MethodOne()
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">子系统方法1</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }
    }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SubSystemTwo
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> MethodTwo()
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">子系统方法2</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }
    }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SubSystemThree
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> MethodThree()
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">子系统方法3</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }
    }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SubSystemFour
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> MethodFour()
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">子系统方法4</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }
    }
}

外观模式代码</span></pre>
</div>
<span class="cnblogs_code_collapse">结构代码</span></div>
<p><strong><span style="font-size: 18px;">6，Flyweight（享元，对象模式）&nbsp;<a name="b6"></a></span></strong></p>
<p><span style="color: #ff6600;"><strong>意图：</strong>运用共享技术有效地支持大量细粒度的对象</span></p>
<p><span style="color: #ff6600;"><strong>应用场景：</strong>当一个系统中存在大量重复对象的时候，我们就可以利用享元模式</span></p>
<p><span style="color: #ff6600;"><strong>结构：</strong></span></p>
<p><img src="https://img2023.cnblogs.com/blog/741594/202303/741594-20230329223115636-818512901.png" alt="" width="454" height="270" loading="lazy" /></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('c1141a20-098e-4338-8536-2dec6a2464fd')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_c1141a20-098e-4338-8536-2dec6a2464fd" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_c1141a20-098e-4338-8536-2dec6a2464fd" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_c1141a20-098e-4338-8536-2dec6a2464fd" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 定义享元接口</span>
<span style="color: #0000ff;">interface</span><span style="color: #000000;"> IShape
{
    </span><span style="color: #0000ff;">void</span> Draw(<span style="color: #0000ff;">int</span> x, <span style="color: #0000ff;">int</span><span style="color: #000000;"> y);
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 实现享元类</span>
<span style="color: #0000ff;">class</span><span style="color: #000000;"> Circle : IShape
{
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">string</span><span style="color: #000000;"> color;

    </span><span style="color: #0000ff;">public</span> Circle(<span style="color: #0000ff;">string</span><span style="color: #000000;"> color)
    {
        </span><span style="color: #0000ff;">this</span>.color =<span style="color: #000000;"> color;
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> Draw(<span style="color: #0000ff;">int</span> x, <span style="color: #0000ff;">int</span><span style="color: #000000;"> y)
    {
        Console.WriteLine($</span><span style="color: #800000;">"</span><span style="color: #800000;">在坐标 ({x}, {y}) 画了一个 {color} 的圆形</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 实现享元工厂类</span>
<span style="color: #0000ff;">class</span><span style="color: #000000;"> ShapeFactory
{
    </span><span style="color: #0000ff;">private</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, IShape&gt; shapes = <span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, IShape&gt;<span style="color: #000000;">();

    </span><span style="color: #0000ff;">public</span> IShape GetCircle(<span style="color: #0000ff;">string</span><span style="color: #000000;"> color)
    {
        </span><span style="color: #0000ff;">if</span> (shapes.TryGetValue(color, <span style="color: #0000ff;">out</span><span style="color: #000000;"> IShape shape))
        {
            Console.WriteLine($</span><span style="color: #800000;">"</span><span style="color: #800000;">使用已存在的 {color} 圆形</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> shape;
        }
        </span><span style="color: #0000ff;">else</span><span style="color: #000000;">
        {
            IShape newShape </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> Circle(color);
            shapes[color] </span>=<span style="color: #000000;"> newShape;
            Console.WriteLine($</span><span style="color: #800000;">"</span><span style="color: #800000;">创建新的 {color} 圆形</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> newShape;
        }
    }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 客户端代码</span>
<span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
{
    </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
    {
        ShapeFactory factory </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> ShapeFactory();

        IShape redCircle </span>= factory.GetCircle(<span style="color: #800000;">"</span><span style="color: #800000;">红色</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        redCircle.Draw(</span><span style="color: #800080;">1</span>, <span style="color: #800080;">2</span><span style="color: #000000;">);

        IShape blueCircle </span>= factory.GetCircle(<span style="color: #800000;">"</span><span style="color: #800000;">蓝色</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        blueCircle.Draw(</span><span style="color: #800080;">3</span>, <span style="color: #800080;">4</span><span style="color: #000000;">);

        IShape greenCircle </span>= factory.GetCircle(<span style="color: #800000;">"</span><span style="color: #800000;">绿色</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        greenCircle.Draw(</span><span style="color: #800080;">5</span>, <span style="color: #800080;">6</span><span style="color: #000000;">);

        IShape redCircle2 </span>= factory.GetCircle(<span style="color: #800000;">"</span><span style="color: #800000;">红色</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        redCircle2.Draw(</span><span style="color: #800080;">7</span>, <span style="color: #800080;">8</span><span style="color: #000000;">);
    }
}



创建新的 红色 圆形
在坐标 (</span><span style="color: #800080;">1</span>, <span style="color: #800080;">2</span><span style="color: #000000;">) 画了一个 红色 的圆形
创建新的 蓝色 圆形
在坐标 (</span><span style="color: #800080;">3</span>, <span style="color: #800080;">4</span><span style="color: #000000;">) 画了一个 蓝色 的圆形
创建新的 绿色 圆形
在坐标 (</span><span style="color: #800080;">5</span>, <span style="color: #800080;">6</span><span style="color: #000000;">) 画了一个 绿色 的圆形
使用已存在的 红色 圆形
在坐标 (</span><span style="color: #800080;">7</span>, <span style="color: #800080;">8</span>) 画了一个 红色 的圆形</pre>
</div>
<span class="cnblogs_code_collapse">结构代码</span></div>
<p><strong><span style="font-size: 18px;">7，Proxy（代理，对象模式）&nbsp;<a name="b7"></a></span></strong></p>
<p><span style="color: #ff6600;"><strong>意图：</strong>为其他对象提供一种代理以控制对这个对象的访问</span></p>
<p><span style="color: #ff6600;"><strong>应用场景：</strong>代理对象访问</span></p>
<p><span style="color: #ff6600;"><strong>结构：</strong></span></p>
<p><img src="https://img2023.cnblogs.com/blog/741594/202303/741594-20230330204138881-1288428972.png" alt="" width="420" height="311" loading="lazy" /></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('50ff2d05-9792-48a2-80d4-80065094a0f3')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_50ff2d05-9792-48a2-80d4-80065094a0f3" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_50ff2d05-9792-48a2-80d4-80065094a0f3" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_50ff2d05-9792-48a2-80d4-80065094a0f3" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> _4_代理模式
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            Proxy pro </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> Proxy();
            pro.Request();

            Console.ReadLine();
        }
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">接口</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> Subject
    {
        </span><span style="color: #0000ff;">void</span><span style="color: #000000;"> Request();
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">真实对象</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> RealSubject : Subject
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Request()
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">请求访问</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }
    }
    </span><span style="color: #008000;">//</span><span style="color: #008000;">代理</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Proxy : Subject
    {
        </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> RealSubject realSubject;
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Request()
        {
            </span><span style="color: #0000ff;">if</span> (realSubject == <span style="color: #0000ff;">null</span><span style="color: #000000;">)
                realSubject </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> RealSubject();
            </span><span style="color: #008000;">//</span><span style="color: #008000;">额外职责</span>
            Console.WriteLine(<span style="color: #800000;">"</span><span style="color: #800000;">额外职责</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            realSubject.Request();
        }
    }


}

代理模式代码</span></pre>
</div>
<span class="cnblogs_code_collapse">结构代码</span></div>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: rgba(22, 159, 230, 1);"><span style="color: rgba(255, 255, 255, 1);">三、行为型<a name="c"></a></span></p>
<p><strong><span style="font-size: 18px;">1，Chain of Responsibility（职责链，对象模式）<a name="c1"></a></span></strong></p>
<p><span style="color: #ff6600;"><strong>意图：</strong>使多个对象都有机会处理请求，从而避免请求的发送者和接收者之间的耦合关系。将这些对象连成一条链，并沿着这条链传递该请求，直到有一个对象处理它为止</span></p>
<p><span style="color: #ff6600;"><strong>应用场景：</strong>处理管道</span></p>
<p><span style="color: #ff6600;"><strong>结构：</strong></span></p>
<p><img src="https://img2023.cnblogs.com/blog/741594/202304/741594-20230406220327361-71714622.png" alt="" loading="lazy" /></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('1a7244be-dd47-4b4f-a997-b898c5d91d89')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_1a7244be-dd47-4b4f-a997-b898c5d91d89" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_1a7244be-dd47-4b4f-a997-b898c5d91d89" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_1a7244be-dd47-4b4f-a997-b898c5d91d89" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> _19_职责链模式
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            Handle h1 </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> ConcreteHandleA();
            Handle h2 </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> ConcreteHandleB();
            h1.SetSuccessor(h2);

            h1.HandleRequest(</span><span style="color: #800080;">11</span><span style="color: #000000;">);

            Console.ReadLine();

        }
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">定义处理请求的接口</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Handle
    {
        </span><span style="color: #0000ff;">protected</span><span style="color: #000000;"> Handle handle;

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> SetSuccessor(Handle successor)
        {
            handle </span>=<span style="color: #000000;"> successor;
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">void</span> HandleRequest(<span style="color: #0000ff;">int</span><span style="color: #000000;"> request);
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">具体处理者</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ConcreteHandleA : Handle
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span> HandleRequest(<span style="color: #0000ff;">int</span><span style="color: #000000;"> request)
        {
            </span><span style="color: #0000ff;">if</span> (request &lt; <span style="color: #800080;">10</span><span style="color: #000000;">)
            {
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">ConcreteHandleA处理</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }
            </span><span style="color: #0000ff;">else</span><span style="color: #000000;">
            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;">后继者处理</span>
<span style="color: #000000;">                handle.HandleRequest(request);
            }
        }
    }
    </span><span style="color: #008000;">//</span><span style="color: #008000;">具体处理者</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ConcreteHandleB : Handle
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span> HandleRequest(<span style="color: #0000ff;">int</span><span style="color: #000000;"> request)
        {
            </span><span style="color: #0000ff;">if</span> (request &gt; <span style="color: #800080;">10</span><span style="color: #000000;">)
            {
                Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">ConcreteHandleB处理</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }
            </span><span style="color: #0000ff;">else</span><span style="color: #000000;">
            {
                </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> Exception(<span style="color: #800000;">"</span><span style="color: #800000;">异常</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }
        }
    }

}

职责链模式代码</span></pre>
</div>
<span class="cnblogs_code_collapse">结构代码</span></div>
<p><strong><span style="font-size: 18px;">2，Command（命令，对象模式）<a name="c2"></a></span></strong></p>
<p><span style="color: #ff6600;"><strong>意图：</strong>将一个请求封装为一个对象，从而使你可用不同的请求对象对客户进行参数化，对请求排队或记录请求日志，以及支持可撤销的操作</span></p>
<p><span style="color: #ff6600;"><strong>应用场景：</strong>将请求封装为对象</span></p>
<p><span style="color: #ff6600;"><strong>结构：</strong></span></p>
<p><img src="https://img2023.cnblogs.com/blog/741594/202304/741594-20230409124934005-41864775.png" alt="" width="502" height="270" loading="lazy" /></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('586ebcad-4311-4461-ab22-70feaed4d4b3')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_586ebcad-4311-4461-ab22-70feaed4d4b3" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_586ebcad-4311-4461-ab22-70feaed4d4b3" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_586ebcad-4311-4461-ab22-70feaed4d4b3" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> _18_命令模式
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            Reciver r </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> Reciver();
            Invoker inv </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> Invoker();

            Commend comA </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> ConcreteCommendA(r);
            Commend comB </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> ConcreteCommendB(r);
            inv.SetCommend(comA);
            inv.SetCommend(comB);
            inv.Notify();

            Console.ReadLine();
        }
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">接受者（厨师）</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Reciver
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> ActionA()
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">做鱼香肉丝</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> ActionB()
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">做番茄操蛋</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">抽象命令</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Commend
    {
        </span><span style="color: #0000ff;">protected</span><span style="color: #000000;"> Reciver reciver;
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Commend(Reciver reciver)
        {
            </span><span style="color: #0000ff;">this</span>.reciver =<span style="color: #000000;"> reciver;
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Execute();
    }
    </span><span style="color: #008000;">//</span><span style="color: #008000;">具体的命令（做鱼香肉丝）</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ConcreteCommendA : Commend
    {
        </span><span style="color: #0000ff;">public</span> ConcreteCommendA(Reciver reciver) : <span style="color: #0000ff;">base</span><span style="color: #000000;">(reciver)
        {
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Execute()
        {
            reciver.ActionA();
        }
    }
    </span><span style="color: #008000;">//</span><span style="color: #008000;">具体的命令（做番茄操蛋）</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ConcreteCommendB : Commend
    {
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> ConcreteCommendB(Reciver reciver)
            : </span><span style="color: #0000ff;">base</span><span style="color: #000000;">(reciver)
        {
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Execute()
        {
            reciver.ActionB();
        }
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">调用者（服务员）</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Invoker
    {
        </span><span style="color: #0000ff;">private</span> List&lt;Commend&gt; commends = <span style="color: #0000ff;">new</span> List&lt;Commend&gt;<span style="color: #000000;">();

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> SetCommend(Commend c)
        {
            Console.WriteLine(</span><span style="color: #0000ff;">string</span>.Format(<span style="color: #800000;">"</span><span style="color: #800000;">下单时间{0}</span><span style="color: #800000;">"</span><span style="color: #000000;">,DateTime.Now));
            commends.Add(c);
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> RemoveCommend(Commend c)
        {
            Console.WriteLine(</span><span style="color: #0000ff;">string</span>.Format(<span style="color: #800000;">"</span><span style="color: #800000;">取消时间{0}</span><span style="color: #800000;">"</span><span style="color: #000000;">, DateTime.Now));
            commends.Remove(c);
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Notify()
        {
            </span><span style="color: #0000ff;">foreach</span> (<span style="color: #0000ff;">var</span> commend <span style="color: #0000ff;">in</span><span style="color: #000000;"> commends)
            {
                commend.Execute();
            }
        }
    }

}

命令模式代码</span></pre>
</div>
<span class="cnblogs_code_collapse">结构代码</span></div>
<p><strong><span style="font-size: 18px;">3，Interpreter（解释器，类模式）&nbsp;<a name="c3"></a></span></strong></p>
<p><span style="color: #ff6600;"><strong>意图：</strong>给定一个语言，定义它的文法的一种表示，并定义一个解释器，这个解释器使用该表示来解释语言中的句子</span></p>
<p><span style="color: #ff6600;"><strong>应用场景：</strong>解释对象</span></p>
<p><span style="color: #ff6600;"><strong>结构：</strong></span></p>
<p><img src="https://img2023.cnblogs.com/blog/741594/202304/741594-20230409130117392-1804902025.png" alt="" width="392" height="254" loading="lazy" /></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('abbfc4a5-7cd7-44af-9b31-81b16c4825ac')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_abbfc4a5-7cd7-44af-9b31-81b16c4825ac" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_abbfc4a5-7cd7-44af-9b31-81b16c4825ac" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_abbfc4a5-7cd7-44af-9b31-81b16c4825ac" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> _22_解释器模式
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            Context con </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> Context();
            con.Message </span>= <span style="color: #800000;">"</span><span style="color: #800000;">Hunter</span><span style="color: #800000;">"</span><span style="color: #000000;">;

            AbstractExpression abe1</span>=<span style="color: #0000ff;">new</span><span style="color: #000000;"> InExpression();
            abe1.Interperter(con);
            Console.WriteLine(con.Message);

            AbstractExpression abe2 </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> DeExpression();
            abe2.Interperter(con);
            Console.WriteLine(con.Message);

            Console.ReadLine();
        }
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">需要解释的类</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Context
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Message { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">抽象解释器</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> AbstractExpression
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Interperter(Context con);
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">加密</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> InExpression : AbstractExpression
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Interperter(Context con)
        {
            con.Message </span>= <span style="color: #800000;">"</span><span style="color: #800000;">加密之后的字符</span><span style="color: #800000;">"</span><span style="color: #000000;">;
        }
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">解密</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> DeExpression : AbstractExpression
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Interperter(Context con)
        {
            con.Message </span>= <span style="color: #800000;">"</span><span style="color: #800000;">解密之后的字符</span><span style="color: #800000;">"</span><span style="color: #000000;">;
        }
    }

}
解释器模式代码</span></pre>
</div>
<span class="cnblogs_code_collapse">结构代码</span></div>
<p><span style="font-size: 18px;"><strong>4，Iterator（迭代器，对象模式）&nbsp;&nbsp;<a name="c4"></a></strong></span></p>
<p><span style="color: #ff6600;"><strong>意图：</strong>提供一种方法顺序访问一个聚合对象中的各个元素，而又不需要暴露该对象的内部表示</span></p>
<p><span style="color: #ff6600;"><strong>应用场景：</strong>顺序访问集合的各个元素</span></p>
<p><span style="color: #ff6600;"><strong>结构：</strong></span></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('48359eb8-c6d7-4c1f-b799-5d624ba3e5fb')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_48359eb8-c6d7-4c1f-b799-5d624ba3e5fb" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_48359eb8-c6d7-4c1f-b799-5d624ba3e5fb" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_48359eb8-c6d7-4c1f-b799-5d624ba3e5fb" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections;

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyCollection : IEnumerable
{
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">int</span><span style="color: #000000;">[] items;

    </span><span style="color: #0000ff;">public</span> MyCollection(<span style="color: #0000ff;">int</span><span style="color: #000000;">[] items)
    {
        </span><span style="color: #0000ff;">this</span>.items =<span style="color: #000000;"> items;
    }

    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> IEnumerator GetEnumerator()
    {
        </span><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> i = <span style="color: #800080;">0</span>; i &lt; items.Length; i++<span style="color: #000000;">)
        {
            </span><span style="color: #0000ff;">yield</span> <span style="color: #0000ff;">return</span><span style="color: #000000;"> items[i];
        }
    }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Main()
    {
        MyCollection collection </span>= <span style="color: #0000ff;">new</span> MyCollection(<span style="color: #0000ff;">new</span> <span style="color: #0000ff;">int</span>[] { <span style="color: #800080;">1</span>, <span style="color: #800080;">2</span>, <span style="color: #800080;">3</span>, <span style="color: #800080;">4</span>, <span style="color: #800080;">5</span><span style="color: #000000;"> });

        </span><span style="color: #0000ff;">foreach</span> (<span style="color: #0000ff;">int</span> item <span style="color: #0000ff;">in</span><span style="color: #000000;"> collection)
        {
            Console.WriteLine(item);
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">结构代码</span></div>
<p><strong><span style="font-size: 18px;">5，Mediator（中介者，对象模式）<a name="c5"></a></span></strong></p>
<p><span style="color: #ff6600;"><strong>意图：</strong>提用一个中介对象来封装一系列的对象交互。中介者是各对象不需要显示地相互引用，从而使其耦合松散，而且可以独立地改变他们之间的交互</span></p>
<p><span style="color: #ff6600;"><strong>应用场景：</strong>中介对象来封装一系列的对象交互</span></p>
<p><span style="color: #ff6600;"><strong>结构：</strong></span></p>
<p><img src="https://img2023.cnblogs.com/blog/741594/202304/741594-20230409155549325-70786554.png" alt="" width="739" height="372" loading="lazy" /></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('2944aba3-7580-4f10-81a6-5deba8443f89')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_2944aba3-7580-4f10-81a6-5deba8443f89" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_2944aba3-7580-4f10-81a6-5deba8443f89" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_2944aba3-7580-4f10-81a6-5deba8443f89" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Mvc;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ConsoleApp1
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IMediator
    {
        </span><span style="color: #0000ff;">void</span><span style="color: #000000;"> RegisterComponent(IComponent component);
        </span><span style="color: #0000ff;">void</span> Notify(<span style="color: #0000ff;">string</span><span style="color: #000000;"> message, IComponent sender);
    }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ConcreteMediator : IMediator
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span> List&lt;IComponent&gt; _components = <span style="color: #0000ff;">new</span> List&lt;IComponent&gt;<span style="color: #000000;">();

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> RegisterComponent(IComponent component)
        {
            _components.Add(component);
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> Notify(<span style="color: #0000ff;">string</span><span style="color: #000000;"> message, IComponent sender)
        {
            </span><span style="color: #0000ff;">foreach</span> (<span style="color: #0000ff;">var</span> component <span style="color: #0000ff;">in</span><span style="color: #000000;"> _components)
            {
                </span><span style="color: #0000ff;">if</span> (component !=<span style="color: #000000;"> sender)
                {
                    component.Receive(message);
                }
            }
        }
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IComponent
    {
        </span><span style="color: #0000ff;">void</span> Send(<span style="color: #0000ff;">string</span><span style="color: #000000;"> message);
        </span><span style="color: #0000ff;">void</span> Receive(<span style="color: #0000ff;">string</span><span style="color: #000000;"> message);
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ConcreteComponentA : IComponent
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> IMediator _mediator;

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> ConcreteComponentA(IMediator mediator)
        {
            _mediator </span>=<span style="color: #000000;"> mediator;
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> Send(<span style="color: #0000ff;">string</span><span style="color: #000000;"> message)
        {
            _mediator.Notify(message, </span><span style="color: #0000ff;">this</span><span style="color: #000000;">);
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> Receive(<span style="color: #0000ff;">string</span><span style="color: #000000;"> message)
        {
            Console.WriteLine($</span><span style="color: #800000;">"</span><span style="color: #800000;">Component A received message: {message}</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ConcreteComponentB : IComponent
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> IMediator _mediator;

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> ConcreteComponentB(IMediator mediator)
        {
            _mediator </span>=<span style="color: #000000;"> mediator;
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> Send(<span style="color: #0000ff;">string</span><span style="color: #000000;"> message)
        {
            _mediator.Notify(message, </span><span style="color: #0000ff;">this</span><span style="color: #000000;">);
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> Receive(<span style="color: #0000ff;">string</span><span style="color: #000000;"> message)
        {
            Console.WriteLine($</span><span style="color: #800000;">"</span><span style="color: #800000;">Component B received message: {message}</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> HomeController : Controller
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> IMediator _mediator;

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> HomeController(IMediator mediator)
        {
            _mediator </span>=<span style="color: #000000;"> mediator;
        }

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> IActionResult Index()
        {
            </span><span style="color: #0000ff;">var</span> componentA = <span style="color: #0000ff;">new</span><span style="color: #000000;"> ConcreteComponentA(_mediator);
            </span><span style="color: #0000ff;">var</span> componentB = <span style="color: #0000ff;">new</span><span style="color: #000000;"> ConcreteComponentB(_mediator);
            _mediator.RegisterComponent(componentA);
            _mediator.RegisterComponent(componentB);

            componentA.Send(</span><span style="color: #800000;">"</span><span style="color: #800000;">Hello from component A</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            componentB.Send(</span><span style="color: #800000;">"</span><span style="color: #800000;">Hello from component B</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> View();
        }
    }

}</span></pre>
</div>
<span class="cnblogs_code_collapse">结构代码</span></div>
<p><strong><span style="font-size: 18px;">6，Memento（备忘录，对象模式）<a name="c6"></a>&nbsp;</span> &nbsp;</strong></p>
<p><span style="color: #ff6600;"><strong>意图：</strong>在不破坏封装的前提下，捕获一个对象的内部状态，并在该对象之外保存这个状态。这样以后就可将该对象恢复到原先保存的状态。</span></p>
<p><span style="color: #ff6600;"><strong>应用场景：</strong>这可以用于实现&ldquo;撤销&rdquo;和&ldquo;重做&rdquo;等功能，或者在发生意外情况时还原对象状态</span></p>
<p><span style="color: #ff6600;"><strong>结构：</strong></span></p>
<p>&nbsp;<img src="https://img2023.cnblogs.com/blog/741594/202304/741594-20230410211218115-711931729.png" alt="" width="611" height="332" loading="lazy" /></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('006967cc-9a01-4b28-a68a-e0996b3b8c32')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_006967cc-9a01-4b28-a68a-e0996b3b8c32" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_006967cc-9a01-4b28-a68a-e0996b3b8c32" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_006967cc-9a01-4b28-a68a-e0996b3b8c32" class="cnblogs_code_hide">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">备忘录类</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Memento
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> State { <span style="color: #0000ff;">get</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span> Memento(<span style="color: #0000ff;">string</span><span style="color: #000000;"> state)
    {
        State </span>=<span style="color: #000000;"> state;
    }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">原始对象类</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Originator
{
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">string</span><span style="color: #000000;"> _state;

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span><span style="color: #000000;"> State
    {
        </span><span style="color: #0000ff;">get</span> =&gt;<span style="color: #000000;"> _state;
        </span><span style="color: #0000ff;">set</span><span style="color: #000000;">
        {
            Console.WriteLine($</span><span style="color: #800000;">"</span><span style="color: #800000;">Setting state to {value}</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            _state </span>=<span style="color: #000000;"> value;
        }
    }

    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Memento SaveState()
    {
        Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">Saving state...</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> Memento(_state);
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> RestoreState(Memento memento)
    {
        Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">Restoring state...</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        _state </span>=<span style="color: #000000;"> memento.State;
    }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">备忘录管理类</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Caretaker
{
    </span><span style="color: #0000ff;">public</span> Memento Memento { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">使用备忘录模式</span>
<span style="color: #0000ff;">var</span> originator = <span style="color: #0000ff;">new</span><span style="color: #000000;"> Originator();
</span><span style="color: #0000ff;">var</span> caretaker = <span style="color: #0000ff;">new</span><span style="color: #000000;"> Caretaker();

originator.State </span>= <span style="color: #800000;">"</span><span style="color: #800000;">State 1</span><span style="color: #800000;">"</span><span style="color: #000000;">;
caretaker.Memento </span>=<span style="color: #000000;"> originator.SaveState();

originator.State </span>= <span style="color: #800000;">"</span><span style="color: #800000;">State 2</span><span style="color: #800000;">"</span><span style="color: #000000;">;

</span><span style="color: #008000;">//</span><span style="color: #008000;">还原状态</span>
originator.RestoreState(caretaker.Memento);</pre>
</div>
<span class="cnblogs_code_collapse">结构代码</span></div>
<p><strong><span style="font-size: 18px;">7，Observer（观察者，对象模式）<a name="c7"></a></span></strong></p>
<p><span style="color: #ff6600;"><strong>意图：</strong>定义对象间的一种一对多的依赖关系，当一个对象的状态发生改变时，所有依赖于它的对象都得到通知并被自动更新</span></p>
<p><span style="color: #ff6600;"><strong>应用场景：</strong>发布通知</span></p>
<p><span style="color: #ff6600;"><strong>结构：</strong></span></p>
<p><img src="https://img2023.cnblogs.com/blog/741594/202304/741594-20230410211842683-2125486534.png" alt="" width="585" height="313" loading="lazy" /></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('5e992e95-16f0-4f1c-aea6-872c51de8ca8')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_5e992e95-16f0-4f1c-aea6-872c51de8ca8" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_5e992e95-16f0-4f1c-aea6-872c51de8ca8" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_5e992e95-16f0-4f1c-aea6-872c51de8ca8" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> _10_观察者模式
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            ConcreteSubject conS </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> ConcreteSubject();

            ConcreteObserver conO </span>= <span style="color: #0000ff;">new</span> ConcreteObserver(<span style="color: #800000;">"</span><span style="color: #800000;">具体观察者</span><span style="color: #800000;">"</span><span style="color: #000000;">,conS);

            conS.Attach(conO);

            conS.State </span>= <span style="color: #800000;">"</span><span style="color: #800000;">主题状态变化了</span><span style="color: #800000;">"</span><span style="color: #000000;">;
            conS.Notify();

            Console.ReadLine();

        }
    }


    </span><span style="color: #008000;">//</span><span style="color: #008000;">抽象观察者</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Observer
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Update();
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">具体观察者</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ConcreteObserver:Observer
    {
        </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> Subject subject;
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">string</span><span style="color: #000000;"> name;

        </span><span style="color: #0000ff;">public</span> ConcreteObserver(<span style="color: #0000ff;">string</span><span style="color: #000000;"> name, Subject subject)
        {
            </span><span style="color: #0000ff;">this</span>.name =<span style="color: #000000;"> name;
            </span><span style="color: #0000ff;">this</span>.subject =<span style="color: #000000;"> subject;
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Update()
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">{0}。{1}通知到了</span><span style="color: #800000;">"</span><span style="color: #000000;">, subject.State,name);
        }
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">抽象主题</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Subject
    {
        </span><span style="color: #0000ff;">private</span> List&lt;Observer&gt; observerList = <span style="color: #0000ff;">new</span> List&lt;Observer&gt;<span style="color: #000000;">();

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Attach(Observer ob)
        {
            observerList.Add(ob);
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Detach(Observer ob)
        {
            observerList.Remove(ob);
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Notify()
        {
            </span><span style="color: #0000ff;">foreach</span> (<span style="color: #0000ff;">var</span> observer <span style="color: #0000ff;">in</span><span style="color: #000000;"> observerList)
            {
                observer.Update();
            }
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">string</span> State { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">具体主题</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ConcreteSubject : Subject
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">string</span><span style="color: #000000;"> _state;

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">string</span><span style="color: #000000;"> State
        {
            </span><span style="color: #0000ff;">get</span> { <span style="color: #0000ff;">return</span><span style="color: #000000;"> _state; }
            </span><span style="color: #0000ff;">set</span> { _state =<span style="color: #000000;"> value; }
        }
    }


}

观察者模式代码</span></pre>
</div>
<span class="cnblogs_code_collapse">结构代码</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('135c0275-c9d8-48c1-bd3f-f76f3debe5a5')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_135c0275-c9d8-48c1-bd3f-f76f3debe5a5" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_135c0275-c9d8-48c1-bd3f-f76f3debe5a5" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_135c0275-c9d8-48c1-bd3f-f76f3debe5a5" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> ObserverPattern
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> MyObservable : IObservable&lt;<span style="color: #0000ff;">string</span>&gt;<span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">private</span> List&lt;IObserver&lt;<span style="color: #0000ff;">string</span>&gt;&gt;<span style="color: #000000;"> observers;

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> MyObservable()
        {
            observers </span>= <span style="color: #0000ff;">new</span> List&lt;IObserver&lt;<span style="color: #0000ff;">string</span>&gt;&gt;<span style="color: #000000;">();
        }

        </span><span style="color: #0000ff;">public</span> IDisposable Subscribe(IObserver&lt;<span style="color: #0000ff;">string</span>&gt;<span style="color: #000000;"> observer)
        {
            </span><span style="color: #0000ff;">if</span> (!<span style="color: #000000;">observers.Contains(observer))
            {
                observers.Add(observer);
            }
            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> Unsubscriber(observers, observer);
        }

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Unsubscriber : IDisposable
        {
            </span><span style="color: #0000ff;">private</span> List&lt;IObserver&lt;<span style="color: #0000ff;">string</span>&gt;&gt;<span style="color: #000000;"> _observers;
            </span><span style="color: #0000ff;">private</span> IObserver&lt;<span style="color: #0000ff;">string</span>&gt;<span style="color: #000000;"> _observer;

            </span><span style="color: #0000ff;">public</span> Unsubscriber(List&lt;IObserver&lt;<span style="color: #0000ff;">string</span>&gt;&gt; observers, IObserver&lt;<span style="color: #0000ff;">string</span>&gt;<span style="color: #000000;"> observer)
            {
                _observers </span>=<span style="color: #000000;"> observers;
                _observer </span>=<span style="color: #000000;"> observer;
            }

            </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Dispose()
            {
                </span><span style="color: #0000ff;">if</span> (_observer != <span style="color: #0000ff;">null</span> &amp;&amp;<span style="color: #000000;"> _observers.Contains(_observer))
                {
                    _observers.Remove(_observer);
                }
            }
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> NotifyObservers(<span style="color: #0000ff;">string</span><span style="color: #000000;"> message)
        {
            </span><span style="color: #0000ff;">foreach</span> (<span style="color: #0000ff;">var</span> observer <span style="color: #0000ff;">in</span><span style="color: #000000;"> observers)
            {
                observer.OnNext(message);
            }
        }
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> MyObserver : IObserver&lt;<span style="color: #0000ff;">string</span>&gt;<span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> IDisposable unsubscriber;

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">virtual</span> <span style="color: #0000ff;">void</span> Subscribe(IObservable&lt;<span style="color: #0000ff;">string</span>&gt;<span style="color: #000000;"> provider)
        {
            unsubscriber </span>= provider.Subscribe(<span style="color: #0000ff;">this</span><span style="color: #000000;">);
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">virtual</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Unsubscribe()
        {
            unsubscriber.Dispose();
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">virtual</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> OnCompleted()
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">Observer completed</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">virtual</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> OnError(Exception e)
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">Observer error: {0}</span><span style="color: #800000;">"</span><span style="color: #000000;">, e.Message);
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">virtual</span> <span style="color: #0000ff;">void</span> OnNext(<span style="color: #0000ff;">string</span><span style="color: #000000;"> value)
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">Observer got value: {0}</span><span style="color: #800000;">"</span><span style="color: #000000;">, value);
        }
    }

    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            MyObservable observable </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> MyObservable();
            MyObserver observer1 </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> MyObserver();
            MyObserver observer2 </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> MyObserver();

            observer1.Subscribe(observable);
            observer2.Subscribe(observable);

            observable.NotifyObservers(</span><span style="color: #800000;">"</span><span style="color: #800000;">Hello World!</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            observer1.Unsubscribe();

            observable.NotifyObservers(</span><span style="color: #800000;">"</span><span style="color: #800000;">Goodbye World!</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            Console.ReadKey();
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">IObservable 和 IObserver </span></div>
<p><strong><span style="font-size: 18px;">8，State（状态，对象模式）<a name="c8"></a>&nbsp;</span></strong></p>
<p><span style="color: #ff6600;"><strong>意图：</strong>允许一个对象在其内部状态改变时改变它的行为。对象看起来似乎修改了它的类</span></p>
<p><span style="color: #ff6600;"><strong>应用场景：</strong>发布通知</span></p>
<p><span style="color: #ff6600;"><strong>结构：</strong></span></p>
<p>&nbsp;<img src="https://img2023.cnblogs.com/blog/741594/202304/741594-20230410224441065-1562133506.png" alt="" width="775" height="303" loading="lazy" /></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('3e877375-7d7f-4f43-b67f-2998988bd93d')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_3e877375-7d7f-4f43-b67f-2998988bd93d" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_3e877375-7d7f-4f43-b67f-2998988bd93d" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_3e877375-7d7f-4f43-b67f-2998988bd93d" class="cnblogs_code_hide">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> 定义状态接口</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IOrderState
{
    </span><span style="color: #0000ff;">void</span><span style="color: #000000;"> Process(Order order);
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 实现具体状态类</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> NewOrderState : IOrderState
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Process(Order order)
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 处理新订单</span>
        order.State = <span style="color: #0000ff;">new</span><span style="color: #000000;"> ProcessingOrderState();
    }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ProcessingOrderState : IOrderState
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Process(Order order)
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 处理正在处理的订单</span>
        order.State = <span style="color: #0000ff;">new</span><span style="color: #000000;"> CompletedOrderState();
    }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> CompletedOrderState : IOrderState
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Process(Order order)
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 处理已完成的订单</span>
<span style="color: #000000;">    }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 将状态机封装到订单中</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Order
{
    </span><span style="color: #0000ff;">public</span> IOrderState State { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Order()
    {
        State </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> NewOrderState();
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> ProcessOrder()
    {
        State.Process(</span><span style="color: #0000ff;">this</span><span style="color: #000000;">);
    }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 在程序中使用状态模式</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
{
    </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
    {
        </span><span style="color: #0000ff;">var</span> order = <span style="color: #0000ff;">new</span><span style="color: #000000;"> Order();
        order.ProcessOrder(); </span><span style="color: #008000;">//</span><span style="color: #008000;"> 处理新订单</span>
        order.ProcessOrder(); <span style="color: #008000;">//</span><span style="color: #008000;"> 处理正在处理的订单</span>
        order.ProcessOrder(); <span style="color: #008000;">//</span><span style="color: #008000;"> 处理已完成的订单</span>
<span style="color: #000000;">    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">结构代码</span></div>
<p><strong><span style="font-size: 18px;">9，Strategy（策略，对象模式）<a name="c9"></a></span></strong></p>
<p><span style="color: #ff6600;"><strong>意图：</strong>定义一系列的算法，把它们一个个封装起来，并且使它们可相互替换。本模式使得算法可独立于使用它的客户而变化。</span></p>
<p><span style="color: #ff6600;"><strong>应用场景：</strong>封装算法</span></p>
<p><span style="color: #ff6600;"><strong>结构：</strong></span></p>
<p><img src="https://img2023.cnblogs.com/blog/741594/202304/741594-20230411214821569-863837742.png" alt="" width="609" height="289" loading="lazy" /></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('bb1fba39-97c4-4d5c-adcd-6e0dfc2b96c4')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_bb1fba39-97c4-4d5c-adcd-6e0dfc2b96c4" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_bb1fba39-97c4-4d5c-adcd-6e0dfc2b96c4" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_bb1fba39-97c4-4d5c-adcd-6e0dfc2b96c4" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> PaymentProcessor
{
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> IPaymentStrategy _paymentStrategy;

    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> PaymentProcessor(IPaymentStrategy paymentStrategy)
    {
        _paymentStrategy </span>=<span style="color: #000000;"> paymentStrategy;
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> ProcessPayment(<span style="color: #0000ff;">double</span><span style="color: #000000;"> amount)
    {
        _paymentStrategy.ProcessPayment(amount);
    }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IPaymentStrategy
{
    </span><span style="color: #0000ff;">void</span> ProcessPayment(<span style="color: #0000ff;">double</span><span style="color: #000000;"> amount);
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> CreditCardPaymentStrategy : IPaymentStrategy
{
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span> <span style="color: #0000ff;">string</span><span style="color: #000000;"> _cardNumber;
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span> <span style="color: #0000ff;">string</span><span style="color: #000000;"> _expiryDate;
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span> <span style="color: #0000ff;">string</span><span style="color: #000000;"> _cvv;

    </span><span style="color: #0000ff;">public</span> CreditCardPaymentStrategy(<span style="color: #0000ff;">string</span> cardNumber, <span style="color: #0000ff;">string</span> expiryDate, <span style="color: #0000ff;">string</span><span style="color: #000000;"> cvv)
    {
        _cardNumber </span>=<span style="color: #000000;"> cardNumber;
        _expiryDate </span>=<span style="color: #000000;"> expiryDate;
        _cvv </span>=<span style="color: #000000;"> cvv;
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> ProcessPayment(<span style="color: #0000ff;">double</span><span style="color: #000000;"> amount)
    {
        Console.WriteLine($</span><span style="color: #800000;">"</span><span style="color: #800000;">Processing credit card payment of {amount} with card number {_cardNumber}...</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 与处理信用卡付款的实际逻辑</span>
<span style="color: #000000;">    }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> PayPalPaymentStrategy : IPaymentStrategy
{
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span> <span style="color: #0000ff;">string</span><span style="color: #000000;"> _emailAddress;
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span> <span style="color: #0000ff;">string</span><span style="color: #000000;"> _password;

    </span><span style="color: #0000ff;">public</span> PayPalPaymentStrategy(<span style="color: #0000ff;">string</span> emailAddress, <span style="color: #0000ff;">string</span><span style="color: #000000;"> password)
    {
        _emailAddress </span>=<span style="color: #000000;"> emailAddress;
        _password </span>=<span style="color: #000000;"> password;
    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> ProcessPayment(<span style="color: #0000ff;">double</span><span style="color: #000000;"> amount)
    {
        Console.WriteLine($</span><span style="color: #800000;">"</span><span style="color: #800000;">Processing PayPal payment of {amount} with email address {_emailAddress}...</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 与处理PayPal付款的实际逻辑</span>
<span style="color: #000000;">    }
}


</span><span style="color: #0000ff;">var</span> creditCardPayment = <span style="color: #0000ff;">new</span> CreditCardPaymentStrategy(<span style="color: #800000;">"</span><span style="color: #800000;">1234567890123456</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">10/23</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">123</span><span style="color: #800000;">"</span><span style="color: #000000;">);
</span><span style="color: #0000ff;">var</span> paymentProcessor = <span style="color: #0000ff;">new</span><span style="color: #000000;"> PaymentProcessor(creditCardPayment);
paymentProcessor.ProcessPayment(</span><span style="color: #800080;">100.00</span><span style="color: #000000;">);

</span><span style="color: #0000ff;">var</span> payPalPayment = <span style="color: #0000ff;">new</span> PayPalPaymentStrategy(<span style="color: #800000;">"</span><span style="color: #800000;">johndoe@example.com</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">p@ssword</span><span style="color: #800000;">"</span><span style="color: #000000;">);
paymentProcessor </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> PaymentProcessor(payPalPayment);
paymentProcessor.ProcessPayment(</span><span style="color: #800080;">50.00</span>);</pre>
</div>
<span class="cnblogs_code_collapse">结构代码</span></div>
<p><strong><span style="font-size: 18px;">10，Template Method（模板方法，类模式）<a name="c10"></a></span></strong></p>
<p><span style="color: #ff6600;"><strong>意图：</strong>定义一个操作骨架，而将一些步骤延迟到子类中。TemplateMethod使得子类可以不改变一个算法的结构即可重定义该算法的某些特定步骤。</span></p>
<p><span style="color: #ff6600;"><strong>应用场景：</strong>定义一个操作骨架</span></p>
<p><span style="color: #ff6600;"><strong>结构：</strong></span></p>
<p>&nbsp;<img src="https://img2023.cnblogs.com/blog/741594/202304/741594-20230411220059340-925375584.png" alt="" width="334" height="370" loading="lazy" /></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('f197c38e-4f8c-4a5d-9ded-88504ee209f6')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_f197c38e-4f8c-4a5d-9ded-88504ee209f6" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_f197c38e-4f8c-4a5d-9ded-88504ee209f6" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_f197c38e-4f8c-4a5d-9ded-88504ee209f6" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> 模板方法模式
{
    </span><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            AbstractClass ab</span>=<span style="color: #0000ff;">new</span><span style="color: #000000;"> ConcreteClassA();
            ab.TemplateMethod();

            Console.ReadLine();
        }
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">模板类</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> AbstractClass
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> PrimitiveOperation1();
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> PrimitiveOperation2();

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> TemplateMethod()
        {
            PrimitiveOperation1();
            PrimitiveOperation2();
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">模板</span><span style="color: #800000;">"</span><span style="color: #000000;">); 
        }
    }
    </span><span style="color: #008000;">//</span><span style="color: #008000;">具体类A</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ConcreteClassA : AbstractClass
    {

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> PrimitiveOperation1()
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">具体类A-PrimitiveOperation1</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> PrimitiveOperation2()
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">具体类A-PrimitiveOperation2</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }
    }
    </span><span style="color: #008000;">//</span><span style="color: #008000;">具体类B</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ConcreteClassB : AbstractClass
    {

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> PrimitiveOperation1()
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">具体类B-PrimitiveOperation1</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> PrimitiveOperation2()
        {
            Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">具体类B-PrimitiveOperation2</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }
    }

}

模板方法模式代码</span></pre>
</div>
<span class="cnblogs_code_collapse">结构代码</span></div>
<p><strong><span style="font-size: 18px;">11，Visitor（访问者，对象模式）<a name="c11"></a></span></strong></p>
<p><span style="color: #ff6600;"><strong>意图：</strong>表示一个作用于某对象结构中的各个元素操作。它使得你可以在不改变各元素的类的前提下定义作用于这些元素的新操作。</span></p>
<p><span style="color: #ff6600;"><strong>应用场景：</strong>你可以定义一个访问者接口，用于在不同的控制器上执行操作，然后在应用程序中的不同地方使用该接口来执行特定操作</span></p>
<p><span style="color: #ff6600;"><strong>结构：</strong></span></p>
<p>&nbsp;<img src="https://img2023.cnblogs.com/blog/741594/202304/741594-20230411221127917-1015141712.png" alt="" width="739" height="380" loading="lazy" /></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('84cc4779-b123-4e7e-86d3-e71b8b83304c')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_84cc4779-b123-4e7e-86d3-e71b8b83304c" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_84cc4779-b123-4e7e-86d3-e71b8b83304c" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_84cc4779-b123-4e7e-86d3-e71b8b83304c" class="cnblogs_code_hide">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> 定义访问者接口</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IVisitor
{
    </span><span style="color: #0000ff;">void</span><span style="color: #000000;"> Visit(ControllerA controller);
    </span><span style="color: #0000ff;">void</span><span style="color: #000000;"> Visit(ControllerB controller);
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 定义被访问元素（控制器）</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> BaseController
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Accept(IVisitor visitor);
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ControllerA : BaseController
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Accept(IVisitor visitor)
    {
        visitor.Visit(</span><span style="color: #0000ff;">this</span><span style="color: #000000;">);
    }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ControllerB : BaseController
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Accept(IVisitor visitor)
    {
        visitor.Visit(</span><span style="color: #0000ff;">this</span><span style="color: #000000;">);
    }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 实现访问者接口</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Visitor : IVisitor
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Visit(ControllerA controller)
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 执行 ControllerA 特定操作</span>
<span style="color: #000000;">    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Visit(ControllerB controller)
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 执行 ControllerB 特定操作</span>
<span style="color: #000000;">    }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 使用访问者模式</span>
<span style="color: #0000ff;">var</span> controllerA = <span style="color: #0000ff;">new</span><span style="color: #000000;"> ControllerA();
</span><span style="color: #0000ff;">var</span> controllerB = <span style="color: #0000ff;">new</span><span style="color: #000000;"> ControllerB();

</span><span style="color: #0000ff;">var</span> visitor = <span style="color: #0000ff;">new</span><span style="color: #000000;"> Visitor();
controllerA.Accept(visitor);
controllerB.Accept(visitor);</span></pre>
</div>
<span class="cnblogs_code_collapse">结构代码</span></div>
<p>&nbsp;</p>