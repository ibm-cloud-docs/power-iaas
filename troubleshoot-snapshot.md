---

copyright:
  years: 2019, 2026

lastupdated: "2026-10-14"

keywords: snapshot, restore, clone, troubleshoot

subcollection: power-iaas

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Troubleshooting snapshot, clone and restore issues
{: #troubleshoot-iaas-snapshot}

---



{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}


---

Learn how to troubleshoot {{site.data.keyword.powerSysShort}} snapshot, clone and restore issues.
{: shortdesc}

## How do I resolve the issue where both volumes in my AIX operating system have the same PVID?
{: #troubleshoot-clone}
{: troubleshoot}

When you clone and attach a volume to the same PVM as the PVM containing the original volume, the PVIDs of both volumes are found to be the same on your AIX operating system.
{: tsSymptoms}

There is a problem with the underlying technology that supports the clone feature.
{: tsCauses}

To resolve this issue, run the following commands:
{: tsResolve}

1. `chdev -a pv=clear -l hdisk2`
2. `recreatevg -y copyvg hdisk2`
3. `mount /fs/<original-mount-point>`

In this example, `hdisk2` refers to the cloned volume name and `copyvg` is the name to be given to the newly created volume group. The `recreatevg` command creates a new file system with the same name as the original but in the `/fs` path. For more information, see "Section B" under [Possible Cause and Solution 2: The Disks Are Copies of Each Other](https://www.ibm.com/support/pages/resolving-lvm-and-hard-disk-pvid-issues){: external}.
