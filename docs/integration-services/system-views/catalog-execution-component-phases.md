---
title: catalog.execution_component_phases | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 07a9a163-4787-40f7-b371-ac5c6cb4b095
author: janinezhang
ms.author: janinez
ms.openlocfilehash: ce4f3284e5b0e483c09ea9cc95e64ed20fc1a1cd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68065252"
---
# <a name="catalogexecutioncomponentphases"></a>catalog.execution_component_phases 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Muestra el tiempo dedicado por un componente de flujo de datos a cada fase de ejecución.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|phase_stats_id|**bigint**|Identificador (id.) único de la fase.|  
|execution_id|**bigint**|Identificador único de la instancia de ejecución.|  
|package_name|**nvarchar(260)**|Nombre del primer paquete que se inició durante la ejecución.|  
|task_name|**nvarchar(4000)**|Nombre de la tarea Flujo de datos.|  
|subcomponent_name|**nvarchar(4000)**|Nombre del componente de flujo de datos.|  
|phase|**nvarchar(128)**|Nombre de la fase de ejecución.|  
|start_time|**datetimeoffset(7)**|Hora a la que se inició la fase.|  
|end_time|**datetimeoffset(7)**|Hora a la que finalizó la fase.|  
|execution_path|**nvarchar(max)**|Ruta de ejecución de la tarea Flujo de datos.|  
  
## <a name="remarks"></a>Notas  
 Esta vista muestra una fila para cada fase de ejecución de un componente de flujo de datos, como Validate, Pre-Execute, Post-Execute, PrimeOutput y ProcessInput. Cada fila muestra la hora de inicio y de finalización de una fase de ejecución concreta.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se usa la vista catalog.execution_component_phases para averiguar la cantidad total de tiempo que invierte un paquete concreto para su ejecución en todas las fases (**active_time**) y el tiempo transcurrido total para el paquete (**total_time**).  
  
> [!WARNING]  
>  La vista catalog.execution_component_phases proporciona esta información cuando el nivel de registro de la ejecución del paquete se establece en Performance (Rendimiento) o Verbose (Detallado). Para más información, vea [Habilitar el registro para la ejecución de paquetes en el servidor SSIS](../../integration-services/performance/integration-services-ssis-logging.md#server_logging).  
  
```sql
use SSISDB  
select package_name, task_name, subcomponent_name, execution_path,  
    SUM(DATEDIFF(ms,start_time,end_time)) as active_time,  
    DATEDIFF(ms,min(start_time), max(end_time)) as total_time  
from catalog.execution_component_phases  
where execution_id = 1841  
group by package_name, task_name, subcomponent_name, execution_path  
order by package_name, task_name, subcomponent_name, execution_path  
```  
  
## <a name="permissions"></a>Permisos  
 Esta vista exige uno de los siguientes permisos:  
  
-   Permiso READ en la instancia de ejecución  
  
-   Pertenencia al rol de base de datos de **ssis_admin**  
  
-   Pertenencia al rol de servidor de **sysadmin**  
  
> [!NOTE]  
>  Cuando se dispone de permiso para realizar una operación en el servidor, también se dispone de permiso para ver información sobre la operación. Se aplica la seguridad en el nivel de fila; solo se muestran las filas para las que disponga de permiso para ver.  
  
  
