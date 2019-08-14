---

copyright:
  years: 2019

lastupdated: "2019-06-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}

# Precificação para o servidor virtual Power Systems no IBM Cloud
{: #pricing-virtual-server}

O {{site.data.keyword.powerSysFull}} é oferecido em regiões selecionadas com partições lógicas de ampliação (LPAR) de até 15 núcleos e 320 GB de memória e com LPARs corporativas de até 143 núcleos e 8192 GB de memória. Com essas opções, o {{site.data.keyword.powerSys_notm}} pode atender a quaisquer requisitos de carga de trabalho de seus negócios. O faturamento ocorre com base em uma taxa mensal.
{:shortdesc}

## Uso mensal
{: #pricing-monthly-usage}

As instâncias do {{site.data.keyword.powerSys_notm}} são cobradas com base em uma taxa mensal rateada por hora. Se você incluir recursos em uma LPAR no meio de um mês, a fatura mensal para a LPAR refletirá a mudança de recurso e o preço da LPAR rateado por hora.

### Exemplo de uso mensal
{: #pricing-monthly-usage-example}

No exemplo a seguir, você adquire uma instância do {{site.data.keyword.powerSys_notm}} que possui 1 núcleo com 8 GB de memória, um disco de 150 GB e está executando o AIX 7200-03-02 com um preço base de US$ 250,57 por mês (US$ 0,343 por hora). Ao longo do mês, você inclui mais memória. O novo preço para a LPAR é US$ 339,45 por mês (US$ 0,465 por hora). A fatura mensal é rateada por hora para os recursos implementados.

| Horas decorridas em um mês       | Quantia cobrada   |  Descrição da LPAR     |
| ----------------------------- | ----------------- | --------------------  |
| 300 horas        | 300 horas x US$ 251/mês = US$ 103  | 1 núcleo, 8 GB de memória, disco de 150 GB, AIX    |
| 430 horas        | 430 horas x US$ 339/mês = US$ 200  | 1 núcleo, 16 GB de memória, disco de 150 GB, AIX  |
| 730 horas (total mensal)  | US$ 103 + US$ 200 = US$ 303 (total mensal)  |   1 núcleo, 16 GB de memória, disco de 150 GB, AIX |
{: caption="Tabela 1. Exemplo de encargos mensais de LPAR" caption-side="top"}

Neste exemplo, os recursos da LPAR são aumentados de 8 GB para 16 GB de memória após a hora 300 do mês. O preço da LPAR é rateado por hora para o preço mensal final da LPAR (US$ 303).

## Preços de instância de base
{: #pricing-base-instance-prices}

O faturamento da instância base depende das opções, como o tipo de máquina, o número de núcleos e a quantia de memória, selecionadas ao criar um {{site.data.keyword.powerSys_notm}}. Ao criar sua instância de servidor virtual, a taxa mensal associada será exibida. Para obter mais informações, consulte [Criando um {{site.data.keyword.powerSys_notm}}](/docs/infrastructure/power-iaas?topic=power-iaas-creating-power-virtual-server#creating-power-virtual-server).

## Sistemas operacionais
{: #pricing-operating-systems}

Consulte a seguir as imagens de estoque fornecidas a você pela IBM:
* AIX
  * 7200-03-02
  * 7100-05-03

* IBM i
  * 7.3 TR5
  * 7.2 TR9

É possível usar sua própria imagem customizada em uma instância do {{site.data.keyword.powerSys_notm}}, mas uma licença de sistema operacional ainda é comprada para o IBM Cloud. Não é possível usar uma licença existente do AIX ou do IBM i para LPARs em uma instância do {{site.data.keyword.powerSys_notm}}. O preço cobrado será igual para uma imagem customizada ou uma imagem de estoque. Para obter mais informações, consulte [Configurando uma imagem customizada](/docs/infrastructure/power-iaas?topic=power-iaas-configuring-custom-image#configuring-custom-image).

## Fim do faturamento
{: #pricing-end-of-billing}

O ciclo de faturamento mensal termina quando você exclui a LPAR. Se a capacidade de sua infraestrutura for aumentada ou reduzida em resposta aos requisitos de carga de trabalho, seu faturamento seguirá a sincronização da mudança de provisão da LPAR. Se você parar a LPAR, o processo de faturamento não será interrompido. Deve-se excluir a LPAR para parar o ciclo de faturamento.
