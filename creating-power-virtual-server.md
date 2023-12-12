---

copyright:
  years: 2019, 2023

lastupdated: "2023-12-12"

keywords: getting started, {{site.data.keyword.powerSys_notm}}, configure instance, processor, profile, networking

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
{:external: target="_blank" .external}
{:help: data-hd-content-type='help'}
{:support: data-reuse='support'}

# Creating a {{site.data.keyword.powerSys_notm}}
{: #creating-power-virtual-server}
{: help}
{: support}

To create and configure an IBM&reg; Power Systems&trade; Virtual Server, complete the following steps.
{: shortdesc}

## Creating a {{site.data.keyword.powerSys_notm}} workspace
{: #creating-service}

1. Log in to the [IBM catalog](https://cloud.ibm.com/catalog){: external} with your credentials.

2. In the catalog's search box, type **{{site.data.keyword.powerSys_notm}}** and click the **Workspace for {{site.data.keyword.powerSys_notm}}** tile.

3. Click **Create workspace**.

4. Specify a name for your workspace and choose where you'd like to deploy your {{site.data.keyword.powerSys_notm}} instance. See the following table to select the appropriate region for your workspace.

    Japanese language support for IBM i is supported in OSA21, SAO01, TOK04, DAL12, FRA04, FRA05, and SYD05 data centers.
    {: note}

    | Geography | Location | Region | IBM Power infrastructure zone | IBM Cloud Classic infrastructure data center | IBM Cloud VPC infrastructure zone |
    | --------- | -------- | ------ | ----------------------------- | ----------------- | ----------------------- |
    | America | Dallas, USA | us-south | DAL10 \n DAL12 \n us-south | DAL10 \n DAL12 \n DAL13 | us-south-1 \n us-south-2 \n us-south-3 |
    | America | Washington DC, USA | us-east | us-east \n WDC06 \n WDC07| WDC04 \n WDC06 \n WDC07| us-east-1 \n us-east-2 \n us-east-3|
    | America | São Paulo, Brazil | br-sao | SAO01 \n SAO04| SAO01 \n SAO04| br-sao-1 \n br-sao-2 |
    | America | Toronto, Canada | ca-tor | TOR01 | TOR01 | ca-tor-1 |
    | America | Montreal, Canada | ca-mon | MON01 | MON01 | - |
    | Europe | Frankfurt, Germany | eu-de | eu-de-1 \n eu-de-2 | FRA04 \n FRA05 | eu-de-2 \n eu-de-3 |
    | Europe | London, UK | eu-gb | LON04 \n LON06 | LON04 \n LON06 | eu-gb-1 \n eu-gb-3 |
    | Europe | Madrid, Spain| eu-es | MAD02 \n MAD04 | MAD02 \n MAD04 | eu-es-1 \n eu-es-2|
    | Asia Pacific | Sydney, Australia | au-syd | SYD04 \n SYD05 | SYD04 \n SYD05 | au-syd-2 \n au-syd-3 |
    | Asia Pacific | Tokyo, Japan | jp-tok | TOK04 | TOK04 | jp-tok-2 |
    | Asia Pacific | Osaka, Japan | jp-osa | OSA21 | OSA21 | jp-osa-1 |
    {: caption="Table 1. {{site.data.keyword.powerSys_notm}} data centers" caption-side="bottom"}

5. Click **Create**. You are redirected to the **Workspaces** page where you can select your desired or existing workspace.

## Configuring a {{site.data.keyword.powerSys_notm}} instance
{: #configuring-instance}

To begin, create a [{{site.data.keyword.powerSys_notm}} workspace](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#creating-service) and select a workspace.

1. Log in to the [IBM catalog](https://cloud.ibm.com/catalog){: external} with your credentials.

2. In the catalog's search box, type **{{site.data.keyword.powerSys_notm}}** and click the **Workspace for {{site.data.keyword.powerSys_notm}}** tile.

3. Click **Select workspace** on the left navigation under **Workspace** of the {{site.data.keyword.powerSys_notm}} user interface to select from a list of previously created workspace. 
   If you do not have a workspace, click **Create a workspace**.

4. Click **Virtual server instances**.
   
    Make sure you select the desired workspace to display all the virtual server instances you have already created. You must refresh the page to see the updated information if you see outdated information. For more information, see the FAQ page on [What should I do if I do not see the latest information in the UI](/docs/power-iaas?topic=power-iaas-power-iaas-faqs#ui-not-updated).
    {: important}

5. Click **Create instance**. If you select more than one instance under **Number of instances**, you are presented with additional options.

    The total due per month is dynamically updated in the **Order Summary** based on your selections. You can easily create a cost-effective {{site.data.keyword.powerSys_notm}} instance that satisfies your business needs.
    {: tip}
    
    You must pin the IBM i virtual server instances that use the IBM i licenses. If you do not pin the virtual server instances and request for migration to a different host, the serial numbers will change, and the IBM i license will not work.
    {: important}

6. Choose an existing SSH key or create one to securely connect to your {{site.data.keyword.powerSys_notm}}.

7. Complete the **Boot image** fields as instructed by your organization. When you select **Boot image**, the {{site.data.keyword.powerSys_notm}} user interface allows you to select boot images from a set of available stock images or from a custom image in your image catalog. Custom images are images that you have imported from IBM COS or created from a PVM instance (VM) capture. When you select a stock image, you must also select the storage type (tier) and the storage pool selection. 
   
    You can select a For more information, see [Storage tiers](/docs/power-iaas?topic=power-iaas-about-virtual-server#storage-tiers).

    If you select AIX as the boot image, the {{site.data.keyword.powerSys_notm}} user interface provides you with an option to configure the VM instance for epic workload. For more information on epic, see [configuring a VM for EPIC workloads](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#configuring-a-vm-for-epic-workloads).

    If you select IBM i as the boot image, the {{site.data.keyword.powerSys_notm}} user interface provides you with an option to include the following licenses to your VM instance: *IBM i Cloud Storage Solution*, *IBM i Power HA*, *IBM Db2 Web Query for i*, and *Rational Dev Studio for IBM i*. Adding a license increases the service cost. The selected licenses are injected to your VM instance. You can install specific solutions on your VM instance, and the licenses are automatically set. If you want to use these licensed programs on your IBM i VM instance, you must order these licenses through {{site.data.keyword.powerSys_notm}}. You cannot use existing licenses in your VM instance.

    Cloud Optical Repository (COR) is a virtual image that can be deployed and used as a Network File Server (NFS) to perform various IBM i tasks that require media. This virtual optical image includes a collection of the media necessary for various IBM i tasks, for all supported IBM i releases. With the COR image deployed, a second {{site.data.keyword.powerSys_notm}} Instance can be deployed on the same VLAN that is set up as the client and pointed to the COR (target) NFS Server Instance. For more information on COR images, see [Cloud Optical Repository](https://cloud.ibm.com/media/docs/downloads/power-iaas/Cloud_Optical_Repository.pdf){: external}.

8.  Select your **Machine type**, the number of **Cores**, the amount of **Memory (GB)** and whether you'd like a **Dedicated processor**, **Uncapped shared processor**, or **Capped shared processor**.

    There is a core-to-vCPU ratio of 1:1. For shared processors, fractional cores round up to the nearest whole number. For example, 1.25 cores equal 2 vCPUs. For more information on processor types, see [What's the difference between capped and uncapped shared processor performance? How does they compare to dedicated processor performance?](/docs/power-iaas?topic=power-iaas-power-iaas-faqs#processor). If the machine type is S922 & S1022 and the operating system is IBM i, IBM i supports a maximum of 4 cores per VM.
    {: important}

    When using an AIX stock image as the boot volume, a console session is required for the initial setting of the root user password. Without completing this step, SSH login appears as being *disabled*. For more information, see [How to create a new AIX VM with SSH keys for root login](/docs/power-iaas?topic=power-iaas-create-vm).

9.  You can use the user interface to set the affinity policies for storage pools only when the total number of VMs in your account is less than 100. If your account has more than 100 VMs, then you must use the CLI or API to set the volume affinity policies.

    Select one of the following Storage pool options: 
    - **Auto-select pool**: Use this option to allow the system to automatically select a storage pool for the storage tier with sufficient capacity. 
  
    - **Affinity**: Use this option to identify the storage pool that must be used to place the boot volumes based on an existing PVM instance (VM) or storage volume from your account. The new storage volumes for the VM will be placed in the same storage pool where the affinity object resides. If you are using a PVM instance as the affinity object, the storage pool that is selected is based on the PMV instance's root (boot) volume.  
  
    - **Anti-affinity**: Use this option to identify one or more storage pools that you want to exclude from getting selected to place the boot volumes based on one or more existing PVM instances (VMs) or storage volumes from your account. While choosing a storage pool to create the custom image storage volumes, the storage pools in which the list of anti-affinity object(s) reside will not be selected. If you are using PVM instances as the anti-affinity objects, the storage pools are excluded depending on each PVM instance’s root (boot) volume that you specified.

    To learn more about the flexible tier offering of {{site.data.keyword.powerSys_notm}}, see: [Storage tiers](/docs/power-iaas?topic=power-iaas-about-virtual-server#storage-tiers)

    For more information about affinity and anti-affinity policy, see [What does it mean to set an affinity or anti-affinity rule?](/docs/power-iaas?topic=power-iaas-power-iaas-faqs#affinity).

    All volumes created during VM provisioning are created on the same storage pool as the boot volume irrespective of their tier selection.
    {: note}
    
10. Finally, define your **Network interfaces** by adding a public network, private network, or both. When adding an existing private network, you can choose a specific IP address or have one auto-assigned.

    For an AIX VM, network interface controllers (NICs) are assigned based on the order in which you specify them during creation. To display information about all of the network interfaces after provisioning, open the AIX console and type `ifconfig -a`.
    {: note}

11. Accept the **Terms of Use** and click **Create instance** to provision a new {{site.data.keyword.powerSys_notm}}. To view your boot images, go to **Boot images** after you provision the instance.

Refer to the following table for more information on each {{site.data.keyword.powerSys_notm}} instance field.

| Field | Description |
|----------|---------|
| General | **Instance name**: Specify an apt name for your virtual server instance. \n **Number of Instances** : Specify the number of instances that you want to create for the {{site.data.keyword.powerSys_notm}}. You can apply placement groups only when you are creating a single VM instance. If you choose the Machine type as E980, you can choose [anti-affinity policy](/docs/power-iaas?topic=power-iaas-power-iaas-faqs#affinity) with maximum of 2 VM instances. \n **Placement group**: If you are creating only one instance, you can choose the placement group to control on which host this instance will be hosted on. Select a placement group from the list. To create a new placement group select one of the following options: \n Same server : Select this option to place the VM on the same host. \n Different server : Select this option to place the VM on a different host.  \n **Colocation rules**: If you specify more than one instance, you can select the following naming conventions and colo rules: \n **No preference**: Select this option if you do not have a hosting preference. \n **Same server** : Select this option to host all instances on the same server. A placement group is automatically created. The instance name previously provided will be used as the group name and cannot be edited. \n **Different server** :  Select this option to host each instance on a different server. You can use this option if you are concerned about a single-server outage that might affect all {{site.data.keyword.powerSys_notm}} instances. A placement group is automatically created. The instance name previously provided will be used as the group name and cannot be edited. \n **Numerical prefix** : Select this option to add numbers before the name of the virtual server. If, for example, the first {{site.data.keyword.powerSys_notm}} name is *Austin* the next name for the virtual instance is *1Austin*. \n **Numerical postfix** : Select this option to add numbers after the name of the virtual server. If, for example, the first {{site.data.keyword.powerSys_notm}} name is *Austin* the next name for the virtual instance is *Austin1*. \n **VM pinning** : Select this option to pin your virtual server instance. You can choose either a *soft* or *hard* pinning policy. \n [Learn more](/docs/power-iaas?topic=power-iaas-power-iaas-faqs#pinning). \n **Note:** When you create multiple instances of the virtual server, you must select **On** from the **Shareable** field for each data volume that you add. If you do not want the data volume to be shareable, you can add the data volume after you create the virtual server. For IBM i OS you cannot have shareable data volumes.|
| Machine type | Specify the machine type. The machine type that you select determines the number of cores and memory that is available. For more information about hardware specifications, see<!-- [E880 (Dallas only)](https://www-01.ibm.com/common/ssi/ShowDoc.wss?docURL=/common/ssi/rep_sm/5/872/ENUS9119-_h05/index.html&lang=en){: external}, --> [S922](https://www.ibm.com/downloads/cas/KQ4BOJ3N){: external}, and [E980 (Data centers other than Dallas and Washington)](http://www-01.ibm.com/support/docview.wss?uid=ssm1platformaix9080-M9S-vios-only){: external}. |
| Cores | There is a core-to-vCPU ratio of 1:1. For shared processors, fractional cores round up to the nearest whole number. For example, 1.25 cores equals 2 vCPUs. |
| Memory | Select the amount of memory for the {{site.data.keyword.powerSys_notm}}. If you choose to use more than 64 GBs of memory per core, you are charged a higher price. For example, when you choose one core with 128 GBs of memory, you are charged the regular price for the first 64 GBs. After the first 64 GBs (64 - 128 GBs), you are charged a higher price. |
| Boot image | Select a version of the IBM-provided AIX or IBM i operating system stock image. You can also select Linux stock images for SAP HANA and SAP NetWeaver applications. For these SAP stock images it is mandatory to set an SSH key while creating the VM. You will be able to access the VM instance only via SSH after launch. However, it is recommended to set a password by using the `passwd` command during the first SSH access. By setting a password, you are able to access the instance in the UI console. You can also [deploy your own custom image](/docs/power-iaas?topic=power-iaas-deploy-custom-image) of AIX, IBM i, or Linux. IBM also provides a community supported CentOS image under Linux operating system. However, IBM does not provide any support for this image. For CentOS support, see the [CentOS forum](https://forums.centos.org/){: external} or [FAQ](https://forums.centos.org/app.php/help/faq){: external} page. {{site.data.keyword.powerSys_notm}} now supports Linux (RHEL and SLES) stock images for non-SAP applications. \n To provision {{site.data.keyword.powerSys_notm}} instance that supports SAP HANA and SAP NetWeaver applications, see [Provisioning your IBM Power Virtual Server](/docs/sap?topic=sap-power-vs-set-up-infrastructure#power-vs-provision-server). \n **Important:** When you use an AIX stock image as the boot volume, a console session is required for the initial setting of the root user password. Without completing this step, SSH login as root appears as being *disabled*. \n For IBM i operating system licensing information, see [IBM i License Program Products (LPP) and Operating System (OS) feature bundles](/docs/power-iaas?topic=power-iaas-ibmi-lpps). |
| Attached volumes | You can either create a new data volume or attach an existing one that you defined in your account. \n **Create volume**: Click **Create volume** to create a new data volume for your {{site.data.keyword.powerSys_notm}} instance. Enter the **Name in VSI**, choose the desired **Size**, **Quantity**, and **Tiers**.If you want to allow multiple virtual instances to write data to the same data volume, you must click **On** under **Shareable**. \n **Attached Volume**: You can select an existing data volume from the **Attached volumes** list. If a previously used data volume does not appear, it might exist under a different account or resource instance. |
| Public Networks | Select this option to use an IBM-provided public network. There is a cost that is associated with selecting this option. \n [Learn more](/docs/power-iaas?topic=power-iaas-about-virtual-server#public-private-networks) |
| Private Networks | Click **Add** to identify a new private network for the virtual server. If you already added a private network, you can select it from the list. For more information, see [Configure private network](/docs/power-iaas?topic=power-iaas-configuring-subnet).|
{: caption="Table 2. {{site.data.keyword.powerSys_notm}} instance fields" caption-side="bottom"}

## Dedicated host
{: #dedicated-host}

The dedicated host feature on IBM {{site.data.keyword.powerSys_notm}} significantly expands the range of computing options available by providing the ability to provision a dedicated host for your exclusive use. Dedicated hosts are metered by the hour for the entire capacity of the host. 

A dedicated host provides an additional flexibility to create virtual server instances, control their placement, and utilize the unique shared processor pool capabilities that are offered by {{site.data.keyword.powerSys_notm}}. With dedicated hosts, you can more easily optimize your cloud infrastructure by utilizing single tenant servers to manage software licensing costs while increasing isolation from other users in a cloud environment.   

<!-- Dedicated hosts are ideal for your environment if you need a high level of customization and control over your cloud infrastructure, while also benefiting from the scalability and cost-effectiveness of cloud computing. -->

The dedicated host provides the following features:
1.	Reserve a host server (IBM Power S922 or S1022) for your exclusive use. All cores and memory on the host are provisioned for your use.
2.	Flexibly create virtual server instances and place them on the dedicated host.  
3.	Create shared processor pools on the dedicated host and flexibly manage resource utilization including the Virtual Processor (VP) to Entitled Capacity (EC) ratio up to 1:20.
    
Dedicated hosts are rolled out in two phases – Select Availability and General Availability. Select Availability is in `DAL10`, `DAL12`, `WDC06`, and `WDC07` data centers. General Availability will expand the reach of dedicated host capabilities further around the world.
{: note}

## Reusing Volume names or VM names in Power System Virtual Servers
{: #reusing_volume_names}

You can deploy a Power System Virtual Server VM by specifying any name. If you want to delete that VM and deploy a new VM with the same name, you must allow 1 hour between deleting the original instance and creating a VM by using the same name again.

For example, you create a VM with the name TEST-VM and you delete this VM later. The name "TEST-VM" is not immediately available for reuse. Before you attempt to use the name TEST-VM again, you must allow 1 hour to pass after the VM was deleted.


## Implementing SAP NetWeaver and SAP HANA in the {{site.data.keyword.powerSys_notm}} environment
{: #sap_netweaver_hana}

You can deploy SAP NetWeaver on an AIX or Linux&reg; operating system, and SAP HANA on Linux operating system, in your {{site.data.keyword.powerSys_notm}} environment. You must consider several SAP-specific infrastructure requirements to run SAP applications on {{site.data.keyword.powerSys_notm}}s. For more information, see [Planning your deployment](https://cloud.ibm.com/docs/sap?topic=sap-power-vs-planning-items) and [Deploying your infrastructure](https://cloud.ibm.com/docs/sap?topic=sap-power-vs-set-up-infrastructure).

On IBM Power Systems E980 that are running in a multiple VM environment with at least one SAP HANA production system, you can deploy up to sixteen VMs per physical server with dedicated or dedicated-donating processor cores. Each concurrently running VM instance must be configured according to the workload and must fulfill the SAP HANA Hardware Configuration Check Tool (HWCCT) key performance indicators (KPIs). You must also consider the minimum number of CPU cores and memory size of VMs as described in SAP Note 2188482. For more information see, [SAP support Launchpad](https://launchpad.support.sap.com/#/notes/2230704){: external}. You must have an SAP ID to access this web page.

## Configuring a VM for Epic workloads

{: #configure-vm-epic}

You can configure your virtual server instance to deploy Epic workloads when you select AIX as your operating system.

To configure a VM instance for Epic workloads, select the **Configure for Epic workloads** checkbox on the **Boot image** tile. You can verify whether the deployed VM supports Epic workloads by checking the corresponding VM details page. On the VM details page, the **Deployment type** field must be se to **Epic**.

In the VM details page, for the VMs on which Epic workloads are supported, you must not create or attach volumes from Tier 3 to avoid performance issues.
{: warning}

For the VMs on which Epic workloads are supported and are in shut-down state, you must not change the core type to any value other than dedicated to avoid performance issues.
{:important}

The following table explains the difference in VM configuration that may or may not support Epic workloads:

|VM deployed for|Storage volume|Core type|Machine type|
|-----|------|-----|-----|
|Non-epic workloads|Tier 1 or Tier 3|Shared uncapped, \n shared capped, or \n dedicated|S922 or E980|
|Epic workloads|Always Tier 1|Always dedicated|Always E980|
{: caption="Table 2. VM configuration difference that supports non-Epic and Epic workloads" caption-side="bottom"}

The epic VMs are not pinned by default that you can use internally for non production usage. You must consider pinning the production epic VMs to avoid performance issues.
{:note}

You can choose to configure a VM for Epic workloads only when you select AIX as your operating system. The other conditions that apply are as follows:

1. Epic workloads is supported on AIX 7.2, and later. You cannot choose AIX 7.1.
2. Supported storage volume is Tier 1. You can change or attach Tier 3 storage volume. This lead, to performance issues.
3. Supported machine type is E980. You cannot select S922.
4. Supported core type is dedicated. You can switch to other core type, but it might lead, to performance issues.
