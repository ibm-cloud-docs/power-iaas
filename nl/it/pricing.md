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

# Prezzi di Power Systems Virtual Server on IBM Cloud
{: #pricing-virtual-server}

{{site.data.keyword.powerSysFull}} è offerto in regioni selezionate con partizioni logiche di ridimensionamento incrementale (LPAR) con fino a 15 core e 320 GB di memoria e anche con LPAR aziendali fino a 143 core e 8192 GB di memoria. Con queste opzioni, {{site.data.keyword.powerSys_notm}} può soddisfare tutti i requisiti di carico di lavoro per il tuo business. La tua fatturazione è su frequenza mensile.
{:shortdesc}

## Utilizzo mensile
{: #pricing-monthly-usage}

L'addebito delle istanze di {{site.data.keyword.powerSys_notm}} è su frequenza mensile e viene calcolato su base proporzionale oraria. Se aggiungi delle risorse a una LPAR durante un mese, la fattura mensile per la LPAR riflette la modifica di risorse e il prezzo della LPAR è su base proporzionale oraria.

### Esempio di utilizzo mensile
{: #pricing-monthly-usage-example}

Nel seguente esempio, acquisti un'istanza di {{site.data.keyword.powerSys_notm}} con un 1 core con 8 GB di memoria, un disco da 150 GB ed eseguita su AIX 7200-03-02, al prezzo di base di $250,57 al mese ($0,343 all'ora). Con il passare del mese, aggiungi ulteriore memoria. Il nuovo prezzo per la LPAR è $339,45 al mese ($0,465 all'ora). La fattura mensile viene calcolata su base proporzionale oraria per le risorse distribuite.

| Ore trascorse in un mese       |Importo addebitato |  Descrizione LPAR     |
| ----------------------------- | ----------------- | --------------------  |
| 300 ore        | 300 ore x $251/mese = $103  | 1 core, 8 GB di memoria, disco da 150 GB, AIX    |
| 430 ore        | 430 ore x $339/mese = $200  | 1 core, 16 GB di memoria, disco da 150 GB, AIX    |
| 730 ore (totale mensile)  | $103 + $200 = $303 (totale mensile)  | 1 core, 16 GB di memoria, disco da 150 GB, AIX    |
{: caption="Tabella 1. Esempio di addebiti LPAR mensili" caption-side="top"}

In questo esempio, le risorse LPAR vengono aumentate dopo 300 ore del mese da 8 GB di memoria a 16 GB. Il prezzo per la LPAR viene calcolato su base proporzionale oraria per il prezzo mensile finale della LPAR ($303).

## Prezzi dell'istanza di base
{: #pricing-base-instance-prices}

La fatturazione dell'istanza di base dipende dalle opzioni, ad esempio il tipo di macchina, il numero di core e la quantità di memoria che selezioni quando crei un {{site.data.keyword.powerSys_notm}}. Quando crei la tua istanza del server virtuale, viene visualizzata la frequenza mensile associata. Per ulteriori informazioni, vedi [Creazione di un {{site.data.keyword.powerSys_notm}}](/docs/infrastructure/power-iaas?topic=power-iaas-creating-power-virtual-server#creating-power-virtual-server).

## Sistemi operativi
{: #pricing-operating-systems}

Le seguenti sono le immagini disponibili che ti vengono fornite da IBM:
* AIX
  * 7200-03-02
  * 7100-05-03

* IBM i
  * 7.3 TR5
  * 7.2 TR9

Puoi utilizzare la tua immagine personalizzata su un'istanza di {{site.data.keyword.powerSys_notm}} ma viene comunque acquistata una licenza per IBM Cloud. Non puoi utilizzare una licenza AIX o IBM i esistente per le LPAR in un'istanza di {{site.data.keyword.powerSys_notm}}. Se utilizzi un'immagine personalizzata o disponibile, ti viene addebitato lo stesso prezzo. Per ulteriori informazioni, vedi [Configurazione di un'immagine personalizzata](/docs/infrastructure/power-iaas?topic=power-iaas-configuring-custom-image#configuring-custom-image).

## Termine della fatturazione
{: #pricing-end-of-billing}

Il ciclo di fatturazione mensile termina quando elimini la LPAR. Se ridimensioni la tua struttura in modo incrementale o decrementale in risposta ai requisiti di carico di lavoro, la tua fatturazione segue la tempistica della modifica al provisioning di LPAR. Se arresti la LPAR, il processo di fatturazione non viene arrestato. Devi eliminare la LPAR per arrestare il ciclo di fatturazione.
