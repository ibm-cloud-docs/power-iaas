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
{:tip: .tip}
{:download: .download}
{:note: .note}

# Gestione di risorse e utenti {{site.data.keyword.powerSys_notm}} 
{: #managing-resources-and-users}

Le procedure di gestione di risorse e autorizzazioni {{site.data.keyword.powerSysFull}} si coordinano con i servizi IBM Cloud Identity and Access Management (IAM). IAM ti consente di autenticare in modo sicuro gli utenti, controllare l'acceso alle risorse {{site.data.keyword.powerSys_notm}} con i gruppi di risorse e consentire l'accesso a risorse specifiche per una serie di utenti con i gruppi di accesso. In altre parole, IAM è la tua risorsa completa per tutta la gestione di utenti e risorse in {{site.data.keyword.cloud_notm}}.
{: shortdesc}

Puoi assegnare le autorizzazioni IAM in base ai seguenti criteri:

* Singoli utenti
* Gruppi di accesso (gruppi di utenti)
* Tipi di risorse specifici
* Gruppo di risorse

Per ulteriori informazioni su IAM, rivedi le seguenti informazioni:

* [Introduzione a IAM](https://cloud.ibm.com/docs/iam?topic=iam-getstarted#getstarted)
* [Concetti di IAM](https://cloud.ibm.com/docs/iam?topic=iam-iamoverview)
* [Gestione dei gruppi di risorse](https://cloud.ibm.com/docs/resources?topic=resources-rgs)
* [Configurazione dei gruppi di accesso](https://cloud.ibm.com/docs/iam?topic=iam-groups)

## Ruoli di accesso alla piattaforma
{: #platform-access-roles}

Puoi utilizzare i ruoli di accesso alla piattaforma per consentire agli utenti di completare attività sulle risorse {{site.data.keyword.cloud_notm}}, come la creazione di utenti o l'aggiunta di servizi.

La seguente tabella visualizza i ruoli di accesso alla piattaforma IAM e il tipo corrispondente di controllo consentito da {{site.data.keyword.powerSys_notm}}:

| Ruolo accesso piattaforma |Tipo di accesso consentito|
|-----------|-------------------------|
| Visualizzatore | Visualizza ed elenca le istanze |
| Operatore | Visualizza ed elenca le istanze |
| Editor | Visualizza, elenca, crea ed elimina le istanze  |
|Amministratore| Visualizza, elenca, crea ed elimina le istanze ed assegna le politiche ad altri utenti. |

## Ruoli di accesso al servizio 
{: #service-access-roles}

Puoi utilizzare i ruoli di accesso al servizio per definire come gli utenti possono utilizzare le funzioni del servizio {{site.data.keyword.powerSys_notm}}.

La seguente tabella visualizza i ruoli di accesso al servizio IAM e le azioni corrispondenti che un utente può completare con {{site.data.keyword.powerSys_notm}}:

|Ruolo di accesso al servizio |Descrizione delle azioni |
|-----------|-------------------------|
|Lettore | Visualizza tutte le risorse, ad esempio le chiavi SSH, i volumi di archiviazione e le impostazioni di rete. Non puoi apportare alcuna modifica alle risorse. |
|Gestore| Puoi configurare tutte le risorse. Le seguenti sono alcune azioni che puoi eseguire:<ul><li>Creare istanze</li><li>Aumentare le dimensioni del volume di archiviazione</li><li>Creare le chiavi SSH</li><li>Modificare le impostazioni di rete</li><li>Creare immagini di avvio</li><li>Eliminare volumi di archiviazione</li>
</ul>

## Scenari di accesso utente
{: #user-access-scenarios}

I seguenti scenari di accesso coprono la procedura necessaria per aggiungere un nuovo utente e modificare le autorizzazioni di un utente esistente.

### Invito di un nuovo utente per visualizzare le risorse {{site.data.keyword.powerSys_notm}} 
{: #inviting-a-new-user-to-create-or-manage-resources}

Devi invitare un utente IBM Cloud nel tuo account e fornirgli l'accesso per visualizzare le risorse {{site.data.keyword.powerSys_notm}}. Ricorda, il ruolo di accesso al servizio determina il livello di accesso a disposizione di un utente con le risorse {{site.data.keyword.powerSys_notm}}.

Completa la seguente procedura in IAM per consentire a un utente di visualizzare le risorse {{site.data.keyword.powerSys_notm}}:

1. Vai all'[IU Utenti IAM ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/iam/users){: new_window} nella console IBM Cloud e fai clic su **Invita utenti**.

      ![Visualizza l'icona di invito utenti dall'IU IAM](/images/invite_users.png "Invito di utenti dall'IU IAM")

2. Nella sezione **Utenti**, immetti gli indirizzi email desiderati nel campo **Indirizzo email**.
3. Successivamente, seleziona **Risorsa** dal campo **Assegna accesso a** e **{{site.data.keyword.powerSys_notm}}** nel campo **Servizi**.

    ![Visualizza i campi del servizio](/images/invite_users2.png "Selezione del servizio {{site.data.keyword.powerSys_notm}} per un nuovo utente dall'IU IAM")

4. Seleziona il ruolo di accesso alla piattaforma che vuoi assegnare agli utenti. In questo scenario, l'utente può solo visualizzare le risorse {{site.data.keyword.cloud_notm}} e {{site.data.keyword.powerSys_notm}}.

    ![Visualizza l'IU per i ruoli IAM](/images/invite_users3.png "Selezione dei ruoli per un nuovo utente dall'IU IAM")

5. Fai clic su **Invita utenti**. L'utente deve accettare l'invito per essere aggiunto all'account. Se l'invito viene inviato correttamente, viene visualizzato un messaggio.

    ![Visualizza il messaggio per l'invito avvenuto correttamente](/images/invite_users4.png "Messaggio di invito inviato correttamente")

### Fornire un'autorizzazione utente esistente per gestire le risorse {{site.data.keyword.powerSys_notm}} 
{: #giving-an-existing-user-permission-to-manage-resources}

Completa la seguente procedura per fornire l'autorizzazione a un utente esistente nel tuo account in modo che possa configurare le risorse {{site.data.keyword.powerSys_notm}}.

1. Vai all'[IU Utenti IAM ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/iam/users){: new_window} nella console IBM Cloud.
2. Dall'elenco di utenti, seleziona quello a cui vuoi modificare l'autorizzazione.
3. Fai clic su **Politiche di accesso** e fai clic sui ruoli correnti per gli utenti. In questo scenario, fai clic su **Visualizzatore, lettore**.

    ![Visualizza come modificare le autorizzazioni di un utente esistente](/images/existing_user1.png "Modifica delle autorizzazioni per un utente dall'IU IAM")

4. Dal campo **Seleziona ruoli**, fai clic su **Gestore**. Puoi lasciare il ruolo **Lettore** selezionato.

    ![Visualizza l'aggiunta del ruolo di gestore per un utente esistente](/images/existing_user2.png "Selezione del ruolo di gestore dall'IU IAM")

5. Fai clic su **Salva**.

   L'utente è ora autorizzato a configurare le risorse {{site.data.keyword.powerSys_notm}}. Tuttavia, questo utente non può gestire i servizi e le risorse specifici della piattaforma {{site.data.keyword.cloud_notm}}. Ad esempio non può aggiungere dei nuovi utenti.
   {: note}
