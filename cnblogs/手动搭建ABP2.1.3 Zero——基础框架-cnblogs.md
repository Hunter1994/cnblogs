<p><a href="#a1"><strong>一、基础层搭建</strong></a></p>
<p><a href="#a2"><strong><strong>二、PM.Core</strong></strong></a></p>
<p><a href="#a3"><strong>三、PM.EntityFramework</strong></a></p>
<p><a href="#a4"><strong><strong>四、PM.Application</strong></strong></a></p>
<p><a href="#a5"><strong>五、PM.WebApi</strong>&nbsp;</a></p>
<p><a href="#a6"><strong>六、PM.Web（MPA）</strong></a></p>
<p><a href="#a7"><strong>七、PM.Web（SPA）</strong></a></p>
<p><a href="#a8"><strong>八、单元测试</strong></a></p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;"><strong><a name="a1"></a>一、基础层搭建</strong></span></p>
<p><strong><span style="font-size: 16px;">1，创建一个空解决方案&nbsp;</span></strong></p>
<p><strong><span style="font-size: 16px;">2，层结构</span></strong></p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201710/741594-20171025102658738-1476614088.png" alt="" /></p>
<p>PM.Core[v:4.6]：类库</p>
<p>PM.EntityFramework[v:4.6]：类库（引用PM.Core）</p>
<p>PM.Application[v:4.6]：类库（引用PM.Core）</p>
<p>PM.WebApi[v:4.6]：类库（引用PM.Application、PM.Core）</p>
<p>PM.Web[v:4.6]：WebMvc5.X（引用PM.Core、PM.EntityFramework、PM.Application、PM.WebApi）</p>
<p>PM.Test[v:4.6]：（引用PM.EntityFramework、PM.Core、PM.Application）</p>
<p style="background-color: #169fe6;"><span style="font-size: 18pt; color: #ffffff;"><strong><a name="a2"></a>二、PM.Core</strong></span></p>
<p><span style="font-size: 16px;"><strong>1，NuGet安装Abp.Zero2.1.3</strong></span></p>
<p><span style="font-size: 16px;"><strong>程序集引用：System.ComponentModel.DataAnnotations</strong></span></p>
<p><span style="font-size: 16px;"><strong>2，基本结构</strong></span></p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201710/741594-20171026171408680-602214336.png" alt="" /></p>
<p><strong>Authorization</strong></p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201710/741594-20171026173203289-1035441906.png" alt="" /></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('55ef87fa-7f1b-4e6e-a8a2-cb4b8c3d49ab')"><img id="code_img_closed_55ef87fa-7f1b-4e6e-a8a2-cb4b8c3d49ab" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_55ef87fa-7f1b-4e6e-a8a2-cb4b8c3d49ab" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('55ef87fa-7f1b-4e6e-a8a2-cb4b8c3d49ab',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_55ef87fa-7f1b-4e6e-a8a2-cb4b8c3d49ab" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.MultiTenancy;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Zero.Configuration;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.Core.Authorization.Roles
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> PMRoleConfig
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Configure(IRoleManagementConfig roleManagementConfig)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">静态主机角色</span>
            roleManagementConfig.StaticRoles.Add(<span style="color: #0000ff;">new</span><span style="color: #000000;"> StaticRoleDefinition(
                StaticRoleNames.Host.Admin
                , MultiTenancySides.Host));

            </span><span style="color: #008000;">//</span><span style="color: #008000;">静态租户角色</span>
            roleManagementConfig.StaticRoles.Add(<span style="color: #0000ff;">new</span><span style="color: #000000;"> StaticRoleDefinition(
                StaticRoleNames.Tenants.Admin,
                MultiTenancySides.Tenant));
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">PMRoleConfig</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('b3c0be17-92a3-4285-ad73-9a6c07fc8dd8')"><img id="code_img_closed_b3c0be17-92a3-4285-ad73-9a6c07fc8dd8" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_b3c0be17-92a3-4285-ad73-9a6c07fc8dd8" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('b3c0be17-92a3-4285-ad73-9a6c07fc8dd8',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_b3c0be17-92a3-4285-ad73-9a6c07fc8dd8" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Authorization.Roles;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.Users;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.Core.Authorization.Roles
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> Role : AbpRole&lt;User&gt;<span style="color: #000000;">
    {

    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Role</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('35825f1a-67fa-4b95-8179-775a1e51ce14')"><img id="code_img_closed_35825f1a-67fa-4b95-8179-775a1e51ce14" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_35825f1a-67fa-4b95-8179-775a1e51ce14" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('35825f1a-67fa-4b95-8179-775a1e51ce14',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_35825f1a-67fa-4b95-8179-775a1e51ce14" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Authorization;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Authorization.Roles;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Domain.Uow;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Runtime.Caching;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Zero.Configuration;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.Users;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.Core.Authorization.Roles
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> RoleManager:AbpRoleManager&lt;Role,User&gt;<span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> RoleManager(
            RoleStore store, 
            IPermissionManager permissionManager,
            IRoleManagementConfig roleManagementConfig, 
            ICacheManager cacheManager, 
            IUnitOfWorkManager unitOfWorkManager)
            : </span><span style="color: #0000ff;">base</span><span style="color: #000000;">(store, 
                  permissionManager, 
                  roleManagementConfig, 
                  cacheManager, 
                  unitOfWorkManager)
        {
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">RoleManager</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('8eb298ed-8c0e-4e63-aa58-d326cf1ab6f6')"><img id="code_img_closed_8eb298ed-8c0e-4e63-aa58-d326cf1ab6f6" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_8eb298ed-8c0e-4e63-aa58-d326cf1ab6f6" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('8eb298ed-8c0e-4e63-aa58-d326cf1ab6f6',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_8eb298ed-8c0e-4e63-aa58-d326cf1ab6f6" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Authorization.Roles;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Authorization.Users;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Domain.Repositories;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.Users;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.Core.Authorization.Roles
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> RoleStore:AbpRoleStore&lt;Role,User&gt;<span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> RoleStore(
            IRepository</span>&lt;Role&gt;<span style="color: #000000;"> roleRepository, 
            IRepository</span>&lt;UserRole, <span style="color: #0000ff;">long</span>&gt;<span style="color: #000000;"> userRoleRepository,
            IRepository</span>&lt;RolePermissionSetting, <span style="color: #0000ff;">long</span>&gt;<span style="color: #000000;"> rolePermissionSettingRepository)
            : </span><span style="color: #0000ff;">base</span><span style="color: #000000;">(roleRepository, 
                  userRoleRepository, 
                  rolePermissionSettingRepository)
        {
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">RoleStore</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('861156d0-459b-442d-978e-3221730676e1')"><img id="code_img_closed_861156d0-459b-442d-978e-3221730676e1" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_861156d0-459b-442d-978e-3221730676e1" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('861156d0-459b-442d-978e-3221730676e1',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_861156d0-459b-442d-978e-3221730676e1" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.Core.Authorization.Roles
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> StaticRoleNames
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">class</span><span style="color: #000000;">  Host
        {
            </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">const</span> <span style="color: #0000ff;">string</span> Admin = <span style="color: #800000;">"</span><span style="color: #800000;">Admin</span><span style="color: #800000;">"</span><span style="color: #000000;">;
        }
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> Tenants
        {
            </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">const</span> <span style="color: #0000ff;">string</span> Admin = <span style="color: #800000;">"</span><span style="color: #800000;">Admin</span><span style="color: #800000;">"</span><span style="color: #000000;">;
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">StaticRoleNames</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('d45bfa67-34c5-428e-bde7-7a40f0141656')"><img id="code_img_closed_d45bfa67-34c5-428e-bde7-7a40f0141656" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_d45bfa67-34c5-428e-bde7-7a40f0141656" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('d45bfa67-34c5-428e-bde7-7a40f0141656',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_d45bfa67-34c5-428e-bde7-7a40f0141656" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Authorization;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Authorization.Roles;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Authorization.Users;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Configuration;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Domain.Repositories;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Domain.Uow;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.IdentityFramework;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Localization;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Organizations;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Runtime.Caching;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.Authorization.Roles;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.Core.Users
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> UserManager : AbpUserManager&lt;Role, User&gt;<span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> UserManager(
            UserStore userStore, 
            RoleManager roleManager,
            IPermissionManager permissionManager, 
            IUnitOfWorkManager unitOfWorkManager, 
            ICacheManager cacheManager,
            IRepository</span>&lt;OrganizationUnit, <span style="color: #0000ff;">long</span>&gt;<span style="color: #000000;"> organizationUnitRepository,
            IRepository</span>&lt;UserOrganizationUnit, <span style="color: #0000ff;">long</span>&gt;<span style="color: #000000;"> userOrganizationUnitRepository,
            IOrganizationUnitSettings organizationUnitSettings, 
            ILocalizationManager localizationManager,
            IdentityEmailMessageService emailService, 
            ISettingManager settingManager,
            IUserTokenProviderAccessor userTokenProviderAccessor)
            : </span><span style="color: #0000ff;">base</span><span style="color: #000000;">(
                userStore, 
                roleManager, 
                permissionManager, 
                unitOfWorkManager, 
                cacheManager, 
                organizationUnitRepository,
                userOrganizationUnitRepository, 
                organizationUnitSettings, 
                localizationManager, 
                emailService,
                settingManager, 
                userTokenProviderAccessor)
        {
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">UserManager</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('c599fcd4-332a-47f1-a349-205ec166b66b')"><img id="code_img_closed_c599fcd4-332a-47f1-a349-205ec166b66b" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_c599fcd4-332a-47f1-a349-205ec166b66b" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('c599fcd4-332a-47f1-a349-205ec166b66b',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_c599fcd4-332a-47f1-a349-205ec166b66b" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Authorization.Users;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Domain.Repositories;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Domain.Uow;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.Authorization.Roles;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.Core.Users
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> UserStore:AbpUserStore&lt;Role,User&gt;<span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> UserStore(
            IRepository</span>&lt;User, <span style="color: #0000ff;">long</span>&gt;<span style="color: #000000;"> userRepository, 
            IRepository</span>&lt;UserLogin, <span style="color: #0000ff;">long</span>&gt;<span style="color: #000000;"> userLoginRepository,
            IRepository</span>&lt;UserRole, <span style="color: #0000ff;">long</span>&gt;<span style="color: #000000;"> userRoleRepository, 
            IRepository</span>&lt;Role&gt;<span style="color: #000000;"> roleRepository,
            IRepository</span>&lt;UserPermissionSetting, <span style="color: #0000ff;">long</span>&gt;<span style="color: #000000;"> userPermissionSettingRepository,
            IUnitOfWorkManager unitOfWorkManager, 
            IRepository</span>&lt;UserClaim, <span style="color: #0000ff;">long</span>&gt;<span style="color: #000000;"> userClaimRepository)
            : </span><span style="color: #0000ff;">base</span><span style="color: #000000;">(
                userRepository, 
                userLoginRepository, 
                userRoleRepository, 
                roleRepository, 
                userPermissionSettingRepository,
                unitOfWorkManager, 
                userClaimRepository)
        {
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">UserStore</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('821f366c-a8bf-4480-996e-57b3859e9387')"><img id="code_img_closed_821f366c-a8bf-4480-996e-57b3859e9387" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_821f366c-a8bf-4480-996e-57b3859e9387" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('821f366c-a8bf-4480-996e-57b3859e9387',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_821f366c-a8bf-4480-996e-57b3859e9387" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Authorization;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Authorization.Roles;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Authorization.Users;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Configuration;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Configuration.Startup;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Dependency;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Domain.Repositories;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Domain.Uow;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Zero.Configuration;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.Authorization.Roles;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.MultiTenant;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.Users;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.Core.Authorization
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> LogInManager : AbpLogInManager&lt;Tenant,Role,User&gt;<span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> LogInManager(
            UserManager userManager, 
            IMultiTenancyConfig multiTenancyConfig,
            IRepository</span>&lt;Tenant&gt;<span style="color: #000000;"> tenantRepository, 
            IUnitOfWorkManager unitOfWorkManager, 
            ISettingManager settingManager,
            IRepository</span>&lt;UserLoginAttempt, <span style="color: #0000ff;">long</span>&gt;<span style="color: #000000;"> userLoginAttemptRepository, 
            IUserManagementConfig userManagementConfig,
            IIocResolver iocResolver, 
            RoleManager roleManager)
            : </span><span style="color: #0000ff;">base</span><span style="color: #000000;">(
                userManager, 
                multiTenancyConfig, 
                tenantRepository, 
                unitOfWorkManager, 
                settingManager,
                userLoginAttemptRepository, 
                userManagementConfig, 
                iocResolver, 
                roleManager)
        {
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">LogInManager</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('883731de-43b9-461c-b855-2e15b4b238b0')"><img id="code_img_closed_883731de-43b9-461c-b855-2e15b4b238b0" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_883731de-43b9-461c-b855-2e15b4b238b0" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('883731de-43b9-461c-b855-2e15b4b238b0',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_883731de-43b9-461c-b855-2e15b4b238b0" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Authorization;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Authorization.Users;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.Authorization.Roles;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.Users;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.Core.Authorization
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> PermissionChecker:PermissionChecker&lt;Role,User&gt;<span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">public</span> PermissionChecker(UserManager userManager) : <span style="color: #0000ff;">base</span><span style="color: #000000;">(userManager)
        {
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">PermissionChecker</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('8f7c0661-0244-446e-b04f-c2a083f8ac95')"><img id="code_img_closed_8f7c0661-0244-446e-b04f-c2a083f8ac95" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_8f7c0661-0244-446e-b04f-c2a083f8ac95" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('8f7c0661-0244-446e-b04f-c2a083f8ac95',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_8f7c0661-0244-446e-b04f-c2a083f8ac95" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.Core.Authorization
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> PermisstionNames
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">const</span> <span style="color: #0000ff;">string</span> Pages_Tenants = <span style="color: #800000;">"</span><span style="color: #800000;">Pages.Tenants</span><span style="color: #800000;">"</span><span style="color: #000000;">;
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">const</span> <span style="color: #0000ff;">string</span> Pages_Users = <span style="color: #800000;">"</span><span style="color: #800000;">Pages.Users</span><span style="color: #800000;">"</span><span style="color: #000000;">;
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">const</span> <span style="color: #0000ff;">string</span> Pages_Roles = <span style="color: #800000;">"</span><span style="color: #800000;">Pages.Roles</span><span style="color: #800000;">"</span><span style="color: #000000;">;
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">PermisstionNames</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('38f46d80-05ce-49bf-933f-06ad35b98821')"><img id="code_img_closed_38f46d80-05ce-49bf-933f-06ad35b98821" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_38f46d80-05ce-49bf-933f-06ad35b98821" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('38f46d80-05ce-49bf-933f-06ad35b98821',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_38f46d80-05ce-49bf-933f-06ad35b98821" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Authorization;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Localization;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Localization.Sources;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.MultiTenancy;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.Core.Authorization
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> PMProjectNameAuthorizationProvider: AuthorizationProvider
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> SetPermissions(IPermissionDefinitionContext context)
        {

            context.CreatePermission(PermisstionNames.Pages_Users, L(</span><span style="color: #800000;">"</span><span style="color: #800000;">Users</span><span style="color: #800000;">"</span><span style="color: #000000;">));
            context.CreatePermission(PermisstionNames.Pages_Roles, L(</span><span style="color: #800000;">"</span><span style="color: #800000;">Roles</span><span style="color: #800000;">"</span><span style="color: #000000;">));
            context.CreatePermission(PermisstionNames.Pages_Tenants, L(</span><span style="color: #800000;">"</span><span style="color: #800000;">Tenants</span><span style="color: #800000;">"</span><span style="color: #000000;">),multiTenancySides:MultiTenancySides.Host);

        }

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">static</span> ILocalizableString L(<span style="color: #0000ff;">string</span><span style="color: #000000;"> name)
        {
            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> LocalizableString(name, PMProjectNameConsts.LocalizationSourceName);
        }

    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">PMProjectNameAuthorizationProvider</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('f542b382-71d9-41b2-942d-a40442ee2635')"><img id="code_img_closed_f542b382-71d9-41b2-942d-a40442ee2635" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_f542b382-71d9-41b2-942d-a40442ee2635" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('f542b382-71d9-41b2-942d-a40442ee2635',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_f542b382-71d9-41b2-942d-a40442ee2635" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Authorization.Users;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Extensions;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNet.Identity;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.Core.Users
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> User:AbpUser&lt;User&gt;<span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">const</span> <span style="color: #0000ff;">string</span> DefaultPassword = <span style="color: #800000;">"</span><span style="color: #800000;">123qwe</span><span style="color: #800000;">"</span><span style="color: #000000;">;

        </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
        <span style="color: #808080;">///</span><span style="color: #008000;"> 创建随机密码
        </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
        <span style="color: #808080;">///</span> <span style="color: #808080;">&lt;returns&gt;&lt;/returns&gt;</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">string</span><span style="color: #000000;"> CreateRandomPassword()
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">截断16位</span>
            <span style="color: #0000ff;">return</span> Guid.NewGuid().ToString(<span style="color: #800000;">"</span><span style="color: #800000;">N</span><span style="color: #800000;">"</span>).Truncate(<span style="color: #800080;">16</span><span style="color: #000000;">);
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> User CreateTenantAdminUser(<span style="color: #0000ff;">int</span> tenantId, <span style="color: #0000ff;">string</span> emailAddress, <span style="color: #0000ff;">string</span><span style="color: #000000;"> password)
        {
            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> User()
            {
                TenantId </span>=<span style="color: #000000;"> tenantId,
                UserName </span>=<span style="color: #000000;"> AdminUserName,
                Name </span>=<span style="color: #000000;"> AdminUserName,
                Surname </span>=<span style="color: #000000;"> AdminUserName,
                EmailAddress </span>=<span style="color: #000000;"> emailAddress,
                Password </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> PasswordHasher().HashPassword(password),
                IsEmailConfirmed </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">,
                IsActive </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">
            };
        }

    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">User</span></div>
<p><strong>Configuration</strong></p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201710/741594-20171026175101836-1689023564.png" alt="" /></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('ec63896a-c608-4278-82a2-500040f2f576')"><img id="code_img_closed_ec63896a-c608-4278-82a2-500040f2f576" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_ec63896a-c608-4278-82a2-500040f2f576" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('ec63896a-c608-4278-82a2-500040f2f576',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_ec63896a-c608-4278-82a2-500040f2f576" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.Core.Configuration
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> PMSettingNames
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">const</span> <span style="color: #0000ff;">string</span> UiTheme = <span style="color: #800000;">"</span><span style="color: #800000;">App.UiTheme</span><span style="color: #800000;">"</span><span style="color: #000000;">;
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">PMSettingNames</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('8b23726f-6074-42df-84bd-3f6f309645f1')"><img id="code_img_closed_8b23726f-6074-42df-84bd-3f6f309645f1" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_8b23726f-6074-42df-84bd-3f6f309645f1" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('8b23726f-6074-42df-84bd-3f6f309645f1',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_8b23726f-6074-42df-84bd-3f6f309645f1" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Configuration;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.Core.Configuration
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> PMSettingProvider:SettingProvider
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> IEnumerable&lt;SettingDefinition&gt;<span style="color: #000000;"> GetSettingDefinitions(SettingDefinitionProviderContext context)
        {
            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;">[]
            {
                </span><span style="color: #0000ff;">new</span> SettingDefinition(PMSettingNames.UiTheme, <span style="color: #800000;">"</span><span style="color: #800000;">red</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    scopes: SettingScopes.Application </span>| SettingScopes.Tenant |<span style="color: #000000;"> SettingScopes.User,
                    isVisibleToClients: </span><span style="color: #0000ff;">true</span><span style="color: #000000;">)
            };
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">PMSettingProvider</span></div>
<p><strong>Editions</strong></p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201710/741594-20171026175442586-1427908942.png" alt="" /></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('e9d031d0-3c10-48df-a1c7-56a7def08371')"><img id="code_img_closed_e9d031d0-3c10-48df-a1c7-56a7def08371" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_e9d031d0-3c10-48df-a1c7-56a7def08371" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('e9d031d0-3c10-48df-a1c7-56a7def08371',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_e9d031d0-3c10-48df-a1c7-56a7def08371" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Application.Editions;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Application.Features;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Domain.Repositories;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.Core.Editions
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> EditionManager:AbpEditionManager
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">const</span> <span style="color: #0000ff;">string</span> DefaultEditionName = <span style="color: #800000;">"</span><span style="color: #800000;">Standard</span><span style="color: #800000;">"</span><span style="color: #000000;">;

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> EditionManager(
            IRepository</span>&lt;Edition&gt;<span style="color: #000000;"> editionRepository, 
            IAbpZeroFeatureValueStore featureValueStore)
            : </span><span style="color: #0000ff;">base</span><span style="color: #000000;">(editionRepository, 
                  featureValueStore)
        {
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">EditionManager</span></div>
<p><strong>Features</strong></p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201710/741594-20171026175628039-2019162841.png" alt="" />&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('4d32be24-3721-4dad-946d-311e4d05922c')"><img id="code_img_closed_4d32be24-3721-4dad-946d-311e4d05922c" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_4d32be24-3721-4dad-946d-311e4d05922c" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('4d32be24-3721-4dad-946d-311e4d05922c',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_4d32be24-3721-4dad-946d-311e4d05922c" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Application.Features;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Domain.Repositories;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Domain.Uow;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.MultiTenancy;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Runtime.Caching;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.MultiTenant;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.Users;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.Core.Features
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> FeaturesValueStore:AbpFeatureValueStore&lt;Tenant,User&gt;<span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> FeaturesValueStore(
            ICacheManager cacheManager,
            IRepository</span>&lt;TenantFeatureSetting, <span style="color: #0000ff;">long</span>&gt;<span style="color: #000000;"> tenantFeatureRepository, 
            IRepository</span>&lt;Tenant&gt;<span style="color: #000000;"> tenantRepository,
            IRepository</span>&lt;EditionFeatureSetting, <span style="color: #0000ff;">long</span>&gt;<span style="color: #000000;"> editionFeatureRepository, 
            IFeatureManager featureManager,
            IUnitOfWorkManager unitOfWorkManager)
            : </span><span style="color: #0000ff;">base</span><span style="color: #000000;">(
                cacheManager, 
                tenantFeatureRepository, 
                tenantRepository, 
                editionFeatureRepository, 
                featureManager,
                unitOfWorkManager)
        {
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">FeaturesValueStore</span></div>
<p><strong>Localization</strong></p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201710/741594-20171026181054851-2097080446.png" alt="" /></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('83092ccd-9d36-4345-87a9-b839b7a7a428')"><img id="code_img_closed_83092ccd-9d36-4345-87a9-b839b7a7a428" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_83092ccd-9d36-4345-87a9-b839b7a7a428" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('83092ccd-9d36-4345-87a9-b839b7a7a428',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_83092ccd-9d36-4345-87a9-b839b7a7a428" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">&lt;?</span><span style="color: #ff00ff;">xml version="1.0" encoding="utf-8" </span><span style="color: #0000ff;">?&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">localizationDictionary </span><span style="color: #ff0000;">culture</span><span style="color: #0000ff;">="zh-CN"</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">texts</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">text </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="Users"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">="用户"</span><span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">text </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="Roles"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">="角色"</span><span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">text </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="Tenants"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">="租户"</span><span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">texts</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">localizationDictionary</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<span class="cnblogs_code_collapse">PMProjectName-zh-CN.xml</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('127266d0-24f7-4773-a064-8eea076cc019')"><img id="code_img_closed_127266d0-24f7-4773-a064-8eea076cc019" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_127266d0-24f7-4773-a064-8eea076cc019" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('127266d0-24f7-4773-a064-8eea076cc019',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_127266d0-24f7-4773-a064-8eea076cc019" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">&lt;?</span><span style="color: #ff00ff;">xml version="1.0" encoding="utf-8" </span><span style="color: #0000ff;">?&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">localizationDictionary </span><span style="color: #ff0000;">culture</span><span style="color: #0000ff;">="en"</span><span style="color: #0000ff;">&gt;</span>
  <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">texts</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">text </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="Users"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">="Users"</span><span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">text </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="Roles"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">="Roles"</span><span style="color: #0000ff;">/&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">text </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="Tenants"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">="Tenants"</span><span style="color: #0000ff;">/&gt;</span>
  <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">texts</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">localizationDictionary</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<span class="cnblogs_code_collapse">PMProjectName.xml</span></div>
<p><strong>MultiTenant</strong></p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201710/741594-20171026181149414-1110165266.png" alt="" /></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('3ac03265-5ddb-45a9-8ef6-5ad37b633103')"><img id="code_img_closed_3ac03265-5ddb-45a9-8ef6-5ad37b633103" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_3ac03265-5ddb-45a9-8ef6-5ad37b633103" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('3ac03265-5ddb-45a9-8ef6-5ad37b633103',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_3ac03265-5ddb-45a9-8ef6-5ad37b633103" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.MultiTenancy;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.Users;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.Core.MultiTenant
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> Tenant:AbpTenant&lt;User&gt;<span style="color: #000000;">
    {

    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Tenant</span></div>
<div class="cnblogs_code" onclick="cnblogs_code_show('b6005d47-5bda-4eb8-8625-ebb3e85d5e17')"><img id="code_img_closed_b6005d47-5bda-4eb8-8625-ebb3e85d5e17" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_b6005d47-5bda-4eb8-8625-ebb3e85d5e17" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('b6005d47-5bda-4eb8-8625-ebb3e85d5e17',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_b6005d47-5bda-4eb8-8625-ebb3e85d5e17" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Application.Editions;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Application.Features;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Domain.Repositories;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.MultiTenancy;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.Users;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.Core.MultiTenant
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> TenantManager:AbpTenantManager&lt;Tenant,User&gt;<span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> TenantManager(
            IRepository</span>&lt;Tenant&gt;<span style="color: #000000;"> tenantRepository,
            IRepository</span>&lt;TenantFeatureSetting, <span style="color: #0000ff;">long</span>&gt;<span style="color: #000000;"> tenantFeatureRepository, 
            AbpEditionManager editionManager,
            IAbpZeroFeatureValueStore featureValueStore)
            : </span><span style="color: #0000ff;">base</span><span style="color: #000000;">(tenantRepository, 
                  tenantFeatureRepository, 
                  editionManager, 
                  featureValueStore)
        {
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">TenantManager</span></div>
<p><strong>Validation</strong></p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201710/741594-20171026181232476-2098238417.png" alt="" /></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('cb54b525-6e87-4e26-b27d-bfa77ce9cd8f')"><img id="code_img_closed_cb54b525-6e87-4e26-b27d-bfa77ce9cd8f" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_cb54b525-6e87-4e26-b27d-bfa77ce9cd8f" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('cb54b525-6e87-4e26-b27d-bfa77ce9cd8f',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_cb54b525-6e87-4e26-b27d-bfa77ce9cd8f" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Extensions;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text.RegularExpressions;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.Core.Validation
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ValidationHelper
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">const</span> <span style="color: #0000ff;">string</span> EmailRegex = <span style="color: #800000;">@"</span><span style="color: #800000;">^\w+([-+.']\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*$</span><span style="color: #800000;">"</span><span style="color: #000000;">;

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> <span style="color: #0000ff;">bool</span> IsEmail(<span style="color: #0000ff;">string</span><span style="color: #000000;"> value)
        {
            </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (value.IsNullOrEmpty())
            {
                </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">false</span><span style="color: #000000;">;
            }

            </span><span style="color: #0000ff;">var</span> regex = <span style="color: #0000ff;">new</span><span style="color: #000000;"> Regex(EmailRegex);
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> regex.IsMatch(value);
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">ValidationHelper</span></div>
<p><strong>PMProjectNameConsts 公共常量类</strong></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('417f2b89-1f3f-4f5a-a68e-c76abc8b7530')"><img id="code_img_closed_417f2b89-1f3f-4f5a-a68e-c76abc8b7530" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_417f2b89-1f3f-4f5a-a68e-c76abc8b7530" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('417f2b89-1f3f-4f5a-a68e-c76abc8b7530',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_417f2b89-1f3f-4f5a-a68e-c76abc8b7530" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.Core
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> PMProjectNameConsts
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">const</span> <span style="color: #0000ff;">string</span> LocalizationSourceName = <span style="color: #800000;">"</span><span style="color: #800000;">PMProjectName</span><span style="color: #800000;">"</span><span style="color: #000000;">;
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">const</span> <span style="color: #0000ff;">bool</span> MultiTenantEnabled = <span style="color: #0000ff;">true</span><span style="color: #000000;">;
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">PMProjectNameConsts</span></div>
<p><strong>PMVersionHepler 版本帮助类</strong></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('c059cdd8-28ee-4a47-9402-4c3fb4322c2b')"><img id="code_img_closed_c059cdd8-28ee-4a47-9402-4c3fb4322c2b" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_c059cdd8-28ee-4a47-9402-4c3fb4322c2b" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('c059cdd8-28ee-4a47-9402-4c3fb4322c2b',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_c059cdd8-28ee-4a47-9402-4c3fb4322c2b" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.IO;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Reflection.Extensions;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.Core
{
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
    <span style="color: #808080;">///</span><span style="color: #008000;"> 应用版本中心
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> PMVersionHepler
    {
        </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
        <span style="color: #808080;">///</span><span style="color: #008000;"> 获取应用程序当前版本
        </span><span style="color: #808080;">///</span><span style="color: #008000;"> 显示在网页中
        </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">const</span> <span style="color: #0000ff;">string</span> Version = <span style="color: #800000;">"</span><span style="color: #800000;">1.0.0.0</span><span style="color: #800000;">"</span><span style="color: #000000;">;

        </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
        <span style="color: #808080;">///</span><span style="color: #008000;"> 获取应用程序最后一次发布的时间
        </span><span style="color: #808080;">///</span><span style="color: #008000;"> 它显示在网页中
        </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span><span style="color: #000000;"> DateTime ReleaseDate
        {
            </span><span style="color: #0000ff;">get</span> { <span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> FileInfo(<span style="color: #0000ff;">typeof</span><span style="color: #000000;">(PMVersionHepler).GetAssembly().Location).LastWriteTime; }
        }

    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">PMVersionHepler</span></div>
<p><strong>PMCoreModule模块类</strong></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('b522be6d-e8a7-4fe0-b8d0-47e04d4efa4c')"><img id="code_img_closed_b522be6d-e8a7-4fe0-b8d0-47e04d4efa4c" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_b522be6d-e8a7-4fe0-b8d0-47e04d4efa4c" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('b522be6d-e8a7-4fe0-b8d0-47e04d4efa4c',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_b522be6d-e8a7-4fe0-b8d0-47e04d4efa4c" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Reflection;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Localization.Dictionaries;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Localization.Dictionaries.Xml;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Modules;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Zero;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Zero.Configuration;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.Authorization;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.Authorization.Roles;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.Configuration;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.MultiTenant;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.Users;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.Core
{
    [DependsOn(</span><span style="color: #0000ff;">typeof</span><span style="color: #000000;">(AbpZeroCoreModule))]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> PMCoreModule:AbpModule
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> PreInitialize()
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">如果当前用户未登录，请设置为true以启用保存审核日志。默认值：</span>
            Configuration.Auditing.IsEnabledForAnonymousUsers = <span style="color: #0000ff;">true</span><span style="color: #000000;">;

            </span><span style="color: #008000;">//</span><span style="color: #008000;">声明实体类型</span>
            Configuration.Modules.Zero().EntityTypes.Tenant = <span style="color: #0000ff;">typeof</span><span style="color: #000000;"> (Tenant);
            Configuration.Modules.Zero().EntityTypes.Role </span>= <span style="color: #0000ff;">typeof</span><span style="color: #000000;"> (Role);
            Configuration.Modules.Zero().EntityTypes.User </span>= <span style="color: #0000ff;">typeof</span><span style="color: #000000;"> (User);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">开启多租户</span>
            Configuration.MultiTenancy.IsEnabled =<span style="color: #000000;"> PMProjectNameConsts.MultiTenantEnabled;

            </span><span style="color: #008000;">//</span><span style="color: #008000;">添加删除本地化源</span>
<span style="color: #000000;">            Configuration.Localization.Sources.Add(
                </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> DictionaryBasedLocalizationSource(PMProjectNameConsts.LocalizationSourceName,
                    </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> XmlEmbeddedFileLocalizationDictionaryProvider(Assembly.GetExecutingAssembly(),
                        </span><span style="color: #800000;">"</span><span style="color: #800000;">PM.Localization.Source</span><span style="color: #800000;">"</span><span style="color: #000000;">)));

            </span><span style="color: #008000;">//</span><span style="color: #008000;">设置静态角色</span>
<span style="color: #000000;">            PMRoleConfig.Configure(Configuration.Modules.Zero().RoleManagement);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">初始化权限</span>
            Configuration.Authorization.Providers.Add&lt;PMProjectNameAuthorizationProvider&gt;<span style="color: #000000;">();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">初始化设置</span>
            Configuration.Settings.Providers.Add&lt;PMSettingProvider&gt;<span style="color: #000000;">();

        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Initialize()
        {
            IocManager.RegisterAssemblyByConvention(Assembly.GetExecutingAssembly());
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">PMCoreModule</span></div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a3"></a>三、PM.EntityFramework</span></strong></span></p>
<p><strong>1，NuGet安装Abp.Zero2.1.3、Abp.Zero.EntityFramework2.13</strong></p>
<p><strong>2，基本结构</strong></p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201710/741594-20171029142410726-1251294283.png" alt="" />&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('7debb767-eac0-4cda-a7d4-129c116d2e44')"><img id="code_img_closed_7debb767-eac0-4cda-a7d4-129c116d2e44" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_7debb767-eac0-4cda-a7d4-129c116d2e44" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('7debb767-eac0-4cda-a7d4-129c116d2e44',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_7debb767-eac0-4cda-a7d4-129c116d2e44" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Domain.Entities;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.EntityFramework;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.EntityFramework.Repositories;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.EntityFramework.EntityFramework.Repositories
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> PMRepositoryBase&lt;TEntity, TPrimaryKey&gt; : EfRepositoryBase&lt;PMDBContext, TEntity, TPrimaryKey&gt;
        <span style="color: #0000ff;">where</span> TEntity:<span style="color: #0000ff;">class</span>,IEntity&lt;TPrimaryKey&gt;<span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">public</span> PMRepositoryBase(IDbContextProvider&lt;PMDBContext&gt; dbContextProvider) : <span style="color: #0000ff;">base</span><span style="color: #000000;">(dbContextProvider)
        {
        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;">为所有存储库添加常用方法</span>
<span style="color: #000000;">    }

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> PMRepositoryBase&lt;TEntity&gt; : PMRepositoryBase&lt;TEntity, <span style="color: #0000ff;">int</span>&gt;
        <span style="color: #0000ff;">where</span> TEntity : <span style="color: #0000ff;">class</span>, IEntity&lt;<span style="color: #0000ff;">int</span>&gt;<span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">public</span> PMRepositoryBase(IDbContextProvider&lt;PMDBContext&gt; dbContextProvider) : <span style="color: #0000ff;">base</span><span style="color: #000000;">(dbContextProvider)
        {
        }
        </span><span style="color: #008000;">//</span><span style="color: #008000;">不要在这里添加任何方法，添加到上面的类（因为它继承它）</span>
<span style="color: #000000;">    }

}</span></pre>
</div>
<span class="cnblogs_code_collapse">PMRepositoryBase</span></div>
<p>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('6d97fda0-bce3-417b-9430-a773dd0fe8c2')"><img id="code_img_closed_6d97fda0-bce3-417b-9430-a773dd0fe8c2" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_6d97fda0-bce3-417b-9430-a773dd0fe8c2" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('6d97fda0-bce3-417b-9430-a773dd0fe8c2',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_6d97fda0-bce3-417b-9430-a773dd0fe8c2" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Data.Common;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Zero.EntityFramework;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.Authorization.Roles;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.MultiTenant;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.Users;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.EntityFramework.EntityFramework
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> PMDBContext:AbpZeroDbContext&lt;Tenant,Role,User&gt;<span style="color: #000000;">
    {
        </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
        <span style="color: #808080;">///</span><span style="color: #008000;"> 将&ldquo;默认&rdquo;设置为基类可帮助我们在Package Manager Console上执行迁移命令时使用。
        </span><span style="color: #808080;">///</span><span style="color: #008000;"> 但是，在运行EF的Migrate.exe时可能会导致问题。 如果要在命令行上应用迁移，请不要将连接字符串名称传递给基类。 ABP工作方式。
        </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
        <span style="color: #0000ff;">public</span> PMDBContext() : <span style="color: #0000ff;">base</span>(<span style="color: #800000;">"</span><span style="color: #800000;">Default</span><span style="color: #800000;">"</span><span style="color: #000000;">)
        {
        }

        </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
        <span style="color: #808080;">///</span><span style="color: #008000;"> ABP使用此构造函数传递PMDBContext.PreInitialize中定义的连接字符串。
        </span><span style="color: #808080;">///</span><span style="color: #008000;"> 注意，实际上你不会直接创建一个PMDBContext的实例，因为ABP自动处理它。
        </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
        <span style="color: #808080;">///</span> <span style="color: #808080;">&lt;param name="nameOrnameOrConnectionString"&gt;&lt;/param&gt;</span>
        <span style="color: #0000ff;">public</span> PMDBContext(<span style="color: #0000ff;">string</span> nameOrnameOrConnectionString) : <span style="color: #0000ff;">base</span><span style="color: #000000;">(nameOrnameOrConnectionString)
        {
        }

        </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
        <span style="color: #808080;">///</span><span style="color: #008000;"> 这个构造函数用于测试
        </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
        <span style="color: #808080;">///</span> <span style="color: #808080;">&lt;param name="existingConnection"&gt;&lt;/param&gt;</span>
        <span style="color: #0000ff;">public</span> PMDBContext(DbConnection existingConnection) : <span style="color: #0000ff;">base</span>(existingConnection,<span style="color: #0000ff;">false</span><span style="color: #000000;">)
        {
        }

        </span><span style="color: #0000ff;">public</span> PMDBContext(DbConnection existingConnection, <span style="color: #0000ff;">bool</span><span style="color: #000000;"> contextOwnsConnection)
            : </span><span style="color: #0000ff;">base</span><span style="color: #000000;">(existingConnection, contextOwnsConnection)
        {
        }

    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">PMDBContext</span></div>
<p>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('7dce6fa9-8b52-44ef-bd8f-27a93e7467f0')"><img id="code_img_closed_7dce6fa9-8b52-44ef-bd8f-27a93e7467f0" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_7dce6fa9-8b52-44ef-bd8f-27a93e7467f0" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('7dce6fa9-8b52-44ef-bd8f-27a93e7467f0',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_7dce6fa9-8b52-44ef-bd8f-27a93e7467f0" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Application.Editions;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.Editions;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.EntityFramework.EntityFramework;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.EntityFramework.Migrations.SeedData
{

    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
    <span style="color: #808080;">///</span><span style="color: #008000;"> 默认版本创建者
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> DefaultEditionsCreator
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> PMDBContext _context;

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> DefaultEditionsCreator(PMDBContext context)
        {
            _context </span>=<span style="color: #000000;"> context;
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Create()
        {
            CreateEdtions();
        }

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> CreateEdtions()
        {
            </span><span style="color: #0000ff;">var</span> defaultEdtion = _context.Editions.FirstOrDefault(e =&gt; e.Name ==<span style="color: #000000;"> EditionManager.DefaultEditionName);
            </span><span style="color: #0000ff;">if</span> (defaultEdtion == <span style="color: #0000ff;">null</span><span style="color: #000000;">)
            {
                defaultEdtion </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> Edition()
                {
                    Name </span>=<span style="color: #000000;"> EditionManager.DefaultEditionName,
                    DisplayName </span>=<span style="color: #000000;"> EditionManager.DefaultEditionName
                };
                _context.Editions.Add(defaultEdtion);
                _context.SaveChanges();

                </span><span style="color: #008000;">//</span><span style="color: #008000;">TODO：如果需要，可以在标准版中添加所需的功能！</span>
<span style="color: #000000;">            }
        }

    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">DefaultEditionsCreator</span></div>
<p>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('e8ee5b8a-e554-4f22-ae32-60dbcea5f3a3')"><img id="code_img_closed_e8ee5b8a-e554-4f22-ae32-60dbcea5f3a3" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_e8ee5b8a-e554-4f22-ae32-60dbcea5f3a3" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('e8ee5b8a-e554-4f22-ae32-60dbcea5f3a3',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_e8ee5b8a-e554-4f22-ae32-60dbcea5f3a3" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Localization;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.EntityFramework.EntityFramework;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.EntityFramework.Migrations.SeedData
{
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
    <span style="color: #808080;">///</span><span style="color: #008000;"> 默认语言创建者
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> DefaultLanguagesCreator
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> List&lt;ApplicationLanguage&gt; InitialLanguages { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">private</span> <span style="color: #0000ff;">set</span><span style="color: #000000;">; } 
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> PMDBContext _context;

        </span><span style="color: #0000ff;">static</span><span style="color: #000000;"> DefaultLanguagesCreator()
        {
            InitialLanguages </span>= <span style="color: #0000ff;">new</span> List&lt;ApplicationLanguage&gt;<span style="color: #000000;">
            {
                </span><span style="color: #0000ff;">new</span> ApplicationLanguage(<span style="color: #0000ff;">null</span>, <span style="color: #800000;">"</span><span style="color: #800000;">en</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">English</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">famfamfam-flags gb</span><span style="color: #800000;">"</span><span style="color: #000000;">),
                </span><span style="color: #0000ff;">new</span> ApplicationLanguage(<span style="color: #0000ff;">null</span>, <span style="color: #800000;">"</span><span style="color: #800000;">tr</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">T&uuml;rk&ccedil;e</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">famfamfam-flags tr</span><span style="color: #800000;">"</span><span style="color: #000000;">),
                </span><span style="color: #0000ff;">new</span> ApplicationLanguage(<span style="color: #0000ff;">null</span>, <span style="color: #800000;">"</span><span style="color: #800000;">zh-CN</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">简体中文</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">famfamfam-flags cn</span><span style="color: #800000;">"</span><span style="color: #000000;">),
                </span><span style="color: #0000ff;">new</span> ApplicationLanguage(<span style="color: #0000ff;">null</span>, <span style="color: #800000;">"</span><span style="color: #800000;">pt-BR</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">Portugu&ecirc;s-BR</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">famfamfam-flags br</span><span style="color: #800000;">"</span><span style="color: #000000;">),
                </span><span style="color: #0000ff;">new</span> ApplicationLanguage(<span style="color: #0000ff;">null</span>, <span style="color: #800000;">"</span><span style="color: #800000;">es</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">Espa&ntilde;ol</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">famfamfam-flags es</span><span style="color: #800000;">"</span><span style="color: #000000;">),
                </span><span style="color: #0000ff;">new</span> ApplicationLanguage(<span style="color: #0000ff;">null</span>, <span style="color: #800000;">"</span><span style="color: #800000;">fr</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">Fran&ccedil;ais</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">famfamfam-flags fr</span><span style="color: #800000;">"</span><span style="color: #000000;">),
                </span><span style="color: #0000ff;">new</span> ApplicationLanguage(<span style="color: #0000ff;">null</span>, <span style="color: #800000;">"</span><span style="color: #800000;">it</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">Italiano</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">famfamfam-flags it</span><span style="color: #800000;">"</span><span style="color: #000000;">),
                </span><span style="color: #0000ff;">new</span> ApplicationLanguage(<span style="color: #0000ff;">null</span>, <span style="color: #800000;">"</span><span style="color: #800000;">ja</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">日本語</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">famfamfam-flags jp</span><span style="color: #800000;">"</span><span style="color: #000000;">),
                </span><span style="color: #0000ff;">new</span> ApplicationLanguage(<span style="color: #0000ff;">null</span>, <span style="color: #800000;">"</span><span style="color: #800000;">nl-NL</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">Nederlands</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">famfamfam-flags nl</span><span style="color: #800000;">"</span><span style="color: #000000;">),
                </span><span style="color: #0000ff;">new</span> ApplicationLanguage(<span style="color: #0000ff;">null</span>, <span style="color: #800000;">"</span><span style="color: #800000;">lt</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">Lietuvos</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">famfamfam-flags lt</span><span style="color: #800000;">"</span><span style="color: #000000;">),
                </span><span style="color: #0000ff;">new</span> ApplicationLanguage(<span style="color: #0000ff;">null</span>, <span style="color: #800000;">"</span><span style="color: #800000;">vn</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">Vietnamese</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">famfamfam-flags vn</span><span style="color: #800000;">"</span><span style="color: #000000;">)
            };
        }

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> DefaultLanguagesCreator(PMDBContext context)
        {
            _context </span>=<span style="color: #000000;"> context;
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Create()
        {
            CreateLanguages();
        }

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> CreateLanguages()
        {
            </span><span style="color: #0000ff;">foreach</span> (<span style="color: #0000ff;">var</span> applicationLanguage <span style="color: #0000ff;">in</span><span style="color: #000000;"> InitialLanguages)
            {
                AddLanguageIfNotExists(applicationLanguage);
            }
        }

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> AddLanguageIfNotExists(ApplicationLanguage language)
        {
            </span><span style="color: #0000ff;">if</span> (_context.Languages.Any(l =&gt; l.TenantId == language.TenantId &amp;&amp; l.Name ==<span style="color: #000000;"> language.Name))
            {
                </span><span style="color: #0000ff;">return</span><span style="color: #000000;">;
            }
            _context.Languages.Add(language);
            _context.SaveChanges();
        }



    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">DefaultLanguagesCreator</span></div>
<p>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('88f4c699-4105-49d8-8a0c-9599e812363c')"><img id="code_img_closed_88f4c699-4105-49d8-8a0c-9599e812363c" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_88f4c699-4105-49d8-8a0c-9599e812363c" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('88f4c699-4105-49d8-8a0c-9599e812363c',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_88f4c699-4105-49d8-8a0c-9599e812363c" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Configuration;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Localization;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Net.Mail;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.EntityFramework.EntityFramework;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.EntityFramework.Migrations.SeedData
{
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
    <span style="color: #808080;">///</span><span style="color: #008000;"> 默认设置创建者
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> DefaultSettingsCreator
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> PMDBContext _context;

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> DefaultSettingsCreator(PMDBContext context)
        {
            _context </span>=<span style="color: #000000;"> context;
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Create()
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">邮箱</span>
            AddSettingIfNotExists(EmailSettingNames.DefaultFromAddress, <span style="color: #800000;">"</span><span style="color: #800000;">qq962410314@163.com</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            AddSettingIfNotExists(EmailSettingNames.DefaultFromDisplayName, </span><span style="color: #800000;">"</span><span style="color: #800000;">qq962410314@163.com</span><span style="color: #800000;">"</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">语言</span>
            AddSettingIfNotExists(LocalizationSettingNames.DefaultLanguage, <span style="color: #800000;">"</span><span style="color: #800000;">zh-CN</span><span style="color: #800000;">"</span><span style="color: #000000;">);
        }

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">void</span> AddSettingIfNotExists(<span style="color: #0000ff;">string</span> name, <span style="color: #0000ff;">string</span> value, <span style="color: #0000ff;">int</span>? tenantId = <span style="color: #0000ff;">null</span><span style="color: #000000;">)
        {
            </span><span style="color: #0000ff;">if</span> (_context.Settings.Any(s =&gt; s.Name == name &amp;&amp; s.TenantId == tenantId &amp;&amp; s.UserId == <span style="color: #0000ff;">null</span><span style="color: #000000;">))
            {
                </span><span style="color: #0000ff;">return</span><span style="color: #000000;">;
            }
            _context.Settings.Add(</span><span style="color: #0000ff;">new</span> Setting(tenantId, <span style="color: #0000ff;">null</span><span style="color: #000000;">, name, value));
            _context.SaveChanges();
        }


    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">DefaultSettingsCreator</span></div>
<p>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('7a7368f1-1935-43be-876a-8b87d704fe6d')"><img id="code_img_closed_7a7368f1-1935-43be-876a-8b87d704fe6d" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_7a7368f1-1935-43be-876a-8b87d704fe6d" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('7a7368f1-1935-43be-876a-8b87d704fe6d',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_7a7368f1-1935-43be-876a-8b87d704fe6d" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.MultiTenant;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.EntityFramework.EntityFramework;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.EntityFramework.Migrations.SeedData
{
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
    <span style="color: #808080;">///</span><span style="color: #008000;"> 默认租户创建者
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> DefaultTenantCreator
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> PMDBContext _context;

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> DefaultTenantCreator(PMDBContext context)
        {
            _context </span>=<span style="color: #000000;"> context;
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Create()
        {
            CreateUserAndRoles();
        }

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> CreateUserAndRoles()
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">默认租户</span>
            <span style="color: #0000ff;">var</span> defaultTenant = _context.Tenants.FirstOrDefault(t =&gt; t.TenancyName ==<span style="color: #000000;"> Tenant.DefaultTenantName);
            </span><span style="color: #0000ff;">if</span> (defaultTenant == <span style="color: #0000ff;">null</span><span style="color: #000000;">)
            {
                _context.Tenants.Add(</span><span style="color: #0000ff;">new</span><span style="color: #000000;"> Tenant()
                {
                    TenancyName </span>=<span style="color: #000000;"> Tenant.DefaultTenantName,
                    Name </span>=<span style="color: #000000;"> Tenant.DefaultTenantName
                });
                _context.SaveChanges();
            }

        }

    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">DefaultTenantCreator</span></div>
<p>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('e4e76ab1-94fd-43ef-88eb-b0dac2dd5813')"><img id="code_img_closed_e4e76ab1-94fd-43ef-88eb-b0dac2dd5813" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_e4e76ab1-94fd-43ef-88eb-b0dac2dd5813" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('e4e76ab1-94fd-43ef-88eb-b0dac2dd5813',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_e4e76ab1-94fd-43ef-88eb-b0dac2dd5813" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Authorization;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Authorization.Roles;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Authorization.Users;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.MultiTenancy;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNet.Identity;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.Authorization;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.Authorization.Roles;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.Users;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.EntityFramework.EntityFramework;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.EntityFramework.Migrations.SeedData
{
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
    <span style="color: #808080;">///</span><span style="color: #008000;"> 主机admin创建者
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> HostRoleAndUserCreator
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> PMDBContext _context;

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> HostRoleAndUserCreator(PMDBContext context)
        {
            _context </span>=<span style="color: #000000;"> context;
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Create()
        {
            CreateHostRoleAndUsers();
        }

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> CreateHostRoleAndUsers()
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">主机角色</span>
            <span style="color: #0000ff;">var</span> adminRoleForHost= _context.Roles.FirstOrDefault(r =&gt; r.TenantId == <span style="color: #0000ff;">null</span> &amp;&amp; r.Name ==<span style="color: #000000;"> StaticRoleNames.Host.Admin);
            </span><span style="color: #0000ff;">if</span> (adminRoleForHost == <span style="color: #0000ff;">null</span><span style="color: #000000;">)
            {
                adminRoleForHost </span>= _context.Roles.Add(<span style="color: #0000ff;">new</span><span style="color: #000000;"> Role()
                {
                    Name </span>=<span style="color: #000000;"> StaticRoleNames.Host.Admin,
                    DisplayName </span>=<span style="color: #000000;"> StaticRoleNames.Host.Admin,
                    IsStatic </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">
                });
                _context.SaveChanges();

                </span><span style="color: #008000;">//</span><span style="color: #008000;">授予所有租户权限</span>
                <span style="color: #0000ff;">var</span> permisstions = PermissionFinder.GetAllPermissions(<span style="color: #0000ff;">new</span><span style="color: #000000;"> PMProjectNameAuthorizationProvider())
                    .Where(p </span>=&gt;<span style="color: #000000;"> p.MultiTenancySides.HasFlag(MultiTenancySides.Host))
                    .ToList();
                </span><span style="color: #0000ff;">foreach</span> (<span style="color: #0000ff;">var</span> permisstion <span style="color: #0000ff;">in</span><span style="color: #000000;"> permisstions)
                {
                    _context.Permissions.Add(</span><span style="color: #0000ff;">new</span><span style="color: #000000;"> RolePermissionSetting()
                    {
                        Name </span>=<span style="color: #000000;"> permisstion.Name,
                        IsGranted </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">,
                        RoleId </span>=<span style="color: #000000;"> adminRoleForHost.Id
                    });
                }
                _context.SaveChanges();
            }

            </span><span style="color: #008000;">//</span><span style="color: #008000;">主机admin</span>
            <span style="color: #0000ff;">var</span> adminUserForHost =<span style="color: #000000;">
                _context.Users.FirstOrDefault(u </span>=&gt; u.TenantId == <span style="color: #0000ff;">null</span> &amp;&amp; u.UserName ==<span style="color: #000000;"> User.AdminUserName);
            </span><span style="color: #0000ff;">if</span> (adminUserForHost == <span style="color: #0000ff;">null</span><span style="color: #000000;">)
            {
                adminUserForHost </span>= _context.Users.Add(<span style="color: #0000ff;">new</span><span style="color: #000000;"> User()
                {
                    UserName </span>=<span style="color: #000000;"> User.AdminUserName,
                    Name </span>= <span style="color: #800000;">"</span><span style="color: #800000;">System</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    Surname </span>= <span style="color: #800000;">"</span><span style="color: #800000;">Administrator</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    EmailAddress </span>= <span style="color: #800000;">"</span><span style="color: #800000;">qq962410314@163.com</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    IsEmailConfirmed </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">,
                    Password </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> PasswordHasher().HashPassword(User.DefaultPassword)
                });

                _context.SaveChanges();
                _context.UserRoles.Add(</span><span style="color: #0000ff;">new</span> UserRole(<span style="color: #0000ff;">null</span><span style="color: #000000;">, adminUserForHost.Id, adminRoleForHost.Id));
                _context.SaveChanges();
            }


        }

    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">HostRoleAndUserCreator</span></div>
<p>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('fff173d9-6f3d-4d96-985e-3b9dc15a6f1d')"><img id="code_img_closed_fff173d9-6f3d-4d96-985e-3b9dc15a6f1d" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_fff173d9-6f3d-4d96-985e-3b9dc15a6f1d" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('fff173d9-6f3d-4d96-985e-3b9dc15a6f1d',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_fff173d9-6f3d-4d96-985e-3b9dc15a6f1d" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> EntityFramework.DynamicFilters;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.EntityFramework.EntityFramework;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.EntityFramework.Migrations.SeedData
{
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
    <span style="color: #808080;">///</span><span style="color: #008000;"> 初始化主机数据库提供者
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> InitialHostDbBuilder
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> PMDBContext _context;

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> InitialHostDbBuilder(PMDBContext context)
        {
            _context </span>=<span style="color: #000000;"> context;
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Create()
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">禁用所有过滤器</span>
<span style="color: #000000;">            _context.DisableAllFilters();

            </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> DefaultEditionsCreator(_context).Create();
            </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> DefaultLanguagesCreator(_context).Create();
            </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> HostRoleAndUserCreator(_context).Create();
            </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> DefaultSettingsCreator(_context).Create();

        }

    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">InitialHostDbBuilder</span></div>
<p>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('0b6955c2-4c55-4a8a-b713-a23390c66bb4')"><img id="code_img_closed_0b6955c2-4c55-4a8a-b713-a23390c66bb4" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_0b6955c2-4c55-4a8a-b713-a23390c66bb4" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('0b6955c2-4c55-4a8a-b713-a23390c66bb4',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_0b6955c2-4c55-4a8a-b713-a23390c66bb4" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Authorization;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Authorization.Roles;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Authorization.Users;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.MultiTenancy;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.Authorization;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.Authorization.Roles;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.Users;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.EntityFramework.EntityFramework;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.EntityFramework.Migrations.SeedData
{
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
    <span style="color: #808080;">///</span><span style="color: #008000;"> 租户admin创建者
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> TenantRoleAndUserBuilder
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> PMDBContext _context;
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span> <span style="color: #0000ff;">int</span><span style="color: #000000;"> _tenantId;

        </span><span style="color: #0000ff;">public</span> TenantRoleAndUserBuilder(PMDBContext context, <span style="color: #0000ff;">int</span><span style="color: #000000;"> tenantId)
        {
            _context </span>=<span style="color: #000000;"> context;
            _tenantId </span>=<span style="color: #000000;"> tenantId;
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Create()
        {
            CreateRolesAndUsers();
        }

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> CreateRolesAndUsers()
        {

            </span><span style="color: #008000;">//</span><span style="color: #008000;">租户角色</span>
            <span style="color: #0000ff;">var</span> adminRole =<span style="color: #000000;">
                _context.Roles.FirstOrDefault(r </span>=&gt; r.TenantId == _tenantId &amp;&amp; r.Name ==<span style="color: #000000;"> StaticRoleNames.Tenants.Admin);
            </span><span style="color: #0000ff;">if</span> (adminRole==<span style="color: #0000ff;">null</span><span style="color: #000000;">)
            {
                adminRole </span>=<span style="color: #000000;">
                    _context.Roles.Add(</span><span style="color: #0000ff;">new</span><span style="color: #000000;"> Role(_tenantId, StaticRoleNames.Tenants.Admin, StaticRoleNames.Tenants.Admin)
                    {
                        IsStatic </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">
                    });
                _context.SaveChanges();

                </span><span style="color: #008000;">//</span><span style="color: #008000;">授予管理员角色的所有权限</span>
                <span style="color: #0000ff;">var</span> permisstions = PermissionFinder.GetAllPermissions(<span style="color: #0000ff;">new</span><span style="color: #000000;"> PMProjectNameAuthorizationProvider())
                    .Where(p </span>=&gt;<span style="color: #000000;"> p.MultiTenancySides.HasFlag(MultiTenancySides.Tenant))
                    .ToList();
                </span><span style="color: #0000ff;">foreach</span> (<span style="color: #0000ff;">var</span> permisstion <span style="color: #0000ff;">in</span><span style="color: #000000;"> permisstions)
                {
                    _context.Permissions.Add(</span><span style="color: #0000ff;">new</span><span style="color: #000000;"> RolePermissionSetting()
                    {
                        TenantId </span>=<span style="color: #000000;"> _tenantId,
                        Name </span>=<span style="color: #000000;"> permisstion.Name,
                        IsGranted </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">,
                        RoleId </span>=<span style="color: #000000;"> adminRole.Id
                    });
                }
                _context.SaveChanges();
            }

            </span><span style="color: #008000;">//</span><span style="color: #008000;">租户admin</span>
            <span style="color: #0000ff;">var</span> adminUser =<span style="color: #000000;">
                _context.Users.FirstOrDefault(u </span>=&gt; u.TenantId == _tenantId &amp;&amp; u.UserName ==<span style="color: #000000;"> User.AdminUserName);
            </span><span style="color: #0000ff;">if</span> (adminUser == <span style="color: #0000ff;">null</span><span style="color: #000000;">)
            {
                adminUser </span>= User.CreateTenantAdminUser(_tenantId, <span style="color: #800000;">"</span><span style="color: #800000;">qq962410314@163.com</span><span style="color: #800000;">"</span><span style="color: #000000;">, User.DefaultPassword);
                adminUser.IsEmailConfirmed </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">;
                adminUser.IsActive </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">;

                _context.Users.Add(adminUser);
                _context.SaveChanges();

                _context.UserRoles.Add(</span><span style="color: #0000ff;">new</span><span style="color: #000000;"> UserRole(_tenantId, adminUser.Id, adminRole.Id));
                _context.SaveChanges();
            }
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">TenantRoleAndUserBuilder</span></div>
<p>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('abb573ef-7bf6-48a8-bb04-2208d9831ccc')"><img id="code_img_closed_abb573ef-7bf6-48a8-bb04-2208d9831ccc" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_abb573ef-7bf6-48a8-bb04-2208d9831ccc" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('abb573ef-7bf6-48a8-bb04-2208d9831ccc',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_abb573ef-7bf6-48a8-bb04-2208d9831ccc" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.EntityFramework.Migrations
{
    </span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
    </span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
    </span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Data.Entity.Infrastructure.Annotations;
    </span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Data.Entity.Migrations;
    
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">partial</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> init : DbMigration
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Up()
        {
            CreateTable(
                </span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpAuditLogs</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                c </span>=&gt; <span style="color: #0000ff;">new</span><span style="color: #000000;">
                    {
                        Id </span>= c.Long(nullable: <span style="color: #0000ff;">false</span>, identity: <span style="color: #0000ff;">true</span><span style="color: #000000;">),
                        TenantId </span>=<span style="color: #000000;"> c.Int(),
                        UserId </span>=<span style="color: #000000;"> c.Long(),
                        ServiceName </span>= c.String(maxLength: <span style="color: #800080;">256</span><span style="color: #000000;">),
                        MethodName </span>= c.String(maxLength: <span style="color: #800080;">256</span><span style="color: #000000;">),
                        Parameters </span>= c.String(maxLength: <span style="color: #800080;">1024</span><span style="color: #000000;">),
                        ExecutionTime </span>= c.DateTime(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        ExecutionDuration </span>= c.Int(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        ClientIpAddress </span>= c.String(maxLength: <span style="color: #800080;">64</span><span style="color: #000000;">),
                        ClientName </span>= c.String(maxLength: <span style="color: #800080;">128</span><span style="color: #000000;">),
                        BrowserInfo </span>= c.String(maxLength: <span style="color: #800080;">256</span><span style="color: #000000;">),
                        Exception </span>= c.String(maxLength: <span style="color: #800080;">2000</span><span style="color: #000000;">),
                        ImpersonatorUserId </span>=<span style="color: #000000;"> c.Long(),
                        ImpersonatorTenantId </span>=<span style="color: #000000;"> c.Int(),
                        CustomData </span>= c.String(maxLength: <span style="color: #800080;">2000</span><span style="color: #000000;">),
                    },
                annotations: </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">
                {
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_AuditLog_MayHaveTenant</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                })
                .PrimaryKey(t </span>=&gt;<span style="color: #000000;"> t.Id);
            
            CreateTable(
                </span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpBackgroundJobs</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                c </span>=&gt; <span style="color: #0000ff;">new</span><span style="color: #000000;">
                    {
                        Id </span>= c.Long(nullable: <span style="color: #0000ff;">false</span>, identity: <span style="color: #0000ff;">true</span><span style="color: #000000;">),
                        JobType </span>= c.String(nullable: <span style="color: #0000ff;">false</span>, maxLength: <span style="color: #800080;">512</span><span style="color: #000000;">),
                        JobArgs </span>= c.String(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        TryCount </span>= c.Short(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        NextTryTime </span>= c.DateTime(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        LastTryTime </span>=<span style="color: #000000;"> c.DateTime(),
                        IsAbandoned </span>= c.Boolean(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        Priority </span>= c.Byte(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        CreationTime </span>= c.DateTime(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        CreatorUserId </span>=<span style="color: #000000;"> c.Long(),
                    })
                .PrimaryKey(t </span>=&gt;<span style="color: #000000;"> t.Id)
                .Index(t </span>=&gt; <span style="color: #0000ff;">new</span><span style="color: #000000;"> { t.IsAbandoned, t.NextTryTime });
            
            CreateTable(
                </span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpFeatures</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                c </span>=&gt; <span style="color: #0000ff;">new</span><span style="color: #000000;">
                    {
                        Id </span>= c.Long(nullable: <span style="color: #0000ff;">false</span>, identity: <span style="color: #0000ff;">true</span><span style="color: #000000;">),
                        Name </span>= c.String(nullable: <span style="color: #0000ff;">false</span>, maxLength: <span style="color: #800080;">128</span><span style="color: #000000;">),
                        Value </span>= c.String(nullable: <span style="color: #0000ff;">false</span>, maxLength: <span style="color: #800080;">2000</span><span style="color: #000000;">),
                        CreationTime </span>= c.DateTime(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        CreatorUserId </span>=<span style="color: #000000;"> c.Long(),
                        EditionId </span>=<span style="color: #000000;"> c.Int(),
                        TenantId </span>=<span style="color: #000000;"> c.Int(),
                        Discriminator </span>= c.String(nullable: <span style="color: #0000ff;">false</span>, maxLength: <span style="color: #800080;">128</span><span style="color: #000000;">),
                    },
                annotations: </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">
                {
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_TenantFeatureSetting_MustHaveTenant</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                })
                .PrimaryKey(t </span>=&gt;<span style="color: #000000;"> t.Id)
                .ForeignKey(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpEditions</span><span style="color: #800000;">"</span>, t =&gt; t.EditionId, cascadeDelete: <span style="color: #0000ff;">true</span><span style="color: #000000;">)
                .Index(t </span>=&gt;<span style="color: #000000;"> t.EditionId);
            
            CreateTable(
                </span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpEditions</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                c </span>=&gt; <span style="color: #0000ff;">new</span><span style="color: #000000;">
                    {
                        Id </span>= c.Int(nullable: <span style="color: #0000ff;">false</span>, identity: <span style="color: #0000ff;">true</span><span style="color: #000000;">),
                        Name </span>= c.String(nullable: <span style="color: #0000ff;">false</span>, maxLength: <span style="color: #800080;">32</span><span style="color: #000000;">),
                        DisplayName </span>= c.String(nullable: <span style="color: #0000ff;">false</span>, maxLength: <span style="color: #800080;">64</span><span style="color: #000000;">),
                        IsDeleted </span>= c.Boolean(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        DeleterUserId </span>=<span style="color: #000000;"> c.Long(),
                        DeletionTime </span>=<span style="color: #000000;"> c.DateTime(),
                        LastModificationTime </span>=<span style="color: #000000;"> c.DateTime(),
                        LastModifierUserId </span>=<span style="color: #000000;"> c.Long(),
                        CreationTime </span>= c.DateTime(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        CreatorUserId </span>=<span style="color: #000000;"> c.Long(),
                    },
                annotations: </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">
                {
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_Edition_SoftDelete</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                })
                .PrimaryKey(t </span>=&gt;<span style="color: #000000;"> t.Id);
            
            CreateTable(
                </span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpLanguages</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                c </span>=&gt; <span style="color: #0000ff;">new</span><span style="color: #000000;">
                    {
                        Id </span>= c.Int(nullable: <span style="color: #0000ff;">false</span>, identity: <span style="color: #0000ff;">true</span><span style="color: #000000;">),
                        TenantId </span>=<span style="color: #000000;"> c.Int(),
                        Name </span>= c.String(nullable: <span style="color: #0000ff;">false</span>, maxLength: <span style="color: #800080;">10</span><span style="color: #000000;">),
                        DisplayName </span>= c.String(nullable: <span style="color: #0000ff;">false</span>, maxLength: <span style="color: #800080;">64</span><span style="color: #000000;">),
                        Icon </span>= c.String(maxLength: <span style="color: #800080;">128</span><span style="color: #000000;">),
                        IsDisabled </span>= c.Boolean(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        IsDeleted </span>= c.Boolean(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        DeleterUserId </span>=<span style="color: #000000;"> c.Long(),
                        DeletionTime </span>=<span style="color: #000000;"> c.DateTime(),
                        LastModificationTime </span>=<span style="color: #000000;"> c.DateTime(),
                        LastModifierUserId </span>=<span style="color: #000000;"> c.Long(),
                        CreationTime </span>= c.DateTime(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        CreatorUserId </span>=<span style="color: #000000;"> c.Long(),
                    },
                annotations: </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">
                {
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_ApplicationLanguage_MayHaveTenant</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_ApplicationLanguage_SoftDelete</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                })
                .PrimaryKey(t </span>=&gt;<span style="color: #000000;"> t.Id);
            
            CreateTable(
                </span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpLanguageTexts</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                c </span>=&gt; <span style="color: #0000ff;">new</span><span style="color: #000000;">
                    {
                        Id </span>= c.Long(nullable: <span style="color: #0000ff;">false</span>, identity: <span style="color: #0000ff;">true</span><span style="color: #000000;">),
                        TenantId </span>=<span style="color: #000000;"> c.Int(),
                        LanguageName </span>= c.String(nullable: <span style="color: #0000ff;">false</span>, maxLength: <span style="color: #800080;">10</span><span style="color: #000000;">),
                        Source </span>= c.String(nullable: <span style="color: #0000ff;">false</span>, maxLength: <span style="color: #800080;">128</span><span style="color: #000000;">),
                        Key </span>= c.String(nullable: <span style="color: #0000ff;">false</span>, maxLength: <span style="color: #800080;">256</span><span style="color: #000000;">),
                        Value </span>= c.String(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        LastModificationTime </span>=<span style="color: #000000;"> c.DateTime(),
                        LastModifierUserId </span>=<span style="color: #000000;"> c.Long(),
                        CreationTime </span>= c.DateTime(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        CreatorUserId </span>=<span style="color: #000000;"> c.Long(),
                    },
                annotations: </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">
                {
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_ApplicationLanguageText_MayHaveTenant</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                })
                .PrimaryKey(t </span>=&gt;<span style="color: #000000;"> t.Id);
            
            CreateTable(
                </span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpNotifications</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                c </span>=&gt; <span style="color: #0000ff;">new</span><span style="color: #000000;">
                    {
                        Id </span>= c.Guid(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        NotificationName </span>= c.String(nullable: <span style="color: #0000ff;">false</span>, maxLength: <span style="color: #800080;">96</span><span style="color: #000000;">),
                        Data </span>=<span style="color: #000000;"> c.String(),
                        DataTypeName </span>= c.String(maxLength: <span style="color: #800080;">512</span><span style="color: #000000;">),
                        EntityTypeName </span>= c.String(maxLength: <span style="color: #800080;">250</span><span style="color: #000000;">),
                        EntityTypeAssemblyQualifiedName </span>= c.String(maxLength: <span style="color: #800080;">512</span><span style="color: #000000;">),
                        EntityId </span>= c.String(maxLength: <span style="color: #800080;">96</span><span style="color: #000000;">),
                        Severity </span>= c.Byte(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        UserIds </span>=<span style="color: #000000;"> c.String(),
                        ExcludedUserIds </span>=<span style="color: #000000;"> c.String(),
                        TenantIds </span>=<span style="color: #000000;"> c.String(),
                        CreationTime </span>= c.DateTime(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        CreatorUserId </span>=<span style="color: #000000;"> c.Long(),
                    })
                .PrimaryKey(t </span>=&gt;<span style="color: #000000;"> t.Id);
            
            CreateTable(
                </span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpNotificationSubscriptions</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                c </span>=&gt; <span style="color: #0000ff;">new</span><span style="color: #000000;">
                    {
                        Id </span>= c.Guid(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        TenantId </span>=<span style="color: #000000;"> c.Int(),
                        UserId </span>= c.Long(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        NotificationName </span>= c.String(maxLength: <span style="color: #800080;">96</span><span style="color: #000000;">),
                        EntityTypeName </span>= c.String(maxLength: <span style="color: #800080;">250</span><span style="color: #000000;">),
                        EntityTypeAssemblyQualifiedName </span>= c.String(maxLength: <span style="color: #800080;">512</span><span style="color: #000000;">),
                        EntityId </span>= c.String(maxLength: <span style="color: #800080;">96</span><span style="color: #000000;">),
                        CreationTime </span>= c.DateTime(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        CreatorUserId </span>=<span style="color: #000000;"> c.Long(),
                    },
                annotations: </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">
                {
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_NotificationSubscriptionInfo_MayHaveTenant</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                })
                .PrimaryKey(t </span>=&gt;<span style="color: #000000;"> t.Id)
                .Index(t </span>=&gt; <span style="color: #0000ff;">new</span><span style="color: #000000;"> { t.NotificationName, t.EntityTypeName, t.EntityId, t.UserId });
            
            CreateTable(
                </span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpOrganizationUnits</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                c </span>=&gt; <span style="color: #0000ff;">new</span><span style="color: #000000;">
                    {
                        Id </span>= c.Long(nullable: <span style="color: #0000ff;">false</span>, identity: <span style="color: #0000ff;">true</span><span style="color: #000000;">),
                        TenantId </span>=<span style="color: #000000;"> c.Int(),
                        ParentId </span>=<span style="color: #000000;"> c.Long(),
                        Code </span>= c.String(nullable: <span style="color: #0000ff;">false</span>, maxLength: <span style="color: #800080;">95</span><span style="color: #000000;">),
                        DisplayName </span>= c.String(nullable: <span style="color: #0000ff;">false</span>, maxLength: <span style="color: #800080;">128</span><span style="color: #000000;">),
                        IsDeleted </span>= c.Boolean(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        DeleterUserId </span>=<span style="color: #000000;"> c.Long(),
                        DeletionTime </span>=<span style="color: #000000;"> c.DateTime(),
                        LastModificationTime </span>=<span style="color: #000000;"> c.DateTime(),
                        LastModifierUserId </span>=<span style="color: #000000;"> c.Long(),
                        CreationTime </span>= c.DateTime(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        CreatorUserId </span>=<span style="color: #000000;"> c.Long(),
                    },
                annotations: </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">
                {
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_OrganizationUnit_MayHaveTenant</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_OrganizationUnit_SoftDelete</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                })
                .PrimaryKey(t </span>=&gt;<span style="color: #000000;"> t.Id)
                .ForeignKey(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpOrganizationUnits</span><span style="color: #800000;">"</span>, t =&gt;<span style="color: #000000;"> t.ParentId)
                .Index(t </span>=&gt;<span style="color: #000000;"> t.ParentId);
            
            CreateTable(
                </span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpPermissions</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                c </span>=&gt; <span style="color: #0000ff;">new</span><span style="color: #000000;">
                    {
                        Id </span>= c.Long(nullable: <span style="color: #0000ff;">false</span>, identity: <span style="color: #0000ff;">true</span><span style="color: #000000;">),
                        TenantId </span>=<span style="color: #000000;"> c.Int(),
                        Name </span>= c.String(nullable: <span style="color: #0000ff;">false</span>, maxLength: <span style="color: #800080;">128</span><span style="color: #000000;">),
                        IsGranted </span>= c.Boolean(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        CreationTime </span>= c.DateTime(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        CreatorUserId </span>=<span style="color: #000000;"> c.Long(),
                        RoleId </span>=<span style="color: #000000;"> c.Int(),
                        UserId </span>=<span style="color: #000000;"> c.Long(),
                        Discriminator </span>= c.String(nullable: <span style="color: #0000ff;">false</span>, maxLength: <span style="color: #800080;">128</span><span style="color: #000000;">),
                    },
                annotations: </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">
                {
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_PermissionSetting_MayHaveTenant</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_RolePermissionSetting_MayHaveTenant</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_UserPermissionSetting_MayHaveTenant</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                })
                .PrimaryKey(t </span>=&gt;<span style="color: #000000;"> t.Id)
                .ForeignKey(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUsers</span><span style="color: #800000;">"</span>, t =&gt; t.UserId, cascadeDelete: <span style="color: #0000ff;">true</span><span style="color: #000000;">)
                .ForeignKey(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpRoles</span><span style="color: #800000;">"</span>, t =&gt; t.RoleId, cascadeDelete: <span style="color: #0000ff;">true</span><span style="color: #000000;">)
                .Index(t </span>=&gt;<span style="color: #000000;"> t.RoleId)
                .Index(t </span>=&gt;<span style="color: #000000;"> t.UserId);
            
            CreateTable(
                </span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpRoles</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                c </span>=&gt; <span style="color: #0000ff;">new</span><span style="color: #000000;">
                    {
                        Id </span>= c.Int(nullable: <span style="color: #0000ff;">false</span>, identity: <span style="color: #0000ff;">true</span><span style="color: #000000;">),
                        Description </span>=<span style="color: #000000;"> c.String(),
                        TenantId </span>=<span style="color: #000000;"> c.Int(),
                        Name </span>= c.String(nullable: <span style="color: #0000ff;">false</span>, maxLength: <span style="color: #800080;">32</span><span style="color: #000000;">),
                        DisplayName </span>= c.String(nullable: <span style="color: #0000ff;">false</span>, maxLength: <span style="color: #800080;">64</span><span style="color: #000000;">),
                        IsStatic </span>= c.Boolean(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        IsDefault </span>= c.Boolean(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        IsDeleted </span>= c.Boolean(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        DeleterUserId </span>=<span style="color: #000000;"> c.Long(),
                        DeletionTime </span>=<span style="color: #000000;"> c.DateTime(),
                        LastModificationTime </span>=<span style="color: #000000;"> c.DateTime(),
                        LastModifierUserId </span>=<span style="color: #000000;"> c.Long(),
                        CreationTime </span>= c.DateTime(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        CreatorUserId </span>=<span style="color: #000000;"> c.Long(),
                    },
                annotations: </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">
                {
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_Role_MayHaveTenant</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_Role_SoftDelete</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                })
                .PrimaryKey(t </span>=&gt;<span style="color: #000000;"> t.Id)
                .ForeignKey(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUsers</span><span style="color: #800000;">"</span>, t =&gt;<span style="color: #000000;"> t.CreatorUserId)
                .ForeignKey(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUsers</span><span style="color: #800000;">"</span>, t =&gt;<span style="color: #000000;"> t.DeleterUserId)
                .ForeignKey(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUsers</span><span style="color: #800000;">"</span>, t =&gt;<span style="color: #000000;"> t.LastModifierUserId)
                .Index(t </span>=&gt;<span style="color: #000000;"> t.DeleterUserId)
                .Index(t </span>=&gt;<span style="color: #000000;"> t.LastModifierUserId)
                .Index(t </span>=&gt;<span style="color: #000000;"> t.CreatorUserId);
            
            CreateTable(
                </span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUsers</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                c </span>=&gt; <span style="color: #0000ff;">new</span><span style="color: #000000;">
                    {
                        Id </span>= c.Long(nullable: <span style="color: #0000ff;">false</span>, identity: <span style="color: #0000ff;">true</span><span style="color: #000000;">),
                        AuthenticationSource </span>= c.String(maxLength: <span style="color: #800080;">64</span><span style="color: #000000;">),
                        UserName </span>= c.String(nullable: <span style="color: #0000ff;">false</span>, maxLength: <span style="color: #800080;">32</span><span style="color: #000000;">),
                        TenantId </span>=<span style="color: #000000;"> c.Int(),
                        EmailAddress </span>= c.String(nullable: <span style="color: #0000ff;">false</span>, maxLength: <span style="color: #800080;">256</span><span style="color: #000000;">),
                        Name </span>= c.String(nullable: <span style="color: #0000ff;">false</span>, maxLength: <span style="color: #800080;">32</span><span style="color: #000000;">),
                        Surname </span>= c.String(nullable: <span style="color: #0000ff;">false</span>, maxLength: <span style="color: #800080;">32</span><span style="color: #000000;">),
                        Password </span>= c.String(nullable: <span style="color: #0000ff;">false</span>, maxLength: <span style="color: #800080;">128</span><span style="color: #000000;">),
                        EmailConfirmationCode </span>= c.String(maxLength: <span style="color: #800080;">328</span><span style="color: #000000;">),
                        PasswordResetCode </span>= c.String(maxLength: <span style="color: #800080;">328</span><span style="color: #000000;">),
                        LockoutEndDateUtc </span>=<span style="color: #000000;"> c.DateTime(),
                        AccessFailedCount </span>= c.Int(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        IsLockoutEnabled </span>= c.Boolean(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        PhoneNumber </span>=<span style="color: #000000;"> c.String(),
                        IsPhoneNumberConfirmed </span>= c.Boolean(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        SecurityStamp </span>=<span style="color: #000000;"> c.String(),
                        IsTwoFactorEnabled </span>= c.Boolean(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        IsEmailConfirmed </span>= c.Boolean(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        IsActive </span>= c.Boolean(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        LastLoginTime </span>=<span style="color: #000000;"> c.DateTime(),
                        IsDeleted </span>= c.Boolean(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        DeleterUserId </span>=<span style="color: #000000;"> c.Long(),
                        DeletionTime </span>=<span style="color: #000000;"> c.DateTime(),
                        LastModificationTime </span>=<span style="color: #000000;"> c.DateTime(),
                        LastModifierUserId </span>=<span style="color: #000000;"> c.Long(),
                        CreationTime </span>= c.DateTime(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        CreatorUserId </span>=<span style="color: #000000;"> c.Long(),
                    },
                annotations: </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">
                {
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_User_MayHaveTenant</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_User_SoftDelete</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                })
                .PrimaryKey(t </span>=&gt;<span style="color: #000000;"> t.Id)
                .ForeignKey(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUsers</span><span style="color: #800000;">"</span>, t =&gt;<span style="color: #000000;"> t.CreatorUserId)
                .ForeignKey(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUsers</span><span style="color: #800000;">"</span>, t =&gt;<span style="color: #000000;"> t.DeleterUserId)
                .ForeignKey(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUsers</span><span style="color: #800000;">"</span>, t =&gt;<span style="color: #000000;"> t.LastModifierUserId)
                .Index(t </span>=&gt;<span style="color: #000000;"> t.DeleterUserId)
                .Index(t </span>=&gt;<span style="color: #000000;"> t.LastModifierUserId)
                .Index(t </span>=&gt;<span style="color: #000000;"> t.CreatorUserId);
            
            CreateTable(
                </span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUserClaims</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                c </span>=&gt; <span style="color: #0000ff;">new</span><span style="color: #000000;">
                    {
                        Id </span>= c.Long(nullable: <span style="color: #0000ff;">false</span>, identity: <span style="color: #0000ff;">true</span><span style="color: #000000;">),
                        TenantId </span>=<span style="color: #000000;"> c.Int(),
                        UserId </span>= c.Long(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        ClaimType </span>=<span style="color: #000000;"> c.String(),
                        ClaimValue </span>=<span style="color: #000000;"> c.String(),
                        CreationTime </span>= c.DateTime(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        CreatorUserId </span>=<span style="color: #000000;"> c.Long(),
                    },
                annotations: </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">
                {
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_UserClaim_MayHaveTenant</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                })
                .PrimaryKey(t </span>=&gt;<span style="color: #000000;"> t.Id)
                .ForeignKey(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUsers</span><span style="color: #800000;">"</span>, t =&gt; t.UserId, cascadeDelete: <span style="color: #0000ff;">true</span><span style="color: #000000;">)
                .Index(t </span>=&gt;<span style="color: #000000;"> t.UserId);
            
            CreateTable(
                </span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUserLogins</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                c </span>=&gt; <span style="color: #0000ff;">new</span><span style="color: #000000;">
                    {
                        Id </span>= c.Long(nullable: <span style="color: #0000ff;">false</span>, identity: <span style="color: #0000ff;">true</span><span style="color: #000000;">),
                        TenantId </span>=<span style="color: #000000;"> c.Int(),
                        UserId </span>= c.Long(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        LoginProvider </span>= c.String(nullable: <span style="color: #0000ff;">false</span>, maxLength: <span style="color: #800080;">128</span><span style="color: #000000;">),
                        ProviderKey </span>= c.String(nullable: <span style="color: #0000ff;">false</span>, maxLength: <span style="color: #800080;">256</span><span style="color: #000000;">),
                    },
                annotations: </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">
                {
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_UserLogin_MayHaveTenant</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                })
                .PrimaryKey(t </span>=&gt;<span style="color: #000000;"> t.Id)
                .ForeignKey(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUsers</span><span style="color: #800000;">"</span>, t =&gt; t.UserId, cascadeDelete: <span style="color: #0000ff;">true</span><span style="color: #000000;">)
                .Index(t </span>=&gt;<span style="color: #000000;"> t.UserId);
            
            CreateTable(
                </span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUserRoles</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                c </span>=&gt; <span style="color: #0000ff;">new</span><span style="color: #000000;">
                    {
                        Id </span>= c.Long(nullable: <span style="color: #0000ff;">false</span>, identity: <span style="color: #0000ff;">true</span><span style="color: #000000;">),
                        TenantId </span>=<span style="color: #000000;"> c.Int(),
                        UserId </span>= c.Long(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        RoleId </span>= c.Int(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        CreationTime </span>= c.DateTime(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        CreatorUserId </span>=<span style="color: #000000;"> c.Long(),
                    },
                annotations: </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">
                {
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_UserRole_MayHaveTenant</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                })
                .PrimaryKey(t </span>=&gt;<span style="color: #000000;"> t.Id)
                .ForeignKey(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUsers</span><span style="color: #800000;">"</span>, t =&gt; t.UserId, cascadeDelete: <span style="color: #0000ff;">true</span><span style="color: #000000;">)
                .Index(t </span>=&gt;<span style="color: #000000;"> t.UserId);
            
            CreateTable(
                </span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpSettings</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                c </span>=&gt; <span style="color: #0000ff;">new</span><span style="color: #000000;">
                    {
                        Id </span>= c.Long(nullable: <span style="color: #0000ff;">false</span>, identity: <span style="color: #0000ff;">true</span><span style="color: #000000;">),
                        TenantId </span>=<span style="color: #000000;"> c.Int(),
                        UserId </span>=<span style="color: #000000;"> c.Long(),
                        Name </span>= c.String(nullable: <span style="color: #0000ff;">false</span>, maxLength: <span style="color: #800080;">256</span><span style="color: #000000;">),
                        Value </span>= c.String(maxLength: <span style="color: #800080;">2000</span><span style="color: #000000;">),
                        LastModificationTime </span>=<span style="color: #000000;"> c.DateTime(),
                        LastModifierUserId </span>=<span style="color: #000000;"> c.Long(),
                        CreationTime </span>= c.DateTime(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        CreatorUserId </span>=<span style="color: #000000;"> c.Long(),
                    },
                annotations: </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">
                {
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_Setting_MayHaveTenant</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                })
                .PrimaryKey(t </span>=&gt;<span style="color: #000000;"> t.Id)
                .ForeignKey(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUsers</span><span style="color: #800000;">"</span>, t =&gt;<span style="color: #000000;"> t.UserId)
                .Index(t </span>=&gt;<span style="color: #000000;"> t.UserId);
            
            CreateTable(
                </span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpTenantNotifications</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                c </span>=&gt; <span style="color: #0000ff;">new</span><span style="color: #000000;">
                    {
                        Id </span>= c.Guid(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        TenantId </span>=<span style="color: #000000;"> c.Int(),
                        NotificationName </span>= c.String(nullable: <span style="color: #0000ff;">false</span>, maxLength: <span style="color: #800080;">96</span><span style="color: #000000;">),
                        Data </span>=<span style="color: #000000;"> c.String(),
                        DataTypeName </span>= c.String(maxLength: <span style="color: #800080;">512</span><span style="color: #000000;">),
                        EntityTypeName </span>= c.String(maxLength: <span style="color: #800080;">250</span><span style="color: #000000;">),
                        EntityTypeAssemblyQualifiedName </span>= c.String(maxLength: <span style="color: #800080;">512</span><span style="color: #000000;">),
                        EntityId </span>= c.String(maxLength: <span style="color: #800080;">96</span><span style="color: #000000;">),
                        Severity </span>= c.Byte(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        CreationTime </span>= c.DateTime(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        CreatorUserId </span>=<span style="color: #000000;"> c.Long(),
                    },
                annotations: </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">
                {
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_TenantNotificationInfo_MayHaveTenant</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                })
                .PrimaryKey(t </span>=&gt;<span style="color: #000000;"> t.Id);
            
            CreateTable(
                </span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpTenants</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                c </span>=&gt; <span style="color: #0000ff;">new</span><span style="color: #000000;">
                    {
                        Id </span>= c.Int(nullable: <span style="color: #0000ff;">false</span>, identity: <span style="color: #0000ff;">true</span><span style="color: #000000;">),
                        EditionId </span>=<span style="color: #000000;"> c.Int(),
                        Name </span>= c.String(nullable: <span style="color: #0000ff;">false</span>, maxLength: <span style="color: #800080;">128</span><span style="color: #000000;">),
                        TenancyName </span>= c.String(nullable: <span style="color: #0000ff;">false</span>, maxLength: <span style="color: #800080;">64</span><span style="color: #000000;">),
                        ConnectionString </span>= c.String(maxLength: <span style="color: #800080;">1024</span><span style="color: #000000;">),
                        IsActive </span>= c.Boolean(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        IsDeleted </span>= c.Boolean(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        DeleterUserId </span>=<span style="color: #000000;"> c.Long(),
                        DeletionTime </span>=<span style="color: #000000;"> c.DateTime(),
                        LastModificationTime </span>=<span style="color: #000000;"> c.DateTime(),
                        LastModifierUserId </span>=<span style="color: #000000;"> c.Long(),
                        CreationTime </span>= c.DateTime(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        CreatorUserId </span>=<span style="color: #000000;"> c.Long(),
                    },
                annotations: </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">
                {
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_Tenant_SoftDelete</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                })
                .PrimaryKey(t </span>=&gt;<span style="color: #000000;"> t.Id)
                .ForeignKey(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUsers</span><span style="color: #800000;">"</span>, t =&gt;<span style="color: #000000;"> t.CreatorUserId)
                .ForeignKey(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUsers</span><span style="color: #800000;">"</span>, t =&gt;<span style="color: #000000;"> t.DeleterUserId)
                .ForeignKey(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpEditions</span><span style="color: #800000;">"</span>, t =&gt;<span style="color: #000000;"> t.EditionId)
                .ForeignKey(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUsers</span><span style="color: #800000;">"</span>, t =&gt;<span style="color: #000000;"> t.LastModifierUserId)
                .Index(t </span>=&gt;<span style="color: #000000;"> t.EditionId)
                .Index(t </span>=&gt;<span style="color: #000000;"> t.DeleterUserId)
                .Index(t </span>=&gt;<span style="color: #000000;"> t.LastModifierUserId)
                .Index(t </span>=&gt;<span style="color: #000000;"> t.CreatorUserId);
            
            CreateTable(
                </span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUserAccounts</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                c </span>=&gt; <span style="color: #0000ff;">new</span><span style="color: #000000;">
                    {
                        Id </span>= c.Long(nullable: <span style="color: #0000ff;">false</span>, identity: <span style="color: #0000ff;">true</span><span style="color: #000000;">),
                        TenantId </span>=<span style="color: #000000;"> c.Int(),
                        UserId </span>= c.Long(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        UserLinkId </span>=<span style="color: #000000;"> c.Long(),
                        UserName </span>=<span style="color: #000000;"> c.String(),
                        EmailAddress </span>=<span style="color: #000000;"> c.String(),
                        LastLoginTime </span>=<span style="color: #000000;"> c.DateTime(),
                        IsDeleted </span>= c.Boolean(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        DeleterUserId </span>=<span style="color: #000000;"> c.Long(),
                        DeletionTime </span>=<span style="color: #000000;"> c.DateTime(),
                        LastModificationTime </span>=<span style="color: #000000;"> c.DateTime(),
                        LastModifierUserId </span>=<span style="color: #000000;"> c.Long(),
                        CreationTime </span>= c.DateTime(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        CreatorUserId </span>=<span style="color: #000000;"> c.Long(),
                    },
                annotations: </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">
                {
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_UserAccount_SoftDelete</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                })
                .PrimaryKey(t </span>=&gt;<span style="color: #000000;"> t.Id);
            
            CreateTable(
                </span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUserLoginAttempts</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                c </span>=&gt; <span style="color: #0000ff;">new</span><span style="color: #000000;">
                    {
                        Id </span>= c.Long(nullable: <span style="color: #0000ff;">false</span>, identity: <span style="color: #0000ff;">true</span><span style="color: #000000;">),
                        TenantId </span>=<span style="color: #000000;"> c.Int(),
                        TenancyName </span>= c.String(maxLength: <span style="color: #800080;">64</span><span style="color: #000000;">),
                        UserId </span>=<span style="color: #000000;"> c.Long(),
                        UserNameOrEmailAddress </span>= c.String(maxLength: <span style="color: #800080;">255</span><span style="color: #000000;">),
                        ClientIpAddress </span>= c.String(maxLength: <span style="color: #800080;">64</span><span style="color: #000000;">),
                        ClientName </span>= c.String(maxLength: <span style="color: #800080;">128</span><span style="color: #000000;">),
                        BrowserInfo </span>= c.String(maxLength: <span style="color: #800080;">256</span><span style="color: #000000;">),
                        Result </span>= c.Byte(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        CreationTime </span>= c.DateTime(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                    },
                annotations: </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">
                {
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_UserLoginAttempt_MayHaveTenant</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                })
                .PrimaryKey(t </span>=&gt;<span style="color: #000000;"> t.Id)
                .Index(t </span>=&gt; <span style="color: #0000ff;">new</span><span style="color: #000000;"> { t.UserId, t.TenantId })
                .Index(t </span>=&gt; <span style="color: #0000ff;">new</span><span style="color: #000000;"> { t.TenancyName, t.UserNameOrEmailAddress, t.Result });
            
            CreateTable(
                </span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUserNotifications</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                c </span>=&gt; <span style="color: #0000ff;">new</span><span style="color: #000000;">
                    {
                        Id </span>= c.Guid(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        TenantId </span>=<span style="color: #000000;"> c.Int(),
                        UserId </span>= c.Long(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        TenantNotificationId </span>= c.Guid(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        State </span>= c.Int(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        CreationTime </span>= c.DateTime(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                    },
                annotations: </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">
                {
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_UserNotificationInfo_MayHaveTenant</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                })
                .PrimaryKey(t </span>=&gt;<span style="color: #000000;"> t.Id)
                .Index(t </span>=&gt; <span style="color: #0000ff;">new</span><span style="color: #000000;"> { t.UserId, t.State, t.CreationTime });
            
            CreateTable(
                </span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUserOrganizationUnits</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                c </span>=&gt; <span style="color: #0000ff;">new</span><span style="color: #000000;">
                    {
                        Id </span>= c.Long(nullable: <span style="color: #0000ff;">false</span>, identity: <span style="color: #0000ff;">true</span><span style="color: #000000;">),
                        TenantId </span>=<span style="color: #000000;"> c.Int(),
                        UserId </span>= c.Long(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        OrganizationUnitId </span>= c.Long(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        CreationTime </span>= c.DateTime(nullable: <span style="color: #0000ff;">false</span><span style="color: #000000;">),
                        CreatorUserId </span>=<span style="color: #000000;"> c.Long(),
                    },
                annotations: </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">
                {
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_UserOrganizationUnit_MayHaveTenant</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                })
                .PrimaryKey(t </span>=&gt;<span style="color: #000000;"> t.Id);
            
        }
        
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Down()
        {
            DropForeignKey(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpTenants</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">LastModifierUserId</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUsers</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            DropForeignKey(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpTenants</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EditionId</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpEditions</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            DropForeignKey(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpTenants</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">DeleterUserId</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUsers</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            DropForeignKey(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpTenants</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">CreatorUserId</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUsers</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            DropForeignKey(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpPermissions</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">RoleId</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpRoles</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            DropForeignKey(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpRoles</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">LastModifierUserId</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUsers</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            DropForeignKey(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpRoles</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">DeleterUserId</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUsers</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            DropForeignKey(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpRoles</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">CreatorUserId</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUsers</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            DropForeignKey(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpSettings</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">UserId</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUsers</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            DropForeignKey(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUserRoles</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">UserId</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUsers</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            DropForeignKey(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpPermissions</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">UserId</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUsers</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            DropForeignKey(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUserLogins</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">UserId</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUsers</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            DropForeignKey(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUsers</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">LastModifierUserId</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUsers</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            DropForeignKey(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUsers</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">DeleterUserId</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUsers</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            DropForeignKey(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUsers</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">CreatorUserId</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUsers</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            DropForeignKey(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUserClaims</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">UserId</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUsers</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            DropForeignKey(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpOrganizationUnits</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">ParentId</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpOrganizationUnits</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            DropForeignKey(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpFeatures</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EditionId</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpEditions</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            DropIndex(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUserNotifications</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span>[] { <span style="color: #800000;">"</span><span style="color: #800000;">UserId</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">State</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">CreationTime</span><span style="color: #800000;">"</span><span style="color: #000000;"> });
            DropIndex(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUserLoginAttempts</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span>[] { <span style="color: #800000;">"</span><span style="color: #800000;">TenancyName</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">UserNameOrEmailAddress</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">Result</span><span style="color: #800000;">"</span><span style="color: #000000;"> });
            DropIndex(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUserLoginAttempts</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span>[] { <span style="color: #800000;">"</span><span style="color: #800000;">UserId</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">TenantId</span><span style="color: #800000;">"</span><span style="color: #000000;"> });
            DropIndex(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpTenants</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span>[] { <span style="color: #800000;">"</span><span style="color: #800000;">CreatorUserId</span><span style="color: #800000;">"</span><span style="color: #000000;"> });
            DropIndex(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpTenants</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span>[] { <span style="color: #800000;">"</span><span style="color: #800000;">LastModifierUserId</span><span style="color: #800000;">"</span><span style="color: #000000;"> });
            DropIndex(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpTenants</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span>[] { <span style="color: #800000;">"</span><span style="color: #800000;">DeleterUserId</span><span style="color: #800000;">"</span><span style="color: #000000;"> });
            DropIndex(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpTenants</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span>[] { <span style="color: #800000;">"</span><span style="color: #800000;">EditionId</span><span style="color: #800000;">"</span><span style="color: #000000;"> });
            DropIndex(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpSettings</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span>[] { <span style="color: #800000;">"</span><span style="color: #800000;">UserId</span><span style="color: #800000;">"</span><span style="color: #000000;"> });
            DropIndex(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUserRoles</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span>[] { <span style="color: #800000;">"</span><span style="color: #800000;">UserId</span><span style="color: #800000;">"</span><span style="color: #000000;"> });
            DropIndex(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUserLogins</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span>[] { <span style="color: #800000;">"</span><span style="color: #800000;">UserId</span><span style="color: #800000;">"</span><span style="color: #000000;"> });
            DropIndex(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUserClaims</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span>[] { <span style="color: #800000;">"</span><span style="color: #800000;">UserId</span><span style="color: #800000;">"</span><span style="color: #000000;"> });
            DropIndex(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUsers</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span>[] { <span style="color: #800000;">"</span><span style="color: #800000;">CreatorUserId</span><span style="color: #800000;">"</span><span style="color: #000000;"> });
            DropIndex(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUsers</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span>[] { <span style="color: #800000;">"</span><span style="color: #800000;">LastModifierUserId</span><span style="color: #800000;">"</span><span style="color: #000000;"> });
            DropIndex(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUsers</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span>[] { <span style="color: #800000;">"</span><span style="color: #800000;">DeleterUserId</span><span style="color: #800000;">"</span><span style="color: #000000;"> });
            DropIndex(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpRoles</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span>[] { <span style="color: #800000;">"</span><span style="color: #800000;">CreatorUserId</span><span style="color: #800000;">"</span><span style="color: #000000;"> });
            DropIndex(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpRoles</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span>[] { <span style="color: #800000;">"</span><span style="color: #800000;">LastModifierUserId</span><span style="color: #800000;">"</span><span style="color: #000000;"> });
            DropIndex(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpRoles</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span>[] { <span style="color: #800000;">"</span><span style="color: #800000;">DeleterUserId</span><span style="color: #800000;">"</span><span style="color: #000000;"> });
            DropIndex(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpPermissions</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span>[] { <span style="color: #800000;">"</span><span style="color: #800000;">UserId</span><span style="color: #800000;">"</span><span style="color: #000000;"> });
            DropIndex(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpPermissions</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span>[] { <span style="color: #800000;">"</span><span style="color: #800000;">RoleId</span><span style="color: #800000;">"</span><span style="color: #000000;"> });
            DropIndex(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpOrganizationUnits</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span>[] { <span style="color: #800000;">"</span><span style="color: #800000;">ParentId</span><span style="color: #800000;">"</span><span style="color: #000000;"> });
            DropIndex(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpNotificationSubscriptions</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span>[] { <span style="color: #800000;">"</span><span style="color: #800000;">NotificationName</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityTypeName</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityId</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">UserId</span><span style="color: #800000;">"</span><span style="color: #000000;"> });
            DropIndex(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpFeatures</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span>[] { <span style="color: #800000;">"</span><span style="color: #800000;">EditionId</span><span style="color: #800000;">"</span><span style="color: #000000;"> });
            DropIndex(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpBackgroundJobs</span><span style="color: #800000;">"</span>, <span style="color: #0000ff;">new</span>[] { <span style="color: #800000;">"</span><span style="color: #800000;">IsAbandoned</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">NextTryTime</span><span style="color: #800000;">"</span><span style="color: #000000;"> });
            DropTable(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUserOrganizationUnits</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                removedAnnotations: </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">
                {
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_UserOrganizationUnit_MayHaveTenant</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                });
            DropTable(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUserNotifications</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                removedAnnotations: </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">
                {
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_UserNotificationInfo_MayHaveTenant</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                });
            DropTable(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUserLoginAttempts</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                removedAnnotations: </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">
                {
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_UserLoginAttempt_MayHaveTenant</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                });
            DropTable(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUserAccounts</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                removedAnnotations: </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">
                {
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_UserAccount_SoftDelete</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                });
            DropTable(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpTenants</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                removedAnnotations: </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">
                {
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_Tenant_SoftDelete</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                });
            DropTable(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpTenantNotifications</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                removedAnnotations: </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">
                {
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_TenantNotificationInfo_MayHaveTenant</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                });
            DropTable(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpSettings</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                removedAnnotations: </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">
                {
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_Setting_MayHaveTenant</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                });
            DropTable(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUserRoles</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                removedAnnotations: </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">
                {
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_UserRole_MayHaveTenant</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                });
            DropTable(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUserLogins</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                removedAnnotations: </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">
                {
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_UserLogin_MayHaveTenant</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                });
            DropTable(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUserClaims</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                removedAnnotations: </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">
                {
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_UserClaim_MayHaveTenant</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                });
            DropTable(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpUsers</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                removedAnnotations: </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">
                {
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_User_MayHaveTenant</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_User_SoftDelete</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                });
            DropTable(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpRoles</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                removedAnnotations: </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">
                {
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_Role_MayHaveTenant</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_Role_SoftDelete</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                });
            DropTable(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpPermissions</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                removedAnnotations: </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">
                {
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_PermissionSetting_MayHaveTenant</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_RolePermissionSetting_MayHaveTenant</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_UserPermissionSetting_MayHaveTenant</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                });
            DropTable(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpOrganizationUnits</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                removedAnnotations: </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">
                {
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_OrganizationUnit_MayHaveTenant</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_OrganizationUnit_SoftDelete</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                });
            DropTable(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpNotificationSubscriptions</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                removedAnnotations: </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">
                {
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_NotificationSubscriptionInfo_MayHaveTenant</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                });
            DropTable(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpNotifications</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            DropTable(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpLanguageTexts</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                removedAnnotations: </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">
                {
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_ApplicationLanguageText_MayHaveTenant</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                });
            DropTable(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpLanguages</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                removedAnnotations: </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">
                {
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_ApplicationLanguage_MayHaveTenant</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_ApplicationLanguage_SoftDelete</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                });
            DropTable(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpEditions</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                removedAnnotations: </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">
                {
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_Edition_SoftDelete</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                });
            DropTable(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpFeatures</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                removedAnnotations: </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">
                {
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_TenantFeatureSetting_MustHaveTenant</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                });
            DropTable(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpBackgroundJobs</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            DropTable(</span><span style="color: #800000;">"</span><span style="color: #800000;">dbo.AbpAuditLogs</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                removedAnnotations: </span><span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">string</span>, <span style="color: #0000ff;">object</span>&gt;<span style="color: #000000;">
                {
                    { </span><span style="color: #800000;">"</span><span style="color: #800000;">DynamicFilter_AuditLog_MayHaveTenant</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">EntityFramework.DynamicFilters.DynamicFilterDefinition</span><span style="color: #800000;">"</span><span style="color: #000000;"> },
                });
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">init</span></div>
<p>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('6975c775-33b8-4691-8001-974260f0eb9f')"><img id="code_img_closed_6975c775-33b8-4691-8001-974260f0eb9f" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_6975c775-33b8-4691-8001-974260f0eb9f" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('6975c775-33b8-4691-8001-974260f0eb9f',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_6975c775-33b8-4691-8001-974260f0eb9f" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Dependency;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Domain.Uow;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.MultiTenancy;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Zero.EntityFramework;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.EntityFramework.EntityFramework;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.EntityFramework.Migrations
{
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
    <span style="color: #808080;">///</span><span style="color: #008000;"> 执行数据库迁移
    </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
    <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> AbpZeroDbMigrator : AbpZeroDbMigrator&lt;PMDBContext, Configuration&gt;<span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> AbpZeroDbMigrator(IUnitOfWorkManager unitOfWorkManager,
            IDbPerTenantConnectionStringResolver connectionStringResolver, IIocResolver iocResolver)
            : </span><span style="color: #0000ff;">base</span><span style="color: #000000;">(unitOfWorkManager, connectionStringResolver, iocResolver)
        {
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">AbpZeroDbMigrator</span></div>
<p>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('f6978d1b-771d-4e16-9df7-df182b677d3a')"><img id="code_img_closed_f6978d1b-771d-4e16-9df7-df182b677d3a" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_f6978d1b-771d-4e16-9df7-df182b677d3a" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('f6978d1b-771d-4e16-9df7-df182b677d3a',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_f6978d1b-771d-4e16-9df7-df182b677d3a" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.MultiTenancy;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Zero.EntityFramework;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> EntityFramework.DynamicFilters;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.EntityFramework.Migrations.SeedData;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.EntityFramework.Migrations
{
    </span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
    </span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Data.Entity;
    </span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Data.Entity.Migrations;
    </span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;

    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">sealed</span> <span style="color: #0000ff;">class</span> Configuration : DbMigrationsConfiguration&lt;PM.EntityFramework.EntityFramework.PMDBContext&gt;<span style="color: #000000;">,IMultiTenantSeed
    {
        </span><span style="color: #0000ff;">public</span> AbpTenantBase Tenant { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> Configuration()
        {
            AutomaticMigrationsEnabled </span>= <span style="color: #0000ff;">false</span><span style="color: #000000;">;
            ContextKey </span>= <span style="color: #800000;">"</span><span style="color: #800000;">PM</span><span style="color: #800000;">"</span><span style="color: #000000;">;
        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;">Seed() 方法会在你每次你执行 Update-Database 指令时被呼叫一次</span>
        <span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Seed(PM.EntityFramework.EntityFramework.PMDBContext context)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">禁用所有过滤</span>
<span style="color: #000000;">            context.DisableAllFilters();
            </span><span style="color: #0000ff;">if</span> (Tenant == <span style="color: #0000ff;">null</span><span style="color: #000000;">)
            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;">主机种子</span>
                <span style="color: #0000ff;">new</span><span style="color: #000000;"> InitialHostDbBuilder(context).Create();

                </span><span style="color: #008000;">//</span><span style="color: #008000;">默认租户种子</span>
                <span style="color: #0000ff;">new</span><span style="color: #000000;"> DefaultTenantCreator(context).Create();
                </span><span style="color: #0000ff;">new</span> TenantRoleAndUserBuilder(context, <span style="color: #800080;">1</span><span style="color: #000000;">).Create();
            }
            </span><span style="color: #0000ff;">else</span><span style="color: #000000;">
            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;">您可以为租户数据库添加种子并使用租户属性...</span>
<span style="color: #000000;">            }
            context.SaveChanges();
        }

    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">Configuration</span></div>
<p>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('a673a9fd-8804-4c22-96c9-e369d773763c')"><img id="code_img_closed_a673a9fd-8804-4c22-96c9-e369d773763c" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_a673a9fd-8804-4c22-96c9-e369d773763c" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('a673a9fd-8804-4c22-96c9-e369d773763c',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_a673a9fd-8804-4c22-96c9-e369d773763c" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Data.Entity;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Reflection;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Modules;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Zero.EntityFramework;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.EntityFramework.EntityFramework;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.EntityFramework
{
    [DependsOn(</span><span style="color: #0000ff;">typeof</span>(PMCoreModule),<span style="color: #0000ff;">typeof</span><span style="color: #000000;">(AbpZeroEntityFrameworkModule))]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> PMDataModule:AbpModule
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> PreInitialize()
        {
            Database.SetInitializer(</span><span style="color: #0000ff;">new</span> CreateDatabaseIfNotExists&lt;PMDBContext&gt;<span style="color: #000000;">());
            Configuration.DefaultNameOrConnectionString </span>= <span style="color: #800000;">"</span><span style="color: #800000;">Default</span><span style="color: #800000;">"</span><span style="color: #000000;">;
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Initialize()
        {
            IocManager.RegisterAssemblyByConvention(Assembly.GetExecutingAssembly());
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">PMDataModule</span></div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a4"></a>四、PM.Application</span></strong></span></p>
<p><strong>1，NuGet安装Abp.Zero2.1.3、Abp.AutoMapper2.1.3</strong></p>
<p><strong>程序集引用：System.ComponentModel.DataAnnotations</strong></p>
<p><strong><strong>2，基本结构</strong></strong></p>
<p><strong><strong><img src="http://images2017.cnblogs.com/blog/741594/201711/741594-20171103141320607-974345572.png" alt="" width="464" height="580" /></strong></strong></p>
<p>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('6e4169c2-7bb8-4aed-aec1-c736f61c64ce')"><img id="code_img_closed_6e4169c2-7bb8-4aed-aec1-c736f61c64ce" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_6e4169c2-7bb8-4aed-aec1-c736f61c64ce" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('6e4169c2-7bb8-4aed-aec1-c736f61c64ce',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_6e4169c2-7bb8-4aed-aec1-c736f61c64ce" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Application.Services;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.IdentityFramework;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Runtime.Session;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNet.Identity;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.MultiTenant;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.Users;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.Application
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> PMAppServiceBase:ApplicationService
    {
        </span><span style="color: #0000ff;">public</span> TenantManager TenantManager { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }
        </span><span style="color: #0000ff;">public</span> UserManager UserManager { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

        </span><span style="color: #0000ff;">protected</span><span style="color: #000000;"> PMAppServiceBase()
        {
            LocalizationSourceName </span>=<span style="color: #000000;"> PMProjectNameConsts.LocalizationSourceName;
        }

        </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">virtual</span> Task&lt;User&gt;<span style="color: #000000;"> GetCurrentUserAsync()
        {
            </span><span style="color: #0000ff;">var</span> user=<span style="color: #000000;"> UserManager.FindByIdAsync(AbpSession.GetUserId());
            </span><span style="color: #0000ff;">if</span> (user == <span style="color: #0000ff;">null</span><span style="color: #000000;">)
            {
                </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> ApplicationException(<span style="color: #800000;">"</span><span style="color: #800000;">目前没有用户！</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> user;
        }

        </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">virtual</span> Task&lt;Tenant&gt;<span style="color: #000000;"> GetCurrentTenantAsync()
        {
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> TenantManager.GetByIdAsync(AbpSession.GetTenantId());
        }

        </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">virtual</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> CheckErrors(IdentityResult identityResult)
        {
            identityResult.CheckErrors(LocalizationManager);
        }


    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">PMAppServiceBase</span></div>
<p>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('d9c12509-493f-44c3-846c-b265b01346c3')"><img id="code_img_closed_d9c12509-493f-44c3-846c-b265b01346c3" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_d9c12509-493f-44c3-846c-b265b01346c3" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('d9c12509-493f-44c3-846c-b265b01346c3',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_d9c12509-493f-44c3-846c-b265b01346c3" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Reflection;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Authorization;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Authorization.Roles;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.AutoMapper;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Modules;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Application.Roles.Dto;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Application.Users.Dto;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.Authorization.Roles;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.Users;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.Application
{
    [DependsOn(</span><span style="color: #0000ff;">typeof</span>(PMCoreModule),<span style="color: #0000ff;">typeof</span><span style="color: #000000;">(AbpAutoMapperModule))]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> PMApplicationModule:AbpModule
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Initialize()
        {
            IocManager.RegisterAssemblyByConvention(Assembly.GetExecutingAssembly());
            Configuration.Modules.AbpAutoMapper().Configurators.Add(cfg </span>=&gt;<span style="color: #000000;">
            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;"> Role and permission</span>
                cfg.CreateMap&lt;Permission, <span style="color: #0000ff;">string</span>&gt;().ConvertUsing(r =&gt;<span style="color: #000000;"> r.Name);
                cfg.CreateMap</span>&lt;RolePermissionSetting, <span style="color: #0000ff;">string</span>&gt;().ConvertUsing(r =&gt;<span style="color: #000000;"> r.Name);

                cfg.CreateMap</span>&lt;CreateRoleDto, Role&gt;().ForMember(x =&gt; x.Permissions, opt =&gt;<span style="color: #000000;"> opt.Ignore());
                cfg.CreateMap</span>&lt;RoleDto, Role&gt;().ForMember(x =&gt; x.Permissions, opt =&gt;<span style="color: #000000;"> opt.Ignore());

                cfg.CreateMap</span>&lt;UserDto, User&gt;<span style="color: #000000;">();
                cfg.CreateMap</span>&lt;UserDto, User&gt;().ForMember(x =&gt; x.Roles, opt =&gt;<span style="color: #000000;"> opt.Ignore());

                cfg.CreateMap</span>&lt;CreateUserDto, User&gt;<span style="color: #000000;">();
                cfg.CreateMap</span>&lt;CreateUserDto, User&gt;().ForMember(x =&gt; x.Roles, opt =&gt;<span style="color: #000000;"> opt.Ignore());
            });

        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">PMApplicationModule</span></div>
<p>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('50c6f8c5-025e-4e3e-b4e8-937788d118ed')"><img id="code_img_closed_50c6f8c5-025e-4e3e-b4e8-937788d118ed" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_50c6f8c5-025e-4e3e-b4e8-937788d118ed" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('50c6f8c5-025e-4e3e-b4e8-937788d118ed',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_50c6f8c5-025e-4e3e-b4e8-937788d118ed" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Zero.Configuration;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Application.Authorization.Accounts.Dto;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.Authorization.Users;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Configuration;
</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.Application.Authorization.Accounts
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> AccountAppService:PMAppServiceBase,IAccountAppService
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> UserRegistrationManager _userRegistrationManager;

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> AccountAppService(UserRegistrationManager userRegistrationManager)
        {
            _userRegistrationManager </span>=<span style="color: #000000;"> userRegistrationManager;
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task&lt;IsTenantAvaliableOutput&gt;<span style="color: #000000;"> IsTenantAvaliable(IsTenantAvaliableInput input)
        {
            </span><span style="color: #0000ff;">var</span> tenant = <span style="color: #0000ff;">await</span><span style="color: #000000;"> TenantManager.FindByTenancyNameAsync(input.TenantName);
            </span><span style="color: #0000ff;">if</span> (tenant == <span style="color: #0000ff;">null</span><span style="color: #000000;">)
            {
                </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> IsTenantAvaliableOutput(TenantAvaliablityState.NotFound);
            }
            </span><span style="color: #0000ff;">if</span> (!<span style="color: #000000;">tenant.IsActive)
            {
                </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> IsTenantAvaliableOutput(TenantAvaliablityState.InActive);
            }
            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> IsTenantAvaliableOutput(TenantAvaliablityState.Avaliable, tenant.Id);
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task&lt;RegisterOutput&gt;<span style="color: #000000;"> Register(RegisterInput input)
        {
            </span><span style="color: #0000ff;">var</span> user =<span style="color: #0000ff;">await</span><span style="color: #000000;"> _userRegistrationManager.RegisterAsync(input.Name, input.Surname, input.EmailAddress,
                input.UserName,
                input.Password, </span><span style="color: #0000ff;">false</span><span style="color: #000000;">);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">电子邮件确认需要登录</span>
            <span style="color: #0000ff;">var</span> isEmailConfirmationRequiredForLogin = <span style="color: #0000ff;">await</span> SettingManager.GetSettingValueAsync&lt;<span style="color: #0000ff;">bool</span>&gt;<span style="color: #000000;">(
                AbpZeroSettingNames.UserManagement.IsEmailConfirmationRequiredForLogin);

            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> RegisterOutput()
            {
                CanLogin </span>= user.IsActive &amp;&amp; (user.IsEmailConfirmed || !<span style="color: #000000;">isEmailConfirmationRequiredForLogin)
            };
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">AccountAppService</span></div>
<p>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('d482c6b8-3b22-4d40-9ca8-a0c07dddccd6')"><img id="code_img_closed_d482c6b8-3b22-4d40-9ca8-a0c07dddccd6" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_d482c6b8-3b22-4d40-9ca8-a0c07dddccd6" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('d482c6b8-3b22-4d40-9ca8-a0c07dddccd6',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_d482c6b8-3b22-4d40-9ca8-a0c07dddccd6" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Runtime.Session;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Application.Configuration.Dto;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.Configuration;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.Application.Configuration
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> ConfigurationAppService : PMAppServiceBase, IConfigurationAppService
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span><span style="color: #000000;"> Task ChangeUiTheme(ChangeUiThemeInput input)
        {
            </span><span style="color: #0000ff;">await</span><span style="color: #000000;">
                SettingManager.ChangeSettingForUserAsync(AbpSession.ToUserIdentifier(), PMSettingNames.UiTheme,
                    input.Theme);
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">ConfigurationAppService</span></div>
<p>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('96ac499e-15fd-47fb-87f9-fc88f997ee05')"><img id="code_img_closed_96ac499e-15fd-47fb-87f9-fc88f997ee05" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_96ac499e-15fd-47fb-87f9-fc88f997ee05" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('96ac499e-15fd-47fb-87f9-fc88f997ee05',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_96ac499e-15fd-47fb-87f9-fc88f997ee05" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Application.Services;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Application.Services.Dto;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.AutoMapper;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Domain.Repositories;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Extensions;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.IdentityFramework;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.MultiTenancy;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Runtime.Security;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNet.Identity;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Application.MultiTenancy.Dto;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.Authorization.Roles;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.Editions;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.MultiTenant;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.Users;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.Application.MultiTenancy
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> TenantAppService :  AsyncCrudAppService&lt;Tenant, TenantDto, <span style="color: #0000ff;">int</span>, PagedResultRequestDto, CreateTenantDto, TenantDto&gt;<span style="color: #000000;">, ITenantAppService
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> TenantManager _tenantManager;
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> EditionManager _editionManager;
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> UserManager _userManager;
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> RoleManager _roleManager;
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> IAbpZeroDbMigrator _abpZeroDbMigrator;

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> TenantAppService(
            IRepository</span>&lt;Tenant, <span style="color: #0000ff;">int</span>&gt;<span style="color: #000000;"> repository,
            TenantManager tenantManager,
            EditionManager editionManager,
            UserManager userManager,
            RoleManager roleManager,
            IAbpZeroDbMigrator abpZeroDbMigrator
            ) : </span><span style="color: #0000ff;">base</span><span style="color: #000000;">(repository)
        {
            _editionManager </span>=<span style="color: #000000;"> editionManager;
            _tenantManager </span>=<span style="color: #000000;"> tenantManager;
            _userManager </span>=<span style="color: #000000;"> userManager;
            _roleManager </span>=<span style="color: #000000;"> roleManager;
            _abpZeroDbMigrator </span>=<span style="color: #000000;"> abpZeroDbMigrator;
        }

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> CheckError(IdentityResult identityResult)
        {
            identityResult.CheckErrors();
        }

        </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
        <span style="color: #808080;">///</span><span style="color: #008000;"> 创建租户
        </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
        <span style="color: #808080;">///</span> <span style="color: #808080;">&lt;param name="input"&gt;&lt;/param&gt;</span>
        <span style="color: #808080;">///</span> <span style="color: #808080;">&lt;returns&gt;&lt;/returns&gt;</span>
        <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">async</span> Task&lt;TenantDto&gt;<span style="color: #000000;"> Create(CreateTenantDto input)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">判断是否已拥有此接口的权限（Create方法），需要赋值CreatePermissionName属性</span>
<span style="color: #000000;">            CheckCreatePermission();

            </span><span style="color: #0000ff;">var</span> tenant = input.MapTo&lt;Tenant&gt;<span style="color: #000000;">();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">加密数据库链接字符串（采用AES对称加密）</span>
            tenant.ConnectionString =<span style="color: #000000;"> input.ConnectionString.IsNullOrEmpty()
                </span>? <span style="color: #0000ff;">null</span><span style="color: #000000;">
                : SimpleStringCipher.Instance.Encrypt(input.ConnectionString);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">当前租户使用的版本（Standard标准版）</span>
            <span style="color: #0000ff;">var</span> defaultEdition = <span style="color: #0000ff;">await</span><span style="color: #000000;"> _editionManager.FindByNameAsync(EditionManager.DefaultEditionName);
            </span><span style="color: #0000ff;">if</span> (defaultEdition != <span style="color: #0000ff;">null</span><span style="color: #000000;">)
            {
                tenant.EditionId </span>=<span style="color: #000000;"> defaultEdition.Id;
            }

            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建租户</span>
            <span style="color: #0000ff;">await</span><span style="color: #000000;"> _tenantManager.CreateAsync(tenant);
            </span><span style="color: #008000;">//</span><span style="color: #008000;">获得租户的id</span>
            <span style="color: #0000ff;">await</span><span style="color: #000000;"> CurrentUnitOfWork.SaveChangesAsync();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">创建租户数据库</span>
<span style="color: #000000;">            _abpZeroDbMigrator.CreateOrMigrateForTenant(tenant);

            </span><span style="color: #0000ff;">using</span><span style="color: #000000;"> (CurrentUnitOfWork.SetTenantId(tenant.Id))
            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;">创建静态租户角色，该静态角色通过IRoleManagementConfig配置</span>
                CheckError(<span style="color: #0000ff;">await</span><span style="color: #000000;"> _roleManager.CreateStaticRoles(tenant.Id));
                </span><span style="color: #0000ff;">await</span> CurrentUnitOfWork.SaveChangesAsync();<span style="color: #008000;">//</span><span style="color: #008000;">获取静态角色id

                </span><span style="color: #008000;">//</span><span style="color: #008000;">授予管理员角色所有权限（该权限通过IPermissionDefinitionContext配置）</span>
                <span style="color: #0000ff;">var</span> adminRole = _roleManager.Roles.Single(r =&gt; r.Name ==<span style="color: #000000;"> StaticRoleNames.Tenants.Admin);
                </span><span style="color: #0000ff;">await</span><span style="color: #000000;"> _roleManager.GrantAllPermissionsAsync(adminRole);

                </span><span style="color: #008000;">//</span><span style="color: #008000;">创建租户admin用户</span>
                <span style="color: #0000ff;">var</span> adminUser=<span style="color: #000000;"> User.CreateTenantAdminUser(tenant.Id, input.AdminEmailAddress, User.DefaultPassword);
                CheckError(</span><span style="color: #0000ff;">await</span><span style="color: #000000;"> _userManager.CreateAsync(adminUser));
                </span><span style="color: #0000ff;">await</span> CurrentUnitOfWork.SaveChangesAsync();<span style="color: #008000;">//</span><span style="color: #008000;">获取用户id

                </span><span style="color: #008000;">//</span><span style="color: #008000;">讲角色分配给租户admin用户</span>
                CheckError(<span style="color: #0000ff;">await</span><span style="color: #000000;"> _userManager.AddToRoleAsync(adminUser.Id, adminRole.Name));
                </span><span style="color: #0000ff;">await</span><span style="color: #000000;"> CurrentUnitOfWork.SaveChangesAsync();
            }

            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> MapToEntityDto(tenant);
        }

        </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> MapToEntity(TenantDto updateInput, Tenant entity)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">手动映射，因为TenantDto也包含不可编辑的属性。</span>
            entity.Name =<span style="color: #000000;"> updateInput.Name;
            entity.TenancyName </span>=<span style="color: #000000;"> updateInput.TenancyName;
            entity.IsActive </span>=<span style="color: #000000;"> updateInput.IsActive;
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">async</span> Task Delete(EntityDto&lt;<span style="color: #0000ff;">int</span>&gt;<span style="color: #000000;"> input)
        {
            CheckDeletePermission();
            </span><span style="color: #0000ff;">var</span> tenant =<span style="color: #0000ff;">await</span><span style="color: #000000;"> _tenantManager.FindByIdAsync(input.Id);
            </span><span style="color: #0000ff;">await</span><span style="color: #000000;"> _tenantManager.DeleteAsync(tenant);
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">TenantAppService</span></div>
<p>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('1bcd61f1-9115-464d-a611-48befcb97351')"><img id="code_img_closed_1bcd61f1-9115-464d-a611-48befcb97351" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_1bcd61f1-9115-464d-a611-48befcb97351" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('1bcd61f1-9115-464d-a611-48befcb97351',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_1bcd61f1-9115-464d-a611-48befcb97351" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Application.Services;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Application.Services.Dto;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Authorization.Users;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.AutoMapper;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Domain.Repositories;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.IdentityFramework;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.UI;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNet.Identity;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Application.Roles.Dto;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.Authorization.Roles;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.MultiTenant;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.Users;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.Application.Roles
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> RoleAppService:AsyncCrudAppService&lt;Role,RoleDto,Int32,PagedResultRequestDto,CreateRoleDto,RoleDto&gt;<span style="color: #000000;">,IRoleAppService
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> RoleManager _roleManager;
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> UserManager _userManager;
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span> IRepository&lt;User, <span style="color: #0000ff;">long</span>&gt;<span style="color: #000000;"> _userRepository;
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span> IRepository&lt;UserRole, <span style="color: #0000ff;">long</span>&gt;<span style="color: #000000;"> _userRoleRepository;
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span> IRepository&lt;Role&gt;<span style="color: #000000;"> _roleRepository; 
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> RoleAppService(
            IRepository</span>&lt;Role, <span style="color: #0000ff;">int</span>&gt;<span style="color: #000000;"> repository,
            RoleManager roleManager,
            UserManager userManager,
            IRepository</span>&lt;User,<span style="color: #0000ff;">long</span>&gt;<span style="color: #000000;"> userRepository,
            IRepository</span>&lt;UserRole,<span style="color: #0000ff;">long</span>&gt;<span style="color: #000000;"> userRoleRepository,
            IRepository</span>&lt;Role&gt;<span style="color: #000000;"> roleRepository    
            ) : </span><span style="color: #0000ff;">base</span><span style="color: #000000;">(repository)
        {
            _roleManager </span>=<span style="color: #000000;"> roleManager;
            _userManager </span>=<span style="color: #000000;"> userManager;
            _userRepository </span>=<span style="color: #000000;"> userRepository;
            _userRoleRepository </span>=<span style="color: #000000;"> userRoleRepository;
            _roleRepository </span>=<span style="color: #000000;"> roleRepository;
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">async</span> Task&lt;RoleDto&gt;<span style="color: #000000;"> Create(CreateRoleDto input)
        {
            CheckCreatePermission();

            </span><span style="color: #0000ff;">var</span> role = input.MapTo&lt;Role&gt;<span style="color: #000000;">();

            CheckErrors(</span><span style="color: #0000ff;">await</span><span style="color: #000000;"> _roleManager.CreateAsync(role));

            </span><span style="color: #008000;">//</span><span style="color: #008000;">查询权限</span>
            <span style="color: #0000ff;">var</span> grantedPermissions =<span style="color: #000000;">
                PermissionManager.GetAllPermissions().Where(p </span>=&gt;<span style="color: #000000;"> input.Permissions.Contains(p.Name)).ToList();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">给角色设置权限</span>
            <span style="color: #0000ff;">await</span><span style="color: #000000;"> _roleManager.SetGrantedPermissionsAsync(role, grantedPermissions);

            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> MapToEntityDto(role);
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">async</span> Task Delete(EntityDto&lt;<span style="color: #0000ff;">int</span>&gt;<span style="color: #000000;"> input)
        {
            CheckDeletePermission();

            </span><span style="color: #0000ff;">var</span> role = <span style="color: #0000ff;">await</span><span style="color: #000000;"> _roleManager.FindByIdAsync(input.Id);
            </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (role.IsStatic)
            {
                </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> UserFriendlyException(<span style="color: #800000;">"</span><span style="color: #800000;">无法删除静态角色</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }

            </span><span style="color: #008000;">//</span><span style="color: #008000;">删除用户角色关联</span>
            <span style="color: #0000ff;">var</span> users = <span style="color: #0000ff;">await</span><span style="color: #000000;"> GetUsersInRoleAsync(role.Name);

            </span><span style="color: #0000ff;">foreach</span> (<span style="color: #0000ff;">var</span> user <span style="color: #0000ff;">in</span><span style="color: #000000;"> users)
            {
                CheckErrors(</span><span style="color: #0000ff;">await</span><span style="color: #000000;"> _userManager.RemoveFromRoleAsync(user, role.Name));
            }

            </span><span style="color: #008000;">//</span><span style="color: #008000;">删除角色</span>
            <span style="color: #0000ff;">await</span><span style="color: #000000;"> _roleManager.DeleteAsync(role);
        }


        </span><span style="color: #0000ff;">private</span> Task&lt;List&lt;<span style="color: #0000ff;">long</span>&gt;&gt; GetUsersInRoleAsync(<span style="color: #0000ff;">string</span><span style="color: #000000;"> roleName)
        {
           </span><span style="color: #0000ff;">var</span> users= (<span style="color: #0000ff;">from</span> user <span style="color: #0000ff;">in</span><span style="color: #000000;"> _userRepository.GetAll()
                join userRole </span><span style="color: #0000ff;">in</span><span style="color: #000000;"> _userRoleRepository.GetAll() on user.Id equals userRole.UserId
                join role </span><span style="color: #0000ff;">in</span><span style="color: #000000;"> _roleRepository.GetAll() on userRole.RoleId equals role.Id
                </span><span style="color: #0000ff;">where</span> role.Name ==<span style="color: #000000;"> roleName
                </span><span style="color: #0000ff;">select</span><span style="color: #000000;"> user.Id).Distinct().ToList();
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> Task.FromResult(users);
        }


        </span><span style="color: #0000ff;">public</span> Task&lt;ListResultDto&lt;PermissionDto&gt;&gt;<span style="color: #000000;"> GetAllPermissions()
        {
            </span><span style="color: #0000ff;">var</span> permissions =<span style="color: #000000;"> PermissionManager.GetAllPermissions();
            </span><span style="color: #0000ff;">return</span> Task.FromResult(<span style="color: #0000ff;">new</span> ListResultDto&lt;PermissionDto&gt;(permissions.MapTo&lt;List&lt;PermissionDto&gt;&gt;<span style="color: #000000;">()));
        }

        </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span> Task&lt;Role&gt; GetEntityByIdAsync(<span style="color: #0000ff;">int</span><span style="color: #000000;"> id)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">查询角色，并包含该角色的权限</span>
            <span style="color: #0000ff;">var</span> role = Repository.GetAllIncluding(x =&gt; x.Permissions).FirstOrDefault(x =&gt; x.Id ==<span style="color: #000000;"> id);
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> Task.FromResult(role);
        }
        </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
        <span style="color: #808080;">///</span><span style="color: #008000;"> 创建过滤查询
        </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
        <span style="color: #808080;">///</span> <span style="color: #808080;">&lt;param name="input"&gt;&lt;/param&gt;</span>
        <span style="color: #808080;">///</span> <span style="color: #808080;">&lt;returns&gt;&lt;/returns&gt;</span>
        <span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span> IQueryable&lt;Role&gt;<span style="color: #000000;"> CreateFilteredQuery(PagedResultRequestDto input)
        {
            </span><span style="color: #0000ff;">return</span> Repository.GetAllIncluding(x =&gt;<span style="color: #000000;"> x.Permissions);
        }

        </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
        <span style="color: #808080;">///</span><span style="color: #008000;"> 应用排序
        </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
        <span style="color: #808080;">///</span> <span style="color: #808080;">&lt;param name="query"&gt;&lt;/param&gt;</span>
        <span style="color: #808080;">///</span> <span style="color: #808080;">&lt;param name="input"&gt;&lt;/param&gt;</span>
        <span style="color: #808080;">///</span> <span style="color: #808080;">&lt;returns&gt;&lt;/returns&gt;</span>
        <span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span> IQueryable&lt;Role&gt; ApplySorting(IQueryable&lt;Role&gt;<span style="color: #000000;"> query, PagedResultRequestDto input)
        {
            </span><span style="color: #0000ff;">return</span> query.OrderBy(r =&gt;<span style="color: #000000;"> r.DisplayName);
        }
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> CheckErrors(IdentityResult identityResult)
        {
            identityResult.CheckErrors(LocalizationManager);
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">RoleAppService</span></div>
<p>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('8d3261fe-fe64-4410-8910-d870b89dbe6f')"><img id="code_img_closed_8d3261fe-fe64-4410-8910-d870b89dbe6f" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_8d3261fe-fe64-4410-8910-d870b89dbe6f" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('8d3261fe-fe64-4410-8910-d870b89dbe6f',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_8d3261fe-fe64-4410-8910-d870b89dbe6f" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Auditing;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.AutoMapper;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Application.Sessions.Dto;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.Application.Sessions
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> SessionAppService:PMAppServiceBase,ISessionAppService
    {

        [DisableAuditing]
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task&lt;GetCurrentLoginInformationsOutput&gt;<span style="color: #000000;"> GetCurrentLoginInformations()
        {
            </span><span style="color: #0000ff;">var</span> output=<span style="color: #0000ff;">new</span><span style="color: #000000;"> GetCurrentLoginInformationsOutput();
            </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (AbpSession.UserId.HasValue)
            {
                output.User </span>= (<span style="color: #0000ff;">await</span> GetCurrentUserAsync()).MapTo&lt;UserLoginInfoDto&gt;<span style="color: #000000;">();
            }
            </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (AbpSession.TenantId.HasValue)
            {
                output.Tenant </span>= (<span style="color: #0000ff;">await</span> GetCurrentTenantAsync()).MapTo&lt;TenantLoginInfoDto&gt;<span style="color: #000000;">();
            }
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> output;
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">SessionAppService</span></div>
<p>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('c12d5b8b-c0a0-4c84-9e91-f2b75a7e0318')"><img id="code_img_closed_c12d5b8b-c0a0-4c84-9e91-f2b75a7e0318" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_c12d5b8b-c0a0-4c84-9e91-f2b75a7e0318" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('c12d5b8b-c0a0-4c84-9e91-f2b75a7e0318',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_c12d5b8b-c0a0-4c84-9e91-f2b75a7e0318" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.ObjectModel;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Application.Services;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Application.Services.Dto;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Authorization.Users;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.AutoMapper;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Domain.Repositories;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.IdentityFramework;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNet.Identity;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Application.Roles.Dto;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Application.Users.Dto;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.Authorization.Roles;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.Users;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.Application.Users
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> UserAppService:AsyncCrudAppService&lt;User,UserDto,<span style="color: #0000ff;">long</span>,PagedResultRequestDto,CreateUserDto,UpdateUserDto&gt;<span style="color: #000000;">,IUserAppService
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> UserManager _userManager;
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span> IRepository&lt;Role&gt;<span style="color: #000000;"> _roleRepository;
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> RoleManager _roleManager;

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> UserAppService(
            IRepository</span>&lt;User, <span style="color: #0000ff;">long</span>&gt;<span style="color: #000000;"> repository,
            UserManager userManager,
            IRepository</span>&lt;Role&gt;<span style="color: #000000;"> roleRepository,
            RoleManager roleManager 
            ) : </span><span style="color: #0000ff;">base</span><span style="color: #000000;">(repository)
        {
            _userManager </span>=<span style="color: #000000;"> userManager;
            _roleRepository </span>=<span style="color: #000000;"> roleRepository;
            _roleManager </span>=<span style="color: #000000;"> roleManager;
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">async</span> Task&lt;UserDto&gt; Get(EntityDto&lt;<span style="color: #0000ff;">long</span>&gt;<span style="color: #000000;"> input)
        {
            </span><span style="color: #0000ff;">var</span> user = <span style="color: #0000ff;">await</span> <span style="color: #0000ff;">base</span><span style="color: #000000;">.Get(input);
            </span><span style="color: #0000ff;">var</span> userRoles = <span style="color: #0000ff;">await</span><span style="color: #000000;"> _userManager.GetRolesAsync(user.Id);
            user.Roles </span>=<span style="color: #000000;"> userRoles.ToArray();
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> user;
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">async</span> Task&lt;UserDto&gt;<span style="color: #000000;"> Create(CreateUserDto input)
        {
            CheckCreatePermission();
            </span><span style="color: #0000ff;">var</span> user = input.MapTo&lt;User&gt;<span style="color: #000000;">();
            user.TenantId </span>=<span style="color: #000000;"> AbpSession.TenantId;
            user.Password </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> PasswordHasher().HashPassword(input.Password);
            user.IsEmailConfirmed </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">;

            </span><span style="color: #008000;">//</span><span style="color: #008000;">分配角色（从租户的所有）</span>
            user.Roles = <span style="color: #0000ff;">new</span> Collection&lt;UserRole&gt;<span style="color: #000000;">();
            </span><span style="color: #0000ff;">foreach</span> (<span style="color: #0000ff;">var</span> roleName <span style="color: #0000ff;">in</span><span style="color: #000000;"> input.RoleNames)
            {
                </span><span style="color: #0000ff;">var</span> role = <span style="color: #0000ff;">await</span><span style="color: #000000;"> _roleManager.GetRoleByNameAsync(roleName);
                user.Roles.Add(</span><span style="color: #0000ff;">new</span><span style="color: #000000;"> UserRole(AbpSession.TenantId, user.Id, role.Id));
            }
            CheckErrors(</span><span style="color: #0000ff;">await</span><span style="color: #000000;"> _userManager.CreateAsync(user));
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> MapToEntityDto(user);
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">async</span> Task&lt;UserDto&gt;<span style="color: #000000;"> Update(UpdateUserDto input)
        {
            CheckUpdatePermission();
            </span><span style="color: #0000ff;">var</span> user = <span style="color: #0000ff;">await</span><span style="color: #000000;"> _userManager.GetUserByIdAsync(input.Id);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">把有变动的属性赋值到user对象中</span>
<span style="color: #000000;">            MapToEntity(input, user);

            CheckErrors(</span><span style="color: #0000ff;">await</span><span style="color: #000000;"> _userManager.UpdateAsync(user));

            </span><span style="color: #0000ff;">if</span> (input.RoleNames != <span style="color: #0000ff;">null</span><span style="color: #000000;">)
            {
                </span><span style="color: #008000;">//</span><span style="color: #008000;">_userManager.SetRoles方法的作用：变更角色（前提：用户表以已经创建）</span>
                CheckErrors(<span style="color: #0000ff;">await</span><span style="color: #000000;"> _userManager.SetRoles(user, input.RoleNames));
            }

            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">await</span><span style="color: #000000;"> Get(input);
        }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">async</span> Task Delete(EntityDto&lt;<span style="color: #0000ff;">long</span>&gt;<span style="color: #000000;"> input)
        {
            </span><span style="color: #0000ff;">var</span> user = <span style="color: #0000ff;">await</span><span style="color: #000000;"> _userManager.GetUserByIdAsync(input.Id);

            </span><span style="color: #008000;">//</span><span style="color: #008000;">admin用户不能被删除（删除用户的同时会删除UserRole）</span>
            <span style="color: #0000ff;">await</span><span style="color: #000000;"> _userManager.DeleteAsync(user);
        }
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task&lt;ListResultDto&lt;RoleDto&gt;&gt;<span style="color: #000000;"> GetRoles()
        {
            </span><span style="color: #0000ff;">var</span> roles = <span style="color: #0000ff;">await</span><span style="color: #000000;"> _roleRepository.GetAllListAsync();
            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> ListResultDto&lt;RoleDto&gt;(roles.MapTo&lt;List&lt;RoleDto&gt;&gt;<span style="color: #000000;">());
        }

        </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span><span style="color: #000000;"> User MapToEntity(CreateUserDto createInput)
        {
            </span><span style="color: #0000ff;">var</span> user = ObjectMapper.Map&lt;User&gt;<span style="color: #000000;">(createInput);
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> user;
        }

        </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> MapToEntity(UpdateUserDto updateInput, User entity)
        {
            ObjectMapper.Map(updateInput, entity);
        }

        </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span> IQueryable&lt;User&gt;<span style="color: #000000;"> CreateFilteredQuery(PagedResultRequestDto input)
        {
            </span><span style="color: #0000ff;">return</span> Repository.GetAllIncluding(x =&gt;<span style="color: #000000;"> x.Roles);
        }

        </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">async</span> Task&lt;User&gt; GetEntityByIdAsync(<span style="color: #0000ff;">long</span><span style="color: #000000;"> id)
        {
            </span><span style="color: #0000ff;">var</span> user = Repository.GetAllIncluding(x =&gt; x.Roles).FirstOrDefault(x =&gt; x.Id ==<span style="color: #000000;"> id);
            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">await</span><span style="color: #000000;"> Task.FromResult(user);
        }
        </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span> IQueryable&lt;User&gt; ApplySorting(IQueryable&lt;User&gt;<span style="color: #000000;"> query, PagedResultRequestDto input)
        {
            </span><span style="color: #0000ff;">return</span> query.OrderBy(r =&gt;<span style="color: #000000;"> r.UserName);
        }

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> CheckErrors(IdentityResult identityResult)
        {
            identityResult.CheckErrors(LocalizationManager);
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">UserAppService</span></div>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a5"></a>五、PM.WebApi</span></strong></span></p>
<p><strong>1，NuGet安装：</strong></p>
<p><strong>Abp.Zero、Abp.Web.Api、Abp.AutoMapper、Microsoft.Owin.Security.OAuth、Microsoft.AspNet.WebApi.Owin</strong></p>
<p><strong>System.ComponentModel.DataAnnotations</strong></p>
<p><strong>2，WebApi</strong><strong>Module</strong></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Web.Http;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Application.Services;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Configuration.Startup;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Modules;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.WebApi;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> MyPassword.Api
{
    [DependsOn(</span><span style="color: #0000ff;">typeof</span>(AbpWebApiModule), <span style="color: #0000ff;">typeof</span><span style="color: #000000;">(MyPasswordApplicationModule))]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyPasswordWebApiModule : AbpModule
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> Initialize()
        {
            IocManager.RegisterAssemblyByConvention(Assembly.GetExecutingAssembly());

            Configuration.Modules.AbpWebApi().DynamicApiControllerBuilder
                .ForAll</span>&lt;IApplicationService&gt;(<span style="color: #0000ff;">typeof</span>(MyPasswordApplicationModule).Assembly, <span style="color: #800000;">"</span><span style="color: #800000;">app</span><span style="color: #800000;">"</span><span style="color: #000000;">)
                .Build();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">添加访问令牌类型（Access Token Types）过滤（不加这句话也支持Bearer）</span>
            Configuration.Modules.AbpWebApi().HttpConfiguration.Filters.Add(<span style="color: #0000ff;">new</span> HostAuthenticationFilter(<span style="color: #800000;">"</span><span style="color: #800000;">Bearer</span><span style="color: #800000;">"</span><span style="color: #000000;">));
        }
    }
}</span></pre>
</div>
<p>备注：访问令牌类型（Access Token Types）包括bearer类型或mac类型。</p>
<p>①bearer类型</p>
<p>[RFC6750]中定义的&ldquo;bearer&rdquo;令牌类型被简单地包含在请求中的访问令牌字符串中：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">     GET /resource/1 HTTP/1.1
     Host: example.com
     Authorization: Bearer mF_9.B5f-4.1JqM</span></pre>
</div>
<p>②mac类型</p>
<p>而[OAuth-HTTP-MAC]中定义的&ldquo;mac&rdquo;令牌类型是通过发送消息认证码（MAC）密钥与用于签署HTTP请求的某些组件的访问令牌一起使用的：</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">     GET /resource/1 HTTP/1.1
     Host: example.com
     Authorization: MAC id="h480djs93hd8",
                        nonce="274312:dj83hs9s",
                        mac="kDZvddkndxvhGRXZhvuDjEWhGeE="</span></pre>
</div>
<p><span style="font-size: 15px;"><strong>3，AccountController（获取访问令牌）</strong></span></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('72beacbe-2c5c-48ae-a775-627b8cbfffa2')"><img id="code_img_closed_72beacbe-2c5c-48ae-a775-627b8cbfffa2" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_72beacbe-2c5c-48ae-a775-627b8cbfffa2" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('72beacbe-2c5c-48ae-a775-627b8cbfffa2',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_72beacbe-2c5c-48ae-a775-627b8cbfffa2" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Web.Http;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Authorization;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Authorization.Users;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.UI;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Web.Models;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.WebApi.Controllers;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> MyPassword.Api.Models;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> MyPassword.Authorization;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> MyPassword.Authorization.Users;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> MyPassword.MultiTenancy;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> MyPassword.Users;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Owin.Infrastructure;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Owin.Security;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.Owin.Security.OAuth;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> MyPassword.Api.Controllers
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> AccountController : AbpApiController
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">static</span> OAuthBearerAuthenticationOptions OAuthBearerOptions { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">private</span> <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> LogInManager _logInManager;

        </span><span style="color: #0000ff;">static</span><span style="color: #000000;"> AccountController()
        {
            OAuthBearerOptions </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> OAuthBearerAuthenticationOptions();
        }

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> AccountController(LogInManager logInManager)
        {
            _logInManager </span>=<span style="color: #000000;"> logInManager;
            LocalizationSourceName </span>=<span style="color: #000000;"> MyPasswordConsts.LocalizationSourceName;
        }

        </span><span style="color: #008000;">//</span><span style="color: #008000;">获取访问令牌</span>
<span style="color: #000000;">        [HttpPost]
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">async</span> Task&lt;AjaxResponse&gt;<span style="color: #000000;"> Authenticate(LoginModel loginModel)
        {
            CheckModelState();

            </span><span style="color: #0000ff;">var</span> loginResult = <span style="color: #0000ff;">await</span><span style="color: #000000;"> GetLoginResultAsync(
                loginModel.UsernameOrEmailAddress,
                loginModel.Password,
                loginModel.TenancyName
                );

            </span><span style="color: #0000ff;">var</span> ticket = <span style="color: #0000ff;">new</span> AuthenticationTicket(loginResult.Identity, <span style="color: #0000ff;">new</span><span style="color: #000000;"> AuthenticationProperties());

            </span><span style="color: #0000ff;">var</span> currentUtc = <span style="color: #0000ff;">new</span><span style="color: #000000;"> SystemClock().UtcNow;
            ticket.Properties.IssuedUtc </span>=<span style="color: #000000;"> currentUtc;
            ticket.Properties.ExpiresUtc </span>= currentUtc.Add(TimeSpan.FromMinutes(<span style="color: #800080;">30</span><span style="color: #000000;">));

            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> AjaxResponse(OAuthBearerOptions.AccessTokenFormat.Protect(ticket));
        }

        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">async</span> Task&lt;AbpLoginResult&lt;Tenant, User&gt;&gt; GetLoginResultAsync(<span style="color: #0000ff;">string</span> usernameOrEmailAddress, <span style="color: #0000ff;">string</span> password, <span style="color: #0000ff;">string</span><span style="color: #000000;"> tenancyName)
        {
            </span><span style="color: #0000ff;">var</span> loginResult = <span style="color: #0000ff;">await</span><span style="color: #000000;"> _logInManager.LoginAsync(usernameOrEmailAddress, password, tenancyName);

            </span><span style="color: #0000ff;">switch</span><span style="color: #000000;"> (loginResult.Result)
            {
                </span><span style="color: #0000ff;">case</span><span style="color: #000000;"> AbpLoginResultType.Success:
                    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> loginResult;
                </span><span style="color: #0000ff;">default</span><span style="color: #000000;">:
                    </span><span style="color: #0000ff;">throw</span><span style="color: #000000;"> CreateExceptionForFailedLoginAttempt(loginResult.Result, usernameOrEmailAddress, tenancyName);
            }
        }

        </span><span style="color: #0000ff;">private</span> Exception CreateExceptionForFailedLoginAttempt(AbpLoginResultType result, <span style="color: #0000ff;">string</span> usernameOrEmailAddress, <span style="color: #0000ff;">string</span><span style="color: #000000;"> tenancyName)
        {
            </span><span style="color: #0000ff;">switch</span><span style="color: #000000;"> (result)
            {
                </span><span style="color: #0000ff;">case</span><span style="color: #000000;"> AbpLoginResultType.Success:
                    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> ApplicationException(<span style="color: #800000;">"</span><span style="color: #800000;">Don't call this method with a success result!</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                </span><span style="color: #0000ff;">case</span><span style="color: #000000;"> AbpLoginResultType.InvalidUserNameOrEmailAddress:
                </span><span style="color: #0000ff;">case</span><span style="color: #000000;"> AbpLoginResultType.InvalidPassword:
                    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> UserFriendlyException(L(<span style="color: #800000;">"</span><span style="color: #800000;">LoginFailed</span><span style="color: #800000;">"</span>), L(<span style="color: #800000;">"</span><span style="color: #800000;">InvalidUserNameOrPassword</span><span style="color: #800000;">"</span><span style="color: #000000;">));
                </span><span style="color: #0000ff;">case</span><span style="color: #000000;"> AbpLoginResultType.InvalidTenancyName:
                    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> UserFriendlyException(L(<span style="color: #800000;">"</span><span style="color: #800000;">LoginFailed</span><span style="color: #800000;">"</span>), L(<span style="color: #800000;">"</span><span style="color: #800000;">ThereIsNoTenantDefinedWithName{0}</span><span style="color: #800000;">"</span><span style="color: #000000;">, tenancyName));
                </span><span style="color: #0000ff;">case</span><span style="color: #000000;"> AbpLoginResultType.TenantIsNotActive:
                    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> UserFriendlyException(L(<span style="color: #800000;">"</span><span style="color: #800000;">LoginFailed</span><span style="color: #800000;">"</span>), L(<span style="color: #800000;">"</span><span style="color: #800000;">TenantIsNotActive</span><span style="color: #800000;">"</span><span style="color: #000000;">, tenancyName));
                </span><span style="color: #0000ff;">case</span><span style="color: #000000;"> AbpLoginResultType.UserIsNotActive:
                    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> UserFriendlyException(L(<span style="color: #800000;">"</span><span style="color: #800000;">LoginFailed</span><span style="color: #800000;">"</span>), L(<span style="color: #800000;">"</span><span style="color: #800000;">UserIsNotActiveAndCanNotLogin</span><span style="color: #800000;">"</span><span style="color: #000000;">, usernameOrEmailAddress));
                </span><span style="color: #0000ff;">case</span><span style="color: #000000;"> AbpLoginResultType.UserEmailIsNotConfirmed:
                    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> UserFriendlyException(L(<span style="color: #800000;">"</span><span style="color: #800000;">LoginFailed</span><span style="color: #800000;">"</span>), <span style="color: #800000;">"</span><span style="color: #800000;">Your email address is not confirmed. You can not login</span><span style="color: #800000;">"</span>); <span style="color: #008000;">//</span><span style="color: #008000;">TODO: localize message</span>
                <span style="color: #0000ff;">default</span>: <span style="color: #008000;">//</span><span style="color: #008000;">Can not fall to default actually. But other result types can be added in the future and we may forget to handle it</span>
                    Logger.Warn(<span style="color: #800000;">"</span><span style="color: #800000;">Unhandled login fail reason: </span><span style="color: #800000;">"</span> +<span style="color: #000000;"> result);
                    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> UserFriendlyException(L(<span style="color: #800000;">"</span><span style="color: #800000;">LoginFailed</span><span style="color: #800000;">"</span><span style="color: #000000;">));
            }
        }

        </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">virtual</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> CheckModelState()
        {
            </span><span style="color: #0000ff;">if</span> (!<span style="color: #000000;">ModelState.IsValid)
            {
                </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> UserFriendlyException(<span style="color: #800000;">"</span><span style="color: #800000;">Invalid request!</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">AccountController</span></div>
<p>&nbsp;</p>
<p><strong>4，Web工程下的Startup.cs</strong></p>
<div class="cnblogs_code">
<pre>app.UseOAuthBearerAuthentication(AccountController.OAuthBearerOptions);</pre>
</div>
<p>将Bearer Token处理添加到OWIN应用程序管道。<br />这个中间件理解适当的格式化和安全的令牌出现在请求头。 <br />如果Options.AuthenticationMode处于Active状态，则不记名令牌（bearer token）中的声明将被添加到当前请求的IPrincipal用户。 <br />如果Options.AuthenticationMode是Passive的，那么当前请求不被修改，但IAuthenticationManager AuthenticateAsync可以随时用来从请求的不记名令牌（bearer token）中获得请求。 <br />另见<a href="http://tools.ietf.org/html/rfc6749" target="_blank">http://tools.ietf.org/html/rfc6749</a></p>
<p>&nbsp;</p>
<p><strong>5，案例</strong></p>
<p>请求授权接口</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201712/741594-20171204220042519-661036403.png" alt="" /></p>
<p>返回令牌</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201712/741594-20171204220104628-714353891.png" alt="" /></p>
<p>&nbsp;</p>
<p>请求受保护的资源</p>
<p><img src="http://images2017.cnblogs.com/blog/741594/201712/741594-20171204220126284-318730314.png" alt="" /></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><span style="color: #ffffff;"><strong><span style="font-size: 18pt;"><a name="a6"></a>六、PM.Web（MPA）</span></strong></span></p>
<p><strong>1，NuGet安装：Abp.Zero、Abp.EntityFramework、Abp.Zero.EntityFramework、Abp.Web.Api、Abp.Web.Mvc、Abp.AutoMapper、Abp.Castle.Log4Net、Abp.Owin</strong></p>
<p><strong>可选则安装：Abp.Web.SignalR</strong></p>
<p>注意，先安装<strong>Abp.EntityFramework</strong>再安装<strong>Abp.Zero.EntityFramework</strong></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>针对通用的依赖类型的解析与创建，微软默认定义了4种类别的生命周期，分别如下：</p>
<table style="height: 115px; width: 873px;" border="1">
<thead>
<tr class="header"><th>类型</th><th>描述</th></tr>


</thead>
<tbody>
<tr class="odd">
<td>Instance</td>
<td>任何时间都只能使用特定的实例对象，开发人员需要负责该对象的初始化工作。</td>


</tr>
<tr class="even">
<td>Transient</td>
<td>每次都重新创建一个实例。</td>


</tr>
<tr class="odd">
<td>Singleton</td>
<td>创建一个单例，以后每次调用的时候都返回该单例对象。</td>


</tr>
<tr class="even">
<td>Scoped</td>
<td>在当前作用域内，不管调用多少次，都是一个实例，换了作用域就会再次创建实例，类似于特定作用内的单例。</td>


</tr>


</tbody>


</table>
<p>&nbsp;</p>
<p>前端笔记</p>
<p>1，按钮</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">button </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="button"</span><span style="color: #ff0000;"> class</span><span style="color: #0000ff;">="btn btn-primary btn-circle waves-effect waves-circle waves-float"</span><span style="color: #ff0000;">  data-toggle</span><span style="color: #0000ff;">="modal"</span><span style="color: #0000ff;">&gt;&lt;</span><span style="color: #800000;">i </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="material-icons"</span><span style="color: #0000ff;">&gt;</span>add<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">i</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">button</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p><img src="http://images2017.cnblogs.com/blog/741594/201711/741594-20171109105357075-1410317680.png" alt="" /></p>
<p>btn-circle：圆形按钮</p>
<p>pull-right：右浮动</p>
<p>waves-effect：点击按钮波浪效果</p>
<p>waves-block：块状效果</p>
<p>waves-circle：圆状效果</p>
<p>waves-float：效果浮动</p>
<p>2， 模态框</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">a </span><span style="color: #ff0000;">href</span><span style="color: #0000ff;">="#"</span><span style="color: #ff0000;"> class</span><span style="color: #0000ff;">="waves-effect waves-block edit-role"</span><span style="color: #ff0000;"> data-role-id</span><span style="color: #0000ff;">="@role.Id"</span><span style="color: #ff0000;"> data-toggle</span><span style="color: #0000ff;">="modal"</span><span style="color: #ff0000;"> data-target</span><span style="color: #0000ff;">="#RoleEditModal"</span><span style="color: #0000ff;">&gt;&lt;</span><span style="color: #800000;">i </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="material-icons"</span><span style="color: #0000ff;">&gt;</span>edit<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">i</span><span style="color: #0000ff;">&gt;</span>@L("Edit")<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">a</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="modal fade"</span><span style="color: #ff0000;"> id</span><span style="color: #0000ff;">="RoleEditModal"</span><span style="color: #ff0000;"> tabindex</span><span style="color: #0000ff;">="-1"</span><span style="color: #ff0000;"> role</span><span style="color: #0000ff;">="dialog"</span><span style="color: #ff0000;"> aria-labelledby</span><span style="color: #0000ff;">="RoleEditModalLabel"</span><span style="color: #ff0000;"> data-backdrop</span><span style="color: #0000ff;">="static"</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="modal-dialog"</span><span style="color: #ff0000;"> role</span><span style="color: #0000ff;">="document"</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="modal-content"</span><span style="color: #0000ff;">&gt;</span>

        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<div class="cnblogs_code" onclick="cnblogs_code_show('cb4fa3fb-a115-47f2-836a-f7891f684e07')"><img id="code_img_closed_cb4fa3fb-a115-47f2-836a-f7891f684e07" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_cb4fa3fb-a115-47f2-836a-f7891f684e07" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('cb4fa3fb-a115-47f2-836a-f7891f684e07',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_cb4fa3fb-a115-47f2-836a-f7891f684e07" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="modal fade"</span><span style="color: #ff0000;"> id</span><span style="color: #0000ff;">="RoleCreateModal"</span><span style="color: #ff0000;"> tabindex</span><span style="color: #0000ff;">="-1"</span><span style="color: #ff0000;"> role</span><span style="color: #0000ff;">="dialog"</span><span style="color: #ff0000;"> aria-labelledby</span><span style="color: #0000ff;">="RoleCreateModalLabel"</span><span style="color: #ff0000;"> data-backdrop</span><span style="color: #0000ff;">="static"</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="modal-dialog"</span><span style="color: #ff0000;"> role</span><span style="color: #0000ff;">="document"</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="modal-content"</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="modal-header"</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">h4 </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="modal-title"</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">span</span><span style="color: #0000ff;">&gt;</span>@L("CreateNewRole")<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">span</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">h4</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="modal-body"</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">form </span><span style="color: #ff0000;">name</span><span style="color: #0000ff;">="roleCreateForm"</span><span style="color: #ff0000;"> role</span><span style="color: #0000ff;">="form"</span><span style="color: #ff0000;"> novalidate class</span><span style="color: #0000ff;">="form-validation"</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="row clearfix"</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="col-sm-12"</span><span style="color: #0000ff;">&gt;</span>
                            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="form-group form-float"</span><span style="color: #0000ff;">&gt;</span>
                                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="form-line"</span><span style="color: #0000ff;">&gt;</span>
                                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">id</span><span style="color: #0000ff;">="rolename"</span><span style="color: #ff0000;"> type</span><span style="color: #0000ff;">="text"</span><span style="color: #ff0000;"> name</span><span style="color: #0000ff;">="Name"</span><span style="color: #ff0000;"> required maxlength</span><span style="color: #0000ff;">="32"</span><span style="color: #ff0000;"> minlength</span><span style="color: #0000ff;">="2"</span><span style="color: #ff0000;"> class</span><span style="color: #0000ff;">="validate form-control"</span><span style="color: #0000ff;">&gt;</span>
                                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">label </span><span style="color: #ff0000;">for</span><span style="color: #0000ff;">="rolename"</span><span style="color: #ff0000;"> class</span><span style="color: #0000ff;">="form-label"</span><span style="color: #0000ff;">&gt;</span>@L("RoleName")<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">label</span><span style="color: #0000ff;">&gt;</span>
                                <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
                            <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>

                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="row clearfix"</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="col-sm-12"</span><span style="color: #0000ff;">&gt;</span>
                            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="form-group form-float"</span><span style="color: #0000ff;">&gt;</span>
                                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="form-line"</span><span style="color: #0000ff;">&gt;</span>
                                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">id</span><span style="color: #0000ff;">="displayname"</span><span style="color: #ff0000;"> type</span><span style="color: #0000ff;">="text"</span><span style="color: #ff0000;"> name</span><span style="color: #0000ff;">="DisplayName"</span><span style="color: #ff0000;"> required maxlength</span><span style="color: #0000ff;">="32"</span><span style="color: #ff0000;"> minlength</span><span style="color: #0000ff;">="2"</span><span style="color: #ff0000;"> class</span><span style="color: #0000ff;">="validate form-control"</span><span style="color: #0000ff;">&gt;</span>
                                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">label </span><span style="color: #ff0000;">for</span><span style="color: #0000ff;">="displayname"</span><span style="color: #ff0000;"> class</span><span style="color: #0000ff;">="form-label"</span><span style="color: #0000ff;">&gt;</span>@L("DisplayName")<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">label</span><span style="color: #0000ff;">&gt;</span>
                                <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
                            <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>

                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="row"</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="col-sm-12"</span><span style="color: #0000ff;">&gt;</span>
                            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="form-group form-float"</span><span style="color: #0000ff;">&gt;</span>
                                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="form-line"</span><span style="color: #0000ff;">&gt;</span>
                                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">textarea </span><span style="color: #ff0000;">id</span><span style="color: #0000ff;">="role-description"</span><span style="color: #ff0000;"> name</span><span style="color: #0000ff;">="Description"</span><span style="color: #ff0000;"> class</span><span style="color: #0000ff;">="validate form-control"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">textarea</span><span style="color: #0000ff;">&gt;</span>
                                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">label </span><span style="color: #ff0000;">for</span><span style="color: #0000ff;">="role-description"</span><span style="color: #ff0000;"> class</span><span style="color: #0000ff;">="form-label"</span><span style="color: #0000ff;">&gt;</span>Role Description<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">label</span><span style="color: #0000ff;">&gt;</span>
                                <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
                            <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>

                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="row clearfix"</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="col-sm-12"</span><span style="color: #0000ff;">&gt;</span>
                            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">h4</span><span style="color: #0000ff;">&gt;</span>Permissions<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">h4</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">
                            @foreach (var permission in Model.Permissions)
                            {
                                </span><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="col-sm-6"</span><span style="color: #0000ff;">&gt;</span>
                                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="checkbox"</span><span style="color: #ff0000;"> name</span><span style="color: #0000ff;">="permission"</span><span style="color: #ff0000;"> value</span><span style="color: #0000ff;">="@permission.Name"</span><span style="color: #ff0000;"> class</span><span style="color: #0000ff;">="filled-in"</span><span style="color: #ff0000;"> id</span><span style="color: #0000ff;">="@string.Format("</span><span style="color: #ff0000;">permission{0}",permission.Name)" checked</span><span style="color: #0000ff;">="checked"</span> <span style="color: #0000ff;">/&gt;</span>
                                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">label </span><span style="color: #ff0000;">for</span><span style="color: #0000ff;">="@string.Format("</span><span style="color: #ff0000;">permission{0}",permission.Name)"</span><span style="color: #0000ff;">&gt;</span>@permission.DisplayName<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">label</span><span style="color: #0000ff;">&gt;</span>
                                <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">
                            }
                        </span><span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="modal-footer"</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">button </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="button"</span><span style="color: #ff0000;"> class</span><span style="color: #0000ff;">="btn btn-default waves-effect"</span><span style="color: #ff0000;"> data-dismiss</span><span style="color: #0000ff;">="modal"</span><span style="color: #0000ff;">&gt;</span>@L("Cancel")<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">button</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">button </span><span style="color: #ff0000;">type</span><span style="color: #0000ff;">="submit"</span><span style="color: #ff0000;"> class</span><span style="color: #0000ff;">="btn btn-primary waves-effect"</span><span style="color: #0000ff;">&gt;</span>@L("Save")<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">button</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">form</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<span class="cnblogs_code_collapse">View Code</span></div>
<p>3，for属性</p>
<p>在用户注册的时候，常常用户点击文字就需要将光标聚焦到对应的表单上面，这个是怎么实现的呢？就是下面我要介绍的&lt;label&gt;标签的for属性</p>
<p>定义：for 属性规定 label 与哪个表单元素绑定</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">　　　　　　　　　　　　　　　　　　&lt;</span><span style="color: #800000;">div </span><span style="color: #ff0000;">class</span><span style="color: #0000ff;">="form-line"</span><span style="color: #0000ff;">&gt;</span>
                                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">input </span><span style="color: #ff0000;">id</span><span style="color: #0000ff;">="rolename"</span><span style="color: #ff0000;"> type</span><span style="color: #0000ff;">="text"</span><span style="color: #ff0000;"> name</span><span style="color: #0000ff;">="Name"</span><span style="color: #ff0000;"> required maxlength</span><span style="color: #0000ff;">="32"</span><span style="color: #ff0000;"> minlength</span><span style="color: #0000ff;">="2"</span><span style="color: #ff0000;"> class</span><span style="color: #0000ff;">="validate form-control"</span><span style="color: #0000ff;">&gt;</span>
                                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">label </span><span style="color: #ff0000;">for</span><span style="color: #0000ff;">="rolename"</span><span style="color: #ff0000;"> class</span><span style="color: #0000ff;">="form-label"</span><span style="color: #0000ff;">&gt;</span>@L("RoleName")<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">label</span><span style="color: #0000ff;">&gt;</span>
                                <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">div</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a7"></a>七、PM.Web（SPA）</span></strong></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p style="background-color: #169fe6;"><strong><span style="font-size: 18pt; color: #ffffff;"><a name="a8"></a>八、单元测试</span></strong></p>
<p><strong>1，NuGet安装：</strong></p>
<p><span style="font-size: 12px;"><strong>Abp.TestBase、</strong></span><span style="font-size: 12px;"><strong><strong>Abp.EntityFramework、</strong></strong></span><span style="font-size: 12px;"><strong>Effort.EF6、</strong></span><span style="font-size: 12px;"><strong>xunit、</strong></span><span style="font-size: 12px;"><strong><strong>Shouldly、</strong></strong></span><span style="font-size: 12px;"><strong><strong><strong>xunit.runner.visualstudio、</strong></strong></strong></span><span style="font-size: 12px;"><strong><strong><strong>Abp.Zero.EntityFramework、<strong>NSubstitute</strong></strong></strong></strong></span></p>
<p><strong>2，基本结构</strong></p>
<div class="cnblogs_code" onclick="cnblogs_code_show('3abd4893-c19a-42d9-bcc2-2f122d85b82e')"><img id="code_img_closed_3abd4893-c19a-42d9-bcc2-2f122d85b82e" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_3abd4893-c19a-42d9-bcc2-2f122d85b82e" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('3abd4893-c19a-42d9-bcc2-2f122d85b82e',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_3abd4893-c19a-42d9-bcc2-2f122d85b82e" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Data.Common;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Data.Entity;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Configuration.Startup;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Domain.Uow;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Runtime.Session;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.TestBase;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Castle.MicroKernel.Registration;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Effort;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> EntityFramework.DynamicFilters;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.MultiTenant;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Core.Users;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.EntityFramework.EntityFramework;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.EntityFramework.Migrations.SeedData;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.Test
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> PMTestBase: AbpIntegratedTestBase&lt;PMTestModule&gt;<span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> DbConnection _hostDb;
        </span><span style="color: #0000ff;">private</span> Dictionary&lt;<span style="color: #0000ff;">int</span>, DbConnection&gt; _tenantDbs; <span style="color: #008000;">//</span><span style="color: #008000;">only used for db per tenant architecture</span>

        <span style="color: #0000ff;">protected</span><span style="color: #000000;"> PMTestBase()
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">Seed initial data for host</span>
            AbpSession.TenantId = <span style="color: #0000ff;">null</span><span style="color: #000000;">;
            UsingDbContext(context </span>=&gt;<span style="color: #000000;">
            {
                </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> InitialHostDbBuilder(context).Create();
                </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> DefaultTenantCreator(context).Create();
            });

            </span><span style="color: #008000;">//</span><span style="color: #008000;">Seed initial data for default tenant</span>
            AbpSession.TenantId = <span style="color: #800080;">1</span><span style="color: #000000;">;
            UsingDbContext(context </span>=&gt;<span style="color: #000000;">
            {
                </span><span style="color: #0000ff;">new</span> TenantRoleAndUserBuilder(context, <span style="color: #800080;">1</span><span style="color: #000000;">).Create();
            });

            LoginAsDefaultTenantAdmin();
        }

        </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> PreInitialize()
        {
            </span><span style="color: #0000ff;">base</span><span style="color: #000000;">.PreInitialize();

            </span><span style="color: #008000;">/*</span><span style="color: #008000;"> You can switch database architecture here: </span><span style="color: #008000;">*/</span><span style="color: #000000;">
            UseSingleDatabase();
            </span><span style="color: #008000;">//</span><span style="color: #008000;">UseDatabasePerTenant();</span>
<span style="color: #000000;">        }

        </span><span style="color: #008000;">/*</span><span style="color: #008000;"> Uses single database for host and all tenants.
         </span><span style="color: #008000;">*/</span>
        <span style="color: #0000ff;">private</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> UseSingleDatabase()
        {
            _hostDb </span>=<span style="color: #000000;"> DbConnectionFactory.CreateTransient();

            LocalIocManager.IocContainer.Register(
                Component.For</span>&lt;DbConnection&gt;<span style="color: #000000;">()
                    .UsingFactoryMethod(() </span>=&gt;<span style="color: #000000;"> _hostDb)
                    .LifestyleSingleton()
                );
        }

        </span><span style="color: #008000;">/*</span><span style="color: #008000;"> Uses single database for host and Default tenant,
         * but dedicated databases for all other tenants.
         </span><span style="color: #008000;">*/</span>
        <span style="color: #0000ff;">private</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> UseDatabasePerTenant()
        {
            _hostDb </span>=<span style="color: #000000;"> DbConnectionFactory.CreateTransient();
            _tenantDbs </span>= <span style="color: #0000ff;">new</span> Dictionary&lt;<span style="color: #0000ff;">int</span>, DbConnection&gt;<span style="color: #000000;">();

            LocalIocManager.IocContainer.Register(
                Component.For</span>&lt;DbConnection&gt;<span style="color: #000000;">()
                    .UsingFactoryMethod((kernel) </span>=&gt;<span style="color: #000000;">
                    {
                        </span><span style="color: #0000ff;">lock</span><span style="color: #000000;"> (_tenantDbs)
                        {
                            </span><span style="color: #0000ff;">var</span> currentUow = kernel.Resolve&lt;ICurrentUnitOfWorkProvider&gt;<span style="color: #000000;">().Current;
                            </span><span style="color: #0000ff;">var</span> abpSession = kernel.Resolve&lt;IAbpSession&gt;<span style="color: #000000;">();

                            </span><span style="color: #0000ff;">var</span> tenantId = currentUow != <span style="color: #0000ff;">null</span> ?<span style="color: #000000;"> currentUow.GetTenantId() : abpSession.TenantId;

                            </span><span style="color: #0000ff;">if</span> (tenantId == <span style="color: #0000ff;">null</span> || tenantId == <span style="color: #800080;">1</span>) <span style="color: #008000;">//</span><span style="color: #008000;">host and default tenant are stored in host db</span>
<span style="color: #000000;">                            {
                                </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> _hostDb;
                            }

                            </span><span style="color: #0000ff;">if</span> (!<span style="color: #000000;">_tenantDbs.ContainsKey(tenantId.Value))
                            {
                                _tenantDbs[tenantId.Value] </span>=<span style="color: #000000;"> DbConnectionFactory.CreateTransient();
                            }

                            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> _tenantDbs[tenantId.Value];
                        }
                    }, </span><span style="color: #0000ff;">true</span><span style="color: #000000;">)
                    .LifestyleTransient()
                );
        }

        </span><span style="color: #0000ff;">#region</span> UsingDbContext

        <span style="color: #0000ff;">protected</span> IDisposable UsingTenantId(<span style="color: #0000ff;">int</span>?<span style="color: #000000;"> tenantId)
        {
            </span><span style="color: #0000ff;">var</span> previousTenantId =<span style="color: #000000;"> AbpSession.TenantId;
            AbpSession.TenantId </span>=<span style="color: #000000;"> tenantId;
            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span> DisposeAction(() =&gt; AbpSession.TenantId =<span style="color: #000000;"> previousTenantId);
        }

        </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">void</span> UsingDbContext(Action&lt;PMDBContext&gt;<span style="color: #000000;"> action)
        {
            UsingDbContext(AbpSession.TenantId, action);
        }

        </span><span style="color: #0000ff;">protected</span> Task UsingDbContextAsync(Func&lt;PMDBContext, Task&gt;<span style="color: #000000;"> action)
        {
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> UsingDbContextAsync(AbpSession.TenantId, action);
        }

        </span><span style="color: #0000ff;">protected</span> T UsingDbContext&lt;T&gt;(Func&lt;PMDBContext, T&gt;<span style="color: #000000;"> func)
        {
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> UsingDbContext(AbpSession.TenantId, func);
        }

        </span><span style="color: #0000ff;">protected</span> Task&lt;T&gt; UsingDbContextAsync&lt;T&gt;(Func&lt;PMDBContext, Task&lt;T&gt;&gt;<span style="color: #000000;"> func)
        {
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> UsingDbContextAsync(AbpSession.TenantId, func);
        }

        </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">void</span> UsingDbContext(<span style="color: #0000ff;">int</span>? tenantId, Action&lt;PMDBContext&gt;<span style="color: #000000;"> action)
        {
            </span><span style="color: #0000ff;">using</span><span style="color: #000000;"> (UsingTenantId(tenantId))
            {
                </span><span style="color: #0000ff;">using</span> (<span style="color: #0000ff;">var</span> context = LocalIocManager.Resolve&lt;PMDBContext&gt;<span style="color: #000000;">())
                {
                    context.DisableAllFilters();
                    action(context);
                    context.SaveChanges();
                }
            }
        }

        </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">async</span> Task UsingDbContextAsync(<span style="color: #0000ff;">int</span>? tenantId, Func&lt;PMDBContext, Task&gt;<span style="color: #000000;"> action)
        {
            </span><span style="color: #0000ff;">using</span><span style="color: #000000;"> (UsingTenantId(tenantId))
            {
                </span><span style="color: #0000ff;">using</span> (<span style="color: #0000ff;">var</span> context = LocalIocManager.Resolve&lt;PMDBContext&gt;<span style="color: #000000;">())
                {
                    context.DisableAllFilters();
                    </span><span style="color: #0000ff;">await</span><span style="color: #000000;"> action(context);
                    </span><span style="color: #0000ff;">await</span><span style="color: #000000;"> context.SaveChangesAsync();
                }
            }
        }

        </span><span style="color: #0000ff;">protected</span> T UsingDbContext&lt;T&gt;(<span style="color: #0000ff;">int</span>? tenantId, Func&lt;PMDBContext, T&gt;<span style="color: #000000;"> func)
        {
            T result;

            </span><span style="color: #0000ff;">using</span><span style="color: #000000;"> (UsingTenantId(tenantId))
            {
                </span><span style="color: #0000ff;">using</span> (<span style="color: #0000ff;">var</span> context = LocalIocManager.Resolve&lt;PMDBContext&gt;<span style="color: #000000;">())
                {
                    context.DisableAllFilters();
                    result </span>=<span style="color: #000000;"> func(context);
                    context.SaveChanges();
                }
            }

            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> result;
        }

        </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">async</span> Task&lt;T&gt; UsingDbContextAsync&lt;T&gt;(<span style="color: #0000ff;">int</span>? tenantId, Func&lt;PMDBContext, Task&lt;T&gt;&gt;<span style="color: #000000;"> func)
        {
            T result;

            </span><span style="color: #0000ff;">using</span><span style="color: #000000;"> (UsingTenantId(tenantId))
            {
                </span><span style="color: #0000ff;">using</span> (<span style="color: #0000ff;">var</span> context = LocalIocManager.Resolve&lt;PMDBContext&gt;<span style="color: #000000;">())
                {
                    context.DisableAllFilters();
                    result </span>= <span style="color: #0000ff;">await</span><span style="color: #000000;"> func(context);
                    </span><span style="color: #0000ff;">await</span><span style="color: #000000;"> context.SaveChangesAsync();
                }
            }

            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> result;
        }

        </span><span style="color: #0000ff;">#endregion</span>

        <span style="color: #0000ff;">#region</span> Login

        <span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> LoginAsHostAdmin()
        {
            LoginAsHost(User.AdminUserName);
        }

        </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> LoginAsDefaultTenantAdmin()
        {
            LoginAsTenant(Tenant.DefaultTenantName, User.AdminUserName);
        }

        </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> LogoutAsDefaultTenant()
        {
            LogoutAsTenant(Tenant.DefaultTenantName);
        }

        </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">void</span> LoginAsHost(<span style="color: #0000ff;">string</span><span style="color: #000000;"> userName)
        {
            AbpSession.TenantId </span>= <span style="color: #0000ff;">null</span><span style="color: #000000;">;

            </span><span style="color: #0000ff;">var</span> user =<span style="color: #000000;">
                UsingDbContext(
                    context </span>=&gt;<span style="color: #000000;">
                        context.Users.FirstOrDefault(u </span>=&gt; u.TenantId == AbpSession.TenantId &amp;&amp; u.UserName ==<span style="color: #000000;"> userName));
            </span><span style="color: #0000ff;">if</span> (user == <span style="color: #0000ff;">null</span><span style="color: #000000;">)
            {
                </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> Exception(<span style="color: #800000;">"</span><span style="color: #800000;">There is no user: </span><span style="color: #800000;">"</span> + userName + <span style="color: #800000;">"</span><span style="color: #800000;"> for host.</span><span style="color: #800000;">"</span><span style="color: #000000;">);
            }

            AbpSession.UserId </span>=<span style="color: #000000;"> user.Id;
        }

        </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> LogoutAsHost()
        {
            Resolve</span>&lt;IMultiTenancyConfig&gt;().IsEnabled = <span style="color: #0000ff;">true</span><span style="color: #000000;">;

            AbpSession.TenantId </span>= <span style="color: #0000ff;">null</span><span style="color: #000000;">;
            AbpSession.UserId </span>= <span style="color: #0000ff;">null</span><span style="color: #000000;">;
        }

        </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">void</span> LoginAsTenant(<span style="color: #0000ff;">string</span> tenancyName, <span style="color: #0000ff;">string</span><span style="color: #000000;"> userName)
        {
            </span><span style="color: #0000ff;">var</span> tenant = UsingDbContext(context =&gt; context.Tenants.FirstOrDefault(t =&gt; t.TenancyName ==<span style="color: #000000;"> tenancyName));
            </span><span style="color: #0000ff;">if</span> (tenant == <span style="color: #0000ff;">null</span><span style="color: #000000;">)
            {
                </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> Exception(<span style="color: #800000;">"</span><span style="color: #800000;">There is no tenant: </span><span style="color: #800000;">"</span> +<span style="color: #000000;"> tenancyName);
            }

            AbpSession.TenantId </span>=<span style="color: #000000;"> tenant.Id;

            </span><span style="color: #0000ff;">var</span> user =<span style="color: #000000;">
                UsingDbContext(
                    context </span>=&gt;<span style="color: #000000;">
                        context.Users.FirstOrDefault(u </span>=&gt; u.TenantId == AbpSession.TenantId &amp;&amp; u.UserName ==<span style="color: #000000;"> userName));
            </span><span style="color: #0000ff;">if</span> (user == <span style="color: #0000ff;">null</span><span style="color: #000000;">)
            {
                </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> Exception(<span style="color: #800000;">"</span><span style="color: #800000;">There is no user: </span><span style="color: #800000;">"</span> + userName + <span style="color: #800000;">"</span><span style="color: #800000;"> for tenant: </span><span style="color: #800000;">"</span> +<span style="color: #000000;"> tenancyName);
            }

            AbpSession.UserId </span>=<span style="color: #000000;"> user.Id;
        }

        </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">void</span> LogoutAsTenant(<span style="color: #0000ff;">string</span><span style="color: #000000;"> tenancyName)
        {
            </span><span style="color: #0000ff;">var</span> tenant = UsingDbContext(context =&gt; context.Tenants.FirstOrDefault(t =&gt; t.TenancyName ==<span style="color: #000000;"> tenancyName));
            </span><span style="color: #0000ff;">if</span> (tenant == <span style="color: #0000ff;">null</span><span style="color: #000000;">)
            {
                </span><span style="color: #0000ff;">throw</span> <span style="color: #0000ff;">new</span> Exception(<span style="color: #800000;">"</span><span style="color: #800000;">There is no tenant: </span><span style="color: #800000;">"</span> +<span style="color: #000000;"> tenancyName);
            }

            AbpSession.TenantId </span>=<span style="color: #000000;"> tenant.Id;
            AbpSession.UserId </span>= <span style="color: #0000ff;">null</span><span style="color: #000000;">;
        }

        </span><span style="color: #0000ff;">#endregion</span>

        <span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
        <span style="color: #808080;">///</span><span style="color: #008000;"> Gets current user if </span><span style="color: #808080;">&lt;see cref="IAbpSession.UserId"/&gt;</span><span style="color: #008000;"> is not null.
        </span><span style="color: #808080;">///</span><span style="color: #008000;"> Throws exception if it's null.
        </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
        <span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">async</span> Task&lt;Core.Users.User&gt;<span style="color: #000000;"> GetCurrentUserAsync()
        {
            </span><span style="color: #0000ff;">var</span> userId =<span style="color: #000000;"> AbpSession.GetUserId();
            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">await</span> UsingDbContext(context =&gt; context.Users.SingleAsync(u =&gt; u.Id ==<span style="color: #000000;"> userId));
        }

        </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;summary&gt;</span>
        <span style="color: #808080;">///</span><span style="color: #008000;"> Gets current tenant if </span><span style="color: #808080;">&lt;see cref="IAbpSession.TenantId"/&gt;</span><span style="color: #008000;"> is not null.
        </span><span style="color: #808080;">///</span><span style="color: #008000;"> Throws exception if there is no current tenant.
        </span><span style="color: #808080;">///</span> <span style="color: #808080;">&lt;/summary&gt;</span>
        <span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">async</span> Task&lt;Tenant&gt;<span style="color: #000000;"> GetCurrentTenantAsync()
        {
            </span><span style="color: #0000ff;">var</span> tenantId =<span style="color: #000000;"> AbpSession.GetTenantId();
            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">await</span> UsingDbContext(context =&gt; context.Tenants.SingleAsync(t =&gt; t.Id ==<span style="color: #000000;"> tenantId));
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">PMTestBase</span></div>
<p>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('a7f998cf-01d1-4efa-84f0-19603520a7b8')"><img id="code_img_closed_a7f998cf-01d1-4efa-84f0-19603520a7b8" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_a7f998cf-01d1-4efa-84f0-19603520a7b8" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('a7f998cf-01d1-4efa-84f0-19603520a7b8',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_a7f998cf-01d1-4efa-84f0-19603520a7b8" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Text;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Modules;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.MultiTenancy;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.TestBase;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Abp.Zero.Configuration;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Castle.MicroKernel.Registration;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> NSubstitute;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.Application;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> PM.EntityFramework;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> PM.Test
{
    [DependsOn(
           </span><span style="color: #0000ff;">typeof</span><span style="color: #000000;">(PMDataModule),
           </span><span style="color: #0000ff;">typeof</span><span style="color: #000000;">(PMApplicationModule),
           </span><span style="color: #0000ff;">typeof</span><span style="color: #000000;">(AbpTestBaseModule)
       )]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> PMTestModule:AbpModule
    {
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">void</span><span style="color: #000000;"> PreInitialize()
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;">使用数据库进行语言管理</span>
<span style="color: #000000;">            Configuration.Modules.Zero().LanguageManagement.EnableDbLocalization();

            </span><span style="color: #008000;">//</span><span style="color: #008000;">注册伪服务</span>
<span style="color: #000000;">
            IocManager.IocContainer.Register(
                Component.For</span>&lt;IAbpZeroDbMigrator&gt;<span style="color: #000000;">()
                    .UsingFactoryMethod(() </span>=&gt; Substitute.For&lt;IAbpZeroDbMigrator&gt;<span style="color: #000000;">())
                    .LifestyleSingleton()
                );
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">PMTestModule</span></div>
<p>&nbsp;</p>
<div class="cnblogs_code" onclick="cnblogs_code_show('fdd052ac-4208-4df8-a074-9281ecf5aec0')"><img id="code_img_closed_fdd052ac-4208-4df8-a074-9281ecf5aec0" class="code_img_closed" src="http://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif" alt="" /><img id="code_img_opened_fdd052ac-4208-4df8-a074-9281ecf5aec0" class="code_img_opened" style="display: none;" onclick="cnblogs_code_hide('fdd052ac-4208-4df8-a074-9281ecf5aec0',event)" src="http://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif" alt="" />
<div id="cnblogs_code_open_fdd052ac-4208-4df8-a074-9281ecf5aec0" class="cnblogs_code_hide">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> Xunit;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> AbpCompanyName.AbpProjectName.Tests
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">sealed</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MultiTenantFactAttribute : FactAttribute
    {
        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> MultiTenantFactAttribute()
        {
            </span><span style="color: #0000ff;">if</span> (!<span style="color: #000000;">AbpProjectNameConsts.MultiTenancyEnabled)
            {
                Skip </span>= <span style="color: #800000;">"</span><span style="color: #800000;">MultiTenancy is disabled.</span><span style="color: #800000;">"</span><span style="color: #000000;">;
            }
        }
    }
}</span></pre>
</div>
<span class="cnblogs_code_collapse">MultiTenantFactAttribute</span></div>
<p>&nbsp;</p>