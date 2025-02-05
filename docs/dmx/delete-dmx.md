---
title: DELETE (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c1c75a6ff18b26bee65365acbc068de87678a9c7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070763"
---
# <a name="delete-dmx"></a>DELETE (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Borra un modelo de minería de datos, una estructura de minería datos, o una estructura de minería de datos y todos sus modelos de minería de datos asociados, según las cláusulas DMX (Extensiones de minería de datos) que utilice.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DELETE FROM [MINING MODEL] <model>[.CONTENT]  
DELETE FROM [MINING STRUCTURE] <structure>[.CONTENT]|[.CASES]  
```  
  
## <a name="arguments"></a>Argumentos  
 *model*  
 Identificador de modelo.  
  
 *estructura*  
 Identificador de estructura.  
  
## <a name="remarks"></a>Comentarios  
 Si no especifica **MINING MODEL** o **MINING STRUCTURE**, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] busca el tipo de objeto según el nombre y procesa el objeto correcto. Si el servidor contiene una estructura y un modelo de minería de datos con el mismo nombre, se devuelve un error.  
  
 En la siguiente tabla se describen los resultados de usar las diferentes formas de sintaxis.  
  
|Instrucción|Resultado|  
|---------------|------------|  
|DELETE FROM MINING STRUCTURE *\<estructura >*<br /><br /> o Administrador de configuración de<br /><br /> DELETE FROM MINING STRUCTURE *\<estructura >* . CONTENIDO|Realiza ProcessClear en la estructura de minería de datos. Se borra todo el contenido de la estructura de minería de datos y sus modelos de minería de datos asociados.|  
|DELETE FROM MINING STRUCTURE *\<estructura >* . CASOS|Realiza ProcessClearStructureOnly en la estructura de minería de datos. Se borra todo el contenido de la estructura de minería de datos y se dejan intactos sus modelos de minería de datos asociados. La obtención de detalles de los modelos de minería de datos asociados produce un error tras el borrado de la estructura de minería de datos.|  
|ELIMINAR del modelo de minería de datos *\<modelo >*<br /><br /> o Administrador de configuración de<br /><br /> ELIMINAR del modelo de minería de datos *\<modelo >* . CONTENIDO|Realiza ProcessClear en el modelo de minería de datos, pero deja intactos los valores de estado. Los valores de estado son los estados posibles de una columna. Por ejemplo, los valores de estado de una columna de género serían masculino y femenino.|  
  
 Para obtener más información acerca de los tipos de procesamiento, vea [elemento Type &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/type-element-xmla).  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se quita todo el contenido del modelo NB_Sample.  
  
```  
DELETE FROM NB_Sample.CONTENT  
```  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de definición de datos](../dmx/dmx-statements-data-definition.md)   
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de manipulación de datos](../dmx/dmx-statements-data-manipulation.md)   
 [Referencia de instrucciones de Extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
