---

copyright:
  years: 2019, 2024

lastupdated: "2024-07-22"

keywords: migration strategies, cos, mass data migration, pwoervc, backup and restore, replication, aspera, mksysb, aws cli, pip, yum

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Using third-party tools for migration
{: #migration-strategies-managed-thirdparty}




You can use the third-party tools to complete your data migration. The following third-party tools are commonly used for data migration:
{: shortdesc}

- Double-Take® MoveTM for AIX
- [Falconstor StorSafe VTL](https://cloud.ibm.com/catalog/content/vtltile-tags-v10.03-01-f1e88e51-7e3d-4fbc-a7ed-3ab9adb2afea-global)
- [Rocket iCluster HA/DR](https://cloud.ibm.com/catalog/content/poc-iClusterNew-df2ab864-0eb4-4645-8c08-f08e008e66bd-global)
- Maxava HA
- [Migrate 23](https://cloud.ibm.com/catalog/services/bus4i-system-copy---migrate-23-for-power-i)
- MIMIX

## FalconStor StorSafe VTL
{: #storsafe-vtl}

StorSafe VTL is an IBM-certified solution for migration, backup optimization, archive, and data recovery (DR).

StorSafe VTL is software that emulates physical tape drives and libraries to optimize backup and recovery. It works for both in the cloud and On-premises. It enables simple and easy migration from On-premises to {{site.data.keyword.powerSysFull}}. StorSafe VTL can backup IBM i or AIX workloads On-premises, replicate to a cloud-resident StorSafe VTL, and then restore to a {{site.data.keyword.powerSys_notm}}. Similarly, legacy tapes can be handled.

Following are some of the features of StorSafe VTL:
- Nondisruptive and secure process that can scale to PB-sized workloads.
- Deduplication and replication improve performance and reduces storage capacity.
- The same tool for On-premises and cloud that enables both workload and tape migrations.
- System and application data are deduplicated and compressed before transmitting over the network, thereby accelerating migration, even on the initial baseline transfer.
- Replicated tapes land in Cloud Object Storage and can be used by the cloud VTL as a backup baseline without copying the data.
- Migration uses existing backup processes and tools by using existing environment and knowledge.
- Data replication can occur over time as part of the backups with final sync replication completed fast during regular backup windows.
- FalconStor StorSafe VTL for {{site.data.keyword.powerSys_notm}} can take advantage of IBM low-cost Cloud Object Storage storage for its repository.

### Migrating an IBM i system
{: #mig-storsafe-ibmi}

See the video that shows migration of an IBM i system from On-premises to {{site.data.keyword.powerSys_notm}} - [Migration of an IBM i system](https://www.youtube.com/watch?v=E9_B5n3FYOM){: external}.



You can access StorSafe VTL from the [IBM Cloud catalog](https://cloud.ibm.com/catalog). In the search field, enter `FalconStor StorSafe VTL for PowerVS Cloud` or `FalconStor StorSafe VTL for Power On-Premises`.

### FalconStor StorSafe VTL for Cloud
{: #storsafe-cloud}

FalconStor StorSafe VTL for {{site.data.keyword.powerSys_notm}} comes bundled with OS and can be deployed from the IBM Cloud catalog with one click.

### FalconStor StorSafe VTL for On-Premises
{: #storsafe-onprem}

FalconStor StorSafe VTL for On-premises provides flexible deployment options for the user:
-	It can be installed on any X86 server that is on [Falconstor certification matrix](https://www.falconstor.com/support/certification-matrix/server-hardware/){: external}.
-	It can be installed as a VM in Hypervisors such as VMware, HyperV, Xen, and KVM.
-	It can be installed inside {{site.data.keyword.powerSys_notm}} as an LPAR.

### Migration Services
{: #mig-services}

Services to help migration are available from IBM, FalconStor, and Authorized Migration Partners. Reach out if you would like more information about using migration services or becoming a FalconStor Migration Partner at [PowerVSMigration@falconstor.com](mailto:PowerVSMigration@falconstor.com).

If you need any help with deploying FalconStor StorSafe VTL, see [FalconStor VTL for IBM Deployment Guide](https://falconstor-download.s3.us-east.cloud-object-storage.appdomain.cloud/FalconStor%20VTL%20for%20IBM%20Deployment%20Guide.pdf){: external}.

For more information on FalconStor StorSafe VTL, see [www.falconstor.com](https://www.falconstor.com/){: external}.
