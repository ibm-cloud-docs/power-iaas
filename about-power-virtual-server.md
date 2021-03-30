---

copyright:
  years: 2019, 2020, 2021

lastupdated: "2021-03-12"

keywords: power systems, infrastructure as a service, multiple virtual servers, hybrid cloud environment, linux, aix, ibm i

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

# What is a Power Systems Virtual Server?
{: #about-virtual-server}

{{site.data.keyword.powerSysFull}} is a Power Systems enterprise infrastructure as a service (IaaS) offering. {{site.data.keyword.powerSys_notm}}s are physically located with low-latency connectivity to the IBM Cloud&trade; infrastructure. In the data centers, the {{site.data.keyword.powerSys_notm}}s are separated from the rest of the IBM Cloud servers with separate networks and direct-attached storage. The internal networks are fenced but offer connectivity options to IBM Cloud infrastructure or on-premises environments. This infrastructure design enables {{site.data.keyword.powerSys_notm}} to maintain key enterprise software certification and support as the {{site.data.keyword.powerSys_notm}} architecture is identical to certified on-premises infrastructure. The virtual servers, also known as logical partitions (LPAR), run on IBM Power Systems hardware with the PowerVM hypervisor.
{:shortdesc}

With the {{site.data.keyword.powerSys_notm}} service, you can quickly create and deploy one or more virtual servers (that are running either the AIX, IBM i, or Linux operating systems). After you provision the {{site.data.keyword.powerSys_notm}}, it is your responsibility to make sure that your operating system is secure.

<!--Current AIX, IBM i, and Linux&reg; clients can use the {{site.data.keyword.powerSys_notm}} service for a number of workload scenarios, including disaster recovery, development environments, and partial IT infrastructure moves. {{site.data.keyword.powerSys_notm}} clients can stay competitive with the scaling of their infrastructure and remain flexible with their workload management and capacity both on- and off-premise. And since the infrastructure layer is identical, system administrators who run on-premises AIX, IBM i, and Linux systems today can use their same tools, workflows, and enhancements in the Power Systems Virtual Server.-->

## Key features
{: #key-features}

The following are some of the key features for the {{site.data.keyword.powerSys_notm}} service.

### Straightforward billing
{: #straightforward-billing}

The {{site.data.keyword.powerSys_notm}} service uses a monthly billing rate that includes the licenses for the AIX and IBM i operating systems. The monthly billing rate is pro-rated by the hour based on the resources that are deployed to the {{site.data.keyword.powerSys_notm}} instance for the month. When you create the {{site.data.keyword.powerSys_notm}} instance, you can see the total cost for your configuration based on the options that you specify. You can quickly identify what configuration options provide you with the best value for your business needs. For more information, see [Pricing](/docs/power-iaas?topic=power-iaas-pricing-virtual-server#pricing-virtual-server).

The {{site.data.keyword.powerSys_notm}} service does not provide Linux stock images. You must bring your own Linux image (OVA format) and subscription. SLES and RHEL OVA images are supported. [Learn more](/docs/power-iaas?topic=power-iaas-using-linux)
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

IBM provides you with stock AIX and IBM i images when you create a {{site.data.keyword.powerSys_notm}}. However, you can always [bring your own](/docs/power-iaas?topic=power-iaas-deploy-custom-image) custom AIX, IBM i or Linux image that you have tested and deployed.

### Support for SAP NetWeaver or SAP HANA applications
{: #support-SAPNetWeaver-or-SAPHANA}

When you provision a {{site.data.keyword.powerSys_notm}} instance to support SAP NetWeaver applications, select a version of the IBM-provided AIX or Linux stock operating system image. When you provision a {{site.data.keyword.powerSys_notm}} instance to support the SAP HANA applications, select a version of the IBM provided SUSE Enterprise Linux&reg; server (SLES) stock image. IBM i operating system and custom AIX and Linux images are not supported for SAP workloads. For information about the supported operating system versions, see [FAQ](/docs/power-iaas?topic=power-iaas-power-iaas-faqs). For more information, see [Deploying your infrastructure](/docs/sap?topic=sap-power-vs-planning-items).

When provisioning a {{site.data.keyword.powerSys_notm}} to support SAP NetWeaver applications, select a version of the IBM-provided AIX operating system stock image. IBM i and operating system custom images are not supported for SAP workloads at this time.
{: note} 

### Support for deploying a Red Hat OpenShift Cluster
{: #support-redhat-openshift}

When you provision a Red Hat OpenShift Cluster on {{site.data.keyword.powerSys_notm}}, it is easier to use the IBM&trade; provided automation to create the entire cluster of servers and install Red Hat OpenShift rather than individually provisioning {{site.data.keyword.powerSys_notm}} instances. For instructions to deploy a Red Hat OpenShift Cluster on {{site.data.keyword.powerSys_notm}}, including preparation of the required Operation System images for the cluster, see [Deploying Red Hat OpenShift Container Platform 4.x on IBM Power Systems Virtual Servers](https://developer.ibm.com/components/ibm-power/series/deploy-ocp-cloud-paks-power-virtual-server/){: new_window}{: external}.

## Hardware specifications
{: #hardware-specifications}

The following IBM Power Systems can host a {{site.data.keyword.powerSys_notm}}: IBM Power System E880 (9080-M9S) (Dallas and Washington only), IBM Power System S922 (9009-22A), and IBM Power System E980 (9080-M9S) (Data centers other than Washington). For more information about these systems and how they're used inside the {{site.data.keyword.powerSys_notm}} service, see their data sheets and the hardware overview table.

If you'd like to compare your current environment's performance to what's available through the {{site.data.keyword.powerSys_notm}} service, see the [IBM Power Systems performance report](https://www.ibm.com/downloads/cas/K90RQOW8){: new_window}{: external}. For a more condensed comparison, see [IBM Power Systems CPW performance data comparison](https://www.itechsol.com/wp-content/uploads/2018/07/IBM-Power-Systems-CPW-Performance-Data-Comparison-P7-vs-P8-vs-P9-rev3-July-2018.pdf){: new_window}{: external}.
{: tip}

**Data sheets**

* [IBM Power System E880 (9119-MHE) - Dallas and Washington only](https://www.ibm.com/downloads/cas/EE476WAP){: new_window}{: external}
* [IBM Power System S922 (9009-22A)](https://www.ibm.com/downloads/cas/KQ4BOJ3N){: new_window}{: external}
* [IBM Power System E980 (9080-M9S) - Data centers other Washington](https://www.ibm.com/downloads/cas/VX0AM0EP){: new_window}{: external}

| Compute     | Storage      | Network      |
|------------ | ------------ | ------------ |
| <ul><li>Power E880 (9080-MHE)</li><li>Power S922 (9009-22A)</li></ul> | <ul><li>Flash storage from IBM FS9000 series devices</li><li>V7000 SSD (no new VMs)</li><li>32 GB SAN infrastructure</li></ul> | <ul><li>Cisco Nexus9000 93180YC-EX (10G)</li><li>Cisco Nexus9000 C9348GC-FXP (1G)</li><li>Avocent ACS8048</li></ul> |
{: class="simple-tab-table"}
{: tab-group="hardware"}
{: caption="Table 1. Hardware overview (Washington, D.C.)" caption-side="top"}
{: #hw-spec-1}
{: tab-title="Washington, D.C. (WDC04)"}

| Compute  | Storage   | Network   |
|--------- | --------- | --------- |
| <ul><li>Power E880 (9080-M9S)</li><li>Power S922 (9009-22A)</li></ul> | <ul><li>Flash storage from IBM FS9000 series devices</li><li>V7000 SSD (no new VMs)</li><li>32 GB SAN</li> | <ul><li>Cisco Nexus9000 C9336PQ  (Spine 10G)</li><li>Cisco Nexus9000 C93180YC (10G)</li><li>Cisco Nexus9000 C93108TC-EX (1G)</li><li>Cisco UCS - APIC controller</li><li>Cisco ASR1001-HX Router</li><li>Avocent ACS8016</li></ul> |
{: class="simple-tab-table"}
{: tab-group="hardware"}
{: caption="Table 2. Hardware overview (Dallas, TX)" caption-side="top"}
{: #hw-spec-2}
{: tab-title="Dallas (DAL13)"}

| Compute  | Storage   | Network   |
|--------- | --------- | --------- |
| <ul><li>Power E980 (9080-M9S)</li><li>Power S922 (9009-22A)</li></ul> | <ul><li>Flash storage from IBM FS9000 series devices</li><li>32 Gb SAN infrastructure</li> | <ul><li>Cisco Nexus9000 N9K-C9364C (Spine 10G)</li><li>Cisco Nexus9000 9348GC-FXP (Leaf 1G) </li><li>Cisco Nexus9000 93180YC-FX (Leaf 25G)</li><li>Cisco UCS - APIC controller</li><li>Cisco ASR1001-HX Router</li><li>Avocent ACS8032DAC-400</li></ul> |
{: class="simple-tab-table"}
{: tab-group="hardware"}
{: caption="Table 3. Hardware overview (Non-US)" caption-side="top"}
{: #hw-spec-3}
{: tab-title="Non-US"}

For a complete list of supported data centers, see [Creating a Power Systems Virtual Server service](https://cloud.ibm.com/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#creating-service).
{: note}

## Storage tiers
{: #storage-tiers}

For each {{site.data.keyword.powerSys_notm}} instance, you must select a storage tier - **Tier 1** or **Tier 3**. The storage tiers in {{site.data.keyword.powerSys_notm}} are based on I/O operations per second (IOPS). It means that the performance of your storage volumes is limited to the maximum number of IOPS based on volume size and storage tier. Although, the exact numbers might change over time, the **Tier 3** storage is currently set to 3 IOPS/GB, and the **Tier 1** storage is currently set to 10 IOPS/GB. For example, a 100 GB Tier 3 storage volume can receive up to 300 IOPs, and a 100 GB Tier 1 storage volume can receive up to 1000 IOPS. After the IOPS limit is reached for the storage volume, the I/O latency increases.

<!--Currently, the IOPS-based storage tiers are available in all locations except WDC04 and DAL13 data centers.
{: note}-->

## Public and private networks
{: #public-private-networks}

When you create a {{site.data.keyword.powerSys_notm}}, you can select a private or public network interface.

**Public network**

* Easy and quick method to connect to a {{site.data.keyword.powerSys_notm}} instance.
* IBM configures the network environment to enable a secure public network connection from the internet to the {{site.data.keyword.powerSys_notm}} instance.
* Connectivity is implemented by using an IBM Cloud Virtual Router Appliance (VRA) and a Direct Link Connect connection.
* Protected by firewall and supports the following secure network protocols:
    * SSH
    * HTTPS
    * Ping
    * IBM i 5250 terminal emulation with SSL (port 992)

**Private network**

* Allows your {{site.data.keyword.powerSys_notm}} instance to access existing {{site.data.keyword.cloud_notm}} resources, such as IBM Cloud Bare Metal Servers, Kubernetes containers, and Cloud Object Storage.
* Uses a Direct Link Connect connection to connect to your IBM Cloud account network and resources.
* Required for communication between different {{site.data.keyword.powerSys_notm}} instances.

  For more information about the different options for configuring a private network, see [Configure a private network](/docs/power-iaas?topic=power-iaas-configuring-subnet).
  {: note}

<!-- The following figure displays the basic configuration for a public and private network:

![Displays how network traffic flows for public or private connection](/images/power-iaas-network1.svg "Displays how network traffic flows for public or private connection"){: caption="Figure 1. Private and public network configuration" caption-side="bottom"} -->

