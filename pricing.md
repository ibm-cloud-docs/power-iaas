---

copyright:
  years: 2019

lastupdated: "2019-05-17"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}

# Pricing for Power Systems Virtual Server on IBM Cloud
{: #pricing-virtual-server}

{{site.data.keyword.powerSysFull}} is offered in select regions with up to 150 Cores and 9600 GB of memory to fit any workload requirements. You are billed at an hourly rate.
{:shortdesc}

## Sustained usage
{: #pricing-sustained-usage}

Although {{site.data.keyword.powerSys_notm}} instances are charged at an hourly rate, the longer you use the instance the larger discount you receive. The following rates help take the guess work out of determining how long you want the instance to run for a month. As the billing month progresses, you receive the following hourly discounts.

| Time elapsed in a month       | Billing discount  |
| ----------------------------- | ----------------- |
| 0-20%                         | regular retail rate |
| 21-40%                        | 5%        |
| 41-60%                        | 10%       |
| 61-80%                        | 15%        |
| 81-100%                       | 20% |
{: caption="Table 1. Tiered discounts" caption-side="top"}

The discounted tiers provide you with a 10% savings for keeping instances that are running monthly versus hourly. This discount applies to only compute and software hourly rates, and it doesn't apply to storage, network, or other charges.

The usage rates are reset to 0% at the beginning of every month.
{:note}

### Sustained usage example
In this example, you purchase an instance that has 2 cores and 64 GB RAM, at a base price of $0.795 per hour. As the month progresses, your rate decreases as follows:

| Time elapsed in a month       | Billing discount  |  Example rate     |
| ----------------------------- | ----------------- | -------- |
| 0-20%                         | regular retail rate ($.795) | $1.46    |
| 21-40%                        | 5%        |   $1.39   |
| 41-60%                        | 10%       |    $1.25  |
| 61-80%                        | 15%        |    $1.06 |
| 81-100%                       | 20% |       $.85      |
{: caption="Table 2. Tiered discounts example" caption-side="top"}

In this usage example, if you leave the {{site.data.keyword.powerSys_notm}} instance running for the entire month, your total bill would be $962.53. The discounts result in a monthly savings of 10%, compared to the hourly rate.

## Base instance prices
{: #pricing-base-instance-prices}

The base instance billing depends on the options, such as machine type, number of cores, and amount of memory that you select when you are creating a {{site.data.keyword.powerSys_notm}}. When you create your virtual server instance, the associated hourly rate is displayed. The hourly rate changes dynamically depending on the options that you select. For more information, see [Creating a {{site.data.keyword.powerSys_notm}}](/docs/infrastructure/power-iaas?topic=power-iaas-creating-power-virtual-server#creating-power-virtual-server).

## Operating systems
{: #pricing-operating-systems}

The following are the stock images that are provided to you by IBM:
* AIX
  * 7200-03-02
  * 7100-05-03

* IBM i
  * 7.3 TR5
  * 7.2 TR9

You can bring your own custom image to use on a {{site.data.keyword.powerSys_notm}}. For more information, see [Configuring a custom image](/docs/infrastructure/power-iaas?topic=power-iaas-configuring-custom-image#configuring-custom-image).

If you use a stock or custom image, the cost of the operating system license is covered by the hourly rate. You cannot transfer operating system licenses to a {{site.data.keyword.powerSys_notm}}.
{:note}

## End of billing
{: #pricing-end-of-billing}

When the Power Systems Hardware is returned, the billing is stopped. If you scale your infrastructure up and down in response to workload requirements, your billing follows the timing of the logical partition (LPAR) provision change. If you stop the LPAR, the billing process is not stopped.