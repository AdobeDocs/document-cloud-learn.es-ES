---
title: Enviar notificaciones con Acrobat Sign para Microsoft Dynamics 365 y Marketo
description: Aprenda a enviar un mensaje de texto, un correo electrónico o una notificación push para informar al firmante de que un acuerdo está en camino
feature: Integrations
role: Admin
solution: Acrobat Sign, Marketo, Document Cloud
level: Intermediate
topic: Integrations
topic-revisit: Integrations
jira: KT-7249
thumbnail: KT-7249.jpg
exl-id: 2e0de48c-70bf-4dc5-8251-88e7399f588a
source-git-commit: 51d1a59999a7132cb6e47351cc39a93d9a38eaeb
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 0%

---

# Enviar notificaciones con Acrobat Sign para Microsoft Dynamics 365 y Marketo

Aprenda a enviar un mensaje de texto, un correo electrónico o una notificación push para informar al firmante de que un acuerdo está en camino mediante Acrobat Sign, Acrobat Sign para Microsoft Dynamic, Marketo y Marketo Microsoft Dynamics Sync. Para enviar notificaciones desde Marketo, primero debe adquirir o configurar una función de administración de SMS de Marketo. Este tutorial utiliza [Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/), pero hay disponibles otras soluciones de SMS de Marketo.

## Requisitos previos

1. Instale Marketo Microsoft Dynamics Sync.

   La información y el complemento más reciente para Microsoft Dynamics Sync están disponibles [aquí.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/marketo-plugin-releases-for-microsoft-dynamics.html?lang=es)

1. Instale Acrobat Sign para Microsoft Dynamics.

   La información sobre este complemento está disponible [aquí.](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)

## Buscar el objeto personalizado

Una vez completadas las configuraciones de Marketo Microsoft Dynamics Sync y Acrobat Sign para Dynamics , aparecen dos nuevas opciones en el Terminal de administración de Marketo.

![Administrador](assets/adminTerminal.png)

* Haga clic en **[!UICONTROL Sincronización de entidades de Dynamics]**.

  La sincronización debe desactivarse antes de sincronizar entidades personalizadas. Haga clic en **[!UICONTROL Sincronizar esquema]** si es la primera vez que lo hace. De lo contrario, haga clic en **[!UICONTROL Actualizar esquema]**.

  ![Actualizar](assets/refreshSchema.png)

## Sincronizar el objeto personalizado

1. En el lado derecho, busca objetos personalizados basados en [!UICONTROL Lead], [!UICONTROL Contact] y [!UICONTROL Account].

   * **[!UICONTROL Habilite la sincronización]** para los objetos en Candidato si desea activarla cuando se agregue un Candidato a un acuerdo en Dynamics.

   * **[!UICONTROL Habilite la sincronización]** para los objetos en Contacto si desea activarla cuando se agregue un contacto a un acuerdo en Dynamics.

   * **[!UICONTROL Habilite la sincronización]** para los objetos de Account si desea activarla cuando se agregue una cuenta a un acuerdo en Dynamics.

   * **Habilite la sincronización** para el objeto Acuerdo en el elemento principal deseado (Candidato, Contacto o Cuenta).

   ![Objetos personalizados](assets/enableSyncDynamics.png)

1. En la nueva ventana, seleccione las propiedades que desee en Acuerdo.

   Habilite los cuadros bajo **[!UICONTROL Restricción]** y **[!UICONTROL Desencadenador]** para exponerlos a sus actividades de marketing.

   ![Sincronización personalizada 1](assets/entitySync1.png)

   ![Sincronización personalizada 2](assets/entitySync2.png)

1. Vuelva a activar la sincronización después de activar la sincronización en los objetos personalizados.

   Vuelve al [!UICONTROL Terminal de administración], haz clic en **[!UICONTROL Microsoft Dynamics]** y luego en **[!UICONTROL Habilitar sincronización]**.

   ![Microsoft Dynamics](assets/microsoftDynamics.png)

   ![Habilitar global](assets/enableGlobalDynamics.png)

## Crear el programa

1. En [!UICONTROL Actividades de marketing], haga clic con el botón derecho en **[!UICONTROL Actividades de marketing]** en la barra izquierda, seleccione **[!UICONTROL Nueva carpeta de campaña]** y asígnele un nombre.

   ![Nueva carpeta](assets/newFolder.png)

1. Haga clic con el botón derecho en la carpeta creada, seleccione **[!UICONTROL Nuevo programa]** y asígnele un nombre.

   Deja todo lo demás como predeterminado y luego haz clic en **[!UICONTROL Crear]**.

   ![Nuevo programa 1](assets/newProgram1.png)

   ![Nuevo programa 2](assets/newProgram2.png)

## Configurar [!DNL Twilio] SMS

Primero, asegúrate de tener una cuenta de [!DNL Twilio] activa y de haber adquirido las funciones de SMS que necesitas.

La configuración del webhook de SMS de Marketo - [!DNL Twilio] requiere tres parámetros de [!DNL Twilio] de su cuenta.

* SID de cuenta
* Token de cuenta
* Número de teléfono Twilio

Recupere estos parámetros de su cuenta y abra su instancia de Marketo.

1. Haga clic en **[!UICONTROL Administrador]** en la parte superior derecha.

   ![Administrador](assets/adminTab.png)

1. Haga clic en **[!UICONTROL Webhooks]** y, a continuación, en **[!UICONTROL Nuevo webhook]**.

   ![Webhooks](assets/webhooks.png)

1. Escriba un **[!UICONTROL Nombre de webhook]** y una **[!UICONTROL Descripción]**.

1. Escriba la siguiente dirección URL y asegúrese de reemplazar `ACCOUNT_SID` y `AUTH_TOKEN` por sus credenciales de [!DNL Twilio].

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. Selecciona **[!UICONTROL POST]** como tu tipo de solicitud.

1. Escribe la siguiente **plantilla** y asegúrate de reemplazar `MY_TWILIO_NUMBER` por tu número de teléfono [!DNL Twilio] y `YOUR_MESSAGE` por un mensaje de tu elección.

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. Establezca **[!UICONTROL Codificación de token de solicitud]** en *Formulario/URL*.

1. Establezca el tipo de respuesta en *JSON* y, a continuación, haga clic en **[!UICONTROL Guardar]**.

## Configurar el activador inteligente de la campaña

1. En la sección Actividades de marketing, haz clic con el botón derecho en el programa que has creado y, a continuación, selecciona **[!UICONTROL Nueva campaña inteligente]**.

   ![Smart Campaign 1](assets/smartCampaign1.png)

1. Asígnele un nombre y, a continuación, haga clic en **[!UICONTROL Crear]**.

   ![Smart Campaign 2](assets/smartCampaign3.png)

   Debería ver varios desencadenadores disponibles para su uso en la carpeta Microsoft.

1. Haga clic y arrastre **[!UICONTROL Agregado al acuerdo]** a la **[!UICONTROL lista inteligente]**; a continuación, agregue las restricciones que desee tener en el desencadenador.

   ![Agregado al acuerdo](assets/addedToAgreementDynamics.png)

## Configurar el flujo de campaña inteligente

1. Haz clic en la pestaña **[!UICONTROL Flujo]** en [!UICONTROL Smart Campaign].

   Busque y arrastre el flujo **Call Webhook** al lienzo y seleccione el webhook que creó en la sección anterior.

   ![Llamar a webhook](assets/callWebhook.png)

1. La campaña de avisos por SMS para clientes potenciales añadidos a un acuerdo ya está configurada.
