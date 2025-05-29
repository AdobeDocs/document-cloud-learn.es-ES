---
title: Enviar recordatorios con Acrobat Sign para Microsoft Dynamics 365 y Marketo
description: Obtenga información sobre cómo enviar un recordatorio por correo electrónico cuando un acuerdo permanece sin firmar después de un período de tiempo
feature: Integrations
role: Admin
solution: Acrobat Sign, Marketo Engage, Document Cloud
level: Intermediate
topic: Integrations
topic-revisit: Integrations
jira: KT-7250
thumbnail: KT-7250.jpg
exl-id: 5a97fade-18a3-448a-8504-efb9e38e9187
source-git-commit: a88ec5a68aa2a02ec2f118332ec31f47d3d5d300
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 0%

---

# Enviar recordatorios con Acrobat Sign para Microsoft Dynamics 365 y Marketo

Obtenga información sobre cómo enviar un recordatorio por correo electrónico cuando un acuerdo permanece sin firmar después de un período de tiempo. Esta integración utiliza Acrobat Sign, Acrobat Sign para Microsoft Dynamics, Marketo y Marketo Microsoft Dynamics Sync.

## Requisitos previos

1. Instale Marketo Microsoft Dynamics Sync.

   La información y el complemento más reciente para Microsoft Dynamics Sync están disponibles [aquí.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/marketo-plugin-releases-for-microsoft-dynamics.html)

1. Instale [Acrobat Sign para Microsoft Dynamics](https://appsource.microsoft.com/es-es/product/dynamics-365/adobesign.f3b856fc-a427-4d47-ad4b-d5d1baba6f86).

   La información sobre este complemento está disponible [aquí.](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)

## Buscar el objeto personalizado

Una vez completadas las configuraciones de Marketo Microsoft Dynamics Sync y Acrobat Sign para Dynamics , aparecen dos nuevas opciones en el Terminal de administración de Marketo.

![Administrador](assets/adminTerminal.png)

1. Haga clic en **[!UICONTROL Sincronización de entidades de Dynamics]**.

   La sincronización debe desactivarse antes de sincronizar entidades personalizadas. Haga clic en **Sincronizar esquema** si es la primera vez que lo hace. De lo contrario, haga clic en **Actualizar esquema**.

   ![Actualizar](assets/refreshSchema.png)

## Sincronizar el objeto personalizado

1. En el lado derecho, busca objetos personalizados basados en [!UICONTROL Lead], [!UICONTROL Contact] y [!UICONTROL Account].

   * **Habilite la sincronización** para los objetos de **[!UICONTROL Candidato]** si desea enviar un recordatorio cuando un [!UICONTROL Candidato] no haya firmado un acuerdo en Dynamics.

   * **Habilite la sincronización** para los objetos de **[!UICONTROL Contacto]** si desea enviar un recordatorio cuando un [!UICONTROL Contacto] no haya firmado un acuerdo en Dynamics.

   * **Habilite la sincronización** para los objetos de **[!UICONTROL Cuenta]** si desea enviar un recordatorio cuando una [!UICONTROL Cuenta] no haya firmado un acuerdo en Dynamics.

   * **Habilitar sincronización** para el objeto de acuerdo en la **[!UICONTROL Principal]** ([!UICONTROL Candidato], [!UICONTROL Contacto] o [!UICONTROL Cuenta]) deseada.

   ![Objetos personalizados](assets/enableSyncDynamics.png)

1. En la nueva ventana, seleccione las propiedades que desee en Acuerdo y, a continuación, habilite los cuadros bajo **Restricción** y **Desencadenador** para exponerlos a sus actividades de marketing.

   ![Sincronización personalizada 1](assets/entitySync1.png)

   ![Sincronización personalizada 2](assets/entitySync2.png)

1. Vuelva a activar la sincronización después de activar la sincronización en los objetos personalizados.

   Vuelve al Terminal de administración, haz clic en **Microsoft Dynamics** y luego en **Habilitar sincronización**.

   ![Microsoft Dynamics](assets/microsoftDynamics.png)

   ![Habilitar global](assets/enableGlobalDynamics.png)

## Crear el programa y el token

1. En la sección Actividades de marketing de Marketo, haga clic con el botón derecho en **Actividades de marketing** en la barra izquierda.

   Seleccione **Nueva carpeta de campaña** y asígnele un nombre.

   ![Nueva carpeta](assets/newFolder.png)

1. Haga clic con el botón derecho en la carpeta creada, seleccione **Nuevo programa** y asígnele un nombre.

   Deja todo lo demás como predeterminado y luego haz clic en **Crear**.

   ![Nuevo programa 1](assets/newProgram1.png)

   ![Nuevo programa 2](assets/newProgram2.png)

1. Haz clic en **Mis tokens** y arrastra **Script de correo electrónico** al lienzo.

   ![Script de correo electrónico](assets/emailScript.png)

1. Dale un nombre y, a continuación, haz clic en **Clic para editar**.

   ![Asignar nombre y editar](assets/nameAndSave.png)

1. Expanda **[!UICONTROL Objetos personalizados]** en el lado derecho y, a continuación, expanda el objeto **[!UICONTROL Acuerdo]**.

   Busque y arrastre [!UICONTROL Nombre], Estado del acuerdo, Enviado el y URL del firmante actual al lienzo.

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

Entre los ejemplos de personalización se incluyen: el nombre del firmante, el nombre del acuerdo, un vínculo al acuerdo, etc.

1. Haz clic con el botón derecho en el programa que has creado, haz clic en **[!UICONTROL Nuevo activo local]** y selecciona **[!UICONTROL Correo electrónico]**.

   ![Nuevo correo electrónico](assets/createNewEmail.png)

1. En la nueva pestaña, introduzca un **[!UICONTROL Nombre]** y una **[!UICONTROL Descripción]** para el correo electrónico y seleccione una plantilla en el selector de plantillas.

   ![Selector de plantilla](assets/templatePicker.png)

1. Haga clic en **[!UICONTROL Crear]**.

1. Establezca **[!UICONTROL Nombre de origen]** y **[!UICONTROL Dirección de origen]**.

   ![Correo electrónico de recordatorio](assets/reminderEmail.png)

1. Haga clic en el cuerpo del mensaje para activar el editor.

   Haga clic en el botón **[!UICONTROL Insertar token]**, busque el token de URL de acuerdo personalizado que creó y, a continuación, haga clic en **[!UICONTROL Insertar]**. Termina de personalizar tu correo electrónico y haz clic en **[!UICONTROL Guardar]**.

   ![Insertar token](assets/insertToken.png)

1. Previsualice mediante un perfil que tenga un acuerdo asignado.

   Debería ver un vínculo a la dirección URL con el nombre del acuerdo como etiqueta.

   ![Vínculo de correo electrónico](assets/emailLink.png)

## Configurar el filtro de Smart Campaign

1. Haz clic con el botón derecho en el programa que has creado y, a continuación, haz clic en **[!UICONTROL Nueva campaña inteligente]**.

   ![Smart Campaign 1](assets/smartCampaign1.png)

1. Dale el nombre que quieras y, a continuación, haz clic en **[!UICONTROL Crear]**.

   ![Smart Campaign 2](assets/smartCampaign2.png)

1. Busque y, a continuación, haga clic y arrastre **[!UICONTROL Tiene acuerdo]** a la lista inteligente.

   ![Tiene acuerdo](assets/hasAgreementDynamics1.png)

   Los campos expuestos al desencadenador deben estar disponibles en **[!UICONTROL Agregar restricción]**.

1. Seleccione **[!UICONTROL Estado del acuerdo]** y cualquier otro campo por el que desee filtrar.

   Para cada campo añadido, defina los valores por los que filtrar. En este caso, solo se activa cuando el **[!UICONTROL Estado del acuerdo]** es *Enviado para firmar* y **[!UICONTROL Enviado el]** es *pasado antes de 1 semana*.

   ![Estado del acuerdo](assets/hasAgreementDynaSentOn.png)

   >[!NOTE]
   >
   > Agregue un identificador único a las restricciones, como **Name**, si desea que esta campaña se ejecute solo para determinados acuerdos.

1. Confirma el público de la campaña y comprueba quién cumple los requisitos en la pestaña Programación.

   ![Calificadores](assets/qualifiers.png)

## Configurar el flujo de campaña inteligente

Dado que se utilizó el filtro de campaña **Días hasta que caduque**, puede utilizar una periodicidad programada para la campaña.

1. Haz clic en la pestaña **[!UICONTROL Flujo]** en [!UICONTROL Smart Campaign].

   Busque y arrastre el flujo **Enviar correo electrónico** al lienzo y seleccione el correo electrónico de recordatorio que creó en la sección anterior.

   ![Enviar correo electrónico](assets/sendEmail.png)

1. Haga clic en la pestaña **[!UICONTROL Programación]** en Smart Campaign. Asegúrese de que el flujo de la campaña esté limitado para ejecutarse solo una vez por persona en **Configuración inteligente de la campaña**. Luego, haz clic en la pestaña **Programar periodicidad**.

   ![Ficha Programación](assets/scheduleTab.png)

1. Establezca **Schedule** en _Daily_. Elija un día y una hora de inicio y una fecha de finalización para la campaña, si es necesario.

   ![Configuración de programación](assets/scheduleSettings.png)
