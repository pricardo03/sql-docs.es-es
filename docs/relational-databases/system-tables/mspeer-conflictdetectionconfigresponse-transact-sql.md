---
title: MSpeer_conflictdetectionconfigresponse (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpeer_conflictdetectionconfigresponse
- MSpeer_conflictdetectionconfigresponse_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_conflictdetectionconfigureresponse
ms.assetid: 2685fb66-731d-40f7-af4b-596b9222c5d4
author: stevestein
ms.author: sstein
ms.openlocfilehash: 430008b1a689c413bf69c9907a60f4129dc8e5b9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006876"
---
# <a name="mspeerconflictdetectionconfigresponse-transact-sql"></a>MSpeer_conflictdetectionconfigresponse (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Se utiliza en la replicación punto a punto para almacenar la respuesta de cada nodo a una solicitud de configuración de toda la topología. Esta tabla se almacena en la base de datos de publicación.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|request_id|**int**|Identifica una entrada de solicitud de configuración de conflicto en el [MSpeer_conflictdetectionconfigrequest](../../relational-databases/system-tables/mspeer-conflictdetectionconfigrequest-transact-sql.md) tabla.|  
|peer_node|**sysname**|Nombre de la instancia del servidor que generó la respuesta.|  
|peer_db|**sysname**|Base de datos de suscripciones del mismo nivel que generó la respuesta.|  
|peer_version|**sysname**|Identifica el número de versión del publicador.|  
|peer_db_version|**sysname**|Identifica el número de versión de la base de datos del mismo nivel.|  
|is_peer|**bit**|Indica si un nodo es un suscriptor de solo lectura. Un valor de **0** indica un suscriptor de solo lectura.|  
|conflict_detection_enabled|**bit**|Indica si la detección de conflictos está habilitada para la topología.|  
|originator_id|**varbinary (16)**|Identifica cada nodo de la topología para detectar conflictos. Para más información, consulte [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).|  
|peer_conflict_retention|**int**|Período de tiempo, en días, durante el cual los metadatos se almacenan en tablas conflictivas.|  
|peer_subscriptions|**XML**|Información sobre el nodo que respondió a la solicitud.|  
|progress_phase|**nvarchar(32)**|Identifica la fase actual de procesamiento, utilizando uno de los valores siguientes:<br /><br /> Started<br /><br /> Versión del mismo nivel recopilada<br /><br /> Estado recopilado|  
|modified_date|**datetime**|Fecha y hora en que se completó una fase.|  
  
## <a name="see-also"></a>Vea también  
 [Las tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
