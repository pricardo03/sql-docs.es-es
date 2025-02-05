---
title: Configurar protocolos de cliente | Microsoft Docs
ms.custom: ''
ms.date: 07/27/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- default protocols
- network protocols [SQL Server], client configuration
- TCP/IP [SQL Server], client protocols
- disabling client protocols
- ordering protocols [SQL Server]
- protocols [SQL Server], order for client computers
- configure client protocols
- client protocols [SQL Server]
- protocols [SQL Server], client configuration
- default protocols, client
ms.assetid: 3dfa2702-ba65-43b4-a777-6727846e133a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 2fa898451638503b2f91c97026158e7331a25e90
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68012812"
---
# <a name="configure-client-protocols"></a>configurar protocolos de cliente
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se describe cómo configurar los protocolos de cliente utilizados por aplicaciones cliente de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite comunicaciones de cliente con el protocolo de red TCP/IP y el protocolo de canalizaciones con nombre. El protocolo de memoria compartida también está disponible si el cliente se está conectando a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] en el mismo equipo. Hay varios métodos habituales para seleccionar el protocolo.  
  
-   Configure todas las aplicaciones cliente para que usen el mismo protocolo de red estableciendo el orden de protocolos en el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Configure una sola aplicación cliente para que use otro protocolo de red creando un alias. Para obtener más información, vea [Crear o eliminar un alias de servidor para que lo utilice un cliente &#40;Administrador de configuración de SQL Server&#41;](../../database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client.md).  
  
-   Algunas aplicaciones cliente, como sqlcmd.exe, pueden especificar el protocolo como parte de la cadena de conexión. Para obtener más información, vea [Conectarse al motor de base de datos con sqlcmd](../../relational-databases/scripting/sqlcmd-connect-to-the-database-engine.md).  
  
##  <a name="SSMSProcedure"></a> Usar el Administrador de configuración de SQL Server  
  
###  <a name="EnableDisable"></a> Para habilitar o deshabilitar un protocolo de cliente  
  
1.  En el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], expanda **Configuración de SQL Server Native Client**, haga clic con el botón derecho en **Protocolos de cliente** y, luego, haga clic en **Propiedades**.  
  
2.  Haga clic en un protocolo en el cuadro **Protocolos deshabilitados** y, a continuación, haga clic en **Habilitar**para habilitar el protocolo.  
  
3.  Haga clic en un protocolo en el cuadro **Protocolos habilitados** y, a continuación, haga clic en **Deshabilitar**para deshabilitar el protocolo.  
  
###  <a name="ChangeDefault"></a> Para cambiar el protocolo o el orden de protocolos predeterminado de los equipos cliente  
  
1.  En el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], expanda **Configuración de SQL Server Native Client**, haga clic con el botón derecho en **Protocolos de cliente** y, luego, haga clic en **Propiedades**.  
  
2.  En el cuadro **Protocolos habilitados** , haga clic en **Subir** o **Bajar**para cambiar el orden en el que los protocolos se utilizan cuando se intenta la conexión a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El protocolo superior del cuadro **Protocolos habilitados** es el protocolo predeterminado.  
  
    > [!IMPORTANT]  
    >  El Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea entradas del Registro para las configuraciones de alias del servidor y la biblioteca de red de cliente predeterminada. Sin embargo, la aplicación no instala ni las bibliotecas de red de cliente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ni los protocolos de red. Las bibliotecas de red de cliente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se instalan durante la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; los protocolos de red se instalan como parte del programa de instalación de Microsoft Windows (o desde **Redes** en el **Panel de control**). Es posible que un protocolo de red específico no esté disponible como parte del programa de instalación de Windows. Para obtener más información acerca de cómo instalar estos protocolos de red, consulte la documentación del fabricante.  
  
###  <a name="Configure"></a> Para configurar el uso de TCP/IP en un cliente  
  
1.  En el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], expanda **Configuración de SQL Server Native Client**, haga clic con el botón derecho en **Protocolos de cliente** y, luego, haga clic en **Propiedades**.  
  
2.  En el cuadro **Protocolos habilitados** , haga clic en las flechas arriba o abajo para cambiar el orden en que se prueban los protocolos al intentar conectarse a SQL Server. El protocolo superior del cuadro **Protocolos habilitados** es el protocolo predeterminado.  
  
 El protocolo de memoria compartida se habilita de forma independiente activando la casilla **Habilitar el protocolo de memoria compartida** .  
  
## <a name="see-also"></a>Consulte también  
 [Establecer la opción de configuración del servidor Tiempo de espera de inicio de sesión remoto](../../database-engine/configure-windows/configure-the-remote-login-timeout-server-configuration-option.md)  
  
  
