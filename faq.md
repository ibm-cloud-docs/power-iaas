---

copyright:
  years: 2019, 2023

lastupdated: "2023-09-22"

keywords: faq, virtual server, network bandwidth, private network setup, multi-tenant environment, delete workspace, supported operating systems, hardware specifications, software maps, affinity, processor types, pinning, snapshot, clone, restore

subcollection: power-iaas

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
{:faq: data-hd-content-type='faq'}
{:support: data-reuse='support'}

# FAQ
{: #power-iaas-faqs}

## What is IBM Power Systems Virtual Server?
{: #what-is-powervs}
{: faq}
{: support}

IBM Power Systems Virtual Server is a hosted infrastructure offering that allows you to quickly integrate with the Internet for on-demand provisioning. This offering provides a secure and scalable server virtualization environment that is built upon the advanced RAS features and leading performance of the Power Systems™ platform. The IBM Power Systems Virtual Servers are located in IBM data centers and distinct from the IBM Cloud servers with separate networks and direct-attached storage.

## What versions of AIX, IBM i, and Linux are supported?
{: #os-versions}
{: faq}
{: support}

The supported AIX, IBM i, and Linux&reg; operating system versions depend on the IBM Power Systems hardware that you select for the {{site.data.keyword.powerSys_notm}}: S922 (9009-22A), E980 (9080-M9S)<!-- , E1080 (9080-HEX), --> or S1022 (9105-22A). To view a list of the supported AIX, IBM i, and Linux operating system technology levels, see the following system software maps:

**AIX** - The {{site.data.keyword.powerSys_notm}} offering supports AIX 7.1, or later on the S922 (9009-22A) and E980 (9080-M9S). 

Power Systems <!-- E1080 (9080-HEX) and --> S1022 (9105-22A) supports AIX 7.1 TL 5 and later.

When you view the system software maps, refer to the AIX 7.1, AIX 7.2, and AIX 7.3 information. If you use an unsupported version, it is subject to outages during planned maintenance windows with no advanced notification given.

- [S922 (9009-22A) AIX software map](https://www-01.ibm.com/support/docview.wss?uid=ssm1platformaix9009-22A-vios-only){: external}
- [E980 (9080-M9S) AIX software map](http://www-01.ibm.com/support/docview.wss?uid=ssm1platformaix9080-M9S-vios-only){: external}
- [S1022 (9105-22A) AIX software map](https://www.ibm.com/support/pages/node/6604269){: external}

<!-- - [E1080 (9080-HEX) AIX software map](https://www.ibm.com/support/pages/system-software-map-power-systems-e1080-9080-hex-and-aix-all-io-configurations){: external} -->

For information on end of service pack support (EoSPS) dates, see [AIX support lifecycle](https://www.ibm.com/support/pages/aix-support-lifecycle-information){: external}.

AIX stock images currently available when you create a VM are:

* AIX 7.3 TL1 SP2
* AIX 7.2 TL5 SP6
* AIX 7.1 TL5 SP9

**IBM i** - {{site.data.keyword.powerSys_notm}} supports IBM i 7.1, or later. Clients running IBM i 6.1 must first upgrade the OS to a current support level before migrating to the Power Systems Virtual Server. IBM i 7.2 supports direct [upgrades from IBM i 6.1 or 7.1 (N-2)](https://www.ibm.com/support/knowledgecenter/ssw_ibm_i_72/rzahc/fastpathrzahc.htm){: external}.

- [S922 (9009-22A), E980 (9080-M9S)<!-- , E1080 (9080-HEX),--> and S1022 (9105-22A) software maps](https://www-01.ibm.com/support/docview.wss?uid=ssm1platformibmi){: external}
- [IBM i PTF minimum levels](/docs/power-iaas?topic=power-iaas-minimum-levels)
- [IBM i release life cycle](https://www.ibm.com/support/pages/release-life-cycle){: external}

IBM i stock images currently available when you create a VM are:

* IBM i 7.5 TR2
* IBM i 7.4 TR8
* IBM i 7.3 (end of support and are in service extension. Therefore, additional Service Extension fees apply)
* IBM i 7.2 (end of support and are in service extension. Therefore, additional Service Extension fees apply)
* IBM i 7.1 (end of support and are in service extension. Therefore, additional Service Extension fees apply)

**Linux** - {{site.data.keyword.powerSys_notm}} supports Red Hat Enterprise Linux (RHEL) and SUSE Linux Enterprise (SLES) distributions. The following Linux stock images are currently available when you select Full Linux Subscription (learn more about [Full Linux Subscription](/docs/power-iaas?topic=power-iaas-set-full-Linux)):

Red Hat
* RHEL8.4 for SAP HANA (RHEL8-SP4-SAP) 
* RHEL8.4 for SAP NetWeaver (RHEL8-SP4-SAP-NETWEAVER) 
* RHEL 8.4 general purpose (RHEL8-SP4)
* RHEL 8.6 general purpose (RHEL8-SP6)
* RHEL8.6 for SAP HANA (RHEL8-SP6-SAP )             
* RHEL8.4 for SAP NetWeaver (RHEL8-SP6-SAP-NETWEAVER)

SUSE
* SLES 15 SP2 for SAP HANA (SLES15-SP2-SAP)
* SLES 15 SP2 for SAP NetWeaver (SLES15-SP2-SAP-NETWEAVER)
* SLES 15 SP3 for SAP HANA (SLES15-SP3-SAP)
* SLES 15 SP3 for SAP NetWeaver (SLES15-SP3-SAP-NETWEAVER)
* SLES 15 SP3 general purpose (SLES15-SP3)
* SLES 15 SP4 general purpose (SLES15-SP4)
* SLES 15 SP4 for SAP HANA (SLES15-SP4-SAP)
* SLES 15 SP4 for SAP NetWeaver (SLES15-SP4-SAP-NETWEAVER)

The S1022 systems supports RHEL 8.4 (and later) and SLES 15 SP3 (and later) versions. SAP Netweaver is not certified for use with S1022 systems, making them suitable exclusively for non-production workloads.
{: note} 

If you opt for a Linux subscription directly from Red Hat or SUSE, you will need to bring your own image. {{site.data.keyword.powerSys_notm}} supports custom images for following Linux distributions:

General purpose:
* SLES 12 SP4 or later and SLES 15 SP1 or later
* RHEL 8.4 or later

For SAP workloads:
* SLES 12 SP4 or later and SLES 15 SP1 or later
* RHEL 8.1 or later

To view the certification details in the Red Hat catalog, see [IBM Power System E980 (9080-M9S)](https://catalog.redhat.com/cloud/instance-types/detail/5636201){: external} and [IBM Power System S922 (9009-22A)](https://catalog.redhat.com/cloud/instance-types/detail/5636281){: external}. For additional support, refer to the distribution (distro). For instructions, see [Installing and configuring cloud-init on Linux](https://www.ibm.com/support/knowledgecenter/en/SSXK2N_1.4.4/com.ibm.powervc.standard.help.doc/powervc_install_cloudinit_hmc.html){: external}.

## Can I use my own AIX, IBM i, or Linux image?
{: #image}
{: faq}
{: support}

Yes. This function is known as **bring your own image**. For more information, see [Deploying a custom image within a Power Systems Virtual Server](/docs/power-iaas?topic=power-iaas-deploy-custom-image).

## What versions of stock images are available? 
{: #stock-images}
{: faq}
{: support}

For each major version (example: Technology Level) of the operating system (OS) that is enabled through the offering, Power Systems Virtual Server provides a single stock image. PowerVS typically provides stock images for the last three major versions of the supported OS. Any update to the OS stock image is planned only when the image level is certified for PowerVM&trade; environment.

## When are stock images removed from the catalog?
{: #remove-stock-images}
{: faq}
{: support}

Any unsupported and older stock images are periodically removed from the offering. You will be notified three weeks before the images are removed. 

## What happens to VMs deployed using stock images that are being removed?
{: #vm-stock-images}
{: faq}
{: support}

VMs deployed by using stock images that are being removed can continue to operate without any issues. You are recommended to follow operating system vendor’s guidelines to update the OS as needed. 

## What formats should I use when uploading a custom image?
{: #custom-image}
{: faq}

Currently, you can import a custom image in the following formats: _.ova_, _.ova.gz_, _.tar_, _.tar.gz_ and _.tgz_.

## What are the available storage types in the storage area network (SAN)?
{: #storage}
{: faq}
{: support}

All regions use **Tier 1** or **Tier 3** storage types. The **Tier 1** storage type is best for customers who require higher throughput. Customers who do not require exceptionally high throughput and are looking to minimize costs want to select **Tier 3**. A VM cannot have disks from both storage types while provisioning. But, you can add a volume of the other storage types after the VM has been provisioned. For more information, see [Storage tiers](/docs/power-iaas?topic=power-iaas-about-virtual-server#storage-tiers).

The boot image storage type is predefined and cannot be chosen.
{: note}

## How do I extend my AIX rootvg?
{: #rootvg}
{: faq}

By default, the system deploys 20 GBs for the AIX *rootvg*. You can extend the AIX *rootvg* by using the [extendvg](https://www.ibm.com/support/knowledgecenter/ssw_aix_72/e_commands/extendvg.html){: external} command to add a physical volume.

## What's the difference between capped and uncapped shared processor performance? How do they compare to dedicated processor performance?
{: #processor}
{: faq}

When deploying a VM, customers can choose between **dedicated**, **capped shared**, or **uncapped shared** processors for their virtual CPUs (vCPUs). The following list provides a simplified breakdown of their differences:

- **Dedicated**: resources are allocated for a specific client (used for specific third-party considerations)
- **Uncapped shared**: shared among other clients
- **Capped shared**: shared, but resources do not expand beyond those that are requested (used mostly for licensing)

There is a core-to-vCPU ratio of 1:1. For shared processors, fractional cores round up to the nearest whole number. For example, 1.25 cores equals 2 vCPUs. For more information, see [How does shared processor performance compare to dedicated processors](https://community.ibm.com/community/user/power/blogs/pete-heyrman1/2020/06/16/how-does-shared-processor-performance-compare-to-d?CommunityKey=71e6bb8a-5b34-44da-be8b-277834a183b0&tab=recentcommunityblogsdashboard){: external} and [Processor pricing](/docs/power-iaas?topic=power-iaas-pricing-virtual-server#pricing-processor).

|Dedicated processors|
|:-----------------|
| The hypervisor makes a 1:1 binding of a partition’s processor to a physical processor core. Once a VM is activated, the 1:1 binding is static in that a given operating system (OS) logical thread will always run on that same physical hardware. With a dedicated processor partition, you need to size the wanted number of cores to meet the **peak** demand of the partition. For example, if during a typical workday the CPU consumption is around four cores, but it peaks around eight cores, you need to configure the partition with eight cores. Otherwise, you might encounter queuing delays in dispatching applications because there are not enough cores to handle the peak demand.|
{: class="simple-tab-table"}
{: tab-group="processor"}
{: caption="Table 1. Dedicated processors" caption-side="top"}
{: #proc-table-1}
{: tab-title="Dedicated processors"}

|Shared processors|
|:-----------------|
| For shared processors, there are two sharing modes: capped or uncapped. For a capped partition, the amount of CPU time is capped to the value specified for the entitlement. For example, the partition might consume at most 30 seconds of CPU time every minute for a capped partition with processing units set to 0.5. For an uncapped partition, the number of virtual processors defines the upper limit of CPU consumption and not the value that is specified for processing units. For example, if virtual processors are set to 3, the partition might consume 180 seconds of CPU time every minute (three virtual processors each running at 100% utilization would be three physical cores worth of CPU time). There must be unused capacity available on the server for a partition to consume more than its configured processing units.|
{: class="simple-tab-table"}
{: tab-group="processor"}
{: caption="Table 2. Shared processors" caption-side="top"}
{: #proc-table-2}
{: tab-title="Shared processors"}

## How does my current environment compare to what's available through the Power Systems Virtual Server?
{: #performance}
{: faq}

If you'd like to compare your current environment's performance to what's available through the {{site.data.keyword.powerSys_notm}} offering, see the [IBM Power Systems Performance Report](https://www.ibm.com/downloads/cas/K90RQOW8){: external}.

## How do I migrate my VM from one data center to another (WDC04 to DAL13)?
{: #vm-migration}
{: faq}

To migrate your VM from one data center to another, you must capture and export your VM to Cloud Object Storage (COS). After you successfully capture and export your VM, copy it to the COS in the destination region, then perform an import followed by a deploy.

## What does VM pinning do?
{: #pinning}
{: faq}

You can choose to *soft pin* or *hard pin* a VM to the host where it is running. When you *soft pin* a VM for high availability, PowerVC automatically migrates the VM back to the original host once the host is back to its operating state. If the VM has a licensing restriction with the host, the *hard pin* option restricts the movement of the VM during remote restart, automated remote restart, DRO, and live partition migration. The default pinning policy is *none*.

## What does it mean to set an affinity or anti-affinity rule?
{: #affinity}
{: faq}

You can apply affinity and anti-affinity policies to both VMs and volumes.

**VM affinity and anti-affinity policy** allows you to spread a group of VMs across different hosts or keep them on a specific host.

Volume affinity and anti-affinity policy allow you to control the placement of a new volume based on an existing PVM instance (VM) or volume. When you set an affinity policy for a new storage volume, the volume is created within the same storage provider as an existing PVM instance or volume. With an anti-affinity policy, the new volume is created in a different storage provider other than the storage provider the existing PVM instance or volume is located in.

The use of volume affinity policy (affinity or anti-affinity) requires the availability of multiple storage providers. You might experience the following errors when you use a volume affinity policy:

- If an additional storage provider is not available to fulfill the requested policy, you might receive an error that indicates the inability to locate a storage provider to create a volume by using the requested volume affinity policy.

- If additional storage providers exist but the storage providers do not have sufficient space to fulfill the requested policy, you might receive an error that indicates the inability to locate a storage provider with enough free capacity to satisfy the requested volume size.

## How to set a PVM instance to allow attaching mixed storage?
{: #mixed_storage}
{: faq}

You can now attach storage volumes to a PVM instance from different storage tiers and pools, other than the storage pool the PVM instance's root (boot) volume is deployed in. To accomplish this you must modify the PVM instance and set the new PVM instance *storagePoolAffinity* property to false. The PVM instance *storagePoolAffinity* property is set to true by default when the PVM instance is deployed and can be changed only by using the modify PVM instance API. For more information about modifying a PVM instance API, see [Modify PVM Instance](/apidocs/power-cloud#pcloud-pvminstances-put). Attaching mixed storage to a PVM instance has implications on the PVM instance capture, clone, and snapshot features. See [Modify PVM Instance](/apidocs/power-cloud#pcloud-pvminstances-put) API for more details.

## Does IBM provide maintenance for the AIX, IBM i or Linux operating systems?
{: #licensing-os}
{: faq}

No. It is the customer's responsibility to maintain, update, and manage the AIX, IBM i or Linux operating system.

## How does licensing work for the AIX, IBM i, or Linux operating systems?
{: #os-support}
{: faq}

The license for the AIX and IBM i operating systems is part of the overall cost for the workspace. You cannot use an existing license that you already purchased. Refer to the AIX section to learn how to [create an AIX VM](/docs/power-iaas?topic=power-iaas-create-vm).

You can use the movable IBM i (IBM i MOL) to move your existing on premises entitlements to {{site.data.keyword.powerSys_notm}}. Contact support to know more about the IBM i MOL, see [Getting help and support](/docs/power-iaas?topic=power-iaas-getting-help-and-support).

{{site.data.keyword.powerSys_notm}} supports multiple levels of RHEL and SLES. You can either use IBM provided stock Linux images with IBM Full Linux Subscription or bring your own custom Linux image with vendor-provided subscription.

See the [various versions of OSs](/docs/power-iaas?topic=power-iaas-power-iaas-faqs#os-versions) that {{site.data.keyword.powerSys_notm}} supports.

## How does third-party licensing work?
{: #third-party}
{: faq}

Clients are responsible for third-party licensing.

## What are the hardware specifications?
{: #hardware-specs}
{: faq}
{: support}

For more information, see [Hardware specifications](/docs/power-iaas?topic=power-iaas-about-virtual-server#hardware-specifications).

## Do Power Systems Virtual Servers run in a multi-tenant environment?
{: #multi}
{: faq}

Yes, {{site.data.keyword.powerSys_notm}} run in a multi-tenant environment.

## Are there bare-metal options?
{: #bare}
{: faq}

There are no bare-metal options. The {{site.data.keyword.powerSys_notm}} offering focuses on virtual instances.

## Can you tell me more about the snapshotting, cloning, and restoring capabilities?
{: #snapshot}
{: faq}

{{site.data.keyword.powerSys_notm}} provides the capability to capture full, point-in-time copies of entire logical volumes or data sets. Using IBM's *FlashCopy* feature, the [Power Systems Virtual Server API](https://cloud.ibm.com/apidocs/power-cloud#introduction) lets you create delta snapshots, volume clones, and restore your disks. To learn more, see [Snapshotting, cloning, and restoring](/docs/power-iaas?topic=power-iaas-volume-snapshot-clone).

## What are the key differences between a snapshot and clone?
{: #snap-vs-clone}
{: faq}

The key differences are as follows:

| Context | Snapshot | Clone |
|-|-|-|
| Definion | A snapshot is a thin-provisioned group of volumes that cannot be attached to a host or accessed/manipulated. | A clone is created from a snapshot and results in independent volumes which surface in the GUI and can be attached to hosts.|
| Primary function | Revert or restore the source disks to a desired state|Create a complete volume clone|
| Ease of creation | Easy and quick process| Three-step process and takes long time|
| Pricing | Charged 30% of the regular storage rate| target volume storage plus the GRS costs|

See [Snapshots, cloning, and restoring](/docs/power-iaas?topic=power-iaas-volume-snapshot-clone#volume-snapshot-clone) for more detailed information.

## Is there any UI to perform snapshot or clone operations?
{: #snap-clone-ui}
{: faq}

None. You should use the API and CLI to perform snapshot or clone operations. Using the {{site.data.keyword.powerSys_notm}} API and command line interface (CLI) you can create, restore, delete and attach the snap-shots and volume-clones.

**APIs to create snapshot and clone**
- [Create a new volumes clone request and initiates the Prepare action](/apidocs/power-cloud#pcloud-v2-volumesclone-post)
- [Create a PVM Instance snapshot](/apidocs/power-cloud#pcloud-pvminstances-snapshots-post)

**CLIs to create snapshot and clone**
- [Create a snapshot](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#create-snapshot)
- [Create a volume clone for specific volumes](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#create-volume-clone)

## Are there any initial snapshot requirement in terms of storage?
{: #snap-storage-req}
{: faq}

None. The storage is allocated on demand.

## Does the snapshot and volume clone supports any safeguard policy?
{: #snap-clone-safeguard}
{: faq}

None. {{site.data.keyword.powerSys_notm}} does not (currently) provide any options to safeguarded copy (such as cyber protection).

## Can you tell me more about the backup process using the PowerHA Toolkit for IBM i?
{: #poweha-toolkit}
{: faq}

The PowerHA Toolkit for IBM i provides the 5250 user interfaces and automation to use them for backups. In a nutshell, it does the following:
- Automates the memory flush
- Create the volumes-clone
- Attach the clones to a host
- Start the host
- kicki-off the backups
- Move the BRMS data back to the production VM before shutting down the backup VM
- Remove the cloned volumes.

It also allows you to quickly create an intermediate snap-shot then a volumes-clone before entering the long-running volume detach or attach phase. You have the ability to pause the process immediately before attaching volumes.

## How do you set up private networks between Intel&reg; Virtual Servers (x86) and Power Systems Virtual Servers?
{: #connecting}
{: faq}
{: support}

See the tutorial on [IBM Power Systems Virtual Server integration with x86-based workloads](https://cloud.ibm.com/media/docs/downloads/power-iaas-tutorials/PowerVS_and_x86_Integration_Tutorial_v1.pdf).

## How do you set up customer site access to a private network by using VPN?
{: #configuring}
{: faq}
{: support}

For a complete tutorial on site-to-site Virtual Private Network (VPN) connectivity from an on-premise environment to Power Systems Virtual Server, see [IBM Power Virtual Server Virtual Private Network Connectivity](https://cloud.ibm.com/media/docs/downloads/power-iaas-tutorials/PowerVS_VPN_Tutorial_v1.pdf){: external}.
For more information on VPN, see [Managing VPN connections](/docs/power-iaas?topic=power-iaas-VPN-connections).

## What firewall options are there around VPN connectivity?
{: #firewall}
{: faq}

You must set your own firewall in your IBM Cloud account.

## How do you connect a server instance between two data centers (DAL13 to WDC04)?
{: #gts-cloud-connect}
{: faq}
{: support}

You can use IBM Cloud Connect to connect two data centers. IBM Cloud Connect is a software-defined network interconnect service that brings secure connectivity to client locations around the world. For more information, see [Connecting Power Systems Virtual Server instances and networks](/docs/power-iaas?topic=power-iaas-connecting-networks).

IBM Cloud Connect is only available to IBM clients within the US.
{: important}

## How is network bandwidth billed?
{: #billing}
{: faq}
{: support}

**IBM Cloud Classic environment:** Inbound bandwidth is unlimited and not charged. Outbound bandwidth is charged per GB tier with bandwidth offered as an allotment for each month. As an example, for your compute instances, 250 GB is included with each monthly virtual server and 20 TB is included with each monthly bare metal server. Extra bandwidth can also be purchased per packages. For more information, see [Bandwidth packages](https://www.ibm.com/cloud/bandwidth){: external}.

**IBM Power Systems Virtual Server environment:** Inbound bandwidth is unlimited and not charged. Bandwidth is not charged when you use a public network. If you are using a private network with DirectLink Connect, you are charged **IBM Cloud Classic environment** rates.

## What monitoring services are available?
{: #monitoring}
{: faq}

IBM does not provide status and performance monitoring for the Power Systems Virtual Server. Clients must use their own on-premises tools.

## What performance and capacity planning services do you provide for IBM i?
{: #ibmi-performance}
{: faq}

IBM uses the same tools that are on an on-premises system.

## IBM i and solution certification
{: #ibmi-certification}
{: faq}

You can find self-certification and listing information on the [IBM Global Solutions Directory](https://www.ibm.com/partnerworld/public/find-partner-solution){: external}.

## How do I delete a workspace?
{: #delete-service}
{: faq}

To delete a workspace (and all its resources), use the left navigation to navigate the workspace page. Find the workspace to be deleted and click on the overflow menu on the top right corner of the tile. Click **Delete** and confirm the request from the pull-down menu by typing *Delete* in the text field. Finally, click the red **Delete** button to initiate the request.

## How do I delete a single virtual server instance?
{: #delete-service-instance}
{: faq}

There are two methods to delete a virtual server instance. Both deletion methods are manual processes. There is no way to delete all VSIs without deleting the workspace or deleting a subset of the virtual server instance.

- Delete a single virtual server instance from the Virtual server instances page.
Click on the overflow menu (icon with 3 vertical dots) on the far right of each virtual server instance entry on the table. From the pull-down menu, click **Delete** to open the delete confirmation modal. Click **Delete instance** to initiate the deletion request. This action cannot be undone.

- Delete a single virtual server instance from the its details page.
Navigate to the virtual server instance's details page by clicking on the virtual server instance name on the table on the Virtual server instances page. Find and click on the trash icon on the top right of the screen. Confirm the request by clicking **Delete instance**. This action cannot be undone.

## How do I open a support ticket for the Power Systems Virtual Server workspace?
{: #support-ticket}
{: faq}

To open a support ticket, see [Getting help and support](/docs/power-iaas?topic=power-iaas-getting-help-and-support).

## What are the supported databases that I can run for SAP on Power Systems Virtual Server?
{: #support-databases}
{: faq}

On an AIX VM, the following databases are supported:
- IBM Db2 for LUW (Linux, UNIX, and Windows) version 10.5, or later
- Oracle Database version 12.1.0.2, or later
- SAP Adaptive Server Enterprise version 16.0 SP03, or later

On a Linux VM, the following database is supported:
- SAP HANA Platform 2.0 SPS 04, or later

You can find an up-to-date list at [SAP Apps on IBM Power Systems Virtual Server](https://launchpad.support.sap.com/#/notes/2855850){: external}.

## How can I get the WebSphere Application Server that are delivered through the **Web Enablement for i** packages, and are available at no additional charge with IBM i?
{: #web-enablement-for-ibmi}
{: faq}

If you have an IBM i VM instance with the licensed program bundle in the Power Systems Virtual Server offering, you can download the WebSphere Application Server that is available  in the Web Enablement for i software at the Entitled System Support (ESS) website by completing the following steps:

1. Go to the [ESS website](https://www.ibm.com/servers/eserver/ess/index.wss){: external}.

2. Sign in. If this is the first time you are using ESS, refer to the **Help** section on the left menu. Download and read the **ESS_Registration_IBM_Customers_Guidelines** PDF.

3. Go to **My Entitled Software > IBM i evaluation and NLV download**.

4. Find the required software that you can download, install, and use. For example:

    **Web Enablement for i (5722-WE2)** - WebSphere Express V8.5.5
    **Web Enablement for i (5733-WE3)** - WebSphere V9

## How do I run Red Hat OpenShift Container Platform (OCP) on Power Systems Virtual Servers?
{: #ocp_on_powervs}
{: faq}

You can find a complete tutorial at the IBM Developer site: [Deploying Red Hat OpenShift Container Platform 4.x on IBM Power Systems Virtual Servers](https://developer.ibm.com/series/deploy-ocp-cloud-paks-power-virtual-server/){: external}.


## What is the network latency over Direct Link?
{: #network_latency}
{: faq}

Network latency over Direct link is less than 1 millisecond in every location. To know more about network latency, see [Understanding latency](https://cloud.ibm.com/docs/dl?topic=dl-understanding-latency). 

## Are we notified about any planned maintenance activities?
{: #planned_maintenance_activity}
{: faq}

For planned maintenance and disruptive changes, the Power Systems Virtual Server operations team sends you notifications at least 7 days in advance. Watch the Notifications space in the IBM Cloud dashboard for these alerts. You can receive a copy of these notifications directly in your inbox if your email is subscribed for notifications.

## How do I convert existing volumes to replication enabled volumes?
{: #convert-to-replication-vol}
{: faq}

You can  retype the volume to toggle the `replicationEnable` flag of the volume using [Perform an action on a Volume](/apidocs/power-cloud#pcloud-cloudinstances-volumes-action-post) request. This is possible only when the volume pool of existing volume supports replication.

## How can I check whether volume is already replication enabled?
{: #check-for-replication-vol}
{: faq}

You need to check the `replicationEnabled` attribute of the volume. A volume is replicationEnabled when it is true.

## How can I check whether volume is master or auxiliary volume?
{: #check-for-primary-vol}
{: faq}

Volume is auxiliary when `isAuxiliary` field of volume is true.  When `replicationEnabled` is true and `isAuxiliary` is false then volume is a master volume.

## How can I check the serial number of my virtual server instance?
{: #check-serial-no}
{: faq}

The serial number is available after you deploy your virtual server instance and you can choose to display the serial number system value. 

You must pin the IBM i virtual server instances that use the IBM i licenses. If you do not pin the virtual server instances and request a migration to a different host, the serial numbers changes, and the IBM i license will not work.

## What should I do If I do not see the latest information in the UI?
{: #ui-not-updated}
{: faq}

Consider the following if you do not see an update in the User Interface(UI):

1. Power System Virtual Server utilizes a new caching mechanism for some resources to ensure that UI refresh operations complete in a timely manner.
2. In some scenarios out-dated information may be shown while the cache is updated, for approximately four minutes.
3. You can refresh the page to trigger an update to the cached data, eventually leading to the updated information's display.
4. When the DC has a heavy amount of traffic, and the cache has not been refreshed within the last four minutes, Power System Virtual Server UI may display an error message. A subsequent page refresh will retrieve and display the updated information.

## Why I cannot see the storage pool and tier of my boot images?
{: #stock-image-copy-improve}
{: faq}

IBM improved the performance of copying a stock image into customers' accounts. As a result of this new feature, the newly copied stock image acts like an image reference, where volumes are not accessible to the user. The improved process now offers:
1.  Faster copy of stock image to your private project.
2.  The stock image cannot be exported. One can do VM capture and export on a deployed VM that uses the stock image.
3.  Storage pool and tier of a stock image shows "Empty" (API) or "Any" (UI) as VM can be deployed to any tier/pool by using the stock image.

## Can I select a specific resource group when I create a cloud connection?
{: #cc-res-group}
{: faq}

NO. When you create a cloud connection by using {{site.data.keyword.powerSys_notm}}, the cloud connection is always created in the default resource group even if you choose a specific resource group.

## What is the Maximum Transmission Unit (MTU) size supported in {{site.data.keyword.powerSys_notm}} networks?
{: #mtu-max}
{: faq}

The {{site.data.keyword.powerSys_notm}} supports a smaller MTU size of 1476 bytes for the public network interfaces and for the private network interfaces that are attached to a {{site.data.keyword.powerSys_notm}} VPN.

## Can I automate the Maximum Transmission Unit (MTU) configuration?
{: #mtu-config}
{: faq}

Yes, you can automate the network configurations such as the Maximum Transmission Unit (MTU).

To automate the MTU configuration, you need to customize your cloud-init network configuration. For more information, see the [Cloud-init docs on network configuration](https://cloudinit.readthedocs.io/en/latest/reference/network-config-format-v1.html){: external}.

Both AIX and IBM i supports custom cloud-init configurations at the time of {{site.data.keyword.powerSys_notm}} instace (VM) deployment. 

You can customize the cloud-init configurations only through the {{site.data.keyword.powerSys_notm}} API. The custom cloud-init is specified by the `userData` request parameter. For more information, see [Create a new Power VM Instance](https://cloud.ibm.com/apidocs/power-cloud#pcloud-pvminstances-post).