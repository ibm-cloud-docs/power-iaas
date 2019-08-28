---

copyright:
  years: 2019

lastupdated: "2019-08-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}

# What is a Power Systems Virtual Server?
{: #about-power-virtual-server}

{{site.data.keyword.powerSysFull}} uses the existing IBM Cloud platform to create {{site.data.keyword.powerSysFull}}, also known as logical partitions (LPAR), that run on IBM Power Systems hardware with the PowerVM hypervisor.
{:shortdesc}

{{site.data.keyword.powerSysFull}} are a form of infrastructure as a service (IaaS). With the {{site.data.keyword.powerSys_notm}} service, you can quickly create and deploy one or multiple virtual servers that are running either the AIX or IBM i operating systems in a public cloud. After you provision the virtual server in the cloud, it is your responsibility to make sure that the AIX or IBM i operating system is secure.

Current AIX and IBM i clients can use {{site.data.keyword.powerSysFull}} for a number of workload scenarios, including disaster recovery, development environments, and partial IT infrastructure moves. {{site.data.keyword.powerSysFull}} clients can not only stay competitive with the scaling of their infrastructure, but also stay flexible with the management and capacity of their workloads both on- and off-premise. And since the infrastructure layer is identical, system administrators who run on-premise AIX and IBM i systems today can use their same tools, workflows, and enhancements in the cloud.

## Key features
{: #apvs-key-features}

The following are some of the key features for {{site.data.keyword.powerSys_notm}}.

### Straightforward billing
{: #apvs-billing}

The {{site.data.keyword.powerSys_notm}} uses a monthly billing rate that includes the licenses for the AIX and IBM i operating systems. The monthly billing rate is pro-rated by the hour based on the resources that are deployed to the {{site.data.keyword.powerSys_notm}} instance for the month. When you create the {{site.data.keyword.powerSys_notm}} instance, you can see the total cost for your configuration based on the options that you specify.  You can quickly identify what configuration options provide you with the best value for your business needs. For more information, see [Pricing](/docs/infrastructure/power-iaas?topic=power-iaas-pricing-virtual-server#pricing-virtual-server).

### Hybrid cloud environment
{: #apvs-hybrid}

You can use the {{site.data.keyword.powerSys_notm}}s to run any AIX or IBM i workloads off-premise from your existing Power Systems hardware infrastructure. Running your workloads in the public cloud allows you to enjoy all the advantages the cloud as to offer such as self-service, fast delivery, elasticity, and connectivity to other IBM Cloud services. Although your AIX and IBM i workloads are running in the cloud, you still keep the same scalable, resilient, production-ready features that Power Systems Hardware provides.

### Infrastructure customization
{: #apvs-customization}

You can configure and customize the following options when you create a {{site.data.keyword.powerSys_notm}}:

* Number of virtual server instances
* Number of cores
* Amount of memory
* Data volume size and type (HDD or SSD)
* Private or public network

### Bring your own image
{: #apvs-own-image}

IBM provides you with stock AIX and IBM i operating system images when you create a {{site.data.keyword.powerSys_notm}}. However, you can bring your own custom AIX or IBM i operating system image that you have previously deployed and tested. For more information, see [Configuring a custom image](/docs/infrastructure/power-iaas?topic=power-iaas-configuring-custom-image#configuring-custom-image).

## Hardware specifications
{: #apvs-hardware-specifications}

The following IBM Power Systems hardware hosts the {{site.data.keyword.powerSys_notm}}:

**Compute**

[Power System E880 (9119-MHE) ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/downloads/cas/EE476WAP){: new_window}

* 9 TB memory
* 8 x 16 Gigabit PCI Express Dual-port Fibre Channel (FC)
* 10 x 10 Gigabit Ethernet-SR PCI Express Dual-port

[Power System S922 (9009-22A) ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/downloads/cas/KQ4BOJ3N){: new_window}

* 384 GB memory
* 2 x 16 Gigabit PCI Express Dual-port FC
* 3 x 10 Gigabit Ethernet-SR PCI Express Dual-port

**Storage**

* Storewize V7000F(2076-AF6) Dual Controller
* Storwize V7000 (2076-624) Dual Controller

**Network**

* Cisco Nexus9000 93180YC-EX (10G)
* Cisco Nexus9000 C9348GC-FXP (1G)

## Public and private networks
{: #apvs-public-and-private}

When you create a {{site.data.keyword.powerSys_notm}}, you can select a private network interfaces or a public network interface.

**Public network**

* Easy and quick method to connect to a {{site.data.keyword.powerSys_notm}} instance.
* IBM configures the network infrastructure to enable a secure public network connection from the internet to the {{site.data.keyword.powerSys_notm}} instance.
* Connectivity is implemented by using an IBM Cloud Virtual Router Appliance (VRA) and a Direct Link Connect connection.
* Protected by firewall and supports the following secure network protocols:
    * SSH
    * HTTPS
    * Ping
    * IBM i 5250 terminal emulation with SSL (port 992)

**Private network**

* Allows the resources for your {{site.data.keyword.powerSys_notm}} instance to access existing {{site.data.keyword.cloud_notm}} resources, such as Bare Metal Servers, Kubernetes containers, or cloud storage.
* Uses a Direct Link Connect connection to connect to your IBM Cloud account network and resources. The process for creating a Direct Link Connect connection can take a few days because IBM Cloud support must configure the link.
* Required for communication between different {{site.data.keyword.powerSys_notm}} instances.

  For more information about the different options for configuring a private network, see [Configure a private network](/docs/infrastructure/power-iaas?topic=power-iaas-cpn-configuring#cpn-configuring).
  {: note}

The following figure displays the the basic configuration for a public and private network:

![Displays how network traffic flows for public or private connection](/images/power-iaas-network1.svg "Displays how network traffic flows for public or private connection"){: caption="Figure 1. Private and public network configuration" caption-side="bottom"}

<!-- Customer A is able to connect to a public network by using a Direct Link Dedicated connection with their {{site.data.keyword.cloud_notm}} Power account. -->
<!-- Customer A is able to connect to a private network by using a Direct Link Connect connection with their {{site.data.keyword.cloud_notm}} account. -->
<!-- Customer A can use either a public or private network to access their {{site.data.keyword.powerSys_notm}}. -->
<!-- Customer B is able to connect to only a private network by using a Direct Link Connect connection with their {{site.data.keyword.cloud_notm}} account.  -->