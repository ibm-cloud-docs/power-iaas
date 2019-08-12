---

copyright:
  years: 2019

lastupdated: "2019-08-1"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:table: .aria-labeledby="caption"}

# 创建 Power Systems Virtual Server
{: #creating-power-virtual-server}

要创建和配置 {{site.data.keyword.powerSysFull}}，请完成以下步骤：

1. 使用 IBM Cloud 帐户凭证登录到 [IBM Cloud 目录 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com/catalog){: new_window}。
2. 在目录的搜索框中，输入 **Power Systems Virtual Server**，然后单击 {{site.data.keyword.powerSys_notm}} 磁贴。

    ![IBM Cloud“目录”](./images/catalog-search-bar.png "IBM Cloud“目录”")

3. 为服务提供名称，然后选择要部署 {{site.data.keyword.powerSys_notm}} 实例的位置。

    ![服务和区域选择](./images/power-iaas-service-region.png "服务和区域选择")

4. 单击 Web 页面底部的**创建**按钮。

    ![“创建”按钮](./images/power-iaas-create-button.png "“创建”按钮")

5. 单击**创建**按钮后，会将您重定向到**资源列表**面板。
6. 从**资源列表**中的**服务**下选择您的服务，以转至**管理**面板。

    ![IBM Cloud 资源列表](./images/power-iaas-resource-list.png "IBM Cloud 资源列表")

7. 在此，单击**供应新项**按钮。

    ![供应新的虚拟服务器](./images/power-iaas-provision-new.png "供应新的虚拟服务器")

8. 填写所有必填字段以成功创建新实例：

     填写字段以创建 {{site.data.keyword.powerSys_notm}} 时，价格会在**订单摘要**部分中动态更新。这允许您轻松创建具有成本效益的 {{site.data.keyword.powerSys_notm}}，以满足业务需求。
     {: tip}

    1. 填写**虚拟服务器**部分下的所有字段。如果选择了多个实例，那么将显示其他选项。

      ![创建新的 Power Virtual Server 实例](./images/console-virtual-instance.png "创建新的 Power Virtual Server 实例")

    1. 选择是需要**专用处理器**还是**共享处理器**。此外，还务必选择所需的**机器类型**、核心数和内存量。

      ![选择处理器和系统](./images/console-profile.png "选择处理器和系统")

    1. 最后，按照组织的指示，填写**引导卷**、**连接的卷**和**网络接口**字段。

      ![定义卷和网络接口](./images/console-volume-network.png "定义卷和网络接口")

9. 接受**使用条款**，然后单击**创建**按钮以供应新的 {{site.data.keyword.powerSys_notm}}。

下表提供了有关**虚拟服务器实例**字段的信息：

<table>
<caption>表 1. 新建 Power Virtual Server 实例的字段</caption>
<tr>
<th>字段</th>
<th>描述</th>
</tr>
<tr>
<td>实例数</td>
<td>指定要为 {{site.data.keyword.powerSys_notm}} 创建的实例数。如果指定多个实例，那么可以选择以下命名约定和主机托管规则：
  <dl>
    <dt><strong>无首选项</strong></dt>
  <dd>如果没有托管首选项，请选择此选项。</dd>
    <dt><strong>不同服务器</strong></dt>
  <dd>选择此选项可使每个实例在不同的服务器上托管。如果您担心发生可能影响所有 {{site.data.keyword.powerSys_notm}} 实例的单服务器中断，那么可以使用此选项。</dd>
  <dt><strong>数字前缀</strong></dt>
  <dd>选择此选项可在虚拟服务器的名称前面添加数字。例如，如果第一个 {{site.data.keyword.powerSys_notm}} 名称为 <kbd>Austin</kbd>，那么下一个虚拟实例名称为 <kbd>1Austin</kbd>。</dd>
  <dt><strong>数字后缀</strong></dt>
  <dd>选择此选项可在虚拟服务器的名称后面添加数字。例如，如果第一个 {{site.data.keyword.powerSys_notm}} 名称为 <kbd>Rochester</kbd>，那么下一个虚拟实例名称为 <kbd>Rochester1</kbd>。</dd>
  </dl>
  <p>
  <strong>注：</strong>创建虚拟服务器的多个实例时，必须在添加的每个数据卷的<strong>可共享</strong>字段中选择<strong>开启</strong>。如果您不希望数据卷可共享，那么可以在创建虚拟服务器后添加数据卷。
  </p>
   </td>
</tr>
<tr>
<td>锁定虚拟机</td>
<td>选择<strong>开启</strong>可将 {{site.data.keyword.powerSys_notm}} 锁定到主机系统上。如果选择<strong>开启</strong>，那么无法将虚拟服务器移至其他主机。例如，如果选择<strong>开启</strong>，那么在主机维护期间将遇到中断。</td>
</tr>
<tr>
<td>机器类型</td>
<td>指定机器类型。选择的机器类型将确定可用的核心数和内存量。有关硬件规范的更多信息，请参阅 <a href="https://www.ibm.com/downloads/cas/KQ4BOJ3N" target="_blank">S922</a> 和 <a href="https://www.ibm.com/downloads/cas/EE476WAP" target="_blank">E880</a>。</td>
</tr>
<tr>
<td>核心数</td>
<td>选择 {{site.data.keyword.powerSys_notm}} 的核心数。如果选择了<strong>共享处理器</strong>，那么可以按 0.25 的增量指定核心数。例如，有效的核心值为 0.5、1.25 和 2.75。这将为每 0.25 个权利分配一个虚拟 CPU。

如果您担心性能问题，那么可以选择<strong>专用处理器</strong>，因为该处理器将专用于虚拟服务器，而不会共享。有关更多信息，请参阅 <a href="https://www.ibm.com/developerworks/community/wikis/home?lang=en#!/wiki/Power%20Systems/page/How%20does%20Shared%20Processor%20Performance%20Compare%20to%20Dedicated%20Processors" target="_blank">How does Shared Processor Performance Compare to Dedicated Processors</a>。</td>
</tr>
<tr>
<td>内存</td>
<td>选择 {{site.data.keyword.powerSys_notm}} 的内存量。可以选择的内存量取决于所选的核心数。对于选择的每个核心，最多可以分配 64 GB。例如，如果选择了四个核心，那么允许您选择最多 256 GB 内存。</td>
</tr>
<tr>
<td>创建引导卷</td>
<td>选择为您提供的 AIX 或 IBM i 操作系统库存映像的版本，或者选择先前内部部署的定制 AIX 或 IBM i 操作系统映像。有关操作系统许可信息，请参阅 IBM 的 <a href="https://www-03.ibm.com/software/sla/sladb.nsf" target="_blank">License Information documents</a>。

如果要使用自带定制映像，那么必须使用在<strong>机器类型</strong>字段中选择的 Power Systems 硬件所支持的 AIX 或 IBM i 操作系统映像技术级别。有关更多信息，请参阅<a href="/docs/infrastructure/power-iaas?topic=power-iaas-configuring-custom-image#configuring-custom-image">配置定制映像</a>。</td>
</tr>
<tr>
<td>连接的数据卷</td>
<td>可以创建新的数据卷，也可以连接已在 IBM Cloud 帐户中定义的现有数据卷。<dl>
  <dt><strong>创建数据卷</strong></dt>
  <dd>单击<strong>添加</strong>可创建新数据卷，以用于为 {{site.data.keyword.powerSys_notm}} 实例提供更多存储空间。如果要允许 {{site.data.keyword.powerSys_notm}} 的多个实例将数据写入同一数据卷，那么必须在<strong>可共享</strong>字段中选择<strong>开启</strong>。</dd>
  <dt><strong>连接现有数据卷</strong></dt>
  <dd>选择现有数据卷，以用于为 {{site.data.keyword.powerSys_notm}} 实例提供更多存储空间。如果列表中未显示先前使用过的数据卷，可能是因为该数据卷是使用其他 IBM Cloud 帐户创建的。</dd>
</dl>
</td>
</tr>
<tr>
<td>公用网络</td>
<td>选择此选项可使用 IBM 提供的公用网络。选择此选项会有关联的成本。有关更多信息，请参阅<a href="/docs/infrastructure/power-iaas?topic=power-iaas-about-power-virtual-server#apvs-public-and-private" target="_blank">公用和专用网络</a>。</td>
</tr>
<tr>
<td>专用网络</td>
<td>单击<strong>添加</strong>以识别虚拟服务器的新专用网络。如果已添加专用网络，那么可以从列表中选择该网络。有关更多信息，请参阅<a href="/docs/infrastructure/power-iaas?topic=power-iaas-cpn-configuring#cpn-configuring" target="_blank">配置专用网络</a>。</td>
</tr></table>
