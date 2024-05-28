---

copyright:
  years: 2023

lastupdated: "2023-04-22"

keywords: modifying an instance, {{site.data.keyword.powerSys_notm}} as a service, private clouds, howto, terminology, video, how-to

subcollection: power-iaas

---


{{site.data.keyword.attribute-definition-list}}


# Modifying a {{site.data.keyword.powerSys_notm}} instance
{: #modifying-instance}

Learn how to modify your {{site.data.keyword.powerSysFull}} to better meet your business needs.
{: shortdesc}

## Resizing an instance by using the {{site.data.keyword.powerSys_notm}} user interface
{: #resizing-vm}

To resize a {{site.data.keyword.powerSys_notm}} instance after its [initial creation](/docs-draft/power-iaas?topic=power-iaas-creating-power-virtual-server), complete the following steps:

1. Go to **Virtual server instances** in the {{site.data.keyword.powerSys_notm}} user interface and click your instance.

2. Click the **Edit details** in the server details pane.

3. Click the **Edit** icon, a menu appears. From the menu, select the value you want to modify for the {{site.data.keyword.powerSys_notm}} instance. You can modify the following values: **Name**, **Entitled capacity**, **Memory (GB)**, and **VM pinning** state.

    If the virtual machine (VM) is inactive, you can change the processor type to *Dedicated processor*, *Uncapped shared processor*, or *Capped shared processor*.
    {: tip}

4. Check the service agreement box and click **Order** to complete the instance modification process and accept the price.

5. View the **Server details** pane to verify {{site.data.keyword.powerSys_notm}} instance modification.

### Resizing the memory and core counts of the virtual machine
{: #resize-core-mem}

You can scale up and scale down the memory and core counts of the virtual machine (VM) according to your workload requirements. When the VM is active, you can resize the memory and core counts to a maximum of eight times of the specified values. When the VM is provisioned, you can resize the memory and core counts to a minimum of 1/8 times of the specified values. However, you cannot resize the memory and core count to less than 2 GB memorey and 0.25 cores respectively. You can resize the memory and core count beyond the 8x and 1/8x boundaries when the VM is shut down. The following table shows an example of recalculated values:

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

To resize an existing VM that was created before 15 December 2020 to an 8x ratio of memory and core counts, you must first shut down the VM, resize it, and then activate it. Resize the VM at least once when the VM is shut down to enable the 8x ratio. Simply shutting down and activating the VM does not enable the 8x ratio of memory and core counts.

## Managing your storage volumes
{: #modifying-volume-network}

You can attach storage volumes to a VM instance from different storage tiers and pools. However, you cannot attach storage volumes to the storage pool where the root (boot) volume of the VM instance is deployed. To attach a storage volume, you must modify the VM instance and set the new VM instance *storagePoolAffinity* property to false. You can now attach mixed storage to a VM instance. For more information, see [How to set a VM instance to allow attaching mixed storage?](/docs-draft/power-iaas?topic=power-iaas-powervs-faqs#mixed_storage).

You can create a storage volume by specifying any name of your choice. If you want to reuse the storage volume name, you must delete the existing storage volume with the same name. After you delete the original volume, allow one hour before creating a new volume with the same name.
{: note}

### Adding and managing storage volumes
{: #adding-managing-volume}

If you want to attach or detach a volume, complete the following steps:

1. Go to **Virtual server instances** in the {{site.data.keyword.powerSys_notm}} user interface and click your instance.

2. Under the Attached volumes section, click **Attach volume** to add a storage volume from the list.

   Attaching storage volumes to a virtual server instance is an asynchronous operation. Before you use the storage volume, reload the page and check the status of the selected storage volume to confirm that it is successfully attached to the virtual server instance. If the volume is still not attached, you must make another attachment request.
   {: note}

3. To detach a storage volume, click **Detach** in the table.

    The user interface may display a failure message when you attempt to detach a volume from a virtual server instance. In such cases, you need to reload the page after a brief delay in order to see if the volume has been successfully detached. Another detach request should be made if the volume is still not disconnected.
    {: note}

4. You can also create a new storage volume.

5. Enter the **Name**, **Tier**, **Number of volumes**, and **Size** of the storage volume. You can also toggle the Shareable switch to the On position to allow multiple virtual instances to write data to the same data volume.

6. Select one of the following Storage pool options:
   - **Auto-select pool**: Use this option to allow the system to automatically select a storage pool, for the desired storage tier, that has sufficient capacity.
   - **Affinity**: Use this option to select an existing VM instance (VM) or an existing volume as the affinity object. The new volume is created in the same storage pool where the affinity object resides. If you are using VM instance as an affinity object, the storage pool that is selected is based on the PMV instance's root (boot) volume.
   - **Anti-affinity**: Use this option to specify one or more existing VM instances or one or more volumes as the anti-affinity objects. The new volume is created in a different storage pool than the storage pool where one or more anti-affinity objects reside.

    For more information about affinity and anti-affinity policy, see [What does it mean to set an affinity or anti-affinity rule?](/docs-draft/power-iaas?topic=power-iaas-powervs-faqs#affinity).

    In the API for create volume feature two new properties *antiAffinityVMInstances* and *antiAffinityVolumes* have been added. These properties are used only to specify anti-affinity objects. You can specify only one object type for affinity or anti-affinity objects, either VM Instances or Volumes. For more information about storage volumes APIs, see [Create a new data volume](/apidocs/power-cloud#pcloud-cloudinstances-volumes-post) and [Create multiple data volumes from a single definition](/apidocs/power-cloud#pcloud-v2-volumes-post).
    {: note}

7.  Click **Create and Attach**.

### Resizing a storage volume
{: #resizing-volume}
{: help}
{: support}

You can resize a storage volume after its initial creation. To delete a volume, its status must indicate one of the following states: `available`, `error`, `error_restoring`, `error_extending`, or `error_managing`. Additionally, the storage volume cannot be deleted if it is migrating, attached, belongs to a group, has snapshots, or is disassociated from its snapshots after a transfer. Resizing is not immediately available after you deploy a VM.

[Off-Premises]{: tag-blue} For IBM i 7.3 and later versions, you can resize volume to increase the volume size, but this requires an initial program load (IPL) to recognize the new volume size.

Before you perform the IPL operation, you must run the macro to ensure that the volume resize operation is complete, then proceed with the IPL operation. For more information, see  [Dynamically increasing the size of a SAN LUN](https://www.ibm.com/support/pages/dynamically-increasing-size-san-lun){: external}. If you perform an IPL operation before the resize operation is complete, an additional IPL is required.
{: important}

If you cannot take the downtime, you can add additional volumes. You can attach maximum of 127 volumes to the VM.

[Off-Premises]{: tag-blue} Any volume that has been included in a snapshot cannot be resized. To resize a volume that has been included in a snapshot, you must first delete all of the snapshots the volume is a part of.
{: important}

1. Go to the {{site.data.keyword.powerSys_notm}} user interface and click **Storage volumes**.

2. Click the **Edit** icon to the right of your storage volume.

3. Click on **Edit** to select the desired storage volume size in the **Modify storage volume** window. You can increase only the size of the storage volume.

4. Read the service agreement and agree to the terms. Click **Order** to complete the volume modification process and accept the price.

5. To verify your new storage size, go back to **Storage volumes**.

6. In an AIX VM instance, if you resize your boot storage volume, run the `chvg -g rootvg` command.

To apply or verify an IBM i software key, the VM must be active and in running state. If you already ran a resize operation, you must wait until the resize operation complete and VM returns to OK status.
{: note}

## Adding or removing a public network
{: #adding-removing-network}

[Off-Premises]{: tag-blue}

You can remove or add a public network by clicking the **Public networks** toggle in **Virtual server instances**. When you toggle a public network off and then on, the {{site.data.keyword.powerSys_notm}} user interface regenerates new internal and external IP addresses. You need to check the {{site.data.keyword.powerSys_notm}} user interface for the new internal IP address (that maps to the external IP address). You must add a network interface controller (NIC) and point it to the new internal IP address. For information on how to add or remove an interface, see [How to add or remove a network interface from an AIX virtual machine (VM)](/docs-draft/power-iaas?topic=power-iaas-managing-network-interface) or [How to add or remove a network interface from an IBM i virtual machine (VM)](/docs-draft/power-iaas?topic=power-iaas-managing-network-interface-ibmi).

You cannot toggle a public network off if there are no other defined networks.
{: note}

## Detecting problems by using the System Reference Code (SRC)
{: #detect-problems-using-src}

SRC is only supported for AIX and IBMi virtual machines.
{: note}

A *system reference code (SRC)* is a set of eight alphanumeric characters that identifies the name of the system component that detects, the error codes, and the reference code that describes the error condition. When the {{site.data.keyword.powerSys_notm}} instance detects a problem, an SRC number is displayed along with a timestamp in the **Server details** page. You can use the SRC to resolve the issue yourself. If you are contacting support to resolve a problem, the SRC number might help the hardware service provider better understand the problem and to provide the solution.

[Off-Premises]{: tag-blue} For an IBM i VM, the SRC number can be progress code, operation code, or software code. For more information, see the [System Reference Code list](https://www.ibm.com/support/knowledgecenter/ssw_ibm_i_73/rzahb/rzahbsrclist.htm){: external} in IBM i documentation. For AIX VM instances, the SRC numbers are progress codes that provide information about the stages involved in powering on and performing initial program load (IPL). AIX SRCs refresh once in 2 minutes. For more information, see [AIX IPL progress codes](https://www.ibm.com/support/knowledgecenter/POWER9_REF/p9eai/aixIPL_info.htm){: external}.


## Use cases
{: #use-case-resize-vm}

The different scenarios that you may face while requesting for resizing a {{site.data.keyword.powerSys_notm}} instance's memory are listed below.

### You request for resizing both memory and CPU fails
{: #resize-mem-cpu-fail}

When you attempt to resize the memory as well as CPU of a deployed virtual server instance through a single request it may fail due to the following reasons:
- There is no free memory available on the host.
- There is no free memory available on the logical partition as the resources on it are running.
- The free memory available on the logical partition is less than that of the desired value indicated in the resizing request.
- You have made multiple attempts for resizing.
- Currently, there is no preference for memory or CPU on what should be resized first. If the first request being processed fails, the second one will also fail automatically.

`Example`: When the currently allocated memory for the logical partition is 4GB and you are trying to reduce the value to 2GB and the logical partition at the time of request does not have free 2GB memory for resizing (considering the logical partition is using upto 3.2 GB for running resources in it), then there is a possibility that both the CPU and memory resize will fail.

### You request for resizing the memory but you get a partial resize
{: #resize-mem-cpu-partial}

When you attempt to resize the memory of a deployed virtual server instance through a request, it may partially resize or in the worst scenarios even fail due to the following reasons:
- There is no free memory available on the host will result in failed request.
- There is no free memory available on the logical partition as the resources are running on it. This will result in a failed request.
- The free memory available on the logical partition is less than that of the desired value indicated in the resizing request. This will result in a partial resize.
- You have made multiple attempts for resizing. This will result in a failed request.

`Example`:When the currently allocated memory for the logical partition is 4GB and you are trying to reduce the value to 2GB and the logical partition at the time of request does not have free 2GB memory for resizing (considering the logical partition is using upto 3 GB for running resources in it) and can free up only 1 GB, then the partial resize should be possible to reduce the memory to 3GB.

In the current cloud environment, it may take upto 1.5 hours approximately for the change in memory to be updated to places referring to the memory of the logical partition. Hence if you attempt to repeat the resize request, the consecutive retires will fail, until all referencing tables are updated.
{: important}
