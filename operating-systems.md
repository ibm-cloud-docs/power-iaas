---

copyright:
  years: 2025, 2026 

lastupdated: "2026-04-16"

keywords: Operating systems, powerVS OS


subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Operating systems supported in IBM Power Virtual Server
{: #operating-systems-powervs}

---


{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}


---

{{site.data.keyword.powerSysFull}} supports AIX, IBM i, and Linux operating systems. You can run these operating systems on your virtual server instances (VSIs), also known as logical partitions (LPARs). Each operating system (OS) runs natively on the IBM Power architecture and follows a specific version, update, and support requirements. This topic lists the supported OS versions, key technical details, and lifecycle information. The availability of specific operating systems depends on whether the Power system is deployed in an IBM data center or at a client location.

The choice between AIX, IBM i, and Linux depends on the type of the workload that you want to run on a VSI.

## AIX
{: #aix-os}

You can use AIX to run enterprise UNIX applications that require high availability, scalability, and system-level performance. For more information about AIX, see [IBM AIX](https://www.ibm.com/products/aix){: external}.

For information about supported AIX versions for {{site.data.keyword.powerSys_notm}}, see [Supported AIX versions for {{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-operating-systems-powervs#aix-public-private).


## IBM i
{: #ibmi-os}

You can use IBM i to run integrated business applications that rely on IBM&reg; Db2&reg;, Report Program Generator (RPG), or Control Language (CL) in a secure and stable environment. For more information about IBM i, see [IBM i](https://www.ibm.com/products/ibm-i){: external}.

For information about supported IBM i versions for {{site.data.keyword.powerSys_notm}}, see [Supported IBM i versions for {{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-operating-systems-powervs#ibmi-public-private).

When you use IBM i for your VSI, review the following requirements:

- If you are using IBM i 6.1, you must upgrade the OS to a current support level and then migrate to {{site.data.keyword.powerSys_notm}}. IBM i 7.2 supports direct [upgrades from IBM i 6.1 or 7.1 (N-2)](https://www.ibm.com/support/knowledgecenter/ssw_ibm_i_72/rzahc/fastpathrzahc.htm){: external}.

- Install the appropriate program temporary fixes (PTFs) depending on the version of IBM i that you use. For more information about the minimum PTF levels, see [Minimum PTF levels for IBM i](/docs/power-iaas?topic=power-iaas-minimum-levels).

- The IBM i 7.4, 7.5, 7.6, and Cloud Optical Repository (COR) OS images support Power10 and later systems. However, you can create a custom image or upgrade your IBM i VSI by downloading the media from [Entitled Systems Support (ESS)](https://www.ibm.com/servers/eserver/ess/landing/landing-page) and navigating to the **My entitled software** > **IBM i Evaluation and NLV Download** section.

## Linux
{: #linux-os}

You can use Linux to run open source, cloud-native, or containerized workloads with flexibility by using the supported Red Hat Enterprise Linux (RHEL) and SUSE Linux Enterprise Server (SLES) distributions on {{site.data.keyword.powerSys_notm}}. For more information about the supported Linux distributions, see [Enterprise Linux on Power](https://www.ibm.com/products/power/linux){: external}.

For information about supported Linux versions for {{site.data.keyword.powerSys_notm}}, see [Supported Linux versions for {{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-operating-systems-powervs#linux-public-private).

When you use Linux for your VSI, review the following Linux distribution options and requirements:



- {{site.data.keyword.powerSys_notm}} in the IBM data center supports Red Hat Enterprise Linux (RHEL) and SUSE Linux Enterprise Server (SLES) distributions. The Linux stock images are available when you select the Full Linux Subscription (FLS) option or the bring‑your‑own‑license (BYOL) option. An FLS image refers to an IBM‑provided RHEL or SLES stock OS image that includes the full Linux subscription support delivered through IBM.

    For more information about FLS, see [Full Linux® subscription for Power Virtual Server](/docs/power-iaas?topic=power-iaas-set-full-Linux){: external}.

    SAP FLS stock images are available only in IBM data centers and are not available in the {{site.data.keyword.powerSys_notm}} Private Cloud environments deployed at the client locations.
    {: important}

- To use your own license, select the OS image with the `-BYOL` suffix. On the *Create virtual server instance* page, these images are listed under the *Client supplied subscription* section. Alternatively, you can create your own customized Linux image in Open Virtualization Appliance (OVA) format by using the Linux stock images that are available when you select Full Linux Subscription (FLS). For more information, see [Creating a custom Linux image in OVA format](/docs/power-iaas?topic=power-iaas-linux-deployment).

The following IBM Power systems are supported by Red Hat and SUSE:

   - [IBM Power System E1180 (9080-HEU)](https://catalog.redhat.com/en/hardware/system/detail/282317){: external}
   - [IBM Power System E1150 (9043-MRU)](https://catalog.redhat.com/en/hardware/system/detail/280037){: external}
   - [IBM Power System S1122 (9824-22A)](https://catalog.redhat.com/en/hardware/system/detail/287077){: external}
   - [IBM Power System E1080 (9080-HEX)](https://catalog.redhat.com/en/hardware/system/detail/129035){: external}
   - [IBM Power System E1050 (9040-MRX)](https://catalog.redhat.com/en/hardware/system/detail/142977){: external}
   - [IBM Power System S1022 (9105-22A)](https://catalog.redhat.com/en/hardware/system/detail/144747){: external}
   - [IBM Power System E980 (9080-M9S)](https://catalog.redhat.com/hardware/servers/detail/17035){: external}
   - [IBM Power System S922 (9009-22A)](https://catalog.redhat.com/hardware/servers/detail/9225){: external}
   - [IBM Power System S922 (9009-22G)](https://catalog.redhat.com/en/hardware/system/detail/58365){: external}

For additional Linux support, refer to your distribution’s documentation. For cloud‑init configuration instructions, see [Installing and configuring cloud-init on Linux](https://www.ibm.com/support/knowledgecenter/en/SSXK2N_1.4.4/com.ibm.powervc.standard.help.doc/powervc_install_cloudinit_hmc.html){: external}.



## Stock images
{: #stock-images}

A stock image is an IBM‑supplied OS image that is ready for deployment on {{site.data.keyword.powerSys_notm}}. Stock images are available for use when you deploy the VSIs. The latest version of each supported OS is provided for provisioning new {{site.data.keyword.powerSys_notm}} instances. As an alternative, you can use your own backup copy of an OS image. This option is called bring-your-own-image (BYOI). For more information, see [Deploying a custom image within IBM Power Virtual Server](/docs/power-iaas?topic=power-iaas-deploy-custom-image).

For each major version of the OS that is enabled through the offering, {{site.data.keyword.powerSys_notm}} provides a single stock image. {{site.data.keyword.powerSys_notm}} typically provides stock images for the last three major versions of the supported OS. Any update to the OS stock image is planned only when the image level is validated for {{site.data.keyword.powerSys_notm}} environment. IBM Cloud sends advance notifications before removing the unsupported stock OS images.

The VSIs can continue to run without any issues after the stock OS images are removed from the image catalog. However, you are advised to update the VSIs to the supported OS versions.
{: note}

## Supported AIX, IBM i, and Linux versions for {{site.data.keyword.powerSys_notm}}
{: #os-matrix-public-private}

The following table lists the supported AIX, IBM i, and Linux OS versions that can be installed on {{site.data.keyword.powerSys_notm}} instances. OS versions not listed in the following table are not supported and cannot be installed on a VSI.


| **Processor family** | **Supported AIX versions** | **Latest stock image versions**                        |
| -------------------- | -------------------------- | ------------------------------------------------------ |
| Power11              | AIX 7.2 TL5 or later       | AIX 7.3 TL4 SP1 \n AIX 7.3 TL3 SP2 \n AIX 7.2 TL5 SP11 |
| Power10[^d]          | AIX 7.2 TL5 or later       | AIX 7.3 TL4 SP1 \n AIX 7.3 TL3 SP2 \n AIX 7.2 TL5 SP11 |
| Power9[^a]           | AIX 7.2 TL5 or later       | AIX 7.3 TL4 SP1 \n AIX 7.3 TL3 SP2 \n AIX 7.2 TL5 SP11 |
{: caption="Supported AIX versions for {{site.data.keyword.powerSys_notm}}" caption-side="bottom"}
{: summary="This table lists the supported AIX versions for {{site.data.keyword.powerSys_notm}}"}
{: #aix-public-private}
{: tab-title="AIX"}
{: tab-group="operating-systems-public-private"}
{: class="comparison-tab-table"}
{: row-headers}

| **Processor family** | **Supported IBM i versions** | **Latest stock image versions**                                                          |
| -------------------- | ---------------------------- | ---------------------------------------------------------------------------------------- |
| Power11              | IBM i 7.4 or later           | IBM i COR[^3] [^4] \n IBM i 7.5 TR7 \n IBM i 7.4 TR12                                    |
| Power10              | IBM i 7.3 or later           | IBM i COR \n IBM i 7.5 TR7 \n IBM i 7.4 TR12 \n IBM i 7.3 TR13[^5]                       |
| Power9[^b]           | IBM i 7.1 or later[^i]       | IBM i COR \n IBM i 7.5 TR7 \n IBM i 7.4 TR12 \n IBM i 7.3 TR13 \n IBM i 7.2 TR9[^6] [^7] |
{: caption="Supported IBM i versions for {{site.data.keyword.powerSys_notm}}" caption-side="bottom"}
{: summary="This table lists the supported IBM i versions for {{site.data.keyword.powerSys_notm}}"}
{: #ibmi-public-private}
{: tab-title="IBM i"}
{: tab-group="operating-systems-public-private"}
{: class="comparison-tab-table"}
{: row-headers}

| **Processor family** | **Supported RHEL versions**                                                                                                                                           | **Latest stock image versions**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Power11              | * RHEL 9.6 general purpose and SAP \n * RHEL 9.4 general purpose and SAP \n * RHEL 8.10 general purpose and SAP                                                       | * RHEL 9.6 general purpose (RHEL9-SP6) \n * RHEL 9.6 for SAP HANA (RHEL9-SP6-SAP-HANA) \n * RHEL 9.6 for SAP NetWeaver (RHEL9-SP6-SAP-NETWEAVER) \n * RHEL 9.4 general purpose (RHEL9-SP4) \n * RHEL 9.4 for SAP HANA (RHEL9-SP4-SAP-HANA) \n * RHEL 9.4 for SAP NetWeaver (RHEL9-SP4-SAP-NETWEAVER) \n * RHEL 8.10 general purpose (RHEL8-SP10) \n * RHEL 8.10 for SAP HANA (RHEL8-SP10-SAP-HANA) \n * RHEL 8.10 for SAP NetWeaver (RHEL8-SP10-SAP-NETWEAVER)                                                                                                                                                                                                                                                                                                                |
| Power10              | * RHEL 9.6 general purpose and SAP \n * RHEL 9.4 general purpose and SAP \n * RHEL 9.2 SAP \n * RHEL 8.10 general purpose and SAP \n * RHEL 8.8 SAP \n * RHEL 8.6 SAP | * RHEL 9.6 general purpose (RHEL9-SP6) \n * RHEL 9.6 for SAP HANA (RHEL9-SP6-SAP-HANA) \n * RHEL 9.6 for SAP NetWeaver (RHEL9-SP6-SAP-NETWEAVER) \n * RHEL 9.4 general purpose (RHEL9-SP4) \n * RHEL 9.4 for SAP HANA (RHEL9-SP4-SAP-HANA) \n * RHEL 9.4 for SAP NetWeaver (RHEL9-SP4-SAP-NETWEAVER) \n * RHEL 9.2 for SAP HANA (RHEL9-SP2-SAP) \n * RHEL 9.2 for SAP NetWeaver (RHEL9-SP2-SAP-NETWEAVER) \n * RHEL 8.10 general purpose (RHEL8-SP10) \n * RHEL 8.10 for SAP HANA (RHEL8-SP10-SAP-HANA) \n * RHEL 8.10 for SAP NetWeaver (RHEL8-SP10-SAP-NETWEAVER) \n * RHEL 8.8 for SAP HANA (RHEL8-SP8-SAP) \n * RHEL 8.8 for SAP NetWeaver (RHEL8-SP8-SAP-NETWEAVER) \n * RHEL 8.6 for SAP HANA (RHEL8-SP6-SAP) \n * RHEL 8.6 for SAP NetWeaver (RHEL8-SP6-SAP-NETWEAVER) |
| Power9[^c]           | * RHEL 9.6 general purpose and SAP \n * RHEL 9.4 general purpose and SAP \n * RHEL 9.2 SAP \n * RHEL 8.10 general purpose and SAP \n * RHEL 8.8 SAP \n * RHEL 8.6 SAP | * RHEL 9.6 general purpose (RHEL9-SP6) \n * RHEL 9.6 for SAP HANA (RHEL9-SP6-SAP-HANA) \n * RHEL 9.6 for SAP NetWeaver (RHEL9-SP6-SAP-NETWEAVER) \n * RHEL 9.4 general purpose (RHEL9-SP4) \n * RHEL 9.4 for SAP HANA (RHEL9-SP4-SAP-HANA) \n * RHEL 9.4 for SAP NetWeaver (RHEL9-SP4-SAP-NETWEAVER) \n * RHEL 9.2 for SAP HANA (RHEL9-SP2-SAP) \n * RHEL 9.2 for SAP NetWeaver (RHEL9-SP2-SAP-NETWEAVER) \n * RHEL 8.10 general purpose (RHEL8-SP10) \n * RHEL 8.10 for SAP HANA (RHEL8-SP10-SAP-HANA) \n * RHEL 8.10 for SAP NetWeaver (RHEL8-SP10-SAP-NETWEAVER) \n * RHEL 8.8 for SAP HANA (RHEL8-SP8-SAP) \n * RHEL 8.8 for SAP NetWeaver (RHEL8-SP8-SAP-NETWEAVER) \n * RHEL 8.6 for SAP HANA (RHEL8-SP6-SAP) \n * RHEL 8.6 for SAP NetWeaver (RHEL8-SP6-SAP-NETWEAVER) |
{: caption="Supported Linux versions for {{site.data.keyword.powerSys_notm}}" caption-side="bottom"}
{: summary="This table lists the supported Linux versions for {{site.data.keyword.powerSys_notm}}"}
{: #linux-public-private}
{: tab-title="Linux (RHEL)"}
{: tab-group="operating-systems-public-private"}
{: class="comparison-tab-table"}
{: row-headers}

| **Processor family** | **Supported SLES versions**                                                                                                                   | **Latest stock image versions**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Power11              | * SLES 16 general purpose \n * SLES 15.7 general purpose and SAP \n * SLES 15.6 general purpose and SAP                                       | * SLES 16 general purpose (SLES16) \n * SLES 15 SP7 general purpose (SLES15) \n * SLES 15 SP7 for SAP HANA (SLES15-SP7-SAP) \n * SLES 15 SP7 for SAP NetWeaver (SLES15-SP7-SAP-NETWEAVER) \n * SLES 15 SP6 general purpose (SLES15) \n * SLES 15 SP6 for SAP HANA (SLES15-SP6-SAP) \n * SLES 15 SP6 for SAP NetWeaver (SLES15-SP6-SAP-NETWEAVER)                                                                                                                                                                                                                           |
| Power10              | * SLES 16 general purpose \n * SLES 15.7 general purpose and SAP \n * SLES 15.6 general purpose and SAP \n * SLES 15.5 SAP \n * SLES 15.4 SAP | * SLES 16 general purpose (SLES16) \n * SLES 15 SP7 general purpose (SLES15) \n * SLES 15 SP7 for SAP HANA (SLES15-SP7-SAP) \n * SLES 15 SP7 for SAP NetWeaver (SLES15-SP7-SAP-NETWEAVER) \n * SLES 15 SP6 general purpose (SLES15) \n * SLES 15 SP6 for SAP HANA (SLES15-SP6-SAP) \n * SLES 15 SP6 for SAP NetWeaver (SLES15-SP6-SAP-NETWEAVER) \n * SLES 15 SP5 for SAP HANA (SLES15-SP5-SAP) \n * SLES 15 SP5 for SAP NetWeaver (SLES15-SP5-SAP-NETWEAVER) \n * SLES 15 SP4 for SAP HANA (SLES15-SP4-SAP) \n * SLES 15 SP4 for SAP NetWeaver (SLES15-SP4-SAP-NETWEAVER) |
| Power9[^c]           | * SLES 16 general purpose \n * SLES 15.7 general purpose and SAP \n * SLES 15.6 general purpose and SAP \n * SLES 15.5 SAP \n * SLES 15.4 SAP | * SLES 16 general purpose (SLES16) \n * SLES 15 SP7 general purpose (SLES15) \n * SLES 15 SP7 for SAP HANA (SLES15-SP7-SAP) \n * SLES 15 SP7 for SAP NetWeaver (SLES15-SP7-SAP-NETWEAVER) \n * SLES 15 SP6 general purpose (SLES15) \n * SLES 15 SP6 for SAP HANA (SLES15-SP6-SAP) \n * SLES 15 SP6 for SAP NetWeaver (SLES15-SP6-SAP-NETWEAVER) \n * SLES 15 SP5 for SAP HANA (SLES15-SP5-SAP) \n * SLES 15 SP5 for SAP NetWeaver (SLES15-SP5-SAP-NETWEAVER) \n * SLES 15 SP4 for SAP HANA (SLES15-SP4-SAP) \n * SLES 15 SP4 for SAP NetWeaver (SLES15-SP4-SAP-NETWEAVER) |
{: caption="Supported Linux versions for {{site.data.keyword.powerSys_notm}}" caption-side="bottom"}
{: summary="This table lists the supported Linux versions for {{site.data.keyword.powerSys_notm}}"}
{: #linux-public-private}
{: tab-title="Linux (SLES)"}
{: tab-group="operating-systems-public-private"}
{: class="comparison-tab-table"}
{: row-headers}


[^a]: Not available for {{site.data.keyword.on-prem-fname}} in client locations.
[^b]: Not available for {{site.data.keyword.on-prem-fname}} in client locations.
[^c]: Not available for {{site.data.keyword.on-prem-fname}} in client locations.
[^d]: Power10 systems running firmware level FW1110 support AIX 7.2 TL5 and later.
[^3]: IBM i Cloud Optical Repository (COR) is a virtual image. You can deploy the image and use it as a Network File Server (NFS) to perform various IBM i tasks that require media. For more information on COR images, see [Cloud Optical Repository](https://cloud.ibm.com/media/docs/downloads/power-iaas/Cloud_Optical_Repository.pdf){: external}.
[^4]: For more information about performing an upgrade, see [57xxSS1 Option 1 or Option 3 in *ERROR - Tips Before Reinstallation](https://www.ibm.com/support/pages/57xxss1-option-1-or-option-3-error-tips-reinstallation){: external}.
[^5]: IBM i 7.3 and 7.2 on Power Virtual Server ended normal support on 1 October 2023 and are supported via paid service extension only. Please refer to the [IBM i lifecycle](https://www.ibm.com/support/pages/release-life-cycle){: external} page for upcoming EoL dates and prepare to upgrade to a later version.
[^6]: IBM i 7.3 and 7.2 on Power Virtual Server ended normal support on 1 October 2023 and are supported via paid service extension only. Please refer to the [IBM i lifecycle](https://www.ibm.com/support/pages/release-life-cycle){: external} page for upcoming EoL dates and prepare to upgrade to a later version.
[^7]: Not supported on {{site.data.keyword.on-prem}}.
[^i]: IBM i 7.1 is supported on the IBM Power9 S924 and E980 models.

## System software maps
{: #sw-mapping}

System software maps are reference documents that outline the compatibility between different OS versions and IBM Power Systems hardware. For more information about AIX, IBM i, and Linux (SUSE and RHEL) versions that are compatible with various Power systems, refer to the following software maps:

- [System software maps for AIX](https://www.ibm.com/support/pages/node/6020074){: external}
- [System software maps for IBM i](https://www.ibm.com/support/pages/node/6023368){: external}
- [System software maps for SUSE Linux Enterprise Server](https://www.ibm.com/support/pages/node/6023374){: external}
- [System software maps for Red Hat Enterprise Linux](https://www.ibm.com/support/pages/node/6024466){: external}


## Licensing and software components
{: #licensing-sw-components}

The license for the AIX and IBM i operating systems is a part of the overall cost for the workspace. You cannot use an existing license that you have already purchased.

You can use movable IBM i OS entitlements (IBM i Moveable Operating License (MOL)) to move your existing on-premises entitlements to the {{site.data.keyword.powerSys_notm}}. Contact IBM support to know more about IBM i MOL. For the available support resources, see [Getting help and support](/docs/power-iaas?topic=power-iaas-getting-help-and-support){: external}.

Power Virtual Server supports multiple levels of RHEL and SLES. You can either use the stock Linux images that IBM provides with Full Linux Subscription or bring your own custom Linux image with vendor-provided subscription.

For more information about licensing, see:

- IBM i: /docs/power-iaas?topic=power-iaas-ibmi-lpps
- AIX: https://www.ibm.com/support/customer/csol/terms/#search-result

You must ensure compliance with all third-party software licenses that you use in your environment, including middleware, application software, monitoring tools, and any other non-IBM licensed components.
{: important}

## Operating system lifecycle information
{: #os-lifecycle}

Review the lifecycle information for the OSs that you deploy in the {{site.data.keyword.powerSys_notm}} environment. You can use the following resources to plan upgrades, support, and long-term maintenance for your AIX, IBM i, and Linux-based VSIs:

- [AIX support lifecycle information](https://www.ibm.com/support/pages/aix-support-lifecycle-information){: external}
- [IBM i release lifecycle](https://www.ibm.com/support/pages/release-life-cycle){: external}
- [Red Hat Enterprise Linux lifecycle](https://access.redhat.com/support/policy/updates/errata){: external}
- [SUSE Linux Enterprise Server product support lifecycle](https://www.suse.com/lifecycle/#suse-linux-enterprise-server-10){: external}

## Unsupported operating system versions in {{site.data.keyword.powerSys_notm}}
{: #unsupported-os-pvs}

You can deploy various IBM i, AIX, and Linux operating systems in {{site.data.keyword.powerSys_notm}} environment. However, any OS version that IBM no longer supports is considered unsupported, even if the OS version still runs on the {{site.data.keyword.powerSys_notm}} infrastructure.

You must upgrade your VSIs to a supported OS to ensure compatibility with the platform features, maintain system reliability, and receive security updates and technical support.

### Risks of using unsupported operating system versions
{: #unsupported-os-risks}

Unsupported OS versions might continue to work in the {{site.data.keyword.powerSys_notm}} infrastructure, but they carry significant risks and do not qualify for support, including:

- **Limited feature compatibility**: {{site.data.keyword.powerSys_notm}} automation features such as Live Partition Mobility (LPM) and remote restart might not work, which can reduce application uptime during host maintenance.

- **Server restart failures**: The standard {{site.data.keyword.powerSys_notm}} restart functionality might not work, which can cause the VSIs to remain pinned to the host and disrupt availability.

- **Security vulnerabilities**: Unsupported OS versions might not receive critical security updates, which can increase exposure to security threats.

### Customer responsibilities
{: #cust-responsibility-os}

If you run an unsupported operating system version, you are responsible for managing all the associated risks and issues that might occur. You are also responsible for maintaining, updating, and supporting any custom image that is based on an unsupported OS. In addition, you acknowledge that if IBM identifies a security vulnerability or a critical issue, IBM can suspend any VSI that is running an unsupported OS in the {{site.data.keyword.powerSys_notm}} environment.
