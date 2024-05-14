---

copyright:
  years: 2019, 2024

lastupdated: "2024-05-14"

keywords: backup strategies, cos, brms, icc, veeam for aix, ibm spectrum support, cloud setup, direct link, reverse proxy

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Additional backup strategies
{: #additional-backup-strategies}

The additional backup strategies that you can use are as follows:

### Image capture
{: #backup-image-capture}

Image capture produces a storage FlashCopy of the logical partition (LPAR) and works on both AIX, Linux, and IBM i LPARs. You can use image capture to store VM images within your account (locally) as a part of your image catalog, or directly to [IBM Cloud Object Storage](https://cloud.ibm.com/docs/power-iaas?topic=power-iaas-capturing-exporting-vm), or both.

Importing and exporting images requires a considerable amount of processing power and network bandwidth. As a result, you can submit only one import or export request before it is queued. Typically, users import or export system disks (AIX rootvg disks) that are smaller in size (**less than 1 TB**) to facilitate the transfer to and from Cloud Object Storage. If your image size is greater than 1 TB, your transfer might take a long time and is prone to failure. The maximum image size that you can import or export is **10 TB**.

### Cloud Object Storage
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

#### Cloud Object Storage on AIX
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

### Veeam for AIX

Veeam for AIX provides simple physical server backup solutions for machines that are running in respective UNIX® operating systems. With them, IT organizations can provide industry-leading file-based backup and disaster recovery for their environments. For more information, see [Veeam Agents for IBM AIX](https://www.veeam.com/ibm-aix-oracle-solaris-backup.html){: external}.

#### Ordering Veeam standalone licenses
{: #backup_veeam_ordering_licenses}

You can order a Veeam® standalone license, via IBM Cloud portal [Order Veeam Licesne](https://cloud.ibm.com/infrastructure/vmware-solutions/console/instances/licenses)

An email will be sent confirming the order. Should the order be incorrect, it can be deleted. For more information, see [Managing Veeam licenses](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_managing_licenses).

A license key will be generated and emailed to whomever placed the order.

### FalconStor StorSafe VTL

For more information see [FalconStor StorSafe VTL](/docs/power-iaas?topic=power-iaas-migration-strategies-power#falconstor-storsafe-vtl).
  
### Managed services and IBM resiliency services
{: #managed-services}

Contact an IBM representative if you need help with understanding the different backup lifecycle processes.
