---
title: Extraer datos mediante el origen de XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- extracting data [Integration Services]
- sources [Integration Services], XML
- XML source [Integration Services]
ms.assetid: 5d5be54c-2b7e-4957-9193-c5ea5c5d6d15
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3c7a9b107a05b0645f2286f534f457d46a1b6f11
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62771101"
---
# <a name="extract-data-by-using-the-xml-source"></a>Extraer datos mediante el origen de XML
  Para agregar y configurar un origen XML, el paquete ya debe incluir por lo menos una tarea Flujo de datos.  
  
### <a name="to-extract-data-using-an-xml-source"></a>Para extraer datos mediante un origen XML  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de datos** y, a continuación, desde el **cuadro de herramientas**, arrastre el origen XML a la superficie de diseño.  
  
4.  Haga doble clic en el origen XML.  
  
5.  En el **Editor de origen de XML**, en la página **Administrador de conexiones** , seleccione un modo de acceso de datos:  
  
    -   Para ir al modo de acceso **Ubicación del archivo XML** , haga clic en **Examinar** y ubique la carpeta que contiene el archivo XML.  
  
    -   Para ir al modo de acceso **Archivo XML de variable** , seleccione la variable definida por el usuario que contiene la ruta del archivo XML.  
  
    -   Para ir al modo de acceso **Datos XML de variable** , seleccione la variable definida por el usuario que contiene los datos XML.  
  
    > [!NOTE]  
    >  Las variables se deben definir en el ámbito de la tarea Flujo de datos que contiene el origen XML, o en el ámbito del paquete. Además, la variable debe tener un tipo de datos de cadena.  
  
6.  Opcionalmente, seleccione **Utilizar esquema insertado** para indicar que el documento XML incluye información de esquema.  
  
7.  Para especificar un lenguaje externo de definición de Esquema XML (XSD) para el archivo XML, realice una de las siguientes acciones:  
  
    -   Haga clic en **Examinar** para buscar un archivo XSD existente.  
  
    -   Haga clic en **Generar XSD** para crear un XSD a partir del archivo XML.  
  
8.  Para actualizar los nombres de las columnas de salida, haga clic en **Columnas** y modifique los valores en la lista **Columna de salida** .  
  
9. Para configurar la salida de error, haga clic en **Salida de error**. Para más información, vea [Configurar una salida de error en un componente de flujo de datos](../configure-an-error-output-in-a-data-flow-component.md).  
  
10. Haga clic en **Aceptar**.  
  
11. Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados**, en el menú **Archivo**.  
  
## <a name="see-also"></a>Vea también  
 [Origen XML](xml-source.md)   
 [Transformaciones de Integration Services](transformations/integration-services-transformations.md)   
 [Rutas de Integration Services](integration-services-paths.md)   
 [Tarea Flujo de datos](../control-flow/data-flow-task.md)  
  
  
