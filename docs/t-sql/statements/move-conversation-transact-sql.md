---
title: MOVE CONVERSATION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- MOVE_CONVERSATION_TSQL
- MOVE CONVERSATION
- MOVE_TSQL
- MOVE
dev_langs:
- TSQL
helpviewer_keywords:
- moving conversations
- MOVE CONVERSATION statement
- relocating conversations
- conversations [Service Broker], groups
- conversations [Service Broker], moving
ms.assetid: 1da4d2c9-e767-434e-b49b-615711a7f626
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d76dd0507336a110337f01509440d4ad64afc085
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68129435"
---
# <a name="move-conversation-transact-sql"></a>MOVE CONVERSATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Mueve una conversación a otro grupo de conversación diferente.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
MOVE CONVERSATION conversation_handle  
   TO conversation_group_id  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *conversation_handle*  
 Es una variable o una constante que contiene el identificador de conversación de la conversación que se va a mover. *conversation_handle* debe ser de tipo **uniqueidentifier**.  
  
 TO *conversation_group_id*  
 Es una variable o una constante que contiene el identificador del grupo de conversación donde se va a mover la conversación. *conversation_group_id* debe ser de tipo **uniqueidentifier**.  
  
## <a name="remarks"></a>Notas  
 La instrucción MOVE CONVERSATION mueve la conversación especificada por *conversation_handle* al grupo de conversaciones identificado por *conversation_group_id*. Los diálogos solo se pueden redirigir entre grupos de conversación que están asociados a la misma cola.  
  
> [!IMPORTANT]  
>  Si la instrucción MOVE CONVERSATION no es la primera de un lote o un procedimiento almacenado, la instrucción anterior debe terminar en un punto y coma ( **;** ), que es el terminador de instrucciones de [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 La instrucción MOVE CONVERSATION bloquea el grupo de conversaciones asociado con *conversation_handle* y el grupo de conversaciones especificado por *conversation_group_id* hasta que la transacción que contiene la instrucción se confirma o se revierte.  
  
 MOVE CONVERSATION no es válido en una función definida por el usuario.  
  
## <a name="permissions"></a>Permisos  
 Para mover una conversación, el usuario actual debe ser el propietario de la conversación y el grupo de conversación, o miembro del rol fijo de servidor sysadmin o miembro del rol fijo de base de datos db_owner.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se mueve una conversación a otro grupo de conversación.  
  
```  
DECLARE @conversation_handle UNIQUEIDENTIFIER,  
        @conversation_group_id UNIQUEIDENTIFIER ;  
  
SET @conversation_handle =  
    <retrieve conversation handle from database> ;  
SET @conversation_group_id =  
    <retrieve conversation group ID from database> ;  
  
MOVE CONVERSATION @conversation_handle TO @conversation_group_id ;  
```  
  
## <a name="see-also"></a>Consulte también  
 [BEGIN DIALOG CONVERSATION &#40;Transact-SQL&#41;](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)   
 [GET CONVERSATION GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/get-conversation-group-transact-sql.md)   
 [END CONVERSATION &#40;Transact-SQL&#41;](../../t-sql/statements/end-conversation-transact-sql.md)   
 [sys.conversation_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-conversation-groups-transact-sql.md)   
 [sys.conversation_endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-conversation-endpoints-transact-sql.md)  
  
  
