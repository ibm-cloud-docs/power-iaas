---

copyright:
  years: 2019

lastupdated: "2019-06-17"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:download: .download}


# Commande d'IBM Cloud Direct Link Connect pour Power Systems Virtual Servers
{: #ordering-direct-link-connect}

Une des options de configuration d'un réseau privé avec {{site.data.keyword.powerSys_notm}} consiste à utiliser le service Direct Link Connect. Le service Direct Link Connect crée une connexion qui permet d'accéder aux ressources {{site.data.keyword.cloud}} à partir de votre instance {{site.data.keyword.powerSys_notm}}. Le service Direct Link Connect est également utilisé pour connecter votre réseau sur site au dispositif de routeur virtuel (VRA) d'IBM Cloud.

Vous pouvez utiliser la console de l'interface utilisateur {{site.data.keyword.cloud_notm}} pour commander le service Direct Link Connect. Pour se connecter à votre environnement {{site.data.keyword.powerSys_notm}}, vous désirez commander deux connexions Direct Link Connect. Direct Link Connect est un service distinct du service {{site.data.keyword.powerSys_notm}}. Pour consulter les frais liés à Direct Link Connect, voir [Tarification d'IBM Cloud Direct Link](/docs/infrastructure/direct-link?topic=direct-link-pricing-for-direct-link-connect){: new_window}.

## Avant de commencer
{: #before-direct-link-connect}

* Vérifiez que votre compte {{site.data.keyword.cloud}} dispose des autorisations appropriées pour commander le service Direct Link Connect.
* Familiarisez-vous avec les concepts réseau de base du service Direct Link Connect en consultant les rubriques suivantes :
  * [Concepts Direct Link Connect](/docs/infrastructure/direct-link?topic=direct-link-direct-link-connect-solution#direct-link-connect-solution)
  * [Détails de Direct Link Connect](/docs/infrastructure/direct-link?topic=direct-link-ibm-cloud-direct-link-connect-details)
  * [Limitations de Direct Link Connect](/docs/infrastructure/direct-link?topic=direct-link-known-limitations#ibm-cloud-direct-link-exchange-and-direct-link-connect-limitations)
  * [Limitations strictes pour les affectations d'adresse IP](/docs/infrastructure/direct-link?topic=direct-link-configure-ibm-cloud-direct-link#strict-limitations-on-ip-assignments)

## Commande de Direct Link Connect
{: #steps-to-order-direct-link-connect}

Pour commander le service Direct Link Connect qui crée une connexion à l'instance {{site.data.keyword.powerSys_notm}}, procédez comme suit :

1. Connectez-vous au [catalogue d'IBM Cloud ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/catalog){: new_window} avec vos informations d'authentification au compte IBM Cloud. Votre compte doit disposer des autorisations appropriées pour commander le service Direct Link Connect.

1. Dans la section **Mise en réseau**, cliquez sur la vignette **Direct Link Connect**.
![Affichage de la vignette de catalogue Direct Link](/images/directlink1.png "Affichage de la vignette de catalogue Direct Link")

1. Dans l'entrée de catalogue Direct Link Connect, cliquez sur **Créer**.

1. Sur la page IBM Cloud Direct Link, cliquez sur **Commander Direct Link Connect**.

1. Sur la page de création de la connexion IBM Cloud Direct Link Connect, complétez les zones suivantes. 

   Lorsque vous complétez les zones suivantes pour la création du service Direct Link Connect, le tarif est automatiquement mis à jour pour refléter vos sélections.
   {:note}

   <dl>
   <dt><strong>Direct Link Instance Name</strong><dt>
   <dd>Entrez un nom caractéristique de l'objectif de Direct Link Connect.</dd>
   <dt><strong>Location</strong><dt>
   <dd>Sélectionnez le même emplacement que l'instance {{site.data.keyword.powerSys_notm}}. Le tableau suivant identifie l'emplacement de l'instance {{site.data.keyword.powerSys_notm}} et l'option de connexion Direct Link Connect correspondante :
   <table>
   <caption>Tableau 1. Options d'emplacement de Direct Link Connect</caption>
   <tr>
   <th>Emplacement de Power Systems Virtual Server</th>
   <th>Emplacement de Direct Link Connect</th>
   </tr>
   <tr>
   <td>Dallas, TX US</td>
   <td>Dallas 4</td>
   </tr>
   <tr>
   <td>Washington D.C, US</td>
   <td>Washington 2</td>
   </tr>
   </table>
   </dd>
   <dt><strong>Network Provider</strong><dt>
   <dd>Vous devez sélectionner <strong>MEGAPORT</strong> dans la liste.</dd>
   <dt><strong>Link Speed</strong><dt>
   <dd>Sélectionnez la vitesse de liaison répondant aux exigences liées à vos charges de travail. La sélection recommandée pour cette zone est 1000 Mbps.</dd>
   <dt><strong>Routing Option</strong><dt>
   <dd>Sélectionnez <b>Local Routing (Free)</b> pour accéder à tous les centres de données connectés à l'emplacement que vous avez indiqué dans la zone <b>Location</b>. Sélectionnez <b>Global Routing</b> pour accéder à tous les centres de données IBM Cloud dans le monde entier. </dd>
   <dt><strong>BGP ASN</strong><dt>
   <dd>Vous devez entrer le numéro BGP ASN correspondant à l'emplacement spécifique de Direct Link Connect dans le tableau suivant.
   <table>
   <caption>Tableau 2. Numéro BGP ASN correspondant à des emplacements spécifiques</caption>
   <tr>
   <th>Emplacement de Direct Link Connect</th>
   <th>Numéro BGP ASN</th>
   </tr>
   <tr>
   <td>Dallas 4</td>
   <td>64997</td>
   </tr>
   <tr>
   <td>Washington 2</td>
   <td>64999</td>
   </tr>
   </table>
   </dd>
   <dt><strong>Select VRF</strong><dt>
   <dd>Sélectionnez l'option de routage et de transfert virtuel (VRF) pour la connexion. Si cette option n'est pas identifiée dans votre compte, cette zone n'est pas affichée. Vous pouvez toujours créer le service Direct Link Connect sans sélectionner d'option VRF.</dd>
   <dd>
   La figure suivante est un exemple de zones de Direct Link Connect.
   ![Affichage des zones de Direct Link Connect renseignées](/images/directlink2.png "Affichage des zones de Direct Link Connect renseignées")
   </dd>
   </dl>
1. Lisez le contrat principal de services (MSA) et sélectionnez la case à cocher. Vous devez lire ce contrat car il contient des informations techniques importantes que vous devez connaître avant de continuer.

1. Cliquez sur **Create**. Le message suivant s'affiche lorsque la soumission de votre demande a abouti.
![Affichage du message de soumission réussie pour Direct Link Connect](/images/directlink3.png "Affichage du message de soumission réussie pour Direct Link Connect")

1. Cliquez sur le lien du numéro de cas correspondant au service Direct Link Connect. Les informations contenues dans le numéro de cas sont utilisées pour identifier les informations relatives à Direct Link Connect à utiliser pour connecter votre instance {{site.data.keyword.powerSys_notm}}.

  L'équipe de support IBM peut nécessiter jusqu'à trois jours ouvrables pour créer la connexion Direct Link Connect.
  {: note}

1. Ouvrez un nouveau cas pour que l'équipe de support {{site.data.keyword.powerSys_notm}} crée une connexion à l'instance {{site.data.keyword.powerSys_notm}} en utilisant le service Direct Link Connect. Dans le cas {{site.data.keyword.powerSys_notm}}, indiquez le numéro de cas correspondant à Direct Link Connect. Le cas {{site.data.keyword.powerSys_notm}} est mis à jour avec un ID de service. Pour en savoir plus sur l'ouverture d'un cas, voir [Aide et support](/docs/infrastructure/power-iaas?topic=power-iaas-getting-help-and-support).

1. Entrez l'ID de service obtenu dans le numéro de cas {{site.data.keyword.powerSys_notm}} dans le numéro de cas Direct Link Connect. Lorsque la connexion à Direct Link Connect est créée, le numéro de cas Direct Link Connect est clôturé. Voici un exemple d'informations réseau affichées dans le cas :

  ```
  Link Speed:                  1000 Mbps
  Location:                    Washington 2
  Network Provider:            MEGAPORT
  IBM IP Address:              10.254.0.25/30
  Customer IP Address:         10.254.0.26/30
  Service Key:                 None
  BGP ASN:                     64999
  Network Identifier:          1748523-1
  Date Created:                2019-06-12T14:56:45-06:00
  ```
  {: screen}

1. Utilisez ces informations issues du numéro de cas Direct Link Connect et entrez les informations réseau suivantes dans le cas {{site.data.keyword.powerSys_notm}} :

  ```
  Customer name:
  Customer account ID:
  Direct Link Connect subnet:
  Power Systems Virtual Server network IP address:
  IBM Cloud IP address:
  Power Systems Virtual Server network ASN:
  IBM Cloud ASN:
  Private Network ID (1):
  Private Network ID (2):
  Private Network ID (3):
  ```
  {: codeblock}

1. Le cas {{site.data.keyword.powerSys_notm}} est clôturé lorsque la connexion Direct Link Connect est configurée pour communiquer avec votre instance {{site.data.keyword.powerSys_notm}}.
