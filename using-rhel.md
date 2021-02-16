---

copyright:
  years: 2020

lastupdated: "2020-12-14"

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

# Using RHEL within the Power Systems Virtual Server service
{: linux-with-powervs}

You can use the Power Systems Virtual Server service to deploy a generic Red Hat Enterprise Linux (RHEL) virtual machine (VM). When you are provisioning a VM, select **Linux – Client supplied subscription** for your operating system. The Power Systems Virtual Server service does not provide Linux stock images. You must bring your own Linux image (OVA format) and subscription. The following versions of Linux are supported:

- RHEL 8.3 Batch Update 1

To view the certification details in the Red Hat catalog, see [IBM Power System E980 (9080-M9S)](https://catalog.redhat.com/cloud/instance-types/detail/5636281){: new_window}{: external} and [IBM Power System S922 (9009-22A)](https://catalog.redhat.com/cloud/instance-types/detail/5636201){: new_window}{: external}.

You must obtain the subscription for the Linux operating system directly from the vendor. After you deploy your Linux VM, you must log in to the VM and register it with the Linux vendor’s satellite server. To reach the Linux vendor satellite servers (where you can register and obtain packages and fixes), you must attach a public network to your VM.

When you create an OVA image, you must include the appropriate IBM Cloud environment *cloud-init* packages. Download the appropriate cloud-init and configure it as per the steps documented at [Installing and configuring cloud-init on Linux](https://www.ibm.com/support/knowledgecenter/en/SSXK2N_1.4.4/com.ibm.powervc.standard.help.doc/powervc_install_cloudinit_hmc.html){: new_window}{: external}.

You can use the [pvsadm tool](https://github.com/ppc64le-cloud/pvsadm) to convert the RHEL 8.3 Qcow2 images to OVA image.
{: note}

## Registering and subscribing to RHEL
{: subscribing-to-rhel}

The Power Systems Virtual Server service does not provide a subscription to RHEL. You must purchase the RHEL subscription from Red Hat and then enable it.

You cannot contact the Red Hat-based repository and download the appropriate software packages without first enabling your RHEL subscription.
{: note}

1. To buy a RHEL subscription, see [Red Hat Enterprise Linux Server](https://www.redhat.com/en/store/red-hat-enterprise-linux-server){: new_window}{: external}.

2. To register your system, see [Quick Registration for RHEL](https://access.redhat.com/documentation/en-us/red_hat_subscription_management/1/html/quick_registration_for_rhel/index){: new_window}{: external}.

## Capturing and importing a RHEL image
{: import-rhel-image}

To use RHEL within the Power Systems Virtual Server service, you can use the [IBM Power Virtualization Center (PowerVC)](https://www.ibm.com/support/knowledgecenter/en/SSXK2N_1.4.4/com.ibm.powervc.standard.help.doc/powervc_images_hmc.html){: new_window} to capture your Linux image, then [import it](/docs/power-iaas?topic=power-iaas-deploy-custom-image) as an Open Virtualization Appliance (OVA) file. You must also bring your own license (BYOL). If you cannot use PowerVC to capture an image, see the [Power Systems OVA image capture](/docs/power-iaas?topic=power-iaas-linux-deployment#vios-capture) instructions.

## Linux networking
{: linux-networking}

To connect a Linux virtual machine (VM) to the public internet, you must add a public network when you provision a Power Systems Virtual Server. You must set up a Linux-based Network Address Translation (NAT) gateway on a public-facing Linux VM if you have Linux VMs that do not need an internet-facing external IP address. For more information on NAT router, [Linux NAT Router Explained](https://www.slashroot.in/linux-nat-network-address-translation-router-explained){: new_window}{: external}.

### Configuring Network Address Translation (NAT) in the Power Systems Virtual Server environment
{: nat-configuration}

Most organizations are allotted a limited number of publicly routable IP addresses from their ISP. Due to this limited allowance, administrators must find a way to share access to internet services without giving limited public IP addresses to every node on the LAN. RHEL 8 uses the nftables utility, instead of iptables, to set up complex firewalls. For instructions on setting up NAT on RHEL, see [Configuring NAT using nftables](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/configuring_and_managing_networking/getting-started-with-nftables_configuring-and-managing-networking#configuring-nat-using-nftables_getting-started-with-nftables){: new_window}{: external}.

Complete these steps to accurately configure your Source NAT (SNAT) router:

1. Deploy a RHEL LPAR on a public network.

2. Create subnets that require the SNAT function to get internet access.

3. Use the following commands to allow private network traffic to be accessible for SNAT-ing:

  ```
  iptables -A FORWARD -i eth1 -j ACCEPT
  iptables -A FORWARD -o eth1 -j ACCEPT
  ```

  These commands assume that the network device for the public network is eth0, and eth1 for the private network.
  {: important}

You can permanently set **IP forwarding** by editing the `/etc/sysctl.conf` file:

1. Find and edit the following line within the */etc/sysctl.conf* file (replacing 0 with 1 if required):

  ```
  net.ipv4.ip_forward = 1
  ```

2. Update the *sysctl.conf* file by entering the following command:

  ```
  sysctl -p /etc/sysctl.conf
  ```

3. Finally, configure the source NAT by entering the following command:

  ```
  iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
  ```

### Configuring Linux VMs to use a SNAT router
{: use-snat-router}

1. [Deploy the Linux VMs](/docs/power-iaas?topic=power-iaas-linux-deployment) that will be using the SNAT router to access the internet. Make sure that the SNAT router is routing the attached private networks.

2. Assign the SNAT router IP (eth1 as per the previous example) on the private network as the default router on your newly created Linux VM.