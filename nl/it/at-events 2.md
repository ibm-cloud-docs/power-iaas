---

copyright:
  years: 2016, 2019
lastupdated: "2019-07-29"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:important: .important}
{:note: .note}

# Eventi di {{site.data.keyword.powerSys_notm}} Activity Tracker 
{: #at_events}

Come responsabile della sicurezza, revisore o gestore, puoi utilizzare il servizio Activity Tracker per tenere traccia di come gli utenti e le applicazioni interagiscono con il servizio {{site.data.keyword.powerSys_notm}} in {{site.data.keyword.cloud}}.
{: shortdesc}

{{site.data.keyword.at_full_notm}} registra le attività avviate dall'utente che modificano lo stato di un servizio in {{site.data.keyword.cloud_notm}}. Puoi utilizzare questo servizio per investigare l'attività anomala, le azioni critiche e per rispettare i requisiti di controllo normativi. Inoltre, puoi essere avvisato riguardo le azioni quando si verificano. Gli eventi vengono raccolti conformi agli standard CADF (Cloud Auditing Data Federation).
[Ulteriori informazioni](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started).

## Elenco di eventi: lettura
{: #at_actions_read}

Il seguente evento viene utilizzato per leggere l'istanza di {{site.data.keyword.powerSys_notm}}.

| Azione                     |Descrizione|
|:---------------------------|:--------------------------------|
| pcloud.cloud-instance.read | Leggi un'istanza Power Cloud     |


## Elenco di eventi: immagini
{: #at_actions_images}

I seguenti eventi sono pensati per l'utilizzo delle immagini nella tua istanza di {{site.data.keyword.powerSys_notm}}.

| Azione                     |Descrizione|
|:---------------------------|:--------------------------------|
| pcloud.image.read          | Leggi un'immagine o tutte le immagini     |
| pcloud.image.create        | Crea una nuova immagine              |
| pcloud.image.update        | Aggiorna un'immagine                 |
| pcloud.image.delete        | Elimina un'immagine                 |
| pcloud.image.capture       | Esporta un'immagine                |


## Elenco di eventi: reti
{: #at_actions_networks}

I seguenti eventi sono pensati per l'utilizzo delle reti nella tua istanza di {{site.data.keyword.powerSys_notm}}.

| Azione                     |Descrizione|
|:---------------------------|:--------------------------------------|
| pcloud.network.read        | Leggi una rete o tutte le reti        |
| pcloud.network.create      | Crea una nuova rete (pubblica/privata) |
| pcloud.network.update      | Aggiorna una Rete                      |
| pcloud.network.delete      | Elimina una rete                      |
{: caption="Tabella 3. Azioni che generano eventi" caption-side="top"}

## Elenco di eventi: {{site.data.keyword.powerSys_notm}}
{: #at_actions_virtual_servers}

I seguenti eventi sono pensati per l'utilizzo di ciascun server virtuale all'interno dell'istanza di {{site.data.keyword.powerSys_notm}}.

| Azione                     |Descrizione|
|:------------------------------|:-------------------------------------|
| pcloud.pvm-instance.read      | Leggi un'istanza del server virtuale Power                  |
| pcloud.pvm-instance.create    | Crea un'istanza del server virtuale Power                  |
| pcloud.pvm-instance.update    | Aggiorna un'istanza del server virtuale Power                  |
| pcloud.pvm-instance.delete    | Elimina un'istanza del server virtuale Power                  |
| pcloud.pvm-instance.start     | Avvia un'istanza del server virtuale Power                  |
| pcloud.pvm-instance.stop      | Arresta un'istanza del server virtuale Power                  |
| pcloud.pvm-instance.renew     | Riavvia un'istanza del server virtuale Power                  |
| pcloud.pvm-instance.unknown   | Azione sconosciuta su un'istanza del server virtuale Power     |
| pcloud.pvm-instance.monitor   | Accesso della console a un'istanza del server virtuale Power     |
| pcloud.pvm-instance.capture   | Acquisisci un'istanza del server virtuale in un'immagine |

## Elenco di eventi: chiavi SSH
{: #at_actions_ssh_keys}

I seguenti eventi sono pensati per l'utilizzo delle chiavi SSH e dell'account nella tua istanza di {{site.data.keyword.powerSys_notm}}.

| Azione                     |Descrizione|
|:-------------------------|:----------------------------|
| pcloud.tenant.read       | Leggi le tue informazioni sul tenant       |
| pcloud.ssh-key.read      | Leggi una o più chiavi SSH   |
| pcloud.ssh-key.create    | Crea una chiave SSH            |
| pcloud.ssh-key.update    | Aggiorna una chiave SSH            |
| pcloud.ssh-key.delete    | Elimina una chiave SSH            |

## Elenco di eventi: volumi di dati
{: #at_actions_data_volumes}

I seguenti eventi sono pensati per l'utilizzo dei volumi di dati nella tua istanza di {{site.data.keyword.powerSys_notm}}.

| Azione                     |Descrizione|
|:-------------------------|:----------------------------|
| pcloud.volume.read       | Leggi uno o più volumi    |
| pcloud.volume.create     | Crea un volume            |
| pcloud.volume.update     | Aggiorna un volume            |
| pcloud.volume.delete     | Elimina un volume            |
| pcloud.volume.configure  | Collega o scollega un volume   |

## Visualizzazione degli eventi
{: #at_ui}

Gli eventi sono disponibili nell'ubicazione **Dallas**.

{{site.data.keyword.at_full_notm}} può avere solo un'istanza per ubicazione. Per visualizzare gli eventi, devi accedere all'IU web del servizio {{site.data.keyword.at_full_notm}} nell'ubicazione `us-south`. [Ulteriori informazioni](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-launch#launch_step2).
