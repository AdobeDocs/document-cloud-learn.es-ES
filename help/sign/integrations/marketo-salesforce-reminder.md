---
title: Enviar recordatorios con Acrobat Sign para Salesforce y la Guía de configuración de Marketo
description: Obtenga información sobre cómo enviar un recordatorio por correo electrónico desde Marketo cuando un acuerdo permanece sin firmar después de un período de tiempo
role: Admin
product: adobe sign
solution: Acrobat Sign, Marketo, Document Cloud
level: Intermediate
jira: KT-7248
topic-revisit: Integrations
thumbnail: KT-7248.jpg
exl-id: 33aca2e0-2f27-4100-a16f-85ba652c17a3
source-git-commit: aa8fd589d214879f2bfcb6bc54576c707532fd6f
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 1%

---

# Enviar recordatorios con Acrobat Sign para Salesforce y la Guía de configuración de Marketo

Obtenga información sobre cómo enviar un recordatorio por correo electrónico desde Marketo cuando un acuerdo permanece sin firmar después de un período de tiempo. Esta integración utiliza Acrobat Sign, Acrobat Sign para Salesforce, Marketo y Marketo y Salesforce Sync.

## Requisitos previos

1. Instale Marketo Salesforce Sync.

   Dispone de información y del plugin más reciente para Salesforce Sync [aquí.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/understanding-the-salesforce-sync.html)

1. Instalación de Acrobat Sign para Salesforce.

   Información sobre este plugin está disponible [aquí.](https://helpx.adobe.com/ca/sign/using/salesforce-integration-installation-guide.html)

## Buscar el objeto personalizado

Cuando las configuraciones Sincronización de Marketo Salesforce y Acrobat Sign para Salesforce se han completado, aparecen varias opciones nuevas en el Terminal de administración de Marketo.

![Administrador](assets/adminTab.png)

![Sincronización de objetos](assets/salesforceAdmin.png)

1. Haga clic en **Sincronizar esquema** si es tu primera vez. De lo contrario, haga clic en **Actualizar esquema**.

   ![Actualizar](assets/refreshSchema1.png)

1. Si se está ejecutando la sincronización global, deshabilite haciendo clic en **Deshabilitar la sincronización global**.

   ![Desactivar](assets/disableGlobal.png)

1. Haga clic en **Actualizar esquema**.

   ![Actualizar 2](assets/refreshSchema2.png)

## Sincronizar el objeto personalizado

En el lado derecho, consulte Objetos personalizados basados en clientes potenciales, contactos y cuentas.

**Habilitar sincronización** para los objetos de Candidato si desea enviar un recordatorio cuando un Candidato no ha firmado un acuerdo en Salesforce.

**Habilitar sincronización** para los objetos de Contacto si desea enviar un recordatorio cuando un Contacto no ha firmado un acuerdo en Salesforce.

**Habilitar sincronización** para los objetos de Cuenta si desea enviar un recordatorio cuando una Cuenta no ha firmado un acuerdo en Salesforce.

1. **Habilitar sincronización** para el **Acuerdo** objeto que se muestra bajo el padre deseado (Candidato, Contacto o Cuenta). Haga esto para cualquier otro objeto personalizado que desee sincronizar.

   ![Objeto Acuerdo](assets/agreementObject.png)

1. Los siguientes activos muestran cómo **Habilitar sincronización**.

   ![Sincronización personalizada 1](assets/customObjectSync1.png)

   ![Sincronización personalizada 2](assets/customObjectSync2.png)

## Exponer los campos de objetos personalizados a activadores

1. Mientras la sincronización global esté desactivada, seleccione el objeto personalizado del acuerdo para el que habilitó la sincronización y, a continuación, **Editar campos visibles**.

1. Marque el campo &quot;Nombre del acuerdo&quot; en la columna del activador para mostrarlo en los activadores de acciones de campaña. Marque cualquier otro campo por el que desee filtrar y, a continuación, **Guardar**.

   ![Editar campos visibles 1](assets/editVisible1.png)

   ![Editar campos visibles 2](assets/editVisible2.png)

1. Cuando haya terminado de activar la sincronización en los objetos personalizados y de mostrar los valores del activador, recuerde reactivar la sincronización:

   ![Habilitar global](assets/enableGlobal.png)

## Crear el programa y el token

1. En la sección Actividades de marketing de Marketo, haga clic con el botón derecho en **Actividades de marketing** en la barra izquierda, seleccione **Nueva carpeta de campaña** y ponle un nombre.

   ![Nueva carpeta](assets/newFolder.png)

1. Haga clic con el botón derecho en la carpeta creada y seleccione **Nuevo programa** y ponle un nombre. Deje todo lo demás como predeterminado y, a continuación, haga clic en **Crear**.

   ![Nuevo programa 1](assets/newProgram1.png)

   ![Nuevo programa 2](assets/newProgram2.png)

1. Haga clic en **Mis tokens**, y arrastre  **Script de correo electrónico** al lienzo.

   ![Script de correo electrónico](assets/emailScript.png)

1. Asigne un nombre y, a continuación, haga clic en **Haga clic para editar**.

   ![Nombre y edición](assets/nameAndSave.png)

1. Expandir **Objetos personalizados** en el lado derecho y, a continuación, expanda el **Acuerdo** objeto. Busque y arrastre Nombre del acuerdo, Estado del acuerdo, Fecha de firma y URL de firma al lienzo.

1. Escriba un script de velocidad usando estos tokens para mostrar la URL de acuerdo de un acuerdo que no se firme durante una semana. A continuación se muestra un ejemplo que compara la fecha actual con la Fecha de envío:

   ```
   #foreach($agreement in $echosign_dev1__SIGN_Agreement__cList)
       #if($agreement.echosign_dev1__Status__c == "Out for Signature")
           #set($todayCalObj = $date.toCalendar($date.toDate("yyyy-MM-dd",$date.get('yyyy-MM-dd'))) )
           #set($dateSentCalObj = $date.toCalendar($date.toDate("yyyy-MM-dd",$agreement.echosign_dev1__DateSent__c)) )
           #set($dateDiff = ($todayCalObj.getTimeInMillis() - $dateSentCalObj.getTimeInMillis()) / 86400000 )
   
           #if($dateDiff >= 7)
               #set($agreementName = $agreement.Name)
               #set($agreementURL = $agreement.echosign_dev1__Signing_URL__c.substring(8))
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

1. Haga clic en **Guardar**.

## Crear el recordatorio y añadir personalización

Algunos ejemplos de personalización son: el nombre del firmante, el nombre del acuerdo, un vínculo al acuerdo, etc.

1. Haga clic con el botón derecho en el programa que ha creado y haga clic en **Nuevo activo local**, luego seleccione **Correo electrónico**.

   ![Nuevo correo electrónico](assets/createNewEmail.png)

1. En la nueva pestaña, introduzca un **Nombre** y **Descripción** para el correo electrónico y seleccione una plantilla en el selector de plantillas. Haga clic en **Crear**.

   ![Selector de plantilla](assets/templatePicker.png)

1. Establezca el **Nombre de origen** y **Dirección de origen**.

   ![Correo electrónico recordatorio](assets/reminderEmail.png)

1. Haga clic en el cuerpo del mensaje para activar el editor. Haga clic en el **Insertar token** , busque el token de URL del acuerdo personalizado que ha creado y, a continuación, haga clic en **Insertar**. Termina de personalizar tu correo electrónico y haz clic en **Guardar**.

   ![Insertar token](assets/insertToken.png)

1. Previsualice mediante un perfil que tenga un acuerdo asignado. Debería ver un vínculo a la dirección URL con el nombre del acuerdo como etiqueta.

   ![Vínculo de correo electrónico](assets/emailLink.png)

## Configurar el filtro de Smart Campaign

1. Haga clic con el botón derecho en el programa que creó y, a continuación, haga clic en **Nueva campaña inteligente**.

   ![Smart Campaign 1](assets/smartCampaign1.png)

1. Asigne un nombre a su elección y, a continuación, haga clic en **Crear**.

   ![Smart Campaign 2](assets/smartCampaign2.png)

1. Busque y, a continuación, haga clic y arrastre **Tiene acuerdo** a la lista inteligente.

   ![Tiene acuerdo](assets/hasAgreement.png)

1. Los campos que expuso al activador ahora deben estar disponibles en **Agregar restricción**. Seleccionar **Estado del acuerdo** y cualquier otro campo por el que desee filtrar. Para cada campo añadido, defina los valores por los que filtrar. En este caso, solo se activará cuando el **Estado del acuerdo** está Enviado para firmar y **Fecha de envío** está en el pasado antes de 7 días.

   ![Estado del acuerdo](assets/agreementStatus.png)

   >[!NOTE]
   >
   > d un identificador único para las restricciones, como **Nombre del acuerdo**, si desea que esta campaña se ejecute solo para determinados acuerdos.

1. Confirma el público de la campaña y comprueba quién cumple los requisitos en la pestaña Programación.

   ![Cualificadores](assets/qualifiers.png)

## Configurar el flujo de campaña inteligente

Porque el filtro de campaña **Días sin firmar** , puede utilizar una periodicidad programada para la campaña.

1. Haga clic en el **Flujo** de la Campaña inteligente. Busque y arrastre el **Enviar correo electrónico** en el lienzo y seleccione el correo electrónico de recordatorio que creó en la sección anterior.

   ![Enviar correo electrónico](assets/sendEmail.png)

1. Haga clic en el **Programación** de la Campaña inteligente. Asegúrese de que el flujo de la campaña esté limitado a ejecutarse solo una vez por persona en el **Configuración inteligente de campañas**. A continuación, haga clic en el **Programar periodicidad** .

   ![Ficha Programación](assets/scheduleTab.png)

1. Establezca el **Programación** a Diario, elija un día y una hora de inicio y una fecha de finalización para la campaña si es necesario.

   ![Configuración de programación](assets/scheduleSettings.png)

>[!TIP]
>
>Este tutorial forma parte del curso [Agiliza los ciclos de ventas con Acrobat Sign para Salesforce y Marketo](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) que está disponible de forma gratuita en el Experience League!
