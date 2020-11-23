---

copyright:
  years: 2020

lastupdated: "2020-11-23"

keywords: 

subcollection: power-iaas

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}

# Using Linux within the Power Systems Virtual Server
{: linux-with-powervs}

You can use the Power Systems Virtual Server service to deploy a generic Linux&trade; virtual machine (VM). When you are provisioning a VM, select **Linux – Client supplied subscription** for your operating system. The Power Systems Virtual Server service does not provide Linux stock images. You must bring your own Linux image (OVA format) and subscription. The following versions of Linux are supported:

- RHEL 7.7 - Minimum level: TBD
- RHEL 8.0 - Minimum level: TBD
- RHEL 8.2 – Minimum level: TBD

You must obtain the subscription for the Linux operating system directly from the vendor. After you deploy your Linux VM, you must log in to the VM and register it with the Linux vendor’s satellite server. To reach the Linux vendor satellite servers (where you can register and obtain packages and fixes), you must attach a public network to your VM.

When you create an OVA image, you must include the appropriate IBM Cloud environment *cloud-init* packages. Please download the appropriate *cloud-init* packages from [IBM PowerVC packages](http://public.dhe.ibm.com/systems/virtualization/powervc/){: new_window}{: external}.

## Registering and subscribing to RHEL
{: subscribing-to-rhel}

The Power Systems Virtual Server service does not provide a subscription to RHEL. You must purchase the RHEL subscription from Red Hat and then enable it.

You cannot contact the Red Hat-based repository and download the appropriate software packages without first enabling your SLES subscription.
{: note}

1. To buy a RHEL subscription, see **TBD**.

2. To register your system, see **TBD**.

## Capturing and importing a RHEL image
{: import-rhel-image}

To use RHEL within the Power Systems Virtual Server service, you can use the [IBM Power Virtualization Center (PowerVC)](https://www.ibm.com/support/knowledgecenter/en/SSXK2N_1.4.4/com.ibm.powervc.standard.help.doc/powervc_images_hmc.html){: new_window} to capture your Linux image, then [import it](/docs/power-iaas?topic=power-iaas-deploy-custom-image) as an Open Virtualization Appliance (OVA) file. You must also bring your own license (BYOL). If you cannot use PowerVC to capture an image, see the [Power Systems OVA image capture](/docs/power-iaas?topic=power-iaas-linux-deployment#vios-capture) instructions.

## Linux networking
{: linux-networking}

To connect a Linux virtual machine (VM) to the public internet, you must add a public network when you provision a Power Systems Virtual Server. You must set up a Linux-based NAT gateway on a public-facing Linux VM if you have Linux VMs that do not need an internet-facing external IP address. For more information, see [19.6 Basic Router Setup](https://documentation.suse.com/sles/15-SP1/html/SLES-all/cha-network.html#sec-network-router){: new_window}{: external} and [Linux NAT(Network Address Translation) Router Explained](https://www.slashroot.in/linux-nat-network-address-translation-router-explained){: new_window}{: external}.

### Configuring SNAT in the Power Systems Virtual Server environment
{: configure-snat-in-powervs}

Most organizations are allotted a limited number of publicly routable IP addresses from their ISP. Due to this limited allowance, administrators must find a way to share access to internet services without giving limited public IP addresses to every node on the LAN. To learn more, see [Forward and NAT rules](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/4/html/security_guide/s1-firewall-ipt-fwd){: new_window}{: external}.

### SNAT router configuration
{: snat-configuration}

Complete these steps to accurately configure your SNAT router.

1. Deploy a RHEL LPAR on a public network.

2. Create subnets that require the SNAT function to get internet access.

3. Use the following commands to allow private network traffic to be accessible for SNAT-ing: