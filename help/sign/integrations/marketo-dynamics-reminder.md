---
title: Envío de recordatorios con Adobe Sign para Microsoft Dynamics 365 y Marketo
description: Obtenga más información sobre cómo enviar un recordatorio por correo electrónico cuando un acuerdo permanece sin firmar tras un período de tiempo
role: Admin
product: adobe sign
solution: Adobe Sign, Marketo, Document Cloud
level: Intermediate
topic-revisit: Integrations
thumbnail: KT-7250.jpg
exl-id: 5a97fade-18a3-448a-8504-efb9e38e9187
source-git-commit: bcddb0ee106239f2786debaed908b2a2ec5ce792
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 3%

---

# Envío de recordatorios con Adobe Sign para Microsoft Dynamics 365 y Marketo

Obtenga más información sobre cómo enviar un recordatorio por correo electrónico cuando un acuerdo permanece sin firmar después de un período de tiempo. Esta integración utiliza Adobe Sign, Adobe Sign para Microsoft Dynamics, Marketo y Marketo Microsoft Dynamics Sync.

## Requisitos previos

1. Instale Marketo Microsoft Dynamics Sync.

   La información y el último complemento para Microsoft Dynamics Sync están disponibles [aquí.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/marketo-plugin-releases-for-microsoft-dynamics.html)

1. Instale [Adobe Sign para Microsoft Dynamics](https://appsource.microsoft.com/es-es/product/dynamics-365/adobesign.f3b856fc-a427-4d47-ad4b-d5d1baba6f86).

   La información sobre este complemento está disponible [aquí.](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)

## Buscar el objeto personalizado

Una vez completadas las configuraciones de Marketo Microsoft Dynamics Sync y Adobe Sign para Dynamics, aparecen dos nuevas opciones en Marketo Admin Terminal.

![Administrador](assets/adminTerminal.png)

1. Haga clic en **[!UICONTROL Sincronización de entidades de Dynamics]**.

   La sincronización debe estar desactivada antes de sincronizar entidades personalizadas. Haga clic en **Sincronizar esquema** si es la primera vez. De lo contrario, haga clic en **Actualizar esquema**.

   ![Actualizar](assets/refreshSchema.png)

## Sincronizar el objeto personalizado

1. En el lado derecho, localice los objetos personalizados basados en [!UICONTROL Candidato], [!UICONTROL Contacto] y [!UICONTROL Cuenta].

   * **Habilite** Sincronizar los objetos en  **** Candidato si desea enviar un recordatorio cuando un   Candidato no haya firmado un acuerdo en Dynamics.

   * **Active Sincronizar** los objetos en  **** Contacto si desea enviar un recordatorio cuando un   Contacto no ha firmado un acuerdo en Dynamics.

   * **Habilite** Sincronizar los objetos en  **** Cuenta si desea enviar un recordatorio cuando una   cuenta no haya firmado un acuerdo en Dynamics.

   * **Habilite** Sincronizar para el objeto de acuerdo en el  **[!UICONTROL elemento principal]**  deseado ([!UICONTROL Candidato],  [!UICONTROL Contacto] o  [!UICONTROL Cuenta]).

   ![Objetos personalizados](assets/enableSyncDynamics.png)

1. En la nueva ventana, seleccione las propiedades que desee en Acuerdo y, a continuación, habilite las casillas en **Restricción** y **Activador** para exponerlas a sus actividades de marketing.

   ![Sincronización personalizada 1](assets/entitySync1.png)

   ![Sincronización personalizada 2](assets/entitySync2.png)

1. Reactive la sincronización después de activar la sincronización en los objetos personalizados.

   Vuelva a Admin Terminal, haga clic en **Microsoft Dynamics** y, a continuación, haga clic en **Activar sincronización**.

   ![Microsoft Dynamics](assets/microsoftDynamics.png)

   ![Activar global](assets/enableGlobalDynamics.png)

## Crear el programa y el token

1. En la sección Actividades de marketing de Marketo, haga clic con el botón derecho en **Actividades de marketing** en la barra izquierda.

   Seleccione **Nueva carpeta de campaña** y asígnele un nombre.

   ![Nueva carpeta](assets/newFolder.png)

1. Haga clic con el botón derecho en la carpeta creada, seleccione **Nuevo programa** y asígnele un nombre.

   Deje todo lo demás como predeterminado y, a continuación, haga clic en **Crear**.

   ![Nuevo programa 1](assets/newProgram1.png)

   ![Nuevo programa 2](assets/newProgram2.png)

1. Haga clic en **Mis tokens** y, a continuación, arrastre **Script de correo electrónico** al lienzo.

   ![Script de correo electrónico](assets/emailScript.png)

1. Asigne un nombre y haga clic en **Haga clic para editar**.

   ![Nombre y edición](assets/nameAndSave.png)

1. Expanda **[!UICONTROL Objetos personalizados]** en el lado derecho y, a continuación, expanda el objeto **[!UICONTROL Acuerdo]**.

   Busque y arrastre [!UICONTROL Nombre], Estado del acuerdo, Enviado en y Url del firmante actual al lienzo.

1. Escriba una secuencia de comandos Velocity utilizando estos distintivos para mostrar la dirección URL del acuerdo de un acuerdo sin firmar durante una semana. A continuación se muestra un ejemplo que compara la fecha actual con la fecha Enviada:

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

1. Haga clic con el botón derecho en el programa que creó y haga clic en **[!UICONTROL Nuevo activo local]** y, a continuación, seleccione **[!UICONTROL Correo electrónico]**.

   ![Nuevo correo electrónico](assets/createNewEmail.png)

1. En la nueva ficha, introduzca un **[!UICONTROL Nombre]** y una **[!UICONTROL Descripción]** para el correo electrónico y seleccione una plantilla del selector de plantillas.

   ![Selector de plantilla](assets/templatePicker.png)

1. Haga clic en **[!UICONTROL Crear]**.

1. Establezca los valores **[!UICONTROL Desde nombre]** y **[!UICONTROL Desde dirección]**.

   ![Correo electrónico recordatorio](assets/reminderEmail.png)

1. Haga clic en el cuerpo del mensaje para activar el editor.

   Haga clic en el botón **[!UICONTROL Insertar token]**, busque el token de URL de acuerdo personalizado que creó y, a continuación, haga clic en **[!UICONTROL Insertar]**. Termine de personalizar su correo electrónico y haga clic en **[!UICONTROL Guardar]**.

   ![Insertar token](assets/insertToken.png)

1. Vista previa mediante un perfil que tenga asignado un acuerdo.

   Debe ver un vínculo a la URL con el nombre del acuerdo como etiqueta.

   ![Vínculo de correo electrónico](assets/emailLink.png)

## Configuración del filtro de campaña inteligente

1. Haga clic con el botón derecho en el programa que creó y, a continuación, haga clic en **[!UICONTROL Nueva campaña inteligente]**.

   ![Smart Campaign 1](assets/smartCampaign1.png)

1. Asigne un nombre a su elección y, a continuación, haga clic en **[!UICONTROL Crear]**.

   ![Smart Campaign 2](assets/smartCampaign2.png)

1. Busque y, a continuación, haga clic y arrastre **[!UICONTROL Tiene acuerdo]** a la lista inteligente.

   ![Tiene acuerdo](assets/hasAgreementDynamics1.png)

   Los campos expuestos al activador deben estar disponibles en **[!UICONTROL Agregar restricción]**.

1. Seleccione **[!UICONTROL Estado del acuerdo]** y cualquier otro campo por el que desee filtrar.

   Para cada campo agregado, defina los valores por los que filtrar. En este caso, solo se activa cuando **[!UICONTROL Estado del acuerdo]** está *Enviado para firmar* y **[!UICONTROL Enviado el]** está *en el pasado antes de 1 semana*.

   ![Estado del acuerdo](assets/hasAgreementDynaSentOn.png)

   >[!NOTE]
   >
   > Agregue un identificador único a las restricciones, como **Name**, si desea que esta campaña se ejecute solo para determinados acuerdos.

1. Confirme la audiencia de la campaña y vea quién calificará en la ficha Programación.

   ![Calificadores](assets/qualifiers.png)

## Configuración del flujo de campaña inteligente

Dado que se utilizó el filtro de campaña **Días hasta que caduque**, puede utilizar una repetición programada para la campaña.

1. Haga clic en la ficha **[!UICONTROL Flow]** en la [!UICONTROL Smart Campaign].

   Busque y arrastre el flujo **Enviar correo electrónico** al lienzo y seleccione el correo electrónico de recordatorio que creó en la sección anterior.

   ![Enviar correo electrónico](assets/sendEmail.png)

1. Haga clic en la ficha **[!UICONTROL Programar]** en la campaña inteligente. Asegúrese de que el flujo de campaña esté limitado a ejecutarse solo una vez por persona en la **Configuración de campaña inteligente**. A continuación, haga clic en la ficha **Programar repetición**.

   ![Pestaña Programar](assets/scheduleTab.png)

1. Establezca el **Programa** en _Diario_. Elija un día y una hora de inicio y una fecha de finalización para la campaña si es necesario.

   ![Configuración de programación](assets/scheduleSettings.png)

>[!TIP]
>
>Este tutorial es parte del curso [Acelerar los ciclos de ventas con Adobe Sign para Microsoft Dynamics y Marketo](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) que está disponible de forma gratuita para el Experience League.