---
title: Optimización del seguimiento de SQL | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- time [SQL Server], traces
- SQL Trace, performance
- traces [SQL Server], performance
- performance [SQL Server], trace
ms.assetid: 50944218-925f-4576-aec8-4379846d7681
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 59b1a599a38e31abeee677059d5a99842e76d807
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68033218"
---
# <a name="optimize-sql-trace"></a>Optimizar el seguimiento de SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Aunque la ejecución de Seguimiento de SQL supone un costo de rendimiento porque utiliza recursos del sistema para recopilar datos, dicho costo se puede reducir al mínimo de muchas maneras. Para minimizar el costo de rendimiento que provoca un seguimiento, intente las siguientes acciones:  
  
-   Considere el uso del símbolo del sistema para ejecutar seguimientos. El uso de una interfaz gráfica de usuario afecta negativamente al rendimiento. Para obtener más información, vea [sp_trace_create &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md).  
  
-   Evite incluir eventos que tienen lugar con frecuencia. Si es posible, ajuste el seguimiento con clases de eventos específicas y filtros. Si se recopilan menos eventos de seguimiento, serán necesarios menos recursos del sistema para admitir las trazas.  
  
-   Ajuste el seguimiento para que solo recopile eventos que proporcionen datos relevantes. Por ejemplo, si el seguimiento va a identificar interbloqueos, incluya la clase de evento **Lock:Deadlock** , pero no la clase **Lock:Acquired** . Si incluye ambas clases de eventos, el seguimiento debe responder a todos los bloqueos que se adquieren y el costo de ejecución se duplica.  
  
-   Evite recopilar datos duplicados. Por ejemplo, si recopila datos de **SQL:BatchStarted** y **SQL:BatchCompleted**, puede minimizar el tamaño del conjunto de resultados recopilando datos de texto únicamente para la clase de evento **SQL:BatchStarted** .  
  
-   Utilice filtros en la definición del seguimiento. Por ejemplo, si sabe que determinado usuario obtiene un rendimiento lento durante las consultas ad hoc, cree un filtro por **LoginName**. Configure el filtro para incluir solo los eventos en los que **LoginName** coincida con el nombre de usuario.  
  
 Si debe ejecutar un seguimiento para eventos que afectan significativamente al rendimiento, considere la posibilidad de limitar el impacto en el servidor mediante uno de los siguientes métodos:  
  
-   Ejecute los seguimientos durante períodos más breves. Puede controlar el tiempo de ejecución de un seguimiento habilitando una hora de detención. Esto es especialmente importante si no puede limitar las clases de eventos o filtrar un evento. La habilitación de una hora de detención asegura que la duración del costo de rendimiento no es indefinida.  
  
-   Limite el tamaño de los resultados del seguimiento. Puede limitar el tamaño de los resultados del seguimiento a un tamaño de archivo máximo. Esta estrategia asegura que el costo de rendimiento se detiene cuando se alcanza el límite de tamaño del archivo (si no está habilitada la sustitución incremental de archivos).  
  
-   Limite el número de eventos que se devuelven. Con [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] , puede limitar el número de eventos devueltos guardando el seguimiento en una tabla y configurando el número máximo de filas. Los resultados del seguimiento siguen mostrándose en la pantalla de [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] tras alcanzar el número máximo de filas, pero se elimina el costo de registrar los resultados en una tabla.  
  
## <a name="see-also"></a>Consulte también  
 [Filtrar un seguimiento](../../relational-databases/sql-trace/filter-a-trace.md)  
  
  
