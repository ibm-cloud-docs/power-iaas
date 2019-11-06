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

# Troubleshooting AIX-related issues
{: #troubleshoot-iaas-aix}

Learn how to troubleshoot {{site.data.keyword.powerSysShort}} AIX-related issues.
{: shortdesc}

## What can I do if my AIX virtual machine (VM) does not initially boot?
{: #troubleshoot-hung-aix}
{: troubleshoot}

If the AIX VM does not boot, the {{site.data.keyword.cloud}} Console does not display the LEDs. You must boot the AIX VM into **Maintenance Mode** to debug the boot issue.
{: tsSymptoms}

1. Start the console to the AIX VM from the Novalink host. The AIX VM must be powered on.

2. Restart the AIX VM from a **different** SSH session to the Novalink host.

3. Press **CTL+C** from the console on the first session. This should force the AIX VM to boot to System Management Services (SMS).
{: tsResolve}
