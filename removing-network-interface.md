---

copyright:
  years: 2019, 2020

lastupdated: "2020-04-10"

keywords: network interface, NIC, AIX VM, ifconfig command, detach, en0, rmdev, external IP address, smitty mktcpip, namerslv command

subcollection: power-iaas

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:external: .external}
{:help: data-hd-content-type='help'}
{:support: data-reuse='support'}

# How to add or remove a network interface from an AIX virtual machine (VM)
{: #managing-network-interface}

Since IBM PowerVC Version 1.2.2, IBM PowerVC can dynamically add a network interface controller (NIC) to a VM or remove a NIC from a VM. IBM PowerVC does not set the IP address for new network interfaces that are created after the machine deployment. Any removal of a NIC results in freeing the IP address that was set on it.  You must remove and readd the AIX VM network interface if you choose to disconnect the {{site.data.keyword.powerSys_notm}} AIX VM from a public network.
{: shortdesc}

When you toggle a public network off and then on, the {{site.data.keyword.powerSys_notm}} user interface regenerates new internal and external IP addresses. You need to check the {{site.data.keyword.powerSys_notm}} user interface for the new internal IP address to complete this procedure.
{: note}

## Removing a network interface from an AIX VM
{: #remove-nic-aix}
{: help}
{: support}

1. Use the `ifconfig` command to remove the network interface from the AIX VM. In the following example, *en0* is the public interface.

    ```
    ifconfig en0 down detach
    ```
    {: codeblock}

2. Next, run the `rmdev` command to remove the device from the AIX system.

    ```
    rmdev -dl en0
    ```
    {: codeblock}

3. Use the `cfgmgr` command to reconfigure the device.

## Adding a network interface to an AIX VM
{: #add-nic}

When you toggle a public network off and then on, a new Virtual Ethernet Adapter (VEA) is created on your VM. You must identify the network interface that the new VLAN is associated with before reconfiguring the IP adress.

Every time you toggle a public network off and then on, the system creates multiple network interfaces. As a result, the `ifconfig -a` command will show several unused network interfaces after toggling the public network. To remove these stale network interfaces, use `ifconfig` and `rmdev` as described in the previous section.
{: note}

1. After you toggle a public network off and then on, look up the list of networks and write down the public network VLAN ID. To find the public network VLAN ID, see [Get a network's current state or information](https://cloud.ibm.com/apidocs/power-cloud#get-a-network-s-current-state-or-information){: new_window}{: external}.

2. Use the `lsdev -Cc adapter` command to generate the list of adapters.

3. Use either the `ifconfig -a` or `netstat -in` command to see all of the network interfaces.

4. To find the network interface that has the public network VLAN ID, enter `entstat -d ent X | grep VLAN` (where *X* is the adapter number).

To add a network interface (for example, *en0*) and point it to the new internal IP address (as shown in the {{site.data.keyword.powerSys_notm}} user interface), you can use `smitty mktcpip`. You can also use the AIX command line to perform the same task by using the [mktcpip command](https://www.ibm.com/support/knowledgecenter/en/ssw_aix_72/m_commands/mktcpip.html){: new_window}{: external} (replacing the values with your own):

```
/usr/sbin/mktcpip -h power-systems-virtual-instance -a 192.168.103.12 -m 255.255.255.240 -i en0 -t N/A -g 192.168.103.1 -D 0.0.0.0
```
{: codeblock}

If you'd like to manipulate domain name server (DNS) entries for local resolver routines in the system configuration database, see the [namerslv command](https://www.ibm.com/support/knowledgecenter/ssw_aix_72/n_commands/namerslv.html){: new_window}{: external}.

## Moving data to the cloud
{: move-data-to-cloud}

Depending on your network bandwidth and size constraints, data moving process is as simple as creating an *OVA* or *mksysb* (root volume group) image, and a set of *savevg* images for data volumes. By using an *OVA* or *mksysb* image, you can build or provision a VM and then proceed to migrate their data volume groups by using the **restvg** command.

Following are the options for backing up data (on premise) and moving the data to IBM {{site.data.keyword.powerSys_notm}}.

### Migrating volume group data using savevg
{: migrate-data-using-savevg}

A volume group is a collection of physical volumes of varying sizes and types. When a physical volume is assigned to a volume group, the physical blocks of storage media on it are organized into physical partitions of a size that you specify when you create the volume group. You can use built-in AIX *savevg* and *restvg* commands to backup and restore non-root volume groups. <!--The *savevg* and *restvg* commands can simplify the creation of your new volume groups and file systems on your new VM.-->

The *savevg* command finds and backs up all the files belonging to a specified volume group. The volume group must be varied-on, and the file systems must be mounted. The *savevg* command uses the data file created by the *mkvgdata* command.

Use the following command to find and backup all the files that belongs to a perticular Volume group (VG).

```
# savevg –f <destination path> -i <non root vg files to be backed up>
```
{: codeblock}

Example:

```
# savevg –f /home/admin01/datavg_bkup –i  datavg
```

### Using *mkvgdata* and *restvg* for multiple volume backups
{: multiple-volume-backups}

Small systems might require only one data volume group to contain all the physical volumes which house non-root volume data. You might want to create separate volume groups, for security reasons, because each volume group can have its own security permissions. Separate volume groups also make maintenance easier because groups other than the one being serviced can remain active.

Run the *mkvgdata* command for each online volume group to generate output for a volume group in `/tmp/vgdata` location. The resulting output is then tar'd and stored in the `/backup` file system directory. This allows information regarding all volume groups, logical volumes, and file systems to be included in a single image. The resulting image can be transferred or even stored within a *mksysb* backup if the `/backup` resides on *rootvg*.

Use the following command to recreate the volume groups, logical volumes and file systems:

```
# tar -xvf /backup/vgdata.tar
```

Now edit `/tmp/vgdata/{volume group name}/{volume group name}.data file` and look for the line with `VG_SOURCE_DISK_LIST=`. Change the line to have the *hdisks*, *vpaths* or *hdiskpowers* based on your requirement.

```
# restvg -r -d /tmp/vgdata/{volume group name}/{volume group name}.data
```

### Migrating raw partitions using dd
{: migrating-raw-partitions}

The output file of *savevg* can be restored by using the *restvg* command. The size of a *savevg* backup file is small in comparison to the size of the physical volume(s) in the volume group. <!-- So, the prescribed method of moving volume data using savevg covers many use cases.  However, there are environments where data is of a magnitude larger than several TBs and may present a disadvantage when considering transference and/or restoration procedures. -->

You can use the *savevg* command to backup volume groups. All logical volume information is archived, as well as JFS and JFS2 mounted file systems. However, *savevg* command cannot be used to backup raw logical volumes.

Use the following methods to backup content of a file system (and to later restore):

- Unmount the file system.
- Save the raw logical volume content into a file by using:
  
  ```
  # dd if=/dev/lvname of=/file/system/lvname.dd
  ```
  {: codeblock}

This creates a copy of logical volume **lvname** to a file **lvname.dd** in file system `/file/system`. Make sure that wherever you write your output file to (in the example above to `/file/system`) has enough disk space available to hold a full copy of the logical volume. If the logical volume is 100 GB, you need 100 GB file system space for the copy.

On the destination server, recreate the logical volume and the file system by using an unmounted file system.

Run the following dd command to restore the backup copy:

```
# dd if=/file/system/lvname.dd of=/dev/lvname
```
{: codeblock}

After you run the dd command, mounting the file system provides access to the contents of the original file system.
