---
title: Administrar los paquetes en ejecución mediante programación | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- packages [Integration Services], managing
- running packages [Integration Services]
ms.assetid: 0e91f4ac-6f29-40d7-8c28-9b82e4802c35
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 02fc0b5a135ff54b7545fadd8371f889f44f015b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68028447"
---
# <a name="managing-running-packages-programmatically"></a>Administrar los paquetes en ejecución mediante programación

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Cuando trabaja con paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] mediante programación, puede que desee determinar los paquetes que se están ejecutando en ese momento. La clase <xref:Microsoft.SqlServer.Dts.Runtime.Application> del espacio de nombres <xref:Microsoft.SqlServer.Dts.Runtime> proporciona métodos y clases para satisfacer estos requisitos.  
  
 Para obtener más información sobre la supervisión de paquetes, consulte [Administración de paquetes &#40;servicio SSIS&#41;](../../integration-services/service/package-management-ssis-service.md).  
  
 Todos los métodos descritos en este tema, requieren que se haga una referencia al ensamblado **Microsoft.SqlServer.ManagedDTS**. Después de agregar la referencia en un proyecto nuevo, importe el espacio de nombres <xref:Microsoft.SqlServer.Dts.Runtime> mediante una instrucción **using** o **Imports**.  
  
> [!IMPORTANT]  
>  Los métodos de la clase <xref:Microsoft.SqlServer.Dts.Runtime.Application> para trabajar con el almacén de paquetes SSIS solamente admiten ".", localhost o el nombre del servidor local. No puede utilizar "(local)".  
  
## <a name="determining-which-packages-are-currently-running"></a>Determinar los paquetes que se están ejecutando  
 Para determinar qué paquetes se están ejecutando actualmente en el servidor especificado, llame al método <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetRunningPackages%2A>. Este método devuelve una colección <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackages> de objetos <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage>.  
  
> [!NOTE]  
>  Los administradores ven todos los paquetes que se están ejecutando actualmente en el equipo; el resto de usuarios solamente ve los paquetes que han iniciado ellos mismos.  
  
## <a name="working-with-running-packages"></a>Trabajar con paquetes en ejecución  
 Una vez determinados los paquetes que se están ejecutando actualmente, puede recuperar información sobre los paquetes y solicitar que se detenga un paquete.  
  
### <a name="getting-information-about-a-running-package"></a>Obtener información sobre un paquete en ejecución  
 Al recorrer en iteración la colección <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackages>, puede utilizar las propiedades del objeto <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage> para buscar un paquete u obtener información adicional sobre los paquetes que se están ejecutando:  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.ExecutionDuration%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.ExecutionStartTime%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.InstanceID%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.PackageDescription%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.PackageID%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.PackageName%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.UserName%2A>  
  
### <a name="stopping-a-running-package"></a>Detener un paquete en ejecución  
 Puede llamar al método <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.Stop%2A> de un objeto <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage> para solicitar que se detenga el paquete. Es posible que se produzca un retraso entre el momento en el que se emite una solicitud de detención y el momento en el que realmente se detiene el paquete.  
  
## <a name="see-also"></a>Consulte también  
 [Administración de paquetes &#40;servicio SSIS&#41;](../../integration-services/service/package-management-ssis-service.md)   
 [Enumerar los paquetes disponibles mediante programación](../../integration-services/run-manage-packages-programmatically/enumerating-available-packages-programmatically.md)  
  
  
