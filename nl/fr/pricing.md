---

copyright:
  years: 2019

lastupdated: "2019-06-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}

# Tarification pour Power Systems Virtual Server on IBM Cloud
{: #pricing-virtual-server}

{{site.data.keyword.powerSysFull}} est proposé dans une sélection de régions avec des partitions logiques (LPAR) à évolution linéaire pouvant atteindre jusqu'à 15 coeurs et 320 Go de mémoire, avec également des partitions LPAR d'entreprise pouvant atteindre 143 coeurs et 8192 Go de mémoire. Grâce à ces options, {{site.data.keyword.powerSys_notm}} est en mesure de répondre à toutes les exigences des charges de travail dans le cadre de votre entreprise. Vous êtes facturé tous les mois.
{:shortdesc}

## Utilisation mensuelle
{: #pricing-monthly-usage}

Les instances {{site.data.keyword.powerSys_notm}} sont facturées par mois et calculées au prorata du nombre d'heures. Si vous ajoutez des ressources à une partition logique en milieu de mois, la facture mensuelle de la partition logique reflète cette modification de ressource et son tarif est calculé au prorata du nombre d'heures.

### Exemple d'utilisation mensuelle
{: #pricing-monthly-usage-example}

Dans l'exemple suivant, vous achetez une instance {{site.data.keyword.powerSys_notm}} disposant d'un coeur et de 8 Go de mémoire, d'un disque de 150 Go et qui exécute AIX 7200-03-02, pour un prix de base fixé à 250,57 $ par mois (soit 0,343 dollar par heure). Au fil du mois, vous ajoutez plus de mémoire. Le nouveau prix de la partition logique s'élève à 339,45 $ par mois (soit 0,465 $ par heure). La facture mensuelle est calculée au prorata du nombre d'heures pour les ressources déployées.

| Heures écoulées dans le mois       | Montant facturé   |  Description de la partition logique     |
| ----------------------------- | ----------------- | --------------------  |
| 300 heures        | 300 heures x 251 $/mois = 103 $  | 1 coeur, 8 Go de mémoire, disque de 150 Go, AIX    |
| 430 heures        | 430 heures x 339 $/mois = 200 $  | 1 coeur, 16 Go de mémoire, disque de 150 Go, AIX  |
| 730 heures (total mensuel)  | 103 $ + 200 $ = 303 $ (total mensuel)  |   1 coeur, 16 Go de mémoire, disque de 150 Go, AIX |
{: caption="Tableau 1. Exemple de facturation mensuelle de partition logique" caption-side="top"}

Dans cet exemple, les ressources LPAR sont augmentées au bout de la 300e heure du mois pour passer de 8 Go à 16 Go de mémoire. Le prix de la partition logique est calculé au prorata du nombre d'heures pour aboutir au prix mensuel final de cette partition logique (303 $).

## Tarifs de base d'une instance
{: #pricing-base-instance-prices}

La facturation de base d'une instance dépend des options, par exemple, du type de machine, du nombre de coeurs et de la quantité de mémoire que vous sélectionnez lorsque vous créez une instance {{site.data.keyword.powerSys_notm}}. Lorsque vous créez votre instance de serveur virtuel, la tarif mensuel associé s'affiche. Pour plus d'informations, voir [Création d'une instance {{site.data.keyword.powerSys_notm}}](/docs/infrastructure/power-iaas?topic=power-iaas-creating-power-virtual-server#creating-power-virtual-server).

## Systèmes d'exploitation
{: #pricing-operating-systems}

Les images stockées suivantes vous sont fournies par IBM :
* AIX
  * 7200-03-02
  * 7100-05-03

* IBM i
  * 7.3 TR5
  * 7.2 TR9

Vous pouvez aussi fournir votre propre image personnalisée à utiliser sur une instance {{site.data.keyword.powerSys_notm}}, mais vous devez toujours vous acquitter d'une licence de système d'exploitation pour IBM Cloud. Vous ne pouvez pas utiliser une licence AIX ou IBM i existante pour les partitions logiques dans une instance {{site.data.keyword.powerSys_notm}}. Si vous utilisez une image personnalisée ou une image stockée, vous êtes facturé au même prix. Pour plus d'informations, voir [Configuration d'une image personnalisée](/docs/infrastructure/power-iaas?topic=power-iaas-configuring-custom-image#configuring-custom-image).

## Fin du cycle de facturation
{: #pricing-end-of-billing}

La facturation mensuelle prend fin lorsque vous supprimez la partition logique. Si vous augmentez ou réduisez votre infrastructure en fonction des besoins de vos charges de travail, la facturation suit le planning des changements liés à la mise à disposition de la partition logique. Si vous arrêtez la partition logique, le processus de facturation ne s'arrête pas. Vous devez supprimer la partition logique pour mettre un terme au cycle de facturation.
