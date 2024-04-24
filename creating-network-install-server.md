---

copyright:
  years: 2019, 2020

lastupdated: "2020-04-13"

keywords: ibm i, network intsall server, volume_list

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Setting up an IBM i network install server
{: #preparing-install-server}

[On Cloud]{: tag-blue}

Before you can install or upgrade an IBM i system through the network, you must set up a network installation server. The network installation server contains images of the IBM i operating system, its internal code as well as licensed programs and PTFs. To share virtual optical images through a network, the network installation server must meet the following requirements:

## Configuration
{: #ibmi-nw-server-config}

To complete the configuration of an IBM i network installation server, see [Virtual optical storage using the Network File System](https://www.ibm.com/docs/en/i/7.4?topic=storage-virtual-optical-using-network-file-system){: external} and [IBM i Network Install](http://www.redbooks.ibm.com/redpapers/pdfs/redp4937.pdf){: external}.

Cloud Optical Repository (COR) is a virtual image that can be deployed and used as a Network File Server (NFS) to perform various IBM i tasks that require media. This virtual optical image includes a collection of the media necessary for various IBM i tasks, for all supported IBM i releases. With the COR image deployed, a second {{site.data.keyword.powerSys_notm}} Instance can be deployed on the same VLAN that is set up as the client and pointed to the COR (target) NFS Server Instance. For more information on COR images, see [Cloud Optical Repository](https://cloud.ibm.com/media/docs/downloads/power-iaas/Cloud_Optical_Repository.pdf){: external}.
