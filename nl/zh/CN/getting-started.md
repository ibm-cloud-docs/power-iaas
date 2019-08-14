---

copyright:
  years: 2019

lastupdated: "2019-7-12"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:important: .important}
{:tip: .tip}

# Power Systems Virtual Server 入门
{: #getting-started}


{{site.data.keyword.powerSysFull}} 是一种基础架构即服务产品，可用于在几分钟内部署虚拟服务器，也称为逻辑分区 (LPAR)。
{:shortdesc}

您可以快速部署 {{site.data.keyword.powerSys_notm}}，以满足特定业务需求。通过 {{site.data.keyword.powerSys_notm}}，可以创建混合云环境，使您能够轻松控制工作负载需求。

{{site.data.keyword.powerSys_notm}} 可以在不同地理位置运行 AIX 或 IBM i 工作负载。

## 术语
{: #gs-terminology}

在创建虚拟服务器之前，您必须了解 {{site.data.keyword.powerSys_notm}} **服务**和 {{site.data.keyword.powerSys_notm}} **实例**在术语上的差异。请将 {{site.data.keyword.powerSys_notm}} **服务**视为特定地理位置中所有 {{site.data.keyword.powerSys_notm}} **实例**的容器。{{site.data.keyword.powerSys_notm}} **服务**可通过 {{site.data.keyword.cloud}} UI 中的**资源列表**使用。服务可以包含多个 {{site.data.keyword.powerSys_notm}} **实例**。

例如，您可以有两个 {{site.data.keyword.powerSys_notm}} **服务**，一个位于达拉斯，另一个位于华盛顿。每个服务可以包含多个 {{site.data.keyword.powerSys_notm}} **实例**。

## 开始之前
{: #gs-before-you-begin}

创建第一个 Power Systems Virtual Server 实例之前，请查看以下先决条件：

1. {: hide-dashboard}创建 IBM Cloud 帐户。要创建 IBM Cloud 帐户，请参阅[注册 IBM Cloud ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com/registration){: new_window}。

2. 创建可用于安全连接到 {{site.data.keyword.powerSys_notm}} 的公用和专用 SSH 密钥。要创建公用和专用 SSH 密钥，请参阅[添加 SSH 密钥 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com/docs/infrastructure/ssh-keys?topic=ssh-keys-adding-an-ssh-key)。

3. （可选）如果要将定制映像用于 AIX 或 IBM i 操作系统，那么必须创建 IBM Cloud Object Storage 并上传该映像。有关更多信息，请参阅[配置定制映像](/docs/infrastructure/power-iaas?topic=power-iaas-configuring-custom-image#configuring-custom-image)。

4. （可选）如果要使用专用网络连接到 {{site.data.keyword.powerSys_notm}} 实例，那么必须订购 Direct Link Connect 服务。有关更多信息，请参阅[通过 UI 控制台订购 IBM Cloud Direct Link Connect](/docs/infrastructure/power-iaas?topic=power-iaas-ordering-direct-link-connect)。

## 后续步骤
{: #gs-next-steps}

有了 IBM Cloud 帐户以及专用和公用 SSH 密钥，现在您已准备好[创建 {{site.data.keyword.powerSys_notm}} 服务](/docs/infrastructure/power-iaas?topic=power-iaas-creating-power-virtual-server#creating-power-virtual-server)。
