<p>1，依赖注入</p>
<div>EntityframeworkDemoSchemaDbMigrator&nbsp;:&nbsp;IDemoSchemaDbMigrator,&nbsp;ITransientDependency</div>
<div>约定：实现类后面的命令必须包含DemoSchemaDbMigrator</div>
<p>&nbsp;</p>
<p>2，appsettings.json</p>
<p>①始终复制</p>
<div class="cnblogs_code">
<pre>  &lt;ItemGroup&gt;
    &lt;Content Include=<span style="color: #800000;">"</span><span style="color: #800000;">appsettings.json</span><span style="color: #800000;">"</span>&gt;
      &lt;CopyToPublishDirectory&gt;PreserveNewest&lt;/CopyToPublishDirectory&gt;
      &lt;CopyToOutputDirectory&gt;Always&lt;/CopyToOutputDirectory&gt;
    &lt;/Content&gt;
  &lt;/ItemGroup&gt;</pre>
</div>
<p>②嵌入的资源</p>
<div class="cnblogs_code">
<pre>  &lt;ItemGroup&gt;
    &lt;None Remove=<span style="color: #800000;">"</span><span style="color: #800000;">Templates\Files\Hello.tpl</span><span style="color: #800000;">"</span> /&gt;
    &lt;EmbeddedResource Include=<span style="color: #800000;">"</span><span style="color: #800000;">Templates\Files\Hello.tpl</span><span style="color: #800000;">"</span> /&gt;
  &lt;/ItemGroup&gt;</pre>
</div>
<div class="cnblogs_code">
<pre>  &lt;ItemGroup&gt;
    &lt;EmbeddedResource Include=<span style="color: #800000;">"</span><span style="color: #800000;">Localization\Files\*.json</span><span style="color: #800000;">"</span> /&gt;
    &lt;Content Remove=<span style="color: #800000;">"</span><span style="color: #800000;">Localization\Files\*.json</span><span style="color: #800000;">"</span> /&gt;
  &lt;/ItemGroup&gt;</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>3，迁移程序执行流程</p>
<p><img src="https://img2020.cnblogs.com/blog/741594/202101/741594-20210126111352300-666975942.png" alt="" width="1041" height="657" loading="lazy" /></p>
<p>&nbsp;</p>
<p>4，Hw_ScheduDbContextModelCreatingExtensions</p>
<div class="cnblogs_code">
<pre>             builder.Entity&lt;TaskInfo&gt;(b=&gt;<span style="color: #000000;">{
                b.ToTable(AbpIdentityDbProperties.DbTablePrefix </span>+ <span style="color: #800000;">"</span><span style="color: #800000;">TaskInfos</span><span style="color: #800000;">"</span><span style="color: #000000;">);
                b.ConfigureByConvention();
                b.Property(x</span>=&gt;<span style="color: #000000;">x.Name).HasMaxLength(TaskInfoConsts.MaxNameLength).IsRequired();
                b.Property(x</span>=&gt;<span style="color: #000000;">x.Remark).HasMaxLength(TaskInfoConsts.MaxRemarkLength);
                b.Property(x</span>=&gt;<span style="color: #000000;">x.Api).HasMaxLength(TaskInfoConsts.MaxApiLength).IsRequired();
                b.Property(x</span>=&gt;<span style="color: #000000;">x.Cron).HasMaxLength(TaskInfoConsts.MaxCronLength).IsRequired();
                b.Property(x</span>=&gt;<span style="color: #000000;">x.Status).IsRequired();
                b.Property(x</span>=&gt;<span style="color: #000000;">x.SystemInfoId).IsRequired();
                b.Property(x</span>=&gt;x.CreationTime).HasColumnType(<span style="color: #800000;">"</span><span style="color: #800000;">datetime</span><span style="color: #800000;">"</span>).HasDefaultValueSql(<span style="color: #800000;">"</span><span style="color: #800000;">now()</span><span style="color: #800000;">"</span><span style="color: #000000;">).IsRequired();
                b.Property(x</span>=&gt;x.LastModificationTime).HasColumnType(<span style="color: #800000;">"</span><span style="color: #800000;">datetime</span><span style="color: #800000;">"</span>).HasDefaultValueSql(<span style="color: #800000;">"</span><span style="color: #800000;">now()</span><span style="color: #800000;">"</span><span style="color: #000000;">).IsRequired();
                b.Property(x</span>=&gt;x.DeletionTime).HasColumnType(<span style="color: #800000;">"</span><span style="color: #800000;">datetime</span><span style="color: #800000;">"</span>).HasDefaultValueSql(<span style="color: #800000;">"</span><span style="color: #800000;">now()</span><span style="color: #800000;">"</span><span style="color: #000000;">).IsRequired();
                b.HasIndex(x</span>=&gt;<span style="color: #000000;">x.SystemInfoId);
            });</span></pre>
</div>
<p>&nbsp;</p>
<p>5，dto验证</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.ComponentModel;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.ComponentModel.DataAnnotations;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> EasyAbp.EShop.Stores.Stores;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Volo.Abp.ObjectExtending;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> EasyAbp.EShop.Orders.Orders.Dtos
{
    [Serializable]
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> CreateOrderDto : ExtensibleObject, IMultiStore
    {
        [DisplayName(</span><span style="color: #800000;">"</span><span style="color: #800000;">OrderStoreId</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
        </span><span style="color: #0000ff;">public</span> Guid StoreId { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

        [DisplayName(</span><span style="color: #800000;">"</span><span style="color: #800000;">OrderCustomerRemark</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">string</span> CustomerRemark { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

        [DisplayName(</span><span style="color: #800000;">"</span><span style="color: #800000;">OrderLine</span><span style="color: #800000;">"</span><span style="color: #000000;">)]
        </span><span style="color: #0000ff;">public</span> List&lt;CreateOrderLineDto&gt; OrderLines { <span style="color: #0000ff;">get</span>; <span style="color: #0000ff;">set</span><span style="color: #000000;">; }

        </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> IEnumerable&lt;ValidationResult&gt;<span style="color: #000000;"> Validate(ValidationContext validationContext)
        {
            </span><span style="color: #0000ff;">base</span><span style="color: #000000;">.Validate(validationContext);
            
            </span><span style="color: #0000ff;">if</span> (OrderLines.Count == <span style="color: #800080;">0</span><span style="color: #000000;">)
            {
                </span><span style="color: #0000ff;">yield</span> <span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> ValidationResult(
                    </span><span style="color: #800000;">"</span><span style="color: #800000;">OrderLines should not be empty.</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    </span><span style="color: #0000ff;">new</span>[] { <span style="color: #800000;">"</span><span style="color: #800000;">OrderLines</span><span style="color: #800000;">"</span><span style="color: #000000;"> }
                );
            }
            
            </span><span style="color: #0000ff;">if</span> (OrderLines.Any(orderLine =&gt; orderLine.Quantity &lt;= <span style="color: #800080;">0</span><span style="color: #000000;">))
            {
                </span><span style="color: #0000ff;">yield</span> <span style="color: #0000ff;">return</span> <span style="color: #0000ff;">new</span><span style="color: #000000;"> ValidationResult(
                    </span><span style="color: #800000;">"</span><span style="color: #800000;">Quantity should be greater than 0.</span><span style="color: #800000;">"</span><span style="color: #000000;">,
                    </span><span style="color: #0000ff;">new</span>[] { <span style="color: #800000;">"</span><span style="color: #800000;">OrderLines</span><span style="color: #800000;">"</span><span style="color: #000000;"> }
                );
            }
        }
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p>6，基于资源的授权</p>
<div class="cnblogs_code">
<pre> <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">async</span> Task&lt;OrderDto&gt;<span style="color: #000000;"> CreateAsync(CreateOrderDto input)
        {
            </span><span style="color: #008000;">//</span><span style="color: #008000;"> Todo: Check if the store is open.</span>

            <span style="color: #0000ff;">var</span> productDict = <span style="color: #0000ff;">await</span> GetProductDictionaryAsync(input.OrderLines.Select(dto =&gt;<span style="color: #000000;"> dto.ProductId).ToList());

            </span><span style="color: #0000ff;">await</span><span style="color: #000000;"> AuthorizationService.CheckAsync(
                </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> OrderCreationResource
                {
                    Input </span>=<span style="color: #000000;"> input,
                    ProductDictionary </span>=<span style="color: #000000;"> productDict
                },
                </span><span style="color: #0000ff;">new</span><span style="color: #000000;"> OrderOperationAuthorizationRequirement(OrderOperation.Creation)
            );

            </span><span style="color: #0000ff;">var</span> productDetailIds =<span style="color: #000000;"> input.OrderLines
                .Select(dto </span>=&gt;<span style="color: #000000;">
                    productDict[dto.ProductId].GetSkuById(dto.ProductSkuId).ProductDetailId </span>??<span style="color: #000000;">
                    productDict[dto.ProductId].ProductDetailId)
                .Where(x </span>=&gt;<span style="color: #000000;"> x.HasValue)
                .Select(x </span>=&gt;<span style="color: #000000;"> x.Value)
                .ToList();
            
            </span><span style="color: #0000ff;">var</span> productDetailDict = <span style="color: #0000ff;">await</span><span style="color: #000000;"> GetProductDetailDictionaryAsync(productDetailIds);

            </span><span style="color: #008000;">//</span><span style="color: #008000;"> Todo: Can we use IProductDataScopedCache/IProductDetailDataScopedCache instead of productDict/productDetailDict?</span>
            <span style="color: #0000ff;">var</span> order = <span style="color: #0000ff;">await</span><span style="color: #000000;"> _newOrderGenerator.GenerateAsync(CurrentUser.GetId(), input, productDict, productDetailDict);

            </span><span style="color: #0000ff;">await</span><span style="color: #000000;"> DiscountOrderAsync(order, productDict);

            </span><span style="color: #0000ff;">await</span> Repository.InsertAsync(order, autoSave: <span style="color: #0000ff;">true</span><span style="color: #000000;">);

            </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">await</span><span style="color: #000000;"> MapToGetOutputDtoAsync(order);
        }</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Authorization;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> EasyAbp.EShop.Orders.Orders
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">abstract</span> <span style="color: #0000ff;">class</span> OrderCreationAuthorizationHandler : AuthorizationHandler&lt;OrderOperationAuthorizationRequirement, OrderCreationResource&gt;<span style="color: #000000;">
    {
        </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">async</span><span style="color: #000000;"> Task HandleRequirementAsync(AuthorizationHandlerContext context, OrderOperationAuthorizationRequirement requirement,
            OrderCreationResource resource)
        {
            </span><span style="color: #0000ff;">if</span> (requirement.OrderOperation !=<span style="color: #000000;"> OrderOperation.Creation)
            {
                </span><span style="color: #0000ff;">return</span><span style="color: #000000;">;
            }
            
            </span><span style="color: #0000ff;">await</span><span style="color: #000000;"> HandleOrderCreationAsync(context, requirement, resource);
        }

        </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">abstract</span><span style="color: #000000;"> Task HandleOrderCreationAsync(AuthorizationHandlerContext context,
            OrderOperationAuthorizationRequirement requirement, OrderCreationResource resource);
    }
}</span></pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">using</span><span style="color: #000000;"> System;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Collections.Generic;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Linq;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> System.Threading.Tasks;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> EasyAbp.EShop.Orders.Authorization;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> EasyAbp.EShop.Orders.Orders.Dtos;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> EasyAbp.EShop.Products.Products;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> EasyAbp.EShop.Products.Products.Dtos;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Microsoft.AspNetCore.Authorization;
</span><span style="color: #0000ff;">using</span><span style="color: #000000;"> Volo.Abp.Authorization.Permissions;

</span><span style="color: #0000ff;">namespace</span><span style="color: #000000;"> EasyAbp.EShop.Orders.Orders
{
    </span><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> BasicOrderCreationAuthorizationHandler : OrderCreationAuthorizationHandler
    {
        </span><span style="color: #0000ff;">private</span> <span style="color: #0000ff;">readonly</span><span style="color: #000000;"> IPermissionChecker _permissionChecker;

        </span><span style="color: #0000ff;">public</span><span style="color: #000000;"> BasicOrderCreationAuthorizationHandler(IPermissionChecker permissionChecker)
        {
            _permissionChecker </span>=<span style="color: #000000;"> permissionChecker;
        }
        
        </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">override</span> <span style="color: #0000ff;">async</span><span style="color: #000000;"> Task HandleOrderCreationAsync(AuthorizationHandlerContext context,
            OrderOperationAuthorizationRequirement requirement, OrderCreationResource resource)
        {
            </span><span style="color: #0000ff;">if</span> (!<span style="color: #0000ff;">await</span><span style="color: #000000;"> _permissionChecker.IsGrantedAsync(OrdersPermissions.Orders.Create))
            {
                context.Fail();
                </span><span style="color: #0000ff;">return</span><span style="color: #000000;">;
            }
            
            </span><span style="color: #0000ff;">if</span> (!<span style="color: #0000ff;">await</span><span style="color: #000000;"> IsProductsPublishedAsync(resource.Input, resource.ProductDictionary))
            {
                context.Fail();
                </span><span style="color: #0000ff;">return</span><span style="color: #000000;">;
            }

            </span><span style="color: #0000ff;">if</span> (!<span style="color: #0000ff;">await</span><span style="color: #000000;"> IsInventoriesSufficientAsync(resource.Input, resource.ProductDictionary))
            {
                context.Fail();
                </span><span style="color: #0000ff;">return</span><span style="color: #000000;">;
            }
            
            context.Succeed(requirement);
        }

        </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">virtual</span> Task&lt;<span style="color: #0000ff;">bool</span>&gt;<span style="color: #000000;"> IsProductsPublishedAsync(CreateOrderDto input,
            Dictionary</span>&lt;Guid, ProductDto&gt;<span style="color: #000000;"> productDictionary)
        {
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> Task.FromResult(
                input.OrderLines.Select(dto </span>=&gt;<span style="color: #000000;"> dto.ProductId).Distinct().ToArray()
                    .All(productId </span>=&gt;<span style="color: #000000;"> productDictionary[productId].IsPublished)
            );
        }

        </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">virtual</span> Task&lt;<span style="color: #0000ff;">bool</span>&gt;<span style="color: #000000;"> IsInventoriesSufficientAsync(CreateOrderDto input,
            Dictionary</span>&lt;Guid, ProductDto&gt;<span style="color: #000000;"> productDictionary)
        {
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> Task.FromResult(
                </span>!(<span style="color: #0000ff;">from</span> orderLine <span style="color: #0000ff;">in</span><span style="color: #000000;"> input.OrderLines
                    let product </span>=<span style="color: #000000;"> productDictionary[orderLine.ProductId]
                    let inventory </span>= product.ProductSkus.Single(sku =&gt; sku.Id ==<span style="color: #000000;"> orderLine.ProductSkuId).Inventory
                    </span><span style="color: #0000ff;">where</span> product.InventoryStrategy != InventoryStrategy.NoNeed &amp;&amp; inventory &lt;<span style="color: #000000;"> orderLine.Quantity
                    </span><span style="color: #0000ff;">select</span><span style="color: #000000;"> orderLine).Any()
            );
        }
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p>7，abp sorting</p>
<ul>
<li><code>sorting</code>&nbsp;可以是一个字符串, 如&nbsp;<code>Name</code>,&nbsp;<code>Name ASC</code>&nbsp;或&nbsp;<code>Name DESC</code>. 通过使用&nbsp;<a href="https://www.nuget.org/packages/System.Linq.Dynamic.Core">System.Linq.Dynamic.Core</a>&nbsp;NuGet 包是可能的.</li>
</ul>
<p>&nbsp;</p>