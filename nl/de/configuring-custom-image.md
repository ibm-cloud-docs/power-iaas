---

copyright:
  years: 2019

lastupdated: "2019-7-25"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}

# Angepasstes Image mit einem Power Systems Virtual Server konfigurieren
{: #configuring-custom-image}

Sie können Ihr eigenes angepasstes AIX- oder IBM i-Betriebssystemimage verwenden, um {{site.data.keyword.powerSysFull}} bereitzustellen.
{:shortdesc}

Sie können eine Betriebssystemlizenz nicht von einem On-Premises-System auf eine{{site.data.keyword.powerSys_notm}}-Instanz übertragen, die in der Cloudumgebung ausgeführt wird. Die Lizenzgebühr ist im Gesamtbetrag der Abrechnung enthalten.
{: note}

## Vorbereitende Schritte
{: #cci-before-you-begin}

Bevor Sie ein angepasstes Image als Bootdatenträger verwenden, prüfen Sie die folgenden Punkte: 

* Sie müssen überprüfen, dass das Technology Level des Betriebssystems AIX oder IBM i von der Power Systems-Hardware unterstützt wird, die Sie im Feld **Maschinentyp** ausgewählt haben. Eine Liste der unterstützten Technology Level der Betriebssysteme AIX- und IBM i und der Power System-Hardware finden Sie unter [Systemsoftwarezuordnungen![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://www-01.ibm.com/support/docview.wss?uid=ssm1maps).
* Sie müssen ein Grundverständnis des Konzepts von **IBM Cloud Object Storage** haben. Weitere Informationen finden Sie unter [Informationen zu IBM Cloud Object Storage](/docs/services/cloud-object-storage?topic=cloud-object-storage-about-ibm-cloud-object-storage).
* Wenn Sie nicht über ein AIX- oder IBM i-Image verfügen, können Sie IBM® PowerVC™ verwenden, um ein Image zu erfassen und zu exportieren, das mit {{site.data.keyword.powerSys_notm}} verwendet wird. Weitere Informationen finden Sie unter [Virtuelle Maschine erfassen![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/support/knowledgecenter/en/SSXK2N_1.4.2/com.ibm.powervc.standard.help.doc/powervc_capturing_hmc.html){: new_window} und [Images exportieren![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/support/knowledgecenter/en/SSXK2N_1.4.2/com.ibm.powervc.standard.help.doc/powervc_export_image_hmc.html){: new_window}.

## Angepasstes Image als Objekt hochladen
{: #cci-uploading}

1. Erstellen Sie ein IBM Cloud Storage-Objekt und laden Sie Ihr Image hoch. Weitere Informationen finden Sie unter [Daten hochladen](/docs/services/cloud-object-storage?topic=cloud-object-storage-upload).
2. Generieren Sie geheime Schlüssel und Zugriffsschlüssel mit HMAC (Hash-based Message Authentication Code). Sie können diese Schlüssel generieren, wenn Sie die Serviceberechtigungsnachweise für das IBM Cloud Storage-Objekt erstellen. Um die Serviceberechtigungsnachweise zu erstellen, müssen Sie über Schreibzugriff (`Writer`) für das Bucket **Object Storage** verfügen. Weitere Informationen finden Sie unter [Serviceberechtigungsnachweise](/docs/services/cloud-object-storage?topic=cloud-object-storage-service-credentials) und [Bucket-Berechtigungen](/docs/services/cloud-object-storage?topic=cloud-object-storage-iam-bucket-permissions).
3. Klicken Sie im [IBM Cloud-Katalog ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://cloud.ibm.com/catalog){: new_window} auf die Kachel 'Power Virtual Server', um das Image hinzuzufügen. Wenn Sie die virtuelle Serverinstanz bereits erstellt haben, wählen Sie **Menüsymbol ![Menüsymbol](../icons/icon_hamburger.svg "Menüsymbol") > Ressourcenliste > Geräte** aus und wählen Sie dann Ihren vorhanden virtuellen Server aus. 

 Füllen Sie die folgenden Felder aus, um Ihre {{site.data.keyword.powerSys_notm}}-Instanz zu erstellen und klicken Sie auf **AIX-Image anpassen** oder **IBM i-Image anpassen**.

| Feld  | Beschreibung|
| ------| ------------|
| Cloud Object Storage-Bucketname | Um Ihren Bucketnamen zu ermitteln, wählen Sie **Menüsymbol![Menüsymbol](../icons/icon_hamburger.svg "Menüsymbol") > Ressourcenliste > Speicher > Cloud Storage Object-Name > Buckets** aus. |
| Cloud Object Storage-Zugriffsschlüssel | Um Ihren Zugriffsschlüssel zu ermitteln, wählen Sie **Menüsymbol ![Menüsymbol](../icons/icon_hamburger.svg "Menüsymbol") > Ressourcenliste > Speicher > Cloud Storage Object-Name > Serviceberechtigungsnachweise > Berechtigungsnachweis anzeigen** aus. Kopieren Sie den Wert für `access_key_id` und fügen Sie ihn in dieses Feld ein. |
| Geheimer Cloud Object Storage-Schlüssel | Um Ihren geheimen Schlüssel zu ermitteln, wählen Sie **Menüsymbol ![Menüsymbol](../icons/icon_hamburger.svg "Menüsymbol") > Ressourcenliste > Speicher > Cloud Storage Object-Name > Serviceberechtigungsnachweise > Berechtigungsnachweise anzeigen** aus. Kopieren Sie den Wert für `secret_access_key` und fügen Sie ihn in dieses Feld ein. |
| Imagepfad | Geben Sie den vollständig qualifizierten Pfad für die Imagedatei ein. Der vollständig qualifizierte Pfad muss dieses Format aufweisen: `endpoint/bucket_name/file_name`. Sie müssen die private Endpunktdomäne verwenden. Zum Beispiel: `s3.private.us-east.cloud-object-storage.appdomain.cloud/power-iaasprod-images-bucket/Aix_7200-03-02-1846_cldrdy_112018.gz`. Sie können die Endpunktdomäne, den Bucketnamen und den Dateinamen ermitteln, indem Sie **Menüsymbol ![Menüsymbol](../icons/icon_hamburger.svg "Menüsymbol") > Ressourcenliste > Speicher > Cloud Storage Object** auswählen.
