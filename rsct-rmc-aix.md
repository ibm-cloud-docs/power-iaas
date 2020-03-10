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

## Diagnosing and recoverying from a missing IPv6 address
{: #rsct-diagnosis-recovery}

One of your AIX VM network interface controllers (NICs) must include an IPv6 address to connect to the Novalink host. If your NIC does not have an associated IPv6 address, you must perform a recovery procedure.

1. Enter the `ifconfig -a` command on your AIX VM terminal. Check to see whether one of your NICs shows an IPv6 address (for example, `2001:1234:5723:ABCD:5678:D14E:DBCA:0764/64`). The following example is a network interface controller (NIC) without an IPv6 address:

        ```
        en0: flags=1e084863,480<UP,BROADCAST,NOTRAILERS,RUNNING,SIMPLEX,MULTICAST,GROUPRT,64BIT,CHECKSUM_OFFLOAD(ACTIVE),CHAIN>
        inet 192.168.2.104 netmask 0xfffffff0 broadcast 192.168.2.111
        ```

    If one of your NICs does not contain an IPv6 address, continue to the next step.

2. Enter the `lslpp -L rsct.*` command to ensure that an operating system (OS) modification did not affect the RSCT file set level. For more informati9on, see [Verifying RSCT installation on AIX nodes](https://www.ibm.com/support/knowledgecenter/SGVKBA_3.2/admin/bl503_instvaix.html){: new_window}{: external}.

        *3.1.x* is the **minimum** release supported by the {{site.data.keyword.powerSys_notm}} service. If you redployed an AIX image with a package that is older than 3.1, you must upgrade RSCT first.
        {: important}

3. If you still have the originally deployed {site.data.keyword.powerSys_notm}} boot image, complete the following steps:

    1. Boot to the original {site.data.keyword.powerSys_notm}} boot image.
    2. Rerun the `ifconfig -a` command. The output includes the configured IPv6 address. If you removed the IPv6 address from the original boot image configuration, you can read the AIX `cloud-init` logs to find the IPv6 address.
    3. Open the `/var/log/cloud-init-output.log` file.
    4. Use the `grep` command to search for the IP injection. There is an IPv4 address and an IPv6 address.

4. Using the found IPv6 address for the host, [restart the RMC services](https://www.ibm.com/support/pages/fixing-no-rmc-connection-error){: new_window}{: external} on AIX:

        ```
        /usr/sbin/rsct/bin/rmcctrl -z
        /usr/sbin/rsct/bin/rmcctrl -A
        /usr/sbin/rsct/bin/rmcctrl -p
        ```

5. *(Optional)* If you altered the *node ID* (that is unique to RMC), it might have impacted RMC. Begin by rebuilding the node:

        ```
        oemdelete -o CuAt -q name=cluster0 to remove 'cluster0' entry from the CuAt ODM.
        ```

        For example, when you are using PowerHA and trying to copy your `nodeid` details from an on-premises deploy that is not supported.On the AIX VM, `cat /etc/ct_node_id` and save the output
        {: note}

6. *(Optional)* To build a new `nodeid`, run the `/opt/rsct/install/bin/recfgct` file.

7. *(Optional)* Restart RMC services again.

        ```
        /usr/sbin/rsct/bin/rmcctrl -z
        /usr/sbin/rsct/bin/rmcctrl -A
        /usr/sbin/rsct/bin/rmcctrl -p
        ```

If none of the above restore health the RMC status to **active** and health to **OK**, open a case with [support ticket](/docs/power-iaas?topic=power-iaas-getting-help-and-support).

<!-- ## Section 2

If the original boot disk PowerIaaS created exists

1. Prior to shutting down the VM, Grab the IPv6 details.

2. From Smitty gather the IP interface and adapter configuration details.

3. Also grab the nodeid by running
/usr/sbin/rsct/bin/lsnodeid

4. confirm this matches output of
cat /etc/ct_node_id

5. confirm that matches
cat /var/ct/cfg/ct_node_id

6. Check the management node details (to be used on your disk later)
lsrsrc ManagementServer hostname

7. Power down the VM and reboot using your custom boot disk

8. Using smitty recreate the same network configuration as on the IBM boot disk.

9. Validate the RSCT packages are at least 3.1 or later
lslpp -L rsct.*

10. check what your boot OS management node is lsrsrc ManagementServer hostname

11. If this does not match the original IBM boot disk...
Stop RMC
rmcctrl -K

12. Use rmrsrc to remove your management node
example syntax /opt/rsct/bin/rmrsrc -s 'Hostname = "hmc1.mydomain.mycompany.com"' ManagementServer
where hmc1.mydomain.mycompany.com is the value returned on the lssrc command above.

13. run /usr/sbin/rsct/bin/lsnodeid. This likely will NOT match the data from the IBM boot lpar.

14. delete file /etc/ct_node_id

15. Generate a Nodeid to match the original boot id

recfgct -i value from /etc/ct_node_id on the original IBM boot disk collected above.

16. Start RMC again wait 15 minutes,
/usr/sbin/rsct/bin/rmcctrl -A
/usr/sbin/rsct/bin/rmcctrl -p

17. Run /usr/sbin/rsct/bin/lsnodeid

18. Output should be the same as the output from the IBM Boot disk.
