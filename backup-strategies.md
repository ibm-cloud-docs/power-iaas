---

copyright:
  years: 2023, 2024

lastupdated: "2024-01-05"

keywords: backup strategy, {{site.data.keyword.powerSys_notm}} as a service, private cloud, terminology

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Backup strategies
{: #backup-strategies}

Learn more about different AIX and IBM i backup strategies for {{site.data.keyword.powerSysFull}}.
{: shortdesc}

[Private Cloud]{: tag-red} Your application configuration and data are not backed up automatically. To recover from a disaster, IBM backs up your configuration data that is required to rebuild a pod. The configuration data includes the virtual machine configurations and private cloud image repositories. However, backup and restoration of client data and client OS images is your responsibility.

## Image capture
{: #backup-image-capture}

This function produces a storage Flash Copy of the virtual server and works for any operating system. You can capture the VM images within your account locally as a part of your image catalog in {{site.data.keyword.powerSys_notm}}, or directly to IBM Cloud Object Storage, or both. For instructions, see [Capturing and exporting a VM](/docs-draft/power-iaas?topic=power-iaas-capturing-exporting-vm).

Importing and exporting images requires a considerable amount of processing power and network bandwidth. As a result, you can submit only one import or export request before it is queued. Typically, users import or export system disks (AIX rootvg disks) that are smaller in size (**less than 1 TB**) to facilitate the transfer to and from Cloud Object Storage. If your image size is greater than 1 TB, your transfer might take a long time and is prone to failure. The maximum [uncompressed ]{: tag-teal}image size that you can import or export is **10 TB**.

[Private Cloud]{: tag-red} For advanced backup options, you must use your own backup strategy and tools. You can use software such as IBM Storage Protect and solution-based technologies such as SAP HANA replication.

## Snapshots
{: #snapshots}

This function provides the capability to capture full, point-in-time copies of entire logical volumes or data sets. You can also restore your virtual server in case a critical failure occurs. For instructions, see [Snapshots, cloning, and restoring](/docs-draft/power-iaas?topic=power-iaas-snapshots-cloning)

## AIX backup strategies
{: #backup-aix}

{{site.data.keyword.powerSys_notm}} users can implement any compatible agent-based backup for AIX virtual machines (VM). *Veeam for AIX* and *IBM Storage Protect* (formerly *IBM Spectrum Protect*) are two commonly used backup strategies.

- *Veeam for AIX* - See [Additional backup strategies](/docs-draft/power-iaas?topic=power-iaas-backup-strategies#add-backup) for more information.

- *IBM Storage Protect* provides scalable data protection for physical file servers, applications, and virtual environments. Organizations can scale up to manage billions of objects per backup server. They can reduce backup infrastructure costs with built-in data efficiency capabilities and the ability to migrate data to tape, public cloud services, and on-premises object storage. *IBM Storage Protect* can also be a data offload target for *IBM Storage Protect Plus,* for a long-term data retention and disaster recovery. For more information, see [What can IBM Storage Protect do for your business?](https://www.ibm.com/products/storage-protect){: external}.

It's the user's responsibility to set up and maintain these environments. Remember to check for any connectivity and bandwidth restrictions to the LPAR server. Your LPAR servers can also use {{site.data.keyword.cos_full_notm}} as a repository.

For a complete tutorial on backing up and restoring AIX VM data, see [Backing up and restoring data in an AIX VM](https://cloud.ibm.com/media/docs/downloads/power-iaas-tutorials/PowerVS_AIX_Backups_Tutorial_v1.pdf){: external}.

For best practices and guidelines on AIX backup performance on {{site.data.keyword.powerSysFull}}, see [AIX Backup Performance Best Practices and Guidelines on IBM Power Systems Virtual Server](https://cloud.ibm.com/media/docs/downloads/power-iaas/PowerVS_AIX_Backup_Performance_Best_Practices_and_Guidelines_v1_0_03012022.pdf){: external}.<!--The PDF has the title with "Systems". So, the name is not changed-->

### IBM i backup strategies
{: #backup-ibmi}

A common IBM i backup strategy is to use IBM® Backup, Recovery, and Media Services (BRMS) and IBM Cloud Storage Solutions (ICC). Together, these products automatically back up your LPARs to {{site.data.keyword.cos_full_notm}}. The ICC product can be integrated with BRMS to move and retrieve objects from remote locations, including Cloud Object Storage. In most cases, this process involves backing up to virtual tapes and image catalogs. Note, you might need extra storage for the LPAR to host the image catalogs until they are moved to Cloud Object Storage.

The typical IBM i customer uses the following flow to back up LPARs and objects:

1. Use the 5733-ICC product to connect to Cloud Object Storage (COS) (~2 times the disk capacity to hold the backup images).
2. Connect to IBM COS by following the steps mentioned in [Using Cloud Object Storage](/docs-draft/power-iaas?topic=power-iaas-backup-strategies#cos-over-directlink).
3. Complete the back up to COS by choosing the speed and resiliency that is required.

   - [Working with files in Cloud Storage Solutions](https://www.ibm.com/docs/en/i/7.5?topic=guide-working-files-in-cloud-storage-solutions){: external}
   - [BRMS with Cloud Storage Solutions for i considerations and requirements](https://www.ibm.com/docs/en/i/7.5?topic=i-brms-cloud-storage-solutions-considerations-requirements){: external}
   - [Data backup and recovery by using BRMS and IBM Cloud Storage Solutions for i](https://www.ibm.com/docs/en/i/7.5?topic=ubcssi-data-backup-recovery-using-brms-cloud-storage-solutions-i){: external}

For a complete tutorial on backing up and restoring IBM i VM data, see [Backing up and restoring data in an IBM i VM](https://cloud.ibm.com/media/docs/downloads/power-iaas-tutorials/PowerVS_IBMi_Backups_Tutorial_v1.pdf){: external}.

## Using Cloud Object Storage
{: #cos-over-directlink}

[On Cloud]{: tag-blue}

The preferred way to connect to Cloud Object Storage (COS) from a VM in {{site.data.keyword.powerSys_notm}} are as follows:

1.  In a PER workspace, attach the {{site.data.keyword.powerSys_notm}} workspace to a Transit Gateway and directly access the COS direct endpoint. See, [Attaching Transit Gateway to a PER workspace](/docs-draft/power-iaas?topic=power-iaas-per#attaching-transit-gateway-to-a-per-workspace).
2.  In a non-PER workspace that are in a multi-zone region (MZR) the best way to connect to COS is as follows:
    1. Create a [Virtual Private Cloud (VPC) with subnet(s)](/docs/vpc?topic=vpc-subnets-configure&interface=ui#subnets-create-ui) in the same region as your {{site.data.keyword.powerSys_notm}} workspace.
    2. Create a [Virtual Private Endpoint gateway](/docs/vpc?topic=vpc-ordering-endpoint-gateway&interface=ui) (VPE).
    3. Connect the VPC to a [Transit Gateway](/docs/transit-gateway?topic=transit-gateway-ordering-transit-gateway&interface=ui#tg-ui-creating-transit-gateway).
    4. [Create a cloud connection](/docs-draft/power-iaas?topic=power-iaas-cloud-connections#create-cloud-connections) to connect the non-PER {{site.data.keyword.powerSys_notm}} workspace to the same transit gateway.

    The {{site.data.keyword.powerSys_notm}} would then use the VPE's IP address to connect to COS. A Custom Resolver (CR) is needed by the {{site.data.keyword.powerSys_notm}} to reach the COS. If the VPE has multiple IP addresses, you can set up custom DNS and a custom hostname to connect to COS.
3.  Deploy a Nginx reverse proxy server in either the classic or VPC infrastructure.

    Nginx is a mature, compact, and fast open source web server that excels at specialized tasks, including the reverse proxy server role. For information on setting up a Nginx reverse proxy server, see [Installing your Nginx reverse proxy](/docs/direct-link?topic=direct-link-using-ibm-cloud-direct-link-to-connect-to-ibm-cloud-object-storage#direct-link-installing-your-nginx-reverse-proxy).

[Private Cloud]{: tag-red}: You must setup the connection from a virtual machine to Cloud Object Storage (COS) as required.

### Cloud Object Storage on AIX
{: #cos-aix}

IBM Power that are running AIX 7.2 TL3, or later, have a script that is located in the path, `/usr/samples/nim/cloud_setup`. The `cloud_setup` command installs the command-line environment for cloud storage services.

```text
cloud_setup [-I | G | C] [-v]

-I: Install the necessary RPMs for universal CLI (supports COS).
-G: Install the necessary RPMs for gsutil CLI (Google Cloud Storage).
-C: Install the necessary RPMs for cloud-init.
-v: Enable debug output.
```

1. To begin, copy the file to the system that requires AWS and give it execute permission.

2. Enter the `cloud_setup -I` command to install the AWS CLI and all of the dependant RPMs.

3. After the installation is complete, you must configure `awscli` for access to COS and provide the correct region (where your bucket COS is defined) in the `aws --endpoint-url` s3 command. In the following example, the **us-east** region is used:

```text
# export PATH=$PATH:/opt/freeware/bin

# aws configure
AWS Access Key ID [None]: d197axxxxxxxxxxxxxxxxxxxxxxxxxxxa4
AWS Secret Access Key [None]: f52a5xxxxxxxxxxxxxxxxxxxxxxx001a33b74d8
Default region name [None]: us-east
Default output format [None]: json

# aws --endpoint-url https://s3.us-east.cloud-object-storage.appdomain.cloud s3 ls
2019-01-28 13:32:40 poweriaastest

# aws --endpoint-url https://s3.us-east.cloud-object-storage.appdomain.cloud s3 ls s3://poweriaastest
2019-01-28 13:33:42 6832 nimstat.sh
2019-01-28 15:05:25 1380725 yum-3.4.3-5.aix6.1.noarch.rpm
```

## Additional backup strategies
{: #add-backup}

The additional backup strategies that you can use are as follows:
- FalconStor StorSafe VTL - For more information see [FalconStor StorSafe VTL](/docs-draft/power-iaas?topic=power-iaas-migration-strategies-power#falconstor-storsafe-vtl).
- Veeam for AIX - It provides simple physical server backup solutions for machines that are running in respective UNIX® operating systems. With them, IT organizations can provide industry-leading file-based backup and disaster recovery for their environments. For more information, see [Veeam Agents for IBM AIX](https://www.veeam.com/ibm-aix-oracle-solaris-backup.html){: external}.

### Ordering Veeam standalone licenses
{: #backup_veeam_ordering_licenses}

You can order a Veeam® standalone license, via IBM Cloud portal [Order Veeam Licesne](https://cloud.ibm.com/infrastructure/vmware-solutions/console/instances/licenses)

An email will be sent confirming the order. Should the order be incorrect, it can be deleted. For more information, see [Managing Veeam licenses](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_managing_licenses).

A license key will be generated and emailed to whomever placed the order.

## Managed services and IBM resiliency services
{: #managed-services}

Contact an IBM representative if you need help with understanding the different backup lifecycle processes.
