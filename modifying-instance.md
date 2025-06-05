---

copyright:
  years: 2024

lastupdated: "2025-06-05"

keywords: modifying an instance, {{site.data.keyword.powerSys_notm}} as a service, private clouds, howto, terminology, video, how-to, storage volume, new storage size, modifying server, editing volume, volume modification, DLPAR, modifying instance, scaling vm, public network, nic, affinity

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}


# Modifying an IBM {{site.data.keyword.powerSys_notm}} instance
{: #modifying-instance}

---



{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}


---

Learn how to modify your {{site.data.keyword.powerSysFull}} to better meet your business needs.
{: shortdesc}

## Resizing an instance by using the {{site.data.keyword.powerSys_notm}} user interface
{: #resizing-vm}

To resize a {{site.data.keyword.powerSys_notm}} instance after its [initial creation](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server), complete the following steps:

1. Go to **Virtual server instances** in the {{site.data.keyword.powerSys_notm}} user interface.

2. Click a virtual server instance to open the **Virtual server instance details** page.

3. Click the **Edit** icon, a menu appears. From the menu, select the value that you want to modify for the {{site.data.keyword.powerSys_notm}} instance. You can modify the following values: **Name**, **Entitled capacity**, **Memory (GB)**, and **VM pinning** state.

    If the virtual machine (VM) is inactive, you can change the processor type to *Dedicated*, *Shared uncapped shared*, or *Shared capped*.
    {: tip}

4. Select the service agreement box and click **Order** to complete the instance modification process and accept the price.

5. View the **Server details** page to verify {{site.data.keyword.powerSys_notm}} instance modification.

### Resizing the memory and core counts of the virtual machine
{: #resize-core-mem}

You can scale up and scale down the memory and core counts of the virtual machine (VM) according to your workload requirements. When the VM is active, you can resize the memory and core counts to a maximum of eight times of the specified values. When the VM is provisioned, you can resize the memory and core counts to a minimum of 1/8 times of the specified values. However, you cannot resize the memory and core count to less than 2 GB memory and 0.25 cores respectively. You can resize the memory and core count beyond the 8x and 1/8x boundaries when the VM is shut down. The following table shows an example of recalculated values:

| Specified value when the VM instance was provisioned | Minimum resize value (must be greater than or equal to 0.25 cores, 2 GB memory) | Maximum resize value |
|---------------------- | ------------------------- | ------------------------- |
|4 core and 8 GB memory | 0.5 cores and 2 GB memory | 32 cores and 64 GB memory |
{: class="simple-tab-table"}
{: tab-group="resize_core_memory"}
{: caption="Resizing VM core count and memory when the VM is active" caption-side="top"}
{: #resize_core_memory-1}
{: tab-title="When VM is active"}


| Specified value when the VM instance was provisioned | Minimum resize value (must be greater than or equal to 0.25 cores, 2 GB memory) | Maximum resize value |
|---------------------- | ------------------------- | ------------------------- |
|4 core and 8 GB memory | You can specify any value that is greater than 0.25 cores, 2 GB memory | You can specify any value that is smaller than the available resources in the host |
{: class="simple-tab-table"}
{: tab-group="resize_core_memory"}
{: caption="Resizing VM core count and memory when the VM is shut down" caption-side="top"}
{: #resize_core_memory-2}
{: tab-title="When VM is shut down"}

To resize an existing VM that was created before 15 December 2020 to an 8x ratio of memory and core counts, you must first shut down the VM, resize it, and then activate it. Resize the VM at least once when the VM is shut down to enable the 8x ratio. If you shut down and activate the VM, the 8x ratio of memory and core counts are not enabled.

## Managing your storage volumes
{: #modifying-volume-network}

You can attach storage volumes to a VM instance from different storage tiers and pools. However, you cannot attach storage volumes to the storage pool where the root (boot) volume of the VM instance is deployed. To attach a storage volume, you must modify the VM instance and set the new VM instance *storagePoolAffinity* property to false. You can now attach mixed storage to a VM instance. For more information, see [How to set a VM instance to allow attaching mixed storage?](/docs/power-iaas?topic=power-iaas-powervs-faqs#mixed_storage).

### Creating a storage volume
{: #create-storage-vol}

You can create a storage volume by specifying any name of your choice. If you want to reuse the storage volume name, you must delete the existing storage volume with the same name. If the existing volume is a replication-enabled volume, follow the steps to [delete a primary volume](/docs/power-iaas?topic=power-iaas-getting-started-GRS#delete-prime-vol). After you delete the original volume, you must allow a minimum of one hour to create a new volume with the same name.
{: note}


You can create a replication-enabled volume from any site. The site from which the replication is initiated contains what is referred to as the `primary volume`; the remote site volume is referred to as the `auxiliary volume`. For more information, see [Global Replication Services (GRS)](/docs/power-iaas?topic=power-iaas-getting-started-GRS).

When you are creating a storage volume from the user interface, you can enable the volume for replication by completing the following steps:

- In the **Global Replication Service** section, set the **Volume replication** to on. The name of the primary data center is displayed.
- From the **Secondary data center** list, select the displayed secondary site name.

The primary volume and the auxiliary volume are mapped into one-to-one relationship mode in both directions. These two sites are fixed and are in replication partnership in both directions. For more information, see [Setting up GRS](/docs/power-iaas?topic=power-iaas-getting-started-GRS#configure-GRS).

The GRS details of the volume are displayed when you click the storage volume.


### Adding and managing storage volumes
{: #adding-managing-volume}

If you want to attach or detach a volume, complete the following steps:


1. Go to **Virtual server instances** in the {{site.data.keyword.powerSys_notm}} user interface and click your instance.

2. Under the Attached volumes section, click **Attach volume** to add a storage volume from the list.

   Attaching storage volumes to a virtual server instance is an asynchronous operation. Before you use the storage volume, reload the page and check the status of the selected storage volume to confirm that it is successfully attached to the virtual server instance. If the volume is still not attached, you must make another attachment request.
   {: note}

3. To detach a storage volume, click **Detach** in the table.

    The user interface might display a failure message when you attempt to detach a volume from a virtual server instance. In such cases, you need to reload the page after a brief delay to see whether the volume is successfully detached. Make another detach request if the volume is still not disconnected.
    {: note}

4. You can also create a new storage volume.

5. Enter the **Name**, **Tier**, **Number of volumes**, and **Size** of the storage volume. You can also toggle the Shareable switch to the On position to allow multiple virtual instances to write data to the same data volume.

6. Select one of the following Storage pool options:
   - **Auto-select pool**: Use this option to allow the system to automatically select a storage pool, for the desired storage tier, that has sufficient capacity.
   - **Affinity**: Use this option to select an existing virtual server instance (VM) or an existing volume as the affinity object. The new volume is created in the same storage pool where the affinity object resides. If you are using VM instance as an affinity object, the storage pool that is selected is based on the PMV instance's root (boot) volume.
   - **Anti-affinity**: Use this option to specify one or more existing VM instances or one or more volumes as the anti-affinity objects. The new volume is created in a different storage pool than the storage pool where one or more anti-affinity objects reside.

    For more information about affinity and anti-affinity policies, see [What does it mean to set an affinity or anti-affinity rule?](/docs/power-iaas?topic=power-iaas-powervs-faqs#affinity).

    In the API, for create volume feature the properties `antiAffinityVMInstances` and `antiAffinityVolumes` are used to specify anti-affinity objects. You can specify only one object type for affinity or anti-affinity objects, either VM instances or Volumes. For more information about storage volumes APIs, see [Create a new data volume](/apidocs/power-cloud#pcloud-cloudinstances-volumes-post) and [Create multiple data volumes from a single definition](/apidocs/power-cloud#pcloud-v2-volumes-post).
    {: note}

7.  Click **Create and Attach**.


For more information about updating the volume groups for GRS, see [Updating a volume group](/docs/power-iaas?topic=power-iaas-getting-started-GRS&q=deleting+a+volume&tags=power-iaas#update-vol-grp).



Verify that the action that you perform on a volume group meets the current state of the volume group. Otherwise, an error message appears indicating that the volume group is not in the expected state.
{: attention}

The error message appears when you perform the following actions:
- Stop a volume group when the `ReplicationStatus` is in the `disabled` state.
- Start a volume group when the `ReplicationStatus` is in the `enabled` state or `available` state.
- Reset a volume group that is not in the error state.






### Resizing a storage volume
{: #resizing-volume}
{: help}
{: support}

You can resize a storage volume after its initial creation. However, resizing is not immediately available after you deploy a VM.


For more information about resizing a replication-enabled volume, see [Updating a primary volume](/docs/power-iaas?topic=power-iaas-getting-started-GRS&q=deleting+a+volume&tags=power-iaas#update-prime-vol).


[{{site.data.keyword.off-prem}}]{: tag-blue} For IBM i 7.3 and later versions, you can resize a volume to increase the volume size, but this action requires an initial program load (IPL) to recognize the new volume size.

Before you perform the IPL operation, you must run the macro to ensure that the volume resize operation is complete, then proceed with the IPL operation. For more information, see [Dynamically increasing the size of a SAN LUN](https://www.ibm.com/support/pages/dynamically-increasing-size-san-lun){: external}. If you do an IPL operation before the resize operation is complete, an extra IPL is required.
{: important}

If you cannot take the downtime, you can add extra volumes. You can attach a maximum of 127 volumes to the VM.

[{{site.data.keyword.off-prem}}]{: tag-blue} Any volume that is included in a snapshot cannot be resized. To resize a volume that is included in a snapshot, you must first delete all the snapshots the volume is a part of.
{: important}

1. Go to the {{site.data.keyword.powerSys_notm}} user interface and click **Storage volumes**.

2. Click the **Edit** icon to the right of your storage volume.

3. Click **Edit** to select the desired storage volume size in the **Modify storage volume** window. You can increase only the size of the storage volume.

4. Read the service agreement and agree to the terms. Click **Order** to complete the volume modification process and accept the price.

5. To verify your new storage size, go back to **Storage volumes**.

6. In an AIX VM instance, if you resize your boot storage volume, run the `chvg -g rootvg` command.

To apply or verify an IBM i software key, the VM must be active and in a running state. If you already ran a resize operation, you must wait until the resize operation completes and the VM returns to OK status.
{: note}



### Deleting a volume
{: #deleting-volume}
{: help}
{: support}

To delete a volume or a replication-enabled primary volume, the status of the storage volume must indicate one of the following states: `available`, `error`, `error_restoring`, `error_extending`, or `error_managing`. Also, the storage volume cannot be deleted if it is in the state of migrating, attached, belongs to a group, has snapshots, or is disassociated from its snapshots after a transfer.

Once you initiate the action to delete the volume, the action cannot be undone.
{: note}

For more information about deleting a primary volume, see [Deleting a primary volume](/docs/power-iaas?topic=power-iaas-getting-started-GRS#delete-prime-vol).




### Deleting a virtual server instance
{: #deleting-virtual-server-instance}
{: help}
{: support}

Deleting a virtual server instance is a manual process. To delete all virtual server instances, delete the workspace or delete a subset of the virtual server instance.

You can delete a single virtual server instance by completing the following steps:


1. On the **Virtual server instances** page, click the overflow menu (icon with 3 vertical dots) at the end of each virtual server instance entry on the table. From the overflow menu, click **Delete**. The **Delete virtual server instance** confirmation message box appears.<br>
Or<br>
On the **Virtual server instances** page, click the name of the virtual server instance that you want to delete. The **Virtual server instance details** page opens. Find and click the trash icon on the upper right of the screen. The **Delete virtual server instance** confirmation message box appears.
2. On the confirmation message box, if you set the toggle button to on you agree for the following actions to occur:
    - To delete the data volumes that are attached to the virtual server instance. The data volumes are not deleted if they are attached to multiple virtual server instances.
    - To delete any auxiliary volumes on the secondary site.
3. Type the virtual server instance name in the textbox.
4. Click **Delete the virtual server instance** to initiate the deletion request.

After the deletion request is initiated, the action cannot be undone.
{: note}



## Adding or removing a public network
{: #adding-removing-network}

[{{site.data.keyword.off-prem}}]{: tag-blue}

You can remove or add a public network by clicking the **Public networks** toggle in **Virtual server instances**. When you toggle a public network off and then on, the {{site.data.keyword.powerSys_notm}} user interface regenerates new internal and external IP addresses. You need to check the {{site.data.keyword.powerSys_notm}} user interface for the new internal IP address (that maps to the external IP address). You must add a network interface controller (NIC) and point it to the new internal IP address. For information about how to add or remove an interface, see [How to add or remove a network interface from an AIX virtual machine (VM)](/docs/power-iaas?topic=power-iaas-managing-network-interface) or [How to add or remove a network interface from an IBM i virtual machine (VM)](/docs/power-iaas?topic=power-iaas-managing-network-interface-ibmi).

You cannot toggle a public network off if there are no other defined networks.
{: note}

## Detecting problems by using the System Reference Code (SRC)
{: #detect-problems-using-src}

SRC is only supported for AIX and IBM i virtual machines.
{: note}

A *system reference code (SRC)* is a set of eight alphanumeric characters that identifies the name of the system component that detects the error codes and the reference code. The error codes and the reference code describe the error condition. When the {{site.data.keyword.powerSys_notm}} instance detects a problem, an SRC number is displayed along with a timestamp in the **Server details** page. You can use the SRC to resolve the issue yourself. If you are contacting support to resolve a problem, the SRC number might help the hardware service provider better understand the problem and to provide the solution.

[{{site.data.keyword.off-prem}}]{: tag-blue} For an IBM i VM, the SRC number can be progress code, operation code, or software code. For more information, see the [System Reference Code list](https://www.ibm.com/support/knowledgecenter/ssw_ibm_i_73/rzahb/rzahbsrclist.htm){: external} in the IBM i documentation. For AIX VM instances, the SRC numbers are progress codes that provide information about the stages that are involved in powering on and performing initial program load (IPL). AIX SRCs refresh once in 2 minutes. For more information, see [AIX IPL progress codes](https://www.ibm.com/support/knowledgecenter/POWER9_REF/p9eai/aixIPL_info.htm){: external}.


## Use cases
{: #use-case-resize-vm}

The following are some of the scenarios that you might face when you make a request for resizing the memory of a {{site.data.keyword.powerSys_notm}} instance:

### Your request for resizing both memory and CPU fails:
{: #resize-mem-cpu-fail}

When you attempt to resize the memory and the CPU of a deployed virtual server instance through a single request, it might fail due to the following reasons:
- No free memory is available on the host.
- No free memory is available on the logical partition as the resources on it are running.
- The free memory that is available on the logical partition is less than the desired value indicated in the resizing request.
- Multiple attempts are made for resizing.

    Currently, there is no preference for memory or CPU on what can be resized first. If the first request processing fails, the second request also fails automatically.
    {: note}

`Example`: Consider that the allocated memory for the logical partition is 4 GB. You make a request to reduce the memory value to 2 GB. The logical partitioning is using up to 3.2 GB for running resources in it. So, logical partitioning does not have free 2 GB memory for resizing. In such a scenario, it is possible that both the CPU and memory resize might fail.



### You request for resizing the memory, but you get a partial resize:
{: #resize-mem-cpu-partial}

When you attempt to resize the memory of a deployed virtual server instance through a request, it might partially resize or might fail due to the following reasons:
- No free memory is available on the host.
- No free memory is available on the logical partition as the resources are running on it.
- The free memory that is available on the logical partition is less than the desired value indicated in the resizing request.
- Multiple attempts are made for resizing.

`Example`: Consider that the allocated memory for the logical partition is 4 GB. You make a request to reduce the memory value to 2 GB. The logical partitioning is using up to 3 GB for running resources in it and so can free up only 1 GB memory. Then, the partial resize can reduce the memory to 3 GB.



In the current cloud environment, it might take up to 1.5 hours for the change in memory to be updated. All the places that are referring to the memory of the logical partition are to be updated. Hence, if you attempt to repeat the resize request, the consecutive retires fails until all referencing tables are updated.
{: important}
