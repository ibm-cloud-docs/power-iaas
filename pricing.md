---

copyright:
  years: 2019, 2021

lastupdated: "2021-05-18"

keywords: pricing, monthly usage, billing process, billing cycle, DLPAR, processor types, linux

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

# Pricing for Power Systems Virtual Servers
{: #pricing-virtual-server}

{{site.data.keyword.powerSys_notm}}s is offered in select regions with scale-out logical partitions (LPAR). The IBM Power Systems that can host {{site.data.keyword.powerSys_notm}}s have the following theoretical maximums:

|  Power Systems    |  Processors  |  Memory                         |
|-------------------|--------------|---------------------------------|
| E880 (9119-MHE)   |  143         | up to 7,463 GB                  |
| E980 (9080-M9S)   |  143         | up to 15,307 GB [^1] |
| S922 (9009-22A) [^2]   |  15          | up to 942 GB                    |
{: caption="Table 1. Theoretical maximum memory" caption-side="bottom"}

[^1]: In DAL12, DAL13, and TOK04 data centers, the E980 systems allow up to 23,070 GB of memory.

[^2]: If the machine type is S922 and operating system is IBM i, IBM i supports maximum of 4 cores per VM.

It's important to note that a system's theoretical maximum depends on the data center. Also, the {{site.data.keyword.powerSys_notm}} development team enforces the current available resources within each data center. With these processing maximums, the {{site.data.keyword.powerSys_notm}} service can meet any business workload requirement.
{: shortdesc}

In the Cloud catalog for {{site.data.keyword.powerSys_notm}}s, the estimated price might be different than the actual price when you purchase the {{site.data.keyword.powerSys_notm}} service or instances based on the discounts and promotion codes.

## Monthly usage
{: #pricing-monthly-usage}

{{site.data.keyword.powerSys_notm}} instances are charged at a monthly rate that is prorated per hour. If you add resources to an LPAR during the middle of the month, the monthly bill for the LPAR reflects the resource change and the LPAR price that is prorated per hour.

In the following monthly usage example, the customer purchases a {{site.data.keyword.powerSys_notm}} instance that has one core with 8 GB of memory, a 150 GB disk, and is running AIX 7200-03-02, at a base price of $250.57 per month ($0.343 per hour). As the month progresses, the customer adds more memory. The new price for the LPAR is $339.45 per month ($0.465 per hour). The monthly bill is prorated by the hour for the resources deployed.

| Hours elapsed in a month  | Amount charged                     | LPAR description                       |
| ------------------------- | ---------------------------------- | -------------------------------------- |
| 300 hours                 | (300 hours x $0.343)/month = $103      | 1 core, 8 GB memory, 150 GB disk, AIX  |
| 430 hours                 | (430 hours x $0.465)/month = $200      | 1 core, 16 GB memory, 150 GB disk, AIX |
| 730 hours (Monthly Total) | $103 + $200 = $303 (Monthly Total) | 1 core, 16 GB memory, 150 GB disk, AIX |
{: caption="Table 2. Monthly LPAR charges" caption-side="top"}

In this example, the LPAR resources are increased (after reaching 300 hours in the month) from 8 GB to 16 GB of memory. The price of the LPAR is prorated by the hour for the final monthly price of $303.

For detailed usage and billing information, you can refer to the part number in your invoice. The part numbers in the invoice represent the charge unit. Refer to the following table to view the part numbers and its corresponding description.

| Part number  | Description                     | 
| ------------------------- | ---------------------------------- |
| SOS_VIRTUAL_PROCESSOR_CORE_HOURS     | Scale out shared uncapped processor per core-hour       |
| SOD_VIRTUAL_PROCESSOR_CORE_HOURS     | Scale out dedicated processor per core-hour      |
| ES_VIRTUAL_PROCESSOR_CORE_HOURS     | E880 shared uncapped processor per core-hour      |
| ED_VIRTUAL_PROCESSOR_CORE_HOURS     | E880 dedicated processor per core-hour      |
| MS_GIGABYTE_HOURS     | RAM gigabyte-hour      |
| MHU_GIGABYTE_HOURS     | High use RAM (>64 Gb per core) gigabyte-hour      |
| TIER_ONE_STORAGE_GIGABYTE_HOURS     | Tier-1 storage gigabyte-hour      |
| TIER_THREE_STORAGE_GIGABYTE_HOURS     | Tier-3 storage gigabyte-hour     |
| AIX_SMALL_APPLICATION_INSTANCE_HOURS     | AIX scale out license per core-hour      |
| AIX_MEDIUM_APPLICATION_INSTANCE_HOURS     | AIX enterprise license per core-hour     |
| IBMI_OS_PTEN_APPLICATION_INSTANCE_HOURS     | IBM i OS P10 license per core-hour      |
| IBMI_OS_PTHIRTY_APPLICATION_INSTANCE_HOURS     | IBM i OS P30 license per core-hour      |
| IBMI_LPP_PTEN_APPLICATION_INSTANCE_HOURS     | IBM i LPP P10 license per core-hour      |
| IBMI_LPP_PTHIRTY_APPLICATION_INSTANCE_HOURS     | IBM i LPP P30 license per core-hour     |
| SOC_VIRTUAL_PROCESSOR_CORE_HOURS     | Scale out shared capped processor per core-hour      |
| EC_VIRTUAL_PROCESSOR_CORE_HOURS     | E880 Enterprise shared capped processor per core-hour      |
| IBMIHA_PTEN_APPLICATION_INSTANCES     | PowerHA for IBM i P10 license per core-hour      |
| IBMIHA_PTHIRTY_APPLICATION_INSTANCES     | PowerHA for IBM i P30 license per core-hour      |
| IBMICOS_APPLICATION_INSTANCES     | IBM Cloud Storage Solutions for IBM i license per core-hour      |
| IBMIRDS_APPLICATION_INSTANCES     | IBM Rational Development Studio for IBM i license per users-hour      |
| IBMI_DBIIWQ_APPLICATION_INSTANCE_HOURS     | IBM Db2 Web Query for i core-hour      |
| BHHANA_APPLICATION_INSTANCE_HOURS     | Balanced for Online analytical processing (OLAP) HANA application instance hour       |
| COREHANA_APPLICATION_INSTANCE_HOURS     | Core HANA application instance hour      |
| MEMHANA_APPLICATION_INSTANCE_HOURS     | Memory HANA application instance hour      |
| UMHHANA_APPLICATION_INSTANCE_HOURS     | Ultra Memory HANA for Online analytical processing (OLAP) application instance hour      |
| IBMIOS_PTEN_MOL_APPLICATION_INSTANCE_HOURS     | Movable IBM i P10 license per core-hour      |
| IBMIOS_PTHIRTY_MOL_APPLICATION_INSTANCE_HOURS     | Movable IBM i P30 license per core-hour      |
| IBMILPP_PTEN_MOL_APPLICATION_INSTANCE_HOURS     | Movable IBM i LPP P10 license per core-hour      |
| IBMILPP_PTHIRTY_MOL_APPLICATION_INSTANCE_HOURS     | Movable IBM i LPP P30 license per core-hour      |
| ESS_VIRTUAL_PROCESSOR_CORE_HOURS     | E980 shared uncapped processor per core-hour      |
| ECC_VIRTUAL_PROCESSOR_CORE_HOURS     | E980 shared capped processor per core-hour      |
| EDD_VIRTUAL_PROCESSOR_CORE_HOURS     | E980 dedicated virtual processor per core-hour      |
| IBM_I_OS_PTEN_SRVC_EXT_PER_PROC_CORE_HR     | IBM i OS P10 service extension per core-hour      |
| IBM_I_SERVICE_EXTENSION_PER_CORE_HOUR     | IBM i OS P30 service extension per core-hour      |


## Base instances
{: #pricing-base-instance-prices}

The base instance billing depends on your virtual instance options when you create a {{site.data.keyword.powerSys_notm}}. The machine type, number of cores, and amount of memory all affect the base instance billing. When you create your virtual server instance, the associated monthly rate is displayed. For more information, see [Creating a Power Systems Virtual Server](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#creating-power-virtual-server).

The pricing for memory is calculated based on a ratio of 64 GB per core. For example, if you use more than 16 GB for 0.25 cores, you must pay a premium high-use RAM price for the excess memory. However, if you use up to 128 GB for 2 cores, you do not have to pay any premium memory price.

## Operating systems
{: #pricing-operating-systems}

The {{site.data.keyword.powerSys_notm}} pricing for AIX and IBM i includes license and IBM software maintenance.

The {{site.data.keyword.powerSys_notm}} service provides AIX and IBM i stock images. The operating system version levels of the stock images are subject to change.

You can also bring your own custom image to use on a {{site.data.keyword.powerSys_notm}} instance, but you must still purchase an operating system license for virtual server resources. If you bring your own custom image, you are charged for the image size and the storage tier that you use for the image. After you deploy a stock image (and only after deployment), you are charged for the space the image is stored in. The storage unit price (per GB) for the stored boot images is same as the selected storage tier (Tier 0 or Tier 3) where your boot disks are deployed. To identify the estimated storage rates, use the Cost Estimator tool. To reduce costs you can capture the virtual machine and delete when it is not needed. The pricing for AIX and IBM i operating system license is not determined by whether you use a custom image or a stock image. To learn more, go to [Deploying a custom image within a Power Systems Virtual Server](/docs/power-iaas?topic=power-iaas-deploy-custom-image).

The {{site.data.keyword.powerSys_notm}} service does not provide Linux stock images. You must bring your own Linux image (OVA format) and subscription. Both Red Hat Linux Enterprise (RHEL) and SUSE Linux Enterprise Server (SLES) OVA images are supported.

## Processor types
{: #pricing-processor}

You are charged different rates depending on the processor type you choose for your virtual machine (VM). **Dedicated processors** are priced the highest as they provide the best overall performance. **Shared capped processors** cost slightly more than **shared uncapped processors** because of their flexibility in addressing licensing restrictions. The processors are all charged on an hourly prorated basis according to the machine type, processor type, and the number of cores used in a month.

Each processor has a different hourly rate depending on its type (**Dedicated** vs **Uncapped shared**). Processors also have a different hourly rate depending on the system that they are on **(Dedicated S922** vs **Dedicated E880/E980**). For information on different processor type functions, see [What's the difference between capped and uncapped shared processor performance?How do they compare to dedicated processor performance?](/docs/power-iaas?topic=power-iaas-power-iaas-faqs#processor).

The following tables show how different processor types affect the cost per system:

| Number of cores (S922) | Hourly rate (Processor type) | Monthly cost (730 hours) |
| ---------------------- | ---------------------------- | ------------------------ |
| 1                      | $0.64 (dedicated)            | $353.028                  |
| 1                      | $0.28 (uncapped shared)      | $88.257                  |
| 1                      | $0.34 (capped shared)        | $132.422                  |
{: caption="Table 1. S922 processor type pricing" caption-side="bottom"}

<br>

| Number of cores (E880) | Hourly rate (Processor type) | Monthly cost (730 hours) |
| --------------------------- | ---------------------------- | ------------------------ |
| 1                           | $1.52 (dedicated)            | $950.533                 |
| 1                           | $0.54 (uncapped shared)      | $237.615                  |
| 1                           | $0.70 (capped shared)        | $356.459                  |
{: caption="Table 2. E880 processor type pricing" caption-side="bottom"}

<br>

| Number of cores (E980) | Hourly rate (Processor type) | Monthly cost (730 hours) |
| --------------------------- | ---------------------------- | ------------------------ |
| 1                           | $1.91 (dedicated)            | $1235.671                 |
| 1                           | $0.64 (uncapped shared)      | $308.936                  |
| 1                           | $0.85 (capped shared)        | $463.404                  |
{: caption="Table 3. EE980 processor type pricing" caption-side="bottom"}

## End of billing
{: #pricing-end-billing}

The monthly billing cycle ends when you delete the LPAR. If you scale your infrastructure up and down in response to workload requirements, your billing follows the timing of the LPAR provision change. If you stop the LPAR, the billing process is not stopped. You must delete the LPAR to stop the billing cycle.

You are still charged if the VM is in a *suspended state*. When your VM is inactive, you can use Dynamic Logical Partitioning (DLPAR) to resize it to a minimal state. You can drastically decrease the price per hour by reducing the VM's core count and memory.
{: important}
