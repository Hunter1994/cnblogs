<p>您可以订阅一个接口，然后发布该接口的实现。</p>
<p>我们来看一个例子。 我有一个接口IAnimal和两个实现猫和狗：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IAnimal
{
    </span><span style="color: #0000ff;">string</span> Name { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Cat : IAnimal
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Name { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Meow { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Dog : IAnimal
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Name { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Bark { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}</span></pre>
</div>
<p>我可以订阅IAnimal并获得猫和狗类：</p>
<div class="cnblogs_code">
<pre>bus.Subscribe&lt;IAnimal&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">polymorphic_test</span><span style="color: #800000;">"</span>, @interface =&gt;<span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">var</span> cat = @interface <span style="color: #0000ff;">as</span><span style="color: #000000;"> Cat;
        </span><span style="color: #0000ff;">var</span> dog = @interface <span style="color: #0000ff;">as</span><span style="color: #000000;"> Dog;

        </span><span style="color: #0000ff;">if</span> (cat != <span style="color: #0000ff;">null</span><span style="color: #000000;">)
        {
            Console.Out.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">Name = {0}</span><span style="color: #800000;">"</span><span style="color: #000000;">, cat.Name);
            Console.Out.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">Meow = {0}</span><span style="color: #800000;">"</span><span style="color: #000000;">, cat.Meow);
        }
        </span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span> (dog != <span style="color: #0000ff;">null</span><span style="color: #000000;">)
        {
            Console.Out.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">Name = {0}</span><span style="color: #800000;">"</span><span style="color: #000000;">, dog.Name);
            Console.Out.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">Bark = {0}</span><span style="color: #800000;">"</span><span style="color: #000000;">, dog.Bark);
        }
        </span><span style="color: #0000ff;">else</span><span style="color: #000000;">
        {
            Console.Out.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">message was not a dog or a cat</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }
    });</span></pre>
</div>
<p>让我们发布一只猫和一只狗：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> cat = <span style="color: #0000ff;">new</span><span style="color: #000000;"> Cat
{
    Name </span>= <span style="color: #800000;">"</span><span style="color: #800000;">Gobbolino</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    Meow </span>= <span style="color: #800000;">"</span><span style="color: #800000;">Purr</span><span style="color: #800000;">"</span><span style="color: #000000;">
};

</span><span style="color: #0000ff;">var</span> dog = <span style="color: #0000ff;">new</span><span style="color: #000000;"> Dog
{
    Name </span>= <span style="color: #800000;">"</span><span style="color: #800000;">Rover</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    Bark </span>= <span style="color: #800000;">"</span><span style="color: #800000;">Woof</span><span style="color: #800000;">"</span><span style="color: #000000;">
};

bus.Publish</span>&lt;IAnimal&gt;<span style="color: #000000;">(cat);
bus.Publish</span>&lt;IAnimal&gt;(dog);</pre>
</div>
<p>请注意，我必须明确指定我发布IAnimal。 EasyNetQ使用&ldquo;发布&rdquo;和&ldquo;订阅&rdquo;方法中指定的泛型类型将发布路由到订阅。</p>