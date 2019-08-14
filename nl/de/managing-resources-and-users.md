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

# {{site.data.keyword.powerSys_notm}}-Ressourcen und Benutzer verwalten
{: #managing-resources-and-users}

Die Verfahren der Autorisierung und des Ressourcenmanagements von {{site.data.keyword.powerSysFull}} werden mit den IBM Cloud IAM-Services (Identity and Access Management) koordiniert. IAM ermöglicht es Ihnen, Benutzer sicher zu authentifizieren, den Zugriff auf {{site.data.keyword.powerSys_notm}}-Ressourcen mit Ressourcengruppen zu steuern und für eine Gruppe von Benutzern mithilfe von Zugriffsgruppen den Zugriff auf bestimmte Ressourcen zuzulassen. Mit anderen Worten: IAM ist Ihr zentraler Punkt für das gesamte Benutzer- und Ressourcenmanagement in der {{site.data.keyword.cloud_notm}}.
{: shortdesc}

Sie können IAM-Berechtigungen basierend auf den folgenden Kriterien zuordnen:

* Einzelne Benutzer
* Zugriffsgruppen (Benutzergruppen)
* Bestimmte Ressourcentypen
* Ressourcengruppen

Weitere Informationen zu IAM finden Sie in den folgenden Informationen: 

* [Einführung in IAM](https://cloud.ibm.com/docs/iam?topic=iam-getstarted#getstarted)
* [IAM-Konzepte](https://cloud.ibm.com/docs/iam?topic=iam-iamoverview)
* [Ressourcengruppen verwalten](https://cloud.ibm.com/docs/resources?topic=resources-rgs)
* [Zugriffsgruppen einrichten](https://cloud.ibm.com/docs/iam?topic=iam-groups)

## Plattformzugriffsrollen
{: #platform-access-roles}

Sie können Plattformzugriffsrollen verwenden, um Benutzern das Ausführen von Tasks mit {{site.data.keyword.cloud_notm}}-Ressourcen, wie z. B. das Erstellen von Benutzern oder das Hinzufügen von Services zu ermöglichen.

In der folgenden Tabelle werden die Zugriffsrollen für die IAM-Plattform und der entsprechende Typ der Steuerung angezeigt, der von {{site.data.keyword.powerSys_notm}} zugelassen wird: 

| Plattformzugriffsrolle | Zulässige Zugriffsart |
|-----------|-------------------------|
| Anzeigeberechtigter | Instanzen anzeigen und auflisten. |
| Operator | Instanzen anzeigen und auflisten. |
| Editor | Instanzen anzeigen, auflisten, erstellen und löschen. |
| Administrator | Instanzen anzeigen, auflisten, erstellen und löschen und anderen Benutzern Zugriffsrichtlinien zuordnen. |

## Servicezugriffsrollen
{: #service-access-roles}

Sie können die Servicezugriffsrollen verwenden, um zu definieren, was Benutzer mit {{site.data.keyword.powerSys_notm}}-Servicefunktionen tun können.

In der folgenden Tabelle werden die Zugriffsrollen für den IAM-Service und die entsprechenden Aktionen angezeigt, die ein Benutzer mit {{site.data.keyword.powerSys_notm}} ausführen kann:

| Servicezugriffsrolle | Beschreibung der Aktionen |
|-----------|-------------------------|
| Leseberechtigter | Alle Ressourcen anzeigen, wie z. B. SSH-Schlüssel, Speicherdatenträger und Netzeinstellungen. Sie können keine Änderungen an den Ressourcen vornehmen.|
| Manager | Sie können alle Ressourcen konfigurieren. Im Folgenden sind einige der Aktionen beschrieben, die Sie ausführen können: <ul><li>Instanzen erstellen</li><li>Größe des Speicherdatenträgers erhöhen</li><li>SSH-Schlüssel erstellen</li><li>Netzeinstellungen ändern</li><li>Boot-Images erstellen</li><li>Speicherdatenträger löschen</li>
</ul>

## Szenarios für den Benutzerzugriff
{: #user-access-scenarios}

Die folgenden Zugriffsszenarios decken die Schritte ab, die erforderlich sind, um einen neuen Benutzer hinzuzufügen und die Berechtigungen für einen vorhandenen Benutzer zu ändern. 

### Neuen Benutzer einladen, die {{site.data.keyword.powerSys_notm}}-Ressourcen anzuzeigen
{: #inviting-a-new-user-to-create-or-manage-resources}

Sie müssen einen IBM Cloud-Benutzer in Ihr Konto einladen und ihm Zugriff erteilen, damit er {{site.data.keyword.powerSys_notm}}-Ressourcen anzeigen kann. Denken Sie daran, dass die Servicezugriffsrolle die Zugriffsebene bestimmt, die ein Benutzer für {{site.data.keyword.powerSys_notm}}-Ressourcen hat.

Führen Sie die folgenden Schritte in IAM aus, um einem Benutzer zu ermöglichen, {{site.data.keyword.powerSys_notm}}-Ressourcen anzuzeigen: 

1. Navigieren Sie zur [Benutzerschnittstelle für IAM-Benutzer![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://cloud.ibm.com/iam/users){: new_window} in der IBM Cloud-Konsole und klicken Sie auf den Link, mit dem Sie einen **Benutzer einladen** können.

      ![Zeigt das Symbol zum Einladen von Benutzern in der IAM-Benutzerschnittstelle](/images/invite_users.png "Benutzer über die IAM-Benutzerschnittstelle einladen")

2. Geben Sie im Abschnitt für **Benutzer** die gewünschte E-Mail-Adresse in das Feld für die **E-Mail-Adresse** ein.
3. Wählen Sie danach eine **Ressource** im Feld zum **Zugriff erteilen auf** aus. Wählen Sie in **{{site.data.keyword.powerSys_notm}}** im Feld für **Services** aus. 

    ![Zeigt die Servicefelder an.](/images/invite_users2.png "Auswahl des {{site.data.keyword.powerSys_notm}}-Service für einen neuen Benutzer in der IAM-Benutzerschnittstelle")

4. Wählen Sie die Plattformzugriffsrolle aus, die Sie den Benutzern zuordnen möchten. In diesem Szenario kann der Benutzer nur {{site.data.keyword.cloud_notm}}- und {{site.data.keyword.powerSys_notm}}-Ressourcen anzeigen. 

    ![Zeigt die Benutzerschnittstelle für IAM-Rollen an.](/images/invite_users3.png "Die Auswahl von Rollen für einen neuen Benutzer in der IAM-Benutzerschnittstelle")

5. Klicken Sie auf die entsprechende Option, mit der Sie **Benutzer einladen** können. Der Benutzer muss die Einladung akzeptieren, um dem Konto hinzugefügt zu werden. Wenn die Einladung erfolgreich gesendet wurde, wird eine Nachricht angezeigt.

    ![Zeigt die Nachricht über die erfolgreich Einladung an.](/images/invite_users4.png "Nachricht über erfolgreiche Einladung")

### Einem vorhandenen Benutzer die Berechtigung zum Verwalten von {{site.data.keyword.powerSys_notm}}-Ressourcen erteilen.
{: #giving-an-existing-user-permission-to-manage-resources}

Führen Sie die folgenden Schritte aus, um einem vorhandenem Benutzer in Ihrem Konto die Berechtigung zum Konfigurieren von{{site.data.keyword.powerSys_notm}}-Ressourcen zu erteilen. 

1. Navigieren Sie zur [Benutzerschnittstelle für IAM-Benutzer![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://cloud.ibm.com/iam/users){: new_window} in der IBM Cloud-Konsole.
2. Wählen Sie in der Liste der Benutzer den Benutzer aus, deren Berechtigung Sie ändern möchten. 
3. Klicken Sie auf **Zugriffsrichtlinien** und dann auf die aktuellen Rollen für den Benutzer. Klicken Sie in diesem Szenario auf **Anzeigeberechtigter, Leseberechtigter**.

    ![Zeigt, wie die Berechtigungen für einen vorhandenen Benutzer geändert werden.](/images/existing_user1.png "Änderung der Berechtigungen für einen Benutzer von der IAM-Benutzerschnittstelle")

4. Klicken Sie im Feld **Rollen auswählen** auf **Manager**. Sie können die Rolle **Leseberechtigter** ausgewählt lassen. 

    ![Zeigt das Hinzufügen der Rolle für Managementaufgaben für einen vorhandenen Benutzer.](/images/existing_user2.png "Auswahl der Rolle für Managementaufgaben von der IAM-Benutzerschnittstelle")

5. Klicken Sie auf **Speichern**.

   Der Benutzer ist nun berechtigt, {{site.data.keyword.powerSys_notm}}-Ressourcen zu konfigurieren. Dieser Benutzer kann jedoch keine Services und Ressourcen verwalten, die für die {{site.data.keyword.cloud_notm}}-Plattform spezifisch sind. Er kann zum Beispiel keine neuen Benutzer hinzufügen.
{: note}
