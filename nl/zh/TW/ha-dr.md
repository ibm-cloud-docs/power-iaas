---

copyright:
  years: 2019

lastupdated: "2019-07-29"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:important: .important}
{:tip: .tip}
{:note: .note}

# Power Systems Virtual Servers 中的高可用性及災難回復選項
{: #ha-dr}

如果發生硬體故障，{{site.data.keyword.powerSys_notm}} 實例會在不同的主機系統上重新啟動虛擬伺服器。這個處理程序會為 {{site.data.keyword.powerSys_notm}} 服務提供基本的高可用性 (HA) 功能。
{:shortdesc}

如果您想要更進階的 HA 或災難回復 (DR) 解決方案，可以在您的 {{site.data.keyword.powerSys_notm}} 環境中部署下列應用程式。

## PowerHA SystemMirror for AIX Standard Edition
{: #ha-dr-ha-standard}

購買 PowerHA SystemMirror for AIX Standard Edition 時可以使用每月訂閱模型。如需相關資訊，請參閱 [Standard Edition monthly pricing options ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/common/ssi/ShowDoc.wss?docURL=/common/ssi/rep_ca/8/897/ENUS219-288/index.html)。

購買軟體之後，您可以從 [IBM Entitled Systems Support (ESS) ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/eserver/ess) 下載。您可以在 {{site.data.keyword.powerSys_notm}} 環境中執行的虛擬伺服器上，安裝 PowerHA SystemMirror for AIX。如需安裝指示，請參閱 [Installing PowerHA SystemMirror ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/support/knowledgecenter/SSPHQG_7.2/install/ha_install.html)。

請檢閱下列資訊，以便在 {{site.data.keyword.powerSys_notm}} 環境中實作 PowerHA SystemMirror for AIX。

* 建立屬於 PowerHA SystemMirror 叢集一部分的虛擬伺服器時，必須從**主機代管規則**欄位選取**不同的伺服器**。
![顯示主機代管規則欄位](/images/hadr2.png "顯示主機代管規則欄位"){: caption="圖 1. 在不同的伺服器上建立虛擬伺服器" caption-side="bottom"}

* 在為屬於 PowerHA SystemMirror 叢集一部分的虛擬伺服器建立儲存空間磁區（磁碟）時，必須從**可共用**欄位選取**開啟**。
![顯示可共用規則欄位](/images/hadr1.png "顯示可共用欄位"){: caption="圖 2. 建立可共用的儲存空間磁區" caption-side="bottom"}

* 藉由使用 {{site.data.keyword.powerSys_notm}} 服務，您不會具有 HMC、VIOS 及主機系統的存取權。因此，無法使用需要存取這些功能的任何 PowerHA SystemMirror 功能，例如資源最佳化高可用性 (ROHA) 和作用中節點中止原則 (ANHP)。

<!--* When you deploy PowerHA SystemMirror, you must verify that the Service IP address is defined as a private IP address. This Service IP address can be accessed by another {{site.data.keyword.powerSys_notm}} instance or from other {{site.data.keyword.cloud}} applications. You cannot use a public IP address because it cannot be moved from one interface to another interface within a virtual server or across different virtual servers. -->

<!--When you deploy PowerHA SystemMirror for AIX Enterprise Edition clusters in the {{site.data.keyword.powerSys_notm}} environment, you can only use the Geographic Logical Volume Manager (GLVM) functions. You cannot use storage mirroring functions that are part of PowerHA SystemMirror for AIX Enterprise Edition because you do not have access to the subsystem storage in the {{site.data.keyword.powerSys_notm}} environment. For more information, see [Geographic Logical Volume Manager ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SSPHQG_7.2/glvm/ha_glvm_kick.html).
{:note}
[Enterprise Edition monthly pricing options ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/common/ssi/cgi-bin/ssialias?infotype=AN&subtype=CA&htmlfid=897/ENUS219-286) -->

## 透過備份及還原達到營運持續
{: #ha-dr-ha-business}

您的 {{site.data.keyword.powerSys_notm}} 配置及資料不會由 {{site.data.keyword.cloud}} 備份。

您可以使用 {{site.data.keyword.cloud_notm}} 使用者介面，將虛擬伺服器備份到 {{site.data.keyword.cloud_notm}} Object Storage。使用此處理程序，便可在發生重要失敗時還原虛擬伺服器。如需相關資訊，請參閱 [Cloud Object Storage ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](/docs/services/cloud-object-storage?topic=cloud-object-storage-getting-started)。
