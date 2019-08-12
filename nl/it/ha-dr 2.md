---

copyright:
  years: 2019

lastupdated: "2019-06-14"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:important: .important}
{:tip: .tip}
{:note: .note}

#Opzioni Alta disponibilità e Ripristino di emergenza in Power Systems Virtual Servers
{: #ha-dr}

L'istanza {{site.data.keyword.powerSys_notm}} riavvia i server virtuali su un sistema host diverso se si verifica un errore hardware. Questo processo fornisce le funzionalità di Alta disponibilità (HA, High Availability) di base per il servizio {{site.data.keyword.powerSys_notm}}.
{:shortdesc}

Se vuoi soluzioni HA o Ripristino di emergenza (DR, Disaster Recovery) più avanzate, puoi distribuire le seguenti applicazione nel tuo ambiente {{site.data.keyword.powerSys_notm}}.

## PowerHA SystemMirror for AIX Standard Edition
{: #ha-dr-ha-standard}

Puoi utilizzare un modello di sottoscrizione mensile quando acquisti PowerHA SystemMirror for AIX Standard Edition. Per ulteriori informazioni, vedi [Standard Edition monthly pricing options ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/common/ssi/ShowDoc.wss?docURL=/common/ssi/rep_ca/8/897/ENUS219-288/index.html).

Dopo aver acquistato il software, puoi scaricarlo da [IBM Entitled Systems Support (ESS) ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](http://www.ibm.com/eserver/ess). Puoi installare PowerHA SystemMirror for AIX sul server virtuale in esecuzione nel tuo ambiente {{site.data.keyword.powerSys_notm}}. Per le istruzioni di installazione, vedi [Installing PowerHA SystemMirror ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/support/knowledgecenter/SSPHQG_7.2/install/ha_install.html).

Controlla le seguenti informazioni per l'implementazione di PowerHA SystemMirror for AIX nel tuo ambiente {{site.data.keyword.powerSys_notm}}.

* Quando crei i server virtuali che fanno parte del cluster PowerHA SystemMirror, devi selezionare **Different Server** dal campo **Colocation Rules**.
![Visualizza il campo rules field](/images/hadr2.png "Visualizza il campo rules field")

* Quando crei i volumi di archiviazione (dischi) per i server virtuali che fanno parte del cluster PowerHA SystemMirror, devi selezionare **On** dal campo **Shareable**.
![Visualizza il campo shareable rules](/images/hadr1.png "Visualizza il campo shareable rules")

* Utilizzando il servizio {{site.data.keyword.powerSys_notm}}, non hai accesso a HMC, VIOS e al sistema host. Pertanto, tutte le funzioni di PowerHA SystemMirror che richiedono l'accesso a queste funzionalità, ad esempio Resource Optimized High Availability (ROHA) e Active Node Halt Policy (ANHP), non sono disponibili.

* Quando distribuisci PowerHA SystemMirror, devi verificare che l'indirizzo IP del servizio sia definito some un indirizzo IP privato. A questo indirizzo IP del servizio è possibile accedere da un'altra istanza di {{site.data.keyword.powerSys_notm}} o da altre applicazioni {{site.data.keyword.cloud}}. Non puoi utilizzare un indirizzo IP pubblico perché non può essere spostato da un'interfaccia a un'altra all'interno di un server virtuale o tra server virtuali diversi.

<!--When you deploy PowerHA SystemMirror for AIX Enterprise Edition clusters in the {{site.data.keyword.powerSys_notm}} environment, you can only use the Geographic Logical Volume Manager (GLVM) functions. You cannot use storage mirroring functions that are part of PowerHA SystemMirror for AIX Enterprise Edition because you do not have access to the subsystem storage in the {{site.data.keyword.powerSys_notm}} environment. For more information, see [Geographic Logical Volume Manager ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SSPHQG_7.2/glvm/ha_glvm_kick.html).
{:note}
[Enterprise Edition monthly pricing options ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/common/ssi/cgi-bin/ssialias?infotype=AN&subtype=CA&htmlfid=897/ENUS219-286) -->

## Continuità di business tramite il backup e il ripristino
{: #ha-dr-ha-business}

Non viene eseguito il backup della tua configurazione e dei tuoi dati di {{site.data.keyword.powerSys_notm}} da {{site.data.keyword.cloud}}.

Puoi utilizzare l'IU {{site.data.keyword.cloud_notm}} per eseguire il backup del tuo server virtuale in {{site.data.keyword.cloud_notm}} Object Storage. Puoi utilizzare questo processo per ripristinare il tuo server virtuale nel caso in cui si verifichi un errore critico. Per ulteriori informazioni, vedi [Cloud Object Storage ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](/docs/services/cloud-object-storage?topic=cloud-object-storage-getting-started).
