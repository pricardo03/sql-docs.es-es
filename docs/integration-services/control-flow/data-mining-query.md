---
title: Consulta de minería de datos| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataminingquery.f1
ms.assetid: 948e358a-6245-429f-82c7-4cedc5e048fd
author: janinezhang
ms.author: janinez
ms.openlocfilehash: fdff711249e7fd356ad74f37faf5bb98482672d2
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893093"
---
# <a name="data-mining-query"></a>Consulta de minería de datos

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  El panel de diseño contiene el generador de consultas de predicción de minería de datos, que puede utilizar para generar consultas de predicción de minería de datos. Puede diseñar consultas de predicción basadas en tablas de entrada o consultas singleton de predicción. Cambie a la vista de resultado para ejecutar la consulta y ver los resultados. La vista de consulta muestra la consulta de Extensiones de minería de datos (DMX) creada mediante el generador de consultas de predicción.  
  
## <a name="options"></a>Opciones  
 Botón Cambiar vista  
 Haga clic en un icono para cambiar entre el panel de diseño y el de consulta. De forma predeterminada, el panel de diseño está abierto.  
  
 Para cambiar al panel de diseño, haga clic en el icono ![icono de diseño](../../integration-services/control-flow/media/ssis-designicon.gif "Design icon").  
  
 Para cambiar al panel de consulta, haga clic en el icono ![icono de SQL](../../integration-services/control-flow/media/ssis-queryicon.gif "icono de SQL").  
  
 **Modelo de minería de datos**  
 Muestra el modelo de minería de datos seleccionado en el que desea basar las predicciones.  
  
 **Seleccionar modelo**  
 Abre el cuadro de diálogo **Seleccionar modelo de minería de datos** .  
  
 **Columnas de entrada**  
 Muestra las columnas de entrada seleccionadas que se utilizan para generar las predicciones.  
  
 **Source**  
 Seleccione el origen que contiene el campo que utilizará para la columna desde la lista desplegable. Puede usar el modelo de minería de datos seleccionado en la tabla **Modelo de minería de datos** , la tabla o las tablas de entrada seleccionadas en la tabla **Seleccionar tabla(s) de entrada** , una función de predicción o una expresión personalizada.  
  
 Las columnas pueden arrastrarse desde las tablas que contienen el modelo de minería de datos y las columnas de entrada a la celda.  
  
 **Campo**  
 En la tabla de origen, seleccione una columna de la lista de columnas derivadas. Si ha seleccionado **Función de predicción** en **Origen**, esta celda contiene una lista desplegable de las funciones de predicción disponibles para el modelo de minería de datos seleccionado.  
  
 **Alias**  
 El nombre de la columna que devuelve el servidor.  
  
 **Mostrar**  
 Seleccione esta opción para devolver la columna o para utilizar solamente la columna en la cláusula WHERE.  
  
 **Grupo**  
 Use esta opción con la columna **Y/O** para agrupar expresiones. Por ejemplo, (expr1 O expr2) Y expr3.  
  
 **Y/O**  
 Utilice esta opción para crear una consulta lógica. Por ejemplo, (expr1 O expr2) Y expr3.  
  
 **Criterios o argumento**  
 Especifique una condición o una expresión de usuario que se aplica a la columna. Las columnas pueden arrastrarse desde las tablas que contienen el modelo de minería de datos y las columnas de entrada a la celda.  
  
## <a name="see-also"></a>Consulte también  
 [Herramientas de consulta de minería de datos](https://docs.microsoft.com/analysis-services/data-mining/data-mining-query-tools)   
 [Referencia de instrucciones de Extensiones de minería de datos &#40;DMX&#41;](../../dmx/data-mining-extensions-dmx-statements.md)  
  
  
