---

copyright:
  years: 2016, 2019
lastupdated: "2019-05-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:important: .important}
{:note: .note}

# Sucesos de Activity Tracker del {{site.data.keyword.powerSys_notm}}
{: #at_events}

Como responsable de seguridad, auditor o directivo, puede utilizar el servicio Activity Tracker para realizar un seguimiento de cómo interactúan los usuarios y las aplicaciones con el servicio {{site.data.keyword.powerSys_notm}} en {{site.data.keyword.cloud}}.
{:shortdesc}

{{site.data.keyword.at_full_notm}} registra las actividades iniciadas por el usuario que han cambiado el estado de un servicio en {{site.data.keyword.cloud_notm}}. Puede utilizar este servicio para investigar las acciones graves y de actividad anormal y también para cumplir con los requisitos de auditoría de regulación. Además, puede recibir alertas sobre las acciones mientras se producen. Los sucesos que se recopilan cumplen con la normativa de Cloud Auditing Data Federation (CADF). [Más información](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started).

## Lista de sucesos: Lectura
{: #at_actions_read}

El suceso siguiente se utiliza para leer la instancia del {{site.data.keyword.powerSys_notm}}.

| Acción                     | Descripción                     |
|:---------------------------|:--------------------------------|
| pcloud.cloud-instance.read | Leer instancia de Power Cloud     |


## Lista de sucesos: Imágenes
{: #at_actions_images}

Los sucesos siguientes son para trabajar con imágenes en la instancia del {{site.data.keyword.powerSys_notm}}.

| Acción                     | Descripción                     |
|:---------------------------|:--------------------------------|
| pcloud.image.read          | Leer una imagen o todas las imágenes     |
| pcloud.image.create        | Crear una imagen nueva              |
| pcloud.image.update        | Actualizar una imagen                 |
| pcloud.image.delete        | Suprimir una imagen                 |
| pcloud.image.capture       | Exportar una imagen                |


## Lista de sucesos: Redes
{: #at_actions_networks}

Los sucesos siguientes son para trabajar con redes en la instancia del {{site.data.keyword.powerSys_notm}}.

| Acción                     | Descripción                           |
|:---------------------------|:--------------------------------------|
| pcloud.network.read        | Leer una red o todas las redes        |
| pcloud.network.create      | Crear una red nueva (pública/privada) |
| pcloud.network.update      | Actualizar una red                      |
| pcloud.network.delete      | Suprimir una red                      |
{: caption="Tabla 3. Acciones que generan sucesos" caption-side="top"}

## Lista de sucesos: {{site.data.keyword.powerSys_notm}}
{: #at_actions_virtual_servers}

Los sucesos siguientes son para trabajar con cada servidor virtual en la instancia del {{site.data.keyword.powerSys_notm}}.

| Acción                        | Descripción                          |
|:------------------------------|:-------------------------------------|
| pcloud.pvm-instance.read      | Leer una instancia del servidor virtual de Power                  |
| pcloud.pvm-instance.create    | Crear una instancia del servidor virtual de Power                |
| pcloud.pvm-instance.update    | Actualizar una instancia del servidor virtual de Power                |
| pcloud.pvm-instance.delete    | Suprimir una instancia del servidor virtual de Power                |
| pcloud.pvm-instance.start     | Iniciar una instancia del servidor virtual de Power                 |
| pcloud.pvm-instance.stop      | Detener una instancia del servidor virtual de Power                  |
| pcloud.pvm-instance.renew     | Reiniciar una instancia del servidor virtual de Power                |
| pcloud.pvm-instance.unknown   | Acción desconocida en instancia serv. virtual de Power     |
| pcloud.pvm-instance.monitor   | Acceso a consola en instancia servidor virtual Power     |
| pcloud.pvm-instance.capture   | Capturar instancia serv. virtual Power en una imagen |

## Lista de sucesos: claves SSH
{: #at_actions_ssh_keys}

Los sucesos siguientes son para trabajar con claves de cuenta y SSH en la instancia del {{site.data.keyword.powerSys_notm}}.

| Acción                   | Descripción                 |
|:-------------------------|:----------------------------|
| pcloud.tenant.read       | Leer la información de arrendatario       |
| pcloud.ssh-key.read      | Leer una clave SSH o varias   |
| pcloud.ssh-key.create    | Crear una clave SSH            |
| pcloud.ssh-key.update    | Actualizar una clave SSH           |
| pcloud.ssh-key.delete    | Suprimir una clave SSH           |

## Lista de sucesos: Volúmenes de datos
{: #at_actions_data_volumes}

Los sucesos siguientes son para trabajar con volúmenes de datos en la instancia del {{site.data.keyword.powerSys_notm}}.

| Acción                   | Descripción                 |
|:-------------------------|:----------------------------|
| pcloud.volume.read       | Leer un volumen o varios    |
| pcloud.volume.create     | Crear un volumen            |
| pcloud.volume.update     | Actualizar un volumen            |
| pcloud.volume.delete     | Suprimir un volumen            |
| pcloud.volume.configure  | Conectar o desconectar un volumen   |

## Visualización de sucesos
{: #at_ui}

Los sucesos están disponibles en la ubicación de **Dallas**.

{{site.data.keyword.at_full_notm}} solamente puede tener una instancia por ubicación. Para ver los sucesos, debe acceder a la interfaz de usuario web del servicio {{site.data.keyword.at_full_notm}} en la ubicación `us-south`. [Más información](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-launch#launch_step2).
