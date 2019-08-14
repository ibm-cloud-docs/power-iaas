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

# Gestión de recursos y usuarios del {{site.data.keyword.powerSys_notm}}
{: #managing-resources-and-users}

La gestión de recursos y la autorización del {{site.data.keyword.powerSysFull}} se coordina con los servicios de IBM Cloud Identity and Access Management (IAM). Gracias a IAM podrá autenticar usuarios de forma segura, controlar el acceso a los recursos del {{site.data.keyword.powerSys_notm}} con los grupos de recursos y podrá acceder a recursos específicos para un conjunto de usuarios con grupos de acceso. En otras palabras, IAM es su tienda única para la gestión de todos los usuarios y recursos en {{site.data.keyword.cloud_notm}}.
{: shortdesc}

Puede asignar las autorizaciones de IAM en función de los criterios siguientes:

* Usuarios individuales
* Grupos de acceso (grupos de usuarios)
* Tipos específicos de recursos
* Grupos de recursos

Para obtener más información sobre IAM, consulte la información siguiente:

* [Iniciación a IAM](https://cloud.ibm.com/docs/iam?topic=iam-getstarted#getstarted)
* [Conceptos de IAM](https://cloud.ibm.com/docs/iam?topic=iam-iamoverview)
* [Gestión de grupos de recursos](https://cloud.ibm.com/docs/resources?topic=resources-rgs)
* [Configuración de grupos de acceso](https://cloud.ibm.com/docs/iam?topic=iam-groups)

## Roles de acceso a la plataforma
{: #platform-access-roles}

Puede utilizar los roles de acceso a la plataforma para permitir que los usuarios lleven a cabo tareas en los recursos de {{site.data.keyword.cloud_notm}} como, por ejemplo, la creación de usuarios o la adición de servicios.

En la tabla siguiente se muestran los roles de acceso a la plataforma de IAM así como el tipo correspondiente de control que permite el {{site.data.keyword.powerSys_notm}}:

| Rol acceso plataforma | Tipo acceso permitido |
|-----------|-------------------------|
| Visor | Visualiza instancias y lista instancias. |
| Operador | Visualiza instancias y lista instancias. |
| Editor | Visualiza instancia, lista instancias, crea instancias y suprime instancias.  |
| Administrador | Visualiza instancias, lista instancias, crea instancias, suprime instancias y asigna políticas a otros usuarios. |

## Roles de acceso al servicio
{: #service-access-roles}

Puede utilizar los roles de acceso al servicio para definir los que los usuarios pueden hacer con las funciones del servicio {{site.data.keyword.powerSys_notm}}.

En la tabla siguiente se muestran los roles de acceso al servicio de IAM y las acciones correspondientes que puede llevar a cabo un usuario con el {{site.data.keyword.powerSys_notm}}:

| Rol de acceso al servicio | Descripción de acciones |
|-----------|-------------------------|
| Lector | Visualiza todos los roles como, por ejemplo, las claves SSH, los volúmenes de almacenamiento y los valores de red. No puede realizar ningún cambio en los recursos. |
| Gestor | Puede configurar todos los recursos. A continuación se hallan algunas de las acciones que puede realizar:<ul><li>Crear instancias</li><li>Aumentar los tamaños de los volúmenes de almacenamiento</li><li>Crear claves SSH</li><li>Modificar valores de red</li><li>Crear imágenes de arranque</li><li>Suprimir volúmenes de almacenamiento</li>
</ul>

## Casos de ejemplo de acceso de usuario
{: #user-access-scenarios}

Los siguientes casos de ejemplo de acceso muestran los pasos que hay que seguir para añadir un usuario nuevo y modificar los permisos para un usuario existente.

### Invitación a un usuario nuevo para que vea los recursos del {{site.data.keyword.powerSys_notm}}
{: #inviting-a-new-user-to-create-or-manage-resources}

Debe invitar a un usuario de IBM Cloud a su cuenta y concederle acceso para que vea los recursos del {{site.data.keyword.powerSys_notm}}. Recuerde, el rol de acceso al servicio determina el nivel de acceso que tiene un usuario para los recursos del {{site.data.keyword.powerSys_notm}}.

Lleve a cabo los pasos siguientes en IAM para que un usuario pueda ver los recursos del {{site.data.keyword.powerSys_notm}}:

1. Vaya hasta la [IU de los usuarios de IAM ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/iam/users){: new_window} en la consola de IBM Cloud y pulse **Invitar a usuarios**.

      ![Muestra el icono de Invitar a usuarios desde la IU de IAM](/images/invite_users.png "Invitación de usuarios desde la IU de IAM")

2. Bajo la sección **Usuarios**, escriba las direcciones de correo electrónico que desee en el campo **Dirección de correo electrónico**.
3. A continuación, seleccione **Recurso** del campo **Asignar acceso a** y **{{site.data.keyword.powerSys_notm}}** en el campo **Servicios**.

    ![Muestra los campos de servicio](/images/invite_users2.png "Selección del servicio {{site.data.keyword.powerSys_notm}} para un usuario nuevo desde la IU de IAM")

4. Seleccione el rol de acceso de la plataforma que desea asignar a los usuarios. En este caso de ejemplo, el usuario sólo puede ver los recursos de {{site.data.keyword.cloud_notm}} y del {{site.data.keyword.powerSys_notm}}.

    ![Muestra la IU para los roles de IAM](/images/invite_users3.png "Selección de roles para un usuario nuevo desde la IU de IAM")

5. Pulse **Invitar a usuarios**. El usuario debe aceptar la invitación para poderlo añadir en la cuenta. Si la invitación se envía correctamente, se visualizará un mensaje.

    ![Muestra el mensaje que indica que la invitación se ha enviado correctamente](/images/invite_users4.png "Mensaje de invitación correcta")

### Cómo otorgar un permiso de usuario existente para gestionar los recursos del {{site.data.keyword.powerSys_notm}}
{: #giving-an-existing-user-permission-to-manage-resources}

Lleve a cabo los pasos siguientes para proporcionar permiso a su cuenta a un usuario existente con el fin que configure los recursos del
{{site.data.keyword.powerSys_notm}}.

1. Vaya hasta la [IU de usuarios de IAM ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/iam/users){: new_window} en la consola de IBM Cloud.
2. Desde la lista de usuarios, seleccione el usuario cuya autorización desee cambiar.
3. Pulse **Políticas de acceso** y pulse los roles actuales de los usuarios. En este caso de ejemplo, pulse **Visor, Lector**.

    ![Muestra cómo se cambian los permisos para un usuario existente](/images/existing_user1.png "Cambio de los permisos para un usuario desde la IU de IAM")

4. Desde el campo **Seleccionar roles**, pulse **Gestor**. Puede dejar el rol **Lector** seleccionado.

    ![Muestra la adición del rol de gestor para un usuario existente](/images/existing_user2.png "Selección del rol de gestor desde la IU de IAM")

5. Pulse **Guardar**.

   Ahora el usuario dispone de autorización para configurar los recursos del {{site.data.keyword.powerSys_notm}}. Sin embargo, este usuario no puede gestionar servicios y recursos que sean específicos de la plataforma de {{site.data.keyword.cloud_notm}}. Por ejemplo, no pueden añadir usuarios nuevos.
   {: note}
