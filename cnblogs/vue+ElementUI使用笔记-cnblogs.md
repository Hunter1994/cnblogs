<p>&nbsp;</p>
<p>1，使用表单验证：</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('e7e8dd4d-9d2b-4085-bc50-c577ef73e989')"><img id="code_img_closed_e7e8dd4d-9d2b-4085-bc50-c577ef73e989" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_e7e8dd4d-9d2b-4085-bc50-c577ef73e989" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('e7e8dd4d-9d2b-4085-bc50-c577ef73e989',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_e7e8dd4d-9d2b-4085-bc50-c577ef73e989" class="cnblogs_code_hide">
<pre><span style="color: #008000;">//</span><span style="color: #008000;">定义验证规则</span>
window.varifyUtil =<span style="color: #000000;"> {
    </span><span style="color: #008000;">//</span><span style="color: #008000;">验证数字</span>
<span style="color: #000000;">    validateNumber: function(rule, value, callback){
        </span><span style="color: #0000ff;">if</span> (!<span style="color: #000000;">isGreaterZero(value)) {
            </span><span style="color: #0000ff;">return</span> callback(<span style="color: #0000ff;">new</span> Error(<span style="color: #800000;">"</span><span style="color: #800000;">请输入数字类型</span><span style="color: #800000;">"</span><span style="color: #000000;">));
        }
        callback();
    },
    </span><span style="color: #008000;">//</span><span style="color: #008000;">验证身份证号</span>
    validateIdcard: function(rule, value, callback){<span style="color: #008000;">//</span><span style="color: #008000;">身份证验证</span>
        <span style="color: #0000ff;">var</span> reg = /^(\d{<span style="color: #800080;">6</span>})(\d{<span style="color: #800080;">4</span>})(\d{<span style="color: #800080;">2</span>})(\d{<span style="color: #800080;">2</span>})(\d{<span style="color: #800080;">3</span>})([<span style="color: #800080;">0</span>-<span style="color: #800080;">9</span>]|X)$/
        <span style="color: #0000ff;">if</span> (value &amp;&amp; !<span style="color: #000000;">reg.test(value)) {
            </span><span style="color: #0000ff;">return</span> callback(<span style="color: #0000ff;">new</span> Error(<span style="color: #800000;">'</span><span style="color: #800000;">身份证号码格式有误</span><span style="color: #800000;">'</span><span style="color: #000000;">));
        }
        callback();
    },
    validateIdcardRequired: function(rule, value, callback){</span><span style="color: #008000;">//</span><span style="color: #008000;">身份证验证</span>
        <span style="color: #0000ff;">var</span> reg = /^(\d{<span style="color: #800080;">6</span>})(\d{<span style="color: #800080;">4</span>})(\d{<span style="color: #800080;">2</span>})(\d{<span style="color: #800080;">2</span>})(\d{<span style="color: #800080;">3</span>})([<span style="color: #800080;">0</span>-<span style="color: #800080;">9</span>]|X)$/
        <span style="color: #0000ff;">if</span> (!value || !<span style="color: #000000;">reg.test(value)) {
            </span><span style="color: #0000ff;">return</span> callback(<span style="color: #0000ff;">new</span> Error(<span style="color: #800000;">'</span><span style="color: #800000;">身份证号码格式有误</span><span style="color: #800000;">'</span><span style="color: #000000;">));
        }
        callback();
    },
    </span><span style="color: #008000;">//</span><span style="color: #008000;">验证手机</span>
<span style="color: #000000;">    validateMobile: function(rule, value, callback){
        </span><span style="color: #0000ff;">var</span> reg = /^<span style="color: #800080;">1</span>\d{<span style="color: #800080;">10</span>}$/
        <span style="color: #0000ff;">if</span> (value &amp;&amp; !<span style="color: #000000;">reg.test(value)) {
            </span><span style="color: #0000ff;">return</span> callback(<span style="color: #0000ff;">new</span> Error(<span style="color: #800000;">'</span><span style="color: #800000;">电话号码格式有误</span><span style="color: #800000;">'</span><span style="color: #000000;">));
        }
        callback()
    },
    </span><span style="color: #008000;">//</span><span style="color: #008000;">验证手机</span>
<span style="color: #000000;">    validateMobileRequired: function(rule, value, callback){
        </span><span style="color: #0000ff;">var</span> reg = /^<span style="color: #800080;">1</span>\d{<span style="color: #800080;">10</span>}$/
        <span style="color: #0000ff;">if</span> (!<span style="color: #000000;">reg.test(value)) {
            </span><span style="color: #0000ff;">return</span> callback(<span style="color: #0000ff;">new</span> Error(<span style="color: #800000;">'</span><span style="color: #800000;">电话号码格式有误</span><span style="color: #800000;">'</span><span style="color: #000000;">));
        }
        callback()
    },
    </span><span style="color: #008000;">//</span><span style="color: #008000;">验证电话号码</span>
<span style="color: #000000;">    validateTel: function(rule, value, callback){
        </span><span style="color: #0000ff;">var</span> reg = /^[\d\+\*-]+$/
        <span style="color: #0000ff;">if</span> (value &amp;&amp; !<span style="color: #000000;">reg.test(value)) {
            </span><span style="color: #0000ff;">return</span> callback(<span style="color: #0000ff;">new</span> Error(<span style="color: #800000;">'</span><span style="color: #800000;">电话号码格式有误</span><span style="color: #800000;">'</span><span style="color: #000000;">));
        }
        callback()
    },
    </span><span style="color: #008000;">//</span><span style="color: #008000;">验证电话号码</span>
<span style="color: #000000;">    validateTelRequired: function(rule, value, callback){
        </span><span style="color: #0000ff;">var</span> reg = /^[\d\+\*-]+$/
        <span style="color: #0000ff;">if</span> (!<span style="color: #000000;">reg.test(value)) {
            </span><span style="color: #0000ff;">return</span> callback(<span style="color: #0000ff;">new</span> Error(<span style="color: #800000;">'</span><span style="color: #800000;">电话号码格式有误</span><span style="color: #800000;">'</span><span style="color: #000000;">));
        }
        callback()
    },
    </span><span style="color: #008000;">//</span><span style="color: #008000;">验证邮箱</span>
<span style="color: #000000;">    validateEmail: function(rule, value, callback){
        </span><span style="color: #0000ff;">var</span> reg = /^[\w!#$%&amp;<span style="color: #800000;">'</span><span style="color: #800000;">*+/=?^_`{|}~-]+(?:\.[\w!#$%&amp;</span><span style="color: #800000;">'</span>*+/=?^_`{|}~-]+)*@(?:[\w](?:[\w-]*[\w])?\.)+[\w](?:[\w-]*[\w])?$/
        <span style="color: #0000ff;">if</span> (value &amp;&amp; !<span style="color: #000000;">reg.test(value)) {
            </span><span style="color: #0000ff;">return</span> callback(<span style="color: #0000ff;">new</span> Error(<span style="color: #800000;">'</span><span style="color: #800000;">Email地址格式有误</span><span style="color: #800000;">'</span><span style="color: #000000;">));
        }
        callback()
    },
    </span><span style="color: #008000;">//</span><span style="color: #008000;">验证密码</span>
<span style="color: #000000;">    validatePwd: function(rule, value, callback){
        </span><span style="color: #0000ff;">var</span> reg = /^(\w){<span style="color: #800080;">6</span>,<span style="color: #800080;">16</span>}$/    <span style="color: #008000;">//</span><span style="color: #008000;">'[A-Za-z0-9_]'</span>
        <span style="color: #0000ff;">if</span>(!<span style="color: #000000;">value){
            </span><span style="color: #0000ff;">return</span> callback(<span style="color: #0000ff;">new</span> Error(<span style="color: #800000;">'</span><span style="color: #800000;">请输入密码</span><span style="color: #800000;">'</span><span style="color: #000000;">));
        }</span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span> (!<span style="color: #000000;">reg.test(value)) {
            </span><span style="color: #0000ff;">return</span> callback(<span style="color: #0000ff;">new</span> Error(<span style="color: #800000;">'</span><span style="color: #800000;">密码由字母、数字、下划线组成，长度为6～16个字符</span><span style="color: #800000;">'</span><span style="color: #000000;">));
        }
        callback()
    },
    validateBankNo: function(rule, value, callback){
        </span><span style="color: #0000ff;">var</span> reg = /^\d{<span style="color: #800080;">16</span>,<span style="color: #800080;">19</span>}$/
        <span style="color: #0000ff;">if</span>(value &amp;&amp; !<span style="color: #000000;">reg.test(value)) {
            </span><span style="color: #0000ff;">return</span> callback(<span style="color: #0000ff;">new</span> Error(<span style="color: #800000;">'</span><span style="color: #800000;">银行卡号格式有误</span><span style="color: #800000;">'</span><span style="color: #000000;">))
        }
        callback();
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">定义验证规则</span></div>
<div class="cnblogs_code">
<pre><span style="color: #008000;">&lt;!--</span><span style="color: #008000;">from表单：</span><span style="color: #008000;">--&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">el-dialog </span><span style="color: #ff0000;">title</span><span style="color: #0000ff;">="补全机构信息"</span><span style="color: #ff0000;"> :visible.sync</span><span style="color: #0000ff;">="dialogEnterpriseVisible"</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">el-form </span><span style="color: #ff0000;">:model</span><span style="color: #0000ff;">="enterpriseForm"</span><span style="color: #ff0000;"> :rules</span><span style="color: #0000ff;">="enterpriseFormRules"</span><span style="color: #ff0000;"> ref</span><span style="color: #0000ff;">="enterpriseForm"</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">el-form-item </span><span style="color: #ff0000;">label</span><span style="color: #0000ff;">="机构类型："</span><span style="color: #ff0000;"> prop</span><span style="color: #0000ff;">="func_type"</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">el-select </span><span style="color: #ff0000;">v-model</span><span style="color: #0000ff;">="enterpriseForm.func_type"</span><span style="color: #ff0000;"> placeholder</span><span style="color: #0000ff;">="机构类型"</span><span style="color: #0000ff;">&gt;</span>
          <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">el-option </span><span style="color: #ff0000;">v-for</span><span style="color: #0000ff;">="ft in functypes"</span><span style="color: #ff0000;"> :key</span><span style="color: #0000ff;">="ft.name"</span><span style="color: #ff0000;"> :value</span><span style="color: #0000ff;">="ft.name"</span><span style="color: #ff0000;"> :value</span><span style="color: #0000ff;">="ft.name"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">el-option</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">el-select</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">el-form-item</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">el-form-item </span><span style="color: #ff0000;">label</span><span style="color: #0000ff;">="机构名称："</span><span style="color: #ff0000;"> prop</span><span style="color: #0000ff;">="name"</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">el-input </span><span style="color: #ff0000;">v-model</span><span style="color: #0000ff;">="enterpriseForm.name"</span><span style="color: #ff0000;"> placeholder</span><span style="color: #0000ff;">="机构名称"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">el-input</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">el-form-item</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">el-form</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">slot</span><span style="color: #0000ff;">="footer"</span><span style="color: #ff0000;"> class</span><span style="color: #0000ff;">="dialog-footer"</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">el-button </span><span style="color: #ff0000;">@click</span><span style="color: #0000ff;">="dialogEnterpriseVisible = false"</span><span style="color: #0000ff;">&gt;</span>取 消<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">el-button</span><span style="color: #0000ff;">&gt;</span>
      <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">el-button </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="primary"</span><span style="color: #ff0000;"> @click</span><span style="color: #0000ff;">="AddEnterprise"</span><span style="color: #0000ff;">&gt;</span>继续<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">el-button</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">el-dialog</span><span style="color: #0000ff;">&gt;</span>


<span style="color: #008000;">&lt;!--</span><span style="color: #008000;">数据：</span><span style="color: #008000;">--&gt;</span><span style="color: #000000;">
functypes:[],
enterpriseForm:{
    func_type:'',
    name:''
},
enterpriseFormRules:{
    func_type:[{required: true, message: '请选择机构类型', trigger: 'change'}],
    name:[{required: true, message: '请输入机构名称', trigger: 'blur'}]
},

</span><span style="color: #008000;">&lt;!--</span><span style="color: #008000;">方法：</span><span style="color: #008000;">--&gt;</span><span style="color: #000000;">
AddEnterprise:function(){
    var vm = this
    vm.$refs['enterpriseForm'].validate(function (valid) {
        if(valid){
            
        }else{
           
        }
    })
}</span></pre>
</div>
<p>单独对一个input验证：&nbsp;<span class="cnblogs_code">vm.$refs[<span style="color: #800000;">'</span><span style="color: #800000;">user</span><span style="color: #800000;">'</span>].validateField(<span style="color: #800000;">"name</span><span style="color: #800000;">"</span>)</span>&nbsp;</p>
<div class="cnblogs_code">
<pre>vm.$refs[<span style="color: #800000;">'</span><span style="color: #800000;">user</span><span style="color: #800000;">'</span>].validateField(<span style="color: #800000;">"</span><span style="color: #800000;">mobile</span><span style="color: #800000;">"</span><span style="color: #000000;">,function(msg){
                        </span><span style="color: #0000ff;">if</span>(msg!=<span style="color: #0000ff;">null</span>&amp;&amp;msg!=<span style="color: #800000;">""</span>)<span style="color: #0000ff;">return</span>
                        <span style="color: #0000ff;">else</span><span style="color: #000000;">
                        {
                            alert(</span><span style="color: #800000;">"</span><span style="color: #800000;">asdasd</span><span style="color: #800000;">"</span><span style="color: #000000;">)
                        }

                    })</span></pre>
</div>
<p>&nbsp;</p>
<p>①文本验证&nbsp;<span class="cnblogs_code">{required: true, message: '请输入项目名称', trigger: 'blur'}</span>&nbsp;</p>
<p>②下拉框验证&nbsp;<span class="cnblogs_code">{required: true, message: '请选择项目类型', trigger: 'change'}</span>&nbsp;</p>
<p>③自定义验证</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">{ required: true, validator: validateRegion, trigger: 'change' }

function validateRegion(rule, value, callback) {
            if (!VM.selectedProvince || !VM.selectedCity || !VM.selectedArea) {
                return callback(new Error('请选择省市区'));
            }
            callback();
        };</span></pre>
</div>
<p>④长度验证&nbsp;<span class="cnblogs_code">{min: 1, max: 50, message: '长度在 1 到 50 个字符', trigger: 'blur'}</span>&nbsp;&nbsp;</p>
<p>⑤日期选择验证&nbsp;<span class="cnblogs_code">{ type: 'date', required: true, message: '请选择时间', trigger: 'change' }</span>&nbsp;&nbsp;</p>
<p>⑥金额验证（可有小数点）：</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('c0eac409-5d14-4d86-97e9-dc44dc204aa8')"><img id="code_img_closed_c0eac409-5d14-4d86-97e9-dc44dc204aa8" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_c0eac409-5d14-4d86-97e9-dc44dc204aa8" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('c0eac409-5d14-4d86-97e9-dc44dc204aa8',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_c0eac409-5d14-4d86-97e9-dc44dc204aa8" class="cnblogs_code_hide">
<pre><span style="color: #000000;">function validatorApplyAmountRequired(rule, value, callback) {
            if (value == '' || value == null) {
                return callback(new Error("输入不能为空"));
            }
            if (!isGreaterZeroNumber(value)) {
                return callback(new Error("请输入格式有误"));
            }
            callback();
        };

//验证V是否是大于0
function isGreaterZeroNumber(v) {
    if (isNaN(v) || !v) {
        return false;
    }
    if (v </span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;"> 0</span><span style="color: #ff0000;">) {
        return false;
    }
    return true;
}</span></pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<p>&nbsp;⑦值下拉框验证：</p>
<div class="cnblogs_code">
<pre>[{required: <span style="color: #0000ff;">true</span>,type:<span style="color: #800000;">"</span><span style="color: #800000;">number</span><span style="color: #800000;">"</span>,message: <span style="color: #800000;">'</span><span style="color: #800000;">请选择项目</span><span style="color: #800000;">'</span>, trigger: <span style="color: #800000;">'</span><span style="color: #800000;">change</span><span style="color: #800000;">'</span>}]</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>2，返回上一级</p>
<div class="cnblogs_code">
<pre>handleBack: <span style="color: #0000ff;">function</span><span style="color: #000000;">(obj){
            window.location.href </span>=<span style="color: #000000;"> document.referrer; 
            </span><span style="color: #008000;">//</span><span style="color: #008000;">window.history.go(-1) 不刷新</span>
        }</pre>
</div>
<p>&nbsp;</p>
<p>3，调用子iframe里面的方法</p>
<div class="cnblogs_code">
<pre> 
 <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> page content begin </span><span style="color: #008000;">--&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="main"</span><span style="color: #ff0000;"> id</span><span style="color: #0000ff;">="main"</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">iframe </span><span style="color: #ff0000;">id</span><span style="color: #0000ff;">="mainFrame"</span><span style="color: #ff0000;"> name</span><span style="color: #0000ff;">="mainFrame"</span><span style="color: #ff0000;"> src</span><span style="color: #0000ff;">=""</span><span style="color: #ff0000;"> width</span><span style="color: #0000ff;">="100%"</span><span style="color: #ff0000;"> height</span><span style="color: #0000ff;">="100%"</span><span style="color: #ff0000;"> frameborder</span><span style="color: #0000ff;">=0 </span><span style="color: #ff0000;">style</span><span style="color: #0000ff;">="background-color: transparent;"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">iframe</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> page content end </span><span style="color: #008000;">--&gt;</span><span style="color: #000000;">

//调用子页面flushSubData方法
                    try{
                        $(window.parent.document).contents().find("#mainFrame")[0].contentWindow.flushSubData(); 
                    }catch(err){}</span></pre>
</div>
<p>&nbsp;</p>
<p>3，input效果</p>
<p><img src="https://images2018.cnblogs.com/blog/741594/201804/741594-20180410164534630-557639368.png" alt="" /></p>
<div class="cnblogs_code">
<pre> &lt;el-input <span style="color: #0000ff;">class</span>=<span style="color: #800000;">"</span><span style="color: #800000;">input-m</span><span style="color: #800000;">"</span> type=<span style="color: #800000;">"</span><span style="color: #800000;">number</span><span style="color: #800000;">"</span> min=<span style="color: #800000;">"</span><span style="color: #800000;">0</span><span style="color: #800000;">"</span> v-model.trim=<span style="color: #800000;">"</span><span style="color: #800000;">formProject.months</span><span style="color: #800000;">"</span>&gt;
                            &lt;template slot=<span style="color: #800000;">"</span><span style="color: #800000;">append</span><span style="color: #800000;">"</span>&gt;<span style="color: #000000;">
                                    月
                              </span>&lt;/template&gt;
                    &lt;/el-input&gt;</pre>
</div>
<p>&nbsp;</p>
<p>4，使用Echarts</p>
<p>①快速使用Echarts</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('5c7282f6-5ec4-47b1-8a45-14829dd29f1f')"><img id="code_img_closed_5c7282f6-5ec4-47b1-8a45-14829dd29f1f" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_5c7282f6-5ec4-47b1-8a45-14829dd29f1f" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('5c7282f6-5ec4-47b1-8a45-14829dd29f1f',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_5c7282f6-5ec4-47b1-8a45-14829dd29f1f" class="cnblogs_code_hide">
<pre>&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
    &lt;meta charset=<span style="color: #800000;">"</span><span style="color: #800000;">utf-8</span><span style="color: #800000;">"</span>&gt;
    &lt;!-- 引入 ECharts 文件 --&gt;
    &lt;script src=<span style="color: #800000;">"</span><span style="color: #800000;">echarts.min.js</span><span style="color: #800000;">"</span>&gt;&lt;/script&gt;
&lt;/head&gt;
&lt;/html&gt;</pre>
</div>
<span class="cnblogs_code_collapse">引入jse</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('7d630b14-84ba-44ac-8ec6-3f01710894a6')"><img id="code_img_closed_7d630b14-84ba-44ac-8ec6-3f01710894a6" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_7d630b14-84ba-44ac-8ec6-3f01710894a6" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('7d630b14-84ba-44ac-8ec6-3f01710894a6',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_7d630b14-84ba-44ac-8ec6-3f01710894a6" class="cnblogs_code_hide">
<pre>&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
    &lt;meta charset=<span style="color: #800000;">"</span><span style="color: #800000;">utf-8</span><span style="color: #800000;">"</span>&gt;
    &lt;title&gt;ECharts&lt;/title&gt;
    &lt;!-- 引入 echarts.js --&gt;
    &lt;script src=<span style="color: #800000;">"</span><span style="color: #800000;">echarts.min.js</span><span style="color: #800000;">"</span>&gt;&lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
    &lt;!-- 为ECharts准备一个具备大小（宽高）的Dom --&gt;
    &lt;div id=<span style="color: #800000;">"</span><span style="color: #800000;">main</span><span style="color: #800000;">"</span> style=<span style="color: #800000;">"</span><span style="color: #800000;">width: 600px;height:400px;</span><span style="color: #800000;">"</span>&gt;&lt;/div&gt;
    &lt;script type=<span style="color: #800000;">"</span><span style="color: #800000;">text/javascript</span><span style="color: #800000;">"</span>&gt;
        <span style="color: #008000;">//</span><span style="color: #008000;"> 基于准备好的dom，初始化echarts实例</span>
        <span style="color: #0000ff;">var</span> myChart = echarts.init(document.getElementById(<span style="color: #800000;">'</span><span style="color: #800000;">main</span><span style="color: #800000;">'</span><span style="color: #000000;">));

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 指定图表的配置项和数据</span>
        <span style="color: #0000ff;">var</span> option =<span style="color: #000000;"> {
            title: {
                text: </span><span style="color: #800000;">'</span><span style="color: #800000;">ECharts 入门示例</span><span style="color: #800000;">'</span><span style="color: #000000;">
            },
            tooltip: {},
            legend: {
                data:[</span><span style="color: #800000;">'</span><span style="color: #800000;">销量</span><span style="color: #800000;">'</span><span style="color: #000000;">]
            },
            xAxis: {
                data: [</span><span style="color: #800000;">"</span><span style="color: #800000;">衬衫</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">羊毛衫</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">雪纺衫</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">裤子</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">高跟鞋</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">袜子</span><span style="color: #800000;">"</span><span style="color: #000000;">]
            },
            yAxis: {},
            series: [{
                name: </span><span style="color: #800000;">'</span><span style="color: #800000;">销量</span><span style="color: #800000;">'</span><span style="color: #000000;">,
                type: </span><span style="color: #800000;">'</span><span style="color: #800000;">bar</span><span style="color: #800000;">'</span><span style="color: #000000;">,
                data: [</span><span style="color: #800080;">5</span>, <span style="color: #800080;">20</span>, <span style="color: #800080;">36</span>, <span style="color: #800080;">10</span>, <span style="color: #800080;">10</span>, <span style="color: #800080;">20</span><span style="color: #000000;">]
            }]
        };

        </span><span style="color: #008000;">//</span><span style="color: #008000;"> 使用刚指定的配置项和数据显示图表。</span>
<span style="color: #000000;">        myChart.setOption(option);
    </span>&lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;</pre>
</div>
<span class="cnblogs_code_collapse">绘制一个简单的图表</span></div>
<p>②使用主题</p>
<p>下载主题：<a href="http://echarts.baidu.com/download-theme.html" target="_blank">http://echarts.baidu.com/download-theme.html</a></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('9a800904-1279-4af5-bbce-db78e621d687')"><img id="code_img_closed_9a800904-1279-4af5-bbce-db78e621d687" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_9a800904-1279-4af5-bbce-db78e621d687" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('9a800904-1279-4af5-bbce-db78e621d687',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_9a800904-1279-4af5-bbce-db78e621d687" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="echarts.js"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> 引入 vintage 主题 </span><span style="color: #008000;">--&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="theme/vintage.js"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
<span style="background-color: #f5f5f5; color: #008000;">//</span><span style="background-color: #f5f5f5; color: #008000;"> 第二个参数可以指定前面引入的主题</span>
<span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> chart </span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;"> echarts.init(document.getElementById(</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">main</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">), </span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">vintage</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">);
chart.setOption({
    ...
});
</span><span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<span class="cnblogs_code_collapse">实例</span></div>
<p>③vue使用Echarts案例</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('123b0675-fd0e-4cb9-a237-88ea8d87c698')"><img id="code_img_closed_123b0675-fd0e-4cb9-a237-88ea8d87c698" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_123b0675-fd0e-4cb9-a237-88ea8d87c698" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('123b0675-fd0e-4cb9-a237-88ea8d87c698',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_123b0675-fd0e-4cb9-a237-88ea8d87c698" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">&lt;!</span><span style="color: #ff00ff;">DOCTYPE html</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">html</span><span style="color: #0000ff;">&gt;</span>

<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">head</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">meta </span><span style="color: #ff0000;">charset</span><span style="color: #0000ff;">="UTF-8"</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">meta </span><span style="color: #ff0000;">http-equiv</span><span style="color: #0000ff;">="X-UA-Compatible"</span><span style="color: #ff0000;"> content</span><span style="color: #0000ff;">="IE=edge"</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">meta </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="viewport"</span><span style="color: #ff0000;"> content</span><span style="color: #0000ff;">="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0"</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">meta </span><span style="color: #ff0000;">content</span><span style="color: #0000ff;">="瓯云"</span><span style="color: #ff0000;"> name</span><span style="color: #0000ff;">="description"</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">meta </span><span style="color: #ff0000;">content</span><span style="color: #0000ff;">="瓯云"</span><span style="color: #ff0000;"> name</span><span style="color: #0000ff;">="author"</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">link </span><span style="color: #ff0000;">href</span><span style="color: #0000ff;">="/favicon.ico"</span><span style="color: #ff0000;"> rel</span><span style="color: #0000ff;">="icon"</span><span style="color: #ff0000;"> type</span><span style="color: #0000ff;">="image/x-icon"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">title</span><span style="color: #0000ff;">&gt;</span>劳动力分析<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">title</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">link </span><span style="color: #ff0000;">rel</span><span style="color: #0000ff;">="stylesheet"</span><span style="color: #ff0000;"> href</span><span style="color: #0000ff;">="../../lib/elementui/elementui-1.4.1.css"</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">link </span><span style="color: #ff0000;">rel</span><span style="color: #0000ff;">="stylesheet"</span><span style="color: #ff0000;"> href</span><span style="color: #0000ff;">="../../css/common.css?v=20171219001"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">link </span><span style="color: #ff0000;">rel</span><span style="color: #0000ff;">="stylesheet"</span><span style="color: #ff0000;"> href</span><span style="color: #0000ff;">="../../css/console.css?v=20171219001"</span> <span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="../../lib/jquery-1.9.1.min.js"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">language</span><span style="color: #0000ff;">="javascript"</span><span style="color: #ff0000;"> src</span><span style="color: #0000ff;">="../../lib/jquery.base64.js"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="../../lib/jquery.cookie.js"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="../../lib/elementui/vue-2.4.2.js"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="../../lib/elementui/elementui-1.4.1.js"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="../../lib/echarts/echarts-3.6.2.min.js"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="../../lib/echarts/macarons.js"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="../../lib/JSLINQ.js"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="../../js/console.js?v=20171219001"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="../../js/utils.js?v=20171219001"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>


<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">head</span><span style="color: #0000ff;">&gt;</span>

<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">body </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="frame-body"</span><span style="color: #0000ff;">&gt;</span>

    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="wrap"</span><span style="color: #ff0000;"> id</span><span style="color: #0000ff;">="oyunVue"</span><span style="color: #ff0000;"> v-loading.fullscreen.lock</span><span style="color: #0000ff;">="loading"</span><span style="color: #ff0000;"> element-loading-text</span><span style="color: #0000ff;">=""</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> 导航条 </span><span style="color: #008000;">--&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="breadcrumb clearfix"</span><span style="color: #0000ff;">&gt;&lt;</span><span style="color: #800000;">h2</span><span style="color: #0000ff;">&gt;</span>劳动力分析<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">h2</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
         <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> 搜索条件 start </span><span style="color: #008000;">--&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="clearfix"</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">el-form </span><span style="color: #ff0000;">:model</span><span style="color: #0000ff;">="searchForm"</span><span style="color: #ff0000;"> :inline</span><span style="color: #0000ff;">="true"</span><span style="color: #ff0000;"> class</span><span style="color: #0000ff;">="demo-form-inline"</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">el-form-item</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">el-select </span><span style="color: #ff0000;">v-model</span><span style="color: #0000ff;">="searchForm.org_name"</span><span style="color: #ff0000;"> clearable placeholder</span><span style="color: #0000ff;">="请选择"</span><span style="color: #0000ff;">&gt;</span>
                            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">el-option
                                </span><span style="color: #ff0000;">v-for</span><span style="color: #0000ff;">="item in groupData"</span><span style="color: #ff0000;">
                                :key</span><span style="color: #0000ff;">="item.ent_name"</span><span style="color: #ff0000;">
                                :label</span><span style="color: #0000ff;">="item.ent_name"</span><span style="color: #ff0000;">
                                :value</span><span style="color: #0000ff;">="item.ent_name"</span><span style="color: #0000ff;">&gt;</span>
                            <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">el-option</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">el-select</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">el-form-item</span><span style="color: #0000ff;">&gt;</span>
                
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">el-form-item</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">el-button </span><span style="color: #ff0000;">:loading</span><span style="color: #0000ff;">="searchLoading"</span><span style="color: #ff0000;"> type</span><span style="color: #0000ff;">="primary"</span><span style="color: #ff0000;"> icon</span><span style="color: #0000ff;">="search"</span><span style="color: #ff0000;"> @click</span><span style="color: #0000ff;">="fnSearch"</span><span style="color: #0000ff;">&gt;</span>搜索<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">el-button</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">el-form-item</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">el-form</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>


        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">el-tabs </span><span style="color: #ff0000;">v-model</span><span style="color: #0000ff;">="activeName"</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">el-tab-pane </span><span style="color: #ff0000;">label</span><span style="color: #0000ff;">="工种分布表"</span><span style="color: #ff0000;"> name</span><span style="color: #0000ff;">="first"</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">id</span><span style="color: #0000ff;">="worktype"</span><span style="color: #ff0000;"> style</span><span style="color: #0000ff;">="width: 800px;height:400px;margin-left: 100px;margin-top: 20px"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">el-tab-pane</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">el-tab-pane </span><span style="color: #ff0000;">label</span><span style="color: #0000ff;">="籍贯分布表"</span><span style="color: #ff0000;"> name</span><span style="color: #0000ff;">="second"</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">id</span><span style="color: #0000ff;">="native"</span><span style="color: #ff0000;"> style</span><span style="color: #0000ff;">="width: 800px;height:400px;margin-left: 100px;margin-top: 20px"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">el-tab-pane</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">el-tab-pane </span><span style="color: #ff0000;">label</span><span style="color: #0000ff;">="年龄段分布表"</span><span style="color: #ff0000;"> name</span><span style="color: #0000ff;">="third"</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">id</span><span style="color: #0000ff;">="age"</span><span style="color: #ff0000;"> style</span><span style="color: #0000ff;">="width: 800px;height:400px;margin-left: 100px;margin-top: 20px"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">el-tab-pane</span><span style="color: #0000ff;">&gt;</span>
          <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">el-tabs</span><span style="color: #0000ff;">&gt;</span>



       
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
    <span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> vueOptions </span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;"> {
        data: {
            activeName: </span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">first</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">,
            getGroupDataApi:</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">ProjectEnterprise/GetList</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">,
            groupData:[],
            searchForm: {
                    prj_id: </span><span style="background-color: #f5f5f5; color: #000000;">''</span><span style="background-color: #f5f5f5; color: #000000;">,
                    org_name: </span><span style="background-color: #f5f5f5; color: #000000;">''</span><span style="background-color: #f5f5f5; color: #000000;">,
                },
           worktypeData:[],
           worktypeChart:{},
           nativeChart:{}
        },
        mounted: </span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;">() {
            </span><span style="background-color: #f5f5f5; color: #0000ff;">this</span><span style="background-color: #f5f5f5; color: #000000;">.pageAuth(</span><span style="background-color: #f5f5f5; color: #000000;">747981802455041</span><span style="background-color: #f5f5f5; color: #000000;">)
            </span><span style="background-color: #f5f5f5; color: #0000ff;">this</span><span style="background-color: #f5f5f5; color: #000000;">.projectAuth()
            </span><span style="background-color: #f5f5f5; color: #0000ff;">this</span><span style="background-color: #f5f5f5; color: #000000;">.getgroups()
            </span><span style="background-color: #f5f5f5; color: #0000ff;">this</span><span style="background-color: #f5f5f5; color: #000000;">.fnSearch()
            </span><span style="background-color: #f5f5f5; color: #0000ff;">this</span><span style="background-color: #f5f5f5; color: #000000;">.worktypeChart </span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;"> echarts.init(document.getElementById(</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">worktype</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">),</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">macarons</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">);
            </span><span style="background-color: #f5f5f5; color: #0000ff;">this</span><span style="background-color: #f5f5f5; color: #000000;">.nativeChart </span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;"> echarts.init(document.getElementById(</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">native</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">),</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">macarons</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">);
            </span><span style="background-color: #f5f5f5; color: #0000ff;">this</span><span style="background-color: #f5f5f5; color: #000000;">.ageChart </span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;"> echarts.init(document.getElementById(</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">age</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">),</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">macarons</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">);

        },
        methods: {
           </span><span style="background-color: #f5f5f5; color: #008000;">//</span><span style="background-color: #f5f5f5; color: #008000;">查询班组</span>
<span style="background-color: #f5f5f5; color: #000000;">                getgroups:</span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;">(){
                    </span><span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> vm</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #0000ff;">this</span>
                    <span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> option</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;">{
                        data:{
                            pageindex:</span><span style="background-color: #f5f5f5; color: #000000;">1</span><span style="background-color: #f5f5f5; color: #000000;">,
                            pagesize:</span><span style="background-color: #f5f5f5; color: #000000;">9999</span><span style="background-color: #f5f5f5; color: #000000;">,
                            parameter:{
                                prj_id:getCurrentProjectId()
                            }
                        },
                        route:vm.getGroupDataApi,
                        success:</span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;">(res){
                            vm.groupData</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;">res.data
                        }
                    }
                    $.ajaxExt(option)
                },
                fnSearch:</span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;">(){
                    </span><span style="background-color: #f5f5f5; color: #0000ff;">this</span><span style="background-color: #f5f5f5; color: #000000;">.getgroups()
                    </span><span style="background-color: #f5f5f5; color: #0000ff;">this</span><span style="background-color: #f5f5f5; color: #000000;">.fnGetWorktype()
                    </span><span style="background-color: #f5f5f5; color: #0000ff;">this</span><span style="background-color: #f5f5f5; color: #000000;">.fnNative()
                    </span><span style="background-color: #f5f5f5; color: #0000ff;">this</span><span style="background-color: #f5f5f5; color: #000000;">.fnAge()
                },
                fnAge:</span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;">(){
                    </span><span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> vm</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #0000ff;">this</span><span style="background-color: #f5f5f5; color: #000000;">
                    vm.searchForm.prj_id</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;">getCurrentProjectId()
                    </span><span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> option</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;">{
                        data:{
                            parameter:vm.searchForm
                        },
                        route:</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">UsrEmployee/GetEmployeeAgeStatistics</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">,
                        success:</span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;">(res)
                        {
                            </span><span style="background-color: #f5f5f5; color: #0000ff;">if</span><span style="background-color: #f5f5f5; color: #000000;">(res.ret</span><span style="background-color: #f5f5f5; color: #000000;">!=</span><span style="background-color: #f5f5f5; color: #000000;">0</span><span style="background-color: #f5f5f5; color: #000000;">||</span><span style="background-color: #f5f5f5; color: #000000;">res.data</span><span style="background-color: #f5f5f5; color: #000000;">==</span><span style="background-color: #f5f5f5; color: #000000;">''</span><span style="background-color: #f5f5f5; color: #000000;">||</span><span style="background-color: #f5f5f5; color: #000000;">res.data</span><span style="background-color: #f5f5f5; color: #000000;">==</span><span style="background-color: #f5f5f5; color: #0000ff;">null</span><span style="background-color: #f5f5f5; color: #000000;">||</span><span style="background-color: #f5f5f5; color: #000000;">res.data.length</span><span style="background-color: #f5f5f5; color: #000000;">&lt;=</span><span style="background-color: #f5f5f5; color: #000000;">0</span><span style="background-color: #f5f5f5; color: #000000;">)
                            {
                                vm.ageChart.setOption(vm.fnAgeChart(</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">年龄段分布统计</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">,[],[]))
                                </span><span style="background-color: #f5f5f5; color: #0000ff;">return</span><span style="background-color: #f5f5f5; color: #000000;">;
                            }
                            
                            </span><span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> fullnames</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;"> JSLINQ(res.data).Select(x</span><span style="background-color: #f5f5f5; color: #000000;">=&gt;</span><span style="background-color: #f5f5f5; color: #000000;">x.fullname).ToArray();
                            </span><span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> data</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;"> JSLINQ(res.data).Select(x</span><span style="background-color: #f5f5f5; color: #000000;">=&gt;</span><span style="background-color: #f5f5f5; color: #000000;">x.age).ToArray();
                            </span><span style="background-color: #f5f5f5; color: #008000;">//</span><span style="background-color: #f5f5f5; color: #008000;"> var data= new Array()</span>
                            <span style="background-color: #f5f5f5; color: #008000;">//</span><span style="background-color: #f5f5f5; color: #008000;"> for(var i=0;i&lt;res.data.length;i++)</span>
                            <span style="background-color: #f5f5f5; color: #008000;">//</span><span style="background-color: #f5f5f5; color: #008000;"> {</span>
                            <span style="background-color: #f5f5f5; color: #008000;">//</span><span style="background-color: #f5f5f5; color: #008000;">     data.push({value:res.data[i].age,name:res.data[i].fullname})</span>
                            <span style="background-color: #f5f5f5; color: #008000;">//</span><span style="background-color: #f5f5f5; color: #008000;"> }                            </span>
<span style="background-color: #f5f5f5; color: #000000;">                            
                            vm.ageChart.setOption(vm.fnAgeChart(</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">年龄段分布统计</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">,fullnames,data))
                        }
                    }
                    $.ajaxExt(option)
                },
                fnNative:</span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;">(){
                    </span><span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> vm</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #0000ff;">this</span><span style="background-color: #f5f5f5; color: #000000;">
                    vm.searchForm.prj_id</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;">getCurrentProjectId()
                    </span><span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> option</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;">{
                        data:{
                            parameter:vm.searchForm
                        },
                        route:</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">UsrEmployee/GetEmployeeNativeStatistics</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">,
                        success:</span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;">(res)
                        {
                            </span><span style="background-color: #f5f5f5; color: #0000ff;">if</span><span style="background-color: #f5f5f5; color: #000000;">(res.ret</span><span style="background-color: #f5f5f5; color: #000000;">!=</span><span style="background-color: #f5f5f5; color: #000000;">0</span><span style="background-color: #f5f5f5; color: #000000;">||</span><span style="background-color: #f5f5f5; color: #000000;">res.data</span><span style="background-color: #f5f5f5; color: #000000;">==</span><span style="background-color: #f5f5f5; color: #000000;">''</span><span style="background-color: #f5f5f5; color: #000000;">||</span><span style="background-color: #f5f5f5; color: #000000;">res.data</span><span style="background-color: #f5f5f5; color: #000000;">==</span><span style="background-color: #f5f5f5; color: #0000ff;">null</span><span style="background-color: #f5f5f5; color: #000000;">||</span><span style="background-color: #f5f5f5; color: #000000;">res.data.length</span><span style="background-color: #f5f5f5; color: #000000;">&lt;=</span><span style="background-color: #f5f5f5; color: #000000;">0</span><span style="background-color: #f5f5f5; color: #000000;">){
                                vm.nativeChart.setOption(vm.fnPieChart(</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">籍贯分布统计</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">,[],[]))
                                </span><span style="background-color: #f5f5f5; color: #0000ff;">return</span><span style="background-color: #f5f5f5; color: #000000;">;
                            }
                            
                            </span><span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> natives</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;"> JSLINQ(res.data).Select(x</span><span style="background-color: #f5f5f5; color: #000000;">=&gt;</span><span style="background-color: #f5f5f5; color: #000000;">x.native).ToArray();
                            </span><span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> data</span><span style="background-color: #f5f5f5; color: #000000;">=</span> <span style="background-color: #f5f5f5; color: #0000ff;">new</span><span style="background-color: #f5f5f5; color: #000000;"> Array()
                            </span><span style="background-color: #f5f5f5; color: #0000ff;">for</span><span style="background-color: #f5f5f5; color: #000000;">(</span><span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> i</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;">0</span><span style="background-color: #f5f5f5; color: #000000;">;i</span><span style="background-color: #f5f5f5; color: #000000;">&lt;</span><span style="background-color: #f5f5f5; color: #000000;">res.data.length;i</span><span style="background-color: #f5f5f5; color: #000000;">++</span><span style="background-color: #f5f5f5; color: #000000;">)
                            {
                                data.push({value:res.data[i].count,name:res.data[i].native})
                            }                            
                            
                            vm.nativeChart.setOption(vm.fnPieChart(</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">籍贯分布统计</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">,natives,data))
                        }
                    }
                    $.ajaxExt(option)
                },
                fnGetWorktype:</span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;">(){
                    </span><span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> vm</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #0000ff;">this</span><span style="background-color: #f5f5f5; color: #000000;">
                    vm.searchForm.prj_id</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;">getCurrentProjectId()
                    </span><span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> option</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;">{
                        data:{
                            parameter:vm.searchForm
                        },
                        route:</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">UsrEmployee/GetEmployeeWorktypeStatistics</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">,
                        success:</span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;">(res)
                        {
                            </span><span style="background-color: #f5f5f5; color: #0000ff;">if</span><span style="background-color: #f5f5f5; color: #000000;">(res.ret</span><span style="background-color: #f5f5f5; color: #000000;">!=</span><span style="background-color: #f5f5f5; color: #000000;">0</span><span style="background-color: #f5f5f5; color: #000000;">||</span><span style="background-color: #f5f5f5; color: #000000;">res.data</span><span style="background-color: #f5f5f5; color: #000000;">==</span><span style="background-color: #f5f5f5; color: #000000;">''</span><span style="background-color: #f5f5f5; color: #000000;">||</span><span style="background-color: #f5f5f5; color: #000000;">res.data</span><span style="background-color: #f5f5f5; color: #000000;">==</span><span style="background-color: #f5f5f5; color: #0000ff;">null</span><span style="background-color: #f5f5f5; color: #000000;">||</span><span style="background-color: #f5f5f5; color: #000000;">res.data.length</span><span style="background-color: #f5f5f5; color: #000000;">&lt;=</span><span style="background-color: #f5f5f5; color: #000000;">0</span><span style="background-color: #f5f5f5; color: #000000;">)
                            {
                                vm.worktypeChart.setOption(vm.fnPieChart(</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">工种分布统计</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">,[],[]))   
                                </span><span style="background-color: #f5f5f5; color: #0000ff;">return</span><span style="background-color: #f5f5f5; color: #000000;">;
                            }
                            
                            </span><span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> worktypes</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;"> JSLINQ(res.data).Select(x</span><span style="background-color: #f5f5f5; color: #000000;">=&gt;</span><span style="background-color: #f5f5f5; color: #000000;">x.worktype).ToArray();
                            </span><span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> data</span><span style="background-color: #f5f5f5; color: #000000;">=</span> <span style="background-color: #f5f5f5; color: #0000ff;">new</span><span style="background-color: #f5f5f5; color: #000000;"> Array()
                            </span><span style="background-color: #f5f5f5; color: #0000ff;">for</span><span style="background-color: #f5f5f5; color: #000000;">(</span><span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> i</span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;">0</span><span style="background-color: #f5f5f5; color: #000000;">;i</span><span style="background-color: #f5f5f5; color: #000000;">&lt;</span><span style="background-color: #f5f5f5; color: #000000;">res.data.length;i</span><span style="background-color: #f5f5f5; color: #000000;">++</span><span style="background-color: #f5f5f5; color: #000000;">)
                            {
                                data.push({value:res.data[i].icount,name:res.data[i].worktype})
                            }                            
                            
                            vm.worktypeChart.setOption(vm.fnPieChart(</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">工种分布统计</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">,worktypes,data))
                        }
                    }
                    $.ajaxExt(option)
                },
                fnPieChart:</span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;">(title,names,datas){
                  </span><span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;">  option </span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;"> {
                                title : {
                                    text: title,
                                    x:</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">center</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">
                                },
                                tooltip : {
                                    trigger: </span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">item</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">,
                                    formatter: </span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">{a} &lt;br/&gt;{b} : {c} ({d}%)</span><span style="background-color: #f5f5f5; color: #000000;">"</span><span style="background-color: #f5f5f5; color: #000000;">
                                },
                                legend: {
                                    orient : </span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">vertical</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">,
                                    x : </span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">left</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">,
                                    data:names
                                },
                                calculable : </span><span style="background-color: #f5f5f5; color: #0000ff;">true</span><span style="background-color: #f5f5f5; color: #000000;">,
                                series : [
                                    {
                                        name:</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">访问来源</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">,
                                        type:</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">pie</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">,
                                        radius : </span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">55%</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">,
                                        center: [</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">50%</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">, </span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">60%</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">],
                                        data:datas
                                    }
                                ]
                            };
                    </span><span style="background-color: #f5f5f5; color: #0000ff;">return</span><span style="background-color: #f5f5f5; color: #000000;"> option;
                },
                fnAgeChart:</span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;">(title,names,datas)
                {
                   </span><span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> option </span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;"> {
                        title : {
                            text: title,
                        },
                        tooltip : {
                            trigger: </span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">axis</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">
                        },
                        legend: {
                            data:[</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">年龄</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">]
                        },
                        calculable : </span><span style="background-color: #f5f5f5; color: #0000ff;">true</span><span style="background-color: #f5f5f5; color: #000000;">,
                        xAxis : [
                            {
                                type : </span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">category</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">,
                                boundaryGap : </span><span style="background-color: #f5f5f5; color: #0000ff;">false</span><span style="background-color: #f5f5f5; color: #000000;">,
                                data : names
                            }
                        ],
                        yAxis : [
                            {
                                type : </span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">value</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">,
                                axisLabel : {
                                    formatter: </span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">{value}岁</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">
                                }
                            }
                        ],
                        series : [
                            {
                                name:</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">年龄</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">,
                                type:</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">line</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">,
                                data:datas,
                                markPoint : {
                                    data : [
                                        {type : </span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">max</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">, name: </span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">最大值</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">},
                                        {type : </span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">min</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">, name: </span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">最小值</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">}
                                    ]
                                },
                                markLine : {
                                    data : [
                                        {type : </span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">average</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">, name: </span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">平均值</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">}
                                    ]
                                }
                            }
                        ]
                    };
                    </span><span style="background-color: #f5f5f5; color: #0000ff;">return</span><span style="background-color: #f5f5f5; color: #000000;"> option;                  
                }
        }
    }
    </span><span style="background-color: #f5f5f5; color: #0000ff;">var</span><span style="background-color: #f5f5f5; color: #000000;"> VM </span><span style="background-color: #f5f5f5; color: #000000;">=</span><span style="background-color: #f5f5f5; color: #000000;"> createVue(vueOptions);
    $(</span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;">(){
        $(</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">#advancedSearch</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">).on(</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">keypress</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">,</span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;">(e){
            </span><span style="background-color: #f5f5f5; color: #0000ff;">if</span><span style="background-color: #f5f5f5; color: #000000;">(e.keyCode </span><span style="background-color: #f5f5f5; color: #000000;">==</span> <span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">13</span><span style="background-color: #f5f5f5; color: #000000;">'</span><span style="background-color: #f5f5f5; color: #000000;">) {
                VM.fnSearch();
                </span><span style="background-color: #f5f5f5; color: #0000ff;">return</span> <span style="background-color: #f5f5f5; color: #0000ff;">false</span><span style="background-color: #f5f5f5; color: #000000;">;
            }
        })
    })

     </span><span style="background-color: #f5f5f5; color: #0000ff;">function</span><span style="background-color: #f5f5f5; color: #000000;"> flushSubData(){
            VM.fnSearch()
            VM.projectAuth()
        }

    </span><span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">body</span><span style="color: #0000ff;">&gt;</span>

<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">html</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<span class="cnblogs_code_collapse">案例</span></div>
<p>④设置x、y轴字体颜色</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('3e1198f4-738d-455f-b5a0-ff7ba018e678')"><img id="code_img_closed_3e1198f4-738d-455f-b5a0-ff7ba018e678" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_3e1198f4-738d-455f-b5a0-ff7ba018e678" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('3e1198f4-738d-455f-b5a0-ff7ba018e678',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_3e1198f4-738d-455f-b5a0-ff7ba018e678" class="cnblogs_code_hide">
<pre><span style="color: #000000;"> xAxis : [
                            {
                                type : 'category',
                                data : ['木工', '水泥工', '瓦工', '钢筋工', '油漆工', '塔吊工', '后勤人员'],
                                axisTick: {
                                    alignWithLabel: true
                                },
                                axisLabel: {
                                    show: true,
                                    textStyle: {
                                        color: '#fff'
                                    }
                                }
                                
                            }
                        ],
                        yAxis : [
                            {
                                type : 'value',
                                splitLine: {
                                    show: false
                                },
                                axisLabel : {
                                    formatter: '{value}',
                                    textStyle: {
                                        color: '#fff'
                                    }
                                }
                            }
                        ],</span></pre>
</div>
<span class="cnblogs_code_collapse">demo</span></div>
<p>&nbsp;</p>
<p>5，JSLINQ使用</p>
<p>官网：<a href="https://archive.codeplex.com/?p=jslinq" target="_blank">https://archive.codeplex.com/?p=jslinq</a></p>
<p>包/案例下载：<a href="https://pan.baidu.com/s/14QZvQ7gcEmhxoFV1fT-Mvw" target="_blank">https://pan.baidu.com/s/14QZvQ7gcEmhxoFV1fT-Mvw</a></p>
<p>①引入js</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('bc49225c-eeeb-4ee1-9f5f-2b1e4b184e48')"><img id="code_img_closed_bc49225c-eeeb-4ee1-9f5f-2b1e4b184e48" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_bc49225c-eeeb-4ee1-9f5f-2b1e4b184e48" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('bc49225c-eeeb-4ee1-9f5f-2b1e4b184e48',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_bc49225c-eeeb-4ee1-9f5f-2b1e4b184e48" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="../../lib/JSLINQ.js"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<p>②简单使用</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('8cf86a06-d587-4ad4-99e7-82ff48c253c4')"><img id="code_img_closed_8cf86a06-d587-4ad4-99e7-82ff48c253c4" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_8cf86a06-d587-4ad4-99e7-82ff48c253c4" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('8cf86a06-d587-4ad4-99e7-82ff48c253c4',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_8cf86a06-d587-4ad4-99e7-82ff48c253c4" class="cnblogs_code_hide">
<pre>var natives= JSLINQ(res.data).Select(x=&gt;x.native).ToArray();</pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<p>&nbsp;</p>