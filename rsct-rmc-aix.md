---

copyright:
  years: 2019, 2020

lastupdated: "2020-03-10"

keywords: rsct, rmc, IPv6

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

# Recommended Reliable Scalable Cluster Technology (RSCT) package levels for imported AIX images
{: #recommended-rsct-package}

RSCT is a set of software components that together provide a comprehensive clustering environment for AIX&reg;, Linux&reg;, Solaris, and Windows&reg; operating systems. RSCT is the infrastructure that is used by various IBM products to provide clusters with improved system availability, scalability, and ease of use. For the {{site.data.keyword.powerSys_notm}} offering, RSCT 3.1 is the minimum package level that is required for an imported AIX image (provides IPv6 support). However, the {{site.data.keyword.powerSys_notm}} development team recommends you use [RSCT 3.2](https://www.ibm.com/support/knowledgecenter/SGVKBA_3.2/navigation/welcome.html){: new_window}{: external} for optimal performance.
{: shortdesc}

The RSCT `nodeid` is not rebuilt if you are deploying an AIX VM from a network installation management (NIM) server without `cloud-init`, and RSCT is installed.
{: important}

## Resource Management Control (RMC)
{: #rmc-aix}

The [RMC subsystem](https://www.ibm.com/support/knowledgecenter/SGVKBA_3.2/admin/bl503_undrmc.html){: new_window}{: external} is the scalable backbone of RSCT that provides a generalized framework for managing resources within a single system or a cluster. Its generalized framework is used by cluster management tools to monitor, query, modify, and control cluster resources. RMC provides a single monitoring and management infrastructure for both RSCT peer domains and management domains.

The AIX VM's RMC status is presented in the {{site.data.keyword.cloud}} dashboard as a health status. The RMC health status can be either **OK** or **Warning**. **Warning** statuses happen when the RMC subsystem between your VM and the management system is not connected.

The RMC connection between your VM and the system management service is configured when you create the AIX VM. When you deploy an AIX VM, the IPv6 management interface is injected into the VM. If you remove or overwrite this interface, an RMC connection is not possible. The following procedures can cause the injected IPv6 management interface to be lost after you deploy the AIX VM:

- You attach a different boot volume to the VM and boot from it
- You use the `mksysb restore` operation from an on-premises VM
- You use `smitty` to remove the IPv6 interface

## Diagnosing and recovering from a missing IPv6 address
{: #rsct-diagnosis-recovery}

One of your AIX VM network interface controllers (NICs) must include an IPv6 address to connect to the Novalink host. If your NIC does not have an associated IPv6 address, you must perform a recovery procedure.

### Diagnosing a missing IPv6 address
{: #diagnosing-ipv6}

Enter the `ifconfig -a` command on your AIX VM terminal. Check to see whether one of your NICs shows an IPv6 address (for example, `2001:1234:5723:ABCD:5678:D14E:DBCA:0764/64`). The following example is a network interface controller (NIC) without an IPv6 address:

```
en0: flags=1e084863,480<UP,BROADCAST,NOTRAILERS,RUNNING,SIMPLEX,MULTICAST,GROUPRT,64BIT,CHECKSUM_OFFLOAD(ACTIVE),CHAIN>
inet 192.168.2.104 netmask 0xfffffff0 broadcast 192.168.2.111
```
{: screen}

If one of your NICs does not contain an IPv6 address, continue on to the next section.

### Using a Power Systems Virtual Server boot image to recover from a missing IPv6 address
{: #recovering-ipv6}

1. Enter the `lslpp -L rsct.*` command to ensure that an operating system (OS) modification did not affect the RSCT file set level. For more informati9on, see [Verifying RSCT installation on AIX nodes](https://www.ibm.com/support/knowledgecenter/SGVKBA_3.2/admin/bl503_instvaix.html){: new_window}{: external}.

    *3.1.x* is the **minimum** release that is supported by the {{site.data.keyword.powerSys_notm}} service. If you redeployed an AIX image with a package that is older than 3.1, you must upgrade RSCT first.
    {: important}

2. If you still have the {{site.data.keyword.powerSys_notm}} deployed boot image, complete the following steps:

    1. Boot to the original {{site.data.keyword.powerSys_notm}} boot image.
    2. Rerun the `ifconfig -a` command. The output includes the configured IPv6 address. If you removed the IPv6 address from the original boot image configuration, you can read the AIX `cloud-init` logs to find the IPv6 address.
    3. Open the `/var/log/cloud-init-output.log` file.
    4. Use the `grep` command to search for the IP injection. There is an IPv4 address and an IPv6 address.

3. Using the IPv6 address for the host, [restart the RMC services](https://www.ibm.com/support/pages/fixing-no-rmc-connection-error){: new_window}{: external}:

    ```
    /usr/sbin/rsct/bin/rmcctrl -z
    /usr/sbin/rsct/bin/rmcctrl -A
    /usr/sbin/rsct/bin/rmcctrl -p
    ```
    {: codeblock}

4. *(Optional)* If you altered the *node ID* (that is unique to RMC), it might have impacted RMC. For example, when you are using PowerHA and trying to copy your `nodeid` details from an on-premises deployment that is not supported. Begin by rebuilding the node:

    ```
    oemdelete -o CuAt -q name=cluster0 to remove 'cluster0' entry from the CuAt ODM.
    ```
    {: codeblock}

5. *(Optional)* On the AIX VM, enter the `cat /etc/ct_node_id` command and save the output.

6. *(Optional)* To build a new `nodeid`, run the `/opt/rsct/install/bin/recfgct` file.

7. *(Optional)* Restart RMC services:

    ```
    /usr/sbin/rsct/bin/rmcctrl -z
    /usr/sbin/rsct/bin/rmcctrl -A
    /usr/sbin/rsct/bin/rmcctrl -p
    ```
    {: codeblock}

If these recovery steps do not restore the RMC status to **active** and its health to **OK**, open a case with [support ticket](/docs/power-iaas?topic=power-iaas-getting-help-and-support).

## Recovering from a missing IPv6 address when using your own boot image
{: #recover-ipv6-own}

Complete the following steps to recover from a missing IPv6 address:

1. Before you shut down the AIX VM, grab the IPv6 details.

2. Gather the IP interface and adapter configuration details by using `smitty`.

3. Run `/usr/sbin/rsct/bin/lsnodeid` to grab the `nodeid`.

4. Confirm that the `nodeid` matches the output from `cat /etc/ct_node_id` and c`at /var/ct/cfg/ct_node_id`.

5. Check the management node details (to be used on your disk later) by entering the following command, `lsrsrc ManagementServer hostname`.

6. Power down the AIX VM and restart it by using your custom boot image.

7. Re-create the same network configuration as on the IBM boot image by using `smitty`.

8. Validate that the RSCT packages are at least *3.1* or later by running the `lslpp -L rsct.*` command.

9. Check what your boot OS management node is by entering, `lsrsrc ManagementServer hostname`.

10. If your boot OS management node does not match the original IBM boot image, enter:

    ```
    Stop RMC
    rmcctrl -K
    ```
    {: codeblock}

11. Use the `rmrsrc` command to remove your management node.

    ```
    /opt/rsct/bin/rmrsrc -s 'Hostname = "hmc1.mydomain.mycompany.com"' ManagementServer

    where hmc1.mydomain.mycompany.com is the value returned on the lssrc command above.
    ```
    {: screen}

12. Run `/usr/sbin/rsct/bin/lsnodeid`. This will likely **not** match the data from the IBM boot image.

13. Delete the file, `/etc/ct_node_id`.

14. Generate a `Nodeid` to match the original boot ID.

    ```
    recfgct -i value from /etc/ct_node_id (on the original IBM boot disk collected above)
    ```
    {: screen}

15. Start RMC again and wait 15 minutes.

    ```
    /usr/sbin/rsct/bin/rmcctrl -A
    /usr/sbin/rsct/bin/rmcctrl -p
    ```
    {: codeblock}

16. Run `/usr/sbin/rsct/bin/lsnodeid`.

17. Output should be the same as the output from the IBM boot image.
