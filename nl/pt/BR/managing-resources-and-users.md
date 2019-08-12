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

# Gerenciando recursos e usuários do {{site.data.keyword.powerSys_notm}}
{: #managing-resources-and-users}

As práticas de gerenciamento de recursos e autorização do {{site.data.keyword.powerSysFull}} são coordenadas com os serviços do IBM Cloud Identity and Access Management (IAM). O IAM permite que você autentique usuários com segurança, controle o acesso aos recursos do {{site.data.keyword.powerSys_notm}} com grupos de recursos e permita acesso a recursos específicos para um conjunto de usuários com grupos de acesso. Em outras palavras, o IAM reúne todo o gerenciamento de recursos e usuários no {{site.data.keyword.cloud_notm}}.
{: shortdesc}

É possível designar autorizações do IAM com base nos critérios a seguir:

* Usuários individuais
* Grupos de acesso (grupos de usuários)
* Tipos específicos de recursos
* Grupos de Recursos

Para saber mais sobre o IAM, consulte as informações a seguir:

* [Introdução ao IAM](https://cloud.ibm.com/docs/iam?topic=iam-getstarted#getstarted)
* [Conceitos do IAM](https://cloud.ibm.com/docs/iam?topic=iam-iamoverview)
* [Gerenciando grupos de recursos](https://cloud.ibm.com/docs/resources?topic=resources-rgs)
* [Configurando grupos de acesso](https://cloud.ibm.com/docs/iam?topic=iam-groups)

## Funções de acesso de plataforma
{: #platform-access-roles}

É possível usar funções de acesso de plataforma para permitir que os usuários concluam tarefas em recursos do {{site.data.keyword.cloud_notm}}, como a criação de usuários ou a inclusão de serviços.

A tabela a seguir exibe as funções de acesso de plataforma do IAM e o tipo correspondente de controle permitido pelo {{site.data.keyword.powerSys_notm}}:

| Função de acesso de plataforma | Tipo de acesso permitido |
|-----------|-------------------------|
| Visualizador | Visualizar e listar instâncias. |
| Operador | Visualizar e listar instâncias. |
| Aplicativos | Visualizar, listar, criar e excluir instâncias.  |
| Administrador | Visualizar, listar, criar, excluir e designar políticas a outros usuários. |

## Funções de acesso de serviço
{: #service-access-roles}

É possível usar as funções de acesso de serviço para definir o que os usuários podem fazer com as funções de serviço do {{site.data.keyword.powerSys_notm}}.

A tabela a seguir exibe as funções de acesso de serviço do IAM e as ações correspondentes que podem ser concluídas por um usuário com o {{site.data.keyword.powerSys_notm}}:

| Função de acesso de serviço | Descrição das ações |
|-----------|-------------------------|
| Leitor | Visualizar todos os recursos, como chaves SSH, volumes de armazenamento e configurações de rede. Não é possível fazer mudanças nos recursos. |
| Gerenciador | É possível configurar todos os recursos. Consulte a seguir algumas das ações que podem ser executadas:<ul><li>Criar instâncias</li><li>Aumentar o tamanho do volume de armazenamento</li><li>Criar chaves SSH</li><li>Modificar configurações de rede</li><li>Criar imagens de inicialização</li><li>Excluir volumes de armazenamento</li>
</ul>

## Cenários de acesso de usuário
{: #user-access-scenarios}

Os cenários de acesso a seguir abrangem as etapas necessárias para incluir um novo usuário e modificar as permissões para um usuário existente.

### Convidando um novo usuário para visualizar recursos do {{site.data.keyword.powerSys_notm}}
{: #inviting-a-new-user-to-create-or-manage-resources}

Um convite para sua conta deve ser realizado a um usuário do IBM Cloud e o acesso de visualização dos recursos do {{site.data.keyword.powerSys_notm}} deve ser fornecido. Lembre-se, a função de acesso de serviço determina o nível de acesso que um usuário tem aos recursos do {{site.data.keyword.powerSys_notm}}.

Conclua as etapas a seguir no IAM para permitir que um usuário visualize os recursos do {{site.data.keyword.powerSys_notm}}:

1. Navegue até a [IU dos usuários do IAM ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/iam/users){: new_window} no console do IBM Cloud e clique em **Convidar usuários**.

      ![Exibe o ícone Convidar usuários na IU do IAM](/images/invite_users.png "Convidando usuários na IU do IAM")

2. Na seção **Usuários**, insira os endereços de e-mail do usuário desejados no campo **Endereço de e-mail**.
3. Em seguida, selecione **Recurso** no campo **Designar acesso a** e **{{site.data.keyword.powerSys_notm}}** no campo **Serviços**.

    ![Exibe os campos de serviço](/images/invite_users2.png "Selecionando o serviço {{site.data.keyword.powerSys_notm}} para um novo usuário na IU do IAM")

4. Selecione a função de acesso à plataforma que você deseja designar aos usuários. Neste cenário, o usuário pode visualizar somente os recursos do {{site.data.keyword.cloud_notm}} e do {{site.data.keyword.powerSys_notm}}.

    ![Exibe a IU para funções do IAM](/images/invite_users3.png "Selecionando funções para um novo usuário na IU do IAM")

5. Clique em **Convidar usuários**. O usuário deve aceitar o convite para ser incluído na conta. Se o convite for enviado com sucesso, uma mensagem será exibida.

    ![Exibe uma mensagem para um convite bem-sucedido](/images/invite_users4.png "Mensagem de convite bem-sucedido")

### Fornecendo permissão a um usuário existente para gerenciar recursos do {{site.data.keyword.powerSys_notm}}
{: #giving-an-existing-user-permission-to-manage-resources}

Conclua as etapas a seguir para fornecer permissão a um usuário existente na sua conta para configurar recursos do {{site.data.keyword.powerSys_notm}}.

1. Navegue para a [IU de usuários do IAM ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/iam/users){: new_window} no IBM Cloud Console.
2. Na lista de usuários, selecione o usuário cuja autorização deseja mudar.
3. Clique em **Políticas de acesso** e clique nas funções atuais dos usuários. Neste cenário, clique em **Visualizador, leitor**.

    ![Exibe como mudar as permissões de um usuário existente](/images/existing_user1.png "Mudando as permissões de um usuário na IU do IAM")

4. No campo **Selecionar funções**, clique em **Gerenciador**. É possível manter a função **Leitor** selecionada.

    ![Exibe como incluir a função de gerenciador para um usuário existente](/images/existing_user2.png "Selecionando a função de gerenciador na IU do IAM")

5. Clique em **Salvar**.

   Agora, o usuário está autorizado a configurar os recursos do {{site.data.keyword.powerSys_notm}}. No entanto, esse usuário não pode gerenciar serviços e recursos específicos da plataforma {{site.data.keyword.cloud_notm}}. Por exemplo, ele não pode incluir novos usuários.
   {: note}
