---

copyright:
  years: 2019

lastupdated: "2019-07-29"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:important: .important}
{:tip: .tip}
{:note: .note}

# High Availability and Disaster Recovery options in Power Systems Virtual Servers
{: #ha-dr}

The {{site.data.keyword.powerSys_notm}} instance restarts the virtual servers on a different host system if a hardware failure occurs. This process provides basic High Availability (HA) capabilities for the {{site.data.keyword.powerSys_notm}} service.
{:shortdesc}

If you want more advanced HA or Disaster Recover (DR) solutions, you can deploy the following applications in your {{site.data.keyword.powerSys_notm}} environment.

## PowerHA SystemMirror for AIX Standard Edition
{: #ha-dr-ha-standard}

You can use a monthly subscription model when purchasing PowerHA SystemMirror for AIX Standard Edition. For more information, see [Standard Edition monthly pricing options ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/common/ssi/ShowDoc.wss?docURL=/common/ssi/rep_ca/8/897/ENUS219-288/index.html).

After you purchase the software, you can download it from [IBM Entitled Systems Support (ESS) ![External link icon](../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/eserver/ess). You can install PowerHA SystemMirror for AIX on the virtual server that is running in your {{site.data.keyword.powerSys_notm}} environment. For installation instructions, see [Installing PowerHA SystemMirror ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SSPHQG_7.2/install/ha_install.html).

Review the following information for implementing PowerHA SystemMirror for AIX in your {{site.data.keyword.powerSys_notm}} environment.

* When you are creating the virtual servers that are part of the PowerHA SystemMirror cluster, you must select **Different Server** from the **Colocation Rules** field.
![Displays colocation rules field](/images/hadr2.png "Displays colocation rules field"){: caption="Figure 1. Creating virtual servers on different servers" caption-side="bottom"}

* When you are creating storage volumes (disks) for the virtual severs that are part of the PowerHA SystemMirror cluster, you must select **On** from the **Shareable** field.
![Displays sharable rules field](/images/hadr1.png "Displays shareable field"){: caption="Figure 2. Creating storage volumes that are shareable" caption-side="bottom"}

* By using the {{site.data.keyword.powerSys_notm}} service, you do not have access to the HMC, VIOS, and the host system. Therefore, any PowerHA SystemMirror functions that require access to these capabilities, such as Resource Optimized High Availability (ROHA) and Active Node Halt Policy (ANHP), are not available.

<!--* When you deploy PowerHA SystemMirror, you must verify that the Service IP address is defined as a private IP address. This Service IP address can be accessed by another {{site.data.keyword.powerSys_notm}} instance or from other {{site.data.keyword.cloud}} applications. You cannot use a public IP address because it cannot be moved from one interface to another interface within a virtual server or across different virtual servers. -->

<!--When you deploy PowerHA SystemMirror for AIX Enterprise Edition clusters in the {{site.data.keyword.powerSys_notm}} environment, you can only use the Geographic Logical Volume Manager (GLVM) functions. You cannot use storage mirroring functions that are part of PowerHA SystemMirror for AIX Enterprise Edition because you do not have access to the subsystem storage in the {{site.data.keyword.powerSys_notm}} environment. For more information, see [Geographic Logical Volume Manager ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SSPHQG_7.2/glvm/ha_glvm_kick.html).
{:note}
[Enterprise Edition monthly pricing options ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/common/ssi/cgi-bin/ssialias?infotype=AN&subtype=CA&htmlfid=897/ENUS219-286) -->

## Business Continuity through backup and restore
{: #ha-dr-ha-business}

Your {{site.data.keyword.powerSys_notm}} configuration and data are not backed up by {{site.data.keyword.cloud}}.

You can use the {{site.data.keyword.cloud_notm}} UI to back up your virtual server to {{site.data.keyword.cloud_notm}} Object Storage. You can use this process to restore your virtual server in case a critical failure occurs. For more information, see [Cloud Object Storage ![External link icon](../icons/launch-glyph.svg "External link icon")](/docs/services/cloud-object-storage?topic=cloud-object-storage-getting-started).
