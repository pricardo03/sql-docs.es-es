---
title: Clase de eventos Lock:Released | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Released event class
ms.assetid: a150c300-72fa-4231-8f41-f1abd550a429
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cf04a73d2ecc100ae5e9b41b5807aa25b05ba32a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63023845"
---
# <a name="lockreleased-event-class"></a>Lock:Released (clase de eventos)
  La clase de eventos Lock:Released indica que se ha liberado un bloqueo en un recurso, por ejemplo una página.  
  
 Las clases de eventos Lock:Acquired y Lock:Released se pueden utilizar para supervisar cuándo se bloquean objetos, el tipo de bloqueos obtenidos y cuánto tiempo se han mantenido éstos. Los bloqueos mantenidos durante largos períodos pueden causar problemas de contención y se deben investigar. Por ejemplo, una aplicación puede estar adquiriendo bloqueos en filas de una tabla y esperar después a que se produzca una entrada del usuario. Puesto que la introducción de datos puede tardar bastante tiempo, los bloqueos pueden bloquear a otros usuarios. En tal caso, es necesario volver a diseñar la aplicación para que realice solicitudes de bloqueo solo cuando sea preciso y no solicite que el una entrada del usuario cuando se han adquirido bloqueos.  
  
## <a name="lock-released-event-class-data-columns"></a>Bloqueo: Columnas de datos de clase de eventos de lanzamiento  
  
|Nombre de columna de datos|Tipo de datos|Descripción|Identificador de columna|Filtrable|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|Nombre de la aplicación cliente que ha creado la conexión a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta columna se rellena con los valores que pasa la aplicación, en lugar de con el nombre que se muestra para el programa.|10|Sí|  
|BinaryData|`image`|Identificador del recurso de bloqueo.|2|Sí|  
|ClientProcessID|`int`|Identificador que el equipo host asigna al proceso en el que se ejecuta la aplicación cliente. Esta columna de datos se rellena si el cliente proporciona el identificador de proceso del cliente.|9|Sí|  
|DatabaseID|`int`|Identificador de la base de datos en la que se ha liberado el bloqueo. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] muestra el nombre de la base de datos si se captura la columna de datos ServerName en el seguimiento y el servidor está disponible. Determina el valor de una base de datos mediante la función DB_ID.|3|Sí|  
|EventClass|`int`|Tipo de evento = 23.|27|Sin|  
|EventSequence|`int`|Secuencia de un evento determinado de la solicitud.|51|No|  
|GroupID|`int`|Id. del grupo de carga de trabajo donde se activa el evento de Seguimiento de SQL.|66|Sí|  
|HostName|`nvarchar`|Nombre del equipo en el que se está ejecutando el cliente. Esta columna de datos se rellena si el cliente proporciona el nombre del host. Para determinar el nombre del host, utilice la función HOST_NAME.|8|Sí|  
|IntegerData2|`int`|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|55|Sí|  
|IsSystem|`int`|Indica si el evento ha ocurrido en un proceso del sistema o en un proceso de usuario. 1 = sistema, 0 = usuario.|60|Sí|  
|LoginName|`nvarchar`|Nombre del inicio de sesión del usuario (inicio de sesión de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenciales de inicio de sesión de Windows en formato DOMINIO\nombreDeUsuario).|11|Sí|  
|LoginSid|`image`|SID (número de identificación de seguridad) del usuario que ha iniciado la sesión. Puede buscar esta información en la vista de catálogo sys.server_principals. Cada SID es único para cada inicio de sesión en el servidor.|41|Sí|  
|Modo|`int`|Modo resultante tras liberar el bloqueo.<br /><br /> 0=NULL: Compatible con los demás modos de bloqueo (LCK_M_NL)<br /><br /> 1=Bloqueo Estabilidad del esquema (LCK_M_SCH_S)<br /><br /> 2=Bloqueo Modificación del esquema (LCK_M_SCH_M)<br /><br /> 3=Bloqueo Compartido (LCK_M_S)<br /><br /> 4=Bloqueo Actualizar (LCK_M_U)<br /><br /> 5=Bloqueo Exclusivo (LCK_M_X)<br /><br /> 6=Bloqueo Intención compartida (LCK_M_IS)<br /><br /> 7=Bloqueo Actualizar intención (LCK_M_IU)<br /><br /> 8=Bloqueo Intención exclusiva (LCK_M_IX)<br /><br /> 9=Actualizar intención compartida (LCK_M_SIU)<br /><br /> 10=Intención compartida exclusiva (LCK_M_SIX)<br /><br /> 11=Actualizar intención exclusiva (LCK_M_UIX)<br /><br /> 12=Bloqueo Actualización masiva (LCK_M_BU)<br /><br /> 13=Intervalo de claves compartido/compartido (LCK_M_RS_S)<br /><br /> 14=Intervalo de claves compartido/actualización (LCK_M_RS_U)<br /><br /> 15=Intervalo de claves de inserción NULL (LCK_M_RI_NL)<br /><br /> 16=Intervalo de claves de inserción compartido (LCK_M_RI_S)<br /><br /> 17=Intervalo de claves de inserción de actualización (LCK_M_RI_U)<br /><br /> 18=Intervalo de claves de inserción exclusivo (LCK_M_RI_X)<br /><br /> 19=Intervalo de claves exclusivo compartido (LCK_M_RX_S)<br /><br /> 20=Intervalo de claves exclusivo de actualización (LCK_M_RX_U)<br /><br /> 21=Intervalo de claves exclusivo exclusivo (LCK_M_RX_X)|32|Sí|  
|NTDomainName|`nvarchar`|Dominio de Windows al que pertenece el usuario.|7|Sí|  
|NTUserName|`nvarchar`|Nombre del usuario de Windows.|6|Sí|  
|ObjectID|`int`|Id. asignado por el sistema del objeto que se ha liberado, si está disponible y es aplicable.|22|Sí|  
|ObjectID2|`bigint`|Id. del objeto o entidad relacionado, si está disponible y es aplicable.|56|Sí|  
|OwnerID|`int`|1=TRANSACTION<br /><br /> 2=CURSOR<br /><br /> 3=SESSION<br /><br /> 4=SHARED_TRANSACTION_WORKSPACE<br /><br /> 5=EXCLUSIVE_TRANSACTION_WORKSPACE|58|Sí|  
|IdSolicitud|`int`|Identificador de la solicitud que contiene la instrucción.|49|Sí|  
|ServerName|`nvarchar`|Nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de la que se realiza un seguimiento.|26|No|  
|SessionLoginName|`nvarchar`|Nombre de inicio de sesión del usuario que originó la sesión. Por ejemplo, si se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando inicioDeSesión1 y ejecuta una instrucción como inicioDeSesión2, SessionLoginName muestra inicioDeSesión1 y LoginName muestra inicioDeSesión2. En esta columna se muestran los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y de Windows.|64|Sí|  
|SPID|`int`|Identificador de la sesión en la que se produjo el evento.|12|Sí|  
|StartTime|`datetime`|Hora a la que se inició el evento, si está disponible.|14|Sí|  
|TextData|`ntext`|Valor de texto que depende de la clase de eventos capturada en el seguimiento.|1|Sí|  
|TransactionID|`bigint`|Id. de la transacción asignado por el sistema.|4|Sí|  
|Tipo|`int`|1=NULL_RESOURCE<br /><br /> 2=DATABASE<br /><br /> 3=FILE<br /><br /> 5=OBJECT<br /><br /> 6=PAGE<br /><br /> 7=KEY<br /><br /> 8=EXTENT<br /><br /> 9=RID<br /><br /> 10=APPLICATION<br /><br /> 11=METADATA<br /><br /> 12=AUTONAMEDB<br /><br /> 13=HOBT<br /><br /> 14=ALLOCATION_UNIT|57|Sí|  
  
## <a name="see-also"></a>Vea también  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Lock:Acquired (clase de eventos)](lock-acquired-event-class.md)   
 [sys.dm_tran_locks &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql)  
  
  
