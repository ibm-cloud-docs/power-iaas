---

copyright:
  years: 2019, 2025

lastupdated: "2025-07-25"

keywords: release notes, announcements, feature updates, changes, power virtual server, IBM data center, Client location

---

{{site.data.keyword.attribute-definition-list}}

# Release notes for {{site.data.keyword.powerSys_notm}}
{: #release-notes}


Use these release notes to learn about the latest changes to {{site.data.keyword.powerSysFull}}.
{: shortdesc}

## July 2025
{: #July-2025}



- Starting on 25 July 2025, you can deploy Power Virtual Server instances running the AIX, IBM i, RHEL, and SLES operating systems on IBM Power11 (subject to capacity availability). Refer to the [supported operating system levels](/docs/power-iaas?topic=power-iaas-powervs-faqs#os-versions) for Power11.



- With IBM Power10 systems and later, you can assign an {{site.data.keyword.ibmi-vst}} to a virtual server instance (VSI). The {{site.data.keyword.ibmi-vst}} limits the size of the VSI, but not the physical system on which it runs. It controls the pricing tier for the IBM i operating system and licensed program products (LPPs). The {{site.data.keyword.ibmi-vst}} also defines the boundaries for the virtual processors and memory size. For more information, see [Assigning an IBM i software tier to an IBM i Power Virtual Server instance](/docs/power-iaas?topic=power-iaas-ibmi-vsw-tiers).



- You can set the scope of an SSH key to improve the security and privacy of the SSH key. When the scope is set, the visibility of the SSH key is restricted to a workspace or an account. For more information, see [Setting the scope of an SSH key in a Power Virtual Server workspace](/docs/power-iaas?topic=power-iaas-creating-ssh-key).







[{{site.data.keyword.off-prem}}]{: tag-blue}



- You can use the routes feature in your PER-enabled Power Virtual Server workspaces to view implicit network routes and to create or manage static routes. For more information, see [Creating and managing network routes in IBM Power Virtual Server workspaces](/docs/power-iaas?topic=power-iaas-routes).

- The network security group feature is enhanced to provide the following additional capabilities:

    - You can clone an existing network security group to create a network security group. For more information, see [Cloning an NSG](/docs/power-iaas?topic=power-iaas-nsg#clone-nsg).

    - You can transfer members from one network security group to another. For more information, see [Moving members from one NSG to another NSG](/docs/power-iaas?topic=power-iaas-nsg#move-members).



- You can enable the Address Resolution Protocol (ARP) to map IP addresses to physical Media Access Control (MAC) addresses in the {{site.data.keyword.powerSys_notm}} network. For more information, see [Configuring the Subnet ARP Broadcast in Power Virtual Server subnets](/docs/power-iaas?topic=power-iaas-subnet-arp-oracle-rac).



- You can integrate your Power Virtual Server workspace with IBM Cloud&reg; Monitoring service to gain operational visibility about the performance and health of your applications, services, and platforms. For more information, see [Monitoring metrics for IBM Power Virtual Server](/docs/power-iaas?topic=power-iaas-monitor-sysdig#monitor-pvsw).






- New server placement groups and shared processor pools are created with Cloud Resource Names (CRNs), to provide benefits such as tagging and visibility in the IBM Cloud Resource list. The existing server placement groups and shared processor pools will be assigned a CRN by the end of August 2025.








On 14 July 2025, the {{site.data.keyword.powerSys_notm}} VPNaaS product reached its end of life and is no longer available for use. However, you can use the IBM Cloud VPC VPN to avoid VPN service interruptions. For assistance to upgrade or migrate to IBM Cloud VPC VPN, open a [support ticket](https://www.ibm.com/cloud/support){: external} or engage with your Customer Support Manager (CSM).
{: important}

- IBM {{site.data.keyword.powerSys_notm}} integrates with IBM watsonx SaaS services to deliver a powerful and flexible infrastructure. The integrated infrastructure supports demanding workloads, runs advanced AI applications, and scales rapidly in a hybrid cloud environment with automated AI infrastructure setup and management. For more information, see [IBM Power Virtual Server and watsonx integration](/docs/powervs-watsonx-toolkit).

**End of Life Reminder**: Effective 1 July 2025, Cloud Connections is no longer available at no-charge (see [March 2025](/docs/power-iaas?topic=power-iaas-release-notes#March-2025) for details), and you will incur monthly charges for any Direct Link connections that you continue to use. The pricing is based on the port speed of your connections. To avoid these charges, migrate your workspace to PER-enabled workspaces. The `CHE01` and `MON01` data centers continue to use Cloud Connections without any charges. For more information, see [Migrating to PER](/docs/power-iaas?topic=power-iaas-per#migrate-per).
{: important}





## June 2025
{: #June-2025}

[{{site.data.keyword.off-prem}}]{: tag-blue}


- You can deploy SAP certified profiles on IBM Power10 or later servers using a single custom OS boot image. For more information, see [SAP certified profiles](/docs/power-iaas?topic=power-iaas-SAP-certified-profiles).
- The single byte IBM i 7.6 stock image for IBM Power10 systems is available in the OS image catalog. This stock image is not supported on IBM Power9 systems. The double byte IBM i 7.6 stock image will be available at a later date.



- The migration of existing workspaces to Cloud Resource Names (CRNs) in all the data centers except DAL14 is completed. For more information about CRNs, see [IBM Cloud Resource Names](/docs/power-iaas?topic=power-iaas-pricing-virtual-server-on-cloud#granular-crns).

- The following RHEL OS stock images are removed from the Power Virtual Server image library as the OS levels are no longer supported by Red Hat:

  - RHEL8.8 general purpose
  - RHEL9.2 general purpose
  - RHEL8.4 for SAP (HANA)
  - RHEL8.4 for SAP NetWeaver






## May 2025
{: #May-2025}



- If you have existing IBM Cloud Connections that are managed from non-PER enabled workspaces, you can now view and delete them using the [IBM Cloud CLI](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-cloud-connection-delete){: external} or [API](/apidocs/power-cloud#pcloud-cloudconnections-delete){: external} from a PER-enabled workspace.




[{{site.data.keyword.off-prem}}]{: tag-blue}

- The following RHEL OS stock images are refreshed and available for Power Virtual Servers in the IBM data centers:
  - RHEL 9.4 for SAP
  - RHEL 9.2 for SAP
  - RHEL 8.10 for SAP
  - RHEL 8.8 for SAP
  - RHEL 8.10 general purpose
  - RHEL 9.4 general purpose

- You can deploy SAP NetWeaver sr2 profiles on IBM Power servers. For more information, see [SAP NetWeaver profiles](/docs/power-iaas?topic=power-iaas-SAP-hana-certified-profiles#sap-appser-profiles).

## April 2025
{: #April-2025}


[{{site.data.keyword.off-prem}}]{: tag-blue}



The Red Hat Enterprise Linux (RHEL) End of Support date for RHEL 9.2 general purpose, RHEL 8.8 general purpose, and RHEL 8.4 for SAP is 30 May 2025. Stock images for these OS levels are scheduled to be removed from the Power Virtual Server image library starting 31 May 2025. The existing virtual machines (VMs) that are using these stock images can continue to operate without interruption. However, to ensure ongoing support and maintenance, update your VMs to a supported OS level. For more information about the RHEL End of Support guidelines, see [Red Hat Enterprise Linux Life Cycle](https://access.redhat.com/support/policy/updates/errata){: external} and for available OS stock images, see [FAQs](/docs/power-iaas?topic=power-iaas-powervs-faqs).
{: important}

- IBM i 7.3, 7.2 and COR stock images have been refreshed.

- In [February 2025](#Feb-2025), IBM {{site.data.keyword.powerSys_notm}} started the support of cloud resource names (CRNs) for new workspaces. Starting from April to June 2025, the existing workspaces are being migrated to CRNs. CRN identifiers are assigned to uniquely identify resources in the IBM Cloud, such as virtual machines (VMs), shared processor pools (SPPs), volumes, snapshots, and dedicated hosts.

  The billing and metering plans are updated with the following changes:

    - For billing, an instance of a resource is identified by using the associated CRN and not by the `Consumer ID` value.
    - Each resource type has its own billing plan instead of billing all the resources under the `Workspace for Power Virtual Server` plan.
    - The value for the `Pricing Region` field is based on metro regions and is not based on data center and zone regions. However, the value for the `Location` field of the instance is based on the data center and zone regions.
    - The costs of the snapshots are now billed by using independent metrics for snapshots and are not included with the volume metrics.

  The existing price of the resources does not change. The organization and visualization of the costs of the resources are updated to match the billing and metering plans for {{site.data.keyword.on-prem-fname}} in {{site.data.keyword.on-prem}} that supports CRNs.





- The idle timeout for the Virtual Server Instance (VSI) console (previously called VNC console) is extended to up to 2 hours from 30 minutes. For more information, see [Working with the VSI console](/docs/power-iaas?topic=power-iaas-vsi-console).



- Global replication service supports new data center pair `WDC06`-`DAL14`. For more information, see [Locations that support global replication service](/docs/power-iaas?topic=power-iaas-getting-started-GRS#locations-GRS).



- You can enable Cloud Security Posture Management (CSPM) feature in your existing and new {{site.data.keyword.powerSys_notm}} workspaces. For more information about CSPM, see [Integrating Power Virtual Server with IBM Cloud Security and Compliance Center Workload Protection](/docs/power-iaas?topic=power-iaas-integrate-scc).





## March 2025
{: #March-2025}

- New AIX 7.3 TL3 SP0 and 7.2 TL5 SP9, IBM i 7.4 TR11 and 7.5 TR5, SLES 15 SP6 for SAP HANA (SLES15-SP6-SAP) and SLES 15 SP6 for SAP NetWeaver (SLES15-SP6-SAP-NETWEAVER) operating system images are available. For more information, see the [FAQ documentation](/docs/power-iaas?topic=power-iaas-powervs-faqs#os-versions).


[{{site.data.keyword.off-prem}}]{: tag-blue}





The End of Life date for the no-charge Cloud Connections, which IBM Power Virtual Server provides to clients to access IBM Cloud resources in their network, is now extended indefinitely beyond the original date of 18 June 2025. However, starting with 1 July 2025 metering charges are applied to any remaining Direct Link connections. After this date, you will incur monthly charges for any Direct Link connections, with pricing based on the port speed of your connections. To avoid these charges, migrate your workspace before 1 July 2025. For more information about the migration, see [Migrating to Power Edge Router](/docs/power-iaas?topic=power-iaas-per#migrate-per).
{: important}




- You can deploy SAP HANA CH2 and BH2 profiles on specific IBM Power servers. For more information, see [SAP HANA certified profiles](/docs/power-iaas?topic=power-iaas-SAP-hana-certified-profiles).



- Shared Processor Pool (SPP) metering is optimized to improve the Total Cost of Ownership (TCO) for AIX and IBM i software licensing and DR scenarios. Virtual servers that are configured within an SPP will not incur additional cost for per VM core or the cost for high-use memory parts. For more information, see [Pricing for shared processor pool for {{site.data.keyword.off-prem-fname}} in {{site.data.keyword.off-prem}}](/docs/power-iaas?topic=power-iaas-pricing-virtual-server-on-cloud#price-spp) and [Pricing for shared processor pool for {{site.data.keyword.on-prem-fname}} in {{site.data.keyword.on-prem}}](/docs/power-iaas?topic=power-iaas-pricing-private-cloud#pricing-spp-private-cloud)



[{{site.data.keyword.on-prem}}]{: tag-red}

- The pricing for IBM Power Subscription plan to provision VMs with SAP BYOL or Linux BYOL images is now based on a flat subscription rate instead of metered usage charges. For more information, see [Using SLES within IBM Power Virtual Server](/docs/power-iaas?topic=power-iaas-using-linux) or [Using RHEL within the Power Virtual Server](/docs/power-iaas?topic=power-iaas-linux-with-powervs).


## February 2025
{: #Feb-2025}





The End of Support date for Cloud Connections has been extended from 18 April, 2025 to 18 June, 2025 to align with its end of life date. For more information about the End of Service and End of Life Notice, see [December 2024](#Dec-2024).
{: important}





{{_include-segments/workspace-note.md}}



- {{site.data.keyword.powerSys_notm}} is now HITRUST CSF&reg; compliant. For more information, see [Compliance certifications](/docs/power-iaas?topic=power-iaas-compliances-list#hitrust).

[{{site.data.keyword.off-prem}}]{: tag-blue}

- {{site.data.keyword.powerSys_notm}} is enhanced to provide complete billing transparency. With the enablement of IBM Cloud Resource Names (CRNs), you can view the contribution of each resource to your monthly cloud expenditure. For more information, see [IBM Cloud Resource Names](/docs/power-iaas?topic=power-iaas-pricing-virtual-server-on-cloud#granular-crns). This enhancement does not introduce any changes in {{site.data.keyword.powerSys_notm}} pricing. The IBM CRNs are displayed when you create new workspaces. Note that the existing workspaces are planned to be enhanced with CRNs by `June 2025` without disrupting your work.



- You can now use Network security groups (NSG) in your PER-enabled {{site.data.keyword.powerSys_notm}} workspaces to control internal and external inbound traffic to your virtual network. You can define security rules for NSGs based on source IP addresses, ports, and protocols (TCP, UDP, ICMP, and Any). This new capability is available when creating new PER-enabled workspaces. Existing workspaces are planned to be migrated to support NSGs by `June 2025`. For more information, see [Network security groups](/docs/power-iaas?topic=power-iaas-nsg).



## January 2025
{: #Jan-2025}



**End of Service reminder** - Effective `January 18, 2025`, IBM will no longer deliver standard support for the {{site.data.keyword.powerSys_notm}} VPNaaS product. On `July 14, 2025`, the {{site.data.keyword.powerSys_notm}} VPNaaS product will reach its end of life. If you are using {{site.data.keyword.powerSys_notm}} VPNaaS product, you are encouraged to move to the [IBM Cloud VPC VPN](/docs/power-iaas?topic=power-iaas-VPN-connections#vpc-vpn) to avoid VPN service interruptions.
{: important}


- Starting `January 22, 2025`, [Virtual Serial Number (VSN)](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#vsn) and [Virtual host identifier](/docs/power-iaas?topic=power-iaas-dedicated-host#virtual-host-ID) are supported in all the data centers.


- Global replication service supports new data center pair `LON04`-`LON06`. For more information, see [Locations that support global replication service](/docs/power-iaas?topic=power-iaas-getting-started-GRS#locations-GRS).








## December 2024
{: #Dec-2024}


[{{site.data.keyword.off-prem}}]{: tag-blue}

- You can now assign a Virtual Serial Number (VSN) to an IBM i VM. With a VSN associated with your VM, you need not pin the VM to a host for licensing or entitlement purposes. For more information, see [Virtual Serial Number (VSN)](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#vsn).
- You can now use automation to migrate an existing network to Power Edge Router (PER) through CLI. For more information, see [Migrating to PER](/docs/power-iaas?topic=power-iaas-per#migrate-per).
- As the {{site.data.keyword.powerSys_notm}} offering transitions to the PER integrated network solution, the ability to create new {{site.data.keyword.powerSys_notm}} Cloud Connections across most data centers is disabled. You are encouraged to migrate to PER now if you have not done so already. For more information about PER, see [Getting Started with Power Edge Router](/docs/power-iaas?topic=power-iaas-per). You can create Cloud Connections only in the `CHE01` and `MON01` data centers. For more information, see [IBM Power Virtual Server Cloud Connections](/docs/power-iaas?topic=power-iaas-cloud-connections).

Support for Cloud Connections ends on `April 18, 2025` and the Cloud Connections solution will reach the end of life on `June 18, 2025`. For more information about End of Service Notice, see [July 2024](/docs/power-iaas?topic=power-iaas-release-notes#jul-2024).
{: note}

- All IBM {{site.data.keyword.powerSys_notm}} data centers are now PER-enabled, except for the `CHE01` and `MON01` data centers. For more information, see [Getting Started with Power Edge Router](/docs/power-iaas?topic=power-iaas-per).
- A new data center `DAL14` is available. Following are some of the capabilities of the `DAL14` data center:

    - New {{site.data.keyword.powerSys_notm}} node, [IBM Power System E1050 (9043-MRX)](https://www.ibm.com/downloads/cas/MKQOQAYV) which is a 4-socket server.
    - {{site.data.keyword.powerSys_notm}} capabilities such as Power Edge Router network connectivity, IBM Cloud Monitoring, and Flexible IOPS.

 For more information about your data center capabilities, see {{site.data.keyword.powerSys_notm}} [overview](https://cloud.ibm.com/power/overview) page in the IBM Cloud console.

- New RHEL 8.10 general purpose (RHEL8-SP10), RHEL 8.10 for SAP HANA (RHEL8-SP10-SAP-HANA), RHEL 8.10 for SAP NetWeaver (RHEL8-SP10-SAP-NETWEAVER), RHEL 9.4 for SAP HANA (RHEL9-SP4-SAP-HANA), RHEL 9.4 for SAP NetWeaver (RHEL9-SP4-SAP-NETWEAVER), SLES 15 SP6 general purpose (SLES15), and AIX 7.3 TL2 SP2 operating system images are available. For more information, see the [FAQs](/docs/power-iaas?topic=power-iaas-powervs-faqs#os-versions).

- Starting `February 24, 2025`, the {{site.data.keyword.powerSys_notm}} dedicated host identifier will use the virtual host ID format. The virtual host ID has the standard format that is used to uniquely identify other {{site.data.keyword.powerSys_notm}} resources. If you are using dedicated hosts and depend on specific resource identifiers such as API and CLI calls, you must update the logic to use the virtual host ID format; otherwise, the logic might fail. For more information, see [Understanding a Virtual host identifier](/docs/power-iaas?topic=power-iaas-dedicated-host#virtual-host-ID).


[{{site.data.keyword.on-prem}}]{: tag-red}

- You can now enable Global Replication Services (GRS) for asynchronous replication of data between the primary location infrastructure and the secondary location infrastructure. For more information, see [Global Replication Services in {{site.data.keyword.on-prem}}](/docs/power-iaas?topic=power-iaas-getting-started-GRS#grs-on-prem).
- You can now access external connectivity to and from the virtual machines in a subnet. For more information, see [Use case 2: Multiple external connectivities](/docs/power-iaas?topic=power-iaas-network_use_cases#static-l3).
- You can now discover infrastructure capabilities and important information that helps you to develop solutions by using Power Virtual Server on the {{site.data.keyword.powerSys_notm}}    [overview](https://cloud.ibm.com/power/overview){: external} page in the IBM Cloud console. For more information, see [Data center capabilities](/docs/power-iaas?topic=power-iaas-private-cloud-architecture#dc-capabilities).
- The new AIX 7.3 TL2 SP2 operating system image is available. For more information, see the [FAQs](/docs/power-iaas?topic=power-iaas-powervs-faqs#os-versions).


## October 2024
{: #Oct-2024}








- [{{site.data.keyword.off-prem}}]{: tag-blue}You can now configure a virtual machine that contains a boot volume and deploy an IBM i virtual machine to support the attachment of large quantity of data volumes. You can configure a virtual machine available in all the data centers except for the virtual machines in the `CHE01` data center. For more information, see [Configuring large quantity of data volumes on {{site.data.keyword.off-prem}}](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#config-large-vol).

- [{{site.data.keyword.off-prem}}]{: tag-blue}IBM Cloud Monitoring service is now available in the `CHE01` data center. For more information, see [Monitoring metrics for {{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-monitor-sysdig).



- [{{site.data.keyword.off-prem}}]{: tag-blue} The refreshed RHEL 9.2 for SAP, RHEL 8.8 for general purpose and SAP, and RHEL 8.6 for general purpose and SAP OS images are available in the image catalog that supports SAP t-shirt profiles with more than 64 cores. For more information, see the [SAP documentation on OS](/docs/sap?topic=sap-compute-os-design-considerations#os-power) for IBM {{site.data.keyword.powerSys_notm}}.



The latest IBM i and AIX stock images were added to the OS image catalog in September. Hence, the previous versions of the service pack will be removed from the catalog in the next thirty days. For more information about the OS versions, see the [FAQs](/docs/power-iaas?topic=power-iaas-powervs-faqs#os-versions). For new deployments, you must use the latest stock image in the catalog. Existing VMs that use the previous stock images continue to operate without problems. However, it is recommended that you update your VM to the latest service pack level for the most recent maintenance.
{: note}

## September 2024
{: #Sep-2024}

- You can now discover data center capabilities and important information that helps you to develop solutions by using Power Virtual Server on the {{site.data.keyword.powerSys_notm}} [overview](https://cloud.ibm.com/power/overview){: external} page in the IBM Cloud console. For more information, see [Data center capabilities](/docs/power-iaas?topic=power-iaas-ibm-cloud-reg#dc-capabilities).
- [{{site.data.keyword.off-prem}}]{: tag-blue}You can now enable the replication services for a volume from the user interface. For more information, see [Global Replication Services (GRS)](/docs/power-iaas?topic=power-iaas-getting-started-GRS).
- [{{site.data.keyword.off-prem}}]{: tag-blue}You can now configure a virtual machine that contains a boot volume and deploy an IBM i virtual machine to support the attachment of large quantity of data volumes available in `DAL10` and `WDC07` data centers. For more information, see [Configuring large quantity of data volumes on {{site.data.keyword.off-prem}}](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#config-large-vol).
- [{{site.data.keyword.on-prem}}]{: tag-red}You can now select the `DAL10` and `WDC07` location pair to resize a replication-enabled primary volume from the primary site. The system then resizes the associated auxiliary volume on its corresponding remote site within 24 hours. For more information, see [Updating a primary volume](/docs/power-iaas?topic=power-iaas-getting-started-GRS#update-prime-vol).
- [{{site.data.keyword.on-prem}}]{: tag-red}You can now select the SUSE Linux Enterprise Server (SLES) stock image when you register for full Linux subscription, for {{site.data.keyword.powerSys_notm}}. For more information, see [Full Linux® subscription for IBM Power Virtual Server in {{site.data.keyword.on-prem}}](/docs/power-iaas?topic=power-iaas-full-linux-sub).
- [{{site.data.keyword.on-prem}}]{: tag-red}You can now validate the import file against the SHA-256 checksum file from the user interface. For more information, see [Using the Power Virtual Server user interface to import a boot image](/docs/power-iaas?topic=power-iaas-importing-boot-image#console-import-image) and [Using the Power Virtual Server user interface to capture and export a VM](/docs/power-iaas?topic=power-iaas-capturing-exporting-vm#console-capture-export).
- You can now download, Secure Automated Backup with Compass by Cobalt Iron, from [IBM Cloud Catalog](https://cloud.ibm.com/catalog){: external} for immediate deployment. The solution provides the environment for Cloud backup and recovery for IBM {{site.data.keyword.powerSys_notm}} workloads. The offering is the only automated BaaS and recovery solution for IBM {{site.data.keyword.powerSys_notm}} workloads that are powered by IBM Storage Protect, such as SAP HANA, Oracle, Db2 on AIX and Linux. For more information, see [Cobalt Iron Expands Access to Secure Automated Backup With Compass for IBM Power Virtual Server](https://info.cobaltiron.com/news/cobalt-iron-ibm-vs-baas-global-expansion){: external}.

- [{{site.data.keyword.off-prem}}]{: tag-blue} new AIX 7.2 TL5 SP8 and RHEL 9.4 general purpose (RHEL9-SP4) operating system images are available. For more information, see the [FAQs](/docs/power-iaas?topic=power-iaas-powervs-faqs#os-versions).
- [{{site.data.keyword.on-prem}}]{: tag-red} new AIX 7.3 TL2 SP1 and AIX 7.2 TL5 SP8 operating system images are available. For more information, see the [FAQs](/docs/power-iaas?topic=power-iaas-powervs-faqs#os-versions).
- New IBM i 7.5 TR4 and IBM i 7.4 TR10 operating system images are available for both {{site.data.keyword.off-prem}} and {{site.data.keyword.on-prem}}. For more information, see the [FAQs](/docs/power-iaas?topic=power-iaas-powervs-faqs#os-versions).
- New `IBM i COR` stock image is available for both {{site.data.keyword.off-prem}} and {{site.data.keyword.on-prem}}. While you are installing the image, if you encounter any issues, you can refer to the [57xxSS1 Option 1 or Option 3 in *ERROR - Tips Before Reinstallation](https://www.ibm.com/support/pages/57xxss1-option-1-or-option-3-error-tips-reinstallation){: external} procedure. For more information, see [FAQs](/docs/power-iaas?topic=power-iaas-powervs-faqs#ibm-os-versions).

**End of Service Notice** - End of service effective `October 31, 2024` will prevent the use of E880 hosts in the IBM {{site.data.keyword.powerSys_notm}} offering. E880 hosts will no longer be accessible to establish new or existing workspaces. You must ensure that all existing workspaces are moved to another host. {{site.data.keyword.powerSys_notm}} team is available to assist you. If you need assistance, [open a support ticket](/docs/power-iaas?topic=power-iaas-getting-help-and-support). If you choose not to take the recommended action and encounter issues, IBM will not be able to support you. The solution will reach its end of life on `October 31, 2024`.
{: important}



## August 2024
{: #Aug-2024}

- IBM Cloud Monitoring service is now available in `MON01`. For more information, see [Monitoring metrics for {{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-monitor-sysdig).
- You can now migrate Db2 on AIX to {{site.data.keyword.powerSys_notm}}. For more information, see [Migrating Db2 on AIX to {{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-db2-migration).

## July 2024
{: #jul-2024}

- IBM Cloud Monitoring service is now available in `TOR01`. For more information, see [Monitoring metrics for {{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-monitor-sysdig).
- Global replication service supports new data center pairs `SAO01`-`SAO04` and `MON01`-`TOR01`. For more information, see [Locations that support global replication service](/docs/power-iaas?topic=power-iaas-getting-started-GRS#locations-GRS).
- You can now deploy Linux for SAP (HANA or Netweaver) OS images within IBM {{site.data.keyword.powerSys_notm}} by using the SAP provided central image repository or by bringing your own customized image. For more information, see [SAP provided central image repository](/docs/power-iaas?topic=power-iaas-deploying-SAP-image) and [Bring your own customized Linux for SAP (HANA or NetWeaver) image](/docs/power-iaas?topic=power-iaas-deploying-SAP-image).
- You can now deploy SAP full system profiles on S1022 systems, if no virtual machines are deployed on the system. For more information, see the [SAP full system profiles](/docs/power-iaas?topic=power-iaas-SAP-full-system-profiles).
- You can now deploy SAP HANA sr2 and sh2 profiles on S1022 and E1080 systems. For more information, see [SAP HANA sr2 and sh2 profiles](/docs/power-iaas?topic=power-iaas-SAP-hana-sr2-sh2-profiles).
- You can now provision {{site.data.keyword.powerSys_notm}} workloads on Power10 E1080 (9080-HEX) hosts available in `DAL10` and `WDC07` data centers.

**End of Service Notice** - End of marketing effective `October 19, 2024` will prevent new Cloud Connections from being established in existing workspaces. In turn, IBM will stop delivering standard support for {{site.data.keyword.powerSys_notm}} Direct Link Connect in PER-enabled data centers by `April 18, 2025`. If you choose not to take the recommended action and encounter issues, IBM will not be able to support you. The solution will reach its end of life on `June 18, 2025`.
{: important}


- Due to inherent configuration complexity of the current {{site.data.keyword.powerSys_notm}} Cloud Connections which leverage Direct Link Connect service for connectivity to IBM Cloud, the direction going forward is to leverage the newly enabled Power Edge Router capability along with Transit Gateway service to connect {{site.data.keyword.powerSys_notm}} workspaces with IBM Cloud resources for a better user experience, improved reliability, and significantly higher bandwidth. You can follow a detailed [migration plan](/docs/power-iaas?topic=power-iaas-migrate-ws-per) to move your existing workspace to a PER workspace if you have set up your network manually using the Cloud Connections solution. {{site.data.keyword.powerSys_notm}} team is available to assist you. If you need assistance, open a [open a support ticket](/docs/power-iaas?topic=power-iaas-getting-help-and-support).

## June 2024
{: #jun-2024}

- {{site.data.keyword.powerSys_notm}} Private Cloud, an infrastructure as a service (IaaS) offering, is now available. It extends the capabilities and benefits of {{site.data.keyword.powerSys_notm}} within your data center, with a prescriptive set of hardware and delivered in a consumption model with no upfront payment. For more information about {{site.data.keyword.powerSys_notm}} Private Cloud and how to get started, see [Getting started with IBM Power Virtual Server](/docs/power-iaas?topic=power-iaas-getting-started).

    The content specific to IBM {{site.data.keyword.powerSys_notm}} Private Cloud is marked with [{{site.data.keyword.on-prem}}]{: tag-red} tag and the content specific to IBM {{site.data.keyword.powerSys_notm}} is marked with [{{site.data.keyword.off-prem}}]{: tag-blue} tag.
    {: note}

- The RHEL 8.6 general purpose (RHEL8-SP6) stock image is removed from the {{site.data.keyword.powerSys_notm}} data centers because the OS level is no longer supported by Red Hat.

- Global replication service supports the new data center pairs `OSA21` and `TOK04`; `SYD04` and `SYD05`. For more information, see [Locations that support global replication service](/docs/power-iaas?topic=power-iaas-getting-started-GRS#locations-GRS).

- Access the dedicated host capability from the {{site.data.keyword.powerSys_notm}} user interface. IBM Power S922 and S1022 servers can be provisioned for your dedicated use. For more information, see [Dedicated host](/docs/power-iaas?topic=power-iaas-dedicated-host).

- Snapshot usage information is now available using the API. For more information, see [Get a list of all the snapshots on a workspace](/apidocs/power-cloud#v1-snapshots-getall) and [Get the detail of a snapshot](/apidocs/power-cloud#v1-snapshots-get) for API details.

    Dedicated Hosts and Snapshots require PowerVC (PVC) 2.2.1 that is deployed worldwide except in four data centers. These four data centers are upgraded to PVC 2.2.1 with the following timeline:

    -  `MAD02` and `CHE01` on June 21, 2024
    -  `DAL12` on June 24, 2024
    -  `SAO01` on September 07, 2024

    {{site.data.keyword.on-prem-fname}} is also enabled for users to run Power workloads in a private pod Hybrid Cloud environment.

- In a {{site.data.keyword.powerSys_notm}} with Power10, you can provision a VM inside a Shared Processor Pool (SPP) with values of up to 3.0 Virtual Cores. This enables you to select the maximum number of cores for the Virtual Cores deployment, providing greater flexibility for Oracle licensing. For more information, see [Managing the shared processor pool](/docs/power-iaas?topic=power-iaas-manage-SPP).

## May 2024
{: #may-2024}

- Power Edge Router (PER) is now available in the `DAL13`, `TOR01`, and `WDC04` data centers. For more information, see [Getting Started with Power Edge Router](/docs/power-iaas?topic=power-iaas-per).
- Power Virtual Server now offers refreshed images for IBM i 7.2 TR 9.
- The SLES 15 SP4 general purpose (SLES15-SP4) stock image is in the process of being removed from the {{site.data.keyword.powerSys_notm}} data centers since the OS level is no longer supported by Red Hat.
- You can now see a **Consumer ID** in your [Billing and Usage](https://cloud.ibm.com/billing){: external} page. Using the consumer ID you can identify and get a detailed view at the resource level broken down by part metric. For more information, see [Consumer ID](/docs/power-iaas?topic=power-iaas-pricing-virtual-server-on-cloud#consumer-id).
- {{site.data.keyword.powerSys_notm}} is now Financial Services® Validated and has received a SOC 2 Type II report. For more information, see the [compliance](/docs/power-iaas?topic=power-iaas-compliances-list#fs-cloud-comp) page.
- Flexible I/O operation per second (IOPS) is now available in the `TOR01` data center. For more information, see [Flexible IOPS](/docs/power-iaas?topic=power-iaas-on-cloud-architecture#storage-tiers).

## April 2024
{: #apr-2024}

- Power Edge Router (PER) is now available in the `LON06` and `SYD04` data centers. For more information, see [Getting Started with Power Edge Router](/docs/power-iaas?topic=power-iaas-per).
- {{site.data.keyword.powerSys_notm}} now offers refreshed images for RHEL 9.2 general purpose, RHEL 9.2 for SAP, RHEL8.8 general purpose, and RHEL 8.8 for SAP. For more information, see the [SAP documentation on OS](/docs/sap?topic=sap-compute-os-design-considerations#os-power) for IBM {{site.data.keyword.powerSys_notm}} and [FAQ documentation for supported OS versions](/docs/power-iaas?topic=power-iaas-powervs-faqs#os-versions).
- AIX 7.1 will continue to be charged at standard usage rates until further notice [^2]. For additional information on AIX lifecycle and service extensions, refer to [AIX support lifecycle information](https://www.ibm.com/support/pages/aix-support-lifecycle-information){: external}.
- {{site.data.keyword.powerSys_notm}} on IBM Cloud is now HIPAA-ready. See the [Compliance certifications](/docs/power-iaas?topic=power-iaas-compliances-list#HIPAA-cert) for more details.



[^2]: This update is regarding the service extension update in the [May 2023](/docs/power-iaas?topic=power-iaas-release-notes#may-2023) release notes section.

## March 2024
{: #mar-2024}

- Reserve an IP address from the {{site.data.keyword.powerSys_notm}} user interface. The IP address that you reserve are not assigned to a virtual server instance. For more information. see [Reserving IP addresses](/docs/power-iaas?topic=power-iaas-configuring-subnet#reserv-ip).
- New AIX 7.3 TL2, and 7.2 TL5 SP7 operating system images are available. For more information, see the [FAQ documentation](/docs/power-iaas?topic=power-iaas-powervs-faqs#os-versions).
- New IBM i 7.5 TR3, IBM i 7.4 TR9, and IBM i COR[^1] operating system images are available. For more information, see the [FAQ documentation](/docs/power-iaas?topic=power-iaas-powervs-faqs#os-versions).
- A new data center `CHE01` is available. The following are some capabilities that differ for this data center:
    - `CHE01` supports up to 5 GB Direct Link connections compared to other data centers that supports up to 10 GB.
    - To use Transit Gateway, you need to connect to `CHE01` using a different data center that supports Transit Gateway. For more information, see [Managing IBM Cloud connections](/docs/power-iaas?topic=power-iaas-cloud-connections).
    - IBM Cloud Monitoring and Power Edge Router network connectivity are currently unavailable for `CHE01`.
- SUSE part numbers for each tier are available. For more information, see the part numbers table in [Pricing for Power Virtual Servers](/docs/power-iaas?topic=power-iaas-pricing-virtual-server-on-cloud).
- Flexible I/O operation per second (IOPS) is now available in the `DAL12`, `DAL13`, `SAO01`, `SAO04`, `WDC04`, and `WDC06` data centers. For more information, see [Flexible IOPS](/docs/power-iaas?topic=power-iaas-on-cloud-architecture#storage-tiers).
- IBM Cloud Monitoring service is now available in `DAL13` and `FRA04`. For more information, see [Monitoring metrics for {{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-monitor-sysdig).
- PER is now available in the `OSA21`, `SYD05`, and `TOK04` data center. For more information, see [Getting Started with Power Edge Router](/docs/power-iaas?topic=power-iaas-per).

[^1]: IBM i Cloud Optical Repository (COR) is a virtual image that can be deployed and used as a Network File Server (NFS) to perform various IBM i tasks that require media. For more information on COR images, see [Cloud Optical Repository](https://cloud.ibm.com/media/docs/downloads/power-iaas/Cloud_Optical_Repository.pdf){: external}.

## February 2024
{: #feb-2024}

- PER is now available in the `SAO01` data center. For more information, see [Getting Started with Power Edge Router](/docs/power-iaas?topic=power-iaas-per).
- You can now provision the SLES 15 SP5 images. You are required to install an additional [software package](/docs/sap?topic=sap-power-vs-set-up-power-instances#power-vs-addtl-sw-sles-sap) as a prerequisite for SAP and Netweaver workloads.
- You can now choose to use IBM provided Linux images with your own license. While provisioning the boot image, select the OS image that is listed under the **Client supplied subscription** section. The stock non-Full Linux Subscription (FLS) images are available across all the data centers. For more information see, [Full Linux® subscription for Power Virtual Servers](/docs/power-iaas?topic=power-iaas-set-full-Linux).
- Flexible IOPS is now available in the `FRA04`, `LON06`, and `MAD02` data centers. For more information, see [Flexible IOPS](/docs/power-iaas?topic=power-iaas-on-cloud-architecture#storage-tiers).
- Global Replication Service (GRS) is now available in `WDC07` and `DAL10` data center pair.
- You can now migrate your workspace that uses a Direct Link connection to a PER workspace through a support ticket. For more information, see [Migrating to Power Edge Router](/docs/power-iaas?topic=power-iaas-migrate-ws-per).
- IBM Cloud Monitoring service is now available in `OSA21`, `DAL10`, and `WDC07`.

## January 2024
{: #jan-2024}

- Certain stock images for SAP will be updated with new Ansible packages. Until then it is recommended that you do not use the following images to create a new {{site.data.keyword.powerSys_notm}} instance for use with SAP workloads:
    - RHEL8-SP8-SAP
    - RHEL8-SP8-SAP-NETWEAVER
    - RHEL9-SP2-SAP
    - RHEL9-SP2-SAP-NETWEAVER

- The {{site.data.keyword.powerSys_notm}} workspaces provisioned in London, São Paulo, Osaka, Washington D.C., Montreal, and Toronto will send events to activity tracker instances in their respective regions effective from 29 January 2024. For more information, see [Activity tracker regions](/docs/power-iaas?topic=power-iaas-at-events#at-regions).
- PER is now available in `DAL12` and `FRA04`. For more information, see [Getting Started with Power Edge Router](/docs/power-iaas?topic=power-iaas-per).

- The direction going forward for VPN connectivity capability of the {{site.data.keyword.powerSys_notm}} will be to use the existing [IBM Cloud VPC VPN](/docs/power-iaas?topic=power-iaas-VPN-connections#vpc-vpn) for a one cloud experience, improved reliability, and high availability connections.

    The VPNAAS_CONNECT_APPLICATION_INSTANCE_HOURS part ID of the {{site.data.keyword.powerSys_notm}} is designed only for {{site.data.keyword.powerSys_notm}} and will be withdrawn by the end of March 2024.

    Existing users can choose to continue to use {{site.data.keyword.powerSys_notm}} VPN until the end of service or upgrade to their preferred IBM Cloud VPN for VPC service.

    By January 18, 2025, IBM will no longer deliver standard support for the {{site.data.keyword.powerSys_notm}} VPNaaS product, thus if you choose not to take the recommended action and run into issues, IBM will not support with end of life for parts occurring six months later on July 14, 2025. Additionally, after March 2024 new connections can no longer be provisioned with the {{site.data.keyword.powerSys_notm}} VPN thus you are encouraged to upgrade to the IBM Cloud VPC VPN at your earliest convenience and ideally before March 2024.

- IBM Cloud Monitoring service is now available in `SYD04`, `SAO04`, and `DAL12`.

## December 2023
{: #dec-2023}

- **New data center availability**
    - `MAD04` is available. It is a PER-enabled Power10 data center that supports IBM Cloud Monitoring service.
    - `SAO04` is available for PER.
  - **Cost estimator tool**
    A new cost estimator tool for {{site.data.keyword.powerSys_notm}} is available. You can access it from the {{site.data.keyword.powerSys_notm}} [home page](https://cloud.ibm.com/power/overview){: external}. To learn more about the cost estimator tool, see [Getting started with the cost estimator tool](/docs/power-iaas?topic=power-iaas-generating-an-estimate).
  - **Dedicated hosts**
    A new dedicated host capability is available. You can provision IBM Power S922 and S1022 servers for your dedicated use. For more information, see [Dedicated host](/docs/power-iaas?topic=power-iaas-dedicated-host).
  - **VPC VPN service**
    The VPC VPN is a robust service that replaces the legacy {{site.data.keyword.powerSys_notm}} VPN. To learn more on VPC VPN, see [Creating a Virtual Private Cloud VPN connection](/docs/power-iaas?topic=power-iaas-VPN-connections#vpc-vpn).
  - **Flexible IOPS**
    {{site.data.keyword.powerSys_notm}} now offers a tier-less storage service with the name Flexible IOPS. With Flexible IOPS, you can now change the IOPS level for your existing volumes and clone volumes to your choice of IOPS level, and much more. See: [Flexible IOPS](/docs/power-iaas?topic=power-iaas-on-cloud-architecture#storage-tiers).
  - New RHEL versions are available. See the [FAQ](/docs/power-iaas?topic=power-iaas-powervs-faqs#os-versions) page for details on the latest version.
  - **Update on the new SAP HANA large t-shirt profiles feature**
    The latest RHEL 9.2 for SAP, RHEL 8.8 for general purpose and SAP, and current RHEL 8.6 for general purpose and SAP OS images are being updated to support the larger t-shirt profiles. Until further notice, use t-shirt profiles with less than 64 cores for RHEL 9.2, RHEL 8.8, and RHEL 8.6 OS images. For more information, see the [SAP documentation on OS](/docs/sap?topic=sap-compute-os-design-considerations#os-power) for IBM {{site.data.keyword.powerSys_notm}}.
  - **New Global Replication Service (GRS) pairs support**
    The respective data center pairs `MAD02` and `FRA04` along with `MAD04` and `FRA05` now supports GRS.

## November 2023
{: #nov-2023}

- `WDC06` and `MAD02` data center are now available for PER. `MAD02` is a PER-enabled Power10 data center.
- Availibity of IBM Cloud Monitoring service is now extended in `FRA04`, `FRA05`, `LON04`, `LON06`, `MAD02`, `SAO01`, and `TOK04`.

## September 2023
{: #sep-2023}

- **{{site.data.keyword.powerSys_notm}} and SysDig Integration**
: You can now seamlessly monitor your platform metrics within the IBM Cloud environment by using the IBM Cloud Monitoring service. For detailed instructions on how to access and use this integration, refer to the documentation: [Monitoring metrics for {{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-monitor-sysdig).

The data center where you can monitor your platform metrics currently are `WDC06`, `SYD05`, and `WDC04` with other data center coming soon.
  {: note}

- **Introduction of {{site.data.keyword.powerSys_notm}} S1022 processor**
: The Power10 S1022 (9105-22A) is now available in `WDC07` data center. As we progress, additional data centers are made available.

  SAP Netweaver is not certified for use with S1022 systems, making them suitable exclusively for nonproduction workloads.
  {: note}

- **IBM i 7.3 service extension pricing**
: Effective 1 October 2023, IBM i 7.3 on {{site.data.keyword.powerSys_notm}} is at the end of normal support and will be in service extension. Service extension pricing is automatically added to the IBM i charge for IBM i 7.3 usage.

- **Addition of New Global Replication Service data center pair**
: {{site.data.keyword.powerSys_notm}} expanded the Global Replication Service (GRS) capabilities by adding a new data center pair - `DAL13` and `WDC04`. This enhancement is available on the Tier 1 storage support within the GRS framework. See: [Locations that support global replication service](/docs/power-iaas?topic=power-iaas-getting-started-GRS#locations-GRS).

## June 2023
{: #jun-2023}

-  The {{site.data.keyword.powerSys_notm}} enhances the management of stock images in the backend. This enhancement eliminates identical versions (copies) of stock images and improves the performance of copying a stock image in your account by using an image reference. Find more information in the [FAQ doc page](/docs/power-iaas?topic=power-iaas-powervs-faqs#stock-image-copy-improve).

    We are currently rolling out the feature to eliminate stock image copies in all data centers in phases. If your data center has already received the update, you notice that the export option for stock images is no longer available because you are using the reference of the stock image.

- IBM {{site.data.keyword.powerSys_notm}} is sequentially rolling out a Power Edge Router (PER) solution that is available in `DAL10` data center.

    PER improves network communication across different parts of the IBM network. See, [Getting Started with Power Edge Router](/docs/power-iaas?topic=power-iaas-per) for more information.

## May 2023
{: #may-2023}

- IBM {{site.data.keyword.powerSys_notm}} now supports two new data centers `WDC07` (Washington DC) and `SAO04` (São Paulo).
- IBM {{site.data.keyword.keymanagementserviceshort}} is now supported on AIX and Linux workloads. For more information, see [Integrating {{site.data.keyword.powerSys_notm}} with IBM Cloud Key Management Services](/docs/power-iaas?topic=power-iaas-integrate-hpcs#AIX-hpcs).
- Effective 1 May 2023, AIX 7.1 on {{site.data.keyword.powerSys_notm}} is covered for software support. In {{site.data.keyword.powerSys_notm}}, starting March 2024[^1], Service Extension pricing is automatically added to the AIX charge for AIX 7.1 usage. AIX 7.1 Service Extension was announced on January 24, 2023. For more information see, [AIX support lifecycle information](https://www.ibm.com/support/pages/aix-support-lifecycle-information){: external}.

[^1]: See the update in the [April 2024](/docs/power-iaas?topic=power-iaas-release-notes#apr-2024) release note section.

## March 2023
{: #mar-2023}

- **Update on the new SAP HANA large t-shirt profiles feature**:
    IBM supports SLES15 SP4 for SAP and RHEL8.6 for SAP OS images with all other features on all t-shirt profiles with fewer than 64 cores. These SLES15 SP4 for SAP and RHEL8.6 for SAP OS images are while being updated to support the larger t-shirt profiles. Until further notice, use the larger t-shirt profiles with the SLES15 SP3 for SAP OS image or the RHEL8.4 for SAP OS image. For more information, see the SAP documentation on [OS for IBM Power Virtual Servers](/docs/sap?topic=sap-compute-os-design-considerations#os-power).

    The RHEL8.6 for SAP OS image is available in `DAL10`, `DAL12`, `FRA04`, `FRA05`, `LON04`, `LON05`, `MON01`, `SYD05`, `TOR01`, `WDC04`, and `WDC06`. The image is available in all data centers by 3/27/23.

- **{{site.data.keyword.powerSys_notm}} cost estimator**:
    Effective 3/23/23, two of the latest large SAP HANA t-shirt profiles `mh1-90x16200` and `mh1-100x18000` are available options in the [cost estimator](https://cloud.ibm.com/power/overview#estimator){: external}. In April 2023, the latest largest profile `mh1-125x22500` will also be available in the estimator.

- **Access your event logs and notifications**:
    You can now access your event logs and notification from the **Event logs** page on the {{site.data.keyword.powerSys_notm}} user interface. For more information, see [Managing events logs and notifications](/docs/power-iaas?topic=power-iaas-manage-event-logs)

## February 2023
{: #feb-2023}

- Added a new data center DAL10 in the existing list of {{site.data.keyword.powerSys_notm}} data centers. For more information, see [Creating a {{site.data.keyword.powerSys_notm}} workspace](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#creating-service).

## December 2022
{: #dec-2022}

- Get the list of internationally recognized {{site.data.keyword.powerSys_notm}} compliance certifications. For more information, see [{{site.data.keyword.powerSys_notm}} compliance certifications](/docs/power-iaas?topic=power-iaas-compliances-list).

- You can integrate Hyper Protect Crypto Services (HPCS) with {{site.data.keyword.powerSys_notm}} to securely store and protect encryption key information for AIX and Linux. For more information, see [Integrating {{site.data.keyword.powerSys_notm}} with HPCS](/docs/power-iaas?topic=power-iaas-integrate-hpcs).

## September 2022
{: #sept-2022}

- You can share a group of processors between multiple virtual machines that allows you to group your applications together by using the shared processor pool. For more information, see [Managing shared processor pool](/docs/power-iaas?topic=power-iaas-manage-SPP).

- {{site.data.keyword.powerSys_notm}} allows you to automate the complete data recovery solution by using the API and CLI interfaces of a global replication service. For more information, see [Managing a global replication service](/docs/power-iaas?topic=power-iaas-getting-started-GRS).

- You can choose to deploy Epic workloads on a VM for more cost savings. For more information, see [Configuring a VM for Epic workloads](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#configuring-a-vm-for-epic-workloads).

- The full Linux subscription on {{site.data.keyword.powerSys_notm}} now supports SLES 15 SP4 (General).

## August 2022
{: #aug-2022}

- You can use FalconStor VTL in {{site.data.keyword.powerSys_notm}} for data protection and cloud migration as a Service for IBM i. See [Managing Virtual tape library](/docs/power-iaas?topic=power-iaas-manage-vtl).

## July 2022
{: #jul-2022}

- You can use IBM Transit Gateway to interconnect your {{site.data.keyword.powerSys_notm}} to the {{site.data.keyword.cloud_notm}} classic and Virtual Private Cloud (VPC). See [Creating IBM Cloud connections](/docs/power-iaas?topic=power-iaas-cloud-connections#create-cloud-connections).
- {{site.data.keyword.powerSys_notm}} now supports a full Linux subscription on RHEL 8.6. See [Full Linux® subscription for {{site.data.keyword.powerSys_notm}}s](/docs/power-iaas?topic=power-iaas-set-full-Linux).

## June 2022
{: #jun-2022}

- {{site.data.keyword.powerSys_notm}} now supports Linux (RHEL and SLES) stock images for non-SAP applications by using full Linux subscription. See [Full Linux® subscription for {{site.data.keyword.powerSys_notm}}s](/docs/power-iaas?topic=power-iaas-set-full-Linux).
- IBM i 7.5 is supported on {{site.data.keyword.powerSys_notm}}s.
- With virtual appliances independent software vendors (ISV) can offer OVA (ISV software plus operating system of your choice) for quick deployment of {{site.data.keyword.powerSys_notm}} workloads. See [Managing virtual appliances](/docs/power-iaas?topic=power-iaas-virtual-appliances).
