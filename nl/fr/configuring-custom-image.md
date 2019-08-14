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

# Configuration d'une image personnalisée avec une instance Power Systems Virtual Server
{: #configuring-custom-image}

Vous pouvez apporter votre propre image de système d'exploitation AIX ou IBM i personnalisée pour déployer une instance {{site.data.keyword.powerSysFull}}.
{:shortdesc}

Vous ne pouvez pas transférer une licence de système d'exploitation d'un système local à une instance {{site.data.keyword.powerSys_notm}} qui s'exécute dans un environnement de cloud. Le coût de la licence est pris en compte dans le taux de facturation horaire global.
{: note}

## Avant de commencer
{: #cci-before-you-begin}

Pour pouvoir utiliser une image personnalisée en tant que volume d'initialisation, consultez les informations suivantes :

* Vous devez vérifier que le niveau de technologie du système d'exploitation AIX ou IBM i est pris en charge sur le matériel Power Systems que vous avez sélectionné dans la zone **Type machine**. Pour afficher la liste des niveaux de technologie pour les systèmes d'exploitation AIX et IBM i et le matériel Power System pris en charge, voir [System software maps ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://www-01.ibm.com/support/docview.wss?uid=ssm1maps).
* Vous devez avoir des connaissances de base des concepts d'**IBM Cloud Object Storage**. Pour plus d'informations, voir [A propos d'IBM Cloud Object Storage](/docs/services/cloud-object-storage?topic=cloud-object-storage-about-ibm-cloud-object-storage).
* Si vous n'avez pas d'image AIX ou IBM i existante à disposition, vous pouvez utiliser IBM® PowerVC™ pour capturer et exporter une image à utiliser avec {{site.data.keyword.powerSys_notm}}. Pour plus d'informations, voir [Capture d'une machine virtuelle ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/support/knowledgecenter/en/SSXK2N_1.4.2/com.ibm.powervc.standard.help.doc/powervc_capturing_hmc.html){: new_window} et [Exportation d'images ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/support/knowledgecenter/en/SSXK2N_1.4.2/com.ibm.powervc.standard.help.doc/powervc_export_image_hmc.html){: new_window}.

## Téléchargement d'une image personnalisée sous forme d'objet
{: #cci-uploading}

1. Créez un objet IBM Cloud Storage et téléchargez votre image. Pour plus d'informations, voir [Téléchargement de données](/docs/services/cloud-object-storage?topic=cloud-object-storage-upload).
2. Générez une valeur confidentielle (secret) et des clés d'accès avec HMAC (Hash-based Message Authentication Code). Vous pouvez générer ces clés lorsque vous créez les données d'identification du service pour l'objet IBM Cloud Storage. Pour créer les données d'identification du service, vous devez disposer de l'accès `Writer` pour le compartiment **Object Storage**. Pour plus d'informations, voir [Données d'identification pour le service](/docs/services/cloud-object-storage?topic=cloud-object-storage-service-credentials) et [Droits des compartiments](/docs/services/cloud-object-storage?topic=cloud-object-storage-iam-bucket-permissions).
3. Dans le [catalogue IBM Cloud ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/catalog){: new_window}, cliquez sur la vignette Power Virtual Server pour ajouter l'image. Si vous avez déjà créé l'instance de serveur virtuel, sélectionnez l'**icône Menu ![Icône Menu](../icons/icon_hamburger.svg "Icône Menu") > Liste de ressources > Périphériques** et sélectionnez votre serveur virtuel.

 Renseignez les zones suivantes pour créer votre instance {{site.data.keyword.powerSys_notm}} et cliquez sur **Image AIX personnalisée** ou **Image IBM i personnalisée**.

| Zone | Description |
| ------| ------------|
| Nom de compartiment Cloud Object Storage | Pour identifier le nom de votre compartiment, sélectionnez l'**icône Menu ![Icône Menu](../icons/icon_hamburger.svg "Icône Menu") > Liste de ressources > Stockage > Nom de l'objet Cloud Storage > Compartiments**. |
| Clé d'accès Cloud Object Storage | Pour identifier votre clé d'accès, sélectionnez l'**icône Menu ![Icône Menu](../icons/icon_hamburger.svg "Icône Menu") > Liste de ressources > Stockage > Nom de l'objet Cloud Storage > Données d'identification du service > Afficher les données d'identification**. Copiez la valeur de `access_key_id` et collez-la dans cette zone. |
| Clé secrète Cloud Object Storage | Pour identifier votre clé secrète, sélectionnez l'**icône Menu ![Icône Menu](../icons/icon_hamburger.svg "Icône Menu") > Liste de ressources > Stockage > Nom de l'objet Cloud Storage > Données d'identification du service > Afficher les données d'identification**. Copiez la valeur de `secret_access_key` et collez-la dans cette zone. |
| Chemin de l'image | Entrez le chemin d'accès complet au fichier de l'image. Ce chemin doit être au format `noeud_final/nom_compartiment/nom_fichier`. Vous devez utiliser le domaine du noeud final privé. Par exemple, `s3.private.us-east.cloud-object-storage.appdomain.cloud/power-iaasprod-images-bucket/Aix_7200-03-02-1846_cldrdy_112018.gz`. Vous pouvez identifier le domaine du noeud final, le nom du compartiment et le nom du fichier en sélectionnant l'**icône Menu ![Icône Menu](../icons/icon_hamburger.svg "Icône Menu") > Liste de ressources > Stockage > Cloud Object Storage**.
