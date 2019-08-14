---

copyright:
  years: 2019

lastupdated: "2019-06-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}

# Power Systems Virtual Server on IBM Cloud 定价
{: #pricing-virtual-server}

{{site.data.keyword.powerSysFull}} 在精选区域中提供，对于横向扩展的逻辑分区 (LPAR)，最多可有 15 个核心，320 GB 内存；此外对于企业 LPAR，最多可有 143 个核心和 8192 GB 内存。通过这些选项，{{site.data.keyword.powerSys_notm}} 可以满足您业务的任何工作负载需求。将按每月费率向您计费。
{:shortdesc}

## 每月使用情况
{: #pricing-monthly-usage}

{{site.data.keyword.powerSys_notm}} 实例按每月费率收费（按比例以小时计算）。如果在月中将资源添加到 LPAR，那么该 LPAR 的每月帐单将反映出资源更改以及按比例以小时计算的 LPAR 价格。

### 每月使用情况示例
{: #pricing-monthly-usage-example}

在以下示例中，您购买的 {{site.data.keyword.powerSys_notm}} 实例具有 1 个核心，8 GB 内存，150 GB 磁盘，运行的是 AIX 7200-03-02，基础价格为 250.57 美元/月（0.343 美元/小时）。在该月后面的时间，您添加了更多内存。LPAR 的新价格为 339.45 美元/月（0.465 美元/小时）。所部署资源的每月帐单将按比例以小时计算。

|一个月内耗用的小时数|收费金额|LPAR 描述|
| ----------------------------- | ----------------- | --------------------  |
|300 小时|300 小时 x 251 美元/月 = 103 美元|1 个核心，8 GB 内存，150 GB 磁盘，AIX|
|430 小时|430 小时 x 339 美元/月 = 200 美元|1 个核心，16 GB 内存，150 GB 磁盘，AIX|
|730 小时（每月总计）|103 美元 + 200 美元 = 303 美元（每月总计）|1 个核心，16 GB 内存，150 GB 磁盘，AIX|
{: caption="表 1. 每月 LPAR 费用示例" caption-side="top"}

在此示例中，LPAR 资源在该月使用 300 小时后从 8 GB 内存增加到 16 GB 内存。LPAR 的价格按比例以小时计算，得出 LPAR 的最终每月价格（303 美元）。

## 基础实例价格
{: #pricing-base-instance-prices}

基础实例计费取决于在创建 {{site.data.keyword.powerSys_notm}} 时选择的选项，例如机器类型、核心数和内存量。创建虚拟服务器实例时，将显示关联的每月费率。有关更多信息，请参阅[创建 {{site.data.keyword.powerSys_notm}}](/docs/infrastructure/power-iaas?topic=power-iaas-creating-power-virtual-server#creating-power-virtual-server)。

## 操作系统
{: #pricing-operating-systems}

下面是 IBM 提供的库存映像：
* AIX
  * 7200-03-02
  * 7100-05-03

* IBM i
  * 7.3 TR5
  * 7.2 TR9

您可以在 {{site.data.keyword.powerSys_notm}} 实例上使用自带定制映像，但仍会向 IBM Cloud 购买操作系统许可证。不能将现有 AIX 或 IBM i 许可证用于 {{site.data.keyword.powerSys_notm}} 实例中的 LPAR。如果使用定制映像或库存映像，将以相同价格收费。有关更多信息，请参阅[配置定制映像](/docs/infrastructure/power-iaas?topic=power-iaas-configuring-custom-image#configuring-custom-image)。

## 计费结束
{: #pricing-end-of-billing}

删除 LPAR 时，每月计费周期即结束。如果扩展和缩减基础架构以响应工作负载需求，那么计费会根据 LPAR 供应更改的时间进行计算。如果停止 LPAR，计费流程并不会停止。必须删除 LPAR 才能停止计费周期。
