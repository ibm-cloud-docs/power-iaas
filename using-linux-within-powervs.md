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

1. Deploy the Linux VMs that will be using the SNAT router to access the internet. Make sure that the SNAT router is routing the attached private networks.

2. Set the default router for your Linux VM to the SNAT router IP on the private network.

# Deploying a Linux virtual machine (VM)
{: deploy-linux-vm}

You can use the Power Systems Virtual Server service to deploy a generic Linux&trade; virtual machine (VM). When you are provisioning a VM, select **Linux-Client supplied subscription** for your operating system. The Power Systems Virtual Server service does not provide Linux stock images. You must bring your own Linux image (OVA format) and subscription.

You must obtain the subscription for Linux directly from the vendor. After you deploy your Linux VM, you must log in to the VM and register it with the Linux vendor's satellite server. To reach the Linux vendor satellite servers (where you can register and obtain packages and fixes), you must attach a public network to your VM. To learn more about the registration process, see [Registering and subscribing to RHEL](/docs/power-iaas?topic=power-iaas-using-linux).

## How to create an OVA format Linux image
{: ova-linux-image}

Learn how to create an OVA image of a RHEL operating system and import it into the Power Systems Virtual Server environment. You can use PowerVC or VIOS to capture an image.

### Using PowerVC to capture and import an OVA image
{: import-ova-image}

If you've deployed PowerVC in your on-premises environment, you can use it to [capture any supported LPAR](https://www.ibm.com/support/knowledgecenter/en/SSXK2N_1.4.0/com.ibm.powervc.standard.help.doc/powervc_capturing_hmc.html){: new_window} and create an OVA image. After you create the OVA image, upload it to your Cloud Object Storage account and import it into the Power Systems Virtual Server environment.

### Capturing an image from VIOS
{: capture-image}

The [create_ova RPM](https://cloud.ibm.com/media/docs/downloads/create_ova-1.0-2.aix7.2.ppc.rpm){: new_window} contains scripts that create a virtual disk image of a `mksysb` backup, raw disk file, or disk volume and packages the content into a consumable Open Virtual Appliance (OVA) package. To use this capture method, it is required that the root file system be present on a single disk. When you use the VIOS disk capture capability, you must obtain the appropriate disk volume name of the client VM that you are trying to capture. For more information on finding the disk configuration of a VIOS client, see [VIOS disk mapping in a nutshell](https://developer.ibm.com/technologies/systems/articles/au-viosmapping/){: new_window}. **You must shut down your Linux LPAR for this method to work. Otherwise, you might encounter disk errors and the OVA image might not boot**.

The `create_ova RPM` also contains the `create_ova` man page and license. You must install the RPM on VIOS.
{: note}

To see the contents of the RPM package, enter the rpm command as shown in the following example:

```
# rpm -qlp /tmp/create_ova-1.0-2.aix7.2.ppc.rpm
/opt/freeware/doc/create_ova-1.0
/opt/freeware/doc/create_ova-1.0/create_ova.pdf
/opt/freeware/licenses/create_ova-1.0
/opt/freeware/licenses/create_ova-1.0/LICENSE
/opt/ibm/sysmgt/cloudrdy
/opt/ibm/sysmgt/cloudrdy/EXTRAS/pv-1.6.0-1.aix6.1.ppc.rpm
/opt/ibm/sysmgt/cloudrdy/LICENSE
/opt/ibm/sysmgt/cloudrdy/bin/cloud_setup
/opt/ibm/sysmgt/cloudrdy/bin/create_ova
/opt/ibm/sysmgt/cloudrdy/bin/print_ovf
/opt/ibm/sysmgt/cloudrdy/doc/create_ova.pdf
/usr/share/man/man1/create_ova.1
```

Once you obtain the correct disk name (through virtual adapter mapping), you can create a virtual disk image and package the contents into an OVA. After the RPM is installed, the man page and the executable (*create_ova*) are available in the normal paths. Note that a link is made to `/usr/bin/create_ova`, so there is no need to set the user path. If you decide to perform an uninstall, any links, files, or directories that are tracked by the RPM for this package are removed. The following example contains a list of sample commands and output:

You can upload the ova.gz file into your Cloud Object storage account. Once you upload it, go to the Power Systems Virtual Server user interface and import the OVA image from your Cloud Object Storage account.
{: important}

```
ssh (isotopes-vios2)

IBM Virtual I/O Server

login: padmin
padmin's Password:
Last login: Sun May 10 17:41:00 CDT 2020 on /dev/pts/0

$ lsmap -vadapter vhost18
SVSA            Physloc                                      Client Partition ID
--------------- -------------------------------------------- ------------------
vhost18         U8233.E8B.100121P-V8-C21                     0x0000000f

VTD                   isotopes13_dsk1
Status                Available
LUN                   0x8100000000000000
Backing device        isotopes13_lv1
Physloc
Mirrored              N/A

$ oem_setup_env
# create_ova -o /datafs -d risotopes13_lv1 -t sles -e -f
Initializing resources ...

Checking for resource group ROOTVG...
Checking for resource group PIPEVIEWER...already installed.
Checking /datafs space requirement...done

Checking for resource group sles_20200511101424.img...
20480+0 records in1.2MiB/s] [10.6MiB/s] [=======================================================================> ] 99% ETA 0:00:00
20480+0 records out
  20GiB 0:32:15 [10.6MiB/s] [10.6MiB/s] [=======================================================================>] 100%
41943040+0 records in
41943040+0 records out
done

Checking for resource group sles_20200511101424.ova.gz...
Checking /datafs space requirement...done
a ./sles_20200511101424.ovf 4 blocks
a ./sles_20200511101424.img 41943040 blocks
  20GiB 0:49:23 [6.91MiB/s] [6.91MiB/s] [=======================================================================>] 100%

Done verifying resources.

# ls -l /datafs/sles_20200511101424.ova.gz
-rw-r--r--    1 root     staff    1890363097 May 11 2020  /datafs/rsle_20200511101424.ova.gz
```
{: screen}

