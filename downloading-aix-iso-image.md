---

copyright:
  years: 2019, 2020

lastupdated: "2019-12-09"

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

# Using Entitled Software Support (ESS) to download ISO images
{: #using-ess-iso}

Entitled software means that the software is covered by a valid Software Maintenance Agreement (SWMA). If you obtain software maintenance by using a custom SWMA contract (as opposed to a standard SWMA), you might need to register on the [Entitled Software Support (ESS)](https://www.ibm.com/servers/eserver/ess/ProtectedServlet.wss){: new_window}{: external} website to access the custom SWMA contract. Without access to the customer SWMA contract, you might not be able to download ISO images. You cannot download all levels of entitled software. For example, you cannot download installation media for AIX technology levels that are outdated.
{: shortdesc}

The ESS customer number registration process can take several days.
{: important}

## Before you begin
{: #before-you-begin-ess}

Before you can download an ISO image of an AIX installation DVD, you must have an [IBM ID](https://www.ibm.com/account/reg/us-en/signup?formid=urx-19776){: new_window}{: external} and your IBM Cloud customer number. If you bought entitlement through [Passport Advantage](https://www.ibm.com/software/passportadvantage/){: external}, Entitled Systems Support (ESS) will not recognize your customer number. In this case, you need to get the customer number that the entitlement is being purchased under and go to Passport Advantage to download the files under the **5737-D09** product ID. Meanwhile, you can also purchase and download other optional software products for AIX through Passport Advantage, such as IBM Open XL C/C++ and Fortran compilers, under the **5725-C72** and **5725-C74** product ID. For informtaion on using Passport advantage, see [Passport Advantage](https://www.ibm.com/docs/en/b2b-integrator/6.0.1?topic=items-passport-advantage){: new_window}{: external}.

## Using the ESS website to download an ISO image
{: #downloading-ess-iso}

To download an ISO image from the ESS website, complete the following steps. If you have issues related to ESS entitlement or image availability, you can contact ESS support through [Contacts page](https://www.ibm.com/servers/eserver/ess/OpenServlet.wss). See [Handling AIX filesets](https://www-01.ibm.com/support/docview.wss?uid=ibm10871636){: external} for information on handling AIX fileset requisite issues.

1. Go to the ESS website and log in with your IBM ID.
2. Click **Register customer number** in the navigation pane and enter your IBM Cloud customer number in **Customer Number (include country code)**. Decide whether you want to register your customer number permanently and click **Submit**.

    The first IBM ID to register a customer number becomes the primary contact for that customer number. If you attempt to register a customer number that already has a primary contact, you're offered the option of sending a request. The request goes to the customer number's primary contact and asks for access. You are not given access until the primary contact responds to that request.
    {: note}

3. After IBM has registered the customer number or server, click **Software downloads** under **My entitled software** in the navigation pane.

4. Select a category and group.

5. Check the box next to the installation image you would like to download and click **Continue**.

6. Next, select the language feature that you want and click **Continue**.

7. Agree to the terms and conditions.

8. Click the **Click here to use HTTP** link to download the ISO image by using HTTP. You can also click the **Download now** button.

AIX installation DVDs are delivered as ISO image files, while other installation images are delivered as compressed _tar_ archives. In some cases, AIX ISO images are zipped and can be unzipped by using the [AIX Toolbox for Linux Application](https://www.ibm.com/support/pages/aix-toolbox-linux-applications-overview){: external}. After you download an ISO image, it is not necessary to burn a DVD to access the contents of the ISO image.
{: tip}

## Copying and installing your ISO image to an AIX virtual machine (VM)
{: #copying-installing-iso}

After you download an AIX installation DVD as an ISO image, you must copy the image to an existing AIX VM's file system. To copy the image, you must use Secure Copy Protocol (SCP). SCP is a protocol for securely transferring files between a local and a remote host or between two remote hosts.

1. Copy the ISO image to an existing AIX VM's file system by using the [`scp`](https://www.ibm.com/support/knowledgecenter/ST5Q4U_1.5.2/com.ibm.storwize.v7000.unified.152.doc/usgr_usng_scp.html){: new_window}{: external} command.

    The `scp` command does not work unless you are on a public network.
    {: important}

    ```text
    scp [Options][[User@]From_Host:]Source_File [[User@]To_Host:][Destination_File]
    ```

2. Run the [`loopmount`](https://www.ibm.com/support/knowledgecenter/en/ssw_aix_72/l_commands/loopmount.html){: new_window}{: external} command to make the ISO image available as a file system by using the loopback device.

    ```text
    loopmount {-i imagefile | -l device}[-o mount options -m mountpoint]
    ```

3. Use the [`installp`](https://www.ibm.com/support/knowledgecenter/ssw_aix_72/i_commands/installp.html){: new_window}{: external} command to install the image in a compatible installation package. The following command and flags are most commonly used during installations, `installp -agXd path software_to_install`.

4. Upon the completion of the installation, the system generates an installation summary. Verify that the **Result** column shows success for all of the loaded files. You can also verify the installation's success by typing, `lslpp -aL`, at a command line.

## Installing optional software products from the AIX stock image
{: installing-aix-stock-image} 

The AIX stock images have a local repository that contains all available packages for the current level of the operating system. Any software that is not automatically installed is considered as optional and is included with the operating system in a separate file system starting with the 7100-05-05 or newer images `/usr/sys/inst.images`. By creating a separate file system, the local repository prevents the expansion of `/usr` file system. In addition, the separate file system can be safely removed if you want to reclaim the additional space used by the local repository.

The optional software products found under the `/usr/sys/inst.images` file system can be installed by using either command-line or SMIT menu options. For more information on installation options, visit the [installp](https://www.ibm.com/support/knowledgecenter/ssw_aix_72/i_commands/installp.html){: new_window}{: external} command guide.

### Examples:
{: example}

- To list all the software products and installable filesets in the `/usr/sys/inst.images` file system, enter the following command:

```text
 installp -L -d /usr/sys/inst.images
```

- To install and commit all software within the Geographic Logical Volume Manager software package (located in the `/usr/sys/inst.images` directory) and expand the file systems if necessary, enter the following command:

```text
 installp -acXd /usr/sys/inst.images glvm.*
```

- To preview the installation of the bos.sysmgt.nim.master fileset (located in the `/usr/sys/inst.images` directory) and all requisite software, enter the following command:

```text
 installp -pagXd /usr/sys/inst.images bos.sysmgt.nim.master
```

- To install software by using the SMIT interface, enter the following command:

```text
 smit install
```
