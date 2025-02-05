---
title: sys.user_token (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.user_token
- user_token
- sys.user_token_TSQL
- user_token_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- logins [SQL Server], security tokens
- sys.user_token catalog view
- user tokens [SQL Server]
- tokens [SQL Server]
- user_token catalog view
ms.assetid: be018103-5e57-43a4-9160-9bf420892aa7
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 42214bc08d0d4eb24c3b51f3edd8010ba8bdb0e5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68095552"
---
# <a name="sysusertoken-transact-sql"></a>sys.user_token (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve una fila por cada entidad de seguridad de base de datos que forma parte del token del usuario en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**principal_id**|**int**|Id. de la entidad de seguridad. El valor es único en la base de datos.|  
|**sid**|**varbinary(85)**|Identificador de seguridad de la entidad de seguridad si ésta está definida como externa a la base de datos. Por ejemplo, puede ser un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], un inicio de sesión de Windows, un inicio de sesión del grupo de Windows o un inicio de sesión asignado a un certificado; de lo contrario, este valor es NULL.|  
|**name**|**nvarchar (128)**|Nombre de la entidad de seguridad. El valor es único en la base de datos.|  
|**type**|**nvarchar (128)**|Descripción del tipo de entidad de seguridad. Todos los tipos se asignan a **sid**. El valor puede ser uno de los siguientes:<br /><br /> SQL USER<br /><br /> WINDOWS LOGIN<br /><br /> WINDOWS GROUP<br /><br /> ROLE<br /><br /> APPLICATION ROLE<br /><br /> ROL DE BASE DE DATOS<br /><br /> USER MAPPED TO CERTIFICATE<br /><br /> USER MAPPED TO ASYMMETRIC KEY<br /><br /> CERTIFICATE<br /><br /> ASYMMETRIC KEY|  
|**usage**|**nvarchar (128)**|Indica que la entidad de seguridad participa en la evaluación de los permisos GRANT o DENY o sirve como autenticador.<br /><br /> Este valor puede ser uno de los siguientes:<br /><br /> GRANT o DENY<br /><br /> DENY ONLY<br /><br /> AUTHENTICATOR|  
  
## <a name="see-also"></a>Vea también  
 [sys.login_token &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-login-token-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
