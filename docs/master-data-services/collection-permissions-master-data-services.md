---
title: Permisos de colección (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- collections [Master Data Services], permissions
- permissions [Master Data Services], collections
ms.assetid: 703e1bf5-4b4b-4830-8a5b-f979b09f677d
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 7e2e1dbbf51533e03d3e1f5a6930dd0a022cf215
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67941110"
---
# <a name="collection-permissions-master-data-services"></a>Permisos de colección (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Los permisos de colección se aplican a todas las colecciones de una entidad. No puede conceder permisos a una colección específica; los permisos se aplican a todas las colecciones.  
  
> [!NOTE]  
>  Estos permisos solo se aplican al área funcional del **Explorador** de la interfaz de usuario.  
  
|Permiso|Descripción|  
|----------------|-----------------|  
|**Lectura**|El usuario puede leer los miembros de las colecciones y los atributos de los miembros.|  
|**Crear**|El usuario puede crear miembros de colecciones y asignar valores de atributos.|  
|**Update**|El usuario puede actualizar los miembros de las colecciones, así como los atributos y relaciones.|  
|**Eliminar**|El usuario puede eliminar miembros de colecciones.|  
|**Denegar**|Denegar todo el acceso a los miembros de las colecciones.|  
  
 Los permisos de lectura, creación, actualización y eliminación se pueden combinar. Cuando se asignan Crear, Actualizar y Eliminar, el permiso de lectura se asigna automáticamente.  
  
## <a name="see-also"></a>Vea también  
 [Asignar permisos de objeto de modelo &#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)   
 [Colecciones &#40;Master Data Services&#41;](../master-data-services/collections-master-data-services.md)   
 [Permisos de objeto del modelo &#40;Master Data Services&#41;](../master-data-services/model-object-permissions-master-data-services.md)  
  
  
