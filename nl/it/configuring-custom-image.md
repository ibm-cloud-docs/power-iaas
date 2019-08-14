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

# Configurazione di un'immagine personalizzata con un Power Systems Virtual Server
{: #configuring-custom-image}

Puoi utilizzare la tua immagine di sistema operativo AIX o IBM i personalizzata per distribuire un {{site.data.keyword.powerSysFull}}.
{:shortdesc}

Non puoi trasferire una licenza di sistema operativo da un sistema in loco a un {{site.data.keyword.powerSys_notm}} in esecuzione nell'ambiente cloud. Il costo della licenza è incluso nella frequenza di fatturazione oraria generale.
{: note}

## Prima di cominciare 
{: #cci-before-you-begin}

Prima di poter utilizzare un'immagine personalizzata come volume di avvio, controlla le seguenti informazioni:

* Devi verificare che il livello di tecnologia del sistema operativo AIX o IBM i sia supportato sull'hardware Power Systems che selezioni nel campo **Machine Type**. Per visualizzare l'elenco di livelli di tecnologia del sistema operativo AIX e IBM i supportati e l'hardware Power System, vedi [System software maps ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www-01.ibm.com/support/docview.wss?uid=ssm1maps).
* Devi avere una conoscenza di base dei concetti di **IBM Cloud Object Storage**. Per ulteriori informazioni, vedi [Informazioni su IBM Cloud Object Storage](/docs/services/cloud-object-storage?topic=cloud-object-storage-about-ibm-cloud-object-storage).
* Se non disponi di un'immagine AIX o IBM i esistente, puoi utilizzare IBM® PowerVC™ per acquisire ed esportare un'immagine da utilizzare con un {{site.data.keyword.powerSys_notm}}. Per ulteriori informazioni, vedi [Capturing a virtual machine ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/support/knowledgecenter/en/SSXK2N_1.4.2/com.ibm.powervc.standard.help.doc/powervc_capturing_hmc.html){: new_window} e [Exporting images ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/support/knowledgecenter/en/SSXK2N_1.4.2/com.ibm.powervc.standard.help.doc/powervc_export_image_hmc.html){: new_window}.

## Caricamento di un'immagine personalizzata come un oggetto
{: #cci-uploading}

1. Crea un oggetto IBM Cloud Storage e carica la tua immagine. Per ulteriori informazioni, vedi [Carica i dati](/docs/services/cloud-object-storage?topic=cloud-object-storage-upload).
2. Genera le chiavi di accesso e segreto con HMAC (hash-based message authentication code). Puoi generare queste chiavi quando crei le credenziali del servizio per l'oggetto IBM Cloud Storage. Per creare le credenziali del servizio, devi avere l'accesso come `Writer` per il bucket **Object Storage**. Per ulteriori informazioni, vedi [Credenziali del servizio](/docs/services/cloud-object-storage?topic=cloud-object-storage-service-credentials) e [Autorizzazioni bucket](/docs/services/cloud-object-storage?topic=cloud-object-storage-iam-bucket-permissions).
3. Dal [Catalogo IBM Cloud ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/catalog){: new_window}, fai clic sul tile Power Virtual Server per aggiungere l'immagine. Se hai già creato l'istanza del server virtuale, seleziona **Menu icon ![icona Menu](../icons/icon_hamburger.svg "icona Menu") > Resource list > Devices** e seleziona il tuo server virtuale esistente.

 Completa i seguenti campi per creare il tuo {{site.data.keyword.powerSys_notm}} e fai clic su **Custom AIX image** o **Custom IBM i Image**.

|Campo| Descrizione |
| ------| ------------|
| Nome bucket Cloud Object Storage | Per identificare il tuo nome del bucket, seleziona **Menu icon ![icona Menu](../icons/icon_hamburger.svg "icona Menu") > Resource list > Storage > Cloud Storage Object name > Buckets**. |
| Chiave di accesso Cloud Object Storage | Per identificare la tua chiave di accesso, seleziona **Menu icon ![icona Menu](../icons/icon_hamburger.svg "icona Menu") > Resource list > Storage > Cloud Storage Object name > Service credentials > View credentials**. Copia il valore `access_key_id` e incollalo in questo campo. |
| Chiave del segreto Cloud Object Storage | Per identificare la tua chiave del segreto, seleziona **Menu icon ![icona Menu](../icons/icon_hamburger.svg "icona Menu") > Resource list > Storage > Cloud Storage Object name > Service credentials > View credentials**. Copia il valore `secret_access_key` e incollalo in questo campo. |
| Percorso immagine| Immetti il percorso completo per il file immagine. Il percorso completo deve essere in questo formato, `endpoint/bucket_name/file_name`. Devi utilizzare il dominio di endpoint privato. Ad esempio, `s3.private.us-east.cloud-object-storage.appdomain.cloud/power-iaasprod-images-bucket/Aix_7200-03-02-1846_cldrdy_112018.gz`. Puoi identificare il dominio di endpoint, il nome del bucket e il nome del file selezionando **Menu icon ![icona Menu](../icons/icon_hamburger.svg "icona Menu") > Resource list > Storage > Cloud Storage Object**.
