---
title: Envío de notificaciones con Adobe Sign para Microsoft Dynamics 365 y Marketo
description: Obtenga más información sobre cómo enviar un mensaje de texto, un correo electrónico o una notificación de inserción para que el firmante sepa que un acuerdo está en camino
role: Admin
product: adobe sign
solution: Adobe Sign, Marketo, Document Cloud
level: Intermediate
topic-revisit: Integrations
thumbnail: KT-7249.jpg
exl-id: 2e0de48c-70bf-4dc5-8251-88e7399f588a
source-git-commit: bcddb0ee106239f2786debaed908b2a2ec5ce792
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---

# Envío de notificaciones con Adobe Sign para Microsoft Dynamics 365 y Marketo

Obtenga más información sobre cómo enviar un mensaje de texto, un correo electrónico o una notificación push para que el firmante sepa que un acuerdo está en camino mediante Adobe Sign, Adobe Sign para Microsoft Dynamic, Marketo y Marketo Microsoft Dynamics Sync. Para enviar notificaciones desde Marketo, primero debe adquirir o configurar una función de administración de SMS de Marketo. Este tutorial utiliza [Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/), pero hay otras soluciones SMS de Marketo disponibles.

## Requisitos previos

1. Instale Marketo Microsoft Dynamics Sync.

   La información y el último complemento para Microsoft Dynamics Sync están disponibles [aquí.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/marketo-plugin-releases-for-microsoft-dynamics.html)

1. Instale Adobe Sign para Microsoft Dynamics.

   La información sobre este complemento está disponible [aquí.](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)

## Buscar el objeto personalizado

Una vez completadas las configuraciones de Marketo Microsoft Dynamics Sync y Adobe Sign para Dynamics, aparecen dos nuevas opciones en Marketo Admin Terminal.

![Administrador](assets/adminTerminal.png)

* Haga clic en **[!UICONTROL Sincronización de entidades de Dynamics]**.

   La sincronización debe estar desactivada antes de sincronizar entidades personalizadas. Haga clic en **[!UICONTROL Sincronizar esquema]** si es la primera vez. De lo contrario, haga clic en **[!UICONTROL Actualizar esquema]**.

   ![Actualizar](assets/refreshSchema.png)

## Sincronizar el objeto personalizado

1. En el lado derecho, localice los objetos personalizados basados en [!UICONTROL Candidato], [!UICONTROL Contacto] y [!UICONTROL Cuenta].

   * **[!UICONTROL Habilite]** Sincronizar para los objetos en Candidato si desea activarlo cuando se añada un Candidato a un acuerdo en Dynamics.

   * **[!UICONTROL Habilite]** Sincronizar para los objetos en Contacto si desea activarlo cuando se añada un Contacto a un acuerdo en Dynamics.

   * **[!UICONTROL Habilite]** Sincronizar para los objetos en Cuenta si desea activarlo cuando se añada una cuenta a un acuerdo en Dynamics.

   * **Habilite** Sincronizar para el objeto Acuerdo en el elemento principal deseado (Candidato, Contacto o Cuenta).

   ![Objetos personalizados](assets/enableSyncDynamics.png)

1. En la nueva ventana, seleccione las propiedades que desee en Acuerdo.

   Active las casillas de **[!UICONTROL Restricción]** y **[!UICONTROL Activador]** para exponerlas a sus actividades de marketing.

   ![Sincronización personalizada 1](assets/entitySync1.png)

   ![Sincronización personalizada 2](assets/entitySync2.png)

1. Reactive la sincronización después de activar la sincronización en los objetos personalizados.

   Vuelva al [!UICONTROL Terminal de administración], haga clic en **[!UICONTROL Microsoft Dynamics]** y, a continuación, haga clic en **[!UICONTROL Habilitar sincronización]**.

   ![Microsoft Dynamics](assets/microsoftDynamics.png)

   ![Activar global](assets/enableGlobalDynamics.png)

## Crear el programa

1. En [!UICONTROL Actividades de marketing], haga clic con el botón derecho en **[!UICONTROL Actividades de marketing]** en la barra izquierda, seleccione **[!UICONTROL Nueva carpeta de campaña]** y asígnele el nombre.

   ![Nueva carpeta](assets/newFolder.png)

1. Haga clic con el botón derecho en la carpeta creada, seleccione **[!UICONTROL Nuevo programa]** y asígnele un nombre.

   Deje todo lo demás como predeterminado y, a continuación, haga clic en **[!UICONTROL Crear]**.

   ![Nuevo programa 1](assets/newProgram1.png)

   ![Nuevo programa 2](assets/newProgram2.png)

## Configurar [!DNL Twilio] SMS

En primer lugar, asegúrese de tener una cuenta activa [!DNL Twilio] y de haber adquirido las funciones de SMS que necesita.

La configuración del webhook de SMS Marketo - [!DNL Twilio] requiere tres parámetros [!DNL Twilio] de su cuenta.

* SID de cuenta
* Token de cuenta
* Número de teléfono de Twilio

Recupere estos parámetros de su cuenta y abra su instancia de Marketo.

1. Haga clic en **[!UICONTROL Administrador]** en la parte superior derecha.

   ![Administrador](assets/adminTab.png)

1. Haga clic en **[!UICONTROL Webhooks]** y, a continuación, haga clic en **[!UICONTROL Nuevo Webhook]**.

   ![Webhooks](assets/webhooks.png)

1. Introduzca un **[!UICONTROL Nombre de Webhook]** y **[!UICONTROL Descripción]**.

1. Introduzca la siguiente URL y asegúrese de reemplazar las `ACCOUNT_SID` y `AUTH_TOKEN` por sus credenciales [!DNL Twilio].

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. Seleccione **[!UICONTROL POST]** como tipo de solicitud.

1. Introduzca la siguiente **Plantilla** y asegúrese de reemplazar `MY_TWILIO_NUMBER` por su [!DNL Twilio] número de teléfono y `YOUR_MESSAGE` por un mensaje de su elección.

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. Establezca **[!UICONTROL Codificación de token de solicitud]** en *Formulario/URL*.

1. Establezca el tipo de respuesta en *JSON* y, a continuación, haga clic en **[!UICONTROL Guardar]**.

## Configuración del activador de la campaña inteligente

1. En la sección Actividades de marketing, haga clic con el botón derecho en el programa que ha creado y, a continuación, seleccione **[!UICONTROL Nueva campaña inteligente]**.

   ![Smart Campaign 1](assets/smartCampaign1.png)

1. Asígnele un nombre y haga clic en **[!UICONTROL Crear]**.

   ![Smart Campaign 2](assets/smartCampaign3.png)

   Debería ver varios activadores disponibles para su uso en la carpeta Microsoft.

1. Haga clic y arrastre **[!UICONTROL Agregado al acuerdo]** a la **[!UICONTROL lista inteligente]** y, a continuación, agregue las restricciones que desee tener en el activador.

   ![Agregado al acuerdo](assets/addedToAgreementDynamics.png)

## Configuración del flujo de campaña inteligente

1. Haga clic en la ficha **[!UICONTROL Flow]** en la [!UICONTROL Smart Campaign].

   Busque y arrastre el flujo **Llamar a Webhook** al lienzo y seleccione el webhook que creó en la sección anterior.

   ![Llamar a Webhook](assets/callWebhook.png)

1. Ya está configurada tu campaña de notificación SMS para los posibles clientes que se añaden a un acuerdo.
>[!TIP]
>
>Este tutorial es parte del curso [Acelerar los ciclos de ventas con Adobe Sign para Microsoft Dynamics y Marketo](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) que está disponible de forma gratuita para el Experience League.