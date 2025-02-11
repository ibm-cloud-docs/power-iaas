---

copyright:
  years: 2019, 2024

lastupdated: "2025-02-11"

keywords: pricing, monthly usage, billing process, billing cycle, DLPAR, processor types, linux

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Pricing for IBM {{site.data.keyword.powerSys_notm}} in {{site.data.keyword.off-prem}}
{: #pricing-virtual-server-on-cloud}

---

{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


---





{{site.data.keyword.powerSysFull}}s is offered in select regions with scale-out logical partitions (LPAR). The IBM Power that can host {{site.data.keyword.powerSys_notm}}s have the following theoretical maximums:

All prices that are mentioned in the topic are illustrative and do not represent the actual amounts that are used for billing. To calculate the exact pricing, use the [cost estimator](https://cloud.ibm.com/power/estimate){: external}.
{: important}




|  Power Systems         |  Processors  |  Memory                     |
|------------------------|--------------|-----------------------------|
| E980 (9080-M9S)        |  143         | Up to 15,307 GB [^1]        |
| S922 (9009-22A) [^2]   |   15         | Up to 942 GB                |
| S1022 (9105-22A) [^3]  |   33         | Up to 1984 GB               |
| E1080 (9080-HEX)       |  240         | Up to 64 TB                 |
| E1050 (9043-MRX)       |   96         | Up to  8,192 GB             |
{: caption="Theoretical maximum memory" caption-side="bottom"}

[^1]: In DAL12, DAL13, OSA21, SAO01, TOK04, WDC04, and WDC06 data centers, the E980 systems allow up to 23,070 GB of memory.

[^2]: If the machine type is S922 and the operating system is IBM i, IBM i supports a maximum of 4 cores per VM.

[^3]: If the machine type is S1022 and the operating system is IBM i, IBM i supports a maximum of 4 cores per VM.


For more information about the availability of the systems for your data center, see the overview page of the [IBM {{site.data.keyword.powerSys_notm}}](https://cloud.ibm.com/power/overview) in the IBM Cloud console.

It's important to note that a system's theoretical maximum depends on the data center. Also, the {{site.data.keyword.powerSys_notm}} development team enforces the current available resources within each data center. With these processing maximums, the {{site.data.keyword.powerSys_notm}} can meet any business workload requirement.
{: shortdesc}

In the Cloud catalog for {{site.data.keyword.powerSys_notm}}s, the estimated price might be different than the actual price when you purchase the {{site.data.keyword.powerSys_notm}} or instances based on the discounts and promotion codes.



## Consumer ID
{: #consumer-id}

Consumer ID groups the billing usages that are under a single resource such as virtual machines, shared processor pools, and storages. You can view resource usage with a broken down metrics. There is no change in billing or pricing and you continue to receive your bills as-is today.

Following are the benefits of consumer ID:
- You can see a more granular view of your bill by using the **Usage** page in the [Billing and Usage](https://cloud.ibm.com/billing/usage){: external} portal.
- Charges are now broken down by resource that is identified in the **Consumer ID** field with the format `resource-type:resource-uuid`.

To view the usage details at the resource level, do the following steps:
1. Open the [Billing and Usage](https://cloud.ibm.com/billing/usage){: external} page in the IBM Cloud console.
2. On the left navigation menu, click **Usage**.
3. Click **View plans** for the entry- **Workspace for Power Virtual Server**. A page listing all your workspaces is opened.
4. Click **View details** for a workspace. A page listing the usage details of a selected workspace is opened.
5. Scroll to the bottom of the page and click **View instance details**. A page listing the usage details of the selected virtual server instance is opened.

For more information on the billing and usage page, see [Billing and Usage documentation](https://cloud.ibm.com/docs/account?topic=account-viewingusage&interface=ui){: external}.



## Monthly usage
{: #pricing-monthly-usage}

{{site.data.keyword.powerSys_notm}} instances are charged at a monthly rate that is prorated per hour. If you add resources to an LPAR during the middle of the month, the monthly bill for the LPAR reflects the resource change and the LPAR price that is prorated per hour.

In the following monthly usage example, the customer purchases a {{site.data.keyword.powerSys_notm}} instance that has one core with 8 GB of memory, a 150 GB disk, and is running AIX 7200-03-02, at a base price of $250.57 per month ($0.343 per hour). As the month progresses, the customer adds more memory. The new price for the LPAR is $339.45 per month ($0.465 per hour). The monthly bill is prorated by the hour for the resources deployed.

All prices that are mentioned in the topic are illustrative and do not represent the actual amounts that are used for billing. To generate an estimated price, use the [{{site.data.keyword.powerSys_notm}} Estimate pricing](https://cloud.ibm.com/power/estimate){: external} tool. For more information, see [Generating an estimate](/docs/power-iaas?topic=power-iaas-generating-an-estimate).
{: important}

| Hours elapsed in a month  | Amount charged                     | LPAR description                       |
| ------------------------- | ---------------------------------- | -------------------------------------- |
| 300 hours                 | (300 hours x $0.343)/month = $103      | 1 core, 8 GB memory, 150 GB disk, AIX  |
| 430 hours                 | (430 hours x $0.465)/month = $200      | 1 core, 16 GB memory, 150 GB disk, AIX |
| 730 hours (Monthly Total) | $103 + $200 = $303 (Monthly Total) | 1 core, 16 GB memory, 150 GB disk, AIX |
{: caption="Monthly LPAR charges" caption-side="top"}

In this example, the LPAR resources are increased (after reaching 300 hours in the month) from 8 GB to 16 GB of memory. The price of the LPAR is prorated by the hour for the final monthly price of $303.


## Part numbers
{: #part-numbers}

For detailed usage and billing information, you can refer to the part number in your invoice. The part numbers in the invoice represent the charge unit. Refer to the following table to view the part number and its corresponding description.

| Part number  | Description                     |
| ------------------------- | ---------------------------------- |
| SOS_VIRTUAL_PROCESSOR_CORE_HOURS     | Scale out shared uncapped processor per core-hour       |
| SOD_VIRTUAL_PROCESSOR_CORE_HOURS     | Scale out dedicated processor per core-hour      |
| MS_GIGABYTE_HOURS|      Memory standard gigabyte-hour|
| MHU_GIGABYTE_HOURS     | High use RAM (>64 Gb per core) gigabyte-hour      |
| TIER_ONE_STORAGE_GIGABYTE_HOURS     | Tier-1 storage gigabyte-hour      |
| TIER_THREE_STORAGE_GIGABYTE_HOURS     | Tier-3 storage gigabyte-hour     |
| TIER_ZERO_STORAGE_GIGABYTE_HOURS |Tier-0 storage gigabyte-hour |
| FIXED_5K_OPS_GIGABYTE_HOURS |Fixed IOPS storage gigabyte-hour  |
| AIX_SMALL_APPLICATION_INSTANCE_HOURS     | AIX scale out license per core-hour      |
| AIX_MEDIUM_APPLICATION_INSTANCE_HOURS     | AIX enterprise license per core-hour     |
| IBMI_OS_PTEN_APPLICATION_INSTANCE_HOURS     | IBM i OS P10 license per core-hour      |
| IBMI_OS_PTHIRTY_APPLICATION_INSTANCE_HOURS     | IBM i OS P30 license per core-hour      |
| IBMI_LPP_PTEN_APPLICATION_INSTANCE_HOURS     | IBM i LPP P10 license per core-hour      |
| IBMI_LPP_PTHIRTY_APPLICATION_INSTANCE_HOURS     | IBM i LPP P30 license per core-hour     |
| SOC_VIRTUAL_PROCESSOR_CORE_HOURS     | Scale out shared capped processor per core-hour      |
| IBMIHA_PTEN_APPLICATION_INSTANCES     | PowerHA for IBM i P10 license per core-hour      |
| IBMIHA_PTHIRTY_APPLICATION_INSTANCES     | PowerHA for IBM i P30 license per core-hour      |
| IBMICOS_APPLICATION_INSTANCES     | IBM Cloud Storage Solutions for IBM i license per core-hour      |
| IBMIRDS_APPLICATION_INSTANCES     | IBM Rational Development Studio for IBM i license per users-hour      |
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
| S922_DEDICATED_SERVER_HOURS           |  Dedicated host for S922 host per server-hour   |
| S1022_DEDICATED_SERVER_HOURS  |     Dedicated host for S1022 host per server-hour        |
| REDHAT_GP_ON_SCALE_OUT_APP_INSTANCE_HOURS	|    Redhat GP Scale Out License per Core Hour |
| REDHAT_GP_SCALE_UP_LICENSE_CORE_HOURS	    |  Redhat GP Scale Up License per Core Hour |
| REDHAT_SAP_SCALE_OUT_LICENSE_PER_CORE_HOUR	|	Redhat SAP Scale Out License/Core Hour |
| REDHAT_SAP_SCALE_UP_LICENSE_PER_CORE_HOUR	|   Redhat SAP Scale Up License/Core Hour |
| SUSE_OS_GP_TIER_ONE_INSTANCE_HOURS	  |	SUSE GP Tier 1 Instance Hours |
| SUSE_OS_GP_TIER_THREE_INSTANCE_HOURS	|	SUSE GP Tier 3 Instance Hours |
| SUSE_OS_GP_TIER_TWO_INSTANCE_HOURS	  | SUSE GP Tier 2 Instance Hours |
| SUSE_OS_SAP_TIER_ONE_INSTANCE_HOURS	  |	SUSE SAP Tier 1 Instance Hours |
| SUSE_OS_SAP_TIER_THREE_INSTANCE_HOURS	|	SUSE SAP Tier 3 Instance Hours |
| SUSE_OS_SAP_TIER_TWO_INSTANCE_HOURS	  |	SUSE SAP Tier 2 Instance Hours |
| S1022_NW_SHARED_UNCAPPED_CORE_HOURS | S1022 SAP NetWeaver Shared Processor |
| S1022_NW_SHARED_CAPPED_CORE_HOURS | S1022 SAP NetWeaver Dedicated Processor |
| S1022_NW_DEDICATED_CORE_HOURS | S1022 NW Dedicated Processor |
| S1022_NW_MEM_GB_HOURS | S1022 SAP NetWeaver Memory  |
| PTEN_ESS_VIRTUAL_PROCESSOR_CORE_HOURS | E1080 Shared Processor |
| PTEN_EDD_VIRTUAL_PROCESSOR_CORE_HOURS | E1080 Dedicated Processor |
| PTEN_ECC_VIRTUAL_PROCESSOR_CORE_HOURS | E1080 Shared Capped Processor |
| PTEN_MS_GIGABYTE_HOURS | P10 Standard Memory |
| PTEN_MHU_GIGABYTE_HOURS | P10 High Use Memory (>64 Gb per core) |
| PTEN_SOS_VIRTUAL_PROC_CORE_HRS  | S1022 Shared Processor |
| PTEN_SOC_VIRTUAL_PROC_CORE-HRS  | S1022 Shared Capped Processor |
| PTEN_SOD_VIRTUAL_PROC_CORE_HRS  | S1022 Dedicated Processor |
| S1022_SR2_HANA_CORE_HOURS | SAP HANA Workload Optimized Profile (SR2) - S1022 Processor |
| S1022_SR2_HANA_MEM_GB_HOURS | SAP HANA Workload Optimized Profile (SR2) - S1022 Memory  |
| E1080_SR2_HANA_CORE_HOURS | SAP HANA Workload Optimized Profile (SR2) - E1080 Processor  |
| E1080_SR2_HANA_MEM_GB_HOURS | SAP HANA Workload Optimized Profile (SR2) - E1080 Memory  |
| S1022_SH2_HANA_CORE_HOURS  | SAP HANA Workload Small Profile (SH2) - S1022 Processor  |
| S1022_SH2_HANA_MEM_GB_HOURS | SAP HANA Workload Small Profile (SH2) - S1022 Memory  |
| E1080_SH2_HANA_CORE_HOURS | SAP HANA Workload Small Profile (SH2) - E1080 Processor  |
| E1080_SH2_HANA_MEM_GB_HOURS  | SAP HANA Workload Small Profile (SH2) - E1080 Memory |
| TIER_ONE_SNAPSHOT_GIGABYTE_HOURS  | Snapshot Tier One Gigabyte Hours |
| TIER_THREE_SNAPSHOT_GIGABYTE_HOURS  | Snapshot Tier Three Gigabyte Hours |
| TIER_ZERO_SNAPSHOT_GIGABYTE_HOURS.  | Snapshot Tier Zero Gigabyte Hours |
| FIXED_FIVE_K_OPS_SNAPSHOT_GIGABYTE_HOURS  |Snapshot Tier Fixed 5k Gigabyte Hours |
{: caption="Part numbers" caption-side="bottom"}

## Base instances
{: #pricing-base-instance-prices}

The base instance billing depends on your virtual instance options when you create a {{site.data.keyword.powerSys_notm}}. The machine type, number of cores, and amount of memory all affect the base instance billing. When you create your virtual server instance, the associated monthly rate is displayed. For more information, see [Creating a {{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#creating-power-virtual-server).

The pricing for memory is calculated based on a ratio of 64 GB per core. For example, if you use more than 16 GB for 0.25 cores, you must pay a premium high-use RAM price for the excess memory. However, if you use up to 128 GB for 2 cores, you do not have to pay any premium memory price.

## Operating systems
{: #pricing-operating-systems}

The {{site.data.keyword.powerSys_notm}} pricing for AIX and IBM i includes license and IBM software maintenance.

{{site.data.keyword.powerSys_notm}} provides AIX and IBM i stock images. The operating system version levels of the stock images are subject to change.

You can also bring your own custom image to use on a {{site.data.keyword.powerSys_notm}} instance, but you must still purchase an operating system license for virtual server resources. If you bring your own custom image, you are charged for the image size and the storage tier that you use for the image. After you deploy a stock image (and only after deployment), you are charged for the space the image is stored in. The storage unit price (per GB) for the stored boot images is the same as the selected storage tier (Tier 0 or Tier 3) where your boot disks are deployed. To identify the estimated storage rates, use the Cost Estimator tool. To reduce costs, you can capture the virtual machine and delete it when it is not needed. The pricing for AIX and IBM i operating system license is not determined by whether you use a custom image or a stock image. To learn more, go to [Deploying a custom image within IBM {{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-deploy-custom-image).

The {{site.data.keyword.powerSys_notm}} also provides Linux&reg; stock images. You might select a Linux stock image that is provided by IBM or bring your own Red Hat Linux Enterprise (RHEL) and SUSE Linux Enterprise Server (SLES) image OVA format. For a Linux subscription, you might opt to use a [full Linux&reg; subscription](/docs/power-iaas?topic=power-iaas-set-full-Linux) for {{site.data.keyword.powerSys_notm}} or obtain the subscription for the Linux operating system directly from the vendor. For more information about how to create an OVA format Linux image, see [deploying a Linux virtual machine](/docs/power-iaas?topic=power-iaas-linux-deployment).


## Linux for SAP workloads
{: #linux-SAP-workload-types}

You can deploy the following types of SAP workloads as virtual machines:

* **SAP NetWeaver**: For SAP NetWeaver for Linux, the charges for hardware, processors, and memory are similar to other types of Linux deployments. However, the SAP NetWeaver for Linux requires a different type of operating system and license to be deployed. So, the charges for these types of deployments are not same as that of Red Hat Enterprise Linux for SAP (non-SAP OS). SAP NetWeaver can be deployed on both S1022 and E1080 systems.

* **SAP HANA**: For SAP HANA, there are distinct processor and memory billing parts. The charges on these distinct parts appear on the monthly invoices. Similar to other types of deployments, the following types of systems, processors, and memory are supported for SAP HANA:
    - System types: S1022 (for workloads less than 2 TB of RAM) or E1080 (for workloads more than 2 TB of RAM)
    - Virtual processor core types: dedicated, shared capped, or shared uncapped
    - Memory types: scale-out or scale-up

For SAP HANA workloads, the charges for processor and memory parts are the same as compared to non-SAP HANA workloads. To estimate the costs for non-SAP HANA workloads, see Tables 3, 4, 5, and 6.

The pricing is subject to change depending on the SAP HANA operational costs.
{: note}


## Processor types
{: #pricing-processor}

You are charged different rates depending on the processor type that you choose for your virtual machine (VM). **Dedicated processors** are priced the highest as they provide the best overall performance. **Shared capped processors** cost slightly more than **shared uncapped processors** because of their flexibility in addressing licensing restrictions. The processors are all charged on an hourly prorated basis according to the machine type, processor type, and the number of cores used in a month.

Each processor has a different hourly rate depending on its type (**Dedicated** vs **Shared uncapped**). Processors also have a different hourly rate depending on the system that they are on **(Dedicated S922** vs **Dedicated E980**). For information on different processor type functions, see [What's the difference between shared capped and shared uncapped processor performance? How do they compare to dedicated processor performance?](/docs/power-iaas?topic=power-iaas-powervs-faqs#processor).

All prices that are mentioned in the topic are illustrative and do not represent the actual amounts that are used for billing. To generate an estimated price, use the [{{site.data.keyword.powerSys_notm}} cost estimator](https://cloud.ibm.com/power/estimate){: external} tool. For more information, see [Generating an estimate](/docs/power-iaas?topic=power-iaas-generating-an-estimate).
{: important}

The following tables show how different processor types affect the cost per system:

| Number of cores (S922) | Hourly rate (Processor type) | Monthly cost (730 hours) |
| ---------------------- | ---------------------------- | ------------------------ |
| 1                      | $0.51 (dedicated)            | $368.91                  |
| 1                      | $0.13 (shared uncapped)      | $92.33                  |
| 1                      | $0.19 (shared capped)        | $138.38                  |
{: caption="S922 processor type pricing" caption-side="bottom"}

| Number of cores (E980) | Hourly rate (Processor type) | Monthly cost (730 hours) |
| --------------------------- | ---------------------------- | ------------------------ |
| 1                           | $1.77 (dedicated)            | $1291.28               |
| 1                           | $0.44 (shared uncapped)      | $322.84                  |
| 1                           | $0.66 (shared capped)        | $484.26                  |
{: caption="E980 processor type pricing" caption-side="bottom"}

| Number of cores (S1022) | Hourly rate (Processor type) | Monthly cost (730 hours) |
| --------------------------- | ----------------------------- | ------------------------ |
| 1                           | $0.58 (dedicated)            | $424.25                 |
| 1                           | $0.15 (shared uncapped)     | $106.06                  |
| 1                           | $0.22 (shared capped)       | $159.14                  |
{: caption="S1022 processor type pricing" caption-side="bottom"}


## Pricing for dedicated hosts
{: #pricing-dh}

Dedicated hosts are priced based on the host type – either an IBM Power S922 or IBM Power S1022.  Each server type is metered by the hour and the price includes the entire capacity of the host.

Consider the following points for dedicated host pricing:
* You are not charged separately for shared processor pools that you deploy to the dedicated host.
* Software charges for the supported operating systems are metered and charged by the core.


To learn more about the dedicated host, see: [dedicated host](/docs/power-iaas?topic=power-iaas-dedicated-host).

## Storage types
{: #storage-type}

The {{site.data.keyword.powerSys_notm}} charges based on three different storage types:
- **Data volumes**: These are the simplest form of volume that you create. You are billed based on the current volume size at the metering time. The following table shows an example of how you are billed based on your volume creation:
    |Volume size you create|You are billed|
    |----------------------|--------------|
    |10 GB|10 GB|
    |10+5 GB|15 GB|
    {: caption="Calculation of data volume" caption-side="bottom"}

- **Image backing volumes**: These volumes are part of a boot image in your cloud-instance boot image catalog. You are billed based on the total volume sizes contained in the image.
    When the image has a single backing volume, you are billed based on the GB size of the single volume. When the image has multiple backing volumes, you are billed based on tallying up the sizes of all the image backing volumes. The following table shows an example of how you are billed based on your boot volume:

    |Image volume size |Single or multiple backing|You are billed|
    |------------------|--------------------------|--------------|
    |20 GB|Single backing volume|20 GB|
    |Volume 1 (20 GB), volume 2 (10 GB)|Multiple backing volumes|30 GB|
    {: caption="Calculation of image backing volume" caption-side="bottom"}

- **Deployed VM volumes**: These volumes are created when you deploy a VM with an image. The deployed VMs get a copy of all the volumes in the image. Any additional data volumes attached to the deployed VM are already accounted for under Data Volumes. The following table shows an example of how you are billed based on the VMs that you deploy:
   |Image backing volume|You are billed|
    |--------------------|--------------|
    |20 GB|20 GB|
    |20 GB + 30 GB|50 GB|
    {: caption="Calculation of deployed VMs volume" caption-side="bottom"}






### Use case of account billable storage
{: #account-billable-storage}

The following table shows the use case on how you are billed based on the storage that you use (assuming tier 1):

| Name     | Size    | State/Description      |
|----------|---------|------------------------|
|data-volume-1|20 GB|Available|
|data-volume-2|25 GB|In-use (attached to vm-1)|
|data-volume-3|100 GB|In-use (attached to vm-1)|
|data-volume-4|30 GB|Available|
|data-volume-5|60 GB|In-use (attached to vm-2)|
{: class="simple-tab-table"}
{: tab-group="storage"}
{: caption="Account billable for storage use case" caption-side="top"}
{: #storage-spec-1}
{: tab-title="Data volumes of 235 GB"}

| Name     | Size    | State/Description      |
|----------|---------|------------------------|
|AIX-71-01|30 GB|1 backing volume|
|IBMi-74-001| 100 GB + 30 GB|2 backing volumes|
|SLES-15-1|40 GB|1 backing volume|
{: class="simple-tab-table"}
{: tab-group="storage"}
{: caption="Account billable for storage use case" caption-side="top"}
{: #storage-spec-2}
{: tab-title="Boot volumes of 200 GB"}

| Name     | Size    | State/Description    |
|----------|---------|----------------------|
|vm-1 deployed AIX-71|30 GB|Volume of AIX-71 +  \n data-volume-2 +  \n data-volume-3  \n (volumes that are created from copying  \n the deployed AIX-71 image,  \n Data volumes are already accounted.)|
|vm-2 deployed IBMi-74-001|130 GB|Volume of IBMi-74-001 +  \n data-volume-5  \n (volumes that are created from copying  \n the deployed IBMi-74-001 image,  \n Data volumes are already accounted.)|
{: class="simple-tab-table"}
{: tab-group="storage"}
{: caption="Account billable for storage use case" caption-side="top"}
{: #storage-spec-3}
{: tab-title="Deployed VMs of 160 GB"}

Total billable storage = 595 GB

- Data volumes: 235 GB
- Image volumes: 200 GB
- Deployed VMs: 160 GB

## Pricing for IBM {{site.data.keyword.powerSys_notm}} VPN (VPN) connection
{: #pricing-vpn}

When you use a VPN connection, you are billed monthly.

IBM charges with the base price hourly per connection. The base price varies per region. So, if you use one VPN connection that is active for a month, the monthly bill would be the VPN hourly base price for your region X 24 hours X 30 days. For example, if VPN is used in a US region and the US base price is $0.05 per VPN instance, the monthly price would be $36. VPN charges are associated with the {{site.data.keyword.powerSys_notm}} Workspace resource.

[Query-5]{: tag-red}Replaced the word "geography" with "region". Is "region" better or "location"?



## Pricing for Power Edge Router (PER)
{: #per-pricing}

No additional charges are levied for PER in IBM {{site.data.keyword.powerSys_notm}}. You are only charged based on the number of Transit Gateway connections and routing options associated to the use of PER.

The following table shows an example of the charges based on the routing option that you select:

| Routing type | Charges |
|--------------|---------|
|Local routing data transfer | No charges |
|Global routing data transfer | $0.011 GB|
{: caption="An example of Transit Gateway charges based on routing" caption-side="top"}

The following table shows examples of the charges based on the number of connections that includes Direct Link, VPC, Classic that you can create:

| Number of connections | Charges |
|-----------------------|---------|
|1 - 4 | No charges |
|5 - 20 | $9.405 |
|21 - 50 |$7.315 |
|51+ | $4.7025 |
{: caption="Examples of Transit Gateway charges based on number of connections" caption-side="top"}


The Transit Gateway charges indicated in the preceding tables are subjected to change. See the summary of Transit Gateway charges from the [provisioning page](https://cloud.ibm.com/interconnectivity/transit/provision) in the IBM Cloud console. See the [Pricing considerations](/docs/transit-gateway?topic=transit-gateway-helpful-tips#pricing-considerations) section in the Transit Gateway documentation for more information.
{: important}

## End of billing
{: #pricing-end-billing}

The monthly billing cycle ends when you delete the LPAR. If you scale your infrastructure up and down in response to workload requirements, your billing follows the timing of the LPAR provision change. If you stop the LPAR, the billing process is not stopped. You must delete the LPAR to stop the billing cycle.

You are still charged if the VM is in a *suspended state*. When your VM is inactive, you can use Dynamic Logical Partitioning (DLPAR) to resize it to a minimal state. You can drastically decrease the price per hour by reducing the VM's core count and memory.
{: important}
