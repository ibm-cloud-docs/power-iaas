---

copyright:
  years: 2020, 2021

lastupdated: "2020-04-19"

keywords: aix mksysb, volume group, backup multiple volumes, savevg, dd command

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Moving data from your private cloud environment to {{site.data.keyword.powerSys_notm}}
{: #move-data-to-cloud}

Depending on your network bandwidth and data size constraints, the process of moving the data volume group is as simple as creating an *Open Virtualization Appliance (OVA) file* or an *mksysb* image (root volume group), and creating a set of *savevg* images for volume group data. By using an *OVA* file or an *mksysb* image, you can build or provision a VM and then migrate the data volume groups of the virtual machine (VM) by using the **restvg** command.

You can use the following methods to back up your private cloud data and move the data to {{site.data.keyword.powerSysFull}}.

## Migrating volume group data by using the *savevg* command
{: #migrate-data-using-savevg}

A volume group is a collection of physical volumes of various sizes and types. When a physical volume is assigned to a volume group, the physical blocks of storage media are organized into physical partitions. You can specify the size of the physical partition when you create the volume group. You can use built-in AIX *savevg* and *restvg* commands to back up and restore non-root volume groups. The *savevg* and *restvg* commands simplify the creation of new volume groups and file systems on the new VM.

The *savevg* command finds and backs up all files that belong to a specified volume group. The volume group must be varied-on, and the file systems must be mounted. The *savevg* command uses the data file that the *mkvgdata* command creates.

Use the following command to find and back up all files in a specific volume group.

```text
# savevg –f <destination path> -i <non root vg files to be backed up>
```
{: codeblock}

For example:

```text
# savevg –f /home/admin01/datavg_bkup –i  datavg
```

## Backing up multiple volume groups by using the *mkvgdata* and *restvg* commands
{: #multiple-volume-backups}

Small systems might require only one data volume group to contain all the physical volumes. For a non-root user you might want to create separate volume groups, for security reasons, because each volume group can have its own security permissions. If a volume group stops working, other volume groups remain active. Hence, separate volume groups are easier to maintain.

Run the following commands to back up multiple volume groups:

```text
# lsvg -o | xargs -i mkvgdata {}
# tar -cvf /backup/vgdata.tar /tmp/vgdata
```
{: codeblock}

To generate an output file that contains information about the volume group, run the *mkvgdata* command for each online volume group to generate the output file. This output file is located in the `/tmp/vgdata` directory. You can compress and store this output file in the `/backup` file system directory as shown in the following example. This output file contains information about all volume groups, logical volumes, and file systems that can be used as a single image. This image can be transferred or stored within an *mksysb* backup image if the `/backup` directory is located on the root volume group.

Run the following command to re-create the volume groups, logical volumes, and file systems:

```text
# tar -xvf /backup/vgdata.tar
```

Now edit the `/tmp/vgdata/{volume group name}/{volume group name}.data file` and look for the line with `VG_SOURCE_DISK_LIST=`. Change the line to have *hdisks*, *vpaths*, or *hdiskpowers* based on your requirement.

For example:

```text
# restvg -r -d /tmp/vgdata/{volume group name}/{volume group name}.data
```

## Migrating raw partitions by using the dd command
{: #migrating-raw-partitions}

The output file of the *savevg* command can be restored by using the *restvg* command. The size of a *savevg* backup file is small in comparison to the size of the physical volumes in the volume group. If the environments have several TBs of data, the prescribed method of moving volume group data by using the *savevg* command might present a disadvantage while considering transference and restoration procedures.

You can use the *savevg* command to back up volume groups. All logical volume information, Journaled File System (JFS), and JFS2 mounted file systems are archived. However, you cannot use the *savevg* command to back up raw logical volumes.

Use the following methods to back up and restore contents of a file system:

1. Unmount the file system.
2. Save the raw logical volume content into a file by running the following command:

```code
  # dd if=/dev/lvname of=/file/system/lvname.dd
```


This command creates a copy of the logical volume named **lvname** to a file named **lvname.dd** in file system `/file/system`. Make sure that the specified directory where the output file will be stored (`/file/system` in the example) has enough available disk space to hold a full copy of the logical volume. For example, if the logical volume size is 100 GB, you need 100 GB file system space for the logical volume copy.

On the destination server, re-create the logical volume and the file system. If you are using an unmounted file system, run the following command to restore the backup copy:

```code
# dd if=/file/system/lvname.dd of=/dev/lvname
```

After you run the `dd` command to mount the file system, you can access the contents of the original file system.
