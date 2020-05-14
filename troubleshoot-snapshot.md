---

copyright:
  years: 2019, 2020

lastupdated: "2020-04-17"

keywords: snapshot, restore, clone, troubleshoot

subcollection: power-iaas

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}

# Troubleshooting snapshot, clone and restore issues
{: #troubleshoot-iaas-snapshot}

Learn how to troubleshoot {{site.data.keyword.powerSysShort}} snapshot, clone and restore issues.
{: shortdesc}

## The PVIDs of both of my volumes are the same on my AIX operating system. How do I resolve this issue?
{: #troubleshoot-clone}
{: troubleshoot}

{: tsSymptoms}
When you clone and attach a volume to the same PVM as the PVM containing the original volume, the PVIDs of both volumes are found to be the same on your AIX operating system.

{: tsCauses}
There's a problem with the underlying technology that is supporting the clone feature.

{: tsResolve}
To resolve this issue, enter the following commands:

1. `chdev -a pv=clear -l hdisk2`
2. `recreatevg -y copyvg hdisk2`
3. `mount /fs/<original-mount-point>`

In this example, `hdisk2` refers to the cloned volume name and `copyvg` is the name to be given to the newly created volume group. The `recreatevg` command creates a new file system with the same name as the original but in the `/fs` path. For more information, see "Section B" under [Possible Cause and Solution 2: The Disks Are Copies of Each Other](https://www.ibm.com/support/pages/resolving-lvm-and-hard-disk-pvid-issues){: new_window}{: external}.
