---
title: Configurar el cierre de la ejecución de trabajos (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], stopping
- SQL Server Agent jobs, stopping
- stopping jobs
- SQL Server Agent jobs, execution shutdowns
ms.assetid: ac23e88f-53fc-41de-bb16-0c27c002d5a5
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 14e03fffc3a952464bc0949d7023bfa8a20c4f89
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68267837"
---
# <a name="set-job-execution-shutdown-sql-server-management-studio"></a>Configurar el cierre de la ejecución de trabajos (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

En este tema se describe cómo configurar el tiempo que el Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esperará a que finalice la ejecución de los trabajos antes de que el propio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] finalice en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
**En este tema**  
  
-   **Antes de empezar:**  
  
    [Seguridad](#Security)  
  
-   **Para establecer un tiempo de cierre para un trabajo del Agente SQL Server, utilizando:**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>Antes de empezar  
  
### <a name="Security"></a>Seguridad  
  
#### <a name="Permissions"></a>Permissions  
De forma predeterminada, los miembros del rol fijo de servidor **sysadmin** pueden establecer el tiempo que el Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esperará a que finalice la ejecución de los trabajos antes de que el propio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] finalice. Al resto de usuarios se les debe conceder uno de los siguientes roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
## <a name="SSMSProcedure"></a>Usar SQL Server Management Studio  
  
#### <a name="to-set-job-execution-shutdown"></a>Para configurar el cierre de la ejecución de trabajos  
  
1.  En **El Explorador de objetos** , haga clic en el signo más para expandir el servidor en el que desea establecer un intervalo de cierre de la ejecución de trabajos.  
  
2.  Haga clic con el botón derecho en **Agente SQL Server** y seleccione **Propiedades**.  
  
3.  En **Seleccionar una página**, seleccione **Sistema de trabajo**.  
  
4.  Configure **Intervalo de tiempo de espera de cierre** en segundos para aumentar o reducir dicho intervalo. Así se determina el tiempo que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] va a esperar a que finalice la ejecución de los trabajos antes de que se cierre el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
