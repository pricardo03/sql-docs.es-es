---
title: catalog.environment_references (base de datos de SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: efec53ef-3e5a-4b76-b71d-a0cf9e11ac00
author: janinezhang
ms.author: janinez
ms.openlocfilehash: c70439da5ba3f09cd39ea9cec78a14ea366d126d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038411"
---
# <a name="catalogenvironmentreferences-ssisdb-database"></a>catalog.environment_references (base de datos de SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Muestra las referencias del entorno de todos los proyectos en el catálogo de **SSISDB**.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|reference_id|**bigint**|Identificador (id.) único de la referencia.|  
|identificador de proyecto|**bigint**|Identificador único del proyecto.|  
|reference_type|**char(1)**|Indica si el entorno se puede encontrar en la misma carpeta que el proyecto (referencia relativa) o en una carpeta diferente (referencia absoluta). Cuando el valor es `R`, el entorno se encuentra utilizando una referencia relativa. Cuando el valor es `A`, el entorno se encuentra utilizando una referencia absoluta.|  
|environment_folder_name|**sysname**|Nombre de la carpeta si el entorno se encuentra utilizando una referencia absoluta.|  
|environment_name|**sysname**|Nombre del entorno al que hace referencia el proyecto.|  
|validation_status|**char(1)**|El estado de la validación.|  
|last_validation_time|**datatimeoffset(7)**|Hora de la última validación.|  
  
## <a name="remarks"></a>Notas  
 En esta vista se muestra una fila por cada referencia al entorno del catálogo.  
  
## <a name="permissions"></a>Permisos  
 Esta vista exige uno de los siguientes permisos:  
  
-   Permiso READ en el proyecto correspondiente  
  
-   Pertenencia al rol de base de datos de **ssis_admin**  
  
-   Pertenencia al rol del servidor de **sysadmin**  
  
> [!NOTE]  
>  Si tiene permiso READ en un proyecto, también tendrá permiso READ en todos los paquetes y referencias de entorno asociados a ese proyecto. Se aplica la seguridad en el nivel de fila; solo se muestran las filas para las que disponga de permiso para ver.  
  
## <a name="remarks"></a>Notas  
 Un proyecto puede tener referencias de entorno absolutas o relativas. Las referencias relativas se refieren al entorno por nombre y requieren que resida en la misma carpeta que el proyecto. Las referencias absolutas hacen referencia al entorno por nombre y carpeta, y pueden hacer referencia a los entornos que residen en una carpeta diferente que el proyecto. Un proyecto puede hacer referencia a varios entornos.  
  
  
