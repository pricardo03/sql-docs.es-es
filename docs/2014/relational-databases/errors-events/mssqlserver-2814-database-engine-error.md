---
title: MSSQLSERVER_2814 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2814 (Database Engine error)
ms.assetid: 22800748-9be9-4511-9428-6b8b40e5bef9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4c8def0fad1ae7eddb9de2e7206923b872c41ed2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "67046773"
---
# <a name="mssqlserver2814"></a>MSSQLSERVER_2814
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|2814|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|PR_POSSIBLE_INFINITE_RECOMPILE|  
|Texto del mensaje|Se detectó una posible recompilación infinita de SQLHANDLE %hs, PlanHandle %hs, desplazamiento de inicio %d, desplazamiento de fin %d. El motivo de la última recompilación fue % d.|  
  
## <a name="explanation"></a>Explicación  
 Una o más instrucciones hicieron que el lote de consultas se recompilara por lo menos 50 veces. La instrucción especificada se debe corregir para evitar más recompilaciones.  
  
 En la siguiente tabla se muestran los motivos de la recompilación.  
  
|Código del motivo|Descripción|  
|-----------------|-----------------|  
|1|Esquema modificado|  
|2|Estadísticas modificadas|  
|3|Compilación diferida|  
|4|Cambio en opción configurada|  
|5|Cambio en tabla Temp|  
|6|Conjunto de filas remoto modificado|  
|7|Permisos For Browse cambiados|  
|8|Entorno de notificación de consultas modificado|  
|9|Vista de partición cambiada|  
|10|Opciones de cursor modificadas|  
|11|Opción (recompilar) solicitada.|  
  
## <a name="user-action"></a>Acción del usuario  
  
1.  Vea la instrucción que produce la recompilación ejecutando la consulta siguiente. Reemplace los marcadores de posición *sql_handle*, *starting_offset*, *ending_offset* y *plan_handle* por los valores especificados en el mensaje de error. Observe que las columnas **database_name** y **object_name** serán NULL para instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] ad hoc y preparadas.  
  
     SELECT DB_NAME(st.dbid) AS database_name  
  
     , OBJECT_NAME(st.objectid) AS object_name  
  
     , st.text  
  
     FROM sys.dm_exec_query_stats AS qs  
  
     CROSS APPLY sys.dm_exec_sql_text (*sql_handle*) AS st  
  
     WHERE qs.statement_start_offset = *starting_offset*  
  
     AND qs.statement_end_offset = *ending_offset*  
  
     AND qs.plan_handle = *plan_handle*;  
  
2.  Según sea la descripción del código del motivo, modifique la instrucción, lote o procedimiento para evitar las recompilaciones. Por ejemplo, un procedimiento almacenado puede contener una o más instrucciones SET. Estas instrucciones se deben quitar del procedimiento. Para obtener ejemplos adicionales de causas de la recompilación y sus soluciones, vea [Problemas de compilación y recompilación de lotes, y de almacenamiento en caché de planes en SQL Server 2005](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/administrator/cc966425(v=technet.10)).  
  
3.  Si el problema persiste, póngase en contacto con los Servicios de soporte al cliente (CSS) de Microsoft.  
  
## <a name="see-also"></a>Vea también  
 [SQL:StmtRecompile Event Class](../event-classes/sql-stmtrecompile-event-class.md)  
  
  
