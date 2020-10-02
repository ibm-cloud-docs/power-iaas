---

copyright:
  years: 2019, 2020

lastupdated: "2020-04-29"

keywords: backup strategies, cos, brms, icc, veam for aix, ibm spectrum support, cloud setup, direct link, reverse proxy

subcollection: power-iaas

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:preview: .preview}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}

# Backup strategies for IBM Power Systems Virtual Servers
{: #backup-strategies}

Learn more about different AIX and IBM i backup strategies for the IBM&reg; Power Systems&trade; Virtual Server service.
{: shortdesc}

## Image capture
{: #backup-image-capture}

Image capture produces a storage FlashCopy of the logical partition (LPAR) and works on both IBM i or AIX virtual machines (VMs). You can use image capture to store backup images within your account (locally), directly to [IBM Cloud Object Storage (COS)](https://cloud.ibm.com/docs/power-iaas?topic=power-iaas-capturing-exporting-vm), or both.

Importing and exporting images requires a considerable amount of processing power and network bandwidth. As a result, you can submit only one import or export request before it is queued. Typically, users import or export system disks (AIX rootvg disks) that are smaller in size (**less than 1 TB**) to facilitate the transfer to and from COS. If your image size is greater than 1 TB, your transfer might take a long time and is prone to failure. The maximum image size that you can import or export is **10 TB**.

## AIX backup strategies
{: #backup-aix}

{{site.data.keyword.powerSys_notm}} users can implement any compatible agent-based backup for AIX virtual machines (VM). *Veeam for AIX* and *IBM Spectrum Protect* are two commonly used backup strategies.

- *Veeam for AIX* provides simple physical server backup solutions for machines that are running in respective UNIX&reg; operating systems. With them, IT organizations can provide industry-leading file-based backup and disaster recovery for their environments. For more information, see [Veeam Agents for IBM AIX](https://www.veeam.com/ibm-aix-oracle-solaris-backup.html){: new_window}{: external}.
- *IBM Spectrum Protect* provides scalable data protection for physical file servers, applications, and virtual environments. Organizations can scale up to manage billions of objects per backup server. They can reduce backup infrastructure costs with built-in data efficiency capabilities and the ability to migrate data to tape, public cloud services, and on-premises object storage. *IBM Spectrum Protect* can also be a data offload target for *IBM Spectrum Protect Plus,* providing the ability to use your existing investment for long-term data retention and disaster recovery. For more information, see [What can IBM Spectrum Protect do for your business?](https://www.ibm.com/us-en/marketplace/data-protection-and-recovery){: new_window}{: external}.

It's the user's responsibility to set up and maintain these environments. Remember to check for any connectivity and bandwidth restrictions to the LPAR server. Your LPAR servers can also use {{site.data.keyword.cos_full_notm}} as a repository. 

For a complete tutorial on backing up and restoring AIX VM data, see [Backing up and restoring data in an AIX VM](https://cloud.ibm.com/media/docs/downloads/power-iaas-tutorials/PowerVS_AIX_Backup_Tutorial.pdf).

## IBM i backup strategies
{: #backup-ibmi}

A common IBM i backup strategy is to use IBM® Backup, Recovery, and Media Services (BRMS) and IBM Cloud Storage Solutions (ICC). Together, these products automatically back up your LPARs to {{site.data.keyword.cos_full_notm}}. The ICC product can be integrated with BRMS to move and retrieve objects from remote locations, including COS. In most cases, this process involves backing up to virtual tapes and image catalogs. Note, you might need extra storage for the LPAR to host the image catalogs until they are moved to COS.

The typical IBM i customer uses the following flow to perform a backup:

1. Use the 5733-ICC product to connect to COS (~2 times the disk capacity to hold the backup images).
2. Connect to IBM's classic infrastructure by using Direct Link Connect.
3. Create a Nginx reverse proxy. You can provision the reverse proxy from a virtual server instance (x86) for bandwidth up to 1 Gbps. If more bandwidth is needed, you must use a bare metal server.
4. Complete the back up to COS by choosing the speed and resiliency that is required.

   - [Working with ICC](https://www.ibm.com/support/knowledgecenter/ssw_ibm_i_72/icc/topics/iccucon_commands_cloud_overview.htm){: new_window}{: external}
   - [BRMS with Cloud Storage Solutions for i considerations and requirements](https://www.ibm.com/support/knowledgecenter/en/ssw_ibm_i_74/rzai8/rzai8brmscloudrequireandconsider.htm){: new_window}{: external}
   - [Data backup and recovery by using BRMS and IBM Cloud Storage Solutions for i](https://www.ibm.com/support/knowledgecenter/en/ssw_ibm_i_74/rzai8/rzai8backupandrecoveryusingBRMSandICC.htm){: new_window}{: external}

## Using COS over IBM Cloud Direct Link
{: #cos-over-directlink}

IBM Cloud customers who purchase COS and Direct Link can make remote connections to COS private endpoints. This type of connection extends the advantages of private service endpoints, so they can be used by client systems outside of IBM Cloud facilities.

HTTPS (secure HTTP) COS requests are initiated from a client at a remote site. They're transmitted securely through IBM Cloud Direct Link, targeting one of a cluster of reverse proxy servers deployed in a customer’s IBM Cloud account. From there, requests are passed to a COS private endpoint, processed, and then the results returned to the remote calling client.

Any sample client code that works with COS should also work through a [reverse proxy server](/docs/direct-link?topic=direct-link-using-ibm-cloud-direct-link-to-connect-to-ibm-cloud-object-storage#direct-link-installing-your-nginx-reverse-proxy). The only change that is required is that, instead of targeting a COS private endpoint URL published by IBM, the client targets the IP address or URL of the reverse proxy server. Nginx is a mature, compact, and fast open source web server that excels at specialized tasks, including the reverse proxy server role. For information on setting up a Nginx reverse proxy server, see [Installing your Nginx reverse proxy](/docs/direct-link?topic=direct-link-using-ibm-cloud-direct-link-to-connect-to-ibm-cloud-object-storage#direct-link-installing-your-nginx-reverse-proxy).

IBM Power Systems that are running AIX 7.2 TL3, or later, have a script located in the path, `/usr/samples/nim/cloud_setup`. The `cloud_setup` command installs the command line environment for cloud storage services.

```
cloud_setup [-I | G | C] [-v]

-I: Install the necessary RPMs for universal CLI (supports COS).
-G: Install the necessary RPMs for gsutil CLI (Google Cloud Storage).
-C: Install the necessary RPMs for cloud-init.
-v: Enable debug output.
```

1. To begin, copy the file to the system which requires AWS and give it execute permission.

2. Enter the `cloud_setup -I` command to install the AWS CLI and all of the dependant RPMs.

3. Once installed, you must configure `awscli` for access to COS and provide the correct region (where youre bucket COS is defined) in the `aws --endpoint-url` s3 command. In the following example, the **us-east** region is used:

```
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

## Managed services and IBM resiliency services
{: #managed-services}

Contact an IBM representative if you need help with understanding the different backup lifecycle processes.
