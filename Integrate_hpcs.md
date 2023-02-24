---

copyright:
  years: 2022, 2023

lastupdated: "2023-02-24"

keywords: Hyper Protect Crypto Services for Power VS, HPCS Power VS, AIX HPCS, LINUX HPCS, Configure HPCS

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Integrating {{site.data.keyword.powerSys_notm}} with Hyper Protect Crypto Services
{: #integrate-hpcs}

[IBM Cloud® Hyper Protect Crypto Services](/docs/hs-crypto?topic=hs-crypto-overview) (HPCS) is a dedicated key management service and hardware security module (HSM) based on IBM Cloud. You can integrate HPCS with {{site.data.keyword.powerSys_notm}} to securely store and protect encryption key information for AIX and Linux.
{: shortdesc}

## Using Hyper Protect Crypto Services for AIX
{: #AIX-hpcs}

HPCS is supported with AIX 7.3 TL1 for AIX logical volume encryption.
{: note}

You can use {{site.data.keyword.powerSys_notm}} to integrate with HPCS to leverage for encryption of AIX file systems with `keysvrmgr` and `hdcryptmgr` command.

The `keysvrmgr` command manages the Object Data Manager (ODM) database entries that are associated with the encryption key server when the logical or physical volume uses the key server key-protection method for encryption. For more information, see [keysvrmgr Command](https://www.ibm.com/docs/en/aix/7.3?topic=k-keysvrmgr-command){: external}

The `hdcryptmgr` command helps to manage the cryptographic management of logical volumes (LV) and physical volumes (PV). For more information, see [hdcryptmgr Command](https://www.ibm.com/docs/en/aix/7.3?topic=h-hdcryptmgr-command){: external}

## Using Hyper Protect Crypto Services (HPCS) for Linux
{: #Linux-hpcs}

You can use {{site.data.keyword.powerSys_notm}} to integrate with HPCS to protect Linux Unified Key Setup (LUKS) encryption keys from being compromised. The HPCS acts as the single point of control to enable or disable access to data across the enterprise. The HPCS does this by successively wrapping encryption keys, with the ultimate control being a master key that resides in a hardware security module (HSM). 

For more information, see [Protect LUKS encryption keys with IBM Cloud Hyper Protect Crypto Services](https://developer.ibm.com/tutorials/protect-luks-encryption-keys-with-ibm-cloud-hyper-protect-crypto-services/){: external}

### HPCS for Linux virtual server instances
{: #Linux-vm-hpcs}

The {{site.data.keyword.powerSys_notm}} instances that runs on Linux operating system are integrated with IBM Cloud Key Protect service. For more information, see [Protect LUKS encryption keys with IBM Cloud Hyper Protect Crypto Services](https://developer.ibm.com/tutorials/protect-luks-encryption-keys-with-ibm-cloud-hyper-protect-crypto-services/){: external}

## Additional support for configuring Hyper Protect Crypto Services
{: #support-hpcs}

For any additional information and assistance using HPCS for AIX or Linux, [contact IBM](mailto:zaas.client.acceleration@ibm.com).

