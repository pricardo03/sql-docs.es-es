---
title: sp_syscollector_set_cache_window (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_set_cache_window
- sp_syscollector_set_cache_window_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_set_cache_window stored procedure
- data collector [SQL Server], stored procedures
ms.assetid: 660f2749-392f-46bf-89f3-27764d848507
author: stevestein
ms.author: sstein
ms.openlocfilehash: 80462381e058c4cb9107aa4ac07138e42d27e677
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68010633"
---
# <a name="spsyscollectorsetcachewindow-transact-sql"></a>sp_syscollector_set_cache_window (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Establece el número de veces que se va a intentar la carga de los datos en caso de error. Al reintentar una carga en caso de error, disminuye el riesgo de perder los datos recopilados.  

  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_syscollector_set_cache_window [ @cache_window = ] cache_window   
```  
  
## <a name="arguments"></a>Argumentos  
 [ @cache_window =] *cache_window*  
 Es el número de veces que se va a reintentar una carga de datos al almacén de administración de datos en caso de error sin perder datos. *cache_window* es **int** con un valor predeterminado de 1. *cache_window* puede tener uno de los siguientes valores:  
  
|Valor|Descripción|  
|-----------|-----------------|  
|-1|Almacenar en memoria caché todos los datos de carga provenientes de los errores de carga anteriores.|  
|0|No almacenar en memoria caché ningún dato proveniente de un error de carga.|  
|*n*|Almacenar en caché datos de errores de carga anteriores, donde *n* > = 1.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 Debe deshabilitar el recopilador de datos antes de cambiar la configuración de la ventana de la caché. Se produce un error en este procedimiento almacenado si se habilita el recopilador de datos. Para obtener más información, consulte [habilitar o deshabilitar la recopilación de datos](../../relational-databases/data-collection/enable-or-disable-data-collection.md), y [administrar la recopilación de datos](../../relational-databases/data-collection/manage-data-collection.md).  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol fijo de base de datos dc_admin (con permiso EXECUTE) para ejecutar este procedimiento.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se deshabilita el recopilador de datos, se configura la ventana de la caché para retener los datos hasta que se produzcan tres errores en las cargas y, a continuación, se habilita el recopilador de datos.  
  
```sql  
USE msdb;  
GO  
EXECUTE dbo.sp_syscollector_disable_collector;  
GO  
EXECUTE dbo.sp_syscollector_set_cache_window 3;  
GO  
EXECUTE dbo.sp_syscollector_enable_collector;  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_syscollector_set_cache_directory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-cache-directory-transact-sql.md)  
  
  
