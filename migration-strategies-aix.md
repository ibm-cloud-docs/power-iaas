---

copyright:
  years: 2019, 2024

lastupdated: "2024-05-24"

keywords: migration strategies, AIX, NIM, savevg, mksysb, AIX migration

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

Learn about the various AIX migration strategies for {{site.data.keyword.powerSysFull}}.

## Migrating your on-premise environment to {{site.data.keyword.powerSys_notm}}
{: #mig-onprem-cloud}

See the [Move data from your on-premise environment to {{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-move-data-to-cloud) topic for complete information.

## Migrating using NIM on {{site.data.keyword.powerSys_notm}}
{: #mig-nim}

You can configure your Network Installation Management (NIM) server on a {{site.data.keyword.powerSys_notm}} and migrate an AIX virtual server instance from AIX 7.1 to AIX 7.2/7.3, as well as other operations.

See [Migrating using NIM on {{site.data.keyword.powerSys_notm}}](https://www.ibm.com/support/pages/node/7033798){: external} for more information.

## Migration by using MKSYSB
{: #migration-mksysb}

You can migrate your data by using the `mksysb` command:

1. Back up the on-premises OS with the `alt_disk_mksysb` command and transfer it to COS.
2. Create a {{site.data.keyword.powerSys_notm}} and import the image.
3. Restore the on-premises image.

For more information, see [Restoring an AIX mksysb image onto a {{site.data.keyword.powerSys_notm}} instance](/docs/power-iaas?topic=power-iaas-restoring-aix-mksysb-image).

## Alternative AIX migration strategies
{: #migration-alternative-aix}

Some alternative AIX migration strategies include:

- `rsync` for nondatabase files
- Log shipping for databases

For a complete tutorial on migrating your AIX workloads to {{site.data.keyword.powerSys_notm}}s, see [Migrating AIX to IBM {{site.data.keyword.powerSys_notm}}s](https://cloud.ibm.com/media/docs/downloads/power-iaas-tutorials/PowerVS_AIX_Migration_Tutorial_v1.pdf){: external}.