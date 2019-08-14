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

# Informazioni su Power Systems Virtual Servers
{: #about-power-virtual-server}

{{site.data.keyword.powerSysFull}} utilizza la piattaforma IBM Cloud esistente per creare i server virtuali Power Systems, noti anche come partizioni logiche (LPAR), eseguiti su hardware IBM Power Systems con l'hypervisor PowerVM.
{:shortdesc}

{{site.data.keyword.powerSys_notm}} sono una forma di IaaS (infrastructure as a service). Con il servizio {{site.data.keyword.powerSys_notm}}, puoi creare e distribuire velocemente uno o più server virtuali eseguiti su sistemi operativi AIX o IBM i in un cloud pubblico. Dopo il provisioning del server virtuale nel cloud, è tua responsabilità assicurarti che i sistemi operativi AIX o IBM i siano sicuri.

## Funzioni chiave
{: #apvs-key-features}

Le seguenti sono alcune delle funzioni chiave per {{site.data.keyword.powerSys_notm}}.

### Fatturazione immediata
{: #apvs-billing}

{{site.data.keyword.powerSys_notm}} utilizza una frequenza di fatturazione mensile che include le licenze per i sistemi operativi AIX e IBM i. La frequenza di fatturazione mensile è su base proporzionale oraria sulle risorse distribuite all'istanza di {{site.data.keyword.powerSys_notm}} al mese. Quando crei l'istanza di {{site.data.keyword.powerSys_notm}}, puoi visualizzare i costi totali della tua configurazione basati sulle opzioni che specifichi.  Puoi identificare velocemente quali opzioni di configurazione ti forniscono il valore migliore per le tue esigenze di business. Per ulteriori informazioni, vedi [Prezzi](/docs/infrastructure/power-iaas?topic=power-iaas-pricing-virtual-server#pricing-virtual-server).

### Ambiente cloud ibrido
{: #apvs-hybrid}

Puoi utilizzare {{site.data.keyword.powerSys_notm}} per eseguire tutti i carichi di lavoro AIX o IBM i non in loco dalla tua infrastruttura hardware Power Systems esistente. L'esecuzione dei tuoi carichi di lavoro nel cloud pubblico ti consente di usufruire di tutti i vantaggi che il cloud ha da offrire come self-service, fornitura veloce, elasticità e connettività ad altri servizi IBM Cloud. Sebbene i tuoi carichi di lavoro AIX e IBM i vengano eseguiti nel cloud, continui a mantenere alcune funzioni scalabili, resilienti e pronte per la produzione fornite dall'hardware Power Systems.

### Personalizzazione dell'infrastruttura
{: #apvs-customization}

Puoi configurare e personalizzare le seguenti opzioni quando crei un {{site.data.keyword.powerSys_notm}}:
* Numero di istanze del server virtuali
* Numero di core
* Quantità di memoria
* Tipo e dimensione del volume di dati (HDD o SSD)
* Rete privata o pubblica

### Utilizza la tua immagine
{: #apvs-own-image}

IBM ti fornisce immagini di sistemi operativi AIX e IBM i disponibili quando crei un {{site.data.keyword.powerSys_notm}}. Tuttavia, puoi utilizzare la tua immagine di sistema operativo AIX o IBM i personalizzata che hai precedentemente distribuito e verificato. Per ulteriori informazioni, vedi [Configurazione di un'immagine personalizzata](/docs/infrastructure/power-iaas?topic=power-iaas-configuring-custom-image#configuring-custom-image).

## Specifiche hardware
{: #apvs-hardware-specifications}

Il seguente hardware di IBM Power Systems ospita il {{site.data.keyword.powerSys_notm}}:

* Calcolo
  * [Power System E880 (9119-MHE) ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/support/knowledgecenter/en/POWER8/p8hdx/9119_mhe_landing.htm){: new_window}
    * 9 TB di memoria
    * 8 x 16 Gigabit PCI Express Dual-port Fibre Channel (FC)
    * 10 x 10 Gigabit Ethernet-SR PCI Express Dual-port
  * [Power System S922 (9009-22A) ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/support/knowledgecenter/en/POWER9/p9hdx/9009_22a_landing.htm){: new_window}
    * 384 GB di memoria
    * 2 x 16 Gigabit PCI Express Dual-port FC
    * 3 x 10 Gigabit Ethernet-SR PCI Express Dual-port

* Archiviazione
  * Storewize V7000F(2076-AF6) Dual Controller
  * Storwize V7000 (2076-624) Dual Controller

* Rete
  * Cisco Nexus9000 93180YC-EX (10G)
  * Cisco Nexus9000 C9348GC-FXP (1G)

## Reti pubbliche e private
{: #apvs-public-and-private}

Quando crei un {{site.data.keyword.powerSys_notm}}, puoi selezionare delle interfacce di rete private o una pubblica.

* Rete pubblica
  * Metodo facile e veloce per la connessione a un'istanza di {{site.data.keyword.powerSys_notm}}.
  * IBM configura l'infrastruttura di rete per abilitare una connessione di rete pubblica sicura da internet all'istanza {{site.data.keyword.powerSys_notm}}.
  * La connettività viene implementata utilizzando un VRA (Virtual Router Appliance) di IBM Cloud e una connessione Direct Link Connect.
  * Protetta da firewall e supporta i seguenti protocolli di rete sicuri:
    * SSH
    * HTTPS
    * Ping
    * Emulazione di terminale IBM i 5250 con SSL (porta 992)

* Rete privata 
  * Consente alle risorse della tua istanza di {{site.data.keyword.powerSys_notm}} di accedere alle risorse {{site.data.keyword.cloud_notm}} esistenti, ad esempio server bare metal, contenitori Kubernetes o archiviazione cloud.
  * Utilizza una connessione Direct Link Connect per il collegamento alle tue risorse e alla tua rete dell'account IBM Cloud. Il processo di creazione di una connessione Direct Link Connect può durare alcuni giorni perché il supporto IBM Cloud deve configurare il link.
  * Necessaria per la comunicazione tra istanze di {{site.data.keyword.powerSys_notm}} differenti.

    Per ulteriori informazioni sulle diverse opzioni per la configurazione di una rete privata, vedi [Configura una rete privata](/docs/infrastructure/power-iaas?topic=power-iaas-cpn-configuring#cpn-configuring).
    {: note}

La seguente figura mostra la configurazione di base per una rete pubblica e privata.

![Visualizza come il traffico di rete fluisce per la connessione pubblica o privata](/images/power-iaas-network1.svg "Visualizza come il traffico di rete fluisce per la connessione pubblica o privata")

<!-- Customer A is able to connect to a public network by using a Direct Link Dedicated connection with their {{site.data.keyword.cloud_notm}} Power account. -->
<!-- Customer A is able to connect to a private network by using a Direct Link Connect connection with their {{site.data.keyword.cloud_notm}} account. -->
<!-- Customer A can use either a public or private network to access their {{site.data.keyword.powerSys_notm}}. -->
<!-- Customer B is able to connect to only a private network by using a Direct Link Connect connection with their {{site.data.keyword.cloud_notm}} account.  -->
