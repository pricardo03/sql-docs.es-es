---
title: Clase de eventos QN:Dynamics | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- event classes [SQL Server], QN:Dynamics
ms.assetid: 3c1ffa0c-c9e5-40a6-a26b-28339f60ebc3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: eb59abed8be5649d9258bce0f279222e4498b547
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63035761"
---
# <a name="qndynamics-event-class"></a>QN:Dynamics (clase de eventos)
  La clase de eventos QN:Dynamics ofrece información acerca de la actividad en segundo plano que realiza [!INCLUDE[ssDE](../../includes/ssde-md.md)] para admitir las notificaciones de consulta. En el [!INCLUDE[ssDE](../../includes/ssde-md.md)], un subproceso en segundo plano supervisa los tiempos de espera de las suscripciones, las suscripciones pendientes que se deben activar y la destrucción de tablas de parámetros.  
  
## <a name="qndynamics-event-class-data-columns"></a>Columnas de datos de la clase de eventosQN:Dynamics  
  
|Columna de datos|Tipo|Descripción|Número de columna|Filtrable|  
|-----------------|----------|-----------------|-------------------|----------------|  
|ApplicationName|`nvarchar`|Nombre de la aplicación cliente que ha creado la conexión a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta columna se rellena con los valores que pasa la aplicación, en lugar de con el nombre que se muestra para el programa.|10|Sí|  
|ClientProcessID|`int`|Id. que el equipo host asigna al proceso en el que se ejecuta la aplicación cliente. Esta columna de datos se rellena si el cliente proporciona su identificador de proceso.|9|Sí|  
|DatabaseID|`int`|Identificador de la base de datos especificada mediante la instrucción USE *database* o identificador de la base de datos predeterminada si no se ha emitido la instrucción USE *database*para una instancia determinada. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] muestra el nombre de la base de datos si se captura la columna de datos Server Name en el seguimiento y el servidor está disponible. Determina el valor de una base de datos mediante la función DB_ID.|3|Sí|  
|DatabaseName|`nvarchar`|Nombre de la base de datos en que se ejecuta la instrucción del usuario.|35|Sí|  
|EventClass|`int`|Tipo de evento = 202|27|Sin|  
|EventSequence|`int`|Número de secuencia de este evento.|51|No|  
|EventSubClass|`nvarchar`|Tipo de subclase de evento que proporciona más información acerca de cada clase de evento. Esta columna puede incluir los valores siguientes:<br /><br /> Ejecución iniciada de reloj: Indica que el subproceso en segundo plano el [!INCLUDE[ssDE](../../includes/ssde-md.md)] que las programaciones expiradas tablas de parámetros para ha iniciado la limpieza.<br /><br /> Reloj ejecución finalizada: Indica que el subproceso en segundo plano el [!INCLUDE[ssDE](../../includes/ssde-md.md)] que las programaciones expiradas tablas de parámetros para ha finalizado la limpieza.<br /><br /> Tarea de limpieza maestra iniciada: Indica cuándo empieza la limpieza (recolección de elementos) para eliminar los datos de suscripciones de notificación de consulta expiradas.<br /><br /> Tarea de limpieza maestro finalizó: Indica cuándo finaliza la limpieza (recolección de elementos) para eliminar los datos de suscripciones de notificación de consulta expiradas.<br /><br /> Se omitió la tarea de limpieza maestro: Indica que el [!INCLUDE[ssDE](../../includes/ssde-md.md)] no realizó la limpieza (recolección de elementos) para eliminar los datos de suscripción de notificaciones de consulta expiradas.|21|Sí|  
|GroupID|`int`|Id. del grupo de carga de trabajo donde se activa el evento de Seguimiento de SQL.|66|Sí|  
|HostName|`nvarchar`|Nombre del equipo en el que se está ejecutando el cliente. Esta columna de datos se rellena si el cliente proporciona el nombre del host. Para determinar el nombre del host, utilice la función HOST_NAME.|8|Sí|  
|IsSystem|`int`|Indica si el evento ha ocurrido en un proceso del sistema o en un proceso de usuario.<br /><br /> 0 = usuario<br /><br /> 1 = sistema|60|No|  
|LoginName|`nvarchar`|Nombre del inicio de sesión del usuario (inicio de sesión de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenciales de inicio de sesión de Windows en formato *DOMINIO\nombreDeUsuario*).|11|Sin|  
|LoginSID|`image`|SID (número de identificación de seguridad) del usuario que ha iniciado la sesión. Puede buscar esta información en la vista de catálogo sys.server_principals. Cada SID es único para cada inicio de sesión en el servidor.|41|Sí|  
|NTDomainName|`nvarchar`|Dominio de Windows al que pertenece el usuario.|7|Sí|  
|NTUserName|`nvarchar`|Nombre del usuario al que pertenece la conexión que generó este evento.|6|Sí|  
|IdSolicitud|`int`|Identificador de la solicitud que contiene la instrucción.|49|Sí|  
|ServerName|`nvarchar`|Nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de la que se realiza un seguimiento.|26|Sin|  
|SessionLoginName|`nvarchar`|Nombre de inicio de sesión del usuario que originó la sesión. Por ejemplo, si una aplicación se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando inicioDeSesión1 y ejecuta una instrucción como inicioDeSesión2, SessionLoginName muestra "inicioDeSesión1" y LoginName muestra "inicioDeSesión2". En esta columna se muestran los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y de Windows.|64|Sí|  
|SPID|`int`|Identificador de la sesión en la que se produjo el evento.|12|Sí|  
|StartTime|`datetime`|Hora a la que se inició el evento, si está disponible.|14|Sí|  
|TextData|`ntext`|Devuelve un documento XML que contiene información específica de este evento. Este documento se ajusta al esquema XML disponible en la página sobre el [esquema de eventos del analizador de notificaciones de consultas de SQL Server](https://go.microsoft.com/fwlink/?LinkId=63331)|1|Sí|  
  
  
