---

copyright:
  years: 2019, 2025

lastupdated: "2025-04-07"

keywords: pricing, monthly usage, billing process, billing cycle, DLPAR, processor types, linux

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Pricing for IBM {{site.data.keyword.powerSys_notm}} in {{site.data.keyword.off-prem}}s
{: #pricing-virtual-server-on-cloud}

---

{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


---






{{site.data.keyword.powerSysFull}} in {{site.data.keyword.off-prem}} provides a secure and unified billing system for the used hardware and software resources. Metering is done based on resource allocation for the purpose of billing. The following list of resources are metered:

* Virtual machines: CPU (in cores) with processor modes (capped, shared, or dedicated), and memory (in GB)

* Volumes: Storage volumes (in GB)

* Snapshots: Storage snapshots (in GB)

* Dedicated Hosts: Dedicated hosts in host units

In addition to hardware resources, the licensed operating systems and the associated workloads are metered along with virtual machine (VM) resources. For more information about the billing of VM resources, see [Operating systems](https://cloud.ibm.com/docs/power-iaas?topic=power-iaas-pricing-virtual-server-on-cloud#pricing-operating-systems) and [Linux for SAP workloads](https://cloud.ibm.com/docs/power-iaas?topic=power-iaas-pricing-virtual-server-on-cloud#linux-SAP-workload-types).



You can generate an estimate of the resources on the {{site.data.keyword.cloud_notm}} catalog for IBM {{site.data.keyword.powerSys_notm}}. The estimated cost might differ from the actual cost when you purchase the {{site.data.keyword.cloud_notm}} infrastructure or instances. The actual cost might include discounts and promotion codes. For more information, see [Generating an estimate for IBM Power Virtual Server](/docs/power-iaas?topic=power-iaas-generating-an-estimate).

IBM {{site.data.keyword.powerSys_notm}}s are offered in selected regions with scale-out or scale-up logical partitions (LPARs). The IBM Power systems that can host {{site.data.keyword.powerSys_notm}}s have the following theoretical maximums:

All prices that are mentioned in the topic are illustrative and do not represent the actual amounts that are used for billing. To calculate the exact pricing, use the [cost estimator](https://cloud.ibm.com/power/estimate){: external}.
{: important}




|  Power systems         |  Usable cores  |  Memory                     |
|------------------------|--------------|-----------------------------|
| E980 (9080-M9S)        |  143         | Up to 15,307 GB [^1]        |
| S922 (9009-22A) [^2]   |   15         | Up to 942 GB                |
| S1022 (9105-22A) [^3]  |   33         | Up to 1984 GB               |
| E1080 (9080-HEX)       |  165         | Up to 64 TB                 |
| E1050 (9043-MRX)       |   87         | Up to 8,192 GB             |
{: caption="Theoretical maximum processors and memory" caption-side="bottom"}

[^1]: In DAL12, DAL13, OSA21, SAO01, TOK04, WDC04, and WDC06 data centers, the E980 systems allow up to 23,070 GB of memory.

[^2]: If the machine type is S922 and the operating system is IBM i, IBM i supports a maximum of 4 cores per VM.

[^3]: If the machine type is S1022 and the operating system is IBM i, IBM i supports a maximum of 4 cores per VM.


For more information about the availability of the systems for your data center, see the overview page of the [{{site.data.keyword.powerSys_notm}}](https://cloud.ibm.com/power/overview) in the IBM Cloud console.

It is important to note that a theoretical maximum of a system depends on the data center. Also, the {{site.data.keyword.powerSys_notm}} development team enforces the current available resources within each data center. With these processing maximums, the {{site.data.keyword.powerSys_notm}} can meet any business workload requirement.
{: shortdesc}

## Billing details
{: #billing-details}

In your invoice, use one of the following identifiers to identify the charges that apply to the deployed resource instances:

* [Consumer ID](#consumer-id)
    The Consumer ID groups the billing usages that are under a single resource.

* [IBM Cloud Resource Names (CRNs)](#granular-crns)
    The IBM CRNs enable the identification and tracking of Power Virtual Server resources, such as volumes and snapshots, to manage and bill the usage of the resources.


### Consumer ID
{: #consumer-id}

The Consumer ID groups the billing usages that are under a single resource such as VMs, shared processor pools (SPP), and storages. You can view resource usage with broken down metrics.

Following are the benefits of consumer ID:
- You can see a more granular view of your bill by using the **Usage** page in the [Billing and Usage](https://cloud.ibm.com/billing/usage){: external} portal.
- Charges are itemized by resource that is identified in the **Consumer ID** field with the format `resource-type:resource-uuid`.

To view the usage details at the resource level, do the following steps:
1. Open the [Billing and Usage](https://cloud.ibm.com/billing/usage){: external} page in the IBM Cloud console.
2. On the left navigation menu, click **Usage**.
3. Click **View plans** for the entry- **{{site.data.keyword.powerSys_notm}} Workspace**. A page that lists all your workspaces is opened.
4. Click **View details** for a workspace. A page that lists the usage details of a selected workspace is opened.
5. Scroll to the end of the page and click **View instance details**. A page that lists the usage details of the selected virtual server instance is opened.

For more information on the billing and usage page, see [Billing and Usage documentation](https://cloud.ibm.com/docs/account?topic=account-viewingusage&interface=ui){: external}.



### IBM Cloud Resource Names
{: #granular-crns}



IBM Cloud Resource Names (CRNs) are identifiers that are assigned to uniquely identify resources within IBM Cloud.
As CRNs are assigned to individual resources, a comprehensive bill is generated with individual {{site.data.keyword.powerSys_notm}} resource billing.

When you create a resource, {{site.data.keyword.cloud_notm}} assigns a CRN to the resource.

When you delete a workspace, the resources that are associated with the workspace are deleted and then the workspace is deleted. If you are using a dedicated host that is shared with a secondary workspace, remove the secondary workspace resources (VMs) from the dedicated host and then delete the dedicated host workspace.

For more information about {{site.data.keyword.cloud_notm}} CRNs, see [Cloud Resource Names](https://cloud.ibm.com/docs/account?topic=account-crn).



To view or search for resources that are provisioned in IBM {{site.data.keyword.powerSys_notm}} by using the assigned `user tags`, see [Searching for Resources](/docs/account?topic=account-manage_resource&interface=cli#searching-for-resources){: external}. The user tags are not included in the response for GET API and CLI requests.
{: note}



The following table lists the {{site.data.keyword.powerSys_notm}} resources that are CRN enabled.

| Logical Resource | IBM Power Virtual Server in IBM data center | IBM Power Virtual Server Private Cloud in Client location | Billable elements |
| ---------------- | ------------------------------------------- | ---------------------------------------------------------- | ------------- |
| **General**          ||||
| Workspace        | ![Checkmark icon](./images/checkmark.svg)   | ![Checkmark icon](./images/checkmark.svg)                  | * VPN \n * IBM i DB2 Web Query|
|  **Compute**         ||||
| Virtual machine  | ![Checkmark icon](./images/checkmark.svg)   | ![Checkmark icon](./images/checkmark.svg)                  | * Cores \n * Memory \n * SAP workload licenses \n * OS licenses |
| Shared Processor Pool | ![Checkmark icon](./images/checkmark.svg) | ![Checkmark icon](./images/checkmark.svg)               | SPP cores |
| Dedicated Host   | ![Checkmark icon](./images/checkmark.svg)   | X                                                          | Dedicated host capacity |
| **Storage**          ||||
| Volume           | ![Checkmark icon](./images/checkmark.svg)   | ![Checkmark icon](./images/checkmark.svg)                  | * Standard volume storage \n * Image volume storage (onboarded by users) \n * Replicated volume storage \n * Service charges for Global replication services  |
| Snapshot         | ![Checkmark icon](./images/checkmark.svg)   | ![Checkmark icon](./images/checkmark.svg)                  | Snapshot storage |
{: caption="{{site.data.keyword.powerSys_notm}} resources that are CRN enabled." caption-side="bottom"}



## Monthly usage
{: #pricing-monthly-usage}

IBM {{site.data.keyword.powerSys_notm}} instances are charged at a monthly rate that is prorated per hour. If you add resources to an LPAR during the middle of the month, the monthly bill for the LPAR reflects the resource change and the LPAR price that is prorated per hour.

To reduce costs, you can capture and delete the VM when it is not used. For more information, see [Capturing and exporting a virtual machine (VM)](https://cloud.ibm.com/docs/power-iaas?topic=power-iaas-capturing-exporting-vm).

All prices that are mentioned in the topic are illustrative and do not represent the actual amounts that are used for billing. To generate an estimated price, use the [{{site.data.keyword.powerSys_notm}} Estimate pricing](https://cloud.ibm.com/power/estimate){: external} tool. For more information, see [Generating an estimate](/docs/power-iaas?topic=power-iaas-generating-an-estimate).
{: important}

In the following monthly usage example, the customer purchases a {{site.data.keyword.powerSys_notm}} instance with the following configurations at a base price of $250.57 per month ($0.343 per hour):

- One core with 8 GB of memory
- A 150 GB disk
- AIX 7200-03-02 OS.

As the month progresses, the customer adds more memory. The new price for the LPAR is $339.45 per month ($0.465 per hour). The monthly bill is prorated by the hour for the resources deployed.


| Hours elapsed in a month  | Amount charged                     | LPAR description                       |
| ------------------------- | ---------------------------------- | -------------------------------------- |
| 300 hours                 | (300 hours x $0.343)/month = $103      | 1 core, 8 GB memory, 150 GB disk, AIX  |
| 430 hours                 | (430 hours x $0.465)/month = $200      | 1 core, 16 GB memory, 150 GB disk, AIX |
| 730 hours (Monthly Total) | $103 + $200 = $303 (Monthly Total) | 1 core, 16 GB memory, 150 GB disk, AIX |
{: caption="Monthly LPAR charges" caption-side="bottom"}

In this example, if 300 hours is reached in the month, the LPAR resources are increased from 8 GB to 16 GB of memory. The price of the LPAR is prorated by the hour for the final monthly price of $303.


## Part number descriptions
{: #part-numbers}

A part number is associated with the license for the software product to be used in {{site.data.keyword.cloud_notm}}. For detailed usage and billing information, you can refer to the part number descriptions listed in your invoice or in the [IBM&reg; Cloud billing](https://cloud.ibm.com/billing){: external} portal.

Refer to the following table to view the part number descriptions and the associated metric IDs.

| Part description (available on the IBM invoice)  | Metric ID (available in the IBM Cloud catalog)  |
| ------------------------- | ---------------------------------- |
|  **Billing plan: IBM {{site.data.keyword.powerSys_notm}} virtual machine group**  | |
|  IBM Power E1080 shared capped core-hour | power-iaas-metric-E1080-core-capped  |
|  IBM Power E1080 dedicated core-hour | power-iaas-metric-E1080-core-dedicated  |
|  IBM Power E1080 shared uncapped core-hour | power-iaas-metric-E1080-core-shared  |
|  IBM Power E980 shared capped core-hour | power-iaas-metric-E980-core-capped  |
|  IBM Power E980 dedicated core-hour | power-iaas-metric-E980-core-dedicated  |
|  IBM Power E980 shared uncapped core-hour | power-iaas-metric-E980-core-shared  |
|  IBM Power S1022 shared capped core-hour | power-iaas-metric-S1022-core-capped  |
|  IBM Power S1022 dedicated core-hour | power-iaas-metric-S1022-core-dedicated  |
|  IBM Power S1022 shared uncapped core-hour | power-iaas-metric-S1022-core-shared  |
|  IBM Power S922 shared capped core-hour | power-iaas-metric-S922-core-capped  |
|  IBM Power S922 dedicated core-hour | power-iaas-metric-S922-core-dedicated  |
|  IBM Power S922 shared uncapped core-hour | power-iaas-metric-S922-core-shared  |
|  AIX scale-out license core-hour | power-iaas-metric-aix-scale-out  |
|  AIX scale-up license core-hour | power-iaas-metric-aix-scale-up  |
|  SAP HANA workload balanced profile (bh1) - IBM Power E980 core-hour | power-iaas-metric-bh1-hana-core  |
|  SAP HANA workload compute optimized profile (ch1) - IBM Power E980 core-hour | power-iaas-metric-ch1-hana-core  |
|  SAP HANA workload custom profile (cnp) - IBM Power E980 core-hour | power-iaas-metric-hana-core  |
|  SAP HANA workload custom profile (cnp) - IBM Power E980 memory gigabyte-hour | power-iaas-metric-hana-memory  |
|  IBM i Cloud Object Storage instance core-hour | power-iaas-metric-ibmi-cos  |
|  IBM i P10 LPP core-hour | power-iaas-metric-ibmi-lpp-p10  |
|  IBM i P10 LPP - SWMA paid - mobile core-hour | power-iaas-metric-ibmi-lpp-p10-mol  |
|  IBM i P30 LPP core-hour | power-iaas-metric-ibmi-lpp-p30  |
|  IBM i P30 LPP - SWMA paid - mobile core-hour | power-iaas-metric-ibmi-lpp-p30-mol  |
|  IBM i P10 license core-hour | power-iaas-metric-ibmi-os-p10  |
|  IBM i P10 license - SWMA paid - mobile core-hour | power-iaas-metric-ibmi-os-p10-mol  |
|  IBM i P10 service extension core-hour | power-iaas-metric-ibmi-os-p10-sve  |
|  IBM i P30 license core-hour | power-iaas-metric-ibmi-os-p30  |
|  IBM i P30 license - SWMA paid - mobile core-hour | power-iaas-metric-ibmi-os-p30-mol  |
|  IBM i P30 service extension core-hour | power-iaas-metric-ibmi-os-p30-sve  |
|  IBM i P10 - PowerHA instance core-hour | power-iaas-metric-ibmi-pha-p10  |
|  IBM i P30 - PowerHA instance core-hour | power-iaas-metric-ibmi-pha-p30  |
|  IBM i Rational Developer Studio instance-hour | power-iaas-metric-ibmi-rds  |
|  SAP HANA workload memory optimized profile (mh1) - IBM Power E980 core-hour | power-iaas-metric-mh1-hana-core  |
|  SAP NetWeaver workload - IBM Power S1022 shared capped core-hour | power-iaas-metric-netweaver-S1022-capped  |
|  SAP NetWeaver workload - IBM Power S1022 dedicated core-hour | power-iaas-metric-netweaver-S1022-dedicated  |
|  SAP NetWeaver workload - IBM Power S1022 shared uncapped core-hour | power-iaas-metric-netweaver-S1022-shared  |
|  SAP NetWeaver workload - IBM Power S1022 memory gigabyte-hour | power-iaas-metric-netweaver-S1022-memory  |
|  IBM Power10 high-use scale-out memory gigabyte-hour | power-iaas-metric-p10-so-memory-highuse  |
|  IBM Power10 standard scale-out memory gigabyte-hour | power-iaas-metric-p10-so-memory-standard  |
|  IBM Power10 high-use scale-up memory gigabyte-hour | power-iaas-metric-p10-su-memory-highuse  |
|  IBM Power10 standard scale-up memory gigabyte-hour | power-iaas-metric-p10-su-memory-standard  |
|  IBM Power9 high-use memory gigabyte-hour | power-iaas-metric-p9-memory-highuse  |
|  IBM Power9 standard memory gigabyte-hour | power-iaas-metric-p9-memory-standard  |
|  Red Hat Enterprise Linux SAP RISE scale-out license core-hour | power-iaas-metric-rhel-sap-rise-scale-out  |
|  Red Hat Enterprise Linux SAP RISE scale-up license core-hour | power-iaas-metric-rhel-sap-rise-scale-up  |
|  Red Hat Enterprise Linux SAP scale-out license core-hour | power-iaas-metric-rhel-sap-scale-out  |
|  Red Hat Enterprise Linux SAP scale-up license core-hour | power-iaas-metric-rhel-sap-scale-up  |
|  Red Hat Enterprise Linux scale-out license core-hour | power-iaas-metric-rhel-scale-out  |
|  Red Hat Enterprise Linux scale-up license core-hour | power-iaas-metric-rhel-scale-up  |
|  SAP HANA workload small profile (sh2) - IBM Power E1050 core-hour | power-iaas-metric-sh2-hana-E1050-core  |
|  SAP HANA workload small profile (sh2) - IBM Power E1050 memory gigabyte-hour | power-iaas-metric-sh2-hana-E1050-memory  |
|  SAP HANA workload small profile (sh2) - IBM Power E1080 core-hour | power-iaas-metric-sh2-hana-E1080-core  |
|  SAP HANA workload small profile (sh2) - IBM Power E1080 memory gigabyte-hour | power-iaas-metric-sh2-hana-E1080-memory  |
|  SAP HANA workload small profile (sh2) - IBM Power S1022 core-hour | power-iaas-metric-sh2-hana-S1022-core  |
|  SAP HANA workload small profile (sh2) - IBM Power S1022 memory gigabyte-hour | power-iaas-metric-sh2-hana-S1022-memory  |
|  SUSE Linux Enterprise Server SAP tier 1 instance-hour | power-iaas-metric-sles-sap-tier1  |
|  SUSE Linux Enterprise Server SAP tier 2 instance-hour | power-iaas-metric-sles-sap-tier2  |
|  SUSE Linux Enterprise Server SAP tier 3 instance-hour | power-iaas-metric-sles-sap-tier3  |
|  SUSE Linux Enterprise Server tier 1 instance-hour | power-iaas-metric-sles-tier1  |
|  SUSE Linux Enterprise Server tier 2 instance-hour | power-iaas-metric-sles-tier2  |
|  SUSE Linux Enterprise Server tier 3 instance-hour | power-iaas-metric-sles-tier3  |
|  SAP RISE - SAP HANA workload optimized profile (sr2) - IBM Power E1050 core-hour | power-iaas-metric-sr2-hana-E1050-core  |
|  SAP RISE - SAP HANA workload optimized profile (sr2) - IBM Power E1050 memory gigabyte-hour | power-iaas-metric-sr2-hana-E1050-memory  |
|  SAP RISE - SAP HANA workload optimized profile (sr2) - IBM Power E1080 core-hour | power-iaas-metric-sr2-hana-E1080-core  |
|  SAP RISE - SAP HANA workload optimized profile (sr2) - IBM Power E1080 memory gigabyte-hour | power-iaas-metric-sr2-hana-E1080-memory  |
|  SAP RISE - SAP HANA workload optimized profile (sr2) - IBM Power S1022 core-hour | power-iaas-metric-sr2-hana-S1022-core  |
|  SAP RISE - SAP HANA workload optimized profile (sr2) - IBM Power S1022 memory gigabyte-hour | power-iaas-metric-sr2-hana-S1022-memory  |
|  SAP HANA workload ultra-memory optimized profile (umh) - IBM Power E980 core-hour | power-iaas-metric-umh-hana-core  |
|  Virtual Tape Library terabyte-hour | power-iaas-metric-vtl  |
|  IBM Power E1050 shared capped core-hour | ppcaas-metric-E1050-cores-capped  |
|  IBM Power E1050 dedicated core-hour | ppcaas-metric-E1050-cores-dedicated  |
|  IBM Power E1050 shared uncapped core-hour | ppcaas-metric-E1050-cores-shared  |
|  SAP HANA workload - IBM Power E1050 shared capped core-hour | ppcaas-metric-E1050-hana-cores-capped  |
|  SAP HANA workload - IBM Power E1050 dedicated core-hour | ppcaas-metric-E1050-hana-cores-dedicated  |
|  SAP HANA workload - IBM Power E1050 shared uncapped core-hour | ppcaas-metric-E1050-hana-cores-shared  |
|  IBM Power E1080 shared capped core-hour | ppcaas-metric-E1080-cores-capped  |
|  IBM Power E1080 dedicated core-hour | ppcaas-metric-E1080-cores-dedicated  |
|  IBM Power E1080 shared uncapped core-hour | ppcaas-metric-E1080-cores-shared  |
|  SAP HANA workload - IBM Power E1080 shared capped core-hour | ppcaas-metric-E1080-hana-cores-capped  |
|  SAP HANA workload - IBM Power E1080 dedicated core-hour | ppcaas-metric-E1080-hana-cores-dedicated  |
|  SAP HANA workload - IBM Power E1080 shared uncapped core-hour | ppcaas-metric-E1080-hana-cores-shared  |
|  IBM Power S1022 shared capped core-hour | ppcaas-metric-S1022-cores-capped  |
|  IBM Power S1022 dedicated core-hour | ppcaas-metric-S1022-cores-dedicated  |
|  IBM Power S1022 shared uncapped core-hour | ppcaas-metric-S1022-cores-shared  |
|  SAP HANA workload - IBM Power S1022 shared capped core-hour | ppcaas-metric-S1022-hana-cores-capped  |
|  SAP HANA workload - IBM Power S1022 dedicated core-hour | ppcaas-metric-S1022-hana-cores-dedicated  |
|  SAP HANA workload - IBM Power S1022 shared uncapped core-hour | ppcaas-metric-S1022-hana-cores-shared  |
|  AIX scale-up license core-hour | ppcaas-metric-aix-scale-out  |
|  AIX scale-out license core-hour | ppcaas-metric-aix-scale-up  |
|  IBM i Cloud Storage Solutions instance core-hour | ppcaas-metric-ibmi-cos  |
|  IBM i P10 LPP core-hour | ppcaas-metric-ibmi-lpp-p10  |
|  IBM i P10 LPP - SWMA paid - mobile core-hour | ppcaas-metric-ibmi-lpp-p10-mol  |
|  IBM i P30 LPP core-hour | ppcaas-metric-ibmi-lpp-p30  |
|  IBM i P30 LPP - SWMA paid - mobile core-hour | ppcaas-metric-ibmi-lpp-p30-mol  |
|  IBM i P10 license core-hour | ppcaas-metric-ibmi-os-p10  |
|  IBM i P10 license - SWMA paid - mobile core-hour | ppcaas-metric-ibmi-os-p10-mol  |
|  IBM i P10 service extension core-hour | ppcaas-metric-ibmi-os-p10-sve  |
|  IBM i P30 license core-hour | ppcaas-metric-ibmi-os-p30  |
|  IBM i P30 license - SWMA paid - mobile core-hour | ppcaas-metric-ibmi-os-p30-mol  |
|  IBM i P30 service extension core-hour | ppcaas-metric-ibmi-os-p30-sve  |
|  IBM i P10 - PowerHA instance core-hour | ppcaas-metric-ibmi-pha-p10  |
|  IBM i P30 - PowerHA instance core-hour | ppcaas-metric-ibmi-pha-p30  |
|  IBM i Rational Development Studio instance-hour | ppcaas-metric-ibmi-rds  |
|  SAP HANA workload - IBM Power10 standard scale-out memory gigabyte-hour | ppcaas-metric-p10-2u-hana-memory-standard  |
|  IBM Power10 standard scale-out memory gigabyte-hour | ppcaas-metric-p10-2u-memory-standard  |
|  SAP HANA workload - IBM Power10 standard scale-up memory gigabyte-hour | ppcaas-metric-p10-4u-hana-memory-standard  |
|  IBM Power10 standard scale-up memory gigabyte-hour | ppcaas-metric-p10-4u-memory-standard  |
|  Red Hat Enterprise Linux SAP scale-out license core-hour | ppcaas-metric-rhel-sap-scale-out  |
|  Red Hat Enterprise Linux SAP scale-up license core-hour | ppcaas-metric-rhel-sap-scale-up  |
|  Red Hat Enterprise Linux scale-out license core-hour | ppcaas-metric-rhel-scale-out  |
|  Red Hat Enterprise Linux scale-up license core-hour | ppcaas-metric-rhel-scale-up  |
|  SUSE Linux Enterprise Server SAP tier 1 instance-hour | ppcaas-metric-sles-sap-tier1  |
|  SUSE Linux Enterprise Server SAP tier 2 instance-hour | ppcaas-metric-sles-sap-tier2  |
|  SUSE Linux Enterprise Server SAP tier 3 instance-hour | ppcaas-metric-sles-sap-tier3  |
|  SUSE Linux Enterprise Server tier 1 instance-hour | ppcaas-metric-sles-tier1  |
|  SUSE Linux Enterprise Server tier 2 instance-hour | ppcaas-metric-sles-tier2  |
|  SUSE Linux Enterprise Server tier 3 instance-hour | ppcaas-metric-sles-tier3  |
|  Virtual Tape Library terabyte-hour | ppcaas-metric-vtl  |
{: class="simple-tab-table"}
{: tab-group="part_number_descriptions"}
{: caption="Part number descriptions for IBM {{site.data.keyword.powerSys_notm}}." caption-side="bottom"}
{: #virtual-machine-group}
{: tab-title="Virtual machine group"}

| Part description (available on the IBM invoice)  | Metric ID (available in the IBM Cloud catalog)  |
| ------------------------- | ---------------------------------- |
|  **Billing plan: IBM {{site.data.keyword.powerSys_notm}} shared processor pool group**  ||
|  Shared Processor Pool - IBM Power S1022 core-hour | power-iaas-metric-S1022-cores-spp  |
|  Shared Processor Pool - IBM Power E1050 core-hour | power-iaas-metric-E1050-cores-spp  |
|  Shared Processor Pool - IBM Power E1080 core-hour | power-iaas-metric-E1080-cores-spp  |
|  Shared Processor Pool - IBM Power S922 core-hour | power-iaas-metric-S922-cores-spp  |
|  Shared Processor Pool - IBM Power E980 core-hour | power-iaas-metric-E980-cores-spp  |
|  Shared Processor Pool - IBM Power E880 core-hour | power-iaas-metric-E980-cores-spp  |
{: class="simple-tab-table"}
{: tab-group="part_number_descriptions"}
{: caption="Part number descriptions for IBM {{site.data.keyword.powerSys_notm}}." caption-side="bottom"}
{: #shared-processor-pool-group}
{: tab-title="Shared processor pool group"}

| Part description (available on the IBM invoice)  | Metric ID (available in the IBM Cloud catalog)  |
| ------------------------- | ---------------------------------- |
|  **Billing plan: IBM {{site.data.keyword.powerSys_notm}} dedicated host group**  ||
|  IBM Power S922 (15 usable cores; 1 TB memory) dedicated host-hour | power-iaas-metric-S922-dedicated-host  |
|  IBM Power S1022 (33 usable cores; 2 TB memory) dedicated host-hour | power-iaas-metric-S1022-dedicated-host  |
{: class="simple-tab-table"}
{: tab-group="part_number_descriptions"}
{: caption="Part number descriptions for IBM {{site.data.keyword.powerSys_notm}}." caption-side="bottom"}
{: #dedicated-host-group}
{: tab-title="Dedicated host group"}


| Part description (available on the IBM invoice)  | Metric ID (available in the IBM Cloud catalog)  |
| ------------------------- | ---------------------------------- |
|  **Billing plan: IBM {{site.data.keyword.powerSys_notm}} volume group**  ||
|  Volume storage (tier 0: 25 IOPS per GB) gigabyte-hour  | power-iaas-metric-volume-tier0  |
|  Volume storage (tier 1: 10 IOPS per GB) gigabyte-hour | power-iaas-metric-volume-tier1  |
|  Volume storage (tier 3: 3 IOPS per GB) gigabyte-hour | power-iaas-metric-volume-tier3  |
|  Volume storage (tier 5k: 5,000 IOPS) gigabyte-hour | power-iaas-metric-volume-tier5k  |
|  Volume storage (low IOP) gigabyte-hour   | power-iaas-metric-volume-lowiop  |
|  Asynchronous global replication storage gigabyte-hour | power-iaas-metric-volume-async-replication-service  |
|  Asynchronous replicated volume storage (tier 0: 25 IOPS per GB) gigabyte-hour | power-iaas-metric-volume-tier0-async-replicated  |
|  Asynchronous replicated volume storage (tier 1: 10 IOPS per GB) gigabyte-hour | power-iaas-metric-volume-tier1-async-replicated  |
|  Asynchronous replicated volume storage (tier 3: 3 IOPS per GB) gigabyte-hour | power-iaas-metric-volume-tier3-async-replicated  |
|  Asynchronous replicated volume storage (tier 5k: 5,000 IOPS) gigabyte-hour | power-iaas-metric-volume-tier5k-async-replicated  |
{: class="simple-tab-table"}
{: tab-group="part_number_descriptions"}
{: caption="Part number descriptions for IBM {{site.data.keyword.powerSys_notm}}." caption-side="bottom"}
{: #volume-group}
{: tab-title="Volume group"}

| Part description (available on the IBM invoice)  | Metric ID (available in the IBM Cloud catalog)  |
| ------------------------- | ---------------------------------- |
|  **Billing plan: IBM {{site.data.keyword.powerSys_notm}} snapshot group**  ||
|  Snapshot storage (tier 0: 25 IOPS per GB) gigabyte-hour | power-iaas-metric-snapshot-tier0  |
|  Snapshot storage (tier 1: 10 IOPS per GB) gigabyte-hour | power-iaas-metric-snapshot-tier1  |
|  Snapshot storage (tier 3: 3 IOPS per GB) gigabyte-hour | power-iaas-metric-snapshot-tier3  |
|  Snapshot storage (tier 5k: 5,000 IOPS) gigabyte-hour | power-iaas-metric-snapshot-tier5k  |
{: class="simple-tab-table"}
{: tab-group="part_number_descriptions"}
{: caption="Part number descriptions for IBM {{site.data.keyword.powerSys_notm}}." caption-side="bottom"}
{: #snapshot-group}
{: tab-title="Snapshot group"}






## Base instances
{: #pricing-base-instance-prices}

The base instance billing depends on your virtual instance options when you create a {{site.data.keyword.powerSys_notm}}. The machine type, number of cores, and amount of memory all affect the base instance billing. When you create your virtual server instance, the associated monthly rate is displayed. For more information, see [Creating a {{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#creating-power-virtual-server).

The pricing for memory is calculated based on a ratio of 64 GB per core. For example, if you use more than 16 GB for 0.25 cores, you must pay a premium high-use RAM price for the excess memory. However, if you use up to 128 GB for 2 cores, you do not have to pay any premium memory price.

## Operating systems
{: #pricing-operating-systems}

The {{site.data.keyword.powerSys_notm}} pricing for AIX and IBM i includes license and IBM software maintenance.

{{site.data.keyword.powerSys_notm}} provides AIX and IBM i stock images. The operating system version levels of the stock images are subject to change.

You can bring your own custom AIX or IBM i image to use on a {{site.data.keyword.powerSys_notm}} instance, but you must purchase an operating system license for virtual server resources. The pricing for AIX and IBM i operating system license is not based on whether you use a custom image or a stock image.

IBM {{site.data.keyword.powerSys_notm}} also provides Linux&reg; stock images. You can select a Linux stock image that is provided by IBM or bring your own Red Hat Linux Enterprise (RHEL) and SUSE Linux Enterprise Server (SLES) image OVA format. For a Linux subscription, you can opt to use a [full Linux&reg; subscription](/docs/power-iaas?topic=power-iaas-set-full-Linux) for {{site.data.keyword.powerSys_notm}} or obtain the subscription for the Linux operating system directly from the vendor. For more information about how to create an OVA format Linux image, see [deploying a Linux virtual machine](/docs/power-iaas?topic=power-iaas-linux-deployment).

If you bring your own image, you are charged for the image size and the storage tier that you use for the image. The storage unit price (per GB) for stored boot images is the same as the selected storage tier (Tier 0 or Tier 3) in which your boot disks are deployed. To generate an estimated price, use the [{{site.data.keyword.powerSys_notm}} Estimate pricing](https://cloud.ibm.com/power/estimate){: external} tool. For more information, see [Deploying a custom image within IBM {{site.data.keyword.powerSys_notm}}](https://cloud.ibm.com/docs/power-iaas?topic=power-iaas-deploy-custom-image).


## Linux for SAP workloads
{: #linux-SAP-workload-types}

You can deploy the following types of SAP workloads as virtual machines:

* **SAP NetWeaver**: For SAP NetWeaver for Linux, the charges for hardware, processors, and memory are like other types of Linux deployments. However, the SAP NetWeaver for Linux requires a different type of operating system and license to be deployed. So, the charges for these types of deployments are not the same as that of Red Hat Enterprise Linux for SAP (non-SAP OS). SAP NetWeaver can be deployed on S1022, E1080, S922, and E980 systems.

* **SAP HANA**: For SAP HANA, the billing parts for processor and memory are distinct. The charges on these distinct parts appear on the monthly invoices. The following types of systems, processors, and memory are supported for SAP HANA:
    - System types: S1022 (for workloads less than 2 TB of RAM), E1080 (for workloads more than 2 TB of RAM), or E980.
    - Virtual processor core type: dedicated
    - Memory types: scale-out or scale-up

For SAP HANA workloads, the charges for processor and memory parts are the same as compared to non-SAP HANA workloads.

The pricing is subject to change depending on the SAP HANA operational costs.
{: note}

You can also bring your own SAP (HANA or NetWeaver) image with your own subscription. For more information, see [Deploying a Linux for SAP (HANA or NetWeaver) custom image](https://cloud.ibm.com/docs/power-iaas?topic=power-iaas-deploying-SAP-image).


## Processor types
{: #pricing-processor}

You are charged different rates based on the processor type that you choose for your virtual machine (VM). **Dedicated processors** are priced the highest as they provide the best overall performance. **Shared capped processors** cost slightly more than **shared uncapped processors** because of their flexibility in addressing licensing restrictions. The processors are all charged on an hourly prorated basis according to the machine type, processor type, and the number of cores used in a month.

Processor cores are charged at different hourly rates based on the core type (**Dedicated**, **Shared uncapped**, or **Shared capped**) and the machine type (S922, E1080, S1022, or E1080). For information on different processor type functions, see [What's the difference between shared capped and shared uncapped processor performance? How are they compared with dedicated processor performance?](/docs/power-iaas?topic=power-iaas-powervs-faqs#processor).

All prices that are mentioned in the topic are illustrative and do not represent the actual amounts that are used for billing. To generate an estimated price, use the [{{site.data.keyword.powerSys_notm}} cost estimator](https://cloud.ibm.com/power/estimate){: external} tool. For more information, see [Generating an estimate](/docs/power-iaas?topic=power-iaas-generating-an-estimate).
{: important}

The following tables show examples of how different processor types affect the cost per system:

| Number of cores (S922) | Hourly rate (Processor type) | Monthly cost (730 hours) |
| ---------------------- | ---------------------------- | ------------------------ |
| 1                      | $0.51 (dedicated)            | $368.91                  |
| 1                      | $0.13 (shared uncapped)      | $92.33                  |
| 1                      | $0.19 (shared capped)        | $138.38                  |
{: caption="S922 processor type pricing example" caption-side="bottom"}

| Number of cores (E980) | Hourly rate (Processor type) | Monthly cost (730 hours) |
| --------------------------- | ---------------------------- | ------------------------ |
| 1                           | $1.77 (dedicated)            | $1291.28               |
| 1                           | $0.44 (shared uncapped)      | $322.84                  |
| 1                           | $0.66 (shared capped)        | $484.26                  |
{: caption="E980 processor type pricing example" caption-side="bottom"}

| Number of cores (S1022) | Hourly rate (Processor type) | Monthly cost (730 hours) |
| --------------------------- | ----------------------------- | ------------------------ |
| 1                           | $0.58 (dedicated)            | $424.25                 |
| 1                           | $0.15 (shared uncapped)     | $106.06                  |
| 1                           | $0.22 (shared capped)       | $159.14                  |
{: caption="S1022 processor type pricing example" caption-side="bottom"}

## Pricing for shared processor pool
{: #price-spp}


Shared processor pool (SPP) provides the capability to manage CPU cores efficiently. The number of cores that are assigned to an SPP depends on the entitled cores (EC) and virtual cores (VC) ratio. The EC:VP ratio varies by system type. For example, Power10 systems allow different ratios as compared to Power9 systems. For more information, see [Managing the shared processor pool](/docs/power-iaas?topic=power-iaas-manage-SPP).




Shared Processor Pool (SPP) metering is optimized to improve the Total Cost of Ownership (TCO) for AIX and IBM i software licensing and disaster recovery (DR) scenarios. Virtual servers that are configured within an SPP do not incur additional cost per VM core or the cost for high-use memory parts.










## Pricing for dedicated hosts
{: #pricing-dh}

Dedicated hosts are priced based on the host type – either an IBM Power S922 or IBM Power S1022. Each server type is metered by the hour and the price includes the entire capacity of the host.

Consider the following points for dedicated host pricing:
* You are not charged separately for SPPs that you deploy to the dedicated host.
* Software charges for the supported operating systems are metered and charged by the core.


To learn more about the dedicated host, see: [dedicated host](/docs/power-iaas?topic=power-iaas-dedicated-host).

## Storage types
{: #storage-type}

The {{site.data.keyword.powerSys_notm}} charges based on three different storage types:
- **Data volumes** are the simplest form of volume that you create. You are billed based on the current volume size at the metering time. The following table shows an example of how you are billed based on your volume creation:

    |Volume size that you create| Volume size that you are billed|
    |----------------------|--------------|
    |10 GB|10 GB|
    |10+5 GB|15 GB|
    {: caption="Calculation of data volume" caption-side="bottom"}

- **Image backing volumes** are part of a boot image in your cloud-instance boot image catalog. You are billed based on the total volume sizes that are contained in the image.
    When the image has a single backing volume, you are billed based on the GB size of the single volume. When the image has multiple backing volumes, you are billed based on tallying up the sizes of all the image backing volumes. The following table shows an example of how you are billed based on your boot volume:

    |Image volume size |Single or multiple backing|You are billed|
    |------------------|--------------------------|--------------|
    |20 GB|Single backing volume|20 GB|
    |Volume 1 (20 GB), volume 2 (10 GB)|Multiple backing volumes|30 GB|
    {: caption="Calculation of image backing volume" caption-side="bottom"}

- **Deployed VM volumes** are created when you deploy a VM with an image. The deployed VMs get a copy of all the volumes in the image. Any additional data volumes attached to the deployed VM are already accounted for under Data Volumes. The following table shows an example of how you are billed based on the VMs that you deploy:

    |Image backing volume|You are billed|
    |--------------------|--------------|
    |20 GB|20 GB|
    |20 GB + 30 GB|50 GB|
    {: caption="Calculation of deployed VMs volume" caption-side="bottom"}


- **Deployed virtual machine snapshots** are the snapshots of the volumes that are taken after the virtual machine is deployed. The size of the volume snapshot is related to the number of updates that are made to the virtual machine. When you take a snapshot for the first time, the size of the snapshot is a fraction of the size of one or more volumes of the virtual machine. The size of subsequent snapshots might increase based on the changes that are made to the original volume.

For an example, consider a virtual machine with a volume of 100 GB. The size of the first snapshot is 100 GB. The size of the second snapshot might be 1 GB.

Snapshot sizes are not predictable as they are related to the updates made to the volume between two snapshots.
{: note}


The following tables show examples of how different storage types affect the cost per system:

| Volume storage           | Hourly rate (Processor type)  | Monthly cost (730 hours)  |
|  ----------------------  | ----------------------------  | ------------------------  |
|  Tier 0                  | $0.00029589                   | $0.22                     |
|  Tier 1                  | $0.00024658                   | $0.18                     |
|  Tier 3                  | $0.00012884                   | $0.09                     |
|  Tier 5k                 | $0.00035507                   | $0.26                     |
{: caption="Volume storage pricing example" caption-side="bottom"}

| Snapshot storage         | Hourly rate (Processor type)  | Monthly cost (730 hours)  |
|  ----------------------  | ----------------------------  | ------------------------  |
|  Tier 0                  | $0.00008877                   | $0.06                     |
|  Tier 1                  | $0.00007397                   | $0.05                     |
|  Tier 3                  | $0.00003865                   | $0.03                     |
|  Tier 5k                 | $0.00010652                   | $0.08                     |
{: caption="Snapshot storage pricing example" caption-side="bottom"}








### Use case of account billable storage
{: #account-billable-storage}

The following table shows the use case on how you are billed based on the storage that you use (assuming tier 1):

| Name     | Size    | State      |
|----------|---------|------------------------|
|data-volume-1|20 GB|Available|
|data-volume-2|25 GB|In-use (attached to vm-1)|
|data-volume-3|100 GB|In-use (attached to vm-1)|
|data-volume-4|30 GB|Available|
|data-volume-5|60 GB|In-use (attached to vm-2)|
{: class="simple-tab-table"}
{: tab-group="storage"}
{: caption="Account billable for storage use case" caption-side="bottom"}
{: #storage-spec-1}
{: tab-title="Data volumes of 235 GB"}

| Name     | Size    | Description      |
|----------|---------|------------------------|
|AIX-71-01|30 GB|1 backing volume|
|IBMi-74-001| 100 GB + 30 GB|2 backing volumes|
|SLES-15-1|40 GB|1 backing volume|
{: class="simple-tab-table"}
{: tab-group="storage"}
{: caption="Account billable for storage use case" caption-side="bottom"}
{: #storage-spec-2}
{: tab-title="Boot volumes of 200 GB"}

| Name     | Size    | Description    |
|----------|---------|----------------------|
|vm-1 deployed AIX-71|30 GB|Volume of AIX-71 +  \n data-volume-2 +  \n data-volume-3  \n (volumes that are created from copying  \n the deployed AIX-71 image,  \n Data volumes are already accounted.)|
|vm-2 deployed IBMi-74-001|130 GB|Volume of IBMi-74-001 +  \n data-volume-5  \n (volumes that are created from copying  \n the deployed IBMi-74-001 image,  \n Data volumes are already accounted.)|
{: class="simple-tab-table"}
{: tab-group="storage"}
{: caption="Account billable for storage use case" caption-side="bottom"}
{: #storage-spec-3}
{: tab-title="Deployed VMs of 160 GB"}

Total billable storage = 595 GB

- Data volumes: 235 GB
- Image volumes: 200 GB
- Deployed VMs: 160 GB

## Pricing for IBM {{site.data.keyword.powerSys_notm}} VPN (VPN) connection
{: #pricing-vpn}

When you use a VPN connection, you are billed monthly.

IBM charges with the base price hourly per connection. The base price varies per region. So, if you use one VPN connection that is active for a month, the monthly bill would be the VPN hourly base price for your region X 24 hours X 30 days. For example, if VPN is used in a US region and the US base price is $0.05 per VPN instance, the monthly price would be $36. VPN charges are associated with the {{site.data.keyword.powerSys_notm}} workspace resource.

On `July 14, 2025`, the {{site.data.keyword.powerSys_notm}} VPNaaS product will reach its end of life. If you are using {{site.data.keyword.powerSys_notm}} VPNaaS product, you are encouraged to move to the [IBM Cloud VPC VPN](/docs/power-iaas?topic=power-iaas-VPN-connections#vpc-vpn) to avoid VPN service interruptions.
{: important}

## Pricing for Power Edge Router (PER)
{: #per-pricing}

No additional charges are levied for PER in IBM {{site.data.keyword.powerSys_notm}}. You are only charged based on the number of Transit Gateway connections and routing options that are associated to the use of PER.

The following table shows an example of the charges based on the routing option that you select:

| Routing type | Charges |
|--------------|---------|
|Local routing data transfer | No charges |
|Global routing data transfer | $0.011 GB|
{: caption="An example of Transit Gateway charges based on routing" caption-side="bottom"}

The following table shows examples of the charges based on the number of connections that includes Direct Link, VPC, Classic that you can create:

| Number of connections | Charges |
|-----------------------|---------|
|1 - 4 | No charges |
|5 - 20 | $9.405 |
|21 - 50 |$7.315 |
|51+ | $4.7025 |
{: caption="Examples of Transit Gateway charges based on number of connections" caption-side="bottom"}

The Transit Gateway charges indicated in the preceding tables are subjected to change. See the summary of Transit Gateway charges from the [provisioning page](https://cloud.ibm.com/interconnectivity/transit/provision) in the IBM Cloud console. See the [Pricing considerations](/docs/transit-gateway?topic=transit-gateway-helpful-tips#pricing-considerations) section in the Transit Gateway documentation for more information.
{: important}

## End of billing
{: #pricing-end-billing}

The monthly billing cycle ends when you delete the LPAR. If you scale your infrastructure up and down in response to workload requirements, your billing follows the timing of the LPAR provision change. If you stop the LPAR, the billing process is not stopped. You must delete the LPAR to stop the billing cycle.

You are still charged if the VM is in a *suspended state*. When your VM is inactive, you can use Dynamic Logical Partitioning (DLPAR) to resize it to a minimal state. You can drastically decrease the price per hour by reducing the VM's core count and memory.
{: important}
