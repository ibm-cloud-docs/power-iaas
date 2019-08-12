---

copyright:
  years: 2019

lastupdated: "2019-03-29"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:important: .important}
{:tip: .tip}
{:faq: data-hd-content-type='faq'}

# 常见问题
{: #power-iaas-faqs}


## 支持哪些版本的 AIX 和 IBM i 操作系统？
{: #os_versions}
{: faq}

支持的 AIX 和 IBM i 版本取决于您选择的是 S922 (9009-22A) 还是 E880 (9119-MHE) 作为 {{site.data.keyword.powerSys_notm}} 的 IBM Power Systems 硬件。要查看支持的 AIX 和 IBM i 操作系统技术级别以及 Power System 硬件的列表，请参阅 [System software maps ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www-01.ibm.com/support/docview.wss?uid=ssm1maps)。

## 可以使用我自己的 AIX 或 IBM i 映像吗？
{: #image}
{: faq}

可以。此功能称为自带映像。有关自带映像的更多信息，请参阅[配置定制映像](/docs/infrastructure/power-iaas?topic=power-iaas-configuring-custom-image#configuring-custom-image)。

## IBM 会为 AIX 或 IBM i 操作系统提供维护吗？
{: #licensing_os}
{: faq}

不会。维护、更新和管理 AIX 或 IBM i 操作系统是客户的职责。

## AIX 和 IBM i 操作系统的许可是如何运作的？
{: #os_support}
{: faq}

操作系统的许可证是服务总体成本的一部分。不能使用已购买的现有许可证。

## 第三方许可是如何运作的？
{: #thridparty}
{: faq}

您负责 {{site.data.keyword.cloud_notm}} 中的第三方许可。

## 有哪些硬件规范？
{: #hardwarespecs}
{: faq}

有关硬件规范，请参阅[硬件规范](/docs/infrastructure/power-iaas?topic=power-iaas-about-power-virtual-server#apvs-hardware-specifications)。

## {{site.data.keyword.powerSys_notm}} 是在多租户环境中运行吗？
{: #multi}
{: faq}

是的。

## 有裸机选项吗？
{: #bare}
{: faq}

没有。{{site.data.keyword.powerSys_notm}} 产品的范围是专注于虚拟实例，而不是裸机。

<!-- 
## Is there a price difference between shared or dedicated cores?
{: #shared}
{: faq}

No. Performance of shared cores is almost identical to dedicated cores. However, as server utilization spikes, there might be a cache or memory latency impacts. -->
