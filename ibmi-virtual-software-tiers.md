---

copyright:
  years: 2025

lastupdated: "2025-08-28"

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





Starting with IBM Power10 systems and later, you can assign an {{site.data.keyword.ibmi-vst}} to a virtual server instance (VSI). The {{site.data.keyword.ibmi-vst}} limits the size of the VSI. But, you can select any physical system that supports the selected {{site.data.keyword.ibmi-vst}}. For example, a virtual server that is assigned to a P10 tier can run on either an S1022 or an E1080 server. The tier restricts the resource allocation for the VSI, not its hardware compatibility.

The {{site.data.keyword.ibmi-vst}} determines the pricing tier for the IBM i operating system and licensed program products (LPPs). It also defines the limits for the following resources:
- Maximum number of virtual processors
- Maximum memory size

You can dynamically adjust the number of CPUs and the memory size if the numbers are within the {{site.data.keyword.ibmi-vst}} limits. To expand the size beyond the limit of the current {{site.data.keyword.ibmi-vst}}, you must follow these steps:
1. Power off the VSI.
2. Change the {{site.data.keyword.ibmi-vst}} to a tier that aligns with your resource requirements.

For more information, see [Supported resource limits by the IBM i software tier](/docs/power-iaas?topic=power-iaas-ibmi-vsw-tiers#ibmi-vsw-vp-mem).

When you change the software tier, the billing for the {{site.data.keyword.ibmi-vst}} automatically changes to reflect the selected tier.

You can generate an estimate of {{site.data.keyword.powerSys_notm}} resources with an {{site.data.keyword.ibmi-vst}} before you deploy the resources. For more information, see [Estimating a virtual server instance](/docs/power-iaas?topic=power-iaas-generating-an-estimate#est-vsi).

You must complete the following prerequisites to assign an {{site.data.keyword.ibmi-vst}} to a {{site.data.keyword.powerSys_notm}} instance:

- Select an IBM i image with version 7.3 or later from the **Image** list under the **Boot image** section.
- Select an IBM Power10 or later server type from the **Machine type** list.
- Complete the following steps to assign a VSN to the instance:
  - Edit the **Virtual serial number (VSN)** field.
  - The Virtual serial number (VSN) summary pane appears.
  - Select either **Auto-assign** or **Select from retained VSNs** option to assign a VSN.

A list of supported {{site.data.keyword.ibmi-vst}}s is displayed in the **{{site.data.keyword.ibmi-vst}}** list based on the machine type. A recommended {{site.data.keyword.ibmi-vst}} is displayed based on the number of cores and memory size that you select. You can select the recommended {{site.data.keyword.ibmi-vst}} from the **{{site.data.keyword.ibmi-vst}}** list or other options from the list.

For more information, see [Configuring a Power Virtual Server instance](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#configuring-instance).



## Supported resource limits by the {{site.data.keyword.ibmi-vst}}
{: #ibmi-vsw-vp-mem}

For each {{site.data.keyword.ibmi-vst}}, the supported limits for resources are defined. These limits help align resource usage with software licensing costs. You must understand the supported limits of resources for planning your VSI size and ensure compliance with IBM i licensing models.

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

All {{site.data.keyword.ibmi-vst}}s are not supported on all the {{site.data.keyword.powerSys_notm}} system types. The following table shows which {{site.data.keyword.ibmi-vst}}s are compatible with each system type.



| System types | Supported IBM i software tiers | | | |
| ----------- | --- | --- | --- | --- |
|             | P05 | P10 | P20 | P30 |
| S1022       | Yes | Yes | Yes | No  |
| S1122       | Yes | Yes | Yes | No  |
| E1080       | No  | Yes | Yes | Yes |
| E1180       | No  | Yes | Yes | Yes |
{: caption="Supported {{site.data.keyword.ibmi-vst}}s on {{site.data.keyword.powerSys_notm}}s" caption-side="bottom"}





IBM i is not supported on IBM E1050 and E1150 system types.
{: note}





If you deploy multiple IBM i virtual server instances (VSIs) simultaneously on the IBM S1022 hosts using the P20 IBM i software tiers, the deployment might fail when the IBM data center is being upgraded. However, the deployment of a single VSI is supported.
{: restriction}
