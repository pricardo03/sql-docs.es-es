---
title: Sys.sysusers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sysusers
- sys.sysusers_TSQL
- sysusers_TSQL
- sysusers
dev_langs:
- TSQL
helpviewer_keywords:
- sysusers system table
- sys.sysusers compatibility view
ms.assetid: 5f0e6a8d-c983-44f6-97e9-aab5bff67d18
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1b8bec28a2e7778a449cb36aeee81481a311c6b9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68018061"
---
# <a name="syssysusers-transact-sql"></a>sys.sysusers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Contiene una fila para cada [!INCLUDE[msCoName](../../includes/msconame-md.md)] usuario de Windows, el grupo de Windows, [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usuario, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rol en la base de datos.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**UID**|**smallint**|Id. de usuario, único en esta base de datos.<br /><br /> 1 = Propietario de la base de datos<br /><br /> Produce un desbordamiento o devuelve NULL si el número de usuarios y roles es superior a 32.767.|  
|**status**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**name**|**sysname**|Nombre de usuario o de grupo, único en esta base de datos.|  
|**sid**|**varbinary(85)**|Identificador de seguridad de esta entrada.|  
|**Roles**|**varbinary(2048)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**createdate**|**datetime**|Fecha en que se agregó la cuenta.|  
|**updatedate**|**datetime**|Fecha en que se cambió la cuenta por última vez.|  
|**altuid**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> Produce un desbordamiento o devuelve NULL si el número de usuarios y roles es superior a 32.767.|  
|**password**|**varbinary(256)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**GID**|**smallint**|Id. de grupo al que pertenece este usuario. Si **uid** es el mismo que **gid**, esta entrada define un grupo. Produce un desbordamiento o devuelve NULL si el número combinado de grupos y usuarios es superior a 32.767.|  
|**Environ**|**varchar(255)**|Reservado.|  
|**hasdbaccess**|**int**|1 = La cuenta tiene acceso a la base de datos.|  
|**islogin**|**int**|1 = La cuenta pertenece a un grupo de Windows, a un usuario de Windows o a un usuario de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con una cuenta de inicio de sesión.|  
|**isntname**|**int**|1 = La cuenta corresponde a un usuario o grupo de Windows.|  
|**isntgroup**|**int**|1 = La cuenta corresponde a un grupo de Windows.|  
|**isntuser**|**int**|1 = La cuenta corresponde a un usuario de Windows.|  
|**issqluser**|**int**|1 = La cuenta corresponde a un usuario de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**isaliased**|**int**|1 = La cuenta tiene un alias para otro usuario.|  
|**issqlrole**|**int**|1 = La cuenta corresponde a un rol de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**isapprole**|**int**|1 = La cuenta corresponde a un rol de aplicación.|  
  
## <a name="see-also"></a>Vea también  
 [Asignar tablas del sistema a vistas del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Vistas de compatibilidad &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
