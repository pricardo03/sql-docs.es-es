---
title: MSSQLSERVER_17300 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17300 (Database Engine error)
ms.assetid: c1d6bfb6-28af-4df6-8087-25807602d282
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a6577ec13cc990eb65d66eb2975d61b5f1147201
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62915354"
---
# <a name="mssqlserver17300"></a>MSSQLSERVER_17300
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|17300|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|PROC_OUT_OF_SYSTASK_SESSIONS|  
|Texto del mensaje|SQL Server no pudo ejecutar una nueva tarea de sistema porque la memoria no es suficiente o porque el número de sesiones configuradas supera el máximo permitido en el servidor. Compruebe que el servidor tiene la memoria necesaria. Utilice sp_configure con la opción 'user connections' para comprobar el número máximo de conexiones de usuario permitido. Utilice sys.dm_exec_sessions para comprobar el número de sesiones actual, incluidos los procesos de usuario.|  
  
## <a name="explanation"></a>Explicación  
 Se ha producido un error en un intento de ejecutar una nueva tarea de sistema porque la memoria no es suficiente o porque se ha superado el número de sesiones configuradas en el servidor.  
  
## <a name="user-action"></a>Acción del usuario  
 Compruebe que el servidor tiene memoria suficiente. Compruebe el número actual de tareas de sistema utilizando sys.dm_exec_sessions, y compruebe el valor configurado de conexiones de usuario máximas utilizando sp_configure.  
  
 Realice las siguientes tareas, según corresponda:  
  
-   Agregue más memoria al servidor.  
  
-   Finalice una o más sesiones.  
  
-   Aumente el número máximo de conexiones de usuario permitido en el servidor.  
  
## <a name="see-also"></a>Vea también  
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sys.dm_exec_sessions &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql)   
 [Configurar la opción de configuración del servidor de conexiones de usuario](../../database-engine/configure-windows/configure-the-user-connections-server-configuration-option.md)   
 [KILL &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/kill-transact-sql)  
  
  
