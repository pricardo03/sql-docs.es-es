---
title: Suspender una base de datos de disponibilidad (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygroup.suspenddatamove.f1
helpviewer_keywords:
- secondary databases [SQL Server], in availability group
- primary databases [SQL Server], in availability group
- Availability Groups [SQL Server], suspending a database
- Availability Groups [SQL Server], databases
ms.assetid: 86858982-6af1-4e80-9a93-87451f0d7ee9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5853ef42066eca006bfc5b7229f7bd7900a8fb6d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62814028"
---
# <a name="suspend-an-availability-database-sql-server"></a>Suspender una base de datos de disponibilidad (SQL Server)
  Puede suspender una base de datos de disponibilidad en [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]o PowerShell en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Observe que un comando de suspender tiene que emitirse en la instancia de servidor que hospeda la base de datos que se va a suspender o a reanudar.  
  
 El efecto de un comando de suspensión depende de si suspende una base de datos secundaria o una base de datos principal, según se indica a continuación:  
  
|Base de datos suspendida|Efecto del comando de suspensión|  
|------------------------|-------------------------------|  
|Base de datos secundaria|Solo la base de datos secundaria local se suspende y su estado de sincronización se pasa a NOT SYNCHRONIZED. Otras bases de datos secundarias no se ven afectadas. La base de datos suspendida deja de recibir y aplicar datos (registros) y comienza a quedar rezagada respecto de la principal base de datos principal. Las conexiones existentes en la secundaria legible siguen estando utilizables. Las nuevas conexiones a la base de datos suspendida en la secundaria legible no se permiten hasta que se reanude el movimiento de datos.<br /><br /> La base de datos principal sigue estando disponible. Si suspende cada una de las bases de datos secundarias correspondientes, la base de datos principal se queda expuesta.<br /><br /> **\*\* Importante \*\*** Mientras se suspende una base de datos secundaria, la cola de envío de la base de datos principal correspondiente acumulará registros de transacciones sin enviar. Las conexiones a la réplica secundaria devuelven los datos que estaban disponibles en el momento en que suspendió el movimiento de datos.|  
|Base de datos principal|La base de datos principal detiene el movimiento de datos a cada base de datos secundaria conectada. La base de datos principal continúa ejecutándose en un modo expuesto. La base de datos principal sigue disponible para los clientes y las conexiones existentes en una base de datos secundaria legible permanecen utilizables y se pueden establecer nuevas conexiones.|  
  
> [!NOTE]  
>  Suspender una base de datos secundaria de AlwaysOn no afecta directamente a la disponibilidad de la base de datos principal. Sin embargo, suspender una base de datos secundaria puede afectar a las capacidades de la redundancia y de conmutación por error para la base de datos principal. Esto se diferencia del reflejo de base de datos, en el que el estado de reflejo se suspende tanto en la base de datos reflejada como en la base de datos principal. Al suspender una base de datos principal AlwaysOn, se suspende el movimiento de datos en todas las bases de datos secundarias y las capacidades de conmutación por error y redundancia cesan para esa base de datos hasta que la base de datos principal se reanuda.  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Requisitos previos](#Prerequisites)  
  
     [Recomendaciones](#Recommendations)  
  
     [Seguridad](#Security)  
  
-   **Para suspender una base de datos con:**  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   **Sigue:** [Evitar un registro de transacciones lleno](#FollowUp)  
  
-   [Tareas relacionadas](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
 Un comando SUSPEND realiza la devolución en cuanto haya sido aceptado por la réplica que hospeda la base de datos de destino, pero la suspensión real de la base de datos se produce de forma asincrónica.  
  
###  <a name="Prerequisites"></a> Requisitos previos  
 Debe estar conectado a la instancia de servidor que hospeda la base de datos que desea suspender. Para suspender una base de datos principal y las bases de datos secundarias correspondientes, conéctese a la instancia del servidor que hospeda la réplica principal. Para suspender una base de datos secundaria dejando disponible la base de datos principal, conéctese a la réplica secundaria.  
  
###  <a name="Recommendations"></a> Recomendaciones  
 Durante los cuellos de botella, la suspensión breve de una o varias bases de datos secundarias puede ser útil para mejorar temporalmente el rendimiento de la réplica principal. Mientras una base de datos secundaria permanece suspendida, el registro de transacciones de la base de datos principal correspondiente no puede truncarse. Esto hace que las entradas de registro se acumulen en la base de datos principal. Por tanto, se recomienda reanudar o quitar rápidamente una base de datos secundaria suspendida. Para obtener más información, consulte [seguimiento: Evitar un registro de transacciones lleno](#FollowUp), más adelante en este tema.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Requiere el permiso ALTER en la base de datos.  
  
 Se requiere el permiso ALTER AVAILABILITY GROUP en el grupo de disponibilidad, el permiso CONTROL AVAILABILITY GROUP, el permiso ALTER ANY AVAILABILITY GROUP o el permiso CONTROL SERVER.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 **Para suspender una base de datos**  
  
1.  En el Explorador de objetos, conéctese a la instancia de servidor que hospeda la réplica de disponibilidad en la que desea suspender una base de datos y expanda el árbol. Para obtener más información, vea [Requisitos previos](#Prerequisites), anteriormente en este tema.  
  
2.  Expanda los nodos **Alta disponibilidad de AlwaysOn** y **Grupos de disponibilidad** .  
  
3.  Expanda el grupo de disponibilidad.  
  
4.  Expanda el nodo **Bases de datos de disponibilidad** , haga clic con el botón derecho en la base de datos y haga clic en **Suspender movimiento de datos**.  
  
5.  En el cuadro de diálogo **Suspender movimiento de datos** , haga clic en **Aceptar**.  
  
     El Explorador de objetos indica que la base de datos está suspendida mediante el cambio del icono de la base de datos para mostrar un indicador de detención.  
  
> [!NOTE]  
>  Para suspender bases de datos adicionales en esta ubicación de réplica, repita los pasos 4 y 5 para cada base de datos.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 **Para suspender una base de datos**  
  
1.  Conéctese a la instancia del servidor que hospeda la réplica cuya base de datos desea suspender. Para obtener más información, vea [Requisitos previos](#Prerequisites), anteriormente en este tema.  
  
2.  Suspenda la base de datos mediante la siguiente instrucción [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-set-hadr):  
  
     ALTER DATABASE *database_name* SET HADR SUSPEND  
  
##  <a name="PowerShellProcedure"></a> Usar PowerShell  
 **Para suspender una base de datos**  
  
1.  Cambie el directorio (`cd`) a la instancia de servidor que hospeda la réplica cuya base de datos desea suspender. Para obtener más información, vea [Requisitos previos](#Prerequisites), anteriormente en este tema.  
  
2.  Utilice el cmdlet `Suspend-SqlAvailabilityDatabase` para suspender el grupo de disponibilidad.  
  
     Por ejemplo, el siguiente comando suspende la sincronización de datos para la base de datos de disponibilidad `MyDb3` en el grupo de disponibilidad `MyAg` en la instancia del servidor denominada `Computer\Instance`.  
  
    ```  
    Suspend-SqlAvailabilityDatabase `   
    -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg\Databases\MyDb3  
    ```  
  
    > [!NOTE]  
    >  Para ver la sintaxis de un cmdlet, use el cmdlet `Get-Help` en el entorno de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Para más información, consulte [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
 **Para configurar y usar el proveedor de SQL Server PowerShell**  
  
-   [Proveedor de SQL Server PowerShell Provider](../../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="FollowUp"></a> Seguimiento: Evitar un registro de transacciones lleno  
 Normalmente, cuando se lleva a cabo un punto de comprobación automático en una base de datos, su registro de transacciones se trunca en dicho punto de comprobación después de la siguiente copia de seguridad del registro. Sin embargo, mientras una base de datos secundaria está suspendida, todas las entradas de registro actuales permanecen activas en la base de datos principal. Si el registro de transacciones se llena (bien porque alcanza su tamaño máximo o porque la instancia del servidor se queda sin espacio), la base de datos no puede realizar más actualizaciones.  
  
 Para evitar este problema, debe realizar una de las siguientes acciones:  
  
-   Agregar más espacio del registro para la base de datos principal.  
  
-   Reanudar la base de datos secundaria antes de que el registro se llene. Para obtener más información, vea [Reanudar una base de datos de disponibilidad &#40;SQL Server&#41;](resume-an-availability-database-sql-server.md).  
  
-   Quitar la base de datos secundaria. Para obtener más información, vea [Quitar una base de datos secundaria de un grupo de disponibilidad &#40;SQL Server&#41;](remove-a-secondary-database-from-an-availability-group-sql-server.md).  
  
 **Para solucionar problemas en un registro de transacciones lleno**  
  
-   [Solucionar problemas de un registro de transacciones lleno &#40;Error 9002 de SQL Server&#41;](../../../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Reanudar una base de datos de disponibilidad &#40;SQL Server&#41;](resume-an-availability-database-sql-server.md)  
  
## <a name="see-also"></a>Vea también  
 [Información general de grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Reanudar una base de datos de disponibilidad &#40;SQL Server&#41;](resume-an-availability-database-sql-server.md)  
  
  
