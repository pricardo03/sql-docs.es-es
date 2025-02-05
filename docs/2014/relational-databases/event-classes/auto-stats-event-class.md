---
title: Clase de eventos Auto Stats | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Auto Stats event class
ms.assetid: cd613fce-01e1-4d8f-86cc-7ffbf0759f9e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 354c2e39716dc0cfa215e4392945bf9aa5899da0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63012362"
---
# <a name="auto-stats-event-class"></a>Auto Stats [clase de eventos]
  La clase de evento **Auto Stats** indica que se ha producido una actualización automática del índice y de las estadísticas de las columnas.  
  
## <a name="auto-stats-event-class-data-columns"></a>Columnas de datos de la clase de evento Auto Stats  
  
|Nombre de columna de datos|Tipo de datos|Descripción|Identificador de columna|Filtrable|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|Nombre de la aplicación cliente que ha creado la conexión a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta columna se rellena con los valores que pasa la aplicación, en lugar de con el nombre que se muestra para el programa.|10|Sí|  
|**ClientProcessID**|**int**|Identificador que el equipo host asigna al proceso en el que se ejecuta la aplicación cliente. Esta columna de datos se rellena si el cliente proporciona el identificador de proceso del cliente.|9|Sí|  
|**DatabaseID**|**int**|Identificador de la base de datos especificada mediante la instrucción USE *database* o la base de datos predeterminada si no se emite la instrucción USE *database* para una determinada instancia. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] muestra el nombre de la base de datos si se captura la columna de datos **ServerName** en el seguimiento y el servidor está disponible. Determina el valor de una base de datos mediante la función DB_ID.|3|Sí|  
|**DatabaseName**|**nvarchar**|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|35|Sí|  
|**Duración**|**bigint**|Tiempo (en microsegundos) que tarda el evento.|13|Sí|  
|**EndTime**|**datetime**|Hora a la que finalizó el evento.|15|Sí|  
|**Error**|**int**|Número de error de un evento dado. Con frecuencia, es el número de error almacenado en la vista de catálogo **sys.messages** .|31|Sí|  
|**EventClass**|**int**|Tipo de evento = 58.|27|Sin|  
|**EventSequence**|**int**|Secuencia de un evento determinado de la solicitud.|51|Sin|  
|**EventSubClass**|**int**|Tipo de subclase de evento:<br /><br /> 1: Estadísticas creadas o actualizadas de forma sincrónica; **TextData** columna indica qué estadísticas y si se crea o se actualizaron.<br /><br /> 2: Actualización de estadísticas asincrónica; trabajo en cola.<br /><br /> 3: Actualización de estadísticas asincrónica; inicio del trabajo.<br /><br /> 4: Actualización de estadísticas asincrónica; trabajo completado.|21|Sí|  
|**GroupID**|**int**|Id. del grupo de carga de trabajo donde se activa el evento de Seguimiento de SQL.|66|Sí|  
|**HostName**|**nvarchar**|Nombre del equipo en el que se está ejecutando el cliente. Esta columna de datos se rellena si el cliente proporciona el nombre del host. Para determinar el nombre del host, utilice la función HOST_NAME.|8|Sí|  
|**IndexID**|**int**|Id. de la entrada del índice/estadísticas del objeto afectada por el evento. Para averiguar el identificador de índice de un objeto, use la columna **index_id** de la vista de catálogo **sys.indexes** .|24|Sí|  
|**IntegerData**|**int**|Número de colecciones de estadísticas que se actualizaron satisfactoriamente.|25|Sí|  
|**IntegerData2**|**int**|Número de secuencia de trabajo.|55|Sí|  
|**IsSystem**|**int**|Indica si el evento ha ocurrido en un proceso del sistema o en un proceso de usuario. 1 = sistema, 0 = usuario.|60|Sí|  
|**LoginName**|**nvarchar**|Nombre del inicio de sesión del usuario (inicio de sesión de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenciales de inicio de sesión de Windows en formato DOMINIO\nombreDeUsuario).|11|Sí|  
|**LoginSid**|**image**|SID (número de identificación de seguridad) del usuario que ha iniciado la sesión. Puede encontrar esta información en la vista de catálogo **sys.server_principals** . Cada SID es único para cada inicio de sesión en el servidor.|41|Sí|  
|**NTDomainName**|**nvarchar**|Dominio de Windows al que pertenece el usuario.|7|Sí|  
|**NTUserName**|**nvarchar**|Nombre del usuario de Windows.|6|Sí|  
|**ObjectID**|**int**|Identificador del objeto asignado por el sistema.|22|Sí|  
|**IdSolicitud**|**int**|Id. de la solicitud que contiene la instrucción.|49|Sí|  
|**ServerName**|**nvarchar**|Nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de la que se realiza un seguimiento.|26|No|  
|**SessionLoginName**|**nvarchar**|Nombre de inicio de sesión del usuario que originó la sesión. Por ejemplo, si se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando inicioDeSesión1 y ejecuta una instrucción como inicioDeSesión2, **SessionLoginName** muestra inicioDeSesión1 y **LoginName** muestra inicioDeSesión2. En esta columna se muestran los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y de Windows.|64|Sí|  
|**SPID**|**int**|Identificador de la sesión en la que se produjo el evento.|12|Sí|  
|**StartTime**|**datetime**|Hora a la que se inició el evento, si está disponible.|14|Sí|  
|**Correcto**|**int**|0 = error.<br /><br /> 1 = correcto.<br /><br /> 2 = omisión debida a la limitación del servidor (MSDE).|23|Sí|  
|**TextData**|**ntext**|El contenido de esta columna depende de si las estadísticas se actualizan de forma sincrónica (**EventSubClass** 1) o asincrónica (**EventSubClass** 2, 3 o 4):<br /><br /> 1: Las enumera estadísticas actualizadas o creadas<br /><br /> 2, 3 o 4: ES NULL; **IndexID** columna se rellena con el Id. de índice o estadística de las estadísticas actualizadas.|1|Sí|  
|**TransactionID**|**bigint**|Id. de la transacción asignado por el sistema.|4|Sí|  
|**Tipo**|**int**|Tipo de trabajo.|57|Sí|  
  
## <a name="see-also"></a>Vea también  
 [Eventos extendidos](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
