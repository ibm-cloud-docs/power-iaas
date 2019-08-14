---

copyright:
  years: 2019

lastupdated: "2019-05-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}

# A propos de Power Systems Virtual Servers
{: #about-power-virtual-server}

{{site.data.keyword.powerSysFull}} utilise la plateforme IBM Cloud pour créer des serveurs virtuels Power Systems, également appelés partitions logiques (LPAR), qui s'exécutent sur du matériel IBM Power Systems avec l'hyperviseur PowerVM.
{:shortdesc}

{{site.data.keyword.powerSys_notm}}s est une forme d'infrastructure sous forme de services (IaaS). Avec le service {{site.data.keyword.powerSys_notm}}, vous pouvez facilement créer et déployer un ou plusieurs serveurs virtuels qui exécutent le système d'exploitation AIX ou IBM i dans un cloud public. Une fois que vous avez mis à disposition le serveur virtuel dans le cloud, il vous incombe de vérifier que le système d'exploitation AIX ou IBM i est sécurisé.

## Fonctions principales
{: #apvs-key-features}

Voici quelques-unes des fonctions principales de {{site.data.keyword.powerSys_notm}}.

### Facturation directe
{: #apvs-billing}

{{site.data.keyword.powerSys_notm}} utilise un taux de facturation mensuel comprenant les licences pour les systèmes d'exploitation AIX et IBM i. Ce taux est calculé au prorata du nombre d'heures en fonction des ressources déployées sur l'instance {{site.data.keyword.powerSys_notm}} dans le mois. Lorsque vous créez l'instance {{site.data.keyword.powerSys_notm}}, vous pouvez voir le coût total de votre configuration en fonction des options que vous spécifiez.  Vous pouvez rapidement identifier les options de configuration qui vous offrent le meilleur rapport qualité-prix pour vos besoins métier. Pour plus d'informations, voir [Tarification](/docs/infrastructure/power-iaas?topic=power-iaas-pricing-virtual-server#pricing-virtual-server).

### Environnement de cloud hybride
{: #apvs-hybrid}

Vous pouvez utiliser {{site.data.keyword.powerSys_notm}}s pour exécuter toute charge de travail AIX ou IBM i hors site à partir de votre infrastructure matérielle Power Systems existante. L'exécution de vos charges de travail sur le cloud public vous permet de profiter de tous les avantages du cloud et d'offrir de l'élasticité, un accès en libre service, ainsi qu'une diffusion et une connectivité rapides à d'autres services IBM Cloud. Bien que vos charges de travail AIX et IBM i s'exécutent dans le cloud, vous conservez les mêmes fonctions évolutives, résilientes et prêtes pour la production offertes par le matériel Power Systems.

### Personnalisation de l'infrastructure
{: #apvs-customization}

Vous pouvez configurer et personnaliser les options suivantes lorsque vous créez un service {{site.data.keyword.powerSys_notm}} :
* Nombre d'instances de serveur virtuel
* Nombre de coeurs
* Quantité de mémoire
* Taille et type de volume de données (HDD ou SSD)
* Réseau privé ou public

### Utilisation de votre propre image
{: #apvs-own-image}

IBM vous fournit un stock d'images de systèmes d'exploitation AIX et IBM i lorsque vous créez un service {{site.data.keyword.powerSys_notm}}. Cependant, vous pouvez fournir votre propre image de système d'exploitation AIX ou IBM i personnalisée que vous avez préalablement déployée et testée. Pour plus d'informations, voir [Configuration d'une image personnalisée](/docs/infrastructure/power-iaas?topic=power-iaas-configuring-custom-image#configuring-custom-image).

## Spécifications matérielles
{: #apvs-hardware-specifications}

Le matériel IBM Power Systems suivant héberge l'instance {{site.data.keyword.powerSys_notm}} :

* Calcul
  * [Power System E880 (9119-MHE) ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/support/knowledgecenter/en/POWER8/p8hdx/9119_mhe_landing.htm){: new_window}
    * 9 To de mémoire
    * Carte PCI Express Fibre Channel (FC) 8 x 16 Gbits 2 ports
    * Carte PCI Express Ethernet-SR 10 x 10 Gbits 2 ports
  * [Power System S922 (9009-22A) ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/support/knowledgecenter/en/POWER9/p9hdx/9009_22a_landing.htm){: new_window}
    * 384 Go de mémoire
    * Carte PCI Express FC 2 x 16 Gbits 2 ports
    * Carte PCI Express Ethernet-SR 3 x 10 Gbits 2 ports

* Stockage
  * Storwize V7000F(2076-AF6) 2 contrôleurs
  * Storwize V7000 (2076-624) 2 contrôleurs

* Réseau
  * Cisco Nexus9000 93180YC-EX (10G)
  * Cisco Nexus9000 C9348GC-FXP (1G)

## Réseau public et réseau privé
{: #apvs-public-and-private}

Lorsque vous créez une instance {{site.data.keyword.powerSys_notm}}, vous pouvez sélectionner une interface de réseau privé ou une interface de réseau public.

* Réseau public
  * Méthode facile et rapide pour se connecter à une instance {{site.data.keyword.powerSys_notm}}.
  * IBM configure l'infrastructure réseau pour permettre une connexion de réseau public sécurisée sur Internet à l'instance {{site.data.keyword.powerSys_notm}}.
  * La connectivité est implémentée à l'aide d'un dispositif de routeur virtuel IBM Cloud (VRA) et d'une connexion Direct Link Connect.
  * Protection par pare-feu et prise en charge des protocoles réseau sécurisés suivants :
    * SSH
    * HTTPS
    * Ping
    * Emulation de terminal IBM i 5250 avec SSL (port 992)

* Réseau privé
  * Permet aux ressources de votre instance {{site.data.keyword.powerSys_notm}} d'accéder aux ressources {{site.data.keyword.cloud_notm}} existantes, comme par exemple des serveurs bare metal, des conteneurs Kubernetes ou du stockage en cloud.
  * Utilise une connexion Direct Link Connect pour la connexion à votre compte et aux ressources IBM Cloud. Le processus de création d'une connexion Direct Link Connect peut prendre quelques jours car l'équipe de support IBM Cloud doit configurer le lien.
  * Obligatoire pour la communication entre les différentes instances {{site.data.keyword.powerSys_notm}}.

    Pour plus d'informations sur les différentes options utilisées pour configurer un réseau privé, voir [Configuration d'un réseau privé](/docs/infrastructure/power-iaas?topic=power-iaas-cpn-configuring#cpn-configuring).
    {: note}

La figure suivante affiche la configuration de base d'un réseau public et d'un réseau privé :

![Affichage du trafic réseau pour connexion publique ou privée](/images/power-iaas-network1.svg "Affichage du trafic réseau pour connexion publique ou privée")

<!-- Customer A is able to connect to a public network by using a Direct Link Dedicated connection with their {{site.data.keyword.cloud_notm}} Power account. -->
<!-- Customer A is able to connect to a private network by using a Direct Link Connect connection with their {{site.data.keyword.cloud_notm}} account. -->
<!-- Customer A can use either a public or private network to access their {{site.data.keyword.powerSys_notm}}. -->
<!-- Customer B is able to connect to only a private network by using a Direct Link Connect connection with their {{site.data.keyword.cloud_notm}} account.  -->
