---
title: Sys.dm_os_memory_nodes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_memory_nodes_TSQL
- sys.dm_os_memory_nodes
- sys.dm_os_memory_nodes_TSQL
- dm_os_memory_nodes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_nodes dynamic management view
ms.assetid: bf4032fe-7db1-40e9-a62e-d69cebff4b44
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7d1be540f73a5a5e625a1f33f1c3f24e409fd307
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265762"
---
# <a name="sysdmosmemorynodes-transact-sql"></a>sys.dm_os_memory_nodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Las asignaciones internas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizan el administrador de memoria de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Seguimiento de la diferencia entre los contadores de memoria de proceso de **sys.dm_os_process_memory** y los contadores internos pueden indicar el uso de memoria de los componentes externos en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] espacio de memoria.  
  
 Los nodos se crean por nodo de memoria de NUMA físico. Estos podrían ser diferentes de los nodos de CPU en **sys.dm_os_nodes**.  
  
 Se realiza un seguimiento de las asignaciones que no se realizan directamente a través de las rutinas de asignación de memoria de Windows. La tabla siguiente proporciona información sobre asignaciones de memoria que se han realizado utilizando únicamente las interfaces de administrador de memoria de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Al llamarlo desde [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use el nombre **sys.dm_pdw_nodes_os_memory_nodes**.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**memory_node_id**|**smallint**|Especifica el identificador del nodo de memoria. Relacionadas con **memory_node_id** de **sys.dm_os_memory_clerks**. No acepta valores NULL.|  
|**virtual_address_space_reserved_kb**|**bigint**|Indica el número de reservas de dirección virtual, en kilobytes (KB), que no se han confirmado ni asignado a páginas físicas. No acepta valores NULL.|  
|**virtual_address_space_committed_kb**|**bigint**|Especifica la cantidad de dirección virtual, en KB, que se ha confirmado o asignado a páginas físicas. No acepta valores NULL.|  
|**locked_page_allocations_kb**|**bigint**|Especifica la cantidad de memoria física, en KB, bloqueada por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No acepta valores NULL.|  
|**single_pages_kb**|**bigint**|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Cantidad de memoria confirmada, en KB, que se asigna utilizando el asignador de páginas individuales por subprocesos que se ejecutan en este nodo. Esta memoria se asigna desde el grupo de búferes. Este valor indica el nodo donde se ha producido la solicitud de las asignaciones, no la ubicación física donde se satisfizo la solicitud de asignación.|  
|**pages_kb**|**bigint**|**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Especifica la cantidad de memoria confirmada, En KB, que se ha asignado desde este nodo NUMA mediante el Asignador de páginas del Administrador de memoria. No acepta valores NULL.|  
|**multi_pages_kb**|**bigint**|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Cantidad de memoria confirmada, en KB, que se asigna utilizando el asignador de páginas múltiples por subprocesos que se ejecutan en este nodo. Esta memoria se asigna desde fuera del grupo de búferes. Este valor indica el nodo donde se han producido las solicitudes de las asignaciones, no la ubicación física donde se satisfizo la solicitud de asignación.|  
|**shared_memory_reserved_kb**|**bigint**|Especifica la cantidad de memoria compartida, en KB, que se ha reservado desde este nodo. No acepta valores NULL.|  
|**shared_memory_committed_kb**|**bigint**|Especifica la cantidad de memoria compartida, en KB, que se ha confirmado en este nodo. No acepta valores NULL.|  
|**cpu_affinity_mask**|**bigint**|**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Exclusivamente para uso interno. No acepta valores NULL.|  
|**online_scheduler_mask**|**bigint**|**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Exclusivamente para uso interno. No acepta valores NULL.|  
|**processor_group**|**smallint**|**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Exclusivamente para uso interno. No acepta valores NULL.|  
|**foreign_committed_kb**|**bigint**|**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Especifica la cantidad de memoria confirmada, en KB, desde otros nodos de memoria. No acepta valores NULL.|  
|**target_kb** |**bigint** |**Se aplica a**: de [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> Especifica el objetivo de memoria para el nodo de memoria en KB. |   
|**pdw_node_id**|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> El identificador para el nodo en esta distribución.|  
  
## <a name="permissions"></a>Permisos

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles Premium, requieren el `VIEW DATABASE STATE` permiso en la base de datos. En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] niveles estándar y básico, requiere el **administrador del servidor** o un **Administrador de Azure Active Directory** cuenta.   

## <a name="see-also"></a>Vea también  
  [Vistas de administración dinámica relacionadas con el sistema operativo SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


