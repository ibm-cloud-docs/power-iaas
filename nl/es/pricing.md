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

# Fijación de precios para el servidor virtual de Power Systems en IBM Cloud
{: #pricing-virtual-server}

{{site.data.keyword.powerSysFull}} se ofrece en regiones seleccionadas con particiones lógicas
(LPAR) a escala de hasta 15 núcleos y 320 GB de memoria y también con LPAR de empresa de hasta 143 núcleos y 8192 GB de memoria. Con estas opciones, un {{site.data.keyword.powerSys_notm}} puede cumplir cualquier requisito de carga de trabajo de su empresa. Se le facturará una tarifa mensual.
{:shortdesc}

## Uso mensual
{: #pricing-monthly-usage}

Las instancias del {{site.data.keyword.powerSys_notm}} se cargan en una tarifa mensual que se prorratea por hora. Si añade recursos a una LPAR a mitad de mes, la factura mensual de la LPAR reflejará el cambio de recursos y el precio de la LPAR se prorrateará por hora.

### Ejemplo de uso mensual
{: #pricing-monthly-usage-example}

En el ejemplo siguiente, adquirimos una instancia del {{site.data.keyword.powerSys_notm}} que tiene 1 núcleo con 8 GB de memoria, 150 GB de disco y ejecuta AIX 7200-03-02, con un precio base de 250,57 dólares al mes (0,343 dólares por hora). A medida que avanza el mes, se añade más memoria. El nuevo precio de la LPAR es de 339,45 dólares al mes (0,465 dólares por hora). La factura mensual se prorratea por hora en función de los recursos desplegados.

| Horas transcurridas al mes       | Importe cargado   |  Descripción de la LPAR     |
| ----------------------------- | ----------------- | --------------------  |
| 300 horas        | 300 horas x 251$/mes = 103$  | 1 núcleo, 8 GB de memoria, 150 GB de disco, AIX    |
| 430 horas        | 430 horas x 339$/mes = 200$  | 1 núcleo, 16 GB de memoria, 150 GB de disco, AIX  |
| 730 horas (total mensual)  | 103$ + 200$ = 303$ (total mensual)  |   1 núcleo, 16 GB de memoria, 150 GB de disco, AIX |
{: caption="Tabla 1. Ejemplo de cargos mensuales de la LPAR" caption-side="top"}

En este ejemplo, los recursos de la LPAR aumentan después de 300 horas del mes, pasando de 8 GB de memoria a 16 GB. El precio de la LPAR se prorratea por hora en función del precio mensual final de la LPAR (303$).

## Precios de instancia de base
{: #pricing-base-instance-prices}

La facturación de instancia de base depende de las opciones como, por ejemplo, del tipo de máquina, el número de núcleos y la cantidad de memoria que se selecciona cuando se crea un {{site.data.keyword.powerSys_notm}}. Cuando se crea la instancia de su servidor virtual, se visualiza la tarifa mensual asociada. Para obtener más información, consulte [Creación de un {{site.data.keyword.powerSys_notm}}](/docs/infrastructure/power-iaas?topic=power-iaas-creating-power-virtual-server#creating-power-virtual-server).

## Sistemas operativos
{: #pricing-operating-systems}

A continuación se indican las imágenes en stock que IBM proporciona:
* AIX
  * 7200-03-02
  * 7100-05-03

* IBM i
  * 7.3 TR5
  * 7.2 TR9

Puede incorporar su propia imagen personalizada para utilizarla en una instancia del {{site.data.keyword.powerSys_notm}} pero igualmente debe comprar una licencia del sistema operativo para IBM Cloud. No es posible utilizar una licencia existente de AIX o IBM i para las LPAR en una instancia del {{site.data.keyword.powerSys_notm}}. Si utiliza una imagen personalizada o una imagen en stock, se le cargará el mismo precio. Para obtener más información, consulte [Configuración de una imagen personalizada](/docs/infrastructure/power-iaas?topic=power-iaas-configuring-custom-image#configuring-custom-image).

## Fin de la facturación
{: #pricing-end-of-billing}

El ciclo de facturación mensual termina cuando se suprime la LPAR. Si se escala la infraestructura aumentándola y reduciéndola como respuesta a los requisitos de carga de trabajo, la facturación seguirá la temporización del cambio de provisión de la LPAR. Si detiene la LPAR, el proceso de facturación no se detiene. Debe suprimir la LPAR para detener el ciclo de facturación.
