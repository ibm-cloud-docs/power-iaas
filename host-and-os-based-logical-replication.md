---

copyright:
  years: 2022, 2024

lastupdated: "2024-05-31"

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

- Db2 HADR
- [Rocket iCluster HA/DR](https://cloud.ibm.com/catalog/content/poc-iClusterNew-df2ab864-0eb4-4645-8c08-f08e008e66bd-global)
- Maxava HA
- [Migrate 23](https://cloud.ibm.com/catalog/services/bus4i-system-copy---migrate-23-for-power-i)
- MIMIX
- Oracle Data Guard
- Oracle Goldengate

