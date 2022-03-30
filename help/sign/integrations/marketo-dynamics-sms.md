---
title: Enviar notificaciones con Adobe Sign para Microsoft Dynamics 365 y Marketo
description: Aprenda a enviar un mensaje de texto, un correo electrónico o una notificación push para informar al firmante de que un acuerdo está en camino
role: Admin
product: adobe sign
solution: Acrobat Sign, Marketo, Document Cloud
level: Intermediate
topic-revisit: Integrations
thumbnail: KT-7249.jpg
exl-id: 2e0de48c-70bf-4dc5-8251-88e7399f588a
source-git-commit: 089b6768cee4e3af8f1a349d5754d84aa3f4f69a
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---

# Enviar notificaciones con Adobe Sign para Microsoft Dynamics 365 y Marketo

Aprenda a enviar un mensaje de texto, un correo electrónico o una notificación push para informar al firmante de que un acuerdo está en camino mediante Adobe Sign, Adobe Sign para Microsoft Dynamic, Marketo y Marketo Microsoft Dynamics Sync. Para enviar notificaciones desde Marketo, primero debe adquirir o configurar una función de administración de SMS de Marketo. Este tutorial utiliza [Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/), pero hay otras soluciones SMS de Marketo disponibles.

## Requisitos previos

1. Instale Marketo Microsoft Dynamics Sync.

   Dispone de información y del plugin más reciente para Microsoft Dynamics Sync [aquí.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/marketo-plugin-releases-for-microsoft-dynamics.html)

1. Instale Adobe Sign para Microsoft Dynamics.

   Información sobre este plugin está disponible [aquí.](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)

## Buscar el objeto personalizado

Una vez completadas las configuraciones de Marketo Microsoft Dynamics Sync y Adobe Sign para Dynamics , aparecen dos nuevas opciones en el Terminal de administración de Marketo.

![Administrador](assets/adminTerminal.png)

* Haga clic en **[!UICONTROL Sincronización de entidades de Dynamics]**.

   La sincronización debe desactivarse antes de sincronizar entidades personalizadas. Haga clic en **[!UICONTROL Sincronizar esquema]** si es tu primera vez. De lo contrario, haga clic en **[!UICONTROL Actualizar esquema]**.

   ![Actualizar](assets/refreshSchema.png)

## Sincronizar el objeto personalizado

1. En el lado derecho, localice [!UICONTROL Plomo], [!UICONTROL Contacto]y [!UICONTROL Cuenta]objetos personalizados basados en el usuario.

   * **[!UICONTROL Habilitar sincronización]** para los objetos en Candidato si desea activar cuando se añade un Candidato a un acuerdo en Dynamics.

   * **[!UICONTROL Habilitar sincronización]** para los objetos de Contacto si desea activar cuando se agrega un Contacto a un acuerdo en Dynamics.

   * **[!UICONTROL Habilitar sincronización]** para los objetos de Account si desea activar cuando se agrega una cuenta a un acuerdo en Dynamics.

   * **Habilitar sincronización** para el objeto Acuerdo bajo el padre deseado (Candidato, Contacto o Cuenta).

   ![Objetos personalizados](assets/enableSyncDynamics.png)

1. En la nueva ventana, seleccione las propiedades que desee en Acuerdo.

   Active las casillas de **[!UICONTROL Restricción]** y **[!UICONTROL Desencadenador]** para exponerlos a sus actividades de marketing.

   ![Sincronización personalizada 1](assets/entitySync1.png)

   ![Sincronización personalizada 2](assets/entitySync2.png)

1. Vuelva a activar la sincronización después de activar la sincronización en los objetos personalizados.

   Volver a la [!UICONTROL Terminal de administración], haga clic en **[!UICONTROL Microsoft Dynamics]** y, a continuación, haga clic en **[!UICONTROL Habilitar sincronización]**.

   ![Microsoft Dynamics](assets/microsoftDynamics.png)

   ![Habilitar global](assets/enableGlobalDynamics.png)

## Crear el programa

1. En [!UICONTROL Actividades de marketing], haga clic con el botón derecho **[!UICONTROL Actividades de marketing]** en la barra izquierda, seleccione **[!UICONTROL Nueva carpeta de campaña]** y ponle un nombre.

   ![Nueva carpeta](assets/newFolder.png)

1. Haga clic con el botón derecho en la carpeta creada y seleccione **[!UICONTROL Nuevo programa]** y ponle un nombre.

   Deje todo lo demás como predeterminado y, a continuación, haga clic en **[!UICONTROL Crear]**.

   ![Nuevo programa 1](assets/newProgram1.png)

   ![Nuevo programa 2](assets/newProgram2.png)

## Configuración [!DNL Twilio] SMS

Primero asegúrese de que tiene un [!DNL Twilio] y ha adquirido las funciones SMS que necesita.

Configuración de Marketo: [!DNL Twilio] SMS webhook requiere tres [!DNL Twilio] de su cuenta.

* SID de cuenta
* Token de cuenta
* Número de teléfono Twilio

Recupere estos parámetros de su cuenta y abra su instancia de Marketo.

1. Haga clic en **[!UICONTROL Administrador]** en la parte superior derecha.

   ![Administrador](assets/adminTab.png)

1. Haga clic en **[!UICONTROL Webhooks]**, haga clic en **[!UICONTROL Nuevo webhook]**.

   ![Webhooks](assets/webhooks.png)

1. Introduzca un **[!UICONTROL Nombre de webhook]** y **[!UICONTROL Descripción]**.

1. Introduzca la siguiente dirección URL y asegúrese de reemplazar la `ACCOUNT_SID` y `AUTH_TOKEN` con su [!DNL Twilio] credenciales.

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. Seleccionar **[!UICONTROL POST]** como tipo de solicitud.

1. Introduzca lo siguiente **Plantilla** y asegúrese de reemplazar `MY_TWILIO_NUMBER` con su [!DNL Twilio] número de teléfono y `YOUR_MESSAGE` con un mensaje de su elección.

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. Establezca el **[!UICONTROL Codificación de token de solicitud]** para *Formulario/URL*.

1. Establezca el Tipo de respuesta en *JSON* a continuación, haga clic en **[!UICONTROL Guardar]**.

## Configurar el activador inteligente de campañas

1. En la sección Actividades de marketing, haga clic con el botón derecho en el programa que ha creado y, a continuación, seleccione **[!UICONTROL Nueva campaña inteligente]**.

   ![Smart Campaign 1](assets/smartCampaign1.png)

1. Asígnele un nombre y, a continuación, haga clic en **[!UICONTROL Crear]**.

   ![Smart Campaign 2](assets/smartCampaign3.png)

   Debería ver varios desencadenadores disponibles para su uso en la carpeta Microsoft.

1. Haga clic y arrastre **[!UICONTROL Añadido al acuerdo]** a la **[!UICONTROL Smart List]** y, a continuación, añada las restricciones que desee tener en el activador.

   ![Añadido al acuerdo](assets/addedToAgreementDynamics.png)

## Configurar el flujo de campaña inteligente

1. Haga clic en **[!UICONTROL Flujo]** en la pestaña [!UICONTROL Smart Campaign].

   Busque y arrastre el **Llamar a webhook** en el lienzo y seleccione el webhook creado en la sección anterior.

   ![Llamar a webhook](assets/callWebhook.png)

1. La campaña de avisos por SMS para clientes potenciales añadidos a un acuerdo ya está configurada.
>[!TIP]
>
>Este tutorial forma parte del curso [Agiliza los ciclos de ventas con Adobe Sign para Microsoft Dynamics y Marketo](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) que está disponible de forma gratuita en el Experience League!