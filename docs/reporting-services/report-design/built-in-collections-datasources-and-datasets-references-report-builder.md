---
title: Referencias a las colecciones DataSources y DataSets (Generador de informes y SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: f951a4aa-da55-4e43-8579-4a5d4480d11f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 930dfe2773b72723c2b8dc8571272847bb0d62d3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65581807"
---
# <a name="built-in-collections---datasources-and-datasets-references-report-builder"></a>Colecciones integradas: referencias a DataSources y DataSets (Generador de informes)
  La colección **DataSources** representa todos los orígenes de datos usados en un informe. De igual forma, la colección **DataSets** representa todos los conjuntos de datos de todos los orígenes de datos existentes en un informe. Use el panel **Datos de informe** para obtener acceso a una vista jerárquica en la que aparezcan los conjuntos de datos de informe organizados debajo del origen de datos al que hacen referencia. Si incluye referencias a estas colecciones, no verá los valores cuando obtenga acceso a una vista previa del informe. Estas colecciones solo están disponibles una vez publicado el informe en un servidor de informes.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="datasources"></a>DataSources  
 La colección **DataSources** representa los orígenes de datos a los que se hace referencia en una definición de informe publicado. Puede decidir incluir esta información en el informe para documentar el origen de los datos de informe. Esta colección no está disponible en el modo **Vista previa** . En la siguiente tabla, se describen las variables de la colección **DataSources** .  
  
|**Variable**|**Tipo**|**Descripción**|  
|------------------|--------------|---------------------|  
|**DataSourceReference**|**String**|Ruta de acceso completa de la definición de origen de datos en el servidor de informes. Por ejemplo, puede incluir una lista de todos los orígenes de datos que usó un informe como parte de un historial de informes. En el ejemplo siguiente se muestra la ruta de acceso completa del origen de datos denominado AdventureWorks2012:<br /><br /> `/DataSources/AdventureWorks2012`.|  
|**Tipo**|**String**|Tipo de proveedor de datos para el origen de datos. Por ejemplo, `SQL`.|  
  
## <a name="datasets"></a>DataSets  
 La colección **DataSets** representa los conjuntos de datos a los que se hace referencia en una definición de informe. Puede decidir incluir la consulta en el informe en un cuadro de texto, de modo que un usuario que esté interesado en saber exactamente qué datos están en el informe pueda ver el texto del comando original. Esta colección no está disponible en el modo **Vista previa** . En la siguiente tabla, se describen los miembros de la colección **DataSets** .  
  
|**Miembro**|**Tipo**|**Descripción**|  
|----------------|--------------|---------------------|  
|**CommandText**|**String**|Para los orígenes de datos de base de datos, ésta es la consulta que se utiliza para recuperar datos del origen de datos. Si la consulta es una expresión, ésta es la expresión evaluada.|  
|**RewrittenCommandText**|**String**|El valor CommandText expandido del proveedor de datos. Se utiliza normalmente en informes con parámetros de consulta que se asignan a parámetros de informe. El proveedor de datos establece esta propiedad al expandir las referencias de los parámetros de texto de comando a los valores constantes seleccionados para los parámetros de informe asignados.|  
  
### <a name="using-query-expressions"></a>Usar expresiones de consulta  
 Puede usar expresiones de consulta para definir la consulta contenida en un conjunto de datos. Puede usar esta característica para diseñar informes cuyas consultas cambien en función de la información facilitada por el usuario, de los datos de otros conjuntos de datos o de otras variables. Para más información sobre las consultas, vea [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte también  
 [Expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
