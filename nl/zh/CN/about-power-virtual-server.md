---

copyright:
  years: 2019

lastupdated: "2019-05-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}

# 关于 Power Systems Virtual Server
{: #about-power-virtual-server}

{{site.data.keyword.powerSysFull}} 使用现有 IBM Cloud 平台来创建 Power Systems 虚拟服务器，这种虚拟服务器也称为逻辑分区 (LPAR)，通过 PowerVM 系统管理程序在 IBM Power Systems 硬件上运行。
{:shortdesc}

{{site.data.keyword.powerSys_notm}} 是一种形式的基础架构即服务 (IaaS)。通过 {{site.data.keyword.powerSys_notm}} 服务，可以快速创建和部署在公共云中运行 AIX 或 IBM i 操作系统的一个或多个虚拟服务器。在云中供应虚拟服务器后，您应负责确保 AIX 或 IBM i 操作系统安全。

## 主要功能
{: #apvs-key-features}

下面是 {{site.data.keyword.powerSys_notm}} 的一些主要功能。

### 简单的计费方式
{: #apvs-billing}

{{site.data.keyword.powerSys_notm}} 使用每月计费费率，其中包含 AIX 和 IBM i 操作系统的许可证。每月计费费率会根据当月部署到 {{site.data.keyword.powerSys_notm}} 实例的资源，按比例以小时计算。创建 {{site.data.keyword.powerSys_notm}} 实例时，可以根据指定的选项来查看配置的总成本。您可以快速确定哪些配置选项提供的价值最符合您的业务需求。有关更多信息，请参阅[定价](/docs/infrastructure/power-iaas?topic=power-iaas-pricing-virtual-server#pricing-virtual-server)。

### 混合云环境
{: #apvs-hybrid}

您可以使用 {{site.data.keyword.powerSys_notm}} 来运行现有 Power Systems 硬件基础架构外部部署的任何 AIX 或 IBM i 工作负载。通过在公共云中运行工作负载，您可以享受云中提供的所有优势，例如自助服务、快速交付、弹性以及与其他 IBM Cloud 服务的连接。虽然 AIX 和 IBM i 工作负载在云中运行，但您拥有的可扩展性、弹性和生产就绪型功能仍保持与 Power Systems 硬件提供的相同。

### 基础架构定制
{: #apvs-customization}

创建 {{site.data.keyword.powerSys_notm}} 时，可以配置和定制以下选项：
* 虚拟服务器实例数
* 核心数
* 内存量
* 数据卷大小和类型（HDD 或 SSD）
* 专用或公用网络

### 自带映像
{: #apvs-own-image}

在创建 {{site.data.keyword.powerSys_notm}} 时，IBM 会提供 AIX 和 IBM i 操作系统库存映像。但是，您可以使用先前已部署并测试的自带定制 AIX 或 IBM i 操作系统映像。有关更多信息，请参阅[配置定制映像](/docs/infrastructure/power-iaas?topic=power-iaas-configuring-custom-image#configuring-custom-image)。

## 硬件规范
{: #apvs-hardware-specifications}

以下 IBM Power Systems 硬件托管 {{site.data.keyword.powerSys_notm}}：

* 计算
  * [Power System E880 (9119-MHE) ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/support/knowledgecenter/en/POWER8/p8hdx/9119_mhe_landing.htm){: new_window}
    * 9 TB 内存
    * 8 个 16 千兆位 PCI Express 双端口光纤通道 (FC)
    * 10 个 10 千兆以太网 SR PCI Express 双端口
  * [Power System S922 (9009-22A) ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/support/knowledgecenter/en/POWER9/p9hdx/9009_22a_landing.htm){: new_window}
    * 384 GB 内存
    * 2 个 16 千兆位 PCI Express 双端口 FC
    * 3 个 10 千兆以太网 SR PCI Express 双端口

* 存储
  * Storewize V7000F(2076-AF6) 双控制器
  * Storwize V7000 (2076-624) 双控制器

* 网络
  * Cisco Nexus9000 93180YC-EX (10G)
  * Cisco Nexus9000 C9348GC-FXP (1G)

## 公用和专用网络
{: #apvs-public-and-private}

创建 {{site.data.keyword.powerSys_notm}} 时，可以选择专用网络接口或公用网络接口。

* 公用网络
  * 连接到 {{site.data.keyword.powerSys_notm}} 实例的简单快速方法。
  * IBM 配置网络基础架构，以支持从因特网到 {{site.data.keyword.powerSys_notm}} 实例的安全公用网络连接。
  * 连接性使用 IBM Cloud 虚拟路由器设备 (VRA) 和 Direct Link Connect 连接来实现。
  * 通过防火墙保护，并支持以下安全网络协议：
    * SSH
    * HTTPS
    * Ping
    * 使用 SSL 的 IBM i 5250 终端仿真（端口 992）

* 专用网络
  * 允许 {{site.data.keyword.powerSys_notm}} 实例的资源访问现有 {{site.data.keyword.cloud_notm}} 资源，例如裸机服务器、Kubernetes 容器或云存储器。
  * 使用 Direct Link Connect 连接来连接到 IBM Cloud 帐户网络和资源。创建 Direct Link Connect 连接的过程可能需要几天时间，因为 IBM Cloud 支持人员必须配置该链路。
  * 不同的 {{site.data.keyword.powerSys_notm}} 实例之间进行通信需要专用网络。

    有关配置专用网络的不同选项的更多信息，请参阅[配置专用网络](/docs/infrastructure/power-iaas?topic=power-iaas-cpn-configuring#cpn-configuring)。
    {: note}

下图显示了公用和专用网络的基本配置：

![显示公共或专用连接的网络流量如何流动](/images/power-iaas-network1.svg "显示公共或专用连接的网络流量如何流动")

<!-- Customer A is able to connect to a public network by using a Direct Link Dedicated connection with their {{site.data.keyword.cloud_notm}} Power account. -->
<!-- Customer A is able to connect to a private network by using a Direct Link Connect connection with their {{site.data.keyword.cloud_notm}} account. -->
<!-- Customer A can use either a public or private network to access their {{site.data.keyword.powerSys_notm}}. -->
<!-- Customer B is able to connect to only a private network by using a Direct Link Connect connection with their {{site.data.keyword.cloud_notm}} account.  -->
