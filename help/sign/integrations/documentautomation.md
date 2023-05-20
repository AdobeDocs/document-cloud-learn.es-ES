---
title: Automatización de documentos con Acrobat Sign para Microsoft Power Platform
description: Obtenga información sobre cómo activar y usar los conectores de Acrobat Sign y Adobe PDF Tools para Microsoft Power Apps. Crea flujos de trabajo que automatizan los procesos de aprobación y firma de la empresa de forma rápida y segura sin ningún código
role: User, Developer
level: Intermediate
topic: Integrations
thumbnail: KT-7488.jpg
kt: 7488
exl-id: 4113bc3f-293c-44a8-94ab-e1dbac74caed
source-git-commit: e02b1250de94ec781e7984c6c146dbae993f5d31
workflow-type: tm+mt
source-wordcount: '2436'
ht-degree: 1%

---

# Automatización de documentos con Acrobat Sign para Microsoft Power Platform

Obtenga información sobre cómo activar y usar los conectores de Acrobat Sign y Adobe PDF Tools para Microsoft Power Apps. Crea flujos de trabajo que automatizan los procesos de aprobación y firma de la empresa de forma rápida y segura sin ningún código. Este tutorial práctico consta de cuatro partes que se describen en los vínculos siguientes:

<table style="table-layout:fixed">
<tr>
  <td>
    <a href="documentautomation.md#part1">
        <img alt="Parte 1: Almacenar acuerdo firmado en SharePoint con Acrobat Sign" src="assets/documentautomation/AutomationPart1_thumb.jpg" />
    </a>
    <div>
    <a href="documentautomation.md#part1"><strong>Parte 1: Almacenar acuerdo firmado en SharePoint con Acrobat Sign</strong></a>
    </div>
  </td>
  <td>
    <a href="documentautomation.md#part2">
        <img alt="Parte 2: Proceso de aprobación automatizado para obtener firmas electrónicas con Acrobat Sign" src="assets/documentautomation/AutomationPart2_thumb.jpg" />
    </a>
    <div>
    <a href="documentautomation.md#part2"><strong>Parte 2: Proceso de aprobación automatizado para obtener firmas electrónicas con Acrobat Sign</strong></a>
    </div>
  </td>
  <td>
   <a href="documentautomation.md#part3">
      <img alt="Parte 3: OCR de documento automatizado con Adobe PDF Tools" src="assets/documentautomation/AutomationPart3_thumb.jpg" />
   </a>
    <div>
    <a href="documentautomation.md#part3"><strong>Parte 3: OCR de documento automatizado con Adobe PDF Tools</strong></a>
    </div>
  </td>
  <td>
   <a href="documentautomation.md#part4">
      <img alt="Parte 4: Ensamblaje automatizado de documentos con Adobe PDF Tools" src="assets/documentautomation/AutomationPart4_thumb.jpg" />
   </a>
    <div>
    <a href="documentautomation.md#part4"><strong>Parte 4: Ensamblaje automatizado de documentos con Adobe PDF Tools</strong></a>
    </div>
  </td>
</tr>
</table>

## Requisitos previos

* Familiaridad de Microsoft 365 y Power Automate
* Conocimientos de Acrobat Sign
* Cuenta de Microsoft 365 con acceso a SharePoint y Power Automate (básica para Acrobat Sign y premium para Adobe PDF Tools)
* Cuenta de desarrollador de Acrobat Sign para empresas o Acrobat Sign

**Ejercicios 1 y 2**

* Cuenta de Acrobat Sign con acceso a la API. Una cuenta de desarrollador o una cuenta de empresa.
* Sitio de SharePoint al que puede acceder Power Automate y en el que tiene permisos de edición. Se recomienda el acceso completo de administrador.
* Documento de muestra para la solicitud de aprobación de la firma y la firma.

**Ejercicios 3 y 4**

Descargar materiales [aquí](https://github.com/benvanderberg/adobe-sign-pdftools-powerautomate-tutorial)

## Parte 1: Almacenar acuerdo firmado en SharePoint con Acrobat Sign {#part1}

En la primera parte, utilizarás una plantilla de Power Automate Flow para configurar un flujo de trabajo automatizado que guardará todos los acuerdos firmados en tu sitio de SharePoint.

1. Vaya a Power Automate.
1. Busque Acrobat Sign.

   ![Captura de pantalla de la navegación a Power Automate](assets/documentautomation/automation_1.png)

1. Elegir **Guardar un acuerdo completado de Acrobat Sign en la biblioteca de SharePoint**.

   ![Captura de pantalla de la acción Guardar un acuerdo completado de Acrobat Sign en la biblioteca de SharePoint](assets/documentautomation/automation_2.png)

1. Revise la pantalla y configure las conexiones necesarias. Habilite la conexión de Acrobat Sign.
1. Haga clic en el icono `+` símbolo.

   ![Captura de pantalla de la conexión de flujo de Acrobat Sign y SharePoint](assets/documentautomation/automation_3.png)

1. Introduzca el correo electrónico de su cuenta de Acrobat Sign y haga clic en el campo de la contraseña en la nueva ventana.

   ![Captura de pantalla de la pantalla de inicio de sesión de Acrobat Sign](assets/documentautomation/automation_4.png)

   Espera un momento a que el Adobe compruebe tu cuenta.

   >[!NOTE]
   >
   >Esta comprobación le dirigirá al inicio de sesión adecuado si está utilizando un Adobe ID o nuestro SSO corporativo.

1. Complete el inicio de sesión.
1. Haga clic en **Continuar** para ir a la pantalla Edición de flujo .
1. Asigne un nombre al activador.

   ![Captura de pantalla de asignación del nombre al activador](assets/documentautomation/automation_5.png)

1. Configure las opciones de SharePoint.

   ![Captura de pantalla de la configuración de SharePoint](assets/documentautomation/automation_6.png)

   **Dirección del sitio:** Tu sitio de SharePoint
   **Ruta de carpeta:** Ruta a los documentos compartidos que desea utilizar
   **Nombre de archivo:** Aceptar el valor predeterminado
   **Contenido del archivo:** Aceptar el valor predeterminado

1. Guardar el flujo.

   ![Captura de pantalla del icono Guardar](assets/documentautomation/automation_7.png)

1. Vaya a la pantalla de información general de flujo con la flecha azul hacia atrás. Probará este flujo en la parte 2.

   ![Captura de pantalla de la pantalla de resumen de flujo](assets/documentautomation/automation_8.png)

Probará este flujo en la siguiente parte.

## Parte 2: Proceso de aprobación automatizado para obtener firmas electrónicas con Acrobat Sign {#part2}

En la segunda parte, construimos la primera parte con un Flow más robusto y probamos ambos Flow para verlos en acción.

1. Seleccionar **Plantillas** en el lado izquierdo de la interfaz de Power Automate.

   ![Captura de pantalla de selección de plantillas](assets/documentautomation/automation_9.png)

1. Busque &quot;aprobación del responsable&quot;.
1. Seleccionar **Solicitar la aprobación del administrador para un archivo seleccionado**.

   ![Captura de pantalla de selección de Solicitar aprobación del administrador para un archivo seleccionado](assets/documentautomation/automation_10.png)

   Revise las conexiones y añada las que falten.

   >[!NOTE]
   >
   >Si este es el primer flujo que está haciendo con las aprobaciones, se configurarán completamente cuando se ejecute el flujo.

1. Haga clic en **Continuar** para ir a la pantalla edición de flujo.

   Este flujo tiene muchos pasos preconfigurados, incluida la comprobación de errores y pasos condicionales anidados.

1. Configurar **Para un archivo seleccionado** como sigue:
   **Dirección del sitio:** Tu sitio de SharePoint
   **Nombre de biblioteca:** Su repositorio de documentos
1. Añada una entrada de la siguiente manera:
   **Tipo**: Correo electrónico
   **Nombre**: Correo electrónico del firmante

   ![Captura de pantalla de configuración del flujo](assets/documentautomation/automation_11.png)

1. Configurar **Obtener propiedades de archivo:** como sigue:
   **Dirección del sitio:** Tu sitio de SharePoint
   **Nombre de biblioteca:** Su repositorio de documentos

1. Desplácese hacia abajo y busque **En caso afirmativo**.

   ![Captura de pantalla de la configuración If yes](assets/documentautomation/automation_12.png)

1. Haga clic en **Añadir una acción** en el **En caso afirmativo** (no el que aparece más abajo) para agregar los pasos que se van a enviar para firmar.

   ![Captura de pantalla de adición de una acción en el cuadro Si es así](assets/documentautomation/automation_13.png)

1. Buscar por **SharePoint obtener contenido de archivo** y elija **Obtener contenido del archivo**.

   ![Captura de pantalla del cuadro de búsqueda](assets/documentautomation/automation_14.png)

1. Configure el **Obtener contenido del archivo** como sigue:

   ![Captura de pantalla de la configuración de contenido de Obtener archivo](assets/documentautomation/automation_15.png)

   **Dirección del sitio:** Tu sitio de SharePoint.
   **Identificador de archivo:** Busque &quot;identificador&quot; y elija Identificador en el **Obtener propiedades de archivo** paso.
1. Busque &quot;Adobe&quot; y elija **Acrobat Sign** para agregar otra acción.

   ![Captura de pantalla del menú de búsqueda](assets/documentautomation/automation_16.png)

1. Introduce &quot;cargar&quot; en el cuadro de búsqueda de Acrobat Sign y selecciona **Cargar un documento y obtener un ID de documento**.
1. Buscar la variable dinámica **Nombre** para obtener el nombre del elemento/documento seleccionado en el activador en **Nombre de archivo**.
1. Haga clic en **Expresión** en el asistente variable bajo **Contenido del archivo**.

   ![Captura de pantalla de la pantalla Cargar un documento y obtener un ID de documento](assets/documentautomation/automation_17.png)

1. Añada un solo apóstrofo y, a continuación, haga clic en volver a **Contenido dinámico**, eliminar el apóstrofo, seleccione **Contenido del archivo** y haga clic en **OK**.

   Asegúrese de que no haya apóstrofos adicionales y que se parezca a la muestra siguiente.

   ![Captura de pantalla del aspecto que debería tener la pantalla Contenido dinámico](assets/documentautomation/automation_18.png)

1. Busque &quot;crear&quot; en el área de búsqueda de Acrobat Sign para añadir otra acción de Acrobat Sign.
1. Seleccionar **Crear y firmar un acuerdo desde un documento cargado y enviarlo a firmar**.

   ![Captura de pantalla de la búsqueda de crear](assets/documentautomation/automation_19.png)

1. Configure la información necesaria: Elegir **Nombre** del asistente de variable dinámica en **Nombre del acuerdo**.
Elegir **ID de documento** del asistente de variable dinámica en **ID de documento**.
Elegir **Correo electrónico del firmante** del asistente de variable dinámica en **Correo electrónico del participante**.
Introduzca &quot;1&quot; en **Orden del participante**.
Elegir **Firmante** del menú desplegable en **Función de participante**.

   ![Captura de pantalla de la información requerida](assets/documentautomation/automation_20.png)

1. **Guardar** el flujo.

### Probar el flujo

Vaya al repositorio de documentos de su sitio de SharePoint para probarlo.

1. Seleccione el documento y elija **Automatizar** y el **Flujo** acabas de crear.

   ![Captura de pantalla de la selección del menú y flujo Automatizar](assets/documentautomation/automation_21.png)

1. Inicie el flujo para validar las conexiones (solo primera ejecución de flujo).
1. Escriba un mensaje bonito para el aprobador en **Mensaje**.
1. Introduzca un correo electrónico para el documento Firmante en **Correo electrónico del firmante**.
1. Haga clic en **Flujo de ejecución**.

El aprobador configurado para el usuario que inicia el flujo recibirá una solicitud de aprobación. Puede aprobar mediante correo electrónico o mediante el menú Elementos de acción de Power Automate .
Una vez aprobado, firme el documento. Dependiendo de su usuario y si ha iniciado sesión en Sign, es posible que deba abrir las ventanas de firma en una ventana privada del navegador.

![Captura de pantalla de apertura en ventana privada del navegador](assets/documentautomation/automation_22.png)

Complete el proceso de firma y, a continuación, vuelva a buscar en la carpeta SharePoint.

![Captura de pantalla de la carpeta SharePoint](assets/documentautomation/automation_23.png)

## Parte 3: OCR de documento automatizado con Adobe PDF Tools {#part3}

En la tercera parte, aprenderás a automatizar el OCR en los PDF cuando se importan a Microsoft SharePoint. Esto soluciona un problema que se produce con documentos de PDF digitalizados que no se pueden buscar en SharePoint.

![Captura de pantalla del documento de PDF en el navegador](assets/documentautomation/automation_24.png)

### Configurar una carpeta en SharePoint

Vaya a Microsoft SharePoint donde desee almacenar documentos.

1. Haga clic en **+ Nuevo** para crear una nueva carpeta denominada &quot;Contratos procesados&quot;.
1. Haga clic en **+ Nuevo** para crear una nueva carpeta denominada &quot;Contratos antiguos&quot;.

   ![Captura de pantalla de nuevas carpetas](assets/documentautomation/automation_25.png)

Ahora, estas carpetas forman parte del flujo de Power Automate.

### Crear un flujo a partir de una plantilla

1. Inicie sesión en https://flow.microsoft.com.
1. Haga clic en **Plantillas** en la barra lateral.

   ![Captura de pantalla de selección de plantillas](assets/documentautomation/automation_26.png)

1. Seleccionar **Convertir los archivos recién añadidos a un PDF de texto en el que se pueden realizar búsquedas en SharePoint**.
1. Haga clic en **+** junto a Herramientas de Adobe PDF.

   ![Captura de pantalla de selección del símbolo +](assets/documentautomation/automation_27.png)

1. Vaya a https://www.adobe.com/go/powerautomate_getstarted en una nueva pestaña.
1. Haga clic en **Empezar**.

   ![Captura de pantalla del botón Introducción](assets/documentautomation/automation_28.png)

1. Inicie sesión con el Adobe ID.

   ![Captura de pantalla de la pantalla de inicio de sesión](assets/documentautomation/automation_29.png)

1. Introduzca el nombre y la descripción de las credenciales y haga clic en **Crear credenciales**.

   ![Captura de pantalla de la pantalla Crear credenciales](assets/documentautomation/automation_30.png)

   Mantenga la ventana con las credenciales abiertas. Deberá especificarlas en Microsoft Power Automate.

   ![Captura de pantalla de la pestaña del navegador para mantenerla abierta](assets/documentautomation/automation_31.png)

1. Introduzca las credenciales y haga clic en **Crear en Microsoft Power Automate**.

   ![Captura de pantalla de introducción de las credenciales de PDF Tools](assets/documentautomation/automation_32.png)

1. Haga clic en **Continuar**.

   ![Captura de pantalla de dónde hacer clic en Continuar](assets/documentautomation/automation_33.png)

   Ahora puede ver una vista del flujo de trabajo y tendrá que configurarla para su entorno.

1. Seleccione el campo Dirección del sitio y elija el sitio de SharePoint que está utilizando en el activador denominado **Cuando se crea un archivo en una carpeta**.

   ![Captura de pantalla de selección de Cuando se crea un archivo en un activador de carpeta](assets/documentautomation/automation_34.png)

1. Pulse el icono de carpeta para acceder a la carpeta Contratos Antiguos situada en ID de carpeta.

   ![Captura de pantalla de selección de la carpeta Contratos Antiguos](assets/documentautomation/automation_35.png)

1. Edite el **Crear archivo** acción en la parte inferior del flujo:

   Cambiar **Dirección del sitio** a la dirección de su sitio.
Especifique la ubicación de la carpeta Contratos Procesados en la ruta de la carpeta.

1. Haga clic en **Guardar** en la esquina superior derecha.
1. Haga clic en **Prueba**.
1. Seleccionar **Manualmente**.
1. Haga clic en **Prueba**.

   ![Captura de pantalla del flujo de prueba](assets/documentautomation/automation_36.png)

### Prueba tu nuevo flujo

1. Acceda a la carpeta Contratos Antiguos de SharePoint.
1. Acceda a E03/Antiguos Contratos en los archivos de ejercicios que haya descargado.
1. Copie los archivos ReleaseFormXX.pdf en la carpeta Contratos antiguos de SharePoint.

   ![Captura de pantalla de copia de archivos](assets/documentautomation/automation_37.png)

Ahora, si accede a la carpeta Contratos Procesados, podrá ver los PDF disponibles después de que se conceda al flujo unos momentos de ejecución. Si abre los PDF, podrá ver que el texto es seleccionable.
Además, SharePoint indexa el documento, lo que le permite buscar el contenido de sus documentos desde la barra de búsqueda de SharePoint.

## Parte 4: Ensamblaje automatizado de documentos con Adobe PDF Tools {#part4}

En la cuarta parte, aprenderás a combinar muchos documentos según la información proporcionada al seleccionar e iniciar un flujo desde Microsoft SharePoint. En este escenario, el flujo:

* Pida información para elegir qué incluir en un paquete para un cliente.
* En función de la información proporcionada, combina muchos documentos. Estos documentos incluyen una portada y documentos técnicos opcionales.
* El documento combinado se guarda en SharePoint.

### Importar archivos de ejercicios a SharePoint

1. Abra la carpeta E04 en los archivos del ejercicio.
1. Importe las carpetas Propuesta, Plantillas y Documentos generados en SharePoint.

   ![Captura de pantalla de importación de carpetas](assets/documentautomation/automation_38.png)

Estas carpetas se utilizarán como referencia. En concreto, utilizará el archivo Propuesta.docx para su propuesta.

En la carpeta Plantillas, hay una carpeta Portadas que incluye diseños de portadas para diferentes ciudades. También hay una carpeta de documentos técnicos que contiene documentos técnicos adicionales opcionales que se adjuntarán al final si se selecciona.

### Importar el flujo en Microsoft Power Automate

1. Inicie sesión en Microsoft Power Automate (https://flow.microsoft.com).
1. Haga clic en **Mis flujos**.

   ![Captura de pantalla de dónde seleccionar Mis flujos](assets/documentautomation/automation_39.png)

1. Haga clic en **Importar**.

   ![Captura de pantalla de importación](assets/documentautomation/automation_40.png)

1. Haga clic en **Cargar** y elija la carpeta GenerateProposal_20210311231623.zip en E04/Flows/.

   ![Captura de pantalla de selección de carpeta](assets/documentautomation/automation_41.png)

1. Haga clic en **Importar**.

1. Haga clic en el icono de llave inglesa en Acción junto a **Enviar propuesta al cliente**.

   ![Captura de pantalla del icono de llave inglesa](assets/documentautomation/automation_42.png)

1. Seleccionar **Crear como nuevo** en Configuración.
1. Establezca el nombre del flujo en Nombre del recurso.
1. Haga clic en **Guardar**.

   Repita este procedimiento para los otros recursos relacionados y seleccione la conexión.

   ![Captura de pantalla del almacenamiento del archivo](assets/documentautomation/automation_43.png)

1. Haga clic en **Importar** después de haber hecho todas sus conexiones.

### Establecer para un archivo seleccionado

Una vez creado el flujo, haga lo siguiente:

1. Haga clic en **Editar**.

   ![Captura de pantalla de dónde seleccionar la edición](assets/documentautomation/automation_44.png)

1. Seleccione el activador **Para un archivo seleccionado**.

   Añada su sitio de SharePoint en la Dirección del sitio.
Agregue su biblioteca a la biblioteca.

   ![Captura de pantalla del activador completado](assets/documentautomation/automation_45.png)

### Establecer templateFolderPath

1. Haga clic en la variable templateFolderPath.
1. Establezca la ruta de acceso a la ubicación de la carpeta Templates dentro del sitio de SharePoint que ha importado.

### Definir portada Obtener contenido del archivo

1. Haga clic en **Cubrir** , que expande el ámbito.
1. Expandir **Portada: Obtener contenido del archivo**.

   Establezca Dirección del sitio en el sitio de SharePoint.

   ![Captura de pantalla de la cubierta expandida](assets/documentautomation/automation_46.png)



### Definir archivo seleccionado

1. Expanda la **Archivo seleccionado** acción de ámbito.

   Cambie la dirección del sitio y el nombre de la biblioteca por el sitio de SharePoint y la biblioteca, respectivamente, en **Obtener propiedades de archivo**.
Cambie la dirección del sitio a su sitio de SharePoint en **Obtener contenido del archivo**.

   ![Captura de pantalla de la acción expandida Archivo seleccionado](assets/documentautomation/automation_47.png)

### Definir informes técnicos

1. Haga clic en **Informes** acción.
1. Expandir **Condición: Añadir informe técnico**.

   ![Captura de pantalla de la condición expandida Añadir informe técnico](assets/documentautomation/automation_48.png)

1. Expandir **Informe técnico 1: Obtener contenido del archivo mediante la ruta**.
Editar la dirección del sitio en el sitio de SharePoint especificado.

Repita los mismos pasos para **Condición: Añadir informe técnico 2**.

### Establecer Crear archivo

1. Expandir **Crear archivo**.

   Editar la dirección del sitio y la ruta de la carpeta en el sitio de SharePoint y la ruta de acceso donde se encuentra la carpeta Documentos generados.

1. Haga clic en **Guardar**.

### Prueba del flujo

1. Vaya a la carpeta de propuestas en SharePoint.
1. Seleccione la carpeta Propuesta.docx .

   ![Captura de pantalla de selección de carpeta de propuestas](assets/documentautomation/automation_49.png)

1. Seleccione el flujo en la **Automatizar** menú.

   ![Captura de pantalla de Selección del menú Automatizar](assets/documentautomation/automation_50.png)

1. Haga clic en **Continuar** para comenzar el flujo.

   ![Captura de pantalla de la selección del botón Continuar](assets/documentautomation/automation_51.png)

1. Elija la portada y los documentos técnicos que desee adjuntar.
1. Haga clic en **Flujo de ejecución**.

   ![Captura de pantalla del botón Ejecutar flujo](assets/documentautomation/automation_52.png)

Vaya a la carpeta Generar documentos . Ahora debería ver el archivo de PDF generado.

![Captura de pantalla del directorio de SharePoint con el nuevo archivo de PDF](assets/documentautomation/automation_53.png)

### Adición de Protect y otras acciones al flujo

Ahora que ha creado correctamente un flujo, va a editar el flujo para cifrar el documento de PDF con una contraseña. Esto también explica cómo puede utilizar otras acciones.

1. Vuelve al final del flujo.
1. Haga clic en **+** símbolo entre **Combinar PDF** y **Crear archivo**.

   ![Captura de pantalla de dónde seleccionar el símbolo +](assets/documentautomation/automation_54.png)

1. Seleccionar **Añadir una acción**.
1. Busque &quot;Herramientas de Adobe PDF&quot;.

   ![Captura de pantalla de la búsqueda de Adobe PDF](assets/documentautomation/automation_55.png)

1. Seleccionar **PDF de Protect desde la visualización**.
1. Utilice Contenido dinámico para definir el campo Nombre de archivo en **Nombre de archivo del PDF del PDF de combinación**.

   ![Captura de pantalla de contenido dinámico](assets/documentautomation/automation_56.png)

   En el activador, hay un campo Contraseña que forma parte del formulario de inicio. Podemos usar eso aquí.

1. Buscar por **Campo de contraseña** mediante contenido dinámico y colóquelo en el campo Contraseña.

   ![Captura de pantalla de búsqueda de contraseña](assets/documentautomation/automation_57.png)

1. Usar contenido dinámico para configurarlo **Contenido de archivo de PDF de PDF de combinación** en el campo Contenido del archivo.
1. Cambie el **Crear archivo** para obtener el contenido del archivo de Protect PDF en lugar de Fusionar PDF.
1. Expandir **Crear archivo**.
1. Borre el campo Contenido del archivo.
1. Usar contenido dinámico para colocar **Contenido de archivo de PDF** desde **PDF de Protect desde la visualización**.

### Prueba del flujo

1. Vaya a la carpeta de propuestas en SharePoint.
1. Seleccione Propuesta.docx.

   ![Captura de pantalla de selección de carpeta Propuesta](assets/documentautomation/automation_58.png)

1. Seleccionar **Automatizar** para elegir tu flujo.

   ![Captura de pantalla de la selección de Automatizar en el menú](assets/documentautomation/automation_59.png)

1. Haga clic en **Continuar** para comenzar el flujo.

   ![Captura de pantalla de la selección Continuar](assets/documentautomation/automation_60.png)

1. Elija la portada y los documentos técnicos que desee adjuntar.
1. Establezca el campo Contraseña en la Contraseña que desea establecer.
1. Haga clic en **Flujo de ejecución**.

   ![Captura de pantalla de los archivos seleccionados y botón Ejecutar flujo](assets/documentautomation/automation_61.png)

1. Vaya a la carpeta Generar documentos .
Debería ver el archivo de PDF generado. Abra el archivo de PDF y le pedirá que introduzca su contraseña de PDF.

   ![Captura de pantalla del PDF generado en el directorio de SharePoint](assets/documentautomation/automation_62.png)
