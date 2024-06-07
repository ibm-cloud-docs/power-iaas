---

copyright:
  years: 2019, 2024

lastupdated: "2024-06-06"

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

# Additional migration strategies
{: #additional-migration-strategies-power}

## IBM teams and managed services
{: #teams-managed-services}

You can engage IBM teams and services to assist you throughout the migration lifecycle.

- [Expert Labs](https://www.ibm.com/products/expertlabs){: external}
- [IBM Services for Cloud Migration](https://www.ibm.com/services/cloud/migration){: external}

## Aspera Technologies
{: #aspera-technologies}

IBM Aspera&reg; on Cloud is a hosted service that quickly and reliably moves and shares your data sets across a hybrid cloud environment. IBM Aspera can help transfer data to the IBM Cloud for later retrieval from the {{site.data.keyword.powerSys_notm}} environment. For more information, see [IBM Aspera on Cloud](https://www.ibm.com/products/aspera){: external}.

Use the [Accelerated network transfer migration guide](https://cloud.ibm.com/media/docs/downloads/power-iaas/accelerated_migration.pdf){: external} powered by Aspera to accelerate the transfer of your migration content. It helps you to directly transfer the migration content to the {{site.data.keyword.powerSys_notm}} workspace and you achieve faster time to value from IBM cloud.

## IBM Cloud Object Storage (COS)
{: #migration-icos}

COS can be used as an intermediary location to store files from your on-premises environment. You can retrieve and send your files to the {{site.data.keyword.powerSys_notm}} environment from this location. You must create COS buckets to transfer data over the public internet or privately secured links. For more information, see [IBM Cloud Object Storage: FAQ](https://www.ibm.com/cloud/object-storage/faq){: external}.

To copy data from COS to your AIX virtual machine (VM), you must install the [Amazon Web Services (AWS) CLI](/docs/cloud-object-storage?topic=cloud-object-storage-aws-cli) by using either the **Yellowdog Updater, Modified (yum)** or **Pip installs Python pip (pip)** package managers. If you use the yum package manager, you can install the AWS CLI with the `yum install aws-cli` command. For the pip package manager, you can use `pip install awscli` to install the AWS CLI. After the installation, you can use the universal S3 commands that are supported by AWS to copy objects.

You can also find a script that ships (as a sample command) with AIX 7.2 TL3, or later, that simplifies the installation of yum, pip, and the AWS CLI. You can find the script at: `/usr/samples/nim/cloud_setup`.

- [Uses of AIX toolbox for open source software](https://www.ibm.com/support/pages/node/882892){: external}
- [Python for AIX](https://www.ibm.com/support/pages/node/883796){: external}

For an IBM i VM, you must use the [Cloud Storage Solution for IBM i product (5733-ICC)](https://www.ibm.com/support/pages/ibm-cloud-storage-solutions-i){: external} to communicate with COS and transfer data.

## PowerVC images and COS
{: #migration-powervc-icos}

If you have an environment with access to PowerVC, you can capture OVA images to easily migrate your data. Using the {{site.data.keyword.powerSys_notm}} offering, you can provision a new virtual server based on an OVA image. To accomplish this, regardless of the operating system (OS), you must complete the following steps:

1. Create an OVA image on your local system.
2. Copy the OVA image to your **Cloud Object Storage** account.
3. [Deploy the OVA image and provision a new {{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-deploy-custom-image).
