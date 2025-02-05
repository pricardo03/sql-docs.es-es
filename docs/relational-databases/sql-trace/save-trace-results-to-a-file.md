---
title: Guardar los resultados de un seguimiento en un archivo | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 74f80667-62f3-4e14-bb1a-f0c2b6ef3402
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4d0c3b205b457b35d39e8e2648661c1de5e494fe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68132197"
---
# <a name="save-trace-results-to-a-file"></a>Guardar los resultados de un seguimiento en un archivo
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Los resultados de un seguimiento se pueden guardar en un archivo. Un archivo de seguimiento es un archivo donde se escriben los resultados de un seguimiento. Un archivo de seguimiento puede ubicarse en un directorio local (por ejemplo C:\\*nombreDeCarpeta*\\*nombreDeArchivo.trc*) o un directorio de red (por ejemplo \\\nombreDeEquipo\nombreDeRecursoCompartido\nombreDeArchivo.trc).  
  
 Puede utilizar los archivos de seguimiento para realizar lo siguiente:  
  
-   Reproducir seguimientos  
  
-   Auditar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Realizar análisis de rendimiento  
  
-   Correlacionar eventos de seguimiento con contadores de rendimiento para mejorar la detección de problemas  
  
-   Realizar análisis del Asistente para la optimización de motor de bases de datos  
  
-   Optimizar las consultas  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] guarda los resultados de seguimiento en un archivo cuando se ha especificado una ruta de acceso y un nombre de archivo para el argumento **@tracefile** del procedimiento almacenado **sp_trace_create**.  
  
> [!NOTE]  
>  Si hay especificada una ruta de acceso al procedimiento almacenado **sp_trace_create** para guardar el archivo de seguimiento, el directorio debe ser accesible para el servidor. También debe tener presente que si un directorio local está especificado con **sp_trace_create**, se trata de un directorio local en el equipo servidor.  
  
 Si se utiliza [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] , ello le permite guardar los resultados de un seguimiento en un archivo o una tabla. Si guarda los resultados de un seguimiento en una tabla, tendrá el mismo acceso que si guarda el seguimiento en un archivo, además de poder realizar consultas en la tabla para buscar eventos específicos.  
  
 Para obtener más información sobre cómo guardar los resultados de seguimiento, vea [Guardar los resultados de un seguimiento en una tabla &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-table-sql-server-profiler.md) y [Guardar los resultados de seguimiento en un archivo &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-file-sql-server-profiler.md).  
  
## <a name="see-also"></a>Consulte también  
 [sp_trace_create &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)   
 [Crear un seguimiento &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)   
 [Crear un seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
  
  
