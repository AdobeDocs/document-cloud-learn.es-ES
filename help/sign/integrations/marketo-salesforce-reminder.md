---
title: Enviar recordatorios con Acrobat Sign para Salesforce y la Guía de configuración de Marketo
description: Obtenga información sobre cómo enviar un recordatorio por correo electrónico desde Marketo cuando un acuerdo permanece sin firmar después de un período de tiempo
feature: Integrations
role: Admin
solution: Acrobat Sign, Marketo Engage, Document Cloud
level: Intermediate
topic: Integrations
jira: KT-7248
topic-revisit: Integrations
thumbnail: KT-7248.jpg
exl-id: 33aca2e0-2f27-4100-a16f-85ba652c17a3
source-git-commit: a88ec5a68aa2a02ec2f118332ec31f47d3d5d300
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 0%

---

# Enviar recordatorios con Acrobat Sign para Salesforce y la Guía de configuración de Marketo

Obtenga información sobre cómo enviar un recordatorio por correo electrónico desde Marketo cuando un acuerdo permanece sin firmar después de un período de tiempo. Esta integración utiliza Acrobat Sign, Acrobat Sign para Salesforce, Marketo y Marketo y Salesforce Sync.

## Requisitos previos

1. Instale Marketo Salesforce Sync.

   La información y el complemento más reciente para la sincronización de Salesforce están disponibles [aquí.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/understanding-the-salesforce-sync.html?lang=es)

1. Instale Acrobat Sign para Salesforce.

   La información sobre este complemento está disponible [aquí.](https://helpx.adobe.com/ca/sign/using/salesforce-integration-installation-guide.html)

## Buscar el objeto personalizado

Cuando se completan las configuraciones de Sincronización de Marketo Salesforce y Acrobat Sign para Salesforce , aparecen varias opciones nuevas en el Terminal de administración de Marketo.

![Administrador](assets/adminTab.png)

![Sincronización de objetos](assets/salesforceAdmin.png)

1. Haga clic en **Sincronizar esquema** si es la primera vez que lo hace. De lo contrario, haga clic en **Actualizar esquema**.

   ![Actualizar](assets/refreshSchema1.png)

1. Si se está ejecutando la sincronización global, deshabilítela haciendo clic en **Deshabilitar sincronización global**.

   ![Deshabilitar](assets/disableGlobal.png)

1. Haga clic en **Actualizar esquema**.

   ![Actualizar 2](assets/refreshSchema2.png)

## Sincronizar el objeto personalizado

En el lado derecho, consulte Objetos personalizados basados en clientes potenciales, contactos y cuentas.

**Habilite la sincronización** para los objetos en Candidato si desea enviar un recordatorio cuando un Candidato no haya firmado un acuerdo en Salesforce.

**Habilite la sincronización** para los objetos en Contacto si desea enviar un recordatorio cuando un contacto no ha firmado un acuerdo en Salesforce.

**Habilite la sincronización** para los objetos de Cuenta si desea enviar un recordatorio cuando una Cuenta no haya firmado un acuerdo en Salesforce.

1. **Habilite la sincronización** para el objeto **Acuerdo** que se muestra debajo del elemento principal deseado (Candidato, Contacto o Cuenta). Haga esto para cualquier otro objeto personalizado que desee sincronizar.

   ![Objeto de acuerdo](assets/agreementObject.png)

1. Los siguientes activos muestran cómo **Habilitar sincronización**.

   ![Sincronización personalizada 1](assets/customObjectSync1.png)

   ![Sincronización personalizada 2](assets/customObjectSync2.png)

## Exponer los campos de objetos personalizados a los activadores

1. Mientras esté desactivada la sincronización global, seleccione el objeto personalizado del acuerdo para el que habilitó la sincronización y, a continuación, **Editar campos visibles**.

1. Marque el campo &quot;Nombre del acuerdo&quot; en la columna del activador para mostrarlo en los activadores de acciones de campaña. Comprueba cualquier otro campo por el que desees filtrar, después **Guarda**.

   ![Editar campos visibles 1](assets/editVisible1.png)

   ![Editar campos visibles 2](assets/editVisible2.png)

1. Cuando haya terminado de activar la sincronización en los objetos personalizados y de mostrar los valores del activador, recuerde reactivar la sincronización:

   ![Habilitar global](assets/enableGlobal.png)

## Crear el programa y el token

1. En la sección Actividades de marketing de Marketo, haga clic con el botón derecho en **Actividades de marketing** en la barra izquierda, seleccione **Nueva carpeta de campaña** y asígnele un nombre.

   ![Nueva carpeta](assets/newFolder.png)

1. Haga clic con el botón derecho en la carpeta creada, seleccione **Nuevo programa** y asígnele un nombre. Deja todo lo demás como predeterminado y luego haz clic en **Crear**.

   ![Nuevo programa 1](assets/newProgram1.png)

   ![Nuevo programa 2](assets/newProgram2.png)

1. Haz clic en **Mis tokens** y arrastra **Script de correo electrónico** al lienzo.

   ![Script de correo electrónico](assets/emailScript.png)

1. Dale un nombre y, a continuación, haz clic en **Clic para editar**.

   ![Asignar nombre y editar](assets/nameAndSave.png)

1. Expanda **Objetos personalizados** en el lado derecho y, a continuación, expanda el objeto **Acuerdo**. Busque y arrastre Nombre del acuerdo, Estado del acuerdo, Fecha de firma y URL de firma al lienzo.

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

Entre los ejemplos de personalización se incluyen: el nombre del firmante, el nombre del acuerdo, un vínculo al acuerdo, etc.

1. Haz clic con el botón derecho en el programa que has creado, haz clic en **Nuevo activo local** y selecciona **Correo electrónico**.

   ![Nuevo correo electrónico](assets/createNewEmail.png)

1. En la nueva pestaña, introduzca un **Nombre** y una **Descripción** para el correo electrónico y seleccione una plantilla en el selector de plantillas. Haga clic en **Crear**.

   ![Selector de plantilla](assets/templatePicker.png)

1. Establezca **Nombre de origen** y **Dirección de origen**.

   ![Correo electrónico de recordatorio](assets/reminderEmail.png)

1. Haga clic en el cuerpo del mensaje para activar el editor. Haga clic en el botón **Insertar token**, busque el token de URL de acuerdo personalizado que creó y, a continuación, haga clic en **Insertar**. Termina de personalizar tu correo electrónico y haz clic en **Guardar**.

   ![Insertar token](assets/insertToken.png)

1. Previsualice mediante un perfil que tenga un acuerdo asignado. Debería ver un vínculo a la dirección URL con el nombre del acuerdo como etiqueta.

   ![Vínculo de correo electrónico](assets/emailLink.png)

## Configurar el filtro de Smart Campaign

1. Haz clic con el botón derecho en el programa que has creado y, a continuación, haz clic en **Nueva campaña inteligente**.

   ![Smart Campaign 1](assets/smartCampaign1.png)

1. Dale el nombre que quieras y, a continuación, haz clic en **Crear**.

   ![Smart Campaign 2](assets/smartCampaign2.png)

1. Busque y, a continuación, haga clic y arrastre **Tiene acuerdo** a la lista inteligente.

   ![Tiene acuerdo](assets/hasAgreement.png)

1. Los campos que expuso al desencadenador ahora deben estar disponibles en **Agregar restricción**. Seleccione **Estado del acuerdo** y cualquier otro campo por el que desee filtrar. Para cada campo añadido, defina los valores por los que filtrar. En este caso, solo se activará cuando el **Estado del acuerdo** esté Enviado para firmar y la **Fecha de envío** esté en el pasado antes de los 7 días.

   ![Estado del acuerdo](assets/agreementStatus.png)

   >[!NOTE]
   >
   > d un identificador único para las restricciones, como **Nombre del acuerdo**, si desea que esta campaña se ejecute solo para determinados acuerdos.

1. Confirma el público de la campaña y comprueba quién cumple los requisitos en la pestaña Programación.

   ![Calificadores](assets/qualifiers.png)

## Configurar el flujo de campaña inteligente

Dado que se utilizó el filtro de campaña **Días sin firmar**, puede utilizar una periodicidad programada para la campaña.

1. Haz clic en la pestaña **Flujo** en Smart Campaign. Busque y arrastre el flujo **Enviar correo electrónico** al lienzo y seleccione el correo electrónico de recordatorio que creó en la sección anterior.

   ![Enviar correo electrónico](assets/sendEmail.png)

1. Haz clic en la pestaña **Programar** en Smart Campaign. Asegúrese de que el flujo de la campaña esté limitado para ejecutarse solo una vez por persona en **Configuración inteligente de la campaña**. Luego, haz clic en la pestaña **Programar periodicidad**.

   ![Ficha Programación](assets/scheduleTab.png)

1. Establece **Schedule** en Daily, elige un día y una hora de inicio y una fecha de finalización para la campaña si es necesario.

   ![Configuración de programación](assets/scheduleSettings.png)

