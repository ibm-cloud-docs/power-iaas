---

copyright:
  years: 2019, 2020

lastupdated: "2020-03-09"

keywords: ibm i, network intsall server, PTFs

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
{:help: data-hd-content-type='help'}
{:support: data-reuse='support'}

# Setting up an IBM i network install server
{: #setting-install-server}

Before you can install or upgrade an IBM i system through the network, you must set up a network installation server. The network installation server contains images of the IBM i operating system, its internal code as well as licensed programs and PTFs. To share virtual optical images through a network, the network installation server must meet the following requirements:

**Requirements**

- The server must be able to share virtual optical images that use version 3 or later of the Network File System (NFS).
- A volume list (`VOLUME_LIST`) file that contains the list of images to be loaded in the virtual optical device must exist in the image catalog directory. The `VFYIMGCLG` command is used to create the volume list file from the image catalog containing the images that you want to share. The following is an example of the command, `VFYIMGCLG IMGCLG(PUBS) TYPE(*OTHER) NFSSHR(*YES)`.

The image catalog that is used must have an image catalog path name that is limited to 127 characters. Path name characters are limited to A-Z, a-z, 0-9, and / (slash). Each image file name is limited to 127 characters.
{: note}

- A volume list has the following characteristics:
    - Must be called `VOLUME_LIST`
    - Each line is either an image file name or a comment
    - ASCII format
    - All entries are ended by the end of a line
    - All characters following the number sign '#' are considered comments until the end of the line
    - Comments can be added after *#* and must be followed by a EOL character
    - Provides the order that the image files will be processed on the client system
    - File names are limited to 127 characters
    - Can be created with the **Verify Image Catalog Entry** (`VFYIMGCLG`) with the `NFSSHR(*YES)` parameter or manually by using an ASCII editor
    - No tabs or line feeds can be used in the path name

Changes to `VOLUME_LIST` file are not active until the next time the client device is varied off and on.
{: tip}

**Configuration**

To complete the configuration of an IBM i network installation server, see [Virtual optical storage using the Network File System](https://www.ibm.com/support/knowledgecenter/ssw_ibm_i_74/rzam4/rzam4virtualopstoragenfs.htm){: new_window}{: external} and [IBM i Network Install](http://www.redbooks.ibm.com/redpapers/pdfs/redp4937.pdf){: new_window}{: external}.