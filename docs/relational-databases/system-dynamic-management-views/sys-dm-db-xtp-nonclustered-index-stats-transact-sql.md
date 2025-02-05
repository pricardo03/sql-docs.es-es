---
title: sys.dm_db_xtp_nonclustered_index_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_xtp_nonclustered_index_stats_TSQL
- dm_db_xtp_nonclustered_index_stats
- sys.dm_db_xtp_nonclustered_index_stats_TSQL
- sys.dm_db_xtp_nonclustered_index_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_nonclustered_index_stats
ms.assetid: d55ba31c-296c-419b-9c4b-c126e0a3d156
author: stevestein
ms.author: sstein
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 726fd7d44ed64dfee609ad29181a2077364d72e9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68026787"
---
# <a name="sysdmdbxtpnonclusteredindexstats-transact-sql"></a>sys.dm_db_xtp_nonclustered_index_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  sys.dm_db_xtp_nonclustered_index_stats incluye estadísticas sobre las operaciones en índices no clúster en tablas optimizadas para memoria. sys.dm_db_xtp_nonclustered_index_stats contiene una fila por cada índice no clúster de una tabla optimizada para memoria de la base de datos actual.  
  
 Las estadísticas reflejadas en sys.dm_db_xtp_nonclustered_index_stats se recopilan cuando se crea la estructura de índice en memoria. Las estructuras de índice en memoria se vuelven a crear cuando se reinicia la base de datos.  
  
 Use sys.dm_db_xtp_nonclustered_index_stats para entender y supervisar la actividad de índices durante las operaciones DML y cuando se pone en línea una base de datos. Cuando se reinicia una base de datos que tiene una tabla optimizada para memoria, el índice se genera insertando una fila cada vez en la memoria. El recuento de divisiones, mezclas y consolidaciones de páginas puede ayudarle a entender el trabajo realizado para generar el índice cuando se pone en línea una base de datos. También puede examinar estos recuentos antes y después de una serie de operaciones DML.  
  
 Un gran número de reintentos indica la existencia de problemas de simultaneidad; llame al servicio de soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
 Para obtener más información acerca de los índices no clúster optimizados para memoria, vea [SQL Server In-Memory OLTP Internals Overview](https://t.co/T6zToWc6y6), página 17.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|object_id|**int**|Id. del objeto.|  
|xtp_object_id|**bigint**|Identificador de la tabla optimizada para memoria.|  
|index_id|**int**|Id. del índice.|  
|delta_pages|**bigint**|Número total de páginas delta de este índice en el árbol.|  
|internal_pages|**bigint**|Para uso interno. Número total de páginas internas de este índice en el árbol.|  
|leaf_pages|**bigint**|Número total de páginas hoja de este índice en el árbol.|  
|outstanding_retired_nodes|**bigint**|Para uso interno. Número total de nodos de este índice en las estructuras internas.|  
|page_update_count|**bigint**|Número acumulativo de operaciones que actualizan una página del índice.|  
|page_update_retry_count|**bigint**|Número acumulativo de reintentos de una operación que actualiza una página del índice.|  
|page_consolidation_count|**bigint**|Número acumulativo de consolidaciones de páginas del índice.|  
|page_consolidation_retry_count|**bigint**|Número acumulativo de reintentos de operaciones de consolidación de páginas.|  
|page_split_count|**bigint**|Número acumulativo de operaciones de división de páginas del índice.|  
|page_split_retry_count|**bigint**|Número acumulativo de reintentos de operaciones de división de páginas.|  
|key_split_count|**bigint**|Número acumulativo de divisiones de clave del índice.|  
|key_split_retry_count|**bigint**|Número acumulativo de reintentos de operaciones de división de clave.|  
|page_merge_count|**bigint**|Número acumulativo de operaciones de mezcla de páginas del índice.|  
|page_merge_retry_count|**bigint**|Número acumulativo de reintentos de operaciones de mezcla de páginas.|  
|key_merge_count|**bigint**|Número acumulativo de operaciones de mezcla de claves del índice.|  
|key_merge_retry_count|**bigint**|Número acumulativo de reintentos de operaciones de mezcla de claves.|  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso VIEW DATABASE STATE en la base de datos actual.  
  
## <a name="see-also"></a>Vea también  
 [Vistas de administración dinámica de tabla optimizado para memoria &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
