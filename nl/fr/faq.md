---

copyright:
  years: 2019

lastupdated: "2019-03-29"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:important: .important}
{:tip: .tip}
{:faq: data-hd-content-type='faq'}

# Foire aux questions
{: #power-iaas-faqs}


## Quelles sont les versions des systèmes d'exploitation AIX et IBM i prises en charge ?
{: #os_versions}
{: faq}

Les versions d'AIX et IBM i prises en charge dépendent du matériel IBM Power Systems, à savoir S922 (9009-22A) ou E880 (9119-MHE), que vous avez sélectionné pour {{site.data.keyword.powerSys_notm}}. Pour afficher la liste des niveaux de technologie pris en charge pour les systèmes d'exploitation AIX et IBM i et le matériel Power Systems, voir [System software maps ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://www-01.ibm.com/support/docview.wss?uid=ssm1maps).

## Puis-je utiliser ma propre image d'AIX ou d'IBM i ?
{: #image}
{: faq}

Oui. Cette fonction s'appelle importer votre propre image. Pour plus d'informations, voir [Configuration d'une image personnalisée](/docs/infrastructure/power-iaas?topic=power-iaas-configuring-custom-image#configuring-custom-image).

## La maintenance des systèmes d'exploitation AIX ou IBM i est-elle assurée par IBM ?
{: #licensing_os}
{: faq}

Non. Il incombe aux clients d'assurer la maintenance, la mise à jour et la gestion des systèmes d'exploitation AIX ou IBM i.

## Comment fonctionnent les licences pour les systèmes d'exploitation AIX et IBM i ?
{: #os_support}
{: faq}

La licence du système d'exploitation fait partie du coût global du service. Vous ne pouvez pas utiliser une licence existante que vous avez déjà achetée.

## Comment fonctionnent les licences de tiers ?
{: #thridparty}
{: faq}

Vous êtes responsable des licences de tiers dans {{site.data.keyword.cloud_notm}}.

## Que sont les spécifications matérielles ?
{: #hardwarespecs}
{: faq}

Pour en savoir plus sur ces spécifications, voir [Spécifications matérielles](/docs/infrastructure/power-iaas?topic=power-iaas-about-power-virtual-server#apvs-hardware-specifications).

## Est-ce que {{site.data.keyword.powerSys_notm}} s'exécute dans un environnement mutualisé ?
{: #multi}
{: faq}

Oui.

## Y a-t-il des options bare metal ?
{: #bare}
{: faq}

Non. Le champ d'application de l'offre {{site.data.keyword.powerSys_notm}} est focalisé sur les instances virtuelles et non pas bare metal.

<!-- 
## Is there a price difference between shared or dedicated cores?
{: #shared}
{: faq}

No. Performance of shared cores is almost identical to dedicated cores. However, as server utilization spikes, there might be a cache or memory latency impacts. -->
