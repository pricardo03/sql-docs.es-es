---
title: catalog.object_parameters (base de datos de SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: d7b04903-2d61-4159-9456-475942d1f732
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 907678a77620f432411b1714ec7a1603e147129e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68104826"
---
# <a name="catalogobjectparameters-ssisdb-database"></a>catalog.object_parameters (base de datos de SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Muestra los parámetros para todos los paquetes y proyectos en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|parameter_id|**bigint**|Identificador (id.) único del parámetro.|  
|identificador de proyecto|**bigint**|Identificador único del proyecto.|  
|object_type|**smallint**|Tipo de parámetro. El valor es `20` para un parámetro de proyecto y `30` para un parámetro de paquete.|  
|object_name|**sysname**|Nombre del proyecto o paquete correspondiente.|  
|parameter_name|**sysname(nvarchar(128))**|Nombre del parámetro.|  
|data_type|**nvarchar(128)**|El tipo de datos del parámetro.|  
|required|**bit**|Cuando el valor es `1`, se requiere el valor del parámetro para iniciar la ejecución. Cuando el valor es `0`, no se requiere el valor del parámetro para iniciar la ejecución.|  
|sensitive|**bit**|Cuando el valor es `1`, el valor del parámetro es confidencial. Cuando el valor es `0`, el valor del parámetro no es confidencial.|  
|description|**nvarchar(1024)**|Descripción opcional del paquete.|  
|design_default_value|**sql_variant**|Valor predeterminado para el parámetro que se asignó durante el diseño del proyecto o paquete.|  
|default_value|**sql_variant**|Valor predeterminado que se utiliza actualmente en el servidor.|  
|value_type|**char(1)**|Indica el tipo de valor del parámetro. Este campo muestra `V` cuando "parameter_value" es un valor literal y `R` cuando el valor se asigna mediante la referencia a una variable de entorno.|  
|value_set|**bit**|Cuando el valor es `1`, el valor del parámetro se ha asignado. Cuando el valor es `0`, el valor del parámetro no se ha asignado.|  
|referenced_variable_name|**nvarchar(128)**|Nombre de la variable de entorno que se asigna al valor del parámetro. El valor predeterminado es **NULL**.|  
|validation_status|**char(1)**|Solamente se identifica con fines informativos. No se usa en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|last_validation_time|**datetimeoffset(7)**|Solamente se identifica con fines informativos. No se usa en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
  
## <a name="permissions"></a>Permisos  
 Para ver las filas en esta vista, debe tener uno de los siguientes permisos:  
  
-   Permiso READ en el proyecto  
  
-   Pertenencia al rol de base de datos de **ssis_admin**  
  
-   Pertenencia al rol de servidor **sysadmin**  
  
 Se aplica la seguridad en el nivel de fila; solo se muestran las filas para las que disponga de permiso para ver.  
  
  
