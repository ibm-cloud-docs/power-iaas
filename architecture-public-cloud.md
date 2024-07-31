---

copyright:
  years: 2023, 2024

lastupdated: "2024-07-29"

keywords: power systems, infrastructure as a service, multiple virtual servers, hybrid cloud environment, linux, aix, ibm i,

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}


# Architecture for IBM {{site.data.keyword.powerSys_notm}} (Off-premises)
{: #on-cloud-architecture}


---

IBM {{site.data.keyword.powerSys_notm}} located in IBM data centers: [Off-premises]{: tag-blue}

---

{{site.data.keyword.powerSysFull}} is located in the IBM data centers, distinct from the IBM Cloud servers with separate networks and direct-attached storage.

Review the following topics to understand the {{site.data.keyword.powerSys_notm}} architecture, key features, and hardware and software requirements:

*  [High-level architecture](#high-level-architecture-on-cloud)
*  [Key features](#key-features-on-cloud)
*  [Hardware specifications](#hardware-specifications-on-cloud)
*  [Data sheets](#data-sheets)
*  [Storage tiers](#storage-tiers)
*  [Public and private networks](#public-private-networks)

## High-level architecture
{: #high-level-architecture-on-cloud}

{{site.data.keyword.powerSys_notm}} is located in the IBM data centers, distinct from the IBM Cloud servers with separate networks and direct-attached storage.

With the {{site.data.keyword.powerSys_notm}}, you can quickly create and deploy one or more virtual servers (that are running either the AIX, IBM i, or Linux operating systems). After you provision the {{site.data.keyword.powerSys_notm}}, you get access to infrastructure and physical computing resources without the need to manage or operate them. However, you must manage the operating system and the software applications and data. The following graphic represents a responsibility assignment (RACI) matrix for {{site.data.keyword.powerSys_notm}}:

![{{site.data.keyword.powerSys_notm}} responsibility assignment matrix](./images/RACI_matrix.png "{{site.data.keyword.powerSys_notm}} responsibility assignment matrix"){: caption="Figure 1. {{site.data.keyword.powerSys_notm}} responsibility assignment matrix" caption-side="bottom"}

## Key features
{: #key-features-on-cloud}

The key features for the {{site.data.keyword.powerSys_notm}} are as follows.

### Straightforward billing
{: #straightforward-billing-on-cloud}

{{site.data.keyword.powerSys_notm}} uses a monthly billing rate that includes the licenses for the AIX, IBM i, or Linux operating systems. The monthly billing rate is pro-rated by the hour based on the resources that are deployed to the {{site.data.keyword.powerSys_notm}} instance for the month. When you create the {{site.data.keyword.powerSys_notm}} instance, you can see the total cost for your configuration based on the options that you specify. You can quickly identify what configuration options provide you with the best value for your business needs. For more information, see [Pricing](/docs/power-iaas?topic=power-iaas-pricing-virtual-server-on-cloud).

Bring your own Linux image (OVA format) and subscription. SLES and RHEL OVA images are supported. For more information, see [Using SLES within the IBM {{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-using-linux).
{: note}

### Infrastructure customization
{: #infra-customization}

You can configure and customize the following options when you create a {{site.data.keyword.powerSys_notm}}:

* Number of virtual server instances
* Number of cores
* Amount of memory
* Data volume size and type
* Network interfaces

### Bring your own image
{: #bring-own-image}

IBM provides you with stock AIX and IBM i images when you create a {{site.data.keyword.powerSys_notm}}. However, you can always [bring your own](/docs/power-iaas?topic=power-iaas-using-linux) custom AIX, IBM i, or Linux image that is tested and deployed.

### Support for SAP NetWeaver or SAP HANA applications
{: #support-SAPNetWeaver-or-SAPHANA}

When you provision a {{site.data.keyword.powerSys_notm}} instance to support SAP NetWeaver applications, select a version of the IBM-provided AIX or Linux stock operating system image. When you provision a {{site.data.keyword.powerSys_notm}} instance to support the SAP HANA applications, select a version of the IBM provided Linux&reg; stock image. IBM i operating system and custom AIX and Linux images are not supported for SAP workloads. For more information about supported operating system versions, see [FAQ](/docs/power-iaas?topic=power-iaas-powervs-faqs). For more information, see [Deploying your infrastructure](https://cloud.ibm.com/docs/sap?topic=sap-vs-set-up-infrastructure){: external}.

When you provision a {{site.data.keyword.powerSys_notm}} to support SAP NetWeaver applications, select a version of the IBM-provided AIX operating system stock image. IBM i and operating system custom images are not supported for SAP workloads.
{: note}

### Support for deploying a Red Hat OpenShift Cluster
{: #support-redhat-openshift}

When you provision a Red Hat OpenShift Cluster on {{site.data.keyword.powerSys_notm}}, it is easier to use the IBM&trade; provided automation to create the entire cluster of servers. You can install Red Hat OpenShift rather than individually provisioning {{site.data.keyword.powerSys_notm}} instances. For instructions to deploy a Red Hat OpenShift Cluster on {{site.data.keyword.powerSys_notm}}, including preparation of the required Operation System images for the cluster, see [Deploying Red Hat OpenShift Container Platform 4.x on IBM {{site.data.keyword.powerSys_notm}}](https://developer.ibm.com/series/deploy-ocp-cloud-paks-power-virtual-server/){: external}.

## Hardware specifications
{: #hardware-specifications-on-cloud}

The following IBM Power server can host a {{site.data.keyword.powerSys_notm}}:
- IBM Power S922 (9009-22A)
- IBM Power S922 (9009-22G)
- IBM Power E980 (9080-M9S)
- IBM Power E1080 (9080-HEX)
- IBM Power S1022 (9105-22A).

For more information about these systems and how they're used inside the {{site.data.keyword.powerSys_notm}}, see their [data sheets](/docs/power-iaas?topic=power-iaas-about-power-iaas#data-sheets) and the hardware overview table.

You can compare the performance of your current environment with the environment available through the {{site.data.keyword.powerSys_notm}}. For more information, see the [IBM Power Performance Report](https://www.ibm.com/downloads/cas/K90RQOW8){: external}.
{: tip}

## Data sheets
{: #data-sheets}

* [IBM Power System S922 (9009-22A)](https://www.ibm.com/downloads/cas/KQ4BOJ3N){: external}
* [IBM Power System E980 (9080-M9S)](https://www.ibm.com/downloads/cas/VX0AM0EP){: external}
* [IBM Power System S1022 (9105-22A) (Power10)](https://www.ibm.com/downloads/cas/MQR4B1RP){: external}
* [IBM Power System E1080 (9080-HEX)](https://www.ibm.com/downloads/cas/MMOYB4YL){: external}

| Compute     | Storage      | Network      |
|------------ | ------------ | ------------ |
| * Power S922 (9009-22A) \n * Power S922 (9009-22G) \n * Power E980 (9080-MHE) \n * Power E1080 (9080-HEX) \n * Power S1022 (9105-22A)| * Flash Storage from IBM FS9000 series devices \n * V7000 SSD (no new VMs) (WDC04 only) \n * 32 GB SAN infrastructure | * Cisco Nexus 9000 93180YC-EX (10G) \n * Cisco Nexus 9000 C9348GC-FXP (1G) \n * Avocent ACS8048 |
{: class="simple-tab-table"}
{: tab-group="hardware"}
{: caption="Table 1. Hardware overview (Washington, D.C.)" caption-side="top"}
{: #hw-spec-1}
{: tab-title="Washington, D.C. (WDC04, WDC06, and WDC07)"}

| Compute  | Storage   | Network   |
|--------- | --------- | --------- |
| * Power S922 (9009-22A) | * Flash Storage from IBM FS9000 series devices \n * V7000 SSD (no new VMs) \n * 32 GB SAN | * Cisco Nexus 9000 C9336PQ (Spine 10G) \n * Cisco Nexus 9000 C93180YC (10G) \n * Cisco Nexus 9000 C93108TC-EX (1G) \n * Cisco UCS - APIC controller \n * Cisco ASR1001-HX Router \n * Avocent ACS8016 |
{: class="simple-tab-table"}
{: tab-group="hardware"}
{: caption="Table 1. Hardware overview (Dallas, TX)" caption-side="top"}
{: #hw-spec-2}
{: tab-title="Dallas (DAL10, DAL12, DAL13)"}

| Compute  | Storage   | Network   |
|--------- | --------- | --------- |
| * Power E980 (9080-M9S) \n * Power S922 (9009-22A) | * Flash Storage from IBM FS9000 series devices \n * 32 Gb SAN infrastructure | * Cisco Nexus 9000 N9K-C9364C (Spine 10G) \n * Cisco Nexus 9000 9348GC-FXP (Leaf 1G) \n * Cisco Nexus 9000 93180YC-FX (Leaf 25G) \n * Cisco UCS - APIC controller \n * Cisco ASR1001-HX Router \n * Avocent ACS8032DAC-400 |
{: class="simple-tab-table"}
{: tab-group="hardware"}
{: caption="Table 1. Hardware overview (Non-US)" caption-side="top"}
{: #hw-spec-4}
{: tab-title="Non-US"}

For a complete list of supported data centers, see [Creating a {{site.data.keyword.powerSys_notm}} workspace](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#creating-service).
{: note}

## Storage tiers
{: #storage-tiers}

IBM {{site.data.keyword.powerSys_notm}} offers you the option to select an I/O operation per second (IOPS) based storage as per your requirement. Flexible IOPS is a tier-less storage offering that removes the notion of disk type and replace it with a storage pool. Each of the storage pools supports multiple storage tiers. The storage tiers are based on different IOPS levels.

The following table shows the supported storage tiers with corresponding IOPS.

| Tier level | IOPS  | Performance |
|---------------|---------------|---------------------|
| Tier 0 | 25 IOPS/GB | A 100-GB volume receives 2500 IOPS. \n This is 2.5x faster than tier 1 and 8.3x faster than tier 3. |
| Tier 1 | 10 IOPS/GB | A 100-GB volume receives 1000 IOPS. \n This is 3.3x faster than tier 3. |
| Tier 3 | 3 IOPS/GB | A 100-GB volume receives 300 IOPS. |
| Fixed IOPS | 5000 IOPS regardless of size | A 100-GB volume receives 5000 IOPS. |
{: caption="Table 2. Tier and IOPS mapping" caption-side="bottom"}

The use of fixed IOPS is limited to volumes with a size of 200 GB or less, which is the break even size with Tier 0 (200 GB @ 25 IOPS/GB = 5000 IOPS).
{: important}

### Working with the APIs
{: #IOPS-api}

Use the [List of all supported storage tiers for this cloud instance](/apidocs/power-cloud#pcloud-cloudinstances-storagetiers-getall) API to see the supported IOPS levels available for your workspace.

The storage tier that you choose does not influence the determination of the storage pool where a volume gets created in. If the storage tier is not specified, then the storage tier is set to Tier 3, by default.

The storage pool selection is based on the use of storage pool or storage affinity parameters. Specifying a storage pool identifies the storage pool directly while storage affinity uses a policy (affinity or anti-affinity) along with an existing volume or virtual server. For flexible IOPS all storage pools, support any tier level. Additionally, the storage tier is not tied to the storage pool.

### Benefits of flexible IOPS
{: #IOPS-benefits}

Flexible IOPS offers multiple IOPS levels (tiers) of storage to choose from. Each IOPS level has its own pricing, performance, and capability.

With flexible IOPS you can:
* Create a volume (or multiple volumes) and specify the IOPS level that you want.
* Change the volume level of IOPS of existing volumes while staying within the same storage pool.
* Clone one or more volumes to your choice of IOPS level. If any of the volumes is greater than 200 GB, then you cannot have a target tier as Fixed IOPS.
* Deploy the boot volume of a virtual server instance in any of the supported IOPS levels. Additional data volumes that are attached to the new virtual server instance can have different IOPS levels from that of the boot volume of an instance.
* Import an image from IBM Cloud Object Storage to any of the supported IOPS levels.

Best practice for an image import is to use the default IOPS level (Tier 3). While deploying the image you can choose the IOPS level for your boot volume during virtual server instance deployment, the boot volume's IOPS level does not need to match the IOPS level of the image.
{: note}

### Selecting a storage tier
{: #IOPS-tier-select}

Flexible IOPS allows you to select a tier that you need for your:
- Boot volume
- Data volume

**Boot volume**
When you are creating a virtual server instance, you can define the boot volume by performing the following steps:
- Select your **Operating system**.
- Select or clear the **Configure for Epic workloads** indicator.
- Select your **Image**.
- Select from **Tier 0**, **Tier 1**, **Tier 3**, or Fixed IOPS.
- For **Storage pool**, select from **Auto-select pool**, **Affinity**, **Anti-affinity**.

| VM storage pool affinity setting | Action |
|----------------------------------|---------|
| Auto-select pool | {{site.data.keyword.powerSys_notm}} determines the best storage pool available for you. |
| Affinity | The storage pool must be similar to the storage pool of affinity object that you choose. |
| Anti-affinity|  Storage pool makes the storage pool of affinity object that you choose as an exception.|
{: caption="Table 3. Storage pool affinity setting" caption-side="bottom"}

All volumes that are created during VM provisioning are created on the same storage pool as the boot volume irrespective of their tier selection.
{: note}

**Data volume**
To create a volume, complete the following steps:
- Enter a unique name.
- Enter the desired size of the volume.
- Enter the quantity of volumes that you need.
- Select from **Tier 0**, **Tier 1**, **Tier 3**, or Fixed IOPS.

During VM provisioning, if you create additional data volumes to attach to the new virtual server instances then these data volumes can be created on any of the supported storage tiers. All these additional data volumes reside in the same storage pool where the boot volume of the virtual server instance resides.

### Limitations of flexible IOPS
{: #IOPS-limit}

Some of the limitations of flexible IOPS are as follows:

- Snapshot data cannot be changed from one tier to another. All volumes of a snapshot must reside in the same storage pool.
- Any volume that has a storage type of tier 0, tier 1, or tier 3 and the volume size is greater than 200 GB then the option to change to Fixed IOPS is not allowed.



## Public and private networks
{: #public-private-networks}

When you create a {{site.data.keyword.powerSys_notm}}, you can select a private or public network interface.

### Public network
{: #public-network}

* Easy and quick method to connect to a {{site.data.keyword.powerSys_notm}} instance.
* IBM configures the network environment to enable a secure public network connection from the internet to the {{site.data.keyword.powerSys_notm}} instance.
* Connectivity is implemented by using an IBM Cloud Virtual Router Appliance (VRA) and a Direct Link Connect connection.
* The public network is protected by a firewall and supports the following secure network protocols:
    * SSH
    * HTTPS
    * Ping
    * IBM i 5250 terminal emulation with SSL (port 992)

### Private network
{: #private-network}

* Allows your {{site.data.keyword.powerSys_notm}} instance to access existing {{site.data.keyword.cloud_notm}} resources, such as IBM Cloud Bare Metal Servers, Kubernetes containers, and Cloud Object Storage.
* Uses a Direct Link Connect connection to connect to your IBM Cloud account network and resources.
* Required for communication between different {{site.data.keyword.powerSys_notm}} instances.

For more information about the different options for configuring a private network, see [Configure a private network subnet](/docs/power-iaas?topic=power-iaas-configuring-subnet).
{: note}
