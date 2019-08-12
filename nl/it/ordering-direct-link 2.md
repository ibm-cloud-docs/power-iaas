---

copyright:
  years: 2019

lastupdated: "2019-06-17"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:download: .download}


# Ordinazione di IBM Cloud Direct Link Connect per Power Systems Virtual Servers
{: #ordering-direct-link-connect}

Un'opzione per configurare una rete privata con {{site.data.keyword.powerSys_notm}} è di utilizzare il servizio Direct Link Connect. Il servizio Direct Connect Link crea una connessione che consente l'accesso alle risorse {{site.data.keyword.cloud}} dalla tua istanza di {{site.data.keyword.powerSys_notm}}. Il servizio Direct Link Connect viene anche utilizzato per connettere la tua rete in loco alla rete IBM Cloud tramite IBM Cloud Virtual Router Appliance (VRA).

Puoi utilizzare la console dell'IU {{site.data.keyword.cloud_notm}} per ordinare il servizio Direct Link. Per la connessione al tuo ambiente {{site.data.keyword.powerSys_notm}}, vuoi ordinare due connessioni Direct Link Connect. Direct Link Connect è un servizio separato dal servizio {{site.data.keyword.powerSys_notm}}. Per controllare le tariffe di Direct Link Connect, vedi [Prezzi per IBM Cloud Direct Link](/docs/infrastructure/direct-link?topic=direct-link-pricing-for-direct-link-connect){: new_window}.

## Prima di cominciare
{: #before-direct-link-connect}

* Verifica che il tuo account {{site.data.keyword.cloud}} disponga delle autorizzazioni corrette per ordinare il servizio Direct Link Connect.
* Scopri i concetti di rete di base per il servizio Direct Link Connect controllando i seguenti argomenti:
  * [Concetti di Direct Link Connect](/docs/infrastructure/direct-link?topic=direct-link-direct-link-connect-solution#direct-link-connect-solution)
  * [Dettagli di Direct Link Connect](/docs/infrastructure/direct-link?topic=direct-link-ibm-cloud-direct-link-connect-details)
  * [Limitazioni di Direct Link Connect](/docs/infrastructure/direct-link?topic=direct-link-known-limitations#ibm-cloud-direct-link-exchange-and-direct-link-connect-limitations)
  * [Limitazioni rigorose sulle assegnazioni IP](/docs/infrastructure/direct-link?topic=direct-link-configure-ibm-cloud-direct-link#strict-limitations-on-ip-assignments)

## Procedura per ordinare Direct Link Connect
{: #steps-to-order-direct-link-connect}

Per ordinare il servizio Direct Link Connect che crea una connessione all'istanza di {{site.data.keyword.powerSys_notm}}, completa la seguente procedura:

1. Accedi al [Catalogo IBM Cloud ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/catalog){: new_window} con le tue credenziali dell'account IBM Cloud. Il tuo account deve disporre dell'autorizzazione corretta per ordinare il servizio Direct Link Connect.

1. Nella sezione **Networking**, fai clic sul tile **Direct Link Connect**.
![Visualizza il tile del catalogo Direct Link](/images/directlink1.png "Visualizza il tile del catalogo Direct Link")

1. Dalla voce di catalogo Direct Link Connect, fai clic su **Create**.

1. Dalla pagina IBM Cloud Direct Link, fai clic su **Order Direct Link Connect**.

1. Dalla pagina Create IBM Cloud Direct Link Connect Connection, completa i seguenti campi.

   Mentre completi i seguenti campi per la creazione del servizio Direct Link Connect, il prezzo viene aggiornato automaticamente in modo da rispecchiare le tue selezioni.
   {:note}

   <dl>
   <dt><strong>Nome istanza di Direct Link</strong><dt>
   <dd>Immetti un nome che descrive lo scopo di Direct Link Connect.</dd>
   <dt><strong>Ubicazione</strong><dt>
   <dd>Seleziona la stessa ubicazione dell'istanza di {{site.data.keyword.powerSys_notm}}. La seguente tabella identifica l'ubicazione dell'istanza di {{site.data.keyword.powerSys_notm}} e l'opzione di Direct Link Connection corrispondente:
   <table>
   <caption>Tabella 1. Opzioni di ubicazione di Direct Link Connection</caption>
   <tr>
   <th>Ubicazione di Power Systems Virtual Server</th>
   <th>Ubicazione di Direct Link Connect</th>
   </tr>
   <tr>
   <td>Dallas, TX US</td>
   <td>Dallas 4</td>
   </tr>
   <tr>
   <td>Washington D.C, US</td>
   <td>Washington 2</td>
   </tr>
   </table>
   </dd>
   <dt><strong>Provider di rete</strong><dt>
   <dd>Devi selezionare <strong>MEGAPORT</strong> dall'elenco.</dd>
   <dt><strong>Velocità di collegamento</strong><dt>
   <dd>Seleziona la velocità di collegamento che soddisfa i tuoi requisiti di carico di lavoro. La seleziona consigliata per questo campo è 1000 Mbps.</dd>
   <dt><strong>Opzione di instradamento</strong><dt>
   <dd>Seleziona <b>Local Routing (Free)</b> per accedere a tutti i data center connessi all'ubicazione che hai specificato nel campo <b>Location</b>. Seleziona <b>Global Routing</b> per accedere a tutti i data center IBM Cloud nel mondo. </dd>
   <dt><strong>BGP ASN</strong><dt>
   <dd>Devi immettere il numero BGP ASN per l'ubicazione di Direct Link Connect specifica nella seguente tabella.
   <table>
   <caption>Tabella 2. Numero BGP ASN per ubicazioni specifiche</caption>
   <tr>
   <th>Ubicazione di Direct Link Connect</th>
   <th>Numero BGP ASN</th>
   </tr>
   <tr>
   <td>Dallas 4</td>
   <td>64997</td>
   </tr>
   <tr>
   <td>Washington 2</td>
   <td>64999</td>
   </tr>
   </table>
   </dd>
   <dt><strong>Seleziona VRF</strong><dt>
   <dd>Seleziona l'opzione di inoltro e instradamento virtuale per la connessione. Se il tuo account non dispone di una VRF identificata, questo campo non viene visualizzato. Puoi ancora creare il servizio Direct Link Connect senza selezionare una VRF. </dd>
   <dd>
   La seguente figura è un esempio dei campi Direct Link Connect.
   ![Visualizza i campi Direct Link Connect completati](/images/directlink2.png "Visualizza i campi Direct Link Connect completati")
   </dd>
   </dl>
1. Leggi il Master Service Agreement e seleziona la casella di spunta. Devi leggere il Master Service Agreement perché contiene informazioni tecniche importanti che devi comprendere prima di procedere.

1. Fai clic su **Create**. Viene visualizzato il seguente messaggio quando la tua richiesta viene inviata correttamente.
![Visualizza il messaggio Direct Link Connect inviato correttamente](/images/directlink3.png "Visualizza il messaggio Direct Link Connect inviato correttamente")

1. Fai clic sul link Case number del servizio Direct Link Connect. Le informazioni nel numero di caso vengono utilizzate per identificare le informazioni di Direct Link Connect per la connessione alla tua istanza di {{site.data.keyword.powerSys_notm}}.

  Il supporto di IBM Cloud può richiedere fino a tre giorni lavorativi necessari al team di supporto IBM Cloud per creare la connessione Direct Link Connect.
  {: note}

1. Apri un nuovo caso per il team di supporto {{site.data.keyword.powerSys_notm}} per creare una connessione all'istanza di {{site.data.keyword.powerSys_notm}} utilizzando il servizio Direct Link Connect. Nel caso di {{site.data.keyword.powerSys_notm}}, specifica il numero di caso di Direct Link Connect. Il caso di {{site.data.keyword.powerSys_notm}} viene aggiornato con un ID servizio. Per informazioni su come aprire un caso, vedi [Come ottenere aiuto e supporto](/docs/infrastructure/power-iaas?topic=power-iaas-getting-help-and-support).

1. Immetti l'ID servizio dal numero di caso di {{site.data.keyword.powerSys_notm}} nel numero di caso di Direct Link Connect. Quando viene creata la connessione Direct Link Connect, il numero di caso di Direct Link Connect viene chiuso. Il seguente è un esempio delle informazioni sulla rete visualizzate nel caso:

  ```
  Link Speed:                  1000 Mbps
  Location:                    Washington 2
  Network Provider:            MEGAPORT
  IBM IP Address:              10.254.0.25/30
  Customer IP Address:         10.254.0.26/30
  Service Key:                 None
  BGP ASN:                     64999
  Network Identifier:          1748523-1
  Date Created:                2019-06-12T14:56:45-06:00
  ```
  {: screen}

1. Utilizza queste informazioni dal numero di caso di Direct Link Connect e immetti le seguenti informazioni sulla rete nel caso di {{site.data.keyword.powerSys_notm}}:

  ```
  Customer name:
  Customer account ID:
  Direct Link Connect subnet:
  Power Systems Virtual Server network IP address:
  IBM Cloud IP address:
  Power Systems Virtual Server network ASN:
  IBM Cloud ASN:
  Private Network ID (1):
  Private Network ID (2):
  Private Network ID (3):
  ```
  {: codeblock}

1. Il caso di {{site.data.keyword.powerSys_notm}} viene chiuso quando viene configurata la connessione Direct Link Connect in modo che comunichi con la tua istanza di {{site.data.keyword.powerSys_notm}}.
