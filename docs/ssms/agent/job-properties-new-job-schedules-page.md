---
title: 'Propiedades del trabajo: Nuevo trabajo (página Programaciones) | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.job.schedules.f1
ms.assetid: 0b03585b-a510-484d-8a63-9b32459def9c
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 4d9d06def940d757e183b2ed6341d034628ccea7
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68267823"
---
# <a name="job-properties---new-job-schedules-page"></a>Propiedades del trabajo - Nuevo trabajo (página Programaciones)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

Utilice esta página para ver y organizar las programaciones de un trabajo del Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="options"></a>Opciones  
**Lista de programaciones**  
Muestra las programaciones para este trabajo.  
  
**Nueva**  
Crea una nueva programación. Una vez que se haya creado la programación, ésta se agregará al trabajo.  
  
**Seleccionar**  
Selecciona una de las programaciones existentes. Puesto que un trabajo y una programación deben tener el mismo propietario, esta opción solo le permitirá seleccionar programaciones de su propiedad.  
  
**Editarar**  
Edita la programación seleccionada para cambiar las propiedades de programación del trabajo.  
  
**Quitar**  
Quita la programación seleccionada del trabajo. Si no hay otros trabajos que utilicen la programación, ésta se elimina de la base de datos.  
  
## <a name="see-also"></a>Consulte también  
[Implementar trabajos](../../ssms/agent/implement-jobs.md)  
  
