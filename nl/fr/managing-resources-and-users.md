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

# Gestion des ressources et des utilisateurs de {{site.data.keyword.powerSys_notm}}
{: #managing-resources-and-users}

Les pratiques en matière de gestion des ressources et des autorisations de {{site.data.keyword.powerSysFull}} sont coordonnées avec les services Identity and Access Management (IAM) d'IBM Cloud. IAM vous permet d'authentifier les utilisateurs en toute sécurité, contrôler l'accès aux ressources {{site.data.keyword.powerSys_notm}} avec des groupes de ressources et autoriser l'accès à des ressources spécifiques pour un ensemble d'utilisateurs avec des groupes d'accès. En d'autres termes, IAM est votre guichet unique pour gérer l'ensemble des ressources et des utilisateurs dans {{site.data.keyword.cloud_notm}}.
{: shortdesc}

Vous pouvez accorder des autorisations IAM en fonction des critères suivants :

* Utilisateurs individuels
* Groupes d'accès (groupes d'utilisateurs)
* Types spécifiques de ressources
* Groupes de ressources

Pour plus d'informations sur IAM, consultez les informations suivantes :

* [Tutoriel d'initiation à IAM](https://cloud.ibm.com/docs/iam?topic=iam-getstarted#getstarted)
* [Concepts IAM](https://cloud.ibm.com/docs/iam?topic=iam-iamoverview)
* [Gestion des groupes de ressources](https://cloud.ibm.com/docs/resources?topic=resources-rgs)
* [Configuration de groupes d'accès](https://cloud.ibm.com/docs/iam?topic=iam-groups)

## Rôles d'accès à la plateforme
{: #platform-access-roles}

Vous pouvez utiliser des rôles d'accès à la plateforme pour permettre aux utilisateurs d'effectuer des tâches sur les ressources {{site.data.keyword.cloud_notm}}, comme par exemple créer des utilisateur ou ajouter des services.

Le tableau suivant affiche les rôles d'accès à la plateforme d'IAM et le type correspondant de contrôle d'accès autorisé par {{site.data.keyword.powerSys_notm}} :

|Rôle d'accès à la plateforme | Type d'accès autorisé |
|-----------|-------------------------|
| Afficheur | Afficher des instances et répertorier des instances. |
| Opérateur | Afficher des instances et répertorier des instances. |
| Editeur | Afficher des instances, répertorier des instances, créer des instances, supprimer des instances.  |
| Administrateur | Afficher des instances, répertorier des instances, créer des instances, supprimer des instances et affecter des règles à d'autres utilisateurs. |

## Rôles d'accès au service
{: #service-access-roles}

Vous pouvez utiliser les rôles d'accès au service pour définir ce que les utilisateurs peuvent accomplir avec les fonctions des services {{site.data.keyword.powerSys_notm}}.

Le tableau suivant affiche les rôles d'accès au service d'IAM et les actions correspondantes qu'un utilisateur peut effectuer avec {{site.data.keyword.powerSys_notm}} :

| Rôle d'accès au service | Description des actions |
|-----------|-------------------------|
| Lecteur | Afficher toutes les ressources, telles que les clés SSH, les volumes de stockage et les paramètres réseau. Vous ne pouvez en aucun cas modifier les ressources. |
| Responsable | Vous pouvez configurer toutes les ressources. Voici les actions que vous pouvez effectuer :<ul><li>Créer des instances</li><li>Augmenter la taille des volumes de stockage</li><li>Créer des clés SSH</li><li>Modifier les paramètres réseau</li><li>Créer des images d'initialisation</li><li>Supprimer des volumes de stockage</li>
</ul>

## Scénarios d'accès utilisateur
{: #user-access-scenarios}

Les scénarios d'accès suivants englobent les étapes requises pour ajouter un nouvel utilisateur et modifier les droits d'accès d'un utilisateur existant.

### Invitation d'un nouvel utilisateur pour lui permettre d'afficher des ressources {{site.data.keyword.powerSys_notm}}
{: #inviting-a-new-user-to-create-or-manage-resources}

Vous devez inviter un utilisateur IBM Cloud dans votre compte et lui permettre d'afficher des ressources {{site.data.keyword.powerSys_notm}}. Notez que le rôle d'accès au service détermine le niveau d'accès d'un utilisateur aux ressources {{site.data.keyword.powerSys_notm}}.

Pour autoriser un utilisateur à afficher des ressources {{site.data.keyword.powerSys_notm}}, procédez comme suit dans IAM :

1. Accéder à la section [Utilisateurs de l'interface utilisateur IAM ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/iam/users){: new_window} dans la console IBM Cloud et cliquez sur **Inviter des utilisateurs**.

      ![Invitation d'utilisateurs à partir de l'interface utilisateur IAM](/images/invite_users.png "Invitation d'utilisateurs à partir de l'interface utilisateur IAM")

2. Dans la section **Utilisateurs**, entrez les adresses e-mail des utilisateurs désirés dans la zone **Adresse électronique**.
3. Sélectionnez ensuite **Ressource** dans la zone **Affecter l'accès à** et **{{site.data.keyword.powerSys_notm}}** dans la zone **Services**.

    ![Affichage des zones du service](/images/invite_users2.png "Sélection du service {{site.data.keyword.powerSys_notm}} pour un nouvel utilisateur à partir de l'interface utilisateur d'IAM")

4. Sélectionnez le rôle d'accès à la plateforme que vous souhaitez affecter aux utilisateurs. Dans ce scénario, un utilisateur peut uniquement afficher des ressources {{site.data.keyword.cloud_notm}} et {{site.data.keyword.powerSys_notm}}.

    ![Affichage de l'interface utilisateur avec les rôles IAM](/images/invite_users3.png "Sélection de rôles pour un nouvel utilisateur à partir de l'interface utilisateur d'IAM")

5. Cliquez sur **Inviter des utilisateurs**. L'utilisateur doit accepter l'invitation pour être ajouté au compte. Si l'invitation a bien été envoyée, un message s'affiche.

    ![Affichage d'un message indiquant que l'invitation a bien été envoyée](/images/invite_users4.png "Message indiquant que l'invitation a bien été envoyée")

### Octroi de droits de gestion des ressources {{site.data.keyword.powerSys_notm}} à un utilisateur existant
{: #giving-an-existing-user-permission-to-manage-resources}

Pour accorder à un utilisateur existant dans votre compte le droit de configurer des ressources {{site.data.keyword.powerSys_notm}}, procédez comme suit :

1. Accédez à la section [Utilisateurs de l'interface utilisateur d'IAM ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/iam/users){: new_window} dans la console IBM Cloud.
2. Dans la liste des utilisateurs, sélectionnez l'utilisateur dont vous souhaitez modifier l'autorisation.
3. Cliquez sur **Règles d'accès** et cliquez sur les rôles actuels des utilisateurs. Dans ce scénario, cliquez sur **Afficheur, Lecteur**.

    ![Affichage de la modification des droits d'un utilisateur existant](/images/existing_user1.png "Modification des droits d'un utilisateur dans l'interface utilisateur d'IAM")

4. Dans la zone **Sélectionner des rôles**, cliquez sur **Responsable**. Vous pouvez laisser le rôle **Lecteur** sélectionné.

    ![Affichage de l'ajout du rôle de responsable à un utilisateur existant](/images/existing_user2.png "Sélection du rôle de responsable dans l'interface utilisateur d'IAM")

5. Cliquez sur **Sauvegarder**.

   L'utilisateur est désormais autorisé à configurer des ressources {{site.data.keyword.powerSys_notm}}. Cependant, cet utilisateur ne peut pas gérer des services et des ressources spécifiques à la plateforme {{site.data.keyword.cloud_notm}}. Par exemple, il ne peut pas ajouter de nouveaux utilisateurs.
   {: note}
