---
title: syscollector_collection_items (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syscollector_collection_items_TSQL
- syscollector_collection_items
dev_langs:
- TSQL
helpviewer_keywords:
- syscollector_collection_items view
- add data collector view
ms.assetid: a279ecd1-a59c-4315-9f08-bf221f00a465
author: stevestein
ms.author: sstein
ms.openlocfilehash: 78e8211c10d019c3b2a8c2435c5ddde8f8182a14
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68060410"
---
# <a name="syscollectorcollectionitems-transact-sql"></a>syscollector_collection_items (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información sobre un elemento en un conjunto de recopilación.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**collection_set_id**|**int**|Identifica el conjunto de recopilación. No admite valores NULL.|  
|**collection_item_id**|**int**|Identifica un elemento en el conjunto de recopilación. No admite valores NULL.|  
|**collector_type_uid**|**uniqueidentifier**|GUID utilizado para identificar el tipo de recopilador. No admite valores NULL.|  
|**name**|**nvarchar(4000)**|Nombre del conjunto de recopilación. Acepta valores NULL.|  
|**Frecuencia**|**int**|Frecuencia con que un elemento de recopilación recopila datos. No admite valores NULL.|  
|**parameters**|**xml**|Describe la parametrización para el tipo de recopilador asociado al elemento de recopilación. El esquema XML para este elemento de recopilación se valida con los esquemas XML (XSD) almacenado en el **parameter_schema** para un tipo de recopilador determinado. Acepta valores NULL. Para obtener más información, consulte [syscollector_collector_types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collector-types-transact-sql.md).|  
  
## <a name="permissions"></a>Permisos  
 Requiere SELECT para **dc_operator**, **dc_proxy**.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del recopilador de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Vistas del recopilador de datos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [Recopilación de datos](../../relational-databases/data-collection/data-collection.md)  
  
  
