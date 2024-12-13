---

copyright:
  years: 2019, 2024

lastupdated: "2024-12-05"

keywords: ibm i, program temporary fixes

subcollection: power-iaas

---
{{site.data.keyword.attribute-definition-list}}

# Minimum PTF levels for IBM i
{: #minimum-levels}

---



{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}


---

Install the following program temporary fixes (PTFs) depending on the version of IBM i that is being used:

- IBM i 7.2 - 5770SS1 SI71091 (prerequisite System Licensed Internal Code (SLIC) PTFs: MF66395, MF66394, MF66391, SI77413, SI77272)
- IBM i 7.3 - MF99207 (TR7) and SI77412, SI77206
- IBM i 7.4 - MF99301 (TR1) and SI77411, SI77202
- IBM i 7.5 - No PTF is required

For more information on installing PTF packages, see [Installing cumulative PTF packages](https://www.ibm.com/docs/en/i/7.4?topic=scenario-installing-cumulative-ptf-packages){: external}. The `SNDPTFORD` command can also be used to send PTFs to the system, see [Send PTF Order (SNDPTFORD)](https://www.ibm.com/docs/en/i/7.4?topic=ssw_ibm_i_74/cl/sndptford.htm){: external}.

When you use an IBM i custom image, these PTFs must be installed and the software that is required for `Cloud-Init`. For more information, see [Cloud-Init Support for IBM i](https://www.ibm.com/support/pages/node/1166194){: external}.
An overview of IBM i fix concepts and terms is found at [Fixes concepts and terms](https://www.ibm.com/docs/en/i/7.4?topic=fixes-concepts-terms){: external}.

To learn more about the options available to upgrade the IBM i operating system, see [Performing IBM i Upgrades on Power Virtual Servers](https://www.ibm.com/support/pages/performing-ibm-i-upgrades-power-virtual-servers){: external}.
{: important}

## Required PTFs for iSCSI Virtual Tape Library (VTL)
{: #ptfs-iscsi-vtl}

You must install the program temporary fixes (PTFs) depending on the version of IBM i that you are using. To view PTF for each release along with the configuration procedures, see [IBM i Support for iSCSI VTL](https://www.ibm.com/support/pages/ibm-i-removable-media-support-iscsi-vtl).

## Best practices for using IBM i stock images
{: #best-practice-stock-images}

1.	When you select an IBM i stock image, you must verify that the latest group of PTFs are installed, especially the Hiper and Security group. For more information, see [IBM i Group PTFs with level](https://www.ibm.com/support/pages/ibm-i-group-ptfs-level).
2.	Refer to the [IBM PSIRT blog](https://www.ibm.com/blogs/psirt/) for the latest Product Security Incident Response.
3.	You can subscribe to valuable product notifications at [My Notifications](https://www.ibm.com/support/pages/node/253211).
4. Cloud Optical Repository (COR) is a virtual image that can be deployed and used as a Network File Server (NFS) to perform various IBM i tasks that require media. This virtual optical image includes a collection of the media necessary for various IBM i tasks, for all supported IBM i releases. With the COR image deployed, a second {{site.data.keyword.powerSys_notm}} Instance can be deployed on the same VLAN that is set up as the client and pointed to the COR (target) NFS Server Instance. For more information on COR images, see [Cloud Optical Repository](https://cloud.ibm.com/media/docs/downloads/power-iaas/Cloud_Optical_Repository.pdf){: external}.
