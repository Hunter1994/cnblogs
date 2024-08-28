<p><a href="#a1"><strong>一、Grain持久性</strong></a></p>
<p><a href="#a2"><strong>二、定时器和提醒</strong></a></p>
<p><a href="#a3"><strong>三、依赖注入</strong></a></p>
<p><a href="#a4"><strong>四、观察者</strong></a></p>
<p><a href="#a5"><strong><strong>五、无状态工作者Grains</strong></strong></a></p>
<p><a href="#a6"><strong><strong>六、流</strong></strong></a></p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a1"></a>一、Grain持久化</span></strong></span></p>
<p>1，Grain持久化目标&nbsp;</p>
<p>①允许不同类型的存储提供者使用不同类型的存储提供者（例如，一个使用Azure表，一个使用ADO.NET表），或者使用不同类型的存储提供者，但具有不同的配置（例如，两者都使用Azure表， 存储帐户＃1和一个使用存储帐户＃2）</p>
<p>②允许配置存储提供程序实例（例如Dev-Test-Prod），只更改配置文件，不需要更改代码。</p>
<p>③提供一个框架，以便稍后由Orleans团队或其他人编写其他存储提供程序。</p>
<p>④提供最少量的生产级存储提供商</p>
<p>⑤存储提供者可以完全控制他们如何在持久性后台存储中存储Grain状态数据。 推论：Orleans没有提供全面的ORM存储解决方案，但允许定制存储提供商在需要时支持特定的ORM要求。</p>
<p>2，Grain持久化Api</p>
<p>Grain类型可以通过以下两种方式之一进行声明：</p>
<ul>
<li>如果它们没有任何持久状态，或者它们将自己处理所有的持续状态，则扩展<span style="background-color: #ffff99; color: #ff0000;">Grain</span></li>
<li>如果他们有一些他们想要Orleans运行时处理的持续状态，请扩展<span style="background-color: #ffff99; color: #ff0000;">Grain &lt;T&gt;</span>。 换句话说，通过扩展<span style="color: #ff0000; background-color: #ffff99;">Grain &lt;T&gt;</span>，grain类型自动加入到Orleans系统管理的持久化框架中。</li>
</ul>
<p>对于本节的其余部分，我们将只考虑选项＃2 / Grain &lt;T&gt;，因为选项1的Grain将继续像现在一样运行而不会有任何行为改变。</p>
<p>3，Grain状态存储</p>
<p>从Grain &lt;T&gt;继承的Grain类（其中T是需要持久化的特定于应用程序的状态数据类型）将从指定的存储区自动加载它们的状态。</p>
<p>Grain将被标记为[StorageProvider]属性，该属性指定用于读取/写入谷物的状态数据的存储提供者的命名实例。</p>
<div class="cnblogs_code">
<pre>[StorageProvider(ProviderName=<span style="color: #800000;">"</span><span style="color: #800000;">store1</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> MyGrain&lt;MyGrainState&gt;<span style="color: #000000;"> ...
{
  ...
}</span></pre>
</div>
<p>Orleans提供者管理框架提供了一种机制，指定和注册仓储配置文件不同的存储供应商和存储选项。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">OrleansConfiguration </span><span style="color: #ff0000;">xmlns</span><span style="color: #0000ff;">="urn:orleans"</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Globals</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">StorageProviders</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Provider </span><span style="color: #ff0000;">Type</span><span style="color: #0000ff;">="Orleans.Storage.MemoryStorage"</span><span style="color: #ff0000;"> Name</span><span style="color: #0000ff;">="DevStore"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Provider </span><span style="color: #ff0000;">Type</span><span style="color: #0000ff;">="Orleans.Storage.AzureTableStorage"</span><span style="color: #ff0000;"> Name</span><span style="color: #0000ff;">="store1"</span><span style="color: #ff0000;">
            DataConnectionString</span><span style="color: #0000ff;">="DefaultEndpointsProtocol=https;AccountName=data1;AccountKey=SOMETHING1"</span> <span style="color: #0000ff;">/&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Provider </span><span style="color: #ff0000;">Type</span><span style="color: #0000ff;">="Orleans.Storage.AzureBlobStorage"</span><span style="color: #ff0000;"> Name</span><span style="color: #0000ff;">="store2"</span><span style="color: #ff0000;">
            DataConnectionString</span><span style="color: #0000ff;">="DefaultEndpointsProtocol=https;AccountName=data2;AccountKey=SOMETHING2"</span>  <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">StorageProviders</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>4，配置存储提供程序</p>
<p>①AzureTableStorage</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Provider </span><span style="color: #ff0000;">Type</span><span style="color: #0000ff;">="Orleans.Storage.AzureTableStorage"</span><span style="color: #ff0000;"> Name</span><span style="color: #0000ff;">="TableStore"</span><span style="color: #ff0000;">
    DataConnectionString</span><span style="color: #0000ff;">="UseDevelopmentStorage=true"</span> <span style="color: #0000ff;">/&gt;</span></pre>
</div>
<p>以下属性可以添加到&lt;Provider /&gt;元素来配置提供程序：</p>
<ul>
<li><code>DataConnectionString="..."（必需） - 要使用的Azure存储连接字符串</code></li>
<li><code>TableName="OrleansGrainState"</code>&nbsp;（可选） - 表格存储中使用的表格名称，默认为OrleansGrainState</li>
<li><code>DeleteStateOnClear="false"</code>&nbsp;（可选） - 如果为true，则在grain状态被清除时记录将被删除，否则将写入空记录，默认为false</li>
<li><code>UseJsonFormat="false"</code>&nbsp;（可选） - 如果为true，则使用json序列化程序，否则将使用Orleans二进制序列化程序，默认为false</li>
<li><code>UseFullAssemblyNames="false"（可选） - （如果UseJsonFormat =&ldquo;true&rdquo;）序列化具有完整程序集名称（true）或简单（false）的类型，默认为false</code></li>
<li><code>IndentJSON="false"（可选） - （如果UseJsonFormat =&ldquo;true&rdquo;）缩进序列化的json，默认为false</code></li>
</ul>
<p>注意：状态不应超过64KB，由表存储限制。</p>
<p>②AzureBlobStorage</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Provider </span><span style="color: #ff0000;">Type</span><span style="color: #0000ff;">="Orleans.Storage.AzureTableStorage"</span><span style="color: #ff0000;"> Name</span><span style="color: #0000ff;">="BlobStore"</span><span style="color: #ff0000;">
    DataConnectionString</span><span style="color: #0000ff;">="UseDevelopmentStorage=true"</span> <span style="color: #0000ff;">/&gt;</span></pre>
</div>
<p>以下属性可以添加到&lt;Provider /&gt;元素来配置提供程序：</p>
<ul>
<li><code>DataConnectionString="..."</code>&nbsp;（必需） - 要使用的Azure存储连接字符串</li>
<li><code>ContainerName="grainstate"</code>&nbsp;（可选） - 要使用的Blob存储容器，默认为grainstate</li>
<li><code>UseFullAssemblyNames="false"</code>&nbsp;（可选） - 使用完整程序集名称（true）或简单（false）序列化类型，默认为false</li>
<li><code>IndentJSON="false"</code>&nbsp;（可选） - 缩进序列化的json，默认为false</li>
</ul>
<p>③DynamoDBStorageProvider</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Provider </span><span style="color: #ff0000;">Type</span><span style="color: #0000ff;">="Orleans.Storage.DynamoDBStorageProvider"</span><span style="color: #ff0000;"> Name</span><span style="color: #0000ff;">="DDBStore"</span><span style="color: #ff0000;">
    DataConnectionString</span><span style="color: #0000ff;">="Service=us-wes-1;AccessKey=MY_ACCESS_KEY;SecretKey=MY_SECRET_KEY;"</span> <span style="color: #0000ff;">/&gt;</span></pre>
</div>
<ul>
<li><code>DataConnectionString="..."（必需） - 要使用的DynamoDB存储连接字符串。 您可以在其中设置Service，AccessKey，SecretKey，ReadCapacityUnits和WriteCapacityUnits。</code></li>
<li><code>TableName="OrleansGrainState"</code>&nbsp;（可选） - 表格存储中使用的表格名称，默认为OrleansGrainState</li>
<li><code>DeleteStateOnClear="false"</code>&nbsp;（可选） - 如果为true，则在grain状态被清除时记录将被删除，否则将写入空记录，默认为false</li>
<li><code>UseJsonFormat="false"</code>&nbsp;（可选） - 如果为true，则使用json序列化程序，否则将使用Orleans二进制序列化程序，默认为false</li>
<li><code>UseFullAssemblyNames="false"</code>&nbsp;（可选） - （如果UseJsonFormat =&ldquo;true&rdquo;）序列化具有完整程序集名称（true）或简单（false）的类型，默认为false</li>
<li><code>IndentJSON="false"</code>&nbsp;（可选） - （如果UseJsonFormat =&ldquo;true&rdquo;）缩进序列化的json，默认为false</li>
</ul>
<p>④ADO.NET Storage Provider (SQL Storage Provider)</p>
<p>ADO .NET存储提供程序允许您在关系数据库中存储grain状态。 目前支持以下数据库：</p>
<ul>
<li>SQL Server</li>
<li>MySQL/MariaDB</li>
<li>PostgreSQL</li>
<li>Oracle</li>
</ul>
<p>首先，安装基础包：&nbsp;<span class="cnblogs_code">Install-Package Microsoft.Orleans.OrleansSqlUtils</span>&nbsp;</p>
<p>在与您的项目一起安装软件包的文件夹下，可以找到支持数据库供应商的不同SQL脚本。 你也可以从OrleansSQLUtils仓库获取它们。 创建一个数据库，然后运行适当的脚本来创建表。</p>
<p>接下来的步骤是安装第二个NuGet软件包（请参阅下表），并根据需要安装数据库供应商，并以编程方式或通过XML配置来配置存储提供程序。</p>
<table class="table table-bordered table-striped table-condensed" border="1">
<thead>
<tr><th>Database</th><th>Script</th><th>NuGet Package</th><th>AdoInvariant</th><th>Remarks</th></tr>
</thead>
<tbody>
<tr>
<td>SQL Server</td>
<td><a href="https://github.com/dotnet/orleans/blob/master/src/OrleansSQLUtils/CreateOrleansTables_SQLServer.sql">CreateOrleansTables_SQLServer.sql</a></td>
<td><a href="https://www.nuget.org/packages/System.Data.SqlClient/">System.Data.SqlClient</a></td>
<td>System.Data.SqlClient</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>MySQL / MariaDB</td>
<td><a href="https://github.com/dotnet/orleans/blob/master/src/OrleansSQLUtils/CreateOrleansTables_MySQL.sql">CreateOrleansTables_MySQL.sql</a></td>
<td><a href="https://www.nuget.org/packages/MySql.Data/">MySql.Data</a></td>
<td>MySql.Data.MySqlClient</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>PostgreSQL</td>
<td><a href="https://github.com/dotnet/orleans/blob/master/src/OrleansSQLUtils/CreateOrleansTables_PostgreSQL.sql">CreateOrleansTables_PostgreSQL.sql</a></td>
<td><a href="https://www.nuget.org/packages/Npgsql/">Npgsql</a></td>
<td>Npgsql</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>Oracle</td>
<td><a href="https://github.com/dotnet/orleans/blob/master/src/OrleansSQLUtils/CreateOrleansTables_Oracle.sql">CreateOrleansTables_Oracle.sql</a></td>
<td><a href="https://www.nuget.org/packages/Oracle.ManagedDataAccess/">ODP.net</a></td>
<td>Oracle.DataAccess.Client</td>
<td>No .net Core support</td>
</tr>
</tbody>
</table>
<p>&nbsp;以下是如何使用XML配置来配置ADO .NET存储提供程序的示例：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">OrleansConfiguration </span><span style="color: #ff0000;">xmlns</span><span style="color: #0000ff;">="urn:orleans"</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Globals</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">StorageProviders</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Provider </span><span style="color: #ff0000;">Type</span><span style="color: #0000ff;">="Orleans.Storage.AdoNetStorageProvider"</span><span style="color: #ff0000;">
                Name</span><span style="color: #0000ff;">="OrleansStorage"</span><span style="color: #ff0000;">
                AdoInvariant</span><span style="color: #0000ff;">="&lt;AdoInvariant&gt;"</span><span style="color: #ff0000;">
                DataConnectionString</span><span style="color: #0000ff;">="&lt;ConnectionString&gt;"</span><span style="color: #ff0000;">
                UseJsonFormat</span><span style="color: #0000ff;">="true"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">StorageProviders</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Globals</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">OrleansConfiguration</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>在代码中，你需要像下面这样的东西：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> properties = <span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">string</span>&gt;<span style="color: #000000;">()
{
    [</span><span style="color: #800000;">"</span><span style="color: #800000;">AdoInvariant</span><span style="color: #800000;">"</span>] = <span style="color: #800000;">"</span><span style="color: #800000;">&lt;AdoInvariant&gt;</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    [</span><span style="color: #800000;">"</span><span style="color: #800000;">DataConnectionString</span><span style="color: #800000;">"</span>] = <span style="color: #800000;">"</span><span style="color: #800000;">&lt;ConnectionString&gt;</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    [</span><span style="color: #800000;">"</span><span style="color: #800000;">UseJsonFormat</span><span style="color: #800000;">"</span>] = <span style="color: #800000;">"</span><span style="color: #800000;">true</span><span style="color: #800000;">"</span><span style="color: #000000;">
};

config.Globals.RegisterStorageProvider</span>&lt;AdoNetStorageProvider&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">OrleansStorage</span><span style="color: #800000;">"</span>, properties);</pre>
</div>
<p>本质上，您只需要设置数据库供应商特定的连接字符串和标识供应商的AdoInvariant（参见上表）。 您也可以选择保存数据的格式，可以是二进制（默认），JSON或XML。 虽然二进制是最紧凑的选项，但它是不透明的，你将无法读取或处理数据。 JSON是推荐的选项。</p>
<p>您可以设置以下属性：</p>
<table class="table table-bordered table-striped table-condensed" border="1" frame="border">
<thead>
<tr><th>Name</th><th>Type</th><th>Description</th></tr>
</thead>
<tbody>
<tr>
<td>Name</td>
<td>String</td>
<td>持久性Grain将用于引用这个存储提供程序的任意名称</td>
</tr>
<tr>
<td>Type</td>
<td>String</td>
<td>设置为&nbsp;<code>Orleans.Storage.AdoNetStorageProvider</code></td>
</tr>
<tr>
<td>AdoInvariant</td>
<td>String</td>
<td>标识数据库供应商(请参阅上表中的值;默认是System.Data.SqlClient)</td>
</tr>
<tr>
<td>DataConnectionString</td>
<td>String</td>
<td>供应商特定的数据库连接字符串（必需）</td>
</tr>
<tr>
<td>UseJsonFormat</td>
<td>Boolean</td>
<td>使用JSON格式（推荐）</td>
</tr>
<tr>
<td>UseXmlFormat</td>
<td>Boolean</td>
<td>使用XML格式</td>
</tr>
<tr>
<td>UseBinaryFormat</td>
<td>Boolean</td>
<td>使用紧凑的二进制格式（默认）</td>
</tr>
</tbody>
</table>
<p><a href="https://github.com/dotnet/orleans/tree/master/Samples/StorageProviders">StorageProviders</a>示例提供了一些代码，您可以使用它们来快速测试以上内容，并展示一些自定义存储提供程序。 在软件包管理器控制台中使用以下命令将所有的Orleans软件包更新到最新版本：</p>
<div class="cnblogs_code">
<pre>Get-Package | <span style="color: #0000ff;">where</span> Id -like <span style="color: #800000;">'</span><span style="color: #800000;">Microsoft.Orleans.*</span><span style="color: #800000;">'</span> | <span style="color: #0000ff;">foreach</span> { update-package $_.Id }</pre>
</div>
<p>ADO.NET持久性具有对数据进行版本化的功能，并可以使用任意应用程序规则和流来定义任意（de）序列化程序，但目前没有办法将它们公开给应用程序代码。</p>
<p>⑤MemoryStorage</p>
<p>MemoryStorage是一个简单的存储提供者，它并不真正使用下面的持久数据存储。 了解如何快速与存储提供商合作很方便，但不打算在实际情况下使用。</p>
<p><span style="font-size: 12px; color: #ff0000;">注意:这个提供者将状态持久化到不稳定的内存中，该内存在仓储关闭时被删除。只使用进行测试。</span></p>
<p>使用XML配置设置内存存储提供程序：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;?</span><span style="color: #ff00ff;">xml version="1.0" encoding="utf-8"</span><span style="color: #0000ff;">?&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">OrleansConfiguration </span><span style="color: #ff0000;">xmlns</span><span style="color: #0000ff;">="urn:orleans"</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Globals</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">StorageProviders</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Provider </span><span style="color: #ff0000;">Type</span><span style="color: #0000ff;">="Orleans.Storage.MemoryStorage"</span><span style="color: #ff0000;">
                Name</span><span style="color: #0000ff;">="OrleansStorage"</span><span style="color: #ff0000;">
                NumStorageGrains</span><span style="color: #0000ff;">="10"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">StorageProviders</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Globals</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">OrleansConfiguration</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>要在代码中设置它：</p>
<div class="cnblogs_code">
<pre>siloHost.Config.Globals.RegisterStorageProvider&lt;MemoryStorage&gt;(<span style="color: #800000;">"</span><span style="color: #800000;">OrleansStorage</span><span style="color: #800000;">"</span>);</pre>
</div>
<p>您可以设置以下属性：</p>
<div class="table-responsive">
<table class="table table-bordered table-striped table-condensed" border="1" frame="border">
<thead>
<tr><th>Name</th><th>Type</th><th>Description</th></tr>
</thead>
<tbody>
<tr>
<td>Name</td>
<td>String</td>
<td>持久性Grain将用于引用这个存储提供程序的任意名称</td>
</tr>
<tr>
<td>Type</td>
<td>String</td>
<td>设置为&nbsp;<code>Orleans.Storage.MemoryStorage</code></td>
</tr>
<tr>
<td>NumStorageGrains</td>
<td>Integer</td>
<td>用来存储状态的Grain数量，默认为10</td>
</tr>
</tbody>
</table>
</div>
<p>⑥ShardedStorageProvider</p>
<div class="cnblogs_code">
<pre>&lt;Provider Type=<span style="color: #800000;">"</span><span style="color: #800000;">Orleans.Storage.ShardedStorageProvider</span><span style="color: #800000;">"</span> Name=<span style="color: #800000;">"</span><span style="color: #800000;">ShardedStorage</span><span style="color: #800000;">"</span>&gt;
    &lt;Provider /&gt;
    &lt;Provider /&gt;
    &lt;Provider /&gt;
&lt;/Provider&gt;</pre>
</div>
<p>简单的存储提供程序，用于编写多个其他存储提供程序共享的Grain状态数据。</p>
<p>一致的散列函数（默认是Jenkins Hash）用于决定哪个碎片（按照它们在配置文件中定义的顺序）负责存储指定Grain的状态数据，然后将读/写/清除请求桥接 到合适的底层提供者执行。</p>
<p>⑦存储提供者的注意事项</p>
<p>如果没有为Grain &lt;T&gt; grain类指定[StorageProvider]属性，则会搜索名为Default的提供程序。 如果没有找到，则将其视为缺少的存储提供者。</p>
<p>如果在仓储配置文件中只有一个提供者，它将被视为这个仓储的默认提供者。</p>
<p>使用存储提供程序的Grain（Grain装载时不存在并定义在Grain配置中）将无法加载，但是仓储里的其他Grain仍然可以装载和运行。Orleans之后的任何一种Grain类型的调用都将失败。指定未加载Grain类型的Storage.BadProviderConfigException错误。</p>
<p>用于给定Grain类型的存储提供程序实例由该Grain类型的[StorageProvider]属性中定义的存储提供程序名称，加上仓储配置中定义的提供者的提供者类型和配置选项。</p>
<p>不同的Grain类型可以使用不同的配置存储提供程序，即使它们是相同的类型：例如，两个不同的Azure表存储提供程序实例连接到不同的Azure存储帐户（请参阅上面的配置文件示例）。</p>
<p>存储提供程序的所有配置详细信息是在仓储启动时读取的仓储配置中静态定义的。 目前没有提供机制来动态更新或更改仓储所使用的存储提供商列表。 但是，这是一个优先/工作量约束，而不是一个基本的设计约束。</p>
<p>&nbsp;</p>
<p>5，状态存储API</p>
<p>对于Grain 状态/持久性api有两个主要部分:grainto - runtime和runtimeto - storage - provider。</p>
<p>&nbsp;</p>
<p>6，Grain状态存储API</p>
<p>Orleans Runtime中的Grain状态存储功能将提供读写操作，以自动填充/保存该Grain的GrainState数据对象。 在内部，这些功能将被连接到通过配置为该Grain适当持久性提供（由Orleans&nbsp;客户端根工具生成的代码中）。&nbsp;</p>
<p>&nbsp;</p>
<p>7，Grain状态读/写功能</p>
<p>当Grain被激活时，Grain状态将自动被读取，但是Grain负责明确地触发任何改变的Grain状态的写入。 有关错误处理机制的详细信息，请参见下面的失败模式部分。</p>
<p>在为该激活调用OnActivateAsync()方法之前，将自动读取GrainState（使用base.ReadStateAsync()的等效项）。 在任何方法调用Grain之前，Grain状态不会被刷新，除非这个Grain被激活了。</p>
<p>在任何grain方法调用期间，grain可以请求Orleans运行时通过调用base.WriteStateAsync()将该激活的当前grain状态数据写入指定的存储提供者。 grain是负责执行明确写操作时，他们做出显著更新他们的状态数据。 最常见的是，grain方法将返回base.WriteStateAsync()任务作为从grain方法返回的最终结果Task，但不要求遵循此模式。 在任何grain方法之后，运行时不会自动更新存储的粮食状态。</p>
<p>在grain中的grain方法或定时器回调处理程序期间，grain可以通过调用base.ReadStateAsync()来请求Orleans运行时从指定的存储提供程序重新读取当前的grain状态数据。 这将使用从持久性存储中读取的最新值完全覆盖当前存储在Grain状态对象中的当前状态数据。</p>
<p>不透明的特定于提供者的Etag值(字符串)可能由存储提供程序设置，作为在读取状态时填充的Grain状态元数据的一部分。如果不使用Etags，一些提供者可能会选择将其保留为null。&nbsp;</p>
<p>从概念上讲，在任何写操作中，奥尔良运行时都将对grain状态数据对象进行深入的复制。在覆盖范围内，运行时可以使用优化规则和启发式来避免在某些情况下执行某些或全部的深度拷贝，前提是保留预期的逻辑隔离语义。</p>
<p>&nbsp;</p>
<p>8，Grain状态读取/写入操作的示例代码</p>
<p>Grain必须扩展Grain&lt; T &gt;类，以参与Orleans Grain状态的持久性机制。以上定义中的T将被一种特定于应用的Grain状态类所取代;看下面的例子。&nbsp;</p>
<p>grain类还应该用一个[StorageProvider]属性进行注释，该属性告诉运行时哪个存储提供者（实例）与这种类型的Grain一起使用。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyGrainState
{
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">int</span> Field1 { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
  </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> Field2 { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
}

[StorageProvider(ProviderName</span>=<span style="color: #800000;">"</span><span style="color: #800000;">store1</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> MyPersistenceGrain : Grain&lt;MyGrainState&gt;<span style="color: #000000;">, IMyPersistenceGrain
{
  ...
}</span></pre>
</div>
<p>&nbsp;</p>
<p>9，Grain状态读取</p>
<p>在Grain的OnActivateAsync()方法被调用之前，Grain状态的初始读取将由Orleans运行时自动发生;不需要应用程序代码来实现这一点，从那时起，Grain的状态将通过Grain&lt;T&gt;.State属性获取</p>
<p>&nbsp;</p>
<p>10，Grain状态写入</p>
<p>在对grain的内存状态进行任何适当的更改之后，grain应该调用base.WriteStateAsync()方法通过定义的存储提供程序将这些更改写入到持久存储中。 此方法是异步的，并返回一个通常由grain方法作为其自己的完成任务返回的Task。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> Task DoWrite(<span style="color: #0000ff;">int</span><span style="color: #000000;"> val)
{
  State.Field1 </span>=<span style="color: #000000;"> val;
  </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">base</span><span style="color: #000000;">.WriteStateAsync();
}</span></pre>
</div>
<p>&nbsp;</p>
<p>11，&nbsp;Grain状态刷新</p>
<p>如果Grain希望明确地从后备存储中重新读取这个Grain的最新状态，Grain应该调用base.ReadStateAsync()方法。这将从持久性存储中重新加载Grain状态，通过为这种Grain类型定义的存储提供程序，并且在ReadStateAsync()任务完成时，将覆盖任何先前的Grain状态的内存副本。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task&lt;<span style="color: #0000ff;">int</span>&gt;<span style="color: #000000;"> DoRead()
{
  </span><span style="color: #0000ff;">await</span> <span style="color: #0000ff;">base</span><span style="color: #000000;">.ReadStateAsync();
  </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> State.Field1;
}</span></pre>
</div>
<p>&nbsp;</p>
<p>12，Grain状态持久性操作的失败模式</p>
<p>①Grain状态读取操作的失败模式</p>
<p>存储提供者在初始读取该特定Grain的状态数据期间返回的故障将导致该Grain的激活操作失败；在这种情况下，将不会有任何的调用</p>
<p>OnActivateAsync()生命周期回调方法。对引起激活的Grain的原始请求将会被错误地反馈给调用者，就像在Grain激活过程中其他的故障一样。存储提供程序遇到的错误读取特定Grain的状态数据将导致ReadStateAsync()任务出错。就像Orleans的其他任务一样，Grain可以选择处理或忽略这一断层任务&nbsp;</p>
<p>任何试图发送一个消息到未能在筒仓中加载的Grain会抛Orleans.BadProviderConfigException错误。</p>
<p>②Grain状态写入操作的失败模式</p>
<p>存储提供程序遇到写入特定Grain的状态数据时遇到的故障将导致WriteStateAsync()任务出现故障。 通常情况下，如果WriteStateAsync()任务被正确链接到这个grain方法的最终返回Task中，这将意味着grain调用会返回给客户端调用者。 但是，某些高级方案可能会编写grain代码来专门处理这种写入错误，就像他们可以处理任何其他故障的Task一样。</p>
<p>执行错误处理/恢复代码的Grain必须捕获异常/故障的WriteStateAsync()任务，而不是重新抛出以表示他们已成功处理写入错误。</p>
<p>&nbsp;</p>
<p>13，存储提供商框架</p>
<p>有一个服务提供者API用于编写额外的持久性提供者 - IStorageProvider。</p>
<p>持久性提供程序API涵盖GrainState数据的读取和写入操作。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IStorageProvider
{
  Logger Log { </span><span style="color: #0000ff;">get</span><span style="color: #000000;">; }
  Task Init();
  Task Close();

  Task ReadStateAsync(</span><span style="color: #0000ff;">string</span><span style="color: #000000;"> grainType, GrainReference grainReference, IGrainState grainState);
  Task WriteStateAsync(</span><span style="color: #0000ff;">string</span><span style="color: #000000;"> grainType, GrainReference grainReference, IGrainState grainState);
}</span></pre>
</div>
<p>&nbsp;</p>
<p>14，存储提供程序语义</p>
<p>当存储提供程序检测到Etag约束违规时，任何尝试执行写入操作都应该导致写入任务出现瞬态错误Orleans.InconsistentStateException，并封装基础存储异常。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> InconsistentStateException : AggregateException
{
  </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span><span style="color: #008000;">Etag值当前持久存储。</span><span style="color: #808080;">&lt;/summary&gt;</span>
  <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> StoredEtag { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">private</span> <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
  </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span><span style="color: #008000;">Etag值目前保存在内存中，并试图更新。</span><span style="color: #808080;">&lt;/summary&gt;</span>
  <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> CurrentEtag { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">private</span> <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

  </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> InconsistentStateException(
    </span><span style="color: #0000ff;">string</span><span style="color: #000000;"> errorMsg,
    </span><span style="color: #0000ff;">string</span><span style="color: #000000;"> storedEtag,
    </span><span style="color: #0000ff;">string</span><span style="color: #000000;"> currentEtag,
    Exception storageException
    ) : </span><span style="color: #0000ff;">base</span><span style="color: #000000;">(errorMsg, storageException)
  {
    </span><span style="color: #0000ff;">this</span>.StoredEtag =<span style="color: #000000;"> storedEtag;
    </span><span style="color: #0000ff;">this</span>.CurrentEtag =<span style="color: #000000;"> currentEtag;
  }

  </span><span style="color: #0000ff;">public</span> InconsistentStateException(<span style="color: #0000ff;">string</span> storedEtag, <span style="color: #0000ff;">string</span><span style="color: #000000;"> currentEtag, Exception storageException)
    : </span><span style="color: #0000ff;">this</span><span style="color: #000000;">(storageException.Message, storedEtag, currentEtag, storageException)
  { }
}<br /></span></pre>
</div>
<p>来自写入操作的任何其他故障情况都应该导致写入任务被破坏，并且包含基础存储异常的异常。</p>
<p>&nbsp;</p>
<p>15，数据映射</p>
<p>单独的存储提供商应该决定如何最好地存储Grain状态blob（各种格式/序列化的形式）或列每场是明显的选择。</p>
<p>Azure Table的基本存储提供程序使用Orleans二进制序列化将状态数据字段编码为单个表列。</p>
<p>&nbsp;</p>
<p>16，ADO.NET持久性原理</p>
<p>ADO.NET支持的持久性存储的原则是：</p>
<ol>
<li>在数据，数据和代码格式不断发展的同时，保持业务关键型数据的安全。</li>
<li>利用供应商和存储特定的功能。</li>
</ol>
<p>实际上，这意味着坚持ADO.NET implementation goals，并在ADO.NET特定的存储提供程序中添加一些实现逻辑，允许演变存储中的数据形状。</p>
<p>除了通常的存储提供者功能外，ADO.NET提供者还具有内置的功能</p>
<ol>
<li>在往返状态时将存储数据格式从一种格式更改为另一种格式（例如，从JSON格式转换为二进制格式）。</li>
<li>以任意方式对存储的类型进行整形或从存储中读取。 这有助于演变版本状态。</li>
<li>将数据流出数据库。</li>
</ol>
<p>两个1和2。可用于任意选择参数，如Grain ID、Grain Type、payload data等。</p>
<p>发生这种情况以便人们选择一种格式，例如 简单的二进制编码（SBE）并实现IStorageDeserializer和IStorageSerializer。 内置的（de）序列化器是使用这种方法构建的。 OrleansStorageDefault（De）序列化程序可以用作如何实现其他格式的示例。</p>
<p>当（de）序列化器已经实现时，他们需要将ba添加到AdoNetStorageProvider的StorageSerializationPicker属性中。 这是IStorageSerializationPicker的一个实现。 默认情况下将使用StorageSerializationPicker。 在RelationalStorageTests中可以看到更改数据存储格式或使用（de）序列化器的示例。</p>
<p>目前没有任何方法可以将这个信息暴露给Orleans应用程序，因为没有方法可以访问创建的AdoNetStorageProvider实例的框架。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff; font-size: 18pt;"><strong><a name="a2"></a>二、定时器和提醒</strong></span></p>
<p>Orleans运行时提供了两种称为定时器和提醒的机制，使开发人员能够指定谷物的周期性行为。</p>
<p>1，定时器</p>
<p>①描述</p>
<p>定时器用于创建不需要跨越多个激活（Grain实例化）的周期性Grain行为。 它与标准的.NET System.Threading.Timer类基本相同。 另外，它在运行的Grain激活内受单线程执行保证。</p>
<p>每个激活可能有零个或多个与之关联的定时器。 运行时在与其关联的激活的运行时上下文中执行每个定时器例程。</p>
<p>②用法<br />要启动计时器，请使用Grain.RegisterTimer方法，该方法返回一个IDisposable引用：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">protected</span> IDisposable RegisterTimer(Func&lt;<span style="color: #0000ff;">object</span>, Task&gt; asyncCallback, <span style="color: #0000ff;">object</span> state, TimeSpan dueTime, TimeSpan period)</pre>
</div>
<ul>
<li>asyncCallback是当计时器计时时调用的函数。</li>
<li>state是一个对象，当计时器计时时，它将被传递给asyncCallback。</li>
<li>dueTime指定在发出第一个计时器之前等待的时间量。</li>
<li>
<p>period&nbsp;指定计时器的周期。<br />取消定时器。<br />如果激活被停用或发生故障或发生故障，计时器将停止触发。<br />重要的注意事项</p>



















</li>
<li>
<p>启用激活集合时，计时器回调的执行不会将激活状态从空闲状态更改为使用。这意味着计时器不能用于延迟其他空闲激活的停用。</p>



















</li>
<li>传递给Grain.RegisterTimer的时间是，从asyncCallback返回的任务到下一次调用asyncCallback时所经过的时间。这不仅使连续调用asyncCallback无法重叠，还使得异步回调的时间长度影响到异步调用的频率。这与system.thread.timer的语义有很大的偏差。</li>
<li>每次调用asyncCallback都会在一个单独的回合中传递给一个激活，并且永远不会与其他回合在同一个激活中同时运行。 但是，请注意，asyncCallback调用不作为消息传递，因此不受消息交错语义限制。 这意味着asyncCallback的调用应该被认为是像对其他消息运行在一个可重入的Grain上一样。</li>



















</ul>
<p>2，提醒</p>
<p>①描述</p>
<p>提醒与定时器类似，但有一些重要的区别：</p>
<ul>
<li>除非明确取消，否则提醒将保持不变，并会在所有情况下继续触发（包括部分或全部群集重新启动）。</li>
<li>提醒与Grain有关，而不是任何特定的激活。</li>
<li>如果Grain有没有与之相关的激活和提醒蜱，一个将被创建。例如：如果激活变为空闲并且被停用，则与相同Grain相关联的提醒将在接下来ticks时重新激活Grain。</li>
<li>提醒是通过消息传递的，并且与所有其他的grain方法一样，都受到相同的交错语义的影响。</li>
<li>提醒不应该用于高频计时器&mdash;&mdash;它们的周期应该以分钟、小时或天数来衡量。</li>


















</ul>
<p>②配置</p>
<p>提醒，持久，依赖存储功能。在提醒子系统将运行之前，您必须指定使用哪种存储支持。提醒功能由服务器端配置中的SystemStore元素控制。它使用Azure表或SQL Server作为存储。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">SystemStore </span><span style="color: #ff0000;">SystemStoreType</span><span style="color: #0000ff;">="AzureTable"</span> <span style="color: #0000ff;">/&gt;</span><span style="color: #000000;"> OR
</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">SystemStore </span><span style="color: #ff0000;">SystemStoreType</span><span style="color: #0000ff;">="SqlServer"</span> <span style="color: #0000ff;">/&gt;</span></pre>
</div>
<p>&nbsp;如果您只是想要一个占位符实现的提醒，而不需要设置一个Azure帐户或SQL数据库，然后将这个元素添加到配置文件（在&ldquo;Globals&rdquo;下）将会给你一个提醒系统的开发实现：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ReminderService </span><span style="color: #ff0000;">ReminderServiceType</span><span style="color: #0000ff;">="ReminderTableGrain"</span><span style="color: #0000ff;">/&gt;</span></pre>
</div>
<p>③使用</p>
<p>使用提醒Grain必须实现IRemindable.RecieveReminder方法。</p>
<div class="cnblogs_code">
<pre>Task IRemindable.ReceiveReminder(<span style="color: #0000ff;">string</span><span style="color: #000000;"> reminderName, TickStatus status)
{
    Console.WriteLine(</span><span style="color: #800000;">"</span><span style="color: #800000;">感谢提醒我 - 我差点忘了！</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> TaskDone.Done;
}</span></pre>
</div>
<p>要开始提醒，请使用Grain.RegisterOrUpdateReminder方法，该方法返回一个IOrleansReminder对象：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">protected</span> Task&lt;IOrleansReminder&gt; RegisterOrUpdateReminder(<span style="color: #0000ff;">string</span> reminderName, TimeSpan dueTime, TimeSpan period)</pre>
</div>
<ul>
<li>reminderName是一个字符串，必须在上下文的范围内唯一标识提醒。</li>
<li>dueTime指定在发出第一个计时器tick之前等待的时间量。</li>
<li>period指定定时器的周期。</li>
</ul>
<p>由于提醒在任何一次激活的生命周期中都能够存活，因此必须明确取消（而不是被处置）。 您可以通过调用Grain.UnregisterReminder来取消提醒：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">protected</span> Task UnregisterReminder(IOrleansReminder reminder)</pre>
</div>
<p>提醒是由Grain.RegisterOrUpdateReminder返回的处理对象。</p>
<p>IOrleansReminder的实例不能保证超过激活的有效期。 如果您希望以某种方式识别提醒，请使用包含提醒名称的字符串。</p>
<p>如果您只有提醒的名称并需要IOrleansReminder的相应实例，请调用Grain.GetReminder方法：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">protected</span> Task&lt;IOrleansReminder&gt; GetReminder(<span style="color: #0000ff;">string</span> reminderName)</pre>
</div>
<p>&nbsp;</p>
<p>3，我应该使用哪个？</p>
<p>我们建议您在以下情况下使用计时器：</p>
<ul>
<li>如果激活被停用或发生故障，则定时器停止工作并不重要（或不期望）。</li>
<li>如果计时器的频率很小(例如几秒钟或几分钟)</li>
<li>定时器回调可以从Grain.OnActivateAsync启动，或者在调用grain方法时启动。</li>
</ul>
<p>我们建议您在以下情况下使用提醒：</p>
<ul>
<li>当周期性行为需要经受激活和任何失败。</li>
<li>执行不频繁的任务（例如在几分钟，几小时或几天内合理表达）。</li>
</ul>
<p>结合计时器和提醒您可以考虑使用提醒和定时器的组合来实现您的目标。 例如，如果您需要一个需要在激活状态下保留的小频率的计时器，则可以使用每5分钟运行一次的提醒，其目的是唤醒一个可重新启动本地计时器的计时器，该计时器可能由于 停用。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a3"></a>三、依赖注入</span></strong></p>
<p>1，什么是依赖注入</p>
<p>依赖注入（DI）是一种软件设计模式，它实现了解决依赖关系的控制反转。</p>
<p>Orleans正在使用由ASP.NET Core开发人员编写的抽象概念。</p>
<p>2，Orleans中的DI</p>
<p>目前仅在Orleans的服务器端支持依赖注入。</p>
<p>Orleans可以将依赖关系注入到Grains应用程序中。</p>
<p>然而Orleans支持每个容器依赖的注入机制，其中最常用的方法是构造器注入。</p>
<p>理论上，任何类型都可以在Silo启动期间注册在IServiceCollection中。</p>
<p>注：由于新Orleans是不断发展的，因为目前的计划，将有可能利用其他应用类的依赖注入，以及像StreamProviders。</p>
<p>3，配置DI</p>
<p>DI配置是一个全局配置值，必须在此配置。</p>
<p>Orleans使用与ASP.NET Core类似的方法来配置DI。 您的应用程序中必须包含一个启动类，其中必须包含ConfigureServices方法。 它必须返回一个类型为IServiceProvider的对象实例。</p>
<p>通过下面介绍的方法之一来指定启动类的类型来完成配置。</p>
<p>注意：以前的DI配置是在集群节点级别指定的，在最近的版本中进行了更改。</p>
<p>4，从代码配置<br />可以通过基于代码的配置告诉Orleans您喜欢使用什么Startup类型。。 在ClusterConfiguration类中有一个名为UseStartup的扩展方法，您可以使用它进行此操作。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> configuration = <span style="color: #0000ff;">new</span><span style="color: #000000;"> ClusterConfiguration();
configuration.UseStartupType</span>&lt;MyApplication.Configuration.MyStartup&gt;();</pre>
</div>
<p>5，通过XML配置<br />要使用Orleans注册Startup类，必须将Startup元素添加到Defaults部分，并在Type属性中指定该类型的程序集限定名称。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;?</span><span style="color: #ff00ff;">xml version="1.0" encoding="utf-8" </span><span style="color: #0000ff;">?&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">tns:OrleansConfiguration </span><span style="color: #ff0000;">xmlns:tns</span><span style="color: #0000ff;">="urn:orleans"</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">tns:Defaults</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">tns:Startup </span><span style="color: #ff0000;">Type</span><span style="color: #0000ff;">="MyApplication.Configuration.Startup,MyApplication"</span> <span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">tns:Defaults</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">tns:OrleansConfiguration</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>6，例子<br />这是一个完整的Startup类示例：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> MyApplication.Configuration
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyStartup
    {
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> IServiceProvider ConfigureServices(IServiceCollection services)
        {
            services.AddSingleton</span>&lt;IInjectedService, InjectedService&gt;<span style="color: #000000;">();

            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> services.BuildServiceProvider();
        }
    }
}</span></pre>
</div>
<p>这个例子显示了Grain如何通过构造函数注入来利用IInjectedService，以及注入服务的完整声明和实现：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> ISimpleDIGrain : IGrainWithIntegerKey
{
    Task</span>&lt;<span style="color: #0000ff;">long</span>&gt;<span style="color: #000000;"> GetTicksFromService();
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SimpleDIGrain : Grain, ISimpleDIGrain
{
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> IInjectedService injectedService;

    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> SimpleDIGrain(IInjectedService injectedService)
    {
        </span><span style="color: #0000ff;">this</span>.injectedService =<span style="color: #000000;"> injectedService;
    }

    </span><span style="color: #0000ff;">public</span> Task&lt;<span style="color: #0000ff;">long</span>&gt;<span style="color: #000000;"> GetTicksFromService()
    {
        </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> injectedService.GetTicks();
    }
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IInjectedService
{
    Task</span>&lt;<span style="color: #0000ff;">long</span>&gt;<span style="color: #000000;"> GetTicks();
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> InjectedService : IInjectedService
{
    </span><span style="color: #0000ff;">public</span> Task&lt;<span style="color: #0000ff;">long</span>&gt;<span style="color: #000000;"> GetTicks()
    {
        </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> Task.FromResult(DateTime.UtcNow.Ticks);
    }
}</span></pre>
</div>
<p>7，测试框架集成<br />与真正的测试框架结合在一起验证代码的正确性。&nbsp;</p>
<p>你需要做两件事，设置DI和测试。首先，您需要实现服务的模拟。这是在我们的例子中使用Moq来完成的，Moq是.net的一个流行的mocking框架。这里有一个对服务进行mocking的例子。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MockServices
{
    </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> IServiceProvider ConfigureServices(IServiceCollection services)
    {
        </span><span style="color: #0000ff;">var</span> mockInjectedService = <span style="color: #0000ff;">new</span> Mock&lt;IInjectedService&gt;<span style="color: #000000;">();

        mockInjectedService.Setup(t </span>=&gt;<span style="color: #000000;"> t.GetTicks()).Returns(knownDateTime);
        services.AddSingleton</span>&lt;IInjectedService&gt;<span style="color: #000000;">(mockInjectedService.Object);
        </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> services.BuildServiceProvider();
    }
}</span></pre>
</div>
<p>要将这些服务包含在您的测试仓库中，您需要指定MockServices作为仓储启动类。 这是做这个的一个例子。</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">[TestClass]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> IInjectedServiceTests: TestingSiloHost
{
    </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> TestingSiloHost host;

    [TestInitialize]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Setup()
    {
        </span><span style="color: #0000ff;">if</span> (host == <span style="color: #0000ff;">null</span><span style="color: #000000;">)
        {
            host </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> TestingSiloHost(
                </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> TestingSiloOptions
                {
                    StartSecondary </span>= <span style="color: #0000ff;">false</span><span style="color: #000000;">,
                    AdjustConfig </span>= clusterConfig =&gt;<span style="color: #000000;">
                    {
                        clusterConfig.UseStartupType</span>&lt;MockServices&gt;<span style="color: #000000;">();
                    }
                });
        }
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a4"></a>四、观察者</span></strong></p>
<p>有些情况下，简单的消息/响应模式不够，客户端需要接收异步通知。 例如，用户可能希望在朋友发布新的即时消息时得到通知。&nbsp;</p>
<p>客户端观察者是一种允许异步通知客户端的机制。 观察者是从IGrainObserver继承的单向异步接口，它的所有方法必须是无效的。 Grain通过调用Grain接口方法来发送通知给观察者，除了它没有返回值，Grain不需要依赖结果。 Orleans运行时将确保通知的单向传递。 发布此类通知的Grain应提供API以添加或删除观察者。 另外，公开允许取消现有订阅的方法通常是方便的。 Grain开发人员可以使用 Orleans ObserverSubscriptionManager &lt;T&gt;泛型类来简化观察到的Grain类型的开发。</p>
<p>要订阅通知，客户端必须首先创建一个实现观察者接口的本地C＃对象。 然后调用观察者工厂的一个静态方法CreateObjectReference()，将C＃对象变成一个Grain引用，然后可以将它传递给通知Grain上的订阅方法。</p>
<p>其他Grain也可以使用此模型来接收异步通知。 与客户端订阅的情况不同，订阅的grain只是将观察者接口作为一个方面来实现，并传入一个对自身的引用（例如this.AsReference &lt;IMyGrainObserverInterface&gt;）。</p>
<p>1，代码示例<br />我们假设我们有一个周期性地向客户发送消息的Grain。 为了简单起见，我们示例中的消息将是一个字符串。 我们首先定义将接收消息的客户端上的接口。</p>
<p>界面将如下所示：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span><span style="color: #000000;"> IChat : IGrainObserver
{
    </span><span style="color: #0000ff;">void</span> ReceiveMessage(<span style="color: #0000ff;">string</span><span style="color: #000000;"> message);
}</span></pre>
</div>
<p>唯一特别的是，该接口应该从IGrainObserver继承。 现在任何想要观察这些消息的客户端都应该实现一个实现IChat的类。</p>
<p>最简单的情况是这样的：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Chat : IChat
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> ReceiveMessage(<span style="color: #0000ff;">string</span><span style="color: #000000;"> message)
    {
        Console.WriteLine(message);
    }
}</span></pre>
</div>
<p>现在在服务器上，我们应该有一个Grain发送这些聊天消息到客户端。 Grain也应该有一个机制，客户订阅和退订自己接收通知。 对于订阅，Grain可以使用实用工具类ObserverSubscriptionManager：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">class</span><span style="color: #000000;"> HelloGrain : Grain, IHello
{
    </span><span style="color: #0000ff;">private</span> ObserverSubscriptionManager&lt;IChat&gt;<span style="color: #000000;"> _subsManager;

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">async</span><span style="color: #000000;"> Task OnActivateAsync()
    {
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 我们在激活时创建了这个工具。</span>
        _subsManager = <span style="color: #0000ff;">new</span> ObserverSubscriptionManager&lt;IChat&gt;<span style="color: #000000;">();
        </span><span style="color: #0000ff;">await</span> <span style="color: #0000ff;">base</span><span style="color: #000000;">.OnActivateAsync();
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">客户端调用此订阅</span>
    <span style="color: #0000ff;">public</span><span style="color: #000000;"> Task Subscribe(IChat observer)
    {
        _subsManager.Subscribe(observer);
        </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> TaskDone.Done;
    }

    </span><span style="color: #008000;">//</span><span style="color: #008000;">此外，客户端使用这个取消订阅自己不再接收消息。</span>
    <span style="color: #0000ff;">public</span><span style="color: #000000;"> Task UnSubscribe(IChat observer)
    {
        _subsManager.Unsubscribe(observer);
        </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> TaskDone.Done;
    }
}</span></pre>
</div>
<p>要将消息发送到客户端，可以使用ObserverSubscriptionManager &lt;IChat&gt;实例的通知方法。 该方法采用Action &lt;T&gt;方法或lambda表达式（其中T是IChat类型）。 您可以调用接口上的任何方法将其发送给客户端。 在我们的例子中，我们只有一个方法ReceiveMessage，我们在服务器上的发送代码如下所示：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> Task SendUpdateMessage(<span style="color: #0000ff;">string</span><span style="color: #000000;"> message)
{
    _subsManager.Notify(s </span>=&gt;<span style="color: #000000;"> s.ReceiveMessage(message));
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> TaskDone.Done;
}</span></pre>
</div>
<p>现在我们的服务器有一个向观察者客户端发送消息的方法，订阅/取消订阅的方法有两种，客户端实现了一个类来观察这些消息。 最后一步是使用我们以前实现的Chat类在客户端上创建一个观察者引用，并在订阅它之后让它接收消息。</p>
<p>代码看起来像这样：</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">首先创建Grain引用</span>
<span style="color: #0000ff;">var</span> friend = GrainClient.GrainFactory.GetGrain&lt;IHello&gt;(<span style="color: #800080;">0</span><span style="color: #000000;">);
Chat c </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> Chat();

</span><span style="color: #008000;">//</span><span style="color: #008000;">创建可用于订阅observable grain的引用。</span>
<span style="color: #0000ff;">var</span> obj = <span style="color: #0000ff;">await</span> GrainClient.GrainFactory.CreateObjectReference&lt;IChat&gt;<span style="color: #000000;">(c);
</span><span style="color: #008000;">//</span><span style="color: #008000;">订阅该实例以接收消息。</span>
<span style="color: #0000ff;">await</span> friend.Subscribe(obj);</pre>
</div>
<p>现在，当服务器上的Grain调用SendUpdateMessage方法时，所有订阅的客户端都将收到消息。 在我们的客户端代码中，变量c中的Chat实例将接收消息并将其输出到控制台。</p>
<p>注意：传递给CreateObjectReference的对象通过WeakReference &lt;T&gt;被保存，因此如果不存在其他引用，将被垃圾回收。 用户应该为每个观察者保留一个他们不想被收集的参考。</p>
<p>注意：观察者本质上是不可靠的，因为您没有得到任何回应，知道是否由于分布式系统中可能出现的任何情况而收到并处理了消息或者仅仅是失败了。 因为你的观察者应该定期轮询Grain，或者使用其他机制来确保他们收到了他们应该收到的所有信息。在某些情况下，你可以损失一些信息，你不需要任何额外的机制，但是如果你需要确保所有的观察者都接收到这些信息并且接收所有的信息，定期的重新订阅和轮询观察Grain，可以帮助确保最终处理所有消息。</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a5"></a>五、无状态工作者Grains</span></strong></p>
<p>默认情况下，Orleans运行时只会在集群内创建一个Grain的激活。 这是虚拟主角模型的最直观的表达方式，每个Grain对应于具有唯一类型/标识的实体。 但是，也有一些情况是应用程序需要执行功能无状态的操作，而这些操作不会绑定到系统中的特定实体。 例如，如果客户端发送带有压缩有效载荷的请求，并在它们能够被路由到目标Grain进行处理之前需要被解压缩，则这样的解压缩/路由逻辑不绑定到应用中的特定实体，并且可以容易地向外扩展。&nbsp;</p>
<p>当[StatelessWorker]特性应用于Grain类时，它向Orleans运行时指示该类的Grain应被视为无状态工作者Grain。 无状态工作者Grain具有以下特性，使其执行与普通Grain类别的执行有很大不同。</p>
<ol>
<li>Orleans运行时可以并且将在集群的不同仓储上创建无状态工作者Grain的多个激活。</li>
<li>对无状态工作者Grain的请求总是在当地执行，也就是在请求发起的同一个仓储里，要么由Grain运行，要么由仓储的客户端网关接收。 因此，从其他Grain或客户网关调用无状态工作者Grain从不会产生远程信息。</li>
<li>Orleans运行时自动创建一个无状态工作者Grain额外的激活，如果现有的忙。 除非可选的maxLocalWorkers参数明确指定，否则运行时创建的无状态工作器的最大激活次数默认受机器上CPU内核数量的限制。</li>
<li>由于2和3，无状态工作者Grain激活并不是单个可寻址的。对无状态工作者Grain的两个后续请求可以通过不同的激活来处理。</li>
</ol>
<p>无状态工作者Grain提供了一个直接的方式，创建一个自动管理的Grain激活池，根据实际负载自动扩展和缩减。运行时总是以相同的顺序扫描可用的无状态工作者Grain激活。因此，它总是将请求发送到它可以找到的第一个空闲本地激活，并且如果以前的所有激活都忙，则只能到最后一个激活。如果所有的激活都很忙，并且没有达到激活限制，它会在列表的末尾再创建一个激活，并将请求发送给它。这意味着，当对无状态工作者Grain需求量增加，而且现有的激活当前都很忙时，运行时将其激活池扩大到极限。相反，当负载下降，并且可以通过少量无状态工作者Grain的激活来处理时，在列表尾部的激活将不会被发送到他们的请求。他们将变得闲置，并最终被标准的激活收集过程停用。因此，激活池将最终缩小以匹配负载。</p>
<p>以下示例使用默认的最大激活数限制定义无状态工作者谷物类MyStatelessWorkerGrain。</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">[StatelessWorker]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyStatelessWorkerGrain : Grain, IMyStatelessWorkerGrain
{
 ...
}</span></pre>
</div>
<p>调用无状态工作者Grain和其他Grain一样。 唯一的区别是，在大多数情况下，使用一个单一的GrainID，0或Guid.Empty。 具有多个无状态工作者Grain池时，可以使用多个GrainID，每个ID需要一个Grain池。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> worker = GrainFactory.GetGrain&lt;IMyStatelessWorkerGrain&gt;(<span style="color: #800080;">0</span><span style="color: #000000;">);
</span><span style="color: #0000ff;">await</span> worker.Process(args);</pre>
</div>
<p>这个定义了一个无状态的工作者Grain类每个仓储不超过一个Grain激活。</p>
<div class="cnblogs_code">
<pre>[StatelessWorker(<span style="color: #800080;">1</span>)] <span style="color: #008000;">//</span><span style="color: #008000;"> max 1 activation per silo</span>
<span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyLonelyWorkerGrain : ILonelyWorkerGrain
{
 ...
}</span></pre>
</div>
<p>请注意，[StatelessWorker]属性不会改变目标Grain类的重入性。 就像任何其他Grain一样，无状态工作者Grain默认情况下是不可重入的。 可以通过向Grain类添加一个[Reentrant]属性来明确地重新定位它们。</p>
<p><span style="font-size: 12px; color: #ff0000;">可重入(reentrant)函数可以由多于一个任务并发使用,而不必担心数据错误。相反,不可重入(non-reentrant)函数不能由超过一个任务所共享</span></p>
<p>1，State</p>
<p>&ldquo;Stateless&rdquo;部分的&ldquo;Stateless Worker&rdquo;部分并不意味着无状态的工作者不能拥有状态，并且仅限于执行功能操作。和其他Grain一样，无状态的工人Grain可以装载并保存它需要的任何状态。这只是因为在同一个和不同的集群上创建了一个无状态的工作者Grain的多个激活，没有简单的机制来协调不同激活状态所持有的状态。</p>
<p>涉及Stateless Worker&nbsp;有几种有用的模式。</p>
<p>①向外扩展热缓存项<br />对于经历高吞吐量的热缓存项目，将每个这样的项目保持在无状态工作者Grain中使得a）在仓储中并在群集中的所有仓储中自动扩展; b）通过客户端网关在收到客户端请求的仓储上使数据始终本地可用，这样就可以在不需要额外网络跳转到另一个仓储的情况下应答请求。</p>
<p>②减少样式聚合</p>
<p>在某些场景中，应用程序需要计算集群中特定类型的所有Grains的特定指标， 并定期报告聚集体。 举例来说，每个游戏地图的玩家数量，VoIP呼叫的平均持续时间， 等等，如果成千上万的Grain中的每一个都将它们的指标报告给一个单一的全局聚合器，那么聚合器就会立即过载，无法处理大量的报告。另一种方法是将此任务转换成一个2(或更多)步骤，减少样式聚合。第一层的聚合是通过向无状态的工作者预聚集的Gtrain发送他们的指标。Orleans运行时将自动为每个仓储创建无状态工作者Grain的多个激活。由于所有这些调用都将在本地处理，不需要远程调用或序列化消息，因此此类聚合的成本将显著低于远程情况。现在，每个预聚集无状态的工作者Grain激活，独立地或与其他本地激活进行协调，可以在不超载的情况下将聚合报告发送到全局最终聚合器(或在必要时再进行另一个还原层)。</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a6"></a>六、流</span></strong></p>
<p><strong>1，介绍</strong></p>
<p>1）Orleans Streams<br />Orleansv.1.0.0增加了对编程模型的流式扩展的支持。 流式扩展提供了一系列抽象和API，使工作流更简单、更健壮。 流式扩展允许开发人员编写响应式应用程序，以结构化的方式对一系列事件进行操作。 流提供程序的可扩展性模型使得编程模型与大量现有排队技术（如<a href="http://azure.microsoft.com/en-us/services/event-hubs/">Event Hubs</a>,&nbsp;<a href="http://azure.microsoft.com/en-us/services/service-bus/">ServiceBus</a>,&nbsp;<a href="http://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-how-to-use-queues/">Azure Queues</a>和<a href="http://kafka.apache.org/">Apache Kafka</a>.）兼容并可移植。 不需要编写特殊的代码或运行专门的进程来与这样的队列进行交互。</p>
<p>2）我为什么要关心？</p>
<p>如果你已经知道了&nbsp;<a href="http://blog.confluent.io/2015/01/29/making-sense-of-stream-processing/">Stream Processing</a>&nbsp;和熟悉各种技术&nbsp;<a href="http://azure.microsoft.com/en-us/services/event-hubs/">Event Hubs</a>,&nbsp;<a href="http://kafka.apache.org/">Kafka</a>,&nbsp;<a href="http://azure.microsoft.com/en-us/services/stream-analytics/">Azure Stream Analytics</a>,&nbsp;<a href="https://storm.apache.org/">Apache Storm</a>,&nbsp;<a href="https://spark.apache.org/streaming/">Apache Spark Streaming</a>, 和<a href="https://msdn.microsoft.com/en-us/data/gg577609.aspx">Reactive Extensions (Rx) in .NET</a>, 你可能会问，你为什么要关心这个。为什么我们需要另一个流处理系统，以及Actors如何与流相关?&nbsp;<a href="https://dotnet.github.io/orleans/Documentation/Orleans-Streams/Streams-Why.html">"Why Orleans Streams?"</a>&nbsp;是用来回答这个问题的。</p>
<p>3）编程模型<br />Orleans流编程模型背后有许多原理。</p>
<ol>
<li>遵循Orleans的虚拟Actors，Orleans流是虚拟的。也就是说,流总是存在。它没有被显式地创建或销毁，它永远不会失败。</li>
<li>流是由流id识别的，它们只是由GUIDs和字符串组成的逻辑名称。</li>
<li>Orleans Streams允许从时间和空间的处理中分离数据的生成。 这意味着，流生产者和流消费者可能在不同的服务器上，在不同的时间，并会承受失败。</li>
<li>Orleans流是轻量级和动态的。 Orleans Streaming Runtime旨在处理大量来来往往的高速流。</li>
<li>Orleans流绑定是动态的。 Orleans Streaming Runtime旨在处理grain以高速连接和断开流的情况。</li>
<li>Orleans Streaming Runtime透明地管理流消耗的生命周期。 应用程序订阅一个流之后，即使在出现故障的情况下，它也会收到流的事件。</li>
<li>Orleans流在grain和Orleans的客户中工作一致。</li>











</ol>
<p>4）编程API</p>
<p>应用程序通过与.NET中众所周知的Reactive Extensions（Rx）非常相似的API与流进行交互，通过使用Orleans.Streams.IAsyncStream &lt;T&gt;实现<br />Orleans.Streams.IAsyncObserver &lt;T&gt;和Orleans.Streams.IAsyncObservable &lt;T&gt;接口。</p>
<p>在下面的典型示例中，设备会生成一些数据，这些数据会作为HTTP请求发送到云中运行的服务。 在前端服务器上运行的Orleans客户端接收到这个HTTP调用并将数据发布到匹配的设备流中：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span><span style="color: #000000;"> Task OnHttpCall(DeviceEvent deviceEvent)
{
     </span><span style="color: #008000;">//</span><span style="color: #008000;"> 将数据直接发布到设备的流中。</span>
     IStreamProvider streamProvider = GrainClient.GetStreamProvider(<span style="color: #800000;">"</span><span style="color: #800000;">myStreamProvider</span><span style="color: #800000;">"</span><span style="color: #000000;">);
     IAsyncStream</span>&lt;DeviceEventData&gt; deviceStream = streamProvider.GetStream&lt;DeviceEventData&gt;<span style="color: #000000;">(deviceEvent.DeviceId);
     </span><span style="color: #0000ff;">await</span><span style="color: #000000;"> deviceStream.OnNextAsync(deviceEvent.Data);
}</span></pre>
</div>
<p>在下面的另一个例子中，聊天用户（实现为Orleans Grain）加入聊天室，获取由该房间中所有其他用户生成的聊天消息流，并订阅该消息。 请注意，聊天用户既不需要知道聊天室Grain本身（我们的系统中可能没有这样的Grain），也不需要知道该群中产生消息的其他用户。 不用说，为了产生聊天流，用户不需要知道谁当前订阅了流。 这说明聊天用户如何在时间和空间上完全分离。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ChatUser: Grain
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task JoinChat(<span style="color: #0000ff;">string</span><span style="color: #000000;"> chatGroupName)
    {
       IStreamProvider streamProvider </span>= <span style="color: #0000ff;">base</span>.GetStreamProvider(<span style="color: #800000;">"</span><span style="color: #800000;">myStreamProvider</span><span style="color: #800000;">"</span><span style="color: #000000;">);
       IAsyncStream</span>&lt;<span style="color: #0000ff;">string</span>&gt; chatStream = streamProvider.GetStream&lt;<span style="color: #0000ff;">string</span>&gt;<span style="color: #000000;">(chatGroupName);
       </span><span style="color: #0000ff;">await</span> chatStream.SubscribeAsync((<span style="color: #0000ff;">string</span> chatEvent) =&gt;<span style="color: #000000;"> Console.Out.Write(chatEvent));
    }
}</span></pre>
</div>
<p>5）快速启动示例</p>
<p>快速入门示例是在应用程序中使用流的总体工作流程的快速概览。 阅读之后，您应该阅读Streams Programming API，以深入了解这些概念。</p>
<p>6）流编程API<br />流编程API提供了编程API的详细描述。</p>
<p>7）流提供者<br />流可以通过各种形状和形式的物理通道来实现，并且可以具有不同的语义。 Orleans Streaming旨在通过流提供程序的概念来支持这种多样性，这是系统中的一个可扩展点。 Orleans目前有两个流提供程序的实现：基于TCP的简单消息流提供程序和基于Azure队列的Azure队列流提供程序。 有关Steam提供商的更多详细信息可以在Stream Providers上找到。</p>
<p>8）流语义<br />流Subsription语义：Orleans流保证Stream Subsription操作的顺序一致性。 具体说就是，当消费者订阅一个流时，一旦代表该subsription操作的Task被成功解决，消费者就会看到订阅之后生成的所有事件。 另外，可重放的流允许通过使用StreamSequenceToken从任意时间点订阅。</p>
<p>单个流事件传送保证：单个事件传送保证取决于各个流提供者。 一些服务器只提供一次交付（例如简单消息流），而另一些则至少提供一次交付（例如Azure队列流）。 甚至有可能建立一个能够保证一次交付的流提供者（我们还没有这样的提供者，但是可以用可扩展性模型来构建一个提供者）。</p>
<p>事件传递顺序：事件顺序还取决于特定的流提供者。 在SMS流中，制作者通过控制发布它们的方式来控制消费者看到的事件的顺序。 Azure队列流不保证FIFO顺序，因为下层的Azure队列不能保证顺序失败。 应用程序还可以通过使用StreamSequenceToken来控制自己的流传送顺序。&nbsp;</p>
<p>10）流实现<br />Orleans Streams Implementation提供了内部实现的高层次概述。&nbsp;</p>
<p>11）流扩展性<br />Orleans Streams Extensibility介绍了如何使用新功能扩展流。</p>
<p>12）代码示例<br />在这里可以找到更多关于如何在谷物中使用流API的例子。 我们计划在未来创造更多样本。</p>
<p>&nbsp;</p>
<p><strong>2，流，快速启动</strong></p>
<p>本指南将向您展示安装和使用Orleans Streams的快速方法。 要详细了解流式传输功能的详细信息，请阅读本文档的其他部分。</p>
<p>1）所需的配置<br />在本指南中，我们将使用基于简单消息的流，它使用谷物消息向订户发送流数据。 我们将使用内存存储提供商存储的订阅列表，所以它不是真正的生产应用明智的最佳的选择。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Globals</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">StorageProviders</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Provider </span><span style="color: #ff0000;">Type</span><span style="color: #0000ff;">="Orleans.Storage.MemoryStorage"</span><span style="color: #ff0000;"> Name</span><span style="color: #0000ff;">="Default"</span> <span style="color: #0000ff;">/&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Provider </span><span style="color: #ff0000;">Type</span><span style="color: #0000ff;">="Orleans.Storage.MemoryStorage"</span><span style="color: #ff0000;"> Name</span><span style="color: #0000ff;">="PubSubStore"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">StorageProviders</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">StreamProviders</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Provider </span><span style="color: #ff0000;">Type</span><span style="color: #0000ff;">="Orleans.Providers.Streams.SimpleMessageStream.SimpleMessageStreamProvider"</span><span style="color: #ff0000;"> Name</span><span style="color: #0000ff;">="SMSProvider"</span><span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">StreamProviders</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>现在我们可以创建流，使用它们作为生产者发送数据，也可以作为订户接收数据。</p>
<p>2）生产事件<br />为流生成事件相对容易。 您应该首先访问您在上面的配置（SMSProvider）中定义的流提供程序，然后选择一个流并将数据推送到它。</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">//选择一个聊天室grain和聊天室流guid
var guid = some guid identifying the chat room
//获取我们在配置中定义的提供者之一
var streamProvider = GetStreamProvider("SMSProvider");
//获取流的引用
var stream = streamProvider.GetStream</span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">int</span><span style="color: #0000ff;">&gt;</span>(guid, "RANDOMDATA");</pre>
</div>
<p>正如你可以看到我们的流有一个GUID和一个命名空间。 这将使识别独特的流变得容易。 例如，在聊天室命名空间中，&ldquo;Rooms&rdquo;和GUID可以是拥有RoomGrain的GUID。</p>
<p>这里我们使用一些已知的聊天室的GUID。 现在使用流的OnNext方法，我们可以将数据推送到它。 让我们在一个计时器内使用随机数字。 您也可以使用任何其他数据类型的流。</p>
<div class="cnblogs_code">
<pre>RegisterTimer(s =&gt;<span style="color: #000000;">
        {
            </span><span style="color: #0000ff;">return</span> stream.OnNextAsync(<span style="color: #0000ff;">new</span><span style="color: #000000;"> System.Random().Next());
        }, </span><span style="color: #0000ff;">null</span>, TimeSpan.FromMilliseconds(<span style="color: #800080;">1000</span>), TimeSpan.FromMilliseconds(<span style="color: #800080;">1000</span>));</pre>
</div>
<p>3）订阅和接收流数据<br />为了接收数据，我们可以使用隐式/显式订阅，在手册的其他页面中对这些订阅进行了全面描述。 在这里，我们使用的是更容易隐士订阅。 当grain类型想要隐式地订阅一个流时，它使用ImplicitStreamSubscription (namespace)]。</p>
<p>对于我们的情况，我们将像这样定义一个ReceiverGrain：</p>
<div class="cnblogs_code">
<pre>[ImplicitStreamSubscription(<span style="color: #800000;">"</span><span style="color: #800000;">RANDOMDATA</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> ReceiverGrain : Grain, IRandomReceiver</pre>
</div>
<p>现在，无论何时将某些数据推送到名称空间RANDOMDATA的流中（如定时器中所示），具有相同流的GUID的ReceiverGrain类型的Grain将收到该消息。 即使目前不存在Grain的激活，运行时也会自动创建一个新消息并将消息发送给它。</p>
<p>为了使这个工作，我们需要通过设置我们的OnNext方法接收数据来完成订阅过程。 所以我们的ReceiverGrain应该调用OnActivateAsync这样的东西</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">Create a GUID based on our GUID as a grain</span>
<span style="color: #0000ff;">var</span> guid = <span style="color: #0000ff;">this</span><span style="color: #000000;">.GetPrimaryKey();
</span><span style="color: #008000;">//</span><span style="color: #008000;">获取我们在配置中定义的一个提供者</span>
<span style="color: #0000ff;">var</span> streamProvider = GetStreamProvider(<span style="color: #800000;">"</span><span style="color: #800000;">SMSProvider</span><span style="color: #800000;">"</span><span style="color: #000000;">);
</span><span style="color: #008000;">//</span><span style="color: #008000;">获取对流的引用</span>
<span style="color: #0000ff;">var</span> stream = streamProvider.GetStream&lt;<span style="color: #0000ff;">int</span>&gt;(guid, <span style="color: #800000;">"</span><span style="color: #800000;">RANDOMDATA</span><span style="color: #800000;">"</span><span style="color: #000000;">);
</span><span style="color: #008000;">//</span><span style="color: #008000;">将我们的OnNext方法设置为lambda，它只输出数据，这不会产生新的订阅</span>
<span style="color: #0000ff;">await</span> stream.SubscribeAsync&lt;<span style="color: #0000ff;">int</span>&gt;(<span style="color: #0000ff;">async</span> (data, token) =&gt; Console.WriteLine(data));</pre>
</div>
<p>我们现在都准备好了 唯一的要求就是触发我们的生产者Grain的创建，然后它将注册计时器，并开始发送随机整数给所有订阅的各方。</p>
<p>再次，这个指南跳过了很多细节，只是为了展示大局。 阅读本手册的其他部分以及RX上的其他资源，以便了解可用的内容和方式。</p>
<p>反应式编程是解决许多问题的一个非常有效的方法。 你可以例如在用户中使用LINQ来过滤数字，并做各种有趣的东西。</p>
<p>&nbsp;</p>
<p><strong>3，为什么选择流</strong></p>
<p>1）为什么选择Orleans Streams?</p>
<p>已经有很多技术可以让你建立流处理系统。 这些系统包括持久存储流数据的系统（例如，事件中心和Kafka）以及用于在流数据上表达计算操作的系统（例如，Azure流分析，Apache风暴和Apache Spark流）。 这些都是非常棒的系统，可以让您构建高效的数据流处理管道。</p>
<p>2）现有系统的局限性<strong><br /></strong></p>
<p>然而，这些系统不适合fine-grained free-form compute over stream data。他的流计算系统首先提到，允许您指定一个统一的数据流图，以相同的方式应用于所有的流项目。当数据是一致的时候，这是一个强大的模型，并且您想要对这些数据表达相同的转换、过滤或聚合操作。但是也有其他的用例，您需要在不同的数据项上表达完全不同的操作。在其中一些过程中，作为处理的一部分，您偶尔需要进行外部调用，例如调用一些任意REST API。统一的数据流处理引擎要么不支持这些场景，要么以有限的、受限的方式支持它们，或者在支持它们方面效率低下。这是因为它们天生就针对大量类似的项目进行优化，并且通常在表达性和处理方面都很有限。Orleans流的目标是那些其他的情形。</p>
<p>3）动机<br />这一切都是从Orleans用户的请求开始的，他们支持从一个Grain方法调用返回一个项目序列。你可以想象，这只是冰山一角。实际上他们需要的远不止这些。</p>
<p>Orleans Streams的一个典型场景是当你有每个用户流，并且你想在每个用户的上下文中为每个用户执行不同的处理。 我们可能有数百万用户，但其中一些对天气感兴趣，可以订阅特定位置的天气警报，而有些则对体育赛事感兴趣; 有人正在跟踪某个航班的状态。 处理这些事件需要不同的逻辑，但是您不希望运行两个独立的流处理实例。 一些用户只对特定的库存感兴趣，并且只有在某些外部条件适用的情况下，条件可能不一定是流数据的一部分（因此需要在运行时作为处理的一部分在动态时检查）。</p>
<p>用户一直在改变他们的兴趣，因此他们对特定事件流的订阅动态地来来回回，因此流动拓扑结构动态而迅速地变化。 此外，根据用户状态和外部事件，每个用户的处理逻辑也会动态变化和变化。 外部事件可能会修改特定用户的处理逻辑。 例如，在游戏作弊检测系统中，当发现新的作弊方式时，处理逻辑需要根据新的规则进行更新，以检测出新的违规行为。 这当然需要在不中断正在进行的处理流程的情况下完成。 批量数据流流处理引擎不是为了支持这种情况而构建的。</p>
<p>毋庸置疑，这样的系统必须在多个联网的机器上运行，而不是在单个节点上运行。 因此，处理逻辑必须以可扩展和弹性的方式分布在一组服务器上。</p>
<p>4）新的要求<br />我们确定了我们的流处理系统的4个基本要求，这将允许它针对上述情况。</p>
<ol>
<li>灵活的流处理逻辑</li>
<li>支持动态拓扑</li>
<li>细粒度的流粒度</li>
<li>分布</li>




</ol>
<p>5）灵活的流处理逻辑<br />我们希望系统支持表达流处理逻辑的不同方式。 我们上面提到的现有系统要求开发人员编写一个声明式的数据流计算图，通常是遵循函数式编程风格。 这限制了处理逻辑的表达性和灵活性。 Orleans流对表达处理逻辑的方式漠不关心。 它可以表示为数据流（例如，通过在.NET中使用Reactive Extensions（Rx））; 作为功能程序; 作为声明性查询; 或在一般的命令逻辑。 逻辑可以是有状态或无状态的，可能有也可能不会有副作用，并且可以触发外部行为。 所有权力都交给开发者。</p>
<p>6）支持动态拓扑<br />我们希望系统允许动态演进的拓扑结构。 我们上面提到的现有系统通常仅限于在部署时固定并且不能在运行时发展的静态拓扑。 在下面的数据流表达式例子中，一切都很好，很简单，直到你需要改变它。</p>
<div class="cnblogs_code">
<pre>Stream.GroupBy(x=&gt; x.key).Extract(x=&gt;x.field).Select(x=&gt;x+<span style="color: #800080;">2</span>).AverageWindow(x, 5sec).Where(x=&gt;x &gt; <span style="color: #800080;">0.8</span>) *</pre>
</div>
<p>在Where过滤器中更改阈值条件，添加额外的Select语句或在数据流图中添加另一个分支并生成新的输出流。 在现有的系统中，如果不拆除整个拓扑并重新启动数据流，这是不可能的。 实际上，这些系统将检查现有的计算，并能够从最新的检查点重新启动。 但是，这样的重启对于实时产生结果的在线服务是破坏性的并且是昂贵的。 当我们谈论大量这样的以相似但不同的（每用户，每个设计等等）参数执行并且保持不断变化的表达式时，这样的重新启动变得特别不切实际。</p>
<p>我们希望系统允许在运行时演进流处理图，通过向计算图添加新的链接或节点，或通过改变计算节点内的处理逻辑。</p>
<p>7）细粒度的流粒度<br />在现有的系统中，抽象的最小单位通常是整个流程（拓扑）。但是，我们的许多目标场景要求拓扑中的单个节点/链路本身是一个逻辑实体。这样每个实体都可以独立管理。例如，在由多个链路组成的大流量拓扑中，不同链路可以具有不同的特性，并且可以在不同的物理传输上实现。一些链接可以通过TCP套接字，而另一些则通过可靠的队列。不同的链接可以有不同的交付保证。不同的节点可以有不同的检查点策略，其处理逻辑可以用不同的模型甚至不同的语言来表示。现有系统通常不具有这种灵活性。</p>
<p>抽象单位和灵活性的论点类似于SoA（面向服务的体系结构）与参与者的比较。演员系统允许更多的灵活性，因为每个人本质上是一个独立管理的&ldquo;小服务&rdquo;。同样，我们希望系统允许这样一个细粒度的控制。</p>
<p>8）分配<br />当然，我们的系统应该具有&ldquo;良好的分布式系统&rdquo;的所有特性。 包括：</p>
<ol>
<li>可伸缩性 - 支持大量的流和计算元素。</li>
<li>弹性 - 允许添加/删除资源以根据负载进行增长/收缩。</li>
<li>可靠性 - 对故障具有恢复能力</li>
<li>效率 - 高效使用底层资源</li>
<li>响应能力 - 启用接近实时的情况。</li>




</ol>
<p>说明：Orleans目前不直接支持编写声明式数据流表达式，如上例所示。 目前的Orleans流媒体API是更低层次的构建块，如下所述。 提供声明性数据流表达式是我们未来的目标。</p>
<p>&nbsp;</p>
<p><strong>4，流编程API</strong></p>
<p>1）Orleans Streams编程API<br />应用程序通过与.NET中众所周知的反应式扩展（Rx）非常相似的API与流进行交互。 主要区别在于Orleans流扩展是异步的，以便在Orleans的分布式和可伸缩计算结构中提高处理效率。</p>
<p>2）异步流<br />应用程序启动使用流提供者得到一个处理流。 您可以在这里阅读关于流提供者的更多信息，但现在您可以将其视为流工厂，允许实现者自定义流行为和语义：</p>
<div class="cnblogs_code">
<pre>IStreamProvider streamProvider = <span style="color: #0000ff;">base</span>.GetStreamProvider(<span style="color: #800000;">"</span><span style="color: #800000;">SimpleStreamProvider</span><span style="color: #800000;">"</span><span style="color: #000000;">);
IAsyncStream</span>&lt;T&gt; stream = streamProvider.GetStream&lt;T&gt;(Guid, <span style="color: #800000;">"</span><span style="color: #800000;">MyStreamNamespace</span><span style="color: #800000;">"</span>);</pre>
</div>
<p>应用程序可以通过在Grain类中调用Grain类的GetStreamProvider方法，或者在客户端上调用GrainClient.GetStreamProvider()方法来获得对流提供者的引用。</p>
<p>Orleans.Streams.IAsyncStream &lt;T&gt;是虚拟流的逻辑强类型句柄。 它与Orleans Grain引用的相似。&nbsp;调用GetStreamProvider和GetStream纯粹是本地的。 GetStream的参数是一个GUID和一个额外的字符串，我们称之为流名称空间（可以为空）。 GUID和名称空间字符串一起组成流标识（类似于GrainFactory.GetGrain的参数）。 GUID和名称空间字符串的组合为确定流标识提供了额外的灵活性。 就像Grain类型PlayerGrain中可能存在Grain 7，并且Grain类型ChatRoomGrain内可能存在不同Grain 7，则流123可以与流名称空间PlayerEventsStream一起存在，并且流名称空间ChatRoomMessagesStream内可以存在不同的流123。</p>
<p>3）生产和消费<br />IAsyncStream &lt;T&gt;实现了Orleans.Streams.IAsyncObserver &lt;T&gt;和Orleans.Streams.IAsyncObservable &lt;T&gt;接口。 这样，应用程序就可以使用这个流来使用Orleans.Streams.IAsyncObserver &lt;T&gt;来产生新的事件到流中，或者通过使用Orleans.Streams.IAsyncObservable &lt;T&gt;来订阅和使用来自流的事件。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span> IAsyncObserver&lt;<span style="color: #0000ff;">in</span> T&gt;<span style="color: #000000;">
{
    Task OnNextAsync(T item, StreamSequenceToken token </span>= <span style="color: #0000ff;">null</span><span style="color: #000000;">);
    Task OnCompletedAsync();
    Task OnErrorAsync(Exception ex);
}

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">interface</span> IAsyncObservable&lt;T&gt;<span style="color: #000000;">
{
    Task</span>&lt;StreamSubscriptionHandle&lt;T&gt;&gt; SubscribeAsync(IAsyncObserver&lt;T&gt;<span style="color: #000000;"> observer);
}</span></pre>
</div>
<p>为了在流中生成事件，应用程序只需要调用</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">await</span> stream.OnNextAsync&lt;T&gt;(<span style="color: #0000ff;">event</span>)</pre>
</div>
<p>要订阅一个流，应用程序调用</p>
<div class="cnblogs_code">
<pre>StreamSubscriptionHandle&lt;T&gt; subscriptionHandle = <span style="color: #0000ff;">await</span> stream.SubscribeAsync(IAsyncObserver)</pre>
</div>
<p>SubscribeAsync的参数既可以是实现IAsyncObserver接口的对象，也可以是用于处理传入事件的lambda函数的组合。 SubscribeAsync的更多选项可通过AsyncObservableExtensions类获得。 SubscribeAsync返回一个StreamSubscriptionHandle &lt;T&gt;，它是一个不透明的Handle，可用于取消订阅流（类似于IDisposable的异步版本）。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">await</span> subscriptionHandle.UnsubscribeAsync()</pre>
</div>
<p>需要注意的是订阅是一个Grain，而不是一个激活。 一旦Grain代码订阅了流，这个订阅超过了这种激活的生命，并保持永久持续，直到Grain代码（可能在不同的激活）明确退订。 这是虚拟流抽象的核心：不仅所有的流都是逻辑地存在，而且流订阅也是持久的，并且超出了发布此订阅的特定物理激活。</p>
<p>4）多重性<br />Orleans流可能有多个生产者和多个消费者。 生产者发布的消息将被传递给消息发布之前订阅了流的所有消费者。</p>
<p>另外，消费者可以多次订阅相同的流。 每次订阅时，都会返回一个唯一的StreamSubscriptionHandle &lt;T&gt;。 如果Grain（或客户端）被X次订阅到同一个流，它将接收相同的事件X次，每次订阅一次。 消费者还可以通过以下方式退订个人订阅或查找其当前所有订阅：</p>
<div class="cnblogs_code">
<pre>IList&lt;StreamSubscriptionHandle&lt;T&gt;&gt; allMyHandles = <span style="color: #0000ff;">await</span> IAsyncStream&lt;T&gt;.GetAllSubscriptionHandles()</pre>
</div>
<p>5）从故障中恢复<br />如果一个流的生产者挂了（或者它的Grain被停用），那么它就没有必要去做。 下一次这个Grain想要产生更多的事件，它可以重新获得流处理，并以相同的方式产生新的事件。</p>
<p>消费者逻辑涉及更多一点。 正如我们之前所说，一旦消费者Grain订阅了一个流，这个订阅是有效的，直到它明确退订。 如果流的消费者死亡（或其Grain被停用），并且在该流上产生新的事件，则消费者Grain将被自动地重新激活（就像任何常规的Orleans Grain在向其发送消息时自动激活）。 grain代码现在唯一需要做的就是提供一个IAsyncObserver &lt;T&gt;来处理数据。 消费者基本上需要重新附加处理逻辑作为OnActivateAsync方法的一部分。 要做到这一点，可以调用：</p>
<div class="cnblogs_code">
<pre>StreamSubscriptionHandle&lt;<span style="color: #0000ff;">int</span>&gt; newHandle = <span style="color: #0000ff;">await</span> subscriptionHandle.ResumeAsync(IAsyncObserver)</pre>
</div>
<p>消费者使用它在第一次订购时得到的上一个句柄，以便&ldquo;恢复处理&rdquo;。 请注意，ResumeAsync仅使用IAsyncObserver逻辑的新实例更新现有订阅，并不会更改此消费者已订阅此流的事实。</p>
<p>消费者如何拥有一个旧的订阅句柄?有两个选项。消费者可能已经持久化了从原来的SubscribeAsync操作中返回的句柄，现在可以使用它了。或者，如果消费者没有这个句柄，它可以通过调用来要求IAsyncStream 的所有主动订阅句柄:</p>
<div class="cnblogs_code">
<pre>IList&lt;StreamSubscriptionHandle&lt;T&gt;&gt; allMyHandles = <span style="color: #0000ff;">await</span> IAsyncStream&lt;T&gt;.GetAllSubscriptionHandles()</pre>
</div>
<p>消费者现在可以恢复所有这些，或者如果他愿意的话退订。</p>
<p>注释：如果用户grain直接实现了IAsyncObserver接口（公共类MyGrain &lt;T&gt;：Grain，IAsyncObserver &lt;T&gt;），理论上不需要重新连接IAsyncObserver，因此不需要调用ResumeAsync。 流式运行时应该能够自动确定grain已经实现了IAsyncObserver，并且只会调用那些IAsyncObserver方法。 然而，流式运行环境目前不支持这个，即使粮食直接实现了IAsyncObserver，粮食代码仍然需要显式调用ResumeAsync。 支持这是在我们的TODO名单上。</p>
<p>6）显式和隐式订阅<br />默认情况下，流消费者必须显式订阅流。 这种订阅通常会由Grain（或客户端）收到的一些外部消息触发，指示他们订阅。 例如，在聊天服务中，当用户加入聊天室时，他的Grain会收到带有聊天名称的JoinChatGroup消息，并且会导致用户Grain订阅这个聊天流。</p>
<p>此外，Orleans Streams也支持&ldquo;隐式订阅&rdquo;。在这个模型中，Grain并不明确订阅流。这个Grain是自动订阅的，隐式的，只是基于其Grain身份和一个ImplicitStreamSubscription属性。隐式订阅的主要价值是允许流活动触发Grain激活（因此触发订阅）自动。 例如，使用SMS流，如果一个Grain想要产生一个流，而另一个Grain处理这个流，那么生产者就需要知道消费者Grain的身份，并且要求Grain调用它来订购这个流。 只有在此之后，才能开始发送事件。 只有在此之后，才能开始发送事件。 相反，使用隐式订阅，生产者可以开始将事件生成到流上，并且消费者Grain将自动被激活并订阅流。 在这种情况下，制片人完全不在乎谁在阅读这些事件</p>
<p>类型为MyGrainType的Grain实现类可以声明一个属性[ImplicitStreamSubscription（&ldquo;MyStreamNamespace&rdquo;）]。 这将告诉流式运行时，如果在标识为GUID XXX和&ldquo;MyStreamNamespace&rdquo;命名空间的流上生成事件，则应该将其传递给标识为XXX类型为MyGrainType的grain。 也就是说，运行时将流&lt;XXX，MyStreamNamespace&gt;映射到消费者Grain&lt;XXX，MyGrainType&gt;。</p>
<p>ImplicitStreamSubscription的存在使得流式运行时自动将这个Grain订阅到一个流，并将流事件传递给它。 然而，grain代码仍然需要告诉运行时如何处理事件。 本质上，它需要附加IAsyncObserver。 因此，在激活Grain时，OnActivateAsync中的Grain代码需要调用：</p>
<div class="cnblogs_code">
<pre>IStreamProvider streamProvider = <span style="color: #0000ff;">base</span>.GetStreamProvider(<span style="color: #800000;">"</span><span style="color: #800000;">SimpleStreamProvider</span><span style="color: #800000;">"</span><span style="color: #000000;">);
IAsyncStream</span>&lt;T&gt; stream = streamProvider.GetStream&lt;T&gt;(<span style="color: #0000ff;">this</span>.GetPrimaryKey(), <span style="color: #800000;">"</span><span style="color: #800000;">MyStreamNamespace</span><span style="color: #800000;">"</span><span style="color: #000000;">);
StreamSubscriptionHandle</span>&lt;T&gt; subscription = <span style="color: #0000ff;">await</span> stream.SubscribeAsync(IAsyncObserver&lt;T&gt;);</pre>
</div>
<p>7）编写订阅逻辑<br />以下是关于如何为各种情况编写订阅逻辑的准则：显式和隐式订阅，可回放和不可回放的流。 显式和隐式订阅的主要区别在于，对于隐式的grain，每个流名称空间总是只有一个隐式订阅，没有办法创建多个订阅（没有订阅多重性），没有办法退订，而 grain逻辑总是只需要附加处理逻辑。 这也意味着，对于隐式订阅，从不需要恢复订阅。 另一方面，对于明确的订阅，需要恢复订阅，否则如果再次订阅，将会导致订阅多次。</p>
<p>①隐含订阅：</p>
<p>对于隐式订阅，Grain需要订阅附加处理逻辑。 这应该在Grain的OnActivateAsync方法中完成。 Grain应该简单地执行在其OnActivateAsync方法中等待stream.SubscribeAsync（OnNext ...）。 这将导致这个特定的激活附加OnNext函数来处理该流。 grain可以选择指定StreamSequenceToken作为SubscribeAsync的参数，这将导致这个隐式订阅从该标记开始消耗。 从不需要隐式订阅来调用ResumeAsync。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> <span style="color: #0000ff;">override</span><span style="color: #000000;"> Task OnActivateAsync()
{
    </span><span style="color: #0000ff;">var</span> streamProvider =<span style="color: #000000;"> GetStreamProvider(PROVIDER_NAME);
    </span><span style="color: #0000ff;">var</span> stream = streamProvider.GetStream&lt;<span style="color: #0000ff;">string</span>&gt;(<span style="color: #0000ff;">this</span>.GetPrimaryKey(), <span style="color: #800000;">"</span><span style="color: #800000;">MyStreamNamespace</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    </span><span style="color: #0000ff;">await</span><span style="color: #000000;"> stream.SubscribeAsync(OnNextAsync)
}</span></pre>
</div>
<p>②显式订阅：</p>
<p>对于显式订阅，grain必须调用SubscribeAsync来订阅流。 这创建了一个订阅，以及附加的处理逻辑。 显式订阅将存在，直到Grain退订，所以如果Grain被取消激活，Grain仍然显式订阅，但不附加处理逻辑。 在这种情况下，Grain需要重新连接处理逻辑。 要做到这一点，在OnActivateAsync中，Grain首先需要通过调用stream.GetAllSubscriptionHandles（）来找出它的订阅。 grain必须在每个希望继续处理的handle上执行ResumeAsync，或者在完成的任何handle上执行UnsubscribeAsync。 Grain还可以选择指定StreamSequenceToken作为ResumeAsync调用的参数，这将导致显式订阅从该令牌开始消耗。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> <span style="color: #0000ff;">override</span><span style="color: #000000;"> Task OnActivateAsync()
{
    </span><span style="color: #0000ff;">var</span> streamProvider =<span style="color: #000000;"> GetStreamProvider(PROVIDER_NAME);
    </span><span style="color: #0000ff;">var</span> stream = streamProvider.GetStream&lt;<span style="color: #0000ff;">string</span>&gt;(<span style="color: #0000ff;">this</span>.GetPrimaryKey(), <span style="color: #800000;">"</span><span style="color: #800000;">MyStreamNamespace</span><span style="color: #800000;">"</span><span style="color: #000000;">);
    </span><span style="color: #0000ff;">var</span> subscriptionHandles = <span style="color: #0000ff;">await</span><span style="color: #000000;"> stream.GetAllSubscriptionHandles();
    </span><span style="color: #0000ff;">if</span> (!<span style="color: #000000;">subscriptionHandles.IsNullOrEmpty())
        subscriptionHandles.ForEach(</span><span style="color: #0000ff;">async</span> x =&gt; <span style="color: #0000ff;">await</span><span style="color: #000000;"> x.ResumeAsync(OnNextAsync));
}</span></pre>
</div>
<p>8）流顺序和序列令牌<br />个体生产者和个人消费者之间交付事件的顺序取决于流提供者。</p>
<p>通过SMS，生产者通过控制他发布的方式来明确地控制消费者看到的事件的顺序。 默认情况下（如果SMS提供程序的FireAndForget选项设置为false），并且生产者等待每个OnNextAsync调用，则事件按FIFO顺序到达。 在SMS中，由生产者决定如何处理由OnNextAsync调用返回的破坏的Task所指示的交付失败。</p>
<p>Azure队列流不保证FIFO顺序，因为底层的Azure队列不能保证在失败情况下的顺序（它们确保在无故障执行中的FIFO顺序）。 当生产者将事件生成到Azure队列中时，如果排队操作失败，则由生产者尝试另一个排队，然后再处理潜在的重复消息。 在交付方面，Orleans Streaming运行时从Azure队列中取出事件并尝试将其交付给消费者进行处理。 Orleans Streaming运行时只有在成功处理后才会从队列中删除事件。 如果交付或处理失败，则该事件不会从队列中删除，并会在稍后自动重新出现在队列中。 Streaming运行时将尝试再次传送，因此可能会破坏FIFO的顺序。 描述的行为符合Azure队列的常规语义。</p>
<p>应用程序定义的顺序：要处理上述顺序问题，应用程序可以选择指定自己的顺序。 这是通过StreamSequenceToken的概念来实现的。 StreamSequenceToken是一个不透明的IComparable对象，可用于对事件进行排序。 生产者可以将可选的StreamSequenceToken传递给OnNext调用。 这个StreamSequenceToken将被一直传递给消费者，并将与该事件一起交付。 这样，应用程序就可以独立于流式运行时间来推理和重建它的顺序。</p>
<p>9）可回放的流<br />一些数据流只允许应用程序在最近的时间点开始订阅，而其他数据流允许&ldquo;回溯&rdquo;。 后者的能力取决于潜在的排队技术和特定的流提供者。 例如，Azure队列只允许使用最新的入队事件，而EventHub允许从任意时间点（最多到某个过期时间）重放事件。 支持回溯的流被称为可回溯流。</p>
<p>可重放流的使用者可以将StreamSequenceToken传递给SubscribeAsync调用，并且运行时将从该StreamSequenceToken（一个null标记表示消费者希望从最近开始接收事件）开始向其传递事件。</p>
<p>回放流的能力在恢复场景中非常有用。 例如，考虑订阅流的grain，并定期检查其状态以及最新的序列标记。 从故障中恢复时，grain可以从最新的检查点序列标记重新订阅相同的流，从而进行恢复，而不会丢失自上一个检查点以来生成的任何事件。</p>
<p>可重放流的当前状态：SMS和Azure队列提供程序都不可回滚，Orleans当前不包含可重放流的实现。 我们正在积极努力。</p>
<p>10）无状态自动扩展处理<br />默认情况下，Orleans Streaming的目标是支持大量相对较小的流，每个流都由一个或多个完整的Grains进行处理。 所有的流加工在一起，在大量的正常（稳定的）Grain中被分割。 应用程序代码通过分配流ID，grain ID和显式订阅来控制这个分片。 目标是分解状态处理。</p>
<p>但是，自动扩展的无状态处理也是一个有趣的场景。 在这种情况下应用程序有少量的流（甚至一个大的流），目标是无状态处理。 例如，所有事件的所有消息的全局流以及涉及某种解码/解密的处理，并可能将它们转发到另一组流中进行进一步的有状态处理。 Orleans通过StatelessWorker谷物支持无状态的扩展流处理。</p>
<p>无状态自动扩展处理的当前状态：目前尚未实现（由于优先级限制）。 尝试订阅来自StatelessWorker grain的流将导致未定义的行为。 我们正在考虑支持这个选项。</p>
<p>11）Grain和Orleans客户端<br />Orleans流在Grain和Orleans客户端之间均匀流通。 也就是说，Grain和Orleans客户端可以使用完全相同的API来生成和消费事件。 这极大地简化了应用程序逻辑，使特殊的客户端API（如Grain Observers）变得冗余。</p>
<p>12）完全管理和可靠的流媒体Pub-Sub<br />为了跟踪流预订，Orleans使用一个名为Streaming Pub-Sub的运行时组件，它作为流消费者和流生产者的集合点。 Pub Sub跟踪所有的流订阅，保持它们，并将流消费者与流生产者匹配。</p>
<p>应用程序可以选择Pub-Sub数据的存储位置和方式。 Pub-Sub组件本身被实现为Grain（称为PubSubRendezvousGrain），它正在使用Orleans声明式持久性来表示这些Grain。 PubSubRendezvousGrain使用名为PubSubStore的存储提供程序。 与任何Grain一样，您可以指定一个存储提供者的实现。 对于Streaming Pub-Sub，您可以在配置文件中更改PubSubStore的实现：&nbsp;</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">OrleansConfiguration </span><span style="color: #ff0000;">xmlns</span><span style="color: #0000ff;">="urn:orleans"</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Globals</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">StorageProviders</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Provider </span><span style="color: #ff0000;">Type</span><span style="color: #0000ff;">="Orleans.Storage.AzureTableStorage"</span><span style="color: #ff0000;"> Name</span><span style="color: #0000ff;">="PubSubStore"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">StorageProviders</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Globals</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">OrleansConfiguration</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>这样，Pub-Sub数据将持久存储在Azure表中。 对于最初的开发，您也可以使用内存存储。 除Pub-Sub之外，Orleans Streaming Runtime还将生产者的事件传递给消费者，管理分配给主动使用的流的所有运行时资源，并透明地垃圾从未使用的流中收集运行时资源。</p>
<p>13）配置<br />为了使用流，您需要通过配置启用流提供程序。 你可以在这里阅读更多关于流提供者。 示例流提供程序配置：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">OrleansConfiguration </span><span style="color: #ff0000;">xmlns</span><span style="color: #0000ff;">="urn:orleans"</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Globals</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">StreamProviders</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Provider </span><span style="color: #ff0000;">Type</span><span style="color: #0000ff;">="Orleans.Providers.Streams.SimpleMessageStream.SimpleMessageStreamProvider"</span><span style="color: #ff0000;"> Name</span><span style="color: #0000ff;">="SMSProvider"</span><span style="color: #0000ff;">/&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Provider </span><span style="color: #ff0000;">Type</span><span style="color: #0000ff;">="Orleans.Providers.Streams.AzureQueue.AzureQueueStreamProvider"</span><span style="color: #ff0000;"> Name</span><span style="color: #0000ff;">="AzureQueueProvider"</span><span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">StreamProviders</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Globals</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">OrleansConfiguration</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>也可以通过调用Orleans.Runtime.Configuration.GlobalConfiguration或Orleans.Runtime.Configuration.ClientConfiguration类中的一个RegisterStreamProvider方法来以编程方式注册流提供程序。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> RegisterStreamProvider(<span style="color: #0000ff;">string</span> providerTypeFullName, <span style="color: #0000ff;">string</span> providerName, IDictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">string</span>&gt; properties = <span style="color: #0000ff;">null</span><span style="color: #000000;">)

</span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span> RegisterStreamProvider&lt;T&gt;(<span style="color: #0000ff;">string</span> providerName, IDictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">string</span>&gt; properties = <span style="color: #0000ff;">null</span>) <span style="color: #0000ff;">where</span> T : IStreamProvider</pre>
</div>
<p>&nbsp;</p>
<p><strong>5，流提供者</strong></p>
<p>&nbsp;流可以有不同的形状和形式，&nbsp;一些流可能通过直接的TCP链接传递事件，而另一些则通过持久队列传递事件。不同的流类型可能使用不同的批处理策略、不同的缓存算法或不同的背压过程。我们不希望将流应用程序限制在这些行为选择的一小部分。 相反，Stream Providers是Orleans Streaming Runtime的扩展点，允许用户实现任何类型的流。 这个可扩展性与Orleans存储提供商的精神是相似的。 Orleans目前提供两个默认流提供程序：简单消息流提供程序和Azure队列流提供程序。</p>
<p>1）简单的消息流提供者<br />简单的消息流提供商，也被称为SMS提供商，通过利用常规的Orleans Grain消息传递在TCP上传递事件。 由于SMS中的事件是通过不可靠的TCP链接传送的，因此SMS不保证可靠的事件传送，也不会自动重新发送SMS流的失败消息。 SMS流的生产者有一种方法来知道他的事件是否被成功地接收和处理：默认情况下，对stream.OnNextAsync的调用返回一个代表流消费者处理状态的Task。 如果这个任务失败了，生产者可以决定再次发送相同的事件，从而在应用层面上实现可靠性。 虽然个人流消息传递是尽力而为的，但SMS流本身是可靠的。 也就是说，Pub Sub执行的用户到生产者的绑定是完全可靠的。</p>
<p>2）Azure队列（AQ）流提供程序<br />Azure队列（AQ）流提供程序通过Azure队列传递事件。 在生产者方面，AQ Stream Provider将事件直接排入Azure队列。 在消费者方面，AQ Stream Provider管理一组拉取代理，这些拉取代理从一组Azure队列中提取事件，并将其传递给使用它们的应用程序代码。 人们可以把提取代理想象成一个分布式的&ldquo;微服务&rdquo; - 一个分区的，高度可用的，有弹性的分布式组件。 拉出的代理程序运行在宿主应用程序Grains的同一仓储内。 因此，不需要运行独立的Azure角色来从队列中拉出。 牵引代理的存在，其管理，后台管理，平衡他们之间的队列以及将失败代理中的队列交给另一个代理完全由Orleans Streaming Runtime管理，并且对于使用流的应用程序代码是透明的。</p>
<p>3）队列适配器<br />通过持久队列传递事件的不同流提供者表现出类似的行为，并受到类似的实现。 因此，我们提供了一个通用的可扩展PersistentStreamProvider，它允许开发人员从头开始写入不同类型的队列，而无需从头开始编写全新的流提供程序。 PersistentStreamProvider用IQueueAdapter参数化，IQueueAdapter抽象出特定的队列实现细节，并提供入队和出队事件的方法。 其余的由PersistentStreamProvider内部的逻辑处理。 上面提到的Azure队列提供程序也是这样实现的：它是具有AzureQueueAdapter的PersistentStreamProvider实例。</p>
<p><strong>6，流实现</strong></p>
<p>本节提供了Orleans Stream实现的高级概述。 它描述了在应用程序级别上不可见的概念和细节。 如果您只打算使用流，则不必阅读本节。 但是，如果您打算扩展流，请在阅读Streams Extensibility部分之前阅读本节。</p>
<p>术语：</p>
<p>我们将&ldquo;queue&rdquo;这个词引用到任何可以提取流事件的持久存储技术，并允许提取事件或提供基于推的机制来消费事件。 通常，为了提供可伸缩性，这些技术提供分片/分区队列。 例如，Azure队列允许创建多个队列，事件中心有多个中心，Kafka主题，...</p>
<p>1）持久化流<br />所有Orleans持久流提供者共享一个通用的实现PersistentStreamProvider。 这个通用的流提供者是通过一个技术特定的IQueueAdapter进行参数化的。</p>
<p>当流生成器生成一个新的流项并调用stream.OnNext()时，Orleans流运行时调用该流提供者的IQueueAdapter上的适当方法，将该项直接排入适当的队列。</p>
<p>2）拉代理<br />持续流提供者的核心是拉动代理。 提取代理从一组持久队列中提取事件，并将它们传送到消耗它们的Grain中的应用程序代码。 人们可以把提取代理想象成一个分布式的&ldquo;微服务&rdquo; - 一个分区的，高度可用的，有弹性的分布式组件。 牵引剂运行在托管Grain的同一个仓储内，并由Orleans Streaming Runtime完全管理。</p>
<p>3）StreamQueueMapper和StreamQueueBalancer</p>
<p>Pulling代理使用IStreamQueueMapper和StreamQueueBalancerType进行参数化。IStreamQueueMapper提供了所有队列的列表，并负责将流映射到队列。 这样，持久流提供者的生产者端知道将哪个队列排入消息。StreamQueueBalancerType表示Orleans仓储和代理之间的队列平衡方式。 目标是以平衡的方式将队列分配给代理，以防止瓶颈和支持弹性。 当新的仓储被添加到Orleans集群时，队列会自动在旧的和新的筒仓中重新平衡。 StreamQueueBalancer允许自定义该进程。 Orleans有一些内置的StreamQueueBalancers，用于支持不同的平衡方案（大小队列数）和不同的环境（Azure，on prem，static）。&nbsp;</p>
<p>4）Pulling 协议</p>
<p>每个仓储都运行一组拖放代理，每个代理都从一个队列中拉出。提取代理本身由内部运行时组件(称为SystemTarget)实现。系统目标本质上是运行时的Grain，受到单线程并发性的影响，可以使用常规的Grain消息传递，并且像Grain一样轻。与Grain相反，系统目标不是虚拟的:它们是显式创建的(由运行时创建的)，也不是位置透明的。通过将拉代理实现为系统目标，对Orleans的流运行时可以依赖于许多内置的Orleans特性，并且可以扩展到大量的队列，因为创建一个新的拉动代理就像创建一种新的谷Grain一样便宜。</p>
<p>每个拉取代理都运行定期计时器，该计时器从队列中拉出（通过调用IQueueAdapterReceiver）GetQueueMessagesAsync（）方法。 返回的消息放在名为IQueueCache的内部每个代理程序数据结构中。 每条消息都被检查以找出其目的地流。 代理程序使用Pub Sub来找出订阅此流的流消费者的列表。 一旦消费者列表被检索到，代理将其存储在本地（在其pub-sub高速缓存中），因此不需要在每个消息上咨询Pub Sub。 代理还与pub-sub订阅，以接收任何订阅该流的新消费者的通知。 代理与pub-sub之间的握手保证了强大的流式订阅语义：一旦消费者订阅了流，它就会看到订阅之后生成的所有事件（另外，使用StreamSequenceToken允许在过去订阅）。</p>
<p>5）队列缓存<br />IQueueCache是一种内部的每个代理数据结构，允许将新事件从队列中传递给消费者。 它也允许将交付分离到不同的流和不同的消费者。</p>
<p>想象一下，一个流有三个流消费者，其中一个流很慢。 如果不小心，缓慢的消费者有可能会影响代理商的进度，减缓其他消费者的消费，甚至有可能减缓其他消费者的排队和交付。 为了防止这种情况，并允许代理中的最大并行性，我们使用IQueueCache。</p>
<p>IQueueCache缓存流事件，并为代理提供一种方式，以按照其速度向每个消费者传递事件。 每个消费者交付由称为IQueueCacheCursor的内部组件实现，该组件跟踪每个消费者的进度。 这样，每个消费者都能按照自己的速度接收事件：快速消费者接收事件的速度就像从队列中出列的速度一样快，而慢速消费者接收事件的速度也是如此。 一旦消息被传递给所有消费者，它可以从缓存中删除。</p>
<p>6）Backpressure<br />在Orleans，流运行时的Backpressure应用于两个地方:将流事件从队列中引入代理，并将事件从代理传递到流消费者。</p>
<p>后者由内置的Orleans消息传递机制提供。 每一个流事件都是通过标准的Orleans grain 消息从代理商传递给消费者，一次一个。 也就是说，代理向每个流消费者发送一个事件（或一个有限的大小的事件）并等待这个呼叫。 下一个事件将不会开始传递，直到上一个事件的任务已解决或中断。 这样，我们自然地将每个消费者的交付率限制在一个消息。</p>
<p>关于从排队到代理商的流事件Orleans流媒体提供了一个新的特殊的Backpressure机制。由于代理将队列中的事件从队列中分离出来并交付给消费者，所以单个缓慢的消费者可能落后得太多以至于IQueueCache将被填满。为了防止IQueueCache无限增长，我们限制它的大小（大小限制是可配置的）。然而，代理从来没有抛出未交付的事件。相反，当缓存开始填满时，代理会降低从队列中取出事件的速率。那样的话，我们可以通过调整我们从队列中消耗的速度（&ldquo;背压&rdquo;）来&ldquo;调整&rdquo;缓慢的交付周期，并在稍后恢复到快速消费速度。为了检测&ldquo;慢速递送&rdquo;谷，IQueueCache使用高速缓存桶的内部数据结构来追踪事件传递给单个流消费者的进度。这导致了一个非常灵敏和自我调整的系统。</p>
<p><strong>7，流扩展性</strong></p>
<p>&nbsp;开发人员可以通过三种方式扩展当前已实现的Orleans流的行为:</p>
<ol>
<li>利用或扩展流提供者配置。</li>
<li>编写一个自定义队列适配器。</li>
<li>写入一个新的流提供程序</li>
</ol>
<p>我们将在下面描述这些。请在阅读本节之前阅读新Orleans的Streams实现，以便对内部实现有一个高级的视图。</p>
<p>1）流提供程序配置<br />目前实现的流提供程序支持一些配置选项。</p>
<p>简单的消息流提供者配置。 SMS Stream Provider当前仅支持单个配置选项：</p>
<ol>
<li>FireAndForgetDelivery：这个选项指定SMS流生成器发送的消息是否被发送，忘记了是否被发送。 当FireAndForgetDelivery设置为false（消息发送不是FireAndForget）时，流生成器的调用stream.OnNext（）将返回一个Task，它表示流消费者的处理状态。 如果这个任务成功了，那么制作人就可以确定消息已经成功传递和处理了。 如果FireAndForgetDelivery设置为true，则返回的Task仅表示Orleans运行时已接受消息并将其排入队列以供进一步传送。 FireAndForgetDelivery的默认值为false。</li>
</ol>
<p>持续流提供程序配置。 所有持久流提供程序都支持以下配置选项：</p>
<ol>
<li>GetQueueMessagesTimerPeriod - 在代理尝试再次拉取之前，最后一次尝试从队列中拉出没有返回任何项目的拉取代理等待的时间。 缺省值是100毫秒。</li>
<li>InitQueueTimeout - 拉取代理程序等待适配器初始化与队列的连接的时间。 默认是5秒。</li>
<li>QueueBalancerType - 用于在队列和代理之间平衡队列的平衡算法的类型。 默认是ConsistentRingBalancer。</li>
</ol>
<p>Azure队列流提供程序配置。 Azure队列流提供程序除持久化流提供程序支持的以外，还支持以下配置选项：</p>
<ol>
<li>DataConnectionString - Azure队列存储连接字符串。</li>
<li>DeploymentId - 此Orleans集群的部署标识（通常类似于Azure部署标识）。</li>
<li>CacheSize - 持久提供者缓存的大小，用于存储流消息以进一步传递。 默认是4096。</li>
</ol>
<p>这将是完全可能的，而且很多时候很容易提供额外的配置选项。 例如，在某些场景中，开发人员可能需要更多地控制队列适配器使用的队列名称。 这是目前抽象与IStreamQueueMapper，但目前没有办法配置哪个IStreamQueueMapper使用，而无需编写一个新的代码。 如果需要的话，我们很乐意提供这样的选择。 所以在编写一个全新的提供者之前，请考虑在现有的流提供者中添加更多的配置选</p>
<p>2）编写自定义队列适配器<br />如果您想使用不同的排队技术，则需要编写一个队列适配器，将适配器的访问权限抽象出来。 下面我们提供如何完成的细节。 有关示例，请参阅AzureQueueAdapterFactory。</p>
<ol>
<li>
<p>首先定义一个实现IQueueAdapterFactory的MyQueueFactory类。 你需要：</p>
<p>a.&nbsp;初始化工厂：读取传递的配置值，如果需要，可能会分配一些数据结构等。</p>
<p>b.&nbsp;实现一个返回IQueueAdapter的方法。</p>
<p>c.实现一个返回IQueueAdapterCache的方法。 理论上来说，你可以建立你自己的IQueueAdapterCache，但是你不需要。 分配并返回Orleans的SimpleQueueAdapterCache是个好主意。</p>
<p>d.实现一个返回IStreamQueueMapper的方法。 再一次，理论上可以建立你自己的IStreamQueueMapper，但是你不需要。 分配并返回一个Orleans HashRingBasedStreamQueueMapper是一个好主意。</p>
</li>
<li>
<p>实现实现IQueueAdapter接口的MyQueueAdapter类，该接口是管理对分片队列的访问的接口。 IQueueAdapter管理对一组队列/队列分区（这些是由IStreamQueueMapper返回的队列）的访问。 它提供了在指定的队列中排队消息的能力，并为特定的队列创建IQueueAdapterReceiver。</p>
</li>
<li>
<p>实现实现IQueueAdapterReceiver的MyQueueAdapterReceiver类，它是管理对一个队列（一个队列分区）的访问的接口。 除了初始化和关闭之外，它基本上提供了一种方法：从队列中检索最多maxCount消息。</p>
</li>
<li>
<p>声明公共类MyQueueStreamProvider：PersistentStreamProvider &lt;MyQueueFactory&gt;。 这是您的新Stream Provider。</p>
</li>
<li>
<p>配置：为了加载和使用你新的流提供商，你需要通过仓储配置文件来正确配置它。 如果您需要在客户端上使用它，则需要在客户端配置文件中添加一个类似的配置元素。 也可以以编程方式配置流提供程序。 以下是仓储配置的一个例子：</p>
</li>
</ol>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">OrleansConfiguration </span><span style="color: #ff0000;">xmlns</span><span style="color: #0000ff;">="urn:orleans"</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Globals</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">StreamProviders</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">Provider </span><span style="color: #ff0000;">Type</span><span style="color: #0000ff;">="My.App.MyQueueStreamProvider"</span><span style="color: #ff0000;"> Name</span><span style="color: #0000ff;">="MyStreamProvider"</span><span style="color: #ff0000;"> GetQueueMessagesTimerPeriod</span><span style="color: #0000ff;">="100ms"</span><span style="color: #ff0000;"> AdditionalProperty</span><span style="color: #0000ff;">="MyProperty"</span><span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">StreamProviders</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">Globals</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">OrleansConfiguration</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>3）编写一个完全新的流提供程序也可以编写一个全新的Stream Provider</p>
<p>在这种情况下，从Orleans 的角度来看，需要做的很少的整合。 您只需要实现IStreamProviderImpl接口，该接口是一个允许应用程序代码获取流的句柄的精简接口。 除此之外，如何实施它完全取决于你。 实现一个全新的Stream Provider可能变成一个相当复杂的任务，因为您可能需要访问各种内部运行时组件，其中一些可能具有内部访问权限。</p>
<p>我们目前没有预想到需要实现一个全新的Stream Provider并且不能通过上面提到的两个选项来实现他的目标的场景：通过扩展配置或者通过编写队列适配器。 但是，如果您认为您有这样的情况，我们希望听到这个消息，并一起努力简化编写新的流提供程序。</p>
<p>&nbsp;</p>