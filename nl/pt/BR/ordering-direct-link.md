---

copyright:
  years: 2019

lastupdated: "2019-07-30"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:download: .download}

# Solicitando o IBM Cloud Direct Link Connect para servidores virtuais Power Systems
{: #ordering-direct-link-connect}

Uma opção para configurar uma rede privada com o {{site.data.keyword.powerSys_notm}} é usar o serviço Direct Link Connect. O serviço Direct Connect Link cria uma conexão que permite acesso aos recursos do {{site.data.keyword.cloud}} por meio de sua instância do {{site.data.keyword.powerSys_notm}}. O serviço Direct Link Connect também é usado para conectar sua rede local à rede do IBM Cloud usando o IBM Cloud Virtual Router Appliance (VRA).
{:shortdesc}

É possível usar o console da IU do {{site.data.keyword.cloud_notm}} para solicitar o serviço Direct Link Connect. O Direct Link Connect é um serviço separado do serviço {{site.data.keyword.powerSys_notm}}. Para revisar os encargos do Direct Link Connect, consulte [Precificação do IBM Cloud Direct Link](/docs/infrastructure/direct-link?topic=direct-link-pricing-for-direct-link-connect).

A IBM recomenda solicitar uma segunda conexão do Direct Link Connect para fins de backup.

## Antes de começar
{: #before-direct-link-connect}

* Verifique se sua conta do {{site.data.keyword.cloud}} tem as autorizações corretas para solicitar o serviço Direct Link Connect.
* Entenda os conceitos básicos de rede do serviço Direct Link Connect revisando os tópicos a seguir:
    * [Conceitos do Direct Link Connect](/docs/infrastructure/direct-link?topic=direct-link-direct-link-connect-solution#direct-link-connect-solution)
    * [Detalhes do Direct Link Connect](/docs/infrastructure/direct-link?topic=direct-link-ibm-cloud-direct-link-connect-details)
    * [Limitações do Direct Link Connect](/docs/infrastructure/direct-link?topic=direct-link-known-limitations#ibm-cloud-direct-link-exchange-and-direct-link-connect-limitations)
    * [Limitações estritas em designações de IP](/docs/infrastructure/direct-link?topic=direct-link-configure-ibm-cloud-direct-link#strict-limitations-on-ip-assignments)

## Etapas para pedir o Direct Link Connect
{: #steps-to-order-direct-link-connect}

Para solicitar o serviço Direct Link Connect que cria uma conexão com a instância do {{site.data.keyword.powerSys_notm}}, conclua as etapas a seguir:

1. Efetue login no [catálogo do IBM Cloud ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/catalog){: new_window} com as credenciais de sua conta do IBM Cloud. Sua conta deve ter a autorização correta para solicitar o serviço Direct Link Connect.

2. Na seção **Redes**, clique no quadro **Direct Link Connect**.
![Exibe o quadro do catálogo do Direct Link](/images/directlink1.png "Exibe o quadro do catálogo do Direct Link")

1. Na entrada do catálogo do Direct Link Connect, clique em **Criar**.

1. Na página do IBM Cloud Direct Link, clique em **Solicitar o Direct Link Connect**.

1. Na página Criar uma conexão do IBM Cloud Direct Link Connect, preencha os campos a seguir.

   À medida que você preenche os campos a seguir para criar o serviço Direct Link Connect, o preço é atualizado automaticamente para refletir suas seleções.
   {: note}

   <dl>
   <dt><strong>Nome da instância do Direct Link</strong><dt>
   <dd>Insira um nome que descreva o propósito do Direct Link Connect.</dd>
   <dt><strong>Local</strong><dt>
   <dd>Selecione o mesmo local da instância do {{site.data.keyword.powerSys_notm}}. A tabela a seguir identifica o local da instância do {{site.data.keyword.powerSys_notm}} e a opção correspondente do Direct Link Connection:
   <table>
   <caption>Tabela 1. Opções de local do Direct Link Connection</caption>
   <tr>
   <th>Local do servidor virtual Power Systems</th>
   <th>Local do Direct Link Connect</th>
   </tr>
   <tr>
   <td>Dallas, TX EUA</td>
   <td>Dallas 4</td>
   </tr>
   <tr>
   <td>Washington D.C., EUA</td>
   <td>Washington 2</td>
   </tr>
   </table>
   </dd>
   <dt><strong>Provedor de rede</strong><dt>
   <dd>Deve-se selecionar <strong>MEGAPORT</strong> na lista.</dd>
   <dt><strong>Velocidade do link</strong><dt>
   <dd>Selecione a velocidade do link para atender aos seus requisitos de carga de trabalho. A seleção recomendada para esse campo é 1000 Mbps.</dd>
   <dt><strong>Opção de roteamento</strong><dt>
   <dd>Selecione <strong>Roteamento local (grátis)</strong> para acessar todos os data centers conectados no local especificado no campo <strong>Local</strong>. Selecione <strong>Roteamento global</strong> para acessar todos os data centers do IBM Cloud no mundo. </dd>
   <dt><strong>BGP ASN</strong><dt>
   <dd>Deve-se inserir o número do BGP ASN para o local específico do Direct Link Connect na tabela a seguir.
   <table>
   <caption>Tabela 2. Número do BGP ASN para locais específicos</caption>
   <tr>
   <th>Local do Direct Link Connect</th>
   <th>Número do BGP ASN</th>
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
   <dt><strong>Selecionar VRF</strong><dt>
   <dd>Selecione a opção de encaminhamento e roteamento virtual para a conexão. Se sua conta não tiver um VRF identificado, esse campo não será exibido. Ainda será possível criar o serviço Direct Link Connect sem selecionar um VRF. A figura a seguir é um exemplo dos campos do Direct Link Connect.</dd>
   <dd>

   ![Exibe os campos preenchidos do Direct Link Connect](/images/directlink2.png "Exibe os campos preenchidos do Direct Link Connect")
   </dd>
   </dl>
2. Leia o **Contrato de serviço principal** e selecione a caixa de seleção. Deve-se ler e entender o **Contrato de serviço principal**, pois ele contém informações técnicas importantes.

3. Clique em **Criar**. A mensagem a seguir é exibida quando sua solicitação é enviada com sucesso.
![Exibe a mensagem de envio bem-sucedido do Direct Link Connect](/images/directlink3.png "Exibe a mensagem de envio bem-sucedido do Direct Link Connect")

1. Clique no link **Número do caso** para o serviço Direct Link Connect. As informações no número do caso são usadas para identificar as informações do Direct Link Connect para a conexão de sua instância do {{site.data.keyword.powerSys_notm}}.

  Pode levar ao suporte do IBM Cloud até três dias úteis para criar a conexão do Direct Link Connect.
  {: note}

2. Para criar uma conexão com a instância do {{site.data.keyword.powerSys_notm}} usando o serviço Direct Link Connect, abra um [novo caso](/docs/infrastructure/power-iaas?topic=power-iaas-getting-help-and-support) para a equipe de suporte do {{site.data.keyword.powerSys_notm}}.

      1. No campo de descrição do novo caso, inclua o número de caso do Direct Link Connect.
      2. Copie o ID de serviço do IAM do caso do {site.data.keyword.powerSys_notm}} gerado automaticamente pelo sistema.

3. Insira o ID de serviço do IAM do caso do {{site.data.keyword.powerSys_notm}} no caso do Direct Link Connect. Quando a conexão do Direct Link Connect é criada, o número do caso do Direct Link Connect é encerrado. Consulte a seguir um exemplo das informações de rede exibidas no caso:

  ```shell
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

1. Use essas informações do número do caso do Direct Link Connect e insira as informações de rede a seguir no caso do {{site.data.keyword.powerSys_notm}}:

  ```shell
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

1. O caso do {{site.data.keyword.powerSys_notm}} é encerrado quando a conexão do Direct Link Connect é configurada para se comunicar com sua instância do {{site.data.keyword.powerSys_notm}}.
