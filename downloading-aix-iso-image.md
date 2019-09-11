---

copyright:
  years: 2019

lastupdated: "2019-09-11"

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

# Downloading ISO images of AIX installation media
{: downloading-aix-iso}

Entitled software means that the software is covered by a valid Software Maintenance Agreement (SWMA). If you obtain software maintenance by using a custom SWMA contract (as opposed to a standard SWMA), you might need to register on the [Entitled Software Support (ESS)](https://www.ibm.com/servers/eserver/ess/index.wss) website to access the custom SWMA contract. Without access to the customer SWMA contract, you might not be able to download ISO images. You cannot download all levels of entitled software. For example, you cannot download installation media for AIX technology levels that are outdated.
{: shortdesc}

The ESS customer number registration process can take several days.
{: important}

## Before you begin
{: before-you-begin}

Before you can download an ISO image of an AIX installation DVD, you must have an [IBM ID](https://www.ibm.com/account/reg/us-en/signup?formid=urx-19776) and the IBM customer number under which the software was ordered. You must also have one of the following items:

If you are missing any of the listed items, contact your IBM or Business Partner Power Systems sales representative with the machine type-model and serial number on which the software is licensed. If you are uncertain of the machine type-model of a server on which AIX is already running in your environment, enter the commands `lsconf` and `head` and look for the **System Model** and **Machine Serial Number** fields. Registering with a serial number provides access only to the entitled software download.
{: note}

* An IBM machine serial number on which the software is entitled
* IBM system number (from software packing list)
* IBM order number (from software packing list)
* Custom SWMA contract number

## Using the ESS website to download an ISO image
{: defining-aix-helper-vm}

1. Go to the [ESS](https://www.ibm.com/servers/eserver/ess/index.wss) website and log in with your IBM ID.

1. Click **Register customer number** in the navigation pane and enter either **Hardware or Software serial number** or **Customer Number (include country code)**. Decide whether you want to register your customer number permanently and click **Submit**.

The first IBM ID to register a customer number becomes the primary contact for that customer number. If you attempt to register a customer number that already has a primary contact, you're offered the option of sending a request. The request goes to the customer number's primary contact and asks for access. You are not given access until the primary contact responds to that request.
{: note}

1. After IBM has registered the customer number or server, click **Software downloads** under **My entitled software** in the navigation pane.

1. Select a category and group.

1. Check the box next to the installation image you would like to download and click **Continue**.

1. Next, select the language feature that you want and click **Continue**. Agree to the terms and conditions.

1. Click the **Click here to use HTTP** link to download the ISO image by using HTTP. You can also click the **Download now** button.

AIX installation DVDs are delivered as ISO image files, while other installation images are delivered as compressed _tar_ archives. In some cases, AIX ISO images are zipped and can be unzipped by using the [AIX Toolbox for Linux&trade Application](https://www.ibm.com/support/pages/aix-toolbox-linux-applications-overview). After you download an ISO image, it is not necessary to burn a DVD to access the contents of the ISO image.
{: note}

## Copying your ISO image to an AIX virtual machine (VM)
