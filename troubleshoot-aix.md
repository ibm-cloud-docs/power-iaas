---

copyright:
  years: 2019

lastupdated: "2019-11-05"

keywords: troubleshooting, hung virtual machine, support, help, system management services, SMS

subcollection: power-iaas

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:new_window: target="_blank"}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:external: target="_blank" .external}

# Troubleshooting AIX-related issues
{: #troubleshoot-iaas-aix}

Learn how to troubleshoot {{site.data.keyword.powerSysShort}} AIX-related issues.
{: shortdesc}

## What can I do if my AIX virtual machine (VM) does not initially boot?
{: #troubleshoot-hung-aix}
{: troubleshoot}

The AIX boot disk being used to provision an AIX VM is not successfully booting. As a result, the console displays a blank screen without standard debugging options.
{: tsSymptoms}

If the AIX VM does not boot, you must provision an additional AIX VM and use it as a Network Installation Management (NIM) server. Without a NIM server, you cannot debug the boot issue and must re-image your disk. For information on setting up a NIM server, see [Setting up NIM to boot into maintenance mode](https://www.ibm.com/support/pages/setting-nim-boot-maintenance-mode){: new_window}{: external}. If you are unfamiliar with this process, create a [new support case](/docs/infrastructure/power-iaas?topic=power-iaas-getting-help-and-support).
{: tsResolve}
