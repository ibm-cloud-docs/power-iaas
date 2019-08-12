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

# Options pour la haute disponibilité et la reprise après incident dans Power Systems Virtual Servers
{: #ha-dr}

L'instance {{site.data.keyword.powerSys_notm}} redémarre les serveurs virtuels sur un autre système hôte en cas de défaillance de matériel. Ce processus fournit des fonctions de haute disponibilité (HA) pour le service {{site.data.keyword.powerSys_notm}}.
{:shortdesc}

Si vous souhaitez disposer de solutions de haute disponibilité et de reprise après incident plus avancées, vous pouvez déployer les applications suivantes dans votre environnement {{site.data.keyword.powerSys_notm}}.

## PowerHA SystemMirror for AIX Standard Edition
{: #ha-dr-ha-standard}

Vous pouvez utiliser un modèle d'abonnement mensuel lors de l'achat de l'application PowerHA SystemMirror for AIX Standard Edition. Pour plus d'informations, voir les [options de tarification mensuelle pour Standard Edition ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/common/ssi/ShowDoc.wss?docURL=/common/ssi/rep_ca/8/897/ENUS219-288/index.html).

Après l'achat du logiciel, vous pouvez le télécharger à partir du site [IBM Entitled Systems Support (ESS) ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](http://www.ibm.com/eserver/ess). Vous pouvez installer PowerHA SystemMirror for AIX sur le serveur virtuel qui s'exécute dans votre environnement {{site.data.keyword.powerSys_notm}}. Pour obtenir les instructions d'installation, voir [Installing PowerHA SystemMirror ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/support/knowledgecenter/SSPHQG_7.2/install/ha_install.html).

Consultez les informations suivantes pour implémenter PowerHA SystemMirror for AIX dans votre environnement {{site.data.keyword.powerSys_notm}}.

* Lorsque vous créez les serveurs virtuels qui font partie du cluster PowerHA SystemMirror, vous devez sélectionner **Serveur différent** dans la zone **Règles de colocalisation**.
![Affichage de la zone Règles de colocalisation](/images/hadr2.png "Affichage de la zone Règles de colocalisation")

* Lorsque vous créez des volumes de stockage (disques) pour les serveurs virtuels qui font partie du cluster PowerHA SystemMirror, vous devez sélectionner **Activé** dans la zone **Partageable**.
![Affichage de la zone Partageable](/images/hadr1.png "Affichage de la zone Partageable")

* En utilisant le service {{site.data.keyword.powerSys_notm}}, vous n'avez pas accès à la console HMC, à VIOS et au système hôte. Par conséquent, toutes les fonctions de PowerHA SystemMirror qui nécessitent l'accès à ces fonctionnalités, telles que Resource Optimized High Availability (ROHA) et Active Node Halt Policy (ANHP), ne sont pas disponibles.

<!--* When you deploy PowerHA SystemMirror, you must verify that the Service IP address is defined as a private IP address. This Service IP address can be accessed by another {{site.data.keyword.powerSys_notm}} instance or from other {{site.data.keyword.cloud}} applications. You cannot use a public IP address because it cannot be moved from one interface to another interface within a virtual server or across different virtual servers. -->

<!--When you deploy PowerHA SystemMirror for AIX Enterprise Edition clusters in the {{site.data.keyword.powerSys_notm}} environment, you can only use the Geographic Logical Volume Manager (GLVM) functions. You cannot use storage mirroring functions that are part of PowerHA SystemMirror for AIX Enterprise Edition because you do not have access to the subsystem storage in the {{site.data.keyword.powerSys_notm}} environment. For more information, see [Geographic Logical Volume Manager ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SSPHQG_7.2/glvm/ha_glvm_kick.html).
{:note}
[Enterprise Edition monthly pricing options ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/common/ssi/cgi-bin/ssialias?infotype=AN&subtype=CA&htmlfid=897/ENUS219-286) -->

## Continuité des opérations via les fonctions de sauvegarde et restauration
{: #ha-dr-ha-business}

Votre configuration de {{site.data.keyword.powerSys_notm}} et vos données ne sont pas sauvegardées par {{site.data.keyword.cloud}}.

Vous pouvez utiliser l'interface utilisateur d'{{site.data.keyword.cloud_notm}} pour sauvegarder votre serveur virtuel dans {{site.data.keyword.cloud_notm}} Object Storage. Vous pouvez utiliser ce processus pour restaurer votre serveur virtuel en cas de panne critique. Pour plus d'informations, voir [Cloud Object Storage ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](/docs/services/cloud-object-storage?topic=cloud-object-storage-getting-started).
