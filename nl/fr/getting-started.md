---

copyright:
  years: 2019

lastupdated: "2019-7-12"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:important: .important}
{:tip: .tip}

# Initiation à Power Systems Virtual Servers
{: #getting-started}


{{site.data.keyword.powerSysFull}} est une offre de type Infrastructure sous forme de services (IaaS) que vous pouvez utiliser pour déployer un serveur virtuel, également appelé partition logique (LPAR), en quelques minutes.
{:shortdesc}

Vous pouvez déployer rapidement des instances {{site.data.keyword.powerSys_notm}} pour répondre à vos besoins métier spécifiques. Avec {{site.data.keyword.powerSys_notm}}, vous pouvez créer un environnement de cloud hybride qui vous permet de contrôler facilement les demandes en charge de travail.

{{site.data.keyword.powerSys_notm}}s peut exécuter des charges de travail AIX ou IBM i dans différentes zones géographiques.

## Terminologie
{: #gs-terminology}

Avant de créer un serveur virtuel, vous devez vous familiariser avec les différences terminologiques entre un **service** {{site.data.keyword.powerSys_notm}} et une **instance** {{site.data.keyword.powerSys_notm}}. Considérez le **service** {{site.data.keyword.powerSys_notm}} comme un conteneur regroupant toutes les **instances** {{site.data.keyword.powerSys_notm}} dans une zone géographique spécifique. Le **service** {{site.data.keyword.powerSys_notm}} est disponible dans la **Liste de ressources** de l'interface utilisateur d'{{site.data.keyword.cloud}}. Le service peut contenir plusieurs **instances** {{site.data.keyword.powerSys_notm}}.

Par exemple, vous pouvez disposer de deux **services** {{site.data.keyword.powerSys_notm}}, l'un à Dallas et l'autre à Washington DC. Chaque service peut contenir plusieurs **instances** {{site.data.keyword.powerSys_notm}}.

## Avant de commencer
{: #gs-before-you-begin}

Avant de créer votre première instance Power Systems Virtual Server, passez en revue les prérequis suivants :

1. {: hide-dashboard} Créez un compte IBM Cloud. Pour créer un compte IBM Cloud, voir le site d'[inscription à IBM Cloud ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/registration){: new_window}.

2. Créez une clé SSH publique et privée que vous pouvez utiliser pour vous connecter de manière sécurisée à {{site.data.keyword.powerSys_notm}}. Pour créer une clé SSH publique et une clé SSH privée, voir [Ajout d'une clé SSH ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/docs/infrastructure/ssh-keys?topic=ssh-keys-adding-an-ssh-key)

3. (Facultatif) Si vous souhaitez utiliser une image personnalisée pour les systèmes d'exploitation AIX ou IBM i, vous devez créer un compartiment IBM Cloud Object Storage et téléchargez l'image. Pour plus d'informations, voir [Configuration d'une image personnalisée](/docs/infrastructure/power-iaas?topic=power-iaas-configuring-custom-image#configuring-custom-image).

4. (Facultatif) Si vous souhaitez utiliser un réseau privé pour vous connecter à une instance {{site.data.keyword.powerSys_notm}}, vous devez commander le service Direct Link Connect. Pour plus d'informations, voir [Commande d'IBM Cloud Direct Link Connect à partir de la console de l'interface utilisateur](/docs/infrastructure/power-iaas?topic=power-iaas-ordering-direct-link-connect).

## Etapes suivantes
{: #gs-next-steps}

Avec un compte IBM Cloud et une clé SSH privée et une clé SSH publique, vous êtes désormais prêt à [créer le service {{site.data.keyword.powerSys_notm}}](/docs/infrastructure/power-iaas?topic=power-iaas-creating-power-virtual-server#creating-power-virtual-server).
