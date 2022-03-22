---

copyright:
  years: 2019, 2021

lastupdated: "2021-05-07"

keywords: getting started, power systems virtual server, configure instance, processor, profile, networking

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

# Creating a Power Systems Virtual Server
{: #creating-power-virtual-server}
{: help}
{: support}

To create and configure an IBM&reg; Power Systems&trade; Virtual Server, complete the following steps.
{: shortdesc}

## Creating a Power Systems Virtual Server service
{: #creating-service}

1. Log in to the [IBM catalog](https://cloud.ibm.com/catalog){: external} with your credentials.

2. In the catalog's search box, type **Power Systems Virtual Server** and click the {{site.data.keyword.powerSys_notm}} tile.

3. Specify a name for your service and choose where you'd like to deploy your {{site.data.keyword.powerSys_notm}} instance. See the following table to select the appropriate location for your service.

    Japanese language support for IBM i is supported in OSA21, SAO01, TOK04, DAL12, FRA04, FRA05, and SYD05 data centers.
    {: note}

    | Geography | Location | Region | IBM Power infrastructure zone | Colocated IBM Cloud Classic infrastructure data center | Colocated IBM Cloud VPC infrastructure zone |
    | --------- | -------- | ------ | ----------------------------- | ----------------- | ----------------------- |
    | America | Dallas, USA | us-south | DAL12 \n us-south | DAL12 \n DAL13 | us-south-2 \n us-south-3 |
    | America | Washington DC, USA | us-east | us-east \n WDC06 | WDC04 \n WDC06 | us-east-1 \n us-east-2 |
    | America | São Paulo, Brazil | br-sao | SAO01 | SAO01 | - |
    | America | Toronto, Canada | ca-tor | TOR01 | TOR01 | - |
    | America | Montreal, Canada | ca-mon | MON01 | MON01 | - |
    | Europe | Frankfurt, Germany | eu-de | eu-de-1 \n eu-de-2 | FRA04 \n FRA05 | eu-de-2 \n eu-de-3 |
    | Europe | London, UK | eu-gb | LON04 \n LON06 | LON04 \n LON06 | eu-gb-1 \n eu-gb-3 |
    | Asia Pacific | Sydney, Australia | au-syd | SYD04 \n SYD05 | SYD04 \n SYD05 | au-syd-2 \n au-syd-3 |
    | Asia Pacific | Tokyo, Japan | jp-tok | TOK04 | TOK04 | jp-tok-2 |
    | Asia Pacific | Osaka, Japan | jp-osa | OSA21 | OSA21 | - |
    {: caption="Table 1. Power Systems Virtual Server data centers" caption-side="bottom"}

4. Click **Create**. You are redirected to the **Resource List**.

5. From the **Resource List**, select your {{site.data.keyword.powerSys_notm}} service under **Services**.

    ![The IBM Cloud Resource List](./images/power-iaas-resource-list.png "The IBM Cloud Resource List"){: caption="Figure 1. The IBM Cloud Resource List" caption-side="bottom"}

6. Click **Create instance** under **Virtual server instances**.

## Configuring a Power Systems Virtual Server instance
{: #configuring-instance}

To begin, complete all of the fields under the **Virtual servers** section. If you select more than one instance, you are presented with additional options.

The total due per month is dynamically updated in the **Order Summary** based on your selections. You can easily create a cost-effective Power Systems Virtual Server instance that satisfies your business needs.
{: tip}

![Creating a power virtual server instance](./images/console-create-virtual-instance.png "Creating a power virtual server instance"){: caption="Figure 2. Creating a Power Systems Virtual Server instance" caption-side="bottom"}

1. Choose an existing SSH key or create one to securely connect to your {{site.data.keyword.powerSys_notm}}.

2. Complete the **Boot image** fields as instructed by your organization. When you select **Boot image**, the {{site.data.keyword.powerSys_notm}} user interface allows you to select boot images from a set of available stock images or from a custom image in your image catalogue. Custom images are images that you have imported from IBM COS or created from a PVM instance (VM) capture. When you select a stock image you must also select the storage type (tier) and the storage pool selection. When you select a custom image, the new PVM instance(s) will be deployed into the same storage tier and pool where the image resides. You must select a storage type for stock images. Currently, you cannot mix **Tier 1** and **Tier 3** storage types. For more information, see [Storage tiers](/docs/power-iaas?topic=power-iaas-about-virtual-server#storage-tiers).

    If you select IBM i as the boot image, the {{site.data.keyword.powerSys_notm}} user interface provides you an option to include the following licenses to your VM instance: *IBM i Cloud Storage Solution*, *IBM i Power HA*, *IBM Db2 Web Query for i*, and *Rational Dev Studio for IBM i*. Adding a license increases the service cost. The selected licenses are injected to your VM instance. You can install specific solutions on your VM instance, and the licenses will be automatically set. If you want to use these licensed programs on your IBM i VM instance, you must order these licenses through {{site.data.keyword.powerSys_notm}}. You cannot use existing licenses in your VM instance.

    You can use the user interface to set the affinity policies for storage pools only when the total number of VMs in your account is less than 100. If your account has more than 100 VMs, then you must use the CLI or API to set the volume affinity policies.
    {: important}

    Select one of the following Storage pool options: 
    - **Auto-select pool**: Use this option to allow the system to automatically select a storage pool for the storage tier with sufficient capacity. 
  
    - **Affinity**: Use this option to identify the storage pool that must be used to place the boot volumes based on an existing PVM instance (VM) or storage volume from your account. The new storage volume(s) for the VM will be placed in the same storage pool where the affinity object resides. If you are using a PVM instance as the affinity object, the storage pool that is selected is based on the PMV instance's root (boot) volume.  
  
    - **Anti-affinity**: Use this option to identify one or more storage pools that you want to exclude from getting selected to place the boot voulmes based on one or more existing PVM instances (VMs) or storage volumes from your account. While choosing a storage pool to create the custom image storage volume(s), the storage pools in which the list of anti-affinity object(s) reside will not be selected. If you are using PVM instances as the anti-affinity objects, the storage pools are excluded depending on each PVM instance’s root (boot) volume that you specified.

    For more information about affinity and anti-affinity policy, see [What does it mean to set an affinity or anti-affinity rule?](/docs/power-iaas?topic=power-iaas-power-iaas-faqs#affinity).

    If you add volumes to be created and attached to your new VM during creation then all the volumes will be placed in the same selected storage pool. Volumes can be created in different storage pools after the VM has been provisioned.
    {: note}

3. Select your **Machine type**, the number of **Cores**, the amount of **Memory (GB)** and whether you'd like a **Dedicated processor**, **Uncapped shared processor**, or **Capped shared processor**.

    There is a core-to-vCPU ratio of 1:1. For shared processors, fractional cores round up to the nearest whole number. For example, 1.25 cores equals 2 vCPUs. For more information on processor types, see [What's the difference between capped and uncapped shared processor performance? How does they compare to dedicated processor performance?](/docs/power-iaas?topic=power-iaas-power-iaas-faqs#processor). If the machine type is S922 and operating system is IBM i, IBM i supports maximum of 4 cores per VM.
    {: important}

    ![Selecting your processor and system](./images/console-profile.png "Selecting your processor and system"){: caption="Figure 3. Selecting your processor and system" caption-side="bottom"}

    When using an AIX stock image as the boot volume, a console session is required for the initial setting of the root user password. Without completing this step, SSH login appears as being *disabled*. For more information, see [How to create a new AIX VM with SSH keys for root login](/docs/power-iaas?topic=power-iaas-create-vm).

4. Finally, define your **Network interfaces** by adding a public network, private network, or both. When adding an existing private network, you can choose a specific IP address or have one auto-assigned.

    For an AIX VM, network interface controllers (NICs) are assigned based on the order in which you specify them during creation. To display information about all of the network interfaces after provisioning, open the AIX console and type `ifconfig -a`.
    {: note}

5. Accept the **Terms of Use** and click **Create instance** to provision a new {{site.data.keyword.powerSys_notm}}. To view your boot images, go to **Boot images** after you provision the instance.

Refer to the following table for more information on each {{site.data.keyword.powerSys_notm}} instance field.

| Field | Description |
|----------|---------|
| General | **Instance name**: Specify an apt name for your virtual server instance. \n **Number of Instances** : Specify the number of instances that you want to create for the {{site.data.keyword.powerSys_notm}}. You can apply placement groups only when you are creating a single VM instance. If you choose the Machine type as E880 or E980, you can choose [anti-affinity policy](/docs/power-iaas?topic=power-iaas-power-iaas-faqs#affinity) with maximum of 2 VM instances. \n **Placement group**: If you are creating only one instance, you can choose the placement group to control on which host this instance will be hosted on. Select a placement group from the list. To create a new placement group select one of the following options: \n Same server : Select this option to place the VM on the same host. \n Different server : Select this option to place the VM on a different host.  \n **Colocation rules**: If you specify more than one instance, you can select the following naming conventions and colo rules: \n **No preference**: Select this option if you do not have a hosting preference. \n **Same server** : Select this option to host all instances on the same server. A placement group is automatically created. The instance name previously provided will be used as the group name and cannot be edited. \n **Different server** :  Select this option to host each instance on a different server. You can use this option if you are concerned about a single-server outage that might affect all {{site.data.keyword.powerSys_notm}} instances. A placement group is automatically created. The instance name previously provided will be used as the group name and cannot be edited. \n **Numerical prefix** : Select this option to add numbers before the name of the virtual server. If, for example, the first {{site.data.keyword.powerSys_notm}} name is *Austin* the next name for the virtual instance is *1Austin*. \n **Numerical postfix** : Select this option to add numbers after the name of the virtual server. If, for example, the first {{site.data.keyword.powerSys_notm}} name is *Austin* the next name for the virtual instance is *Austin1*. \n **VM pinning** : Select this option to pin your virtual machine. You can choose either a *soft* or *hard* pinning policy. \n [Learn more](/docs/power-iaas?topic=power-iaas-power-iaas-faqs#pinning). \n **Note:** When you create multiple instances of the virtual server, you must select **On** from the **Shareable** field for each data volume that you add. If you do not want the data volume to be shareable, you can add the data volume after you create the virtual server. For IBM i OS you cannot have shareable data volumes.|
| Machine type | Specify the machine type. The machine type that you select determines the number of cores and memory that is available. For more information about hardware specifications, see [E880 (Dallas only)](https://www-01.ibm.com/common/ssi/ShowDoc.wss?docURL=/common/ssi/rep_sm/5/872/ENUS9119-_h05/index.html&lang=en){: external}, [S922](https://www.ibm.com/downloads/cas/KQ4BOJ3N){: external}, and [E980 (Data centers other than Dallas and Washington)](http://www-01.ibm.com/support/docview.wss?uid=ssm1platformaix9080-M9S-vios-only){: external}. |
| Cores | There is a core-to-vCPU ratio of 1:1. For shared processors, fractional cores round up to the nearest whole number. For example, 1.25 cores equals 2 vCPUs. |
| Memory | Select the amount of memory for the {{site.data.keyword.powerSys_notm}}. If you choose to use more than 64 GBs of memory per core, you are charged a higher price. For example, when you choose one core with 128 GBs of memory, you are charged the regular price for the first 64 GBs. After the first 64 GBs (64 - 128 GBs), you are charged a higher price. |
| Boot image | Select a version of the IBM-provided AIX or IBM i operating system stock image. You can also select Linux stock images for SAP HANA and SAP NetWeaver applications. For these SAP stock images it is mandatory to set an SSH key while creating the VM. You will be able to access the VM instance only via SSH after launch. However, it is recommended to set a password by using the `passwd` command during the first SSH access. By setting a password, you are able to access the instance in the UI console. You can also [deploy your own custom image](/docs/power-iaas?topic=power-iaas-deploy-custom-image) of AIX, IBM i, or Linux. IBM also provides a community supported CentOS image under Linux operating system. However, IBM does not provide any support for this image. For CentOS support, see the [CentOS forum](https://forums.centos.org/){: external} or [FAQ](https://forums.centos.org/app.php/help/faq){: external} page. \n To provision Power Systems Virtual Server instance that supports SAP HANA and SAP NetWeaver applications, see [Provisioning your IBM Power Virtual Server](/docs/sap?topic=sap-power-vs-set-up-infrastructure#power-vs-provision-server). \n **Important:** When you use an AIX stock image as the boot volume, a console session is required for the initial setting of the root user password. Without completing this step, SSH login as root appears as being *disabled*. \n For IBM i operating system licensing information, see [IBM i License Program Products (LPP) and Operating System (OS) feature bundles](/docs/power-iaas?topic=power-iaas-ibmi-lpps). |
| Attached volumes | You can either create a new data volume or attach an existing one that you defined in your account. \n **Create volume**: Click **Create volume** to create a new data volume for your {{site.data.keyword.powerSys_notm}} instance. If you want to allow multiple virtual instances to write data to the same data volume, you must click **On** under **Shareable**. \n **Attached Volume**: You can select an existing data volume from the **Attached volumes** list. If a previously used data volume does not appear, it might exist under a different account or resource instance. |
| Public Networks | Select this option to use an IBM-provided public network. There is a cost that is associated with selecting this option. \n [Learn more](/docs/power-iaas?topic=power-iaas-about-virtual-server#public-private-networks) |
| Private Networks | Click **Add** to identify a new private network for the virtual server. If you already added a private network, you can select it from the list. For more information, see [Configure private network](/docs/power-iaas?topic=power-iaas-configuring-subnet).|
{: caption="Table 2. Power Systems Virtual Server instance fields" caption-side="bottom"}

## Reusing Volume names or VM names in Power System Virtual Servers
{: #reusing_volume_names}

You can deploy a Power System Virtual Server VM by specifying any name. If you want to delete that VM and deploy a new VM with the same name, you must allow 1 hour between deleting the original instance and creating a VM by using the same name again.

For example, you create a VM with the name TEST-VM and you delete this VM later. The name "TEST-VM" is not immediately available for reuse. Before you attempt to use the name TEST-VM again, you must allow 1 hour to pass after the VM was deleted.


## Implementing SAP NetWeaver and SAP HANA in the Power Systems Virtual Server environment
{: #sap_netweaver_hana}

You can deploy SAP NetWeaver on an AIX or Linux&reg; operating system, and SAP HANA on Linux operating system, in your {{site.data.keyword.powerSys_notm}} environment. You must consider several SAP-specific infrastructure requirements to run SAP applications on {{site.data.keyword.powerSys_notm}}s. For more information, see [Planning your deployment](https://cloud.ibm.com/docs/sap?topic=sap-power-vs-planning-items) and [Deploying your infrastructure](https://cloud.ibm.com/docs/sap?topic=sap-power-vs-set-up-infrastructure).

On IBM Power Systems E950 and E980 that are running in a multiple VM environment with at least one SAP HANA production system, you can deploy up to sixteen VMs per physical server with dedicated or dedicated-donating processor cores. Each concurrently running VM instance must be configured according to the workload and must fulfill the SAP HANA Hardware Configuration Check Tool (HWCCT) key performance indicators (KPIs). You must also consider the minimum number of CPU cores and memory size of VMs as described in SAP Note 2188482. For more information see, [SAP support Launchpad](https://launchpad.support.sap.com/#/notes/2230704){: external}. You must have an SAP ID to access this web page.
