---
title: sp_dbmmonitorhelpalert (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dbmmonitorhelpalert_TSQL
- sp_dbmmonitorhelpalert
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbmmonitorhelpalert
- database mirroring [SQL Server], monitoring
ms.assetid: 43911660-b4e4-4934-8c02-35221160aaec
author: stevestein
ms.author: sstein
ms.openlocfilehash: fc850c8be9b5222fe178563de78e34e2ba263c12
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67899189"
---
# <a name="spdbmmonitorhelpalert-transact-sql"></a>sp_dbmmonitorhelpalert (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información acerca de los umbrales de advertencia de una o todas las métricas claves de rendimiento de creación de reflejo de la base de datos.  
 
  ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_dbmmonitorhelpalert database_name   
    [ , alert_id ]   
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 Especifica la base de datos.  
  
 [ *alert_id* ]  
 Valor entero que identifica la advertencia que se va a devolver. Si se omite este argumento, se devuelven todas las advertencias, pero no se devuelve el período de retención.  
  
 Para devolver una advertencia determinada, especifique uno de los valores siguientes:  
  
|Valor|Métrica de rendimiento|Umbral de advertencia|  
|-----------|------------------------|-----------------------|  
|1|Transacción no enviada más antigua|Especifica el número de minutos de transacciones que se pueden acumular en la cola de envío antes de que se genere una advertencia en la instancia del servidor principal. Esta advertencia ayuda a medir el potencial de pérdida de datos en términos de tiempo y es especialmente relevante para el modo de alto rendimiento. No obstante, la advertencia también es relevante para el modo de alta seguridad cuando la creación de reflejo se detiene o suspende debido a que los asociados se han desconectado.|  
|2|Registro sin enviar|Especifica cuántos kilobytes (KB) de registro sin enviar generan una advertencia en la instancia del servidor principal. Esta advertencia ayuda a medir el potencial de pérdida de datos en términos de KB y es especialmente relevante para el modo de alto rendimiento. No obstante, la advertencia también es relevante para el modo de alta seguridad cuando la creación de reflejo se detiene o suspende debido a que los asociados se han desconectado.|  
|3|Registro sin restaurar|Especifica cuántos KB de registro sin restaurar generan una advertencia en la instancia del servidor reflejado. Esta advertencia ayuda a medir el tiempo de conmutación por error. El*tiempo de la conmutación por error* se compone principalmente del tiempo que el servidor reflejado anterior necesita para poner al día los registros pendientes en su cola rehecha, más un breve tiempo adicional.|  
|4|Sobrecarga de confirmación del servidor reflejado|Especifica el número de milisegundos de retardo medio por transacción que se tolera antes de que se genere una advertencia en el servidor principal. Este retardo es la cantidad de sobrecarga en la que se incurre mientras la instancia del servidor principal espera a la instancia del servidor reflejado para escribir la entrada de registro de la transacción en la cola de puesta al día. Este valor solo es relevante en el modo de alta seguridad.|  
|5|Período de retención|Metadatos que controlan cómo se conservan las filas largas en la tabla de estado de la creación de reflejo de la base de datos.|  
  
 Para obtener información acerca de los identificadores de evento correspondientes a las advertencias, vea [los umbrales de advertencia de uso y las alertas en métricas de rendimiento de la creación de reflejo &#40;SQL Server&#41;](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md).  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 None  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Para cada alerta devuelta, devuelve una fila que contiene las siguientes columnas:  
  
|columna|Data type|Descripción|  
|------------|---------------|-----------------|  
|**alert_id**|**int**|La tabla siguiente muestra la **alert_id** valor para cada métrica de rendimiento y la unidad de medida de la métrica mostrada en el **sp_dbmmonitorresults** conjunto de resultados:|  
|**threshold**|**int**|Valor de umbral de la advertencia. Si se devuelve un valor superior a este umbral cuando se actualiza el estado de la creación de reflejos, se escribe una entrada en el registro de eventos de Windows. Este valor representa el número de KB, minutos o milisegundos, en función de la advertencia. Si el umbral no está establecido actualmente, el valor es NULL.<br /><br /> **Nota:** Para ver los valores actuales, ejecute el [sp_dbmmonitorresults](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md) procedimiento almacenado.|  
|**enabled**|**bit**|0 = El evento está deshabilitado.<br /><br /> 1 = El evento está habilitado.<br /><br /> **Nota:** El período de retención siempre está habilitado.|  
  
|Valor|Métrica de rendimiento|Unidad|  
|-----------|------------------------|----------|  
|1|Transacción no enviada más antigua|Minutos|  
|2|Registro sin enviar|KB|  
|3|Registro sin restaurar|KB|  
|4|Sobrecarga de confirmación del servidor reflejado|Milisegundos|  
|5|Período de retención|Horas|  
  
## <a name="permissions"></a>Permisos  
 Requiere la pertenencia al rol fijo de servidor **sysadmin** .  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se devuelve una fila que indica si una advertencia está habilitada para la métrica de rendimiento de transacción sin enviar más antigua en la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
EXEC sp_dbmmonitorhelpalert AdventureWorks2012, 1 ;  
```  
  
 El ejemplo siguiente devuelve una fila para cada métrica de rendimiento que indica si ésta está habilitada en la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
EXEC sp_dbmmonitorhelpalert AdventureWorks2012;  
```  
  
## <a name="see-also"></a>Vea también  
 [Supervisar la creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [sp_dbmmonitorchangealert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangealert-transact-sql.md)   
 [sp_dbmmonitorchangemonitoring &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql.md)   
 [sp_dbmmonitordropalert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropalert-transact-sql.md)   
 [sp_dbmmonitorupdate &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorupdate-transact-sql.md)   
 [sp_dbmmonitorhelpmonitoring &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql.md)   
 [sp_dbmmonitorresults &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)  
  
  
