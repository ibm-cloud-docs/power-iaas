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

# Eventos do {{site.data.keyword.powerSys_notm}} Activity Tracker
{: #at_events}

Como um responsável pela segurança, auditor ou gerente, é possível usar o serviço Activity Tracker para rastrear como os usuários e aplicativos interagem com o serviço {{site.data.keyword.powerSys_notm}} no {{site.data.keyword.cloud}}.
{: shortdesc}

O {{site.data.keyword.at_full_notm}} registra atividades iniciadas pelo usuário que mudam o estado de um serviço no {{site.data.keyword.cloud_notm}}. É possível usar esse serviço para investigar atividade anormal e ações críticas e para obedecer aos requisitos de auditoria regulamentares. Além disso, é possível ser alertado sobre ações conforme elas acontecem. Os eventos que são coletados obedecem ao padrão Cloud Auditing Data Federation (CADF). [ Saiba mais ](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started).

## Lista de eventos: leitura
{: #at_actions_read}

O evento a seguir é usado para ler a instância do {{site.data.keyword.powerSys_notm}}.

| Ações                     | Descrição                     |
|:---------------------------|:--------------------------------|
| pcloud.cloud-instance.read | Ler uma instância da nuvem do Power     |


## Lista de eventos: imagens
{: #at_actions_images}

Os eventos a seguir são usados para trabalhar com imagens em sua instância do {{site.data.keyword.powerSys_notm}}.

| Ações                     | Descrição                     |
|:---------------------------|:--------------------------------|
| pcloud.image.read          | Ler uma ou todas as imagens     |
| pcloud.image.create        | Criar uma nova imagem              |
| pcloud.image.update        | Atualizar uma imagem                 |
| pcloud.image.delete        | Excluir uma imagem                 |
| pcloud.image.capture       | Exporta uma imagem                |


## Lista de eventos: redes
{: #at_actions_networks}

Os eventos a seguir são usados para trabalhar com redes em sua instância do {{site.data.keyword.powerSys_notm}}.

| Ações                     | Descrição                           |
|:---------------------------|:--------------------------------------|
| pcloud.network.read        | Ler uma ou todas as redes        |
| pcloud.network.create      | Criar uma nova rede (pública/privada) |
| pcloud.network.update      | Atualizar uma rede                      |
| pcloud.network.delete      | Excluir uma rede                      |
{: caption="Tabela 3. Ações que geram eventos" caption-side="top"}

## Lista de eventos: {{site.data.keyword.powerSys_notm}}
{: #at_actions_virtual_servers}

Os eventos a seguir são usados para trabalhar com cada servidor virtual dentro da instância do {{site.data.keyword.powerSys_notm}}.

| Ações                        | Descrição                          |
|:------------------------------|:-------------------------------------|
| pcloud.pvm-instance.read      | Ler uma instância de servidor virtual do Power                  |
| pcloud.pvm-instance.create    | Criar uma instância de servidor virtual do Power                |
| pcloud.pvm-instance.update    | Atualizar uma instância de servidor virtual do Power                |
| pcloud.pvm-instance.delete    | Excluir uma instância de servidor virtual do Power                |
| pcloud.pvm-instance.start     | Iniciar uma instância de servidor virtual do Power                 |
| pcloud.pvm-instance.stop      | Parar uma instância de servidor virtual do Power                  |
| pcloud.pvm-instance.renew     | Reinicializar uma instância de servidor virtual do Power                |
| pcloud.pvm-instance.unknown   | Ação desconhecida em uma instância de servidor virtual do Power     |
| pcloud.pvm-instance.monitor   | Acesso por meio do console a uma instância de servidor virtual do Power     |
| pcloud.pvm-instance.capture   | Capturar uma instância de servidor virtual do Power em uma imagem |

## Lista de eventos: chaves SSH
{: #at_actions_ssh_keys}

Os eventos a seguir são usados para trabalhar com contas e chaves SSH em sua instância do {{site.data.keyword.powerSys_notm}}.

| Ações                   | Descrição                 |
|:-------------------------|:----------------------------|
| pcloud.tenant.read       | Ler as informações de seu locatário       |
| pcloud.ssh-key.read      | Ler uma ou diversas chaves SSH   |
| pcloud.ssh-key.create    | Criar uma chave SSH            |
| pcloud.ssh-key.update    | Atualizar uma chave SSH           |
| pcloud.ssh-key.delete    | Excluir uma chave SSH           |

## Lista de eventos: volumes de dados
{: #at_actions_data_volumes}

Os eventos a seguir são usados para trabalhar com volumes de dados em sua instância do {{site.data.keyword.powerSys_notm}}.

| Ações                   | Descrição                 |
|:-------------------------|:----------------------------|
| pcloud.volume.read       | Ler um ou diversos volumes    |
| pcloud.volume.create     | Criar um volume            |
| pcloud.volume.update     | Atualizar um volume            |
| pcloud.volume.delete     | Excluir um volume            |
| pcloud.volume.configure  | Anexar ou remover um volume   |

## Visualizando eventos
{: #at_ui}

Os eventos estão disponíveis no local **Dallas**.

O {{site.data.keyword.at_full_notm}} pode ter apenas uma instância por local. Para visualizar eventos, deve-se acessar a IU da web do serviço {{site.data.keyword.at_full_notm}} no local `us-south`. [ Saiba mais ](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-launch#launch_step2).
