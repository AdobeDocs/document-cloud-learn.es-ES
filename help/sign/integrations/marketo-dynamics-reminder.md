---
title: Enviar recordatorios con Acrobat Sign para Microsoft Dynamics 365 y Marketo
description: Obtenga información sobre cómo enviar un recordatorio por correo electrónico cuando un acuerdo permanece sin firmar después de un período de tiempo
role: Admin
solution: Acrobat Sign, Marketo, Document Cloud
level: Intermediate
topic: Integrations
topic-revisit: Integrations
jira: KT-7250
thumbnail: KT-7250.jpg
exl-id: 5a97fade-18a3-448a-8504-efb9e38e9187
source-git-commit: ad54f7afa78b0fbb31eccf455723a8890cb92355
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 2%

---

# Enviar recordatorios con Acrobat Sign para Microsoft Dynamics 365 y Marketo

Obtenga información sobre cómo enviar un recordatorio por correo electrónico cuando un acuerdo permanece sin firmar después de un período de tiempo. Esta integración utiliza Acrobat Sign, Acrobat Sign para Microsoft Dynamics, Marketo y Marketo Microsoft Dynamics Sync.

## Requisitos previos

1. Instale Marketo Microsoft Dynamics Sync.

   Dispone de información y del plugin más reciente para Microsoft Dynamics Sync [aquí.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/marketo-plugin-releases-for-microsoft-dynamics.html)

1. Instalar [Acrobat Sign para Microsoft Dynamics](https://appsource.microsoft.com/es-es/product/dynamics-365/adobesign.f3b856fc-a427-4d47-ad4b-d5d1baba6f86).

   Información sobre este plugin está disponible [aquí.](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)

## Buscar el objeto personalizado

Una vez completadas las configuraciones de Marketo Microsoft Dynamics Sync y Acrobat Sign para Dynamics , aparecen dos nuevas opciones en el Terminal de administración de Marketo.

![Administrador](assets/adminTerminal.png)

1. Haga clic en **[!UICONTROL Sincronización de entidades de Dynamics]**.

   La sincronización debe desactivarse antes de sincronizar entidades personalizadas. Haga clic en **Sincronizar esquema** si es tu primera vez. De lo contrario, haga clic en **Actualizar esquema**.

   ![Actualizar](assets/refreshSchema.png)

## Sincronizar el objeto personalizado

1. En el lado derecho, localice [!UICONTROL Plomo], [!UICONTROL Contacto]y [!UICONTROL Cuenta]objetos personalizados basados en el usuario.

   * **Habilitar sincronización** para los objetos bajo **[!UICONTROL Plomo]** si desea enviar un recordatorio cuando un [!UICONTROL Plomo] no ha firmado ningún acuerdo en Dynamics.

   * **Habilitar sincronización** para los objetos bajo **[!UICONTROL Contacto]** si desea enviar un recordatorio cuando un [!UICONTROL Contacto] no ha firmado ningún acuerdo en Dynamics.

   * **Habilitar sincronización** para los objetos bajo **[!UICONTROL Cuenta]** si desea enviar un recordatorio cuando un [!UICONTROL Cuenta] no ha firmado ningún acuerdo en Dynamics.

   * **Habilitar sincronización** para el objeto de acuerdo en la **[!UICONTROL Principal]** ([!UICONTROL Plomo], [!UICONTROL Contacto], o [!UICONTROL Cuenta]).

   ![Objetos personalizados](assets/enableSyncDynamics.png)

1. En la nueva ventana, seleccione las propiedades que desee en Acuerdo y, a continuación, active las casillas de **Restricción** y **Desencadenador** para exponerlos a sus actividades de marketing.

   ![Sincronización personalizada 1](assets/entitySync1.png)

   ![Sincronización personalizada 2](assets/entitySync2.png)

1. Vuelva a activar la sincronización después de activar la sincronización en los objetos personalizados.

   Vuelva a Terminal de administración y haga clic en **Microsoft Dynamics** y, a continuación, haga clic en **Habilitar sincronización**.

   ![Microsoft Dynamics](assets/microsoftDynamics.png)

   ![Habilitar global](assets/enableGlobalDynamics.png)

## Crear el programa y el token

1. En la sección Actividades de marketing de Marketo, haga clic con el botón derecho en **Actividades de marketing** en la barra izquierda.

   Seleccionar **Nueva carpeta de campaña** y ponle un nombre.

   ![Nueva carpeta](assets/newFolder.png)

1. Haga clic con el botón derecho en la carpeta creada y seleccione **Nuevo programa** y ponle un nombre.

   Deje todo lo demás como predeterminado y, a continuación, haga clic en **Crear**.

   ![Nuevo programa 1](assets/newProgram1.png)

   ![Nuevo programa 2](assets/newProgram2.png)

1. Haga clic en **Mis tokens**, y arrastre **Script de correo electrónico** al lienzo.

   ![Script de correo electrónico](assets/emailScript.png)

1. Asigne un nombre y, a continuación, haga clic en **Haga clic para editar**.

   ![Nombre y edición](assets/nameAndSave.png)

1. Expandir **[!UICONTROL Objetos personalizados]** en el lado derecho y, a continuación, expanda el **[!UICONTROL Acuerdo]** objeto.

   Buscar y arrastrar [!UICONTROL Nombre], Estado del acuerdo, Enviado el y URL del firmante actual en el lienzo.

1. Escriba un script de velocidad usando estos tokens para mostrar la URL de acuerdo de un acuerdo que no se firme durante una semana. A continuación se muestra un ejemplo que compara la fecha actual con la fecha de envío:

   ```
   #foreach($agreement in $adobe_agreementList)
       #if($agreement.adobe_esagreementstatus == "Out for Signature")
           #set($todayCalObj = $date.toCalendar($date.toDate("yyyy-MM-dd",$date.get('yyyy-MM-dd'))) )
           #set($dateSentCalObj = $date.toCalendar($date.toDate("yyyy-MM-dd",$agreement.adobe_datesent)) )
           #set($dateDiff = ($todayCalObj.getTimeInMillis() - $dateSentCalObj.getTimeInMillis()) / 86400000 )
   
           #if($dateDiff >= 7)
               #set($agreementName = $agreement.adobe_name)
               #set($agreementURL = $agreement.adobe_currentsignerurl.substring(8))
               #break
           #else
           #end
       #else
       #end
   #end
   
   #if(${agreementName})
       <a href="https://${agreementURL}">${agreementName}</a>
   #else
       Please contact us. 
   #end
   ```

1. Haga clic en **[!UICONTROL Guardar]**.

## Crear el recordatorio y añadir personalización

Algunos ejemplos de personalización son: el nombre del firmante, el nombre del acuerdo, un vínculo al acuerdo, etc.

1. Haga clic con el botón derecho en el programa que ha creado y haga clic en **[!UICONTROL Nuevo activo local]**, luego seleccione **[!UICONTROL Correo electrónico]**.

   ![Nuevo correo electrónico](assets/createNewEmail.png)

1. En la nueva pestaña, introduzca un **[!UICONTROL Nombre]** y **[!UICONTROL Descripción]** para el correo electrónico y seleccione una plantilla en el selector de plantillas.

   ![Selector de plantilla](assets/templatePicker.png)

1. Haga clic en **[!UICONTROL Crear]**.

1. Establezca el **[!UICONTROL Nombre de origen]** y **[!UICONTROL Dirección de origen]**.

   ![Correo electrónico recordatorio](assets/reminderEmail.png)

1. Haga clic en el cuerpo del mensaje para activar el editor.

   Haga clic en el **[!UICONTROL Insertar token]** , busque el token de URL del acuerdo personalizado que ha creado y, a continuación, haga clic en **[!UICONTROL Insertar]**. Termina de personalizar tu correo electrónico y haz clic en **[!UICONTROL Guardar]**.

   ![Insertar token](assets/insertToken.png)

1. Previsualice mediante un perfil que tenga un acuerdo asignado.

   Debería ver un vínculo a la dirección URL con el nombre del acuerdo como etiqueta.

   ![Vínculo de correo electrónico](assets/emailLink.png)

## Configurar el filtro de Smart Campaign

1. Haga clic con el botón derecho en el programa que creó y, a continuación, haga clic en **[!UICONTROL Nueva campaña inteligente]**.

   ![Smart Campaign 1](assets/smartCampaign1.png)

1. Asigne un nombre a su elección y, a continuación, haga clic en **[!UICONTROL Crear]**.

   ![Smart Campaign 2](assets/smartCampaign2.png)

1. Busque y, a continuación, haga clic y arrastre **[!UICONTROL Tiene acuerdo]** a la lista inteligente.

   ![Tiene acuerdo](assets/hasAgreementDynamics1.png)

   Los campos que expuso al activador deben estar disponibles en **[!UICONTROL Agregar restricción]**.

1. Seleccionar **[!UICONTROL Estado del acuerdo]** y cualquier otro campo por el que desee filtrar.

   Para cada campo añadido, defina los valores por los que filtrar. En este caso, solo se activa cuando el **[!UICONTROL Estado del acuerdo]** es *Enviado para firmar* y **[!UICONTROL Enviado el]** es *en el pasado antes de 1 semana*.

   ![Estado del acuerdo](assets/hasAgreementDynaSentOn.png)

   >[!NOTE]
   >
   > Agregue un identificador único a las restricciones, como **Nombre**, si desea que esta campaña se ejecute solo para determinados acuerdos.

1. Confirma el público de la campaña y comprueba quién cumple los requisitos en la pestaña Programación.

   ![Cualificadores](assets/qualifiers.png)

## Configurar el flujo de campaña inteligente

Porque el filtro de campaña **Días hasta que caduque** , puede utilizar una periodicidad programada para la campaña.

1. Haga clic en **[!UICONTROL Flujo]** en la pestaña [!UICONTROL Smart Campaign].

   Busque y arrastre el **Enviar correo electrónico** en el lienzo y seleccione el correo electrónico de recordatorio que creó en la sección anterior.

   ![Enviar correo electrónico](assets/sendEmail.png)

1. Haga clic en **[!UICONTROL Programación]** de la Campaña inteligente. Asegúrese de que el flujo de la campaña esté limitado a ejecutarse solo una vez por persona en el **Configuración inteligente de campañas**. A continuación, haga clic en el **Programar periodicidad** .

   ![Ficha Programación](assets/scheduleTab.png)

1. Establezca el **Programación** para _Diario_. Elija un día de inicio y una fecha de finalización para la campaña, si es necesario.

   ![Configuración de programación](assets/scheduleSettings.png)

>[!TIP]
>
>Este tutorial forma parte del curso [Agiliza los ciclos de ventas con Acrobat Sign para Microsoft Dynamics y Marketo](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) que está disponible de forma gratuita en el Experience League!