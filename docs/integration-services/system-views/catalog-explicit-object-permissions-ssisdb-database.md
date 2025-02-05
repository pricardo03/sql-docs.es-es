---
title: catalog.explicit_object_permissions (base de datos de SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 49b09e0f-06e8-451f-b979-a0d91000bfe3
author: janinezhang
ms.author: janinez
ms.openlocfilehash: bfb24dc3d07953460fd33f7d0016cdc891ff5be9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67934635"
---
# <a name="catalogexplicitobjectpermissions-ssisdb-database"></a>catalog.explicit_object_permissions (base de datos de SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Muestra solo los permisos asignados explícitamente al usuario.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|object_type|**smallint**|Tipo del objeto protegible. Entre los tipos de objetos protegibles se incluyen carpeta (`1`), proyecto (`2`), entorno (`3`) y operación (`4`).|  
|object_id|**bigint**|Identificador único (ID) o clave principal del objeto protegido.|  
|principal_id|**int**|Identificador de la entidad de seguridad de base de datos.|  
|permission_type|**smallint**|Tipo de permiso.|  
|is_deny|**bit**|Indica si el permiso se ha denegado o se ha concedido. Cuando el valor es `1`, el permiso se ha denegado. Cuando el valor es `0`, el permiso no se ha denegado.|  
|grantor_id|**int**|El identificador de la entidad de seguridad que concedió el permiso.|  
  
## <a name="remarks"></a>Notas  
 Esta vista muestra los tipos de permisos enumerados en la siguiente tabla:  
  
|Valor de permission_type|Nombre del permiso|Descripción del permiso|Tipos de objetos aplicables|  
|----------------------------|---------------------|----------------------------|-----------------------------|  
|`1`|READ|Permite a la entidad de seguridad leer información que se considera parte del objeto, como las propiedades. No permite a la entidad de seguridad enumerar o leer el contenido de otros objetos contenidos dentro del objeto.|Carpeta, proyecto, entorno, operación|  
|`2`|MODIFY|Permite a la entidad de seguridad modificar información que se considera parte del objeto, como las propiedades. No permite a la entidad de seguridad modificar otros objetos contenidos dentro del objeto.|Carpeta, proyecto, entorno, operación|  
|`3`|Ejecute|Permite a la entidad de seguridad ejecutar todos los paquetes del proyecto.|Proyecto|  
|`4`|MANAGE_PERMISSIONS|Permite a la entidad de seguridad asignar permisos a los objetos.|Carpeta, proyecto, entorno, operación|  
|`100`|CREATE_OBJECTS|Permite a la entidad de seguridad crear objetos en la carpeta.|Carpeta|  
|`101`|READ_OBJECTS|Permite a la entidad de seguridad leer todos los objetos de la carpeta.|Carpeta|  
|`102`|MODIFY_OBJECTS|Permite a la entidad de seguridad modificar todos los objetos de la carpeta.|Carpeta|  
|`103`|EXECUTE_OBJECTS|Permite a la entidad de seguridad ejecutar todos los paquetes de todos los proyectos de la carpeta.|Carpeta|  
|`104`|MANAGE_OBJECT_PERMISSIONS|Permite a la entidad de seguridad administrar los permisos de todos los objetos de la carpeta.|Carpeta|  
  
## <a name="permissions"></a>Permisos  
 Esta vista no proporciona una vista completa de los permisos para la entidad de seguridad actual. El usuario también debe comprobar si el entidad de seguridad es un miembro de los roles y grupos que tienen permisos asignados.  
  
  
