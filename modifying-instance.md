---

copyright:
  years: 2019, 2020

lastupdated: "2020-02-24"

keywords: storage volume, new storage size, modifying server, editing volume, volume modification, DLPAR, modifying instance, scaling vm, public network, nic, affinity

subcollection: power-iaas

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:preview: .preview}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}

# Modifying a Power Systems Virtual Server instance
{: #modifying-server}

Learn how to modify your {{site.data.keyword.powerSysShort}} to better meet your business needs.
{: shortdesc}

## Resizing an instance by using the Power Systems Virtual Server user interface
{: #resizing-vm}

To resize a {{site.data.keyword.powerSys_notm}} instance after its [initial creation](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server), complete the following steps:

1. Go to **Virtual server instances** in the {{site.data.keyword.powerSys_notm}} user interface and click your instance.

2. Click the **Edit** icon in the **Server details** pane.

    ![Finding your server details](./images/console-server-details.png "Finding your server details"){: caption="Figure 1. Finding your server details" caption-side="bottom"}

3. A menu appears after you click the **Edit** icon. Here, you can change your instance's **Name**, **Entitled capacity**, **Memory (GB)**, and **VM pinning** state.

    If the VM is inactive or shut down, you can change the processor type to Dedicated processor, Uncapped shared processor or Capped shared processor.
    {: tip}

4. Check the service agreement box and click **Order** to complete the instance modification process and accept the price.

5. View the **Server details** pane to verify your instance modification.

### Resizing the virtual machine core count and memory
{: #resize-core-mem}

You can scale up and scale down the core count and memory of the virtual machine (VM) as per your workload requirements. When the VM is active, you can resize the memory and core counts to a maximum of eight times of the specified values, and to a minimum of 1/8 times of the specified values when the VM was provisioned. However, you cannot resize the memory and core count to less than 0.25 cores and 2 GB memory. You can resize the memory and core count beyond the 8x and 1/8x boundaries when the VM is shut down. The following table shows an example of recalculated values:

| Specified value when the VM instance was provisioned | Minimum resize value (must be greater than or equal to 0.25 cores, 2 GB memory) | Maximum resize value |
|---------------------- | ------------------------- | ------------------------- |
|4 core and 8 GB memory | 0.5 cores and 2 GB memory | 32 cores and 64 GB memory |
{: class="simple-tab-table"}
{: tab-group="resize_core_memory"}
{: caption="Table 1. Resizing VM core count and memory when the VM is active" caption-side="top"}
{: #resize_core_memory-1}
{: tab-title="When VM is active"}


| Specified value when the VM instance was provisioned | Minimum resize value (must be greater than or equal to 0.25 cores, 2 GB memory) | Maximum resize value |
|---------------------- | ------------------------- | ------------------------- |
|4 core and 8 GB memory | You can specify any value that is greater than 0.25 cores, 2 GB memory | You can specify any value that is smaller than the available resources in the host |
{: class="simple-tab-table"}
{: tab-group="resize_core_memory"}
{: caption="Table 1. Resizing VM core count and memory when the VM is shut down" caption-side="top"}
{: #resize_core_memory-2}
{: tab-title="When VM is shut down"}

If you want to resize an existing VM that was created before 15 December 2020 to 8x ratio of core count and memory, you must first shut down the VM, resize the VM, and then activate the VM. You must resize the VM at least once when the VM is shut down to enable 8x ratio. Simply shutting down and activating the VM does not enable the 8x ratio of core count and memory.

## Managing your storage volumes
{: #modifying-volume-network}

Learn how to add new storage volumes and modify existing ones. You can now attach storage volumes to a PVM instance from different storage tiers and pools, other than the storage pool the PVM instance's root (boot) volume is deployed in. To accomplish this you must modify the PVM instance and set the new PVM instance *storagePoolAffinity* property to false.

### Adding and managing storage volumes
{: #adding-managing-volume}

You can now attach mixed storage to a PVM instance. For more information, see [How to set a PVM instance to allow attaching mixed storage?](/docs/power-iaas?topic=power-iaas-power-iaas-faqs#mixed_storage)

If you'd like to attach or detach a volume, click **Manage existing volumes** and select the wanted volume. 

1. Click **New volume** to add a storage volume.

2. Enter the **Name**, **Type**, and **Size** of the storage volume. You can also select whether to make the storage volume **Shareable** and select **Auto-select pool**, **Affinity**, or **Anti-affinity**. If you select **Auto-select pool**, the storage volume is automatically created in a pool with sufficient capacity. You can use storage affinity to control the placement of a new volume in a particular storage provider (pool) based on an affinity policy. When you set the affinity policy to **affinity** for creating a new volume, you can select an existing PVM instance (VM) or an existing volume as the affinity object. The new volume is created in the same storage pool where the affinity object resides. If you are using PVM instance as an affinity object, the storage pool that is selected is based on the PMV instance's root (boot) volume. When you select the affinity policy to **anti-affinity** for creating a new volume, you can specify one or more existing PVM instances or one or more volumes as the anti-affinity objects. The new volume is created in a different storage pool than the storage pool where one or more anti-affinity objects reside. For more information about affinity and anti-affinity policy, see [What does it mean to set an affinity or anti-affinity rule?](/docs/power-iaas?topic=power-iaas-power-iaas-faqs#affinity).

     In the API for create volume feature two new properties *antiAffinityPVMInstances* and *antiAffinityVolumes* are added. These two new properties are used for specifying anti-affinity objects only. You can specify only one object type for affinity or anti-affinity objects, either PVM Instances or Volumes. For more information about storage volumes APIs, see [Create a new data volume](/apidocs/power-cloud#pcloud-cloudinstances-volumes-post) and [Create multiple data volumes from a single definition](/apidocs/power-cloud#pcloud-v2-volumes-post).
    {: note}

3. Click **Next**, agree to the service agreement, and submit your **Order**.

### Resizing a storage volume
{: #resizing-volume}
{: help}
{: support}

You can resize a storage volume after its initial creation. To delete a volume, its status must indicate one of the following states: `available`, `error`, `error_restoring`, `error_extending`, or `error_managing`. Additionally, the storage volume cannot be deleted if it is migrating, attached, belongs to a group, has snapshots, or is disassociated from its snapshots after a transfer. Resizing is not immediately available after you deploy a VM. For IBM i 7.3 and 7.4 versions, you can resize volume to increase the volume size, but this requires an initial program load (IPL) to recognize the new volume size. 

Before you perform the IPL operation, you must run the macro to ensure that the volume resize operation is complete, then proceed with the IPL operation. For more information, see  [Dynamically increasing the size of a SAN LUN](https://www.ibm.com/support/pages/dynamically-increasing-size-san-lun){: external}. If you perform an IPL operation before the resize operation is complete, an additional IPL is required. 
{: important}

If you cannot take the downtime, you can add additional volumes. You can attach maximum of 127 volumes to the VM.

Any volume that has been included in a snapshot cannot be resized. To resize a volume that has been included in a snapshot, you must first delete all of the snapshots the volume is a part of.
{: important}

1. Go to the {{site.data.keyword.powerSys_notm}} user interface and click **Storage volumes**.

2. Click the **Edit** icon to the right of your storage volume.

3. After you click the **Edit** icon, a menu appears. Select the wanted storage volume size. You can increase only the size of the storage volume.

    ![Modifying your storage volume](./images/console-modify-volume.png "Modifying your storage volume"){: caption="Figure 2. Modifying your storage volume" caption-side="bottom"}

4. Read the service agreement and agree to the terms. Click **Order** to complete the volume modification process and accept the price.

5. To verify your new storage size, go back to **Storage volumes**.

6. In an AIX VM instance, if you resize your boot storage volume, run the `chvg -g rootvg` command.

To apply or verify an IBM i software key, the VM must be active and in running state. If you already ran a resize operation, you must wait until the resize operation complete and VM returns to OK status.
{: note}

## Adding or removing a public network
{: #adding-removing-network}

You can remove or add a public network by clicking the **Public networks** toggle in **Virtual server instances**. When you toggle a public network off and then on, the {{site.data.keyword.powerSys_notm}} user interface regenerates new internal and external IP addresses. You need to check the {{site.data.keyword.powerSys_notm}} user interface for the new internal IP address (that maps to the external IP address). You must add a network interface controller (NIC) and point it to the new internal IP address. For information on how to add or remove an interface, see [How to add or remove a network interface from an AIX virtual machine (VM)](/docs/power-iaas?topic=power-iaas-managing-network-interface) or [How to add or remove a network interface from an IBM i virtual machine (VM)](/docs/power-iaas?topic=power-iaas-managing-network-interface-ibmi).

You cannot toggle a public network off if there are no other defined networks.
{: note}

## Detecting problems by using the System Reference Code (SRC)
{: #detect-problems-using-src}

A *system reference code (SRC)* is a set of eight alphanumeric characters that identifies the name of the system component that detects, the error codes, and the reference code that describes the error condition. When the {{site.data.keyword.powerSys_notm}} instance detects a problem, an SRC number is displayed along with a timestamp in the **Server details** page. You can use the SRC to resolve the issue yourself. If you are contacting support to resolve a problem, the SRC number might help the hardware service provider better understand the problem and to provide the solution.

For an IBM i VM, the SRC number can be progress code, operation code, or software code. For more information, see the [System Reference Code list](https://www.ibm.com/support/knowledgecenter/ssw_ibm_i_73/rzahb/rzahbsrclist.htm){: external} in IBM i documentation. For AIX VM instances, the SRC numbers are progress codes that provide information about the stages involved in powering on and performing initial program load (IPL). AIX SRCs refresh once in 2 minutes. For more information, see [AIX IPL progress codes](https://www.ibm.com/support/knowledgecenter/POWER9_REF/p9eai/aixIPL_info.htm){: external}.