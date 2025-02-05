---
title: dbo.sysjobservers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysjobservers
- sysjobservers_TSQL
- dbo.sysjobservers
- dbo.sysjobservers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobservers system table
ms.assetid: 9abcc20f-a421-4591-affb-62674d04575e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 590fa6eff10c11af303b7bb9d4750ef98852cc44
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68004807"
---
# <a name="dbosysjobservers-transact-sql"></a>dbo.sysjobservers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Almacena la asociación o relación de un trabajo determinado con uno o más servidores de destino. Esta tabla se almacena en la base de datos msdb.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|job_id|**uniqueidentifier**|Número de identificación del trabajo.|  
|server_id|**int**|Número de identificación del servidor.|  
|last_run_outcome|**tinyint**|Resultado de la última ejecución del trabajo:<br /><br /> **0** = error<br /><br /> **1** = correctamente<br /><br /> **3** = cancelado|  
|mensaje last_outcome_|**nvarchar(1024)**|Mensaje asociado, si existe, a la columna last_run_outcome.|  
|last_run_date|**int**|Fecha en que el trabajo se ejecutó por última vez.|  
|last_run_time|**int**|Hora a la que se ejecutó el trabajo por última vez.|  
|last_run_duration|**int**|Duración de la ejecución del trabajo, en horas, minutos y segundos. Calcula mediante la fórmula: (*horas*\*10000) + (*minutos*\*100) + *segundos*.|  
  
## <a name="see-also"></a>Vea también  
 [Tablas del Agente SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sql-server-agent-tables-transact-sql.md)  
  
  
