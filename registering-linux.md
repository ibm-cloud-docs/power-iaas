---

copyright:
  years: 2019, 2024

lastupdated: "2025-07-08"

keywords: linux, registering, subscription, sles, powervc, snat

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}


# Using SLES within IBM {{site.data.keyword.powerSys_notm}}
{: #using-linux}

---

{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}


---

You can deploy a Linux&reg; virtual machine (VM) by using one of the IBM stock operating system (OS) images, or you can bring your own Linux image (in OVA format).
{: shortdesc}

You can choose from the following options:
- Register for a full Linux subscription.
- Use your own Linux subscription from a Linux vendor.

If you choose to register for full Linux subscription, an extra charge applies to your provisioned VM for Linux support through IBM. A full Linux subscription requires use of one of the stock OS images that are provided by IBM. In the image menu, select **IBM provided subscription** to choose one of the IBM stock images. For more information on how to provision and register by using a full Linux subscription, see [Full Linux subscription for {{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-set-full-Linux).

If you plan to use your own license, select the OS image that is suffixed with `-BYOL`. On the VM Provisioning page, these images are listed under the **Client supplied subscription** section.
{: note}

The {{site.data.keyword.powerSysFull}} provides Linux (RHEL and SLES) stock images for SAP and non-SAP applications. To know more about the SLES versions that are supported, see [What versions of AIX, IBM i, and Linux are supported?](/docs/power-iaas?topic=power-iaas-powervs-faqs#os-versions).


To ensure that you are running the supported OS levels and to plan for upgrades to the latest levels, refer to [SLES](https://www.suse.com/lifecycle#suse-linux-enterprise-server-15){: external} OS release lifecycle information.
{: important}

If you do not choose to use the full Linux subscription for {{site.data.keyword.powerSys_notm}} you must obtain the subscription directly from the vendor and bring your image. After you deploy your Linux VM, you must log in to the VM and register it with the Linux vendor’s satellite server. To reach the Linux vendor satellite servers (where you can register and obtain packages and fixes), you must attach a public network to your VM.

When you create an OVA image, you must include the appropriate {{site.data.keyword.powerSys_notm}} environment `cloud-init` packages. Download the appropriate `cloud-init` package from [Installing and configuring cloud-init](https://www.ibm.com/docs/en/powervc/2.0.1?topic=machine-installing-configuring-cloud-init){: external}.

To run SUSE Linux Enterprise Server on {{site.data.keyword.powerSys_notm}}, your hardware must meet the minimum memory requirements. A minimum of 1024 MB of memory is required for a minimal installation. On machines with more than two processors, add 512 MB per CPU. The memory values specified are valid only for the installation of the operating system. The actual memory requirement in production depends on the workload of the system. For more information about the SLES hardware recommendations, see [https://documentation.suse.com/sles/15-SP4/html/SLES-all/cha-power.html]{: external}.

{{_include-segments/sap-subscription-mode.md}}

## Registering and purchasing a subscription to SLES
{: #registering-sles}

You cannot contact the SUSE-based repository and download the appropriate software packages without first enabling your SLES subscription.
{: note}

1. To buy a SUSE subscription, see [How to Buy](https://www.suse.com/support/?id=SUSE_Linux_Enterprise_Server_for_SAP_Applications#how-to-buy){: external}.

2. To register your system, see [Registering an Installed System](https://www.suse.com/support/kb/doc/?id=000018564){: external} .

## Capturing and importing a SLES image
{: #preparing-linux-image}

To use SLES within the {{site.data.keyword.powerSys_notm}}, you can use the [IBM Power Virtualization Center (PowerVC)](https://www.ibm.com/support/knowledgecenter/en/SSXK2N_1.4.4/com.ibm.powervc.standard.help.doc/powervc_images_hmc.html){: external} to capture your Linux image, then [import it](/docs/power-iaas?topic=power-iaas-deploy-custom-image) as an Open Virtualization Appliance (OVA) file. You must also BYOL. If you cannot use PowerVC to capture an image, see the [Power OVA image capture](/docs/power-iaas?topic=power-iaas-linux-deployment#vios-capture) instructions.

## Linux networking
{: #sles-linux-networking}

To connect a Linux virtual machine (VM) to the public internet, you must add a public network when you provision a {{site.data.keyword.powerSys_notm}}. You must set up a Linux-based NAT gateway on a public-facing Linux VM if you have Linux VMs that do not need an internet-facing external IP address. For more information, see [19.6 Basic Router Setup](https://documentation.suse.com/sles/15-SP1/html/SLES-all/cha-network.html#sec-network-router){: external} and [Linux NAT(Network Address Translation) Router Explained](https://www.slashroot.in/linux-nat-network-address-translation-router-explained){: external}.

When you are configuring a Source NAT (SNAT) gateway between your public and private networks, ensure that the TCP checksum offload option is disabled. You must also set the maximum transmission unit (MTU) value to 1450 on the network interface that is connected to the private network. To ensure that the interface checksum offloading and MTU settings of the network interface are persistent whenever the virtual machine is restarted, you need to modify the configuration files of your network interface.

The TCP checksum offload option must be disabled on the private network interface of the SNAT Gateway and virtual Ethernet device must be of the type `ibmveth`. You do not need to change the TCP checksum offload option for public network interface. {{site.data.keyword.powerSysFull}} VMs are deployed by using ibmveth devices only.
{: note}

You can verify that the device interface type is `ibmveth` by using the following command:

```text
ethtool -i <interface name> | grep driver
```

The following instructions are applicable to SLES version SP15. If you need additional help to configure network interfaces, refer to the SLES documentation.

1. Identify the name of the private network interface that you want to modify. Use the following command to identify the network interface names based on the IP address that is assigned to the network interface:

    ```text
    ip -4 a s (for IPv4 address)
    ip -6 a s (for IPv6 address)
    ```

2. Edit the `ifcfg-<NIC>` file (where NIC is the network interface name that is identified in step 1).

    ```text
       SLES:  /etc/sysconfig/network/ifcfg-<NIC>
    ```
    - Add or modify the following lines:

    ```text
     For SLES:
       MTU='1450'
       ETHTOOL_OPTIONS='-K <NIC> rx off'
    ```

3. Restart the VM.

4. After the restart operation is complete, verify that the MTU value and the checksum offloading setting are correct.
    - Verify the checksum offloading setting by running the following command:

      ```text
       ethtool -k eth0
       Features for eth0:
       rx-checksumming: off
       tx-checksumming: off
       <cut>
      ```

The `ethtool` command sets both the rx-checksumming and tx-checksumming options to off when one of these options is disabled.
{: note}

Verify the MTU value by running the following command:
```text
ip link show eth0
eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1450 qdisc fq_codel state UNKNOWN mode DEFAULT <...>
```

### Configuring SNAT in the {{site.data.keyword.powerSys_notm}} environment
{: #configuring-snat}

Most organizations are allotted a limited number of publicly routable IP addresses from their ISP. Due to this limited allowance, administrators must find a way to share access to internet services without giving limited public IP addresses to every node on the LAN. To learn more, see [Forward and NAT rules](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/4/html/security_guide/s1-firewall-ipt-fwd){: external}.

### SNAT router configuration
{: #snat-router-configuration}

Complete these steps to accurately configure your SNAT router.

1. Deploy a SLES LPAR on a public network.
2. Create subnets that require the SNAT function to get internet access.
3. Use the following commands to allow private network traffic to be accessible for SNAT-ing:

```text
iptables -A FORWARD -i eth1 -j ACCEPT
iptables -A FORWARD -o eth1 -j ACCEPT
```

These commands assume that the network device for the public network is `eth0`, and `eth1` for the private network.
{: important}

You can permanently set **IP forwarding** by editing the `/etc/sysctl.conf` file:

1. Find and edit the following line within the `/etc/sysctl.conf` file (replacing `0` with `1` if required): `net.ipv4.ip_forward = 1`.

2. Update the `sysctl.conf` file by entering the following command: `sysctl -p /etc/sysctl.conf`.

3. Finally, configure the source NAT by entering the following command: `iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE`.

### Configuring Linux VMs to use a SNAT router
{: #linux-snat-router}

1. [Deploy the Linux VMs](/docs/power-iaas?topic=power-iaas-linux-deployment) that will be using the SNAT router to access the internet. Make sure that the SNAT router is routing the attached private networks.

2. Set the default router for your Linux VM to the SNAT router IP on the private network.
