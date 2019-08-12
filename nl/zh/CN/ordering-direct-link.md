---

copyright:
  years: 2019

lastupdated: "2019-07-30"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:download: .download}

# 订购 IBM Cloud Direct Link Connect 以用于 Power Systems Virtual Server
{: #ordering-direct-link-connect}

配置专用网络以用于 {{site.data.keyword.powerSys_notm}} 的一个选项是使用 Direct Link Connect 服务。Direct Connect Link 服务将创建一个连接，用于允许通过 {{site.data.keyword.powerSys_notm}} 实例访问 {{site.data.keyword.cloud}} 资源。Direct Link Connect 服务还可用于通过 IBM Cloud 虚拟路由器设备 (VRA) 将内部部署网络连接到 IBM Cloud 网络。
{:shortdesc}

可以使用 {{site.data.keyword.cloud_notm}} UI 控制台来订购 Direct Link Connect 服务。Direct Link Connect 服务独立于 {{site.data.keyword.powerSys_notm}} 服务。要查看 Direct Link Connect 的费用，请参阅 [IBM Cloud Direct Link 定价](/docs/infrastructure/direct-link?topic=direct-link-pricing-for-direct-link-connect)。

IBM 建议您订购另一个 Direct Link Connect 连接以用作备份。

## 开始之前
{: #before-direct-link-connect}

* 验证 {{site.data.keyword.cloud}} 帐户是否具有正确的授权可订购 Direct Link Connect 服务。
* 通过查看以下主题，了解 Direct Link Connect 服务的基本联网概念：
    * [Direct Link Connect 概念](/docs/infrastructure/direct-link?topic=direct-link-direct-link-connect-solution#direct-link-connect-solution)
    * [Direct Link Connect 详细信息](/docs/infrastructure/direct-link?topic=direct-link-ibm-cloud-direct-link-connect-details)
    * [Direct Link Connect 限制](/docs/infrastructure/direct-link?topic=direct-link-known-limitations#ibm-cloud-direct-link-exchange-and-direct-link-connect-limitations)
    * [对 IP 分配的严格限制](/docs/infrastructure/direct-link?topic=direct-link-configure-ibm-cloud-direct-link#strict-limitations-on-ip-assignments)

## 订购 Direct Link Connect 的步骤
{: #steps-to-order-direct-link-connect}

要订购 Direct Link Connect 服务以创建与 {{site.data.keyword.powerSys_notm}} 实例的连接，请完成以下步骤；

1. 使用 IBM Cloud 帐户凭证登录到 [IBM Cloud 目录 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com/catalog){: new_window}。您的帐户必须具有正确的授权才能订购 Direct Link Connect 服务。

2. 在**联网**部分中，单击 **Direct Link Connect** 磁贴。
![显示 Direct Link 目录磁贴](/images/directlink1.png "显示 Direct Link 目录磁贴")

1. 在 Direct Link Connect 目录条目中，单击**创建**。

1. 在 IBM Cloud Direct Link 页面中，单击**订购 Direct Link Connect**。

1. 在“创建 IBM Cloud Direct Link Connect 连接”页面中，填写以下字段。

   填写以下字段以创建 Direct Link Connect 服务时，价格会自动更新以反映出您的选择。
   {: note}

   <dl>
   <dt><strong>Direct Link 实例名称</strong><dt>
   <dd>输入描述 Direct Link Connect 用途的名称。</dd>
   <dt><strong>位置</strong><dt>
   <dd>选择与 {{site.data.keyword.powerSys_notm}} 实例相同的位置。下表标识了 {{site.data.keyword.powerSys_notm}} 实例位置和相应的 Direct Link 连接选项：
   <table>
   <caption>表 1. Direct Link 连接位置选项</caption>
   <tr>
   <th>Power Systems Virtual Server 位置</th>
   <th>Direct Link Connect 位置</th>
   </tr>
   <tr>
   <td>美国得克萨斯州达拉斯</td>
   <td>达拉斯 4</td>
   </tr>
   <tr>
   <td>美国华盛顿</td>
   <td>华盛顿 2</td>
   </tr>
   </table>
   </dd>
   <dt><strong>网络提供商</strong><dt>
   <dd>必须从列表中选择 <strong>MEGAPORT</strong>。</dd>
   <dt><strong>链路速度</strong><dt>
   <dd>选择满足工作负载需求的链路速度。此字段的建议选择是 1000 Mbps。</dd>
   <dt><strong>路由选项</strong><dt>
   <dd>选择<strong>本地路由（免费）</strong>可访问在<strong>位置</strong>字段中指定的位置所连接的所有数据中心。选择<strong>全球路由</strong>可访问全球所有 IBM Cloud 数据中心。</dd>
   <dt><strong>BGP ASN</strong><dt>
   <dd>必须输入下表中特定 Direct Link Connect 位置的 BGP ASN 编号。
   <table>
   <caption>表 2. 特定位置的 BGP ASN 编号</caption>
   <tr>
   <th>Direct Link Connect 位置</th>
   <th>BGP ASN 编号</th>
   </tr>
   <tr>
   <td>达拉斯 4</td>
   <td>64997</td>
   </tr>
   <tr>
   <td>华盛顿 2</td>
   <td>64999</td>
   </tr>
   </table>
   </dd>
   <dt><strong>选择 VRF</strong><dt>
   <dd>选择连接的虚拟路由和转发选项。如果帐户未识别到 VRF，那么不会显示此字段。您仍可以在不选择 VRF 的情况下创建 Direct Link Connect 服务。下图是 Direct Link Connect 字段的示例。</dd>
   <dd>

   ![显示已填写的 Direct Link Connect 字段](/images/directlink2.png "显示已填写的 Direct Link Connect 字段")
   </dd>
   </dl>
2. 阅读**主服务协议**，然后选中相应复选框。您必须阅读并理解**主服务协议**，因为其中包含重要的技术信息。

3. 单击**创建**。成功提交请求后，将显示以下消息。
![显示 Direct Link Connect 已成功提交的消息](/images/directlink3.png "显示 Direct Link Connect 已成功提交的消息")

1. 单击 Direct Link Connect 服务的**案例号**链接。案例号中的信息用于标识连接 {{site.data.keyword.powerSys_notm}} 实例的 Direct Link Connect 信息。

  IBM Cloud 支持团队创建 Direct Link Connect 连接可能需要最长三个工作日。
  {: note}

2. 要使用 Direct Link Connect 服务创建与 {{site.data.keyword.powerSys_notm}} 实例的连接，请向 {{site.data.keyword.powerSys_notm}} 支持团队打开[新案例](/docs/infrastructure/power-iaas?topic=power-iaas-getting-help-and-support)。

      1. 在新案例的描述字段中，添加 Direct Link Connect 案例号。
      2. 复制系统自动生成的 {site.data.keyword.powerSys_notm}} 案例 IAM 服务标识。

3. 将 {{site.data.keyword.powerSys_notm}} 案例中的 IAM 服务标识输入到 Direct Link Connect 案例中。创建 Direct Link Connect 连接后，Direct Link Connect 案例号会关闭。下面是在案例中显示的网络信息的示例：

  ```shell
  Link Speed:                  1000 Mbps
  Location:                    Washington 2
  Network Provider:            MEGAPORT
  IBM IP Address:              10.254.0.25/30
  Customer IP Address:         10.254.0.26/30
  Service Key:                 None
  BGP ASN:                     64999
  Network Identifier:          1748523-1
  Date Created:                2019-06-12T14:56:45-06:00
  ```
  {: screen}

1. 使用 Direct Link Connect 案例号中的这些信息，并将以下网络信息输入到 {{site.data.keyword.powerSys_notm}} 案例中：

  ```shell
  Customer name:
  Customer account ID:
  Direct Link Connect subnet:
  Power Systems Virtual Server network IP address:
  IBM Cloud IP address:
  Power Systems Virtual Server network ASN:
  IBM Cloud ASN:
  Private Network ID (1):
  Private Network ID (2):
  Private Network ID (3):
  ```
  {: codeblock}

1. 将 Direct Link Connect 连接配置为与 {{site.data.keyword.powerSys_notm}} 实例通信后，{{site.data.keyword.powerSys_notm}} 案例会关闭。
