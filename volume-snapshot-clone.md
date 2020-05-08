---

copyright:
  years: 2019, 2020

lastupdated: "2020-05-11"

keywords: volume snapshot, clone, restore

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
{:external: target="_blank" .external}
{:help: data-hd-content-type='help'}
{:support: data-reuse='support'}

# Snapshotting, cloning, and restoring a volume
{: #volume-snapshot-clone}

The {{site.data.keyword.powerSysShort}} service provides storage-based snapshot, restore, and clone capabilities. These interfaces are available as cloud APIs (REST). It is important to note that these operations are initiated on the storage controller and calls return to the user before the are fully completed. For example, an administrator can initiate a clone operation and start utilizing the target disks before the copy procedure (from the source to target disks) is complete. Certain changes or operations are not possible until the clone operation is complete (resizing of the source or target disks is not allowed). To learn more about snapshotting, cloning, and restoring volumes inside the {{site.data.keyword.powerSys_notm}} environment, review the information in this topic.

![Snapshot and clone API use cases](./images/snapshot-clone-use-cases.png "Snapshot and clone API use cases"){: caption="Figure 1. Snapshot and clone API use cases" caption-side="bottom"}

## Taking a snapshot
{: #volume-snapshot}

**Best Practices**

- Before you take a snapshot, ensure that all of the data is flushed to the disk. If you take a snapshot on a running virtual machine (VM) and did not flush the file system, you might lose some content.

**Use cases**

- Taking a snapshot of a VM targeting only the boot volume
- Taking a snapshot of a VM targeting only data volumes
- Taking a snapshot of a VM targeting all volumes (both boot and data)
- Taking multiple snapshots of a single VM (the snapshots must be taken one at a time)
- Taking multiple snapshots of different VMs at the same time

**Restrictions and considerations**

- Parallel VM snapshot operations for the same shared volume are not allowed.
- You cannot restore a VM if you are taking a snapshot and there are clone (full-copy) *FlashCopy* operations that are running in the background. The *FlashCopy* operations must first complete.

## Cloning a volume
{: #cloning-volume}

Cloning a volume creates a full copy of the volume. You can select multiple volumes and attempt a group clone. When multiple volumes are selected, the clone operation ensures that a consistent data copy is created.

**Prerequisites**

You **must** assign a storage template to all of the volumes you select as clone volumes.

**Use cases**

- Cloning multiple volumes in an available state
- Cloning multiple volumes that are attached to the VM

**Restrictions and considerations**

- When the clone operation is performed on an in-use volume, the {{site.data.keyword.powerSys_notm}} service creates a consistent group snapshot and re-creates the cloned volume copy by using the group snapshot.

## Restoring a virtual machine (VM)
{: #volume-restore}

The restore operation restores all of the volumes that are part of a VM snapshot. While restoring the VM, the {{site.data.keyword.powerSys_notm}} service creates a backup snapshot, which can be used if the restore operation fails. If the restore operation succeeds, the backup snapshots are deleted. If the restore operation fails, you can perform the `restore-retry` operation to retry the restore operation. You can also perform the `restore-rollback` operation to roll back to the backup snapshot. When the restore operation fails, the VM enters an **Error** state.

**Prerequisites**

By default, the VM restore operations expect the VM to be **shutoff**. This ensures that there is no data corruption while performing the restore operation. If the VM has volumes that are hosting external database application, quiesce all of your applications and ensure that there are no active IO transactions on the disk. Failure to do this can lead to data corruption and put the VM in maintenance mode.

**Use cases**

- Restoring all of the volumes that are part of a VM snapshot
- Running multiple VM restore operations (considering there are no shared volumes)
- Retrying a VM restore operation if it originally failed
- Rolling back a VM to its original volume state

**Restrictions and considerations**

- If the restore operation fails, reach out to your storage support administrator. A failed restore operation can leave behind incomplete `fcmaps`, which need to be manually cleaned up before you can the `restore-rety` operation.
- If you choose to restore a shared volume on one VM, you cannot perform the snapshot, restore, clone, or capture operations on the other VMs that are using the shared volume (while the restore operation is running).
