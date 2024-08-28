<p>一、config.xml配置文件</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('b5ffc2aa-83cb-4711-99d5-d98947c99e60')"><img id="code_img_closed_b5ffc2aa-83cb-4711-99d5-d98947c99e60" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_b5ffc2aa-83cb-4711-99d5-d98947c99e60" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('b5ffc2aa-83cb-4711-99d5-d98947c99e60',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_b5ffc2aa-83cb-4711-99d5-d98947c99e60" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">widget </span><span style="color: #ff0000;">id</span><span style="color: #0000ff;">="A12345678901"</span><span style="color: #ff0000;">  version</span><span style="color: #0000ff;">="0.0.1"</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">name</span><span style="color: #0000ff;">&gt;</span>API Example<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">name</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">description</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">
        API Example App.
    </span><span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">description</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">author </span><span style="color: #ff0000;">email</span><span style="color: #0000ff;">="developer@apicloud.com"</span><span style="color: #ff0000;"> href</span><span style="color: #0000ff;">="http://www.apicloud.com"</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">
        APICloud.SIR
    </span><span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">author</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">content </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="index.html"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">access </span><span style="color: #ff0000;">origin</span><span style="color: #0000ff;">="*"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">preference </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="windowBackground"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">="#FFF"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">permission </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="call"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">feature </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="weiXin"</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">param </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="urlScheme"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">="wx7779c7c063a9d4d9"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">feature</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">widget</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<span class="cnblogs_code_collapse">config.xml</span></div>
<ul>
<li>&ldquo;id&rdquo;: 必填，应用ID，由云服务器自动分配。它是该应用的唯一标识。</li>
<li>&ldquo;version&rdquo;：必填，应用的版本号。</li>
<li>&ldquo;name&rdquo;：必填，应用名称。</li>
<li>&ldquo;description&rdquo;：可选，应用简单描述信息。</li>
<li>&ldquo;content&rdquo;：必填，应用运行的起始页。</li>
<li>&ldquo;permission&rdquo;：必填，权限配置。 （详细介绍见<a href="https://docs.apicloud.com/APICloud/%E6%8A%80%E6%9C%AF%E4%B8%93%E9%A2%98/app-config-manual">应用配置指南</a>文档）</li>
</ul>
<p>二、模块调用</p>
<div class="cnblogs_code">
<pre> <span style="color: #0000ff;">var</span><span style="color: #000000;"> dialogBox;
    apiready </span>= <span style="color: #0000ff;">function</span><span style="color: #000000;">() { 
        dialogBox </span>= api.require('dialogBox'<span style="color: #000000;">);
    }</span></pre>
</div>
<p>三、属性</p>
<p>1，tapmode</p>
<p>tapmode具有速点击事件功能，在触发事件中加入tapmode可以消除JS中标准click事件的300毫秒延迟；同时，它具有触发可显示样式的效果，tapmode='css样式类' 属性，当该元素touchstart touchmove的时候就会展现css样式。</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('64d725fa-0b0a-4572-a359-2984cbeb751e')"><img id="code_img_closed_64d725fa-0b0a-4572-a359-2984cbeb751e" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_64d725fa-0b0a-4572-a359-2984cbeb751e" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('64d725fa-0b0a-4572-a359-2984cbeb751e',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_64d725fa-0b0a-4572-a359-2984cbeb751e" class="cnblogs_code_hide">
<pre> <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">tapmode onclick</span><span style="color: #0000ff;">="aa()"</span><span style="color: #0000ff;">&gt;</span>点击我tapmode<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">
function aa()
{
    alert("aa");
}</span></pre>
</div>
<span class="cnblogs_code_collapse">code</span></div>
<p>四、方法</p>
<p>1，parseTapmode</p>
<p>&nbsp;<span class="cnblogs_code">api.parseTapmode()</span>&nbsp;</p>
<p>若是之后用代码创建的 dom 元素，则需要调用该方法后 tapmode 属性才会生效&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('1f75f22a-65c6-4834-b25d-911cec944c53')"><img id="code_img_closed_1f75f22a-65c6-4834-b25d-911cec944c53" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_1f75f22a-65c6-4834-b25d-911cec944c53" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('1f75f22a-65c6-4834-b25d-911cec944c53',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_1f75f22a-65c6-4834-b25d-911cec944c53" class="cnblogs_code_hide">
<pre><span style="color: #000000;">!!!注意!!!：引擎对具有tapmode属性的元素点击事件的优化处理会在apiready事件触发之前，根据当前的dom树自动进行优化。在apiready之后加载的数据使用要显式的调用api.parseTapmode方法来进行主动的tapmode处理，例如在上拉加载更多数据后，要调用一下api.parseTapmode方法.
!!!注意!!!：要按UE设计确定可点击区域的大小，可以适当扩大点击区域来保障点击反应的灵敏。
!!!注意!!!：api.parseTapmode调用会有性能成本，不需要的情况下不要随便调用。
!!!注意!!!：要按照需求明确所有按钮点击时的交互效果，为tapmode属性设置正确的样式值，对于没有交互效果的点击实现，可以不为tapmode属性指定任何样式，但是为了优化点击速度，必须要给元素增加tapmode属性。</span></pre>
</div>
<span class="cnblogs_code_collapse">注意事项</span></div>
<p>2，fixStatusBar&nbsp;</p>
<p>传入的DOM元素增加适当的上内边距，避免header与状态栏重叠</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('907cb20f-2a61-4eac-8c0c-6374a06d2fc6')"><img id="code_img_closed_907cb20f-2a61-4eac-8c0c-6374a06d2fc6" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_907cb20f-2a61-4eac-8c0c-6374a06d2fc6" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('907cb20f-2a61-4eac-8c0c-6374a06d2fc6',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_907cb20f-2a61-4eac-8c0c-6374a06d2fc6" class="cnblogs_code_hide">
<pre><span style="color: #000000;">var header = $api.byId('aui-header');
    if (header) {
        $api.fixStatusBar(header);
    }</span></pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('52a47ef4-2a86-4997-9395-77dabd3f0faa')"><img id="code_img_closed_52a47ef4-2a86-4997-9395-77dabd3f0faa" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_52a47ef4-2a86-4997-9395-77dabd3f0faa" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('52a47ef4-2a86-4997-9395-77dabd3f0faa',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_52a47ef4-2a86-4997-9395-77dabd3f0faa" class="cnblogs_code_hide">
<pre>无法跟config.xml里面的 <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">preference </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="statusBarAppearance"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">="false"</span> <span style="color: #0000ff;">/&gt;</span> 一起使用</pre>
</div>
<span class="cnblogs_code_collapse">注意</span></div>
<p>3，setStorage/getStorage</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('97a830ae-e8e2-4cf9-a879-2f05227d7202')"><img id="code_img_closed_97a830ae-e8e2-4cf9-a879-2f05227d7202" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_97a830ae-e8e2-4cf9-a879-2f05227d7202" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('97a830ae-e8e2-4cf9-a879-2f05227d7202',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_97a830ae-e8e2-4cf9-a879-2f05227d7202" class="cnblogs_code_hide">
<pre><span style="color: #000000;">//设置
$api.setStorage('user', {name:'hunter',sex:'男'});
//获取
var user=$api.getStorage('user');
var str= "姓名："+user.name+"；性别："+user.sex;</span></pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<p>4，JSON</p>
<p>JSON.parse(&lsquo;&rsquo;) 方法用于将一个 JSON 字符串转换为对象</p>
<p>JSON.stringify(data) 方法是将一个JavaScript值(对象或者数组)转换为一个 JSON字符串&nbsp;</p>
<p>5，win/frm传参</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('6a406d8c-a60f-4dff-a5c1-70cb007e1c05')"><img id="code_img_closed_6a406d8c-a60f-4dff-a5c1-70cb007e1c05" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_6a406d8c-a60f-4dff-a5c1-70cb007e1c05" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('6a406d8c-a60f-4dff-a5c1-70cb007e1c05',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_6a406d8c-a60f-4dff-a5c1-70cb007e1c05" class="cnblogs_code_hide">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">传入参数        </span>
<span style="color: #000000;">api.openWin({
        name: </span><span style="color: #800000;">'</span><span style="color: #800000;">prodetail_win</span><span style="color: #800000;">'</span><span style="color: #000000;">,
        url: </span><span style="color: #800000;">'</span><span style="color: #800000;">project/prodetail_win.html</span><span style="color: #800000;">'</span><span style="color: #000000;">,
        pageParam: {
            prj_id: id
        }
    });

接收参数
api.pageParam</span></pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<p>6，上传文件</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('1684eba9-ba74-44ec-b531-034226ba1526')"><img id="code_img_closed_1684eba9-ba74-44ec-b531-034226ba1526" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_1684eba9-ba74-44ec-b531-034226ba1526" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('1684eba9-ba74-44ec-b531-034226ba1526',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_1684eba9-ba74-44ec-b531-034226ba1526" class="cnblogs_code_hide">
<pre><span style="color: #000000;">function fnUpload(filepath, callback) {
    </span><span style="color: #0000ff;">var</span> files =<span style="color: #000000;"> [];
    </span><span style="color: #0000ff;">if</span> (<span style="color: #0000ff;">typeof</span>(filepath) == <span style="color: #800000;">'</span><span style="color: #800000;">string</span><span style="color: #800000;">'</span><span style="color: #000000;">) {
        files.push(filepath);
    } </span><span style="color: #0000ff;">else</span><span style="color: #000000;"> {
        files </span>=<span style="color: #000000;"> filepath
    }
    api.ajax({
        url: webpage </span>+ <span style="color: #800000;">'</span><span style="color: #800000;">/api/Sys/UploadFile</span><span style="color: #800000;">'</span><span style="color: #000000;">,
        method: </span><span style="color: #800000;">'</span><span style="color: #800000;">post</span><span style="color: #800000;">'</span><span style="color: #000000;">,
        data: {
            files: {
                </span><span style="color: #800000;">'</span><span style="color: #800000;">headimg</span><span style="color: #800000;">'</span><span style="color: #000000;">: files
            }
        }
    }, function(ret, err) {
        </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (ret) {
            </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (checktoken(ret.ret)) {
                </span><span style="color: #0000ff;">if</span> (ret.ret == <span style="color: #800080;">0</span><span style="color: #000000;">) {
                    callback(ret);
                } </span><span style="color: #0000ff;">else</span><span style="color: #000000;"> {
                    alertmsg(ret.msg);
                }
            }
        } </span><span style="color: #0000ff;">else</span><span style="color: #000000;"> {
            errormsg(err);
        }
    });
};</span></pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('ec06728f-d1c7-40e9-86c3-9c73cf1fdb0d')"><img id="code_img_closed_ec06728f-d1c7-40e9-86c3-9c73cf1fdb0d" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_ec06728f-d1c7-40e9-86c3-9c73cf1fdb0d" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('ec06728f-d1c7-40e9-86c3-9c73cf1fdb0d',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_ec06728f-d1c7-40e9-86c3-9c73cf1fdb0d" class="cnblogs_code_hide">
<pre> getOneImg(<span style="color: #800000;">'</span><span style="color: #800000;">camera</span><span style="color: #800000;">'</span>, <span style="color: #800000;">'</span><span style="color: #800000;">url</span><span style="color: #800000;">'</span><span style="color: #000000;">, function(result) {
                        </span><span style="color: #0000ff;">var</span> url =<span style="color: #000000;"> result.data;
                        fnUpload(url,function(res){
                            </span><span style="color: #0000ff;">if</span>(res.ret==<span style="color: #800080;">0</span><span style="color: #000000;">)VM.imgUrls.push(res.data)
                        })
                        </span><span style="color: #008000;">//</span><span style="color: #008000;">gouploadfile(url, dirpid);</span>
                     });</pre>
</div>
<span class="cnblogs_code_collapse">调用</span></div>
<p>7，调用相机或图库&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('040773fd-62d9-4004-98ee-26866f88b0fd')"><img id="code_img_closed_040773fd-62d9-4004-98ee-26866f88b0fd" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_040773fd-62d9-4004-98ee-26866f88b0fd" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('040773fd-62d9-4004-98ee-26866f88b0fd',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_040773fd-62d9-4004-98ee-26866f88b0fd" class="cnblogs_code_hide">
<pre><span style="color: #000000;">function getOneImg(sourceType, destinationType, callback) {
    </span><span style="color: #0000ff;">var</span> quality = <span style="color: #800080;">80</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">var</span> targetWidth = <span style="color: #800080;">800</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">var</span> targetHeight = <span style="color: #800080;">800</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">if</span> (api.systemType == <span style="color: #800000;">'</span><span style="color: #800000;">ios</span><span style="color: #800000;">'</span><span style="color: #000000;">) {
        quality </span>= <span style="color: #800080;">50</span><span style="color: #000000;">;
        targetWidth </span>= <span style="color: #800080;">500</span><span style="color: #000000;">;
        targetHeight </span>= <span style="color: #800080;">500</span><span style="color: #000000;">;
    }
    api.getPicture({
        sourceType: sourceType,
        encodingType: </span><span style="color: #800000;">'</span><span style="color: #800000;">jpg</span><span style="color: #800000;">'</span><span style="color: #000000;">,
        mediaValue: </span><span style="color: #800000;">'</span><span style="color: #800000;">pic</span><span style="color: #800000;">'</span><span style="color: #000000;">,
        destinationType: destinationType,
        quality: quality,
        targetWidth: targetWidth,
        targetHeight: targetHeight
    }, function(ret, err) {
        </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (ret) {
            </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (ret.data) {
                callback(ret);
            } </span><span style="color: #0000ff;">else</span><span style="color: #000000;"> {
                api.toast({
                    msg: </span><span style="color: #800000;">'</span><span style="color: #800000;">取消选择</span><span style="color: #800000;">'</span><span style="color: #000000;">
                });
            }
        } </span><span style="color: #0000ff;">else</span><span style="color: #000000;"> {
            </span><span style="color: #0000ff;">if</span> (err.msg === <span style="color: #800000;">'</span><span style="color: #800000;">user canceled</span><span style="color: #800000;">'</span><span style="color: #000000;">) {
                api.toast({
                    msg: </span><span style="color: #800000;">'</span><span style="color: #800000;">取消选择</span><span style="color: #800000;">'</span><span style="color: #000000;">
                });
            } </span><span style="color: #0000ff;">else</span><span style="color: #000000;"> {
                api.toast({
                    msg: </span><span style="color: #800000;">'</span><span style="color: #800000;">读取图片错误</span><span style="color: #800000;">'</span><span style="color: #000000;">
                });
            }
        }
    });
}</span></pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<p>8，多图选择</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('732acfe0-98c3-47e3-8048-904f7f632e36')"><img id="code_img_closed_732acfe0-98c3-47e3-8048-904f7f632e36" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_732acfe0-98c3-47e3-8048-904f7f632e36" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('732acfe0-98c3-47e3-8048-904f7f632e36',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_732acfe0-98c3-47e3-8048-904f7f632e36" class="cnblogs_code_hide">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">多图选择</span>
<span style="color: #000000;">function getImgsObj(max, callback) {
    </span><span style="color: #0000ff;">var</span> UIAlbumBrowser = api.require(<span style="color: #800000;">'</span><span style="color: #800000;">UIAlbumBrowser</span><span style="color: #800000;">'</span><span style="color: #000000;">);
    </span><span style="color: #0000ff;">var</span> fcolor = <span style="color: #800000;">'</span><span style="color: #800000;">#fff</span><span style="color: #800000;">'</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">if</span> (api.systemType == <span style="color: #800000;">'</span><span style="color: #800000;">ios</span><span style="color: #800000;">'</span><span style="color: #000000;">) {
        fcolor </span>= <span style="color: #800000;">'</span><span style="color: #800000;">#000</span><span style="color: #800000;">'</span><span style="color: #000000;">;
    }
    UIAlbumBrowser.open({
        max: max,
        type: </span><span style="color: #800000;">'</span><span style="color: #800000;">image</span><span style="color: #800000;">'</span><span style="color: #000000;">,
        styles: {
            bg: </span><span style="color: #800000;">'</span><span style="color: #800000;">#fff</span><span style="color: #800000;">'</span><span style="color: #000000;">,
            mark: {
                icon: </span><span style="color: #800000;">''</span><span style="color: #000000;">,
                position: </span><span style="color: #800000;">'</span><span style="color: #800000;">bottom_left</span><span style="color: #800000;">'</span><span style="color: #000000;">,
                size: </span><span style="color: #800080;">20</span><span style="color: #000000;">
            },
            nav: {
                bg: </span><span style="color: #800000;">'</span><span style="color: #800000;">#03a9f4</span><span style="color: #800000;">'</span><span style="color: #000000;">,
                titleColor: </span><span style="color: #800000;">'</span><span style="color: #800000;">#fff</span><span style="color: #800000;">'</span><span style="color: #000000;">,
                titleSize: </span><span style="color: #800080;">18</span><span style="color: #000000;">,
                cancelColor: </span><span style="color: #800000;">'</span><span style="color: #800000;">#fff</span><span style="color: #800000;">'</span><span style="color: #000000;">,
                cancelSize: </span><span style="color: #800080;">16</span><span style="color: #000000;">,
                finishColor: fcolor,
                finishSize: </span><span style="color: #800080;">16</span><span style="color: #000000;">
            }
        },
        rotation: </span><span style="color: #0000ff;">true</span><span style="color: #000000;">
    }, function(ret) {
        </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (ret) {
            </span><span style="color: #0000ff;">if</span> (ret.eventType == <span style="color: #800000;">'</span><span style="color: #800000;">confirm</span><span style="color: #800000;">'</span><span style="color: #000000;">) {
                </span><span style="color: #0000ff;">if</span> (!ret.list || ret.list.length &lt;= <span style="color: #800080;">0</span>) <span style="color: #0000ff;">return</span><span style="color: #000000;">;
                callback(ret);
            }
        }
    });
}</span></pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('00f5c243-cc41-4648-b2f4-f01593dbb086')"><img id="code_img_closed_00f5c243-cc41-4648-b2f4-f01593dbb086" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_00f5c243-cc41-4648-b2f4-f01593dbb086" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('00f5c243-cc41-4648-b2f4-f01593dbb086',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_00f5c243-cc41-4648-b2f4-f01593dbb086" class="cnblogs_code_hide">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">多图上传</span>
                        getImgsObj(<span style="color: #800080;">5</span><span style="color: #000000;">, function(res) {
                             showProgressMsg(</span><span style="color: #800000;">'</span><span style="color: #800000;">图片处理中</span><span style="color: #800000;">'</span><span style="color: #000000;">);
                             </span><span style="color: #0000ff;">var</span> index=<span style="color: #800080;">0</span><span style="color: #000000;">;
                             </span><span style="color: #0000ff;">var</span> total=<span style="color: #000000;">res.list.length;
                             </span><span style="color: #0000ff;">if</span>(api.systemType==<span style="color: #800000;">"</span><span style="color: #800000;">ios</span><span style="color: #800000;">"</span><span style="color: #000000;">)
                                {
                                    </span><span style="color: #0000ff;">for</span>(<span style="color: #0000ff;">var</span> i=<span style="color: #800080;">0</span>;i&lt;total;i++<span style="color: #000000;">)
                                    {
                                        </span><span style="color: #0000ff;">var</span> UIAlbumBrowser = api.require(<span style="color: #800000;">'</span><span style="color: #800000;">UIAlbumBrowser</span><span style="color: #800000;">'</span><span style="color: #000000;">);
                                        UIAlbumBrowser.transPath({
                                            path: res.list[i].path,
                                            scale: </span><span style="color: #800080;">0.1</span> <span style="color: #008000;">//</span><span style="color: #008000;">图片压缩 0~1.0</span>
<span style="color: #000000;">                                        }, function(rett, errr) {
                                            </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (rett) {
                                                fnUpload(rett.path,function(resss){
                                                    </span><span style="color: #0000ff;">if</span>(resss.ret==<span style="color: #800080;">0</span><span style="color: #000000;">)VM.imgUrls.push(resss.data);
                                                    </span><span style="color: #0000ff;">if</span>(++index==<span style="color: #000000;">total)api.hideProgress();
                                                })
                                            } </span><span style="color: #0000ff;">else</span><span style="color: #000000;"> {
                                                
                                            }
                                        });
                                    }
                                }
                                </span><span style="color: #0000ff;">else</span><span style="color: #000000;">
                                {
                                    </span><span style="color: #0000ff;">for</span>(<span style="color: #0000ff;">var</span> i=<span style="color: #800080;">0</span>;i&lt;res.list.length;i++<span style="color: #000000;">)
                                    {
                                        fnUpload(res.list[i].path,function(resss){
                                                </span><span style="color: #0000ff;">if</span>(resss.ret==<span style="color: #800080;">0</span><span style="color: #000000;">)VM.imgUrls.push(resss.data);
                                                </span><span style="color: #008000;">//</span><span style="color: #008000;">if(++index==total)api.hideProgress();</span>
<span style="color: #000000;">                                            })
                                    }
                                }
                                
                        });</span></pre>
</div>
<span class="cnblogs_code_collapse">调用</span></div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>五、AUI</p>
<p>1，aui-img-round设置图片为圆形</p>
<p>&nbsp;<span class="cnblogs_code"><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">img </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="../../image/2.0/scurity-yx.png"</span><span style="color: #ff0000;"> class</span><span style="color: #0000ff;">="aui-img-round aui-list-img-sm"</span><span style="color: #0000ff;">&gt;</span></span>&nbsp;</p>
<p>2，栅格系统</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('e5643753-f2ce-4eb0-b930-ceeb734fa986')"><img id="code_img_closed_e5643753-f2ce-4eb0-b930-ceeb734fa986" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_e5643753-f2ce-4eb0-b930-ceeb734fa986" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('e5643753-f2ce-4eb0-b930-ceeb734fa986',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_e5643753-f2ce-4eb0-b930-ceeb734fa986" class="cnblogs_code_hide">
<pre>    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="aui-content aui-content-padded"</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="aui-row aui-row-padded"</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="aui-col-xs-2"</span><span style="color: #0000ff;">&gt;</span>1<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="aui-col-xs-2"</span><span style="color: #0000ff;">&gt;</span>2<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="aui-col-xs-2"</span><span style="color: #0000ff;">&gt;</span>3<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="aui-col-xs-2"</span><span style="color: #0000ff;">&gt;</span>4<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<p>3，表单</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('9dc4c1cd-f010-41b1-ad10-5a68cd96cc94')"><img id="code_img_closed_9dc4c1cd-f010-41b1-ad10-5a68cd96cc94" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_9dc4c1cd-f010-41b1-ad10-5a68cd96cc94" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('9dc4c1cd-f010-41b1-ad10-5a68cd96cc94',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_9dc4c1cd-f010-41b1-ad10-5a68cd96cc94" class="cnblogs_code_hide">
<pre>        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="aui-content aui-margin-b-15"</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ul </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="aui-list aui-form-list"</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">li </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="aui-list-header"</span><span style="color: #0000ff;">&gt;</span>基本信息<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span>
                
                 <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">li </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="aui-list-item"</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="aui-list-item-inner"</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="aui-list-item-label"</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">
                            检查项目
                        </span><span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="aui-list-item-input"</span><span style="color: #0000ff;">&gt;</span>
                            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">select</span><span style="color: #0000ff;">&gt;</span>
                                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">option</span><span style="color: #0000ff;">&gt;</span>上海瓯云总部<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">option</span><span style="color: #0000ff;">&gt;</span>
                                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">option</span><span style="color: #0000ff;">&gt;</span>绿地集团<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">option</span><span style="color: #0000ff;">&gt;</span>
                            <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">select</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span>
                
                 <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">li </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="aui-list-item"</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="aui-list-item-inner"</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="aui-list-item-label"</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">
                            检查部件
                        </span><span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="aui-list-item-input"</span><span style="color: #0000ff;">&gt;</span>
                            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">select</span><span style="color: #0000ff;">&gt;</span>
                                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">option</span><span style="color: #0000ff;">&gt;</span>起重机1号<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">option</span><span style="color: #0000ff;">&gt;</span>
                            <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">select</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span>
                

            <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">ul</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<p>4，右边的图片加文字</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('be6dbef7-5e62-4881-85d8-df5eb2d62a33')"><img id="code_img_closed_be6dbef7-5e62-4881-85d8-df5eb2d62a33" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_be6dbef7-5e62-4881-85d8-df5eb2d62a33" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('be6dbef7-5e62-4881-85d8-df5eb2d62a33',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_be6dbef7-5e62-4881-85d8-df5eb2d62a33" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="aui-pull-right aui-list-item-media"</span><span style="color: #ff0000;"> style</span><span style="color: #0000ff;">="width:100px;display:flex;align-items: center;justify-content: center;"</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">img </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="../../image/2.0/saomiao.png"</span><span style="color: #ff0000;"> style</span><span style="color: #0000ff;">="width: 1.2rem"</span><span style="color: #ff0000;"> class</span><span style="color: #0000ff;">="aui-list-img-sm"</span> <span style="color: #0000ff;">/&gt;</span><span style="color: #000000;">开始扫描
                    </span><span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<p>5，图片文字一起居中</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('f533f211-f9e0-472b-b848-92f8863b5abf')"><img id="code_img_closed_f533f211-f9e0-472b-b848-92f8863b5abf" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_f533f211-f9e0-472b-b848-92f8863b5abf" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('f533f211-f9e0-472b-b848-92f8863b5abf',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_f533f211-f9e0-472b-b848-92f8863b5abf" class="cnblogs_code_hide">
<pre><span style="color: #800000;">.box</span>{<span style="color: #ff0000;">
        display</span>:<span style="color: #0000ff;">flex</span>;<span style="color: #ff0000;">
        align-items</span>:<span style="color: #0000ff;"> center</span>;<span style="color: #ff0000;">//子元素垂直居中
        justify-content</span>:<span style="color: #0000ff;"> center</span>;<span style="color: #ff0000;">//子元素水平居中
</span>}</pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<p>6，加上&gt;箭头</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('6ff869b1-5c2a-42d5-b3c3-fd46079ad1b2')"><img id="code_img_closed_6ff869b1-5c2a-42d5-b3c3-fd46079ad1b2" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_6ff869b1-5c2a-42d5-b3c3-fd46079ad1b2" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('6ff869b1-5c2a-42d5-b3c3-fd46079ad1b2',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_6ff869b1-5c2a-42d5-b3c3-fd46079ad1b2" class="cnblogs_code_hide">
<pre> &lt;div <span style="color: #0000ff;">class</span>=<span style="color: #800000;">"</span><span style="color: #800000;">aui-list-item-inner aui-list-item-arrow</span><span style="color: #800000;">"</span>&gt;
                        &lt;div <span style="color: #0000ff;">class</span>=<span style="color: #800000;">"</span><span style="color: #800000;">aui-list-item-label</span><span style="color: #800000;">"</span>&gt;<span style="color: #000000;">
                            子领域
                        </span>&lt;/div&gt;
                        &lt;div <span style="color: #0000ff;">class</span>=<span style="color: #800000;">"</span><span style="color: #800000;">aui-list-item-input</span><span style="color: #800000;">"</span>&gt;
                            &lt;<span style="color: #0000ff;">select</span> v-model=<span style="color: #800000;">"</span><span style="color: #800000;">frmData.subdoman</span><span style="color: #800000;">"</span> tapmodel onchange=<span style="color: #800000;">"</span><span style="color: #800000;">getZgxwt()</span><span style="color: #800000;">"</span>&gt;
                                &lt;option v-<span style="color: #0000ff;">for</span>=<span style="color: #800000;">"</span><span style="color: #800000;">item in subDomains</span><span style="color: #800000;">"</span> v-bind:value=<span style="color: #800000;">"</span><span style="color: #800000;">item.id</span><span style="color: #800000;">"</span>&gt;{{item.content}}&lt;/option&gt;
                            &lt;/<span style="color: #0000ff;">select</span>&gt;
                        &lt;/div&gt;
                    &lt;/div&gt;</pre>
</div>
<span class="cnblogs_code_collapse">aui-list-item-arrow</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('8e494f97-606d-4c91-b98e-db9db3e79340')"><img id="code_img_closed_8e494f97-606d-4c91-b98e-db9db3e79340" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_8e494f97-606d-4c91-b98e-db9db3e79340" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('8e494f97-606d-4c91-b98e-db9db3e79340',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_8e494f97-606d-4c91-b98e-db9db3e79340" class="cnblogs_code_hide">
<pre> &lt;li <span style="color: #0000ff;">class</span>=<span style="color: #800000;">"</span><span style="color: #800000;">aui-list-item</span><span style="color: #800000;">"</span> onclick=<span style="color: #800000;">"</span><span style="color: #800000;">add('contacts')</span><span style="color: #800000;">"</span>&gt;
                &lt;div <span style="color: #0000ff;">class</span>=<span style="color: #800000;">"</span><span style="color: #800000;">aui-list-item-label-icon</span><span style="color: #800000;">"</span>&gt;
                    &lt;i <span style="color: #0000ff;">class</span>=<span style="color: #800000;">"</span><span style="color: #800000;">aui-iconfont aui-icon-mobile</span><span style="color: #800000;">"</span>&gt;&lt;/i&gt;
                &lt;/div&gt;
                &lt;div <span style="color: #0000ff;">class</span>=<span style="color: #800000;">"</span><span style="color: #800000;">aui-list-item-inner aui-list-item-arrow</span><span style="color: #800000;">"</span>&gt;
                    &lt;div <span style="color: #0000ff;">class</span>=<span style="color: #800000;">"</span><span style="color: #800000;">aui-list-item-title</span><span style="color: #800000;">"</span>&gt;选择手机联系人&lt;/div&gt;
                    &lt;div <span style="color: #0000ff;">class</span>=<span style="color: #800000;">"</span><span style="color: #800000;">aui-list-item-right</span><span style="color: #800000;">"</span>&gt;无需审核&lt;/div&gt;
                &lt;/div&gt;
            &lt;/li&gt;</pre>
</div>
<span class="cnblogs_code_collapse">带图标</span></div>
<p>7，图片加圆形边框&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('2fbe849f-4cf3-4cba-9384-75c26311c786')"><img id="code_img_closed_2fbe849f-4cf3-4cba-9384-75c26311c786" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_2fbe849f-4cf3-4cba-9384-75c26311c786" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('2fbe849f-4cf3-4cba-9384-75c26311c786',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_2fbe849f-4cf3-4cba-9384-75c26311c786" class="cnblogs_code_hide">
<pre>&lt;img src=<span style="color: #800000;">"</span><span style="color: #800000;">../../image/demo5.png</span><span style="color: #800000;">"</span> <span style="color: #0000ff;">class</span>=<span style="color: #800000;">"</span><span style="color: #800000;">aui-img-round aui-list-img-sm</span><span style="color: #800000;">"</span>&gt;</pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>六、第三方插件</p>
<p>1，datetime</p>
<p>插件下载：<a href="https://pan.baidu.com/s/18fG4M3k72PEPUEE-9e4QCg" target="_blank">https://pan.baidu.com/s/18fG4M3k72PEPUEE-9e4QCg</a></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('6dbb8838-8133-46d9-81b5-3d98a10169b3')"><img id="code_img_closed_6dbb8838-8133-46d9-81b5-3d98a10169b3" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_6dbb8838-8133-46d9-81b5-3d98a10169b3" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('6dbb8838-8133-46d9-81b5-3d98a10169b3',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_6dbb8838-8133-46d9-81b5-3d98a10169b3" class="cnblogs_code_hide">
<pre>&lt;link rel=<span style="color: #800000;">"</span><span style="color: #800000;">stylesheet</span><span style="color: #800000;">"</span> type=<span style="color: #800000;">"</span><span style="color: #800000;">text/css</span><span style="color: #800000;">"</span> href=<span style="color: #800000;">"</span><span style="color: #800000;">../../script/datetime/mobiscroll.javascript.min.css</span><span style="color: #800000;">"</span> /&gt;

&lt;script type=<span style="color: #800000;">"</span><span style="color: #800000;">text/javascript</span><span style="color: #800000;">"</span> src=<span style="color: #800000;">"</span><span style="color: #800000;">../../script/datetime/mobiscroll.javascript.min.js</span><span style="color: #800000;">"</span>&gt;&lt;/script&gt;</pre>
</div>
<span class="cnblogs_code_collapse">引用js和css文件</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('198bb500-a26c-47d0-b05a-280644be7805')"><img id="code_img_closed_198bb500-a26c-47d0-b05a-280644be7805" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_198bb500-a26c-47d0-b05a-280644be7805" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('198bb500-a26c-47d0-b05a-280644be7805',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_198bb500-a26c-47d0-b05a-280644be7805" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="text"</span><span style="color: #ff0000;"> placeholder</span><span style="color: #0000ff;">="选择时间"</span><span style="color: #ff0000;"> readonly</span><span style="color: #0000ff;">="readonly"</span><span style="color: #ff0000;"> v-model</span><span style="color: #0000ff;">="frmData.xjdate"</span><span style="color: #ff0000;"> id</span><span style="color: #0000ff;">="startday"</span><span style="color: #0000ff;">/&gt;</span><span style="color: #000000;"> 

function datatimeInit() {
    mobiscroll.datetime('#startday', {
        lang: 'zh',
        display: 'bottom',
        dateFormat: 'yy-mm-dd',
        timeFormat: 'hh:ii',
        onBeforeShow: function(event, inst) {
            api.setFrameAttr({
                name: api.frameName,
                bounces: false
            });
        },
        onBeforeClose: function(event, inst) {
            api.setFrameAttr({
                name: api.frameName,
                bounces: true
            });
        },
        onSet: function(event, inst) {
            if(event.valueText)$api.val($api.byId('startday'), event.valueText);
        }
    });
}</span></pre>
</div>
<span class="cnblogs_code_collapse">datatimeInit</span></div>
<p>2，多级选择器UIActionSelector</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('95e87731-e141-427b-8261-950375f69d6e')"><img id="code_img_closed_95e87731-e141-427b-8261-950375f69d6e" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_95e87731-e141-427b-8261-950375f69d6e" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('95e87731-e141-427b-8261-950375f69d6e',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_95e87731-e141-427b-8261-950375f69d6e" class="cnblogs_code_hide">
<pre><span style="color: #008000;">/*</span><span style="color: #008000;">* 多级数据选择器 </span><span style="color: #008000;">*/</span><span style="color: #000000;">
function fnOpenActionSelector(itemsData, callback, num) {
    api.setFrameAttr({
        name: api.frameName,
        bounces: </span><span style="color: #0000ff;">false</span><span style="color: #000000;">
    });
    </span><span style="color: #0000ff;">var</span> colnum = <span style="color: #800080;">1</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (num) {
        colnum </span>=<span style="color: #000000;"> num;
    }
    </span><span style="color: #0000ff;">var</span> UIActionSelector = api.require(<span style="color: #800000;">'</span><span style="color: #800000;">UIActionSelector</span><span style="color: #800000;">'</span><span style="color: #000000;">);
    UIActionSelector.open({
        datas: itemsData,
        layout: {
            row: </span><span style="color: #800080;">5</span><span style="color: #000000;">,
            col: colnum,
            height: </span><span style="color: #800080;">30</span><span style="color: #000000;">,
            size: </span><span style="color: #800080;">14</span><span style="color: #000000;">,
            sizeActive: </span><span style="color: #800080;">14</span><span style="color: #000000;">,
            maskBg: </span><span style="color: #800000;">'</span><span style="color: #800000;">rgba(0,0,0,0.2)</span><span style="color: #800000;">'</span><span style="color: #000000;">,
            bg: </span><span style="color: #800000;">'</span><span style="color: #800000;">#fff</span><span style="color: #800000;">'</span><span style="color: #000000;">,
            color: </span><span style="color: #800000;">'</span><span style="color: #800000;">#888</span><span style="color: #800000;">'</span><span style="color: #000000;">,
            colorActive: </span><span style="color: #800000;">'</span><span style="color: #800000;">#f00</span><span style="color: #800000;">'</span><span style="color: #000000;">,
            colorSelected: </span><span style="color: #800000;">'</span><span style="color: #800000;">#f00</span><span style="color: #800000;">'</span><span style="color: #000000;">
        },
        animation: </span><span style="color: #0000ff;">true</span><span style="color: #000000;">,
        cancel: {
            text: </span><span style="color: #800000;">'</span><span style="color: #800000;">取消</span><span style="color: #800000;">'</span><span style="color: #000000;">,
            size: </span><span style="color: #800080;">14</span><span style="color: #000000;">,
            w: </span><span style="color: #800080;">90</span><span style="color: #000000;">,
            h: </span><span style="color: #800080;">44</span><span style="color: #000000;">,
            bg: </span><span style="color: #800000;">'</span><span style="color: #800000;">transparent</span><span style="color: #800000;">'</span><span style="color: #000000;">,
            bgActive: </span><span style="color: #800000;">'</span><span style="color: #800000;">transparent</span><span style="color: #800000;">'</span><span style="color: #000000;">,
            color: </span><span style="color: #800000;">'</span><span style="color: #800000;">#888</span><span style="color: #800000;">'</span><span style="color: #000000;">,
            colorActive: </span><span style="color: #800000;">'</span><span style="color: #800000;">#888</span><span style="color: #800000;">'</span><span style="color: #000000;">
        },
        ok: {
            text: </span><span style="color: #800000;">'</span><span style="color: #800000;">确定</span><span style="color: #800000;">'</span><span style="color: #000000;">,
            size: </span><span style="color: #800080;">14</span><span style="color: #000000;">,
            w: </span><span style="color: #800080;">90</span><span style="color: #000000;">,
            h: </span><span style="color: #800080;">44</span><span style="color: #000000;">,
            bg: </span><span style="color: #800000;">'</span><span style="color: #800000;">transparent</span><span style="color: #800000;">'</span><span style="color: #000000;">,
            bgActive: </span><span style="color: #800000;">'</span><span style="color: #800000;">transparent</span><span style="color: #800000;">'</span><span style="color: #000000;">,
            color: </span><span style="color: #800000;">'</span><span style="color: #800000;">#03a9f4</span><span style="color: #800000;">'</span><span style="color: #000000;">,
            colorActive: </span><span style="color: #800000;">'</span><span style="color: #800000;">#03a9f4</span><span style="color: #800000;">'</span><span style="color: #000000;">
        },
        title: {
            text: </span><span style="color: #800000;">''</span><span style="color: #000000;">,
            size: </span><span style="color: #800080;">14</span><span style="color: #000000;">,
            h: </span><span style="color: #800080;">44</span><span style="color: #000000;">,
            bg: </span><span style="color: #800000;">'</span><span style="color: #800000;">#fff</span><span style="color: #800000;">'</span><span style="color: #000000;">,
            color: </span><span style="color: #800000;">'</span><span style="color: #800000;">#888</span><span style="color: #800000;">'</span><span style="color: #000000;">
        },
        fixedOn: api.frameName
    }, function(ret, err) {
        api.setFrameAttr({
            name: api.frameName,
            bounces: </span><span style="color: #0000ff;">true</span><span style="color: #000000;">
        });
        </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (ret) {
            </span><span style="color: #0000ff;">if</span> (ret.eventType == <span style="color: #800000;">'</span><span style="color: #800000;">cancel</span><span style="color: #800000;">'</span><span style="color: #000000;">) {
                UIActionSelector.close();
                </span><span style="color: #0000ff;">return</span><span style="color: #000000;">;
            }
            callback(ret);
        } </span><span style="color: #0000ff;">else</span><span style="color: #000000;"> {
            errormsg(JSON.stringify(err));
        }
    })
}</span></pre>
</div>
<span class="cnblogs_code_collapse">封装代码</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('514bd1e9-bed1-49df-a7fa-72de1906a8c7')"><img id="code_img_closed_514bd1e9-bed1-49df-a7fa-72de1906a8c7" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_514bd1e9-bed1-49df-a7fa-72de1906a8c7" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('514bd1e9-bed1-49df-a7fa-72de1906a8c7',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_514bd1e9-bed1-49df-a7fa-72de1906a8c7" class="cnblogs_code_hide">
<pre>&lt;div <span style="color: #0000ff;">class</span>=<span style="color: #800000;">"</span><span style="color: #800000;">aui-list-item-inner aui-list-item-arrow</span><span style="color: #800000;">"</span> tapmode onclick=<span style="color: #800000;">"</span><span style="color: #800000;">getPrimaryDomain()</span><span style="color: #800000;">"</span>&gt;
                        &lt;div <span style="color: #0000ff;">class</span>=<span style="color: #800000;">"</span><span style="color: #800000;">aui-list-item-label</span><span style="color: #800000;">"</span>&gt;<span style="color: #000000;">
                            主领域
                        </span>&lt;/div&gt;
                        &lt;div <span style="color: #0000ff;">class</span>=<span style="color: #800000;">"</span><span style="color: #800000;">aui-list-item-input</span><span style="color: #800000;">"</span>&gt;
                            &lt;input type=<span style="color: #800000;">"</span><span style="color: #800000;">text</span><span style="color: #800000;">"</span> <span style="color: #0000ff;">readonly</span>=<span style="color: #800000;">"</span><span style="color: #800000;">readonly</span><span style="color: #800000;">"</span> v-model=<span style="color: #800000;">"</span><span style="color: #800000;">frmData.primarydoman</span><span style="color: #800000;">"</span>&gt;
                            &lt;!-- &lt;<span style="color: #0000ff;">select</span> v-model=<span style="color: #800000;">"</span><span style="color: #800000;">frmData.primarydoman</span><span style="color: #800000;">"</span> tapmode onchange=<span style="color: #800000;">"</span><span style="color: #800000;">getSubDomain()</span><span style="color: #800000;">"</span>&gt;
                                &lt;option v-<span style="color: #0000ff;">for</span>=<span style="color: #800000;">"</span><span style="color: #800000;">item in primaryDomains</span><span style="color: #800000;">"</span> v-bind:value=<span style="color: #800000;">"</span><span style="color: #800000;">item.id</span><span style="color: #800000;">"</span>&gt;{{item.content}}&lt;/option&gt;
                            &lt;/<span style="color: #0000ff;">select</span>&gt; --&gt;
                        &lt;/div&gt;
                    &lt;/div&gt;</pre>
</div>
<span class="cnblogs_code_collapse">页面代码</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('7bb48950-e8c9-4b60-8858-d82befbbf650')"><img id="code_img_closed_7bb48950-e8c9-4b60-8858-d82befbbf650" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_7bb48950-e8c9-4b60-8858-d82befbbf650" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('7bb48950-e8c9-4b60-8858-d82befbbf650',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_7bb48950-e8c9-4b60-8858-d82befbbf650" class="cnblogs_code_hide">
<pre>function getPrimaryDomain(){<span style="color: #008000;">//</span><span style="color: #008000;">获取主领域</span>
    getCommonDomain(<span style="color: #800080;">1</span><span style="color: #000000;">,function(data){
        fnOpenActionSelector(data, function(ret) {
            </span><span style="color: #0000ff;">if</span>(ret.eventType==<span style="color: #800000;">"</span><span style="color: #800000;">ok</span><span style="color: #800000;">"</span><span style="color: #000000;">)
            {
                </span><span style="color: #0000ff;">var</span> info=ret.selectedInfo[<span style="color: #800080;">0</span><span style="color: #000000;">];
                VM.frmData.primarydoman</span>=<span style="color: #000000;"> info.name;
                VM.frmData.primarydomanid</span>=<span style="color: #000000;"> info.value;
                VM.frmData.subdoman</span>= <span style="color: #800000;">''</span><span style="color: #000000;">;
                VM.frmData.zgxwt</span>= <span style="color: #800000;">''</span><span style="color: #000000;">;
            }
         })
    });
}
function getCommonDomain(param,callback)
{
    console.log(</span><span style="color: #800000;">"</span><span style="color: #800000;">getCommonDomain</span><span style="color: #800000;">"</span><span style="color: #000000;">)
     fnPost(</span><span style="color: #800000;">'</span><span style="color: #800000;">/api/ProjectHazard/GetHazardList</span><span style="color: #800000;">'</span>, {parameter:param}, <span style="color: #800000;">'</span><span style="color: #800000;">application/json;charset=utf-8</span><span style="color: #800000;">'</span>, <span style="color: #0000ff;">true</span><span style="color: #000000;">, function(ret, err) {
                    </span><span style="color: #0000ff;">var</span><span style="color: #000000;"> data;
                    </span><span style="color: #0000ff;">if</span>(ret.ret==<span style="color: #800080;">0</span>&amp;&amp;ret.data!=<span style="color: #0000ff;">null</span>&amp;&amp;ret.data.length&gt;<span style="color: #800080;">0</span><span style="color: #000000;">)
                    {
                        data</span>=<span style="color: #0000ff;">new</span><span style="color: #000000;"> Array();
                        </span><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">var</span> i = ret.data.length - <span style="color: #800080;">1</span>; i &gt;= <span style="color: #800080;">0</span>; i--<span style="color: #000000;">) {
                            
                            data.push({</span><span style="color: #800000;">"</span><span style="color: #800000;">name</span><span style="color: #800000;">"</span>:ret.data[i].content,<span style="color: #800000;">"</span><span style="color: #800000;">value</span><span style="color: #800000;">"</span><span style="color: #000000;">:ret.data[i].id})
                        }
                    }
                    </span><span style="color: #0000ff;">if</span><span style="color: #000000;">(callback)
                    {
                        callback(data)
                    }
                },</span><span style="color: #0000ff;">false</span>,<span style="color: #800000;">""</span><span style="color: #000000;">);
}</span></pre>
</div>
<span class="cnblogs_code_collapse">调用代码</span></div>
<p>3，mescroll下拉上拉组件</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('5edab5f1-f99f-4a46-b0e4-a952085e2cf0')"><img id="code_img_closed_5edab5f1-f99f-4a46-b0e4-a952085e2cf0" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_5edab5f1-f99f-4a46-b0e4-a952085e2cf0" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('5edab5f1-f99f-4a46-b0e4-a952085e2cf0',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_5edab5f1-f99f-4a46-b0e4-a952085e2cf0" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">&lt;!</span><span style="color: #ff00ff;">DOCTYPE HTML</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">html</span><span style="color: #0000ff;">&gt;</span>

<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">head</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">meta </span><span style="color: #ff0000;">charset</span><span style="color: #0000ff;">="utf-8"</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">meta </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="viewport"</span><span style="color: #ff0000;"> content</span><span style="color: #0000ff;">="maximum-scale=1.0, minimum-scale=1.0, user-scalable=0, initial-scale=1.0, width=device-width"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">meta </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="format-detection"</span><span style="color: #ff0000;"> content</span><span style="color: #0000ff;">="telephone=no, email=no, date=no, address=no"</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">title</span><span style="color: #0000ff;">&gt;</span>瓯云APP<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">title</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">link </span><span style="color: #ff0000;">rel</span><span style="color: #0000ff;">="stylesheet"</span><span style="color: #ff0000;"> type</span><span style="color: #0000ff;">="text/css"</span><span style="color: #ff0000;"> href</span><span style="color: #0000ff;">="../../css/api.css"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">link </span><span style="color: #ff0000;">rel</span><span style="color: #0000ff;">="stylesheet"</span><span style="color: #ff0000;"> type</span><span style="color: #0000ff;">="text/css"</span><span style="color: #ff0000;"> href</span><span style="color: #0000ff;">="../../css/aui.css"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">link </span><span style="color: #ff0000;">rel</span><span style="color: #0000ff;">="stylesheet"</span><span style="color: #ff0000;"> type</span><span style="color: #0000ff;">="text/css"</span><span style="color: #ff0000;"> href</span><span style="color: #0000ff;">="../../css/style.css"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">link </span><span style="color: #ff0000;">rel</span><span style="color: #0000ff;">="stylesheet"</span><span style="color: #ff0000;"> type</span><span style="color: #0000ff;">="text/css"</span><span style="color: #ff0000;"> href</span><span style="color: #0000ff;">="../../script/mescroll/mescroll.min.css"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">style</span><span style="color: #0000ff;">&gt;</span><span style="background-color: #f5f5f5; color: #800000;">
        .div-top</span><span style="background-color: #f5f5f5; color: #000000;">{</span><span style="background-color: #f5f5f5; color: #ff0000;">
            background-color</span><span style="background-color: #f5f5f5; color: #000000;">:</span><span style="background-color: #f5f5f5; color: #0000ff;"> #FCFCFC</span><span style="background-color: #f5f5f5; color: #000000;">;</span>
        <span style="background-color: #f5f5f5; color: #000000;">}</span><span style="background-color: #f5f5f5; color: #800000;">
        .type-button</span><span style="background-color: #f5f5f5; color: #000000;">{</span><span style="background-color: #f5f5f5; color: #ff0000;">
            text-align</span><span style="background-color: #f5f5f5; color: #000000;">:</span><span style="background-color: #f5f5f5; color: #0000ff;"> center</span><span style="background-color: #f5f5f5; color: #000000;">;</span><span style="background-color: #f5f5f5; color: #ff0000;">
            height</span><span style="background-color: #f5f5f5; color: #000000;">:</span><span style="background-color: #f5f5f5; color: #0000ff;"> 40px</span><span style="background-color: #f5f5f5; color: #000000;">;</span><span style="background-color: #f5f5f5; color: #ff0000;">
            line-height</span><span style="background-color: #f5f5f5; color: #000000;">:</span><span style="background-color: #f5f5f5; color: #0000ff;"> 40px</span><span style="background-color: #f5f5f5; color: #000000;">;</span>
        <span style="background-color: #f5f5f5; color: #000000;">}</span><span style="background-color: #f5f5f5; color: #800000;">
        .type-active</span><span style="background-color: #f5f5f5; color: #000000;">{</span><span style="background-color: #f5f5f5; color: #ff0000;">
            color</span><span style="background-color: #f5f5f5; color: #000000;">:</span><span style="background-color: #f5f5f5; color: #0000ff;"> #88B459</span><span style="background-color: #f5f5f5; color: #000000;">;</span><span style="background-color: #f5f5f5; color: #ff0000;">
            border-bottom-style</span><span style="background-color: #f5f5f5; color: #000000;">:</span><span style="background-color: #f5f5f5; color: #0000ff;">solid</span><span style="background-color: #f5f5f5; color: #000000;">;</span><span style="background-color: #f5f5f5; color: #ff0000;">
            border-bottom-color</span><span style="background-color: #f5f5f5; color: #000000;">:</span><span style="background-color: #f5f5f5; color: #0000ff;">#88B459</span><span style="background-color: #f5f5f5; color: #000000;">;</span><span style="background-color: #f5f5f5; color: #ff0000;">
            border-bottom-width</span><span style="background-color: #f5f5f5; color: #000000;">:</span><span style="background-color: #f5f5f5; color: #0000ff;"> 3px</span><span style="background-color: #f5f5f5; color: #000000;">;</span><span style="background-color: #f5f5f5; color: #ff0000;">
            width</span><span style="background-color: #f5f5f5; color: #000000;">:</span><span style="background-color: #f5f5f5; color: #0000ff;"> 50%</span><span style="background-color: #f5f5f5; color: #000000;">;</span><span style="background-color: #f5f5f5; color: #ff0000;"> 
            margin</span><span style="background-color: #f5f5f5; color: #000000;">:</span><span style="background-color: #f5f5f5; color: #0000ff;"> auto</span><span style="background-color: #f5f5f5; color: #000000;">;</span><span style="background-color: #f5f5f5; color: #ff0000;"> 
            height</span><span style="background-color: #f5f5f5; color: #000000;">:</span><span style="background-color: #f5f5f5; color: #0000ff;"> 5px</span><span style="background-color: #f5f5f5; color: #000000;">;</span>
        <span style="background-color: #f5f5f5; color: #000000;">}</span><span style="background-color: #f5f5f5; color: #800000;">
        .type-fgx</span><span style="background-color: #f5f5f5; color: #000000;">{</span><span style="background-color: #f5f5f5; color: #ff0000;">
            height</span><span style="background-color: #f5f5f5; color: #000000;">:</span><span style="background-color: #f5f5f5; color: #0000ff;">40px</span><span style="background-color: #f5f5f5; color: #000000;">;</span><span style="background-color: #f5f5f5; color: #ff0000;">
            line-height</span><span style="background-color: #f5f5f5; color: #000000;">:</span><span style="background-color: #f5f5f5; color: #0000ff;"> 40px</span><span style="background-color: #f5f5f5; color: #000000;">;</span><span style="background-color: #f5f5f5; color: #ff0000;">
            float</span><span style="background-color: #f5f5f5; color: #000000;">:</span><span style="background-color: #f5f5f5; color: #0000ff;">left</span><span style="background-color: #f5f5f5; color: #000000;">;</span>
        <span style="background-color: #f5f5f5; color: #000000;">}</span><span style="background-color: #f5f5f5; color: #800000;">
        .type-fgx span</span><span style="background-color: #f5f5f5; color: #000000;">{</span><span style="background-color: #f5f5f5; color: #ff0000;">
            color</span><span style="background-color: #f5f5f5; color: #000000;">:</span><span style="background-color: #f5f5f5; color: #0000ff;"> #E3E3E3
        </span><span style="background-color: #f5f5f5; color: #000000;">}</span><span style="background-color: #f5f5f5; color: #800000;">

        .aui-media-list</span><span style="background-color: #f5f5f5; color: #000000;">{</span><span style="background-color: #f5f5f5; color: #ff0000;">
            border</span><span style="background-color: #f5f5f5; color: #000000;">:</span><span style="background-color: #f5f5f5; color: #0000ff;">1px solid #E4E4E4</span><span style="background-color: #f5f5f5; color: #000000;">;</span><span style="background-color: #f5f5f5; color: #ff0000;">
            border-radius</span><span style="background-color: #f5f5f5; color: #000000;">:</span><span style="background-color: #f5f5f5; color: #0000ff;">5px</span><span style="background-color: #f5f5f5; color: #000000;">;</span><span style="background-color: #f5f5f5; color: #ff0000;">
            -moz-border-radius</span><span style="background-color: #f5f5f5; color: #000000;">:</span><span style="background-color: #f5f5f5; color: #0000ff;">5px</span><span style="background-color: #f5f5f5; color: #000000;">;</span> <span style="background-color: #f5f5f5; color: #008000;">/*</span><span style="background-color: #f5f5f5; color: #008000;"> Old Firefox </span><span style="background-color: #f5f5f5; color: #008000;">*/</span><span style="background-color: #f5f5f5; color: #ff0000;">
            margin</span><span style="background-color: #f5f5f5; color: #000000;">:</span><span style="background-color: #f5f5f5; color: #0000ff;"> 10px</span><span style="background-color: #f5f5f5; color: #000000;">;</span>
        <span style="background-color: #f5f5f5; color: #000000;">}</span><span style="background-color: #f5f5f5; color: #800000;">

        .img-right</span><span style="background-color: #f5f5f5; color: #000000;">{</span><span style="background-color: #f5f5f5; color: #ff0000;">
            float</span><span style="background-color: #f5f5f5; color: #000000;">:</span><span style="background-color: #f5f5f5; color: #0000ff;"> right</span><span style="background-color: #f5f5f5; color: #000000;">;</span><span style="background-color: #f5f5f5; color: #ff0000;">
            display</span><span style="background-color: #f5f5f5; color: #000000;">:</span><span style="background-color: #f5f5f5; color: #0000ff;"> inline</span><span style="background-color: #f5f5f5; color: #000000;">;</span><span style="background-color: #f5f5f5; color: #ff0000;">
            margin-bottom</span><span style="background-color: #f5f5f5; color: #000000;">:</span><span style="background-color: #f5f5f5; color: #0000ff;"> auto</span><span style="background-color: #f5f5f5; color: #000000;">;</span><span style="background-color: #f5f5f5; color: #ff0000;">
            margin-top</span><span style="background-color: #f5f5f5; color: #000000;">:</span><span style="background-color: #f5f5f5; color: #0000ff;"> auto</span><span style="background-color: #f5f5f5; color: #000000;">;</span><span style="background-color: #f5f5f5; color: #ff0000;">
            margin-right</span><span style="background-color: #f5f5f5; color: #000000;">:</span><span style="background-color: #f5f5f5; color: #0000ff;"> 10px</span><span style="background-color: #f5f5f5; color: #000000;">;</span>
        <span style="background-color: #f5f5f5; color: #000000;">}</span><span style="background-color: #f5f5f5; color: #800000;">
        
        .div-status</span><span style="background-color: #f5f5f5; color: #000000;">{</span><span style="background-color: #f5f5f5; color: #ff0000;">
            color</span><span style="background-color: #f5f5f5; color: #000000;">:</span><span style="background-color: #f5f5f5; color: #0000ff;">#FFFFFF</span><span style="background-color: #f5f5f5; color: #000000;">;</span><span style="background-color: #f5f5f5; color: #ff0000;">
            background-color</span><span style="background-color: #f5f5f5; color: #000000;">:</span><span style="background-color: #f5f5f5; color: #0000ff;"> #87B453</span><span style="background-color: #f5f5f5; color: #000000;">;</span><span style="background-color: #f5f5f5; color: #ff0000;">
            border-radius</span><span style="background-color: #f5f5f5; color: #000000;">:</span><span style="background-color: #f5f5f5; color: #0000ff;">5px</span><span style="background-color: #f5f5f5; color: #000000;">;</span><span style="background-color: #f5f5f5; color: #ff0000;">
            -moz-border-radius</span><span style="background-color: #f5f5f5; color: #000000;">:</span><span style="background-color: #f5f5f5; color: #0000ff;">5px</span><span style="background-color: #f5f5f5; color: #000000;">;</span> <span style="background-color: #f5f5f5; color: #008000;">/*</span><span style="background-color: #f5f5f5; color: #008000;"> Old Firefox </span><span style="background-color: #f5f5f5; color: #008000;">*/</span><span style="background-color: #f5f5f5; color: #ff0000;">
            display</span><span style="background-color: #f5f5f5; color: #000000;">:</span><span style="background-color: #f5f5f5; color: #0000ff;"> inline-block</span><span style="background-color: #f5f5f5; color: #000000;">;</span>
        <span style="background-color: #f5f5f5; color: #000000;">}</span>

    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">style</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">head</span><span style="color: #0000ff;">&gt;</span>

<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">body</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">id</span><span style="color: #0000ff;">="app"</span><span style="color: #ff0000;"> v-cloak class</span><span style="color: #0000ff;">="mescroll"</span><span style="color: #0000ff;">&gt;</span>
    
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="aui-row div-top"</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="aui-col-5"</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ul</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="type-button"</span><span style="color: #ff0000;"> tapmode onclick</span><span style="color: #0000ff;">="getInspectionList('待办')"</span><span style="color: #0000ff;">&gt;</span>待办<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">li </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="type-active"</span><span style="color: #ff0000;"> v-if</span><span style="color: #0000ff;">="frmData.type=='待办'"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">ul</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="aui-col-5"</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ul</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="type-fgx"</span><span style="color: #0000ff;">&gt;&lt;</span><span style="color: #800000;">span</span><span style="color: #0000ff;">&gt;</span>|<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">span</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="type-button"</span><span style="color: #ff0000;"> tapmode onclick</span><span style="color: #0000ff;">="getInspectionList('处理中')"</span><span style="color: #0000ff;">&gt;</span>处理中<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">li </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="type-active"</span><span style="color: #ff0000;"> v-if</span><span style="color: #0000ff;">="frmData.type=='处理中'"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">ul</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="aui-col-5"</span><span style="color: #0000ff;">&gt;</span>
             <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ul</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="type-fgx"</span><span style="color: #0000ff;">&gt;&lt;</span><span style="color: #800000;">span</span><span style="color: #0000ff;">&gt;</span>|<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">span</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="type-button"</span><span style="color: #ff0000;"> tapmode onclick</span><span style="color: #0000ff;">="getInspectionList('通过')"</span><span style="color: #0000ff;">&gt;</span>通过<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">li </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="type-active"</span><span style="color: #ff0000;"> v-if</span><span style="color: #0000ff;">="frmData.type=='通过'"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">ul</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="aui-col-5"</span><span style="color: #0000ff;">&gt;</span>
             <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ul</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="type-fgx"</span><span style="color: #0000ff;">&gt;&lt;</span><span style="color: #800000;">span</span><span style="color: #0000ff;">&gt;</span>|<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">span</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="type-button"</span><span style="color: #ff0000;"> tapmode onclick</span><span style="color: #0000ff;">="getInspectionList('改进')"</span><span style="color: #0000ff;">&gt;</span>改进<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">li </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="type-active"</span><span style="color: #ff0000;"> v-if</span><span style="color: #0000ff;">="frmData.type=='改进'"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">ul</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="aui-col-5"</span><span style="color: #0000ff;">&gt;</span>
             <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">ul</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="type-fgx"</span><span style="color: #0000ff;">&gt;&lt;</span><span style="color: #800000;">span</span><span style="color: #0000ff;">&gt;</span>|<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">span</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="type-button"</span><span style="color: #ff0000;"> tapmode onclick</span><span style="color: #0000ff;">="getInspectionList('整改')"</span><span style="color: #0000ff;">&gt;</span>整改<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">li </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="type-active"</span><span style="color: #ff0000;"> v-if</span><span style="color: #0000ff;">="frmData.type=='整改'"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">li</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">ul</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>


    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">style</span><span style="color: #0000ff;">="margin: 10px;"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>


    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="aui-list aui-media-list"</span><span style="color: #ff0000;"> v-show</span><span style="color: #0000ff;">="inspectionList.length&gt;0"</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="aui-list-item"</span><span style="color: #ff0000;"> v-for</span><span style="color: #0000ff;">="item in inspectionList"</span><span style="color: #0000ff;">&gt;</span>
              <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="aui-media-list-item-inner"</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="aui-list-item-inner"</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="aui-list-item-text"</span><span style="color: #0000ff;">&gt;</span>
                                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="aui-list-item-title aui-font-size-14"</span><span style="color: #0000ff;">&gt;</span>{{item.xj_content}}<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
                                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="aui-list-item-right"</span><span style="color: #0000ff;">&gt;&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="aui-btn aui-btn-success"</span><span style="color: #0000ff;">&gt;</span>{{item.type}}<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="aui-list-item-text"</span><span style="color: #0000ff;">&gt;</span>
                            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="aui-list-item-title"</span><span style="color: #0000ff;">&gt;</span>
                                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">i </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="aui-iconfont aui-icon-my"</span><span style="color: #ff0000;"> style</span><span style="color: #0000ff;">="margin-right:10px"</span><span style="color: #0000ff;">&gt;</span>{{item.cuser}}<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">i</span><span style="color: #0000ff;">&gt;</span>
                                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">i </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="aui-iconfont aui-icon-date"</span><span style="color: #0000ff;">&gt;</span>{{item.xj_date}}<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">i</span><span style="color: #0000ff;">&gt;</span>
                            <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="img-right"</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">img </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="../../image/ui/index_arrow.png"</span><span style="color: #ff0000;"> class</span><span style="color: #0000ff;">="aui-list-img-sm"</span><span style="color: #ff0000;"> style</span><span style="color: #0000ff;">="width:0.8rem"</span> <span style="color: #0000ff;">/&gt;</span>
                    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
              <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>  
        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> &lt;div id="nomore" class="nomore" v-if="inspectionList.length&gt;=total"&gt;没有更多数据了&lt;/div&gt;
        &lt;div id="nomore" class="nomore" v-else="inspectionList.length&gt;=total"&gt;下翻加载更多信息&lt;/div&gt; </span><span style="color: #008000;">--&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>

    
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">body</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="text/javascript"</span><span style="color: #ff0000;"> src</span><span style="color: #0000ff;">="../../script/api.js"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="text/javascript"</span><span style="color: #ff0000;"> src</span><span style="color: #0000ff;">="../../script/request.js"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="text/javascript"</span><span style="color: #ff0000;"> src</span><span style="color: #0000ff;">="../../script/vue.js"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="text/javascript"</span><span style="color: #ff0000;"> src</span><span style="color: #0000ff;">="../../script/mescroll/mescroll.min.js"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="text/javascript"</span><span style="color: #0000ff;">&gt;</span>
<span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> VM;
</span><span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> mescroll;
apiready </span><span style="background-color: #f5f5f5; color: #000000;">=</span> <span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;">() {

    VM</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #0000ff;">new</span><span style="background-color: #f5f5f5; color: #000000;"> Vue({
         el: </span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">#app</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">,
         data:{
            frmData:{
                type:</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">待办</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">
            },
            inspectionList:[],</span><span style="background-color: #f5f5f5; color: #008000;">//</span><span style="background-color: #f5f5f5; color: #008000;">巡检列表</span>
<span style="background-color: #f5f5f5; color: #000000;">            total:</span><span style="background-color: #f5f5f5; color: #000000;">0</span><span style="background-color: #f5f5f5; color: #000000;">,
            pageindex:</span><span style="background-color: #f5f5f5; color: #000000;">1</span><span style="background-color: #f5f5f5; color: #000000;">,
            pagesize:</span><span style="background-color: #f5f5f5; color: #000000;">10</span><span style="background-color: #f5f5f5; color: #000000;">,
            mescroll:{}
         },
         mounted:</span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;">(){
            </span><span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> vm</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #0000ff;">this</span><span style="background-color: #f5f5f5; color: #000000;">;
            vm.fnInspectionInit(</span><span style="background-color: #f5f5f5; color: #0000ff;">true</span><span style="background-color: #f5f5f5; color: #000000;">);
            vm.fnInitMescroll();
         },
         methods:{
             fnInitMescroll:</span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;">(){
                </span><span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> vm</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #0000ff;">this</span><span style="background-color: #f5f5f5; color: #000000;">;
                vm.mescroll</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #0000ff;">new</span><span style="background-color: #f5f5f5; color: #000000;"> MeScroll(</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">app</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">, {
                    down: {
                        auto: </span><span style="background-color: #f5f5f5; color: #0000ff;">false</span><span style="background-color: #f5f5f5; color: #000000;">,
                        callback: vm.fnDownCallback
                    },
                    up: {
                        auto: </span><span style="background-color: #f5f5f5; color: #0000ff;">false</span><span style="background-color: #f5f5f5; color: #000000;">,
                        noMoreSize:</span><span style="background-color: #f5f5f5; color: #000000;">1</span><span style="background-color: #f5f5f5; color: #000000;">,
                        </span><span style="background-color: #f5f5f5; color: #008000;">//</span><span style="background-color: #f5f5f5; color: #008000;"> isBounce: false,</span>
<span style="background-color: #f5f5f5; color: #000000;">                        htmlNodata:</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">&lt;p class="upwarp-nodata"&gt;-- 没有更多数据了 --&lt;/p&gt;</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">,
                        callback: vm.fnUpCallback
                    }
                });
             },
             fnDownCallback:</span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;">(){</span><span style="background-color: #f5f5f5; color: #008000;">//</span><span style="background-color: #f5f5f5; color: #008000;">下拉刷新</span>
                <span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> vm</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #0000ff;">this</span><span style="background-color: #f5f5f5; color: #000000;">;
                 setTimeout(</span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;"> () {
                    vm.fnInspectionInit(</span><span style="background-color: #f5f5f5; color: #0000ff;">false</span><span style="background-color: #f5f5f5; color: #000000;">,</span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;">(){
                        
                        vm.mescroll.endSuccess(); </span><span style="background-color: #f5f5f5; color: #008000;">//</span><span style="background-color: #f5f5f5; color: #008000;">刷新成功后调用此方法隐藏</span>
<span style="background-color: #f5f5f5; color: #000000;">                    })
                },</span><span style="background-color: #f5f5f5; color: #000000;">1000</span><span style="background-color: #f5f5f5; color: #000000;">);
             },
             fnUpCallback:</span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;">(){</span><span style="background-color: #f5f5f5; color: #008000;">//</span><span style="background-color: #f5f5f5; color: #008000;">上拉刷新</span>
                <span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> vm</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #0000ff;">this</span><span style="background-color: #f5f5f5; color: #000000;">;
                setTimeout(</span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;"> () {
                    vm.pageindex</span><span style="background-color: #f5f5f5; color: #000000;">++</span><span style="background-color: #f5f5f5; color: #000000;">;
                    console.log(vm.pageindex)
                    vm.fnGetCommonInspectionList(</span><span style="background-color: #f5f5f5; color: #0000ff;">false</span><span style="background-color: #f5f5f5; color: #000000;">,vm.pageindex,</span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;">(data){
                        </span><span style="background-color: #f5f5f5; color: #0000ff;">if</span><span style="background-color: #f5f5f5; color: #000000;">(data</span><span style="background-color: #f5f5f5; color: #000000;">!=</span><span style="background-color: #f5f5f5; color: #0000ff;">null</span><span style="background-color: #f5f5f5; color: #000000;">&amp;&amp;</span><span style="background-color: #f5f5f5; color: #000000;">data.length</span><span style="background-color: #f5f5f5; color: #000000;">&gt;</span><span style="background-color: #f5f5f5; color: #000000;">0</span><span style="background-color: #f5f5f5; color: #000000;">)
                        {
                            </span><span style="background-color: #f5f5f5; color: #0000ff;">for</span><span style="background-color: #f5f5f5; color: #000000;"> (</span><span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> i </span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;"> data.length </span><span style="background-color: #f5f5f5; color: #000000;">-</span> <span style="background-color: #f5f5f5; color: #000000;">1</span><span style="background-color: #f5f5f5; color: #000000;">; i </span><span style="background-color: #f5f5f5; color: #000000;">&gt;=</span> <span style="background-color: #f5f5f5; color: #000000;">0</span><span style="background-color: #f5f5f5; color: #000000;">; i</span><span style="background-color: #f5f5f5; color: #000000;">--</span><span style="background-color: #f5f5f5; color: #000000;">) {
                                vm.inspectionList.push(data[i]);
                            }
                        }
                        console.log(</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">total:</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">+</span><span style="background-color: #f5f5f5; color: #000000;">vm.total</span><span style="background-color: #f5f5f5; color: #000000;">+</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">,length:</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">+</span><span style="background-color: #f5f5f5; color: #000000;">vm.inspectionList.length);

                        </span><span style="background-color: #f5f5f5; color: #0000ff;">if</span><span style="background-color: #f5f5f5; color: #000000;">(vm.total</span><span style="background-color: #f5f5f5; color: #000000;">&gt;</span><span style="background-color: #f5f5f5; color: #000000;">vm.inspectionList.length)
                        {
                            vm.mescroll.optUp.hasNext </span><span style="background-color: #f5f5f5; color: #000000;">=</span> <span style="background-color: #f5f5f5; color: #0000ff;">true</span><span style="background-color: #f5f5f5; color: #000000;">;</span><span style="background-color: #f5f5f5; color: #008000;">//</span><span style="background-color: #f5f5f5; color: #008000;">可上拉</span>
<span style="background-color: #f5f5f5; color: #000000;">                            vm.mescroll.endUpScroll(</span><span style="background-color: #f5f5f5; color: #0000ff;">false</span><span style="background-color: #f5f5f5; color: #000000;">);</span><span style="background-color: #f5f5f5; color: #008000;">//</span><span style="background-color: #f5f5f5; color: #008000;">隐藏上拉</span>
<span style="background-color: #f5f5f5; color: #000000;">                        }
                        </span><span style="background-color: #f5f5f5; color: #0000ff;">else</span><span style="background-color: #f5f5f5; color: #000000;">
                        {
                            vm.mescroll.optUp.hasNext </span><span style="background-color: #f5f5f5; color: #000000;">=</span> <span style="background-color: #f5f5f5; color: #0000ff;">false</span><span style="background-color: #f5f5f5; color: #000000;">;</span><span style="background-color: #f5f5f5; color: #008000;">//</span><span style="background-color: #f5f5f5; color: #008000;">可上拉</span>
<span style="background-color: #f5f5f5; color: #000000;">                            vm.mescroll.endUpScroll(</span><span style="background-color: #f5f5f5; color: #0000ff;">true</span><span style="background-color: #f5f5f5; color: #000000;">);</span><span style="background-color: #f5f5f5; color: #008000;">//</span><span style="background-color: #f5f5f5; color: #008000;">隐藏上拉</span>
<span style="background-color: #f5f5f5; color: #000000;">                        }
                        </span><span style="background-color: #f5f5f5; color: #008000;">//</span><span style="background-color: #f5f5f5; color: #008000;">vm.mescroll.endSuccess(vm.inspectionList.length,vm.total&gt;vm.inspectionList.length); </span>
<span style="background-color: #f5f5f5; color: #000000;">                    });
                },</span><span style="background-color: #f5f5f5; color: #000000;">300</span><span style="background-color: #f5f5f5; color: #000000;">);
             },
             fnInspectionInit:</span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;">(showProgress,callback){
                </span><span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> vm</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #0000ff;">this</span><span style="background-color: #f5f5f5; color: #000000;">;
                vm.pageindex</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;">1</span><span style="background-color: #f5f5f5; color: #000000;">;
                vm.fnGetCommonInspectionList(showProgress,vm.pageindex,</span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;">(data){
                    vm.inspectionList</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;">data
                    </span><span style="background-color: #f5f5f5; color: #0000ff;">if</span><span style="background-color: #f5f5f5; color: #000000;">(vm.total</span><span style="background-color: #f5f5f5; color: #000000;">&gt;</span><span style="background-color: #f5f5f5; color: #000000;">vm.inspectionList.length)
                    {
                        vm.mescroll.optUp.hasNext </span><span style="background-color: #f5f5f5; color: #000000;">=</span> <span style="background-color: #f5f5f5; color: #0000ff;">true</span><span style="background-color: #f5f5f5; color: #000000;">;</span><span style="background-color: #f5f5f5; color: #008000;">//</span><span style="background-color: #f5f5f5; color: #008000;">可上拉</span>
<span style="background-color: #f5f5f5; color: #000000;">                        vm.mescroll.endUpScroll(</span><span style="background-color: #f5f5f5; color: #0000ff;">false</span><span style="background-color: #f5f5f5; color: #000000;">);</span><span style="background-color: #f5f5f5; color: #008000;">//</span><span style="background-color: #f5f5f5; color: #008000;">隐藏上拉</span>
<span style="background-color: #f5f5f5; color: #000000;">                    }
                    </span><span style="background-color: #f5f5f5; color: #0000ff;">else</span><span style="background-color: #f5f5f5; color: #000000;">
                    {
                        vm.mescroll.optUp.hasNext </span><span style="background-color: #f5f5f5; color: #000000;">=</span> <span style="background-color: #f5f5f5; color: #0000ff;">false</span><span style="background-color: #f5f5f5; color: #000000;">;</span><span style="background-color: #f5f5f5; color: #008000;">//</span><span style="background-color: #f5f5f5; color: #008000;">可上拉</span>
<span style="background-color: #f5f5f5; color: #000000;">                        vm.mescroll.endUpScroll(</span><span style="background-color: #f5f5f5; color: #0000ff;">true</span><span style="background-color: #f5f5f5; color: #000000;">);</span><span style="background-color: #f5f5f5; color: #008000;">//</span><span style="background-color: #f5f5f5; color: #008000;">隐藏上拉</span>
<span style="background-color: #f5f5f5; color: #000000;">                    }
                    </span><span style="background-color: #f5f5f5; color: #0000ff;">if</span><span style="background-color: #f5f5f5; color: #000000;">(callback)callback()
                });
             },
             fnGetCommonInspectionList:</span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;">(showProgress,pageindex,callback){</span><span style="background-color: #f5f5f5; color: #008000;">//</span><span style="background-color: #f5f5f5; color: #008000;">获取巡检</span>
                <span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> vm</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #0000ff;">this</span><span style="background-color: #f5f5f5; color: #000000;">; 

                </span><span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> prjid</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;">$api.getStorage(</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">userInfo</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">).myproinfo.id;

                </span><span style="background-color: #f5f5f5; color: #0000ff;">if</span><span style="background-color: #f5f5f5; color: #000000;">(vm.frmData.type</span><span style="background-color: #f5f5f5; color: #000000;">==</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">待办</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">)
                {
                    </span><span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> param</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;">{parameter:{prj_id:prjid},pageindex:pageindex,pagesize:vm.pagesize};
                    fnPost(</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">/api/SafeInspection/GetTodoList</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">,param, </span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">application/json;charset=utf-8</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">, </span><span style="background-color: #f5f5f5; color: #0000ff;">true</span><span style="background-color: #f5f5f5; color: #000000;">, </span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;">(ret, err) {
                        </span><span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> data;
                        </span><span style="background-color: #f5f5f5; color: #0000ff;">if</span><span style="background-color: #f5f5f5; color: #000000;">(ret</span><span style="background-color: #f5f5f5; color: #000000;">!=</span><span style="background-color: #f5f5f5; color: #0000ff;">null</span><span style="background-color: #f5f5f5; color: #000000;">&amp;&amp;</span><span style="background-color: #f5f5f5; color: #000000;">ret.ret</span><span style="background-color: #f5f5f5; color: #000000;">==</span><span style="background-color: #f5f5f5; color: #000000;">0</span><span style="background-color: #f5f5f5; color: #000000;">&amp;&amp;</span><span style="background-color: #f5f5f5; color: #000000;">ret.data.length</span><span style="background-color: #f5f5f5; color: #000000;">&gt;</span><span style="background-color: #f5f5f5; color: #000000;">0</span><span style="background-color: #f5f5f5; color: #000000;">)
                        {
                            data</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;">ret.data;
                            vm.total</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;">ret.total;
                        }
                        </span><span style="background-color: #f5f5f5; color: #0000ff;">else</span><span style="background-color: #f5f5f5; color: #000000;">
                        {
                            data</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;">[];
                            vm.total</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;">0</span><span style="background-color: #f5f5f5; color: #000000;">;
                        }
                        </span><span style="background-color: #f5f5f5; color: #0000ff;">if</span><span style="background-color: #f5f5f5; color: #000000;">(callback)callback(data);
                    },showProgress,</span><span style="background-color: #f5f5f5; color: #000000;">""</span><span style="background-color: #f5f5f5; color: #000000;">);
                }
                </span><span style="background-color: #f5f5f5; color: #0000ff;">else</span><span style="background-color: #f5f5f5; color: #000000;">
                {
                    </span><span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> param</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;">{parameter:{prj_id:prjid,type:vm.frmData.type},pageindex:pageindex,pagesize:vm.pagesize};
                    fnPost(</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">/api/SafeInspection/GetOtherList</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">,param, </span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">application/json;charset=utf-8</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">, </span><span style="background-color: #f5f5f5; color: #0000ff;">true</span><span style="background-color: #f5f5f5; color: #000000;">, </span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;">(ret, err) {
                        </span><span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> data;
                        </span><span style="background-color: #f5f5f5; color: #0000ff;">if</span><span style="background-color: #f5f5f5; color: #000000;">(ret</span><span style="background-color: #f5f5f5; color: #000000;">!=</span><span style="background-color: #f5f5f5; color: #0000ff;">null</span><span style="background-color: #f5f5f5; color: #000000;">&amp;&amp;</span><span style="background-color: #f5f5f5; color: #000000;">ret.ret</span><span style="background-color: #f5f5f5; color: #000000;">==</span><span style="background-color: #f5f5f5; color: #000000;">0</span><span style="background-color: #f5f5f5; color: #000000;">&amp;&amp;</span><span style="background-color: #f5f5f5; color: #000000;">ret.data.length</span><span style="background-color: #f5f5f5; color: #000000;">&gt;</span><span style="background-color: #f5f5f5; color: #000000;">0</span><span style="background-color: #f5f5f5; color: #000000;">)
                        {
                            data</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;">ret.data;
                            vm.total</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;">ret.total;
                        }
                        </span><span style="background-color: #f5f5f5; color: #0000ff;">else</span><span style="background-color: #f5f5f5; color: #000000;">
                        {
                            data</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;">[];
                            vm.total</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;">0</span><span style="background-color: #f5f5f5; color: #000000;">;
                        }
                        </span><span style="background-color: #f5f5f5; color: #0000ff;">if</span><span style="background-color: #f5f5f5; color: #000000;">(callback)callback(data);
                    },showProgress,</span><span style="background-color: #f5f5f5; color: #000000;">""</span><span style="background-color: #f5f5f5; color: #000000;">);
                }

             }


         }
     });

};


</span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;"> getInspectionList(type){
    VM.frmData.type</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;">type;
    VM.fnInspectionInit(</span><span style="background-color: #f5f5f5; color: #0000ff;">true</span><span style="background-color: #f5f5f5; color: #000000;">);
}



</span><span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>

<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">html</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<span class="cnblogs_code_collapse">案例</span></div>
<p>js下载：<a href="https://pan.baidu.com/s/113VxMA48GCtwjlRa2_ZC4g" target="_blank">https://pan.baidu.com/s/113VxMA48GCtwjlRa2_ZC4g</a></p>
<p>组件官网：<a href="http://www.mescroll.com/" target="_blank">http://www.mescroll.com/</a></p>
<p>4，提示组件dialogBox</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('0ce83570-636e-4dcb-b610-494caac47404')"><img id="code_img_closed_0ce83570-636e-4dcb-b610-494caac47404" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_0ce83570-636e-4dcb-b610-494caac47404" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('0ce83570-636e-4dcb-b610-494caac47404',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_0ce83570-636e-4dcb-b610-494caac47404" class="cnblogs_code_hide">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">提示信息</span>
<span style="color: #000000;">function alertmsg(msg, funname) {
    </span><span style="color: #0000ff;">var</span> closeset = <span style="color: #0000ff;">true</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">if</span> (funname == <span style="color: #800000;">'</span><span style="color: #800000;">exit</span><span style="color: #800000;">'</span><span style="color: #000000;">) {
        closeset </span>= <span style="color: #0000ff;">false</span><span style="color: #000000;">;
    }
    </span><span style="color: #0000ff;">var</span> dialogBox = api.require(<span style="color: #800000;">'</span><span style="color: #800000;">dialogBox</span><span style="color: #800000;">'</span><span style="color: #000000;">);
    dialogBox.alert({
        texts: {
            title: </span><span style="color: #800000;">'</span><span style="color: #800000;">提示信息</span><span style="color: #800000;">'</span><span style="color: #000000;">,
            content: msg,
            leftBtnTitle: </span><span style="color: #800000;">'</span><span style="color: #800000;">确定</span><span style="color: #800000;">'</span><span style="color: #000000;">,
        },
        styles: {
            bg: </span><span style="color: #800000;">'</span><span style="color: #800000;">#fff</span><span style="color: #800000;">'</span><span style="color: #000000;">,
            w: </span><span style="color: #800080;">280</span><span style="color: #000000;">,
            title: {
                marginT: </span><span style="color: #800080;">10</span><span style="color: #000000;">,
                icon: </span><span style="color: #800000;">''</span><span style="color: #000000;">,
                iconSize: </span><span style="color: #800080;">40</span><span style="color: #000000;">,
                titleSize: </span><span style="color: #800080;">16</span><span style="color: #000000;">,
                titleColor: </span><span style="color: #800000;">'</span><span style="color: #800000;">#000</span><span style="color: #800000;">'</span><span style="color: #000000;">
            },
            content: {
                color: </span><span style="color: #800000;">'</span><span style="color: #800000;">#000</span><span style="color: #800000;">'</span><span style="color: #000000;">,
                size: </span><span style="color: #800080;">14</span><span style="color: #000000;">
            },
            left: {
                marginB: </span><span style="color: #800080;">5</span><span style="color: #000000;">,
                marginL: </span><span style="color: #800080;">5</span><span style="color: #000000;">,
                w: </span><span style="color: #800080;">270</span><span style="color: #000000;">,
                h: </span><span style="color: #800080;">40</span><span style="color: #000000;">,
                corner: </span><span style="color: #800080;">2</span><span style="color: #000000;">,
                bg: </span><span style="color: #800000;">'</span><span style="color: #800000;">#03A9F4</span><span style="color: #800000;">'</span><span style="color: #000000;">,
                color: </span><span style="color: #800000;">'</span><span style="color: #800000;">#FFF</span><span style="color: #800000;">'</span><span style="color: #000000;">,
                size: </span><span style="color: #800080;">14</span><span style="color: #000000;">
            }
        },
        tapClose: closeset
    }, function(ret) {
        </span><span style="color: #0000ff;">if</span> (ret.eventType == <span style="color: #800000;">'</span><span style="color: #800000;">left</span><span style="color: #800000;">'</span><span style="color: #000000;">) {
            </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (funname) {
                </span><span style="color: #0000ff;">if</span> (funname == <span style="color: #800000;">'</span><span style="color: #800000;">exit</span><span style="color: #800000;">'</span><span style="color: #000000;">) {
                    exitThisApp();
                } </span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span> (funname == <span style="color: #800000;">'</span><span style="color: #800000;">back</span><span style="color: #800000;">'</span><span style="color: #000000;">) {
                    goback();
                } </span><span style="color: #0000ff;">else</span><span style="color: #000000;"> {
                    api.execScript({
                        name: api.winName,
                        frameName: api.frameName,
                        script: funname </span>+ <span style="color: #800000;">'</span><span style="color: #800000;">();</span><span style="color: #800000;">'</span><span style="color: #000000;">
                    });
                }
            }
            dialogBox.close({
                dialogName: </span><span style="color: #800000;">'</span><span style="color: #800000;">alert</span><span style="color: #800000;">'</span><span style="color: #000000;">
            });
        }
    });
}</span></pre>
</div>
<span class="cnblogs_code_collapse">公共方法</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('195d0604-f74c-43c1-ad50-f99409277a43')"><img id="code_img_closed_195d0604-f74c-43c1-ad50-f99409277a43" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_195d0604-f74c-43c1-ad50-f99409277a43" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('195d0604-f74c-43c1-ad50-f99409277a43',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_195d0604-f74c-43c1-ad50-f99409277a43" class="cnblogs_code_hide">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">返回</span>
<span style="color: #000000;">function goback() {
    api.closeWin();
}</span></pre>
</div>
<span class="cnblogs_code_collapse">goback</span></div>
<p>5，图片浏览组件photoBrowser</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('01e97a33-47c2-41cc-8cff-cdeab4b0afc9')"><img id="code_img_closed_01e97a33-47c2-41cc-8cff-cdeab4b0afc9" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_01e97a33-47c2-41cc-8cff-cdeab4b0afc9" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('01e97a33-47c2-41cc-8cff-cdeab4b0afc9',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_01e97a33-47c2-41cc-8cff-cdeab4b0afc9" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">&lt;!</span><span style="color: #ff00ff;">DOCTYPE HTML</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">html</span><span style="color: #0000ff;">&gt;</span>

<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">head</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">meta </span><span style="color: #ff0000;">charset</span><span style="color: #0000ff;">="utf-8"</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">meta </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="viewport"</span><span style="color: #ff0000;"> content</span><span style="color: #0000ff;">="maximum-scale=1.0, minimum-scale=1.0, user-scalable=0, initial-scale=1.0, width=device-width"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">meta </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="format-detection"</span><span style="color: #ff0000;"> content</span><span style="color: #0000ff;">="telephone=no, email=no, date=no, address=no"</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">title</span><span style="color: #0000ff;">&gt;</span>瓯云APP<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">title</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">link </span><span style="color: #ff0000;">rel</span><span style="color: #0000ff;">="stylesheet"</span><span style="color: #ff0000;"> type</span><span style="color: #0000ff;">="text/css"</span><span style="color: #ff0000;"> href</span><span style="color: #0000ff;">="../../css/api.css"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">link </span><span style="color: #ff0000;">rel</span><span style="color: #0000ff;">="stylesheet"</span><span style="color: #ff0000;"> type</span><span style="color: #0000ff;">="text/css"</span><span style="color: #ff0000;"> href</span><span style="color: #0000ff;">="../../css/style.css"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">style</span><span style="color: #0000ff;">&gt;</span>

    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">style</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">head</span><span style="color: #0000ff;">&gt;</span>

<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">body</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">body</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="text/javascript"</span><span style="color: #ff0000;"> src</span><span style="color: #0000ff;">="../../script/api.js"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="text/javascript"</span><span style="color: #ff0000;"> src</span><span style="color: #0000ff;">="../../script/request.js"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="text/javascript"</span><span style="color: #0000ff;">&gt;</span>
<span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> photoBrowser;
apiready </span><span style="background-color: #f5f5f5; color: #000000;">=</span> <span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;">() {
    api.parseTapmode();
    </span><span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> imgarr </span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;"> api.pageParam.imgarr;
    </span><span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> imgnamearr </span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;"> api.pageParam.imgnamearr;
    </span><span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> name </span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;"> api.pageParam.name;
    </span><span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> imgindex </span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;"> api.pageParam.imgindex;
    photoBrowser </span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;"> api.require(</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">photoBrowser</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">);
    </span><span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> downloadpath </span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;"> imgarr[imgindex];
    photoBrowser.open({
        images: imgarr,
        activeIndex: imgindex,
        placeholderImg: </span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">widget://image/banner_bg.png</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">,
        bgColor: </span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">#000</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">
    }, </span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;">(ret, err) {
        </span><span style="background-color: #f5f5f5; color: #0000ff;">if</span><span style="background-color: #f5f5f5; color: #000000;"> (ret) {
            </span><span style="background-color: #f5f5f5; color: #0000ff;">if</span><span style="background-color: #f5f5f5; color: #000000;"> (name) {
                </span><span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> f_h </span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;"> api.frameHeight </span><span style="background-color: #f5f5f5; color: #000000;">-</span> <span style="background-color: #f5f5f5; color: #000000;">50</span><span style="background-color: #f5f5f5; color: #000000;">;
                api.openFrame({
                    name: </span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">imgname_frm</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">,
                    url: </span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">imgname_frm.html</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">,
                    rect: {
                        x: </span><span style="background-color: #f5f5f5; color: #000000;">0</span><span style="background-color: #f5f5f5; color: #000000;">,
                        y: f_h,
                        w: </span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">auto</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">,
                        h: </span><span style="background-color: #f5f5f5; color: #000000;">50</span><span style="background-color: #f5f5f5; color: #000000;">
                    },
                    pageParam: {
                        name: name
                    },
                    bounces: </span><span style="background-color: #f5f5f5; color: #0000ff;">false</span><span style="background-color: #f5f5f5; color: #000000;">
                });
            }
            </span><span style="background-color: #f5f5f5; color: #0000ff;">if</span><span style="background-color: #f5f5f5; color: #000000;"> (ret.eventType </span><span style="background-color: #f5f5f5; color: #000000;">==</span> <span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">loadImgFail</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">) {
                api.toast({
                    msg: </span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">图片下载失败</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">
                });
            }
            </span><span style="background-color: #f5f5f5; color: #0000ff;">if</span><span style="background-color: #f5f5f5; color: #000000;"> (ret.eventType </span><span style="background-color: #f5f5f5; color: #000000;">==</span> <span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">change</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">) {
                photoBrowser.getIndex(</span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;">(ret, err) {
                    </span><span style="background-color: #f5f5f5; color: #0000ff;">if</span><span style="background-color: #f5f5f5; color: #000000;"> (ret) {
                        </span><span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> nowindex </span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;"> ret.index;
                        downloadpath </span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;"> imgarr[nowindex];
                        getimgname(nowindex, imgnamearr);
                    } </span><span style="background-color: #f5f5f5; color: #0000ff;">else</span><span style="background-color: #f5f5f5; color: #000000;"> {
                        alert(JSON.stringify(err));
                    }
                });
            }
            </span><span style="background-color: #f5f5f5; color: #0000ff;">if</span><span style="background-color: #f5f5f5; color: #000000;"> (ret.eventType </span><span style="background-color: #f5f5f5; color: #000000;">==</span> <span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">click</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">) {
                api.actionSheet({
                    title: </span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">请选择</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">,
                    cancelTitle: </span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">取消</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">,
                    buttons: [</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">保存到相册</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">, </span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">关闭窗口</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">]
                }, </span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;">(ret, err) {
                    </span><span style="background-color: #f5f5f5; color: #0000ff;">if</span><span style="background-color: #f5f5f5; color: #000000;"> (ret) {
                        </span><span style="background-color: #f5f5f5; color: #0000ff;">if</span><span style="background-color: #f5f5f5; color: #000000;"> (ret.buttonIndex </span><span style="background-color: #f5f5f5; color: #000000;">==</span> <span style="background-color: #f5f5f5; color: #000000;">1</span><span style="background-color: #f5f5f5; color: #000000;">) {
                            api.download({
                                url: downloadpath,
                                report: </span><span style="background-color: #f5f5f5; color: #0000ff;">true</span><span style="background-color: #f5f5f5; color: #000000;">,
                                cache: </span><span style="background-color: #f5f5f5; color: #0000ff;">true</span><span style="background-color: #f5f5f5; color: #000000;">,
                                allowResume: </span><span style="background-color: #f5f5f5; color: #0000ff;">true</span><span style="background-color: #f5f5f5; color: #000000;">
                            }, </span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;">(ret, err) {
                                </span><span style="background-color: #f5f5f5; color: #0000ff;">if</span><span style="background-color: #f5f5f5; color: #000000;"> (ret.state </span><span style="background-color: #f5f5f5; color: #000000;">==</span> <span style="background-color: #f5f5f5; color: #000000;">1</span><span style="background-color: #f5f5f5; color: #000000;">) {
                                    api.saveMediaToAlbum({
                                        path: ret.savePath
                                    }, </span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;">(ret, err) {
                                        </span><span style="background-color: #f5f5f5; color: #0000ff;">if</span><span style="background-color: #f5f5f5; color: #000000;"> (ret </span><span style="background-color: #f5f5f5; color: #000000;">&amp;&amp;</span><span style="background-color: #f5f5f5; color: #000000;"> ret.status) {
                                            api.toast({
                                                msg: </span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">保存成功</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">
                                            });
                                        } </span><span style="background-color: #f5f5f5; color: #0000ff;">else</span><span style="background-color: #f5f5f5; color: #000000;"> {
                                            api.toast({
                                                msg: </span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">保存失败！</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">
                                            });
                                        }
                                    });
                                } </span><span style="background-color: #f5f5f5; color: #0000ff;">else</span> <span style="background-color: #f5f5f5; color: #0000ff;">if</span><span style="background-color: #f5f5f5; color: #000000;"> (ret.state </span><span style="background-color: #f5f5f5; color: #000000;">==</span> <span style="background-color: #f5f5f5; color: #000000;">2</span><span style="background-color: #f5f5f5; color: #000000;">) {
                                    alert(</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">保存失败</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">);
                                } </span><span style="background-color: #f5f5f5; color: #0000ff;">else</span><span style="background-color: #f5f5f5; color: #000000;"> {
                                    </span><span style="background-color: #f5f5f5; color: #008000;">//</span><span style="background-color: #f5f5f5; color: #008000;">下载中</span>
<span style="background-color: #f5f5f5; color: #000000;">                                }
                            });
                        } </span><span style="background-color: #f5f5f5; color: #0000ff;">else</span> <span style="background-color: #f5f5f5; color: #0000ff;">if</span><span style="background-color: #f5f5f5; color: #000000;"> (ret.buttonIndex </span><span style="background-color: #f5f5f5; color: #000000;">==</span> <span style="background-color: #f5f5f5; color: #000000;">2</span><span style="background-color: #f5f5f5; color: #000000;">) {
                            photoBrowser.close();
                            goback();
                        } </span><span style="background-color: #f5f5f5; color: #0000ff;">else</span><span style="background-color: #f5f5f5; color: #000000;"> {
                            </span><span style="background-color: #f5f5f5; color: #0000ff;">return</span><span style="background-color: #f5f5f5; color: #000000;">;
                        }
                    } </span><span style="background-color: #f5f5f5; color: #0000ff;">else</span><span style="background-color: #f5f5f5; color: #000000;"> {
                        alert(JSON.stringify(err));
                    }
                });
            }
        } </span><span style="background-color: #f5f5f5; color: #0000ff;">else</span><span style="background-color: #f5f5f5; color: #000000;"> {
            alertmsg(</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">图片打开错误</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">);
        }
    });
};
</span><span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>

<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">html</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<p>&nbsp;</p>