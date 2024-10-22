---

copyright:
  years: 2023, 2024

lastupdated: "2024-10-21"

keywords: power systems, infrastructure as a service, multiple virtual servers, hybrid cloud environment, linux, aix, ibm i,

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}


# Architecture for IBM {{site.data.keyword.powerSys_notm}} ({{site.data.keyword.on-prem}})
{: #private-cloud-architecture}


---



{{site.data.keyword.on-prem-fname}}: [{{site.data.keyword.on-prem}}]{: tag-red}


---

{{site.data.keyword.powerSysFull}} is an as-a-service offering that includes a prescriptive set of physical infrastructure (compute, network, and storage). The physical infrastructure is deployed in your data center. The site reliability engineers (SREs) from IBM maintain and operates this infrastructure and manage it through the IBM Cloud platform.

To understand the {{site.data.keyword.on-prem}} architecture, key features, and hardware and software requirements, review the following topics:

*  [High-level architecture](#high-level-architecture-private-cloud)
*  [Key features](#key-features)
*  [Hardware and software specifications](#hardware-software-specs-private-cloud)
*  [Network](#network-spec-private-cloud)

## High-level architecture
{: #high-level-architecture-private-cloud}

The following diagram provides a high-level architectural view IBM {{site.data.keyword.powerSys_notm}} ({{site.data.keyword.on-prem}}):

![High-level IBM {{site.data.keyword.powerSys_notm}} ({{site.data.keyword.on-prem}}) architecture](./figures/PPC-network-arc-Sept.png "High-Level IBM {{site.data.keyword.powerSys_notm}} ({{site.data.keyword.on-prem}}) architecture"){: caption="High-Level IBM {{site.data.keyword.powerSys_notm}} ({{site.data.keyword.on-prem}}) architecture" caption-side="bottom"}

## Key features
{: #key-features}

The key features for the {{site.data.keyword.on-prem}} version of IBM {{site.data.keyword.powerSys_notm}} are as follows:

* **Easy management and automation interfaces**: You can easily manage your {{site.data.keyword.powerSys_notm}} resources by using GUI, CLI, API, or Terraform interfaces.
* **Bring your own image**: You can bring your own custom IBM AIX, Linux&reg;, or IBM i image that is tested and deployed. Currently, the supported images include the following operating system images:
    * IBM AIX 7.2, or later
    * IBM i 7.3, or later and IBM i COR [^1] 
    * Red Hat Enterprise Linux (RHEL)
    * SUSE Linux Enterprise Server (SLES)
    * Red Hat Enterprise Linux CoreOS (RHCOS) for OpenShift Container Platform

    [^1]: IBM i Cloud Optical Repository (COR) is a virtual image that can be deployed and used as a Network File Server (NFS) to perform various IBM i tasks that require media. For more information on COR images, see [Cloud Optical Repository](https://cloud.ibm.com/media/docs/downloads/power-iaas/Cloud_Optical_Repository.pdf){: external}.

* **Dynamic resource adjustment**: You can configure and customize the following resources on the virtual server when you work with IBM {{site.data.keyword.powerSys_notm}}({{site.data.keyword.on-prem}}):
    - Number of cores
    - Amount of memory
    - Storage volume size
* **Shared (capped and uncapped) and dedicated virtual machine**: When you deploy a virtual machine, you can choose one of the following options for the type of core:
    - **Shared capped**: The processor is shared among other virtual machines but the partition cannot use higher number of cores than the assigned numbers unlike shared uncapped processor partitions. This option is used mostly for licensing purposes.
    - **Shared uncapped**: The processor is shared among other virtual machines.
    - **Dedicated**: The processor is allocated for the specific virtual machine.

* **Colocation policies for virtual machines and volumes**: You can apply an affinity or anti-affinity policy to each virtual machine instance to control the server on which a new virtual machine is placed. You can build high availability infrastructure within a data center by using this feature.
* **Volume snapshot and clone operations**: You can capture full, point-in-time copies of the virtual machines or data sets. You can create delta snapshots, volume clones, and restore your disks by using IBM FlashCopy feature on {{site.data.keyword.powerSys_notm}}.
* **Entitled processor-to-virtual-processor ratio**: The core-to-virtual core ratio can be in the range of 1:1 to 1:20. For shared processors, fractional cores round up to the nearest whole number. For example, 1.25 cores equal 2 virtual cores.

## Hardware and software specifications
{: #hardware-software-specs-private-cloud}

For more information about IBM Cloud regions can host connections from the pods for IBM {{site.data.keyword.powerSys_notm}}({{site.data.keyword.on-prem}}), see [IBM Satellite location](/docs/power-iaas?topic=power-iaas-satellite-location-spec-private-cloud).

### Pods
{: #pod-spec-private-cloud}

The following pod sizes are available:
* Small: 1 rack of IBM Power10 (S1022 and E1050) processors
* Medium: 2 – 4 racks of IBM Power10 (S1022, E1050, or E1080) processors.

You can expand the pod by adding more compute nodes up to a specific maximum number. This limit is related to the configuration size of the pod. For example, if you start the pod with 5 nodes, you can later add 3 more nodes. The pods are equipped with a spare compute node per compute type. For example, 1 compute node for each group of IBM Power E1080 processors. The spare nodes is used for maintenance or automatic high availability purposes.
You can use 100% of the core, memory, and storage of the nodes by excluding the spare nodes.

The spare node is used by the IBM site reliability engineering (SRE) team for maintenance and is not available for your use.
{: note}






### Small pod configurations
{: #pod-config-small}

A small pod has 1x42U rack and S1022 and E1050 system types are supported in the rack.

[Table 1](#single-rack) illustrates the available configurations for server types and memory types on small pod that has one rack. [Table 2](#single-rack-storage) illustrates the available configurations for storage types on small pod with flash system storage options.


| Server types                | Min   | Min | Max |
| --------------------------- | ------|-----|---- |
| Server quantity in a pod    | 6     | 5   | 9   |
| Number of cores per server  | 40    | 40  | 40  |
| Total number of cores       | 240   | 200 | 360 |
| Usable cores                | 198   | 165 | 297 |
|                             |       |     |     |
| **Memory types**            |       |     |     |
| 2 TB                        | 12    | -   | 18  |
| 4 TB                        | -     | 20  | 36  |
| 8 TB                        | -     | -   | -   |
{: class="simple-tab-table"}
{: tab-group="host_selection"}
{: caption="Small pod configuration." caption-side="top"}
{: #single-rack}
{: tab-title="S1022"}

| Server types                | Min      | Max |
| --------------------------- | -------- | --- |
| Server quantity in a pod    | 2        | 4   |
| Number of cores per server  | 96       | 96  |
| Total number of cores       | 192      | 384 |
| Usable cores                | 170      | 340 |
|                             |          |     |
| **Memory types**            |          |     |
| 2 TB                        |  -       | -   |
| 4 TB                        |  -       | -   |
| 8 TB                        | 16       | 32  |
{: class="simple-tab-table"}
{: tab-group="host_selection"}
{: caption="Small pod configuration." caption-side="top"}
{: #single-rack}
{: tab-title="E1050"}

The small pod with one rack is available with FS 230 TB flash system storage.

| Storage types                         | FS 230 TB |        |
| ------------------------------------- | ----------|--------|
| Number of racks                       | 1         |   1    |
| Drives for each flash system          | 12        | 12     |
| Capacity for each drive in TB         | 19.2      | 19.2   |
| Number of flash systems in a pod      | 1         | 2      |
| Total drives in a pod                 | 12        | 24     |
| Total capacity in TB                  | 230       | 460    |
| Usable capacity in TB                 | 219       | 438    |
| Usable capacity in TB at 2x compression | 438        | 876    |
{: caption="Small pod with flash system storage configuration." caption-side="top"}
{: #single-rack-storage}

### Medium pod configurations
{: #pod-config-medium}


A  medium pod has 2x42 U or 4x42 U rack and S1022, E1050, and E1080 (2CEC) system types are supported in the rack.

[Table 3](#multi-rack) illustrates the available configurations for server types and memory types on medium pod storage options. [Table 4](#multi-rack-storage) illustrates the available configurations for storage types on medium pod with flash system storage options.

|  Server types               | Min   | Max | Min | Max  |
| --------------------------- | ------|-----|-----|------|
| Number of racks             | 2     |  2  | 4   |  4   |
| Server quantity in a pod    | 12    | 15  | 16  | 40   |
| Number of cores per server  | 40    | 40  | 40  | 40   |
| Total number of cores       | 480   | 600 | 640 | 1600 |
| Usable cores                | 396   | 495 | 528 | 1320 |
| **Memory types**            |       |     |     |      |
| 2 TB                        | 24    | 30  | 32  | 80   |
| 4 TB                        | 48    | 60  | 64  | 160  |
| 8 TB                        |  -    |  -  | -   |  -   |
| 16 TB                       |  -    |  -  | -   |  -   |
| 32 TB                       |  -    |  -  | -   |  -   |
{: class="simple-tab-table"}
{: tab-group="host_selection_multi_rack"}
{: caption="Medium pod configuration." caption-side="top"}
{: #multi-rack}
{: tab-title="S1022"}

| Server types                | Min      | Max  | Min   | Max  |
| --------------------------- | -------- | ---- | ----- | ---- |
| Number of racks             | 2        | 2    | 4     | 4    |
| Server quantity in a pod    | 5        | 7    | 8     | 19   |
| Number of cores per server  | 96       | 96   | 96    | 96   |
| Total number of cores       | 480      | 672  | 768   | 1824 |
| Usable cores                | 425      | 595  | 680   | 1615 |
| **Memory types**            |          |      |       |      |
| 2 TB                        |  -       |  -   |  -    |  -   |
| 4 TB                        | 20       | 28   |  32   | 76   |
| 8 TB                        | 40       | 56   | 64    | 152  |
| 16 TB                       |  -       |  -   |  -    |  -   |
| 32 TB                       |  -       |  -   |  -    |  -   |
{: class="simple-tab-table"}
{: tab-group="host_selection_multi_rack"}
{: caption="Medium pod configuration." caption-side="top"}
{: #multi-rack}
{: tab-title="E1050"}

| Server types                | Min          | Max |
| --------------------------- | -------------| --- |
| Number of racks             | 4            | 4   |
| Server quantity in a pod    | 2            | 5   |
| Number of cores per server  | 120          | 120 |
| Total number of cores       | 240          | 600 |
| Usable cores                | 214          | 535 |
| **Memory types**            |              |     |
| 2 TB                        |  -           | -   |
| 4 TB                        |  -           |  -  |
| 8 TB                        | 16           | 40  |
| 16 TB                       | 32           | 80  |
| 32 TB                       | 64           | 160 |
{: class="simple-tab-table"}
{: tab-group="host_selection_multi_rack"}
{: caption="Medium pod configuration." caption-side="top"}
{: #multi-rack}
{: tab-title="E1080 (2CEC)"}

The medium pod with two or four racks is available with FS 460 TB or FS 920 TB flash system storage.

| Storage types                         | Min                    | Max  | Min   | Max  |
| ------------------------------------- | -----------------------|----- | ------|------|
| Drives for each flash system          | 24                     | 48   | 24    | 48   |
| Capacity for each drive in TB         | 19.2                   | 19.2 | 19.2  | 19.2 |
| Number of flash systems in a pod      | 1                      | 1    | 2     | 2    |
| Total Drives in a pod                 | 24                     | 48   | 48    | 96   |
| Total capacity in TB                  | 460                    | 920  | 920   | 1840 |
| Usable capacity in TB                 | 438                    | 876  | 876   | 1752 |
| Usable capacity in TB at 2x compression | 876                  | 1752 | 1752  | 3504 |
{: class="simple-tab-table"}
{: tab-group="host_selection_storage_multi"}
{: caption="Medium pod with flash system storage configuration." caption-side="top"}
{: #multi-rack-storage}
{: tab-title="2 or 4 racks"}

| Storage types                         | Min   | Max  | Min   | Max   |
| ------------------------------------- | ----- | ---- | ----- | ----- |
| Drives for each flash system          | 24    | 48   | 24    | 48    |
| Capacity for each drive in TB         | 19.2  | 19.2 | 19.2  | 19.2  |
| Number of flash systems in a pod      | 3     | 3    | 4     | 4     |
| Total Drives in a pod                 | 72    | 144  | 96    | 192   |
| Total capacity in TB                  | 1380  | 2760 | 1840  | 3680  |
| Usable capacity in TB                 | 1314  | 2628 | 1752  | 3504  |
| Usable capacity in TB at 2x compression | 2628  | 5256 | 3504  | 7007  |
{: class="simple-tab-table"}
{: tab-group="host_selection_storage_multi"}
{: caption="Medium pod with flash system storage configuration." caption-side="top"}
{: #multi-rack-storage}
{: tab-title="4 racks"}




### Supported Power10 servers
{: #power-system-spec-private-cloud}

The following Power10 are supported:

* [IBM Power S1022](https://www.ibm.com/downloads/cas/MQR4B1RP){: external}
* [IBM Power E1050](https://www.ibm.com/downloads/cas/MKQOQAYV){: external}
* [IBM Power E1080](https://www.ibm.com/downloads/cas/MMOYB4YL){: external}

### Operating systems
{: #os-spec-private-cloud}

The Power10 supports Linux, AIX, or IBM i operating system.

IBM {{site.data.keyword.powerSys_notm}} {{site.data.keyword.on-prem}} provides a complete Red Hat Enterprise Linux (RHEL) offering experience with RHEL stock images. The offering includes support from IBM and access to RHEL bug fixes from Satellite servers that are hosted in IBM Cloud. Currently, you must bring your own licenses for all the other operating system images. For more flexibility, you can always bring your own custom Linux image that is tested and deployed. The AIX  stock images are supported on the Power10 with AIX  operating system.

### Storage
{: #storage-private-cloud}

For small pods only the IBM Flash System FS5200 is supported. For more information, see [IBM Flash System FS5200](https://www.ibm.com/in-en/products/flashsystem-5200){: external}.




You can extend the storage capacity of the pods, but you cannot add more storage controllers.
{: note}

### Storage tiers
{: #storage-tiers-spec-private-cloud}

The storage tiers are based on I/O operations per second (IOPs). The performance of your storage volumes is limited to the maximum number of IOPs based on the storage volume size and storage tier.

Flexible IOPS is a tier-less storage offering that removes the notion of a disk type and replace it with a storage pool. Each of the storage pools supports multiple storage tiers. The storage tiers are based on different IOPS levels.

Table 5 shows the supported storage tiers with corresponding IOPS.

| Tier level | IOPS  | Performance |
|---------------|---------------|---------------------|
| Tier 0 | 25 IOPS/GB | A 100-GB volume receives 2500 IOPS. \n This is 2.5x faster than tier 1 and 8.3x faster than tier 3. |
| Tier 1 | 10 IOPS/GB | A 100-GB volume receives 1000 IOPS. \n This is 3.3x faster than tier 3. |
| Tier 3 | 3 IOPS/GB | A 100-GB volume receives 300 IOPS. |
| Fixed IOPS | 5000 IOPS regardless of size | A 100-GB volume receives 5000 IOPS. |
{: caption="Tier and IOPS mapping" caption-side="bottom"}

The use of fixed IOPS is limited to volumes with a size of 200 GB or less, which is the break even size with Tier 0 (200 GB @ 25 IOPS/GB = 5000 IOPS).
{: important}

For example, a 100 GB Tier 3 storage can receive up to 300 IOPs, and a 100 GB Tier 1 storage volume can receive up to 1000 IOPs. After the IOPs limit is reached for the storage volume, the I/O latency increases. Tier 3 storage is not suitable for production workloads. When you are choosing a storage tier, ensure that you consider not just the average I/O load, but more importantly the peak IOPs of your storage workload.

## Network
{: #network-spec-private-cloud}

The entire network subsystem can be divided into the following parts:

* **Control plane network traffic**: The control plane network is the connection between IBM Cloud and client data center. The IBM SREs establish this connection manually by using the Direct Link Connect (secure) or Virtual private network (VPN) between IBM Cloud and your {{site.data.keyword.on-prem}} data center during the initial deployment.
* **Client data plane network traffic**: The client data plane is the connection between the client data center and the {{site.data.keyword.powerSys_notm}} pods. Communication between each virtual machine within a pod is established by using private IP addresses. The IBM SREs configure the communication between virtual machines and the data center corporate network manually by using different network use cases. For more information, see [Network use cases](/docs/power-iaas?topic=power-iaas-network_use_cases). Use your own model for firewall and load balancer services. For any communication between your {{site.data.keyword.on-prem}} data center and other IBM Cloud services, you must manually set up the network configuration.

For more information, see [Network overview](/docs/power-iaas?topic=power-iaas-network-private-cloud).
