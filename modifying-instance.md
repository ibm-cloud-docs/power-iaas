---

copyright:
  years: 2024

lastupdated: "2025-10-14"

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


After you create a virtual server instance (VSI) in your {{site.data.keyword.powerSysFull}} workspace, you can modify some of its configurations to meet your business and workload needs. You can update the VSI name, change the preferred processor compatibility mode, adjust its pinning state and placement group, change its capacity, such as the core type, number of cores, virtual cores, and memory. You can also manage the storage volumes and reconfigure the network interfaces that are attached to the VSI.
{: shortdesc}


## Modifying a VSI by using the {{site.data.keyword.powerSys_notm}} user interface
{: #resizing-vm}

To modify a VSI after its [initial creation](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server), complete the following steps:

1. Open the {{site.data.keyword.powerSys_notm}} user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.

2. Click **Workspaces** in the navigation panel. The Workspaces page with a list of existing workspaces is displayed.

3. Select the workspace that contains the virtual server instance that you want to modify. The Workspace details panel is displayed.

4. Click **View virtual servers**. The Virtual server instances page is displayed.

5. Select the VSI that you want to modify. The Virtual server instance details page is displayed for the selected VSI.



From the Virtual server instance details page, You can use the **Overview**, **Storage**, and **Networking** tabs to modify specific components of a VSI. Depending on your requirements, you can perform the following modifications:
- [Changing the VSI name](#edit-vsi-name)
- [Changing the preferred processor compatibility mode](#change-cpu-compatibility)
- [Changing the pinning state and server placement group](#edit-vsi-pinning-placement)
- [Resizing the capacity of a VSI](#resize-core-mem)
- [Managing the storage volumes](#modifying-volume-network)
- [Adding or removing a public network](#adding-removing-network)






### Changing the VSI name
{: #edit-vsi-name}

To change the name of the VSI, complete the following steps:

1. On the **Overview** tab, click the **Edit** icon in the Virtual server instance details section. The Edit virtual server instance details panel is displayed.
2. Enter the new name in the **Name** field.
3. Click **Save**.

### Changing the preferred processor compatibility mode
{: #change-cpu-compatibility}

In virtualization environments, a VSI can operate in different processor compatibility modes. These modes determine the Instruction Set Architecture (ISA) version that is used by the processor and the platform-level features that are available to the VSI. The Virtual server instance details page on the **Overview** tab displays the *Preferred* and *Effective* processor compatibility mode that is currently set for the VSI. Processor compatibility modes are defined as follows:

- **Preferred processor compatibility mode**: The processor mode in which you want the VSI to operate. By default, {{site.data.keyword.powerSys_notm}} sets the preferred processor compatibility mode to the highest mode that is supported by the targeted host type for the VSI.

- **Effective processor compatibility mode**: The processor mode that is currently in use for the VSI. The physical host where the VSI is running determines the effective processor compatibility mode.

You cannot dynamically change the effective processor compatibility mode of a VSI. To change the effective processor compatibility mode, you must first change the preferred processor compatibility mode of the VSI, shut down the VSI, and then start the VSI again. During VSI activation, the hypervisor attempts to set the effective processor compatibility mode to match the preferred mode that you have specified for the VSI.

You must select the appropriate processor mode to ensure compatibility with the operating system that is in use. If you set the preferred processor compatibility mode to a mode that the operating system in your VSI does not support, the VSI does not boot correctly and might enter the *Error* state. To resolve this problem, open a [support ticket](/docs/power-iaas?topic=power-iaas-getting-help-and-support){: external}.
{: important}








The effective mode might differ from the preferred mode if the host does not support the preferred mode that you have specified for the VSI.
{: note}

You can use the CLI, API or Terraform to set the preferred processor compatibility mode for a VSI during its creation. When using the GUI, you can change the preferred mode only by editing an existing VSI that has already been deployed.

To change the preferred processor compatibility mode of a VSI by using the {{site.data.keyword.powerSys_notm}} user interface, complete the following steps:

1. On the **Overview** tab, click the **Edit** icon in the Virtual server instance details section. The Edit virtual server instance details panel is displayed.
2. Select the preferred processor compatibility mode from the **Preferred processor compatibility mode** list.
3. Click **Save**.

Note that after you change the preferred processor compatibility mode of a VSI, you must shut down the VSI and then start the VSI again for the changes to take effect. A restart alone does not activate the selected preferred processor compatibility mode.

To shut down the VSI, complete the following steps:

1. From the virtual server instance details page of the selected VSI, select **OS Shutdown** from the overflow menu (⋮). The OS shutdown confirmation dialog is displayed.

2. Click **Shutdown** to procced. A notification is displayed to indicate that the shutdown process has started.

To start the VSI again, complete the following steps :

1. From the virtual server instance details page of the selected VSI, select **Start** from the overflow menu (⋮). A notification is displayed to indicate that the VSI is being started.

2. Click the **Refresh** icon to see the change take effect.

For more information about the processor compatibility mode, see [How does the processor compatibility mode work in a VSI?](/docs/power-iaas?topic=power-iaas-powervs-faqs#processor-compatibility-modes-vsi){: external}


### Changing the pinning state and server placement group
{: #edit-vsi-pinning-placement}

You can use VSI pinning to control the movement of VSIs during disasters and other restart events. You can either choose *soft* pin or *hard* pin to pin a VSI to the host where it is running. For more information about VSI pinning, see [What does VM pinning do?](/docs/power-iaas?topic=power-iaas-powervs-faqs#pinning){: external}.

Server placement groups provides you control over the host or server on which a new VSI is placed. By using server placement groups, you can build high availability within a data center. For more information about see [Managing server placement groups](/docs/power-iaas?topic=power-iaas-managing-placement-groups){: external}.

To change the pinning state and server placement group of the VSI, complete the following steps:

1. In the **Overview** tab, click the **Edit** icon in the Placement section. The Edit placement panel is displayed.
3. Select the new pinning policy from the **Virtual server pinning** list and the placement group from the **Placement group** list.
4. Click **Save**

### Resizing the capacity of a VSI
{: #resize-core-mem}

You can edit a VSI to resize its capacity, including memory, core type, and number of physical and virtual cores.

You can scale up and scale down the memory and core counts of the VSI according to your workload requirements. When the VSI is active, you can resize the memory and core counts to a maximum of eight times of the specified values. When the VSI is provisioned, you can resize the memory and core counts to a minimum of 1/8 times of the specified values. However, you cannot resize the memory and core count to less than 2 GB memory and 0.25 cores respectively. You can resize the memory and core count beyond the 8x and 1/8x boundaries when the VSI is shut down. The following table shows an example of recalculated values:

| Specified value when the VSI instance was provisioned | Minimum resize value (must be greater than or equal to 0.25 cores, 2 GB memory) | Maximum resize value |
|---------------------- | ------------------------- | ------------------------- |
|4 core and 8 GB memory | 0.5 cores and 2 GB memory | 32 cores and 64 GB memory |
{: class="simple-tab-table"}
{: tab-group="resize_core_memory"}
{: caption="Resizing VSI core count and memory when the VSI is active" caption-side="top"}
{: #resize_core_memory-1}
{: tab-title="When VSI is active"}


| Specified value when the VSI instance was provisioned | Minimum resize value (must be greater than or equal to 0.25 cores, 2 GB memory) | Maximum resize value |
|---------------------- | ------------------------- | ------------------------- |
|4 core and 8 GB memory | You can specify any value that is greater than 0.25 cores, 2 GB memory | You can specify any value that is smaller than the available resources in the host |
{: class="simple-tab-table"}
{: tab-group="resize_core_memory"}
{: caption="Resizing VSI core count and memory when the VSI is shut down" caption-side="top"}
{: #resize_core_memory-2}
{: tab-title="When VSI is shut down"}

To resize an existing VSI that was created before 15 December 2020 to an 8x ratio of memory and core counts, you must first shut down the VSI, resize it, and then activate it. Resize the VSI at least once when the VSI is shut down to enable the 8x ratio. If you shut down and activate the VSI, the 8x ratio of memory and core counts are not enabled.

To edit a VSI and resize its capacity, complete the following steps:

1. On the **Overview** tab, click the **Edit** icon in the Capacity section. The Edit capacity panel is displayed.
2. Select the new value and size for the VSI's memory, cores, and virtual cores. The total estimated cost for the new selection is displayed for your review.
3. Click the terms and conditions link to read the IBM Cloud Terms of Use. To continue, select the **I agree to the Terms and conditions** checkbox and click **Save**.

    If the VSI that you are editing is in inactive state, you can change the **Core type** to *Dedicated*, *Shared uncapped shared*, or *Shared capped*.
    {: tip}



## Managing your storage volumes
{: #modifying-volume-network}

You can attach storage volumes to a VSI from different storage tiers and pools. However, you cannot attach storage volumes to the storage pool where the root (boot) volume of the VSI is deployed. To attach a storage volume, you must modify the VSI and set the new VSI's *storagePoolAffinity* property to false. You can now attach mixed storage to a VSI. For more information, see [How to set a VSI to allow attaching mixed storage?](/docs/power-iaas?topic=power-iaas-powervs-faqs#mixed_storage).

### Creating a storage volume
{: #create-storage-vol}

After you create a VSI, you can modify the VSI to include additional storage volumes, either by adding new volumes or attaching existing ones.

To modify a VSI to add additional storage volumes, complete the following steps:

1. Open the {{site.data.keyword.powerSys_notm}} user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.

2. Click **Workspaces** in the navigation panel. The Workspaces page with a list of existing workspaces is displayed.

3. Select the workspace that contains the virtual server instance to which you want to add additional volumes to. The Workspace details panel is displayed.

4. Click **View virtual servers**. The Virtual server instances page is displayed.

5. Select the VSI to which you want to add additional volumes. The Virtual server instance details page is displayed for the selected VSI.

Based on whether you want to attach an existing storage volume or create a new one for the VSI, follow the steps in the relevant section below.

- [Attaching an existing volume to the VSI](#attach-existing-vol)
- [Creating a new storage volume for the VSI](#create-new-vol)

#### Attaching an existing volume to the VSI
{: #attach-existing-vol}

1. On the **Storage** tab, click **Attach existing** in the Storage volumes section. The Attach storage volumes panel is displayed with a list of existing storage volumes.

2. Select the storage volumes that you want to add to the VSI. If the **Mixed storage pools in virtual server instances** warning message is displayed, select the following checkboxes:
    - *I acknowledge snapshots and clones will fail when performed on a set of volumes that are on mixed pools*.
    - *I acknowledge volume replication across mixed storage pools will require managing multiple volume replication groups when enabled*.

3. Click **Attach volume**.

Attaching storage volumes to a virtual server instance is an asynchronous operation. Before you use the storage volume, refresh the VSI details page and check the status of the selected storage volume to confirm that it is successfully attached to the virtual server instance. If the volume is still not attached, you must make another attachment request.
{: note}

#### Creating a new storage volume for the VSI
{: #create-new-vol}

1. On the **Storage** tab, click **Create volume** in the Storage volumes section. The Create volume panel is displayed.

2. Enter the **Name**, and **User tags** (optional) for the storage volume.

3. Select the required storage tier from the **Tier** list.

4. Enter the **Number of volumes**, and **Size** of the storage volume.

5. Set **Shareable** to **On** to allow multiple virtual instances to write data to the same data volume.

6. Select one of the following **Storage pool** options:

   - **Auto-select pool**: Use this option to allow the system to automatically select a storage pool, for the desired storage tier, that has sufficient capacity.

   - **Affinity**: Use this option to select an existing virtual server instance (VSI) or an existing volume as the affinity object. The new volume is created in the same storage pool where the affinity object resides. If you are using the VSI as an affinity object, the storage pool that is selected is based on the PMV instance's root (boot) volume.

   - **Anti-affinity**: Use this option to specify one or more existing VSIs or one or more volumes as the anti-affinity objects. The new volume is created in a different storage pool than the storage pool where one or more anti-affinity objects reside.

    For more information about affinity and anti-affinity policies, see [What does it mean to set an affinity or anti-affinity rule?](/docs/power-iaas?topic=power-iaas-powervs-faqs#affinity).

    In the API, for create volume feature the properties `antiAffinityVMInstances` and `antiAffinityVolumes` are used to specify anti-affinity objects. You can specify only one object type for affinity or anti-affinity objects, either VSIs or Volumes. For more information about storage volumes APIs, see [Create a new data volume](/apidocs/power-cloud#pcloud-cloudinstances-volumes-post) and [Create multiple data volumes from a single definition](/apidocs/power-cloud#pcloud-v2-volumes-post).
    {: note}

7. Optional: Set **Volume replication with GRS** to on to enable the volume for asynchronous replication. The name of the primary location (data center) is displayed. From the **Secondary data center** list, select the required secondary location.

    If the **Mixed storage pools in virtual server instances** warning message is displayed, select the following checkboxes:
    - *I acknowledge snapshots and clones will fail when performed on a set of volumes that are on mixed pools*.
    - *I acknowledge volume replication across mixed storage pools will require managing multiple volume replication groups when enabled*.

8. Click the terms and conditions link to read the [IBM Cloud Terms of Use](/docs/overview?topic=overview-terms). To continue, select the **I agree to the Terms and conditions** checkbox and then click **Create and Attach**.


You can create a storage volume by specifying any name of your choice. If you want to reuse the storage volume name, you must delete the existing storage volume with the same name. If the existing volume is a replication-enabled volume, follow the steps to [delete a primary volume](/docs/power-iaas?topic=power-iaas-getting-started-GRS#delete-prime-vol). After you delete the original volume, you must allow a minimum of one hour to create a new volume with the same name.
{: note}

You can create a replication-enabled volume from any site. The site from which the replication is initiated contains what is referred to as the `primary volume`; the remote site volume is referred to as the `auxiliary volume`. For more information, see [Global Replication Services (GRS)](/docs/power-iaas?topic=power-iaas-getting-started-GRS). The GRS details of the volume are displayed when you click the storage volume.

The primary volume and the auxiliary volume are mapped into one-to-one relationship mode in both directions. These two sites are fixed and are in replication partnership in both directions. For more information, see [Setting up GRS](/docs/power-iaas?topic=power-iaas-getting-started-GRS#configure-GRS).
{: note}

For more information about updating the volume groups for GRS, see [Updating a volume group](/docs/power-iaas?topic=power-iaas-getting-started-GRS&q=deleting+a+volume&tags=power-iaas#update-vol-grp).



Verify that the action that you perform on a volume group meets the current state of the volume group. Otherwise, an error message appears indicating that the volume group is not in the expected state.
{: attention}

The error message appears when you perform the following actions:
- Stop a volume group when the `ReplicationStatus` is in the `disabled` state.
- Start a volume group when the `ReplicationStatus` is in the `enabled` state or `available` state.
- Reset a volume group that is not in the error state.




### Detaching storage volumes from a VSI
{: #detaching-volumes}

If you want to detach storage volumes from a VSI, complete the following steps:

1. On the **Storage** tab, select the storage volumes that you want to detach from the Storage volumes section.

2. Click **Detach**. The **Confirm detach** dialog is displayed.

    Detached volumes are not deleted. Volumes must be deleted to stop charges from incurring.To delete a volume, see [Deleting a volume](#deleting-volume).
    {: note}

3. To confirm, click **Detach**.

    The user interface might display a failure message when you attempt to detach a volume from a virtual server instance. In such cases, you need to reload the page after a brief delay to see whether the volume is successfully detached. Make another detach request if the volume is still not disconnected.
    {: note}

### Resizing a storage volume
{: #resizing-volume}
{: help}
{: support}

You can resize a storage volume after its initial creation. However, resizing is not immediately available after you deploy a VSI.

For more information about resizing a replication-enabled volume, see [Updating a primary volume](/docs/power-iaas?topic=power-iaas-getting-started-GRS&q=deleting+a+volume&tags=power-iaas#update-prime-vol).

[{{site.data.keyword.off-prem}}]{: tag-blue} For IBM i 7.3 and later versions, you can resize a volume to increase the volume size, but this action requires an initial program load (IPL) to recognize the new volume size.

Before you perform the IPL operation, you must run the macro to ensure that the volume resize operation is complete, then proceed with the IPL operation. For more information, see [Dynamically increasing the size of a SAN LUN](https://www.ibm.com/support/pages/dynamically-increasing-size-san-lun){: external}. If you do an IPL operation before the resize operation is complete, an extra IPL is required.
{: important}

If you cannot accommodate downtime, you can add extra volumes. You can attach a maximum of 127 volumes to the VSI.

[{{site.data.keyword.off-prem}}]{: tag-blue} Any volume that is included in a snapshot cannot be resized. To resize a volume that is included in a snapshot, you must first delete all the snapshots the volume is a part of.
{: important}

To resize a storage volume after its creation, complete the following steps:

1. Open the {{site.data.keyword.powerSys_notm}} user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.

2. Click **Workspaces** in the navigation panel. The Workspaces page with a list of existing workspaces is displayed.

3. Select the workspace which contains the virtual server instance that you want modify to resize its storage volumes. The Workspace details panel is displayed.

4. Click **View virtual servers**. The Virtual server instances page is displayed.

5. Select the VSI with the attached storage volume that you want to resize. The Virtual server instance details page is displayed for the selected VSI.

6. Click the **Storage** tab.

7. From the Storage volumes section, click the overflow menu (⋮) on the volume entry that you want to resize and select **Edit**. The Edit storage volume panel is displayed.

8. You can specify a new name, storage tier, and size for the storage volume.

    The size of a volume cannot be decreased once it is created. The maximum size of a volume that can be created is 72551 GB.
    {: note}

9. Optional: Set either the Shareable or Bootable property of the storage volume to **On**. You cannot set both the options to **On** at the same time.

10. Click the terms and conditions link to read the [IBM Cloud Terms of Use](/docs/overview?topic=overview-terms). To continue, select the **I agree to the Terms and conditions** checkbox and click **Save**.

In an AIX VSI, if you resize your boot storage volume, run the `chvg -g rootvg` command.
{: note}


### Deleting a volume
{: #deleting-volume}
{: help}
{: support}

When you modify a VSI to update its configuration, you can use the **Storage** tab only to detach a storage volume from the VSI, not to delete it. Detached volumes are not deleted. To delete a storage volume, complete the following steps:

1. Open the {{site.data.keyword.powerSys_notm}} user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.

2. Click **Workspaces** in the navigation panel. The Workspaces page with a list of existing workspaces is displayed.

3. Select the workspace which contains the storage volume that you want delete. The Workspace details panel is displayed.

4. Click **View virtual servers**. The Virtual server instances page is displayed.

5. In the navigation panel, click **Storage** > **Storage volumes**. The Storage volumes page is displayed with a list of existing storage volumes on the **Volumes** tab.

6. Click the overflow menu (⋮) on the volume entry that you want to delete and select **Delete**. The Confirm delete dialog is displayed.

7. To continue, click **Delete**.

    You cannot recover a storage volume after it is successfully deleted.
    {: note}

To delete a volume or a replication-enabled primary volume, the status of the storage volume must be `available`, `error`, `error_restoring`, `error_extending`, or `error_managing`. Also, the storage volume cannot be deleted if it is in the state of migrating, attached, belongs to a group, has snapshots, or is disassociated from its snapshots after a transfer.
{: note}

For more information about deleting a primary volume, see [Deleting a primary volume](/docs/power-iaas?topic=power-iaas-getting-started-GRS#delete-prime-vol).



## Deleting a virtual server instance
{: #deleting-virtual-server-instance}
{: help}
{: support}

You must delete a virtual server instance manually. To delete all virtual server instances, delete the workspace or delete a subset of the virtual server instance.

To delete a single virtual server instance, complete the following steps:


1. On the **Virtual server instances** page, click the overflow menu (⋮) at the end of the virtual server instance entry and select **Delete**. The **Delete virtual server instance** confirmation dialog is displayed.<br>

    Or <br>

   On the **Virtual server instances** page, select the virtual server instance that you want to delete. The **Virtual server instance details** page is displayed. Click the **delete** icon on the upper right of the screen. The **Delete virtual server instance** confirmation dialog appears.

2. On the confirmation dialog, set **Delete data volumes attached to this instance** to on to agree to the following:
    - To delete the data volumes that are attached to the virtual server instance. The data volumes are not deleted if they are attached to multiple virtual server instances.
    - To delete any auxiliary volumes on the secondary site.

3. To confirm, type the virtual server instance name in the text field.

4. Click **Delete virtual server instance** to initiate the deletion request.

You cannot recover a virtual server instance after it is successfully deleted.
{: note}



You cannot delete a virtual server instance if it has one or more associated snapshots. You must first delete all associated snapshots before you can delete the virtual server instance. For more information about how to delete a snapshot, see [Deleting a snapshot](/docs/power-iaas?topic=power-iaas-snapshots-cloning#delete-snapshot).
{: important}



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

[{{site.data.keyword.off-prem}}]{: tag-blue} For an IBM i VM, the SRC number can be progress code, operation code, or software code. For more information, see the [System Reference Code list](https://www.ibm.com/support/knowledgecenter/ssw_ibm_i_73/rzahb/rzahbsrclist.htm){: external} in the IBM i documentation. For AIX VSIs, the SRC numbers are progress codes that provide information about the stages that are involved in powering on and performing initial program load (IPL). AIX SRCs refresh once in 2 minutes. For more information, see [AIX IPL progress codes](https://www.ibm.com/support/knowledgecenter/POWER9_REF/p9eai/aixIPL_info.htm){: external}.


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
