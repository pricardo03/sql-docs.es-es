---
title: Servidor y catálogo de Integration Services (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- packages [Integration Services], managing
- managing packages [Integration Services]
ms.assetid: 6d667bba-7c25-492a-8f4d-70ebaca28f40
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 4b0911b650d164e1ae53281b70d6822353b1f2cb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070677"
---
# <a name="integration-services-ssis-server-and-catalog"></a>Servidor y catálogo de Integration Services (SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Después de diseñar y probar paquetes en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], puede implementar los proyectos que contienen los paquetes en el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 El servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] es una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que hospeda la base de datos de **SSISDB** . La base de datos almacena los objetos siguientes: paquetes, proyectos, parámetros, permisos, propiedades del servidor e historial operativo.  
  
 La base de datos de **SSISDB** expone la información de objetos en vistas públicas que puede consultar. La base de datos también proporciona procedimientos almacenados a los que puede llamar para administrar los objetos.  
  
 Para poder implementar los proyectos en el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , debe crear el catálogo de **SSISDB** .  
  
 Para obtener información general de la funcionalidad del catálogo de SSISDB, consulte [SSIS Catalog (Catálogo de SSIS)](../../integration-services/catalog/ssis-catalog.md).  
  
## <a name="high-availability"></a>Alta disponibilidad  
 Como otras bases de datos de usuario, la base de datos de **SSISDB** admite la creación de reflejo de la base de datos y la replicación. Para obtener más información sobre la creación de reflejo y la replicación, consulte [Creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).  
  
 También puede proporcionar alta disponibilidad de SSISDB y de su contenido mediante SSIS y los grupos de disponibilidad Always On. Para más información, vea [Always On para el catálogo de SSIS (SSISDB)](ssis-catalog.md#always-on-for-ssis-catalog-ssisdb). Vea también esta entrada de blog de Matt Masson, [SSIS with Always On](https://go.microsoft.com/fwlink/?LinkId=255873) (SSIS con Always On), en blogs.msdn.com.  
  
##  <a name="ssms"></a> Servidor de Integration Services en SQL Server Management Studio  
 Al conectarse a una instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que hospeda la base de datos de **SSISDB** , ve los objetos siguientes en el Explorador de objetos:  
  
-   **Base de datos SSISDB**  
  
     La base de datos de **SSISDB** aparece en el nodo **Bases de datos** del Explorador de objetos. Puede consultar las vistas y llamar a los procedimientos almacenados que administran el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y los objetos que están almacenados en el servidor.  
  
-   **Catálogos de Integration Services**  
  
     En el nodo **Catálogos de Integration Services** hay carpetas para los proyectos y los entornos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Ver la lista de paquetes en el servidor de Integration Services](../../integration-services/catalog/view-the-list-of-packages-on-the-integration-services-server.md)  
  
-   [Implementar proyectos y paquetes de Integration Services (SSIS)](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)  
  
-   [Ejecutar paquetes de Integration Services (SSIS)](../../integration-services/packages/run-integration-services-ssis-packages.md)  
  
## <a name="related-content"></a>Contenido relacionado  
 Entrada de blog, [SSIS with Always On (SSIS con AlwaysOn)](https://go.microsoft.com/fwlink/?LinkId=255873) en blogs.msdn.com.  
  
  
