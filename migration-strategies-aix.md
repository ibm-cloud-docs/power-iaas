﻿---

copyright:
  years: 2019, 2024

lastupdated: "2024-12-06"

keywords: migration strategies, AIX, NIM, savevg, mksysb, AIX migration

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Migration strategies for AIX
{: #migration-aix}

---



{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}


---

Learn about the various AIX migration strategies for {{site.data.keyword.powerSysFull}}.

## Migrating an AIX-based Oracle database
{: #oracle-mig-ref}

To migrate an AIX-based Oracle database from IBM Power to Power Virtual Server, see [Oracle technical migration procedure](https://cloud.ibm.com/media/docs/downloads/power-iaas/Oracle_Technical_Migration_procedure.pdf){: external}.


## Migrating Db2 on AIX to {{site.data.keyword.powerSys_notm}}
{: #db2-migration-ref}

See the use case on [Migrating Db2 on AIX to {{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-db2-migration) for complete information.

## Migrating client-managed environment to {{site.data.keyword.powerSys_notm}}
{: #mig-onprem-cloud}

See the [Move data from client-managed environment to {{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-move-data-to-cloud) topic for complete information.

## Migrating by using NIM on {{site.data.keyword.powerSys_notm}}
{: #mig-nim}

You can configure your Network Installation Management (NIM) server on a {{site.data.keyword.powerSys_notm}} and migrate an AIX virtual server instance from AIX 7.1 to AIX 7.2 or 7.3, and other operations.

See [Migrating by using NIM on {{site.data.keyword.powerSys_notm}}](https://www.ibm.com/support/pages/node/7033798){: external} for more information.

## Migration by using MKSYSB
{: #migration-mksysb}

You can migrate your data by using the `mksysb` command:

1. Back up the client-managed environment OS image with the `alt_disk_mksysb` command and transfer it to Cloud Object Storage.
2. Create a {{site.data.keyword.powerSys_notm}} and import the image.
3. Restore the client-managed environment OS image.

For more information, see [Restoring an AIX mksysb image onto a {{site.data.keyword.powerSys_notm}} instance](/docs/power-iaas?topic=power-iaas-restoring-aix-mksysb-image).

## Alternative AIX migration strategies
{: #migration-alternative-aix}

Some alternative AIX migration strategies include:

- `rsync` for nondatabase files
- Log shipping for databases
