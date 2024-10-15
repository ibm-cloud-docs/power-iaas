---
copyright:
  years: 2019, 2024

lastupdated: "2024-10-15"

keywords: getting started, {{site.data.keyword.powerSys_notm}}, configure instance, processor, profile, networking, large volumes, ibm i 500 volume, boot vm, epic

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Creating an IBM {{site.data.keyword.powerSys_notm}}
{: #creating-power-virtual-server}
{: help}
{: support}

---

IBM {{site.data.keyword.powerSys_notm}} located in IBM data centers: [Off-premises]{: tag-blue}

IBM {{site.data.keyword.powerSys_notm}} Private Cloud: [On-premises]{: tag-red}

---

To create and configure an {{site.data.keyword.powerSysFull}}, complete the following steps.
{: shortdesc}


## Creating a {{site.data.keyword.powerSys_notm}} workspace
{: #creating-service}

1. Log in to the [IBM Cloud catalog](https://cloud.ibm.com/catalog){: external} with your credentials.
2. In the search box, type **{{site.data.keyword.powerSys_notm}}** and click the **{{site.data.keyword.powerSys_notm}}** tile.
3. Click **Create a workspace**.
4. Select **Location type** as On-premises or Off-premises.

   For On-premises location types, select the name of the created satellite location from the **Satellite Location** drop-down list.

   For Off-premises location types, select the IBM Cloud region that is closest to your physical location from the Satellite Location drop-down list. For the list of available IBM Cloud regions, see [IBM Cloud regions](/docs/power-iaas?topic=power-iaas-ibm-cloud-reg).

5. In the **Details** section, provide a name for the workspace and select the resource groups.
6. Click **Continue**. The selected workspace details are displayed on the Summary page.
   Review the estimated cost on the Summary page.
7. Select **I agree to the Terms and conditions** checkbox.
8. Click **Create**. You are redirected to the **Workspaces** page where you can select an existing workspace.


For more information about appropriate region for your workspace, see [IBM Cloud regions](/docs/power-iaas?topic=power-iaas-ibm-cloud-reg).

## Configuring a {{site.data.keyword.powerSys_notm}} instance
{: #configuring-instance}

To create a virtual server instance, you must first create a [{{site.data.keyword.powerSys_notm}} workspace](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#creating-service) and select a workspace. The created workspaces are listed under **Workspaces** of the {{site.data.keyword.powerSys_notm}} user interface in the left navigation page. Select the workspace for which you want to create an instance. Complete the following steps to create a virtual machine instance:

1. Click **Virtual server instances** on the left page.

    Select a workspace to display all the virtual server instances you have provisioned. You must refresh the page to see the updated information if you see outdated information. For more information, see the FAQ page [What should I do when I do not see the latest information in the UI](/docs/power-iaas?topic=power-iaas-powervs-faqs#ui-not-updated).
    {: important}

    The virtual server instances that are associated with the selected workspace are displayed.

    [On-premises]{: tag-red} if an error occurs immediately after creating or opening the virtual server instance, you must delete it.
    {: note}

2. To create a new instance, click **Create instance**.

    If you select more than one instance under **Number of instances**, additional options are displayed.

    The total due per month is dynamically updated in the **Order Summary** based on your selections. You can easily create a cost-effective {{site.data.keyword.powerSys_notm}} instance that satisfies your business needs.
    {: tip}

    You must pin the IBM i virtual server instances that use the IBM i licenses. If you do not pin the virtual server instances and request for migration to a different host, the serial numbers change and the IBM i license will not work.
    {: important}

3. Choose an existing SSH key or create one to securely connect to your {{site.data.keyword.powerSys_notm}}.

4. Complete the **Boot image** fields.

    You can create or provision a virtual server instance (VM) without any initial boot image volume. VMs without boot volume are helpful in [high availability and disaster recovery](/docs/power-iaas?topic=power-iaas-ha-dr) use cases. A VM can be created without boot volume and the volume which is cloned or replicated can be attached to VM to bring the backed up VM.

    Select the **Deploy empty virtual server instance** checkbox to provision a VM without a boot volume. For more information, see [Provisioning a virtual machine without an initial boot volume](#empty-vm).

    You can create a VM without a boot volume for AIX, IBM i, and Linux (with a subscription provided by IBM) operating systems.
    {: important}

    You can set the affinity policies for storage pools. For more information, see [Configuring affinity policies](#affinity-pol).


    When you select **Boot image**, the {{site.data.keyword.powerSys_notm}} user interface allows you to select the boot images from a set of available stock images or from a custom image in your image catalog. Custom images are images that you can import from IBM Cloud Object Storage or create from a virtual server instance (VM) capture. When you select a stock image, you must also select the storage tier and the storage pool. When you select a custom image, the new VMs are deployed into the same storage tier and pool where the image resides. You must select a storage type for stock images. Currently, you cannot mix **Tier 1** and **Tier 3** storage types. For more information, see [Storage tiers](/docs/power-iaas?topic=power-iaas-on-cloud-architecture#storage-tiers).

    [On-premises]{: tag-red} if you select a custom image from a local catalog, the VMs are deployed on a single storage tier.
    {: note}

    If you select AIX as the boot image, the {{site.data.keyword.powerSys_notm}} user interface provides you with an option to configure the VM instance for epic workload. For more information on epic, see [configuring a VM for EPIC workloads](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#configuring-a-vm-for-epic-workloads).

    If you select IBM i as the boot image, the {{site.data.keyword.powerSys_notm}} user interface provides you with an option to include the following licenses to your VM instance:
    - IBM i Cloud Storage Solution
    - IBM i Power HA, and
    - Rational Dev Studio for IBM i.

    Adding a license increases the service cost. The selected licenses are injected to your VM instance. You can install specific solutions on your VM instance, and the licenses are automatically set. If you want to use these licensed programs on your IBM i VM instance, you must order these licenses through {{site.data.keyword.powerSys_notm}}. You cannot use existing licenses in your VM instance.

    

    If you select Full Linux Subscription (FLS) images, the {{site.data.keyword.powerSys_notm}} user interface provides you with an option to pass in user data or scripts during the first boot runtime. There are some validation checks in place for Linux images on the user data that you enter. No validation checks are done for AIX and Bring Your Own License (BYOL) images. For more information, see [Passing user-defined scripts](/docs/power-iaas?topic=power-iaas-set-full-Linux#cloud-init-fls).

    Cloud Optical Repository (COR) is a virtual image that can be deployed and used as a Network File Server (NFS) to perform various IBM i tasks that require media. This virtual optical image includes a collection of the media necessary for various IBM i tasks, for all supported IBM i releases. With the COR image deployed, a second {{site.data.keyword.powerSys_notm}} Instance can be deployed on the same VLAN that is set up as the client and pointed to the COR (target) NFS Server Instance. For more information on COR images, see [Cloud Optical Repository](https://cloud.ibm.com/media/docs/downloads/power-iaas/Cloud_Optical_Repository.pdf){: external}.

5. Complete the **Profile** fields, which will require you to select the **Machine type**, the number of **Cores**, the amount of **Memory (GB)** and **Core type**.

    There is a core-to-virtual core ratio of 1:1. For shared processors, fractional cores round up to the nearest whole number. For example, 1.25 cores equals 2 virtual cores. For more information about processor types, see [What's the difference between shared capped and shared uncapped processor performance? How does they compare to dedicated processor performance?](/docs/power-iaas?topic=power-iaas-powervs-faqs#processor). If the machine type is S922 and the operating system is IBM i, IBM i supports a maximum of 4 cores per VM.
    {: important}

    When using an AIX stock image as the boot volume, a console session is required for the initial setting of the root user password. Without completing this step, SSH login appears as disabled. For more information, see [How to create a new AIX VM with SSH keys for root login](/docs/power-iaas?topic=power-iaas-create-vm).

6.  Complete the **Storage volumes** fields to attach or create new volumes and associate them with the virtual server instance.

    Under **Advanced configurations**, enable the **Configure for large quantity volumes** toggle button to support more than 127 (up to 500) volumes. This is a VM-level setting that remains unmodifiable upon provisioning.

    Machine types E980 and E1080 are optimized to support the attachment of large quantity of volumes. Only IBM i VMs support the configuration of large volumes. You cannot create or attach volumes with more than 2 TB for IBM i VMs.
    {: note}

    For more information, see [Configuring for large quantity of volumes](#config-large-vol).

7.  Define your **Network interfaces** by adding a public network, private network, or both. When adding an existing private network, you can choose a specific IP address or have one auto-assigned.

    When you choose to provide a specific IP address, ensure that the IP address is not listed under [reserved IP](/docs/power-iaas?topic=power-iaas-configuring-subnet#reserv-ip).
    {: important}

    For an AIX VM, network interface controllers (NICs) are assigned based on the order in which you specify them during creation. To display information about all the network interfaces after provisioning, open the AIX console and type `ifconfig -a`.
    {: note}

8.  Accept the **Terms of Use** and click **Create instance** to provision a new {{site.data.keyword.powerSys_notm}}. To view your boot images, go to **Boot images** after you provision the instance.

    If your account has fewer than 100 VMs, you can use the {{site.data.keyword.powerSys_notm}} user interface to view the VMs. If your account has more than 100 VMs, the VMs might not be display in the user interface. You can reduce the number of VMs by using the CLI or API so that they are displayed again on the user interface.
    {: note}


The following table provides more information about each {{site.data.keyword.powerSys_notm}} instance field.

| Field | Description |
|----------|---------|
| General | **Instance name**: Specify a name for your virtual server instance. \n **Number of Instances** : Specify the number of instances that you want to create for the {{site.data.keyword.powerSys_notm}}. You can apply placement groups only when you are creating a single VM instance. If you choose the Machine type as E980, you can choose an [anti-affinity policy](/docs/power-iaas?topic=power-iaas-powervs-faqs#affinity) with maximum of 2 VM instances. \n **Placement group**: If you are creating only one instance, you can choose the placement group to control on which host this instance will be hosted on. Select a placement group from the list. To create a new placement group, select one of the following options: \n Same server : Select this option to place the VM on the same host. \n Different servers : Select this option to place the VM on a different host.  \n **Colocation rules**: If you specify more than one instance, you can select the following naming conventions and colo rules: \n **No preference**: Select this option if you do not have a hosting preference. \n **Same server** : Select this option to host all instances on the same server. A placement group is automatically created. The instance name that is previously provided will be used as the group name and cannot be edited. \n **Different server** :  Select this option to host each instance on a different server. You can use this option if you are concerned about a single-server outage that might affect all {{site.data.keyword.powerSys_notm}} instances. A placement group is automatically created. The instance name that is previously provided will be used as the group name and cannot be edited. \n **Numerical prefix** : Select this option to add numbers before the name of the virtual server. If, for example, the first {{site.data.keyword.powerSys_notm}} name is *Austin* the next name for the virtual instance is *1Austin*. \n **Numerical postfix** : Select this option to add numbers after the name of the virtual server. If, for example, the first {{site.data.keyword.powerSys_notm}} name is *Austin* the next name for the virtual instance is *Austin 1*. \n **VM pinning** : Select this option to pin your virtual machine. You can choose either a *soft* or *hard* pinning policy. \n [Learn more](/docs/power-iaas?topic=power-iaas-powervs-faqs#pinning). \n **Note:** When you create multiple instances of the virtual server, you must select **On** from the **Shareable** field for each data volume that you add. If you do not want the data volume to be shareable, you can add the data volume after you create the virtual server. For IBM i OS you cannot have shareable data volumes.|
| Machine type | Specify the machine type. The machine type that you select determines the number of cores and memory that is available. For more information about hardware specifications, see [E880 (Dallas only)](https://www-01.ibm.com/common/ssi/ShowDoc.wss?docURL=/common/ssi/rep_sm/5/872/ENUS9119-_h05/index.html&lang=en){: external},  [S922](https://www.ibm.com/downloads/cas/KQ4BOJ3N){: external} and [E980 (Data centers other than Dallas and Washington)](http://www-01.ibm.com/support/docview.wss?uid=ssm1platformaix9080-M9S-vios-only){: external}. |
| Cores | There is a core-to-virtual core ratio of 1:1. For shared processors, fractional cores round up to the nearest whole number. For example, 1.25 cores equals 2 virtual cores. |
| Memory | Select the amount of memory for the {{site.data.keyword.powerSys_notm}}. If you choose to use more than 64 GBs of memory per core, you are charged a higher price. For example, when you choose one core with 128 GBs of memory, you are charged the regular price for the first 64 GBs. After the first 64 GBs (64 - 128 GBs), you are charged a higher price. |
| Boot image | Select a version of the IBM-provided AIX or IBM i operating system stock image. You can also select Linux stock images for SAP HANA and SAP NetWeaver applications. For the SAP stock images it is mandatory to set an SSH key while creating the VM. You will be able to access the VM instance only via SSH after launch. However, it is recommended to set a password by using the `passwd` command during the first SSH access. By setting a password, you are able to access the instance in the UI console. You can also [deploy your own custom image](/docs/power-iaas?topic=power-iaas-deploy-custom-image) of AIX, IBM i, or Linux. IBM also provides a community-supported CentOS image under the Linux operating system. However, IBM does not provide any support for this image. For CentOS support, see the [CentOS forum](https://forums.centos.org/){: external} or [FAQ](https://wiki.centos.org/FAQ.html){: external}  page. {{site.data.keyword.powerSys_notm}} now supports Linux (RHEL and SLES) stock images for non-SAP applications. \n To provision {{site.data.keyword.powerSys_notm}} instance that supports SAP HANA and SAP NetWeaver applications, see [Provisioning your {{site.data.keyword.powerSysFull}}](https://cloud.ibm.com/docs/sap?topic=sap-power-vs-planning-items){: external}. \n **Important:** When you use an AIX stock image as the boot volume, a console session is required for the initial setting of the root user password. Without completing this step, SSH login as root appears as being *disabled*. \n For IBM i operating system licensing information, see [IBM i License Program Products (LPP) and Operating System (OS) feature bundles](/docs/power-iaas?topic=power-iaas-ibmi-lpps). |
| Attached volumes | You can either create a new data volume or attach an existing one that you defined in your account. \n **Create volume**: Click **Create volume** to create a new data volume for your {{site.data.keyword.powerSys_notm}} instance. If you want to allow multiple virtual instances to write data to the same data volume, you must click **On** under **Shareable**. \n **Attached Volume**: You can select an existing data volume from the **Attached volumes** list. If a previously used data volume does not appear, it might exist under a different account or resource instance. |
| Public Networks | Select this option to use an IBM-provided public network. There is a cost that is associated with selecting this option. \n [Learn more](/docs/power-iaas?topic=power-iaas-on-cloud-architecture#public-private-networks) |
| Private Networks | Click **Add** to identify a new private network for the virtual server. If you already added a private network, you can select it from the list. For more information, see [Configure a private network subnet](/docs/power-iaas?topic=power-iaas-configuring-subnet).|
{: caption="{{site.data.keyword.powerSys_notm}} instance fields" caption-side="bottom"}

## Reusing Volume names or VM names in {{site.data.keyword.powerSys_notm}}
{: #reusing_volume_names}

You can deploy a {{site.data.keyword.powerSys_notm}} VM by specifying any name. If you want to delete that VM and deploy a new VM with the same name, you must allow 1 hour between deleting the original instance and creating a VM by using the same name again.

For example, you create a VM with the name TEST-VM and you delete this VM later. The name "TEST-VM" is not immediately available for reuse. Before you attempt to use the name TEST-VM again, you must allow 1 hour to pass after the VM was deleted.


## Implementing SAP NetWeaver and SAP HANA in the {{site.data.keyword.powerSys_notm}} environment
{: #sap_netweaver_hana}

You can deploy SAP NetWeaver on an AIX or Linux&reg; operating system, and SAP HANA on Linux operating system, in your {{site.data.keyword.powerSys_notm}} environment. You must consider several SAP-specific infrastructure requirements to run SAP applications on {{site.data.keyword.powerSys_notm}}s. For more information, see [Planning your deployment](https://cloud.ibm.com/docs/sap?topic=sap-power-vs-planning-items){: external} and [Deploying your infrastructure](https://cloud.ibm.com/docs/sap?topic=sap-power-vs-set-up-power-infrastructure){: external}.

On IBM Power server E980 that is running in a multiple VM environment with at least one SAP HANA production system, you can deploy up to sixteen VMs per physical server with dedicated or dedicated-donating processor cores. Each concurrently running VM instance must be configured according to the workload and must fulfill the SAP HANA Hardware Configuration Check Tool (HWCCT) key performance indicators (KPIs). You must also consider the minimum number of CPU cores and memory size of VMs as described in SAP Note 2188482. For more information see, [SAP support Launchpad](https://launchpad.support.sap.com/#/notes/2230704){: external}. You must have an SAP ID to access this web page.

## Configuring a VM for Epic workloads
{: #configuring-a-vm-for-epic-workloads}

You can configure your virtual machine (VM) instance to deploy Epic workloads when you select AIX as your operating system.

To configure a VM instance for Epic workloads, select the **Configure for Epic workloads** checkbox on the **Boot image** tile. You can verify whether the deployed VM supports Epic workloads by checking the corresponding VM details page. On the VM details page, the **Deployment type** field must be set to **Epic**.

In the VM details page, for the VMs on which Epic workloads are supported, you must not create or attach volumes from Tier 3 to avoid performance issues.  For the VMs on which Epic workloads are supported and are in shut-down state, you must not change the core type to any value other than `dedicated` to avoid performance issues.
{: important}

The following table explains the differences in VM configuration that may or might not support Epic workloads:

|VM deployed for|Storage volume|Core type|Machine type|
|-----|------|-----|-----|
|Non-epic workloads|Tier 1 or Tier 3|Shared uncapped, \n shared capped, or \n dedicated| S922 or E980|
|Epic workloads|Always Tier 1|Always dedicated| E980 or E1080 |
{: caption="VM configuration difference that supports non-Epic and Epic workloads" caption-side="bottom"}

The epic VMs are not pinned by default that you can use internally for non-production usage. You must consider pinning the production epic VMs to avoid performance issues.
{: note}

You can choose to configure a VM for Epic workloads only when you select AIX as your operating system. The other conditions that apply are as follows:

1. Epic workloads are supported on AIX 7.2 and later. You cannot choose AIX 7.1.
2. Supported storage volume is Tier 1. You can change or attach Tier 3 storage volume. This leads to performance issues.
3. Supported machine types are E980 or E1080. You cannot select S922.
4. Supported core type is dedicated. You can switch to other core type, but it might lead to performance issues.

## Configuring affinity policies
{: #affinity-pol}

You can use the user interface to set the affinity policies for storage pools only when the total number of VMs in your account is less than 100. If your account has more than 100 VMs, then you must use the CLI or API to set the volume affinity policies.

Select one of the following Storage pool options:
- **Auto-select pool**: Use this option to allow the system to automatically select a storage pool for the storage tier with sufficient capacity.

- **Affinity**: Use this option to identify the storage pool that must be used to place the boot volumes based on an existing VM or storage volume from your account. The new storage volumes for the VM will be placed in the same storage pool where the affinity object resides. If you are using a PVM instance as the affinity object, the storage pool that is selected is based on the PMV instance's root (boot) volume.

- **Anti-affinity**: Use this option to identify one or more storage pools that you want to exclude from getting selected to place the boot volumes based on one or more existing VMs or storage volumes from your account. While choosing a storage pool to create the custom image storage volumes, the storage pools in which the list of anti-affinity objects reside will not be selected. If you are using VM as the anti-affinity objects, the storage pools are excluded depending on the root (boot) volume of each PVM instance that you specify.

To learn more about the flexible tier offering of {{site.data.keyword.powerSys_notm}}, see: [Storage tiers](/docs/power-iaas?topic=power-iaas-on-cloud-architecture#storage-tiers).

For more information about affinity and anti-affinity policy, see [What does it mean to set an affinity or anti-affinity rule?](/docs/power-iaas?topic=power-iaas-powervs-faqs#affinity).

If you add volumes to be created and attached to your new VM during creation then all the volumes are provisioned in the same selected storage pool. Volumes can be created in different storage pools after the VM has been provisioned.
{: note}



## Provisioning a virtual machine without an initial boot volume
{: #empty-vm}

Create and deploy a virtual server instance (VM) without an initial boot volume.

The VMs without boot volume can be used for cloning operations. These VMs are not bootable until a boot volume is attached post provisioning. The following table shows which images are deployed based on your OS selection:

When you attach boot volume post provisioning of VM, the boot image still shows the OS specific image without boot volume name. 
{: note}

| OS selected | Image deployed                  |
|-------------|---------------------------------|
| AIX         |  AIX (Empty image) image without boot volume             |
| IBM i       |  IBM i (Empty image) image without boot volume           |
| Linux       |  You must select one of the following images: \n * Linux - SUSE (Empty image) \n * Linux - RedHat Enterprise (Empty image) image without boot volume       |
| Linux for SAP (HANA)| Provision of VM without boot volume is not supported|
| Linux for SAP (NetWeaver)| Provision of VM without boot volume is not supported|
| Client supplied subscriptions | Provision of VM without boot volume is not supported for these OSs |
{: caption="Provision of VMs without boot volume based on the OS selection." caption-side="top"}

When you select the **Deploy empty virtual server instance** checkbox, you can provision a VM without a boot image and boot volume. Review the following table to understand how the selection of the **Deploy empty virtual server instance** checkbox works along with the provisioning of the large quantity of data volumes:

| Features | 'Deploy empty virtual server instance' checkbox is clear | 'Deploy empty virtual server instance' checkbox is selected |
|----------|-------------------------------------------------------|-------------------------------------------------------------|
| Boot image and volume	| Provision a VM with a boot image and boot volume	| Provision a VM without a boot image and boot volume.
| Creating new volume during VM provisioning | Create up to 10 volumes from the VM provisioning page. To create volumes in bulk, use the [Storage volumes](https://cloud.ibm.com/power/storage) page in the {{site.data.keyword.powerSys_notm}} user interface.	| You cannot create any volumes and attach to the VM during initial provisioning. You can create up to 10 volumes after provisioning. |
| Attaching existing volume during VM provisioning | Attach up to 500 existing data volumes	| You cannot attach any volumes to the VM during initial provisioning. You can attach one boot volume and up to 500 data volumes after provisioning. |
| Attaching from multiple storage tiers	| Supported. But if multiple storage tier volumes are used, there is a potential risk of failure of clone operation. | Supported. But if multiple storage tier volumes are used, there is a potential risk of failure of clone operation. |
| Boot volume | Boot volume is attached while provisioning. Click three dots on any data volume and set it as the boot volume. However, you cannot set shareable volumes as boot volumes. | 	Boot volume is attached after provisioning. Click three dots on any data volume and set it as the boot volume. However, you cannot set shareable volumes as boot volumes. |
{: caption="Provisioning a VM with or without a boot volume." caption-side="top"}


## Configuring large quantity of data volumes on Off-premises
{: #config-large-vol}

[Off-premises]{: tag-blue}

You can configure your virtual server instance (VM) while provisioning to enable it to attach or detach more than 127 (up to 500) data volumes from the user interface.













IBM i virtual machines in all the data centers support the configuration of large quanitity of data volumes except for the virtual machines in the `CHE01`, `LON06`, `MAD04`, and `TOR01` data centers. Configuring the large quantity of data volumes is supported only on Off-premises.
{: note}



### Limitations of large quantity volumes
{: #limit-large-vols}

Review the following limitations when you are configuring for large quantity of volumes:
- It is recommended to perform the operations, such as deploy, attach, detach, or delete, in a sequential order to avoid any performance delays.

- It is recommended to use image catalog to capture the virtual machines with large quantity volumes. Using Cloud Object Storage (COS) or any other cloud option might result in delays. The delay is depending on the size of your volume and network speed.

- When you attach large quantity of volumes in a single request, displaying the status value from `available` to `attaching` might be delayed. It is recommended to wait for the `attach` operation to be completed and then select the attached volumes for other operations.

- Provisioning an IBM i VM with small data volumes (even fewer than 10 volumes in some cases) can cause a 3-5 hour delay if bulk-volume operations are ongoing on the storage controller. During this delay, the VM remains in the building state and cannot be modified.

- When a bulk delete operation is in progress on a storage controller, provisioning an IBM i virtual machine, even with fewer data volumes, might get delayed. During provisioning, the virtual machine status continues to be in the `building` state and this status cannot be modified.
