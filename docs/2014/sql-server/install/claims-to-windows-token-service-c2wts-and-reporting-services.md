---
title: Notificaciones del servicio de Token de Windows (C2WTS) y Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/25/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- c2wts.exe.config
- SharePoint mode
- C2WTS
- WSS_WPG
ms.assetid: 4d380509-deed-4b4b-a9c1-a9134cc40641
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: e08be032df493913cc6cebf5ae29d583f26c86ba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66096549"
---
# <a name="claims-to-windows-token-service-c2wts-and-reporting-services"></a>Notificaciones del servicio de token de Windows (C2WTS) y Reporting Services
  Las notificaciones de SharePoint al servicio de Token de Windows (c2WTS) se requiere con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] el modo de SharePoint si desea usar la autenticación de windows para orígenes de datos que están fuera de la granja de SharePoint. Esto es cierto incluso si el usuario accede a los orígenes de datos con la autenticación de Windows porque la comunicación entre el servicio front-end web (WFE) y el servicio compartido de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se realizará siempre con autenticación de notificaciones.  
  
 c2WTS es necesario aunque los orígenes de datos estén en el mismo equipo que el servicio compartido. Sin embargo, en este escenario no es necesaria la delegación restringida.  
  
 Los tokens creados por c2WTS funcionarán solo con delegación restringida (limitaciones a servicios concretos) y la opción de configuración "Usar cualquier protocolo de autenticación". Como se indicaba anteriormente, si los orígenes de datos están en el mismo equipo que el servicio compartido, la delegación restringida no es necesaria.  
  
 Si en su entorno se usa la delegación limitada de Kerberos, el servicio SharePoint Server y los orígenes de datos externos deben residir en el mismo dominio de Windows. Cualquier servicio que use Notificaciones del servicio de token de Windows (c2WTS) debe emplear la delegación **restringida** de Kerberos para permitir que c2WTS use la transición del protocolo Kerberos para traducir las notificaciones en credenciales de Windows. Estos requisitos son verdaderos para todos los servicios compartidos de SharePoint. Para obtener más información, consulte [información general de la autenticación Kerberos para productos de Microsoft SharePoint 2010 (https://technet.microsoft.com/library/gg502594.aspx)](https://technet.microsoft.com/library/gg502594.aspx).  
  
 El procedimiento se resume en este tema.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013 &#124; SharePoint 2010|  
  
## <a name="prerequisites"></a>Requisitos previos  
  
> [!NOTE]  
>  Nota: Algunos de los pasos de configuración pueden cambiar, o pueden no funcionar en algunas topologías de granja. Por ejemplo, una instalación de un solo servidor no admite los servicios c2WTS de Windows Identity Foundation, por lo que las notificaciones a los escenarios de delegación de token de Windows no son posibles con esta configuración de granja.  
  
### <a name="basic-steps-needed-to-configure-c2wts"></a>Pasos básicos necesarios para configurar c2WTS  
  
1.  Configure la cuenta de servicio c2WTS. Agregue la cuenta de servicio al grupo de administradores local en cada servidor de aplicaciones ejecuta c2WTS. Además, compruebe que la cuenta tiene los siguientes derechos de directiva de seguridad local:  
  
    -   Actuar como parte del sistema operativo  
  
    -   Suplantar un cliente después de autenticación  
  
    -   Iniciar sesión como servicio  
  
     La cuenta que utilice para c2WTS también debe configurarse para la delegación restringida con transición de protocolo y necesita permisos para delegar a los servicios se requiere comunicación (es decir, motor SQL Server, SQL Server Analysis Services). Para configurar la delegación puede utilizar el complemento de usuarios de Active Directory y el equipo.  
  
    1.  Haga clic con el botón secundario en cada cuenta de servicio y abra el cuadro de diálogo de propiedades. En el cuadro de diálogo, haga clic en la pestaña **Delegación** .  
  
        > [!NOTE]  
        >  Nota: la pestaña de delegación solo está visible si el objeto tiene asignado un SPN. c2WTS no requiere un SPN en la cuenta de c2WTS pero, sin un SPN, la pestaña **Delegación** no estará visible. Una manera alternativa de configurar la delegación restringida es utilizar una herramienta como **ADSIEdit**.  
  
    2.  Las opciones de configuración clave en la pestaña de delegación son las siguientes:  
  
        -   Seleccionar "Confiar en este usuario para la delegación solo a servicios especificados"  
  
        -   Seleccione "Usar cualquier protocolo de autenticación"  
  
         Para obtener más información, consulte la sección "configurar la delegación restringida de Kerberos para equipos y cuentas de servicio" de las notas siguientes [configurar la autenticación Kerberos para productos de SharePoint 2010 y SQL Server 2008 R2](http://blogs.technet.com/b/tothesharepoint/archive/2010/07/22/whitepaper-configuring-kerberos-authentication-for-sharepoint-2010-and-sql-server-2008-r2-products.aspx)  
  
2.  Configurar "AllowedCallers" de c2WTS  
  
     c2WTS requiere que las identidades de los 'autores de llamadas' explícitamente enumeradas en el archivo de configuración **c2wtshost.exe.config**. c2WTS no acepta solicitudes de todos los usuarios autenticados en el sistema a menos que esté configurado para ello. En este caso el "autor de la llamada" es el grupo de Windows WSS_WPG. El archivo c2wtshost.exe.confi se guarda en la ubicación siguiente:  
  
     **\Program Files\Windows identity Foundation\v3.5\c2wtshost.exe.config**  
  
     A continuación se muestra un ejemplo del archivo de configuración:  
  
    ```  
    <configuration>  
      <windowsTokenService>  
        <!--  
            By default no callers are allowed to use the Windows Identity Foundation Claims To NT Token Service.  
            Add the identities you wish to allow below.  
          -->  
        <allowedCallers>  
          <clear/>  
          <add value="WSS_WPG" />  
        </allowedCallers>  
      </windowsTokenService>  
    </configuration>  
    ```  
  
3.  Iniciar el servicio c2WTS del sistema operativo:  
  
    1.  Configure el servicio para usar la cuenta de servicio que configuró en el paso anterior.  
  
    2.  Cambie el tipo de inicio a "**automática**" e inicie el servicio.  
  
4.  Iniciar las "Notificaciones al servicio de Token de Windows" de SharePoint: Inicie las Notificaciones del servicio de token de Windows a través de la Administración central de SharePoint en la página **Administrar servicios en el servidor**. El servicio se debe iniciar en el servidor que realizará la acción. Por ejemplo, si tiene un servidor que es un servidor web front-end (WFE) y otro servidor que es un servidor de aplicaciones que tiene la ejecución del servicio compartido de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , solo tiene que iniciar c2WTS en el servidor de aplicaciones. c2WTS no es necesario en el servidor web front-end (WFE).  
  
## <a name="see-also"></a>Vea también  
 [Notificaciones al servicio de Token de Windows (c2WTS) (información general https://msdn.microsoft.com/library/ee517278.aspx)](https://msdn.microsoft.com/library/ee517278.aspx)   
 [Introducción a la autenticación de Kerberos para productos de Microsoft SharePoint 2010 (https://technet.microsoft.com/library/gg502594.aspx)](https://technet.microsoft.com/library/gg502594.aspx)  
  
  
