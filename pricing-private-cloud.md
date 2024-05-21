---

copyright:
  years: 2023

lastupdated: "2023-03-28"

keywords: pricing, {{site.data.keyword.powerSys_notm}} as a service, private cloud, before you begin, terminology, video, how-to

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Pricing for IBM {{site.data.keyword.powerSys_notm}} Private Cloud
{: #pricing-private-cloud}

[Private Cloud]{: tag-red}

{{site.data.keyword.powerSysFull}} Private Cloud provides a secure and unified billing for the separate hardware resources and software resources that you use. The following list of hardware resources are metered:

- Virtual machines: The CPU (in cores), with processor mode (capped, shared, dedicated), and memory (in GB) are metered.

- Volumes: Volume (in GB) is metered.

- Snapshots: Snapshots (in GB) are metered.

For more information about billing for operating systems, see [Operating systems](/docs/power-iaas?topic=power-iaas-pricing-private-cloud#operating-systems).

In the IBM Cloud catalog for IBM {{site.data.keyword.powerSys_notm}} Private Cloud, the estimated price might be different from the actual price when you purchase the IBM {{site.data.keyword.powerSys_notm}} Private Cloud infrastructure or instances, based on the discounts and promotion codes.

The following IBM Cloud regions can host connections from the pods for IBM {{site.data.keyword.powerSys_notm}} Private Cloud in your data center:
- Dallas
- Frankfurt
- London
- Madrid
- Osaka
- Sao Paulo
- Sydney
- Tokyo
- Toronto
- Washington, DC

Selection of IBM Cloud region is one of the factors for computing pricing.
{: Note}

## Monthly usage
{: #monthly-usage}

IBM {{site.data.keyword.powerSys_notm}} Private Cloud instances are charged at a monthly rate that is prorated per hour. If you add resources to a <!--virtual server instance--> virtual machine during the middle of the month, the monthly bill for the <!--virtual server instance--> virtual machine reflects the resource change and the <!--virtual server instance--> virtual machine price that is prorated per hour.

All prices mentioned on this page are illustrative and do not represent the actual amounts used for billing. To generate an estimated price, use the [{{site.data.keyword.powerSys_notm}} Estimate pricing](https://cloud.ibm.com/power/estimate){: external} tool. For more information, see [Generating an estimate](/docs/power-iaas?topic=power-iaas-generating-an-estimate).
{: important}

In the following example, the customer provisions an IBM {{site.data.keyword.powerSys_notm}} Private Cloud instance that has one core with 8 GB of memory, a 150 GB disk, and is running Red Hat Enterprise Linux (RHEL) operating system (OS).
Let us assume the following hypothetical monthly prices:
* Cores: $143.23/month x 1 = $143.23
* Memory: $9/month each GB x 8 = $ 72.00
* Storage: $0.216/month each GB x 150 GB = $ 32.40
* OS license: $43.80/month each core   = $ 43.80

**Total cost per month**     = $291.43

Factoring the example quantities and prices, the base price for this <!--virtual server instance--> virtual machine is $291.43/month or an average of $0.399/hour for all the resources consumed.

Assume that in the course of the month, the customer allocates more memory to the <!--virtual server instance--> virtual machine. At the end of the month, the new price for the <!--virtual server instance--> virtual machine will be higher to account for the extra memory and amounts to $0.498/hour for all the resources consumed. The monthly bill is prorated by an hour for the resources deployed as shown in Table 1.

In Table 1, the <!--virtual server instance--> virtual machine resources are increased (after the resources reach 300 hours in the month) from 8 GB to 16 GB of memory. The price of the <!--virtual server instance--> virtual machine is prorated by an hour for the final monthly price of $303.

| Hours elapsed in a month   | Amount charged                               |  Virtual machine  description    |
| -------------------------- | -------------------------------------------- |  --------------------------------------- |
| 300 hours                  | (300 hours x $0.399)/month = $119.70         |  1 core, 8 GB memory, 150 GB disk, RHEL  |
| 430 hours                  | (430 hours x $0.498)/month = $214.14         |  1 core, 16 GB memory, 150 GB disk, RHEL |
| 730 hours (Monthly Total)  | $119.70 + $214.14 = $333.84 (Monthly Total)  |  1 core, 16 GB memory, 150 GB disk, RHEL |
{: caption="Table 1. An example of monthly charges for a virtual machine" caption-side="bottom"}

For detailed usage and billing information, you can refer to the part numbers in your invoice. The part numbers in the invoice represent the charge unit for each individual resource charged. For this example, we would see four distinct part numbers in the invoice for that <!--virtual server instance--> virtual machine, one each for: the virtual cores, the memory, the volume storage (disk), and the OS license (RHEL). To view the part numbers, refer to Table 2.


|  Part description (visible on the invoice from IBM)              | Metric ID (visible in the IBM Cloud catalogue) |
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
| Red Hat Enterprise Linux operating system scale-out license core-hour - SAP workload  | ppcaas-metric-rhel-sap-scale-out |
| Red Hat Enterprise Linux operating system scale-up license core-hour - SAP workload  | ppcaas-metric-rhel-sap-scale-up |
| SUSE Linux Enterprise Server operating system tier 1 instance-hour - SAP workload  | ppcaas-metric-sles-sap-tier1 |
| SUSE Linux Enterprise Server operating system tier 2 instance-hour - SAP workload  | ppcaas-metric-sles-sap-tier2 |
| SUSE Linux Enterprise Server operating system tier 3 instance-hour - SAP workload  | ppcaas-metric-sles-sap-tier3 |
| **IBM Power Systems Virtual Server operating systems group**       |                                                |
| AIX operating system scale-up license core-hour | ppcaas-metric-aix-scale-up |
| AIX operating system scale-out license core-hour | ppcaas-metric-aix-scale-out |
| Red Hat Enterprise Linux operating system scale-up license core-hour | ppcaas-metric-rhel-scale-up |
| Red Hat Enterprise Linux operating system scale-out license core-hour | ppcaas-metric-rhel-scale-out |
| SUSE Linux Enterprise Server operating system tier 1 instance-hour | ppcaas-metric-sles-tier1 |
| SUSE Linux Enterprise Server operating system tier 2 instance-hour | ppcaas-metric-sles-tier2 |
| SUSE Linux Enterprise Server operating system tier 3 instance-hour | ppcaas-metric-sles-tier3 |
| [Q2-2024 update start]{: tag-teal} IBM i operating system P10 license core-hour | ppcaas-metric-ibmi-os-p10 |
| IBM i operating system P30 license core-hour | ppcaas-metric-ibmi-os-p30 |
| IBM i operating system P10 movable license - SWMA paid - core-hour | ppcaas-metric-ibmi-os-p10-mol |
| IBM i operating system P30 movable license - SWMA paid - core-hour | ppcaas-metric-ibmi-os-p30-mol |
| IBM i operating system P10 service extension core-hour | ppcaas-metric-ibmi-os-p10-sve |
| IBM i operating system P30 service extension core-hour | ppcaas-metric-ibmi-os-p30-sve |
| IBM i LPP P10 license core-hour | ppcaas-metric-ibmi-lpp-p10 |
| IBM i LPP P30 license core-hour | ppcaas-metric-ibmi-lpp-p30 |
| IBM i LPP P10 movable license - SWMA paid - core-hour | ppcaas-metric-ibmi-lpp-p10-mol |
| IBM i LPP P30 movable license - SWMA paid - core-hour | ppcaas-metric-ibmi-lpp-p30-mol |
| IBM i P10 PowerHA instance core-hour | ppcaas-metric-ibmi-pha-p10 |
| IBM i P30 PowerHA instance core-hour | ppcaas-metric-ibmi-pha-p30 |
| IBM i Cloud Storage Solutions instance core-hour | ppcaas-metric-ibmi-cos |
| IBM i Rational Developer Studio instance core-hour| ppcaas-metric-ibmi-rds [Q2-2024 update end]{: tag-teal}|
| **IBM Power Systems Virtual Server Private Cloud volume group**  |
| Volume Storage Tier 0 gigabyte-hour  | ppcaas-metric-volume-tier0 |
| Volume Storage Tier 1 gigabyte-hour  | ppcaas-metric-volume-tier1 |
| Volume Storage Tier 3 gigabyte-hour  | ppcaas-metric-volume-tier3 |
| Volume Storage Tier 5k gigabyte-hour | ppcaas-metric-volume-tier5k |
| **IBM Power Systems Virtual Server Private Cloud snapshot group**  |
| Snapshot Storage Tier 0 gigabyte-hour  | ppcaas-metric-snapshot-tier0 |
| Snapshot Storage Tier 1 gigabyte-hour  | ppcaas-metric-snapshot-tier1 |
| Snapshot Storage Tier 3 gigabyte-hour  | ppcaas-metric-snapshot-tier3 |
| Snapshot Storage Tier 5k gigabyte-hour | ppcaas-metric-snapshot-tier5k |
| **IBM Power Systems Virtual Server Private Cloud virtual tape library group** |
| [Q2-2024 update start]{: tag-teal} Virtual Tape Library terabyte-hour | ppcaas-metric-vtl [Q2-2024 update end]{: tag-teal}|
| **IBM Power Systems Virtual Server Private Cloud shared processor pool group** |             |
| [Q2-2024 update start]{: tag-teal} IBM Power Systems S1022 virtual processor core-hour - Shared Processor Pool | ppcaas-metric-E1080-spp-cores |
| IBM Power Systems E1050 virtual processor core-hour - Shared Processor Pool | ppcaas-metric-E1050-spp-cores |
| IBM Power Systems E1080 virtual processor core-hour - Shared Processor Pool | ppcaas-metric-S1022-spp-cores [Q2-2024 update end]{: tag-teal} |
{: caption="Table 2. Part descriptions and metric IDs" caption-side="bottom"}
{: #Table2}


## Base instances
{: #base-instances}

The base instance billing depends on the options that you select when you create a <!--virtual server instance--> virtual machine. The machine type, number of cores, and amount of memory affects the base instance billing. When you create your <!--virtual server instance--> virtual machine, the associated monthly rate is displayed on the base instance billing.

The pricing for memory is calculated based on a ratio of 64 GB per core. For example, if you use more than 16 GB for 0.25 cores, you must pay a premium high-use RAM price for the excess memory. However, if you use up to 128 GB for 2 cores, you do not have to pay any premium memory price.

## Operating systems
{: #operating-systems}

Currently, Linux and AIX operating systems are supported and only RHEL stock images are available. For more information about supported versions and distributions, see [Full Linux subscription for Power Virtual Server private cloud](/docs/power-iaas?topic=power-iaas-full-linux-sub). If you select a RHEL Linux stock image, the pricing includes the full Linux subscription charges. The full Linux subscription allows you to subscribe to updated or upgraded packages from a Red Hat Satellite server by configuring the provisioned virtual machine. The metering for RHEL full Linux subscription starts when you create the virtual machine. If you bring your own license, it is not metered or billed.

If you bring your own custom image, you are charged for the image size and the storage tier that you use for the custom image. After you deploy a stock image (and only after deployment), you are charged for the space used to store the stock image. The storage unit price (per GB) for the stored boot images is same as the selected storage tier (Tier 0, Tier 1, or Tier 3) where your boot disks are deployed. To identify the estimated storage rates, use the [{{site.data.keyword.powerSys_notm}} Estimate pricing](https://cloud.ibm.com/power/estimate){: external} tool. To reduce costs, you can select the virtual machine and delete it when it is not needed.

## Processor types
{: #processor-types}

You are charged different rates that depends on the type of system that you choose for your <!--virtual server instance--> virtual machine. Enterprise systems, such as E1080 or E1050, cost more because they provide more processing capacity per core. For example, E1080 costs more than E1050.

You can choose the one of the following core types for your workload:
* **Dedicated virtual processor cores**
* **Shared capped virtual processor cores**
* **Shared uncapped virtual processor cores**

Different scenarios provide different benefits when you use each type of virtual processor cores.

All prices mentioned on this page are illustrative and do not represent the actual amounts used for billing. To generate an estimated price, use the [{{site.data.keyword.powerSys_notm}} Estimate pricing](https://cloud.ibm.com/power/estimate){: external} tool. For more information, see [Generating an estimate](/docs/power-iaas?topic=power-iaas-generating-an-estimate).
{: important}

In the following example, assume that the cost of different types of virtual processor cores is same within each type of system they belong to.

Tables 3 to 5 show how different processor types affect the cost per system:

| Number of cores (S1022)  | Hourly rate (Processor type)  | Monthly cost (730 hours)  |
|  ----------------------  | ----------------------------  | ------------------------  |
|  1                       | $0.1962 (dedicated)           | $143.226                  |
|  1                       | $0.1962 (uncapped shared)     | $143.226                  |
|  1                       | $0.1962 (capped shared)       | $143.226                  |
{: caption="Table 3. S1022 processor type pricing" caption-side="bottom"}

| Number of cores (E1080)  | Hourly rate (Processor type)  | Monthly cost (730 hours)  |
|  ----------------------  | ----------------------------  | ------------------------  |
|  1                       | $0.6866 (dedicated)           | $501.20                   |
|  1                       | $0.6866 (uncapped shared)     | $501.20                   |
|  1                       | $0.6866 (capped shared)       | $501.20                   |
{: caption="Table 4. E1080 processor type pricing" caption-side="bottom"}

| Number of cores (E1050)  | Hourly rate (Processor type)  | Monthly cost (730 hours)  |
|  ----------------------  | ----------------------------  | ------------------------  |
|  1                       | $0.2945 (dedicated)           | $215.00                   |
|  1                       | $0.2945 (uncapped shared)     | $215.00                   |
|  1                       | $0.2945 (capped shared)       | $215.00                   |
{: caption="Table 5. E1050 processor type pricing" caption-side="bottom"}



## Memory types
{: #memory-types}

Charges for IBM {{site.data.keyword.powerSys_notm}} Private Cloud are determined by the amount of memory used (in gigabytes) and the type of the system that you choose for your virtual machine. Enterprise systems, such as E1080 or E1050, use scale-up memory with higher density, whereas S1022 systems use scale-up memory with lesser density. Currently, both scale-up and scale-out memory might cost you the same price. However, this pricing is subject to change in the future, depending on the cost of the memory chips. Table 6 shows how memory types affect the cost per system:

| Number of GBs |  Memory type                      | Hourly rate (Processor type)  | Monthly cost (730 hours)  |
| ---------------- | ----------------------------------  | -----------------------  | ------------------------  |
|  1               | IBM Power Systems scale-out memory  | $0.01232877              | $9.00                     |
|  1               | IBM Power Systems scale-up memory   | $0.01232877              | $9.00                     |
{: caption="Table 6. Memory type pricing" caption-side="bottom"}


## SAP workload types
{: #SAP-workload-types}

You can deploy the following two types of SAP workloads as virtual machines:

* **SAP NetWeaver**: For SAP NetWeaver for Linux, the charges for hardware, processors, and memory are similar to other types of Linux deployments. However, the SAP NetWeaver for Linux requires a different type of operating system and license to be deployed. So, the charges for these types of deployments are not same as that of Red Hat Enterprise Linux for SAP (non-SAP OS).

* **SAP HANA**: For SAP HANA, there are distinct processor and memory billing parts. The charges on these distinct parts appear on the monthly invoices. Similar to other types of deployments, the following types of systems, processors, and memory are supported for SAP HANA:
    - System types: S1022, E1050, or E1080
    - Virtual processor core types: dedicated, shared capped, or shared uncapped
    - Memory types: scale-out or scale-up

For SAP HANA workloads, the charges for processor and memory parts are the same as compared to non-SAP HANA workloads. To estimate the costs for non-SAP HANA workloads, see Tables 3, 4, 5, and 6.

The pricing is subject to change depending on the SAP HANA operational costs.
{: note}


## Pricing for dedicated hosts
{: #pricing-dh}

[Q2-2024 update start]{: tag-teal}
Dedicated hosts are priced based upon the host type – either an IBM Power S922 or IBM Power S1022.  Each server type is metered by the hour and the price includes the entire capacity of the host.

Consider the following points for dedicated host pricing:
* You are not charged separately for shared processor pools you deploy to the dedicated host.
* Software charges for the supported operating systems are metered and charged by the core.

To learn more about the dedicated host, see: [dedicated host](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#dedicated-host).
[Q2-2024 update end]{: tag-teal}


## Storage types
{: #storage-types}

IBM {{site.data.keyword.powerSys_notm}} Private Cloud charges are based on the following storage types:

* **Data volumes**: These volumes are of the simplest form that you can create. You are billed based on the current volume size at the metering time. Table 7 shows an example of how you are billed based on your volume creation:

   | Volume size you create  | Volume size you are billed  |
   |  ---------------------  | ----------------------------  |
   |  10 GB                  | 10 GB                         |
   |  10+5 GB                | 15 GB                         |
   {: caption="Table 7. Calculation of data volume" caption-side="bottom"}


* **Image backing volumes**: These volumes are part of a boot image in your cloud-instance present in the boot image catalog. You are billed based on the total volume size(s) contained in the image.

    When the image has a single backing volume, you are billed based on the size (GB) of the single volume. When the image has multiple backing volumes, you are billed based on tallying up the size(s) of all the image backing volumes. Table 8 shows an example of how you are billed based on your boot volume:


   | Image volume size                   | Single or multiple backing  | Billed volume size |
   | ----------------------------------  | --------------------------  | ----------------|
   | 20 GB                               | Single backing volume       | 20 GB           |
   | volume 1 (20 GB), volume 2 (10 GB)  | Multiple backing volumes     | 30 GB           |
   {: caption="Table 8. Calculation of image backing volume" caption-side="bottom"}


* **Deployed virtual machine volumes**: These volumes are created when you deploy a virtual machine with an image. The deployed virtual machines get a copy of all the volumes in the image. Any additional data volumes attached to the deployed virtual machine are already billed under Data Volumes. Table 9 shows an example of how you are billed based on the virtual machines that you deploy:

   | Image backing volume  | Billed volume size |
   |  -------------------  | ----------------|
   |  20 GB                | 20 GB           |
   |  20 GB + 30 GB        | 50 GB           |
   {: caption="Table 9. Calculation of deployed virtual machines volume" caption-side="bottom"}

* **Deployed virtual machine snapshots**: The snapshots of the volumes are taken after the virtual machine is deployed. The size of the volume snapshot is related to the number of updates made to the virtual machine. When you take the snapshot of the volume for the first time, the size of the snapshot is equal to the volume of the virtual machine. Subsequently, when you take the snapshots of the same volume, the updates made to the volume after the first snapshot taken is only saved. So, the subsequent snapshots when compared with the first snapshot taken are smaller and thus cost less.

For an example, consider a virtual machine with a volume of 100 GB. The size of the first snapshot is 100 GB. The the size of the second snapshot might be 1 GB.

Snapshot sizes are not predictable as they are related to the updates made to the volume between two snapshots.
{: note}


Tables 10 and 11 show how different storage types affect the cost per system:

| Volume storage           | Hourly rate (Processor type)  | Monthly cost (730 hours)  |
|  ----------------------  | ----------------------------  | ------------------------  |
|  Tier 0                  | $0.00029589                   | $0.22                     |
|  Tier 1                  | $0.00024658                   | $0.18                     |
|  Tier 3                  | $0.00012884                   | $0.09                     |
|  Tier 5k                 | $0.00035507                   | $0.26                     |
{: caption="Table 10. Volume storage pricing" caption-side="bottom"}

| Snapshot storage         | Hourly rate (Processor type)  | Monthly cost (730 hours)  |
|  ----------------------  | ----------------------------  | ------------------------  |
|  Tier 0                  | $0.00008877                   | $0.06                     |
|  Tier 1                  | $0.00007397                   | $0.05                     |
|  Tier 3                  | $0.00003865                   | $0.03                     |
|  Tier 5k                 | $0.00010652                   | $0.08                     |
{: caption="Table 11. Snapshot storage pricing" caption-side="bottom"}


### Use case of account billable storage
{: #billable-storage}

Table 12 shows the use case on how you are billed based on the storage that you use (assuming tier 1):

   | Name           |  Size    | State or Description         |
   | -------------  | -------  | ------------------------- |
   | data-volume-1  |  20 GB   | Available                 |
   | data-volume-2  |  25 GB   | In-use (attached to vm-1) |
   | data-volume-3  | 100 GB   | In-use (attached to vm-1) |
   | data-volume-4  |  30 GB   | Available                 |
   | data-volume-5  |  60 GB   | In-use (attached to vm-2) |
   | image-volume-1 | 100 GB   | In-use (attached to vm-1) |
   | image-volume-2 | 100 GB   | In-use (attached to vm-2) |
   {: caption="Table 12. Account billable for storage use case" caption-side="bottom"}

Total billable storage = 595 GB

* Data volumes: 235 GB

* Image volumes: 200 GB

* Deployed virtual machine boot volumes: 200GB

To generate an estimated price, use the [{{site.data.keyword.powerSys_notm}} Estimate pricing](https://cloud.ibm.com/power/estimate){: external} tool. For more information, see [Generating an estimate](/docs/power-iaas?topic=power-iaas-generating-an-estimate).
{: important}

## End of billing
{: #end-billing}

The monthly billing cycle ends when you delete the <!--virtual server instance--> virtual machine. If you scale your infrastructure up and down in response to workload requirements, your billing follows the timing of the <!--virtual server instance--> virtual machine provision change. If you stop the <!--virtual server instance--> virtual machine, the billing process is not stopped. Delete the <!--virtual server instance--> virtual machine to stop the billing cycle.

When your virtual machine is active but idle, you can use Dynamic Logical Partitioning (DLPAR) to resize it to a minimal state. You can drastically decrease the price per hour by reducing the core count and memory of the virtual machine.
{: important}

## Frequently asked questions
{: #faq}

Review the following frequently asked questions about pricing:

### Where do I find cost estimates for {{site.data.keyword.powerSys_notm}} offerings?
{: #cost-estimates}

   You can generate an estimated price by using the [{{site.data.keyword.powerSys_notm}} Estimate pricing](https://cloud.ibm.com/power/estimate){: external} tool. For more information, see [Generating an estimate](/docs/power-iaas?topic=power-iaas-generating-an-estimate).

   By default, the cost estimator shows hourly prices for the selected resources and their units of measure. For more information, see [Estimating your costs](https://cloud.ibm.com/docs/billing-usage?topic=billing-usage-cost){: external}

### How do I find the unit prices for the billing metrics?
{: #billing-metrics}

   On the [IBM global catalog](https://globalcatalog.cloud.ibm.com/){: external}, you can view the unit prices for the billing metrics for IBM {site.data.keyword.powerSys_notm}. On the global catalog, perform the following steps to view the pricing for each metric ID:
     * Search for 'power-iaas' in the search bar.
     * From the search results, click the global catalog entry, 'Workspace for Power Virtual Server'.
         The **Workspace for Power Virtual Server** page opens.
     * Click **Power Virtual Server Private Cloud Group** from the left pane.
         The groups with different satellite regions are displayed.
     * Select the group with the satellite region where you might host the IBM {{site.data.keyword.powerSys_notm}} Private Cloud.
         For example, the **Power Virtual Server Private Cloud PVM Instance Groupsatcon_dal** group displays the pricing for virtual machines in Dallas.
     * Click the **Pricing** tab on the right navigation pane to view the pricing for different Metric IDs.
         Refer to [Table 2: Part definition and metric ID](#Table2) to find the metric ID corresponding to the Part numbers. Prices are listed on all IBM Cloud supported currencies.


### Is there any initial one-time payment before the pod infrastructure is installed in the client private cloud data center?
{: #initial-one-time-payment}

   No

### In terms of cost, what do I pay for?
{: #payment}

   The monthly consumption charges are factored based on the minimum committed spend and metered consumption charges. If the consumption charges are less than or equal to the minimum committed spend, you pay the minimum committed spend amount. If the consumption charges exceeds the minimum commmitted spend, you pay the metered consumption charges.

### Can I change infrastructure configuration based on my requirements after my virtual servers are provisioned? How will it impact billing?
{: #change-infra-post-provisioning}

   Yes, you can add additional nodes but cannot reduce the number of nodes. The billing will get updated from the date the new nodes are added.

### When does the billing begin?
{: #billing-schedule}

   Billing begins when an IBM representative sets up and registers the pod in the client private cloud data center.
