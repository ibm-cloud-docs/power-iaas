---

copyright:
  years: 2023, 2024

lastupdated: "2024-10-21"

keywords: managing virtual tape library, ppcaas, virtual tape library, VTL IBM, VTL, tape library, FalconStor, VTL deployment guide

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Managing a Virtual Tape Library
{: #manage-vtl}

---



{{site.data.keyword.off-prem-fname}}: [{{site.data.keyword.off-prem}}]{: tag-blue}


{{site.data.keyword.on-prem-fname}}: [{{site.data.keyword.on-prem}}]{: tag-red}


---

FalconStor Virtual Tape Library (VTL) is an optimized backup and deduplication solution that provides tape library emulation, high-speed backup or restore, data archival to supported S3 clouds for long-term storage, global data deduplication, enterprise-wide replication, and long-term cloud-based container archive, without requiring changes to the existing environment.
{: shortdesc}

Here are some of the StorSafe VTL Benefits
* Up to 95% data reduction. FalconStor reduces the storage capacity required by backup data on-premises and in the cloud by up to 95%.
* Ransomware Protection. Recover data from any point in time with air-gapped, immutable backups.
* Offsite Protection. For offsite protection, StorSafe VTL exports virtual tapes as physical tapes, and keeps track of their location with a management dashboard. Virtual tapes can remain in the library for fast restores or can be stubbed when exported to local object storage.
* High Performance. Improve both backup and recovery.
* Modernize. FalconStor is 100% compatible with existing backup software, hardware, and operational procedures.

VTL is offered through the IBM Cloud Catalog for both {{site.data.keyword.off-prem}} and {{site.data.keyword.on-prem}} with the following names:
- [FalconStor StorSafe VTL for Power On-Premises](https://cloud.ibm.com/catalog/services/falconstor-storsafe-vtl-for-power-on-premises){: external} and
- [FalconStor StorSafe VTL for PowerVS Cloud](https://cloud.ibm.com/catalog/content/vtltile-tags-v10.03-01-f1e88e51-7e3d-4fbc-a7ed-3ab9adb2afea-global){: external}.

For more information on how to create and configure an {{site.data.keyword.powerSysFull}} running the FalconStor VTL software in the {{site.data.keyword.cloud}}, see [FalconStor VTL for IBM Deployment Guide](https://falconstor-download.s3.us-east.cloud-object-storage.appdomain.cloud/FalconStor%20VTL%20for%20IBM%20Deployment%20Guide.pdf){: external}.

## Migrating by using Falconstor StorSafe VTL
{: #storsafe-migr}

See [FalconStor StorSafe VTL](/docs/power-iaas?topic=power-iaas-migration-strategies-managed-thirdparty#storsafe-vtl) for migration steps.
