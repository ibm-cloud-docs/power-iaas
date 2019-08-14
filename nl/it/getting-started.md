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

# Introduzione a Power Systems Virtual Servers
{: #getting-started}


{{site.data.keyword.powerSysFull}} è un'offerta IaaS (Infrastructure as a Service) che puoi utilizzare per distribuire un server virtuale, noto anche come partizione logica (LPAR), in pochi minuti.
{:shortdesc}

Puoi distribuire velocemente i {{site.data.keyword.powerSys_notm}} per soddisfare le tue esigenze di business specifiche. Con {{site.data.keyword.powerSys_notm}} puoi creare un ambiente cloud ibrido che ti consente di controllare facilmente le richieste di carico di lavoro.

I {{site.data.keyword.powerSys_notm}} possono eseguire i carichi di lavoro AIX o IBM i in diverse ubicazioni geografiche.

## Terminologia
{: #gs-terminology}

Prima di creare un server virtuale, devi comprendere la differenza nella terminologia tra un **servizio** {{site.data.keyword.powerSys_notm}} e un'**istanza** {{site.data.keyword.powerSys_notm}}. Pensa a un **servizio** {{site.data.keyword.powerSys_notm}} come a un contenitore di tutte le **istanze** {{site.data.keyword.powerSys_notm}} in un'ubicazione geografica specifica. Il **servizio** {{site.data.keyword.powerSys_notm}} è disponibile da **Resource list** nell'IU {{site.data.keyword.cloud}}. Il servizio può contenere più **istanze** {{site.data.keyword.powerSys_notm}}.

Ad esempio, puoi avere due **servizi** {{site.data.keyword.powerSys_notm}}, uno in Dallas e un altro in Washington DC. Ciascun servizio può contenere più **istanze** {{site.data.keyword.powerSys_notm}}.

## Prima di cominciare 
{: #gs-before-you-begin}

Prima di creare la tua prima istanza di Power Systems Virtual Server, controlla i seguenti prerequisiti.

1. {: hide-dashboard} Crea un account IBM Cloud. Per creare un account IBM Cloud, vedi [Registrati in IBM Cloud ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/registration){: new_window}.

2. Crea una chiave SSH pubblica e privata che puoi utilizzare per connetterti in modo sicuro al tuo {{site.data.keyword.powerSys_notm}}. Per creare una chiave SSH pubblica e privata, vedi [Aggiunta di una chiave SSH ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/docs/infrastructure/ssh-keys?topic=ssh-keys-adding-an-ssh-key)

3. (Facoltativo) Se vuoi utilizzare un'immagine personalizzata per i sistemi operativi AIX o IBM i, devi creare un IBM Cloud Object Storage e caricare l'immagine. Per ulteriori informazioni, vedi [Configurazione di un'immagine personalizzata](/docs/infrastructure/power-iaas?topic=power-iaas-configuring-custom-image#configuring-custom-image).

4. (Facoltativo) se vuoi utilizzare una rete privata per connetterti a un'istanza di {{site.data.keyword.powerSys_notm}}, devi ordinare il servizio Direct Link Connect. Per ulteriori informazioni, vedi [Ordinazione di IBM Cloud Direct Link Connect dalla console dell'IU](/docs/infrastructure/power-iaas?topic=power-iaas-ordering-direct-link-connect).

## Passi successivi 
{: #gs-next-steps}

Con un account IBM Cloud e una chiave SSH pubblica e privata, sei ora pronto per [Creare il servizio {{site.data.keyword.powerSys_notm}}](/docs/infrastructure/power-iaas?topic=power-iaas-creating-power-virtual-server#creating-power-virtual-server).
