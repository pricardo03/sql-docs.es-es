---
title: Ayuda del Administrador de configuración de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/01/2018
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Configuration Manager, help
ms.assetid: 6e909911-39a6-469b-b22a-3afdfd08a30b
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: fa579e072ffdddc70e10d3ad1e9a205840374aee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68024089"
---
# <a name="sql-server-configuration-manager-help"></a>Ayuda del Administrador de configuración de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  Use el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para configurar los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y la conectividad de red. Para crear o administrar objetos de base de datos, configurar la seguridad y escribir consultas [!INCLUDE[tsql](../../includes/tsql-md.md)] , use la herramienta [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obtener más información acerca de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], vea los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  

 > [!TIP]
 > Si necesita configurar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en Linux, use la herramienta **MSSQL-conf** . Para obtener más información, consulte [configuración de SQL Server en Linux con la herramienta MSSQL-conf](../../linux/sql-server-linux-configure-mssql-conf.md).

 En esta sección se incluyen los temas de la Ayuda F1 para los cuadros de diálogo del Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] El Administrador de configuración no puede configurar versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
## <a name="services"></a>Services  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] administra los servicios relacionados con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Aunque muchas de estas tareas se pueden llevar a cabo utilizando el cuadro de diálogo Servicios de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, es importante tener en cuenta que el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] realiza operaciones adicionales en los servicios que administra, como aplicar los permisos correctos cuando se cambia la cuenta de servicio. Si se usa el cuadro de diálogo normal de los servicios de Windows para configurar cualquiera de los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , pueden producirse errores de funcionamiento en el servicio.  
  
 Utilice el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para las siguientes tareas relacionadas con los servicios:  
  
-   Iniciar, detener y pausar los servicios  
  
-   Configurar los servicios para que se inicien de forma automática o manual, para deshabilitarlos o para cambiar otras opciones de los servicios  
  
-   Cambiar las contraseñas de las cuentas utilizadas por los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Iniciar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con marcas de seguimiento (parámetros de línea de comandos)  
  
-   Ver las propiedades de los servicios  
  
## <a name="sql-server-network-configuration"></a>Configuración de red de SQL Server  
 Utilice el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para llevar a cabo las siguientes tareas relacionadas con los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en este equipo:  
  
-   Habilitar o deshabilitar un protocolo de red de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Configurar un protocolo de red de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
> [!NOTE]  
>  Para obtener un tutorial breve sobre cómo configurar protocolos y conectar al [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], vea [Tutorial: Introducción al motor de base de datos](../../relational-databases/tutorial-getting-started-with-the-database-engine.md).  
  
## <a name="sql-server-native-client-configuration"></a>Configuración de SQL Server Native Client  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se conectan a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la biblioteca de red de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Utilice el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para llevar a cabo las siguientes tareas relacionadas con las aplicaciones cliente en este equipo:  
  
-   Para las aplicaciones cliente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en este equipo, especificar el orden de los protocolos al conectarse a instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Configurar los protocolos de conexión de cliente.  
  
-   Para las aplicaciones cliente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , crear alias para las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], de forma que los clientes puedan conectarse usando una cadena de conexión personalizada.  
  
 Para obtener más información acerca de cada una de estas tareas, vea la Ayuda F1 de cada tarea.  
  
#### <a name="to-open-sql-server-configuration-manager"></a>Para abrir el Administrador de configuración de SQL Server  
  
-   En el menú **Inicio** , seleccione **Todos los programas**, **Microsoft SQL Server** (versión), **Herramientas de configuración**y, después, haga clic en **Administrador de configuración de SQL Server**.  
  
  
 **Para tener acceso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager mediante [!INCLUDE[win8](../../includes/win8-md.md)]**  
  
 Como el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es un complemento del programa [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console y no un programa independiente, el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no aparece como una aplicación cuando se ejecuta [!INCLUDE[win8](../../includes/win8-md.md)]. Para abrir [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, en el botón de acceso **Buscar**, en **Aplicaciones**, escriba **SQLServerManager12.msc** (para [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]) o **SQLServerManager11.msc** (para [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) y pulse **Entrar**.  
  

## <a name="see-also"></a>Consulte también  
 [Servicios de SQL Server](../../tools/configuration-manager/sql-server-services.md)   
 [Configuración de red de SQL Server](../../tools/configuration-manager/sql-server-network-configuration.md)   
 [Configuración de SQL Native Client 11.0](../../tools/configuration-manager/sql-native-client-11-0-configuration.md)   
 [Elegir un protocolo de red](https://msdn.microsoft.com/library/6565fb7d-b076-4447-be90-e10d0dec359a)  
  
  
