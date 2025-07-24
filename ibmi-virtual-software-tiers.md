---

copyright:
  years: 2025

lastupdated: "2025-07-24"

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






With IBM Power10 systems and later, you can assign {{site.data.keyword.ibmi-vst}} to a virtual server instance (VSI). The software tier limits the size of the VSI, but not the physical system it runs on. For example, a virtual server assigned a P10 tier can run on either an S1022 or an E1080 server. The tier restricts the resource allocation for the VSI, not its hardware compatibility.

The {{site.data.keyword.ibmi-vst}} controls the pricing tier for the IBM i operating system and licensed program products (LPPs). It also defines the boundaries for the following resources:
- Maximum number of virtual processors
- Maximum memory size

You can dynamically adjust the number of CPUs and the memory size if the values are within the {{site.data.keyword.ibmi-vst}} limits. To grow beyond the limit of the current {{site.data.keyword.ibmi-vst}}, you must follow these steps:
1. Power off the VSI
2. Change the {{site.data.keyword.ibmi-vst}} for the VSI to a new tier that aligns with your new resource requirements

When you change the software tier, the billing for the {{site.data.keyword.ibmi-vst}} automatically updates to reflect the selected tier.

You can generate an estimate of {{site.data.keyword.powerSys_notm}} resources with an {{site.data.keyword.ibmi-vst}} before you deploy the resources. For more information, see [Estimating a virtual server instance](/docs/power-iaas?topic=power-iaas-generating-an-estimate#est-vsi).

When you create a VSI, complete the following steps to assign an {{site.data.keyword.ibmi-vst}} to it:

- Select an IBM i image with version 7.3 or later from the **Image** list under the **Boot image** section
- Select an IBM Power10 or a later server from the **Machine type** list
- Assign a VSN to the VSI. If a virtual serial number (VSN) is not assigned to the VSI, edit the **Virtual serial number (VSN)** field. In the VSN pane, select either **Auto-assign** or **Select from retained VSNs** option to assign a VSN.

For more information, see [Configuring a Power Virtual Server instance](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#configuring-instance).



## Allowed resource limits by the {{site.data.keyword.ibmi-vst}}
{: #ibmi-vsw-vp-mem}

For each {{site.data.keyword.ibmi-vst}}, the supported limits for resources are defined. These limits help align resource usage with software licensing costs. Understanding the limitations is essential for planning your VSI size and ensuring compliance with IBM i licensing models.

The following table provides the details of the maximum number of virtual processors and memory size allowed on each {{site.data.keyword.ibmi-vst}}.

| IBM i software tiers | Maximum virtual processors | Maximum memory size |
| ---- | -------------------------- | -------------- |
| P05 | 1 | 64 GB |
| P10 | 4 | 1 TB |
| P20 | 12 | 1 TB |
| P30 | No limit | No limit |
{: caption="Maximum virtual processors and memory size for each {{site.data.keyword.ibmi-vst}}" caption-side="bottom"}


## Supported {{site.data.keyword.ibmi-vst}}s on {{site.data.keyword.powerSys_notm}}
{: #ibmi-vsw-system-types}

Not all {{site.data.keyword.ibmi-vst}}s are supported on all the {{site.data.keyword.off-prem-fname}} types. The following table shows which {{site.data.keyword.ibmi-vst}}s are compatible with each system type.



| System types | IBM i software tiers | | | |
| ----------- | --- | --- | --- | --- |
|             | P05 | P10 | P20 | P30 |
| S1022       | Yes | Yes | Yes | No  |
| S1122       | Yes | Yes | Yes | No  |
| E1080       | No  | Yes | Yes | Yes |
| E1180       | No  | Yes | Yes | Yes |
{: caption="Supported {{site.data.keyword.ibmi-vst}}s on {{site.data.keyword.powerSys_notm}}s" caption-side="bottom"}





IBM i is not supported on IBM E1050 and E1150 system types.
{: note}






