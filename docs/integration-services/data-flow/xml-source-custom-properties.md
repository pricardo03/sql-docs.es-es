---
title: Propiedades personalizadas del origen XML | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: eb29b28c-3159-41ec-b3d7-fce5b2f2be55
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 32afa6d65929fda676f7eebb1bc78ab1d05cd789
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68074019"
---
# <a name="xml-source-custom-properties"></a>Propiedades personalizadas del origen XML

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  El origen XML tiene propiedades personalizadas y propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas del origen XML. Todas las propiedades son de lectura y escritura.  
  
|Nombre de propiedad|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer|Modo que se usa para tener acceso los datos XML.|  
|UseInlineSchema|Boolean|Valor que indica si se usa una definición de esquema insertada dentro del origen XML. El valor predeterminado de esta propiedad es **False**.|  
|XMLDATA|String|Archivo o variables desde las que recuperar los datos XML.<br /><br /> Puede especificar el valor de esta propiedad con una expresión de propiedad.|  
|XMLSchemaDefinition|String|Ruta de acceso y nombre del archivo de definición de esquema (.xsd).<br /><br /> Puede especificar el valor de esta propiedad con una expresión de propiedad.|  
  
 En la tabla siguiente se describen las propiedades personalizadas de la salida del origen XML. Todas las propiedades son de lectura y escritura.  
  
|Nombre de propiedad|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|RowsetID|String|Valor que identifica el conjunto de filas asociado a la salida.|  
  
 La salida y las columnas de salida del origen XML no tienen ninguna propiedad personalizada.  
  
 Para más información, consulte [XML Source](../../integration-services/data-flow/xml-source.md).  
  
## <a name="see-also"></a>Consulte también  
 [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
