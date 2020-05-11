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
{:preview: .preview}
{:external: target="_blank" .external}
{:help: data-hd-content-type='help'}
{:support: data-reuse='support'}

# Snapshotting, cloning, and restoring
{: #volume-snapshot-clone}

The {{site.data.keyword.powerSysShort}} service provides the capability to capture full, point-in-time copies of entire logical volumes or data sets. Using IBM's *FlashCopy* feature, the {{site.data.keyword.powerSys_notm}} API lets you create delta snapshots, volume clones, and restore your disk if needed.

The {{site.data.keyword.powerSys_notm}} snapshot, clone, and restore capabilities are currently available only in *DAL13*.
{: preview}

![Snapshot and clone API use cases](./images/snapshot-clone-use-cases.png "Snapshot and clone API use cases"){: caption="Figure 1. Snapshot and clone API use cases" caption-side="bottom"}

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

**Best Practices**

- Before you take a snapshot, ensure that all of the data is flushed to the disk. If you take a snapshot on a running virtual machine (VM) and did not flush the file system, you might lose some content that is residing in memory.

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

As soon as the call returns, you can start using the target disks. The clone operation will continue to copy data from the source disks to target disks in the background. Depending on the size of the source disks and the amount of data to copy, the clone operation can take a significant amount of time.

You cannot modify the source or target disk attributes, such as disk size, while the clone operation is in progress.
{: note}

**Use cases**

- Cloning multiple volumes in an available state
- Cloning multiple volumes that are attached to the VM

**Restrictions and considerations**

- When the clone operation is performed on an in-use volume, the {{site.data.keyword.powerSys_notm}} service creates a consistent group snapshot and re-creates the cloned volume copy by using the group snapshot.

## Cloning a VM
{: #cloning-vm}

You can clone a VM by using the {{site.data.keyword.powerSys_notm}} API. By cloning a VM, you create a replica of an existing VM with the same configuration (processor, memory, volumes cloned, etc.).

## Restoring a VM
{: #restoring-vm}

The restore operation restores all of the volumes that are part of a VM snapshot back to the source disks. While it restores the VM, the {{site.data.keyword.powerSys_notm}} service creates a backup snapshot, which can be used if the restore operation fails. If the restore operation succeeds, the backup snapshots are deleted. If the restore operation fails, you can pass in the `restore_fail_action` query parameter with a value of `retry` to retry the restore operation. To roll back a previous disk state, you can pass in the `restore_fail_action` query parameter with a value of `rollback`. When the restore operation fails, the VM enters an **Error** state.

**Prerequisites**

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
