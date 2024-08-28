<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">&nbsp;一、序列化与反序列化</span></strong></span></p>
<p>序列化是将对象图转换成字节流的过程，反序列化是将字节流转换回对象图的过程</p>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            List</span>&lt;<span style="color: #0000ff;">string</span>&gt; objectGraph = <span style="color: #0000ff;">new</span> List&lt;<span style="color: #0000ff;">string</span>&gt;() {<span style="color: #800000;">"</span><span style="color: #800000;">关羽</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">吕蒙</span><span style="color: #800000;">"</span><span style="color: #000000;">};
            Stream stream </span>=<span style="color: #000000;"> SerialzeToMemory(objectGraph);

            stream.Position </span>= <span style="color: #800080;">0</span>;<span style="color: #008000;">//</span><span style="color: #008000;">反序列化前，定位到内存流的起始位置</span>
            objectGraph = (List&lt;<span style="color: #0000ff;">string</span>&gt;<span style="color: #000000;">)DeserialzeFromMemory(stream);
            </span><span style="color: #0000ff;">foreach</span> (<span style="color: #0000ff;">var</span> obj <span style="color: #0000ff;">in</span><span style="color: #000000;"> objectGraph)
            {
                Console.WriteLine(obj);
            }
            Console.ReadKey();
        }



        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> MemoryStream SerialzeToMemory(<span style="color: #0000ff;">object</span><span style="color: #000000;"> objectGraph)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">构造流来容纳序列化的对象</span>
            MemoryStream stream = <span style="color: #0000ff;">new</span><span style="color: #000000;"> MemoryStream();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">构造序列化格式化器来执行所有真正的工作</span>
            BinaryFormatter formatter = <span style="color: #0000ff;">new</span><span style="color: #000000;"> BinaryFormatter();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">告诉格式化器将对象序列化到流中</span>
<span style="color: #000000;">            formatter.Serialize(stream, objectGraph);

            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> stream;
        }

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">object</span><span style="color: #000000;"> DeserialzeFromMemory(Stream stream)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">构造序列化格式化器来做所有真正的工作</span>
            BinaryFormatter formatter = <span style="color: #0000ff;">new</span><span style="color: #000000;"> BinaryFormatter();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">告诉格式化器从流中反序列化对象</span>
            <span style="color: #0000ff;">return</span><span style="color: #000000;"> formatter.Deserialize(stream);
        }

    }</span></pre>
</div>
<p>&nbsp;</p>
<p>注意事项：</p>
<p>①保证代码为序列化和反序列化使用相同的格式化器<br />②可将多个对象图序列化到一个流中</p>
<div class="cnblogs_code">
<pre>        <span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> List&lt;Customer&gt; s_customers = <span style="color: #0000ff;">new</span> List&lt;Customer&gt;<span style="color: #000000;">();
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> List&lt;Order&gt; s_pendingOrders = <span style="color: #0000ff;">new</span> List&lt;Order&gt;<span style="color: #000000;">();
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> List&lt;Order&gt; s_processedOrders = <span style="color: #0000ff;">new</span> List&lt;Order&gt;<span style="color: #000000;">();

        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">将多个对象图序列化一个流中</span>
            MemoryStream stream = <span style="color: #0000ff;">new</span><span style="color: #000000;"> MemoryStream();
            BinaryFormatter formatter </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> BinaryFormatter();
            formatter.Serialize(stream, s_customers);
            formatter.Serialize(stream, s_pendingOrders);
            formatter.Serialize(stream, s_processedOrders);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">反序列化应用程序的完整状态（和序列化时的顺序一样）</span>
            s_customers = (List&lt;Customer&gt;<span style="color: #000000;">) formatter.Deserialize(stream);
            s_pendingOrders </span>= (List&lt;Order&gt;<span style="color: #000000;">) formatter.Deserialize(stream);
            s_processedOrders </span>= (List&lt;Order&gt;<span style="color: #000000;">) formatter.Deserialize(stream);

            Console.ReadKey();
        }</span></pre>
</div>
<p>③序列化对象时，类型的全名和类型定义程序集的全名会被写入流。BinaryFormatter默认输出程序集的完整标识，其中包含程序集的文件名（无扩展名）、版本号、语言文化以及公钥信息。反序列化对象时，格式化器首先获取程序集标识信息，并通过调用System.Reflection.Assembly的Load方法确保程序集已加载到正在执行的AppDoamin中。程序集加载好之后，格式化器在程序集中查找与要反序列化的对象匹配类型。找不到匹配类型则抛出异常，不再对更多的对象进行序列化，找到匹配的类型，就创建类型的实例，并用流中包含的值对其字段进行初始化。如果类型中的字段与流中读取的字段名不完全匹配，就抛出SerializetionException异常，不再对更多的对象进行序列化</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">&nbsp;二、使类型可序列化</span></strong></span></p>
<p>1，必须在需要序列化的类型上加上System.SerializebleAttibute特性<br />2，SerializebleAttibute这个定制特性只能应用与引用类型（class）、值类型（struct）、枚举类型（enum）和委托类型（delegate）。注意类型和委托总是可序列化的，所以不必显示应用SerializebleAttibute特性。<br />3，SerializebleAttibute特性不会被派生类继承<br />5，System.Object应用了SerializebleAttibute特性<br />6，序列化会读取对象的所有字段，不管这些字段声明为public、protected、internal还是private</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">三、控制序列化和反序列化</span></strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">[Serializable]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">sealed</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Circle
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">double</span> m_radius=<span style="color: #800080;">10</span>;<span style="color: #008000;">//</span><span style="color: #008000;">半径</span>
<span style="color: #000000;">
        [NonSerialized]</span><span style="color: #008000;">//</span><span style="color: #008000;">当前字段不会被序列化（反序列化时，此值为0）</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">double</span> m_area=<span style="color: #800080;">10</span>;<span style="color: #008000;">//</span><span style="color: #008000;">面积</span>
<span style="color: #000000;">


        [OnDeserializing]
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> OnDeserializing(StreamingContext context)
        {
            m_area </span>= <span style="color: #800080;">20</span>;<span style="color: #008000;">//</span><span style="color: #008000;">举例：在这个类型新版本中</span>
<span style="color: #000000;">        }

        [OnDeserialized]
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> OnDeserialized(StreamingContext context)
        {
            m_area </span>= <span style="color: #800080;">10</span>;<span style="color: #008000;">//</span><span style="color: #008000;">举例：根据字段值初始化瞬时状态</span>
<span style="color: #000000;">        }

        [OnSerializing]
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> OnSerializing(StreamingContext context)
        {
            m_area </span>= <span style="color: #800080;">10</span>;<span style="color: #008000;">//</span><span style="color: #008000;">举例：在序列化前，修改任何需要修改的状态</span>
<span style="color: #000000;">        }
        [OnSerialized]
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> OnSerialized(StreamingContext context)
        {
            m_area </span>= <span style="color: #800080;">10</span>;<span style="color: #008000;">//</span><span style="color: #008000;">举例：在序列化后，恢复任何需要恢复的状态</span>
<span style="color: #000000;">        }

    }</span></pre>
</div>
<p>①定义的方法必须获取一个StreamingContext参数，并返回void。方法名称可随意命名<br />②调用顺序：序列化一组对象时先调用标记了OnSerializing的方法，然后调用标记了OnSerialized特性的方法。反序列化时先调用标记了OnDeserializing的方法，然后调用标记了OnDeserialized的方法</p>
<p>如果序列化类型的实例，在类型中添加新字段，然后视图反序列化不包含新字段的对象，格式化器会抛出SerializationExcption异常。可在新增字段中加上OptionalFieldAttribute特性</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">四、格式化器如何序列化类型实例</span></strong></span></p>
<p>FCL在System.Runtime.Serialization命名空间提供了一个FormatterServices类型，该类型只包含静态方法，而且该类型不能实例化</p>
<p><strong><span style="font-size: 14pt;">1，格式化器如何自动序列化类型引用了SerializableAttribute特性的对象</span></strong></p>
<p>①格式化器调用FormatterServices的GetSerializableMembers方法。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> MemberInfo[] GetSerializableMembers(Type type, StreamingContext context);</pre>
</div>
<p>这个方法利用反射获取类型的public和private实例字段（标记了NonSerializedAttribute特性的字段除外）。方法返回由MemberInfo对象构成的数组，其中每个元素都对应一个可序列化的实例字段</p>
<p>②对象被序列化，System.Reflection.MemberInfo对象数组传给FormatterServices的静态方法GetObjectData</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">object</span>[] GetObjectData(<span style="color: #0000ff;">object</span> obj, MemberInfo[] members);</pre>
</div>
<p>这个方法返回一个Object数组，其中每个元素都标识了被序列化的那个对象的一个字段的值。object数组中的元素0是MemberInfo数组中的元素0所标识的那个成员的值</p>
<p>③格式化器将程序集标识和类型的完整名称写入流中</p>
<p>④格式化器然后遍历两个数组中的元素，将每个成员的名称和值写入流中</p>
<p>&nbsp;</p>
<p><strong><span style="font-size: 14pt;">2，格式化器如何自动反序列化类型应用了SerializableAttribute特性的对象</span></strong><br />①格式化器流中读取程序集标识和完整类名称。如果程序集当没有加载到AppDomain中，就加载它。如果程序集不能加载，就抛出一个SerializetionException异常，对象不能反序列化。如果程序集已加载，格式化器将程序集标识信息和类型全名传给FormatterServices的静态方法GetTypeFromAssembly</p>
<div class="cnblogs_code">
<pre> <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> Type GetTypeFromAssembly(Assembly assem, <span style="color: #0000ff;">string</span> name);</pre>
</div>
<p>这个方法返回一个System.Type对象，它代表要反序列化的那个对象的类型</p>
<p>②格式化器调用FormatterServices的静态方法GetUninitializedObject</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">object</span> GetUninitializedObject(System.Type type)</pre>
</div>
<p>这个方法为一个新对象分配内存，但不为对象调用构造器。然而，对象的所有字节都被初始化成null或0</p>
<p>③格式化器现在构造并初始化一个MemberInfo数组，具体做法和前面一样，都是调用FormatterServices的GetSerializableMembers方法。这个方法返回序列化好、现在需要反序列化的一组字段</p>
<p>④格式化器根据流中包含的数据创建并初始化一个Object数组</p>
<p>⑤将新分配对象、MemberInfo数组以及并行Object数组（其中包含字段值）的引用传给FormatterServices的静态方法PopulateObjectMembers</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">object</span> PopulateObjectMembers(<span style="color: #0000ff;">object</span> obj, System.Reflection.MemberInfo[] members, <span style="color: #0000ff;">object</span>[] data)</pre>
</div>
<p>这个方法遍历数组，将每个字段初始化成对应的值。</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">五、控制序列化/反序列化的数据</span></strong></span></p>
<p><strong><span style="font-size: 14pt;">1，ISerializable</span></strong></p>
<p>格式化器内部使用的是反射，反射的速度比较慢。为了对序列化和反序列化完全控制，需要实现System.Runtime.Serialization.ISerializable接口。派生此接口的类型最好是派生类。</p>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> ISerializable
    {
        </span><span style="color: #0000ff;">void</span><span style="color: #000000;"> GetObjectData(SerializationInfo info,StreamingContext context){}
    }</span></pre>
</div>
<p>建议向GetObjectData方法和特殊构造器应用以下特性</p>
<p>[SecurityPermission(SecurityAction.Demand, SerializationFormatter = true)]</p>
<p><strong><span style="font-size: 14pt;">2，SerializationInfo（包含了要为对象序列化的值得集合）</span></strong></p>
<p>构造此对象需要传递两个参数Type和System.Runtime.Serialization.IFormatterConverter</p>
<p>SerializationInfo对象的AddValue方法添加要序列化的信息&nbsp;</p>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            CustomerSerializeable c </span>= <span style="color: #0000ff;">new</span> CustomerSerializeable() {Name = <span style="color: #800000;">"</span><span style="color: #800000;">张三</span><span style="color: #800000;">"</span>, Age =<span style="color: #800080;">12</span><span style="color: #000000;">};

            MemoryStream ms </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> MemoryStream();
            BinaryFormatter b </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> BinaryFormatter();
            b.Serialize(ms, c);
            ms.Position </span>= <span style="color: #800080;">0</span><span style="color: #000000;">;
            </span><span style="color: #0000ff;">var</span> aa=<span style="color: #000000;">(CustomerSerializeable)b.Deserialize(ms);
            Console.WriteLine(aa.Name);
            Console.WriteLine(aa.Age);</span><span style="color: #008000;">//</span><span style="color: #008000;">不会被序列化</span>
<span style="color: #000000;">
            Console.ReadKey();
        }
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">设置此类型最好是密封的</span>
<span style="color: #000000;">    [Serializable]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">sealed</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> CustomerSerializeable : ISerializable,IDeserializationCallback
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Name { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span> Age { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

        </span><span style="color: #008000;">//</span><span style="color: #008000;">只用于反序列化</span>
        <span style="color: #0000ff;">private</span><span style="color: #000000;"> SerializationInfo m_siInfo;

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> CustomerSerializeable(){}

        </span><span style="color: #008000;">//</span><span style="color: #008000;">用于控制反序列化的特殊构造器(不加此构造函数反序列化将抛异常)</span>
        [SecurityPermission(SecurityAction.Demand, SerializationFormatter = <span style="color: #0000ff;">true</span><span style="color: #000000;">)]
        private </span><span style="color: #000000;">CustomerSerializeable(SerializationInfo info, StreamingContext sc)
        {
            m_siInfo </span>=<span style="color: #000000;"> info;
        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;">用于控制序列化的方法</span>
<span style="color: #000000;">        [SecurityCritical]
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> GetObjectData(SerializationInfo info, StreamingContext context)
        {
            info.AddValue(</span><span style="color: #800000;">"</span><span style="color: #800000;">Name</span><span style="color: #800000;">"</span>, Name, <span style="color: #0000ff;">typeof</span> (<span style="color: #0000ff;">string</span><span style="color: #000000;">));
        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;">所有key/value对象都反序列化好之后调用的方法</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> OnDeserialization(<span style="color: #0000ff;">object</span><span style="color: #000000;"> sender)
        {
            </span><span style="color: #0000ff;">if</span>(m_siInfo==<span style="color: #0000ff;">null</span>)<span style="color: #0000ff;">return</span>;<span style="color: #008000;">//</span><span style="color: #008000;">从不设置，直接返回</span>
            Name = m_siInfo.GetString(<span style="color: #800000;">"</span><span style="color: #800000;">Name</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }
    }</span></pre>
</div>
<p>如果一个字段的类型实现了ISerializable接口，就不要在字段上调用GetObjectData。相反，调用AddValue来添加字段</p>
<p><strong><span style="font-size: 14pt;">&nbsp;3，IFormatterConverter</span></strong></p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201708/741594-20170802200622897-874409986.png" alt="" /></p>
<p>FormatterConverter类型调用System.Convert类的各种静态方法在不同的核心类型之间对值进行转换</p>
<p><span style="font-size: 14pt;"><strong>4，要实现&nbsp;ISerializable但基类型没有实现怎么办？</strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">    [Serializable]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Base
    {
        </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">string</span> m_name = <span style="color: #800000;">"</span><span style="color: #800000;">张三</span><span style="color: #800000;">"</span><span style="color: #000000;">;
    }

    [Serializable]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Derived : Base,ISerializable
    {
        </span><span style="color: #0000ff;">private</span> DateTime m_date=<span style="color: #000000;">DateTime.Now;

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Derived(){}

        </span><span style="color: #008000;">//</span><span style="color: #008000;">用于控制反序列化的特殊构造器(不加此构造函数反序列化将抛异常)</span>
        [SecurityPermission(SecurityAction.Demand, SerializationFormatter = <span style="color: #0000ff;">true</span><span style="color: #000000;">)]
        </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> Derived(SerializationInfo info, StreamingContext context)
        {
            m_date </span>= info.GetDateTime(<span style="color: #800000;">"</span><span style="color: #800000;">Date</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            Type baseType </span>=<span style="color: #000000;"> GetType().BaseType;
            MemberInfo[] mis </span>= FormatterServices.GetSerializableMembers(baseType, context);<span style="color: #008000;">//</span><span style="color: #008000;">获取类型所有可序列化的成员
            </span><span style="color: #008000;">//</span><span style="color: #008000;">从info对象反序列化基类的字段</span>
            <span style="color: #0000ff;">foreach</span> (<span style="color: #0000ff;">var</span> memberInfo <span style="color: #0000ff;">in</span><span style="color: #000000;"> mis)
            {
                FieldInfo f </span>=<span style="color: #000000;"> (FieldInfo) memberInfo;
                f.SetValue(</span><span style="color: #0000ff;">this</span>, info.GetValue(baseType.FullName + <span style="color: #800000;">"</span><span style="color: #800000;">+</span><span style="color: #800000;">"</span> +<span style="color: #000000;"> f.Name, f.FieldType));
            }
        }
        [SecurityPermission(SecurityAction.Demand, SerializationFormatter </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">)]
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> GetObjectData(SerializationInfo info, StreamingContext context)
        {
            info.AddValue(</span><span style="color: #800000;">"</span><span style="color: #800000;">Date</span><span style="color: #800000;">"</span><span style="color: #000000;">, m_date);
            Type baseType </span>=<span style="color: #000000;"> GetType().BaseType;
            MemberInfo[] mis </span>= FormatterServices.GetSerializableMembers(baseType, context);<span style="color: #008000;">//</span><span style="color: #008000;">获取类型所有可序列化的成员
            </span><span style="color: #008000;">//</span><span style="color: #008000;">将基类字段序列化到info对象中</span>
            <span style="color: #0000ff;">foreach</span> (<span style="color: #0000ff;">var</span> memberInfo <span style="color: #0000ff;">in</span><span style="color: #000000;"> mis)
            {
                FieldInfo f </span>=<span style="color: #000000;"> (FieldInfo)memberInfo;
                info.AddValue(baseType.FullName </span>+ <span style="color: #800000;">"</span><span style="color: #800000;">+</span><span style="color: #800000;">"</span> + f.Name,f.GetValue(<span style="color: #0000ff;">this</span><span style="color: #000000;">));
            }
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">string</span><span style="color: #000000;"> ToString()
        {
            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">string</span>.Format(<span style="color: #800000;">"</span><span style="color: #800000;">Name={0},Date={1}</span><span style="color: #800000;">"</span><span style="color: #000000;">, m_name, m_date);
        }
    }</span></pre>
</div>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {

            Derived c </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> Derived();

            MemoryStream ms </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> MemoryStream();
            BinaryFormatter b </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> BinaryFormatter();
            b.Serialize(ms, c);
            ms.Position </span>= <span style="color: #800080;">0</span><span style="color: #000000;">;
            </span><span style="color: #0000ff;">var</span> aa=<span style="color: #000000;">(Derived)b.Deserialize(ms);
            Console.WriteLine(aa);

            Console.ReadKey();
        }
    }</span></pre>
</div>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">六、序列化和反序列化单实例</span></strong></p>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {
            Singleton[] ss </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> Singleton[] {Singleton.GetSingleton(), Singleton.GetSingleton()};
            Console.WriteLine(ss[</span><span style="color: #800080;">0</span>]==ss[<span style="color: #800080;">1</span>]);<span style="color: #008000;">//</span><span style="color: #008000;">True</span>

            <span style="color: #0000ff;">using</span> (MemoryStream ms = <span style="color: #0000ff;">new</span><span style="color: #000000;"> MemoryStream())
            {
                BinaryFormatter formatter </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> BinaryFormatter();
                formatter.Serialize(ms, ss);
                ms.Position </span>= <span style="color: #800080;">0</span><span style="color: #000000;">;
                </span><span style="color: #0000ff;">var</span> ss2 =<span style="color: #000000;"> (Singleton[]) formatter.Deserialize(ms);
                Console.WriteLine(ss2[</span><span style="color: #800080;">0</span>] == ss2[<span style="color: #800080;">1</span>]);<span style="color: #008000;">//</span><span style="color: #008000;">True</span>
                Console.WriteLine(ss[<span style="color: #800080;">0</span>] == ss2[<span style="color: #800080;">0</span>]);<span style="color: #008000;">//</span><span style="color: #008000;">True</span>
<span style="color: #000000;">            }
            Console.ReadKey();
        }
    }

    [Serializable]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">sealed</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Singleton : ISerializable
    {

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> Singleton s_theOneObject = <span style="color: #0000ff;">new</span><span style="color: #000000;"> Singleton();
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Name = <span style="color: #800000;">"</span><span style="color: #800000;">张三</span><span style="color: #800000;">"</span><span style="color: #000000;">;
        </span><span style="color: #0000ff;">public</span>  DateTime Date=<span style="color: #000000;">DateTime.Now;

        </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> Singleton(){}

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> Singleton GetSingleton(){<span style="color: #0000ff;">return</span><span style="color: #000000;"> s_theOneObject;}


        [SecurityPermission(SecurityAction.Demand, SerializationFormatter </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">)]
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> GetObjectData(SerializationInfo info, StreamingContext context)
        {
            info.SetType(</span><span style="color: #0000ff;">typeof</span><span style="color: #000000;">(SingletonSerializationHepler));
        }

        [Serializable]
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">sealed</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SingletonSerializationHepler : IObjectReference
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">这个方法在对象（他没有字段）反序列化之后调用</span>
            <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">object</span><span style="color: #000000;"> GetRealObject(StreamingContext context)
            {
                </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> GetSingleton();
            }
        }
    }</span></pre>
</div>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;">&nbsp;七、序列化代理</span></strong></p>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">class</span><span style="color: #000000;"> Program
    {
        </span><span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> Main(<span style="color: #0000ff;">string</span><span style="color: #000000;">[] args)
        {

            </span><span style="color: #0000ff;">using</span> (<span style="color: #0000ff;">var</span> ms = <span style="color: #0000ff;">new</span><span style="color: #000000;"> MemoryStream())
            {
                IFormatter formatter </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> BinaryFormatter();

                </span><span style="color: #008000;">//</span><span style="color: #008000;">构造一个SurrogateSelector（代理选择器）对象</span>
                SurrogateSelector ss = <span style="color: #0000ff;">new</span><span style="color: #000000;"> SurrogateSelector();
                </span><span style="color: #008000;">//</span><span style="color: #008000;">告诉代理选择器为Datetime对象使用我们的代理</span>
                ss.AddSurrogate(<span style="color: #0000ff;">typeof</span> (DateTime), formatter.Context, <span style="color: #0000ff;">new</span><span style="color: #000000;"> LocalTimeSerializationSurrogate());
                </span><span style="color: #008000;">//</span><span style="color: #008000;">注意：AddSurrogate可多次调用来登记多个代理

                </span><span style="color: #008000;">//</span><span style="color: #008000;">告诉格式化选择器使用代理对象</span>
                formatter.SurrogateSelector =<span style="color: #000000;"> ss;

                </span><span style="color: #008000;">//</span><span style="color: #008000;">创建一个DateTime来代表机器上的本地时间，并序列化它</span>
                DateTime localDateTime =<span style="color: #000000;"> DateTime.Now;
                formatter.Serialize(ms, localDateTime);

                </span><span style="color: #008000;">//</span><span style="color: #008000;">反序列化</span>
                ms.Position = <span style="color: #800080;">0</span><span style="color: #000000;">;
                </span><span style="color: #0000ff;">var</span> dt =<span style="color: #000000;"> (DateTime) formatter.Deserialize(ms);

                Console.WriteLine(dt);
            }

            Console.ReadKey();
        }
    }


    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">sealed</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> LocalTimeSerializationSurrogate : ISerializationSurrogate
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> GetObjectData(<span style="color: #0000ff;">object</span><span style="color: #000000;"> obj, SerializationInfo info, StreamingContext context)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">将DateTime从本地时间转换成UTC</span>
            info.AddValue(<span style="color: #800000;">"</span><span style="color: #800000;">Date</span><span style="color: #800000;">"</span><span style="color: #000000;">, ((DateTime) obj).ToShortDateString());
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">object</span> SetObjectData(<span style="color: #0000ff;">object</span><span style="color: #000000;"> obj, SerializationInfo info, StreamingContext context, ISurrogateSelector selector)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">将DateTime从UTC转换成本地时间</span>
            <span style="color: #0000ff;">return</span> Convert.ToDateTime(info.GetString(<span style="color: #800000;">"</span><span style="color: #800000;">Date</span><span style="color: #800000;">"</span><span style="color: #000000;">));
        }
    }</span></pre>
</div>
<p>&nbsp;</p>