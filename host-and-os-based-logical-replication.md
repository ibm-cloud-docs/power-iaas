---

copyright:
  years: 2022, 2024

lastupdated: "2024-10-05"

keywords: Host and OS based logical replication, Replication, Application specific replication, 

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Host and OS-based logical replication
{: #replication-host}

IBM recommends that you use PowerHA SystemMirror (Enterprise Edition) with Geographic Mirroring (Geo mirroring) and Geographic Logical Volume Manager (GLVM). The following host and OS-based logical replication options exist depending on your OS:

- **AIX** - GLVM
- **IBM i** - Geo mirroring

## Application-specific replication
{: #replication-app}

Applications might have replication mechanisms that can sync multiple environments. These options are commonly used for application-specific replication:

- *Db2 HADR*
- *Oracle Data Guard*
- *Oracle Goldengate*
- *iCluster*
- *MIMIX from Syncsort*
- *Maxava HA*


