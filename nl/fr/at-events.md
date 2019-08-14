---

copyright:
  years: 2016, 2019
lastupdated: "2019-05-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:important: .important}
{:note: .note}

# Evénements Activity Tracker pour {{site.data.keyword.powerSys_notm}}
{: #at_events}

En tant que responsable de la sécurité, auditeur ou gestionnaire, vous pouvez utiliser le service Activity Tracker pour suivre comment les utilisateurs et les applications interagissent avec le service {{site.data.keyword.powerSys_notm}} dans {{site.data.keyword.cloud}}.
{:shortdesc}

{{site.data.keyword.at_full_notm}} enregistre les activités initiées par l'utilisateur qui changent l'état d'un service dans {{site.data.keyword.cloud_notm}}. Vous pouvez utiliser ce service pour étudier une activité anormale et des actions critiques, ainsi que pour respecter des exigences en matière de vérification de réglementation. En outre, vous avez la possibilité d'être alerté des actions lors de leur déroulement. Les événements collectés sont conformes à la norme CADF (Cloud Auditing Data Federation). [En savoir plus](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started).

## Liste d'événements : Lecture
{: #at_actions_read}

L'événement suivant est utilisé pour lire l'instance {{site.data.keyword.powerSys_notm}}.

| Action                     | Description                     |
|:---------------------------|:--------------------------------|
| pcloud.cloud-instance.read | Lire une instance Power Cloud    |


## Liste d'événements : Images
{: #at_actions_images}

Les événements suivants concernent l'utilisation des images dans votre instance {{site.data.keyword.powerSys_notm}}.

| Action                     | Description                     |
|:---------------------------|:--------------------------------|
| pcloud.image.read          | Lire une image ou toutes les images   |
| pcloud.image.create        | Créer une image                 |
| pcloud.image.update        | Mettre à jour une image         |
| pcloud.image.delete        | Supprimer une image             |
| pcloud.image.capture       | Exporter une image              |


## Liste d'événements : Réseaux
{: #at_actions_networks}

Les événements suivants concernent l'utilisation des réseaux dans votre instance {{site.data.keyword.powerSys_notm}}.

| Action                     | Description                           |
|:---------------------------|:--------------------------------------|
| pcloud.network.read        | Lire un réseau ou tous les réseaux    |
| pcloud.network.create      | Créer un réseau (public/privé)        |
| pcloud.network.update      | Mettre à jour un réseau               |
| pcloud.network.delete      | Supprimer un réseau                   |
{: caption="Tableau 3. Actions qui génèrent des événements" caption-side="top"}

## Liste d'événements : {{site.data.keyword.powerSys_notm}}
{: #at_actions_virtual_servers}

Les événements suivants concernent l'utilisation de chaque serveur virtuel au sein de l'instance {{site.data.keyword.powerSys_notm}}.

| Action                        | Description                          |
|:------------------------------|:-------------------------------------|
| pcloud.pvm-instance.read      | Lire une instance Power Systems Virtual Server           |
| pcloud.pvm-instance.create    | Créer une instance Power Systems Virtual Server          |
| pcloud.pvm-instance.update    | Mettre à jour une instance Power Systems Virtual Server  |
| pcloud.pvm-instance.delete    | Supprimer une instance Power Systems Virtual Server      |
| pcloud.pvm-instance.start     | Démarrer une instance Power Systems Virtual Server       |
| pcloud.pvm-instance.stop      | Arrêter une instance Power Systems Virtual Server        |
| pcloud.pvm-instance.renew     | Redémarrer une instance Power Systems Virtual Server     |
| pcloud.pvm-instance.unknown   | Action inconnue sur une instance Power Systems Virtual Server |
| pcloud.pvm-instance.monitor   | Accès à la console sur une instance Power Systems Virtual Server |
| pcloud.pvm-instance.capture   | Capturer une instance Power Systems Virtual Server dans une image |

## Liste d'événements : Clés SSH
{: #at_actions_ssh_keys}

Les événements suivants concernent l'utilisation d'un compte et de clés SSH dans votre instance {{site.data.keyword.powerSys_notm}}.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| pcloud.tenant.read       | Lire les informations concernant votre locataire       |
| pcloud.ssh-key.read      | Lire une clé SSH ou des clés SSH |
| pcloud.ssh-key.create    | Créer une clé SSH           |
| pcloud.ssh-key.update    | Mettre à jour une clé SSH   |
| pcloud.ssh-key.delete    | Supprimer une clé SSH       |

## Liste d'événements : Volumes de données
{: #at_actions_data_volumes}

Les événements suivants concernent l'utilisation des volumes de données dans votre instance {{site.data.keyword.powerSys_notm}}.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| pcloud.volume.read       | Lire un ou plusieurs volumes|
| pcloud.volume.create     | Créer un volume             |
| pcloud.volume.update     | Mettre à jour un volume     |
| pcloud.volume.delete     | Supprimer un volume         |
| pcloud.volume.configure  | Connecter ou déconnecter un volume |

## Affichage des événements
{: #at_ui}

Les événements sont disponibles à l'emplacement **Dallas**.

{{site.data.keyword.at_full_notm}} ne peut posséder qu'une seule instance par emplacement. Pour afficher des événements, vous devez accéder à l'interface utilisateur Web du service {{site.data.keyword.at_full_notm}} à l'emplacement `us-south`. [En savoir plus](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-launch#launch_step2).
