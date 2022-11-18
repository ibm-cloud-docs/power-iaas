---

copyright:
  years: 2019, 2022

lastupdated: "2022-09-18"

keywords: linux deployment, ova, powervc capture, vios

subcollection: power-iaas

---

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

# Creating a custom Linux image in OVA format
{: #linux-deployment}

You can use {{site.data.keyword.powerSys_notm}} workspace to deploy a generic Linux&reg; virtual machine (VM). When you are provisioning a VM, select **Linux-Client supplied subscription** for your operating system (the OS filename for Linux-Client supplied subscription starts with `Linux-RHEL` or `Linux-SUSE`). The {{site.data.keyword.powerSys_notm}} workspace provides few Linux stock images for SAP HANA and SAP NetWeaver applications. You can also bring your own Linux image (OVA format) and subscription. Power Systems Virtual Server also supports Linux (RHEL and SLES) stock images for non-SAP applications by using full Linux subscription. For more information, see [Full Linux® subscription for Power Systems Virtual Servers](/docs/power-iaas?topic=power-iaas-set-full-Linux).
{: shortdesc}

For SAP applications, ensure that you use an IBM stock OS image for SAP. These images are certified for SAP application use; bring your own images are not supported. To learn more about SAP applications with PowerVS, please see these [Must-Reads](https://cloud.ibm.com/docs/sap?topic=sap-power-vs-planning-items){: external} before you start deployment. 
{:note:}

You must obtain the subscription for Linux directly from the vendor. After you deploy your Linux VM, you must log in to the VM and register it with the Linux vendor's satellite server. To reach the Linux vendor satellite servers (where you can register and obtain packages and fixes), you must attach a public network to your VM. To learn more about the registration process, see [Registering and subscribing to SLES](/docs/power-iaas?topic=power-iaas-using-linux#registering-sles) or [Registering and subscribing to RHEL](/docs/power-iaas?topic=power-iaas-linux-with-powervs#subscribing-to-rhel).

## How to create an OVA format Linux image
{: #ova-format}

Learn how to create an OVA image of a Linux operating system and import it into the {{site.data.keyword.powerSys_notm}} environment. You can use PowerVC or VIOS to capture an image.

### Using PowerVC to capture and import an OVA image
{: #powervc-capture}

If you've deployed PowerVC in your on-premises environment, you can use it to [capture any supported LPAR](https://www.ibm.com/support/knowledgecenter/en/SSXK2N_1.4.0/com.ibm.powervc.standard.help.doc/powervc_capturing_hmc.html){: external} and create an OVA image. After you create the OVA image, upload it to your Cloud Object Storage account and import it into the {{site.data.keyword.powerSys_notm}} environment.

### Capturing an image from VIOS
{: #vios-capture}

The [`create_ova` RPM](https://cloud.ibm.com/media/docs/downloads/create_ova-1.0-2.aix7.2.ppc.rpm){: external} contains scripts that create a virtual disk image of a `mksysb` backup, raw disk file, or disk volume and packages the content into a consumable Open Virtual Appliance (OVA) package. To use this capture method, it is required that the root file system be present on a single disk. When you use the VIOS disk capture capability, you must obtain the appropriate disk volume name of the client VM that you are trying to capture. For more information on finding the disk configuration of a VIOS client, see [VIOS disk mapping in a nutshell](https://developer.ibm.com/technologies/systems/articles/au-viosmapping/){: external}. **You must shut down your Linux LPAR for this method to work. Otherwise, you might encounter disk errors and the OVA image might not boot**.

The `create_ova` RPM also contains the `create_ova` man page and license. You must install the RPM on VIOS releases which are prior to VIOS 3.1.2.0. The `create_ova` command is provided as a system command on VIOS release 3.1.2.0, or later.
{: note}

To see the contents of the RPM package, enter the `rpm` command as shown in the following example:

```text
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

Once you obtain the correct disk name (through virtual adapter mapping), you can create a virtual disk image and package the contents into an OVA. After the RPM is installed, the man page and the executable (`create_ova`) are available in the normal paths. Note that a link is made to `/usr/bin/create_ova)`, so there is no need to set the user path. If you decide to perform an uninstall, any links, files, or directories that are tracked by the RPM for this package are removed. The following example contains a list of sample commands and output:

You can upload the `ova.gz` file into your Cloud Object storage account. Once you upload it, go to the {{site.data.keyword.powerSys_notm}} user interface and import the OVA image from your Cloud Object Storage account.
{: important}

```text
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
# create_ova -o /datafs -d risotopes13_lv1 -t sles -e -f  /use rhel for RHEL
Initializing resources ...

Checking for resource group ROOTVG...
Checking for resource group PIPEVIEWER...already installed.
Checking /datafs space requirement...done

Checking for resource group linux_20200511101424.img...
20480+0 records in1.2MiB/s] [10.6MiB/s] [=======================================================================> ] 99% ETA 0:00:00
20480+0 records out
  20GiB 0:32:15 [10.6MiB/s] [10.6MiB/s] [=======================================================================>] 100%
41943040+0 records in
41943040+0 records out
done

Checking for resource group linux_20200511101424.ova.gz...
Checking /datafs space requirement...done
a ./linux_20200511101424.ovf 4 blocks
a ./linux_20200511101424.img 41943040 blocks
  20GiB 0:49:23 [6.91MiB/s] [6.91MiB/s] [=======================================================================>] 100%

Done verifying resources.

# ls -l /datafs/linux_20200511101424.ova.gz
-rw-r--r--    1 root     staff    1890363097 May 11 2020  /datafs/linux_20200511101424.ova.gz
```
