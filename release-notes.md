---

copyright:
  years: 2019, 2024

lastupdated: "2024-04-17"

keywords: release notes, announcements, feature updates, changes, power virtual server

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:preview: .preview}
{:external: target="_blank" .external}

# Release notes
{: #release-notes}

Use these release notes to learn about the latest changes to the {{site.data.keyword.powerSysFull}}.
{: shortdesc}

## April 2024
{: #apr-2024}

- Power Edge Router (PER) is now available in the `LON06` data center. For more information, see [Getting Started with Power Edge Router](/docs/power-iaas?topic=power-iaas-per).
- {{site.data.keyword.powerSys_notm}} now supports the large t-shirt profiles on the latest RHEL 9.2 for SAP and RHEL 8.8 for SAP OS images. For more information, see the [SAP documentation on OS](https://test.cloud.ibm.com/docs/sap?topic=sap-compute-os-design-considerations#os-power) for IBM {{site.data.keyword.powerSys_notm}} and [FAQ documentation for supported OS versions](/docs/power-iaas?topic=power-iaas-power-iaas-faqs#os-versions).

## March 2024
{: #mar-2024}

- Reserve an IP address from the {{site.data.keyword.powerSys_notm}} user interface. The IP address that you reserve are not assigned to a virtual server instance. For more information. see [Reserving IP addresses](/docs/power-iaas?topic=power-iaas-configuring-subnet#reserv-ip).
- New AIX 7.3 TL2, and 7.2 TL5 SP7 operating system images are available. For more information, See the [FAQ documentation](/docs/power-iaas?topic=power-iaas-power-iaas-faqs#os-versions).
- New IBM i 7.5 TR3, IBM i 7.4 TR9, and IBM i COR operating system images are available. For more information, See the [FAQ documentation](/docs/power-iaas?topic=power-iaas-power-iaas-faqs#os-versions).
- New data center `CHE01` is available. The following are some capabilities that differ for this data center:
  - `CHE01` supports up to 5 GB Direct Link connections compared to other datacenters that supports up to 10 GB.
  - To use Transit Gateway, you will need to connect to `CHE01` using a different data center that supports Transit Gateway. For more information, see [Managing IBM Cloud connections](/docs/power-iaas?topic=power-iaas-cloud-connections).
  - IBM Cloud Monitoring and Power Edge Router network connectivity are currently unavailable for `CHE01`.
- SUSE part numbers for each tier are available. For more information, see the part numbers table in [Pricing for Power Virtual Servers](/docs/power-iaas?topic=power-iaas-pricing-virtual-server).
- Flexible I/O operation per second (IOPS) is now available in the `DAL12`, `DAL13`, `SAO01`, `SAO04`, `WDC04`, and `WDC06` data centers. For more information, see [Flexible IOPS](/docs/power-iaas?topic=power-iaas-about-virtual-server#storage-tiers).
- IBM Cloud Monitoring service is now avilable in `DAL13` and `FRA04`. For more information, see [Monitoring metrics for {{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-monitor-sysdig).
- PER is now available in the `OSA21`, `SYD05`, and `TOK04` data center. For more information, see [Getting Started with Power Edge Router](/docs/power-iaas?topic=power-iaas-per).

## February 2024
{: #feb-2024}

- PER is now available in the `SAO01` data center. For more information, see [Getting Started with Power Edge Router](/docs/power-iaas?topic=power-iaas-per).
- You can now provision the SLES 15 SP5 images. You are required to install an additional [software package](/docs/sap?topic=sap-power-vs-set-up-power-instances#power-vs-addtl-sw-sles-sap) as a prerequisite for SAP and Netweaver workloads.
- You can now choose to use IBM provided Linux images with your own license. While provisioning the boot image, select the OS image that is listed under the **Client supplied subscription** section. The stock non-Full Linux Subscription (FLS) images are available across all the data centers. For more information see, [Full Linux® subscription for Power Virtual Servers](/docs/power-iaas?topic=power-iaas-set-full-Linux).
- Flexible IOPS is now available in the `FRA04`, `LON06`, and `MAD02` data centers. For more information, see [Flexible IOPS](/docs/power-iaas?topic=power-iaas-about-virtual-server#storage-tiers).
- Global Replication Service (GRS) is now available in `WDC07` and `DAL10` data center pair.
- You can now migrate your workspace that uses a Direct Link connection to a PER workspace through a support ticket. For more information, see [Migrating to Power Edge Router](/docs/power-iaas?topic=power-iaas-migrate-ws-per).
- IBM Cloud Monitoring service is now avilable in `OSA21`, `DAL10`, and `WDC07`.

## January 2024
{: #jan-2024}

- Certain stock images for SAP will be updated with new Ansible packages. Until then it is recommended that you do not use the following images to create a new {{site.data.keyword.powerSys_notm}} instance for use with SAP workloads:
  - RHEL8-SP8-SAP
  - RHEL8-SP8-SAP-NETWEAVER
  - RHEL9-SP2-SAP
  - RHEL9-SP2-SAP-NETWEAVER

- The {{site.data.keyword.powerSys_notm}} workspaces provisioned in London, São Paulo, Osaka, Washington D.C., Montreal, and Toronto will send events to activity tracker instances in their respective regions effective from 29 January 2024. For more information, see [Activity tracker regions](/docs/power-iaas?topic=power-iaas-at-events#at-regions).
- PER is now available in `DAL12` and `FRA04`. For more information, see [Getting Started with Power Edge Router](/docs/power-iaas?topic=power-iaas-per).
  
- The direction going forward for VPN connectivity capability of the {{site.data.keyword.powerSys_notm}} will be to use the existing [IBM Cloud VPC VPN](/docs/power-iaas?topic=power-iaas-VPN-connections#vpc-vpn) for a one cloud experience, improved reliability, and high availability connections.
  
  The VPNAAS_CONNECT_APPLICATION_INSTANCE_HOURS part ID of the {{site.data.keyword.powerSys_notm}} is designed only for {{site.data.keyword.powerSys_notm}} and will be withdrawn by the end of March 2024.

  Existing users can choose to continue to use {{site.data.keyword.powerSys_notm}} VPN until the end of service or upgrade to their preferred IBM Cloud VPN for VPC service.

  By January 18, 2025 IBM will no longer deliver standard support for the {{site.data.keyword.powerSys_notm}} VPNaaS product, thus if you choose not to take the recommended action and run into issues, IBM will not support with end of life for parts occurring six months later on July 14, 2025. Additionally, after March 2024 new connections can no longer be provisioned with the {{site.data.keyword.powerSys_notm}} VPN thus you are encouraged to upgrade to the IBM Cloud VPC VPN at your earliest convenience and ideally before March 2024.

- IBM Cloud Monitoring service is now avilable in `SYD04`, `SAO04`, and `DAL12`.
 
## December 2023
{: #dec-2023}

- **New data center availability**  
  - `MAD04` is available. It is a PER-enabled Power10 data center that supports IBM Cloud Monitoring service.
  - `SAO04` is available for PER.
- **Cost estimator tool**  
  A new cost estimator tool for {{site.data.keyword.powerSys_notm}} is available. You can access it from the {{site.data.keyword.powerSys_notm}} [home page](https://cloud.ibm.com/power/overview){: external}. To learn more about the cost estimator tool, see [Getting started with the cost estimator tool](/docs/power-iaas?topic=power-iaas-getting-started-with-the-cost-estimator-tool).
- **Dedicated hosts**  
  A new dedicated host capability is available. You can provision IBM Power S922 and S1022 servers for your dedicated use. For more information, see [Dedicated host](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#dedicated-host).
- **VPC VPN service**  
  The VPC VPN is a robust service that replaces the legacy {{site.data.keyword.powerSys_notm}} VPN. To learn more on VPC VPN, see [Creating a Virtual Private Cloud VPN connection](/docs/power-iaas?topic=power-iaas-VPN-connections#vpc-vpn).
- **Flexible IOPS**  
  {{site.data.keyword.powerSys_notm}} now offers a tier-less storage service with the name Flexible IOPS. With Flexible IOPS, you can now change the IOPS level for your existing volumes and clone volumes to your choice of IOPS level, and much more. See: [Flexible IOPS](/docs/power-iaas?topic=power-iaas-about-virtual-server#storage-tiers).
- New RHEL versions are available. See the [FAQ](/docs/power-iaas?topic=power-iaas-power-iaas-faqs#os-versions) page for details on the latest version.
- **Update on the new SAP HANA large t-shirt profiles feature**  
  The latest RHEL 9.2 for SAP, RHEL 8.8 for general purpose and SAP, and current RHEL 8.6 for general purpose and SAP OS images are being updated to support the larger t-shirt profiles. Until further notice, use t-shirt profiles with less than 64 cores for RHEL 9.2, RHEL 8.8, and RHEL 8.6 OS images. For more information, see the [SAP documentation on OS](https://test.cloud.ibm.com/docs/sap?topic=sap-compute-os-design-considerations#os-power) for IBM {{site.data.keyword.powerSys_notm}}.
- **New Global Replication Service (GRS) pairs support**
  The respective data center pairs `MAD02` and `FRA04` along with `MAD04` and `FRA05` now supports GRS.
  
## November 2023
{: #nov-2023}

- `WDC06` and `MAD02` data center are now available for PER. `MAD02` is a PER-enabled Power10 data center.
- Availibity of IBM Cloud Monitoring service is now extended in `FRA04`, `FRA05`, `LON04`, `LON06`, `MAD02`, `SAO01`, and `TOK04`.
  
## September 2023
{: #sep-2023}

- **{{site.data.keyword.powerSys_notm}} and SysDig Integration**
: You can now seamlessly monitor your platform metrics within the IBM Cloud environment by using the IBM Cloud Monitoring service. For detailed instructions on how to access and use this integration, refer to the documentation: [Monitoring metrics for {{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-monitor-sysdig).

The data center where you can monitor your platform metrics currently are `WDC06`, `SYD05`, and `WDC04` with other data center coming soon.
  {: note}

- **Introduction of {{site.data.keyword.powerSys_notm}} S1022 processor**
: The Power10 S1022 (9105-22A) is now available in `WDC07` data center. As we progress, additional data centers are made available.

  SAP Netweaver is not certified for use with S1022 systems, making them suitable exclusively for nonproduction workloads.
  {: note}

- **IBM i 7.3 service extension pricing**
: Effective 1 October 2023, IBM i 7.3 on {{site.data.keyword.powerSys_notm}} is at the end of normal support and will be in service extension. Service extension pricing is automatically added to the IBM i charge for IBM i 7.3 usage.

- **Addition of New Global Replication Service data center pair**
: {{site.data.keyword.powerSys_notm}} expanded the Global Replication Service (GRS) capabilities by adding a new data center pair - `DAL13` and `WDC04`. This enhancement is available on the Tier 1 storage support within the GRS framework. See: [Locations that support global replication service](/docs/power-iaas?topic=power-iaas-getting-started-GRS#locations-GRS).

## June 2023
{: #jun-2023}

-  The {{site.data.keyword.powerSys_notm}} enhances the management of stock images in the backend. This enhancement eliminates identical versions (copies) of stock images and improves the performance of copying a stock image in your account by using an image reference. Find more information in the [FAQ doc page](/docs/power-iaas?topic=power-iaas-power-iaas-faqs#stock-image-copy-improve).

  We are currently rolling out the feature to eliminate stock image copies in all data centers in phases. If your data center has already received the update, you notice that the export option for stock images is no longer available because you are using the reference of the stock image.

- IBM {{site.data.keyword.powerSys_notm}} is sequentially rolling out a Power Edge Router (PER) solution that is available in `DAL10` data center.
  
  PER improves network communication across different parts of the IBM network. See, [Getting Started with Power Edge Router](/docs/power-iaas?topic=power-iaas-per) for more information.

## May 2023
{: #may-2023}

- IBM {{site.data.keyword.powerSys_notm}} now supports two new data centers `WDC07` (Washington DC) and `SAO04` (São Paulo).
- IBM {{site.data.keyword.keymanagementserviceshort}} is now supported on AIX and Linux workloads. For more information, see [Integrating {{site.data.keyword.powerSys_notm}} with IBM Cloud Key Management Services](/docs/power-iaas?topic=power-iaas-integrate-hpcs#AIX-hpcs).
- Effective 1 May 2023, AIX 7.1 on {{site.data.keyword.powerSys_notm}} is covered for software support. In {{site.data.keyword.powerSys_notm}}, starting March 2024, Service Extension pricing is automatically added to the AIX charge for AIX 7.1 usage. AIX 7.1 Service Extension was announced on January 24, 2023. For more information see, [Service Extension for IBM AIX 7.1](https://www.ibm.com/common/ssi/ShowDoc.wss?docURL=/common/ssi/rep_ca/4/877/ENUSZS23-0004/index.html&lang=en&request_locale=en){: external}.

## March 2023
{: #mar-2023}

- **Update on the new SAP HANA large t-shirt profiles feature**:
  IBM supports SLES15 SP4 for SAP and RHEL8.6 for SAP OS images with all other features on all t-shirt profiles with fewer than 64 cores. These SLES15 SP4 for SAP and RHEL8.6 for SAP OS images are while being updated to support the larger t-shirt profiles. Until further notice, use the larger t-shirt profiles with the SLES15 SP3 for SAP OS image or the RHEL8.4 for SAP OS image. For more information, see the SAP documentation on [OS for IBM Power Virtual Servers](/docs/sap?topic=sap-compute-os-design-considerations#os-power).

  The RHEL8.6 for SAP OS image is available in `DAL10`, `DAL12`, `FRA04`, `FRA05`, `LON04`, `LON05`, `MON01`, `SYD05`, `TOR01`, `WDC04`, and `WDC06`. The image is available in all data centers by 3/27/23.

- **{{site.data.keyword.powerSys_notm}} cost estimator**:
  Effective 3/23/23, two of the latest large SAP HANA t-shirt profiles `mh1-90x16200` and `mh1-100x18000` are available options in the [cost estimator](https://cloud.ibm.com/power/overview#estimator){: external}. In April 2023, the latest largest profile `mh1-125x22500` will also be available in the estimator.

- **Access your event logs and notifications**:
  You can now access your event logs and notification from the **Event logs** page on the {{site.data.keyword.powerSys_notm}} user interface. For more information, see [Managing events logs and notifications](/docs/power-iaas?topic=power-iaas-manage-event-logs)

## February 2023
{: #feb-2023}

- Added a new data center DAL10 in the existing list of {{site.data.keyword.powerSys_notm}} data centers. For more information, see [Creating a {{site.data.keyword.powerSys_notm}} workspace](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#creating-service).

## December 2022
{: #dec-2022}

- Get the list of internationally recognized {{site.data.keyword.powerSys_notm}} compliance certifications. For more information, see [{{site.data.keyword.powerSys_notm}} compliance certifications](/docs/power-iaas?topic=power-iaas-compliances-list).

- You can integrate Hyper Protect Crypto Services (HPCS) with {{site.data.keyword.powerSys_notm}} to securely store and protect encryption key information for AIX and Linux. For more information, see [Integrating {{site.data.keyword.powerSys_notm}} with HPCS](/docs/power-iaas?topic=power-iaas-integrate-hpcs).

## September 2022
{: #sept-2022}

- You can share a group of processors between multiple virtual machines that allows you to group your applications together by using the shared processor pool. For more information, see [Managing shared processor pool](/docs/power-iaas?topic=power-iaas-manage-SPP).

- {{site.data.keyword.powerSys_notm}} allows you to automate the complete data recovery solution by using the API and CLI interfaces of a global replication service. For more information, see [Managing a global replication service](/docs/power-iaas?topic=power-iaas-getting-started-GRS).

- You can choose to deploy Epic workloads on a VM for more cost savings. For more information, see [Configuring a VM for Epic workloads](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#configuring-a-vm-for-epic-workloads).

- The full Linux subscription on {{site.data.keyword.powerSys_notm}} now supports SLES 15 SP4 (General).

## August 2022
{: #aug-2022}

- You can use FalconStor VTL in {{site.data.keyword.powerSys_notm}} for data protection and cloud migration as a Service for IBM i. See [Managing Virtual tape library](/docs/power-iaas?topic=power-iaas-managing-virtual-tape-library).

## July 2022
{: #jul-2022}

- You can use IBM Transit Gateway to interconnect your {{site.data.keyword.powerSys_notm}} to the {{site.data.keyword.cloud_notm}} classic and Virtual Private Cloud (VPC). See [Creating IBM Cloud connections](/docs/power-iaas?topic=power-iaas-cloud-connections#create-cloud-connections).
- {{site.data.keyword.powerSys_notm}} now supports a full Linux subscription on RHEL 8.6. See [Full Linux® subscription for {{site.data.keyword.powerSys_notm}}s](/docs/power-iaas?topic=power-iaas-set-full-Linux).

## June 2022
{: #jun-2022}

- {{site.data.keyword.powerSys_notm}} now supports Linux (RHEL and SLES) stock images for non-SAP applications by using full Linux subscription. See [Full Linux® subscription for {{site.data.keyword.powerSys_notm}}s](/docs/power-iaas?topic=power-iaas-set-full-Linux).
- IBM i 7.5 is supported on {{site.data.keyword.powerSys_notm}}s.
- With virtual appliances independent software vendors (ISV) can offer OVA (ISV software plus operating system of your choice) for quick deployment of {{site.data.keyword.powerSys_notm}} workloads. See [Managing virtual appliances](/docs/power-iaas?topic=power-iaas-virtual-appliances).
  
## April 2022
{: #apr-2022}

- Snapshots that are created are monitored hourly and priced depending on the disk space used. See [Metering and pricing of snapshot](/docs/power-iaas?topic=power-iaas-volume-snapshot-clone#metering-snapshot).

## March 2022
{: #march-2022}

- The {{site.data.keyword.powerSys_notm}} now supports [AIX 7.3](/docs/power-iaas?topic=power-iaas-deploy-custom-image#aix-details).
- You can view best practices and guidelines on [AIX backup performance on IBM {{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-backup-strategies#backup-aix).

## December 2021
{: #dec-2021}

- You can now configure [Virtual private network (VPN)](/docs/power-iaas?topic=power-iaas-VPN-connections) by using the {{site.data.keyword.powerSys_notm}} GUI.
- You can now configure [Placement groups](/docs/power-iaas?topic=power-iaas-placement-groups) by using the {{site.data.keyword.powerSys_notm}} GUI.
- You can now set a [10 Gbps speed for Cloud connection](/docs/power-iaas?topic=power-iaas-cloud-connections) by using the {{site.data.keyword.powerSys_notm}} GUI.
- You can now set [affinity policies for storage pools](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#configuring-instance) by using the {{site.data.keyword.powerSys_notm}} GUI.

## October 2021
{: #oct-2021}

- You can now use [Virtual private network (VPN)](/docs/power-iaas?topic=power-iaas-VPN-connections) to connect an on-premises VPN gateway to an IBM Cloud™ VPN gateway that is created within a {{site.data.keyword.powerSys_notm}} VPN service. 
- You can now use [Virtual tape libraries](/docs/power-iaas?topic=power-iaas-virtual-tape-libraries) to backup IBM i data. 

## September 2021
{: #sep-2021}

- You can now use [Capturing and exporting a virtual machine](/docs/power-iaas?topic=power-iaas-capturing-exporting-vm) to view the new Job feature and view restrictions for VM capture, image import, and image export.
- You can now use [Mixed storage](/docs/power-iaas?topic=power-iaas-power-iaas-faqs#mixed_storage) to attach storage volumes to a PVM instance from different storage tiers and pools.

## June 2021
{: #jun-2021}

- You can now use [Placement groups](/docs/power-iaas?topic=power-iaas-placement-groups) to add your servers into groups and apply affinity or anti-affinity policies.

## May 2021
{: #may-2021}

- You can now use [Cloud connections](/docs/power-iaas?topic=power-iaas-managing-cloud-connections) to automate the way you connect your {{site.data.keyword.powerSys_notm}} instances to the IBM Cloud resources.
- {{site.data.keyword.powerSys_notm}} now supports SAP HANA applications in IBM-provided RHEL stock images. For more information, see [Preparing Linux OS on IBM Power VS for SAP HANA](/docs/sap?topic=sap-power-vs-sles-hana).


## March 2021
{: #mar-2021}

- You can now deploy a Red Hat Enterprise Linux (RHEL) 8.1 and 8.2 virtual machine (VM) on a VM instance. For more information, see [Using RHEL within the {{site.data.keyword.powerSys_notm}} workspace](/docs/power-iaas?topic=power-iaas-linux-with-powervs).
- {{site.data.keyword.powerSys_notm}} provides a community-supported CentOS image under the Linux operating system. However, IBM does not provide any support for this image. For more information, see [Configuring a {{site.data.keyword.powerSys_notm}} instance](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#configuring-instance ).
- You can now choose an `OSA21` data center to deploy your {{site.data.keyword.powerSys_notm}}.

## February 2021
{: #feb-2021}

- You can now choose a `MON01` data center to deploy your {{site.data.keyword.powerSys_notm}}.
- The {{site.data.keyword.powerSys_notm}} offering now supports IBM i 7.1. For more information, see [Minimum PTF levels for IBM i](/docs/power-iaas?topic=power-iaas-minimum-levels).
- You can clone a volume or multiple volumes to create a consistent full copy of the volume. For more information, see [Cloning a volume](/docs/power-iaas?topic=power-iaas-volume-snapshot-clone#cloning-volume).
- You can resize the memory and core counts to a maximum of 8 times of the specified values, and to a minimum of 1/8 times of the specified values when the VM was provisioned. For more information, see [Resizing the virtual machine core count and memory](/docs/power-iaas?topic=power-iaas-modifying-server#resize-core-mem).
