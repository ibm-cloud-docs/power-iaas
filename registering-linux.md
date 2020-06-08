---

copyright:
  years: 2019, 2020

lastupdated: "2020-06-08"

keywords: linux, registering, subscription, sles, rhel, red hat, powervc, snat

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

# Using Linux within the Power Systems Virtual Server service
{: #using-linux}

The {{site.data.keyword.powerSysShort}} service supports SUSE Linux&reg; Enterprise Server (SLES) and Red Hat Enterprise Linux (RHEL).
{: shortdesc}

The following Linux operating systems are supported with `cloud-init` version **cloud-init-19.1-4.sles15.ibm.noarch** on all IBM Power Systems hardware that is used in the {{site.data.keyword.powerSys_notm}} service:

- Red Hat Enterprise Linux (RHEL)
- SUSE Linux Enterprise (SLES)

For additional support, refer to the distribution (distro). You can find a list of cloud-init packages at [IBM PowerVC packages](http://public.dhe.ibm.com/systems/virtualization/powervc/){: new_window}{: external}.

## Registering and subscribing to SLES
{: #registering-sles}

The {{site.data.keyword.powerSys_notm}} service does not provide a subscription to SUSE Linux. You must purchase the SUSE Linux subscription from SUSE and then enable it.

You cannot contact the SUSE-based repository and download the appropriate software packages without first enabling your SUSE Linux subscription.
{: note}

1. To buy a SUSE subscription, see [How to Buy](https://www.suse.com/support/?id=SUSE_Linux_Enterprise_Server_for_SAP_Applications#how-to-buy){: new_window}{: external}.
2. To register your system, see [Registering an Installed System](https://documentation.suse.com/sles/12-SP4/single-html/SLES-deployment/#sec-y2-sw-register){: new_window}{: external}.

## Registering and subscribing to RHEL
{: #registering-rhel}

The {{site.data.keyword.powerSys_notm}} service does not provide a subscription to RHEL. You must purchase the RHEL subscription from RHEL and then enable it. For more information on moving Red Hat product subscriptions to the IBM Cloud, see [Red Hat Cloud Access Frequently Asked Questions](https://access.redhat.com/articles/3664231){: new_window}{: external}.

You cannot contact the RHEL-based repository and download the appropriate software packages without first enabling your RHEL Linux subscription.
{: note}

1. To buy a RHEL subscription, see [How to Buy](https://www.redhat.com/en/store/linux-platforms){: new_window}{: external}.
2. To register your system, see [How to register and subscribe a system to the Red Hat Customer Portal](https://access.redhat.com/solutions/253273){: new_window}{: external}.

## Capturing and importing a RHEL or SUSE image
{: #preparing-linux-image}

To use either RHEL or SUSE within the {{site.data.keyword.powerSys_notm}} service, you must use the [IBM Power Virtualization Center (PowerVC)](https://www.ibm.com/support/knowledgecenter/en/SSXK2N_1.4.4/com.ibm.powervc.standard.help.doc/powervc_images_hmc.html){: new_window}{: external} to capture your Linux image, then [import it](/docs/power-iaas?topic=power-iaas-deploy-custom-image) as an Open Virtualization Appliance (OVA) file. You must also bring your own license (BYOL). If you are cannot use PowerVC to capture an image, there is a separate tool available for [Power Systems OVA image capture](/docs/power-iaas?topic=power-iaas-linux-deployment#vios-capture).

## Linux networking
{: #linux-networking}

To connect a Linux virtual machine (VM) to the public internet, you must add a public network when you provision a {{site.data.keyword.powerSys_notm}}. You must set up a Linux-based NAT gateway on a public-facing Linux VM if you have Linux VMs that you do not want to have an internet-facing external IP address. For more information, see [19.6 Basic Router Setup](https://documentation.suse.com/sles/15-SP1/html/SLES-all/cha-network.html#sec-network-router){: new_window}{: external} and [Linux NAT(Network Address Translation) Router Explained](https://www.slashroot.in/linux-nat-network-address-translation-router-explained){: new_window}{: external}.

### Configuring SNAT in the Power Systems Virtual Server environment by using RHEL
{: #configuring-snat}

Most organizations are allotted a limited number of publicly routable IP addresses from their ISP. Due to this limited allowance, administrators must find a way to share access to internet services without giving limited public IP addresses to every node on the LAN. To learn more, see [Forward and NAT rules](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/4/html/security_guide/s1-firewall-ipt-fwd){: new_window}{: external}.

### SNAT router configuration
{: #snat-router-configuration}

1. Deploy a RHEL 7 LPAR on a public network and create subnets (that need to use the SNAT function to get internet access).
2. Use the following commands to allow private network traffic to be accessible for SNAT-ing (these commands assume that the network device for the public IP is `eth0`, and `eth1` for the private network):

```
iptables -A FORWARD -i eth1 -j ACCEPT
iptables -A FORWARD -o eth1 -j ACCEPT
```
{: codeblock}

You can permanently set **IP forwarding** by editing the `/etc/sysctl.conf` file:

1. Find and edit the following line within the `/etc/sysctl.conf` file (replacing `0` with `1` if required): `net.ipv4.ip_forward = 1`.
2. To perform the update to the `sysctl.conf` file, enter the following command: `sysctl -p /etc/sysctl.conf`.
3. Finally, configure the source NAT by entering the following command: `iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE`.

### Configuring Linux VMs to use a SNAT router
{: #linux-snat-router}

1. Deploy the Linux VMs that will be using the SNAT router to access the internet. Make sure that the SNAT router is routing the attached private networks.
2. Set the default router for your Linux VM to the SNAT router IP on the private network.
