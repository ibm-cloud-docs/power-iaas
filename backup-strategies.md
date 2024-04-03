---

copyright:
  years: 2019, 2024

lastupdated: "2024-04-03"

keywords: backup strategies, cos, brms, icc, veeam for aix, ibm spectrum support, cloud setup, direct link, reverse proxy

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Backup strategies for IBM {{site.data.keyword.powerSys_notm}}s
{: #backup-strategies}

Learn more about different AIX and IBM i backup strategies for IBM&reg; Power Systems&trade; Virtual Server.
{: shortdesc}

## Image capture
{: #backup-image-capture}

Image capture produces a storage FlashCopy of the logical partition (LPAR) and works on both AIX, Linux, and IBM i LPARs. You can use image capture to store VM images within your account (locally) as a part of your image catalog, or directly to [IBM Cloud Object Storage](https://cloud.ibm.com/docs/power-iaas?topic=power-iaas-capturing-exporting-vm), or both.

Importing and exporting images requires a considerable amount of processing power and network bandwidth. As a result, you can submit only one import or export request before it is queued. Typically, users import or export system disks (AIX rootvg disks) that are smaller in size (**less than 1 TB**) to facilitate the transfer to and from Cloud Object Storage. If your image size is greater than 1 TB, your transfer might take a long time and is prone to failure. The maximum image size that you can import or export is **10 TB**.

## Secure automated backup with Compass for AIX and Linux®
{: #baas}

IBM Cloud® Partner Cobalt Iron® provides an automated backup offering for AIX and Linux instances of {{site.data.keyword.powerSysFull}}. The backup offering is called Secure Automated Backup with Compass® referred hereafter as “Backup Offering.”  

The Backup Offering is powered by Cobalt Iron Compass and is accessible from the IBM Cloud [catalog](https://cloud.ibm.com/catalog){: external}. The Backup Offering provides enterprise-class backup and restore features in a cloud-centric SaaS solution. Compass capabilities and security features, along with many other security functions provides protection and self-assessments to protect enterprise data and applications. 

Cobalt Iron Compass provides the ability to protect a variety of platforms, applications, and data classes. The Backup Offering includes the following unique features and functions: 

1. AIX operating systems 

   1. File-level backup and restore 

   2. Image-level backup and restore 

   3. Policy management down to the directory and file object or type levels 

   4. Backup and archive features that includes long-term retention of data 

2. Linux on Power operating systems 

   1. File-level backup and restore 

   2. Image-level backup and restore 

   3. Policy management down to the directory and file object or type levels 

   4. Backup and archive features that includes long-term retention of data 

3.  DB2 on AIX databases 

    1.  DB2-integrated backup and restore of DB2 databases 

    2.  DB2-integrated archive logging of DB2 databases 

4.  Oracle on AIX databases 

    1.  RMAN-integrated backup and restore of Oracle databases 

    2.  RMAN-integrated archive logging of Oracle databases 

    3.  Support for Oracle Automated Storage Management (Oracle ASM) features 

5.  SAP HANA on Linux on Power databases 

    1.  HDBackInt-integrated backup and restore of SAP HANA databases 

    2.  HDBackInt-integrated backup and restore of SAP HANA redo log files 

    3.  Support for the SAP HANA Cockpit for configuration, monitoring, and scheduling of backups 


The Backup Offering provides a variety of integrated security and operational features including: 

1. Alerting, notifications, and ticketing features and integration
2. Automated auditing and validation of backup server landscape 
3. Backup server automation that includes hands-free automation of all backup server tasks 
4. Centralized policy management 
5. Complete governance 
6. Data reduction through compression and deduplication 
7. Data replication across regions in IBM Cloud 
8. Encryption of data in all phases from in-transit, to-storage, and at-rest 
9.  Extensive support for encryption, data immutability, and other security access controls 
10. Multitenancy and unlimited sub-organizations
11. Role-based access control management.

The Backup Offering is not currently applicable to IBM i environment in Power Virtual Server.
{: note}

You can use the Backup Offering to backup your AIX and Linux virtual server instances in IBM Cloud Power Virtual Server.  

To deploy the Backup Offering, complete the following steps: 

* From IBM Cloud catalog, provision the Backup Offering for your account for a region. 

* Attach Power Virtual Server workspace you want to enable for backup zones to the IBM Cloud Transit Gateway.  

* Access the Cobalt Iron Commander graphical interface to download the software and install the agent inside the virtual machines. 

* Define the fine granular backup policies for your virtual server instances, files, and file systems. 

### Architecture diagram
{: #baas-architechture}

Following diagram provides insights about how the Backup Offering is deployed and requirements for AIX and Linux VMs on Power to access the Compass backup servers through IBM Cloud network. 

Compass backup servers are preconfigured in data centers and are also replicated across to the other regions. When a customer provisions the Backup Offering through IBM Cloud catalog, an automation process deploys the Backup Offering, Virtual Private Cloud (VPC) and necessary Virtual Private Endpoints (VPE) to establish secure private network connection to the Compass backup servers.  

It is highly recommended that you refrain from deploying any additional resources to Backup Offering VPC.
{: important}

![Backup Offering network architecture diagram](./images/Cobalt_Iron_Architecture.svg "Backup Offering network architecture diagram"){: caption="Figure 1. Backup Offering network architecture diagram" caption-side="bottom"}

* The Backup Offering VPC is the managed backup server instance that is deployed when the Backup Offering is provisioned. 

* Upon deployment of the backup server instance, an automation process creates the following: 

  * A local Transit Gateway if it does not already exist 

  * A VPC for exclusive use of the backup activity 

  * A VPE for each of the backup servers 

* Security group with inbound rule, address prefix, and subnet. 

* The Backup Offering VPC and the Power Virtual Server workspaces should be in the same region and connected using the local Transit Gateway. 

### Deploying the backup instance
{: #baas-deploy}

To create and deploy a backup server instance from the IBM Cloud catalog, complete the following steps: 

1. Log in to the IBM Cloud [catalog](https://cloud.ibm.com/catalog){: external} with your credentials.
2. In the search box, type _Compass Backup_ and click **Secure Automated Backup with Compass** tile.
3. Select a deployment location for your backup instance.
4. Define the fields – **Pricing plan**, **Service name**, **Resource group**, and your **IBM Cloud API key** as per your business needs.
5. Click **Create**.
6. Connect VPC of this deployment and the {{site.data.keyword.powerSys_notm}} workspace that you want to back up by using the local Transit Gateway. You can use you existing Transit Gateway or create a new one. 

  For more information, see [Ordering IBM Cloud Transit Gateway](/docs/transit-gateway?topic=transit-gateway-ordering-transit-gateway&interface=ui) and [Using virtual private endpoints for VPC to privately connect to IBM Cloud Transit Gateway](/docs/transit-gateway?topic=transit-gateway-vpe-connection&interface=cli).

6. Click **Launch Compass UI** which will redirect you to Cobalt Iron Compass page where you will need to complete the setup. For more information, see [Cobalt Iron documentation](https://help.cobaltiron.com/wp-login.php){: external} (login required).

### Pricing
{: #baas-pricing} 

When you use the Backup Offering, you are billed monthly through IBM Cloud for amount of data backed up for the region and is metered hourly (GB/hour basis).  

Connectivity between {{site.data.keyword.powerSys_notm}} instances and the backup servers is established via a transit gateway connection to the backup VPC. Name resolution is for the backup server connections which is also required. You can accomplish this using the agent system's /etc/hosts file, or by adding CNAME entries to your agent system's DNS server. These elements need to be deployed in your account (transit gateway and VPC provisioning and setup happens through automation when the Backup Offering is provisioned). 

### Supported data center pairs
{:#baas-dcs} 

The Backup Offering is available in the following data center pairs: 

| Data Center 1 | Data Center 2 |
|---------------|---------------|
| DAL10         | WDC07         |
| DAL12         | WDC06         |
| MAD02         | FRA04         |
| MAD04         | FRA05         |
| SAO01         | SAO04         |
| OSA21         | TOK04         |
{: caption="Table 1. Data center pair availibility for backup offering" caption-side="bottom"}

### Additional support
{: #baas-support}

Support for the Backup Offering is provided by Cobalt Iron and you will need to have login credentials to Cobalt Iron to access the following:
* For more information about the offering, see the [Cobalt Iron documentation](https://help.cobaltiron.com/wp-login.php){: extrnal}.
* For issues related to backup and restore, reach out to Cobalt Iron by opening a service ticket via `support.cobaltiron.com`.

If you encounter an issue related to Power Virtual Server or IBM Cloud, see [Getting help and support](/docs/power-iaas?topic=power-iaas-getting-help-and-support). 

## IBM i backup strategies
{: #backup-ibmi}

A common IBM i backup strategy is to use IBM® Backup, Recovery, and Media Services (BRMS) and IBM Cloud Storage Solutions (ICC). Together, these products automatically back up your LPARs to {{site.data.keyword.cos_full_notm}}. The ICC product can be integrated with BRMS to move and retrieve objects from remote locations, including Cloud Object Storage. In most cases, this process involves backing up to virtual tapes and image catalogs. Note, you might need extra storage for the LPAR to host the image catalogs until they are moved to Cloud Object Storage.

The typical IBM i customer uses the following flow to back up LPARs and objects:

1. Use the 5733-ICC product to connect to Cloud Object Storage (COS) (~2 times the disk capacity to hold the backup images).
2. Connect to IBM COS by following the steps mentioned in [Using Cloud Object Storage](/docs/power-iaas?topic=power-iaas-backup-strategies#cos-over-directlink).
4. Complete the back up to COS by choosing the speed and resiliency that is required.

   - [Working with ICC](https://www.ibm.com/support/knowledgecenter/ssw_ibm_i_72/icc/topics/iccucon_commands_cloud_overview.htm){: external}
   - [BRMS with Cloud Storage Solutions for i considerations and requirements](https://www.ibm.com/support/knowledgecenter/en/ssw_ibm_i_74/rzai8/rzai8brmscloudrequireandconsider.htm){: external}
   - [Data backup and recovery by using BRMS and IBM Cloud Storage Solutions for i](https://www.ibm.com/support/knowledgecenter/en/ssw_ibm_i_74/rzai8/rzai8backupandrecoveryusingBRMSandICC.htm){: external}

For a complete tutorial on backing up and restoring IBM i VM data, see [Backing up and restoring data in an IBM i VM](https://cloud.ibm.com/media/docs/downloads/power-iaas-tutorials/PowerVS_IBMi_Backups_Tutorial_v1.pdf){: external}.

## Using Cloud Object Storage
{: #cos-over-directlink}

The preferred way to connect to Cloud Object Storage (COS) from a VM in {{site.data.keyword.powerSys_notm}} are as follows:

1.  In a PER workspace, attach the {{site.data.keyword.powerSys_notm}} workspace to a Transit Gateway and directly access the COS direct endpoint. See, [Attaching Transit Gateway to a PER workspace](/docs/power-iaas?topic=power-iaas-per#attaching-transit-gateway-to-a-per-workspace).
2.  In a non-PER workspace that are in a multi-zone region (MZR) the best way to connect to COS is as follows:
    1. Create a [Virtual Private Cloud (VPC) with subnet(s)](/docs/vpc?topic=vpc-subnets-configure&interface=ui#subnets-create-ui) in the same region as your {{site.data.keyword.powerSys_notm}} workspace.
    2. Create a [Virtual Private Endpoint gateway](/docs/vpc?topic=vpc-ordering-endpoint-gateway&interface=ui) (VPE).
    3. Connect the VPC to a [Transit Gateway](/docs/transit-gateway?topic=transit-gateway-ordering-transit-gateway&interface=ui#tg-ui-creating-transit-gateway).
    4. [Create a cloud connection](/docs/power-iaas?topic=power-iaas-cloud-connections#create-cloud-connections) to connect the non-PER {{site.data.keyword.powerSys_notm}} workspace to the same transit gateway. 
    
    The {{site.data.keyword.powerSys_notm}} would then use the VPE's IP address to connect to COS. A Custom Resolver (CR) is needed by the {{site.data.keyword.powerSys_notm}} to reach the COS. If the VPE has multiple IP addresses, you can set up custom DNS and a custom hostname to connect to COS. 
3.  Deploy a Nginx reverse proxy server in either the classic or VPC infrastructure.

    Nginx is a mature, compact, and fast open source web server that excels at specialized tasks, including the reverse proxy server role. For information on setting up a Nginx reverse proxy server, see [Installing your Nginx reverse proxy](/docs/direct-link?topic=direct-link-using-ibm-cloud-direct-link-to-connect-to-ibm-cloud-object-storage#direct-link-installing-your-nginx-reverse-proxy).

### Cloud Object Storage on AIX
{: cos-aix}

IBM Power Systems that are running AIX 7.2 TL3, or later, have a script that is located in the path, `/usr/samples/nim/cloud_setup`. The `cloud_setup` command installs the command-line environment for cloud storage services.

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
{: add-backup}

The additional backup strategies that you can use are as follows:
- FalconStor StorSafe VTL - For more information see [FalconStor StorSafe VTL](/docs/power-iaas?topic=power-iaas-migration-strategies-power#falconstor-storsafe-vtl).
- Veeam for AIX - It provides simple physical server backup solutions for machines that are running in respective UNIX® operating systems. With them, IT organizations can provide industry-leading file-based backup and disaster recovery for their environments. For more information, see [Veeam Agents for IBM AIX](https://www.veeam.com/ibm-aix-oracle-solaris-backup.html){: external}.

### Ordering Veeam standalone licenses
{: #backup_veeam_ordering_licenses}

You can order a Veeam® standalone license, via IBM Cloud portal [Order Veeam Licesne](https://cloud.ibm.com/infrastructure/vmware-solutions/console/instances/licenses)

An email will be sent confirming the order. Should the order be incorrect, it can be deleted. For more information, see [Managing Veeam licenses](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_managing_licenses).

A license key will be generated and emailed to whomever placed the order.
  
## Managed services and IBM resiliency services
{: #managed-services}

Contact an IBM representative if you need help with understanding the different backup lifecycle processes.
