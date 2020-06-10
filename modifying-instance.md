---

copyright:
  years: 2019, 2020

lastupdated: "2020-04-10"

keywords: storage volume, new storage size, modifying server, editing volume, volume modification, DLPAR, modifying instance, scaling vm, public network, nic, affinity

subcollection: power-iaas

---

{:new_window: target="_blank"}
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

    If the VM is inactive, you can change the processor type to **Dedicated processor**, **Uncapped shared processor** or **Capped shared processor** and adjust the amount of memory however you'd like. The minimum and maximum values for **Memory (GB)** and **Entitled capacity** are recalculated based on the type of processor. When you choose to resize an active VM, you cannot change the processor type. The minimum amount of **Memory (GB)** and **Entitled capacity** are half of what was allocated at provisioning time, while their maximum amounts are double.
    {: tip}

    <!-- ![Modifying your server details](./images/console-modify-server-details.png "Modifying your server details"){: caption="Figure 2. Modifying your server details" caption-side="bottom"} -->

4. Check the service agreement box and click **Order** to complete the instance modification process and accept the price.

5. View the **Server details** pane to verify your instance modification.

## Managing your storage volumes
{: #modifying-volume-network}

Learn how to add new storage volumes and modify existing ones. Currently, you cannot mix **Tier 1** and **Tier 3** storage types.

### Adding and managing storage volumes
{: #adding-managing-volume}

If you'd like to attach or detach a volume, click **Manage existing volumes** and select the wanted volume. You can also change the boot status of a volume by clicking the **Bootable** toggle. To add a volume, you must complete the following steps:

1. Click **New volume** to add a storage volume.

2. Enter the **Name**, **Type**, and **Size** of the storage volume. You can also select whether to make it **Shareable** and set an **Affinity policy**.

    Volume affinity allows you to control the placement of a new volume in a particular storage provider based on an existing volume. When you set an affinity policy for a new storage volume, the volume is created within the same storage provider as an existing volume. With an anti-affinity policy, the new volume is created in a different storage provider as an existing volume.
    {: note}

3. Click **Next**, agree to the service agreement, and submit your **Order**.

<!-- ![Managing your existing volumes](./images/console-modify-attached-volume.png "Managing your existing volumes"){: caption="Figure 3. Managing your existing volumes" caption-side="bottom"} -->

### Resizing a storage volume
{: #resizing-volume}
{: help}
{: support}

You can resize a storage volume after its initial creation. To delete a volume, its status must indicate one of the following states: `available`, `error`, `error_restoring`, `error_extending`, or `error_managing`. Additionally, the storage volume cannot be deleted if it is migrating, attached, belongs to a group, has snapshots, or is disassociated from its snapshots after a transfer. Resizing is not immediately available after you deploy a VM.

Any volume that has been included in a snapshot cannot be resized. To resize a volume that has been included in a snapshot, you must first delete all of the snapshots the volume is a part of.
{: important}

1. Go to the {{site.data.keyword.powerSys_notm}} user interface and click **Storage volumes**.

2. Click the **Edit** icon to the right of your storage volume.

3. After you click the **Edit** icon, a menu appears. Select the wanted storage volume size. You can increase only the size of the storage volume.

    ![Modifying your storage volume](./images/console-modify-volume.png "Modifying your storage volume"){: caption="Figure 2. Modifying your storage volume" caption-side="bottom"}

4. Read the service agreement and agree to the terms. Click **Order** to complete the volume modification process and accept the price.

5. To verify your new storage size, go back to **Storage volumes**.

## Adding or removing a public network
{: #adding-removing-network}

You can remove or add a public network by clicking the **Public networks** toggle in **Virtual server instances**. When you toggle a public network off and then on, the {{site.data.keyword.powerSys_notm}} user interface regenerates new internal and external IP addresses. You need to check the {{site.data.keyword.powerSys_notm}} user interface for the new internal IP address (that maps to the external IP address). You must add a network interface controller (NIC) and point it to the new internal IP address. For information on how to add or remove an interface, see [How to add or remove a network interface from an AIX virtual machine (VM)](/docs/power-iaas?topic=power-iaas-managing-network-interface) or [How to add or remove a network interface from an IBM i virtual machine (VM)](/docs/power-iaas?topic=power-iaas-managing-network-interface-ibmi).

You cannot toggle a public network off if there are no other defined networks.
{: note}

<!-- ![Toggling a public network on or off](./images/console-public-network-toggle.png "Toggling a public network on or off"){: caption="Figure 4. Toggling a public network on or off" caption-side="bottom"} -->
