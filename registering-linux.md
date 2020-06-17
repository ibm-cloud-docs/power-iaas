---

copyright:
  years: 2019, 2020

lastupdated: "2020-06-15"

keywords: linux, registering, subscription, sles, powervc, snat

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

You can use the {{site.data.keyword.powerSys_notm}}) service to deploy a generic Linux™ virtual machine (VM). When you are provisioning a VM, select **Linux – Client supplied subscription** for your operating system. The {{site.data.keyword.powerSys_notm}} service does not provide Linux stock images. You must bring your own Linux image (OVA format) and subscription. The following versions of Linux are supported:

- `SLES 12 : Minimum level: SP5`
- `SLES 15 : Minimum level SP1 + kernel 4.12.14-197.45-default`

You must obtain the subscription for the Linux operating system directly from the vendor. After you deploy your Linux VM, you must log in to the VM and register it with the Linux vendor’s satellite server. To reach the Linux vendor satellite servers (where you can register and obtain packages and fixes), you must attach a public network to your VM.

When you create an OVA image, you must include the appropriate IBM Cloud environment `cloud-init` packages. Please download the appropriate `cloud-init` package from [IBM PowerVC packages](http://public.dhe.ibm.com/systems/virtualization/powervc/){: new_window}{: external}.

You must exercise caution when you use the Linux VM resize option (especially the resize reduction of a resource). There are Linux kernel fixes that are required. If you do not integrate these Linux kernel fixes, the VM will go into an **Error** state requiring help from IBM support. You can use the `sudo zypper update` command to update all of the Linux packages. You must verify that the distro (kernel) level contains these Linux fixes. If not, you should avoid using the resize option altogether or perform it in conjunction with a VM stop/restart action.
{: important}

## Registering and subscribing to SLES
{: #registering-sles}

The {{site.data.keyword.powerSys_notm}} service does not provide a subscription to SLES. You must purchase the SLES subscription from SUSE and then enable it.

You cannot contact the SUSE-based repository and download the appropriate software packages without first enabling your SLES subscription.
{: note}

1. To buy a SUSE subscription, see [How to Buy](https://www.suse.com/support/?id=SUSE_Linux_Enterprise_Server_for_SAP_Applications#how-to-buy){: new_window}{: external}.

2. To register your system, see [Registering an Installed System](https://documentation.suse.com/sles/12-SP4/single-html/SLES-deployment/#sec-y2-sw-register){: new_window}{: external}.

## Capturing and importing a SLES image
{: #preparing-linux-image}

To use SLES within the {{site.data.keyword.powerSys_notm}} service, you can use the [IBM Power Virtualization Center (PowerVC)](https://www.ibm.com/support/knowledgecenter/en/SSXK2N_1.4.4/com.ibm.powervc.standard.help.doc/powervc_images_hmc.html){: new_window}{: external} to capture your Linux image, then [import it](/docs/power-iaas?topic=power-iaas-deploy-custom-image) as an Open Virtualization Appliance (OVA) file. You must also bring your own license (BYOL). If you cannot use PowerVC to capture an image, see the [Power Systems OVA image capture](/docs/power-iaas?topic=power-iaas-linux-deployment#vios-capture) instructions.

## Linux networking
{: #linux-networking}

To connect a Linux virtual machine (VM) to the public internet, you must add a public network when you provision a {{site.data.keyword.powerSys_notm}}. You must set up a Linux-based NAT gateway on a public-facing Linux VM if you have Linux VMs that do not need an internet-facing external IP address. For more information, see [19.6 Basic Router Setup](https://documentation.suse.com/sles/15-SP1/html/SLES-all/cha-network.html#sec-network-router){: new_window}{: external} and [Linux NAT(Network Address Translation) Router Explained](https://www.slashroot.in/linux-nat-network-address-translation-router-explained){: new_window}{: external}.

### Configuring SNAT in the Power Systems Virtual Server environment
{: #configuring-snat}

Most organizations are allotted a limited number of publicly routable IP addresses from their ISP. Due to this limited allowance, administrators must find a way to share access to internet services without giving limited public IP addresses to every node on the LAN. To learn more, see [Forward and NAT rules](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/4/html/security_guide/s1-firewall-ipt-fwd){: new_window}{: external}.

### SNAT router configuration
{: #snat-router-configuration}

Complete these steps to accurately configure your SNAT router.

1. Deploy a SLES LPAR on a public network.
2. Create subnets that require the SNAT function to get internet access.
3. Use the following commands to allow private network traffic to be accessible for SNAT-ing:

```
iptables -A FORWARD -i eth1 -j ACCEPT
iptables -A FORWARD -o eth1 -j ACCEPT
```
{: codeblock}

These commands assume that the network device for the public network is `eth0`, and `eth1` for the private network.
{: important}

You can permanently set **IP forwarding** by editing the `/etc/sysctl.conf` file:

1. Find and edit the following line within the `/etc/sysctl.conf` file (replacing `0` with `1` if required): `net.ipv4.ip_forward = 1`.

2. Update the `sysctl.conf` file by entering the following command: `sysctl -p /etc/sysctl.conf`.

3. Finally, configure the source NAT by entering the following command: `iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE`.

### Configuring Linux VMs to use a SNAT router
{: #linux-snat-router}

1. Deploy the Linux VMs that will be using the SNAT router to access the internet. Make sure that the SNAT router is routing the attached private networks.

2. Set the default router for your Linux VM to the SNAT router IP on the private network.
