---
title: sys.syscurconfigs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.syscurconfigs
- sys.syscurconfigs_TSQL
- syscurconfigs
- syscurconfigs_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.syscurconfigs compatibility view
- syscurconfigs system table
ms.assetid: 454ab849-07a5-4b50-ba0a-6b1b14721f77
author: rothja
ms.author: jroth
ms.openlocfilehash: 1b0fad344831d8073badb2618eb2c34a1cdc2161
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68089179"
---
# <a name="syssyscurconfigs-transact-sql"></a>sys.syscurconfigs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una entrada por cada opción de configuración actual. Además, esta vista contiene cuatro entradas que describen la estructura de configuración. **syscurconfigs** se genera dinámicamente cuando un usuario realiza una consulta. Para obtener más información, consulte [sys.sysconfigures &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysconfigures-transact-sql.md).  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**value**|**int**|Valor de la variable, que el usuario puede modificar. [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] lo utiliza solo si se ha ejecutado RECONFIGURE.|  
|**config**|**smallint**|Número de la variable de configuración.|  
|**comment**|**nvarchar(255)**|Explicación de la opción de configuración.|  
|**status**|**smallint**|Mapa de bits que indica el estado de la opción. Entre los valores posibles figuran los siguientes:<br /><br /> 0 = Estático. Configuración surte efecto cuando se reinicia el servidor.<br /><br /> 1 = Dinámico. La variable surte efecto cuando se ejecuta la instrucción RECONFIGURE.<br /><br /> 2 = Avanzado. Se muestra la variable solo cuando el **Mostrar opciones avanzadas** está establecido.<br /><br /> 3 = Dinámico y avanzado.|  
  
## <a name="see-also"></a>Vea también  
 [Asignar tablas del sistema a vistas del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Vistas de compatibilidad &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
