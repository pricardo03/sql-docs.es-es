---
title: Cómo se determinan los permisos (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- permissions [Master Data Services], determining permissions
ms.assetid: 1dc0b43a-d023-4e7d-b027-8b1459fd058c
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 2f92a270bb599c84f5d0b2bd85e713c3f406f81b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65479530"
---
# <a name="how-permissions-are-determined-master-data-services"></a>Cómo se determinan los permisos (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], la manera más sencilla de configurar la seguridad es asignar permisos del objeto de modelo a un grupo al que pertenece el usuario.  
  
 La seguridad se hace más compleja cuando:  
  
-   Se asignan permisos del objeto de modelo y permisos de los miembros de una jerarquía.  
  
-   El usuario pertenece a grupos y el permiso se asigna al usuario y los grupos.  
  
-   El usuario pertenece a grupos y el permiso se asigna a varios grupos.  
  
## <a name="permissions-assigned-to-a-single-group-or-user"></a>Permisos asignados a un solo grupo o usuario  
 Si asigna permisos a un solo grupo o usuario, los permisos se determinan en función del siguiente flujo de trabajo.  
  
 ![mds_conc_security_no_overlap](../../2014/master-data-services/media/mds-conc-security-no-overlap.gif "mds_conc_security_no_overlap")  
  
### <a name="step-1-effective-attribute-permissions-are-determined"></a>Paso 1: Se determinan los permisos de atributo efectivos.  
 En la siguiente lista se describe cómo se determinan los permisos de atributo efectivos:  
  
-   Los permisos asignados a objetos de modelo determinan a qué atributos puede tener acceso un usuario.  
  
-   Todos los objetos de modelo heredan automáticamente el permiso del objeto más cercano en un nivel superior de la estructura del modelo.  
  
-   Todos los objetos del mismo nivel que la entidad se deniegan implícitamente.  
  
-   Todos los objetos de un nivel superior reciben acceso de navegación. Para obtener más información sobre el acceso de navegación, consulte [acceso por navegación &#40;Master Data Services&#41;](navigational-access-master-data-services.md).  
  
 En este ejemplo, **de sólo lectura** permiso se asigna a una entidad y su atributo, que se encuentra en un nivel inferior de la estructura del modelo heredan ese permiso. El modelo proporciona acceso de navegación a esta entidad y su atributo. La otra entidad del modelo no tiene ningún permiso explícito asignado y no hereda ningún permiso, de modo que se deniega implícitamente.  
  
 ![mds_conc_inheritance_model](../../2014/master-data-services/media/mds-conc-inheritance-model.gif "mds_conc_inheritance_model")  
  
### <a name="step-2-if-hierarchy-member-permissions-are-assigned-effective-member-permissions-are-determined"></a>Paso 2: Si se asignan los permisos de los miembros de una jerarquía, se determinan los permisos de miembros efectivos.  
 En la siguiente lista se describe cómo se determinan los permisos de los miembros de una jerarquía efectivos:  
  
-   Los permisos asignados a los nodos de la jerarquía determinan a qué miembros puede tener acceso un usuario.  
  
-   Todos los nodos de una jerarquía heredan automáticamente el permiso del objeto más cercano en un nivel superior en la estructura de la jerarquía.  
  
-   Todos los nodos del mismo nivel se deniegan implícitamente.  
  
-   Todos los nodos de niveles superiores a los que no se asignan los permisos se deniegan implícitamente.  
  
 En este ejemplo, **de sólo lectura** permiso se asigna a un nodo de la jerarquía y un nodo en un nivel inferior de la estructura de jerarquía heredan ese permiso. La raíz no tiene ningún permiso asignado, de modo que se deniega implícitamente. El otro nodo de la estructura de la jerarquía no tiene ningún permiso explícito asignado y no hereda ningún permiso, de modo que se deniega implícitamente.  
  
 ![mds_conc_inheritance_hierarchy](../../2014/master-data-services/media/mds-conc-inheritance-hierarchy.gif "mds_conc_inheritance_hierarchy")  
  
### <a name="step-3-the-intersection-of-attribute-and-member-permissions-is-determined"></a>Paso 3: Se determina la intersección de los permisos de atributo y de miembro.  
 Si los permisos de atributo efectivos son diferentes que los permisos de miembro efectivos, los permisos se deben determinar para cada valor de atributo individual. Para obtener más información, consulte [Superponer permisos de modelo y de miembro &#40;Master Data Services&#41;](../../2014/master-data-services/overlapping-model-and-member-permissions-master-data-services.md).  
  
## <a name="permissions-assigned-to-multiple-groups"></a>Permisos asignados a varios grupos  
 Si un usuario pertenece a uno o más grupos y se asignan permisos al usuario y a los grupos, el flujo de trabajo se vuelve más complejo.  
  
 ![mds_conc_security_group_overlap](../../2014/master-data-services/media/mds-conc-security-group-overlap.gif "mds_conc_security_group_overlap")  
  
 En este caso, los permisos de usuario y de grupo que se superpongan se deben resolver para poder comparar los permisos del objeto de modelo y del miembro de jerarquía. Para obtener más información, consulte [Superponer permisos de usuario y de grupo &#40;Master Data Services&#41;](../../2014/master-data-services/overlapping-user-and-group-permissions-master-data-services.md).  
  
## <a name="see-also"></a>Vea también  
 [Superponer permisos de usuario y de grupo &#40;Master Data Services&#41;](../../2014/master-data-services/overlapping-user-and-group-permissions-master-data-services.md)   
 [Superponer permisos de modelo y de miembro &#40;Master Data Services&#41;](../../2014/master-data-services/overlapping-model-and-member-permissions-master-data-services.md)  
  
  
