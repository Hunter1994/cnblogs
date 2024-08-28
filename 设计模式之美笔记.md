<p style="font-size: 18pt; background-color: #169fe6;"><strong><span style="color: #ffffff;">一、好代码的评判标准</span></strong></p>
<p>1，可维护性：在不破坏原有代码设计，不引入新的bug情况下，能够快速的修改或者添加代码。</p>
<p>2，可读性：代码是否符合编码规范，命名是否答意，注释是否详尽，函数是否长短合适，模块划分是否清晰，是否符合高内聚低耦合等等</p>
<p>3，可扩展性：在不修改或者少量修改原有代码的情况下，通过扩展点的方式添加新的功能</p>
<p>4，可复用性：尽量减少重复代码的编写，复用已有的代码</p>
<p>面向对象中的继承，多态能让我们写出可复用的代码;变成规范能让我们写出可复用的代码;设计模式中的单一职责,DIY,基于接口而非实现,里氏替换原则等可以让我们写出可复用,灵活,可读性好,易扩展,易维护的代码;设计模式可以让我们写出易扩展的代码;持续重构可以时刻保持代码的可维护性等等</p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: #169fe6;"><strong><span style="color: #ffffff;">二、设计原则与思想：面向对象</span></strong></p>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">1，什么是面向对象：它以类和对象作为组织代码的基本单元，并将封装、继承、抽象、多态作为代码设计和实现的基石</span></strong></span></p>
<p>①封装：信息隐藏或者数据访问保护</p>
<p>②继承：主要解决代码复用问题</p>
<p>③抽象：一方面提高代码的可扩展性、维护性；另一方面也是处理复杂系统的有效手段，能有效地过滤掉不必要的关注信息</p>
<p>④多态：多态可以提高代码的扩展性和复用性，是很多设计模式、设计原则、编程技巧的代码实现基础</p>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">2，面向对象与面向过程</span></strong></span></p>
<p>①什么是面向过程编程与面向对象编程</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('1ad4784f-f050-4b25-9861-658f88c45c5a')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_1ad4784f-f050-4b25-9861-658f88c45c5a" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_1ad4784f-f050-4b25-9861-658f88c45c5a" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_1ad4784f-f050-4b25-9861-658f88c45c5a" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">struct</span><span style="color: #000000;"> User {
  </span><span style="color: #0000ff;">char</span> name[<span style="color: #800080;">64</span><span style="color: #000000;">];
  </span><span style="color: #0000ff;">int</span><span style="color: #000000;"> age;
  </span><span style="color: #0000ff;">char</span> gender[<span style="color: #800080;">16</span><span style="color: #000000;">];
};

</span><span style="color: #0000ff;">struct</span> User parse_to_user(<span style="color: #0000ff;">char</span>*<span style="color: #000000;"> text) {
  </span><span style="color: #008000;">//</span><span style="color: #008000;"> 将text(&ldquo;小王&amp;28&amp;男&rdquo;)解析成结构体struct User</span>
<span style="color: #000000;">}

</span><span style="color: #0000ff;">char</span>* format_to_text(<span style="color: #0000ff;">struct</span><span style="color: #000000;"> User user) {
  </span><span style="color: #008000;">//</span><span style="color: #008000;"> 将结构体struct User格式化成文本（"小王\t28\t男"）</span>
<span style="color: #000000;">}

</span><span style="color: #0000ff;">void</span> sort_users_by_age(<span style="color: #0000ff;">struct</span><span style="color: #000000;"> User users[]) {
  </span><span style="color: #008000;">//</span><span style="color: #008000;"> 按照年龄从小到大排序users</span>
<span style="color: #000000;">}

</span><span style="color: #0000ff;">void</span> format_user_file(<span style="color: #0000ff;">char</span>* origin_file_path, <span style="color: #0000ff;">char</span>*<span style="color: #000000;"> new_file_path) {
  </span><span style="color: #008000;">//</span><span style="color: #008000;"> open files...</span>
  <span style="color: #0000ff;">struct</span> User users[<span style="color: #800080;">1024</span>]; <span style="color: #008000;">//</span><span style="color: #008000;"> 假设最大1024个用户</span>
  <span style="color: #0000ff;">int</span> count = <span style="color: #800080;">0</span><span style="color: #000000;">;
  </span><span style="color: #0000ff;">while</span>(<span style="color: #800080;">1</span>) { <span style="color: #008000;">//</span><span style="color: #008000;"> read until the file is empty</span>
    <span style="color: #0000ff;">struct</span> User user =<span style="color: #000000;"> parse_to_user(line);
    users[count</span>++] =<span style="color: #000000;"> user;
  }
  
  sort_users_by_age(users);
  
  </span><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> i = <span style="color: #800080;">0</span>; i &lt; count; ++<span style="color: #000000;">i) {
    </span><span style="color: #0000ff;">char</span>* formatted_user_text =<span style="color: #000000;"> format_to_text(users[i]);
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> write to new file...</span>
<span style="color: #000000;">  }
  </span><span style="color: #008000;">//</span><span style="color: #008000;"> close files...</span>
<span style="color: #000000;">}

</span><span style="color: #0000ff;">int</span> main(<span style="color: #0000ff;">char</span>** args, <span style="color: #0000ff;">int</span><span style="color: #000000;"> argv) {
  format_user_file(</span><span style="color: #800000;">"</span><span style="color: #800000;">/home/zheng/user.txt</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">/home/zheng/formatted_users.txt</span><span style="color: #800000;">"</span><span style="color: #000000;">);
}</span></pre>
</div>
<span class="cnblogs_code_collapse">面向过程代码</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('e33aee73-765b-45cb-8560-b34fd017d8df')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_e33aee73-765b-45cb-8560-b34fd017d8df" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_e33aee73-765b-45cb-8560-b34fd017d8df" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_e33aee73-765b-45cb-8560-b34fd017d8df" class="cnblogs_code_hide">
<pre> <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> User {
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> String name;
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">int</span><span style="color: #000000;"> age;
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> String gender;
  
  </span><span style="color: #0000ff;">public</span> User(String name, <span style="color: #0000ff;">int</span><span style="color: #000000;"> age, String gender) {
    </span><span style="color: #0000ff;">this</span>.name =<span style="color: #000000;"> name;
    </span><span style="color: #0000ff;">this</span>.age =<span style="color: #000000;"> age;
    </span><span style="color: #0000ff;">this</span>.gender =<span style="color: #000000;"> gender;
  }
  
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> User praseFrom(String userInfoText) {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 将text(&ldquo;小王&amp;28&amp;男&rdquo;)解析成类User</span>
<span style="color: #000000;">  }
  
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> String formatToText() {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 将类User格式化成文本（"小王\t28\t男"）</span>
<span style="color: #000000;">  }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> UserFileFormatter {
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> format(String userFile, String formattedUserFile) {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> Open files...</span>
    List users = <span style="color: #0000ff;">new</span> ArrayList&lt;&gt;<span style="color: #000000;">();
    </span><span style="color: #0000ff;">while</span> (<span style="color: #800080;">1</span>) { <span style="color: #008000;">//</span><span style="color: #008000;"> read until file is empty 
      </span><span style="color: #008000;">//</span><span style="color: #008000;"> read from file into userText...</span>
      User user =<span style="color: #000000;"> User.parseFrom(userText);
      users.add(user);
    }
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> sort users by age...</span>
    <span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> i = <span style="color: #800080;">0</span>; i &lt; users.size(); ++<span style="color: #000000;">i) {
      String formattedUserText </span>=<span style="color: #000000;"> user.formatToText();
      </span><span style="color: #008000;">//</span><span style="color: #008000;"> write to new file...</span>
<span style="color: #000000;">    }
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> close files...</span>
<span style="color: #000000;">  }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MainApplication {
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> main(String[] args) {
    UserFileFormatter userFileFormatter </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> UserFileFormatter();
    userFileFormatter.format(</span><span style="color: #800000;">"</span><span style="color: #800000;">/home/zheng/users.txt</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">/home/zheng/formatted_users.txt</span><span style="color: #800000;">"</span><span style="color: #000000;">);
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">面向对象代码</span></div>
<p>面向过程风格的代码被组织成了一组方法集合及其数据结构（struct User），方法和数据结构是分开的 。</p>
<p>面向对象风格的代码被组织成一组类 ，方法和数据结构被绑定在一起，定义在类中。</p>
<p>②面向对象编程比面向过程编程有哪些优势</p>
<p>OOP更加能够应复杂业务应用的开发</p>
<p>OOP风格的代码更加易复用、易扩展、易维护</p>
<p>OOP语言更加人性化、更加高级、更加智能</p>
<p>③三种违反面向对象编程风格的典型代码设计</p>
<p>滥用getter、setter方法：违反了面向对象封装特效</p>
<p>Constants、Utils类的设计问题 ：对于这两个类的设计，我们尽量能做到职责单一，比如：RedisConstants、FileUtils，而不是这几一个大而全的类</p>
<p>基于贫血模型的开发模式：数据和操作分开定义在VO/BO/Entity和Controller/Service/Repository中</p>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">3，接口与抽象类</span></strong></span></p>
<p>①定义</p>
<p>抽象类：不能被实例化、只能被继承。可以包含属性和方法，方法可以包含实现，也可以不包含实现（抽象方法），子类继承抽象类必须实现所有抽象方法</p>
<p>接口：不能被实例化、只能声明方法，方法不能包含实现</p>
<p>②设计思想</p>
<p>抽象类：是一种自下而上的设计思路，现有子类的代码重复，而后抽象成上层的父类（也就是抽象类）</p>
<p>接口：是一种自上而下的设计思路，定义协议或者契约</p>
<p>③使用场景</p>
<p>抽象类：是一种is-a关系，为了解决代码复用问题。</p>
<p>接口：是一种has-a关系，为了解决解耦问题、隔离接口和具体实现，提高代码的扩展性</p>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">4，基于接口而非实现编程</span></strong></span></p>
<p>①做开发的时候需要有抽象意识、封装意识、接口意识。设计越抽象，越能提高代码的灵活性、扩展性、可维护性</p>
<p>②设计指导</p>
<p>函数命名不能暴露任何实现细节。比如，前面提到的uploadToAliyun()就不符合要求，应该去掉aliyun这样的字眼，改为更加抽象的命名方式upload()</p>
<p>封装具体的实现细节。比如跟阿里云特殊的上传流程不应该暴露给调用者</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('06a53aa9-aa8b-4991-bdb8-9198f99af181')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_06a53aa9-aa8b-4991-bdb8-9198f99af181" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_06a53aa9-aa8b-4991-bdb8-9198f99af181" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_06a53aa9-aa8b-4991-bdb8-9198f99af181" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> ImageStore {
  String upload(Image image, String bucketName);
  Image download(String url);
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> AliyunImageStore implements ImageStore {
  </span><span style="color: #008000;">//</span><span style="color: #008000;">...省略属性、构造函数等...</span>

  <span style="color: #0000ff;">public</span><span style="color: #000000;"> String upload(Image image, String bucketName) {
    createBucketIfNotExisting(bucketName);
    String accessToken </span>=<span style="color: #000000;"> generateAccessToken();
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...上传图片到阿里云...
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...返回图片在阿里云上的地址(url)...</span>
<span style="color: #000000;">  }

  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Image download(String url) {
    String accessToken </span>=<span style="color: #000000;"> generateAccessToken();
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...从阿里云下载图片...</span>
<span style="color: #000000;">  }

  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> createBucketIfNotExisting(String bucketName) {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> ...创建bucket...
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> ...失败会抛出异常..</span>
<span style="color: #000000;">  }

  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> String generateAccessToken() {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> ...根据accesskey/secrectkey等生成access token</span>
<span style="color: #000000;">  }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 上传下载流程改变：私有云不需要支持access token</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> PrivateImageStore implements ImageStore  {
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> String upload(Image image, String bucketName) {
    createBucketIfNotExisting(bucketName);
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...上传图片到私有云...
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...返回图片的url...</span>
<span style="color: #000000;">  }

  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Image download(String url) {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...从私有云下载图片...</span>
<span style="color: #000000;">  }

  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> createBucketIfNotExisting(String bucketName) {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> ...创建bucket...
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> ...失败会抛出异常..</span>
<span style="color: #000000;">  }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> ImageStore的使用举例</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ImageProcessingJob {
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> final String BUCKET_NAME = <span style="color: #800000;">"</span><span style="color: #800000;">ai_images_bucket</span><span style="color: #800000;">"</span><span style="color: #000000;">;
  </span><span style="color: #008000;">//</span><span style="color: #008000;">...省略其他无关代码...</span>
  
  <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> process() {
    Image image </span>= ...;<span style="color: #008000;">//</span><span style="color: #008000;">处理图片，并封装为Image对象</span>
    ImageStore imageStore = <span style="color: #0000ff;">new</span><span style="color: #000000;"> PrivateImageStore(...);
    imagestore.upload(image, BUCKET_NAME);
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">demo</span></div>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">5，为什么推荐多用组合少用继承</span></strong></span></p>
<p>继承是is-a的关系，可以解决代码复用问题，但是继承层次过深、过复杂，影响代码的可维护性</p>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">6，DDD充血模型与贫血模型</span></strong></span></p>
<p>基于充血模型的DDD设计模式跟基于贫血模型的传统开发模式相比，主要区别在Service层。充血模式下让部分原来在Service类中的业务逻辑移动到了一个充血的Domain领域模型中，让Service类的实现依赖这个Domain类</p>
<p>在基于充血模型的DDD开发模式下，Service类并不会移除，而是负责一些不适合放在Domain类中的功能。比如，负责与Repository层打交道、跨领域模型业务聚合功能，幂等事务等工作</p>
<p>基于充血模型的DDD设计模式跟基于贫血模型的传统开发模式相比，Controller层和repsitory层的代码基本上相同。因为，Repository层的Entity生命周期有限。Contrller层的VO只是单纯作为一个DTO，两部分的业务都不会太复杂。业务逻辑主要集中在Service层。所以，Repository层和controller层继续使用贫血模型的设计思路是没有问题的</p>
<p>①基于贫血的开发模式</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('52260917-fdac-4ab3-802f-c37cd3caf67c')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_52260917-fdac-4ab3-802f-c37cd3caf67c" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_52260917-fdac-4ab3-802f-c37cd3caf67c" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_52260917-fdac-4ab3-802f-c37cd3caf67c" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> VirtualWalletController {
  </span><span style="color: #008000;">//</span><span style="color: #008000;"> 通过构造函数或者IOC框架注入</span>
  <span style="color: #0000ff;">private</span><span style="color: #000000;"> VirtualWalletService virtualWalletService;
  
  </span><span style="color: #0000ff;">public</span> BigDecimal getBalance(Long walletId) { ... } <span style="color: #008000;">//</span><span style="color: #008000;">查询余额</span>
  <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> debit(Long walletId, BigDecimal amount) { ... } <span style="color: #008000;">//</span><span style="color: #008000;">出账</span>
  <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> credit(Long walletId, BigDecimal amount) { ... } <span style="color: #008000;">//</span><span style="color: #008000;">入账</span>
  <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> transfer(Long fromWalletId, Long toWalletId, BigDecimal amount) { ...} <span style="color: #008000;">//</span><span style="color: #008000;">转账</span>
}</pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('135588d2-1a01-4646-9fa0-d8cf54803cbc')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_135588d2-1a01-4646-9fa0-d8cf54803cbc" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_135588d2-1a01-4646-9fa0-d8cf54803cbc" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_135588d2-1a01-4646-9fa0-d8cf54803cbc" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> VirtualWalletBo {<span style="color: #008000;">//</span><span style="color: #008000;">省略getter/setter/constructor方法</span>
  <span style="color: #0000ff;">private</span><span style="color: #000000;"> Long id;
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> Long createTime;
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> BigDecimal balance;
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> VirtualWalletService {
  </span><span style="color: #008000;">//</span><span style="color: #008000;"> 通过构造函数或者IOC框架注入</span>
  <span style="color: #0000ff;">private</span><span style="color: #000000;"> VirtualWalletRepository walletRepo;
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> VirtualWalletTransactionRepository transactionRepo;
  
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> VirtualWalletBo getVirtualWallet(Long walletId) {
    VirtualWalletEntity walletEntity </span>=<span style="color: #000000;"> walletRepo.getWalletEntity(walletId);
    VirtualWalletBo walletBo </span>=<span style="color: #000000;"> convert(walletEntity);
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> walletBo;
  }
  
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> BigDecimal getBalance(Long walletId) {
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> walletRepo.getBalance(walletId);
  }
  
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> debit(Long walletId, BigDecimal amount) {
    VirtualWalletEntity walletEntity </span>=<span style="color: #000000;"> walletRepo.getWalletEntity(walletId);
    BigDecimal balance </span>=<span style="color: #000000;"> walletEntity.getBalance();
    </span><span style="color: #0000ff;">if</span> (balance.compareTo(amount) &lt; <span style="color: #800080;">0</span><span style="color: #000000;">) {
      </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> NoSufficientBalanceException(...);
    }
    walletRepo.updateBalance(walletId, balance.subtract(amount));
  }
  
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> credit(Long walletId, BigDecimal amount) {
    VirtualWalletEntity walletEntity </span>=<span style="color: #000000;"> walletRepo.getWalletEntity(walletId);
    BigDecimal balance </span>=<span style="color: #000000;"> walletEntity.getBalance();
    walletRepo.updateBalance(walletId, balance.add(amount));
  }
  
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> transfer(Long fromWalletId, Long toWalletId, BigDecimal amount) {
    VirtualWalletTransactionEntity transactionEntity </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> VirtualWalletTransactionEntity();
    transactionEntity.setAmount(amount);
    transactionEntity.setCreateTime(System.currentTimeMillis());
    transactionEntity.setFromWalletId(fromWalletId);
    transactionEntity.setToWalletId(toWalletId);
    transactionEntity.setStatus(Status.TO_BE_EXECUTED);
    Long transactionId </span>=<span style="color: #000000;"> transactionRepo.saveTransaction(transactionEntity);
    </span><span style="color: #0000ff;">try</span><span style="color: #000000;"> {
      debit(fromWalletId, amount);
      credit(toWalletId, amount);
    } </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (InsufficientBalanceException e) {
      transactionRepo.updateStatus(transactionId, Status.CLOSED);
      ...rethrow exception e...
    } </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (Exception e) {
      transactionRepo.updateStatus(transactionId, Status.FAILED);
      ...rethrow exception e...
    }
    transactionRepo.updateStatus(transactionId, Status.EXECUTED);
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<p>②基于充血模型的DDD开发模式</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('b657ab9d-8524-45d5-938e-5118cafbab34')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_b657ab9d-8524-45d5-938e-5118cafbab34" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_b657ab9d-8524-45d5-938e-5118cafbab34" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_b657ab9d-8524-45d5-938e-5118cafbab34" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> VirtualWallet { <span style="color: #008000;">//</span><span style="color: #008000;"> Domain领域模型(充血模型)</span>
  <span style="color: #0000ff;">private</span><span style="color: #000000;"> Long id;
  </span><span style="color: #0000ff;">private</span> Long createTime =<span style="color: #000000;"> System.currentTimeMillis();;
  </span><span style="color: #0000ff;">private</span> BigDecimal balance =<span style="color: #000000;"> BigDecimal.ZERO;
  
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> VirtualWallet(Long preAllocatedId) {
    </span><span style="color: #0000ff;">this</span>.id =<span style="color: #000000;"> preAllocatedId;
  }
  
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> BigDecimal balance() {
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">this</span><span style="color: #000000;">.balance;
  }
  
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> debit(BigDecimal amount) {
    </span><span style="color: #0000ff;">if</span> (<span style="color: #0000ff;">this</span>.balance.compareTo(amount) &lt; <span style="color: #800080;">0</span><span style="color: #000000;">) {
      </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> InsufficientBalanceException(...);
    }
    </span><span style="color: #0000ff;">this</span><span style="color: #000000;">.balance.subtract(amount);
  }
  
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> credit(BigDecimal amount) {
    </span><span style="color: #0000ff;">if</span> (amount.compareTo(BigDecimal.ZERO) &lt; <span style="color: #800080;">0</span><span style="color: #000000;">) {
      </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> InvalidAmountException(...);
    }
    </span><span style="color: #0000ff;">this</span><span style="color: #000000;">.balance.add(amount);
  }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> VirtualWalletService {
  </span><span style="color: #008000;">//</span><span style="color: #008000;"> 通过构造函数或者IOC框架注入</span>
  <span style="color: #0000ff;">private</span><span style="color: #000000;"> VirtualWalletRepository walletRepo;
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> VirtualWalletTransactionRepository transactionRepo;
  
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> VirtualWallet getVirtualWallet(Long walletId) {
    VirtualWalletEntity walletEntity </span>=<span style="color: #000000;"> walletRepo.getWalletEntity(walletId);
    VirtualWallet wallet </span>=<span style="color: #000000;"> convert(walletEntity);
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> wallet;
  }
  
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> BigDecimal getBalance(Long walletId) {
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> walletRepo.getBalance(walletId);
  }
  
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> debit(Long walletId, BigDecimal amount) {
    VirtualWalletEntity walletEntity </span>=<span style="color: #000000;"> walletRepo.getWalletEntity(walletId);
    VirtualWallet wallet </span>=<span style="color: #000000;"> convert(walletEntity);
    wallet.debit(amount);
    walletRepo.updateBalance(walletId, wallet.balance());
  }
  
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> credit(Long walletId, BigDecimal amount) {
    VirtualWalletEntity walletEntity </span>=<span style="color: #000000;"> walletRepo.getWalletEntity(walletId);
    VirtualWallet wallet </span>=<span style="color: #000000;"> convert(walletEntity);
    wallet.credit(amount);
    walletRepo.updateBalance(walletId, wallet.balance());
  }
  
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> transfer(Long fromWalletId, Long toWalletId, BigDecimal amount) {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...跟基于贫血模型的传统开发模式的代码一样...</span>
<span style="color: #000000;">  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">7，面向对象分析（OOA）、面向对象设计（OOD）、面向对象编程（OOP）</span></strong></span></p>
<p>①面向对象分析：面向对象分析主要的分析对象是&ldquo;需求&rdquo;，可以看成是需求分析</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('e3f98c29-ee0a-4c27-899f-3b51d17fe3a7')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_e3f98c29-ee0a-4c27-899f-3b51d17fe3a7" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_e3f98c29-ee0a-4c27-899f-3b51d17fe3a7" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_e3f98c29-ee0a-4c27-899f-3b51d17fe3a7" class="cnblogs_code_hide">
<pre><span style="color: #800080;">1</span><span style="color: #000000;">，调用方进行接口请求的时候，将 URL、AppID、密码、时间戳拼接在一起，通过加密算法生成 token，并且将 token、AppID、时间戳拼接在 URL 中，一并发送到微服务端。
</span><span style="color: #800080;">2</span><span style="color: #000000;">，微服务端在接收到调用方的接口请求之后，从请求中拆解出 token、AppID、时间戳。
</span><span style="color: #800080;">3</span><span style="color: #000000;">，微服务端首先检查传递过来的时间戳跟当前时间，是否在 token 失效时间窗口内。如果已经超过失效时间，那就算接口调用鉴权失败，拒绝接口调用请求。
</span><span style="color: #800080;">4</span>，如果 token 验证没有过期失效，微服务端再从自己的存储中，取出 AppID 对应的密码，通过同样的 token 生成算法，生成另外一个 token，与调用方传递过来的 token 进行匹配。如果一致，则鉴权成功，允许接口调用；否则就拒绝接口调用。</pre>
</div>
<span class="cnblogs_code_collapse">详细需求分析文档</span></div>
<p>②面向对象设计：根据需求转化为具体的类</p>
<p>划分职责而识别出有哪些类</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('3f9cca73-f7f1-45ef-ba60-78262a667ddb')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_3f9cca73-f7f1-45ef-ba60-78262a667ddb" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_3f9cca73-f7f1-45ef-ba60-78262a667ddb" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_3f9cca73-f7f1-45ef-ba60-78262a667ddb" class="cnblogs_code_hide">
<pre><span style="color: #800080;">1</span><span style="color: #000000;">，把 URL、AppID、密码、时间戳拼接为一个字符串；
</span><span style="color: #800080;">2</span><span style="color: #000000;">，对字符串通过加密算法加密生成 token；
</span><span style="color: #800080;">3</span><span style="color: #000000;">，将 token、AppID、时间戳拼接到 URL 中，形成新的 URL；
</span><span style="color: #800080;">4</span><span style="color: #000000;">，解析 URL，得到 token、AppID、时间戳等信息；
</span><span style="color: #800080;">5</span><span style="color: #000000;">，从存储中取出 AppID 和对应的密码；
</span><span style="color: #800080;">6</span><span style="color: #000000;">，根据时间戳判断 token 是否过期失效；
</span><span style="color: #800080;">7</span><span style="color: #000000;">，验证两个 token 是否匹配；

从上面的功能列表中，我们发现，</span><span style="color: #800080;">1</span>、<span style="color: #800080;">2</span>、<span style="color: #800080;">6</span>、<span style="color: #800080;">7</span> 都是跟 token 有关，负责 token 的生成、验证；<span style="color: #800080;">3</span>、<span style="color: #800080;">4</span> 都是在处理 URL，负责 URL 的拼接、解析；<span style="color: #800080;">5</span> 是操作 AppID 和密码，负责从存储中读取 AppID 和密码。所以，我们可以粗略地得到三个核心的类：AuthToken、Url、CredentialStorage。AuthToken 负责实现 <span style="color: #800080;">1</span>、<span style="color: #800080;">2</span>、<span style="color: #800080;">6</span>、<span style="color: #800080;">7</span> 这四个操作；Url 负责 <span style="color: #800080;">3</span>、<span style="color: #800080;">4</span> 两个操作；CredentialStorage 负责 <span style="color: #800080;">5</span> 这个操作</pre>
</div>
<span class="cnblogs_code_collapse">下面是我逐句拆解上述需求描述之后，得到的功能点列表</span></div>
<p>定义类及其属性方法</p>
<p>定义类之间的交互关系</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('db83a085-b099-4274-95eb-bd61bada3209')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_db83a085-b099-4274-95eb-bd61bada3209" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_db83a085-b099-4274-95eb-bd61bada3209" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_db83a085-b099-4274-95eb-bd61bada3209" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> A { ... }
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> B extends A { ... }</pre>
</div>
<span class="cnblogs_code_collapse">泛化（Generalization）可以简单理解为继承关系。具体到 Java 代码就是下面这样</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('9af50f75-902f-42ee-8a71-5652cd742b27')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_9af50f75-902f-42ee-8a71-5652cd742b27" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_9af50f75-902f-42ee-8a71-5652cd742b27" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_9af50f75-902f-42ee-8a71-5652cd742b27" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> A {...}
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> B implements A { ... }</pre>
</div>
<span class="cnblogs_code_collapse">实现（Realization）一般是指接口和实现类之间的关系。具体到 Java 代码就是下面这样：</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('c92452d0-3eb7-4af1-9b62-1e6ae0fb483d')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_c92452d0-3eb7-4af1-9b62-1e6ae0fb483d" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_c92452d0-3eb7-4af1-9b62-1e6ae0fb483d" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_c92452d0-3eb7-4af1-9b62-1e6ae0fb483d" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> A {
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> B b;
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> A(B b) {
    </span><span style="color: #0000ff;">this</span>.b =<span style="color: #000000;"> b;
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">聚合（Aggregation）是一种包含关系，A 类对象包含 B 类对象，B 类对象的生命周期可以不依赖 A 类对象的生命周期，也就是说可以单独销毁 A 类对象而不影响 B 对象</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('4875b206-eb88-43df-94a0-2351178864e2')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_4875b206-eb88-43df-94a0-2351178864e2" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_4875b206-eb88-43df-94a0-2351178864e2" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_4875b206-eb88-43df-94a0-2351178864e2" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> A {
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> B b;
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> A() {
    </span><span style="color: #0000ff;">this</span>.b = <span style="color: #0000ff;">new</span><span style="color: #000000;"> B();
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">组合（Composition）也是一种包含关系。A 类对象包含 B 类对象，B 类对象的生命周期跟依赖 A 类对象的生命周期，B 类对象不可单独存在</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('371a0efc-7a54-4951-b826-2a09be96275f')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_371a0efc-7a54-4951-b826-2a09be96275f" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_371a0efc-7a54-4951-b826-2a09be96275f" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_371a0efc-7a54-4951-b826-2a09be96275f" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> A {
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> B b;
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> A(B b) {
    </span><span style="color: #0000ff;">this</span>.b =<span style="color: #000000;"> b;
  }
}
或者
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> A {
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> B b;
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> A() {
    </span><span style="color: #0000ff;">this</span>.b = <span style="color: #0000ff;">new</span><span style="color: #000000;"> B();
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">关联（Association）是一种非常弱的关系，包含聚合、组合两种关系。具体到代码层面，如果 B 类对象是 A 类的成员变量，那 B 类和 A 类就是关联关系</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('b461cf2b-770e-4661-9a0f-4630dfa81496')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_b461cf2b-770e-4661-9a0f-4630dfa81496" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_b461cf2b-770e-4661-9a0f-4630dfa81496" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_b461cf2b-770e-4661-9a0f-4630dfa81496" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> A {
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> B b;
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> A(B b) {
    </span><span style="color: #0000ff;">this</span>.b =<span style="color: #000000;"> b;
  }
}
或者
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> A {
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> B b;
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> A() {
    </span><span style="color: #0000ff;">this</span>.b = <span style="color: #0000ff;">new</span><span style="color: #000000;"> B();
  }
}
或者
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> A {
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> func(B b) { ... }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">依赖（Dependency）是一种比关联关系更加弱的关系，包含关联关系。不管是 B 类对象是 A 类对象的成员变量，还是 A 类的方法使用 B 类对象作为参数或者返回值、局部变量，只要 B 类对象和 A 类对象有任何使用关系，我们都称它们有依赖关系</span></div>
<p>将类组装起来并提供执行入口</p>
<p>③面向对象编程：将设计思路翻译成代码实现。有了前面的类图，实现就简单了</p>
<p>不过，在平时的工作中，大部分程序员往往都是在脑子里或者草纸上完成面向对象分析和设计，然后就开始写代码了，边写边思考边重构，并不会严格地按照刚刚的流程来执行。而且，说实话，即便我们在写代码之前，花很多时间做分析和设计，绘制出完美的类图、UML 图，也不可能把每个细节、交互都想得很清楚。在落实到代码的时候，我们还是要反复迭代、重构、打破重写。毕竟，整个软件开发本来就是一个迭代、修修补补、遇到问题解决问题的过程，是一个不断重构的过程。我们没法严格地按照顺序执行各个步骤</p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: #169fe6;"><span style="color: #ffffff;"><strong>三、设计原则</strong></span></p>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">1，单一职责原则（SRP Single Responsibility Principle）</span></strong></span></p>
<p>①理解SRP</p>
<p>一个类只负责完成一个职责或功能。不要设计大而全的类，要设计粒度小、功能单一的类。</p>
<p>单一职责原则是为了实现代码的高内聚、低耦合，提高代码的<strong>复用性</strong>、<strong>可读性</strong>、<strong>可维护性</strong>。</p>
<p>②指导设计</p>
<p>类中的代码行数、函数或属性过多（代码行数不易超过200行，函数和属性不易超过10个），会影响代码的可读性与可维护性，我们需要考虑对类进行拆分。</p>
<p>类依赖的其他类过多，不符合高内聚、低耦合的设计思想，我们需要考虑对类进行拆分。</p>
<p>私有方法过多，我们就要考虑能否将私有方法独立到新的类中，设置为public方法，供更多的类使用，从而提高代码的复用性</p>
<p>比较难给类起一个名字，很难用一个业务名词概括，或者只能用一个笼统的Manager、Context之类的词语来命名，这说明类的职责定义可能不够清晰</p>
<p>类中的大量方法都是集中操作类中的某几个属性，比如UserInfo例子中，如果一半的方法都是在操作address信息，那就可以考虑将这几个属性和对应的方法拆出来</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('bc6c4c67-b2f5-4672-9993-9c36c24ca076')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_bc6c4c67-b2f5-4672-9993-9c36c24ca076" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_bc6c4c67-b2f5-4672-9993-9c36c24ca076" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_bc6c4c67-b2f5-4672-9993-9c36c24ca076" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> UserInfo {
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">long</span><span style="color: #000000;"> userId;
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> String username;
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> String email;
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> String telephone;
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">long</span><span style="color: #000000;"> createTime;
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">long</span><span style="color: #000000;"> lastLoginTime;
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> String avatarUrl;
  </span><span style="color: #0000ff;">private</span> String provinceOfAddress; <span style="color: #008000;">//</span><span style="color: #008000;"> 省</span>
  <span style="color: #0000ff;">private</span> String cityOfAddress; <span style="color: #008000;">//</span><span style="color: #008000;"> 市</span>
  <span style="color: #0000ff;">private</span> String regionOfAddress; <span style="color: #008000;">//</span><span style="color: #008000;"> 区 </span>
  <span style="color: #0000ff;">private</span> String detailedAddress; <span style="color: #008000;">//</span><span style="color: #008000;"> 详细地址
  </span><span style="color: #008000;">//</span><span style="color: #008000;"> ...省略其他属性和方法...</span>
}</pre>
</div>
<span class="cnblogs_code_collapse">UserInfo</span></div>
<p><strong>个人理解一句话总结：类的职责尽量简单明确，不要设计大而全的类 。提高代码的可复用性、可读性、可维护性</strong></p>
<p>&nbsp;</p>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">2，开闭原则（OCP Open Closed Principle）&nbsp;</span></strong></span></p>
<p>①理解OCP</p>
<p>对扩展开放、对修改关闭，提高代码的<strong>扩展性</strong></p>
<p>添加一个新功能，应该是通过在已有代码基础上扩展代码（新增模块、类、方法、属性等），而非修改已有代码（修改模块、类、方法、属性等）的方式来完成。</p>
<p>开闭原则并不是完全杜绝修改，而是以最小的修改代码的代价来完成新的功能开发。</p>
<p>同样的代码改动，在粗代码粒度下，可能被认为是&ldquo;修改&rdquo;；在细代码粒度下，可能被任务是&ldquo;扩展&rdquo;</p>
<p>②如何做到&ldquo;对扩展开放，对修改关闭&rdquo;</p>
<p>时刻具备扩展、抽象、封装意识。我们要多花点时间思考一下，这段代码未来可能有哪些需求变更，如何设计代码结构，事先留好扩展点，以便在未来需求变更的时候，在不改动代码整体结构、做到最小代码改动的情况下，将新的代码灵活地插入到扩展点上</p>
<p>很多设计原则、设计思想、设计模式，都是以提高代码的扩展性为最终目的的</p>
<p><strong><strong>个人理解一句话总结</strong>：尽量小的改动，完成新的功能模块的开发。高扩展性&nbsp;</strong></p>
<p>&nbsp;</p>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">3，里氏替换原则（LSP Liskov Substitution Principle）</span></strong></span></p>
<p>里氏替换原则是用来指导，<strong>继承关系中子类该如何设计</strong></p>
<p>核心理解就是按照协议来设计子类</p>
<p>父类定义了函数的&ldquo;约定&rdquo;（或者叫协议），那子类可以改变函数的内部实现逻辑，但不能改变函数原有的&ldquo;约定&rdquo;。这里的约定包括：函数声明要实现的功能；对输入、输出、异常的约定；甚至包括注释中所罗列的任何特殊说明。</p>
<p>①与多态的区别</p>
<p>多态是面向对象编程的一大特性，也是面向对象编程语言的一种语法。它是一种代码实现的思路</p>
<p>里式替换是一种设计原则，用来指导继承关系中子类该如何设计，子类的设计要保证在替换父类的时候，不改变原有程序的逻辑及不破坏原有程序的正确性。</p>
<p><strong><strong>个人理解一句话总结</strong>：指导设计继承类，约定实现规则</strong></p>
<p>&nbsp;</p>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">4，接口隔离原则（ISP Interface Segregation Principle）&nbsp;</span></strong></span></p>
<p>①理解ISP</p>
<p>把&ldquo;接口&rdquo;理解为一组接口集合（微服务或者是类库的接口）：如果部分接口只被部分调用者使用，我们就需要将这部分接口隔离出来，单独给这部分调用者使用，而不强迫其他调用者也依赖这部分不会被用到的接口</p>
<p>把&ldquo;接口&rdquo;理解为单个 API 接口或函数：部分调用者只需要函数中的部分功能，那我们就需要把函数拆分成粒度更细的多个函数，让调用者只依赖它需要的那个细粒度函数</p>
<p>把&ldquo;接口&rdquo;理解为 OOP 中的接口：也可以理解为面向对象编程语言中的接口语法。那接口的设计要尽量单一，不要让接口的实现类和调用者，依赖不需要的接口函数</p>
<p><strong><strong>个人理解一句话总结</strong>：隔离出不相干的接口，保留客户端关心的接口</strong></p>
<p>&nbsp;</p>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">5，依赖反转原则（DIP Dependency Inversion Principle）</span></strong></span></p>
<p>高层模块不依赖低层模块，它们共同依赖同一个抽象。抽象不要依赖具体实现细节，具体实现细节依赖抽象</p>
<p>这条原则主要还是用来指导<strong>框架层面的设计</strong></p>
<p><strong>个人理解一句话总结：消除类与类直接的依赖。DIP原则用于指导抽象出接口或者抽象类</strong></p>
<p>&nbsp;</p>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">6，KISS原则（简单原则）</span></strong></span></p>
<p>KISS 原则是保持代码<strong>可读和可维护</strong>的重要手段。KISS 原则中的&ldquo;简单&rdquo;并不是以代码行数来考量的。代码行数越少并不代表代码越简单，我们还要考虑逻辑复杂度、实现难度、代码的可读性等。而且，本身就复杂的问题，用复杂的方法解决，并不违背 KISS 原则。除此之外，同样的代码，在某个业务场景下满足 KISS 原则，换一个应用场景可能就不满足了</p>
<p>①指导设计</p>
<p>不要使用同事可能不懂的技术来实现代码</p>
<p>不要重复造轮子，要善于使用已经有的工具类库</p>
<p>不要过度优化</p>
<p><strong>个人理解一句话总结：保证代码简单，提高代码的可读性与可维护性</strong></p>
<p>&nbsp;</p>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">7，YAGNI原则（不要过度设计）</span></strong></span></p>
<p>不要去设计当前用不到的功能；不要去编写当前用不到的代码。实际上，这条原则的核心思想就是：不要做过度设计。</p>
<p>YAGNI 原则跟 KISS 原则并非一回事儿。KISS 原则讲的是&ldquo;如何做&rdquo;的问题（尽量保持简单），而 YAGNI 原则说的是&ldquo;要不要做&rdquo;的问题（当前不需要的就不要做）&nbsp;</p>
<p>&nbsp;</p>
<p><strong><span style="font-size: 16px; color: #ff6600;">8，DRY原则（不要写重复的代码）</span></strong></p>
<p>三种代码重复的情况：实现逻辑重复、功能语义重复、代码执行重复。实现逻辑重复，但功能语义不重复的代码，并不违反 DRY 原则。实现逻辑不重复，但功能语义重复的代码，也算是违反 DRY 原则。除此之外，代码执行重复也算是违反 DRY 原则</p>
<p><strong>个人理解一句话总结：发现功能类似的方法，不要重复实现，尽量复用代码（可以重构代码）</strong></p>
<p>&nbsp;</p>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">9，LOD原则（迪米法特原则）</span></strong></span></p>
<p>高类聚：相近功能放在一个类中</p>
<p>松耦合：类之间的依赖清晰，一个类的改动不会影响另一个类</p>
<p>迪米法特原则：不该有直接依赖关系的类之间，不要有依赖；有依赖关系的类之间，尽量只依赖必要的接口</p>
<p><span style="color: #000000;"><strong>个人理解一句话总结：减少类之间的依赖关系，侧重低耦合</strong></span></p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: #169fe6;"><span style="color: #ffffff;"><strong>四、规范与重构</strong></span></p>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">1，重构的目的：为什么重构（Why）&nbsp;</span></strong></span></p>
<p>对于项目来言，重构可以保持代码质量持续处于一个可控状态，不至于腐化到无可救药的地步。对于个人而言，重构非常锻炼一个人的代码能力，并且是一件非常有成就感的事情。它是我们学习的经典设计思想、原则、模式、编程规范等理论知识的练兵场</p>
<p>&nbsp;</p>
<p><span style="font-size: 16px; color: #ff6600;"><strong>2，重构的对象：重构什么（What）&nbsp;</strong></span></p>
<p>大规模高层次重构：代码分层、模块化、解耦、梳理类与类之间的交互、抽象复用组件等等。这部分工作利用的更多的是比较抽象、比较顶层的设计思想、原则、模式&nbsp;</p>
<p>小规模低层次重构：规范命名、注释、修正函数参数过多、消除超大类、提取重复代码等等编程细节问题，主要是针对类、函数级别的重构。更多的是利用编码规范这一理论知识</p>
<p>&nbsp;</p>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">3，重构的时机：什么时候重构（When）</span></strong></span></p>
<p>建立持续重构意识，把重构作为开发必不可少的部分，融入开发中。而不是等代码出现很大的问题的时候，再大刀阔斧的重构</p>
<p>&nbsp;</p>
<p><strong><span style="font-size: 16px; color: #ff6600;">4，重构的方法：如何重构（How）</span></strong></p>
<p>大规模高层次的重构难度比较大，需要组织、有计划地进行，分阶段地小步快跑，时刻让代码处于一个可运行的状态。而小规模低层次的重构，因为影响范围小，改动耗时短，所以，只要你愿意并且有时间，随时随地都可以去做。我们还可以借助很多成熟的静态代码分析工具（比如 CheckStyle、FindBugs、PMD），来自动发现代码中的问题，然后针对性地进行重构优化。</p>
<p>&nbsp;</p>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">5，采用单元测试&nbsp;保证重构不出错</span></strong></span></p>
<p>单元测试：单元测试的测试对象是类或者函数，用来测试一个类和函数是否都按照预期的逻辑执行。这是代码层级的测试</p>
<p>集成测试：集成测试的测试对象是整个系统或者某个功能模块，比如测试用户注册、登录功能是否正常，是一种端到端（end to end）的测试</p>
<p>①如何编写单元测试：</p>
<p>写单元测试就是针对代码设计覆盖各种输入、异常、边界条件的测试用例，并将这些测试用例翻译成代码的过程。&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('0ef86720-f720-4f01-9370-d67e801f58a3')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_0ef86720-f720-4f01-9370-d67e801f58a3" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_0ef86720-f720-4f01-9370-d67e801f58a3" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_0ef86720-f720-4f01-9370-d67e801f58a3" class="cnblogs_code_hide">
<pre><span style="color: #000000;">为了保证测试的全面性，针对 toNumber() 函数，我们需要设计下面这样几个测试用例

如果字符串只包含数字：&ldquo;</span><span style="color: #800080;">123</span>&rdquo;，toNumber() 函数输出对应的整数：<span style="color: #800080;">123</span><span style="color: #000000;">。
如果字符串是空或者 </span><span style="color: #0000ff;">null</span>，toNumber() 函数返回：<span style="color: #0000ff;">null</span><span style="color: #000000;">。
如果字符串包含首尾空格：&ldquo; </span><span style="color: #800080;">123</span>&rdquo;，&ldquo;<span style="color: #800080;">123</span> &rdquo;，&ldquo; <span style="color: #800080;">123</span> &rdquo;，toNumber() 返回对应的整数：<span style="color: #800080;">123</span><span style="color: #000000;">。
如果字符串包含多个首尾空格：&ldquo; </span><span style="color: #800080;">123</span> &rdquo;，toNumber() 返回对应的整数：<span style="color: #800080;">123</span><span style="color: #000000;">；
如果字符串包含非数字字符：&ldquo;123a4&rdquo;，&ldquo;</span><span style="color: #800080;">123</span> <span style="color: #800080;">4</span>&rdquo;，toNumber() 返回 <span style="color: #0000ff;">null</span>；</pre>
</div>
<span class="cnblogs_code_collapse">单元测试用例</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('bb916a6b-f345-4fc7-8637-1d2fdc142814')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_bb916a6b-f345-4fc7-8637-1d2fdc142814" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_bb916a6b-f345-4fc7-8637-1d2fdc142814" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_bb916a6b-f345-4fc7-8637-1d2fdc142814" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Text {
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> String content;

  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Text(String content) {
    </span><span style="color: #0000ff;">this</span>.content =<span style="color: #000000;"> content;
  }

  </span><span style="color: #008000;">/*</span><span style="color: #008000;">*
   * 将字符串转化成数字，忽略字符串中的首尾空格；
   * 如果字符串中包含除首尾空格之外的非数字字符，则返回null。
   </span><span style="color: #008000;">*/</span>
  <span style="color: #0000ff;">public</span><span style="color: #000000;"> Integer toNumber() {
    </span><span style="color: #0000ff;">if</span> (content == <span style="color: #0000ff;">null</span> ||<span style="color: #000000;"> content.isEmpty()) {
      </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">null</span><span style="color: #000000;">;
    }
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...省略代码实现...</span>
    <span style="color: #0000ff;">return</span> <span style="color: #0000ff;">null</span><span style="color: #000000;">;
  }
}



import org.junit.Assert;
import org.junit.Test;

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> TextTest {
  @Test
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> testToNumber() {
    Text text </span>= <span style="color: #0000ff;">new</span> Text(<span style="color: #800000;">"</span><span style="color: #800000;">123</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    Assert.assertEquals(</span><span style="color: #0000ff;">new</span> Integer(<span style="color: #800080;">123</span><span style="color: #000000;">), text.toNumber());
  }

  @Test
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> testToNumber_nullorEmpty() {
    Text text1 </span>= <span style="color: #0000ff;">new</span> Text(<span style="color: #0000ff;">null</span><span style="color: #000000;">);
    Assert.assertNull(text1.toNumber());

    Text text2 </span>= <span style="color: #0000ff;">new</span> Text(<span style="color: #800000;">""</span><span style="color: #000000;">);
    Assert.assertNull(text2.toNumber());
  }

  @Test
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> testToNumber_containsLeadingAndTrailingSpaces() {
    Text text1 </span>= <span style="color: #0000ff;">new</span> Text(<span style="color: #800000;">"</span><span style="color: #800000;"> 123</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    Assert.assertEquals(</span><span style="color: #0000ff;">new</span> Integer(<span style="color: #800080;">123</span><span style="color: #000000;">), text1.toNumber());

    Text text2 </span>= <span style="color: #0000ff;">new</span> Text(<span style="color: #800000;">"</span><span style="color: #800000;">123 </span><span style="color: #800000;">"</span><span style="color: #000000;">);
    Assert.assertEquals(</span><span style="color: #0000ff;">new</span> Integer(<span style="color: #800080;">123</span><span style="color: #000000;">), text2.toNumber());

    Text text3 </span>= <span style="color: #0000ff;">new</span> Text(<span style="color: #800000;">"</span><span style="color: #800000;"> 123 </span><span style="color: #800000;">"</span><span style="color: #000000;">);
    Assert.assertEquals(</span><span style="color: #0000ff;">new</span> Integer(<span style="color: #800080;">123</span><span style="color: #000000;">), text3.toNumber());
  }

  @Test
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> testToNumber_containsMultiLeadingAndTrailingSpaces() {
    Text text1 </span>= <span style="color: #0000ff;">new</span> Text(<span style="color: #800000;">"</span><span style="color: #800000;">  123</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    Assert.assertEquals(</span><span style="color: #0000ff;">new</span> Integer(<span style="color: #800080;">123</span><span style="color: #000000;">), text1.toNumber());

    Text text2 </span>= <span style="color: #0000ff;">new</span> Text(<span style="color: #800000;">"</span><span style="color: #800000;">123  </span><span style="color: #800000;">"</span><span style="color: #000000;">);
    Assert.assertEquals(</span><span style="color: #0000ff;">new</span> Integer(<span style="color: #800080;">123</span><span style="color: #000000;">), text2.toNumber());

    Text text3 </span>= <span style="color: #0000ff;">new</span> Text(<span style="color: #800000;">"</span><span style="color: #800000;">  123  </span><span style="color: #800000;">"</span><span style="color: #000000;">);
    Assert.assertEquals(</span><span style="color: #0000ff;">new</span> Integer(<span style="color: #800080;">123</span><span style="color: #000000;">), text3.toNumber());
  }

  @Test
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> testToNumber_containsInvalidCharaters() {
    Text text1 </span>= <span style="color: #0000ff;">new</span> Text(<span style="color: #800000;">"</span><span style="color: #800000;">123a4</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    Assert.assertNull(text1.toNumber());

    Text text2 </span>= <span style="color: #0000ff;">new</span> Text(<span style="color: #800000;">"</span><span style="color: #800000;">123 4</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    Assert.assertNull(text2.toNumber());
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">单元测试demo</span></div>
<p>②如何编写可测试性代码</p>
<p>依赖注入是编写可测试性代码的最有效手段。通过依赖注入，我们在编写单元测试的时候，可以通过 mock 的方法解依赖外部服务，这也是我们在编写单元测试的过程中最有技术挑战的地方</p>
<p>&nbsp;</p>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">6，如何&ldquo;解耦&rdquo;？</span></strong></span></p>
<p>①封装与抽象</p>
<p>封装和抽象可以有效地隐藏实现的复杂性，隔离实现的易变性，给依赖的模块提供稳定且易用的抽象接口</p>
<p>②中间层</p>
<p>引入中间层能简化模块或类之间的依赖关系</p>
<p>第一阶段：引入一个中间层，包裹老的接口，提供新的接口定义。</p>
<p>第二阶段：新开发的代码依赖中间层提供的新接口。</p>
<p>第三阶段：将依赖老接口的代码改为调用新接口。</p>
<p>第四阶段：确保所有的代码都调用新接口之后，删除掉老的接口</p>
<p>③模块化</p>
<p>模块化是构建复杂系统常用的手段</p>
<p>模块化的思想无处不在，像 SOA、微服务、lib 库、系统内模块划分，甚至是类、函数的设计，都体现了模块化思想。如果追本溯源，模块化思想更加本质的东西就是分而治之</p>
<p>④其他设计思想和原则</p>
<p>单一职责原则、基于接口而非实现编程、依赖注入、多用组合少用继承、迪米特法则</p>
<p>&nbsp;</p>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">7，命名</span></strong></span></p>
<p>①利用上下文简化命名</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('fdd38104-ccd9-49ca-9605-1b34715ec12d')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_fdd38104-ccd9-49ca-9605-1b34715ec12d" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_fdd38104-ccd9-49ca-9605-1b34715ec12d" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_fdd38104-ccd9-49ca-9605-1b34715ec12d" class="cnblogs_code_hide">
<pre>User user = <span style="color: #0000ff;">new</span><span style="color: #000000;"> User();
user.getName(); </span><span style="color: #008000;">//</span><span style="color: #008000;"> 借助user对象这个上下文</span></pre>
</div>
<span class="cnblogs_code_collapse">借助对象简化命名</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('814ffd9a-8c50-47cf-88cf-e3cec4aa4416')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_814ffd9a-8c50-47cf-88cf-e3cec4aa4416" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_814ffd9a-8c50-47cf-88cf-e3cec4aa4416" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_814ffd9a-8c50-47cf-88cf-e3cec4aa4416" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> uploadUserAvatarImageToAliyun(String userAvatarImageUri);
</span><span style="color: #008000;">//</span><span style="color: #008000;">利用上下文简化为：</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> uploadUserAvatarImageToAliyun(String imageUri);</pre>
</div>
<span class="cnblogs_code_collapse">借助函数这个上下文来简化命名</span></div>
<p>②命名要可读、可搜索</p>
<p>我们在命名的时候，最好能符合整个项目的命名习惯。大家都用&ldquo;selectXXX&rdquo;表示查询，你就不要用&ldquo;queryXXX&rdquo;；大家都用&ldquo;insertXXX&rdquo;表示插入一条数据，你就要不用&ldquo;addXXX&rdquo;，统一规约是很重要的，能减少很多不必要的麻烦</p>
<p>③如何命名接口和抽象类</p>
<p>接口有两种命名方式：一种是在接口中带前缀&ldquo;I&rdquo;；另一种是在接口的实现类中带后缀&ldquo;Impl&rdquo;。对于抽象类的命名，也有两种方式，一种是带上前缀&ldquo;Abstract&rdquo;，一种是不带前缀。这两种命名方式都可以，关键是要在项目中统一</p>
<p>&nbsp;</p>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">8，注释</span></strong></span></p>
<p>注释的目的就是让代码更容易看懂。只要符合这个要求的内容，你就可以将它写到注释里。总结一下，注释的内容主要包含这样三个方面：做什么、为什么、怎么做。对于一些复杂的类和接口，我们可能还需要写明&ldquo;如何用&rdquo;。</p>
<p>注释本身有一定的维护成本，所以并非越多越好。类和函数一定要写注释，而且要写得尽可能全面、详细，而函数内部的注释要相对少一些，一般都是靠好的命名、提炼函数、解释性变量、总结性注释来提高代码可读性。</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('89ffc8ef-6156-43d8-b2b9-3fa512bfa2fa')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_89ffc8ef-6156-43d8-b2b9-3fa512bfa2fa" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_89ffc8ef-6156-43d8-b2b9-3fa512bfa2fa" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_89ffc8ef-6156-43d8-b2b9-3fa512bfa2fa" class="cnblogs_code_hide">
<pre><span style="color: #008000;">/*</span><span style="color: #008000;">*
* (what) Bean factory to create beans. 
* 
* (why) The class likes Spring IOC framework, but is more lightweight. 
*
* (how) Create objects from different sources sequentially:
* user specified object &gt; SPI &gt; configuration &gt; default object.
</span><span style="color: #008000;">*/</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> BeansFactory {
  </span><span style="color: #008000;">//</span><span style="color: #008000;"> ...</span>
}</pre>
</div>
<span class="cnblogs_code_collapse">注释</span></div>
<p>&nbsp;</p>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">9，代码风格</span></strong></span></p>
<p>①类、函数多大才合适</p>
<p>类：当一个类的代码读起来让你感觉头大了，实现某个功能时不知道该用哪个函数了，想用哪个函数翻半天都找不到了，只用到一个小功能要引入整个类（类中包含很多无关此功能实现的函数）的时候，这就说明类的行数过多了</p>
<p>函数：一个函数最好能完整地显示在 IDE 中，最大代码行数不能超过 50</p>
<p>②一行代码多长合适</p>
<p>&nbsp;一行代码最长最好不能超过 IDE 显示的宽度</p>
<p>③善用空格分隔单元块</p>
<p>对于比较长的函数，如果逻辑上可以分为几个独立的代码块，在不方便将这些独立的代码块抽取成小函数的情况下，可以使用空行来分割各个代码块</p>
<p>④四格缩进还是两格缩进</p>
<p>推荐两格缩进，在代码嵌套层次比较深的情况下，累计缩进较多的话，容易导致一个语句被折成两行，影响代码可读性。不要使用tab缩进</p>
<p>⑤大括号是否要另起一行</p>
<p>我个人还是比较推荐，将括号放到跟语句同一行的风格</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;">1</span> <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ClassName {
</span><span style="color: #008080;">2</span>   <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> foo() {
</span><span style="color: #008080;">3</span>     <span style="color: #008000;">//</span><span style="color: #008000;"> method body</span>
<span style="color: #008080;">4</span> <span style="color: #000000;">  }
</span><span style="color: #008080;">5</span> }</pre>
</div>
<p>⑥类中成员的排列顺序</p>
<p>依赖类按照字母序从小到大排列</p>
<p>成员变量排在函数的前面。成员变量之间或函数之间，都是按照&ldquo;先静态（静态函数或静态成员变量）、后普通（非静态函数或非静态成员变量）&rdquo;的方式来排列的</p>
<p>除此之外，成员变量之间或函数之间，还会按照作用域范围从大到小的顺序来排列，先写 public 成员变量或函数，然后是 protected 的，最后是 private 的</p>
<p>&nbsp;</p>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">10， 编程技巧</span></strong></span></p>
<p>①把代码分隔成更小的单元块</p>
<p>我们要有模块化和抽象思维，善于将大块的复杂逻辑提炼成类或者函数，屏蔽掉细节，让阅读代码的人不至于迷失在细节中，这样能极大地提高代码的可读性</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('a97c9f12-6d0b-47a2-b2c8-330e34f19a8b')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_a97c9f12-6d0b-47a2-b2c8-330e34f19a8b" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_a97c9f12-6d0b-47a2-b2c8-330e34f19a8b" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_a97c9f12-6d0b-47a2-b2c8-330e34f19a8b" class="cnblogs_code_hide">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> 重构前的代码</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> invest(<span style="color: #0000ff;">long</span> userId, <span style="color: #0000ff;">long</span><span style="color: #000000;"> financialProductId) {
  Calendar calendar </span>=<span style="color: #000000;"> Calendar.getInstance();
  calendar.setTime(date);
  calendar.</span><span style="color: #0000ff;">set</span>(Calendar.DATE, (calendar.<span style="color: #0000ff;">get</span>(Calendar.DATE) + <span style="color: #800080;">1</span><span style="color: #000000;">));
  </span><span style="color: #0000ff;">if</span> (calendar.<span style="color: #0000ff;">get</span>(Calendar.DAY_OF_MONTH) == <span style="color: #800080;">1</span><span style="color: #000000;">) {
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;">;
  }
  </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 重构后的代码：提炼函数之后逻辑更加清晰</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> invest(<span style="color: #0000ff;">long</span> userId, <span style="color: #0000ff;">long</span><span style="color: #000000;"> financialProductId) {
  </span><span style="color: #0000ff;">if</span> (isLastDayOfMonth(<span style="color: #0000ff;">new</span><span style="color: #000000;"> Date())) {
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;">;
  }
  </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">}

</span><span style="color: #008000;">//</span><span style="color: #008000;">判断今天是不是当月的最后一天</span>
<span style="color: #0000ff;">public</span><span style="color: #000000;"> boolean isLastDayOfMonth(Date date) {
  Calendar calendar </span>=<span style="color: #000000;"> Calendar.getInstance();
  calendar.setTime(date);
  calendar.</span><span style="color: #0000ff;">set</span>(Calendar.DATE, (calendar.<span style="color: #0000ff;">get</span>(Calendar.DATE) + <span style="color: #800080;">1</span><span style="color: #000000;">));
  </span><span style="color: #0000ff;">if</span> (calendar.<span style="color: #0000ff;">get</span>(Calendar.DAY_OF_MONTH) == <span style="color: #800080;">1</span><span style="color: #000000;">) {
   </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">true</span><span style="color: #000000;">;
  }
  </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">false</span><span style="color: #000000;">;
}</span></pre>
</div>
<span class="cnblogs_code_collapse">把代码分割成更小的单元块</span></div>
<p>②避免函数参数过多</p>
<p>函数包含 3、4 个参数的时候还是能接受的，大于等于 5 个的时候，我们就觉得参数有点过多了，会影响到代码的可读性，使用起来也不方便</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('6990be1f-e1e5-41f2-9868-34e5f39beb13')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_6990be1f-e1e5-41f2-9868-34e5f39beb13" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_6990be1f-e1e5-41f2-9868-34e5f39beb13" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_6990be1f-e1e5-41f2-9868-34e5f39beb13" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span><span style="color: #000000;"> User getUser(String username, String telephone, String email);

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 拆分成多个函数</span>
<span style="color: #0000ff;">public</span><span style="color: #000000;"> User getUserByUsername(String username);
</span><span style="color: #0000ff;">public</span><span style="color: #000000;"> User getUserByTelephone(String telephone);
</span><span style="color: #0000ff;">public</span> User getUserByEmail(String email);</pre>
</div>
<span class="cnblogs_code_collapse">考虑函数是否职责单一，是否能通过拆分成多个函数的方式来减少参数</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('d8875bbd-ebee-401d-95da-6ed36a7b5ff1')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_d8875bbd-ebee-401d-95da-6ed36a7b5ff1" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_d8875bbd-ebee-401d-95da-6ed36a7b5ff1" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_d8875bbd-ebee-401d-95da-6ed36a7b5ff1" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> postBlog(String title, String summary, String keywords, String content, String category, <span style="color: #0000ff;">long</span><span style="color: #000000;"> authorId);

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 将参数封装成对象</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Blog {
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> String title;
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> String summary;
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> String keywords;
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> Strint content;
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> String category;
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">long</span><span style="color: #000000;"> authorId;
}
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> postBlog(Blog blog);</pre>
</div>
<span class="cnblogs_code_collapse">将函数的参数封装成对象</span></div>
<p>③勿用函数参数来控制逻辑</p>
<p>不要在函数中使用布尔类型的标识参数来控制内部逻辑，true 的时候走这块逻辑，false 的时候走另一块逻辑。这明显违背了单一职责原则和接口隔离原则。我建议将其拆成两个函数，可读性上也要更好</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('848863b5-9669-428a-834e-efabd9762ae2')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_848863b5-9669-428a-834e-efabd9762ae2" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_848863b5-9669-428a-834e-efabd9762ae2" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_848863b5-9669-428a-834e-efabd9762ae2" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> buyCourse(<span style="color: #0000ff;">long</span> userId, <span style="color: #0000ff;">long</span><span style="color: #000000;"> courseId, boolean isVip);

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 将其拆分成两个函数</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> buyCourse(<span style="color: #0000ff;">long</span> userId, <span style="color: #0000ff;">long</span><span style="color: #000000;"> courseId);
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> buyCourseForVip(<span style="color: #0000ff;">long</span> userId, <span style="color: #0000ff;">long</span> courseId);</pre>
</div>
<span class="cnblogs_code_collapse">示例1</span></div>
<p>不过，如果函数是 private 私有函数，影响范围有限，或者拆分之后的两个函数经常同时被调用，我们可以酌情考虑保留标识参数。</p>
<p>④函数设计要职责单一</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('9e8faa6d-20bb-4e3f-a1bf-d9fee8d0113b')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_9e8faa6d-20bb-4e3f-a1bf-d9fee8d0113b" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_9e8faa6d-20bb-4e3f-a1bf-d9fee8d0113b" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_9e8faa6d-20bb-4e3f-a1bf-d9fee8d0113b" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span><span style="color: #000000;"> boolean checkUserIfExisting(String telephone, String username, String email)  { 
  </span><span style="color: #0000ff;">if</span> (!<span style="color: #000000;">StringUtils.isBlank(telephone)) {
    User user </span>=<span style="color: #000000;"> userRepo.selectUserByTelephone(telephone);
    </span><span style="color: #0000ff;">return</span> user != <span style="color: #0000ff;">null</span><span style="color: #000000;">;
  }
  
  </span><span style="color: #0000ff;">if</span> (!<span style="color: #000000;">StringUtils.isBlank(username)) {
    User user </span>=<span style="color: #000000;"> userRepo.selectUserByUsername(username);
    </span><span style="color: #0000ff;">return</span> user != <span style="color: #0000ff;">null</span><span style="color: #000000;">;
  }
  
  </span><span style="color: #0000ff;">if</span> (!<span style="color: #000000;">StringUtils.isBlank(email)) {
    User user </span>=<span style="color: #000000;"> userRepo.selectUserByEmail(email);
    </span><span style="color: #0000ff;">return</span> user != <span style="color: #0000ff;">null</span><span style="color: #000000;">;
  }
  
  </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">false</span><span style="color: #000000;">;
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 拆分成三个函数</span>
<span style="color: #0000ff;">public</span><span style="color: #000000;"> boolean checkUserIfExistingByTelephone(String telephone);
</span><span style="color: #0000ff;">public</span><span style="color: #000000;"> boolean checkUserIfExistingByUsername(String username);
</span><span style="color: #0000ff;">public</span> boolean checkUserIfExistingByEmail(String email);</pre>
</div>
<span class="cnblogs_code_collapse">示例1</span></div>
<p>⑤移除过深的嵌套层次</p>
<p>代码嵌套层次过深往往是因为 if-else、switch-case、for 循环过度嵌套导致的。我个人建议，嵌套最好不超过两层，超过两层之后就要思考一下是否可以减少嵌套</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('b28fc594-ec8f-493e-83c9-5ac2b135f6ad')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_b28fc594-ec8f-493e-83c9-5ac2b135f6ad" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_b28fc594-ec8f-493e-83c9-5ac2b135f6ad" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_b28fc594-ec8f-493e-83c9-5ac2b135f6ad" class="cnblogs_code_hide">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> 示例一</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">double</span> caculateTotalAmount(List&lt;Order&gt;<span style="color: #000000;"> orders) {
  </span><span style="color: #0000ff;">if</span> (orders == <span style="color: #0000ff;">null</span> ||<span style="color: #000000;"> orders.isEmpty()) {
    </span><span style="color: #0000ff;">return</span> <span style="color: #800080;">0.0</span><span style="color: #000000;">;
  } </span><span style="color: #0000ff;">else</span> { <span style="color: #008000;">//</span><span style="color: #008000;"> 此处的else可以去掉</span>
    <span style="color: #0000ff;">double</span> amount = <span style="color: #800080;">0.0</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> (Order order : orders) {
      </span><span style="color: #0000ff;">if</span> (order != <span style="color: #0000ff;">null</span><span style="color: #000000;">) {
        amount </span>+= (order.getCount() *<span style="color: #000000;"> order.getPrice());
      }
    }
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> amount;
  }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 示例二</span>
<span style="color: #0000ff;">public</span> List&lt;String&gt; matchStrings(List&lt;String&gt;<span style="color: #000000;"> strList,String substr) {
  List</span>&lt;String&gt; matchedStrings = <span style="color: #0000ff;">new</span> ArrayList&lt;&gt;<span style="color: #000000;">();
  </span><span style="color: #0000ff;">if</span> (strList != <span style="color: #0000ff;">null</span> &amp;&amp; substr != <span style="color: #0000ff;">null</span><span style="color: #000000;">) {
    </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> (String str : strList) {
      </span><span style="color: #0000ff;">if</span> (str != <span style="color: #0000ff;">null</span>) { <span style="color: #008000;">//</span><span style="color: #008000;"> 跟下面的if语句可以合并在一起</span>
        <span style="color: #0000ff;">if</span><span style="color: #000000;"> (str.contains(substr)) {
          matchedStrings.add(str);
        }
      }
    }
  }
  </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> matchedStrings;
}</span></pre>
</div>
<span class="cnblogs_code_collapse">去掉多余的 if 或 else 语句</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('fed680e8-6a77-4a80-8501-3bb8e0b7049e')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_fed680e8-6a77-4a80-8501-3bb8e0b7049e" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_fed680e8-6a77-4a80-8501-3bb8e0b7049e" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_fed680e8-6a77-4a80-8501-3bb8e0b7049e" class="cnblogs_code_hide">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> 重构前的代码</span>
<span style="color: #0000ff;">public</span> List&lt;String&gt; matchStrings(List&lt;String&gt;<span style="color: #000000;"> strList,String substr) {
  List</span>&lt;String&gt; matchedStrings = <span style="color: #0000ff;">new</span> ArrayList&lt;&gt;<span style="color: #000000;">();
  </span><span style="color: #0000ff;">if</span> (strList != <span style="color: #0000ff;">null</span> &amp;&amp; substr != <span style="color: #0000ff;">null</span><span style="color: #000000;">){ 
    </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> (String str : strList) {
      </span><span style="color: #0000ff;">if</span> (str != <span style="color: #0000ff;">null</span> &amp;&amp;<span style="color: #000000;"> str.contains(substr)) {
        matchedStrings.add(str);
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 此处还有10行代码...</span>
<span style="color: #000000;">      }
    }
  }
  </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> matchedStrings;
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 重构后的代码：使用continue提前退出</span>
<span style="color: #0000ff;">public</span> List&lt;String&gt; matchStrings(List&lt;String&gt;<span style="color: #000000;"> strList,String substr) {
  List</span>&lt;String&gt; matchedStrings = <span style="color: #0000ff;">new</span> ArrayList&lt;&gt;<span style="color: #000000;">();
  </span><span style="color: #0000ff;">if</span> (strList != <span style="color: #0000ff;">null</span> &amp;&amp; substr != <span style="color: #0000ff;">null</span><span style="color: #000000;">){ 
    </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> (String str : strList) {
      </span><span style="color: #0000ff;">if</span> (str == <span style="color: #0000ff;">null</span> || !<span style="color: #000000;">str.contains(substr)) {
        </span><span style="color: #0000ff;">continue</span><span style="color: #000000;">; 
      }
      matchedStrings.add(str);
      </span><span style="color: #008000;">//</span><span style="color: #008000;"> 此处还有10行代码...</span>
<span style="color: #000000;">    }
  }
  </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> matchedStrings;
}</span></pre>
</div>
<span class="cnblogs_code_collapse">使用编程语言提供的 continue、break、return 关键字，提前退出嵌套</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('59e47624-02e7-4428-8127-6312a75cacdc')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_59e47624-02e7-4428-8127-6312a75cacdc" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_59e47624-02e7-4428-8127-6312a75cacdc" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_59e47624-02e7-4428-8127-6312a75cacdc" class="cnblogs_code_hide">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> 重构前的代码</span>
<span style="color: #0000ff;">public</span> List&lt;String&gt; matchStrings(List&lt;String&gt;<span style="color: #000000;"> strList,String substr) {
  List</span>&lt;String&gt; matchedStrings = <span style="color: #0000ff;">new</span> ArrayList&lt;&gt;<span style="color: #000000;">();
  </span><span style="color: #0000ff;">if</span> (strList != <span style="color: #0000ff;">null</span> &amp;&amp; substr != <span style="color: #0000ff;">null</span><span style="color: #000000;">) {
    </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> (String str : strList) {
      </span><span style="color: #0000ff;">if</span> (str != <span style="color: #0000ff;">null</span><span style="color: #000000;">) {
        </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (str.contains(substr)) {
          matchedStrings.add(str);
        }
      }
    }
  }
  </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> matchedStrings;
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 重构后的代码：先执行判空逻辑，再执行正常逻辑</span>
<span style="color: #0000ff;">public</span> List&lt;String&gt; matchStrings(List&lt;String&gt;<span style="color: #000000;"> strList,String substr) {
  </span><span style="color: #0000ff;">if</span> (strList == <span style="color: #0000ff;">null</span> || substr == <span style="color: #0000ff;">null</span>) { <span style="color: #008000;">//</span><span style="color: #008000;">先判空</span>
    <span style="color: #0000ff;">return</span><span style="color: #000000;"> Collections.emptyList();
  }

  List</span>&lt;String&gt; matchedStrings = <span style="color: #0000ff;">new</span> ArrayList&lt;&gt;<span style="color: #000000;">();
  </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> (String str : strList) {
    </span><span style="color: #0000ff;">if</span> (str != <span style="color: #0000ff;">null</span><span style="color: #000000;">) {
      </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (str.contains(substr)) {
        matchedStrings.add(str);
      }
    }
  }
  </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> matchedStrings;
}</span></pre>
</div>
<span class="cnblogs_code_collapse">调整执行顺序来减少嵌套</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('ad44a9f3-933e-4676-b16e-19e87c4dfe66')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_ad44a9f3-933e-4676-b16e-19e87c4dfe66" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_ad44a9f3-933e-4676-b16e-19e87c4dfe66" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_ad44a9f3-933e-4676-b16e-19e87c4dfe66" class="cnblogs_code_hide">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> 重构前的代码</span>
<span style="color: #0000ff;">public</span> List&lt;String&gt; appendSalts(List&lt;String&gt;<span style="color: #000000;"> passwords) {
  </span><span style="color: #0000ff;">if</span> (passwords == <span style="color: #0000ff;">null</span> ||<span style="color: #000000;"> passwords.isEmpty()) {
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> Collections.emptyList();
  }
  
  List</span>&lt;String&gt; passwordsWithSalt = <span style="color: #0000ff;">new</span> ArrayList&lt;&gt;<span style="color: #000000;">();
  </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> (String password : passwords) {
    </span><span style="color: #0000ff;">if</span> (password == <span style="color: #0000ff;">null</span><span style="color: #000000;">) {
      </span><span style="color: #0000ff;">continue</span><span style="color: #000000;">;
    }
    </span><span style="color: #0000ff;">if</span> (password.length() &lt; <span style="color: #800080;">8</span><span style="color: #000000;">) {
      </span><span style="color: #008000;">//</span><span style="color: #008000;"> ...</span>
    } <span style="color: #0000ff;">else</span><span style="color: #000000;"> {
      </span><span style="color: #008000;">//</span><span style="color: #008000;"> ...</span>
<span style="color: #000000;">    }
  }
  </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> passwordsWithSalt;
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 重构后的代码：将部分逻辑抽成函数</span>
<span style="color: #0000ff;">public</span> List&lt;String&gt; appendSalts(List&lt;String&gt;<span style="color: #000000;"> passwords) {
  </span><span style="color: #0000ff;">if</span> (passwords == <span style="color: #0000ff;">null</span> ||<span style="color: #000000;"> passwords.isEmpty()) {
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> Collections.emptyList();
  }

  List</span>&lt;String&gt; passwordsWithSalt = <span style="color: #0000ff;">new</span> ArrayList&lt;&gt;<span style="color: #000000;">();
  </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> (String password : passwords) {
    </span><span style="color: #0000ff;">if</span> (password == <span style="color: #0000ff;">null</span><span style="color: #000000;">) {
      </span><span style="color: #0000ff;">continue</span><span style="color: #000000;">;
    }
    passwordsWithSalt.add(appendSalt(password));
  }
  </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> passwordsWithSalt;
}

</span><span style="color: #0000ff;">private</span><span style="color: #000000;"> String appendSalt(String password) {
  String passwordWithSalt </span>=<span style="color: #000000;"> password;
  </span><span style="color: #0000ff;">if</span> (password.length() &lt; <span style="color: #800080;">8</span><span style="color: #000000;">) {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> ...</span>
  } <span style="color: #0000ff;">else</span><span style="color: #000000;"> {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> ...</span>
<span style="color: #000000;">  }
  </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> passwordWithSalt;
}</span></pre>
</div>
<span class="cnblogs_code_collapse">将部分嵌套逻辑封装成函数调用，以此来减少嵌套</span></div>
<p>⑥学会使用解释性变量</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('a4e50f28-6342-45b1-a02b-9f803d7d0782')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_a4e50f28-6342-45b1-a02b-9f803d7d0782" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_a4e50f28-6342-45b1-a02b-9f803d7d0782" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_a4e50f28-6342-45b1-a02b-9f803d7d0782" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">double</span> CalculateCircularArea(<span style="color: #0000ff;">double</span><span style="color: #000000;"> radius) {
  </span><span style="color: #0000ff;">return</span> (<span style="color: #800080;">3.1415</span>) * radius *<span style="color: #000000;"> radius;
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 常量替代魔法数字</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> final Double PI = <span style="color: #800080;">3.1415</span><span style="color: #000000;">;
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">double</span> CalculateCircularArea(<span style="color: #0000ff;">double</span><span style="color: #000000;"> radius) {
  </span><span style="color: #0000ff;">return</span> PI * radius *<span style="color: #000000;"> radius;
}</span></pre>
</div>
<span class="cnblogs_code_collapse">常量取代魔法数字</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('a0c5b150-5d5d-4832-95f2-193ad761520e')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_a0c5b150-5d5d-4832-95f2-193ad761520e" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_a0c5b150-5d5d-4832-95f2-193ad761520e" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_a0c5b150-5d5d-4832-95f2-193ad761520e" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">if</span> (date.after(SUMMER_START) &amp;&amp;<span style="color: #000000;"> date.before(SUMMER_END)) {
  </span><span style="color: #008000;">//</span><span style="color: #008000;"> ...</span>
} <span style="color: #0000ff;">else</span><span style="color: #000000;"> {
  </span><span style="color: #008000;">//</span><span style="color: #008000;"> ...</span>
<span style="color: #000000;">}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 引入解释性变量后逻辑更加清晰</span>
boolean isSummer = date.after(SUMMER_START)&amp;&amp;<span style="color: #000000;">date.before(SUMMER_END);
</span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (isSummer) {
  </span><span style="color: #008000;">//</span><span style="color: #008000;"> ...</span>
} <span style="color: #0000ff;">else</span><span style="color: #000000;"> {
  </span><span style="color: #008000;">//</span><span style="color: #008000;"> ...</span>
} </pre>
</div>
<span class="cnblogs_code_collapse">使用解释性变量来解释复杂表达式</span></div>
<p>&nbsp;</p>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">11，如何发现质量问题</span></strong></span></p>
<p>①常规checklist</p>
<p>目录设置是否齐全、模块划分是否清晰、代码结构是否满足&ldquo;高内聚、松耦合&rdquo;？</p>
<p>是否遵循经典的设计原则和设计思想（SLOID、DRY、KISS、YAGIN、LOD等）？</p>
<p>设计模式是否应用得当？是否有过度设计？</p>
<p>代码是否容易扩展？如果要添加新的功能，是否容易实现？</p>
<p>代码是否可以复用？是否可以复用已有的项目或类库？是否有重复造轮子？</p>
<p>代码是否容易测试？单元测试是否全面覆盖各种正常和异常的情况？</p>
<p>代码是否易读？是否符合编程规范（比如命名和注释是否恰当、代码风格是否一致等）？</p>
<p>②业务需求checklist</p>
<p>代码是否实现了预期的业务需求？</p>
<p>逻辑是否正确？是否处理了各种异常情况？</p>
<p>日志打印是否得当？是否方面debug排查问题？</p>
<p>接口是否易用？是否支持幂等、事务等？</p>
<p>代码是够存在并发问题？是否线程安全？</p>
<p>性能是否有优化空间，比如，SQL、算法是否可以优化？</p>
<p>是否有安全漏洞？比如，输入输出校验是否全面？</p>
<p>&nbsp;</p>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">12，代码重构</span></strong></span></p>
<p>第一轮重构：提高代码的可读性</p>
<p>第二轮重构：提高代码的可测试性</p>
<p>第三轮重构：编写完善的单元测试</p>
<p>第四轮重构：所有重构完成之后添加注释　</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('6131b453-743f-4f06-a8f6-e4e6f78345e6')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_6131b453-743f-4f06-a8f6-e4e6f78345e6" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_6131b453-743f-4f06-a8f6-e4e6f78345e6" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_6131b453-743f-4f06-a8f6-e4e6f78345e6" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> IdGenerator {
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> final Logger logger = LoggerFactory.getLogger(IdGenerator.<span style="color: #0000ff;">class</span><span style="color: #000000;">);

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> String generate() {
    String id </span>= <span style="color: #800000;">""</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">try</span><span style="color: #000000;"> {
      String hostName </span>=<span style="color: #000000;"> InetAddress.getLocalHost().getHostName();
      String[] tokens </span>= hostName.split(<span style="color: #800000;">"</span><span style="color: #800000;">\\.</span><span style="color: #800000;">"</span><span style="color: #000000;">);
      </span><span style="color: #0000ff;">if</span> (tokens.length &gt; <span style="color: #800080;">0</span><span style="color: #000000;">) {
        hostName </span>= tokens[tokens.length - <span style="color: #800080;">1</span><span style="color: #000000;">];
      }
      </span><span style="color: #0000ff;">char</span>[] randomChars = <span style="color: #0000ff;">new</span> <span style="color: #0000ff;">char</span>[<span style="color: #800080;">8</span><span style="color: #000000;">];
      </span><span style="color: #0000ff;">int</span> count = <span style="color: #800080;">0</span><span style="color: #000000;">;
      Random random </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> Random();
      </span><span style="color: #0000ff;">while</span> (count &lt; <span style="color: #800080;">8</span><span style="color: #000000;">) {
        </span><span style="color: #0000ff;">int</span> randomAscii = random.nextInt(<span style="color: #800080;">122</span><span style="color: #000000;">);
        </span><span style="color: #0000ff;">if</span> (randomAscii &gt;= <span style="color: #800080;">48</span> &amp;&amp; randomAscii &lt;= <span style="color: #800080;">57</span><span style="color: #000000;">) {
          randomChars[count] </span>= (<span style="color: #0000ff;">char</span>)(<span style="color: #800000;">'</span><span style="color: #800000;">0</span><span style="color: #800000;">'</span> + (randomAscii - <span style="color: #800080;">48</span><span style="color: #000000;">));
          count</span>++<span style="color: #000000;">;
        } </span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span> (randomAscii &gt;= <span style="color: #800080;">65</span> &amp;&amp; randomAscii &lt;= <span style="color: #800080;">90</span><span style="color: #000000;">) {
          randomChars[count] </span>= (<span style="color: #0000ff;">char</span>)(<span style="color: #800000;">'</span><span style="color: #800000;">A</span><span style="color: #800000;">'</span> + (randomAscii - <span style="color: #800080;">65</span><span style="color: #000000;">));
          count</span>++<span style="color: #000000;">;
        } </span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span> (randomAscii &gt;= <span style="color: #800080;">97</span> &amp;&amp; randomAscii &lt;= <span style="color: #800080;">122</span><span style="color: #000000;">) {
          randomChars[count] </span>= (<span style="color: #0000ff;">char</span>)(<span style="color: #800000;">'</span><span style="color: #800000;">a</span><span style="color: #800000;">'</span> + (randomAscii - <span style="color: #800080;">97</span><span style="color: #000000;">));
          count</span>++<span style="color: #000000;">;
        }
      }
      id </span>= String.format(<span style="color: #800000;">"</span><span style="color: #800000;">%s-%d-%s</span><span style="color: #800000;">"</span><span style="color: #000000;">, hostName,
              System.currentTimeMillis(), </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> String(randomChars));
    } </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (UnknownHostException e) {
      logger.warn(</span><span style="color: #800000;">"</span><span style="color: #800000;">Failed to get the host name.</span><span style="color: #800000;">"</span><span style="color: #000000;">, e);
    }

    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> id;
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">原始代码</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('49b88e65-ba63-430c-a56a-a9cc4562d593')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_49b88e65-ba63-430c-a56a-a9cc4562d593" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_49b88e65-ba63-430c-a56a-a9cc4562d593" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_49b88e65-ba63-430c-a56a-a9cc4562d593" class="cnblogs_code_hide">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">hostName 变量不应该被重复使用，尤其当这两次使用时的含义还不同的时候；
</span><span style="color: #008000;">//</span><span style="color: #008000;">将获取 hostName 的代码抽离出来，定义为 getLastfieldOfHostName() 函数；
</span><span style="color: #008000;">//</span><span style="color: #008000;">删除代码中的魔法数，比如，57、90、97、122；
</span><span style="color: #008000;">//</span><span style="color: #008000;">将随机数生成的代码抽离出来，定义为 generateRandomAlphameric() 函数；
</span><span style="color: #008000;">//</span><span style="color: #008000;">generate() 函数中的三个 if 逻辑重复了，且实现过于复杂，我们要对其进行简化；
</span><span style="color: #008000;">//</span><span style="color: #008000;"> 对 IdGenerator 类重命名，并且抽象出对应的接口</span>

<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IdGenerator {
  String generate();
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> LogTraceIdGenerator extends IdGenerator {
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> RandomIdGenerator implements IdGenerator {
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> final Logger logger = LoggerFactory.getLogger(RandomIdGenerator.<span style="color: #0000ff;">class</span><span style="color: #000000;">);

  @Override
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> String generate() {
    String substrOfHostName </span>=<span style="color: #000000;"> getLastfieldOfHostName();
    </span><span style="color: #0000ff;">long</span> currentTimeMillis =<span style="color: #000000;"> System.currentTimeMillis();
    String randomString </span>= generateRandomAlphameric(<span style="color: #800080;">8</span><span style="color: #000000;">);
    String id </span>= String.format(<span style="color: #800000;">"</span><span style="color: #800000;">%s-%d-%s</span><span style="color: #800000;">"</span><span style="color: #000000;">,
            substrOfHostName, currentTimeMillis, randomString);
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> id;
  }

  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> String getLastfieldOfHostName() {
    String substrOfHostName </span>= <span style="color: #0000ff;">null</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">try</span><span style="color: #000000;"> {
      String hostName </span>=<span style="color: #000000;"> InetAddress.getLocalHost().getHostName();
      String[] tokens </span>= hostName.split(<span style="color: #800000;">"</span><span style="color: #800000;">\\.</span><span style="color: #800000;">"</span><span style="color: #000000;">);
      substrOfHostName </span>= tokens[tokens.length - <span style="color: #800080;">1</span><span style="color: #000000;">];
      </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> substrOfHostName;
    } </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (UnknownHostException e) {
      logger.warn(</span><span style="color: #800000;">"</span><span style="color: #800000;">Failed to get the host name.</span><span style="color: #800000;">"</span><span style="color: #000000;">, e);
    }
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> substrOfHostName;
  }

  </span><span style="color: #0000ff;">private</span> String generateRandomAlphameric(<span style="color: #0000ff;">int</span><span style="color: #000000;"> length) {
    </span><span style="color: #0000ff;">char</span>[] randomChars = <span style="color: #0000ff;">new</span> <span style="color: #0000ff;">char</span><span style="color: #000000;">[length];
    </span><span style="color: #0000ff;">int</span> count = <span style="color: #800080;">0</span><span style="color: #000000;">;
    Random random </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> Random();
    </span><span style="color: #0000ff;">while</span> (count &lt;<span style="color: #000000;"> length) {
      </span><span style="color: #0000ff;">int</span> maxAscii = <span style="color: #800000;">'</span><span style="color: #800000;">z</span><span style="color: #800000;">'</span><span style="color: #000000;">;
      </span><span style="color: #0000ff;">int</span> randomAscii =<span style="color: #000000;"> random.nextInt(maxAscii);
      boolean isDigit</span>= randomAscii &gt;= <span style="color: #800000;">'</span><span style="color: #800000;">0</span><span style="color: #800000;">'</span> &amp;&amp; randomAscii &lt;= <span style="color: #800000;">'</span><span style="color: #800000;">9</span><span style="color: #800000;">'</span><span style="color: #000000;">;
      boolean isUppercase</span>= randomAscii &gt;= <span style="color: #800000;">'</span><span style="color: #800000;">A</span><span style="color: #800000;">'</span> &amp;&amp; randomAscii &lt;= <span style="color: #800000;">'</span><span style="color: #800000;">Z</span><span style="color: #800000;">'</span><span style="color: #000000;">;
      boolean isLowercase</span>= randomAscii &gt;= <span style="color: #800000;">'</span><span style="color: #800000;">a</span><span style="color: #800000;">'</span> &amp;&amp; randomAscii &lt;= <span style="color: #800000;">'</span><span style="color: #800000;">z</span><span style="color: #800000;">'</span><span style="color: #000000;">;
      </span><span style="color: #0000ff;">if</span> (isDigit|| isUppercase ||<span style="color: #000000;"> isLowercase) {
        randomChars[count] </span>= (<span style="color: #0000ff;">char</span><span style="color: #000000;">) (randomAscii);
        </span>++<span style="color: #000000;">count;
      }
    }
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> String(randomChars);
  }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">代码使用举例</span>
LogTraceIdGenerator logTraceIdGenerator = <span style="color: #0000ff;">new</span> RandomIdGenerator();</pre>
</div>
<span class="cnblogs_code_collapse">第一轮重构</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('c2b37995-a00b-43f1-8d4c-1c0baaa0cf61')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_c2b37995-a00b-43f1-8d4c-1c0baaa0cf61" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_c2b37995-a00b-43f1-8d4c-1c0baaa0cf61" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_c2b37995-a00b-43f1-8d4c-1c0baaa0cf61" class="cnblogs_code_hide">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">generate() 函数定义为静态函数，会影响使用该函数的代码的可测试性；
</span><span style="color: #008000;">//</span><span style="color: #008000;">generate() 函数的代码实现依赖运行环境（本机名）、时间函数、随机函数，所以 generate() 函数本身的可测试性也不好
</span><span style="color: #008000;">//</span><span style="color: #008000;">从 getLastfieldOfHostName() 函数中，将逻辑比较复杂的那部分代码剥离出来，定义为 getLastSubstrSplittedByDot() 函数。因为 getLastfieldOfHostName() 函数依赖本地主机名，所以，剥离出主要代码之后这个函数变得非常简单，可以不用测试。我们重点测试 getLastSubstrSplittedByDot() 函数即可。
</span><span style="color: #008000;">//</span><span style="color: #008000;">将 generateRandomAlphameric() 和 getLastSubstrSplittedByDot() 这两个函数的访问权限设置为 protected。这样做的目的是，可以直接在单元测试中通过对象来调用两个函数进行测试
</span><span style="color: #008000;">//</span><span style="color: #008000;">给 generateRandomAlphameric() 和 getLastSubstrSplittedByDot() 两个函数添加 Google Guava 的 annotation @VisibleForTesting。这个 annotation 没有任何实际的作用，只起到标识的作用，告诉其他人说，这两个函数本该是 private 访问权限的，之所以提升访问权限到 protected，只是为了测试，只能用于单元测试中</span>

<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> RandomIdGenerator implements IdGenerator {
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> final Logger logger = LoggerFactory.getLogger(RandomIdGenerator.<span style="color: #0000ff;">class</span><span style="color: #000000;">);

  @Override
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> String generate() {
    String substrOfHostName </span>=<span style="color: #000000;"> getLastfieldOfHostName();
    </span><span style="color: #0000ff;">long</span> currentTimeMillis =<span style="color: #000000;"> System.currentTimeMillis();
    String randomString </span>= generateRandomAlphameric(<span style="color: #800080;">8</span><span style="color: #000000;">);
    String id </span>= String.format(<span style="color: #800000;">"</span><span style="color: #800000;">%s-%d-%s</span><span style="color: #800000;">"</span><span style="color: #000000;">,
            substrOfHostName, currentTimeMillis, randomString);
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> id;
  }

  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> String getLastfieldOfHostName() {
    String substrOfHostName </span>= <span style="color: #0000ff;">null</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">try</span><span style="color: #000000;"> {
      String hostName </span>=<span style="color: #000000;"> InetAddress.getLocalHost().getHostName();
      substrOfHostName </span>=<span style="color: #000000;"> getLastSubstrSplittedByDot(hostName);
    } </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (UnknownHostException e) {
      logger.warn(</span><span style="color: #800000;">"</span><span style="color: #800000;">Failed to get the host name.</span><span style="color: #800000;">"</span><span style="color: #000000;">, e);
    }
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> substrOfHostName;
  }

  @VisibleForTesting
  </span><span style="color: #0000ff;">protected</span><span style="color: #000000;"> String getLastSubstrSplittedByDot(String hostName) {
    String[] tokens </span>= hostName.split(<span style="color: #800000;">"</span><span style="color: #800000;">\\.</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    String substrOfHostName </span>= tokens[tokens.length - <span style="color: #800080;">1</span><span style="color: #000000;">];
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> substrOfHostName;
  }

  @VisibleForTesting
  </span><span style="color: #0000ff;">protected</span> String generateRandomAlphameric(<span style="color: #0000ff;">int</span><span style="color: #000000;"> length) {
    </span><span style="color: #0000ff;">char</span>[] randomChars = <span style="color: #0000ff;">new</span> <span style="color: #0000ff;">char</span><span style="color: #000000;">[length];
    </span><span style="color: #0000ff;">int</span> count = <span style="color: #800080;">0</span><span style="color: #000000;">;
    Random random </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> Random();
    </span><span style="color: #0000ff;">while</span> (count &lt;<span style="color: #000000;"> length) {
      </span><span style="color: #0000ff;">int</span> maxAscii = <span style="color: #800000;">'</span><span style="color: #800000;">z</span><span style="color: #800000;">'</span><span style="color: #000000;">;
      </span><span style="color: #0000ff;">int</span> randomAscii =<span style="color: #000000;"> random.nextInt(maxAscii);
      boolean isDigit</span>= randomAscii &gt;= <span style="color: #800000;">'</span><span style="color: #800000;">0</span><span style="color: #800000;">'</span> &amp;&amp; randomAscii &lt;= <span style="color: #800000;">'</span><span style="color: #800000;">9</span><span style="color: #800000;">'</span><span style="color: #000000;">;
      boolean isUppercase</span>= randomAscii &gt;= <span style="color: #800000;">'</span><span style="color: #800000;">A</span><span style="color: #800000;">'</span> &amp;&amp; randomAscii &lt;= <span style="color: #800000;">'</span><span style="color: #800000;">Z</span><span style="color: #800000;">'</span><span style="color: #000000;">;
      boolean isLowercase</span>= randomAscii &gt;= <span style="color: #800000;">'</span><span style="color: #800000;">a</span><span style="color: #800000;">'</span> &amp;&amp; randomAscii &lt;= <span style="color: #800000;">'</span><span style="color: #800000;">z</span><span style="color: #800000;">'</span><span style="color: #000000;">;
      </span><span style="color: #0000ff;">if</span> (isDigit|| isUppercase ||<span style="color: #000000;"> isLowercase) {
        randomChars[count] </span>= (<span style="color: #0000ff;">char</span><span style="color: #000000;">) (randomAscii);
        </span>++<span style="color: #000000;">count;
      }
    }
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> String(randomChars);
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">第二轮重构</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('dfaac688-1fad-4e3e-95ec-6de4d027b83c')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_dfaac688-1fad-4e3e-95ec-6de4d027b83c" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_dfaac688-1fad-4e3e-95ec-6de4d027b83c" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_dfaac688-1fad-4e3e-95ec-6de4d027b83c" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> RandomIdGeneratorTest {
  @Test
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> testGetLastSubstrSplittedByDot() {
    RandomIdGenerator idGenerator </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> RandomIdGenerator();
    String actualSubstr </span>= idGenerator.getLastSubstrSplittedByDot(<span style="color: #800000;">"</span><span style="color: #800000;">field1.field2.field3</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    Assert.assertEquals(</span><span style="color: #800000;">"</span><span style="color: #800000;">field3</span><span style="color: #800000;">"</span><span style="color: #000000;">, actualSubstr);

    actualSubstr </span>= idGenerator.getLastSubstrSplittedByDot(<span style="color: #800000;">"</span><span style="color: #800000;">field1</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    Assert.assertEquals(</span><span style="color: #800000;">"</span><span style="color: #800000;">field1</span><span style="color: #800000;">"</span><span style="color: #000000;">, actualSubstr);

    actualSubstr </span>= idGenerator.getLastSubstrSplittedByDot(<span style="color: #800000;">"</span><span style="color: #800000;">field1#field2$field3</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    Assert.assertEquals(</span><span style="color: #800000;">"</span><span style="color: #800000;">field1#field2#field3</span><span style="color: #800000;">"</span><span style="color: #000000;">, actualSubstr);
  }

  </span><span style="color: #008000;">//</span><span style="color: #008000;"> 此单元测试会失败，因为我们在代码中没有处理hostName为null或空字符串的情况
  </span><span style="color: #008000;">//</span><span style="color: #008000;"> 这部分优化留在第36、37节课中讲解</span>
<span style="color: #000000;">  @Test
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> testGetLastSubstrSplittedByDot_nullOrEmpty() {
    RandomIdGenerator idGenerator </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> RandomIdGenerator();
    String actualSubstr </span>= idGenerator.getLastSubstrSplittedByDot(<span style="color: #0000ff;">null</span><span style="color: #000000;">);
    Assert.assertNull(actualSubstr);

    actualSubstr </span>= idGenerator.getLastSubstrSplittedByDot(<span style="color: #800000;">""</span><span style="color: #000000;">);
    Assert.assertEquals(</span><span style="color: #800000;">""</span><span style="color: #000000;">, actualSubstr);
  }

  @Test
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> testGenerateRandomAlphameric() {
    RandomIdGenerator idGenerator </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> RandomIdGenerator();
    String actualRandomString </span>= idGenerator.generateRandomAlphameric(<span style="color: #800080;">6</span><span style="color: #000000;">);
    Assert.assertNotNull(actualRandomString);
    Assert.assertEquals(</span><span style="color: #800080;">6</span><span style="color: #000000;">, actualRandomString.length());
    </span><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">char</span><span style="color: #000000;"> c : actualRandomString.toCharArray()) {
      Assert.assertTrue((</span><span style="color: #800000;">'</span><span style="color: #800000;">0</span><span style="color: #800000;">'</span> &lt; c &amp;&amp; c &gt; <span style="color: #800000;">'</span><span style="color: #800000;">9</span><span style="color: #800000;">'</span>) || (<span style="color: #800000;">'</span><span style="color: #800000;">a</span><span style="color: #800000;">'</span> &lt; c &amp;&amp; c &gt; <span style="color: #800000;">'</span><span style="color: #800000;">z</span><span style="color: #800000;">'</span>) || (<span style="color: #800000;">'</span><span style="color: #800000;">A</span><span style="color: #800000;">'</span> &lt; c &amp;&amp; c &lt; <span style="color: #800000;">'</span><span style="color: #800000;">Z</span><span style="color: #800000;">'</span><span style="color: #000000;">));
    }
  }

  </span><span style="color: #008000;">//</span><span style="color: #008000;"> 此单元测试会失败，因为我们在代码中没有处理length&lt;=0的情况
  </span><span style="color: #008000;">//</span><span style="color: #008000;"> 这部分优化留在第36、37节课中讲解</span>
<span style="color: #000000;">  @Test
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> testGenerateRandomAlphameric_lengthEqualsOrLessThanZero() {
    RandomIdGenerator idGenerator </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> RandomIdGenerator();
    String actualRandomString </span>= idGenerator.generateRandomAlphameric(<span style="color: #800080;">0</span><span style="color: #000000;">);
    Assert.assertEquals(</span><span style="color: #800000;">""</span><span style="color: #000000;">, actualRandomString);

    actualRandomString </span>= idGenerator.generateRandomAlphameric(-<span style="color: #800080;">1</span><span style="color: #000000;">);
    Assert.assertNull(actualRandomString);
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">第三轮重构</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('3bcd52e2-3cae-482f-a168-8b2f66de0cf5')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_3bcd52e2-3cae-482f-a168-8b2f66de0cf5" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_3bcd52e2-3cae-482f-a168-8b2f66de0cf5" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_3bcd52e2-3cae-482f-a168-8b2f66de0cf5" class="cnblogs_code_hide">
<pre><span style="color: #008000;">/*</span><span style="color: #008000;">*
 * 用于生成随机ID的ID生成器
 *
 * &lt;p&gt;
 * 此类生成的ID并非绝对唯一，但是重复的可能性非常低。
 </span><span style="color: #008000;">*/</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> RandomIdGenerator implements IdGenerator {
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> final Logger logger = LoggerFactory.getLogger(RandomIdGenerator.<span style="color: #0000ff;">class</span><span style="color: #000000;">);

  </span><span style="color: #008000;">/*</span><span style="color: #008000;">*
   * 生成随机ID。 这些ID仅在极端情况下可以重复。
   *
   * @返回一个随机ID
   </span><span style="color: #008000;">*/</span><span style="color: #000000;">
  @Override
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> String generate() {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">  }

  </span><span style="color: #008000;">/*</span><span style="color: #008000;">*
   * 获取本地主机名，并提取由定界符&ldquo;.&rdquo;分隔的名称字符串的最后一个字段。
   *
   * @返回主机名的最后一个字段。 如果未获得主机名，则返回null。
   </span><span style="color: #008000;">*/</span>
  <span style="color: #0000ff;">private</span><span style="color: #000000;"> String getLastfieldOfHostName() {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">  }

  </span><span style="color: #008000;">/*</span><span style="color: #008000;">*
   * 获取由定界符&ldquo;.&rdquo;分隔的{@hostName}的最后一个字段。
   *
   * @参数hostName不能为null
   * @90/5000
返回{@hostName}的最后一个字段。 如果{@hostName}为空字符串，则返回空字符串。
   </span><span style="color: #008000;">*/</span><span style="color: #000000;">
  @VisibleForTesting
  </span><span style="color: #0000ff;">protected</span><span style="color: #000000;"> String getLastSubstrSplittedByDot(String hostName) {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">  }

  </span><span style="color: #008000;">/*</span><span style="color: #008000;">*
   * 生成随机字符串
   * 仅包含数字，大写字母和小写字母。
   *
   * @参数长度不应小于0
   * @返回随机字符串。 如果{@length}为0，则返回空字符串
   </span><span style="color: #008000;">*/</span><span style="color: #000000;">
  @VisibleForTesting
  </span><span style="color: #0000ff;">protected</span> String generateRandomAlphameric(<span style="color: #0000ff;">int</span><span style="color: #000000;"> length) {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">第四轮重构</span></div>
<p>&nbsp;</p>
<p><span style="font-size: 16px; color: #ff6600;"><strong>13，函数出错返回什么？NULL、异常、错误码、空对象？</strong></span></p>
<p>①返回错误码</p>
<p>C 语言中没有异常这样的语法机制，因此，返回错误码便是最常用的出错处理方式。而在 Java、Python 等比较新的编程语言中，大部分情况下，我们都用异常来处理函数出错的情况，极少会用到错误码。</p>
<p>如果你熟悉的编程语言中有异常这种语法机制，那就尽量不要使用错误码。异常相对于错误码，有诸多方面的优势，比如可以携带更多的错误信息（exception 中可以有 message、stack trace 等信息）等。</p>
<p>② 返回NULL值</p>
<p>对于以 get、find、select、search、query 等单词开头的查找函数来说，数据不存在，并非一种异常情况，这是一种正常行为。所以，返回代表不存在语义的 NULL 值比返回异常更加合理</p>
<p>③返回空对象</p>
<p>返回 NULL 值有各种弊端，对此有一个比较经典的应对策略，那就是应用空对象设计模式。当函数返回的数据是字符串类型或者集合类型的时候，我们可以用空字符串或空集合替代 NULL 值，来表示不存在的情况。这样，我们在使用函数的时候，就可以不用做 NULL 值判断。</p>
<p>④抛出异常</p>
<p>上层调用方是否关心这个异常。关心就抛出异常，否则就直接吞噬掉。是否需要包装成新的异常抛出，看上层代码是否能理解这个异常、是否业务相关。如果能理解、业务相关就可以直接抛出，否则就封装成新的异常抛出。</p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: #169fe6;"><span style="color: #ffffff;"><strong>五、设计模式与范式：创建型</strong></span></p>
<p><span style="color: #888888; font-size: 12px;">创建型模式主要解决对象的创建问题，封装复杂的创建过程，解耦对象的创建代码和使用代码</span></p>
<p><span style="color: #888888; font-size: 12px;">创建型模式是将创建和使用代码解耦</span></p>
<p><span style="color: #888888; font-size: 12px;">单例模式用来创建全局唯一的对象。</span></p>
<p><span style="color: #888888; font-size: 12px;">工厂模式用来创建不同但是相关类型的对象（继承同一父类或者接口的一组子类），由给定的参数来决定创建哪种类型的对象。</span></p>
<p><span style="color: #888888; font-size: 12px;">建造者模式是用来创建复杂对象，可以通过设置不同的可选参数，&ldquo;定制化&rdquo;地创建不同的对象。</span></p>
<p><span style="color: #888888; font-size: 12px;">原型模式针对创建成本比较大的对象，利用对已有对象进行复制的方式进行创建，以达到节省创建时间的目的。</span></p>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">1，单例模式</span></strong></span></p>
<p>一个类只允许创建一个对象（或者叫实例）&nbsp;</p>
<p>①单例的用途</p>
<p>处理资源访问：</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('6895d9f6-3ead-48d8-8b56-2a2fcee163c1')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_6895d9f6-3ead-48d8-8b56-2a2fcee163c1" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_6895d9f6-3ead-48d8-8b56-2a2fcee163c1" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_6895d9f6-3ead-48d8-8b56-2a2fcee163c1" class="cnblogs_code_hide">
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
}</span></pre>
</div>
<span class="cnblogs_code_collapse">单例模式相对于之前类级别锁的好处是，不用创建那么多 Logger 对象，一方面节省内存空间，另一方面节省系统文件句柄</span></div>
<p>表示全局唯一类：</p>
<p>从业务概念上，如果有些数据在系统中只应保存一份，那就比较适合设计为单例类。比如，配置信息类。在系统中，我们只有一个配置文件，当配置文件被加载到内存之后，以对象的形式存在，也理所应当只有一份。再比如，唯一递增 ID 号码生成器，如果程序中有两个对象，那就会存在生成重复 ID 的情况，所以，我们应该将 ID 生成器类设计为单例。</p>
<p>②如何实现一个单例类</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('722fd9cb-4c47-44f5-ab4a-d1e1e4cb3b0a')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_722fd9cb-4c47-44f5-ab4a-d1e1e4cb3b0a" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_722fd9cb-4c47-44f5-ab4a-d1e1e4cb3b0a" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_722fd9cb-4c47-44f5-ab4a-d1e1e4cb3b0a" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> IdGenerator { 
  </span><span style="color: #0000ff;">private</span> AtomicLong id = <span style="color: #0000ff;">new</span> AtomicLong(<span style="color: #800080;">0</span><span style="color: #000000;">);
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> final IdGenerator instance = <span style="color: #0000ff;">new</span><span style="color: #000000;"> IdGenerator();
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> IdGenerator() {}
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> IdGenerator getInstance() {
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> instance;
  }
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">long</span><span style="color: #000000;"> getId() { 
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> id.incrementAndGet();
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">饿汉式：饿汉式的实现方式比较简单。在类加载的时候，instance 静态实例就已经创建并初始化好了，所以，instance 实例的创建过程是线程安全的</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('5ad30768-9246-4b44-992b-e9b3309898ca')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_5ad30768-9246-4b44-992b-e9b3309898ca" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_5ad30768-9246-4b44-992b-e9b3309898ca" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_5ad30768-9246-4b44-992b-e9b3309898ca" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> IdGenerator { 
  </span><span style="color: #0000ff;">private</span> AtomicLong id = <span style="color: #0000ff;">new</span> AtomicLong(<span style="color: #800080;">0</span><span style="color: #000000;">);
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> IdGenerator instance;
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> IdGenerator() {}
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> synchronized IdGenerator getInstance() {
    </span><span style="color: #0000ff;">if</span> (instance == <span style="color: #0000ff;">null</span><span style="color: #000000;">) {
      instance </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> IdGenerator();
    }
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> instance;
  }
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">long</span><span style="color: #000000;"> getId() { 
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> id.incrementAndGet();
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">懒汉式：懒汉式相对于饿汉式的优势是支持延迟加载。不过懒汉式的缺点也很明显，我们给 getInstance() 这个方法加了一把大锁，导致这个函数的并发度很低</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('74cc998c-b6c1-4cb6-ac3f-f2c02c5a23ad')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_74cc998c-b6c1-4cb6-ac3f-f2c02c5a23ad" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_74cc998c-b6c1-4cb6-ac3f-f2c02c5a23ad" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_74cc998c-b6c1-4cb6-ac3f-f2c02c5a23ad" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> IdGenerator { 
  </span><span style="color: #0000ff;">private</span> AtomicLong id = <span style="color: #0000ff;">new</span> AtomicLong(<span style="color: #800080;">0</span><span style="color: #000000;">);
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> IdGenerator instance;
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> IdGenerator() {}
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> IdGenerator getInstance() {
    </span><span style="color: #0000ff;">if</span> (instance == <span style="color: #0000ff;">null</span><span style="color: #000000;">) {
      synchronized(IdGenerator.</span><span style="color: #0000ff;">class</span>) { <span style="color: #008000;">//</span><span style="color: #008000;"> 此处为类级别的锁</span>
        <span style="color: #0000ff;">if</span> (instance == <span style="color: #0000ff;">null</span><span style="color: #000000;">) {
          instance </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> IdGenerator();
        }
      }
    }
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> instance;
  }
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">long</span><span style="color: #000000;"> getId() { 
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> id.incrementAndGet();
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">双重检测：既支持延迟加载、又支持高并发的单例实现方式，也就是双重检测实现方式。</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('acf86b79-0421-44b2-9aea-6f03abd7b8d6')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_acf86b79-0421-44b2-9aea-6f03abd7b8d6" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_acf86b79-0421-44b2-9aea-6f03abd7b8d6" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_acf86b79-0421-44b2-9aea-6f03abd7b8d6" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> IdGenerator { 
  </span><span style="color: #0000ff;">private</span> AtomicLong id = <span style="color: #0000ff;">new</span> AtomicLong(<span style="color: #800080;">0</span><span style="color: #000000;">);
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> IdGenerator() {}

  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SingletonHolder{
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> final IdGenerator instance = <span style="color: #0000ff;">new</span><span style="color: #000000;"> IdGenerator();
  }
  
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> IdGenerator getInstance() {
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> SingletonHolder.instance;
  }
 
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">long</span><span style="color: #000000;"> getId() { 
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> id.incrementAndGet();
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">静态内部类：比双重检测更加简单的实现方法，那就是利用 静态内部类。它有点类似饿汉式，但又能做到了延迟加载</span></div>
<p>③如何实现线程内唯一单例</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('80cedcd6-358f-4f79-95a2-fe52870091b3')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_80cedcd6-358f-4f79-95a2-fe52870091b3" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_80cedcd6-358f-4f79-95a2-fe52870091b3" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_80cedcd6-358f-4f79-95a2-fe52870091b3" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> IdGenerator {
  </span><span style="color: #0000ff;">private</span> AtomicLong id = <span style="color: #0000ff;">new</span> AtomicLong(<span style="color: #800080;">0</span><span style="color: #000000;">);

  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> final ConcurrentHashMap&lt;Long, IdGenerator&gt;<span style="color: #000000;"> instances
          </span>= <span style="color: #0000ff;">new</span> ConcurrentHashMap&lt;&gt;<span style="color: #000000;">();

  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> IdGenerator() {}

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> IdGenerator getInstance() {
    Long currentThreadId </span>=<span style="color: #000000;"> Thread.currentThread().getId();
    instances.putIfAbsent(currentThreadId, </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> IdGenerator());
    </span><span style="color: #0000ff;">return</span> instances.<span style="color: #0000ff;">get</span><span style="color: #000000;">(currentThreadId);
  }

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">long</span><span style="color: #000000;"> getId() {
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> id.incrementAndGet();
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">通过一个 HashMap 来存储对象，其中 key 是线程 ID，value 是对象</span></div>
<p>④如何实现集群环境下单例</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('76fad7c8-092d-408c-8366-d24bd35b55cb')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_76fad7c8-092d-408c-8366-d24bd35b55cb" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_76fad7c8-092d-408c-8366-d24bd35b55cb" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_76fad7c8-092d-408c-8366-d24bd35b55cb" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> IdGenerator {
  </span><span style="color: #0000ff;">private</span> AtomicLong id = <span style="color: #0000ff;">new</span> AtomicLong(<span style="color: #800080;">0</span><span style="color: #000000;">);
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> IdGenerator instance;
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> SharedObjectStorage storage = FileSharedObjectStorage(<span style="color: #008000;">/*</span><span style="color: #008000;">入参省略，比如文件地址</span><span style="color: #008000;">*/</span><span style="color: #000000;">);
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> DistributedLock <span style="color: #0000ff;">lock</span> = <span style="color: #0000ff;">new</span><span style="color: #000000;"> DistributedLock();
  
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> IdGenerator() {}

  </span><span style="color: #0000ff;">public</span> synchronized <span style="color: #0000ff;">static</span><span style="color: #000000;"> IdGenerator getInstance() 
    </span><span style="color: #0000ff;">if</span> (instance == <span style="color: #0000ff;">null</span><span style="color: #000000;">) {
      </span><span style="color: #0000ff;">lock</span>.<span style="color: #0000ff;">lock</span><span style="color: #000000;">();
      instance </span>= storage.load(IdGenerator.<span style="color: #0000ff;">class</span><span style="color: #000000;">);
    }
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> instance;
  }
  
  </span><span style="color: #0000ff;">public</span> synchroinzed <span style="color: #0000ff;">void</span><span style="color: #000000;"> freeInstance() {
    storage.save(</span><span style="color: #0000ff;">this</span>, IdGeneator.<span style="color: #0000ff;">class</span><span style="color: #000000;">);
    instance </span>= <span style="color: #0000ff;">null</span>; <span style="color: #008000;">//</span><span style="color: #008000;">释放对象</span>
    <span style="color: #0000ff;">lock</span><span style="color: #000000;">.unlock();
  }
  
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">long</span><span style="color: #000000;"> getId() { 
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> id.incrementAndGet();
  }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> IdGenerator使用举例</span>
IdGenerator idGeneator =<span style="color: #000000;"> IdGenerator.getInstance();
</span><span style="color: #0000ff;">long</span> id =<span style="color: #000000;"> idGenerator.getId();
IdGenerator.freeInstance();</span></pre>
</div>
<span class="cnblogs_code_collapse">需要把这个单例对象序列化并存储到外部共享存储区（比如文件）。进程在使用这个单例对象的时候，需要先从外部共享存储区中将它读取到内存，并反序列化成对象，然后再使用，使用完成之后还需要再存储回外部共享存储区</span></div>
<p>⑤如何实现一个多例模式</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('c8412d27-0b17-4a9c-b917-224ba8943738')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_c8412d27-0b17-4a9c-b917-224ba8943738" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_c8412d27-0b17-4a9c-b917-224ba8943738" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_c8412d27-0b17-4a9c-b917-224ba8943738" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> BackendServer {
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">long</span><span style="color: #000000;"> serverNo;
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> String serverAddress;

  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> final <span style="color: #0000ff;">int</span> SERVER_COUNT = <span style="color: #800080;">3</span><span style="color: #000000;">;
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> final Map&lt;Long, BackendServer&gt; serverInstances = <span style="color: #0000ff;">new</span> HashMap&lt;&gt;<span style="color: #000000;">();

  </span><span style="color: #0000ff;">static</span><span style="color: #000000;"> {
    serverInstances.put(</span><span style="color: #800080;">1L</span>, <span style="color: #0000ff;">new</span> BackendServer(<span style="color: #800080;">1L</span>, <span style="color: #800000;">"</span><span style="color: #800000;">192.134.22.138:8080</span><span style="color: #800000;">"</span><span style="color: #000000;">));
    serverInstances.put(</span><span style="color: #800080;">2L</span>, <span style="color: #0000ff;">new</span> BackendServer(<span style="color: #800080;">2L</span>, <span style="color: #800000;">"</span><span style="color: #800000;">192.134.22.139:8080</span><span style="color: #800000;">"</span><span style="color: #000000;">));
    serverInstances.put(</span><span style="color: #800080;">3L</span>, <span style="color: #0000ff;">new</span> BackendServer(<span style="color: #800080;">3L</span>, <span style="color: #800000;">"</span><span style="color: #800000;">192.134.22.140:8080</span><span style="color: #800000;">"</span><span style="color: #000000;">));
  }

  </span><span style="color: #0000ff;">private</span> BackendServer(<span style="color: #0000ff;">long</span><span style="color: #000000;"> serverNo, String serverAddress) {
    </span><span style="color: #0000ff;">this</span>.serverNo =<span style="color: #000000;"> serverNo;
    </span><span style="color: #0000ff;">this</span>.serverAddress =<span style="color: #000000;"> serverAddress;
  }

  </span><span style="color: #0000ff;">public</span> BackendServer getInstance(<span style="color: #0000ff;">long</span><span style="color: #000000;"> serverNo) {
    </span><span style="color: #0000ff;">return</span> serverInstances.<span style="color: #0000ff;">get</span><span style="color: #000000;">(serverNo);
  }

  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> BackendServer getRandomInstance() {
    Random r </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> Random();
    </span><span style="color: #0000ff;">int</span> no = r.nextInt(SERVER_COUNT)+<span style="color: #800080;">1</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">return</span> serverInstances.<span style="color: #0000ff;">get</span><span style="color: #000000;">(no);
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">一个类可以创建多个对象，但是个数是有限制的，比如只能创建 3 个对象</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('89d9df9a-18d7-424d-867f-f0f509c52cff')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_89d9df9a-18d7-424d-867f-f0f509c52cff" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_89d9df9a-18d7-424d-867f-f0f509c52cff" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_89d9df9a-18d7-424d-867f-f0f509c52cff" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Logger {
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> final ConcurrentHashMap&lt;String, Logger&gt;<span style="color: #000000;"> instances
          </span>= <span style="color: #0000ff;">new</span> ConcurrentHashMap&lt;&gt;<span style="color: #000000;">();

  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> Logger() {}

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> Logger getInstance(String loggerName) {
    instances.putIfAbsent(loggerName, </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> Logger());
    </span><span style="color: #0000ff;">return</span> instances.<span style="color: #0000ff;">get</span><span style="color: #000000;">(loggerName);
  }

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> log() {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">  }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">l1==l2, l1!=l3</span>
Logger l1 = Logger.getInstance(<span style="color: #800000;">"</span><span style="color: #800000;">User.class</span><span style="color: #800000;">"</span><span style="color: #000000;">);
Logger l2 </span>= Logger.getInstance(<span style="color: #800000;">"</span><span style="color: #800000;">User.class</span><span style="color: #800000;">"</span><span style="color: #000000;">);
Logger l3 </span>= Logger.getInstance(<span style="color: #800000;">"</span><span style="color: #800000;">Order.class</span><span style="color: #800000;">"</span>);</pre>
</div>
<span class="cnblogs_code_collapse">logger name 就是刚刚说的&ldquo;类型&rdquo;，同一个 logger name 获取到的对象实例是相同的，不同的 logger name 获取到的对象实例是不同的</span></div>
<p>&nbsp;</p>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">2，工厂模式</span></strong></span></p>
<p>大部分工厂类都是以&ldquo;Factory&rdquo;这个单词结尾的，工厂类中创建对象的方法一般都是 create 开头，比如代码中的 createParser()，但有的也命名为 getInstance()、createInstance()、newInstance()</p>
<p>①简单工厂</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('708976b1-4201-4c0d-b6aa-33e847256f6d')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_708976b1-4201-4c0d-b6aa-33e847256f6d" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_708976b1-4201-4c0d-b6aa-33e847256f6d" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_708976b1-4201-4c0d-b6aa-33e847256f6d" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> RuleConfigSource {
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> RuleConfig load(String ruleConfigFilePath) {
    String ruleConfigFileExtension </span>=<span style="color: #000000;"> getFileExtension(ruleConfigFilePath);
    IRuleConfigParser parser </span>=<span style="color: #000000;"> RuleConfigParserFactory.createParser(ruleConfigFileExtension);
    </span><span style="color: #0000ff;">if</span> (parser == <span style="color: #0000ff;">null</span><span style="color: #000000;">) {
      </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> InvalidRuleConfigException(
              </span><span style="color: #800000;">"</span><span style="color: #800000;">Rule config file format is not supported: </span><span style="color: #800000;">"</span> +<span style="color: #000000;"> ruleConfigFilePath);
    }

    String configText </span>= <span style="color: #800000;">""</span><span style="color: #000000;">;
    </span><span style="color: #008000;">//</span><span style="color: #008000;">从ruleConfigFilePath文件中读取配置文本到configText中</span>
    RuleConfig ruleConfig =<span style="color: #000000;"> parser.parse(configText);
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> ruleConfig;
  }

  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> String getFileExtension(String filePath) {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...解析文件名获取扩展名，比如rule.json，返回json</span>
    <span style="color: #0000ff;">return</span> <span style="color: #800000;">"</span><span style="color: #800000;">json</span><span style="color: #800000;">"</span><span style="color: #000000;">;
  }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> RuleConfigParserFactory {
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> IRuleConfigParser createParser(String configFormat) {
    IRuleConfigParser parser </span>= <span style="color: #0000ff;">null</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">if</span> (<span style="color: #800000;">"</span><span style="color: #800000;">json</span><span style="color: #800000;">"</span><span style="color: #000000;">.equalsIgnoreCase(configFormat)) {
      parser </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> JsonRuleConfigParser();
    } </span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span> (<span style="color: #800000;">"</span><span style="color: #800000;">xml</span><span style="color: #800000;">"</span><span style="color: #000000;">.equalsIgnoreCase(configFormat)) {
      parser </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> XmlRuleConfigParser();
    } </span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span> (<span style="color: #800000;">"</span><span style="color: #800000;">yaml</span><span style="color: #800000;">"</span><span style="color: #000000;">.equalsIgnoreCase(configFormat)) {
      parser </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> YamlRuleConfigParser();
    } </span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span> (<span style="color: #800000;">"</span><span style="color: #800000;">properties</span><span style="color: #800000;">"</span><span style="color: #000000;">.equalsIgnoreCase(configFormat)) {
      parser </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> PropertiesRuleConfigParser();
    }
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> parser;
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">简单工厂第一种实现</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('c6f4e89a-9bce-41f8-9951-0e81208d8c29')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_c6f4e89a-9bce-41f8-9951-0e81208d8c29" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_c6f4e89a-9bce-41f8-9951-0e81208d8c29" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_c6f4e89a-9bce-41f8-9951-0e81208d8c29" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> RuleConfigParserFactory {
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> final Map&lt;String, RuleConfigParser&gt; cachedParsers = <span style="color: #0000ff;">new</span> HashMap&lt;&gt;<span style="color: #000000;">();

  </span><span style="color: #0000ff;">static</span><span style="color: #000000;"> {
    cachedParsers.put(</span><span style="color: #800000;">"</span><span style="color: #800000;">json</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span><span style="color: #000000;"> JsonRuleConfigParser());
    cachedParsers.put(</span><span style="color: #800000;">"</span><span style="color: #800000;">xml</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span><span style="color: #000000;"> XmlRuleConfigParser());
    cachedParsers.put(</span><span style="color: #800000;">"</span><span style="color: #800000;">yaml</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span><span style="color: #000000;"> YamlRuleConfigParser());
    cachedParsers.put(</span><span style="color: #800000;">"</span><span style="color: #800000;">properties</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span><span style="color: #000000;"> PropertiesRuleConfigParser());
  }

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> IRuleConfigParser createParser(String configFormat) {
    </span><span style="color: #0000ff;">if</span> (configFormat == <span style="color: #0000ff;">null</span> ||<span style="color: #000000;"> configFormat.isEmpty()) {
      </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">null</span>;<span style="color: #008000;">//</span><span style="color: #008000;">返回null还是IllegalArgumentException全凭你自己说了算</span>
<span style="color: #000000;">    }
    IRuleConfigParser parser </span>= cachedParsers.<span style="color: #0000ff;">get</span><span style="color: #000000;">(configFormat.toLowerCase());
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> parser;
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">简单工厂第二种实现</span></div>
<p>在 RuleConfigParserFactory 的第一种代码实现中，有一组 if 分支判断逻辑，是不是应该用多态或其他设计模式来替代呢？实际上，如果 if 分支并不是很多，代码中有 if 分支也是完全可以接受的</p>
<p>②工厂方法</p>
<p>工厂方法模式比起简单工厂模式更加符合开闭原则</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('21f5083e-501e-4e03-8751-eda0bd41b014')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_21f5083e-501e-4e03-8751-eda0bd41b014" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_21f5083e-501e-4e03-8751-eda0bd41b014" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_21f5083e-501e-4e03-8751-eda0bd41b014" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IRuleConfigParserFactory {
  IRuleConfigParser createParser();
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> JsonRuleConfigParserFactory implements IRuleConfigParserFactory {
  @Override
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> IRuleConfigParser createParser() {
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> JsonRuleConfigParser();
  }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> XmlRuleConfigParserFactory implements IRuleConfigParserFactory {
  @Override
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> IRuleConfigParser createParser() {
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> XmlRuleConfigParser();
  }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> YamlRuleConfigParserFactory implements IRuleConfigParserFactory {
  @Override
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> IRuleConfigParser createParser() {
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> YamlRuleConfigParser();
  }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> PropertiesRuleConfigParserFactory implements IRuleConfigParserFactory {
  @Override
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> IRuleConfigParser createParser() {
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> PropertiesRuleConfigParser();
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">工厂方法</span></div>
<p>工厂方法讲工厂类对象的创建逻辑又耦合进了 load() 函数中。我们可以为工厂类再创建一个简单工厂，也就是工厂的工厂，用来创建工厂类对象</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('50895338-8f83-4f83-9702-533da8e3a20c')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_50895338-8f83-4f83-9702-533da8e3a20c" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_50895338-8f83-4f83-9702-533da8e3a20c" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_50895338-8f83-4f83-9702-533da8e3a20c" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> RuleConfigSource {
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> RuleConfig load(String ruleConfigFilePath) {
    String ruleConfigFileExtension </span>=<span style="color: #000000;"> getFileExtension(ruleConfigFilePath);

    IRuleConfigParserFactory parserFactory </span>=<span style="color: #000000;"> RuleConfigParserFactoryMap.getParserFactory(ruleConfigFileExtension);
    </span><span style="color: #0000ff;">if</span> (parserFactory == <span style="color: #0000ff;">null</span><span style="color: #000000;">) {
      </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> InvalidRuleConfigException(<span style="color: #800000;">"</span><span style="color: #800000;">Rule config file format is not supported: </span><span style="color: #800000;">"</span> +<span style="color: #000000;"> ruleConfigFilePath);
    }
    IRuleConfigParser parser </span>=<span style="color: #000000;"> parserFactory.createParser();

    String configText </span>= <span style="color: #800000;">""</span><span style="color: #000000;">;
    </span><span style="color: #008000;">//</span><span style="color: #008000;">从ruleConfigFilePath文件中读取配置文本到configText中</span>
    RuleConfig ruleConfig =<span style="color: #000000;"> parser.parse(configText);
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> ruleConfig;
  }

  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> String getFileExtension(String filePath) {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...解析文件名获取扩展名，比如rule.json，返回json</span>
    <span style="color: #0000ff;">return</span> <span style="color: #800000;">"</span><span style="color: #800000;">json</span><span style="color: #800000;">"</span><span style="color: #000000;">;
  }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">因为工厂类只包含方法，不包含成员变量，完全可以复用，
</span><span style="color: #008000;">//</span><span style="color: #008000;">不需要每次都创建新的工厂类对象，所以，简单工厂模式的第二种实现思路更加合适。</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> RuleConfigParserFactoryMap { <span style="color: #008000;">//</span><span style="color: #008000;">工厂的工厂</span>
  <span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> final Map&lt;String, IRuleConfigParserFactory&gt; cachedFactories = <span style="color: #0000ff;">new</span> HashMap&lt;&gt;<span style="color: #000000;">();

  </span><span style="color: #0000ff;">static</span><span style="color: #000000;"> {
    cachedFactories.put(</span><span style="color: #800000;">"</span><span style="color: #800000;">json</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span><span style="color: #000000;"> JsonRuleConfigParserFactory());
    cachedFactories.put(</span><span style="color: #800000;">"</span><span style="color: #800000;">xml</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span><span style="color: #000000;"> XmlRuleConfigParserFactory());
    cachedFactories.put(</span><span style="color: #800000;">"</span><span style="color: #800000;">yaml</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span><span style="color: #000000;"> YamlRuleConfigParserFactory());
    cachedFactories.put(</span><span style="color: #800000;">"</span><span style="color: #800000;">properties</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span><span style="color: #000000;"> PropertiesRuleConfigParserFactory());
  }

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> IRuleConfigParserFactory getParserFactory(String type) {
    </span><span style="color: #0000ff;">if</span> (type == <span style="color: #0000ff;">null</span> ||<span style="color: #000000;"> type.isEmpty()) {
      </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">null</span><span style="color: #000000;">;
    }
    IRuleConfigParserFactory parserFactory </span>= cachedFactories.<span style="color: #0000ff;">get</span><span style="color: #000000;">(type.toLowerCase());
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> parserFactory;
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">改造之后的工厂方法</span></div>
<p>③什么时候使用简单工厂，什么时候使用工厂方法</p>
<p>之所以将某个代码块剥离出来，独立为函数或者类，原因是这个代码块的逻辑过于复杂，剥离之后能让代码更加清晰，更加可读、可维护。但是，如果代码块本身并不复杂，就几行代码而已，我们完全没必要将它拆分成单独的函数或者类</p>
<p>当每个对象的创建逻辑都比较简单的时候，我推荐使用简单工厂模式，将多个对象的创建逻辑放到一个工厂类中</p>
<p>对象的创建比较复杂，需要组合其他类对象，做各种初始化操作的时候，我们推荐使用工厂方法模式，将复杂的创建逻辑拆分到多个工厂类中，让每个工厂类都不至于过于复杂。</p>
<p>④何为创建逻辑比较复杂？</p>
<p>第一种情况：类似规则配置解析的例子，代码中存在 if-else 分支判断，动态地根据不同的类型创建不同的对象。针对这种情况，我们就考虑使用工厂模式，将这一大坨 if-else 创建对象的代码抽离出来，放到工厂类中。</p>
<p>还有一种情况，尽管我们不需要根据不同的类型创建不同的对象，但是，单个对象本身的创建过程比较复杂，比如前面提到的要组合其他类对象，做各种初始化操作。在这种情况下，我们也可以考虑使用工厂模式，将对象的创建过程封装到工厂类中。</p>
<p>⑤抽象工厂</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('79efbc2f-c677-4792-8a90-8925e8db4813')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_79efbc2f-c677-4792-8a90-8925e8db4813" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_79efbc2f-c677-4792-8a90-8925e8db4813" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_79efbc2f-c677-4792-8a90-8925e8db4813" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IConfigParserFactory {
  IRuleConfigParser createRuleParser();
  ISystemConfigParser createSystemParser();
  </span><span style="color: #008000;">//</span><span style="color: #008000;">此处可以扩展新的parser类型，比如IBizConfigParser</span>
<span style="color: #000000;">}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> JsonConfigParserFactory implements IConfigParserFactory {
  @Override
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> IRuleConfigParser createRuleParser() {
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> JsonRuleConfigParser();
  }

  @Override
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> ISystemConfigParser createSystemParser() {
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> JsonSystemConfigParser();
  }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> XmlConfigParserFactory implements IConfigParserFactory {
  @Override
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> IRuleConfigParser createRuleParser() {
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> XmlRuleConfigParser();
  }

  @Override
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> ISystemConfigParser createSystemParser() {
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> XmlSystemConfigParser();
  }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 省略YamlConfigParserFactory和PropertiesConfigParserFactory代码</span></pre>
</div>
<span class="cnblogs_code_collapse">抽象工厂就是针对这种非常特殊的场景而诞生的。我们可以让一个工厂负责创建多个不同类型的对象（IRuleConfigParser、ISystemConfigParser 等），而不是只创建一种 parser 对象。这样就可以有效地减少工厂类的个数</span></div>
<p>&nbsp;</p>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">3，建造者模式</span></strong></span></p>
<p>建造者模式是让建造者类来负责对象的创建工作</p>
<p>①与工厂模式的区别</p>
<p>工厂模式：工厂模式用来创建不同但是相关类型的对象（继承同一父类或者接口的一组子类），由给定的参数来决定创建哪种类型的对象</p>
<p>构造者模式：建造者模式是用来创建一种类型的复杂对象，通过设置不同的可选参数，&ldquo;定制化&rdquo;地创建不同的对象</p>
<p>②使用场景</p>
<p>我们把类的必填属性放到构造函数中，强制创建对象的时候就设置。如果必填的属性有很多，把这些必填属性都放到构造函数中设置，那构造函数就又会出现参数列表很长的问题。如果我们把必填属性通过 set() 方法设置，那校验这些必填属性是否已经填写的逻辑就无处安放了。</p>
<p>如果类的属性之间有一定的依赖关系或者约束条件，我们继续使用构造函数配合 set() 方法的设计思路，那这些依赖关系或约束条件的校验逻辑就无处安放了。</p>
<p>如果我们希望创建不可变对象，也就是说，对象在创建好之后，就不能再修改内部的属性值，要实现这个功能，我们就不能在类中暴露 set() 方法。构造函数配合 set() 方法来设置属性值的方式就不适用了。</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('bc4da77a-df40-4105-b4be-89fbc7155f5c')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_bc4da77a-df40-4105-b4be-89fbc7155f5c" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_bc4da77a-df40-4105-b4be-89fbc7155f5c" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_bc4da77a-df40-4105-b4be-89fbc7155f5c" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ResourcePoolConfig {
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> String name;
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">int</span><span style="color: #000000;"> maxTotal;
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">int</span><span style="color: #000000;"> maxIdle;
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">int</span><span style="color: #000000;"> minIdle;

  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> ResourcePoolConfig(Builder builder) {
    </span><span style="color: #0000ff;">this</span>.name =<span style="color: #000000;"> builder.name;
    </span><span style="color: #0000ff;">this</span>.maxTotal =<span style="color: #000000;"> builder.maxTotal;
    </span><span style="color: #0000ff;">this</span>.maxIdle =<span style="color: #000000;"> builder.maxIdle;
    </span><span style="color: #0000ff;">this</span>.minIdle =<span style="color: #000000;"> builder.minIdle;
  }
  </span><span style="color: #008000;">//</span><span style="color: #008000;">...省略getter方法...

  </span><span style="color: #008000;">//</span><span style="color: #008000;">我们将Builder类设计成了ResourcePoolConfig的内部类。
  </span><span style="color: #008000;">//</span><span style="color: #008000;">我们也可以将Builder类设计成独立的非内部类ResourcePoolConfigBuilder。</span>
  <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Builder {
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> final <span style="color: #0000ff;">int</span> DEFAULT_MAX_TOTAL = <span style="color: #800080;">8</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> final <span style="color: #0000ff;">int</span> DEFAULT_MAX_IDLE = <span style="color: #800080;">8</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> final <span style="color: #0000ff;">int</span> DEFAULT_MIN_IDLE = <span style="color: #800080;">0</span><span style="color: #000000;">;

    </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> String name;
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">int</span> maxTotal =<span style="color: #000000;"> DEFAULT_MAX_TOTAL;
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">int</span> maxIdle =<span style="color: #000000;"> DEFAULT_MAX_IDLE;
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">int</span> minIdle =<span style="color: #000000;"> DEFAULT_MIN_IDLE;

    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> ResourcePoolConfig build() {
      </span><span style="color: #008000;">//</span><span style="color: #008000;"> 校验逻辑放到这里来做，包括必填项校验、依赖关系校验、约束条件校验等</span>
      <span style="color: #0000ff;">if</span><span style="color: #000000;"> (StringUtils.isBlank(name)) {
        </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> IllegalArgumentException(<span style="color: #800000;">"</span><span style="color: #800000;">...</span><span style="color: #800000;">"</span><span style="color: #000000;">);
      }
      </span><span style="color: #0000ff;">if</span> (maxIdle &gt;<span style="color: #000000;"> maxTotal) {
        </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> IllegalArgumentException(<span style="color: #800000;">"</span><span style="color: #800000;">...</span><span style="color: #800000;">"</span><span style="color: #000000;">);
      }
      </span><span style="color: #0000ff;">if</span> (minIdle &gt; maxTotal || minIdle &gt;<span style="color: #000000;"> maxIdle) {
        </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> IllegalArgumentException(<span style="color: #800000;">"</span><span style="color: #800000;">...</span><span style="color: #800000;">"</span><span style="color: #000000;">);
      }

      </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> ResourcePoolConfig(<span style="color: #0000ff;">this</span><span style="color: #000000;">);
    }

    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Builder setName(String name) {
      </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (StringUtils.isBlank(name)) {
        </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> IllegalArgumentException(<span style="color: #800000;">"</span><span style="color: #800000;">...</span><span style="color: #800000;">"</span><span style="color: #000000;">);
      }
      </span><span style="color: #0000ff;">this</span>.name =<span style="color: #000000;"> name;
      </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">this</span><span style="color: #000000;">;
    }

    </span><span style="color: #0000ff;">public</span> Builder setMaxTotal(<span style="color: #0000ff;">int</span><span style="color: #000000;"> maxTotal) {
      </span><span style="color: #0000ff;">if</span> (maxTotal &lt;= <span style="color: #800080;">0</span><span style="color: #000000;">) {
        </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> IllegalArgumentException(<span style="color: #800000;">"</span><span style="color: #800000;">...</span><span style="color: #800000;">"</span><span style="color: #000000;">);
      }
      </span><span style="color: #0000ff;">this</span>.maxTotal =<span style="color: #000000;"> maxTotal;
      </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">this</span><span style="color: #000000;">;
    }

    </span><span style="color: #0000ff;">public</span> Builder setMaxIdle(<span style="color: #0000ff;">int</span><span style="color: #000000;"> maxIdle) {
      </span><span style="color: #0000ff;">if</span> (maxIdle &lt; <span style="color: #800080;">0</span><span style="color: #000000;">) {
        </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> IllegalArgumentException(<span style="color: #800000;">"</span><span style="color: #800000;">...</span><span style="color: #800000;">"</span><span style="color: #000000;">);
      }
      </span><span style="color: #0000ff;">this</span>.maxIdle =<span style="color: #000000;"> maxIdle;
      </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">this</span><span style="color: #000000;">;
    }

    </span><span style="color: #0000ff;">public</span> Builder setMinIdle(<span style="color: #0000ff;">int</span><span style="color: #000000;"> minIdle) {
      </span><span style="color: #0000ff;">if</span> (minIdle &lt; <span style="color: #800080;">0</span><span style="color: #000000;">) {
        </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> IllegalArgumentException(<span style="color: #800000;">"</span><span style="color: #800000;">...</span><span style="color: #800000;">"</span><span style="color: #000000;">);
      }
      </span><span style="color: #0000ff;">this</span>.minIdle =<span style="color: #000000;"> minIdle;
      </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">this</span><span style="color: #000000;">;
    }
  }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 这段代码会抛出IllegalArgumentException，因为minIdle&gt;maxIdle</span>
ResourcePoolConfig config = <span style="color: #0000ff;">new</span><span style="color: #000000;"> ResourcePoolConfig.Builder()
        .setName(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbconnectionpool</span><span style="color: #800000;">"</span><span style="color: #000000;">)
        .setMaxTotal(</span><span style="color: #800080;">16</span><span style="color: #000000;">)
        .setMaxIdle(</span><span style="color: #800080;">10</span><span style="color: #000000;">)
        .setMinIdle(</span><span style="color: #800080;">12</span><span style="color: #000000;">)
        .build();</span></pre>
</div>
<span class="cnblogs_code_collapse">使用案例</span></div>
<p>&nbsp;</p>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">4，原型模式</span></strong></span></p>
<p>①什么是原型模式</p>
<p>如果对象的创建成本比较大，而同一个类的不同对象之间差别不大（大部分字段都相同），在这种情况下，我们可以利用对已有对象（原型）进行复制（或者叫拷贝）的方式，来创建新对象，以达到节省创建时间的目的。这种基于原型来创建对象的方式就叫作原型设计模式，简称原型模式。</p>
<p>②原型模式的两种实现方法</p>
<p>深拷贝和浅拷贝。浅拷贝只会复制对象中基本数据类型数据和引用对象的内存地址，不会递归地复制引用对象，以及引用对象的引用对象&hellip;&hellip;而深拷贝得到的是一份完完全全独立的对象。所以，深拷贝比起浅拷贝来说，更加耗时，更加耗内存空间。</p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: #169fe6;"><span style="color: #ffffff;"><strong>六、设计模式与范式：结构型</strong></span></p>
<p><span style="color: #000000; font-size: 14px;"><span style="font-size: 12px; color: #808080;">结构型设计模式主要解决&ldquo;类或对象的组合或组装&rdquo;问题</span><br /></span></p>
<p><span style="color: #000000; font-size: 14px;"><span style="font-size: 12px; color: #808080;">结构型模式是将不同功能代码解耦</span></span></p>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">1，代理模式</span></strong></span></p>
<p>它在不改变原始类（或叫被代理类）代码的情况下，通过引入代理类来给原始类附加功能</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('bc614672-6343-4f84-be4d-8acad51df443')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_bc614672-6343-4f84-be4d-8acad51df443" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_bc614672-6343-4f84-be4d-8acad51df443" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_bc614672-6343-4f84-be4d-8acad51df443" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IUserController {
  UserVo login(String telephone, String password);
  UserVo register(String telephone, String password);
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> UserController implements IUserController {
  </span><span style="color: #008000;">//</span><span style="color: #008000;">...省略其他属性和方法...</span>
<span style="color: #000000;">
  @Override
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> UserVo login(String telephone, String password) {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...省略login逻辑...
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...返回UserVo数据...</span>
<span style="color: #000000;">  }

  @Override
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> UserVo register(String telephone, String password) {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...省略register逻辑...
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...返回UserVo数据...</span>
<span style="color: #000000;">  }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> UserControllerProxy implements IUserController {
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> MetricsCollector metricsCollector;
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> UserController userController;

  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> UserControllerProxy(UserController userController) {
    </span><span style="color: #0000ff;">this</span>.userController =<span style="color: #000000;"> userController;
    </span><span style="color: #0000ff;">this</span>.metricsCollector = <span style="color: #0000ff;">new</span><span style="color: #000000;"> MetricsCollector();
  }

  @Override
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> UserVo login(String telephone, String password) {
    </span><span style="color: #0000ff;">long</span> startTimestamp =<span style="color: #000000;"> System.currentTimeMillis();

    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 委托</span>
    UserVo userVo =<span style="color: #000000;"> userController.login(telephone, password);

    </span><span style="color: #0000ff;">long</span> endTimeStamp =<span style="color: #000000;"> System.currentTimeMillis();
    </span><span style="color: #0000ff;">long</span> responseTime = endTimeStamp -<span style="color: #000000;"> startTimestamp;
    RequestInfo requestInfo </span>= <span style="color: #0000ff;">new</span> RequestInfo(<span style="color: #800000;">"</span><span style="color: #800000;">login</span><span style="color: #800000;">"</span><span style="color: #000000;">, responseTime, startTimestamp);
    metricsCollector.recordRequest(requestInfo);

    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> userVo;
  }

  @Override
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> UserVo register(String telephone, String password) {
    </span><span style="color: #0000ff;">long</span> startTimestamp =<span style="color: #000000;"> System.currentTimeMillis();

    UserVo userVo </span>=<span style="color: #000000;"> userController.register(telephone, password);

    </span><span style="color: #0000ff;">long</span> endTimeStamp =<span style="color: #000000;"> System.currentTimeMillis();
    </span><span style="color: #0000ff;">long</span> responseTime = endTimeStamp -<span style="color: #000000;"> startTimestamp;
    RequestInfo requestInfo </span>= <span style="color: #0000ff;">new</span> RequestInfo(<span style="color: #800000;">"</span><span style="color: #800000;">register</span><span style="color: #800000;">"</span><span style="color: #000000;">, responseTime, startTimestamp);
    metricsCollector.recordRequest(requestInfo);

    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> userVo;
  }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">UserControllerProxy使用举例
</span><span style="color: #008000;">//</span><span style="color: #008000;">因为原始类和代理类实现相同的接口，是基于接口而非实现编程
</span><span style="color: #008000;">//</span><span style="color: #008000;">将UserController类对象替换为UserControllerProxy类对象，不需要改动太多代码</span>
IUserController userController = <span style="color: #0000ff;">new</span> UserControllerProxy(<span style="color: #0000ff;">new</span> UserController());</pre>
</div>
<span class="cnblogs_code_collapse">采用组合模式</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('cced4663-1983-4041-82ea-f2371080c7e3')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_cced4663-1983-4041-82ea-f2371080c7e3" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_cced4663-1983-4041-82ea-f2371080c7e3" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_cced4663-1983-4041-82ea-f2371080c7e3" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> UserControllerProxy extends UserController {
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> MetricsCollector metricsCollector;

  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> UserControllerProxy() {
    </span><span style="color: #0000ff;">this</span>.metricsCollector = <span style="color: #0000ff;">new</span><span style="color: #000000;"> MetricsCollector();
  }

  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> UserVo login(String telephone, String password) {
    </span><span style="color: #0000ff;">long</span> startTimestamp =<span style="color: #000000;"> System.currentTimeMillis();

    UserVo userVo </span>=<span style="color: #000000;"> super.login(telephone, password);

    </span><span style="color: #0000ff;">long</span> endTimeStamp =<span style="color: #000000;"> System.currentTimeMillis();
    </span><span style="color: #0000ff;">long</span> responseTime = endTimeStamp -<span style="color: #000000;"> startTimestamp;
    RequestInfo requestInfo </span>= <span style="color: #0000ff;">new</span> RequestInfo(<span style="color: #800000;">"</span><span style="color: #800000;">login</span><span style="color: #800000;">"</span><span style="color: #000000;">, responseTime, startTimestamp);
    metricsCollector.recordRequest(requestInfo);

    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> userVo;
  }

  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> UserVo register(String telephone, String password) {
    </span><span style="color: #0000ff;">long</span> startTimestamp =<span style="color: #000000;"> System.currentTimeMillis();

    UserVo userVo </span>=<span style="color: #000000;"> super.register(telephone, password);

    </span><span style="color: #0000ff;">long</span> endTimeStamp =<span style="color: #000000;"> System.currentTimeMillis();
    </span><span style="color: #0000ff;">long</span> responseTime = endTimeStamp -<span style="color: #000000;"> startTimestamp;
    RequestInfo requestInfo </span>= <span style="color: #0000ff;">new</span> RequestInfo(<span style="color: #800000;">"</span><span style="color: #800000;">register</span><span style="color: #800000;">"</span><span style="color: #000000;">, responseTime, startTimestamp);
    metricsCollector.recordRequest(requestInfo);

    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> userVo;
  }
}
</span><span style="color: #008000;">//</span><span style="color: #008000;">UserControllerProxy使用举例</span>
UserController userController = <span style="color: #0000ff;">new</span> UserControllerProxy();</pre>
</div>
<span class="cnblogs_code_collapse">采用继承模式</span></div>
<p>所谓动态代理（Dynamic Proxy），就是我们不事先为每个原始类编写代理类，而是在运行的时候，动态地创建原始类对应的代理类，然后在系统中用代理类替换掉原始类。Spring AOP 底层的实现原理就是基于动态代理</p>
<p>使用场景：监控、统计、鉴权、限流、事务、幂等、日志</p>
<p>&nbsp;</p>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">2，桥接模式</span></strong></span></p>
<p>一个类存在两个（或多个）独立变化的维度，我们通过组合的方式，让这两个（或多个）维度可以独立进行扩展</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('6f823351-ecd6-4d5a-8df3-b567e5e3e1fe')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_6f823351-ecd6-4d5a-8df3-b567e5e3e1fe" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_6f823351-ecd6-4d5a-8df3-b567e5e3e1fe" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_6f823351-ecd6-4d5a-8df3-b567e5e3e1fe" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> MsgSender {
  </span><span style="color: #0000ff;">void</span><span style="color: #000000;"> send(String message);
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> TelephoneMsgSender implements MsgSender {
  </span><span style="color: #0000ff;">private</span> List&lt;String&gt;<span style="color: #000000;"> telephones;

  </span><span style="color: #0000ff;">public</span> TelephoneMsgSender(List&lt;String&gt;<span style="color: #000000;"> telephones) {
    </span><span style="color: #0000ff;">this</span>.telephones =<span style="color: #000000;"> telephones;
  }

  @Override
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> send(String message) {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">  }

}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> EmailMsgSender implements MsgSender {
  </span><span style="color: #008000;">//</span><span style="color: #008000;"> 与TelephoneMsgSender代码结构类似，所以省略...</span>
<span style="color: #000000;">}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> WechatMsgSender implements MsgSender {
  </span><span style="color: #008000;">//</span><span style="color: #008000;"> 与TelephoneMsgSender代码结构类似，所以省略...</span>
<span style="color: #000000;">}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Notification {
  </span><span style="color: #0000ff;">protected</span><span style="color: #000000;"> MsgSender msgSender;

  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Notification(MsgSender msgSender) {
    </span><span style="color: #0000ff;">this</span>.msgSender =<span style="color: #000000;"> msgSender;
  }

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> notify(String message);
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SevereNotification extends Notification {
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> SevereNotification(MsgSender msgSender) {
    super(msgSender);
  }

  @Override
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> notify(String message) {
    msgSender.send(message);
  }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> UrgencyNotification extends Notification {
  </span><span style="color: #008000;">//</span><span style="color: #008000;"> 与SevereNotification代码结构类似，所以省略...</span>
<span style="color: #000000;">}
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> NormalNotification extends Notification {
  </span><span style="color: #008000;">//</span><span style="color: #008000;"> 与SevereNotification代码结构类似，所以省略...</span>
<span style="color: #000000;">}
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> TrivialNotification extends Notification {
  </span><span style="color: #008000;">//</span><span style="color: #008000;"> 与SevereNotification代码结构类似，所以省略...</span>
}</pre>
</div>
<span class="cnblogs_code_collapse">桥接模式案例</span></div>
<p>&nbsp;</p>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">3，装饰器模式</span></strong></span></p>
<p>装饰器模式主要解决继承关系过于复杂的问题，通过组合来替代继承。它主要的作用是给原始类添加增强功能。这也是判断是否该用装饰器模式的一个重要的依据。除此之外，装饰器模式还有一个特点，那就是可以对原始类嵌套使用多个装饰器。为了满足这个应用场景，在设计的时候，装饰器类需要跟原始类继承相同的抽象类或者接口。</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('d50d5be7-b6d9-4d02-bb21-d66a7f57ab91')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_d50d5be7-b6d9-4d02-bb21-d66a7f57ab91" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_d50d5be7-b6d9-4d02-bb21-d66a7f57ab91" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_d50d5be7-b6d9-4d02-bb21-d66a7f57ab91" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> InputStream {
  </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
  <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span> read(<span style="color: #0000ff;">byte</span><span style="color: #000000;"> b[]) throws IOException {
    </span><span style="color: #0000ff;">return</span> read(b, <span style="color: #800080;">0</span><span style="color: #000000;">, b.length);
  }
  
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span> read(<span style="color: #0000ff;">byte</span> b[], <span style="color: #0000ff;">int</span> off, <span style="color: #0000ff;">int</span><span style="color: #000000;"> len) throws IOException {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">  }
  
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">long</span> skip(<span style="color: #0000ff;">long</span><span style="color: #000000;"> n) throws IOException {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">  }

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span><span style="color: #000000;"> available() throws IOException {
    </span><span style="color: #0000ff;">return</span> <span style="color: #800080;">0</span><span style="color: #000000;">;
  }
  
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> close() throws IOException {}

  </span><span style="color: #0000ff;">public</span> synchronized <span style="color: #0000ff;">void</span> mark(<span style="color: #0000ff;">int</span><span style="color: #000000;"> readlimit) {}
    
  </span><span style="color: #0000ff;">public</span> synchronized <span style="color: #0000ff;">void</span><span style="color: #000000;"> reset() throws IOException {
    </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> IOException(<span style="color: #800000;">"</span><span style="color: #800000;">mark/reset not supported</span><span style="color: #800000;">"</span><span style="color: #000000;">);
  }

  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> boolean markSupported() {
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">false</span><span style="color: #000000;">;
  }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> BufferedInputStream extends InputStream {
  </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">volatile</span> InputStream <span style="color: #0000ff;">in</span><span style="color: #000000;">;

  </span><span style="color: #0000ff;">protected</span> BufferedInputStream(InputStream <span style="color: #0000ff;">in</span><span style="color: #000000;">) {
    </span><span style="color: #0000ff;">this</span>.<span style="color: #0000ff;">in</span> = <span style="color: #0000ff;">in</span><span style="color: #000000;">;
  }
  
  </span><span style="color: #008000;">//</span><span style="color: #008000;">...实现基于缓存的读数据接口...  </span>
<span style="color: #000000;">}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> DataInputStream extends InputStream {
  </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">volatile</span> InputStream <span style="color: #0000ff;">in</span><span style="color: #000000;">;

  </span><span style="color: #0000ff;">protected</span> DataInputStream(InputStream <span style="color: #0000ff;">in</span><span style="color: #000000;">) {
    </span><span style="color: #0000ff;">this</span>.<span style="color: #0000ff;">in</span> = <span style="color: #0000ff;">in</span><span style="color: #000000;">;
  }
  
  </span><span style="color: #008000;">//</span><span style="color: #008000;">...实现读取基本类型数据的接口</span>
}</pre>
</div>
<span class="cnblogs_code_collapse">装饰模式</span></div>
<p>①装饰模式与简单的组合关系</p>
<p>第一个比较特殊的地方：装饰器类和原始类继承同样的父类，这样我们可以对原始类&ldquo;嵌套&rdquo;多个装饰器类</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('20e481b8-f8b1-41b4-87de-bbceccc60772')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_20e481b8-f8b1-41b4-87de-bbceccc60772" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_20e481b8-f8b1-41b4-87de-bbceccc60772" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_20e481b8-f8b1-41b4-87de-bbceccc60772" class="cnblogs_code_hide">
<pre>InputStream <span style="color: #0000ff;">in</span> = <span style="color: #0000ff;">new</span> FileInputStream(<span style="color: #800000;">"</span><span style="color: #800000;">/user/wangzheng/test.txt</span><span style="color: #800000;">"</span><span style="color: #000000;">);
InputStream bin </span>= <span style="color: #0000ff;">new</span> BufferedInputStream(<span style="color: #0000ff;">in</span><span style="color: #000000;">);
DataInputStream din </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> DataInputStream(bin);
</span><span style="color: #0000ff;">int</span> data = din.readInt();</pre>
</div>
<span class="cnblogs_code_collapse">比如，下面这样一段代码，我们对 FileInputStream 嵌套了两个装饰器类：BufferedInputStream 和 DataInputStream，让它既支持缓存读取，又支持按照基本数据类型来读取数据。</span></div>
<p>第二个比较特殊的地方：装饰器类是对功能的增强，这也是装饰器类应用场景的一个重要特点</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('57acc785-c6f6-47a4-bb37-f0c80e696651')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_57acc785-c6f6-47a4-bb37-f0c80e696651" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_57acc785-c6f6-47a4-bb37-f0c80e696651" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_57acc785-c6f6-47a4-bb37-f0c80e696651" class="cnblogs_code_hide">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> 代理模式的代码结构(下面的接口也可以替换成抽象类)</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IA {
  </span><span style="color: #0000ff;">void</span><span style="color: #000000;"> f();
}
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> A impelements IA {
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> f() { <span style="color: #008000;">//</span><span style="color: #008000;">... }</span>
<span style="color: #000000;">}
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> AProxy impements IA {
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> IA a;
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> AProxy(IA a) {
    </span><span style="color: #0000ff;">this</span>.a =<span style="color: #000000;"> a;
  }
  
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> f() {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 新添加的代理逻辑</span>
<span style="color: #000000;">    a.f();
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 新添加的代理逻辑</span>
<span style="color: #000000;">  }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 装饰器模式的代码结构(下面的接口也可以替换成抽象类)</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IA {
  </span><span style="color: #0000ff;">void</span><span style="color: #000000;"> f();
}
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> A impelements IA {
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> f() { <span style="color: #008000;">//</span><span style="color: #008000;">... }</span>
<span style="color: #000000;">}
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ADecorator impements IA {
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> IA a;
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> ADecorator(IA a) {
    </span><span style="color: #0000ff;">this</span>.a =<span style="color: #000000;"> a;
  }
  
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> f() {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 功能增强代码</span>
<span style="color: #000000;">    a.f();
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 功能增强代码</span>
<span style="color: #000000;">  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">代理模式中，代理类附加的是跟原始类无关的功能，而在装饰器模式中，装饰器类附加的是跟原始类相关的增强功能</span></div>
<p>&nbsp;</p>
<p><span style="font-size: 16px; color: #ff6600;"><strong>4，适配器模式</strong></span></p>
<p>适配器模式将不兼容的接口转换为可兼容的接口，让原本由于接口不兼容而不能一起工作的类可以一起工作。</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('9362f555-8a74-49ec-b51f-958ef60e1411')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_9362f555-8a74-49ec-b51f-958ef60e1411" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_9362f555-8a74-49ec-b51f-958ef60e1411" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_9362f555-8a74-49ec-b51f-958ef60e1411" class="cnblogs_code_hide">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> 类适配器: 基于继承</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> ITarget {
  </span><span style="color: #0000ff;">void</span><span style="color: #000000;"> f1();
  </span><span style="color: #0000ff;">void</span><span style="color: #000000;"> f2();
  </span><span style="color: #0000ff;">void</span><span style="color: #000000;"> fc();
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Adaptee {
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> fa() { <span style="color: #008000;">//</span><span style="color: #008000;">... }</span>
  <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> fb() { <span style="color: #008000;">//</span><span style="color: #008000;">... }</span>
  <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> fc() { <span style="color: #008000;">//</span><span style="color: #008000;">... }</span>
<span style="color: #000000;">}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Adaptor extends Adaptee implements ITarget {
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> f1() {
    super.fa();
  }
  
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> f2() {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...重新实现f2()...</span>
<span style="color: #000000;">  }
  
  </span><span style="color: #008000;">//</span><span style="color: #008000;"> 这里fc()不需要实现，直接继承自Adaptee，这是跟对象适配器最大的不同点</span>
}</pre>
</div>
<span class="cnblogs_code_collapse">类适配器，基于继承</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('27f41bec-48ee-4c65-a4eb-b47613d78a98')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_27f41bec-48ee-4c65-a4eb-b47613d78a98" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_27f41bec-48ee-4c65-a4eb-b47613d78a98" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_27f41bec-48ee-4c65-a4eb-b47613d78a98" class="cnblogs_code_hide">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> 对象适配器：基于组合</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> ITarget {
  </span><span style="color: #0000ff;">void</span><span style="color: #000000;"> f1();
  </span><span style="color: #0000ff;">void</span><span style="color: #000000;"> f2();
  </span><span style="color: #0000ff;">void</span><span style="color: #000000;"> fc();
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Adaptee {
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> fa() { <span style="color: #008000;">//</span><span style="color: #008000;">... }</span>
  <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> fb() { <span style="color: #008000;">//</span><span style="color: #008000;">... }</span>
  <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> fc() { <span style="color: #008000;">//</span><span style="color: #008000;">... }</span>
<span style="color: #000000;">}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Adaptor implements ITarget {
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> Adaptee adaptee;
  
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Adaptor(Adaptee adaptee) {
    </span><span style="color: #0000ff;">this</span>.adaptee =<span style="color: #000000;"> adaptee;
  }
  
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> f1() {
    adaptee.fa(); </span><span style="color: #008000;">//</span><span style="color: #008000;">委托给Adaptee</span>
<span style="color: #000000;">  }
  
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> f2() {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...重新实现f2()...</span>
<span style="color: #000000;">  }
  
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> fc() {
    adaptee.fc();
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">对象适配器，基于组合</span></div>
<p>针对这两种实现方式，在实际的开发中，到底该如何选择使用哪一种呢？判断的标准主要有两个，一个是 Adaptee 接口的个数，另一个是 Adaptee 和 ITarget 的契合程度。</p>
<p><span style="font-size: 12px;">如果 Adaptee 接口并不多，那两种实现方式都可以。</span></p>
<p><span style="font-size: 12px;">如果 Adaptee 接口很多，而且 Adaptee 和 ITarget 接口定义大部分都相同，那我们推荐使用类适配器，因为 Adaptor 复用父类 Adaptee 的接口，比起对象适配器的实现方式，Adaptor 的代码量要少一些。</span></p>
<p><span style="font-size: 12px;">如果 Adaptee 接口很多，而且 Adaptee 和 ITarget 接口定义大部分都不相同，那我们推荐使用对象适配器，因为组合结构相对于继承更加灵活。</span></p>
<p>①使用场景</p>
<p>封装有缺陷的接口设计</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('5c4c7336-6fa8-4750-b743-dc570021f1b7')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_5c4c7336-6fa8-4750-b743-dc570021f1b7" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_5c4c7336-6fa8-4750-b743-dc570021f1b7" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_5c4c7336-6fa8-4750-b743-dc570021f1b7" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> CD { <span style="color: #008000;">//</span><span style="color: #008000;">这个类来自外部sdk，我们无权修改它的代码
  </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
  <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span> staticFunction1() { <span style="color: #008000;">//</span><span style="color: #008000;">... }</span>
  
  <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> uglyNamingFunction2() { <span style="color: #008000;">//</span><span style="color: #008000;">... }</span>

  <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> tooManyParamsFunction3(<span style="color: #0000ff;">int</span> paramA, <span style="color: #0000ff;">int</span> paramB, ...) { <span style="color: #008000;">//</span><span style="color: #008000;">... }</span>
  
   <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> lowPerformanceFunction4() { <span style="color: #008000;">//</span><span style="color: #008000;">... }</span>
<span style="color: #000000;">}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 使用适配器模式进行重构</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ITarget {
  </span><span style="color: #0000ff;">void</span><span style="color: #000000;"> function1();
  </span><span style="color: #0000ff;">void</span><span style="color: #000000;"> function2();
  </span><span style="color: #0000ff;">void</span><span style="color: #000000;"> fucntion3(ParamsWrapperDefinition paramsWrapper);
  </span><span style="color: #0000ff;">void</span><span style="color: #000000;"> function4();
  </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">}
</span><span style="color: #008000;">//</span><span style="color: #008000;"> 注意：适配器类的命名不一定非得末尾带Adaptor</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> CDAdaptor extends CD implements ITarget {
  </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
  <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> function1() {
     super.staticFunction1();
  }
  
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> function2() {
    super.uglyNamingFucntion2();
  }
  
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> function3(ParamsWrapperDefinition paramsWrapper) {
     super.tooManyParamsFunction3(paramsWrapper.getParamA(), ...);
  }
  
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> function4() {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...reimplement it...</span>
<span style="color: #000000;">  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">假设我们依赖的外部系统在接口设计方面有缺陷（比如包含大量静态方法），引入之后会影响到我们自身代码的可测试性。为了隔离设计上的缺陷，我们希望对外部系统提供的接口进行二次封装，抽象出更好的接口设计，这个时候就可以使用适配器模式了。</span></div>
<p>统一多个类的接口设计</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('019bb72c-e612-4d03-bb1b-7917db22bef1')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_019bb72c-e612-4d03-bb1b-7917db22bef1" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_019bb72c-e612-4d03-bb1b-7917db22bef1" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_019bb72c-e612-4d03-bb1b-7917db22bef1" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> ASensitiveWordsFilter { <span style="color: #008000;">//</span><span style="color: #008000;"> A敏感词过滤系统提供的接口
  </span><span style="color: #008000;">//</span><span style="color: #008000;">text是原始文本，函数输出用***替换敏感词之后的文本</span>
  <span style="color: #0000ff;">public</span><span style="color: #000000;"> String filterSexyWords(String text) {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> ...</span>
<span style="color: #000000;">  }
  
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> String filterPoliticalWords(String text) {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> ...</span>
<span style="color: #000000;">  } 
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> BSensitiveWordsFilter  { <span style="color: #008000;">//</span><span style="color: #008000;"> B敏感词过滤系统提供的接口</span>
  <span style="color: #0000ff;">public</span><span style="color: #000000;"> String filter(String text) {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">  }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> CSensitiveWordsFilter { <span style="color: #008000;">//</span><span style="color: #008000;"> C敏感词过滤系统提供的接口</span>
  <span style="color: #0000ff;">public</span><span style="color: #000000;"> String filter(String text, String mask) {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">  }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 未使用适配器模式之前的代码：代码的可测试性、扩展性不好</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> RiskManagement {
  </span><span style="color: #0000ff;">private</span> ASensitiveWordsFilter aFilter = <span style="color: #0000ff;">new</span><span style="color: #000000;"> ASensitiveWordsFilter();
  </span><span style="color: #0000ff;">private</span> BSensitiveWordsFilter bFilter = <span style="color: #0000ff;">new</span><span style="color: #000000;"> BSensitiveWordsFilter();
  </span><span style="color: #0000ff;">private</span> CSensitiveWordsFilter cFilter = <span style="color: #0000ff;">new</span><span style="color: #000000;"> CSensitiveWordsFilter();
  
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> String filterSensitiveWords(String text) {
    String maskedText </span>=<span style="color: #000000;"> aFilter.filterSexyWords(text);
    maskedText </span>=<span style="color: #000000;"> aFilter.filterPoliticalWords(maskedText);
    maskedText </span>=<span style="color: #000000;"> bFilter.filter(maskedText);
    maskedText </span>= cFilter.filter(maskedText, <span style="color: #800000;">"</span><span style="color: #800000;">***</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> maskedText;
  }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 使用适配器模式进行改造</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span> ISensitiveWordsFilter { <span style="color: #008000;">//</span><span style="color: #008000;"> 统一接口定义</span>
<span style="color: #000000;">  String filter(String text);
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ASensitiveWordsFilterAdaptor implements ISensitiveWordsFilter {
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> ASensitiveWordsFilter aFilter;
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> String filter(String text) {
    String maskedText </span>=<span style="color: #000000;"> aFilter.filterSexyWords(text);
    maskedText </span>=<span style="color: #000000;"> aFilter.filterPoliticalWords(maskedText);
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> maskedText;
  }
}
</span><span style="color: #008000;">//</span><span style="color: #008000;">...省略BSensitiveWordsFilterAdaptor、CSensitiveWordsFilterAdaptor...

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 扩展性更好，更加符合开闭原则，如果添加一个新的敏感词过滤系统，
</span><span style="color: #008000;">//</span><span style="color: #008000;"> 这个类完全不需要改动；而且基于接口而非实现编程，代码的可测试性更好。</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> RiskManagement { 
  </span><span style="color: #0000ff;">private</span> List&lt;ISensitiveWordsFilter&gt; filters = <span style="color: #0000ff;">new</span> ArrayList&lt;&gt;<span style="color: #000000;">();
 
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> addSensitiveWordsFilter(ISensitiveWordsFilter filter) {
    filters.add(filter);
  }
  
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> String filterSensitiveWords(String text) {
    String maskedText </span>=<span style="color: #000000;"> text;
    </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> (ISensitiveWordsFilter filter : filters) {
      maskedText </span>=<span style="color: #000000;"> filter.filter(maskedText);
    }
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> maskedText;
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">假设我们的系统要对用户输入的文本内容做敏感词过滤，为了提高过滤的召回率，我们引入了多款第三方敏感词过滤系统，依次对用户输入的内容进行过滤，过滤掉尽可能多的敏感词。但是，每个系统提供的过滤接口都是不同的。这就意味着我们没法复用一套逻辑来调用各个系统。这个时候，我们就可以使用适配器模式，将所有系统的接口适配为统一的接口定义，这样我们可以复用调用敏感词过滤的代码。</span></div>
<p>替换依赖的外部系统</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('f86c3916-c533-4d85-bac2-8130955b29c1')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_f86c3916-c533-4d85-bac2-8130955b29c1" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_f86c3916-c533-4d85-bac2-8130955b29c1" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_f86c3916-c533-4d85-bac2-8130955b29c1" class="cnblogs_code_hide">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> 外部系统A</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IA {
  </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
  <span style="color: #0000ff;">void</span><span style="color: #000000;"> fa();
}
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> A implements IA {
  </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
  <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> fa() { <span style="color: #008000;">//</span><span style="color: #008000;">... }</span>
<span style="color: #000000;">}
</span><span style="color: #008000;">//</span><span style="color: #008000;"> 在我们的项目中，外部系统A的使用示例</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Demo {
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> IA a;
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Demo(IA a) {
    </span><span style="color: #0000ff;">this</span>.a =<span style="color: #000000;"> a;
  }
  </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">}
Demo d </span>= <span style="color: #0000ff;">new</span> Demo(<span style="color: #0000ff;">new</span><span style="color: #000000;"> A());

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 将外部系统A替换成外部系统B</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> BAdaptor implemnts IA {
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> B b;
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> BAdaptor(B b) {
    </span><span style="color: #0000ff;">this</span>.b=<span style="color: #000000;"> b;
  }
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> fa() {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">    b.fb();
  }
}
</span><span style="color: #008000;">//</span><span style="color: #008000;"> 借助BAdaptor，Demo的代码中，调用IA接口的地方都无需改动，
</span><span style="color: #008000;">//</span><span style="color: #008000;"> 只需要将BAdaptor如下注入到Demo即可。</span>
Demo d = <span style="color: #0000ff;">new</span> Demo(<span style="color: #0000ff;">new</span> BAdaptor(<span style="color: #0000ff;">new</span> B()));</pre>
</div>
<span class="cnblogs_code_collapse">当我们把项目中依赖的一个外部系统替换为另一个外部系统的时候，利用适配器模式，可以减少对代码的改动。</span></div>
<p>兼容老版本接口</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('14ce3e02-0514-47a6-a152-d0891d5421cc')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_14ce3e02-0514-47a6-a152-d0891d5421cc" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_14ce3e02-0514-47a6-a152-d0891d5421cc" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_14ce3e02-0514-47a6-a152-d0891d5421cc" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Collections {
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> Emueration emumeration(final Collection c) {
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> Enumeration() {
      Iterator i </span>=<span style="color: #000000;"> c.iterator();
      
      </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> boolean hasMoreElments() {
        </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> i.hashNext();
      }
      
      </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Object nextElement() {
        </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> i.next():
      }
    }
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">JDK1.0 中包含一个遍历集合容器的类 Enumeration。JDK2.0 对这个类进行了重构，将它改名为 Iterator 类，并且对它的代码实现做了优化。但是考虑到如果将 Enumeration 直接从 JDK2.0 中删除，那使用 JDK1.0 的项目如果切换到 JDK2.0，代码就会编译不通过。为了避免这种情况的发生，我们必须把项目中所有使用到 Enumeration 的地方，都修改为使用 Iterator 才行。</span></div>
<p>②代理、桥接、装饰器、适配器4种模式额区别</p>
<p>代理、桥接、装饰器、适配器，这 4 种模式是比较常用的结构型设计模式。它们的代码结构非常相似。笼统来说，它们都可以称为 Wrapper 模式，也就是通过 Wrapper 类二次封装原始类。</p>
<p>代理模式：代理模式在不改变原始类接口的条件下，为原始类定义一个代理类，主要目的是控制访问，而非加强功能，这是它跟装饰器模式最大的不同</p>
<p>桥接模式：一个类存在两个（或多个）独立变化的维度，我们通过组合的方式，让这两个（或多个）维度可以独立进行扩展</p>
<p>装饰器模式：装饰者模式在不改变原始类接口的情况下，对原始类功能进行增强，并且支持多个装饰器的嵌套使用</p>
<p>适配器模式：适配器模式是一种事后的补救策略。适配器提供跟原始类不同的接口，而代理模式、装饰器模式提供的都是跟原始类相同的接口&nbsp;</p>
<p>&nbsp;</p>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">5，门面模式</span></strong></span></p>
<p>门面模式为子系统提供一组统一的接口，定义一组高层接口让子系统更易用。</p>
<p>主要在接口设计方面使用</p>
<p>尽量保持接口的可复用性，但针对特殊情况，允许提供冗余的门面接口，来提供更易用的接口</p>
<p>①应用场景</p>
<p>解决易用性问题：假设有一个系统 A，提供了 a、b、c、d 四个接口。系统 B 完成某个业务功能，需要调用 A 系统的 a、b、d 接口。利用门面模式，我们提供一个包裹 a、b、d 接口调用的门面接口 x，给系统 B 直接使用</p>
<p>解决性能问题：我们通过将多个接口调用替换为一个门面接口调用，减少网络通信成本，提高 App 客户端的响应速度</p>
<p>②与适配器模式的区别</p>
<p>适配器模式注重的是兼容性，而门面模式注重的是易用性</p>
<p>&nbsp;</p>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">6，组合模式</span></strong></span></p>
<p>&ldquo;组合模式&rdquo;，主要是用来处理树形结构数据。这里的&ldquo;数据&rdquo;，可以简单理解为一组对象集合</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('08747012-060a-4c73-9e1a-c70cdf044511')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_08747012-060a-4c73-9e1a-c70cdf044511" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_08747012-060a-4c73-9e1a-c70cdf044511" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_08747012-060a-4c73-9e1a-c70cdf044511" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> FileSystemNode {
  </span><span style="color: #0000ff;">protected</span><span style="color: #000000;"> String path;

  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> FileSystemNode(String path) {
    </span><span style="color: #0000ff;">this</span>.path =<span style="color: #000000;"> path;
  }

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">int</span><span style="color: #000000;"> countNumOfFiles();
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">long</span><span style="color: #000000;"> countSizeOfFiles();

  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> String getPath() {
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> path;
  }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> File extends FileSystemNode {
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> File(String path) {
    super(path);
  }

  @Override
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span><span style="color: #000000;"> countNumOfFiles() {
    </span><span style="color: #0000ff;">return</span> <span style="color: #800080;">1</span><span style="color: #000000;">;
  }

  @Override
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">long</span><span style="color: #000000;"> countSizeOfFiles() {
    java.io.File file </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> java.io.File(path);
    </span><span style="color: #0000ff;">if</span> (!file.exists()) <span style="color: #0000ff;">return</span> <span style="color: #800080;">0</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> file.length();
  }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Directory extends FileSystemNode {
  </span><span style="color: #0000ff;">private</span> List&lt;FileSystemNode&gt; subNodes = <span style="color: #0000ff;">new</span> ArrayList&lt;&gt;<span style="color: #000000;">();

  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Directory(String path) {
    super(path);
  }

  @Override
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span><span style="color: #000000;"> countNumOfFiles() {
    </span><span style="color: #0000ff;">int</span> numOfFiles = <span style="color: #800080;">0</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> (FileSystemNode fileOrDir : subNodes) {
      numOfFiles </span>+=<span style="color: #000000;"> fileOrDir.countNumOfFiles();
    }
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> numOfFiles;
  }

  @Override
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">long</span><span style="color: #000000;"> countSizeOfFiles() {
    </span><span style="color: #0000ff;">long</span> sizeofFiles = <span style="color: #800080;">0</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> (FileSystemNode fileOrDir : subNodes) {
      sizeofFiles </span>+=<span style="color: #000000;"> fileOrDir.countSizeOfFiles();
    }
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> sizeofFiles;
  }

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> addSubNode(FileSystemNode fileOrDir) {
    subNodes.add(fileOrDir);
  }

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> removeSubNode(FileSystemNode fileOrDir) {
    </span><span style="color: #0000ff;">int</span> size =<span style="color: #000000;"> subNodes.size();
    </span><span style="color: #0000ff;">int</span> i = <span style="color: #800080;">0</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">for</span> (; i &lt; size; ++<span style="color: #000000;">i) {
      </span><span style="color: #0000ff;">if</span> (subNodes.<span style="color: #0000ff;">get</span><span style="color: #000000;">(i).getPath().equalsIgnoreCase(fileOrDir.getPath())) {
        </span><span style="color: #0000ff;">break</span><span style="color: #000000;">;
      }
    }
    </span><span style="color: #0000ff;">if</span> (i &lt;<span style="color: #000000;"> size) {
      subNodes.remove(i);
    }
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">设计一个类来表示文件系统中的目录，能方便地实现下面这些功能：动态地添加、删除某个目录下的子目录或文件；统计指定目录下的文件个数；统计指定目录下的文件总大小。</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('0038ded8-504e-40cd-9e16-f092d0387890')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_0038ded8-504e-40cd-9e16-f092d0387890" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_0038ded8-504e-40cd-9e16-f092d0387890" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_0038ded8-504e-40cd-9e16-f092d0387890" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Demo {
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> main(String[] args) {
    </span><span style="color: #008000;">/*</span><span style="color: #008000;">*
     * /
     * /wz/
     * /wz/a.txt
     * /wz/b.txt
     * /wz/movies/
     * /wz/movies/c.avi
     * /xzg/
     * /xzg/docs/
     * /xzg/docs/d.txt
     </span><span style="color: #008000;">*/</span><span style="color: #000000;">
    Directory fileSystemTree </span>= <span style="color: #0000ff;">new</span> Directory(<span style="color: #800000;">"</span><span style="color: #800000;">/</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    Directory node_wz </span>= <span style="color: #0000ff;">new</span> Directory(<span style="color: #800000;">"</span><span style="color: #800000;">/wz/</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    Directory node_xzg </span>= <span style="color: #0000ff;">new</span> Directory(<span style="color: #800000;">"</span><span style="color: #800000;">/xzg/</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    fileSystemTree.addSubNode(node_wz);
    fileSystemTree.addSubNode(node_xzg);

    File node_wz_a </span>= <span style="color: #0000ff;">new</span> File(<span style="color: #800000;">"</span><span style="color: #800000;">/wz/a.txt</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    File node_wz_b </span>= <span style="color: #0000ff;">new</span> File(<span style="color: #800000;">"</span><span style="color: #800000;">/wz/b.txt</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    Directory node_wz_movies </span>= <span style="color: #0000ff;">new</span> Directory(<span style="color: #800000;">"</span><span style="color: #800000;">/wz/movies/</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    node_wz.addSubNode(node_wz_a);
    node_wz.addSubNode(node_wz_b);
    node_wz.addSubNode(node_wz_movies);

    File node_wz_movies_c </span>= <span style="color: #0000ff;">new</span> File(<span style="color: #800000;">"</span><span style="color: #800000;">/wz/movies/c.avi</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    node_wz_movies.addSubNode(node_wz_movies_c);

    Directory node_xzg_docs </span>= <span style="color: #0000ff;">new</span> Directory(<span style="color: #800000;">"</span><span style="color: #800000;">/xzg/docs/</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    node_xzg.addSubNode(node_xzg_docs);

    File node_xzg_docs_d </span>= <span style="color: #0000ff;">new</span> File(<span style="color: #800000;">"</span><span style="color: #800000;">/xzg/docs/d.txt</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    node_xzg_docs.addSubNode(node_xzg_docs_d);

    System.</span><span style="color: #0000ff;">out</span>.println(<span style="color: #800000;">"</span><span style="color: #800000;">/ files num:</span><span style="color: #800000;">"</span> +<span style="color: #000000;"> fileSystemTree.countNumOfFiles());
    System.</span><span style="color: #0000ff;">out</span>.println(<span style="color: #800000;">"</span><span style="color: #800000;">/wz/ files num:</span><span style="color: #800000;">"</span> +<span style="color: #000000;"> node_wz.countNumOfFiles());
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">调用</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('508a0345-ae6e-4a95-b088-0ee1fcbc136b')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_508a0345-ae6e-4a95-b088-0ee1fcbc136b" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_508a0345-ae6e-4a95-b088-0ee1fcbc136b" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_508a0345-ae6e-4a95-b088-0ee1fcbc136b" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> HumanResource {
  </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">long</span><span style="color: #000000;"> id;
  </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">double</span><span style="color: #000000;"> salary;

  </span><span style="color: #0000ff;">public</span> HumanResource(<span style="color: #0000ff;">long</span><span style="color: #000000;"> id) {
    </span><span style="color: #0000ff;">this</span>.id =<span style="color: #000000;"> id;
  }

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">long</span><span style="color: #000000;"> getId() {
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> id;
  }

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">double</span><span style="color: #000000;"> calculateSalary();
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Employee extends HumanResource {
  </span><span style="color: #0000ff;">public</span> Employee(<span style="color: #0000ff;">long</span> id, <span style="color: #0000ff;">double</span><span style="color: #000000;"> salary) {
    super(id);
    </span><span style="color: #0000ff;">this</span>.salary =<span style="color: #000000;"> salary;
  }

  @Override
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">double</span><span style="color: #000000;"> calculateSalary() {
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> salary;
  }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Department extends HumanResource {
  </span><span style="color: #0000ff;">private</span> List&lt;HumanResource&gt; subNodes = <span style="color: #0000ff;">new</span> ArrayList&lt;&gt;<span style="color: #000000;">();

  </span><span style="color: #0000ff;">public</span> Department(<span style="color: #0000ff;">long</span><span style="color: #000000;"> id) {
    super(id);
  }

  @Override
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">double</span><span style="color: #000000;"> calculateSalary() {
    </span><span style="color: #0000ff;">double</span> totalSalary = <span style="color: #800080;">0</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> (HumanResource hr : subNodes) {
      totalSalary </span>+=<span style="color: #000000;"> hr.calculateSalary();
    }
    </span><span style="color: #0000ff;">this</span>.salary =<span style="color: #000000;"> totalSalary;
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> totalSalary;
  }

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> addSubNode(HumanResource hr) {
    subNodes.add(hr);
  }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 构建组织架构的代码</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Demo {
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> final <span style="color: #0000ff;">long</span> ORGANIZATION_ROOT_ID = <span style="color: #800080;">1001</span><span style="color: #000000;">;
  </span><span style="color: #0000ff;">private</span> DepartmentRepo departmentRepo; <span style="color: #008000;">//</span><span style="color: #008000;"> 依赖注入</span>
  <span style="color: #0000ff;">private</span> EmployeeRepo employeeRepo; <span style="color: #008000;">//</span><span style="color: #008000;"> 依赖注入</span>

  <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> buildOrganization() {
    Department rootDepartment </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> Department(ORGANIZATION_ROOT_ID);
    buildOrganization(rootDepartment);
  }

  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> buildOrganization(Department department) {
    List</span>&lt;Long&gt; subDepartmentIds =<span style="color: #000000;"> departmentRepo.getSubDepartmentIds(department.getId());
    </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> (Long subDepartmentId : subDepartmentIds) {
      Department subDepartment </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> Department(subDepartmentId);
      department.addSubNode(subDepartment);
      buildOrganization(subDepartment);
    }
    List</span>&lt;Long&gt; employeeIds =<span style="color: #000000;"> employeeRepo.getDepartmentEmployeeIds(department.getId());
    </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> (Long employeeId : employeeIds) {
      </span><span style="color: #0000ff;">double</span> salary =<span style="color: #000000;"> employeeRepo.getEmployeeSalary(employeeId);
      department.addSubNode(</span><span style="color: #0000ff;">new</span><span style="color: #000000;"> Employee(employeeId, salary));
    }
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">我们再拿组合模式的定义跟这个例子对照一下：&ldquo;将一组对象（员工和部门）组织成树形结构，以表示一种&lsquo;部分 - 整体&rsquo;的层次结构（部门与子部门的嵌套结构）。组合模式让客户端可以统一单个对象（员工）和组合对象（部门）的处理逻辑（递归遍历）。</span></div>
<p>&nbsp;</p>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">7，享元模式</span></strong></span></p>
<p>当一个系统中存在大量重复对象的时候，我们就可以利用享元模式，将对象设计成享元，在内存中只保留一份实例，供多处代码引用，这样可以减少内存中对象的数量，以起到节省内存的目的</p>
<p>①享元模式的实现</p>
<p>享元模式的代码实现非常简单，主要是通过工厂模式，在工厂类中，通过一个 Map 或者 List 来缓存已经创建好的享元对象，以达到复用的目的。</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('2fe7f2bb-a672-492a-8f78-96b0a745b2bf')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_2fe7f2bb-a672-492a-8f78-96b0a745b2bf" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_2fe7f2bb-a672-492a-8f78-96b0a745b2bf" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_2fe7f2bb-a672-492a-8f78-96b0a745b2bf" class="cnblogs_code_hide">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> 享元类</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ChessPieceUnit {
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">int</span><span style="color: #000000;"> id;
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> String text;
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> Color color;

  </span><span style="color: #0000ff;">public</span> ChessPieceUnit(<span style="color: #0000ff;">int</span><span style="color: #000000;"> id, String text, Color color) {
    </span><span style="color: #0000ff;">this</span>.id =<span style="color: #000000;"> id;
    </span><span style="color: #0000ff;">this</span>.text =<span style="color: #000000;"> text;
    </span><span style="color: #0000ff;">this</span>.color =<span style="color: #000000;"> color;
  }

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">enum</span><span style="color: #000000;"> Color {
    RED, BLACK
  }

  </span><span style="color: #008000;">//</span><span style="color: #008000;"> ...省略其他属性和getter方法...</span>
<span style="color: #000000;">}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ChessPieceUnitFactory {
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> final Map&lt;Integer, ChessPieceUnit&gt; pieces = <span style="color: #0000ff;">new</span> HashMap&lt;&gt;<span style="color: #000000;">();

  </span><span style="color: #0000ff;">static</span><span style="color: #000000;"> {
    pieces.put(</span><span style="color: #800080;">1</span>, <span style="color: #0000ff;">new</span> ChessPieceUnit(<span style="color: #800080;">1</span>, <span style="color: #800000;">"</span><span style="color: #800000;">車</span><span style="color: #800000;">"</span><span style="color: #000000;">, ChessPieceUnit.Color.BLACK));
    pieces.put(</span><span style="color: #800080;">2</span>, <span style="color: #0000ff;">new</span> ChessPieceUnit(<span style="color: #800080;">2</span>,<span style="color: #800000;">"</span><span style="color: #800000;">馬</span><span style="color: #800000;">"</span><span style="color: #000000;">, ChessPieceUnit.Color.BLACK));
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...省略摆放其他棋子的代码...</span>
<span style="color: #000000;">  }

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> ChessPieceUnit getChessPiece(<span style="color: #0000ff;">int</span><span style="color: #000000;"> chessPieceId) {
    </span><span style="color: #0000ff;">return</span> pieces.<span style="color: #0000ff;">get</span><span style="color: #000000;">(chessPieceId);
  }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ChessPiece {
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> ChessPieceUnit chessPieceUnit;
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">int</span><span style="color: #000000;"> positionX;
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">int</span><span style="color: #000000;"> positionY;

  </span><span style="color: #0000ff;">public</span> ChessPiece(ChessPieceUnit unit, <span style="color: #0000ff;">int</span> positionX, <span style="color: #0000ff;">int</span><span style="color: #000000;"> positionY) {
    </span><span style="color: #0000ff;">this</span>.chessPieceUnit =<span style="color: #000000;"> unit;
    </span><span style="color: #0000ff;">this</span>.positionX =<span style="color: #000000;"> positionX;
    </span><span style="color: #0000ff;">this</span>.positionY =<span style="color: #000000;"> positionY;
  }
  </span><span style="color: #008000;">//</span><span style="color: #008000;"> 省略getter、setter方法</span>
<span style="color: #000000;">}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ChessBoard {
  </span><span style="color: #0000ff;">private</span> Map&lt;Integer, ChessPiece&gt; chessPieces = <span style="color: #0000ff;">new</span> HashMap&lt;&gt;<span style="color: #000000;">();

  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> ChessBoard() {
    init();
  }

  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> init() {
    chessPieces.put(</span><span style="color: #800080;">1</span>, <span style="color: #0000ff;">new</span><span style="color: #000000;"> ChessPiece(
            ChessPieceUnitFactory.getChessPiece(</span><span style="color: #800080;">1</span>), <span style="color: #800080;">0</span>,<span style="color: #800080;">0</span><span style="color: #000000;">));
    chessPieces.put(</span><span style="color: #800080;">1</span>, <span style="color: #0000ff;">new</span><span style="color: #000000;"> ChessPiece(
            ChessPieceUnitFactory.getChessPiece(</span><span style="color: #800080;">2</span>), <span style="color: #800080;">1</span>,<span style="color: #800080;">0</span><span style="color: #000000;">));
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...省略摆放其他棋子的代码...</span>
<span style="color: #000000;">  }

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> move(<span style="color: #0000ff;">int</span> chessPieceId, <span style="color: #0000ff;">int</span> toPositionX, <span style="color: #0000ff;">int</span><span style="color: #000000;"> toPositionY) {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...省略...</span>
<span style="color: #000000;">  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">示例代码</span></div>
<p>②享元模式vs单例、缓存、对象池</p>
<p>享元模式：为了实现对象复用，节省内存</p>
<p>单例模式：为了保证对象全局唯一</p>
<p>缓存：是为了提高访问效率，而非复用</p>
<p>对象池：池化技术中的&ldquo;复用&rdquo;理解为&ldquo;重复使用&rdquo;，主要是为了节省时间，提高性能</p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: #169fe6;"><span style="color: #ffffff;"><strong>七、设计模式与范式：行为型</strong></span></p>
<p><span style="font-size: 12px; color: #808080;">行为型设计模式主要解决的就是&ldquo;类或对象之间的交互&rdquo;问题</span></p>
<p><span style="font-size: 12px; color: #808080;">行为型模式是将不同的行为代码解耦</span></p>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">1，观察者模式</span></strong></span></p>
<p>在对象之间定义一个一对多的依赖，当一个对象状态改变的时候，所有依赖的对象都会自动收到通知</p>
<p>根据应用场景的不同，观察者模式会对应不同的代码实现方式：</p>
<p><span style="font-size: 12px;">同步阻塞是最经典的实现方式，主要是为了代码解耦</span></p>
<p><span style="font-size: 12px;">异步非阻塞除了能实现代码解耦之外，还能提高代码的执行效率</span></p>
<p><span style="font-size: 12px;">进程间的观察者模式解耦更加彻底，一般是基于消息队列来实现，用来实现不同进程间的被观察者和观察者之间的交互</span></p>
<p>一般情况下，被依赖的对象叫作被观察者（Observable），依赖的对象叫作观察者（Observer）。不过，在实际的项目开发中，这两种对象的称呼是比较灵活的，有各种不同的叫法，比如：Subject-Observer、Publisher-Subscriber、Producer-Consumer、EventEmitter-EventListener、Dispatcher-Listener。不管怎么称呼，只要应用场景符合刚刚给出的定义，都可以看作观察者模式</p>
<p>&nbsp;</p>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">2，模板方法</span></strong></span></p>
<p>模板方法模式在一个方法中定义一个算法骨架，并将某些步骤推迟到子类中实现。模板方法模式可以让子类在不改变算法整体结构的情况下，重新定义算法中的某些步骤</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('6b543123-c837-4adf-b810-32a65c1c7a03')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_6b543123-c837-4adf-b810-32a65c1c7a03" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_6b543123-c837-4adf-b810-32a65c1c7a03" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_6b543123-c837-4adf-b810-32a65c1c7a03" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> AbstractClass {
  </span><span style="color: #0000ff;">public</span> final <span style="color: #0000ff;">void</span><span style="color: #000000;"> templateMethod() {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">    method1();
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">    method2();
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">  }
  
  </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> method1();
  </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> method2();
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ConcreteClass1 extends AbstractClass {
  @Override
  </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> method1() {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">  }
  
  @Override
  </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> method2() {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">  }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ConcreteClass2 extends AbstractClass {
  @Override
  </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> method1() {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">  }
  
  @Override
  </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> method2() {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">  }
}

AbstractClass demo </span>=<span style="color: #000000;"> ConcreteClass1();
demo.templateMethod();</span></pre>
</div>
<span class="cnblogs_code_collapse">魔板方法示例</span></div>
<p>模板模式主要是用来解决复用和扩展两个问题</p>
<p>复用指的是，所有的子类可以复用父类中提供的模板方法的代码</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('c0234707-5aec-48c5-8283-46b77c437e61')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_c0234707-5aec-48c5-8283-46b77c437e61" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_c0234707-5aec-48c5-8283-46b77c437e61" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_c0234707-5aec-48c5-8283-46b77c437e61" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> InputStream implements Closeable {
  </span><span style="color: #008000;">//</span><span style="color: #008000;">...省略其他代码...</span>
  
  <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span> read(<span style="color: #0000ff;">byte</span> b[], <span style="color: #0000ff;">int</span> off, <span style="color: #0000ff;">int</span><span style="color: #000000;"> len) throws IOException {
    </span><span style="color: #0000ff;">if</span> (b == <span style="color: #0000ff;">null</span><span style="color: #000000;">) {
      </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> NullPointerException();
    } </span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span> (off &lt; <span style="color: #800080;">0</span> || len &lt; <span style="color: #800080;">0</span> || len &gt; b.length -<span style="color: #000000;"> off) {
      </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> IndexOutOfBoundsException();
    } </span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span> (len == <span style="color: #800080;">0</span><span style="color: #000000;">) {
      </span><span style="color: #0000ff;">return</span> <span style="color: #800080;">0</span><span style="color: #000000;">;
    }

    </span><span style="color: #0000ff;">int</span> c =<span style="color: #000000;"> read();
    </span><span style="color: #0000ff;">if</span> (c == -<span style="color: #800080;">1</span><span style="color: #000000;">) {
      </span><span style="color: #0000ff;">return</span> -<span style="color: #800080;">1</span><span style="color: #000000;">;
    }
    b[off] </span>= (<span style="color: #0000ff;">byte</span><span style="color: #000000;">)c;

    </span><span style="color: #0000ff;">int</span> i = <span style="color: #800080;">1</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">try</span><span style="color: #000000;"> {
      </span><span style="color: #0000ff;">for</span> (; i &lt; len ; i++<span style="color: #000000;">) {
        c </span>=<span style="color: #000000;"> read();
        </span><span style="color: #0000ff;">if</span> (c == -<span style="color: #800080;">1</span><span style="color: #000000;">) {
          </span><span style="color: #0000ff;">break</span><span style="color: #000000;">;
        }
        b[off </span>+ i] = (<span style="color: #0000ff;">byte</span><span style="color: #000000;">)c;
      }
    } </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (IOException ee) {
    }
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> i;
  }
  
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">int</span><span style="color: #000000;"> read() throws IOException;
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ByteArrayInputStream extends InputStream {
  </span><span style="color: #008000;">//</span><span style="color: #008000;">...省略其他代码...</span>
<span style="color: #000000;">  
  @Override
  </span><span style="color: #0000ff;">public</span> synchronized <span style="color: #0000ff;">int</span><span style="color: #000000;"> read() {
    </span><span style="color: #0000ff;">return</span> (pos &lt; count) ? (buf[pos++] &amp; <span style="color: #800080;">0xff</span>) : -<span style="color: #800080;">1</span><span style="color: #000000;">;
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">复用-Java InputStream。read() 函数是一个模板方法，定义了读取数据的整个流程，并且暴露了一个可以由子类来定制的抽象方法。不过这个方法也被命名为了 read()，只是参数跟模板方法不同</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('8cf33a54-6803-46bc-a6d3-c02ca2badeba')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_8cf33a54-6803-46bc-a6d3-c02ca2badeba" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_8cf33a54-6803-46bc-a6d3-c02ca2badeba" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_8cf33a54-6803-46bc-a6d3-c02ca2badeba" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> boolean addAll(<span style="color: #0000ff;">int</span> index, Collection&lt;? extends E&gt;<span style="color: #000000;"> c) {
    rangeCheckForAdd(index);
    boolean modified </span>= <span style="color: #0000ff;">false</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> (E e : c) {
        add(index</span>++<span style="color: #000000;">, e);
        modified </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">;
    }
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> modified;
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> add(<span style="color: #0000ff;">int</span><span style="color: #000000;"> index, E element) {
    </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> UnsupportedOperationException();
}</span></pre>
</div>
<span class="cnblogs_code_collapse">复用-Java AbstractList。在 Java AbstractList 类中，addAll() 函数可以看作模板方法，add() 是子类需要重写的方法，尽管没有声明为 abstract 的，但函数实现直接抛出了 UnsupportedOperationException 异常。前提是，如果子类不重写是不能使用的。</span></div>
<p>扩展指的是，框架通过模板模式提供功能扩展点，让框架用户可以在不修改框架源码的情况下，基于扩展点定制化框架的功能</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('30d79487-d657-4fe0-b87f-17f8ce92a5c5')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_30d79487-d657-4fe0-b87f-17f8ce92a5c5" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_30d79487-d657-4fe0-b87f-17f8ce92a5c5" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_30d79487-d657-4fe0-b87f-17f8ce92a5c5" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> service(ServletRequest req, ServletResponse res)
    throws ServletException, IOException
{
    HttpServletRequest  request;
    HttpServletResponse response;
    </span><span style="color: #0000ff;">if</span> (!(req instanceof HttpServletRequest &amp;&amp;<span style="color: #000000;">
            res instanceof HttpServletResponse)) {
        </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> ServletException(<span style="color: #800000;">"</span><span style="color: #800000;">non-HTTP request or response</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    }
    request </span>=<span style="color: #000000;"> (HttpServletRequest) req;
    response </span>=<span style="color: #000000;"> (HttpServletResponse) res;
    service(request, response);
}

</span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> service(HttpServletRequest req, HttpServletResponse resp)
    throws ServletException, IOException
{
    String method </span>=<span style="color: #000000;"> req.getMethod();
    </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (method.equals(METHOD_GET)) {
        </span><span style="color: #0000ff;">long</span> lastModified =<span style="color: #000000;"> getLastModified(req);
        </span><span style="color: #0000ff;">if</span> (lastModified == -<span style="color: #800080;">1</span><span style="color: #000000;">) {
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> servlet doesn't support if-modified-since, no reason
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> to go through further expensive logic</span>
<span style="color: #000000;">            doGet(req, resp);
        } </span><span style="color: #0000ff;">else</span><span style="color: #000000;"> {
            </span><span style="color: #0000ff;">long</span> ifModifiedSince =<span style="color: #000000;"> req.getDateHeader(HEADER_IFMODSINCE);
            </span><span style="color: #0000ff;">if</span> (ifModifiedSince &lt;<span style="color: #000000;"> lastModified) {
                </span><span style="color: #008000;">//</span><span style="color: #008000;"> If the servlet mod time is later, call doGet()
                </span><span style="color: #008000;">//</span><span style="color: #008000;"> Round down to the nearest second for a proper compare
                </span><span style="color: #008000;">//</span><span style="color: #008000;"> A ifModifiedSince of -1 will always be less</span>
<span style="color: #000000;">                maybeSetLastModified(resp, lastModified);
                doGet(req, resp);
            } </span><span style="color: #0000ff;">else</span><span style="color: #000000;"> {
                resp.setStatus(HttpServletResponse.SC_NOT_MODIFIED);
            }
        }
    } </span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span><span style="color: #000000;"> (method.equals(METHOD_HEAD)) {
        </span><span style="color: #0000ff;">long</span> lastModified =<span style="color: #000000;"> getLastModified(req);
        maybeSetLastModified(resp, lastModified);
        doHead(req, resp);
    } </span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span><span style="color: #000000;"> (method.equals(METHOD_POST)) {
        doPost(req, resp);
    } </span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span><span style="color: #000000;"> (method.equals(METHOD_PUT)) {
        doPut(req, resp);
    } </span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span><span style="color: #000000;"> (method.equals(METHOD_DELETE)) {
        doDelete(req, resp);
    } </span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span><span style="color: #000000;"> (method.equals(METHOD_OPTIONS)) {
        doOptions(req,resp);
    } </span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span><span style="color: #000000;"> (method.equals(METHOD_TRACE)) {
        doTrace(req,resp);
    } </span><span style="color: #0000ff;">else</span><span style="color: #000000;"> {
        String errMsg </span>= lStrings.getString(<span style="color: #800000;">"</span><span style="color: #800000;">http.method_not_implemented</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        Object[] errArgs </span>= <span style="color: #0000ff;">new</span> Object[<span style="color: #800080;">1</span><span style="color: #000000;">];
        errArgs[</span><span style="color: #800080;">0</span>] =<span style="color: #000000;"> method;
        errMsg </span>=<span style="color: #000000;"> MessageFormat.format(errMsg, errArgs);
        resp.sendError(HttpServletResponse.SC_NOT_IMPLEMENTED, errMsg);
    }
}




</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> HelloServlet extends HttpServlet {
  @Override
  </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    </span><span style="color: #0000ff;">this</span><span style="color: #000000;">.doPost(req, resp);
  }
  
  @Override
  </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    resp.getWriter().write(</span><span style="color: #800000;">"</span><span style="color: #800000;">Hello World.</span><span style="color: #800000;">"</span><span style="color: #000000;">);
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">HttpServlet 的 service() 方法就是一个模板方法，它实现了整个 HTTP 请求的执行流程，doGet()、doPost() 是模板中可以由子类来定制的部分。实际上，这就相当于 Servlet 框架提供了一个扩展点（doGet()、doPost() 方法），让框架用户在不用修改 Servlet 框架源码的情况下，将业务代码通过扩展点镶嵌到框架中执行</span></div>
<p>&nbsp;</p>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">3，策略模式</span></strong></span></p>
<p>定义一族算法类，将每个算法分别封装起来，让它们可以互相替换。策略模式可以使算法的变化独立于使用它们的客户端（这里的客户端代指使用算法的代码）</p>
<p>①策略的定义</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('52db6df3-d80b-41a8-a4ff-57ae1727d59f')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_52db6df3-d80b-41a8-a4ff-57ae1727d59f" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_52db6df3-d80b-41a8-a4ff-57ae1727d59f" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_52db6df3-d80b-41a8-a4ff-57ae1727d59f" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> Strategy {
  </span><span style="color: #0000ff;">void</span><span style="color: #000000;"> algorithmInterface();
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ConcreteStrategyA implements Strategy {
  @Override
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;">  algorithmInterface() {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">具体的算法...</span>
<span style="color: #000000;">  }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ConcreteStrategyB implements Strategy {
  @Override
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;">  algorithmInterface() {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">具体的算法...</span>
<span style="color: #000000;">  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">包含一个策略接口和一组实现这个接口的策略类</span></div>
<p>②策略的创建</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('3a1b7087-ecde-4de6-a3f5-866572966841')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_3a1b7087-ecde-4de6-a3f5-866572966841" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_3a1b7087-ecde-4de6-a3f5-866572966841" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_3a1b7087-ecde-4de6-a3f5-866572966841" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> StrategyFactory {
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> final Map&lt;String, Strategy&gt; strategies = <span style="color: #0000ff;">new</span> HashMap&lt;&gt;<span style="color: #000000;">();

  </span><span style="color: #0000ff;">static</span><span style="color: #000000;"> {
    strategies.put(</span><span style="color: #800000;">"</span><span style="color: #800000;">A</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span><span style="color: #000000;"> ConcreteStrategyA());
    strategies.put(</span><span style="color: #800000;">"</span><span style="color: #800000;">B</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span><span style="color: #000000;"> ConcreteStrategyB());
  }

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> Strategy getStrategy(String type) {
    </span><span style="color: #0000ff;">if</span> (type == <span style="color: #0000ff;">null</span> ||<span style="color: #000000;"> type.isEmpty()) {
      </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> IllegalArgumentException(<span style="color: #800000;">"</span><span style="color: #800000;">type should not be empty.</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    }
    </span><span style="color: #0000ff;">return</span> strategies.<span style="color: #0000ff;">get</span><span style="color: #000000;">(type);
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">因为策略模式会包含一组策略，在使用它们的时候，一般会通过类型（type）来判断创建哪个策略来使用。为了封装创建逻辑，我们需要对客户端代码屏蔽创建细节。我们可以把根据 type 创建策略的逻辑抽离出来，放到工厂类中。如果策略类是无状态的，不包含成员变量，只是纯粹的算法实现，这样的策略对象是可以被共享使用的，不需要在每次调用 getStrategy() 的时候，都创建一个新的策略对象。针对这种情况，我们可以使用上面这种工厂类的实现方式，事先创建好每个策略对象，缓存到工厂类中，用的时候直接返回</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('57e5ba36-f132-4178-a6d9-2f79710d7383')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_57e5ba36-f132-4178-a6d9-2f79710d7383" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_57e5ba36-f132-4178-a6d9-2f79710d7383" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_57e5ba36-f132-4178-a6d9-2f79710d7383" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> StrategyFactory {
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> Strategy getStrategy(String type) {
    </span><span style="color: #0000ff;">if</span> (type == <span style="color: #0000ff;">null</span> ||<span style="color: #000000;"> type.isEmpty()) {
      </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> IllegalArgumentException(<span style="color: #800000;">"</span><span style="color: #800000;">type should not be empty.</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    }

    </span><span style="color: #0000ff;">if</span> (type.equals(<span style="color: #800000;">"</span><span style="color: #800000;">A</span><span style="color: #800000;">"</span><span style="color: #000000;">)) {
      </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> ConcreteStrategyA();
    } </span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span> (type.equals(<span style="color: #800000;">"</span><span style="color: #800000;">B</span><span style="color: #800000;">"</span><span style="color: #000000;">)) {
      </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> ConcreteStrategyB();
    }

    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">null</span><span style="color: #000000;">;
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">如果策略类是有状态的，根据业务场景的需要，我们希望每次从工厂方法中，获得的都是新创建的策略对象，而不是缓存好可共享的策略对象，那我们就需要按照如下方式来实现策略工厂类</span></div>
<p>③策略的使用</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('3383df6a-17fc-43d3-8d82-34bad63793d4')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_3383df6a-17fc-43d3-8d82-34bad63793d4" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_3383df6a-17fc-43d3-8d82-34bad63793d4" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_3383df6a-17fc-43d3-8d82-34bad63793d4" class="cnblogs_code_hide">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> 策略接口：EvictionStrategy
</span><span style="color: #008000;">//</span><span style="color: #008000;"> 策略类：LruEvictionStrategy、FifoEvictionStrategy、LfuEvictionStrategy...
</span><span style="color: #008000;">//</span><span style="color: #008000;"> 策略工厂：EvictionStrategyFactory</span>

<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> UserCache {
  </span><span style="color: #0000ff;">private</span> Map&lt;String, User&gt; cacheData = <span style="color: #0000ff;">new</span> HashMap&lt;&gt;<span style="color: #000000;">();
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> EvictionStrategy eviction;

  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> UserCache(EvictionStrategy eviction) {
    </span><span style="color: #0000ff;">this</span>.eviction =<span style="color: #000000;"> eviction;
  }

  </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 运行时动态确定，根据配置文件的配置决定使用哪种策略</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Application {
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> main(String[] args) throws Exception {
    EvictionStrategy evictionStrategy </span>= <span style="color: #0000ff;">null</span><span style="color: #000000;">;
    Properties props </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> Properties();
    props.load(</span><span style="color: #0000ff;">new</span> FileInputStream(<span style="color: #800000;">"</span><span style="color: #800000;">./config.properties</span><span style="color: #800000;">"</span><span style="color: #000000;">));
    String type </span>= props.getProperty(<span style="color: #800000;">"</span><span style="color: #800000;">eviction_type</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    evictionStrategy </span>=<span style="color: #000000;"> EvictionStrategyFactory.getEvictionStrategy(type);
    UserCache userCache </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> UserCache(evictionStrategy);
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">  }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 非运行时动态确定，在代码中指定使用哪种策略</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Application {
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> main(String[] args) {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
    EvictionStrategy evictionStrategy = <span style="color: #0000ff;">new</span><span style="color: #000000;"> LruEvictionStrategy();
    UserCache userCache </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> UserCache(evictionStrategy);
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">示例代码</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('fd98de4a-d8a2-4346-bf0f-140c8ec17b42')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_fd98de4a-d8a2-4346-bf0f-140c8ec17b42" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_fd98de4a-d8a2-4346-bf0f-140c8ec17b42" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_fd98de4a-d8a2-4346-bf0f-140c8ec17b42" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> OrderService {
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">double</span><span style="color: #000000;"> discount(Order order) {
    </span><span style="color: #0000ff;">double</span> discount = <span style="color: #800080;">0.0</span><span style="color: #000000;">;
    OrderType type </span>=<span style="color: #000000;"> order.getType();
    </span><span style="color: #0000ff;">if</span> (type.equals(OrderType.NORMAL)) { <span style="color: #008000;">//</span><span style="color: #008000;"> 普通订单
      </span><span style="color: #008000;">//</span><span style="color: #008000;">...省略折扣计算算法代码</span>
    } <span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span> (type.equals(OrderType.GROUPON)) { <span style="color: #008000;">//</span><span style="color: #008000;"> 团购订单
      </span><span style="color: #008000;">//</span><span style="color: #008000;">...省略折扣计算算法代码</span>
    } <span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span> (type.equals(OrderType.PROMOTION)) { <span style="color: #008000;">//</span><span style="color: #008000;"> 促销订单
      </span><span style="color: #008000;">//</span><span style="color: #008000;">...省略折扣计算算法代码</span>
<span style="color: #000000;">    }
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> discount;
  }
}



</span><span style="color: #008000;">//</span><span style="color: #008000;"> 策略的定义</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> DiscountStrategy {
  </span><span style="color: #0000ff;">double</span><span style="color: #000000;"> calDiscount(Order order);
}
</span><span style="color: #008000;">//</span><span style="color: #008000;"> 省略NormalDiscountStrategy、GrouponDiscountStrategy、PromotionDiscountStrategy类代码...

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 策略的创建</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> DiscountStrategyFactory {
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> final Map&lt;OrderType, DiscountStrategy&gt; strategies = <span style="color: #0000ff;">new</span> HashMap&lt;&gt;<span style="color: #000000;">();

  </span><span style="color: #0000ff;">static</span><span style="color: #000000;"> {
    strategies.put(OrderType.NORMAL, </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> NormalDiscountStrategy());
    strategies.put(OrderType.GROUPON, </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> GrouponDiscountStrategy());
    strategies.put(OrderType.PROMOTION, </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> PromotionDiscountStrategy());
  }

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> DiscountStrategy getDiscountStrategy(OrderType type) {
    </span><span style="color: #0000ff;">return</span> strategies.<span style="color: #0000ff;">get</span><span style="color: #000000;">(type);
  }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 策略的使用</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> OrderService {
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">double</span><span style="color: #000000;"> discount(Order order) {
    OrderType type </span>=<span style="color: #000000;"> order.getType();
    DiscountStrategy discountStrategy </span>=<span style="color: #000000;"> DiscountStrategyFactory.getDiscountStrategy(type);
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> discountStrategy.calDiscount(order);
  }
}


</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> DiscountStrategyFactory {
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> DiscountStrategy getDiscountStrategy(OrderType type) {
    </span><span style="color: #0000ff;">if</span> (type == <span style="color: #0000ff;">null</span><span style="color: #000000;">) {
      </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> IllegalArgumentException(<span style="color: #800000;">"</span><span style="color: #800000;">Type should not be null.</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    }
    </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (type.equals(OrderType.NORMAL)) {
      </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> NormalDiscountStrategy();
    } </span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span><span style="color: #000000;"> (type.equals(OrderType.GROUPON)) {
      </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> GrouponDiscountStrategy();
    } </span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span><span style="color: #000000;"> (type.equals(OrderType.PROMOTION)) {
      </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> PromotionDiscountStrategy();
    }
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">null</span><span style="color: #000000;">;
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">使用策略模式消除if else判断。本质上都是借助&ldquo;查表法&rdquo;，根据 type 查表（代码中的 strategies 就是表）替代根据 type 分支判断</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('8cc218d2-4c74-4843-bde7-7d4ad0922b2b')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_8cc218d2-4c74-4843-bde7-7d4ad0922b2b" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_8cc218d2-4c74-4843-bde7-7d4ad0922b2b" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_8cc218d2-4c74-4843-bde7-7d4ad0922b2b" class="cnblogs_code_hide">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">原始代码</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Sorter {
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> final <span style="color: #0000ff;">long</span> GB = <span style="color: #800080;">1000</span> * <span style="color: #800080;">1000</span> * <span style="color: #800080;">1000</span><span style="color: #000000;">;

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> sortFile(String filePath) {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 省略校验逻辑</span>
    File file = <span style="color: #0000ff;">new</span><span style="color: #000000;"> File(filePath);
    </span><span style="color: #0000ff;">long</span> fileSize =<span style="color: #000000;"> file.length();
    </span><span style="color: #0000ff;">if</span> (fileSize &lt; <span style="color: #800080;">6</span> * GB) { <span style="color: #008000;">//</span><span style="color: #008000;"> [0, 6GB)</span>
<span style="color: #000000;">      quickSort(filePath);
    } </span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span> (fileSize &lt; <span style="color: #800080;">10</span> * GB) { <span style="color: #008000;">//</span><span style="color: #008000;"> [6GB, 10GB)</span>
<span style="color: #000000;">      externalSort(filePath);
    } </span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span> (fileSize &lt; <span style="color: #800080;">100</span> * GB) { <span style="color: #008000;">//</span><span style="color: #008000;"> [10GB, 100GB)</span>
<span style="color: #000000;">      concurrentExternalSort(filePath);
    } </span><span style="color: #0000ff;">else</span> { <span style="color: #008000;">//</span><span style="color: #008000;"> [100GB, ~)</span>
<span style="color: #000000;">      mapreduceSort(filePath);
    }
  }

  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> quickSort(String filePath) {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 快速排序</span>
<span style="color: #000000;">  }

  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> externalSort(String filePath) {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 外部排序</span>
<span style="color: #000000;">  }

  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> concurrentExternalSort(String filePath) {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 多线程外部排序</span>
<span style="color: #000000;">  }

  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> mapreduceSort(String filePath) {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 利用MapReduce多机排序</span>
<span style="color: #000000;">  }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SortingTool {
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> main(String[] args) {
    Sorter sorter </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> Sorter();
    sorter.sortFile(args[</span><span style="color: #800080;">0</span><span style="color: #000000;">]);
  }
}


</span><span style="color: #008000;">//</span><span style="color: #008000;">第一次优化。这一步实际上就是策略模式的第一步，也就是将策略的定义分离出来</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> ISortAlg {
  </span><span style="color: #0000ff;">void</span><span style="color: #000000;"> sort(String filePath);
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> QuickSort implements ISortAlg {
  @Override
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> sort(String filePath) {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">  }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ExternalSort implements ISortAlg {
  @Override
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> sort(String filePath) {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">  }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ConcurrentExternalSort implements ISortAlg {
  @Override
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> sort(String filePath) {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">  }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MapReduceSort implements ISortAlg {
  @Override
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> sort(String filePath) {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
<span style="color: #000000;">  }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Sorter {
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> final <span style="color: #0000ff;">long</span> GB = <span style="color: #800080;">1000</span> * <span style="color: #800080;">1000</span> * <span style="color: #800080;">1000</span><span style="color: #000000;">;

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> sortFile(String filePath) {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 省略校验逻辑</span>
    File file = <span style="color: #0000ff;">new</span><span style="color: #000000;"> File(filePath);
    </span><span style="color: #0000ff;">long</span> fileSize =<span style="color: #000000;"> file.length();
    ISortAlg sortAlg;
    </span><span style="color: #0000ff;">if</span> (fileSize &lt; <span style="color: #800080;">6</span> * GB) { <span style="color: #008000;">//</span><span style="color: #008000;"> [0, 6GB)</span>
      sortAlg = <span style="color: #0000ff;">new</span><span style="color: #000000;"> QuickSort();
    } </span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span> (fileSize &lt; <span style="color: #800080;">10</span> * GB) { <span style="color: #008000;">//</span><span style="color: #008000;"> [6GB, 10GB)</span>
      sortAlg = <span style="color: #0000ff;">new</span><span style="color: #000000;"> ExternalSort();
    } </span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span> (fileSize &lt; <span style="color: #800080;">100</span> * GB) { <span style="color: #008000;">//</span><span style="color: #008000;"> [10GB, 100GB)</span>
      sortAlg = <span style="color: #0000ff;">new</span><span style="color: #000000;"> ConcurrentExternalSort();
    } </span><span style="color: #0000ff;">else</span> { <span style="color: #008000;">//</span><span style="color: #008000;"> [100GB, ~)</span>
      sortAlg = <span style="color: #0000ff;">new</span><span style="color: #000000;"> MapReduceSort();
    }
    sortAlg.sort(filePath);
  }
}



</span><span style="color: #008000;">//</span><span style="color: #008000;">第二次优化。每种排序类都是无状态的，我们没必要在每次使用的时候，都重新创建一个新的对象。所以，我们可以使用工厂模式对对象的创建进行封装</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SortAlgFactory {
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> final Map&lt;String, ISortAlg&gt; algs = <span style="color: #0000ff;">new</span> HashMap&lt;&gt;<span style="color: #000000;">();

  </span><span style="color: #0000ff;">static</span><span style="color: #000000;"> {
    algs.put(</span><span style="color: #800000;">"</span><span style="color: #800000;">QuickSort</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span><span style="color: #000000;"> QuickSort());
    algs.put(</span><span style="color: #800000;">"</span><span style="color: #800000;">ExternalSort</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span><span style="color: #000000;"> ExternalSort());
    algs.put(</span><span style="color: #800000;">"</span><span style="color: #800000;">ConcurrentExternalSort</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span><span style="color: #000000;"> ConcurrentExternalSort());
    algs.put(</span><span style="color: #800000;">"</span><span style="color: #800000;">MapReduceSort</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span><span style="color: #000000;"> MapReduceSort());
  }

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> ISortAlg getSortAlg(String type) {
    </span><span style="color: #0000ff;">if</span> (type == <span style="color: #0000ff;">null</span> ||<span style="color: #000000;"> type.isEmpty()) {
      </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> IllegalArgumentException(<span style="color: #800000;">"</span><span style="color: #800000;">type should not be empty.</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    }
    </span><span style="color: #0000ff;">return</span> algs.<span style="color: #0000ff;">get</span><span style="color: #000000;">(type);
  }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Sorter {
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> final <span style="color: #0000ff;">long</span> GB = <span style="color: #800080;">1000</span> * <span style="color: #800080;">1000</span> * <span style="color: #800080;">1000</span><span style="color: #000000;">;

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> sortFile(String filePath) {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 省略校验逻辑</span>
    File file = <span style="color: #0000ff;">new</span><span style="color: #000000;"> File(filePath);
    </span><span style="color: #0000ff;">long</span> fileSize =<span style="color: #000000;"> file.length();
    ISortAlg sortAlg;
    </span><span style="color: #0000ff;">if</span> (fileSize &lt; <span style="color: #800080;">6</span> * GB) { <span style="color: #008000;">//</span><span style="color: #008000;"> [0, 6GB)</span>
      sortAlg = SortAlgFactory.getSortAlg(<span style="color: #800000;">"</span><span style="color: #800000;">QuickSort</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    } </span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span> (fileSize &lt; <span style="color: #800080;">10</span> * GB) { <span style="color: #008000;">//</span><span style="color: #008000;"> [6GB, 10GB)</span>
      sortAlg = SortAlgFactory.getSortAlg(<span style="color: #800000;">"</span><span style="color: #800000;">ExternalSort</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    } </span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span> (fileSize &lt; <span style="color: #800080;">100</span> * GB) { <span style="color: #008000;">//</span><span style="color: #008000;"> [10GB, 100GB)</span>
      sortAlg = SortAlgFactory.getSortAlg(<span style="color: #800000;">"</span><span style="color: #800000;">ConcurrentExternalSort</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    } </span><span style="color: #0000ff;">else</span> { <span style="color: #008000;">//</span><span style="color: #008000;"> [100GB, ~)</span>
      sortAlg = SortAlgFactory.getSortAlg(<span style="color: #800000;">"</span><span style="color: #800000;">MapReduceSort</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    }
    sortAlg.sort(filePath);
  }
}



</span><span style="color: #008000;">//</span><span style="color: #008000;">基于查表法来解决的，其中的&ldquo;algs&rdquo;就是&ldquo;表&rdquo;。消除if else</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Sorter {
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> final <span style="color: #0000ff;">long</span> GB = <span style="color: #800080;">1000</span> * <span style="color: #800080;">1000</span> * <span style="color: #800080;">1000</span><span style="color: #000000;">;
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> final List&lt;AlgRange&gt; algs = <span style="color: #0000ff;">new</span> ArrayList&lt;&gt;<span style="color: #000000;">();
  </span><span style="color: #0000ff;">static</span><span style="color: #000000;"> {
    algs.add(</span><span style="color: #0000ff;">new</span> AlgRange(<span style="color: #800080;">0</span>, <span style="color: #800080;">6</span>*GB, SortAlgFactory.getSortAlg(<span style="color: #800000;">"</span><span style="color: #800000;">QuickSort</span><span style="color: #800000;">"</span><span style="color: #000000;">)));
    algs.add(</span><span style="color: #0000ff;">new</span> AlgRange(<span style="color: #800080;">6</span>*GB, <span style="color: #800080;">10</span>*GB, SortAlgFactory.getSortAlg(<span style="color: #800000;">"</span><span style="color: #800000;">ExternalSort</span><span style="color: #800000;">"</span><span style="color: #000000;">)));
    algs.add(</span><span style="color: #0000ff;">new</span> AlgRange(<span style="color: #800080;">10</span>*GB, <span style="color: #800080;">100</span>*GB, SortAlgFactory.getSortAlg(<span style="color: #800000;">"</span><span style="color: #800000;">ConcurrentExternalSort</span><span style="color: #800000;">"</span><span style="color: #000000;">)));
    algs.add(</span><span style="color: #0000ff;">new</span> AlgRange(<span style="color: #800080;">100</span>*GB, Long.MAX_VALUE, SortAlgFactory.getSortAlg(<span style="color: #800000;">"</span><span style="color: #800000;">MapReduceSort</span><span style="color: #800000;">"</span><span style="color: #000000;">)));
  }

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> sortFile(String filePath) {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 省略校验逻辑</span>
    File file = <span style="color: #0000ff;">new</span><span style="color: #000000;"> File(filePath);
    </span><span style="color: #0000ff;">long</span> fileSize =<span style="color: #000000;"> file.length();
    ISortAlg sortAlg </span>= <span style="color: #0000ff;">null</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> (AlgRange algRange : algs) {
      </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (algRange.inRange(fileSize)) {
        sortAlg </span>=<span style="color: #000000;"> algRange.getAlg();
        </span><span style="color: #0000ff;">break</span><span style="color: #000000;">;
      }
    }
    sortAlg.sort(filePath);
  }

  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> AlgRange {
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">long</span><span style="color: #000000;"> start;
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">long</span><span style="color: #000000;"> end;
    </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> ISortAlg alg;

    </span><span style="color: #0000ff;">public</span> AlgRange(<span style="color: #0000ff;">long</span> start, <span style="color: #0000ff;">long</span><span style="color: #000000;"> end, ISortAlg alg) {
      </span><span style="color: #0000ff;">this</span>.start =<span style="color: #000000;"> start;
      </span><span style="color: #0000ff;">this</span>.end =<span style="color: #000000;"> end;
      </span><span style="color: #0000ff;">this</span>.alg =<span style="color: #000000;"> alg;
    }

    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> ISortAlg getAlg() {
      </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> alg;
    }

    </span><span style="color: #0000ff;">public</span> boolean inRange(<span style="color: #0000ff;">long</span><span style="color: #000000;"> size) {
      </span><span style="color: #0000ff;">return</span> size &gt;= start &amp;&amp; size &lt;<span style="color: #000000;"> end;
    }
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">通过使用策略模式优化代码</span></div>
<p>&nbsp;</p>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">4，职责链模式</span></strong></span></p>
<p>在职责链模式中，多个处理器依次处理同一个请求。一个请求先经过 A 处理器处理，然后再把请求传递给 B 处理器，B 处理器处理完后再传递给 C 处理器，以此类推，形成一个链条。链条上的每个处理器各自承担各自的处理职责，所以叫作职责链模式。</p>
<p>在 GoF 的定义中，一旦某个处理器能处理这个请求，就不会继续将请求传递给后续的处理器了。当然，在实际的开发中，也存在对这个模式的变体，那就是请求不会中途终止传递，而是会被所有的处理器都处理一遍</p>
<p>①职责链模式有两种常用的实现。一种是使用链表来存储处理器，另一种是使用数组来存储处理器，后面一种实现方式更加简单</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('02e61491-bed1-42d9-be68-2fb7b793d904')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_02e61491-bed1-42d9-be68-2fb7b793d904" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_02e61491-bed1-42d9-be68-2fb7b793d904" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_02e61491-bed1-42d9-be68-2fb7b793d904" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Handler {
  </span><span style="color: #0000ff;">protected</span> Handler successor = <span style="color: #0000ff;">null</span><span style="color: #000000;">;

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> setSuccessor(Handler successor) {
    </span><span style="color: #0000ff;">this</span>.successor =<span style="color: #000000;"> successor;
  }

  </span><span style="color: #0000ff;">public</span> final <span style="color: #0000ff;">void</span><span style="color: #000000;"> handle() {
    boolean handled </span>=<span style="color: #000000;"> doHandle();
    </span><span style="color: #0000ff;">if</span> (successor != <span style="color: #0000ff;">null</span> &amp;&amp; !<span style="color: #000000;">handled) {
      successor.handle();
    }
  }

  </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">abstract</span><span style="color: #000000;"> boolean doHandle();
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> HandlerA extends Handler {
  @Override
  </span><span style="color: #0000ff;">protected</span><span style="color: #000000;"> boolean doHandle() {
    boolean handled </span>= <span style="color: #0000ff;">false</span><span style="color: #000000;">;
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
    <span style="color: #0000ff;">return</span><span style="color: #000000;"> handled;
  }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> HandlerB extends Handler {
  @Override
  </span><span style="color: #0000ff;">protected</span><span style="color: #000000;"> boolean doHandle() {
    boolean handled </span>= <span style="color: #0000ff;">false</span><span style="color: #000000;">;
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
    <span style="color: #0000ff;">return</span><span style="color: #000000;"> handled;
  }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> HandlerChain和Application代码不变</span></pre>
</div>
<span class="cnblogs_code_collapse">使用链表来存储处理器</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('46cb40d5-cf8d-4aa2-b2c1-4150b3f0f824')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_46cb40d5-cf8d-4aa2-b2c1-4150b3f0f824" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_46cb40d5-cf8d-4aa2-b2c1-4150b3f0f824" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_46cb40d5-cf8d-4aa2-b2c1-4150b3f0f824" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IHandler {
  boolean handle();
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> HandlerA implements IHandler {
  @Override
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> boolean handle() {
    boolean handled </span>= <span style="color: #0000ff;">false</span><span style="color: #000000;">;
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
    <span style="color: #0000ff;">return</span><span style="color: #000000;"> handled;
  }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> HandlerB implements IHandler {
  @Override
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> boolean handle() {
    boolean handled </span>= <span style="color: #0000ff;">false</span><span style="color: #000000;">;
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
    <span style="color: #0000ff;">return</span><span style="color: #000000;"> handled;
  }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> HandlerChain {
  </span><span style="color: #0000ff;">private</span> List&lt;IHandler&gt; handlers = <span style="color: #0000ff;">new</span> ArrayList&lt;&gt;<span style="color: #000000;">();

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> addHandler(IHandler handler) {
    </span><span style="color: #0000ff;">this</span><span style="color: #000000;">.handlers.add(handler);
  }

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> handle() {
    </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> (IHandler handler : handlers) {
      boolean handled </span>=<span style="color: #000000;"> handler.handle();
      </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (handled) {
        </span><span style="color: #0000ff;">break</span><span style="color: #000000;">;
      }
    }
  }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 使用举例</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Application {
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> main(String[] args) {
    HandlerChain chain </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> HandlerChain();
    chain.addHandler(</span><span style="color: #0000ff;">new</span><span style="color: #000000;"> HandlerA());
    chain.addHandler(</span><span style="color: #0000ff;">new</span><span style="color: #000000;"> HandlerB());
    chain.handle();
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">使用数组来存储处理器</span></div>
<p>②使用职责链模式给敏感词打马赛克</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('37154f9e-ac67-4fe2-b3f5-dc61941868e7')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_37154f9e-ac67-4fe2-b3f5-dc61941868e7" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_37154f9e-ac67-4fe2-b3f5-dc61941868e7" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_37154f9e-ac67-4fe2-b3f5-dc61941868e7" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> SensitiveWordFilter {
  boolean doFilter(Content content);
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SexyWordFilter implements SensitiveWordFilter {
  @Override
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> boolean doFilter(Content content) {
    boolean legal </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">;
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
    <span style="color: #0000ff;">return</span><span style="color: #000000;"> legal;
  }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> PoliticalWordFilter、AdsWordFilter类代码结构与SexyWordFilter类似</span>

<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SensitiveWordFilterChain {
  </span><span style="color: #0000ff;">private</span> List&lt;SensitiveWordFilter&gt; filters = <span style="color: #0000ff;">new</span> ArrayList&lt;&gt;<span style="color: #000000;">();

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> addFilter(SensitiveWordFilter filter) {
    </span><span style="color: #0000ff;">this</span><span style="color: #000000;">.filters.add(filter);
  }

  </span><span style="color: #008000;">//</span><span style="color: #008000;"> return true if content doesn't contain sensitive words.</span>
  <span style="color: #0000ff;">public</span><span style="color: #000000;"> boolean filter(Content content) {
    </span><span style="color: #0000ff;">for</span><span style="color: #000000;"> (SensitiveWordFilter filter : filters) {
      </span><span style="color: #0000ff;">if</span> (!<span style="color: #000000;">filter.doFilter(content)) {
        </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">false</span><span style="color: #000000;">;
      }
    }
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">true</span><span style="color: #000000;">;
  }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ApplicationDemo {
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> main(String[] args) {
    SensitiveWordFilterChain filterChain </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> SensitiveWordFilterChain();
    filterChain.addFilter(</span><span style="color: #0000ff;">new</span> AdsWordFilter());<span style="color: #008000;">//</span><span style="color: #008000;">广告</span>
    filterChain.addFilter(<span style="color: #0000ff;">new</span> SexyWordFilter());<span style="color: #008000;">//</span><span style="color: #008000;">涉黄</span>
    filterChain.addFilter(<span style="color: #0000ff;">new</span> PoliticalWordFilter());<span style="color: #008000;">//</span><span style="color: #008000;">反动</span>
<span style="color: #000000;">
    boolean legal </span>= filterChain.filter(<span style="color: #0000ff;">new</span><span style="color: #000000;"> Content());
    </span><span style="color: #0000ff;">if</span> (!<span style="color: #000000;">legal) {
      </span><span style="color: #008000;">//</span><span style="color: #008000;"> 不发表</span>
    } <span style="color: #0000ff;">else</span><span style="color: #000000;"> {
      </span><span style="color: #008000;">//</span><span style="color: #008000;"> 发表</span>
<span style="color: #000000;">    }
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">示例代码</span></div>
<p>③职责链模式最常用来开发框架的过滤器和拦截器</p>
<p>职责链模式的实现包含处理器接口（IHandler）或抽象类（Handler），以及处理器链（HandlerChain）。对应到 Servlet Filter，javax.servlet.Filter 就是处理器接口，FilterChain 就是处理器链</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('9b0d83af-4448-42f1-839d-78b1a3f66cb1')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_9b0d83af-4448-42f1-839d-78b1a3f66cb1" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_9b0d83af-4448-42f1-839d-78b1a3f66cb1" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_9b0d83af-4448-42f1-839d-78b1a3f66cb1" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> LogFilter implements Filter {
  @Override
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> init(FilterConfig filterConfig) throws ServletException {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 在创建Filter时自动调用，
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 其中filterConfig包含这个Filter的配置参数，比如name之类的（从配置文件中读取的）</span>
<span style="color: #000000;">  }

  @Override
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
    System.</span><span style="color: #0000ff;">out</span>.println(<span style="color: #800000;">"</span><span style="color: #800000;">拦截客户端发送来的请求.</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    chain.doFilter(request, response);
    System.</span><span style="color: #0000ff;">out</span>.println(<span style="color: #800000;">"</span><span style="color: #800000;">拦截发送给客户端的响应.</span><span style="color: #800000;">"</span><span style="color: #000000;">);
  }

  @Override
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> destroy() {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> 在销毁Filter时自动调用</span>
<span style="color: #000000;">  }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 在web.xml配置文件中如下配置：</span>
&lt;filter&gt;
  &lt;filter-name&gt;logFilter&lt;/filter-name&gt;
  &lt;filter-<span style="color: #0000ff;">class</span>&gt;com.xzg.cd.LogFilter&lt;/filter-<span style="color: #0000ff;">class</span>&gt;
&lt;/filter&gt;
&lt;filter-mapping&gt;
    &lt;filter-name&gt;logFilter&lt;/filter-name&gt;
    &lt;url-pattern&gt;<span style="color: #008000;">/*</span><span style="color: #008000;">&lt;/url-pattern&gt;
&lt;/filter-mapping&gt;






public final class ApplicationFilterChain implements FilterChain {
  private int pos = 0; //当前执行到了哪个filter
  private int n; //filter的个数
  private ApplicationFilterConfig[] filters;
  private Servlet servlet;
  
  @Override
  public void doFilter(ServletRequest request, ServletResponse response) {
    if (pos &lt; n) {
      ApplicationFilterConfig filterConfig = filters[pos++];
      Filter filter = filterConfig.getFilter();
      filter.doFilter(request, response, this);
    } else {
      // filter都处理完毕后，执行servlet
      servlet.service(request, response);
    }
  }
  
  public void addFilter(ApplicationFilterConfig filterConfig) {
    for (ApplicationFilterConfig filter:filters)
      if (filter==filterConfig)
         return;

    if (n == filters.length) {//扩容
      ApplicationFilterConfig[] newFilters = new ApplicationFilterConfig[n + INCREMENT];
      System.arraycopy(filters, 0, newFilters, 0, n);
      filters = newFilters;
    }
    filters[n++] = filterConfig;
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Servlet Filter</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('32ee9ad4-699e-4c2a-aa8d-1990d957343c')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_32ee9ad4-699e-4c2a-aa8d-1990d957343c" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_32ee9ad4-699e-4c2a-aa8d-1990d957343c" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_32ee9ad4-699e-4c2a-aa8d-1990d957343c" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> LogInterceptor implements HandlerInterceptor {

  @Override
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
    System.</span><span style="color: #0000ff;">out</span>.println(<span style="color: #800000;">"</span><span style="color: #800000;">拦截客户端发送来的请求.</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">true</span>; <span style="color: #008000;">//</span><span style="color: #008000;"> 继续后续的处理</span>
<span style="color: #000000;">  }

  @Override
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
    System.</span><span style="color: #0000ff;">out</span>.println(<span style="color: #800000;">"</span><span style="color: #800000;">拦截发送给客户端的响应.</span><span style="color: #800000;">"</span><span style="color: #000000;">);
  }

  @Override
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
    System.</span><span style="color: #0000ff;">out</span>.println(<span style="color: #800000;">"</span><span style="color: #800000;">这里总是被执行.</span><span style="color: #800000;">"</span><span style="color: #000000;">);
  }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">在Spring MVC配置文件中配置interceptors</span>
&lt;mvc:interceptors&gt;
   &lt;mvc:interceptor&gt;
       &lt;mvc:mapping path=<span style="color: #800000;">"</span><span style="color: #800000;">/*</span><span style="color: #800000;">"</span>/&gt;
       &lt;bean <span style="color: #0000ff;">class</span>=<span style="color: #800000;">"</span><span style="color: #800000;">com.xzg.cd.LogInterceptor</span><span style="color: #800000;">"</span> /&gt;
   &lt;/mvc:interceptor&gt;
&lt;/mvc:interceptors&gt;





<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> HandlerExecutionChain {
 </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> final Object handler;
 </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> HandlerInterceptor[] interceptors;
 
 </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> addInterceptor(HandlerInterceptor interceptor) {
  initInterceptorList().add(interceptor);
 }

 boolean applyPreHandle(HttpServletRequest request, HttpServletResponse response) throws Exception {
  HandlerInterceptor[] interceptors </span>=<span style="color: #000000;"> getInterceptors();
  </span><span style="color: #0000ff;">if</span> (!<span style="color: #000000;">ObjectUtils.isEmpty(interceptors)) {
   </span><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> i = <span style="color: #800080;">0</span>; i &lt; interceptors.length; i++<span style="color: #000000;">) {
    HandlerInterceptor interceptor </span>=<span style="color: #000000;"> interceptors[i];
    </span><span style="color: #0000ff;">if</span> (!interceptor.preHandle(request, response, <span style="color: #0000ff;">this</span><span style="color: #000000;">.handler)) {
     triggerAfterCompletion(request, response, </span><span style="color: #0000ff;">null</span><span style="color: #000000;">);
     </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">false</span><span style="color: #000000;">;
    }
   }
  }
  </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">true</span><span style="color: #000000;">;
 }

 </span><span style="color: #0000ff;">void</span><span style="color: #000000;"> applyPostHandle(HttpServletRequest request, HttpServletResponse response, ModelAndView mv) throws Exception {
  HandlerInterceptor[] interceptors </span>=<span style="color: #000000;"> getInterceptors();
  </span><span style="color: #0000ff;">if</span> (!<span style="color: #000000;">ObjectUtils.isEmpty(interceptors)) {
   </span><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> i = interceptors.length - <span style="color: #800080;">1</span>; i &gt;= <span style="color: #800080;">0</span>; i--<span style="color: #000000;">) {
    HandlerInterceptor interceptor </span>=<span style="color: #000000;"> interceptors[i];
    interceptor.postHandle(request, response, </span><span style="color: #0000ff;">this</span><span style="color: #000000;">.handler, mv);
   }
  }
 }

 </span><span style="color: #0000ff;">void</span><span style="color: #000000;"> triggerAfterCompletion(HttpServletRequest request, HttpServletResponse response, Exception ex)
   throws Exception {
  HandlerInterceptor[] interceptors </span>=<span style="color: #000000;"> getInterceptors();
  </span><span style="color: #0000ff;">if</span> (!<span style="color: #000000;">ObjectUtils.isEmpty(interceptors)) {
   </span><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> i = <span style="color: #0000ff;">this</span>.interceptorIndex; i &gt;= <span style="color: #800080;">0</span>; i--<span style="color: #000000;">) {
    HandlerInterceptor interceptor </span>=<span style="color: #000000;"> interceptors[i];
    </span><span style="color: #0000ff;">try</span><span style="color: #000000;"> {
     interceptor.afterCompletion(request, response, </span><span style="color: #0000ff;">this</span><span style="color: #000000;">.handler, ex);
    } </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (Throwable ex2) {
     logger.error(</span><span style="color: #800000;">"</span><span style="color: #800000;">HandlerInterceptor.afterCompletion threw exception</span><span style="color: #800000;">"</span><span style="color: #000000;">, ex2);
    }
   }
  }
 }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Spring Interceptor</span></div>
<p>&nbsp;</p>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">5，状态模式</span></strong></span></p>
<p>状态机又叫有限状态机，它有 3 个部分组成：状态、事件、动作。其中，事件也称为转移条件。事件触发状态的转移及动作的执行。不过，动作不是必须的，也可能只转移状态，不执行任何动作</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202008/741594-20200819233656713-174215014.png" alt="" width="313" height="249" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>状态：小马里奥（Small Mario）、超级马里奥（Super Mario）、火焰马里奥（Fire Mario）、斗篷马里奥（Cape Mario）</p>
<p>事件：吃了蘑菇、获得斗篷、获得火焰、遇到怪物</p>
<p>动作：增加/扣减积分</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('5b407921-ffa2-401a-b0c1-5a4c0798d575')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_5b407921-ffa2-401a-b0c1-5a4c0798d575" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_5b407921-ffa2-401a-b0c1-5a4c0798d575" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_5b407921-ffa2-401a-b0c1-5a4c0798d575" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">enum</span><span style="color: #000000;"> State {
  SMALL(</span><span style="color: #800080;">0</span><span style="color: #000000;">),
  SUPER(</span><span style="color: #800080;">1</span><span style="color: #000000;">),
  FIRE(</span><span style="color: #800080;">2</span><span style="color: #000000;">),
  CAPE(</span><span style="color: #800080;">3</span><span style="color: #000000;">);

  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">int</span><span style="color: #000000;"> value;

  </span><span style="color: #0000ff;">private</span> State(<span style="color: #0000ff;">int</span><span style="color: #000000;"> value) {
    </span><span style="color: #0000ff;">this</span>.value =<span style="color: #000000;"> value;
  }

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span><span style="color: #000000;"> getValue() {
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">this</span><span style="color: #000000;">.value;
  }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MarioStateMachine {
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">int</span><span style="color: #000000;"> score;
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> State currentState;

  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> MarioStateMachine() {
    </span><span style="color: #0000ff;">this</span>.score = <span style="color: #800080;">0</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">this</span>.currentState =<span style="color: #000000;"> State.SMALL;
  }

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> obtainMushRoom() {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">TODO</span>
<span style="color: #000000;">  }

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> obtainCape() {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">TODO</span>
<span style="color: #000000;">  }

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> obtainFireFlower() {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">TODO</span>
<span style="color: #000000;">  }

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> meetMonster() {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">TODO</span>
<span style="color: #000000;">  }

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span><span style="color: #000000;"> getScore() {
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">this</span><span style="color: #000000;">.score;
  }

  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> State getCurrentState() {
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">this</span><span style="color: #000000;">.currentState;
  }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ApplicationDemo {
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> main(String[] args) {
    MarioStateMachine mario </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> MarioStateMachine();
    mario.obtainMushRoom();
    </span><span style="color: #0000ff;">int</span> score =<span style="color: #000000;"> mario.getScore();
    State state </span>=<span style="color: #000000;"> mario.getCurrentState();
    System.</span><span style="color: #0000ff;">out</span>.println(<span style="color: #800000;">"</span><span style="color: #800000;">mario score: </span><span style="color: #800000;">"</span> + score + <span style="color: #800000;">"</span><span style="color: #800000;">; state: </span><span style="color: #800000;">"</span> +<span style="color: #000000;"> state);
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">骨架代码</span></div>
<p>①三种实现方式-分支逻辑法</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('3af1b783-248e-478d-98c2-a87bbc15d0ca')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_3af1b783-248e-478d-98c2-a87bbc15d0ca" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_3af1b783-248e-478d-98c2-a87bbc15d0ca" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_3af1b783-248e-478d-98c2-a87bbc15d0ca" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MarioStateMachine {
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">int</span><span style="color: #000000;"> score;
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> State currentState;

  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> MarioStateMachine() {
    </span><span style="color: #0000ff;">this</span>.score = <span style="color: #800080;">0</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">this</span>.currentState =<span style="color: #000000;"> State.SMALL;
  }
</span><span style="color: #008000;">//</span><span style="color: #008000;">获取蘑菇</span>
  <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> obtainMushRoom() {
    </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (currentState.equals(State.SMALL)) {
      </span><span style="color: #0000ff;">this</span>.currentState =<span style="color: #000000;"> State.SUPER;
      </span><span style="color: #0000ff;">this</span>.score += <span style="color: #800080;">100</span><span style="color: #000000;">;
    }
  }
</span><span style="color: #008000;">//</span><span style="color: #008000;">获得斗篷</span>
  <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> obtainCape() {
    </span><span style="color: #0000ff;">if</span> (currentState.equals(State.SMALL) ||<span style="color: #000000;"> currentState.equals(State.SUPER) ) {
      </span><span style="color: #0000ff;">this</span>.currentState =<span style="color: #000000;"> State.CAPE;
      </span><span style="color: #0000ff;">this</span>.score += <span style="color: #800080;">200</span><span style="color: #000000;">;
    }
  }
</span><span style="color: #008000;">//</span><span style="color: #008000;">获取火焰</span>
  <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> obtainFireFlower() {
    </span><span style="color: #0000ff;">if</span> (currentState.equals(State.SMALL) ||<span style="color: #000000;"> currentState.equals(State.SUPER) ) {
      </span><span style="color: #0000ff;">this</span>.currentState =<span style="color: #000000;"> State.FIRE;
      </span><span style="color: #0000ff;">this</span>.score += <span style="color: #800080;">300</span><span style="color: #000000;">;
    }
  }
</span><span style="color: #008000;">//</span><span style="color: #008000;">遇到怪物</span>
  <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> meetMonster() {
    </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (currentState.equals(State.SUPER)) {
      </span><span style="color: #0000ff;">this</span>.currentState =<span style="color: #000000;"> State.SMALL;
      </span><span style="color: #0000ff;">this</span>.score -= <span style="color: #800080;">100</span><span style="color: #000000;">;
      </span><span style="color: #0000ff;">return</span><span style="color: #000000;">;
    }

    </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (currentState.equals(State.CAPE)) {
      </span><span style="color: #0000ff;">this</span>.currentState =<span style="color: #000000;"> State.SMALL;
      </span><span style="color: #0000ff;">this</span>.score -= <span style="color: #800080;">200</span><span style="color: #000000;">;
      </span><span style="color: #0000ff;">return</span><span style="color: #000000;">;
    }

    </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (currentState.equals(State.FIRE)) {
      </span><span style="color: #0000ff;">this</span>.currentState =<span style="color: #000000;"> State.SMALL;
      </span><span style="color: #0000ff;">this</span>.score -= <span style="color: #800080;">300</span><span style="color: #000000;">;
      </span><span style="color: #0000ff;">return</span><span style="color: #000000;">;
    }
  }

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span><span style="color: #000000;"> getScore() {
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">this</span><span style="color: #000000;">.score;
  }

  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> State getCurrentState() {
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">this</span><span style="color: #000000;">.currentState;
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">示例代码</span></div>
<p>②三种实现方式-查表法</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202008/741594-20200819234247347-9590481.png" alt="" width="377" height="129" loading="lazy" /></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('f03b37df-0656-4f25-9fe7-83924d2616cd')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_f03b37df-0656-4f25-9fe7-83924d2616cd" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_f03b37df-0656-4f25-9fe7-83924d2616cd" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_f03b37df-0656-4f25-9fe7-83924d2616cd" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">enum</span><span style="color: #000000;"> Event {
  GOT_MUSHROOM(</span><span style="color: #800080;">0</span><span style="color: #000000;">),
  GOT_CAPE(</span><span style="color: #800080;">1</span><span style="color: #000000;">),
  GOT_FIRE(</span><span style="color: #800080;">2</span><span style="color: #000000;">),
  MET_MONSTER(</span><span style="color: #800080;">3</span><span style="color: #000000;">);

  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">int</span><span style="color: #000000;"> value;

  </span><span style="color: #0000ff;">private</span> Event(<span style="color: #0000ff;">int</span><span style="color: #000000;"> value) {
    </span><span style="color: #0000ff;">this</span>.value =<span style="color: #000000;"> value;
  }

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span><span style="color: #000000;"> getValue() {
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">this</span><span style="color: #000000;">.value;
  }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MarioStateMachine {
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">int</span><span style="color: #000000;"> score;
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> State currentState;

  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> final State[][] transitionTable =<span style="color: #000000;"> {
          {SUPER, CAPE, FIRE, SMALL},
          {SUPER, CAPE, FIRE, SMALL},
          {CAPE, CAPE, CAPE, SMALL},
          {FIRE, FIRE, FIRE, SMALL}
  };

  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> final <span style="color: #0000ff;">int</span>[][] actionTable =<span style="color: #000000;"> {
          {</span>+<span style="color: #800080;">100</span>, +<span style="color: #800080;">200</span>, +<span style="color: #800080;">300</span>, +<span style="color: #800080;">0</span><span style="color: #000000;">},
          {</span>+<span style="color: #800080;">0</span>, +<span style="color: #800080;">200</span>, +<span style="color: #800080;">300</span>, -<span style="color: #800080;">100</span><span style="color: #000000;">},
          {</span>+<span style="color: #800080;">0</span>, +<span style="color: #800080;">0</span>, +<span style="color: #800080;">0</span>, -<span style="color: #800080;">200</span><span style="color: #000000;">},
          {</span>+<span style="color: #800080;">0</span>, +<span style="color: #800080;">0</span>, +<span style="color: #800080;">0</span>, -<span style="color: #800080;">300</span><span style="color: #000000;">}
  };

  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> MarioStateMachine() {
    </span><span style="color: #0000ff;">this</span>.score = <span style="color: #800080;">0</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">this</span>.currentState =<span style="color: #000000;"> State.SMALL;
  }

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> obtainMushRoom() {
    executeEvent(Event.GOT_MUSHROOM);
  }

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> obtainCape() {
    executeEvent(Event.GOT_CAPE);
  }

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> obtainFireFlower() {
    executeEvent(Event.GOT_FIRE);
  }

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> meetMonster() {
    executeEvent(Event.MET_MONSTER);
  }

  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">void</span> executeEvent(Event <span style="color: #0000ff;">event</span><span style="color: #000000;">) {
    </span><span style="color: #0000ff;">int</span> stateValue =<span style="color: #000000;"> currentState.getValue();
    </span><span style="color: #0000ff;">int</span> eventValue = <span style="color: #0000ff;">event</span><span style="color: #000000;">.getValue();
    </span><span style="color: #0000ff;">this</span>.currentState =<span style="color: #000000;"> transitionTable[stateValue][eventValue];
    </span><span style="color: #0000ff;">this</span>.score =<span style="color: #000000;"> actionTable[stateValue][eventValue];
  }

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span><span style="color: #000000;"> getScore() {
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">this</span><span style="color: #000000;">.score;
  }

  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> State getCurrentState() {
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">this</span><span style="color: #000000;">.currentState;
  }

}</span></pre>
</div>
<span class="cnblogs_code_collapse">示例代码</span></div>
<p>②三种实现方式-状态模式</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('2e0b130e-39c3-44eb-9313-3bd0011907d3')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_2e0b130e-39c3-44eb-9313-3bd0011907d3" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_2e0b130e-39c3-44eb-9313-3bd0011907d3" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_2e0b130e-39c3-44eb-9313-3bd0011907d3" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span> IMario { <span style="color: #008000;">//</span><span style="color: #008000;">所有状态类的接口</span>
<span style="color: #000000;">  State getName();
  </span><span style="color: #008000;">//</span><span style="color: #008000;">以下是定义的事件</span>
  <span style="color: #0000ff;">void</span><span style="color: #000000;"> obtainMushRoom();
  </span><span style="color: #0000ff;">void</span><span style="color: #000000;"> obtainCape();
  </span><span style="color: #0000ff;">void</span><span style="color: #000000;"> obtainFireFlower();
  </span><span style="color: #0000ff;">void</span><span style="color: #000000;"> meetMonster();
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SmallMario implements IMario {
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> MarioStateMachine stateMachine;

  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> SmallMario(MarioStateMachine stateMachine) {
    </span><span style="color: #0000ff;">this</span>.stateMachine =<span style="color: #000000;"> stateMachine;
  }

  @Override
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> State getName() {
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> State.SMALL;
  }

  @Override
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> obtainMushRoom() {
    stateMachine.setCurrentState(</span><span style="color: #0000ff;">new</span><span style="color: #000000;"> SuperMario(stateMachine));
    stateMachine.setScore(stateMachine.getScore() </span>+ <span style="color: #800080;">100</span><span style="color: #000000;">);
  }

  @Override
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> obtainCape() {
    stateMachine.setCurrentState(</span><span style="color: #0000ff;">new</span><span style="color: #000000;"> CapeMario(stateMachine));
    stateMachine.setScore(stateMachine.getScore() </span>+ <span style="color: #800080;">200</span><span style="color: #000000;">);
  }

  @Override
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> obtainFireFlower() {
    stateMachine.setCurrentState(</span><span style="color: #0000ff;">new</span><span style="color: #000000;"> FireMario(stateMachine));
    stateMachine.setScore(stateMachine.getScore() </span>+ <span style="color: #800080;">300</span><span style="color: #000000;">);
  }

  @Override
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> meetMonster() {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> do nothing...</span>
<span style="color: #000000;">  }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SuperMario implements IMario {
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> MarioStateMachine stateMachine;

  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> SuperMario(MarioStateMachine stateMachine) {
    </span><span style="color: #0000ff;">this</span>.stateMachine =<span style="color: #000000;"> stateMachine;
  }

  @Override
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> State getName() {
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> State.SUPER;
  }

  @Override
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> obtainMushRoom() {
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> do nothing...</span>
<span style="color: #000000;">  }

  @Override
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> obtainCape() {
    stateMachine.setCurrentState(</span><span style="color: #0000ff;">new</span><span style="color: #000000;"> CapeMario(stateMachine));
    stateMachine.setScore(stateMachine.getScore() </span>+ <span style="color: #800080;">200</span><span style="color: #000000;">);
  }

  @Override
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> obtainFireFlower() {
    stateMachine.setCurrentState(</span><span style="color: #0000ff;">new</span><span style="color: #000000;"> FireMario(stateMachine));
    stateMachine.setScore(stateMachine.getScore() </span>+ <span style="color: #800080;">300</span><span style="color: #000000;">);
  }

  @Override
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> meetMonster() {
    stateMachine.setCurrentState(</span><span style="color: #0000ff;">new</span><span style="color: #000000;"> SmallMario(stateMachine));
    stateMachine.setScore(stateMachine.getScore() </span>- <span style="color: #800080;">100</span><span style="color: #000000;">);
  }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 省略CapeMario、FireMario类...</span>

<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MarioStateMachine {
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">int</span><span style="color: #000000;"> score;
  </span><span style="color: #0000ff;">private</span> IMario currentState; <span style="color: #008000;">//</span><span style="color: #008000;"> 不再使用枚举来表示状态</span>

  <span style="color: #0000ff;">public</span><span style="color: #000000;"> MarioStateMachine() {
    </span><span style="color: #0000ff;">this</span>.score = <span style="color: #800080;">0</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">this</span>.currentState = <span style="color: #0000ff;">new</span> SmallMario(<span style="color: #0000ff;">this</span><span style="color: #000000;">);
  }

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> obtainMushRoom() {
    </span><span style="color: #0000ff;">this</span><span style="color: #000000;">.currentState.obtainMushRoom();
  }

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> obtainCape() {
    </span><span style="color: #0000ff;">this</span><span style="color: #000000;">.currentState.obtainCape();
  }

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> obtainFireFlower() {
    </span><span style="color: #0000ff;">this</span><span style="color: #000000;">.currentState.obtainFireFlower();
  }

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> meetMonster() {
    </span><span style="color: #0000ff;">this</span><span style="color: #000000;">.currentState.meetMonster();
  }

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span><span style="color: #000000;"> getScore() {
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">this</span><span style="color: #000000;">.score;
  }

  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> State getCurrentState() {
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">this</span><span style="color: #000000;">.currentState.getName();
  }

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> setScore(<span style="color: #0000ff;">int</span><span style="color: #000000;"> score) {
    </span><span style="color: #0000ff;">this</span>.score =<span style="color: #000000;"> score;
  }

  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> setCurrentState(IMario currentState) {
    </span><span style="color: #0000ff;">this</span>.currentState =<span style="color: #000000;"> currentState;
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">示例代码</span></div>
<p>&nbsp;</p>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">6，迭代器模式</span></strong></span></p>
<p>迭代器模式，也叫游标模式。它用来遍历集合对象。这里说的&ldquo;集合对象&rdquo;，我们也可以叫&ldquo;容器&rdquo;&ldquo;聚合对象&rdquo;，实际上就是包含一组对象的对象，比如，数组、链表、树、图、跳表。</p>
<p>1，完整的迭代器模式包含容器和容器迭代器两部分</p>
<p>容器中需要定义 iterator() 方法，用来创建迭代器</p>
<p>迭代器接口中需要定义 hasNext()、currentItem()、next() 三个最基本的方法。容器对象通过依赖注入传递到迭代器类中。</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202009/741594-20200923212128075-1730307652.png" alt="" width="326" height="151" loading="lazy" /></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('50794c2b-b056-4d6a-850e-e846d4c5f254')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_50794c2b-b056-4d6a-850e-e846d4c5f254" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_50794c2b-b056-4d6a-850e-e846d4c5f254" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_50794c2b-b056-4d6a-850e-e846d4c5f254" class="cnblogs_code_hide">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">两种定义方法
</span><span style="color: #008000;">//</span><span style="color: #008000;"> 接口定义方式一</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span> Iterator&lt;E&gt;<span style="color: #000000;"> {
  boolean hasNext();
  </span><span style="color: #0000ff;">void</span><span style="color: #000000;"> next();
  E currentItem();
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 接口定义方式二</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span> Iterator&lt;E&gt;<span style="color: #000000;"> {
  boolean hasNext();
  E next();
}



</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> ArrayIterator&lt;E&gt; implements Iterator&lt;E&gt;<span style="color: #000000;"> {
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">int</span><span style="color: #000000;"> cursor;
  </span><span style="color: #0000ff;">private</span> ArrayList&lt;E&gt;<span style="color: #000000;"> arrayList;

  </span><span style="color: #0000ff;">public</span> ArrayIterator(ArrayList&lt;E&gt;<span style="color: #000000;"> arrayList) {
    </span><span style="color: #0000ff;">this</span>.cursor = <span style="color: #800080;">0</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">this</span>.arrayList =<span style="color: #000000;"> arrayList;
  }

  @Override
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> boolean hasNext() {
    </span><span style="color: #0000ff;">return</span> cursor != arrayList.size(); <span style="color: #008000;">//</span><span style="color: #008000;">注意这里，cursor在指向最后一个元素的时候，hasNext()仍旧返回true。</span>
<span style="color: #000000;">  }

  @Override
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> next() {
    cursor</span>++<span style="color: #000000;">;
  }

  @Override
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> E currentItem() {
    </span><span style="color: #0000ff;">if</span> (cursor &gt;=<span style="color: #000000;"> arrayList.size()) {
      </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> NoSuchElementException();
    }
    </span><span style="color: #0000ff;">return</span> arrayList.<span style="color: #0000ff;">get</span><span style="color: #000000;">(cursor);
  }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Demo {
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> main(String[] args) {
    ArrayList</span>&lt;String&gt; names = <span style="color: #0000ff;">new</span> ArrayList&lt;&gt;<span style="color: #000000;">();
    names.add(</span><span style="color: #800000;">"</span><span style="color: #800000;">xzg</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    names.add(</span><span style="color: #800000;">"</span><span style="color: #800000;">wang</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    names.add(</span><span style="color: #800000;">"</span><span style="color: #800000;">zheng</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    
    Iterator</span>&lt;String&gt; iterator = <span style="color: #0000ff;">new</span><span style="color: #000000;"> ArrayIterator(names);
    </span><span style="color: #0000ff;">while</span><span style="color: #000000;"> (iterator.hasNext()) {
      System.</span><span style="color: #0000ff;">out</span><span style="color: #000000;">.println(iterator.currentItem());
      iterator.next();
    }
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">迭代器</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('384acc90-a0fd-4f08-a5b4-510465a8fa6a')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_384acc90-a0fd-4f08-a5b4-510465a8fa6a" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_384acc90-a0fd-4f08-a5b4-510465a8fa6a" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_384acc90-a0fd-4f08-a5b4-510465a8fa6a" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span> List&lt;E&gt;<span style="color: #000000;"> {
  Iterator iterator();
  </span><span style="color: #008000;">//</span><span style="color: #008000;">...省略其他接口函数...</span>
<span style="color: #000000;">}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> ArrayList&lt;E&gt; implements List&lt;E&gt;<span style="color: #000000;"> {
  </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
  <span style="color: #0000ff;">public</span><span style="color: #000000;"> Iterator iterator() {
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> ArrayIterator(<span style="color: #0000ff;">this</span><span style="color: #000000;">);
  }
  </span><span style="color: #008000;">//</span><span style="color: #008000;">...省略其他代码</span>
<span style="color: #000000;">}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Demo {
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> main(String[] args) {
    List</span>&lt;String&gt; names = <span style="color: #0000ff;">new</span> ArrayList&lt;&gt;<span style="color: #000000;">();
    names.add(</span><span style="color: #800000;">"</span><span style="color: #800000;">xzg</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    names.add(</span><span style="color: #800000;">"</span><span style="color: #800000;">wang</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    names.add(</span><span style="color: #800000;">"</span><span style="color: #800000;">zheng</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    
    Iterator</span>&lt;String&gt; iterator =<span style="color: #000000;"> names.iterator();
    </span><span style="color: #0000ff;">while</span><span style="color: #000000;"> (iterator.hasNext()) {
      System.</span><span style="color: #0000ff;">out</span><span style="color: #000000;">.println(iterator.currentItem());
      iterator.next();
    }
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">在容器中定义一个 iterator() 方法</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('f71c619f-0c0f-45c9-a5c2-89d012e1d66e')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_f71c619f-0c0f-45c9-a5c2-89d012e1d66e" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_f71c619f-0c0f-45c9-a5c2-89d012e1d66e" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_f71c619f-0c0f-45c9-a5c2-89d012e1d66e" class="cnblogs_code_hide">
<pre>List&lt;String&gt; names = <span style="color: #0000ff;">new</span> ArrayList&lt;&gt;<span style="color: #000000;">();
names.add(</span><span style="color: #800000;">"</span><span style="color: #800000;">xzg</span><span style="color: #800000;">"</span><span style="color: #000000;">);
names.add(</span><span style="color: #800000;">"</span><span style="color: #800000;">wang</span><span style="color: #800000;">"</span><span style="color: #000000;">);
names.add(</span><span style="color: #800000;">"</span><span style="color: #800000;">zheng</span><span style="color: #800000;">"</span><span style="color: #000000;">);

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 第一种遍历方式：for循环</span>
<span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> i = <span style="color: #800080;">0</span>; i &lt; names.size(); i++<span style="color: #000000;">) {
  System.</span><span style="color: #0000ff;">out</span>.print(names.<span style="color: #0000ff;">get</span>(i) + <span style="color: #800000;">"</span><span style="color: #800000;">,</span><span style="color: #800000;">"</span><span style="color: #000000;">);
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 第二种遍历方式：foreach循环</span>
<span style="color: #0000ff;">for</span><span style="color: #000000;"> (String name : names) {
  System.</span><span style="color: #0000ff;">out</span>.print(name + <span style="color: #800000;">"</span><span style="color: #800000;">,</span><span style="color: #800000;">"</span><span style="color: #000000;">)
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 第三种遍历方式：迭代器遍历</span>
Iterator&lt;String&gt; iterator =<span style="color: #000000;"> names.iterator();
</span><span style="color: #0000ff;">while</span><span style="color: #000000;"> (iterator.hasNext()) {
  System.</span><span style="color: #0000ff;">out</span>.print(iterator.next() + <span style="color: #800000;">"</span><span style="color: #800000;">,</span><span style="color: #800000;">"</span>);<span style="color: #008000;">//</span><span style="color: #008000;">Java中的迭代器接口是第二种定义方式，next()既移动游标又返回数据</span>
}</pre>
</div>
<span class="cnblogs_code_collapse">一般来讲，遍历集合数据有三种方法：for 循环、foreach 循环、iterator 迭代器。对于这三种方式</span></div>
<p>遍历集合一般有三种方式：for 循环、foreach 循环、迭代器遍历。后两种本质上属于一种，都可以看作迭代器遍历。相对于 for 循环遍历，利用迭代器来遍历有下面三个优势：</p>
<ul>
<li><span style="font-size: 12px;">迭代器模式封装集合内部的复杂数据结构，开发者不需要了解如何遍历，直接使用容器提供的迭代器即可；</span></li>
<li><span style="font-size: 12px;">迭代器模式将集合对象的遍历操作从集合类中拆分出来，放到迭代器类中，让两者的职责更加单一；</span></li>
<li><span style="font-size: 12px;">迭代器模式让添加新的遍历算法更加容易，更符合开闭原则。除此之外，因为迭代器都实现自相同的接口，在开发中，基于接口而非实现编程，替换迭代器也变得更加容易。</span></li>
</ul>
<p>2，在遍历的同时增删集合会发生什么</p>
<p>会发生不可预期的行为。放着这种情况，可以在遍历集合的同时发现增删集合抛出异常</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('b5502cc2-cb0b-42c7-afd3-84378b8d8d8e')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_b5502cc2-cb0b-42c7-afd3-84378b8d8d8e" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_b5502cc2-cb0b-42c7-afd3-84378b8d8d8e" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_b5502cc2-cb0b-42c7-afd3-84378b8d8d8e" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ArrayIterator implements Iterator {
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">int</span><span style="color: #000000;"> cursor;
  </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> ArrayList arrayList;
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">int</span><span style="color: #000000;"> expectedModCount;

  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> ArrayIterator(ArrayList arrayList) {
    </span><span style="color: #0000ff;">this</span>.cursor = <span style="color: #800080;">0</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">this</span>.arrayList =<span style="color: #000000;"> arrayList;
    </span><span style="color: #0000ff;">this</span>.expectedModCount =<span style="color: #000000;"> arrayList.modCount;
  }

  @Override
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> boolean hasNext() {
    checkForComodification();
    </span><span style="color: #0000ff;">return</span> cursor &lt;<span style="color: #000000;"> arrayList.size();
  }

  @Override
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> next() {
    checkForComodification();
    cursor</span>++<span style="color: #000000;">;
  }

  @Override
  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Object currentItem() {
    checkForComodification();
    </span><span style="color: #0000ff;">return</span> arrayList.<span style="color: #0000ff;">get</span><span style="color: #000000;">(cursor);
  }
  
  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> checkForComodification() {
    </span><span style="color: #0000ff;">if</span> (arrayList.modCount !=<span style="color: #000000;"> expectedModCount)
        </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> ConcurrentModificationException();
  }
}

</span><span style="color: #008000;">//</span><span style="color: #008000;">代码示例</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Demo {
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> main(String[] args) {
    List</span>&lt;String&gt; names = <span style="color: #0000ff;">new</span> ArrayList&lt;&gt;<span style="color: #000000;">();
    names.add(</span><span style="color: #800000;">"</span><span style="color: #800000;">a</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    names.add(</span><span style="color: #800000;">"</span><span style="color: #800000;">b</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    names.add(</span><span style="color: #800000;">"</span><span style="color: #800000;">c</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    names.add(</span><span style="color: #800000;">"</span><span style="color: #800000;">d</span><span style="color: #800000;">"</span><span style="color: #000000;">);

    Iterator</span>&lt;String&gt; iterator =<span style="color: #000000;"> names.iterator();
    iterator.next();
    names.remove(</span><span style="color: #800000;">"</span><span style="color: #800000;">a</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    iterator.next();</span><span style="color: #008000;">//</span><span style="color: #008000;">抛出ConcurrentModificationException异常</span>
<span style="color: #000000;">  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">怎么确定在遍历时候，集合有没有增删元素呢？我们在 ArrayList 中定义一个成员变量 modCount，记录集合被修改的次数，集合每调用一次增加或删除元素的函数，就会给 modCount 加 1。当通过调用集合上的 iterator() 函数来创建迭代器的时候，我们把 modCount 值传递给迭代器的 expectedModCount 成员变量，之后每次调用迭代器上的 hasNext()、next()、currentItem() 函数，我们都会检查集合上的 modCount 是否等于 expectedModCount，也就是看，在创建完迭代器之后，modCount 是否改变过。如果两个值不相同，那就说明集合存储的元素已经改变了，要么增加了元素，要么删除了元素，之前创建的迭代器已经不能正确运行了，再继续使用就会产生不可预期的结果，所以我们选择 fail-fast 解决方式，抛出运行时异常，结束掉程序，让程序员尽快修复这个因为不正确使用迭代器而产生的 bug。</span></div>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">八、开源实战</span></strong></span></p>
<p><span style="color: #ff6600;"><strong><span style="font-size: 16px;">1，&nbsp;通过剖析Java JDK源码学习灵活应用设计模式</span></strong></span></p>
<p>①工厂模式在 Calendar 类中的应用</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('0b484cc6-a28a-4ca5-b137-2a77015b5452')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_0b484cc6-a28a-4ca5-b137-2a77015b5452" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_0b484cc6-a28a-4ca5-b137-2a77015b5452" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_0b484cc6-a28a-4ca5-b137-2a77015b5452" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">class</span> Calendar implements Serializable, Cloneable, Comparable&lt;Calendar&gt;<span style="color: #000000;"> {
  </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
  <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> Calendar getInstance(TimeZone zone, Locale aLocale){
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> createCalendar(zone, aLocale);
  }

  </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> Calendar createCalendar(TimeZone zone,Locale aLocale) {
    CalendarProvider provider </span>=<span style="color: #000000;"> LocaleProviderAdapter.getAdapter(
        CalendarProvider.</span><span style="color: #0000ff;">class</span><span style="color: #000000;">, aLocale).getCalendarProvider();
    </span><span style="color: #0000ff;">if</span> (provider != <span style="color: #0000ff;">null</span><span style="color: #000000;">) {
      </span><span style="color: #0000ff;">try</span><span style="color: #000000;"> {
        </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> provider.getInstance(zone, aLocale);
      } </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (IllegalArgumentException iae) {
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> fall back to the default instantiation</span>
<span style="color: #000000;">      }
    }

    Calendar cal </span>= <span style="color: #0000ff;">null</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (aLocale.hasExtensions()) {
      String caltype </span>= aLocale.getUnicodeLocaleType(<span style="color: #800000;">"</span><span style="color: #800000;">ca</span><span style="color: #800000;">"</span><span style="color: #000000;">);
      </span><span style="color: #0000ff;">if</span> (caltype != <span style="color: #0000ff;">null</span><span style="color: #000000;">) {
        </span><span style="color: #0000ff;">switch</span><span style="color: #000000;"> (caltype) {
          </span><span style="color: #0000ff;">case</span> <span style="color: #800000;">"</span><span style="color: #800000;">buddhist</span><span style="color: #800000;">"</span><span style="color: #000000;">:
            cal </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> BuddhistCalendar(zone, aLocale);
            </span><span style="color: #0000ff;">break</span><span style="color: #000000;">;
          </span><span style="color: #0000ff;">case</span> <span style="color: #800000;">"</span><span style="color: #800000;">japanese</span><span style="color: #800000;">"</span><span style="color: #000000;">:
            cal </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> JapaneseImperialCalendar(zone, aLocale);
            </span><span style="color: #0000ff;">break</span><span style="color: #000000;">;
          </span><span style="color: #0000ff;">case</span> <span style="color: #800000;">"</span><span style="color: #800000;">gregory</span><span style="color: #800000;">"</span><span style="color: #000000;">:
            cal </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> GregorianCalendar(zone, aLocale);
            </span><span style="color: #0000ff;">break</span><span style="color: #000000;">;
        }
      }
    }
    </span><span style="color: #0000ff;">if</span> (cal == <span style="color: #0000ff;">null</span><span style="color: #000000;">) {
      </span><span style="color: #0000ff;">if</span> (aLocale.getLanguage() == <span style="color: #800000;">"</span><span style="color: #800000;">th</span><span style="color: #800000;">"</span> &amp;&amp; aLocale.getCountry() == <span style="color: #800000;">"</span><span style="color: #800000;">TH</span><span style="color: #800000;">"</span><span style="color: #000000;">) {
        cal </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> BuddhistCalendar(zone, aLocale);
      } </span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span> (aLocale.getVariant() == <span style="color: #800000;">"</span><span style="color: #800000;">JP</span><span style="color: #800000;">"</span> &amp;&amp; aLocale.getLanguage() == <span style="color: #800000;">"</span><span style="color: #800000;">ja</span><span style="color: #800000;">"</span> &amp;&amp; aLocale.getCountry() == <span style="color: #800000;">"</span><span style="color: #800000;">JP</span><span style="color: #800000;">"</span><span style="color: #000000;">) {
        cal </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> JapaneseImperialCalendar(zone, aLocale);
      } </span><span style="color: #0000ff;">else</span><span style="color: #000000;"> {
        cal </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> GregorianCalendar(zone, aLocale);
      }
    }
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> cal;
  }
  </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
}</pre>
</div>
<span class="cnblogs_code_collapse">①Calendar 类提供了大量跟日期相关的功能代码，同时，又提供了一个 getInstance() 工厂方法，用来根据不同的 TimeZone 和 Locale 创建不同的 Calendar 子类对象，也就是说，功能代码和工厂方法代码耦合在了一个类中。 ②Calendar 类 的getInstance() 方法可以根据不同 TimeZone 和 Locale，创建不同的 Calendar 子类对象（比如 BuddhistCalendar、JapaneseImperialCalendar、GregorianCalendar）。这些细节完全封装在工厂方法中，使用者只需要传递当前的时区和地址，就能够获得一个 Calendar 类对象来使用</span></div>
<p>②建造者模式在 Calendar 类中的应用</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('7fcad8bd-47fd-4d75-b5dc-6b6d61ce0c6b')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_7fcad8bd-47fd-4d75-b5dc-6b6d61ce0c6b" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_7fcad8bd-47fd-4d75-b5dc-6b6d61ce0c6b" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_7fcad8bd-47fd-4d75-b5dc-6b6d61ce0c6b" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">class</span> Calendar implements Serializable, Cloneable, Comparable&lt;Calendar&gt;<span style="color: #000000;"> {
  </span><span style="color: #008000;">//</span><span style="color: #008000;">...</span>
  <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Builder {
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> final <span style="color: #0000ff;">int</span> NFIELDS = FIELD_COUNT + <span style="color: #800080;">1</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> final <span style="color: #0000ff;">int</span> WEEK_YEAR =<span style="color: #000000;"> FIELD_COUNT;
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">long</span><span style="color: #000000;"> instant;
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">int</span><span style="color: #000000;">[] fields;
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">int</span><span style="color: #000000;"> nextStamp;
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">int</span><span style="color: #000000;"> maxFieldIndex;
    </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> String type;
    </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> TimeZone zone;
    </span><span style="color: #0000ff;">private</span> boolean lenient = <span style="color: #0000ff;">true</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> Locale locale;
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">int</span><span style="color: #000000;"> firstDayOfWeek, minimalDaysInFirstWeek;

    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Builder() {}
    
    </span><span style="color: #0000ff;">public</span> Builder setInstant(<span style="color: #0000ff;">long</span><span style="color: #000000;"> instant) {
        </span><span style="color: #0000ff;">if</span> (fields != <span style="color: #0000ff;">null</span><span style="color: #000000;">) {
            </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> IllegalStateException();
        }
        </span><span style="color: #0000ff;">this</span>.instant =<span style="color: #000000;"> instant;
        nextStamp </span>=<span style="color: #000000;"> COMPUTED;
        </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">this</span><span style="color: #000000;">;
    }
    </span><span style="color: #008000;">//</span><span style="color: #008000;">...省略n多set()方法</span>
    
    <span style="color: #0000ff;">public</span><span style="color: #000000;"> Calendar build() {
      </span><span style="color: #0000ff;">if</span> (locale == <span style="color: #0000ff;">null</span><span style="color: #000000;">) {
        locale </span>=<span style="color: #000000;"> Locale.getDefault();
      }
      </span><span style="color: #0000ff;">if</span> (zone == <span style="color: #0000ff;">null</span><span style="color: #000000;">) {
        zone </span>=<span style="color: #000000;"> TimeZone.getDefault();
      }
      Calendar cal;
      </span><span style="color: #0000ff;">if</span> (type == <span style="color: #0000ff;">null</span><span style="color: #000000;">) {
        type </span>= locale.getUnicodeLocaleType(<span style="color: #800000;">"</span><span style="color: #800000;">ca</span><span style="color: #800000;">"</span><span style="color: #000000;">);
      }
      </span><span style="color: #0000ff;">if</span> (type == <span style="color: #0000ff;">null</span><span style="color: #000000;">) {
        </span><span style="color: #0000ff;">if</span> (locale.getCountry() == <span style="color: #800000;">"</span><span style="color: #800000;">TH</span><span style="color: #800000;">"</span> &amp;&amp; locale.getLanguage() == <span style="color: #800000;">"</span><span style="color: #800000;">th</span><span style="color: #800000;">"</span><span style="color: #000000;">) {
          type </span>= <span style="color: #800000;">"</span><span style="color: #800000;">buddhist</span><span style="color: #800000;">"</span><span style="color: #000000;">;
        } </span><span style="color: #0000ff;">else</span><span style="color: #000000;"> {
          type </span>= <span style="color: #800000;">"</span><span style="color: #800000;">gregory</span><span style="color: #800000;">"</span><span style="color: #000000;">;
        }
      }
      </span><span style="color: #0000ff;">switch</span><span style="color: #000000;"> (type) {
        </span><span style="color: #0000ff;">case</span> <span style="color: #800000;">"</span><span style="color: #800000;">gregory</span><span style="color: #800000;">"</span><span style="color: #000000;">:
          cal </span>= <span style="color: #0000ff;">new</span> GregorianCalendar(zone, locale, <span style="color: #0000ff;">true</span><span style="color: #000000;">);
          </span><span style="color: #0000ff;">break</span><span style="color: #000000;">;
        </span><span style="color: #0000ff;">case</span> <span style="color: #800000;">"</span><span style="color: #800000;">iso8601</span><span style="color: #800000;">"</span><span style="color: #000000;">:
          GregorianCalendar gcal </span>= <span style="color: #0000ff;">new</span> GregorianCalendar(zone, locale, <span style="color: #0000ff;">true</span><span style="color: #000000;">);
          </span><span style="color: #008000;">//</span><span style="color: #008000;"> make gcal a proleptic Gregorian</span>
          gcal.setGregorianChange(<span style="color: #0000ff;">new</span><span style="color: #000000;"> Date(Long.MIN_VALUE));
          </span><span style="color: #008000;">//</span><span style="color: #008000;"> and week definition to be compatible with ISO 8601</span>
          setWeekDefinition(MONDAY, <span style="color: #800080;">4</span><span style="color: #000000;">);
          cal </span>=<span style="color: #000000;"> gcal;
          </span><span style="color: #0000ff;">break</span><span style="color: #000000;">;
        </span><span style="color: #0000ff;">case</span> <span style="color: #800000;">"</span><span style="color: #800000;">buddhist</span><span style="color: #800000;">"</span><span style="color: #000000;">:
          cal </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> BuddhistCalendar(zone, locale);
          cal.clear();
          </span><span style="color: #0000ff;">break</span><span style="color: #000000;">;
        </span><span style="color: #0000ff;">case</span> <span style="color: #800000;">"</span><span style="color: #800000;">japanese</span><span style="color: #800000;">"</span><span style="color: #000000;">:
          cal </span>= <span style="color: #0000ff;">new</span> JapaneseImperialCalendar(zone, locale, <span style="color: #0000ff;">true</span><span style="color: #000000;">);
          </span><span style="color: #0000ff;">break</span><span style="color: #000000;">;
        </span><span style="color: #0000ff;">default</span><span style="color: #000000;">:
          </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> IllegalArgumentException(<span style="color: #800000;">"</span><span style="color: #800000;">unknown calendar type: </span><span style="color: #800000;">"</span> +<span style="color: #000000;"> type);
      }
      cal.setLenient(lenient);
      </span><span style="color: #0000ff;">if</span> (firstDayOfWeek != <span style="color: #800080;">0</span><span style="color: #000000;">) {
        cal.setFirstDayOfWeek(firstDayOfWeek);
        cal.setMinimalDaysInFirstWeek(minimalDaysInFirstWeek);
      }
      </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (isInstantSet()) {
        cal.setTimeInMillis(instant);
        cal.complete();
        </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> cal;
      }

      </span><span style="color: #0000ff;">if</span> (fields != <span style="color: #0000ff;">null</span><span style="color: #000000;">) {
        boolean weekDate </span>= isSet(WEEK_YEAR) &amp;&amp; fields[WEEK_YEAR] &gt;<span style="color: #000000;"> fields[YEAR];
        </span><span style="color: #0000ff;">if</span> (weekDate &amp;&amp; !<span style="color: #000000;">cal.isWeekDateSupported()) {
          </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> IllegalArgumentException(<span style="color: #800000;">"</span><span style="color: #800000;">week date is unsupported by </span><span style="color: #800000;">"</span> +<span style="color: #000000;"> type);
        }
        </span><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> stamp = MINIMUM_USER_STAMP; stamp &lt; nextStamp; stamp++<span style="color: #000000;">) {
          </span><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> index = <span style="color: #800080;">0</span>; index &lt;= maxFieldIndex; index++<span style="color: #000000;">) {
            </span><span style="color: #0000ff;">if</span> (fields[index] ==<span style="color: #000000;"> stamp) {
              cal.</span><span style="color: #0000ff;">set</span>(index, fields[NFIELDS +<span style="color: #000000;"> index]);
              </span><span style="color: #0000ff;">break</span><span style="color: #000000;">;
             }
          }
        }

        </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (weekDate) {
          </span><span style="color: #0000ff;">int</span> weekOfYear = isSet(WEEK_OF_YEAR) ? fields[NFIELDS + WEEK_OF_YEAR] : <span style="color: #800080;">1</span><span style="color: #000000;">;
          </span><span style="color: #0000ff;">int</span> dayOfWeek = isSet(DAY_OF_WEEK) ? fields[NFIELDS +<span style="color: #000000;"> DAY_OF_WEEK] : cal.getFirstDayOfWeek();
          cal.setWeekDate(fields[NFIELDS </span>+<span style="color: #000000;"> WEEK_YEAR], weekOfYear, dayOfWeek);
        }
        cal.complete();
      }
      </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> cal;
    }
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Calendar 类用到了建造者模式。我们知道，建造者模式有两种实现方法，一种是单独定义一个 Builder 类，另一种是将 Builder 实现为原始类的内部类。Calendar 就采用了第二种实现思路</span></div>
<p>工厂模式是用来创建不同但是相关类型的对象（继承同一父类或者接口的一组子类），由给定的参数来决定创建哪种类型的对象。</p>
<p>建造者模式用来创建一种类型的复杂对象，通过设置不同的可选参数，&ldquo;定制化&rdquo;地创建不同的对象。</p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">九、从Unix开源开发学习应对大型复杂项目开发</span></strong></span></p>
<p>导致代码质量不高的原因有很多，比如：代码无注释，无文档，命名差，层次结构不清晰，调用关系混乱，到处 hardcode，充斥着各种临时解决方案等等</p>
<p>面对大型复杂项目的开发，如何长期保证代码质量，让代码长期可维护？</p>
<p>1，&nbsp;吹毛求疵般地执行编码规范</p>
<ul>
<li><span style="font-size: 12px;">严格执行代码规范、统一风格。</span></li>
<li><span style="font-size: 12px;">良好的变量命名、函数、类和注释。</span></li>
<li><span style="font-size: 12px;">在 Code Review 时，我们一定要严格要求，看到不符合规范的代码，一定要指出并要求修改</span></li>
</ul>
<p>2，编写高质量的单元测试</p>
<ul>
<li><span style="font-size: 12px;">单元测试是最容易执行且对提高代码质量见效最快的方法之一</span></li>
<li><span style="font-size: 12px;">除了测试正常逻辑的执行之外，还要重点、全面地测试异常下的执行情况。毕竟代码出问题的地方大部分都发生在异常、边界条件下</span></li>
</ul>
<p>3，不流于形式的 Code Review</p>
<ul>
<li><span style="font-size: 12px;">要想真正发挥 Code Review 的作用，关键还是要执行到位，不能流于形式</span></li>
</ul>
<p>4，开发未动、文档先行</p>
<ul>
<li><span style="font-size: 12px;">一般来讲，在开发某个系统或者重要模块或者功能之前，我们应该先写技术文档，然后，发送给同组或者相关同事审查，在审查没有问题的情况下再开发。这样能够保证事先达成共识，开发出来的东西不至于走样</span></li>
<li><span style="font-size: 12px;">而且，当开发完成之后，进行 Code Review 的时候，代码审查者通过阅读开发文档，也可以快速理解代码</span></li>
<li><span style="font-size: 12px;">对于团队和公司来讲，文档是重要的财富。对新人熟悉代码或任务的交接等，技术文档很有帮助</span></li>
</ul>
<p>5，持续重构、重构、重构</p>
<ul>
<li><span style="font-size: 12px;">&nbsp;不支持大刀阔斧、推倒重来式的大重构，但持续的小重构我还是比较提倡的。它也是时刻保证代码质量、防止代码腐化的有效手段。换句话说，不要等到问题堆得太多了再去解决，要时刻有人对代码整体质量负责任，平时没事就改改代码。千万不要觉得重构代码就是浪费时间，不务正业！</span></li>
<li><span style="font-size: 12px;">特别是一些业务开发团队，有时候为了快速完成一个业务需求，只追求速度，到处 hard code，在完全不考虑非功能性需求、代码质量的情况下，堆砌烂代码。实际上，这种情况还是比较常见的。不过没关系，等你有时间了，一定要记着重构，不然烂代码越堆越多，总有一天代码会变得无法维护。</span></li>
</ul>
<p>6，对项目与团队进行拆分</p>
<ul>
<li><span style="font-size: 12px;">团队人比较少，比如十几个人的时候，代码量不多，不超过 10 万行，怎么开发、怎么管理都没问题，大家互相都比较了解彼此做的东西。即便代码质量太差了，我们大不了把它重写一遍。但是，对于一个大型项目来说，参与开发的人员会比较多，代码量很大，有几十万、甚至几百万行代码，有几十、甚至几百号人同时开发维护，那研发管理就变得极其重要。</span></li>
<li><span style="font-size: 12px;">面对大型复杂项目，我们不仅仅需要对代码进行拆分，还需要对研发团队进行拆分。上一节课我们讲到了一些代码拆分的方法，比如模块化、分层等。同理，我们也可以把大团队拆成几个小团队。每个小团队对应负责一个小的项目（模块、微服务等），这样每个团队负责的项目包含的代码都不至于很多，也不至于出现代码质量太差无法维护的情况</span></li>
</ul>
<p>7，Code Review</p>
<p><strong>①有人认为，Code Review 流程太长，太浪费时间，特别是工期紧的时候，今天改的代码，明天就要上，如果要等同事 Review，同事有可能没时间，这样就来不及。这个时候该怎么办呢？</strong></p>
<p>我所经历的项目还没有一个因为工期紧，导致没有时间 Code Review 的。工期都是人排的，稍微排松点就行了啊。我觉得关键还是在于整个公司对 Code Review 的接受程度。而且，Code Review 熟练之后，并不需要花费太长的时间。尽管开始做 Code Review 的时候，你可能因为不熟练，需要有一个 checklist 对照着来做。起步阶段可能会比较耗时。但当你熟练之后，Code Review 就像键盘盲打一样，你已经忘记了哪个手指按的是哪个键了，扫一遍代码就能揪出绝大部分问题。</p>
<p><strong>②有人认为，业务一直在变，今天写的代码明天可能就要再改，代码可能不会长期维护，写得太好也没用。这种情况下是不是就不需要 Code Review 了呢？</strong></p>
<p>项目讲求短平快，先验证产品，再优化技术。如果确实面对的还只是生存问题，代码质量确实不是首要的，特殊情况下，不做 Code Review 是支持的！</p>
<p>团队成员技术水平不高，过往也没有 Code Review 的经验，可以先让资深同事、技术好的同事或技术 leader，来 Review 其他所有人的代码。Review 的过程本身就是一种&ldquo;传帮带&rdquo;的过程。慢慢地，整个团队就知道该如何 Review 了。虽然这可能会有一个相当长的过程，但如果真的想在团队中执行 Code Review，这不失为一种&ldquo;曲线救国&rdquo;的方法。</p>
<p><strong>③还有人说，刚开始 Code Review 的时候，大家都还挺认真，但时间长了，大家觉得这事跟 KPI 无关，而且我还要看别人的代码，理解别人写的代码的业务，多浪费时间啊。慢慢地，Code Review 就变得流于形式了。有人提交了代码，随便抓个人 Review。Review 的人也不认真，随便扫一眼就点&ldquo;approve&rdquo;。这种情况该如何应对？</strong></p>
<p>首先，要明确的告诉 Code Review 的重要性，要严格执行，让大家不要懈怠，适当的时候可以&ldquo;杀鸡儆猴&rdquo;。其次，可以像 Google 一样，将 Code Review 间接地跟 KPI、升职等联系在一块，高级工程师有义务做 Code Review，就像有义务做技术面试一样。再次，想办法活跃团队的技术氛围，把 Code Review 作为一种展示自己技术的机会，带动起大家对 Code Review 的积极性，提高大家对 Code Review 的认同感。</p>
<p>&nbsp;</p>
<p style="font-size: 18pt; background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;">十、借Google Guava学习发现和开发通用功能模块</span></strong></span></p>
<p>1，在业务开发中，跟业务无关的通用功能模块，常见的一般有三类：类库（library）、框架（framework）、功能组件（component）等。</p>
<ul>
<li><span style="font-size: 12px;">类库：&nbsp;提供一组 API 接口（例如Google Guava 属于类库）</span></li>
<li><span style="font-size: 12px;">框架：EventBus、DI 容器属于框架，提供骨架代码，能让业务开发人员聚焦在业务开发部分，在预留的扩展点里填充业务代码</span></li>
<li><span style="font-size: 12px;">功能组件：ID 生成器、性能计数器属于功能组件，提供一组具有某一特殊功能的 API 接口，有点类似类库，但更加聚焦和重量级，比如，ID 生成器有可能会依赖 Redis 等外部系统，不像类库那么简单。</span></li>
</ul>
<p>&nbsp;实际上，不管是类库、框架还是功能组件，这些通用功能模块有两个最大的特点：复用和业务无关。</p>
<p>2，Builder 模式在 Guava 中的应用</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('68c6081d-f729-4d70-9271-56012590f107')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_68c6081d-f729-4d70-9271-56012590f107" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_68c6081d-f729-4d70-9271-56012590f107" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_68c6081d-f729-4d70-9271-56012590f107" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> CacheDemo {
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> main(String[] args) {
    Cache</span>&lt;String, String&gt; cache =<span style="color: #000000;"> CacheBuilder.newBuilder()
            .initialCapacity(</span><span style="color: #800080;">100</span><span style="color: #000000;">)
            .maximumSize(</span><span style="color: #800080;">1000</span><span style="color: #000000;">)
            .expireAfterWrite(</span><span style="color: #800080;">10</span><span style="color: #000000;">, TimeUnit.MINUTES)
            .build();

    cache.put(</span><span style="color: #800000;">"</span><span style="color: #800000;">key1</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">value1</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    String value </span>= cache.getIfPresent(<span style="color: #800000;">"</span><span style="color: #800000;">key1</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    System.</span><span style="color: #0000ff;">out</span><span style="color: #000000;">.println(value);
  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Cache 对象是通过 CacheBuilder 这样一个 Builder 类来创建的。</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('c0c17f84-4174-4e5e-825c-10f3405185b6')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_c0c17f84-4174-4e5e-825c-10f3405185b6" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_c0c17f84-4174-4e5e-825c-10f3405185b6" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_c0c17f84-4174-4e5e-825c-10f3405185b6" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> &lt;K1 extends K, V1 extends V&gt; Cache&lt;K1, V1&gt;<span style="color: #000000;"> build() {
  </span><span style="color: #0000ff;">this</span><span style="color: #000000;">.checkWeightWithWeigher();
  </span><span style="color: #0000ff;">this</span><span style="color: #000000;">.checkNonLoadingCache();
  </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> LocalManualCache(<span style="color: #0000ff;">this</span><span style="color: #000000;">);
}

</span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> checkNonLoadingCache() {
  Preconditions.checkState(</span><span style="color: #0000ff;">this</span>.refreshNanos == -<span style="color: #800080;">1L</span>, <span style="color: #800000;">"</span><span style="color: #800000;">refreshAfterWrite requires a LoadingCache</span><span style="color: #800000;">"</span><span style="color: #000000;">);
}

</span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> checkWeightWithWeigher() {
  </span><span style="color: #0000ff;">if</span> (<span style="color: #0000ff;">this</span>.weigher == <span style="color: #0000ff;">null</span><span style="color: #000000;">) {
    Preconditions.checkState(</span><span style="color: #0000ff;">this</span>.maximumWeight == -<span style="color: #800080;">1L</span>, <span style="color: #800000;">"</span><span style="color: #800000;">maximumWeight requires weigher</span><span style="color: #800000;">"</span><span style="color: #000000;">);
  } </span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span> (<span style="color: #0000ff;">this</span><span style="color: #000000;">.strictParsing) {
    Preconditions.checkState(</span><span style="color: #0000ff;">this</span>.maximumWeight != -<span style="color: #800080;">1L</span>, <span style="color: #800000;">"</span><span style="color: #800000;">weigher requires maximumWeight</span><span style="color: #800000;">"</span><span style="color: #000000;">);
  } </span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span> (<span style="color: #0000ff;">this</span>.maximumWeight == -<span style="color: #800080;">1L</span><span style="color: #000000;">) {
    logger.log(Level.WARNING, </span><span style="color: #800000;">"</span><span style="color: #800000;">ignoring weigher specified without maximumWeight</span><span style="color: #800000;">"</span><span style="color: #000000;">);
  }

}</span></pre>
</div>
<span class="cnblogs_code_collapse">必须使用 Builder 模式的主要原因是，在真正构造 Cache 对象的时候，我们必须做一些必要的参数校验，也就是 build() 函数中前两行代码要做的工作。如果采用无参默认构造函数加 setXXX() 方法的方案，这两个校验就无处安放了。而不经过校验，创建的 Cache 对象有可能是不合法、不可用的。</span></div>
<p>3，函数式编程</p>
<p>函数式编程因其编程的特殊性，仅在科学计算、数据处理、统计分析等领域，才能更好地发挥它的优势，所以，我个人觉得，它并不能完全替代更加通用的面向对象编程范式。</p>
<ul>
<li><span style="font-size: 12px;">面向对象编程最大的特点是：以类、对象作为组织代码的单元以及它的四大特性。</span></li>
<li><span style="font-size: 12px;">面向过程编程最大的特点是：以函数作为组织代码的单元，数据与方法相分离。&nbsp;</span></li>
<li><span style="font-size: 12px;">函数式编程：函数式编程最独特的地方在于它的编程思想。函数式编程认为，程序可以用一系列数学函数或表达式的组合来表示。函数式编程是程序面向数学的更底层的抽象，将计算过程描述为表达式</span></li>
</ul>
<div class="cnblogs_code" onclick="cnblogs_code_show('53e0fb81-f0cb-4894-9308-e5b29515e462')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_53e0fb81-f0cb-4894-9308-e5b29515e462" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_53e0fb81-f0cb-4894-9308-e5b29515e462" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_53e0fb81-f0cb-4894-9308-e5b29515e462" class="cnblogs_code_hide">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> 有状态函数: 执行结果依赖b的值是多少，即便入参相同，多次执行函数，函数的返回值有可能不同，因为b值有可能不同。</span>
<span style="color: #0000ff;">int</span><span style="color: #000000;"> b;
</span><span style="color: #0000ff;">int</span> increase(<span style="color: #0000ff;">int</span><span style="color: #000000;"> a) {
  </span><span style="color: #0000ff;">return</span> a +<span style="color: #000000;"> b;
}

</span><span style="color: #008000;">//</span><span style="color: #008000;"> 无状态函数：执行结果不依赖任何外部变量值，只要入参相同，不管执行多少次，函数的返回值就相同</span>
<span style="color: #0000ff;">int</span> increase(<span style="color: #0000ff;">int</span> a, <span style="color: #0000ff;">int</span><span style="color: #000000;"> b) {
  </span><span style="color: #0000ff;">return</span> a +<span style="color: #000000;"> b;
}</span></pre>
</div>
<span class="cnblogs_code_collapse">它跟面向过程编程的区别在于，它的函数是无状态的。何为无状态？简单点讲就是，函数内部涉及的变量都是局部变量，不会像面向对象编程那样，共享类成员变量，也不会像面向过程编程那样，共享全局变量。函数的执行结果只与入参有关，跟其他任何外部变量无关。同样的入参，不管怎么执行，得到的结果都是一样的。这实际上就是数学函数或数学表达式的基本要求。</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('6f84a45b-6e49-4292-92db-9630ed42608f')"><img src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" id="code_img_closed_6f84a45b-6e49-4292-92db-9630ed42608f" class="code_img_closed" /><img src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" id="code_img_opened_6f84a45b-6e49-4292-92db-9630ed42608f" class="code_img_opened" style="display: none;" />
<div id="cnblogs_code_open_6f84a45b-6e49-4292-92db-9630ed42608f" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> FPDemo {
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> main(String[] args) {
    Optional</span>&lt;Integer&gt; result = Stream.of(<span style="color: #800000;">"</span><span style="color: #800000;">f</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">ba</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">hello</span><span style="color: #800000;">"</span><span style="color: #000000;">)
            .map(s </span>-&gt;<span style="color: #000000;"> s.length())
            .filter(l </span>-&gt; l &lt;= <span style="color: #800080;">3</span><span style="color: #000000;">)
            .max((o1, o2) </span>-&gt; o1-<span style="color: #000000;">o2);
    System.</span><span style="color: #0000ff;">out</span>.println(result.<span style="color: #0000ff;">get</span>()); <span style="color: #008000;">//</span><span style="color: #008000;"> 输出2</span>
<span style="color: #000000;">  }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">这段代码的作用是从一组字符串数组中，过滤出长度小于等于 3 的字符串，并且求得这其中的最大长度。</span></div>
<p>Java 为函数式编程引入了三个新的语法概念：Stream 类、Lambda 表达式和函数接口（Functional Inteface）。Stream 类用来支持通过&ldquo;.&rdquo;级联多个函数操作的代码编写方式；引入 Lambda 表达式的作用是简化代码编写；函数接口的作用是让我们可以把函数包裹成函数接口，来实现把函数当做参数一样来使用</p>
<p>&nbsp;</p>