---

copyright:
  years: 2019

lastupdated: "2019-09-12"

keywords: aix iso, install media, entitled software support, ess

subcollection: power-iaas

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:external: .external}

# Using Entitled Software Support (ESS) to download ISO images of AIX installation media
{: using-ess-iso}

Entitled software means that the software is covered by a valid Software Maintenance Agreement (SWMA). If you obtain software maintenance by using a custom SWMA contract (as opposed to a standard SWMA), you might need to register on the [Entitled Software Support (ESS) website to access the custom SWMA contract. Without access to the customer SWMA contract, you might not be able to download ISO images. You cannot download all levels of entitled software. For example, you cannot download installation media for AIX technology levels that are outdated.
{: shortdesc}

The ESS customer number registration process can take several days.
{: important}

## Before you begin
{: before-you-begin}

Before you can download an ISO image of an AIX installation DVD, you must have an [IBM ID](https://www.ibm.com/account/reg/us-en/signup?formid=urx-19776){: external} and the IBM customer number under which the software was ordered. You must also have one of the following items:

* An IBM machine serial number on which the software is entitled
* IBM system number (from software packing list)
* IBM order number (from software packing list)
* Custom SWMA contract number

If you are missing any of the listed items, contact your IBM or Business Partner Power Systems sales representative with the machine type-model and serial number on which the software is licensed. If you are uncertain of the machine type-model of a server on which AIX is already running in your environment, enter the commands `lsconf` and `head` and look for the **System Model** and **Machine Serial Number** fields. Registering with a serial number provides access only to the entitled software download.

## Using the ESS website to download an ISO image
{: downloading-ess-iso}

1. Go to the ESS website and log in with your IBM ID.
2. Click **Register customer number** in the navigation pane and enter either a **Hardware or Software serial number** or **Customer Number (include country code)**. Decide whether you want to register your customer number permanently and click **Submit**.

    The first IBM ID to register a customer number becomes the primary contact for that customer number. If you attempt to register a customer number that already has a primary contact, you're offered the option of sending a request. The request goes to the customer number's primary contact and asks for access. You are not given access until the primary contact responds to that request.
    {: note}

3. After IBM has registered the customer number or server, click **Software downloads** under **My entitled software** in the navigation pane.
4. Select a category and group.
5. Check the box next to the installation image you would like to download and click **Continue**.
6. Next, select the language feature that you want and click **Continue**. Agree to the terms and conditions.
7. Click the **Click here to use HTTP** link to download the ISO image by using HTTP. You can also click the **Download now** button.

AIX installation DVDs are delivered as ISO image files, while other installation images are delivered as compressed _tar_ archives. In some cases, AIX ISO images are zipped and can be unzipped by using the [AIX Toolbox for Linux Application](https://www.ibm.com/support/pages/aix-toolbox-linux-applications-overview). After you download an ISO image, it is not necessary to burn a DVD to access the contents of the ISO image.
{: tip}

## Copying and installing your ISO image to an AIX virtual machine (VM)
{: copying-installing-iso}

After you download an AIX installation DVD as an ISO image, you must copy the image to an existing AIX VM's file system. To copy the image, you must use Secure Copy Protocol (SCP). SCP is a protocol for securely transferring files between a local and a remote host or between two remote hosts.

1. Copy the ISO image to an existing AIX VM's file system by using the [`scp`](https://www.ibm.com/support/knowledgecenter/ST5Q4U_1.5.2/com.ibm.storwize.v7000.unified.152.doc/usgr_usng_scp.html){: external}) command.

    The scp command does not work unless you are on a public network.
    {: important}

    ```shell
    scp [Options] [[User@]From_Host:]Source_File [[User@]To_Host:][Destination_File]
    ```
    {: pre}

1. Run the [`loopmount`](https://www.ibm.com/support/knowledgecenter/en/ssw_aix_72/l_commands/loopmount.html){: external} command to make the ISO image available as a file system by using the loopback device.

    ```shell
    loopmount {-i imagefile | -l device} [-o mount options -m mountpoint]
    ```
    {: pre}

1. Use the [`installp`](https://www.ibm.com/support/knowledgecenter/ssw_aix_72/i_commands/installp.html) command to install the image in a compatible installation package. You must use the `-R` flag to specify your ISO image's path.

    ```shell
    installp [-R _path_] [-a |-a -c [-N]] [-_eLogFile_] [-V _Number_  [-_dDevice_] [-E] [-Y] [-b] [-S] [-B] [-D] [-I] [-p] [-Q] [-q] [ -v] [-X] [-F | -g] [-O { [r] [s] [u]}] [-t _SaveDirectory_ ] [-w] [-_zBlockSize_] { _FilesetName_ [_Level_]... | -f _ListFile_ | all}
      ```
    {: pre}

1. Upon the completion of the installation, the system generates an installation summary. Verify that the **Result** column shows success for all of the loaded files. You can also verify the installation's success by typing, `lslpp -aL | grep -i idsldap`, at a command line.
