---

copyright:
  years: 2020, 2024

lastupdated: "2024-10-04"

keywords: rhel, using RHEL with PowerVS, Linux, NAT, SNAT

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Using RHEL within the {{site.data.keyword.powerSys_notm}}
{: #linux-with-powervs}

---

IBM {{site.data.keyword.powerSys_notm}} located in IBM data centers: [Off-premises]{: tag-blue}

IBM {{site.data.keyword.powerSys_notm}} Private Cloud: [On-premises]{: tag-red}

---

You can deploy a Linux&reg; virtual machine (VM) by using one of the IBM stock OS images, or you can bring your own Linux image (in OVA format).
{: shortdesc}

You can choose from the following options:
- Register for a full Linux subscription.
- Use your own Linux subscription from a Linux vendor.

If you choose to register for full Linux subscription, an extra charge applies to your provisioned VM for Linux support through IBM. A full Linux subscription requires use of one of the stock operating system images that are provided by IBM. In the image menu, select **IBM provided subscription** to choose one of the IBM stock images. For more information on how to provision and register by using a full Linux subscription, see [Full Linux subscription for {{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-set-full-Linux).

If you plan to use your own license, select the OS image that is suffixed with `-BYOL`. On the VM Provisioning page, these images are listed under the **Client supplied subscription** section.
{: note}

The {{site.data.keyword.powerSysFull}} provides Linux (RHEL and SLES) stock images for SAP and non-SAP applications. To know more about the SLES versions that are supported, see [What versions of AIX, IBM i, and Linux are supported?](/docs/power-iaas?topic=power-iaas-powervs-faqs#os-versions).




To view the certification details in the Red Hat catalog, see [IBM Power System E980 (9080-M9S)](https://catalog.redhat.com/hardware/system/detail/17035){: external} and [IBM Power System S922 (9009-22A)](https://catalog.redhat.com/hardware/system/detail/9225){: external}.

If you do not choose to use the full Linux subscription for {{site.data.keyword.powerSys_notm}} you must obtain the subscription directly from the vendor and bring your image. After you deploy your Linux VM, you must log in to the VM and register it with the Linux vendor’s satellite server. To reach the Linux vendor satellite servers (where you can register and obtain packages and fixes), you must attach a public network to your VM.

When you create an OVA image, ensure that the image includes the correct version of RHEL image with cloud-init version from March 2021, or later. If you are using an earlier RHEL image, download the appropriate cloud-init and configure it as in the steps that are documented at [Installing and configuring cloud-init on Linux](https://www.ibm.com/support/knowledgecenter/en/SSXK2N_1.4.4/com.ibm.powervc.standard.help.doc/powervc_install_cloudinit_hmc.html){: external}.

You can use the [pvsadm tool](https://github.com/ppc64le-cloud/pvsadm#readme) to convert the RHEL 8.3 Qcow2 images to OVA image. The pvsadm tool is an open source tool and not an IBM-supported product. If you experience any issues with this tool, you can [open an issue](https://github.com/ppc64le-cloud/pvsadm/issues) within the pvsadm tool GitHub repository. If you use any tool for RHEL releases that are in extended support, ensure that only the Extended Update Support (EUS)-related packages are downloaded and packaged by the tool.
{: note}

## Registering and purchasing a subscription to RHEL
{: #subscribing-to-rhel}

You cannot contact the Red Hat-based repository and download the appropriate software packages without first enabling your RHEL subscription.
{: note}

1. To buy an RHEL subscription, see [Red Hat Enterprise Linux Server](https://www.redhat.com/en/store/red-hat-enterprise-linux-ibm-power-little-endian){: external}.

2. To register your system, see [Quick Registration for RHEL](https://docs.redhat.com/en/documentation/subscription_central/1-latest/html/getting_started_with_rhel_system_registration/basic-reg-rhel-gui){: external}.


## Capturing and importing an RHEL image
{: #import-rhel-image}

To use RHEL within {{site.data.keyword.powerSys_notm}}, you can use the [IBM Power Virtualization Center (PowerVC)](https://www.ibm.com/support/knowledgecenter/en/SSXK2N_1.4.4/com.ibm.powervc.standard.help.doc/powervc_images_hmc.html){: external} to capture your Linux image, then [import it](/docs/power-iaas?topic=power-iaas-deploy-custom-image) as an Open Virtualization Appliance (OVA) file. You must also bring your own license (BYOL). If you cannot use PowerVC to capture an image, see the [Power OVA image capture](/docs/power-iaas?topic=power-iaas-linux-deployment#vios-capture) instructions.

## Linux networking
{: #linux-networking}

To connect a Linux virtual machine (VM) to the public internet, you must add a public network when you provision a {{site.data.keyword.powerSys_notm}}. You must set up a Linux-based Network Address Translation (NAT) gateway on a public-facing Linux VM if you have Linux VMs that do not need an internet-facing external IP address. For more information on NAT router, [Linux NAT Router Explained](https://www.slashroot.in/linux-nat-network-address-translation-router-explained){: external}.

When you are configuring a Source NAT (SNAT) gateway between your public and private networks, ensure that the TCP checksum offload option is disabled. You must also set the maximum transmission unit (MTU) value to 1450 on the network interface that is connected to the private network. To ensure that the interface checksum offloading and MTU settings of the network interface are persistent whenever the virtual machine is restarted, you need to modify the configuration files of your network interface.

The TCP checksum offload option must be disabled on the private network interface of the SNAT Gateway and virtual Ethernet device must be of the type `ibmveth`. You do not need to change the TCP checksum offload option for public network interface. IBM {{site.data.keyword.powerSys_notm}} VMs are deployed by using ibmveth devices only.
{: note}

You can verify that the device interface type is `ibmveth` by using the following command:

```text
ethtool -i <interface name> | grep driver
```

The following instructions are applicable to RHEL version 8.1 and later. If you need more help to configure network interfaces, refer to the Red Hat documentation.

1. Identify the name of the private network interface that you want to modify. Use the following command to identify the network interface names based on the IP address that is assigned to the network interface:

    ```text
    ip -4 a s (for IPv4 address)
    ip -6 a s (for IPv6 address)
    ```

2. Edit the `ifcfg-<NIC>` file (where NIC is the network interface name that is identified in step 1).

    ```text
      RHEL:  /etc/sysconfig/network-scripts/ifcfg-<NIC>
    ```
    - Add or modify the following lines:

    ```text
     For RHEL:
       MTU=1450
       ETHTOOL_OPTS="-K <NIC> rx off"
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

### Configuring Network Address Translation (NAT) in the {{site.data.keyword.powerSys_notm}} environment
{: #nat-configuration}

Most organizations are allotted a limited number of publicly routable IP addresses from their ISP. Due to this limited allowance, administrators must find a way to share access to internet services without giving limited public IP addresses to every node on the LAN. RHEL 8 uses the nftables utility, instead of iptables, to set up complex firewalls. For instructions on setting up NAT on RHEL, see [Configuring NAT using nftables](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/configuring_and_managing_networking/getting-started-with-nftables_configuring-and-managing-networking#configuring-nat-using-nftables_getting-started-with-nftables){: external}.

Before running the `iptables` commands, complete the following steps to ensure that the configuration settings persist after the virtual machine is restarted.

1. Use the following command to list all the zones:
   ```text
   firewall-cmd --get-zones
   block dmz drop external home internal nm-shared public trusted work
   ```

2. Use the following command to list the network interfaces for zones:
   ```text
   firewall-cmd --zone=public --list-all
   ```

3. To turn on the masquerade option that will set the configuration settings persist after the restart operations, run the following command:
   ```text
   firewall-cmd --zone=public --add-masquerade --permanent
   success
   ```

4. Restart the system firewall:
   ```text
   systemctl restart firewalld
   ```

5. Verify whether the configuration is successful:
   ```text
   #sudo firewall-cmd --zone=public --query-masquerade
   yes
   ```

Complete these steps to accurately configure your Source NAT (SNAT) router:

1. Deploy an RHEL LPAR on a public network.

2. Create subnets that require the SNAT function to get internet access.

3. Use the following commands to allow private network traffic to be accessible for SNAT-ing:

   ```text
   iptables -A FORWARD -i eth1 -j ACCEPT
   iptables -A FORWARD -o eth1 -j ACCEPT
   ```

   These commands assume that the network device for the public network is eth0, and eth1 for the private network.
   {: important}

You can permanently set **IP forwarding** by editing the `/etc/sysctl.conf` file:

1. Find and edit the following line within the */etc/sysctl.conf* file (replacing 0 with 1 if required):

    ```text
    net.ipv4.ip_forward = 1
    ```

2. Update the *sysctl.conf* file by entering the following command:

    ```text
    sysctl -p /etc/sysctl.conf
    ```

3. Finally, configure the source NAT by entering the following command:

    ```text
    iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
    ```

### Configuring Linux VMs to use a SNAT router
{: #use-snat-router}

1. [Deploy the Linux VMs](/docs/power-iaas?topic=power-iaas-linux-deployment) that use the SNAT router to access the internet. Make sure that the SNAT router is routing the attached private networks.

2. Assign the SNAT router IP (eth1 as in the previous example) on the private network as the default router on your newly created Linux VM.
