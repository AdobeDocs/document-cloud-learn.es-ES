---
title: Trabajar con campos de formulario
description: Aprenda a agregar varios tipos de campos de formulario, establecer propiedades de campos de formulario y agregar seguridad para crear formularios profesionales de alta calidad
feature: Form, Edit PDF
role: User
level: Intermediate
jira: KT-9345
thumbnail: KT-9345.jpg
exl-id: b7dde660-846c-4875-b5a7-741ff087ccc9
source-git-commit: 4e6fbf91e96d26f9ee8f1105ad68738b9450a32d
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 0%

---

# Trabajar con campos de formulario

En este tutorial práctico, aprenda a agregar varios tipos de campos de formulario, establecer propiedades de campos de formulario y agregar seguridad para crear formularios profesionales de alta calidad.

<br> 

## Lo que necesitas

[![Obtener archivo](../assets/Getfiles.svg)](../assets/Questionnaire.pdf)
Archivo de práctica del tutorial (PDF, 934 KB)

<br> 

## Aprenda a trabajar con campos de formulario

Utilice la herramienta Prepare Form para agregar automáticamente campos de formulario a un PDF existente.

>[!TIP]
>
>Active los aceleradores de una sola tecla en Preferencias, en la categoría General.

<br> 

>[!VIDEO](https://video.tv.adobe.com/v/3448514?quality=12&learn=on&hidetitle=true&captions=spa)

<br> 

## En este vídeo has aprendido a trabajar con campos de formulario.

Para agregar varios tipos de campos de formulario y establecer sus propiedades en un PDF existente.

1. Descargue y abra *Questionnaire.pdf*.
1. Seleccione **Prepare Form** en el Centro de herramientas.
1. Seleccione **Inicio**.
1. Seleccione **Editar texto e imágenes** en la barra de herramientas para corregir la errata.
1. Elija **Seleccionar** en la barra de herramientas para salir del modo de edición.
1. Seleccione y elimine el campo de formulario superior.
1. Seleccione **Vista previa** para ver el formulario.
1. Seleccione **Editar** para salir del modo de vista previa.

Agregar un campo de lista reduce la posibilidad de errores en los datos del formulario.

1. Seleccione y elimine el campo de texto *Ubicación HQ*.
1. Seleccione **Cuadro de lista** en la barra de herramientas y coloque un nuevo campo en la ubicación del campo de texto eliminado.
1. Escriba *HQ Location* en **Nombre de campo:**.
1. Seleccione **Todas las propiedades** y elija la pestaña **Opciones**.
1. Agregue tres ubicaciones diferentes en el campo **Elemento:**.
1. Seleccione la ubicación predeterminada en el campo **Lista de elementos:**.
1. Seleccione **Cerrar**.
1. Mantenga pulsada la tecla Mayús y seleccione el campo siguiente.
1. Selecciona **Igualar ancho y alto** y **Alinear a la izquierda** en el panel derecho.

Los campos del selector de fecha agregan interactividad y eliminan errores en un formulario.

1. Seleccione y elimine los campos *Cronología del proyecto* y *FECHA DE FINALIZACIÓN*.
1. Seleccione **Campo de fecha** en la barra de herramientas y coloque el nuevo campo en la ubicación de campo *Cronología del proyecto* eliminada.
1. Escriba *Inicio del proyecto* en **Nombre del campo:**.
1. Seleccione **Todas las propiedades** y elija la ficha **Formato**.
1. Elige una opción de formato de fecha y selecciona **Cerrar**.
1. Mantenga pulsadas las teclas Ctrl + Mayús (Cmd + Mayús en el Mac) para duplicar el campo.
1. Haga doble clic en el nuevo campo, seleccione la pestaña **General** y cambie el nombre del campo *Fin del proyecto*.
1. Seleccione **Cerrar**.
1. Mantenga pulsada la tecla Mayús y seleccione los tres campos.
1. Seleccione **Igualar ancho y alto** en el panel derecho.
1. Utilice las teclas de flecha para alinear cada campo si es necesario.

Las propiedades Comb se utilizan para distribuir texto uniformemente por el ancho de un campo de texto.

1. Haga doble clic en el campo *Código de referencia* y seleccione la pestaña **Opciones**.
1. Desmarque todas las casillas excepto **Comb of**.
1. Escriba *5* en el cuadro de caracteres.
1. Selecciona la pestaña **Aspecto** y elige cualquier color en el cuadro **Color de borde**.
1. Seleccione **Cerrar**.
1. Seleccione **Vista previa** e introduzca algunos números para probar el campo combinado.
1. Seleccione **Más** > **Borrar formulario** para eliminar los datos en el panel derecho.

## Aprenda a establecer propiedades para varios campos a la vez, el orden de tabulación y para proteger un formulario

<br> 

>[!VIDEO](https://video.tv.adobe.com/v/3439895?hidetitle=true&captions=spa)

<br> 

## En este vídeo has aprendido a configurar propiedades para varios campos a la vez, el orden de tabulación y a proteger un formulario.

Para establecer las propiedades de varios campos a la vez, el orden de tabulación y para proteger un formulario. Establecer todas las propiedades de los campos de texto ahorra tiempo y da coherencia visual a un formulario.

1. Mantenga pulsada la tecla Mayús y seleccione todos los campos de texto y de lista en el panel derecho.
1. Haga clic con el botón derecho y seleccione **Propiedades...**.
1. Seleccione *12* en el menú desplegable **Tamaño de fuente:**.
1. Seleccione **Cerrar**.

Establecer el orden de tabulación garantiza que el rellenador del formulario pueda desplazarse fácilmente de un campo a otro mientras rellena un formulario.

1. Escriba *Mayús + N* para mostrar el orden de tabulación.
1. Mueva el campo *Ubicación de HQ* debajo del campo *Número de empleados* en el panel derecho.
1. Mueva los campos *Comienzo del proyecto* y *Fin del proyecto* debajo del campo *DIRECCIÓN DE CORREO ELECTRÓNICO* en el panel derecho.

Proteger un formulario garantiza que no se puedan modificar los campos o el contenido del documento.

1. Escriba *Ctrl + D (Cmd + D en el Mac)* para que aparezca el cuadro de diálogo **Propiedades del documento**.
1. Seleccione la pestaña **Seguridad**.
1. Seleccione **Seguridad mediante contraseña** en el menú desplegable **Método de seguridad:**.
1. Marque **Restringir la edición e impresión del documento. Se requerirá una contraseña para cambiar esta configuración de permisos.**
1. Seleccione **Alta resolución** en el menú desplegable **Impresión permitida:**.
1. Seleccione **Rellenar campos de formulario y firmar campos de firma existentes** en el menú desplegable **Cambios permitidos:**.
1. Escriba una contraseña segura en el campo **Cambiar contraseña de permisos:**.
1. Confirme la contraseña y seleccione **Aceptar**.
1. Seleccione **Aceptar** para salir del cuadro de diálogo.
