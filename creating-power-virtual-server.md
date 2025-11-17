---
copyright:
  years: 2019, 2025

lastupdated: "2025-11-17"

keywords: getting started, {{site.data.keyword.powerSys_notm}}, configure instance, processor, profile, networking, large volumes, ibm i 500 volume, boot vm, epic

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Creating an IBM {{site.data.keyword.powerSys_notm}}
{: #creating-power-virtual-server}
{: help}
{: support}

---

{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}


---

To create and configure an {{site.data.keyword.powerSysFull}}, complete the following steps.
{: shortdesc}


## Creating a {{site.data.keyword.powerSys_notm}} workspace
{: #creating-service}

1. Log in to the [IBM Cloud catalog](https://cloud.ibm.com/catalog){: external} with your credentials.
2. In the search box, type **{{site.data.keyword.powerSys_notm}}** and click the **{{site.data.keyword.powerSys_notm}}** tile.
3. Click **Create a workspace**.
4. Select **Location type** as {{site.data.keyword.on-prem}} or {{site.data.keyword.off-prem}}.

   For {{site.data.keyword.on-prem}} location types, select the name of the created satellite location from the **Satellite Location** list.

   For {{site.data.keyword.off-prem}} location types, select the IBM Cloud region that is closest to your physical location from the **Satellite Location** list. For the list of available IBM Cloud regions, see [IBM Cloud regions](/docs/power-iaas?topic=power-iaas-ibm-cloud-reg).

5. In the **Details** section, provide a name for the workspace and select the resource groups.
6. Click **Continue**. The selected workspace details are displayed on the Summary page.
   Review the estimated cost on the Summary page.
7. Select **I agree to the Terms and conditions** checkbox.
8. Click **Create**. You are redirected to the **Workspaces** page where you can select an existing workspace.


For more information about appropriate region for your workspace, see [IBM Cloud regions](/docs/power-iaas?topic=power-iaas-ibm-cloud-reg).




{{_include-segments/workspace-note.md}}



## Configuring a {{site.data.keyword.powerSys_notm}} instance
{: #configuring-instance}

To create a virtual server instance, you must first create a [{{site.data.keyword.powerSys_notm}} workspace](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#creating-service) and select a workspace. The created workspaces are listed under **Workspaces** of the {{site.data.keyword.powerSys_notm}} user interface in the navigation panel. Select the workspace for which you want to create an instance. Complete the following steps to create a virtual machine instance:

1. Click **Virtual server instances** in the navigation panel.

    Select a workspace to display the virtual server instances that were provisioned. You must refresh the page to see the updated information if you see outdated information. For more information, see the FAQ page [What should I do when I do not see the latest information in the UI](/docs/power-iaas?topic=power-iaas-powervs-faqs#ui-not-updated).
    {: important}

    The virtual server instances that are associated with the selected workspace are displayed.

    [{{site.data.keyword.on-prem}}]{: tag-red} If an error occurs immediately after you create or open the virtual server instance, you must delete it.
    {: note}

2. To create a new instance, click **Create instance**.

    If you select more than one instance under **Number of instances**, additional options are displayed.

    The total due per month is dynamically updated in the **Order Summary** based on your selections. You can easily create a cost-effective {{site.data.keyword.powerSys_notm}} instance that satisfies your business needs.
    {: tip}

    

3. Choose an existing SSH key or create one to securely connect to your {{site.data.keyword.powerSys_notm}}.

4. Complete the **Boot image** fields.

    You can create or provision a virtual server instance (VSI) without any initial boot image volume. VSIs without boot volume are helpful in [high availability and disaster recovery](/docs/power-iaas?topic=power-iaas-ha-dr) use cases. A VSI can be created without a boot volume and the volume that is cloned or replicated can be attached to a VSI to bring the backed-up VSI.

    Select the **Deploy empty virtual server instance** checkbox to provision a VSI without a boot volume. For more information, see [Provisioning a virtual machine without an initial boot volume](#empty-vm).

    

    

    You can create a VSI without a boot volume for the AIX, IBM i, and Linux operating systems with an IBM provided subscription. If a Virtual serial number (VSN) is assigned to a VSI without storage, you must assign the VSN before you attach the boot volume and start the VSI.
    {: important}

    

    You can set the affinity policies for storage pools. For more information, see [Configuring affinity policies](#affinity-pol).

    When you select **Boot image**, the {{site.data.keyword.powerSys_notm}} user interface allows you to select the boot images from a set of available stock images or from a custom image in your image catalog. Custom images are images that you can import from IBM Cloud Object Storage or create from a VSI capture. When you select a stock image, you must also select the storage tier and the storage pool. When you select a custom image, the new VSIs are deployed into the same storage tier and pool where the image resides. You must select a storage type for stock images. Currently, you cannot mix **Tier 1** and **Tier 3** storage types. For more information, see [Storage tiers](/docs/power-iaas?topic=power-iaas-on-cloud-architecture#storage-tiers).

    [{{site.data.keyword.on-prem}}]{: tag-red} If you select a custom image from a local catalog, the VSIs are deployed on a single storage tier.
    {: note}

    If you select AIX as the boot image, the {{site.data.keyword.powerSys_notm}} user interface provides you with an option to configure the VSI for epic workload. For more information on epic, see [configuring a VSI for EPIC workloads](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#configuring-a-vm-for-epic-workloads).

    

    If you select IBM i as the boot image, the {{site.data.keyword.powerSys_notm}} user interface provides you with the following options:
    - Include the following licenses to your VSI:
      - IBM i Cloud Storage Solution
      - IBM i Power HA, and
      - Rational Dev Studio for IBM i.

        Adding a license increases the service cost. The selected licenses are injected to your VSI. You can install specific solutions on your VSI, and the licenses are automatically set. If you want to use these licensed programs on your IBM i VSI, you must order these licenses through {{site.data.keyword.powerSys_notm}}. You cannot use existing licenses in your VSI.

    - Select the {{site.data.keyword.ibmi-vst}} from the **{{site.data.keyword.ibmi-vst}}** list. To select an {{site.data.keyword.ibmi-vst}}, you must select an image with OS version 7.3 or later from the **Boot image** field and set the **Virtual serial number (VSN)** as assigned.

    

    If you select Full Linux Subscription (FLS) images, the {{site.data.keyword.powerSys_notm}} user interface provides you with an option to pass in user data or scripts during the first boot runtime. When you end the user data for the Linux images, you must complete the validation checks that are in place. No validation checks are done for AIX and bring your own license images. For more information, see [Passing user-defined scripts](/docs/power-iaas?topic=power-iaas-set-full-Linux#cloud-init-fls).

    Cloud Optical Repository (COR) is a virtual image that can be deployed and used as a Network File Server (NFS) to perform various IBM i tasks that require media. This virtual optical image includes a collection of the media necessary for various IBM i tasks, for all supported IBM i releases. With the COR image deployed, a second {{site.data.keyword.powerSys_notm}} Instance can be deployed on the same VLAN that is set up as the client and pointed to the COR (target) NFS Server Instance. For more information on COR images, see [Cloud Optical Repository](https://cloud.ibm.com/media/docs/downloads/power-iaas/Cloud_Optical_Repository.pdf){: external}.


    

    To deploy an SAP workload, from the **Operating system** list select one of the following options:

    - Select **Linux for SAP (HANA)** in the IBM provided subscription section to use the IBM provided Linux subscription.
    - Select **Linux for SAP (HANA)** in the Client supplied subscription section to use your own license.

    To deploy an SAP certified profile from the **Standard RISE** or **Application server** tabs, set **SAP RISE deployment** to on in the Advance Configuration section. The **SAP RISE deployment** option is enabled only if you select the OS as **Linux for SAP (HANA)** and the machine type is IBM Power10 or later.

    

5. Complete the **Profile** fields by selecting the **Machine type**, the number of **Cores**, the amount of **Memory (GB)** and **Core type**.

    The core-to-virtual core ratio is 1:1. For shared processors, fractional cores round-up to the nearest whole number. For example, 1.25 cores are equal to 2 virtual cores. For more information about processor types, see [What's the difference between shared capped and shared uncapped processor performance? How do they compare to dedicated processor performance?](/docs/power-iaas?topic=power-iaas-powervs-faqs#processor). If the machine type is S922 and the operating system is IBM i, IBM i supports a maximum of 4 cores per VSI.
    {: important}

    When you use an AIX stock image as the boot volume, a console session is required for the initial setting of the root user password. Without completing this step, SSH login appears as disabled. For more information, see [How to create a new AIX VSI with SSH keys for root login](/docs/power-iaas?topic=power-iaas-create-vm).

    

    You must complete the following prerequisites to assign an {{site.data.keyword.ibmi-vst}} to a {{site.data.keyword.powerSys_notm}} instance:

   - Select an IBM i image with version 7.3 or later from the **Image** list under the **Boot image** section.
   - Select an IBM Power10 or later server type from the **Machine type** list.
   - Complete the following steps to assign a VSN to the instance:
     - Edit the **Virtual serial number (VSN)** field.
     - The Virtual serial number (VSN) summary pane appears.
     - Select either **Auto-assign** or **Select from retained VSNs** option to assign a VSN.

    The supported {{site.data.keyword.ibmi-vst}}s are displayed in the **{{site.data.keyword.ibmi-vst}}** list based on the machine type that you select. The recommended {{site.data.keyword.ibmi-vst}} is displayed in the **{{site.data.keyword.ibmi-vst}}** field based on the number of cores and the memory size. You can select the {{site.data.keyword.ibmi-vst}} that is displayed in the **{{site.data.keyword.ibmi-vst}}** field or other options from the list.

    

    
    To deploy an SAP workload, complete the following steps:

    1. Select a **Machine type** from the list.
       - To deploy an SAP HANA profile, you can select a machine type from the list.
       - To deploy an SAP certified profile, you must select an IBM Power10 or later machine type from the list.
    2. Select a profile to deploy an SAP HANA profile.

    3. Select a profile from the **Standard RISE** or **Application Server** tab to deploy an SAP certified profile. The tabs are enabled if you set **SAP RISE deployment** to on in the Advance Configuration section.

    The **SAP RISE deployment** option is enabled if **Linux for SAP (HANA)** from the Operating system list and IBM Power10 or later from the Machine type list are selected.

    

    

    You cannot create or attach volumes larger than 2047 GB on IBM i-based VSIs. However, machine types E890 and E1080 are optimized to support the attachment of a higher number of volumes on IBM i-based VSIs. For more information, see [Configuring for large quantity of volumes](#config-large-vol).
    {: note}

    


8.  Define your **Network interfaces** by adding a public network, private network, or both. When you add an existing private network, you can choose a specific IP address or have one auto-assigned.

    When you choose to provide a specific IP address, ensure that the IP address is not listed under [reserved IP](/docs/power-iaas?topic=power-iaas-configuring-subnet#reserv-ip).
    {: important}

    For an AIX VM, network interface controllers (NICs) are assigned based on the order in which you specify them during creation. To display the information about all the network interfaces after provisioning, open the AIX console and type `ifconfig -a`.
    {: note}

9.  Accept the **Terms of Use** and click **Create instance** to provision a new {{site.data.keyword.powerSys_notm}}. To view your boot images, go to **Boot images** after you provision the instance.

    If your account has fewer than 100 VSIs, you can use the {{site.data.keyword.powerSys_notm}} user interface to view the VSIs. If your account has more than 100 VSIs, the VSIs might not be displayed in the user interface. You can reduce the number of VSIs by using the CLI or API so that they are displayed again on the user interface.
    {: note}




## About Virtual Serial Number in {{site.data.keyword.off-prem}}
{: #vsn}

You can assign a Virtual Serial Number (VSN) to a VSI.

VSN is supported only on a VSI with IBM i operating system.
{: note}




VSN has the following characteristics:

* It has seven digits and is a unique string.
* It is used for licensing and tracking the usage of the VSI.
* It can be associated with only one VSI.
* It can be assigned to a new or an existing VSI.
* It can be assigned to an empty virtual server instance in [{{site.data.keyword.off-prem}}]{: tag-blue}. 

For more information, see [Assigning the virtual serial number to a logical partition](https://www.ibm.com/docs/en/power10/9080-HEX?topic=9080-HEX/p10hat/p10hat_pvsn.html){: external}.

A VSI is moved across systems with its associated VSN. Hence, when a VSN is associated with a VSI you need not pin the VSI to a host for licensing or entitlement purpose.




VSN is a unique identifier and can be assigned only to one VSI at a time. If you simultaneously deploy more than one VSI assigning the same VSN, only one of the VSIs gets the VSN, and the others are deployed without the VSN being assigned.
{: important}



View the details of a VSN associated with a VSI on the VSI details page. You can also view the details of the VSNs associated with the VSIs for the workspace on the Virtual serial numbers page. The VSNs are either in `assigned` or in `retained` state.


### Mapping the customer account number to the cloud account ID
{: #VSN-id-map}

For VSN support in the IBM {{site.data.keyword.powerSys_notm}}, you must open a support ticket to map your IBM customer number with your IBM Cloud account ID. For more information, see [Assigning a Virtual Serial Number to an IBM customer number in IBM Power Virtual Server](https://www.ibm.com/docs/en/entitled-systems-support?topic=mp-cloud-power-virtual-server-using-virtual-serial-numbers-customer-numbers){: external}.

### Assigning a VSN to a new VM
{: #VSN-new-VM}

You can assign a VSN only to a VSI with IBM i OS. To assign a VSN when you create a VM, select **IBM i** OS. The **Virtual serial number** field is enabled. The default VSN value is **None**.

Edit the default VSN value and select one of the following options:

- **Auto-assign**: Assigns a system-generated VSN to your VSI only if your `IBM Cloud account ID` is mapped with your `customer number` in the Entitled System Support (ESS).
- **Select from retained VSNs**: Displays a list of the retained VSNs. You can select a VSN in the `retained` state and assign it to your IBM i VSI.

For more information about creating a VM, see [Configuring a {{site.data.keyword.powerSys_notm}} instance](#configuring-instance).









### Assigning a VSN to an existing VSI
{: #VSN-existing-VM}

To assign a VSN for an existing IBM i VSI, complete the following steps:

1. Shut down the IBM i VSI that you plan to assign the VSN.
2. Open the VSI to access the **Virtual server instance details** page.
3. Edit the **Virtual serial number** field.
4. From the **VSN assignment** list, select one of the following options:
    - **None**: Does not assign a VSN to the VSI.
    - **Auto-assign**: Assigns a system-generated VSN to the VSI.
    - **Select from retained VSNs**: Displays the list of retained VSNs that can be selected.
5. Click **Save**.
6. Power on the VSI.









### Releasing or retaining a VSN
{: #VSN-rel-del}



When you delete a VSI, you can either retain the VSN or release it. When you edit the VSI details to change the VSN, you can retain the existing VSN or release it. To release or retain a VSN, complete the following steps:

1. Delete a VSI by clicking the delete icon from the Virtual server instance details page. The Delete virtual server instance window is displayed.
2. Edit the details of a VSI by clicking the overflow menu (icon with 3 vertical dots) on the far right of the VSI entry from the Virtual server instance details page. The Edit virtual server instance window is displayed.
3. Set **Release the VSN attached to the VM** to `Enable` or `Disable` on the page to release or retain the VSN:
    - `Enable`: (Default) Deletes the VSI and attaches the VSN to the VSI that is released and no longer associated with your account. By default, the **Release the VSN attached to the VM** is enabled.
    - `Disable`: Deletes only the VSI and retains the VSN that continues to be associated with your account. The retained VSN is moved to the retained VSN pool.






The following table provides more information about each {{site.data.keyword.powerSys_notm}} instance field.

| Field | Description |
|----------|---------|
| General | **Instance name**: Specify a name for your virtual server instance.  \n **Number of Instances** : Specify the number of instances that you want to create for the {{site.data.keyword.powerSys_notm}}. You can apply placement groups only when you are creating a single VSI. If you choose the Machine type as E980, you can choose an [anti-affinity policy](/docs/power-iaas?topic=power-iaas-powervs-faqs#affinity) with maximum of 2 VSIs.  \n **Placement group**: If you are creating only one instance, you can choose the placement group to control the selection of the host to host the instance. Select a placement group from the list. To create a new placement group, select one of the following options:  \n Same server : Select this option to place the VSI on the same host.  \n Different servers : Select this option to place the VSI on a different host.  \n **Colocation rules**: If you specify more than one instance, you can select the following naming conventions and colo rules:  \n **No preference**: Select this option if you do not have a hosting preference.  \n **Same server** : Select this option to host all instances on the same server. A placement group is automatically created. The instance name that is previously provided is used as the group name and cannot be edited.  \n **Different server** :  Select this option to host each instance on a different server. You can use this option if you are concerned about a single-server outage that might affect all {{site.data.keyword.powerSys_notm}} instances. A placement group is automatically created. The instance name that is previously provided is used as the group name and cannot be edited.  \n **Numerical prefix** : Select this option to add numbers before the name of the virtual server. If, for example, the first {{site.data.keyword.powerSys_notm}} name is *Austin* the next name for the virtual instance is *1Austin*.  \n **Numerical postfix** : Select this option to add numbers after the name of the virtual server. If, for example, the first {{site.data.keyword.powerSys_notm}} name is *Austin* the next name for the virtual instance is *Austin 1*.  \n **Virtual server pinning** : Select this option to pin your VSI. You can choose either a *soft* or *hard* pinning policy.  \n [Learn more](/docs/power-iaas?topic=power-iaas-powervs-faqs#pinning).  \n **Note:** When you create multiple instances of the virtual server, you must select **On** from the **Shareable** field for each data volume that you add. If you do not want the data volume to be shareable, you can add the data volume after you create the virtual server. For IBM i OS, you cannot have shareable data volumes.|
| Machine type | Specify the machine type. The machine type that you select determines the number of cores and memory that is available. For more information about hardware specifications, see [S922](https://www.ibm.com/downloads/cas/KQ4BOJ3N){: external} and [E980 (Data centers other than Dallas and Washington)](http://www-01.ibm.com/support/docview.wss?uid=ssm1platformaix9080-M9S-vios-only){: external}. |
| Cores | The core-to-virtual core ratio is 1:1. For shared processors, fractional cores round-up to the nearest whole number. For example, 1.25 cores are equal to 2 virtual cores. |
| Memory | Select the amount of memory for the {{site.data.keyword.powerSys_notm}}. If you choose to use more than 64 GBs of memory per core, you are charged a higher price. For example, when you choose one core with 128 GBs of memory, you are charged the regular price for the first 64 GBs. After the first 64 GBs (64 - 128 GBs), you are charged a higher price. |
| Boot image | Select a version of the IBM-provided AIX or IBM i operating system stock image. You can also select Linux stock images for SAP HANA and SAP NetWeaver applications. For the SAP stock images, it is mandatory to set an SSH key when you create the VSI. You will be able to access the VSI only via SSH after launch. However, it is recommended to set a password by using the `passwd` command during the first SSH access. By setting a password, you are able to access the instance in the UI console. You can also [deploy your own custom image](/docs/power-iaas?topic=power-iaas-deploy-custom-image) of AIX, IBM i, or Linux. IBM also provides a community-supported CentOS image under the Linux operating system. However, IBM does not provide any support for this image. For CentOS support, see the [CentOS forum](https://forums.centos.org/){: external} or [FAQ](https://wiki.centos.org/FAQ.html){: external} page. {{site.data.keyword.powerSys_notm}} now supports Linux (RHEL and SLES) stock images for non-SAP applications.  \n  To provision {{site.data.keyword.powerSys_notm}} instance that supports SAP HANA and SAP NetWeaver applications, see [Provisioning your {{site.data.keyword.powerSysFull}}](https://cloud.ibm.com/docs/sap?topic=sap-power-vs-planning-items){: external}.  \n  **Important:** When you use an AIX stock image as the boot volume, a console session is required for the initial setting of the root user password. Without completing this step, SSH login as root appears as being *disabled*.  \n  For IBM i operating system licensing information, see [IBM i License Program Products (LPP) and Operating System (OS) feature bundles](/docs/power-iaas?topic=power-iaas-ibmi-lpps). |
| Attached volumes | You can either create a new data volume or attach an existing one that you defined in your account.  \n **Create volume**: Click **Create volume** to create a new data volume for your {{site.data.keyword.powerSys_notm}} instance. If you want to allow multiple virtual instances to write data to the same data volume, you must click **On** under **Shareable**.  \n **Attached Volume**: You can select an existing data volume from the **Attached volumes** list. If a previously used data volume does not appear, it might exist under a different account or resource instance. |
| Public Networks | Select this option to use an IBM-provided public network. Cost is associated when you select this option.  \n [Learn more](/docs/power-iaas?topic=power-iaas-on-cloud-architecture#public-private-networks) |
| Private Networks | Click **Add** to identify a new private network for the virtual server. If you already added a private network, you can select it from the list. For more information, see [Configure a private network subnet](/docs/power-iaas?topic=power-iaas-configuring-subnet).|
{: caption="{{site.data.keyword.powerSys_notm}} instance fields" caption-side="bottom"}






## Reusing Volume names or VSI names in {{site.data.keyword.powerSys_notm}}
{: #reusing_volume_names}



You can deploy a {{site.data.keyword.powerSys_notm}} VSI by specifying any name. To delete a VSI and to deploy a new VSI with the same name, you must allow up to 1 hour between deleting the original instance and creating a VSI with the same name.



For example, you create a VSI with the name TEST-VSI and you delete this VSI later. The name "TEST-VSI" is not immediately available for reuse. Before you attempt to use the name TEST-VSI again, you must allow 1 hour to pass after the VSI was deleted.


## Implementing SAP NetWeaver and SAP HANA in the {{site.data.keyword.powerSys_notm}} environment
{: #sap_netweaver_hana}

You can deploy SAP NetWeaver on an AIX or Linux&reg; operating system, and SAP HANA on Linux operating system, in your {{site.data.keyword.powerSys_notm}} environment. You must consider several SAP-specific infrastructure requirements to run SAP applications on {{site.data.keyword.powerSys_notm}}s. For more information, see [Planning your deployment](https://cloud.ibm.com/docs/sap?topic=sap-power-vs-planning-items){: external} and [Deploying your infrastructure](https://cloud.ibm.com/docs/sap?topic=sap-power-vs-set-up-power-infrastructure){: external}.

Consider an IBM Power server E980 that is running in a multiple VSI environment with at least one SAP HANA production system. You can deploy up to sixteen VSIs per physical server with dedicated or dedicated-donating processor cores. Each concurrently running VSI must be configured according to the workload and must fulfill the SAP HANA Hardware Configuration Check Tool (HWCCT) key performance indicators (KPIs). You must also consider the minimum number of CPU cores and memory size of VSIs as described in SAP Note 2188482. For more information see, [SAP support Launchpad](https://launchpad.support.sap.com/#/notes/2230704){: external}. You must have an SAP ID to access this web page.

## Configuring a VSI for Epic workloads
{: #configuring-a-vm-for-epic-workloads}

You can configure your VSI to deploy Epic workloads when you select AIX as your operating system.

To configure a VSI for Epic workloads, select the **Configure for Epic workloads** checkbox on the **Boot image** tile. You can verify whether the deployed VSI supports Epic workloads by checking the corresponding VSI details page. On the VSI details page, the **Deployment type** field must be set to **Epic**.

In the VSI details page, for the VSIs on which Epic workloads are supported, you must not create or attach volumes from Tier 3 to avoid performance issues. For the VSIs on which Epic workloads are supported and are in a shut-down state, you must not change the core type to any value other than `dedicated` to avoid performance issues.
{: important}

The following table explains the differences in VSI configuration that may or might not support Epic workloads:

|VSI deployed for|Storage volume|Core type|Machine type|
|-----|------|-----|-----|
|Non-epic workloads|Tier 1 or Tier 3|Shared uncapped,  \n shared capped, or  \n dedicated| S922 or E980|
|Epic workloads|Always Tier 1|Always dedicated| E980 or E1080 |
{: caption="VSI configuration difference that supports non-Epic and Epic workloads" caption-side="bottom"}

The epic VSIs are not pinned by default that you can use internally for non-production usage. You must consider pinning the production epic VSIs to avoid performance issues.
{: note}

You can choose to configure a VSI for Epic workloads only when you select AIX as your operating system. The other conditions that apply are as follows:

1. Epic workloads are supported on AIX 7.2 and later. You cannot choose AIX 7.1.
2. Supported storage volume is Tier 1. You can change or attach Tier 3 storage volume.

    Changing the Tiers leads to performance issues.
    {: note}

3. Supported machine types are E980 or E1080. You cannot select S922.
4. Supported core type is dedicated. You can switch to other core type, but it might lead to performance issues.

## Configuring affinity policies
{: #affinity-pol}

You can use the user interface to set the affinity policies for storage pools only when the total number of VSIs in your account is less than 100. If your account has more than 100 VSIs, then you must use the CLI or API to set the volume affinity policies.

Select one of the following Storage pool options:
- **Auto-select pool**: Use this option to allow the system to automatically select a storage pool for the storage tier with sufficient capacity.

- **Affinity**: Use this option to identify the storage pool that must be used to place the boot volumes based on an existing VSI or storage volume from your account. The new storage volumes for the VSI are placed in the same storage pool where the affinity object resides. If you are using a PVM instance as the affinity object, the storage pool that is selected is based on the PMV instance's root (boot) volume.

- **Anti-affinity**: Use this option to identify one or more storage pools that you want to exclude from getting selected to place the boot volumes. The boot volumes are placed based on one or more existing VSIs or storage volumes from your account. When you select a storage pool to create the custom image storage volumes, the storage pools in which the list of anti-affinity objects reside are not selected. If you are using VSI as the anti-affinity objects, the storage pools are excluded depending on the root (boot) volume of each PVM instance that you specify.

To learn more about the flexible tier offering of {{site.data.keyword.powerSys_notm}}, see: [Storage tiers](/docs/power-iaas?topic=power-iaas-on-cloud-architecture#storage-tiers).

For more information about affinity and anti-affinity policy, see [What does it mean to set an affinity or anti-affinity rule?](/docs/power-iaas?topic=power-iaas-powervs-faqs#affinity).

If you add volumes to be created and attached to your new VSI during creation then all the volumes are provisioned in the same selected storage pool. Volumes can be created in different storage pools after the VSI is provisioned.
{: note}


## Provisioning a virtual machine without an initial boot volume
{: #empty-vm}

Create and deploy a virtual server instance (VM) without an initial boot volume.

The VSIs without boot volume can be used for cloning operations. These VSIs are not bootable until a boot volume is attached post provisioning. The following table shows which images are deployed based on your OS selection:

When you attach boot volume post provisioning of the VM, the boot image still shows the OS-specific image without the boot volume name. 
{: note}

| OS selected | Image deployed                  |
|-------------|---------------------------------|
| AIX         |  AIX (Empty image) image without boot volume             |
| IBM i       |  IBM i (Empty image) image without boot volume           |
| Linux       |  You must select one of the following images:  \n * Linux - SUSE (Empty image)  \n * Linux - RedHat Enterprise (Empty image) image without boot volume       |
| Linux for SAP (HANA)| Provision of VSI without boot volume is not supported|
| Linux for SAP (NetWeaver)| Provision of VSI without boot volume is not supported|
| Client supplied subscriptions | Provision of VSI without boot volume is not supported for these OSs |
{: caption="Provision of VSIs without boot volume based on the OS selection." caption-side="top"}

When you select the **Deploy empty virtual server instance** checkbox, you can provision a VSI without a boot image and boot volume. Review the following table to understand how the selection of the **Deploy empty virtual server instance** checkbox works along with the provisioning of the large quantity of data volumes:

| Features | 'Deploy empty virtual server instance' checkbox is clear | 'Deploy empty virtual server instance' checkbox is selected |
|----------|-------------------------------------------------------|-------------------------------------------------------------|
| Boot image and volume	| Provision a VSI with a boot image and boot volume	| Provision a VSI without a boot image and boot volume.
| Creating new volume during VSI provisioning | Create up to 10 volumes from the VSI provisioning page. To create volumes in bulk, use the [Storage volumes](https://cloud.ibm.com/power/storage) page in the {{site.data.keyword.powerSys_notm}} user interface.	| You cannot create any volumes and attach to the VSI during initial provisioning. You can create up to 10 volumes after provisioning. |
| Attaching existing volume during VSI provisioning | Attach up to 500 existing data volumes	| You cannot attach any volumes to the VSI during initial provisioning. You can attach one boot volume and up to 500 data volumes after provisioning. |
| Attaching from multiple storage tiers	| Supported. But if multiple storage tier volumes are used, a potential risk of failure of clone operation can occur. | Supported. But if multiple storage tier volumes are used, a potential risk of failure of clone operation is possible. |
| Boot volume | Boot volume is attached while provisioning. Click three dots on any data volume and set it as the boot volume. However, you cannot set shareable volumes as boot volumes. | 	Boot volume is attached after provisioning. Click three dots on any data volume and set it as the boot volume. However, you cannot set shareable volumes as boot volumes. |
{: caption="Provisioning a VSI with or without a boot volume." caption-side="top"}


## Configuring large quantity of data volumes on {{site.data.keyword.off-prem}}
{: #config-large-vol}

[{{site.data.keyword.off-prem}}]{: tag-blue}

While provisioning, you can configure your virtual server instance (VM) to enable it to attach or detach more than 127 (up to 500) data volumes from the user interface.




IBM i virtual machines in all the data centers except for the virtual machines in the `CHE01` data center support the configuration of large quantity of data volumes. Configuring the large quantity of data volumes is supported only on {{site.data.keyword.off-prem}}.
{: note}




### Limitations of large quantity volumes
{: #limit-large-vols}

Review the following limitations when you are configuring for large quantity of volumes:
- It is recommended to perform the operations, such as deploy, attach, detach, or delete, in a sequential order to avoid any performance delays.

- It is recommended to use image catalog to capture the virtual machines with large quantity volumes. Using Cloud Object Storage (COS) or any other cloud option might result in delays. The delay is depending on the size of your volume and network speed.

- When you attach a large quantity of volumes in a single request, displaying the status value from `available` to `attaching` might be delayed. It is recommended to wait for the `attach` operation to be completed and then select the attached volumes for other operations.

- Provisioning an IBM i VSI with small data volumes (even fewer than 10 volumes in some cases) can cause a 3-5 hour delay if bulk-volume operations are ongoing on the storage controller. During this delay, the VSI remains in the building state and cannot be modified.

- When a bulk delete operation is in progress on a storage controller, provisioning an IBM i virtual machine, even with fewer data volumes, might get delayed. During provisioning, the virtual machine status continues to be in the `building` state and this status cannot be modified.
