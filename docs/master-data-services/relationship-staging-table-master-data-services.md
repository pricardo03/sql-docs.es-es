---
title: Tabla de ensayo de relaciones (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 04/01/2016
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- relationships staging table [Master Data Services]
- database [Master Data Services], relationships table
ms.assetid: e19b6002-67bd-4e7d-9f19-ecb455522b1a
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 77d4bd0bfab8b2c1a7337cae1f5d96300b7f3625
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67910003"
---
# <a name="relationship-staging-table-master-data-services"></a>Tabla de ensayo de relaciones (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Use la tabla de almacenamiento provisional de relaciones (stg.name_Relationship) en la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] para cambiar la ubicación de los miembros de una jerarquía explícita, en función de las relaciones que tienen los miembros entre sí.  
  
##  <a name="TableColumns"></a> Columnas de la tabla  
 En la tabla siguiente se explica para qué se usa cada uno de los campos de la tabla de ensayo Relationship.  
  
|Nombre de la columna|Descripción|Valor|  
|-----------------|-----------------|-----------|  
|**ID**|Identificador asignado automáticamente.|No especifique ningún valor en este campo. Si no se ha procesado el lote, este campo está en blanco.|  
|**RelationshipType**|Obligatorio<br /><br /> Tipo de relación que se está estableciendo.|Los valores posibles son:<br /><br /> **1**: primario<br /><br /> **2**: elemento relacionado (del mismo nivel)|  
|**ImportStatus_ID**|Obligatorio<br /><br /> Estado del proceso de importación.|Los valores posibles son:<br /><br /> **0**, que se especifica para indicar que el registro está listo para el almacenamiento provisional.<br /><br /> **1**, que se asigna e indica automáticamente que el proceso de almacenamiento provisional del registro ha sido correcto.<br /><br /> **2**, que se asigna automáticamente e indica que el proceso de almacenamiento provisional del registro no ha sido correcto.|  
|**Batch_ID**|Solo lo necesita el servicio web<br /><br /> Identificador asignado automáticamente que agrupa los registros para el almacenamiento provisional.<br /><br /> Si no se ha procesado el lote, este campo está en blanco.|A todos los miembros del lote se les asigna este identificador, que se muestra en la columna [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Id. **de la interfaz de usuario de** .|  
|**BatchTag**|Obligatorio, excepto para el servicio web<br /><br /> Nombre único para el lote, de hasta 50 caracteres.||  
|**HierarchyName**|Obligatorio<br /><br /> Nombre de jerarquía explícita. Cada miembro consolidado solo puede pertenecer a una jerarquía.||  
|**ParentCode**|Obligatorio<br /><br /> Para las relaciones de elementos primarios y secundarios, el código del miembro consolidado que será el elemento primario del miembro secundario hoja o consolidado.<br /><br /> Para las relaciones relacionadas, el código de uno de los miembros relacionados.||  
|**ChildCode**|Obligatorio<br /><br /> Para las relaciones de elementos primarios y secundarios, el código del miembro consolidado u hoja que será el elemento secundario.<br /><br /> Para las relaciones relacionadas, el código de uno de los miembros relacionados.||  
|**Criterio de ordenación**|Opcional<br /><br /> Entero que indica el orden del miembro en relación con los demás miembros bajo el elemento primario. Cada miembro secundario debe tener un identificador único.||  
|**ErrorCode**|Muestra un código de error. Para todos los registros con un **ImportStatus_ID** de **2**, consulte [Errores del proceso de almacenamiento provisional &#40;Master Data Services&#41;](../master-data-services/staging-process-errors-master-data-services.md).||  
  
## <a name="see-also"></a>Vea también  
 [Información general: importación de datos de tablas &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)   
 [Ver los errores que se producen durante el almacenamiento provisional &#40;Master Data Services&#41;](../master-data-services/view-errors-that-occur-during-staging-master-data-services.md)   
 [Errores del proceso de almacenamiento provisional &#40;Master Data Services&#41;](../master-data-services/staging-process-errors-master-data-services.md)  
  
  
