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

# {{site.data.keyword.powerSys_notm}} Activity Tracker-Ereignisse
{: #at_events}

Als Sicherheitsbeauftragter, Auditor oder Manager können Sie den Activity Tracker-Service verwenden, um zu verfolgen, wie Benutzer und Anwendungen mit dem {{site.data.keyword.powerSys_notm}}-Service in {{site.data.keyword.cloud}} interagieren.{: shortdesc}

{{site.data.keyword.at_full_notm}} zeichnet benutzerinitiierte Aktivitäten auf, die den Status eines Service in {{site.data.keyword.cloud_notm}} ändern. Sie können diesen Service verwenden, um abnormale Aktivitäten und kritische Aktionen zu untersuchen und die regulatorischen Prüfungsanforderungen zu erfüllen. Darüber hinaus können Sie benachrichtigt werden, wenn bestimmte Aktionen ausgeführt werden. Die erfassten Ereignisse entsprechen dem Standard Cloud Auditing Data Federation (CADF). [Weitere Informationen](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started).

## Ereignisliste: Lesen
{: #at_actions_read}

Das folgende Ereignis wird verwendet, um die {{site.data.keyword.powerSys_notm}}-Instanz zu lesen.

| Aktion                     | Beschreibung                    |
|:---------------------------|:--------------------------------|
| pcloud.cloud-instance.read | Power Cloud-Instanz lesen       |


## Ereignisliste: Images
{: #at_actions_images}

Die folgenden Ereignisse sind für die Arbeit mit Images in Ihrer {{site.data.keyword.powerSys_notm}}-Instanz vorgesehen. 

| Aktion                     | Beschreibung                    |
|:---------------------------|:--------------------------------|
| pcloud.image.read          | Ein Image oder alle Images lesen|
| pcloud.image.create        | Ein neues Image erstellen           |
| pcloud.image.update        | Ein Image aktualisieren             |
| pcloud.image.delete        | Ein Image löschen               |
| pcloud.image.capture       | Ein Image exportieren           |


## Ereignisliste: Netze
{: #at_actions_networks}

Die folgenden Ereignisse sind für die Arbeit mit Netzen in Ihrer {{site.data.keyword.powerSys_notm}}-Instanz vorgesehen.

| Aktion                     | Beschreibung                           |
|:---------------------------|:--------------------------------------|
| pcloud.network.read        | Ein Netz oder alle Netze lesen         |
| pcloud.network.create      | Ein neues Netz erstellen (öffentlich/privat)|
| pcloud.network.update      | Ein Netz aktualisieren                     |
| pcloud.network.delete      | Ein Netz löschen                           |
{: caption="Tabelle 3. Aktionen, die Ereignisse generieren" caption-side="top"}

## Ereignisliste: {{site.data.keyword.powerSys_notm}}
{: #at_actions_virtual_servers}

Die folgenden Ereignisse sind für die Arbeit mit jedem virtuellen Server innerhalb der {{site.data.keyword.powerSys_notm}}-Instanz vorgesehen. 

| Aktion                        | Beschreibung                                          |
|:------------------------------|:-------------------------------------|
| pcloud.pvm-instance.read      | Virtuelle Power-Serverinstanz lesen                   |
| pcloud.pvm-instance.create    | Virtuelle Power-Serverinstanz erstellen               |
| pcloud.pvm-instance.update    | Virtuelle Power-Serverinstanz aktualisieren           |
| pcloud.pvm-instance.delete    | Virtuelle Power-Serverinstanz löschen                 |
| pcloud.pvm-instance.start     | Virtuelle Power-Serverinstanz starten                 |
| pcloud.pvm-instance.stop      | Virtuelle Power-Serverinstanz stoppen                 |
| pcloud.pvm-instance.renew     | Virtuelle Power-Serverinstanz neu starten             |
| pcloud.pvm-instance.unknown   | Unbekannte Aktion auf virtueller Power-Serverinstanz  |
| pcloud.pvm-instance.monitor   | Konsolenzugriff auf virtuelle Power-Serverinstanz     |
| pcloud.pvm-instance.capture   | Virtuelle Power-Serverinstanz in einem Image erfassen |

## Ereignisliste: SSH-Schlüssel
{: #at_actions_ssh_keys}

Die folgenden Ereignisse sind für die Arbeit mit Konto- und SSH-Schlüsseln in Ihrer {{site.data.keyword.powerSys_notm}}-Instanz vorgesehen. 

| Aktion                   | Beschreibung                   |
|:-------------------------|:----------------------------|
| pcloud.tenant.read       | Ihre Tenant-Information lesen         |
| pcloud.ssh-key.read      | Einen oder mehrere SSH-Schlüssel lesen |
| pcloud.ssh-key.create    | Einen SSH-Schlüssel erstellen        |
| pcloud.ssh-key.update    | Einen SSH-Schlüssel aktualisieren    |
| pcloud.ssh-key.delete    | Einen SSH-Schlüssel löschen          |

## Ereignisliste: Datenträger
{: #at_actions_data_volumes}

Die folgenden Ereignisse sind für die Arbeit mit Datenträgern in Ihrer {{site.data.keyword.powerSys_notm}}-Instanz vorgesehen. 

| Aktion                   | Beschreibung                 |
|:-------------------------|:----------------------------|
| pcloud.volume.read       | Datenträger lesen            |
| pcloud.volume.create     | Datenträger erstellen        |
| pcloud.volume.update     | Datenträger aktualisieren    |
| pcloud.volume.delete     | Datenträger löschen          |
| pcloud.volume.configure  | Datenträger an- oder abhängen|

## Ereignisse anzeigen
{: #at_ui}

Die Ereignisse stehen am Standort **Dallas** zur Verfügung. 

{{site.data.keyword.at_full_notm}} kann nur eine Instanz pro Standort aufweisen. Um Ereignisse anzeigen zu können, müssen Sie auf die Webbenutzerschnittstelle des {{site.data.keyword.at_full_notm}}-Service am Standort `us-south` zugreifen. [Weitere Informationen](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-launch#launch_step2).
