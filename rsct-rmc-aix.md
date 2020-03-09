---

copyright:
  years: 2019, 2020

lastupdated: "2020-03-09"

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

RSCT is a set of software components that together provide a comprehensive clustering environment for AIX&reg;, Linux&reg;, Solaris, and Windows&reg; operating systems. RSCT is the infrastructure that is used by various IBM products to provide clusters with improved system availability, scalability, and ease of use. For the {{site.data.keyword.powerSys_notm}} offering, RSCT 3.1 is the minimum package level that is required for an imported AIX image (provides IPv6 support). The {{site.data.keyword.powerSys_notm}} development team, however, recommends you use [RSCT 3.2](https://www.ibm.com/support/knowledgecenter/SGVKBA_3.2/navigation/welcome.html){: new_window}{: external} for optimal performance.

The RSCT `nodeid` is not rebuilt If you are deploying an AIX VM from a network installation management (NIM) server without `cloud-init`, and RSCT is installed.
{: important}

## Resource Managment Control (RMC)
{: #rmc-aix}

The [RMC subsystem](https://www.ibm.com/support/knowledgecenter/SGVKBA_3.2/admin/bl503_undrmc.html){: new_window}{: external} is the scalable backbone of RSCT that provides a generalized framework for managing resources within a single system or a cluster. Its generalized framework is used by cluster management tools to monitor, query, modify, and control cluster resources. RMC provides a single monitoring and management infrastructure for both RSCT peer domains and management domains.

The AIX VM's RMC status is presented in the {{site.data.keyword.cloud}} dashboard as a health status. The RMC health status can be either **OK** or **Warning**. **Warning** statuses happen when the RMC subsystem between your VM and the management system is not connected.

The RMC connection between your VM and the system management service is configured when you create the AIX VM. When you deploy an AIX VM, the IPv6 management interface is injected into the VM. If you remove or overwrite this interface, an RMC connection is not possible. The following procedures can cause the injected IPv6 management interface to be lost after you deploy the AIX VM:

- You attach a different boot volume to the VM and boot from it
- You use the `mksysb restore` operation from an on-premises VM
- You use `smitty` to remove the IPv6 interface

## Issue diagnosis and recovery
{: #-rsct-diagnosis-recovery}

Diagnosis of the issue.

ifconfig -a ( on the client AIX lpar)
The ouput should include an IPV6 address which connects to the novalink host.
If the IPV6 address is missing

en0: flags=1e084863,480<UP,BROADCAST,NOTRAILERS,RUNNING,SIMPLEX,MULTICAST,GROUPRT,64BIT,CHECKSUM_OFFLOAD(ACTIVE),CHAIN>
   inet 192.168.2.104 netmask 0xfffffff0 broadcast 192.168.2.111

Above we find the output from ifconfig -a on the AIX lpar. notice there is only ipv4 addresses, no ipv6..

Resolving the issue.
Validate the customer modification to the OS did not downlevel RSCT packages
https://www.ibm.com/support/knowledgecenter/SGVKBA_3.2/admin/bl503_instvaix.html
lslpp -L rsct.*
3.1.x is the MINIMUM release supported by PowerIaaS,
If they redployed an OS image with older packages than 3.1 they must upgrade RSCT FIRST

If the customer still has the original disk PowerIaaS created at deploy available...
Boot to that disk.. rerun ifconfig -a , the output will include the configured IPV6 address.
If the ipv6 address was removed from the original boot disk configuration ,
the cloud-init logs on AIX can be read to find the IPV6 address
Open /var/log/cloud-init-output.log  
grep for the IP injection, there will be the IPV4 address and then the IPV6 address.

using the found IPV6 address for the host https://cloud.ibm.com/docs/infrastructure/power-iaas?topic=power-iaas-managing-network-interface
Next step is to restart RMC services on AIX

/usr/sbin/rsct/bin/rmcctrl -z
/usr/sbin/rsct/bin/rmcctrl -A
/usr/sbin/rsct/bin/rmcctrl -p
https://www.ibm.com/support/pages/fixing-no-rmc-connection-error

If the customer altered the node id (unique to RMC), it may have impacted management .
(IF the customer is using PowerHA and trying to copy their nodeid details from their on-prem deploy that is NOT supported).
On the AIX lpar
cat /etc/ct_node_id
save output

rebuild node
oemdelete -o CuAt -q name=cluster0 to remove 'cluster0' entry from the CuAt ODM.
then
/opt/rsct/install/bin/recfgct
to build a new nodeid.

restart services again
/usr/sbin/rsct/bin/rmcctrl -z
/usr/sbin/rsct/bin/rmcctrl -A
/usr/sbin/rsct/bin/rmcctrl -p

If none of the above restore health to OK and RMC status to active open a case with support.