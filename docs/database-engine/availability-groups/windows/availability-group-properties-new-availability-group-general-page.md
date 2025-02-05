---
title: 'Propiedades del grupo de disponibilidad: Nuevo grupo de disponibilidad (página General)'
titleSuffix: SQL Server
description: Una descripción de las distintas propiedades de la página "General" del "Asistente para nuevo grupo de disponibilidad" en SQL Server Management Studio.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.availabilitygroupproperties.general.f1
ms.assetid: 9af5379f-91b8-4729-9f75-4a80242a30e9
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a0f5e7c7ad7fe916b2203b2d1815e50602d30e2d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67934877"
---
# <a name="availability-group-properties-new-availability-group-general-page"></a>Propiedades del grupo de disponibilidad: Nuevo grupo de disponibilidad (página General)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tema se aplica a la pestaña **General** del cuadro de diálogo de **Nuevo grupo de disponibilidad** y el cuadro de diálogo de **Propiedades de grupo de disponibilidad** .  El cuadro de diálogo **Nuevo grupo de disponibilidad** permite crear un nuevo grupo de disponibilidad sin utilizar [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)]. El cuadro de diálogo **Propiedades de grupo de disponibilidad** permite ver y modificar la configuración de un grupo de disponibilidad existente.  
  
 **Para ver las propiedades del grupo de disponibilidad**  
  
-   [Ver las propiedades del grupo de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-properties-sql-server.md)  
  
-   [Usar el Panel AlwaysOn &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
## <a name="uielement-list"></a>Lista de UIElement  
 **Nombre del grupo de disponibilidad**  
 Nombre del grupo de disponibilidad. Es un nombre definido por el usuario que debe ser único dentro del clúster de conmutación por error de Windows Server (WSFC).  
  
## <a name="availability-databases"></a>Bases de datos de disponibilidad  
 **Database Name**  
 Nombre de una base de datos que se ha agregado al grupo de disponibilidad.  
  
 **Agregar**  
 Haga clic para agregar una base de datos al grupo de disponibilidad.  
  
 **Quitar**  
 Haga clic para quitar una base de datos seleccionada del grupo de disponibilidad.  
  
## <a name="availability-replicas"></a>Réplicas de disponibilidad  
 **Instancia del servidor**  
 Nombre de servidor de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospeda esta réplica y, para una instancia no predeterminada, su nombre de instancia.  
  
 **Rol**  
 **Principal**  
 Actualmente la réplica principal.  
  
 **Secundario**  
 Actualmente una réplica secundaria.  
  
 **Resolver**  
 Actualmente el rol de la réplica están en proceso de resolverse al rol principal o al rol secundario.  
  
 **Modo de disponibilidad**  
 Modo de disponibilidad de la réplica, que puede ser alguno de los siguientes:  
  
 **Confirmación asincrónica**  
 La réplica principal puede confirmar transacciones sin esperar a que la réplica secundaria escriba el registro en disco.  
  
 **Confirmación sincrónica**  
 La réplica principal espera para confirmar una determinada transacción hasta que la réplica secundaria escribe la transacción en el disco.  
  
 Para obtener más información, vea [Modos de disponibilidad &#40;grupos de disponibilidad AlwaysOn&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md).  
  
 **Modo de conmutación por error**  
 Modo de conmutación por error de la réplica, que puede ser uno de los siguientes:  
  
 **Automático**  
 Conmutación por error automática. La réplica es un destino de las conmutaciones por error automáticas. Esto solo se admite si el modo de disponibilidad se establece en confirmación sincrónica.  
  
 **Manual**  
 Conmutación por error manual. La réplica solo puede ser objeto de conmutación por error manual por parte del administrador de base de datos.  
  
 **Conexiones el en rol principal**  
 El tipo de conexiones de cliente admitidas cuando la réplica posee el rol principal.  
  
 **Permitir todas las conexiones**  
 Se permiten todas las conexiones con las bases de datos de la réplica principal. Esta es la configuración predeterminada.  
  
 **Permitir conexiones de lectura o escritura**  
 No se permiten las conexiones en las que la propiedad de conexión Application Intent esté establecida en **ReadOnly** . Cuando la propiedad Application Intent está establecida en **ReadWrite** o no tiene ningún valor, se permite la conexión. Para obtener más información sobre propiedad de conexión Application Intent, vea [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 **Secundario legible**  
 Si una réplica de disponibilidad que está realizando el rol secundario (es decir, una réplica secundaria) puede aceptar conexiones de clientes; puede tener uno de los valores siguientes:  
  
 **No**  
 No se permiten conexiones directas a las bases de datos secundarias de esta réplica. No están disponibles para acceso de lectura. Esta es la configuración predeterminada.  
  
 **Solo intento de lectura**  
 Únicamente se permiten conexiones directas de solo lectura a las bases de datos secundarias de esta réplica. Todas las bases de datos secundarias están disponibles para acceso de lectura.  
  
 **Sí**  
 Se permiten todas las conexiones a las bases de datos secundarias de esta réplica, pero solo para acceso de lectura. Todas las bases de datos secundarias están disponibles para acceso de lectura.  
  
 **Tiempo de espera de sesión (segundos)**  
 El número de segundos del período de tiempo de espera de la sesión en esta réplica.  
  
 **Dirección URL del extremo**  
 La dirección URL del extremo. Para obtener más información sobre el formato de estas direcciones URL, vea [Especificar la dirección URL del punto de conexión al agregar o modificar una réplica de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md).  
  
 **Agregar**  
 Haga clic para agregar una réplica secundaria al grupo de disponibilidad.  
  
 **Quitar**  
 Haga clic para quitar una réplica secundaria del grupo de disponibilidad.  
  
## <a name="see-also"></a>Consulte también  
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
