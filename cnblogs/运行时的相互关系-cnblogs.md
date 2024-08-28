<p>&nbsp;</p>
<div class="cnblogs_code">
<pre>    <span style="color: #0000ff;">internal</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Employee
    {
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Int32 GetYearEmployee()
        {
            </span><span style="color: #0000ff;">return</span> <span style="color: #800080;">5</span><span style="color: #000000;">;
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">virtual</span><span style="color: #000000;"> String GetProgressReport()
        {
            </span><span style="color: #0000ff;">return</span> <span style="color: #800000;">""</span><span style="color: #000000;">;
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> Employee Lookup(String name)
        {
            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> Manager();
        }

    }

    </span><span style="color: #0000ff;">internal</span> <span style="color: #0000ff;">sealed</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Manager : Employee
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">string</span><span style="color: #000000;"> GetProgressReport()
        {
            </span><span style="color: #0000ff;">return</span> <span style="color: #800000;">""</span><span style="color: #000000;">;
        }
    }</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p><img src="http://images2015.cnblogs.com/blog/741594/201702/741594-20170220213042335-1003144365.jpg" alt="" /><br />1，Windows进程已启动，CLR已加载到其中，托管堆已初始化，创建了一个线程（分配1MB栈空间），线程已经执行了一些代码，马上要调用M3方法了</p>
<p> <img src="http://images2015.cnblogs.com/blog/741594/201702/741594-20170220213053179-1280715037.jpg" alt="" /><br />1，JIT编译器将M3的IL代码转换成本机CPU指令时，会确认M3内部引用的所有类型（Employee、Int32、Manager、String）是否都已加载<br />2，利用程序集的元数据，CLR提取与这些类有关的信息，创建一些数据结构来表示类型本身<br /> <img src="http://images2015.cnblogs.com/blog/741594/201702/741594-20170220213059632-1323061032.jpg" alt="" /><br />1，CLR确认该方法所需的所有类型对象都已经创建，M3的代码已经编译之后，就允许线程执行M3的本机代码，M3的&ldquo;序幕&rdquo;代码必须为局部变量分配内存<br /> <img src="http://images2015.cnblogs.com/blog/741594/201702/741594-20170220213106320-1145507971.jpg" alt="" /><br />1，M3执行代码构造一个Manager对象，这造成在托管堆创建Manager类型的一个实例。Manager对象也有类型对象指针和同步块索引。<span style="color: #ff0000;">实例字段</span>包括当前类型（Manager）和所有基类定义的所有实例数据字段</p>
<p><br /> <img src="http://images2015.cnblogs.com/blog/741594/201702/741594-20170220213113570-1008341275.jpg" alt="" /><br />1，M3下一行调用Employee的静态方法Lookup，该方法在堆上构造了一个新的Manager对象<br />2，CLR会定位Employee类型对象，JIT编译器在类型对象的方法表中查找对应的记录项，对方法进行JIT编译（没被编译过），在调用JIT编译好的代码<br />3，该地址保存到局部变量e中</p>
<p><br /> <img src="http://images2015.cnblogs.com/blog/741594/201702/741594-20170220213124445-1023965211.jpg" alt="" /><br />1，M3的下一行代码调用Employee的非虚方法GetYearsEmployed。如果Employee类型没有定义该方法，则JIT编译器会回溯类层次结构（一直回溯到Object），并在沿途的每个类型中查找该方法<br />2，JIT编译器在类型对象的方法表中找到被调用方法的记录项，进行编译（没被编译过），在调用JIT编译好的代码<br />3，将返回的值赋值到year变量中<br /> <img src="http://images2015.cnblogs.com/blog/741594/201702/741594-20170220213135382-1211226955.jpg" alt="" /><br />1，M3的下一行代码调用Employee的虚实例方法GetProgressReport，调用虚实例方法时，JIT编译器要在方法中生成一些额外的代码，方法每次调用都会执行这些代码<br />2，额外的代码检查出e变量当前引用的是代表&ldquo;Joe&rdquo;的Manager对象，然后检查对象内部的&ldquo;类型对象指针&rdquo;成员，该成员指向对象的实际类型（Manager类型对象）<br />3，代码在类型对象的方法表中找到了方法的记录项，进行JIT编译（没被编译过），再调用JIT编译好的方法</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;">类型对象指针</span></p>
<p><br /> <img src="http://images2015.cnblogs.com/blog/741594/201702/741594-20170220213143601-1190701712.jpg" alt="" /><br />1，Employee和Manager类型对象都包含&ldquo;类型对象指针&rdquo;成员。CLR创建类型对象时必须初始化这些成员，他们的&ldquo;类型对象指针&rdquo;成员会被初始化成System.Type类型对象的引用，System.Type类型对象的&ldquo;类型对象指针&rdquo;指向它本身<br />2，System.Object的GetType方法返回存储在指定对象的&ldquo;类型对象指针&rdquo;成员中的地址。也就是说，GetType方法返回对象的真实类型</p>