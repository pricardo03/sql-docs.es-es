---
title: Administrar roles de paquete mediante programación (servicio SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Integration Services packages, roles
- roles [Integration Services]
- packages [Integration Services], roles
ms.assetid: 2e0ca0d5-d4f5-421d-b17d-a48b37b923e5
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 5833ff25bc698b94e1798aa77e3fc776d5955a1c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68028516"
---
# <a name="managing-package-roles-programmatically-ssis-service"></a>Administrar roles de paquete mediante programación (servicio SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Cuando trabaja mediante programación con paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], puede determinar qué roles están disponibles para aplicar a los paquetes o bien determinar o establecer los roles que se aplican a un paquete individual. La clase <xref:Microsoft.SqlServer.Dts.Runtime.Application> del espacio de nombres <xref:Microsoft.SqlServer.Dts.Runtime> proporciona diferentes métodos para satisfacer estos requisitos.  
  
 Los roles se aplican solo a paquetes almacenados en la base de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **msdb**. Para obtener más información acerca de los roles de paquete, consulte [Integration Services Roles &#40;SSIS Service&#41; (Roles de Integration Services &#40;servicio SSIS&#41;)](../../integration-services/security/integration-services-roles-ssis-service.md).  
  
 Todos los métodos descritos en este tema requieren que se haga una referencia al ensamblado **Microsoft.SqlServer.ManagedDTS**. Después de agregar la referencia en un proyecto nuevo, importe el espacio de nombres <xref:Microsoft.SqlServer.Dts.Runtime> mediante una instrucción **using** o **Imports**.  
  
> [!IMPORTANT]  
>  Los métodos de la clase <xref:Microsoft.SqlServer.Dts.Runtime.Application> para trabajar con el almacén de paquetes SSIS solamente admiten ".", localhost o el nombre del servidor local. No puede utilizar "(local)".  
  
## <a name="determining-which-roles-are-available"></a>Determinar los roles disponibles  
 Para determinar qué roles están disponibles para los paquetes almacenados en un servidor determinado, llame al método <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetDtsServerRoles%2A> de la clase <xref:Microsoft.SqlServer.Dts.Runtime.Application>.  
  
## <a name="determining-which-roles-are-assigned"></a>Determinar los roles asignados  
 Para determinar qué roles se han asignado ya a un paquete determinado, llame al método <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetPackageRoles%2A>. Para asignar roles a un paquete, llame al método <xref:Microsoft.SqlServer.Dts.Runtime.Application.SetPackageRoles%2A>.  
  
## <a name="see-also"></a>Consulte también  
 [Roles de Integration Services &#40;servicio SSIS&#41;](../../integration-services/security/integration-services-roles-ssis-service.md)  
  
  
