---
title: Supervisar la actividad de trabajos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, monitoring
- jobs [SQL Server Agent], monitoring
- monitoring [SQL Server], jobs
- activity monitoring [SQL Server Agent]
- monitoring [SQL Server], SQL Server Agent
- monitoring [SQL Server Agent]
- SQL Server Agent Job Activity Monitor
- SQL Server Agent jobs, monitoring
- performance [SQL Server], jobs
- current activity
ms.assetid: 71cb432b-631d-4b8b-9965-e731b3d8266d
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a227b7ee1723dd8a77d7eb118476969575c5951c
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68267502"
---
# <a name="monitor-job-activity"></a>Actividad de trabajos de monitor
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

Puede supervisar la actividad actual de todos los trabajos definidos de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante el Monitor de actividad de trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="sql-server-agent-sessions"></a>Sesiones del Agente SQL Server  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] El Agente crea una sesión cada vez que se inicia el servicio. Al crear una sesión, la tabla **sysjobactivity** de la base de datos **msdb** se rellena con todos los trabajos definidos existentes. Esta tabla mantiene la última actividad para los trabajos cuando se reinicia el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Cada sesión registra la actividad de trabajo normal del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde el inicio del trabajo hasta que termina. La información acerca de estas sesiones se almacena en la tabla **syssessions** de la base de datos **msdb** .  
  
## <a name="job-activity-monitor"></a>Monitor de actividad de trabajo  
El Monitor de actividad de trabajo permite ver la tabla **sysjobactivity** mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Puede ver todos los trabajos del servidor, o bien puede definir filtros para limitar el número de trabajos mostrados. También puede ordenar la información sobre los trabajos haciendo clic en un encabezado de columna de la cuadrícula **Actividad de trabajo del agente** . Por ejemplo, al seleccionar el encabezado de columna **Última ejecución** , puede ver los trabajos en el orden en que se ejecutaron por última vez. Al volver a hacer clic en el encabezado de columna, el orden de los trabajos cambia entre ascendente y descendente basándose en la fecha en que se ejecutaron por última vez.  
  
El Monitor de actividad de trabajo le permite realizar las siguientes tareas:  
  
-   Iniciar y detener trabajos.  
  
-   Ver las propiedades del trabajo.  
  
-   Ver el historial de un determinado trabajo.  
  
-   Actualizar la información de la cuadrícula **Actividad de trabajo del agente** manualmente o establecer un intervalo de actualización automático haciendo clic en **Ver configuración de actualización**.  
  
Utilice el Monitor de actividad de trabajo cuando desee localizar los trabajos que están programados para su ejecución, el último resultado de los trabajos que se han ejecutado durante la sesión actual y localizar los trabajos que se están ejecutando actualmente o que están inactivos. Si el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiene un error inesperado, puede determinar los trabajos que se estaban ejecutando buscando en la sesión anterior del Monitor de actividad de trabajo.  
  
Para abrir el Monitor de actividad de trabajo, expanda **Agente SQL Server** en el Explorador de objetos de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] , haga clic con el botón derecho en **Monitor de actividad de trabajo**y haga clic en **Ver actividad de trabajo**.  
  
También puede ver la actividad de trabajo de la sesión actual mediante el procedimiento almacenado **sp_help_jobactivity**.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**Descripción**|**Tema**|  
|Describe cómo ver el estado de tiempo de ejecución de los trabajos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|[Ver actividad de trabajo](../../ssms/agent/view-job-activity.md)|  
  
## <a name="see-also"></a>Consulte también  
[Ver actividad de trabajo](../../ssms/agent/view-job-activity.md)  
[sysjobactivity (Transact-SQL)](https://msdn.microsoft.com/fd17cac9-5d1f-4b44-b2dc-ee9346d8bf1e)  
[syssessions (Transact-SQL)](https://msdn.microsoft.com/187819b6-c7f4-4a26-b74c-0a89e96695cf)  
[sp_help_jobactivity (Transact-SQL)](https://msdn.microsoft.com/d344864f-b4d3-46b1-8933-b81dec71f511)  
  
