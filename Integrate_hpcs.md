---

copyright:
  years: 2022, 2023

lastupdated: "2023-05-22"

keywords: Hyper Protect Crypto Services for Power VS, HPCS Power VS, AIX HPCS, LINUX HPCS, Configure HPCS

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Integrating {{site.data.keyword.powerSys_notm}} with IBM Cloud Key Management Services
{: #integrate-hpcs}

[On-premises]{: tag-red}To integrate {{site.data.keyword.powerSysFull}} with IBM Cloud key management services, establish a connection from your virtual machine to IBM Cloud.
{: note}

IBM provides two Cloud key management services that integrate with {{site.data.keyword.powerSys_notm}} workloads:
{: shortdesc}

1. [IBM Cloud® Hyper Protect Crypto Services (HPCS)](/docs/hs-crypto?topic=hs-crypto-overview) is a dedicated key management service and hardware security module (HSM) based on IBM Cloud. You can integrate HPCS with {{site.data.keyword.powerSys_notm}} to securely store and protect encryption key information for AIX and Linux.
2. [IBM {{site.data.keyword.keymanagementserviceshort}}](/docs/key-protect?topic=key-protect-about) is a full-service multi-tenant encryption solution that allows data to be secured and stored in IBM Cloud™ using the latest envelope encryption techniques. You can integrate {{site.data.keyword.keymanagementserviceshort}} with {{site.data.keyword.powerSys_notm}} to securely store and protect encryption key information for AIX and Linux.

## Using Hyper Protect Crypto Services (HPCS) and {{site.data.keyword.keymanagementserviceshort}} for AIX
{: #AIX-hpcs}

HPCS and {{site.data.keyword.keymanagementserviceshort}} are supported by AIX 7.3 TL1 for AIX logical volume encryption.
{: note}

Power-AIX integration for PKCS11 / TDE integration for Oracle/DB2 workloads is not available at this time. There is no impact to the volume-level encryption for AIX, Power-Linux with HPCS.
{: important}

You can use {{site.data.keyword.powerSys_notm}} to integrate with HPCS and {{site.data.keyword.keymanagementserviceshort}} to leverage for encryption of AIX file systems with `keysvrmgr` and `hdcryptmgr` command.

The `keysvrmgr` command manages the Object Data Manager (ODM) database entries that are associated with the encryption key server when the logical or physical volume uses the key server key-protection method for encryption. For more information, see [keysvrmgr Command](https://www.ibm.com/docs/en/aix/7.3?topic=k-keysvrmgr-command){: external}.

The `hdcryptmgr` command helps to manage the cryptographic management of logical volumes (LV) and physical volumes (PV). For more information, see [hdcryptmgr Command](https://www.ibm.com/docs/en/aix/7.3?topic=h-hdcryptmgr-command){: external}.

## Using Hyper Protect Crypto Services (HPCS) or Key Protect for Linux
{: #Linux-hpcs}

You can use {{site.data.keyword.powerSys_notm}} to integrate with HPCS or {{site.data.keyword.keymanagementserviceshort}} to protect Linux Unified Key Setup (LUKS) encryption keys from being compromised. Either key management service can act as the single point of control to enable or disable access to data across the enterprise. This is done by successively wrapping encryption keys, with the ultimate control being a master key that resides in a hardware security module (HSM).

For more information, see [Protect LUKS encryption keys with IBM Cloud Hyper Protect Crypto Services and {{site.data.keyword.keymanagementserviceshort}}](https://developer.ibm.com/tutorials/protect-luks-encryption-keys-with-ibm-cloud-hyper-protect-crypto-services/){: external}.

## Additional support for configuring Hyper Protect Crypto Services or {{site.data.keyword.keymanagementserviceshort}}
{: #support-hpcs}

For any additional information and assistance on HPCS or {{site.data.keyword.keymanagementserviceshort}} for AIX or Linux, [contact IBM](mailto:zaas.client.acceleration@ibm.com).
