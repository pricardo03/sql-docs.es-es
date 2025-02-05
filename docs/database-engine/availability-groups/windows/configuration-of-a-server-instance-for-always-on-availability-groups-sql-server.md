---
title: Habilitación de la característica de grupo de disponibilidad para una instancia de SQL Server
description: Se describe cómo habilitar la característica de grupo de disponibilidad Always On para una instancia de SQL Server.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], server instance
- Availability Groups [SQL Server], about
ms.assetid: fad8db32-593e-49d5-989c-39eb8399c416
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 94f3a9b92e05983ff9e2a10473a171069acf9a77
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67988556"
---
# <a name="enable-the-always-on-availability-group-feature-for-a-sql-server-instance"></a>Habilitación de la característica de grupo de disponibilidad Always On para una instancia de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tema contiene información sobre los requisitos para configurar una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para que se admita [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
> [!IMPORTANT]  
>  Para obtener información esencial sobre los requisitos previos y las restricciones de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] para los nodos de clústeres de conmutación por error de Windows Server (WSFC) y para las instancias de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], vea [Requisitos previos, restricciones y recomendaciones para Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
   
##  <a name="TermsAndDefinitions"></a> Términos y definiciones  
 [Grupos de disponibilidad AlwaysOn](../../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
 Una solución de alta disponibilidad y de recuperación ante desastres que proporciona una alternativa en el nivel de empresa a la creación de reflejo de la base de datos. Un *grupo de disponibilidad* admite un entorno de conmutación por error para un conjunto discreto de bases de datos de usuario, conocido como *bases de datos de disponibilidad*, que realizan la conmutación por error conjuntamente.  
  
 réplica de disponibilidad  
 Una instancia de un grupo de disponibilidad hospedado en una instancia específica de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y que mantiene una copia local de cada base de datos de disponibilidad perteneciente al grupo de disponibilidad. Existen dos tipos de réplicas de disponibilidad: una sola *réplica principal* y de una a cuatro *réplicas secundarias*. Las instancias de servidor que hospedan las réplicas de disponibilidad para un grupo de disponibilidad dado deben residir en nodos diferentes de un único clúster de clústeres de conmutación por error (WSFC).  
  
 [extremo de creación de reflejo de la base de datos](../../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)  
 Un extremo es un objeto de SQL Server que permite la comunicación de SQL Server en la red. Para participar en la creación de reflejo de la base de datos y/o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] , una instancia del servidor requiere un extremo dedicado especial. Todas las conexiones de grupo de disponibilidad y creación de reflejo en una instancia de servidor utilizan el mismo extremo de creación de reflejo de la base de datos. Se trata de un extremo especial que se utiliza exclusivamente para recibir estas conexiones procedentes de otras instancias de servidor.  
  
##  <a name="ConfigSI"></a> Para configurar una instancia del servidor para admitir grupos de disponibilidad AlwaysOn  
 Para admitir [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], una instancia de servidor debe residir en un nodo del clúster de conmutación por error de WSFC que hospeda el grupo de disponibilidad, estar habilitada para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] y poseer un extremo de creación de reflejo de la base de datos.  
  
1.  Habilite la característica de grupos de disponibilidad de AlwaysOn en cada instancia del servidor que vaya a participar en uno o varios grupos de disponibilidad. Una instancia del servidor determinada solo puede hospedar una única réplica de disponibilidad para un grupo de disponibilidad dado.  
  
2.  Asegúrese de que la instancia del servidor posee un extremo de creación de reflejo de la base de datos.  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
 **Para habilitar los grupos de disponibilidad de AlwaysOn**  
  
-   [Habilitar y deshabilitar grupos de disponibilidad de AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)  
  
 **Para determinar si existe un extremo de creación de reflejo de la base de datos**  
  
-   [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)  
  
 **Para crear un extremo de creación de reflejo de la base de datos**  
  
-   [Crear un punto de conexión de creación de reflejo de la base de datos para grupos de disponibilidad AlwaysOn &#40;SQL Server PowerShell&#41;](../../../database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell.md)  
  
-   [Crear un punto de conexión de creación de reflejo de la base de datos para la autenticación de Windows &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [Permitir que un punto de conexión de creación de reflejo de la base de datos use certificados para las conexiones salientes &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
##  <a name="RelatedContent"></a> Contenido relacionado  
  
-   **Blogs:**  
  
     [Always On - HADRON Learning Series: Worker Pool Usage for HADRON Enabled Databases](https://blogs.msdn.com/b/psssql/archive/2012/05/17/Always%20On-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx) (Series de aprendizaje de Always ON - HADRON: uso del grupo de trabajo para las bases de datos compatibles con HADRON)  
  
     [Blogs del equipo de Always On de SQL Server: el blog oficial del equipo de Always On de SQL Server](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
     [Blogs de los ingenieros de SQL Server de CSS](https://blogs.msdn.com/b/psssql/)  
  
-   **Vídeos:**  
  
     [Microsoft SQL Server Code-Named "Denali", Serie Always On, parte 1: Introducción a la solución de alta disponibilidad de próxima generación](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server Code-Named "Denali", Serie Always On, parte 2: Creación de una solución crítica de alta disponibilidad mediante Always On](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **Notas del producto:**  
  
     [Guía de soluciones AlwaysOn de Microsoft SQL Server para lograr alta disponibilidad y recuperación ante desastres](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [Notas del producto de Microsoft para SQL Server 2012](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [Notas del producto del equipo de asesoramiento al cliente de SQL Server](https://techcommunity.microsoft.com/t5/DataCAT/bg-p/DataCAT/)  
  
## <a name="see-also"></a>Consulte también  
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Requisitos previos, restricciones y recomendaciones para Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)   
 [El punto de conexión de creación de reflejo de la base de datos &#40;SQL Server&#41;](../../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [Grupos de disponibilidad Always On: Interoperabilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-availability-groups-interoperability-sql-server.md)   
 [Clústeres de conmutación por error y grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [Clústeres de conmutación por error de Windows Server &#40;WSFC&#41; con SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)   
 [Instancias de clúster de conmutación por error de AlwaysOn &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)  
  
  
