---
title: 'TM: Commit Tran Completed, clase de evento | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- 'TM: Commit Tran Completed event class'
ms.assetid: c102de15-f312-42a7-b52a-fc4879cc43aa
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 224bfd47c31c94e19935a97c6ed1cc726e233bb2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63061313"
---
# <a name="tm-commit-tran-completed-event-class"></a>TM: Clase de eventos Commit Tran Completed
  TM: Commit Tran Completed, clase de evento indica que ha completado una solicitud COMMIT TRANSACTION. La solicitud fue enviada desde el cliente mediante la interfaz de administración de transacciones. La columna EventSubClass indica si se reiniciará una nueva transacción una vez se confirme la transacción actual.  
  
## <a name="tm-commit-tran-completed-event-class-data-columns"></a>TM: Commit Tran completado columnas de datos de clase de eventos  
  
|Nombre de columna de datos|Tipo de datos|Descripción|Identificador de columna|Sí|  
|----------------------|---------------|-----------------|---------------|---------|  
|ApplicationName|`nvarchar`|Nombre de la aplicación cliente que ha creado la conexión a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta columna se rellena con los valores que pasa la aplicación, en lugar de con el nombre que se muestra para el programa.|10|Sí|  
|ClientProcessID|`int`|Identificador que el equipo host asigna al proceso en el que se ejecuta la aplicación cliente. Esta columna de datos se rellena si el cliente proporciona su identificador de proceso.|9|Sí|  
|DatabaseID|`int`|Identificador de la base de datos especificada mediante la instrucción USE database o la base de datos predeterminada si no se emite la instrucción USE database para una determinada instancia. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] muestra el nombre de la base de datos si se captura la columna de datos ServerName en el seguimiento y el servidor está disponible. Determina el valor de una base de datos mediante la función DB_ID.|3|Sí|  
|DatabaseName|`nvarchar`|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|35|Sí|  
|Error|`int`|Número de error de un evento dado. Con frecuencia, es el número de error almacenado en la vista de catálogo sys.messages.|31|Sí|  
|EventClass|`int`|Tipo de evento = 186.|27|Sin|  
|EventSequence|`int`|Secuencia de un evento determinado dentro de la solicitud.|51|Sin|  
|EventSubClass|`int`|Tipo de la subclase de eventos.<br /><br /> 1=Confirmar<br /><br /> 2=Confirmar y empezar|21|Sí|  
|GroupID|`int`|Id. del grupo de carga de trabajo donde se activa el evento de Seguimiento de SQL.|66|Sí|  
|HostName|`nvarchar`|Nombre del equipo en el que se está ejecutando el cliente. Esta columna de datos se rellena si el cliente proporciona el nombre del host. Para determinar el nombre del host, utilice la función HOST_NAME.|8|Sí|  
|IsSystem|`int`|Indica si el evento ha ocurrido en un proceso del sistema o en un proceso de usuario. 1 = sistema, 0 = usuario.|60|Sí|  
|LoginName|`nvarchar`|Nombre del inicio de sesión del usuario (inicio de sesión de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenciales de inicio de sesión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows con el formato DOMINIO\nombreDeUsuario).|11|Sí|  
|LoginSid|`image`|SID (número de identificación de seguridad) del usuario que ha iniciado la sesión. Puede buscar esta información en la vista de catálogo sys.server_principals. Cada SID es único para cada inicio de sesión en el servidor.|41|Sí|  
|NTDomainName|`nvarchar`|Dominio de Windows al que pertenece el usuario.|7|Sí|  
|NTUserName|`nvarchar`|Nombre del usuario de Windows.|6|Sí|  
|IdSolicitud|`int`|Identificador de la solicitud que contiene la instrucción.|49|Sí|  
|ServerName|`nvarchar`|Nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de la que se realiza un seguimiento.|26|Sin|  
|SessionLoginName|`nvarchar`|Nombre de inicio de sesión del usuario que originó la sesión. Por ejemplo, si se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando inicioDeSesión1 y ejecuta una instrucción como inicioDeSesión2, SessionLoginName muestra inicioDeSesión1 y LoginName muestra inicioDeSesión2. En esta columna se muestran los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y de Windows.|64|Sí|  
|SPID|`int`|Identificador de la sesión en la que se produjo el evento.|12|Sí|  
|StartTime|`datetime`|Hora a la que se inició el evento, si está disponible.|14|Sí|  
|Correcto|`int`|1 = correcto. 0 = error (por ejemplo, 1 significa que se ha comprobado un permiso correctamente y 0 significa que se ha producido un error en la comprobación).|23|Sí|  
|TextData|`ntext`|Valor de texto que depende de la clase de eventos capturada en el seguimiento.|1|Sí|  
|TransactionID|`bigint`|Id. de la transacción asignado por el sistema.|4|Sí|  
|XactSequence|`bigint`|Token que describe la transacción actual.|50|Sí|  
  
## <a name="see-also"></a>Vea también  
 [Eventos extendidos](../extended-events/extended-events.md)   
 [COMMIT TRANSACTION &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/commit-transaction-transact-sql)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
