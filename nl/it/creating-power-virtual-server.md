---

copyright:
  years: 2019

lastupdated: "2019-08-1"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:table: .aria-labeledby="caption"}

# Creazione di un Power Systems Virtual Server
{: #creating-power-virtual-server}

Per creare e configurare un {{site.data.keyword.powerSysFull}}, completa la seguente procedura:

1. Accedi al [Catalogo IBM Cloud ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/catalog){: new_window} con le tue credenziali dell'account IBM Cloud.
2. Nella casella di ricerca del catalogo ,immetti **Power Systems Virtual Server** e fai clic sul tile {{site.data.keyword.powerSys_notm}}.

    ![Catalogo IBM Cloud](./images/catalog-search-bar.png "Catalogo IBM Cloud")

3. Assegna un nome al tuo servizio e scegli dove desideri distribuire la tua istanza di {{site.data.keyword.powerSys_notm}}.

    ![Selezione di servizio e regione](./images/power-iaas-service-region.png "Selezione di servizio e regione")

4. Fai clic sul pulsante **Create** in fondo alla pagina web.

    ![Pulsante Create](./images/power-iaas-create-button.png "Pulsante Create")

5. Dopo aver fatto clic sul pulsante **Create**, vieni reindirizzato al pannello **Resource List**.
6. Da **Resource List**, seleziona il tuo servizio in **Services** per andare al pannello **Manage**.

    ![IBM Cloud Resource List](./images/power-iaas-resource-list.png "IBM Cloud Resource List")

7. Da qui, fai clic sul pulsante **provision new**.

    ![Provisioning di un nuovo server virtuale](./images/power-iaas-provision-new.png "Provisioning di un nuovo server virtuale")

8. Completa tutti i campi obbligatori per creare in modo corretto una nuova stanza:

     Il prezzo viene aggiornato in modo dinamico nella sezione **Order Summary** mentre compili i campi per creare un {{site.data.keyword.powerSys_notm}}. Questo ti consente di creare facilmente un {{site.data.keyword.powerSys_notm}} conveniente che soddisfa le tue esigenze di business.
     {: tip}

    1. Compila tutti i campi nella sezione **Virtual servers**. Se selezioni più di un'istanza, ti vengono presentate ulteriori opzioni.

      ![Creazione di una nuova istanza del server virtuale Power](./images/console-virtual-instance.png "Creazione di una nuova istanza del server virtuale Power")

    1. Seleziona se desideri un **Dedicated processor** o un **Shared processor**. Ricorda di fare clic sul tipo di macchina (**Machine type**) desiderato e anche sul numero di core e sulla quantità di memoria.

      ![Selezione di processore e sistema](./images/console-profile.png "Selezione di processore e sistema")

    1. Infine, completa i campi **Boot volume**, **Attached volumes** e **Network interfaces** come indicato dalla tua organizzazione.

      ![Definisci le interfacce di rete e i volumi](./images/console-volume-network.png "Definisci le interfacce di rete e i volumi")

9. Accetta i termini di servizio (**Terms of Use**) e fai clic sul pulsante **Create** per eseguire il provisioning di un nuovo {{site.data.keyword.powerSys_notm}}.

La seguente tabella fornisce le informazioni sui campi **Virtual server instance**:

<table>
<caption>Tabella 1. Nuovi campi dell'istanza del server virtuale Power</caption>
<tr>
<th>Campo</th>
<th>Descrizione</th>
</tr>
<tr>
<td>Numero di istanze</td>
<td>Specifica il numero di istanze che vuoi creare per il {{site.data.keyword.powerSys_notm}}. Se specifichi più di un'istanza, puoi selezionare le seguenti convenzioni di denominazione e regole di posizionamento:
  <dl>
    <dt><strong>Nessuna preferenza</strong></dt>
  <dd>Seleziona questa opzione se non hai una preferenza per l'hosting.</dd>
    <dt><strong>Server differente</strong></dt>
  <dd>Seleziona questa opzione per fare in modo che ogni istanza sia ospitata su un server diverso.  Puoi utilizzare questa opzione se sei preoccupato che si verifichi un'interruzione a server singolo che potrebbe influenzare tutte le istanze di {{site.data.keyword.powerSys_notm}}. </dd>
  <dt><strong>Prefisso numerico</strong></dt>
  <dd>Seleziona questa opzione per aggiungere dei numeri prima del nome del server virtuale. Ad esempio, se il primo nome {{site.data.keyword.powerSys_notm}} è <kbd>Austin</kbd> il nome successivo per l'istanza virtuale è <kbd>1Austin</kbd></dd>
  <dt><strong>Suffisso numerico</strong></dt>
  <dd>Seleziona questa opzione per aggiungere dei numeri dopo il nome del server virtuale. Ad esempio, se il primo nome {{site.data.keyword.powerSys_notm}} è <kbd>Rochester</kbd> il nome successivo per l'istanza virtuale è <kbd>Rochester1</kbd>.</dd>
  </dl>
  <p>
  <strong>Nota:</strong> quando crei più istanze del server virtuale, devi selezionare <strong>On</strong> dal campo <strong>Shareable</strong> per ogni volume di dati che aggiungi. Se non vuoi che il volume di dati sia condivisibile, puoi aggiungerlo dopo aver creato il server virtuale.
  </p>
   </td>
</tr>
<tr>
<td>Blocca macchina virtuale</td>
<td>Seleziona <strong>On</strong> per bloccare il {{site.data.keyword.powerSys_notm}} in un sistema host. Se selezioni <strong>On</strong>, il server virtuale non può essere spostato su un host differente. Ad esempio, selezionando <strong>On</strong> riscontrerai un'interruzione durante la manutenzione dell'host.</td>
</tr>
<tr>
<td>Tipo di macchina</td>
<td>Specifica il tipo di macchina. Il tipo di macchina che selezioni determina il numero di core e la memoria disponibili. Per informazioni sulle specifiche hardware, vedi <a href="https://www.ibm.com/downloads/cas/KQ4BOJ3N" target="_blank">S922</a> e <a href="https://www.ibm.com/downloads/cas/EE476WAP" target="_blank">E880</a>.</td>
</tr>
<tr>
<td>Core</td>
<td>Seleziona il numero di core per il {{site.data.keyword.powerSys_notm}}. Se hai selezionato <strong>Shared Processors</strong>, puoi specificare il numero di core con incrementi di 0,25. Ad esempio, dei valori di core validi sono 0,5, 1,25 e 2,75. Una CPU virtuale viene assegnata per ogni titolarità di 0,25.

Se sei preoccupato riguardo i problemi di prestazioni, puoi selezionare <strong>Dedicated Processor</strong> perché il processo venga dedicato al tuo server virtuale e non condiviso. Per ulteriori informazioni, vedi <a href="https://www.ibm.com/developerworks/community/wikis/home?lang=en#!/wiki/Power%20Systems/page/How%20does%20Shared%20Processor%20Performance%20Compare%20to%20Dedicated%20Processors" target="_blank">How does Shared Processor Performance Compare to Dedicated Processors</a>.</td>
</tr>
<tr>
<td>Memoria</td>
<td>Seleziona la quantità di memoria per il {{site.data.keyword.powerSys_notm}}. La quantità di memoria che puoi selezionare dipende dal numero di core che hai selezionato. Per ogni core che selezioni, puoi assegnare fino a 64 GB. Ad esempio, se hai selezionato quattro core puoi selezionare fino a 256 GB di memoria. </td>
</tr>
<tr>
<td>Crea il volume di avvio</td>
<td>Seleziona una versione dell'immagine disponibile del sistema operativo AIX o IBM i che ti viene fornita o selezionane una personalizzata che hai precedentemente distribuito in locale. Per le informazioni sulle licenze del sistema operativo, vedi l'argomento <a href="https://www-03.ibm.com/software/sla/sladb.nsf" target="_blank">License Information documents</a> di IBM.

Se vuoi utilizzare la tua immagine personalizzata, devi utilizzare un livello di tecnologia supportato dell'immagine del sistema operativo AIX o IBM i per l'hardware Power Systems che hai selezionato nel campo <strong>Machine Type</strong>. Per ulteriori informazioni, vedi <a href="/docs/infrastructure/power-iaas?topic=power-iaas-configuring-custom-image#configuring-custom-image">Configurazione di un'immagine personalizzata</a>.</td>
</tr>
<tr>
<td>Volumi di dati collegati</td>
<td>Puoi creare un nuovo volume di dati o collegarne uno esistente che è già definito nel tuo account IBM Cloud.
<dl>
  <dt><strong>Crea volume di dati</strong></dt>
  <dd>Fai clic su <strong>Add</strong> per creare un nuovo volume di dati che può essere utilizzato come ulteriore archiviazione per la tua istanza di {{site.data.keyword.powerSys_notm}}. Se vuoi consentire a più istanze di {{site.data.keyword.powerSys_notm}} di scrivere i dati sullo stesso volume di dati, devi selezionare <strong>On</strong> dal campo <strong>Shareable</strong>. </dd>
  <dt><strong>Collega un volume di dati esistente</strong></dt>
  <dd>Seleziona un volume di dati esistente per fornire ulteriore archiviazione alla tua istanza di {{site.data.keyword.powerSys_notm}}. Se l'elenco non visualizza un volume di dati che hai precedentemente utilizzato, potrebbe essere perché è stato creato con un account IBM Cloud differente.</dd>
</dl>
</td>
</tr>
<tr>
<td>Reti pubbliche</td>
<td>Seleziona questa opzione per utilizzare una rete pubblica fornita da IBM. C'è un costo associato alla selezione di questa opzione. Per ulteriori informazioni, vedi <a href="/docs/infrastructure/power-iaas?topic=power-iaas-about-power-virtual-server#apvs-public-and-private" target="_blank">Reti pubbliche e private</a>.
</td>
</tr>
<tr>
<td>Reti private</td>
<td>Fai clic su <strong>Add</strong> per identificare una nuova rete privata per il server virtuale. Se hai già aggiunto una rete privata, puoi selezionarla dall'elenco. Per ulteriori informazioni, vedi <a href="/docs/infrastructure/power-iaas?topic=power-iaas-cpn-configuring#cpn-configuring" target="_blank">Configura rete privata</a>.</td>
</tr></table>
