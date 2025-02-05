---
title: sp_helptracertokens (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helptracertokens
- sp_helptracertokens_TSQL
helpviewer_keywords:
- sp_helptracertokens
ms.assetid: 61f27234-531d-4b37-8fa3-fe4c32e6f521
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9b4df50d1cf43ba1b0f4eb8b8f313634b4d11d18
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771536"
---
# <a name="sphelptracertokens-transact-sql"></a>sp_helptracertokens (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Devuelve una fila para cada testigo de seguimiento que se ha insertado en una publicación para determinar la latencia. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación o en el distribuidor de la base de datos de distribución.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helptracertokens [ @publication = ] 'publication'   
    [ , [ @publisher = ] 'publisher' ]   
    [ , [ @publisher_db = ] 'publisher_db' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`Es el nombre de la publicación en la que se insertaron los testigos de seguimiento. *Publication* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @publisher = ] 'publisher'`Nombre del publicador. *Publisher* es de **tipo sysname y su**valor predeterminado es NULL.  
  
> [!NOTE]
>  Este parámetro solo debe especificarse para los publicadores que no sean de [!INCLUDE[msCoName](../../includes/msconame-md.md)]. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
`[ @publisher_db = ] 'publisher_db'`Nombre de la base de datos de publicación. *publisher_db* es de **tipo sysname y su**valor predeterminado es NULL. Si el procedimiento almacenado se ejecuta en el publicador, se omite este parámetro.  
  
## <a name="result-set"></a>Tipo de cursor  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**tracer_id**|**int**|Identifica un registro de un token de seguimiento.|  
|**publisher_commit**|**datetime**|Fecha y hora a la que el registro de token se confirmó en el publicador de la base de datos de publicaciones.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_helptracertokens** se utiliza en la replicación transaccional.  
  
 **sp_helptracertokens** se usa para obtener los identificadores de token de seguimiento al ejecutar [ &#40;sp_helptracertokenhistory&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md).  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_tracertokens](../../relational-databases/replication/codesnippet/tsql/sp-helptracertokens-tran_1.sql)]  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** , del rol fijo de base de datos **db_owner** en la base de datos de publicación o de los roles fijos de base de datos **db_owner** o **replmonitor** de la base de datos de distribución pueden ejecutar **SP _ helptracertokenhistory**.  
  
## <a name="see-also"></a>Vea también  
 [Medir la latencia y validar las conexiones de la replicación transaccional](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)   
 [sp_deletetracertokenhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-deletetracertokenhistory-transact-sql.md)  
  
  
