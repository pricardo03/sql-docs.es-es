---
title: Configurar cuentas de inicio de sesión de creación de reflejo de base de datos o grupos de disponibilidad AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], deployment
- logins [SQL Server], database mirroring
ms.assetid: e9f5287b-1325-4cda-88a6-19eaaa52a652
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5fd397349bc3fa3ed7f69e9e1293415ea96fc75d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62754310"
---
# <a name="set-up-login-accounts-for-database-mirroring-or-alwayson-availability-groups-sql-server"></a>Configurar cuentas de inicio de sesión para la creación de reflejo de la base de datos o grupos de disponibilidad de AlwaysOn (SQL Server)
  Para que dos instancias del servidor se conecten a [extremos de creación de reflejo de la base de datos](the-database-mirroring-endpoint-sql-server.md) entre sí, la cuenta de inicio de sesión de cada instancia debe tener acceso a la otra instancia. Además, cada cuenta de inicio de sesión requiere permiso de conexión al extremo de creación de reflejo de la base de datos de la otra instancia.  
  
 El impacto de este requisito depende de si las instancias de servidor se ejecutan como la misma cuenta de usuario de dominio:  
  
-   Si las instancias del servidor se ejecutan como la misma cuenta de usuario de dominio, automáticamente existen los inicios de sesión de usuario correctos en ambas bases de datos **maestras** . Esto simplifica la configuración de seguridad de la creación de reflejo de la base de datos y de los grupos de disponibilidad AlwaysOn.  
  
-   Si las instancias de servidor se ejecutan como cuentas de usuario diferentes, los inicios de sesión de usuario en la instancia de servidor que hospeda el servidor principal o la réplica principal deben reproducirse manualmente en la instancia de servidor que hospeda el servidor reflejado o en cada instancia de servidor que hospeda una réplica secundaria. Para obtener más información, vea [Crear un inicio de sesión para una cuenta diferente](#CreateLogin) y [Conceder el permiso de conexión](#GrantConnect), más adelante en este tema.  
  
    > [!IMPORTANT]  
    >  Para crear un entorno más seguro, considere la posibilidad de usar cuentas de dominio diferentes para cada instancia de servidor.  
  
##  <a name="CreateLogin"></a> Crear un inicio de sesión para una cuenta diferente  
 Si dos instancias del servidor se ejecutan como cuentas diferentes, el administrador del sistema debe utilizar la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE LOGIN para crear un inicio de sesión para la cuenta de servicio de inicio de la instancia remota para cada instancia del servidor. Para obtener más información, vea [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql).  
  
> [!IMPORTANT]  
>  Si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ejecuta con una cuenta que no sea de dominio, es necesario utilizar certificados. Para obtener más información, vea [Usar certificados para un punto de conexión de creación de reflejo de la base de datos &#40;Transact-SQL&#41;](use-certificates-for-a-database-mirroring-endpoint-transact-sql.md).  
  
 Por ejemplo, para que la instancia del servidor sqlA, que se ejecuta con loginA, se conecte a la instancia del servidor sqlB, que se ejecuta con loginB, loginA debe estar en sqlB y loginB debe estar en sqlA. Además, en una sesión de creación de reflejo de la base de datos que incluya una instancia del servidor testigo (sqlC) y en la que las tres instancias del servidor se ejecuten con diferentes cuentas de dominio, deben crearse los siguientes inicios de sesión:  
  
|En la instancia...|Cree inicios de sesión y conceda permiso de conexión para ...|  
|--------------------|--------------------------------------------------------------|  
|sqlA|sqlB y sqlC|  
|sqlB|sqlA y sqlC|  
|sqlC|sqlA y sqlB|  
  
> [!NOTE]  
>  Es posible conectarse a la cuenta de servicio de red mediante la cuenta del equipo en lugar de un usuario de dominio. Si se utiliza la cuenta de equipo, debe agregarse como un usuario en la otra instancia del servidor.  
  
##  <a name="GrantConnect"></a> Conceder el permiso de conexión  
 Una vez creado un inicio de sesión en una instancia del servidor, debe concederse al inicio de sesión permiso para conectarse al extremo de creación de reflejo de la base de datos de la instancia del servidor. El administrador del sistema concede el permiso de conexión mediante una instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] GRANT. Para obtener más información, vea [GRANT &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-transact-sql).  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Crear un inicio de sesión](../../relational-databases/security/authentication-access/create-a-login.md)  
  
-   [Permitir el acceso de red a un punto de conexión de creación de reflejo de la base de datos mediante la autenticación de Windows &#40;SQL Server&#41;](../database-mirroring-allow-network-access-windows-authentication.md).  
  
-   [Usar certificados para un punto de conexión de creación de reflejo de la base de datos &#40;Transact-SQL&#41;](use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
## <a name="see-also"></a>Vea también  
 [El punto de conexión de creación de reflejo de la base de datos &#40;SQL Server&#41;](the-database-mirroring-endpoint-sql-server.md)   
 [Solucionar problemas de configuración de creación de reflejo de la base de datos &#40;SQL Server&#41;](troubleshoot-database-mirroring-configuration-sql-server.md)   
 [Solución de problemas de configuración de grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
  
