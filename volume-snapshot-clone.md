---

copyright:
  years: 2023, 2024

lastupdated: "2024-10-06"

keywords: cloning and restoring snapshots, power virtual server as a service, private cloud, snapshots, clone API

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Snapshots, cloning, and restoring
{: #snapshots-cloning}

---

IBM {{site.data.keyword.powerSys_notm}} located in IBM data centers: [Off-premises]{: tag-blue}

IBM {{site.data.keyword.powerSys_notm}} Private Cloud: [On-premises]{: tag-red}

---

{{site.data.keyword.powerSysFull}} provides the capability to capture full, point-in-time copies of entire logical volumes or data sets. Using IBM's *FlashCopy* feature, {{site.data.keyword.powerSysShort}} APIs you can create delta snapshots, volume clones, and restore your disks.

**APIs to create snapshot and clone**
- [Create a new volume clone request and initiates the Prepare action](/apidocs/power-cloud#pcloud-v2-volumesclone-post)
- [Create a PVM Instance snapshot](/apidocs/power-cloud#pcloud-pvminstances-snapshots-post)

**CLIs to create snapshot and clone**
- [Create a snapshot](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#ibmcloud-pi-snapshot-create)
- [Create a volume clone for specific volumes](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#ibmcloud-pi-volume-create-clone)


## Taking a snapshot
{: #volume-snapshot}

With the snapshot interface you can create a relationship between your source disks and a target disks (target disks are created as part of the snapshot API) at time **T1**. The snapshot API tracks the delta changes done to the source disk beyond time **T1**. Thus, you can restore the source disks to their **T1** state at a later point in time.

There are several use cases for the snapshot feature. For example,
- An administrator plans to upgrade the middleware but would like to be able to revert to its original state before proceeding with an upgrade.
- If the middleware fails, the administrator can restore the source disk to its previous state. To accomplish this, the administrator would perform the following steps:

1. Initiate the snapshot API with the source disk where the middleware information resides.
2. Upgrade the middleware.
3. If the upgrade fails, restore the source disks by using the snapshot that is created in the previous step.
4. If the upgrade succeeds, delete the snapshot that is created in the first step.

You can initiate multiple snapshot operations. However, these concurrent snapshot operations occur on a different set of disks.
{: note}

### Metering and pricing of snapshot
{: #metering-snapshot}

Each snapshot that you create is monitored every hour and charged depending on the disk space that is requested for the snapshot. The space that is used by a snapshot is charged at 30% of the base rate. For example, if you have **M** disks on a VM that add up to 600 GB of space, and those **M** disks are used as source disks for snapshots, the following charges are applicable:

- If you create one snapshot, you are charged for the disk space that is used by the base 600 GB of **M** disks plus 30% of 600 GB of disk space. That is, 600 GB (space of M disks) + 180 GB (30% of 600 GB) = 780 GB of disk space.
- If you create one more snapshot by using same disks, you are charged for disk space that is used by **M** disks (600 GB) + (30% of 600 GB) + (30% of 600 GB) = 960 GB of disk space.
- The pricing that is charged for the snapshot is based on the storage tier that contains the source volumes: Tier 1 or Tier 3.

### Best practices
{: #best-practice1}

- Before you take a snapshot, ensure that all of the data is flushed to the disk. If you take a snapshot on a running virtual machine (VM) and did not flush the file system, you might lose some content that is residing in memory.
- It is recommended that you quiesce all of the applications on the snapshot volume.

### Use cases
{: #use-case1}

- Taking a snapshot of a VM targeting only the boot volume
- Taking a snapshot of a VM targeting only data volumes
- Taking a snapshot of a VM targeting all volumes (both boot and data)
- Taking multiple snapshots of a single VM (the snapshots must be taken one at a time)
- Taking multiple snapshots of different VMs at the same time

### Restrictions and considerations
{: #restrict-consider1}

- Parallel VM snapshot operations from different VM nodes for the same shared volume are not allowed.
- You cannot restore a VM if you are taking a snapshot and there are clone (full-copy) *FlashCopy* operations that are running in the background. The *FlashCopy* operations must first be complete.
- Some of the attributes of source disks cannot be changed while the disks are in a snapshot relationship. For example, you cannot resize the source disks when there are snapshot relationships in place for those disks.
- Volumes that are in a snapshot relationship cannot be detached from the VM.

## Cloning a volume
{: #cloning-volume}

The clone operation creates a full copy of the volume. You can select multiple volumes and initiate a group clone operation. When multiple volumes are selected, the clone operation ensures that a consistent data copy is created.

The clone operation continues to copy data from the source disks to target disks in the background. Depending on the size of the source disks and the amount of data to be copied, the clone operation can take a significant amount of time.

You cannot modify the source or target disk attributes, such as disk size, while the clone operation is in progress.
{: note}

**Best practice**: Quiesce all of the applications on the volume that you want to clone.

**Use case**: You can perform the clone operation on multiple volumes that are attached to the VM and that are in an available state.

**Restrictions and considerations**: When the clone operation is performed on a volume that is in-use, {{site.data.keyword.powerSys_notm}} creates a consistent group snapshot and re-creates the copy of the cloned volume by using the group snapshot.

**Steps**: Doing the clone operation on a volume consists of three steps: prepare, start, and run the volumes-clone request. These steps allow you to perform preparatory actions and to authorize the ongoing I/O operations on the source volumes. Breaking the clone operation on a volume into multiple steps provides consistent clones and reduces the VM quiesce time. The clone operation on a volume consists of the following steps:

When any of the prepare, start, or clone steps fails then first perform the cancel clone step and then re-run all the three steps.
{: important}

### 1. Create a volumes-clone request and initiate the Prepare action
{: #create-vol-clone req}

- **Requirements**
    - A minimum of two volumes
    - A minimum of one volume to be in the **in-use** state
    - A unique volumes-clone name

- **Status change**
    When the preparatory actions are initiated, the initial status of the volume clone request is set to **Preparing**. When the preparatory actions are completed successfully, the status changes to **Prepared**. If an error occurs during the preparatory actions, the status changes to **Failed**. You can view the reasons for the failure by using the [get volumes-clone detail](https://cloud.ibm.com/apidocs/power-cloud#pcloud-v2-volumesclone-get) request or the [get volumes-clone list](https://cloud.ibm.com/apidocs/power-cloud#pcloud-v2-volumesclone-getall) request.

    If you cancel the volumes-clone request, the status is changed to **Cancelling**. You can cancel a volumes-clone request only when the volumes-clone request status is changed to **Prepared** state.

- **Output**
    A new volumes-clone ID is generated along with the volumes-clone object.

### 2. Start the volumes-clone request
{: #start-vol-clone-req}

This step allows the consistency group to initiate the FlashCopy operation. As a best practice, you must manually quiesce the VM before you initiate the start action of a volumes-clone request.

- **Requirements**
    The volumes-clone request must be in the **Prepared** state.

- **Status change**
    You can view the latest volumes-clone request status by using the [get volumes-clone detail](https://cloud.ibm.com/apidocs/power-cloud#pcloud-v2-volumesclone-get) request or the [get volumes-clone list](https://cloud.ibm.com/apidocs/power-cloud#pcloud-v2-volumesclone-getall) request. When the volumes-clone request is initiated, the initial status is set to **Starting**. When the group snapshot is created, the request status changes to **Available**. The start action of the volumes-clone request is synchronous and when the API call returns to the client, the volumes-clone request status changes to **Available** unless an error occurs. If an error occurred during the start action, the status of the volume-clone request changes to **Failed**. The reason for failure is specified in the error that is returned with the start action response. The prepared snapshot data is removed so that you can clone the same set of volumes again. If you cancel the start action of a volumes-clone request, the status of the volumes-clone request changes to **Cancelling**. You can cancel a volumes-clone request when the volumes-clone request is in the **Available** state.

- **Output**
    The volumes-clone request is updated to **view the status**.

### 3. Run the volumes-clone request
{: #execute-vol-clone}

Performs the remaining execution action to create the cloned volumes from the available group snapshot. As a best practice, you must manually unquiesce the VM before you initiate the run action of a volumes-clone request.

- **Requirements**
    The volumes-clone request must be in the **available** status.

- **Status change**
    If the run action of a volumes-clone request is initiated, the initial status is set to **Executing**. When the run action is completed successfully, the request status changes to **Completed**. If an error occurs during the volume cloning process, any artifacts that are created by the cloning process are removed. The group snapshot is returned to the **Available** state so that you can retry the run action. If you cancel the run action of a volumes-clone request, the status of the volumes-clone request is changed to **Cancelling**. You can cancel a volumes-clone request when the volumes-clone request is in the **Executing** state.

    A volumes-clone request is considered complete when the status of the volumes-clone request is changed to one of the **Completed**, **Failed**, or **Cancelled** state.

- **Output**
    The volumes-clone request is updated to **view the current status**.

#### Additional volumes-clone APIs that can be used with volumes-clone requests
{: #add-vol-clone-api}

- **Get details of a volumes-clone request**

    This API request returns detailed information about the status of the volume-clone request. For example, the list of source volumes that are getting cloned and the list of cloned volumes when the run action is successfully completed.

- **Get a list of all volumes-clone requests**

    The API request provides a list of all volumes-clone requests and the latest status for each request. The detailed information about the source volumes or cloned volumes is not provided.

- **Cancel a volumes-clone request**

    This API request removes the group snapshot. If the volumes-clone request is in the **Executing** state, any artifacts that are created by the clone operation process are removed. If you cancel the volumes-clone request, the initial status of the volumes-clone request is set to **Cancelling**. The status changes to **Cancelled** state when all the clean-up work is completed successfully.

- **Delete a volume-clone request**

    When a volumes-clone request is not required any longer, you can call the **volumes-clone delete** API to remove the data. You can delete a volumes-clone request only when the request status is in one of the finalized statuses: **Completed**, **Failed**, or **Cancelled** state.

## Restoring a snapshot
{: #restoring-snapshot}

The restore operation restores all of the volumes that are part of a VM snapshot back to the source disks. While it restores the VM, {{site.data.keyword.powerSys_notm}} creates a backup snapshot, which can be used if the restore operation fails. If the restore operation succeeds, the backup snapshots are deleted. If the restore operation fails, you can pass in the `restore_fail_action` query parameter with a value of `retry` to retry the restore operation. To roll back a previous disk state, you can pass in the `restore_fail_action` query parameter with a value of `rollback`. When the restore operation fails, the VM enters an **Error** state.

### Best practices
{: #best-practice-vol}

During the restore operation, **it is critical that your source disks be quiesced**. Your source disks cannot be in use. Shut down all of your applications, including file systems and volume managers. If you are running an AIX VM, make sure that the disks are freed from the LVM by varying it off.

If you plan to restore the boot disks, **your VM must be shut down**. If the VM has volumes that are hosting external database applications, quiesce all of your applications and ensure that there are no active IO transactions on the disk. Failure to do so can lead to data corruption and put the VM in maintenance mode.

### Use cases
{: #use-case-vol}

- Restoring all of the volumes that are part of a VM snapshot
- Running multiple VM restore operations
- Retrying a VM restore operation if it originally failed
- Rolling back a VM to its original volume state

### Restrictions and considerations
{: #restrict-consider}

- If the restore operation fails, reach out to your storage support administrator. A failed restore operation can leave behind incomplete states, which might require a cleanup initiative from an IBM operation's team.
- If you choose to restore a shared volume on one VM, you cannot perform the snapshot, restore, clone, or capture operations on the other VMs that are using the shared volume (while the restore operation is running).
- If you encounter a failure while submitting multiple volume clone requests on the same volume, you should either delete any previous requests or start and run the previous volume clone request.

## Frequently asked questions
{: #snap-clone-faqs}

Here are some of the following frequently asked questions on snapshots and clonning that are documented on the FAQ page:
- [What are the key differences between a snapshot and a clone?](/docs/power-iaas?topic=power-iaas-powervs-faqs#snap-vs-clone)
- [Is there any UI to perform snapshot or clone operations?](/docs/power-iaas?topic=power-iaas-powervs-faqs#snap-clone-ui)
- [Are there any initial snapshot requirements in terms of storage?](/docs/power-iaas?topic=power-iaas-powervs-faqs#snap-storage-req)
- [Does the snapshot and volume clone support any safeguard policy?](/docs/power-iaas?topic=power-iaas-powervs-faqs#snap-clone-safeguard)
- [Can you tell me more about the backup process by using the PowerHA Toolkit for IBM i?](/docs/power-iaas?topic=power-iaas-powervs-faqs#poweha-toolkit)
