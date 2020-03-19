---

copyright:
  years: 2019, 2020

lastupdated: "2020-03-19"

keywords: pricing, monthly usage, billing process, billing cycle, DLPAR, processor

subcollection: power-iaas

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}

# Pricing for Power Systems Virtual Servers on IBM Cloud
{: #pricing-virtual-server}

{{site.data.keyword.powerSysFull}} is offered in select regions with scale-out logical partitions (LPAR). The {{site.data.keyword.powerSys_notm}} systems have the following theoretical maximums:

- E880 (9119-MHE): 155 processors and 8,099 GB of memory
- E980 (9080-M9S): 155 processors and 16,255 GB of memory
- S922 (9009-22A): 15 processors and 959 GB of memory

It's important to note that a system's theoretical maximum depends on the data center. Also, the {{site.data.keyword.powerSys_notm}} development team enforces the current available resources within each data center. With these processing maximums, the {{site.data.keyword.powerSys_notm}} service can meet any business workload requirement. You are billed at a monthly rate.
{: shortdesc}

## Monthly usage
{: #pricing-monthly-usage}

{{site.data.keyword.powerSys_notm}} instances are charged at a monthly rate that is pro-rated per hour. If you add resources to an LPAR during the middle of a month, the monthly bill for the LPAR reflects the resource change and the LPAR price that is pro-rated per hour.

In the following monthly usage example, the customer purchases a {{site.data.keyword.powerSys_notm}} instance that has one core with 8 GB of memory, a 150 GB disk, and is running AIX 7200-03-02, at a base price of $250.57 per month ($0.343 per hour). As the month progresses, the customer adds more memory. The new price for the LPAR is $339.45 per month ($0.465 per hour). The monthly bill is pro-rated by the hour for the resources deployed.

| Hours elapsed in a month       | Amount charged   |  LPAR description     |
| ----------------------------- | ----------------- | --------------------  |
| 300 hours        | 300 hours x $251/month = $103  | 1 core, 8 GB memory, 150 GB disk, AIX    |
| 430 hours        | 430 hours x $339/month = $200  | 1 core, 16 GB memory, 150 GB disk, AIX  |
| 730 hours (Monthly Total)  | $103 + $200 = $303 (Monthly Total)  |   1 core, 16 GB memory, 150 GB disk, AIX |
{: caption="Table 1. Monthly LPAR charges example" caption-side="top"}

In this example, the LPAR resources are increased after the 300 hour of the month from 8 GB of memory to 16 GB of memory. The price of the LPAR is prorated by the hour for the final monthly price of the LPAR ($303).

## Base instance prices
{: #pricing-base-instance-prices}

The base instance billing depends on your virtual instance options when you create a {{site.data.keyword.powerSys_notm}}. The machine type, number of cores, and amount of memory all affect the base instance billing. When you create your virtual server instance, the associated monthly rate is displayed. For more information, see [Creating a {{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#creating-power-virtual-server).

## Operating systems
{: #pricing-operating-systems}

IBM provides AIX and IBM i stock images. The operating system version levels of the stock images are subject to change.

You can also bring your own custom image to use on a {{site.data.keyword.powerSys_notm}} instance, but you must still purchase an operating system license for IBM Cloud. You cannot use an existing AIX or IBM i license for LPARs in a {{site.data.keyword.powerSys_notm}} instance. If you use a custom image or a stock image, you are charged the same price. For more information, see [Deploying a custom image within a Power Systems Virtual Server](/docs/power-iaas?topic=power-iaas-deploy-custom-image).

## Processor type
{: #pricing-processor}



## End of billing
{: #pricing-end-billing}

The monthly billing cycle ends when you delete the LPAR. If you scale your infrastructure up and down in response to workload requirements, your billing follows the timing of the LPAR provision change. If you stop the LPAR, the billing process is not stopped. You must delete the LPAR to stop the billing cycle.

You are still charged if the VM is in a *suspended state*. When your VM is inactive, you can use Dynamic Logical Partitioning (DLPAR) to resize it to a minimal state. You can drastically decrease the price per hour by reducing the VM's core count and memory.
{: important}
