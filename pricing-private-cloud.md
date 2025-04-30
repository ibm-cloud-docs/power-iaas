---

copyright:
  years: 2024

lastupdated: "2025-04-29"

keywords: pricing, {{site.data.keyword.powerSys_notm}}, private cloud, before you begin, terminology, video, how-to, pricing for private cloud, monthly usage, storage type, memory type

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Pricing for {{site.data.keyword.on-prem-fname}}
{: #pricing-private-cloud}

----



{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}


----

The {{site.data.keyword.powerSysFull}} in {{site.data.keyword.on-prem}} provides secure and unified billing for using the hardware and software resources. The following list of hardware resources is metered:

- Virtual machines: The CPU (in cores), with processor modes (capped, shared, dedicated), and memory (in GB).

- Volumes: Volume (in GB).

- Snapshots: Snapshots (in GB).

For more information about billing for operating systems, see [Operating systems](/docs/power-iaas?topic=power-iaas-pricing-private-cloud#operating-systems).

In the IBM Cloud catalog for {{site.data.keyword.on-prem-fname}}, the estimated price might differ from the actual price when you purchase the {{site.data.keyword.on-prem-fname}} infrastructure or instances. The actual price might include the discounts and promotion codes.


For more information about IBM Cloud regions that can host connections from the pods for {{site.data.keyword.on-prem-fname}}, see [IBM Satellite location](/docs/power-iaas?topic=power-iaas-satellite-location-spec-private-cloud).


## Monthly usage
{: #monthly-usage}

{{site.data.keyword.on-prem-fname}} instances are charged at a monthly rate that is prorated per hour. If you add resources to a virtual machine in the middle of the month, the bill for the virtual machine reflects the resource change at a per-hour prorated price.

All prices that are mentioned in the topic are illustrative and do not represent the actual amounts that are used for billing. To generate an estimated price, use the [{{site.data.keyword.powerSys_notm}} Estimate pricing](https://cloud.ibm.com/power/estimate){: external} tool. For more information, see [Generating an estimate](/docs/power-iaas?topic=power-iaas-generating-an-estimate).
{: important}

In the following example, the customer provisions an {{site.data.keyword.on-prem-fname}} instance. The instance has 1 core with 8 GB of memory, a 150 GB disk, and is running Red Hat Enterprise Linux (RHEL) operating system (OS).
Assume the following hypothetical monthly prices:
* Cores: $143.23/month x 1 = $143.23
* Memory: $9/month each GB x 8 = $ 72.00
* Storage: $0.216/month each GB x 150 GB = $ 32.40
* OS license: $43.80/month each core   = $ 43.80

**Total cost per month**     = $291.43

Factoring the example quantities and prices, the base price for the virtual machine is $291.43 per month or an average of $0.399 per hour for all the resources consumed. Assume that in the course of the month, the customer allocates more memory to the virtual machine. At the end of the month, the new price for the virtual machine is higher to account for the extra memory. The new price amounts to $0.498 per hour for all the resources consumed. The monthly bill is prorated by an hour for the resources that are deployed as shown in Table 1.

In Table 1, the virtual machine resources are increased (after the resources reach 300 hours in the month) from 8 GB to 16 GB of memory. The price of the virtual machine is prorated by an hour for the final monthly price of $303.

| Hours elapsed in a month   | Amount charged                               |  Virtual machine description    |
| -------------------------- | -------------------------------------------- |  --------------------------------------- |
| 300 hours                  | (300 hours x $0.399)/month = $119.70         |  1 core, 8 GB memory, 150 GB disk, RHEL  |
| 430 hours                  | (430 hours x $0.498)/month = $214.14         |  1 core, 16 GB memory, 150 GB disk, RHEL |
| 730 hours (Monthly Total)  | $119.70 + $214.14 = $333.84 (Monthly Total)  |  1 core, 16 GB memory, 150 GB disk, RHEL |
{: caption="An example of monthly charges for a virtual machine" caption-side="bottom"}

For the example in Table 1, we might see four distinct part numbers for the following resources in the invoice:
* The virtual cores (one for each core)
* The memory
* The volume storage (disk)
* The OS license (RHEL)



For detailed usage and billing information, refer to the part numbers in your invoice. The part numbers in the invoice represent the charge unit for each resource charged. Refer to the following table to view the part number descriptions and the associated metric IDs.







|  Part description (visible on the invoice from IBM)              | Metric ID (visible in the IBM Cloud catalog) |
|  --------------------------------------------------------------- | ---------------------------------------------- |
| **IBM Power Systems Virtual Server virtual machine group**       |                                                |
| IBM Power Systems E1080 virtual processor core hour - capped     | ppcaas-metric-E1080-cores-capped |
| IBM Power Systems E1080 virtual processor core hour - dedicated  | ppcaas-metric-E1080-cores-dedicated |
| IBM Power Systems E1080 virtual processor core hour - shared     | ppcaas-metric-E1080-cores-shared |
| IBM Power Systems E1050 virtual processor core hour - capped     | ppcaas-metric-E1050-cores-capped |
| IBM Power Systems E1050 virtual processor core hour - dedicated  | ppcaas-metric-E1050-cores-dedicated |
| IBM Power Systems E1050 virtual processor core hour - shared     | ppcaas-metric-E1050-cores-shared |
| IBM Power Systems S1022 virtual processor core hour - capped     | ppcaas-metric-S1022-cores-capped |
| IBM Power Systems S1022 virtual processor core hour - dedicated  | ppcaas-metric-S1022-cores-dedicated |
| IBM Power Systems S1022 virtual processor core hour - shared     | ppcaas-metric-S1022-cores-shared |
| IBM Power Systems scale-out memory gigabyte hours                | ppcaas-metric-p10-2u-memory-standard |
| IBM Power Systems scale-up memory gigabyte hours                 | ppcaas-metric-p10-4u-memory-standard |
| IBM Power Systems E1080 virtual processor core hour - capped - SAP HANA workload  | ppcaas-metric-E1080-hana-cores-capped |
| IBM Power Systems E1080 virtual processor core hour - dedicated - SAP HANA workload  | ppcaas-metric-E1080-hana-cores-dedicated |
| IBM Power Systems E1080 virtual processor core hour - shared - SAP HANA workload     | ppcaas-metric-E1080-hana-cores-shared |
| IBM Power Systems E1050 virtual processor core hour - capped - SAP HANA workload     | ppcaas-metric-E1050-hana-cores-capped |
| IBM Power Systems E1050 virtual processor core hour - dedicated - SAP HANA workload  | ppcaas-metric-E1050-hana-cores-dedicated |
| IBM Power Systems E1050 virtual processor core hour - shared - SAP HANA workload     | ppcaas-metric-E1050-hana-cores-shared |
| IBM Power Systems S1022 virtual processor core hour - capped - SAP HANA workload     | ppcaas-metric-S1022-hana-cores-capped |
| IBM Power Systems S1022 virtual processor core hour - dedicated - SAP HANA workload  | ppcaas-metric-S1022-hana-cores-dedicated |
| IBM Power Systems S1022 virtual processor core hour - shared - SAP HANA workload     | ppcaas-metric-S1022-hana-cores-shared |
| IBM Power Systems scale-out memory gigabyte hours - SAP HANA workload  | ppcaas-metric-p10-2u-hanamem-standard |
| IBM Power Systems scale-up memory gigabyte hours - SAP HANA workload  | ppcaas-metric-p10-4u-hanamem-standard |
| AIX operating system scale-up license core-hour | ppcaas-metric-aix-scale-up |
| AIX operating system scale-out license core-hour | ppcaas-metric-aix-scale-out |
| Red Hat Enterprise Linux operating system scale-up license core-hour | ppcaas-metric-rhel-scale-up |
| Red Hat Enterprise Linux operating system scale-out license core-hour | ppcaas-metric-rhel-scale-out |
| Red Hat Enterprise Linux operating system scale-up license core-hour - SAP workload  | ppcaas-metric-rhel-sap-scale-up |
| Red Hat Enterprise Linux operating system scale-out license core-hour - SAP workload  | ppcaas-metric-rhel-sap-scale-out |
| SUSE Linux Enterprise Server operating system tier 1 instance-hour | ppcaas-metric-sles-tier1 |
| SUSE Linux Enterprise Server operating system tier 2 instance-hour | ppcaas-metric-sles-tier2 |
| SUSE Linux Enterprise Server operating system tier 3 instance-hour | ppcaas-metric-sles-tier3 |
| SUSE Linux Enterprise Server operating system tier 1 instance-hour - SAP workload  | ppcaas-metric-sles-sap-tier1 |
| SUSE Linux Enterprise Server operating system tier 2 instance-hour - SAP workload  | ppcaas-metric-sles-sap-tier2 |
| SUSE Linux Enterprise Server operating system tier 3 instance-hour - SAP workload  | ppcaas-metric-sles-sap-tier3 |
| IBM i operating system P10 license core-hour | ppcaas-metric-ibmi-os-p10 |
| IBM i operating system P30 license core-hour | ppcaas-metric-ibmi-os-p30 |
| IBM i operating system P10 service extension core-hour | ppcaas-metric-ibmi-os-p10-sve |
| IBM i operating system P30 service extension core-hour | ppcaas-metric-ibmi-os-p30-sve |
| IBM i LPP P10 license core-hour | ppcaas-metric-ibmi-lpp-p10 |
| IBM i LPP P30 license core-hour | ppcaas-metric-ibmi-lpp-p30 |
| IBM i P10 PowerHA instance core-hour | ppcaas-metric-ibmi-pha-p10 |
| IBM i P30 PowerHA instance core-hour | ppcaas-metric-ibmi-pha-p30 |
| IBM i Cloud Storage Solutions instance core-hour | ppcaas-metric-ibmi-cos |
| IBM i Rational Developer Studio instance core-hour| ppcaas-metric-ibmi-rds |
| Virtual Tape Library terabyte-hour | ppcaas-metric-vtl |
{: class="simple-tab-table"}
{: tab-group="part_number_descriptions_private"}
{: caption="Part number descriptions for {{site.data.keyword.on-prem-fname}} in {{site.data.keyword.on-prem}}." caption-side="bottom"}
{: #virtual-machine-group-private}
{: tab-title="Virtual machine group"}


|  Part description (visible on the invoice from IBM)              | Metric ID (visible in the IBM Cloud catalog) |
|  --------------------------------------------------------------- | ---------------------------------------------- |
| **IBM Power Systems Virtual Server Private Cloud volume group**  |
| Volume Storage Tier 0 gigabyte-hour  | ppcaas-metric-volume-tier0 |
| Volume Storage Tier 1 gigabyte-hour  | ppcaas-metric-volume-tier1 |
| Volume Storage Tier 3 gigabyte-hour  | ppcaas-metric-volume-tier3 |
| Volume Storage Tier 5k gigabyte-hour | ppcaas-metric-volume-tier5k |
{: class="simple-tab-table"}
{: tab-group="part_number_descriptions_private"}
{: caption="Part number descriptions for {{site.data.keyword.on-prem-fname}} in {{site.data.keyword.on-prem}}." caption-side="bottom"}
{: #volume-group-private}
{: tab-title="Volume group"}


|  Part description (visible on the invoice from IBM)              | Metric ID (visible in the IBM Cloud catalog) |
|  --------------------------------------------------------------- | ---------------------------------------------- |
| **IBM Power Systems Virtual Server Private Cloud snapshot group**  |
| Snapshot Storage Tier 0 gigabyte-hour  | ppcaas-metric-snapshot-tier0 |
| Snapshot Storage Tier 1 gigabyte-hour  | ppcaas-metric-snapshot-tier1 |
| Snapshot Storage Tier 3 gigabyte-hour  | ppcaas-metric-snapshot-tier3 |
| Snapshot Storage Tier 5k gigabyte-hour | ppcaas-metric-snapshot-tier5k |
{: class="simple-tab-table"}
{: tab-group="part_number_descriptions_private"}
{: caption="Part number descriptions for {{site.data.keyword.on-prem-fname}} in {{site.data.keyword.on-prem}}." caption-side="bottom"}
{: #snapshot-group-private}
{: tab-title="Snapshot group"}


|  Part description (visible on the invoice from IBM)              | Metric ID (visible in the IBM Cloud catalog) |
|  --------------------------------------------------------------- | ---------------------------------------------- |
| **IBM Power Systems Virtual Server Private Cloud shared processor pool group** |             |
|  IBM Power Systems S1022 virtual processor core-hour - Shared Processor Pool | ppcaas-metric-S1022-spp-cores |
| IBM Power Systems E1050 virtual processor core-hour - Shared Processor Pool | ppcaas-metric-E1050-spp-cores |
| IBM Power Systems E1080 virtual processor core-hour - Shared Processor Pool | ppcaas-metric-E1080-spp-cores  |
{: class="simple-tab-table"}
{: tab-group="part_number_descriptions_private"}
{: caption="Part number descriptions for {{site.data.keyword.on-prem-fname}} in {{site.data.keyword.on-prem}}." caption-side="bottom"}
{: #shared-procesor-pool-group-private}
{: tab-title="Shared Processor Pool group"}







For more information about unit prices for each metric ID, see [Where can I find the unit prices for the billing metrics?](#billing-metrics).




## Base instances
{: #base-instances}

The billing of a base instance depends on the options that you select when you create a virtual machine. The machine type, number of cores, and amount of memory affect the base instance billing. When you create your virtual machine, the associated monthly rate is displayed on the billing of the base instances.

The pricing for memory is calculated based on a ratio of 64 GB per core. For example, if you use more than 16 GB for 0.25 cores, you must pay a premium high-use RAM price for the excess memory. However, if you use up to 128 GB for 2 cores, you do not have to pay any premium memory price.

## Operating systems
{: #operating-systems}

Linux and AIX operating systems are supported and only RHEL stock images are available. For more information about supported versions and distributions, see [Full Linux subscription for Power Virtual Server in {{site.data.keyword.on-prem}}](/docs/power-iaas?topic=power-iaas-full-linux-sub). When you select a RHEL Linux stock image, the pricing includes the full Linux subscription charges. By using the Full Linux subscription, you can subscribe to an updated or upgraded package from a Red Hat Satellite server by configuring the provisioned virtual machine. The usage meter for RHEL full Linux subscription starts when you create the virtual machine. If you Bring Your Own License (BYOL), it is not metered or billed.

If you bring your own custom image, you are charged for the image size and the storage tier that you use for the custom image. After you deploy a stock image (and only after deployment), you are charged for the space that is used to store the stock image. The storage unit price (per GB) for the stored boot images is the same as the selected storage tier (Tier 0, Tier 1, or Tier 3) where your boot disks are deployed. To estimate the storage rates, use the [{{site.data.keyword.powerSys_notm}} Estimate pricing](https://cloud.ibm.com/power/estimate){: external} tool. To reduce costs, select the virtual machine that is not needed and delete it.


## Processor types
{: #processor-types}

Depending on the type of system that you choose for your virtual machine, you are charged different rates. Enterprise systems, such as E1080 or E1050, cost more because they provide more processing capacity per core. For example, the E1080 costs more than the E1050.

You can choose one of the following core types for your workload:
* **Dedicated virtual processor cores**
* **Shared capped virtual processor cores**
* **Shared uncapped virtual processor cores**

Different scenarios provide different benefits when you use each type of virtual processor core.

All prices that are mentioned in the topic are illustrative and do not represent the actual amounts that are used for billing. To generate an estimated price, use the [{{site.data.keyword.powerSys_notm}} Estimate pricing](https://cloud.ibm.com/power/estimate){: external} tool. For more information, see [Generating an estimate](/docs/power-iaas?topic=power-iaas-generating-an-estimate).
{: important}

In the following example, assume that the cost of different types of virtual processor cores is the same within each system type they belong to.

Tables 3 to 5 show how different processor types affect the cost per system:

| Number of cores (S1022)  | Hourly rate (Processor type)  | Monthly cost (730 hours)  |
|  ----------------------  | ----------------------------  | ------------------------  |
|  1                       | $0.1962 (dedicated)           | $143.23                  |
|  1                       | $0.1962 (shared uncapped)     | $143.23                  |
|  1                       | $0.1962 (shared capped)       | $143.23                  |
{: caption="S1022 processor type pricing" caption-side="bottom"}

| Number of cores (E1080)  | Hourly rate (Processor type)  | Monthly cost (730 hours)  |
|  ----------------------  | ----------------------------  | ------------------------  |
|  1                       | $0.6866 (dedicated)           | $501.20                   |
|  1                       | $0.6866 (shared uncapped)     | $501.20                   |
|  1                       | $0.6866 (shared capped)       | $501.20                   |
{: caption="E1080 processor type pricing" caption-side="bottom"}

| Number of cores (E1050)  | Hourly rate (Processor type)  | Monthly cost (730 hours)  |
|  ----------------------  | ----------------------------  | ------------------------  |
|  1                       | $0.2945 (dedicated)           | $215.00                   |
|  1                       | $0.2945 (shared uncapped)     | $215.00                   |
|  1                       | $0.2945 (shared capped)       | $215.00                   |
{: caption="E1050 processor type pricing" caption-side="bottom"}



## Memory types
{: #memory-types}

Charges for {{site.data.keyword.on-prem-fname}} are determined by the memory usage (in gigabytes), and the type of the system chosen for the virtual machine. Enterprise systems, such as E1080 or E1050, use scale-up memory with higher density, whereas S1022 systems use scale-up memory with lesser density. Currently, both scale-up and scale-out memory might cost you the same price. However, this pricing is subject to change in the future, depending on the cost of the memory chips. Table 6 shows how memory types affect the cost per system:

| Number of GBs |  Memory type                      | Hourly rate (Processor type)  | Monthly cost (730 hours)  |
| ---------------- | ----------------------------------  | -----------------------  | ------------------------  |
|  1               | IBM Power Systems scale-out memory  | $0.01232877              | $9.00                     |
|  1               | IBM Power Systems scale-up memory   | $0.01232877              | $9.00                     |
{: caption="Memory type pricing" caption-side="bottom"}





## Pricing for shared processor pool
{: #pricing-spp-private-cloud}






Shared Processor Pool (SPP) metering is optimized to improve the Total Cost of Ownership (TCO) for AIX and IBM i software licensing and DR scenarios. Virtual servers that are configured within an SPP do not incur additional cost for per VM core.




In the {{site.data.keyword.on-prem-fname}} environment, a minimum core-to-virtual core ratio of 1:20 exists. This ratio stipulates the relationship between physical cores and virtual cores within the cloud infrastructure. Therefore, the calculation of the operating system license charges follows a distinct method within the {{site.data.keyword.on-prem-fname}} setup to accommodate the core-to-virtual core ratio efficiently.

{{_include-segments/spp-pricing-JIRA-18311.md}}

When you use SPP in {{site.data.keyword.on-prem-fname}}, you pay for the following items:

* The maximum capacity of the SPP reserved cores that use the shared capped part number.
* The entitled capacity of the shared capped or uncapped part numbers when virtual server instance cores are deployed into the SPP. This amount is variable and depends on the entitled capacity.
* The operating system license, which is based on the following types of virtual server instances:
    * Capped SPP: pricing is determined by the entitled capacity.
    * Uncapped SPP: pricing is determined by the minimum value between the total number of virtual processors and the maximum capacity of the SPP. To get the total number of virtual processors, count the number of virtual processors that are associated with the partitions in an SPP for each type of operating system such as AIX or IBM i.

Table 12 shows the details of SPP in {{site.data.keyword.on-prem-fname}}.




| Solution  | Core-to-virtual core ratio  | Core Pricing  | OS license pricing |
| -----------------  | -----------  | ------------  | ------------------ |
| {{site.data.keyword.on-prem-fname}}	User-defined Pools  | 1:20 | 1. SPP capacity at shared capped processor rate  \n 2. VM cores charged at EC (capped or uncapped)  \n 3. Existing behavior – no change | Per OS type: Minimum of (sum of VP of VMs in pool or max capacity of pool); only for uncapped mode  \n For {{site.data.keyword.on-prem-fname}}, these OS license charges are associated with the respective VM proportionate to VPs of that VM |
| Default Pool | 1:20 | 1. No charge at SPP level  \n 2. VM cores charged at EC (capped or uncapped)  \n 3. Existing behavior – no change |
{: caption="Shared processor pool for {{site.data.keyword.on-prem-fname}}" caption-side="bottom"}

For more information about calculating the pricing for OS licensing in the uncapped SPP, see [How to calculate the pricing for OS licensing in SPP](#cal-OSlic).









## Pricing for dedicated hosts
{: #pricing-dh-private}

Dedicated hosts are priced based on the host type – either an IBM Power S922 or IBM Power S1022. Each server type is metered by the hour and the price includes the entire capacity of the host.

Consider the following points for dedicated host pricing:
* You are not charged separately for shared processor pools you deploy to the dedicated host.
* Software charges for the supported operating systems are metered and charged by the core.

To learn more about the dedicated host, see: [dedicated host](/docs/power-iaas?topic=power-iaas-dedicated-host).

## Storage types
{: #storage-types}

{{site.data.keyword.on-prem-fname}} charges are based on the following storage types:

* **Data volumes**: These volumes are basic forms that you can create. The billing depends on the volume size when metered. Table 7 shows an example of how you are billed based on your volume creation:

   | Volume size that you create  | Volume size that you are billed  |
   |  ---------------------  | ----------------------------  |
   |  10 GB                  | 10 GB                         |
   |  10+5 GB                | 15 GB                         |
   {: caption="Calculation of data volume" caption-side="bottom"}


* **Image backing volumes**: These volumes are part of a boot image in your cloud instance that is listed in the boot image catalog. Billing for image backing volumes is determined as follows:


   - Single volume billing - When the image has a single backing volume, you are billed based on the size (GB) of the single volume.
   - Multiple volume billing - When the image has multiple backing volumes, billing is based on tallying up the sizes of all the image backing volumes.

Table 8 shows an example of how you are billed based on your boot volume:


   | Image volume size                   | Single or multiple backing  | Billed volume size |
   | ----------------------------------  | --------------------------  | ----------------|
   | 20 GB                               | Single backing volume       | 20 GB           |
   | Volume 1 (20 GB), volume 2 (10 GB)  | Multiple backing volumes     | 30 GB           |
   {: caption="Calculation of image backing volume" caption-side="bottom"}


* **Deployed virtual machine volumes**: When you deploy a virtual machine with an image, it gets a copy of all the volumes in the image. Extra data volumes added to the deployed virtual machine are billed separately as Data Volumes. Table 9 shows an example of how you are billed based on the virtual machines that you deploy:

   | Image backing volume  | Billed volume size |
   |  -------------------  | ----------------|
   |  20 GB                | 20 GB           |
   |  20 GB + 30 GB        | 50 GB           |
   {: caption="Calculation of deployed virtual machines volume" caption-side="bottom"}

* **Deployed virtual machine snapshots**: The snapshots of the volumes are taken after the virtual machine is deployed. The size of the volume snapshot is related to the number of updates that are made to the virtual machine. When you take a snapshot for the first time, the size of the snapshot is a fraction of the size of the volumes of the virtual machine. The size of subsequent snapshots might increase based on the changes that are made to the original volume.



For an example, consider a virtual machine with a volume of 100 GB. The size of the first snapshot is 100 GB. The size of the second snapshot might be 1 GB.

Snapshot sizes are not predictable as they are related to the updates made to the volume between two snapshots.
{: note}


Tables 10 and 11 show how different storage types affect the cost per system:

| Volume storage           | Hourly rate (Processor type)  | Monthly cost (730 hours)  |
|  ----------------------  | ----------------------------  | ------------------------  |
|  Tier 0                  | $0.00029589                   | $0.22                     |
|  Tier 1                  | $0.00024658                   | $0.18                     |
|  Tier 3                  | $0.00012884                   | $0.09                     |
|  Tier 5k                 | $0.00035507                   | $0.26                     |
{: caption="Volume storage pricing" caption-side="bottom"}

| Snapshot storage         | Hourly rate (Processor type)  | Monthly cost (730 hours)  |
|  ----------------------  | ----------------------------  | ------------------------  |
|  Tier 0                  | $0.00008877                   | $0.06                     |
|  Tier 1                  | $0.00007397                   | $0.05                     |
|  Tier 3                  | $0.00003865                   | $0.03                     |
|  Tier 5k                 | $0.00010652                   | $0.08                     |
{: caption="Snapshot storage pricing" caption-side="bottom"}


### Use case of account billable storage
{: #billable-storage}

Table 13 shows the use case on how you are billed based on the storage that you use (assuming tier 1):

   | Name           |  Size    | State or Description         |
   | -------------  | -------  | ------------------------- |
   | data-volume-1  |  20 GB   | Available                 |
   | data-volume-2  |  25 GB   | In-use (attached to vm-1) |
   | data-volume-3  | 100 GB   | In-use (attached to vm-1) |
   | data-volume-4  |  30 GB   | Available                 |
   | data-volume-5  |  60 GB   | In-use (attached to vm-2) |
   | image-volume-1 | 100 GB   | In-use (attached to vm-1) |
   | image-volume-2 | 100 GB   | In-use (attached to vm-2) |
   {: caption="Account billable for storage use case" caption-side="bottom"}

Total billable storage = 595 GB

* Data volumes: 235 GB

* Image volumes: 200 GB

* Deployed virtual machine boot volumes: 200 GB

To generate an estimated price, use the [{{site.data.keyword.powerSys_notm}} Estimate pricing](https://cloud.ibm.com/power/estimate){: external} tool. For more information, see [Generating an estimate](/docs/power-iaas?topic=power-iaas-generating-an-estimate).
{: important}

## End of billing
{: #end-billing}

The monthly billing cycle ends when you delete the virtual machine. If you scale your infrastructure up and down in response to workload requirements, your billing follows the timing of the virtual machine provision change. If you stop the virtual machine, the billing process is not stopped. Delete the virtual machine to stop the billing cycle.

When your virtual machine is active but idle, you can use Dynamic Logical Partitioning (DLPAR) to resize it to a minimal state. You can drastically decrease the price per hour by reducing the core count and memory of the virtual machine.
{: important}

## Frequently asked questions
{: #faq}

Review the following frequently asked questions about pricing:

### Where do I find cost estimates for {{site.data.keyword.powerSys_notm}} offerings?
{: #cost-estimates}

   You can generate an estimated price by using the [{{site.data.keyword.powerSys_notm}} Estimate pricing](https://cloud.ibm.com/power/estimate){: external} tool. For more information, see [Generating an estimate](/docs/power-iaas?topic=power-iaas-generating-an-estimate).


   By default, the cost estimator shows hourly prices for the selected resources and their units of measure. For more information, see [Estimating your costs](https://cloud.ibm.com/docs/billing-usage?topic=billing-usage-cost){: external}.














### Where can I find the unit prices for the billing metrics?
{: #billing-metrics}

   You can view the unit prices for the billing metrics for {{site.data.keyword.on-prem-fname}} on the [IBM global catalog](https://globalcatalog.cloud.ibm.com/){: external}.

   On the global catalog, complete the following steps to view the pricing for each metric ID:

   * Log on to [IBM global catalog](https://globalcatalog.cloud.ibm.com/){: external}.
   * Search the catalog for the resources for which you need pricing. The following options for search strings are available:
     - `Power Virtual Server Virtual Machine` for virtual machines that includes processor, memory, operating systems, and workloads.
     - `Power Virtual Server Volume` for Volumes.
     - `Power Virtual Server Snapshot` for Snapshots.
     - `Power Virtual Server Shared Processor Pool` for Shared Processor Pools. No pricing is associated with other types of resources.
   * Click the selected resource type entry from the search results. The corresponding page opens.
   * Click the {{site.data.keyword.powerSys_notm}} Private Cloud billing plan from the left page:
     - `Power Virtual Server Private Cloud Virtual Machine Group` for virtual machines.
     - `Power Virtual Server Private Cloud Volume Group` for Volumes.
     - `Power Virtual Server Private Cloud Snapshot Group` for Snapshots.
     - `Power Virtual Server Private Cloud Shared Processor Pool` for Shared Processor Pools (SPP).
         Deployments with different satellite regions are displayed.
   * Select the deployment with the name that ends with the satellite region for which you want the pricing.
      For example, the **Power Virtual Server Private Cloud PVM Instance Groupsatcon_dal** deployment displays the pricing for virtual machines in the satellite locations that are hosted in the Dallas region.
   * Click the **Pricing** tab on the right navigation page to view the pricings for different **Metric IDs**.
      Refer to [Table 2: Part definition and metric ID](#Table2) to find the metric ID corresponding to the part description. Prices are listed for all IBM Cloud supported currencies.







### How to calculate the pricing for OS licensing in the uncapped SPP?
{: #cal-OSlic}


To calculate the price for OS licensing in the uncapped SPP, consider the following conditions:
* If the total number of VPs associated with the partitions in an SPP is greater than the maximum capacity of the pool, then the cost is distributed proportionately for all VPs.
* If the total number of VPs associated with the partitions in an SPP is less than or equal to the maximum capacity of the pool, then the pricing is considered for each VP.





Table 14 shows how the pricing for OS licensing is calculated considering that the maximum pool capacity is 8 cores :

| Example | VM      | VP on VM | Total number of VPs versus Maximum pool capacity | Cost calculation |
| ------  | ------- | -------- | --------------------------------------------- | ---------------- |
| 1       | AIX VM1 | 4        | 6 < 8 (6 is considered)                      | 4 x cost of AIX OS license |
|         | AIX VM2 | 2        |                                               | 2 x cost of AIX OS license |
| 2       | AIX VM1 | 4        | 10 > 8 (8 is considered)                      | 3.2 x cost of AIX OS license |
|         | AIX VM2 | 2        |                                               | 1.6 x cost of AIX OS license |
|         | AIX VM3 | 4        |                                               | 3.2 x cost of AIX OS license |
{: caption="Pricing for OS licensing in SPP in {{site.data.keyword.on-prem-fname}}" caption-side="bottom"}










### Is there any initial one-time payment before the pod infrastructure is installed in the {{site.data.keyword.on-prem-fname}} data center?
{: #initial-one-time-payment}

   No



### In terms of costs, what do I pay for?
{: #payment}

   The monthly consumption charges are factored based on the minimum committed spend and metered consumption charges. If the consumption charges are less than or equal to the minimum-committed spend, you pay the minimum-committed spend amount. If the consumption charges exceed the minimum committed spend, you pay the metered consumption charges.

### Can I change infrastructure configuration based on my requirements after my virtual servers are provisioned? How will it impact billing?
{: #change-infra-post-provisioning}

   Yes, you can add extra nodes but cannot reduce the number of nodes. The billing gets updated from the date that the new nodes are added.

### When does the billing begin?
{: #billing-schedule}

   Billing begins when an IBM representative sets up and registers the pod in the {{site.data.keyword.on-prem-fname}} data center.
