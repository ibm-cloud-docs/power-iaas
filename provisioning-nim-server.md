---

copyright:
  years: 2019, 2020

lastupdated: "2020-02-25"

keywords: troubleshooting, NIM server, support, fixes, updates

subcollection: power-iaas

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}

# Setting up a Network Installation Management (NIM) server
{: #provisioning-nim}

You can provision an AIX virtual machine (VM) and use it as a NIM server for troubleshooting purposes or for downloading fixes and updates.

1. Determine the hostname and IP address of the system by using the following two commands, `hostname` and `ifconfig -a`.

    ![Determining your hostname and IP address](./images/terminal-aix-hostname.png "Determining your hostname and IP address"){: caption="Figure 1. Determining your hostname and IP address" caption-side="bottom"}

2. Using the information from the previous step, add an entry for your hostname and IP address into `/etc/hosts`. For example, `echo "192.168.0.15 aix-7100-05-04" >> /etc/hosts`.

3. Run the following command, `nim_master_setup -a device=/usr/sys/inst.images -a mk_resource=no`.

    ![Creating a NIM master](./images/terminal-aix-nim.png "Creating a NIM master"){: caption="Figure 2. Creating a NIM master" caption-side="bottom"}

4. Once completed, the NIM master file set has been installed and the basic resource objects created. The administrator is now able to add more NIM clients and define resources.

    ![NIM master installation summary](./images/terminal-aix-nim-summary.png "NIM master installation summary"){: caption="Figure 3. NIM master installation summary" caption-side="bottom"}

For more information, see [Setting up NIM to boot into maintenance mode](https://www.ibm.com/support/pages/setting-nim-boot-maintenance-mode){: external}. If you are unfamiliar with this process, create a [new support case](/docs/power-iaas?topic=power-iaas-getting-help-and-support).
