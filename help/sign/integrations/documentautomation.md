---
title: Automatización de documentos con Adobe Sign para Microsoft Power Platform
description: Aprenda a activar y utilizar los conectores de Adobe Sign y Adobe PDF Tools para Microsoft Power Apps. Crear flujos de trabajo que automaticen los procesos de aprobación y firma del negocio de forma rápida y segura sin ningún código
role: User, Developer
level: Intermediate
topic: Integrations
thumbnail: KT-7488.jpg
kt: 7488
exl-id: 4113bc3f-293c-44a8-94ab-e1dbac74caed
source-git-commit: 018cbcfd1d1605a8ff175a0cda98f0bfb4d528a8
workflow-type: tm+mt
source-wordcount: '2436'
ht-degree: 0%

---

# Automatización de documentos con Adobe Sign para Microsoft Power Platform

Aprenda a activar y utilizar los conectores de Adobe Sign y Adobe PDF Tools para Microsoft Power Apps. Cree flujos de trabajo que automaticen los procesos de aprobación y firma empresarial de forma rápida y segura sin necesidad de utilizar código. Este tutorial práctico consta de cuatro partes y se describe en los vínculos siguientes:

<table style="table-layout:fixed">
<tr>
  <td>
    <a href="documentautomation.md#part1">
        <img alt="Parte 1: Almacenar un acuerdo firmado en SharePoint con Adobe Sign" src="assets/documentautomation/AutomationPart1_thumb.jpg" />
    </a>
    <div>
    <a href="documentautomation.md#part1"><strong>Parte 1: Almacenar un acuerdo firmado en SharePoint con Adobe Sign</strong></a>
    </div>
  </td>
  <td>
    <a href="documentautomation.md#part2">
        <img alt="Parte 2: Proceso de aprobación automatizado para obtener la firma electrónica con Adobe Sign" src="assets/documentautomation/AutomationPart2_thumb.jpg" />
    </a>
    <div>
    <a href="documentautomation.md#part2"><strong>Parte 2: Proceso de aprobación automatizado para obtener la firma electrónica con Adobe Sign</strong></a>
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
      <img alt="Parte 4: Conjunto automatizado de documentos con Adobe PDF Tools" src="assets/documentautomation/AutomationPart4_thumb.jpg" />
   </a>
    <div>
    <a href="documentautomation.md#part4"><strong>Parte 4: Conjunto automatizado de documentos con Adobe PDF Tools</strong></a>
    </div>
  </td>
</tr>
</table>

## Requisitos previos

* Microsoft 365 y Power Automatizar la familiaridad
* Conocimiento de Adobe Sign
* Cuenta de Microsoft 365 con acceso a SharePoint y Power Automate (básica para Adobe Sign, Premium para Adobe PDF Tools)
* Cuenta de desarrollador de Adobe Sign para empresas o Adobe Sign

**Ejercicios 1 y 2**

* Cuenta de Adobe Sign con acceso a la API. Una cuenta de desarrollador o una cuenta de empresa.
* Sitio de SharePoint al que puede acceder Power Automatizar para el que tiene permisos de edición. Se recomienda el acceso de administrador completo.
* Documento de muestra para la solicitud de aprobación de firma y la firma.

**Ejercicios 3 y 4**

Descargar materiales [aquí](https://github.com/benvanderberg/adobe-sign-pdftools-powerautomate-tutorial)

## Parte 1: Almacenar un acuerdo firmado en SharePoint con Adobe Sign {#part1}

En la primera parte, usará una plantilla de flujo de trabajo Power Automate para configurar un flujo de trabajo automatizado que guardará todos los acuerdos firmados en su sitio de SharePoint.

1. Vaya a Power Automate.
1. Buscar Adobe Sign.

   ![Captura de pantalla de la navegación a Power Automate](assets/documentautomation/automation_1.png)

1. Elija **Guardar un acuerdo completado por Adobe Sign en la biblioteca de SharePoint**.

   ![Captura de pantalla de Guardar un acuerdo completado por Adobe Sign en la acción de biblioteca de SharePoint](assets/documentautomation/automation_2.png)

1. Revise la pantalla y configure las conexiones necesarias. Habilite la conexión de Adobe Sign.
1. Haga clic en el símbolo azul `+`.

   ![Captura de pantalla de la conexión de flujo de Adobe Sign y SharePoint](assets/documentautomation/automation_3.png)

1. Introduzca el correo electrónico de su cuenta de Adobe Sign y haga clic en el campo de contraseña en la nueva ventana.

   ![Captura de pantalla de inicio de sesión de Adobe Sign](assets/documentautomation/automation_4.png)

   Espere un momento para que el Adobe compruebe su cuenta.

   >[!NOTE]
   >
   >Esta comprobación le dirigirá al inicio de sesión adecuado si utiliza un Adobe ID o nuestro SSO corporativo.

1. Inicio de sesión completo.
1. Haga clic en **Continuar** para ir a la pantalla de edición de Flow.
1. Asigne un nombre al activador.

   ![Captura de pantalla del nombre del activador](assets/documentautomation/automation_5.png)

1. Configure la configuración de SharePoint.

   ![Captura de pantalla de la configuración de SharePoint](assets/documentautomation/automation_6.png)

   **Dirección del sitio:** su sitio de SharePoint
   **Ruta de carpeta:** ruta a los documentos compartidos que desea utilizar
   **Nombre de archivo:** aceptar el valor predeterminado
   **Contenido del archivo:** aceptar el valor predeterminado

1. Guardar el flujo.

   ![Captura de pantalla del icono Guardar](assets/documentautomation/automation_7.png)

1. Vaya a la pantalla de información general de flujo con la flecha azul hacia atrás. Probará este flujo en la parte 2.

   ![Captura de pantalla de la pantalla de información general del flujo](assets/documentautomation/automation_8.png)

Probará este flujo en la siguiente parte.

## Parte 2: Proceso de aprobación automatizado para obtener la firma electrónica con Adobe Sign {#part2}

En la segunda parte, construimos la primera parte con un flujo más robusto y probamos ambos flujos para verlos en acción.

1. Seleccione **Plantillas** en el lado izquierdo de la interfaz de Power Automate.

   ![Captura de pantalla de selección de plantillas](assets/documentautomation/automation_9.png)

1. Busque &quot;aprobación del responsable&quot;.
1. Seleccione **Aprobación del administrador de solicitudes para un archivo seleccionado**.

   ![Captura de pantalla de selección de la aprobación del gestor de solicitudes para un archivo seleccionado](assets/documentautomation/automation_10.png)

   Revise las conexiones y añada las que le falten.

   >[!NOTE]
   >
   >Si este es el primer flujo que se realiza con las aprobaciones, se configurarán completamente cuando se ejecute el flujo.

1. Haga clic en **Continuar** para ir a la pantalla de edición de flujo.

   Este flujo tiene muchos pasos preconfigurados, como la comprobación de errores y los pasos condicionales anidados.

1. Configure **para un archivo seleccionado** como se indica a continuación:
   **Dirección del sitio:** su sitio de SharePoint
   **Nombre de la biblioteca:** repositorio de documentos
1. Añada una entrada como se indica a continuación:
   **Tipo**: Correo electrónico
   **Nombre**: Correo electrónico del firmante

   ![Captura de pantalla de configuración del flujo](assets/documentautomation/automation_11.png)

1. Configure **Obtener propiedades de archivo:** de la siguiente manera:
   **Dirección del sitio:** su sitio de SharePoint
   **Nombre de la biblioteca:** repositorio de documentos

1. Desplácese hacia abajo y busque **If yes**.

   ![Captura de pantalla de la configuración If yes](assets/documentautomation/automation_12.png)

1. Haga clic en **Agregar una acción** en el cuadro **Si sí** (no en la parte inferior de la lista) para agregar los pasos para enviar para firmar.

   ![Captura de pantalla de adición de una acción en el cuadro Si es](assets/documentautomation/automation_13.png)

1. Busque **SharePoint obtener contenido de archivo** y elija **Obtener contenido de archivo**.

   ![Captura de pantalla del cuadro de búsqueda](assets/documentautomation/automation_14.png)

1. Configure el **Obtener contenido de archivo** de la siguiente manera:

   ![Captura de pantalla de la configuración de contenido del archivo Get](assets/documentautomation/automation_15.png)

   **Dirección del sitio:** su sitio de SharePoint.
   **Identificador de archivo:** busque &quot;identificador&quot; y elija Identificador en el paso  **Obtener** propiedades de archivo.
1. Busque &quot;Adobe&quot; y elija **Adobe Sign** para agregar otra acción.

   ![Captura de pantalla del menú de búsqueda](assets/documentautomation/automation_16.png)

1. Introduzca &quot;cargar&quot; en el cuadro de búsqueda de Adobe Sign y seleccione **Cargar un documento y obtener un ID de documento**.
1. Busque la variable dinámica **Name** para obtener el nombre del elemento o documento seleccionado en el activador en **File Name**.
1. Haga clic en **Expresión** en el asistente de variables en **Contenido de archivo**.

   ![Captura de pantalla de Cargar un documento y obtener una pantalla de ID de documento](assets/documentautomation/automation_17.png)

1. Añada un solo apóstrofo y, a continuación, haga clic de nuevo en **Contenido dinámico**, elimine su apóstrofe, seleccione **Contenido del archivo** y, a continuación, haga clic en **Aceptar**.

   Asegúrese de que no haya apóstrofos adicionales y que tenga el aspecto que se muestra a continuación.

   ![Captura de pantalla del aspecto que debería tener la pantalla Contenido dinámico](assets/documentautomation/automation_18.png)

1. Busque &quot;crear&quot; en el área de búsqueda de Adobe Sign para añadir otra acción de Adobe Sign.
1. Seleccione **Crear y aceptar a partir de un documento cargado y enviarlo para firmar**.

   ![Captura de pantalla de la búsqueda para crear](assets/documentautomation/automation_19.png)

1. Configure la información necesaria:
Elija **Nombre** del asistente de variables dinámicas en **Nombre del acuerdo**.
Elija **ID de documento** del asistente de variables dinámicas en **ID de documento**.
Elija **Correo electrónico del firmante** del asistente de variables dinámicas en **Correo electrónico del participante**.
Introduzca &quot;1&quot; en **Orden del participante**.
Elija **Firmante** en el menú desplegable en **Función de participante**.

   ![Captura de pantalla de la información requerida](assets/documentautomation/automation_20.png)

1. **** Guarde el flujo.

### Prueba del flujo

Vaya al repositorio de documentos de su sitio de SharePoint para probarlo.

1. Seleccione el documento y elija **Automatizar** y el **Flujo** que acaba de crear.

   ![Captura de pantalla de selección del menú Automatizar y el flujo](assets/documentautomation/automation_21.png)

1. Inicie el flujo para validar las conexiones (solo la primera ejecución del flujo).
1. Introduzca un mensaje bueno al aprobador en **Mensaje**.
1. Introduzca el correo electrónico del firmante del documento en **Correo electrónico del firmante**.
1. Haga clic en **Ejecutar flujo**.

El aprobador configurado para el usuario que inicia el flujo obtendrá una solicitud de aprobación. Puede aprobarlo por correo electrónico o a través del menú Power Automate Action Items.
Una vez aprobado, firme el documento. Dependiendo del usuario y de si ha iniciado sesión en Sign, es posible que deba abrir las ventanas de firma en una ventana privada del navegador.

![Captura de pantalla de apertura en la ventana privada del navegador](assets/documentautomation/automation_22.png)

Complete la firma y, a continuación, vuelva a mirar en la carpeta de SharePoint.

![Captura de pantalla de la carpeta SharePoint](assets/documentautomation/automation_23.png)

## Parte 3: OCR de documento automatizado con Adobe PDF Tools {#part3}

En la tercera parte, aprenderás a automatizar OCR en archivos PDF cuando se importen a Microsoft SharePoint. Esto soluciona un problema que se produce con los documentos PDF digitalizados que no se pueden buscar en SharePoint.

![Captura de pantalla del documento PDF en el navegador](assets/documentautomation/automation_24.png)

### Configuración de una carpeta en SharePoint

Vaya a Microsoft SharePoint donde desee almacenar documentos.

1. Haga clic en **+ Nuevo** para crear una nueva carpeta llamada &quot;Contratos procesados&quot;.
1. Haga clic en **+ Nuevo** para crear una nueva carpeta llamada &quot;Contratos antiguos&quot;.

   ![Captura de pantalla de nuevas carpetas](assets/documentautomation/automation_25.png)

Ahora se hace referencia a estas carpetas como parte del flujo de Power Automate.

### Creación de un flujo a partir de una plantilla

1. Inicie sesión en https://flow.microsoft.com.
1. Haga clic en **Plantillas** en la barra lateral.

   ![Captura de pantalla de selección de plantillas](assets/documentautomation/automation_26.png)

1. Seleccione **Convertir archivos recién añadidos a PDF en el que se pueda buscar texto en SharePoint**.
1. Haga clic en el símbolo **+** junto a Adobe PDF Tools.

   ![Captura de pantalla de selección del símbolo +](assets/documentautomation/automation_27.png)

1. Vaya a https://www.adobe.com/go/powerautomate_getstarted en una nueva ficha.
1. Haga clic en **Introducción**.

   ![Captura de pantalla del botón Introducción](assets/documentautomation/automation_28.png)

1. Inicie sesión con su Adobe ID.

   ![Captura de pantalla de la pantalla de inicio de sesión](assets/documentautomation/automation_29.png)

1. Introduzca el nombre de las credenciales y la descripción de las credenciales y haga clic en **Crear credenciales**.

   ![Captura de pantalla de la pantalla Crear credenciales](assets/documentautomation/automation_30.png)

   Mantenga abierta la ventana con las credenciales. Deberá introducirlos en Microsoft Power Automate.

   ![Captura de pantalla de la ficha del navegador para mantenerla abierta](assets/documentautomation/automation_31.png)

1. Introduzca las credenciales y haga clic en **Crear en Microsoft Power Automate**.

   ![Captura de pantalla de introducción de las credenciales de Herramientas de PDF](assets/documentautomation/automation_32.png)

1. Haga clic en **Continuar**.

   ![Captura de pantalla de dónde hacer clic en Continuar](assets/documentautomation/automation_33.png)

   Ahora puede ver una vista del flujo de trabajo y tendrá que configurarlo para su entorno.

1. Seleccione el campo Dirección del sitio y elija el sitio de SharePoint que está utilizando en el activador denominado **Cuando se crea un archivo en una carpeta**.

   ![Captura de pantalla de selección Cuando se crea un archivo en un activador de carpeta](assets/documentautomation/automation_34.png)

1. Haga clic en el icono de carpeta para ir a la carpeta Contratos antiguos, situada debajo del ID de carpeta.

   ![Captura de pantalla de selección de la carpeta Contratos antiguos](assets/documentautomation/automation_35.png)

1. Edite la acción **Crear archivo** en la parte inferior del flujo:

   Cambie **Dirección del sitio** a la dirección del sitio.
Especifique la ubicación de la carpeta Contratos procesados en la ruta de carpeta.

1. Haga clic en **Guardar** en la esquina superior derecha.
1. Haga clic en **Prueba**.
1. Seleccione **Manualmente**.
1. Haga clic en **Prueba**.

   ![Captura de pantalla del flujo de prueba](assets/documentautomation/automation_36.png)

### Prueba el nuevo flujo

1. Vaya a la carpeta Contratos antiguos de SharePoint.
1. Vaya a Contratos E03/Antiguos en los archivos de ejercicio descargados.
1. Copie los archivos ReleaseFormXX.pdf en la carpeta Old Contracts de SharePoint.

   ![Captura de pantalla de copia de los archivos](assets/documentautomation/automation_37.png)

Ahora, si navega a la carpeta Contratos procesados, podrá ver los archivos PDF disponibles después de que el flujo tenga unos momentos para ejecutarse. Si abre los archivos PDF, podrá ver que el texto se puede seleccionar.
Además, SharePoint indexa el documento, lo que permite buscar el contenido de los documentos desde la barra de búsqueda de SharePoint.

## Parte 4: Conjunto automatizado de documentos con Adobe PDF Tools {#part4}

En la cuarta parte, aprenderá a combinar muchos documentos en función de la información proporcionada al seleccionar e iniciar un flujo de Microsoft SharePoint. En este escenario, el flujo:

* Solicite información para elegir qué incluir en un paquete para un cliente.
* Según la información proporcionada, combina muchos documentos. Estos documentos incluyen una portada y white papers opcionales.
* El documento combinado se guarda en SharePoint.

### Importación de archivos de ejercicio a SharePoint

1. Abra la carpeta E04 en los archivos de Ejercicio.
1. Importe las carpetas Propuesta, Plantillas y Documentos generados en SharePoint.

   ![Captura de pantalla de importación de carpetas](assets/documentautomation/automation_38.png)

Estas carpetas se utilizarán como referencia. En particular, utilizará el archivo Propuesta.docx para su propuesta.

En la carpeta Templates, hay una carpeta Covers que incluye diseños de portada para diferentes ciudades. También hay una carpeta de documentos técnicos que contiene documentos técnicos adicionales opcionales que se adjuntarán al final, si se selecciona.

### Importar el flujo a Microsoft Power Automatizar

1. Inicie sesión en Microsoft Power Automate (https://flow.microsoft.com).
1. Haga clic en **Mis flujos**.

   ![Captura de pantalla de dónde seleccionar Mis flujos](assets/documentautomation/automation_39.png)

1. Haga clic en **Importar**.

   ![Captura de pantalla de importación](assets/documentautomation/automation_40.png)

1. Haga clic en **Cargar** y elija la carpeta GeneratePropuesta_20210311231623.zip en E04/Flows/.

   ![Captura de pantalla de selección de carpeta](assets/documentautomation/automation_41.png)

1. Haga clic en **Importar**.

1. Haga clic en el icono de llave inglesa en Acción junto a **Enviar propuesta al cliente**.

   ![Captura de pantalla del icono de llave inglesa](assets/documentautomation/automation_42.png)

1. Seleccione **Crear como nuevo** en Configuración.
1. Establezca el nombre del flujo en Nombre de recurso.
1. Haga clic en **Guardar**.

   Repita este procedimiento para los otros recursos relacionados y seleccione su conexión.

   ![Captura de pantalla del archivo guardado](assets/documentautomation/automation_43.png)

1. Haga clic en **Importar** después de haber realizado todas las conexiones.

### Definir para un archivo seleccionado

Ahora que se ha creado el flujo, haga lo siguiente:

1. Haga clic en **Editar**.

   ![Captura de pantalla de dónde seleccionar la edición](assets/documentautomation/automation_44.png)

1. Seleccione el activador **Para un archivo seleccionado**.

   Agregue su sitio de SharePoint en la dirección del sitio.
Añada su biblioteca en la biblioteca.

   ![Captura de pantalla del activador completado](assets/documentautomation/automation_45.png)

### Establecer templateFolderPath

1. Haga clic en la variable templateFolderPath.
1. Establezca la ruta en la que se encuentra la carpeta Templates dentro del sitio de SharePoint que ha importado.

### Definir contenido de archivo de portada

1. Haga clic en la acción **Tapa**, que amplía el ámbito.
1. Expandir **portada: Obtener contenido de archivo**.

   Establezca Dirección del sitio en su sitio de SharePoint.

   ![Captura de pantalla de la portada expandida](assets/documentautomation/automation_46.png)



### Definir archivo seleccionado

1. Expanda la acción de ámbito **Archivo seleccionado**.

   Cambie la dirección del sitio y el nombre de la biblioteca a su sitio y biblioteca de SharePoint respectivamente en **Obtener propiedades de archivo**.
Cambie la dirección del sitio al sitio de SharePoint en **Obtener contenido de archivo**.

   ![Captura de pantalla de la acción Archivo seleccionado expandida](assets/documentautomation/automation_47.png)

### Definir papeles

1. Haga clic en la acción **White papers**.
1. Expandir **Condición: Añadir documento técnico**.

   ![Captura de pantalla de la condición de Añadir documento técnico expandida](assets/documentautomation/automation_48.png)

1. Expanda **Libro blanco 1: Obtener contenido de archivo mediante la ruta**.
Edite la dirección del sitio en el sitio de SharePoint especificado.

Repita los mismos pasos para **Condición: Añadir documento técnico 2**.

### Establecer archivo

1. Expanda **Crear archivo**.

   Edite la dirección del sitio y la ruta de carpeta al sitio de SharePoint y a la ruta donde se encuentra la carpeta Documentos generados.

1. Haga clic en **Guardar**.

### Prueba del flujo

1. Vaya a la carpeta Propuesta en SharePoint.
1. Seleccione la carpeta Propuesta.docx.

   ![Captura de pantalla de selección de la carpeta de propuestas](assets/documentautomation/automation_49.png)

1. Seleccione el flujo en el menú **Automatizar**.

   ![Captura de pantalla de Selección del menú Automatizar](assets/documentautomation/automation_50.png)

1. Haga clic en **Continuar** para iniciar el flujo.

   ![Captura de pantalla de selección del botón Continuar](assets/documentautomation/automation_51.png)

1. Elija la portada y los documentos técnicos que desee anexar.
1. Haga clic en **Ejecutar flujo**.

   ![Captura de pantalla del botón Ejecutar flujo](assets/documentautomation/automation_52.png)

Vaya a la carpeta Generar documentos. Ahora debería ver el archivo PDF generado.

![Captura de pantalla del directorio de SharePoint con nuevo archivo PDF](assets/documentautomation/automation_53.png)

### Adición de Protect y otras acciones al flujo

Ahora que ha creado correctamente un flujo, va a editar el flujo para codificar el documento PDF con una contraseña. Esto también explica cómo puede utilizar otras acciones.

1. Vuelva al final del flujo.
1. Haga clic en el símbolo **+** entre **Combinar archivos PDF** y **Crear archivo**.

   ![Captura de pantalla de dónde seleccionar + símbolo](assets/documentautomation/automation_54.png)

1. Seleccione **Agregar una acción**.
1. Busque &quot;Herramientas de Adobe PDF&quot;.

   ![Captura de pantalla de búsqueda de Adobe PDF](assets/documentautomation/automation_55.png)

1. Seleccione **Protect PDF desde la visualización**.
1. Utilice Contenido dinámico para establecer el campo Nombre de archivo en **Nombre de archivo PDF de combinación PDF**.

   ![Captura de pantalla de contenido dinámico](assets/documentautomation/automation_56.png)

   En el activador, hay un campo Contraseña que forma parte del formulario de inicio. Podemos usarlo aquí.

1. Busque **Campo de contraseña** con contenido dinámico y colóquelo en el campo Contraseña.

   ![Captura de pantalla de búsqueda de contraseña](assets/documentautomation/automation_57.png)

1. Utilice contenido dinámico para establecerlo en **Contenido del archivo PDF de combinación de archivos PDF** en el campo Contenido del archivo.
1. Cambie el **Crear archivo** para obtener el contenido del archivo de Protect PDF en lugar de combinar archivos PDF.
1. Expanda **Crear archivo**.
1. Borre el campo Contenido del archivo.
1. Utilice Contenido dinámico para colocar **Contenido del archivo PDF** desde **Protect PDF desde la visualización**.

### Prueba del flujo

1. Vaya a la carpeta Propuesta en SharePoint.
1. Seleccione Propuesta.docx.

   ![Captura de pantalla de selección de la carpeta Propuesta](assets/documentautomation/automation_58.png)

1. Seleccione **Automatizar** para elegir el flujo.

   ![Captura de pantalla de selección de Automatizar en el menú](assets/documentautomation/automation_59.png)

1. Haga clic en **Continuar** para iniciar el flujo.

   ![Captura de pantalla de selección de Continuar](assets/documentautomation/automation_60.png)

1. Elija la portada y los documentos blancos que desea anexar.
1. Establezca el campo Contraseña en la Contraseña que desee establecer.
1. Haga clic en **Ejecutar flujo**.

   ![Captura de pantalla de los archivos seleccionados y botón Ejecutar flujo](assets/documentautomation/automation_61.png)

1. Vaya a la carpeta Generar documentos.
Debería ver el archivo PDF generado. Abra el archivo PDF y le pedirá que introduzca su contraseña.

   ![Captura de pantalla del PDF generado en el directorio de SharePoint](assets/documentautomation/automation_62.png)
