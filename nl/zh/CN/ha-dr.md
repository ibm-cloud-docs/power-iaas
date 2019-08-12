---

copyright:
  years: 2019

lastupdated: "2019-07-29"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:important: .important}
{:tip: .tip}
{:note: .note}

# Power Systems Virtual Server 的高可用性和灾难恢复选项
{: #ha-dr}

如果发生硬件故障，{{site.data.keyword.powerSys_notm}} 实例会在不同的主机系统上重新启动虚拟服务器。此过程为 {{site.data.keyword.powerSys_notm}} 服务提供了基本高可用性 (HA) 功能。
{:shortdesc}

如果需要更高级的 HA 或灾难恢复 (DR) 解决方案，可以在 {{site.data.keyword.powerSys_notm}} 环境中部署以下应用程序。

## PowerHA SystemMirror for AIX Standard Edition
{: #ha-dr-ha-standard}

购买 PowerHA SystemMirror for AIX Standard Edition 时，可以使用按月预订模型。有关更多信息，请参阅 [Standard Edition monthly pricing options ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/common/ssi/ShowDoc.wss?docURL=/common/ssi/rep_ca/8/897/ENUS219-288/index.html)。

购买软件后，可以从 [IBM Entitled Systems Support (ESS) ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](http://www.ibm.com/eserver/ess) 下载该软件。您可以在 {{site.data.keyword.powerSys_notm}} 环境中运行的虚拟服务器上安装 PowerHA SystemMirror for AIX。有关安装指示信息，请参阅 [Installing PowerHA SystemMirror ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/support/knowledgecenter/SSPHQG_7.2/install/ha_install.html)。

请查看以下信息，以在 {{site.data.keyword.powerSys_notm}} 环境中实现 PowerHA SystemMirror for AIX。

* 创建属于 PowerHA SystemMirror 集群的虚拟服务器时，必须从**主机托管规则**字段中选择**不同服务器**。
![显示“主机托管规则”字段](/images/hadr2.png "显示“主机托管规则”字段")

* 为属于 PowerHA SystemMirror 集群的虚拟服务器创建存储卷（磁盘）时，必须在**可共享**字段中选择**开启**。
![显示“可共享规则”字段](/images/hadr1.png "显示“可共享”字段")

* 使用 {{site.data.keyword.powerSys_notm}} 服务时，您无权访问 HMC、VIOS 和主机系统。因此，需要访问这些功能的任何 PowerHA SystemMirror 功能都不可用，例如资源优化的高可用性 (ROHA) 和活动节点中止策略 (ANHP)。

<!--* When you deploy PowerHA SystemMirror, you must verify that the Service IP address is defined as a private IP address. This Service IP address can be accessed by another {{site.data.keyword.powerSys_notm}} instance or from other {{site.data.keyword.cloud}} applications. You cannot use a public IP address because it cannot be moved from one interface to another interface within a virtual server or across different virtual servers. -->

<!--When you deploy PowerHA SystemMirror for AIX Enterprise Edition clusters in the {{site.data.keyword.powerSys_notm}} environment, you can only use the Geographic Logical Volume Manager (GLVM) functions. You cannot use storage mirroring functions that are part of PowerHA SystemMirror for AIX Enterprise Edition because you do not have access to the subsystem storage in the {{site.data.keyword.powerSys_notm}} environment. For more information, see [Geographic Logical Volume Manager ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SSPHQG_7.2/glvm/ha_glvm_kick.html).
{:note}
[Enterprise Edition monthly pricing options ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/common/ssi/cgi-bin/ssialias?infotype=AN&subtype=CA&htmlfid=897/ENUS219-286) -->

## 通过备份和复原实现业务连续性
{: #ha-dr-ha-business}

{{site.data.keyword.cloud}} 不会备份 {{site.data.keyword.powerSys_notm}} 配置和数据。

您可以使用 {{site.data.keyword.cloud_notm}} UI 将虚拟服务器备份到 {{site.data.keyword.cloud_notm}} Object Storage。如果发生严重故障，可以使用此过程来复原虚拟服务器。有关更多信息，请参阅 [Cloud Object Storage ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](/docs/services/cloud-object-storage?topic=cloud-object-storage-getting-started)。
