---

copyright:
  years: 2019

lastupdated: "2019-11-18"

keywords: network inteface, AIX cloud VM, ifconfig, detach, en0, rmdev, external IP address

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

# How to add or remove a network interface from an AIX virtual machine (VM)
{: #managing-network-interface}

 You must remove and readd the AIX VM network interface if you choose to disconnect the {{site.data.keyword.powerSys_notm}} AIX VM from a public network.
{: shortdesc}

1. Use the `ifconfig` command to remove the network interface from the AIX VM. In the following example, *en0* is the public inteface.

    ```
    ifconfig en0 down detach
    ```
    {: codeblock}

2. Next, run the `rmdev` command to remove the device from the AIX system.

    ```
    rmdev -dl en0
    ```
    {: codeblock}

3. To readd the *en0* network interface and point it to the new external instance IP address, enter the following command:

    Since Version 1.2.2, IBM PowerVC can dynamically add a network interface controller (NIC) to a VM or remove a NIC from a VM. IBM PowerVC does not set the IP address for new network interfaces that are created after the machine deployment. Any removal of a NIC results in freeing the IP address that was set on it.
    {: note}

    ```
    ifconfig en0 169.47.176.8
    ```
    {: codeblock}

    ![Finding your external IP address](./images/console-external-ip.png "Finding your external IP address"){: caption="Figure 1. Finding your external IP address" caption-side="bottom"}
