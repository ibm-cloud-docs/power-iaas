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

# Optionen für Hochverfügbarkeit und Disaster-Recovery in Power Systems Virtual Servers
{: #ha-dr}

Die {{site.data.keyword.powerSys_notm}}-Instanz startet die virtuellen Server auf einem anderen Hostsystem erneut, wenn ein Hardwarefehler auftritt. Dieser Prozess stellt grundlegende Leistungsmerkmale der Hochverfügbarkeit (HA) für den {{site.data.keyword.powerSys_notm}}-Service bereit.
{:shortdesc}

Wenn Sie professionellere Lösungen für HA oder Disaster Recovery (DR) wünschen, können Sie die folgenden Anwendungen in Ihrer {{site.data.keyword.powerSys_notm}}-Umgebung bereitstellen. 

## PowerHA SystemMirror for AIX Standard Edition
{: #ha-dr-ha-standard}

Sie können ein monatliches Abonnementmodell nutzen, wenn Sie PowerHA SystemMirror for AIX Standard Edition kaufen. Weitere Informationen finden Sie unter [Standard Edition monthly pricing options ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/common/ssi/ShowDoc.wss?docURL=/common/ssi/rep_ca/8/897/ENUS219-288/index.html).

Nachdem Sie die Software gekauft haben, können Sie sie von [IBM Entitled Systems Support (ESS) ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](http://www.ibm.com/eserver/ess) herunterladen. Sie können PowerHA SystemMirror für AIX auf dem virtuellen Server installieren, der in Ihrer {{site.data.keyword.powerSys_notm}}-Umgebung ausgeführt wird. Installationsanweisungen finden Sie unter [Installing PowerHA SystemMirror ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/support/knowledgecenter/SSPHQG_7.2/install/ha_install.html).

Lesen Sie die folgenden Informationen für die Bereitstellung von PowerHA SystemMirror for AIX in Ihrer {{site.data.keyword.powerSys_notm}}-Umgebung. 

* Wenn Sie die virtuellen Server erstellen, die Teil des PowerHA SystemMirror-Clusters sind, müssen Sie **Anderer Server** im Feld **Zusammenstellungsregeln** auswählen. ![Feld 'Zusammenstellungsregeln'](/images/hadr2.png "Feld 'Zusammenstellungsregeln'")

* Wenn Sie Datenträger (Platten) für die virtuellen Server erstellen, die Teil des PowerHA SystemMirror-Clusters sind, müssen Sie im Feld **Gemeinsam nutzbar** die Option **Ein** auswählen. ![Feld 'Gemeinsam nutzbare Regeln'](/images/hadr1.png "Feld 'Gemeinsam nutzbar'")

* Durch die Verwendung des {{site.data.keyword.powerSys_notm}}-Service haben Sie keinen Zugriff auf HMC, VIOS und das Hostsystem. Daher sind alle Funktionen von PowerHA SystemMirror, die Zugriff auf diese Funktionalitäten erfordern, wie beispielsweise Resource Optimized High Availability (ROHA) und Active Node Halt Policy (ANHP) nicht verfügbar. 

<!--* When you deploy PowerHA SystemMirror, you must verify that the Service IP address is defined as a private IP address. This Service IP address can be accessed by another {{site.data.keyword.powerSys_notm}} instance or from other {{site.data.keyword.cloud}} applications. You cannot use a public IP address because it cannot be moved from one interface to another interface within a virtual server or across different virtual servers. -->

<!--When you deploy PowerHA SystemMirror for AIX Enterprise Edition clusters in the {{site.data.keyword.powerSys_notm}} environment, you can only use the Geographic Logical Volume Manager (GLVM) functions. You cannot use storage mirroring functions that are part of PowerHA SystemMirror for AIX Enterprise Edition because you do not have access to the subsystem storage in the {{site.data.keyword.powerSys_notm}} environment. For more information, see [Geographic Logical Volume Manager ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SSPHQG_7.2/glvm/ha_glvm_kick.html).
{:note}
[Enterprise Edition monthly pricing options ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/common/ssi/cgi-bin/ssialias?infotype=AN&subtype=CA&htmlfid=897/ENUS219-286) -->

## Business Continuity über Sicherung und Wiederherstellung
{: #ha-dr-ha-business}

Für Ihre {{site.data.keyword.powerSys_notm}}-Konfiguration und -Daten erstellt {{site.data.keyword.cloud}} keine Sicherungskopie. 

Sie können die Benutzerschnittstelle von {{site.data.keyword.cloud_notm}} verwenden, um ein Backup für Ihren virtuellen Server auf {{site.data.keyword.cloud_notm}} Object Storage zu erstellen. Sie können dieses Backup verwenden, um Ihren virtuellen Server im Fall eines kritischen Ausfalls wieder herzustellen. Weitere Informationen finden Sie unter [Cloud Object Storage ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](/docs/services/cloud-object-storage?topic=cloud-object-storage-getting-started).
