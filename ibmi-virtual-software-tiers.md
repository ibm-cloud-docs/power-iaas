---

copyright:
  years: 2025, 2026

lastupdated: "2026-09-21"

keywords: ibm i, virtual tiers, {{site.data.keyword.vst}}s, ibm i {{site.data.keyword.vst}}s

subcollection: power-iaas

---
{{site.data.keyword.attribute-definition-list}}

# Assigning an {{site.data.keyword.ibmi-vst}} to an IBM i {{site.data.keyword.powerSys_notm}} instance
{: #ibmi-vsw-tiers}

---

{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}


---





{{site.data.keyword.ibmi-vst}}s are a licensing model that classifies IBM {{site.data.keyword.powerSys_notm}}s by processor characteristics to determine the price and feature set for the IBM i operating system (OS) and other software.
{: shortdesc}

On IBM Power10 and later systems, you can assign an {{site.data.keyword.ibmi-vst}} to a virtual server instance (VSI). The {{site.data.keyword.ibmi-vst}} limits the capacity of the VSI, but you can select any physical system that supports the assigned tier. For example, a virtual server that is assigned to a P10 tier can run on either an S1022 or an E1080 server. The tier restricts the resource allocation for the VSI but not its hardware compatibility.

IBM i is not supported on IBM E1050 and E1150 system types.
{: note}

The {{site.data.keyword.ibmi-vst}} determines the pricing tier for the IBM i OS and Licensed Program Products (LPPs). The tier also defines the limits for the following resources:
- Maximum number of virtual processors
- Maximum memory


You can adjust the number of CPUs and the amount of memory without powering off the VSI if the values are in the {{site.data.keyword.ibmi-vst}} limits. To increase the capacity beyond the current {{site.data.keyword.ibmi-vst}} limits, you must complete the following steps:
1. Power off the VSI.
2. Change the {{site.data.keyword.ibmi-vst}} to a tier that supports your required number of virtual processors and memory.

For more information, see [Supported resource limits by the IBM i software tier](/docs/power-iaas?topic=power-iaas-ibmi-vsw-tiers#ibmi-vsw-vp-mem).

When you change the software tier, the billing for the {{site.data.keyword.ibmi-vst}} automatically changes to reflect the selected tier.

You can generate an estimate of {{site.data.keyword.powerSys_notm}} resources with an {{site.data.keyword.ibmi-vst}} before you deploy the resources. For more information, see [Estimating a virtual server instance](/docs/power-iaas?topic=power-iaas-generating-an-estimate#est-vsi).


To assign an {{site.data.keyword.ibmi-vst}} to an IBM i {{site.data.keyword.powerSys_notm}} instance, complete the following steps:

1. Create a VSI by following the instructions at [Configuring a Power Virtual Server instance](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#configuring-instance).
2. Select an IBM i image with version 7.3 or later from the **Image** list in the **Boot image** section.
3. Select an IBM Power10 or later server type from the **Machine type** list in the **Profile** section.
4. Click the **Edit** icon for the **Virtual serial number (VSN)** field in the **Profile** section. The virtual serial number summary pane appears.
5. Select **Auto-assign** or **Select from retained VSNs** to assign a VSN.

You can assign a VSN only to a VSI that runs IBM i version 7.2 or later.
{: note}

The **{{site.data.keyword.ibmi-vst}}** list displays only the tiers that are compatible with the machine type that you select. The **{{site.data.keyword.ibmi-vst}}** list also shows the recommended tier based on the number of cores and memory that you configure. You can select the {{site.data.keyword.ibmi-vst}} that is displayed in the **{{site.data.keyword.ibmi-vst}}** field or other options from the list.

## Supported resource limits by the {{site.data.keyword.ibmi-vst}}
{: #ibmi-vsw-vp-mem}


{{site.data.keyword.ibmi-vst}}s are available in different licensing models such as P05, P10, P20, and P30. Each {{site.data.keyword.ibmi-vst}} defines the supported resource limits. These limits help align resource usage with software licensing costs. You must understand the supported limits of resources for planning your VSI capacity and ensure compliance with IBM i licensing models.

The following table lists the maximum number of virtual processors and memory for each {{site.data.keyword.ibmi-vst}}:

| {{site.data.keyword.ibmi-vst}} | Maximum virtual processors | Maximum memory |
| ------------------------------ | -------------------------- | -------------- |
| P05                            | 1                          | 64 GB          |
| P10                            | 4                          | 1 TB           |
| P20                            | 12                         | 1 TB           |
| P30                            | Unlimited                  | Unlimited      |
{: caption="Maximum virtual processors and memory for each {{site.data.keyword.ibmi-vst}}" caption-side="bottom"}


## Supported {{site.data.keyword.ibmi-vst}}s on {{site.data.keyword.powerSys_notm}}
{: #ibmi-vsw-system-types}






You can assign {{site.data.keyword.ibmi-vst}}s only to compatible {{site.data.keyword.powerSys_notm}} system types. The available software tiers vary depending on the current host capacity. The following table lists the {{site.data.keyword.ibmi-vst}}s that are compatible with each system type.

| System types | Supported IBM i software tiers |           |           |               |
| ------------ | ------------------------------ | --------- | --------- | ------------- |
|              | P05                            | P10       | P20       | P30           |
| S1022        | Supported                      | Supported | Supported | Not supported |
| E1080        | Not supported                  | Supported | Supported | Supported     |
| Power11      | Supported                      | Supported | Supported | Supported     |
{: caption="Supported {{site.data.keyword.ibmi-vst}}s on {{site.data.keyword.powerSys_notm}}s" caption-side="bottom"}

### Behavior of IBM i deployments on IBM Power11 servers
{: #ibmi-power11-vsw-tier-behavior}

When you create a VSI, if you select Power11 as the machine type, {{site.data.keyword.powerSys_notm}} automatically places VSIs on a supported host server based on your workload requirements. This behavior differs from earlier Power servers, such as S1022 or E1080, where you manually select the specific system type. For more information about creating a VSI, see [Creating a Power Virtual Server workspace](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#creating-service).

If you have a VSI that is running on an E1180 or S1122 host server, the VSI continues to run on the same host server.
{: note}

When you deploy an IBM i VSI on Power11 without assigning an {{site.data.keyword.ibmi-vst}}, the following behaviors apply:

Automatic tier assignment based on host server type
:   If you do not select an {{site.data.keyword.ibmi-vst}} while creating an IBM i VSI, the VSI is assigned to a tier based on the underlying host server where {{site.data.keyword.powerSys_notm}} places the instance. For example:
    * A VSI that is placed on an S1122 host server is assigned to the P10 tier.
    * A VSI that is placed on an E1180 host server is assigned to the P30 tier.

Dynamic resizing limit (4-core cap)
:   An IBM i VSI with 4 or fewer cores that is deployed without an IBM i software tier can dynamically resize only up to 4 cores (the P10 tier limit).

    To resize an IBM i VSI beyond 4 cores, complete the following steps:
    1. Power off the VSI. For more information, see [Shut down and restart a VSI](/docs/power-iaas?topic=power-iaas-modifying-instance#shut-down-restart-vsi).
    2. Assign a virtual serial number (VSN) to the VSI. For more information, see [Assigning a VSN to an existing VSI](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#VSN-existing-VM).
    3. Assign a compatible {{site.data.keyword.ibmi-vst}} that supports more than 4 cores to the VSI. For more information, see [Configuring a Power Virtual Server instance](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#configuring-instance). For more information about maximum cores supported by {{site.data.keyword.ibmi-vst}}, see [Supported resource limits by the {{site.data.keyword.ibmi-vst}}](#ibmi-vsw-system-types).
    4. Update the processor core count to the required size.
    5. Power on the VSI.











If you deploy multiple IBM i VSIs with the P20 software tier on IBM S1022 hosts, the deployment might fail during an IBM data center upgrade. However, deploying a single IBM i VSI with the P20 software tier on an S1022 host is supported.
{: restriction}
