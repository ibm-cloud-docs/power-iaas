---

copyright:
  years: 2019, 2024

lastupdated: "2024-05-14"

keywords: migration strategies, cos, mass data migration, pwoervc, backup and restore, replication, aspera, mksysb, aws cli, pip, yum

subcollection: power-iaas

---

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
{:video: .video}
{{site.data.keyword.attribute-definition-list}}

# Migration strategies for AIX
{: #migration-aix}

Learn about migration strategies that are specific to AIX systems.

## Migration by using MKSYSB
{: #migration-mksysb}

You can migrate your data by using the `mksysb` command:

1. Back up the on-premises OS with the `alt_disk_mksysb` command and transfer it to COS.
2. Create a {{site.data.keyword.powerSys_notm}} and import the image.
3. Restore the on-premises image.

For more information, see [Restoring an AIX mksysb image onto a {{site.data.keyword.powerSys_notm}} instance](/docs/power-iaas?topic=power-iaas-restoring-aix-mksysb-image).

## Logical replication with GLVM and PowerHA SystemMirror for AIX Enterprise Edition
{: #logical-replication}

GLVM is an OS-based IP replication strategy. It is based on the AIX LVM and enables data and logical volume mirroring across geographically distant locations. GLVM supports both synchronous and asynchronous modes. You can integrate PowerHA SystemMirror (Enterprise Edition) for network monitoring and automated failover support.

- [Geographic Logical Volume Manager (GLVM)](https://www.ibm.com/support/knowledgecenter/en/SSPHQG_7.2/glvm/ha_glvm_glvm.html){: external}
- [Configuring geographically mirrored volume groups](https://www.ibm.com/support/knowledgecenter/en/SSPHQG_7.2/glvm/ha_glvm_config_glvm.html){: external}
- [Using IBM PowerHA SystemMirror V6.1 for AIX Enterprise Edition](http://www.redbooks.ibm.com/redbooks/pdfs/sg247841.pdf){: external}
- [PowerHA SystemMirror for AIX 7.2](https://www.ibm.com/support/knowledgecenter/en/SSPHQG_7.2/navigation/welcome.html){: external}
- [IBM PowerHA SystemMirror for AIX Cookbook](http://www.redbooks.ibm.com/abstracts/sg247739.html){: external}

## Alternative AIX migration strategies
{: #migration-alternative-aix}

Some alternative AIX migration strategies include:

- `rsync` for nondatabase files
- The `savevg` and `restvg` AIX commands
- Log shipping for databases

For a complete tutorial on migrating your AIX workloads to {{site.data.keyword.powerSys_notm}}s, see [Migrating AIX to IBM {{site.data.keyword.powerSys_notm}}s](https://cloud.ibm.com/media/docs/downloads/power-iaas-tutorials/PowerVS_AIX_Migration_Tutorial_v1.pdf){: external}.