---
title: sp_check_subset_filter (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_check_TSQL
- sp_check_subset_filter
- filter
- subset
- subset_TSQL
- sp_check
- sp_check_subset_filter_TSQL
helpviewer_keywords:
- sp_check_subset_filter
ms.assetid: 525cfcfc-f317-478d-ba84-72e62285f160
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3c1510260a5b381b91a399984121834ca4ce30b5
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771315"
---
# <a name="spchecksubsetfilter-transact-sql"></a>sp_check_subset_filter (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Se utiliza para comprobar una cláusula de filtro en una tabla para determinar si es válida para esa tabla. Este procedimiento almacenado devuelve información sobre el filtro suministrado, incluso si el filtro es apto para su uso con particiones precalculadas. Este procedimiento almacenado se ejecuta en el publicador de la base de datos que contiene la publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_check_subset_filter [ @filtered_table = ] 'filtered_table'  
        , [ @subset_filterclause = ] 'subset_filterclause'  
    [ , [ @has_dynamic_filters = ] has_dynamic_filters OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @filtered_table = ] 'filtered_table'`Es el nombre de una tabla filtrada. *filtered_table* es de tipo **nvarchar (400)** y no tiene ningún valor predeterminado.  
  
`[ @subset_filterclause = ] 'subset_filterclause'`Es la cláusula de filtro que se está probando. *subset_filterclause* es de tipo **nvarchar (1000)** y no tiene ningún valor predeterminado.  
  
`[ @has_dynamic_filters = ] has_dynamic_filters`Es si la cláusula de filtro es un filtro de fila con parámetros. *has_dynamic_filters* es de **bit**, su valor predeterminado es NULL y es un parámetro de salida. Devuelve un valor de **1** cuando la cláusula de filtro es un filtro de fila con parámetros.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**can_use_partition_groups**|**bit**|Es si la publicación es apta para usar particiones precalculadas; donde **1** significa que se pueden usar las particiones precalculadas, y **0** significa que no se pueden usar.|  
|**has_dynamic_filters**|**bit**|Indica si la cláusula de filtro proporcionada incluye al menos un filtro de fila con parámetros; donde **1** significa que se utiliza un filtro de fila con parámetros y **0** significa que no se utiliza dicha función.|  
|**dynamic_filters_function_list**|**nvarchar(500)**|Lista de las funciones de la cláusula de filtro que filtran un artículo dinámicamente; las funciones están separadas por puntos y comas.|  
|**uses_host_name**|**bit**|Si se usa la función [host_name ()](../../t-sql/functions/host-name-transact-sql.md) en la cláusula de filtro, donde **1** significa que esta función está presente.|  
|**uses_suser_sname**|**bit**|Si se usa la función [SUSER_SNAME ()](../../t-sql/functions/suser-sname-transact-sql.md) en la cláusula de filtro, donde **1** significa que esta función está presente.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_check_subset_filter** se utiliza en la replicación de mezcla.  
  
 **sp_check_subset_filter** se puede ejecutar en cualquier tabla, incluso si la tabla no está publicada. Este procedimiento almacenado se puede utilizar para comprobar una cláusula de filtro antes de definir un artículo filtrado.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** o del rol fijo de base de datos **db_owner** pueden ejecutar **sp_check_subset_filter**.  
  
## <a name="see-also"></a>Vea también  
 [Optimizar el rendimiento de los filtros con parámetros con particiones calculadas previamente](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)  
  
  
