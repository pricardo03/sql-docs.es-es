---
title: Sys.dm_db_missing_index_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_missing_index_columns_TSQL
- sys.dm_db_missing_index_columns_TSQL
- sys.dm_db_missing_index_columns
- dm_db_missing_index_columns
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_missing_index_columns dynamic management function
- missing indexes feature [SQL Server], sys.dm_db_missing_index_columns dynamic management function
ms.assetid: 3b24e5ed-0c79-47e5-805c-a0902d0aeb86
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 38d21e20ec158ea316caf6acd17f7225c8d3a49d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68002652"
---
# <a name="sysdmdbmissingindexcolumns-transact-sql"></a>sys.dm_db_missing_index_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve información sobre las columnas de la tabla de la base de datos que no tienen índice, sin incluir los índices espaciales. **Sys.dm_db_missing_index_columns** es una función de administración dinámica.  

## <a name="syntax"></a>Sintaxis  
  
```  
  
sys.dm_db_missing_index_columns(index_handle)  
```  
  
## <a name="arguments"></a>Argumentos  
 *index_handle*  
 Un entero que identifica de forma única un índice que falta. Puede obtenerse a partir de los siguientes objetos de administración dinámica:  
  
 [sys.dm_db_missing_index_details &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)  
  
 [sys.dm_db_missing_index_groups &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-groups-transact-sql.md)  
  
## <a name="table-returned"></a>Tabla devuelta  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**column_id**|**int**|Identificador de la columna.|  
|**column_name**|**sysname**|Nombre de la columna de la tabla.|  
|**column_usage**|**varchar(20)**|Forma en que la consulta utiliza la columna. Son los valores posibles y sus descripciones:<br /><br /> IGUALDAD: Columna contribuye a un predicado que expresa igualdad, del formulario: <br />                        *table.column* = *constant_value*<br /><br /> DESIGUALDAD: Columna contribuye a crear un predicado que expresa desigualdad, por ejemplo, un predicado del formulario: *table.column* > *constant_value*. Cualquier operador de comparación distinto de "=" expresa desigualdad.<br /><br /> INCLUÍR: Columna no se usa para evaluar un predicado, pero se utiliza cualquier otro motivo, por ejemplo, para cubrir una consulta.|  
  
## <a name="remarks"></a>Comentarios  
 Información devuelta por **sys.dm_db_missing_index_columns** se actualiza cuando una consulta está optimizada por el optimizador de consultas y no se conserva. La información sobre índices que faltan solo se conserva hasta que se reinicia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los administradores de bases de datos deben realizar copias de seguridad de forma periódica de la información de índices que faltan si desean conservarla después de reciclar el servidor.  
  
## <a name="transaction-consistency"></a>Coherencia de las transacciones  
 Si una transacción crea o quita una tabla, las filas que contienen información de índices que faltan sobre los objetos quitados se eliminan de este objeto de administración dinámica para mantener la coherencia de la transacción.  
  
## <a name="permissions"></a>Permisos  
 Los usuarios deben disponer del permiso VIEW SERVER STATE o de cualquier permiso que implique el permiso VIEW SERVER STATE para consultar esta función de administración dinámica.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se ejecuta una consulta en la tabla `Address` y, después, otra con la vista de administración dinámica `sys.dm_db_missing_index_columns` para devolver las columnas de la tabla a las que les falta un índice.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT City, StateProvinceID, PostalCode  
FROM Person.Address  
WHERE StateProvinceID = 9;  
GO  
SELECT mig.*, statement AS table_name,  
    column_id, column_name, column_usage  
FROM sys.dm_db_missing_index_details AS mid  
CROSS APPLY sys.dm_db_missing_index_columns (mid.index_handle)  
INNER JOIN sys.dm_db_missing_index_groups AS mig ON mig.index_handle = mid.index_handle  
ORDER BY mig.index_group_handle, mig.index_handle, column_id;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sys.dm_db_missing_index_details &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)   
 [sys.dm_db_missing_index_groups &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-groups-transact-sql.md)   
 [sys.dm_db_missing_index_group_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-group-stats-transact-sql.md)  
  
  
