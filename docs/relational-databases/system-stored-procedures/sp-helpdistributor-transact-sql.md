---
title: sp_helpdistributor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpdistributor_TSQL
- sp_helpdistributor
helpviewer_keywords:
- sp_helpdistributor
ms.assetid: 37b0983e-3b69-4f0f-977e-20efce0a0b97
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0681e82f9e36fd2a2f66bb8b7d3faa2f07a72f13
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770939"
---
# <a name="sphelpdistributor-transact-sql"></a>sp_helpdistributor (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Muestra información acerca del distribuidor, la base de datos de distribución, [!INCLUDE[msCoName](../../includes/msconame-md.md)] el directorio de trabajo y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la cuenta de usuario del agente. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicaciones o en cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpdistributor [ [ @distributor= ] 'distributor' OUTPUT ]  
    [ , [ @distribdb= ] 'distribdb' OUTPUT ]  
    [ , [ @directory= ] 'directory' OUTPUT ]  
    [ , [ @account= ] 'account' OUTPUT ]  
    [ , [ @min_distretention= ] min_distretention OUTPUT ]  
    [ , [ @max_distretention= ] max_distretention OUTPUT ]  
    [ , [ @history_retention= ] history_retention OUTPUT ]  
    [ , [ @history_cleanupagent= ] 'history_cleanupagent' OUTPUT ]  
    [ , [ @distrib_cleanupagent = ] 'distrib_cleanupagent' OUTPUT ]  
    [ , [ @publisher = ] 'publisher' ]   
    [ , [ @local = ] 'local' ]  
    [ , [ @rpcsrvname= ] 'rpcsrvname' OUTPUT ]  
    [ , [ @publisher_type = ] 'publisher_type' OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @distributor = ] 'distributor' OUTPUT`Es el nombre del distribuidor. Distributor es de **tipo sysname y su**valor **%** predeterminado es, que es el único valor que devuelve un conjunto de resultados.  
  
`[ @distribdb = ] 'distribdb' OUTPUT`Es el nombre de la base de datos de distribución. *distribdb* es de **tipo sysname y su**valor **%** predeterminado es, que es el único valor que devuelve un conjunto de resultados.  
  
`[ @directory = ] 'directory' OUTPUT`Es el directorio de trabajo. el *directorio* es de tipo **nvarchar (255)** y su **%** valor predeterminado es, que es el único valor que devuelve un conjunto de resultados.  
  
`[ @account = ] 'account' OUTPUT`Es la [!INCLUDE[msCoName](../../includes/msconame-md.md)] cuenta de usuario de Windows. *account*es de tipo **nvarchar (255)** y su valor **%** predeterminado es, que es el único valor que devuelve un conjunto de resultados.  
  
`[ @min_distretention = ] _min_distretentionOUTPUT`Es el período mínimo de retención de la distribución, en horas. *min_distretention* es de **tipo int**y su valor predeterminado es **-1**.  
  
`[ @max_distretention = ] _max_distretentionOUTPUT`Es el período máximo de retención de distribución, en horas. *max_distretention* es de **tipo int**y su valor predeterminado es **-1**.  
  
`[ @history_retention = ] _history_retentionOUTPUT`Es el período de retención del historial, en horas. *history_retention* es de **tipo int**y su valor predeterminado es **-1**.  
  
`[ @history_cleanupagent = ] 'history_cleanupagent' OUTPUT`Es el nombre del agente de limpieza del historial. *history_cleanupagent* es de tipo **nvarchar (100)** y su valor **%** predeterminado es, que es el único valor que devuelve un conjunto de resultados.  
  
`[ @distrib_cleanupagent = ] 'distrib_cleanupagent' OUTPUT`Es el nombre del agente de limpieza de distribución. *distrib_cleanupagent* es de tipo **nvarchar (100)** y su valor **%** predeterminado es, que es el único valor que devuelve un conjunto de resultados.  
  
`[ @publisher = ] 'publisher'`Es el nombre del publicador. *Publisher* es de **tipo sysname y su**valor predeterminado es NULL.  
  
`[ @local = ] 'local'`Indica si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe obtener valores del servidor local. *local* es de tipo **nvarchar (5)** y su valor predeterminado es NULL.  
  
`[ @rpcsrvname = ] 'rpcsrvname' OUTPUT`Es el nombre del servidor que emite llamadas a procedimientos remotos. *rpcsrvname* es de **tipo sysname y su**valor **%** predeterminado es, que es el único valor que devuelve un conjunto de resultados.  
  
`[ @publisher_type = ] 'publisher_type' OUTPUT`Es el tipo de publicador del publicador. *publisher_type* es de **tipo sysname y su**valor **%** predeterminado es, que es el único valor que devuelve un conjunto de resultados.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**distributor**|**sysname**|Nombre del distribuidor.|  
|**base de datos de distribución**|**sysname**|Nombre de la base de datos de distribución.|  
|**directory**|**nvarchar(255)**|Nombre del directorio de trabajo.|  
|**account**|**nvarchar(255)**|Nombre de la cuenta de usuario de Windows.|  
|**retención mínima de distrib.**|**int**|Período mínimo de retención de la distribución.|  
|**retención máxima de distrib.**|**int**|Período máximo de retención de la distribución.|  
|**retención del historial**|**int**|Período de retención del historial.|  
|**agente de limpieza del historial**|**nvarchar(100)**|Nombre del Agente de limpieza del historial.|  
|**agente de limpieza de distribución**|**nvarchar(100)**|Nombre del Agente de limpieza de distribución.|  
|**nombre del servidor RPC**|**sysname**|Nombre del distribuidor remoto o local.|  
|**nombre de inicio de sesión RPC**|**sysname**|Inicio de sesión utilizado por las llamadas a procedimientos remotos al distribuidor remoto.|  
|**tipo de publicador**|**sysname**|Tipo de publicador; puede ser uno de los siguientes:<br /><br /> **MSSQLSERVER**<br /><br /> **ORACLE**<br /><br /> **PUERTA DE ENLACE DE ORACLE**|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_helpdistributor** se utiliza en todos los tipos de replicación.  
  
 Si se especifican uno o más parámetros OUTPUT al ejecutar **sp_helpdistributor**, todos los parámetros de salida establecidos en NULL se asignan a los valores de Exit y no se devuelve ningún conjunto de resultados. Si no se especifica ningún parámetro de salida, se devuelve un conjunto de resultados.  
  
## <a name="permissions"></a>Permisos  
 Las siguientes columnas del conjunto de resultados o parámetros de salida se devuelven a los miembros del rol fijo de servidor **sysadmin** en el publicador y el rol fijo de base de datos **db_owner** en la base de datos de publicación:  
  
|Columna del conjunto de resultados|Parámetro de salida|  
|-----------------------|----------------------|  
|account|**@account**|  
|min distrib retention|**@min_distretention**|  
|max distrib retention|**@max_distretention**|  
|history retention|**@history_retention**|  
|history cleanup agent|**@history_cleanupagent**|  
|distribution cleanup agent|**@distrib_cleanupagent**|  
|rpc login name|none|  
  
 La siguiente columna de conjuntos de resultados se devuelve a los usuarios de la lista de acceso a la publicación para una publicación en el distribuidor:  
  
-   directory  
  
 Las siguientes columnas de conjuntos de resultados se devuelven a todos los usuarios.  
  
|Columna del conjunto de resultados|Parámetro de salida|  
|-----------------------|----------------------|  
|distributor|**@distributor**|  
|base de datos de distribución|**@distribdb**|  
|rpc server name|**@rpcsrvname**|  
|publisher type|**@publisher_type**|  
  
## <a name="see-also"></a>Vea también  
 [Ver y modificar las propiedades del distribuidor y del publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_dropdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)  
  
  
