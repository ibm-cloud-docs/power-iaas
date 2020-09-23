---

copyright:
  years: 2019, 2020

lastupdated: "2020-09-23"

keywords: volume snapshot, clone, restore, api, flashcopy

subcollection: power-iaas

---

{:new_window: target="_blank"}
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
{:help: data-hd-content-type='help'}
{:support: data-reuse='support'}

# Snapshotting, cloning, and restoring
{: #volume-snapshot-clone}

The {{site.data.keyword.powerSysShort}} service provides the capability to capture full, point-in-time copies of entire logical volumes or data sets. Using IBM's *FlashCopy* feature, the [Power Systems Virtual Server API](https://cloud.ibm.com/apidocs/power-cloud#introduction) lets you create delta snapshots, volume clones, and restore your disks.

<!-- !The {{site.data.keyword.powerSys_notm}} snapshot, clone, and restore capabilities are currently available only in *DAL13*, *WDC*, *FRA04*, and *FRA05*.
{: preview} -->

<!-- ![Snapshot and clone API use cases](./images/snapshot-clone-use-cases.png "Snapshot and clone API use cases"){: caption="Figure 1. Snapshot and clone API use cases" caption-side="bottom"} -->

## Taking a snapshot
{: #volume-snapshot}

The snapshot interface allows you to create a relationship between your source disks and a target disks (target disks are created as part of the snapshot API) at time **T1**. The snapshot API tracks the delta changes done to the source disk beyond time **T1**. This enables the user to restore the source disks to their **T1** state at later point in time.

There are several use cases for the snapshot feature. For example, an administrator plans to upgrade the middleware on his system but would like to be able to revert to its original state before proceeding with an upgrade. If the middleware fails, the administrator can restore the source disk to its previous state. To accomplish this, the administrator would perform the following steps:

1. Initiate the snapshot API with the source disks where the middleware information resides.
2. Upgrade the middleware.
3. If the upgrade fails, restore the source disks by using the snapshot created in the previous step.
4. If the upgrade succeeds, delete the snapshot created in the first step.

You can initiate multiple snapshot operations. However, these concurrent snapshot operations occur on a different set of disks.
{: note}

**Best practices**

- Before you take a snapshot, ensure that all of the data is flushed to the disk. If you take a snapshot on a running virtual machine (VM) and did not flush the file system, you might lose some content that is residing in memory.
- It is recommended that you quiesce all of the applications on the snapshot volume.

**Use cases**

- Taking a snapshot of a VM targeting only the boot volume
- Taking a snapshot of a VM targeting only data volumes
- Taking a snapshot of a VM targeting all volumes (both boot and data)
- Taking multiple snapshots of a single VM (the snapshots must be taken one at a time)
- Taking multiple snapshots of different VMs at the same time

**Restrictions and considerations**

- Parallel VM snapshot operations from different VM nodes for the same shared volume are not allowed.
- You cannot restore a VM if you are taking a snapshot and there are clone (full-copy) *FlashCopy* operations that are running in the background. The *FlashCopy* operations must first complete.
- Some of the attributes of source disks cannot be changed while the disks are in a snapshot relationship. For example, you cannot resize the source disks when there are snapshot relationships in place for those disks.
- Volumes that are in a snapshot relationship cannot be detached from the VM.

## Cloning a volume
{: #cloning-volume}

Cloning a volume creates a full copy of the volume. You can select multiple volumes and initiate a group clone. When multiple volumes are selected, the clone operation ensures that a consistent data copy is created.

The clone operation will continue to copy data from the source disks to target disks in the background. Depending on the size of the source disks and the amount of data to copy, the clone operation can take a significant amount of time.<br>

You cannot modify the source or target disk attributes, such as disk size, while the clone operation is in progress.
{: note}

**Best practices**

- It is recommended that you quiesce all of the applications on the volume you wish to clone.

**Use cases**

- Cloning multiple volumes in an available state
- Cloning multiple volumes that are attached to the VM

**Restrictions and considerations**

- When the clone operation is performed on an in-use volume, the {{site.data.keyword.powerSys_notm}} service creates a consistent group snapshot and re-creates the cloned volume copy by using the group snapshot.

<!-- ## clone volume process-limiting the amount of VM quiesce time

Clone volume process breaks the clone volumes API into multiple steps which allows the customer to do preparatory steps which allows ongoing I/O on the source volumes and provides application consistent clones while reducing the VM quiesce time.

### Phase 1: create a new volumes-clone request and initiate the Prepare action

Prepare action does the preparatory work for creating the snapshot volumes to the volumes-clone create API in the doc.

**Requirements**:

- requires a minimum of two volumes.
- requires a minimum of one volume to be in the 'in-use' state.
- requires a unique volumes-clone name.

**Status**:

- Initial status is ‘preparing’ and will transition to the ‘prepared’ when  the Prepare action has successfully completed.

**Failure**:

- If an error occurs during the Prepare action the status will transition to the ‘failed’ state. The error reason can be viewed using the volumes-clone Get Detail or List requests.

**Cancel**:

- A volumes clone request can be cancelled when the volumes-clone request has transitioned to the ‘Prepared’ state. The volumes-clone request will be set to the ‘cancelling’ status.

**Return**:

- A new volumes-clone ID will be generated and returned along with the volumes-clone object.

**Best Practice**:

- The User should manually quiesce the VM before starting Phase 2.

### Phase 2 :Initiate the Start action for a volumes-clone request

Start action starts the consistency group to initiate the flash copy to volumes-clone start API in the doc.

**Requirements**:

- requires the volumes-clone request to be in the ‘prepared’ status.
- the latest volumes-clone request status can be viewed using the get volumes-clone detail request or getting the list of all volumes-clone requests.

**Status**:

- Initial status is ‘starting’ and will transition to the ‘available’ status, group snapshot created. This request is synchronous and when the API call returns to the client the volumes-clone request status will have already transitioned to the ‘available’ status unless an error occurred.

**Failure**:

- if an error occurs during the Start action an error will be returned detailing the error reason with the Start action response.  The status will transition to the ‘failed’ state. The prepared snapshot data will be removed allowing the user to retry cloning the same set of volumes again.

**Cancel**:

- A volumes-clone request can be cancelled when the volumes-clone request is in the
‘Available’ status. The volumes-clone request will be set to the ‘cancelling’ status to the volumes-clone cancel API in the doc.

**Return**:

- Updated volumes-clone request showing the latest status.

**Best Practice**:

- The User should manually un-quiesce the VM before starting Phase 3.

### Phase 3 :Initiate the Execute action for a volumes-clone request

Execute action performs the remaining execution to create the cloned volumes from the available group snapshot to the volumes-clone execute API in the doc.

**Requirements**:

- requires the volumes-clone request to be in the ‘available’ status.

**Status**:

- Initial status is ‘executing’ and will transition to the ‘completed’ status when the Execute Action has successfully completed.

**Failure**:

- If an error occurs during the volume cloning process any artifacts that the  cloning process created will be removed.  The group snapshot will be returned to the ‘available’ state, allowing a user to retry the execute action.

**Cancel**:

- a volumes-clone request can be cancelled when the volumes-clone request is in the ‘Executing’ state. The volumes-clone request will be set to the ‘cancelling’ status.

**Return**:

- updated volumes-clone request showing the latest status.

### Additional volumes-clone APIs that can be used with volumes-clone requests

**Get Detail of a volumes-clone request**:

- The get volumes-clone detail request will return detailed information about the current status of the request and includes the list of source volumes getting cloned as well as the cloned volumes when the Execute action has successfully completed to the get volumes-clone detail API in the doc.

**Get a list of all volumes-clone requests**:

- The get list of volumes-clone requests will provide a list of all volumes-clone requests and the latest Status for each request. The listed information does not provide detailed information about the source or cloned
Volumes to the get list of volumes-clone request API in the doc.

**Cancel a volumes-clone request**

- The volumes-clone Cancel request will perform a removal of the group snapshot and if the volumes-clonerequest is currently in the ‘executing’ status any artifacts that the  cloning process has created will be removed. The initial status will be ‘cancelling’ and will transition to the ‘cancelled’ state when all the cleanup work has completed to the Cancel volumes-clone request API in the doc.

- A volumes-clone request is considered completed when the status has transitioned to one of “completed’, ‘failed’, or ‘cancelled’ status.

**Delete a volume-clone request**

- All volumes-clone request will be returned when calling the get list volumes-clone request API.When a volumes-clone request is no longer needed, the volumes-clone Delete API can be called to remove the data to the delete volumes-clone request API in the doc.

**Requirements**:

- requires the volumes-clone request to be in a finalized status. The finalized statuses includes ‘completed’, ‘failed’, and ‘cancelled’. -->

## Restoring a snapshot
{: #restoring-snapshot}

The restore operation restores all of the volumes that are part of a VM snapshot back to the source disks. While it restores the VM, the {{site.data.keyword.powerSys_notm}} service creates a backup snapshot, which can be used if the restore operation fails. If the restore operation succeeds, the backup snapshots are deleted. If the restore operation fails, you can pass in the `restore_fail_action` query parameter with a value of `retry` to retry the restore operation. To roll back a previous disk state, you can pass in the `restore_fail_action` query parameter with a value of `rollback`. When the restore operation fails, the VM enters an **Error** state.

**Best practices**

During the restore operation, **it is critical that your source disks be quiesced**. Your source disks cannot be in use. Shut down all of your applications, including file systems and volume managers. If you are running an AIX VM, make sure that the disks are freed from the LVM by varying it off.

If you plan to restore the boot disks, **your VM must be shut down**. If the VM has volumes that are hosting external database applications, quiesce all of your applications and ensure that there are no active IO transactions on the disk. Failure to do so can lead to data corruption and put the VM in maintenance mode.

**Use cases**

- Restoring all of the volumes that are part of a VM snapshot
- Running multiple VM restore operations
- Retrying a VM restore operation if it originally failed
- Rolling back a VM to its original volume state

**Restrictions and considerations**

- If the restore operation fails, reach out to your storage support administrator. A failed restore operation can leave behind incomplete states, which might require a cleanup initiative from an IBM operation's team.
- If you choose to restore a shared volume on one VM, you cannot perform the snapshot, restore, clone, or capture operations on the other VMs that are using the shared volume (while the restore operation is running).

<!-- ## Cloning a VM
{: #cloning-vm}

You can clone the entire source VM and deploy a target VM (based on the source VM). When doing so, you can customize the network information and VM resource configuration (CPU, memory, shared volumes, etc.).

You can perform only a limited number of concurrent VM clone operations. If you get an error message, wait a few minutes and try again.
{: important} -->
